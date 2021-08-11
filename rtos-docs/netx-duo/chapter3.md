---
title: Bölüm 3 - NetX Duo Azure RTOS İşlevsel Bileşenleri
description: Bu bölümde NetX Duo TCP/IP yığınının işlevsel Azure RTOS yüksek performanslı bağlantıların açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 32af483db1f97b45bfe3d334b8c79d984dedc8470a37ce1d4164331549b6954c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116789057"
---
# <a name="chapter-3---functional-components-of-azure-rtos-netx-duo"></a>Bölüm 3 - NetX Duo Azure RTOS İşlevsel Bileşenleri

Bu bölümde NetX Duo TCP/IP yığınının işlevsel Azure RTOS yüksek performanslı bağlantıların açıklaması yer almaktadır. 

## <a name="execution-overview"></a>Yürütmeye Genel Bakış

NetX Duo uygulaması içinde beş tür program yürütme vardır: başlatma, uygulama arabirimi çağrıları, iç IP iş parçacığı, IP düzenli süre önceleri ve ağ sürücüsü.

> [!NOTE]
> *NetX Duo, ThreadX'in var olduğunu varsayıyor ve iş parçacığı yürütme, askıya alma, düzenli süreler ve karşılıklı dışlama tesislerine bağlıdır.*

### <a name="initialization"></a>Başlatma

Başka bir NetX Duo **nx_system_initialize** çağrılmadan önce hizmet * nx_system_initialize _ çağrısı gerekir. Sistem başlatma, ThreadX _ tx_application_define **_işlevinden_* veya uygulama iş parçacıklarından çağrılebilir.

***nx_system_initialize** _ döndürdikten sonra sistem paket havuzları ve IP örnekleri oluşturmak için hazırdır. BIR IP örneği oluşturmak için varsayılan paket havuzu gerekli olduğundan, IP örneği oluşturmadan önce en az bir NetX Duo paket havuzu mevcut olması gerekir. Paket havuzları ve IP örnekleri oluşturma, ThreadX başlatma işlevinden _ *_tx_application_define_** ve uygulama iş parçacıklarından izin verilir.

Dahili olarak, bir IP örneği oluşturma iki bölümde yapılır: İlk bölüm, çağrıyı yapanın bağlamından veya tx_application_define iş parçacığının bağlamından yapılır.  Buna IP veri yapısını ayarlama ve iç IP iş parçacığı da dahil olmak üzere çeşitli IP kaynakları oluşturma dahildir. İkinci bölüm, iç IP iş parçacığından ilk yürütme sırasında gerçekleştirilir. BURADA, IP oluşturmanın ilk bölümü sırasında sağlanan ağ sürücüsüne ilk çağrılır. İç IP iş parçacığından ağ sürücüsünün çağrılarak sürücünün başlatma işlemi sırasında I/O gerçekleştirmesi ve askıya alınmasına olanak sağlar.

Ağ sürücüsü başlatma işlemeden döndüğünde IP oluşturma işlemi tamamlanır.

NetX Duo'da IPv6'yı başlatma için birkaç ek NetX Duo hizmeti gerekir. Bunlar, bu bölümün ilerleyen kısımlarında [NetX Duo'daki IPv6](#ipv6-in-netx-duo) bölümünde daha ayrıntılı olarak açıklanmıştır.

> [!NOTE]
> *NetX Duo hizmeti **nx_ip_status_check** IP örneği ve birincil arabirim durumu hakkında bilgi almak için kullanılabilir. Bu tür durum bilgileri, bağlantının başlatılmış, etkin ve IP adresinin çözümlenmiş olup olmadığını içerir. Bu bilgiler, yeni oluşturulan bir IP örneğini kullanmak zorunda olan uygulama iş parçacıklarını eşitlemek için kullanılır. Birden çok girişli sistemler için bkz. [Çoklu Giriş Desteği.](#multihome-support) **nx_ip_interface_status_check** arabirimde 3information elde etmek için kullanılabilir.*

### <a name="application-interface-calls"></a>Uygulama Arabirimi Çağrıları

Uygulama çağrıları büyük ölçüde ThreadX RTOS altında çalışan uygulama iş parçacıklarından yapılır. Ancak, bazı başlatma, oluşturma ve etkinleştirme hizmetleri ***tx_application_define.*** [Bölüm 4 - NetX Duo Services'Azure RTOS](chapter4.md) açıklaması'nın "İzin VerilenLer" bölümleri, her NetX Duo hizmetinin hangi hizmetlerden çağrıl çağrıl olduğunu belirtmektedir.

Çoğu durumda, sağlama sağlamaları hesaplama gibi yoğun etkinlikler, diğer iş parçacıklarının IP örneğine erişimini engellemeden çağıran iş parçacığının bağlamında yapılır. Örneğin, iletimde UDP sağlama sayısı hesaplaması*nx_udp_socket_send _ hizmeti içinde, temel ALıNAN IP gönderme işlevi çağrıldan önce gerçekleştirilir. Alınan bir pakette UDP sağlama toplam değeri, uygulama *_iş parçacığında yürütülen_* _ nx_udp_socket_receive * hizmette hesaplanır. Bu, düşük öncelikli iş parçacıklarında yoğun sağlamam hesaplaması nedeniyle yüksek öncelikli iş parçacıklarının ağ isteklerinin duraklamasını önlemeye yardımcı olur.

IP adresleri ve bağlantı noktası numaraları gibi değerler, konak bayt sırasına göre API'lere geçirildi. Dahili olarak bu değerler de konak bayt sırasına göre depolanır. Bu, geliştiricilerin değerleri bir hata ayıklayıcısı aracılığıyla kolayca görüntülemelerini sağlar. Bu değerler iletim için bir çerçevede programlanmışsa, ağ baytı sırasına dönüştürülür.

### <a name="internal-ip-thread"></a>İç IP İş Parçacığı

Daha önce belirtildiği gibi, NetX Duo'daki her IP örneğinin kendi iş parçacığı vardır. İç IP iş parçacığının öncelik ve yığın boyutu, nx_ip_create ***tanımlanır.*** İç IP iş parçacığı yürütmeye hazır modda oluşturulur. IP iş parçacığı, çağıran iş parçacığından daha yüksek önceliğe sahipse, IP oluşturma çağrısının içinde önme oluşabilir.

İç IP iş parçacığının giriş noktası , _ veya iç ***işlevinde nx_ip_thread_entry.*** İlk kez, iç IP iş parçacığı ilk olarak uygulamaya özgü ağ sürücüsüne üç çağrı yapmadan oluşan ağ sürücüsü başlatmayı tamamlar. İlk çağrı, ağ sürücüsünü IP örneğine eklemek ve ardından ağ sürücüsünün başlatma işleminin üzerinden geçerek bir başlatma çağrısı yapmaktır. Ağ sürücüsü başlatmadan döndükten sonra (donanımın düzgün şekilde ayarlanmış olması beklerken askıya alabilir), iç IP iş parçacığı bağlantıyı etkinleştirmek için ağ sürücüsünü yeniden arar. Ağ sürücüsü bağlantı etkinleştirme çağrısından döndüğünde, iç IP iş parçacığı bu IP örneği için işlemesi gereken çeşitli olaylar için sonsuza kadar döngü denetimi girer. Bu döngüde işlenen olaylar ertelenmiş IP paketi alımı, IP paket parçası derlemesi, ICMP ping işleme, IGMP işleme, TCP paket kuyruğu işleme, TCP düzenli işleme, IP parçası derleme zaman aşımı ve IGMP düzenli işlemeyi içerir. Olaylar adres çözümleme etkinliklerini de içerir; IPv4'te ARP paket işleme ve ARP düzenli işleme, IPv6'da Yinelenen Adres Algılama, Yönlendirici İsteneni ve Komşu Bulma.

> [!CAUTION]
> *Geri çağırmaları dinleme ve bağlantıyı kesme de dahil olmak üzere NetX Duo geri çağırma işlevleri, özgün çağıran iş parçacığından değil, iç IP iş parçacığından çağrılır. Uygulama herhangi bir NetX Duo geri çağırma işlevinin içinde askıya almama özeni gösterir.*

### <a name="ip-periodic-timers"></a>IP Düzenli Süre süreleri

Her IP örneği için kullanılan iki ThreadX düzenli süreer vardır. İlki ARP, IGMP, TCP zaman aşımı için bir saniyelik süreölçerdir ve aynı zamanda IP parçası yeniden birleşebilir işlemeyi de destekler. İkinci zamanlayıcı, TCP yeniden iletim zaman aşımını ve IPv6 ile ilgili işlemleri başlatmak için 100 m'lık bir zamanlayıcıdır.

### <a name="network-driver"></a>Ağ Sürücüsü

NetX Duo'daki her IP örneğinin birincil arabirimi vardır ve bu arabirim, nx_ip_create ***hizmette belirtilen cihaz sürücüsü tarafından*** tanımlanır. Ağ sürücüsü, paket iletimi, paket alımı ve durum ve denetim istekleri gibi çeşitli NetX Duo isteklerinin işlenmesinden sorumludur. 

Çok girişli bir sistem için, IP örneğinin her biri ilgili arabirim için bu görevleri gerçekleştiren ilişkili bir ağ sürücüsüne sahip birden çok arabirimi vardır.

Ağ sürücüsünün medyada oluşan zaman uyumsuz olayları da işlemesi gerekir. Medyadan gelen zaman uyumsuz olaylar paket alımını, paket iletimini tamamlamayı ve durum değişikliklerini içerir. NetX Duo, ağ sürücüsüne çeşitli olayları işlemek için çeşitli erişim işlevleri sağlar. Bu işlevler, ağ sürücüsünün kesinti hizmeti yordamı kısmından çağrılarak tasarlanmıştır. IPv4 ağları için, ağ sürücüsü alınan tüm ARP paketlerini iç ***işleve _nx_arp_packet_deferred_receive*** iletmesi gerekir. Tüm RARP paketleri , _ iç işlevine *** _nx_rarp_packet_deferred_receive** ilet gerekir. IP paketleri için iki seçenek vardır. IP paketlerinin hızlı bir şekilde sevk edilmesi gerekirse, gelen IP paketleri hemen işleme için _ *_ _nx_ip_packet_receive_* _ adresine iletildi. Bu, IP paketlerinin işlenmesinde NetX Duo performansını büyük ölçüde artırır. Aksi takdirde, IP paketlerini _ _ nx_ip_packet_deferred_receive * adresine iletmenin yapılması gerekir.** Bu hizmet, IP paketini ertelenen işleme kuyruğuna, daha sonra iç IP iş parçacığı tarafından işleyiciye yer verir ve bu da en az ISR işleme süresiyle sonuç verir.

Ağ sürücüsü, IP iş parçacığı bağlamının dışında çalışması için kesme işlemini erteleyebilirsiniz. Bu modda, ISR gerekli bilgileri kaydetmeli, _nx_ip_driver_deferred_processing iç işlevini ***çağırarak*** kesme denetleyicisini kabul eder. Bu hizmet, kesintiye neden olan olayın işlemini tamamlamak için IP iş parçacığına cihaz sürücüsüne bir geri arama zamanlaması konusunda bilgi verir.

Bazı ağ denetleyicileri, değerli CPU kaynaklarını tüketmeden donanımda TCP/IP üst bilgi sağlama işlemi ve doğrulama gerçekleştirebilirsiniz. Donanım özelliği özelliğine sahip olan NetX Duo, derleme zamanında çeşitli yazılım sağlamam hesaplamasını etkinleştirmeye veya devre dışı bırakmaya ek olarak çalışma zamanında sağlamam hesaplamasını açma veya kapatma seçenekleri sunar. Cihaz sürücüsü donanım özellikleriyle ilgili IP katmanıyla iletişim kurabilirse. NetX Duo ağ Azure RTOS yazma hakkında daha ayrıntılı bilgi için bkz. Bölüm [5 - NetX Duo](chapter5.md) Ağ Sürücüleri.

### <a name="multihome-support"></a>Birden Çok Giriş Desteği

NetX Duo, tek bir IP örneği kullanarak birden çok fiziksel cihaza bağlı sistemleri destekler. Her fiziksel arabirim, IP örneğinde bir arabirim denetim bloğuna atanır. Çoklu giriş sistemi kullanmak isteyen uygulamaların sisteme bağlı fiziksel cihaz **sayısına*** NX_MAX_PHSYCIAL_INTERFACES _ değerini tanımlaması ve NetX Duo kitaplığını yeniden oluşturması gerekir. Varsayılan olarak _ *_NX_MAX_PHYSICAL_INTERFACES_** bir olarak ayarlanır ve IP örneğinde bir arabirim denetim bloğu oluşturulur.

NetX Duo uygulaması, * nx_ip_create _ hizmetini kullanarak birincil **cihaz için tek bir** IP örneği oluşturur. Uygulama, her ek ağ cihazı için _ nx_ip_interface_attach * hizmetini kullanarak cihazı IP *_örneğine_* iliştirer.

Her ağ arabirimi yapısı; arabirim IPv4 adresi, alt ağ maskesi, IP MTU boyutu ve MAC katmanı adres bilgileri de dahil olmak üzere IP denetim bloğunda yer alan ağ arabirimi hakkında bir ağ bilgileri alt kümesi içerir.

> [!NOTE]
> *Çoklu giriş desteğine sahip NetX Duo, NetX Duo'un önceki sürümleriyle geriye dönük olarak uyumludur. Açık arabirim bilgilerini almayan hizmetler varsayılan olarak birincil ağ cihazıdır.*

Birincil arabirim, IP örneği listesinde sıfır dizinine sahiptir. IP örneğine bağlı sonraki her cihaza bir sonraki dizin atanır.

IP örneğinin etkin olduğu TCP, UDP, ICMP ve IGMP gibi tüm üst katman protokol hizmetleri tüm bağlı cihazlar tarafından kullanılabilir.

Çoğu durumda, NetX Duo bir paket iletilirken en iyi kaynak adresini belirler. Kaynak adres seçimi, hedef adresi temel alan bir seçimdir. NetX Duo hizmetleri, uygulamaların, hedef adres tarafından en uygun olanı belirlenemezseniz belirli bir kaynak adresi belirtmesine olanak sağlayacak şekilde eklenir. Örneğin, birden çok girişli sistemde bir uygulamanın bir paketi IPv4 yayınına veya çok noktaya yayın hedef adreslerine göndermesi gerekir.

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

Bu hizmetler [NetX Duo Services açıklamasında daha ayrıntılı olarak açıklanmıştır.](chapter4.md)

### <a name="loopback-interface"></a>Geri Döngü Arabirimi

Geri döngü arabirimi, fiziksel bağlantının bağlı olduğu özel bir ağ arabirimidir. Geri döngü arabirimi, uygulamaların IPv4 geri döngü adresi 127.0.0.1'i kullanarak iletişim kurmasına  olanak sağlar. Mantıksal geri döngü arabiriminden yararlanmak için, uygulamanın NX_DISABLE_LOOPBACK_INTERFACE emin olun.

### <a name="interface-control-blocks"></a>Arabirim Denetim Blokları

IP örneğinde arabirim denetim bloklarının sayısı, fiziksel arabirim sayısıdır (***NX_MAX_PHYSICAL_INTERFACES** _) ve etkinleştirildiyse geri döngü arabirimidir. Toplam arabirim sayısı __*_ ve **NX_MAX_IP_INTERFACES tanımlanır.

## <a name="protocol-layering"></a>Protokol Katmanlama

NetX Duo tarafından uygulanan TCP/IP katmanlı bir protokoldür ve bu da daha karmaşık protokollerin temel alınan daha basit protokoller üzerine inşa edile bir protokol olduğu anlamına gelir. TCP/IP'de en düşük katman protokolü *bağlantı düzeyindedir* ve ağ sürücüsü tarafından ele alınan bir protokoldür. Bu düzey genellikle Ethernet'e yöneliktir, ancak fiber, seri veya neredeyse tüm fiziksel medyalar da olabilir.

Bağlantı katmanının üzerinde ağ katmanı *yer ağına yer verir.* TCP/IP'de bu, ağ genelinde en iyi çabayla basit paketleri göndermekten ve almakla sorumlu olan IP'dir. ICMP ve IGMP gibi yönetim türü protokoller, gönderme ve alma için IP'ye bağlı olsalar bile genellikle ağ katmanları olarak kategorilere ayrılmıştır.

Aktarım *katmanı,* ağ katmanının üzerinde yer almaktadır. Bu katman, ağ üzerinde konaklar arasında veri akışını yönetmekle sorumludur. NetX Duo tarafından desteklenen iki tür taşıma hizmeti vardır: UDP ve TCP. UDP hizmetleri iki konak arasında bağlantısız bir şekilde veri göndermek ve almak için en iyi çabayı sunarken, TCP iki konak varlığı arasında güvenilir bağlantı odaklı hizmet sağlar.

Bu katman gerçek ağ veri paketlerine yansıtıldı. TCP/IP'de her katman üst bilgi olarak adlandırılan bir bilgi bloğu içerir. Bir üst bilgi ile verileri (ve muhtemelen protokol bilgilerini) çevreleyen bu teknik genellikle veri kapsülleme olarak adlandırılan bir tekniktir. Şekil 1'de NetX Duo katmanlama örneği ve Şekil 2'de gönderilen UDP verileri için elde edilen veri kapsüllemesi yer almaktadır.

![Protokol Katmanlama](./media/user-guide/image12.jpg)

**ŞEKIL 1. Protokol Katmanlama**

## <a name="packet-pools"></a>Paket Havuzları

Paketlerin hızlı ve belirlenimci bir şekilde belirlenmesi, gerçek zamanlı ağ uygulamalarında her zaman bir zorlukdur. NetX Duo, sabit boyutlu ağ paketlerinin birden çok havuzu oluşturma ve yönetme olanağı sağlar.

NetX Duo paket havuzları sabit boyutlu bellek bloklarından oluşan olduğundan, hiçbir zaman iç parçalanma sorunu oluşturmaz. Elbette parçalanma, doğası gereği belirlenemeyen davranışlara neden olur. Ayrıca NetX Duo paketini ayırmak ve serbest bırakma süresi, basit bağlantılı liste işlemesi sağlar. Ayrıca paket ayırma ve ayırma işlemleri kullanılabilir listenin başında yapılır. Bu, mümkün olan en hızlı bağlantılı liste işlemeyi sağlar.

![UDP Veri Kapsüllemesi](./media/user-guide/image13.png)

**ŞEKIL 2. UDP Veri Kapsüllemesi**

Esneklik eksikliği genellikle sabit boyutlu paket havuzlarının temel dezavantajıdır. En kötü durum gelen paketi de işleyecek en uygun paket yükü boyutunu belirlemek zor bir görevdir. NetX Duo paketleri, paket zincirleme olarak adlandırılan isteğe bağlı bir özellikle bu sorunu ele almaktadır. Gerçek bir ağ paketi, birbirine bağlı bir veya daha fazla NetX Duo paketinden olabilir. Ayrıca, paket üst bilgisi paketin üst kısmında bir işaretçi bulundurrarak. Ek protokoller eklendiklerine göre bu işaretçi geriye doğru taşınır ve yeni üst bilgi doğrudan verilerin önüne yazılır. Esnek paket teknolojisi olmadan, yığının başka bir arabellek ayırması ve verileri yeni üst bilgiyle yeni bir arabelleğe kopyalaması gerekir ve bu da yoğun bir işlemdir.

Belirli bir paket havuzu için her paket yükü boyutu sabit olduğu için, yük boyutundan büyük uygulama verileri birbirine zincirlenmiş birden çok paket gerektirir. Bir paketi kullanıcı verileriyle doldururken, uygulama tarafından ***nx_packet_data_append.*** Bu hizmet uygulama verilerini bir pakete taşır. Bir paketin kullanıcı verilerini tutmak için yeterli olduğu durumlarda, kullanıcı verilerini depolamak için ek paketler ayrılır. Paket zinciri kullanmak için, sürücünün zincirlenmiş paketlere alalı veya zincirli paketlerden aktaranı olması gerekir.

Paket zincirleme özelliğini kullanması gerek kullanmayan katıştırılmış sistemlerde, paket zincirleme mantığını kaldırmak için NetX Duo kitaplığı ***NX_DISABLE_PACKET_CHAIN** _ ile birlikte kullanılabilir. IP parçalanması ve yeniden değerlendirme özelliğinin zincirleme paket özelliğini kullanması gerektirebilirsiniz. Bu nedenle _*_NX_DISABLE_PACKET_CHAIN_*_ _ *_NX_DISABLE_FRAGMENTATION_** da tanımlanmalıdır. 

Her NetX Duo paket bellek havuzu genel bir kaynaktır. NetX Duo, paket havuzlarının nasıl kullanıldıklarına hiçbir kısıtlama uygulamaz. 

### <a name="packet-pool-memory-area"></a>Paket Havuzu Bellek Alanı

Paket havuzunun bellek alanı oluşturma sırasında belirtilir. ThreadX ve NetX Duo nesnelerinin diğer bellek alanlarında olduğu gibi, hedefin adres alanı içinde herhangi bir yerde yer alıyor olabilir. 

Uygulamaya verdiği önemli esneklik nedeniyle bu önemli bir özelliktir. Örneğin, bir iletişim ürününün ağ arabellekleri için yüksek hızlı bir bellek alanına sahip olduğunu varsayalım. Bu bellek alanı, NetX Duo paket bellek havuzuna dönüştürerek kolayca kullanılabilir.

### <a name="creating-packet-pools"></a>Paket Havuzları Oluşturma

Paket havuzları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. NetX Duo uygulamasında paket bellek havuzu sayısıyla ilgili bir sınır yoktur.

### <a name="dual-packet-pool"></a>Çift Paket Havuzu

Genellikle varsayılan IP paket havuzunun yük boyutu, ağ arabirimi MTU'suna kadar çerçeve boyutuna yetecek kadar büyüktür. Normal işlem sırasında IP iş parçacığının ARP, TCP denetim iletileri, IGMP iletileri, ICMPv6 iletileri gibi iletiler göndermesi gerekir. Bu iletiler, IP örneğinde varsayılan paket havuzundan ayrılan paketleri kullanır. Paket havuzu için kullanılabilir bellek miktarının sınırlı olduğu bellek kısıtlı bir sistemde, tek bir paket havuzu kullanmak (MTU boyutuna uygun büyük yük boyutuna sahip) en uygun çözüm olmayabilir. NetX Duo, uygulamanın yük boyutunun daha küçük olduğu bir yardımcı paket havuzu yüklemesini sağlar. Yardımcı paket havuzu yüklendikten sonra IP yardımcı iş parçacığı, ilettiği iletinin boyutuna bağlı olarak paketleri varsayılan paket havuzundan veya yardımcı havuzdan ayırır. Yardımcı paket havuzu için 200 baytlık bir yük boyutu, IP yardımcı iş parçacığının ilettiği iletilerin çoğuyla çalışır.

Varsayılan olarak NetX Duo kitaplığı çift paket havuzu etkinleştirilmeden hazır edilmiştir. Özelliği etkinleştirmek için kitaplığı * NX_DUAL_PACKET_POOL_ENABLE **_** tanımlı olarak derleme. Daha sonra yardımcı paket havuzu _,*_ veya **nx_ip_auxiliary_packet_pool_set.

Ayrıca, birden fazla paket havuzu oluşturma seçeneği de vardır. Örneğin, beklenen ileti boyutları için en uygun yük boyutuna sahip bir iletme paketi havuzu oluşturulur. Sürücüde yük boyutu sürücü MTU'su olarak ayarlanmış bir alma paket havuzu oluşturulur çünkü alınan paketlerin boyutunu tahmin etmek mümkün değil.

### <a name="packet-header-nx_packet"></a>Paket Üst Bilgisi NX_PACKET   
Varsayılan olarak, NetX Duo paket üst bilgilerini paket yükü alanından hemen önce yer alır. Paket bellek havuzu temelde paket yükünden hemen sonra gelen üst bilgiler olan bir paket dizisidir. Paket üst bilgisi (***NX_PACKET***) ve paket havuzunun düzeni Şekil 3'te görüntülanmıştır.

Sıfır kopyalama işlemi gerçekleştirebilecek ağ cihazları sürücüsü için, genellikle paket yükü alanı başlangıç adresi DMA mantığına programlanır. Bazı DMA altyapılarının yük alanında hizalama gereksinimi vardır. Yük alanı başlangıç adresinin DMA altyapısı veya önbellek işlemi için düzgün bir şekilde hizalanması için kullanıcı, 'de ***NX_PACKET_ALIGNMENT.***

> [!WARNING]
> *Bir paketin iletimi tamamlandığında ağ **sürücüsünün nx_packet_transmit_release** işlevini kullanması önemlidir. Bu işlev, paketin kullanılabilir havuza geri yerleştirilmeden önce tcp çıkış kuyruğuna parçası olmadığını denetler.*

![Paket Üst Bilgisi ve Paket Havuzu Düzeni](./media/user-guide/image14.jpg)

**ŞEKIL 3. Paket Üst Bilgisi ve Paket Havuzu Düzeni**

Paket üst bilgisi alanları aşağıdaki gibi tanımlanır. Bu tablonun, tablo yapısında yer alan tüm üyelerin kapsamlı *NX_PACKET* unutmayın.

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

| Paket üst bilgisi | Amaç |
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
|***8 bit protokol***|Bu alan, hangi protokolün IP datagramı kullandığını belirtir. Geçerli protokollerin ve bunların değerlerinin listesi aşağıda verilmiştir:<br />- ICMP: 0x01 <br />- IGMP: 0x02<br />- TCP: 0X06<br />- UDP: 0X11 |
|***16 bit sağlamaları*** |Bu alan yalnızca IP üst bilgisini kapsayan 16 bit sağlama sağlamalarını içerir. IP yükünü üst düzey protokollerde ek sağlama sağlamaları vardır. |
|***32 bit kaynak IP adresi*** |Bu alan gönderenin IP adresini içerir ve her zaman bir konak adresidir. |
|***32 bit hedef IP adresi*** |Bu alan, adres bir yayın veya çok noktaya yayın adresi ise alıcı veya alıcıların IP adresini içerir. |

### <a name="creating-ip-instances"></a>IP Örnekleri Oluşturma

IP örnekleri başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. Uygulama yalnızca IPv6 ağları kullanmayı hedeflese bile, ilk IPv4 adresi, ağ maskesi, varsayılan paket havuzu, medya sürücüsü ve iç IP iş parçacığının bellek ve önceliği ***nx_ip_create*** hizmeti tarafından tanımlanır. Uygulama, IP örneğini IPv4 adresi geçersiz bir adrese (0.0.0.0) ayarlanmış şekilde başlatıyorsa, arabirim adresinin daha sonra el ile yapılandırma, RARP veya DHCP ya da benzer protokoller aracılığıyla çözülecek olduğu varsayılır.

Birden çok ağ arabirimine sahip sistemler için birincil arabirim * nx_ip_create _ **çağrılır.** Her ek arabirim ,* veya **çağrısıyla aynı IP _örneğine nx_ip_interface_attach._ Bu hizmet, ağ arabirimi (IP adresi, ağ maskesi gibi) hakkında bilgileri arabirim denetim bloğunda depolar ve sürücü örneğini IP örneğinde arabirim denetim bloğuyla ilişkilendirmektedir. Sürücü bir veri paketi aldığında, IP alma mantığına iletmeden önce arabirim NX_PACKET veri yapısında depolaması gerekir. Arabirim eklemeden önce bir IP örneğinin önceden oluşturulmuş olması gerektiğini unutmayın.

IPv6 hizmetleri * nx_ip_create _ **çağrısı nx_ip_create.** IPv6 hizmetlerini kullanmak isteyen uygulamaların IPv6'yı başlatmak için _ *_nx_ipv6_enable_** çağrısında olması gerekir.

IPv6 ağın bir IP örneğinde yer alan her arabirimin birden çok IPv6 genel adresi olabilir. Cihaz, IPv6 adres ataması için DHCPv6 kullanmaya ek olarak Durum Bilgisiz Adres Otomatik Yapılandırması da kullanabilir. Bu bölümün ilerleyen bölümlerindeki "IP Denetim Bloğu" ve "IPv6 Adres Çözümlemesi" bölümlerinde daha fazla bilgi edinebilirsiniz.

### <a name="ip-send"></a>IP Gönderme

NetX Duo'daki IP gönderme işlemi çok kolaylaştırılmıştır. Pakette ön uç işaretçisi, IP üst bilgisine uyum sağlayacak şekilde geriye doğru taşınır. IP üst bilgisi tamamlanır (çağrı protokolü katmanı tarafından belirtilen tüm seçeneklerle birlikte), IP sağlama sayısı satır içinde hesaplanır (yalnızca IPv4 paketleri için) ve paket ilişkili ağ sürücüsüne sevk edilir. Ayrıca giden parçalanma, IP gönderme işleminin içinde de eşgüdüm sağlar.

IPv4 için, hedef IP adresi için fiziksel eşleme gerekirse NetX Duo ARP isteklerini başlatıyor. IPv6, IPv6-address-tophysical-address eşlemesi için Komşu Bulma kullanır.

> [!NOTE]
> *IPv4 bağlantısı için, IP adresi çözümlemesi (fiziksel eşleme) gerektiren paketler, kuyruğa alınan paket sayısı ARP kuyruk derinliğini (NX_ARP_MAX_QUEUE_DEPTH simgesiyle tanımlanır) aşana kadar ARP kuyruğunda kuyruğa eklenir. Kuyruk derinliğine ulaşıldı ise NetX Duo, kuyrukta en eski paketi kaldırır ve kuyrukta kalan paketler için adres çözümlemesini beklemeye devam eder. Öte yandan, bir ARP girişi çözümlenmezse, ARP girdisi üzerinde bekleyen paketler ARP girdisi zaman aşımına karşı serbest bıraktır.*

NetX Duo, birden çok ağ arabirimine sahip sistemler için hedef IP adresine göre bir arabirim seçer. Aşağıdaki yordam seçim işlemi için geçerlidir:

1. Gönderen bir giden arabirim belirtirse ve arabirim geçerli ise, bu arabirimi kullanın.
2. Hedef adres IPv4 yayını veya çok noktaya yayın ise, ilk etkin fiziksel arabirim kullanılır.
3. Hedef adres statik yönlendirme tablosunda bulunursa, ağ geçidiyle ilişkili arabirim kullanılır.
4. Hedef bağlantıda ise, bağlantı arabirimi kullanılır.
5. Hedef adres bir bağlantı yerel adresi ise (169.254.0.0/16), ilk geçerli arabirim kullanılır.
6. Varsayılan ağ geçidi yapılandırılmışsa, paketi iletmek için varsayılan ağ geçidiyle ilişkili arabirimi kullanın.
7. Son olarak, geçerli arabirim IP adreslerinden biri bağlantı yerel adresi (169.254.0.0/16) ise, bu arabirim iletim için kaynak adres olarak kullanılır.
8. Yukarıdakilerin hepsi başarısız olursa çıkış paketi bırakılır.

### <a name="ip-receive"></a>IP Alma

IP alma işlemesi ağ sürücüsünden veya iç IP iş parçacığından çağrılır (ertelenen alınan paket kuyruğunda paketlerin iş için). IP alma işlemi protokol alanını inceler ve paketi uygun protokol bileşenine göndermeyi çalışır. Paket gerçekten gönderlanmadan önce, ip üst bilgisi, ip üst bilgisini geçerek ön uç işaretçisi ekılarak kaldırılır.

IP alma işlemi ayrıca parçalı IP paketlerini algılar ve parçalanma etkinse bunları yeniden bir hale almak için gerekli adımları gerçekleştirir. Parçalanma gerekli ancak etkinleştirilmemişse paket bırakılır.

NetX Duo, pakette belirtilen arabirime göre uygun ağ arabirimini belirler. Paket arabirimi NULL ise, NetX Duo varsayılan olarak birincil arabirimdir. Bu, eski NetX Duo Ethernet sürücüleriyle uyumluluğu garanti etmek için yapılır.

### <a name="raw-ip-send"></a>Ham IP Gönderme

Ham IP paketi, NetX Duo tarafından doğrudan desteklenmemektedir (ve işlenmemektedir) üst katman protokol yükünü içeren bir IP çerçevesidir. Ham paket, geliştiricilerin kendi IP tabanlı uygulamalarını tanımlamalarına olanak sağlar. Bir uygulama, ham IP paketi işleme nxd_ip_raw_packet_send hizmette etkinleştirildiyse **,*** nxd_ip_raw_packet_send _ hizmetini kullanarak ham _*_IP nx_ip_raw_packet_enabled_*_ gönderebilir. Bir IPv6 ağına tek noktaya yayın paketi iletilirken NetX Duo, hedef adrese bağlı olarak paketleri göndermek için en iyi kaynak IPv6 adresini otomatik olarak belirler. Ancak hedef adres bir çok noktaya yayın (veya IPv4 için yayın) adresi ise, NetX Duo varsayılan olarak ilk (birincil) arabirimdir. Bu nedenle, bu tür paketleri ikincil arabirimlere göndermek için uygulama, giden paket için nx_ip_raw_packet_source_send kaynak adresini belirtmek üzere _ *_nx_ip_raw_packet_source_send_** hizmetini kullanmalıdır.

### <a name="raw-ip-receive"></a>Ham IP Alma

Ham IP paketi işleme etkinleştirildiyse, uygulama * nx_ip_raw_packet_receive _ **hizmeti** aracılığıyla ham IP paketleri alır. Tüm gelen paketler IP üst bilgisinde belirtilen protokole göre işlenir. Protokol UDP, TCP, IGMP veya ICMP'yi belirtirse, NetX Duo paket protokol türü için uygun işleyiciyi kullanarak paketi işler. Protokol bu protokollerden biri değilse ve ham IP alma etkinse, gelen paket uygulamanın nx_ip_raw_packet_receive * hizmeti aracılığıyla bunu almalarını bekleyen ham paket _*_kuyruğuna_* eklenir. Ayrıca, uygulama iş parçacıkları ham IP paketi beklerken isteğe bağlı bir zaman aşımı ile askıya alabilir. Ham paket kuyruğunda kuyruğa alına paket sayısı sınırlıdır. En büyük değer , varsayılan değeri **20 NX_IP_RAW_MAX_QUEUE_DEPTH**_* içinde tanımlanır. Bir uygulama , _ nx_ip_raw_receive_queue_max_set * hizmetini *_çağırarak maksimum_* değeri değiştirebilir.

Alternatif olarak, NetX Duo kitaplığı ***NX_ENABLE_IP_RAW_PACKET_FILTER* ile de NX_ENABLE_IP_RAW_PACKET_FILTER.** Bu işlem modunda, uygulama işlanmamış protokol türüne sahip bir paket her alınğında çağrılan bir geri çağırma işlevi sağlar. IP alma mantığı, paketi kullanıcı tanımlı ham paket alma filtresi yordamına iletir. Filtre yordamı, ham paketin gelecekteki işlemler için tutulup tutulup tutulmay kararını verir. Geri çağırma yordamından dönüş değeri, paketin ham paket alma filtresi tarafından işlenmiş olup olmadığını gösterir. Paket geri çağırma işlevi tarafından işlenirse, uygulama paketle tamam olduktan sonra paket serbest bırak gerekir. Aksi takdirde Paketin serbest bırakılmasından NetX Duo sorumludur. Ham paket **_nx_ip_raw_packet_filter_set_** kullanma hakkında daha fazla bilgi için aşağıdaki ayrıntılara bakın.

> [!NOTE]
> *NetX Duo için BSD sarmalayıcı işlevi, BSD ham yuvalarını işlemek için ham paket filtresi işlevini kullanır. Bu nedenle, BSD sarmalayıcıda ham yuvayı desteklemek için NetX Duo kitaplığı ***NX_ENABLE_IP_RAW_PACKET_FILTER** _ tanımlı ile oluşturmalı ve uygulama kendi ham paket filtresini yüklemek için _*_nx_ip_raw_packet_filter_set_*_ kullanma functions._

### <a name="default-packet-pool"></a>Varsayılan Paket Havuzu

Oluşturma sırasında her IP örneğine varsayılan bir paket havuzu verilir. Bu paket havuzu ARP, RARP, ICMP, IGMP, çeşitli TCP denetim paketleri (SYN, ACK ve diğer), Komşu Bulma, Yönlendirici Bulma ve Yinelenen Adres Algılama için paket ayırmak için kullanılır. NetX Duo'ya bir paket ayırması gereken varsayılan paket havuzu boşsa NetX Duo'nın belirli bir işlemi durdurması gerekir ve mümkünse bir hata iletisi döndürür.

### <a name="ip-helper-thread"></a>IP Yardımcı İş Parçacığı

Her IP örneğinin bir yardımcı iş parçacığı vardır. Bu iş parçacığı, ertelenen tüm paket işleme ve tüm düzenli işlemlerin işlenmesinden sorumludur. IP yardımcı iş parçacığı, ***nx_ip_create.*** İş parçacığına yığını ve önceliği burada verilir. IP yardımcı iş parçacığında ilk işlemenin, IP oluşturma hizmetiyle ilişkili ağ sürücüsü başlatma işlemini tamamlamak olduğunu unutmayın. Ağ sürücüsü başlatma işlemi tamamlandıktan sonra yardımcı iş parçacığı, paket ve düzenli istekleri işlemeye yarayan sonsuz bir döngü başlatır.

> [!IMPORTANT]
> *IP yardımcı iş parçacığında açıklanamayan bir davranış görülürse, IP oluşturma hizmeti sırasında yığın boyutunu artırmak ilk hata ayıklama adımıdır. Yığın çok küçükse, IP yardımcı iş parçacığı büyük olasılıkla belleğin üzerine yazılabilir ve bu da olağan dışı sorunlara neden olabilir.*

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma

Uygulama iş parçacıkları ham IP paketlerini almaya çalışırken askıya alabilir. Ham bir paket alındıktan sonra, yeni paket askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı devam eder. Paket almaya giden NetX Duo hizmetlerinin hepsi isteğe bağlı bir askıya alma zaman aşımına neden olur. Bir paket alınca veya zaman aşımı sona erdiğinde, uygulama iş parçacığı uygun tamamlanma durumuyla devam eder.

### <a name="ip-statistics-and-errors"></a>IP İstatistikleri ve Hataları

Etkinleştirilirse NetX Duo, uygulama için yararlı olacak çeşitli istatistikleri ve hataları takip eder. Her IP örneği için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen Toplam IP Paketleri
- Gönderilen Toplam IP Bayt Sayısı
- Alınan Toplam IP Paketleri
- Alınan Toplam IP Bayt Sayısı
- Toplam IP Geçersiz Paketleri
- Bırakılan Toplam IP Alma Paketleri
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

Bir ARP isteği veya ARP yanıt paketi alındığında ve gönderici aynı IP adresine sahip olduğunda ve bu düğümün IP adresiyle çakışıyorsa, NetX Duo, bu adres için bir savunma olarak bir ARP isteği gönderir. Çakışma ARP paketi 10 saniye içinde birden çok kez alınmışsa NetX Duo daha fazla savunma paketi göndermez. Varsayılan Aralık 10 saniye, ***NX_ARP_DEFEND_INTERVAL** _ tarafından yeniden tanımlanabilir. Bu davranış, RFC5227 (c) üzerinde belirtilen ilkeyi izler. Windows XP arp bildirisini arp araştırması için bir yanıt olarak yoksaydığından, kullanıcı, arp yanıtını ek erteleme olarak göndermek için _ *_NX_ARP_DEFEND_BY_REPLY_** tanımlayabilir.

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
|Yük Uzunluğu |IPv6 temel üst bilgisini takip eden IPv6 paketinin bayt cinsinden veri miktarını belirten 16 bit alan. Bu, kapsüllene tüm protokol üst bilgilerini ve verilerini içerir.|
|Sonraki Üst Bilgi | IPv6 temel üst bilgisinde yer alan uzantı üst bilgisi türünü belirten 8 bitlik alan. Bu alan, IPv4'te Protokol alanını değiştirir.|
|Atlama Sınırı |Paketin geçişine izin verilen yönlendirici sayısını sınırlayan 8 bitlik alan. Bu alan, *IPv4'te TTL* alanını değiştirir.|
|Kaynak Adres |Gönderenin IPv6 adresini depolar 128 bit alan.|
|Hedef Adres |Hedefin IPv6 adresini alan 128 bitlik alan.|

### <a name="enabling-ipv6-in-netx-duo"></a>NetX Duo'da IPv6'yı etkinleştirme    
IPv6 varsayılan olarak NetX Duo'da etkindir. _nx_user.h* içinde yapılandırılabilir ***NX_DISABLE_IPV6** _ seçeneği tanımlanmamışsa IPv6 hizmetleri NetX Duo'da etkinleştirilir. Bu ***NX_DISABLE_IPV6,*** NetX Duo yalnızca IPv4 hizmetleri sunar ve IPv6 ile ilgili tüm modüller ve hizmetler NetX Duo kitaplığında yerleşik olarak yer alan bir hizmet değildir.

Aşağıdaki hizmet, uygulamaların cihaz IPv6 adresini yapılandırmaları için sağlanmıştır: ***nxd_ipv6_address_set***

Sistem, cihazın IPv6 adreslerini el ile ayarlamaya ek olarak Durum Bilgisiz Adres Otomatik Yapılandırması da kullanabilir. Bu seçeneği kullanmak için uygulamanın cihazda IPv6 **nxd_ipv6_enable** başlatmak için * nxd_ipv6_enable _ çağrısında olması gerekir. Buna ek olarak, NetX Duo'ya Yönlendirici İsteneni, Komşu Bulma _*_ve_*_ Yinelenen Adres Algılama gibi hizmetleri gerçekleştirmesine olanak sağlayan ICMPv6 hizmetleri nxd_icmp_enable çağrılarak başlatılabilir. IPv4 _*_nx_icmp_enable_*_ ICMP'nin başlatı olduğunu unutmayın. _*_nxd_icmp_enable_*_ IPv4 ve IPv6 için ICMP hizmetlerini başlatır. Sistemin ICMPv6 hizmetlerine ihtiyacı yoksa,** ICMPv6 modülünün sisteme bağlı nx_icmp_enable * için _ nx_icmp_enable * kullanılabilir.

Aşağıdaki örnek, tipik bir NetX Duo IPv6 başlatma yordamını gösterir.

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

Üst katman protokolleri (TCP ve UDP gibi) IPv6 başlamadan önce veya başladıktan sonra etkinleştirilebilir.

> [!IMPORTANT]  
> *IPv6 hizmetleri yalnızca IP iş parçacığı başlatıldıktan ve cihaz etkinleştirildikten sonra kullanılabilir.*

Arabirim etkinleştirildikten sonra (yani arabirim cihazı sürücüsü veri göndermeye ve almaya hazır olur ve geçerli bir bağlantı yerel adresi elde edilir), cihaz şu yöntemlerden birini kullanarak genel IPv6 adreslerini elde edebilirsiniz:

- Durum Bilgisiz Adres Otomatik Yapılandırması;  
- El ile IPv6 adresi yapılandırması;  
- DHCPv6 aracılığıyla adres yapılandırması (isteğe bağlı DHCPv6 paketi ile)

İlk iki yöntem aşağıda açıklanmıştır. 3. yöntem (DHCPv6) DHCP paketinde açıklanmıştır.

### <a name="stateless-address-autoconfiguration-using-router-solicitation"></a>YönlendiriciYi Kullanarak Durum Bilgisiz Adres Otomatik Yapılandırması      
NetX Duo cihazları, ön ek bilgileri temin eden bir yönlendirici ile bir IPv6 ağına bağlanıldığında arabirimlerini otomatik olarak yapılandırabilirsiniz. Durum Bilgisiz Adres Otomatik Yapılandırması gerektiren cihazlar yönlendirici istek (RS) iletileri gönderir. Ağ üzerinde yönlendiriciler, istenmeyen yönlendirici tanıtım (RA) iletileriyle yanıt verir. RA iletileri, bir bağlantıyla ilişkili ağ adreslerini tanımlamak için ön ekleri tanıtıyor. Cihazlar daha sonra cihazın bağlı olduğu ağ için benzersiz bir tanımlayıcı üretir. Adres, ön ek ve benzersiz tanımlayıcısı birleştirerek oluşturulur. RA iletilerini alırken bu şekilde, konaklar IP adreslerini üretir. Yönlendiriciler düzenli aralıklarla istenmeyen RA iletileri de gönderebilir. 

> [!WARNING]
> *NetX Duo, bir uygulamanın çalışma zamanında Durum Bilgileri Olmayan Adres Otomatik Yapılandırmayı etkinleştirmesini veya devre dışı bırakmasını sağlar. Bu özelliği etkinleştirmek için NetX Duo kitaplığının tanımlanmış bir NX_IPV6_STATELESS_AUTOCONFIG_CONTROL **gerekir.** Bu özellik etkinleştirildikten sonra, uygulamalar IPv6 **durum nxd_ipv6_stateless_address_autoconfigure_enable*** otomatik nxd_ipv6_stateless_address_autocofigure_disable etkinleştirmek veya devre dışı bırakmak için uygulama ve uygulamaları kullanabilir.

### <a name="manual-ipv6-address-configuration"></a>El ile IPv6 Adresi Yapılandırması     
Belirli bir IPv6 adresi gerekirse, uygulama bir ***IPv6 nxd_ipv6_address_set*** el ile yapılandırmak için IPv6 adresini kullanabilir. Bir ağ arabiriminin birden çok IPv6 adresi olabilir. Ancak, bir sistemde Durum Bilgisiz Adres Otomatik Yapılandırması aracılığıyla veya El ile Yapılandırma aracılığıyla alınan IPv6 adreslerinin toplam sayısının , değerini ***NX_MAX_IPV6_ADDRESSES.***

Aşağıdaki örnekte, bir genel adresi birincil arabirimde (cihaz 0) el ile yapılandırma adımları ip_0:

```c
NXD_ADDRESS global_address;
global_address.nxd_ip_version = NX_IP_VERSION_V6;
global_address.nxd_ip_address.v6[0] = 0x20010000;
global_address.nxd_ip_address.v6[1] = 0x00000000;
global_address.nxd_ip_address.v6[2] = 0x00000000;
global_address.nxd_ip_address.v6[3] = 0x0000ABCD;
```

Konak daha sonra bu adresi genel IP adresi olarak atamak için aşağıdaki NetX Duo hizmetini çağırarak:

```c
status = nxd_ipv6_address_set(&ip_0, 0,  
                              &global_address, 64
                              NX_NULL);
```

### <a name="duplicate-address-detection-dad"></a>Yinelenen Adres Algılama (MİS)    
Sistem IPv6 adresini yapılandırdikten sonra *adres,ATIVE olarak işaretlenir.* RFC 4862'de açıklanan Yinelenen Adres Algılama (TAMAM) etkinse NetX Duo hedef olarak bu geçici adresle birlikte otomatik olarak komşu istek (NS) iletileri gönderir. Ağ üzerinde bu NS iletilerine verilen süre içinde yanıt veren konak yoksa, adresin yerel bağlantıda benzersiz olduğu varsayılır ve durum VALID durumuna geçişler. Bu noktada uygulama iletişim için bu IP adresini kullanmaya başlayabilir.  

THELI işlevi, ICMPv6 modülünün bir parçasıdır. Bu nedenle, yeni yapılandırılan bir adresin GEÇMİS IŞLEMINI geçemeden önce uygulamanın ICMPv6 hizmetlerini etkinleştirmesi gerekir. Alternatif olarak, NETX Duo kitaplığı derlemeortamında nx_user (NX_DISABLE_IPV6_DAD.h olarak tanımlanır) * NX_DISABLE_IPV6_DAD _ seçeneği tanımlayarak DAHİÇ işlemi _*_kapatabilirsiniz._*_ THEIL işlemi sırasında _*_NX_IPV6_DAD_TRANSMITS_*_ parametresi, adresin benzersiz olduğunu belirlemeye yanıt almadan NetX Duo tarafından gönderilen NS iletilerinin sayısını belirler. Varsayılan olarak ve RFC 4862 tarafından önerilen _ *_NX_IPV6_DAD_TRANSMITS_** değeri 3 olarak ayarlanır. Bu simgenin sıfır olarak ayarlanıyor olması, ZAMANI devre dışı bırakır.

Uygulama bir IPv6 adresi atarken ICMPv6 veya THEI etkin değilse, TAMAMI gerçekleştirilecek değildir ve NetX Duo, IPv6 adresinin durumunu hemen VALID olarak ayarlar.

NetX Duo, yerel ve/veya genel adresi geçerli olana kadar IPv6 ağına bağlanamaz. Geçerli bir adres alındıktan sonra NetX Duo, gelen paketin hedef adresini yapılandırılmış IPv6 adresi veya etkin çok noktaya yayın adresiyle eşleşmeye çalışır. Eşleşme bulunamasa paket bırakılır. 

> [!WARNING]  
> *GEÇİCİ işlem sırasında, iletilen ND NS paketlerinin sayısı ***NX_IPV6_DAD_TRANSMITS** tarafından tanımlanır. Varsayılan değer 3'tir ve varsayılan olarak her BIR NS iletisi arasında bir saniyelik bir gecikme _vardır. Bu nedenle, BIR IPv6_ adresi atandıktan sonra (ve bunun yinelenen bir adres olmadığını varsayarak), IP adresinin VALID durumda ve iletişim için hazır olması yaklaşık 3 saniyelik gecikme olur.

Sistemde IPv6 adresleri değiştiriken uygulamalar bildirim almak istiyor olabilir. IPv6 adres değişikliği bildirimi özelliğini etkinleştirmek için NetX Duo kitaplığı tanımlandığı gibi **simgesiyle NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY** gerekir. Özellik etkinleştirildikten sonra, uygulamalar geri çağırma işlevini nxd_ipv6_address_change_notify **_yükleyebilir._**

Bir IPv6 adresi değiştirildi veya geçersiz hale geldi mi, kullanıcı tarafından sağlanan geri çağırma işlevi aşağıdaki bilgilerle çağrılır:

| İşlev  | Açıklama  |
|---|---|
|ip_ptr |IP örneğinin işaretçisi|
|interface_index |Bu IPv6 adresinin ilişkili olduğu ağ arabirimine dizin oluşturma
|ipv6_addr_index |IPv6 adres tablosu dizini|
|ipv6_address |Dört ULONG tamsayısı dizisi şeklinde IPv6 adresinin işaretçisi. Pv6 adresleri konak bayt sırasına göre sunulmuştur.|

### <a name="ipv6-multicast-support-in-netx-duo"></a>NetX Duo'da IPv6 Çok Noktaya Yayın Desteği      
Çok noktaya yayın adresleri, internet üzerinde dinamik bir konak grubu belirtir. Çok noktaya yayın grubunun üyeleri her zaman katılarak ayrıl olabilir. NetX Duo, IP çok noktaya yayın özelliği gerektiren Yinelenen Adres Algılama, Komşu Bulma ve Yönlendirici Bulma dahil olmak üzere çeşitli ICMPv6 protokolleri kullanır. Bu nedenle NetX Duo, temel alınan cihaz sürücüsünün çok noktaya yayın işlemlerini desteklemesi beklemektedir.

NetX Duo'nın çok noktaya yayın grubuna katılması veya gruptan ayrılması  (tüm düğümler için çok noktaya yayın adresi ve istenmeyen düğüm çok noktaya yayın adresi gibi) için cihaz sürücüsüne çok noktaya yayın mac adresi eklemesi veya bırakması için bir sürücü komutu verir. Çok noktaya yayın adresine katılmak için sürücü komutu ***NX_LINK_MULTICAST_JOIN** _. NetX Duo, çok noktaya yayın adresi bırakmak için _* sürücü komutunu _**NX_LINK_MULTICAST_LEAVE_ sağlar. ICMPv6 protokolünün düzgün çalışması için cihaz sürücüsünün bu iki komutu uygulaması gerekir.

Uygulamalar, bir IPv6 çok noktaya yayın grubuna ***nxd_ipv6_multicast_interface_join* hizmetini kullanarak katılabilir.** Bu hizmet, çok noktaya yayın adresini IP yığınına kaydettiriyor ve ardından IPv6 çok noktaya yayın adresinin belirtilen cihaz sürücüsüne bilgi verir. Uygulamalar, çok noktaya yayın grubundan ayrılmak için hizmet ***nxd_ipv6_multicast_interface_leave.***

### <a name="neighbor-discovery-nd"></a>Komşu Bulma (ND)    
Komşu Bulma, fiziksel adresleri IPv6 adreslerine (genel adres veya bağlantı yerel adresi) eşlemek için IPv6 ağlarında bir protokoldür. Bu eşleme, Komşu Bulma Önbelleğinde (ND Önbelleği) korunur. ND işlemi, IPv4'te ARP işleminin eşdeğeridir ve ND Önbelleği de ARP tablosuna benzer. Bir IPv6 düğümü, Komşu Bulma (ND) protokolünü kullanarak komşusunun MAC adresini edinebilirsiniz. Tüm düğümler için istekte bulunulan çok noktaya yayın adresine bir komşu istek (NS) iletisi gönderir ve karşılık gelen komşu tanıtım (NA) iletisi bekler. Bu işlemle alınan MAC adresi ND Önbelleği'ne depolanır.

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

Kullanıcı Veri Birimi Protokolü (UDP), ağ üyeleri arasında en basit veri aktarımı formunu sağlar (RFC 768). UDP veri paketleri bir ağ üyesinden diğerine en iyi çabayla gönderilir; Örneğin, paket alıcısı tarafından onay için yerleşik bir mekanizma yoktur. Ayrıca, UDP paketi göndermek için önceden bağlantı kurulmasına gerek olmaz. Bu nedenle, UDP paket iletimi çok verimlidir.

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
|**16 bit UDP sağlamaları** |Bu alan UDP üst bilgisi, paket veri alanı ve sahte IP üst bilgisi de dahil olmak üzere paket için 16 bit sağlama toplamlarını içerir. |

### <a name="udp-enable"></a>UDP Etkinleştirme   
UDP paket iletiminin mümkün olması için önce uygulamanın nx_udp_enable ***çağırarak UDP'yi etkinleştirmesi*** gerekir. Etkinleştirildikten sonra, uygulama UDP paketlerini gönderebilir ve almakta serbesttir.  

### <a name="udp-socket-create"></a>UDP Yuva Oluşturma    
UDP yuvaları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. İlk hizmet türü, yaşam süresi ve kuyruk derinliği, hizmet tarafından nx_udp_socket_create ***tanımlanır.*** Bir uygulamanın UDP yuvalarının sayısıyla ilgili bir sınır yoktur.

### <a name="udp-checksum"></a>UDP SağlamaLarı   
IPv6 protokolü, paket verilerinde UDP üst bilgi sağlama sayısı hesaplaması gerektirirken IPv4 protokolünde isteğe bağlıdır.  

UDP, IP sahte üst bilgisini (kaynak IP adresi, hedef IP adresi ve protokol/uzunluk IP sözcüğünden oluşan), UDP üst bilgisini ve UDP paket verilerini kapsayan 16 bitlik tamamlayıcı sağlama toplamlarını belirtir. IPv4 ve IPv6 UDP paket üst bilgisi sağlamaları arasındaki tek fark, IPv6'da 128 bit olan kaynak ve hedef IP adreslerinin IPv4'te 32 bit olmasıdır. Hesaplanan UDP sağlama toplam değeri 0 ise, hepsi (0xFFFF). Gönderen yuvada UDP sağlama toplam mantığı devre dışı bırakılmışsa, sağlama toplam hesaplaması olmadığını belirtmek için UDP sağlama toplam alanına sıfır yerleştirilir.

UDP sağlama sayısı alıcı tarafından hesaplanan sağlama sayısı ile eşlenemzse, UDP paketi basitçe atılır.

IPv4 ağına UDP sağlama verileri isteğe bağlıdır. NetX Duo, bir uygulamanın yuva başına UDP sağlama sayısı hesaplamasını etkinleştirmesini veya devre dışı bırakmasını sağlar. Varsayılan olarak UDP yuva sağlama verileri mantığı etkindir. Uygulama , * nx_udp_socket_checksum_disable _ hizmetini çağırarak belirli bir UDP yuvası için **sağlama nx_udp_socket_checksum_disable** devre dışı bırakabilirsiniz. Ancak, IPv6 ağına UDP sağlama verileri zorunludur. Bu nedenle, hizmet _ *_nx_udp_socket_checksum_disable_** IPv6 ağı üzerinden bir paket gönderirken UDP sağlama sayısı mantığını devre dışı bırakmaz.

Bazı Ethernet denetleyicileri, UDP sağlamalarını çalışır şekilde oluşturabiliyor. Sistem donanım sağlama sağlamaları hesaplama özelliğini kullanıyorsa, NetX Duo kitaplığı sağlama sağlama mantığı olmadan da kullanılabilir. UDP yazılım sağlamalarını devre dışı bırakmak için NetX Duo kitaplığının tanımlanmış şu sembollerle inşa edilmiş olması gerekir: ***NX_DISABLE_UDP_TX_CHECKSUM** _ ve NX_DISABLE_UDP_RX_CHECKSUM (Bölüm _*_2'de_*_ açıklanmıştır). Yapılandırma seçenekleri NetX Duo'dan UDP sağlama kümesi mantığını tamamen kaldırırken _ *_nx_udp_socket_checksum_disable_** hizmeti çağrılması, uygulamanın yuva başına IPv4 UDP sağlama tamamı işlemeyi devre dışı bırakmasını sağlar.

### <a name="udp-ports-and-binding"></a>UDP Bağlantı Noktaları ve Bağlama      
UDP bağlantı noktası, UDP protokolünde mantıksal bir uç noktasıdır. NetX Duo'daki UDP bileşeninde 1 ila 1 arasında geçerli 65.535 bağlantı noktası 0xFFFF. UDP verilerini göndermek veya almak için uygulamanın önce bir UDP yuvası oluşturması ve ardından istenen bağlantı noktasına bağlaması gerekir. Bir UDP yuvasını bir bağlantı noktasına bağlamanın ardından uygulama bu yuvada veri gönderebilir ve bu verileri alır.

### <a name="udp-fast-pathtrade"></a>UDP Hızlı Yolu&trade;   
UDP Hızlı &trade; Yolu, NetX Duo UDP uygulaması aracılığıyla düşük paket ek yükü yolunun adıdır. UDP paketi göndermek için yalnızca birkaç işlev çağrısı gerekir: ***nx_udp_socket_send** _, _*_nx_ip_packet_send_*_ ve ağ sürücüsüne yapılan son çağrı. _*_nx_udp_socket_send_*_ NetX Duo'da mevcut NetX uygulamaları için kullanılabilir ve yalnızca IPv4 paketleri için geçerlidir. Ancak tercih edilen yöntem aşağıda ele alınarak _ *_nxd_udp_socket_send_** hizmetini kullanmaktır. UDP paket alımında, UDP paketi uygun UDP yuva alma kuyruğuna yerleştirilir veya ağ sürücüsünün alma kesme işlemeden gelen tek bir işlev çağrısında askıya alınmış bir uygulama iş parçacığına teslim edilir. UDP paketlerini göndermek ve almak için yüksek oranda iyileştirilmiş bu mantık, UDP Hızlı Yol teknolojisinin özüdür.  

### <a name="udp-packet-send"></a>UDP Paket Gönderme    
IPv6 veya IPv4 ağları üzerinden UDP verileri gönderme, * nxd_udp_socket_send _ işlevi **çağrılarak** kolayca gerçek olur. Çağıran, ip sürümünü NXD_ADDRESS parametresinin _nx_ip_version* alanında ayarlaması gerekir. NetX Duo, hedef IPv4/IPv6 adresine göre iletilen UDP paketleri için en iyi kaynak adresi belirler. Bu hizmet, paket verilerinin önüne bir UDP üst bilgisi yer alır ve bunu iç IP gönderme yordamını kullanarak ağa gönderir. Tüm UDP paket iletimleri hemen işlendiğinden, UDP paketleri gönderirken iş parçacığı askıya alınmaz. 

Çok noktaya yayın veya yayın hedefleri için, NetX Duo cihazında seçilecek birden çok IP adresi varsa uygulamanın kaynak IP adresini belirtmesi gerekir. Bu, aşağıdaki hizmetlerle ***nxd_udp_socket_source_send.***

> [!IMPORTANT]    
> *Çok **nx_udp_socket_send** veya yayın paketlerinin iletildiğinde kullanılırsa,* ilk etkinleştirilmiş arabirimin IP adresi kaynak adresi olarak kullanılır.

> [!NOTE] 
> Bu yuva için UDP sağlama toplama mantığı etkinleştirilmişse, sağlama toplama işlemi, UDP veya IP veri yapılarına erişimi engellemeden, çağırma iş parçacığı *bağlamında gerçekleştirilir.* 

> [!WARNING]    
> *Bu yapıda bulunan UDP yükü NX_PACKET uzun sözcük sınırında yer al olmalıdır. Uygulamanın UDP, IP ve* fiziksel medya üst bilgilerini yer aldığı NetX Duo için ön uç işaretçisi ile veri başlatma işaretçisi arasında yeterli alan bırakması gerekir.

### <a name="udp-packet-receive"></a>UDP Paket Alma    
Uygulama iş parçacıkları, belirli bir yuvadan udp paketleri almak için ***nx_udp_socket_receive.*** Yuva alma işlevi, yuvanın alma kuyruğunda en eski paketi teslim ediyor. Alma kuyruğunda paket yoksa, bir paket gelene kadar çağıran iş parçacığı askıya alabilir (isteğe bağlı bir zaman aşımı ile).

UDP alma paketi işlemesi (genellikle ağ sürücüsünün alma kesme işleyicisi tarafından çağrılır), paketi UDP yuvasının alma kuyruğuna yerleştirmekten veya paketi bekleyen ilk askıya alınmış iş parçacığına teslim etmekten sorumludur. Paket kuyruğa alınıyorsa, alma işlemi yuvayla ilişkili en yüksek alma kuyruğu derinliğini de denetler. Yeni kuyruğa alınan bu paket kuyruk derinliğini aşarsa kuyrukta en eski paket atılır.

### <a name="udp-receive-notify"></a>UDP Alma Bildirimi   
Uygulama iş parçacığının birden fazla yuvadan alınan verileri işlemesi gerekirse, ***nx_udp_socket_receive_notify*** işlevi kullanılmalıdır. Bu işlev yuva için bir alma paketi geri çağırma işlevini kaydedmektedir. Yuvada bir paket alınan her zaman, geri çağırma işlevi yürütülür.

Geri çağırma işlevinin içeriği applicationspecific'tir; ancak, büyük olasılıkla işleme iş parçacığına bir paketin artık karşılık gelen yuvada kullanılabilir olduğunu bildirmek için mantık içerir.

### <a name="peer-address-and-port"></a>Eş Adresi ve Bağlantı Noktası   
Bir UDP paketi alırken, uygulama gönderenin IP adresini ve bağlantı noktası numarasını bulmak için bir hizmet ***nx_udp_packet_info_extract.*** Başarılı bir geri dönüşte, bu hizmet gönderenin IP adresi, gönderenin bağlantı noktası numarası ve paketin üzerinden alınarak alınan yerel arabirim hakkında bilgi sağlar.  

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma   
Daha önce belirtildiği gibi, uygulama iş parçacıkları belirli bir UDP bağlantı noktası üzerinde BIR UDP paketi almaya çalışırken askıya alabilir. Bu bağlantı noktası üzerinde bir paket alındıktan sonra, askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı daha sonra devam eder. Çoğu NetX Duo hizmeti için kullanılabilen bir özellik olan UDP alma paketi askıya alınarak isteğe bağlı bir zaman aşımı sağlanır.  

### <a name="udp-socket-statistics-and-errors"></a>UDP Yuva İstatistikleri ve Hataları     
Etkinleştirilirse, NetX Duo UDP yuva yazılımı uygulama için yararlı olan çeşitli istatistikleri ve hataları takip eder. Her IP/UDP örneği için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen Toplam UDP Paketleri  
- Gönderilen Toplam UDP Bayt Sayısı  
- Alınan Toplam UDP Paketleri   
- Alınan Toplam UDP Bayt Sayısı  
- Toplam UDP Geçersiz Paketleri  
- Bırakılan Toplam UDP Alma Paketleri  
- Toplam UDP Alma Sağlama Toplamı Hataları  
- Gönderilen UDP Yuva Paketleri  
- Gönderilen UDP Yuva Baytları  
- Alınan UDP Yuva Paketleri   
- Alınan UDP Yuva Baytları  
- Kuyruğa Alınan UDP Yuva Paketleri  
- Bırakılan UDP Yuva Alma Paketleri  
- UDP Yuva Sağlama Sayısı Hataları  

Tüm bu istatistikler ve hata raporları, tüm UDP yuvaları üzerinde UDP istatistikleri için ***nx_udp_info_get** _ hizmeti ve belirtilen UDP yuvasında UDP istatistikleri için _ *_nx_udp_socket_info_get_** hizmeti ile uygulama tarafından kullanılabilir.

### <a name="udp-socket-control-block-nx_udp_socket"></a>UDP Yuva Denetim Bloğu NX_UDP_SOCKET
Her UDP yuvanın özellikleri, ilişkili NX_UDP_SOCKET bulunur. IP veri yapısı bağlantısı, gönderme ve alma yolları için ağ arabirimi, bağlı bağlantı noktası ve alma paketi kuyruğu gibi yararlı bilgiler içerir. Bu yapı, ***nx_api.h dosyasında*** tanımlanır.

## <a name="transmission-control-protocol-tcp"></a>İletim Denetimi Protokolü (TCP)

İletim Denetimi Protokolü (TCP), iki ağ üyesi (RFC 793) arasında güvenilir akış veri aktarımı sağlar. Bir ağ üyesinden gönderilen tüm veriler, alıcı üye tarafından doğrulanır ve onaylanır. Ayrıca, iki üyenin herhangi bir veri aktarımından önce bir bağlantı kurmış olması gerekir. Tüm bu sonuçlar güvenilir veri aktarımına neden olur; ancak, daha önce açıklanan UDP veri aktarımından çok daha fazla ek yük gerektirir.

Burada da önemli olan, IPv6'nın temel IP katmanıyla ilgili olduğu için NetX ile NetX Duo arasındaki TCP protokolü API hizmetlerindeki hiçbir değişiklik yoktur. Tüm NetX Duo TCP hizmetleri IPv4 veya IPv6 bağlantıları için kullanılabilir.

### <a name="tcp-header"></a>TCP Üst Bilgisi   
İletimde, TCP üst bilgisi kullanıcıdan gelen verilerin önüne yerleştirilir. Alımın ardından TCP üst bilgisi gelen paketten kaldırılır ve yalnızca kullanıcı verileri uygulama için kullanılabilir olur. TCP, paketleri göndermek ve almak için IP protokolünü kullanır; bu, paket ağ üzerindeyken TCP üst bilgisi önünde bir IP üst bilgisi olduğu anlamına gelir. Şekil 13'te TCP üst bilgisi biçimi görüntülenir.

![TCP üst bilgisi biçiminin diyagramı.](./media/user-guide/image22.png)

### <a name="figure-13-tcp-header"></a>ŞEKIL 13. TCP Üst Bilgisi

Tcp üst bilgisi biçimi aşağıda açıklanmıştır:

|Üst Bilgi &nbsp; Alanı |Amaç |
|------|------|
| **16 bit kaynak bağlantı noktası numarası** | Bu alan, TCP paketinin gönderildiği bağlantı noktasını içerir. Geçerli TCP bağlantı noktaları 1 ile 0xFFFF. |
| **16 bit hedef bağlantı noktası** | Bu alan, paketin gönderildiği TCP bağlantı noktasını içerir. Geçerli TCP bağlantı noktaları 1 ile 0xFFFF. |
| **32 bit sıra numarası** | Bu alan, bağlantının bu ucundan gönderilen verilerin sıra numarasını içerir. Özgün dizi, iki TCP düğümü arasındaki ilk bağlantı sırası sırasında oluşturulur. Bu noktadan yapılan her veri aktarımı, gönderilen bayt miktarına göre sıra numarasının bir artışıyla sonuç verir. |
| **32 bit onay numarası** | Bu alan, bağlantının bu tarafında alınan son bayta karşılık gelen sıra numarasını içerir. Bu, daha önce gönderilen verilerin bağlantının diğer ucundan başarıyla alınıp alına olmadığını belirlemek için kullanılır. |
| **4 bit üst bilgi uzunluğu** | Bu alan, TCP üst bilgisinde 32 bit sözcük sayısını içerir. TCP üst bilgisinde seçenek yoksa bu alan 5'tir. |
| **6 bit kod bitleri** |Bu alan, bağlantıyla ilişkili çeşitli denetim bilgilerini göstermek için kullanılan altı farklı kod biti içerir. Denetim bitleri şu şekilde tanımlanır: <br - BR (21): Acil veri önceden<\> br \> - ACK (20): Onay numarası geçerli<br \> - PSH (19): Bu verileri anında işleme<br \> - RST (18): Bağlantıyı sıfırlama<br - SYN (17): Dizi numaralarını eşitleme (bağlantı kurmak için \> kullanılır)<br \> - FIN (16): Gönderenin aktarım işlemi tamamlandı (bağlantıyı kapatmak için kullanılır) |
|**16 bit pencere** |Bu alan akış denetimi için kullanılır. Bu, yuvanın şu anda aldırılana bayt miktarını içerir. Bu temel olarak akış denetimi için kullanılır. Gönderici, gönderilecek verilerin alıcının tanıtıldı penceresine sığacak olduğundan emin olmakla sorumludur. |
|**16 bit TCP sağlamaları** |Bu alan TCP üst bilgisi, paket veri alanı ve sözde IP üst bilgisi dahil olmak üzere paket için 16 bit sağlama toplamlarını içerir. |
|**16 bit acil işaretçi** |Bu alan, acil verilerin son bayta pozitif uzaklığını içerir. Bu alan yalnızca üst bilgide SATıR kodu biti ayarlanmışsa geçerlidir. |

> [!NOTE]  
> *TCP/IP uygulamasındaki tüm üst big endian beklenir.  Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır.*

### <a name="tcp-enable"></a>TCP Etkinleştirme       
TCP bağlantıları ve paket iletimleri mümkün olmadan önce, uygulamanın önce tcp'yi nx_tcp_enable ***etkinleştirmesi*** gerekir. Etkinleştirildikten sonra uygulamanın tüm TCP hizmetlerine erişimi ücretsizdir.  

### <a name="tcp-socket-create"></a>TCP Yuvası Oluşturma    
TCP yuvaları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. İlk hizmet türü, yaşam süresi ve pencere boyutu, nx_tcp_socket_create ***tanımlanır.*** Bir uygulamanın TCP yuvalarının sayısıyla ilgili bir sınır yoktur.  

### <a name="tcp-checksum"></a>TCP SağlamaLarı     
TCP, IP sahte üst bilgisini (kaynak IP adresi, hedef IP adresi ve protokol/uzunluk IP sözcüğünden oluşan), TCP üst bilgisini ve TCP paket verilerini kapsayan 16 bitlik tamamlayıcı sağlama toplamlarını belirtir. IPv4 ve IPv6 TCP paket üst bilgisi sağlamaları arasındaki tek fark, kaynak ve hedef IP adreslerinin IPv4'te 32 bit ve IPv6'da 128 bit olmasıdır. 

Bazı ağ denetleyicileri donanımda TCP sağlama sağlamaları hesaplama ve doğrulama gerçekleştirebilirsiniz. Bu tür sistemlerde, uygulamalar çalışma zamanı ek yükünü azaltmak için mümkün olduğunca donanım sağlama sağlama mantığı kullanmak istiyor olabilir. Uygulamalar, * NX_DISABLE_TCP_TX_CHECKSUM _ ve _* değer ** tanımlayarak NetX Duo kitaplığından TCP sağlama grubu **hesaplama** mantığını derleme zamanında tamamen _devre dışı NX_DISABLE_TCP_RX_CHECKSUM._ Bu şekilde, TCP sağlama sağlama kodu içinde derlenmiş değildir. Ancak isteğe bağlı NetX Duo IPsec paketi yüklüyse ve TCP bağlantısının güvenli bir kanaldan geçmesi gerekirse dikkatli olunması gerekir. Bu durumda, TCP bağlantısına ait paketlerde bulunan veriler zaten şifrelenir ve ağ sürücüsünde bulunan çoğu donanım TCP sağlama toplama modülü şifrelenmiş TCP yükünden doğru sağlama toplama değeri oluşturamaz.

Bu sorunu gidermek için uygulama, kitaplıkta tcp sağlama süresi mantığını tutmalı ve arabirim özelliği özelliğini kullansa gerekmektedir. Arabirim özelliği etkinleştirildiğinde, sürücü sağlama toplam değerini de hesap tanıyorsa TCP modülü TCP sağlama toplamlarını düzgün bir şekilde nasıl işley bilir:

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
> Uygulama, nx_tcp_socket_send() işleviyle birlikte döndürdikten sonra paketi yeniden *kullanmamalıdır veya paketin NX_SUCCESS. İletilen paket, veriler diğer uç tarafından onaylandıktan* sonra NetX Duo iç işleme tarafından serbest bırakıldı.

### <a name="tcp-keepalive"></a>TCP Keepalive     
TCP Sürekliliği özelliği, bir yuvanın uygun sonlandırma olmadan eş bağlantısının kesilip kesilmemesi (örneğin, eş kilitlenmesi) veya belirli ağ izleme tesislerinin uzun süre boşta kalma süresiyle bağlantıyı sonlandırmasını önlemesini sağlar. TCP Keepalive, düzenli aralıklarla verisi olan bir TCP çerçevesi göndererek çalışır ve dizi numarası geçerli dizi numarasından bir küçük olarak ayarlanır. Bu tür TCP Keepalive çerçevesini alan alıcı, hala canlıysa geçerli sıra numarası için bir ACK ile yanıtlar. Bu, süreklilik işlemini tamamlar.  

Varsayılan olarak, tutma özelliği etkin değildir. Bu özelliği kullanmak için NetX Duo kitaplığı * NX_ENABLE_TCP_KEEPALIVE **_** tanımlı olarak hazırlanmalıdır. _ *_NX_TCP_KEEPALIVE_INITIAL_** simgesi, tutma çerçevesinin başlatıldığı saniye sayısını belirtir.  

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

Tüm bu istatistikler ve hata raporları, toplam TCP istatistikleri için * nx_tcp_info_get _ hizmeti ve yuva **başına** TCP istatistikleri için _ *_nx_tcp_socket_info_get_** hizmeti ile uygulamada kullanılabilir.

### <a name="tcp-socket-control-block-nx_tcp_socket"></a>TCP Yuva Denetim Bloğu NX_TCP_SOCKET      
Her TCP yuvasının özellikleri, IP *veri* yapısına bağlantı, ağ bağlantı arabirimi, bağlı bağlantı noktası ve alma paket kuyruğu gibi yararlı bilgiler içeren ilişkili NX_TCP_SOCKET denetim bloğunda bulunur. Bu yapı, ***nx_api.h dosyasında*** tanımlanır.