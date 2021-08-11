---
title: Bölüm 8 - Azure RTOS NetX izleme olayları
description: Bu bölümde NetX olaylarının Azure RTOS yer almaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: f785b421ffc6d588080eb45a50dad949daf1ca6a9bf36770110f0450cd465bf1
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116806574"
---
# <a name="chapter-8---azure-rtos-netx-trace-events"></a>Bölüm 8 - Azure RTOS NetX izleme olayları

Bu bölümde NetX olaylarının Azure RTOS yer almaktadır. 

## <a name="list-of-events-and-icons"></a>Olay ve Simgelerin Listesi

TraceX tarafından görüntülenen NetX olaylarının listesi aşağıdadır.

| Simge                                           | Anlamı                 |
| -------------------------------- | ------------------------------------- |
| ![R P İsteği Alma iç simgesi](./media/user-guide/netx-events/image1.png)    | İç ARP İsteği Alma |
| ![İç A R P İstek Gönderme simgesi](./media/user-guide/netx-events/image2.png)    | İç ARP İstek Gönderme |
| ![İç A R P Yanıt Alma simgesi](./media/user-guide/netx-events/image3.png)    | İç ARP Yanıt Alma |
| ![İç A R P Yanıt Gönderme simgesi](./media/user-guide/netx-events/image4.png)    | İç ARP Yanıt Gönderme |
| ![İç I C M P Alma simgesi](./media/user-guide/netx-events/image5.png)    | İç ICMP Alma |
| ![İç I C M P Gönder simgesi](./media/user-guide/netx-events/image6.png)    | İç ICMP Gönderme |
| ![İç NetX I G M P Alma simgesi](./media/user-guide/netx-events/image7.png)    | İç NetX IGMP Alma |
| ![İç I P Alma simgesi](./media/user-guide/netx-events/image8.png)    | İç IP Alma |
| ![İç I P Gönder simgesi](./media/user-guide/netx-events/image9.png)    | İç IP Gönderme |
| ![İç T C P Veri Alma simgesi](./media/user-guide/netx-events/image10.png)    | İç TCP Verileri Alma |
| ![İç T C P Veri Gönderme simgesi](./media/user-guide/netx-events/image11.png)    | İç TCP Veri Gönderme |
| ![İç T C P FIN Alma simgesi](./media/user-guide/netx-events/image12.png)    | İç TCP FIN Alma |
| ![İç T C P F I N Gönder simgesi](./media/user-guide/netx-events/image13.png)    | İç TCP FIN Gönderme |
| ![İç T C P R S T Alma simgesi](./media/user-guide/netx-events/image14.png)    | İç TCP RST Alma |
| ![İç T C P R S T Gönderme simgesi](./media/user-guide/netx-events/image15.png)    | İç TCP RST Gönderme |
| ![İç T C P S Y N Alma simgesi](./media/user-guide/netx-events/image16.png)    | İç TCP SYN Alma |
| ![İç T C P S Y N Gönder simgesi](./media/user-guide/netx-events/image17.png)    | İç TCP SYN Gönderme |
| ![İç UD P Alma simgesi](./media/user-guide/netx-events/image18.png)    | İç UDP Alma |
| ![İç UD P Gönder simgesi](./media/user-guide/netx-events/image19.png)    | İç UDP Gönderme |
| ![İç R A R P Alma simgesi](./media/user-guide/netx-events/image20.png)    | İç RARP Alma |
| ![İç R A R P Gönder simgesi](./media/user-guide/netx-events/image21.png)    | İç RARP Gönderme |
| ![İç T C P Yeniden Deneme simgesi](./media/user-guide/netx-events/image22.png)    | İç TCP Yeniden Denemesi |
| ![İç T C P Durum Değişikliği simgesi](./media/user-guide/netx-events/image23.png)    | İç TCP Durum Değişikliği |
| ![İç I / O Sürücüsü Paket Gönderme simgesi](./media/user-guide/netx-events/image24.png)    | İç I/O Sürücü Paketi Gönderme |
| ![Simge](./media/user-guide/netx-events/image25.png)    | İç I/O Sürücüsü Başlatma |
| ![İç I / O Sürücüsü Başlatma simgesi](./media/user-guide/netx-events/image26.png)    | İç I/O Sürücü Bağlantısı Etkinleştirme |
| ![İç I / O Sürücüsü Bağlantısı Devre Dışı Bırak simgesi](./media/user-guide/netx-events/image27.png)    | İç I/O Sürücü Bağlantısını Devre Dışı Bırakma |
| ![İç I / O Sürücüsü Paket Yayını simgesi](./media/user-guide/netx-events/image28.png)    | İç I/O Sürücü Paketi Yayını |
| ![İç G/Ç Sürücüsü ARP Gönderme simgesi](./media/user-guide/netx-events/image29.png)    | İç G/Ç Sürücüsü ARP Gönderme |
| ![İç G/Ç Sürücüsü ARP Yanıt Gönderme simgesi](./media/user-guide/netx-events/image30.png)    | İç G/Ç Sürücüsü ARP Yanıt Gönderme |
| ![İç G/Ç Sürücüsü RARP Gönderme simgesi](./media/user-guide/netx-events/image31.png)    | İç G/Ç Sürücüsü RARP Gönderme |
| ![İç I / O Sürücüsü Çok Noktaya Yayına Katılma simgesi](./media/user-guide/netx-events/image32.png)    | İç I/O Sürücüsü Çok Noktaya Yayına Katılma |
| ![İç I / O Sürücüsü Çok Noktaya Yayın Bırak simgesi](./media/user-guide/netx-events/image33.png)    | İç I/O Sürücüsü Çok Noktaya Yayın Bırakma |
| ![İç I / O Sürücüsü Durumu Al simgesi](./media/user-guide/netx-events/image34.png)    | İç I/O Sürücüsü Durumu Al |
| ![İç I / O Sürücüsü Hız Al simgesi](./media/user-guide/netx-events/image35.png)    | İç I/O Sürücüsü Hız Al |
| ![İç I / O Sürücüsü Çift Yönlü Türü Al simgesi](./media/user-guide/netx-events/image36.png)    | İç I/O Sürücüsü Çift Yönlü Türü Al |
| ![İç I / O Sürücüsü Hata Sayısını Al simgesi](./media/user-guide/netx-events/image37.png)    | İç I/O Sürücüsü Hata Sayısını Al |
| ![İç G/Ç Sürücüsü RX Sayısını Al simgesi](./media/user-guide/netx-events/image38.png)    | İç G/Ç Sürücüsü RX Sayısını Al |
| ![İç I / O Sürücüsü TX Sayısını Al simgesi](./media/user-guide/netx-events/image39.png)    | İç I/O Sürücüsü TX Sayısını Al |
| ![İç I / O Sürücüsü Ayırma Hatalarını Al simgesi](./media/user-guide/netx-events/image40.png)    | İç I/O Sürücüsü Ayırma Hatalarını Al |
| ![İç I / O Sürücüsü Başlatmayı Geri Başlat simgesi](./media/user-guide/netx-events/image41.png)    | İç I/O Sürücüsü Başlatmayı Geri Başlatma |
| ![İç I / O Sürücüsü Ertelenmiş İşleme simgesi](./media/user-guide/netx-events/image42.png)    | İç I/O Sürücüsü Ertelenmiş İşleme |
| ![R P Dinamik Girişleri Geçersiz Kıldı simgesi](./media/user-guide/netx-events/image43.png)    | **ARP Dinamik Girişleri Geçersiz Kılınıyor** (*nx_arp_dynamic_entries_invalidate*) |
| ![R P Dinamik Giriş Kümesi simgesi](./media/user-guide/netx-events/image44.png)    | **ARP Dinamik Giriş Kümesi** (*nx_arp_dynamic_entry_set*) |
| ![R P Etkinleştir simgesi](./media/user-guide/netx-events/image45.png)    | **ARP Etkinleştirme** (*nx_arp_enable*) |
| ![R P Gratuitous Send simgesi](./media/user-guide/netx-events/image46.png)    | **ARP Gratuitous Send** (*nx_arp_gratuitous_send*) |
| ![R P Donanım Adresi Bul simgesi](./media/user-guide/netx-events/image47.png)    | **ARP Donanım Adresi Bulma** (*nx_arp_hardware_address_find*) |
| ![R P Bilgileri Al simgesi](./media/user-guide/netx-events/image48.png)    | **ARP Bilgi Al** (*nx_arp_info_get*) |
| ![R P IP Adresi Bul simgesi](./media/user-guide/netx-events/image49.png)    | **ARP IP Adresi Bulma** (*nx_arp_ip_address_find*) |
| ![R P Statik Giriş Oluşturma simgesi](./media/user-guide/netx-events/image50.png)    | **ARP Statik Giriş Oluşturma** (*nx_arp_static_entry_create*) |
| ![R P Statik Girdileri Silme simgesi](./media/user-guide/netx-events/image51.png)    | **ARP Statik Girdileri Silme** (*nx_arp_static_entries_delete*) |
| ![R P Statik Giriş Silme simgesi](./media/user-guide/netx-events/image52.png)    | **ARP Statik Giriş Silme** (*nx_arp_static_entry_delete*) |
| ![Duo Cache Girişi Silme simgesi](./media/user-guide/netx-events/image53.png)    | **Duo Cache Girişi Silme** (*nxd_nd_cache_entry_delete*) |
| ![Duo Cache Giriş Kümesi simgesi](./media/user-guide/netx-events/image54.png)    | **Duo Cache Giriş Kümesi** (*nxd_nd_cache_entry_set*) |
| ![Duo Cache Invalidate simgesi](./media/user-guide/netx-events/image55.png)    | **Duo Cache Invalidate** (*nxd_nd_cache_invalidate*) |
| ![Duo Cache I P Adresi Bul simgesi](./media/user-guide/netx-events/image56.png)    | **Duo Önbelleği IP Adresi Bulma** (*nxd_nd_cache_ip_address_find*) |
| ![Duo I C M P Enable simgesi](./media/user-guide/netx-events/image57.png)    | **Duo ICMP Enable** (*nxd_icmp_enable*) |
| ![Duo I C M P I P v 6 Ping simgesi](./media/user-guide/netx-events/image58.png)    | **Duo ICMP IPv6 Ping** (*nxd_icmp_ping*) |
| ![Duo I P Max Payload Size Find simgesi](./media/user-guide/netx-events/image59.png)    | **Duo IP Max Payload Size Find** (*nx_max_payload_size_find*) |
| ![Duo I P Ham Paket Gönderme simgesi](./media/user-guide/netx-events/image60.png)    | **Duo IP Ham Paket Gönderme** (*nxd_ip_raw_packet_send*) |
| ![Duo I P v 6 Varsayılan Yönlendirici Ekle simgesi](./media/user-guide/netx-events/image61.png)    | **Duo IPv6 Varsayılan Yönlendirici Ekleme** (*nxd_ipv6_default_router_add*) |
| ![Duo I P v 6 Varsayılan Yönlendirici Silme simgesi](./media/user-guide/netx-events/image62.png)    | **Duo IPv6 Varsayılan Yönlendirici Silme** (*nxd_ipv6_default_router_delete)* |
| ![Duo I P v 6 Etkinleştir simgesi](./media/user-guide/netx-events/image63.png)    | **Duo IPv6 Etkinleştirme** (*nxd_ipv6_enable)* |
| ![Duo I P v 6 Genel Adres Al simgesi](./media/user-guide/netx-events/image64.png)    | **Duo IPv6 Genel Adres Al** (*nxd_ipv6_global_address_get*) |
| ![Duo I P v 6 Genel Adres Kümesi simgesi](./media/user-guide/netx-events/image65.png)    | **Duo IPv6 Genel Adres Kümesi** (*nxd_ipv6_global_address_set*) |
| ![Duo I P v 6 Initiate Initiate Initiate Process simgesi](./media/user-guide/netx-events/image66.png)    | **Duo IPv6 Initiate Process** (*nxd_ipv6_initiate_dad_process*) |
| ![Duo I P v 6 Arabirim Adresi Al simgesi](./media/user-guide/netx-events/image67.png)    | **Duo IPv6 Arabirim Adresi Get** (*nxd_ipv6_interface_address_get*) |
| ![Duo I P v 6 Arabirim Adres Kümesi simgesi](./media/user-guide/netx-events/image68.png)    | **Duo IPv6 Arabirim Adres Kümesi** (*nxd_ipv6_interface_address_set*) |
| ![Duo I P v 6 Link Local Address Get simgesi](./media/user-guide/netx-events/image69.png)    | **Duo IPv6 Link Local Address Get** (*nxd_ipv6_linklocal_address_get*) |
| ![Duo I P v 6 Link Local Address Set simgesi](./media/user-guide/netx-events/image70.png)    | **Duo IPv6 Link Yerel Adres Kümesi** (*nxd_ipv6_linklocal_address_set*) |
| ![Duo I P v 6 Ham Paket Gönderme simgesi](./media/user-guide/netx-events/image71.png)    | **Duo IPv6 Ham Paket Gönderme** (*nxd_ipv6_raw_packet_send)* |
| ![Duo T C P Yuva Eş Bilgileri Al simgesi](./media/user-guide/netx-events/image72.png)    | **Duo TCP Yuva Eş Bilgisi Al** (*nxd_tcp_socket_peer_info_get*) |
| ![Duo T C P Yuva Kümesi Arabirimi simgesi](./media/user-guide/netx-events/image73.png)    | **Duo TCP Yuva Kümesi Arabirimi** (*nxd_tcp_socket_set_interface*) |
| ![Duo U D P Yuva Gönderme simgesi](./media/user-guide/netx-events/image74.png)    | **Duo UDP Yuva Gönderme** (*nxd_udp_socket_send*) |
| ![Duo U D P Yuva Kümesi Arabirimi simgesi](./media/user-guide/netx-events/image75.png)    | **Duo UDP Yuva Kümesi Arabirimi** (*nxd_udp_socket_set_interface*) |
| ![Duo U D P Source Extract simgesi](./media/user-guide/netx-events/image76.png)    | **Duo UDP Kaynak Ayıklama** (*nxd_udp_source_extract*) |
| ![I C M P Enable simgesi](./media/user-guide/netx-events/image77.png)    | **ICMP Etkinleştirme** (*nx_icmp_enable*) |
| ![I C M P Bilgi Al simgesi](./media/user-guide/netx-events/image78.png)    | **ICMP Bilgileri Al** (*nx_icmp_info_get*) |
| ![I C M P Ping simgesi](./media/user-guide/netx-events/image79.png)    | **ICMP Ping** (*nx_icmp_ping*) |
| ![I G M P Etkinleştir simgesi](./media/user-guide/netx-events/image80.png)    | **IGMP Etkinleştirme** (*nx_igmp_enable*) |
| ![I G M P Bilgileri Al simgesi](./media/user-guide/netx-events/image81.png)    | **IGMP Bilgileri Al** (*nx_igmp_info_get*) |
| ![I G M P Geri Döngü Devre Dışı Bırak simgesi](./media/user-guide/netx-events/image82.png)    | **IGMP Geri Döngü Devre Dışı Bırakma** (*nx_igmp_loopback_disable*) |
| ![I G M P Geri Döngü Etkinleştir simgesi](./media/user-guide/netx-events/image83.png)    | **IGMP Geri Döngü Etkinleştirme** (*nx_igmp_loopback_enable*) |
| ![I G M P Çok Noktaya Yayına Katılma simgesi](./media/user-guide/netx-events/image84.png)    | **IGMP Çok Noktaya Yayın Birleştirme** (*nx_igmp_multicast_join*) |
| ![I G M P Multicast Leave simgesi](./media/user-guide/netx-events/image85.png)    | **IGMP Çok Noktaya Yayın Bırakma** (*nx_igmp_multicast_leave*) |
| ![I P Adresi Değişikliği Bildirimi simgesi](./media/user-guide/netx-events/image86.png)    | **IP Adresi Değişikliği Bildirimi** (*nx_ip_address_change_notify*) |
| ![I P Adresi Al simgesi](./media/user-guide/netx-events/image87.png)    | **IP Adresi Al** (*nx_ip_address_get*) |
| ![I P Adresi Kümesi simgesi](./media/user-guide/netx-events/image88.png)    | **IP Adresi Kümesi** (*nx_ip_address_set*) |
| ![I P Oluştur simgesi](./media/user-guide/netx-events/image89.png)    | **IP Oluşturma** (*nx_ip_create*) |
| ![I P Sil simgesi](./media/user-guide/netx-events/image90.png)    | **IP Silme** (*nx_ip_delete*) |
| ![I P Sürücüsü Doğrudan Komut simgesi](./media/user-guide/netx-events/image91.png)    | **IP Sürücüsü Doğrudan Komutu** (*nx_ip_driver_direct_command*) |
| ![I P İ iletme devre dışı bırakma simgesi](./media/user-guide/netx-events/image92.png)    | **IP IletmeYi Devre Dışı Bırakma** (*nx_ip_forwarding_disable*) |
| ![I P İ iletme etkinleştirme simgesi](./media/user-guide/netx-events/image93.png)    | **IP Iletme Etkinleştirme (** *nx_ip_forwarding_enable*) |
| ![I P Parçası Devre Dışı Bırak simgesi](./media/user-guide/netx-events/image94.png)    | **IP Parçasını Devre Dışı** Bırakma (*nx_ip_fragment_disable*) |
| ![I P Parçası Etkinleştirme simgesi](./media/user-guide/netx-events/image95.png)    | **IP Parçası Etkinleştirme** (*nx_ip_fragment_enable*)  |
| ![I P Ağ Geçidi Adres Kümesi simgesi](./media/user-guide/netx-events/image96.png)    | **IP Ağ Geçidi Adres Kümesi** (*nx_ip_gateway_address_set*) |
| ![I P Bilgileri Al simgesi](./media/user-guide/netx-events/image97.png)    | **IP Bilgileri Al** (*nx_ip_info_get*) |
| ![I P Arabirimi Ekleme simgesi](./media/user-guide/netx-events/image98.png)    | **IP Arabirimi Ekleme** (*nx_ip_interface_attach*) |
| ![I P Arabirimi Bilgileri Al simgesi](./media/user-guide/netx-events/image99.png)    | **IP Arabirimi Bilgileri Al** (*nx_ip_interface_info_get*) |
| ![I P Ham Paketi Devre Dışı Bırak simgesi](./media/user-guide/netx-events/image100.png)    | **IP Ham Paketi Devre Dışı** Bırakma (*nx_ip_raw_packet_disable*) |
| ![I P Ham Paketi Etkinleştir simgesi](./media/user-guide/netx-events/image101.png)    | **IP Ham Paket Etkinleştirme** (*nx_ip_raw_packet_enable*) |
| ![I P Ham Paket Alma simgesi](./media/user-guide/netx-events/image102.png)    | **IP Ham Paket Alma** (*nx_ip_raw_packet_receive*) |
| ![I P Ham Paket Gönderme simgesi](./media/user-guide/netx-events/image103.png)    | **IP Ham Paket Gönderme** (*nx_ip_raw_packet_send*) |
| ![I P Statik Yol Ekle simgesi](./media/user-guide/netx-events/image104.png)    | **IP Statik Yol Ekleme** (*nx_ip_static_route_add*) |
| ![I P Statik Rota Silme simgesi](./media/user-guide/netx-events/image105.png)    | **IP Statik Rota Silme** (*nx_ip_static_route_delete)* |
| ![I P Durum Denetimi simgesi](./media/user-guide/netx-events/image106.png)    | **IP Durum Denetimi** (*nx_ip_status_check*)|
| ![I PS E C Etkinleştir simgesi](./media/user-guide/netx-events/image107.png)    | **IPSEC Etkinleştirme** (*nx_ipsec_enable)* |
| ![Paket Ayırma simgesi](./media/user-guide/netx-events/image108.png)    | **Paket Ayırma** (*nx_packet_allocate*) |
| ![Paket Kopyalama simgesi](./media/user-guide/netx-events/image109.png)    | **Paket Kopyalama** (*nx_packet_copy*) |
| ![Paket Verileri Ekleme simgesi](./media/user-guide/netx-events/image110.png)    | **Paket Veri Ekleme** (*nx_packet_data_append*) |
| ![Paket Verilerini Ayıklama Uzaklık simgesi](./media/user-guide/netx-events/image111.png)    | **Paket Verileri Ayıklama Uzaklığı** (*nx_packet_data_extract_offset*) |
| ![Paket Verilerini Alma simgesi](./media/user-guide/netx-events/image112.png)    | **Paket Verilerini Alma** (*nx_packet_data_retrieve*) |
| ![Paket Uzunluğu Al simgesi](./media/user-guide/netx-events/image113.png)    | **Paket Uzunluğu Al** (*nx_packet_length_get*) |
| ![Paket Havuzu Oluştur simgesi](./media/user-guide/netx-events/image114.png)    | **Paket Havuzu Oluşturma** (*nx_packet_pool_create*) |
| ![Paket Havuzu Silme simgesi](./media/user-guide/netx-events/image115.png)    | **Paket Havuzu Silme** (*nx_packet_pool_delete*) |
| ![Paket Havuzu Bilgileri Al simgesi](./media/user-guide/netx-events/image116.png)    | **Paket Havuzu Bilgilerini Al** (*nx_packet_pool_info_get*) |
| ![Paket Sürümü simgesi](./media/user-guide/netx-events/image117.png)    | **Paket Sürümü** (*nx_packet_release*) |
| ![Paket İletme Sürümü simgesi](./media/user-guide/netx-events/image118.png)    | **Paket İletme Sürümü** (*nx_packet_transmit_release*) |
| ![R A R P Devre Dışı Bırak simgesi](./media/user-guide/netx-events/image119.png)    | **RARP Devre Dışı** Bırakma (*nx_rarp_disable*) |
| ![R A R P Etkinleştir simgesi](./media/user-guide/netx-events/image120.png)    | **RARP Etkinleştirme** (*nx_rarp_enable*) |
| ![R A R P Bilgileri Al simgesi](./media/user-guide/netx-events/image121.png)    | **RARP Bilgi Al** (*nx_rarp_info_get*) |
| ![Sistem Başlatma simgesi](./media/user-guide/netx-events/image122.png)    | **Sistem Başlatma** (*nx_system_initialize*) |
| ![T C P İstemci Yuvası Bağlama simgesi](./media/user-guide/netx-events/image123.png)    | **TCP İstemci Yuva Bağlaması** (*nx_tcp_client_socket_bind*) |
| ![T C P İstemci Yuvası Bağlan simgesi](./media/user-guide/netx-events/image124.png)    | **TCP İstemci Yuvası Bağlan** (*nx_tcp_client_socket_connect*) |
| ![T C P İstemci Yuvası Bağlantı Noktası Al simgesi](./media/user-guide/netx-events/image125.png)    | **TCP İstemci Yuvası Bağlantı Noktası Al** (*nx_tcp_client_socket_port_get*) |
| ![T C P İstemci Yuvası Bağlantıdan Çıkar simgesi](./media/user-guide/netx-events/image126.png)    | **TCP İstemci Yuvası BağlantıDan Çıkar** (*nx_tcp_client_socket_unbind*) |
| ![T C P Etkinleştir simgesi](./media/user-guide/netx-events/image127.png)    | **TCP Etkinleştirme** (*nx_tcp_enable*) |
| ![T C P Ücretsiz Bağlantı Noktası Bul simgesi](./media/user-guide/netx-events/image128.png)    | **TCP Ücretsiz Bağlantı Noktası Bulma** (*nx_tcp_free_port_find*) |
| ![T C P Bilgileri Al simgesi](./media/user-guide/netx-events/image129.png)    | **TCP Bilgileri Al** (*nx_tcp_info_get*) |
| ![T C P Sunucu Yuvası Kabul Et simgesi](./media/user-guide/netx-events/image130.png)    | **TCP Sunucu Yuvası Kabul Etme** (*nx_tcp_server_socket_accept*) |
| ![T C P Sunucu Yuvası Dinleme simgesi](./media/user-guide/netx-events/image131.png)    | **TCP Sunucu Yuvası Dinleme** (*nx_tcp_server_socket_listen*) |
| ![T C P Sunucu Yuvası Yeniden Listele simgesi](./media/user-guide/netx-events/image132.png)    | **TCP Sunucusu Yuva Listesi** (*nx_tcp_server_socket_relisten*) |
| ![T C P Sunucu Yuvası Kabul Etme simgesi](./media/user-guide/netx-events/image133.png)    | **TCP Sunucu Yuvası Kabul Değil** (*nx_tcp_server_socket_unaccept*) |
| ![T C P Sunucu Yuvası Listeden Çıkar simgesi](./media/user-guide/netx-events/image134.png)    | **TCP Sunucu Yuvası Listeden Çıkar** (*nx_tcp_server_socket_unlisten*) |
| ![T C P Yuva Bayt Sayısı Kullanılabilir simgesi](./media/user-guide/netx-events/image135.png)    | **TCP Yuva BaytLarı Kullanılabilir** (*nx_tcp_socket_bytes_available*) |
| ![T C P Yuva Oluştur simgesi](./media/user-guide/netx-events/image136.png)    | **TCP Yuva Oluşturma** (*nx_tcp_socket_create*) |
| ![T C P Yuva Silme simgesi](./media/user-guide/netx-events/image137.png)    | **TCP Yuva Silme** (*nx_tcp_socket_delete*) |
| ![T C P Yuva Bağlantısını Kes simgesi](./media/user-guide/netx-events/image138.png)    | **TCP Yuvası Bağlantısını** Kesme (*nx_tcp_socket_disconnect*) |
| ![T C P Yuva Bilgileri Al simgesi](./media/user-guide/netx-events/image139.png)    | **TCP Yuva Bilgilerini Al** (*nx_tcp_socket_info_get*) |
| ![T C P Yuva MSS Al simgesi](./media/user-guide/netx-events/image140.png)    | **TCP Yuvası MSS Get** (*nx_tcp_socket_mss_get*) |
| ![T C P Yuva MSS Eş Al simgesi](./media/user-guide/netx-events/image141.png)    | **TCP Yuvası MSS Eş Alı** (*nx_tcp_socket_mss_peer_get*) |
| ![T C P Yuva MSS Kümesi simgesi](./media/user-guide/netx-events/image142.png)    | **TCP Yuvası MSS Kümesi** (*nx_tcp_socket_mss_set*) |
| ![T C P Yuva Eş Bilgileri Al simgesi](./media/user-guide/netx-events/image143.png)    | **TCP Yuva Eş Bilgileri Al** (*nx_tcp_socket_peer_info_get*) |
| ![T C P Yuva Alma simgesi](./media/user-guide/netx-events/image144.png)    | **TCP Yuva Alma** (*nx_tcp_socket_receive*) |
| ![T C P Yuva Alma Bildirimi simgesi](./media/user-guide/netx-events/image145.png)    | **TCP Yuvası Alma Bildirimi** (*nx_tcp_socket_receive_notify*) |
| ![T C P Yuva Gönderme simgesi](./media/user-guide/netx-events/image146.png)    | **TCP Yuva Gönderme** (*nx_tcp_socket_send*) |
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
- Bilgi Alanı 3: Paket işaretçisi
- Bilgi Alanı 4: ICMP üst bilgisinin Word 0'sı

### <a name="internal-igmp-receive"></a>İç IGMP Alma 

#### <a name="internal-igmp-receive"></a>İç IGMP alma

**Simge** ![ İç I G M P alma simgesi](./media/user-guide/netx-events/image7.png)

**Açıklama**

Bu olay bir iç NetX IGMP alma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP İşaretçisi
- Bilgi Alanı 2: Kaynak IP adresi
- Bilgi Alanı 3: Paket işaretçisi
- Bilgi Alanı 4: IGMP üst bilgisinin Word 0'sı

### <a name="internal-ip-receive"></a>İç IP Alma 

#### <a name="internal-ip-receive"></a>İç IP alma

**Simge** ![ İç I P alma simgesi](./media/user-guide/netx-events/image8.png)

**Açıklama**

Bu olay bir iç NetX IP alma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kaynak IP adresi
- Bilgi Alanı 3: Paket işaretçisi
- Bilgi Alanı 4: Paket uzunluğu

### <a name="internal-ip-send"></a>İç IP Gönderme

#### <a name="internal-ip-send"></a>İç IP gönderme

**Simge** ![ İç I P gönderme simgesi](./media/user-guide/netx-events/image9.png)

**Açıklama**

Bu olay bir iç NetX IP gönderme olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Hedef IP adresi
- Bilgi Alanı 3: Paket işaretçisi
- Bilgi Alanı 4: Paket uzunluğu

### <a name="internal-tcp-data-receive"></a>İç TCP Verileri Alma 

#### <a name="internal-tcp-data-receive"></a>İç TCP Verileri Alma

**Simge** ![ İç T C P verileri alma simgesi](./media/user-guide/netx-events/image10.png)

**Açıklama**

Bu olay bir iç NetX TCP veri alma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kaynak IP adresi
- Bilgi Alanı 3: Paket işaretçisi
- Bilgi Alanı 4: Alma sırası numarası

### <a name="internal-tcp-data-send"></a>İç TCP veri gönderme 

#### <a name="internal-tcp-data-send"></a>İç TCP Veri Gönderme

**Simge** ![ İç T C P veri gönderme simgesi](./media/user-guide/netx-events/image11.png)

**Açıklama**

Bu olay bir iç NetX TCP veri gönderme olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Paket işaretçisi
- Bilgi Alanı 4: Sıra numarasını iletme

### <a name="internal-tcp-fin-receive"></a>İç TCP FIN Alma 

#### <a name="internal-tcp-fin-receive"></a>İç TCP fin alma

**Simge** ![ İç T C P F I N alma simgesi](./media/user-guide/netx-events/image12.png)

**Açıklama**

Bu olay bir iç NetX TCP FIN alma olayı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Paket işaretçisi
- Bilgi Alanı 4: Alma sırası numarası

### <a name="internal-tcp-fin-send"></a>İç TCP FIN Gönderme 

#### <a name="internal-tcp-fin-send"></a>İç TCP fin gönderme

**Simge** ![ İç T C P F I N gönderme simgesi](./media/user-guide/netx-events/image13.png)

**Açıklama**

Bu olay bir iç NetX TCP FIN gönderme olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Paket işaretçisi
- Bilgi Alanı 4:Sıra numarasını iletme

### <a name="internal-tcp-rst-receive"></a>İç TCP RST Alma 

#### <a name="internal-tcp-rst-receive"></a>İç TCP RST alma

**Simge** ![ İç T C P R S T alma simgesi](./media/user-guide/netx-events/image14.png)

**Açıklama**

Bu olay bir iç NetX TCP sıfırlama alma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi.
- Bilgi Alanı 2: Yuva işaretçisi.
- Bilgi Alanı 3: Paket işaretçisi.
- Bilgi Alanı 4: Sıra numarasını alma.

### <a name="internal-tcp-rst-send"></a>İç TCP RST Gönderme 

#### <a name="internal-tcp-rst-send"></a>İç TCP RST gönderme

**Simge** ![ İç T C P R S T gönderme simgesi](./media/user-guide/netx-events/image15.png)

**Açıklama**

Bu olay bir iç NetX TCP sıfırlama gönderme olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Paket işaretçisi
- Bilgi Alanı 4: Sıra numarasını iletme

### <a name="internal-tcp-syn-receive"></a>İç TCP SYN Alma 

#### <a name="internal-tcp-syn-receive"></a>İç TCP SYN alma

**Simge** ![ İç T C P S Y N alma simgesi](./media/user-guide/netx-events/image16.png)

**Açıklama**

Bu olay bir iç NetX TCP SYN alma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Yuva işaretçisi
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
- Bilgi Alanı 4: Kullanılmadı.

### <a name="internal-io-driver-link-disable"></a>İç I/O Sürücü Bağlantısını Devre Dışı Bırakma 

#### <a name="internal-io-driver-link-disable"></a>İç işletim sistemi sürücü bağlantısını devre dışı bırakma

**Simge** ![ İç I/O sürücüsü bağlantısı devre dışı bırakma simgesi](./media/user-guide/netx-events/image27.png)

**Açıklama**

Bu olay iç NetX I/O sürücü bağlantısı devre dışı bırakma olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="internal-io-driver-packet-broadcast"></a>İç I/O Sürücü Paketi Yayını 

#### <a name="internal-io-driver-packet-broadcast"></a>İç I/O sürücü paketi yayını

**Simge** ![ İç I/ O sürücü paketi yayın simgesi](./media/user-guide/netx-events/image28.png)

**Açıklama**

Bu olay bir iç NetX I/O sürücü paketi yayın olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Paket işaretçisi
- Bilgi Alanı 3: Paket boyutu
- Bilgi Alanı 4: Kullanılmadı

### <a name="internal-io-driver-arp-send"></a>İç G/Ç Sürücüsü ARP Gönderme 

#### <a name="internal-io-driver-arp-send"></a>İç G/Ç sürücüsü ARP gönderme

**Simge** ![ İç G/Ç sürücüsü ARP gönderme simgesi](./media/user-guide/netx-events/image29.png)

**Açıklama**

Bu olay bir iç NetX G/Ç sürücüsü ARP gönderme olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Paket işaretçisi
- Bilgi Alanı 3: Paket boyutu
- Bilgi Alanı 4: Kullanılmadı

### <a name="internal-io-driver-arp-response-send"></a>İç G/Ç Sürücüsü ARP Yanıt Gönderme 

#### <a name="internal-io-driver-arp-response-send"></a>İç G/Ç sürücüsü ARP yanıt gönderme

**Simge** ![ İç G/Ç sürücüsü ARP yanıtı gönderme simgesi](./media/user-guide/netx-events/image30.png)

**Açıklama**

Bu olay iç NetX G/Ç sürücüsü ARP yanıt gönderme olayını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Paket işaretçisi
- Bilgi Alanı 3: Paket boyutu
- Bilgi Alanı 4: Kullanılmadı

### <a name="internal-io-driver-rarp-send"></a>İç G/Ç Sürücüsü RARP Gönderme 

#### <a name="internal-io-driver-rarp-send"></a>İç G/Ç sürücüsü RARP gönderme

**Simge** ![ İç G/Ç sürücüsü RARP gönderme simgesi](./media/user-guide/netx-events/image31.png)

**Açıklama**

Bu olay bir iç NetX G/Ç sürücüsü RARP gönderme olayı temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Paket işaretçisi
- Bilgi Alanı 3: Paket boyutu
- Bilgi Alanı 4: Kullanılmadı

### <a name="internal-io-driver-multicast-join"></a>İç I/O Sürücüsü Çok Noktaya Yayına Katılma 

#### <a name="internal-io-driver-multicast-join"></a>İç I/O sürücüsü çok noktaya yayın birleştirme

**Simge** ![ İç I/O sürücüsü çok noktaya yayın birleştirme simgesi](./media/user-guide/netx-events/image32.png)

**Açıklama**

Bu olay bir iç NetX I/O sürücüsü çok noktaya yayın birleştirme olayı temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="internal-io-driver-multicast-leave"></a>İç I/O Sürücüsü Çok Noktaya Yayın Bırakma 

#### <a name="internal-io-driver-multicast-leave"></a>İç I/O sürücüsü çok noktaya yayın bırakma

**Simge** ![ İç I/O sürücüsü çok noktaya yayın bırakma simgesi](./media/user-guide/netx-events/image33.png)

**Açıklama**

Bu olay bir iç NetX I/O sürücüsü çok noktaya yayın bırakma olayıdır.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="internal-io-driver-get-status"></a>İç I/O Sürücüsü Durumu Al 

#### <a name="internal-io-driver-get-status"></a>İç I/O sürücüsünün durumu

**Simge** ![ İç I/ O sürücüsü durum al simgesi](./media/user-guide/netx-events/image34.png)

**Açıklama**

Bu olay iç NetX I/O sürücüsünün durum durumunu al olaylarını temsil eder.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="internal-io-driver-get-speed"></a>İç I/O Sürücüsü Hız Al 

#### <a name="internal-io-driver-get-speed"></a>İç I/O sürücüsü hız elde ediyor

**Simge** ![ İç I/ O sürücüsü hız al simgesi](./media/user-guide/netx-events/image35.png)

**Açıklama**

Bu olay iç NetX I/O sürücüsünün hız olayına sahip olduğunu gösterir.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="internal-io-driver-get-duplex-type"></a>İç I/O Sürücüsü Çift Yönlü Türü Al 

#### <a name="internal-io-driver-get-duplex-type"></a>İç I/O sürücüsü çift yönlü türe sahip

**Simge** ![ İç I/O sürücüsü çift yönlü tür al simgesi](./media/user-guide/netx-events/image36.png)

**Açıklama**

Bu olay, iç NetX I/O sürücüsünün çift yönlü tür olaylarını temsil eder.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
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
- Bilgi Alanı 4: Kullanılmadı

### <a name="arp-hardware-address-find"></a>ARP Donanım Adresi Bulma 

#### <a name="nx_arp_hardware_address_find"></a>nx_arp_hardware_address_find

**Simge** ![ R P Donanım Adresi Bul simgesi](./media/user-guide/netx-events/image47.png)

**Açıklama**

Bu olay, sanal ağ üzerinden fiziksel bir nx_arp_hardware_address_find.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: IP adresi
- Bilgi Alanı 3: Fiziksel adres (MSW)
- Bilgi Alanı 4: Fiziksel adres (LSW)

### <a name="arp-information-get"></a>ARP Bilgileri Al 

#### <a name="nx_arp_info_get"></a>nx_arp_info_get

**Simge** ![ R P bilgi al simgesi](./media/user-guide/netx-events/image48.png)

**Açıklama**

Bu olay, bilgi alma bilgilerini nx_arp_info_get.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: APS gönderildi
- Bilgi Alanı 3: ARP yanıtları
- Bilgi Alanı 4: APS alındı

### <a name="arp-ip-address-find"></a>ARP IP Adresi Bulma 

#### <a name="nx_arp_ip_address_find"></a>nx_arp_ip_address_find

**Simge** ![ R P I P adresi bulma simgesi](./media/user-guide/netx-events/image49.png)

**Açıklama**

Bu olay, sanal ağ üzerinden sağlanan fiziksel adresle ilişkili bir IP nx_arp_ip_address_find.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: IP adresi
- Bilgi Alanı 3: Fiziksel adres (MSW)
- Bilgi Alanı 4: Fiziksel adres (LSW)

### <a name="arp-static-entry-create"></a>ARP Statik Giriş Oluşturma 

#### <a name="nx_arp_static_entry_create"></a>nx_arp_static_entry_create

**Simge** ![ R P statik giriş oluşturma simgesi](./media/user-guide/netx-events/image50.png)

**Açıklama**

Bu olay, nx_arp_static_entry_create aracılığıyla statik ARP girişi oluşturmayı nx_arp_static_entry_create.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: IP adresi
- Bilgi Alanı 3: Fiziksel adres (MSW)
- Bilgi Alanı 4: Fiziksel adres (LSW)

### <a name="arp-static-entries-delete"></a>ARP Statik Girdileri Silme 

#### <a name="nx_arp_static_entries_delete"></a>nx_arp_static_entries_delete

**Simge** ![ R P statik girişleri silme simgesi](./media/user-guide/netx-events/image51.png)

**Açıklama**

Bu olay, tüm ARP statik girişlerinin kaynak aracılığıyla silinmesini nx_arp_static_entries_delete.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Girişler silindi
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="arp-static-entry-delete"></a>ARP Statik Giriş Silme 

### <a name="nx_arp_static_entry_delete"></a>nx_arp_static_entry_delete

**Simge** ![ R P statik giriş silme simgesi](./media/user-guide/netx-events/image52.png)

**Açıklama**

Bu olay, bir statik ARP girişinin nx_arp_static_entry_delete.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: IP adresi
- Bilgi Alanı 3: Fiziksel adres (MSW)
- Bilgi Alanı 4: Fiziksel adres (LSW)

### <a name="duo-cache-entry-delete"></a>Duo Cache Girişi Silme 

#### <a name="nxd_und_cache_entry_delete"></a>nxd_und_cache_entry_delete

**Simge** ![ Duo cache girişi silme simgesi](./media/user-guide/netx-events/image53.png)

**Açıklama**

Bu olay, komşu önbellek tablosunda yer alan bir girişin nx_udp_socket_create.

**Bilgi Alanları** 

- Bilgi Alanı 1: Silinecek IPv6 bağlantısı yerel adresinin dördüncü (en az önemli) sözcüğü
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-cache-entry-set"></a>Duo Cache Giriş Kümesi 

#### <a name="nxd_nd_cache_entry_set"></a>nxd_nd_cache_entry_set

**Simge** ![ Duo cache giriş kümesi simgesi](./media/user-guide/netx-events/image54.png)

**Açıklama**

Bu olay, önbellek girişi oluşturmayı ve bu giriş aracılığıyla komşu önbellek tablosuna eklemeyi nxd_nd_cache_entry_set.

**Bilgi Alanları** 

- Bilgi Alanı 1: Eklemek için IPv6 adresinin dördüncü (en az önemli) sözcüğü
- Bilgi Alanı 2: Fiziksel adres msb
- Bilgi Alanı 3: Fiziksel adres lsb
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-cache-invalidate"></a>Duo Cache Invalidate 

#### <a name="nxd_nd_cache_invalidate"></a>nxd_nd_cache_invalidate

**Simge** ![ Duo cache invalidate simgesi](./media/user-guide/netx-events/image55.png)

**Açıklama**

Bu olay, tüm komşu önbellek tablolarının geçersiz kılınarak yeni bir nxd_nd_cache_invalidate.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-cache-ip-address-find"></a>Duo Önbelleği IP Adresi Bulma 

#### <a name="nxd_nd_cache_ip_address_find"></a>nxd_nd_cache_ip_address_find

**Simge** ![ Duo cache I P adresi bulma simgesi](./media/user-guide/netx-events/image56.png)

**Açıklama**

Bu olay, önbellek tablosundan sağlanan fiziksel adresle eşleşen bir IP adresinin bu adresle eş nxd_nd_cache_ip_address_find.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: IPv6 adresinin dördüncü (en az önemli) sözcüğü
- Bilgi Alanı 3: Fiziksel adres msb
- Bilgi Alanı 4: Fiziksel adres lsb

### <a name="duo-icmp-enable"></a>Duo ICMP Etkinleştirme 

#### <a name="nxd_icmp_enable"></a>nxd_icmp_enable

**Simge** ![ Duo I C M P enable simgesi](./media/user-guide/netx-events/image57.png)

**Açıklama**

Bu olay, belirtilen IP örneğinde etkin olan ICMPv4 ve ICMPv6 hizmetlerini nxd_icmp_enable.

**Bilgi Alanları**
- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-icmp-ping"></a>Duo ICMP Ping 

#### <a name="nxd_icmp_ping"></a>nxd_icmp_ping

**Simge** ![ Duo I C M P ping simgesi](./media/user-guide/netx-events/image58.png)

**Açıklama**

Bu olay, IPv6 ana bilgisayar üzerinden bir ping (yankı isteği) göndermeyi nxd_icmp_ping.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: IPv6 adresi
- Bilgi Alanı 3: Yankı verileri işaretçisi
- Bilgi Alanı 4: Yankı verisi boyutu

### <a name="duo-ip-max-payload-size-find"></a>Duo IP Maksimum Yük Boyutu Bul 

#### <a name="nxd_ip_max_payload_size"></a>nxd_ip_max_payload_size

**Simge** ![ Duo I P maksimum yük boyutu bul simgesi](./media/user-guide/netx-events/image59.png)

**Açıklama**

Bu olay, belirtilen paketin parçalanmasına gerek kalmadan taşıy kapasitesi üst limiti hesaplar.

**Bilgi Alanları**

- Bilgi Alanı 1: Yuva işaretçisi
- Bilgi Alanı 2: Eş IP adresi
- Bilgi Alanı 3: Eş bağlantı noktası Bilgi Alanı 4: Kullanılmadı

### <a name="duo-ip-raw-packet-send"></a>Duo IP Ham Paket Gönderme 

#### <a name="nxd_ip_max_packet_send"></a>nxd_ip_max_packet_send

**Simge** ![ Duo I P ham paket gönderme simgesi](./media/user-guide/netx-events/image60.png)

**Açıklama**

Bu olay, belirtilen ağ arabiriminden sağlanan IP hedef adresine bir ham IP paketinin nxd_ip_raw_packet_send.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Göndermek için paket işaretçisi
- Bilgi Alanı 3: Hedef adres işaretçisi
- Bilgi Alanı 4: Paket protokolü

### <a name="duo-ipv6-default-router-add"></a>Duo IPv6 Varsayılan Yönlendirici Ekleme 

#### <a name="nxd_ipv6_default_router_add"></a>nxd_ipv6_default_router_add

**Simge** ![ Duo I P v 6 varsayılan yönlendirici ekleme simgesi](./media/user-guide/netx-events/image61.png)

**Açıklama**

Bu olay, IP örneğinin IPv6 yönlendirme tablosuna bir varsayılan yönlendirici eklemeyi nxd_ipv6_default_router_add.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi.
- Bilgi Alanı 2: Hedef Ağ adresi.
- Bilgi Alanı 3: Yaşam süresi bilgileri.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="duo-ipv6-default-router-delete"></a>Duo IPv6 Varsayılan Yönlendirici Silme 

#### <a name="nxd_ipv6_default_router_delete"></a>nxd_ipv6_default_router_delete

**Simge** ![ Duo I P v 6 varsayılan yönlendirici silme simgesi](./media/user-guide/netx-events/image62.png)

**Açıklama**

Bu olay, ip örneği IPv6 yönlendirme tablosundan bir varsayılan yönlendiricinin ip adresi üzerinden kaldırılmasını nxd_ipv6_default_router_delete.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi.
- Bilgi Alanı 2: Varsayılan yönlendirici IPv6 adresinin dördüncü sözcüğü (en az önemli).
- Bilgi Alanı 3: Kullanılmaz.
- Bilgi Alanı 4: Kullanılmadı.

### <a name="duo-ipv6-enable"></a>Duo IPv6 Etkinleştirme 

#### <a name="nxd_ipv6_enable"></a>nxd_ipv6_enable

**Simge** ![ Duo I P v 6 enable simgesi](./media/user-guide/netx-events/image63.png)

**Açıklama**

Bu olay, sağlanan IP örneğinde IPv6 hizmetlerini etkinleştirmeyi temsil eder ve nxd_ipv6_enable.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-ipv6-global-address-get"></a>Duo IPv6 Genel Adres Al 

#### <a name="nxd_ipv6_global_address_get"></a>nxd_ipv6_global_address_get

**Simge** ![ Duo I P v 6 genel adres al simgesi](./media/user-guide/netx-events/image64.png)

**Açıklama**

Bu olay, ip örneği arabirim tablosunda dizin 1'de yer alan IP örneğinde genel (birincil) IP adresinin, ip adresi üzerinden alınması nxd_ipv6_global_address_get.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi.
- Bilgi Alanı 2: Genel adresin dördüncü sözcüğü (en az önemli)
- Bilgi Alanı 3: IPv6 adres ön eki uzunluğu.
- Bilgi Alanı 4: IP arabirimi tablosuna dizinleme (1).

### <a name="duo-ipv6-global-address-set"></a>Duo IPv6 Genel Adres Kümesi 

#### <a name="nxd_ipv6_global_address_set"></a>nxd_ipv6_global_address_set

**Simge** ![ Duo I P v 6 genel adres kümesi simgesi](./media/user-guide/netx-events/image65.png)

**Açıklama**

Bu olay, ip örneği arabirim tablosunda dizin 1'de bulunan IP örneğinde genel (birincil) IP adresinin ip adresi olarak nxd_ipv6_global_address_set.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Genel adresin dördüncü sözcüğü (en az önemli)
- Bilgi Alanı 3: IPv6 adres ön eki uzunluğu
- Bilgi Alanı 4: IP arabirimi tablosuna dizinleme (1)

### <a name="duo-ipv6-initiate-dad-process"></a>Duo IPv6 İşleme Başlatma 

#### <a name="nxd_ipv6_initiate_dad_process"></a>nxd_ipv6_initiate_dad_process

**Simge** ![ Duo I P v 6 başlatma işlemi simgesi](./media/user-guide/netx-events/image66.png)

**Açıklama**

Bu olay, IP örneğine yerel bağlantı atandığı zaman Yinelenen Adres Algılama (TAMAM) işleminin başlangıcını veya ip arabirimi adresi nxd_ipv6_initiate_dad_process.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-ipv6-interface-address-get"></a>Duo IPv6 Arabirim Adresi Al 

#### <a name="nxd_ipv6_interface_address_get"></a>nxd_ipv6_interface_address_get

**Simge** ![ Duo I P v 6 arabirim adresi get simgesi](./media/user-guide/netx-events/image67.png)

**Açıklama**

Bu olay, ip adresi ve ön ekin belirtilen dizinde IP örneği arabirim adresi tablosuna alınmasıyla ilgili bilgileri nxd_ipv6_interface_address_get.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: İade etmek için IPv6 adresinin dördüncü sözcüğü (en az önemli)
- Bilgi Alanı 4: IP örneği arabirim tablosuna arabirim dizini

### <a name="duo-ipv6-interface-address-set"></a>Duo IPv6 Arabirim Adres Kümesi 

### <a name="nxd_ipv6_interface_address_set"></a>nxd_ipv6_interface_address_set

**Simge** ![ Duo I P v 6 arabirim adresleri et simgesi](./media/user-guide/netx-events/image68.png)

**Açıklama**

Bu olay, belirtilen dizinde IP adresinin ve ön ekin IP örneği arabirim adresi tablosuna ayar ayarlamayı temsil eder. Sıfır dizininde (yerel adresi bağlama) izin ver nxd_ipv6_interface_address_set.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: İade etmek için IPv6 adresinin dördüncü sözcüğü (en az önemli)
- Bilgi Alanı 3: Ön ek uzunluğu
- Bilgi Alanı 4: IP örneği arabirim tablosuna arabirim dizini

### <a name="duo-ipv6-link-local-address-get"></a>Duo IPv6 Bağlantı Yerel Adresi Al 

#### <a name="nxd_ipv6_linklocal_address_get"></a>nxd_ipv6_linklocal_address_get

**Simge** ![ Duo I P v 6 bağlantı yerel adresi al simgesi](./media/user-guide/netx-events/image69.png)

**Açıklama**

Bu olay, belirtilen IP örneğinin bağlantı yerel adresinin ağ üzerinden alınması nxd_ipv6_linklocal_address_get.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: IP v6 bağlantı yerel adresinin dördüncü sözcüğü (en az önemli)
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-ipv6-link-local-address-set"></a>Duo IPv6 Link Yerel Adres Kümesi 

#### <a name="nxd_ipv6_linklocal_address_set"></a>nxd_ipv6_linklocal_address_set

**Simge** ![ Duo I P v 6 bağlantı yerel adres kümesi simgesi](./media/user-guide/netx-events/image70.png)

**Açıklama**

Bu olay, ip örneğinin bağlantı yerel adresinin ip adresi olarak nxd_ipv6_linklocal_address_set.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: IPv6 bağlantısı yerel adresinin dördüncü (en az önemli) sözcüğü
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-ipv6-raw-packet-send"></a>Duo IPv6 Ham Paket Gönderme 

#### <a name="nxd_ipv6_raw_packet_send"></a>nxd_ipv6_raw_packet_send

**Simge** ![ Duo I P v 6 ham paket gönderme simgesi](./media/user-guide/netx-events/image71.png)

**Açıklama**

Bu olay, birincil IP arabirimi aracılığıyla verimsiz hedefe bir ham IP paketinin nxd_ip_raw_packet_send.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Göndermek için paket işaretçisi
- Bilgi Alanı 3: Hedef IP adresi
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-tcp-socket-peer-info-get"></a>Duo TCP Yuva Eş Bilgisi Al 

#### <a name="nxd_tcp_socket_peer_info_get"></a>nxd_tcp_socket_peer_info_get

**Simge** ![ Duo T C P yuva eş bilgisi get simgesi](./media/user-guide/netx-events/image72.png)

**Açıklama**

Bu olay, belirtilen yuvada alınan bir TCP paketinden gönderen verilerini ayıklar. Gönderenin IP adresini ve bağlantı noktasını döndürür.

**Bilgi Alanları**

- Bilgi Alanı 1: Yuva işaretçisi
- Bilgi Alanı 2: Eş IP adresi
- Bilgi Alanı 3: Eş bağlantı noktası
- Bilgi Alanı 4: IP adresinin önemli 32 bit kirası

### <a name="duo-tcp-socket-set-interface"></a>Duo TCP Yuva Kümesi Arabirimi 

#### <a name="nxd_tcp_socket_set_interface"></a>nxd_tcp_socket_set_interface

**Simge** ![ Duo T C P yuva kümesi arabirimi simgesi](./media/user-guide/netx-events/image73.png)

**Açıklama**

Bu olay, istemci belirtilen sunucu IP adresi üzerinde bir TCP sunucusu ile bağlantı kurmanın ardından giden yuva arabiriminin ayar nxd_tcp_client_socket_connect.

**Bilgi Alanları** 

- Bilgi Alanı 1: TCP Yuvası İşaretçisi
- Bilgi Alanı 2: Arabirim Kimliği
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-udp-socket-send"></a>Duo UDP Yuva Gönderme 

#### <a name="nxd_udp_socket_send"></a>nxd_udp_socket_send

**Simge** ![ Duo U D P yuva gönderme simgesi](./media/user-guide/netx-events/image74.png)

**Açıklama**

Bu olay, giriş IP adresi ve bağlantı noktası ile belirtilen yuva üzerinden bir UDP paketi göndermeyi temsil eder ve nxd_udp_socket_send.

**Bilgi Alanları** 

- Bilgi Alanı 1: İşaretçi UDP Yuvası
- Bilgi Alanı 2: UDP paketi işaretçisi
- Bilgi Alanı 3: Paket uzunluğu
- Bilgi Alanı 4: Kullanılmadı


### <a name="duo-udp-socket-set-interface"></a>Duo UDP Yuva Kümesi Arabirimi 

#### <a name="nxd_udp_socket_set_interface"></a>nxd_udp_socket_set_interface

**Simge** ![ Duo U D P yuva kümesi arabirim simgesi](./media/user-guide/netx-events/image75.png)

**Açıklama**

Bu olay, belirtilen UDP yuva giden arabiriminin, ağ üzerinden giriş arabirimi kimliğine karşılık gelen arabirime nxd_udp_socket_set_interface.

**Bilgi Alanları** 

- Bilgi Alanı 1: UDP Yuvası İşaretçisi
- Bilgi Alanı 2: Arabirim Kimliği
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="duo-udp-source-extract"></a>Duo UDP Kaynak Ayıklama 

#### <a name="nxd_udp_socket_extract"></a>nxd_udp_socket_extract

**Simge** ![ Duo U D P kaynak ayıklama simgesi](./media/user-guide/netx-events/image76.png)

**Açıklama**

Bu olay, alınan bir paketin (IPv4 veya IPv6) IP adresini ve kaynak bağlantı noktasını ayıklamayı temsil eder. IPv6 ise, IP adresinin dördüncü sözcüğü (en az önemli) ip adresi nxd_udp_source_extract.

**Bilgi Alanları**

- Bilgi Alanı 1: Paketin işaretçisi
- Bilgi Alanı 2: IP sürümü
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
- Bilgi Alanı 3: Ek bilgi işaretçisi
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-address-get"></a>IP Adresi Al 

#### <a name="nx_ip_address_get"></a>nx_ip_address_get

**Simge** ![ I P adresi get simgesi](./media/user-guide/netx-events/image87.png)

**Açıklama**

Bu olay, ip adresinin ip adresi üzerinden nx_ip_address_get.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: IP adresi
- Bilgi Alanı 3: Ağ maskesi
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-address-set"></a>IP Adresi Kümesi 

#### <a name="nx_ip_address_set"></a>nx_ip_address_set

**Simge** ![ I P adresi kümesi simgesi](./media/user-guide/netx-events/image88.png)

**Açıklama**

Bu olay IP adresinin ip adresi olarak nx_ip_address_set.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: IP adresi
- Bilgi Alanı 3: Ağ maskesi
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-create"></a>IP Oluşturma 

#### <a name="nx_ip_create"></a>nx_ip_create

**Simge** ![ I P oluşturma simgesi](./media/user-guide/netx-events/image89.png)

**Açıklama**

Bu olay, ip örneği oluşturmak için nx_ip_create.

**Bilgi Alanları** 
- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: IP adresi
- Bilgi Alanı 3: Ağ maskesi
- Bilgi Alanı 4: Varsayılan paket havuzu işaretçisi

### <a name="ip-delete"></a>IP Silme 

#### <a name="nx_ip_delete"></a>nx_ip_delete

**Simge** ![ I P silme simgesi](./media/user-guide/netx-events/image90.png)

**Açıklama**

Bu olay, ip örneği silmeyi nx_ip_delete.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-driver-direct-command"></a>IP Sürücüsü Doğrudan Komutu 

#### <a name="nx_ip_driver_direct_command"></a>nx_ip_driver_direct_command

**Simge** ![ I P sürücüsü doğrudan komut simgesi](./media/user-guide/netx-events/image91.png)

**Açıklama**

Bu olay, komut satırı aracılığıyla doğrudan bir I/O nx_ip_driver_direct_command.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Sürücü komutu
- Bilgi Alanı 3: Dönüş değeri
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-forwarding-disable"></a>IP Iletmeyi Devre Dışı Bırakma 

#### <a name="nx_ip_forwarding_disable"></a>nx_ip_forwarding_disable

**Simge** ![ I P iletme devre dışı bırakma simgesi](./media/user-guide/netx-events/image92.png)

**Açıklama**

Bu olay, ip iletmeyi ip üzerinden devre dışı nx_ip_forwarding_disable.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-forwarding-enable"></a>IP IletmeYi Etkinleştirme 

#### <a name="nx_ip_forwarding_enable"></a>nx_ip_forwarding_enable

**Simge** ![ I P iletme etkinleştirme simgesi](./media/user-guide/netx-events/image93.png)

**Açıklama**

Bu olay, ip iletmeyi ağ üzerinden etkinleştirmeyi nx_ip_forwarding_enable.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-fragment-disable"></a>IP Parçasını Devre Dışı Bırakma 

#### <a name="nx_ip_fragment_disable"></a>nx_ip_fragment_disable

**Simge** ![ I P parçası devre dışı bırakma simgesi](./media/user-guide/netx-events/image94.png)

**Açıklama**

Bu olay, ip parçalanması sırasında ip parçalanmanın devre dışı nx_ip_fragment_disable.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-fragment-enable"></a>IP Parçası Etkinleştirme 

#### <a name="nx_ip_fragment_enable"></a>nx_ip_fragment_enable

**Simge** ![ I P parçası etkinleştirme simgesi](./media/user-guide/netx-events/image95.png)

**Açıklama**

Bu olay, ip parçalanmasına izin veri nx_ip_fragment_enable.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-gateway-address-set"></a>IP Ağ Geçidi Adres Kümesi 

#### <a name="nx_ip_gateway_address_set"></a>nx_ip_gateway_address_set

**Simge** ![ I P ağ geçidi adres kümesi simgesi](./media/user-guide/netx-events/image96.png)

**Açıklama**

Bu olay, ağ geçidi IP adresinin ağ geçidi ip adresi nx_ip_gateway_address_set.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Ağ geçidi IP adresi
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-information-get"></a>IP Bilgileri Al 

#### <a name="nx_ip_info_get"></a>nx_ip_info_get

**Simge** ![ I P bilgileri al simgesi](./media/user-guide/netx-events/image97.png)

**Açıklama** Bu olay, ip bilgilerini nx_ip_info_get.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Gönderilen IP baytları
- Bilgi Alanı 3: ALıNAN IP bayt sayısı
- Bilgi Alanı 4: BıRAKıLAN IP paketleri

### <a name="ip-interface-attach"></a>IP Arabirimi Ekleme 

#### <a name="nx_interface_attach"></a>nx_interface_attach

**Simge** ![ I P iterface attach simgesi](./media/user-guide/netx-events/image98.png)

**Açıklama**

Bu olay, ip örneğiyle ip örneğine eklenmiş olan ikincil bir ağ arabirimini nx_ip_interface_attach.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Arabirim IP Adresi
- Bilgi Alanı 3: IP arabirimi tablosuna dizinleme
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-interface-info-get"></a>IP Arabirimi Bilgileri Al 

#### <a name="nx_ip_interface_info_get"></a>nx_ip_interface_info_get

**Simge** ![ IP arabirimi bilgileri al simgesi](./media/user-guide/netx-events/image99.png)

**Açıklama**

Bu olay, ağ arabirimi aracılığıyla belirtilen ağ arabiriminden alınan bilgileri nx_ip_interface_info_get.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Arabirim IP adresi
- Bilgi Alanı 3: Arabirim MAC adresi msb
- Bilgi Alanı 4: Arabirim MAC adresi lsb

### <a name="ip-raw-packet-disable"></a>IP Ham Paketi Devre Dışı Bırakma 

#### <a name="nx_ip_raw_packet_disable"></a>nx_ip_raw_packet_disable

**Simge** ![ I P ham paketi devre dışı bırakma simgesi](./media/user-guide/netx-events/image100.png)

**Açıklama**

Bu olay, ağ üzerinden ham IP paketi iletişimini devre dışı nx_ip_raw_packet_disable.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-raw-packet-enable"></a>IP Ham Paketi Etkinleştirme 

#### <a name="nx_ip_raw_packet_enable"></a>nx_ip_raw_packet_enable

**Simge** ![ I P ham paketi etkinleştirme simgesi](./media/user-guide/netx-events/image101.png)

**Açıklama**

Bu olay, ağ üzerinden ham IP paketi iletişimini etkinleştirmeyi nx_ip_raw_packet_enable.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-raw-packet-receive"></a>IP Ham Paket Alma 

#### <a name="nx_ip_raw_packet_receive"></a>nx_ip_raw_packet_receive

**Simge** ![ I P ham paket alma simgesi](./media/user-guide/netx-events/image102.png)

**Açıklama**

Bu olay, ip adresi aracılığıyla ham BIR IP nx_ip_raw_packet_receive.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Paket işaretçisi
- Bilgi Alanı 3: Bekleme seçeneği
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-raw-packet-send"></a>IP Ham Paket Gönderme 

#### <a name="nx_ip_raw_packet_send"></a>nx_ip_raw_packet_send

**Simge** ![ I P ham paket gönderme simgesi](./media/user-guide/netx-events/image103.png)

**Açıklama**

Bu olay, ağ üzerinden bir ham IP nx_ip_raw_packet_send.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: Paket işaretçisi
- Bilgi Alanı 3: Hedef IP adresi
- Bilgi Alanı 4: Hizmet türü

### <a name="ip-static-route-add"></a>IP Statik Yol Ekleme 

#### <a name="nx_ip_static_route_add"></a>nx_ip_static_route_add

**Simge** ![ I P statik yol ekleme simgesi](./media/user-guide/netx-events/image104.png)

**Açıklama**

Bu olay, ip örneği yönlendirme tablosuna ip örneği yönlendirme tablosuna eklenen statik bir yolu nx_ip_static_route_add.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Ağ adresi
- Bilgi Alanı 3: Ağ maskesi
- Bilgi Alanı 4: Sonraki atlama

### <a name="ip-static-route-delete"></a>IP Statik Rota Silme 

#### <a name="nx_ip_static_route_delete"></a>nx_ip_static_route_delete

**Simge** ![ I P statik rute silme simgesi](./media/user-guide/netx-events/image105.png)

**Açıklama**

Bu olay, ip örneği yönlendirme tablosundan ip örneği yönlendirme tablosundan kaldırılan statik bir yolu nx_ip_static_route_delete.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Ağ adresi
- Bilgi Alanı 3: Ağ maskesi
- Bilgi Alanı 4: Kullanılmadı

### <a name="ip-status-check"></a>IP Durum Denetimi 

#### <a name="nx_ip_status_check"></a>nx_ip_status_check

**Simge** ![ I P durum denetimi simgesi](./media/user-guide/netx-events/image106.png)

**Açıklama**

Bu olay, ip durumunun ip adresi üzerinden denetlen nx_ip_status_check.

Bilgi Alanları 

- Bilgi Alanı 1: IP örneğinin işaretçisi
- Bilgi Alanı 2: İstenen durum
- Bilgi Alanı 3: Gerçek durum
- Bilgi Alanı 4: Bekleme seçeneği

### <a name="ipsec-enable"></a>IPSEC Etkinleştirme 

#### <a name="nx_ipsec_enable"></a>nx_ipsec_enable

**Simge** ![ I P S E C etkinleştirme simgesi](./media/user-guide/netx-events/image107.png)

**Açıklama**

Bu olay, sağlanan IP örneğinde ipsec hizmetlerinin etkinleştirilmesini temsil eder ve nx_ipsec_enable.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="packet-allocate"></a>Paket Ayırma 

#### <a name="nx_packet_allocate"></a>nx_packet_allocate

**Simge** ![ Paket ayırma simgesi](./media/user-guide/netx-events/image108.png)

**Açıklama**

Bu olay, bir paketin özel durum nx_packet_allocate.

**Bilgi Alanları**

- Bilgi Alanı 1: Paket havuzunun işaretçisi
- Bilgi Alanı 2: Ayrılan paketin işaretçisi
- Bilgi Alanı 3: Paket türü
- Bilgi Alanı 4: Kullanılabilir paketler

### <a name="packet-copy"></a>Paket Kopyası 

#### <a name="nx_packet_copy"></a>nx_packet_copy

**Simge** ![ Paket cpy simgesi](./media/user-guide/netx-events/image109.png)

**Açıklama**

Bu olay, nx_packet_copy aracılığıyla bir paketin kopya nx_packet_copy.

**Bilgi Alanları**

- Bilgi Alanı 2: Yeni paket işaretçisi
- Bilgi Alanı 3: Paket havuzunun işaretçisi
- Bilgi Alanı 4: Bekleme seçeneği

### <a name="packet-data-append"></a>Paket Verileri Ekleme 

#### <a name="nx_packet_data_append"></a>nx_packet_data_append

**Simge** ![ Paket verileri ekleme simgesi](./media/user-guide/netx-events/image110.png)

**Açıklama**

Bu olay, veri kaynağı aracılığıyla pakete veri nx_packet_data_append.

**Bilgi Alanları**

- Bilgi Alanı 1: Paketin işaretçisi
- Bilgi Alanı 2: Veri işaretçisi
- Bilgi Alanı 3: Veri boyutu
- Bilgi Alanı 4: Paket havuzunun işaretçisi

### <a name="packet-data-extract-offset"></a>Paket Verileri Ayıklama Uzaklığı 

#### <a name="nx_udp_source_extract_offset"></a>nx_udp_source_extract_offset

**Simge** ![ Paket verilerini ayıklama uzaklık simgesi](./media/user-guide/netx-events/image111.png)

**Açıklama**

Bu olay, bir paketten sağlanan arabelleğe ayıklanan paket verilerini nx_udp_source_extract_offset.

**Bilgi Alanları**

- Bilgi Alanı 1: Paket işaretçisi
- Bilgi Alanı 2: Belirtilen arabellek boyutu
- Bilgi Alanı 3: Kopyalanan bayt sayısı
- Bilgi Alanı 4: Kullanılmadı

### <a name="packet-data-retrieve"></a>Paket Verilerini Alma 

#### <a name="nx_packet_data_retrieve"></a>nx_packet_data_retrieve

**Simge** ![ Paket verilerini alma simgesi](./media/user-guide/netx-events/image112.png)

**Açıklama**

Bu olay, bir paketten veri alma verilerini nx_packet_data_retrieve.

**Bilgi Alanları** 

- Bilgi Alanı 1: Paketin işaretçisi
- Bilgi Alanı 2: Arabelleği başlatma işaretçisi
- Bilgi Alanı 3: Kopyalanan bayt sayısı
- Bilgi Alanı 4: Kullanılmadı

### <a name="packet-length-get"></a>Paket Uzunluğu Al 

#### <a name="nx_packet_length_get"></a>nx_packet_length_get

**Simge** ![ Paket uzunluğu al simgesi](./media/user-guide/netx-events/image113.png)

**Açıklama**

Bu olay, bir paketin uzunluğunun nx_packet_length_get.

**Bilgi Alanları**

- Bilgi Alanı 1: Paketin işaretçisi
- Bilgi Alanı 2: Paket uzunluğu
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="packet-pool-create"></a>Paket Havuzu Oluşturma 

#### <a name="nx_packet_pool_create"></a>nx_packet_pool_create

**Simge** ![ Paket havuzu oluşturma simgesi](./media/user-guide/netx-events/image114.png)

**Açıklama**

Bu olay, ağ üzerinden paket havuzu nx_packet_pool_create.

**Bilgi Alanları** 

- Bilgi Alanı 1: Paket havuzunun işaretçisi
- Bilgi Alanı 2: Paket yükü boyutu
- Bilgi Alanı 3: Havuz bellek alanı işaretçisi
- Bilgi Alanı 4: Havuz bellek alanı boyutu

### <a name="packet-pool-delete"></a>Paket Havuzu Silme 

#### <a name="nx_packet_pool_delete"></a>nx_packet_pool_delete

**Simge** ![ Paket havuzu silme simgesi](./media/user-guide/netx-events/image115.png)

**Açıklama**

Bu olay, bir paket havuzunun ağ üzerinden silinmesini nx_packet_pool_delete.

**Bilgi Alanları** 

- Bilgi Alanı 1: Paket havuzunun işaretçisi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

#### <a name="packet-pool-information-get"></a>Paket Havuzu Bilgilerini Al 

#### <a name="nx_packet_pool_info_get"></a>nx_packet_pool_info_get

**Simge** ![ Paket havuzu bilgilerini al simgesi](./media/user-guide/netx-events/image116.png)

**Açıklama**

Bu olay, paket havuzu bilgilerini nx_packet_pool_info_get.

**Bilgi Alanları**

- Bilgi Alanı 1: Paket havuzunun işaretçisi
- Bilgi Alanı 2: Toplam paket sayısı
- Bilgi Alanı 3: Kullanılabilir paketler
- Bilgi Alanı 4: Boş istekler

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

### <a name="tcp-client-socket-connect"></a>TCP istemci yuvası Bağlan 

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

### <a name="tcp-enable"></a>TCP Etkinleştirme 

#### <a name="nx_tcp_enable"></a>nx_tcp_enable

**Simge** ![ T C P etkinleştirme simgesi](./media/user-guide/netx-events/image127.png)

**Açıklama**

Bu olay, tcp'nin ağ üzerinden etkinleştirilmesini nx_tcp_enable.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Kullanılmadı
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

###  <a name="tcp-free-port-find-tcp-free-port-find"></a>TCP Ücretsiz Bağlantı Noktası Bul TCP Ücretsiz Bağlantı Noktası Bul 

#### <a name="nx_tcp_free_port_find"></a>nx_tcp_free_port_find

**Simge** ![ T CP ücretsiz bağlantı noktası bul simgesi](./media/user-guide/netx-events/image128.png)

**Açıklama**

Bu olay, ağ üzerinden ücretsiz bir TCP bağlantı noktası nx_tcp_free_port_find.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Arama bağlantı noktası numarasını başlatma
- Bilgi Alanı 3: Ücretsiz bağlantı noktası numarası
- Bilgi Alanı 4: Kullanılmadı

###  <a name="tcp-infomation-get"></a>TCP Bilgi Al 

#### <a name="nx_tcp_info_get"></a>nx_tcp_info_get

**Simge** ![ T C P bilgileri al simgesi](./media/user-guide/netx-events/image129.png)

**Açıklama**

Bu olay, belirtilen IP örneği için ip adresi üzerinden TCP bilgilerini alma nx_tcp_info_get.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Gönderilen bayt sayısı
- Bilgi Alanı 3: Alınan bayt sayısı
- Bilgi Alanı 4: Geçersiz paket sayısı

###  <a name="tcp-server-socket-accept"></a>TCP Sunucu Yuvası Kabul Etme 

#### <a name="nx_tcp_server_socket_accept"></a>nx_tcp_server_socket_accept

**Simge** ![ T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image130.png)

**Açıklama**

Bu olay, ağ üzerinden etkin bir bağlantı isteği alındıktan sonra sunucu yuvasının nx_tcp_server_socket_accept.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Bekleme seçeneği
- Bilgi Alanı 4: Yuva durumu

###  <a name="tcp-server-socket-listen"></a>TCP Sunucusu Yuvası Dinleme 

#### <a name="nx_tcp_server_socket_listen"></a>nx_tcp_server_socket_listen

**Simge** ![ T C P sunucu yuvası lsten simgesi](./media/user-guide/netx-events/image131.png)

**Açıklama**

Bu olay, bir dinleme isteğini ve belirtilen TCP bağlantı noktası için bir sunucu yuvası kaydetmeyi temsil eder nx_tcp_server_socket_listen.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: TCP bağlantı noktası numarası
- Bilgi Alanı 3: Yuva işaretçisi
- Bilgi Alanı 4: Kuyruğa alınan en fazla bağlantı sayısı

###  <a name="tcp-server-socket-relisten"></a>TCP Sunucusu Yuva Yeniden Listesi 

#### <a name="nx_tcp_server_socket_relisten"></a>nx_tcp_server_socket_relisten

**Simge** ![ T C P sunucu yuvası yeniden listele simgesi](./media/user-guide/netx-events/image132.png)

**Açıklama**

Bu olay, belirtilen TCP bağlantı noktası üzerinde mevcut bir dinleme isteği için başka bir sunucu yuvası kaydetmeyi temsil eder nx_tcp_server_socket_relisten.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: TCP bağlantı noktası numarası
- Bilgi Alanı 3: Yuva işaretçisi
- Bilgi Alanı 4: Yuva durumu

###  <a name="tcp-server-socket-unaccept"></a>TCP Sunucu Yuvası Kabul Uzamadı 

#### <a name="nx_tcp_server_socket_unaccept"></a>nx_tcp_server_socket_unaccept

**Simge** ![ T C P sunucu yuvası kabul etme simgesi](./media/user-guide/netx-events/image133.png)

**Açıklama**

Bu olay, sunucu yuvasının bağlantı noktası aracılığıyla daha önce pasif bağlantı alan bağlantı noktasıyla ilişkilendirmeden kaldırılmasını nx_tcp_server_socket_unaccept.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Yuva durumu
- Bilgi Alanı 4: Kullanılmadı

###  <a name="tcp-server-socket-unlisten-tcp-server-socket-unlisten"></a>TCP Sunucusu Yuvası Listede Olmayan TCP Sunucusu Yuvası Listeden Çıkar 

#### <a name="nx_tcp_server_socket_unlisten"></a>nx_tcp_server_socket_unlisten

**Simge** ![ T C P sunucu yuvası listede yok simgesi](./media/user-guide/netx-events/image134.png)

**Açıklama**

Bu olay, belirtilen TCP bağlantı noktası için önceki bir dinleme isteğinin nx_tcp_server_socket_unlisten.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: TCP bağlantı noktası numarası
- Bilgi Alanı 3: Kullanılmadı
- Bilgi Alanı 4: Kullanılmadı

### <a name="tcp-socket-bytes-available"></a>TCP Yuva BaytLarı Kullanılabilir 

#### <a name="nx_tcp_socket_bytes_available"></a>nx_tcp_socket_bytes_available

**Simge** ![ T C P yuva baytları kullanılabilir simgesi](./media/user-guide/netx-events/image135.png)

**Açıklama**

Bu olay, belirtilen TCP alma yuvasında şu anda kullanılabilir olan bayt sayısını nx_tcp_socket_bytes_available.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: TCP yuvası işaretçisi
- Bilgi Alanı 3: Yuvada alınan bayt sayısı
- Bilgi Alanı 4: Kullanılmadı

### <a name="tcp-socket-create"></a>TCP Yuvası Oluşturma 

#### <a name="nx_tcp_socket_create"></a>nx_tcp_socket_create

**Simge** ![ T C P yuva oluşturma simgesi](./media/user-guide/netx-events/image136.png)

**Açıklama**

Bu olay, ağ üzerinden TCP yuvası oluşturmayı nx_tcp_socket_create.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Hizmet türü
- Bilgi Alanı 4: Alma penceresi boyutu

### <a name="tcp-socket-delete"></a>TCP Yuva Silme 

#### <a name="nx_tcp_socket_delete"></a>nx_tcp_socket_delete

**Simge** ![ T C P yuva silme simgesi](./media/user-guide/netx-events/image137.png)

**Açıklama**

Bu olay, yuva aracılığıyla yuva silmeyi nx_tcp_socket_delete.

**Bilgi Alanları** 

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Yuva durumu
- Bilgi Alanı 4: Kullanılmadı

### <a name="tcp-socket-disconnect"></a>TCP Yuvası Bağlantısını Kesme 

#### <a name="nx_tcp_socket_disconnect"></a>nx_tcp_socket_disconnect

**Simge** ![ T C P yuva bağlantısını kesme simgesi](./media/user-guide/netx-events/image138.png)

**Açıklama**

Bu olay, yuva aracılığıyla bir yuvanın bağlantısının nx_tcp_socket_disconnect.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Bekleme seçeneği
- Bilgi Alanı 4: Yuva durumu

### <a name="tcp-socket-information-get"></a>TCP Yuvası Bilgilerini Al 

#### <a name="nx_tcp_socket_info_get"></a>nx_tcp_socket_info_get

**Simge** ![ T C P yuva bilgilerini al simgesi](./media/user-guide/netx-events/image139.png)

**Açıklama**

Bu olay, yuva aracılığıyla yuva hakkında bilgi nx_tcp_socket_info_get.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Bu yuvadan gönderilen bayt sayısı
- Bilgi Alanı 4: Bu yuvadan alınan bayt sayısı

### <a name="tcp-socket-mss-get"></a>TCP Yuvası MSS Get 

#### <a name="nx_tcp_socket_mss_get"></a>nx_tcp_socket_mss_get

**Simge** ![ T C P yuvası M S S get simgesi](./media/user-guide/netx-events/image140.png)

**Açıklama**

Bu olay, yuvanın MSS'lerini nx_tcp_socket_mss_get.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: En Büyük Kesim Boyutu (MSS)
- Bilgi Alanı 4: Yuva durumu

### <a name="tcp-socket-mss-peer-get"></a>TCP Yuvası MSS Eş Al 

#### <a name="nx_tcp_socket_mss_peer_get"></a>nx_tcp_socket_mss_peer_get

**Simge** ![ T C P yuvası M S S eş al simgesi](./media/user-guide/netx-events/image141.png)

**Açıklama**

Bu olay, yuvanın eş eş değerinin MSS değerinin nx_tcp_socket_mss_peer_get.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Eşlerin MSS'leri
- Bilgi Alanı 4: Yuva durumu

### <a name="tcp-socket-mss-set"></a>TCP Yuvası MSS Kümesi 

#### <a name="nx_tcp_socket_mss_set"></a>nx_tcp_socket_mss_set

**Simge** ![ T C P yuvası M S S kümesi simgesi](./media/user-guide/netx-events/image142.png)

**Açıklama**

Bu olay, bir yuvanın MSS'lerini nx_tcp_socket_mss_set.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: MSS
- Bilgi Alanı 4: Yuva durumu

### <a name="tcp-socket-peer-info-get"></a>TCP Yuvası Eş Bilgileri Al 

#### <a name="nx_tcp_socket_peer_info_get"></a>nx_tcp_socket_peer_info_get

**Simge** ![ T C P yuva eş bilgisi al simgesi](./media/user-guide/netx-events/image143.png)

**Açıklama**

Bu olay, tcp yuvasından eş ip adresi (örneğin, >bağlantı noktası) IP adresi ve bağlantı noktası ile ilgili olarak alınan bilgileri nx_tcp_socket_peer_info_get.

**Bilgi Alanları**

- Bilgi Alanı 1: TCP yuvası işaretçisi
- Bilgi Alanı 2: Eş IP adresi
- Bilgi Alanı 3: Eş bağlantı noktası numarası
- Bilgi Alanı 4: Kullanılmadı

### <a name="tcp-socket-receive"></a>TCP Yuvası Alma 

#### <a name="nx_tcp_socket_receive"></a>nx_tcp_socket_receive

**Simge** ![ T C P yuvası alma simgesi](./media/user-guide/netx-events/image144.png)

**Açıklama**

Bu olay, bir yuvadan veri alma verilerini nx_tcp_socket_receive.

**Bilgi Alanları**

- Bilgi Alanı 1: Yuva işaretçisi
- Bilgi Alanı 2: Alınan paketin işaretçisi
- Bilgi Alanı 3: Alınan paket uzunluğu
- Bilgi Alanı 4: Alma sırası numarası

### <a name="tcp-socket-receive-notify"></a>TCP Yuvası Alma Bildirimi 

#### <a name="nx_tcp_socket_receive_notify"></a>nx_tcp_socket_receive_notify

**Simge** ![ T C P yuvası alma bildirim simgesi](./media/user-guide/netx-events/image145.png)

**Açıklama**

Bu olay, bir yuva için bir alma bildirimi geri çağırma kaydını nx_tcp_socket_receive_notify.

**Bilgi Alanları**

- Bilgi Alanı 1: IP örneğine işaretçi
- Bilgi Alanı 2: Yuva işaretçisi
- Bilgi Alanı 3: Bildirim geri çağırma alma işaretçisi Bilgi Alanı 4: Kullanılmadı

### <a name="tcp-socket-send"></a>TCP Yuva Gönderme 

#### <a name="nx_tcp_socket_send"></a>nx_tcp_socket_send

**Simge** ![ T C P yuva gönderme simgesi](./media/user-guide/netx-events/image146.png)

**Açıklama**

Bu olay, veri kaynağı aracılığıyla bir yuvaya veri nx_tcp_socket_send.

**Bilgi Alanları**

- Bilgi Alanı 1: Yuva işaretçisi
- Bilgi Alanı 2: Paket işaretçisi
- Bilgi Alanı 3: Paketin uzunluğu
- Bilgi Alanı 4: Sıra numarasını iletme

### <a name="tcp-socket-state-wait"></a>TCP Yuva Durumu Bekleme 

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