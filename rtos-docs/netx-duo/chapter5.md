---
title: Bölüm 5 - Azure RTOS NetX Duo Ağ Sürücüleri
description: Bu bölümde NetX Duo için ağ sürücülerinin Azure RTOS yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7d30e14ce1865e2fbce4a6e00cff787c859b32be
ms.sourcegitcommit: 20a136b06a25e31bbde718b4d12a03ddd8db9051
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2021
ms.locfileid: "123552424"
---
# <a name="chapter-5---azure-rtos-netx-duo-network-drivers"></a>Bölüm 5 - Azure RTOS NetX Duo Ağ Sürücüleri

Bu bölümde NetX Duo için ağ sürücülerinin Azure RTOS yer almaktadır. Sunulan bilgiler, geliştiricilerin NetX Duo için uygulamaya özgü ağ sürücüleri yazmalarına yardımcı olmak üzere tasarlanmıştır.

## <a name="driver-introduction"></a>Sürücü Tanıtımı

Bu NX_IP, tek bir IP örneğini yönetmek için gereken her şeyi içerir. Bu, genel TCP/IP protokolü bilgilerini ve uygulamaya özgü fiziksel ağ sürücüsünün giriş yordamını içerir. Sürücünün giriş yordamı * nx_ip_create **_** hizmeti sırasında tanımlanır. IP örneğine _ nx_ip_interface_attach * hizmeti *_aracılığıyla ek_* cihazlar eklenebilir.

NetX Duo ile uygulamanın ağ sürücüsü arasındaki iletişim, istek yapısına **NX_IP_DRIVER** gerçekleştirildi. Bu yapı genellikle çağıranın yığınında yerel olarak tanımlanır ve bu nedenle sürücü ve çağrı işlevi dönüşü sonrasında serbest bırakılabilir. Yapı aşağıdaki gibi tanımlanır.

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
## <a name="driver-entry"></a>Sürücü Girdisi 

NetX Duo, sürücü başlatma ve paket gönderme ile ağ cihazı başlatma ve etkinleştirme gibi çeşitli denetim ve durum işlemleri için ağ sürücüsü giriş işlevini çağırır. NetX Duo, _ NX_IP_DRIVER * istek **yapısında*** nx_ip_driver_command _ alanını *ayar NX_IP_DRIVER* sürücüye komut verir. Sürücü girişi işlevi aşağıdaki biçime sahiptir:

```c
VOID my_driver_entry(NX_IP_DRIVER *request);
```
## <a name="driver-requests"></a>Sürücü İstekleri

NetX Duo, sürücü isteğini belirli bir komutla oluşturur ve komutu yürütmek için driver entry işlevini çağırır. Her ağ sürücüsünün tek bir giriş işlevi olduğundan, NetX Duo tüm istekleri sürücü isteği veri yapısı üzerinden yapar. sürücü **nx_ip_driver_command** yapısının üyesi olan *_NX_IP_DRIVER**), isteği tanımlar. Durum bilgileri, * veya üyesinde *_çağırana nx_ip_driver_status._*_ Bu alan _*NX_SUCCESS** ise, sürücü isteği başarıyla tamamlandı.

NetX Duo sürücüye tüm erişimi seri hale getirme. Bu nedenle, sürücünün giriş işlevini zaman uyumsuz olarak çağıran birden çok iş parçacığını işlemesi gerek yoktur. Cihaz sürücüsü işlevinin IP mutex kilitli olarak yürütülmektedir. Bu nedenle cihaz sürücüsü iç işlevi kendisini engellemez.

Genellikle cihaz sürücüsü kesintileri de işler. Bu nedenle tüm sürücü işlevlerinin kesintiye karşı güvenli olması gerekir.

### <a name="driver-initialization"></a>Sürücü Başlatma   
Gerçek sürücü başlatma işlemi uygulamaya özgü olsa da, genellikle veri yapısı ve fiziksel donanım başlatmadan oluşur. Sürücü başlatma için NetX Duo'dan gereken bilgiler, IP katmanı yükü için kullanılabilir bayt sayısı (IPv4 veya IPv6 üst bilgisi dahil) ve fiziksel arabirimin mantıksal-fiziksel eşlemeye ihtiyacı olup olmadığını ifade eden IP Maksimum İletim Birimidir (MTU). Sürücü, nx_ip_interface_mtu_set çağırarak arabirim MTU ***değerini nx_ip_interface_mtu_set.***

NetX Duo'ya arabirim **adresi eşlemenin gerekli olup olmadığını bildirmek** için cihaz sürücüsünün * nx_ip_interface_address_mapping_configure _ çağrısında olması gerekir. Adres eşlemesi gerekirse, sürücü arabirimi geçerli MAC adresiyle yapılandırmak ve MAC adresini _* veya **ile NetX'e _sağlamak nx_ip_interface_physical_address_set_ sorumludur.

Ağ sürücüsü NetX Duo'dan NX_LINK INITIALIZE isteğini aldığında, yukarıda gösterilen istek denetim bloğuyla birlikte IP NX_IP_DRIVER işaretçisini alır.

Uygulama tarafından ***nx_ip_create*** sonra, IP yardımcı iş parçacığı fiziksel ağ arabirimini başlatmak için sürücüye NX_LINK_INITIALIZE olarak ayarlanmış bir sürücü isteği gönderir. Aşağıdaki NX_IP_DRIVER başlatma isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye | Anlamı    |
| ------------------------- | ----------------------------- |
| nx_ip_driver_command   | NX_LINK_INITIALIZE    |
| nx_ip_driver_ptr       | IP örneğinin işaretçisi. Sürücü işlevinin üzerinde çalışan IP örneğini bulması için bu değer sürücü tarafından kaydedilebilir.    |
| nx_ip_driver_interface | IP örneği içindeki ağ arabirimi yapısına işaretçi. Bu bilgiler sürücü tarafından kaydedilebilir. Paket alırken sürücü, paketi yığına gönderirken arabirim yapısı bilgilerini kullansın. Arabirim dizini (cihaz dizini) bu veri yapısının içindeki üye nx_interface_index okunarak elde edilir. |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü IP örneğine belirtilen arabirimi başlataamadığında sıfır olmayan bir hata durumu döndürür. |


> [!NOTE]  
> *Sürücü, IP örneği için oluşturulan IP yardımcı iş parçacığından çağrılır. Bu nedenle, sürücü yordamı* engelleme işlemleri gerçekleştirmekten kaçınmalıdır veya IP yardımcı iş parçacığı durarak IP iş parçacığına bağlı uygulamalarda sınırsız gecikmelere neden olabilir.

### <a name="enable-link"></a>Bağlantıyı Etkinleştir   
Ardından, IP yardımcı iş parçacığı sürücü komutunu sürücü isteğinde varsayılan olarak NX_LINK_ENABLE ve isteği ağ sürücüsüne göndererek fiziksel ağı etkinleştirir. Bu, IP yardımcı iş parçacığı başlatma isteğini tamamlandıktan kısa bir süre sonra gerçekleşir. Bağlantının etkinleştirilmesi, arabirim örneğinde nx_interface_link_up *ayarını* yapmak kadar basit olabilir. Ancak fiziksel donanımın da işlemesi de olabilir. Aşağıdaki NX_IP_DRIVER bağlantı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye       | Anlamı                      |
| ------------------------- | ---------------------------- |
| nx_ip_driver_command   | NX_LINK_ENABLE   |
| nx_ip_driver_ptr       | IP örneğine işaretçi  |
| nx_ip_driver_interface | Arabirim örneğinin işaretçisi |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü belirtilen arabirimi etkinleştirenene kadar sıfır olmayan bir hata durumu döndürür. |

### <a name="disable-link"></a>Bağlantıyı Devre Dışı Bırak   
Bu istek, * nx_ip_delete _ hizmeti tarafından IP örneği **silinerek** NetX Duo tarafından yapılır. Veya bir uygulama, güç tasarrufu yapmak için bağlantıyı geçici olarak devre dışı bırakmak için bu komutu da verdi. Bu hizmet IP örneğinde fiziksel ağ arabirimini devre dışı bırakıyor. Bağlantıyı devre dışı bırakma işlemi, arabirim örneğinde _nx_interface_link_up* bayrağını temizlemek kadar basit olabilir. Ancak fiziksel donanımın da işlemesi de olabilir. Genellikle * Bağlantıyı Etkinleştir işlemi ters **bir işlemdir.**_ Bağlantı devre dışı bırakılmıştır, uygulama arabirimini etkinleştirmek için _ *_Bağlantıyı Etkinleştir_** işlemi isteğinde ılmıştır.

Aşağıdaki NX_IP_DRIVER devre dışı bırakma bağlantısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye     | Anlamı                      |
| ------------------------- | ---------------------------- |
| nx_ip_driver_command   | NX_LINK_DISABLE    |
| nx_ip_driver_ptr       | IP örneğine işaretçi   |
| nx_ip_driver_interface | Arabirim örneğinin işaretçisi   |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü IP örneğinde belirtilen arabirimi devre dışı bırakamasa sıfır olmayan bir hata durumu döndürür. |

### <a name="uninitialize-link"></a>Bağlantıyı Uninitialize   
Bu istek, * nx_ip_delete _ hizmeti tarafından IP örneği **silinerek** NetX Duo tarafından yapılır. Bu istek arabirimi başlatmayı geri alar ve başlatma aşamasında oluşturulan tüm kaynakları serbest bırakın. Genellikle _ Initialize Link * işlemi *_ters bir_* işlemdir. Arabirim başlatılmamış hale getirildikten sonra, arabirim yeniden başlatılana kadar cihaz kullanılamaz.

Aşağıdaki NX_IP_DRIVER devre dışı bırakma bağlantısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye    | Anlamı                  |
|------------------------|--------------------------|
| nx_ip_driver_command   | NX_LINK_UNINITIALZE      |
| nx_ip_driver_ptr       | IP örneğine işaretçi   |
| nx_ip_driver_interface | Arabirim örneğinin işaretçisi |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü, belirtilen arabirimi IP örneğine geri getirene kadar sıfır olmayan bir hata durumu döndürür. |

### <a name="packet-send"></a>Paket Gönderme   
Bu istek, tüm NetX Duo protokollerin paketleri iletmek için (ARP, RARP hariç) kullanmak üzere dahili IPv4 veya IPv6 gönderme işlemi sırasında yapılır. Paket gönderme komutunu alırken, *nx_packet_prepend_ptr* gönderilecek paketin başlangıcına (IPv4 veya IPv6 üst bilgisi) gösterir. *nx_packet_length* aktarılan verilerin toplam boyutunu (bayt cinsinden) gösterir. Geçerli *nx_packet_next,* giden IP veri birimi birden çok pakette depolanır, sürücünün zincirli paketi izlemesi ve çerçevenin tamamını iletmesi gerekir. Her zincirli pakette geçerli veri alanı, ile nx_packet_prepend_ptr *arasında* *nx_packet_append_ptr.*

Sürücü, fiziksel üst bilgi oluşturmakla sorumludur. IP adresine fiziksel adres eşlemesi gerekli ise (Ethernet gibi), IP katmanı MAC adresini zaten çözümledi. Hedef MAC adresi, ip örneğinden geçirilecek, nx_ip_driver_physical_address_msw *ve nx_ip_driver_physical_address_lsw.*

Fiziksel üst bilgi ekledikten sonra paket gönderme işlemi, paketi iletmek için sürücünün çıkış işlevini çağırmıştır.

Aşağıdaki NX_IP_DRIVER paket gönderme isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye              | Anlamı                               |
| -----------------------------------| --------------------------------------|
| nx_ip_driver_command            | NX_LINK_PACKET_SEND                |
| nx_ip_driver_ptr                | IP örneğine işaretçi                |
| nx_ip_driver_packet             | Göndermek için paket işaretçisi         |
| nx_ip_driver_interface          | Arabirim örneğinin işaretçisi.    |
| nx_ip_driver_physical_address_msw | En önemli 32 bit fiziksel adres (yalnızca fiziksel eşleme gerektiğinde) |
| nx_ip_driver_physical_address_lsw | En az önemli 32 bit fiziksel adres (yalnızca fiziksel eşleme gerektiğinde) |
| nx_ip_driver_status             | Tamamlanma durumu. Sürücü paketi gönderenene kadar sıfır olmayan bir hata durumu döndürür. |

### <a name="packet-broadcastipv4-packets-only"></a>Paket Yayını (yalnızca IPv4 paketleri)  
Bu istek, paket gönderme isteğiyle neredeyse aynıdır. Tek fark, hedef fiziksel adres alanlarının Ethernet yayını MAC adresine ayarlanmış olduğudur. Aşağıdaki NX_IP_DRIVER yayın isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye                | Anlamı                                                                                                  |
|------------------------------------|----------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_PACKET_BROADCAST                                                                                 |
| nx_ip_driver_ptr                   | IP örneğine işaretçi                                                                                   |
| nx_ip_driver_packet                | Göndermek için paket işaretçisi                                                                            |
| nx_ip_driver_physical_address_ms | 0x0000FFFF (yayın)                                                                                   |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (yayın)                                                                                   |
| nx_ip_driver_interface             | Arabirim örneğinin işaretçisi.                                                                       |
| nx_ip_driver_status                | Tamamlanma durumu. Sürücü paketi gönderenene kadar sıfır olmayan bir hata durumu döndürür. |

### <a name="arp-send"></a>ARP Gönderme  
Bu istek, IP paketi gönderme isteğine de benzer. Tek fark Ethernet üst bilgisi IP paketi yerine bir ARP paketi belirtir ve hedef fiziksel adres alanları MAC yayın adresi olarak ayarlanır. Aşağıdaki NX_IP_DRIVER ARP gönderme isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye                | Anlamı                                                                                                      |
|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_ARP_SEND                                                                                             |
| nx_ip_driver_ptr                   | IP örneğine işaretçi                                                                                       |
| nx_ip_driver_packet                | Göndermek için paket işaretçisi                                                                                |
| nx_ip_driver_physical_address_ms | 0x0000FFFF (yayın)                                                                                       |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (yayın)                                                                                       |
| nx_ip_driver_interface             | Arabirim örneğinin işaretçisi.                                                                           |
| nx_ip_driver_status                | Tamamlanma durumu. Sürücü ARP paketini gönderenene kadar sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Fiziksel eşleme gerekli yoksa, bu isteğin uygulanması gerekli değildir.*

ARP, IPv6'da Komşu Bulma Protokolü ve Yönlendirici Bulma Protokolü ile değiştirilmiş olsa da, Ethernet ağ sürücüleri hala IPv4 eşleri ve yönlendiricilerle *uyumlu olmalıdır. Bu nedenle, sürücülerin yine de ARP paketlerini işlemesi gerekir.*

### <a name="arp-response-send"></a>ARP Yanıt Gönderme  
Bu istek, ARP paket gönderme isteğiyle neredeyse aynıdır. Tek fark, hedef fiziksel adres alanlarının IP örneğinden geçirilecekleridir. Aşağıdaki NX_IP_DRIVER ARP yanıt gönderme isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye                  | Anlamı                                  |
| -------------------------------------- | -----------------------------------------|
| nx_ip_driver_command                | NX_LINK_ARP_RESPONSE_SEND            |
| nx_ip_driver_ptr                    | IP örneğine işaretçi   |
| nx_ip_driver_packet                 | Göndermek için paket işaretçisi          |
| nx_ip_driver_physical_address_msw | En önemli 32 bit fiziksel adres |
| nx_ip_driver_physical_address_lsw | En az önemli 32 bit fiziksel adres |
| nx_ip_driver_interface              | Arabirim örneğinin işaretçisi |
| nx_ip_driver_status                 | Tamamlanma durumu. Sürücü ARP paketini gönderenene kadar sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Fiziksel eşleme gerekli yoksa, bu isteğin uygulanması gerekli değildir.*

### <a name="rarp-send"></a>RARP Gönderme   
Bu istek, ARP paket gönderme isteğiyle neredeyse aynıdır. Tek fark paket üst bilgisi türü ve fiziksel adres alanları gerekli değildir çünkü fiziksel hedef her zaman bir yayın adresidir.

Aşağıdaki NX_IP_DRIVER RARP gönderme isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye                | Anlamı                                                                                                       |
|------------------------------------|---------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command               | NX_LINK_RARP_SEND                                                                                             |
| nx_ip_driver_ptr                   | IP örneğine işaretçi                                                                                        |
| nx_ip_driver_packet                | Göndermek için paket işaretçisi                                                                                 |
| nx_ip_driver_physical_address_ms | 0x0000FFFF (yayın)                                                                                        |
| nx_ip_driver_physical_address_lsw  | 0xFFFFFFFF (yayın)                                                                                        |
| nx_ip_driver_interface             | Arabirim örneğinin işaretçisi.                                                                            |
| nx_ip_driver_status                | Tamamlanma durumu. Sürücü RARP paketini gönderenene kadar sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *RARP hizmeti gerektiren uygulamalar bu komutu uygulamalı.*

### <a name="multicast-group-join"></a>Çok Noktaya Yayın Grubu Birleştirme   
Bu istek IPv4'te ***nx_igmp_multicast_interface join** _ _*_ve nx_ipv4_multicast_interface_join_*_ hizmeti, IPv6'da _ *_nxd_ipv6_multicast_interface_join_** hizmeti ve IPv6 için gereken çeşitli işlemle yapılır. Ağ sürücüsü sağlanan çok noktaya yayın grubu adresini alır ve bu çok noktaya yayın grubu adresine gelen paketleri kabul etmek için fiziksel medyayı ayarlar. Çok noktaya yayın filtresini desteklemeen sürücüler için sürücünün alma mantığının açık modda olması gerekebilirsiniz. Bu durumda, sürücünün gelen kareleri hedef MAC adresine göre filtrelemesi, böylece IP örneğine geçirilen trafik miktarını azaltması gerekir. Aşağıdaki NX_IP_DRIVER çok noktaya yayın grubu birleştirme isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye                  | Anlamı                                 |
| -------------------------------------- | --------------------------------------- |
| nx_ip_driver_command                | NX_LINK_MULTICAST_JOIN               |
| nx_ip_driver_ptr                    | IP örneğine işaretçi  |
| nx_ip_driver_physical_address_msw | En önemli 32 bit fiziksel çok noktaya yayın adresi |
| nx_ip_driver_physical_address_lsw | En az önemli 32 bit fiziksel çok noktaya yayın adresi |
| nx_ip_driver_interface              | Arabirim örneğinin işaretçisi |
| nx_ip_driver_status                 | Tamamlanma durumu. Sürücü çok noktaya yayın grubuna katılayamasa sıfır olmayan bir hata durumu döndürür. |

> [!NOTE]  
> *IPv6 uygulamaları, adres yapılandırması gibi ICMPv6 tabanlı protokoller için sürücüde çok noktaya yayının uygulanmasını gerektirir. Ancak, IPv4 uygulamaları için, çok noktaya yayın özellikleri gerekli yoksa bu isteğin uygulanması gerekmez.*

> [!IMPORTANT]  
> *IPv6 etkinleştirilmediyse ve çok* noktaya yayın özellikleri IPv4 tarafından gerekli yoksa, bu isteğin uygulanması gerekmez.

### <a name="multicast-group-leave"></a>Çok Noktaya Yayın Grubu Bırakma  
Bu istek, IPv4'te ***nx_igmp_multicast_interface_leave** _ _*_veya nx_ipv4_multicast_interface_leave_*_ hizmetleri, IPv6'da _ *_nxd_ipv6_multicast_interface_leave_** hizmeti açıkça çağrılarak veya IPv6 için gereken çeşitli iç NetX Duo işlemleri tarafından çağrılır. Sürücü sağlanan Ethernet çok noktaya yayın adresini çok noktaya yayın listesinden kaldırır. Bir konak çok noktaya yayın grubundan ayrıldıktan sonra, ağ üzerinde bu Ethernet çok noktaya yayın adresine sahip paketler artık bu IP örneği tarafından alınamaz. Aşağıdaki NX_IP_DRIVER, çok noktaya yayın grubu bırakma isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye              | Anlamı                              |
| -----------------------------------| -------------------------------------|
| nx_ip_driver_command            | NX_LINK_MULTICAST_LEAVE           |
| nx_ip_driver_ptr                | IP örneğine işaretçi   |
| nx_ip_driver_physical_address_msw | En önemli 32 bit fiziksel çok noktaya yayın adresi |
| nx_ip_driver_physical_address_lsw | En az önemli 32 bit fiziksel çok noktaya yayın adresi |
| nx_ip_driver_interface              | Arabirim örneğinin işaretçisi |
| nx_ip_driver_status                 | Tamamlanma durumu. Sürücü çok noktaya yayın grubundan ayrılamasa, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *IPv4 veya IPv6 için çok noktaya yayın özellikleri gerekmiyorsa, bu isteğin uygulanması gerekmez.*

### <a name="attach-interface"></a>Arabirim Ekleme  
Bu istek NetX Duo'dan cihaz sürücüsüne çağrılır ve sürücünün sürücü örneğini ilgili IP örneğiyle ve IP içindeki fiziksel arabirim örneğiyle ilişkilendirmesini sağlar. Aşağıdaki NX_IP_DRIVER ekleme arabirimi isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye    | Anlamı                  |
|------------------------|--------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_ATTACH |
| nx_ip_driver_ptr       | IP örneğine işaretçi   |
| nx_ip_driver_interface | Arabirim örneğinin işaretçisi.|
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü belirtilen arabirimi IP örneğine ayıramasa, sıfır olmayan bir hata durumu döndürür. |

### <a name="detach-interface"></a>Arabirimi Ayırma    
Bu istek NetX Duo tarafından cihaz sürücüsüne çağrılır ve sürücünün sürücü örneğini ilgili IP örneğiyle ve IP'nin içindeki fiziksel arabirim örneğiyle ilişkilendirilmemiş olarak kabul sınar. Aşağıdaki NX_IP_DRIVER ekleme arabirimi isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye    | Anlamı                                                                                                                                    |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| nx_ip_driver_command   | NX_LINK_INTERFACE_DETACH                                                                                                                   |
| nx_ip_driver_ptr       | IP örneğine işaretçi                                                                                                                     |
| nx_ip_driver_interface | Arabirim örneğinin işaretçisi.                                                                                                         |
| nx_ip_driver_status    | Tamamlanma durumu. Sürücü belirtilen arabirimi IP örneğine ekleyemezse sıfır olmayan bir hata durumu döndürür. |

### <a name="get-link-status"></a>Bağlantı Durumunu Al    
Uygulama, ana bilgisayar üzerinde herhangi bir arabirim için NetX Duo ***nx_ip_interface_status_check*** ağ arabirimi bağlantı durumunu sorgular. Bu hizmetlerle ilgili daha fazla bilgi için 149. sayfada 4. Bölüm olan "NetX Duo Services'in Açıklaması" sayfasına bakın.

Bağlantı durumu, nx_interface_link_up *işaretçisi* tarafından işaret NX_INTERFACE yapının *nx_ip_driver_interface* içerir. Aşağıdaki NX_IP_DRIVER bağlantı durumu isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye       | Anlamı                  |
| --------------------------- | -------------------------|
| nx_ip_driver_command     | NX_LINK_GET_STATUS    |
| nx_ip_driver_ptr         | IP örneği işaretçisi   |
| nx_ip_driver_return_ptr | Durumu yerleştirilecek hedefe yönelik işaretçi. |
| nx_ip_driver_interface   | Arabirim örneği işaretçisi   |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü belirli bir durum alamazsanız, sıfır olmayan bir hata durumu döndürür. |

> [!NOTE]  
> ***nx_ip_status_check** _, birincil arabirimin durumunu denetlemek için hala kullanılabilir. Ancak, uygulama geliştiricilerinin arabirime özgü hizmeti kullanması önerilir: _ *_nx_ip_interface_status_check._**

### <a name="get-link-speed"></a>Bağlantı hızını al  
Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, belirtilen hedefte bağlantının hat hızını depolar. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı hattı hız isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi   | Anlamı                   |
| ------------------------| ------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_SPEED          |
| nx_ip_driver_ptr         | IP örneği işaretçisi                                                                                         |
| nx_ip_driver_return_ptr | Satır hızını yerleştirmek için hedefin işaretçisi                                                             |
| nx_ip_driver_interface   | Arabirim örneği işaretçisi                                                                              |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü hız bilgilerini alamazsanız, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu Istek NetX Duo tarafından dahili olarak kullanılmadığından, uygulamanın isteğe bağlı olması önerilir*.

### <a name="get-duplex-type"></a>Çift yönlü tür al   
Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının çift yönlü türünü sağlanan hedefte depolar. Aşağıdaki NX_IP_DRIVER üyeleri çift yönlü tür isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi   | Anlamı                                                                                                    |
| --------------------------- | -------------------------------------------------------------------------------------------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_DUPLEX_TYPE                                                                                    |
| nx_ip_driver_ptr         | IP örneği işaretçisi                                                                                         |
| nx_ip_driver_return_ptr | Çift yönlü türü yerleştirmek için hedefin işaretçisi                                                            |
| nx_ip_driver_interface   | Arabirim örneği işaretçisi                                                                              |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü çift yönlü bilgileri alamazsanız, sıfır dışında bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu Istek NetX Duo tarafından dahili olarak kullanılmadığından, uygulamanın isteğe bağlı olması önerilir*.

### <a name="get-error-count"></a>Hata sayısını Al   
Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının hata sayısını sağlanan hedefte depolar. Bu özelliği desteklemek için sürücünün işlem hatalarını izlemesi gerekir. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı hata sayısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi   | Anlamı                   |
| --------------------------- | -------------------------------|
| nx_ip_driver_command     | NX_LINK_GET_ERROR_COUNT   |
| nx_ip_driver_ptr         | IP örneği işaretçisi   |
| nx_ip_driver_return_ptr | Hata sayısını yerleştirmek için hedefin işaretçisi |
| nx_ip_driver_interface   | Arabirim örneği işaretçisi|
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü hata sayısını alamazsanız, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]
> *Bu Istek NetX Duo tarafından dahili olarak kullanılmadığından, uygulamanın isteğe bağlı olması önerilir*.

### <a name="get-receive-packet-count"></a>Alma paketi sayısını Al    
Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının alma paketi sayısını sağlanan hedefte depolar. Bu özelliği desteklemek için sürücünün alınan paket sayısını izlemesi gerekir. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı alma paketi sayısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi       | Anlamı                        |
| --------------------------- | -------------------------------|
| nx_ip_driver_command     | NX_LINK_GET_RX_COUNT      |
| nx_ip_driver_ptr         | IP örneği işaretçisi  |
| nx_ip_driver_return_ptr | Alma paketi sayısını yerleştirmek için hedefin işaretçisi   |
| nx_ip_driver_interface   | Fiziksel ağ arabirimine yönelik işaretçi  |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü alma sayısı alamadıysanız, sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu Istek NetX Duo tarafından dahili olarak kullanılmadığından, uygulamanın isteğe bağlı olması önerilir*.

### <a name="get-transmit-packet-count"></a>Iletme paketi sayısını Al   
Bu istek ***nx_ip_driver_direct_command*** hizmeti içinden yapılır. Sürücü, bağlantının aktarım paketi sayısını sağlanan hedefte depolar. Bu özelliği desteklemek için sürücünün her bir arabirimde ilettiği her bir paketi izlemesi gerekir. Aşağıdaki NX_IP_DRIVER üyeleri bağlantı iletme paketi sayısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üyesi   | Anlamı                   |
| ----------------------- | ------------------------- |
| nx_ip_driver_command | NX_LINK_GET_TX_COUNT  |
| nx_ip_driver_ptr     | IP örneği işaretçisi    |
| nx_ip_driver_return_ptr | İletme paketi sayısını yerleştirmek için hedefin işaretçisi  |
| nx_ip_driver_interface   | Arabirim örneğinin işaretçisi   |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü aktarım sayısını alamayacaksa sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu istek NetX Duo tarafından dahili olarak kullanılmaz, bu nedenle uygulaması isteğe bağlıdır.*

### <a name="get-allocation-errors"></a>Ayırma Hatalarını Al   
Bu istek, hizmetten ***nx_ip_driver_direct_command*** yapılır. Sürücü, bağlantının paket havuzu ayırma hata sayısını sağlanan hedefte depolar. Aşağıdaki NX_IP_DRIVER ayırma hata sayısı isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye       | Anlamı                       |
| --------------------------- | ----------------------------- |
| nx_ip_driver_command     | NX_LINK_GET_ALLOC_ERRORS  |
| nx_ip_driver_ptr         | IP örneğine işaretçi     |
| nx_ip_driver_return_ptr | Ayırma hata sayısını yer alan hedefin işaretçisi  |
| nx_ip_driver_interface   | Arabirim örneğinin işaretçisi  |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü ayırma hatalarını alamayacaksa sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT]  
> *Bu istek NetX Duo tarafından dahili olarak kullanılmaz, bu nedenle uygulaması isteğe bağlıdır.*

### <a name="driver-deferred-processing"></a>Sürücü Ertelenmiş İşleme    
Bu istek, bir iletme veya alma ISR'sinde nx_ip_driver_deferred_processing çağıran sürücüye yanıt olarak IP yardımcı iş parçacığından yapılır. _*_ Bu, sürücü ISR'nin paket alma ve iletme işlemini IP yardımcı iş parçacığına ertelemesini ve böylece ISR'de işlem miktarını azaltmasını sağlar. _nx_interface_additional_link_info tarafından işaret NX_INTERFACE* *alanı nx_ip_driver_interface* ip yardımcı iş parçacığı bağlamından ertelenen işleme olayıyla ilgili bilgileri depolamak için sürücü tarafından kullanılabilir. Aşağıdaki NX_IP_DRIVER ertelenen işleme olayı için kullanılır.

| NX_IP_DRIVER &nbsp; üye     | Anlamı                           |
| ------------------------- | --------------------------------- |
| nx_ip_driver_command   | NX_LINK_DEFERRED_PROCESSING    |
| nx_ip_driver_ptr       | IP örneğine işaretçi            |
| nx_ip_driver_interface | Arabirim örneğinin işaretçisi |

### <a name="set-physical-address"></a>Fiziksel Adresi Ayarla  
Bu istek * nx_ip_interface_physical_address_set **_** hizmetinin içinde yapılır. Bu hizmet, bir uygulamanın çalışma zamanında arabirim fiziksel adresini değiştirmesini sağlar. Bu komutu aldıktan sonra, sürücünün ağ arabiriminin donanım adresini sağlanan fiziksel adrese yeniden yapılandırması gerekir. IP örneği yeni adresine zaten sahip olduğu için, bu komuttan _ *_nx_ip_interface_address_set_** hizmetini çağırmaya gerek yoktur.

Aşağıdaki NX_IP_DRIVER kullanıcı komut isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye      | Anlamı                      |
| -------------------------- | ---------------------------- |
| nx_ip_driver_command    | NX_LINK_SET_PHYSICAL_ADDRESS  |
| nx_ip_driver_ptr        | IP örneğine işaretçi  |
| nx_ip_driver_interface  | Arabirim örneğinin işaretçisi   |
| nx_ip_driver_physical_ad dress_msw | Yeni fiziksel adresin en önemli 32 biti  |
| nx_ip_driver_physical_ad dress_lsw | Yeni fiziksel adresin en az önemli 32 biti  |
| nx_ip_driver_status                  | Tamamlanma durumu. Sürücü fiziksel adresi yeniden yapılandıramasa sıfır olmayan bir hata durumu döndürür. |

### <a name="user-commands"></a>Kullanıcı Komutları    
Bu istek, hizmetten ***nx_ip_driver_direct_command*** yapılır. Sürücü uygulamaya özgü kullanıcı komutlarını işler. Aşağıdaki NX_IP_DRIVER kullanıcı komut isteği için kullanılır.

| NX_IP_DRIVER &nbsp; üye       | Anlamı                       |
| --------------------------- | ----------------------------- |
| nx_ip_driver_command     | NX_LINK_USER_COMMAND       |
| nx_ip_driver_ptr         | IP örneğine işaretçi        |
| nx_ip_driver_return_ptr | Kullanıcı tanımlı       |
| nx_ip_driver_interface   | Arabirim örneğinin işaretçisi    |
| nx_ip_driver_status      | Tamamlanma durumu. Sürücü kullanıcı komutlarını yürütenene kadar sıfır olmayan bir hata durumu döndürür. |

> [!IMPORTANT] 
> *Bu istek NetX Duo tarafından dahili olarak kullanılmaz, bu nedenle uygulaması isteğe bağlıdır.*

### <a name="unimplemented-commands"></a>Uygulanmamış Komutlar  
Ağ sürücüsü tarafından uygulanmamış komutlarda dönüş durumu alanı varsayılan olarak NX_UNHANDLED_COMMAND.

## <a name="driver-capability"></a>Sürücü Özelliği

Bazı ağ arabirimleri sağlama süresi boşaltma özellikleri sunar. Cihaz sürücüleri, çeşitli sağlama süresi hesaplamalarını çalıştırmadan CPU süresinden yararlanmak için donanım hızlandırmalarından faydalanır.

Donanımdan donanım sağlamalarının destek düzeyine bağlı olarak, cihaz sürücüsünün IP örneğine hangi donanım özelliğinin etkin olduğunu bildirmesi gerekir. Bu şekilde IP örneği donanım özelliğinin farkındadır ve mümkün olduğunca fazla hesaplamayı donanıma devreder. Sürücü, fiziksel ***arabirimin nx_ip_interface_capability_set*** tüm özellikleri ayarlamak için API api'sini kullan gerekir.

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

Donanımda gerçekleştirilecek sağlama verileri hesaplaması için sürücünün donanım veya arabellek tanımlayıcılarını doğru şekilde ayarlaması gerekir; böylece giden paket sağlamaları donanım tarafından oluşturularak üst bilgiye eklenebilir. Paket alırken, donanım sağlama sağlamaları mantığı sağlama sağlama değerini doğrulayana kadar devam etmek zorunda. Sağlama değeri yanlışsa, alınan çerçeve atılmalıdır.

Donanımda sağlama toplamı hesaplaması gerçekleştirme özelliği de dahil olmak üzere, IP örneği sağlama toplamı özelliğini hala korur. Bazı senaryolarda, IPSec korumasından geçen bir UDP veri birimi gibi bazı senaryolarda, UDP çerçevesini yığına geçirmeden önce UDP sağlama toplamı yazılımda hesaplanmalıdır. Çoğu donanım sağlama toplamı özelliği, IPSec tarafından korunan bir veri segmenti için sağlama toplamı hesaplamasını desteklemez. Parçalanması gereken bir UDP veya ıCMP çerçevesi için, yazılımın UDP veya ıCMP sağlama toplamı 'nda hesaplanması gerekir. Çoğu donanım sağlama toplamı mantığı, verilerin birden çok çerçeveye bölündüğü durumu işlemez.

## <a name="driver-output"></a>Sürücü çıkışı  

Daha önce bahsedilen tüm paket iletme istekleri, sürücüde uygulanan bir çıkış işlevi gerektirir. Belirli bir iletme mantığı donanıma özeldir, ancak genellikle paketin hemen gönderilmesi için donanım kapasitesini denetlemesinin oluşur. Mümkünse, paket yükü (ve paket zincirindeki ek yükleri) bir veya daha fazla donanım gönderme arabelleğine yüklenir ve bir iletme işlemi başlatılır. Paket, kullanılabilir iletim arabelleklerine uymuyorsa, paketin kuyruğa alınması ve iletim arabelleklerinin kullanılabilir hale gelmesi durumunda iletilmesi gerekir.

Önerilen iletim kuyruğu, hem baş hem de tail işaretçilerine sahip olan listedir bağlantılı bir listesidir. Yeni paketler sıranın sonuna eklenir ve en eski paketin ön tarafında tutulması sağlanır. *Nx_packet_queue_next* alanı, paketin sıradaki sonraki bağlantısı olarak kullanılır. Sürücü, iletme sırasının baş ve kuyruklu işaretçilerini tanımlar.

> [!CAUTION]  
> *Bu kuyruğa, sürücünün iş parçacığından ve kesme bölümlerinden erişildiği için, kesme koruması sıra işlemelerinin çevresine yerleştirilmelidir*.

Fiziksel donanım uygulamalarının çoğu, paket iletimi tamamlandıktan sonra bir kesme üretir. Sürücü böyle bir kesme aldığında, genellikle yalnızca iletilmekte olan paketle ilişkili kaynakları serbest bırakır. Aktarım mantığının verileri NX_PACKET arabelleğinden doğrudan okuduğu durumlarda, sürücü, ilet Tamam kesmesi ile ilişkili paketi kullanılabilir paket havuzuna yeniden yayınlamak için ***nx_packet_transmit_release*** hizmetini kullanmalıdır. Daha sonra sürücü, gönderilmesi bekleyen ek paketlere yönelik iletim sırasını inceler. Donanım iletme arabelleklerine sığan sıraya alınmış iletim paketlerinin birçoğu sıraya alınır ve arabelleklere yüklenir. Bu, başka bir gönderme işleminin başlatılması ile izlenir.

NX_PACKET veriler, (veya bir sürücünün sıfır-kopyalama işlemini desteklemesi durumunda, NX_PACKET verileri iletilmiş olması durumunda), nx_packet_transmit_release çağrılmadan önce sürücünün *NX_PACKET_PREPEND_PTR* IP üstbilgisinin başına taşınması gerekir)**.** _ _Nx_packet_length * alanını uygun şekilde ayarlamayı unutmayın. Bir IP çerçevesi birden çok paketten yapılırsa, yalnızca paket zincirinin kafa bırakılması gerekir.

## <a name="driver-input"></a>Sürücü girişi

Alınan bir paket kesmesi alındıktan sonra, ağ sürücüsü paketi fiziksel donanım alma arabelleklerinden alır ve geçerli bir NetX Duo paketi oluşturur. Geçerli bir NetX Duo paketi oluşturmak, uygun uzunluk alanını ayarlamayı ve gelen paketin boyutu tek bir paket yükünden daha büyükse birden çok paketi birlikte zincirlemeyi içerir. Düzgün derlendikten sonra, *prepend_ptr* fiziksel katman üst bilgisi ve alma paketi NETX Duo 'a gönderilir.

NetX Duo, IP (IPv4 ve IPv6) ve ARP başlıklarının bir **ulong** sınırında hizalandığını varsayar. Bu nedenle NetX Duo sürücüsü, bu hizalamadan emin olmalıdır. Ethernet ortamlarında bu, paketin başından Ethernet üst bilgisi iki bayt başlatılarak yapılır. *Nx_packet_prepend_ptr* Ethernet üstbilgisinin dışına taşındığında, temeldeki IP (IPv4 ve IPv6) veya ARP üst bilgisi 4 bayt hizalı olur.

> [!WARNING] 
> *IPv6 ve IPv6 Ethernet üstbilgileri arasındaki önemli farklılıklar için aşağıdaki "Ethernet üstbilgileri" bölümüne bakın*.

NetX Duo içinde çeşitli alma paketi işlevleri mevcuttur. Alınan paket bir ARP paketidir, _* **nx_arp_packet_deferred_receive**_ çağırılır. Alınan paket bir RARP paketi ise, _ _*_nx_rarp_packet_deferred_receive_*_ çağrılır. Gelen IP paketlerini işlemek için çeşitli seçenekler vardır. IP paketlerinin en hızlı şekilde yönetilmesi için _ _*_nx_ip_packet_receive_*_ çağrılır. Bu yaklaşım en az yüke sahiptir, ancak sürücünün alma kesme hizmeti işleyicisinde (ıSR) daha fazla işlem gerektirir. En az ıSR işleme __ *_nx_ip_packet_deferred_receive_** çağırılır.

Yeni alma paketi düzgün derlendikten sonra, fiziksel donanımın Alma arabellekleri daha fazla veri alacak şekilde ayarlanır. Bu, NetX Duo paketleri ayırmayı ve yük adresini donanım alma arabelleğine yerleştirmeyi gerektirebilir veya donanım alma arabelleğindeki bir ayarı değiştirmek yalnızca miktar olabilir. Taşma olasılıklarını en aza indirmek için, bir paket alındıktan sonra donanımın Alım arabelleklerinin kullanılabilir arabellekler olması önemlidir.

> [!IMPORTANT] 
> *İlk alma arabellekleri, sürücü başlatma sırasında ayarlanır*.

### <a name="deferred-receive-packet-handling"></a>Ertelenmiş alma paketi Işleme  
Sürücü, alma paketi işlemini NetX Duo IP Yardımcısı iş parçacığına erteedebilir. Bazı uygulamalarda, bu, ıSR işleminin yanı sıra bırakılan paketleri de en aza indirmek için gerekli olabilir. 

Ertelenmiş paket işlemeyi kullanmak için, önce NetX Duo Kitaplığı ***NX_DRIVER_DEFERRED_PROCESSING** _ tanımlı ile derlenmelidir. Bu, ertelenen paket mantığını NetX Duo IP Yardımcısı iş parçacığına ekler. Sonra, bir veri paketi alındığında sürücü __nx_ip_packet_deferred_receive () öğesini çağırmalıdır:*

```c
_nx_ip_packet_deferred_receive(ip_ptr, packet_ptr);
```
Ertelenmiş alma işlevi, *packet_ptr* tarafından temsil edilen alma PAKETINI bir FIFO (bağlantılı liste) olarak koyar ve IP Yardımcısı iş parçacığına bildirir. Yürütmeden sonra, IP Yardımcısı kaldı her ertelenmiş paketi işlemek için ertelenmiş işleme işlevini çağırır. Ertelenmiş işleyici işleme genellikle paketin fiziksel katman üst bilgisini (genellikle Ethernet) kaldırmayı ve bu NetX Duo alma işlevlerinden birine bağlamayı içerir:

- ***_nx_ip_packet_receive***
- ***_nx_arp_packet_deferred_receive***
- ***_nx_rarp_packet_deferred_receive***

## <a name="ethernet-headers"></a>Ethernet üstbilgileri 

Ethernet üst bilgileri için IPv6 ve IPv4 arasındaki en önemli farklılıklardan biri çerçeve türü ayarıdır. Paket gönderirken, Ethernet sürücüsü giden paketlerde Ethernet çerçeve türünü ayarlamaktan sorumludur. IPv6 paketleri için çerçeve türü 0x86DD; olmalıdır. IPv4 paketleri için çerçeve türü 0x0800 olmalıdır.

Aşağıdaki kod segmenti bu süreci göstermektedir:

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
Benzer şekilde, gelen paketler için, Ethernet sürücüsü, Ethernet çerçeve türünden paket türünü belirlemelidir. IPv6 (0x86DD), IPv4 (0x0800), ARP (0x0806) ve RARP (0x8035) çerçeve türlerini kabul etmek için uygulanmalıdır.

## <a name="example-ram-ethernet-network-driver"></a>Örnek RAM Ethernet ağ sürücüsü

NetX Duo demo sistemi, ***nx_ram_network_driver. c*** dosyasında tanımlanan küçük bir RAM tabanlı ağ sürücüsüyle birlikte dağıtılır. Bu sürücü, IP örneklerinin aynı ağ üzerinde olduğunu varsayar ve her bir cihaz örneğine sanal donanım adreslerini (MAC adresleri) oluşturuldukları şekilde atar. Bu dosya, NetX Duo fiziksel ağ sürücülerinin temel yapısına iyi bir örnek sağlar. Kullanıcılar, bu örnekte sunulan sürücü çerçevesini kullanarak kendi ağ sürücülerini geliştirebilir.

Ağ sürücüsünün giriş işlevi, "**_nx_ram_network_driver (),** _ ve IP örneği oluşturma çağrısı ' ne geçirilir. Ek ağ arabirimleri için giriş işlevleri _nx_ip_interface_attach () * hizmetine geçirilebilir. IP örneği çalışmaya başladıktan sonra, cihazı başlatmak ve etkinleştirmek için sürücü girdisi işlevi çağrılır (durum **NX_LINK_INITIALIZE** ve **NX_LINK_ENABLE**). **NX_LINK_ENABLE** komutu verildikten sonra, cihaz paketleri iletmeye ve almaya hazırlanmalıdır. 

IP örneği şu komutlardan biri aracılığıyla ağ paketlerini iletir:

| Komut                         |  Açıklama                                                   |
| ------------------------------- | -------------------------------------------------------------- |
| ***NX_LINK_PACKET_SEND***    | Bir IPv4 veya IPv6 paketi iletiliyor,                   |
| ***NX_LINK_ARP_SEND***       | Bir ARP isteği veya ARP yanıt paketi iletiliyor,    |
| ***NX_LINK_ARP_RARP_SEND*** | Ters ARP isteği veya yanıt paketi iletiliyor, |

Bu komutları işlerken, ağ sürücüsünün uygun Ethernet çerçeve üst bilgisini eklemesi ve ardından iletim için temel alınan donanıma gönderilmesi gerekir. İletim işlemi sırasında, ağ sürücüsü paket arabelleği alanının dışlamalı sahipliğine sahiptir. Bu nedenle, veriler aktarıldıktan sonra (veya veriler iç aktarım arabelleğine kopyalandıktan sonra), önce paket arabelleğini serbest bırakmaktan önce, ilk olarak Ethernet üst bilgisini IP üstbilgisine taşıyarak (ve paket uzunluğunu uygun olarak ayarlayarak) ve ardından paketi serbest bırakmak için ***nx_packet_transmit_release ()*** hizmetini çağırarak paket arabelleğini yayınlamaktan sorumludur. Veri iletimi paketlerin sızmasına neden olduktan sonra paketin serbest bırakılmamasına neden olur.

Ağ aygıtı sürücüsü, gelen veri paketlerini işlemekten de sorumludur. RAM sürücüsü örneğinde, alınan paket ***_nx_ram_network_driver_receive ()*** işlevi tarafından işlenir. Cihaz bir Ethernet çerçevesini aldıktan sonra, verilerin NX_PACKET yapıda depolanmasından sürücü sorumludur. NetX Duo, IP üstbilgisinin 4 baytlık hizalanmış adresten başlayacağını varsaydığını unutmayın. Ethernet üstbilgisinin uzunluğu 14byte olduğundan, IP üstbilgisinin 4 baytlık hizalanmış adreste başlamasını sağlamak için sürücünün Ethernet üstbilgisinin başlangıcını 2 baytlık hizalanmış adreste depolaması gerekir.

## <a name="tcpip-offload-driver-guidance"></a>TCP/IP boşaltma sürücüsü kılavuzu
TCP/IP boşaltması özelliği için her IP arabirimi için bir sürücü işlevi gerekir. Ağ sürücüsüne yönelik ek görevlerin listesi aşağıda verilmiştir.

* Komut için `NX_LINK_INITIALIZE` ,
  * TCP/IP boşaltma alma olaylarını işlemek için bir sürücü iş parçacığı oluşturun.
* Komut için `NX_LINK_INTERFACE_ATTACH` ,
  * Özelliğini sürücü arabirimine ayarlayın. Aşağıdaki örnek koda bakın.
``` C
driver_req_ptr -> nx_ip_driver_interface -> nx_interface_capability_flag = NX_INTERFACE_CAPABILITY_TCPIP_OFFLOAD;
```
* Komut için `NX_LINK_ENABLE` ,
  * Sürücü iş parçacığını başlatın.
  * TCP/IP geri çağırma işlevini sürücü arabirimine ayarlayın. Aşağıdaki örnek koda bakın.
``` C
driver_req_ptr -> nx_ip_driver_interface -> nx_interface_tcpip_offload_handler = _nx_driver_tcpip_handler;
```
* Komut için `NX_LINK_DISABLE` ,
  * Sürücü iş parçacığını durdur
  * Sürücü arabiriminin TCP/IP geri çağırma işlevini temizleyin.
* Komut için `NX_LINK_UNINITIALIZE` ,
  * Sürücü iş parçacığını silme

### <a name="tcpip-offload-driver-thread"></a>TCP/IP boşaltma sürücüsü Iş parçacığı
Sürücü iş parçacığının amacı, gelen TCP veya UDP paketlerini almak için kullanılır. Sürücü iş parçacığında, genellikle gelen TCP veya UDP paketinin kullanılabildiğini veya bağlantısının yapılıp yapılmayacağını denetlemek için bir while döngüsü vardır. Veriler kullanılabilir olduğunda, TCP veya UDP paketini NetX Duo 'e geçirin. Ve arasındaki Oda `nx_packet_data_start` `nx_packet_prepend_ptr` TCP/IP üst bilgisini eklemek için yeterli olmalıdır. TCP soketi için, türü ile paket ayırın `NX_TCP_PACKET` . UDP soketi için, türü ile paket ayırın `NX_UDP_PACKET` . Gelen verileri ' den ' `nx_packet_append_ptr` e girin `nx_packet_data_end` . İçindeki verilerin `nx_packet_append_ptr` yalnızca TCP veya UDP yük içermesi gerekir. TCP/IP üst bilgisi, pakette doldurulmamış **olmalıdır** . Paket uzunluğunu ayarlayın ve alma arabirimini ayarlayın, ardından `_nx_tcp_socket_driver_packet_receive` TCP paketi ve UDP paketi için çağrı yapın `_nx_udp_socket_driver_packet_receive` . Bir TCP bağlantısı kapatıldıktan sonra `_nx_tcp_socket_driver_packet_receive` paket, null olarak ayarlanır. Bağlantı kurulduğu zaman çağırın `_nx_tcp_socket_driver_establish` .

### <a name="tcpip-offload-driver-handler"></a>TCP/IP boşaltması sürücü Işleyicisi
TCP/IP hizmetleriyle ağ arabirimleri için aşağıdaki sürücü komutları gereklidir. 
* İşlem için `NX_TCPIP_OFFLOAD_TCP_CLIENT_SOCKET_CONNECT` ,
  * Gerekirse kaynağı ayır.
  * Yerel TCP bağlantı noktasına bağlayın ve sunucuya bağlanın.
  * Bağlantıda başarılı döndürme durumu oluşturuldu. Bağlantı devam ederken, döndürün `NX_IN_PROGRESS` . Ya da başka bir hata döndürür.
* İşlem için `NX_TCPIP_OFFLOAD_TCP_SERVER_SOCKET_LISTEN` ,
  * Önce yinelenen dinlemeyi denetle. Aynı bağlantı noktasında birden çok kez çağrılabilir. İlk kez `nx_tcp_server_socket_listen` ve sonra `nx_tcp_server_socket_relisten` .
  * Gerekirse kaynağı ayır.
  * Yerel TCP bağlantı noktasını dinleyin.
* İşlem için `NX_TCPIP_OFFLOAD_TCP_SERVER_SOCKET_ACCEPT` ,
  * Gerekirse kaynağı ayır.
  * Bağlantıyı kabul et.
* İşlem için `NX_TCPIP_OFFLOAD_TCP_SERVER_SOCKET_UNLISTEN` ,
  * Yerel bağlantı noktasında dinleme yapan TCP yuvasını bulun.
  * Bulunursa dinleme yuvasını kapatın.
* İşlem için `NX_TCPIP_OFFLOAD_TCP_SOCKET_DISCONNECT` ,
  * TCP/IP boşaltma bağlantısını kapatın.
  * Yerel TCP bağlantı noktasının bağlantısını kaldır.
  * Bağlantı sırasında oluşturulan Temizleme kaynakları.
* İşlem için `NX_TCPIP_OFFLOAD_TCP_SOCKET_SEND` ,
  * TCP/IP boşaltma aracılığıyla veri gönderme. Paketler veya paket zinciri koşulundan daha büyük paket uzunluğunu işlemeye hazırlanmaya hazırlanın.
* İşlem için `NX_TCPIP_OFFLOAD_UDP_SOCKET_BIND` ,
  * Gerekirse kaynağı ayır.
  * Yerel UDP bağlantı noktasına bağlayın.
* İşlem için `NX_TCPIP_OFFLOAD_UDP_SOCKET_UNBIND` ,
  * Yerel UDP bağlantı noktasının bağlantısını kaldır.
  * Bağlama sırasında oluşturulan Temizleme kaynakları.
* İşlem için `NX_TCPIP_OFFLOAD_UDP_SOCKET_SEND` ,
  * TCP/IP boşaltma aracılığıyla veri gönderme. MTU veya paket zinciri koşulundan daha büyük paket uzunluğunu işlemeye hazırlanmaya hazırlanın.