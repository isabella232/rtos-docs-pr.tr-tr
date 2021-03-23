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
# <a name="chapter-8---azure-rtos-netx-trace-events"></a>Bölüm 8-Azure RTOS NetX izleme olayları

Bu bölümde, Azure RTOS NetX olaylarının açıklaması yer almaktadır. 

## <a name="list-of-events-and-icons"></a>Olay ve simgelerin listesi

Aşağıda, TraceX tarafından görünen NetX olaylarının bir listesi verilmiştir.

| Simge                                           | Anlamı                 |
| -------------------------------- | ------------------------------------- |
| ![İç A R P Isteği alma simgesi](./media/user-guide/netx-events/image1.png)    | İç ARP Isteği alma |
| ![Dahili A R P Isteği gönderme simgesi](./media/user-guide/netx-events/image2.png)    | İç ARP Isteği gönderme |
| ![Dahili A R P yanıtı alma simgesi](./media/user-guide/netx-events/image3.png)    | İç ARP yanıtı alma |
| ![Dahili A R P yanıtı gönderme simgesi](./media/user-guide/netx-events/image4.png)    | İç ARP yanıtı gönderme |
| ![İç ı C M P alma simgesi](./media/user-guide/netx-events/image5.png)    | İç ıCMP alma |
| ![İç ı C M P Gönder simgesi](./media/user-guide/netx-events/image6.png)    | İç ıCMP gönderme |
| ![İç NetX ı G M P alma simgesi](./media/user-guide/netx-events/image7.png)    | İç NetX ıGMP alma |
| ![İç ı P alma simgesi](./media/user-guide/netx-events/image8.png)    | İç IP alma |
| ![İç ı P Gönder simgesi](./media/user-guide/netx-events/image9.png)    | İç IP gönderme |
| ![İç T C P veri alma simgesi](./media/user-guide/netx-events/image10.png)    | İç TCP veri alma |
| ![İç T C P veri gönderme simgesi](./media/user-guide/netx-events/image11.png)    | İç TCP veri gönderme |
| ![İç T C P FIN alma simgesi](./media/user-guide/netx-events/image12.png)    | İç TCP FIN alma |
| ![İç T C P F ı N Gönder simgesi](./media/user-guide/netx-events/image13.png)    | İç TCP FIN gönderme |
| ![İç T C P R S T al simgesi](./media/user-guide/netx-events/image14.png)    | İç TCP RST alma |
| ![İç T C P R S T Gönder simgesi](./media/user-guide/netx-events/image15.png)    | İç TCP RST gönderme |
| ![İç T C P S e N al simgesi](./media/user-guide/netx-events/image16.png)    | İç TCP SYN alma |
| ![İç T C P S e N Gönder simgesi](./media/user-guide/netx-events/image17.png)    | İç TCP SYN Send |
| ![İç U D P al simgesi](./media/user-guide/netx-events/image18.png)    | İç UDP alma |
| ![İç U D P Gönder simgesi](./media/user-guide/netx-events/image19.png)    | İç UDP gönderme |
| ![Dahili R A R P alma simgesi](./media/user-guide/netx-events/image20.png)    | İç RARP alma |
| ![Dahili R A R P Gönder simgesi](./media/user-guide/netx-events/image21.png)    | İç RARP gönderme |
| ![İç T C P yeniden deneme simgesi](./media/user-guide/netx-events/image22.png)    | İç TCP yeniden denemesi |
| ![İç T C P durum değiştirme simgesi](./media/user-guide/netx-events/image23.png)    | İç TCP durum değişikliği |
| ![İç g/ç sürücü paketi gönderme simgesi](./media/user-guide/netx-events/image24.png)    | İç g/ç sürücü paketi gönderme |
| ![simg](./media/user-guide/netx-events/image25.png)    | İç g/ç sürücüsü başlatma |
| ![İç g/ç sürücüsü başlatma simgesi](./media/user-guide/netx-events/image26.png)    | İç g/ç sürücü bağlantısı etkinleştir |
| ![İç g/ç sürücü bağlantısı devre dışı simgesi](./media/user-guide/netx-events/image27.png)    | İç g/ç sürücüsü bağlantısı devre dışı |
| ![İç g/ç sürücü paketi yayını simgesi](./media/user-guide/netx-events/image28.png)    | İç g/ç sürücü paketi yayını |
| ![İç g/ç sürücüsü ARP gönderme simgesi](./media/user-guide/netx-events/image29.png)    | İç g/ç sürücüsü ARP gönderme |
| ![İç g/ç sürücüsü ARP yanıtı gönderme simgesi](./media/user-guide/netx-events/image30.png)    | İç g/ç sürücüsü ARP yanıtı gönderme |
| ![İç g/ç sürücüsü RARP Gönder simgesi](./media/user-guide/netx-events/image31.png)    | İç g/ç sürücüsü RARP gönderme |
| ![İç g/ç sürücüsü çok noktaya yayın Birleştir simgesi](./media/user-guide/netx-events/image32.png)    | İç g/ç sürücüsü çok noktaya yayın katılımı |
| ![İç g/ç sürücüsü çok noktaya yayın çıkış simgesi](./media/user-guide/netx-events/image33.png)    | İç g/ç sürücüsü çok noktaya yayını bırakma |
| ![İç g/ç sürücüsü durum Al simgesi](./media/user-guide/netx-events/image34.png)    | İç g/ç sürücüsü Get durumu |
| ![İç g/ç sürücüsü al hız simgesi](./media/user-guide/netx-events/image35.png)    | İç g/ç sürücüsü edinme hızı |
| ![İç g/ç sürücüsü çift yönlü tür simgesi al](./media/user-guide/netx-events/image36.png)    | İç g/ç sürücüsü çift yönlü türü al |
| ![İç g/ç sürücüsü hata sayısını Al simgesi](./media/user-guide/netx-events/image37.png)    | İç g/ç sürücüsü hata sayısını Al |
| ![İç g/ç sürücüsü RX sayısı simgesi al](./media/user-guide/netx-events/image38.png)    | İç g/ç sürücüsü RX sayısı al |
| ![İç g/ç sürücüsü TX sayısı simgesini al](./media/user-guide/netx-events/image39.png)    | İç g/ç sürücüsü TX sayısı al |
| ![İç g/ç sürücüsü ayırma hatalarını al simgesi](./media/user-guide/netx-events/image40.png)    | İç g/ç sürücüsü ayırma hatalarını al |
| ![İç g/ç sürücüsü başlatması kaldır simgesi](./media/user-guide/netx-events/image41.png)    | İç g/ç sürücüsü başlatması geri al |
| ![İç g/ç sürücüsü ertelenmiş Işleme simgesi](./media/user-guide/netx-events/image42.png)    | İç g/ç sürücüsü ertelenmiş Işleme |
| ![R P dinamik girdileri geçersiz kılar simgesi](./media/user-guide/netx-events/image43.png)    | **ARP dinamik girdileri geçersiz kılar** (*nx_arp_dynamic_entries_invalidate*) |
| ![R P dinamik giriş kümesi simgesi](./media/user-guide/netx-events/image44.png)    | **ARP dinamik giriş kümesi** (*nx_arp_dynamic_entry_set*) |
| ![R P etkinleştirme simgesi](./media/user-guide/netx-events/image45.png)    | **ARP etkinleştir** (*nx_arp_enable*) |
| ![R P gereksiz Yolus Gönder simgesi](./media/user-guide/netx-events/image46.png)    | **ARP gereksiz Yolus gönderme** (*nx_arp_gratuitous_send*) |
| ![R P donanım adresi bul simgesi](./media/user-guide/netx-events/image47.png)    | **ARP donanım adresi bul** (*nx_arp_hardware_address_find*) |
| ![R P bilgi al simgesi](./media/user-guide/netx-events/image48.png)    | **ARP bilgileri Get** (*nx_arp_info_get*) |
| ![R P IP adresi bulma simgesi](./media/user-guide/netx-events/image49.png)    | **ARP IP adresi bulma** (*nx_arp_ip_address_find*) |
| ![R P statik giriş oluştur simgesi](./media/user-guide/netx-events/image50.png)    | **ARP statik girdisi oluşturma** (*nx_arp_static_entry_create*) |
| ![R P statik girdileri Sil simgesi](./media/user-guide/netx-events/image51.png)    | **ARP statik girdileri silme** (*nx_arp_static_entries_delete*) |
| ![R P statik giriş silme simgesi](./media/user-guide/netx-events/image52.png)    | **ARP statik giriş silme** (*nx_arp_static_entry_delete*) |
| ![Duo önbellek girişi silme simgesi](./media/user-guide/netx-events/image53.png)    | **Duo önbellek girişi silme** (*nxd_nd_cache_entry_delete*) |
| ![Duo önbellek girdisi kümesi simgesi](./media/user-guide/netx-events/image54.png)    | **Duo önbellek giriş kümesi** (*nxd_nd_cache_entry_set*) |
| ![Duo önbelleği geçersiz kıl simgesi](./media/user-guide/netx-events/image55.png)    | **Duo önbelleği geçersiz kıl** (*nxd_nd_cache_invalidate*) |
| ![Duo önbelleği ı P adresi bul simgesi](./media/user-guide/netx-events/image56.png)    | **Duo ÖNBELLEĞI IP adresi bulma** (*nxd_nd_cache_ip_address_find*) |
| ![Duo ı C M P etkinleştir simgesi](./media/user-guide/netx-events/image57.png)    | **Duo ICMP etkinleştir** (*nxd_icmp_enable*) |
| ![Duo ı C M P I P v 6 ping simgesi](./media/user-guide/netx-events/image58.png)    | **Duo ICMP IPv6 Ping** (*nxd_icmp_ping*) |
| ![Duo ı P maks. yük boyutu bul simgesi](./media/user-guide/netx-events/image59.png)    | **Duo IP en fazla yük boyutu bul** (*nx_max_payload_size_find*) |
| ![Duo ı P ham paket Gönder simgesi](./media/user-guide/netx-events/image60.png)    | **Duo IP ham paket gönderme** (*nxd_ip_raw_packet_send*) |
| ![Duo ı P v 6 varsayılan yönlendirici Ekle simgesi](./media/user-guide/netx-events/image61.png)    | **Duo IPv6 varsayılan yönlendirici eklentisi** (*nxd_ipv6_default_router_add*) |
| ![Duo ı P v 6 varsayılan yönlendirici silme simgesi](./media/user-guide/netx-events/image62.png)    | **Duo IPv6 varsayılan yönlendirici silme** (*nxd_ipv6_default_router_delete)* |
| ![Duo ı P v 6 etkinleştirme simgesi](./media/user-guide/netx-events/image63.png)    | **Duo IPv6 etkinleştir** (*nxd_ipv6_enable)* |
| ![Duo ı P v 6 genel adres al simgesi](./media/user-guide/netx-events/image64.png)    | **Duo IPv6 genel adresi al** (*nxd_ipv6_global_address_get*) |
| ![Duo ı P v 6 genel adres kümesi simgesi](./media/user-guide/netx-events/image65.png)    | **Duo IPv6 genel adres kümesi** (*nxd_ipv6_global_address_set*) |
| ![Duo ı P v 6 babacığım Işlem simgesi](./media/user-guide/netx-events/image66.png)    | **Duo IPv6, babacığım işlemi** (*nxd_ipv6_initiate_dad_process*) |
| ![Duo ı P v 6 arabirim adresi al simgesi](./media/user-guide/netx-events/image67.png)    | **Duo IPv6 arabirim adresi Get** (*nxd_ipv6_interface_address_get*) |
| ![Duo ı P v 6 arabirim adres kümesi simgesi](./media/user-guide/netx-events/image68.png)    | **Duo IPv6 arabirimi adres kümesi** (*nxd_ipv6_interface_address_set*) |
| ![Duo ı P v 6 bağlantısı yerel adres al simgesi](./media/user-guide/netx-events/image69.png)    | **Duo IPv6 bağlantısı yerel adres Get** (*nxd_ipv6_linklocal_address_get*) |
| ![Duo ı P v 6 bağlantısı yerel adres kümesi simgesi](./media/user-guide/netx-events/image70.png)    | **Duo IPv6 bağlantısı yerel adres kümesi** (*nxd_ipv6_linklocal_address_set*) |
| ![Duo ı P v 6 ham paket Gönder simgesi](./media/user-guide/netx-events/image71.png)    | **Duo IPv6 ham paket gönderme** (*nxd_ipv6_raw_packet_send)* |
| ![Duo T C P soket eş bilgileri al simgesi](./media/user-guide/netx-events/image72.png)    | **Duo TCP yuvası eş bilgileri Get** (*nxd_tcp_socket_peer_info_get*) |
| ![Duo T C P yuva kümesi arabirim simgesi](./media/user-guide/netx-events/image73.png)    | **Duo TCP yuva kümesi arabirimi** (*nxd_tcp_socket_set_interface*) |
| ![Duo U D P yuvası gönderme simgesi](./media/user-guide/netx-events/image74.png)    | **Duo UDP yuvası gönderme** (*nxd_udp_socket_send*) |
| ![Duo U D P yuva kümesi arabirim simgesi](./media/user-guide/netx-events/image75.png)    | **Duo UDP yuva kümesi arabirimi** (*nxd_udp_socket_set_interface*) |
| ![Duo U D P kaynağı ayıklama simgesi](./media/user-guide/netx-events/image76.png)    | **Duo UDP kaynağı ayıklama** (*nxd_udp_source_extract*) |
| ![I C M P etkinleştir simgesi](./media/user-guide/netx-events/image77.png)    | **ICMP etkinleştirme** (*nx_icmp_enable*) |
| ![I C M P bilgi al simgesi](./media/user-guide/netx-events/image78.png)    | **ICMP bilgileri al** (*nx_icmp_info_get*) |
| ![I C M P ping simgesi](./media/user-guide/netx-events/image79.png)    | **ICMP ping** (*nx_icmp_ping*) |
| ![G G M P etkinleştirme simgesi](./media/user-guide/netx-events/image80.png)    | **IGMP etkinleştirme** (*nx_igmp_enable*) |
| ![G-M P bilgi al simgesi](./media/user-guide/netx-events/image81.png)    | **IGMP bilgileri al** (*nx_igmp_info_get*) |
| ![I G M P geri döngü devre dışı simgesi](./media/user-guide/netx-events/image82.png)    | **IGMP geri döngü devre dışı** (*nx_igmp_loopback_disable*) |
| ![I G M P geri döngü etkinleştirme simgesi](./media/user-guide/netx-events/image83.png)    | **IGMP geri döngü etkinleştirme** (*nx_igmp_loopback_enable*) |
| ![G & urum çok noktaya yayın Birleştir simgesi](./media/user-guide/netx-events/image84.png)    | **IGMP çok noktaya yayın katılımı** (*nx_igmp_multicast_join*) |
| ![G & urum çok noktaya yayın çıkış simgesi](./media/user-guide/netx-events/image85.png)    | **IGMP çok noktaya yayın** (*nx_igmp_multicast_leave*) |
| ![I P adres değişikliği bildirim simgesi](./media/user-guide/netx-events/image86.png)    | **IP adresi değişikliği bildirme** (*nx_ip_address_change_notify*) |
| ![I P adresi al simgesi](./media/user-guide/netx-events/image87.png)    | **IP adresi al** (*nx_ip_address_get*) |
| ![I P adres kümesi simgesi](./media/user-guide/netx-events/image88.png)    | **IP adresi kümesi** (*nx_ip_address_set*) |
| ![I P Oluştur simgesi](./media/user-guide/netx-events/image89.png)    | **IP oluşturma** (*nx_ip_create*) |
| ![I P Sil simgesi](./media/user-guide/netx-events/image90.png)    | **IP silme** (*nx_ip_delete*) |
| ![I P sürücüsü doğrudan komut simgesi](./media/user-guide/netx-events/image91.png)    | **IP sürücüsü doğrudan komutu** (*nx_ip_driver_direct_command*) |
| ![I P Iletme devre dışı simgesi](./media/user-guide/netx-events/image92.png)    | **IP Iletme devre dışı** (*nx_ip_forwarding_disable*) |
| ![I P Iletme etkinleştirme simgesi](./media/user-guide/netx-events/image93.png)    | **IP Iletme etkinleştir** (*nx_ip_forwarding_enable*) |
| ![I P parçanız devre dışı simgesi](./media/user-guide/netx-events/image94.png)    | **IP parçası devre dışı** (*nx_ip_fragment_disable*) |
| ![I P parçası etkinleştirme simgesi](./media/user-guide/netx-events/image95.png)    | **IP parçası etkinleştir** (*nx_ip_fragment_enable*)  |
| ![I P ağ geçidi adres kümesi simgesi](./media/user-guide/netx-events/image96.png)    | **IP ağ geçidi adres kümesi** (*nx_ip_gateway_address_set*) |
| ![I P bilgileri al simgesi](./media/user-guide/netx-events/image97.png)    | **IP bilgileri al** (*nx_ip_info_get*) |
| ![I P arabirimi Iliştirme simgesi](./media/user-guide/netx-events/image98.png)    | **IP arabirimine iliştirme** (*nx_ip_interface_attach*) |
| ![I P arabirim bilgisi al simgesi](./media/user-guide/netx-events/image99.png)    | **IP arabirimi bilgileri al** (*nx_ip_interface_info_get*) |
| ![I P ham paket devre dışı simgesi](./media/user-guide/netx-events/image100.png)    | **IP ham paket devre dışı** (*nx_ip_raw_packet_disable*) |
| ![I P RAW paketi etkinleştirme simgesi](./media/user-guide/netx-events/image101.png)    | **IP ham paket etkinleştir** (*nx_ip_raw_packet_enable*) |
| ![I P ham paket alma simgesi](./media/user-guide/netx-events/image102.png)    | **IP ham paket alma** (*nx_ip_raw_packet_receive*) |
| ![I P ham paket Gönder simgesi](./media/user-guide/netx-events/image103.png)    | **IP ham paket gönderme** (*nx_ip_raw_packet_send*) |
| ![I P statik yol ekleme simgesi](./media/user-guide/netx-events/image104.png)    | **IP statik yol ekleme** (*nx_ip_static_route_add*) |
| ![I P statik yol silme simgesi](./media/user-guide/netx-events/image105.png)    | **IP statik yol silme** (*nx_ip_static_route_delete)* |
| ![I P durum denetimi simgesi](./media/user-guide/netx-events/image106.png)    | **IP durum denetimi** (*nx_ip_status_check*)|
| ![I P S E C etkinleştir simgesi](./media/user-guide/netx-events/image107.png)    | **IPSec etkinleştir** (*nx_ipsec_enable)* |
| ![Paket ayırma simgesi](./media/user-guide/netx-events/image108.png)    | **Paket ayırma** (*nx_packet_allocate*) |
| ![Paket kopyalama simgesi](./media/user-guide/netx-events/image109.png)    | **Paket kopyası** (*nx_packet_copy*) |
| ![Paket verileri ekleme simgesi](./media/user-guide/netx-events/image110.png)    | **Paket verileri ekleme** (*nx_packet_data_append*) |
| ![Paket verileri ayıklama fark simgesi](./media/user-guide/netx-events/image111.png)    | **Paket verileri ayıklama kayması** (*nx_packet_data_extract_offset*) |
| ![Paket verilerini alma simgesi](./media/user-guide/netx-events/image112.png)    | **Paket verileri alma** (*nx_packet_data_retrieve*) |
| ![Paket uzunluğu al simgesi](./media/user-guide/netx-events/image113.png)    | **Paket uzunluğu al** (*nx_packet_length_get*) |
| ![Paket havuzu oluştur simgesi](./media/user-guide/netx-events/image114.png)    | **Paket havuzu oluşturma** (*nx_packet_pool_create*) |
| ![Paket havuzu silme simgesi](./media/user-guide/netx-events/image115.png)    | **Paket havuzu silme** (*nx_packet_pool_delete*) |
| ![Paket havuzu bilgileri al simgesi](./media/user-guide/netx-events/image116.png)    | **Paket havuzu bilgileri Get** (*nx_packet_pool_info_get*) |
| ![Paket yayını simgesi](./media/user-guide/netx-events/image117.png)    | **Paket sürümü** (*nx_packet_release*) |
| ![Paket Iletme yayını simgesi](./media/user-guide/netx-events/image118.png)    | **Paket Iletme sürümü** (*nx_packet_transmit_release*) |
| ![R A R P devre dışı simgesi](./media/user-guide/netx-events/image119.png)    | **RARP Disable** (*nx_rarp_disable*) |
| ![R A R P etkinleştirme simgesi](./media/user-guide/netx-events/image120.png)    | **RARP etkinleştir** (*nx_rarp_enable*) |
| ![R A R P bilgi al simgesi](./media/user-guide/netx-events/image121.png)    | **RARP Information Get** (*nx_rarp_info_get*) |
| ![Sistem başlatma simgesi](./media/user-guide/netx-events/image122.png)    | **Sistem başlatma** (*nx_system_initialize*) |
| ![T C P Istemci yuvası bağlama simgesi](./media/user-guide/netx-events/image123.png)    | **TCP Istemci yuvası bağlama** (*nx_tcp_client_socket_bind*) |
| ![T C P Istemci yuvası bağlantı simgesi](./media/user-guide/netx-events/image124.png)    | **TCP Istemci yuvası bağlantısı** (*nx_tcp_client_socket_connect*) |
| ![T C P Istemci yuva bağlantı noktası al simgesi](./media/user-guide/netx-events/image125.png)    | **TCP Istemci yuva bağlantı noktası al** (*nx_tcp_client_socket_port_get*) |
| ![T C P Istemci yuvası bağlantı çözme simgesi](./media/user-guide/netx-events/image126.png)    | **TCP Istemci yuvası bağlantısı kesme** (*nx_tcp_client_socket_unbind*) |
| ![T C P etkinleştirme simgesi](./media/user-guide/netx-events/image127.png)    | **TCP etkinleştirme** (*nx_tcp_enable*) |
| ![T C P boş bağlantı noktası bul simgesi](./media/user-guide/netx-events/image128.png)    | **TCP boş bağlantı noktası bul** (*nx_tcp_free_port_find*) |
| ![T C P bilgi al simgesi](./media/user-guide/netx-events/image129.png)    | **TCP bilgileri al** (*nx_tcp_info_get*) |
| ![T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image130.png)    | **TCP sunucusu yuvasını kabul etme** (*nx_tcp_server_socket_accept*) |
| ![T C P sunucu yuvası dinleme simgesi](./media/user-guide/netx-events/image131.png)    | **TCP sunucu yuvası dinleme** (*nx_tcp_server_socket_listen*) |
| ![T C P sunucu yuvası yeniden dinleme simgesi](./media/user-guide/netx-events/image132.png)    | **TCP sunucu yuvası yeniden dinleme** (*nx_tcp_server_socket_relisten*) |
| ![T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image133.png)    | **TCP sunucusu yuvası kabul etme** (*nx_tcp_server_socket_unaccept*) |
| ![T C P Server yuva geri dinleme simgesi](./media/user-guide/netx-events/image134.png)    | **TCP sunucusu yuva geri dinleme** (*nx_tcp_server_socket_unlisten*) |
| ![T C P yuva baytları kullanılabilir simgesi](./media/user-guide/netx-events/image135.png)    | **Kullanılabilir TCP yuva baytları** (*nx_tcp_socket_bytes_available*) |
| ![T C P yuvası oluşturma simgesi](./media/user-guide/netx-events/image136.png)    | **TCP yuvası oluşturma** (*nx_tcp_socket_create*) |
| ![T C P yuvası silme simgesi](./media/user-guide/netx-events/image137.png)    | **TCP yuvası silme** (*nx_tcp_socket_delete*) |
| ![T C P yuvası bağlantı kesme simgesi](./media/user-guide/netx-events/image138.png)    | **TCP yuvası bağlantısı kesme** (*nx_tcp_socket_disconnect*) |
| ![T C P yuva bilgileri al simgesi](./media/user-guide/netx-events/image139.png)    | **TCP yuva bilgileri Get** (*nx_tcp_socket_info_get*) |
| ![T C P soket, al simgesi](./media/user-guide/netx-events/image140.png)    | **TCP yuvası ve Get** (*nx_tcp_socket_mss_get*) |
| ![T C P soket bir eşi al](./media/user-guide/netx-events/image141.png)    | **TCP soketi eşi eş al** (*nx_tcp_socket_mss_peer_get*) |
| ![T C P soket, küme simgesi](./media/user-guide/netx-events/image142.png)    | **TCP yuvası/küme** (*nx_tcp_socket_mss_set*) |
| ![T C P soket eş bilgi al simgesi](./media/user-guide/netx-events/image143.png)    | **TCP yuvası eş bilgileri al** (*nx_tcp_socket_peer_info_get*) |
| ![T C P yuvası alma simgesi](./media/user-guide/netx-events/image144.png)    | **TCP yuvası alma** (*nx_tcp_socket_receive*) |
| ![T C P yuvası alma bildirim simgesi](./media/user-guide/netx-events/image145.png)    | **TCP yuvası alma bildirimi** (*nx_tcp_socket_receive_notify*) |
| ![T C P yuvası gönderme simgesi](./media/user-guide/netx-events/image146.png)    | **TCP yuvası gönderme** (*nx_tcp_socket_send*) |
| ![T C P yuva durumu bekleme simgesi](./media/user-guide/netx-events/image147.png)    | **TCP yuva durumu bekle** (*nx_tcp_socket_state_wait*) |
| ![T C P yuvası Iletme yapılandırma simgesi](./media/user-guide/netx-events/image148.png)    | **TCP yuvası Iletme yapılandırması** (*nx_tcp_socket_transmit_configure*) |
| ![T C P yuvası pencere güncelleştirme bildirim kümesi simgesi](./media/user-guide/netx-events/image149.png)    | **TCP yuvası pencere güncelleştirme bildirim kümesi** (*nx_tcp_socket_window_update_notify_set*)  |
| ![U D P etkinleştirme simgesi](./media/user-guide/netx-events/image150.png)    | **UDP etkinleştirme** (*nx_udp_enable*) |
| ![U D P boş bağlantı noktası bul simgesi](./media/user-guide/netx-events/image151.png)    | **UDP boş bağlantı noktası bul** (*nx_udp_free_port_find*) |
| ![U D P bilgi al simgesi](./media/user-guide/netx-events/image152.png)    | **UDP bilgileri al** (*nx_udp_info_get*) |
| ![U D P yuvası bağlama simgesi](./media/user-guide/netx-events/image153.png)    | **UDP yuva bağlama** (*nx_udp_socket_bind*) |
| ![U D P yuva baytları kullanılabilir simgesi](./media/user-guide/netx-events/image154.png)    | **Kullanılabilir UDP yuva baytları** (*nx_udp_socket_bytes_available*) |
| ![U D P soket sağlama toplamı devre dışı simgesi](./media/user-guide/netx-events/image155.png)    | **UDP yuva sağlama toplamı devre dışı** (*nx_udp_socket_checksum_disable*) |
| ![U D P yuva sağlama toplamı etkinleştir simgesi](./media/user-guide/netx-events/image156.png)    | **UDP yuva sağlama toplamı etkinleştir** *(nx_udp_socket_checksum_enable)* |
| ![U D P yuvası oluşturma simgesi](./media/user-guide/netx-events/image157.png)    | **UDP yuvası oluşturma** (*nx_udp_socket_create*) |
| ![U D P yuvası silme simgesi](./media/user-guide/netx-events/image158.png)    | **UDP yuvası silme** (*nx_udp_socket_delete*) |
| ![U D yuva bilgileri al simgesi](./media/user-guide/netx-events/image159.png)    | **UDP yuva bilgileri Get** (*nx_udp_socket_info_get*) |
| ![U D P yuva arabirimi kümesi simgesi](./media/user-guide/netx-events/image160.png)    | **UDP yuva arabirimi kümesi** (*nx_udp_socket_interface_set*) |
| ![U D P yuva bağlantı noktası al simgesi](./media/user-guide/netx-events/image161.png)    | **UDP yuva bağlantı noktası al** (*nx_udp_socket_port_get*) |
| ![U D P yuvası alma simgesi](./media/user-guide/netx-events/image162.png)    | **UDP yuvası alma** (*nx_udp_socket_receive*) |
| ![U D P yuvası alma bildirim simgesi](./media/user-guide/netx-events/image163.png)    | **UDP yuvası alma bildirimi** (*nx_udp_socket_receive_notify*) |
| ![U D P yuvası gönderme simgesi](./media/user-guide/netx-events/image164.png)    | **UDP yuvası gönderme** (*nx_udp_socket_send*) |
| ![U D P yuvası çözme simgesi](./media/user-guide/netx-events/image165.png)    | **UDP yuvası bağlantısı kesme** (*nx_udp_socket_unbind*) |
| ![U D P kaynağı ayıklama simgesi](./media/user-guide/netx-events/image166.png)    | **UDP kaynağı ayıklama** (*nx_udp_source_extract*) |

## <a name="event-descriptions"></a>Olay Açıklamaları

Aşağıdaki sayfalarda NetX Izleme olayları açıklanır.

### <a name="internal-arp-request-receive"></a>İç ARP Isteği alma 

#### <a name="internal-arp-request-receive"></a>İç ARP isteği alma

**Simge** ![ İç ARP isteği alma simgesi](./media/user-guide/netx-events/image1.png)

**Açıklama**

Bu olay bir iç NetX ARP istek alma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kaynak IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-arp-request-send"></a>İç ARP Isteği gönderme 

#### <a name="internal-arp-request-send"></a>İç ARP isteği gönderme

**Simge** ![ İç ARP isteği gönderme simgesi](./media/user-guide/netx-events/image2.png)

**Açıklama**

Bu olay bir iç NetX ARP istek gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: hedef IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-arp-response-receive"></a>İç ARP yanıtı alma 

#### <a name="internal-arp-request-receive"></a>İç ARP isteği alma

**Simge** ![ Iç ARP isteği alma simgesi](./media/user-guide/netx-events/image3.png)

**Açıklama**

Bu olay bir iç NetX ARP yanıtı alma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kaynak IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-arp-response-send"></a>İç ARP yanıtı gönderme 

#### <a name="internal-arp-request-send"></a>İç ARP isteği gönderme

**Simge** ![ Iç ARP isteği gönderme simgesi](./media/user-guide/netx-events/image4.png)

**Açıklama**

Bu olay bir iç NetX yanıtı gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: hedef IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-icmp-receive"></a>İç ıCMP alma 

#### <a name="internal-icmp-receive"></a>İç ıCMP alma

**Simge** ![ İç ı C M P alma simgesi](./media/user-guide/netx-events/image5.png)

**Açıklama**

Bu olay bir iç NetX ıCMP alma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kaynak IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: ıCMP üstbilgisinin kelime 0

### <a name="internal-icmp-send"></a>İç ıCMP gönderme 

#### <a name="internal-icmp-send"></a>İç ıCMP gönderme

**Simge** ![ İç ı C M P Gönder simgesi](./media/user-guide/netx-events/image6.png)

**Açıklama**

Bu olay bir iç NetX ıCMP gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: hedef IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: ıCMP üstbilgisinin kelime 0

### <a name="internal-igmp-receive"></a>İç ıGMP alma 

#### <a name="internal-igmp-receive"></a>İç ıGMP alma

**Simge** ![ Dahili ı G M P alma simgesi](./media/user-guide/netx-events/image7.png)

**Açıklama**

Bu olay bir iç NetX ıGMP alma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP Işaretçisi
- Bilgi alanı 2: kaynak IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: ıGMP üstbilgisinin 0. sözcüğü

### <a name="internal-ip-receive"></a>İç IP alma 

#### <a name="internal-ip-receive"></a>İç IP alma

**Simge** ![ İç ı P alma simgesi](./media/user-guide/netx-events/image8.png)

**Açıklama**

Bu olay bir iç NetX IP alma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kaynak IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: paket uzunluğu

### <a name="internal-ip-send"></a>İç IP gönderme

#### <a name="internal-ip-send"></a>İç IP gönderme

**Simge** ![ İç ı P Gönder simgesi](./media/user-guide/netx-events/image9.png)

**Açıklama**

Bu olay bir iç NetX IP gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: hedef IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: paket uzunluğu

### <a name="internal-tcp-data-receive"></a>İç TCP veri alma 

#### <a name="internal-tcp-data-receive"></a>İç TCP veri alma

**Simge** ![ İç T C P veri alma simgesi](./media/user-guide/netx-events/image10.png)

**Açıklama**

Bu olay bir iç NetX TCP veri alma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kaynak IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: alma sıra numarası

### <a name="internal-tcp-data-send"></a>İç TCP veri gönderme 

#### <a name="internal-tcp-data-send"></a>İç TCP veri gönderme

**Simge** ![ İç T C P veri gönderme simgesi](./media/user-guide/netx-events/image11.png)

**Açıklama**

Bu olay bir iç NetX TCP veri gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: aktarım sıra numarası

### <a name="internal-tcp-fin-receive"></a>İç TCP FIN alma 

#### <a name="internal-tcp-fin-receive"></a>İç TCP Fin alma

**Simge** ![ İç T C P F ı N al simgesi](./media/user-guide/netx-events/image12.png)

**Açıklama**

Bu olay bir iç NetX TCP FIN alma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: alma sıra numarası

### <a name="internal-tcp-fin-send"></a>İç TCP FIN gönderme 

#### <a name="internal-tcp-fin-send"></a>İç TCP Fin gönderme

**Simge** ![ İç T C P F ı N Gönder simgesi](./media/user-guide/netx-events/image13.png)

**Açıklama**

Bu olay bir iç NetX TCP FIN gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: aktarım sıra numarası

### <a name="internal-tcp-rst-receive"></a>İç TCP RST alma 

#### <a name="internal-tcp-rst-receive"></a>İç TCP RST alma

**Simge** ![ İç T C P R S T al simgesi](./media/user-guide/netx-events/image14.png)

**Açıklama**

Bu olay bir iç NetX TCP sıfırlama alma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi.
- Bilgi alanı 2: yuva Işaretçisi.
- Bilgi alanı 3: paket Işaretçisi.
- Bilgi alanı 4: alma sıra numarası.

### <a name="internal-tcp-rst-send"></a>İç TCP RST gönderme 

#### <a name="internal-tcp-rst-send"></a>İç TCP RST gönderme

**Simge** ![ İç T C P R S T Gönder simgesi](./media/user-guide/netx-events/image15.png)

**Açıklama**

Bu olay bir iç NetX TCP sıfırlama gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: aktarım sıra numarası

### <a name="internal-tcp-syn-receive"></a>İç TCP SYN alma 

#### <a name="internal-tcp-syn-receive"></a>İç TCP SYN alma

**Simge** ![ İç T C P S e N al simgesi](./media/user-guide/netx-events/image16.png)

**Açıklama**

Bu olay bir iç NetX TCP SYN Receive olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: alma sıra numarası

### <a name="internal-tcp-syn-send"></a>İç TCP SYN Send 

#### <a name="internal-tcp-syn-send"></a>İç TCP SYN Send

**Simge** ![ İç T C P S e N Gönder simgesi](./media/user-guide/netx-events/image17.png)

**Açıklama**

Bu olay bir iç NetX TCP SYN Send olayını temsil eder.

Bilgi alanları 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: paket-bilgi alanı 4 Işaretçisi: aktarım sıra numarası

### <a name="internal-udp-receive"></a>İç UDP alma 

#### <a name="internal-udp-receive"></a>İç UDP alma

**Simge** ![ İç U D P al simgesi](./media/user-guide/netx-events/image18.png)

**Açıklama**

Bu olay bir iç NetX UDP alma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: sözcük 0/UDP üst bilgisi

### <a name="internal-udp-send"></a>İç UDP gönderme 

#### <a name="internal-udp-send"></a>İç UDP gönderme

**Simge** ![ İç U D P Gönder simgesi](./media/user-guide/netx-events/image19.png)

**Açıklama**

Bu olay bir iç NetX UDP gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: sözcük 0/UDP üst bilgisi

### <a name="internal-rarp-receive"></a>İç RARP alma 

#### <a name="internal-rarp-receive"></a>İç RARP alma 

**Simge** ![ Dahili R A R P alma simgesi](./media/user-guide/netx-events/image20.png)

**Açıklama**

Bu olay bir iç NetX RARP alma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: hedef IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: RARP üst bilgisinin kelime 1

### <a name="internal-rarp-send"></a>İç RARP gönderme 

#### <a name="internal-rarp-send"></a>İç RARP gönderme 

**Simge** ![ Dahili R A R P Gönder simgesi](./media/user-guide/netx-events/image21.png)

**Açıklama**

Bu olay bir iç NetX RARP Send olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: hedef IP adresi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: RARP üst bilgisinin kelime 1

### <a name="internal-tcp-retry"></a>İç TCP yeniden denemesi 

#### <a name="internal-tcp-retry"></a>İç TCP yeniden denemesi 

**Simge** ![ İç T C P yeniden deneme simgesi](./media/user-guide/netx-events/image22.png)

**Açıklama**

Bu olay bir iç NetX TCP yeniden deneme olayını temsil eder.

**Bilgi alanları**
- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: paket Işaretçisi
- Bilgi alanı 4: yeniden deneme sayısı

### <a name="internal-tcp-state-change"></a>İç TCP durum değişikliği 

#### <a name="internal-tcp-state-change"></a>İç TCP durum değişikliği 

**Simge** ![ İç T C P durum değiştirme simgesi](./media/user-guide/netx-events/image23.png)

**Açıklama**

Bu olay bir iç NetX TCP yuva durumu değişiklik olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: önceki durum
- Bilgi alanı 4: yeni durum

### <a name="internal-io-driver-packet-send"></a>İç g/ç sürücü paketi gönderme 

#### <a name="internal-io-driver-packet-send"></a>İç g/ç sürücü paketi gönderme

**Simge** ![ İç g/ç sürücü paketi gönderme simgesi](./media/user-guide/netx-events/image24.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücü paketi gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: paket boyutu
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-initialize"></a>İç g/ç sürücüsü başlatma 

#### <a name="internal-io-driver-initialize"></a>İç g/ç sürücüsü başlatma

**Simge** ![ İç g/ç sürücüsü başlatma simgesi](./media/user-guide/netx-events/image25.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü başlatma olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="internal-io-driver-link-enable"></a>İç g/ç sürücü bağlantısı etkinleştir 

#### <a name="internal-io-driver-link-enable"></a>İç g/ç sürücü bağlantısı etkinleştir

**Simge** ![ İç g/ç sürücü bağlantısı etkinleştirme simgesi](./media/user-guide/netx-events/image26.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücü bağlantısı etkinleştir olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi.
- Bilgi alanı 2: kullanılmıyor.
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="internal-io-driver-link-disable"></a>İç g/ç sürücüsü bağlantısı devre dışı 

#### <a name="internal-io-driver-link-disable"></a>İç g/ç sürücüsü bağlantısı devre dışı

**Simge** ![ İç g/ç sürücü bağlantısı devre dışı simgesi](./media/user-guide/netx-events/image27.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücü bağlantısını devre dışı olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-packet-broadcast"></a>İç g/ç sürücü paketi yayını 

#### <a name="internal-io-driver-packet-broadcast"></a>İç g/ç sürücü paketi yayını

**Simge** ![ İç g/ç sürücü paketi yayını simgesi](./media/user-guide/netx-events/image28.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücü paketi yayın olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: paket boyutu
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-arp-send"></a>İç g/ç sürücüsü ARP gönderme 

#### <a name="internal-io-driver-arp-send"></a>İç g/ç sürücüsü ARP gönderme

**Simge** ![ İç g/ç sürücüsü ARP gönderme simgesi](./media/user-guide/netx-events/image29.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü ARP gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: paket boyutu
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-arp-response-send"></a>İç g/ç sürücüsü ARP yanıtı gönderme 

#### <a name="internal-io-driver-arp-response-send"></a>İç g/ç sürücüsü ARP yanıtı gönderme

**Simge** ![ İç g/ç sürücüsü ARP yanıtı gönderme simgesi](./media/user-guide/netx-events/image30.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü ARP yanıtı gönderme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: paket boyutu
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-rarp-send"></a>İç g/ç sürücüsü RARP gönderme 

#### <a name="internal-io-driver-rarp-send"></a>İç g/ç sürücüsü RARP gönderme

**Simge** ![ İç g/ç sürücüsü RARP Gönder simgesi](./media/user-guide/netx-events/image31.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü RARP Send olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: paket boyutu
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-multicast-join"></a>İç g/ç sürücüsü çok noktaya yayın katılımı 

#### <a name="internal-io-driver-multicast-join"></a>İç g/ç sürücüsü çok noktaya yayın katılımı

**Simge** ![ İç g/ç sürücüsü çok noktaya yayın Birleştir simgesi](./media/user-guide/netx-events/image32.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü çok noktaya yayın JOIN olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-multicast-leave"></a>İç g/ç sürücüsü çok noktaya yayını bırakma 

#### <a name="internal-io-driver-multicast-leave"></a>İç g/ç sürücüsü çok noktaya yayını bırakma

**Simge** ![ İç g/ç sürücüsü çok noktaya yayın çıkış simgesi](./media/user-guide/netx-events/image33.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü çok noktaya yayın çıkış olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-get-status"></a>İç g/ç sürücüsü Get durumu 

#### <a name="internal-io-driver-get-status"></a>İç g/ç sürücüsü Get durumu

**Simge** ![ İç g/ç sürücüsü durum Al simgesi](./media/user-guide/netx-events/image34.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü al durum olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-get-speed"></a>İç g/ç sürücüsü edinme hızı 

#### <a name="internal-io-driver-get-speed"></a>İç g/ç sürücüsü edinme hızı

**Simge** ![ İç g/ç sürücüsü al hız simgesi](./media/user-guide/netx-events/image35.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü al hız olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-get-duplex-type"></a>İç g/ç sürücüsü çift yönlü türü al 

#### <a name="internal-io-driver-get-duplex-type"></a>İç g/ç sürücüsü çift yönlü türü al

**Simge** ![ İç g/ç sürücüsü çift yönlü tür simgesi al](./media/user-guide/netx-events/image36.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü al çift yönlü türü olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-get-error-count"></a>İç g/ç sürücüsü hata sayısını Al

#### <a name="internal-io-driver-get-error-count"></a>İç g/ç sürücüsü hata sayısını Al

**Simge** ![ İç g/ç sürücüsü hata sayısını Al simgesi](./media/user-guide/netx-events/image37.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü Get hata sayısı olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-get-rx-count"></a>İç g/ç sürücüsü RX sayısı al 

#### <a name="internal-io-driver-get-rx-count"></a>İç g/ç sürücüsü RX sayısı al

**Simge** ![ İç g/ç sürücüsü RX sayısı simgesi al](./media/user-guide/netx-events/image38.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsünü, RX sayısı olayını Al ' ı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-get-tx-count"></a>İç g/ç sürücüsü TX sayısı al 

#### <a name="internal-io-driver-get-tx-count"></a>İç g/ç sürücüsü TX sayısı al

**Simge** ![ İç g/ç sürücüsü Get T X sayı simgesi](./media/user-guide/netx-events/image39.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü Get TX Count olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-get-allocation-errors"></a>İç g/ç sürücüsü ayırma hatalarını al 

#### <a name="internal-io-driver-get-allocation-errors"></a>İç g/ç sürücüsü ayırma hatalarını al

**Simge** ![ İç g/ç sürücüsü ayırma hatalarını al simgesi](./media/user-guide/netx-events/image40.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü al ayırma hataları olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-un-initialize"></a>İç g/ç sürücüsü başlatması geri al 

#### <a name="internal-io-driver-un-initialize"></a>İç g/ç sürücüsü başlatması geri al 

**Simge** ![ İç g/ç sürücüsü başlatması kaldır simgesi](./media/user-guide/netx-events/image41.png)

**Açıklama**

Bu olay bir iç NetX g/ç sürücüsü başlatma kaldırma olayını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="internal-io-driver-deferred-processing"></a>İç g/ç sürücüsü ertelenmiş Işleme 

#### <a name="internal-io-driver-deferred-processing"></a>İç g/ç sürücüsü ertelenmiş işleme 

**Simge** ![ İç g/ç sürücüsü ertelenmiş işleme simgesi](./media/user-guide/netx-events/image42.png)

**Açıklama**

Bu olay, bir iç NetX g/ç sürücüsü ertelenmiş işleme olayını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: paket uzunluğu
- Bilgi alanı 4: kullanılmıyor

### <a name="arp-dynamic-entries-invalidate"></a>ARP dinamik girdileri geçersiz kılar 

#### <a name="nx_arp_dynamic_entries_invalidate"></a>nx_arp_dynamic_entries_invalidate

**Simge** ![ R P dinamik girdileri geçersiz kılar simgesi](./media/user-guide/netx-events/image43.png)

**Açıklama**

Bu olay, tüm dinamik ARP entires nx_arp_dynamic_entries_invalidate aracılığıyla geçersiz kılma gösterir.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: geçersiz kılınan girişler
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="arp-dynamic-entry-set"></a>ARP dinamik giriş kümesi 

#### <a name="nx_arp_dynamic_entry_set"></a>nx_arp_dynamic_entry_set

**Simge** ![ R P dinamik giriş kümesi simgesi](./media/user-guide/netx-events/image44.png)

**Açıklama**

Bu olay, nx_arp_dynamic_entry_set aracılığıyla dinamik bir ARP girişi ayarlamayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP adresi
- Bilgi alanı 3: fiziksel adres (MSW)
- Bilgi alanı 4: fiziksel adres (LSW)

### <a name="arp-enable"></a>ARP etkinleştir 

#### <a name="nx_arp_enable"></a>nx_arp_enable

**Simge** ![ R P etkinleştirme simgesi](./media/user-guide/netx-events/image45.png)

**Açıklama**

Bu olay nx_arp_enable aracılığıyla ARP 'i etkinleştirmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: ARP önbelleği bellek işaretçisi
- Bilgi alanı 3: ARP önbelleği bellek boyutu
- Bilgi alanı 4: kullanılmıyor

### <a name="arp-gratuitous-send"></a>ARP gereksiz Yolus gönder 

#### <a name="nx_arp_gratuitous_send"></a>nx_arp_gratuitous_send

**Simge** ![ R P gereksiz yolus Gönder simgesi](./media/user-guide/netx-events/image46.png)

**Açıklama**

Bu olay, nx_arp_gratuitous_send aracılığıyla gereksiz bir ARP gönderimi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="arp-hardware-address-find"></a>ARP donanım adresi bulma 

#### <a name="nx_arp_hardware_address_find"></a>nx_arp_hardware_address_find

**Simge** ![ R P donanım adresi bul simgesi](./media/user-guide/netx-events/image47.png)

**Açıklama**

Bu olay nx_arp_hardware_address_find aracılığıyla bir fiziksel adres bulmayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP adresi
- Bilgi alanı 3: fiziksel adres (MSW)
- Bilgi alanı 4: fiziksel adres (LSW)

### <a name="arp-information-get"></a>ARP bilgilerini al 

#### <a name="nx_arp_info_get"></a>nx_arp_info_get

**Simge** ![ R P veya daha fazla alma simgesi al](./media/user-guide/netx-events/image48.png)

**Açıklama**

Bu olay nx_arp_info_get aracılığıyla bilgi almayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: ARPs gönderilen
- Bilgi alanı 3: ARP yanıtları
- Bilgi alanı 4: ARPs alındı

### <a name="arp-ip-address-find"></a>ARP IP adresi bulma 

#### <a name="nx_arp_ip_address_find"></a>nx_arp_ip_address_find

**Simge** ![ R P I P adresi bul simgesi](./media/user-guide/netx-events/image49.png)

**Açıklama**

Bu olay, nx_arp_ip_address_find aracılığıyla sağlanan fiziksel adresle ilişkili bir IP adresi bulmayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP adresi
- Bilgi alanı 3: fiziksel adres (MSW)
- Bilgi alanı 4: fiziksel adres (LSW)

### <a name="arp-static-entry-create"></a>ARP statik girdisi oluşturma 

#### <a name="nx_arp_static_entry_create"></a>nx_arp_static_entry_create

**Simge** ![ R P statik giriş oluştur simgesi](./media/user-guide/netx-events/image50.png)

**Açıklama**

Bu olay nx_arp_static_entry_create aracılığıyla statik bir ARP girişi oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP adresi
- Bilgi alanı 3: fiziksel adres (MSW)
- Bilgi alanı 4: fiziksel adres (LSW)

### <a name="arp-static-entries-delete"></a>ARP statik girişleri silme 

#### <a name="nx_arp_static_entries_delete"></a>nx_arp_static_entries_delete

**Simge** ![ R P statik girdileri Sil simgesi](./media/user-guide/netx-events/image51.png)

**Açıklama**

Bu olay, tüm ARP statik girişlerinin nx_arp_static_entries_delete aracılığıyla silinmesini temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: Silinen girdiler
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="arp-static-entry-delete"></a>ARP statik giriş silme 

### <a name="nx_arp_static_entry_delete"></a>nx_arp_static_entry_delete

**Simge** ![ R P statik giriş silme simgesi](./media/user-guide/netx-events/image52.png)

**Açıklama**

Bu olay, nx_arp_static_entry_delete aracılığıyla statik bir ARP girişini silmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP adresi
- Bilgi alanı 3: fiziksel adres (MSW)
- Bilgi alanı 4: fiziksel adres (LSW)

### <a name="duo-cache-entry-delete"></a>Duo önbellek girdisini silme 

#### <a name="nxd_und_cache_entry_delete"></a>nxd_und_cache_entry_delete

**Simge** ![ Duo önbellek girişi silme simgesi](./media/user-guide/netx-events/image53.png)

**Açıklama**

Bu olay, komşu önbellek tablosundaki nx_udp_socket_create aracılığıyla bir girişi silmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IPv6 bağlantısı yerel adresinin silinecek dördüncü (en az önemli) kelime
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-cache-entry-set"></a>Duo önbellek giriş kümesi 

#### <a name="nxd_nd_cache_entry_set"></a>nxd_nd_cache_entry_set

**Simge** ![ Duo önbellek girdisi kümesi simgesi](./media/user-guide/netx-events/image54.png)

**Açıklama**

Bu olay, bir önbellek girişi oluşturmayı ve nxd_nd_cache_entry_set aracılığıyla komşu önbelleği tablosuna eklemeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: eklenecek IPv6 adresinin dördüncü (en az önemli) sözcüğü
- Bilgi alanı 2: fiziksel adres MSB
- Bilgi alanı 3: fiziksel adres LSB
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-cache-invalidate"></a>Duo önbelleği geçersiz kıl 

#### <a name="nxd_nd_cache_invalidate"></a>nxd_nd_cache_invalidate

**Simge** ![ Duo önbelleği geçersiz kıl simgesi](./media/user-guide/netx-events/image55.png)

**Açıklama**

Bu olay, tüm komşu önbellek tablosunun nxd_nd_cache_invalidate aracılığıyla geçersiz kılmalarını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-cache-ip-address-find"></a>Duo önbelleği IP adresi bulma 

#### <a name="nxd_nd_cache_ip_address_find"></a>nxd_nd_cache_ip_address_find

**Simge** ![ Duo önbelleği ı P adresi bul simgesi](./media/user-guide/netx-events/image56.png)

**Açıklama**

Bu olay, nxd_nd_cache_ip_address_find aracılığıyla önbellek tablosundan sağlanan fiziksel adresle eşleşen bir IP adresi almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IPv6 adresinin dördüncü (en az önemli) sözcüğü
- Bilgi alanı 3: fiziksel adres MSB
- Bilgi alanı 4: fiziksel adres LSB

### <a name="duo-icmp-enable"></a>Duo ıCMP etkinleştirme 

#### <a name="nxd_icmp_enable"></a>nxd_icmp_enable

**Simge** ![ Duo ı C M P etkinleştir simgesi](./media/user-guide/netx-events/image57.png)

**Açıklama**

Bu olay, nxd_icmp_enable aracılığıyla belirtilen IP örneğinde etkinleştirilen Icmpv4 ve ICMPv6 hizmetlerini temsil eder.

**Bilgi alanları**
- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-icmp-ping"></a>Duo ıCMP ping 

#### <a name="nxd_icmp_ping"></a>nxd_icmp_ping

**Simge** ![ Duo ı C M P ping simgesi](./media/user-guide/netx-events/image58.png)

**Açıklama**

Bu olay, nxd_icmp_ping aracılığıyla bir IPv6 konağına ping (yankı isteği) göndermeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IPv6 adresi
- Bilgi alanı 3: yankı verileri Işaretçisi
- Bilgi alanı 4: yankı verilerinin boyutu

### <a name="duo-ip-max-payload-size-find"></a>Duo IP en fazla yük boyutu bul 

#### <a name="nxd_ip_max_payload_size"></a>nxd_ip_max_payload_size

**Simge** ![ Duo ı P maks. yük boyutu bul simgesi](./media/user-guide/netx-events/image59.png)

**Açıklama**

Bu olay, belirtilen paketin parçalanma gerekmeden taşıyabilmesi için gereken en fazla yükü hesaplar.

**Bilgi alanları**

- Bilgi alanı 1: yuva işaretçisi
- Bilgi alanı 2: eş IP adresi
- Bilgi alanı 3: eş bağlantı noktası bilgi alanı 4: kullanılmıyor

### <a name="duo-ip-raw-packet-send"></a>Duo IP ham paket gönder 

#### <a name="nxd_ip_max_packet_send"></a>nxd_ip_max_packet_send

**Simge** ![ Duo ı P ham paket Gönder simgesi](./media/user-guide/netx-events/image60.png)

**Açıklama**

Bu olay, nxd_ip_raw_packet_send aracılığıyla sağlanan IP hedefi adresüne belirtilen ağ arabirimini bir ham IP paketi göndermeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: gönderilmek üzere paket Işaretçisi
- Bilgi alanı 3: hedef adres Işaretçisi
- Bilgi alanı 4: paket Protokolü

### <a name="duo-ipv6-default-router-add"></a>Duo IPv6 varsayılan yönlendirici eklentisi 

#### <a name="nxd_ipv6_default_router_add"></a>nxd_ipv6_default_router_add

**Simge** ![ Duo ı P v 6 varsayılan yönlendirici Ekle simgesi](./media/user-guide/netx-events/image61.png)

**Açıklama**

Bu olay, IP örneğinin IPv6 yönlendirme tablosuna nxd_ipv6_default_router_add aracılığıyla varsayılan bir yönlendirici eklemeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi.
- Bilgi alanı 2: hedef ağ adresi.
- Bilgi alanı 3: yaşam süresi bilgileri.
- Bilgi alanı 4: kullanılmıyor.

### <a name="duo-ipv6-default-router-delete"></a>Duo IPv6 varsayılan yönlendirici silme 

#### <a name="nxd_ipv6_default_router_delete"></a>nxd_ipv6_default_router_delete

**Simge** ![ Duo ı P v 6 varsayılan yönlendirici silme simgesi](./media/user-guide/netx-events/image62.png)

**Açıklama**

Bu olay, IP örneğinin IPv6 yönlendirme tablosundan nxd_ipv6_default_router_delete aracılığıyla varsayılan bir yönlendiriciyi kaldırmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi.
- Bilgi alanı 2: varsayılan yönlendirici IPv6 adresinin dördüncü sözcük (en az önemli).
- Bilgi alanı 3: kullanılmıyor.
- Bilgi alanı 4: kullanılmıyor.

### <a name="duo-ipv6-enable"></a>Duo IPv6 etkin 

#### <a name="nxd_ipv6_enable"></a>nxd_ipv6_enable

**Simge** ![ Duo ı P v 6 etkinleştirme simgesi](./media/user-guide/netx-events/image63.png)

**Açıklama**

Bu olay, sağlanan IP örneğindeki nxd_ipv6_enable aracılığıyla IPv6 hizmetlerinin etkinleştirilmesini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-ipv6-global-address-get"></a>Duo IPv6 genel adresi al 

#### <a name="nxd_ipv6_global_address_get"></a>nxd_ipv6_global_address_get

**Simge** ![ Duo ı P v 6 genel adres al simgesi](./media/user-guide/netx-events/image64.png)

**Açıklama**

Bu olay, IP örneği arabirim tablosundaki Dizin 1 ' de bulunan IP örneğindeki genel (birincil) IP adresini nxd_ipv6_global_address_get aracılığıyla almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi.
- Bilgi alanı 2: genel adresin dördüncü sözcüğü (en az önemli)
- Bilgi alanı 3: IPv6 adresi önek uzunluğu.
- Bilgi alanı 4: IP arabirim tablosuna dizin (1).

### <a name="duo-ipv6-global-address-set"></a>Duo IPv6 genel adres kümesi 

#### <a name="nxd_ipv6_global_address_set"></a>nxd_ipv6_global_address_set

**Simge** ![ Duo ı P v 6 genel adres kümesi simgesi](./media/user-guide/netx-events/image65.png)

**Açıklama**

Bu olay, IP örneği arabirim tablosundaki Dizin 1 ' de bulunan IP örneğindeki genel (birincil) IP adresinin nxd_ipv6_global_address_set aracılığıyla ayarlanmasını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: genel adresin dördüncü sözcüğü (en az önemli)
- Bilgi alanı 3: IPv6 adresi önek uzunluğu
- Bilgi alanı 4: IP arabirim tablosuna dizin (1)

### <a name="duo-ipv6-initiate-dad-process"></a>Duo IPv6, babacığım Işlemini Başlat 

#### <a name="nxd_ipv6_initiate_dad_process"></a>nxd_ipv6_initiate_dad_process

**Simge** ![ Duo ı P v 6 babacığım işlem simgesi](./media/user-guide/netx-events/image66.png)

**Açıklama**

Bu olay, IP örneğine nxd_ipv6_initiate_dad_process aracılığıyla bir bağlantı yerel veya IP arabirimi adresi atandığında yinelenen adres algılama (BABACıĞıM) işleminin başlangıcını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-ipv6-interface-address-get"></a>Duo IPv6 arabirim adresi al 

#### <a name="nxd_ipv6_interface_address_get"></a>nxd_ipv6_interface_address_get

**Simge** ![ Duo ı P v 6 arabirim adresi al simgesi](./media/user-guide/netx-events/image67.png)

**Açıklama**

Bu olay, belirtilen dizinde IP adresi ve ön ek nxd_ipv6_interface_address_get aracılığıyla IP örneği arabirim adresi tablosuna alınması temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: döndürülecek IPv6 adresinin dördüncü sözcük (en az önemli)
- Bilgi alanı 4: arabirimin IP örneği arabirim tablosuna dizini

### <a name="duo-ipv6-interface-address-set"></a>Duo IPv6 arabirimi adres kümesi 

### <a name="nxd_ipv6_interface_address_set"></a>nxd_ipv6_interface_address_set

**Simge** ![ Duo ı P v 6 arabirim adresiss et simgesi](./media/user-guide/netx-events/image68.png)

**Açıklama**

Bu olay, belirtilen dizinde IP adresi ve önekinin IP örneği arabirim adresi tablosuna ayarlanmasını temsil eder. Nxd_ipv6_interface_address_set aracılığıyla sıfır dizininde (bağlantı yerel adres) izin verilmez.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: döndürülecek IPv6 adresinin dördüncü sözcük (en az önemli)
- Bilgi alanı 3: ön ek uzunluğu
- Bilgi alanı 4: arabirimin IP örneği arabirim tablosuna dizini

### <a name="duo-ipv6-link-local-address-get"></a>Duo IPv6 bağlantısı yerel adres Get 

#### <a name="nxd_ipv6_linklocal_address_get"></a>nxd_ipv6_linklocal_address_get

**Simge** ![ Duo ı P v 6 bağlantısı yerel adres al simgesi](./media/user-guide/netx-events/image69.png)

**Açıklama**

Bu olay, nxd_ipv6_linklocal_address_get aracılığıyla belirtilen IP örneğinin bağlantı yerel adresini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP V6 bağlantısı yerel adresinin dördüncü sözcük (en az önemli)
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-ipv6-link-local-address-set"></a>Duo IPv6 bağlantısı yerel adres kümesi 

#### <a name="nxd_ipv6_linklocal_address_set"></a>nxd_ipv6_linklocal_address_set

**Simge** ![ Duo ı P v 6 bağlantısı yerel adres kümesi simgesi](./media/user-guide/netx-events/image70.png)

**Açıklama**

Bu olay, IP örneğinin bağlantı yerel adresini nxd_ipv6_linklocal_address_set aracılığıyla ayarlamayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IPv6 bağlantısı yerel adresinin dördüncü (en az önemli) sözcüğü
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-ipv6-raw-packet-send"></a>Duo IPv6 ham paket gönder 

#### <a name="nxd_ipv6_raw_packet_send"></a>nxd_ipv6_raw_packet_send

**Simge** ![ Duo ı P v 6 ham paket Gönder simgesi](./media/user-guide/netx-events/image71.png)

**Açıklama**

Bu olay, nxd_ip_raw_packet_send aracılığıyla bulunan hedefe yönelik birincil IP arabirimi aracılığıyla bir ham IP paketinin gönderilmesini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: gönderilmek üzere paket Işaretçisi
- Bilgi alanı 3: hedef IP adresi
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-tcp-socket-peer-info-get"></a>Duo TCP yuvası eş bilgileri Get 

#### <a name="nxd_tcp_socket_peer_info_get"></a>nxd_tcp_socket_peer_info_get

**Simge** ![ Duo T C P soket eş bilgileri al simgesi](./media/user-guide/netx-events/image72.png)

**Açıklama**

Bu olay, belirtilen yuvada alınan bir TCP paketindeki gönderen verilerini ayıklar. Gönderenin IP adresini ve bağlantı noktasını döndürür.

**Bilgi alanları**

- Bilgi alanı 1: yuva işaretçisi
- Bilgi alanı 2: eş IP adresi
- Bilgi alanı 3: eş bağlantı noktası
- Bilgi alanı 4: IP adresinin Kiralama önemli 32-bit

### <a name="duo-tcp-socket-set-interface"></a>Duo TCP yuva kümesi arabirimi 

#### <a name="nxd_tcp_socket_set_interface"></a>nxd_tcp_socket_set_interface

**Simge** ![ Duo T C P yuva kümesi arabirim simgesi](./media/user-guide/netx-events/image73.png)

**Açıklama**

Bu olay, bir istemci, belirtilen sunucu IP adresi üzerinde nxd_tcp_client_socket_connect aracılığıyla bir TCP sunucusuna bağlandıktan sonra giden yuva arabirimini ayarlamayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: TCP yuvası Işaretçisi
- Bilgi alanı 2: arabirim KIMLIĞI
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-udp-socket-send"></a>Duo UDP yuvası gönderme 

#### <a name="nxd_udp_socket_send"></a>nxd_udp_socket_send

**Simge** ![ Duo U D P yuvası gönderme simgesi](./media/user-guide/netx-events/image74.png)

**Açıklama**

Bu olay, giriş IP adresi ve bağlantı noktası ile nxd_udp_socket_send aracılığıyla belirtilen yuva aracılığıyla bir UDP paketi göndermeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: Işaretçi UDP yuvası
- Bilgi alanı 2: UDP paketi Işaretçisi
- Bilgi alanı 3: paket uzunluğu
- Bilgi alanı 4: kullanılmıyor


### <a name="duo-udp-socket-set-interface"></a>Duo UDP yuva kümesi arabirimi 

#### <a name="nxd_udp_socket_set_interface"></a>nxd_udp_socket_set_interface

**Simge** ![ Duo U D P yuva kümesi arabirim simgesi](./media/user-guide/netx-events/image75.png)

**Açıklama**

Bu olay, belirtilen UDP yuvası giden arabirimini nxd_udp_socket_set_interface aracılığıyla giriş arabirimi KIMLIĞINE karşılık gelen arabirime ayarlamayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: UDP yuvası Işaretçisi
- Bilgi alanı 2: arabirim KIMLIĞI
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="duo-udp-source-extract"></a>Duo UDP kaynağı ayıklama 

#### <a name="nxd_udp_socket_extract"></a>nxd_udp_socket_extract

**Simge** ![ Duo U D P kaynağı ayıklama simgesi](./media/user-guide/netx-events/image76.png)

**Açıklama**

Bu olay, alınan bir paketin IP adresini ve kaynak bağlantı noktasını ayıklamayı (IPv4 veya IPv6) temsil eder. IPv6 ise, IP adresinin dördüncü sözcüğü (en az önemli) nxd_udp_source_extract aracılığıyla döndürülür.

**Bilgi alanları**

- Bilgi alanı 1: paket Işaretçisi
- Bilgi alanı 2: IP sürümü
- Bilgi alanı 3: kaynak IP adresi (IPv4 veya IPv6)
- Bilgi alanı 4: kaynak bağlantı noktası

### <a name="icmp-enable"></a>ICMP etkinleştirme 

#### <a name="nx_icmp_enable"></a>nx_icmp_enable

**Simge** ![ I C M P etkinleştir simgesi](./media/user-guide/netx-events/image77.png)

**Açıklama**

Bu olay nx_icmp_enable aracılığıyla ıCMP etkinleştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğinin Işaretçisi;
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="icmp-information-get"></a>ICMP bilgileri Get 

#### <a name="nx_icmp_info_get"></a>nx_icmp_info_get

**Simge** ![ I C M P bilgi al simgesi](./media/user-guide/netx-events/image78.png)

**Açıklama**

Bu olay nx_icmp_info_get aracılığıyla bilgi almayı temsil eder.

**Bilgi alanları**
- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: gönderilen pingler
- Bilgi alanı 3: ping yanıtları
- Bilgi alanı 4: alınan pingler

### <a name="icmp-ping"></a>ICMP ping 

#### <a name="nx_icmp_ping"></a>nx_icmp_ping

**Simge** ![ I C M P ping simgesi](./media/user-guide/netx-events/image79.png)

**Açıklama**

Bu olay, nx_icmp_ping aracılığıyla bir hedef IP adresinin ping komutunu temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP adresi
- Bilgi alanı 3: veri Işaretçisi
- Bilgi alanı 4: verilerin boyutu

### <a name="igmp-enable"></a>IGMP etkinleştirme 

#### <a name="nx_icmp_enable"></a>nx_icmp_enable

**Simge** ![ G G M P etkinleştirme simgesi](./media/user-guide/netx-events/image80.png)

**Açıklama**

Bu olay nx_igmp_enable aracılığıyla ıGMP etkinleştirmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="igmp-information-get"></a>IGMP bilgi edinme 

#### <a name="nx_icmp_info_get"></a>nx_icmp_info_get

**Simge** ![ G-M P bilgi al simgesi](./media/user-guide/netx-events/image81.png)

**Açıklama**

Bu olay nx_igmp_info_get aracılığıyla bilgi almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: gönderilen raporlar
- Bilgi alanı 3: alınan sorgular
- Bilgi alanı 4: eklenen gruplar

### <a name="igmp-loopback-disable"></a>IGMP geri döngü devre dışı 

#### <a name="nx_igmp_loopback_disable"></a>nx_igmp_loopback_disable

**Simge** ![ I G M P geri döngü devre dışı simgesi](./media/user-guide/netx-events/image82.png)

**Açıklama**

Bu olay nx_igmp_loopback_disable aracılığıyla ıGMP geri döngüsünü devre dışı bırakmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="igmp-loopback-enable"></a>IGMP geri döngü etkinleştirme 

#### <a name="nx_igmp_loopback_enable"></a>nx_igmp_loopback_enable

**Simge** ![ I G M P geri döngü etkinleştirme simgesi](./media/user-guide/netx-events/image83.png)

**Açıklama**

Bu olay nx_igmp_loopback_enable aracılığıyla ıGMP geri döngüsünü etkinleştirmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="igmp-multicast-join"></a>IGMP çok noktaya yayın katılımı 

#### <a name="nx_igmp_multicast_join"></a>nx_igmp_multicast_join

**Simge** ![ G & urum çok noktaya yayın Birleştir simgesi](./media/user-guide/netx-events/image84.png)

**Açıklama**

Bu olay, çok noktaya yayın grubunun nx_igmp_multicast_join aracılığıyla katılmasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: Grup IP adresi
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="igmp-multicast-leave"></a>IGMP çok noktaya yayın bırakma 

#### <a name="nx_igmp_multicast_leave"></a>nx_igmp_multicast_leave

**Simge** ![ G & urum çok noktaya yayın çıkış simgesi](./media/user-guide/netx-events/image85.png)

**Açıklama**

Bu olay, çok noktaya yayın grubunu nx_igmp_multicast_leave aracılığıyla bırakarak temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: Grup IP adresi
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-address-change-notify"></a>IP adresi değişikliği bildirimi 

#### <a name="nx_ip_address_change_notify"></a>nx_ip_address_change_notify

**Simge** ![ I P adres değişikliği bildirim simgesi](./media/user-guide/netx-events/image86.png)

**Açıklama**

Bu olay nx_ip_address_change_notify aracılığıyla IP değişiklik bildirimine kaydolma 'yi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: geri çağırma işlev işaretçisi
- Bilgi alanı 3: ek bilgi işaretçisi
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-address-get"></a>IP adresi al 

#### <a name="nx_ip_address_get"></a>nx_ip_address_get

**Simge** ![ I P adresi al simgesi](./media/user-guide/netx-events/image87.png)

**Açıklama**

Bu olay, IP adresinin nx_ip_address_get aracılığıyla alınmasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP adresi
- Bilgi alanı 3: ağ maskesi
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-address-set"></a>IP adresi kümesi 

#### <a name="nx_ip_address_set"></a>nx_ip_address_set

**Simge** ![ I P adres kümesi simgesi](./media/user-guide/netx-events/image88.png)

**Açıklama**

Bu olay, IP adresini nx_ip_address_set aracılığıyla ayarlamayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP adresi
- Bilgi alanı 3: ağ maskesi
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-create"></a>IP oluşturma 

#### <a name="nx_ip_create"></a>nx_ip_create

**Simge** ![ I P Oluştur simgesi](./media/user-guide/netx-events/image89.png)

**Açıklama**

Bu olay nx_ip_create aracılığıyla bir IP örneği oluşturmayı temsil eder.

**Bilgi alanları** 
- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: IP adresi
- Bilgi alanı 3: ağ maskesi
- Bilgi alanı 4: varsayılan paket havuzu işaretçisi

### <a name="ip-delete"></a>IP silme 

#### <a name="nx_ip_delete"></a>nx_ip_delete

**Simge** ![ I P Sil simgesi](./media/user-guide/netx-events/image90.png)

**Açıklama**

Bu olay nx_ip_delete aracılığıyla bir IP örneğini silmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-driver-direct-command"></a>IP sürücüsü doğrudan komutu 

#### <a name="nx_ip_driver_direct_command"></a>nx_ip_driver_direct_command

**Simge** ![ I P sürücüsü doğrudan komut simgesi](./media/user-guide/netx-events/image91.png)

**Açıklama**

Bu olay, nx_ip_driver_direct_command aracılığıyla doğrudan g/ç sürücüsü komutunu temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: sürücü komutu
- Bilgi alanı 3: dönüş değeri
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-forwarding-disable"></a>IP Iletme devre dışı 

#### <a name="nx_ip_forwarding_disable"></a>nx_ip_forwarding_disable

**Simge** ![ I P iletme devre dışı simgesi](./media/user-guide/netx-events/image92.png)

**Açıklama**

Bu olay nx_ip_forwarding_disable aracılığıyla IP iletmeyi devre dışı bırakmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-forwarding-enable"></a>IP Iletme etkinleştirme 

#### <a name="nx_ip_forwarding_enable"></a>nx_ip_forwarding_enable

**Simge** ![ I P iletme etkinleştirme simgesi](./media/user-guide/netx-events/image93.png)

**Açıklama**

Bu olay nx_ip_forwarding_enable aracılığıyla IP iletmeyi etkinleştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-fragment-disable"></a>IP parçası devre dışı 

#### <a name="nx_ip_fragment_disable"></a>nx_ip_fragment_disable

**Simge** ![ I P parçanız devre dışı simgesi](./media/user-guide/netx-events/image94.png)

**Açıklama**

Bu olay, IP fragmenting nx_ip_fragment_disable aracılığıyla devre dışı bırakmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-fragment-enable"></a>IP parçası etkinleştirme 

#### <a name="nx_ip_fragment_enable"></a>nx_ip_fragment_enable

**Simge** ![ I P parçası etkinleştirme simgesi](./media/user-guide/netx-events/image95.png)

**Açıklama**

Bu olay, IP fragmenting nx_ip_fragment_enable aracılığıyla etkinleştirilmesini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-gateway-address-set"></a>IP ağ geçidi adres kümesi 

#### <a name="nx_ip_gateway_address_set"></a>nx_ip_gateway_address_set

**Simge** ![ I P ağ geçidi adres kümesi simgesi](./media/user-guide/netx-events/image96.png)

**Açıklama**

Bu olay, ağ geçidi IP adresini nx_ip_gateway_address_set aracılığıyla ayarlamayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: ağ geçidi IP adresi
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-information-get"></a>IP bilgileri al 

#### <a name="nx_ip_info_get"></a>nx_ip_info_get

**Simge** ![ I P bilgileri al simgesi](./media/user-guide/netx-events/image97.png)

**Açıklama** Bu olay nx_ip_info_get aracılığıyla IP bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: gönderilen IP baytları
- Bilgi alanı 3: alınan IP baytları
- Bilgi alanı 4: IP paketleri bırakıldı

### <a name="ip-interface-attach"></a>IP arabirimi Iliştirme 

#### <a name="nx_interface_attach"></a>nx_interface_attach

**Simge** ![ I P iteryüz iliştirme simgesi](./media/user-guide/netx-events/image98.png)

**Açıklama**

Bu olay, IP örneğine eklenen bir ikincil ağ arabirimini nx_ip_interface_attach aracılığıyla temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: Arabirim IP adresi
- Bilgi alanı 3: IP arabirim tablosuna Dizin
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-interface-info-get"></a>IP arabirimi bilgilerini al 

#### <a name="nx_ip_interface_info_get"></a>nx_ip_interface_info_get

**Simge** ![ IP arabirimi bilgileri al simgesi](./media/user-guide/netx-events/image99.png)

**Açıklama**

Bu olay, nx_ip_interface_info_get aracılığıyla belirtilen ağ arabiriminden alınan bilgileri temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: Arabirim IP adresi
- Bilgi alanı 3: arabirim MAC adresi MSB
- Bilgi alanı 4: arabirim MAC adresi LSB

### <a name="ip-raw-packet-disable"></a>IP ham paket devre dışı 

#### <a name="nx_ip_raw_packet_disable"></a>nx_ip_raw_packet_disable

**Simge** ![ I P ham paket devre dışı simgesi](./media/user-guide/netx-events/image100.png)

**Açıklama**

Bu olay, ham IP paket iletişimini nx_ip_raw_packet_disable aracılığıyla devre dışı bırakmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-raw-packet-enable"></a>IP ham paket etkinleştir 

#### <a name="nx_ip_raw_packet_enable"></a>nx_ip_raw_packet_enable

**Simge** ![ I P RAW paketi etkinleştirme simgesi](./media/user-guide/netx-events/image101.png)

**Açıklama**

Bu olay, ham IP paket iletişimini nx_ip_raw_packet_enable aracılığıyla etkinleştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-raw-packet-receive"></a>IP ham paket alma 

#### <a name="nx_ip_raw_packet_receive"></a>nx_ip_raw_packet_receive

**Simge** ![ I P ham paket alma simgesi](./media/user-guide/netx-events/image102.png)

**Açıklama**

Bu olay nx_ip_raw_packet_receive aracılığıyla ham IP paketi almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: bekleme seçeneği
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-raw-packet-send"></a>IP ham paket gönder 

#### <a name="nx_ip_raw_packet_send"></a>nx_ip_raw_packet_send

**Simge** ![ I P ham paket Gönder simgesi](./media/user-guide/netx-events/image103.png)

**Açıklama**

Bu olay, ham IP paketini nx_ip_raw_packet_send aracılığıyla göndermeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: hedef IP adresi
- Bilgi alanı 4: hizmet türü

### <a name="ip-static-route-add"></a>IP statik yol ekleme 

#### <a name="nx_ip_static_route_add"></a>nx_ip_static_route_add

**Simge** ![ I P statik yol ekleme simgesi](./media/user-guide/netx-events/image104.png)

**Açıklama**

Bu olay, nx_ip_static_route_add aracılığıyla IP örneği yönlendirme tablosuna eklenmekte olan statik bir yolu temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: ağ adresi
- Bilgi alanı 3: ağ maskesi
- Bilgi alanı 4: sonraki atlama

### <a name="ip-static-route-delete"></a>IP statik yol silme 

#### <a name="nx_ip_static_route_delete"></a>nx_ip_static_route_delete

**Simge** ![ I P statik Rute silme simgesi](./media/user-guide/netx-events/image105.png)

**Açıklama**

Bu olay, nx_ip_static_route_delete aracılığıyla IP örneği yönlendirme tablosundan çıkarılan statik bir yolu temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: ağ adresi
- Bilgi alanı 3: ağ maskesi
- Bilgi alanı 4: kullanılmıyor

### <a name="ip-status-check"></a>IP durum denetimi 

#### <a name="nx_ip_status_check"></a>nx_ip_status_check

**Simge** ![ I P durum denetimi simgesi](./media/user-guide/netx-events/image106.png)

**Açıklama**

Bu olay nx_ip_status_check aracılığıyla bir IP durumunun denetlenmesini temsil eder.

Bilgi alanları 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: Istenen durum
- Bilgi alanı 3: gerçek durum
- Bilgi alanı 4: bekleme seçeneği

### <a name="ipsec-enable"></a>IPSEC etkin 

#### <a name="nx_ipsec_enable"></a>nx_ipsec_enable

**Simge** ![ I P S E C etkinleştir simgesi](./media/user-guide/netx-events/image107.png)

**Açıklama**

Bu olay, sağlanan IP örneğindeki nx_ipsec_enable aracılığıyla IPSec hizmetlerinin etkinleştirilmesini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="packet-allocate"></a>Paket ayırma 

#### <a name="nx_packet_allocate"></a>nx_packet_allocate

**Simge** ![ Paket ayırma simgesi](./media/user-guide/netx-events/image108.png)

**Açıklama**

Bu olay nx_packet_allocate aracılığıyla bir paket ayırmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: paket havuzuna yönelik Işaretçi
- Bilgi alanı 2: ayrılmış paket Işaretçisi
- Bilgi alanı 3: paket türü
- Bilgi alanı 4: kullanılabilir paketler

### <a name="packet-copy"></a>Paket kopyası 

#### <a name="nx_packet_copy"></a>nx_packet_copy

**Simge** ![ Paket CPY simgesi](./media/user-guide/netx-events/image109.png)

**Açıklama**

Bu olay, bir paketin nx_packet_copy aracılığıyla kopyalanmasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 2: yeni paket işaretçisi
- Bilgi alanı 3: paket havuzu Işaretçisi
- Bilgi alanı 4: bekleme seçeneği

### <a name="packet-data-append"></a>Paket verileri ekleme 

#### <a name="nx_packet_data_append"></a>nx_packet_data_append

**Simge** ![ Paket verileri ekleme simgesi](./media/user-guide/netx-events/image110.png)

**Açıklama**

Bu olay nx_packet_data_append aracılığıyla bir pakete veri eklemeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: paket Işaretçisi
- Bilgi alanı 2: veri Işaretçisi
- Bilgi alanı 3: veri boyutu
- Bilgi alanı 4: paket havuzuna yönelik Işaretçi

### <a name="packet-data-extract-offset"></a>Paket verisi ayıklama kayması 

#### <a name="nx_udp_source_extract_offset"></a>nx_udp_source_extract_offset

**Simge** ![ Paket verileri ayıklama fark simgesi](./media/user-guide/netx-events/image111.png)

**Açıklama**

Bu olay, nx_udp_source_extract_offset aracılığıyla bir paketten sağlanan bir arabelleğe ayıklanan paket verilerini temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: paket Işaretçisi
- Bilgi alanı 2: belirtilen arabelleğin boyutu
- Bilgi alanı 3: kopyalanmış bayt sayısı
- Bilgi alanı 4: kullanılmıyor

### <a name="packet-data-retrieve"></a>Paket verilerini alma 

#### <a name="nx_packet_data_retrieve"></a>nx_packet_data_retrieve

**Simge** ![ Paket verilerini alma simgesi](./media/user-guide/netx-events/image112.png)

**Açıklama**

Bu olay nx_packet_data_retrieve aracılığıyla bir paketten veri almayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: paket Işaretçisi
- Bilgi alanı 2: arabelleğin başlangıcına yönelik Işaretçi
- Bilgi alanı 3: bayt kopyalanmış
- Bilgi alanı 4: kullanılmıyor

### <a name="packet-length-get"></a>Paket uzunluğu al 

#### <a name="nx_packet_length_get"></a>nx_packet_length_get

**Simge** ![ Paket uzunluğu al simgesi](./media/user-guide/netx-events/image113.png)

**Açıklama**

Bu olay, nx_packet_length_get aracılığıyla bir paketin uzunluğunu almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: paket Işaretçisi
- Bilgi alanı 2: paket uzunluğu
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="packet-pool-create"></a>Paket havuzu oluşturma 

#### <a name="nx_packet_pool_create"></a>nx_packet_pool_create

**Simge** ![ Paket havuzu oluştur simgesi](./media/user-guide/netx-events/image114.png)

**Açıklama**

Bu olay nx_packet_pool_create aracılığıyla bir paket havuzu oluşturmayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: paket havuzuna yönelik Işaretçi
- Bilgi alanı 2: Paket yükü boyutu
- Bilgi alanı 3: havuz bellek alanı Işaretçisi
- Bilgi alanı 4: havuz bellek alanının boyutu

### <a name="packet-pool-delete"></a>Paket havuzu silme 

#### <a name="nx_packet_pool_delete"></a>nx_packet_pool_delete

**Simge** ![ Paket havuzu silme simgesi](./media/user-guide/netx-events/image115.png)

**Açıklama**

Bu olay nx_packet_pool_delete aracılığıyla bir paket havuzunu silmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: paket havuzuna yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

#### <a name="packet-pool-information-get"></a>Paket havuzu bilgilerini al 

#### <a name="nx_packet_pool_info_get"></a>nx_packet_pool_info_get

**Simge** ![ Paket havuzu bilgileri al simgesi](./media/user-guide/netx-events/image116.png)

**Açıklama**

Bu olay, nx_packet_pool_info_get aracılığıyla paket havuzu bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: paket havuzuna yönelik Işaretçi
- Bilgi alanı 2: toplam paket sayısı
- Bilgi alanı 3: kullanılabilir paketler
- Bilgi alanı 4: boş istekler

### <a name="packet-release"></a>Paket sürümü 

#### <a name="nx_packet_data_release"></a>nx_packet_data_release

**Simge** ![ Paket yayını simgesi](./media/user-guide/netx-events/image117.png)

**Açıklama**

Bu olay nx_packet_release aracılığıyla bir paket serbest bırakmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: paket Işaretçisi
- Bilgi alanı 2: paket durumu
- Bilgi alanı 3: kullanılabilir paketler
- Bilgi alanı 4: kullanılmıyor

### <a name="packet-transmit-release"></a>Paket Iletme yayını 

#### <a name="nx_packet_transmit_release"></a>nx_packet_transmit_release

**Simge** ![ Paket iletme yayını simgesi](./media/user-guide/netx-events/image118.png)

**Açıklama**

Bu olay nx_packet_transmit_release aracılığıyla bir iletme paketi serbest bırakmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: paket Işaretçisi
- Bilgi alanı 2: paket durumu
- Bilgi alanı 3: kullanılabilir paketler
- Bilgi alanı 4: kullanılmıyor

### <a name="rarp-disable"></a>RARP devre dışı 

#### <a name="nx_rarp_disable"></a>nx_rarp_disable

**Simge** ![ R A R P devre dışı simgesi](./media/user-guide/netx-events/image119.png)

**Açıklama**

Bu olay, nx_rarp_disable aracılığıyla RARP devre dışı bırakmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="rarp-enable"></a>RARP etkinleştir 

#### <a name="nx_rarp_enable"></a>nx_rarp_enable

**Simge** ![ R A R P etkinleştirme simgesi](./media/user-guide/netx-events/image120.png)

**Açıklama**

Bu olay, nx_rarp_enable aracılığıyla RARP 'yi etkinleştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="rarp-information-get"></a>RARP bilgi edinme 

#### <a name="nx_rarp_info_get"></a>nx_rarp_info_get

**Simge** ![ R A R P bilgi al simgesi](./media/user-guide/netx-events/image121.png)

**Açıklama**

Bu olay nx_rarp_info_get aracılığıyla RARP bilgilerini almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: gönderilen Istekler
- Bilgi alanı 3: alınan yanıtlar
- Bilgi alanı 4: geçersiz yanıtlar

### <a name="system-initialize"></a>Sistem başlatma 

#### <a name="nx_system_initialize"></a>nx_system_initialize

**Simge** ![ Sistem başlatma simgesi](./media/user-guide/netx-events/image122.png)

**Açıklama**

Bu olay, nx_system_initialize aracılığıyla NetX başlatmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: kullanılmıyor
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="tcp-client-socket-bind"></a>TCP Istemci yuvası bağlama 

#### <a name="nx_tcp_client_socket_bind"></a>nx_tcp_client_socket_bind

**Simge** ![ T P istemci yuvası bağlama simgesi](./media/user-guide/netx-events/image123.png)

**Açıklama**

Bu olay, nx_tcp_client_socket_bind aracılığıyla bir istemci yuvasını bağlantı noktasına bağlamayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: bağlantı noktası istendi
- Bilgi alanı 4: bekleme seçeneği

### <a name="tcp-client-socket-connect"></a>TCP Istemci yuvası bağlantısı 

#### <a name="nx_tcp_client_socket_connect"></a>nx_tcp_client_socket_connect

**Simge** ![ T C P istemci yuvası bağlantı simgesi](./media/user-guide/netx-events/image124.png)

**Açıklama**

Bu olay, nx_tcp_client_socket_connect aracılığıyla bir istemci yuva bağlantısı yapmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: sunucu IP adresi
- Bilgi alanı 4: sunucu bağlantı noktası istendi

### <a name="tcp-client-socket-port-get"></a>TCP Istemci yuva bağlantı noktası al 

#### <a name="nx_tcp_client_socket_port_get"></a>nx_tcp_client_socket_port_get

**Simge** ![ T C P istemci yuva bağlantı noktası al simgesi](./media/user-guide/netx-events/image125.png)

**Açıklama**

Bu olay, istemci yuva bağlantı noktası numarasının nx_tcp_client_socket_port_get aracılığıyla alınmasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: bağlantı noktası numarası
- Bilgi alanı 4: kullanılmıyor

### <a name="tcp-client-socket-unbind"></a>TCP Istemci yuvası bağlantısı kesme 

#### <a name="nx_tcp_client_socket_unbind"></a>nx_tcp_client_socket_unbind

**Simge** ![ T C P istemci yuvası bağlantı çözme simgesi](./media/user-guide/netx-events/image126.png)

**Açıklama**

Bu olay, nx_tcp_client_socket_unbind aracılığıyla yuva ile ilişkili bağlantı noktasının bağlamasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="tcp-enable"></a>TCP etkinleştirme 

#### <a name="nx_tcp_enable"></a>nx_tcp_enable

**Simge** ![ T C P etkinleştirme simgesi](./media/user-guide/netx-events/image127.png)

**Açıklama**

Bu olay nx_tcp_enable aracılığıyla TCP etkinleştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

###  <a name="tcp-free-port-find-tcp-free-port-find"></a>TCP boş bağlantı noktası bulma TCP boş bağlantı noktası bulma 

#### <a name="nx_tcp_free_port_find"></a>nx_tcp_free_port_find

**Simge** ![ T CP boş bağlantı noktası bul simgesi](./media/user-guide/netx-events/image128.png)

**Açıklama**

Bu olay nx_tcp_free_port_find aracılığıyla boş bir TCP bağlantı noktası bulmayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: arama bağlantı noktası numarası başlatılıyor
- Bilgi alanı 3: ücretsiz bağlantı noktası numarası
- Bilgi alanı 4: kullanılmıyor

###  <a name="tcp-infomation-get"></a>TCP bilgisi al 

#### <a name="nx_tcp_info_get"></a>nx_tcp_info_get

**Simge** ![ T C P bilgi al simgesi](./media/user-guide/netx-events/image129.png)

**Açıklama**

Bu olay, nx_tcp_info_get aracılığıyla belirtilen IP örneği için TCP bilgilerini almayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: gönderilen bayt sayısı
- Bilgi alanı 3: alınan bayt sayısı
- Bilgi alanı 4: Geçersiz paketlerin sayısı

###  <a name="tcp-server-socket-accept"></a>TCP sunucusu yuvasını kabul etme 

#### <a name="nx_tcp_server_socket_accept"></a>nx_tcp_server_socket_accept

**Simge** ![ T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image130.png)

**Açıklama**

Bu olay, nx_tcp_server_socket_accept aracılığıyla bir etkin bağlantı isteği alındıktan sonra sunucu yuvasını ayarlamayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: bekleme seçeneği
- Bilgi alanı 4: yuva durumu

###  <a name="tcp-server-socket-listen"></a>TCP sunucusu yuva dinleme 

#### <a name="nx_tcp_server_socket_listen"></a>nx_tcp_server_socket_listen

**Simge** ![ T C P sunucu yuvası lsten simgesi](./media/user-guide/netx-events/image131.png)

**Açıklama**

Bu olay, nx_tcp_server_socket_listen aracılığıyla belirtilen TCP bağlantı noktası için bir dinleme isteğini ve sunucu yuvasını kaydetmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: TCP bağlantı noktası numarası
- Bilgi alanı 3: yuva Işaretçisi
- Bilgi alanı 4: sıraya alınabilen en fazla bağlantı sayısı

###  <a name="tcp-server-socket-relisten"></a>TCP sunucu yuvası yeniden dinleme 

#### <a name="nx_tcp_server_socket_relisten"></a>nx_tcp_server_socket_relisten

**Simge** ![ T C P sunucu yuvası yeniden dinleme simgesi](./media/user-guide/netx-events/image132.png)

**Açıklama**

Bu olay, nx_tcp_server_socket_relisten aracılığıyla belirtilen TCP bağlantı noktasında var olan bir dinleme isteği için başka bir sunucu yuvasını kaydetmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: TCP bağlantı noktası numarası
- Bilgi alanı 3: yuva Işaretçisi
- Bilgi alanı 4: yuva durumu

###  <a name="tcp-server-socket-unaccept"></a>TCP sunucusu yuvası kabul etme 

#### <a name="nx_tcp_server_socket_unaccept"></a>nx_tcp_server_socket_unaccept

**Simge** ![ T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image133.png)

**Açıklama**

Bu olay, nx_tcp_server_socket_unaccept aracılığıyla önceki bir pasif bağlantıyı alan bağlantı noktasıyla ilişkilendirmeden sunucu yuvasını kaldırmayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: yuva durumu
- Bilgi alanı 4: kullanılmıyor

###  <a name="tcp-server-socket-unlisten-tcp-server-socket-unlisten"></a>TCP sunucu yuvası dinleme TCP sunucusu yuva geri dinleme 

#### <a name="nx_tcp_server_socket_unlisten"></a>nx_tcp_server_socket_unlisten

**Simge** ![ T C P Server yuva geri dinleme simgesi](./media/user-guide/netx-events/image134.png)

**Açıklama**

Bu olay, belirtilen TCP bağlantı noktası için önceki bir dinleme isteğinin nx_tcp_server_socket_unlisten aracılığıyla kaldırılmasını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: TCP bağlantı noktası numarası
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="tcp-socket-bytes-available"></a>Kullanılabilir TCP yuvası baytları 

#### <a name="nx_tcp_socket_bytes_available"></a>nx_tcp_socket_bytes_available

**Simge** ![ T C P yuva baytları kullanılabilir simgesi](./media/user-guide/netx-events/image135.png)

**Açıklama**

Bu olay, nx_tcp_socket_bytes_available aracılığıyla belirtilen TCP alma yuvasında mevcut olan bayt sayısını temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: TCP yuvası Işaretçisi
- Bilgi alanı 3: yuvada alınan baytlar
- Bilgi alanı 4: kullanılmıyor

### <a name="tcp-socket-create"></a>TCP yuvası oluşturma 

#### <a name="nx_tcp_socket_create"></a>nx_tcp_socket_create

**Simge** ![ T C P yuvası oluşturma simgesi](./media/user-guide/netx-events/image136.png)

**Açıklama**

Bu olay nx_tcp_socket_create aracılığıyla bir TCP yuvası oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: hizmet türü
- Bilgi alanı 4: pencere boyutunu al

### <a name="tcp-socket-delete"></a>TCP yuvası silme 

#### <a name="nx_tcp_socket_delete"></a>nx_tcp_socket_delete

**Simge** ![ T C P yuvası silme simgesi](./media/user-guide/netx-events/image137.png)

**Açıklama**

Bu olay nx_tcp_socket_delete aracılığıyla bir yuvayı silmeyi temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: yuva durumu
- Bilgi alanı 4: kullanılmıyor

### <a name="tcp-socket-disconnect"></a>TCP yuvası bağlantısı kesme 

#### <a name="nx_tcp_socket_disconnect"></a>nx_tcp_socket_disconnect

**Simge** ![ T C P yuvası bağlantı kesme simgesi](./media/user-guide/netx-events/image138.png)

**Açıklama**

Bu olay nx_tcp_socket_disconnect aracılığıyla bir yuvanın bağlantısını kesmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: bekleme seçeneği
- Bilgi alanı 4: yuva durumu

### <a name="tcp-socket-information-get"></a>TCP yuva bilgileri Get 

#### <a name="nx_tcp_socket_info_get"></a>nx_tcp_socket_info_get

**Simge** ![ T C P yuva bilgileri al simgesi](./media/user-guide/netx-events/image139.png)

**Açıklama**

Bu olay nx_tcp_socket_info_get aracılığıyla bir yuva hakkında bilgi almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: Bu yuva aracılığıyla gönderilen baytlar
- Bilgi alanı 4: Bu yuva aracılığıyla alınan baytlar

### <a name="tcp-socket-mss-get"></a>TCP yuvası ve Get 

#### <a name="nx_tcp_socket_mss_get"></a>nx_tcp_socket_mss_get

**Simge** ![ T C P yuvası M S S al simgesi](./media/user-guide/netx-events/image140.png)

**Açıklama**

Bu olay, nx_tcp_socket_mss_get aracılığıyla yuvanın bir hakete alınmasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: en fazla segment boyutu (
- Bilgi alanı 4: yuva durumu

### <a name="tcp-socket-mss-peer-get"></a>TCP soketi eşi al 

#### <a name="nx_tcp_socket_mss_peer_get"></a>nx_tcp_socket_mss_peer_get

**Simge** ![ T C P yuvası M S S eşi al simgesi](./media/user-guide/netx-events/image141.png)

**Açıklama**

Bu olay, yuvanın eşinin nx_tcp_socket_mss_peer_get aracılığıyla sahip olduğu değeri almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: eşler arası
- Bilgi alanı 4: yuva durumu

### <a name="tcp-socket-mss-set"></a>TCP yuvası, küme 

#### <a name="nx_tcp_socket_mss_set"></a>nx_tcp_socket_mss_set

**Simge** ![ T C P yuvası M S S set simgesi](./media/user-guide/netx-events/image142.png)

**Açıklama**

Bu olay, bir yuvanın nx_tcp_socket_mss_set aracılığıyla ayarlanmasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: Bu
- Bilgi alanı 4: yuva durumu

### <a name="tcp-socket-peer-info-get"></a>TCP yuvası eş bilgi al 

#### <a name="nx_tcp_socket_peer_info_get"></a>nx_tcp_socket_peer_info_get

**Simge** ![ T C P soket eş bilgi al simgesi](./media/user-guide/netx-events/image143.png)

**Açıklama**

Bu olay, eş (örneğin, ana bilgisayar >bağlanması) IP adresi ve bağlantı noktası ile ilgili TCP yuvasından alınan bilgileri nx_tcp_socket_peer_info_get aracılığıyla temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: TCP yuvası Işaretçisi
- Bilgi alanı 2: eş IP adresi
- Bilgi alanı 3: eş bağlantı noktası numarası
- Bilgi alanı 4: kullanılmıyor

### <a name="tcp-socket-receive"></a>TCP yuvası alma 

#### <a name="nx_tcp_socket_receive"></a>nx_tcp_socket_receive

**Simge** ![ T C P yuvası alma simgesi](./media/user-guide/netx-events/image144.png)

**Açıklama**

Bu olay, nx_tcp_socket_receive aracılığıyla bir yuvadan veri almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: yuva Işaretçisi
- Bilgi alanı 2: alınan paket Işaretçisi
- Bilgi alanı 3: paket uzunluğu alındı
- Bilgi alanı 4: alma sıra numarası

### <a name="tcp-socket-receive-notify"></a>TCP yuvası alma bildirimi 

#### <a name="nx_tcp_socket_receive_notify"></a>nx_tcp_socket_receive_notify

**Simge** ![ T C P yuvası alma bildirim simgesi](./media/user-guide/netx-events/image145.png)

**Açıklama**

Bu olay, bir yuva için nx_tcp_socket_receive_notify aracılığıyla bir alma bildirimi geri araması kaydetmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: alma için geri arama bilgi alan 4: kullanılmıyor

### <a name="tcp-socket-send"></a>TCP yuvası gönderme 

#### <a name="nx_tcp_socket_send"></a>nx_tcp_socket_send

**Simge** ![ T C P yuvası gönderme simgesi](./media/user-guide/netx-events/image146.png)

**Açıklama**

Bu olay nx_tcp_socket_send aracılığıyla bir yuvada veri göndermeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: yuva Işaretçisi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: paket uzunluğu
- Bilgi alanı 4: aktarım sıra numarası

### <a name="tcp-socket-state-wait"></a>TCP yuva durumu bekleme 

#### <a name="nx_tcp_socket_state_wait"></a>nx_tcp_socket_state_wait

**Simge** ![ T C P yuva durumu bekleme simgesi](./media/user-guide/netx-events/image147.png)

**Açıklama**

Bu olay, bir yuvanın nx_tcp_socket_state_wait aracılığıyla belirli bir durumu girmesini beklemeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: Istenen yuva durumu
- Bilgi alanı 4: önceki yuva durumu

### <a name="tcp-socket-transmit-configure"></a>TCP yuvası Iletme yapılandırması 

#### <a name="nx_tcp_socket_transmit_configure"></a>nx_tcp_socket_transmit_configure

**Simge** ![ T C P yuvası iletme yapılandırma simgesi](./media/user-guide/netx-events/image148.png)

**Açıklama**

Bu olay, nx_tcp_socket_transmit_configure aracılığıyla bir yuva için iletme seçeneklerini yapılandırmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: aktarım sırası derinliği
- Bilgi alanı 4: zaman aşımı değeri

### <a name="tcp-socket-window-update-notify-set"></a>TCP yuvası pencere güncelleştirme bildirim kümesi 

#### <a name="nx_tcp_window_update_notify_set"></a>nx_tcp_window_update_notify_set

**Simge** ![ T C P yuvası pencere güncelleştirme bildirim kümesi simgesi](./media/user-guide/netx-events/image149.png)

**Açıklama**

Bu olay, nx_tcp_window_update_notify_set aracılığıyla uzak ana bilgisayar alma penceresinde bir artışın TCP yuvası alma bildirimini temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: TCP yuvası Işaretçisi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-enable"></a>UDP etkinleştirme 

#### <a name="nx_udp_enable"></a>nx_udp_enable

**Simge** ![ U D P etkinleştirme simgesi](./media/user-guide/netx-events/image150.png)

**Açıklama**

Bu olay nx_udp_enable aracılığıyla UDP etkinleştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: kullanılmıyor
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-free-port-find"></a>UDP boş bağlantı noktası bulma 

#### <a name="nx_udp_free_port_find"></a>nx_udp_free_port_find

**Simge** ![ U D P boş bağlantı noktası bul simgesi](./media/user-guide/netx-events/image151.png)

**Açıklama**

Bu olay nx_udp_free_port_find aracılığıyla boş bir UDP bağlantı noktası bulmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: arama yapılacak bağlantı noktası başlatılıyor
- Bilgi alanı 3: ücretsiz bağlantı noktası
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-information-get"></a>UDP bilgisi al 

#### <a name="nx_udp_info_get"></a>nx_udp_info_get

**Simge** ![ U D P bilgi al simgesi](./media/user-guide/netx-events/image152.png)

**Açıklama**

Bu olay nx_udp_info_get aracılığıyla bilgi almayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: gönderilen UDP baytları
- Bilgi alanı 3: alınan UDP baytları
- Bilgi alanı 4: geçersiz paketler

### <a name="udp-socket-bind"></a>UDP yuvası bağlama 

#### <a name="nx_udp_socket_bind"></a>nx_udp_socket_bind

**Simge** ![ U D P yuvası bağlama simgesi](./media/user-guide/netx-events/image153.png)

**Açıklama**

Bu olay, nx_udp_socket_bind aracılığıyla bir UDP yuvasını bağlantı noktasına bağlamayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: bağlantı noktası numarası
- Bilgi alanı 4: bekleme seçeneği

### <a name="udp-socket-bytes-available"></a>Kullanılabilir UDP yuva baytları 

#### <a name="nx_udp_socket_bytes_available"></a>nx_udp_socket_bytes_available

**Simge** ![ U D P yuva baytları kullanılabilir simgesi](./media/user-guide/netx-events/image154.png)

**Açıklama**

Bu olay, UDP yuvasında nx_udp_socket_bytes_available aracılığıyla alınan geçerli bayt sayısını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: yuvada alınan baytlar
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-socket-checksum-disable"></a>UDP yuva sağlama toplamı devre dışı 

#### <a name="nx_udp_socket_checksum_disable"></a>nx_udp_socket_checksum_disable

**Simge** ![ U D P soket sağlama toplamı devre dışı simgesi](./media/user-guide/netx-events/image155.png)

**Açıklama**

Bu olay, nx_udp_socket_checksum_disable aracılığıyla bir UDP yuvasında veriler için sağlama toplamı devre dışı bırakmayı temsil eder.

**Bilgi alanları** 

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-socket-checksum-enable"></a>UDP yuva sağlama toplamı etkinleştir 

#### <a name="nx_udp_socket_checksum_enable"></a>nx_udp_socket_checksum_enable

**Simge** ![ U D P yuva sağlama toplamı etkinleştir simgesi](./media/user-guide/netx-events/image156.png)

**Açıklama**

Bu olay, nx_udp_socket_checksum_enable aracılığıyla bir yuvada sağlama toplamı işlemeyi etkinleştirmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-socket-create"></a>UDP yuvası oluşturma 

#### <a name="nx_udp_socket_create"></a>nx_udp_socket_create

**Simge** ![ U D P yuvası oluşturma simgesi](./media/user-guide/netx-events/image157.png)

**Açıklama**

Bu olay nx_udp_socket_create aracılığıyla bir UDP yuvası oluşturmayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: hizmet türü
- Bilgi alanı 4: en fazla alma kuyruğu

### <a name="udp-socket-delete-event"></a>UDP yuvası silme olayı 

#### <a name="nx_udp_socket_delete-event"></a>nx_udp_socket_delete olayı

**Simge** ![ U D P yuvası silme olayı simgesi](./media/user-guide/netx-events/image158.png)

**Açıklama**

Bu olay nx_udp_socket_delete aracılığıyla bir UDP yuvasını silmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-socket-information-get-event"></a>UDP yuva bilgileri Get olayı 

#### <a name="nx_udp_socket_info_get-event"></a>nx_udp_socket_info_get olayı

**Simge** ![ U D P yuva bilgileri olay al simgesi](./media/user-guide/netx-events/image159.png)

**Açıklama**

Bu olay nx_udp_socket_info_get aracılığıyla bir UDP yuvası hakkında bilgi almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: yuva aracılığıyla gönderilen baytlar
- Bilgi alanı 4: yuva aracılığıyla alınan baytlar

### <a name="udp-socket-interface-set"></a>UDP yuva arabirimi kümesi 

#### <a name="nx_udp_socket_interface_set-event"></a>nx_udp_socket_interface_set olayı

**Simge** ![ U D P yuva arabirimi kümesi simgesi](./media/user-guide/netx-events/image160.png)

**Açıklama**

Bu olay, belirtilen UDP yuvasının giden arabirimini nx_udp_socket_interface_set aracılığıyla belirtilen arabirimle ayarlamayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: UDP yuvası Işaretçisi
- Bilgi alanı 2: yuva arabirimine karşılık gelen dizin
- Bilgi alanı 3: kullanılmıyor
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-socket-port-get"></a>UDP yuva bağlantı noktası al 

#### <a name="nx_udp_socket_port_get"></a>nx_udp_socket_port_get

**Simge** ![ U D P yuva bağlantı noktası al simgesi](./media/user-guide/netx-events/image161.png)

**Açıklama**

Bu olay, belirtilen UDP yuvasının nx_udp_socket_port_get aracılığıyla bağlandığı UDP bağlantı noktasının alınması temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: UDP yuvası Işaretçisi
- Bilgi alanı 3: bağlantı noktası numarası
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-socket-receive"></a>UDP yuvası alma 

#### <a name="nx_udp_socket_receive"></a>nx_udp_socket_receive

**Simge** ![ U D P yuvası alma simgesi](./media/user-guide/netx-events/image162.png)

**Açıklama**

Bu olay, belirtilen UDP yuvasında nx_udp_socket_receive aracılığıyla veri almayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: UDP yuvası Işaretçisi
- Bilgi alanı 3: alınan paket Işaretçisi
- Bilgi alanı 4: paket boyutu alındı

### <a name="udp-socket-receive-notify"></a>UDP yuvası alma bildirimi 

#### <a name="nx_udp_socket_receive_notify"></a>nx_udp_socket_receive_notify

**Simge** ![ U D P yuvası alma bildirim simgesi ](./media/user-guide/netx-events/image163.png) s **açıklaması**

Bu olay nx_udp_socket_receive_notify aracılığıyla bir alma bildirimi geri araması kaydetmeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: bildirim alma işlevi bilgi alanı 4: kullanılmıyor

### <a name="udp-socket-send"></a>UDP yuvası gönderme 

#### <a name="nx_udp_socket_send"></a>nx_udp_socket_send

**Simge** ![ U D P yuvası gönderme simgesi](./media/user-guide/netx-events/image164.png)

**Açıklama**

Bu olay nx_udp_socket_send aracılığıyla bir UDP yuvası üzerinden veri göndermeyi temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: yuva Işaretçisi
- Bilgi alanı 2: paket Işaretçisi
- Bilgi alanı 3: paket uzunluğu
- Bilgi alanı 4: hedef IP adresi

### <a name="udp-socket-unbind"></a>UDP yuvası bağlantısı kesme 

#### <a name="nx_udp_socket_unbind"></a>nx_udp_socket_unbind

**Simge** ![ U D P yuvası çözme simgesi](./media/user-guide/netx-events/image165.png)

**Açıklama**

Bu olay, nx_udp_socket_unbind aracılığıyla bir yuva ile UDP bağlantı noktası bağlamayı temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: IP örneğine yönelik Işaretçi
- Bilgi alanı 2: yuva Işaretçisi
- Bilgi alanı 3: bağlantı noktası numarası
- Bilgi alanı 4: kullanılmıyor

### <a name="udp-source-extract"></a>UDP kaynağı ayıklama 

#### <a name="nx_udp_socket_create"></a>nx_udp_socket_create

**Simge** ![ U D P kaynağı ayıklama simgesi](./media/user-guide/netx-events/image166.png)

**Açıklama**

Bu olay, alınan bir UDP paketinin IP adresi ve bağlantı noktası numarasının nx_udp_source_extract aracılığıyla alınmasını temsil eder.

**Bilgi alanları**

- Bilgi alanı 1: paket Işaretçisi
- Bilgi alanı 2: gönderenin IP adresi
- Bilgi alanı 3: gönderenin bağlantı noktası numarası
- Bilgi alanı 4: kullanılmıyor