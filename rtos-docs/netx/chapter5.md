---
title: Bölüm 5-Azure RTOS NetX ağ sürücüleri
description: Bu bölümde, Azure RTOS NetX için ağ sürücülerine yönelik bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 09/11/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ccc55111d785d84cdb193c387830abbc03a15e7c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826854"
---
# <a name="chapter-5---netx-network-drivers"></a>Bölüm 5-NetX ağ sürücüleri

Bu bölüm NetX için ağ sürücülerine yönelik bir açıklama içerir. Sunulan bilgiler, geliştiricilerin Azure RTOS NetX için uygulamaya özel ağ sürücüleri yazmasına yardımcı olmak üzere tasarlanmıştır.

## <a name="driver-introduction"></a>Sürücü tanıtımı

NX_IP yapısı, tek bir IP örneğini yönetmek için her şeyi içerir. Bu, genel TCP/IP protokol bilgilerinin yanı sıra uygulamaya özgü fiziksel ağ sürücüsünün giriş yordamını da içerir. Sürücünün giriş yordamı ***nx_ip_create*** hizmeti sırasında tanımlanmıştır. ***Nx_ip_interface_attach*** HIZMETI aracılığıyla IP örneğine ek cihazlar eklenebilir.

NetX ve uygulamanın ağ sürücüsü arasındaki iletişim **NX_IP_DRIVER** istek yapısı aracılığıyla gerçekleştirilir. Bu yapı genellikle çağıranın yığınında yerel olarak tanımlanır ve bu nedenle sürücü ve çağırma işlevi dönüşden sonra serbest bırakılır. Yapı aşağıdaki gibi tanımlanır.

```C
typedef struct NX_IP_DRIVER_STRUCT
{
    UINT nx_ip_driver_command;
    UINT nx_ip_driver_status;
    ULONG nx_ip_driver_physical_address_msw;
    ULONG nx_ip_driver_physical_address_lsw;
    NX_PACKET *nx_ip_driver_packet;
    ULONG *nx_ip_driver_return_ptr;
    NX_IP *nx_ip_driver_ptr;
    NX_INTERFACE *nx_ip_driver_interface;
} NX_IP_DRIVER;
```

## <a name="driver-entry"></a>Sürücü girdisi

NetX sürücü başlatma ve paket gönderme ve ağ cihazını başlatma ve etkinleştirme dahil çeşitli denetim ve durum işlemleri için ağ sürücüsü girişi işlevini çağırır. NetX, _ *NX_IP_DRIVER** istek yapısındaki ***nx_ip_driver_command** _ alanını ayarlayarak ağ sürücüsüne komutlar verir. Sürücü girdisi işlevi aşağıdaki biçimdedir:

```C
VOID my_driver_entry(NX_IP_DRIVER *request);
```

## <a name="driver-requests"></a>Sürücü Istekleri

NetX, belirli bir komutla sürücü isteği oluşturur ve komutu yürütmek için sürücü girdisi işlevini çağırır. Her ağ sürücüsünün tek bir giriş işlevi olduğundan, NetX tüm istekleri sürücü isteği veri yapısı üzerinden yapar. Sürücü isteği veri yapısının ***nx_ip_driver_command*** üyesi (**NX_IP_DRIVER**) isteği tanımlar. Durum bilgileri, üye ***nx_ip_driver_status*** çağırana geri bildirilir. Bu alan **NX_SUCCESS**, sürücü isteği başarıyla tamamlandı.

NetX, sürücüye tüm erişimi seri hale getirir. Bu nedenle, sürücünün giriş işlevini zaman uyumsuz olarak çağıran birden çok iş parçacığını işlemesi gerekmez. Cihaz sürücüsü işlevinin IP mutex 'i kilitlemeli olarak yürütüldüğünü unutmayın. Bu nedenle, aygıt sürücüsü iç işlevi kendisini engelleyemez.

Genellikle cihaz sürücüsü kesmeleri de işler. Bu nedenle, tüm sürücü işlevlerinin kesme açısından güvenli olması gerekir.

### <a name="driver-initialization"></a>Sürücü başlatma

Asıl sürücü başlatma işlemi uygulamaya özgü olsa da, genellikle veri yapısı ve fiziksel donanım başlatma bilgisinden oluşur. Sürücü başlatma için NetX 'ten gereken bilgiler, IP üst bilgisi dahil olmak üzere IP katmanı yükünün kullanabildiği bayt sayısı olan IP en büyük aktarım birimi (MTU) ve fiziksel arabirimin mantıksal-fiziksel eşleme ihtiyacı varsa. Sürücü gerekiyor

_ *NX_INTERFACE** yapısındaki ***nx_interface_ip_mtu_size** _ içindeki değeri ayarlayarak arabirim MTU 'yu yapılandırmak için.

Cihaz sürücüsünün Ayrıca içindeki ***nx_ip_interface_address_mapping_needed*** değerini ayarlaması gerekir

Arabirim adresi eşlemesinin gerekli olup olmadığını NetX 'e bildirmek için **NX_INTERFACE** . Adres eşleme gerekiyorsa, arabirimi geçerli MAC adresiyle yapılandırmadan sorumludur ve MAC adresini NetX 'e sağlar.

Ağ sürücüsü NetX 'ten NX_LINK başlatma isteği aldığında, yukarıda gösterilen NX_IP_DRIVER isteği denetim bloğunun bir parçası olarak IP denetim bloğuna bir işaretçi alır.

Uygulama ***nx_ip_create*** çağrıldıktan sonra, IP Yardımcısı iş parçacığı, bir sürücü isteğini, bu komutun fiziksel ağ arabirimini başlatmak için sürücüye NX_LINK_INITIALIZE olarak ayarlanmış şekilde gönderir. Başlatma isteği için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

| NX_IP_DRIVER üyesi    | Anlamı |
|------------------------|-----------------------------------------------|
| nx_ip_driver_command   | NX_LINK_INITIALIZE |
| nx_ip_driver_ptr       | IP örneğine yönelik işaretçi. Sürücü işlevinin üzerinde çalışacağı IP örneğini bulabilmesi için bu değer sürücü tarafından kaydedilmelidir. |
| nx_ip_driver_interface | IP örneği içindeki ağ arabirimi yapısına yönelik işaretçi. Bu bilgilerin sürücü tarafından kaydedilmesi gerekir. Paket alındığında, sürücü, paketi yığın üzerine gönderirken arabirim yapısı bilgilerini kullanır. |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, belirtilen arabirimi IP örneğine başlatamayacak, sıfır dışında bir hata durumu döndürür.                                                                                           |


> [!IMPORTANT]
> *Sürücü komutlarının çoğu, IP örneği için oluşturulan IP Yardımcısı iş parçacığından çağırılır. Bu nedenle, sürücü yordamının engelleme işlemlerini gerçekleştirmekten kaçının veya IP Yardımcısı iş parçacığı, IP iş parçacığını kullanan uygulamalarda sınırsız gecikmelere neden olabilir.*

### <a name="enable-link"></a>Bağlantıyı etkinleştir  

Ardından, IP Yardımcısı iş parçacığı, sürücü isteğindeki NX_LINK_ENABLE ve isteği ağ sürücüsüne göndererek fiziksel ağa izin vermez. Bu, kısa süre önce IP Yardımcısı iş parçacığı başlatma isteğini tamamladıktan sonra gerçekleşir. Bağlantının etkinleştirilmesi, arabirim örneğindeki nx_interface_link_up alanını ayarlamak kadar basit olabilir. Ancak fiziksel donanımın işlemesini de içerebilir. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı etkinleştirme isteği için kullanılır.

| NX_IP_DRIVER üyesi    | Anlamı |
|------------------------|------------------------------------------|
| nx_ip_driver_command   | NX_LINK_ENABLE                                                                                                          |
| nx_ip_driver_ptr       | IP örneği işaretçisi                                                                                                  |
| nx_ip_driver_interface | Arabirim örneği işaretçisi                                                                                       |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü belirtilen arabirimi etkinleştiremeyebilir, sıfır olmayan bir hata durumu döndürür. |



### <a name="disable-link"></a>Bağlantıyı devre dışı bırak  

Bu istek, "**nx_ip_delete** _ hizmeti tarafından bir IP örneği silinirken NETX tarafından yapılır. Ya da bir uygulama, güç tasarrufu sağlamak için bağlantıyı geçici olarak devre dışı bırakmak üzere bu komutu verebilir. Bu hizmet, IP örneğindeki fiziksel ağ arabirimini devre dışı bırakır. Bağlantıyı devre dışı bırakma işlemi, _arabirim örneğindeki nx_interface_link_up * bayrağını temizlemek kadar kolay olabilir. Ancak fiziksel donanımın işlemesini de içerebilir. Genellikle, bu, ***bağlantıyı etkinleştirme** işleminin ters bir işlemidir_ . Bağlantı devre dışı bırakıldıktan sonra, arabirimi etkinleştirmek için uygulamanın _ *_bağlantıyı etkinleştir_** işlemini isteyin. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı devre dışı bırak isteği için kullanılır.

| NX_IP_DRIVER üyesi    | Anlamı |
|------------------------|--------------------------------------|
| nx_ip_driver_command   | NX_LINK_DISABLE |
| nx_ip_driver_ptr       | IP örneği işaretçisi |
| nx_ip_driver_interface | Arabirim örneği işaretçisi |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, IP örneğinde belirtilen arabirimi devre dışı bırakamadığından, sıfır olmayan bir hata durumu döndürür. |


### <a name="uninitialize-link"></a>Uninitialize bağlantısı  

Bu istek, ***nx_ip_delete*** hizmeti tarafından bir IP örneği silinirken NETX tarafından yapılır. Bu istek arabirimi Uninitialize ve başlatma aşamasında oluşturulan tüm kaynakları serbest bırakabilir. Genellikle ***bağlantı başlatma*** işleminin ters bir işlemidir. Arabirim geri alındıktan sonra, arabirim yeniden başlatılana kadar cihaz kullanılamaz.

Aşağıdaki NX_IP_DRIVER üyeleri bağlantı devre dışı bırak isteği için kullanılır.

| NX_IP_DRIVER üyesi  | Anlamı                |
|----------------------|------------------------|
| nx_ip_driver_command | NX_LINK_UNINITIALZE    |
| nx_ip_driver_ptr     | IP örneği işaretçisi |
| nx_ip_driver_interface | Arabirim örneği işaretçisi |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, belirtilen arabirimi IP örneğine Uninitialize, sıfır olmayan bir hata durumu döndürür. |


### <a name="packet-send"></a>Paket gönderme  

Bu istek, tüm NetX protokollerinin paketleri iletmek için kullanıldığı iç IP gönderme işlemi sırasında yapılır, işleme (ARP, RARP hariç). Paket Gönder komutunu alırken *nx_packet_prepend_ptr* gönderilecek paketin başlangıcını işaret eder ve bu IP üstbilgisinin başlangıcıdır.
*nx_packet_length* , aktarılan verilerin toplam boyutunu (bayt cinsinden) gösterir. *Nx_packet_next* geçerliyse, giden IP veri birimi birden çok pakette depolanır, sürücü zincirleme paketini izlemek ve tüm çerçeveyi iletmek için gereklidir. Her zincirleme paketindeki geçerli veri alanının *nx_packet_prepend_ptr* ve *nx_packet_append_ptr* arasında depolandığını unutmayın.

Fiziksel üst bilgi oluşturulurken sürücü sorumludur. IP adresi eşlemesinin fiziksel adresi gerekliyse (örneğin, Ethernet), IP katmanı MAC adresini zaten çözümledi. Hedef MAC adresi, *nx_ip_driver_physical_address_msw ve nx_ip_driver_physical_address_lsw* depolanan IP örneğinden geçirilir.

Fiziksel üstbilgi eklendikten sonra, paket gönderme işlemi daha sonra paketin iletilmesi için sürücünün Çıkış işlevini çağırır.

Aşağıdaki NX_IP_DRIVER üyeleri paket gönderme isteği için kullanılır.

| NX_IP_DRIVER üyesi               | Anlamı |
|-----------------------------------|---------------------------------------------------------------|
| nx_ip_driver_command              | NX_LINK_PACKET_SEND |
| nx_ip_driver_ptr                  | IP örneği işaretçisi |
| nx_ip_driver_packet               | Gönderilmek üzere paket işaretçisi |
| nx_ip_driver_interface            | Arabirim örneğine yönelik işaretçi.             |
| nx_ip_driver_physical_address_msw | En önemli 32 bitlik fiziksel adres (yalnızca fiziksel eşleme gerekliyse) |
| nx_ip_driver_physical_address_lsw | En az önemli 32-fiziksel adres (yalnızca fiziksel eşleme gerekliyse)    |
| nx_ip_driver_status               | Tamamlanma durumu. Sürücü paketi gönderemediği takdirde, sıfır olmayan bir hata durumu döndürür.  |

### <a name="packet-broadcast"></a>Paket yayını  
Bu istek, paket gönderme isteğiyle neredeyse aynıdır. Tek fark, hedef fiziksel adres alanlarının Ethernet yayını MAC adresine ayarlanmamanızdır. Aşağıdaki NX_IP_DRIVER üyeleri paket yayını isteği için kullanılır.

| NX_IP_DRIVER üyesi                | Anlamı          |
|------------------------------------|--------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_PACKET_BROADCAST |
| nx_ip_driver_ptr                   | IP örneği işaretçisi  |
| nx_ip_driver_packet                | Paketin sonuna kadar işaretçisi |
| nx_ip_driver_physical_address_ms w | 0x0000FFFF yayını) |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF yayını) |
| nx_ip_driver_interface             | Arabirim örneğine yönelik işaretçi. |
| nx_ip_driver_status                | Tamamlanma durumu. Sürücü paketi gönderemediği takdirde, sıfır olmayan bir hata durumu döndürür. |

### <a name="arp-send"></a>ARP gönderme  

Bu istek, IP paketi gönderme isteğine de benzer.
Tek fark, Ethernet üstbilgisinin IP paketi yerine bir ARP paketi belirttiğinden ve hedef fiziksel adres alanlarının MAC yayın adresi olarak ayarlandığı bir farktır. ARP gönderme isteği için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

| **NX_IP_DRIVER üyesi** | **Anlamı** |
| --- | --- |
| nx_ip_driver_command | NX_LINK_ARP_SEND |
| nx_ip_driver_ptr | IP örneği işaretçisi. |
| nx_ip_driver_packet | Gönderecek paketin işaretçisi. |
| nx_ip_driver_physical_address_msw | 0x0000FFFF (yayın) |
| nx_ip_driver_physical_address_lsw | 0xFFFFFFFF (yayın) |
| nx_ip_driver_interface | Arabirim örneğine yönelik işaretçi. |
| nx_ip_driver_status | Tamamlanma durumu. Sürücü ARP paketini gönderemez, sıfır olmayan bir hata durumu döndürür. |

*Fiziksel eşleme gerekmiyorsa, bu isteğin uygulanması gerekli değildir.*

### <a name="arp-response-send"></a>ARP yanıtı gönderme  

Bu istek ARP gönderme paketi isteğiyle neredeyse aynıdır. Tek fark, hedef fiziksel adres alanlarının IP örneğinden geçirilme örneğidir. Aşağıdaki NX_IP_DRIVER üyeleri ARP yanıtı gönderme isteği için kullanılır.

| NX_IP_DRIVER üyesi               | Anlamı |
|-----------------------------------| ------------------------------------|
| nx_ip_driver_command              | NX_LINK_ARP_RESPONSE_SEND |
| nx_ip_driver_ptr                  | IP örneği işaretçisi |
| nx_ip_driver_packet               | Gönderilmek üzere paket işaretçisi|
| nx_ip_driver_physical_address_msw | En önemli 32-fiziksel adres-bit |
| nx_ip_driver_physical_address_lsw | En az önemli 32-fiziksel adres bitleri                     |
| nx_ip_driver_interface            | Arabirim örneği işaretçisi |
| nx_ip_driver_status               | Tamamlanma durumu. Sürücü ARP paketini gönderemez, sıfır olmayan bir hata durumu döndürür. |

> [!NOTE]
> *Fiziksel eşleme gerekmiyorsa, bu isteğin uygulanması gerekli değildir.*

### <a name="rarp-send"></a>RARP gönderme  

Bu istek ARP gönderme paketi isteğiyle neredeyse aynıdır. Tek farklar paket üstbilgisinin türüdür ve fiziksel hedef, her zaman bir yayın adresi olduğundan fiziksel adres alanları gerekli değildir.

Aşağıdaki NX_IP_DRIVER üyeleri, RARP gönderme isteği için kullanılır.

| NX_IP_DRIVER üyesi               | Anlamı |
|-----------------------------------|---------------------------------|
| nx_ip_driver_command              |NX_LINK_RARP_SEND |
| nx_ip_driver_ptr                  | IP örneği işaretçisi |
| nx_ip_driver_packet               | Gönderilmek üzere paket işaretçisi |
| nx_ip_driver_physical_address_msw | 0x0000FFFF (yayın) |
| nx_ip_driver_physical_address_lsw | 0xFFFFFFFF (yayın) |
| NX_IP_DRIVER üyesi               | Anlamı |
| nx_ip_driver_interface            | Arabirim örneği işaretçisi |
| nx_ip_driver_status               | Tamamlanma durumu. Sürücü, RARP paketini gönderemez, sıfır olmayan bir hata durumu döndürür.  |

> [!NOTE]
> *RARP hizmeti gerektiren uygulamaların bu komutu uygulaması gerekir.*

### <a name="multicast-group-join"></a>Çok noktaya yayın grubuna ekleme  

Bu istek ***nx_igmp_multicast_interface JOIN*** hizmeti ile yapılır. Ağ sürücüsü, sağlanan çok noktaya yayın grubu adresini alır ve fiziksel medyayı bu çok noktaya yayın grubu adresinden gelen paketleri kabul edecek şekilde ayarlar. Çok noktaya yayın filtresini desteklemeyen sürücüler için, sürücü alma mantığının karışık modda olması gerekebileceğini unutmayın. Bu durumda, sürücünün hedef MAC adresine göre gelen çerçeveleri filtrelemeniz ve böylece IP örneğine geçirilen trafik miktarını azaltmasının gerekebilir. Aşağıdaki NX_IP_DRIVER üyeleri çok noktaya yayın grubu JOIN isteği için kullanılır.

| NX_IP_DRIVER üyesi               | Anlamı |
|-----------------------------------|-----------------------------------------------------------------------|
| nx_ip_driver_command              | NX_LINK_MULTICAST_JOIN                                                |
| nx_ip_driver_ptr                  | IP örneği işaretçisi                                                |
| nx_ip_driver_physical_address_msw | En önemli 32-fiziksel çok noktaya yayın adresi                |
| nx_ip_driver_physical_address_lsw | En az önemli 32-fiziksel çok noktaya yayın adresi               |
| nx_ip_driver_interface            | Arabirim örneği işaretçisi                                     |
| nx_ip_driver_status               | Tamamlanma durumu. Sürücü çok noktaya yayın grubuna katılamayabilir, sıfır olmayan bir hata durumu döndürür. |


### <a name="multicast-group-leave"></a>Çok noktaya yayın grubu bırakma  

Bu istek, ***nx_igmp_multicast_leave*** hizmeti açıkça çağırarak çağrılır. Sürücü, sağlanan Ethernet çok noktaya yayın adresini çok noktaya yayın listesinden kaldırır. Bir konak bir çok noktaya yayın grubuna ayrıldıktan sonra, ağ üzerindeki bu Ethernet çok noktaya yayın adresine sahip paketler artık bu IP örneği tarafından alınmaz. Aşağıdaki NX_IP_DRIVER üyeleri çok noktaya yayın grubu bırakma isteği için kullanılır.

| NX_IP_DRIVER üyesi               | Anlamı |
|-----------------------------------|-----------------------------------------------------------------|
| nx_ip_driver_command              | NX_LINK_MULTICAST_LEAVE |
| nx_ip_driver_ptr                  | IP örneği işaretçisi |
| nx_ip_driver_physical_address_msw | En önemli 32 BITS fiziksel çok noktaya yayın adresi |
| nx_ip_driver_physical_address_lsw | En az 32 bit fiziksel çok noktaya yayın adresi |
| nx_ip_driver_interface            | Arabirim örneği işaretçisi |
| nx_ip_driver_status               | Tamamlanma durumu. Sürücü çok noktaya yayın grubunu bırakılamayan, sıfır olmayan bir hata durumu döndürür. |


### <a name="attach-interface"></a>Arabirim Ekle  

Bu istek NetX 'ten cihaz sürücüsüne çağrılır, sürücünün sürücü örneğini karşılık gelen IP örneğiyle ve IP içindeki fiziksel arabirim örneğiyle ilişkilendirebilmesine izin verir. Arabirim Ekle isteği için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

| NX_IP_DRIVER üyesi    | Anlamı |
|------------------------|-------------------------------------------------|
| nx_ip_driver_command   | X_LINK_INTERFACE_ATTACH |
| nx_ip_driver_ptr       | IP örneği işaretçisi |
| nx_ip_driver_interface | Arabirim örneğine yönelik işaretçi. |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, belirtilen arabirimi IP örneğine ayıramayabilir, sıfır olmayan bir hata durumu döndürür.  |


### <a name="detach-interface"></a>Arabirimi ayır  

Bu istek, cihaz sürücüsüne NetX tarafından çağrılır ve sürücünün sürücü örneğinin IP 'nin karşılık gelen IP örneğiyle ve fiziksel arabirim örneğiyle ilişkilendirmesini sağlar. Arabirim Ekle isteği için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

| NX_IP_DRIVER üyesi    | Anlamı |
|------------------------|---------------------------------------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_DETACH |
| nx_ip_driver_ptr       | IP örneği işaretçisi |
| nx_ip_driver_interface | Arabirim örneğine yönelik işaretçi. |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, belirtilen arabirimi IP örneğine iliştiremez, sıfır olmayan bir hata durumu döndürür. |

### <a name="get-link-status"></a>Bağlantı durumunu al  

Uygulama, konaktaki herhangi bir arabirim için NetX Service  ***nx_ip_interface_status_check*** hizmetini kullanarak ağ arabirimi bağlantı durumunu sorgulayabilir. Bu hizmetlerle ilgili daha fazla bilgi için bkz. sayfa 107, "NetX Services açıklaması" başlıklı Bölüm.

Bağlantı durumu, *nx_ip_driver_interface* işaretçisine göre işaret edilen NX_INTERFACE yapısındaki *nx_interface_link_up* alanında bulunur. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı durumu isteği için kullanılır.

| NX_IP_DRIVER üyesi     | Anlamı                                                                                                      |
|-------------------------|--------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_STATUS                                                                                           |
| nx_ip_driver_ptr        | IP örneği işaretçisi                                                                                       |
| nx_ip_driver_return_ptr | Durumu yerleştirilecek hedefe yönelik işaretçi.                                                              |
| nx_ip_driver_interface  | Arabirim örneği işaretçisi                                                                            |
| nx_ip_driver_status     | Tamamlanma durumu. Sürücü belirli bir durum alamazsanız, sıfır olmayan bir hata durumu döndürür. |
|                         |                                                                                                              |

> [!NOTE]
> ***nx_ip_status_check** , birincil arabirimin durumunu denetlemek için hala kullanılabilir. Ancak, uygulama geliştiricilerinin arabirime özgü hizmet nx_ip_interface_status_check kullanması önerilir **.***

### <a name="get-link-speed"></a>Bağlantı hızını al  

Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, belirtilen hedefte bağlantının hat hızını depolar. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı hattı hız isteği için kullanılır.

| NX_IP_DRIVER üyesi     | Anlamı |
|-------------------------|---------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_SPEED |
| nx_ip_driver_ptr        | IP örneği işaretçisi |
| nx_ip_driver_return_ptr | Satır hızını yerleştirmek için hedefin işaretçisi |
| nx_ip_driver_interface  | Arabirim örneği işaretçisi |
| nx_ip_driver_status     | Tamamlanma durumu. Sürücü hız bilgilerini alamazsanız, sıfır olmayan bir hata durumu döndürür.
 |


> [!NOTE]
> *Bu istek NetX tarafından dahili olarak kullanılmadığından, uygulamasının uygulanması isteğe bağlıdır.*

### <a name="get-duplex-type"></a>Çift yönlü tür al  

Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının çift yönlü türünü sağlanan hedefte depolar. Aşağıdaki NX_IP_DRIVER üyeleri çift yönlü tür isteği için kullanılır.

| NX_IP_DRIVER üyesi     | Anlamı |
|-------------------------|-----------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_DUPLEX_TYPE |
| nx_ip_driver_ptr        | IP örneği işaretçisi |
| nx_ip_driver_return_ptr | Çift yönlü türü yerleştirmek için hedefin işaretçisi |
| nx_ip_driver_interface  | Arabirim örneği işaretçisi |
| nx_ip_driver_status     | Tamamlanma durumu. Sürücü çift yönlü bilgileri alamazsanız, sıfır dışında bir hata durumu döndürür.
 |


> [!NOTE]
> *Bu istek NetX tarafından dahili olarak kullanılmadığından, uygulamasının uygulanması isteğe bağlıdır.*

### <a name="get-error-count"></a>Hata sayısını Al  

Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının hata sayısını sağlanan hedefte depolar. Bu özelliği desteklemek için sürücünün işlem hatalarını izlemesi gerekir. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı hata sayısı isteği için kullanılır.

| NX_IP_DRIVER üyesi     | Anlamı                                                                                                  |
|-------------------------|----------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_ERROR_COUNT                                                                                  |
| nx_ip_driver_ptr        | IP örneği işaretçisi                                                                                   |
| nx_ip_driver_return_ptr | Hata sayısını yerleştirmek için hedefin işaretçisi                                                      |
| nx_ip_driver_interface  | Arabirim örneği işaretçisi                                                                        |
| nx_ip_driver_status     | Tamamlanma durumu. Sürücü hata sayısını alamazsanız, sıfır olmayan bir hata durumu döndürür. |


> [!NOTE]
> *Bu istek NetX tarafından dahili olarak kullanılmadığından, uygulamasının uygulanması isteğe bağlıdır.*

### <a name="get-receive-packet-count"></a>Alma paketi sayısını Al  

Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının alma paketi sayısını sağlanan hedefte depolar. Bu özelliği desteklemek için sürücünün alınan paket sayısını izlemesi gerekir. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı alma paketi sayısı isteği için kullanılır.

| NX_IP_DRIVER üyesi     | Anlamı                                                                                                    |
|-------------------------|------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_RX_COUNT                                                                                       |
| nx_ip_driver_ptr        | IP örneği işaretçisi                                                                                     |
| nx_ip_driver_return_ptr | Alma paketi sayısını yerleştirmek için hedefin işaretçisi                                               |
| nx_ip_driver_interface  | Fiziksel ağ arabirimine yönelik işaretçi                                                                  |
| nx_ip_driver_status     | Tamamlanma durumu. Sürücü alma sayısı alamadıysanız, sıfır olmayan bir hata durumu döndürür. |


> [!NOTE]
> *Bu istek NetX tarafından dahili olarak kullanılmadığından, uygulamasının uygulanması isteğe bağlıdır.*

### <a name="get-transmit-packet-count"></a>Iletme paketi sayısını Al  

Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının aktarım paketi sayısını sağlanan hedefte depolar. Bu özelliği desteklemek için sürücünün her bir arabirimde ilettiği her bir paketi izlemesi gerekir. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı iletme paketi sayısı isteği için kullanılır.

| NX_IP_DRIVER üyesi     | Anlamı                                                                                                     |
|-------------------------|-------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_GET_TX_COUNT                                                                                        |
| nx_ip_driver_ptr        | IP örneği işaretçisi                                                                                      |
| nx_ip_driver_return_ptr | İletme paketi sayısını yerleştirmek için hedefin işaretçisi                                               |
| nx_ip_driver_interface  | Arabirim örneği işaretçisi                                                                           |
| nx_ip_driver_status     | Tamamlanma durumu. Sürücü, iletim sayısını alamıyor, sıfır olmayan bir hata durumu döndürür. |


> [!NOTE]
> *Bu istek NetX tarafından dahili olarak kullanılmadığından, uygulamasının uygulanması isteğe bağlıdır.*

### <a name="get-allocation-errors"></a>Ayırma hatalarını al  

Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının paket havuzu ayırma hata sayısını sağlanan hedefte depolar. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı ayırma hata sayısı isteği için kullanılır.

| **NX_IP_DRIVER üyesi** | **Anlamı** |
| --- | ---|
| nx_ip_driver_command | NX_LINK_GET_ALLOC_ERRORS |
| nx_ip_driver_ptr | IP örneği işaretçisi |

| NX_IP_DRIVER üyesi     | Anlamı                                                                                                        |
|-------------------------|----------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_return_ptr | Ayırma hata sayısını yerleştirmek için hedefin işaretçisi                                                 |
| nx_ip_driver_interface  | Arabirim örneği işaretçisi                                                                              |
| nx_ip_driver_status     | Tamamlanma durumu. Sürücü ayırma hatalarını alamazsanız, sıfır olmayan bir hata durumu döndürür. |


*Bu istek NetX tarafından dahili olarak kullanılmadığından, uygulamasının uygulanması isteğe bağlıdır.*

### <a name="driver-deferred-processing"></a>Sürücü ertelenmiş Işleme  

Bu istek, bir iletme veya alma ıSR 'den _ ***nx_ip_driver_deferred_processing*** yordamını çağıran sürücüye yanıt olarak IP Yardımcısı iş parçacığından yapılır. Bu, sürücü ıSR 'nin paket alma ve aktarım işlemeyi IP Yardımcısı iş parçacığına erteetmesine olanak tanır ve bu sayede, ıSR 'de işlem miktarını azaltır. *Nx_ip_driver_interface* tarafından işaret edilen NX_INTERFACE yapısındaki *nx_interface_additional_link_info* alanı, sürücü tarafından IP Yardımcısı iş parçacığı bağlamından ertelenmiş işleme olayı hakkında bilgi depolamak için kullanılabilir. Ertelenmiş işleme olayı için aşağıdaki NX_IP_DRIVER üyeleri kullanılır.

**NX_IP_DRIVER**

| üye                 | Anlamı                           |
|------------------------|-----------------------------------|
| nx_ip_driver_command   | NX_LINK_DEFERRED_PROCESSING       |
| nx_ip_driver_ptr       | IP örneği işaretçisi            |
| nx_ip_driver_interface | Arabirim örneği işaretçisi |


### <a name="user-commands"></a>Kullanıcı komutları  

Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü uygulamaya özgü Kullanıcı komutlarını işler. Aşağıdaki NX_IP_DRIVER üyeleri Kullanıcı komut isteği için kullanılır.

| NX_IP_DRIVER üyesi     | Anlamı                                                                                                        |
|-------------------------|----------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command    | NX_LINK_USER_COMMAND                                                                                           |
| nx_ip_driver_ptr        | IP örneği işaretçisi                                                                                         |
| nx_ip_driver_return_ptr | Kullanıcı tanımlı                                                                                                   |
| nx_ip_driver_interface  | Arabirim örneği işaretçisi                                                                              |
| nx_ip_driver_status     | Tamamlanma durumu. Sürücü, Kullanıcı komutlarını yürütemediğinde, sıfır olmayan bir hata durumu döndürür. |


*Bu istek NetX tarafından dahili olarak kullanılmadığından, uygulamasının uygulanması isteğe bağlıdır.*

### <a name="unimplemented-commands"></a>Uygulanmayan komutlar  

Ağ sürücüsü tarafından uygulanmayan komutların geri dönüş durumu alanı NX_UNHANDLED_COMMAND olarak ayarlanmalıdır.

## <a name="driver-output"></a>Sürücü çıkışı  

Daha önce bahsedilen tüm paket iletme istekleri, sürücüde uygulanan bir çıkış işlevi gerektirir. Belirli bir iletme mantığı donanıma özeldir, ancak genellikle paketin hemen gönderilmesi için donanım kapasitesini denetlemesinin oluşur. Mümkünse, paket yükü (ve paket zincirindeki ek yükleri) bir veya daha fazla donanım gönderme arabelleğine yüklenir ve bir iletme işlemi başlatılır. Paket, kullanılabilir iletim arabelleklerine uymuyorsa, paketin kuyruğa alınması ve iletim arabelleklerinin kullanılabilir hale gelmesi durumunda iletilmesi gerekir.

Önerilen iletim kuyruğu, hem baş hem de tail işaretçilerine sahip olan listedir bağlantılı bir listesidir. Yeni paketler sıranın sonuna eklenir ve en eski paketin ön tarafında tutulması sağlanır. *Nx_packet_queue_next* alanı, paketin sıradaki sonraki bağlantısı olarak kullanılır. Sürücü, iletme sırasının baş ve kuyruklu işaretçilerini tanımlar.

*Bu kuyruğa, sürücünün iş parçacığından ve kesme bölümlerinden erişildiği için, kesme koruması sıra işlemelerinin çevresine yerleştirilmelidir.*

Fiziksel donanım uygulamalarının çoğu, paket iletimi tamamlandıktan sonra bir kesme üretir.
Sürücü böyle bir kesme aldığında, genellikle yalnızca iletilmekte olan paketle ilişkili kaynakları serbest bırakır. Aktarım mantığının verileri NX_PACKET arabelleğinden doğrudan okuduğu durumlarda, sürücü, ilet Tamam kesmesi ile ilişkili paketi kullanılabilir paket havuzuna yeniden yayınlamak için ***nx_packet_transmit_release*** hizmetini kullanmalıdır. Daha sonra sürücü, gönderilmesi bekleyen ek paketlere yönelik iletim sırasını inceler. Donanım iletme arabelleklerine sığan sıraya alınmış iletim paketlerinin birçoğu sıraya alınır ve arabelleklere yüklenir. Bu, başka bir gönderme işleminin başlatılması ile izlenir.

NX_PACKET veriler, (veya bir sürücü sıfırlama işlemini destekliyorsa), nx_packet_transmit_release çağrılmadan önce, sürücünün nx_packet_prepend_ptr IP üst bilgisinin başına taşınması gerekir), bu durumda sürücü, çağrılmadan önce NX_PACKET ***.*** *Nx_packet_length* alanını uygun şekilde ayarlamayı unutmayın. Bir IP çerçevesi birden çok paketten yapılırsa, yalnızca paket zincirinin kafa bırakılması gerekir.

## <a name="driver-input"></a>Sürücü girişi  

Alınan bir paket kesmesi alındıktan sonra, ağ sürücüsü paketi fiziksel donanım alma arabelleklerinden alır ve geçerli bir NetX paketi oluşturur. Geçerli bir NetX paketi oluşturmak, uygun uzunluk alanını ayarlamayı ve gelen paketin boyutu tek bir paket yükünden daha büyükse birden çok paketi birlikte zincirlemeyi içerir. Düzgün derlendikten sonra prepend_ptr fiziksel katman üst bilgisi ve alma paketi NetX 'e gönderildikten sonra taşınır.

NetX, IP ve ARP üstbilgilerinin bir ULONG sınırında hizalandığını varsayar. Bu nedenle NetX sürücüsü olmalıdır. Ethernet ortamlarında bu, paketin başından Ethernet üst bilgisi iki bayt başlatılarak yapılır. *Nx_packet_prepend_ptr* Ethernet üstbilgisinin dışına taşındığında, temeldeki IP veya ARP üstbilgisi 4byte hizalı olur.

NetX 'te sunulan birkaç alma paketi işlevi vardır. Alınan paket bir ARP paketidir, _* **nx_arp_packet_deferred_receive**_ çağırılır. Alınan paket bir RARP paketi ise, _ _*_nx_rarp_packet_deferred_receive_*_ çağrılır. Gelen IP paketlerini işlemek için çeşitli seçenekler vardır. IP paketlerinin en hızlı şekilde yönetilmesi için _ _*_nx_ip_packet_receive_*_ çağrılır. Bu yaklaşım en az yüke sahiptir, ancak sürücünün alma kesme hizmeti işleyicisinde (ıSR) daha fazla işlem gerektirir. En az ıSR işleme __ *_nx_ip_packet_deferred_receive_** çağırılır.

Yeni alma paketi düzgün derlendikten sonra, fiziksel donanımın Alma arabellekleri daha fazla veri alacak şekilde ayarlanır. Bu, NetX paketleri ayırmayı ve yük adresini donanım alma arabelleğine yerleştirmeyi gerektirebilir veya donanım alma arabelleğindeki bir ayarı değiştirmek yalnızca miktar olabilir. Taşma olasılıklarını en aza indirmek için, bir paket alındıktan sonra donanımın Alım arabelleklerinin kullanılabilir arabellekler olması önemlidir.

*İlk alma arabellekleri, sürücü başlatma sırasında ayarlanır.*

### <a name="deferred-receive-packet-handling"></a>Ertelenmiş alma paketi Işleme  

Sürücü, alma paketi işlemini NetX IP Yardımcısı iş parçacığına erteedebilir. Bazı uygulamalarda, bu, ıSR işleminin yanı sıra bırakılan paketleri de en aza indirmek için gerekli olabilir. Ertelenmiş paket işlemeyi kullanmak için, önce NetX Kitaplığı ***NX_DRIVER_DEFERRED_PROCESSING** _ tanımlı ile derlenmelidir. Bu, ertelenen paket mantığını NetX IP Yardımcısı iş parçacığına ekler. Sonra, bir veri paketi alındığında sürücü __nx_ip_packet_deferred_receive () öğesini çağırmalıdır:*

```C
_nx_ip_packet_deferred_receive(ip_ptr, packet_ptr);
```

Ertelenmiş alma işlevi, *packet_ptr* tarafından temsil edilen alma PAKETINI bir FIFO (bağlantılı liste) olarak koyar ve IP Yardımcısı iş parçacığına bildirir. Yürütmeden sonra, IP Yardımcısı kaldı her ertelenmiş paketi işlemek için ertelenmiş işleme işlevini çağırır. Ertelenmiş işleyici işleme genellikle paketin fiziksel katman üst bilgisini (genellikle Ethernet) kaldırmayı ve bu NetX alma işlevlerinden birine bağlamayı içerir:  

***_nx_ip_packet_deferred_receive***  
***_nx_arp_packet_deferred_receive***  
***_nx_rarp_packet_deferred_receive*** 


## <a name="example-ram-ethernet-network-driver"></a>Örnek RAM Ethernet ağ sürücüsü  

NetX tanıtım sistemi, ***nx_ram_network_driver. c*** dosyasında tanımlanan küçük bir RAM tabanlı ağ sürücüsüyle birlikte dağıtılır.
Bu sürücü, IP örneklerinin aynı ağ üzerinde olduğunu varsayar ve her bir cihaz örneğine sanal donanım adreslerini (MAC adresleri) oluşturuldukları şekilde atar. Bu dosya, NetX fiziksel ağ sürücülerinin temel yapısına iyi bir örnek sağlar. Kullanıcılar, bu örnekte sunulan sürücü çerçevesini kullanarak kendi ağ sürücülerini geliştirebilir.

Ağ sürücüsünün giriş işlevi, "**_nx_ram_network_driver,** _ ve IP örneği oluşturma çağrısı ' ne geçirilir. Ek ağ arabirimleri için giriş işlevleri _*_nx_ip_interface_attach_*_ hizmetine geçirilebilir. IP örneği çalışmaya başladıktan sonra, cihazı başlatmak ve etkinleştirmek için sürücü girdisi işlevi çağrılır (Bu durum _ *NX_LINK_INITIALIZE** ve **NX_LINK_ENABLE**). **NX_LINK_ENABLE** komutu verildikten sonra, cihaz paketleri iletmeye ve almaya hazırlanmalıdır. 

IP örneği şu komutlardan biri aracılığıyla ağ paketlerini iletir:

| ***NX_LINK_PACKET_SEND***    | Bir IP paketi aktarılıyor,                             |
| ------------------------------- | -------------------------------------------------------------- |
| ***NX_LINK_ARP_SEND***       | Bir ARP isteği veya ARP yanıt paketi iletiliyor,    |
| ***NX_LINK_ARP_RARP_SEND*** | Ters ARP isteği veya yanıt paketi iletiliyor, |

Bu komutları işlerken, ağ sürücüsünün uygun Ethernet çerçeve üst bilgisini eklemesi ve ardından iletim için temel alınan donanıma gönderilmesi gerekir. İletim işlemi sırasında, ağ sürücüsü paket arabelleği alanının dışlamalı sahipliğine sahiptir. Bu nedenle, veriler aktarıldıktan sonra (veya veriler, iç aktarım arabelleğine kopyalandıktan sonra), önce paket arabelleğini serbest bırakmaktan önce, ilk olarak Ethernet üst bilgisini IP üstbilgisine taşıyarak (ve paket uzunluğunu buna uygun olarak ayarlayarak) ve ardından paketi serbest bırakmak için ***nx_packet_transmit_release*** hizmetini çağırarak paket arabelleğini yayınlamaktan sorumludur. Veri iletimi paketlerin sızmasına neden olduktan sonra paketin serbest bırakılmamasına neden olur.

Ağ aygıtı sürücüsü, gelen veri paketlerini işlemekten de sorumludur. RAM sürücüsü örneğinde, alınan paket ***_nx_ram_network_driver_receive*** işlevi tarafından işlenir.

Cihaz bir Ethernet çerçevesini aldıktan sonra, bu sürücü, verilerin depolanmasından

NX_PACKET yapısı. NetX 'in IP üstbilgisinin 4 baytlık hizalanmış adresten başlayacağını varsaydığını unutmayın. Ethernet üstbilgisinin uzunluğu 14 bayt olduğundan, IP üstbilgisinin 4 baytlık hizalanmış adreste başlamasını sağlamak için sürücünün Ethernet üstbilgisinin başlangıcını 2 baytlık hizalanmış adreste depolaması gerekir.