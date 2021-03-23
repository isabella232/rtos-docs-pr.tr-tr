---
title: Bölüm 1-Azure RTOS NetX DHCP Istemcisine giriş
description: NetX 'te, uygulamanın IP adresi nx_ip_create hizmet çağrısına sağlanan parametrelerden biridir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 44eb764c84a15a1bc96cf94bcbc8f81be7b41eef
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826806"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-dhcp-client"></a><span data-ttu-id="7e609-103">Bölüm 1-Azure RTOS NetX DHCP Istemcisine giriş</span><span class="sxs-lookup"><span data-stu-id="7e609-103">Chapter 1 - Introduction to Azure RTOS NetX DHCP Client</span></span>

<span data-ttu-id="7e609-104">NetX 'te, uygulamanın IP adresi *nx_ip_create* hizmet çağrısına sağlanan parametrelerden biridir.</span><span class="sxs-lookup"><span data-stu-id="7e609-104">In NetX, the application’s IP address is one of the supplied parameters to the *nx_ip_create* service call.</span></span> <span data-ttu-id="7e609-105">IP adresi, statik olarak veya Kullanıcı Yapılandırması aracılığıyla uygulama tarafından biliniyorsa, IP adresi sağlamak sorun vermez.</span><span class="sxs-lookup"><span data-stu-id="7e609-105">Supplying the IP address poses no problem if the IP address is known to the application, either statically or through user configuration.</span></span> <span data-ttu-id="7e609-106">Ancak, uygulamanın IP adresinin ne olduğunu bilmediğini veya ilgilenmediğini bir örnek vardır.</span><span class="sxs-lookup"><span data-stu-id="7e609-106">However, there are some instances where the application doesn’t know or care what its IP address is.</span></span> <span data-ttu-id="7e609-107">Bu gibi durumlarda, *nx_ip_create* işlevine sıfır bir IP adresi verilmelidir ve Azure RTOS DHCP istemci protokolü, dinamik olarak bir IP adresi elde etmek için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7e609-107">In such situations, a zero IP address should be supplied to the *nx_ip_create* function and the Azure RTOS DHCP Client protocol should be used to dynamically obtain an IP address.</span></span>

## <a name="dynamic-ip-address-assignment"></a><span data-ttu-id="7e609-108">Dinamik IP adresi ataması</span><span class="sxs-lookup"><span data-stu-id="7e609-108">Dynamic IP Address Assignment</span></span>

<span data-ttu-id="7e609-109">Ağdan dinamik bir IP adresi elde etmek için kullanılan temel hizmet, ters adres çözümleme protokolüdür (RARP).</span><span class="sxs-lookup"><span data-stu-id="7e609-109">The basic service used to obtain a dynamic IP address from the network is the Reverse Address Resolution Protocol (RARP).</span></span> <span data-ttu-id="7e609-110">Bu protokol ARP ile benzerdir, ancak başka bir ağ düğümünün MAC adresini bulmak yerine kendisi için bir IP adresi almak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7e609-110">This protocol is similar to ARP, except it is designed to obtain an IP address for itself instead of finding the MAC address for another network node.</span></span> <span data-ttu-id="7e609-111">Düşük düzey RARP iletisi yerel ağda yayınlanır ve ağ üzerindeki bir sunucunun, dinamik olarak ayrılan IP adresi içeren bir RARP yanıtıyla yanıt vermesi için bir sorumluluğudur.</span><span class="sxs-lookup"><span data-stu-id="7e609-111">The low-level RARP message is broadcast on the local network and it is the responsibility of a server on the network to respond with an RARP response, which contains a dynamically allocated IP address.</span></span>

<span data-ttu-id="7e609-112">RARP, IP adreslerinin dinamik ayırması için bir hizmet sunmakla birlikte, birkaç eksiklikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="7e609-112">Although RARP provides a service for dynamic allocation of IP addresses, it has several shortcomings.</span></span> <span data-ttu-id="7e609-113">En çok kullanılan eksiklik, RARP 'nin yalnızca IP adresinin dinamik olarak ayrılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e609-113">The most glaring deficiency is that RARP only provides dynamic allocation of the IP address.</span></span> <span data-ttu-id="7e609-114">Çoğu durumda, bir cihazın ağa doğru bir şekilde katılması için daha fazla bilgi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7e609-114">In most situations, more information is necessary in order for a device to properly participate on a network.</span></span> <span data-ttu-id="7e609-115">Bir IP adresine ek olarak, çoğu cihaz ağ maskesine ve ağ geçidi IP adresine ihtiyaç duyar.</span><span class="sxs-lookup"><span data-stu-id="7e609-115">In addition to an IP address, most devices need the network mask and the gateway IP address.</span></span> <span data-ttu-id="7e609-116">Bir DNS sunucusunun IP adresi ve diğer ağ bilgileri de gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="7e609-116">The IP address of a DNS server and other network information may also be needed.</span></span> <span data-ttu-id="7e609-117">RARP 'nin bu bilgileri sağlama yeteneği yoktur.</span><span class="sxs-lookup"><span data-stu-id="7e609-117">RARP does not have the ability to provide this information.</span></span>

## <a name="rarp-alternatives"></a><span data-ttu-id="7e609-118">RARP alternatifleri</span><span class="sxs-lookup"><span data-stu-id="7e609-118">RARP Alternatives</span></span>

<span data-ttu-id="7e609-119">RARP 'nin eksiklikleri aşılabilmesi için, araştırmacılar Önyükleme Protokolü (BOOTP) adlı daha kapsamlı bir IP adresi ayırma mekanizması geliştirmiştir.</span><span class="sxs-lookup"><span data-stu-id="7e609-119">In order to overcome the deficiencies of RARP, researchers developed a more comprehensive IP address allocation mechanism called the Bootstrap Protocol (BOOTP).</span></span> <span data-ttu-id="7e609-120">Bu protokol, IP adresi dinamik olarak tahsis etme ve ayrıca ek önemli ağ bilgileri sağlama yeteneğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7e609-120">This protocol has the ability to dynamically allocate an IP address and also provide additional important network information.</span></span> <span data-ttu-id="7e609-121">Ancak, BOOTP 'nin statik ağ yapılandırmalarına yönelik olarak tasarlanma dezavantajı vardır.</span><span class="sxs-lookup"><span data-stu-id="7e609-121">However, BOOTP has the drawback of being designed for static network configurations.</span></span> <span data-ttu-id="7e609-122">Hızlı veya otomatik adres atamaya izin vermez.</span><span class="sxs-lookup"><span data-stu-id="7e609-122">It does not allow for quick or automated address assignment.</span></span>

<span data-ttu-id="7e609-123">Dinamik ana bilgisayar Yapılandırma Protokolü (DHCP) son derece yararlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7e609-123">This is where the Dynamic Host Configuration Protocol (DHCP) is extremely useful.</span></span> <span data-ttu-id="7e609-124">DHCP, belirli bir süre boyunca istemciye bir IP adresi "kiralamaya" kadar, tam otomatik IP sunucusu ayırması ve tamamen dinamik IP adresi ayırmayı içerecek şekilde, BOOTP 'nin temel işlevlerini genişletmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7e609-124">DHCP is designed to extend the basic functionality of BOOTP to include completely automated IP server allocation and completely dynamic IP address allocation through “leasing” an IP address to a client for a specified period of time.</span></span> <span data-ttu-id="7e609-125">DHCP, IP adreslerini BOOTP gibi statik bir şekilde ayırmak üzere de yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7e609-125">DHCP can also be configured to allocate IP addresses in a static manner like BOOTP.</span></span>

## <a name="dhcp-messages"></a><span data-ttu-id="7e609-126">DHCP Iletileri</span><span class="sxs-lookup"><span data-stu-id="7e609-126">DHCP Messages</span></span>

<span data-ttu-id="7e609-127">DHCP, BOOTP işlevselliğini önemli ölçüde iyileştirse de DHCP, BOOTP ile aynı ileti biçimini kullanır ve BOOTP ile aynı satıcı seçeneklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="7e609-127">Although DHCP greatly enhances the functionality of BOOTP, DHCP uses the same message format as BOOTP and supports the same vendor options as BOOTP.</span></span> <span data-ttu-id="7e609-128">DHCP, işlevini gerçekleştirmek için aşağıdaki şekilde DHCP 'ye özgü yedi seçenek sunar:</span><span class="sxs-lookup"><span data-stu-id="7e609-128">In order to perform its function, DHCP introduces seven new DHCP-specific options, as follows:</span></span>

- <span data-ttu-id="7e609-129">BUL (1) (DHCP Istemcisi tarafından gönderilen)</span><span class="sxs-lookup"><span data-stu-id="7e609-129">DISCOVER (1) (sent by DHCP Client)</span></span>

- <span data-ttu-id="7e609-130">TEKLIF (2) (DHCP sunucusu tarafından gönderilen)</span><span class="sxs-lookup"><span data-stu-id="7e609-130">OFFER (2) (sent by DHCP Server)</span></span>

- <span data-ttu-id="7e609-131">Istek (3) (DHCP Istemcisi tarafından gönderilen)</span><span class="sxs-lookup"><span data-stu-id="7e609-131">REQUEST (3) (sent by DHCP Client)</span></span>

- <span data-ttu-id="7e609-132">Reddet (4) (DHCP Istemcisi tarafından gönderilen)</span><span class="sxs-lookup"><span data-stu-id="7e609-132">DECLINE (4) (sent by DHCP Client)</span></span>

- <span data-ttu-id="7e609-133">ACK (5) (DHCP sunucusu tarafından gönderilen)</span><span class="sxs-lookup"><span data-stu-id="7e609-133">ACK (5) (sent by DHCP Server)</span></span>

- <span data-ttu-id="7e609-134">NACK (6) (DHCP sunucusu tarafından gönderilen)</span><span class="sxs-lookup"><span data-stu-id="7e609-134">NACK (6) (sent by DHCP Server)</span></span>

- <span data-ttu-id="7e609-135">Yayın (7) (DHCP Istemcisi tarafından gönderilen)</span><span class="sxs-lookup"><span data-stu-id="7e609-135">RELEASE (7) (sent by DHCP Client)</span></span>

- <span data-ttu-id="7e609-136">BILDIR (8) (DHCP Istemcisi tarafından gönderilir)</span><span class="sxs-lookup"><span data-stu-id="7e609-136">INFORM (8) (sent by DHCP Client)</span></span>

- <span data-ttu-id="7e609-137">FORCERENEW (9) (DHCP Istemcisi tarafından gönderilen)</span><span class="sxs-lookup"><span data-stu-id="7e609-137">FORCERENEW (9) (sent by DHCP Client)</span></span>

## <a name="dhcp-communication"></a><span data-ttu-id="7e609-138">DHCP Iletişimi</span><span class="sxs-lookup"><span data-stu-id="7e609-138">DHCP Communication</span></span>

<span data-ttu-id="7e609-139">DHCP, istek ve alan yanıtlarını göndermek için UDP protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="7e609-139">DHCP utilizes the UDP protocol to send requests and field responses.</span></span> <span data-ttu-id="7e609-140">IP adresine sahip olmadan önce, DHCP bilgilerini taşıyan UDP iletileri, 255.255.255.255 IP yayını adresi kullanılarak gönderilir ve alınır.</span><span class="sxs-lookup"><span data-stu-id="7e609-140">Prior to having an IP address, UDP messages carrying the DHCP information are sent and received by utilizing the IP broadcast address of 255.255.255.255.</span></span>

## <a name="dhcp-client-state-machine"></a><span data-ttu-id="7e609-141">DHCP Istemci durumu makinesi</span><span class="sxs-lookup"><span data-stu-id="7e609-141">DHCP Client State Machine</span></span>

<span data-ttu-id="7e609-142">DHCP Istemcisi, bir durum makinesi olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7e609-142">The DHCP Client is implemented as a state machine.</span></span> <span data-ttu-id="7e609-143">Durum makinesi, *nx_dhcp_create* işleme sırasında oluşturulan BIR iç DHCP iş parçacığı tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="7e609-143">The state machine is processed by an internal DHCP thread that is created during *nx_dhcp_create* processing.</span></span> <span data-ttu-id="7e609-144">DHCP Istemcisinin ana durumları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7e609-144">The main states of DHCP Client are as follows:</span></span>


- <span data-ttu-id="7e609-145">**NX_DHCP_STATE_BOOT** Önceki bir IP adresi ile başlama</span><span class="sxs-lookup"><span data-stu-id="7e609-145">**NX_DHCP_STATE_BOOT** Starting with a previous IP address</span></span>

- <span data-ttu-id="7e609-146">**NX_DHCP_STATE_INIT** Önceki IP adresi değeri olmadan başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="7e609-146">**NX_DHCP_STATE_INIT** Starting with no previous   IP address value</span></span>

- <span data-ttu-id="7e609-147">**NX_DHCP_STATE_SELECTING** Herhangi bir DHCP sunucusundan yanıt bekleniyor</span><span class="sxs-lookup"><span data-stu-id="7e609-147">**NX_DHCP_STATE_SELECTING** Waiting for a response from any DHCP server</span></span>

- <span data-ttu-id="7e609-148">**NX_DHCP_STATE_REQUESTING** DHCP sunucusu tanımlandı, IP adresi isteği gönderildi</span><span class="sxs-lookup"><span data-stu-id="7e609-148">**NX_DHCP_STATE_REQUESTING** DHCP Server identified, IP address request sent</span></span>

- <span data-ttu-id="7e609-149">**NX_DHCP_STATE_BOUND** DHCP IP adresi kirası oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="7e609-149">**NX_DHCP_STATE_BOUND** DHCP IP Address lease established</span></span>

- <span data-ttu-id="7e609-150">**NX_DHCP_STATE_RENEWING** DHCP IP adresi kira yenileme süresi geçti, yenileme istendi</span><span class="sxs-lookup"><span data-stu-id="7e609-150">**NX_DHCP_STATE_RENEWING** DHCP IP Address lease renewal time elapsed, renewal requested</span></span>

- <span data-ttu-id="7e609-151">**NX_DHCP_STATE_REBINDING** DHCP IP adresi kira yeniden bağlama süresi geçti, yenileme istendi</span><span class="sxs-lookup"><span data-stu-id="7e609-151">**NX_DHCP_STATE_REBINDING** DHCP IP Address lease rebind time elapsed, renewal requested</span></span>

- <span data-ttu-id="7e609-152">**NX_DHCP_STATE_FORCERENEW** DHCP IP adresi kirası oluşturuldu, sunucu tarafından yenilemeyi zorla (Şu anda desteklenmiyor) veya çağıran uygulama tarafından nx_dhcp_force_renew</span><span class="sxs-lookup"><span data-stu-id="7e609-152">**NX_DHCP_STATE_FORCERENEW** DHCP IP Address lease established, force renewal by server (currently not supported) or by the application calling nx_dhcp_force_renew</span></span>

- <span data-ttu-id="7e609-153">**NX_DHCP_STATE_ADDRESS_PROBING** DHCP IP adresi yoklama, IP adresi çakışmasını algılamak için ARP araştırması gönderin.</span><span class="sxs-lookup"><span data-stu-id="7e609-153">**NX_DHCP_STATE_ADDRESS_PROBING** DHCP IP Address probing, send the ARP probe to detect IP address conflict.</span></span>

## <a name="dhcp-client-multiple-interface-support"></a><span data-ttu-id="7e609-154">DHCP Istemcisi birden çok arabirim desteği</span><span class="sxs-lookup"><span data-stu-id="7e609-154">DHCP Client Multiple Interface Support</span></span>

<span data-ttu-id="7e609-155">DHCP Istemcisi daha önce yalnızca tek bir ağ arabiriminde çalışmak üzere uygulandı.</span><span class="sxs-lookup"><span data-stu-id="7e609-155">The DHCP Client was previously implemented to run on only a single network interface.</span></span> <span data-ttu-id="7e609-156">DHCP Istemcisinin birincil arabirimde çalışması için varsayılan davranış (ve yine de aynıdır).</span><span class="sxs-lookup"><span data-stu-id="7e609-156">The default behavior was (and still is) for the DHCP Client to run on the primary interface.</span></span> <span data-ttu-id="7e609-157">*Nx_dhcp_set_interface_index* çağırarak, uygulama birincil arabirim yerine ikincil bir ağ arabiriminde DHCP çalıştırabilir (ve yine de olabilir).</span><span class="sxs-lookup"><span data-stu-id="7e609-157">By calling *nx_dhcp_set_interface_index*, the application could (and still can) run DHCP on a secondary network interface instead of the primary interface.</span></span>

<span data-ttu-id="7e609-158">Artık paralel olarak birden çok arabirimde çalışan DHCP 'yi desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="7e609-158">It now supports DHCP running on multiple interfaces in parallel.</span></span> <span data-ttu-id="7e609-159">DHCP Istemcisini birden fazla fiziksel arabirimde aynı anda çalıştırma hakkında ayrıntılı bilgi için, aynı anda **birden fazla arabirimde DHCP istemcisi** ' ne bakın.</span><span class="sxs-lookup"><span data-stu-id="7e609-159">See **DHCP Client on Multiple Interfaces Simultaneously** in Chapter Two for specific details how to run DHCP Client on more than one physical interface simultaneously.</span></span>

## <a name="dhcp-user-request"></a><span data-ttu-id="7e609-160">DHCP Kullanıcı Isteği</span><span class="sxs-lookup"><span data-stu-id="7e609-160">DHCP User Request</span></span>

<span data-ttu-id="7e609-161">DHCP sunucusu bir IP adresi verdiğinde, DHCP istemci işlemesi, *nx_dhcp_user_option_request* hizmetini kullanarak ek parametreler isteyebilir (tek seferde).</span><span class="sxs-lookup"><span data-stu-id="7e609-161">Once the DHCP server grants an IP address, the DHCP client processing can request additional parameters — one at a time — by using the *nx_dhcp_user_option_request* service.</span></span>

## <a name="dhcp-client-socket-queue"></a><span data-ttu-id="7e609-162">DHCP Istemci yuva kuyruğu</span><span class="sxs-lookup"><span data-stu-id="7e609-162">DHCP Client Socket Queue</span></span> 

<span data-ttu-id="7e609-163">DHCP Istemcisi, sunucunun kendisine yanıt vermesini beklerken, diğer DHCP Istemcilerine yönelik DHCP sunucularından gelen yayın paketlerini otomatik olarak kendi yuva alma sırasından temizler.</span><span class="sxs-lookup"><span data-stu-id="7e609-163">The DHCP Client automatically clears broadcast packets from DHCP Servers intended for other DHCP Clients from its socket receive queue while waiting for Server to respond to itself.</span></span> <span data-ttu-id="7e609-164">Meşgul bir ağda, Bunun gerçekleşmemesi, Istemci için amaçlanan paketlerin bırakılmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7e609-164">In a busy network, not doing so could cause packets intended for the Client to be dropped.</span></span>

## <a name="dhcp-rfcs"></a><span data-ttu-id="7e609-165">DHCP RFC 'Leri</span><span class="sxs-lookup"><span data-stu-id="7e609-165">DHCP RFCs</span></span>

<span data-ttu-id="7e609-166">NetX DHCP, RFC2132, RFC2131 ve ilgili RFC 'lerle uyumludur.</span><span class="sxs-lookup"><span data-stu-id="7e609-166">NetX DHCP is compliant with RFC2132, RFC2131, and related RFCs.</span></span>

