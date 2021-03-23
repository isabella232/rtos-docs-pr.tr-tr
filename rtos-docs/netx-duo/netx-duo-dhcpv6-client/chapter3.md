---
title: Bölüm 3-Azure RTOS NetX Duo DHCPv6 yapılandırma seçenekleri
description: Azure RTOS NetX Duo DHCPv6 'yi oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e5396b1c04581b5f79d337462368c4718ba9bb16
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826087"
---
# <a name="chapter-3---azure-rtos-netx-duo-dhcpv6-configuration-options"></a><span data-ttu-id="58e87-103">Bölüm 3-Azure RTOS NetX Duo DHCPv6 yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="58e87-103">Chapter 3 - Azure RTOS NetX Duo DHCPv6 configuration options</span></span>

<span data-ttu-id="58e87-104">Azure RTOS NetX Duo DHCPv6 'yi oluşturmaya yönelik birkaç yapılandırma seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="58e87-104">There are several configuration options for building Azure RTOS NetX Duo DHCPv6.</span></span> <span data-ttu-id="58e87-105">Aşağıdaki listede her biri ayrıntılı açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="58e87-105">The following list describes each in detail:</span></span>  
  
  
- <span data-ttu-id="58e87-106">**NX_DHCPV6_THREAD_PRIORITY** Istemci iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="58e87-106">**NX_DHCPV6_THREAD_PRIORITY** Priority of the Client thread.</span></span> <span data-ttu-id="58e87-107">Varsayılan olarak, bu değer Istemci iş parçacığının öncelik 2 ' de çalıştığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="58e87-107">By   default, this value specifies that   the Client thread runs at priority   2.</span></span>

- <span data-ttu-id="58e87-108">**NX_DHCPV6_MUTEX_WAIT** DHCPv6 Istemci mutex 'i üzerinde özel bir kilit elde etmek için zaman aşımı seçeneği.</span><span class="sxs-lookup"><span data-stu-id="58e87-108">**NX_DHCPV6_MUTEX_WAIT** Time out option for obtaining an exclusive lock on a DHCPv6 Client mutex.</span></span> <span data-ttu-id="58e87-109">Varsayılan değer TX_WAIT_FOREVER.</span><span class="sxs-lookup"><span data-stu-id="58e87-109">The default value is TX_WAIT_FOREVER.</span></span>

- <span data-ttu-id="58e87-110">**NX_DHCPV6_TICKS_PER_SECOND** Onay işareti sayısının saniyeye oranı.</span><span class="sxs-lookup"><span data-stu-id="58e87-110">**NX_DHCPV6_TICKS_PER_SECOND** Ratio of ticks to seconds.</span></span> <span data-ttu-id="58e87-111">Bu, işlemciye bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="58e87-111">This is processor dependent.</span></span> <span data-ttu-id="58e87-112">Varsayılan değer 100’dür.</span><span class="sxs-lookup"><span data-stu-id="58e87-112">The default value is 100.</span></span>

- <span data-ttu-id="58e87-113">**NX_DHCPV6_IP_LIFETIME_TIMER_INTERVAL**  Saniye cinsinden IP yaşam süresinin Istemciye geçerli IP adresinin atandığı sürenin uzunluğunu güncelleştiren zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="58e87-113">**NX_DHCPV6_IP_LIFETIME_TIMER_INTERVAL**  Time interval in seconds at which the IP lifetime timer updates the length of time the current IP address has been assigned to the Client.</span></span> <span data-ttu-id="58e87-114">Varsayılan olarak, bu değer 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="58e87-114">By default, this value is 1.</span></span>

- <span data-ttu-id="58e87-115">**NX_DHCPV6_SESSION_TIMER_INTERVAL**  Saniye cinsinden oturum süreölçerinin, Istemcinin sunucu ile iletişim kurduğu süre uzunluğunu güncelleştirme süresini güncelleştiren zaman aralığı.</span><span class="sxs-lookup"><span data-stu-id="58e87-115">**NX_DHCPV6_SESSION_TIMER_INTERVAL**  Time interval in seconds at which the session timer updates the length of time the Client has been in session communicating with the Server.</span></span> <span data-ttu-id="58e87-116">Varsayılan olarak, bu değer 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="58e87-116">By default, this value is 1.</span></span>

- <span data-ttu-id="58e87-117">**NX_DHCPV6_MAX_IA_ADDRESS** Istemci kaydına eklenebilecek en fazla IA adresi sayısı.</span><span class="sxs-lookup"><span data-stu-id="58e87-117">**NX_DHCPV6_MAX_IA_ADDRESS** The maximum number of IA addresses that can be added to the Client record.</span></span> <span data-ttu-id="58e87-118">Varsayılan değer 1’dir.</span><span class="sxs-lookup"><span data-stu-id="58e87-118">The default value is 1.</span></span> 

- <span data-ttu-id="58e87-119">**NX_DHCPV6_NUM_DNS_SERVERS** İstemci kaydına depolanacak DNS sunucularının sayısı.</span><span class="sxs-lookup"><span data-stu-id="58e87-119">**NX_DHCPV6_NUM_DNS_SERVERS** Number of DNS servers to store to the client record.</span></span> <span data-ttu-id="58e87-120">Varsayılan değer 2 ' dir.</span><span class="sxs-lookup"><span data-stu-id="58e87-120">The default value is 2.</span></span>

- <span data-ttu-id="58e87-121">**NX_DHCPV6_NUM_TIME_SERVERS** İstemci kaydına depolanacak zaman sunucularının sayısı.</span><span class="sxs-lookup"><span data-stu-id="58e87-121">**NX_DHCPV6_NUM_TIME_SERVERS** Number of time servers to store to the client record.</span></span> <span data-ttu-id="58e87-122">Varsayılan değer 1’dir.</span><span class="sxs-lookup"><span data-stu-id="58e87-122">The default value is 1.</span></span>

- <span data-ttu-id="58e87-123">**NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE**  İstemcinin ağ etki alanı adını tutmak için Istemci kaydındaki arabelleğin boyutu.</span><span class="sxs-lookup"><span data-stu-id="58e87-123">**NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE**  Size of the buffer in the Client record to hold the client’s network domain name.</span></span> <span data-ttu-id="58e87-124">Varsayılan değer 30’dur.</span><span class="sxs-lookup"><span data-stu-id="58e87-124">The default value is 30.</span></span>

- <span data-ttu-id="58e87-125">**NX_DHCPV6_TIME_ZONE_BUFFER_SIZE**  İstemcinin saat dilimini tutmak için Istemci kaydındaki arabelleğin boyutu.</span><span class="sxs-lookup"><span data-stu-id="58e87-125">**NX_DHCPV6_TIME_ZONE_BUFFER_SIZE**  Size of the buffer in the Client record to hold the Client’s time zone.</span></span> <span data-ttu-id="58e87-126">Varsayılan değer 10'dur.</span><span class="sxs-lookup"><span data-stu-id="58e87-126">The default value is 10.</span></span>

- <span data-ttu-id="58e87-127">**NX_DHCPV6_MAX_MESSAGE_SIZE** Sunucu yanıtında durum iletisi seçeneğini tutmak için Istemci kaydındaki arabelleğin boyutu.</span><span class="sxs-lookup"><span data-stu-id="58e87-127">**NX_DHCPV6_MAX_MESSAGE_SIZE** Size of the buffer in the Client record to hold the option status message in a Server reply.</span></span> <span data-ttu-id="58e87-128">Varsayılan değer 100 bayttır.</span><span class="sxs-lookup"><span data-stu-id="58e87-128">The default value is 100 bytes.</span></span>

- <span data-ttu-id="58e87-129">**NX_DHCPV6_PACKET_TIME_OUT** Istemci paket havuzundan bir paket ayırmak için saniye cinsinden zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="58e87-129">**NX_DHCPV6_PACKET_TIME_OUT** Time out in seconds for allocating a packet from the Client packet pool.</span></span> <span data-ttu-id="58e87-130">Varsayılan değer 3 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="58e87-130">The default value is 3 seconds.</span></span>

- <span data-ttu-id="58e87-131">**NX_DHCPV6_TYPE_OF_SERVICE** Bu, DHCPv6 Istemci yuvasından UDP paket iletimi için hizmet türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="58e87-131">**NX_DHCPV6_TYPE_OF_SERVICE** This defines the type of service for UDP packet transmission from the DHCPv6 Client socket.</span></span> <span data-ttu-id="58e87-132">Varsayılan değer **NX_IP_NORMAL**.</span><span class="sxs-lookup"><span data-stu-id="58e87-132">The default value is **NX_IP_NORMAL**.</span></span>

- <span data-ttu-id="58e87-133">**NX_DHCPV6_TIME_TO_LIVE** Paket atılmadan önce bir ağ yönlendiricisinin Istemci paketinin iletme sayısı.</span><span class="sxs-lookup"><span data-stu-id="58e87-133">**NX_DHCPV6_TIME_TO_LIVE** The number of times a Client packet is forwarded by a network router before the packet is discarded.</span></span> <span data-ttu-id="58e87-134">Varsayılan değer 0x80 ' dır.</span><span class="sxs-lookup"><span data-stu-id="58e87-134">The default value is 0x80.</span></span>

- <span data-ttu-id="58e87-135">**NX_DHCPV6_QUEUE_DEPTH** NetX Duo paketleri atmadan önce Istemci UDP yuvası alma kuyruğunda tutulacak paket sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="58e87-135">**NX_DHCPV6_QUEUE_DEPTH** Specifies the number of packets to keep in the Client UDP socket receive queue before NetX Duo discards packets.</span></span> <span data-ttu-id="58e87-136">Varsayılan değer 5 ' tir.</span><span class="sxs-lookup"><span data-stu-id="58e87-136">The default value is 5.</span></span>

## <a name="dhcpv6-message-transmission"></a><span data-ttu-id="58e87-137">DHCPv6 Ileti Iletimi</span><span class="sxs-lookup"><span data-stu-id="58e87-137">DHCPv6 Message Transmission</span></span>

<span data-ttu-id="58e87-138">DHCPv6 ileti iletiminde parametreleri ayarlamak için DHCPv6 Istemci seçenekleri kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="58e87-138">There are a set of DHCPv6 Client options for setting parameters on DHCPv6 message transmission.</span></span> <span data-ttu-id="58e87-139">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="58e87-139">These are:</span></span> 

  - <span data-ttu-id="58e87-140">ilk zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="58e87-140">initial timeout</span></span>

  - <span data-ttu-id="58e87-141">ilk iletimde maksimum gecikme</span><span class="sxs-lookup"><span data-stu-id="58e87-141">maximum delay on the first transmission</span></span>

  - <span data-ttu-id="58e87-142">maksimum yeniden iletim zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="58e87-142">maximum retransmission timeout</span></span> 

  - <span data-ttu-id="58e87-143">maksimum yeniden iletim sayısı</span><span class="sxs-lookup"><span data-stu-id="58e87-143">maximum number of retransmissions</span></span> 

  - <span data-ttu-id="58e87-144">Sunucu yanıtı için beklenecek en uzun süre</span><span class="sxs-lookup"><span data-stu-id="58e87-144">maximum duration to wait for server response</span></span>

<span data-ttu-id="58e87-145">Bu parametreler, DHCPv6 Istemci iletilerinin her biri için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="58e87-145">These parameters apply to each of the DHCPv6 Client messages:</span></span>

- <span data-ttu-id="58e87-146">Istek</span><span class="sxs-lookup"><span data-stu-id="58e87-146">SOLICIT</span></span>

- <span data-ttu-id="58e87-147">ISTEYEN</span><span class="sxs-lookup"><span data-stu-id="58e87-147">REQUEST</span></span>

- <span data-ttu-id="58e87-148">YENILEY</span><span class="sxs-lookup"><span data-stu-id="58e87-148">RENEW</span></span>

- <span data-ttu-id="58e87-149">REBIND</span><span class="sxs-lookup"><span data-stu-id="58e87-149">REBIND</span></span>

- <span data-ttu-id="58e87-150">Yayın</span><span class="sxs-lookup"><span data-stu-id="58e87-150">RELEASE</span></span>

- <span data-ttu-id="58e87-151">Reddet</span><span class="sxs-lookup"><span data-stu-id="58e87-151">DECLINE</span></span>

- <span data-ttu-id="58e87-152">GÖRÜNDÜĞÜNÜ</span><span class="sxs-lookup"><span data-stu-id="58e87-152">CONFIRM</span></span>

- <span data-ttu-id="58e87-153">YAPıLANDıRı</span><span class="sxs-lookup"><span data-stu-id="58e87-153">INFORM</span></span>

<span data-ttu-id="58e87-154">Aşağıda, bu yapılandırılabilir seçeneklerin ve bunların varsayılan listesi verilmiştir</span><span class="sxs-lookup"><span data-stu-id="58e87-154">The following is a complete list of these configurable options and their default</span></span> 

<span data-ttu-id="58e87-155">values:</span><span class="sxs-lookup"><span data-stu-id="58e87-155">values:</span></span>

```C
NX_DHCPV6_FIRST_SOL_MAX_DELAY                   (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_INIT_SOL_TRANSMISSION_TIMEOUT         (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_SOL_RETRANSMISSION_TIMEOUT        (120 *
                                                NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_SOL_RETRANSMISSION_COUNT          0
NX_DHCPV6_MAX_SOL_RETRANSMISSION_DURATION       0

NX_DHCPV6_INIT_REQ_TRANSMISSION_TIMEOUT         (1 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_REQ_RETRANSMISSION_TIMEOUT        (30 * NX_DHCPV6_TICKS_PER_SECOND) 
NX_DHCPV6_MAX_REQ_RETRANSMISSION_COUNT          10
NX_DHCPV6_MAX_REQ_RETRANSMISSION_DURATION       0

NX_DHCPV6_INIT_RENEW_TRANSMISSION_TIMEOUT       (10*NX_DHCPV6_TICKS_PER_SECOND)     
NX_DHCPV6_MAX_RENEW_RETRANSMISSION_TIMEOUT      (600*   
                                                NX_DHCPV6_TICKS_PER_SECOND)  
NX_DHCPV6_MAX_RENEW_RETRANSMISSION_COUNT        0

NX_DHCPV6_INIT_REBIND_TRANSMISSION_TIMEOUT      (10*NX_DHCPV6_TICKS_PER_SECOND)     
NX_DHCPV6_MAX_REBIND_RETRANSMISSION_TIMEOUT     (600*  
                                                NX_DHCPV6_TICKS_PER_SECOND)  
NX_DHCPV6_MAX_REBIND_RETRANSMISSION_COUNT       0 

NX_DHCPV6_INIT_RELEASE_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_TIMEOUT    0 
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_COUNT      5  
NX_DHCPV6_MAX_RELEASE_RETRANSMISSION_DURATION   0

NX_DHCPV6_INIT_DECLINE_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_TIMEOUT    0
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_COUNT      5  
NX_DHCPV6_MAX_DECLINE_RETRANSMISSION_DURATION   0
NX_DHCPV6_FIRST_CONFIRM_MAX_DELAY               (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_INIT_CONFIRM_TRANSMISSION_TIMEOUT     (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_TIMEOUT    (4*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_COUNT      0  
NX_DHCPV6_MAX_CONFIRM_RETRANSMISSION_DURATION   10

NX_DHCPV6_FIRST_INFORM_MAX_DELAY                (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_INIT_INFORM_TRANSMISSION_TIMEOUT      (1*NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_TIMEOUT     (120*   
                                                NX_DHCPV6_TICKS_PER_SECOND)
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_COUNT       0 
NX_DHCPV6_MAX_INFORM_RETRANSMISSION_DURATION    0
```

<span data-ttu-id="58e87-156">Yeniden aktarım zaman aşımında sınır olmaması için ileti yeniden aktarım sayısını 0 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="58e87-156">For no limit on a retransmission timeout, set the message retransmission count to 0.</span></span> <span data-ttu-id="58e87-157">DHCPv6 Istemci iletisinin kaç kez yeniden denendiğinden (yeniden denemeler), ileti yeniden aktarım sayısını 0 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="58e87-157">For no limit on the number of times a DHCPv6 Client message is retransmitted (retries), set the message retransmission count to 0.</span></span>

> [!NOTE]
> <span data-ttu-id="58e87-158">Zaman aşımı süresi veya yeniden deneme sayısı ne olursa olsun, geçerli bir IPv6 adresi yaşam süresi dolduğunda, IP Adresi tablosundan kaldırılır ve artık Istemci tarafından kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="58e87-158">Regardless of length of timeout or number of retries, when an IPv6 address valid lifetime expires, it is removed from the IP address table and can no longer be used by the Client.</span></span> <span data-ttu-id="58e87-159">NetX Duo DHCPv6 Istemcisi, yeni bir IPv6 adresi isteyen Istem iletilerini otomatik olarak göndermeye başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="58e87-159">The NetX Duo DHCPv6 Client will automatically begin sending SOLICIT messages requesting a new IPv6 address.</span></span>