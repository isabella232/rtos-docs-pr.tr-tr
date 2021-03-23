---
title: Azure RTOS TraceX 'i anlama
description: Azure RTOS TraceX, geliştiricilerin gerçek zamanlı sistem olaylarının grafik bir görünümünü sunan ve gerçek zamanlı sistemlerinin davranışını görselleştirmesini ve daha iyi anlamasına olanak tanıyan ana bilgisayar tabanlı çözümleme aracıdır.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 9fd33eec6da69e6dda421a125a2dde5eae93b46d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104828625"
---
# <a name="overview-of-azure-rtos-tracex"></a>Azure RTOS TraceX 'e genel bakış

Azure RTOS TraceX, geliştiricilerin gerçek zamanlı sistem olaylarının grafik bir görünümünü sunan ve gerçek zamanlı sistemlerinin davranışını görselleştirmesini ve daha iyi anlamasına olanak tanıyan ana bilgisayar tabanlı çözümleme aracıdır. Azure RTOS TraceX sayesinde, geliştiriciler standart hata ayıklama araçlarının görünümünden oluşan kesmeler ve bağlam anahtarları gibi sistem olaylarının kullanımını açıkça görebilirler. Bu olayları belirleme ve denetleme ve genel sistem işleminin bağlamında yaptığı oluşumların zamanlamasını belirlemek, geliştiricilerin beklenmedik davranışı bularak programlama sorunlarını çözmelerini ve belirli alanlara daha fazla bilgi vermelerini sağlamak için, uygulama tarafından çalışma zamanında belirlenen arabellek konumu ve boyutu ile hedef sistemdeki bir arabellekte depolanır. Azure RTOS TraceX, yalnızca Azure RTOS ThreadX 'den değil, ancak herhangi bir uygulamadan veya RTOS 'a değil, doğru şekilde oluşturulmuş olan her bir arabelleği işleyebilir. İzleme bilgileri dilediğiniz zaman analiz edilmek üzere konağa yüklenebilir; ya da ya da bir kesme noktası üzerinde. Azure RTOS ThreadX, en son "N" olaylarının sistem arızası veya diğer önemli olay durumunda İnceleme için kullanılabilir olmasını sağlayan bir döngüsel arabellek uygular.

![Azure RTOS TraceX Single-Core görüntüleme](./media/user-guide/screen_shot_33.png)

**TraceX Single-Core görüntüleme**

## <a name="key-capabilites"></a>Key özelliklere

### <a name="azure-rtos-tracex-built-in-system-analysis"></a>Azure RTOS TraceX yerleşik Sistem Analizi

Azure RTOS TraceX, TraceX araç çubuğundan tek bir düğme ile kullanılabilen yerleşik sistem analiz raporları sağlar. Bu düğmeler ve raporlar şunları içerir:

![Yürütme profili raporu oluştur](./media/overview-tracex/execution-profile-report-button.jpg) Yürütme profili raporu oluştur

![Performans Istatistikleri raporu oluştur](./media/overview-tracex/performance-statistics-report-button.jpg) Performans Istatistikleri raporu oluştur

![Iş parçacığı yığını kullanım raporu oluştur](./media/overview-tracex/thread-stack-usage-report-button.jpg) Iş parçacığı yığını kullanım raporu oluştur

### <a name="trace-data-collected-by-azure-rtos-threadx"></a>Azure RTOS ThreadX tarafından toplanan izleme verileri

Azure RTOS TraceX, çalışma zamanı sırasında hedef sistemde sistem ve uygulama "olaylarının" bir veritabanını oluşturan Azure RTOS ThreadX ile çalışmak üzere tasarlanmıştır. Bu olaylar şunları içerir:

* iş parçacığı bağlam geçişleri
* preemptions
* getirilmesi
* sonlanmaları
* Sistem kesmeleri
* uygulamaya özgü olaylar
* Tüm Azure RTOS ThreadX API çağrıları
* Tüm Azure RTOS NetX API çağrıları
* Tüm Azure RTOS FileX API çağrıları
* Tüm Azure RTOS USBX API çağrıları
* uygulama tanımlı simgeler ve bilgiler

Olaylar, zaman damgalama ve etkin iş parçacığı tanımlama ile program denetimi altında günlüğe kaydedilir, böylece daha sonra uygun zaman dizisinde görüntülenebilirler ve uygun iş parçacığıyla ilişkilendirilir. Olay günlüğü, uygulama programı tarafından dinamik olarak durdurulabilir ve yeniden başlatılabilir, örneğin, bir ilgi alanına rastlandı. Bu, sistemin doğru şekilde gerçekleştirilirken veritabanını bir şekilde ve hedef belleği kullanmaya karşı engeller.

### <a name="azure-rtos-tracex-is-like-a-software-logic-analyzer"></a>Azure RTOS TraceX, bir yazılım mantığı Çözümleyicisi gibidir

Olay günlüğü hedef bellekten konağa yüklendikten sonra, Azure RTOS TraceX olayları, olayları temsil eden bir yatay eksende, olayların dikey eksen üzerinde listelenen çeşitli uygulama iş parçacıkları ve sistem yordamları ile grafik olarak görüntülenir. Azure RTOS TraceX konakta bir "yazılım Logic Analyzer" oluşturur ve sistem olayları görünür hale getirir. Olaylar, ilgili iş parçacığının veya sistem yordamının sağında yer alan yatay zaman çizelgesi üzerindeki oluşum noktasında bulunan renk kodlu simgelerle temsil edilir. Bir olay simgesi seçildiğinde, söz konusu olayla ilgili bilgilerin yanı sıra önceki iki ve sonraki iki olay için de bilgiler görüntülenir. Bu, olay ve bu nesnenin hemen çevredeki olayları hakkında en çabuk bilgilere hızlı, tek tıklamayla erişim sağlar. Azure RTOS TraceX, birçok iş parçacığından oluşan sistemlerin analizini kolaylaştırmak için tek bir yatay satırdaki tüm sistem olaylarını gösteren bir "Özet" ekranı sağlar.

### <a name="sequential-view-mode"></a>Sıralı Görünüm modu

Sıralı Görünüm modu, "Sıralı Görünüm" sekmesine tıklanarak seçilir. Bu varsayılan moddur. Bu modda olaylar, aralarında geçen süreden bağımsız olarak, birbirleriyle hemen sonra gösterilir. Ayrıca, görüntü alanının üzerindeki cetveli de göz önünde bulabilirsiniz. İzlemenin başından ilgili olay numarasını gösterir. Bu mod varsayılan moddur ve özellikle sistemde neler olduğuna ilişkin iyi bir genel bakış elde etmek için kullanışlıdır.

![Sıralı Görünüm modu](./media/user-guide/screen_shot_10.png)

**Sıralı Görünüm modu**

### <a name="time-view-mode"></a>Zaman görünümü modu

Bu modda olaylar, olaylar arasındaki yürütmeyi göstermek için düz bir yeşil çubukla birlikte zaman göreli olarak gösterilir. Bu mod özellikle, geliştiricilerin sistemde daha fazla performans ve/veya yanıt verme için sistem ayarlarını ayarlayabilmesine yardımcı olabilecek, işleme toplu işlemin nerede olduğunu görmek için yararlıdır.

Ayrıca, olay görüntüsüne ait olan cetveli de göz önünde bulabilirsiniz. Bu cetvelde, Azure RTOS ThreadX 'in içindeki olay izleme günlüğü 'nde gösterilen zaman damgasından türetildiği gibi, izlemenin başından itibaren göreli ticks gösterilmektedir. Zaman damgaları çok yakın (Düşük Sıklık süreölçeri) ise, olaylar birlikte çalışır. Buna karşılık, zaman damgaları çok uzakta (yüksek sıklık süreölçeri), olaylar çok uzakta olacaktır. Doğru sıklık zaman damgasını seçmek, zaman göreli görünümü anlamlı hale getirmek için önemli bir konudur.

![Zaman görünümü modu](./media/user-guide/screen_shot_31.png)

### <a name="system-summary-line"></a>Sistem Özeti satırı

Azure RTOS TraceX aynı satırdaki tüm olayları içeren tek bir Özet çizgisi de sağlar. Özet satırı, aşağıda karşılık gelen olay özetinin yanı sıra bağlamın bir özetini içerir. Bu, karmaşık bir sisteme genel bakış görmenizi kolaylaştırır. Özet çubuğu, çok sayıda iş parçacığına sahip olan sistemlerde özellikle faydalıdır. Bu tür bir Özet satırı olmadan, kullanıcının Yürütme bağlamını izlemek için dikey kaydırma çubuğunu kullanarak karmaşık sistem etkileşimlerini izlemesi gerekir.

Azure RTOS TraceX, ekran sol tarafındaki sistem bağlamlarını listeler.
Belirli bir bağlamda oluşan olaylar, bu bağlamın sağındaki yatay satırda görüntülenir. Bu şekilde Kullanıcı, olayın hangi bağlamdan oluştuğunu kolayca belirleyebilir ve belirli bir bağlamda gerçekleşen tüm olayları görmek için bu bağlam satırını izleyebilir.

![Sistem Özeti satırı](./media/user-guide/screen_shot_32.png)

**Sistem Özeti satırı**

İlk iki bağlam girişi her zaman "kesme" ve "başlatma/boşta" bağlamıdır. "Kesme" bağlamı, kesme hizmeti yordamlarından (ISRS) yapılan tüm sistem olaylarını temsil eder. "Initialize/Idle" bağlamı, Azure RTOS ThreadX içindeki iki bağlamı temsil eder. Tx_application_define sırasında oluşan olaylar "Initialize" olayıdır ve "Initialize/Idle" bağlamında görüntülenir. Sistem boşta kalırsa ve hiçbir olay gerçekleşmeden, zaman görünümünde "çalışıyor" seçeneğini belirten yeşil çubuk "başlatma/boşta" bağlamında çizilir.

## <a name="methods-of-navigation"></a>Gezinti yöntemleri

Azure RTOS TraceX, geliştiricinin "Ileri" ve "önceki" gezinme düğmelerinin nasıl çalıştığını belirtmesini sağlar.

![Gezinti düğmeleri](./media/user-guide/event.png)

"Olay" seçilirse, sonraki/önceki olayda gezinme yapılır. "Bağlam" seçilirse, aynı bağlamdaki sonraki/önceki olayda gezinme yapılır. "Nesne" seçilirse, geçerli nesnenin bir sonraki/önceki olayında (örneğin, belirli bir kuyrukla ilişkili olaylar) gezinme yapılır. "Anahtarlar" seçilirse, bir sonraki/önceki bağlam anahtarında gezinme yapılır. "Aynı KIMLIK" seçilirse, aynı olay KIMLIĞI için bir sonraki/önceki olayda gezinme yapılır.

### <a name="event-information-display"></a>Olay bilgileri görünümü

Azure RTOS TraceX, bazı 300 olayları hakkında ayrıntılı bilgi sağlar. Bunlar arasında altı adet iç Azure RTOS ThreadX olayı, iki ıSR olayı (Enter ve çıkış), 14 iç Azure RTOS FileX olayları, 42 iç Azure RTOS NetX olayları ve Kullanıcı tanımlı bir olay bulunur. Kalan olaylar doğrudan Azure RTOS ThreadX, Azure RTOS FileX ve Azure RTOS NetX API hizmetlerine karşılık gelir.
Sıralı veya zaman görüntüleme modunun seçili olmasından bağımsız olarak, görüntüleme alanındaki herhangi bir olay üzerinde bir fare, olayın yakınında ayrıntılı olay bilgilerinin görüntülenmesine neden olur. Demo demo_threadx. trx izleme dosyasındaki 494 olayı üzerinde fare üzerinden fare, burada gösterilmektedir:

![Mouse-Over daha fazla bilgi görüntüler](./media/user-guide/screen_shot_37.png)

**Fare üzerindeyken daha fazla bilgi görüntülenir**

Her olay, bağlam ve göreli saat ve zaman damgası hakkında standart bilgiler içerir. Bağlam alanı, olayın gerçekleştiği bağlamı gösterir. Yalnızca dört bağlam vardır: iş parçacığı, boşta, ıSR ve başlatma. Bir iş parçacığı bağlamında bir olay gerçekleştiğinde, iş parçacığı adı ve o zaman önceliği yukarıda gösterildiği gibi toplanır ve görüntülenir. Göreli süre, izlemenin başından itibaren Zamanlayıcı onay işaretleri sayısını gösterir. Ham zaman damgası, olayın ham saat kaynağını gösterir. Son olarak, olaya özgü tüm bilgiler görüntülenir.

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
