---
title: Bölüm 3-Azure RTOS TraceX açıklaması
description: Bu bölümde, GUI 'nin genel işlevselliği de dahil olmak üzere Azure RTOS TraceX sistem analizi aracının genel işlevselliği açıklanmaktadır.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: bb466427374659027bf91c7bb46c74e7d2ff561d200db9dab1a2bddbe6635ef4
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116789535"
---
# <a name="chapter-3---description-of-azure-rtos-tracex"></a>Bölüm 3-Azure RTOS TraceX açıklaması

Bu bölümde, GUI 'nin genel işlevselliği de dahil olmak üzere Azure RTOS TraceX sistem analizi aracının genel işlevselliği açıklanmaktadır. 

## <a name="display-overview"></a>Genel bakışı görüntüle

**Şekil 4** ' te, tracex sistem analizi aracının ana görüntü penceresi gösterilmektedir. Düzen basittir — Yürütme bağlamları, sol taraftaki dikey öğelerle temsil edilir; Örneğin, başlatma, kesme, boşta ve çeşitli iş parçacığı girdileri. Her bağlamda gerçekleşen olaylar yatay olarak aynı bağlam satırında görüntülenir. Örneğin, aşağıda gösterilen **QR** olayları **_iş parçacığı 2_*_, _ tx_queue_receive için birbirini izleyen çağrılar yapıyor***.

![TraceX sistem analizi aracının ana görüntü penceresinin ekran görüntüsü.](./media/user-guide/screen_shot_10.png)


**ŞEKIL 5**

Bağlam değişiklikleri, bağlam çizgilerini bağlayan dikey siyah çizgiler tarafından temsil edilir. Şu anda seçili olan olay düz bir kırmızı dikey çizgi ile temsil edilir. Bu örnekte, Event 494 seçilidir.

## <a name="title-bar"></a>Başlık Çubuğu

TraceX başlık çubuğu çeşitli yararlı bilgiler sağlar. İlk olarak, TraceX 'in geçerli sürümüdür. İkincisi, şu anda açık olan izleme dosyasının tam yoludur. **Şekil 6** ' da örnek **_tracex_*_ Version _*_6.0.0_*_ ' i _*_demo_threadx. trx_** izleme dosyasını görüntülüyor.

![TraceX başlık çubuğunun ekran görüntüsü.](./media/user-guide/screen_shot_11.png)

**ŞEKIL 6**

## <a name="tool-bar"></a>Araç çubuğu

TraceX araç çubuğu, izleme dosyalarını açmak ve bunların görüntüleme öğelerini denetlemek için çeşitli düğmeler sağlar.

![TraceX araç çubuğunun ekran görüntüsü.](./media/user-guide/screen_shot_12.png)


**ŞEKIL 7**

Soldan sağa doğru TraceX araç çubuğu düğmeleri aşağıdaki gibi tanımlanır:
                                             
| **Düğme**                         | **İşlev** |
| ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| ![İzleme dosyasını aç düğmesi](./media/user-guide/screen_shot_13.png)      | Bir izleme dosyası açın |
| ![Kullanıcı Kılavuzu düğmesini aç](./media/user-guide/screen_shot_14.png)      | Bu kullanıcı kılavuzunu aç |
| ![Yürütme profili oluştur düğmesi](./media/user-guide/screen_shot_15.png)       | Yürütme profili oluştur |
| ![ Performans istatistikleri oluştur düğmesi](./media/user-guide/screen_shot_16.png)       | Performans istatistikleri oluşturma |
| ![Iş parçacığı yığını kullanımı oluştur düğmesi](./media/user-guide/screen_shot_17.png)       | Iş parçacığı yığını kullanımı oluştur |
| ![Seçili olay düğmesini görüntüle](./media/user-guide/screen_shot_18.png)       | Seçili durumdaki olayı görüntüle |
| ![Arama düğmesi](./media/user-guide/screen_shot_19.png)      | Olayları ara |
| ![Yakınlaştır düğmesi](./media/user-guide/screen_shot_20.png)      | Yakınlaştırın. |
| ![Görüntü Yakınlaştır düğmesi](./media/user-guide/screen_shot_21.png)      | Görüntü yakınlaştırma yüzdesini seçin; burada %100, tüm izleme dosyası geçerli görünüm içinde görüntülenir. |
| ![Uzaklaştır düğmesi](./media/user-guide/screen_shot_22.png)      | Uzaklaştırın. |
| ![İlk olayı Seç düğmesi](./media/user-guide/screen_shot_23.png)      | İlk olayı seçin. |
| ![Önceki olay sayfasını görüntüle düğmesi](./media/user-guide/screen_shot_24.png)      | Önceki olay sayfasını görüntüle. |
| ![Önceki olay düğmesini görüntüle](./media/user-guide/screen_shot_25.png)      | Önceki olayı görüntüle. |
| ![Sonraki/önceki gezinti düğmesi](./media/user-guide/screen_shot_26.png)      | Sonraki/önceki gezinme düğmelerinin nasıl çalıştığını belirleme. ***Event** _ seçilirse, sonraki/önceki olayda gezinme yapılır. _*_Bağlam_*_ seçilirse, belirtilen bağlamdaki sonraki/önceki olayda gezinme yapılır. _*_Nesne_*_ seçiliyse, belirtilen nesnenin sonraki/önceki olayında gezinme yapılır; Örneğin, belirli bir kuyrukla ilişkili olaylar. _*_Anahtarlar_*_ seçiliyse, bağlam içindeki bir sonraki/önceki değişiklik üzerinde gezinme yapılır. _ *_ID_** seçilirse, BELIRTILEN olay kimliğinin sonraki/önceki olayında gezinme yapılır. |
| ![Sonraki olayı görüntüle düğmesi](./media/user-guide/screen_shot_27.png)      | Sonraki olayı görüntüle. |
| ![Sonraki olay sayfasını görüntüle düğmesi](./media/user-guide/screen_shot_28.png)      | Sonraki olay sayfasını görüntüle. |
| ![Son olayı Seç düğmesi](./media/user-guide/screen_shot_29.png)      | Son olayı seçin. |

## <a name="display-mode-tabs"></a>Görüntüleme modu sekmeleri

Trackingex, sistem olaylarını iki farklı şekilde görüntüler: *sıralı* ve *zaman göreli*. Varsayılan mod sıralıdır ve **Şekil 8**' de gösterilen moddur.

Modu değiştirmek, TraceX penceresinde ***sıralı görünüm** _ veya _*_zaman görünümü_*_ sekmelerini seçmek kadar basittir. _*Şekil 8** **_sıralı görünüm_*_ ve _ *_Saat Görünümü_** sekmelerini gösterir.

![Sıralı Görünüm ve zaman görünümü sekmelerinin ekran görüntüsü.](./media/user-guide/screen_shot_30.png)

**ŞEKIL 8**

## <a name="sequential-view-mode"></a>Sıralı Görünüm modu

Sıralı Görünüm modu _ * Şekil 8 * * ' de gösterilen ***sıralı görünüm** _ sekmesi tarafından seçilir. Bu varsayılan moddur. Bu modda, olaylar gösterilecek anlık ileti.. aralarında geçen süre ne olursa olsun, birbirini izleyen/mediately. Ayrıca **Şekil 8**' de görüntü alanının üzerindeki cetveli de göz önünde bulabilirsiniz. İzlemenin başından ilgili olay numarasını gösterir.

Bu mod varsayılan moddur ve sistemde neler olduğuna ilişkin iyi bir genel bakış elde etmek için kullanışlıdır.

## <a name="time-view-mode"></a>Zaman görünümü modu

Zaman görünümü modu ***zaman görünümü** _ düğmesi tarafından seçilir. _ *Şekil 9**, zaman görünümü modu dışında **Şekil 8** ' de aynı olay izlemesini gösterir. Bu modda, olaylar arasındaki yürütmeyi göstermek için düz yeşil çubuğun kullanıldığı zaman göreli bir şekilde olaylar gösterilir. Bu mod, geliştiricilerin sistemde daha fazla performans ve/veya yanıt verme için sistem ayarlarını ayarlayabilmesine yardımcı olan işleme toplu işleminin nerede olduğunu görmek için yararlıdır.

![Zaman görünümü sekmesinin ekran görüntüsü.](./media/user-guide/screen_shot_31.png)

**ŞEKIL 9**

Ayrıca **Şekil 9**' da olay görünümü ' nde bulunan cetvelin üzerine göz önünde bırakabilirsiniz. Bu cetvel, ThreadX içindeki olay izleme günlüğü 'nde gösterilen zaman damgasından türetilen şekilde izlemenin başından itibaren göreli işaretleri gösterir. Zaman damgaları çok yakınsa (Düşük Sıklık süreölçeri), olaylar birlikte çalışır. Buna karşılık, zaman damgaları çok uzakta (yüksek sıklık süreölçeri), olaylar çok uzakta olur. Doğru sıklık zaman damgasını seçmek, zaman göreli görünümü anlamlı hale getirmek için önemli bir konudur.

## <a name="system-summary-line"></a>Sistem Özeti satırı

TraceX ayrıca aynı satırdaki tüm olayları içeren tek bir Özet çizgisi ( **Şekil 10**' da üst bağlam) sağlar. Bu, karmaşık bir sisteme genel bakış görmenizi kolaylaştırır. Özet çubuğu, çok sayıda iş parçacığı olan sistemlerde özellikle faydalıdır. Bu tür bir Özet satırı olmadan, yürütme bağlamını izlemek için dikey kaydırma çubuğunu kullanarak karmaşık sistem etkileşimlerini izlemeniz gerekir.

![Sıralı Görünüm sekmesindeki Sistem Özet hattının ekran görüntüsü.](./media/user-guide/screen_shot_32.png)


**ŞEKIL 10**

Özet satırı, aşağıda karşılık gelen olay özetinin yanı sıra bağlamın bir özetini içerir. **Şekil 10** ' da gösterilen örnekte, **_2. iş parçacığının_*yürütüldüğü ve kesintiye uğratıldığını görmek kolaydır. Kesme sonuçları _*_iş parçacığı 3_**, ***iş parçacığı 6** _, _*_iş parçacığı 4_*_ ve iş parçacığı _*_7_*_' den sonra _ *_iş parçacığı 2_** yürütmeye devam eder.

## <a name="system-contexts"></a>Sistem bağlamları

TraceX, **Şekil 11**' de gösterildiği gibi, ekran sol tarafındaki sistem bağlamlarını listeler. Belirli bir bağlamda oluşan olaylar, bu bağlamın sağındaki yatay satırda görüntülenir. Bu şekilde, olayın hangi bağlamdan oluştuğunu kolayca belirleyebilir ve belirli bir bağlamda gerçekleşen tüm olayları görmek için bu bağlam satırını izleyebilirsiniz.

İlk Tow bağlam girişleri her zaman ***Interrupt** _ ve _*_Initialize/Idle_*_ bağlamlarıdır. _*_Kesme_*_ bağlamı, kesme hizmeti yordamlarından (IRS) yapılan tüm sistem olaylarını temsil eder. _*_Başlatma/boşta_*_ bağlam, threadx içindeki iki bağlamı temsil eder. _*_Tx_application_define_*_ sırasında oluşan olaylar, _*_Initialize/Idle_*_ bağlamıdır. Sistem boşta kalırsa ve bu nedenle hiçbir olay gerçekleşmeden, zaman görünümünde _*_çalışmayı_*_ gösteren yeşil çubuk _ *_Initialize/Idle_** bağlamında çizilir.

![Ekran sol tarafındaki sistem bağlamlarının ekran görüntüsü.](./media/user-guide/screen_shot_33.png)

**ŞEKIL 11**

**Şekil 11**' deki örnekte, **_sistem Zamanlayıcı iş parçacığı_ _ bağlamından başlayarak dokuz iş parçacığı bağlamı vardır *. Tek bir bağlam hakkındaki ek bilgiler, fareyi bu bağlam üzerine yerleştirerek kullanılabilir. Ek bilgiler, iş parçacığının başlangıç yığını adresini, bitiş yığını adresini, toplam boyut, kullanılan yüzde, göreli yürütme yüzdesini, askıya alma, bağlantının sürdürülmesi sayısı ve izleme sırasında en yüksek ve en düşük önceliği içerir. _* Şekil 12** **_iş parçacığı 0_** için bilgileri gösterir.

![0 iş parçacığı için bilgilerin ekran görüntüsü.](./media/user-guide/screen_shot_34.png)


**ŞEKIL 12**

Bağlamlar, daha fazla ilgi çekici olanları gruplamak için de taşınabilir. Bu, bağlamı sürükleyip bırakarak veya içeriğe sağ tıklanarak yapılır. Bağlam öğesine sağ tıklamak, bağlamı yukarıya veya en alta taşımak için bir iletişim kutusu oluşturur. 

***İlk** _ ' i seçtiğinizde, _*_iş parçacığı 3_*_ bağlamı bağlam listesinin üst kısmına taşınıyor ve _ * şekil 13 * * ' de gösterildiği gibi sonuçlanır.

![Bağlam listesinin en üstüne taşınan bağlamın ekran görüntüsü.](./media/user-guide/screen_shot_35.png)


**ŞEKIL 13**

## <a name="thread-status-information"></a>İş parçacığı durum bilgileri

Etkin olduğunda, TraceX iş parçacığının bağlamındaki renkli bir çizgi aracılığıyla her bir iş parçacığının durumunu görüntüler. Yeşil bir çizgi, iş parçacığının "Ready" durumunda olduğunu belirtir, diğer bir deyişle başka bir renkte bir satır iş parçacığının askıya alındığını gösterir. Askıya alınan iş parçacıkları için satırın rengi, iş parçacığının askıya alındığı ThreadX nesnesinin türünü gösterir. Örneğin, **Şekil 13** ' te, **olay 147 ' den başlayarak _sistem Zamanlayıcı iş parçacığının_*_ bağlamındaki* yeşil çizgi, _ _sistem Zamanlayıcı iş parçacığı_*_ ' nin hazırlandığını gösterir. Olay 147 ' den ve 154 olaydan sonra, yeşil çizginin yokluğu, _*_sistem Zamanlayıcı iş parçacığı_*_ ' nin hazırlandığını gösterir. Olay 147 ' den ve 154 olaydan sonra, yeşil çizginin yokluğu, _*_sistem Zamanlayıcı iş parçacığının_** askıya alındığını gösterir.

![İş parçacığının bağlamındaki renkli bir çizgi aracılığıyla her iş parçacığının durumunun ekran görüntüsü.](./media/user-guide/screen_shot_36.png)

**ŞEKIL 14**

***Seçenekler-> durum satırları** _ menüsü aracılığıyla kullanılabilen üç iş parçacığı durumu görüntüleme modu vardır. _*_Yalnızca Ready_*_ seçeneği, yalnızca Ready (yeşil) durum satırlarını gösterir, ancak askıya alınma durumu satırlarını göstermez. Bu, TraceX için varsayılan seçenektir. _ *_All on_** seçeneği tüm durum çizgilerinin (Ready ve askıya alma) görüntülenmesini mümkün hale gelir.

Son olarak, ***tümü kapalı*** seçeneği tüm durum çizgilerinin görüntülenmesini devre dışı bırakır.

## <a name="event-information-display"></a>Olay bilgileri görünümü

TraceX; ThreadX, FileX, NetX, NetX Duo ve USBX API çağrıları ve iç olaylar dahil bazı 600 çalışma zamanı olayları hakkında ayrıntılı bilgi sağlar. TraceX Ayrıca, ek 61.439 benzersiz kullanıcı tanımlı olayları destekler.

Sıralı veya zaman görüntüleme modunun seçili olmasından bağımsız olarak, görüntüleme alanındaki herhangi bir olay üzerinde bir fare, olayın yakınında ayrıntılı olay bilgilerinin görüntülenmesine neden olur. Demo ***demo_threadx. trx** _ izleme dosyasındaki 143 olayı üzerindeki fare, _ * şekil 15 * * içinde gösteriliyor:

![Örnek bir izleme dosyasında olay 143 ' nin üzerine farede ekran görüntüsü](./media/user-guide/screen_shot_37.png)

**ŞEKIL 15**

Her olay, ***Context** _ ve _*_göreli saat_*_ ve _*_zaman damgası_*_ hakkında standart bilgiler içerir. Bağlam alanı, olayın gerçekleştiği bağlamı gösterir. Yalnızca dört bağlam vardır: iş parçacığı, boşta, ıSR ve başlatma. Bir iş parçacığı bağlamında bir olay gerçekleştiğinde, iş parçacığı adı ve o zaman önceliği yukarıda gösterildiği gibi toplanır ve görüntülenir. _*_Göreli süre_*_ , izlemenin başından itibaren Zamanlayıcı onay işaretleri sayısını gösterir. _ *_RAW zaman damgası_** olayın ham saat kaynağını görüntüler. Son olarak, olaya özgü tüm bilgiler görüntülenir. Bu bilgiler, bu bölümün geri kalanında ayrıntılı olarak açıklanmıştır.

Ayrıntılı olay bilgileri herhangi bir olaya çift tıklanarak da kullanılabilir. Olay 143 ' ye çift tıklamak **Şekil 16**' da gösterilmiştir:

![Bir olaya çift tıklandığında ayrıntılı olay bilgilerinin ekran görüntüsü.](./media/user-guide/screen_shot_38.png)

**ŞEKIL 16**

Aynı anda birden çok olayı görüntüleyebilmekte, kullanıcıya ne olduğunu daha zengin bir görünüm sağlar. Çok sayıda olay birbiriyle ilişkili olduğundan, bunları yan yana görmek oldukça yararlı olur. Bu, birden çok olaya çift tıklanılarak gerçekleştirilir.

## <a name="current-event-display"></a>Geçerli olay görüntüsü

TraceX, geçerli olayı, Kullanıcı tarafından ***View-> geçerli olay*** aracılığıyla veya araç çubuğundaki geçerli olay düğmesine tıklayarak, ayrı bir pencerede görüntüler. Seçili olduktan sonra, TraceX Şu anda seçili olan olayı tek başına pencerede görüntüler ve başka bir olay seçildiğinde bu pencereyi yeniler.

## <a name="event-searching"></a>Olay arama

TraceX, kapsamlı bir olay arama yeteneği sağlar. Her olayın olay KIMLIĞI ve bilgi alanları, birincil arama parametreleridir. Bir arama parametresi için bir değer belirtilmemeksizin, parametrenin bu parametreyi aramadan etkin bir şekilde kaldırdığını gösterir. Ayrıca, arama işlemi, bulunan herhangi bir parametre aramayı karşılayacaktır veya aramayı karşılamak için tüm parametrelerin bulunması gerekir. Arama Ayrıca belirli bir bağlamla kısıtlanabilir veya izlemenin tüm bağlamlarını kapsar. Olay aramasını çağırmak, * şekil 17 * * ' de gösterildiği gibi, araç çubuğundaki ***değere göre ara** _ düğmesi seçilerek yapılır _. Seçildiğinde, arama için tüm parametreleri belirten arama iletişim kutusu görüntülenir. Arama iletişim kutusundaki **_İleri_*_ ve _*_önceki_*_ düğmeler, belirtilen arama ölçütleriyle eşleşen sonraki ve önceki olayları bulmak için kullanılabilir. _ *Şekil 17** arama iletişim kutusunu gösterir.

![Olay aramasının ekran görüntüsü.](./media/user-guide/screen_shot_39.png)

**ŞEKIL 17**

![Arama iletişim kutusunun ekran görüntüsü.](./media/user-guide/screen_shot_40.png)

**ŞEKIL 18**

## <a name="zooming-in-and-out"></a>Yakınlaştırma ve uzaklaştırma

Varsayılan olarak, TraceX olayları tam boyutunda görüntüler. İstediğiniz gibi yakınlaştırabilir veya yakınlaştırabilirsiniz. İzleme, izlemede yakalanan genel olayları görmek için yararlıdır, ancak yakınlaştırma, zaman damgası kaynağının çözümlenmesi nedeniyle olayların çakıştığı koşullarda yararlı olur. **Şekil 19** , izleme dosyasının %100 ' ının gösterilmesi için **_demo_threadx. trx_** dosyasını uzaklaştırdığını gösterir.

![Örnek bir dosyanın ekran görüntüsü, izleme dosyasının %100 ' i gösteriliyor.](./media/user-guide/screen_shot_41.png)

**ŞEKIL 19**

Geçerli görüntü sayfasındaki tüm izlemeyi göstermek için %100 oranında yakınlaştırıldığında, izlemede yakalanan tüm bağlam yürütmesinin yanı sıra bu bağlamlarda gerçekleşen genel olayları görmek kolaydır. **Şekil 16** ' da, **_iş parçacığı 1_*_ ve _*_iş parçacığı 2_** ' nin en sık yürütülecektir. Olayları için mavi renklendirme, bu iş parçacıklarının sıra hizmeti çağrıları (kuyruk olayları renkli olarak mavi) yapmasını da önerir.

Tam bir simge görünümüne geri yükleme işlemi eşit derecede kolaydır; Yakınlaştır düğmesi tekrar tekrar seçilebilir veya bazı 100 faktörü girilmiş olabilir.

## <a name="delta-ticks-between-events"></a>Olaylar arasındaki Delta Işaretleri

Trackingex içindeki çeşitli olaylar arasındaki onay işareti sayısını belirlemek kolaydır. başlangıç olayına tıklayın ve fareyi bitiş olayına sürükleyin. **Şekil 17**' de gösterildiği gibi, olaylar arasındaki işaret değişim sayısı, ekranın sağ üst köşesinde görüntülenir.

![Olaylar arasındaki Delta sayısının ekran görüntüsü.](./media/user-guide/screen_shot_42.png)

**ŞEKIL 17**

**Şekil 17** ' de gösterilen Delta işaretleri, 5032 olay 125 ve olay 154 arasında onay işareti geçtiğini gösterir. Bu, her bir olaydaki göreli zaman damgalarına bakarak ve çıkararak el ile de hesaplanabilir, ancak GUI kullanımı kolay ve anında gerçekleşir.

## <a name="actual-time-display"></a>Gerçek zamanlı görüntüleme

Etkin olduğunda, TraceX gerçek süreyi * zaman görünümü _ ' de ve TraceX tarafından görüntülenen çeşitli Delta zaman bilgileri için bir süre sonra, ***saat görünümünde** gösterir. Varsayılan olarak, gerçek zamanlı görüntüleme devre dışıdır. Gerçek zamanlı görüntülemeyi etkinleştirmek için, mikro saniye başına düşen onay işareti sayısının, mikro saniye * menü seçimi *_başına _ seçenekler-> ticks_* ile girilmesi gerekir (girilecek değer, hedefte tracex olay günlüğü için kullanılan donanım Zamanlayıcı kaynağı tarafından belirlenir).

## <a name="priority-inversions"></a>Öncelikli Inversions 'ları

Trackingex, izleme dosyasında algılanan öncelik sürümlerini otomatik olarak görüntüler. Öncelikli Inversions, daha yüksek öncelikli bir iş parçacığının daha düşük öncelikli bir iş parçacığına ait olan bir mutex elde edilmeye çalıştığı durumlar olarak tanımlanır. Bu durum, sistem bu şekilde çalışacak şekilde ayarlandığından *belirleyici* olarak belirlenir. Trackingex, kullanıcıyı bilgilendirmek için, hafif *öncelikli sürüm* aralıklarını açık somon rengi olarak gösterir.

TraceX, *belirleyici olmayan* öncelikli Inversions 'ları de görüntüler. Bu öncelikli sürümler, farklı bir öncelik düzeyi olan başka bir iş parçacığının, *belirleyici* olmayan bir öncelik sürümünün ortasında yürütülmesi ve bu sayede öncelikli bir süre *belirleyici olmayan* bir durum olması nedeniyle, farklı bir öncelik düzeyi olan diğer bir iş parçacığının daha fazla *belirleyici öncelikli sürümlerinden* farklıdır. Bu durum genellikle kullanıcı için bilinmemektedir ve çok önemli olabilir. Bu koşulun kullanıcısına uyarı vermek için, tracex, daha parlak bir somon rengi olarak *belirleyici olmayan* öncelikli bir şekilde gösterir. **Şekil 18** ' de hem *belirleyici* hem de *belirleyici olmayan* öncelikli Inversions gösterilmektedir.

![Bir izleme dosyasındaki öncelik Inversion ekran görüntüsü.](./media/user-guide/screen_shot_43.png)

**ŞEKIL 18**

**Şekil 18** ' den Event 402 aracılığıyla olay 398 ' den *belirleyici* bir öncelik sürümü gösterilmektedir. Bu aralıkta, daha yüksek öncelikli ***iş parçacığı 0** _, daha düşük öncelikli _*_iş parçacığı 1_*_' in sahip olduğu bir mutex üzerinde engeller. Olayda 402, _ *_thread 1_** mutex 'i serbest bırakır ve bu nedenle öncelikli Inversion 'ı sonlandırır.

Daha parlak gölgeli alan, Event 420 aracılığıyla olay 408 arasında *belirleyici olmayan* bir öncelik gösterir. Bu *belirleyici olmayan* bir deyişle, ***iş parçacığı 1** _, daha yüksek öncelikli _*_iş parçacığı 0_*_ ' ın engellediği mutex 'i tutarken _ *_iş parçacığı 2_* * ' ı devam eden bir kesme meydana geldi ve bu da sistemin öncelikli olmayan süresini yürütür ve uzatır. Bu durum oldukça ciddi ve tanımlanmaları zor olabilir; Ancak, TraceX ile kolayca tanımlanmıştır.
