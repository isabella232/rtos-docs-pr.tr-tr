---
title: Bölüm 3-Azure RTOS NetX Duo 'un Işlevsel bileşenleri
description: Bu bölümde, işlevsel bir perspektiften yüksek performanslı Azure RTOS NetX Duo TCP/IP yığınının bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 07e51643c828afc8e6c0b968e78380316e84ccd7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826212"
---
# <a name="chapter-3---functional-components-of-azure-rtos-netx-duo"></a>Bölüm 3-Azure RTOS NetX Duo 'un Işlevsel bileşenleri

Bu bölümde, işlevsel bir perspektiften yüksek performanslı Azure RTOS NetX Duo TCP/IP yığınının bir açıklaması yer almaktadır. 

## <a name="execution-overview"></a>Yürütmeye genel bakış

NetX Duo uygulaması içinde beş tür program yürütme vardır: başlatma, uygulama arabirimi çağrıları, iç IP iş parçacığı, IP dönemsel zamanlayıcılar ve ağ sürücüsü.

> [!NOTE]
> *NetX Duo, ThreadX 'in varlığını varsayar ve iş parçacığı yürütülmesine, askıya alma, düzenli zamanlayıcılar ve karşılıklı dışlama tesislarına bağlıdır.*

### <a name="initialization"></a>Başlatma

Diğer bir NetX Duo hizmeti çağrılmadan önce, ***nx_system_initialize** _ hizmeti çağrılmalıdır. Sistem başlatması, ThreadX _ *_tx_application_define_** işlevinden ya da uygulama iş parçacıklarından çağrılabilir.

***Nx_system_initialize** _ döndüğünde, sistem paket HAVUZLARı ve IP örnekleri oluşturmaya hazırdır. Bir IP örneği oluşturmak için varsayılan bir paket havuzu gerektiğinden, bir IP örneği oluşturulmadan önce en az bir NetX Duo paket havuzu bulunmalıdır. ThreadX başlatma işlevi _ *_tx_application_define_** ve uygulama iş parçacıklarında paket HAVUZLARı ve IP örnekleri oluşturulmasına izin verilir.

Dahili olarak, bir IP örneği oluşturma iki bölümden oluşur: ilk bölüm, ***tx_application_define*** veya bir uygulama iş parçacığının bağlamının bağlamı içinde yapılır. Bu, IP veri yapısını ayarlamayı ve iç IP iş parçacığı dahil çeşitli IP kaynakları oluşturmayı içerir. İkinci bölüm, iç IP iş parçacığından ilk yürütme sırasında gerçekleştirilir. Bu, IP oluşturma 'nın ilk bölümü sırasında sağlanan ağ sürücüsünün ilk kez çağrıldığı yerdir. Ağ sürücüsünü iç IP iş parçacığından çağırmak, sürücünün başlatma işlemi sırasında g/ç ve askıya alma işlemlerini gerçekleştirmesini sağlar.

Ağ sürücüsü başlatma işleminden döndüğünde, IP oluşturma tamamlanmıştır.

NetX Duo 'da IPv6 başlatması için bazı ek NetX Duo Hizmetleri gerekir. Bunlar, bu bölümün ilerleyen kısımlarında [NetX Duo 'Daki IPv6](#ipv6-in-netx-duo) bölümünde daha ayrıntılı olarak açıklanmıştır.

> [!NOTE]
> *NetX Duo hizmeti **nx_ip_status_check** , IP örneği ve birincil arabirim durumu hakkında bilgi almak için kullanılabilir. Bu tür durum bilgileri bağlantının başlatılıp başlatılmayacağını, etkin ve IP adresinin çözümlenip çözümlenmediğini içerir. Bu bilgiler, yeni oluşturulan bir IP örneğini kullanması gereken uygulama iş parçacıklarını eşleştirmek için kullanılır. Çoklu giriş sistemleri için bkz. [çok kaynaklı destek](#multihome-support). **nx_ip_interface_status_check** , belirtilen arabirim üzerinde 3ınformation elde etmek için kullanılabilir.*

### <a name="application-interface-calls"></a>Uygulama arabirimi çağrıları

Uygulamadan yapılan çağrılar, büyük ölçüde ThreadX RTOS altında çalışan uygulama iş parçacıklarından yapılır. Ancak, bazı başlatma, oluşturma ve etkinleştirme Hizmetleri ***tx_application_define*** adresinden çağrılabilir. Bölüm 4 ' te "Izin verilen" bölümler [-Azure RTOS NetX Duo hizmetlerinin açıklaması](chapter4.md) her bir NETX Duo hizmetinin çağrılabilecek olduğunu gösterir.

Genellikle, diğer iş parçacıklarının IP örneğine erişimini engellemeden, bilgi işlem sağlama işlemleri gibi yoğun etkinliklerin işlenmesi, çağıran iş parçacığının bağlamı içinde yapılır. Örneğin, iletim sırasında UDP sağlama toplamı hesaplaması, temel alınan IP gönderme işlevi çağrılmadan önce ***nx_udp_socket_send** _ hizmeti içinde gerçekleştirilir. Alınan bir pakette, UDP sağlama toplamı, uygulama iş parçacığında yürütülen _ *_nx_udp_socket_receive_** hizmetinde hesaplanır. Bu, düşük öncelikli iş parçacıklarında yoğun sağlama toplamı hesaplamayı işlerken daha yüksek öncelikli iş parçacıklarının ağ isteklerini önlemeye yardımcı olur.

IP adresleri ve bağlantı noktası numaraları gibi değerler, ana bilgisayar bayt düzeninde API 'lere geçirilir. Bu değerler dahili olarak ana bilgisayar bayt düzeninde de depolanır. Bu, geliştiricilerin bir hata ayıklayıcı aracılığıyla değerleri kolayca görüntülemesine olanak tanır. Bu değerler, iletim için bir çerçevede programlandıklarında, ağ bayt sırasına dönüştürülür.

### <a name="internal-ip-thread"></a>İç IP Iş parçacığı

Belirtildiği gibi, NetX Duo 'daki her IP örneğinin kendi iş parçacığı vardır. İç IP iş parçacığının öncelik ve yığın boyutu ***nx_ip_create*** hizmetinde tanımlanmıştır. İç IP iş parçacığı, bir yürütme modunda oluşturulur. IP iş parçacığının, çağıran iş parçacığından daha yüksek bir önceliği varsa, önalım IP oluşturma çağrısı içinde meydana gelebilir.

İç IP iş parçacığının giriş noktası _ ***nx_ip_thread_entry*** iç işlevidir. Başlatıldığında, iç IP iş parçacığı ilk olarak uygulamaya özgü ağ sürücüsüne üç çağrı yapmaktan oluşan ağ sürücüsü başlatma işlemini tamamlar. İlk çağrı, ağ sürücüsünü IP örneğine eklemek ve ardından, ağ sürücüsünün başlatma işleminden geçmesine izin veren bir başlatma çağrısı olur. Ağ sürücüsü başlatma işleminden sonra (donanımın düzgün ayarlanması beklenirken askıda kalabilir), iç IP iş parçacığı bağlantıyı etkinleştirmek için ağ sürücüsünü yeniden çağırır. Ağ sürücüsü bağlantı etkinleştirme çağrısından döndüğünde, iç IP iş parçacığı bu IP örneği için işleme ihtiyacı olan çeşitli olaylar için süresiz bir döngü denetimi girer. Bu döngüde işlenen olaylar ertelenmiş IP paket alımı, IP paket parçası derlemesi, ıCMP ping işlemi, ıGMP işleme, TCP paket kuyruğu işleme, TCP düzenli işleme, IP parçası derleme zaman aşımları ve ıGMP düzenli işleme işlemlerini içerir. Olaylar ayrıca adres çözümleme etkinliklerini içerir; IPv6 'da ARP paket işleme ve ARP düzenli işleme, IPv4, yinelenen adres algılama, yönlendirici ISTEME ve IPv6 'da komşu bulma.

> [!CAUTION]
> *Dinleme ve bağlantı kesme geri çağırmaları dahil NetX Duo geri çağırma işlevleri, özgün çağıran iş parçacığı değil, iç IP iş parçacığından çağırılır. Uygulamanın herhangi bir NetX Duo geri çağırma işlevi içinde askıya alınması gerekli değildir.*

### <a name="ip-periodic-timers"></a>IP dönemsel zamanlayıcılar

Her IP örneği için kullanılan iki ThreadX dönemsel Zamanlayıcı vardır. İlki ARP, ıGMP, TCP zaman aşımı için tek saniyelik bir zamanlayıcıya sahiptir ve ayrıca IP parçası yeniden atama işlemini de yürütür. İkinci süreölçer, TCP yeniden iletim zaman aşımını ve IPv6 ile ilgili işlemleri sağlamak için bir 100ms Zamanlayıcı olur.

### <a name="network-driver"></a>Ağ sürücüsü

NetX Duo 'daki her IP örneğinin, ***nx_ip_create*** hizmetinde belirtilen cihaz sürücüsü tarafından tanımlanan bir birincil arabirimi vardır. Ağ sürücüsü paket iletimi, paket alımı ve durum ve denetim istekleri dahil çeşitli NetX Duo isteklerini işlemekten sorumludur. 

Birden çok ana sistem için, IP örneğinde, her biri ilgili arabirim için bu görevleri gerçekleştiren ilişkili bir ağ sürücüsüne sahip birden çok arabirim vardır.

Ağ sürücüsünün Ayrıca medyada gerçekleşen zaman uyumsuz olayları işlemesi gerekir. Medyadan gelen zaman uyumsuz olaylar, paket alımı, paket iletimi tamamlama ve durum değişiklikleri içerir. NetX Duo, çeşitli olayları işlemek için çeşitli erişim işlevleriyle ağ sürücüsüne olanak sağlar. Bu işlevler, ağ sürücüsünün kesme hizmeti rutin kısmından çağrılabilir şekilde tasarlanmıştır. IPv4 ağları için, ağ sürücüsü ***_nx_arp_packet_deferred_receive*** iç işleve ALıNAN tüm ARP paketlerini iletmelidir. Tüm RARP paketlerinin ***_nx_rarp_packet_deferred_receive** _ iç işlevine iletilmesi gerekir. IP paketlerine yönelik iki seçenek vardır. IP paketlerinin hızlı gönderimi gerekliyse, anında işlenmek üzere gelen IP paketlerinin _ *_ _nx_ip_packet_receive_* _ ' e iletilmesi gerekir. Bu, IP paketlerini işlemede NetX Duo performansını önemli ölçüde artırır. Aksi takdirde, IP paketlerinin _ *_ _nx_ip_packet_deferred_receive_** öğesine iletilmesi yapılmalıdır. Bu hizmet, IP paketini ertelenmiş işleme kuyruğuna koyar ve daha sonra iç IP iş parçacığı tarafından işlenir ve bu da en az ıSR işlem süresine neden olur.

Ağ sürücüsü aynı zamanda kesme işlemeyi IP iş parçacığı bağlamında çalışacak şekilde erteleyebilirsiniz. Bu modda, ıSR gerekli bilgileri kaydeder, iç işlev ***_nx_ip_driver_deferred_processing*** çağırır ve kesme denetleyicisini kabul ediyor. Bu hizmet, IP iş parçacığını, kesintiye neden olan olayın işlemini tamamlaması için cihaz sürücüsüne bir geri çağırma zamanlamasını bildirir.

Bazı ağ denetleyicileri, değerli CPU kaynakları oluşturmadan donanımda TCP/IP üst bilgi sağlama toplamı hesaplama ve doğrulama işlemlerini gerçekleştirebilir. NetX Duo, donanım özelliği özelliğinden yararlanmak için, derleme zamanında çeşitli yazılım sağlama toplamı hesaplamasını etkinleştirmek veya devre dışı bırakmak için seçenekler sağlar ve cihaz sürücüsü, donanım özellikleri hakkında IP katmanıyla iletişim kurabiliyorsa çalışma zamanında sağlama toplamı hesaplamasını açıp devre dışı bırakır. NetX Duo ağ sürücülerini yazma hakkında daha ayrıntılı bilgi için bkz. [Bölüm 5-Azure RTOS NetX Duo ağ sürücüleri](chapter5.md) .

### <a name="multihome-support"></a>Çoklu giriş desteği

NetX Duo, tek bir IP örneği kullanılarak birden çok fiziksel cihaza bağlı olan sistemleri destekler. Her fiziksel arabirim, IP örneğindeki bir arabirim Denetim bloğuna atanır. Çok ana bir sistem kullanmak isteyen uygulamalar, ***NX_MAX_PHSYCIAL_INTERFACES** _ değerini sisteme bağlı fiziksel cihaz sayısına göre tanımlamalıdır ve NETX Duo kitaplığını yeniden derlemelisiniz. Varsayılan olarak _ *_NX_MAX_PHYSICAL_INTERFACES_**, IP örneğinde bir arabirim denetim bloğu oluşturarak bir tane olarak ayarlanır.

NetX Duo uygulaması, ***nx_ip_create** _ hizmeti kullanılarak birincil cihaz için tek bir IP örneği oluşturur. Uygulama, her ek ağ aygıtı için, _ *_nx_ip_interface_attach_** hizmetini kullanarak cihazı IP örneğine iliştirir.

Her ağ arabirimi yapısı, IP denetim bloğunda arabirim IPv4 adresi, alt ağ maskesi, IP MTU boyutu ve MAC-katman adresi bilgileri de dahil olmak üzere ağ arabirimi hakkındaki ağ bilgilerinin bir alt kümesini içerir.

> [!NOTE]
> *Multihome desteğiyle NetX Duo, NetX Duo 'un önceki sürümleriyle geriye dönük olarak uyumludur. Birincil ağ cihazına açık arabirim bilgilerini varsayılan olmayan hizmetler.*

Birincil arabirimde IP örneği listesinde sıfır dizini vardır. IP örneğine eklenen her bir sonraki cihaza bir sonraki dizin atanır.

TCP, UDP, ıCMP ve ıGMP dahil olmak üzere IP örneğinin etkinleştirildiği tüm üst katman protokol Hizmetleri, tüm bağlı cihazlar için kullanılabilir.

Çoğu durumda NetX Duo bir paket aktarırken kullanılacak en iyi kaynak adresini belirleyebilir. Kaynak adresi seçimi, hedef adresi temel alır. NetX Duo Hizmetleri, uygulamaların kullanılmak üzere belirli bir kaynak adresi belirtmesini sağlamak için eklenir ve en uygun bir durum hedef adres tarafından belirlenemez. Bir örnek, çok ana bir sistemde, bir uygulamanın bir IPv4 yayınına veya çok noktaya yayın hedef adreslerine bir paket gönderebilmesi gerekir.

Özellikle çok ana uygulamalar geliştirmeye yönelik hizmetler şunları içerir:

- *nx_igmp_multicast_interface_join*
- *nx_igmp_multicast_interface_leave*
- *nx_ip_driver_interface_direct_command*
- *nx_ip_interface_address_get*
- *nx_ip_interface_address_mapping_configure*
- *nx_ip_interface_address_set*  
- *nx_ip_interface_attach*
- *nx_ip_interface_capability_get* 
- *nx_ip_interface_capability_set*
- *nx_ip_interface_detach*
- *nx_ip_interface_info_get*
- *nx_ip_interface_mtu_set*
- *nx_ip_interface_physical_address_get*
- *nx_ip_interface_physical_address_set*
- *nx_ip_interface_status_check*
- *nx_ip_raw_packet_source_send*
- *nx_ipv4_multicast_interface_join*
- *nx_ipv4_multicast_interface_leave*
- *nx_udp_socket_source_send*
- *nxd_ipv6_multicast_interface_join*
- *nxd_ipv6_multicast_interface_leave* 
- *nxd_udp_socket_source_send*
- *nxd_icmp_source_ping*
- *nxd_ip_raw_packet_source_send*
- *nxd_udp_socket_source_send*

Bu hizmetler [NetX Duo hizmetlerinin açıklaması](chapter4.md)bölümünde daha ayrıntılı olarak açıklanmıştır.

### <a name="loopback-interface"></a>Geri döngü arabirimi

Geri döngü arabirimi, bağlı bir fiziksel bağlantısı olmayan özel bir ağ arabirimidir. Geri döngü arabirimi, mantıksal bir geri döngü arabirimini kullanmak Için 127.0.0.1 IPv4 geri döngü adresini kullanarak iletişim kurmasına izin verir, yapılandırılabilir seçeneğinin ***NX_DISABLE_LOOPBACK_INTERFACE*** ayarlanmamış olduğundan emin olun.

### <a name="interface-control-blocks"></a>Arabirim denetim blokları

IP örneğindeki arabirim denetim bloklarının sayısı, fiziksel arabirimlerin sayısıdır (***NX_MAX_PHYSICAL_INTERFACES** _ tarafından tanımlanır) ve etkinse geri döngü arabirimi. Toplam arabirim sayısı _ *_NX_MAX_IP_INTERFACES_* * içinde tanımlanır.

## <a name="protocol-layering"></a>Protokol katmanlama

NetX Duo tarafından uygulanan TCP/IP katmanlı bir protokoldür, bu da daha karmaşık protokollerin daha basit alt protokollerin üzerine derlendiği anlamına gelir. TCP/IP 'de, en düşük katman Protokolü *bağlantı düzeyindedir* ve ağ sürücüsü tarafından işlenir. Bu düzey genellikle Ethernet 'e yöneliktir, ancak fiber, seri veya neredeyse herhangi bir fiziksel medya olabilir.

Bağlantı katmanının en üstünde *ağ katmanı* bulunur. TCP/IP 'de, bu IP 'nin basit paketleri (en iyi çabayla) ağ genelinde gönderilmesinin ve almamasından sorumlu olan IP 'dir. ICMP ve ıGMP gibi yönetim türü protokoller, genellikle IP 'yi gönderme ve alma için kullandıkları halde ağ katmanları olarak kategorize edilir.

*Aktarım katmanı* , ağ katmanının üzerine oturduğu. Bu katman, ağ üzerindeki konaklar arasında veri akışını yönetmekten sorumludur. NetX Duo: UDP ve TCP tarafından desteklenen iki tür aktarım hizmeti vardır. UDP Hizmetleri, iki ana bilgisayar arasında bağlantısız bir şekilde verileri en iyi şekilde gönderme ve alma olanağı sağlarken, TCP iki konak varlık arasında güvenilir bir bağlantı yönelimli hizmet sağlar.

Bu katman, gerçek ağ veri paketlerine yansıtılır. TCP/IP içindeki her katman, üst bilgi olarak adlandırılan bir bilgi bloğu içerir. Bu verilere (ve muhtemelen protokol bilgilerine) sahip bir üst bilgi içeren bu teknik genellikle veri kapsülleme olarak adlandırılır. Şekil 1 ' de NetX Duo katmanlama örneği gösterilmektedir ve Şekil 2 gönderilen UDP verileri için elde edilen veri kapsüllemesini gösterir.

![Protokol katmanlama](./media/user-guide/image12.jpg)

**ŞEKIL 1. Protokol katmanlama**

## <a name="packet-pools"></a>Paket havuzları

Paketleri hızlı ve belirleyici bir şekilde ayırmak, gerçek zamanlı ağ uygulamalarında her zaman zorluk sergilemektir. NetX Duo, bu şekilde, birden çok sabit boyutlu ağ paketi havuzu oluşturma ve yönetme olanağı sağlar.

NetX Duo Paket havuzları sabit boyutlu bellek blokları içerdiğinden, hiçbir iç parçalama sorunu yoktur. Tabii ki parçalama, doğal olarak belirleyici olmayan davranışa neden olur. Ayrıca, bir NetX Duo paket miktarını ayırmak ve serbest bırakmak için gereken süre basit bağlantılı liste işleme. Ayrıca, paket ayırma ve ayırmayı kaldırma, kullanılabilir listenin başında yapılır. Bu, mümkün olan en hızlı bağlantılı liste işlemesini sağlar.

![UDP veri kapsülleme](./media/user-guide/image13.png)

**ŞEKIL 2. UDP veri kapsülleme**

Esneklik olmaması genellikle sabit boyutlu paket havuzlarının başlıca dezavantajıdır. Büyük/küçük harfe gelen paketi de işleyen en iyi paket yükü boyutunun belirlenmesi zor bir görevdir. NetX Duo paketleri, bu sorunu paket zincirleme adlı isteğe bağlı bir özellikle ele maktadır. Gerçek bir ağ paketi, birbirine bağlı bir veya daha fazla NetX Duo paketi yapılabilir. Ayrıca, paket üst bilgisi paketin en üstüne bir işaretçi tutar. Ek protokoller eklendikçe, bu işaretçi geriye doğru taşınır ve yeni üst bilgi doğrudan verilerin önüne yazılır. Esnek paket teknolojisi olmadan, yığının başka bir arabellek ayırması ve verileri yeni bir üst bilgiyle, yoğun işleme alan yeni bir arabelleğe kopyalaması gerekir.

Her paket yükü boyutu belirli bir paket havuzu için düzeltildiğinden, yük boyutundan daha büyük olan uygulama verileri birlikte birden çok paket zincirleme gerektirir. Bir paketi kullanıcı verileriyle doldururken, uygulama hizmeti ***nx_packet_data_append*** kullanacaktır. Bu hizmet uygulama verilerini bir pakete taşıtur. Bir paketin Kullanıcı verilerini tutmak için yeterli olmadığı durumlarda, Kullanıcı verilerini depolamak için ek paketler ayrılır. Paket zincirlemesini kullanmak için, sürücünün zincirleme paketlere alabilmesi ya da bu paketten iletim yapabilmesi gerekir.

Paket zincirleme özelliğini kullanması gerekmeyen ekli sistemler için, NetX Duo kitaplığı, paket zincirleme mantığını kaldırmak için ***NX_DISABLE_PACKET_CHAIN** _ ile oluşturulabilir. IP parçalama ve yeniden birleştirme özelliğinin zincirleme paket özelliğini kullanmak zorunda olabileceğini unutmayın. Bu nedenle _*_NX_DISABLE_PACKET_CHAIN_*_ tanımlanması _ *_NX_DISABLE_FRAGMENTATION_** için de tanımlanmalıdır. 

Her NetX Duo paket bellek havuzu, genel bir kaynaktır. NetX Duo, paket havuzlarının nasıl kullanılbileceğine ilişkin bir kısıtlama yoktur. 

### <a name="packet-pool-memory-area"></a>Paket havuzu bellek alanı

Paket havuzu için bellek alanı oluşturma sırasında belirtilir. ThreadX ve NetX Duo nesneleri için diğer bellek alanları gibi, hedefin adres alanındaki herhangi bir yerde bulunabilir. 

Bu, uygulamaya verdiği önemli esneklik nedeniyle önemli bir özelliktir. Örneğin, bir iletişim ürününün ağ arabellekleri için yüksek hızlı bellek alanı olduğunu varsayalım. Bu bellek alanı, bir NetX Duo paket bellek havuzunda yapılarak kolayca kullanılır.

### <a name="creating-packet-pools"></a>Paket havuzları oluşturma

Paket havuzları, başlatma sırasında veya çalışma zamanı sırasında uygulama iş parçacıkları tarafından oluşturulur. Bir NetX Duo uygulamasındaki paket belleği havuzlarının sayısında sınır yoktur.

### <a name="dual-packet-pool"></a>Çift paket havuzu

Genellikle varsayılan IP paket havuzunun yük boyutu, ağ arabirimi MTU 'SU için çerçeve boyutunu karşılayacak kadar büyüktür. Normal işlem sırasında, IP iş parçacığının ARP, TCP denetim iletileri, ıGMP iletileri, ICMPv6 iletileri gibi iletileri gönderebilmesi gerekir. Bu iletiler IP örneğindeki varsayılan paket havuzundan ayrılan paketleri kullanır. Paket havuzu için kullanılabilir bellek miktarının sınırlı olduğu, tek bir paket havuzunun kullanılması (MTU boyutuyla eşleşmesi için büyük yük boyutu ile) en iyi çözüm olmayabilir. NetX Duo, uygulamanın yük boyutunun daha küçük olduğu bir yardımcı paket havuzu yüklemesine olanak tanır. Yardımcı paket havuzu yüklendikten sonra, ileten iletinin boyutuna bağlı olarak, IP Yardımcısı iş parçacığı paketleri varsayılan paket havuzundan ya da yardımcı havuzdan ayırır. Bir yardımcı paket havuzu için, 200 baytlık yük boyutu, IP Yardımcısı iş parçacığının ilettiği birçok ileti ile çalışır.

Varsayılan olarak NetX Duo kitaplığı, çift paket havuzu etkinleştirilmeksizin oluşturulur. Özelliği etkinleştirmek için, kitaplığı ***NX_DUAL_PACKET_POOL_ENABLE** _ tanımlı ile derleyin. Daha sonra yardımcı paket havuzu _ *_nx_ip_auxiliary_packet_pool_set_* * çağırarak ayarlanabilir.

Ayrıca, birden fazla paket havuzu oluşturma seçeneği de mevcuttur. Örneğin, beklenen ileti boyutları için en iyi yük boyutuyla bir iletme paketi havuzu oluşturulur. Alınan paketlerin boyutunu tahmin edememesi nedeniyle, bir alma paketi havuzu sürücü MTU olarak ayarlanan yük boyutu olan sürücüde oluşturulur.

### <a name="packet-header-nx_packet"></a>Paket üst bilgisi NX_PACKET   
Varsayılan olarak, NetX Duo paket üst bilgisini paket yük alanından hemen önce koyar. Paket bellek havuzu temel olarak bir dizi paket (üst bilgiler), ardından paket yükünün hemen ardından gelir. Paket üst bilgisi (***NX_PACKET***) ve paket havuzunun düzeni şekil 3 ' te gösterilmiştir.

Sıfır kopyalama işlemi gerçekleştirebilecek ağ cihazları sürücüsü için genellikle paket yük alanının başlangıç adresi DMA mantığıyla programlanabilir. Belirli DMA altyapılarının yük alanında hizalama gereksinimi vardır. Yük alanının başlangıç adresini DMA altyapısı veya önbellek işlemi için doğru şekilde hizalamak için, Kullanıcı symbol ***NX_PACKET_ALIGNMENT*** tanımlayabilir.

> [!WARNING]
> *Bir paketin iletimi tamamlandığında, ağ sürücüsünün **nx_packet_transmit_release** işlevini kullanması önemlidir. Bu işlev, paketin kullanılabilir havuza gerçekten geri yerleştirilmesi için bir TCP çıkış sırasının parçası olmadığından emin olup olmadığını denetler.*

![Paket üst bilgisi ve paket havuzu düzeni](./media/user-guide/image14.jpg)

**ŞEKIL 3. Paket üst bilgisi ve paket havuzu düzeni**

Paket üstbilgisinin alanları aşağıdaki gibi tanımlanır. Bu tablonun *NX_PACKET* yapısındaki tüm üyelerin kapsamlı bir listesi olmadığına unutmayın.

|Paket üst bilgisi | Amaç |
|---|---|
|***nx_packet_pool_owner***|Bu alan, bu belirli paketin sahibi olan paket havuzunu işaret eder. Paket yayınlanmışsa, bu belirli havuza serbest bırakılır. Her paketin içindeki havuz sahipliğiyle, bir veri biriminin birden çok paket havuzundan birden çok pakete yayılması mümkündür.|
|***nx_packet_next** _|Bu alan, aynı çerçeve içindeki bir sonraki pakete işaret eder. NULL ise çerçevenin parçası olan ek paketler yoktur. Bu alan, tüm paketin yeniden yayılmadığı sürece parçalanmış paketleri tutmak için de kullanılır. _ *_NX_DISABLE_PACKET_CHAIN_* * tanımlanmışsa kaldırılır.|
|***nx_packet_last** _|Bu alan, aynı ağ paketi içindeki son paketi işaret eder. NULL ise, bu paket tüm ağ paketini temsil eder. _ *_NX_DISABLE_PACKET_CHAIN_* * tanımlanmışsa Bu alan kaldırılır.|
|***nx_packet_length** _| Bu alan, tüm ağ paketindeki toplam bayt sayısını (_nx_packet_next * üyesi tarafından birlikte zincirleme tüm paketlerin toplam bayt sayısı dahil) içerir.|
|***nx_packet_ip_interface***| Bu alan, arabirim sürücüsü tarafından alındığında pakete atanan arabirim denetim bloğu ve giden paketler için NetX Duo tarafından kullanılır. Arabirim denetim bloğu; ağ adresi, MAC adresi, IP adresi ve bağlantı etkin ve fiziksel eşleme gibi arabirim durumu gibi arabirimi tanımlar.|
|***nx_packet_data_start** _| Bu alan, bu paketin fiziksel yük alanının başlangıcını gösterir. NX_PACKET üst bilgisini hemen takip etmek zorunda değildir, ancak bu, _ *_nx_packet_pool_create_** hizmeti için varsayılandır.|
|***nx_packet_data_end** _|Bu alan, bu paketin fiziksel yük alanının sonuna işaret eder. Bu alan ile _nx_packet_data_start * alanı arasındaki fark, yük boyutunu temsil eder.|
|***nx_packet_prepend_ptr** _|Bu alan paket verilerinin, paket yükü alanındaki mevcut paket verilerinin önüne (varsa) protokol üstbilgisi veya gerçek veriler eklendiğini gösterir. _Nx_packet_data_start * işaretçisi konumundan büyük veya buna eşit ve *nx_packet_append_ptr* işaretçisinden küçük veya buna eşit olmalıdır.|
> [!CAUTION]
> *NETX Duo, performans nedenleriyle iletim için NETX Duo hizmetlerine geçirildiğinde, önüne işaretçisinin uzun sözcük hizalı adrese işaret ettiğini varsayar.*

|   |   |
|---|---|
|***nx_packet_append_ptr** _|Bu alan, şu anda paket yükü alanındaki verilerin sonunu işaret eder. _Nx_packet_prepend_ptr * ve nx_packet_data_end tarafından işaret edilen bellek konumu arasında olmalıdır *.* Bu alan ile *nx_packet_prepend_ptr* alanı arasındaki fark, bu paketteki veri miktarını temsil eder.|
|***nx_packet_packet_pad** _|Bu alanlar, istenen hizalama gereksinimini elde etmek için 4 baytlık sözcüklerdeki doldurma uzunluğunu tanımlar. _*_NX_PACKET_HEADER_PAD_*_ tanımlanmamışsa Bu alan kaldırılır. Alternatif olarak, _nx_packet_header_pad tanımlamak yerine _*_NX_PACKET_ALIGNMENT_*_ kullanılabilir. *|

### <a name="packet-header-offsets"></a>Paket üst bilgisi uzaklıkları

Paket üst bilgisi boyutu, üst bilgi boyutuna uyum sağlamak için yeterli yer sağlamak üzere tanımlanır. ***Nx_packet_allocate*** hizmeti bir paket ayırmak ve belirtilen paket türüne göre paketteki preppointer 'ı ayarlaması için kullanılır. Paket türü NetX Duo protokolünü, protokol verilerinin önüne (UDP, TCP veya ıCMP gibi) eklemek için gereken sapmayı söyler.

Aşağıdaki türler, paketteki IP üstbilgisini ve fiziksel katman (Ethernet) üst bilgisini hesaba çekmek için NetX Duo içinde tanımlanmıştır. İkinci durumda, gereken 4 baytlık hizalamasının dikkate alınması 16 bayt olarak kabul edilir. IPv4 paketleri, uygulamaların IPv4 ağları için paket ayırmasını sağlamak üzere NetX Duo içinde hala tanımlanmıştır. NetX Duo kitaplığı IPv6 etkin ise, genel paket türleri (örneğin, NX_IP_PACKET) IPv6 sürümüne eşlenir. NetX Duo kitaplığı IPv6 etkin olmadan derlenmişse, bu genel paket türleri IPv4 sürümüne eşlenir.

Aşağıdaki tabloda IPv6 etkin olarak tanımlanan semboller gösterilmektedir:

|**Paket türü** |**Değer** |
|---|---|
|NX_IPv6_PACKET (NX_IP_PACKET) | 0x38 |
|NX_UDPv6_PACKET (NX_UDP_PACKET) |0x40 |
|NX_TCPv6_PACKET (NX_TCP_PACKET) |0x4C |
|NX_IPv4_PACKET |0x24 |
|NX_IPv4_UDP_PACKET |0x2C |
|NX_IPv4_TCP_PACKET |0x38 |

Aşağıdaki tabloda IPv6 devre dışı olarak tanımlanan semboller gösterilmektedir:

|**Paket türü** |**Değer** |
|---|---|
|NX_IPv4_PACKET (NX_IP_PACKET) |0x24 |
|NX_IPv4_UDP_PACKET (NX_UDP_PACKET) |0x2C |
|NX_IPv4_TCP_PACKET (NX_TCP_PACKET) |0x38 |

*NX_IPSEC_ENABLE* tanımlanmışsa bu değerlerin değişdiğine unutmayın. IPSec kullanan uygulama için, daha fazla bilgi için NetX Duo IPSec Kullanıcı Kılavuzu 'na bakın.

### <a name="pool-capacity"></a>Havuz kapasitesi

Bir paket havuzundaki paketlerin sayısı, yük boyutunun bir işlevidir ve paket havuzu oluşturma hizmeti için sağlanan bellek alanındaki toplam bayt sayısıdır. Havuzun kapasitesi, paket boyutu (NX_PACKET üst bilgisinin boyutu, yük boyutu ve doğru hizalama) sağlanan bellek alanındaki toplam bayt sayısına bölünerek hesaplanır.

### <a name="payload-area-alignment"></a>Yük alanı hizalaması

NetX Duo 'daki paket havuzu tasarımı sıfır kopyalamayı destekler. Cihaz sürücüsü düzeyinde sürücü, yük alanını doğrudan veri alımı için arabellek tanımlayıcılara atayabilecektir. Bazen DMA altyapısı veya önbellek eşitleme mekanizması, yük alanının başlangıç adresinin belirli bir hizalama gereksinimine sahip olmasını gerektirir. Bu, ***NX_PACKET_ALIGNMENT*** içindeki istenen hizalama gereksinimini (bayt cinsinden) tanımlayarak elde edilebilir. Bir paket havuzu oluştururken, yük alanının başlangıç adresi bu değere hizalanır. Varsayılan olarak, başlangıç adresi 4 bayt hizalı olur.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Uygulama iş parçacıkları, boş bir havuzdan paket beklerken askıya alabilir. Havuza bir paket döndürüldüğünde, askıya alınan iş parçacığına Bu paket verilir ve devam edilir.

Aynı paket havuzunda birden çok iş parçacığı askıya alınırsa, askıya alındığı sırada (FıFO) sürdürülür.

### <a name="pool-statistics-and-errors"></a>Havuz Istatistikleri ve hataları

Etkinleştirilirse, NetX Duo paket yönetimi yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Paket havuzları için aşağıdaki istatistikler ve hata raporları korunur:

- Havuzdaki toplam paket sayısı
- Havuzdaki ücretsiz paketler
- Toplam paket ayırmaları
- Havuz boş ayırma Istekleri
- Havuz boş ayırma getirilmesi
- Geçersiz paket yayınları

Bu istatistik ve hata raporlarının tümü, havuzdaki toplam ve ücretsiz paket sayısı dışında, ***NX_DISABLE_PACKET_INFO** _ tanımlanmadığı sürece NETX Duo kitaplığı 'nda yerleşiktir. Bu veriler, _ *_nx_packet_pool_info_get_** hizmeti ile uygulama tarafından kullanılabilir.

### <a name="packet-pool-control-block-nx_packet_pool"></a>Paket havuzu denetim bloğu NX_PACKET_POOL

Her paket bellek havuzunun özellikleri denetim bloğunda bulunur. Bu havuz, bağlantılı ücretsiz paketlerin listesi, serbest paket sayısı ve bu havuzdaki paketlerin yük boyutu gibi yararlı bilgiler içerir. Bu yapı ***nx_api. h*** dosyasında tanımlanmıştır.

Paket havuzu denetim blokları bellekte herhangi bir yerde bulunabilir, ancak herhangi bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır.

## <a name="ipv4-protocol"></a>IPv4 protokolü

NetX Duo 'un Internet Protokolü (IP) bileşeni, Internet üzerinde IPv4 paketleri göndermekten ve alınmasından sorumludur. NetX Duo sürümünde, temel alınan ağ sürücüsünden yararlanarak, son olarak TCP, UDP, ıCMP ve ıGMP iletileri gönderme ve alma işleminden sorumlu bileşendir.

NetX Duo hem IPv4 protokolünü (RFC 791) hem de IPv6 protokolünü (RFC 2460) destekler. Bu bölümde IPv4 açıklanır. IPv6, sonraki bölümde ele alınmıştır.

### <a name="ipv4-addresses"></a>IPv4 adresleri

Internet üzerindeki her konağın, IP adresi olarak adlandırılan benzersiz bir 32 bit tanımlayıcısı vardır. Şekil 4 ' te açıklandığı gibi beş IPv4 adresi sınıfı vardır. Beş IPv4 adresi sınıfının aralıkları aşağıdaki gibidir:

|Sınıf|Aralık|
|---|---|
|A |0.0.0.0 127.255.255.255|
|B |128.0.0.0 to 191.255.255.255|
|C |192.0.0.0 to 223.255.255.255|
|D |224.0.0.0 ile 239.255.255.255 arası|
|E |240.0.0.0 to 247.255.255.255|

![IPv4 adresi yapısının diyagramı.](./media/user-guide/ipv4-address-structure.png)

### <a name="figure-4-ipv4-address-structure"></a>ŞEKIL 4. IPv4 adresi yapısı

Ayrıca üç tür adres belirtimi vardır: *tek noktaya* yayın, *yayın* ve *çok noktaya yayın*. Tek noktaya yayın adresleri, Internet 'teki belirli bir konağı tanımlayan IPv4 adresleridir. Tek noktaya yayın adresleri bir kaynak ya da hedef IPv4 adresi olabilir. Bir yayın adresi, belirli bir ağ veya alt ağ üzerindeki tüm Konakları tanımlar ve yalnızca hedef adres olarak kullanılabilir. Yayın adresleri, adres kümesinin ana bilgisayar KIMLIĞI kısmı olacak şekilde belirtilir. Çok noktaya yayın adresleri (sınıf D) Internet 'te dinamik bir konaklar grubu belirtir. Çok noktaya yayın grubunun üyeleri her istediklerinde katılabilir ve bırakabilir.

> [!IMPORTANT]
> *Yalnızca IPv4 üzerinden UDP gibi bağlantısız protokoller yayın ve çok noktaya yayın grubunun sınırlı yayın özelliğini kullanabilir.*

> [!IMPORTANT]
> * Makro *IP_address* , ***nx_api. h** _ içinde tanımlanmıştır. Bir nokta yerine virgüller kullanarak IPv4 adreslerinin kolay belirtime olanak sağlar. Örneğin, _IP_ADDRESS (128, 0, 0, 0) * Şekil 4 ' te gösterilen ilk sınıf B adresini belirtir. *

### <a name="ipv4-gateway-address"></a>IPv4 ağ geçidi adresi

Ağ geçitleri, ağları üzerinde yerel etki alanı dışındaki hedeflere giden paketleri geçirmeye yardımcı olur. Her düğüm, bir sonraki atlamanın, komşlarından biri olan veya önceden programlanmış bir statik yönlendirme tablosu aracılığıyla gönderileceği bir bilgi içerir. Ancak, bu yaklaşımlar başarısız olursa düğüm, paketi hedefine yönlendirme hakkında daha fazla bilgi sahibi olan varsayılan ağ geçidine iletir. Varsayılan ağ geçidinin IP örneğine bağlı fiziksel arabirimlerden biri aracılığıyla doğrudan erişilebilir olması gerektiğini unutmayın. Uygulama, IPv4 varsayılan ağ geçidi adresini yapılandırmak için ***nx_ip_gateway_address_set** _ öğesini çağırır. Geçerli IPv4 ağ geçidi ayarlarını almak için hizmet _*_nx_ip_gateway_address_get_*_ kullanın. Uygulama ağ geçidi ayarını temizlemek için _ *_nx_ip_gateway_address_clear_** hizmetini kullanır.

### <a name="ipv4-header"></a>IPv4 üst bilgisi

Herhangi bir IPv4 paketinin Internet üzerinden gönderilmesi için bir IPv4 üst bilgisine sahip olması gerekir. Daha yüksek düzey protokoller (UDP, TCP, ıCMP veya ıGMP) bir paket göndermek için IP bileşenini çağırdığınızda, IPv4 iletme modülü verilerin önüne bir IPv4 üst bilgisi koyar. Buna karşılık, ağdan IP paketleri alındığında, IP bileşeni, üst düzey protokollere teslim etmeden önce, IPv4 üst bilgisini paketten kaldırır. Şekil 5 ' te IP üstbilgisinin biçimi gösterilmektedir.

![IPv4 üst bilgi biçimi](./media/user-guide/ipv4-header-format.png)

### <a name="figure-5-ipv4-header-format"></a>ŞEKIL 5. IPv4 üst bilgi biçimi

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm üstbilgilerin **Big endian** biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur. Örneğin, 4 bit sürümü ve IP üstbilgisinin 4 bitlik üstbilgi uzunluğu üstbilginin ilk baytında bulunmalıdır.*

IPv4 üstbilgisinin alanları aşağıdaki gibi tanımlanır:

|IPv4 &nbsp; üst bilgisi &nbsp; alanı |Amaç |
|---|---|
|***4 bit sürümü*** |Bu alan, bu üst bilginin temsil ettiği IP sürümünü içerir. NetX Duo 'un desteklediği IP sürüm 4 için, bu alanın değeri 4 ' tür. |
|***4 bit üst bilgi uzunluğu*** |Bu alan, IP üstbilgisindeki 32 bitlik sözcüklerin sayısını belirtir. Hiçbir seçenek sözcüğü yoksa, bu alanın değeri 5 ' tir. |
|***8 bit hizmet türü (TOS)*** |Bu alan, bu IP paketi için istenen hizmetin türünü belirtir. Geçerli istekler şunlardır:<br />-Normal: 0x00 <br />-Minimum gecikme: 0x00<br />-En fazla veri: 0x08<br />-En yüksek güvenilirlik: 0x04<br />-Minimum maliyet: 0x02 |
|***16 bit Toplam uzunluk*** |Bu alan IP üst bilgisi dahil olmak üzere bayt cinsinden IP veri biriminin toplam uzunluğunu içerir. Bir IP veri birimi, TCP/IP Interneti üzerinde bulunan temel bilgi birimidir. Verilerin yanı sıra bir hedef ve kaynak adresi içerir. 16 bit alan bir IP veri biriminin en büyük boyutu 65.535 bayttır.|
|***16 bit tanımlama*** |Alan, bir konaktan gönderilen her IP veri birimini benzersiz şekilde tanımlamak için kullanılan bir sayıdır. Bu sayı genellikle bir IP veri birimi gönderildikten sonra artırılır. Alınan IP paket parçalarının montajı özellikle yararlıdır.|
|***3 bit bayrak*** |Bu alan IP parçalama bilgilerini içerir. Bit 14 "parçalara ayırma" bitidir. Bu bit ayarlandıysa, giden IP datagramı parçalanmaz. Bit 13, "daha fazla parça" bitidir. Bu bit ayarlandıysa, daha fazla parça vardır. Bu bit açık ise, IP paketinin son parçadır.|
|***13 bit parça kayması*** |Bu alan, parça kaydırmasına ait 13 bit üst ' i içerir. Bu nedenle, parça uzaklıklarla yalnızca 8 baytlık sınırlarda izin verilir. Parçalanmış bir IP veri biriminin ilk parçası "daha fazla parça" bit kümesine sahip olur ve 0 ' ın bir uzaklığa sahip olur.|
|***8 bit yaşam süresi (TTL)*** |Bu alan, bu veri biriminin geçebileceği yönlendirici sayısını içerir ve bu da veri biriminin ömrünü temel olarak sınırlandırır.|
|***8 bit protokol***|Bu alan, hangi protokolün IP datagramı kullandığını belirtir. Geçerli protokollerin ve bunların değerlerinin listesi aşağıda verilmiştir:<br />-ICMP: 0x01 <br />-IGMP: 0x02<br />-TCP: 0X06<br />-UDP: 0X11 |
|***16 bit sağlama toplamı*** |Bu alan, yalnızca IP üstbilgisini kapsayan 16 bit sağlama toplamını içerir. IP yükünü kapsayan üst düzey protokollerde ek sağlama toplamı vardır. |
|***32-bit kaynak IP adresi*** |Bu alan, gönderenin IP adresini içerir ve her zaman bir ana bilgisayar adresidir. |
|***32-bit hedef IP adresi*** |Bu alan, adres bir yayın veya çok noktaya yayın adresi ise alıcı veya alıcıların IP adresini içerir. |

### <a name="creating-ip-instances"></a>IP örnekleri oluşturma

IP örnekleri, başlatma sırasında veya çalışma zamanı sırasında uygulama iş parçacıkları tarafından oluşturulur. İlk IPv4 adresi, ağ maskesi, varsayılan paket havuzu, medya sürücüsü ve iç IP iş parçacığının belleği ve önceliği, uygulama yalnızca IPv6 ağlarını kullanmayı amaçladığında bile ***nx_ip_create*** hizmeti tarafından tanımlanır. Uygulama, IP örneğini IPv4 adresi ile geçersiz bir adrese (0.0.0.0) ayarlandıysa, arabirim adresinin daha sonra, RARP aracılığıyla ya da DHCP veya benzer protokoller aracılığıyla el ile yapılandırma ile çözüledüğü varsayılır.

Birden çok ağ arabirimine sahip sistemler için, ***nx_ip_create** _ çağrılırken birincil arabirim atanır. Her ek arabirim _ *_nx_ip_interface_attach_* * ÇAĞıRARAK aynı IP örneğine bağlanabilir. Bu hizmet, arabirim denetim bloğunda ağ arabirimi (IP adresi, ağ maskesi gibi) hakkındaki bilgileri depolar ve sürücü örneğini IP örneğindeki arabirim denetim bloğu ile ilişkilendirir. Sürücü bir veri paketi aldığından, IP alma mantığına iletmeden önce arabirim bilgilerini NX_PACKET yapıda depolaması gerekir. Herhangi bir arabirim iliştirmeden önce bir IP örneğinin oluşturulması gerekir.

IPv6 Hizmetleri, ***nx_ip_create** _ çağrıldıktan sonra başlatılmaz. IPv6 hizmetlerini kullanmak isteyen uygulamalar, IPv6 'Yı başlatmak için _ *_nx_ipv6_enable_** hizmetini çağırmalıdır.

IPv6 ağında, bir IP örneğindeki her arabirim birden fazla IPv6 genel adresine sahip olabilir. IPv6 adres ataması için DHCPv6 kullanmanın yanı sıra, bir cihaz durum bilgisiz adres otomatik yapılandırması da kullanabilir. Daha sonra bu bölümün ilerleyen kısımlarında "IP denetim bloğu" ve "IPv6 adres çözümlemesi" bölümlerinde daha fazla bilgi bulunmaktadır.

### <a name="ip-send"></a>IP gönderme

NetX Duo 'da IP gönderme işlemi çok basitleştirilmiştir. Paketteki önüne işaretçisi, IP üst bilgisine uyacak şekilde geriye taşınır. IP üstbilgisi tamamlandı (çağıran protokol katmanı tarafından belirtilen tüm seçeneklerle), IP sağlama toplamı satır içinde hesaplanır (yalnızca IPv4 paketleri için) ve paket ilişkili ağ sürücüsüne gönderilir. Ayrıca, giden parçalanma IP gönderme işlemi içinden de koordine edilir.

IPv4 için NetX Duo, hedef IP adresi için fiziksel eşleme gerekliyse ARP istekleri başlatır. IPv6, IPv6 adresi-tofiziksel adres eşlemesi için komşu bulmayı kullanır.

> [!NOTE]
> *IPv4 bağlantısı için, sıraya alınan paket sayısı ARP kuyruğu derinliğini (sembol **NX_ARP_MAX_QUEUE_DEPTH** tarafından tanımlanır) aşana kadar IP adresi çözümlemesi (yani fiziksel eşleme) GEREKTIREN paketler ARP kuyruğunda sıraya alınır. Sıra derinliğine ulaşıldığında NetX Duo kuyruktaki en eski paketi kaldırır ve kalan paketlerin sıraya alındığı adres çözümlemesini beklemeye devam eder. Öte yandan, bir ARP girdisi çözümlenmezse ARP girişinde bekleyen paketler ARP giriş zaman aşımı üzerine serbest bırakılır.*

Birden çok ağ arabirimine sahip sistemler için NetX Duo, hedef IP adresini temel alan bir arabirim seçer. Aşağıdaki yordam seçim işlemi için geçerlidir:

1. Gönderen bir giden arabirim belirtiyorsa ve arabirim geçerliyse, bu arabirimi kullanın.
2. Bir hedef adres IPv4 yayını veya çok noktaya yayın ise, ilk etkin fiziksel arabirim kullanılır.
3. Hedef adres statik yönlendirme tablosunda bulunursa, ağ geçidiyle ilişkili arabirim kullanılır.
4. Hedef bağlantıalıyorsa, bağlantı bağlantısı arabirimi kullanılır.
5. Hedef adres bir bağlantı yerel adresidir (169.254.0.0/16), ilk geçerli arabirim kullanılır.
6. Varsayılan ağ geçidi yapılandırılmışsa, paketi aktarmak için varsayılan ağ geçidiyle ilişkili arabirimi kullanın.
7. Son olarak, geçerli arabirim IP adresinden biri bağlantı-yerel adres (169.254.0.0/16) ise, bu arabirim iletim için kaynak adresi olarak kullanılır.
8. Yukarıdaki tüm hata oluştuğunda çıkış paketi bırakılır.

### <a name="ip-receive"></a>IP alma

IP alma işlemi ağ sürücüsünden veya iç IP iş parçacığından (ertelenmiş alınan paket sırasındaki paketleri işlemek için) çağrılır. IP alma işlemi protokol alanını inceler ve paketi uygun protokol bileşenine gönderme girişiminde bulunur. Paket gerçekten gönderilmeden önce IP üstbilgisi, IP üstbilgisinin ötesinde önüne işaretçisinin ilerleyerek kaldırılır.

IP alma işlemi, parçalanmış IP paketlerini de algılar ve parçalama etkinse bunları yeniden birleştirmek için gerekli adımları gerçekleştirir. Parçalama gerekliyse ancak etkinleştirilmemişse, paket bırakılır.

NetX Duo, pakette belirtilen arabirime bağlı olarak uygun ağ arabirimini belirler. Paket arabirimi NULL ise NetX Duo varsayılan olarak birincil arabirime ayarlanır. Bu, eski NetX Duo Ethernet sürücüleriyle uyumluluğu güvence altına almak için yapılır.

### <a name="raw-ip-send"></a>Ham IP gönderme

Ham IP paketi, NetX Duo tarafından doğrudan desteklenmeyen (ve işlenen) üst katman protokol yükünün bulunduğu bir IP çerçevesidir. Ham paket, geliştiricilerin kendi IP tabanlı uygulamalarını tanımlamasına olanak tanır. Bir uygulama, _*_nx_ip_raw_packet_enabled_*_ HIZMETIYLE ham IP paket işleme etkinleştirildiyse, doğrudan ***nxd_ip_raw_packet_send** _ hizmetini kullanarak ham IP paketleri gönderebilir. NetX Duo, bir tek noktaya yayın paketini bir IPv6 ağına iletirken, hedef adrese göre, paketleri üzerine göndermek için kullanılacak en iyi kaynak IPv6 adresini otomatik olarak belirler. Hedef adres bir çok noktaya yayın (veya IPv4 için yayın) adresi ise, NetX Duo varsayılan olarak ilk (birincil) arabirime ayarlanır. Bu nedenle, bu tür paketleri ikincil arabirimlerde göndermek için, uygulamanın, giden paket için kullanılacak kaynak adresini belirtmek üzere _ *_nx_ip_raw_packet_source_send_** hizmetini kullanması gerekir.

### <a name="raw-ip-receive"></a>Ham IP alma

Ham IP paket işleme etkinse, uygulama, ***nx_ip_raw_packet_receive** _ hizmeti aracılığıyla ham IP paketleri alabilir. Tüm gelen paketler, IP üstbilgisinde belirtilen protokole göre işlenir. Protokol UDP, TCP, ıGMP veya ıCMP belirtiyorsa, NetX Duo paket protokol türü için uygun işleyiciyi kullanarak paketi işleymeyecektir. Protokol Bu protokollerden biri değilse ve ham IP alma etkinleştirilmişse, gelen paket, uygulamanın _*_nx_ip_raw_packet_receive_** hizmeti aracılığıyla almasını bekleyen ham paket kuyruğuna yerleştirilir. Ayrıca, uygulama iş parçacıkları bir ham IP paketini beklerken isteğe bağlı bir zaman aşımı ile askıya alabilir. Ham paket kuyruğunda sıraya alınabilen paketlerin sayısı sınırlıdır. En büyük değer_, varsayılan değeri 20 olan * NX_IP_RAW_MAX_QUEUE_DEPTH tanımlanmıştır. Uygulama, _ *_nx_ip_raw_receive_queue_max_set_** hizmetini çağırarak maksimum değeri değiştirebilir.

Alternatif olarak, NetX Duo Kitaplığı ***NX_ENABLE_IP_RAW_PACKET_FILTER *** ile oluşturulmuş olabilir. Bu işlem modunda, uygulama, işlenmemiş bir protokol türüne sahip bir paket alındığında çağrılan bir geri çağırma işlevi sağlar. IP alma mantığı, paketi Kullanıcı tanımlı ham paket alma filtresi yordamına iletir. Filtre yordamı, ham paketin gelecekteki işlem için tutulup tutulmayacağını belirler. Geri çağırma yordamlarından gelen dönüş değeri, paketin ham paket alma filtresi tarafından işlenip işlenmediğini belirtir. Paket geri çağırma işlevi tarafından işlenirse, paket ile uygulama yapıldıktan sonra paketin yayımlanması gerekir. Aksi halde, NetX Duo, paketin serbest bırakılmasından sorumludur. Ham paket filtresi işlevinin kullanımı hakkında daha fazla bilgi için **_nx_ip_raw_packet_filter_set_** başvurun.

> [!NOTE]
> * NetX Duo için BSD sarmalayıcı işlevi, BSD ham yuvalarını işlemek için ham paket filtre işlevine dayanır. Bu nedenle, BSD sarmalayıcısında ham yuvayı desteklemek için, NetX Duo Kitaplığı ***NX_ENABLE_IP_RAW_PACKET_FILTER** _ tanımlı ile oluşturulmalıdır ve uygulamanın kendi ham paket filtresini yüklemek için _*_nx_ip_raw_packet_filter_set_*_ kullanmamalıdır Functions._

### <a name="default-packet-pool"></a>Varsayılan paket havuzu

Her IP örneğine oluşturma sırasında varsayılan bir paket havuzu verilir. Bu paket havuzu, ARP, RARP, ıCMP, ıGMP, çeşitli TCP denetim paketleri (SYN, ACK, vb.), komşu bulma, yönlendirici bulma ve yinelenen adres algılama için paket ayırmak üzere kullanılır. NetX Duo bir paket ayırması gerektiğinde varsayılan paket havuzu boşsa, NetX Duo belirli bir işlemi iptal etmek zorunda kalabilir ve mümkünse bir hata mesajı döndürür.

### <a name="ip-helper-thread"></a>IP Yardımcısı Iş parçacığı

Her bir IP örneğinin bir yardımcı iş parçacığı vardır. Bu iş parçacığı, tüm ertelenmiş paket işlemlerini ve tüm düzenli işlemleri işlemekten sorumludur. IP Yardımcısı iş parçacığı ***nx_ip_create oluşturulur.*** Burada iş parçacığına yığın ve öncelik verilir. IP Yardımcısı iş parçacığındaki ilk işleme, IP oluşturma hizmeti ile ilişkili ağ sürücüsü başlatma işlemini bitirebileceğinizi unutmayın. Ağ sürücüsü başlatma işlemi tamamlandıktan sonra, yardımcı iş parçacığı paket ve düzenli istekleri işlemek için sonsuz bir döngü başlatır.

> [!IMPORTANT]
> *IP Yardımcısı iş parçacığı içinde açıklanamayan davranış görüolduysa, IP oluşturma hizmeti sırasında yığın boyutunun artırılması ilk hata ayıklama adımıdır. Yığın çok küçükse, IP Yardımcısı iş parçacığı muhtemelen belleğin üzerine yazılmasına neden olabilir ve bu da olağan dışı sorunlara yol açabilir.*

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Ham IP paketleri alınmaya çalışılırken uygulama iş parçacıkları askıya alabilir. Bir ham paket alındıktan sonra yeni paket, askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı sürdürülür. Paketleri almak için NetX Duo Hizmetleri, isteğe bağlı askıya alma zaman aşımına uğradı. Bir paket alındığında veya zaman aşımı süresi dolduğunda, uygulama iş parçacığı uygun tamamlanma durumuyla sürdürülür.

### <a name="ip-statistics-and-errors"></a>IP Istatistikleri ve hataları

Etkinleştirilirse NetX Duo, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP örneği için aşağıdaki istatistikler ve hata raporları korunur:

- Toplam gönderilen IP paketi sayısı
- Toplam gönderilen IP bayt
- Toplam alınan IP paketi sayısı
- Toplam alınan IP bayt sayısı
- Toplam IP geçersiz paket sayısı
- Bırakılan toplam IP alma paketi sayısı
- Toplam IP alma sağlama toplamı hataları
- Bırakılan toplam IP gönderme paketi sayısı
- Toplam gönderilen IP parçacık
- Toplam alınan IP parçacığı sayısı

Bu istatistik ve hata raporlarının hepsi, ***nx_ip_info_get*** hizmeti ile uygulama tarafından kullanılabilir.

### <a name="ip-control-block-nx_ip"></a>IP denetim bloğu NX_IP

Her bir IP örneğinin özellikleri denetim bloğunda bulunur. Her ağ cihazının IP adresleri ve ağ maskeleri, bir komşu IP ve fiziksel donanım adresi eşleme tablosu gibi yararlı bilgiler içerir. Bu yapı, ***nx_api. h** _file tanımlanmıştır. IPv6 etkinleştirilirse, bir IPv6 adresi dizisi de içerir. bu sayı, Kullanıcı tarafından yapılandırılabilir seçenek _ *_NX_MAX_IPV6_ADDRESSES_* * ile belirtilir. Varsayılan değer, her fiziksel ağ arabiriminin üç IPv6 adresine sahip olmasına izin verir.

IP örneği denetim blokları bellekte herhangi bir yerde bulunabilir, ancak her bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır.

### <a name="static-ipv4-routing"></a>Statik IPv4 yönlendirmesi

Statik yönlendirme özelliği, bir uygulamanın ağ dışı hedef IP adresleri için bir IPv4 ağı ve sonraki atlama adresi belirlemesine izin verir. Statik yönlendirme etkinse NetX Duo, göndermek üzere paketin hedef adresiyle eşleşen bir giriş için statik yönlendirme tablosunda arama yapar. Hiçbir eşleşme bulunmazsa NetX Duo fiziksel arabirimlerin listesini arar ve hedef IP adresine ve ağ maskesine göre bir kaynak IP adresi ve sonraki atlama adresi seçer. Hedef, IP örneğine bağlı ağ sürücülerinin herhangi bir IP adresi ile eşleşmiyorsa, NetX Duo varsayılan ağ geçidine doğrudan bağlı bir arabirim seçer ve arabirimin IP adresini kaynak adresi olarak ve varsayılan ağ geçidini sonraki atlama olarak kullanır.

Girdiler, sırasıyla ***nx_ip_static_route_add** _ ve _ *_nx_ip_static_route_delete_** Hizmetleri kullanılarak statik yönlendirme tablosuna eklenebilir ve kaldırılabilir. Statik yönlendirmeyi kullanmak için, konak uygulamanın NX_ENABLE_IP_STATIC_ROUTING tanımlayarak bu özelliği etkinleştirmesi gerekir ***.***

> [!NOTE]
> *Statik yönlendirme tablosuna bir giriş eklenirken NetX Duo, tabloda zaten belirtilen hedef adresi için eşleşen bir giriş olup olmadığını denetler. Varsa, ağ maskesinde daha küçük ağ (daha uzun ön ek) ile giriş için tercih verir.*

### <a name="ipv4-forwarding"></a>IPv4 Iletme

Gelen IPv4 paketi bu düğüme yönelik değildir ve IPv4 iletme özelliği etkinse, NetX Duo, paketi diğer arabirimler üzerinden iletmeyi dener.  

### <a name="ip-fragmentation"></a>IP parçalanması

Ağ aygıtı, giden paketlerin boyutuyla sınırlı olabilir. Bu sınıra en fazla iletim birimi (MTU) denir. IP MTU, bir bağlantı katmanı sürücüsünün IP paketi fragmenting olmadan aktarabileceği en büyük IP çerçeve boyutudur. Bir cihaz sürücüsü başlatma aşaması sırasında, sürücü modülünün IP MTU boyutunu hizmet nx_ip_interface_mtu_set aracılığıyla yapılandırması gerekir ***.***

Önerilmese de, uygulama cihaz tarafından desteklenen temeldeki IP MTU değerinden daha büyük veri birimleri oluşturabilir. Bu IP veri birimini iletmeden önce, IP katmanı bu paketleri parçalara ayıramalıdır. Parçalanmış IP çerçevelerini alırken, alıcı uç, aynı parçalama KIMLIĞI olan tüm parçalanmış IP çerçevelerini depolamalıdır ve bunları sırayla yeniden birleştirmek zorunda olmalıdır. IP alma mantığı orijinal IP çerçevesini zaman içinde geri yüklemek için tüm parçaları toplayaamadığında tüm parçalar serbest bırakılır. Bu, bu tür paket kaybını tespit etmek ve buradan kurtarmak için üst katman protokolüne sahiptir.

IP parçalanması hem IPv4 hem de IPv6 paketlerine uygulanır.

IP parçalama ve yeniden birleştirme işlemini desteklemek için, sistem tasarımcısının ***nx_ip_fragment_enable*** hizmetini kullanarak NETX Duo 'daki IP parçalama özelliğini etkinleştirmesi gerekir. Bu özellik etkinleştirilmemişse, gelen parçalanmış IP paketlerinin yanı sıra ağ sürücüsünün MTU değerini aşan paketler de atılır.

> [!NOTE]
> * NetX Duo kitaplığı oluşturulurken, IP parçalanma mantığı ***NX_DISABLE_FRAGMENTATION** _ tanımlanarak tamamen kaldırılabilir. Bunun yapılması NetX Duo kod boyutunu azaltmaya yardımcı olur. Bu durumda, hem IPv4 hem de IPv6 parçalama/yeniden birleştirme işlevlerinin disabled._ olduğunu unutmayın.

> [!NOTE]
> ***NX_DISABLE_CHAINED_PACKET** TANıMLANMıŞSA, IP parçalanması devre dışı bırakılmalıdır.*

> [!NOTE]
> *Bir IPv6 ağında, veri biriminin boyutu minimum MTU boyutunu aşarsa, yönlendiriciler bir veri birimini parçalara vermez. Bu nedenle, kaynak ve hedef arasındaki en düşük MTU değerini tespit etmek ve IP veri birimi boyutunun yol MTU değerini aşmadığından emin olmak için gönderen cihaza kadar olur. NetX Duo sürümünde, IPv6 yolu MTU Keşfi, **NX_ENABLE_IPV6_PATH_MTU_DISCOVERY** tanımlı simgesiyle NETX Duo kitaplığı oluşturarak etkinleştirilebilir.*

## <a name="address-resolution-protocol-arp-in-ipv4"></a>IPv4 'de Adres Çözümleme Protokolü (ARP)

Adres Çözümleme Protokolü (ARP), 32 bitlik IPv4 adreslerini temel alınan fiziksel ortamlardan (RFC 826) dinamik olarak eşleştirmekten sorumludur. Ethernet en yaygın fiziksel medyadır ve 48 bit adreslerini destekler. ARP gereksinimi, ***nx_ip_create** _ hizmetine sağlanan ağ sürücüsüne göre belirlenir. Fiziksel eşleme gerekliyse, ağ sürücüsünün sürücü arabirimini düzgün şekilde yapılandırmak için _ *_nx_interface_address_mapping_needed_** hizmetini kullanması gerekir.

### <a name="arp-enable"></a>ARP etkinleştir

ARP 'nin düzgün çalışması için öncelikle ***nx_arp_enable*** hizmeti ile uygulama tarafından etkinleştirilmesi gerekir. Bu hizmet, ARP etkinleştirme hizmetine sağlanan bellekten bir ARP önbelleği alanı oluşturma da dahil olmak üzere, ARP işleme için çeşitli veri yapıları ayarlar.

### <a name="arp-cache"></a>ARP önbelleği

ARP önbelleği, iç ARP eşleme veri yapılarının bir dizisi olarak görüntülenebilir. Her iç yapı, bir IP adresi ile fiziksel bir donanım adresi arasındaki ilişkiyi koruma kapasitesine sahiptir. Ayrıca, her veri yapısının birden fazla bağlantılı listenin parçası olması için bağlantı işaretçileri vardır.

Uygulama, ARP tablosunda eşleme varsa, "**nx_arp_ip_address_find** _ hizmetini kullanarak donanım Mac adresı sağlayarak ARP ÖNBELLEĞINDEN bir IP adresi arayabilir. Benzer şekilde, _ *_nx_arp_hardware_address_find_** hizmeti belırlı bir IP adresı için Mac adresini döndürür.

### <a name="arp-dynamic-entries"></a>ARP dinamik girdileri

Varsayılan olarak, ARP etkinleştirme hizmeti, tüm girişleri kullanılabilir dinamik ARP girişleri listesindeki ARP önbelleğine koyar. Eşlenmemiş bir IP adresine gönderilen istek algılandığında NetX Duo tarafından bu listeden dinamik bir ARP girişi ayrılır. Ayırma işleminden sonra ARP girdisi ayarlanır ve fiziksel medyaya bir ARP isteği gönderilir.

Ayrıca, hizmet ***nx_arp_dynamic_entry_set*** bir dinamik giriş de oluşturulabilir.

> [!IMPORTANT]
> *Tüm dinamik ARP girişleri kullanımda ise, en az kullanılan ARP girişi yeni bir eşleme ile değiştirilmiştir.*

### <a name="arp-static-entries"></a>ARP statik girdileri

Uygulama, ***nx_arp_static_entry_create** _Service kullanarak statik ARP eşlemesi de ayarlayabilir. Bu hizmet, dinamik ARP giriş listesinden bir ARP girişi ayırır ve uygulama tarafından sağlanan eşleme bilgilerini kullanarak statik listeye koyar. Statik ARP girdileri yeniden kullanım veya yaşlandırma uygulanmaz. Uygulama, hizmet _*_nx_arp_static_entry_delete_*_ kullanarak statik bir girişi silebilir. ARP tablosundaki tüm statik girişleri kaldırmak için uygulama, _ *_nx_arp_static_entries_delete_* * hizmetini kullanabilir.

### <a name="automatic-arp-entry"></a>Otomatik ARP girdisi

NetX Duo, ARP isteğine eş yanıtlardan sonra eşin IP/MAC eşlemesini kaydeder. NetX Duo, ağ üzerinden gelen istenmeyen ARP isteklerine göre eş IP/MAC adresi eşlemesini kaydeden otomatik ARP girişi özelliğini de uygular. Bu özellik ARP tablosunun, bu ARP isteği/yanıt döngüsünü ilerlemek için gereken gecikmeyi azaltarak, eş bilgilerle doldurulmasını sağlar. Ancak, otomatik ARP 'yi etkinleştirme ile ilgili diğer taraf ARP tablosunun, yerel bağlantı üzerinde çok sayıda düğüm bulunan meşgul bir ağda hızlı bir şekilde doldurulmasına yol açacağından, bu durum sonunda ARP girişi değişikliği gerçekleşmektedir.

Bu özellik varsayılan olarak etkindir. Devre dışı bırakmak için, NetX Duo kitaplığı tanımlı ***NX_DISABLE_ARP_AUTO_ENTRY*** simgesiyle derlenmiş olmalıdır.</p>

### <a name="arp-messages"></a>ARP Iletileri

Daha önce belirtildiği gibi, IP görevi bir IP adresi için eşlemenin gerekli olduğunu algıladığında bir ARP istek iletisi gönderilir. ARP istekleri, karşılık gelen bir ARP yanıtı alınana kadar düzenli aralıklarla (her ***NX_ARP_UPDATE_RATE** _ saniyede) gönderilir. ARP denemesi terk edilmeden önce toplam _ *_NX_ARP_MAXIMUM_RETRIES_** ARP isteği yapılır. Bir ARP yanıtı alındığında, ilişkili fiziksel adres bilgileri önbellekte olan ARP girişinde depolanır.

NetX Duo, çok ana sistemler için, belirtilen hedef adrese göre ARP isteklerinin ve yanıtlarının gönderileceği arabirimi belirler.

> [!NOTE]
> *NetX Duo ARP yanıtı beklerken giden IP paketleri sıraya alınır. Kuyruğa alınan giden IP paketlerinin sayısı, sabit **NX_ARP_MAX_QUEUE_DEPTH** tarafından tanımlanır.*

NetX Duo Ayrıca yerel IPv4 ağındaki diğer düğümlerden gelen ARP isteklerine yanıt verir. ARP isteğini alan arabirimin geçerli IP adresiyle eşleşen bir dış ARP isteği yapıldığında NetX Duo, geçerli fiziksel adresi içeren bir ARP yanıt iletisi oluşturur.

Ethernet ARP isteklerinin ve yanıtlarının biçimleri Şekil 6 ' da gösterilir ve aşağıda açıklanmıştır.

| **İstek/yanıt &nbsp; alanı**         | **Amaç**            |
| ---------------------------------- | ---------------------- |
| ***Ethernet hedef adresi*** | Bu 6 baytlık alan ARP yanıtının hedef adresini içerir ve ARP istekleri için bir yayındır (tümü). Bu alan, ağ sürücüsü tarafından ayarlanır. 
| ***Ethernet kaynak adresi***      | Bu 6 baytlık alan, ARP isteği veya yanıtı göndericisinin adresini içerir ve ağ sürücüsü tarafından ayarlanır. |
| ***Çerçeve türü*** | Bu 2 baytlık alan, mevcut Ethernet çerçevesinin türünü ve ARP istekleri ve yanıtları için 0x0806 ' ya eşittir. Bu, ağ sürücüsünün ayarlamaktan sorumlu olduğu son alandır. |
| ***Donanım türü*** | Bu 2 baytlık alan, Ethernet için 0x0001 olan donanım türünü içerir. |
| ***Protokol türü*** | Bu 2 baytlık alan, IP adresleri için 0x0800 olan protokol türünü içerir. |
| ***Donanım boyutu*** | Bu 1 baytlık alan, Ethernet adresleri için 6 olan donanım adresi boyutunu içerir. |

![ARP paket biçiminin diyagramı.](./media/user-guide/arp-packet-format.png)

**ŞEKIL 6. ARP paket biçimi**

| İstek/yanıt &nbsp; alanı | Amaç |
|---|---|
| ***Protokol boyutu*** | Bu 1 baytlık alan, IP adresleri için 4 olan IP adresi boyutunu içerir. |
| ***İşlem kodu*** | Bu 2 baytlık alan, bu ARP paketinin işlemini içerir. Bir ARP yanıtı, 0x0002 değeri ile temsil edilirken, 0x0001 değeri ile bir ARP isteği belirtilir. |
| ***Gönderici Ethernet adresi*** | Bu 6 baytlık alan, gönderenin Ethernet adresini içerir. |
| ***Gönderenin IP adresi*** | Bu 4 baytlık alan gönderenin IP adresini içerir. |
| ***Hedef Ethernet adresi*** | Bu 6 baytlık alan, hedefin Ethernet adresini içerir. |
| ***Hedef IP adresi*** | Bu 4 baytlık alan, hedefin IP adresini içerir. |

> [!NOTE]
> *ARP istekleri ve yanıtları Ethernet düzeyindeki paketlerdir. Diğer tüm TCP/IP paketleri bir IP paket üstbilgisiyle kapsüllenir.*

> [!NOTE]
> *TCP/IP uygulamasındaki tüm ARP iletilerinin **Big endian** biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

### <a name="arp-aging"></a>ARP eskime

NetX, otomatik dinamik ARP girişi geçersiz doğrulamasını destekler. ***NX_ARP_EXPIRATION_RATE** _, belırlenen bir IP adresinin fiziksel eşlemenin geçerli kaldığı saniye sayısını belirtir. Süre dolduktan sonra ARP girişi ARP önbelleğinden kaldırılır. Karşılık gelen IP adresine gönderme denemesi, yeni bir ARP isteğine neden olur. _ *_NX_ARP_EXPIRATION_RATE_** değerini sıfıra ayarlamak, varsayılan yapılandırma olan ARP eskimesini devre dışı bırakır.

### <a name="arp-defend"></a>ARP savun

Bir ARP isteği veya ARP yanıt paketi alındığında ve gönderici aynı IP adresine sahip olduğunda ve bu düğümün IP adresiyle çakışıyorsa, NetX Duo, bu adres için bir savunma olarak bir ARP isteği gönderir. Çakışma ARP paketi 10 saniye içinde birden çok kez alınmışsa NetX Duo daha fazla savunma paketi göndermez. Varsayılan Aralık 10 saniye, ***NX_ARP_DEFEND_INTERVAL** _ tarafından yeniden tanımlanabilir. Bu davranış, RFC5227 (c) üzerinde belirtilen ilkeyi izler. Windows XP ARP bildirisini ARP araştırması için bir yanıt olarak yoksaydığından, Kullanıcı, ARP yanıtını ek erteleme olarak göndermek için _ *_NX_ARP_DEFEND_BY_REPLY_** tanımlayabilir.

### <a name="arp-statistics-and-errors"></a>ARP Istatistikleri ve hataları

Etkinleştirilirse, NetX Duo ARP yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Aşağıdaki istatistikler ve hata raporları her IP 'nin ARP işlemleri için tutulur:

- Gönderilen toplam ARP Isteği sayısı
- Alınan toplam ARP Isteği sayısı
- Gönderilen toplam ARP yanıtı 
- Alınan toplam ARP yanıtı 
- Toplam ARP dinamik girişleri 
- Toplam ARP statik girişleri 
- Toplam ARP eski girdileri 
- Toplam ARP geçersiz Iletileri 

Bu istatistik ve hata raporlarının tümü, ***nx_arp_info_get*** hizmeti ile uygulama tarafından kullanılabilir.

## <a name="reverse-address-resolution-protocol-rarp-in-ipv4"></a>IPv4 'de ters Adres Çözümleme Protokolü (RARP)

Ters Adres Çözümleme Protokolü (RARP), konağın 32 bit IP adreslerinin (RFC 903) ağ atamasını istemek için protokoldür. Bu, bir RARP isteği aracılığıyla yapılır ve bir ağ üyesi bir RARP yanıtında ana bilgisayar ağ arabirimine bir IP adresi atalana kadar düzenli olarak devam eder. Uygulama, sıfır IP adresine sahip hizmet ***nx_ip_create*** bir IP örneği oluşturur. RARP uygulama tarafından etkinleştirilmişse, ağ sunucusundan, sıfır IP adresine sahip arabirim aracılığıyla erişilebilen bir IP adresi istemek için RARP protokolünü kullanabilir.

### <a name="rarp-enable"></a>RARP etkinleştir

RARP 'yi kullanmak için, uygulamanın IP adresi sıfır olan IP örneğini oluşturması ve ardından hizmet ***nx_rarp_enable*** kullanarak RARP 'yi etkinleştirmesi gerekir. Çoklu giriş sistemlerinde, IP örneğiyle ilişkilendirilmiş en az bir ağ cihazının IP adresi sıfır olmalıdır. RARP işleme, ağ tarafından atanan IP adresi ile geçerli bir RARP yanıtı alınana kadar bir IP adresi gerektiren NetX Duo sistemine yönelik olarak RARP istek iletileri gönderir. Bu noktada, RARP işleme tamamlanmıştır.

RARP etkinleştirildikten sonra, tüm arabirim adresleri çözümlendikten sonra otomatik olarak devre dışıdır. Uygulama, Service ***nx_rarp_disable*** kullanarak RARP 'yi sonlandırmayı zorlayabilir.

### <a name="rarp-request"></a>RARP Isteği

Bir RARP istek paketinin biçimi, [Şekil 6](#arp-messages)' da gösterilen ARP paketiyle neredeyse aynıdır. Tek fark, çerçeve türü alanı 0x8035 ve *Işlem kodu* alanı 3 ' tür ve bır RARP isteği tanımlayarak 3 ' tür. Daha önce belirtildiği gibi, RARP istekleri düzenli aralıklarla (her ***NX_RARP_UPDATE_RATE*** saniyede), ağ atanmış IP adresine sahıp bır RARP yanıtı alınana kadar gönderilir.

> [!NOTE]
> *TCP/IP uygulamasındaki tüm RARP iletilerinin **Big endian** biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

### <a name="rarp-reply"></a>RARP yanıtı

RARP yanıt iletileri ağdan alınır ve bu konak için ağ tarafından atanan IP adresini içerir. Bir RARP yanıt paketinin biçimi, Şekil 6 ' da gösterilen ARP paketiyle neredeyse aynıdır. Tek fark, çerçeve türü alanı 0x8035 ' dir ve *Işlem kodu* alanı, BIR RARP yanıtı atayan 4 ' tür. Aldıktan sonra IP adresi IP örneğinde ayarlanır, düzenli olarak RARP isteği devre dışıdır ve IP örneği artık normal ağ işlemleri için hazırdır.

Çok ana konaklar için IP adresi, isteyen ağ arabirimine uygulanır. Hala bir IP adresi ataması isteğinde bulunan başka ağ arabirimleri varsa, tüm Arabirim IP adresi istekleri çözümlenene kadar düzenli RARP hizmeti devam eder.

> [!NOTE]
> *Uygulama, RARP işlemesi tamamlanana kadar IP örneğini kullanmamalıdır. **Nx_ip_status_check** , uygulamalar tarafından RARP tamamlanmasını beklemek için kullanılabilir. Çoklu giriş sistemlerinde, bu arabirim üzerinde RARP işlemesi tamamlanana kadar uygulama istekte bulunan arabirimini kullanmamalıdır. İkincil cihazdaki IP adresinin durumu **nx_ip_interface_status_check** hizmetiyle denetlenebilir.*

### <a name="rarp-statistics-and-errors"></a>RARP Istatistikleri ve hataları

Etkinleştirilirse, NetX Duo RARP yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP 'nin RARP işlemesi için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen toplam RARP Isteği
- Toplam alınan RARP yanıtı
- Toplam RARP geçersiz Ileti

Bu istatistik ve hata raporlarının tümü, ***nx_rarp_info_get*** hizmeti ile uygulama tarafından kullanılabilir.

## <a name="internet-control-message-protocol-icmp"></a>Internet Denetim Iletisi Protokolü (ıCMP)

IPv4 için Internet Denetim Iletisi Protokolü (ıCMP), IP ağ üyeleri arasında hata ve denetim bilgilerini geçirme ile sınırlıdır. IPv6 için Internet Denetim Iletisi Protokolü (Icmpv6) Ayrıca hata ve denetim bilgilerini işler ve yinelenen adres algılama (BABACıĞıM) ve durum bilgisiz adresi otomatik yapılandırması gibi adres çözümleme protokolleri için gereklidir.

Diğer çoğu uygulama katmanının (örn. TCP/IP) iletileri, ıCMP ve ICMPv6 iletileri, ıCMP (veya ICMPv6) protokolü atamasının bulunduğu bir IP üstbilgisiyle kapsüllenir.

### <a name="icmp-statistics-and-errors"></a>ICMP Istatistikleri ve hataları

Etkinleştirilirse NetX Duo, uygulama için yararlı olabilecek birkaç ıCMP istatistiğini ve hatasını izler. Her IP 'nin ıCMP işlemi için aşağıdaki istatistikler ve hata raporları korunur: 

- Gönderilen toplam ıCMP pingi  
- Toplam ıCMP ping zaman aşımları 
- Askıya alınan toplam ıCMP ping Iş parçacığı 
- Alınan toplam ıCMP ping yanıtı 
- Toplam ıCMP sağlama toplamı hatası 
- Toplam ıCMP Işlenmemiş Ileti 

Bu istatistik ve hata raporlarının tümü, ***nx_icmp_info_get*** hizmeti ile uygulama tarafından kullanılabilir.

## <a name="icmpv4-services-in-netx-duo"></a>NetX Duo 'da Icmpv4 Hizmetleri

### <a name="icmpv4-enable"></a>ICMPv4 etkinleştir

ICMPv4 iletilerinin NetX Duo tarafından işlenebilmesi için, uygulamanın, Icmpv4 işlemesini etkinleştirmek üzere ***nx_icmp_enable*** hizmetini çağırması gerekir. Bu işlem yapıldıktan sonra uygulama, ping istekleri ve alan gelen ping paketleri verebilir.  

### <a name="icmpv4-echo-request"></a>ICMPv4 yankı Isteği

Yankı isteği, ana bilgisayar IP adresi tarafından tanımlanan şekilde ağ üzerinde belirli bir düğümün varlığını denetlemek için kullanılan bir Icmpv4 iletisi türüdür. Popüler ping komutu, ıCMP yankı isteği/Yankı Yanıtı iletileri kullanılarak uygulanır. Belirli bir konak mevcutsa, ağ yığını ping isteğini ve ping yanıtı ile yanıtları işler. Şekil 7 ' de, Icmpv4 ping iletisi biçimi ayrıntılı olarak gösterilmiştir.

![ICMPv4 ping Iletisi](./media/user-guide/icmpv4-ping-message.png)  

**ŞEKIL 7. ICMPv4 ping Iletisi**

> [!NOTE]
> *TCP/IP uygulamasındaki tüm Icmpv4 iletilerinin **Big endian** biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

Aşağıda, Icmpv4 üst bilgi biçimi açıklanmaktadır:

|Üst bilgi alanı |Amaç |
|---|---|
|**Tür** |Bu alan, Icmpv4 iletisini belirtir (BITS 31-24). En yaygın olarak:<br />-0: yankı yanıtı<br />-3: hedefe ulaşılamıyor<br />-8: yankı Isteği<br />-11: süre aşıldı<br />-12: parametre sorunu |
|**Kod** |Bu alan, tür alanındaki bağlamdır (BITS 23-16). Yankı isteği için veya yanıt kodu sıfır olarak ayarlanır.|
|**Toplam** |Bu alan, tür alanı ile başlayan Icmpv4 üstbilgisinin tamamı de dahil olmak üzere, bir adet toplam Icmpv4 iletisi için 16 bit sağlama toplamı içerir. Sağlama toplamını oluşturmadan önce, sağlama toplamı alanı temizlenir.|
|**Kimlik** | Bu alan, Konağı tanımlayan bir KIMLIK değeri içerir; Ana bilgisayar, YANKı YANıTıNDA YANKı isteğinden ayıklanan KIMLIĞI kullanmalıdır (BITS 31-16).|
|**Sıra numarası** |Bu alan bir KIMLIK değeri içerir; Ana bilgisayar, YANKı YANıTıNDA YANKı isteğinden ayıklanan KIMLIĞI kullanmalıdır (BITS 31-16). Tanımlayıcı alanından farklı olarak, bu değer aynı ana bilgisayardan gelen bir sonraki yankı isteğinde de değişecektir (BITS 15-0).|

### <a name="icmpv4-echo-response"></a>ICMPv4 yankı yanıtı    
Ping yanıtı, dış bir ping isteğine yanıt olarak ıCMP bileşeni tarafından dahili olarak oluşturulan başka bir ıCMP iletisi türüdür. Onay komutuna ek olarak, ping yanıtı da ping isteğinde sağlanan kullanıcı verilerinin bir kopyasını içerir.

### <a name="icmpv4-error-messages"></a>ICMPv4 hata Iletileri   
NetX Duo 'da aşağıdaki Icmpv4 hata iletileri desteklenir: 
- Hedefe ulaşılamıyor 
- Süre aş 
- Parametre sorunu

## <a name="internet-group-management-protocol-igmp"></a>Internet Grup Yönetimi Protokolü (IGMP)

Internet Grup Yönetimi Protokolü (ıGMP), komşileriyle iletişim kurmak için bir cihaz sağlar ve bir IPv4 çok noktaya yayın grubu (RFC 1112 ve RFC 2236) almayı veya katılmayı amaçladığı yönlendiricileriyle iletişim kurar. Çok noktaya yayın grubu temel olarak dinamik bir ağ üyeleri koleksiyonudur ve bir sınıf D IP adresi ile temsil edilir. Çok noktaya yayın grubunun üyeleri herhangi bir zamanda bırakabilir ve yeni üyeler istediğiniz zaman katılabilir. Gruba katılma ve gruptan ayrılmayla ilgili koordinasyon, ıGMP 'nin sorumluluğundadır.

> [!NOTE]
> *IGMP yalnızca IPv4 çok noktaya yayın grupları için tasarlanmıştır. IPv6 ağında kullanılamaz.*

### <a name="igmp-enable"></a>IGMP etkinleştirme     
NetX Duo 'da herhangi bir çok noktaya yayın etkinliğinin gerçekleşmesi için, uygulamanın ***nx_igmp_enable*** hizmetini çağırması gerekir. Bu hizmet, çok noktaya yayın isteklerini hazırlamak için temel ıGMP başlatmayı gerçekleştirir.

### <a name="multicast-ipv4-addressing"></a>Çok noktaya yayın IPv4 adresleme  
Daha önce belirtildiği gibi, çok noktaya yayın adresleri aslında [Şekil 4](#ipv4-addresses)' te gösterildiği gibi sınıf D IP adresleridir. D adresinin daha düşük 28 bit düzeyi çok noktaya yayın grubu KIMLIĞINE karşılık gelir. Önceden tanımlanmış bir dizi çok noktaya yayın adresi vardır; Ancak, *tüm ana bilgisayarlar adresi* (244.0.0.1) özellikle IGMP işleme için önemlidir. *Tüm konaklar adresi* , yönlendiriciler tarafından, ait oldukları çok noktaya yayın gruplarını raporlamak üzere tüm çok noktaya yayın üyelerini sorgulamak için kullanılır.  

### <a name="physical-address-mapping-in-ipv4"></a>IPv4 'de fiziksel adres eşleme
Sınıf D çok noktaya yayın adresleri doğrudan 01.00.5 e. 00.00.00 ile 01.00.5 e. 7f. ff. FF arasında değişen fiziksel Ethernet adreslerine eşlenir. IP çok noktaya yayın adresinin daha düşük 23 biti, Ethernet adresinin daha düşük 23 bitmine doğrudan eşlenir.

### <a name="multicast-group-join"></a>Çok noktaya yayın grubuna ekleme
Belirli bir çok noktaya yayın grubuna katılması gereken uygulamalar, ***nx_igmp_multicast_join*** hizmetini çağırarak bunu yapabiliriz. Bu hizmet, bu çok noktaya yayın grubuna katılması için istek sayısını izler. Bu, çok noktaya yayın grubuna katılması için ilk uygulama isteksiz ise, birincil ağda bu konağın gruba katılması için bir ıGMP raporu gönderilir. Daha sonra, ağ sürücüsü bu çok noktaya yayın grubu için Ethernet adresine sahip paketleri dinlemek üzere ayarlanır.

Çoklu giriş sisteminde, çok noktaya yayın grubuna belirli bir arabirim üzerinden erişilebiliyorsa, uygulama birincil ağdaki çok noktaya yayın gruplarıyla sınırlı olan _ *_nx_igmp_multicast_join_* * yerine ***nx_igmp_multicast_interface_join** _ hizmetini kullanır.

### <a name="multicast-group-leave"></a>Çok noktaya yayın grubu bırakma   
Daha önce birleştirilmiş bir çok noktaya yayın grubuna ayrılmaları gereken uygulamalar, ***nx_igmp_multicast_leave*** hizmetini çağırarak bunu yapamayabilir. Bu hizmet, grubun kaç kez katıldığı ile ilişkili iç sayıyı azaltır. Bir grup için bekleyen bir JOIN isteği yoksa, bu çok noktaya yayın grubunun Ethernet adresine sahip paketleri dinlemeyi devre dışı bırakmak için ağ sürücüsü çağırılır.

### <a name="multicast-loopback"></a>Çok noktaya yayın geri döngüsü    
Bir uygulama, aynı düğümdeki kaynaklardan birinden kaynaklanan çok noktaya yayın trafiğini almak isteyebilir. Bu, hizmet ***nx_igmp_loopback_enable*** kullanılarak IP çok noktaya yayın bileşeninin geri döngüden etkinleştirilmesini gerektirir.

### <a name="igmp-report-message"></a>IGMP rapor Iletisi      
Uygulama bir çok noktaya yayın grubuna katıldığında, ana bilgisayarın belirli bir çok noktaya yayın grubuna katılma işlemini göstermek için ağ üzerinden bir ıGMP rapor iletisi gönderilir. IGMP rapor iletisinin biçimi Şekil 8 ' de gösterilir. Çok noktaya yayın grubu adresi, ıGMP rapor iletisindeki Grup iletisi ve hedef IP adresi için kullanılır.

Yukarıdaki şekilde (Şekil 8), ıGMP üstbilgisi bir sürüm/tür alanı ve en fazla yanıt içerir

![Bir ıGMP rapor iletisinin diyagramı.](./media/user-guide/image17.jpg)

**ŞEKIL 8. IGMP rapor Iletisi**

zaman, sağlama toplamı alanı ve çok noktaya yayın grubu adres alanı. IGMPv1 iletileri için, IGMPv1 protokolünün bir parçası olmadığından en fazla yanıt süresi alanı her zaman sıfır olarak ayarlanır. En fazla yanıt süresi alanı, ana bilgisayar bir sorgu türü bir ıGMP iletisi aldığında ayarlanır ve bir konak, IGMPv2 protokolü tarafından tanımlanan başka bir ana bilgisayarın rapor türü iletisini aldığında temizlenir.

Aşağıda, ıGMP üst bilgi biçimi açıklanmaktadır:

|Üst bilgi alanı|Amaç|
|---|---|
|**Sürüm** |Bu alan, ıGMP sürümünü belirtir (BITS 31-28).|
|**Tür** |Bu alan, ıGMP iletisinin türünü belirtir (BITS 27 -24).|
|**En fazla yanıt süresi** |, IGMP v1 'de kullanılmaz. IGMP v2 'de bu alan en uzun yanıt süresi olarak görev yapar.|
|**Toplam** |Bu alan, ıGMP sürümünden başlayarak, ıGMP iletisinin tamamlama toplamı için 16 bit sağlama toplamı içerir (BITS 0-15)|
|**Grup adresi** |32-bit sınıfı D grup IP adresi|

IGMP rapor iletileri, çok noktaya yayın yönlendiricisi tarafından gönderilen ıGMP sorgu iletilerine yanıt olarak da gönderilir. Çok noktaya yayın yönlendiricileri, hangi konağın hala grup üyeliği gerektirdiğini görmek üzere sorgu iletilerini düzenli aralıklarla gönderir. Sorgu iletileri, Şekil 8 ' de gösterilen ıGMP rapor iletisiyle aynı biçimde olmalıdır. Tek farklar ıGMP türüdür ve grup adresi alanı 0 olarak ayarlanır. IGMP sorgu iletileri, çok noktaya yayın yönlendiricisi tarafından *tüm konaklar* IP adresine gönderilir. Grup üyeliğini sürdürmeye devam eden bir ana bilgisayar, başka bir ıGMP rapor iletisi göndererek yanıt verir.

> [!NOTE]
> *TCP/IP uygulamasındaki tüm iletilerin **Big endian** biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

### <a name="igmp-statistics-and-errors"></a>IGMP Istatistikleri ve hataları    
<th><p>Etkinleştirilirse, NetX Duo ıGMP yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP 'nin ıGMP işlemi için aşağıdaki istatistikler ve hata raporları korunur: 

- Gönderilen toplam ıGMP raporu 
- Alınan toplam ıGMP sorgusu sayısı 
- Toplam ıGMP sağlama toplamı hataları 
- Toplam ıGMP geçerli grup 

Bu istatistik ve hata raporlarının tümü, ***nx_igmp_info_get*** hizmeti ile uygulama tarafından kullanılabilir. 

### <a name="multicast-without-igmp"></a>IGMP olmadan çok noktaya yayın  
IPv4 çok noktaya yayın trafiği bekleyen uygulama, Service ***nx_ipv4_multicast_interface_join*** kullanarak IGMP iletileri çağırmadan çok noktaya yayın grubu adresine katılabilir. Bu hizmet, IPv4 katmanını ve temel alınan arabirim sürücüsünü belirtilen IPv4 çok noktaya yayın adresinden paketleri kabul edecek şekilde yönlendirir. Ancak, bu grup için gönderilen veya işlenen bir ıGMP Grup Yönetim iletisi yoktur.

Uygulama artık gruptan trafik almak istemiyor hizmeti ***nx_ipv4_multicast_interface_leave kullanabilir.***

## <a name="ipv6-in-netx-duo"></a>NetX Duo 'da IPv6

### <a name="ipv6-addresses"></a>IPv6 adresleri   
IPv6 adresleri 128 bittir. IPv6 adresi mimarisi, RFC 4291 ' de açıklanmaktadır. Adres en önemli bitleri ve alt bitleri içeren bir ana bilgisayar adresini içeren bir ön eke bölünmüştür. Ön ek, adresin türünü gösterir ve, IPv4 ağındaki ağ adresinin kabaca eşdeğeridir.

IPv6 'nın üç tür adres belirtimi vardır: tek noktaya yayın, her noktaya yayın (NetX Duo 'da desteklenmez) ve çok noktaya yayın. Tek noktaya yayın adresleri, Internet 'teki belirli bir konağı tanımlayan IP adresleridir. Tek noktaya yayın adresleri bir kaynak ya da hedef IP adresi olabilir. Çok noktaya yayın adresleri Internet 'teki bir dinamik konaklar grubunu belirtir. Çok noktaya yayın grubunun üyeleri her istediklerinde katılabilir ve bırakabilir.

IPv6, IPv4 yayın mekanizmasına eşit değildir. Tüm konaklara paket gönderebilme özelliği, bağlantı yerel tüm konaklar çok noktaya yayın grubuna bir paket gönderilerek elde edilebilir.

IPv6, komşu bulma, yönlendirici bulma ve durum bilgisi Içermeyen adres otomatik yapılandırma yordamlarını gerçekleştirmek için çok noktaya yayın adreslerini kullanır.

İki tür IPv6 tek noktaya yayın adresi vardır: genellikle bilinen bağlantı yerel önekini, arabirim MAC adresiyle birleştirerek oluşturulan yerel adresleri ve ayrıca önek bölümü ve ana bilgisayar KIMLIĞI bölümünü içeren genel IP adreslerini birleştirerek oluşturulur. Genel bir adres el ile veya durum bilgisiz adresi veya DHCPv6 aracılığıyla yapılandırılabilir. NetX Duo hem bağlantı yerel adresini hem de genel adresi destekler.

NetX Duo hem IPv4 hem de IPv6 biçimlerine uyum sağlamak için, IPv4 ve IPv6 adreslerini tutmak üzere NXD_ADDRESS yeni bir veri türü sağlar. Bu yapının tanımı aşağıda gösterilmiştir. Adres alanı, IPv4 ve IPv6 adreslerinin bir birleşimidir.

```c
typedef struct NXD_ADDRESS_STRUCT
{
    ULONG nxd_ip_version;
    union
    {
        ULONG v4;
        ULONG v6[4];
    } nxd_ip_address;
} NXD_ADDRESS;
```

NXD_ADDRESS yapısında, *nxd_ip_version* Ilk öğesi IPv4 veya IPv6 sürümünü gösterir. Desteklenen değerler NX_IP_VERSION_V4 ya da NX_IP_VERSION_V6. *nxd_ip_version* , *nxd_ip_address* UNION alanındaki hangi alanın IP adresi olarak kullanılacağını gösterir. NetX Duo API hizmetleri, genellikle ULONG (32 bit) IP adresi yerine giriş bağımsız değişkeni olarak NXD_ADDRESS yapısına yönelik bir işaretçi alır.

### <a name="link-local-addresses"></a>Yerel adresleri bağla     
Bağlantı yerel adresi yalnızca yerel ağda geçerlidir. Bir cihaz, geçerli bir bağlantı yerel adresi atandıktan sonra aynı ağdaki başka bir cihaza paket gönderebilir ve alabilir. Uygulama, NetX Duo hizmeti ***nxd_ipv6_address_set*** çağırarak bir bağlantı yerel adresi atar ve önek uzunluğu parametresi 10 olarak ayarlanır. Uygulama hizmete bir bağlantı yerel adresi sağlayabilir veya bağlantı yerel adresi olarak NX_NULL kullanabilir ve NetX Duo cihazın MAC adresine göre bağlantı yerel adresi oluşturmasına izin verebilir.

Aşağıdaki örnek, NetX Duo 'un MAC adresini kullanarak birincil cihazdaki (Dizin 0) bağlantı yerel adresini bir önek uzunluğu olan 10 ' un yapılandırmasını sağlar:

```c
nxd_ipv6_address_set(ip_ptr, 0, NX_NULL, 10, NX_NULL);
```
Yukarıdaki örnekte, arabirimin MAC adresi 54:32:10:1A: BC: 67 ise, buna karşılık gelen bağlantı yerel adresi şöyle olur:

```c
FE80::5632:10FF:FE1A:BC67
```
IPv6 adresinin ana bilgisayar KIMLIĞI bölümünün (**5632:10FF: FE1A: BC67**), aşağıdaki değişikliklerle 6 baytlık Mac adresinden yapıldığını unutmayın:

- **0Xfffe** , byte 3 ve Mac adresinin Byte 4 arasına eklenmiştir
- MAC adresinin (U/L bit) ilk baytının ikinci en düşük biti 1 olarak ayarlanmıştır

IPv6 adresinin ana bilgisayar bölümünün arabirim MAC adresinden nasıl oluşturulacağı hakkında daha fazla bilgi için bkz. RFC 2464 (Ethernet ağı üzerinden IPv6 paketlerini Iletim).

IPv6 'daki bir veya daha fazla konağa çok noktaya yayın iletileri göndermek için birkaç özel çok noktaya yayın adresi vardır:

| Grup  | Adres   | Açıklama  |
|---|---|---|
|Tüm düğümler grubu |**FF02:: 1** |Yerel ağdaki tüm konaklar|
|Tüm yönlendiriciler grubu |**FF02:: 2** |Yerel ağdaki tüm yönlendiriciler|
|İstek düğümü |**FF02:: 1: FF00:0/104** |Aşağıda açıklanmıştır|

İstek düğüm çok noktaya yayın adresi, tüm IPv6 Konakları yerine, yerel bağlantıda belirli Konakları hedefler. **FF02:: 1: FF00:0/104** önekini içerir. bu değer 104 bittir ve hedef IPv6 adresinin son 24 bittir. Örneğin, **205B: 209D: D028:: F058: D1C8:1024** bir IPv6 adresi, adres **FF02:: 1: FFC8:1024**.

> [!IMPORTANT]
> İki *nokta üst üste Gösterim, aradaki bitlerin tümünün sıfırlardan olduğunu gösterir. **FF02:: 1: FF00:0/104** tam genişletilmiş gibi görünüyor* **FF02:0000:0000:0000:0000:0001: FF00:0000**

### <a name="global-addresses"></a>Genel adresler    
Bir IPv6 genel adresine örnek **2001:0123:4567:89AB: CDEF:: 1** NETX Duo ıpv6 adreslerini NXD_ADDRESS yapısında depolar. Aşağıdaki örnekte, **global_ipv6_address** NXD_ADDRESS değişkeni bir tek noktaya yayın IPv6 adresi içerir. Aşağıdaki örnek, birincil aygıtı için belirli bir IPv6 genel adresi oluşturan NetX Duo cihazını göstermektedir:

```c
NXD_ADDRESS global_ipv6_address;
UINT        primary_interface_index = 0;

global_ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
global_ipv6_address.nxd_ip_address.v6[0] = 0x20010123;
global_ipv6_address.nxd_ip_address.v6[1] = 0x456789AB;
global_ipv6_address.nxd_ip_address.v6[2] = 0xCDEF0000;
global_ipv6_address.nxd_ip_address.v6[3] = 0x00000001;

status = nxd_ipv6_address_set(
            &ip_0,
            primary_interface_index,
            &global_ipv6_address,
            64,
            NX_NULL);
```
Bu IPv6 adresinin ön ekinin **2001:0123:4567:89AB** olduğunu ve bu 64 bit uzunluğunda olduğunu ve Ethernet üzerinde genel tek noktaya yayın IPv6 adresleri için ortak bir ön ek uzunluğu olduğunu unutmayın.

NXD_ADDRESS yapısı da IPv4 adreslerini barındırır. Global_ipv4_address depolanan **192.1.168.10** (**0xc001a80a**) IP adresi aşağıdaki bellek düzenine sahip olacaktır:

|Alan |Değer |
|---|---|
|global_ipv4_address global_ipv4_address.nxd_ip_version |NX_IP_VERSION_V4|
|global_ipv4_address global_ipv4_address.nxd_ip_address. v4 |0xC001A80A|

Bir uygulama NetX Duo hizmetlerine bir adres geçirdiğinde, *nxd_ip_version* alanı uygun paket işleme IÇIN doğru IP sürümünü belirtmelidir.

NetX Duo, mevcut NetX uygulamalarıyla geriye dönük olarak uyumlu olması için tüm NetX hizmetlerini destekler. NetX Duo, bir NXD_ADDRESS IPv4 adresi türünü gerçek NetX Duo hizmetine iletmeden önce bir veri türüne dönüştürür.

Aşağıdaki örnekte NetX ve NetX Duo Hizmetleri arasındaki benzerlik ve farklar gösterilmektedir.

```c
/* Make a connection to the destination IPv4 address
   192.1.168.12 through an already created TCP socket bound
   to the well known HTTP port number 80. */

global_ipv4_address.nxd_ip_version = NX_IP_VERSION_V4;
global_ipv4_address.nxd_ip_address.v4 = 0xC001A80C;

nxd_tcp_client_socket_connect(&tcp_socket,
                              &global_ipv4_address,
                              port_number,
                              NX_WAIT_FOREVER);
```

Eşdeğer NetX API 'SI aşağıda verilmiştir:

```c
ULONG         server_ip = 0xC001A80C;
NX_TCP_SOCKET tcp_socket;
UINT          port_number = 80;

nx_tcp_client_socket_connect(&tcp_socket,
                             server_ip,
                             port_number,
                             NX_WAIT_FOREVER); 
```

> [!IMPORTANT]
> *Uygulama geliştiricilerinin bu API 'lerin NXD sürümünü kullanması önerilir*.

### <a name="ipv6-default-routers"></a>IPv6 varsayılan yönlendiricileri    
IPv6, paketleri kapalı bağlantı hedeflerine iletmek için varsayılan bir yönlendirici kullanır. NetX Duo hizmeti ***nxd_ipv6_default_router_add***, bir uygulamanın varsayılan yönlendirici tablosuna bir IPv6 yönlendirici eklemesini sağlar. NetX Duo tarafından sunulan daha fazla varsayılan yönlendirici hizmeti için Bölüm 4 "hizmetlerin açıklaması" bölümüne bakın.  

IPv6 paketlerini iletirken, NetX Duo ilk olarak paket hedefinin bağlantı olup olmadığını denetler. Aksi takdirde NetX Duo, bağlantı dışı paketi iletmek için geçerli bir yönlendirici için varsayılan yönlendirme tablosunu denetler.  

Bir yönlendiriciyi IPv6 varsayılan yönlendirici tablosundan kaldırmak için, uygulama ***nxd_ipv6_default_router_delete** _ hizmetini kullanır. IPv6 varsayılan yönlendirici tablosunun girişlerini almak için, _ *_nxd_ipv6_default_router_entry_get_* * hizmetini kullanın.

### <a name="ipv6-header"></a>IPv6 üstbilgisi    
IPv6 üst bilgisi, IPv4 başlığından değiştirildi. Bir paket ayrılırken, çağıran uygulama protokolünü (örn. UDP, TCP), bayt cinsinden arabellek boyutunu ve atlama sınırını belirtir.   

Şekil 9 ' da, IPv6 üstbilgisinin biçimi gösterilir ve tablo, üst bilgi bileşenlerini listeler.

![IPv6 üst bilgi biçiminin diyagramı.](./media/user-guide/image18.png)

**ŞEKIL 9. IPv6 üst bilgi biçimi**

|IP üstbilgisi | Amaç |
|---|---|
|Sürüm |IP sürümü için 4 bit alan. IPv6 ağlarında, bu alandaki değer 6 olmalıdır; IPv4 ağları için 4 olması gerekir.|
|Trafik Sınıfı |trafik sınıfı bilgilerini depolayan 8 bit alan. Bu alan NetX Duo tarafından kullanılmaz.|
|Akış etiketi |bir paketin ilişkilendirildiği akışı benzersiz bir şekilde tanımlamak için 20 bit alan. Sıfır değeri, paketin belirli bir akışa ait olmadığını gösterir. Bu alan, IPv4 içindeki *TOS* alanının yerini alır.|
|Yük uzunluğu |IPv6 temel üst bilgisini izleyen IPv6 paketinin baytdaki veri miktarını belirten 16 bit alan. Bu, tüm kapsüllenmiş protokol üstbilgilerini ve verileri içerir.|
|Sonraki üst bilgi | IPv6 temel üst bilgisini izleyen uzantı üstbilgisinin türünü gösteren 8 bit alan. Bu alan, IPv4 içindeki *protokol* alanını değiştirir.|
|Atlama sınırı |paketin geçmesine izin verilen yönlendirici sayısını sınırlayan 8 bitlik alan. Bu alan IPv4 içindeki *TTL* alanını değiştirir.|
|Kaynak adres |Gönderenin IPv6 adresini depolayan 128 bitlik alan.|
|Hedef adres |Hedefin IPv6 adresini hedefleyen 128 bitlik alan.|

### <a name="enabling-ipv6-in-netx-duo"></a>NetX Duo 'da IPv6 'Yı etkinleştirme    
Varsayılan olarak IPv6, NetX Duo içinde etkindir. _Nx_user. h * içindeki yapılandırılabilir "**NX_DISABLE_IPV6** _ seçeneği tanımlı değilse, NETX Duo 'da IPv6 Hizmetleri etkinleştirilir. ***NX_DISABLE_IPV6*** tanımlanmışsa NETX Duo yalnızca IPv4 hizmetleri sunar ve IPv6 ile ilgili tüm modüller ve hizmetler NETX Duo kitaplığında yerleşik değildir.

Aşağıdaki hizmet uygulamaların cihaz IPv6 adresini yapılandırması için verilmiştir: ***nxd_ipv6_address_set***

Cihazın IPv6 adreslerini el ile ayarlamaya ek olarak, sistem durum bilgisi Içermeyen adres otomatik yapılandırması da kullanabilir. Bu seçeneği kullanmak için, uygulamanın, cihazda IPv6 hizmetlerini başlatması için ***nxd_ipv6_enable** _ çağrısı gerekir. Ayrıca, NetX Duo 'un yönlendirici bağlantısı, komşu bulma ve yinelenen adres algılama gibi hizmetleri gerçekleştirmesini sağlayan _*_nxd_icmp_enable_*_ çağırarak ICMPv6 Hizmetleri başlatılmalıdır. _*_Nx_icmp_enable_*_ yalnızca IPv4 HIZMETLERI için ICMP başlayacağını unutmayın. _*_nxd_icmp_enable_*_ hem IPv4 hem de ıPV6 için ICMP hizmetlerini başlatır. Sistemde ICMPv6 Hizmetleri gerekmiyorsa _ *_nx_icmp_enable_**, ICMPv6 modülünün sisteme bağlı olmaması için kullanılabilir.

Aşağıdaki örnek, tipik bir NetX Duo IPv6 başlatma yordamını göstermektedir.

```c
/* Assume ip_0 has been created and IPv4 services (such as ARP,
   ICMP, have been enabled. */
#define SECONDARY_INTERFACE 1

/* Enable IPv6 */
status = nxd_ipv6_enable(&ip_0);

if(status != NX_SUCCESS)
{
    /* nxd_ipv6_enable failed. */
}

/* Enable ICMPv6 */
status = nxd_icmp_enable(&ip_0);
if(status != NX_SUCCESS)
{
    /* nxd_icmp_enable failed. */
}

/* Configure the link local address on the primary interface. */
status = nxd_ipv6_address_set(&ip_0, 0, NX_NULL, 10, NX_NULL);

/* Configure ip_0 primary interface global address. */
ip_address.nxd_ip_version = NX_IP_VERSION_V6
ip_address.nxd_ip_address.v6[0] = 0x20010db8;
ip_address.nxd_ip_address.v6[1] = 0x0000f101;
ip_address.nxd_ip_address.v6[2] = 0;
ip_address.nxd_ip_address.v6[3] = 0x202;

/* Configure global address of the primary interface. */
status = nxd_ipv6_address_set(&ip_0, SECONDARY_INTERFACE,
                              &ip_address, 64, NX_NULL);
```                              

Üst katman protokolleri (TCP ve UDP gibi), IPv6 başlatılmadan önce veya sonra etkinleştirilebilir.

> [!IMPORTANT]  
> *IPv6 Hizmetleri yalnızca IP iş parçacığı başlatıldıktan ve cihaz etkinleştirildikten sonra kullanılabilir.*

Arabirim etkinleştirildikten sonra (yani, arabirim cihaz sürücüsü veri göndermeye ve almaya hazırsa ve geçerli bir bağlantı yerel adresi edinildikten sonra), cihaz genel IPv6 adreslerini şu yöntemlerden biriyle alabilir:

- Durum bilgisiz adres otomatik yapılandırması;  
- El ile IPv6 adresi yapılandırması;  
- DHCPv6 aracılığıyla adres yapılandırması (isteğe bağlı DHCPv6 paketiyle)

İlk iki yöntem aşağıda açıklanmıştır. 3. Yöntem (DHCPv6), DHCP paketinde açıklanmıştır.

### <a name="stateless-address-autoconfiguration-using-router-solicitation"></a>Yönlendirici bağlantısı kullanılarak durum bilgisiz adres otomatik yapılandırması      
NetX Duo cihazları, ön ek bilgileri sağlayan bir yönlendiriciyle IPv6 ağına bağlanıldığında arabirimlerini otomatik olarak yapılandırabilir. Durum bilgisi olmayan adres otomatik yapılandırması gerektiren cihazlar Yönlendirici isteme (RS) iletileri gönderir. Ağdaki yönlendiriciler, istenen yönlendirici tanıtımı (RA) iletileriyle yanıt verir. RA iletileri bir bağlantıyla ilişkili ağ adreslerini tanımlayan önekleri tanıtır. Cihazlar daha sonra cihazın eklendiği ağ için benzersiz bir tanımlayıcı oluşturur. Adres, öneki ve benzersiz tanımlayıcısını birleştirerek oluşturulur. RA iletilerinin alınması bu şekilde ana bilgisayarlar kendi IP adreslerini oluşturur. Yönlendiriciler, düzenli olarak istenmeyen RA iletileri de gönderebilir. 

> [!WARNING]
> *NETX Duo, bir uygulamanın çalışma zamanında durum bilgisiz adres otomatik yapılandırmasını etkinleştirmesine veya devre dışı bırakmasına izin verir Bu özelliği etkinleştirmek için NetX Duo kitaplığı tanımlı **NX_IPV6_STATELESS_AUTOCONFIG_CONTROL** ile derlenmelidir. Bu özellik etkinleştirildikten sonra, uygulamalar, IPv6 durum bilgisiz adresi otomatik yapılandırması 'nı etkinleştirmek veya devre dışı bırakmak için **nxd_ipv6_stateless_address_autoconfigure_enable** ve **nxd_ipv6_stateless_address_autocofigure_disable** kullanabilir*.

### <a name="manual-ipv6-address-configuration"></a>El ile IPv6 adres yapılandırması     
Belirli bir IPv6 adresi gerekliyse, uygulama bir IPv6 adresini el ile yapılandırmak için ***nxd_ipv6_address_set*** kullanabilir. Ağ arabirimi birden çok IPv6 adresine sahip olabilir. Ancak, bir sistemdeki toplam IPv6 adresi sayısının durum bilgisiz adres otomatik yapılandırması aracılığıyla elde edilen veya el Ile yapılandırma aracılığıyla ***NX_MAX_IPV6_ADDRESSES*** aşılamadığını aklınızda bulundurun.

Aşağıdaki örnek, ip_0 içinde birincil arabirimde (cihaz 0) genel bir adresin el ile nasıl yapılandırılacağını göstermektedir:

```c
NXD_ADDRESS global_address;
global_address.nxd_ip_version = NX_IP_VERSION_V6;
global_address.nxd_ip_address.v6[0] = 0x20010000;
global_address.nxd_ip_address.v6[1] = 0x00000000;
global_address.nxd_ip_address.v6[2] = 0x00000000;
global_address.nxd_ip_address.v6[3] = 0x0000ABCD;
```

Daha sonra ana bilgisayar, bu adresi genel IP adresi olarak atamak için aşağıdaki NetX Duo hizmetini çağırır:

```c
status = nxd_ipv6_address_set(&ip_0, 0,  
                              &global_address, 64
                              NX_NULL);
```

### <a name="duplicate-address-detection-dad"></a>Yinelenen adres algılama (BABACıĞıM)    
Bir sistem, IPv6 adresini yapılandırdıktan sonra, adres *belirsiz* olarak işaretlenir. RFC 4862 ' de açıklanan yinelenen adres algılama (BABACıĞıM) etkinleştirilirse, NetX Duo, bu belirsiz adresle hedef olarak komşu bağlantısı (NS) iletilerini otomatik olarak gönderir. Ağ üzerinde hiçbir ana bilgisayar belirli bir süre içinde bu NS iletilerine yanıt vermezse, adresin yerel bağlantı üzerinde benzersiz olduğu varsayılır ve durumu GEÇERLI duruma ayarlanır. Bu noktada, uygulamanın bu IP adresini iletişim için kullanmaya başlayabiliriz.  

Baba işlevselliği, ICMPv6 modülünün bir parçasıdır. Bu nedenle, yeni yapılandırılmış bir adresin BABACıĞıM işlem üzerinden gidebilmesi için uygulamanın ICMPv6 hizmetlerini etkinleştirmesi gerekir. Alternatif olarak, baba işlemi NetX Duo kitaplık derleme ortamında ***NX_DISABLE_IPV6_DAD** _ seçeneği tanımlanarak kapatılmış olabilir ( _*_nx_user. h_*_ olarak tanımlanır). BABACıĞıM işlemi sırasında, _*_NX_IPV6_DAD_TRANSMITS_*_ parametresi NETX Duo tarafından gönderilen NS iletilerinin sayısını, adresin benzersiz olduğunu belirleyen bir yanıt almadan belirler. Varsayılan olarak, RFC 4862, _ *_NX_IPV6_DAD_TRANSMITS_** 3 ' te ayarlanır. Bu sembolün sıfıra ayarlanması, BABACıĞıM 'ı devre dışı bırakır.

Uygulama bir IPv6 adresi atarken ICMPv6 veya BABACıĞıM etkinleştirilmemişse, BABACıĞıM gerçekleştirilmez ve NetX Duo, IPv6 adresinin durumunu hemen GEÇERLI olarak ayarlar.

NetX Duo, bağlantısı yerel ve/veya genel adresi geçerli olana kadar IPv6 ağı üzerinde iletişim kuramıyor. Geçerli bir adres alındıktan sonra NetX Duo, yapılandırılmış IPv6 adresinden veya etkin bir çok noktaya yayın adresinden birine karşı gelen bir paketin hedef adresini eşleştirmeye çalışır. Eşleşme bulunmazsa paket bırakılır. 

> [!WARNING]  
> * BABACıĞıM işlemi sırasında, aktarılacak baba paketleri sayısı ***NX_IPV6_DAD_TRANSMITS** tarafından tanımlanmıştır _, varsayılan olarak 3 ' e ayarlanır ve varsayılan olarak her bir baba iletisi gönderilirken ikinci bir gecikme vardır. Bu nedenle, BABACıĞıM özellikli bir sistemde, bir IPv6 adresi atandıktan sonra (ve bunun yinelenen bir adres olmadığı varsayılarak), IP adresi GEÇERLI bir durumda ve iletişim için hazır olmak üzere yaklaşık 3 saniyelik gecikme vardır._

Uygulamalar, sistemdeki IPv6 adresleri değiştirildiğinde bildirim almak isteyebilir. IPv6 adres değişikliği bildirim özelliğini etkinleştirmek için, NetX Duo kitaplığı tanımlı **NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY** sembol ile oluşturulmalıdır. Özellik etkinleştirildikten sonra, uygulamalar **_nxd_ipv6_address_change_notify_** hizmetini kullanarak geri çağırma işlevini yükleyebiliriz.

Bir IPv6 adresi değiştirildikten veya geçersiz olduktan sonra, Kullanıcı tarafından sağlanan geri çağırma işlevi aşağıdaki bilgilerle çağrılır:

| İşlev  | Açıklama  |
|---|---|
|ip_ptr |IP örneğine yönelik işaretçi|
|interface_index |Bu IPv6 adresinin ilişkilendirildiği ağ arabiriminin dizini
|ipv6_addr_index |IPv6 adresi tablosunun dizini|
|ipv6_address |Dört ULONG tamsayının dizisi biçiminde IPv6 adresine yönelik işaretçi. Pv6 adresleri, ana bilgisayar bayt düzeninde sunulur.|

### <a name="ipv6-multicast-support-in-netx-duo"></a>NetX Duo 'Da IPv6 çok noktaya yayın desteği      
Çok noktaya yayın adresleri Internet 'teki bir dinamik konaklar grubunu belirtir. Çok noktaya yayın grubunun üyeleri her istediklerinde katılabilir ve bırakabilir. NetX Duo, yinelenen adres algılama, komşu bulma ve IP çok noktaya yayın yeteneği gerektiren yönlendirici bulma dahil olmak üzere çeşitli ICMPv6 protokolleri uygular. Bu nedenle NetX Duo, temel alınan aygıt sürücüsünün çok noktaya yayın işlemlerini desteklemesini bekler.

NetX Duo bir çok noktaya yayın grubuna (örneğin, tüm düğüm çok noktaya yayın adresi ve *istek-düğüm* çok noktaya yayın adresi) katılması veya ayrılması gerektiğinde, bir çok noktaya yayın MAC adresine katılması veya bu adresi bırakmak için aygıt sürücüsüne bir sürücü komutu yayınlar. Çok noktaya yayın adresine katılma için sürücü komutu ***NX_LINK_MULTICAST_JOIN** _. NetX Duo, çok noktaya yayın adresini bırakmak için _ *_NX_LINK_MULTICAST_LEAVE_* * sürücü komutunu yayınlar. ICMPv6 protokollerinin düzgün çalışması için aygıt sürücüsünün bu iki komutu uygulaması gerekir.

Uygulamalar, ***nxd_ipv6_multicast_interface_join *** hizmetini kullanarak bir IPv6 çok noktaya yayın grubuna katılabilir. Bu hizmet, çok noktaya yayın adresini IP yığınına kaydeder ve ardından IPv6 çok noktaya yayın adresinin belirtilen cihaz sürücüsüne bildirir. Bir çok noktaya yayın grubunu bırakmak için, uygulamalar hizmeti ***nxd_ipv6_multicast_interface_leave kullanır.***

### <a name="neighbor-discovery-nd"></a>Komşu Bulma (ND)    
Komşu bulma, IPv6 ağlarındaki fiziksel adresleri IPv6 adresleriyle (genel adres veya bağlantı-yerel adres) eşlemek için IPv6 ağlarında bir protokoldür. Bu eşleme, komşu bulma önbelleğinde (ND Cache) tutulur. ND işlemi, ARP işleminin IPv4 olarak eşdeğeridir ve ND önbelleği ARP tablosuna benzerdir. Bir IPv6 düğümü, komşu bulma (ND) protokolünü kullanarak komşunuzun MAC adresini elde edebilir. Tüm düğüm talep düğümü çok noktaya yayın adresine bir komşu bağlantısı (NS) iletisi gönderir ve karşılık gelen bir komşu tanıtım tanıtımı (NA) iletisini bekler. Bu işlem aracılığıyla elde edilen MAC adresi ND önbelleğinde depolanır.

Her IP örneğinin bir ND önbelleği vardır. ND önbelleği, bir giriş dizisi olarak tutulur. Dizinin boyutu, _ *_nx_user. h_* * içinde ***NX_IPV6_NEIGHBOR_CACHE_SIZE** _ seçeneği ayarlanarak derleme zamanında tanımlanır. Bir IP örneğine bağlı olan tüm arabirimlerin aynı ND önbelleğini paylaştığından emin olmanız gerektiğini unutmayın.

NetX Duo başlatıldığında ND önbelleğinin tamamı boştur. Sistem çalışırken NetX Duo, her ND protokolüne göre giriş ekleme ve silme, ND önbelleğini otomatik olarak güncelleştirir. Ancak, bir uygulama aşağıdaki NetX Duo hizmetlerini kullanarak önbellek girişlerini el ile ekleyerek ve silerek ND önbelleğini güncelleştirebilir:

- ***nxd_nd_cache_entry_delete***  
- ***nxd_nd_cache_entry_set***   
- ***nxd_nd_cache_invalidate***

IPv6 paketlerini gönderirken ve alırken, NetX Duo, ND Cache tablosunu otomatik olarak güncelleştirir.

## <a name="internet-control-message-protocol-in-ipv6-icmpv6"></a>IPv6 'da Internet Denetim Iletisi Protokolü (Icmpv6)  

IPv6 'daki ICMPv6 'nın rolü, IPv6 adresi eşlemesini ve Yönlendirici bulmayı desteklemek için büyük ölçüde genişletilmiştir. Ayrıca NetX Duo ICMPv6, yankı isteği ve yanıtı, ICMPv6 hata raporlarını ve ICMPv6 yeniden yönlendirme iletilerini destekler.

### <a name="icmpv6-enable"></a>ICMPv6 etkin    
ICMPv6 iletilerinin NetX Duo tarafından işlenebilmesi için, uygulamanın daha önce açıklandığı gibi ICMPv6 işlemesini etkinleştirmek üzere ***nxd_icmp_enable*** hizmetini çağırması gerekir. 

### <a name="icmpv6-messages"></a>ICMPv6 Iletileri     
ICMPv6 üst bilgi yapısı, Icmpv4 üstbilgi yapısına benzer. Aşağıda gösterildiği gibi, temel ICMPv6 üstbilgisi üç alanı, tür, kod ve sağlama toplamı ile ICMPv6 seçenek verilerinin değişken uzunluğunu içerir. 

![Temel bir ICMPv6 üstbilgisinin diyagramı.](./media/user-guide/image19.png)

**ŞEKIL 10. Temel ICMPv6 üstbilgisi**

|Alan |Boyut (bayt) |Açıklama |
|-----|-----|-----|
|     | 1   |ICMPv6 ileti türünü tanımlar; |
|     |     |1 hedefe ulaşılamıyor |
|     |     |2 paket çok büyük |
|     |     |3 süre aşıldı |
|     |     |4 parametre sorunu |
|     |     |128 yankı Isteği |
|     |     |129 Echo yanıtı |
|     |     |133 yönlendirici Isteği |
|     |     |134 yönlendirici tanıtımı |
|     |     |135 komşu Isteği |
|     |     |136 komşu tanıtımı |
|     |     |137 yönlendirme Iletisi |
|Kod | 1   |ICMPv6 ileti türünü daha fazla nitelendirir. Genellikle hata iletileriyle birlikte kullanılır. Kullanılmıyorsa, sıfır olarak ayarlanır. Yankı isteği/yanıt ve NS iletileri bunu kullanmaz.|
|Sağlama | 2 |ıCMP üst bilgisi için 16 bit sağlama toplamı alanı. Bu, ICMPv6 üst bilgisi de dahil olmak üzere tüm ICMPv6 iletisinin 16 bitlik bir tamamlığıdır. Ayrıca IPv6 kaynak adresinin, hedef adresinin ve paket yükü uzunluğunun sözde üst bilgisini içerir. |

Örnek bir komşu bağlantısı üst bilgisi aşağıda gösterilmiştir.

![Örnek bir komşu bağlantısı üst bilgisi diyagramı.](./media/user-guide/image20.jpg)

**ŞEKIL 11. Bir komşu ISTEME Iletisi için ICMPv6 üstbilgisi**

|Alan |Boyut (bayt) |Açıklama |
|-----|-----|-----|
|Tür | 1   |Komşu isteme iletileri için ICMPv6 ileti türünü tanımlar. Değer 135 ' dir. |
|Kod | 1   |Kullanılmadı. 0 olarak ayarlayın. |
|Sağlama | 2  |ICMPv6 üst bilgisi için 16 bit sağlama toplamı alanı. |
|Ayrılmıştır | 4  |4 ayrılmış bayt 0 olarak ayarlanır. |
|Hedef adres | 16  |İsteme hedefinin IPv6 adresi. IPv6 adres çözümlemesi için, bağlantı katmanı adresi çözülmesi gereken cihazın asıl tek noktaya yayın IP adresidir. |
|Seçenekler | Değişken |Komşu Bulma Protokolü tarafından belirtilen isteğe bağlı bilgiler. |

### <a name="icmpv6-ping-request"></a>ICMPv6 ping Isteği
NetX Duo uygulamalarında, parametrelerde belirtilen hedef IP adresine göre IPv6 veya IPv4 ping istekleri vermek için ***nxd_icmp_ping*** kullanın.  

### <a name="icmpv6-ping-response"></a>ICMPv6 ping yanıtı
Bir ICMPv6 ping yanıtı, bir dış ICMPv6 ping isteğine yanıt olarak ICMPv6 bileşeni tarafından dahili olarak oluşturulan başka bir Icmpv6 iletisi türüdür. Bildirim ek olarak, ICMPv6 ping yanıtı da ICMPv6 ping isteğinde sağlanan kullanıcı verilerinin bir kopyasını içerir.  

### <a name="thread-suspension"></a>İş parçacığı askıya alma
Uygulama iş parçacıkları başka bir ağ üyesine ping yapılmaya çalışılırken askıya alabilir. Ping yanıtı alındıktan sonra, ping yanıtı iletisi askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı sürdürülür. Tüm NetX Duo hizmetleri gibi, bir ping isteğini askıya alma isteğe bağlı bir zaman aşımı içerir.  

### <a name="other-icmpv6-messages"></a>Diğer ICMPv6 Iletileri
Aşağıdaki özellikler için ICMPv6 iletileri gereklidir:  

- Komşu bulma  
- Durum bilgisiz adres otomatik yapılandırması 
- Yönlendirici bulma 
- Komşu ulaşılamama algılaması  

### <a name="neighbor-unreachability-router-and-prefix-discovery"></a>Komşunlamama, yönlendirici ve ön ek bulma    
Komşunlamama algılama, yönlendirici bulma ve ön ek bulma, komşu bulma protokolünü temel alır ve aşağıda açıklanmıştır. 

***Komşu ulaşılamama algılaması:*** Bir IPv6 aygıtı, bir paket göndermek istediğinde hedef bağlantı katmanı adresi için komşu bulma (ND) önbelleğini arar. Bazen ' sonraki atlama ' olarak adlandırılan acil hedef, aynı bağlantı üzerindeki gerçek hedef olabilir veya hedef bağlantı kapalıysa bir yönlendirici olabilir. ND önbellek girdisi, bir komşunun ulaşılabilirlik üzerindeki durumu içerir.

ERIŞILEBILIR durum, komşunun erişilebilir kabul edileceğini belirtir. Son zamanlarda, komşuyla gönderilen paketlerin alındığını belirten bir komşu alındı. NetX Duo 'da yapılan onay, NetX Duo cihaz tarafından gönderilen bir NS iletisine yanıt olarak komşudan bir NA ileti alma biçimini alır. Ayrıca, uygulama NetX Duo hizmeti ***nxd_nd_cache_entry_set*** bir önbellek kaydını el ile girmesi Için NETX Duo, komşu durumunun durumunu erişilebilir olarak değiştirir.

***Yönlendirici bulma:*** IPv6 cihazı, bağlantı hedefleri için tasarlanan tüm paketleri iletmek için bir yönlendirici kullanır. Ayrıca, kendi genel IPv6 adreslerini yapılandırmak için yönlendirici tanıtımı (RA) iletileri gibi yönlendirici tarafından gönderilen bilgileri de kullanabilir.

Ağdaki bir cihaz, tüm yönlendirici çok noktaya yayın adresine (FF01:: 2) bir yönlendirici bağlantısı (RS) iletisi göndererek yönlendirici bulma işlemini başlatabilir. Ya da yönlendiricilerden düzenli bir RA için tüm düğüm çok noktaya yayın adresini (FF:: 1) bekleyebilir.

RA iletisi, bu ağ için bir IPv6 adresi yapılandırmaya yönelik önek bilgilerini içerir. NetX Duo sürümünde, Yönlendirici isteme varsayılan olarak etkindir ve _ *_nx_user. h_* * içindeki yapılandırma seçeneği ***NX_DISABLE_ICMPV6_ROUTER_SOLICITATION** _ ayarlanarak devre dışı bırakılabilir. Yönlendirici ISTEME parametrelerini ayarlama hakkında daha fazla bilgi için bkz. "NetX Duo yükleme ve kullanma" bölümünde yapılandırma seçenekleri. 

***Ön ek keşfi***: bir IPv6 cihazı, bir yönlendiriciden geçmeden doğrudan erişilebilen hedef konaklara erişim sağlamak için ön ek bulmayı kullanır. Bu bilgiler, yönlendiriciden gelen RA iletilerinden IPv6 cihazında kullanılabilir hale getirilir. IPv6 cihazı ön ek bilgilerini önek tablosunda depolar. Ön ek keşfi IPv6 cihaz öneki tablosundan hedef adrese bir ön ek ile eşleşiyor. Önekte bulunan tüm bitlerin hedef adresin en önemli bitlerini eşleşiyorsa bir önek, hedef adresle eşleşir. Birden fazla önek bir adresi kapsıyorsa, en uzun ön ek seçilir.

### <a name="icmpv6-error-messages"></a>ICMPv6 hata Iletileri    
NetX Duo 'da aşağıdaki ICMPv6 hata iletileri desteklenir:  

- Hedefe ulaşılamıyor  
- Paket çok büyük  
- Süre aş  
- Parametre sorunu  

## <a name="user-datagram-protocol-udp"></a>Kullanıcı veri birimi Protokolü (UDP)

Kullanıcı veri birimi Protokolü (UDP) ağ üyeleri arasında en basit veri aktarımı biçimini sağlar (RFC 768). UDP veri paketleri en iyi çabayla bir ağ üyesinden diğerine gönderilir; Yani, paket alıcısı tarafından onay için yerleşik bir mekanizma yoktur. Ayrıca, bir UDP paketinin gönderilmesi için herhangi bir bağlantının önceden kurulması gerekmez. Bu nedenle, UDP paket iletimi oldukça etkilidir.

NETX uygulamalarını NetX Duo 'e geçirirken geliştiriciler için, NetX ve NetX Duo arasındaki UDP işlevselliğinde yalnızca birkaç temel değişiklik bulunur. Bunun nedeni IPv6 'nın öncelikle temel alınan IP katmanıyla ilgilenmesinden kaynaklanır. Tüm NetX Duo UDP Hizmetleri, IPv4 veya IPv6 bağlantısı için kullanılabilir.

### <a name="udp-header"></a>UDP üst bilgisi       
UDP, iletim sırasında uygulamanın verilerinin önüne basit bir paket üst bilgisi koyar ve alınan bir UDP paketini uygulamaya teslim etmeden önce, Alım paketinden benzer bir UDP üst bilgisini kaldırır. UDP, paket ağda olduğunda UDP üst bilgisinin önünde bir IP üstbilgisi olduğu anlamına gelen paketleri göndermek ve almak için IP protokolünü kullanır. Şekil 12 ' de UDP üstbilgisinin biçimi gösterilmektedir.

![UDP üst bilgi biçiminin diyagramı.](./media/user-guide/image21.png)

### <a name="figure-12-udp-header"></a>ŞEKIL 12. UDP üst bilgisi

> [!NOTE]
> *UDP/IP uygulamasındaki tüm üstbilgilerin **Big endian** biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

Aşağıda UDP üst bilgi biçimi açıklanmaktadır:

|Üst bilgi alanı |Amaç |
|---|---|
|**16 bit kaynak bağlantı noktası numarası** |Bu alan, UDP paketinin gönderilme bağlantı noktasını içerir. Geçerli UDP bağlantı noktaları 1 ile 0xFFFF arasındadır. |
|**16 bit hedef bağlantı noktası numarası** |Bu alan, paketin gönderildiği UDP bağlantı noktasını içerir. Geçerli UDP bağlantı noktaları 1 ile 0xFFFF arasındadır. |
|**16 bit UDP uzunluğu** |Bu alan UDP paketindeki UDP üstbilgisinin boyutu da dahil olmak üzere bayt sayısını içerir. |
|**16 bit UDP sağlama toplamı** |Bu alan, paket için UDP üstbilgisi, paket veri alanı ve sözde IP üstbilgisi dahil olmak üzere 16 bit sağlama toplamı içerir. |

### <a name="udp-enable"></a>UDP etkinleştirme   
UDP paket iletimi mümkün olmadan önce, uygulamanın öncelikle ***nx_udp_enable*** HIZMETINI çağırarak UDP 'yi etkinleştirmesi gerekir. Etkinleştirildikten sonra uygulama, UDP paketlerini göndermek ve almak için ücretsizdir.  

### <a name="udp-socket-create"></a>UDP yuvası oluşturma    
UDP yuvaları, başlatma sırasında veya çalışma zamanı sırasında uygulama iş parçacıkları tarafından oluşturulur. Hizmetin başlangıç türü, yaşam süresi ve alma sırası derinliği ***nx_udp_socket_create*** hizmeti tarafından tanımlanır. Bir uygulamadaki UDP yuvaları sayısında sınır yoktur.

### <a name="udp-checksum"></a>UDP sağlama toplamı   
IPv6 protokolü, paket verilerinde bir UDP üst bilgi sağlama toplamı hesaplaması gerektirir, ancak IPv4 protokolünde isteğe bağlıdır.  

UDP, IP sahte üstbilgisini (kaynak IP adresi, hedef IP adresi ve protokol/uzunluk IP sözcükten oluşan), UDP üstbilgisini ve UDP paket verilerini içeren bir 16 bit tamamlama toplamı belirtir. IPv4 ve IPv6 UDP paket üst bilgisi sağlama toplamı arasındaki tek fark, kaynak ve hedef IP adreslerinin, IPv6 'da 128 bit olduğu sırada IPv4 içinde 32 bitleridir. Hesaplanan UDP sağlama toplamı 0 ise, hepsi (0xFFFF) olarak depolanır. Gönderme yuvasında UDP sağlama toplamı mantığı devre dışıysa, sağlama toplamı hesaplanmadığından, UDP sağlama toplamı alanına sıfır yerleştirilir.

UDP sağlama toplamı, alıcı tarafından hesaplanan sağlama toplamıyla eşleşmezse, UDP paketi yalnızca atılır.

IPv4 ağında, UDP sağlama toplamı isteğe bağlıdır. NetX Duo, bir uygulamanın her yuva temelinde UDP sağlama toplamı hesaplamasını etkinleştirmesine veya devre dışı bırakmasına olanak sağlar. Varsayılan olarak, UDP yuva sağlama toplamı mantığı etkindir. Uygulama, ***nx_udp_socket_checksum_disable** _ hizmetini çağırarak belırlı bir UDP yuvası için sağlama mantığını devre dışı bırakabilir. Bununla birlikte IPv6 ağında, UDP sağlama toplamı zorunludur. Bu nedenle, bu hizmet _ *_nx_udp_socket_checksum_disable_**, IPv6 ağı aracılığıyla bir paket gönderilirken UDP sağlama toplamı mantığını devre dışı bırakmaz.

Belirli Ethernet denetleyicileri anında UDP sağlama toplamı üretebilir. Sistem donanım sağlama toplamı hesaplama özelliğini kullanabiliyor ise, NetX Duo kitaplığı sağlama toplamı mantığı olmadan oluşturulabilir. UDP yazılım sağlama toplamını devre dışı bırakmak için NetX Duo kitaplığı, tanımlanan şu simgelerle oluşturulmalıdır: ***NX_DISABLE_UDP_TX_CHECKSUM** _ ve _*_NX_DISABLE_UDP_RX_CHECKSUM_*_ (Bölüm iki bölümünde açıklanmıştır). Yapılandırma seçenekleri, NetX Duo 'ten gelen UDP sağlama mantığını tamamen kaldırır, _ *_nx_udp_socket_checksum_disable_** hizmetini çağırmak uygulamanın her yuva IÇIN IPv4 UDP sağlama toplamı işlemesini devre dışı bırakmasına olanak sağlar.

### <a name="udp-ports-and-binding"></a>UDP bağlantı noktaları ve bağlama      
UDP bağlantı noktası UDP protokolündeki bir mantıksal bitiş noktasıdır. NetX Duo 'un UDP bileşeninde, 1 ile 0xFFFF arasında 65.535 geçerli bağlantı noktası vardır. UDP verileri göndermek veya almak için önce uygulamanın bir UDP yuvası oluşturması ve ardından bunu istenen bir bağlantı noktasına bağlaması gerekir. Bir UDP yuvasını bir bağlantı noktasına bağladıktan sonra, uygulama o yuvaya veri alıp alabilir.

### <a name="udp-fast-pathtrade"></a>UDP hızlı yolu&trade;   
UDP hızlı yolu, &trade; NetX Duo UDP uygulamasıyla düşük bir paket ek yükü yolunun adıdır. Bir UDP paketinin gönderilmesi yalnızca birkaç işlev çağrısını gerektirir: ***nx_udp_socket_send** _, _*_nx_ip_packet_send_*_ ve ağ sürücüsüne yapılan nihai çağrı. _*_nx_udp_socket_send_*_ , mevcut NETX uygulamalarına yönelik NETX Duo sürümünde kullanılabilir ve yalnızca IPv4 paketleri için geçerlidir. Ancak tercih edilen yöntem, aşağıda açıklanan _ *_nxd_udp_socket_send_** hizmetini kullanmaktır. UDP paket alımı üzerinde, UDP paketi uygun UDP yuvası alma kuyruğuna yerleştirilir veya ağ sürücüsünün alma kesme işleminden gelen tek bir işlev çağrısında askıya alınmış bir uygulama iş parçacığına dağıtılır. UDP paketlerinin gönderilmesi ve alınması için en iyi duruma getirilmiş bu mantık, UDP hızlı yol teknolojisinin özünü önemli bir yoldur.  

### <a name="udp-packet-send"></a>UDP paketi gönderme    
IPv6 veya IPv4 ağları üzerinden UDP verileri göndermek, ***nxd_udp_socket_send** _ işlevi çağırarak kolayca gerçekleştirilir. Çağıran, NXD_ADDRESS işaretçi parametresinin _nx_ip_version * alanındaki IP sürümünü ayarlamış olmalıdır. NetX Duo, iletilen UDP paketlerinin hedef IPv4/IPv6 adresine göre en iyi kaynak adresini belirleyecek. Bu hizmet, paket verilerinin önüne bir UDP üst bilgisi koyar ve bir iç IP gönderme yordamı kullanarak ağı ağa gönderir. UDP paketlerinin gönderilmesi üzerinde hiçbir iş parçacığı askıya alınmaz çünkü tüm UDP paket aktarımları hemen işlenir. 

Çok noktaya yayın veya yayın hedefleri için, NetX Duo cihazında aralarından seçim yapabileceğiniz birden çok IP adresi varsa, uygulamanın kullanılacak kaynak IP adresini belirtmesi gerekir. Bu, Hizmetler ***nxd_udp_socket_source_send yapılabilir.***

> [!IMPORTANT]    
> *Çok noktaya yayın veya yayın paketlerini iletmek için **nx_udp_socket_send** kullanılıyorsa, Ilk etkinleştirilen arabirimin IP adresi kaynak adres olarak kullanılır*.

> [!NOTE] 
> *Bu yuva IÇIN UDP sağlama toplamı mantığı etkinleştirilmişse, sağlama iş parçacığı bağlamında, UDP veya IP veri yapılarına erişimi engellemeden, sağlama toplamı işlemi yapılır*. 

> [!WARNING]    
> *NX_PACKET yapısında bulunan UDP yük verileri uzun bir sözcük sınırında bulunmalıdır. Uygulamanın, IP, IP ve fiziksel medya üst bilgilerini yerleştirmek için, önüne işaretçisi ve NETX Duo için veri başlangıç işaretçisi arasında yeterli alan bırakması gerekir*.

### <a name="udp-packet-receive"></a>UDP paket alma    
Uygulama iş parçacıkları, ***nx_udp_socket_receive*** çağırarak belirli BIR yuvadan UDP paketleri alabilir. Yuva alma işlevi, yuvanın alma sırasındaki en eski paketi sunar. Alma kuyruğunda paket yoksa, bir paket gelene kadar çağıran iş parçacığı askıya alabilir (isteğe bağlı bir zaman aşımı ile).

UDP alma paketi işleme (genellikle ağ sürücüsünün Alım kesme işleyicisinden çağrılır), paketi UDP yuvasının alma kuyruğuna yerleştirmekten veya bir paket için bekleyen ilk askıya alınan iş parçacığına teslim etmekten sorumludur. Paket sıraya alınmışsa, alma işlemi, yuvada ilişkili en fazla alma sırası derinliğini de denetler. Bu yeni kuyruğa alınan paket sıra derinliğini aşarsa, sıradaki en eski paket atılır.

### <a name="udp-receive-notify"></a>UDP alma bildirimi   
Uygulama iş parçacığının birden fazla yuvada alınan verileri işlemesi gerekiyorsa ***nx_udp_socket_receive_notify*** işlevi kullanılmalıdır. Bu işlev, yuva için bir alma paketi geri çağırma işlevi kaydeder. Yuvada her bir paket alındığında geri çağırma işlevi yürütülür.

Geri çağırma işlevinin içerikleri, applicationspecific; Ancak büyük olasılıkla işleme iş parçacığını, ilgili yuvada artık kullanılabilir olduğunu bildirmek için mantık içerebilir.

### <a name="peer-address-and-port"></a>Eş adresi ve bağlantı noktası   
Bir UDP paketi alındığında, uygulama, hizmet ***nx_udp_packet_info_extract*** kullanarak gönderenin IP adresini ve bağlantı noktası numarasını bulabilir. Başarılı bir geri döndüğünüzde, bu hizmet gönderenin IP adresi, gönderenin bağlantı noktası numarası ve paketin alındığı yerel arabirim hakkındaki bilgileri sağlar.  

### <a name="thread-suspension"></a>İş parçacığı askıya alma   
Daha önce belirtildiği gibi, uygulama iş parçacıkları belirli bir UDP bağlantı noktasında UDP paketi alınmaya çalışılırken askıya alabilir. Bu bağlantı noktasında bir paket alındıktan sonra, bu, askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı daha sonra sürdürülür. Çok sayıda NetX Duo hizmeti için kullanılabilen bir UDP alma paketi üzerinde askıya alma sırasında isteğe bağlı bir zaman aşımı kullanılabilir.  

### <a name="udp-socket-statistics-and-errors"></a>UDP yuvası Istatistikleri ve hataları     
Etkinleştirilirse, NetX Duo UDP yuva yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP/UDP örneği için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen toplam UDP paketi sayısı  
- Gönderilen toplam UDP bayt sayısı  
- Alınan toplam UDP paketi sayısı   
- Alınan toplam UDP bayt sayısı  
- Toplam UDP geçersiz paket sayısı  
- Bırakılan toplam UDP alma paketi sayısı  
- Toplam UDP alma sağlama toplamı hatası  
- Gönderilen UDP soket paketleri  
- Gönderilen UDP yuva baytları  
- Alınan UDP soket paketleri   
- Alınan UDP yuva baytları  
- Sıraya alınan UDP yuvası paketleri  
- Bırakılan UDP yuvası alma paketleri  
- UDP yuva sağlama toplamı hataları  

Bu istatistik ve hata raporlarının tümü, tüm UDP yuvaları üzerinden UDP istatistikleri amassed için ***nx_udp_info_get** _ hizmeti ve belirtilen UDP yuvasında UDP istatistikleri için _ *_nx_udp_socket_info_get_** hizmeti ile birlikte kullanılabilir.

### <a name="udp-socket-control-block-nx_udp_socket"></a>UDP yuva denetim bloğu NX_UDP_SOCKET
Her UDP yuvasının özellikleri, ilişkili NX_UDP_SOCKET denetim bloğunda bulunur. IP veri yapısına bağlantı, gönderme ve alma yolları için ağ arabirimi, bağlantı noktası ve alma paketi kuyruğu gibi yararlı bilgiler içerir. Bu yapı ***nx_api. h*** dosyasında tanımlanmıştır.

## <a name="transmission-control-protocol-tcp"></a>İletim Denetimi Protokolü (TCP)

Iletim Denetim Protokolü (TCP) iki ağ üyesi arasında güvenilir akış veri aktarımı sağlar (RFC 793). Bir ağ üyesinden gönderilen tüm veriler, alıcı üye tarafından doğrulanır ve onaylanır. Ayrıca, iki üyenin herhangi bir veri aktarımından önce bir bağlantı oluşturmuş olması gerekir. Tüm bu sonuçlar güvenilir veri aktarımına sahiptir; Ancak, daha önce açıklanan UDP veri aktarımından daha fazla ek yük gerektirir.

Aksi belirtilmedikçe, TCP protokolü API hizmetlerinde NetX ve NetX Duo arasında hiçbir değişiklik yoktur, çünkü IPv6 birincil olarak temel alınan IP katmanıyla ilgilidir. Tüm NetX Duo TCP hizmetleri, IPv4 veya IPv6 bağlantıları için kullanılabilir.

### <a name="tcp-header"></a>TCP üst bilgisi   
İletim sırasında TCP üstbilgisi, kullanıcıdan verilerin önüne yerleştirilir. Alma sırasında TCP üstbilgisi, gelen paketten kaldırılır ve yalnızca uygulamanın kullanabildiği Kullanıcı verileri bırakılır. TCP, paket ağda olduğunda TCP üst bilgisinin önünde bir IP üstbilgisi olduğu anlamına gelen paketleri göndermek ve almak için IP protokolünü kullanır. Şekil 13, TCP üstbilgisinin biçimini gösterir.

![TCP üst bilgi biçiminin diyagramı.](./media/user-guide/image22.png)

### <a name="figure-13-tcp-header"></a>ŞEKIL 13. TCP üst bilgisi

Aşağıda TCP üst bilgi biçimi açıklanmaktadır:

|Üst bilgi &nbsp; alanı |Amaç |
|------|------|
| **16 bit kaynak bağlantı noktası numarası** | Bu alan, TCP paketinin gönderilme bağlantı noktasını içerir. Geçerli TCP bağlantı noktaları 1 ile 0xFFFF arasında değişir. |
| **16 bit hedef bağlantı noktası** | Bu alan, paketin gönderildiği TCP bağlantı noktasını içerir. Geçerli TCP bağlantı noktaları 1 ile 0xFFFF arasında değişir. |
| **32-bit sıra numarası** | Bu alan, bağlantının bu sonundan gönderilen verilerin sıra numarasını içerir. Özgün sıra, iki TCP düğümü arasındaki ilk bağlantı sırası sırasında oluşturulur. Bu noktadan her veri aktarımı, gönderilen toplam bayt sayısına göre sıra numarası artışını elde ediyor. |
| **32-bit onay numarası** | Bu alan, bağlantının bu tarafında alınan son bayta karşılık gelen sıra numarasını içerir. Bu, daha önce gönderilen verilerin bağlantının diğer ucundan başarıyla alındığını belirlemekte kullanılır. |
| **4 bit üst bilgi uzunluğu** | Bu alan, TCP üstbilgisindeki 32 bitlik sözcüklerin sayısını içerir. TCP üstbilgisinde bir seçenek yoksa, bu alan 5 ' tir. |
| **6 bit kod bitleri** |Bu alan, bağlantıyla ilişkili çeşitli denetim bilgilerini belirtmek için kullanılan altı farklı kod bitini içerir. Denetim bitleri şu şekilde tanımlanır: <br \> -URG (21): acil veri ön eki<br \> -ACK (20): onay numarası geçerli<br- \> PSH (19): bu verileri hemen işle<br- \> RST (18): bağlantıyı sıfırlayın<br- \> SYN (17): işlem numaralarını eşitler (bağlantı kurmak için kullanılır) <br \> -FIN (16): gönderici iletim ile tamamlandı (bağlantıyı kapatmak için kullanılır) |
|**16 bit pencere** |Bu alan akış denetimi için kullanılır. Bu, yuvanın Şu anda alabileceği bayt miktarını içerir. Bu temel olarak Flow denetimi için kullanılır. Gönderen verilerin alıcının tanıtılan penceresine sığdırmasını sağlamaktan gönderici sorumludur. |
|**16 bit TCP sağlama toplamı** |Bu alan, paket için TCP üst bilgisi, paket veri alanı ve sözde IP üstbilgisi dahil olmak üzere 16 bit sağlama toplamı içerir. |
|**16 bit acil işaretçi** |Bu alan, acil verilerin son baytının pozitif sapmasını içerir. Bu alan yalnızca üst bilgide URG kod biti ayarlandıysa geçerlidir. |

> [!NOTE]  
> *TCP/IP uygulamasındaki tüm üstbilgilerin **Big endian** biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur*.

### <a name="tcp-enable"></a>TCP etkinleştirme       
TCP bağlantıları ve paket aktarımları mümkün olmadan önce, uygulamanın öncelikle ***nx_tcp_enable*** HIZMETINI çağırarak TCP 'yi etkinleştirmesi gerekir. Etkinleştirildikten sonra, uygulama tüm TCP hizmetlerine erişmeye ücretsizdir.  

### <a name="tcp-socket-create"></a>TCP yuvası oluşturma    
TCP yuvaları, başlatma sırasında veya çalışma zamanı sırasında uygulama iş parçacıkları tarafından oluşturulur. Hizmetin başlangıç türü, yaşam süresi ve pencere boyutu ***nx_tcp_socket_create*** hizmeti tarafından tanımlanır. Bir uygulamadaki TCP yuvaları sayısında sınır yoktur.  

### <a name="tcp-checksum"></a>TCP sağlama toplamı     
TCP, IP sahte üstbilgisini (kaynak IP adresi, hedef IP adresi ve protokol/uzunluk IP sözcükten oluşan), TCP üstbilgisini ve TCP paketi verilerini içeren bir 16 bit tamamlama toplamı belirtir. IPv4 ve IPv6 TCP paket üst bilgisi sağlama toplamı arasındaki tek fark, kaynak ve hedef IP adreslerinin IPv6 'da IPv4 ve 128 bit içinde 32 bitleridir. 

Bazı ağ denetleyicileri donanımda TCP sağlama toplamı hesaplaması ve doğrulaması gerçekleştirebilir. Uygulamalar, bu tür sistemler için, çalışma zamanı yükünü azaltmak için mümkün olduğunca donanım sağlama mantığını kullanmak isteyebilir. Uygulamalar, ***NX_DISABLE_TCP_TX_CHECKSUM** _ ve _ *_NX_DISABLE_TCP_RX_CHECKSUM_* * tanımlayarak derleme zamanında NETX Duo kitaplığından tamamen TCP sağlama toplamı hesaplama mantığını devre dışı bırakabilir. Bu şekilde, TCP sağlama toplamı kodu ' de derlenmez. Ancak, isteğe bağlı NetX Duo IPSec paketi yüklüyse ve TCP bağlantısının güvenli bir kanaldan geçiş yapması gerekebilmelidir, bunlardan biri dikkatli olmalıdır. Bu durumda, TCP bağlantısına ait olan paketlerdeki veriler zaten şifrelenmiştir ve ağ sürücüsünde bulunan donanım TCP sağlama toplamı modülleri, şifrelenmiş TCP yükünden doğru sağlama toplamı değeri üretemiyor.

Bu sorunu gidermek için, uygulama TCP sağlama toplamı mantığını kitaplıkta tutar ve arabirim yetenek özelliğini kullanır. Arabirim özelliği özelliği etkinken, TCP modülü, sürücü sağlama toplamı değerini de hesaplabiliyorsa, TCP sağlama toplamını nasıl doğru şekilde işleyeceğinizi bilir:

1) TCP paketi IPSec işlemine bağlı değilse, ağ arabirimi donanımı sağlama toplamını hesaplamayabilir. Bu nedenle TCP modülü sağlama toplamını hesaplama girişiminde bulunmaz;

2) IPSec paketi yüklüyse ve TCP paketi IPSec işlemine tabidir, TCP modülü, paketi IPSec katmanına göndermeden önce yazılımda sağlama toplamını hesaplar.

### <a name="tcp-port"></a>TCP Bağlantı Noktası     
TCP bağlantı noktası, TCP protokolünde bir mantıksal bağlantı noktasıdır. NetX Duo TCP bileşeninde, 1 ile 0xFFFF arasında 65.535 geçerli bağlantı noktası vardır. Bir bağlantı noktasındaki verilerin diğer hedef bağlantı noktalarına gönderilebileceği UDP 'nin aksine, bir TCP bağlantı noktasının başka bir belirli TCP bağlantı noktasına bağlı olması ve yalnızca bu bağlantı kurulduğu zaman, bağlantıyı oluşturan iki bağlantı noktası arasında olması gerekir.

> [!IMPORTANT]
> *TCP bağlantı noktaları UDP bağlantı noktalarından tamamen ayrıdır; örn. UDP bağlantı noktası numarası 1, TCP bağlantı noktası numarası 1 ile hiçbir ilişkiye sahip değildir*.

### <a name="client-server-model"></a>Client-Server modeli     
Veri aktarımı için TCP kullanmak üzere iki TCP yuvası arasında bir bağlantı kurulması gerekir. Bağlantının kurulması, istemci-sunucu düzeyinde yapılır. Bağlantının istemci tarafı bağlantıyı başlatan tarafdayken, sunucu tarafı herhangi bir işlem yapılmadan önce istemci bağlantı isteklerini bekler.

> [!IMPORTANT]
> *Çok kaynaklı cihazlarda, NetX Duo bağlantı için kullanılacak kaynak adresini ve bağlantının hedef IP adresine göre sonraki atlama adresini otomatik olarak belirler. TCP, tek noktaya yayın (örneğin, yayın olmayan) hedef adreslerine paket göndermeye sınırlı olduğundan, NetX Duo kaynak IPv6 adresini seçmek için bir "ipucu" gerektirmez*.

### <a name="tcp-socket-state-machine"></a>TCP yuva durumu makinesi      
İki TCP yuvası (bir istemci ve bir sunucu) arasındaki bağlantı karmaşıktır ve bir durum makinesi halinde yönetilir. Her TCP yuvası kapalı bir durumda başlar. Bağlantı olayları aracılığıyla her bir yuvanın durum makinesi, TCP 'deki veri aktarımının toplu olarak gerçekleştiği, kurulan duruma geçirilir. Bağlantının bir tarafı artık veri göndermek istediğinde, bağlantısını keser. Diğer tarafın bağlantısı kesildiğinde, TCP yuvası kapalı duruma geri döner. Bu işlem, bir TCP istemcisi ve sunucusu bir bağlantı kurup her kapatışınızda yinelenir. Şekil 14 ' te TCP durum makinesinin çeşitli durumları gösterilmektedir.

### <a name="tcp-client-connection"></a>TCP Istemci bağlantısı       
Daha önce belirtildiği gibi, TCP bağlantısının istemci tarafı bir TCP sunucusuna bağlantı isteği başlatır. Bir bağlantı isteğinin yapılabilmesi için, istemci IP örneğinde TCP 'nin etkinleştirilmesi gerekir. Ayrıca, istemci TCP yuvasının daha sonra ***nx_tcp_socket_create** _ hizmeti ile oluşturulması ve _ *_nx_tcp_client_socket_bind_** hizmeti aracılığıyla bir bağlantı noktasına bağlanması gerekir.

İstemci yuvası bağlandıktan sonra, bir TCP sunucusuyla bağlantı kurmak için ***nxd_tcp_client_socket_connect*** hizmeti kullanılır. Bir bağlantı denemesi başlatmak için yuvanın kapalı durumda olması gerektiğini aklınızda olun. Bağlantı kurma, NetX Duo ile başlar ve sonra bağlantı isteğinin kabul edildiğini belirten bir SYN ACK paketini sunucudan geri bekler. SYN ACK alındıktan sonra NetX Duo bir ACK paketiyle yanıt verir ve istemci yuvasını belırlenen duruma yükseltir.

![TCP durum makinesinin durumlarının diyagramı.](./media/user-guide/image24.png)   

**ŞEKIL 14. TCP durum makinesinin durumları**


> [!WARNING]
> *Uygulamalar IPv4 ve ıPV6 TCP bağlantıları için **nxd_tcp_client_socket_connect** kullanmalıdır. Uygulamalar IPv4 TCP bağlantıları için **nx_tcp_client_socket_connect** kullanmaya devam edebilir, ancak **nx_tcp_client_socket_connect** sonunda kullanım dışı olacağı için geliştiricilerin **nxd_tcp_client_socket_connect** kullanmaları önerilir*.

*Benzer şekilde, **nxd_tcp_socket_peer_info_get** ıPV4 veya IPv6 TCP bağlantılarıyla da çalışır. Ancak, **nx_tcp_socket_peer_info_get** eski uygulamalar için hala kullanılabilir. Geliştiricilerin öne geçmek **nxd_tcp_socket_peer_info_get** kullanmaları önerilir*.

### <a name="tcp-client-disconnection"></a>TCP Istemcisi bağlantısı kesilmesi    
Bağlantıyı kapatmak ***nx_tcp_socket_disconnect*** çağırarak gerçekleştirilir. Askıya alma belirtilmemişse, istemci yuvası sunucu yuvasına bir RST paketi gönderir ve yuvayı kapalı duruma koyar. Aksi takdirde, askıya alma isteniyorsa, tam TCP bağlantı kesme protokolü aşağıdaki gibi gerçekleştirilir: 

- Sunucu daha önce bir bağlantı kesme isteği başlatmışsa (istemci soketi bir FIN paketi zaten aldıysa, bir ACK ile yanıtladı ve kapatma bekleme durumundaysa), NetX Duo istemci TCP yuvası durumunu son ACK durumuna yükseltir ve bir FIN paketi gönderir. Ardından, bağlantıyı kesmeden ve kapalı durumu girerek sunucudan bir ACK 'i bekler.

- Öte yandan istemci, bir bağlantı kesme isteği başlatmakta (sunucu bağlantısı kesilmemiştir ve yuva hala kurulu durumdaysa), NetX Duo bağlantı kesmeyi başlatmak için bir FIN paketi gönderir ve bağlantı kesmeyi tamamlamadan ve yuvayı kapalı bir duruma yerleştirerek sunucudan bir FIN ve bir ACK alıp almamayı bekler.

Yuva iletme kuyruğunda hala paketler varsa, NetX Duo, paketlerin onaylanılmasına izin vermek için belirtilen zaman aşımı süresini askıya alır. Zaman aşımı süresi dolarsa NetX Duo, istemci yuvasının iletim sırasını boşaltır. 

İstemci yuvasıyla bağlantı noktasının bağlantısını kesmek için uygulama ***nx_tcp_client_socket_unbind*** çağırır. Yuva, bağlantı noktası yayınlanmadan önce kapalı durumda veya bağlantısının kesilmesi (örneğin, SÜRELI bekleme durumu) işleminde olmalıdır; Aksi takdirde bir hata döndürülür.

Son olarak, uygulama artık istemci yuvasına ihtiyaç duymuyorsa, yuvasını silmek için ***nx_tcp_socket_delete*** çağırır.

### <a name="tcp-server-connection"></a>TCP sunucusu bağlantısı      
TCP bağlantısının sunucu tarafı pasif olur; Yani, sunucu bir istemcinin bağlantı isteği başlatmasını bekler. İstemci bağlantısını kabul etmek için, önce TCP **nx_tcp_enable** _ HIZMETINI çağırarak IP örneğinde TCP 'nin etkinleştirilmesi gerekir. Daha sonra, uygulamanın _ *_nx_tcp_socket_create_** hizmetini kullanarak bir TCP yuvası oluşturması gerekir.  

Sunucu yuvası, bağlantı isteklerini dinlemek için de ayarlanmalıdır. Bu, ***nx_tcp_server_socket_listen*** hizmeti kullanılarak elde edilir. Bu hizmet, sunucu yuvasını dınleme durumuna koyar ve belirtilen sunucu bağlantı noktasını yuvaya bağlar.

> [!NOTE] 
> *Bir yuva dinleme geri çağırma yordamı ayarlamak için, uygulama **nx_tcp_server_socket_listen** hizmetinin tcp_listen_callback bağımsız değişkeni için uygun geri çağırma işlevini belirtir. Bu uygulama geri çağırma işlevi, bu sunucu bağlantı noktasında her yeni bağlantı istendiğinde NetX Duo tarafından yürütülür. Geri çağırmada işlem uygulama denetimi altında.*

İstemci bağlantı isteklerini kabul etmek için, uygulama ***nx_tcp_server_socket_accept** _ hizmetini çağırır. Sunucu yuvası, bir dınleme durumunda ya da SYN ALıNDı durumunda olmalıdır (yani, sunucu dınleme durumunda ve bağlantı isteyen bir istemciden bir SYN paketi aldı), kabul etme hizmetini çağırmak için. _ *_Nx_tcp_server_socket_accept_** öğesinden başarılı bir dönüş durumu, bağlantının ayarlandığını ve sunucu yuvasının kurulu durumda olduğunu gösterir.

Sunucu yuvasının geçerli bir bağlantısı olduktan sonra, ek istemci bağlantı istekleri listen_queue_size tarafından belirtilen derinliğe kadar sıraya alınır *ve*  * **nx_tcp_server_socket_listen** _ hizmetine geçirilir. Bir sunucu bağlantı noktasında sonraki bağlantıları işlemek için, uygulama _ *_nx_tcp_server_socket_relisten_** öğesini kullanılabilir bir yuva (yani kapalı durumda olan bir yuva) ile çağırmalıdır. Yuva ile ilişkili önceki bağlantı artık tamamlanıp ve yuva kapalı durumdaysa aynı sunucu yuvasının kullanılabileceğini unutmayın.

### <a name="tcp-server-disconnection"></a>TCP sunucusu bağlantısının kesilmesi     
Bağlantıyı kapatmak ***nx_tcp_socket_disconnect*** çağırarak gerçekleştirilir. Askıya alma belirtilmemişse, sunucu yuvası istemci yuvasına bir RST paketi gönderir ve yuvayı kapalı duruma koyar. Aksi takdirde, askıya alma isteniyorsa, tam TCP bağlantı kesme protokolü aşağıdaki gibi gerçekleştirilir:

- İstemci daha önce bir bağlantı kesme isteği başlatmışsa (sunucu yuvası zaten bir FIN paketi aldıysa, bir ACK ile yanıtladı ve kapatma bekleme durumundaysa), NetX Duo TCP yuva durumunu son ACK durumuna yükseltir ve bir FIN paketi gönderir. Ardından, bağlantıyı kesmeden ve kapalı durumu girerek istemciden bir ACK 'i bekler.

- Öte yandan sunucu, bir bağlantı kesme isteği başlatmakta (istemcinin bağlantısı kesilmemiştir ve yuva hala kurulu durumdaysa), NetX Duo bağlantı kesmeyi başlatmak için bir FIN paketi gönderir ve bağlantı kesmeyi tamamlamadan ve yuvayı kapalı bir duruma yerleştirerek istemciden bir el ile onay alıp almamayı bekler.

Yuva iletme kuyruğunda hala paketler varsa, NetX Duo bu paketlerin onaylanılmasına izin vermek için belirtilen zaman aşımı süresini askıya alır. Zaman aşımı süresi dolarsa NetX Duo, sunucu yuvasının iletim sırasını temizler.

Bağlantı kesme işlemi tamamlandıktan ve sunucu yuvası kapalı durumdaysa, Bu yuvanın sunucu bağlantı noktasıyla ilişkilendirmesini sonlandırmak için uygulamanın ***nx_tcp_server_socket_unaccept** _ hizmetini çağırması gerekir. _*_Nx_tcp_socket_disconnect_*_ veya _*_nx_tcp_server_socket_accept_*_ bir hata durumu döndürmesi durumunda bile bu hizmetin uygulama tarafından çağrılması gerekir. _*_Nx_tcp_server_socket_unaccept_*_ çağrıldıktan sonra, yuva istemci veya sunucu yuvası olarak kullanılabilir veya artık gerekmiyorsa silinebilir. Aynı sunucu bağlantı noktasında başka bir istemci bağlantısını kabul etmeniz isteniyorsa, bu yuvada _ *_nx_tcp_server_socket_relisten_** hizmeti çağrılmalıdır.

Aşağıdaki kod segmenti tipik bir TCP sunucusunun kullandığı çağrıların dizisini gösterir:

```c
/* Set up a previously created TCP socket to
   listen on port 12 */
nx_tcp_server_socket_listen()

/* Loop to make a (another) connection. */
while(1)
{
    /* Wait for a client socket connection request
       for 100 ticks. */
    nx_tcp_server_socket_accept();

    /* (Send and receive TCP messages with the TCP
       client) */

    /* Disconnect the server socket. */
    nx_tcp_socket_disconnect();

    /* Remove this server socket from listening on
       the port. */
    nx_tcp_server_socket_unaccept(&server_socket);
    /* Set up server socket to relisten on the
       same port for the next client. */
    nx_tcp_server_socket_relisten();
}
```

### <a name="mss-validation"></a>, Bu doğrulama      
En büyük kesim boyutu (Bu), TCP ana bilgisayarının, temel alınan IP katmanı tarafından parçalanmadan alabileceği en yüksek bayt miktarıdır. TCP bağlantı kurma aşaması sırasında, gönderenin, alıcının alt bileşenlerinden daha büyük bir TCP veri segmenti göndermemesi için kendi TCP sahip olduğu değeri her iki sona erer. NetX Duo TCP modülü, bir bağlantı kurmadan önce, eşin tanıtılan bir değeri isteğe bağlı olarak doğrular. Varsayılan olarak NetX Duo bu tür bir denetimi etkinleştirmez. En az bir NetX Duo kitaplığı oluştururken ve en düşük değer _*_NX_TCP_MSS_MINIMUM_*_ tanımlanmak için, bu, bir, ve bu doğrulamayı gerçekleştirmek isteyen uygulamalar ***NX_ENABLE_TCP_MSS_CHECK** _ tanımlar. _ *_NX_TCP_MSS_MINIMUM_** altındaki, bu değerleri IÇEREN gelen TCP bağlantıları bırakılır.

### <a name="stop-listening-on-a-server-port"></a>Sunucu bağlantı noktasında dinlemeyi durdur    
Uygulama, daha önce ***nx_tcp_server_socket_listen** _ hizmeti çağrısıyla belirtilen bir sunucu bağlantı noktasındaki istemci bağlantı isteklerini dinlemek isterse, uygulama yalnızca _ *_nx_tcp_server_socket_unlisten_** hizmetini çağırır. Bu hizmet, bir bağlantıyı kapalı durumunda geri bekleyen bir yuva koyar ve sıraya alınan istemci bağlantı isteği paketlerini serbest bırakır. 

### <a name="tcp-window-size"></a>TCP pencere boyutu   
Bağlantının kurulum ve veri aktarımı aşamaları sırasında, her bağlantı noktası işleyebileceği veri miktarını rapor edebilir ve bu, pencere boyutu olarak adlandırılır. Veriler alınıp işlendiğinde, bu pencere boyutu dinamik olarak ayarlanır. TCP 'de, gönderici yalnızca alıcının penceresine sığan veri miktarı gönderebilir. Esas olarak pencere boyutu, bağlantının her yönünde veri aktarımı için akış denetimi sağlar.   

### <a name="tcp-packet-send"></a>TCP paketi gönderme     
TCP verilerinin gönderilmesi ***nx_tcp_socket_send*** işlevi çağırarak kolayca gerçekleştirilir. Aktarılan verilerin boyutu, yuvanın sahip olduğu değerin veya geçerli eş alma penceresi boyutunun (hangisi daha küçükse) daha büyükse, iletim için en az (örneğin, eş alma penceresi) olan verileri, TCP iç mantığını kapatır. Bu hizmet daha sonra paketin önünde (sağlama toplamı hesaplaması dahil) bir TCP üst bilgisi oluşturur. Alıcının pencere boyutu sıfır değilse, çağıran alıcının pencere boyutunu dolduracağı kadar veri gönderir. Alma penceresi sıfır olursa, çağıran, bu paketin gönderilmesi için alıcının pencere boyutunun yeterince artırılmasına izin verebilir ve bu işlemin boyutunu bekleyebilir. Belirli bir zamanda, aynı yuva üzerinden veri gönderilmeye çalışılırken birden çok iş parçacığı askıya alabilir. 

> [!WARNING]  
> *NX_PACKET yapısında bulunan TCP verileri uzun bir sözcük sınırında bulunmalıdır. Buna ek olarak, TCP, IP ve fiziksel medya üstbilgilerini yerleştirmek için önüne işaretçisi ve veri başlangıç işaretçisi arasında yeterli alan olması gerekir*.

### <a name="tcp-packet-retransmit"></a>TCP paketi yeniden aktarım      
Daha önce gönderilen TCP paketleri, bağlantının diğer tarafından bir ACK döndürülünceye kadar dahili olarak depolanır. Aktarılan veriler zaman aşımı süresi içinde onaylanmazsa, depolanan paket yeniden gönderilir ve sonraki zaman aşımı süresi ayarlanır. Bir ACK alındığında, iç aktarım sırasındaki onay numarası kapsamındaki tüm paketler son olarak serbest bırakılır.  

> [!WARNING]   
> *Uygulama, paketi yeniden kullanmamalıdır veya nx_tcp_socket_send () NX_SUCCESS geri döndüğünde paketin içeriğini değiştirmeyecektir. İletilen paket son olarak NetX Duo iç işleme tarafından, veriler diğer bir uçtan onaylandıktan sonra serbest* bırakılır.

### <a name="tcp-keepalive"></a>TCP KeepAlive     
TCP KeepAlive özelliği, bir yuvanın, doğru sonlandırma olmadan (örneğin, eşler kilitlendi) veya belirli ağ izleme tesislerinin uzun süreler için bir bağlantıyı sonlandırmasını engellemek için bir yuva sağlar. TCP KeepAlive, veri içermeyen bir TCP çerçevesi göndererek ve sıra numarası geçerli sıra numarasından bir daha az olacak şekilde, düzenli aralıklarla işe yarar. Bu tür TCP KeepAlive çerçevesini alırken alıcı, hala etkin ise geçerli sıra numarası için bir ACK ile yanıtlar. Bu işlem, KeepAlive işlemini tamamlar.  

Varsayılan olarak, KeepAlive özelliği etkin değildir. Bu özelliği kullanmak için NetX Duo Kitaplığı ***NX_ENABLE_TCP_KEEPALIVE** _ tanımlı ile oluşturulmalıdır. _ *_NX_TCP_KEEPALIVE_INITIAL_** sembolü, KEEPALIVE çerçevesi başlatılmadan önce geçen işlem yapılmayan saniye sayısını belirtir.  

### <a name="tcp-packet-receive"></a>TCP paket alma   
TCP alma paketi işleme (IP Yardımcısı iş parçacığından çağrılır), çeşitli bağlantı ve bağlantı kesme eylemlerinin yanı sıra iletme bildirimi işleme işleminden sorumludur. Ayrıca, TCP alma paketi işleme, uygun TCP yuvasının alma kuyruğuna veri alma veya paketi bekleyen ilk askıya alınan iş parçacığına paket teslim etme işleminden sorumludur.

### <a name="tcp-receive-notify"></a>TCP alma bildirimi     
Uygulama iş parçacığının birden fazla yuvada alınan verileri işlemesi gerekiyorsa ***nx_tcp_socket_receive_notify*** işlevi kullanılmalıdır. Bu işlev, yuva için bir alma paketi geri çağırma işlevi kaydeder. Yuvada her bir paket alındığında geri çağırma işlevi yürütülür.  

Geri çağırma işlevinin içerikleri, applicationspecific; Ancak, işlev büyük olasılıkla işleme iş parçacığını bir paketin ilgili yuvada kullanılabilir olduğunu bildirmek için mantık içerebilir. 

### <a name="thread-suspension"></a>İş parçacığı askıya alma      
Daha önce belirtildiği gibi, uygulama iş parçacıkları belirli bir TCP bağlantı noktasından veri almaya çalışırken askıya alabilir. Bu bağlantı noktasında bir paket alındıktan sonra, bu, askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı daha sonra sürdürülür. Birçok NetX Duo hizmeti için kullanılabilen bir TCP alma paketi üzerinde askıya alma sırasında isteğe bağlı bir zaman aşımı kullanılabilir.  

İş parçacığı askıya alma, bağlantı (istemci ve sunucu), istemci bağlama ve bağlantı kesme hizmetleri için de kullanılabilir.  

### <a name="tcp-socket-statistics-and-errors"></a>TCP yuvası Istatistikleri ve hataları     
Etkinleştirilirse, NetX Duo TCP yuvası yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP/TCP örneği için aşağıdaki istatistikler ve hata raporları korunur:   

- Gönderilen toplam TCP paketi sayısı  
- Gönderilen toplam TCP bayt sayısı  
- Toplam alınan TCP paketi sayısı   
- Toplam alınan TCP baytı   
- Toplam TCP geçersiz paket sayısı   
- Bırakılan toplam TCP alma paketi sayısı    
- Toplam TCP alma sağlama toplamı hatası   
- Toplam TCP bağlantısı   
- Toplam TCP bağlantısı sayısı   
- Bırakılan toplam TCP bağlantısı    
- Toplam TCP paketi yeniden Iletim sayısı   
- Gönderilen TCP yuva paketleri   
- Gönderilen TCP yuva baytları   
- Alınan TCP yuvası paketleri   
- Alınan TCP yuva baytları   
- TCP yuvası paketi yeniden aktarımlar    
- Sıraya alınan TCP yuvası paketleri    
- TCP yuvası sağlama toplamı hataları    
- TCP yuva durumu    
- TCP yuvası Iletme sırası derinliği    
- TCP yuvası Iletme penceresi boyutu    
- TCP yuvası alma penceresi boyutu    

Tüm bu istatistik ve hata raporları, toplam TCP istatistikleri için ***nx_tcp_info_get** _ hizmeti ve yuva başına TCP istatistikleri için _ *_nx_tcp_socket_info_get_** hizmeti ile uygulama tarafından kullanılabilir.

### <a name="tcp-socket-control-block-nx_tcp_socket"></a>TCP yuvası denetim bloğu NX_TCP_SOCKET      
Her TCP yuvasının özellikleri, IP veri yapısına, ağ bağlantı arabirimine, bağlı bağlantı noktasına ve alma paketi kuyruğuna bağlantı gibi yararlı bilgiler içeren ilişkili *NX_TCP_SOCKET* denetim bloğunda bulunur. Bu yapı ***nx_api. h*** dosyasında tanımlanmıştır.