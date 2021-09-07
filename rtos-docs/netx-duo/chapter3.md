---
title: Bölüm 3 - NetX Duo Azure RTOS İşlevsel Bileşenleri
description: Bu bölümde NetX Duo TCP/IP yığınının işlevsel Azure RTOS yüksek performanslı bağlantıların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c96e6e422ea570085f5d7c6aeaaaa697a2393b5e
ms.sourcegitcommit: 20a136b06a25e31bbde718b4d12a03ddd8db9051
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2021
ms.locfileid: "123552390"
---
# <a name="chapter-3---functional-components-of-azure-rtos-netx-duo"></a>Bölüm 3 - NetX Duo Azure RTOS İşlevsel Bileşenleri

Bu bölümde NetX Duo TCP/IP yığınının işlevsel Azure RTOS yüksek performanslı bağlantıların açıklaması yer almaktadır. 

## <a name="execution-overview"></a>Yürütmeye Genel Bakış

NetX Duo uygulaması içinde beş tür program yürütme vardır: başlatma, uygulama arabirimi çağrıları, iç IP iş parçacığı, IP düzenli süre önceleri ve ağ sürücüsü.

> [!NOTE]
> *NetX Duo, ThreadX'in var olduğunu varsayıyor ve iş parçacığı yürütme, askıya alma, düzenli süreler ve karşılıklı dışlama tesislerine bağlıdır.*

### <a name="initialization"></a>Başlatma

Başka bir NetX Duo **nx_system_initialize** çağrılmadan önce hizmet * nx_system_initialize _ çağrılmalı. Sistem başlatma, ThreadX _ tx_application_define **_işlevinden_* veya uygulama iş parçacıklarından çağrılebilir.

***nx_system_initialize** _ döndürdikten sonra sistem paket havuzları ve IP örnekleri oluşturmak için hazırdır. BIR IP örneği oluşturmak için varsayılan paket havuzu gerekli olduğundan, IP örneği oluşturmadan önce en az bir NetX Duo paket havuzu mevcut olması gerekir. Paket havuzları ve IP örnekleri oluşturma, ThreadX başlatma işlevinden _ *_tx_application_define_** ve uygulama iş parçacıklarından izin verilir.

Dahili olarak, bir IP örneği oluşturma iki bölümde yapılır: İlk bölüm, çağrıyı yapanın bağlamından veya ***tx_application_define*** iş parçacığının bağlamından yapılır. Buna IP veri yapısını ayarlama ve iç IP iş parçacığı da dahil olmak üzere çeşitli IP kaynakları oluşturma dahildir. İkinci bölüm, iç IP iş parçacığından ilk yürütme sırasında gerçekleştirilir. BURADA IP oluşturmanın ilk bölümü sırasında sağlanan ağ sürücüsüne ilk çağrılır. İç IP iş parçacığından ağ sürücüsünün çağrılarak sürücünün başlatma işlemi sırasında I/O gerçekleştirmesi ve askıya alınmasına olanak sağlar.

Ağ sürücüsü başlatma işlemeden döndüğünde IP oluşturma işlemi tamamlanır.

NetX Duo'da IPv6'yı başlatma için birkaç ek NetX Duo hizmeti gerekir. Bunlar, bu bölümün ilerleyen kısımlarında [NetX Duo'daki IPv6](#ipv6-in-netx-duo) bölümünde daha ayrıntılı olarak açıklanmıştır.

> [!NOTE]
> *NetX Duo hizmeti **nx_ip_status_check** IP örneği ve birincil arabirim durumu hakkında bilgi almak için kullanılabilir. Bu tür durum bilgileri, bağlantının başlatılmış, etkin ve IP adresinin çözümlenmiş olup olmadığını içerir. Bu bilgiler, yeni oluşturulan bir IP örneğini kullanmak zorunda olan uygulama iş parçacıklarını eşitlemek için kullanılır. Birden çok girişli sistemler için bkz. [Çoklu Giriş Desteği.](#multihome-support) **nx_ip_interface_status_check** arabirimde 3information elde etmek için kullanılabilir.*

### <a name="application-interface-calls"></a>Uygulama Arabirimi Çağrıları

Uygulama çağrıları büyük ölçüde ThreadX RTOS altında çalışan uygulama iş parçacıklarından yapılır. Ancak, bazı başlatma, oluşturma ve etkinleştirme hizmetleri ***tx_application_define.*** [Bölüm 4 - NetX Duo Services'Azure RTOS](chapter4.md) açıklaması'nın "İzin VerilenLer" bölümleri, her netx Duo hizmetinin hangi hizmetlerden çağrıla olduğunu belirtmektedir.

Çoğu durumda, sağlama sağlamaları gibi yoğun iş parçacıklarını işleme işlemi, diğer iş parçacıklarının IP örneğine erişimini engellemeden çağrıyı yapılan iş parçacığı bağlamında yapılır. Örneğin, iletimde UDP sağlama sayısı hesaplaması*nx_udp_socket_send _ hizmeti içinde, temel ALıNAN IP gönderme işlevi çağrıldan önce gerçekleştirilir. Alınan bir pakette UDP sağlama toplam değeri, uygulama *_iş parçacığında yürütülen_* _ nx_udp_socket_receive * hizmette hesaplanır. Bu, düşük öncelikli iş parçacıklarında yoğun sağlamam hesaplaması nedeniyle yüksek öncelikli iş parçacıklarının ağ isteklerinin duraklamasını önlemeye yardımcı olur.

IP adresleri ve bağlantı noktası numaraları gibi değerler, konak bayt sırasına göre API'lere geçirildi. Dahili olarak bu değerler de konak bayt sırasına göre depolanır. Bu, geliştiricilerin değerleri bir hata ayıklayıcısı aracılığıyla kolayca görüntülemelerini sağlar. Bu değerler iletim için bir çerçevede programlanmışsa, ağ baytı sırasına dönüştürülür.

### <a name="internal-ip-thread"></a>İç IP İş Parçacığı

Daha önce belirtildiği gibi, NetX Duo'daki her IP örneğinin kendi iş parçacığı vardır. İç IP iş parçacığının öncelik ve yığın boyutu, nx_ip_create ***tanımlanır.*** İç IP iş parçacığı yürütmeye hazır modda oluşturulur. IP iş parçacığı, çağıran iş parçacığından daha yüksek önceliğe sahipse, IP oluşturma çağrısının içinde önme oluşabilir.

İç IP iş parçacığının giriş noktası , _ veya iç ***işlevinde nx_ip_thread_entry.*** İlk kez, iç IP iş parçacığı ilk olarak uygulamaya özgü ağ sürücüsüne üç çağrı yapmadan oluşan ağ sürücüsü başlatmayı tamamlar. İlk çağrı, ağ sürücüsünü IP örneğine eklemek ve ardından ağ sürücüsünün başlatma işleminin üzerinden geçerek bir başlatma çağrısı yapmaktır. Ağ sürücüsü başlatmadan döndükten sonra (donanımın düzgün şekilde ayarlanmış olması beklerken askıya alabilir), iç IP iş parçacığı bağlantıyı etkinleştirmek için ağ sürücüsünü yeniden arar. Ağ sürücüsü bağlantı etkinleştirme çağrısından döndükten sonra, iç IP iş parçacığı bu IP örneği için işlemesi gereken çeşitli olaylar için sonsuza kadar döngü denetimi girer. Bu döngüde işlenen olaylar ertelenmiş IP paketi alımı, IP paket parçası derlemesi, ICMP ping işleme, IGMP işleme, TCP paket kuyruğu işleme, TCP düzenli işleme, IP parçası derleme zaman aşımı ve IGMP düzenli işlemeyi içerir. Olaylar adres çözümleme etkinliklerini de içerir; IPv4'te ARP paket işleme ve ARP düzenli işleme, IPv6'da Yinelenen Adres Algılama, Yönlendirici İsteneni ve Komşu Bulma.

> [!CAUTION]
> *Geri çağırmaları dinleme ve bağlantıyı kesme de dahil olmak üzere NetX Duo geri çağırma işlevleri, özgün çağıran iş parçacığından değil, iç IP iş parçacığından çağrılır. Uygulama herhangi bir NetX Duo geri çağırma işlevinin içinde askıya almama özen gösterir.*

### <a name="ip-periodic-timers"></a>IP Düzenli Süre süreleri

Her IP örneği için kullanılan iki ThreadX düzenli süreer vardır. İlki ARP, IGMP, TCP zaman aşımı için bir saniyelik süreölçerdir ve aynı zamanda IP parçası yeniden birleşebilir işlemeyi de sağlar. İkinci zamanlayıcı, TCP yeniden iletim zaman aşımını ve IPv6 ile ilgili işlemleri başlatmak için 100ms zamanlayıcıdır.

### <a name="network-driver"></a>Ağ Sürücüsü

NetX Duo'daki her IP örneğinin birincil arabirimi vardır ve bu arabirim, nx_ip_create ***hizmette belirtilen cihaz sürücüsü tarafından*** tanımlanır. Ağ sürücüsü, paket iletimi, paket alımı ve durum ve denetim istekleri gibi çeşitli NetX Duo isteklerinin işlenmesinden sorumludur. 

Çok girişli bir sistem için, IP örneğinin her biri ilgili arabirim için bu görevleri gerçekleştiren ilişkili bir ağ sürücüsüne sahip birden çok arabirimi vardır.

Ağ sürücüsünün medyada oluşan zaman uyumsuz olayları da işlemesi gerekir. Medyadan gelen zaman uyumsuz olaylar paket alımını, paket iletimini tamamlamayı ve durum değişikliklerini içerir. NetX Duo, ağ sürücüsüne çeşitli olayları işlemek için çeşitli erişim işlevleri sağlar. Bu işlevler, ağ sürücüsünün kesinti hizmeti yordamı kısmından çağrılarak tasarlanmıştır. IPv4 ağları için, ağ sürücüsü alınan tüm ARP paketlerini iç ***işleve _nx_arp_packet_deferred_receive*** iletmesi gerekir. Tüm RARP paketleri , _ iç işlevi için ***_nx_rarp_packet_deferred_receive** ilet gerekir. IP paketleri için iki seçenek vardır. IP paketlerinin hızlı bir şekilde sevk edilmesi gerekirse, gelen IP paketleri hemen işleme için _ *_ _nx_ip_packet_receive_* _ adresine ilet gerekir. Bu, IP paketlerinin işlenmesinde NetX Duo performansını büyük ölçüde artırır. Aksi takdirde, IP paketlerini _ _ nx_ip_packet_deferred_receive * adresine iletmenin yapılması gerekir.** Bu hizmet, IP paketini ertelenen işleme kuyruğuna, daha sonra iç IP iş parçacığı tarafından işleyiciye yer verir ve bu da en az ISR işleme süresiyle sonuç verir.

Ağ sürücüsü, IP iş parçacığı bağlamının dışında çalışması için kesme işlemini erteleyebilirsiniz. Bu modda, ISR gerekli bilgileri kaydetmeli, _nx_ip_driver_deferred_processing iç işlevini ***çağırarak*** kesme denetleyicisini kabul eder. Bu hizmet, kesintiye neden olan olayın işlemini tamamlamak için IP iş parçacığına cihaz sürücüsüne bir geri arama zamanlaması konusunda bilgi verir.

Bazı ağ denetleyicileri, değerli CPU kaynaklarını tüketmeden donanımda TCP/IP üst bilgi sağlama ve doğrulama gerçekleştirebilirsiniz. Donanım özelliği özelliğine sahip olan NetX Duo, derleme zamanında çeşitli yazılım sağlamam hesaplamasını etkinleştirme veya devre dışı bırakma seçeneklerinin yanı sıra, cihaz sürücüsünün donanım özellikleriyle ilgili IP katmanıyla iletişim kura biliyorsa çalışma zamanında sağlamam hesaplamasını açma veya kapatma seçenekleri sağlar. NetX Duo ağ Azure RTOS yazma hakkında daha ayrıntılı bilgi için Bkz. Bölüm [5 - NetX Duo](chapter5.md) Ağ Sürücüleri.

### <a name="multihome-support"></a>Birden Çok Giriş Desteği

NetX Duo, tek bir IP örneği kullanarak birden çok fiziksel cihaza bağlı sistemleri destekler. Her fiziksel arabirim, IP örneğinde bir arabirim denetim bloğuna atanır. Çoklu giriş sistemi kullanmak isteyen uygulamaların sisteme bağlı fiziksel cihaz **sayısına*** NX_MAX_PHSYCIAL_INTERFACES _ değerini tanımlaması ve NetX Duo kitaplığını yeniden oluşturması gerekir. Varsayılan olarak _ *_NX_MAX_PHYSICAL_INTERFACES_** bir olarak ayarlanır ve IP örneğinde bir arabirim denetim bloğu oluşturulur.

NetX Duo uygulaması, * nx_ip_create _ hizmetini kullanarak birincil **cihaz için tek bir** IP örneği oluşturur. Uygulama, her ek ağ cihazı için _ nx_ip_interface_attach * hizmetini kullanarak cihazı IP *_örneğine_* iliştirer.

Her ağ arabirimi yapısı; arabirim IPv4 adresi, alt ağ maskesi, IP MTU boyutu ve MAC katmanı adres bilgileri de dahil olmak üzere IP denetim bloğunda yer alan ağ arabirimi hakkında bir ağ bilgileri alt kümesi içerir.

> [!NOTE]
> *Çoklu giriş desteğine sahip NetX Duo, NetX Duo'un önceki sürümleriyle geriye dönük olarak uyumludur. Açık arabirim bilgilerini almayan hizmetler varsayılan olarak birincil ağ cihazıdır.*

Birincil arabirim, IP örneği listesinde sıfır dizinine sahiptir. IP örneğine bağlı sonraki her cihaza bir sonraki dizin atanır.

IP örneğinin etkin olduğu TCP, UDP, ICMP ve IGMP gibi tüm üst katman protokol hizmetleri tüm bağlı cihazlar tarafından kullanılabilir.

Çoğu durumda, NetX Duo bir paket iletilirken en iyi kaynak adresini belirler. Kaynak adres seçimi, hedef adresi temel alan bir seçimdir. NetX Duo hizmetleri, uygulamaların hedef adres tarafından en uygun olanı belirlenemezseniz belirli bir kaynak adresi belirtmesine olanak sağlayacak şekilde eklenir. Örneğin, birden çok girişli sistemde bir uygulamanın bir paketi IPv4 yayınına veya çok noktaya yayın hedef adreslerine göndermesi gerekir.

Çok girişli uygulamalar geliştirmeye yönelik hizmetler aşağıdakileri içerir:

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
|***nx_packet_pool_owner***|Bu alan, bu paketin sahibi olan paket havuzunu belirtir. Paket serbest bırakılana kadar bu havuza serbest bırakıldı. Her paketin içindeki havuz sahipliğiyle, bir veri biriminin birden çok paket havuzundan birden çok pakete yayması mümkündür.|
|***nx_packet_next** _|Bu alan, aynı çerçeve içindeki sonraki paketi gösterir. NULL ise, çerçevenin parçası olan ek paket yoktur. Bu alan, paketin tamamı yeniden derlenene kadar parçalanmış paketleri tutmak için de kullanılır. _*NX_DISABLE_PACKET_CHAIN **tanımlanırsa kaldırılır.|
|***nx_packet_last** _|Bu alan, aynı ağ paketi içindeki son paketi belirtir. NULL ise, bu paket tüm ağ paketini temsil eder. Bu alan , _*_NX_DISABLE_PACKET_CHAIN_**tanımlanırsa kaldırılır.|
|***nx_packet_length** _| Bu alan, ağ paketinin tamamına üye tarafından zincirlenmiş tüm paketlerde yer alan tüm baytların toplamı da dahil olmak üzere toplam bayt _nx_packet_next içerir.|
|***nx_packet_ip_interface***| Bu alan, arabirim sürücüsü tarafından alınan pakete ve giden paketler için NetX Duo tarafından atanan arabirim denetim bloğu olur. Arabirim denetim bloğu; ağ adresi, MAC adresi, IP adresi ve bağlantı etkin ve gerekli fiziksel eşleme gibi arabirim durumu gibi arabirimi açıklar.|
|***nx_packet_data_start** _| Bu alan, bu paketin fiziksel yük alanı başlangıcını belirtir. NX_PACKET üst bilgisinde hemen takip etmek zorunda değildir, ancak _ nx_packet_pool_create * hizmeti için *_varsayılan_* değerdir.|
|***nx_packet_data_end** _|Bu alan, bu paketin fiziksel yük alanını belirtir. Bu alan ile _nx_packet_data_start* alanı arasındaki fark yük boyutunu temsil eder.|
|***nx_packet_prepend_ptr** _|Bu alan, paket yükü alanında var olan paket verileri (varsa) önüne protokol üst bilgisi veya gerçek veriler olarak paket verisi eklenmiştir. Bu değer, _nx_packet_data_start* işaretçisi konumunun üzerinde veya ona eşit ve işaretçi işaretçisine *eşit veya nx_packet_append_ptr* gerekir.|
> [!CAUTION]
> *Performansla ilgili nedenlerden dolayı NetX Duo, paket iletim için NetX Duo hizmetlerine geçiriken, ön uç işaretçisinin uzun sözcükle hizalanmış adrese işaret ediyor olduğunu varsayıyor.*

| Paket üst bilgisi | Amaç |
|---|---|
|***nx_packet_append_ptr** _|Bu alan, şu anda paket yükü alanında bulunan verilerin sonuna belirtir. _nx_packet_prepend_ptr* tarafından işaret eden bellek konumu ile *nx_packet_data_end.* Bu alan ile veri alanı *nx_packet_prepend_ptr* bu pakette yer alan veri miktarını temsil eder.|
|***nx_packet_packet_pad** _|Bu alanlar, istenen hizalama gereksinimini elde etmek için doldurma uzunluğunu 4 bayt sözcüklerle tanımlar. Bu alan, _*_NX_PACKET_HEADER_PAD_*_ kaldırılır. Alternatif olarak _*_NX_PACKET_ALIGNMENT_*_ tanımlama yerine _nx_packet_header_pad.*|

### <a name="packet-header-offsets"></a>Paket Üst Bilgisi Uzaklıkları

Paket üst bilgisi boyutu, üst bilgi boyutuna yetecek kadar alan sağlayacak şekilde tanımlanır. Nx_packet_allocate  hizmeti bir paket ayırmak için kullanılır ve pakette ön uç işaretçisini belirtilen paket türüne göre ayarlar. Paket türü, protokol verisi önüne protokol üst bilgisi (UDP, TCP veya ICMP gibi) eklemek için gereken uzaklığı NetX Duo'ya söyler.

Pakette IP üst bilgisi ve fiziksel katman (Ethernet) üst bilgisi dikkate alınarak NetX Duo'da aşağıdaki türler tanımlanmıştır. İkinci durumda, gerekli 4 bayt hizalamayı dikkate alarak 16 bayt olduğu varsayılır. IPv4 paketleri, uygulamaların IPv4 ağlarına paket ayırması için NetX Duo'da hala tanımlanmıştır. NetX Duo kitaplığı IPv6 etkin olarak etkinleştirilmiş olarak etkinleştirilmişse, genel paket türlerinin (NX_IP_PACKET gibi) IPv6 sürümüyle eşlenmiş olduğunu unutmayın. NetX Duo Kitaplığı IPv6 etkin olmadan etkinleştirilmişse, bu genel paket türleri IPv4 sürümüne eşlenmiş.

Aşağıdaki tabloda IPv6 etkin olarak tanımlanan semboller yer alır:

|**Paket Türü** |**Değer** |
|---|---|
|NX_IPv6_PACKET (NX_IP_PACKET) | 0x38 |
|NX_UDPv6_PACKET (NX_UDP_PACKET) |0x40 |
|NX_TCPv6_PACKET (NX_TCP_PACKET) |0x4c |
|NX_IPv4_PACKET |0x24 |
|NX_IPv4_UDP_PACKET |0x2c |
|NX_IPv4_TCP_PACKET |0x38 |

Aşağıdaki tabloda, IPv6 devre dışı bırakılmış olarak tanımlanan semboller yer alır:

|**Paket Türü** |**Değer** |
|---|---|
|NX_IPv4_PACKET (NX_IP_PACKET) |0x24 |
|NX_IPv4_UDP_PACKET (NX_UDP_PACKET) |0x2c |
|NX_IPv4_TCP_PACKET (NX_TCP_PACKET) |0x38 |

Bu değerlerin tanımlandığı *NX_IPSEC_ENABLE* unutmayın. IPsec kullanan uygulama için daha fazla bilgi için NetX Duo IPsec Kullanıcı Kılavuzu'ne bakın.

### <a name="pool-capacity"></a>Havuz Kapasitesi

Paket havuzudaki paket sayısı, yük boyutuna ve paket havuzu oluşturma hizmetine sağlanan bellek alanında yer alan toplam bayt sayısına sahip bir işlevdir. Havuzun kapasitesi, paket boyutu (NX_PACKET üst bilgi boyutu, yük boyutu ve uygun hizalama dahil) sağlanan bellek alanında toplam bayt sayısına bölünerek hesaplanır.

### <a name="payload-area-alignment"></a>Yük Alanı Hizalaması

NetX Duo'da paket havuzu tasarımı sıfır kopyayı destekler. Cihaz sürücüsü düzeyinde, sürücü yük alanı doğrudan veri alımı için arabellek tanımlayıcılarına atayabilecektir. Bazen DMA altyapısı veya önbellek eşitleme mekanizması, yük alanı başlangıç adresinin belirli bir hizalama gereksinimine sahip olması gerekir. Bu, istenen hizalama gereksinimini (bayt cinsinden) içinde tanımlayarak ***NX_PACKET_ALIGNMENT.*** Bir paket havuzu oluştururken, yük alanı başlangıç adresi bu değere hizalanır. Varsayılan olarak, başlangıç adresi 4 bayt hizalıdır.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma

Uygulama iş parçacıkları, boş bir havuzdan paket beklerken askıya alabilir. Havuza bir paket döndürüldü, askıya alınan iş parçacığına bu paket verilir ve devam eder.

Aynı paket havuzunda birden çok iş parçacığı askıya alınırsa, askıya alındıklarına (FIFO) göre devam ederler.

### <a name="pool-statistics-and-errors"></a>Havuz İstatistikleri ve Hataları

Etkinleştirilirse, NetX Duo paket yönetim yazılımı uygulama için yararlı olan çeşitli istatistikleri ve hataları takip eder. Paket havuzları için aşağıdaki istatistikler ve hata raporları korunur:

- Havuzdaki Toplam Paket Sayısı
- Havuza Ücretsiz Paketler
- Toplam Paket Ayırma sayısı
- Havuz Boş Ayırma İstekleri
- Havuz Boş Ayırma Askıya Almaları
- Geçersiz Paket Sürümü

Havuzdaki toplam ve ücretsiz paket sayısı dışındaki tüm bu istatistikler ve hata raporları, * NX_DISABLE_PACKET_INFO _ tanımlanmamışsa NetX Duo **kitaplığında** yerleşik olarak yer alır. Bu veriler uygulama için *___* nx_packet_pool_info_get * hizmetiyle kullanılabilir.

### <a name="packet-pool-control-block-nx_packet_pool"></a>Paket Havuzu Denetim Bloğu NX_PACKET_POOL

Her paket bellek havuzunun özellikleri denetim bloğunda bulunur. Bu, bağlantılı boş paket listesi, boş paket sayısı ve bu havuza gelen paketlerin yük boyutu gibi yararlı bilgiler içerir. Bu yapı, ***nx_api.h dosyasında*** tanımlanır.

Paket havuzu denetim blokları bellekte herhangi bir yerde yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline geldi.

## <a name="ipv4-protocol"></a>IPv4 Protokolü

NetX Duo'nın İnternet Protokolü (IP) bileşeni, İnternet'te IPv4 paketleri göndermekten ve almakla sorumludur. NetX Duo'da, temel ağ sürücüsünü kullanarak TCP, UDP, ICMP ve IGMP iletilerini göndermek ve almak son olarak bileşendir.

NetX Duo hem IPv4 protokolünü (RFC 791) hem de IPv6 protokolünü (RFC 2460) destekler. Bu bölümde IPv4 ele almaktadır. IPv6 bir sonraki bölümde ele alınmıştır.

### <a name="ipv4-addresses"></a>IPv4 Adresleri

İnternet'te her ana bilgisayar, IP adresi olarak adlandırılan benzersiz bir 32 bit tanımlayıcıya sahip olur. Şekil 4'te açıklandığı gibi beş IPv4 adresi sınıfı vardır. Beş IPv4 adres sınıfı aralığı aşağıdaki gibidir:

|Sınıf|Aralık|
|---|---|
|A |0.0.0.0 - 127.255.255.255|
|B |128.0.0.0 - 191.255.255.255|
|C |192.0.0.0 - 223.255.255.255|
|D |224.0.0.0 - 239.255.255.255|
|E |240.0.0.0 - 247.255.255.255|

![IPv4 Adres Yapısı diyagramı.](./media/user-guide/ipv4-address-structure.png)

### <a name="figure-4-ipv4-address-structure"></a>ŞEKIL 4. IPv4 Adres Yapısı

Ayrıca üç tür adres belirtimleri de vardır: *tek noktaya yayın,* *yayın* ve çok *noktaya yayın.* Tek noktaya yayın adresleri, İnternet'te belirli bir ana bilgisayarı tanımlayacak IPv4 adresleridir. Tek noktaya yayın adresleri bir kaynak veya hedef IPv4 adresi olabilir. Yayın adresi belirli bir ağ veya alt ağ üzerinde tüm konakları tanımlar ve yalnızca hedef adres olarak kullanılabilir. Yayın adresleri, adresin ana bilgisayar kimliği kısmının olanlar olarak ayarlanmış olmasıyla belirtilir. Çok noktaya yayın adresleri (Sınıf D), internet üzerinde dinamik bir konak grubu belirtir. Çok noktaya yayın grubunun üyeleri her zaman katılarak ayrıllar.

> [!IMPORTANT]
> *Yalnızca IPv4 üzerinden UDP gibi bağlantısız protokoller yayın ve çok noktaya yayın grubunun sınırlı yayın özelliğini kullanılabilir.*

> [!IMPORTANT]
> *Makro *IP_ADDRESS* ***nx_api.h _ içinde** tanımlanır. Nokta yerine virgül kullanarak IPv4 adreslerinin kolayca belirtimlerini sağlar. Örneğin, _IP_ADDRESS(128,0,0,0)* Şekil 4'te gösterilen birinci sınıf B adresini belirtir.*

### <a name="ipv4-gateway-address"></a>IPv4 Ağ Geçidi Adresi

Ağ geçitleri, ağlarında bulunan konakların yerel etki alanı dışındaki hedeflere giden paketleri iletmelerine yardımcı olur. Her düğüm, hedef komşularından biri veya önceden programlanmış statik yönlendirme tablosu aracılığıyla gönderilecek sonraki atlama hakkında bilgi sahibidir. Ancak bu yaklaşımlar başarısız olursa, düğümün paketi varsayılan ağ geçidine iletmesi gerekir ve bu da paketi hedefine yönlendirme konusunda daha fazla bilgiye sahip olur. Varsayılan ağ geçidine IP örneğine bağlı fiziksel arabirimlerden biri aracılığıyla doğrudan erişilebilir olması gerektiğini unutmayın. Uygulama, IPv4 nx_ip_gateway_address_set ağ **geçidi** adresini yapılandırmak için * nx_ip_gateway_address_set _ çağrısı yapıyor. Geçerli IPv4 _*_nx_ip_gateway_address_get_*_ almak için hizmet sunucusunu kullanın. Uygulama, ağ geçidi ayarını *_temizlemek nx_ip_gateway_address_clear_* _ nx_ip_gateway_address_clear * hizmetini kullanacağız.

### <a name="ipv4-header"></a>IPv4 Üst Bilgisi

Herhangi bir IPv4 paketinin İnternet'te gönderilene bir IPv4 üst bilgisi olması gerekir. Daha üst düzey protokoller (UDP, TCP, ICMP veya IGMP) bir paket göndermek için IP bileşenini çağırsa, IPv4 iletme modülü verilerin önüne bir IPv4 üst bilgisi yer alır. Buna karşılık, IP paketleri ağdan alınarak, IP bileşeni daha üst düzey protokollere teslimten önce paketten IPv4 üst bilgisini kaldırır. Şekil 5'te IP üst bilgisi biçimi görüntülenir.

![IPv4 Üst Bilgi Biçimi](./media/user-guide/ipv4-header-format.png)

### <a name="figure-5-ipv4-header-format"></a>ŞEKIL 5. IPv4 Üst Bilgi Biçimi

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm üst big endian **beklenir.** Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır. Örneğin, IP üst bilgisi 4 bit sürümü ve 4 bit üst bilgi uzunluğu üst bilginin ilk baytı üzerinde yer alalır.*

IPv4 üst bilgisi alanları aşağıdaki gibi tanımlanır:

|IPv4 &nbsp; Üst Bilgi &nbsp; Alanı |Amaç |
|---|---|
|***4 bit sürüm*** |Bu alan, bu üst bilginin temsil ettiği IP sürümünü içerir. NetX Duo'nın desteklediği IP sürüm 4 için bu alanın değeri 4'dür. |
|***4 bit üst bilgi uzunluğu*** |Bu alan, IP üst bilgisinde 32 bit sözcük sayısını belirtir. Seçenek sözcükleri yoksa bu alanın değeri 5'tir. |
|***8 bit hizmet türü (TOS)*** |Bu alan, bu IP paketi için istenen hizmet türünü belirtir. Geçerli istekler aşağıdaki gibidir:<br />- Normal: 0x00 <br />- En Düşük Gecikme: 0x00<br />- Maksimum Veri: 0x08<br />- Maksimum Güvenilirlik: 0x04<br />- Minimum Maliyet: 0x02 |
|***16 bit toplam uzunluk*** |Bu alan, IP üst bilgisi dahil olmak üzere IP veri biriminin bayt cinsinden toplam uzunluğunu içerir. IP veri birimi, TCP/IP İnterneti üzerinde bulunan temel bilgi birimidir. Verilere ek olarak bir hedef ve kaynak adresi içerir. 16 bitlik bir alan olduğundan IP veri biriminin en büyük boyutu 65.535 bayttır.|
|***16 bit tanımlama*** |alanı, bir konaktan gönderilen her IP veri birimini benzersiz olarak tanımlamak için kullanılan bir sayıdır. Bu sayı genellikle bir IP veri birimi gönderildikten sonra artırılır. Özellikle alınan IP paketi parçalarının birleştirilmesinde yararlıdır.|
|***3 bit bayraklar*** |Bu alan IP parçalanma bilgilerini içerir. Bit 14, "parçalama" bitidir. Bu bit ayarlanırsa giden IP veri birimi parçalanmaz. Bit 13, "daha fazla parça" bitidir. Bu bit ayarlanırsa daha fazla parça vardır. Bu bit netse, bu IP paketinin son parçasıdır.|
|***13 bit parça uzaklığı*** |Bu alan, parça uzaklığının üst 13 bitlerini içerir. Bu nedenle, parça uzaklıklarına yalnızca 8 bayt sınırlarda izin verilir. Parçalı BIR IP veri biriminin ilk parçası "daha fazla parça" bit kümesine ve 0 uzaklığına sahip olur.|
|***8 bit yaşam süresi (TTL)*** |Bu alan, bu veri biriminin geçeceği yönlendirici sayısını içerir ve bu da temelde veri biriminin ömrünü sınırlar.|
|***8 bit protokol***|Bu alan, IP veri birimini hangi protokolün kullanmakta olduğunu belirtir. Aşağıda geçerli protokollerin ve bunların değerlerinin listesi ve liste yer almaktadır:<br />-ICMP: 0x01 <br />-IGMP: 0x02<br />-TCP: 0X06<br />-UDP: 0X11 |
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
- Toplam IP Alma Sağlama Toplamı Hataları
- Bırakılan Toplam IP Gönderme Paketleri
- Gönderilen Toplam IP Parçaları
- Alınan Toplam IP Parçaları

Bu istatistiklerin ve hata raporlarının hepsi uygulamanın nx_ip_info_get ***kullanılabilir.***

### <a name="ip-control-block-nx_ip"></a>IP Denetim Bloğu NX_IP

Her IP örneğinin özellikleri denetim bloğunda bulunur. Her ağ aygıtının IP adresleri ve ağ maskeleri gibi yararlı bilgiler ile komşu IP ve fiziksel donanım adresi eşlemesi tablosu içerir. Bu yapı ***nx_api.h _file.** IPv6 etkinse, aynı zamanda bir IPv6 adresi dizisi içerir; bu sayı , kullanıcı tarafından yapılandırılabilir __*_ NX_MAX_IPV6_ADDRESSES ** tarafından belirtilir. Varsayılan değer, her fiziksel ağ arabiriminin üç IPv6 adresine sahip olduğunu gösterir.

IP örneği denetim blokları bellekte herhangi bir yerde yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline gelmektedir.

### <a name="static-ipv4-routing"></a>Statik IPv4 Yönlendirme

Statik yönlendirme özelliği, bir uygulamanın belirli ağ dışı hedef IP adresleri için bir IPv4 ağı ve sonraki atlama adresi belirtmesini sağlar. Statik yönlendirme etkinse NetX Duo, gönderilecek paketin hedef adresiyle eşleşen bir giriş için statik yönlendirme tablosunda arama gönderir. Eşleşme yoksa NetX Duo, fiziksel arabirimler listesinde arama ve hedef IP adresi ile ağ maskesine göre bir kaynak IP adresi ve sonraki atlama adresi seçer. Hedef, IP örneğine bağlı ağ sürücülerinin IP adreslerinden herhangi biri ile eşlen yoksa NetX Duo, varsayılan ağ geçidine doğrudan bağlı bir arabirim seçer ve kaynak adres olarak arabirimin IP adresini, sonraki atlama olarak da varsayılan ağ geçidini kullanır.

Girdiler sırasıyla * nx_ip_static_route_add _ ve _ **nx_ip_static_route_delete*** hizmetleri kullanılarak statik *_yönlendirme tablosundan_* eklenebilir ve kaldırılabilir. Statik yönlendirmeyi kullanmak için konak uygulamanın bu özelliği etkinleştirmesi gerekir. Bu özellik, ***NX_ENABLE_IP_STATIC_ROUTING.***

> [!NOTE]
> *NetX Duo, statik yönlendirme tablosuna bir giriş eklerken tabloda zaten belirtilen hedef adres için eşleşen bir giriş olduğunu denetler. Varsa, ağ maskesinde daha küçük ağ (daha uzun ön ek) olan girişe tercih verir.*

### <a name="ipv4-forwarding"></a>IPv4 İ iletme

Gelen IPv4 paketi bu düğümü hedeflenemdiyse ve IPv4 iletme özelliği etkinse, NetX Duo paketi diğer arabirimler aracılığıyla iletmeye çalışır.  

### <a name="ip-fragmentation"></a>IP Parçalanması

Ağ cihazı giden paketlerin boyutuna göre sınırlara sahip olabilir. Bu sınır, maksimum iletim birimi (MTU) olarak adlandırılan bir sınırdır. IP MTU, bir bağlantı katmanı sürücüsünün IP paketini parçalanmadan ilettiği en büyük IP çerçevesi boyutudur. Bir cihaz sürücüsünü başlatma aşamasında, sürücü modülünün IP MTU boyutunu hizmet sunucusu üzerinden ***nx_ip_interface_mtu_set.***

Önerilmez, ancak uygulama, cihaz tarafından desteklenen temel IP MTU'suna göre daha büyük veri birimleri üretebilir. Bu TÜR BIR IP veri birimini iletmeden önce IP katmanının bu paketleri parçalanması gerekir. Parçalı IP çerçeveleri alırken, alıcı uç aynı parçalanma kimliğine sahip tüm parçalanmış IP çerçevelerini depolamalı ve bunları sırayla yeniden değerlendirebilir. IP alma mantığı özgün IP çerçevesini zamanda geri yüklemek için tüm parçaları topalamazsa, tüm parçalar serbest olur. Bu tür bir paket kaybını algılamak ve bu durumdan kurtarmak üst katman protokolüne göredir.

IP parçalanması hem IPv4 hem de IPv6 paketleri için geçerlidir.

IP parçalanması ve yeniden değerlendirme işlemi desteklemek için sistem tasarımcısının NetX Duo'da IP parçalanma özelliğini nx_ip_fragment_enable ***gerekir.*** Bu özellik etkinleştirilmezse, gelen parçalanmış IP paketleri ve ağ sürücüsünün MTU'suna aşan paketler atılır.

> [!NOTE]
> *NETX Duo kitaplığını oluşturmada ***** NX_DISABLE_FRAGMENTATION _ tanımlayarak IP Parçalanması mantığı tamamen kaldırılabilir. Bunu yapmak NetX Duo'nın kod boyutunu azaltmaya yardımcı olur. Bu durumda, hem IPv4 hem de IPv6 parçalanma/yeniden değerlendirme işlevlerinin disabled._

> [!NOTE]
> *Ip **NX_DISABLE_CHAINED_PACKET** tanımlanmışsa IP parçalanması devre dışı bırakılmıştır.*

> [!NOTE]
> *Bir IPv6 ağına, veri biriminin boyutu en düşük MTU boyutunu aşarsa yönlendiriciler bir veri birimini parçalamaz. Bu nedenle, kaynak ve hedef arasındaki en düşük MTU'nun belirlenmesi ve IP veri birimi boyutunun MTU yolunu aşmaması gönderen cihaza bağlı olur. NetX Duo'da IPv6 PATH MTU bulma özelliği, tanımlanan simgeye sahip NetX Duo **NX_ENABLE_IPV6_PATH_MTU_DISCOVERY** etkinleştirilebilir.*

## <a name="address-resolution-protocol-arp-in-ipv4"></a>IPv4'te Adres Çözümleme Protokolü (ARP)

Adres Çözümleme Protokolü (ARP), 32 bit IPv4 adreslerini temel alınan fiziksel medya (RFC 826) adreslerine dinamik olarak eşlemeden sorumludur. Ethernet en tipik fiziksel medyadır ve 48 bit adresleri destekler. ARP ihtiyacı * nx_ip_create _ hizmetine sağlanan **ağ sürücüsü** tarafından belirlenir. Fiziksel eşleme gerekli ise, ağ sürücüsünün sürücü arabirimini düzgün yapılandırmak için _ *_nx_interface_address_mapping_needed_** hizmetini kullanması gerekir.

### <a name="arp-enable"></a>ARP Etkinleştirme

ARP'nin düzgün çalışması için önce uygulama tarafından nx_arp_enable ***etkinleştirilmesi*** gerekir. Bu hizmet, ARP etkinleştirme hizmetine sağlanan bellekten ARP önbellek alanı oluşturma da dahil olmak üzere ARP işleme için çeşitli veri yapıları ayarlar.

### <a name="arp-cache"></a>ARP Önbelleği

ARP önbelleği, iç ARP eşleme veri yapılarının dizisi olarak görünüme sahip olabilir. Her iç yapı, bir IP adresi ile fiziksel donanım adresi arasındaki ilişkiyi koruyabilirsiniz. Ayrıca, her veri yapısında bağlantı işaretçileri vardır, bu nedenle birden çok bağlantılı liste olabilir.

Uygulama, eşleme ARP tablosunda mevcutsa **,** hizmet * nx_arp_ip_address_find _ kullanarak donanım MAC adresi serek ARP önbelleğinden bir IP adresine bakabilirsiniz. Benzer şekilde, _ *_nx_arp_hardware_address_find_** hizmeti belirli bir IP adresi için MAC adresini döndürür.

### <a name="arp-dynamic-entries"></a>ARP Dinamik Girişleri

Varsayılan olarak, ARP etkinleştirme hizmeti ARP önbelleğine tüm girişleri kullanılabilir dinamik ARP girdileri listesine yer ayarlar. Eşlenmemiş bir IP adresine istek gönder algılandığında NetX Duo tarafından bu listeden dinamik bir ARP girişi ayrılır. Ayırmadan sonra ARP girişi ayarlanır ve fiziksel medyaya bir ARP isteği gönderilir.

Dinamik bir giriş, hizmeti tarafından da ***nx_arp_dynamic_entry_set.***

> [!IMPORTANT]
> *Tüm dinamik ARP girişleri kullanılıyorsa, en son kullanılan ARP girişi yeni bir eşlemeyle değiştirilir.*

### <a name="arp-static-entries"></a>ARP Statik Girişleri

Uygulama ayrıca * ağ eşlemesini kullanarak statik ARP **eşlemesi nx_arp_static_entry_create _service.** Bu hizmet, dinamik ARP giriş listesinden bir ARP girişi ayırır ve uygulama tarafından sağlanan eşleme bilgileriyle statik listeye yer alır. Statik ARP girişleri yeniden kullanılabilir veya eskime durumuna tabi değildir. Uygulama, statik bir girişi silmek için _*_nx_arp_static_entry_delete._*_ Uygulama, ARP tablosunda yer alan tüm statik girişleri kaldırmak için _* nx_arp_static_entries_delete **_hizmetini_ kullanabilir.

### <a name="automatic-arp-entry"></a>Otomatik ARP Girişi

NetX Duo, ARP isteğine eş yanıt verdikten sonra eş ip/MAC eşlemesini kaydeder. NetX Duo ayrıca ağdan gelen istenmeyen ARP isteklerini temel alan eş IP/MAC adresi eşlemesini kaydeden otomatik ARP giriş özelliğini de uygulamaya alır. Bu özellik, ARP tablosu eş bilgileriyle doldurularak ARP isteği/yanıt döngüsünde geçen gecikme süresinin azaltılmasına olanak sağlar. Ancak otomatik ARP'nin etkinleştirilmenin dezavantajı, ARP tablosu meşgul bir ağ üzerinde yerel bağlantıda çok sayıda düğümle hızla doldurulma eğiliminde olmasıdır ve bu da sonunda ARP girişinin değiştirilmesine neden olur.

Bu özellik varsayılan olarak etkindir. Bunu devre dışı bırakmak için NetX Duo kitaplığı, tanımlanan simgeyle ***NX_DISABLE_ARP_AUTO_ENTRY*** gerekir.</p>

### <a name="arp-messages"></a>ARP İletileri

Daha önce belirtildiği gibi, IP görevi bir IP adresi için eşleme gerektiğini algılayan bir ARP istek iletisi gönderilir. ARP istekleri, karşılık gelen bir ARP yanıtı **alınana kadar** düzenli aralıklarla (her * NX_ARP_UPDATE_RATE _ saniye) gönderilir. ARP girişimi *_NX_ARP_MAXIMUM_RETRIES_* önce toplam _ NX_ARP_MAXIMUM_RETRIES * ARP istekleri yapılır. Bir ARP yanıtı alınca, ilişkili fiziksel adres bilgileri önbellekte yer alan ARP girdisinde depolanır.

Çoklu ana bilgisayar sistemleri için NetX Duo, belirtilen hedef adrese göre ARP isteklerinin ve yanıtların gönderilecek arabirimini belirler.

> [!NOTE]
> *NetX Duo ARP yanıtını beklerken giden IP paketleri kuyruğa eklenir. Kuyruğa alınan giden IP paketlerinin sayısı, **NX_ARP_MAX_QUEUE_DEPTH.***

NetX Duo ayrıca yerel IPv4 ağının diğer düğümlerinden gelen ARP isteklerine yanıt verir. ARP isteğini alan arabirimin geçerli IP adresiyle eşleşen bir dış ARP isteği yapılırsa, NetX Duo geçerli fiziksel adresi içeren bir ARP yanıt iletisi derlemez.

Ethernet ARP isteklerinin ve yanıtlarının biçimleri Şekil 6'da gösterilmiştir ve aşağıda açıklanmıştır.

| **İstek/Yanıt &nbsp; Alanı**         | **Amaç**            |
| ---------------------------------- | ---------------------- |
| ***Ethernet Hedef Adresi*** | Bu 6 bayt alanı ARP yanıtının hedef adresini içerir ve ARP istekleri için bir yayındır (hepsi). Bu alan ağ sürücüsü tarafından ayardır. 
| ***Ethernet Kaynak Adresi***      | Bu 6 bayt alanı, ARP isteğini veya yanıtını gönderenin adresini içerir ve ağ sürücüsü tarafından ayarlanır. |
| ***Çerçeve Türü*** | Bu 2 bayt alanı, mevcut Ethernet çerçevesinin türünü içerir ve ARP istekleri ve yanıtları için bu, mevcut Ethernet çerçevesine 0x0806. Bu, ağ sürücüsünün ayarlamadan sorumlu olduğu son alandır. |
| ***Donanım Türü*** | Bu 2 bayt alanı, Ethernet'e uygun olan 0x0001 türünü içerir. |
| ***Protokol Türü*** | Bu 2-byte alanı, IP adresleri için 0x0800 protokol türünü içerir. |
| ***Donanım Boyutu*** | Bu 1 bayt alanı, Ethernet adresleri için 6 olan donanım adresi boyutunu içerir. |

![ARP Paket Biçimi diyagramı.](./media/user-guide/arp-packet-format.png)

**ŞEKIL 6. ARP Paket Biçimi**

| İstek/Yanıt &nbsp; Alanı | Amaç |
|---|---|
| ***Protokol Boyutu*** | Bu 1 bayt alanı, IP adresleri için 4 olan IP adresi boyutunu içerir. |
| ***İşlem Kodu*** | Bu 2 bayt alanı bu ARP paketi için işlemi içerir. ARP isteği, 0x0001 değeriyle belirtilirken, ARP yanıtı 0x0002. |
| ***Gönderen Ethernet Adresi*** | Bu 6 bayt alanı gönderenin Ethernet adresini içerir. |
| ***Gönderen IP Adresi*** | Bu 4 bayt alanı gönderenin IP adresini içerir. |
| ***Hedef Ethernet Adresi*** | Bu 6 bayt alanı hedefin Ethernet adresini içerir. |
| ***Hedef IP Adresi*** | Bu 4 bayt alanı hedefin IP adresini içerir. |

> [!NOTE]
> *ARP istekleri ve yanıtları Ethernet düzeyinde paketlerdir. Diğer tüm TCP/IP paketleri bir IP paket üst bilgisi tarafından kapsüllanır.*

> [!NOTE]
> *TCP/IP uygulamasındaki tüm ARP iletilerinin aynı biçimde **big endian** beklenir. Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır.*

### <a name="arp-aging"></a>ARP Eskime

NetX, otomatik dinamik ARP girişi geçersiz kılınma özelliğini destekler. ***NX_ARP_EXPIRATION_RATE** _ fiziksel eşlemeye kurulan bir IP adresinin geçerli kalma saniye sayısını belirtir. Süre dolsa da ARP girişi ARP önbelleğinden kaldırılır. Karşılık gelen IP adresine bir sonraki gönderme girişimi yeni bir ARP isteğine neden olur. _ *_NX_ARP_EXPIRATION_RATE_** değerinin sıfır olarak ayarlanıyor olması, varsayılan yapılandırma olan ARP eskime özelliğini devre dışı bırakır.

### <a name="arp-defend"></a>ARP Savunması

Bir ARP isteği veya ARP yanıt paketi alınca ve gönderen bu düğümün IP adresiyle çakışan aynı IP adresine sahip olduğunda, NetX Duo bu adres için savunma olarak bir ARP isteği gönderir. Çakışma ARP paketi 10 saniyede birden çok kez alındıktan sonra NetX Duo daha fazla savunma paketi göndermez. Varsayılan 10 saniyelik aralık * NX_ARP_DEFEND_INTERVAL **_.** Bu davranış, RFC5227'nin 2.4(c) tarihinde belirtilen ilkeyi izler. XP Windows ARP araştırmasını yanıt olarak ARP duyurusunu yoksaysa da, kullanıcı ARP yanıtını ek savunma olarak göndermek için _ *_NX_ARP_DEFEND_BY_REPLY_** tanımlayabilir.

### <a name="arp-statistics-and-errors"></a>ARP İstatistikleri ve Hataları

Etkinleştirilirse, NetX Duo ARP yazılımı uygulama için yararlı olan çeşitli istatistikleri ve hataları takip eder. Her IP'nin ARP işlemesi için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen Toplam ARP İsteği Sayısı
- Alınan Toplam ARP İsteği Sayısı
- Gönderilen Toplam ARP Yanıtları 
- Alınan Toplam ARP Yanıtları 
- Toplam ARP Dinamik Girdisi 
- Toplam ARP Statik Girdileri 
- Toplam ARP Eski Girdisi 
- Toplam ARP Geçersiz İleti sayısı 

Bu istatistiklerin ve hata raporlarının hepsi uygulamanın nx_arp_info_get ***kullanılabilir.***

## <a name="reverse-address-resolution-protocol-rarp-in-ipv4"></a>IPv4'te Ters Adres Çözümleme Protokolü (RARP)

Ters Adres Çözümleme Protokolü (RARP), ana bilgisayar 32 bit IP adreslerinin (RFC 903) ağ ataması isteğinde gerçekleştirilen protokoldür. Bu bir RARP isteği aracılığıyla yapılır ve bir ağ üyesi RARP yanıtta konak ağ arabirimine bir IP adresi atana kadar düzenli aralıklarla devam eder. Uygulama, hizmet tarafından sıfır IP ***nx_ip_create*** ip örneği oluşturur. UYGULAMA RARP'yi etkinleştirdiyse, sıfır IP adresine sahip olan arabirim üzerinden erişilebilen ağ sunucusundan bir IP adresi isteğinde etmek için RARP protokolünü kullanabilir.

### <a name="rarp-enable"></a>RARP Etkinleştirme

RARP'yi kullanmak için, uygulamanın IP örneğini sıfır IP adresiyle oluşturması ve ardından raRP'yi etkinleştirmek için ***nx_rarp_enable.*** Birden çok girişli sistemlerde, IP örneğiyle ilişkili en az bir ağ cihazı sıfır IP adresine sahip olmalıdır. RARP işlemi, ağ tarafından belirlenen IP adresiyle geçerli bir RARP yanıtı alınana kadar NetX Duo sistemi için düzenli aralıklarla BIR IP adresi gerektiren RARP istek iletileri gönderir. Bu noktada, RARP işleme tamamlanır.

RARP etkinleştirildikten sonra, tüm arabirim adresleri çözümlendikten sonra otomatik olarak devre dışı bırakılır. Uygulama, rarp'ı hizmeti kullanarak sonlandırmaya ***zor*** nx_rarp_disable.

### <a name="rarp-request"></a>RARP İsteği

RaRP istek paketinin biçimi, Şekil 6'da gösterilen ARP [paketiyle neredeyse aynıdır.](#arp-messages) Tek fark, çerçeve türü alanı 0x8035 ve  İşlem Kodu alanı 3'tür ve raRP isteği belirterek. Daha önce belirtildiği gibi, ağ tarafından atanan IP adresiyle bir RARP ***yanıtı alınana kadar*** RARP istekleri düzenli aralıklarla (her NX_RARP_UPDATE_RATE saniye) gönderilir.

> [!NOTE]
> *TCP/IP uygulamasındaki tüm RARP iletilerinin aynı biçimde **big endian** beklenir. Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır.*

### <a name="rarp-reply"></a>RARP Yanıtı

RARP yanıt iletileri ağdan alınarak bu ana bilgisayar için ağ tarafından atanan IP adresini içerir. RaRP yanıt paketinin biçimi, Şekil 6'da gösterilen ARP paketiyle neredeyse aynıdır. Tek fark, çerçeve türü alanı 0x8035 ve  İşlem Kodu alanı 4'tür ve bu da RARP yanıtını gösterir. Alındıktan sonra, IP adresi IP örneğinde ayar, düzenli RARP isteği devre dışı bırakılır ve IP örneği artık normal ağ işlemi için hazırdır.

Birden çok ana bilgisayar için IP adresi, istekte olan ağ arabirimine uygulanır. IP adresi ataması isteğinde olan başka ağ arabirimleri varsa, tüm arabirim IP adresi istekleri çözümlenene kadar düzenli RARP hizmeti devam eder.

> [!NOTE]
> *RARP işlemesi tamamlandıktan sonra uygulama IP örneğini kullanmaz. Uygulama **nx_ip_status_check** RARP tamamlanmasını beklemek için uygulamalar tarafından kullanılabilir. Birden çok girişli sistemlerde, raRP işlemesi bu arabirimde tamam olana kadar uygulama, istekte bulunduran arabirimi kullanmaz. İkincil cihaz ip adresinin durumu, nx_ip_interface_status_check **denetlenir.***

### <a name="rarp-statistics-and-errors"></a>RARP İstatistikleri ve Hataları

Etkinleştirilirse NetX Duo RARP yazılımı, uygulama için yararlı olan çeşitli istatistikleri ve hataları takip eder. Her IP'nin RARP işlemesi için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen Toplam RARP İsteği Sayısı
- Alınan Toplam RARP Yanıtları
- Toplam RARP Geçersiz İleti sayısı

Bu istatistiklerin ve hata raporlarının hepsi uygulamanın nx_rarp_info_get ***kullanılabilir.***

## <a name="internet-control-message-protocol-icmp"></a>İnternet Denetim İletisi Protokolü (ICMP)

IPv4 için İnternet Denetim İletisi Protokolü (ICMP), IP ağ üyeleri arasında hata ve denetim bilgilerini geçirmeyle sınırlıdır. IPv6 için İnternet Denetim İletisi Protokolü (ICMPv6) hata ve denetim bilgilerini de işlemektedir ve Yinelenen Adres Algılama (ELE) ve durum bilgisi olmayan adres otomatik yapılandırma gibi adres çözümleme protokolleri için gereklidir.

Diğer çoğu uygulama katmanı (örneğin, TCP/IP) iletileri gibi ICMP ve ICMPv6 iletileri de ICMP (veya ICMPv6) protokol ataması ile bir IP üst bilgisi tarafından kapsüllanır.

### <a name="icmp-statistics-and-errors"></a>ICMP İstatistikleri ve Hataları

Etkinleştirilirse NetX Duo, uygulama için yararlı olan çeşitli ICMP istatistiklerini ve hatalarını takip eder. Her IP'nin ICMP işlemesi için aşağıdaki istatistikler ve hata raporları korunur: 

- Gönderilen Toplam ICMP Ping'i  
- Toplam ICMP Ping Zaman Aşımı Sayısı 
- Toplam ICMP Ping İş Parçacığı Askıya Alındı 
- Alınan Toplam ICMP Ping Yanıtları 
- Toplam ICMP Sağlama Toplamı Hataları 
- Toplam ICMP İşsiz İleti sayısı 

Tüm bu istatistikler ve hata raporları, uygulamanın nx_icmp_info_get ***kullanılabilir.***

## <a name="icmpv4-services-in-netx-duo"></a>NetX Duo'da ICMPv4 Hizmetleri

### <a name="icmpv4-enable"></a>ICMPv4 Etkinleştirme

ICMPv4 iletilerinin NetX Duo tarafından işlenmeden önce, uygulamanın ICMPv4 ***işlemeyi etkinleştirmek için nx_icmp_enable*** hizmetine çağrı göndermesi gerekir. Bu yapıldıktan sonra, uygulama ping istekleri ve alan gelen ping paketleri gönderebilir.  

### <a name="icmpv4-echo-request"></a>ICMPv4 Yankı İsteği

Yankı isteği, genellikle ana bilgisayar IP adresiyle tanımlanan ağ üzerinde belirli bir düğümün varlığını kontrol etmek için kullanılan bir ICMPv4 ileti t t dir. Popüler ping komutu ICMP yankı isteği/yankı yanıt iletileri kullanılarak uygulanır. Belirli bir ana bilgisayar varsa, ağ yığını ping isteğini ve yanıtlarını bir ping yanıtıyla işler. Şekil 7'de ICMPv4 ping iletisi biçimi ayrıntılı olarak açık ve açık bir şekilde açık ve açık bir şekilde ve bu bilgiler yer alır.

![ICMPv4 Ping İletisi](./media/user-guide/icmpv4-ping-message.png)  

**ŞEKIL 7. ICMPv4 Ping İletisi**

> [!NOTE]
> *TCP/IP uygulamasındaki tüm ICMPv4 iletilerinin aynı biçimde **big endian** beklenir. Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır.*

Aşağıda ICMPv4 üst bilgi biçimi açıklanmıştır:

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

| Grup  | Adres   | Description  |
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
|Flow Etiketin |bir paketin ilişkilendirildiği akışı benzersiz bir şekilde tanımlamak için 20 bit alan. Sıfır değeri, paketin belirli bir akışa ait olmadığını gösterir. Bu alan, IPv4 içindeki *TOS* alanının yerini alır.|
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

Ağ üzerinde bir cihaz, tüm yönlendirici çok noktaya yayın adresine (FF01::2) bir yönlendirici istek (RS) iletisi göndererek Yönlendirici Bulma işlemini başlatabilirsiniz. Veya yönlendiricilerden düzenli ra için tüm düğüm çok noktaya yayın adresini (FF::1) bekleyebilir.

RA iletisi, o ağ için bir IPv6 adresi yapılandırmaya ilişkin ön ek bilgilerini içerir. NetX Duo'da yönlendirici istek özelliği varsayılan olarak etkindir ve _*_nx_user.h_** içinde ***NX_DISABLE_ICMPV6_ROUTER_SOLICITATION** _ yapılandırma seçeneği ayarlanarak devre dışı bırakılabilir. Router Solicitation parametrelerini ayarlama hakkında daha fazla bilgi için "NetX Duo Yükleme ve Kullanımı" bölümünde Yapılandırma Seçenekleri'ne bakın. 

***Ön Ek Bulma:*** Bir IPv6 cihazı, yönlendiriciden geçilmeden hangi hedef ana bilgisayarlara doğrudan erişil olduğunu öğrenmek için ön ek bulma kullanır. Bu bilgiler, yönlendiriciden GELEN RA iletilerinden IPv6 cihazına kullanılabilir. IPv6 cihazı, ön ek bilgilerini bir ön ek tablosunda depolar. Ön ek bulma, IPv6 cihaz ön eki tablosundan bir ön eki hedef adresle eşler. Ön ekte yer alan tüm bitler hedef adresin en önemli bitleri ile eşlese, ön ek bir hedef adresle eşler. Birden fazla ön ek bir adresi kapsıyorsa, en uzun ön ek seçilir.

### <a name="icmpv6-error-messages"></a>ICMPv6 Hata İletileri    
NetX Duo'da aşağıdaki ICMPv6 hata iletileri de kullanılabilir:  

- Hedefe Ulaşılamaz  
- Paket Çok Büyük  
- Zaman Aşıldı  
- Parametre Sorunu  

## <a name="user-datagram-protocol-udp"></a>Kullanıcı Veri Birimi Protokolü (UDP)

Kullanıcı Veri Birimi Protokolü (UDP), ağ üyeleri arasında en basit veri aktarımı formunu sağlar (RFC 768). UDP veri paketleri en iyi çabayla bir ağ üyesinden diğerine gönderilir; Örneğin, paket alıcısı tarafından onay için yerleşik bir mekanizma yoktur. Ayrıca, UDP paketi göndermek için önceden bağlantı kurulmasına gerek olmaz. Bu nedenle, UDP paket iletimi çok verimlidir.

NetX uygulamalarını NetX Duo'ya alan geliştiriciler için NetX ile NetX Duo arasındaki UDP işlevselliğinde yalnızca birkaç temel değişiklik vardır. Bunun nedeni, IPv6'nın öncelikli olarak temel IP katmanıyla ilgili olup olmadığını belirlemektir. Tüm NetX Duo UDP hizmetleri IPv4 veya IPv6 bağlantısı için kullanılabilir.

### <a name="udp-header"></a>UDP Üst Bilgisi       
UDP, iletim sırasında uygulamanın verilerine basit bir paket üst bilgisi yer alır ve alınan BIR UDP paketini uygulamaya teslimmeden önce benzer bir UDP üst bilgisini alım sırasında paketten kaldırır. UDP, paketleri göndermek ve almak için IP protokolünü kullanır, yani paket ağ üzerindeyken UDP üst bilgisi önünde bir IP üst bilgisi vardır. Şekil 12'de UDP üst bilgisi biçimi görüntülenir.

![UDP üst bilgi biçiminin diyagramı.](./media/user-guide/image21.png)

### <a name="figure-12-udp-header"></a>ŞEKIL 12. UDP Üst Bilgisi

> [!NOTE]
> *UDP/IP uygulamasındaki tüm üst big endian **beklenir.** Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır.*

Aşağıda UDP üst bilgisi biçimi açıklanmıştır:

|Üst Bilgi Alanı |Amaç |
|---|---|
|**16 bit kaynak bağlantı noktası numarası** |Bu alan, UDP paketinin gönderildiği bağlantı noktasını içerir. Geçerli UDP bağlantı noktaları 1 ile 0xFFFF. |
|**16 bit hedef bağlantı noktası numarası** |Bu alan, paketin gönderildiği UDP bağlantı noktasını içerir. Geçerli UDP bağlantı noktaları 1 ile 0xFFFF. |
|**16 bit UDP uzunluğu** |Bu alan, UDP üst bilgisi boyutu da dahil olmak üzere UDP paketinde bayt sayısını içerir. |
|**16 bit UDP sağlamaları** |Bu alan UDP üst bilgisi, paket veri alanı ve sahte IP üst bilgisi dahil olmak üzere paket için 16 bit sağlama toplamlarını içerir. |

### <a name="udp-enable"></a>UDP Etkinleştirme   
UDP paket iletiminin mümkün olması için önce uygulamanın nx_udp_enable çağırarak ***UDP'yi etkinleştirmesi*** gerekir. Etkinleştirildikten sonra, uygulama UDP paketleri gönderebilir ve almakta serbesttir.  

### <a name="udp-socket-create"></a>UDP Yuva Oluşturma    
UDP yuvaları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. İlk hizmet türü, yaşam süresi ve kuyruk derinliği, hizmet tarafından nx_udp_socket_create ***tanımlanır.*** Bir uygulamanın UDP yuvalarının sayısıyla ilgili bir sınır yoktur.

### <a name="udp-checksum"></a>UDP SağlamaLarı   
IPv6 protokolü, paket verilerinde UDP üst bilgi sağlama sayısı hesaplaması gerektirirken IPv4 protokolünde isteğe bağlıdır.  

UDP, IP sahte üst bilgisini (kaynak IP adresi, hedef IP adresi ve protokol/uzunluk IP sözcüğünden oluşan), UDP üst bilgisini ve UDP paket verilerini kapsayan 16 bitlik tamamlayıcı sağlama toplamlarını belirtir. IPv4 ve IPv6 UDP paket üst bilgisi sağlamaları arasındaki tek fark, IPv6'da 128 bit olan kaynak ve hedef IP adreslerinin IPv4'te 32 bit olmasıdır. Hesaplanan UDP sağlama toplam değeri 0 ise, hepsi (0xFFFF). Gönderen yuvada UDP sağlama toplam mantığı devre dışı bırakılmışsa, sağlama toplam hesaplaması olmadığını belirtmek için UDP sağlama toplam alanına sıfır yerleştirilir.

UDP sağlama sayısı alıcı tarafından hesaplanan sağlama sayısı ile eşlenemzse, UDP paketi basitçe atılır.

IPv4 ağına UDP sağlama verileri isteğe bağlıdır. NetX Duo, bir uygulamanın yuva başına UDP sağlama sayısı hesaplamasını etkinleştirmesini veya devre dışı bırakmasını sağlar. Varsayılan olarak UDP yuva sağlama verileri mantığı etkindir. Uygulama , * nx_udp_socket_checksum_disable _ hizmetini çağırarak belirli bir UDP yuvası için **sağlama nx_udp_socket_checksum_disable** devre dışı bırakabilirsiniz. Ancak, IPv6 ağına UDP sağlama verileri zorunludur. Bu nedenle, hizmet _ *_nx_udp_socket_checksum_disable_** IPv6 ağı üzerinden bir paket gönderirken UDP sağlama sayısı mantığını devre dışı bırakmaz.

Bazı Ethernet denetleyicileri, UDP sağlamalarını çalışır şekilde oluşturabiliyor. Sistem donanım sağlama sağlamaları hesaplama özelliğini kullanıyorsa, NetX Duo kitaplığı sağlama sağlama mantığı olmadan da kullanılabilir. UDP yazılım sağlamalarını devre dışı bırakmak için NetX Duo kitaplığının tanımlanmış şu sembollerle inşa edilmiş olması gerekir: ***NX_DISABLE_UDP_TX_CHECKSUM** _ _*_ve NX_DISABLE_UDP_RX_CHECKSUM_*_ (Bölüm 2'de açıklanmıştır). Yapılandırma seçenekleri, _ *_nx_udp_socket_checksum_disable_** hizmetini çağırarak uygulamanın yuva başına IPv4 UDP sağlama tamamı işlemeyi devre dışı bırakmasını sağlarken NetX Duo'dan UDP sağlama sağlamaları mantığını tamamen kaldırır.

### <a name="udp-ports-and-binding"></a>UDP Bağlantı Noktaları ve Bağlama      
UDP bağlantı noktası, UDP protokolünde mantıksal bir uç noktasıdır. NetX Duo'daki UDP bileşeninde 1 ile 1 arasında geçerli 65.535 bağlantı noktası 0xFFFF. UDP verilerini göndermek veya almak için uygulamanın önce bir UDP yuvası oluşturması ve ardından istenen bağlantı noktasına bağlaması gerekir. Bir UDP yuvasını bir bağlantı noktasına bağlamanın ardından uygulama bu yuvada veri gönderebilir ve bu verileri alır.

### <a name="udp-fast-pathtrade"></a>UDP Hızlı Yolu&trade;   
UDP Hızlı &trade; Yolu, NetX Duo UDP uygulaması aracılığıyla düşük paket ek yükü yolunun adıdır. UDP paketi göndermek için yalnızca birkaç işlev çağrısı gerekir: ***nx_udp_socket_send** _, _*_nx_ip_packet_send_*_ ve ağ sürücüsüne son çağrı. _*_nx_udp_socket_send_*_ NetX Duo'da mevcut NetX uygulamaları için kullanılabilir ve yalnızca IPv4 paketleri için geçerlidir. Ancak tercih edilen yöntem, aşağıda ele alınan _ *_nxd_udp_socket_send_** hizmetini kullanmaktır. UDP paket alımında, UDP paketi uygun UDP yuva alma kuyruğuna yerleştirilir veya ağ sürücüsünün alma kesme işlemeden gelen tek bir işlev çağrısında askıya alınmış bir uygulama iş parçacığına teslim edilir. UDP paketlerini göndermek ve almak için yüksek oranda iyileştirilmiş bu mantık, UDP Hızlı Yol teknolojisinin özüdür.  

### <a name="udp-packet-send"></a>UDP Paket Gönderme    
IPv6 veya IPv4 ağları üzerinden UDP verileri gönderme, * nxd_udp_socket_send _ işlevi **çağrılarak** kolayca dolar. Çağıranın, ip sürümünü _nx_ip_version parametresinin _nx_ip_version* alanında NXD_ADDRESS ayarlaması gerekir. NetX Duo, hedef IPv4/IPv6 adresine göre iletilen UDP paketleri için en iyi kaynak adresi belirler. Bu hizmet, paket verilerinin önüne bir UDP üst bilgisi yer alır ve bunu iç IP gönderme yordamını kullanarak ağa gönderir. Tüm UDP paket iletimleri hemen işlendiğinden, UDP paketleri gönderirken iş parçacığı askıya alınmaz. 

Çok noktaya yayın veya yayın hedefleri için, NetX Duo cihazında seçilecek birden çok IP adresi varsa uygulamanın kaynak IP adresini belirtmesi gerekir. Bu, aşağıdaki hizmetlerle ***nxd_udp_socket_source_send.***

> [!IMPORTANT]    
> *Çok **nx_udp_socket_send** veya yayın paketlerinin iletildiğinde kullanılırsa,* ilk etkinleştirilmiş arabirimin IP adresi kaynak adresi olarak kullanılır.

> [!NOTE] 
> Bu yuva için UDP sağlama toplama mantığı etkinleştirilirse, sağlama toplama işlemi, UDP veya IP veri yapılarına erişimi engellemeden, çağırma iş parçacığı *bağlamında gerçekleştirilir.* 

> [!WARNING]    
> *Bu yapıda bulunan UDP yükü NX_PACKET uzun sözcük sınırında yer al olmalıdır. Uygulamanın UDP, IP ve* fiziksel medya üst bilgilerini yer aldığı NetX Duo için ön uç işaretçisi ile veri başlatma işaretçisi arasında yeterli alan bırakması gerekir.

### <a name="udp-packet-receive"></a>UDP Paket Alma    
Uygulama iş parçacıkları, belirli bir yuvadan udp paketleri almak için ***nx_udp_socket_receive.*** Yuva alma işlevi, yuvanın alma kuyruğunda en eski paketi teslim ediyor. Alma kuyruğunda paket yoksa, bir paket gelene kadar çağıran iş parçacığı askıya alabilir (isteğe bağlı bir zaman aşımı ile).

UDP alma paketi işlemesi (genellikle ağ sürücüsünün alma kesme işleyicisi tarafından çağrılır), paketi UDP yuvasının alma kuyruğuna yerleştirmekten veya paketi bekleyen ilk askıya alınmış iş parçacığına teslim etmekten sorumludur. Paket kuyruğa alınıyorsa, alma işlemi yuvayla ilişkili en yüksek alma kuyruğu derinliğini de denetler. Yeni kuyruğa alınan bu paket kuyruk derinliğini aşarsa kuyrukta en eski paket atılır.

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

1) TCP paketi IPsec işlemine tabi yoksa, ağ arabirimi donanımı sağlama toplamlarını hesaplar. Bu nedenle TCP modülü sağlama toplamlarını hesaplamayı denemez;

2) IPsec paketi yüklüyse ve TCP paketi IPsec sürecine tabiyse, TCP modülü paketi IPsec katmanına göndermeden önce yazılımda sağlama toplamlarını hesaplar.

### <a name="tcp-port"></a>TCP Bağlantı Noktası     
TCP bağlantı noktası, TCP protokolünde bir mantıksal bağlantı noktasıdır. NetX Duo'daki TCP bileşeninde 1 ila 1 arasında geçerli 65.535 bağlantı noktası 0xFFFF. Bir bağlantı noktası üzerinden diğer hedef bağlantı noktalarına veri gönderilemenin mümkün olduğu UDP'den farklı olarak, bir TCP bağlantı noktası başka bir tcp bağlantı noktasına bağlanır ve yalnızca bu bağlantı kurulup herhangi bir veri aktarımı edekler ve yalnızca bağlantıyı yapan iki bağlantı noktası arasında yer alır.

> [!IMPORTANT]
> *TCP bağlantı noktaları UDP bağlantı noktalarından tamamen ayrıdır; örneğin, 1 numaralı UDP* bağlantı noktasının 1 numaralı TCP bağlantı noktasıyla hiçbir ilişkisi yoktur.

### <a name="client-server-model"></a>Client-Server Modeli     
Veri aktarımı için TCP kullanmak üzere, önce iki TCP yuvası arasında bir bağlantı kurulacak. Bağlantının kurulması istemci-sunucu olarak yapılır. Bağlantının istemci tarafı bağlantıyı başlatan taraftır, sunucu tarafı ise herhangi bir işlem yapılmadan önce istemci bağlantı isteklerini bekler.

> [!IMPORTANT]
> *Çoklu giriş cihazları için NetX Duo, bağlantı için kaynak adresi ve bağlantının hedef IP adresine göre sonraki atlama adresini otomatik olarak belirler. TCP, paketleri tek* noktaya yayın (örneğin, yayın dışı) hedef adreslere göndermekle sınırlı olduğundan, NetX Duo kaynak IPv6 adresini seçmek için bir "ipucu" gerektirmez.

### <a name="tcp-socket-state-machine"></a>TCP Yuva Durumu Makinesi      
İki TCP yuvası (bir istemci ve bir sunucu) arasındaki bağlantı karmaşıktır ve durum makinesiyle yönetilir. Her TCP yuvası KAPALI durumda başlar. Bağlantı olayları aracılığıyla her yuvanın durum makinesi, TCP'de toplu veri aktarımının bulunduğu ESTABLISHED durumuna geçirilir. Bağlantının bir tarafı artık veri göndermek isterse bağlantının bağlantısı kesi. Diğer taraf bağlantı kesildikten sonra TCP yuvası kapatılan durumuna döner. Tcp istemcisi ve sunucusu bir bağlantıyı her kurduğunda ve kapatıyorken bu işlem yineler. Şekil 14'te TCP durum makinesinin çeşitli durumları gösterir.

### <a name="tcp-client-connection"></a>TCP İstemci Bağlantısı       
Daha önce belirtildiği gibi, TCP bağlantısının istemci tarafı bir TCP sunucusuna bağlantı isteği başlatıyor. Bağlantı isteği gelemeden önce istemci IP örneğinde TCP'nin etkinleştirilmesi gerekir. Ayrıca, istemci TCP yuvası daha sonra * nx_tcp_socket_create _ hizmetiyle **oluşturulacak** ve _ nx_tcp_client_socket_bind * hizmeti aracılığıyla bir *_bağlantı noktasına_* bağlanacak.

İstemci yuvası bağlandıktan sonra, ***nxd_tcp_client_socket_connect*** hizmeti TCP sunucusuyla bağlantı kurmak için kullanılır. Bağlantı denemesi başlatmak için yuvanın KAPALI durumda olması gerektiğini unutmayın. Bağlantının kurulması, NetX Duo'nun bir SYN paketi vermesi ve sunucudan syn ACK paketi beklemesi ile başlar. Bu da bağlantı isteğinin kabul olduğunu gösterir. SYN ACK alındıktan sonra NetX Duo bir ACK paketiyle yanıt verir ve istemci yuvayı ESTABLISHED durumuna yükselter.

![TCP durum makinesinin durumlarının diyagramı.](./media/user-guide/image24.png)   

**ŞEKIL 14. TCP Durum Makinesi durumları**


> [!WARNING]
> *Uygulamalar, **IPv4 nxd_tcp_client_socket_connect** IPv6 TCP bağlantıları için bir ağ arabirimi kullansın. Uygulamalar, IPv4 TCP **nx_tcp_client_socket_connect*** için nx_tcp_client_socket_connect kullanmaya devam eder, ancak sonunda nxd_tcp_client_socket_connect kullanım dışı nx_tcp_client_socket_connect geliştiricilerin bu bağlantıları kullanmaları teşvik edilecektir.

*Benzer şekilde, **nxd_tcp_socket_peer_info_get** IPv4 veya IPv6 TCP bağlantılarıyla çalışır. Ancak, **nx_tcp_socket_peer_info_get** eski uygulamalar için hala kullanılabilir. Geliştiricilerin, daha  sonra nxd_tcp_socket_peer_info_get kullanmaları teşvik edilecektir.*

### <a name="tcp-client-disconnection"></a>TCP İstemci bağlantısının kesilmesi    
Bağlantının kapatılması, ***nx_tcp_socket_disconnect.*** Askıya alma belirtilmezse, istemci yuvası sunucu yuvasına bir RST paketi gönderir ve yuvayı KAPALI durumuna gönderir. Aksi takdirde, bir askıya alma istenecekse, tam TCP bağlantı kesme protokolü aşağıdaki gibi gerçekleştirilir: 

- Sunucu daha önce bir bağlantı kesme isteği başlattı ise (istemci yuvası zaten bir FIN paketi aldı, ACK ile yanıt verdi ve CLOSE WAIT durumda), NetX Duo istemci TCP yuva durumunu LAST ACK durumuna yükselter ve bir FIN paketi gönderir. Ardından bağlantıyı kesmeyi tamamlamadan ve KAPALI durumuna girmeden önce sunucudan bir ACK bekler.

- Öte yandan, bağlantı kesme isteğini başlatan ilk istemci istemci ise (sunucu bağlantısı kesildi ve yuva hala ESTABLISHED durumda), NetX Duo bağlantıyı başlatmak için bir FIN paketi gönderir ve bağlantıyı tamamladıktan ve yuvayı KAPALI bir durumda yerleştirmeden önce sunucudan BIR FIN ve ACK almak için bekler.

Yuva iletme kuyruğunda hala paketler varsa NetX Duo, paketlerin kabul askıya alınması için belirtilen zaman aşımını askıya alır. Zaman aşımı süresi dolsa NetX Duo, istemci yuvasının iletme kuyruğundan boşaltılır. 

Uygulama, bağlantı noktasını istemci yuvasından çıkararak ***nx_tcp_client_socket_unbind.*** Yuva kapatılan bir durumda veya bağlantı noktası serbest bırakılamadan önce bağlantıyı kesme sürecinde (yani TIMED WAIT durumu) olması gerekir; aksi takdirde bir hata döndürülür.

Son olarak, uygulamanın artık istemci yuvasına ihtiyacı yoksa, ***yuvayı nx_tcp_socket_delete*** için uygulama çağrılır.

### <a name="tcp-server-connection"></a>TCP Sunucusu Bağlantısı      
TCP bağlantısının sunucu tarafı pasiftir; Diğer bir ifadeyle, sunucu bir istemcinin bağlantı isteğini başlatması için bekler. bir istemci bağlantısını kabul etmek için, TCP ilk olarak * nx_tcp_enable _ hizmeti çağrılarak IP **örneğinde etkinleştirilmelidir.** Ardından, uygulamanın _ nx_tcp_socket_create * hizmetini kullanarak bir TCP *_yuvası_* oluşturması gerekir.  

Sunucu yuvasının bağlantı isteklerini dinlemek için de ayarlanmış olması gerekir. Bu, nx_tcp_server_socket_listen ***hizmeti kullanılarak*** elde edilir. Bu hizmet sunucu yuvayı LISTEN durumuna yer verir ve belirtilen sunucu bağlantı noktasını yuvaya bağlar.

> [!NOTE] 
> *Yuva dinleme geri çağırma yordamını ayarlamak için uygulama, nx_tcp_server_socket_listen hizmetinin tcp_listen_callback için **uygun geri çağırma işlevini** belirtir. Bu uygulama geri çağırma işlevi daha sonra bu sunucu bağlantı noktası üzerinde yeni bir bağlantı isten her istensin NetX Duo tarafından yürütülür. Geri çağırmada işlem uygulama denetimi altındadır.*

Uygulama, istemci bağlantı isteklerini kabul etmek için ***** nx_tcp_server_socket_accept _ hizmetini çağırıyor. Sunucu yuvası, dinleme veya SYN RECEIVED (SYN RECEIVED) durumda (yani sunucu LISTEN durumda ve bağlantı isteğinde olan istemciden bir SYN paketi aldı) kabul hizmetini çağıran bir SYN paketine sahip olması gerekir. *___* nx_tcp_server_socket_accept * kaynağından başarılı bir dönüş durumu, bağlantının ayar olduğunu ve sunucu yuvasının ESTABLISHED durumunda olduğunu gösterir.

Sunucu yuvasının geçerli bir bağlantısı olduktan sonra, ek istemci bağlantısı istekleri listen_queue_size tarafından belirtilen derinliğe kadar kuyruğa nx_tcp_server_socket_listen _  * **hizmetine** geçiriliyor. Bir sunucu bağlantı noktası üzerinde sonraki bağlantıları işlemesi için, uygulamanın kullanılabilir bir yuvayla (yani KAPALI durumdaki bir yuva) _ *_nx_tcp_server_socket_relisten_** çağrısında olması gerekir. Yuvayla ilişkilendirilmiş önceki bağlantı artık bitti ve yuva KAPALI durumda olursa aynı sunucu yuvasının kullanıla bile olduğunu unutmayın.

### <a name="tcp-server-disconnection"></a>TCP Sunucusu Bağlantısını Kesme     
Bağlantının kapatılması, ***nx_tcp_socket_disconnect.*** Askıya alma belirtilmezse, sunucu yuvası istemci yuvasına bir RST paketi gönderir ve yuvayı KAPALI durumuna gönderir. Aksi takdirde, bir askıya alma istenecekse, tam TCP bağlantı kesme protokolü aşağıdaki gibi gerçekleştirilir:

- İstemci daha önce bir bağlantı kesme isteği başlattı ise (sunucu yuvası zaten bir FIN paketi aldı, ACK ile yanıt verdi ve CLOSE WAIT durumda), NetX Duo TCP yuva durumunu LAST ACK durumuna yükselter ve bir FIN paketi gönderir. Ardından bağlantıyı kesmeyi tamamlamadan ve KAPALI durumuna girmeden önce istemciden bir ACK bekler.

- Diğer taraftan, bağlantı kesme isteğini ilk başlatan sunucu ise (istemci bağlantısı kesildi ve yuva hala ESTABLISHED durumda), NetX Duo bağlantıyı başlatmak için bir FIN paketi gönderir ve bağlantıyı tamamladıktan ve yuvayı KAPALI durumuna yerleştirmeden önce istemciden BIR FIN ve ACK almak için bekler.

Yuva iletme kuyruğunda hala paketler varsa, NetX Duo bu paketlerin kabul askıya alınması için belirtilen zaman aşımını askıya alır. Zaman aşımı süresi dolsa NetX Duo, sunucu yuvasının iletme kuyruğundan boşaltıyor.

Bağlantı kesme işlemi tamamlandıktan ve sunucu yuvası KAPALI durumda olduktan sonra, uygulamanın bu yuvanın sunucu bağlantı noktasıyla olan ilişkilendirmeyi sona nx_tcp_server_socket_unaccept **_** hizmetini çağırmış olması gerekir. Hata durumu döndürürken bu hizmetin uygulama tarafından _*_çağrıl nx_tcp_socket_disconnect_*_ _*_nx_tcp_server_socket_accept_*_ gerektiğini unutmayın. Yuva _*_nx_tcp_server_socket_unaccept_*_ sonra yuva istemci veya sunucu yuvası olarak kullanılabilir, hatta artık gerekli olmadığı sürece silinebilir. Aynı sunucu bağlantı noktası üzerinde başka bir istemci bağlantısı kabul etmek istenirse, _ *_nx_tcp_server_socket_relisten_** hizmeti bu yuvada çağrılır.

Aşağıdaki kod kesimi tipik bir TCP sunucusunun kullandığı çağrı dizisini gösterir:

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

### <a name="mss-validation"></a>MSS Doğrulaması      
En Büyük Kesim Boyutu (MSS), bir TCP ana bilgisayarının temel ALıNAN IP katmanı tarafından parçalanmadan aldırıla maksimum bayt miktarıdır. TCP bağlantısı kurulması aşamasında her iki uç da kendi TCP MSS değerini değiştirmektedir, böylece gönderen alıcının MSS değerinden daha büyük bir TCP veri kesimi göndermez. NetX Duo TCP modülü, bağlantı kurmadan önce isteğe bağlı olarak eş tarafından tanıtılan MSS değerini doğrular. Varsayılan olarak NetX Duo böyle bir denetimi etkinleştirmez. MSS doğrulaması gerçekleştirmek isteyen uygulamalar NetX Duo **NX_ENABLE_TCP_MSS_CHECK** oluşturmada * NX_ENABLE_TCP_MSS_CHECK _ tanımlamalı ve en düşük değer _*_NX_TCP_MSS_MINIMUM._*_ _ NX_TCP_MSS_MINIMUM * altında MSS *_değerlerine sahip_* gelen TCP bağlantıları bırakılır.

### <a name="stop-listening-on-a-server-port"></a>Sunucu Bağlantı Noktası Üzerinde Dinlemeyi Durdurma    
Uygulama artık * nx_tcp_server_socket_listen _ hizmetine yapılan bir çağrıyla belirtilen bir sunucu bağlantı noktası üzerinde istemci bağlantı isteklerini dinlemek isterse, uygulama yalnızca _ **nx_tcp_server_socket_unlisten****_hizmetini_* çağırarak. Bu hizmet, bağlantı için bekleyen tüm yuvaları KAPATILI durumuna döndürür ve kuyruğa alınan tüm istemci bağlantı isteği paketlerini serbest bırakmıştır. 

### <a name="tcp-window-size"></a>TCP Pencere Boyutu   
Bağlantının hem kurulum hem de veri aktarımı aşamaları sırasında, her bağlantı noktası işleyenin pencere boyutu olarak adlandırılan veri miktarını raporlar. Veriler alınarak işlendikten sonra bu pencere boyutu dinamik olarak ayarlanır. TCP'de bir gönderici yalnızca alıcının penceresine sığacak miktarda veri gönderebilir. Pencere boyutu, bağlantının her yönünde veri aktarımı için akış denetimi sağlar.   

### <a name="tcp-packet-send"></a>TCP Paket Gönderme     
TCP verilerini göndermek, nx_tcp_socket_send ***işlevi çağrılarak kolayca*** gerçekleştirebilirsiniz. İletilen verilerin boyutu yuvanın MSS değerinden veya geçerli eş alma penceresi boyutundan büyükse (hangisi daha küçükse), TCP iç mantığı iletim için en düşük değere (MSS, eş alma Penceresi) sığan verileri atlar. Bu hizmet daha sonra paketin önünde bir TCP üst bilgisi (sağlama toplam hesaplaması dahil) derler. Alıcının pencere boyutu sıfıra yakınsa, çağıranı alıcı pencere boyutunu doldurmak için mümkün olan en fazla veri gönderir. Alma penceresi sıfır olursa, çağıranı askıya alabilir ve alıcının pencere boyutunun bu paketin göndernebilecek kadar artmasını bekleyebilir. Herhangi bir zamanda, aynı yuva üzerinden veri göndermeye çalışırken birden çok iş parçacığı askıya alabilir. 

> [!WARNING]  
> *Bu yapıda bulunan TCP NX_PACKET uzun sözcük sınırında yer ala olmalıdır. Ayrıca, TCP, IP ve fiziksel* medya üst bilgilerini yer için ön uç işaretçisi ile veri başlatma işaretçisi arasında yeterli alan olmalıdır.

### <a name="tcp-packet-retransmit"></a>TCP Paketi Yeniden Iletim      
Önceden iletilen TCP paketleri aslında bağlantının diğer tarafından bir ACK döndürülene kadar dahili olarak depolanır. İletilen veriler zaman aşımı süresi içinde onaylanmazsa, depolanan paket yeniden gönderilir ve sonraki zaman aşımı süresi ayarlanır. Bir ACK geldiğinde, iç iletme kuyruğunda onay numarası kapsamındaki tüm paketler son olarak serbest bırakıldı.  

> [!WARNING]   
> Uygulama, nx_tcp_socket_send() işleviyle birlikte döndürdikten sonra paketi yeniden kullanmamalıdır veya *NX_SUCCESS. İletilen paket, veriler diğer uç tarafından onaylandıktan* sonra NetX Duo iç işleme tarafından serbest bırakıldı.

### <a name="tcp-keepalive"></a>TCP Keepalive     
TCP Keepalive özelliği, bir yuvanın uygun sonlandırma olmadan eş bağlantısının kesilip kesilmemesi (örneğin, eş kilitlenmesi) veya belirli ağ izleme olanaklarının uzun süre boşta kalma süresiyle bağlantıyı sonlandırmasını önlemesini sağlar. TCP Keepalive, düzenli aralıklarla verisi olan bir TCP çerçevesi göndererek çalışır ve dizi numarası geçerli dizi numarasından bir küçük olarak ayarlanır. Bu tür TCP Keepalive çerçevesini alan alıcı, hala canlıysa geçerli sıra numarası için bir ACK ile yanıtlar. Bu, süreklilik işlemini tamamlar.  

Varsayılan olarak, keepalive özelliği etkin değildir. Bu özelliği kullanmak için NetX Duo kitaplığı * NX_ENABLE_TCP_KEEPALIVE **_** tanımlı olarak eklanmalıdır. _ *_NX_TCP_KEEPALIVE_INITIAL_** simgesi, tutma çerçevesinin başlatıldığı saniye sayısını belirtir.  

### <a name="tcp-packet-receive"></a>TCP Paketi Alma   
TCP alma paketi işleme (IP yardımcı iş parçacığından çağrılır) çeşitli bağlantı ve bağlantı kesme eylemlerini işlemenin yanı sıra onay iletme işleminin işlenmesinden sorumludur. Ayrıca, TCP alma paketi işleme, alma verilerine sahip paketleri uygun TCP yuvasının alma kuyruğuna yerleştirmekten veya paketi bekleyen ilk askıya alınmış iş parçacığına teslim etmekten sorumludur.

### <a name="tcp-receive-notify"></a>TCP Alma Bildirimi     
Uygulama iş parçacığının birden fazla yuvadan alınan verileri işlemesi gerekirse, ***nx_tcp_socket_receive_notify*** işlevi kullanılmalıdır. Bu işlev yuva için bir alma paketi geri çağırma işlevini kaydedmektedir. Yuvada bir paket alınan her zaman, geri çağırma işlevi yürütülür.  

Geri çağırma işlevinin içeriği applicationspecific'tir; ancak, işlev büyük olasılıkla işleme iş parçacığına karşılık gelen yuvada bir paketin kullanılabilir olduğunu bildirmek için mantık içerir. 

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma      
Daha önce belirtildiği gibi, uygulama iş parçacıkları belirli bir TCP bağlantı noktası üzerinden veri almaya çalışırken askıya alabilir. Bu bağlantı noktası üzerinde bir paket alındıktan sonra, askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı daha sonra devam eder. Çoğu NetX Duo hizmeti için kullanılabilen bir özellik olan TCP alma paketi üzerinde askıya alma sırasında isteğe bağlı bir zaman aşımı mevcuttur.  

İş parçacığı askıya alma, bağlantı (hem istemci hem de sunucu), istemci bağlama ve bağlantı kesme hizmetleri için de kullanılabilir.  

### <a name="tcp-socket-statistics-and-errors"></a>TCP Yuvası İstatistikleri ve Hataları     
Etkinleştirilirse, NetX Duo TCP yuva yazılımı uygulama için yararlı olan çeşitli istatistikleri ve hataları takip eder. Her IP/TCP örneği için aşağıdaki istatistikler ve hata raporları korunur:   

- Gönderilen Toplam TCP Paketleri  
- Gönderilen Toplam TCP Bayt Sayısı  
- Alınan Toplam TCP Paketleri   
- Alınan Toplam TCP Bayt Sayısı   
- Toplam TCP Geçersiz Paketleri   
- Bırakılan Toplam TCP Alma Paketleri    
- Toplam TCP Alma Sağlama Toplamı Hataları   
- Toplam TCP Bağlantısı   
- Toplam TCP Bağlantısı Kesileri   
- Bırakılan Toplam TCP Bağlantısı    
- Toplam TCP Paketi Yeniden Aktarım Sayısı   
- Gönderilen TCP Yuva Paketleri   
- Gönderilen TCP Yuva Bayt sayısı   
- Alınan TCP Yuva Paketleri   
- Alınan TCP Yuva Baytları   
- TCP Yuva Paketi Yeniden Aktarımları    
- Kuyruğa Alınan TCP Yuva Paketleri    
- TCP Yuvası Sağlama Sayısı Hataları    
- TCP Yuva Durumu    
- TCP Yuva İletim Kuyruğu Derinliği    
- TCP Yuva İletme Penceresi Boyutu    
- TCP Yuvası Alma Penceresi Boyutu    

Tüm bu istatistikler ve hata raporları, toplam TCP istatistikleri için * nx_tcp_info_get _ hizmeti **ve** yuva başına TCP istatistikleri için _ *_nx_tcp_socket_info_get_** hizmeti ile uygulamada kullanılabilir.

### <a name="tcp-socket-control-block-nx_tcp_socket"></a>TCP Yuva Denetim Bloğu NX_TCP_SOCKET      
Her TCP yuvasının özellikleri, IP *veri* yapısına bağlantı, ağ bağlantı arabirimi, bağlı bağlantı noktası ve alma paketi kuyruğu gibi yararlı bilgiler içeren ilişkili NX_TCP_SOCKET denetim bloğunda bulunur. Bu yapı, ***nx_api.h dosyasında*** tanımlanır.

## <a name="tcpip-offload"></a>TCP/IP Boşaltma
Bu özellik, NetX Duo'ya donanım üzerinde TCP/IP hizmeti sunan ağ arabirimi kartını desteklemesini sağlar. Bazı WiFi modülleri modülde TCP/IP işleme sunar ve MCU'da uygulamalar, TCP/IP yığınına erişmek için API'ler aracılığıyla paketleri gönderir ve alır. Bu özellik etkinleştirildiğinde, geliştiriciler yerel NetX Duo uygulamalarını doğrudan çalıştırabilirsiniz.

TCP/IP yük boşaltma özelliğini etkinleştirmek için NetX Duo ile birlikte ve `NX_ENABLE_TCPIP_OFFLOAD` `NX_ENABLE_INTERFACE_CAPABILITY` tanımlanmalıdır.

### <a name="tcpip-offload-handler"></a>TCP/IP Yük Boşaltma İşleyicisi
NetX Duo, TCP veya UDP yuva işlemlerini işlemek için bir geri çağırma işlevi aracılığıyla ağ sürücüsüyle iletişim kurar. Geri çağırma işlevi içinde `NX_INTERFACE_STRUCT` tanımlanır. Ağ sürücüsünün sürücü komutu sırasında TCP/IP geri çağırma işlevini `NX_LINK_ENABLE` ayarlaması gerekir. TCP/IP geri çağırma işlevinin prototipi aşağıdaki gibidir.

``` C
UINT (*nx_interface_tcpip_offload_handler)(struct NX_IP_STRUCT *ip_ptr,
                                           struct NX_INTERFACE_STRUCT *interface_ptr,
                                           VOID *socket_ptr, UINT operation, NX_PACKET *packet_ptr,
                                           NXD_ADDRESS *local_ip, NXD_ADDRESS *remote_ip,
                                           UINT local_port, UINT *remote_port, UINT wait_option);
```
Parametrelerin açıklaması.
* `ip_ptr` - IP örneğine işaretçi
* `interface_ptr` - Arabirim işaretçisi
* `socket_ptr` - veya `NX_TCP_SOCKET` `NX_UDP_SOCKET` işaretçisi değerine bağlıdır `operation`
* `operation` - Geçerli işlev çağrısının işlemi. Değerler aşağıda olduğu gibi tanımlanmıştır
``` C
#define NX_TCPIP_OFFLOAD_TCP_CLIENT_SOCKET_CONNECT  0
#define NX_TCPIP_OFFLOAD_TCP_SERVER_SOCKET_LISTEN   1
#define NX_TCPIP_OFFLOAD_TCP_SERVER_SOCKET_ACCEPT   2
#define NX_TCPIP_OFFLOAD_TCP_SERVER_SOCKET_UNLISTEN 3
#define NX_TCPIP_OFFLOAD_TCP_SOCKET_DISCONNECT      4
#define NX_TCPIP_OFFLOAD_TCP_SOCKET_SEND            5
#define NX_TCPIP_OFFLOAD_UDP_SOCKET_BIND            6
#define NX_TCPIP_OFFLOAD_UDP_SOCKET_UNBIND          7
#define NX_TCPIP_OFFLOAD_UDP_SOCKET_SEND            8
```
* `packet_ptr` - Paket işaretçisi. değeri veya olduğunda `operation` `TCP_SOCKET_SEND` ayarlanır `UDP_SOCKET_SEND`
* `local_ip` - Yerel IP adresi işaretçisi. Değer şu olduğunda `operation` ayarlanır: `UDP_SOCKET_SEND`
* `remote_ip` - Uzak IP adresi işaretçisi. değeri veya olduğunda `operation` `TCP_CLIENT_SOCKET_CONNECT` `UDP_SOCKET_SEND` ayarlanır. İşlem `TCP_SERVER_SOCKET_ACCEPT` olduğunda, bu değer geri çağırma işlevi tarafından döndürülmeli
* `local_port` - Yerel bağlantı noktası. Değer , `operation` , `TCP_CLIENT_SOCKET_CONNECT` veya UDP olduğunda `TCP_SERVER_SOCKET_LISTEN` `TCP_SERVER_SOCKET_ACCEPT` `TCP_SERVER_SOCKET_UNLISTEN` ayarlanır
* `remote_port` - Uzak bağlantı noktası. değeri veya olduğunda `operation` `TCP_CLIENT_SOCKET_CONNECT` `UDP_SOCKET_SEND` ayarlanır. İşlem `TCP_SERVER_SOCKET_ACCEPT` olduğunda, bu değer geri çağırma işlevi tarafından döndürülmeli
* `wait_option` - Tıklar içinde bekleme seçeneği. Değer tüm işlemler için ayarlanır

### <a name="tcpip-offload-context"></a>TCP/IP Yük Boşaltma Bağlamı
`NX_TCP_SOCKET`TCP/IP yük boşaltma sürücüsü tarafından kullanılacak yapıya bir işaretçi eklenir.
```
typedef struct NX_TCP_SOCKET_STRUCT
{
    // ...

    /* This pointer is designed to be accessed by TCP/IP offload directly.  */
    VOID *nx_tcp_socket_tcpip_offload_context;
} NX_TCP_SOCKET;
```

`NX_UDP_SOCKET`TCP/IP yük boşaltma sürücüsü tarafından kullanılacak yapıya bir işaretçi eklenir.
```
typedef struct NX_UDP_SOCKET_STRUCT
{
    // ...

    /* This pointer is designed to be accessed by TCP/IP offload directly.  */
    VOID *nx_udp_socket_tcpip_offload_context;
} NX_UDP_SOCKET;
```

### <a name="apis-for-tcpip-offload-network-driver"></a>TCP/IP Yük Boşaltma Ağ Sürücüsü API'leri
``` C
/* Invoked when TCP packet is receive or connection error.  */
VOID _nx_tcp_socket_driver_packet_receive(NX_TCP_SOCKET *socket_ptr, NX_PACKET *packet_ptr);

/* Invoked when TCP connection is establish.  */
UINT _nx_tcp_socket_driver_establish(NX_TCP_SOCKET *socket_ptr, NX_INTERFACE *interface_ptr, UINT remote_port);

/* Invoked when UDP packet is receive.  */
VOID _nx_udp_socket_driver_packet_receive(NX_UDP_SOCKET *socket_ptr, NX_PACKET *packet_ptr,
                                          NXD_ADDRESS *local_ip, NXD_ADDRESS *remote_ip, UINT remote_port);
```
### <a name="tcpip-offload-driver"></a>TCP/IP Yük Boşaltma Sürücüsü
Her IP arabirimi için bir sürücü işlevi gerekir. NetX Duo sürücü işlevlerini geliştirme hakkında daha fazla bilgi için [5.](chapter5.md#tcpip-offload-driver-guidance) Bölüm'e bakın.

### <a name="tcpip-offload-known-limitations"></a>TCP/IP Yük Boşaltma Bilinen Sınırlamaları
- Yalnızca TCP ve UDP yuvaları de destekler
- DHCP genellikle NetX Duo tarafından değil, az kullanılan TCP/IP yığınıyla yapılır
- Altta yer alan TCP/IP yığınına ilişkin diğer sınırlamalar