---
title: TraceX Azure RTOS anlama
description: Azure RTOS TraceX, geliştiricilere gerçek zamanlı sistem olaylarının grafik görünümünü sağlayan ve gerçek zamanlı sistemlerinin davranışını görselleştirmelerine ve daha iyi anlamalarına olanak sağlayan Microsoft'un ana bilgisayar tabanlı analiz aracıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 966f3be5ebe34e006067175e422480fbf1ab664bb0ff627d7b01e71036dc5e82
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792226"
---
# <a name="overview-of-azure-rtos-tracex"></a>Azure RTOS TraceX'e genel bakış

Azure RTOS TraceX, geliştiricilere gerçek zamanlı sistem olaylarının grafik görünümünü sağlayan ve gerçek zamanlı sistemlerinin davranışını görselleştirmelerine ve daha iyi anlamalarına olanak sağlayan Microsoft'un ana bilgisayar tabanlı analiz aracıdır. Diğer Azure RTOS TraceX ile geliştiriciler, standart hata ayıklama araçlarının görünümü dışında oluşan kesintiler ve bağlam anahtarları gibi sistem olaylarının ortaya çıkmalarını net bir şekilde görebilir. Bu olayları belirleyebilme ve inceleyebilme ve bunların genel sistem işlemi bağlamında ortaya çıkma zamanlamasını belirlemek, geliştiricilerin programlama sorunlarını beklenmeyen davranış bularak çözmesine ve belirli alanları daha fazla araştırmalarına olanak tanımak için izleme bilgileri hedef sistemde arabellekte depolanır ve arabellek konumu ve boyutu çalışma zamanında uygulama tarafından belirlenir. Azure RTOS TraceX, yalnızca Azure RTOS ThreadX'ten değil, herhangi bir uygulama veya RTOS'tan doğru şekilde oluşturulmuş herhangi bir arabelleği işebilir. İzleme bilgileri, analiz için herhangi bir zamanda (son inceleme veya bir kesme noktası) ana bilgisayar üzerine karşıya yüklenebilirsiniz. Azure RTOS ThreadX, sistem arızası veya diğer önemli olaylarda en son "N" olayların inceleme için kullanılabilir olması için olanak sağlayan döngüsel bir arabelleğe sahiptir.

![Azure RTOS TraceX Single-Core Görüntüleme](./media/user-guide/screen_shot_33.png)

**TraceX Single-Core Görüntüleme**

## <a name="key-capabilites"></a>Önemli özellikler

### <a name="azure-rtos-tracex-built-in-system-analysis"></a>Azure RTOS TraceX yerleşik sistem analizi

Azure RTOS TraceX, TraceX araç çubuğundan tek bir düğme tıklama ile kullanılabilen yerleşik sistem analizi raporları sağlar. Bu düğmeler ve raporlar şunları içerir:

![Yürütme Profili raporu oluşturma](./media/overview-tracex/execution-profile-report-button.jpg) Yürütme Profili raporu oluşturma

![Performans İstatistikleri raporu oluşturma](./media/overview-tracex/performance-statistics-report-button.jpg) Performans İstatistikleri raporu oluşturma

![İş Parçacığı Yığını Kullanımı raporu oluşturma](./media/overview-tracex/thread-stack-usage-report-button.jpg) İş Parçacığı Yığını Kullanımı raporu oluşturma

### <a name="trace-data-collected-by-azure-rtos-threadx"></a>Azure RTOS ThreadX tarafından toplanan verileri izleme

Azure RTOS TraceX, çalışma zamanı Azure RTOS hedef sistemde sistem ve uygulama "olayları" veritabanı oluşturur Azure RTOS ThreadX ile çalışacak şekilde tasarlanmıştır. Bu olaylar şunlardır:

* iş parçacığı bağlam anahtarları
* preemptions
* Süspansiyon
* sonlandırmalar
* sistem kesintileri
* uygulamaya özgü olaylar
* tüm Azure RTOS ThreadX API çağrıları
* tüm Azure RTOS NetX API çağrıları
* tüm Azure RTOS FileX API çağrıları
* tüm Azure RTOS USBX API çağrıları
* uygulama tanımlı simgeler ve bilgiler

Olaylar, daha sonra uygun zaman dizisinde görüntülenilebilecek ve uygun iş parçacığıyla ilişkilendirililebilecek şekilde zaman damgası ve etkin iş parçacığı tanımlama ile program denetimi altında günlüğe kaydedilir. Olay günlüğü, örneğin bir ilgi alanıyla karşılaşıldığında uygulama programı tarafından dinamik olarak durdurulmuş ve yeniden başlatılacaktır. Bu, sistem doğru şekilde performans gösterirken veritabanının karmaşık hale gelen ve hedef belleği kullanan bir sistemden kaçınmasını sağlar.

### <a name="azure-rtos-tracex-is-like-a-software-logic-analyzer"></a>Azure RTOS TraceX bir yazılım mantığı çözümleyicisi gibi

Olay günlüğü hedef bellekten ana bilgisayarla karşıya yüklendiktan sonra Azure RTOS TraceX olayları, dikey eksende olayların ilişkili olduğu çeşitli uygulama iş parçacıkları ve sistem yordamları ile saati temsil eden yatay eksende grafik olarak görüntüler. Azure RTOS TraceX, konakta bir "yazılım mantığı çözümleyicisi" oluşturur ve sistem olaylarını açıkça görünür hale gelir. Olaylar, ilgili iş parçacığının veya sistem yordamının sağ tarafından yatay zaman çizelgesinde oluşum noktasında bulunan renk kodlu simgelerle temsil eder. Bir olay simgesi seçildiğinde, o olayla ilgili bilgilerin yanı sıra önceki ve sonraki iki olayla ilgili bilgiler görüntülenir. Bu, olay ve onun hemen çevresindeki olaylar hakkında en kısa bilgilere hızlı ve tek tıklamayla erişim sağlar. Azure RTOS TraceX, birçok iş parçacığına sahip sistemlerin analizini basitleştirmek için tüm sistem olaylarını tek bir yatay çizgide gösteren bir "Özet" ekranı sağlar.

### <a name="sequential-view-mode"></a>Sıralı görünüm modu

Sıralı görünüm modu, "Sıralı Görünüm" sekmesine tıklayarak seçilir. Bu varsayılan moddur. Bu modda olaylar, aralarında geçen süre ne olursa olsun hemen birbirinin ardından gösterilir. Ayrıca, görüntü alanı üzerindeki cetveli de not alan. İzlemenin başından itibaren göreli olay numarasını gösterir. Bu mod varsayılan moddur ve özellikle sistemde neler olduğu hakkında iyi bir genel bakış elde edin.

![Sıralı görünüm modu](./media/user-guide/screen_shot_10.png)

**Sıralı görünüm modu**

### <a name="time-view-mode"></a>Zaman görünümü modu

Bu modda olaylar, olaylar arasında yürütmeyi göstermek için kullanılan düz bir yeşil çubukla göreli olarak gösterilir. Bu mod özellikle sistemde toplu işlemenin nerede olduğunu görmek için kullanışlıdır. Bu mod, geliştiricilerin daha yüksek performans ve/veya yanıt hızı için kendi sistemini ayarlamalarına yardımcı olabilir.

Olay görüntüsünde yer alan cetvele de dikkatin. Bu cetvel, ThreadX'in içindeki olay izleme günlüğünde işaret edilen zaman damgasından türetilen, izlemenin başından itibaren göreli Azure RTOS gösterir. Zaman damgaları çok yakınsa (düşük sıklık süreölçeri), olaylar birlikte çalıştır. Buna karşılık, zaman damgaları çok uzaksa (yüksek sıklık süreölçeri), olaylar çok uzak olur. Doğru sıklık zaman damgasını seçmek, zaman göreli görünümünü anlamlı hale açısından önemli bir noktadır.

![Zaman Görünümü Modu](./media/user-guide/screen_shot_31.png)

### <a name="system-summary-line"></a>Sistem özet satırı

Azure RTOS TraceX aynı satırda yer alan tüm olayları içeren tek bir özet satırı da sağlar. Özet satırı, bağlamın bir özetini ve altındaki ilgili olay özetini içerir. Bu, karmaşık bir sisteme genel bakış görmeyi kolaylaştırır. Özet çubuğu özellikle çok sayıda iş parçacığına sahip sistemlerde yararlıdır. Böyle bir özet satırı olmadan, kullanıcının yürütme bağlamını takip etmek için dikey kaydırma çubuğunu kullanarak karmaşık sistem etkileşimlerini izlemesi gerekir.

Azure RTOS TraceX, ekranın sol tarafında sistem bağlamlarını listeler.
Belirli bir bağlamda oluşan olaylar, bu bağlamın sağ tarafından yatay çizgide görüntülenir. Bu şekilde, kullanıcı olayın hangi bağlamın meydana geldiği kolayca tespit edilebilir ve belirli bir bağlamda meydana gelen tüm olayları görmek için bu bağlam çizgilerini takip eder.

![Sistem Özet Satırı](./media/user-guide/screen_shot_32.png)

**Sistem Özet Satırı**

İlk iki bağlam girişi her zaman "Kesme" ve "Başlat/Boşta" bağlamlarıdır. "Kesme" bağlamı, Kesinti Hizmeti Yordamlarından (ISR) yapılan tüm sistem olaylarını temsil eder. "Başlat/Boşta" bağlamı, ThreadX'te Azure RTOS temsil eder. Başlatma sırasında tx_application_define olaylar " Başlat" olaylarıdır ve "Başlat/Boşta" bağlamında görüntülenir. Sistem boşta ise ve bu nedenle hiçbir olay meydana yoksa, zaman görünümünde "Çalışıyor" ifadesini temsil eden yeşil çubuk "Başlat/Boşta" bağlamında çizilir.

## <a name="methods-of-navigation"></a>Gezinti yöntemleri

Azure RTOS TraceX, geliştiricinin "Sonraki" ve "Önceki" gezinti düğmelerinin nasıl çalışılır olduğunu belirtmelerini sağlar.

![Gezinti düğmeleri](./media/user-guide/event.png)

"Olay" seçilirse, gezinti sonraki/önceki olayda yapılır. "Bağlam" seçilirse, gezinti aynı bağlamda bir sonraki/önceki olayda yapılır. "Nesne" seçilirse, gezinti geçerli nesnenin sonraki/önceki olayında (örneğin, belirli bir kuyrukla ilişkili olaylar) yapılır. "Anahtarlar" seçilirse, gezinti sonraki/önceki bağlam anahtarında yapılır. "Aynı Kimlik" seçilirse, gezinti aynı olay kimliği için sonraki/önceki olayda yapılır.

### <a name="event-information-display"></a>Olay bilgileri görüntüleme

Azure RTOS TraceX bazı 300 olay hakkında ayrıntılı bilgi sağlar. Bunlar altı iç Azure RTOS ThreadX olayı, iki ISR olayı (enter ve çıkış), 14 iç Azure RTOS FileX olayı, 42 iç Azure RTOS NetX olayı ve bir kullanıcı tanımlı olaydır. Kalan olaylar doğrudan Azure RTOS, Azure RTOS FileX ve NetX API Azure RTOS karşılık gelir.
Sıralı veya zaman görüntüleme modunun seçili olup olmadığı ne olursa olsun, görüntüleme alanında herhangi bir olayın üzerine fareyle yapılan bir fare ile olayın yakınında ayrıntılı olay bilgileri görüntülenir. Tanıtım demo_threadx.trx izleme dosyasındaki olay 494'ü fareyle üzerine bırakma aşağıda gösterilmiştir:

![Mouse-Over Daha Fazla Bilgi Görüntüler](./media/user-guide/screen_shot_37.png)

**Fareyle Üzerine Doğru Daha Fazla Bilgi Görüntülenir**

Görüntülenen her olay Bağlam ve hem Göreli Saat hem de Zaman Damgası hakkında standart bilgiler içerir. Bağlam alanı, olayın hangi bağlamda olduğunu gösterir. Tam olarak dört bağlam vardır: iş parçacığı, boşta, ISR ve başlatma. Bir olay bir iş parçacığı bağlamında olduğunda, o anda iş parçacığı adı ve önceliği toplanıp yukarıda gösterildiği gibi görüntülenir. Göreli Saat, izlemenin başından itibaren zamanlayıcı saat işaretlerinin göreli sayısını gösterir. Ham Zaman Damgası olayın ham saat kaynağını görüntüler. Son olarak, olaya özgü tüm bilgiler görüntülenir.

### <a name="zooming-in-and-out"></a>Yakınlaştırma ve uzaklaştırma

Varsayılan olarak, Azure RTOS TraceX olayları 1:1 piksel: Tick eşlemesi ile kolay bir biçimde görüntüler. Kullanıcı istediğiniz gibi yakınlaştırabilir veya yakınlaştırabilir. %100 ' a yakınlaştırmak, geçerli görüntü görünümündeki izlemenin tamamını görmek için yararlıdır, ancak yakınlaştırma, zaman damgası kaynağı çözümlenmesinden dolayı olayların çakıştığı koşullarda yararlı olur.

![Ayrıntılar için %100 Zoom-Out görüntüleyin veya yakınlaştırın](./media/user-guide/screen_shot_41.png)

**Ayrıntılar için %100 oranında yakınlaştırın veya yakınlaştırabilirsiniz**

%100 oranında yakınlaştırıldığında, tüm izlemenin geçerli görüntü sayfası içinde gösterilmesi için, izlemede yakalanan tüm bağlam yürütmesinin yanı sıra bu bağlamlarda gerçekleşen genel olayları görmek kolaydır. "İş parçacığı 1" ve "iş parçacığı 2" nin en sık yürütüdiğine dikkat edin. Olayları için mavi renklendirme, bu iş parçacıklarının sıra hizmeti çağrıları (kuyruk olayları renkli olarak mavi) yapmasını da önerir.

Tam bir simge görünümüne geri yükleme işlemi eşit derecede kolaydır; Yakınlaştır düğmesi tekrar tekrar seçilebilir veya bazı 100 faktörü girilmiş olabilir.

### <a name="delta-ticks-between-events"></a>Olaylar arasındaki Delta işaretleri

Azure RTOS TraceX içindeki çeşitli olaylar arasındaki işaret sayısını belirlemek kolaydır; başlangıç olayına tıklayıp fareyi bitiş olayına sürüklemeniz yeterlidir.
Olaylar arasındaki üçgen sayısı, ekranın sağ üst köşesinde görünür.

![Delta Işaretleri](./media/user-guide/screen_shot_42.png)

**Delta Işaretleri**

Delta işaretleri 5032 olay 494 ve olay 496 arasında ticks geçtiğini gösterir. Bu, her bir olaydaki göreli zaman damgalarına bakarak ve çıkararak el ile de hesaplanabilir, ancak GUI kullanımı kolay ve anında gerçekleşir.

### <a name="priority-inversions"></a>Öncelikli Inversions 'ları

Azure RTOS TraceX, izleme dosyasında algılanan öncelik ınksürümlerini otomatik olarak görüntüler. Öncelikli Inversions, daha yüksek öncelikli bir iş parçacığının daha düşük öncelikli bir iş parçacığına ait olan bir mutex elde edilmeye çalıştığı durumlar olarak tanımlanır. Bu koşul, sistem bu şekilde çalışacak şekilde kurulduğundan "belirleyici" olarak adlandırılır. Kullanıcıyı bilgilendirmek için, Azure RTOS tracex, hafif somon rengi olarak "belirleyici" öncelik Inversion aralıklarını gösterir.

Azure RTOS TraceX Ayrıca "belirleyici olmayan" öncelikli Inversions 'ları de görüntüler. Bu öncelikli sürümler, farklı bir öncelik düzeyi olan başka bir iş parçacığının "belirleyici" öncelikli sürümünün ortasında yürütülmesi nedeniyle "belirleyici" öncelikli olmayan sürümlerden farklıdır. bu sayede, öncelik sürümü "belirleyici" olarak zaman içinde zaman ortaya çıkardı. Bu durum genellikle kullanıcı için bilinmemektedir ve çok önemli olabilir. Bu koşulun kullanıcısına uyarı vermek için, Azure RTOS tracex, daha parlak somon rengi olarak "belirleyici olmayan" öncelikli yük sürümlerini gösterir.

![Belirleyici ve belirleyici olmayan öncelikli geçersiz sürüm](./media/user-guide/screen_shot_43.png)

**Belirleyici ve belirleyici olmayan öncelikli geçersiz sürüm**

### <a name="execution-profile"></a>Yürütme profili

Azure RTOS TraceX, şu anda yüklü olan izleme dosyasında yer alan tüm yürütme bağlamları için yerleşik bir yürütme profili raporu sağlar.

![Yürütme profili](./media/user-guide/execution_profile.png)

### <a name="performance-statistics"></a>Performans istatistikleri

Azure RTOS TraceX, şu anda yüklü olan izleme dosyası için yerleşik bir performans istatistikleri raporu sağlar.

![Performans istatistikleri](./media/user-guide/performance_statistics.png)

### <a name="thread-stack-usage"></a>İş parçacığı yığını kullanımı

Azure RTOS TraceX, şu anda yüklü olan izleme dosyasında içinde çalışan tüm iş parçacıkları için yerleşik bir yığın kullanım raporu sağlar.

![Yığın kullanımı](./media/user-guide/thread_stack_usage.png)

Azure RTOS TraceX, şu anda yüklü olan izleme dosyasının Azure RTOS FileX performans istatistiklerini gösterir. Bu bilgiler tüm açık medya nesnelerinde tüm sistem için görüntülenir.

![FileX istatistikleri](./media/user-guide/filex_statistics.png)

### <a name="azure-rtos-netx-statistics"></a>Azure RTOS NetX istatistikleri

Azure RTOS TraceX, şu anda yüklü olan izleme dosyasının NetX performans istatistiklerini de sunmaktadır. Bu bilgiler tüm sistem için görüntülenir.

![NetX istatistikleri](./media/user-guide/netx_statistics.png)

### <a name="raw-trace-dump"></a>Ham izleme dökümü

Azure RTOS TraceX, metin biçiminde bir ham izleme dosyası oluşturabilir ve Not defteri 'ni başlatarak onu görüntüleyebilir.

![Ham izleme dökümü](./media/user-guide/raw_trace_dump.png)

Listelenen tüm zamanlama ve boyut rakamların tahminlerinin olduğunu ve geliştirme platformunuzun farklı olabileceğini lütfen unutmayın
