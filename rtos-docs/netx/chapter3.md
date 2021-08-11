---
title: Bölüm 3-Azure RTOS NetX 'in Işlevsel bileşenleri
description: Bu bölüm, işlevsel bir perspektiften yüksek performanslı Azure RTOS NetX TCP/IP yığınının bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4ebb002bc82d13210acf8db44cafb141d33a1b45fa8710295437e2dd15cbcf22
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784409"
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
IP örneğindeki arabirim denetim bloklarının sayısı, fiziksel arabirimlerin sayısıdır (***NX_MAX_PHYSICAL_INTERFACES** _ tarafından tanımlanır) ve etkinse geri döngü arabirimi. Toplam arabirim sayısı __*_ ve **NX_MAX_IP_INTERFACES tanımlanır.

## <a name="protocol-layering"></a>Protokol Katmanlama

NetX tarafından uygulanan TCP/IP katmanlı bir protokoldür, yani daha karmaşık protokoller temel alınan daha basit protokoller üzerine inşa edilmiştir. TCP/IP'de, en düşük katman protokolü *Bağlantı* Katmanı'ndadır ve ağ sürücüsü tarafından iş birliği yapılan bir protokoldür. Bu düzey genellikle Ethernet'e yöneliktir, ancak fiber, seri veya neredeyse tüm fiziksel medyalar da olabilir.

Bağlantı katmanının üst kısmında Ağ katmanı *yer ağına yer verir.* TCP/IP'de bu, ağ genelinde en iyi çabayla basit paketleri göndermekten ve almakla sorumlu olan IP'dir. ICMP ve IGMP gibi yönetim türü protokolleri, gönderme ve alma için IP'ye bağlı olsalar bile genellikle ağ katmanları olarak kategorilere ayrılmıştır.

Aktarım *katmanı,* ağ katmanının üzerinde yer almaktadır. Bu katman, ağ üzerinde konaklar arasında veri akışını yönetmekle sorumludur. NetX tarafından desteklenen iki tür aktarım hizmeti vardır: UDP ve TCP. UDP hizmetleri iki konak arasında bağlantısız bir şekilde veri göndermek ve almak için en iyi çabayı sunarken, TCP iki konak varlığı arasında güvenilir bağlantı odaklı hizmet sağlar.

Bu katman gerçek ağ veri paketlerine yansıtıldı. TCP/IP'de her katman üst bilgi olarak adlandırılan bir bilgi bloğu içerir. Bir üst bilgi ile verileri (ve muhtemelen protokol bilgilerini) çevreleyen bu teknik genellikle veri kapsülleme olarak adlandırılan bir tekniktir. Şekil 1'de NetX katmanlama örneği, Şekil 2'de ise gönderilen UDP verileri için elde edilen veri kapsüllemesi yer almaktadır.

![Protokol Katmanlama](./media/user-guide/protocol-layering.png)

**ŞEKIL 1. Protokol Katmanlama**

![UDP Veri Kapsüllemesi](./media/user-guide/udp-data-encapsulation.png)

**ŞEKIL 2. UDP Veri Kapsüllemesi**

## <a name="packet-pools"></a>Paket Havuzları

Paketlerin hızlı ve belirlenimci bir şekilde belirlenmesi, gerçek zamanlı ağ uygulamalarında her zaman bir zorlukdur. NetX, bu nedenle sabit boyutlu ağ paketlerinin birden çok havuzu oluşturma ve yönetme olanağı sağlar.

NetX paket havuzları sabit boyutlu bellek bloklarından oluşan olduğundan, hiçbir zaman iç parçalanma sorunu oluşturmaz. Elbette parçalanma, doğası gereği belirlenemeyen davranışlara neden olur.

Ayrıca, bir NetX paketi ayırmak ve serbest bırakma süresi basit bağlantılı liste işlemeye tutar. Ayrıca paket ayırma ve ayırma işlemleri kullanılabilir listenin başında yapılır. Bu, mümkün olan en hızlı bağlantılı liste işlemeyi sağlar.

Esneklik eksikliği genellikle sabit boyutlu paket havuzlarının temel dezavantajıdır. En kötü durum gelen paketi de işleyecek en uygun paket yükü boyutunu belirlemek zor bir görevdir. NetX paketleri, paket zincirleme adlı isteğe bağlı bir özellikle *bu sorunu ele almaktadır.* Gerçek bir ağ paketi, birbirine bağlı bir veya daha fazla NetX paketinden olabilir. Ayrıca, paket üst bilgisi paketin üst kısmında bir işaretçi bulundurrarak. Ek protokoller eklendiklerine göre bu işaretçi geriye doğru taşınır ve yeni üst bilgi doğrudan verilerin önüne yazılır. Esnek paket teknolojisi olmadan, yığının başka bir arabellek ayırması ve verileri yeni üst bilgiyle yeni bir arabelleğe kopyalaması gerekir ve bu da yoğun bir işlemdir.

Belirli bir paket havuzu için her paket yükü boyutu sabit olduğu için, yük boyutundan büyük uygulama verileri birden çok paketin birbirine zincirle bağlı olması gerekir. Bir paketi kullanıcı verileriyle doldururken, uygulamanın ***nx_packet_data_append.*** Bu hizmet uygulama verilerini bir pakete taşır. Bir paketin kullanıcı verilerini tutmak için yeterli olduğu durumlarda, kullanıcı verilerini depolamak için ek paketler ayrılır. Paket zinciri kullanmak için, sürücünün zincirlenmiş paketlere alalı veya zincirli paketlerden aktaranı olması gerekir.

Her NetX paket bellek havuzu genel bir kaynaktır. NetX, paket havuzlarının nasıl kullanıldıklarına hiçbir kısıtlama uygulamaz.

### <a name="packet-pool-memory-area"></a>Paket Havuzu Bellek Alanı
Paket havuzunun bellek alanı oluşturma sırasında belirtilir. ThreadX ve NetX nesnelerinin diğer bellek alanları gibi, hedefin adres alanı içinde herhangi bir yerde yer alıyor olabilir. Uygulamaya verdiği önemli esneklik nedeniyle bu önemli bir özelliktir. Örneğin, bir iletişim ürününün ağ arabellekleri için yüksek hızlı bir bellek alanına sahip olduğunu varsayalım. Bu bellek alanı, bir NetX paket bellek havuzuna dönüştürerek kolayca kullanılır.

### <a name="creating-packet-pools"></a>Paket Havuzları Oluşturma
Paket havuzları başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. NetX uygulamasındaki paket bellek havuzlarının sayısıyla ilgili bir sınır yoktur.

### <a name="packet-header-nx_packet"></a>Paket Üst Bilgisi NX_PACKET
Varsayılan olarak, NetX paket üst bilgilerini paket yükü alanından hemen önce yer alır. Paket bellek havuzu temelde bir paket dizisidir; hemen ardından paket yükü gelen üst bilgiler. Paket üst bilgisi (***NX_PACKET***) ve paket havuzunun düzeni Şekil 3'te görüntülanmıştır.

Sıfır kopyalama işlemi gerçekleştirebilecek ağ cihazları sürücüsü için, genellikle paket yükü alanı başlangıç adresi DMA mantığına programlanır. Bazı DMA altyapılarının yük alanında hizalama gereksinimi vardır.

> [!IMPORTANT]
> *Bir paketin iletimi tamamlandığında ***nx_packet_transmit_release** _ işlevini çağıran ağ sürücüsü. Bu işlev, paketin kullanılabilir havuza geri yerleştirilmeden önce tcp çıkış kuyruğuna parçası olmadığını denetler. Bu işlevin çağrılma başarısız olması öngörülemeyen hatalara behavior._

![Paket Üst Bilgisi ve Paket Havuzu Düzeni](./media/user-guide/packet-header-packet-pool-layout.png)

**ŞEKIL 3. Paket Üst Bilgisi ve Paket Havuzu Düzeni**

Paket üst bilgisi alanları aşağıdaki tabloda gösterildiği gibi tanımlanır. Bu tablonun, tablo yapısında yer alan tüm üyelerin kapsamlı *NX_PACKET* unutmayın.

| Paket üst bilgisi          | Amaç                                                                                                                                                                                                                                                                                                                            |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *nx_packet_pool_owner*   | Bu alan, bu paketin sahibi olan paket havuzunu belirtir. Paket serbest bırakılana kadar bu havuza serbest bırakıldı. Her paketin içindeki havuz sahipliğiyle, bir veri biriminin birden çok paket havuzundan birden çok pakete yayması mümkündür.                                                         |
| *nx_packet_next*         | Bu alan, aynı çerçeve içindeki sonraki paketi gösterir. NULL ise, çerçevenin parçası olan ek paket yoktur. |
| *nx_packet_last*         | Bu alan, aynı ağ paketi içindeki son paketi belirtir. NULL ise, bu paket tüm ağ paketini temsil eder.  |
| *nx_packet_length*       | Bu alan, ağ paketinin tamamına üye tarafından zincirlenmiş tüm paketlerde yer alan tüm baytların toplamı da dahil olmak üzere *toplam bayt nx_packet_next* içerir. |
| *nx_packet_ip_interface* | Bu alan, arabirim sürücüsü tarafından alınan pakete ve giden paketler için NetX tarafından atanan arabirim denetim bloğu olur. Arabirim denetim bloğu; ağ adresi, MAC adresi, IP adresi ve bağlantı etkin ve gerekli fiziksel eşleme gibi arabirim durumu gibi arabirimi açıklar. |
| *nx_packet_data_start*   | Bu alan, bu paketin fiziksel yük alanı başlangıcını belirtir. NX_PACKET üst NX_PACKET hemen takip etmek zorunda değildir, ancak nx_packet_pool_create için ***varsayılan*** değerdir. |
| *nx_packet_data_end*     | Bu alan, bu paketin fiziksel yük alanını belirtir. Bu alanla veri alanı arasındaki nx_packet_data_start yük boyutunu temsil eder. |
| *nx_packet_prepend_ptr*  | Bu alan, paket yükü alanında var olan paket verileri (varsa) önüne protokol üst bilgisi veya gerçek veri olarak paket verisi eklenmiştir. Bu değer, işaretçi konumunun üzerinde veya *nx_packet_data_start* ve işaretçi işaretçisine eşit veya daha *nx_packet_append_ptr* gerekir.  *Performans nedenleriyle NetX, paket iletim için NetX hizmetlerine geçiriken, ön uç işaretçisinin uzun sözcükle hizalanmış adresi işaret ediyor olduğunu varsayıyor.* |
| *nx_packet_append_ptr*    | Bu alan, şu anda paket yükü alanında bulunan verilerin sonuna belirtir. Nx_packet_prepend_ptr ve tarafından işaret eden bellek *konumu nx_packet_data_end.*  Bu alanla alan arasındaki *nx_packet_prepend_ptr* alanı, bu pakette yer alan veri miktarını temsil eder. |
| *nx_packet_fragment_next* | Bu alan, paketin tamamı yeniden derlenene kadar parçalanmış paketleri tutmak için kullanılır. |
| *nx_packet_pad*           | Bu alanlar, istenen hizalama gereksinimini elde etmek için 4-byte sözcükleriyle doldurma uzunluğunu tanımlar. Bu alan, *NX_PACKET_HEADER_PAD* kaldırılır. |
|  |  |

### <a name="packet-header-offsets"></a>Paket Üst Bilgisi Uzaklıkları

Paket üst bilgisi boyutu, üst bilgi boyutuna yetecek kadar alan sağlayacak şekilde tanımlanır. Nx_packet_allocate  hizmeti bir paket ayırmak için kullanılır ve pakette ön uç işaretçisini belirtilen paket türüne göre ayarlar. Paket türü, Protokol verisi önüne protokol üst bilgisi (UDP, TCP veya ICMP gibi) eklemek için gereken uzaklığı NetX'e söyler.

Pakette IP üst bilgisi ve fiziksel katman (Ethernet) üst bilgisi dikkate alınarak NetX'te aşağıdaki türler tanımlanmıştır. İkinci durumda, gerekli 4 bayt hizalamayı dikkate alarak 16 bayt olduğu varsayılır. Ip paketleri, uygulamaların IP ağları için paket ayırması için NetX'te hala tanımlanmıştır. Aşağıdaki tabloda tanımlanmış semboller yer alır:

| Paket Türü   | Değer |
|---------------|-------|
| NX_IP_PACKET  | 0x24  |
| NX_UDP_PACKET | 0x2c  |
| NX_TCP_PACKET | 0x38  |
|               |       |

### <a name="pool-capacity"></a>Havuz Kapasitesi
Paket havuzudaki paket sayısı, yük boyutuna ve paket havuzu oluşturma hizmetine sağlanan bellek alanında yer alan toplam bayt sayısına sahip bir işlevdir. Havuzun kapasitesi, paket boyutu (NX_PACKET üst bilgi boyutu, yük boyutu ve uygun hizalama dahil) sağlanan bellek alanında toplam bayt sayısına bölünerek hesaplanır.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma
Uygulama iş parçacıkları, boş bir havuzdan paket beklerken askıya alabilir. Havuza bir paket döndürüldü, askıya alınan iş parçacığına bu paket verilir ve devam eder.

Aynı paket havuzunda birden çok iş parçacığı askıya alınırsa, bunlar askıya alındıklarına (FIFO) göre devam eder.

### <a name="pool-statistics-and-errors"></a>Havuz İstatistikleri ve Hataları
Etkinleştirilirse, NetX paket yönetimi yazılımı **Hatalar** uygulama için yararlı olan çeşitli istatistikleri ve hataları takip eder. Paket havuzları için aşağıdaki istatistikler ve hata raporları korunur:

* Havuzdaki Toplam Paket Sayısı
* Havuza Ücretsiz Paketler
* Havuz Boş Ayırma İstekleri
* Havuz Boş Ayırma Askıya Almaları
* Geçersiz Paket Sürümü

Havuzdaki toplam ve ücretsiz paket sayısı dışındaki tüm bu istatistikler ve hata raporları, * NX_DISABLE_PACKET_INFO _ tanımlanmamışsa NetX **kitaplığında** yerleşik olarak yer alır. Bu veriler uygulama için *___* nx_packet_pool_info_get * hizmetiyle kullanılabilir.

### <a name="packet-pool-control-block-nx_packet_pool"></a>Paket Havuzu Denetim Bloğu NX_PACKET_POOL

Her paket bellek havuzunun özellikleri denetim bloğunda bulunur. Bu, bağlantılı boş paket listesi, boş paket sayısı ve bu havuza gelen paketler için yük boyutu gibi yararlı bilgiler içerir. Bu yapı, *nx_api.h dosyasında* tanımlanır.

Paket havuzu denetim blokları bellekte herhangi bir yerde yer alıyor olabilir, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline geldi.

## <a name="ip-protocol"></a>IP Protokolü

NetX'in İnternet Protokolü (IP) bileşeni, İnternet'te IP paketleri göndermek ve almakla sorumludur. NetX'te, temel ağ sürücüsünü kullanarak TCP, UDP, ICMP ve IGMP iletilerini göndermek ve almak sonuçta bileşenden sorumludur.

NetX IP protokolünü destekler (RFC 791)

### <a name="ip-addresses"></a>IP Adresleri

İnternet'te her ana bilgisayar, IP adresi olarak adlandırılan benzersiz bir 32 bit tanımlayıcıya sahip olur. Şekil 4'te açıklandığı gibi beş IP adresi sınıfı vardır. Beş IP adresi sınıflarının aralıkları aşağıdaki gibidir:

| Sınıf | Aralık                        |
|-------|------------------------------|
| A     | 0.0.0.0 - 127.255.255.255   |
| B     | 128.0.0.0 - 191.255.255.255 |
| C     | 192.0.0.0 - 223.255.255.255 |
| D     | 224.0.0.0 - 239.255.255.255 |
| E     | 240.0.0.0 - 247.255.255.255 |

**7 bit 24 bit**

![IP Adresi Yapısı](./media/user-guide/ip-address-structure.png)

**ŞEKIL 4. IP Adresi Yapısı**

Ayrıca üç tür adres belirtimleri de vardır: *tek noktaya yayın,* *yayın* ve çok *noktaya yayın.* Tek noktaya yayın adresleri, internet üzerinde belirli bir ana bilgisayarı tanımlamak için bu IP adresleridir. Tek noktaya yayın adresleri bir kaynak veya hedef IP adresi olabilir. Yayın adresi belirli bir ağ veya alt ağ üzerinde tüm konakları tanımlar ve yalnızca hedef adres olarak kullanılabilir. Yayın adresleri, adresin konak kimliği kısmının olanlar olarak ayarlanmış olmasıyla belirtilir. Çok noktaya yayın adresleri (Sınıf D), internet üzerinde dinamik bir konak grubu belirtir. Çok noktaya yayın grubunun üyeleri her zaman katılarak ayrıl olabilir.

> [!IMPORTANT]
> *Yalnızca IP üzerinden UDP gibi bağlantısız protokoller, çok noktaya yayın grubunun yayın ve sınırlı yayın özelliğini kullanılabilir.*

> [!IMPORTANT]
> *Makro* IP_ADDRESS,   * **nx_api.h _ içinde** tanımlanır. Nokta yerine virgül kullanarak IP adreslerinin kolayca belirtimlerini sağlar. Örneğin, IP_ADDRESS(128,0,0,0) _specifies Şekil 4'te gösterilen birinci sınıf B adresidir.*

### <a name="ip-gateway-address"></a>IP Ağ Geçidi Adresi

Ağ geçitleri, ağlarında bulunan konakların yerel etki alanı dışındaki hedeflere giden paketleri iletmelerine yardımcı olur. Her düğüm, hedef komşularından biri veya önceden programlanmış statik yönlendirme tablosu aracılığıyla gönderilecek sonraki atlama hakkında bilgi sahibidir. Ancak bu yaklaşımlar başarısız olursa, düğümün paketi hedefine yönlendirme hakkında daha fazla bilgiye sahip olan varsayılan ağ geçidine iletmesi gerekir. Varsayılan ağ geçidine IP örneğine bağlı fiziksel arabirimlerden biri aracılığıyla doğrudan erişilebilir olması gerektiğini unutmayın. Uygulama, IP ***nx_ip_gateway_address_set*** adresini yapılandırmak için ağ geçidini arar.

### <a name="ip-header"></a>IP Üst Bilgisi

İnternet'e gönderilecek herhangi bir IP paketi için bir IP üst bilgisi olması gerekir. Daha üst düzey protokoller (UDP, TCP, ICMP veya IGMP) bir paket göndermek için IP bileşenini çağırsa, IP iletme modülü verilerin önüne bir IP üst bilgisi yer alır. Buna karşılık, IP paketleri ağdan geldiğinde, IP bileşeni daha üst düzey protokollere teslimten önce IP üst bilgisini paketten kaldırır. Şekil 5'te IP üst bilgisi biçimi görüntülenir.

![IP Üst Bilgisi Biçimi](./media/user-guide/ip-header-format.png)

**ŞEKIL 5. IP Üst Bilgisi Biçimi**

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm üst big endian beklenir. Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır. Örneğin, IP üst bilgisi 4 bit sürümü ve 4 bit üst bilgi uzunluğu üst bilginin ilk baytı üzerinde olmalıdır.*

IP üst bilgisi alanları aşağıdaki gibi tanımlanır:

**IP Üst Bilgisi Alan Amacı**

***4 bit sürüm*** Bu alan, bu üst bilginin temsil ettiği IP sürümünü içerir. NetX'in desteklediği IP sürüm 4 için bu alanın değeri 4'dür.

***4 bit üst bilgi uzunluğu*** Bu alan, IP üst bilgisinde 32 bit sözcük sayısını belirtir. Seçenek sözcükleri yoksa bu alanın değeri 5'tir.

***8 bit hizmet türü (TOS)*** Bu alan, bu IP paketi için istenen hizmet türünü belirtir. Geçerli istekler aşağıdaki gibidir:

| **TOS İsteği**     | **Değer** |
| ------------------- | --------- |
| Normal              | 0x00      |
| Minimum Gecikme       | 0x10      |
| En Fazla Veri        | 0x08      |
| En Yüksek Güvenilirlik | 0x04      |
| En Düşük Maliyet        | 0x02      |

***16 bit toplam uzunluk*** Bu alan, IP üst bilgisi dahil olmak üzere IP veri biriminin bayt cinsinden toplam uzunluğunu içerir. IP veri birimi, TCP/IP İnterneti üzerinde bulunan temel bilgi birimidir. Verilere ek olarak bir hedef ve kaynak adresi içerir. 16 bitlik bir alan olduğundan IP veri biriminin en büyük boyutu 65.535 bayttır.

***16 bit tanımlama*** alanı, bir konaktan gönderilen her IP veri birimini benzersiz olarak tanımlamak için kullanılan bir sayıdır. Bu sayı genellikle bir IP veri birimi gönderildikten sonra artırılır. Özellikle alınan IP paketi parçalarının birleştirilmesinde yararlıdır.

***3 bit bayraklar*** Bu alan IP parçalanma bilgilerini içerir. Bit 14, "parçalama" bitidir. Bu bit ayarlanırsa giden IP veri birimi parçalanmaz. Bit 13, "daha fazla parça" bitidir. Bu bit ayarlanırsa daha fazla parça vardır. Bu bit netse, bu IP paketinin son parçasıdır.

**IP Üst Bilgisi Alan Amacı**

***13 bit parça uzaklığı*** Bu alan, parça uzaklığının üst 13 bitlerini içerir. Bu nedenle, parça uzaklıklarına yalnızca 8 bayt sınırlarda izin verilir. Parçalı BIR IP veri biriminin ilk parçası "daha fazla parça" bit kümesine ve 0 uzaklığına sahip olur.

***8 bit yaşam süresi (TTL)*** Bu alan, bu veri biriminin geçeceği yönlendirici sayısını içerir ve bu da veri biriminin ömrünü sınırlar.

***8 bit protokol*** Bu alan, IP veri birimini kullanan protokolü belirtir. Aşağıda geçerli protokollerin ve bunların değerlerinin listesi ve liste yer almaktadır:

| Protokol | Değer |
|----------|-------|
| ICMP     | 0x01  |
| ıgmp     | 0x02  |
| TCP      | 0X06  |
| UDP      | 0X11  |
|          |       |


***16 bit sağlamaları*** Bu alan yalnızca IP üst bilgisini kapsayan 16 bit sağlama sağlamalarını içerir. IP yükünü üst düzey protokollerde ek sağlama sağlamaları vardır.

***32 bit kaynak IP adresi*** Bu alan gönderenin IP adresini içerir ve her zaman bir konak adresidir.

***32 bit hedef IP adresi*** Bu alan, adres bir yayın veya çok noktaya yayın adresi ise alıcı veya alıcıların IP adresini içerir.

### <a name="creating-ip-instances"></a>IP Örnekleri Oluşturma

IP örnekleri başlatma sırasında veya uygulama iş parçacıkları tarafından çalışma zamanı sırasında oluşturulur. İç IP iş parçacığının ilk IP adresi, ağ maskesi, varsayılan paket havuzu, medya sürücüsü ve bellek ve önceliği, *nx_ip_create* tanımlanır. Uygulama IP örneğini IP adresi geçersiz bir adrese (0.0.0.0) ayarlanmış şekilde başlatıyorsa, arabirim adresinin daha sonra EL ile yapılandırmayla, RARP yoluyla veya DHCP ya da benzer protokoller aracılığıyla çözülecek olduğu varsayılır.

Birden çok ağ arabirimine sahip sistemler için, birincil arabirim, *nx_ip_create.* Her ek arabirim, nx_ip_interface_attach çağrılarak aynı IP *örneğine nx_ip_interface_attach.* Bu hizmet, ağ arabirimi (IP adresi, ağ maskesi gibi) hakkında bilgileri arabirim denetim bloğunda depolar ve sürücü örneğini IP örneğinde arabirim denetim bloğuyla ilişkilendirmektedir. Sürücü bir veri paketi aldığında, IP alma mantığına iletmeden önce arabirim NX_PACKET veri yapısında depolaması gerekir. Arabirim eklemeden önce bir IP örneğinin önceden oluşturulmuş olması gerektiğini unutmayın.

 ### <a name="ip-send"></a>IP Gönderme
 NetX'te IP gönderme işlemi çok kolaylaştırılmıştır.

Pakette ön uç işaretçisi, IP üst bilgisine uyum sağlayacak şekilde geriye doğru taşınır. IP üst bilgisi tamamlanır (çağrı protokolü katmanı tarafından belirtilen tüm seçeneklerle birlikte), IP sağlamaları satır içinde hesaplanır ve paket ilişkili ağ sürücüsüne sevk edilir. Ayrıca giden parçalanma, IP gönderme işleminin içinde de eşgüdüm sağlar.

IP için, hedef IP adresi için fiziksel eşleme gerekirse NetX ARP isteklerini başlatıyor.

> [!IMPORTANT]
> *IP bağlantısı için, IP adresi çözümlemesi (fiziksel eşleme)* gerektiren paketler, kuyruğa alınan paket sayısı ARP kuyruk derinliğini (NX_ARP_MAX_QUEUE_DEPTH simgesiyle tanımlanır) aşana kadar ARP kuyruğunda kuyruğa *eklenir.  Kuyruk derinliğine* *ulaşıldı ise, NetX kuyrukta en eski paketi kaldırır ve kuyrukta kalan paketler için adres çözümlemesini beklemeye devam eder. Öte yandan, bir ARP* girişi çözümlenmezse, ARP girdisi üzerinde bekleyen paketler ARP girdisi zaman aşımına karşı serbest bıraktır.

NetX, birden çok ağ arabirimine sahip sistemler için hedef IP adresine göre bir arabirim seçer. Aşağıdaki yordam seçim işlemi için geçerlidir:

1. Hedef adres IP yayını veya çok noktaya yayın ise ve geçerli bir giden arabirim belirtilirse bu arabirimi kullanın. Aksi takdirde ilk fiziksel arabirim kullanılır.

2. Hedef adres statik yönlendirme tablosunda bulunursa, ağ geçidiyle ilişkili arabirim kullanılır.

3. Hedef bağlantıda ise, bağlantı arabirimi kullanılır.

4. Hedef adres 127.0.0.1 geri döngü adresi ise geri döngü arabirimi kullanılır.

5. Varsayılan ağ geçidi düzgün yapılandırılmışsa, paketi iletmek için varsayılan ağ geçidiyle ilişkili arabirimi kullanın.

6. Yukarıdakilerin hepsi başarısız olursa çıkış paketi bırakılır.

### <a name="ip-receive"></a>IP Alma

IP alma işlemesi ağ sürücüsünden veya iç IP iş parçacığından çağrılır (ertelenen alınan paket kuyruğunda paketlerin iş için). IP alma işlemi protokol alanını inceler ve paketi uygun protokol bileşenine göndermeyi çalışır. Paket gerçekten gönderlanmadan önce, ip üst bilgisi, ip üst bilgisini geçerek ön uç işaretçisi ekılarak kaldırılır.

IP alma işlemi ayrıca parçalı IP paketlerini algılar ve parçalanma etkinse bunları yeniden bir hale almak için gerekli adımları gerçekleştirir. Parçalanma gerekli ancak etkinleştirilmemişse paket bırakılır.

NetX, pakette belirtilen arabirime göre uygun ağ arabirimini belirler. Paket arabirimi NULL ise, NetX varsayılan olarak birincil arabirimdir. Bu, eski NetX Ethernet sürücüleriyle uyumluluğu garanti etmek için yapılır.

### <a name="raw-ip-send"></a>Ham IP Gönderme

Ham IP paketi, NetX tarafından doğrudan desteklenmemektedir (ve işlenmemektedir) üst katman protokol yükünü içeren bir IP çerçevesidir. Ham paket, geliştiricilerin kendi IP tabanlı uygulamalarını tanımlamalarına olanak sağlar. Bir uygulama, ham IP paketi işlemenx_ip_raw_packet_send hizmette etkinleştirildiyse, ham IP paketlerini * nx_ip_raw_packet_enabled _*_gönderebilir._*_ Hedef adres bir çok noktaya yayın veya yayın adresi ise, NetX varsayılan olarak ilk (birincil) arabirimini kullanır. Bu nedenle, bu tür paketleri ikincil arabirimlere göndermek için, uygulama giden paket için kaynak adresini belirtmek üzere _ *_nx_ip_raw_packet_interface_send_** hizmetini kullanmalıdır.

### <a name="raw-ip-receive"></a>Ham IP Alma

Ham IP paketi işleme etkinleştirildiyse, uygulama * nx_ip_raw_packet_receive _ **hizmeti** aracılığıyla ham IP paketleri alır. Tüm gelen paketler IP üst bilgisinde belirtilen protokole göre işlenir. Protokol UDP, TCP, IGMP veya ICMP'yi belirtirse, NetX paket protokolü türü için uygun işleyiciyi kullanarak paketi işler. Protokol bu protokollerden biri yoksa ve ham IP alma etkinse, gelen paket uygulamanın _ nx_ip_raw_packet_receive * hizmeti aracılığıyla bunu almalarını bekleyen ham paket *_kuyruğuna_* eklenir. Ayrıca, uygulama iş parçacıkları ham IP paketi beklerken isteğe bağlı bir zaman aşımı ile askıya alabilir.

### <a name="default-packet-pool"></a>Varsayılan Paket Havuzu

Oluşturma sırasında her IP örneğine varsayılan bir paket havuzu verilir. Bu paket havuzu ARP, RARP, ICMP, IGMP, çeşitli TCP denetim paketleri (SYN, ACK gibi) için paket ayırmak için kullanılır. NetX'in bir paket ayırması gerekirken varsayılan paket havuzu boşsa, NetX'in belirli bir işlemi durdurması gerekir ve mümkünse bir hata iletisi döndürür.

### <a name="ip-helper-thread"></a>IP Yardımcı İş Parçacığı

Her IP örneğinin bir yardımcı iş parçacığı vardır. Bu iş parçacığı, ertelenen tüm paket işleme ve tüm düzenli işlemlerin işlenmesinden sorumludur. IP yardımcı iş parçacığı, ***nx_ip_create.*** İş parçacığına yığını ve önceliği burada verilir. IP yardımcı iş parçacığında ilk işlemenin, IP oluşturma hizmetiyle ilişkili ağ sürücüsü başlatma işlemini tamamlamak olduğunu unutmayın. Ağ sürücüsü başlatma işlemi tamamlandıktan sonra yardımcı iş parçacığı, paket ve düzenli istekleri işlemeye yarayan sonsuz bir döngü başlatır.

> [!IMPORTANT]
> *IP yardımcı iş parçacığında açıklanamayan bir davranış görülürse, IP oluşturma hizmeti sırasında yığın boyutunu artırmak ilk hata ayıklama adımıdır. Yığın çok küçükse, IP yardımcı iş parçacığı büyük olasılıkla belleğin üzerine yazılabilir ve bu da olağan dışı sorunlara neden olabilir.*

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma

Uygulama iş parçacıkları ham IP paketlerini almaya çalışırken askıya alabilir. Ham bir paket alındıktan sonra, yeni paket askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı devam eder. Paketleri almaya uygun NetX hizmetlerinin hepsi isteğe bağlı bir askıya alma zaman aşımına sahip. Bir paket alınca veya zaman aşımı sona erdiğinde, uygulama iş parçacığı uygun tamamlanma durumuyla devam eder.

### <a name="ip-statistics-and-errors"></a>IP İstatistikleri ve Hataları

Etkinleştirilirse, NetX uygulama için yararlı olacak çeşitli istatistikleri ve hataları takip eder. Her IP örneği için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen Toplam IP Paketleri
- Gönderilen Toplam IP Bayt Sayısı
- Alınan Toplam IP Paketleri
- Alınan Toplam IP Bayt Sayısı
- Toplam IP Geçersiz Paketleri
- Bırakılan Toplam IP Alma Paketleri
- Toplam IP Alma Sağlama Toplamı Hataları
- Bırakılan Toplam IP Gönderme Paketleri
- Gönderilen Toplam IP Parçaları
- Alınan Toplam IP Parçaları

Bu istatistiklerin ve hata raporlarının hepsi uygulamanın nx_ip_info_get ***kullanılabilir.***

### <a name="ip-control-block-nx_ip"></a>IP Denetim Bloğu NX_IP

Her IP örneğinin özellikleri denetim bloğunda bulunur. Her ağ aygıtının IP adresleri ve ağ maskeleri gibi yararlı bilgiler ile komşu IP ve fiziksel donanım adresi eşlemesi tablosu içerir. ***Bu yapı, nx_api.h*** IP örneği denetim bloklarında bellek içinde herhangi bir yerde yer alan bir konumda tanımlanır, ancak en yaygın olarak denetim bloğu herhangi bir işlevin kapsamı dışında tanımlayarak genel bir yapı haline gelmektedir.

### <a name="static-ip-routing"></a>Statik IP Yönlendirme

Statik yönlendirme özelliği, bir uygulamanın belirli ağ dışı hedef IP adresleri için bir IP ağı ve sonraki atlama adresi belirtmesini sağlar. Statik yönlendirme etkinse NetX, gönderilecek paketin hedef adresiyle eşleşen bir giriş için statik yönlendirme tablosunda arama gönderir. Eşleşme yoksa NetX, fiziksel arabirimler listesinde arama ve hedef IP adresi ile ağ maskesine göre bir kaynak IP adresi ve sonraki atlama adresi seçer. Hedef, IP örneğine bağlı ağ sürücülerinin IP adreslerinden herhangi biri ile eşlen yoksa NetX, varsayılan ağ geçidine doğrudan bağlı bir arabirim seçer ve arabirimin IP adresini kaynak adres olarak, varsayılan ağ geçidini de sonraki atlama olarak kullanır.

Girişler sırasıyla nx_ip_static_route_add ve * nx_ip_static_route_delete  _ hizmetleri kullanılarak statik **yönlendirme tablosundan** eklenebilir ve kaldırılabilir. Statik yönlendirmeyi kullanmak için konak uygulamanın _ veya .* kimliklerini tanımlayarak *_NX_ENABLE_IP_STATIC_ROUTING_* gerekir

> [!IMPORTANT]
> *NetX, statik yönlendirme tablosuna bir giriş eklerken tabloda zaten belirtilen hedef adres için eşleşen bir girdiyi denetler. Varsa, ağ maskesinde daha küçük bir ağ (daha uzun ön ek) olan girişe tercih verir.*

### <a name="ip-fragmentation"></a>IP Parçalanması

Ağ cihazı giden paketlerin boyutuna göre sınırlara sahip olabilir. Bu sınır, maksimum iletim birimi (MTU) olarak adlandırılan bir sınırdır. IP MTU, bir bağlantı katmanı sürücüsünün IP paketini parçalanmadan ilettiği en büyük IP çerçevesi boyutudur. Cihaz sürücüsü başlatma aşamasında, sürücü modülünün IP MTU boyutunu hizmet * veya .* üzerinden **nx_ip_interface_mtu_set** gerekir

Önerilmez, ancak uygulama, cihaz tarafından desteklenen temel IP MTU'suna göre daha büyük veri birimleri üretebilir. Bu TÜR BIR IP veri birimini iletmeden önce IP katmanının bu paketleri parçalanması gerekir. Parçalı IP çerçeveleri alırken, alıcı uç aynı parçalanma kimliğine sahip tüm parçalanmış IP çerçevelerini depolamalı ve bunları sırayla yeniden değerlendirebilir. IP alma mantığı özgün IP çerçevesini zamanında geri yüklemek için tüm parçaları topalamazsa, tüm parçalar serbest olur. Bu tür bir paket kaybını algılamak ve bu durumdan kurtarmak üst katman protokolüne göredir.

IP parçalanması ve yeniden değerlendirme işlemi desteklemek için sistem tasarımcısının NetX'te IP parçalanma özelliğini nx_ip_fragment_enable ***gerekir.*** Bu özellik etkinleştirilmezse, gelen parçalanmış IP paketleri ve ağ sürücüsünün MTU'suna aşan paketler atılır.

> [!IMPORTANT]
> *IP Parçalanma mantığı tanımlayarak tamamen kaldırılabilir*  * **NX_DISABLE_FRAGMENTATION** _ _when NetX kitaplığını oluşturma. Bunu yapmak NetX'in kod boyutunu azaltmaya yardımcı olur.*

## <a name="address-resolution-protocol-arp-in-ip"></a>IP'de Adres Çözümleme Protokolü (ARP)

Adres Çözümleme Protokolü (ARP), 32 bit IP adreslerini temel alınan fiziksel medya (RFC 826) adreslerine dinamik olarak eşlemeden sorumludur. Ethernet en tipik fiziksel medyadır ve 48 bit adresleri destekler. ARP ihtiyacı, ARP hizmetine sağlanan ağ sürücüsü ***nx_ip_create*** belirlenir. Fiziksel eşleme gerekli ise, ağ sürücüsünün arabirim nx_interface_address_mapping_needed ***bayrağını*** ayarlaması gerekir.

### <a name="arp-enable"></a>ARP Etkinleştirme
ARP'nin düzgün çalışması için önce uygulama tarafından nx_arp_enable ***etkinleştirilmesi*** gerekir. Bu hizmet, ARP etkinleştirme hizmetine sağlanan bellekten ARP önbellek alanı oluşturma da dahil olmak üzere ARP işleme için çeşitli veri yapıları ayarlar.

### <a name="arp-cache"></a>ARP Önbelleği
ARP önbelleği, iç ARP eşleme veri yapılarının dizisi olarak görünüme sahip olabilir. Her iç yapı, bir IP adresi ile fiziksel donanım adresi arasındaki ilişkiyi koruyabilirsiniz. Ayrıca, her veri yapısında bağlantı işaretçileri vardır, bu nedenle birden çok bağlantılı liste olabilir.

Uygulama, eşleme ARP tablosunda mevcutsa , hizmet * nx_arp_ip_address_find _ kullanarak donanım MAC adresi temin eder ve ARP **önbelleğinden** bir IP adresine bakabilirsiniz. Benzer şekilde, _ *_nx_arp_hardware_address_find_** hizmeti belirli bir IP adresi için MAC adresini döndürür.


### <a name="arp-dynamic-entries"></a>ARP Dinamik Girişleri

Varsayılan olarak, ARP etkinleştirme hizmeti ARP önbelleğine tüm girişleri kullanılabilir dinamik ARP girdileri listesine yer ayarlar. Eşlenmemiş bir IP adresine bir gönderme isteği algılandığında, bu listeden NetX tarafından dinamik bir ARP girişi ayrılır. Ayırmadan sonra ARP girişi ayarlanır ve fiziksel medyaya bir ARP isteği gönderilir.

Dinamik giriş, hizmeti tarafından da oluşturulabilir ***nx_arp_dynamic_entry_set.***

> [!IMPORTANT]
> *Tüm dinamik ARP girişleri kullanılıyorsa, en son kullanılan ARP girişi yeni bir eşlemeyle değiştirilir.*

### <a name="arp-static-entries"></a>ARP Statik Girişleri
Uygulama ayrıca statik ARP eşlemesi ayarlamak için nx_arp_static_entry_create ***kullanabilir.*** Bu hizmet, dinamik ARP giriş listesinden bir ARP girişi ayırır ve uygulama tarafından sağlanan eşleme bilgileriyle statik listeye yer alır. Statik ARP girişleri yeniden kullanılabilir veya eskime durumuna tabi değildir. Uygulama, statik bir girişi silmek için ***nx_arp_static_entry_delete.***
Uygulama, ARP tablosunda yer alan tüm statik girişleri kaldırmak için ***nx_arp_static_entries_delete.***

### <a name="automatic-arp-entry"></a>Otomatik ARP Girişi
NetX, ARP isteğine eş yanıtlarından sonra eş ip/MAC eşlemesini kaydeder. NetX ayrıca ağdan gelen istenmeyen ARP isteklerini temel alan eş IP/MAC adresi eşlemesini kaydeden otomatik ARP giriş özelliğini de uygulamaya alır. Bu özellik, ARP tablosu eş bilgileriyle doldurularak ARP isteği/yanıt döngüsünde geçen gecikme süresinin azaltılmasına olanak sağlar. Ancak otomatik ARP'nin etkinleştirilmenin dezavantajı, ARP tablosu meşgul bir ağ üzerinde yerel bağlantıda çok sayıda düğümle hızla dolma eğiliminde olmasıdır ve bu da sonunda ARP girişinin değiştirilmesine neden olur.

Bu özellik varsayılan olarak etkindir. Bunu devre dışı bırakmak için NetX kitaplığının tanımlandığı simgeyle ***NX_DISABLE_ARP_AUTO_ENTRY*** gerekir.

### <a name="arp-messages"></a>ARP İletileri

Daha önce belirtildiği gibi, IP görevi bir IP adresi için eşleme gerektiğini algılayan bir ARP istek iletisi gönderilir. ARP istekleri, karşılık gelen bir ARP **yanıtı alınana kadar** düzenli aralıklarla (NX_ARP_UPDATE_RATE _ saniye) gönderilir. ARP girişimi *_NX_ARP_MAXIMUM_RETRIES_* önce toplam _ NX_ARP_MAXIMUM_RETRIES * ARP istekleri yapılır. Bir ARP yanıtı alınca, ilişkili fiziksel adres bilgileri önbellekte yer alan ARP girdisinde depolanır.

Çoklu ana bilgisayar sistemleri için NetX, belirtilen hedef adrese göre ARP isteklerinin ve yanıtların gönderilecek arabirimini belirler.

> [!IMPORTANT]
> *NetX, ARP yanıtını beklerken giden IP paketleri kuyruğa eklenir. Kuyruğa alınan giden IP* *paketlerinin sayısı,*.* ile  * **NX_ARP_MAX_QUEUE_DEPTH** tanımlanır.

NetX ayrıca yerel IP ağı üzerinde diğer düğümlerden gelen ARP isteklerine yanıt verir. ARP isteğini alan arabirimin geçerli IP adresiyle eşleşen bir dış ARP isteği yapılırsa, NetX geçerli fiziksel adresi içeren bir ARP yanıt iletisi derlemez.

Ethernet ARP isteklerinin ve yanıtlarının biçimleri Şekil 6'da gösterilmiştir ve aşağıda açıklanmıştır:

| İstek/Yanıt Alanı       | Amaç    |
|------------------------------|-----------------|
| Ethernet Hedef Adresi | Bu 6 bayt alanı ARP yanıtının hedef adresini içerir ve ARP istekleri için bir yayındır (hepsi). Bu alan ağ sürücüsü tarafından ayardır. |
| Ethernet Kaynak Adresi      | Bu 6 bayt alanı, ARP isteğini veya yanıtını gönderenin adresini içerir ve ağ sürücüsü tarafından ayarlanır. |
| Çerçeve Türü                   | Bu 2 bayt alanı, mevcut Ethernet çerçevesinin türünü içerir ve ARP istekleri ve yanıtları için bu, mevcut Ethernet çerçevesine 0x0806. Bu, ağ sürücüsünün ayarlamadan sorumlu olduğu son alandır. |
| Donanım Türü                | Bu 2 bayt alanı, Ethernet için geçerli olan 0x0001 türünü içerir. |
| Protokol Türü                | Bu 2-byte alanı, IP adresleri için 0x0800 protokol türünü içerir. |
| Donanım Boyutu                | Bu 1 bayt alanı, Ethernet adresleri için 6 olan donanım adresi boyutunu içerir. |


![ARP Paket Biçimi](./media/user-guide/arp-packet-format.png)

**ŞEKIL 6. ARP Paket Biçimi**

| İstek/Yanıt Alanı | Amaç  |
|---|---|
| Protokol Boyutu | Bu 1 bayt alanı, IP adresleri için 4 olan IP adresi boyutunu içerir.  |
| İşlem Kodu | Bu 2 bayt alanı, bu ARP paketi için işlemi içerir. ARP isteği, 0x0001 değeriyle belirtilirken, ARP yanıtı 0x0002.  |
| Gönderen Ethernet Adresi | Bu 6 bayt alanı gönderenin Ethernet adresini içerir. |
| Gönderen IP Adresi | Bu 4 bayt alanı gönderenin IP adresini içerir. |
| Hedef Ethernet Adresi | Bu 6 bayt alanı hedefin Ethernet adresini içerir. |
| Hedef IP Adresi | Bu 4 bayt alanı hedefin IP adresini içerir. |

> [!IMPORTANT]
> *ARP istekleri ve yanıtları Ethernet düzeyinde paketlerdir. Diğer tüm TCP/IP paketleri bir IP paket üst bilgisi tarafından kapsüllanır.*

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm ARP iletilerinin aynı biçimde big endian beklenir. Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır.*

### <a name="arp-aging"></a>ARP Eskime

NetX, otomatik dinamik ARP girişi geçersiz kılınma özelliğini destekler. ***NX_ARP_EXPIRATION_RATE** _specifies ip adresinin geçerli kalma saniye sayısını belirtir. Süre dolsa da ARP girişi ARP önbelleğinden kaldırılır. Karşılık gelen IP adresine bir sonraki gönderme girişimi yeni bir ARP isteğine neden olur. _ *_NX_ARP_EXPIRATION_RATE_** değerinin sıfır olarak ayarlanıyor olması, varsayılan yapılandırma olan ARP eskime özelliğini devre dışı bırakır.

### <a name="arp-defend"></a>ARP Savunması

Bir ARP isteği veya ARP yanıt paketi alınca ve gönderen bu düğümün IP adresiyle çakışan aynı IP adresine sahip olduğunda, NetX bu adres için savunma olarak bir ARP isteği gönderir. Çakışma ARP paketi 10 saniyede birden fazla kez alındıktan sonra NetX daha fazla savunma paketi göndermez. Varsayılan 10 saniyelik aralık * NX_ARP_DEFEND_INTERVAL **_.** Bu davranış, RFC5227'nin 2.4(c) tarihinde belirtilen ilkeyi izler. XP Windows ARP araştırmasını yanıt olarak ARP duyurusunu yoksaysa da, kullanıcı ARP yanıtını ek savunma olarak göndermek için _*_NX_ARP_DEFEND_BY_REPLY_**'yi tanımlayabilir.

### <a name="arp-statistics-and-errors"></a>ARP İstatistikleri ve Hataları

Etkinleştirilirse, NetX ARP yazılımı uygulama için yararlı olan çeşitli istatistikleri ve hataları takip eder. Her IP'nin ARP işlemesi için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen Toplam ARP İsteği Sayısı
- Alınan Toplam ARP İsteği Sayısı
- Gönderilen Toplam ARP Yanıtları
- Alınan Toplam ARP Yanıtları
- Toplam ARP Dinamik Girdisi
- Toplam ARP Statik Girdileri
- Toplam ARP Eski Girdisi
- Toplam ARP Geçersiz İleti sayısı

Tüm bu istatistikler ve hata raporları, uygulamanın nx_arp_info_get ***kullanılabilir.***

## <a name="reverse-address-resolution-protocol-rarp-in-ip"></a>IP'de Ters Adres Çözümleme Protokolü (RARP)

Ters Adres Çözümleme Protokolü (RARP), ana bilgisayar 32 bit IP adreslerinin (RFC 903) ağ ataması isteğinde gerçekleştirilen protokoldür. Bu bir RARP isteği aracılığıyla yapılır ve bir ağ üyesi RARP yanıtta konak ağ arabirimine bir IP adresi atana kadar düzenli aralıklarla devam eder. Uygulama, sıfır IP adresiyle hizmet ***nx_ip_create*** IP örneği oluşturur. UYGULAMA RARP'yi etkinleştirdiyse, sıfır IP adresine sahip arabirim üzerinden erişilebilen ağ sunucusundan bir IP adresi isteğinde etmek için RARP protokolünü kullanabilir.

### <a name="rarp-enable"></a>RARP Etkinleştirme

RARP'yi kullanmak için, uygulamanın IP örneğini sıfır IP adresiyle oluşturması ve ardından raRP'yi hizmeti kullanarak ***etkinleştirmesi nx_rarp_enable.*** Birden çok girişli sistemlerde, IP örneğiyle ilişkili en az bir ağ cihazı sıfır ip adresine sahip olmalıdır. RARP işlemi, ağ tarafından belirlenen IP adresiyle geçerli bir RARP yanıtı alınana kadar NetX sistemi için BIR IP adresi gerektiren RARP istek iletilerini düzenli aralıklarla gönderir. Bu noktada, RARP işleme tamamlanır.

RARP etkinleştirildikten sonra, tüm arabirim adresleri çözümlendikten sonra otomatik olarak devre dışı bırakılır. Uygulama, hizmeti kullanarak RARP'nin sonlandırılmalarını nx_rarp_disable.

###  <a name="rarp-request"></a>RARP İsteği

RaRP istek paketinin biçimi, ARP İletileri konu başlığında Şekil 6'da gösterilen [ARP paketiyle neredeyse aynıdır.](#arp-messages) Tek fark, çerçeve türü alanı 0x8035 ve  İşlem Kodu alanı 3'tür ve RARP isteği belirterek. Daha önce belirtildiği gibi, ağ tarafından atanan IP adresiyle bir RARP ***yanıtı alınana kadar*** RARP istekleri düzenli aralıklarla (her NX_RARP_UPDATE_RATE saniye) gönderilir.

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm RARP iletilerinin aynı biçimde big endian beklenir. Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır.*

### <a name="rarp-reply"></a>RARP Yanıtı

RARP yanıt iletileri ağdan alınarak bu ana bilgisayar için ağ tarafından atanan IP adresini içerir. RaRP yanıt paketinin biçimi, Şekil 6'da gösterilen ARP paketiyle neredeyse aynıdır. Tek fark, çerçeve türü alanı 0x8035 ve  İşlem Kodu alanı 4'tür ve bu da RARP yanıtını gösterir. Alındıktan sonra, IP adresi IP örneğinde ayar, düzenli RARP isteği devre dışı bırakılır ve IP örneği artık normal ağ işlemi için hazırdır.

Birden çok ana bilgisayar için IP adresi, istekte olan ağ arabirimine uygulanır. IP adresi ataması isteğinde olan başka ağ arabirimleri varsa, tüm arabirim IP adresi istekleri çözümlenene kadar düzenli RARP hizmeti devam eder.

> [!IMPORTANT]
> *RARP işlemesi tamamlandıktan sonra uygulama IP örneğini kullanmaz. Uygulama **nx_ip_status_check** RARP tamamlanmasını beklemek için uygulamalar tarafından kullanılabilir. Birden çok girişli sistemlerde, raRP işlemesi bu arabirimde tamamlandıktan sonra uygulama, istekte bulunduran arabirimi kullanmaz. İkincil cihaz ip adresinin durumu, nx_ip_interface_status_check **denetlenir.***

### <a name="rarp-statistics-and-errors"></a>RARP İstatistikleri ve Hataları

Etkinleştirilirse, NetX RARP yazılımı uygulama için yararlı olan çeşitli istatistikleri ve hataları takip eder. Her IP'nin RARP işlemesi için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen Toplam RARP İsteği Sayısı
- Alınan Toplam RARP Yanıtları
- Toplam RARP Geçersiz İleti sayısı

Tüm bu istatistikler ve hata raporları, uygulamanın nx_rarp_info_get ***kullanılabilir.***

## <a name="internet-control-message-protocol-icmp"></a>İnternet Denetim İletisi Protokolü (ICMP)

IP için İnternet Denetim İletisi Protokolü (ICMP), IP ağ üyeleri arasında hata ve denetim bilgilerini geçirmeyle sınırlıdır.

Diğer çoğu uygulama katmanı (örneğin, TCP/IP) iletileri gibi ICMP iletileri de ICMP protokol ataması ile bir IP üst bilgisi tarafından kapsüllanır.

### <a name="icmp-statistics-and-errors"></a>ICMP İstatistikleri ve Hataları

Etkinleştirilirse NetX, uygulama için yararlı olan çeşitli ICMP istatistiklerini ve hatalarını takip eder. Her IP'nin ICMP işlemesi için aşağıdaki istatistikler ve hata raporları korunur:

- Gönderilen Toplam ICMP Ping'i
- Toplam ICMP Ping Zaman Aşımı Sayısı
- Toplam ICMP Ping İş Parçacığı Askıya Alındı
- Alınan Toplam ICMP Ping Yanıtları
- Toplam ICMP Sağlama Toplamı Hataları
- Toplam ICMP İşsiz İleti sayısı

Tüm bu istatistikler ve hata raporları, uygulamanın nx_icmp_info_get ***kullanılabilir.***

### <a name="icmp-enable"></a>ICMP Etkinleştirme
ICMP iletilerinin NetX tarafından işlenmeden önce, uygulamanın ICMP işlemeyi ***etkinleştirmek nx_icmp_enable*** hizmetine çağrı göndermesi gerekir. Bu yapıldıktan sonra, uygulama ping istekleri ve alan gelen ping paketleri gönderebilir.

### <a name="icmp-echo-request"></a>ICMP Yankı İsteği
Yankı isteği, konak IP adresi tarafından tanımlanan ağ üzerinde belirli bir düğümün varlığını kontrol etmek için genellikle kullanılan icMP ileti t'tir. Popüler ping komutu ICMP yankı isteği/yankı yanıt iletileri kullanılarak uygulanır. Belirli bir ana bilgisayar varsa, ağ yığını ping isteğini ve yanıtlarını bir ping yanıtı ile işler. Şekil 7'de ICMP ping iletisi biçimi ayrıntılı olarak yer alır.

![ICMP Ping İletisi](./media/user-guide/icmp-ping-message.png)

**ŞEKIL 7. ICMP Ping İletisi**

> [!IMPORTANT]
> *TCP/IP uygulamasındaki tüm ICMP iletilerinin aynı biçimde big endian beklenir. Bu biçimde, sözcüğün en önemli bayt en düşük bayt adreste yer almaktadır.*

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

Daha önce belirtildiği gibi, TCP bağlantısının istemci tarafı bir TCP sunucusuna bağlantı isteği başlatıyor. Bağlantı isteği gelemeden önce istemci IP örneğinde TCP'nin etkinleştirilmesi gerekir. Ayrıca, istemci TCP yuvası daha sonra * nx_tcp_socket_create _ hizmetiyle **oluşturulacak** ve nx_tcp_client_socket_bind _*_hizmeti aracılığıyla bir bağlantı noktasına bağlanacak._*_ İstemci yuvası bağlandıktan sonra, tcp *_sunucusuyla nx_tcp_client_socket_connect_* kurmak için _ nx_tcp_client_socket_connect * hizmeti kullanılır. Bağlantı denemesi başlatmak için yuvanın KAPALI durumda olması gerektiğini unutmayın. Bağlantının kurulması, NetX'in bir SYN paketi vermesi ve ardından sunucudan syn ACK paketi beklemesi ile başlar ve bu da bağlantı isteğinin kabulü anlamına gelir. SYN ACK alındıktan sonra, NetX bir ACK paketiyle yanıt verir ve istemci yuvayı ESTABLISHED durumuna yükselter.

### <a name="tcp-client-disconnection"></a>TCP İstemci bağlantısının kesilmesi

Bağlantı kapatılıyor, çağrılarak ***nx_tcp_socket_disconnect.*** Askıya alma belirtilmezse, istemci yuvası sunucu yuvasına bir RST paketi gönderir ve yuvayı KAPALI durumuna gönderir. Aksi takdirde, bir askıya alma istenecekse, tam TCP bağlantı kesme protokolü aşağıdaki gibi gerçekleştirilir:

- Sunucu daha önce bir bağlantı kesme isteği başlattı ise (istemci yuvası zaten bir FIN paketi aldı, bir ACK ile yanıt verdi ve CLOSE WAIT durumda), NetX istemci TCP yuva durumunu LAST ACK durumuna yükselter ve bir FIN paketi gönderir. Ardından bağlantıyı kesmeyi tamamlamadan ve KAPALI durumuna girmeden önce sunucudan bir ACK bekler.

- Öte yandan, istemci ilk kez bağlantı kesme isteği başlatıyorsa (sunucu bağlantısı kesildi ve yuva hala ESTABLISHED durumda), NetX bağlantıyı başlatmak için bir FIN paketi gönderir ve bağlantıyı tamamladıktan ve yuvayı KAPALI bir durumda yerleştirmeden önce sunucudan bir FIN ve ACK almak için bekler.

Yuva iletme kuyruğunda hala paketler varsa NetX, paketlerin kabul askıya alınması için belirtilen zaman aşımını askıya alır. Zaman aşımı süresi dolsa, NetX istemci yuvasının aktarım kuyruğundan boşaltılır.

Uygulama, bağlantı noktasını istemci yuvasından çıkararak ***nx_tcp_client_socket_unbind.*** Yuva kapatılan durumda veya bağlantı noktası serbest bırakılamadan önce bağlantıyı kesme sürecinde (yani ZAMANLI BEKLEME durumu) olması gerekir; aksi takdirde bir hata döndürülür.

Son olarak, uygulamanın artık istemci yuvasına ihtiyacı yoksa, ***yuvayı nx_tcp_socket_delete*** için uygulama çağrılır.

### <a name="tcp-server-connection"></a>TCP Sunucusu Bağlantısı

TCP bağlantısının sunucu tarafı pasiftir; Diğer bir ifadeyle, sunucu bir istemcinin bağlantı isteğini başlatması için bekler. bir istemci bağlantısını kabul etmek için, TCP ilk olarak * nx_tcp_enable _ hizmeti **çağrılarak** IP örneğinde etkinleştirilmelidir. Ardından, uygulamanın _ nx_tcp_socket_create * hizmetini *_kullanarak bir_* TCP yuvası oluşturması gerekir.

Sunucu yuvasının bağlantı isteklerini dinlemek için de ayarlanmış olması gerekir. Bu, nx_tcp_server_socket_listen hizmeti ***kullanılarak*** elde edilir. Bu hizmet sunucu yuvayı LISTEN durumuna yer verir ve belirtilen sunucu bağlantı noktasını yuvaya bağlar.

> [!IMPORTANT]
> *Yuva dinleme geri çağırma yordamını ayarlamak için uygulama, tcp_listen_callback hizmeti için uygun geri çağırma **işlevini nx_tcp_server_socket_listen** belirtir. Bu uygulama geri çağırma işlevi daha sonra bu sunucu bağlantı noktası üzerinde yeni bir bağlantı isten her istensin NetX tarafından yürütülür. Geri çağırmada işlem uygulama denetimi altındadır.*

Uygulama, istemci bağlantı isteklerini kabul etmek için ***** nx_tcp_server_socket_accept _ hizmetini çağırıyor. Sunucu yuvası, dinleme veya SYN RECEIVED (SYN RECEIVED) durumda (yani sunucu LISTEN durumda ve bağlantı isteğinde olan istemciden bir SYN paketi aldı) kabul hizmetini çağıran bir SYN paketine sahip olması gerekir. *___* nx_tcp_server_socket_accept * durumundan başarılı bir dönüş durumu, bağlantının ayar olduğunu ve sunucu yuvasının ESTABLISHED durumunda olduğunu gösterir.

Sunucu yuvasının geçerli bir bağlantısı olduktan sonra, ek istemci bağlantısı istekleri, listen_queue_size tarafından belirtilen derinliğe kadar * *nx_tcp_server_socket_listen* _ **hizmetine** geçiriliyor. Bir sunucu bağlantı noktası üzerinde sonraki bağlantıları işlemesi için, uygulamanın kullanılabilir bir yuvayla (yani KAPALI durumdaki bir yuva) _ *_nx_tcp_server_socket_relisten_** çağrısında olması gerekir. Yuvayla ilişkilendirilmiş önceki bağlantı artık bitti ve yuva KAPALI durumda olursa aynı sunucu yuvasının kullanıla bile olduğunu unutmayın.

### <a name="tcp-server-disconnection"></a>TCP Sunucusu Bağlantısını Kesme

Bağlantı kapatılıyor, çağrılarak ***nx_tcp_socket_disconnect.*** Askıya alma belirtilmezse, sunucu yuvası istemci yuvasına bir RST paketi gönderir ve yuvayı KAPALI durumuna gönderir. Aksi takdirde, bir askıya alma istenecekse, tam TCP bağlantı kesme protokolü şu şekilde gerçekleştirilir: |

- İstemci daha önce bir bağlantı kesme isteği başlattı ise (sunucu yuvası zaten bir FIN paketi aldı, ACK ile yanıt verdi ve CLOSE WAIT durumda), NetX TCP yuva durumunu LAST ACK durumuna yükselter ve bir FIN paketi gönderir. Ardından bağlantıyı kesmeyi tamamlamadan ve KAPALI durumuna girmeden önce istemciden bir ACK bekler.

- Diğer taraftan, bağlantı kesme isteğini başlatan ilk sunucu ise (istemci bağlantısı kesildi ve yuva hala ESTABLISHED durumda), NetX bağlantıyı başlatmak için bir FIN paketi gönderir ve bağlantıyı tamamladıktan ve yuvayı KAPALI bir durumda yerleştirmeden önce istemciden bir FIN ve ACK almak için bekler.

Yuva iletme kuyruğunda hala paketler varsa, NetX bu paketlerin kabul askıya alınması için belirtilen zaman aşımını askıya alır. Zaman aşımı süresi dolsa NetX, sunucu yuvasının iletme kuyruğundan boşaltıyor.

Bağlantı kesme işlemi tamamlandıktan ve sunucu yuvası KAPALI durumda olduktan  sonra, uygulamanın bu yuvanın sunucu bağlantı noktasıyla olan ilişkilendirmeyi sona nx_tcp_server_socket_unaccept için nx_tcp_server_socket_unaccept hizmetini çağırmış olması gerekir. Bu hizmetin, * veya * nx_tcp_socket_disconnect _ ***hata durumu nx_tcp_server_socket_accept*** uygulama **tarafından** çağrıl gerektiğini unutmayın. _ *_nx_tcp_server_socket_unaccept_** döndürdikten sonra yuva, istemci veya sunucu yuvası olarak kullanılabilir, hatta artık gerekli olmadığı sürece silinebilir. Aynı sunucu bağlantı noktası üzerinde başka bir istemci bağlantısını kabul etmek ***istenirse, nx_tcp_server_socket_relisten*** bu yuvada çağrılmalı.

Aşağıdaki kod kesimi tipik bir TCP sunucusunun kullandığı çağrı dizisini gösterir:

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

### <a name="mss-validation"></a>MSS Doğrulaması

En Büyük Kesim Boyutu (MSS), bir TCP ana bilgisayarının temel ALıNAN IP katmanı tarafından parçalanmadan aldırıla maksimum bayt miktarıdır. TCP bağlantısı kurulması aşamasında her iki uç da kendi TCP MSS değerini değiştirmektedir, böylece gönderen alıcının MSS değerinden daha büyük bir TCP veri kesimi göndermez. NetX TCP modülü, bağlantı kurmadan önce isteğe bağlı olarak eş tarafından tanıtılan MSS değerini doğrular. Varsayılan olarak NetX böyle bir denetimi etkinleştirmez. MSS doğrulaması gerçekleştirmek isteyen uygulamalar NetX **kitaplığını NX_ENABLE_TCP_MSS_CHECKING** için * NX_ENABLE_TCP_MSS_CHECKING _ tanımlamalı ve en düşük değer _*_NX_TCP_MSS_MINIMUM._*_ _ NX_TCP_MSS_MINIMUM * altında MSS *_değerlerine sahip_* gelen TCP bağlantıları bırakılır.

### <a name="stop-listening-on-a-server-port"></a>Sunucu Bağlantı Noktası Üzerinde Dinlemeyi Durdurma

Uygulama artık ***nx_tcp_server_socket_listen** _ hizmetine yapılan bir çağrıyla belirtilen bir sunucu bağlantı noktası üzerinde istemci bağlantı isteklerini dinlemek isterse, uygulama yalnızca _ *_nx_tcp_server_socket_unlisten_** hizmetini çağırıyor. Bu hizmet, bağlantı için bekleyen tüm yuvaları KAPATILI durumuna döndürür ve kuyruğa alınan tüm istemci bağlantı isteği paketlerini serbest bırakmıştır.

### <a name="tcp-window-size"></a>TCP Pencere Boyutu

Bağlantının hem kurulum hem de veri aktarımı aşamaları sırasında, her bağlantı noktası işleyene veri miktarını (pencere boyutu olarak adlandırılan) raporlar. Veriler alınarak işlendikten sonra bu pencere boyutu dinamik olarak ayarlanır. TCP'de bir gönderici yalnızca alıcının penceresine sığacak miktarda veri gönderebilir. Pencere boyutu, bağlantının her yönünde veri aktarımı için akış denetimi sağlar.

### <a name="tcp-packet-send"></a>TCP Paket Gönderme

TCP verilerini göndermek, nx_tcp_socket_send işlevi ***çağrılarak*** kolayca gerçekleştirebilirsiniz. İletilen verilerin boyutu yuvanın MSS değerinden veya geçerli eş alma penceresi boyutundan büyükse (hangisi daha küçükse), TCP iç mantığı iletim için en düşük değere (MSS, eş alma Penceresi) sığan verileri alır. Bu hizmet daha sonra paketin önünde bir TCP üst bilgisi (sağlama toplam hesaplaması dahil) derler. Alıcının pencere boyutu sıfır değildir, çağıranı alıcı pencere boyutunu doldurmak için mümkün olduğu kadar çok veri gönderir. Alma penceresi sıfır olursa, çağıranı askıya alabilir ve alıcının pencere boyutunun bu paketin göndernebilecek kadar artmasını bekleyebilir. Herhangi bir zamanda, aynı yuva üzerinden veri göndermeye çalışırken birden çok iş parçacığı askıya alabilir.

> [!IMPORTANT]
> *Bu yapıda bulunan TCP NX_PACKET uzun sözcük sınırında yer ala olmalıdır. Ayrıca, TCP, IP ve fiziksel medya üst bilgilerini yer için ön uç işaretçisi ile veri başlatma işaretçisi arasında yeterli alan olmalıdır.*

### <a name="tcp-packet-retransmit"></a>TCP Paketi Yeniden Iletim

Önceden iletilen TCP paketleri aslında bağlantının diğer tarafından bir ACK döndürülene kadar dahili olarak depolanır. İletilen veriler zaman aşımı süresi içinde onaylanmazsa, depolanan paket yeniden gönderilir ve sonraki zaman aşımı süresi ayarlanır. Bir ACK geldiğinde, iç iletme kuyruğunda onay numarası kapsamındaki tüm paketler son olarak serbest bırakıldı.

> [!IMPORTANT]
> *Uygulama paketi yeniden kullanmamalıdır veya ***** nx_tcp_socket_send _ işlevi NX_SUCCESS. İletilen paket, veriler diğer paket tarafından onaylandıktan sonra NetX iç işleme tarafından end._

### <a name="tcp-keepalive"></a>TCP Keepalive

TCP Sürekliliği özelliği, bir yuvanın uygun sonlandırma olmadan eş bağlantısının kesilip kesilmemesi (örneğin, eş kilitlenmesi) veya belirli ağ izleme tesislerinin uzun süre boşta kalma süresiyle bağlantıyı sonlandırmasını önlemesini sağlar. TCP Keepalive, düzenli aralıklarla verisi olan bir TCP çerçevesi göndererek çalışır ve dizi numarası geçerli dizi numarasından bir küçük olarak ayarlanır. Bu tür TCP Keepalive çerçevesini alan alıcı, hala canlıysa geçerli sıra numarası için bir ACK ile yanıtlar. Bu, süreklilik işlemini tamamlar.

Varsayılan olarak, tutma özelliği etkin değildir. Bu özelliği kullanmak için NetX kitaplığı * NX_ENABLE_TCP_KEEPALIVE **_** tanımlı olarak eklanmalıdır. _ *_NX_TCP_KEEPALIVE_INITIAL_** simgesi, tutma çerçevesinin başlatıldığı saniye sayısını belirtir.

### <a name="tcp-packet-receive"></a>TCP Paketi Alma

TCP alma paketi işleme (IP yardımcı iş parçacığından çağrılır) çeşitli bağlantı ve bağlantı kesme eylemlerini işlemenin yanı sıra onay iletme işleminin işlenmesinden sorumludur. Ayrıca, TCP alma paketi işleme, alma verilerine sahip paketleri uygun TCP yuvasının alma kuyruğuna yerleştirmekten veya paketi bekleyen ilk askıya alınmış iş parçacığına teslim etmekten sorumludur.

### <a name="tcp-receive-notify"></a>TCP Alma Bildirimi

Uygulama iş parçacığının birden fazla yuvadan alınan verileri işlemesi gerekirse, ***nx_tcp_socket_receive_notify*** işlevi kullanılmalıdır. Bu işlev yuva için bir alma paketi geri çağırma işlevini kaydedmektedir. Yuvada bir paket alınan her zaman, geri çağırma işlevi yürütülür.

Geri çağırma işlevinin içeriği uygulamaya özeldir; ancak, işlev büyük olasılıkla işleme iş parçacığına karşılık gelen yuvada bir paketin kullanılabilir olduğunu bildirmek için mantık içerir.

### <a name="thread-suspension"></a>İş ParçacığıNı Askıya Alma

Daha önce belirtildiği gibi, uygulama iş parçacıkları belirli bir TCP bağlantı noktası üzerinden veri almaya çalışırken askıya alabilir. Bu bağlantı noktası üzerinde bir paket alındıktan sonra, askıya alınan ilk iş parçacığına verilir ve bu iş parçacığı daha sonra devam eder. Çoğu NetX hizmeti için kullanılabilen bir özellik olan TCP alma paketi üzerinde askıya alma sırasında isteğe bağlı bir zaman aşımı mevcuttur.

İş parçacığı askıya alma, bağlantı (hem istemci hem de sunucu), istemci bağlama ve bağlantı kesme hizmetleri için de kullanılabilir.

### <a name="tcp-socket-statistics-and-errors"></a>TCP Yuvası İstatistikleri ve Hataları

Etkinleştirilirse, NetX TCP yuva yazılımı uygulama için yararlı olan çeşitli istatistikleri ve hataları takip eder. Her IP/TCP örneği için aşağıdaki istatistikler ve hata raporları korunur:

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
