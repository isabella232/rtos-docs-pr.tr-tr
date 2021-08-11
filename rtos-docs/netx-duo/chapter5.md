---
title: Bölüm 5-Azure RTOS NetX Duo ağ sürücüleri
description: Bu bölümde, Azure RTOS NetX Duo için ağ sürücülerine yönelik bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a0d18929f33f15a342e8fb8b3d01d4ce934d6ec7dc287707f960adb36fb4f44b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788856"
---
# <a name="chapter-5---azure-rtos-netx-duo-network-drivers"></a>Bölüm 5-Azure RTOS NetX Duo ağ sürücüleri

Bu bölümde, Azure RTOS NetX Duo için ağ sürücülerine yönelik bir açıklama yer almaktadır. Sunulan bilgiler, geliştiricilerin NetX Duo için uygulamaya özel ağ sürücüleri yazmasına yardımcı olmak üzere tasarlanmıştır.

## <a name="driver-introduction"></a>Sürücü tanıtımı

NX_IP yapısı, tek bir IP örneğini yönetmek için her şeyi içerir. Bu, genel TCP/IP protokol bilgilerinin yanı sıra uygulamaya özgü fiziksel ağ sürücüsünün giriş yordamını da içerir. Sürücünün giriş yordamı, ***nx_ip_create** _ hizmeti sırasında tanımlanmıştır. Ek cihazlar, _ *_nx_ip_interface_attach_** HIZMETI aracılığıyla IP örneğine eklenebilir.

NetX Duo ve uygulamanın ağ sürücüsü arasındaki iletişim **NX_IP_DRIVER** istek yapısı aracılığıyla gerçekleştirilir. Bu yapı genellikle çağıranın yığınında yerel olarak tanımlanır ve bu nedenle sürücü ve çağırma işlevi dönüşden sonra serbest bırakılır. Yapı aşağıdaki gibi tanımlanır.

```c
typedef struct NX_IP_DRIVER_STRUCT
{
      UINT           nx_ip_driver_command;
      UINT           nx_ip_driver_status;
      ULONG          nx_ip_driver_physical_address_msw;
      ULONG          nx_ip_driver_physical_address_lsw;
      NX_PACKET      *nx_ip_driver_packet;
      ULONG          *nx_ip_driver_return_ptr;
      NX_IP          *nx_ip_driver_ptr;
      NX_INTERFACE   *nx_ip_driver_interface;01
} NX_IP_DRIVER;
```
## <a name="driver-entry"></a>Sürücü girdisi 

NetX Duo, sürücü başlatma ve paket gönderme ve ağ cihazını başlatma ve etkinleştirme dahil çeşitli denetim ve durum işlemleri için ağ sürücüsü girişi işlevini çağırır. NetX Duo, _ *NX_IP_DRIVER** istek yapısındaki ***nx_ip_driver_command** _ alanını ayarlayarak ağ sürücüsüne komutlar verir. Sürücü girdisi işlevi aşağıdaki biçimdedir:

```c
VOID my_driver_entry(NX_IP_DRIVER *request);
```
## <a name="driver-requests"></a>Sürücü Istekleri

NetX Duo, belirli bir komutla sürücü isteği oluşturur ve komutu yürütmek için sürücü girdisi işlevini çağırır. Her ağ sürücüsünün tek bir giriş işlevi olduğundan, NetX Duo tüm istekleri sürücü isteği veri yapısı üzerinden yapar. Sürücü isteği veri yapısının ***nx_ip_driver_command** _ üyesi (_* NX_IP_DRIVER * *) isteği tanımlar. Durum bilgisi, üyenin **_nx_ip_driver_status_* çağıran öğesine geri bildirilir_. Bu alan _ * NX_SUCCESS * * ise, sürücü isteği başarıyla tamamlanmıştır.

NetX Duo, sürücüye tüm erişimi seri hale getirir. Bu nedenle, sürücünün giriş işlevini zaman uyumsuz olarak çağıran birden çok iş parçacığını işlemesi gerekmez. Cihaz sürücüsü işlevinin IP mutex 'i kilitlemeli olarak yürütüldüğünü unutmayın. Bu nedenle, aygıt sürücüsü iç işlevi kendisini engelleyemez.

Genellikle cihaz sürücüsü kesmeleri de işler. Bu nedenle, tüm sürücü işlevlerinin kesme açısından güvenli olması gerekir.

### <a name="driver-initialization"></a>Sürücü başlatma   
Asıl sürücü başlatma işlemi uygulamaya özgü olsa da, genellikle veri yapısı ve fiziksel donanım başlatma bilgisinden oluşur. NetX Duo sürücü başlatması için gereken bilgiler, IP katmanı yükünün IPv4 veya IPv6 üst bilgisi dahil olmak üzere kullanılabilir bayt sayısı olan IP en yüksek Iletim birimidir (MTU) ve fiziksel arabirimin mantıksal-fiziksel eşleme ihtiyacı varsa. Sürücü, ***nx_ip_interface_mtu_set*** ÇAĞıRARAK arabirim MTU değerini yapılandırır.

Arabirim adresi eşlemesinin gerekli olup olmadığına bakılmaksızın, cihaz sürücüsünün NetX Duo 'a bildirmesi için ***nx_ip_interface_address_mapping_configure** _ çağrısı yapması gerekir. Adres eşleme gerekiyorsa, arabirimi geçerli MAC adresiyle yapılandırmak ve _ *_nx_ip_interface_physical_address_set_* * aracılığıyla NETX 'e Mac adresini sağlamak için sürücü sorumludur.

Ağ sürücüsü, NetX Duo 'dan NX_LINK başlatma isteği aldığında, yukarıda gösterilen NX_IP_DRIVER isteği denetim bloğunun bir parçası olarak IP denetim bloğuna bir işaretçi alır.

Uygulama ***nx_ip_create*** çağrıldıktan sonra, IP Yardımcısı iş parçacığı, bir sürücü isteğini, bu komutun fiziksel ağ arabirimini başlatmak için sürücüye NX_LINK_INITIALIZE olarak ayarlanmış şekilde gönderir. Başlatma isteği için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

| NX_IP_DRIVER &nbsp; üyesi | Anlamı    |
| ------------------------- | ----------------------------- |
| nx_ip_driver_command   | NX_LINK_INITIALIZE    |
| nx_ip_driver_ptr       | IP örneğine yönelik işaretçi. Sürücü işlevinin üzerinde çalışacağı IP örneğini bulabilmesi için bu değer sürücü tarafından kaydedilmelidir.    |
| nx_ip_driver_interface | IP örneği içindeki ağ arabirimi yapısına yönelik işaretçi. Bu bilgilerin sürücü tarafından kaydedilmesi gerekir. Paket alındığında, sürücü, paketi yığın üzerine gönderirken arabirim yapısı bilgilerini kullanır. Bu veri yapısının içindeki üye nx_interface_index okunarak arabirim dizini (cihaz dizini) elde edilebilir. |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, belirtilen arabirimi IP örneğine başlatamayacak, sıfır dışında bir hata durumu döndürür. |


> [!NOTE]  
> *Sürücü aslında IP örneği için oluşturulan IP Yardımcısı iş parçacığından çağırılır. Bu nedenle, sürücü yordamının engelleme işlemlerini gerçekleştirmekten kaçının veya IP Yardımcısı iş parçacığı, IP iş parçacığını kullanan uygulamalarda sınırsız gecikmelere neden olabilir*.

### <a name="enable-link"></a>Bağlantıyı etkinleştir   
Ardından, IP Yardımcısı iş parçacığı, sürücü isteğindeki NX_LINK_ENABLE ve isteği ağ sürücüsüne göndererek fiziksel ağa izin vermez. Bu, kısa süre önce IP Yardımcısı iş parçacığı başlatma isteğini tamamladıktan sonra gerçekleşir. Bağlantının etkinleştirilmesi, arabirim örneğindeki *nx_interface_link_up* alanını ayarlamak kadar basit olabilir. Ancak fiziksel donanımın işlemesini de içerebilir. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı etkinleştirme isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi       | Anlamı                      |
| ------------------------- | ---------------------------- |
| nx_ip_driver_command   | NX_LINK_ENABLE   |
| nx_ip_driver_ptr       | IP örneği işaretçisi  |
| nx_ip_driver_interface | Arabirim örneği işaretçisi |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü belirtilen arabirimi etkinleştiremeyebilir, sıfır olmayan bir hata durumu döndürür. |

### <a name="disable-link"></a>Bağlantıyı devre dışı bırak   
Bu istek, bir IP örneğini ***nx_ip_delete** _ hizmeti tarafından silinirken NETX Duo tarafından yapılır. Ya da bir uygulama, güç tasarrufu sağlamak için bağlantıyı geçici olarak devre dışı bırakmak üzere bu komutu verebilir. Bu hizmet, IP örneğindeki fiziksel ağ arabirimini devre dışı bırakır. Bağlantıyı devre dışı bırakma işlemi, _arabirim örneğindeki nx_interface_link_up * bayrağını temizlemek kadar kolay olabilir. Ancak fiziksel donanımın işlemesini de içerebilir. Genellikle, bu, ***bağlantıyı etkinleştirme** işleminin ters bir işlemidir_ . Bağlantı devre dışı bırakıldıktan sonra, arabirimi etkinleştirmek için uygulamanın _ *_bağlantıyı etkinleştir_** işlemini isteyin.

Aşağıdaki NX_IP_DRIVER üyeleri bağlantı devre dışı bırak isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi     | Anlamı                      |
| ------------------------- | ---------------------------- |
| nx_ip_driver_command   | NX_LINK_DISABLE    |
| nx_ip_driver_ptr       | IP örneği işaretçisi   |
| nx_ip_driver_interface | Arabirim örneği işaretçisi   |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, IP örneğinde belirtilen arabirimi devre dışı bırakamadığından, sıfır olmayan bir hata durumu döndürür. |

### <a name="uninitialize-link"></a>Uninitialize bağlantısı   
Bu istek, bir IP örneğini ***nx_ip_delete** _ hizmeti tarafından silinirken NETX Duo tarafından yapılır. Bu istek arabirimi Uninitialize ve başlatma aşamasında oluşturulan tüm kaynakları serbest bırakabilir. Genellikle _ *_Initialize link_** işleminin ters bir işlemidir. Arabirim geri alındıktan sonra, arabirim yeniden başlatılana kadar cihaz kullanılamaz.

Aşağıdaki NX_IP_DRIVER üyeleri bağlantı devre dışı bırak isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi    | Anlamı                  |
|------------------------|--------------------------|
| nx_ip_driver_command   | NX_LINK_UNINITIALZE      |
| nx_ip_driver_ptr       | IP örneği işaretçisi   |
| nx_ip_driver_interface | Arabirim örneği işaretçisi |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, belirtilen arabirimi IP örneğine Uninitialize, sıfır olmayan bir hata durumu döndürür. |

### <a name="packet-send"></a>Paket gönderme   
Bu istek, tüm NetX Duo protokollerinin paketleri iletmek için kullanıldığı iç IPv4 veya IPv6 gönderme işlemleri sırasında yapılır (ARP, RARP hariç). Paket Gönder komutunu alırken *nx_packet_prepend_ptr* gönderilecek paketin başlangıcını işaret eder; bu, IPv4 veya IPv6 üstbilgisinin başlangıcıdır. *nx_packet_length* , aktarılan verilerin toplam boyutunu (bayt cinsinden) gösterir. *Nx_packet_next* geçerliyse, giden IP veri birimi birden çok pakette depolanır, sürücü zincirleme paketini izlemek ve tüm çerçeveyi iletmek için gereklidir. Her zincirleme paketindeki geçerli veri alanının *nx_packet_prepend_ptr* ve *nx_packet_append_ptr* arasında depolandığını unutmayın.

Fiziksel üst bilgi oluşturulurken sürücü sorumludur. IP adresi eşlemesinin fiziksel adresi gerekliyse (örneğin, Ethernet), IP katmanı MAC adresini zaten çözümledi. Hedef MAC adresi, *nx_ip_driver_physical_address_msw ve nx_ip_driver_physical_address_lsw* depolanan IP örneğinden geçirilir.

Fiziksel üstbilgi eklendikten sonra, paket gönderme işlemi daha sonra paketin iletilmesi için sürücünün Çıkış işlevini çağırır.

Aşağıdaki NX_IP_DRIVER üyeleri paket gönderme isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi              | Anlamı                               |
| -----------------------------------| --------------------------------------|
| nx_ip_driver_command            | NX_LINK_PACKET_SEND                |
| nx_ip_driver_ptr                | IP örneği işaretçisi                |
| nx_ip_driver_packet             | Gönderilmek üzere paket işaretçisi         |
| nx_ip_driver_interface          | Arabirim örneğine yönelik işaretçi.    |
| nx_ip_driver_physical_address_msw | En önemli 32 bitlik fiziksel adres (yalnızca fiziksel eşleme gerekliyse) |
| nx_ip_driver_physical_address_lsw | En az önemli 32-fiziksel adres (yalnızca fiziksel eşleme gerekliyse) |
| nx_ip_driver_status             | Tamamlanma durumu. Sürücü paketi gönderemediği takdirde, sıfır olmayan bir hata durumu döndürür. |

### <a name="packet-broadcastipv4-packets-only"></a>Paket yayını (yalnızca IPv4 paketleri)  
Bu istek, paket gönderme isteğiyle neredeyse aynıdır. Tek fark, hedef fiziksel adres alanlarının Ethernet yayını MAC adresine ayarlanmamanızdır. Aşağıdaki NX_IP_DRIVER üyeleri paket yayını isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi                | Anlamı                                                                                                  |
|------------------------------------|----------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_PACKET_BROADCAST                                                                                 |
| nx_ip_driver_ptr                   | IP örneği işaretçisi                                                                                   |
| nx_ip_driver_packet                | Gönderilmek üzere paket işaretçisi                                                                            |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF (yayın)                                                                                   |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (yayın)                                                                                   |
| nx_ip_driver_interface             | Arabirim örneğine yönelik işaretçi.                                                                       |
| nx_ip_driver_status                | Tamamlanma durumu. Sürücü paketi gönderemediği takdirde, sıfır olmayan bir hata durumu döndürür. |

### <a name="arp-send"></a>ARP gönderme  
Bu istek, IP paketi gönderme isteğine de benzer. Tek fark, Ethernet üstbilgisinin IP paketi yerine bir ARP paketi belirttiğinden ve hedef fiziksel adres alanlarının MAC yayın adresi olarak ayarlandığı bir farktır. ARP gönderme isteği için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

| NX_IP_DRIVER &nbsp; üyesi                | Anlamı                                                                                                      |
|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_ARP_SEND                                                                                             |
| nx_ip_driver_ptr                   | IP örneği işaretçisi                                                                                       |
| nx_ip_driver_packet                | Gönderilmek üzere paket işaretçisi                                                                                |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF (yayın)                                                                                       |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (yayın)                                                                                       |
| nx_ip_driver_interface             | Arabirim örneğine yönelik işaretçi.                                                                           |
| nx_ip_driver_status                | Tamamlanma durumu. Sürücü ARP paketini gönderemez, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Fiziksel eşleme gerekmiyorsa, bu isteğin uygulanması gerekli değildir*.

*ARP, Komşu Bulma Protokolü ve IPv6 'Daki yönlendirici bulma protokolü ile değiştirilse de, Ethernet ağ sürücüleri yine de IPv4 eşleri ve yönlendiricilerle uyumlu olmalıdır. Bu nedenle, sürücülerin ARP paketlerini yine de işlemesi gerekir*.

### <a name="arp-response-send"></a>ARP yanıtı gönderme  
Bu istek ARP gönderme paketi isteğiyle neredeyse aynıdır. Tek fark, hedef fiziksel adres alanlarının IP örneğinden geçirilme örneğidir. Aşağıdaki NX_IP_DRIVER üyeleri ARP yanıtı gönderme isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi                  | Anlamı                                  |
| -------------------------------------- | -----------------------------------------|
| nx_ip_driver_command                | NX_LINK_ARP_RESPONSE_SEND            |
| nx_ip_driver_ptr                    | IP örneği işaretçisi   |
| nx_ip_driver_packet                 | Gönderilmek üzere paket işaretçisi          |
| nx_ip_driver_physical_address_msw | En önemli 32-fiziksel adres-bit |
| nx_ip_driver_physical_address_lsw | En az önemli 32-fiziksel adres bitleri |
| nx_ip_driver_interface              | Arabirim örneği işaretçisi |
| nx_ip_driver_status                 | Tamamlanma durumu. Sürücü ARP paketini gönderemez, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Fiziksel eşleme gerekmiyorsa, bu isteğin uygulanması gerekli değildir*.

### <a name="rarp-send"></a>RARP gönderme   
Bu istek ARP gönderme paketi isteğiyle neredeyse aynıdır. Tek farklar paket üstbilgisinin türüdür ve fiziksel hedef, her zaman bir yayın adresi olduğundan fiziksel adres alanları gerekli değildir.

Aşağıdaki NX_IP_DRIVER üyeleri, RARP gönderme isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi                | Anlamı                                                                                                       |
|------------------------------------|---------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_RARP_SEND                                                                                             |
| nx_ip_driver_ptr                   | IP örneği işaretçisi                                                                                        |
| nx_ip_driver_packet                | Gönderilmek üzere paket işaretçisi                                                                                 |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF (yayın)                                                                                        |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (yayın)                                                                                        |
| nx_ip_driver_interface             | Arabirim örneğine yönelik işaretçi.                                                                            |
| nx_ip_driver_status                | Tamamlanma durumu. Sürücü, RARP paketini gönderemez, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *RARP hizmeti gerektiren uygulamaların bu komutu uygulaması gerekir*.

### <a name="multicast-group-join"></a>Çok noktaya yayın grubuna ekleme   
Bu istek, IPv4, _ *_nxd_ipv6_multicast_interface_join_** hizmetinde IPv6 ve IPv6 için gereken çeşitli işlemleri içeren ***nx_igmp_multicast_interface joın** _ ve _*_nx_ipv4_multicast_interface_join_*_ hizmeti ile yapılır. Ağ sürücüsü, sağlanan çok noktaya yayın grubu adresini alır ve fiziksel medyayı bu çok noktaya yayın grubu adresinden gelen paketleri kabul edecek şekilde ayarlar. Çok noktaya yayın filtresini desteklemeyen sürücüler için, sürücü alma mantığının karışık modda olması gerekebileceğini unutmayın. Bu durumda, sürücünün hedef MAC adresine göre gelen çerçeveleri filtrelemeniz ve böylece IP örneğine geçirilen trafik miktarını azaltmasının gerekebilir. Aşağıdaki NX_IP_DRIVER üyeleri çok noktaya yayın grubu JOIN isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi                  | Anlamı                                 |
| -------------------------------------- | --------------------------------------- |
| nx_ip_driver_command                | NX_LINK_MULTICAST_JOIN               |
| nx_ip_driver_ptr                    | IP örneği işaretçisi  |
| nx_ip_driver_physical_address_msw | En önemli 32-fiziksel çok noktaya yayın adresi |
| nx_ip_driver_physical_address_lsw | En az önemli 32-fiziksel çok noktaya yayın adresi |
| nx_ip_driver_interface              | Arabirim örneği işaretçisi |
| nx_ip_driver_status                 | Tamamlanma durumu. Sürücü çok noktaya yayın grubuna katılamayabilir, sıfır olmayan bir hata durumu döndürür. |

> [!NOTE]  
> *IPv6 uygulamaları, adres yapılandırması gibi ICMPv6 tabanlı protokollerin sürücüsüne çok noktaya yayın uygulanmasına gerek duyar. Ancak, IPv4 uygulamaları için, çok noktaya yayın özellikleri gerekmiyorsa bu isteğin uygulanması gerekli değildir*.

> [!IMPORTANT]  
> *IPv6 etkinleştirilmemişse ve çok noktaya yayın özellikleri IPv4 için gerekli değilse, bu isteğin uygulanması gerekli değildir*.

### <a name="multicast-group-leave"></a>Çok noktaya yayın grubu bırakma  
Bu istek,*_Nxd_ipv6_multicast_interface_leave_* IPv4 'de ***nx_igmp_multicast_interface_leave** _ veya _*_nx_ipv4_multicast_interface_leave_*_ Hizmetleri aracılığıyla veya IPv6 Için gereken çeşitli iç NETX Duo işlemlerine açıkça çağırarak çağrılır. Sürücü, sağlanan Ethernet çok noktaya yayın adresini çok noktaya yayın listesinden kaldırır. Bir konak bir çok noktaya yayın grubuna ayrıldıktan sonra, ağ üzerindeki bu Ethernet çok noktaya yayın adresine sahip paketler artık bu IP örneği tarafından alınmaz. Aşağıdaki NX_IP_DRIVER üyeleri çok noktaya yayın grubu bırakma isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi              | Anlamı                              |
| -----------------------------------| -------------------------------------|
| nx_ip_driver_command            | NX_LINK_MULTICAST_LEAVE           |
| nx_ip_driver_ptr                | IP örneği işaretçisi   |
| nx_ip_driver_physical_address_msw | En önemli 32 bitlerin fiziksel çok noktaya yayın adresi |
| nx_ip_driver_physical_address_lsw | En az 32 bit fiziksel çok noktaya yayın adresi |
| nx_ip_driver_interface              | Arabirim örneği işaretçisi |
| nx_ip_driver_status                 | Tamamlanma durumu. Sürücü çok noktaya yayın grubunu bırakılamayan, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Çok noktaya yayın özellikleri IPv4 veya IPv6 için gerekmiyorsa, bu isteğin uygulanması gerekli değildir*.

### <a name="attach-interface"></a>Arabirim Ekle  
Bu istek NetX Duo 'ten cihaz sürücüsüne çağrılır, bu da sürücünün sürücü örneğini karşılık gelen IP örneğiyle ve fiziksel arabirim örneğiyle IP 'nin arasında ilişkilendirilmesine izin verir. Arabirim Ekle isteği için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

| NX_IP_DRIVER &nbsp; üyesi    | Anlamı                  |
|------------------------|--------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_ATTACH |
| nx_ip_driver_ptr       | IP örneği işaretçisi   |
| nx_ip_driver_interface | Arabirim örneğine yönelik işaretçi.|
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, belirtilen arabirimi IP örneğine ayıramayabilir, sıfır olmayan bir hata durumu döndürür. |

### <a name="detach-interface"></a>Arabirimi ayır    
Bu istek NetX Duo tarafından cihaz sürücüsüne çağrılır, böylece sürücü, sürücü örneğinin IP 'nin karşılık gelen IP örneğiyle ve fiziksel arabirim örneğiyle ilişkisini keser. Arabirim Ekle isteği için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

| NX_IP_DRIVER &nbsp; üyesi    | Anlamı                                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_DETACH                                                                                                                   |
| nx_ip_driver_ptr       | IP örneği işaretçisi                                                                                                                     |
| nx_ip_driver_interface | Arabirim örneğine yönelik işaretçi.                                                                                                         |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, belirtilen arabirimi IP örneğine iliştiremez, sıfır olmayan bir hata durumu döndürür. |

### <a name="get-link-status"></a>Bağlantı durumunu al    
Uygulama, konaktaki herhangi bir arabirim için NetX Duo hizmeti ***nx_ip_interface_status_check*** hizmetini kullanarak ağ arabirimi bağlantı durumunu sorgulayabilir. Bu hizmetlerle ilgili daha fazla bilgi için bkz. sayfa 149, "NetX Duo hizmetlerinin açıklaması".

Bağlantı durumu, *nx_ip_driver_interface* işaretçisine göre işaret edilen NX_INTERFACE yapısındaki *nx_interface_link_up* alanında bulunur. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı durumu isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi       | Anlamı                  |
| --------------------------- | -------------------------|
| nx_ip_driver_command     | NX_LINK_GET_STATUS    |
| nx_ip_driver_ptr         | IP örneğine işaretçi   |
| nx_ip_driver_return_ptr | Durumu yer alan hedefin işaretçisi. |
| nx_ip_driver_interface   | Arabirim örneğinin işaretçisi   |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü belirli bir durumu alamasa da sıfır olmayan bir hata durumu döndürür. |

> [!NOTE]  
> ***nx_ip_status_check** _ birincil arabirimin durumunu denetlemeye devam ediyor. Ancak, uygulama geliştiricilerinin arabirime özgü hizmeti kullanmaları teşvik edilecektir: _ *_nx_ip_interface_status_check._**

### <a name="get-link-speed"></a>Bağlantı Hızını Al  
Bu istek, hizmetten ***nx_ip_driver_direct_command*** yapılır. Sürücü, bağlantının hat hızını sağlanan hedefte depolar. Aşağıdaki NX_IP_DRIVER bağlantı çizgisi hızı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye   | Anlamı                   |
| ------------------------| ------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_SPEED          |
| nx_ip_driver_ptr         | IP örneğine işaretçi                                                                                         |
| nx_ip_driver_return_ptr | Çizgi hızının yer İşaretçisi                                                             |
| nx_ip_driver_interface   | Arabirim örneğinin işaretçisi                                                                              |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü hız bilgilerini alamayacaksa sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu istek NetX Duo tarafından dahili olarak kullanılmaz, bu nedenle uygulaması isteğe bağlıdır.*

### <a name="get-duplex-type"></a>Çift Yönlü Türü Al   
Bu istek, hizmetten ***nx_ip_driver_direct_command*** yapılır. Sürücü, bağlantının çift yönlü türünü sağlanan hedefte depolar. Aşağıdaki NX_IP_DRIVER çift yönlü tür isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye   | Anlamı                                                                                                    |
| --------------------------- | -------------------------------------------------------------------------------------------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_DUPLEX_TYPE                                                                                    |
| nx_ip_driver_ptr         | IP örneğine işaretçi                                                                                         |
| nx_ip_driver_return_ptr | Çift yönlü türün yer İşaretçisi                                                            |
| nx_ip_driver_interface   | Arabirim örneğinin işaretçisi                                                                              |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü çift yönlü bilgileri alamayacaksa sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu istek NetX Duo tarafından dahili olarak kullanılmaz, bu nedenle uygulaması isteğe bağlıdır.*

### <a name="get-error-count"></a>Hata Sayısını Al   
Bu istek, hizmetten ***nx_ip_driver_direct_command*** yapılır. Sürücü, bağlantının hata sayısını sağlanan hedefte depolar. Bu özelliği desteklemek için sürücünün işlem hatalarını izlemesi gerekir. Aşağıdaki NX_IP_DRIVER bağlantı hatası sayısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye   | Anlamı                   |
| --------------------------- | -------------------------------|
| nx_ip_driver_command     | NX_LINK_GET_ERROR_COUNT   |
| nx_ip_driver_ptr         | IP örneğine işaretçi   |
| nx_ip_driver_return_ptr | Hata sayısını yer alan hedefin işaretçisi |
| nx_ip_driver_interface   | Arabirim örneğinin işaretçisi|
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü hata sayısını alamasa da sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]
> *Bu istek NetX Duo tarafından dahili olarak kullanılmaz, bu nedenle uygulaması isteğe bağlıdır.*

### <a name="get-receive-packet-count"></a>Alma Paketi Sayısını Alma    
Bu istek, hizmetten ***nx_ip_driver_direct_command*** yapılır. Sürücü, bağlantının alma paketi sayısını sağlanan hedefte depolar. Bu özelliği desteklemek için sürücünün alınan paket sayısını izlemesi gerekir. Aşağıdaki NX_IP_DRIVER, bağlantı alma paket sayısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye       | Anlamı                        |
| --------------------------- | -------------------------------|
| nx_ip_driver_command     | NX_LINK_GET_RX_COUNT      |
| nx_ip_driver_ptr         | IP örneğine işaretçi  |
| nx_ip_driver_return_ptr | Alma paketi sayısını almak için hedefin işaretçisi   |
| nx_ip_driver_interface   | Fiziksel ağ arabirimi işaretçisi  |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü alma sayısını alamasa da sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu istek NetX Duo tarafından dahili olarak kullanılmaz, bu nedenle uygulaması isteğe bağlıdır.*

### <a name="get-transmit-packet-count"></a>İletim Paketi Sayısını Al   
Bu istek, hizmetten ***nx_ip_driver_direct_command*** yapılır. Sürücü, bağlantının aktarım paketi sayısını sağlanan hedefte depolar. Bu özelliği desteklemek için sürücünün her arabirime ilettiği her paketi izlemesi gerekir. Aşağıdaki NX_IP_DRIVER bağlantı iletme paket sayısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye   | Anlamı                   |
| ----------------------- | ------------------------- |
| nx_ip_driver_command | NX_LINK_GET_TX_COUNT  |
| nx_ip_driver_ptr     | IP örneğine işaretçi    |
| nx_ip_driver_return_ptr | İletme paketi sayısını yer alan hedefin işaretçisi  |
| nx_ip_driver_interface   | Arabirim örneği işaretçisi   |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü, iletim sayısını alamıyor, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu Istek NetX Duo tarafından dahili olarak kullanılmadığından, uygulamanın isteğe bağlı olması önerilir*.

### <a name="get-allocation-errors"></a>Ayırma hatalarını al   
Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının paket havuzu ayırma hata sayısını sağlanan hedefte depolar. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı ayırma hata sayısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi       | Anlamı                       |
| --------------------------- | ----------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_ALLOC_ERRORS  |
| nx_ip_driver_ptr         | IP örneği işaretçisi     |
| nx_ip_driver_return_ptr | Ayırma hata sayısını yerleştirmek için hedefin işaretçisi  |
| nx_ip_driver_interface   | Arabirim örneği işaretçisi  |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü ayırma hatalarını alamazsanız, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu Istek NetX Duo tarafından dahili olarak kullanılmadığından, uygulamanın isteğe bağlı olması önerilir*.

### <a name="driver-deferred-processing"></a>Sürücü ertelenmiş Işleme    
Bu istek, bir iletme veya alma ISR 'den _* **nx_ip_driver_deferred_processing**_ yordamını çağıran sürücüye yanıt olarak IP Yardımcısı iş parçacığından yapılır. Bu, sürücü ıSR 'nin paket alma ve aktarım işlemeyi IP Yardımcısı iş parçacığına erteetmesine olanak tanır ve bu sayede, ıSR 'de işlem miktarını azaltır. *Nx_ip_driver_interface* tarafından işaret edilen NX_INTERFACE yapısındaki _nx_interface_additional_link_info * alanı, sürücü tarafından IP Yardımcısı iş parçacığı bağlamından ertelenmiş işleme olayı hakkında bilgi depolamak için kullanılabilir. Ertelenmiş işleme olayı için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

| NX_IP_DRIVER &nbsp; üyesi     | Anlamı                           |
| ------------------------- | --------------------------------- |
| nx_ip_driver_command   | NX_LINK_DEFERRED_PROCESSING    |
| nx_ip_driver_ptr       | IP örneği işaretçisi            |
| nx_ip_driver_interface | Arabirim örneği işaretçisi |

### <a name="set-physical-address"></a>Fiziksel adresi ayarla  
Bu istek, ***nx_ip_interface_physical_address_set** _ hizmeti içinden yapılır. Bu hizmet, bir uygulamanın çalışma zamanında Arabirim fiziksel adresini değiştirmesine izin verir. Bu komut alındığında, sürücünün ağ arabiriminin donanım adresini sağlanan fiziksel adrese yeniden yapılandırması gerekir. IP örneği zaten yeni bir adrese sahip olduğundan, bu komuttan _ *_nx_ip_interface_address_set_** hizmetini çağırmanız gerekmez.

Aşağıdaki NX_IP_DRIVER üyeleri Kullanıcı komut isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi      | Anlamı                      |
| -------------------------- | ---------------------------- |
| nx_ip_driver_command    | NX_LINK_SET_PHYSICAL_ADDRESS  |
| nx_ip_driver_ptr        | IP örneği işaretçisi  |
| nx_ip_driver_interface  | Arabirim örneği işaretçisi   |
| nx_ip_driver_physical_ad dress_msw | En önemli 32-yeni fiziksel adresin bitleri  |
| nx_ip_driver_physical_ad dress_lsw | En az önemli 32-yeni fiziksel adresin bitleri  |
| nx_ip_driver_status                  | Tamamlanma durumu. Sürücü fiziksel adresi yeniden yapılandıramayabilir, sıfır olmayan bir hata durumu döndürür. |

### <a name="user-commands"></a>Kullanıcı komutları    
Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü uygulamaya özgü Kullanıcı komutlarını işler. Aşağıdaki NX_IP_DRIVER üyeleri Kullanıcı komut isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi       | Anlamı                       |
| --------------------------- | ----------------------------- |
| nx_ip_driver_command     | NX_LINK_USER_COMMAND       |
| nx_ip_driver_ptr         | IP örneği işaretçisi        |
| nx_ip_driver_return_ptr | Kullanıcı tanımlı       |
| nx_ip_driver_interface   | Arabirim örneği işaretçisi    |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü, Kullanıcı komutlarını yürütemediğinde, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT] 
> *Bu Istek NetX Duo tarafından dahili olarak kullanılmadığından, uygulamanın isteğe bağlı olması önerilir*.

### <a name="unimplemented-commands"></a>Uygulanmayan komutlar  
Ağ sürücüsü tarafından uygulanmayan komutların geri dönüş durumu alanı NX_UNHANDLED_COMMAND olarak ayarlanmalıdır.

## <a name="driver-capability"></a>Sürücü özelliği

Bazı ağ arabirimleri sağlama toplamı boşaltma özellikleri sunar. Cihaz sürücüleri, çeşitli sağlama toplamı hesaplamaları çalıştırmanın CPU süresini boşaltmak için donanım hızlandırışlarından yararlanabilir.

Donanımdan donanım sağlama toplamı desteğinin düzeyine bağlı olarak, cihaz sürücüsünün, donanım özelliğinin etkin olduğu IP örneğini bilgilendirilmesi gerekir. Bu şekilde, IP örneği donanım özelliğinin farkında olur ve donanıma mümkün olduğunca çok hesaplama yükü vermez. Sürücü, fiziksel arabirimin işleyebileceği tüm özellikleri ayarlamak için API ***nx_ip_interface_capability_set*** kullanmalıdır.

Aşağıdaki özellikler kullanılabilir:

- NX_INTERFACE_CAPABILITY_IPV4_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_IPV4_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_TCP_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_TCP_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_UDP_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_UDP_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_ICMPV4_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_ICMPV4_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_ICMPV6_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_ICMPV6_RX_CHECKSUM
- NX_INTERFACE_CAPABILITY_IGMP_TX_CHECKSUM
- NX_INTERFACE_CAPABILITY_IGMP_RX_CHECKSUM

Donanımda gerçekleştirilebilecek bir sağlama toplamı hesaplaması için, sürücünün donanım veya arabellek tanımlayıcılarını doğru ayarlaması gerekir, böylece bir çıkış paketinin sağlama toplamı donanım tarafından oluşturulabilir ve üstbilgiye eklenebilir. Bir paket alındığında, donanım sağlama toplamı mantığı, sağlama toplamı değerini doğrulayabilmelidir. Sağlama toplamı değeri yanlışsa, alınan çerçeve atılmalıdır.

Donanımda sağlamam hesaplaması gerçekleştirme özelliğine rağmen IP örneği sağlama sağlamam özelliğini korumaya devam ediyor. Belirli senaryolarda, örneğin IPsec koruması üzerinden geçen bir UDP veri birimi, UDP sağlama toplaması yığından aşağı UDP çerçevesini geçirmeden önce yazılımda hesaplanır. Çoğu donanım sağlama toplama özelliği, IPsec tarafından korunan bir veri kesimi için sağlama toplama hesaplamasını desteklemez. Parçalanması gereken bir UDP veya ICMP çerçevesi için, UDP veya ICMP sağlamaları, yazılımda hesaplanması gerekir. Çoğu donanım sağlama sağlama mantığı, verilerin birden çok kareye bölünmesi durumlarını işlemez.

## <a name="driver-output"></a>Sürücü Çıkışı  

Daha önce bahsedilen tüm paket iletme istekleri, sürücüde uygulanan bir çıkış işlevi gerektirir. Belirli bir iletme mantığı donanıma özeldir, ancak genellikle paketi hemen göndermek için donanım kapasitesini denetlemeyi içerir. Mümkünse, paket yükü (ve paket zincirinde ek yükler) bir veya daha fazla donanım iletme arabelleklerine yüklenir ve bir iletme işlemi başlatılır. Paket, kullanılabilir aktarım arabellekleri içine sığmayacaksa, paket kuyruğa alınarak iletim arabellekleri kullanılabilir olduğunda ilet gerekir.

Önerilen iletme kuyruğu tek başına bağlantılı bir listedir ve hem baş hem de kuyruk işaretçileri içerir. Kuyruğun sonuna yeni paketler eklenir ve en eski paket önde olur. Nx_packet_queue_next  alanı, paketin kuyrukta bir sonraki bağlantısı olarak kullanılır. Sürücü, iletme kuyruğunu baş ve kuyruk işaretçilerini tanımlar.

> [!CAUTION]  
> *Bu kuyruğa iş parçacığından erişilip* sürücünün kesme bölümlerine erişilemediklerinden, kesme koruması kuyruk düzenlemelerinin etrafına yerleştirilsin.

Çoğu fiziksel donanım uygulaması, paket iletme tamamlandıktan sonra bir kesintiye neden olur. Sürücü böyle bir kesinti aldığında, genellikle yeni iletilen paketle ilişkili kaynakları serbest bıraktır. İletme mantığının verileri doğrudan NX_PACKET okuması durumunda sürücü, aktarım tamamlama kesmesi ile ilişkili paketi kullanılabilir paket havuzuna geri serbest bırakmak için ***nx_packet_transmit_release*** hizmetini kullandır. Ardından sürücü, gönderilmek üzere bekleyen ek paketler için aktarım kuyruğuna bakarak. Donanım iletme arabelleğine sığan kuyruğa alınan iletim paketlerinin çoğu kuyruğa alınarak arabelleklere yüklenir. Bunun ardından başka bir gönderme işlemi başlatıldı.

NX_PACKET'daki veriler verici FIFO'ya taşındığı anda (veya bir sürücünün sıfır kopyalamayı desteklemesi durumunda, NX_PACKET'daki veriler iletildi), *  nx_packet_prepend_ptr çağırmadan önce sürücünün IP üst bilgisinin başına **nx_packet_transmit_release.** _ Bu alanı* _nx_packet_length ayarlamayı unutmayın. Bir IP çerçevesi birden çok paketden meydana geliyorsa, yalnızca paket zincirinin başı serbest bırakılana kadar devam etmek gerekir.

## <a name="driver-input"></a>Sürücü Girişi

Alınan paket kesintisi alındı sonra, ağ sürücüsü paketi fiziksel donanım alma arabelleklerinden alır ve geçerli bir NetX Duo paketi derlemez. Geçerli bir NetX Duo paketi oluşturmak için uygun uzunluk alanını ayarlamanız ve gelen paketin boyutu tek bir paket yükünden büyükse birden çok paketi zincirlemeniz gerekir. Düzgün bir şekilde *prepend_ptr,* fiziksel katman üst bilgiden sonra taşınır ve alma paketi NetX Duo'ya sevk edilir.

NetX Duo, IP (IPv4 ve IPv6) ve ARP üst bilgilerini bir ULONG sınırında **hizalı olarak kabul** eder. Bu nedenle NetX Duo sürücüsünün bu hizalamadan emin olması gerekir. Ethernet ortamlarında bu, Ethernet üst bilgisi paketin başından iki bayt başlatarak yapılır. Bağlantı *nx_packet_prepend_ptr* Ethernet üst bilgisi dışına taşındığında, temel alınan IP (IPv4 ve IPv6) veya ARP üst bilgisi 4 bayt hizalı olur.

> [!WARNING] 
> *IPv6 ve IPv6 Ethernet* üst bilgileri arasındaki önemli farklar için aşağıdaki "Ethernet Üst Bilgileri" bölümüne bakın.

NetX Duo'da çeşitli alma paketi işlevleri vardır. Alınan paket bir ARP paketi ise, _* **nx_arp_packet_deferred_receive**_ çağrılır. Alınan paket bir RARP paketi ise _ _*_nx_rarp_packet_deferred_receive_*_ çağrılır. Gelen IP paketlerini işlemeye çeşitli seçenekler vardır. IP paketlerinin en hızlı işlenmesi için _ _*_nx_ip_packet_receive_*_ çağrılır. Bu yaklaşım en az ek yüke sahiptir, ancak sürücünün alma kesme hizmeti işleyicisinde (ISR) daha fazla işlem gerektirir. Minimum ISR işleme *____* nx_ip_packet_deferred_receive * çağrılır.

Yeni alma paketi düzgün bir şekilde edildikten sonra, fiziksel donanımın alma arabellekleri daha fazla veri alacak şekilde ayarlar. Bu, NetX Duo paketlerinin ayrılarak ve yük adresinin donanım alma arabelleğine yerleştirilmesini veya yalnızca donanım alma arabelleğinde bir ayarın değiştirilmesini gerektirir. Fazla çalıştırma olanaklarını en aza indirmek için, bir paket alındıktan sonra donanımın alma arabelleklerinin kullanılabilir arabelleklere sahip olduğu önemlidir.

> [!IMPORTANT] 
> *İlk alma arabellekleri, sürücü başlatması sırasında kurulumuna başlar.*

### <a name="deferred-receive-packet-handling"></a>Ertelenmiş Alma Paketi İşleme  
Sürücü, paket işlemeyi NetX Duo IP yardımcı iş parçacığına erteleyebilirsiniz. Bazı uygulamalarda, bırakılan paketlerin yanı sıra ISR işlemeyi en aza indirmek için bu gerekli olabilir. 

Ertelenen paket işlemeyi kullanmak için NetX Duo kitaplığının önce * NX_DRIVER_DEFERRED_PROCESSING _ tanımlı **olarak derlenmiş** olması gerekir. Bu, ertelenen paket mantığını NetX Duo IP yardımcı iş parçacığına ekler. Ardından, bir veri paketi alırken sürücünün __nx_ip_packet_deferred_receive():*

```c
_nx_ip_packet_deferred_receive(ip_ptr, packet_ptr);
```
Ertelenen alma işlevi, bir FIFO (bağlantılı liste) üzerinde bir *packet_ptr* tarafından temsil edilen alma paketini yer alır ve IP yardımcı iş parçacığına bilgi verir. Yürüttkten sonra, IP yardımcısı ertelenen her paketin işlenmesi için ertelenen işleme işlevini tekrar tekrar çağırıyor. Ertelenen işleyici işleme genellikle paketin fiziksel katman üst bilgisini (genellikle Ethernet) kaldırmayı ve bu NetX Duo alma işlevlerinden birini göndermeyi içerir:

- ***_nx_ip_packet_receive***
- ***_nx_arp_packet_deferred_receive***
- ***_nx_rarp_packet_deferred_receive***

## <a name="ethernet-headers"></a>Ethernet Üst Bilgileri 

Ethernet Üst Bilgileri için IPv6 ile IPv4 arasındaki en önemli farklardan biri çerçeve türü ayarıdır. Paketleri gönderirken, Ethernet sürücüsü giden paketlerde Ethernet çerçeve türünü ayarlamadan sorumludur. IPv6 paketleri için çerçeve türü 0x86DD; IPv4 paketleri için çerçeve türü 0x0800.

Aşağıdaki kod kesimi bu işlemi göstermektedir:

```c
NX_PACKET *packet_ptr;
packet_ptr = driver_req_ptr -> nx_ip_driver_packet;
if (packet_ptr -> nx_packet_ip_version == NX_IP_VERSION_V4)
{

   /* Set Ethernet frame type to IPv4 /*
   ethernet_frame_ptr -> frame_type = 0x0800;

   /* Swap endian-ness for little endian targets.*/
   NX_CHANGE_USHORT_ENDIAN(ethernet_frame_ptr -> frame_type);
}
else if (packet_ptr -> nx_packet_ip_version == NX_IP_VERSION_V6)
{

   /* Set Ethernet frame type to IPv6. /*
   ethernet_frame_ptr -> frame_type = 0x86DD;

   /* Swap endian-ness for little endian targets.*/
   NX_CHANGE_USHORT_ENDIAN(ethernet_frame_ptr -> frame_type);
}
else
{

   /* Unknown IP version. Free the packet we will not send. */
   nx_packet_transmit_release(packet_ptr);
}
```
Benzer şekilde, gelen paketler için, Ethernet sürücüsü Ethernet çerçeve türünden paket türünü belirlemeli. IPv6 (0x86DD), IPv4 (0x0800), ARP (0x0806) ve RARP (0x8035) çerçeve türlerini kabul etmek için uygulanması gerekir.

## <a name="example-ram-ethernet-network-driver"></a>Örnek RAM Ethernet Ağ Sürücüsü

NetX Duo tanıtım sistemi, nx_ram_network_driver.c dosyasında tanımlanan ram ***tabanlı küçük bir ağ sürücüsüyle birlikte teslim edilir.*** Bu sürücü, IP örneklerinin hepsinin aynı ağ üzerinde olduğunu ve sanal donanım adreslerini (MAC adresleri) oluşturuldukları anda her cihaz örneğine atadığınız varsayır. Bu dosya NetX Duo fiziksel ağ sürücülerinin temel yapısına iyi bir örnek sağlar. Kullanıcılar bu örnekte sunulan sürücü çerçevesini kullanarak kendi ağ sürücülerini geliştirebilir.

Ağ sürücüsünün giriş işlevi ***_nx_ram_network_driver() ()** şeklindedir ve bu işlev IP örneği oluşturma çağrısına geçirildi. Ek ağ arabirimleri için giriş işlevleri _nx_ip_interface_attach()* hizmetine geçirebilirsiniz. IP örneği çalışmaya başladıktan sonra, cihazı başlatmak ve etkinleştirmek için sürücü girdisi işlevi çağrılır (cihazı başlatmak ve etkinleştirmek için **NX_LINK_INITIALIZE** **ve NX_LINK_ENABLE).** NX_LINK_ENABLE **komutu** verdikten sonra cihazın paketleri iletmeye ve almaya hazır olması gerekir. 

IP örneği, ağ paketlerini şu komutlardan biri aracılığıyla iletir:

| Komut                         |  Açıklama                                                   |
| ------------------------------- | -------------------------------------------------------------- |
| ***NX_LINK_PACKET_SEND***    | Bir IPv4 veya IPv6 paketi iletildi,                   |
| ***NX_LINK_ARP_SEND***       | Bir ARP isteği veya ARP yanıt paketi iletildi,    |
| ***NX_LINK_ARP_RARP_SEND*** | Ters ARP isteği veya yanıt paketi iletildi, |

Bu komutları işlerken, ağ sürücüsünün uygun Ethernet çerçevesi üst bilgisini hazırlaması ve ardından iletim için temel alınan donanıma göndermesi gerekir. İletim işlemi sırasında ağ sürücüsü paket arabellek alanı için özel sahiplik sahibidir. Bu nedenle, veriler iletilmesinin ardından (veya veriler sürücü iç aktarım arabelleğine kopyalandıktan sonra), ağ sürücüsü önce ön uç işaretçisini Ethernet üst bilgisini IP üst bilgisine geçerek (ve paket uzunluğunu uygun şekilde ayarlayalım) ve ardından paketi serbest bırakmak için ***nx_packet_transmit_release()*** hizmetini çağırarak paket arabelleğinin serbest bırakılmasından sorumludur. Veri iletiminden sonra paketi serbest bırakmama, paketlerin sızıntıya neden olur.

Ağ cihazı sürücüsü de gelen veri paketlerinin işlenmesinden sorumludur. RAM sürücüsü örneğinde, alınan paket ***_nx_ram_network_driver_receive() işlevi tarafından işlenir.*** Cihaz bir Ethernet çerçevesi aldığında, sürücü verileri farklı bir yapıda NX_PACKET sorumludur. NetX Duo'da IP üst bilgisi 4 bayt hizalı adresten başladığı varsayıldı. Ethernet üst bilgisi uzunluğu 14bayt olduğu için, IP üst bilgisi 4 bayt hizalı adresle başladığından emin olmak için sürücünün Ethernet üst bilgisi başlatmayı 2 bayt hizalı adreste depolaması gerekir.