---
title: Bölüm 3-Azure RTOS NetX 'in Işlevsel bileşenleri
description: Bu bölüm, işlevsel bir perspektiften yüksek performanslı Azure RTOS NetX TCP/IP yığınının bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: db23aa152b2765ac7cc9be098723fc5df0947484
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826885"
---
# <a name="chapter-3---functional-components-of-azure-rtos-netx"></a>Bölüm 3-Azure RTOS NetX 'in Işlevsel bileşenleri

Bu bölüm, işlevsel bir perspektiften yüksek performanslı Azure RTOS NetX TCP/IP yığınının bir açıklamasını içerir. 

## <a name="execution-overview"></a>Yürütmeye genel bakış

NetX uygulaması içinde beş tür program yürütme vardır: başlatma, uygulama arabirimi çağrıları, iç IP iş parçacığı, IP dönemsel zamanlayıcılar ve ağ sürücüsü.

> [!IMPORTANT]
> NetX, ThreadX yüklemesini gerektirir ve iş parçacığı yürütülmesine, askıya alma, düzenli zamanlayıcılar ve karşılıklı dışlama tesislarına bağlıdır.

### <a name="initialization"></a>Başlatma

Diğer bir NetX hizmeti çağrılmadan önce, ***nx_system_initialize** _ hizmeti çağrılmalıdır. Sistem başlatması, ThreadX _ *_tx_application_define_** yordamından ya da uygulama iş parçacıklarından çağrılabilir.

***Nx_system_initialize** _ döndüğünde, sistem paket HAVUZLARı ve IP örnekleri oluşturmaya hazırdır. Bir IP örneği oluşturmak için varsayılan bir paket havuzu gerektiğinden, bir IP örneği oluşturulmadan önce en az bir NetX paket havuzu bulunmalıdır. ThreadX başlatma işlevi _ *_tx_application_define_** ve uygulama iş parçacıklarında paket HAVUZLARı ve IP örnekleri oluşturulmasına izin verilir.

Dahili olarak, bir IP örneği oluşturmak iki bölümde gerçekleştirilir. İlk bölüm, ***tx_application_define*** veya bir uygulama iş parçacığının bağlamından çağıran bağlamı içinde yapılır. Bu, IP veri yapısını ayarlamayı ve iç IP iş parçacığı dahil çeşitli IP kaynakları oluşturmayı içerir. İkinci bölüm, iç IP iş parçacığından ilk yürütme sırasında gerçekleştirilir. Bu, IP oluşturma 'nın ilk bölümü sırasında sağlanan ağ sürücüsünün ilk kez çağrıldığı yerdir. Ağ sürücüsünü iç IP iş parçacığından çağırmak, sürücünün başlatma işlemi sırasında g/ç ve askıya alma işlemlerini gerçekleştirmesini sağlar. Ağ sürücüsü başlatma işleminden döndüğünde, IP oluşturma tamamlanmıştır.

> [!IMPORTANT]
> NetX hizmeti **nx_ip_status_check** , IP örneği ve birincil arabirim durumu hakkında bilgi almak için kullanılabilir. Bu tür durum bilgileri bağlantının başlatılmış, etkin ve IP adresinin çözümlenip çözümlenmediğini içerir. Bu bilgiler, yeni oluşturulan bir IP örneğini kullanması gereken uygulama iş parçacıklarını eşleştirmek için kullanılır. Çoklu giriş sistemleri için aşağıdaki "çoklu giriş desteği" bölümüne bakın. **nx_ip_interface_status_check** , belirtilen arabirim hakkında bilgi almak için kullanılabilir.

### <a name="application-interface-calls"></a>Uygulama arabirimi çağrıları

Uygulamadan yapılan çağrılar, büyük ölçüde ThreadX RTOS altında çalışan uygulama iş parçacıklarından yapılır. Ancak, bazı başlatma, oluşturma ve etkinleştirme Hizmetleri ***tx_application_define*** adresinden çağrılabilir. Bölüm 4 ' teki "Izin verilen" bölümler her bir NetX hizmetinin çağrılabilecek olduğunu gösterir.

Çoğu bölümde, diğer iş parçacıklarının IP örneğine erişimini engellemeden, bilgi işlem sağlama kaynakları gibi yoğun etkinliklerin işlenmesi, çağıran iş parçacığının bağlamı içinde yapılır. Örneğin, iletim sırasında UDP sağlama toplamı hesaplaması, temel alınan IP gönderme işlevi çağrılmadan önce ***nx_udp_socket_send*** hizmeti içinde gerçekleştirilir. Alınan bir pakette, UDP sağlama toplamı, uygulama iş parçacığı bağlamında yürütülen ***nx_udp_socket_receive*** hizmetinde hesaplanır. Bu, düşük öncelikli iş parçacıklarında yoğun sağlama toplamı hesaplamayı işlerken daha yüksek öncelikli iş parçacıklarının ağ isteklerini önlemeye yardımcı olur.

IP adresleri ve bağlantı noktası numaraları gibi değerler, ana bilgisayar bayt düzeninde API işlevlerine geçirilir. Bu değerler dahili olarak ana bilgisayar bayt düzeninde de depolanır. Bu, geliştiricilerin bir hata ayıklayıcı aracılığıyla değerleri kolayca görüntülemesini sağlar. Bu değerler, iletim için bir çerçevede programlandıklarında, ağ bayt sırasına dönüştürülür.

### <a name="internal-ip-thread"></a>İç IP Iş parçacığı

Belirtildiği gibi, NetX 'teki her IP örneğinin kendi iş parçacığı vardır. İç IP iş parçacığının öncelik ve yığın boyutu ***nx_ip_create*** hizmetinde tanımlanmıştır. İç IP iş parçacığı, bir yürütme modunda oluşturulur. IP iş parçacığının, çağıran iş parçacığından daha yüksek bir önceliği varsa, önalım IP oluşturma çağrısı içinde meydana gelebilir.

İç IP iş parçacığının giriş noktası ***_nx_ip_thread_entry*** iç işlevdir. Başlatıldığında, iç IP iş parçacığı ilk olarak uygulamaya özgü ağ sürücüsüne üç çağrı yapmaktan oluşan ağ sürücüsü başlatma işlemini tamamlar. İlk çağrı, ağ sürücüsünü IP örneğine eklemek ve ardından, ağ sürücüsünün başlatma işleminden geçmesine izin veren bir başlatma çağrısı olur. Ağ sürücüsü başlatma işleminden sonra (donanımın düzgün ayarlanması beklenirken askıda kalabilir), iç IP iş parçacığı bağlantıyı etkinleştirmek için ağ sürücüsünü yeniden çağırır. 

Ağ sürücüsü bağlantı etkinleştirme çağrısından döndüğünde, iç IP iş parçacığı bu IP örneği için işleme ihtiyacı olan çeşitli olaylar için sonsuz bir döngü denetimi girer. Bu döngüde işlenen olaylar ertelenmiş IP paket alımı, IP paket parçası derlemesi, ıCMP ping işlemi, ıGMP işleme, TCP paket kuyruğu işleme, TCP düzenli işleme, IP parçası derleme zaman aşımları ve ıGMP düzenli işleme işlemlerini içerir. Olaylar ayrıca adres çözümleme etkinliklerini içerir: IP ağında ARP paket işleme ve ARP düzenli işleme.

> [!NOTE]
> *Dinleme ve bağlantı kesme geri çağırmaları dahil NetX geri çağırma işlevleri, özgün çağıran iş parçacığı değil, iç IP iş parçacığından çağırılır. Uygulamanın herhangi bir NetX geri çağırma işlevi içinde askıya alınması gerekli değildir.*

### <a name="ip-periodic-timers"></a>IP dönemsel zamanlayıcılar
Her IP örneği için kullanılan iki ThreadX dönemsel Zamanlayıcı vardır. İlki ARP, ıGMP, TCP zaman aşımı için tek saniyelik bir zamanlayıcıya sahiptir ve ayrıca IP parçası yeniden atama işlemini de yürütür. İkinci süreölçer, TCP yeniden iletim zaman aşımını sağlamak için bir 100ms Zamanlayıcı olur.

### <a name="network-driver"></a>Ağ sürücüsü
NetX 'teki her IP örneğinin, ***nx_ip_create*** hizmetinde belirtilen cihaz sürücüsü tarafından tanımlanan bir birincil arabirimi vardır. Ağ sürücüsü, paket iletimi, paket alımı ve durum ve denetim istekleri gibi çeşitli NetX isteklerini işlemekten sorumludur.

Birden çok ana sistem için, IP örneğinde, her biri ilgili arabirim için bu görevleri gerçekleştiren ilişkili bir ağ sürücüsüne sahip birden çok arabirim vardır.

Ağ sürücüsünün Ayrıca medyada gerçekleşen zaman uyumsuz olayları işlemesi gerekir. Medyadan gelen zaman uyumsuz olaylar, paket alımı, paket iletimi tamamlama ve durum değişiklikleri içerir. NetX çeşitli olayları işlemek için çeşitli erişim işlevleriyle ağ sürücüsüne olanak sağlar. Bu işlevler, ağ sürücüsünün kesme hizmeti rutin kısmından çağrılabilir şekilde tasarlanmıştır. IP ağları için ağ sürücüsü, alınan tüm ARP paketlerini ***_nx_arp_packet_deferred_receive** _ iç işlevine iletmelidir. Tüm RARP paketlerinin _ *_ _nx_rarp_packet_deferred_receive_* _ iç işlevine iletilmesi gerekir. IP paketlerine yönelik iki seçenek vardır. IP paketlerinin hızlı gönderimi gerekliyse, anında işlenmek üzere gelen IP paketlerinin _ *_ _nx_ip_packet_receive_* _ ' e iletilmesi gerekir. Bu, IP paketlerini işlemede NetX performansını önemli ölçüde artırır. Aksi takdirde, ağ sürücüsünün IP paketlerini _ * _ _nx_ip_packet_deferred_receive_* * öğesine iletmesi gerekir. Bu hizmet, IP paketini ertelenmiş işleme kuyruğuna koyar ve daha sonra iç IP iş parçacığı tarafından işlenir ve bu da en az ıSR işlem süresine neden olur.

Ağ sürücüsü aynı zamanda kesme işlemeyi IP iş parçacığı bağlamında çalışacak şekilde erteleyebilirsiniz. Bu modda, ıSR gerekli bilgileri kaydeder, iç işlev ***_nx_ip_driver_deferred_processing*** çağırır ve kesme denetleyicisini kabul ediyor. Bu hizmet, IP iş parçacığını, kesintiye neden olan olayın işlenmesini tamamlaması için cihaz sürücüsüne bir geri çağırma zamanlamasını bildirir.

Bazı ağ denetleyicileri, değerli CPU kaynakları oluşturmadan donanımda TCP/IP üst bilgi sağlama toplamı hesaplama ve doğrulama işlemlerini gerçekleştirebilir. NetX, donanım özelliği özelliğinden yararlanmak için derleme zamanında çeşitli yazılım sağlama toplamı hesaplamasını etkinleştirme veya devre dışı bırakma ve çalışma zamanında sağlama toplamı hesaplamasını açma veya kapatma seçeneklerini sunar. NetX ağ sürücülerini yazma hakkında daha ayrıntılı bilgi için "[Bölüm 5 NetX ağ sürücüleri](chapter5.md)" başlığına bakın.

### <a name="multihome-support"></a>Çoklu giriş desteği
NetX, tek bir IP örneği kullanılarak birden çok fiziksel cihaza bağlı olan sistemleri destekler. Her fiziksel arabirim, IP örneğindeki bir arabirim Denetim bloğuna atanır. Çok ana bir sistem kullanmak isteyen uygulamalar, sisteme bağlı fiziksel cihaz sayısına **NX_MAX_PHSYCIAL_INTERFACES** değerini tanımlamalıdır ve NETX kitaplığını yeniden derlemelisiniz. Varsayılan olarak **NX_MAX_PHYSICAL_INTERFACES** , IP örneğinde bir arabirim denetim bloğu oluşturarak bir tane olarak ayarlanır.

NetX uygulaması, ***nx_ip_create** _ hizmeti kullanılarak birincil cihaz için tek bir IP örneği oluşturur. Uygulama, her ek ağ aygıtı için, _ *_nx_ip_interface_attach_** hizmetini kullanarak cihazı IP örneğine iliştirir.

Her ağ arabirimi yapısı, IP denetim bloğunda arabirim IP adresi, alt ağ maskesi, IP MTU boyutu ve MAC-katman adresi bilgileri dahil olmak üzere ağ arabirimi hakkındaki ağ bilgilerinin bir alt kümesini içerir.

> [!IMPORTANT]
> *Multihome desteğiyle NetX, NetX 'in önceki sürümleriyle geriye dönük olarak uyumludur. Birincil ağ cihazına açık arabirim bilgilerini varsayılan olmayan hizmetler.*

Birincil arabirimde IP örneği listesinde sıfır dizini vardır. IP örneğine eklenen her bir sonraki cihaza bir sonraki dizin atanır.

TCP, UDP, ıCMP ve ıGMP dahil olmak üzere IP örneğinin etkinleştirildiği tüm üst katman protokol Hizmetleri, tüm bağlı cihazlar için kullanılabilir.

Çoğu durumda NetX, bir paket aktarırken kullanılacak en iyi kaynak adresini belirleyebilir. Kaynak adresi seçimi, hedef adresi temel alır. NetX Hizmetleri, uygulamaların kullanılmak üzere belirli bir kaynak adresi belirtmesini sağlamak için sağlanır, ancak en uygun bir durum hedef adresle belirlenebilir. Birden çok ana sistemde bir örnek, bir uygulamanın bir IP yayınına veya çok noktaya yayın hedef adreslerine bir paket gönderebilmesi gerekir.

Özellikle çok ana uygulamalar geliştirmeye yönelik hizmetler şunları içerir:

*nx_igmp_multicast_interface_join nx_ip_driver_interface_direct_command nx_ip_interface_address_get nx_ip_interface_address_set nx_ip_interface_attach nx_ip_interface_info_get nx_ip_interface_status_check nx_ip_raw_packet_interface_send nx_udp_socket_interface_send*

Bu hizmetler, "[Bölüm 4-Azure RTOS NetX Services açıklaması](chapter4.md)" bölümünde daha ayrıntılı olarak açıklanmıştır.

### <a name="loopback-interface"></a>Geri döngü arabirimi
Geri döngü arabirimi, bağlı bir fiziksel bağlantısı olmayan özel bir ağ arabirimidir. Geri döngü arabirimi, uygulamaların IP geri döngü adresi 127.0.0.1 kullanılarak iletişim kurmasına izin verir

Mantıksal bir geri döngü arabirimini kullanmak için, yapılandırılabilir seçeneğinin ***NX_DISABLE_LOOPBACK_INTERFACE*** ayarlanmamış olduğundan emin olun.

### <a name="interface-control-blocks"></a>Arabirim denetim blokları
IP örneğindeki arabirim denetim bloklarının sayısı, fiziksel arabirimlerin sayısıdır (***NX_MAX_PHYSICAL_INTERFACES** _ tarafından tanımlanır) ve etkinse geri döngü arabirimi. Toplam arabirim sayısı _ *_NX_MAX_IP_INTERFACES_* * içinde tanımlanır.

## <a name="protocol-layering"></a>Protokol katmanlama

NetX tarafından uygulanan TCP/IP katmanlı bir protokoldür, bu da daha karmaşık alt protokollerin daha basit bir temel protokol üzerine oluşturulmuştur. TCP/IP 'de, en düşük katman Protokolü *bağlantı katmanında* bulunur ve ağ sürücüsü tarafından işlenir. Bu düzey genellikle Ethernet 'e yöneliktir, ancak fiber, seri veya neredeyse herhangi bir fiziksel medya olabilir.

Bağlantı katmanının en üstünde *ağ katmanı* bulunur. TCP/IP 'de, bu, temel olarak basit paketlerin gönderilmesi ve alınması ve ağın tamamında en iyi şekilde sorumlu olan IP 'dir. ICMP ve ıGMP gibi yönetim türü protokoller, genellikle IP 'yi gönderme ve alma için kullandıkları halde ağ katmanları olarak kategorize edilir.

*Aktarım katmanı* , ağ katmanının üzerine oturduğu. Bu katman, ağ üzerindeki konaklar arasında veri akışını yönetmekten sorumludur. NetX: UDP ve TCP tarafından desteklenen iki tür aktarım hizmeti vardır. UDP Hizmetleri, iki ana bilgisayar arasında bağlantısız bir şekilde verileri en iyi şekilde gönderme ve alma olanağı sağlarken, TCP iki konak varlık arasında güvenilir bir bağlantı yönelimli hizmet sağlar.

Bu katman, gerçek ağ veri paketlerine yansıtılır. TCP/IP içindeki her katman, üst bilgi olarak adlandırılan bir bilgi bloğu içerir. Bu verilere (ve muhtemelen protokol bilgilerine) sahip bir üst bilgi içeren bu teknik genellikle veri kapsülleme olarak adlandırılır. Şekil 1 ' de NetX katmanlama örneği ve Şekil 2, gönderilen UDP verileri için elde edilen veri kapsüllemesini gösterir.

![Protokol katmanlama](./media/user-guide/protocol-layering.png)

**ŞEKIL 1. Protokol katmanlama**

![UDP veri kapsülleme](./media/user-guide/udp-data-encapsulation.png)

**ŞEKIL 2. UDP veri kapsülleme**

## <a name="packet-pools"></a>Paket havuzları

Paketleri hızlı ve belirleyici bir şekilde ayırmak, gerçek zamanlı ağ uygulamalarında her zaman zorluk sergilemektir. Bu şekilde NetX, sabit boyutlu ağ paketlerinin birden çok havuzunu oluşturma ve yönetme olanağı sağlar.

NetX Paket havuzları sabit boyutlu bellek blokları içerdiğinden, hiçbir iç parçalama sorunu yoktur. Tabii ki parçalama, doğal olarak belirleyici olmayan davranışa neden olur.

Ayrıca, bir NetX paket tutarlarını ayırmak ve serbest bırakmak için gereken süre basit bağlantılı liste işleme. Ayrıca, paket ayırma ve ayırmayı kaldırma, kullanılabilir listenin başında yapılır. Bu, mümkün olan en hızlı bağlantılı liste işlemesini sağlar.

Esneklik olmaması genellikle sabit boyutlu paket havuzlarının başlıca dezavantajıdır. Büyük/küçük harfe gelen paketi de işleyen en iyi paket yükü boyutunun belirlenmesi zor bir görevdir. NetX paketleri, bu sorunu *paket zincirleme* adlı isteğe bağlı bir özellikle ele maktadır. Gerçek bir ağ paketi, birbirine bağlı bir veya daha fazla NetX paketinden yapılabilir. Ayrıca, paket üst bilgisi paketin en üstüne bir işaretçi tutar. Ek protokoller eklendikçe, bu işaretçi geriye doğru taşınır ve yeni üst bilgi doğrudan verilerin önüne yazılır. Esnek paket teknolojisi olmadan, yığının başka bir arabellek ayırması ve verileri yeni bir üst bilgiyle, yoğun işleme alan yeni bir arabelleğe kopyalaması gerekir.

Her paket yükü boyutu belirli bir paket havuzu için düzeltildiğinden, yük boyutundan daha büyük olan uygulama verileri birlikte birden çok paket zincirleme gerektirir. Bir paketi kullanıcı verileriyle doldururken, uygulamanın hizmet ***nx_packet_data_append*** kullanması gerekir. Bu hizmet uygulama verilerini bir pakete taşıtur. Bir paketin Kullanıcı verilerini tutmak için yeterli olmadığı durumlarda, Kullanıcı verilerini depolamak için ek paketler ayrılır. Paket zincirlemesini kullanmak için, sürücünün zincirleme paketlere alabilmesi ya da bu paketten iletim yapabilmesi gerekir.

Her NetX paket bellek havuzu ortak bir kaynaktır. NetX, paket havuzlarının nasıl kullanılbileceğine ilişkin bir kısıtlama yoktur.

### <a name="packet-pool-memory-area"></a>Paket havuzu bellek alanı
Paket havuzu için bellek alanı oluşturma sırasında belirtilir. ThreadX ve NetX nesnelerinin diğer bellek alanları gibi, hedefin adres alanındaki herhangi bir yerde bulunabilir. Bu, uygulamaya verdiği önemli esneklik nedeniyle önemli bir özelliktir. Örneğin, bir iletişim ürününün ağ arabellekleri için yüksek hızlı bellek alanı olduğunu varsayalım. Bu bellek alanı, bir NetX paket bellek havuzunda yapılarak kolayca kullanılır.

### <a name="creating-packet-pools"></a>Paket havuzları oluşturma
Paket havuzları, başlatma sırasında veya çalışma zamanı sırasında uygulama iş parçacıkları tarafından oluşturulur. Bir NetX uygulamasındaki paket belleği havuzlarının sayısında sınır yoktur.

### <a name="packet-header-nx_packet"></a>Paket üst bilgisi NX_PACKET
Varsayılan olarak, NetX paket üst bilgisini paket yük alanından hemen önce koyar. Paket bellek havuzu temel olarak bir dizi paket (üst bilgiler), ardından paket yükünün hemen ardından gelir. Paket üst bilgisi (***NX_PACKET***) ve paket havuzunun düzeni şekil 3 ' te gösterilmiştir.

Sıfır kopyalama işlemi gerçekleştirebilecek ağ cihazları sürücüsü için genellikle paket yük alanının başlangıç adresi DMA mantığıyla programlanabilir. Belirli DMA altyapılarının yük alanında hizalama gereksinimi vardır.

> [!IMPORTANT]
> * Bir paketin iletimi tamamlandığında, ağ sürücüsünün ***nx_packet_transmit_release** _ işlevini çağırması gerekir. Bu işlev, paketin kullanılabilir havuza gerçekten geri yerleştirilmesi için bir TCP çıkış sırasının parçası olmadığından emin olup olmadığını denetler. Bu işlevi çağırma hatası öngörülemeyen behavior._ neden olabilir

![Paket üst bilgisi ve paket havuzu düzeni](./media/user-guide/packet-header-packet-pool-layout.png)

**ŞEKIL 3. Paket üst bilgisi ve paket havuzu düzeni**

Paket üstbilgisinin alanları aşağıdaki tabloda gösterildiği gibi tanımlanır. Bu tablonun *NX_PACKET* yapısındaki tüm üyelerin kapsamlı bir listesi olmadığına unutmayın.

| Paket üst bilgisi          | Amaç                                                                                                                                                                                                                                                                                                                            |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *nx_packet_pool_owner*   | Bu alan, bu belirli paketin sahibi olan paket havuzunu işaret eder. Paket yayınlanmışsa, bu belirli havuza serbest bırakılır. Her paketin içindeki havuz sahipliğiyle, bir veri biriminin birden çok paket havuzundan birden çok pakete yayılması mümkündür.                                                         |
| *nx_packet_next*         | Bu alan, aynı çerçeve içindeki bir sonraki pakete işaret eder. NULL ise çerçevenin parçası olan ek paketler yoktur. |
| *nx_packet_last*         | Bu alan, aynı ağ paketi içindeki son paketi işaret eder. NULL ise, bu paket tüm ağ paketini temsil eder.  |
| *nx_packet_length*       | Bu alan, *nx_packet_next* üyesi tarafından birlikte zincirlenen tüm paketlerin toplam bayt sayısı dahil tüm ağ paketindeki toplam bayt sayısını içerir. |
| *nx_packet_ip_interface* | Bu alan, arabirim sürücüsü tarafından alındığında pakete atanan arabirim denetim bloğu ve giden paketler için NetX tarafından kullanılır. Arabirim denetim bloğu; ağ adresi, MAC adresi, IP adresi ve bağlantı etkin ve fiziksel eşleme gibi arabirim durumu gibi arabirimi tanımlar. |
| *nx_packet_data_start*   | Bu alan, bu paketin fiziksel yük alanının başlangıcını gösterir. NX_PACKET üst bilgisinin hemen arkasından olması gerekmez, ancak ***nx_packet_pool_create*** hizmeti için varsayılandır. |
| *nx_packet_data_end*     | Bu alan, bu paketin fiziksel yük alanının sonuna işaret eder. Bu alan ile nx_packet_data_start alanı arasındaki fark, yük boyutunu temsil eder. |
| *nx_packet_prepend_ptr*  | Bu alan paket verilerinin, paket yükü alanındaki mevcut paket verilerinin önüne (varsa) protokol üstbilgisi veya gerçek veriler eklendiğini gösterir. *Nx_packet_data_start* işaretçi konumundan büyük veya buna eşit ve *nx_packet_append_ptr* işaretçisinden küçük veya eşit olmalıdır.  *NETX, performans nedenleriyle iletim için NETX hizmetlerine geçirildiğinde, önüne işaretçisinin uzun sözcük hizalı adrese işaret ettiğini varsayar.* |
| *nx_packet_append_ptr*    | Bu alan, şu anda paket yükü alanındaki verilerin sonunu işaret eder. *Nx_packet_prepend_ptr* ve *nx_packet_data_end* tarafından işaret edilen bellek konumu arasında olmalıdır. Bu alan ile *nx_packet_prepend_ptr* alanı arasındaki fark, bu paketteki veri miktarını temsil eder. |
| *nx_packet_fragment_next* | Bu alan, paketin tamamının yeniden yayılmadığı sürece parçalanmış paketleri tutmak için kullanılır. |
| *nx_packet_pad*           | Bu alanlar, istenen hizalama gereksinimini elde etmek için 4 baytlık sözcüklerdeki doldurma uzunluğunu tanımlar. *NX_PACKET_HEADER_PAD* tanımlanmamışsa Bu alan kaldırılır. |
|  |  |

### <a name="packet-header-offsets"></a>Paket üst bilgisi uzaklıkları

Paket üst bilgisi boyutu, üst bilgi boyutuna uyum sağlamak için yeterli yer sağlamak üzere tanımlanır. *Nx_packet_allocate* hizmeti bir paket ayırmak ve belirtilen paket türüne göre paketteki preppointer 'ı ayarlaması için kullanılır. Paket türü, protokol verilerinin önüne (UDP, TCP veya ıCMP gibi) protokol üstbilgisini eklemek için gereken uzaklığa NetX söyler.

Aşağıdaki türler, paketteki IP üstbilgisini ve fiziksel katman (Ethernet) üst bilgisini hesaba çekmek için NetX içinde tanımlanmıştır. İkinci durumda, gereken 4 baytlık hizalamasının dikkate alınması 16 bayt olarak kabul edilir. IP paketleri, IP ağları için paketler ayırmak üzere uygulamalar için NetX içinde hala tanımlanmıştır. Aşağıdaki tabloda tanımlanan semboller gösterilmektedir:

| Paket türü   | Değer |
|---------------|-------|
| NX_IP_PACKET  | 0x24  |
| NX_UDP_PACKET | 0x2C  |
| NX_TCP_PACKET | 0x38  |
|               |       |

### <a name="pool-capacity"></a>Havuz kapasitesi
Bir paket havuzundaki paketlerin sayısı, yük boyutunun bir işlevidir ve paket havuzu oluşturma hizmeti için sağlanan bellek alanındaki toplam bayt sayısıdır. Havuzun kapasitesi, paket boyutu (NX_PACKET üst bilgisinin boyutu, yük boyutu ve doğru hizalama) sağlanan bellek alanındaki toplam bayt sayısına bölünerek hesaplanır.

### <a name="thread-suspension"></a>İş parçacığı askıya alma
Uygulama iş parçacıkları, boş bir havuzdan paket beklerken askıya alabilir. Havuza bir paket döndürüldüğünde, askıya alınan iş parçacığına Bu paket verilir ve devam edilir.

Aynı paket havuzunda birden çok iş parçacığı askıya alınırsa, bunlar askıya alındığı sırada sürdürülür (FıFO).

### <a name="pool-statistics-and-errors"></a>Havuz Istatistikleri ve hataları
Etkinleştirilirse, NetX paket yönetimi yazılım **hataları** , uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Paket havuzları için aşağıdaki istatistikler ve hata raporları korunur:

* Havuzdaki toplam paket sayısı
* Havuzdaki ücretsiz paketler
* Havuz boş ayırma Istekleri
* Havuz boş ayırma getirilmesi
* Geçersiz paket yayınları

Bu istatistik ve hata raporlarının tümü, havuzdaki toplam ve ücretsiz paket sayısı dışında, ***NX_DISABLE_PACKET_INFO** _ tanımlanmadığı sürece NETX kitaplığı 'nda yerleşiktir. Bu veriler, _ *_nx_packet_pool_info_get_** hizmeti ile uygulama tarafından kullanılabilir.

### <a name="packet-pool-control-block-nx_packet_pool"></a>Paket havuzu denetim bloğu NX_PACKET_POOL

Her paket bellek havuzunun özellikleri denetim bloğunda bulunur. Bu havuz, bağlantılı ücretsiz paketlerin listesi, serbest paket sayısı ve bu havuzdaki paketlerin yük boyutu gibi yararlı bilgiler içerir. Bu yapı *nx_api. h* dosyasında tanımlanmıştır.

Paket havuzu denetim blokları bellekte herhangi bir yerde bulunabilir, ancak herhangi bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak yaygın olarak kullanılır.

## <a name="ip-protocol"></a>IP Protokolü

NetX 'in Internet Protokolü (IP) bileşeni, Internet üzerinde IP paketleri göndermekten ve almaktan sorumludur. NetX 'te, temel alınan ağ sürücüsünden yararlanarak TCP, UDP, ıCMP ve ıGMP iletileri gönderip alma işleminden sorumlu olan bileşendir.

NetX, IP protokolünü destekler (RFC 791)

### <a name="ip-addresses"></a>IP Adresleri

Internet üzerindeki her konağın, IP adresi olarak adlandırılan benzersiz bir 32 bit tanımlayıcısı vardır. Şekil 4 ' te açıklandığı gibi beş IP adresi sınıfı vardır. Beş IP adresi sınıfının aralıkları aşağıdaki gibidir:

| Sınıf | Aralık                        |
|-------|------------------------------|
| A     | 0.0.0.0 127.255.255.255   |
| B     | 128.0.0.0 to 191.255.255.255 |
| C     | 192.0.0.0 to 223.255.255.255 |
| D     | 224.0.0.0 ile 239.255.255.255 arası |
| E     | 240.0.0.0 to 247.255.255.255 |

**7 bit 24 bit**

![IP adresi yapısı](./media/user-guide/ip-address-structure.png)

**ŞEKIL 4. IP adresi yapısı**

Ayrıca üç tür adres belirtimi vardır: *tek noktaya* yayın, *yayın* ve *çok noktaya yayın*. Tek noktaya yayın adresleri, Internet 'teki belirli bir konağı tanımlayan IP adresleridir. Tek noktaya yayın adresleri bir kaynak ya da hedef IP adresi olabilir. Bir yayın adresi, belirli bir ağ veya alt ağ üzerindeki tüm Konakları tanımlar ve yalnızca hedef adres olarak kullanılabilir. Yayın adresleri, adres kümesinin ana bilgisayar KIMLIĞI kısmı olacak şekilde belirtilir. Çok noktaya yayın adresleri (sınıf D) Internet 'te dinamik bir konaklar grubu belirtir. Çok noktaya yayın grubunun üyeleri her istediklerinde katılabilir ve bırakabilir.

> [!IMPORTANT]
> *Yalnızca IP üzerinden UDP gibi bağlantısız protokoller yayın ve çok noktaya yayın grubunun sınırlı yayın özelliğini kullanabilir.*

> [!IMPORTANT]
> *Makro* IP_address *,*  * **nx_api. h** _ içinde tanımlanmıştır. IP adreslerinin bir nokta yerine virgüller kullanılarak kolay belirtime olanak sağlar. Örneğin, IP_ADDRESS (128, 0, 0, 0) Şekil 4 ' te gösterilen ilk sınıf B adresi _specifies. *

### <a name="ip-gateway-address"></a>IP ağ geçidi adresi

Ağ geçitleri, ağları üzerinde yerel etki alanı dışındaki hedeflere giden paketleri geçirmeye yardımcı olur. Her düğüm, bir sonraki atlamanın, komşlarından biri olan veya önceden programlanmış bir statik yönlendirme tablosu aracılığıyla gönderileceği bir bilgi içerir. Ancak, bu yaklaşımlar başarısız olursa, düğüm paketin hedefine nasıl yönlendirildiğini hakkında daha fazla bilgi içeren paketi varsayılan ağ geçidine iletmelidir. Varsayılan ağ geçidinin IP örneğine bağlı fiziksel arabirimlerden biri aracılığıyla doğrudan erişilebilir olması gerektiğini unutmayın. Uygulama, IP varsayılan ağ geçidi adresini yapılandırmak için ***nx_ip_gateway_address_set*** çağırır.

### <a name="ip-header"></a>IP üstbilgisi

Internet 'te herhangi bir IP paketinin gönderilmesi için bir IP üst bilgisine sahip olması gerekir. Daha yüksek düzey protokoller (UDP, TCP, ıCMP veya ıGMP) bir paket göndermek için IP bileşenini çağırdığınızda, IP gönderme modülü verilerin önüne bir IP üstbilgisi koyar. Buna karşılık, ağdan IP paketleri alındığında, IP bileşeni, IP üst bilgisini, daha üst düzey protokollere göndermeden önce paketten kaldırır. Şekil 5 ' te IP üstbilgisinin biçimi gösterilmektedir.

![IP üst bilgi biçimi](./media/user-guide/ip-header-format.png)

**ŞEKIL 5. IP üst bilgi biçimi**

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm üstbilgilerin big endian biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur. Örneğin, 4 bit sürümü ve IP üstbilgisinin 4 bitlik üstbilgi uzunluğu üstbilginin ilk baytında bulunmalıdır.*

IP üstbilgisinin alanları aşağıdaki gibi tanımlanır:

**IP üstbilgisi alanı amacı**

***4 bit sürümü*** Bu alan, bu üst bilginin temsil ettiği IP sürümünü içerir. NetX 'in desteklediği IP sürüm 4 için, bu alanın değeri 4 ' tür.

***4 bit üst bilgi uzunluğu*** Bu alan, IP üstbilgisindeki 32 bitlik sözcüklerin sayısını belirtir. Hiçbir seçenek sözcüğü yoksa, bu alanın değeri 5 ' tir.

***8 bit hizmet türü (TOS)*** Bu alan, bu IP paketi için istenen hizmetin türünü belirtir. Geçerli istekler şunlardır:

| **TOS Isteği**     | **Değer** |
| ------------------- | --------- |
| Normal              | -      |
| En az gecikme       | 0x10      |
| Maksimum veri        | 0x08      |
| En yüksek güvenilirlik | 0x04      |
| Minimum maliyet        | 0x02      |

***16 bit Toplam uzunluk*** Bu alan IP üst bilgisi dahil olmak üzere bayt cinsinden IP veri biriminin toplam uzunluğunu içerir. Bir IP veri birimi, TCP/IP Interneti üzerinde bulunan temel bilgi birimidir. Verilerin yanı sıra bir hedef ve kaynak adresi içerir. 16 bit alan bir IP veri biriminin en büyük boyutu 65.535 bayttır.

***16 bit tanımlama*** Alan, bir konaktan gönderilen her IP veri birimini benzersiz şekilde tanımlamak için kullanılan bir sayıdır. Bu sayı genellikle bir IP veri birimi gönderildikten sonra artırılır. Alınan IP paket parçalarının montajı özellikle yararlıdır.

***3 bit bayrak*** Bu alan IP parçalama bilgilerini içerir. Bit 14 "parçalara ayırma" bitidir. Bu bit ayarlandıysa, giden IP datagramı parçalanmaz. Bit 13, "daha fazla parça" bitidir. Bu bit ayarlandıysa, daha fazla parça vardır. Bu bit açık ise, IP paketinin son parçadır.

**IP üstbilgisi alanı amacı**

***13 bit parça kayması*** Bu alan, parça kaydırmasına ait 13 bit üst ' i içerir. Bu nedenle, parça uzaklıklarla yalnızca 8 baytlık sınırlarda izin verilir. Parçalanmış bir IP veri biriminin ilk parçası "daha fazla parça" bit kümesine sahip olur ve 0 ' ın bir uzaklığa sahip olur.

***8 bit yaşam süresi (TTL)*** Bu alan, bu veri biriminin geçebileceği yönlendirici sayısını içerir ve bu da veri biriminin ömrünü sınırlar.

***8 bit protokol*** Bu alan, hangi protokolün IP datagramı kullandığını belirtir. Geçerli protokollerin ve bunların değerlerinin listesi aşağıda verilmiştir:

| Protokol | Değer |
|----------|-------|
| ICMP     | 0x01  |
| IGMP     | 0x02  |
| TCP      | 0X06  |
| UDP      | 0X11  |
|          |       |


***16 bit sağlama toplamı*** Bu alan, yalnızca IP üstbilgisini kapsayan 16 bit sağlama toplamını içerir. IP yükünü kapsayan üst düzey protokollerde ek sağlama toplamı vardır.

***32-bit kaynak IP adresi*** Bu alan, gönderenin IP adresini içerir ve her zaman bir ana bilgisayar adresidir.

***32-bit hedef IP adresi*** Bu alan, adres bir yayın veya çok noktaya yayın adresi ise alıcı veya alıcıların IP adresini içerir.

### <a name="creating-ip-instances"></a>IP örnekleri oluşturma

IP örnekleri, başlatma sırasında veya çalışma zamanı sırasında uygulama iş parçacıkları tarafından oluşturulur. İlk IP adresi, ağ maskesi, varsayılan paket havuzu, medya sürücüsü ve iç IP iş parçacığının belleği ve önceliği *nx_ip_create* hizmeti tarafından tanımlanır. Uygulama IP adresi olan IP adresini geçersiz bir adrese (0.0.0.0) ayarlandıysa, arabirim adresinin daha sonra, RARP aracılığıyla ya da DHCP veya benzer protokoller aracılığıyla el ile yapılandırma ile çözümlenebileceği varsayılır.

Birden çok ağ arabirimine sahip sistemler için, *nx_ip_create* çağrılırken birincil arabirim atanır. Her ek arabirim, *nx_ip_interface_attach* ÇAĞıRARAK aynı IP örneğine bağlanabilir. Bu hizmet, arabirim denetim bloğunda ağ arabirimi (IP adresi, ağ maskesi gibi) hakkındaki bilgileri depolar ve sürücü örneğini IP örneğindeki arabirim denetim bloğu ile ilişkilendirir. Sürücü bir veri paketi aldığından, IP alma mantığına iletmeden önce arabirim bilgilerini NX_PACKET yapıda depolaması gerekir. Herhangi bir arabirim iliştirmeden önce bir IP örneğinin oluşturulması gerekir.

 ### <a name="ip-send"></a>IP gönderme
 NetX 'teki IP gönderme işlemi oldukça kolaylaştırılmıştır.

Paketteki önüne işaretçisi, IP üst bilgisine uyacak şekilde geriye taşınır. IP üstbilgisi tamamlandı (çağıran protokol katmanı tarafından belirtilen tüm seçeneklerle), IP sağlama toplamı satır içinde hesaplanır ve paket ilişkili ağ sürücüsüne gönderilir. Ayrıca, giden parçalanma IP gönderme işlemi içinden de koordine edilir.

IP için NetX, hedef IP adresi için fiziksel eşleme gerekliyse ARP isteklerini başlatır.

> [!IMPORTANT]
> *IP bağlantısı için, sıraya alınan paket sayısı ARP kuyruğu derinliğini (sembol NX_ARP_MAX_QUEUE_DEPTH tarafından tanımlanır) aşana kadar IP adresi çözümlemesi (yani fiziksel eşleme) gerektiren paketler ARP kuyruğunda sıraya alınır* *.* *Sıra derinliğine ulaşıldığında NETX kuyruktaki en eski paketi kaldırır ve kalan paketlerin sıraya alındığı adres çözümlemesini beklemeye devam eder. Öte yandan, bir ARP girdisi çözümlenmezse ARP girişinde bekleyen paketler ARP giriş zaman aşımı üzerine serbest bırakılır.*

Birden çok ağ arabirimine sahip sistemler için NetX, hedef IP adresini temel alan bir arabirim seçer. Aşağıdaki yordam seçim işlemi için geçerlidir:

1. Hedef adres IP yayını veya çok noktaya yayın ise ve geçerli bir giden arabirim belirtilmişse, bu arabirimi kullanın. Aksi takdirde, ilk fiziksel arabirim kullanılır.

2. Hedef adres statik yönlendirme tablosunda bulunursa, ağ geçidiyle ilişkili arabirim kullanılır.

3. Hedef bağlantıalıyorsa, bağlantı bağlantısı arabirimi kullanılır.

4. Hedef adres 127.0.0.1 geri döngü adresli ise, geri döngü arabirimi kullanılır.

5. Varsayılan ağ geçidi düzgün yapılandırıldıysa, paketi aktarmak için varsayılan ağ geçidiyle ilişkili arabirimi kullanın.

6. Yukarıdaki tüm hata oluştuğunda çıkış paketi bırakılır.

### <a name="ip-receive"></a>IP alma

IP alma işlemi ağ sürücüsünden veya iç IP iş parçacığından (ertelenmiş alınan paket sırasındaki paketleri işlemek için) çağrılır. IP alma işlemi protokol alanını inceler ve paketi uygun protokol bileşenine gönderme girişiminde bulunur. Paket gerçekten gönderilmeden önce IP üstbilgisi, IP üstbilgisinin ötesinde önüne işaretçisinin ilerleyerek kaldırılır.

IP alma işlemi, parçalanmış IP paketlerini de algılar ve parçalama etkinse bunları yeniden birleştirmek için gerekli adımları gerçekleştirir. Parçalama gerekliyse ancak etkinleştirilmemişse, paket bırakılır.

NetX, pakette belirtilen arabirime bağlı olarak uygun ağ arabirimini belirler. Paket arabirimi NULL ise NetX varsayılan olarak birincil arabirime ayarlanır. Bu, eski NetX Ethernet sürücüleriyle uyumluluğu güvence altına almak için yapılır.

### <a name="raw-ip-send"></a>Ham IP gönderme

Ham IP paketi, NetX tarafından doğrudan desteklenmeyen (ve işlenen) üst katman protokol yükünün bulunduğu bir IP çerçevesidir. Ham paket, geliştiricilerin kendi IP tabanlı uygulamalarını tanımlamasına olanak tanır. Bir uygulama, _*_nx_ip_raw_packet_enabled_*_ HIZMETIYLE ham IP paket işleme etkinleştirildiyse, doğrudan ***nx_ip_raw_packet_send** _ hizmetini kullanarak ham IP paketleri gönderebilir. Hedef adres bir çok noktaya yayın veya yayın adresidir, ancak NetX varsayılan olarak ilk (birincil) arabirime ayarlanır. Bu nedenle, bu tür paketleri ikincil arabirimlerde göndermek için, uygulamanın, giden paket için kullanılacak kaynak adresini belirtmek üzere _ *_nx_ip_raw_packet_interface_send_** hizmetini kullanması gerekir.

### <a name="raw-ip-receive"></a>Ham IP alma

Ham IP paket işleme etkinse, uygulama, ***nx_ip_raw_packet_receive** _ hizmeti aracılığıyla ham IP paketleri alabilir. Tüm gelen paketler, IP üstbilgisinde belirtilen protokole göre işlenir. Protokol UDP, TCP, ıGMP veya ıCMP belirtiyorsa, NetX paket protokol türü için uygun işleyiciyi kullanarak paketi işler. Protokol Bu protokollerden biri değilse ve ham IP alma etkinleştirilmişse, gelen paket, uygulamanın _ *_nx_ip_raw_packet_receive_** hizmeti aracılığıyla almasını bekleyen ham paket kuyruğuna yerleştirilir. Ayrıca, uygulama iş parçacıkları bir ham IP paketini beklerken isteğe bağlı bir zaman aşımı ile askıya alabilir.

### <a name="default-packet-pool"></a>Varsayılan paket havuzu

Her IP örneğine oluşturma sırasında varsayılan bir paket havuzu verilir. Bu paket havuzu ARP, RARP, ıCMP, ıGMP, çeşitli TCP denetim paketleri (SYN, ACK gibi) için paket ayırmak üzere kullanılır. NetX 'in bir paket ayırması gerektiğinde varsayılan paket havuzu boşsa, NetX belirli bir işlemi iptal etmek zorunda kalabilir ve mümkünse bir hata mesajı döndürür.

### <a name="ip-helper-thread"></a>IP Yardımcısı Iş parçacığı

Her bir IP örneğinin bir yardımcı iş parçacığı vardır. Bu iş parçacığı, tüm ertelenmiş paket işlemlerini ve tüm düzenli işlemleri işlemekten sorumludur. IP Yardımcısı iş parçacığı ***nx_ip_create oluşturulur.*** Burada iş parçacığına yığın ve öncelik verilir. IP Yardımcısı iş parçacığındaki ilk işleme, IP oluşturma hizmeti ile ilişkili ağ sürücüsü başlatma işlemini bitirebileceğinizi unutmayın. Ağ sürücüsü başlatma işlemi tamamlandıktan sonra, yardımcı iş parçacığı paket ve düzenli istekleri işlemek için sonsuz bir döngü başlatır.

> [!IMPORTANT]
> *IP Yardımcısı iş parçacığı içinde açıklanamayan davranış görüolduysa, IP oluşturma hizmeti sırasında yığın boyutunun artırılması ilk hata ayıklama adımıdır. Yığın çok küçükse, IP Yardımcısı iş parçacığı muhtemelen belleğin üzerine yazılmasına neden olabilir ve bu da olağan dışı sorunlara yol açabilir.*

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Ham IP paketleri alınmaya çalışılırken uygulama iş parçacıkları askıya alabilir. Bir ham paket alındıktan sonra yeni paket, askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı sürdürülür. Paketleri almak için NetX Hizmetleri, isteğe bağlı askıya alma zaman aşımına uğradı. Bir paket alındığında veya zaman aşımı süresi dolduğunda, uygulama iş parçacığı uygun tamamlanma durumuyla sürdürülür.

### <a name="ip-statistics-and-errors"></a>IP Istatistikleri ve hataları

Etkinleştirilirse NetX, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP örneği için aşağıdaki istatistikler ve hata raporları korunur:

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

Her bir IP örneğinin özellikleri denetim bloğunda bulunur. Her ağ cihazının IP adresleri ve ağ maskeleri, bir komşu IP ve fiziksel donanım adresi eşleme tablosu gibi yararlı bilgiler içerir. Bu yapı ***nx_api tanımlanmıştır. h*** IP örneği denetim blokları bellekte herhangi bir yerde bulunabilir, ancak her bir işlevin kapsamı dışında tanımlayarak denetimin genel bir yapıyı engellemesini sağlamak en yaygın olarak kullanılır.

### <a name="static-ip-routing"></a>Statik IP yönlendirmesi

Statik yönlendirme özelliği, bir uygulamanın ağ dışı hedef IP adresleri için bir IP ağını ve sonraki atlama adresini belirtmesini sağlar. Statik yönlendirme etkinse NetX, göndermek üzere paketin hedef adresiyle eşleşen bir girdinin statik yönlendirme tablosunda arar. Hiçbir eşleşme bulunmazsa NetX, fiziksel arabirimlerin listesini arar ve hedef IP adresine ve ağ maskesine göre bir kaynak IP adresi ve sonraki atlama adresi seçer. Hedef, IP örneğine bağlı ağ sürücülerinin herhangi bir IP adresi ile eşleşmiyorsa NetX varsayılan ağ geçidine doğrudan bağlı bir arabirim seçer ve arabirimin IP adresini kaynak adresi olarak ve varsayılan ağ geçidini sonraki atlama olarak kullanır.

Girdiler, sırasıyla ***nx_ip_static_route_add*** ve ***nx_ip_static_route_delete** _ Hizmetleri kullanılarak statik yönlendirme tablosuna eklenebilir ve kaldırılabilir. Statik yönlendirmeyi kullanmak için, ana bilgisayar uygulamasının _ *_NX_ENABLE_IP_STATIC_ROUTING_*. * öğesini tanımlayarak bu özelliği etkinleştirmesi gerekir

> [!IMPORTANT]
> *Statik yönlendirme tablosuna bir giriş eklenirken NetX, tabloda zaten belirtilen hedef adresi için eşleşen bir giriş olup olmadığını denetler. Varsa, ağ maskesinde daha küçük ağ (daha uzun ön ek) ile giriş için tercih verir.*

### <a name="ip-fragmentation"></a>IP parçalanması

Ağ aygıtı, giden paketlerin boyutuyla sınırlı olabilir. Bu sınıra en fazla iletim birimi (MTU) denir. IP MTU, bir bağlantı katmanı sürücüsünün IP paketi fragmenting olmadan aktarabileceği en büyük IP çerçeve boyutudur. Bir cihaz sürücüsü başlatma aşaması sırasında, sürücü modülünün IP MTU boyutunu hizmet ***nx_ip_interface_mtu_set** ile yapılandırması gerekir. *

Önerilmese de, uygulama cihaz tarafından desteklenen temeldeki IP MTU değerinden daha büyük veri birimleri oluşturabilir. Bu IP veri birimini iletmeden önce, IP katmanı bu paketleri parçalara ayıramalıdır. Parçalanmış IP çerçevelerini alırken, alıcı uç, aynı parçalama KIMLIĞI olan tüm parçalanmış IP çerçevelerini depolamalıdır ve bunları sırayla yeniden birleştirmek zorunda olmalıdır. IP alma mantığı orijinal IP çerçevesini zaman içinde geri yüklemek için tüm parçaları toplayaamadığında tüm parçalar serbest bırakılır. Bu, bu tür paket kaybını tespit etmek ve buradan kurtarmak için üst katman protokolüne sahiptir.

IP parçalama ve yeniden birleştirme işlemini desteklemek için, sistem tasarımcısının ***nx_ip_fragment_enable*** hizmetini kullanarak NETX 'teki IP parçalama özelliğini etkinleştirmesi gerekir. Bu özellik etkinleştirilmemişse, gelen parçalanmış IP paketlerinin yanı sıra ağ sürücüsünün MTU değerini aşan paketler de atılır.

> [!IMPORTANT]
> *IP parçalanma mantığı tanımlayarak*  * tamamen kaldırılabilir **NX_DISABLE_FRAGMENTATION** _ _When, theNetX kitaplığı oluşturuyor. Bunun yapılması NetX 'in kod boyutunu azaltmaya yardımcı olur. *

## <a name="address-resolution-protocol-arp-in-ip"></a>IP 'de Adres Çözümleme Protokolü (ARP)

Adres Çözümleme Protokolü (ARP), 32 bitlik IP adreslerini temel alınan fiziksel ortamlardan (RFC 826) dinamik olarak eşleştirmekten sorumludur. Ethernet en yaygın fiziksel medyadır ve 48 bit adreslerini destekler. ARP gereksinimi, ***nx_ip_create*** hizmetine sağlanan ağ sürücüsüne göre belirlenir. Fiziksel eşleme gerekliyse, ağ sürücüsünün yapı arabiriminde bayrak ***nx_interface_address_mapping_needed*** ayarlaması gerekir.

### <a name="arp-enable"></a>ARP etkinleştir
ARP 'nin düzgün çalışması için öncelikle ***nx_arp_enable*** hizmeti ile uygulama tarafından etkinleştirilmesi gerekir. Bu hizmet, ARP etkinleştirme hizmetine sağlanan bellekten bir ARP önbelleği alanı oluşturma da dahil olmak üzere, ARP işleme için çeşitli veri yapıları ayarlar.

### <a name="arp-cache"></a>ARP önbelleği
ARP önbelleği, iç ARP eşleme veri yapılarının bir dizisi olarak görüntülenebilir. Her iç yapı, bir IP adresi ile fiziksel bir donanım adresi arasındaki ilişkiyi koruma kapasitesine sahiptir. Ayrıca, her veri yapısının birden fazla bağlantılı listenin parçası olması için bağlantı işaretçileri vardır.

Uygulama, ARP tablosunda eşleme varsa, "**nx_arp_ip_address_find** _ hizmetini kullanarak donanım Mac adresı sağlayarak ARP ÖNBELLEĞINDEN bir IP adresi arayabilir. Benzer şekilde, _ *_nx_arp_hardware_address_find_** hizmeti belırlı bir IP adresı için Mac adresini döndürür.


### <a name="arp-dynamic-entries"></a>ARP dinamik girdileri

Varsayılan olarak, ARP etkinleştirme hizmeti, tüm girişleri kullanılabilir dinamik ARP girişleri listesindeki ARP önbelleğine koyar. Eşlenmemiş bir IP adresine gönderilen istek algılandığında NetX tarafından bu listeden dinamik bir ARP girişi ayrılır. Ayırma işleminden sonra ARP girdisi ayarlanır ve fiziksel medyaya bir ARP isteği gönderilir.

Ayrıca, hizmet ***nx_arp_dynamic_entry_set*** bir dinamik giriş de oluşturulabilir.

> [!IMPORTANT]
> *Tüm dinamik ARP girişleri kullanımda ise, en az kullanılan ARP girişi yeni bir eşleme ile değiştirilmiştir.*

### <a name="arp-static-entries"></a>ARP statik girdileri
Uygulama, ***nx_arp_static_entry_create*** hizmetini kullanarak statik ARP eşlemesi de ayarlayabilir. Bu hizmet, dinamik ARP giriş listesinden bir ARP girişi ayırır ve uygulama tarafından sağlanan eşleme bilgilerini kullanarak statik listeye koyar. Statik ARP girdileri yeniden kullanım veya yaşlandırma uygulanmaz. Uygulama, hizmet ***nx_arp_static_entry_delete*** kullanarak statik bir girişi silebilir.
ARP tablosundaki tüm statik girişleri kaldırmak için, uygulama hizmeti ***nx_arp_static_entries_delete*** kullanabilir.

### <a name="automatic-arp-entry"></a>Otomatik ARP girdisi
NetX, ARP isteğine eş yanıtlardan sonra eşin IP/MAC eşlemesini kaydeder. NetX, ağ üzerinden gelen istenmeyen ARP isteklerine göre eş IP/MAC adresi eşlemesini kaydeden otomatik ARP girişi özelliğini de uygular. Bu özellik ARP tablosunun, bu ARP isteği/yanıt döngüsünü ilerlemek için gereken gecikmeyi azaltarak, eş bilgilerle doldurulmasını sağlar. Ancak, otomatik ARP 'yi etkinleştirme ile ilgili diğer taraf ARP tablosunun, yerel bağlantı üzerinde çok sayıda düğüm bulunan meşgul bir ağda hızlı bir şekilde doldurulmasına yol açacağından, bu durum sonunda ARP girişi değişikliği gerçekleşmektedir.

Bu özellik varsayılan olarak etkindir. Devre dışı bırakmak için, NetX kitaplığı tanımlı ***NX_DISABLE_ARP_AUTO_ENTRY*** simgesiyle derlenmiş olmalıdır.

### <a name="arp-messages"></a>ARP Iletileri

Daha önce belirtildiği gibi, IP görevi bir IP adresi için eşlemenin gerekli olduğunu algıladığında bir ARP istek iletisi gönderilir. ARP istekleri, karşılık gelen bir ARP yanıtı alınana kadar düzenli aralıklarla (her ***NX_ARP_UPDATE_RATE** _ saniyede) gönderilir. ARP denemesi terk edilmeden önce toplam _ *_NX_ARP_MAXIMUM_RETRIES_** ARP isteği yapılır. Bir ARP yanıtı alındığında, ilişkili fiziksel adres bilgileri önbellekte olan ARP girişinde depolanır.

NetX, çok giriş sistemleri için ARP isteklerini ve yanıtlarını belirtilen hedef adrese göre hangi arabirime gönderebileceğinizi belirler.

> [!IMPORTANT]
> *NetX ARP yanıtını beklerken, gıden IP paketleri sıraya alınır. Sıraya alınan giden IP paketlerinin sayısı* *NX_ARP_MAX_QUEUE_DEPTH sabiti tarafından tanımlanır*  * . *

NetX, yerel IP ağındaki diğer düğümlerden gelen ARP isteklerine de yanıt verir. ARP isteğini alan arabirimin geçerli IP adresiyle eşleşen bir dış ARP isteği yapıldığında NetX, geçerli fiziksel adresi içeren bir ARP yanıt iletisi oluşturur.

Ethernet ARP isteklerinin ve yanıtlarının biçimleri Şekil 6 ' da gösterilir ve aşağıda açıklanmıştır:

| İstek/yanıt alanı       | Amaç    |
|------------------------------|-----------------|
| Ethernet hedef adresi | Bu 6 baytlık alan ARP yanıtının hedef adresini içerir ve ARP istekleri için bir yayındır (tümü). Bu alan, ağ sürücüsü tarafından ayarlanır. |
| Ethernet kaynak adresi      | Bu 6 baytlık alan, ARP isteği veya yanıtı göndericisinin adresini içerir ve ağ sürücüsü tarafından ayarlanır. |
| Çerçeve türü                   | Bu 2 baytlık alan, mevcut Ethernet çerçevesinin türünü ve ARP istekleri ve yanıtları için 0x0806 ' ya eşittir. Bu, ağ sürücüsünün ayarlamaktan sorumlu olduğu son alandır. |
| Donanım türü                | Bu 2 baytlık alan, Ethernet için 0x0001 olan donanım türünü içerir. |
| Protokol türü                | Bu 2 baytlık alan, IP adresleri için 0x0800 olan protokol türünü içerir. |
| Donanım boyutu                | Bu 1 baytlık alan, Ethernet adresleri için 6 olan donanım adresi boyutunu içerir. |


![ARP paket biçimi](./media/user-guide/arp-packet-format.png)

**ŞEKIL 6. ARP paket biçimi**

| İstek/yanıt alanı | Amaç  |
|---|---|
| Protokol boyutu | Bu 1 baytlık alan, IP adresleri için 4 olan IP adresi boyutunu içerir.  |
| İşlem kodu | Bu 2 baytlık alan, bu ARP paketinin işlemini içerir. Bir ARP yanıtı, 0x0002 değeri ile temsil edilirken, 0x0001 değeri ile bir ARP isteği belirtilir.  |
| Gönderici Ethernet adresi | Bu 6 baytlık alan, gönderenin Ethernet adresini içerir. |
| Gönderenin IP adresi | Bu 4 baytlık alan gönderenin IP adresini içerir. |
| Hedef Ethernet adresi | Bu 6 baytlık alan, hedefin Ethernet adresini içerir. |
| Hedef IP adresi | Bu 4 baytlık alan, hedefin IP adresini içerir. |

> [!IMPORTANT]
> *ARP istekleri ve yanıtları Ethernet düzeyindeki paketlerdir. Diğer tüm TCP/IP paketleri bir IP paket üstbilgisiyle kapsüllenir.*

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm ARP iletilerinin big endian biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

### <a name="arp-aging"></a>ARP eskime

NetX, otomatik dinamik ARP girişi geçersiz doğrulamasını destekler. ***NX_ARP_EXPIRATION_RATE** _specifies fiziksel eşlemenin ÜZERINDE bir IP adresinin geçerli kaldığı saniye sayısı. Süre dolduktan sonra ARP girişi ARP önbelleğinden kaldırılır. Karşılık gelen IP adresine gönderme denemesi, yeni bir ARP isteğine neden olur. _ *_NX_ARP_EXPIRATION_RATE_** değerini sıfıra ayarlamak, varsayılan yapılandırma olan ARP eskimesini devre dışı bırakır.

### <a name="arp-defend"></a>ARP savun

Bir ARP isteği veya ARP yanıt paketi alındığında ve gönderici aynı IP adresine sahip olduğunda ve bu düğümün IP adresiyle çakışıyorsa NetX, bu adres için bir savunma olarak bir ARP isteği gönderir. Çakışma ARP paketi 10 saniye içinde birden çok kez alınmışsa NetX, daha fazla savunma paketi göndermez. Varsayılan Aralık 10 saniye, ***NX_ARP_DEFEND_INTERVAL** _ tarafından yeniden tanımlanabilir. Bu davranış, RFC5227 (c) üzerinde belirtilen ilkeyi izler. Windows XP ARP bildirisini ARP araştırması için bir yanıt olarak yoksaydığından, Kullanıcı ARP yanıtını ek erteleme olarak göndermek için _ *_NX_ARP_DEFEND_BY_REPLY_* * tanımlayabilir.

### <a name="arp-statistics-and-errors"></a>ARP Istatistikleri ve hataları

Etkinleştirilirse, NetX ARP yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Aşağıdaki istatistikler ve hata raporları her IP 'nin ARP işlemleri için tutulur:

- Gönderilen toplam ARP Isteği sayısı
- Alınan toplam ARP Isteği sayısı
- Gönderilen toplam ARP yanıtı
- Alınan toplam ARP yanıtı
- Toplam ARP dinamik girişleri
- Toplam ARP statik girişleri
- Toplam ARP eski girdileri
- Toplam ARP geçersiz Iletileri

Bu istatistik ve hata raporlarının tümü, ***nx_arp_info_get*** hizmeti ile uygulama tarafından kullanılabilir.

## <a name="reverse-address-resolution-protocol-rarp-in-ip"></a>IP 'de ters Adres Çözümleme Protokolü (RARP)

Ters Adres Çözümleme Protokolü (RARP), konağın 32 bit IP adreslerinin (RFC 903) ağ atamasını istemek için protokoldür. Bu, bir RARP isteği aracılığıyla yapılır ve bir ağ üyesi bir RARP yanıtında ana bilgisayar ağ arabirimine bir IP adresi atalana kadar düzenli olarak devam eder. Uygulama, sıfır IP adresine sahip hizmet ***nx_ip_create*** bir IP örneği oluşturur. RARP uygulama tarafından etkinleştirilmişse, ağ sunucusundan, sıfır IP adresine sahip arabirim aracılığıyla erişilebilen bir IP adresi istemek için RARP protokolünü kullanabilir.

### <a name="rarp-enable"></a>RARP etkinleştir

RARP 'yi kullanmak için, uygulamanın IP adresi sıfır olan IP örneğini oluşturması ve ardından hizmet ***nx_rarp_enable*** kullanarak RARP 'yi etkinleştirmesi gerekir. Çoklu giriş sistemlerinde, IP örneğiyle ilişkilendirilmiş en az bir ağ cihazının IP adresi sıfır olmalıdır. RARP işleme, ağ tarafından belirlenen IP adresine sahip geçerli bir RARP yanıtı alınana kadar IP adresi gerektiren NetX sistemine yönelik olarak RARP istek iletileri gönderir. Bu noktada, RARP işleme tamamlanmıştır.

RARP etkinleştirildikten sonra, tüm arabirim adresleri çözümlendikten sonra otomatik olarak devre dışıdır. Uygulama, Service ***nx_rarp_disable*** kullanarak RARP 'yi sonlandırmayı zorlayabilir.

###  <a name="rarp-request"></a>RARP Isteği

Bir RARP istek paketinin biçimi, [ARP iletileri](#arp-messages)konusunun Şekil 6 ' da gösterilen ARP paketiyle neredeyse aynıdır. Tek fark, çerçeve türü alanı 0x8035 ve *Işlem kodu* alanı 3 ' tür ve bır RARP isteği tanımlayarak 3 ' tür. Daha önce belirtildiği gibi, RARP istekleri düzenli aralıklarla (her ***NX_RARP_UPDATE_RATE*** saniyede), ağ atanmış IP adresine sahıp bır RARP yanıtı alınana kadar gönderilir.

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm RARP iletilerinin big endian biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

### <a name="rarp-reply"></a>RARP yanıtı

RARP yanıt iletileri ağdan alınır ve bu konak için ağ tarafından atanan IP adresini içerir. Bir RARP yanıt paketinin biçimi, Şekil 6 ' da gösterilen ARP paketiyle neredeyse aynıdır. Tek fark, çerçeve türü alanı 0x8035 ' dir ve *Işlem kodu* alanı, BIR RARP yanıtı atayan 4 ' tür. Aldıktan sonra IP adresi IP örneğinde ayarlanır, düzenli olarak RARP isteği devre dışıdır ve IP örneği artık normal ağ işlemleri için hazırdır.

Çok ana konaklar için IP adresi, isteyen ağ arabirimine uygulanır. Hala bir IP adresi ataması isteğinde bulunan başka ağ arabirimleri varsa, tüm Arabirim IP adresi istekleri çözümlenene kadar düzenli RARP hizmeti devam eder.

> [!IMPORTANT]
> *Uygulama, RARP işlemesi tamamlanana kadar IP örneğini kullanmamalıdır. **Nx_ip_status_check** , uygulamalar tarafından RARP tamamlanmasını beklemek için kullanılabilir. Çoklu giriş sistemlerinde, bu arabirim üzerinde RARP işlemesi tamamlanana kadar uygulama istekte bulunan arabirimini kullanmamalıdır. İkincil cihazdaki IP adresinin durumu **nx_ip_interface_status_check** hizmetiyle denetlenebilir.*

### <a name="rarp-statistics-and-errors"></a>RARP Istatistikleri ve hataları

Etkinleştirilirse NetX RARP yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP 'nin RARP işlemesi için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen toplam RARP Isteği
- Toplam alınan RARP yanıtı
- Toplam RARP geçersiz Ileti

Bu istatistik ve hata raporlarının tümü, ***nx_rarp_info_get*** hizmeti ile uygulama tarafından kullanılabilir.

## <a name="internet-control-message-protocol-icmp"></a>Internet Denetim Iletisi Protokolü (ıCMP)

IP için Internet Denetim Iletisi Protokolü (ıCMP), IP ağ üyeleri arasında hata ve denetim bilgilerini geçirme ile sınırlıdır.

Diğer çoğu uygulama katmanının (örn. TCP/IP) iletileri gibi, ıCMP iletileri, ıCMP Protokolü atamasının bulunduğu bir IP üstbilgisiyle kapsüllenir.

### <a name="icmp-statistics-and-errors"></a>ICMP Istatistikleri ve hataları

Etkinleştirilirse NetX, uygulama için yararlı olabilecek birkaç ıCMP istatistiğini ve hatasını izler. Her IP 'nin ıCMP işlemi için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen toplam ıCMP pingi
- Toplam ıCMP ping zaman aşımları
- Askıya alınan toplam ıCMP ping Iş parçacığı
- Alınan toplam ıCMP ping yanıtı
- Toplam ıCMP sağlama toplamı hatası
- Toplam ıCMP Işlenmemiş Ileti

Bu istatistik ve hata raporlarının tümü, ***nx_icmp_info_get*** hizmeti ile uygulama tarafından kullanılabilir.

### <a name="icmp-enable"></a>ICMP etkinleştirme
ICMP iletilerinin NetX tarafından işlenebilmesi için, uygulamanın ıCMP işlemesini etkinleştirmek üzere ***nx_icmp_enable*** hizmetini çağırması gerekir. Bu işlem yapıldıktan sonra uygulama, ping istekleri ve alan gelen ping paketleri verebilir.

### <a name="icmp-echo-request"></a>ICMP yankı Isteği
Yankı isteği, ana bilgisayar IP adresi tarafından tanımlanan şekilde, ağ üzerinde belirli bir düğümün varlığını denetlemek için kullanılan bir ıCMP iletisi türüdür. Popüler ping komutu, ıCMP yankı isteği/Yankı Yanıtı iletileri kullanılarak uygulanır. Belirli bir konak mevcutsa, ağ yığını ping isteğini ve ping yanıtı ile yanıtları işler. Şekil 7 ' de ıCMP ping iletisi biçimi ayrıntılı olarak gösterilmiştir.

![ICMP ping Iletisi](./media/user-guide/icmp-ping-message.png)

**ŞEKIL 7. ICMP ping Iletisi**

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm ıCMP iletilerinin big endian biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

Aşağıdaki tabloda ıCMP başlık biçimi açıklanmaktadır:

| Üst bilgi alanı    | Amaç |
|-----------------|---------------------------------------------------|
| Tür            | Bu alan ıCMP iletisini belirtir (BITS 31-24). En yaygın şunlardır: 0 echo yanıt 8 yankı Isteği |
| Kod            | Bu alan, tür alanındaki bağlamdır (BITS 23-16). Yankı isteği için veya yanıt kodu sıfır olarak ayarlanır. |
| Sağlama        | Bu alan, tür alanından başlayarak ıCMP üstbilgisinin tamamı dahil olmak üzere, ıCMP iletisinin tamamlayıcından oluşan 16 bit sağlama toplamını içerir. Sağlama toplamını oluşturmadan önce, sağlama toplamı alanı temizlenir.                 |
| Kimlik  | Bu alan, Konağı tanımlayan bir KIMLIK değeri içerir; Ana bilgisayar, YANKı YANıTıNDA YANKı isteğinden ayıklanan KIMLIĞI kullanmalıdır (BITS 31-16). |
| Sıra numarası | Bu alan bir KIMLIK değeri içerir; Ana bilgisayar, YANKı YANıTıNDA YANKı isteğinden ayıklanan KIMLIĞI kullanmalıdır (BITS 31-16). Tanımlayıcı alanından farklı olarak, bu değer aynı ana bilgisayardan gelen bir sonraki yankı isteğinde de değişecektir (BITS 15-0). |


### <a name="icmp-echo-response"></a>ICMP yankı yanıtı
Ping yanıtı, dış bir ping isteğine yanıt olarak ıCMP bileşeni tarafından dahili olarak oluşturulan başka bir ıCMP iletisi türüdür. Onay komutuna ek olarak, ping yanıtı da ping isteğinde sağlanan kullanıcı verilerinin bir kopyasını içerir.

## <a name="internet-group-management-protocol-igmp"></a>Internet Grup Yönetimi Protokolü (IGMP)

Internet Grup Yönetimi Protokolü (ıGMP), komşileriyle iletişim kuracak bir cihaz sağlar ve bir IP çok noktaya yayın grubu (RFC 1112 ve RFC 2236) almayı veya katılmayı amaçladığı yönlendiricileriyle iletişim kurar. Çok noktaya yayın grubu temel olarak dinamik bir ağ üyeleri koleksiyonudur ve bir sınıf D IP adresi ile temsil edilir. Çok noktaya yayın grubunun üyeleri herhangi bir zamanda bırakabilir ve yeni üyeler istediğiniz zaman katılabilir. Gruba katılma ve gruptan ayrılmayla ilgili koordinasyon, ıGMP 'nin sorumluluğundadır.

### <a name="igmp-enable"></a>IGMP etkinleştirme

NetX 'te herhangi bir çok noktaya yayın etkinliğinin gerçekleşmesi için, uygulamanın ***nx_igmp_enable*** hizmetini çağırması gerekir. Bu hizmet, çok noktaya yayın isteklerini hazırlamak için temel ıGMP başlatmayı gerçekleştirir.

### <a name="multicast-ip-addressing"></a>Çok noktaya yayın IP adresleme

Daha önce belirtildiği gibi, çok noktaya yayın adresleri aslında 3.58 sayfada Şekil 4 ' te gösterildiği gibi sınıf D IP adresleridir. D adresinin daha düşük 28 bit düzeyi çok noktaya yayın grubu KIMLIĞINE karşılık gelir. Önceden tanımlanmış bir dizi önceden tanımlı çok noktaya yayın adresi vardır. Ancak, *tüm ana bilgisayarlar adresi* (244.0.0.1) özellikle IGMP işleme için önemlidir. *Tüm konaklar adresi* , yönlendiriciler tarafından, ait oldukları çok noktaya yayın gruplarını raporlamak üzere tüm çok noktaya yayın üyelerini sorgulamak için kullanılır.

### <a name="physical-address-mapping-in-ip"></a>IP 'de fiziksel adres eşlemesi

Sınıf D çok noktaya yayın adresleri doğrudan 01.00.5 e. 00.00.00 ile 01.00.5 e. 7f. ff. FF arasında değişen fiziksel Ethernet adreslerine eşlenir. IP çok noktaya yayın adresinin daha düşük 23 biti, Ethernet adresinin daha düşük 23 bitmine doğrudan eşlenir.

### <a name="multicast-group-join"></a>Çok noktaya yayın grubuna ekleme

Belirli bir çok noktaya yayın grubuna katılması gereken uygulamalar, ***nx_igmp_multicast_join*** hizmetini çağırarak bunu yapabiliriz. Bu hizmet, bu çok noktaya yayın grubuna katılması için istek sayısını izler. Bu, çok noktaya yayın grubuna katılması için ilk uygulama isteğidir, birincil ağda bu konağın gruba katılması için bir ıGMP raporu gönderilir. Daha sonra, ağ sürücüsü bu çok noktaya yayın grubu için Ethernet adresine sahip paketleri dinlemek üzere ayarlanır.

Çoklu ana sistemde, çok noktaya yayın grubuna belirli bir arabirim üzerinden erişilebiliyorsa, uygulama, birincil ağdaki çok noktaya yayın gruplarıyla sınırlı olan ***nx_igmp_multicast_join** yerine hizmet ***nx_igmp_multicast_interface_join*** kullanır.

### <a name="multicast-group-leave"></a>Çok noktaya yayın grubu bırakma

Daha önce birleştirilmiş bir çok noktaya yayın grubuna ayrılmaları gereken uygulamalar, ***nx_igmp_multicast_leave*** hizmetini çağırarak bunu yapamayabilir. Bu hizmet, grubun kaç kez katıldığı ile ilişkili iç sayıyı azaltır. Bir grup için bekleyen bir JOIN isteği yoksa, bu çok noktaya yayın grubunun Ethernet adresine sahip paketleri dinlemeyi devre dışı bırakmak için ağ sürücüsü çağırılır

### <a name="multicast-loopback"></a>Çok noktaya yayın geri döngüsü

Bir uygulama, aynı düğümdeki kaynaklardan birinden kaynaklanan çok noktaya yayın trafiğini almak isteyebilir. Bu, hizmet ***nx_igmp_loopback_enable*** kullanılarak IP çok noktaya yayın bileşeninin geri döngüden etkinleştirilmesini gerektirir.

### <a name="igmp-report-message"></a>IGMP rapor Iletisi

Uygulama bir çok noktaya yayın grubuna katıldığında, ana bilgisayarın belirli bir çok noktaya yayın grubuna katılma işlemini göstermek için ağ üzerinden bir ıGMP rapor iletisi gönderilir. IGMP rapor iletisinin biçimi Şekil 8 ' de gösterilir. Çok noktaya yayın grubu adresi, ıGMP rapor iletisindeki Grup iletisi ve hedef IP adresi için kullanılır.

![IGMP rapor Iletisi](./media/user-guide/igmp-report-message.png)

**ŞEKIL 8. IGMP rapor Iletisi**

Yukarıdaki şekilde (Şekil 8), ıGMP üstbilgisi bir sürüm/tür alanı, en fazla yanıt süresi, sağlama toplamı alanı ve çok noktaya yayın grubu adresi alanı içerir. IGMPv1 iletileri için, IGMPv1 protokolünün bir parçası olmadığından en fazla yanıt süresi alanı her zaman sıfır olarak ayarlanır. En fazla yanıt süresi alanı, ana bilgisayar bir sorgu türü bir ıGMP iletisi aldığında ayarlanır ve bir konak, IGMPv2 protokolü tarafından tanımlanan başka bir ana bilgisayarın rapor türü iletisini aldığında temizlenir.

Aşağıda, ıGMP üst bilgi biçimi açıklanmaktadır:

| **Üst bilgi alanı**          | **Amaç** |
|-----------------------|--------------------------------------------------------------------|
| Sürüm               | Bu alan, ıGMP sürümünü belirtir (BITS 31-28).                                                                               |
| Tür                  | Bu alan, ıGMP iletisinin türünü belirtir (BITS 27 -24).                                                                       |
| En fazla yanıt süresi | IGMPv1 içinde kullanılmıyor. IGMPv2 içinde bu alan en uzun yanıt süresi olarak görev yapar.                                                      |
| Sağlama              | Bu alan, ıGMP sürümünden başlayarak, ıGMP iletisinin tamamlama toplamı için 16 bit sağlama toplamı içerir (BITS 0-15) |
| Grup adresi         | 32-bit sınıfı D grup IP adresi |


IGMP rapor iletileri, çok noktaya yayın yönlendiricisi tarafından gönderilen ıGMP sorgu iletilerine yanıt olarak da gönderilir. Çok noktaya yayın yönlendiricileri, hangi konağın hala grup üyeliği gerektirdiğini görmek üzere sorgu iletilerini düzenli aralıklarla gönderir. Sorgu iletileri, Şekil 8 ' de gösterilen ıGMP rapor iletisiyle aynı biçimde olmalıdır. Tek farklar ıGMP türüdür ve grup adresi alanı 0 olarak ayarlanır. IGMP sorgu iletileri, çok noktaya yayın yönlendiricisi tarafından *tüm konaklar* IP adresine gönderilir. Grup üyeliğini sürdürmeye devam eden bir ana bilgisayar, başka bir ıGMP rapor iletisi göndererek yanıt verir.

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm iletilerin **Big endian** biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

### <a name="igmp-statistics-and-errors"></a>IGMP Istatistikleri ve hataları

Etkinleştirilirse, NetX ıGMP yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP 'nin ıGMP işlemi için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen toplam ıGMP raporu
- Alınan toplam ıGMP sorgusu sayısı
- Toplam ıGMP sağlama toplamı hataları
- Toplam ıGMP geçerli grup

Bu istatistik ve hata raporlarının tümü, ***nx_igmp_info_get*** hizmeti ile uygulama tarafından kullanılabilir.

## <a name="user-datagram-protocol-udp"></a>Kullanıcı veri birimi Protokolü (UDP)

Kullanıcı veri birimi Protokolü (UDP) ağ üyeleri arasında en basit veri aktarımı biçimini sağlar (RFC 768). UDP veri paketleri en iyi çabayla bir ağ üyesinden diğerine gönderilir; Yani, paket alıcısı tarafından onay için yerleşik bir mekanizma yoktur. Ayrıca, bir UDP paketinin gönderilmesi için herhangi bir bağlantının önceden kurulması gerekmez. Bu nedenle, UDP paket iletimi oldukça etkilidir.

### <a name="udp-header"></a>UDP üst bilgisi
UDP, iletim sırasında uygulamanın verilerinin önüne basit bir paket üst bilgisi koyar ve alınan bir UDP paketini uygulamaya teslim etmeden önce, Alım paketinden benzer bir UDP üst bilgisini kaldırır. UDP, paket ağda olduğunda UDP üst bilgisinin önünde bir IP üstbilgisi olduğu anlamına gelen paketleri göndermek ve almak için IP protokolünü kullanır. Şekil 9 ' da UDP üstbilgisinin biçimi gösterilmektedir.

![UDP üst bilgisi](./media/user-guide/udp-header.png)

**ŞEKIL 9. UDP üst bilgisi**

> [!IMPORTANT]
> *UDP/IP uygulamasındaki tüm üstbilgilerin big endian biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

Aşağıda UDP üst bilgi biçimi açıklanmaktadır:

| Üst bilgi alanı                   | Amaç |
|--------------------------------|---------------------------------------------|
| 16 bit kaynak bağlantı noktası numarası      | Bu alan, UDP paketinin gönderilme bağlantı noktasını içerir. Geçerli UDP bağlantı noktaları 1 ile 0xFFFF arasındadır. |
| 16 bit hedef bağlantı noktası numarası | Bu alan, paketin gönderildiği UDP bağlantı noktasını içerir. Geçerli UDP bağlantı noktaları 1 ile 0xFFFF arasındadır.   |
| 16 bit UDP uzunluğu   | Bu alan UDP paketindeki UDP üstbilgisinin boyutu da dahil olmak üzere bayt sayısını içerir.                                  |
| 16 bit UDP sağlama toplamı | Bu alan, paket için UDP üstbilgisi, paket veri alanı ve sözde IP üstbilgisi dahil olmak üzere 16 bit sağlama toplamı içerir. |

### <a name="udp-enable"></a>UDP etkinleştirme

UDP paket iletimi mümkün olmadan önce, uygulamanın öncelikle ***nx_udp_enable*** HIZMETINI çağırarak UDP 'yi etkinleştirmesi gerekir. Etkinleştirildikten sonra uygulama, UDP paketlerini göndermek ve almak için ücretsizdir.

### <a name="udp-socket-create"></a>UDP yuvası oluşturma

UDP yuvaları, başlatma sırasında veya çalışma zamanı sırasında uygulama iş parçacıkları tarafından oluşturulur. Hizmetin başlangıç türü, yaşam süresi ve alma sırası derinliği ***nx_udp_socket_create*** hizmeti tarafından tanımlanır. Bir uygulamadaki UDP yuvaları sayısında sınır yoktur.

### <a name="udp-checksum"></a>UDP sağlama toplamı

UDP, IP sahte üstbilgisini (kaynak IP adresi, hedef IP adresi ve protokol/uzunluk IP sözcükten oluşan), UDP üstbilgisini ve UDP paket verilerini içeren bir 16 bit tamamlama toplamı belirtir. Hesaplanan UDP sağlama toplamı 0 ise, hepsi (0xFFFF) olarak depolanır. Gönderme yuvasında UDP sağlama toplamı mantığı devre dışıysa, sağlama toplamı hesaplanmadığından, UDP sağlama toplamı alanına sıfır yerleştirilir. UDP sağlama toplamı, alıcı tarafından hesaplanan sağlama toplamıyla eşleşmezse, UDP paketi yalnızca atılır.

IP ağında, UDP sağlama toplamı isteğe bağlıdır. NetX, bir uygulamanın her yuva temelinde UDP sağlama toplamı hesaplamasını etkinleştirmesine veya devre dışı bırakmasına izin verir. Varsayılan olarak, UDP yuva sağlama toplamı mantığı etkindir. Uygulama, ***nx_udp_socket_checksum_disable*** hizmetini çağırarak belırlı bir UDP yuvası için sağlama mantığını devre dışı bırakabilir.

Belirli Ethernet denetleyicileri anında UDP sağlama toplamı üretebilir. Sistem donanım sağlama toplamı hesaplama özelliğini kullanabiliyor ise NetX kitaplığı sağlama toplamı mantığı olmadan oluşturulabilir. UDP yazılım sağlama toplamını devre dışı bırakmak için NetX kitaplığı, tanımlanan şu simgelerle oluşturulmalıdır: ***NX_DISABLE_UDP_TX_CHECKSUM*** ve ***NX_DISABLE_UDP_RX_CHECKSUM **_ ( [Bölüm 2](chapter2.md)' de açıklanmaktadır). Yapılandırma seçenekleri, NetX 'ten gelen UDP sağlama toplamı mantığını tamamen kaldırır, _* nx_udp_socket_checksum_disable hizmetini çağırmak*** , uygulamanın her yuva IÇIN IP UDP sağlama toplamı işlemesini devre dışı bırakmasına olanak sağlar.

### <a name="udp-ports-and-binding"></a>UDP bağlantı noktaları ve bağlama

UDP bağlantı noktası UDP protokolündeki bir mantıksal bitiş noktasıdır. NetX 'in UDP bileşeninde, 1 ile 0xFFFF arasında 65.535 geçerli bağlantı noktası vardır. UDP verileri göndermek veya almak için önce uygulamanın bir UDP yuvası oluşturması ve ardından bunu istenen bir bağlantı noktasına bağlaması gerekir. Bir UDP yuvasını bir bağlantı noktasına bağladıktan sonra, uygulama o yuvaya veri alıp alabilir.

### <a name="udp-fast-pathtrade"></a>UDP hızlı yolu&trade;

UDP hızlı yolu, &trade; NetX UDP uygulamasıyla düşük bir paket ek yükü yolunun adıdır. Bir UDP paketinin gönderilmesi yalnızca birkaç işlev çağrısını gerektirir: ***nx_udp_socket_send** _, _*_nx_ip_packet_send_*_ ve ağ sürücüsüne yapılan nihai çağrı. _*_nx_udp_socket_send_*_ , mevcut NETX uygulamaları Için NETX 'te kullanılabilir ve yalnızca IP paketleri için geçerlidir. Ancak tercih edilen yöntem, aşağıda açıklanan _ *_nx_udp_socket_send_** hizmetini kullanmaktır. UDP paket alımı üzerinde, UDP paketi uygun UDP yuvası alma kuyruğuna yerleştirilir veya ağ sürücüsünün alma kesme işleminden gelen tek bir işlev çağrısında askıya alınmış bir uygulama iş parçacığına dağıtılır. UDP paketlerinin gönderilmesi ve alınması için en iyi duruma getirilmiş bu mantık, UDP hızlı yol teknolojisinin özünü önemli bir yoldur.

### <a name="udp-packet-send"></a>UDP paketi gönderme

IP ağları üzerinden UDP verilerinin gönderilmesi, ***nx_udp_socket_send** _ işlevi çağırarak kolayca gerçekleştirilir. Çağıranın IP sürümünü _IP adresi * alanında ayarlaması gerekir. NetX, iletilen UDP paketlerinin hedef IP adresine göre en iyi kaynak adresini belirleyecek. Bu hizmet, paket verilerinin önüne bir UDP üst bilgisi koyar ve bir iç IP gönderme yordamı kullanarak ağı ağa gönderir. UDP paketlerinin gönderilmesi üzerinde hiçbir iş parçacığı askıya alınmaz çünkü tüm UDP paket aktarımları hemen işlenir.

Çok noktaya yayın veya yayın hedefleri için, NetX cihazında aralarından seçim yapabileceğiniz birden çok IP adresi varsa uygulamanın kullanılacak kaynak IP adresini belirtmesi gerekir. Bu, Hizmetler ***nx_udp_socket_interface_send yapılabilir.***

> [!IMPORTANT]
> *Çok noktaya yayın veya yayın paketlerini iletmek için **nx_udp_socket_send** kullanılıyorsa, Ilk arabirimin IP adresi kaynak adres olarak kullanılır.*

> [!IMPORTANT]
> *Bu yuva için UDP sağlama toplamı mantığı etkinleştirilmişse, sağlama iş parçacığı bağlamında, UDP veya IP veri yapılarına erişimi engellemeden, sağlama toplamı işlemi yapılır.*

> [!NOTE]
> ***NX_PACKET** yapısında bulunan UDP yük verileri uzun bir sözcük sınırında bulunmalıdır. Uygulamanın, IP, IP ve fiziksel medya üstbilgilerini yerleştirmek için, önüne işaretçisi ve NETX için veri başlangıç işaretçisi arasında yeterli alan bırakması gerekir.*

### <a name="udp-packet-receive"></a>UDP paket alma

Uygulama iş parçacıkları, ***nx_udp_socket_receive*** çağırarak belirli BIR yuvadan UDP paketleri alabilir. Yuva alma işlevi, yuvanın alma sırasındaki en eski paketi sunar. Alma kuyruğunda paket yoksa, bir paket gelene kadar çağıran iş parçacığı askıya alabilir (isteğe bağlı bir zaman aşımı ile).

UDP alma paketi işleme (genellikle ağ sürücüsünün Alım kesme işleyicisinden çağrılır), paketi UDP yuvasının alma kuyruğuna yerleştirmekten veya bir paket için bekleyen ilk askıya alınan iş parçacığına teslim etmekten sorumludur. Paket sıraya alınmışsa, alma işlemi, yuvada ilişkili en fazla alma sırası derinliğini de denetler. Bu yeni kuyruğa alınan paket sıra derinliğini aşarsa, sıradaki en eski paket atılır.

### <a name="udp-receive-notify"></a>UDP alma bildirimi

Uygulama iş parçacığının birden fazla yuvada alınan verileri işlemesi gerekiyorsa ***nx_udp_socket_receive_notify*** işlevi kullanılmalıdır. Bu işlev, yuva için bir alma paketi geri çağırma işlevi kaydeder. Yuvada her bir paket alındığında geri çağırma işlevi yürütülür.

Geri çağırma işlevinin içeriği uygulamaya özgüdür. Ancak büyük olasılıkla işleme iş parçacığını, ilgili yuvada artık kullanılabilir olduğunu bildirmek için mantık içerebilir.

### <a name="peer-address-and-port"></a>Eş adresi ve bağlantı noktası

Bir UDP paketi alındığında, uygulama, hizmet ***nx_udp_packet_info_extract*** kullanarak gönderenin IP adresini ve bağlantı noktası numarasını bulabilir. Başarılı bir geri döndüğünüzde, bu hizmet gönderenin IP adresi, gönderenin bağlantı noktası numarası ve paketin alındığı yerel arabirim hakkındaki bilgileri sağlar.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Daha önce belirtildiği gibi, uygulama iş parçacıkları belirli bir UDP bağlantı noktasında UDP paketi alınmaya çalışılırken askıya alabilir. Bu bağlantı noktasında bir paket alındıktan sonra, bu, askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı daha sonra sürdürülür. Çok sayıda NetX hizmeti için kullanılabilen bir UDP alma paketindeki bir özelliği askıya alırken isteğe bağlı bir zaman aşımı kullanılabilir.

### <a name="udp-socket-statistics-and-errors"></a>UDP yuvası Istatistikleri ve hataları

Etkinleştirilirse, NetX UDP yuva yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP/UDP örneği için aşağıdaki istatistikler ve hata raporları korunur:

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

Bu istatistik ve hata raporlarının tümü, tüm UDP yuvaları üzerinden UDP istatistikleri amassed için ***nx_udp_info_get*** hizmeti ve belirtilen UDP yuvasında UDP istatistikleri için ***nx_udp_socket_info_get*** hizmeti ile kullanılabilir.

### <a name="udp-socket-control-block-nx_udp_socket"></a>UDP yuva denetim bloğu NX_UDP_SOCKET

Her UDP yuvasının özellikleri, ilişkili **NX_UDP_SOCKET** denetim bloğunda bulunur. IP veri yapısına bağlantı, gönderme ve alma yolları için ağ arabirimi, bağlantı noktası ve alma paketi kuyruğu gibi yararlı bilgiler içerir. Bu yapı **_nx_api. h_** dosyasında tanımlanmıştır.

## <a name="transmission-control-protocol-tcp"></a>İletim Denetimi Protokolü (TCP)

Iletim Denetim Protokolü (TCP) iki ağ üyesi arasında güvenilir akış veri aktarımı sağlar (RFC 793). Bir ağ üyesinden gönderilen tüm veriler, alıcı üye tarafından doğrulanır ve onaylanır. Ayrıca, iki üyenin herhangi bir veri aktarımından önce bir bağlantı oluşturmuş olması gerekir. Tüm bu sonuçlar güvenilir veri aktarımına sahiptir; Ancak, daha önce açıklanan UDP veri aktarımından daha fazla ek yük gerektirir.

### <a name="tcp-header"></a>TCP üst bilgisi

İletim sırasında TCP üstbilgisi, kullanıcıdan verilerin önüne yerleştirilir. Alma sırasında TCP üstbilgisi, gelen paketten kaldırılır ve yalnızca uygulamanın kullanabildiği Kullanıcı verileri bırakılır. TCP, paket ağda olduğunda TCP üst bilgisinin önünde bir IP üstbilgisi olduğu anlamına gelen paketleri göndermek ve almak için IP protokolünü kullanır. Şekil 10 ' da TCP üstbilgisinin biçimi gösterilmektedir.

![TCP üst bilgisi](./media/user-guide/tcp-header.png)

**ŞEKIL 10. TCP üst bilgisi**

Aşağıda TCP üst bilgi biçimi açıklanmaktadır:

| Üst bilgi alanı | Amaç |
|---|---|
| 16 bit kaynak bağlantı noktası numarası | Bu alan, TCP paketinin gönderilme bağlantı noktasını içerir. Geçerli TCP bağlantı noktaları 1 ile 0xFFFF arasında değişir. |
| 16 bit hedef bağlantı noktası numarası | Bu alan, paketin gönderildiği TCP bağlantı noktasını içerir. Geçerli TCP bağlantı noktaları 1 ile 0xFFFF arasında değişir. |
| 32-bit sıra numarası | Bu alan, bağlantının bu sonundan gönderilen verilerin sıra numarasını içerir. Özgün sıra, iki TCP düğümü arasındaki ilk bağlantı sırası sırasında oluşturulur. Bu noktadan her veri aktarımı, gönderilen toplam bayt sayısına göre sıra numarası artışını elde ediyor. |
| 32-bit onay numarası | Bu alan, bağlantının bu tarafında alınan son bayta karşılık gelen sıra numarasını içerir. Bu, daha önce gönderilen verilerin bağlantının diğer ucundan başarıyla alındığını belirlemekte kullanılır. |
| 4 bit üst bilgi uzunluğu           | Bu alan, TCP üstbilgisindeki 32 bitlik sözcüklerin sayısını içerir. TCP üstbilgisinde bir seçenek yoksa, bu alan 5 ' tir. |
| 6 bit kod bitleri               | Bu alan, bağlantıyla ilişkili çeşitli denetim bilgilerini belirtmek için kullanılan altı farklı kod bitini içerir. Denetim bitleri aşağıdaki gibi tanımlanır: |



| Name | Sürümleri | Anlamı                                                     |
|------|-----|-------------------------------------------------------------|
| URG  | 21  | Acil veriler var                                         |
| ONAY  | 20  | Onay numarası geçerli                             |
| PSH  | 19  | Bu verileri hemen işle                                |
| K  | 18  | Bağlantıyı sıfırlama                                        |
| EŞITLEMEYE  | 17  | Sıra numaralarını (bağlantı kurmak için kullanılır) eşitler |
| FIN  | 16  | Gönderici iletim ile tamamlandı (bağlantıyı kapatmak için kullanılır) |

**16 bit pencere**

Bu alan akış denetimi için kullanılır. Bu, yuvanın Şu anda alabileceği bayt miktarını içerir. Bu temel olarak Flow denetimi için kullanılır. Gönderen verilerin alıcının tanıtılan penceresine sığdırmasını sağlamaktan gönderici sorumludur.

| **Üst bilgi alanı**          | **Amaç** |
| ------------------------- | --- |
| **16 bit TCP sağlama toplamı**   | Bu alan, paket için TCP üst bilgisi, paket veri alanı ve sözde IP üstbilgisi dahil olmak üzere 16 bit sağlama toplamı içerir.                |
| **16 bit acil işaretçi** | Bu alan, acil verilerin son baytının pozitif sapmasını içerir. Bu alan yalnızca üst bilgide URG kod biti ayarlandıysa geçerlidir. |

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm üstbilgilerin big endian biçimde olması beklenir. Bu biçimde, sözcüğün en önemli baytı en düşük bayt adresinde bulunur.*

### <a name="tcp-enable"></a>TCP etkinleştirme

TCP bağlantıları ve paket aktarımları mümkün olmadan önce, uygulamanın öncelikle nx_tcp_enable hizmetini çağırarak TCP 'yi etkinleştirmesi gerekir. Etkinleştirildikten sonra, uygulama tüm TCP hizmetlerine erişmeye ücretsizdir.

### <a name="tcp-socket-create"></a>TCP yuvası oluşturma

TCP yuvaları, başlatma sırasında veya çalışma zamanı sırasında uygulama iş parçacıkları tarafından oluşturulur. Hizmetin başlangıç türü, yaşam süresi ve pencere boyutu ***nx_tcp_socket_create*** hizmeti tarafından tanımlanır. Bir uygulamadaki TCP yuvaları sayısında sınır yoktur.

### <a name="tcp-checksum"></a>TCP sağlama toplamı

TCP, IP sahte üstbilgisini (kaynak IP adresi, hedef IP adresi ve protokol/uzunluk IP sözcükten oluşan), TCP üstbilgisini ve TCP paketi verilerini içeren bir 16 bit tamamlama toplamı belirtir.

Bazı ağ denetleyicileri donanımda TCP sağlama toplamı hesaplaması ve doğrulaması gerçekleştirebilir. Uygulamalar, bu tür sistemler için, çalışma zamanı yükünü azaltmak için mümkün olduğunca donanım sağlama mantığını kullanmak isteyebilir. Uygulamalar, **NX_DISABLE_TCP_TX_CHECKSUM** ve **NX_DISABLE_TCP_RX_CHECKSUM** tanımlayarak derleme zamanında NETX kitaplığından tamamen TCP sağlama toplamı hesaplama mantığını devre dışı bırakabilir. Bu şekilde, TCP sağlama toplamı kodu ' de derlenmez.

### <a name="tcp-port"></a>TCP Bağlantı Noktası

TCP bağlantı noktası, TCP protokolünde bir mantıksal bağlantı noktasıdır. NetX TCP bileşeninde, 1 ile 0xFFFF arasında 65.535 geçerli bağlantı noktası vardır. Bir bağlantı noktasındaki verilerin diğer hedef bağlantı noktalarına gönderilebileceği UDP 'nin aksine, bir TCP bağlantı noktasının başka bir belirli TCP bağlantı noktasına bağlı olması ve yalnızca bu bağlantı kurulduğu zaman, bağlantıyı oluşturan iki bağlantı noktası arasında olması gerekir.

> [!IMPORTANT]
> *TCP bağlantı noktaları UDP bağlantı noktalarından tamamen ayrıdır; Örneğin, UDP bağlantı noktası numarası 1, TCP bağlantı noktası numarası 1 ile ilişki içermez.*

## <a name="client-server-model"></a>Client-Server modeli

Veri aktarımı için TCP kullanmak üzere iki TCP yuvası arasında bir bağlantı kurulması gerekir. Bağlantının kurulması, istemci-sunucu düzeyinde yapılır. Bağlantının istemci tarafı bağlantıyı başlatan tarafdayken, sunucu tarafı herhangi bir işlem yapılmadan önce istemci bağlantı isteklerini bekler.

> [!IMPORTANT]
> *Çok ana cihazlarda NetX, bağlantı için kullanılacak kaynak adresini ve bağlantının hedef IP adresine göre sonraki atlama adresini otomatik olarak belirler.*

### <a name="tcp-socket-state-machine"></a>TCP yuva durumu makinesi

İki TCP yuvası (bir istemci ve bir sunucu) arasındaki bağlantı karmaşıktır ve bir durum makinesi halinde yönetilir. Her TCP yuvası kapalı bir durumda başlar. Bağlantı olayları aracılığıyla her bir yuvanın durum makinesi, TCP 'deki veri aktarımının toplu olarak gerçekleştiği, kurulan duruma geçirilir. Bağlantının bir tarafı artık veri göndermek istediğinde, bağlantısını keser. Diğer tarafın bağlantısı kesildiğinde, TCP yuvası kapalı duruma geri döner. Bu işlem, bir TCP istemcisi ve sunucusu bir bağlantı kurup her kapatışınızda yinelenir. Şekil 11, TCP durum makinesinin çeşitli durumlarını gösterir.

![TCP durum makinesinin durumları](./media/user-guide/states-tcp-state-machine.png)

### <a name="figure-11-states-of-the-tcp-state-machine"></a>ŞEKIL 11. TCP durum makinesinin durumları

### <a name="tcp-client-connection"></a>TCP Istemci bağlantısı

Daha önce belirtildiği gibi, TCP bağlantısının istemci tarafı bir TCP sunucusuna bağlantı isteği başlatır. Bir bağlantı isteğinin yapılabilmesi için, istemci IP örneğinde TCP 'nin etkinleştirilmesi gerekir. Ayrıca, istemci TCP yuvasının daha sonra ***nx_tcp_socket_create** _ hizmeti ile oluşturulması ve _*_nx_tcp_client_socket_bind_*_ hizmeti aracılığıyla bir bağlantı noktasına bağlanması gerekir. İstemci yuvası bağlandıktan sonra, bir TCP sunucusuyla bağlantı kurmak için _ *_nx_tcp_client_socket_connect_** hizmeti kullanılır. Bir bağlantı denemesi başlatmak için yuvanın kapalı durumda olması gerektiğini aklınızda olun. Bağlantıyı kurmak bir SYN paketi veren NetX ile başlar ve sonra bağlantı isteğinin kabul edildiğini belirten bir SYN ACK paketini sunucudan geri bekler. SYN ACK alındıktan sonra NetX bir ACK paketiyle yanıt verir ve istemci yuvasını belırlenen duruma yükseltir.

### <a name="tcp-client-disconnection"></a>TCP Istemcisi bağlantısı kesilmesi

Bağlantıyı kapatmak ***nx_tcp_socket_disconnect*** çağırarak gerçekleştirilir. Askıya alma belirtilmemişse, istemci yuvası sunucu yuvasına bir RST paketi gönderir ve yuvayı kapalı duruma koyar. Aksi takdirde, askıya alma isteniyorsa, tam TCP bağlantı kesme protokolü aşağıdaki gibi gerçekleştirilir:

- Sunucu daha önce bir bağlantı kesme isteği başlatmışsa (istemci soketi bir FIN paketi zaten aldıysa, bir ACK ile yanıt verdi ve kapatma bekleme durumundaysa), NetX istemci TCP yuvası durumunu son ACK durumuna yükseltir ve bir FIN paketi gönderir. Ardından, bağlantıyı kesmeden ve kapalı durumu girerek sunucudan bir ACK 'i bekler.

- Öte yandan istemci, bir bağlantı kesme isteği başlatmakta (sunucu bağlantısı kesilmemiştir ve yuva hala kurulu durumdaysa), NetX bağlantı kesmeyi başlatmak için bir FIN paketi gönderir ve bağlantı kesmeyi tamamlamadan ve yuvayı kapalı bir duruma yerleştirerek sunucudan bir FIN ve bir ACK alıp almamayı bekler.

Yuva iletme kuyruğunda hala paketler varsa, NetX, paketlerin onaylanılmasına izin vermek için belirtilen zaman aşımı süresini askıya alır. Zaman aşımı süresi dolarsa NetX, istemci yuvasının iletim sırasını boşaltır.

İstemci yuvasıyla bağlantı noktasının bağlantısını kesmek için uygulama ***nx_tcp_client_socket_unbind*** çağırır. Yuva, bağlantı noktası yayınlanmadan önce kapalı durumda veya bağlantısının kesilmesi (örneğin, SÜRELI bekleme durumu) işleminde olmalıdır; Aksi takdirde bir hata döndürülür.

Son olarak, uygulama artık istemci yuvasına ihtiyaç duymuyorsa, yuvasını silmek için ***nx_tcp_socket_delete*** çağırır.

### <a name="tcp-server-connection"></a>TCP sunucusu bağlantısı

TCP bağlantısının sunucu tarafı pasif olur; Yani, sunucu bir istemcinin bağlantı isteği başlatmasını bekler. İstemci bağlantısını kabul etmek için, önce TCP **nx_tcp_enable** _ HIZMETINI çağırarak IP örneğinde TCP 'nin etkinleştirilmesi gerekir. Daha sonra, uygulamanın _ *_nx_tcp_socket_create_** hizmetini kullanarak bir TCP yuvası oluşturması gerekir.

Sunucu yuvası, bağlantı isteklerini dinlemek için de ayarlanmalıdır. Bu, ***nx_tcp_server_socket_listen*** hizmeti kullanılarak elde edilir. Bu hizmet, sunucu yuvasını dınleme durumuna koyar ve belirtilen sunucu bağlantı noktasını yuvaya bağlar.

> [!IMPORTANT]
> *Bir yuva dinleme geri çağırma yordamı ayarlamak için, uygulama **nx_tcp_server_socket_listen** hizmetinin tcp_listen_callback bağımsız değişkeni için uygun geri çağırma işlevini belirtir. Bu uygulama geri çağırma işlevi, bu sunucu bağlantı noktasında her yeni bağlantı istendiğinde NetX tarafından yürütülür. Geri çağırmada işlem uygulama denetimi altında.*

İstemci bağlantı isteklerini kabul etmek için, uygulama ***nx_tcp_server_socket_accept** _ hizmetini çağırır. Sunucu yuvası, bir dınleme durumunda ya da SYN ALıNDı durumunda olmalıdır (yani, sunucu dınleme durumunda ve bağlantı isteyen bir istemciden bir SYN paketi aldı), kabul etme hizmetini çağırmak için. _ *_Nx_tcp_server_socket_accept_** öğesinden başarılı bir dönüş durumu, bağlantının ayarlandığını ve sunucu yuvasının kurulu durumda olduğunu gösterir.

Sunucu yuvasının geçerli bir bağlantısı olduktan sonra, ek istemci bağlantı istekleri, ***nx_tcp_server_socket_listen** _ hizmetine geçirilen *listen_queue_size* tarafından belirtilen derinliğe göre sıralanır. Bir sunucu bağlantı noktasında sonraki bağlantıları işlemek için, uygulama _ *_nx_tcp_server_socket_relisten_** öğesini kullanılabilir bir yuva (yani kapalı durumda olan bir yuva) ile çağırmalıdır. Yuva ile ilişkili önceki bağlantı artık tamamlanıp ve yuva kapalı durumdaysa aynı sunucu yuvasının kullanılabileceğini unutmayın.

### <a name="tcp-server-disconnection"></a>TCP sunucusu bağlantısının kesilmesi

Bağlantıyı kapatmak ***nx_tcp_socket_disconnect*** çağırarak gerçekleştirilir. Askıya alma belirtilmemişse, sunucu yuvası istemci yuvasına bir RST paketi gönderir ve yuvayı kapalı duruma koyar. Aksi takdirde, askıya alma isteniyorsa, tam TCP bağlantı kesme protokolü aşağıdaki gibi gerçekleştirilir: |

- İstemci daha önce bir bağlantı kesme isteği başlatmışsa (sunucu soketi bir FIN paketi zaten aldıysa, bir ACK ile yanıtladı ve kapatma bekleme durumundaysa), NetX TCP yuvası durumunu son ACK durumuna yükseltir ve bir FIN paketi gönderir. Ardından, bağlantıyı kesmeden ve kapalı durumu girerek istemciden bir ACK 'i bekler.

- Öte yandan sunucu, bir bağlantı kesme isteği başlatmakta (istemci bağlantısı kesilmemiştir ve yuva hala kurulu durumdaysa), NetX bağlantı kesmeyi başlatmak için bir FIN paketi gönderir ve bağlantı kesmeyi tamamlamadan ve yuvayı kapalı bir duruma yerleştirerek istemciden bir FIN ve bir ACK alıp almamayı bekler.

Yuva iletme kuyruğunda hala paketler varsa, NetX belirtilen zaman aşımı için bu paketlerin onaylanılmasına izin verir. Zaman aşımı süresi dolarsa NetX, sunucu yuvasının iletim sırasını boşaltır.

Bağlantı kesme işlemi tamamlandıktan ve sunucu yuvası kapalı durumdaysa, uygulamanın Bu yuvanın ilişkilendirmesini sunucu bağlantı noktasıyla sonlandırmak için ***nx_tcp_server_socket_unaccept*** hizmetini çağırması gerekir. ***Nx_tcp_socket_disconnect*** veya ***nx_tcp_server_socket_accept** _ bir hata durumu döndürse bile bu hizmetin uygulama tarafından çağrılması gerekir. _ *_Nx_tcp_server_socket_unaccept_** çağrıldıktan sonra, yuva istemci veya sunucu yuvası olarak kullanılabilir ya da artık gerekmiyorsa silinebilir. Aynı sunucu bağlantı noktasında başka bir istemci bağlantısını kabul etmeniz isteniyorsa, ***nx_tcp_server_socket_relisten*** hizmeti bu yuvada çağrılmalıdır.

Aşağıdaki kod segmenti tipik bir TCP sunucusunun kullandığı çağrıların dizisini gösterir:

```c
/* Set up a previously created TCP socket to listen on port 12 */

nx_tcp_server_socket_listen()

/* Loop to make a (another) connection. */
while(1) {

    /* Wait for a client socket connection request for 100 ticks. */
    nx_tcp_server_socket_accept();

    /* (Send and receive TCP messages with the TCP client) */

    /* Disconnect the server socket. */
    nx_tcp_socket_disconnect();

    /* Remove this server socket from listening on the port. */

    nx_tcp_server_socket_unaccept(&server_socket);

    /* Set up server socket to relisten on the same port for the next
    client. */
    nx_tcp_server_socket_relisten();
}
```

### <a name="mss-validation"></a>, Bu doğrulama

En büyük kesim boyutu (Bu), TCP ana bilgisayarının, temel alınan IP katmanı tarafından parçalanmadan alabileceği en yüksek bayt miktarıdır. TCP bağlantı kurma aşaması sırasında, gönderenin, alıcının alt bileşenlerinden daha büyük bir TCP veri segmenti göndermemesi için kendi TCP sahip olduğu değeri her iki sona erer. NetX TCP modülü, bağlantı kurmadan önce isteğe bağlı olarak, eşin tanıtılan bir değeri doğrular. Varsayılan olarak NetX bu tür bir denetimi etkinleştirmez. En düşük değer, bir NetX kitaplığı oluştururken ***NX_ENABLE_TCP_MSS_CHECKING** _ tanımlar ve en düşük değer _*_NX_TCP_MSS_MINIMUM_*_ olarak tanımlanır. _ *_NX_TCP_MSS_MINIMUM_** altındaki, bu değerleri IÇEREN gelen TCP bağlantıları bırakılır.

### <a name="stop-listening-on-a-server-port"></a>Sunucu bağlantı noktasında dinlemeyi durdur

Uygulama, daha önce ***nx_tcp_server_socket_listen** _ hizmeti çağrısıyla belirtilen bir sunucu bağlantı noktasındaki istemci bağlantı isteklerini dinlemek isterse, uygulama yalnızca _ *_nx_tcp_server_socket_unlisten_** hizmetini çağırır. Bu hizmet, bir bağlantıyı kapalı durumunda geri bekleyen bir yuva koyar ve sıraya alınan istemci bağlantı isteği paketlerini serbest bırakır.

### <a name="tcp-window-size"></a>TCP pencere boyutu

Bağlantının kurulum ve veri aktarımı aşamaları sırasında, her bağlantı noktası işleyebileceği veri miktarını rapor edebilir ve bu, pencere boyutu olarak adlandırılır. Veriler alınıp işlendiğinde, bu pencere boyutu dinamik olarak ayarlanır. TCP 'de, gönderici yalnızca alıcının penceresine sığan veri miktarı gönderebilir. Esas olarak pencere boyutu, bağlantının her yönünde veri aktarımı için akış denetimi sağlar.

### <a name="tcp-packet-send"></a>TCP paketi gönderme

TCP verilerinin gönderilmesi ***nx_tcp_socket_send*** işlevi çağırarak kolayca gerçekleştirilir. Aktarılan verilerin boyutu, yuvanın sahip olduğu değerin veya geçerli eş alma penceresi boyutunun (hangisi daha küçükse) daha büyükse, iletim için en az (örneğin, eş alma penceresi) olan verileri, TCP iç mantığını kapatır. Bu hizmet daha sonra paketin önünde (sağlama toplamı hesaplaması dahil) bir TCP üst bilgisi oluşturur. Alıcının pencere boyutu sıfır değilse, çağıran alıcının pencere boyutunu dolduracağı kadar veri gönderir. Alma penceresi sıfır olursa, çağıran, bu paketin gönderilmesi için alıcının pencere boyutunun yeterince artırılmasına izin verebilir ve bu işlemin boyutunu bekleyebilir. Belirli bir zamanda, aynı yuva üzerinden veri gönderilmeye çalışılırken birden çok iş parçacığı askıya alabilir.

> [!IMPORTANT]
> *NX_PACKET yapısında bulunan TCP verileri uzun bir sözcük sınırında bulunmalıdır. Buna ek olarak, TCP, IP ve fiziksel medya üstbilgilerini yerleştirmek için önüne işaretçisi ve veri başlangıç işaretçisi arasında yeterli alan olması gerekir.*

### <a name="tcp-packet-retransmit"></a>TCP paketi yeniden aktarım

Daha önce gönderilen TCP paketleri, bağlantının diğer tarafından bir ACK döndürülünceye kadar dahili olarak depolanır. Aktarılan veriler zaman aşımı süresi içinde onaylanmazsa, depolanan paket yeniden gönderilir ve sonraki zaman aşımı süresi ayarlanır. Bir ACK alındığında, iç aktarım sırasındaki onay numarası kapsamındaki tüm paketler son olarak serbest bırakılır.

> [!IMPORTANT]
> * Uygulama paketi yeniden kullanmamalıdır veya ***nx_tcp_socket_send** _ işlevi NX_SUCCESS geri döndüğünde paketin içeriğini değiştirmeyecektir. İletilen paket son olarak, veriler diğer end._ tarafından onaylandıktan sonra NetX iç işlemesi tarafından serbest bırakılır

### <a name="tcp-keepalive"></a>TCP KeepAlive

TCP KeepAlive özelliği, bir yuvanın, doğru sonlandırma olmadan (örneğin, eşler kilitlendi) veya belirli ağ izleme tesislerinin uzun süreler için bir bağlantıyı sonlandırmasını engellemek için bir yuva sağlar. TCP KeepAlive, veri içermeyen bir TCP çerçevesi göndererek ve sıra numarası geçerli sıra numarasından bir daha az olacak şekilde, düzenli aralıklarla işe yarar. Bu tür TCP KeepAlive çerçevesini alırken alıcı, hala etkin ise geçerli sıra numarası için bir ACK ile yanıtlar. Bu işlem, KeepAlive işlemini tamamlar.

Varsayılan olarak, KeepAlive özelliği etkin değildir. Bu özelliği kullanmak için NetX Kitaplığı ***NX_ENABLE_TCP_KEEPALIVE** _ tanımlı ile oluşturulmalıdır. _ *_NX_TCP_KEEPALIVE_INITIAL_** sembolü, KEEPALIVE çerçevesi başlatılmadan önce geçen işlem yapılmayan saniye sayısını belirtir.

### <a name="tcp-packet-receive"></a>TCP paket alma

TCP alma paketi işleme (IP Yardımcısı iş parçacığından çağrılır), çeşitli bağlantı ve bağlantı kesme eylemlerinin yanı sıra iletme bildirimi işleme işleminden sorumludur. Ayrıca, TCP alma paketi işleme, uygun TCP yuvasının alma kuyruğuna veri alma veya paketi bekleyen ilk askıya alınan iş parçacığına paket teslim etme işleminden sorumludur.

### <a name="tcp-receive-notify"></a>TCP alma bildirimi

Uygulama iş parçacığının birden fazla yuvada alınan verileri işlemesi gerekiyorsa ***nx_tcp_socket_receive_notify*** işlevi kullanılmalıdır. Bu işlev, yuva için bir alma paketi geri çağırma işlevi kaydeder. Yuvada her bir paket alındığında geri çağırma işlevi yürütülür.

Geri çağırma işlevinin içeriği uygulamaya özgüdür; Ancak, işlev büyük olasılıkla işleme iş parçacığını bir paketin ilgili yuvada kullanılabilir olduğunu bildirmek için mantık içerebilir.

### <a name="thread-suspension"></a>İş parçacığı askıya alma

Daha önce belirtildiği gibi, uygulama iş parçacıkları belirli bir TCP bağlantı noktasından veri almaya çalışırken askıya alabilir. Bu bağlantı noktasında bir paket alındıktan sonra, bu, askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı daha sonra sürdürülür. Çok sayıda NetX hizmeti için kullanılabilen bir TCP alma paketi üzerinde askıya alma sırasında isteğe bağlı bir zaman aşımı kullanılabilir.

İş parçacığı askıya alma, bağlantı (istemci ve sunucu), istemci bağlama ve bağlantı kesme hizmetleri için de kullanılabilir.

### <a name="tcp-socket-statistics-and-errors"></a>TCP yuvası Istatistikleri ve hataları

Etkinleştirilirse, NetX TCP yuvası yazılımı, uygulama için yararlı olabilecek çeşitli istatistik ve hataları izler. Her IP/TCP örneği için aşağıdaki istatistikler ve hata raporları korunur:

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

## <a name="tcp-socket-control-block-nx_tcp_socket"></a>TCP yuvası denetim bloğu NX_TCP_SOCKET

Her TCP yuvasının özellikleri, IP veri yapısına, ağ bağlantı arabirimine, bağlı bağlantı noktasına ve alma paketi kuyruğuna bağlantı gibi yararlı bilgiler içeren ilişkili *NX_TCP_SOCKET* denetim bloğunda bulunur. Bu yapı ***nx_api. h*** dosyasında tanımlanmıştır.
