---
title: Bölüm 8-Azure RTOS NetX izleme olayları
description: Bu bölümde, Azure RTOS NetX olaylarının açıklaması yer almaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: ce355d86d7db0b7e259ae58e306d990277b77a8f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828354"
---
# <a name="chapter-8---azure-rtos-netx-trace-events"></a><span data-ttu-id="37aae-103">Bölüm 8-Azure RTOS NetX izleme olayları</span><span class="sxs-lookup"><span data-stu-id="37aae-103">Chapter 8 - Azure RTOS NetX trace events</span></span>

<span data-ttu-id="37aae-104">Bu bölümde, Azure RTOS NetX olaylarının açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="37aae-104">This chapter contains a description of the Azure RTOS NetX events.</span></span> 

## <a name="list-of-events-and-icons"></a><span data-ttu-id="37aae-105">Olay ve simgelerin listesi</span><span class="sxs-lookup"><span data-stu-id="37aae-105">List of Events and Icons</span></span>

<span data-ttu-id="37aae-106">Aşağıda, TraceX tarafından görünen NetX olaylarının bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="37aae-106">The following is a list of NetX events displayed by TraceX.</span></span>

| <span data-ttu-id="37aae-107">Simge</span><span class="sxs-lookup"><span data-stu-id="37aae-107">Icon</span></span>                                           | <span data-ttu-id="37aae-108">Anlamı</span><span class="sxs-lookup"><span data-stu-id="37aae-108">Meaning</span></span>                 |
| -------------------------------- | ------------------------------------- |
| ![İç A R P Isteği alma simgesi](./media/user-guide/netx-events/image1.png)    | <span data-ttu-id="37aae-110">İç ARP Isteği alma</span><span class="sxs-lookup"><span data-stu-id="37aae-110">Internal ARP Request Receive</span></span> |
| ![Dahili A R P Isteği gönderme simgesi](./media/user-guide/netx-events/image2.png)    | <span data-ttu-id="37aae-112">İç ARP Isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-112">Internal ARP Request Send</span></span> |
| ![Dahili A R P yanıtı alma simgesi](./media/user-guide/netx-events/image3.png)    | <span data-ttu-id="37aae-114">İç ARP yanıtı alma</span><span class="sxs-lookup"><span data-stu-id="37aae-114">Internal ARP Response Receive</span></span> |
| ![Dahili A R P yanıtı gönderme simgesi](./media/user-guide/netx-events/image4.png)    | <span data-ttu-id="37aae-116">İç ARP yanıtı gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-116">Internal ARP Response Send</span></span> |
| ![İç ı C M P alma simgesi](./media/user-guide/netx-events/image5.png)    | <span data-ttu-id="37aae-118">İç ıCMP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-118">Internal ICMP Receive</span></span> |
| ![İç ı C M P Gönder simgesi](./media/user-guide/netx-events/image6.png)    | <span data-ttu-id="37aae-120">İç ıCMP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-120">Internal ICMP Send</span></span> |
| ![İç NetX ı G M P alma simgesi](./media/user-guide/netx-events/image7.png)    | <span data-ttu-id="37aae-122">İç NetX ıGMP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-122">Internal NetX IGMP Receive</span></span> |
| ![İç ı P alma simgesi](./media/user-guide/netx-events/image8.png)    | <span data-ttu-id="37aae-124">İç IP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-124">Internal IP Receive</span></span> |
| ![İç ı P Gönder simgesi](./media/user-guide/netx-events/image9.png)    | <span data-ttu-id="37aae-126">İç IP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-126">Internal IP Send</span></span> |
| ![İç T C P veri alma simgesi](./media/user-guide/netx-events/image10.png)    | <span data-ttu-id="37aae-128">İç TCP veri alma</span><span class="sxs-lookup"><span data-stu-id="37aae-128">Internal TCP Data Receive</span></span> |
| ![İç T C P veri gönderme simgesi](./media/user-guide/netx-events/image11.png)    | <span data-ttu-id="37aae-130">İç TCP veri gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-130">Internal TCP Data Send</span></span> |
| ![İç T C P FIN alma simgesi](./media/user-guide/netx-events/image12.png)    | <span data-ttu-id="37aae-132">İç TCP FIN alma</span><span class="sxs-lookup"><span data-stu-id="37aae-132">Internal TCP FIN Receive</span></span> |
| ![İç T C P F ı N Gönder simgesi](./media/user-guide/netx-events/image13.png)    | <span data-ttu-id="37aae-134">İç TCP FIN gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-134">Internal TCP FIN Send</span></span> |
| ![İç T C P R S T al simgesi](./media/user-guide/netx-events/image14.png)    | <span data-ttu-id="37aae-136">İç TCP RST alma</span><span class="sxs-lookup"><span data-stu-id="37aae-136">Internal TCP RST Receive</span></span> |
| ![İç T C P R S T Gönder simgesi](./media/user-guide/netx-events/image15.png)    | <span data-ttu-id="37aae-138">İç TCP RST gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-138">Internal TCP RST Send</span></span> |
| ![İç T C P S e N al simgesi](./media/user-guide/netx-events/image16.png)    | <span data-ttu-id="37aae-140">İç TCP SYN alma</span><span class="sxs-lookup"><span data-stu-id="37aae-140">Internal TCP SYN Receive</span></span> |
| ![İç T C P S e N Gönder simgesi](./media/user-guide/netx-events/image17.png)    | <span data-ttu-id="37aae-142">İç TCP SYN Send</span><span class="sxs-lookup"><span data-stu-id="37aae-142">Internal TCP SYN Send</span></span> |
| ![İç U D P al simgesi](./media/user-guide/netx-events/image18.png)    | <span data-ttu-id="37aae-144">İç UDP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-144">Internal UDP Receive</span></span> |
| ![İç U D P Gönder simgesi](./media/user-guide/netx-events/image19.png)    | <span data-ttu-id="37aae-146">İç UDP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-146">Internal UDP Send</span></span> |
| ![Dahili R A R P alma simgesi](./media/user-guide/netx-events/image20.png)    | <span data-ttu-id="37aae-148">İç RARP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-148">Internal RARP Receive</span></span> |
| ![Dahili R A R P Gönder simgesi](./media/user-guide/netx-events/image21.png)    | <span data-ttu-id="37aae-150">İç RARP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-150">Internal RARP Send</span></span> |
| ![İç T C P yeniden deneme simgesi](./media/user-guide/netx-events/image22.png)    | <span data-ttu-id="37aae-152">İç TCP yeniden denemesi</span><span class="sxs-lookup"><span data-stu-id="37aae-152">Internal TCP Retry</span></span> |
| ![İç T C P durum değiştirme simgesi](./media/user-guide/netx-events/image23.png)    | <span data-ttu-id="37aae-154">İç TCP durum değişikliği</span><span class="sxs-lookup"><span data-stu-id="37aae-154">Internal TCP State Change</span></span> |
| ![İç g/ç sürücü paketi gönderme simgesi](./media/user-guide/netx-events/image24.png)    | <span data-ttu-id="37aae-156">İç g/ç sürücü paketi gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-156">Internal I/O Driver Packet Send</span></span> |
| ![simg](./media/user-guide/netx-events/image25.png)    | <span data-ttu-id="37aae-158">İç g/ç sürücüsü başlatma</span><span class="sxs-lookup"><span data-stu-id="37aae-158">Internal I/O Driver Initialize</span></span> |
| ![İç g/ç sürücüsü başlatma simgesi](./media/user-guide/netx-events/image26.png)    | <span data-ttu-id="37aae-160">İç g/ç sürücü bağlantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="37aae-160">Internal I/O Driver Link Enable</span></span> |
| ![İç g/ç sürücü bağlantısı devre dışı simgesi](./media/user-guide/netx-events/image27.png)    | <span data-ttu-id="37aae-162">İç g/ç sürücüsü bağlantısı devre dışı</span><span class="sxs-lookup"><span data-stu-id="37aae-162">Internal I/O Driver Link Disable</span></span> |
| ![İç g/ç sürücü paketi yayını simgesi](./media/user-guide/netx-events/image28.png)    | <span data-ttu-id="37aae-164">İç g/ç sürücü paketi yayını</span><span class="sxs-lookup"><span data-stu-id="37aae-164">Internal I/O Driver Packet Broadcast</span></span> |
| ![İç g/ç sürücüsü ARP gönderme simgesi](./media/user-guide/netx-events/image29.png)    | <span data-ttu-id="37aae-166">İç g/ç sürücüsü ARP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-166">Internal I/O Driver ARP Send</span></span> |
| ![İç g/ç sürücüsü ARP yanıtı gönderme simgesi](./media/user-guide/netx-events/image30.png)    | <span data-ttu-id="37aae-168">İç g/ç sürücüsü ARP yanıtı gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-168">Internal I/O Driver ARP Response Send</span></span> |
| ![İç g/ç sürücüsü RARP Gönder simgesi](./media/user-guide/netx-events/image31.png)    | <span data-ttu-id="37aae-170">İç g/ç sürücüsü RARP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-170">Internal I/O Driver RARP Send</span></span> |
| ![İç g/ç sürücüsü çok noktaya yayın Birleştir simgesi](./media/user-guide/netx-events/image32.png)    | <span data-ttu-id="37aae-172">İç g/ç sürücüsü çok noktaya yayın katılımı</span><span class="sxs-lookup"><span data-stu-id="37aae-172">Internal I/O Driver Multicast Join</span></span> |
| ![İç g/ç sürücüsü çok noktaya yayın çıkış simgesi](./media/user-guide/netx-events/image33.png)    | <span data-ttu-id="37aae-174">İç g/ç sürücüsü çok noktaya yayını bırakma</span><span class="sxs-lookup"><span data-stu-id="37aae-174">Internal I/O Driver Multicast Leave</span></span> |
| ![İç g/ç sürücüsü durum Al simgesi](./media/user-guide/netx-events/image34.png)    | <span data-ttu-id="37aae-176">İç g/ç sürücüsü Get durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-176">Internal I/O Driver Get Status</span></span> |
| ![İç g/ç sürücüsü al hız simgesi](./media/user-guide/netx-events/image35.png)    | <span data-ttu-id="37aae-178">İç g/ç sürücüsü edinme hızı</span><span class="sxs-lookup"><span data-stu-id="37aae-178">Internal I/O Driver Get Speed</span></span> |
| ![İç g/ç sürücüsü çift yönlü tür simgesi al](./media/user-guide/netx-events/image36.png)    | <span data-ttu-id="37aae-180">İç g/ç sürücüsü çift yönlü türü al</span><span class="sxs-lookup"><span data-stu-id="37aae-180">Internal I/O Driver Get Duplex Type</span></span> |
| ![İç g/ç sürücüsü hata sayısını Al simgesi](./media/user-guide/netx-events/image37.png)    | <span data-ttu-id="37aae-182">İç g/ç sürücüsü hata sayısını Al</span><span class="sxs-lookup"><span data-stu-id="37aae-182">Internal I/O Driver Get Error Count</span></span> |
| ![İç g/ç sürücüsü RX sayısı simgesi al](./media/user-guide/netx-events/image38.png)    | <span data-ttu-id="37aae-184">İç g/ç sürücüsü RX sayısı al</span><span class="sxs-lookup"><span data-stu-id="37aae-184">Internal I/O Driver Get RX Count</span></span> |
| ![İç g/ç sürücüsü TX sayısı simgesini al](./media/user-guide/netx-events/image39.png)    | <span data-ttu-id="37aae-186">İç g/ç sürücüsü TX sayısı al</span><span class="sxs-lookup"><span data-stu-id="37aae-186">Internal I/O Driver Get TX Count</span></span> |
| ![İç g/ç sürücüsü ayırma hatalarını al simgesi](./media/user-guide/netx-events/image40.png)    | <span data-ttu-id="37aae-188">İç g/ç sürücüsü ayırma hatalarını al</span><span class="sxs-lookup"><span data-stu-id="37aae-188">Internal I/O Driver Get Allocation Errors</span></span> |
| ![İç g/ç sürücüsü başlatması kaldır simgesi](./media/user-guide/netx-events/image41.png)    | <span data-ttu-id="37aae-190">İç g/ç sürücüsü başlatması geri al</span><span class="sxs-lookup"><span data-stu-id="37aae-190">Internal I/O Driver Un-initialize</span></span> |
| ![İç g/ç sürücüsü ertelenmiş Işleme simgesi](./media/user-guide/netx-events/image42.png)    | <span data-ttu-id="37aae-192">İç g/ç sürücüsü ertelenmiş Işleme</span><span class="sxs-lookup"><span data-stu-id="37aae-192">Internal I/O Driver Deferred Processing</span></span> |
| ![R P dinamik girdileri geçersiz kılar simgesi](./media/user-guide/netx-events/image43.png)    | <span data-ttu-id="37aae-194">**ARP dinamik girdileri geçersiz kılar** (*nx_arp_dynamic_entries_invalidate*)</span><span class="sxs-lookup"><span data-stu-id="37aae-194">**ARP Dynamic Entries Invalidate** (*nx_arp_dynamic_entries_invalidate*)</span></span> |
| ![R P dinamik giriş kümesi simgesi](./media/user-guide/netx-events/image44.png)    | <span data-ttu-id="37aae-196">**ARP dinamik giriş kümesi** (*nx_arp_dynamic_entry_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-196">**ARP Dynamic Entry Set** (*nx_arp_dynamic_entry_set*)</span></span> |
| ![R P etkinleştirme simgesi](./media/user-guide/netx-events/image45.png)    | <span data-ttu-id="37aae-198">**ARP etkinleştir** (*nx_arp_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-198">**ARP Enable** (*nx_arp_enable*)</span></span> |
| ![R P gereksiz Yolus Gönder simgesi](./media/user-guide/netx-events/image46.png)    | <span data-ttu-id="37aae-200">**ARP gereksiz Yolus gönderme** (*nx_arp_gratuitous_send*)</span><span class="sxs-lookup"><span data-stu-id="37aae-200">**ARP Gratuitous Send** (*nx_arp_gratuitous_send*)</span></span> |
| ![R P donanım adresi bul simgesi](./media/user-guide/netx-events/image47.png)    | <span data-ttu-id="37aae-202">**ARP donanım adresi bul** (*nx_arp_hardware_address_find*)</span><span class="sxs-lookup"><span data-stu-id="37aae-202">**ARP Hardware Address Find** (*nx_arp_hardware_address_find*)</span></span> |
| ![R P bilgi al simgesi](./media/user-guide/netx-events/image48.png)    | <span data-ttu-id="37aae-204">**ARP bilgileri Get** (*nx_arp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-204">**ARP Information Get** (*nx_arp_info_get*)</span></span> |
| ![R P IP adresi bulma simgesi](./media/user-guide/netx-events/image49.png)    | <span data-ttu-id="37aae-206">**ARP IP adresi bulma** (*nx_arp_ip_address_find*)</span><span class="sxs-lookup"><span data-stu-id="37aae-206">**ARP IP Address Find** (*nx_arp_ip_address_find*)</span></span> |
| ![R P statik giriş oluştur simgesi](./media/user-guide/netx-events/image50.png)    | <span data-ttu-id="37aae-208">**ARP statik girdisi oluşturma** (*nx_arp_static_entry_create*)</span><span class="sxs-lookup"><span data-stu-id="37aae-208">**ARP Static Entry Create** (*nx_arp_static_entry_create*)</span></span> |
| ![R P statik girdileri Sil simgesi](./media/user-guide/netx-events/image51.png)    | <span data-ttu-id="37aae-210">**ARP statik girdileri silme** (*nx_arp_static_entries_delete*)</span><span class="sxs-lookup"><span data-stu-id="37aae-210">**ARP Static Entries Delete** (*nx_arp_static_entries_delete*)</span></span> |
| ![R P statik giriş silme simgesi](./media/user-guide/netx-events/image52.png)    | <span data-ttu-id="37aae-212">**ARP statik giriş silme** (*nx_arp_static_entry_delete*)</span><span class="sxs-lookup"><span data-stu-id="37aae-212">**ARP Static Entry Delete** (*nx_arp_static_entry_delete*)</span></span> |
| ![Duo önbellek girişi silme simgesi](./media/user-guide/netx-events/image53.png)    | <span data-ttu-id="37aae-214">**Duo önbellek girişi silme** (*nxd_nd_cache_entry_delete*)</span><span class="sxs-lookup"><span data-stu-id="37aae-214">**Duo Cache Entry Delete** (*nxd_nd_cache_entry_delete*)</span></span> |
| ![Duo önbellek girdisi kümesi simgesi](./media/user-guide/netx-events/image54.png)    | <span data-ttu-id="37aae-216">**Duo önbellek giriş kümesi** (*nxd_nd_cache_entry_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-216">**Duo Cache Entry Set** (*nxd_nd_cache_entry_set*)</span></span> |
| ![Duo önbelleği geçersiz kıl simgesi](./media/user-guide/netx-events/image55.png)    | <span data-ttu-id="37aae-218">**Duo önbelleği geçersiz kıl** (*nxd_nd_cache_invalidate*)</span><span class="sxs-lookup"><span data-stu-id="37aae-218">**Duo Cache Invalidate** (*nxd_nd_cache_invalidate*)</span></span> |
| ![Duo önbelleği ı P adresi bul simgesi](./media/user-guide/netx-events/image56.png)    | <span data-ttu-id="37aae-220">**Duo ÖNBELLEĞI IP adresi bulma** (*nxd_nd_cache_ip_address_find*)</span><span class="sxs-lookup"><span data-stu-id="37aae-220">**Duo Cache IP Address Find** (*nxd_nd_cache_ip_address_find*)</span></span> |
| ![Duo ı C M P etkinleştir simgesi](./media/user-guide/netx-events/image57.png)    | <span data-ttu-id="37aae-222">**Duo ICMP etkinleştir** (*nxd_icmp_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-222">**Duo ICMP Enable** (*nxd_icmp_enable*)</span></span> |
| ![Duo ı C M P I P v 6 ping simgesi](./media/user-guide/netx-events/image58.png)    | <span data-ttu-id="37aae-224">**Duo ICMP IPv6 Ping** (*nxd_icmp_ping*)</span><span class="sxs-lookup"><span data-stu-id="37aae-224">**Duo ICMP IPv6 Ping** (*nxd_icmp_ping*)</span></span> |
| ![Duo ı P maks. yük boyutu bul simgesi](./media/user-guide/netx-events/image59.png)    | <span data-ttu-id="37aae-226">**Duo IP en fazla yük boyutu bul** (*nx_max_payload_size_find*)</span><span class="sxs-lookup"><span data-stu-id="37aae-226">**Duo IP Max Payload Size Find** (*nx_max_payload_size_find*)</span></span> |
| ![Duo ı P ham paket Gönder simgesi](./media/user-guide/netx-events/image60.png)    | <span data-ttu-id="37aae-228">**Duo IP ham paket gönderme** (*nxd_ip_raw_packet_send*)</span><span class="sxs-lookup"><span data-stu-id="37aae-228">**Duo IP Raw Packet Send** (*nxd_ip_raw_packet_send*)</span></span> |
| ![Duo ı P v 6 varsayılan yönlendirici Ekle simgesi](./media/user-guide/netx-events/image61.png)    | <span data-ttu-id="37aae-230">**Duo IPv6 varsayılan yönlendirici eklentisi** (*nxd_ipv6_default_router_add*)</span><span class="sxs-lookup"><span data-stu-id="37aae-230">**Duo IPv6 Default Router Add** (*nxd_ipv6_default_router_add*)</span></span> |
| ![Duo ı P v 6 varsayılan yönlendirici silme simgesi](./media/user-guide/netx-events/image62.png)    | <span data-ttu-id="37aae-232">**Duo IPv6 varsayılan yönlendirici silme** (*nxd_ipv6_default_router_delete)*</span><span class="sxs-lookup"><span data-stu-id="37aae-232">**Duo IPv6 Default Router Delete** (*nxd_ipv6_default_router_delete)*</span></span> |
| ![Duo ı P v 6 etkinleştirme simgesi](./media/user-guide/netx-events/image63.png)    | <span data-ttu-id="37aae-234">**Duo IPv6 etkinleştir** (*nxd_ipv6_enable)*</span><span class="sxs-lookup"><span data-stu-id="37aae-234">**Duo IPv6 Enable** (*nxd_ipv6_enable)*</span></span> |
| ![Duo ı P v 6 genel adres al simgesi](./media/user-guide/netx-events/image64.png)    | <span data-ttu-id="37aae-236">**Duo IPv6 genel adresi al** (*nxd_ipv6_global_address_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-236">**Duo IPv6 Global Address Get** (*nxd_ipv6_global_address_get*)</span></span> |
| ![Duo ı P v 6 genel adres kümesi simgesi](./media/user-guide/netx-events/image65.png)    | <span data-ttu-id="37aae-238">**Duo IPv6 genel adres kümesi** (*nxd_ipv6_global_address_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-238">**Duo IPv6 Global Address Set** (*nxd_ipv6_global_address_set*)</span></span> |
| ![Duo ı P v 6 babacığım Işlem simgesi](./media/user-guide/netx-events/image66.png)    | <span data-ttu-id="37aae-240">**Duo IPv6, babacığım işlemi** (*nxd_ipv6_initiate_dad_process*)</span><span class="sxs-lookup"><span data-stu-id="37aae-240">**Duo IPv6 Initiate Dad Process** (*nxd_ipv6_initiate_dad_process*)</span></span> |
| ![Duo ı P v 6 arabirim adresi al simgesi](./media/user-guide/netx-events/image67.png)    | <span data-ttu-id="37aae-242">**Duo IPv6 arabirim adresi Get** (*nxd_ipv6_interface_address_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-242">**Duo IPv6 Interface Address Get** (*nxd_ipv6_interface_address_get*)</span></span> |
| ![Duo ı P v 6 arabirim adres kümesi simgesi](./media/user-guide/netx-events/image68.png)    | <span data-ttu-id="37aae-244">**Duo IPv6 arabirimi adres kümesi** (*nxd_ipv6_interface_address_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-244">**Duo IPv6 Interface Address Set** (*nxd_ipv6_interface_address_set*)</span></span> |
| ![Duo ı P v 6 bağlantısı yerel adres al simgesi](./media/user-guide/netx-events/image69.png)    | <span data-ttu-id="37aae-246">**Duo IPv6 bağlantısı yerel adres Get** (*nxd_ipv6_linklocal_address_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-246">**Duo IPv6 Link Local Address Get** (*nxd_ipv6_linklocal_address_get*)</span></span> |
| ![Duo ı P v 6 bağlantısı yerel adres kümesi simgesi](./media/user-guide/netx-events/image70.png)    | <span data-ttu-id="37aae-248">**Duo IPv6 bağlantısı yerel adres kümesi** (*nxd_ipv6_linklocal_address_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-248">**Duo IPv6 Link Local Address Set** (*nxd_ipv6_linklocal_address_set*)</span></span> |
| ![Duo ı P v 6 ham paket Gönder simgesi](./media/user-guide/netx-events/image71.png)    | <span data-ttu-id="37aae-250">**Duo IPv6 ham paket gönderme** (*nxd_ipv6_raw_packet_send)*</span><span class="sxs-lookup"><span data-stu-id="37aae-250">**Duo IPv6 Raw Packet Send** (*nxd_ipv6_raw_packet_send)*</span></span> |
| ![Duo T C P soket eş bilgileri al simgesi](./media/user-guide/netx-events/image72.png)    | <span data-ttu-id="37aae-252">**Duo TCP yuvası eş bilgileri Get** (*nxd_tcp_socket_peer_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-252">**Duo TCP Socket Peer Info Get** (*nxd_tcp_socket_peer_info_get*)</span></span> |
| ![Duo T C P yuva kümesi arabirim simgesi](./media/user-guide/netx-events/image73.png)    | <span data-ttu-id="37aae-254">**Duo TCP yuva kümesi arabirimi** (*nxd_tcp_socket_set_interface*)</span><span class="sxs-lookup"><span data-stu-id="37aae-254">**Duo TCP Socket Set Interface** (*nxd_tcp_socket_set_interface*)</span></span> |
| ![Duo U D P yuvası gönderme simgesi](./media/user-guide/netx-events/image74.png)    | <span data-ttu-id="37aae-256">**Duo UDP yuvası gönderme** (*nxd_udp_socket_send*)</span><span class="sxs-lookup"><span data-stu-id="37aae-256">**Duo UDP Socket Send** (*nxd_udp_socket_send*)</span></span> |
| ![Duo U D P yuva kümesi arabirim simgesi](./media/user-guide/netx-events/image75.png)    | <span data-ttu-id="37aae-258">**Duo UDP yuva kümesi arabirimi** (*nxd_udp_socket_set_interface*)</span><span class="sxs-lookup"><span data-stu-id="37aae-258">**Duo UDP Socket Set Interface** (*nxd_udp_socket_set_interface*)</span></span> |
| ![Duo U D P kaynağı ayıklama simgesi](./media/user-guide/netx-events/image76.png)    | <span data-ttu-id="37aae-260">**Duo UDP kaynağı ayıklama** (*nxd_udp_source_extract*)</span><span class="sxs-lookup"><span data-stu-id="37aae-260">**Duo UDP Source Extract** (*nxd_udp_source_extract*)</span></span> |
| ![I C M P etkinleştir simgesi](./media/user-guide/netx-events/image77.png)    | <span data-ttu-id="37aae-262">**ICMP etkinleştirme** (*nx_icmp_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-262">**ICMP Enable** (*nx_icmp_enable*)</span></span> |
| ![I C M P bilgi al simgesi](./media/user-guide/netx-events/image78.png)    | <span data-ttu-id="37aae-264">**ICMP bilgileri al** (*nx_icmp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-264">**ICMP Information Get** (*nx_icmp_info_get*)</span></span> |
| ![I C M P ping simgesi](./media/user-guide/netx-events/image79.png)    | <span data-ttu-id="37aae-266">**ICMP ping** (*nx_icmp_ping*)</span><span class="sxs-lookup"><span data-stu-id="37aae-266">**ICMP Ping** (*nx_icmp_ping*)</span></span> |
| ![G G M P etkinleştirme simgesi](./media/user-guide/netx-events/image80.png)    | <span data-ttu-id="37aae-268">**IGMP etkinleştirme** (*nx_igmp_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-268">**IGMP Enable** (*nx_igmp_enable*)</span></span> |
| ![G-M P bilgi al simgesi](./media/user-guide/netx-events/image81.png)    | <span data-ttu-id="37aae-270">**IGMP bilgileri al** (*nx_igmp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-270">**IGMP Information Get** (*nx_igmp_info_get*)</span></span> |
| ![I G M P geri döngü devre dışı simgesi](./media/user-guide/netx-events/image82.png)    | <span data-ttu-id="37aae-272">**IGMP geri döngü devre dışı** (*nx_igmp_loopback_disable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-272">**IGMP Loopback Disable** (*nx_igmp_loopback_disable*)</span></span> |
| ![I G M P geri döngü etkinleştirme simgesi](./media/user-guide/netx-events/image83.png)    | <span data-ttu-id="37aae-274">**IGMP geri döngü etkinleştirme** (*nx_igmp_loopback_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-274">**IGMP Loopback Enable** (*nx_igmp_loopback_enable*)</span></span> |
| ![G & urum çok noktaya yayın Birleştir simgesi](./media/user-guide/netx-events/image84.png)    | <span data-ttu-id="37aae-276">**IGMP çok noktaya yayın katılımı** (*nx_igmp_multicast_join*)</span><span class="sxs-lookup"><span data-stu-id="37aae-276">**IGMP Multicast Join** (*nx_igmp_multicast_join*)</span></span> |
| ![G & urum çok noktaya yayın çıkış simgesi](./media/user-guide/netx-events/image85.png)    | <span data-ttu-id="37aae-278">**IGMP çok noktaya yayın** (*nx_igmp_multicast_leave*)</span><span class="sxs-lookup"><span data-stu-id="37aae-278">**IGMP Multicast Leave** (*nx_igmp_multicast_leave*)</span></span> |
| ![I P adres değişikliği bildirim simgesi](./media/user-guide/netx-events/image86.png)    | <span data-ttu-id="37aae-280">**IP adresi değişikliği bildirme** (*nx_ip_address_change_notify*)</span><span class="sxs-lookup"><span data-stu-id="37aae-280">**IP Address Change Notify** (*nx_ip_address_change_notify*)</span></span> |
| ![I P adresi al simgesi](./media/user-guide/netx-events/image87.png)    | <span data-ttu-id="37aae-282">**IP adresi al** (*nx_ip_address_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-282">**IP Address Get** (*nx_ip_address_get*)</span></span> |
| ![I P adres kümesi simgesi](./media/user-guide/netx-events/image88.png)    | <span data-ttu-id="37aae-284">**IP adresi kümesi** (*nx_ip_address_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-284">**IP Address Set** (*nx_ip_address_set*)</span></span> |
| ![I P Oluştur simgesi](./media/user-guide/netx-events/image89.png)    | <span data-ttu-id="37aae-286">**IP oluşturma** (*nx_ip_create*)</span><span class="sxs-lookup"><span data-stu-id="37aae-286">**IP Create** (*nx_ip_create*)</span></span> |
| ![I P Sil simgesi](./media/user-guide/netx-events/image90.png)    | <span data-ttu-id="37aae-288">**IP silme** (*nx_ip_delete*)</span><span class="sxs-lookup"><span data-stu-id="37aae-288">**IP Delete** (*nx_ip_delete*)</span></span> |
| ![I P sürücüsü doğrudan komut simgesi](./media/user-guide/netx-events/image91.png)    | <span data-ttu-id="37aae-290">**IP sürücüsü doğrudan komutu** (*nx_ip_driver_direct_command*)</span><span class="sxs-lookup"><span data-stu-id="37aae-290">**IP Driver Direct Command** (*nx_ip_driver_direct_command*)</span></span> |
| ![I P Iletme devre dışı simgesi](./media/user-guide/netx-events/image92.png)    | <span data-ttu-id="37aae-292">**IP Iletme devre dışı** (*nx_ip_forwarding_disable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-292">**IP Forwarding Disable** (*nx_ip_forwarding_disable*)</span></span> |
| ![I P Iletme etkinleştirme simgesi](./media/user-guide/netx-events/image93.png)    | <span data-ttu-id="37aae-294">**IP Iletme etkinleştir** (*nx_ip_forwarding_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-294">**IP Forwarding Enable** (*nx_ip_forwarding_enable*)</span></span> |
| ![I P parçanız devre dışı simgesi](./media/user-guide/netx-events/image94.png)    | <span data-ttu-id="37aae-296">**IP parçası devre dışı** (*nx_ip_fragment_disable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-296">**IP Fragment Disable** (*nx_ip_fragment_disable*)</span></span> |
| ![I P parçası etkinleştirme simgesi](./media/user-guide/netx-events/image95.png)    | <span data-ttu-id="37aae-298">**IP parçası etkinleştir** (*nx_ip_fragment_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-298">**IP Fragment Enable** (*nx_ip_fragment_enable*)</span></span>  |
| ![I P ağ geçidi adres kümesi simgesi](./media/user-guide/netx-events/image96.png)    | <span data-ttu-id="37aae-300">**IP ağ geçidi adres kümesi** (*nx_ip_gateway_address_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-300">**IP Gateway Address Set** (*nx_ip_gateway_address_set*)</span></span> |
| ![I P bilgileri al simgesi](./media/user-guide/netx-events/image97.png)    | <span data-ttu-id="37aae-302">**IP bilgileri al** (*nx_ip_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-302">**IP Information Get** (*nx_ip_info_get*)</span></span> |
| ![I P arabirimi Iliştirme simgesi](./media/user-guide/netx-events/image98.png)    | <span data-ttu-id="37aae-304">**IP arabirimine iliştirme** (*nx_ip_interface_attach*)</span><span class="sxs-lookup"><span data-stu-id="37aae-304">**IP Interface Attach** (*nx_ip_interface_attach*)</span></span> |
| ![I P arabirim bilgisi al simgesi](./media/user-guide/netx-events/image99.png)    | <span data-ttu-id="37aae-306">**IP arabirimi bilgileri al** (*nx_ip_interface_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-306">**IP Interface Info Get** (*nx_ip_interface_info_get*)</span></span> |
| ![I P ham paket devre dışı simgesi](./media/user-guide/netx-events/image100.png)    | <span data-ttu-id="37aae-308">**IP ham paket devre dışı** (*nx_ip_raw_packet_disable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-308">**IP Raw Packet Disable** (*nx_ip_raw_packet_disable*)</span></span> |
| ![I P RAW paketi etkinleştirme simgesi](./media/user-guide/netx-events/image101.png)    | <span data-ttu-id="37aae-310">**IP ham paket etkinleştir** (*nx_ip_raw_packet_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-310">**IP Raw Packet Enable** (*nx_ip_raw_packet_enable*)</span></span> |
| ![I P ham paket alma simgesi](./media/user-guide/netx-events/image102.png)    | <span data-ttu-id="37aae-312">**IP ham paket alma** (*nx_ip_raw_packet_receive*)</span><span class="sxs-lookup"><span data-stu-id="37aae-312">**IP Raw Packet Receive** (*nx_ip_raw_packet_receive*)</span></span> |
| ![I P ham paket Gönder simgesi](./media/user-guide/netx-events/image103.png)    | <span data-ttu-id="37aae-314">**IP ham paket gönderme** (*nx_ip_raw_packet_send*)</span><span class="sxs-lookup"><span data-stu-id="37aae-314">**IP Raw Packet Send** (*nx_ip_raw_packet_send*)</span></span> |
| ![I P statik yol ekleme simgesi](./media/user-guide/netx-events/image104.png)    | <span data-ttu-id="37aae-316">**IP statik yol ekleme** (*nx_ip_static_route_add*)</span><span class="sxs-lookup"><span data-stu-id="37aae-316">**IP Static Route Add** (*nx_ip_static_route_add*)</span></span> |
| ![I P statik yol silme simgesi](./media/user-guide/netx-events/image105.png)    | <span data-ttu-id="37aae-318">**IP statik yol silme** (*nx_ip_static_route_delete)*</span><span class="sxs-lookup"><span data-stu-id="37aae-318">**IP Static Route Delete** (*nx_ip_static_route_delete)*</span></span> |
| ![I P durum denetimi simgesi](./media/user-guide/netx-events/image106.png)    | <span data-ttu-id="37aae-320">**IP durum denetimi** (*nx_ip_status_check*)</span><span class="sxs-lookup"><span data-stu-id="37aae-320">**IP Status Check** (*nx_ip_status_check*)</span></span>|
| ![I P S E C etkinleştir simgesi](./media/user-guide/netx-events/image107.png)    | <span data-ttu-id="37aae-322">**IPSec etkinleştir** (*nx_ipsec_enable)*</span><span class="sxs-lookup"><span data-stu-id="37aae-322">**IPSEC Enable** (*nx_ipsec_enable)*</span></span> |
| ![Paket ayırma simgesi](./media/user-guide/netx-events/image108.png)    | <span data-ttu-id="37aae-324">**Paket ayırma** (*nx_packet_allocate*)</span><span class="sxs-lookup"><span data-stu-id="37aae-324">**Packet Allocate** (*nx_packet_allocate*)</span></span> |
| ![Paket kopyalama simgesi](./media/user-guide/netx-events/image109.png)    | <span data-ttu-id="37aae-326">**Paket kopyası** (*nx_packet_copy*)</span><span class="sxs-lookup"><span data-stu-id="37aae-326">**Packet Copy** (*nx_packet_copy*)</span></span> |
| ![Paket verileri ekleme simgesi](./media/user-guide/netx-events/image110.png)    | <span data-ttu-id="37aae-328">**Paket verileri ekleme** (*nx_packet_data_append*)</span><span class="sxs-lookup"><span data-stu-id="37aae-328">**Packet Data Append** (*nx_packet_data_append*)</span></span> |
| ![Paket verileri ayıklama fark simgesi](./media/user-guide/netx-events/image111.png)    | <span data-ttu-id="37aae-330">**Paket verileri ayıklama kayması** (*nx_packet_data_extract_offset*)</span><span class="sxs-lookup"><span data-stu-id="37aae-330">**Packet Data Extract Offset** (*nx_packet_data_extract_offset*)</span></span> |
| ![Paket verilerini alma simgesi](./media/user-guide/netx-events/image112.png)    | <span data-ttu-id="37aae-332">**Paket verileri alma** (*nx_packet_data_retrieve*)</span><span class="sxs-lookup"><span data-stu-id="37aae-332">**Packet Data Retrieve** (*nx_packet_data_retrieve*)</span></span> |
| ![Paket uzunluğu al simgesi](./media/user-guide/netx-events/image113.png)    | <span data-ttu-id="37aae-334">**Paket uzunluğu al** (*nx_packet_length_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-334">**Packet Length Get** (*nx_packet_length_get*)</span></span> |
| ![Paket havuzu oluştur simgesi](./media/user-guide/netx-events/image114.png)    | <span data-ttu-id="37aae-336">**Paket havuzu oluşturma** (*nx_packet_pool_create*)</span><span class="sxs-lookup"><span data-stu-id="37aae-336">**Packet Pool Create** (*nx_packet_pool_create*)</span></span> |
| ![Paket havuzu silme simgesi](./media/user-guide/netx-events/image115.png)    | <span data-ttu-id="37aae-338">**Paket havuzu silme** (*nx_packet_pool_delete*)</span><span class="sxs-lookup"><span data-stu-id="37aae-338">**Packet Pool Delete** (*nx_packet_pool_delete*)</span></span> |
| ![Paket havuzu bilgileri al simgesi](./media/user-guide/netx-events/image116.png)    | <span data-ttu-id="37aae-340">**Paket havuzu bilgileri Get** (*nx_packet_pool_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-340">**Packet Pool Information Get** (*nx_packet_pool_info_get*)</span></span> |
| ![Paket yayını simgesi](./media/user-guide/netx-events/image117.png)    | <span data-ttu-id="37aae-342">**Paket sürümü** (*nx_packet_release*)</span><span class="sxs-lookup"><span data-stu-id="37aae-342">**Packet Release** (*nx_packet_release*)</span></span> |
| ![Paket Iletme yayını simgesi](./media/user-guide/netx-events/image118.png)    | <span data-ttu-id="37aae-344">**Paket Iletme sürümü** (*nx_packet_transmit_release*)</span><span class="sxs-lookup"><span data-stu-id="37aae-344">**Packet Transmit Release** (*nx_packet_transmit_release*)</span></span> |
| ![R A R P devre dışı simgesi](./media/user-guide/netx-events/image119.png)    | <span data-ttu-id="37aae-346">**RARP Disable** (*nx_rarp_disable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-346">**RARP Disable** (*nx_rarp_disable*)</span></span> |
| ![R A R P etkinleştirme simgesi](./media/user-guide/netx-events/image120.png)    | <span data-ttu-id="37aae-348">**RARP etkinleştir** (*nx_rarp_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-348">**RARP Enable** (*nx_rarp_enable*)</span></span> |
| ![R A R P bilgi al simgesi](./media/user-guide/netx-events/image121.png)    | <span data-ttu-id="37aae-350">**RARP Information Get** (*nx_rarp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-350">**RARP Information Get** (*nx_rarp_info_get*)</span></span> |
| ![Sistem başlatma simgesi](./media/user-guide/netx-events/image122.png)    | <span data-ttu-id="37aae-352">**Sistem başlatma** (*nx_system_initialize*)</span><span class="sxs-lookup"><span data-stu-id="37aae-352">**System Initialize** (*nx_system_initialize*)</span></span> |
| ![T C P Istemci yuvası bağlama simgesi](./media/user-guide/netx-events/image123.png)    | <span data-ttu-id="37aae-354">**TCP Istemci yuvası bağlama** (*nx_tcp_client_socket_bind*)</span><span class="sxs-lookup"><span data-stu-id="37aae-354">**TCP Client Socket Bind** (*nx_tcp_client_socket_bind*)</span></span> |
| ![T C P Istemci yuvası bağlantı simgesi](./media/user-guide/netx-events/image124.png)    | <span data-ttu-id="37aae-356">**TCP Istemci yuvası bağlantısı** (*nx_tcp_client_socket_connect*)</span><span class="sxs-lookup"><span data-stu-id="37aae-356">**TCP Client Socket Connect** (*nx_tcp_client_socket_connect*)</span></span> |
| ![T C P Istemci yuva bağlantı noktası al simgesi](./media/user-guide/netx-events/image125.png)    | <span data-ttu-id="37aae-358">**TCP Istemci yuva bağlantı noktası al** (*nx_tcp_client_socket_port_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-358">**TCP Client Socket Port Get** (*nx_tcp_client_socket_port_get*)</span></span> |
| ![T C P Istemci yuvası bağlantı çözme simgesi](./media/user-guide/netx-events/image126.png)    | <span data-ttu-id="37aae-360">**TCP Istemci yuvası bağlantısı kesme** (*nx_tcp_client_socket_unbind*)</span><span class="sxs-lookup"><span data-stu-id="37aae-360">**TCP Client Socket Unbind** (*nx_tcp_client_socket_unbind*)</span></span> |
| ![T C P etkinleştirme simgesi](./media/user-guide/netx-events/image127.png)    | <span data-ttu-id="37aae-362">**TCP etkinleştirme** (*nx_tcp_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-362">**TCP Enable** (*nx_tcp_enable*)</span></span> |
| ![T C P boş bağlantı noktası bul simgesi](./media/user-guide/netx-events/image128.png)    | <span data-ttu-id="37aae-364">**TCP boş bağlantı noktası bul** (*nx_tcp_free_port_find*)</span><span class="sxs-lookup"><span data-stu-id="37aae-364">**TCP Free Port Find** (*nx_tcp_free_port_find*)</span></span> |
| ![T C P bilgi al simgesi](./media/user-guide/netx-events/image129.png)    | <span data-ttu-id="37aae-366">**TCP bilgileri al** (*nx_tcp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-366">**TCP Information Get** (*nx_tcp_info_get*)</span></span> |
| ![T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image130.png)    | <span data-ttu-id="37aae-368">**TCP sunucusu yuvasını kabul etme** (*nx_tcp_server_socket_accept*)</span><span class="sxs-lookup"><span data-stu-id="37aae-368">**TCP Server Socket Accept** (*nx_tcp_server_socket_accept*)</span></span> |
| ![T C P sunucu yuvası dinleme simgesi](./media/user-guide/netx-events/image131.png)    | <span data-ttu-id="37aae-370">**TCP sunucu yuvası dinleme** (*nx_tcp_server_socket_listen*)</span><span class="sxs-lookup"><span data-stu-id="37aae-370">**TCP Server Socket Listen** (*nx_tcp_server_socket_listen*)</span></span> |
| ![T C P sunucu yuvası yeniden dinleme simgesi](./media/user-guide/netx-events/image132.png)    | <span data-ttu-id="37aae-372">**TCP sunucu yuvası yeniden dinleme** (*nx_tcp_server_socket_relisten*)</span><span class="sxs-lookup"><span data-stu-id="37aae-372">**TCP Server Socket Relisten** (*nx_tcp_server_socket_relisten*)</span></span> |
| ![T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image133.png)    | <span data-ttu-id="37aae-374">**TCP sunucusu yuvası kabul etme** (*nx_tcp_server_socket_unaccept*)</span><span class="sxs-lookup"><span data-stu-id="37aae-374">**TCP Server Socket Unaccept** (*nx_tcp_server_socket_unaccept*)</span></span> |
| ![T C P Server yuva geri dinleme simgesi](./media/user-guide/netx-events/image134.png)    | <span data-ttu-id="37aae-376">**TCP sunucusu yuva geri dinleme** (*nx_tcp_server_socket_unlisten*)</span><span class="sxs-lookup"><span data-stu-id="37aae-376">**TCP Server Socket Unlisten** (*nx_tcp_server_socket_unlisten*)</span></span> |
| ![T C P yuva baytları kullanılabilir simgesi](./media/user-guide/netx-events/image135.png)    | <span data-ttu-id="37aae-378">**Kullanılabilir TCP yuva baytları** (*nx_tcp_socket_bytes_available*)</span><span class="sxs-lookup"><span data-stu-id="37aae-378">**TCP Socket Bytes Available** (*nx_tcp_socket_bytes_available*)</span></span> |
| ![T C P yuvası oluşturma simgesi](./media/user-guide/netx-events/image136.png)    | <span data-ttu-id="37aae-380">**TCP yuvası oluşturma** (*nx_tcp_socket_create*)</span><span class="sxs-lookup"><span data-stu-id="37aae-380">**TCP Socket Create** (*nx_tcp_socket_create*)</span></span> |
| ![T C P yuvası silme simgesi](./media/user-guide/netx-events/image137.png)    | <span data-ttu-id="37aae-382">**TCP yuvası silme** (*nx_tcp_socket_delete*)</span><span class="sxs-lookup"><span data-stu-id="37aae-382">**TCP Socket Delete** (*nx_tcp_socket_delete*)</span></span> |
| ![T C P yuvası bağlantı kesme simgesi](./media/user-guide/netx-events/image138.png)    | <span data-ttu-id="37aae-384">**TCP yuvası bağlantısı kesme** (*nx_tcp_socket_disconnect*)</span><span class="sxs-lookup"><span data-stu-id="37aae-384">**TCP Socket Disconnect** (*nx_tcp_socket_disconnect*)</span></span> |
| ![T C P yuva bilgileri al simgesi](./media/user-guide/netx-events/image139.png)    | <span data-ttu-id="37aae-386">**TCP yuva bilgileri Get** (*nx_tcp_socket_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-386">**TCP Socket Information Get** (*nx_tcp_socket_info_get*)</span></span> |
| ![T C P soket, al simgesi](./media/user-guide/netx-events/image140.png)    | <span data-ttu-id="37aae-388">**TCP yuvası ve Get** (*nx_tcp_socket_mss_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-388">**TCP Socket MSS Get** (*nx_tcp_socket_mss_get*)</span></span> |
| ![T C P soket bir eşi al](./media/user-guide/netx-events/image141.png)    | <span data-ttu-id="37aae-390">**TCP soketi eşi eş al** (*nx_tcp_socket_mss_peer_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-390">**TCP Socket MSS Peer Get** (*nx_tcp_socket_mss_peer_get*)</span></span> |
| ![T C P soket, küme simgesi](./media/user-guide/netx-events/image142.png)    | <span data-ttu-id="37aae-392">**TCP yuvası/küme** (*nx_tcp_socket_mss_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-392">**TCP Socket MSS Set** (*nx_tcp_socket_mss_set*)</span></span> |
| ![T C P soket eş bilgi al simgesi](./media/user-guide/netx-events/image143.png)    | <span data-ttu-id="37aae-394">**TCP yuvası eş bilgileri al** (*nx_tcp_socket_peer_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-394">**TCP Socket Peer Info Get** (*nx_tcp_socket_peer_info_get*)</span></span> |
| ![T C P yuvası alma simgesi](./media/user-guide/netx-events/image144.png)    | <span data-ttu-id="37aae-396">**TCP yuvası alma** (*nx_tcp_socket_receive*)</span><span class="sxs-lookup"><span data-stu-id="37aae-396">**TCP Socket Receive** (*nx_tcp_socket_receive*)</span></span> |
| ![T C P yuvası alma bildirim simgesi](./media/user-guide/netx-events/image145.png)    | <span data-ttu-id="37aae-398">**TCP yuvası alma bildirimi** (*nx_tcp_socket_receive_notify*)</span><span class="sxs-lookup"><span data-stu-id="37aae-398">**TCP Socket Receive Notify** (*nx_tcp_socket_receive_notify*)</span></span> |
| ![T C P yuvası gönderme simgesi](./media/user-guide/netx-events/image146.png)    | <span data-ttu-id="37aae-400">**TCP yuvası gönderme** (*nx_tcp_socket_send*)</span><span class="sxs-lookup"><span data-stu-id="37aae-400">**TCP Socket Send** (*nx_tcp_socket_send*)</span></span> |
| ![T C P yuva durumu bekleme simgesi](./media/user-guide/netx-events/image147.png)    | <span data-ttu-id="37aae-402">**TCP yuva durumu bekle** (*nx_tcp_socket_state_wait*)</span><span class="sxs-lookup"><span data-stu-id="37aae-402">**TCP Socket State Wait** (*nx_tcp_socket_state_wait*)</span></span> |
| ![T C P yuvası Iletme yapılandırma simgesi](./media/user-guide/netx-events/image148.png)    | <span data-ttu-id="37aae-404">**TCP yuvası Iletme yapılandırması** (*nx_tcp_socket_transmit_configure*)</span><span class="sxs-lookup"><span data-stu-id="37aae-404">**TCP Socket Transmit Configure** (*nx_tcp_socket_transmit_configure*)</span></span> |
| ![T C P yuvası pencere güncelleştirme bildirim kümesi simgesi](./media/user-guide/netx-events/image149.png)    | <span data-ttu-id="37aae-406">**TCP yuvası pencere güncelleştirme bildirim kümesi** (*nx_tcp_socket_window_update_notify_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-406">**TCP Socket Window Update Notify Set** (*nx_tcp_socket_window_update_notify_set*)</span></span>  |
| ![U D P etkinleştirme simgesi](./media/user-guide/netx-events/image150.png)    | <span data-ttu-id="37aae-408">**UDP etkinleştirme** (*nx_udp_enable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-408">**UDP Enable** (*nx_udp_enable*)</span></span> |
| ![U D P boş bağlantı noktası bul simgesi](./media/user-guide/netx-events/image151.png)    | <span data-ttu-id="37aae-410">**UDP boş bağlantı noktası bul** (*nx_udp_free_port_find*)</span><span class="sxs-lookup"><span data-stu-id="37aae-410">**UDP Free Port Find** (*nx_udp_free_port_find*)</span></span> |
| ![U D P bilgi al simgesi](./media/user-guide/netx-events/image152.png)    | <span data-ttu-id="37aae-412">**UDP bilgileri al** (*nx_udp_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-412">**UDP Information Get** (*nx_udp_info_get*)</span></span> |
| ![U D P yuvası bağlama simgesi](./media/user-guide/netx-events/image153.png)    | <span data-ttu-id="37aae-414">**UDP yuva bağlama** (*nx_udp_socket_bind*)</span><span class="sxs-lookup"><span data-stu-id="37aae-414">**UDP Socket Bind** (*nx_udp_socket_bind*)</span></span> |
| ![U D P yuva baytları kullanılabilir simgesi](./media/user-guide/netx-events/image154.png)    | <span data-ttu-id="37aae-416">**Kullanılabilir UDP yuva baytları** (*nx_udp_socket_bytes_available*)</span><span class="sxs-lookup"><span data-stu-id="37aae-416">**UDP Socket Bytes Available** (*nx_udp_socket_bytes_available*)</span></span> |
| ![U D P soket sağlama toplamı devre dışı simgesi](./media/user-guide/netx-events/image155.png)    | <span data-ttu-id="37aae-418">**UDP yuva sağlama toplamı devre dışı** (*nx_udp_socket_checksum_disable*)</span><span class="sxs-lookup"><span data-stu-id="37aae-418">**UDP Socket Checksum Disable** (*nx_udp_socket_checksum_disable*)</span></span> |
| ![U D P yuva sağlama toplamı etkinleştir simgesi](./media/user-guide/netx-events/image156.png)    | <span data-ttu-id="37aae-420">**UDP yuva sağlama toplamı etkinleştir** *(nx_udp_socket_checksum_enable)*</span><span class="sxs-lookup"><span data-stu-id="37aae-420">**UDP Socket Checksum Enable** *(nx_udp_socket_checksum_enable)*</span></span> |
| ![U D P yuvası oluşturma simgesi](./media/user-guide/netx-events/image157.png)    | <span data-ttu-id="37aae-422">**UDP yuvası oluşturma** (*nx_udp_socket_create*)</span><span class="sxs-lookup"><span data-stu-id="37aae-422">**UDP Socket Create** (*nx_udp_socket_create*)</span></span> |
| ![U D P yuvası silme simgesi](./media/user-guide/netx-events/image158.png)    | <span data-ttu-id="37aae-424">**UDP yuvası silme** (*nx_udp_socket_delete*)</span><span class="sxs-lookup"><span data-stu-id="37aae-424">**UDP Socket Delete** (*nx_udp_socket_delete*)</span></span> |
| ![U D yuva bilgileri al simgesi](./media/user-guide/netx-events/image159.png)    | <span data-ttu-id="37aae-426">**UDP yuva bilgileri Get** (*nx_udp_socket_info_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-426">**UDP Socket Information Get** (*nx_udp_socket_info_get*)</span></span> |
| ![U D P yuva arabirimi kümesi simgesi](./media/user-guide/netx-events/image160.png)    | <span data-ttu-id="37aae-428">**UDP yuva arabirimi kümesi** (*nx_udp_socket_interface_set*)</span><span class="sxs-lookup"><span data-stu-id="37aae-428">**UDP Socket Interface Set** (*nx_udp_socket_interface_set*)</span></span> |
| ![U D P yuva bağlantı noktası al simgesi](./media/user-guide/netx-events/image161.png)    | <span data-ttu-id="37aae-430">**UDP yuva bağlantı noktası al** (*nx_udp_socket_port_get*)</span><span class="sxs-lookup"><span data-stu-id="37aae-430">**UDP Socket Port Get** (*nx_udp_socket_port_get*)</span></span> |
| ![U D P yuvası alma simgesi](./media/user-guide/netx-events/image162.png)    | <span data-ttu-id="37aae-432">**UDP yuvası alma** (*nx_udp_socket_receive*)</span><span class="sxs-lookup"><span data-stu-id="37aae-432">**UDP Socket Receive** (*nx_udp_socket_receive*)</span></span> |
| ![U D P yuvası alma bildirim simgesi](./media/user-guide/netx-events/image163.png)    | <span data-ttu-id="37aae-434">**UDP yuvası alma bildirimi** (*nx_udp_socket_receive_notify*)</span><span class="sxs-lookup"><span data-stu-id="37aae-434">**UDP Socket Receive Notify** (*nx_udp_socket_receive_notify*)</span></span> |
| ![U D P yuvası gönderme simgesi](./media/user-guide/netx-events/image164.png)    | <span data-ttu-id="37aae-436">**UDP yuvası gönderme** (*nx_udp_socket_send*)</span><span class="sxs-lookup"><span data-stu-id="37aae-436">**UDP Socket Send** (*nx_udp_socket_send*)</span></span> |
| ![U D P yuvası çözme simgesi](./media/user-guide/netx-events/image165.png)    | <span data-ttu-id="37aae-438">**UDP yuvası bağlantısı kesme** (*nx_udp_socket_unbind*)</span><span class="sxs-lookup"><span data-stu-id="37aae-438">**UDP Socket Unbind** (*nx_udp_socket_unbind*)</span></span> |
| ![U D P kaynağı ayıklama simgesi](./media/user-guide/netx-events/image166.png)    | <span data-ttu-id="37aae-440">**UDP kaynağı ayıklama** (*nx_udp_source_extract*)</span><span class="sxs-lookup"><span data-stu-id="37aae-440">**UDP Source Extract** (*nx_udp_source_extract*)</span></span> |

## <a name="event-descriptions"></a><span data-ttu-id="37aae-441">Olay Açıklamaları</span><span class="sxs-lookup"><span data-stu-id="37aae-441">Event Descriptions</span></span>

<span data-ttu-id="37aae-442">Aşağıdaki sayfalarda NetX Izleme olayları açıklanır.</span><span class="sxs-lookup"><span data-stu-id="37aae-442">The following pages describe the NetX Trace Events.</span></span>

### <a name="internal-arp-request-receive"></a><span data-ttu-id="37aae-443">İç ARP Isteği alma</span><span class="sxs-lookup"><span data-stu-id="37aae-443">Internal ARP Request Receive</span></span> 

#### <a name="internal-arp-request-receive"></a><span data-ttu-id="37aae-444">İç ARP isteği alma</span><span class="sxs-lookup"><span data-stu-id="37aae-444">Internal ARP request receive</span></span>

<span data-ttu-id="37aae-445">**Simge** ![ İç ARP isteği alma simgesi](./media/user-guide/netx-events/image1.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-445">**Icon** ![Internal ARP request receive icon](./media/user-guide/netx-events/image1.png)</span></span>

<span data-ttu-id="37aae-446">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-446">**Description**</span></span>

<span data-ttu-id="37aae-447">Bu olay bir iç NetX ARP istek alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-447">This event represents an internal NetX ARP request receive event.</span></span>

<span data-ttu-id="37aae-448">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-448">**Information Fields**</span></span>

- <span data-ttu-id="37aae-449">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-449">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-450">Bilgi alanı 2: kaynak IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-450">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="37aae-451">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-451">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-452">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-452">Info Field 4: Not used</span></span>

### <a name="internal-arp-request-send"></a><span data-ttu-id="37aae-453">İç ARP Isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-453">Internal ARP Request Send</span></span> 

#### <a name="internal-arp-request-send"></a><span data-ttu-id="37aae-454">İç ARP isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-454">Internal ARP request send</span></span>

<span data-ttu-id="37aae-455">**Simge** ![ İç ARP isteği gönderme simgesi](./media/user-guide/netx-events/image2.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-455">**Icon** ![Internal ARP request send icon](./media/user-guide/netx-events/image2.png)</span></span>

<span data-ttu-id="37aae-456">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-456">**Description**</span></span>

<span data-ttu-id="37aae-457">Bu olay bir iç NetX ARP istek gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-457">This event represents an internal NetX ARP request send event.</span></span>

<span data-ttu-id="37aae-458">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-458">**Information Fields**</span></span>

- <span data-ttu-id="37aae-459">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-459">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-460">Bilgi alanı 2: hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-460">Info Field 2: Destination IP address</span></span>
- <span data-ttu-id="37aae-461">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-461">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-462">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-462">Info Field 4: Not used</span></span>

### <a name="internal-arp-response-receive"></a><span data-ttu-id="37aae-463">İç ARP yanıtı alma</span><span class="sxs-lookup"><span data-stu-id="37aae-463">Internal ARP Response Receive</span></span> 

#### <a name="internal-arp-request-receive"></a><span data-ttu-id="37aae-464">İç ARP isteği alma</span><span class="sxs-lookup"><span data-stu-id="37aae-464">Internal ARP request receive</span></span>

<span data-ttu-id="37aae-465">**Simge** ![ Iç ARP isteği alma simgesi](./media/user-guide/netx-events/image3.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-465">**Icon** ![The Internal ARP request receive icon](./media/user-guide/netx-events/image3.png)</span></span>

<span data-ttu-id="37aae-466">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-466">**Description**</span></span>

<span data-ttu-id="37aae-467">Bu olay bir iç NetX ARP yanıtı alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-467">This event represents an internal NetX ARP response receive event.</span></span>

<span data-ttu-id="37aae-468">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-468">**Information Fields**</span></span>

- <span data-ttu-id="37aae-469">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-469">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-470">Bilgi alanı 2: kaynak IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-470">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="37aae-471">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-471">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-472">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-472">Info Field 4: Not used</span></span>

### <a name="internal-arp-response-send"></a><span data-ttu-id="37aae-473">İç ARP yanıtı gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-473">Internal ARP Response Send</span></span> 

#### <a name="internal-arp-request-send"></a><span data-ttu-id="37aae-474">İç ARP isteği gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-474">Internal ARP request send</span></span>

<span data-ttu-id="37aae-475">**Simge** ![ Iç ARP isteği gönderme simgesi](./media/user-guide/netx-events/image4.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-475">**Icon** ![The Internal ARP request send icon](./media/user-guide/netx-events/image4.png)</span></span>

<span data-ttu-id="37aae-476">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-476">**Description**</span></span>

<span data-ttu-id="37aae-477">Bu olay bir iç NetX yanıtı gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-477">This event represents an internal NetX response send event.</span></span>

<span data-ttu-id="37aae-478">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-478">**Information Fields**</span></span>

- <span data-ttu-id="37aae-479">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-479">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-480">Bilgi alanı 2: hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-480">Info Field 2: Destination IP address</span></span>
- <span data-ttu-id="37aae-481">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-481">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-482">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-482">Info Field 4: Not used</span></span>

### <a name="internal-icmp-receive"></a><span data-ttu-id="37aae-483">İç ıCMP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-483">Internal ICMP Receive</span></span> 

#### <a name="internal-icmp-receive"></a><span data-ttu-id="37aae-484">İç ıCMP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-484">Internal ICMP receive</span></span>

<span data-ttu-id="37aae-485">**Simge** ![ İç ı C M P alma simgesi](./media/user-guide/netx-events/image5.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-485">**Icon** ![Internal I C M P receive icon](./media/user-guide/netx-events/image5.png)</span></span>

<span data-ttu-id="37aae-486">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-486">**Description**</span></span>

<span data-ttu-id="37aae-487">Bu olay bir iç NetX ıCMP alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-487">This event represents an internal NetX ICMP receive event.</span></span>

<span data-ttu-id="37aae-488">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-488">**Information Fields**</span></span>

- <span data-ttu-id="37aae-489">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-489">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-490">Bilgi alanı 2: kaynak IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-490">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="37aae-491">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-491">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-492">Bilgi alanı 4: ıCMP üstbilgisinin kelime 0</span><span class="sxs-lookup"><span data-stu-id="37aae-492">Info Field 4: Word 0 of ICMP header</span></span>

### <a name="internal-icmp-send"></a><span data-ttu-id="37aae-493">İç ıCMP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-493">Internal ICMP Send</span></span> 

#### <a name="internal-icmp-send"></a><span data-ttu-id="37aae-494">İç ıCMP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-494">Internal ICMP send</span></span>

<span data-ttu-id="37aae-495">**Simge** ![ İç ı C M P Gönder simgesi](./media/user-guide/netx-events/image6.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-495">**Icon** ![Internal I C M P send icon](./media/user-guide/netx-events/image6.png)</span></span>

<span data-ttu-id="37aae-496">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-496">**Description**</span></span>

<span data-ttu-id="37aae-497">Bu olay bir iç NetX ıCMP gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-497">This event represents an internal NetX ICMP send event.</span></span>

<span data-ttu-id="37aae-498">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-498">**Information Fields**</span></span>

- <span data-ttu-id="37aae-499">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-499">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-500">Bilgi alanı 2: hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-500">Info Field 2: Destination IP address</span></span>
- <span data-ttu-id="37aae-501">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-501">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-502">Bilgi alanı 4: ıCMP üstbilgisinin kelime 0</span><span class="sxs-lookup"><span data-stu-id="37aae-502">Info Field 4: Word 0 of ICMP header</span></span>

### <a name="internal-igmp-receive"></a><span data-ttu-id="37aae-503">İç ıGMP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-503">Internal IGMP Receive</span></span> 

#### <a name="internal-igmp-receive"></a><span data-ttu-id="37aae-504">İç ıGMP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-504">Internal IGMP receive</span></span>

<span data-ttu-id="37aae-505">**Simge** ![ Dahili ı G M P alma simgesi](./media/user-guide/netx-events/image7.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-505">**Icon** ![Internal I G M P receive icon](./media/user-guide/netx-events/image7.png)</span></span>

<span data-ttu-id="37aae-506">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-506">**Description**</span></span>

<span data-ttu-id="37aae-507">Bu olay bir iç NetX ıGMP alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-507">This event represents an internal NetX IGMP receive event.</span></span>

<span data-ttu-id="37aae-508">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-508">**Information Fields**</span></span>

- <span data-ttu-id="37aae-509">Bilgi alanı 1: IP Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-509">Info Field 1: IP Pointer</span></span>
- <span data-ttu-id="37aae-510">Bilgi alanı 2: kaynak IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-510">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="37aae-511">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-511">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-512">Bilgi alanı 4: ıGMP üstbilgisinin 0. sözcüğü</span><span class="sxs-lookup"><span data-stu-id="37aae-512">Info Field 4: Word 0 of IGMP header</span></span>

### <a name="internal-ip-receive"></a><span data-ttu-id="37aae-513">İç IP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-513">Internal IP Receive</span></span> 

#### <a name="internal-ip-receive"></a><span data-ttu-id="37aae-514">İç IP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-514">Internal IP receive</span></span>

<span data-ttu-id="37aae-515">**Simge** ![ İç ı P alma simgesi](./media/user-guide/netx-events/image8.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-515">**Icon** ![Internal I P receive icon](./media/user-guide/netx-events/image8.png)</span></span>

<span data-ttu-id="37aae-516">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-516">**Description**</span></span>

<span data-ttu-id="37aae-517">Bu olay bir iç NetX IP alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-517">This event represents an internal NetX IP receive event.</span></span>

<span data-ttu-id="37aae-518">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-518">**Information Fields**</span></span>

- <span data-ttu-id="37aae-519">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-519">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-520">Bilgi alanı 2: kaynak IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-520">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="37aae-521">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-521">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-522">Bilgi alanı 4: paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="37aae-522">Info Field 4: Packet length</span></span>

### <a name="internal-ip-send"></a><span data-ttu-id="37aae-523">İç IP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-523">Internal IP Send</span></span>

#### <a name="internal-ip-send"></a><span data-ttu-id="37aae-524">İç IP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-524">Internal IP send</span></span>

<span data-ttu-id="37aae-525">**Simge** ![ İç ı P Gönder simgesi](./media/user-guide/netx-events/image9.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-525">**Icon** ![Internal I P send icon](./media/user-guide/netx-events/image9.png)</span></span>

<span data-ttu-id="37aae-526">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-526">**Description**</span></span>

<span data-ttu-id="37aae-527">Bu olay bir iç NetX IP gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-527">This event represents an internal NetX IP send event.</span></span>

<span data-ttu-id="37aae-528">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-528">**Information Fields**</span></span>

- <span data-ttu-id="37aae-529">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-529">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-530">Bilgi alanı 2: hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-530">Info Field 2: Destination IP address</span></span>
- <span data-ttu-id="37aae-531">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-531">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-532">Bilgi alanı 4: paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="37aae-532">Info Field 4: Packet length</span></span>

### <a name="internal-tcp-data-receive"></a><span data-ttu-id="37aae-533">İç TCP veri alma</span><span class="sxs-lookup"><span data-stu-id="37aae-533">Internal TCP Data Receive</span></span> 

#### <a name="internal-tcp-data-receive"></a><span data-ttu-id="37aae-534">İç TCP veri alma</span><span class="sxs-lookup"><span data-stu-id="37aae-534">Internal TCP Data Receive</span></span>

<span data-ttu-id="37aae-535">**Simge** ![ İç T C P veri alma simgesi](./media/user-guide/netx-events/image10.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-535">**Icon** ![Internal T C P data receive icon](./media/user-guide/netx-events/image10.png)</span></span>

<span data-ttu-id="37aae-536">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-536">**Description**</span></span>

<span data-ttu-id="37aae-537">Bu olay bir iç NetX TCP veri alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-537">This event represents an internal NetX TCP data receive event.</span></span>

<span data-ttu-id="37aae-538">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-538">**Information Fields**</span></span>

- <span data-ttu-id="37aae-539">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-539">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-540">Bilgi alanı 2: kaynak IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-540">Info Field 2: Source IP address</span></span>
- <span data-ttu-id="37aae-541">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-541">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-542">Bilgi alanı 4: alma sıra numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-542">Info Field 4: Receive sequence number</span></span>

### <a name="internal-tcp-data-send"></a><span data-ttu-id="37aae-543">İç TCP veri gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-543">Internal TCP data send</span></span> 

#### <a name="internal-tcp-data-send"></a><span data-ttu-id="37aae-544">İç TCP veri gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-544">Internal TCP Data Send</span></span>

<span data-ttu-id="37aae-545">**Simge** ![ İç T C P veri gönderme simgesi](./media/user-guide/netx-events/image11.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-545">**Icon** ![Internal T C P data send icon](./media/user-guide/netx-events/image11.png)</span></span>

<span data-ttu-id="37aae-546">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-546">**Description**</span></span>

<span data-ttu-id="37aae-547">Bu olay bir iç NetX TCP veri gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-547">This event represents an internal NetX TCP data send event.</span></span>

<span data-ttu-id="37aae-548">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-548">**Information Fields**</span></span>

- <span data-ttu-id="37aae-549">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-549">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-550">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-550">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-551">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-551">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-552">Bilgi alanı 4: aktarım sıra numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-552">Info Field 4: Transmit sequence number</span></span>

### <a name="internal-tcp-fin-receive"></a><span data-ttu-id="37aae-553">İç TCP FIN alma</span><span class="sxs-lookup"><span data-stu-id="37aae-553">Internal TCP FIN Receive</span></span> 

#### <a name="internal-tcp-fin-receive"></a><span data-ttu-id="37aae-554">İç TCP Fin alma</span><span class="sxs-lookup"><span data-stu-id="37aae-554">Internal TCP fin receive</span></span>

<span data-ttu-id="37aae-555">**Simge** ![ İç T C P F ı N al simgesi](./media/user-guide/netx-events/image12.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-555">**Icon** ![Internal T C P F I N receive icon](./media/user-guide/netx-events/image12.png)</span></span>

<span data-ttu-id="37aae-556">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-556">**Description**</span></span>

<span data-ttu-id="37aae-557">Bu olay bir iç NetX TCP FIN alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-557">This event represents an internal NetX TCP FIN receive event.</span></span>

<span data-ttu-id="37aae-558">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-558">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-559">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-559">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-560">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-560">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-561">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-561">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-562">Bilgi alanı 4: alma sıra numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-562">Info Field 4: Receive sequence number</span></span>

### <a name="internal-tcp-fin-send"></a><span data-ttu-id="37aae-563">İç TCP FIN gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-563">Internal TCP FIN Send</span></span> 

#### <a name="internal-tcp-fin-send"></a><span data-ttu-id="37aae-564">İç TCP Fin gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-564">Internal TCP fin send</span></span>

<span data-ttu-id="37aae-565">**Simge** ![ İç T C P F ı N Gönder simgesi](./media/user-guide/netx-events/image13.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-565">**Icon** ![Internal T C P F I N send icon](./media/user-guide/netx-events/image13.png)</span></span>

<span data-ttu-id="37aae-566">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-566">**Description**</span></span>

<span data-ttu-id="37aae-567">Bu olay bir iç NetX TCP FIN gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-567">This event represents an internal NetX TCP FIN send event.</span></span>

<span data-ttu-id="37aae-568">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-568">**Information Fields**</span></span>

- <span data-ttu-id="37aae-569">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-569">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-570">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-570">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-571">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-571">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-572">Bilgi alanı 4: aktarım sıra numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-572">Info Field 4:Transmit sequence number</span></span>

### <a name="internal-tcp-rst-receive"></a><span data-ttu-id="37aae-573">İç TCP RST alma</span><span class="sxs-lookup"><span data-stu-id="37aae-573">Internal TCP RST Receive</span></span> 

#### <a name="internal-tcp-rst-receive"></a><span data-ttu-id="37aae-574">İç TCP RST alma</span><span class="sxs-lookup"><span data-stu-id="37aae-574">Internal TCP RST receive</span></span>

<span data-ttu-id="37aae-575">**Simge** ![ İç T C P R S T al simgesi](./media/user-guide/netx-events/image14.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-575">**Icon** ![Internal T C P R S T receive icon](./media/user-guide/netx-events/image14.png)</span></span>

<span data-ttu-id="37aae-576">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-576">**Description**</span></span>

<span data-ttu-id="37aae-577">Bu olay bir iç NetX TCP sıfırlama alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-577">This event represents an internal NetX TCP reset receive event.</span></span>

<span data-ttu-id="37aae-578">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-578">**Information Fields**</span></span>

- <span data-ttu-id="37aae-579">Bilgi alanı 1: IP örneğine yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="37aae-579">Info Field 1: Pointer to the IP instance.</span></span>
- <span data-ttu-id="37aae-580">Bilgi alanı 2: yuva Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="37aae-580">Info Field 2: Pointer to socket.</span></span>
- <span data-ttu-id="37aae-581">Bilgi alanı 3: paket Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="37aae-581">Info Field 3: Pointer to packet.</span></span>
- <span data-ttu-id="37aae-582">Bilgi alanı 4: alma sıra numarası.</span><span class="sxs-lookup"><span data-stu-id="37aae-582">Info Field 4: Receive sequence number.</span></span>

### <a name="internal-tcp-rst-send"></a><span data-ttu-id="37aae-583">İç TCP RST gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-583">Internal TCP RST Send</span></span> 

#### <a name="internal-tcp-rst-send"></a><span data-ttu-id="37aae-584">İç TCP RST gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-584">Internal TCP RST send</span></span>

<span data-ttu-id="37aae-585">**Simge** ![ İç T C P R S T Gönder simgesi](./media/user-guide/netx-events/image15.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-585">**Icon** ![Internal T C P R S T send icon](./media/user-guide/netx-events/image15.png)</span></span>

<span data-ttu-id="37aae-586">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-586">**Description**</span></span>

<span data-ttu-id="37aae-587">Bu olay bir iç NetX TCP sıfırlama gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-587">This event represents an internal NetX TCP reset send event.</span></span>

<span data-ttu-id="37aae-588">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-588">**Information Fields**</span></span>

- <span data-ttu-id="37aae-589">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-589">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-590">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-590">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-591">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-591">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-592">Bilgi alanı 4: aktarım sıra numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-592">Info Field 4: Transmit sequence number</span></span>

### <a name="internal-tcp-syn-receive"></a><span data-ttu-id="37aae-593">İç TCP SYN alma</span><span class="sxs-lookup"><span data-stu-id="37aae-593">Internal TCP SYN Receive</span></span> 

#### <a name="internal-tcp-syn-receive"></a><span data-ttu-id="37aae-594">İç TCP SYN alma</span><span class="sxs-lookup"><span data-stu-id="37aae-594">Internal TCP SYN receive</span></span>

<span data-ttu-id="37aae-595">**Simge** ![ İç T C P S e N al simgesi](./media/user-guide/netx-events/image16.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-595">**Icon** ![Internal T C P S Y N receive icon](./media/user-guide/netx-events/image16.png)</span></span>

<span data-ttu-id="37aae-596">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-596">**Description**</span></span>

<span data-ttu-id="37aae-597">Bu olay bir iç NetX TCP SYN Receive olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-597">This event represents an internal NetX TCP SYN receive event.</span></span>

<span data-ttu-id="37aae-598">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-598">**Information Fields**</span></span>

- <span data-ttu-id="37aae-599">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-599">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-600">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-600">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-601">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-601">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-602">Bilgi alanı 4: alma sıra numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-602">Info Field 4: Receive sequence number</span></span>

### <a name="internal-tcp-syn-send"></a><span data-ttu-id="37aae-603">İç TCP SYN Send</span><span class="sxs-lookup"><span data-stu-id="37aae-603">Internal TCP SYN Send</span></span> 

#### <a name="internal-tcp-syn-send"></a><span data-ttu-id="37aae-604">İç TCP SYN Send</span><span class="sxs-lookup"><span data-stu-id="37aae-604">Internal TCP SYN send</span></span>

<span data-ttu-id="37aae-605">**Simge** ![ İç T C P S e N Gönder simgesi](./media/user-guide/netx-events/image17.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-605">**Icon** ![Internal T C P S Y N send icon](./media/user-guide/netx-events/image17.png)</span></span>

<span data-ttu-id="37aae-606">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-606">**Description**</span></span>

<span data-ttu-id="37aae-607">Bu olay bir iç NetX TCP SYN Send olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-607">This event represents an internal NetX TCP SYN send event.</span></span>

<span data-ttu-id="37aae-608">Bilgi alanları</span><span class="sxs-lookup"><span data-stu-id="37aae-608">Information Fields</span></span> 

- <span data-ttu-id="37aae-609">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-609">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-610">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-610">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-611">Bilgi alanı 3: paket-bilgi alanı 4 Işaretçisi: aktarım sıra numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-611">Info Field 3: Pointer to packet -Info Field 4: Transmit sequence number</span></span>

### <a name="internal-udp-receive"></a><span data-ttu-id="37aae-612">İç UDP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-612">Internal UDP Receive</span></span> 

#### <a name="internal-udp-receive"></a><span data-ttu-id="37aae-613">İç UDP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-613">Internal UDP receive</span></span>

<span data-ttu-id="37aae-614">**Simge** ![ İç U D P al simgesi](./media/user-guide/netx-events/image18.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-614">**Icon** ![Internal U D P receive icon](./media/user-guide/netx-events/image18.png)</span></span>

<span data-ttu-id="37aae-615">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-615">**Description**</span></span>

<span data-ttu-id="37aae-616">Bu olay bir iç NetX UDP alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-616">This event represents an internal NetX UDP receive event.</span></span>

<span data-ttu-id="37aae-617">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-617">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-618">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-618">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-619">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-619">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-620">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-620">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-621">Bilgi alanı 4: sözcük 0/UDP üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="37aae-621">Info Field 4: Word 0 of UDP header</span></span>

### <a name="internal-udp-send"></a><span data-ttu-id="37aae-622">İç UDP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-622">Internal UDP Send</span></span> 

#### <a name="internal-udp-send"></a><span data-ttu-id="37aae-623">İç UDP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-623">Internal UDP send</span></span>

<span data-ttu-id="37aae-624">**Simge** ![ İç U D P Gönder simgesi](./media/user-guide/netx-events/image19.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-624">**Icon** ![Internal U D P send icon](./media/user-guide/netx-events/image19.png)</span></span>

<span data-ttu-id="37aae-625">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-625">**Description**</span></span>

<span data-ttu-id="37aae-626">Bu olay bir iç NetX UDP gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-626">This event represents an internal NetX UDP send event.</span></span>

<span data-ttu-id="37aae-627">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-627">**Information Fields**</span></span>

- <span data-ttu-id="37aae-628">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-628">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-629">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-629">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-630">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-630">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-631">Bilgi alanı 4: sözcük 0/UDP üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="37aae-631">Info Field 4: Word 0 of UDP header</span></span>

### <a name="internal-rarp-receive"></a><span data-ttu-id="37aae-632">İç RARP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-632">Internal RARP Receive</span></span> 

#### <a name="internal-rarp-receive"></a><span data-ttu-id="37aae-633">İç RARP alma</span><span class="sxs-lookup"><span data-stu-id="37aae-633">Internal RARP receive</span></span> 

<span data-ttu-id="37aae-634">**Simge** ![ Dahili R A R P alma simgesi](./media/user-guide/netx-events/image20.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-634">**Icon** ![Internal R A R P receive icon](./media/user-guide/netx-events/image20.png)</span></span>

<span data-ttu-id="37aae-635">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-635">**Description**</span></span>

<span data-ttu-id="37aae-636">Bu olay bir iç NetX RARP alma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-636">This event represents an internal NetX RARP receive event.</span></span>

<span data-ttu-id="37aae-637">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-637">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-638">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-638">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-639">Bilgi alanı 2: hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-639">Info Field 2: Target IP address</span></span>
- <span data-ttu-id="37aae-640">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-640">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-641">Bilgi alanı 4: RARP üst bilgisinin kelime 1</span><span class="sxs-lookup"><span data-stu-id="37aae-641">Info Field 4: Word 1 of RARP header</span></span>

### <a name="internal-rarp-send"></a><span data-ttu-id="37aae-642">İç RARP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-642">Internal RARP Send</span></span> 

#### <a name="internal-rarp-send"></a><span data-ttu-id="37aae-643">İç RARP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-643">Internal RARP send</span></span> 

<span data-ttu-id="37aae-644">**Simge** ![ Dahili R A R P Gönder simgesi](./media/user-guide/netx-events/image21.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-644">**Icon** ![Internal R A R P send icon](./media/user-guide/netx-events/image21.png)</span></span>

<span data-ttu-id="37aae-645">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-645">**Description**</span></span>

<span data-ttu-id="37aae-646">Bu olay bir iç NetX RARP Send olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-646">This event represents an internal NetX RARP send event.</span></span>

<span data-ttu-id="37aae-647">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-647">**Information Fields**</span></span>

- <span data-ttu-id="37aae-648">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-648">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-649">Bilgi alanı 2: hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-649">Info Field 2: Target IP address</span></span>
- <span data-ttu-id="37aae-650">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-650">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-651">Bilgi alanı 4: RARP üst bilgisinin kelime 1</span><span class="sxs-lookup"><span data-stu-id="37aae-651">Info Field 4: Word 1 of RARP header</span></span>

### <a name="internal-tcp-retry"></a><span data-ttu-id="37aae-652">İç TCP yeniden denemesi</span><span class="sxs-lookup"><span data-stu-id="37aae-652">Internal TCP Retry</span></span> 

#### <a name="internal-tcp-retry"></a><span data-ttu-id="37aae-653">İç TCP yeniden denemesi</span><span class="sxs-lookup"><span data-stu-id="37aae-653">Internal TCP retry</span></span> 

<span data-ttu-id="37aae-654">**Simge** ![ İç T C P yeniden deneme simgesi](./media/user-guide/netx-events/image22.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-654">**Icon** ![Internal T C P retry icon](./media/user-guide/netx-events/image22.png)</span></span>

<span data-ttu-id="37aae-655">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-655">**Description**</span></span>

<span data-ttu-id="37aae-656">Bu olay bir iç NetX TCP yeniden deneme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-656">This event represents an internal NetX TCP retry event.</span></span>

<span data-ttu-id="37aae-657">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-657">**Information Fields**</span></span>
- <span data-ttu-id="37aae-658">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-658">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-659">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-659">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-660">Bilgi alanı 3: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-660">Info Field 3: Pointer to packet</span></span>
- <span data-ttu-id="37aae-661">Bilgi alanı 4: yeniden deneme sayısı</span><span class="sxs-lookup"><span data-stu-id="37aae-661">Info Field 4: Number of retries</span></span>

### <a name="internal-tcp-state-change"></a><span data-ttu-id="37aae-662">İç TCP durum değişikliği</span><span class="sxs-lookup"><span data-stu-id="37aae-662">Internal TCP State Change</span></span> 

#### <a name="internal-tcp-state-change"></a><span data-ttu-id="37aae-663">İç TCP durum değişikliği</span><span class="sxs-lookup"><span data-stu-id="37aae-663">Internal TCP state change</span></span> 

<span data-ttu-id="37aae-664">**Simge** ![ İç T C P durum değiştirme simgesi](./media/user-guide/netx-events/image23.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-664">**Icon** ![Internal T C P state change icon](./media/user-guide/netx-events/image23.png)</span></span>

<span data-ttu-id="37aae-665">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-665">**Description**</span></span>

<span data-ttu-id="37aae-666">Bu olay bir iç NetX TCP yuva durumu değişiklik olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-666">This event represents an internal NetX TCP socket state change event.</span></span>

<span data-ttu-id="37aae-667">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-667">**Information Fields**</span></span>

- <span data-ttu-id="37aae-668">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-668">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-669">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-669">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-670">Bilgi alanı 3: önceki durum</span><span class="sxs-lookup"><span data-stu-id="37aae-670">Info Field 3: Previous state</span></span>
- <span data-ttu-id="37aae-671">Bilgi alanı 4: yeni durum</span><span class="sxs-lookup"><span data-stu-id="37aae-671">Info Field 4: New state</span></span>

### <a name="internal-io-driver-packet-send"></a><span data-ttu-id="37aae-672">İç g/ç sürücü paketi gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-672">Internal I/O Driver Packet Send</span></span> 

#### <a name="internal-io-driver-packet-send"></a><span data-ttu-id="37aae-673">İç g/ç sürücü paketi gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-673">Internal I/O driver packet send</span></span>

<span data-ttu-id="37aae-674">**Simge** ![ İç g/ç sürücü paketi gönderme simgesi](./media/user-guide/netx-events/image24.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-674">**Icon** ![Internal I / O driver packet send icon](./media/user-guide/netx-events/image24.png)</span></span>

<span data-ttu-id="37aae-675">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-675">**Description**</span></span>

<span data-ttu-id="37aae-676">Bu olay bir iç NetX g/ç sürücü paketi gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-676">This event represents an internal NetX I/O driver packet send event.</span></span>

<span data-ttu-id="37aae-677">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-677">**Information Fields**</span></span>

- <span data-ttu-id="37aae-678">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-678">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-679">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-679">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-680">Bilgi alanı 3: paket boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-680">Info Field 3: Packet size</span></span>
- <span data-ttu-id="37aae-681">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-681">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-initialize"></a><span data-ttu-id="37aae-682">İç g/ç sürücüsü başlatma</span><span class="sxs-lookup"><span data-stu-id="37aae-682">Internal I/O Driver Initialize</span></span> 

#### <a name="internal-io-driver-initialize"></a><span data-ttu-id="37aae-683">İç g/ç sürücüsü başlatma</span><span class="sxs-lookup"><span data-stu-id="37aae-683">Internal I/O driver initialize</span></span>

<span data-ttu-id="37aae-684">**Simge** ![ İç g/ç sürücüsü başlatma simgesi](./media/user-guide/netx-events/image25.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-684">**Icon** ![Internal I / O driver initialize icon](./media/user-guide/netx-events/image25.png)</span></span>

<span data-ttu-id="37aae-685">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-685">**Description**</span></span>

<span data-ttu-id="37aae-686">Bu olay bir iç NetX g/ç sürücüsü başlatma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-686">This event represents an internal NetX I/O driver initialize event.</span></span>

<span data-ttu-id="37aae-687">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-687">**Information Fields**</span></span>

- <span data-ttu-id="37aae-688">Bilgi alanı 1: IP örneğine yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="37aae-688">Info Field 1: Pointer to the IP instance.</span></span>
- <span data-ttu-id="37aae-689">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="37aae-689">Info Field 2: Not used.</span></span>
- <span data-ttu-id="37aae-690">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="37aae-690">Info Field 3: Not used.</span></span>
- <span data-ttu-id="37aae-691">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="37aae-691">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-link-enable"></a><span data-ttu-id="37aae-692">İç g/ç sürücü bağlantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="37aae-692">Internal I/O Driver Link Enable</span></span> 

#### <a name="internal-io-driver-link-enable"></a><span data-ttu-id="37aae-693">İç g/ç sürücü bağlantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="37aae-693">Internal I/O driver link enable</span></span>

<span data-ttu-id="37aae-694">**Simge** ![ İç g/ç sürücü bağlantısı etkinleştirme simgesi](./media/user-guide/netx-events/image26.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-694">**Icon** ![Internal I / O driver link enable icon](./media/user-guide/netx-events/image26.png)</span></span>

<span data-ttu-id="37aae-695">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-695">**Description**</span></span>

<span data-ttu-id="37aae-696">Bu olay bir iç NetX g/ç sürücü bağlantısı etkinleştir olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-696">This event represents an internal NetX I/O driver link enable event.</span></span>

<span data-ttu-id="37aae-697">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-697">**Information Fields**</span></span>

- <span data-ttu-id="37aae-698">Bilgi alanı 1: IP örneğine yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="37aae-698">Info Field 1: Pointer to the IP instance.</span></span>
- <span data-ttu-id="37aae-699">Bilgi alanı 2: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="37aae-699">Info Field 2: Not used.</span></span>
- <span data-ttu-id="37aae-700">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="37aae-700">Info Field 3: Not used.</span></span>
- <span data-ttu-id="37aae-701">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="37aae-701">Info Field 4: Not used.</span></span>

### <a name="internal-io-driver-link-disable"></a><span data-ttu-id="37aae-702">İç g/ç sürücüsü bağlantısı devre dışı</span><span class="sxs-lookup"><span data-stu-id="37aae-702">Internal I/O Driver Link Disable</span></span> 

#### <a name="internal-io-driver-link-disable"></a><span data-ttu-id="37aae-703">İç g/ç sürücüsü bağlantısı devre dışı</span><span class="sxs-lookup"><span data-stu-id="37aae-703">Internal I/O driver link disable</span></span>

<span data-ttu-id="37aae-704">**Simge** ![ İç g/ç sürücü bağlantısı devre dışı simgesi](./media/user-guide/netx-events/image27.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-704">**Icon** ![Internal I / O driver link disable icon](./media/user-guide/netx-events/image27.png)</span></span>

<span data-ttu-id="37aae-705">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-705">**Description**</span></span>

<span data-ttu-id="37aae-706">Bu olay bir iç NetX g/ç sürücü bağlantısını devre dışı olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-706">This event represents an internal NetX I/O driver link disable event.</span></span>

<span data-ttu-id="37aae-707">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-707">**Information Fields**</span></span>

- <span data-ttu-id="37aae-708">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-708">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-709">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-709">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-710">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-710">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-711">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-711">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-packet-broadcast"></a><span data-ttu-id="37aae-712">İç g/ç sürücü paketi yayını</span><span class="sxs-lookup"><span data-stu-id="37aae-712">Internal I/O Driver Packet Broadcast</span></span> 

#### <a name="internal-io-driver-packet-broadcast"></a><span data-ttu-id="37aae-713">İç g/ç sürücü paketi yayını</span><span class="sxs-lookup"><span data-stu-id="37aae-713">Internal I/O driver packet broadcast</span></span>

<span data-ttu-id="37aae-714">**Simge** ![ İç g/ç sürücü paketi yayını simgesi](./media/user-guide/netx-events/image28.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-714">**Icon** ![Internal I / O driver packet broadcast icon](./media/user-guide/netx-events/image28.png)</span></span>

<span data-ttu-id="37aae-715">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-715">**Description**</span></span>

<span data-ttu-id="37aae-716">Bu olay bir iç NetX g/ç sürücü paketi yayın olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-716">This event represents an internal NetX I/O driver packet broadcast event.</span></span>

<span data-ttu-id="37aae-717">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-717">**Information Fields**</span></span>

- <span data-ttu-id="37aae-718">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-718">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-719">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-719">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-720">Bilgi alanı 3: paket boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-720">Info Field 3: Packet size</span></span>
- <span data-ttu-id="37aae-721">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-721">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-arp-send"></a><span data-ttu-id="37aae-722">İç g/ç sürücüsü ARP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-722">Internal I/O Driver ARP Send</span></span> 

#### <a name="internal-io-driver-arp-send"></a><span data-ttu-id="37aae-723">İç g/ç sürücüsü ARP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-723">Internal I/O driver ARP send</span></span>

<span data-ttu-id="37aae-724">**Simge** ![ İç g/ç sürücüsü ARP gönderme simgesi](./media/user-guide/netx-events/image29.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-724">**Icon** ![Internal I / O driver ARP send icon](./media/user-guide/netx-events/image29.png)</span></span>

<span data-ttu-id="37aae-725">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-725">**Description**</span></span>

<span data-ttu-id="37aae-726">Bu olay bir iç NetX g/ç sürücüsü ARP gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-726">This event represents an internal NetX I/O driver ARP send event.</span></span>

<span data-ttu-id="37aae-727">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-727">**Information Fields**</span></span>

- <span data-ttu-id="37aae-728">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-728">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-729">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-729">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-730">Bilgi alanı 3: paket boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-730">Info Field 3: Packet size</span></span>
- <span data-ttu-id="37aae-731">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-731">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-arp-response-send"></a><span data-ttu-id="37aae-732">İç g/ç sürücüsü ARP yanıtı gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-732">Internal I/O Driver ARP Response Send</span></span> 

#### <a name="internal-io-driver-arp-response-send"></a><span data-ttu-id="37aae-733">İç g/ç sürücüsü ARP yanıtı gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-733">Internal I/O driver ARP response send</span></span>

<span data-ttu-id="37aae-734">**Simge** ![ İç g/ç sürücüsü ARP yanıtı gönderme simgesi](./media/user-guide/netx-events/image30.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-734">**Icon** ![Internal I / O driver ARP response send icon](./media/user-guide/netx-events/image30.png)</span></span>

<span data-ttu-id="37aae-735">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-735">**Description**</span></span>

<span data-ttu-id="37aae-736">Bu olay bir iç NetX g/ç sürücüsü ARP yanıtı gönderme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-736">This event represents an internal NetX I/O driver ARP response send event.</span></span>

<span data-ttu-id="37aae-737">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-737">**Information Fields**</span></span>

- <span data-ttu-id="37aae-738">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-738">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-739">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-739">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-740">Bilgi alanı 3: paket boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-740">Info Field 3: Packet size</span></span>
- <span data-ttu-id="37aae-741">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-741">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-rarp-send"></a><span data-ttu-id="37aae-742">İç g/ç sürücüsü RARP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-742">Internal I/O Driver RARP Send</span></span> 

#### <a name="internal-io-driver-rarp-send"></a><span data-ttu-id="37aae-743">İç g/ç sürücüsü RARP gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-743">Internal I/O driver RARP send</span></span>

<span data-ttu-id="37aae-744">**Simge** ![ İç g/ç sürücüsü RARP Gönder simgesi](./media/user-guide/netx-events/image31.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-744">**Icon** ![Internal I / O driver RARP send icon](./media/user-guide/netx-events/image31.png)</span></span>

<span data-ttu-id="37aae-745">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-745">**Description**</span></span>

<span data-ttu-id="37aae-746">Bu olay bir iç NetX g/ç sürücüsü RARP Send olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-746">This event represents an internal NetX I/O driver RARP send event.</span></span>

<span data-ttu-id="37aae-747">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-747">**Information Fields**</span></span>

- <span data-ttu-id="37aae-748">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-748">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-749">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-749">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-750">Bilgi alanı 3: paket boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-750">Info Field 3: Packet size</span></span>
- <span data-ttu-id="37aae-751">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-751">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-multicast-join"></a><span data-ttu-id="37aae-752">İç g/ç sürücüsü çok noktaya yayın katılımı</span><span class="sxs-lookup"><span data-stu-id="37aae-752">Internal I/O Driver Multicast Join</span></span> 

#### <a name="internal-io-driver-multicast-join"></a><span data-ttu-id="37aae-753">İç g/ç sürücüsü çok noktaya yayın katılımı</span><span class="sxs-lookup"><span data-stu-id="37aae-753">Internal I/O driver multicast join</span></span>

<span data-ttu-id="37aae-754">**Simge** ![ İç g/ç sürücüsü çok noktaya yayın Birleştir simgesi](./media/user-guide/netx-events/image32.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-754">**Icon** ![Internal I / O driver multicast join icon](./media/user-guide/netx-events/image32.png)</span></span>

<span data-ttu-id="37aae-755">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-755">**Description**</span></span>

<span data-ttu-id="37aae-756">Bu olay bir iç NetX g/ç sürücüsü çok noktaya yayın JOIN olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-756">This event represents an internal NetX I/O driver multicast join event.</span></span>

<span data-ttu-id="37aae-757">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-757">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-758">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-758">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-759">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-759">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-760">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-760">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-761">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-761">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-multicast-leave"></a><span data-ttu-id="37aae-762">İç g/ç sürücüsü çok noktaya yayını bırakma</span><span class="sxs-lookup"><span data-stu-id="37aae-762">Internal I/O Driver Multicast Leave</span></span> 

#### <a name="internal-io-driver-multicast-leave"></a><span data-ttu-id="37aae-763">İç g/ç sürücüsü çok noktaya yayını bırakma</span><span class="sxs-lookup"><span data-stu-id="37aae-763">Internal I/O driver multicast leave</span></span>

<span data-ttu-id="37aae-764">**Simge** ![ İç g/ç sürücüsü çok noktaya yayın çıkış simgesi](./media/user-guide/netx-events/image33.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-764">**Icon** ![Internal I / O driver multicast leave icon](./media/user-guide/netx-events/image33.png)</span></span>

<span data-ttu-id="37aae-765">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-765">**Description**</span></span>

<span data-ttu-id="37aae-766">Bu olay bir iç NetX g/ç sürücüsü çok noktaya yayın çıkış olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-766">This event represents an internal NetX I/O driver multicast leave event.</span></span>

<span data-ttu-id="37aae-767">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-767">**Information Fields**</span></span>

- <span data-ttu-id="37aae-768">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-768">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-769">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-769">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-770">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-770">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-771">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-771">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-status"></a><span data-ttu-id="37aae-772">İç g/ç sürücüsü Get durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-772">Internal I/O Driver Get Status</span></span> 

#### <a name="internal-io-driver-get-status"></a><span data-ttu-id="37aae-773">İç g/ç sürücüsü Get durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-773">Internal I/O driver get status</span></span>

<span data-ttu-id="37aae-774">**Simge** ![ İç g/ç sürücüsü durum Al simgesi](./media/user-guide/netx-events/image34.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-774">**Icon** ![Internal I / O driver get status icon](./media/user-guide/netx-events/image34.png)</span></span>

<span data-ttu-id="37aae-775">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-775">**Description**</span></span>

<span data-ttu-id="37aae-776">Bu olay bir iç NetX g/ç sürücüsü al durum olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-776">This event represents an internal NetX I/O driver get status event.</span></span>

<span data-ttu-id="37aae-777">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-777">**Information Fields**</span></span>

- <span data-ttu-id="37aae-778">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-778">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-779">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-779">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-780">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-780">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-781">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-781">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-speed"></a><span data-ttu-id="37aae-782">İç g/ç sürücüsü edinme hızı</span><span class="sxs-lookup"><span data-stu-id="37aae-782">Internal I/O Driver Get Speed</span></span> 

#### <a name="internal-io-driver-get-speed"></a><span data-ttu-id="37aae-783">İç g/ç sürücüsü edinme hızı</span><span class="sxs-lookup"><span data-stu-id="37aae-783">Internal I/O driver get speed</span></span>

<span data-ttu-id="37aae-784">**Simge** ![ İç g/ç sürücüsü al hız simgesi](./media/user-guide/netx-events/image35.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-784">**Icon** ![Internal I / O driver get speed icon](./media/user-guide/netx-events/image35.png)</span></span>

<span data-ttu-id="37aae-785">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-785">**Description**</span></span>

<span data-ttu-id="37aae-786">Bu olay bir iç NetX g/ç sürücüsü al hız olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-786">This event represents an internal NetX I/O driver get speed event.</span></span>

<span data-ttu-id="37aae-787">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-787">**Information Fields**</span></span>

- <span data-ttu-id="37aae-788">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-788">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-789">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-789">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-790">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-790">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-791">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-791">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-duplex-type"></a><span data-ttu-id="37aae-792">İç g/ç sürücüsü çift yönlü türü al</span><span class="sxs-lookup"><span data-stu-id="37aae-792">Internal I/O Driver Get Duplex Type</span></span> 

#### <a name="internal-io-driver-get-duplex-type"></a><span data-ttu-id="37aae-793">İç g/ç sürücüsü çift yönlü türü al</span><span class="sxs-lookup"><span data-stu-id="37aae-793">Internal I/O driver get duplex type</span></span>

<span data-ttu-id="37aae-794">**Simge** ![ İç g/ç sürücüsü çift yönlü tür simgesi al](./media/user-guide/netx-events/image36.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-794">**Icon** ![Internal I / O driver get duplex type icon](./media/user-guide/netx-events/image36.png)</span></span>

<span data-ttu-id="37aae-795">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-795">**Description**</span></span>

<span data-ttu-id="37aae-796">Bu olay bir iç NetX g/ç sürücüsü al çift yönlü türü olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-796">This event represents an internal NetX I/O driver get duplex type event.</span></span>

<span data-ttu-id="37aae-797">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-797">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-798">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-798">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-799">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-799">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-800">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-800">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-801">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-801">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-error-count"></a><span data-ttu-id="37aae-802">İç g/ç sürücüsü hata sayısını Al</span><span class="sxs-lookup"><span data-stu-id="37aae-802">Internal I/O Driver Get Error Count</span></span>

#### <a name="internal-io-driver-get-error-count"></a><span data-ttu-id="37aae-803">İç g/ç sürücüsü hata sayısını Al</span><span class="sxs-lookup"><span data-stu-id="37aae-803">Internal I/O driver get error count</span></span>

<span data-ttu-id="37aae-804">**Simge** ![ İç g/ç sürücüsü hata sayısını Al simgesi](./media/user-guide/netx-events/image37.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-804">**Icon** ![Internal I / O driver get error count icon](./media/user-guide/netx-events/image37.png)</span></span>

<span data-ttu-id="37aae-805">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-805">**Description**</span></span>

<span data-ttu-id="37aae-806">Bu olay bir iç NetX g/ç sürücüsü Get hata sayısı olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-806">This event represents an internal NetX I/O driver get error count event.</span></span>

<span data-ttu-id="37aae-807">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-807">**Information Fields**</span></span>

- <span data-ttu-id="37aae-808">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-808">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-809">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-809">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-810">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-810">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-811">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-811">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-rx-count"></a><span data-ttu-id="37aae-812">İç g/ç sürücüsü RX sayısı al</span><span class="sxs-lookup"><span data-stu-id="37aae-812">Internal I/O Driver Get RX Count</span></span> 

#### <a name="internal-io-driver-get-rx-count"></a><span data-ttu-id="37aae-813">İç g/ç sürücüsü RX sayısı al</span><span class="sxs-lookup"><span data-stu-id="37aae-813">Internal I/O driver get RX count</span></span>

<span data-ttu-id="37aae-814">**Simge** ![ İç g/ç sürücüsü RX sayısı simgesi al](./media/user-guide/netx-events/image38.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-814">**Icon** ![Internal I / O driver get RX count icon](./media/user-guide/netx-events/image38.png)</span></span>

<span data-ttu-id="37aae-815">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-815">**Description**</span></span>

<span data-ttu-id="37aae-816">Bu olay bir iç NetX g/ç sürücüsünü, RX sayısı olayını Al ' ı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-816">This event represents an internal NetX I/O driver get RX count event.</span></span>

<span data-ttu-id="37aae-817">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-817">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-818">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-818">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-819">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-819">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-820">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-820">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-821">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-821">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-tx-count"></a><span data-ttu-id="37aae-822">İç g/ç sürücüsü TX sayısı al</span><span class="sxs-lookup"><span data-stu-id="37aae-822">Internal I/O Driver Get TX Count</span></span> 

#### <a name="internal-io-driver-get-tx-count"></a><span data-ttu-id="37aae-823">İç g/ç sürücüsü TX sayısı al</span><span class="sxs-lookup"><span data-stu-id="37aae-823">Internal I/O driver get TX count</span></span>

<span data-ttu-id="37aae-824">**Simge** ![ İç g/ç sürücüsü Get T X sayı simgesi](./media/user-guide/netx-events/image39.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-824">**Icon** ![Internal I / O driver get T X count icon](./media/user-guide/netx-events/image39.png)</span></span>

<span data-ttu-id="37aae-825">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-825">**Description**</span></span>

<span data-ttu-id="37aae-826">Bu olay bir iç NetX g/ç sürücüsü Get TX Count olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-826">This event represents an internal NetX I/O driver get TX count event.</span></span>

<span data-ttu-id="37aae-827">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-827">**Information Fields**</span></span>

- <span data-ttu-id="37aae-828">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-828">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-829">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-829">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-830">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-830">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-831">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-831">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-get-allocation-errors"></a><span data-ttu-id="37aae-832">İç g/ç sürücüsü ayırma hatalarını al</span><span class="sxs-lookup"><span data-stu-id="37aae-832">Internal I/O Driver Get Allocation Errors</span></span> 

#### <a name="internal-io-driver-get-allocation-errors"></a><span data-ttu-id="37aae-833">İç g/ç sürücüsü ayırma hatalarını al</span><span class="sxs-lookup"><span data-stu-id="37aae-833">Internal I/O driver get allocation errors</span></span>

<span data-ttu-id="37aae-834">**Simge** ![ İç g/ç sürücüsü ayırma hatalarını al simgesi](./media/user-guide/netx-events/image40.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-834">**Icon** ![Internal I / O driver get allocation errors icon](./media/user-guide/netx-events/image40.png)</span></span>

<span data-ttu-id="37aae-835">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-835">**Description**</span></span>

<span data-ttu-id="37aae-836">Bu olay bir iç NetX g/ç sürücüsü al ayırma hataları olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-836">This event represents an internal NetX I/O driver get allocation errors event.</span></span>

<span data-ttu-id="37aae-837">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-837">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-838">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-838">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-839">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-839">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-840">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-840">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-841">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-841">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-un-initialize"></a><span data-ttu-id="37aae-842">İç g/ç sürücüsü başlatması geri al</span><span class="sxs-lookup"><span data-stu-id="37aae-842">Internal I/O Driver Un-initialize</span></span> 

#### <a name="internal-io-driver-un-initialize"></a><span data-ttu-id="37aae-843">İç g/ç sürücüsü başlatması geri al</span><span class="sxs-lookup"><span data-stu-id="37aae-843">Internal I/O driver un-initialize</span></span> 

<span data-ttu-id="37aae-844">**Simge** ![ İç g/ç sürücüsü başlatması kaldır simgesi](./media/user-guide/netx-events/image41.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-844">**Icon** ![Internal I / O driver un-initialize icon](./media/user-guide/netx-events/image41.png)</span></span>

<span data-ttu-id="37aae-845">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-845">**Description**</span></span>

<span data-ttu-id="37aae-846">Bu olay bir iç NetX g/ç sürücüsü başlatma kaldırma olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-846">This event represents an internal NetX I/O driver un-initialize event.</span></span>

<span data-ttu-id="37aae-847">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-847">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-848">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-848">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-849">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-849">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-850">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-850">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-851">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-851">Info Field 4: Not used</span></span>

### <a name="internal-io-driver-deferred-processing"></a><span data-ttu-id="37aae-852">İç g/ç sürücüsü ertelenmiş Işleme</span><span class="sxs-lookup"><span data-stu-id="37aae-852">Internal I/O Driver Deferred Processing</span></span> 

#### <a name="internal-io-driver-deferred-processing"></a><span data-ttu-id="37aae-853">İç g/ç sürücüsü ertelenmiş işleme</span><span class="sxs-lookup"><span data-stu-id="37aae-853">Internal I/O driver deferred processing</span></span> 

<span data-ttu-id="37aae-854">**Simge** ![ İç g/ç sürücüsü ertelenmiş işleme simgesi](./media/user-guide/netx-events/image42.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-854">**Icon** ![Internal I / O driver deferred processing icon](./media/user-guide/netx-events/image42.png)</span></span>

<span data-ttu-id="37aae-855">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-855">**Description**</span></span>

<span data-ttu-id="37aae-856">Bu olay, bir iç NetX g/ç sürücüsü ertelenmiş işleme olayını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-856">This event represents an internal NetX I/O driver deferred processing event.</span></span>

<span data-ttu-id="37aae-857">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-857">**Information Fields**</span></span>

- <span data-ttu-id="37aae-858">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-858">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-859">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-859">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-860">Bilgi alanı 3: paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="37aae-860">Info Field 3: Packet length</span></span>
- <span data-ttu-id="37aae-861">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-861">Info Field 4: Not used</span></span>

### <a name="arp-dynamic-entries-invalidate"></a><span data-ttu-id="37aae-862">ARP dinamik girdileri geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="37aae-862">ARP Dynamic Entries Invalidate</span></span> 

#### <a name="nx_arp_dynamic_entries_invalidate"></a><span data-ttu-id="37aae-863">nx_arp_dynamic_entries_invalidate</span><span class="sxs-lookup"><span data-stu-id="37aae-863">nx_arp_dynamic_entries_invalidate</span></span>

<span data-ttu-id="37aae-864">**Simge** ![ R P dinamik girdileri geçersiz kılar simgesi](./media/user-guide/netx-events/image43.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-864">**Icon** ![A R P Dynamic Entries Invalidate icon](./media/user-guide/netx-events/image43.png)</span></span>

<span data-ttu-id="37aae-865">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-865">**Description**</span></span>

<span data-ttu-id="37aae-866">Bu olay, tüm dinamik ARP entires nx_arp_dynamic_entries_invalidate aracılığıyla geçersiz kılma gösterir.</span><span class="sxs-lookup"><span data-stu-id="37aae-866">This event represents invalidating all dynamic ARP entires via nx_arp_dynamic_entries_invalidate.</span></span>

<span data-ttu-id="37aae-867">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-867">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-868">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-868">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-869">Bilgi alanı 2: geçersiz kılınan girişler</span><span class="sxs-lookup"><span data-stu-id="37aae-869">Info Field 2: Entries invalidated</span></span>
- <span data-ttu-id="37aae-870">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-870">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-871">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-871">Info Field 4: Not used</span></span>

### <a name="arp-dynamic-entry-set"></a><span data-ttu-id="37aae-872">ARP dinamik giriş kümesi</span><span class="sxs-lookup"><span data-stu-id="37aae-872">ARP Dynamic Entry Set</span></span> 

#### <a name="nx_arp_dynamic_entry_set"></a><span data-ttu-id="37aae-873">nx_arp_dynamic_entry_set</span><span class="sxs-lookup"><span data-stu-id="37aae-873">nx_arp_dynamic_entry_set</span></span>

<span data-ttu-id="37aae-874">**Simge** ![ R P dinamik giriş kümesi simgesi](./media/user-guide/netx-events/image44.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-874">**Icon** ![A R P Dynamic Entry Set icon](./media/user-guide/netx-events/image44.png)</span></span>

<span data-ttu-id="37aae-875">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-875">**Description**</span></span>

<span data-ttu-id="37aae-876">Bu olay, nx_arp_dynamic_entry_set aracılığıyla dinamik bir ARP girişi ayarlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-876">This event represents setting a dynamic ARP entry via nx_arp_dynamic_entry_set.</span></span>

<span data-ttu-id="37aae-877">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-877">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-878">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-878">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-879">Bilgi alanı 2: IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-879">Info Field 2: IP address</span></span>
- <span data-ttu-id="37aae-880">Bilgi alanı 3: fiziksel adres (MSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-880">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="37aae-881">Bilgi alanı 4: fiziksel adres (LSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-881">Info Field 4: Physical address (LSW)</span></span>

### <a name="arp-enable"></a><span data-ttu-id="37aae-882">ARP etkinleştir</span><span class="sxs-lookup"><span data-stu-id="37aae-882">ARP Enable</span></span> 

#### <a name="nx_arp_enable"></a><span data-ttu-id="37aae-883">nx_arp_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-883">nx_arp_enable</span></span>

<span data-ttu-id="37aae-884">**Simge** ![ R P etkinleştirme simgesi](./media/user-guide/netx-events/image45.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-884">**Icon** ![A R P enable icon](./media/user-guide/netx-events/image45.png)</span></span>

<span data-ttu-id="37aae-885">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-885">**Description**</span></span>

<span data-ttu-id="37aae-886">Bu olay nx_arp_enable aracılığıyla ARP 'i etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-886">This event represents enabling ARP via nx_arp_enable.</span></span>

<span data-ttu-id="37aae-887">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-887">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-888">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-888">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-889">Bilgi alanı 2: ARP önbelleği bellek işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-889">Info Field 2: ARP cache memory pointer</span></span>
- <span data-ttu-id="37aae-890">Bilgi alanı 3: ARP önbelleği bellek boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-890">Info Field 3: ARP cache memory size</span></span>
- <span data-ttu-id="37aae-891">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-891">Info Field 4: Not used</span></span>

### <a name="arp-gratuitous-send"></a><span data-ttu-id="37aae-892">ARP gereksiz Yolus gönder</span><span class="sxs-lookup"><span data-stu-id="37aae-892">ARP Gratuitous Send</span></span> 

#### <a name="nx_arp_gratuitous_send"></a><span data-ttu-id="37aae-893">nx_arp_gratuitous_send</span><span class="sxs-lookup"><span data-stu-id="37aae-893">nx_arp_gratuitous_send</span></span>

<span data-ttu-id="37aae-894">**Simge** ![ R P gereksiz yolus Gönder simgesi](./media/user-guide/netx-events/image46.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-894">**Icon** ![A R P gratuitous send icon](./media/user-guide/netx-events/image46.png)</span></span>

<span data-ttu-id="37aae-895">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-895">**Description**</span></span>

<span data-ttu-id="37aae-896">Bu olay, nx_arp_gratuitous_send aracılığıyla gereksiz bir ARP gönderimi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-896">This event represents a gratuitous ARP send via nx_arp_gratuitous_send.</span></span>

<span data-ttu-id="37aae-897">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-897">**Information Fields**</span></span>

- <span data-ttu-id="37aae-898">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-898">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-899">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-899">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-900">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-900">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-901">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-901">Info Field 4: Not used</span></span>

### <a name="arp-hardware-address-find"></a><span data-ttu-id="37aae-902">ARP donanım adresi bulma</span><span class="sxs-lookup"><span data-stu-id="37aae-902">ARP Hardware Address Find</span></span> 

#### <a name="nx_arp_hardware_address_find"></a><span data-ttu-id="37aae-903">nx_arp_hardware_address_find</span><span class="sxs-lookup"><span data-stu-id="37aae-903">nx_arp_hardware_address_find</span></span>

<span data-ttu-id="37aae-904">**Simge** ![ R P donanım adresi bul simgesi](./media/user-guide/netx-events/image47.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-904">**Icon** ![A R P Hardware Address Find icon](./media/user-guide/netx-events/image47.png)</span></span>

<span data-ttu-id="37aae-905">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-905">**Description**</span></span>

<span data-ttu-id="37aae-906">Bu olay nx_arp_hardware_address_find aracılığıyla bir fiziksel adres bulmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-906">This event represents finding a physical address via nx_arp_hardware_address_find.</span></span>

<span data-ttu-id="37aae-907">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-907">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-908">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-908">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-909">Bilgi alanı 2: IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-909">Info Field 2: IP address</span></span>
- <span data-ttu-id="37aae-910">Bilgi alanı 3: fiziksel adres (MSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-910">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="37aae-911">Bilgi alanı 4: fiziksel adres (LSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-911">Info Field 4: Physical address (LSW)</span></span>

### <a name="arp-information-get"></a><span data-ttu-id="37aae-912">ARP bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="37aae-912">ARP Information Get</span></span> 

#### <a name="nx_arp_info_get"></a><span data-ttu-id="37aae-913">nx_arp_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-913">nx_arp_info_get</span></span>

<span data-ttu-id="37aae-914">**Simge** ![ R P veya daha fazla alma simgesi al](./media/user-guide/netx-events/image48.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-914">**Icon** ![A R P informition get icon](./media/user-guide/netx-events/image48.png)</span></span>

<span data-ttu-id="37aae-915">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-915">**Description**</span></span>

<span data-ttu-id="37aae-916">Bu olay nx_arp_info_get aracılığıyla bilgi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-916">This event represents getting information via nx_arp_info_get.</span></span>

<span data-ttu-id="37aae-917">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-917">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-918">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-918">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-919">Bilgi alanı 2: ARPs gönderilen</span><span class="sxs-lookup"><span data-stu-id="37aae-919">Info Field 2: ARPs sent</span></span>
- <span data-ttu-id="37aae-920">Bilgi alanı 3: ARP yanıtları</span><span class="sxs-lookup"><span data-stu-id="37aae-920">Info Field 3: ARP responses</span></span>
- <span data-ttu-id="37aae-921">Bilgi alanı 4: ARPs alındı</span><span class="sxs-lookup"><span data-stu-id="37aae-921">Info Field 4: ARPs received</span></span>

### <a name="arp-ip-address-find"></a><span data-ttu-id="37aae-922">ARP IP adresi bulma</span><span class="sxs-lookup"><span data-stu-id="37aae-922">ARP IP Address Find</span></span> 

#### <a name="nx_arp_ip_address_find"></a><span data-ttu-id="37aae-923">nx_arp_ip_address_find</span><span class="sxs-lookup"><span data-stu-id="37aae-923">nx_arp_ip_address_find</span></span>

<span data-ttu-id="37aae-924">**Simge** ![ R P I P adresi bul simgesi](./media/user-guide/netx-events/image49.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-924">**Icon** ![A R P I P address find icon](./media/user-guide/netx-events/image49.png)</span></span>

<span data-ttu-id="37aae-925">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-925">**Description**</span></span>

<span data-ttu-id="37aae-926">Bu olay, nx_arp_ip_address_find aracılığıyla sağlanan fiziksel adresle ilişkili bir IP adresi bulmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-926">This event represents finding an IP address associated with the supplied physical address via nx_arp_ip_address_find.</span></span>

<span data-ttu-id="37aae-927">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-927">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-928">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-928">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-929">Bilgi alanı 2: IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-929">Info Field 2: IP address</span></span>
- <span data-ttu-id="37aae-930">Bilgi alanı 3: fiziksel adres (MSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-930">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="37aae-931">Bilgi alanı 4: fiziksel adres (LSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-931">Info Field 4: Physical address (LSW)</span></span>

### <a name="arp-static-entry-create"></a><span data-ttu-id="37aae-932">ARP statik girdisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="37aae-932">ARP Static Entry Create</span></span> 

#### <a name="nx_arp_static_entry_create"></a><span data-ttu-id="37aae-933">nx_arp_static_entry_create</span><span class="sxs-lookup"><span data-stu-id="37aae-933">nx_arp_static_entry_create</span></span>

<span data-ttu-id="37aae-934">**Simge** ![ R P statik giriş oluştur simgesi](./media/user-guide/netx-events/image50.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-934">**Icon** ![A R P static entry create icon](./media/user-guide/netx-events/image50.png)</span></span>

<span data-ttu-id="37aae-935">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-935">**Description**</span></span>

<span data-ttu-id="37aae-936">Bu olay nx_arp_static_entry_create aracılığıyla statik bir ARP girişi oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-936">This event represents creating a static ARP entry via nx_arp_static_entry_create.</span></span>

<span data-ttu-id="37aae-937">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-937">**Information Fields**</span></span>

- <span data-ttu-id="37aae-938">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-938">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-939">Bilgi alanı 2: IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-939">Info Field 2: IP address</span></span>
- <span data-ttu-id="37aae-940">Bilgi alanı 3: fiziksel adres (MSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-940">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="37aae-941">Bilgi alanı 4: fiziksel adres (LSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-941">Info Field 4: Physical address (LSW)</span></span>

### <a name="arp-static-entries-delete"></a><span data-ttu-id="37aae-942">ARP statik girişleri silme</span><span class="sxs-lookup"><span data-stu-id="37aae-942">ARP Static Entries Delete</span></span> 

#### <a name="nx_arp_static_entries_delete"></a><span data-ttu-id="37aae-943">nx_arp_static_entries_delete</span><span class="sxs-lookup"><span data-stu-id="37aae-943">nx_arp_static_entries_delete</span></span>

<span data-ttu-id="37aae-944">**Simge** ![ R P statik girdileri Sil simgesi](./media/user-guide/netx-events/image51.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-944">**Icon** ![A R P static entries delete icon](./media/user-guide/netx-events/image51.png)</span></span>

<span data-ttu-id="37aae-945">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-945">**Description**</span></span>

<span data-ttu-id="37aae-946">Bu olay, tüm ARP statik girişlerinin nx_arp_static_entries_delete aracılığıyla silinmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-946">This event represents deleting all ARP static entries via nx_arp_static_entries_delete.</span></span>

<span data-ttu-id="37aae-947">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-947">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-948">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-948">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-949">Bilgi alanı 2: Silinen girdiler</span><span class="sxs-lookup"><span data-stu-id="37aae-949">Info Field 2: Entries deleted</span></span>
- <span data-ttu-id="37aae-950">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-950">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-951">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-951">Info Field 4: Not used</span></span>

### <a name="arp-static-entry-delete"></a><span data-ttu-id="37aae-952">ARP statik giriş silme</span><span class="sxs-lookup"><span data-stu-id="37aae-952">ARP Static Entry Delete</span></span> 

### <a name="nx_arp_static_entry_delete"></a><span data-ttu-id="37aae-953">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="37aae-953">nx_arp_static_entry_delete</span></span>

<span data-ttu-id="37aae-954">**Simge** ![ R P statik giriş silme simgesi](./media/user-guide/netx-events/image52.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-954">**Icon** ![A R P static entry delete icon](./media/user-guide/netx-events/image52.png)</span></span>

<span data-ttu-id="37aae-955">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-955">**Description**</span></span>

<span data-ttu-id="37aae-956">Bu olay, nx_arp_static_entry_delete aracılığıyla statik bir ARP girişini silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-956">This event represents deleting a static ARP entry via nx_arp_static_entry_delete.</span></span>

<span data-ttu-id="37aae-957">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-957">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-958">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-958">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-959">Bilgi alanı 2: IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-959">Info Field 2: IP address</span></span>
- <span data-ttu-id="37aae-960">Bilgi alanı 3: fiziksel adres (MSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-960">Info Field 3: Physical address (MSW)</span></span>
- <span data-ttu-id="37aae-961">Bilgi alanı 4: fiziksel adres (LSW)</span><span class="sxs-lookup"><span data-stu-id="37aae-961">Info Field 4: Physical address (LSW)</span></span>

### <a name="duo-cache-entry-delete"></a><span data-ttu-id="37aae-962">Duo önbellek girdisini silme</span><span class="sxs-lookup"><span data-stu-id="37aae-962">Duo Cache Entry Delete</span></span> 

#### <a name="nxd_und_cache_entry_delete"></a><span data-ttu-id="37aae-963">nxd_und_cache_entry_delete</span><span class="sxs-lookup"><span data-stu-id="37aae-963">nxd_und_cache_entry_delete</span></span>

<span data-ttu-id="37aae-964">**Simge** ![ Duo önbellek girişi silme simgesi](./media/user-guide/netx-events/image53.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-964">**Icon** ![Duo cache entry delete icon](./media/user-guide/netx-events/image53.png)</span></span>

<span data-ttu-id="37aae-965">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-965">**Description**</span></span>

<span data-ttu-id="37aae-966">Bu olay, komşu önbellek tablosundaki nx_udp_socket_create aracılığıyla bir girişi silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-966">This event represents deleting an entry in the neighbor cache table via nx_udp_socket_create.</span></span>

<span data-ttu-id="37aae-967">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-967">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-968">Bilgi alanı 1: IPv6 bağlantısı yerel adresinin silinecek dördüncü (en az önemli) kelime</span><span class="sxs-lookup"><span data-stu-id="37aae-968">Info Field 1: Fourth (least significant) word of the IPv6 link local address to delete</span></span>
- <span data-ttu-id="37aae-969">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-969">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-970">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-970">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-971">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-971">Info Field 4: Not used</span></span>

### <a name="duo-cache-entry-set"></a><span data-ttu-id="37aae-972">Duo önbellek giriş kümesi</span><span class="sxs-lookup"><span data-stu-id="37aae-972">Duo Cache Entry Set</span></span> 

#### <a name="nxd_nd_cache_entry_set"></a><span data-ttu-id="37aae-973">nxd_nd_cache_entry_set</span><span class="sxs-lookup"><span data-stu-id="37aae-973">nxd_nd_cache_entry_set</span></span>

<span data-ttu-id="37aae-974">**Simge** ![ Duo önbellek girdisi kümesi simgesi](./media/user-guide/netx-events/image54.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-974">**Icon** ![Duo cache entry set icon](./media/user-guide/netx-events/image54.png)</span></span>

<span data-ttu-id="37aae-975">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-975">**Description**</span></span>

<span data-ttu-id="37aae-976">Bu olay, bir önbellek girişi oluşturmayı ve nxd_nd_cache_entry_set aracılığıyla komşu önbelleği tablosuna eklemeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-976">This event represents creating a cache entry and adding to the neighbor cache table via nxd_nd_cache_entry_set.</span></span>

<span data-ttu-id="37aae-977">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-977">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-978">Bilgi alanı 1: eklenecek IPv6 adresinin dördüncü (en az önemli) sözcüğü</span><span class="sxs-lookup"><span data-stu-id="37aae-978">Info Field 1: Fourth (least significant) word of the IPv6 address to add</span></span>
- <span data-ttu-id="37aae-979">Bilgi alanı 2: fiziksel adres MSB</span><span class="sxs-lookup"><span data-stu-id="37aae-979">Info Field 2: Physical address msb</span></span>
- <span data-ttu-id="37aae-980">Bilgi alanı 3: fiziksel adres LSB</span><span class="sxs-lookup"><span data-stu-id="37aae-980">Info Field 3: Physical address lsb</span></span>
- <span data-ttu-id="37aae-981">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-981">Info Field 4: Not used</span></span>

### <a name="duo-cache-invalidate"></a><span data-ttu-id="37aae-982">Duo önbelleği geçersiz kıl</span><span class="sxs-lookup"><span data-stu-id="37aae-982">Duo Cache Invalidate</span></span> 

#### <a name="nxd_nd_cache_invalidate"></a><span data-ttu-id="37aae-983">nxd_nd_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="37aae-983">nxd_nd_cache_invalidate</span></span>

<span data-ttu-id="37aae-984">**Simge** ![ Duo önbelleği geçersiz kıl simgesi](./media/user-guide/netx-events/image55.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-984">**Icon** ![Duo cache invalidate icon](./media/user-guide/netx-events/image55.png)</span></span>

<span data-ttu-id="37aae-985">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-985">**Description**</span></span>

<span data-ttu-id="37aae-986">Bu olay, tüm komşu önbellek tablosunun nxd_nd_cache_invalidate aracılığıyla geçersiz kılmalarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-986">This event represents invalidating the entire neighbor cache table via nxd_nd_cache_invalidate.</span></span>

<span data-ttu-id="37aae-987">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-987">**Information Fields**</span></span>

- <span data-ttu-id="37aae-988">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-988">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-989">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-989">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-990">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-990">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-991">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-991">Info Field 4: Not used</span></span>

### <a name="duo-cache-ip-address-find"></a><span data-ttu-id="37aae-992">Duo önbelleği IP adresi bulma</span><span class="sxs-lookup"><span data-stu-id="37aae-992">Duo Cache IP Address Find</span></span> 

#### <a name="nxd_nd_cache_ip_address_find"></a><span data-ttu-id="37aae-993">nxd_nd_cache_ip_address_find</span><span class="sxs-lookup"><span data-stu-id="37aae-993">nxd_nd_cache_ip_address_find</span></span>

<span data-ttu-id="37aae-994">**Simge** ![ Duo önbelleği ı P adresi bul simgesi](./media/user-guide/netx-events/image56.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-994">**Icon** ![Duo cache I P address find icon](./media/user-guide/netx-events/image56.png)</span></span>

<span data-ttu-id="37aae-995">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-995">**Description**</span></span>

<span data-ttu-id="37aae-996">Bu olay, nxd_nd_cache_ip_address_find aracılığıyla önbellek tablosundan sağlanan fiziksel adresle eşleşen bir IP adresi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-996">This event represents retrieving an IP address matching the supplied physical address from the cache table via nxd_nd_cache_ip_address_find.</span></span>

<span data-ttu-id="37aae-997">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-997">**Information Fields**</span></span>

- <span data-ttu-id="37aae-998">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-998">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-999">Bilgi alanı 2: IPv6 adresinin dördüncü (en az önemli) sözcüğü</span><span class="sxs-lookup"><span data-stu-id="37aae-999">Info Field 2: Fourth (least significant) word of the IPv6 address</span></span>
- <span data-ttu-id="37aae-1000">Bilgi alanı 3: fiziksel adres MSB</span><span class="sxs-lookup"><span data-stu-id="37aae-1000">Info Field 3: Physical address msb</span></span>
- <span data-ttu-id="37aae-1001">Bilgi alanı 4: fiziksel adres LSB</span><span class="sxs-lookup"><span data-stu-id="37aae-1001">Info Field 4: Physical address lsb</span></span>

### <a name="duo-icmp-enable"></a><span data-ttu-id="37aae-1002">Duo ıCMP etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="37aae-1002">Duo ICMP Enable</span></span> 

#### <a name="nxd_icmp_enable"></a><span data-ttu-id="37aae-1003">nxd_icmp_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1003">nxd_icmp_enable</span></span>

<span data-ttu-id="37aae-1004">**Simge** ![ Duo ı C M P etkinleştir simgesi](./media/user-guide/netx-events/image57.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1004">**Icon** ![Duo I C M P enable icon](./media/user-guide/netx-events/image57.png)</span></span>

<span data-ttu-id="37aae-1005">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1005">**Description**</span></span>

<span data-ttu-id="37aae-1006">Bu olay, nxd_icmp_enable aracılığıyla belirtilen IP örneğinde etkinleştirilen Icmpv4 ve ICMPv6 hizmetlerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1006">This event represents ICMPv4 and ICMPv6 services being enabled on the specified IP instance via nxd_icmp_enable.</span></span>

<span data-ttu-id="37aae-1007">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1007">**Information Fields**</span></span>
- <span data-ttu-id="37aae-1008">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1008">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1009">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1009">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1010">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1010">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1011">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1011">Info Field 4: Not used</span></span>

### <a name="duo-icmp-ping"></a><span data-ttu-id="37aae-1012">Duo ıCMP ping</span><span class="sxs-lookup"><span data-stu-id="37aae-1012">Duo ICMP Ping</span></span> 

#### <a name="nxd_icmp_ping"></a><span data-ttu-id="37aae-1013">nxd_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="37aae-1013">nxd_icmp_ping</span></span>

<span data-ttu-id="37aae-1014">**Simge** ![ Duo ı C M P ping simgesi](./media/user-guide/netx-events/image58.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1014">**Icon** ![Duo I C M P ping icon](./media/user-guide/netx-events/image58.png)</span></span>

<span data-ttu-id="37aae-1015">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1015">**Description**</span></span>

<span data-ttu-id="37aae-1016">Bu olay, nxd_icmp_ping aracılığıyla bir IPv6 konağına ping (yankı isteği) göndermeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1016">This event represents sending a ping (echo request) to an IPv6 host via nxd_icmp_ping.</span></span>

<span data-ttu-id="37aae-1017">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1017">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1018">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1018">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1019">Bilgi alanı 2: IPv6 adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1019">Info Field 2: IPv6 address</span></span>
- <span data-ttu-id="37aae-1020">Bilgi alanı 3: yankı verileri Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1020">Info Field 3: Pointer to echo data</span></span>
- <span data-ttu-id="37aae-1021">Bilgi alanı 4: yankı verilerinin boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-1021">Info Field 4: Size of echo data</span></span>

### <a name="duo-ip-max-payload-size-find"></a><span data-ttu-id="37aae-1022">Duo IP en fazla yük boyutu bul</span><span class="sxs-lookup"><span data-stu-id="37aae-1022">Duo IP Max Payload Size Find</span></span> 

#### <a name="nxd_ip_max_payload_size"></a><span data-ttu-id="37aae-1023">nxd_ip_max_payload_size</span><span class="sxs-lookup"><span data-stu-id="37aae-1023">nxd_ip_max_payload_size</span></span>

<span data-ttu-id="37aae-1024">**Simge** ![ Duo ı P maks. yük boyutu bul simgesi](./media/user-guide/netx-events/image59.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1024">**Icon** ![Duo I P max payload size find icon](./media/user-guide/netx-events/image59.png)</span></span>

<span data-ttu-id="37aae-1025">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1025">**Description**</span></span>

<span data-ttu-id="37aae-1026">Bu olay, belirtilen paketin parçalanma gerekmeden taşıyabilmesi için gereken en fazla yükü hesaplar.</span><span class="sxs-lookup"><span data-stu-id="37aae-1026">This event computes the max payload the specified packet can carry without requiring fragmentation.</span></span>

<span data-ttu-id="37aae-1027">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1027">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1028">Bilgi alanı 1: yuva işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1028">Info Field 1: Socket pointer</span></span>
- <span data-ttu-id="37aae-1029">Bilgi alanı 2: eş IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1029">Info Field 2: Peer IP address</span></span>
- <span data-ttu-id="37aae-1030">Bilgi alanı 3: eş bağlantı noktası bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1030">Info Field 3: Peer port Info Field 4: Not used</span></span>

### <a name="duo-ip-raw-packet-send"></a><span data-ttu-id="37aae-1031">Duo IP ham paket gönder</span><span class="sxs-lookup"><span data-stu-id="37aae-1031">Duo IP Raw Packet Send</span></span> 

#### <a name="nxd_ip_max_packet_send"></a><span data-ttu-id="37aae-1032">nxd_ip_max_packet_send</span><span class="sxs-lookup"><span data-stu-id="37aae-1032">nxd_ip_max_packet_send</span></span>

<span data-ttu-id="37aae-1033">**Simge** ![ Duo ı P ham paket Gönder simgesi](./media/user-guide/netx-events/image60.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1033">**Icon** ![Duo I P raw packet send icon](./media/user-guide/netx-events/image60.png)</span></span>

<span data-ttu-id="37aae-1034">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1034">**Description**</span></span>

<span data-ttu-id="37aae-1035">Bu olay, nxd_ip_raw_packet_send aracılığıyla sağlanan IP hedefi adresüne belirtilen ağ arabirimini bir ham IP paketi göndermeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1035">This event represents sending a raw IP packet out the specified network interface to the supplied IP destination addressvia nxd_ip_raw_packet_send.</span></span>

<span data-ttu-id="37aae-1036">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1036">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1037">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1037">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1038">Bilgi alanı 2: gönderilmek üzere paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1038">Info Field 2: Pointer to packet to send</span></span>
- <span data-ttu-id="37aae-1039">Bilgi alanı 3: hedef adres Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1039">Info Field 3: Pointer to destination address</span></span>
- <span data-ttu-id="37aae-1040">Bilgi alanı 4: paket Protokolü</span><span class="sxs-lookup"><span data-stu-id="37aae-1040">Info Field 4: Packet protocol</span></span>

### <a name="duo-ipv6-default-router-add"></a><span data-ttu-id="37aae-1041">Duo IPv6 varsayılan yönlendirici eklentisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1041">Duo IPv6 Default Router Add</span></span> 

#### <a name="nxd_ipv6_default_router_add"></a><span data-ttu-id="37aae-1042">nxd_ipv6_default_router_add</span><span class="sxs-lookup"><span data-stu-id="37aae-1042">nxd_ipv6_default_router_add</span></span>

<span data-ttu-id="37aae-1043">**Simge** ![ Duo ı P v 6 varsayılan yönlendirici Ekle simgesi](./media/user-guide/netx-events/image61.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1043">**Icon** ![Duo I P v 6 default router add icon](./media/user-guide/netx-events/image61.png)</span></span>

<span data-ttu-id="37aae-1044">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1044">**Description**</span></span>

<span data-ttu-id="37aae-1045">Bu olay, IP örneğinin IPv6 yönlendirme tablosuna nxd_ipv6_default_router_add aracılığıyla varsayılan bir yönlendirici eklemeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1045">This event represents adding a default router to the IP instance's IPv6 routing table via nxd_ipv6_default_router_add.</span></span>

<span data-ttu-id="37aae-1046">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1046">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1047">Bilgi alanı 1: IP örneğine yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="37aae-1047">Info Field 1: Pointer to IP instance.</span></span>
- <span data-ttu-id="37aae-1048">Bilgi alanı 2: hedef ağ adresi.</span><span class="sxs-lookup"><span data-stu-id="37aae-1048">Info Field 2: Destination Network address.</span></span>
- <span data-ttu-id="37aae-1049">Bilgi alanı 3: yaşam süresi bilgileri.</span><span class="sxs-lookup"><span data-stu-id="37aae-1049">Info Field 3: Life time information.</span></span>
- <span data-ttu-id="37aae-1050">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="37aae-1050">Info Field 4: Not used.</span></span>

### <a name="duo-ipv6-default-router-delete"></a><span data-ttu-id="37aae-1051">Duo IPv6 varsayılan yönlendirici silme</span><span class="sxs-lookup"><span data-stu-id="37aae-1051">Duo IPv6 Default Router Delete</span></span> 

#### <a name="nxd_ipv6_default_router_delete"></a><span data-ttu-id="37aae-1052">nxd_ipv6_default_router_delete</span><span class="sxs-lookup"><span data-stu-id="37aae-1052">nxd_ipv6_default_router_delete</span></span>

<span data-ttu-id="37aae-1053">**Simge** ![ Duo ı P v 6 varsayılan yönlendirici silme simgesi](./media/user-guide/netx-events/image62.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1053">**Icon** ![Duo I P v 6 default router delete icon](./media/user-guide/netx-events/image62.png)</span></span>

<span data-ttu-id="37aae-1054">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1054">**Description**</span></span>

<span data-ttu-id="37aae-1055">Bu olay, IP örneğinin IPv6 yönlendirme tablosundan nxd_ipv6_default_router_delete aracılığıyla varsayılan bir yönlendiriciyi kaldırmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1055">This event represents removing a default router from the IP instance's IPv6 routing table via nxd_ipv6_default_router_delete.</span></span>

<span data-ttu-id="37aae-1056">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1056">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1057">Bilgi alanı 1: IP örneğine yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="37aae-1057">Info Field 1: Pointer to IP instance.</span></span>
- <span data-ttu-id="37aae-1058">Bilgi alanı 2: varsayılan yönlendirici IPv6 adresinin dördüncü sözcük (en az önemli).</span><span class="sxs-lookup"><span data-stu-id="37aae-1058">Info Field 2: Fourth word (least significant) of the default router IPv6 address.</span></span>
- <span data-ttu-id="37aae-1059">Bilgi alanı 3: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="37aae-1059">Info Field 3: Not used.</span></span>
- <span data-ttu-id="37aae-1060">Bilgi alanı 4: kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="37aae-1060">Info Field 4: Not used.</span></span>

### <a name="duo-ipv6-enable"></a><span data-ttu-id="37aae-1061">Duo IPv6 etkin</span><span class="sxs-lookup"><span data-stu-id="37aae-1061">Duo IPv6 Enable</span></span> 

#### <a name="nxd_ipv6_enable"></a><span data-ttu-id="37aae-1062">nxd_ipv6_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1062">nxd_ipv6_enable</span></span>

<span data-ttu-id="37aae-1063">**Simge** ![ Duo ı P v 6 etkinleştirme simgesi](./media/user-guide/netx-events/image63.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1063">**Icon** ![Duo I P v 6 enable icon](./media/user-guide/netx-events/image63.png)</span></span>

<span data-ttu-id="37aae-1064">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1064">**Description**</span></span>

<span data-ttu-id="37aae-1065">Bu olay, sağlanan IP örneğindeki nxd_ipv6_enable aracılığıyla IPv6 hizmetlerinin etkinleştirilmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1065">This event represents enabling IPv6 services on the supplied IP instance via nxd_ipv6_enable.</span></span>

<span data-ttu-id="37aae-1066">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1066">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1067">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1067">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1068">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1068">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1069">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1069">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1070">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1070">Info Field 4: Not used</span></span>

### <a name="duo-ipv6-global-address-get"></a><span data-ttu-id="37aae-1071">Duo IPv6 genel adresi al</span><span class="sxs-lookup"><span data-stu-id="37aae-1071">Duo IPv6 Global Address Get</span></span> 

#### <a name="nxd_ipv6_global_address_get"></a><span data-ttu-id="37aae-1072">nxd_ipv6_global_address_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1072">nxd_ipv6_global_address_get</span></span>

<span data-ttu-id="37aae-1073">**Simge** ![ Duo ı P v 6 genel adres al simgesi](./media/user-guide/netx-events/image64.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1073">**Icon** ![Duo I P v 6 global address get icon](./media/user-guide/netx-events/image64.png)</span></span>

<span data-ttu-id="37aae-1074">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1074">**Description**</span></span>

<span data-ttu-id="37aae-1075">Bu olay, IP örneği arabirim tablosundaki Dizin 1 ' de bulunan IP örneğindeki genel (birincil) IP adresini nxd_ipv6_global_address_get aracılığıyla almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1075">This event represents retrieving the global (primary) IP address on the IP instance located at index 1 in the IP instance interface table via nxd_ipv6_global_address_get.</span></span>

<span data-ttu-id="37aae-1076">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1076">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1077">Bilgi alanı 1: IP örneğine yönelik Işaretçi.</span><span class="sxs-lookup"><span data-stu-id="37aae-1077">Info Field 1: Pointer to IP instance.</span></span>
- <span data-ttu-id="37aae-1078">Bilgi alanı 2: genel adresin dördüncü sözcüğü (en az önemli)</span><span class="sxs-lookup"><span data-stu-id="37aae-1078">Info Field 2: Fourth word (least significant) of the global address</span></span>
- <span data-ttu-id="37aae-1079">Bilgi alanı 3: IPv6 adresi önek uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="37aae-1079">Info Field 3: IPv6 address prefix length.</span></span>
- <span data-ttu-id="37aae-1080">Bilgi alanı 4: IP arabirim tablosuna dizin (1).</span><span class="sxs-lookup"><span data-stu-id="37aae-1080">Info Field 4: Index into IP interface table (1).</span></span>

### <a name="duo-ipv6-global-address-set"></a><span data-ttu-id="37aae-1081">Duo IPv6 genel adres kümesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1081">Duo IPv6 Global Address Set</span></span> 

#### <a name="nxd_ipv6_global_address_set"></a><span data-ttu-id="37aae-1082">nxd_ipv6_global_address_set</span><span class="sxs-lookup"><span data-stu-id="37aae-1082">nxd_ipv6_global_address_set</span></span>

<span data-ttu-id="37aae-1083">**Simge** ![ Duo ı P v 6 genel adres kümesi simgesi](./media/user-guide/netx-events/image65.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1083">**Icon** ![Duo I P v 6 global address set icon](./media/user-guide/netx-events/image65.png)</span></span>

<span data-ttu-id="37aae-1084">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1084">**Description**</span></span>

<span data-ttu-id="37aae-1085">Bu olay, IP örneği arabirim tablosundaki Dizin 1 ' de bulunan IP örneğindeki genel (birincil) IP adresinin nxd_ipv6_global_address_set aracılığıyla ayarlanmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1085">This event represents setting the global (primary) IP address on the IP instance located at index 1 in the IP instance interface table via nxd_ipv6_global_address_set.</span></span>

<span data-ttu-id="37aae-1086">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1086">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1087">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1087">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1088">Bilgi alanı 2: genel adresin dördüncü sözcüğü (en az önemli)</span><span class="sxs-lookup"><span data-stu-id="37aae-1088">Info Field 2: Fourth word (least significant) of the global address</span></span>
- <span data-ttu-id="37aae-1089">Bilgi alanı 3: IPv6 adresi önek uzunluğu</span><span class="sxs-lookup"><span data-stu-id="37aae-1089">Info Field 3: IPv6 address prefix length</span></span>
- <span data-ttu-id="37aae-1090">Bilgi alanı 4: IP arabirim tablosuna dizin (1)</span><span class="sxs-lookup"><span data-stu-id="37aae-1090">Info Field 4: Index into IP interface table (1)</span></span>

### <a name="duo-ipv6-initiate-dad-process"></a><span data-ttu-id="37aae-1091">Duo IPv6, babacığım Işlemini Başlat</span><span class="sxs-lookup"><span data-stu-id="37aae-1091">Duo IPv6 Initiate Dad Process</span></span> 

#### <a name="nxd_ipv6_initiate_dad_process"></a><span data-ttu-id="37aae-1092">nxd_ipv6_initiate_dad_process</span><span class="sxs-lookup"><span data-stu-id="37aae-1092">nxd_ipv6_initiate_dad_process</span></span>

<span data-ttu-id="37aae-1093">**Simge** ![ Duo ı P v 6 babacığım işlem simgesi](./media/user-guide/netx-events/image66.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1093">**Icon** ![Duo I P v 6 initiate dad process icon](./media/user-guide/netx-events/image66.png)</span></span>

<span data-ttu-id="37aae-1094">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1094">**Description**</span></span>

<span data-ttu-id="37aae-1095">Bu olay, IP örneğine nxd_ipv6_initiate_dad_process aracılığıyla bir bağlantı yerel veya IP arabirimi adresi atandığında yinelenen adres algılama (BABACıĞıM) işleminin başlangıcını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1095">This event represents the start of the Duplicate Address Detection (DAD) process when the IP instance is assigned a link local or an IP interface address via nxd_ipv6_initiate_dad_process.</span></span>

<span data-ttu-id="37aae-1096">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1096">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1097">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1097">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1098">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1098">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1099">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1099">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1100">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1100">Info Field 4: Not used</span></span>

### <a name="duo-ipv6-interface-address-get"></a><span data-ttu-id="37aae-1101">Duo IPv6 arabirim adresi al</span><span class="sxs-lookup"><span data-stu-id="37aae-1101">Duo IPv6 Interface Address Get</span></span> 

#### <a name="nxd_ipv6_interface_address_get"></a><span data-ttu-id="37aae-1102">nxd_ipv6_interface_address_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1102">nxd_ipv6_interface_address_get</span></span>

<span data-ttu-id="37aae-1103">**Simge** ![ Duo ı P v 6 arabirim adresi al simgesi](./media/user-guide/netx-events/image67.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1103">**Icon** ![Duo I P v 6 interface address get icon](./media/user-guide/netx-events/image67.png)</span></span>

<span data-ttu-id="37aae-1104">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1104">**Description**</span></span>

<span data-ttu-id="37aae-1105">Bu olay, belirtilen dizinde IP adresi ve ön ek nxd_ipv6_interface_address_get aracılığıyla IP örneği arabirim adresi tablosuna alınması temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1105">This event represents retrieving the IP address and prefix at the specified index into the IP instance interface address table via nxd_ipv6_interface_address_get.</span></span>

<span data-ttu-id="37aae-1106">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1106">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1107">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1107">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1108">Bilgi alanı 2: döndürülecek IPv6 adresinin dördüncü sözcük (en az önemli)</span><span class="sxs-lookup"><span data-stu-id="37aae-1108">Info Field 2: Fourth word (least significant) of the IPv6 address to return</span></span>
- <span data-ttu-id="37aae-1109">Bilgi alanı 4: arabirimin IP örneği arabirim tablosuna dizini</span><span class="sxs-lookup"><span data-stu-id="37aae-1109">Info Field 4: Index of interface into the IP instance interface table</span></span>

### <a name="duo-ipv6-interface-address-set"></a><span data-ttu-id="37aae-1110">Duo IPv6 arabirimi adres kümesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1110">Duo IPv6 Interface Address Set</span></span> 

### <a name="nxd_ipv6_interface_address_set"></a><span data-ttu-id="37aae-1111">nxd_ipv6_interface_address_set</span><span class="sxs-lookup"><span data-stu-id="37aae-1111">nxd_ipv6_interface_address_set</span></span>

<span data-ttu-id="37aae-1112">**Simge** ![ Duo ı P v 6 arabirim adresiss et simgesi](./media/user-guide/netx-events/image68.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1112">**Icon** ![Duo I P v 6 interface addresss et icon](./media/user-guide/netx-events/image68.png)</span></span>

<span data-ttu-id="37aae-1113">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1113">**Description**</span></span>

<span data-ttu-id="37aae-1114">Bu olay, belirtilen dizinde IP adresi ve önekinin IP örneği arabirim adresi tablosuna ayarlanmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1114">This event represents setting the IP address and prefix at the specified index into the IP instance interface address table.</span></span> <span data-ttu-id="37aae-1115">Nxd_ipv6_interface_address_set aracılığıyla sıfır dizininde (bağlantı yerel adres) izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="37aae-1115">Not permitted on index zero (link local address) via nxd_ipv6_interface_address_set.</span></span>

<span data-ttu-id="37aae-1116">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1116">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1117">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1117">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1118">Bilgi alanı 2: döndürülecek IPv6 adresinin dördüncü sözcük (en az önemli)</span><span class="sxs-lookup"><span data-stu-id="37aae-1118">Info Field 2: Fourth word (least significant) of the IPv6 address to return</span></span>
- <span data-ttu-id="37aae-1119">Bilgi alanı 3: ön ek uzunluğu</span><span class="sxs-lookup"><span data-stu-id="37aae-1119">Info Field 3: Prefix length</span></span>
- <span data-ttu-id="37aae-1120">Bilgi alanı 4: arabirimin IP örneği arabirim tablosuna dizini</span><span class="sxs-lookup"><span data-stu-id="37aae-1120">Info Field 4: Index of interface into the IP instance interface table</span></span>

### <a name="duo-ipv6-link-local-address-get"></a><span data-ttu-id="37aae-1121">Duo IPv6 bağlantısı yerel adres Get</span><span class="sxs-lookup"><span data-stu-id="37aae-1121">Duo IPv6 Link Local Address Get</span></span> 

#### <a name="nxd_ipv6_linklocal_address_get"></a><span data-ttu-id="37aae-1122">nxd_ipv6_linklocal_address_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1122">nxd_ipv6_linklocal_address_get</span></span>

<span data-ttu-id="37aae-1123">**Simge** ![ Duo ı P v 6 bağlantısı yerel adres al simgesi](./media/user-guide/netx-events/image69.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1123">**Icon** ![Duo I P v 6 link local address get icon](./media/user-guide/netx-events/image69.png)</span></span>

<span data-ttu-id="37aae-1124">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1124">**Description**</span></span>

<span data-ttu-id="37aae-1125">Bu olay, nxd_ipv6_linklocal_address_get aracılığıyla belirtilen IP örneğinin bağlantı yerel adresini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1125">This event represents retrieving the link local address of the specified IP instance via nxd_ipv6_linklocal_address_get.</span></span>

<span data-ttu-id="37aae-1126">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1126">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1127">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1127">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1128">Bilgi alanı 2: IP V6 bağlantısı yerel adresinin dördüncü sözcük (en az önemli)</span><span class="sxs-lookup"><span data-stu-id="37aae-1128">Info Field 2: Fourth word (least significant) of the IP v6 link local address</span></span>
- <span data-ttu-id="37aae-1129">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1129">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1130">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1130">Info Field 4: Not used</span></span>

### <a name="duo-ipv6-link-local-address-set"></a><span data-ttu-id="37aae-1131">Duo IPv6 bağlantısı yerel adres kümesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1131">Duo IPv6 Link Local Address Set</span></span> 

#### <a name="nxd_ipv6_linklocal_address_set"></a><span data-ttu-id="37aae-1132">nxd_ipv6_linklocal_address_set</span><span class="sxs-lookup"><span data-stu-id="37aae-1132">nxd_ipv6_linklocal_address_set</span></span>

<span data-ttu-id="37aae-1133">**Simge** ![ Duo ı P v 6 bağlantısı yerel adres kümesi simgesi](./media/user-guide/netx-events/image70.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1133">**Icon** ![Duo I P v 6 link local address set icon](./media/user-guide/netx-events/image70.png)</span></span>

<span data-ttu-id="37aae-1134">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1134">**Description**</span></span>

<span data-ttu-id="37aae-1135">Bu olay, IP örneğinin bağlantı yerel adresini nxd_ipv6_linklocal_address_set aracılığıyla ayarlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1135">This event represents setting the link local address of the IP instance via nxd_ipv6_linklocal_address_set.</span></span>

<span data-ttu-id="37aae-1136">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1136">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1137">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1137">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1138">Bilgi alanı 2: IPv6 bağlantısı yerel adresinin dördüncü (en az önemli) sözcüğü</span><span class="sxs-lookup"><span data-stu-id="37aae-1138">Info Field 2: Fourth (least significant) word of the IPv6 link local address</span></span>
- <span data-ttu-id="37aae-1139">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1139">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1140">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1140">Info Field 4: Not used</span></span>

### <a name="duo-ipv6-raw-packet-send"></a><span data-ttu-id="37aae-1141">Duo IPv6 ham paket gönder</span><span class="sxs-lookup"><span data-stu-id="37aae-1141">Duo IPv6 Raw Packet Send</span></span> 

#### <a name="nxd_ipv6_raw_packet_send"></a><span data-ttu-id="37aae-1142">nxd_ipv6_raw_packet_send</span><span class="sxs-lookup"><span data-stu-id="37aae-1142">nxd_ipv6_raw_packet_send</span></span>

<span data-ttu-id="37aae-1143">**Simge** ![ Duo ı P v 6 ham paket Gönder simgesi](./media/user-guide/netx-events/image71.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1143">**Icon** ![Duo I P v 6 raw packet send icon](./media/user-guide/netx-events/image71.png)</span></span>

<span data-ttu-id="37aae-1144">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1144">**Description**</span></span>

<span data-ttu-id="37aae-1145">Bu olay, nxd_ip_raw_packet_send aracılığıyla bulunan hedefe yönelik birincil IP arabirimi aracılığıyla bir ham IP paketinin gönderilmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1145">This event represents sending a raw IP packet through the primary IP interface to the speficied destination via nxd_ip_raw_packet_send.</span></span>

<span data-ttu-id="37aae-1146">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1146">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1147">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1147">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1148">Bilgi alanı 2: gönderilmek üzere paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1148">Info Field 2: Pointer to packet to send</span></span>
- <span data-ttu-id="37aae-1149">Bilgi alanı 3: hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1149">Info Field 3: Destination IP address</span></span>
- <span data-ttu-id="37aae-1150">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1150">Info Field 4: Not used</span></span>

### <a name="duo-tcp-socket-peer-info-get"></a><span data-ttu-id="37aae-1151">Duo TCP yuvası eş bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="37aae-1151">Duo TCP Socket Peer Info Get</span></span> 

#### <a name="nxd_tcp_socket_peer_info_get"></a><span data-ttu-id="37aae-1152">nxd_tcp_socket_peer_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1152">nxd_tcp_socket_peer_info_get</span></span>

<span data-ttu-id="37aae-1153">**Simge** ![ Duo T C P soket eş bilgileri al simgesi](./media/user-guide/netx-events/image72.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1153">**Icon** ![Duo T C P socket peer info get icon](./media/user-guide/netx-events/image72.png)</span></span>

<span data-ttu-id="37aae-1154">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1154">**Description**</span></span>

<span data-ttu-id="37aae-1155">Bu olay, belirtilen yuvada alınan bir TCP paketindeki gönderen verilerini ayıklar.</span><span class="sxs-lookup"><span data-stu-id="37aae-1155">This event extracts the sender data from a received TCP packet on the specified socket.</span></span> <span data-ttu-id="37aae-1156">Gönderenin IP adresini ve bağlantı noktasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="37aae-1156">It returns the IP address and port of the sender.</span></span>

<span data-ttu-id="37aae-1157">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1157">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1158">Bilgi alanı 1: yuva işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1158">Info Field 1: Socket pointer</span></span>
- <span data-ttu-id="37aae-1159">Bilgi alanı 2: eş IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1159">Info Field 2: Peer IP address</span></span>
- <span data-ttu-id="37aae-1160">Bilgi alanı 3: eş bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="37aae-1160">Info Field 3: Peer port</span></span>
- <span data-ttu-id="37aae-1161">Bilgi alanı 4: IP adresinin Kiralama önemli 32-bit</span><span class="sxs-lookup"><span data-stu-id="37aae-1161">Info Field 4: The lease significant 32-bit of the IP address</span></span>

### <a name="duo-tcp-socket-set-interface"></a><span data-ttu-id="37aae-1162">Duo TCP yuva kümesi arabirimi</span><span class="sxs-lookup"><span data-stu-id="37aae-1162">Duo TCP Socket Set Interface</span></span> 

#### <a name="nxd_tcp_socket_set_interface"></a><span data-ttu-id="37aae-1163">nxd_tcp_socket_set_interface</span><span class="sxs-lookup"><span data-stu-id="37aae-1163">nxd_tcp_socket_set_interface</span></span>

<span data-ttu-id="37aae-1164">**Simge** ![ Duo T C P yuva kümesi arabirim simgesi](./media/user-guide/netx-events/image73.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1164">**Icon** ![Duo T C P socket set interface icon](./media/user-guide/netx-events/image73.png)</span></span>

<span data-ttu-id="37aae-1165">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1165">**Description**</span></span>

<span data-ttu-id="37aae-1166">Bu olay, bir istemci, belirtilen sunucu IP adresi üzerinde nxd_tcp_client_socket_connect aracılığıyla bir TCP sunucusuna bağlandıktan sonra giden yuva arabirimini ayarlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1166">This event represents setting the outgoing socket interface after a client connects with a TCP server on the specified server IP address via nxd_tcp_client_socket_connect.</span></span>

<span data-ttu-id="37aae-1167">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1167">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1168">Bilgi alanı 1: TCP yuvası Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1168">Info Field 1: Pointer to TCP Socket</span></span>
- <span data-ttu-id="37aae-1169">Bilgi alanı 2: arabirim KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="37aae-1169">Info Field 2: Interface ID</span></span>
- <span data-ttu-id="37aae-1170">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1170">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1171">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1171">Info Field 4: Not used</span></span>

### <a name="duo-udp-socket-send"></a><span data-ttu-id="37aae-1172">Duo UDP yuvası gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-1172">Duo UDP Socket Send</span></span> 

#### <a name="nxd_udp_socket_send"></a><span data-ttu-id="37aae-1173">nxd_udp_socket_send</span><span class="sxs-lookup"><span data-stu-id="37aae-1173">nxd_udp_socket_send</span></span>

<span data-ttu-id="37aae-1174">**Simge** ![ Duo U D P yuvası gönderme simgesi](./media/user-guide/netx-events/image74.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1174">**Icon** ![Duo U D P socket send icon](./media/user-guide/netx-events/image74.png)</span></span>

<span data-ttu-id="37aae-1175">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1175">**Description**</span></span>

<span data-ttu-id="37aae-1176">Bu olay, giriş IP adresi ve bağlantı noktası ile nxd_udp_socket_send aracılığıyla belirtilen yuva aracılığıyla bir UDP paketi göndermeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1176">This event represents sending a UDP packet through the specified socket with the input IP address and port via nxd_udp_socket_send.</span></span>

<span data-ttu-id="37aae-1177">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1177">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1178">Bilgi alanı 1: Işaretçi UDP yuvası</span><span class="sxs-lookup"><span data-stu-id="37aae-1178">Info Field 1: Pointer UDP Socket</span></span>
- <span data-ttu-id="37aae-1179">Bilgi alanı 2: UDP paketi Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1179">Info Field 2: Pointer to UDP packet</span></span>
- <span data-ttu-id="37aae-1180">Bilgi alanı 3: paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="37aae-1180">Info Field 3: Packet length</span></span>
- <span data-ttu-id="37aae-1181">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1181">Info Field 4: Not used</span></span>


### <a name="duo-udp-socket-set-interface"></a><span data-ttu-id="37aae-1182">Duo UDP yuva kümesi arabirimi</span><span class="sxs-lookup"><span data-stu-id="37aae-1182">Duo UDP Socket Set Interface</span></span> 

#### <a name="nxd_udp_socket_set_interface"></a><span data-ttu-id="37aae-1183">nxd_udp_socket_set_interface</span><span class="sxs-lookup"><span data-stu-id="37aae-1183">nxd_udp_socket_set_interface</span></span>

<span data-ttu-id="37aae-1184">**Simge** ![ Duo U D P yuva kümesi arabirim simgesi](./media/user-guide/netx-events/image75.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1184">**Icon** ![Duo U D P socket set interface icon](./media/user-guide/netx-events/image75.png)</span></span>

<span data-ttu-id="37aae-1185">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1185">**Description**</span></span>

<span data-ttu-id="37aae-1186">Bu olay, belirtilen UDP yuvası giden arabirimini nxd_udp_socket_set_interface aracılığıyla giriş arabirimi KIMLIĞINE karşılık gelen arabirime ayarlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1186">This event represents setting the specified UDP socket outgoing interface to the interface corresponding to the input interface ID via nxd_udp_socket_set_interface.</span></span>

<span data-ttu-id="37aae-1187">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1187">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1188">Bilgi alanı 1: UDP yuvası Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1188">Info Field 1: Pointer to UDP Socket</span></span>
- <span data-ttu-id="37aae-1189">Bilgi alanı 2: arabirim KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="37aae-1189">Info Field 2: Interface ID</span></span>
- <span data-ttu-id="37aae-1190">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1190">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1191">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1191">Info Field 4: Not used</span></span>

### <a name="duo-udp-source-extract"></a><span data-ttu-id="37aae-1192">Duo UDP kaynağı ayıklama</span><span class="sxs-lookup"><span data-stu-id="37aae-1192">Duo UDP Source Extract</span></span> 

#### <a name="nxd_udp_socket_extract"></a><span data-ttu-id="37aae-1193">nxd_udp_socket_extract</span><span class="sxs-lookup"><span data-stu-id="37aae-1193">nxd_udp_socket_extract</span></span>

<span data-ttu-id="37aae-1194">**Simge** ![ Duo U D P kaynağı ayıklama simgesi](./media/user-guide/netx-events/image76.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1194">**Icon** ![Duo U D P source extract icon](./media/user-guide/netx-events/image76.png)</span></span>

<span data-ttu-id="37aae-1195">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1195">**Description**</span></span>

<span data-ttu-id="37aae-1196">Bu olay, alınan bir paketin IP adresini ve kaynak bağlantı noktasını ayıklamayı (IPv4 veya IPv6) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1196">This event represents extracting the IP address and source port of a received packet (either IPv4 or IPv6).</span></span> <span data-ttu-id="37aae-1197">IPv6 ise, IP adresinin dördüncü sözcüğü (en az önemli) nxd_udp_source_extract aracılığıyla döndürülür.</span><span class="sxs-lookup"><span data-stu-id="37aae-1197">If IPv6, the fourth word (least significant) of the IP address is returned via nxd_udp_source_extract.</span></span>

<span data-ttu-id="37aae-1198">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1198">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1199">Bilgi alanı 1: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1199">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="37aae-1200">Bilgi alanı 2: IP sürümü</span><span class="sxs-lookup"><span data-stu-id="37aae-1200">Info Field 2: IP version</span></span>
- <span data-ttu-id="37aae-1201">Bilgi alanı 3: kaynak IP adresi (IPv4 veya IPv6)</span><span class="sxs-lookup"><span data-stu-id="37aae-1201">Info Field 3: Source IP address (IPv4 or IPv6)</span></span>
- <span data-ttu-id="37aae-1202">Bilgi alanı 4: kaynak bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="37aae-1202">Info Field 4: Source port</span></span>

### <a name="icmp-enable"></a><span data-ttu-id="37aae-1203">ICMP etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="37aae-1203">ICMP Enable</span></span> 

#### <a name="nx_icmp_enable"></a><span data-ttu-id="37aae-1204">nx_icmp_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1204">nx_icmp_enable</span></span>

<span data-ttu-id="37aae-1205">**Simge** ![ I C M P etkinleştir simgesi](./media/user-guide/netx-events/image77.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1205">**Icon** ![I C M P enable icon](./media/user-guide/netx-events/image77.png)</span></span>

<span data-ttu-id="37aae-1206">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1206">**Description**</span></span>

<span data-ttu-id="37aae-1207">Bu olay nx_icmp_enable aracılığıyla ıCMP etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1207">This event represents enabling ICMP via nx_icmp_enable.</span></span>

<span data-ttu-id="37aae-1208">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1208">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1209">Bilgi alanı 1: IP örneğinin Işaretçisi;</span><span class="sxs-lookup"><span data-stu-id="37aae-1209">Info Field 1: Pointer to the IP instance l;</span></span>
- <span data-ttu-id="37aae-1210">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1210">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1211">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1211">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1212">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1212">Info Field 4: Not used</span></span>

### <a name="icmp-information-get"></a><span data-ttu-id="37aae-1213">ICMP bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="37aae-1213">ICMP Information Get</span></span> 

#### <a name="nx_icmp_info_get"></a><span data-ttu-id="37aae-1214">nx_icmp_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1214">nx_icmp_info_get</span></span>

<span data-ttu-id="37aae-1215">**Simge** ![ I C M P bilgi al simgesi](./media/user-guide/netx-events/image78.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1215">**Icon** ![I C M P information get icon](./media/user-guide/netx-events/image78.png)</span></span>

<span data-ttu-id="37aae-1216">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1216">**Description**</span></span>

<span data-ttu-id="37aae-1217">Bu olay nx_icmp_info_get aracılığıyla bilgi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1217">This event represents getting information via nx_icmp_info_get.</span></span>

<span data-ttu-id="37aae-1218">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1218">**Information Fields**</span></span>
- <span data-ttu-id="37aae-1219">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1219">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1220">Bilgi alanı 2: gönderilen pingler</span><span class="sxs-lookup"><span data-stu-id="37aae-1220">Info Field 2: Pings sent</span></span>
- <span data-ttu-id="37aae-1221">Bilgi alanı 3: ping yanıtları</span><span class="sxs-lookup"><span data-stu-id="37aae-1221">Info Field 3: Ping responses</span></span>
- <span data-ttu-id="37aae-1222">Bilgi alanı 4: alınan pingler</span><span class="sxs-lookup"><span data-stu-id="37aae-1222">Info Field 4: Pings received</span></span>

### <a name="icmp-ping"></a><span data-ttu-id="37aae-1223">ICMP ping</span><span class="sxs-lookup"><span data-stu-id="37aae-1223">ICMP Ping</span></span> 

#### <a name="nx_icmp_ping"></a><span data-ttu-id="37aae-1224">nx_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="37aae-1224">nx_icmp_ping</span></span>

<span data-ttu-id="37aae-1225">**Simge** ![ I C M P ping simgesi](./media/user-guide/netx-events/image79.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1225">**Icon** ![I C M P ping icon](./media/user-guide/netx-events/image79.png)</span></span>

<span data-ttu-id="37aae-1226">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1226">**Description**</span></span>

<span data-ttu-id="37aae-1227">Bu olay, nx_icmp_ping aracılığıyla bir hedef IP adresinin ping komutunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1227">This event represents pinging a target IP address via nx_icmp_ping.</span></span>

<span data-ttu-id="37aae-1228">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1228">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1229">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1229">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1230">Bilgi alanı 2: IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1230">Info Field 2: IP address</span></span>
- <span data-ttu-id="37aae-1231">Bilgi alanı 3: veri Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1231">Info Field 3: Pointer to data</span></span>
- <span data-ttu-id="37aae-1232">Bilgi alanı 4: verilerin boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-1232">Info Field 4: Size of data</span></span>

### <a name="igmp-enable"></a><span data-ttu-id="37aae-1233">IGMP etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="37aae-1233">IGMP Enable</span></span> 

#### <a name="nx_icmp_enable"></a><span data-ttu-id="37aae-1234">nx_icmp_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1234">nx_icmp_enable</span></span>

<span data-ttu-id="37aae-1235">**Simge** ![ G G M P etkinleştirme simgesi](./media/user-guide/netx-events/image80.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1235">**Icon** ![I G M P enable icon](./media/user-guide/netx-events/image80.png)</span></span>

<span data-ttu-id="37aae-1236">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1236">**Description**</span></span>

<span data-ttu-id="37aae-1237">Bu olay nx_igmp_enable aracılığıyla ıGMP etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1237">This event represents enabling IGMP via nx_igmp_enable.</span></span>

<span data-ttu-id="37aae-1238">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1238">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1239">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1239">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1240">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1240">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1241">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1241">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1242">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1242">Info Field 4: Not used</span></span>

### <a name="igmp-information-get"></a><span data-ttu-id="37aae-1243">IGMP bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="37aae-1243">IGMP Information Get</span></span> 

#### <a name="nx_icmp_info_get"></a><span data-ttu-id="37aae-1244">nx_icmp_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1244">nx_icmp_info_get</span></span>

<span data-ttu-id="37aae-1245">**Simge** ![ G-M P bilgi al simgesi](./media/user-guide/netx-events/image81.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1245">**Icon** ![I G M P information get icon](./media/user-guide/netx-events/image81.png)</span></span>

<span data-ttu-id="37aae-1246">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1246">**Description**</span></span>

<span data-ttu-id="37aae-1247">Bu olay nx_igmp_info_get aracılığıyla bilgi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1247">This event represents getting information via nx_igmp_info_get.</span></span>

<span data-ttu-id="37aae-1248">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1248">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1249">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1249">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1250">Bilgi alanı 2: gönderilen raporlar</span><span class="sxs-lookup"><span data-stu-id="37aae-1250">Info Field 2: Reports sent</span></span>
- <span data-ttu-id="37aae-1251">Bilgi alanı 3: alınan sorgular</span><span class="sxs-lookup"><span data-stu-id="37aae-1251">Info Field 3: Queries received</span></span>
- <span data-ttu-id="37aae-1252">Bilgi alanı 4: eklenen gruplar</span><span class="sxs-lookup"><span data-stu-id="37aae-1252">Info Field 4: Groups joined</span></span>

### <a name="igmp-loopback-disable"></a><span data-ttu-id="37aae-1253">IGMP geri döngü devre dışı</span><span class="sxs-lookup"><span data-stu-id="37aae-1253">IGMP Loopback Disable</span></span> 

#### <a name="nx_igmp_loopback_disable"></a><span data-ttu-id="37aae-1254">nx_igmp_loopback_disable</span><span class="sxs-lookup"><span data-stu-id="37aae-1254">nx_igmp_loopback_disable</span></span>

<span data-ttu-id="37aae-1255">**Simge** ![ I G M P geri döngü devre dışı simgesi](./media/user-guide/netx-events/image82.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1255">**Icon** ![I G M P loopback disable icon](./media/user-guide/netx-events/image82.png)</span></span>

<span data-ttu-id="37aae-1256">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1256">**Description**</span></span>

<span data-ttu-id="37aae-1257">Bu olay nx_igmp_loopback_disable aracılığıyla ıGMP geri döngüsünü devre dışı bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1257">This event represents disabling IGMP loopback via nx_igmp_loopback_disable.</span></span>

<span data-ttu-id="37aae-1258">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1258">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1259">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1259">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1260">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1260">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1261">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1261">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1262">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1262">Info Field 4: Not used</span></span>

### <a name="igmp-loopback-enable"></a><span data-ttu-id="37aae-1263">IGMP geri döngü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="37aae-1263">IGMP Loopback Enable</span></span> 

#### <a name="nx_igmp_loopback_enable"></a><span data-ttu-id="37aae-1264">nx_igmp_loopback_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1264">nx_igmp_loopback_enable</span></span>

<span data-ttu-id="37aae-1265">**Simge** ![ I G M P geri döngü etkinleştirme simgesi](./media/user-guide/netx-events/image83.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1265">**Icon** ![I G M P loopback enable icon](./media/user-guide/netx-events/image83.png)</span></span>

<span data-ttu-id="37aae-1266">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1266">**Description**</span></span>

<span data-ttu-id="37aae-1267">Bu olay nx_igmp_loopback_enable aracılığıyla ıGMP geri döngüsünü etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1267">This event represents enabling IGMP loopback via nx_igmp_loopback_enable.</span></span>

<span data-ttu-id="37aae-1268">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1268">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1269">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1269">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1270">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1270">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1271">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1271">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1272">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1272">Info Field 4: Not used</span></span>

### <a name="igmp-multicast-join"></a><span data-ttu-id="37aae-1273">IGMP çok noktaya yayın katılımı</span><span class="sxs-lookup"><span data-stu-id="37aae-1273">IGMP Multicast Join</span></span> 

#### <a name="nx_igmp_multicast_join"></a><span data-ttu-id="37aae-1274">nx_igmp_multicast_join</span><span class="sxs-lookup"><span data-stu-id="37aae-1274">nx_igmp_multicast_join</span></span>

<span data-ttu-id="37aae-1275">**Simge** ![ G & urum çok noktaya yayın Birleştir simgesi](./media/user-guide/netx-events/image84.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1275">**Icon** ![I G M P multicast join icon](./media/user-guide/netx-events/image84.png)</span></span>

<span data-ttu-id="37aae-1276">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1276">**Description**</span></span>

<span data-ttu-id="37aae-1277">Bu olay, çok noktaya yayın grubunun nx_igmp_multicast_join aracılığıyla katılmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1277">This event represents joining a multicast group via nx_igmp_multicast_join.</span></span>

<span data-ttu-id="37aae-1278">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1278">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1279">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1279">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1280">Bilgi alanı 2: Grup IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1280">Info Field 2: Group IP address</span></span>
- <span data-ttu-id="37aae-1281">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1281">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1282">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1282">Info Field 4: Not used</span></span>

### <a name="igmp-multicast-leave"></a><span data-ttu-id="37aae-1283">IGMP çok noktaya yayın bırakma</span><span class="sxs-lookup"><span data-stu-id="37aae-1283">IGMP Multicast Leave</span></span> 

#### <a name="nx_igmp_multicast_leave"></a><span data-ttu-id="37aae-1284">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="37aae-1284">nx_igmp_multicast_leave</span></span>

<span data-ttu-id="37aae-1285">**Simge** ![ G & urum çok noktaya yayın çıkış simgesi](./media/user-guide/netx-events/image85.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1285">**Icon** ![I G M P multicast leave icon](./media/user-guide/netx-events/image85.png)</span></span>

<span data-ttu-id="37aae-1286">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1286">**Description**</span></span>

<span data-ttu-id="37aae-1287">Bu olay, çok noktaya yayın grubunu nx_igmp_multicast_leave aracılığıyla bırakarak temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1287">This event represents leaving a multicast group via nx_igmp_multicast_leave.</span></span>

<span data-ttu-id="37aae-1288">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1288">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1289">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1289">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1290">Bilgi alanı 2: Grup IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1290">Info Field 2: Group IP address</span></span>
- <span data-ttu-id="37aae-1291">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1291">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1292">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1292">Info Field 4: Not used</span></span>

### <a name="ip-address-change-notify"></a><span data-ttu-id="37aae-1293">IP adresi değişikliği bildirimi</span><span class="sxs-lookup"><span data-stu-id="37aae-1293">IP Address Change Notify</span></span> 

#### <a name="nx_ip_address_change_notify"></a><span data-ttu-id="37aae-1294">nx_ip_address_change_notify</span><span class="sxs-lookup"><span data-stu-id="37aae-1294">nx_ip_address_change_notify</span></span>

<span data-ttu-id="37aae-1295">**Simge** ![ I P adres değişikliği bildirim simgesi](./media/user-guide/netx-events/image86.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1295">**Icon** ![I P address change notify icon](./media/user-guide/netx-events/image86.png)</span></span>

<span data-ttu-id="37aae-1296">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1296">**Description**</span></span>

<span data-ttu-id="37aae-1297">Bu olay nx_ip_address_change_notify aracılığıyla IP değişiklik bildirimine kaydolma 'yi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1297">This event represents registering for IP change notification via nx_ip_address_change_notify.</span></span>

<span data-ttu-id="37aae-1298">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1298">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1299">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1299">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1300">Bilgi alanı 2: geri çağırma işlev işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1300">Info Field 2: Callback function pointer</span></span>
- <span data-ttu-id="37aae-1301">Bilgi alanı 3: ek bilgi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1301">Info Field 3: Additional information pointer</span></span>
- <span data-ttu-id="37aae-1302">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1302">Info Field 4: Not used</span></span>

### <a name="ip-address-get"></a><span data-ttu-id="37aae-1303">IP adresi al</span><span class="sxs-lookup"><span data-stu-id="37aae-1303">IP Address Get</span></span> 

#### <a name="nx_ip_address_get"></a><span data-ttu-id="37aae-1304">nx_ip_address_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1304">nx_ip_address_get</span></span>

<span data-ttu-id="37aae-1305">**Simge** ![ I P adresi al simgesi](./media/user-guide/netx-events/image87.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1305">**Icon** ![I P address get icon](./media/user-guide/netx-events/image87.png)</span></span>

<span data-ttu-id="37aae-1306">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1306">**Description**</span></span>

<span data-ttu-id="37aae-1307">Bu olay, IP adresinin nx_ip_address_get aracılığıyla alınmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1307">This event represents getting the IP address via nx_ip_address_get.</span></span>

<span data-ttu-id="37aae-1308">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1308">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1309">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1309">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1310">Bilgi alanı 2: IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1310">Info Field 2: IP address</span></span>
- <span data-ttu-id="37aae-1311">Bilgi alanı 3: ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1311">Info Field 3: Network mask</span></span>
- <span data-ttu-id="37aae-1312">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1312">Info Field 4: Not used</span></span>

### <a name="ip-address-set"></a><span data-ttu-id="37aae-1313">IP adresi kümesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1313">IP Address Set</span></span> 

#### <a name="nx_ip_address_set"></a><span data-ttu-id="37aae-1314">nx_ip_address_set</span><span class="sxs-lookup"><span data-stu-id="37aae-1314">nx_ip_address_set</span></span>

<span data-ttu-id="37aae-1315">**Simge** ![ I P adres kümesi simgesi](./media/user-guide/netx-events/image88.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1315">**Icon** ![I P address set icon](./media/user-guide/netx-events/image88.png)</span></span>

<span data-ttu-id="37aae-1316">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1316">**Description**</span></span>

<span data-ttu-id="37aae-1317">Bu olay, IP adresini nx_ip_address_set aracılığıyla ayarlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1317">This event represents setting the IP address via nx_ip_address_set.</span></span>

<span data-ttu-id="37aae-1318">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1318">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1319">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1319">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1320">Bilgi alanı 2: IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1320">Info Field 2: IP address</span></span>
- <span data-ttu-id="37aae-1321">Bilgi alanı 3: ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1321">Info Field 3: Network mask</span></span>
- <span data-ttu-id="37aae-1322">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1322">Info Field 4: Not used</span></span>

### <a name="ip-create"></a><span data-ttu-id="37aae-1323">IP oluşturma</span><span class="sxs-lookup"><span data-stu-id="37aae-1323">IP Create</span></span> 

#### <a name="nx_ip_create"></a><span data-ttu-id="37aae-1324">nx_ip_create</span><span class="sxs-lookup"><span data-stu-id="37aae-1324">nx_ip_create</span></span>

<span data-ttu-id="37aae-1325">**Simge** ![ I P Oluştur simgesi](./media/user-guide/netx-events/image89.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1325">**Icon** ![I P create icon](./media/user-guide/netx-events/image89.png)</span></span>

<span data-ttu-id="37aae-1326">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1326">**Description**</span></span>

<span data-ttu-id="37aae-1327">Bu olay nx_ip_create aracılığıyla bir IP örneği oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1327">This event represents creating an IP instance via nx_ip_create.</span></span>

<span data-ttu-id="37aae-1328">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1328">**Information Fields**</span></span> 
- <span data-ttu-id="37aae-1329">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1329">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1330">Bilgi alanı 2: IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1330">Info Field 2: IP address</span></span>
- <span data-ttu-id="37aae-1331">Bilgi alanı 3: ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1331">Info Field 3: Network mask</span></span>
- <span data-ttu-id="37aae-1332">Bilgi alanı 4: varsayılan paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1332">Info Field 4: Default packet pool pointer</span></span>

### <a name="ip-delete"></a><span data-ttu-id="37aae-1333">IP silme</span><span class="sxs-lookup"><span data-stu-id="37aae-1333">IP Delete</span></span> 

#### <a name="nx_ip_delete"></a><span data-ttu-id="37aae-1334">nx_ip_delete</span><span class="sxs-lookup"><span data-stu-id="37aae-1334">nx_ip_delete</span></span>

<span data-ttu-id="37aae-1335">**Simge** ![ I P Sil simgesi](./media/user-guide/netx-events/image90.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1335">**Icon** ![I P delete icon](./media/user-guide/netx-events/image90.png)</span></span>

<span data-ttu-id="37aae-1336">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1336">**Description**</span></span>

<span data-ttu-id="37aae-1337">Bu olay nx_ip_delete aracılığıyla bir IP örneğini silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1337">This event represents deleting an IP instance via nx_ip_delete.</span></span>

<span data-ttu-id="37aae-1338">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1338">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1339">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1339">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1340">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1340">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1341">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1341">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1342">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1342">Info Field 4: Not used</span></span>

### <a name="ip-driver-direct-command"></a><span data-ttu-id="37aae-1343">IP sürücüsü doğrudan komutu</span><span class="sxs-lookup"><span data-stu-id="37aae-1343">IP Driver Direct Command</span></span> 

#### <a name="nx_ip_driver_direct_command"></a><span data-ttu-id="37aae-1344">nx_ip_driver_direct_command</span><span class="sxs-lookup"><span data-stu-id="37aae-1344">nx_ip_driver_direct_command</span></span>

<span data-ttu-id="37aae-1345">**Simge** ![ I P sürücüsü doğrudan komut simgesi](./media/user-guide/netx-events/image91.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1345">**Icon** ![I P driver direct command icon](./media/user-guide/netx-events/image91.png)</span></span>

<span data-ttu-id="37aae-1346">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1346">**Description**</span></span>

<span data-ttu-id="37aae-1347">Bu olay, nx_ip_driver_direct_command aracılığıyla doğrudan g/ç sürücüsü komutunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1347">This event represents a direct I/O driver command via nx_ip_driver_direct_command.</span></span>

<span data-ttu-id="37aae-1348">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1348">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1349">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1349">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1350">Bilgi alanı 2: sürücü komutu</span><span class="sxs-lookup"><span data-stu-id="37aae-1350">Info Field 2: Driver command</span></span>
- <span data-ttu-id="37aae-1351">Bilgi alanı 3: dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="37aae-1351">Info Field 3: Return value</span></span>
- <span data-ttu-id="37aae-1352">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1352">Info Field 4: Not used</span></span>

### <a name="ip-forwarding-disable"></a><span data-ttu-id="37aae-1353">IP Iletme devre dışı</span><span class="sxs-lookup"><span data-stu-id="37aae-1353">IP Forwarding Disable</span></span> 

#### <a name="nx_ip_forwarding_disable"></a><span data-ttu-id="37aae-1354">nx_ip_forwarding_disable</span><span class="sxs-lookup"><span data-stu-id="37aae-1354">nx_ip_forwarding_disable</span></span>

<span data-ttu-id="37aae-1355">**Simge** ![ I P iletme devre dışı simgesi](./media/user-guide/netx-events/image92.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1355">**Icon** ![I P forwarding disable icon](./media/user-guide/netx-events/image92.png)</span></span>

<span data-ttu-id="37aae-1356">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1356">**Description**</span></span>

<span data-ttu-id="37aae-1357">Bu olay nx_ip_forwarding_disable aracılığıyla IP iletmeyi devre dışı bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1357">This event represents disabling IP forwarding via nx_ip_forwarding_disable.</span></span>

<span data-ttu-id="37aae-1358">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1358">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1359">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1359">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1360">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1360">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1361">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1361">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1362">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1362">Info Field 4: Not used</span></span>

### <a name="ip-forwarding-enable"></a><span data-ttu-id="37aae-1363">IP Iletme etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="37aae-1363">IP Forwarding Enable</span></span> 

#### <a name="nx_ip_forwarding_enable"></a><span data-ttu-id="37aae-1364">nx_ip_forwarding_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1364">nx_ip_forwarding_enable</span></span>

<span data-ttu-id="37aae-1365">**Simge** ![ I P iletme etkinleştirme simgesi](./media/user-guide/netx-events/image93.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1365">**Icon** ![I P forwarding enable icon](./media/user-guide/netx-events/image93.png)</span></span>

<span data-ttu-id="37aae-1366">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1366">**Description**</span></span>

<span data-ttu-id="37aae-1367">Bu olay nx_ip_forwarding_enable aracılığıyla IP iletmeyi etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1367">This event represents enabling IP forwarding via nx_ip_forwarding_enable.</span></span>

<span data-ttu-id="37aae-1368">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1368">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1369">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1369">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1370">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1370">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1371">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1371">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1372">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1372">Info Field 4: Not used</span></span>

### <a name="ip-fragment-disable"></a><span data-ttu-id="37aae-1373">IP parçası devre dışı</span><span class="sxs-lookup"><span data-stu-id="37aae-1373">IP Fragment Disable</span></span> 

#### <a name="nx_ip_fragment_disable"></a><span data-ttu-id="37aae-1374">nx_ip_fragment_disable</span><span class="sxs-lookup"><span data-stu-id="37aae-1374">nx_ip_fragment_disable</span></span>

<span data-ttu-id="37aae-1375">**Simge** ![ I P parçanız devre dışı simgesi](./media/user-guide/netx-events/image94.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1375">**Icon** ![I P fragment disable icon](./media/user-guide/netx-events/image94.png)</span></span>

<span data-ttu-id="37aae-1376">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1376">**Description**</span></span>

<span data-ttu-id="37aae-1377">Bu olay, IP fragmenting nx_ip_fragment_disable aracılığıyla devre dışı bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1377">This event represents disabling IP fragmenting via nx_ip_fragment_disable.</span></span>

<span data-ttu-id="37aae-1378">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1378">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1379">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1379">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1380">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1380">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1381">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1381">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1382">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1382">Info Field 4: Not used</span></span>

### <a name="ip-fragment-enable"></a><span data-ttu-id="37aae-1383">IP parçası etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="37aae-1383">IP Fragment Enable</span></span> 

#### <a name="nx_ip_fragment_enable"></a><span data-ttu-id="37aae-1384">nx_ip_fragment_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1384">nx_ip_fragment_enable</span></span>

<span data-ttu-id="37aae-1385">**Simge** ![ I P parçası etkinleştirme simgesi](./media/user-guide/netx-events/image95.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1385">**Icon** ![I P fragment enable icon](./media/user-guide/netx-events/image95.png)</span></span>

<span data-ttu-id="37aae-1386">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1386">**Description**</span></span>

<span data-ttu-id="37aae-1387">Bu olay, IP fragmenting nx_ip_fragment_enable aracılığıyla etkinleştirilmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1387">This event represents enabling IP fragmenting via nx_ip_fragment_enable.</span></span>

<span data-ttu-id="37aae-1388">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1388">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1389">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1389">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1390">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1390">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1391">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1391">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1392">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1392">Info Field 4: Not used</span></span>

### <a name="ip-gateway-address-set"></a><span data-ttu-id="37aae-1393">IP ağ geçidi adres kümesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1393">IP Gateway Address Set</span></span> 

#### <a name="nx_ip_gateway_address_set"></a><span data-ttu-id="37aae-1394">nx_ip_gateway_address_set</span><span class="sxs-lookup"><span data-stu-id="37aae-1394">nx_ip_gateway_address_set</span></span>

<span data-ttu-id="37aae-1395">**Simge** ![ I P ağ geçidi adres kümesi simgesi](./media/user-guide/netx-events/image96.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1395">**Icon** ![I P gateway address set icon](./media/user-guide/netx-events/image96.png)</span></span>

<span data-ttu-id="37aae-1396">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1396">**Description**</span></span>

<span data-ttu-id="37aae-1397">Bu olay, ağ geçidi IP adresini nx_ip_gateway_address_set aracılığıyla ayarlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1397">This event represents setting the gateway IP address via nx_ip_gateway_address_set.</span></span>

<span data-ttu-id="37aae-1398">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1398">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1399">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1399">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1400">Bilgi alanı 2: ağ geçidi IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1400">Info Field 2: Gateway IP address</span></span>
- <span data-ttu-id="37aae-1401">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1401">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1402">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1402">Info Field 4: Not used</span></span>

### <a name="ip-information-get"></a><span data-ttu-id="37aae-1403">IP bilgileri al</span><span class="sxs-lookup"><span data-stu-id="37aae-1403">IP Information Get</span></span> 

#### <a name="nx_ip_info_get"></a><span data-ttu-id="37aae-1404">nx_ip_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1404">nx_ip_info_get</span></span>

<span data-ttu-id="37aae-1405">**Simge** ![ I P bilgileri al simgesi](./media/user-guide/netx-events/image97.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1405">**Icon** ![I P information get icon](./media/user-guide/netx-events/image97.png)</span></span>

<span data-ttu-id="37aae-1406">**Açıklama** Bu olay nx_ip_info_get aracılığıyla IP bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1406">**Description** This event represents getting IP information via nx_ip_info_get.</span></span>

<span data-ttu-id="37aae-1407">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1407">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1408">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1408">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1409">Bilgi alanı 2: gönderilen IP baytları</span><span class="sxs-lookup"><span data-stu-id="37aae-1409">Info Field 2: IP bytes sent</span></span>
- <span data-ttu-id="37aae-1410">Bilgi alanı 3: alınan IP baytları</span><span class="sxs-lookup"><span data-stu-id="37aae-1410">Info Field 3: IP bytes received</span></span>
- <span data-ttu-id="37aae-1411">Bilgi alanı 4: IP paketleri bırakıldı</span><span class="sxs-lookup"><span data-stu-id="37aae-1411">Info Field 4: IP packets dropped</span></span>

### <a name="ip-interface-attach"></a><span data-ttu-id="37aae-1412">IP arabirimi Iliştirme</span><span class="sxs-lookup"><span data-stu-id="37aae-1412">IP Interface Attach</span></span> 

#### <a name="nx_interface_attach"></a><span data-ttu-id="37aae-1413">nx_interface_attach</span><span class="sxs-lookup"><span data-stu-id="37aae-1413">nx_interface_attach</span></span>

<span data-ttu-id="37aae-1414">**Simge** ![ I P iteryüz iliştirme simgesi](./media/user-guide/netx-events/image98.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1414">**Icon** ![I P iterface attach icon](./media/user-guide/netx-events/image98.png)</span></span>

<span data-ttu-id="37aae-1415">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1415">**Description**</span></span>

<span data-ttu-id="37aae-1416">Bu olay, IP örneğine eklenen bir ikincil ağ arabirimini nx_ip_interface_attach aracılığıyla temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1416">This event represents a secondary network interface being attached to the IP instance via nx_ip_interface_attach.</span></span>

<span data-ttu-id="37aae-1417">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1417">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1418">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1418">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1419">Bilgi alanı 2: Arabirim IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1419">Info Field 2: Interface IP Address</span></span>
- <span data-ttu-id="37aae-1420">Bilgi alanı 3: IP arabirim tablosuna Dizin</span><span class="sxs-lookup"><span data-stu-id="37aae-1420">Info Field 3: Index into IP interface table</span></span>
- <span data-ttu-id="37aae-1421">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1421">Info Field 4: Not used</span></span>

### <a name="ip-interface-info-get"></a><span data-ttu-id="37aae-1422">IP arabirimi bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="37aae-1422">IP Interface Info Get</span></span> 

#### <a name="nx_ip_interface_info_get"></a><span data-ttu-id="37aae-1423">nx_ip_interface_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1423">nx_ip_interface_info_get</span></span>

<span data-ttu-id="37aae-1424">**Simge** ![ IP arabirimi bilgileri al simgesi](./media/user-guide/netx-events/image99.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1424">**Icon** ![ IP interface info get icon](./media/user-guide/netx-events/image99.png)</span></span>

<span data-ttu-id="37aae-1425">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1425">**Description**</span></span>

<span data-ttu-id="37aae-1426">Bu olay, nx_ip_interface_info_get aracılığıyla belirtilen ağ arabiriminden alınan bilgileri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1426">This event represents information retrieved from the specified network interface via nx_ip_interface_info_get.</span></span>

<span data-ttu-id="37aae-1427">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1427">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1428">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1428">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1429">Bilgi alanı 2: Arabirim IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1429">Info Field 2: Interface IP address</span></span>
- <span data-ttu-id="37aae-1430">Bilgi alanı 3: arabirim MAC adresi MSB</span><span class="sxs-lookup"><span data-stu-id="37aae-1430">Info Field 3: Interface MAC address msb</span></span>
- <span data-ttu-id="37aae-1431">Bilgi alanı 4: arabirim MAC adresi LSB</span><span class="sxs-lookup"><span data-stu-id="37aae-1431">Info Field 4: Interface MAC address lsb</span></span>

### <a name="ip-raw-packet-disable"></a><span data-ttu-id="37aae-1432">IP ham paket devre dışı</span><span class="sxs-lookup"><span data-stu-id="37aae-1432">IP Raw Packet Disable</span></span> 

#### <a name="nx_ip_raw_packet_disable"></a><span data-ttu-id="37aae-1433">nx_ip_raw_packet_disable</span><span class="sxs-lookup"><span data-stu-id="37aae-1433">nx_ip_raw_packet_disable</span></span>

<span data-ttu-id="37aae-1434">**Simge** ![ I P ham paket devre dışı simgesi](./media/user-guide/netx-events/image100.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1434">**Icon** ![I P raw packet disable icon](./media/user-guide/netx-events/image100.png)</span></span>

<span data-ttu-id="37aae-1435">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1435">**Description**</span></span>

<span data-ttu-id="37aae-1436">Bu olay, ham IP paket iletişimini nx_ip_raw_packet_disable aracılığıyla devre dışı bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1436">This event represents disabling raw IP packet communication via nx_ip_raw_packet_disable.</span></span>

<span data-ttu-id="37aae-1437">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1437">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1438">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1438">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1439">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1439">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1440">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1440">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1441">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1441">Info Field 4: Not used</span></span>

### <a name="ip-raw-packet-enable"></a><span data-ttu-id="37aae-1442">IP ham paket etkinleştir</span><span class="sxs-lookup"><span data-stu-id="37aae-1442">IP Raw Packet Enable</span></span> 

#### <a name="nx_ip_raw_packet_enable"></a><span data-ttu-id="37aae-1443">nx_ip_raw_packet_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1443">nx_ip_raw_packet_enable</span></span>

<span data-ttu-id="37aae-1444">**Simge** ![ I P RAW paketi etkinleştirme simgesi](./media/user-guide/netx-events/image101.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1444">**Icon** ![I P raw packet enable icon](./media/user-guide/netx-events/image101.png)</span></span>

<span data-ttu-id="37aae-1445">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1445">**Description**</span></span>

<span data-ttu-id="37aae-1446">Bu olay, ham IP paket iletişimini nx_ip_raw_packet_enable aracılığıyla etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1446">This event represents enabling raw IP packet communication via nx_ip_raw_packet_enable.</span></span>

<span data-ttu-id="37aae-1447">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1447">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1448">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1448">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1449">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1449">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1450">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1450">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1451">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1451">Info Field 4: Not used</span></span>

### <a name="ip-raw-packet-receive"></a><span data-ttu-id="37aae-1452">IP ham paket alma</span><span class="sxs-lookup"><span data-stu-id="37aae-1452">IP Raw Packet Receive</span></span> 

#### <a name="nx_ip_raw_packet_receive"></a><span data-ttu-id="37aae-1453">nx_ip_raw_packet_receive</span><span class="sxs-lookup"><span data-stu-id="37aae-1453">nx_ip_raw_packet_receive</span></span>

<span data-ttu-id="37aae-1454">**Simge** ![ I P ham paket alma simgesi](./media/user-guide/netx-events/image102.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1454">**Icon** ![I P raw packet receive icon](./media/user-guide/netx-events/image102.png)</span></span>

<span data-ttu-id="37aae-1455">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1455">**Description**</span></span>

<span data-ttu-id="37aae-1456">Bu olay nx_ip_raw_packet_receive aracılığıyla ham IP paketi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1456">This event represents receiving a raw IP packet via nx_ip_raw_packet_receive.</span></span>

<span data-ttu-id="37aae-1457">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1457">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1458">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1458">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1459">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1459">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-1460">Bilgi alanı 3: bekleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="37aae-1460">Info Field 3: Wait option</span></span>
- <span data-ttu-id="37aae-1461">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1461">Info Field 4: Not used</span></span>

### <a name="ip-raw-packet-send"></a><span data-ttu-id="37aae-1462">IP ham paket gönder</span><span class="sxs-lookup"><span data-stu-id="37aae-1462">IP Raw Packet Send</span></span> 

#### <a name="nx_ip_raw_packet_send"></a><span data-ttu-id="37aae-1463">nx_ip_raw_packet_send</span><span class="sxs-lookup"><span data-stu-id="37aae-1463">nx_ip_raw_packet_send</span></span>

<span data-ttu-id="37aae-1464">**Simge** ![ I P ham paket Gönder simgesi](./media/user-guide/netx-events/image103.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1464">**Icon** ![I P raw packet send icon](./media/user-guide/netx-events/image103.png)</span></span>

<span data-ttu-id="37aae-1465">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1465">**Description**</span></span>

<span data-ttu-id="37aae-1466">Bu olay, ham IP paketini nx_ip_raw_packet_send aracılığıyla göndermeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1466">This event represents sending a raw IP packet via nx_ip_raw_packet_send.</span></span>

<span data-ttu-id="37aae-1467">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1467">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1468">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1468">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1469">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1469">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-1470">Bilgi alanı 3: hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1470">Info Field 3: Destination IP address</span></span>
- <span data-ttu-id="37aae-1471">Bilgi alanı 4: hizmet türü</span><span class="sxs-lookup"><span data-stu-id="37aae-1471">Info Field 4: Type of service</span></span>

### <a name="ip-static-route-add"></a><span data-ttu-id="37aae-1472">IP statik yol ekleme</span><span class="sxs-lookup"><span data-stu-id="37aae-1472">IP Static Route Add</span></span> 

#### <a name="nx_ip_static_route_add"></a><span data-ttu-id="37aae-1473">nx_ip_static_route_add</span><span class="sxs-lookup"><span data-stu-id="37aae-1473">nx_ip_static_route_add</span></span>

<span data-ttu-id="37aae-1474">**Simge** ![ I P statik yol ekleme simgesi](./media/user-guide/netx-events/image104.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1474">**Icon** ![I P static route add icon](./media/user-guide/netx-events/image104.png)</span></span>

<span data-ttu-id="37aae-1475">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1475">**Description**</span></span>

<span data-ttu-id="37aae-1476">Bu olay, nx_ip_static_route_add aracılığıyla IP örneği yönlendirme tablosuna eklenmekte olan statik bir yolu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1476">This event represents a static route being added to the IP instance routing table via nx_ip_static_route_add.</span></span>

<span data-ttu-id="37aae-1477">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1477">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1478">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1478">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1479">Bilgi alanı 2: ağ adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1479">Info Field 2: Network address</span></span>
- <span data-ttu-id="37aae-1480">Bilgi alanı 3: ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1480">Info Field 3: Network mask</span></span>
- <span data-ttu-id="37aae-1481">Bilgi alanı 4: sonraki atlama</span><span class="sxs-lookup"><span data-stu-id="37aae-1481">Info Field 4: Next hop</span></span>

### <a name="ip-static-route-delete"></a><span data-ttu-id="37aae-1482">IP statik yol silme</span><span class="sxs-lookup"><span data-stu-id="37aae-1482">IP Static Route Delete</span></span> 

#### <a name="nx_ip_static_route_delete"></a><span data-ttu-id="37aae-1483">nx_ip_static_route_delete</span><span class="sxs-lookup"><span data-stu-id="37aae-1483">nx_ip_static_route_delete</span></span>

<span data-ttu-id="37aae-1484">**Simge** ![ I P statik Rute silme simgesi](./media/user-guide/netx-events/image105.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1484">**Icon** ![I P static rute delete icon](./media/user-guide/netx-events/image105.png)</span></span>

<span data-ttu-id="37aae-1485">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1485">**Description**</span></span>

<span data-ttu-id="37aae-1486">Bu olay, nx_ip_static_route_delete aracılığıyla IP örneği yönlendirme tablosundan çıkarılan statik bir yolu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1486">This event represents a static route being removed from the IP instance routing table via nx_ip_static_route_delete.</span></span>

<span data-ttu-id="37aae-1487">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1487">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1488">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1488">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1489">Bilgi alanı 2: ağ adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1489">Info Field 2: Network address</span></span>
- <span data-ttu-id="37aae-1490">Bilgi alanı 3: ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1490">Info Field 3: Network mask</span></span>
- <span data-ttu-id="37aae-1491">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1491">Info Field 4: Not used</span></span>

### <a name="ip-status-check"></a><span data-ttu-id="37aae-1492">IP durum denetimi</span><span class="sxs-lookup"><span data-stu-id="37aae-1492">IP Status Check</span></span> 

#### <a name="nx_ip_status_check"></a><span data-ttu-id="37aae-1493">nx_ip_status_check</span><span class="sxs-lookup"><span data-stu-id="37aae-1493">nx_ip_status_check</span></span>

<span data-ttu-id="37aae-1494">**Simge** ![ I P durum denetimi simgesi](./media/user-guide/netx-events/image106.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1494">**Icon** ![I P status check icon](./media/user-guide/netx-events/image106.png)</span></span>

<span data-ttu-id="37aae-1495">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1495">**Description**</span></span>

<span data-ttu-id="37aae-1496">Bu olay nx_ip_status_check aracılığıyla bir IP durumunun denetlenmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1496">This event represents checking for an IP status via nx_ip_status_check.</span></span>

<span data-ttu-id="37aae-1497">Bilgi alanları</span><span class="sxs-lookup"><span data-stu-id="37aae-1497">Information Fields</span></span> 

- <span data-ttu-id="37aae-1498">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1498">Info Field 1: Pointer to the IP instance</span></span>
- <span data-ttu-id="37aae-1499">Bilgi alanı 2: Istenen durum</span><span class="sxs-lookup"><span data-stu-id="37aae-1499">Info Field 2: Requested status</span></span>
- <span data-ttu-id="37aae-1500">Bilgi alanı 3: gerçek durum</span><span class="sxs-lookup"><span data-stu-id="37aae-1500">Info Field 3: Actual status</span></span>
- <span data-ttu-id="37aae-1501">Bilgi alanı 4: bekleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="37aae-1501">Info Field 4: Wait option</span></span>

### <a name="ipsec-enable"></a><span data-ttu-id="37aae-1502">IPSEC etkin</span><span class="sxs-lookup"><span data-stu-id="37aae-1502">IPSEC Enable</span></span> 

#### <a name="nx_ipsec_enable"></a><span data-ttu-id="37aae-1503">nx_ipsec_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1503">nx_ipsec_enable</span></span>

<span data-ttu-id="37aae-1504">**Simge** ![ I P S E C etkinleştir simgesi](./media/user-guide/netx-events/image107.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1504">**Icon** ![I P S E C enable icon](./media/user-guide/netx-events/image107.png)</span></span>

<span data-ttu-id="37aae-1505">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1505">**Description**</span></span>

<span data-ttu-id="37aae-1506">Bu olay, sağlanan IP örneğindeki nx_ipsec_enable aracılığıyla IPSec hizmetlerinin etkinleştirilmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1506">This event represents enabling IPSec services on the supplied IP instance via nx_ipsec_enable.</span></span>

<span data-ttu-id="37aae-1507">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1507">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1508">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1508">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1509">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1509">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1510">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1510">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1511">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1511">Info Field 4: Not used</span></span>

### <a name="packet-allocate"></a><span data-ttu-id="37aae-1512">Paket ayırma</span><span class="sxs-lookup"><span data-stu-id="37aae-1512">Packet Allocate</span></span> 

#### <a name="nx_packet_allocate"></a><span data-ttu-id="37aae-1513">nx_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="37aae-1513">nx_packet_allocate</span></span>

<span data-ttu-id="37aae-1514">**Simge** ![ Paket ayırma simgesi](./media/user-guide/netx-events/image108.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1514">**Icon** ![Packet allocate icon](./media/user-guide/netx-events/image108.png)</span></span>

<span data-ttu-id="37aae-1515">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1515">**Description**</span></span>

<span data-ttu-id="37aae-1516">Bu olay nx_packet_allocate aracılığıyla bir paket ayırmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1516">This event represents allocating a packet via nx_packet_allocate.</span></span>

<span data-ttu-id="37aae-1517">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1517">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1518">Bilgi alanı 1: paket havuzuna yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1518">Info Field 1: Pointer to the packet pool</span></span>
- <span data-ttu-id="37aae-1519">Bilgi alanı 2: ayrılmış paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1519">Info Field 2: Pointer to packet allocated</span></span>
- <span data-ttu-id="37aae-1520">Bilgi alanı 3: paket türü</span><span class="sxs-lookup"><span data-stu-id="37aae-1520">Info Field 3: Packet type</span></span>
- <span data-ttu-id="37aae-1521">Bilgi alanı 4: kullanılabilir paketler</span><span class="sxs-lookup"><span data-stu-id="37aae-1521">Info Field 4: Available packets</span></span>

### <a name="packet-copy"></a><span data-ttu-id="37aae-1522">Paket kopyası</span><span class="sxs-lookup"><span data-stu-id="37aae-1522">Packet Copy</span></span> 

#### <a name="nx_packet_copy"></a><span data-ttu-id="37aae-1523">nx_packet_copy</span><span class="sxs-lookup"><span data-stu-id="37aae-1523">nx_packet_copy</span></span>

<span data-ttu-id="37aae-1524">**Simge** ![ Paket CPY simgesi](./media/user-guide/netx-events/image109.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1524">**Icon** ![Packet cpy icon](./media/user-guide/netx-events/image109.png)</span></span>

<span data-ttu-id="37aae-1525">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1525">**Description**</span></span>

<span data-ttu-id="37aae-1526">Bu olay, bir paketin nx_packet_copy aracılığıyla kopyalanmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1526">This event represents copying a packet via nx_packet_copy.</span></span>

<span data-ttu-id="37aae-1527">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1527">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1528">Bilgi alanı 2: yeni paket işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1528">Info Field 2: New packet pointer</span></span>
- <span data-ttu-id="37aae-1529">Bilgi alanı 3: paket havuzu Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1529">Info Field 3: Pointer to packet pool</span></span>
- <span data-ttu-id="37aae-1530">Bilgi alanı 4: bekleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="37aae-1530">Info Field 4: Wait option</span></span>

### <a name="packet-data-append"></a><span data-ttu-id="37aae-1531">Paket verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="37aae-1531">Packet Data Append</span></span> 

#### <a name="nx_packet_data_append"></a><span data-ttu-id="37aae-1532">nx_packet_data_append</span><span class="sxs-lookup"><span data-stu-id="37aae-1532">nx_packet_data_append</span></span>

<span data-ttu-id="37aae-1533">**Simge** ![ Paket verileri ekleme simgesi](./media/user-guide/netx-events/image110.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1533">**Icon** ![Packet data append icon](./media/user-guide/netx-events/image110.png)</span></span>

<span data-ttu-id="37aae-1534">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1534">**Description**</span></span>

<span data-ttu-id="37aae-1535">Bu olay nx_packet_data_append aracılığıyla bir pakete veri eklemeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1535">This event represents appending data to a packet via nx_packet_data_append.</span></span>

<span data-ttu-id="37aae-1536">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1536">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1537">Bilgi alanı 1: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1537">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="37aae-1538">Bilgi alanı 2: veri Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1538">Info Field 2: Pointer to data</span></span>
- <span data-ttu-id="37aae-1539">Bilgi alanı 3: veri boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-1539">Info Field 3: Size of data</span></span>
- <span data-ttu-id="37aae-1540">Bilgi alanı 4: paket havuzuna yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1540">Info Field 4: Pointer to packet pool</span></span>

### <a name="packet-data-extract-offset"></a><span data-ttu-id="37aae-1541">Paket verisi ayıklama kayması</span><span class="sxs-lookup"><span data-stu-id="37aae-1541">Packet Data Extract Offset</span></span> 

#### <a name="nx_udp_source_extract_offset"></a><span data-ttu-id="37aae-1542">nx_udp_source_extract_offset</span><span class="sxs-lookup"><span data-stu-id="37aae-1542">nx_udp_source_extract_offset</span></span>

<span data-ttu-id="37aae-1543">**Simge** ![ Paket verileri ayıklama fark simgesi](./media/user-guide/netx-events/image111.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1543">**Icon** ![Packet data extract offset icon](./media/user-guide/netx-events/image111.png)</span></span>

<span data-ttu-id="37aae-1544">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1544">**Description**</span></span>

<span data-ttu-id="37aae-1545">Bu olay, nx_udp_source_extract_offset aracılığıyla bir paketten sağlanan bir arabelleğe ayıklanan paket verilerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1545">This event represents packet data that is extracted into a supplied buffer from a packet via nx_udp_source_extract_offset.</span></span>

<span data-ttu-id="37aae-1546">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1546">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1547">Bilgi alanı 1: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1547">Info Field 1: Pointer to packet</span></span>
- <span data-ttu-id="37aae-1548">Bilgi alanı 2: belirtilen arabelleğin boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-1548">Info Field 2: Size of specified buffer</span></span>
- <span data-ttu-id="37aae-1549">Bilgi alanı 3: kopyalanmış bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="37aae-1549">Info Field 3: Number of bytes copied</span></span>
- <span data-ttu-id="37aae-1550">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1550">Info Field 4: Not used</span></span>

### <a name="packet-data-retrieve"></a><span data-ttu-id="37aae-1551">Paket verilerini alma</span><span class="sxs-lookup"><span data-stu-id="37aae-1551">Packet Data Retrieve</span></span> 

#### <a name="nx_packet_data_retrieve"></a><span data-ttu-id="37aae-1552">nx_packet_data_retrieve</span><span class="sxs-lookup"><span data-stu-id="37aae-1552">nx_packet_data_retrieve</span></span>

<span data-ttu-id="37aae-1553">**Simge** ![ Paket verilerini alma simgesi](./media/user-guide/netx-events/image112.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1553">**Icon** ![Packet data retrieve icon](./media/user-guide/netx-events/image112.png)</span></span>

<span data-ttu-id="37aae-1554">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1554">**Description**</span></span>

<span data-ttu-id="37aae-1555">Bu olay nx_packet_data_retrieve aracılığıyla bir paketten veri almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1555">This event represents retrieving data from a packet via nx_packet_data_retrieve.</span></span>

<span data-ttu-id="37aae-1556">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1556">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1557">Bilgi alanı 1: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1557">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="37aae-1558">Bilgi alanı 2: arabelleğin başlangıcına yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1558">Info Field 2: Pointer to start of buffer</span></span>
- <span data-ttu-id="37aae-1559">Bilgi alanı 3: bayt kopyalanmış</span><span class="sxs-lookup"><span data-stu-id="37aae-1559">Info Field 3: Bytes copied</span></span>
- <span data-ttu-id="37aae-1560">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1560">Info Field 4: Not used</span></span>

### <a name="packet-length-get"></a><span data-ttu-id="37aae-1561">Paket uzunluğu al</span><span class="sxs-lookup"><span data-stu-id="37aae-1561">Packet Length Get</span></span> 

#### <a name="nx_packet_length_get"></a><span data-ttu-id="37aae-1562">nx_packet_length_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1562">nx_packet_length_get</span></span>

<span data-ttu-id="37aae-1563">**Simge** ![ Paket uzunluğu al simgesi](./media/user-guide/netx-events/image113.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1563">**Icon** ![Packet length get icon](./media/user-guide/netx-events/image113.png)</span></span>

<span data-ttu-id="37aae-1564">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1564">**Description**</span></span>

<span data-ttu-id="37aae-1565">Bu olay, nx_packet_length_get aracılığıyla bir paketin uzunluğunu almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1565">This event represents getting the length of a packet via nx_packet_length_get.</span></span>

<span data-ttu-id="37aae-1566">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1566">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1567">Bilgi alanı 1: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1567">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="37aae-1568">Bilgi alanı 2: paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="37aae-1568">Info Field 2: Packet length</span></span>
- <span data-ttu-id="37aae-1569">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1569">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1570">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1570">Info Field 4: Not used</span></span>

### <a name="packet-pool-create"></a><span data-ttu-id="37aae-1571">Paket havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="37aae-1571">Packet Pool Create</span></span> 

#### <a name="nx_packet_pool_create"></a><span data-ttu-id="37aae-1572">nx_packet_pool_create</span><span class="sxs-lookup"><span data-stu-id="37aae-1572">nx_packet_pool_create</span></span>

<span data-ttu-id="37aae-1573">**Simge** ![ Paket havuzu oluştur simgesi](./media/user-guide/netx-events/image114.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1573">**Icon** ![Packet pool create icon](./media/user-guide/netx-events/image114.png)</span></span>

<span data-ttu-id="37aae-1574">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1574">**Description**</span></span>

<span data-ttu-id="37aae-1575">Bu olay nx_packet_pool_create aracılığıyla bir paket havuzu oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1575">This event represents creating a packet pool via nx_packet_pool_create.</span></span>

<span data-ttu-id="37aae-1576">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1576">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1577">Bilgi alanı 1: paket havuzuna yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1577">Info Field 1: Pointer to the packet pool</span></span>
- <span data-ttu-id="37aae-1578">Bilgi alanı 2: Paket yükü boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-1578">Info Field 2: Packet payload size</span></span>
- <span data-ttu-id="37aae-1579">Bilgi alanı 3: havuz bellek alanı Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1579">Info Field 3: Pointer to pool memory area</span></span>
- <span data-ttu-id="37aae-1580">Bilgi alanı 4: havuz bellek alanının boyutu</span><span class="sxs-lookup"><span data-stu-id="37aae-1580">Info Field 4: Size of pool memory area</span></span>

### <a name="packet-pool-delete"></a><span data-ttu-id="37aae-1581">Paket havuzu silme</span><span class="sxs-lookup"><span data-stu-id="37aae-1581">Packet Pool Delete</span></span> 

#### <a name="nx_packet_pool_delete"></a><span data-ttu-id="37aae-1582">nx_packet_pool_delete</span><span class="sxs-lookup"><span data-stu-id="37aae-1582">nx_packet_pool_delete</span></span>

<span data-ttu-id="37aae-1583">**Simge** ![ Paket havuzu silme simgesi](./media/user-guide/netx-events/image115.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1583">**Icon** ![Packet pool delete icon](./media/user-guide/netx-events/image115.png)</span></span>

<span data-ttu-id="37aae-1584">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1584">**Description**</span></span>

<span data-ttu-id="37aae-1585">Bu olay nx_packet_pool_delete aracılığıyla bir paket havuzunu silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1585">This event represents deleting a packet pool via nx_packet_pool_delete.</span></span>

<span data-ttu-id="37aae-1586">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1586">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1587">Bilgi alanı 1: paket havuzuna yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1587">Info Field 1: Pointer to the packet pool</span></span>
- <span data-ttu-id="37aae-1588">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1588">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1589">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1589">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1590">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1590">Info Field 4: Not used</span></span>

#### <a name="packet-pool-information-get"></a><span data-ttu-id="37aae-1591">Paket havuzu bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="37aae-1591">Packet Pool Information Get</span></span> 

#### <a name="nx_packet_pool_info_get"></a><span data-ttu-id="37aae-1592">nx_packet_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1592">nx_packet_pool_info_get</span></span>

<span data-ttu-id="37aae-1593">**Simge** ![ Paket havuzu bilgileri al simgesi](./media/user-guide/netx-events/image116.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1593">**Icon** ![Packet pool information get icon](./media/user-guide/netx-events/image116.png)</span></span>

<span data-ttu-id="37aae-1594">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1594">**Description**</span></span>

<span data-ttu-id="37aae-1595">Bu olay, nx_packet_pool_info_get aracılığıyla paket havuzu bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1595">This event represents getting packet pool information via nx_packet_pool_info_get.</span></span>

<span data-ttu-id="37aae-1596">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1596">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1597">Bilgi alanı 1: paket havuzuna yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1597">Info Field 1: Pointer to packet pool</span></span>
- <span data-ttu-id="37aae-1598">Bilgi alanı 2: toplam paket sayısı</span><span class="sxs-lookup"><span data-stu-id="37aae-1598">Info Field 2: Total packets</span></span>
- <span data-ttu-id="37aae-1599">Bilgi alanı 3: kullanılabilir paketler</span><span class="sxs-lookup"><span data-stu-id="37aae-1599">Info Field 3: Available packets</span></span>
- <span data-ttu-id="37aae-1600">Bilgi alanı 4: boş istekler</span><span class="sxs-lookup"><span data-stu-id="37aae-1600">Info Field 4: Empty requests</span></span>

### <a name="packet-release"></a><span data-ttu-id="37aae-1601">Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="37aae-1601">Packet Release</span></span> 

#### <a name="nx_packet_data_release"></a><span data-ttu-id="37aae-1602">nx_packet_data_release</span><span class="sxs-lookup"><span data-stu-id="37aae-1602">nx_packet_data_release</span></span>

<span data-ttu-id="37aae-1603">**Simge** ![ Paket yayını simgesi](./media/user-guide/netx-events/image117.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1603">**Icon** ![Packet release icon](./media/user-guide/netx-events/image117.png)</span></span>

<span data-ttu-id="37aae-1604">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1604">**Description**</span></span>

<span data-ttu-id="37aae-1605">Bu olay nx_packet_release aracılığıyla bir paket serbest bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1605">This event represents releasing a packet via nx_packet_release.</span></span>

<span data-ttu-id="37aae-1606">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1606">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1607">Bilgi alanı 1: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1607">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="37aae-1608">Bilgi alanı 2: paket durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1608">Info Field 2: Packet status</span></span>
- <span data-ttu-id="37aae-1609">Bilgi alanı 3: kullanılabilir paketler</span><span class="sxs-lookup"><span data-stu-id="37aae-1609">Info Field 3: Available packets</span></span>
- <span data-ttu-id="37aae-1610">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1610">Info Field 4: Not used</span></span>

### <a name="packet-transmit-release"></a><span data-ttu-id="37aae-1611">Paket Iletme yayını</span><span class="sxs-lookup"><span data-stu-id="37aae-1611">Packet Transmit Release</span></span> 

#### <a name="nx_packet_transmit_release"></a><span data-ttu-id="37aae-1612">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="37aae-1612">nx_packet_transmit_release</span></span>

<span data-ttu-id="37aae-1613">**Simge** ![ Paket iletme yayını simgesi](./media/user-guide/netx-events/image118.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1613">**Icon** ![Packet transmit release icon](./media/user-guide/netx-events/image118.png)</span></span>

<span data-ttu-id="37aae-1614">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1614">**Description**</span></span>

<span data-ttu-id="37aae-1615">Bu olay nx_packet_transmit_release aracılığıyla bir iletme paketi serbest bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1615">This event represents releasing a transmit packet via nx_packet_transmit_release.</span></span>

<span data-ttu-id="37aae-1616">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1616">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1617">Bilgi alanı 1: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1617">Info Field 1: Pointer to the packet</span></span>
- <span data-ttu-id="37aae-1618">Bilgi alanı 2: paket durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1618">Info Field 2: Packet status</span></span>
- <span data-ttu-id="37aae-1619">Bilgi alanı 3: kullanılabilir paketler</span><span class="sxs-lookup"><span data-stu-id="37aae-1619">Info Field 3: Available packets</span></span>
- <span data-ttu-id="37aae-1620">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1620">Info Field 4: Not used</span></span>

### <a name="rarp-disable"></a><span data-ttu-id="37aae-1621">RARP devre dışı</span><span class="sxs-lookup"><span data-stu-id="37aae-1621">RARP Disable</span></span> 

#### <a name="nx_rarp_disable"></a><span data-ttu-id="37aae-1622">nx_rarp_disable</span><span class="sxs-lookup"><span data-stu-id="37aae-1622">nx_rarp_disable</span></span>

<span data-ttu-id="37aae-1623">**Simge** ![ R A R P devre dışı simgesi](./media/user-guide/netx-events/image119.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1623">**Icon** ![R A R P disable icon](./media/user-guide/netx-events/image119.png)</span></span>

<span data-ttu-id="37aae-1624">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1624">**Description**</span></span>

<span data-ttu-id="37aae-1625">Bu olay, nx_rarp_disable aracılığıyla RARP devre dışı bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1625">This event represents disabling RARP via nx_rarp_disable.</span></span>

<span data-ttu-id="37aae-1626">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1626">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1627">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1627">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1628">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1628">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1629">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1629">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1630">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1630">Info Field 4: Not used</span></span>

### <a name="rarp-enable"></a><span data-ttu-id="37aae-1631">RARP etkinleştir</span><span class="sxs-lookup"><span data-stu-id="37aae-1631">RARP Enable</span></span> 

#### <a name="nx_rarp_enable"></a><span data-ttu-id="37aae-1632">nx_rarp_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1632">nx_rarp_enable</span></span>

<span data-ttu-id="37aae-1633">**Simge** ![ R A R P etkinleştirme simgesi](./media/user-guide/netx-events/image120.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1633">**Icon** ![R A R P enable icon](./media/user-guide/netx-events/image120.png)</span></span>

<span data-ttu-id="37aae-1634">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1634">**Description**</span></span>

<span data-ttu-id="37aae-1635">Bu olay, nx_rarp_enable aracılığıyla RARP 'yi etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1635">This event represents enabling RARP via nx_rarp_enable.</span></span>

<span data-ttu-id="37aae-1636">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1636">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1637">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1637">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1638">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1638">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1639">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1639">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1640">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1640">Info Field 4: Not used</span></span>

### <a name="rarp-information-get"></a><span data-ttu-id="37aae-1641">RARP bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="37aae-1641">RARP Information Get</span></span> 

#### <a name="nx_rarp_info_get"></a><span data-ttu-id="37aae-1642">nx_rarp_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1642">nx_rarp_info_get</span></span>

<span data-ttu-id="37aae-1643">**Simge** ![ R A R P bilgi al simgesi](./media/user-guide/netx-events/image121.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1643">**Icon** ![R A R P information get icon](./media/user-guide/netx-events/image121.png)</span></span>

<span data-ttu-id="37aae-1644">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1644">**Description**</span></span>

<span data-ttu-id="37aae-1645">Bu olay nx_rarp_info_get aracılığıyla RARP bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1645">This event represents getting RARP information via nx_rarp_info_get.</span></span>

<span data-ttu-id="37aae-1646">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1646">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1647">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1647">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1648">Bilgi alanı 2: gönderilen Istekler</span><span class="sxs-lookup"><span data-stu-id="37aae-1648">Info Field 2: Requests sent</span></span>
- <span data-ttu-id="37aae-1649">Bilgi alanı 3: alınan yanıtlar</span><span class="sxs-lookup"><span data-stu-id="37aae-1649">Info Field 3: Responses received</span></span>
- <span data-ttu-id="37aae-1650">Bilgi alanı 4: geçersiz yanıtlar</span><span class="sxs-lookup"><span data-stu-id="37aae-1650">Info Field 4: Invalid responses</span></span>

### <a name="system-initialize"></a><span data-ttu-id="37aae-1651">Sistem başlatma</span><span class="sxs-lookup"><span data-stu-id="37aae-1651">System Initialize</span></span> 

#### <a name="nx_system_initialize"></a><span data-ttu-id="37aae-1652">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="37aae-1652">nx_system_initialize</span></span>

<span data-ttu-id="37aae-1653">**Simge** ![ Sistem başlatma simgesi](./media/user-guide/netx-events/image122.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1653">**Icon** ![System initialize icon](./media/user-guide/netx-events/image122.png)</span></span>

<span data-ttu-id="37aae-1654">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1654">**Description**</span></span>

<span data-ttu-id="37aae-1655">Bu olay, nx_system_initialize aracılığıyla NetX başlatmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1655">This event represents initializing NetX via nx_system_initialize.</span></span>

<span data-ttu-id="37aae-1656">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1656">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1657">Bilgi alanı 1: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1657">Info Field 1: Not used</span></span>
- <span data-ttu-id="37aae-1658">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1658">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1659">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1659">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1660">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1660">Info Field 4: Not used</span></span>

### <a name="tcp-client-socket-bind"></a><span data-ttu-id="37aae-1661">TCP Istemci yuvası bağlama</span><span class="sxs-lookup"><span data-stu-id="37aae-1661">TCP Client Socket Bind</span></span> 

#### <a name="nx_tcp_client_socket_bind"></a><span data-ttu-id="37aae-1662">nx_tcp_client_socket_bind</span><span class="sxs-lookup"><span data-stu-id="37aae-1662">nx_tcp_client_socket_bind</span></span>

<span data-ttu-id="37aae-1663">**Simge** ![ T P istemci yuvası bağlama simgesi](./media/user-guide/netx-events/image123.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1663">**Icon** ![T  P client socket bind icon](./media/user-guide/netx-events/image123.png)</span></span>

<span data-ttu-id="37aae-1664">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1664">**Description**</span></span>

<span data-ttu-id="37aae-1665">Bu olay, nx_tcp_client_socket_bind aracılığıyla bir istemci yuvasını bağlantı noktasına bağlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1665">This event represents binding a client socket to a port via nx_tcp_client_socket_bind.</span></span>

<span data-ttu-id="37aae-1666">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1666">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1667">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1667">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1668">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1668">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1669">Bilgi alanı 3: bağlantı noktası istendi</span><span class="sxs-lookup"><span data-stu-id="37aae-1669">Info Field 3: Port requested</span></span>
- <span data-ttu-id="37aae-1670">Bilgi alanı 4: bekleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="37aae-1670">Info Field 4: Wait option</span></span>

### <a name="tcp-client-socket-connect"></a><span data-ttu-id="37aae-1671">TCP Istemci yuvası bağlantısı</span><span class="sxs-lookup"><span data-stu-id="37aae-1671">TCP Client Socket Connect</span></span> 

#### <a name="nx_tcp_client_socket_connect"></a><span data-ttu-id="37aae-1672">nx_tcp_client_socket_connect</span><span class="sxs-lookup"><span data-stu-id="37aae-1672">nx_tcp_client_socket_connect</span></span>

<span data-ttu-id="37aae-1673">**Simge** ![ T C P istemci yuvası bağlantı simgesi](./media/user-guide/netx-events/image124.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1673">**Icon** ![T C P client socket connect icon](./media/user-guide/netx-events/image124.png)</span></span>

<span data-ttu-id="37aae-1674">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1674">**Description**</span></span>

<span data-ttu-id="37aae-1675">Bu olay, nx_tcp_client_socket_connect aracılığıyla bir istemci yuva bağlantısı yapmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1675">This event represents making a client socket connection via nx_tcp_client_socket_connect.</span></span>

<span data-ttu-id="37aae-1676">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1676">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1677">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1677">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1678">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1678">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1679">Bilgi alanı 3: sunucu IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1679">Info Field 3: Server IP address</span></span>
- <span data-ttu-id="37aae-1680">Bilgi alanı 4: sunucu bağlantı noktası istendi</span><span class="sxs-lookup"><span data-stu-id="37aae-1680">Info Field 4: Server port requested</span></span>

### <a name="tcp-client-socket-port-get"></a><span data-ttu-id="37aae-1681">TCP Istemci yuva bağlantı noktası al</span><span class="sxs-lookup"><span data-stu-id="37aae-1681">TCP Client Socket Port Get</span></span> 

#### <a name="nx_tcp_client_socket_port_get"></a><span data-ttu-id="37aae-1682">nx_tcp_client_socket_port_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1682">nx_tcp_client_socket_port_get</span></span>

<span data-ttu-id="37aae-1683">**Simge** ![ T C P istemci yuva bağlantı noktası al simgesi](./media/user-guide/netx-events/image125.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1683">**Icon** ![T C P client socket port get icon](./media/user-guide/netx-events/image125.png)</span></span>

<span data-ttu-id="37aae-1684">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1684">**Description**</span></span>

<span data-ttu-id="37aae-1685">Bu olay, istemci yuva bağlantı noktası numarasının nx_tcp_client_socket_port_get aracılığıyla alınmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1685">This event represents getting the client socket port number via nx_tcp_client_socket_port_get.</span></span>

<span data-ttu-id="37aae-1686">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1686">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1687">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1687">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1688">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1688">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1689">Bilgi alanı 3: bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-1689">Info Field 3: Port number</span></span>
- <span data-ttu-id="37aae-1690">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1690">Info Field 4: Not used</span></span>

### <a name="tcp-client-socket-unbind"></a><span data-ttu-id="37aae-1691">TCP Istemci yuvası bağlantısı kesme</span><span class="sxs-lookup"><span data-stu-id="37aae-1691">TCP Client Socket Unbind</span></span> 

#### <a name="nx_tcp_client_socket_unbind"></a><span data-ttu-id="37aae-1692">nx_tcp_client_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="37aae-1692">nx_tcp_client_socket_unbind</span></span>

<span data-ttu-id="37aae-1693">**Simge** ![ T C P istemci yuvası bağlantı çözme simgesi](./media/user-guide/netx-events/image126.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1693">**Icon** ![T C P client socket unbind icon](./media/user-guide/netx-events/image126.png)</span></span>

<span data-ttu-id="37aae-1694">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1694">**Description**</span></span>

<span data-ttu-id="37aae-1695">Bu olay, nx_tcp_client_socket_unbind aracılığıyla yuva ile ilişkili bağlantı noktasının bağlamasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1695">This event represents unbinding the port associated with the socket via nx_tcp_client_socket_unbind.</span></span>

<span data-ttu-id="37aae-1696">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1696">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1697">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1697">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1698">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1698">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1699">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1699">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1700">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1700">Info Field 4: Not used</span></span>

### <a name="tcp-enable"></a><span data-ttu-id="37aae-1701">TCP etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="37aae-1701">TCP Enable</span></span> 

#### <a name="nx_tcp_enable"></a><span data-ttu-id="37aae-1702">nx_tcp_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1702">nx_tcp_enable</span></span>

<span data-ttu-id="37aae-1703">**Simge** ![ T C P etkinleştirme simgesi](./media/user-guide/netx-events/image127.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1703">**Icon** ![T C P enable icon](./media/user-guide/netx-events/image127.png)</span></span>

<span data-ttu-id="37aae-1704">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1704">**Description**</span></span>

<span data-ttu-id="37aae-1705">Bu olay nx_tcp_enable aracılığıyla TCP etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1705">This event represents enabling TCP via nx_tcp_enable.</span></span>

<span data-ttu-id="37aae-1706">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1706">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1707">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1707">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1708">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1708">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1709">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1709">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1710">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1710">Info Field 4: Not used</span></span>

###  <a name="tcp-free-port-find-tcp-free-port-find"></a><span data-ttu-id="37aae-1711">TCP boş bağlantı noktası bulma TCP boş bağlantı noktası bulma</span><span class="sxs-lookup"><span data-stu-id="37aae-1711">TCP Free Port Find TCP Free Port Find</span></span> 

#### <a name="nx_tcp_free_port_find"></a><span data-ttu-id="37aae-1712">nx_tcp_free_port_find</span><span class="sxs-lookup"><span data-stu-id="37aae-1712">nx_tcp_free_port_find</span></span>

<span data-ttu-id="37aae-1713">**Simge** ![ T CP boş bağlantı noktası bul simgesi](./media/user-guide/netx-events/image128.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1713">**Icon** ![T  CP free port find icon](./media/user-guide/netx-events/image128.png)</span></span>

<span data-ttu-id="37aae-1714">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1714">**Description**</span></span>

<span data-ttu-id="37aae-1715">Bu olay nx_tcp_free_port_find aracılığıyla boş bir TCP bağlantı noktası bulmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1715">This event represents finding a free TCP port via nx_tcp_free_port_find.</span></span>

<span data-ttu-id="37aae-1716">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1716">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1717">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1717">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1718">Bilgi alanı 2: arama bağlantı noktası numarası başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1718">Info Field 2: Starting search port number</span></span>
- <span data-ttu-id="37aae-1719">Bilgi alanı 3: ücretsiz bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-1719">Info Field 3: Free port number</span></span>
- <span data-ttu-id="37aae-1720">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1720">Info Field 4: Not used</span></span>

###  <a name="tcp-infomation-get"></a><span data-ttu-id="37aae-1721">TCP bilgisi al</span><span class="sxs-lookup"><span data-stu-id="37aae-1721">TCP Infomation Get</span></span> 

#### <a name="nx_tcp_info_get"></a><span data-ttu-id="37aae-1722">nx_tcp_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1722">nx_tcp_info_get</span></span>

<span data-ttu-id="37aae-1723">**Simge** ![ T C P bilgi al simgesi](./media/user-guide/netx-events/image129.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1723">**Icon** ![T C P infomation get icon](./media/user-guide/netx-events/image129.png)</span></span>

<span data-ttu-id="37aae-1724">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1724">**Description**</span></span>

<span data-ttu-id="37aae-1725">Bu olay, nx_tcp_info_get aracılığıyla belirtilen IP örneği için TCP bilgilerini almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1725">This event represents retrieving TCP information for the specified IP instance via nx_tcp_info_get.</span></span>

<span data-ttu-id="37aae-1726">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1726">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1727">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1727">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1728">Bilgi alanı 2: gönderilen bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="37aae-1728">Info Field 2: Number of bytes sent</span></span>
- <span data-ttu-id="37aae-1729">Bilgi alanı 3: alınan bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="37aae-1729">Info Field 3: Number of bytes received</span></span>
- <span data-ttu-id="37aae-1730">Bilgi alanı 4: Geçersiz paketlerin sayısı</span><span class="sxs-lookup"><span data-stu-id="37aae-1730">Info Field 4: Number of invalid packets</span></span>

###  <a name="tcp-server-socket-accept"></a><span data-ttu-id="37aae-1731">TCP sunucusu yuvasını kabul etme</span><span class="sxs-lookup"><span data-stu-id="37aae-1731">TCP Server Socket Accept</span></span> 

#### <a name="nx_tcp_server_socket_accept"></a><span data-ttu-id="37aae-1732">nx_tcp_server_socket_accept</span><span class="sxs-lookup"><span data-stu-id="37aae-1732">nx_tcp_server_socket_accept</span></span>

<span data-ttu-id="37aae-1733">**Simge** ![ T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image130.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1733">**Icon** ![T C P server socket accept icon](./media/user-guide/netx-events/image130.png)</span></span>

<span data-ttu-id="37aae-1734">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1734">**Description**</span></span>

<span data-ttu-id="37aae-1735">Bu olay, nx_tcp_server_socket_accept aracılığıyla bir etkin bağlantı isteği alındıktan sonra sunucu yuvasını ayarlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1735">This event represents setting up the server socket after an active connection request was received via nx_tcp_server_socket_accept.</span></span>

<span data-ttu-id="37aae-1736">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1736">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1737">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1737">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1738">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1738">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1739">Bilgi alanı 3: bekleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="37aae-1739">Info Field 3: Wait option</span></span>
- <span data-ttu-id="37aae-1740">Bilgi alanı 4: yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1740">Info Field 4: Socket state</span></span>

###  <a name="tcp-server-socket-listen"></a><span data-ttu-id="37aae-1741">TCP sunucusu yuva dinleme</span><span class="sxs-lookup"><span data-stu-id="37aae-1741">TCP Server Socket Listen</span></span> 

#### <a name="nx_tcp_server_socket_listen"></a><span data-ttu-id="37aae-1742">nx_tcp_server_socket_listen</span><span class="sxs-lookup"><span data-stu-id="37aae-1742">nx_tcp_server_socket_listen</span></span>

<span data-ttu-id="37aae-1743">**Simge** ![ T C P sunucu yuvası lsten simgesi](./media/user-guide/netx-events/image131.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1743">**Icon** ![T C P server socket lsten icon](./media/user-guide/netx-events/image131.png)</span></span>

<span data-ttu-id="37aae-1744">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1744">**Description**</span></span>

<span data-ttu-id="37aae-1745">Bu olay, nx_tcp_server_socket_listen aracılığıyla belirtilen TCP bağlantı noktası için bir dinleme isteğini ve sunucu yuvasını kaydetmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1745">This event represents register a listen request and a server socket for the specified TCP port via nx_tcp_server_socket_listen.</span></span>

<span data-ttu-id="37aae-1746">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1746">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1747">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1747">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1748">Bilgi alanı 2: TCP bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-1748">Info Field 2: TCP port number</span></span>
- <span data-ttu-id="37aae-1749">Bilgi alanı 3: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1749">Info Field 3: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1750">Bilgi alanı 4: sıraya alınabilen en fazla bağlantı sayısı</span><span class="sxs-lookup"><span data-stu-id="37aae-1750">Info Field 4: Maximum number of connections that can be queued</span></span>

###  <a name="tcp-server-socket-relisten"></a><span data-ttu-id="37aae-1751">TCP sunucu yuvası yeniden dinleme</span><span class="sxs-lookup"><span data-stu-id="37aae-1751">TCP Server Socket Relisten</span></span> 

#### <a name="nx_tcp_server_socket_relisten"></a><span data-ttu-id="37aae-1752">nx_tcp_server_socket_relisten</span><span class="sxs-lookup"><span data-stu-id="37aae-1752">nx_tcp_server_socket_relisten</span></span>

<span data-ttu-id="37aae-1753">**Simge** ![ T C P sunucu yuvası yeniden dinleme simgesi](./media/user-guide/netx-events/image132.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1753">**Icon** ![T C P server socket relisten icon](./media/user-guide/netx-events/image132.png)</span></span>

<span data-ttu-id="37aae-1754">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1754">**Description**</span></span>

<span data-ttu-id="37aae-1755">Bu olay, nx_tcp_server_socket_relisten aracılığıyla belirtilen TCP bağlantı noktasında var olan bir dinleme isteği için başka bir sunucu yuvasını kaydetmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1755">This event represents register another server socket for an existing listen request on the specified TCP port via nx_tcp_server_socket_relisten.</span></span>

<span data-ttu-id="37aae-1756">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1756">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1757">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1757">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1758">Bilgi alanı 2: TCP bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-1758">Info Field 2: TCP port number</span></span>
- <span data-ttu-id="37aae-1759">Bilgi alanı 3: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1759">Info Field 3: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1760">Bilgi alanı 4: yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1760">Info Field 4: Socket state</span></span>

###  <a name="tcp-server-socket-unaccept"></a><span data-ttu-id="37aae-1761">TCP sunucusu yuvası kabul etme</span><span class="sxs-lookup"><span data-stu-id="37aae-1761">TCP Server Socket Unaccept</span></span> 

#### <a name="nx_tcp_server_socket_unaccept"></a><span data-ttu-id="37aae-1762">nx_tcp_server_socket_unaccept</span><span class="sxs-lookup"><span data-stu-id="37aae-1762">nx_tcp_server_socket_unaccept</span></span>

<span data-ttu-id="37aae-1763">**Simge** ![ T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image133.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1763">**Icon** ![T C P server socket unaccept icon](./media/user-guide/netx-events/image133.png)</span></span>

<span data-ttu-id="37aae-1764">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1764">**Description**</span></span>

<span data-ttu-id="37aae-1765">Bu olay, nx_tcp_server_socket_unaccept aracılığıyla önceki bir pasif bağlantıyı alan bağlantı noktasıyla ilişkilendirmeden sunucu yuvasını kaldırmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1765">This event represents removing the server socket from association with the port receiving an earlier passive connection via nx_tcp_server_socket_unaccept.</span></span>

<span data-ttu-id="37aae-1766">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1766">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1767">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1767">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1768">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1768">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1769">Bilgi alanı 3: yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1769">Info Field 3: Socket state</span></span>
- <span data-ttu-id="37aae-1770">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1770">Info Field 4: Not used</span></span>

###  <a name="tcp-server-socket-unlisten-tcp-server-socket-unlisten"></a><span data-ttu-id="37aae-1771">TCP sunucu yuvası dinleme TCP sunucusu yuva geri dinleme</span><span class="sxs-lookup"><span data-stu-id="37aae-1771">TCP Server Socket Unlisten TCP Server Socket Unlisten</span></span> 

#### <a name="nx_tcp_server_socket_unlisten"></a><span data-ttu-id="37aae-1772">nx_tcp_server_socket_unlisten</span><span class="sxs-lookup"><span data-stu-id="37aae-1772">nx_tcp_server_socket_unlisten</span></span>

<span data-ttu-id="37aae-1773">**Simge** ![ T C P Server yuva geri dinleme simgesi](./media/user-guide/netx-events/image134.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1773">**Icon** ![T C P server socket unlisten icon](./media/user-guide/netx-events/image134.png)</span></span>

<span data-ttu-id="37aae-1774">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1774">**Description**</span></span>

<span data-ttu-id="37aae-1775">Bu olay, belirtilen TCP bağlantı noktası için önceki bir dinleme isteğinin nx_tcp_server_socket_unlisten aracılığıyla kaldırılmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1775">This event represents removing a previous listen request for the specified TCP port via nx_tcp_server_socket_unlisten.</span></span>

<span data-ttu-id="37aae-1776">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1776">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1777">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1777">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1778">Bilgi alanı 2: TCP bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-1778">Info Field 2: TCP port number</span></span>
- <span data-ttu-id="37aae-1779">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1779">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1780">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1780">Info Field 4: Not used</span></span>

### <a name="tcp-socket-bytes-available"></a><span data-ttu-id="37aae-1781">Kullanılabilir TCP yuvası baytları</span><span class="sxs-lookup"><span data-stu-id="37aae-1781">TCP Socket Bytes Available</span></span> 

#### <a name="nx_tcp_socket_bytes_available"></a><span data-ttu-id="37aae-1782">nx_tcp_socket_bytes_available</span><span class="sxs-lookup"><span data-stu-id="37aae-1782">nx_tcp_socket_bytes_available</span></span>

<span data-ttu-id="37aae-1783">**Simge** ![ T C P yuva baytları kullanılabilir simgesi](./media/user-guide/netx-events/image135.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1783">**Icon** ![T C P socket bytes available icon](./media/user-guide/netx-events/image135.png)</span></span>

<span data-ttu-id="37aae-1784">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1784">**Description**</span></span>

<span data-ttu-id="37aae-1785">Bu olay, nx_tcp_socket_bytes_available aracılığıyla belirtilen TCP alma yuvasında mevcut olan bayt sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1785">This event represents the number of bytes currently available on the specified TCP receiving socket via nx_tcp_socket_bytes_available.</span></span>

<span data-ttu-id="37aae-1786">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1786">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1787">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1787">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1788">Bilgi alanı 2: TCP yuvası Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1788">Info Field 2: Pointer to TCP socket</span></span>
- <span data-ttu-id="37aae-1789">Bilgi alanı 3: yuvada alınan baytlar</span><span class="sxs-lookup"><span data-stu-id="37aae-1789">Info Field 3: Bytes received on the socket</span></span>
- <span data-ttu-id="37aae-1790">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1790">Info Field 4: Not used</span></span>

### <a name="tcp-socket-create"></a><span data-ttu-id="37aae-1791">TCP yuvası oluşturma</span><span class="sxs-lookup"><span data-stu-id="37aae-1791">TCP Socket Create</span></span> 

#### <a name="nx_tcp_socket_create"></a><span data-ttu-id="37aae-1792">nx_tcp_socket_create</span><span class="sxs-lookup"><span data-stu-id="37aae-1792">nx_tcp_socket_create</span></span>

<span data-ttu-id="37aae-1793">**Simge** ![ T C P yuvası oluşturma simgesi](./media/user-guide/netx-events/image136.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1793">**Icon** ![T C P socket create icon](./media/user-guide/netx-events/image136.png)</span></span>

<span data-ttu-id="37aae-1794">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1794">**Description**</span></span>

<span data-ttu-id="37aae-1795">Bu olay nx_tcp_socket_create aracılığıyla bir TCP yuvası oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1795">This event represents creating a TCP socket via nx_tcp_socket_create.</span></span>

<span data-ttu-id="37aae-1796">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1796">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1797">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1797">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1798">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1798">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1799">Bilgi alanı 3: hizmet türü</span><span class="sxs-lookup"><span data-stu-id="37aae-1799">Info Field 3: Type of service</span></span>
- <span data-ttu-id="37aae-1800">Bilgi alanı 4: pencere boyutunu al</span><span class="sxs-lookup"><span data-stu-id="37aae-1800">Info Field 4: Receive window size</span></span>

### <a name="tcp-socket-delete"></a><span data-ttu-id="37aae-1801">TCP yuvası silme</span><span class="sxs-lookup"><span data-stu-id="37aae-1801">TCP Socket Delete</span></span> 

#### <a name="nx_tcp_socket_delete"></a><span data-ttu-id="37aae-1802">nx_tcp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="37aae-1802">nx_tcp_socket_delete</span></span>

<span data-ttu-id="37aae-1803">**Simge** ![ T C P yuvası silme simgesi](./media/user-guide/netx-events/image137.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1803">**Icon** ![T C P socket delete icon](./media/user-guide/netx-events/image137.png)</span></span>

<span data-ttu-id="37aae-1804">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1804">**Description**</span></span>

<span data-ttu-id="37aae-1805">Bu olay nx_tcp_socket_delete aracılığıyla bir yuvayı silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1805">This event represents deleting a socket via nx_tcp_socket_delete.</span></span>

<span data-ttu-id="37aae-1806">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1806">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1807">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1807">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1808">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1808">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1809">Bilgi alanı 3: yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1809">Info Field 3: Socket state</span></span>
- <span data-ttu-id="37aae-1810">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1810">Info Field 4: Not used</span></span>

### <a name="tcp-socket-disconnect"></a><span data-ttu-id="37aae-1811">TCP yuvası bağlantısı kesme</span><span class="sxs-lookup"><span data-stu-id="37aae-1811">TCP Socket Disconnect</span></span> 

#### <a name="nx_tcp_socket_disconnect"></a><span data-ttu-id="37aae-1812">nx_tcp_socket_disconnect</span><span class="sxs-lookup"><span data-stu-id="37aae-1812">nx_tcp_socket_disconnect</span></span>

<span data-ttu-id="37aae-1813">**Simge** ![ T C P yuvası bağlantı kesme simgesi](./media/user-guide/netx-events/image138.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1813">**Icon** ![T C P socket disconnect icon](./media/user-guide/netx-events/image138.png)</span></span>

<span data-ttu-id="37aae-1814">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1814">**Description**</span></span>

<span data-ttu-id="37aae-1815">Bu olay nx_tcp_socket_disconnect aracılığıyla bir yuvanın bağlantısını kesmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1815">This event represents disconnecting a socket via nx_tcp_socket_disconnect.</span></span>

<span data-ttu-id="37aae-1816">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1816">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1817">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1817">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1818">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1818">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1819">Bilgi alanı 3: bekleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="37aae-1819">Info Field 3: Wait option</span></span>
- <span data-ttu-id="37aae-1820">Bilgi alanı 4: yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1820">Info Field 4: Socket state</span></span>

### <a name="tcp-socket-information-get"></a><span data-ttu-id="37aae-1821">TCP yuva bilgileri Get</span><span class="sxs-lookup"><span data-stu-id="37aae-1821">TCP Socket Information Get</span></span> 

#### <a name="nx_tcp_socket_info_get"></a><span data-ttu-id="37aae-1822">nx_tcp_socket_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1822">nx_tcp_socket_info_get</span></span>

<span data-ttu-id="37aae-1823">**Simge** ![ T C P yuva bilgileri al simgesi](./media/user-guide/netx-events/image139.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1823">**Icon** ![T C P socket information get icon](./media/user-guide/netx-events/image139.png)</span></span>

<span data-ttu-id="37aae-1824">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1824">**Description**</span></span>

<span data-ttu-id="37aae-1825">Bu olay nx_tcp_socket_info_get aracılığıyla bir yuva hakkında bilgi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1825">This event represents getting information about a socket via nx_tcp_socket_info_get.</span></span>

<span data-ttu-id="37aae-1826">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1826">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1827">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1827">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1828">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1828">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1829">Bilgi alanı 3: Bu yuva aracılığıyla gönderilen baytlar</span><span class="sxs-lookup"><span data-stu-id="37aae-1829">Info Field 3: Bytes sent through this socket</span></span>
- <span data-ttu-id="37aae-1830">Bilgi alanı 4: Bu yuva aracılığıyla alınan baytlar</span><span class="sxs-lookup"><span data-stu-id="37aae-1830">Info Field 4: Bytes received through this socket</span></span>

### <a name="tcp-socket-mss-get"></a><span data-ttu-id="37aae-1831">TCP yuvası ve Get</span><span class="sxs-lookup"><span data-stu-id="37aae-1831">TCP Socket MSS Get</span></span> 

#### <a name="nx_tcp_socket_mss_get"></a><span data-ttu-id="37aae-1832">nx_tcp_socket_mss_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1832">nx_tcp_socket_mss_get</span></span>

<span data-ttu-id="37aae-1833">**Simge** ![ T C P yuvası M S S al simgesi](./media/user-guide/netx-events/image140.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1833">**Icon** ![T C P socket M S S get icon](./media/user-guide/netx-events/image140.png)</span></span>

<span data-ttu-id="37aae-1834">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1834">**Description**</span></span>

<span data-ttu-id="37aae-1835">Bu olay, nx_tcp_socket_mss_get aracılığıyla yuvanın bir hakete alınmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1835">This event represents getting the socket's MSS via nx_tcp_socket_mss_get.</span></span>

<span data-ttu-id="37aae-1836">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1836">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1837">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1837">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1838">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1838">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1839">Bilgi alanı 3: en fazla segment boyutu (</span><span class="sxs-lookup"><span data-stu-id="37aae-1839">Info Field 3: Maximum Segment Size (MSS)</span></span>
- <span data-ttu-id="37aae-1840">Bilgi alanı 4: yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1840">Info Field 4: Socket state</span></span>

### <a name="tcp-socket-mss-peer-get"></a><span data-ttu-id="37aae-1841">TCP soketi eşi al</span><span class="sxs-lookup"><span data-stu-id="37aae-1841">TCP Socket MSS Peer Get</span></span> 

#### <a name="nx_tcp_socket_mss_peer_get"></a><span data-ttu-id="37aae-1842">nx_tcp_socket_mss_peer_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1842">nx_tcp_socket_mss_peer_get</span></span>

<span data-ttu-id="37aae-1843">**Simge** ![ T C P yuvası M S S eşi al simgesi](./media/user-guide/netx-events/image141.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1843">**Icon** ![T C P socket M S S peer get icon](./media/user-guide/netx-events/image141.png)</span></span>

<span data-ttu-id="37aae-1844">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1844">**Description**</span></span>

<span data-ttu-id="37aae-1845">Bu olay, yuvanın eşinin nx_tcp_socket_mss_peer_get aracılığıyla sahip olduğu değeri almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1845">This event represents getting the MSS value of the socket's peer via nx_tcp_socket_mss_peer_get.</span></span>

<span data-ttu-id="37aae-1846">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1846">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1847">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1847">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1848">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1848">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1849">Bilgi alanı 3: eşler arası</span><span class="sxs-lookup"><span data-stu-id="37aae-1849">Info Field 3: Peer's MSS</span></span>
- <span data-ttu-id="37aae-1850">Bilgi alanı 4: yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1850">Info Field 4: Socket state</span></span>

### <a name="tcp-socket-mss-set"></a><span data-ttu-id="37aae-1851">TCP yuvası, küme</span><span class="sxs-lookup"><span data-stu-id="37aae-1851">TCP Socket MSS Set</span></span> 

#### <a name="nx_tcp_socket_mss_set"></a><span data-ttu-id="37aae-1852">nx_tcp_socket_mss_set</span><span class="sxs-lookup"><span data-stu-id="37aae-1852">nx_tcp_socket_mss_set</span></span>

<span data-ttu-id="37aae-1853">**Simge** ![ T C P yuvası M S S set simgesi](./media/user-guide/netx-events/image142.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1853">**Icon** ![T C P socket M S S set icon](./media/user-guide/netx-events/image142.png)</span></span>

<span data-ttu-id="37aae-1854">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1854">**Description**</span></span>

<span data-ttu-id="37aae-1855">Bu olay, bir yuvanın nx_tcp_socket_mss_set aracılığıyla ayarlanmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1855">This event represents setting a socket's MSS via nx_tcp_socket_mss_set.</span></span>

<span data-ttu-id="37aae-1856">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1856">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1857">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1857">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1858">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1858">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1859">Bilgi alanı 3: Bu</span><span class="sxs-lookup"><span data-stu-id="37aae-1859">Info Field 3: MSS</span></span>
- <span data-ttu-id="37aae-1860">Bilgi alanı 4: yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1860">Info Field 4: Socket state</span></span>

### <a name="tcp-socket-peer-info-get"></a><span data-ttu-id="37aae-1861">TCP yuvası eş bilgi al</span><span class="sxs-lookup"><span data-stu-id="37aae-1861">TCP Socket Peer Info Get</span></span> 

#### <a name="nx_tcp_socket_peer_info_get"></a><span data-ttu-id="37aae-1862">nx_tcp_socket_peer_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1862">nx_tcp_socket_peer_info_get</span></span>

<span data-ttu-id="37aae-1863">**Simge** ![ T C P soket eş bilgi al simgesi](./media/user-guide/netx-events/image143.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1863">**Icon** ![T C P socket peer info get icon](./media/user-guide/netx-events/image143.png)</span></span>

<span data-ttu-id="37aae-1864">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1864">**Description**</span></span>

<span data-ttu-id="37aae-1865">Bu olay, eş (örneğin, ana bilgisayar >bağlanması) IP adresi ve bağlantı noktası ile ilgili TCP yuvasından alınan bilgileri nx_tcp_socket_peer_info_get aracılığıyla temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1865">This event represents information retrieved from the TCP socket regarding the peer (e.g. >connecting host) IP address and port via nx_tcp_socket_peer_info_get.</span></span>

<span data-ttu-id="37aae-1866">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1866">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1867">Bilgi alanı 1: TCP yuvası Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1867">Info Field 1: Pointer to TCP socket</span></span>
- <span data-ttu-id="37aae-1868">Bilgi alanı 2: eş IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-1868">Info Field 2: Peer IP address</span></span>
- <span data-ttu-id="37aae-1869">Bilgi alanı 3: eş bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-1869">Info Field 3: Peer port number</span></span>
- <span data-ttu-id="37aae-1870">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1870">Info Field 4: Not used</span></span>

### <a name="tcp-socket-receive"></a><span data-ttu-id="37aae-1871">TCP yuvası alma</span><span class="sxs-lookup"><span data-stu-id="37aae-1871">TCP Socket Receive</span></span> 

#### <a name="nx_tcp_socket_receive"></a><span data-ttu-id="37aae-1872">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="37aae-1872">nx_tcp_socket_receive</span></span>

<span data-ttu-id="37aae-1873">**Simge** ![ T C P yuvası alma simgesi](./media/user-guide/netx-events/image144.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1873">**Icon** ![T C P socket receive icon](./media/user-guide/netx-events/image144.png)</span></span>

<span data-ttu-id="37aae-1874">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1874">**Description**</span></span>

<span data-ttu-id="37aae-1875">Bu olay, nx_tcp_socket_receive aracılığıyla bir yuvadan veri almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1875">This event represents receiving data from a socket via nx_tcp_socket_receive.</span></span>

<span data-ttu-id="37aae-1876">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1876">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1877">Bilgi alanı 1: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1877">Info Field 1: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1878">Bilgi alanı 2: alınan paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1878">Info Field 2: Pointer to received packet</span></span>
- <span data-ttu-id="37aae-1879">Bilgi alanı 3: paket uzunluğu alındı</span><span class="sxs-lookup"><span data-stu-id="37aae-1879">Info Field 3: Received packet length</span></span>
- <span data-ttu-id="37aae-1880">Bilgi alanı 4: alma sıra numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-1880">Info Field 4: Receive sequence number</span></span>

### <a name="tcp-socket-receive-notify"></a><span data-ttu-id="37aae-1881">TCP yuvası alma bildirimi</span><span class="sxs-lookup"><span data-stu-id="37aae-1881">TCP Socket Receive Notify</span></span> 

#### <a name="nx_tcp_socket_receive_notify"></a><span data-ttu-id="37aae-1882">nx_tcp_socket_receive_notify</span><span class="sxs-lookup"><span data-stu-id="37aae-1882">nx_tcp_socket_receive_notify</span></span>

<span data-ttu-id="37aae-1883">**Simge** ![ T C P yuvası alma bildirim simgesi](./media/user-guide/netx-events/image145.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1883">**Icon** ![T C P socket receive notify icon](./media/user-guide/netx-events/image145.png)</span></span>

<span data-ttu-id="37aae-1884">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1884">**Description**</span></span>

<span data-ttu-id="37aae-1885">Bu olay, bir yuva için nx_tcp_socket_receive_notify aracılığıyla bir alma bildirimi geri araması kaydetmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1885">This event represents registering a receive notify callback for a socket via nx_tcp_socket_receive_notify.</span></span>

<span data-ttu-id="37aae-1886">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1886">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1887">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1887">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1888">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1888">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1889">Bilgi alanı 3: alma için geri arama bilgi alan 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1889">Info Field 3: Pointer to receive notify callback Info Field 4: Not used</span></span>

### <a name="tcp-socket-send"></a><span data-ttu-id="37aae-1890">TCP yuvası gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-1890">TCP Socket Send</span></span> 

#### <a name="nx_tcp_socket_send"></a><span data-ttu-id="37aae-1891">nx_tcp_socket_send</span><span class="sxs-lookup"><span data-stu-id="37aae-1891">nx_tcp_socket_send</span></span>

<span data-ttu-id="37aae-1892">**Simge** ![ T C P yuvası gönderme simgesi](./media/user-guide/netx-events/image146.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1892">**Icon** ![T C P socket send icon](./media/user-guide/netx-events/image146.png)</span></span>

<span data-ttu-id="37aae-1893">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1893">**Description**</span></span>

<span data-ttu-id="37aae-1894">Bu olay nx_tcp_socket_send aracılığıyla bir yuvada veri göndermeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1894">This event represents sending data on a socket via nx_tcp_socket_send.</span></span>

<span data-ttu-id="37aae-1895">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1895">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1896">Bilgi alanı 1: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1896">Info Field 1: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1897">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1897">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-1898">Bilgi alanı 3: paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="37aae-1898">Info Field 3: Length of packet</span></span>
- <span data-ttu-id="37aae-1899">Bilgi alanı 4: aktarım sıra numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-1899">Info Field 4: Transmit sequence number</span></span>

### <a name="tcp-socket-state-wait"></a><span data-ttu-id="37aae-1900">TCP yuva durumu bekleme</span><span class="sxs-lookup"><span data-stu-id="37aae-1900">TCP Socket State Wait</span></span> 

#### <a name="nx_tcp_socket_state_wait"></a><span data-ttu-id="37aae-1901">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="37aae-1901">nx_tcp_socket_state_wait</span></span>

<span data-ttu-id="37aae-1902">**Simge** ![ T C P yuva durumu bekleme simgesi](./media/user-guide/netx-events/image147.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1902">**Icon** ![T C P socket state wait icon](./media/user-guide/netx-events/image147.png)</span></span>

<span data-ttu-id="37aae-1903">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1903">**Description**</span></span>

<span data-ttu-id="37aae-1904">Bu olay, bir yuvanın nx_tcp_socket_state_wait aracılığıyla belirli bir durumu girmesini beklemeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1904">This event represents waiting for a socket to enter a particular state via nx_tcp_socket_state_wait.</span></span>

<span data-ttu-id="37aae-1905">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1905">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1906">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1906">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1907">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1907">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1908">Bilgi alanı 3: Istenen yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1908">Info Field 3: Desired socket state</span></span>
- <span data-ttu-id="37aae-1909">Bilgi alanı 4: önceki yuva durumu</span><span class="sxs-lookup"><span data-stu-id="37aae-1909">Info Field 4: Previous socket state</span></span>

### <a name="tcp-socket-transmit-configure"></a><span data-ttu-id="37aae-1910">TCP yuvası Iletme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="37aae-1910">TCP Socket Transmit Configure</span></span> 

#### <a name="nx_tcp_socket_transmit_configure"></a><span data-ttu-id="37aae-1911">nx_tcp_socket_transmit_configure</span><span class="sxs-lookup"><span data-stu-id="37aae-1911">nx_tcp_socket_transmit_configure</span></span>

<span data-ttu-id="37aae-1912">**Simge** ![ T C P yuvası iletme yapılandırma simgesi](./media/user-guide/netx-events/image148.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1912">**Icon** ![T C P socket transmit configure icon](./media/user-guide/netx-events/image148.png)</span></span>

<span data-ttu-id="37aae-1913">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1913">**Description**</span></span>

<span data-ttu-id="37aae-1914">Bu olay, nx_tcp_socket_transmit_configure aracılığıyla bir yuva için iletme seçeneklerini yapılandırmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1914">This event represents configuring the transmit options for a socket via nx_tcp_socket_transmit_configure.</span></span>

<span data-ttu-id="37aae-1915">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1915">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1916">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1916">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1917">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1917">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1918">Bilgi alanı 3: aktarım sırası derinliği</span><span class="sxs-lookup"><span data-stu-id="37aae-1918">Info Field 3: Transmit queue depth</span></span>
- <span data-ttu-id="37aae-1919">Bilgi alanı 4: zaman aşımı değeri</span><span class="sxs-lookup"><span data-stu-id="37aae-1919">Info Field 4: Timeout value</span></span>

### <a name="tcp-socket-window-update-notify-set"></a><span data-ttu-id="37aae-1920">TCP yuvası pencere güncelleştirme bildirim kümesi</span><span class="sxs-lookup"><span data-stu-id="37aae-1920">TCP Socket Window Update Notify Set</span></span> 

#### <a name="nx_tcp_window_update_notify_set"></a><span data-ttu-id="37aae-1921">nx_tcp_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="37aae-1921">nx_tcp_window_update_notify_set</span></span>

<span data-ttu-id="37aae-1922">**Simge** ![ T C P yuvası pencere güncelleştirme bildirim kümesi simgesi](./media/user-guide/netx-events/image149.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1922">**Icon** ![T C P socket window update notify set icon](./media/user-guide/netx-events/image149.png)</span></span>

<span data-ttu-id="37aae-1923">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1923">**Description**</span></span>

<span data-ttu-id="37aae-1924">Bu olay, nx_tcp_window_update_notify_set aracılığıyla uzak ana bilgisayar alma penceresinde bir artışın TCP yuvası alma bildirimini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1924">This event represents a TCP socket receiving notification of an increase in the remote host receive window via nx_tcp_window_update_notify_set.</span></span>

<span data-ttu-id="37aae-1925">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1925">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1926">Bilgi alanı 1: TCP yuvası Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1926">Info Field 1: Pointer to TCP socket</span></span>
- <span data-ttu-id="37aae-1927">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1927">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1928">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1928">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1929">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1929">Info Field 4: Not used</span></span>

### <a name="udp-enable"></a><span data-ttu-id="37aae-1930">UDP etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="37aae-1930">UDP Enable</span></span> 

#### <a name="nx_udp_enable"></a><span data-ttu-id="37aae-1931">nx_udp_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1931">nx_udp_enable</span></span>

<span data-ttu-id="37aae-1932">**Simge** ![ U D P etkinleştirme simgesi](./media/user-guide/netx-events/image150.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1932">**Icon** ![U D P enable icon](./media/user-guide/netx-events/image150.png)</span></span>

<span data-ttu-id="37aae-1933">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1933">**Description**</span></span>

<span data-ttu-id="37aae-1934">Bu olay nx_udp_enable aracılığıyla UDP etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1934">This event represents enabling UDP via nx_udp_enable.</span></span>

<span data-ttu-id="37aae-1935">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1935">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1936">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1936">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1937">Bilgi alanı 2: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1937">Info Field 2: Not used</span></span>
- <span data-ttu-id="37aae-1938">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1938">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1939">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1939">Info Field 4: Not used</span></span>

### <a name="udp-free-port-find"></a><span data-ttu-id="37aae-1940">UDP boş bağlantı noktası bulma</span><span class="sxs-lookup"><span data-stu-id="37aae-1940">UDP Free Port Find</span></span> 

#### <a name="nx_udp_free_port_find"></a><span data-ttu-id="37aae-1941">nx_udp_free_port_find</span><span class="sxs-lookup"><span data-stu-id="37aae-1941">nx_udp_free_port_find</span></span>

<span data-ttu-id="37aae-1942">**Simge** ![ U D P boş bağlantı noktası bul simgesi](./media/user-guide/netx-events/image151.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1942">**Icon** ![U D P free port find icon](./media/user-guide/netx-events/image151.png)</span></span>

<span data-ttu-id="37aae-1943">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1943">**Description**</span></span>

<span data-ttu-id="37aae-1944">Bu olay nx_udp_free_port_find aracılığıyla boş bir UDP bağlantı noktası bulmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1944">This event represents finding a free UDP port via nx_udp_free_port_find.</span></span>

<span data-ttu-id="37aae-1945">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1945">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1946">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1946">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1947">Bilgi alanı 2: arama yapılacak bağlantı noktası başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1947">Info Field 2: Starting port to search from</span></span>
- <span data-ttu-id="37aae-1948">Bilgi alanı 3: ücretsiz bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="37aae-1948">Info Field 3: Free port</span></span>
- <span data-ttu-id="37aae-1949">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1949">Info Field 4: Not used</span></span>

### <a name="udp-information-get"></a><span data-ttu-id="37aae-1950">UDP bilgisi al</span><span class="sxs-lookup"><span data-stu-id="37aae-1950">UDP Information Get</span></span> 

#### <a name="nx_udp_info_get"></a><span data-ttu-id="37aae-1951">nx_udp_info_get</span><span class="sxs-lookup"><span data-stu-id="37aae-1951">nx_udp_info_get</span></span>

<span data-ttu-id="37aae-1952">**Simge** ![ U D P bilgi al simgesi](./media/user-guide/netx-events/image152.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1952">**Icon** ![U D P information get icon](./media/user-guide/netx-events/image152.png)</span></span>

<span data-ttu-id="37aae-1953">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1953">**Description**</span></span>

<span data-ttu-id="37aae-1954">Bu olay nx_udp_info_get aracılığıyla bilgi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1954">This event represents getting information via nx_udp_info_get.</span></span>

<span data-ttu-id="37aae-1955">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1955">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1956">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1956">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1957">Bilgi alanı 2: gönderilen UDP baytları</span><span class="sxs-lookup"><span data-stu-id="37aae-1957">Info Field 2: UDP bytes sent</span></span>
- <span data-ttu-id="37aae-1958">Bilgi alanı 3: alınan UDP baytları</span><span class="sxs-lookup"><span data-stu-id="37aae-1958">Info Field 3: UDP bytes received</span></span>
- <span data-ttu-id="37aae-1959">Bilgi alanı 4: geçersiz paketler</span><span class="sxs-lookup"><span data-stu-id="37aae-1959">Info Field 4: Invalid packets</span></span>

### <a name="udp-socket-bind"></a><span data-ttu-id="37aae-1960">UDP yuvası bağlama</span><span class="sxs-lookup"><span data-stu-id="37aae-1960">UDP Socket Bind</span></span> 

#### <a name="nx_udp_socket_bind"></a><span data-ttu-id="37aae-1961">nx_udp_socket_bind</span><span class="sxs-lookup"><span data-stu-id="37aae-1961">nx_udp_socket_bind</span></span>

<span data-ttu-id="37aae-1962">**Simge** ![ U D P yuvası bağlama simgesi](./media/user-guide/netx-events/image153.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1962">**Icon** ![U D P socket bind icon](./media/user-guide/netx-events/image153.png)</span></span>

<span data-ttu-id="37aae-1963">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1963">**Description**</span></span>

<span data-ttu-id="37aae-1964">Bu olay, nx_udp_socket_bind aracılığıyla bir UDP yuvasını bağlantı noktasına bağlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1964">This event represents binding a UDP socket to a port via nx_udp_socket_bind.</span></span>

<span data-ttu-id="37aae-1965">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1965">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1966">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1966">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1967">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1967">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1968">Bilgi alanı 3: bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-1968">Info Field 3: Port number</span></span>
- <span data-ttu-id="37aae-1969">Bilgi alanı 4: bekleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="37aae-1969">Info Field 4: Wait option</span></span>

### <a name="udp-socket-bytes-available"></a><span data-ttu-id="37aae-1970">Kullanılabilir UDP yuva baytları</span><span class="sxs-lookup"><span data-stu-id="37aae-1970">UDP Socket Bytes Available</span></span> 

#### <a name="nx_udp_socket_bytes_available"></a><span data-ttu-id="37aae-1971">nx_udp_socket_bytes_available</span><span class="sxs-lookup"><span data-stu-id="37aae-1971">nx_udp_socket_bytes_available</span></span>

<span data-ttu-id="37aae-1972">**Simge** ![ U D P yuva baytları kullanılabilir simgesi](./media/user-guide/netx-events/image154.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1972">**Icon** ![U D P socket bytes available icon](./media/user-guide/netx-events/image154.png)</span></span>

<span data-ttu-id="37aae-1973">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1973">**Description**</span></span>

<span data-ttu-id="37aae-1974">Bu olay, UDP yuvasında nx_udp_socket_bytes_available aracılığıyla alınan geçerli bayt sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1974">This event represents the current number of bytes received on the UDP socket via nx_udp_socket_bytes_available.</span></span>

<span data-ttu-id="37aae-1975">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1975">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1976">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1976">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1977">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1977">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1978">Bilgi alanı 3: yuvada alınan baytlar</span><span class="sxs-lookup"><span data-stu-id="37aae-1978">Info Field 3: Bytes received on socket</span></span>
- <span data-ttu-id="37aae-1979">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1979">Info Field 4: Not used</span></span>

### <a name="udp-socket-checksum-disable"></a><span data-ttu-id="37aae-1980">UDP yuva sağlama toplamı devre dışı</span><span class="sxs-lookup"><span data-stu-id="37aae-1980">UDP Socket Checksum Disable</span></span> 

#### <a name="nx_udp_socket_checksum_disable"></a><span data-ttu-id="37aae-1981">nx_udp_socket_checksum_disable</span><span class="sxs-lookup"><span data-stu-id="37aae-1981">nx_udp_socket_checksum_disable</span></span>

<span data-ttu-id="37aae-1982">**Simge** ![ U D P soket sağlama toplamı devre dışı simgesi](./media/user-guide/netx-events/image155.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1982">**Icon** ![U D P socket checksum disable icon](./media/user-guide/netx-events/image155.png)</span></span>

<span data-ttu-id="37aae-1983">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1983">**Description**</span></span>

<span data-ttu-id="37aae-1984">Bu olay, nx_udp_socket_checksum_disable aracılığıyla bir UDP yuvasında veriler için sağlama toplamı devre dışı bırakmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1984">This event represents disabling the checksum for data on a UDP socket via nx_udp_socket_checksum_disable.</span></span>

<span data-ttu-id="37aae-1985">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1985">**Information Fields**</span></span> 

- <span data-ttu-id="37aae-1986">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1986">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1987">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1987">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1988">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1988">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1989">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1989">Info Field 4: Not used</span></span>

### <a name="udp-socket-checksum-enable"></a><span data-ttu-id="37aae-1990">UDP yuva sağlama toplamı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="37aae-1990">UDP Socket Checksum Enable</span></span> 

#### <a name="nx_udp_socket_checksum_enable"></a><span data-ttu-id="37aae-1991">nx_udp_socket_checksum_enable</span><span class="sxs-lookup"><span data-stu-id="37aae-1991">nx_udp_socket_checksum_enable</span></span>

<span data-ttu-id="37aae-1992">**Simge** ![ U D P yuva sağlama toplamı etkinleştir simgesi](./media/user-guide/netx-events/image156.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-1992">**Icon** ![U D P socket checksum enable icon](./media/user-guide/netx-events/image156.png)</span></span>

<span data-ttu-id="37aae-1993">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-1993">**Description**</span></span>

<span data-ttu-id="37aae-1994">Bu olay, nx_udp_socket_checksum_enable aracılığıyla bir yuvada sağlama toplamı işlemeyi etkinleştirmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-1994">This event represents enabling checksum processing on a socket via nx_udp_socket_checksum_enable.</span></span>

<span data-ttu-id="37aae-1995">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-1995">**Information Fields**</span></span>

- <span data-ttu-id="37aae-1996">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-1996">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-1997">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-1997">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-1998">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1998">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-1999">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-1999">Info Field 4: Not used</span></span>

### <a name="udp-socket-create"></a><span data-ttu-id="37aae-2000">UDP yuvası oluşturma</span><span class="sxs-lookup"><span data-stu-id="37aae-2000">UDP Socket Create</span></span> 

#### <a name="nx_udp_socket_create"></a><span data-ttu-id="37aae-2001">nx_udp_socket_create</span><span class="sxs-lookup"><span data-stu-id="37aae-2001">nx_udp_socket_create</span></span>

<span data-ttu-id="37aae-2002">**Simge** ![ U D P yuvası oluşturma simgesi](./media/user-guide/netx-events/image157.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-2002">**Icon** ![U D P socket create icon](./media/user-guide/netx-events/image157.png)</span></span>

<span data-ttu-id="37aae-2003">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-2003">**Description**</span></span>

<span data-ttu-id="37aae-2004">Bu olay nx_udp_socket_create aracılığıyla bir UDP yuvası oluşturmayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2004">This event represents creating a UDP socket via nx_udp_socket_create.</span></span>

<span data-ttu-id="37aae-2005">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2005">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2006">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-2006">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-2007">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2007">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-2008">Bilgi alanı 3: hizmet türü</span><span class="sxs-lookup"><span data-stu-id="37aae-2008">Info Field 3: Type of service</span></span>
- <span data-ttu-id="37aae-2009">Bilgi alanı 4: en fazla alma kuyruğu</span><span class="sxs-lookup"><span data-stu-id="37aae-2009">Info Field 4: Maximum receive queue</span></span>

### <a name="udp-socket-delete-event"></a><span data-ttu-id="37aae-2010">UDP yuvası silme olayı</span><span class="sxs-lookup"><span data-stu-id="37aae-2010">UDP Socket Delete Event</span></span> 

#### <a name="nx_udp_socket_delete-event"></a><span data-ttu-id="37aae-2011">nx_udp_socket_delete olayı</span><span class="sxs-lookup"><span data-stu-id="37aae-2011">nx_udp_socket_delete event</span></span>

<span data-ttu-id="37aae-2012">**Simge** ![ U D P yuvası silme olayı simgesi](./media/user-guide/netx-events/image158.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-2012">**Icon** ![U D P socket delete event icon](./media/user-guide/netx-events/image158.png)</span></span>

<span data-ttu-id="37aae-2013">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-2013">**Description**</span></span>

<span data-ttu-id="37aae-2014">Bu olay nx_udp_socket_delete aracılığıyla bir UDP yuvasını silmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2014">This event represents deleting a UDP socket via nx_udp_socket_delete.</span></span>

<span data-ttu-id="37aae-2015">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2015">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2016">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-2016">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-2017">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2017">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-2018">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-2018">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-2019">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-2019">Info Field 4: Not used</span></span>

### <a name="udp-socket-information-get-event"></a><span data-ttu-id="37aae-2020">UDP yuva bilgileri Get olayı</span><span class="sxs-lookup"><span data-stu-id="37aae-2020">UDP Socket Information Get Event</span></span> 

#### <a name="nx_udp_socket_info_get-event"></a><span data-ttu-id="37aae-2021">nx_udp_socket_info_get olayı</span><span class="sxs-lookup"><span data-stu-id="37aae-2021">nx_udp_socket_info_get event</span></span>

<span data-ttu-id="37aae-2022">**Simge** ![ U D P yuva bilgileri olay al simgesi](./media/user-guide/netx-events/image159.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-2022">**Icon** ![U D P socket information get event icon](./media/user-guide/netx-events/image159.png)</span></span>

<span data-ttu-id="37aae-2023">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-2023">**Description**</span></span>

<span data-ttu-id="37aae-2024">Bu olay nx_udp_socket_info_get aracılığıyla bir UDP yuvası hakkında bilgi almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2024">This event represents getting information about a UDP socket via nx_udp_socket_info_get.</span></span>

<span data-ttu-id="37aae-2025">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2025">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2026">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-2026">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-2027">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2027">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-2028">Bilgi alanı 3: yuva aracılığıyla gönderilen baytlar</span><span class="sxs-lookup"><span data-stu-id="37aae-2028">Info Field 3: Bytes sent through socket</span></span>
- <span data-ttu-id="37aae-2029">Bilgi alanı 4: yuva aracılığıyla alınan baytlar</span><span class="sxs-lookup"><span data-stu-id="37aae-2029">Info Field 4: Bytes received through socket</span></span>

### <a name="udp-socket-interface-set"></a><span data-ttu-id="37aae-2030">UDP yuva arabirimi kümesi</span><span class="sxs-lookup"><span data-stu-id="37aae-2030">UDP Socket Interface Set</span></span> 

#### <a name="nx_udp_socket_interface_set-event"></a><span data-ttu-id="37aae-2031">nx_udp_socket_interface_set olayı</span><span class="sxs-lookup"><span data-stu-id="37aae-2031">nx_udp_socket_interface_set event</span></span>

<span data-ttu-id="37aae-2032">**Simge** ![ U D P yuva arabirimi kümesi simgesi](./media/user-guide/netx-events/image160.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-2032">**Icon** ![U D P socket interface set icon](./media/user-guide/netx-events/image160.png)</span></span>

<span data-ttu-id="37aae-2033">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-2033">**Description**</span></span>

<span data-ttu-id="37aae-2034">Bu olay, belirtilen UDP yuvasının giden arabirimini nx_udp_socket_interface_set aracılığıyla belirtilen arabirimle ayarlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2034">This event represents setting the outgoing interface of the specified UDP socket with the specified interface via nx_udp_socket_interface_set.</span></span>

<span data-ttu-id="37aae-2035">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2035">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2036">Bilgi alanı 1: UDP yuvası Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2036">Info Field 1: Pointer to UDP socket</span></span>
- <span data-ttu-id="37aae-2037">Bilgi alanı 2: yuva arabirimine karşılık gelen dizin</span><span class="sxs-lookup"><span data-stu-id="37aae-2037">Info Field 2: Index corresponding to the interface for the socket</span></span>
- <span data-ttu-id="37aae-2038">Bilgi alanı 3: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-2038">Info Field 3: Not used</span></span>
- <span data-ttu-id="37aae-2039">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-2039">Info Field 4: Not used</span></span>

### <a name="udp-socket-port-get"></a><span data-ttu-id="37aae-2040">UDP yuva bağlantı noktası al</span><span class="sxs-lookup"><span data-stu-id="37aae-2040">UDP Socket Port Get</span></span> 

#### <a name="nx_udp_socket_port_get"></a><span data-ttu-id="37aae-2041">nx_udp_socket_port_get</span><span class="sxs-lookup"><span data-stu-id="37aae-2041">nx_udp_socket_port_get</span></span>

<span data-ttu-id="37aae-2042">**Simge** ![ U D P yuva bağlantı noktası al simgesi](./media/user-guide/netx-events/image161.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-2042">**Icon** ![U D P socket port get icon](./media/user-guide/netx-events/image161.png)</span></span>

<span data-ttu-id="37aae-2043">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-2043">**Description**</span></span>

<span data-ttu-id="37aae-2044">Bu olay, belirtilen UDP yuvasının nx_udp_socket_port_get aracılığıyla bağlandığı UDP bağlantı noktasının alınması temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2044">This event represents retrieving the UDP port the specified UDP socket is bound to via nx_udp_socket_port_get.</span></span>

<span data-ttu-id="37aae-2045">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2045">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2046">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-2046">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-2047">Bilgi alanı 2: UDP yuvası Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2047">Info Field 2: Pointer to UDP socket</span></span>
- <span data-ttu-id="37aae-2048">Bilgi alanı 3: bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-2048">Info Field 3: Port number</span></span>
- <span data-ttu-id="37aae-2049">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-2049">Info Field 4: Not used</span></span>

### <a name="udp-socket-receive"></a><span data-ttu-id="37aae-2050">UDP yuvası alma</span><span class="sxs-lookup"><span data-stu-id="37aae-2050">UDP Socket Receive</span></span> 

#### <a name="nx_udp_socket_receive"></a><span data-ttu-id="37aae-2051">nx_udp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="37aae-2051">nx_udp_socket_receive</span></span>

<span data-ttu-id="37aae-2052">**Simge** ![ U D P yuvası alma simgesi](./media/user-guide/netx-events/image162.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-2052">**Icon** ![U D P socket receive icon](./media/user-guide/netx-events/image162.png)</span></span>

<span data-ttu-id="37aae-2053">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-2053">**Description**</span></span>

<span data-ttu-id="37aae-2054">Bu olay, belirtilen UDP yuvasında nx_udp_socket_receive aracılığıyla veri almayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2054">This event represents receiving data on the specified UDP socket via nx_udp_socket_receive.</span></span>

<span data-ttu-id="37aae-2055">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2055">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2056">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-2056">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-2057">Bilgi alanı 2: UDP yuvası Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2057">Info Field 2: Pointer to UDP socket</span></span>
- <span data-ttu-id="37aae-2058">Bilgi alanı 3: alınan paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2058">Info Field 3: Pointer to received packet</span></span>
- <span data-ttu-id="37aae-2059">Bilgi alanı 4: paket boyutu alındı</span><span class="sxs-lookup"><span data-stu-id="37aae-2059">Info Field 4: Received packet size</span></span>

### <a name="udp-socket-receive-notify"></a><span data-ttu-id="37aae-2060">UDP yuvası alma bildirimi</span><span class="sxs-lookup"><span data-stu-id="37aae-2060">UDP Socket Receive Notify</span></span> 

#### <a name="nx_udp_socket_receive_notify"></a><span data-ttu-id="37aae-2061">nx_udp_socket_receive_notify</span><span class="sxs-lookup"><span data-stu-id="37aae-2061">nx_udp_socket_receive_notify</span></span>

<span data-ttu-id="37aae-2062">**Simge** ![ U D P yuvası alma bildirim simgesi ](./media/user-guide/netx-events/image163.png) s **açıklaması**</span><span class="sxs-lookup"><span data-stu-id="37aae-2062">**Icon** ![U D P socket receive notify icon](./media/user-guide/netx-events/image163.png)s **Description**</span></span>

<span data-ttu-id="37aae-2063">Bu olay nx_udp_socket_receive_notify aracılığıyla bir alma bildirimi geri araması kaydetmeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2063">This event represents registering a receive notify callback via nx_udp_socket_receive_notify.</span></span>

<span data-ttu-id="37aae-2064">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2064">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2065">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-2065">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-2066">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2066">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-2067">Bilgi alanı 3: bildirim alma işlevi bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-2067">Info Field 3: Pointer to receive notify function Info Field 4: Not used</span></span>

### <a name="udp-socket-send"></a><span data-ttu-id="37aae-2068">UDP yuvası gönderme</span><span class="sxs-lookup"><span data-stu-id="37aae-2068">UDP Socket Send</span></span> 

#### <a name="nx_udp_socket_send"></a><span data-ttu-id="37aae-2069">nx_udp_socket_send</span><span class="sxs-lookup"><span data-stu-id="37aae-2069">nx_udp_socket_send</span></span>

<span data-ttu-id="37aae-2070">**Simge** ![ U D P yuvası gönderme simgesi](./media/user-guide/netx-events/image164.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-2070">**Icon** ![U D P socket send icon](./media/user-guide/netx-events/image164.png)</span></span>

<span data-ttu-id="37aae-2071">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-2071">**Description**</span></span>

<span data-ttu-id="37aae-2072">Bu olay nx_udp_socket_send aracılığıyla bir UDP yuvası üzerinden veri göndermeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2072">This event represents sending data through a UDP socket via nx_udp_socket_send.</span></span>

<span data-ttu-id="37aae-2073">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2073">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2074">Bilgi alanı 1: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2074">Info Field 1: Pointer to socket</span></span>
- <span data-ttu-id="37aae-2075">Bilgi alanı 2: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2075">Info Field 2: Pointer to packet</span></span>
- <span data-ttu-id="37aae-2076">Bilgi alanı 3: paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="37aae-2076">Info Field 3: Packet length</span></span>
- <span data-ttu-id="37aae-2077">Bilgi alanı 4: hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-2077">Info Field 4: Destination IP address</span></span>

### <a name="udp-socket-unbind"></a><span data-ttu-id="37aae-2078">UDP yuvası bağlantısı kesme</span><span class="sxs-lookup"><span data-stu-id="37aae-2078">UDP Socket Unbind</span></span> 

#### <a name="nx_udp_socket_unbind"></a><span data-ttu-id="37aae-2079">nx_udp_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="37aae-2079">nx_udp_socket_unbind</span></span>

<span data-ttu-id="37aae-2080">**Simge** ![ U D P yuvası çözme simgesi](./media/user-guide/netx-events/image165.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-2080">**Icon** ![U D P socket unbind icon](./media/user-guide/netx-events/image165.png)</span></span>

<span data-ttu-id="37aae-2081">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-2081">**Description**</span></span>

<span data-ttu-id="37aae-2082">Bu olay, nx_udp_socket_unbind aracılığıyla bir yuva ile UDP bağlantı noktası bağlamayı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2082">This event represents unbinding a UDP port with a socket via nx_udp_socket_unbind.</span></span>

<span data-ttu-id="37aae-2083">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2083">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2084">Bilgi alanı 1: IP örneğine yönelik Işaretçi</span><span class="sxs-lookup"><span data-stu-id="37aae-2084">Info Field 1: Pointer to IP instance</span></span>
- <span data-ttu-id="37aae-2085">Bilgi alanı 2: yuva Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2085">Info Field 2: Pointer to socket</span></span>
- <span data-ttu-id="37aae-2086">Bilgi alanı 3: bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-2086">Info Field 3: Port number</span></span>
- <span data-ttu-id="37aae-2087">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-2087">Info Field 4: Not used</span></span>

### <a name="udp-source-extract"></a><span data-ttu-id="37aae-2088">UDP kaynağı ayıklama</span><span class="sxs-lookup"><span data-stu-id="37aae-2088">UDP Source Extract</span></span> 

#### <a name="nx_udp_socket_create"></a><span data-ttu-id="37aae-2089">nx_udp_socket_create</span><span class="sxs-lookup"><span data-stu-id="37aae-2089">nx_udp_socket_create</span></span>

<span data-ttu-id="37aae-2090">**Simge** ![ U D P kaynağı ayıklama simgesi](./media/user-guide/netx-events/image166.png)</span><span class="sxs-lookup"><span data-stu-id="37aae-2090">**Icon** ![U D P source extract icon](./media/user-guide/netx-events/image166.png)</span></span>

<span data-ttu-id="37aae-2091">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="37aae-2091">**Description**</span></span>

<span data-ttu-id="37aae-2092">Bu olay, alınan bir UDP paketinin IP adresi ve bağlantı noktası numarasının nx_udp_source_extract aracılığıyla alınmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="37aae-2092">This event represents getting the IP address and port number of a received UDP packet via nx_udp_source_extract.</span></span>

<span data-ttu-id="37aae-2093">**Bilgi alanları**</span><span class="sxs-lookup"><span data-stu-id="37aae-2093">**Information Fields**</span></span>

- <span data-ttu-id="37aae-2094">Bilgi alanı 1: paket Işaretçisi</span><span class="sxs-lookup"><span data-stu-id="37aae-2094">Info Field 1: Pointer to packet</span></span>
- <span data-ttu-id="37aae-2095">Bilgi alanı 2: gönderenin IP adresi</span><span class="sxs-lookup"><span data-stu-id="37aae-2095">Info Field 2: Sender's IP address</span></span>
- <span data-ttu-id="37aae-2096">Bilgi alanı 3: gönderenin bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="37aae-2096">Info Field 3: Sender's port number</span></span>
- <span data-ttu-id="37aae-2097">Bilgi alanı 4: kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="37aae-2097">Info Field 4: Not used</span></span>