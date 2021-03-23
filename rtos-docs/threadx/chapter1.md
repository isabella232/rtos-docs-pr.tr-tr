---
title: Bölüm 1-Azure RTOS ThreadX 'e giriş
description: Bu bölümde, Azure RTOS ThreadX 'e giriş ve uygulamalarının ve avantajlarından ilgili bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 83718ddf5469238e2429855908be2ea5d405f874
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826579"
---
# <a name="chapter-1---introduction-to-azure-rtos-threadx"></a>Bölüm 1-Azure RTOS ThreadX 'e giriş

Azure RTOS ThreadX, özellikle eklenmiş uygulamalar için tasarlanan yüksek performanslı bir gerçek zamanlı çekirlüdür. Bu bölümde, ürüne giriş ve uygulamaların ve avantajlarının açıklaması yer almaktadır.

## <a name="threadx-unique-features"></a>ThreadX benzersiz özellikleri

Diğer gerçek zamanlı kernels uygulamalarından farklı olarak, ThreadX, güçlü CIC, RıSC ve DSP işlemcileri kullanan küçük mikro denetleyici tabanlı uygulamalar arasında kolayca ölçeklendirip çok yönlü olacak şekilde tasarlanmıştır.

ThreadX, temel mimarisine göre ölçeklenebilir. ThreadX Hizmetleri bir C Kitaplığı olarak uygulandığından, yalnızca uygulama tarafından kullanılan hizmetler çalışma zamanı görüntüsüne getirilir. Bu nedenle, ThreadX gerçek boyutu uygulama tarafından tamamen belirlenir. Çoğu uygulama için, ThreadX yönerge görüntüsü, boyutu 2 Kbayt ile 15 kilobayt arasında değişir.

### <a name="picokerneltrade-architecture"></a>*picokernel &trade; mimarisi*

Kernel işlevlerini geleneksel *mikro çekirdek* mimarileri gibi birbirlerine göre katmanlama yerine, threadx Hizmetleri doğrudan kendi çekirdeğine takılır. Bu, en hızlı olası bağlam değiştirme ve hizmet çağrısı performansına neden olur. Bu katmansız tasarımı bir *picokernel* mimarisi olarak çağırıyoruz.

### <a name="ansi-c-source-code"></a>ANSI C kaynak kodu

ThreadX, birincil olarak ANSI C 'de yazılmıştır. Çekirdeği temeldeki hedef işlemciye uyarlamak için küçük miktarda derleme dili gerekir. Bu tasarım, ThreadX 'in (genellikle hafta içinde) çok kısa bir süre içinde yeni bir işlemci ailesine bağlantı noktası kullanmasını mümkün kılar.

### <a name="advanced-technology"></a>Gelişmiş teknoloji

Aşağıda, ThreadX gelişmiş teknolojisinin önemli noktaları verilmiştir.
- Basit *picokernel* mimarisi
- Otomatik ölçeklendirme (küçük ayak izi)
- Belirleyici işleme
- Hızlı gerçek zamanlı performans
- PreEmptive ve işbirlikçi zamanlaması
- Esnek iş parçacığı önceliği desteği
- Dinamik sistem nesnesi oluşturma
- Sınırsız sayıda sistem nesnesi
- İyileştirilmiş kesme işleme
- Önalım-eşik&trade;
- Öncelikli devralma
- Olay zincirleme&trade;
- Hızlı yazılım zamanlayıcılarını
- Çalışma zamanı bellek yönetimi
- Çalışma zamanı performans izleme
- Çalışma zamanı yığın Analizi
- Yerleşik sistem izleme
- Büyük işlemci desteği
- Büyük geliştirme aracı desteği
- Tamamen endian nötr

### <a name="not-a-black-box"></a>Siyah kutu değil

ThreadX dağıtımları, tam C kaynak kodunu ve işlemciye özgü derleme dilini içerir. Bu, çok sayıda ticari kerels ile oluşan "kara kutu" sorunlarını ortadan kaldırır. ThreadX ile uygulama geliştiricileri, tam olarak çekirdeğin ne yaptığını görebilir; herhangi bir gizleyebilmektir!

Kaynak kodu uygulamaya özgü değişikliklere de olanak tanır. Önerilmese de, kesinlikle gerekliyse çekirdeği değiştirme imkanına kesinlikle yarar vardır.

Bu özellikler özellikle, kendi *Şirket içi çekirdekleri* ile çalışmaya alışkın olan geliştiricilere Comforting. Kaynak kodu ve çekirdeği değiştirme yeteneğinin olmasını bekler. ThreadX, bu tür geliştiriciler için en son çekirdedir.

### <a name="the-rtos-standard"></a>RTOS standart

Çok yönlülük, yüksek performanslı *picokernel* mimarisi, gelişmiş teknoloji ve gösterilen taşınabilirlik nedeniyle, threadx bugün 2.000.000.000 ' den fazla cihazda dağıtılır. Bu, derin eklenmiş uygulamalar için ThreadX 'i RTOS standardını etkin hale getirir.

## <a name="safety-certifications"></a>Güvenlik sertifikaları

### <a name="tv-certification"></a>TÜV Sertifikası

ThreadX, SGS-TÜV Saar tarafından, IEC61508 ve ıEC-62304 ' e göre güvenlik açısından kritik sistemlerde kullanılmak üzere sertifikalandırilmiştir. Sertifika, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için Uluslararası Elektroteknik Komisyonu (ıEC) 61508 ve ıEC 62304 ' nin en yüksek güvenlik bütünlüğü düzeylerine yönelik güvenlik ile ilgili yazılımların geliştirilmesi için, ThreadX 'in kullanılabilir olduğunu onaylar. Almanya 'nun sgsgroup ve TÜV Saarland 'ın bir Joint girişim aracılığıyla oluşturulan SGS-TÜV Saar, dünya çapındaki güvenlikle ilgili sistemler için katıştırılmış yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacak, bağımsız şirket haline geldi. Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, 62304 IEC, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin ve demiryolu denetim sistemlerinin işlevsel güvenliğini güvence altına almak için kullanılır.

SGS-TÜV Saar, ISO 26262 standardına göre güvenlik açısından kritik bir oto dili sisteminde kullanılmak üzere sertifikalı ThreadX 'e sahiptir. Ayrıca, ThreadX, en yüksek ISO 26262 sertifikası düzeyini temsil eden, g/v güvenlik bütünlüğü düzeyi (asıl) D 'ye sertifikalı değildir.

Ayrıca, SGS-TÜV Saar, güvenlik açısından kritik demiryolu uygulamalarında kullanılmak üzere sertifikalı threadx 'e sahiptir ve en fazla 50128 standart, en fazla ' a kadar.

![TÜV Sertifikası](./media/overview-threadx/partener-logo-sgs-tuv-saar-2.png)

* IEC 61508, SIL 4 ' e kadar

* IEC 62304 en fazla SW güvenlik sınıfı C

* ISO 26262 ASIL D

* EN 50128 SW-SıL 4

> [!NOTE]
> *Tüm ThreadX sürümleri için TÜV veya test raporlarının, sertifikaların ve ilişkili belgelerin kullanılabilirliği hakkında daha fazla bilgi için lütfen bizimle iletişime geçin.*

### <a name="misra-c-compliant"></a>MISRA C uyumlu

MISRA C, C programlama dilini kullanan kritik sistemler için bir programlama yönergeleri kümesidir. Özgün MISRA C yönergeleri öncelikli olarak, ilk olarak bir oto ve uygulamaları hedeflenmiştir; Ancak, MISRA C artık tüm güvenlik açısından kritik uygulamalar için geçerli olduğu kadar büyük ölçüde tanınır. ThreadX, MISRA-C:2004 ve MISRA c:2012'nin tüm "zorunlu" ve "zorunlu" kuralları ile uyumludur. ThreadX, üç "Danışmanlık" kurallarıyla da uyumludur. Daha fazla ayrıntı için ***ThreadX_MISRA_Compliance.pdf*** belgesine bakın.

### <a name="ul-certification"></a>UL sertifikası

Bkz. ThreadX, UL 60730-1 Ek H, CSA E60730-1 Ek H, ıEC 60730-1 Ek H, UL 60335-1 ek R, ıEC 60335-1 ek R 1998 ve programlanabilir. Ek H 'de "yazılım kullanan denetimler" için gereksinimleri olan ıEC/UL 60730-1 ile birlikte ıEC 60335-1 standardı, ek R. ıEC 60730 ek H ve ıEC 60335-1 ek R içindeki "programlanabilir elektronik devreler" için gereksinimleri açıklar. Örneğin, yıkama makineleri, dishörler, kurutma, kurutıcılar, freezers ve ovens gibi gereçlerde kullanılan MCU donanım ve yazılımlarının güvenliğini ele.

![UL sertifikası](./media/overview-threadx/partener-logo-c-ru-us-2.png)

*UL/ıEC 60730, UL/ıEC 60335, UL 1998*

> [!NOTE]
> *Hangi ThreadX sürümleri TÜV veya test raporlarının, sertifikaların ve ilişkili belgelerin kullanılabilirliği hakkında daha fazla bilgi için lütfen Microsoft 'a başvurun.*

### <a name="certification-pack"></a>Sertifika paketi

ThreadX sertifika paketi, &trade; threadx tabanlı ürünü, güvenlik açısından kritik meydan, tıp ve endüstriyel sistemler için gereken en yüksek güvenilirlik ve önem düzeyi düzeylerine göre onaylamak veya başarıyla göndermek için gereken tüm threadx kanıtını sağlayan, sektöre özgü, tek başına 100 bir pakettir. Desteklenen sertifika sertifikaları şunlardır-178B, ED-12B, DO-278, FDA510 (k), IEC62304, ıEC-60601, ISO-14971, UL-1998, ıEC-61508, CENELEC EN50128, BS50128 ve 49CFR236. Sertifika paketi hakkında daha fazla bilgi için lütfen Microsoft 'a başvurun.

## <a name="embedded-applications"></a>Katıştırılmış uygulamalar

Katıştırılmış uygulamalar, kablosuz iletişim cihazları, Otomobil motorları, lazer yazıcılar, tıbbi cihazlar vb. gibi ürünlerde bulunan mikro işlemcilerde yürütülür. Katıştırılmış uygulamaların başka bir şekilde ayrımı, yazılım ve donanımının özel bir amaca sahip olması olabilir.

### <a name="real-time-software"></a>Gerçek zamanlı yazılım

Uygulama yazılımına zaman kısıtlamaları eklendiğinde, *gerçek* zamanlı yazılım olarak adlandırılır. Gömülü uygulamalar, dış olaylarla kendi kendine ait etkileşimlerinden dolayı neredeyse her zaman gerçek zamanlı olarak gerçekleştirilir.

### <a name="multitasking"></a>Çok görevli

Belirtildiği gibi, katıştırılmış uygulamaların adanmış bir amacı vardır. Bu amacı karşılamak için, yazılımın çeşitli *Görevler* gerçekleştirmesi gerekir. Görev, uygulamanın belirli bir vergileri yürüten yarı bir bağımsız bölümüdür. Ayrıca, bazı görevlerin diğerlerinden daha önemli olması da mümkündür. Katıştırılmış bir uygulamadaki önemli zorluklardaki bir tane, işlemcinin çeşitli uygulama görevleri arasında ayrılması. Rekabet görevleri arasında bu işleme ayırma, ThreadX 'in birincil amacıdır.

### <a name="tasks-vs-threads"></a>Görevler ve Iş parçacıkları

Görevlerle ilgili başka bir ayrım, *görev* teriminin çok çeşitli yollarla kullanılmalarıdır. Bazen ayrı olarak yüklenebilir bir program anlamına gelir. Diğer örneklerde, bir iç program segmentine başvurabilir. Bu nedenle, çağdaş işletim sistemlerinde görev kullanımını daha fazla veya daha az olan iki terim vardır: *işlem* ve *iş parçacığı*. *İşlem* , kendi adres alanına sahip tamamen bağımsız bir programdır, *iş parçacığı* bir işlem içinde yürüten yarı bağımsız bir program segmentleridir. İş parçacıkları aynı işlem adres alanını paylaşır. İş parçacığı yönetimiyle ilişkili ek yük düşüktür.

Çoğu gömülü uygulama, tam bir işlem odaklı işletim sistemiyle ilişkili ek yükü (hem bellek hem de performans) alamaz. Ayrıca, daha küçük mikro işlemciler, doğru bir işlem odaklı işletim sistemini desteklemeye yönelik donanım mimarisine sahip değildir. Bu nedenlerden dolayı, ThreadX gerçek zamanlı gömülü uygulamaların çoğu için son derece etkili ve pratik olan bir iş parçacığı modeli uygular.

Karışıklık olmaması için ThreadX, *görevini* kullanmaz. Bunun yerine, daha açıklayıcı ve çağdaş ad *iş parçacığı* kullanılır.

## <a name="threadx-benefits"></a>ThreadX avantajları

ThreadX kullanmak, gömülü uygulamalara birçok avantaj sağlar. Tabii ki, birincil avantaj, gömülü uygulama iş parçacıklarının işleme zamanına nasıl ayrıldığı üzerine oturacaktır.

### <a name="improved-responsiveness"></a>İyileştirilmiş yanıt hızı

ThreadX gibi gerçek zamanlı çekirdekler öncesinde, genellikle C *Main* işlevinin içinden bir basit denetim döngüsüyle, en çok eklenmiş uygulamalar işlem süresi ayırmıştır. Bu yaklaşım, çok küçük veya basit uygulamalarda kullanılmaya devam etmektedir. Öte yandan, büyük veya karmaşık uygulamalarda, herhangi bir olaya yanıt süresi, denetim döngüsü boyunca bir geçiş işleminin en kötü durum işleme süresinin bir işlevi olduğundan pratik değildir. 

Önemli hale getirmek, denetim döngüsünde değişiklik yapıldığında uygulamanın zamanlama özellikleri değişir. Bu, uygulamayı doğal olarak kararsız hale getirir ve üzerinde bakım ve iyileştirilmesine olanak sağlar.

ThreadX önemli dış olaylara hızlı ve belirleyici yanıt süreleri sağlar. ThreadX bunu, daha yüksek öncelikli bir iş parçacığının yürütülen düşük öncelikli iş parçacığını sağlamasına izin veren preemptive, öncelik tabanlı zamanlama algoritması aracılığıyla gerçekleştirir. Sonuç olarak, en kötü durum yanıt süresi bir bağlam anahtarı gerçekleştirmek için gereken zamana yaklaşır. Bu yalnızca belirleyici değildir, ancak son derece hızlıdır.

### <a name="software-maintenance"></a>Yazılım Bakımı

ThreadX çekirdeği, uygulama geliştiricilerinin uygulamanın diğer alanlarının zamanlamasını değiştirme konusunda endişelenmenize gerek kalmadan uygulama iş parçacıklarının belirli gereksinimlerine odaklanmasını sağlar. Bu özellik ayrıca ThreadX kullanan bir uygulamayı onarmayı veya geliştirmeyi çok daha kolay hale getiriyor.

### <a name="increased-throughput"></a>Artan verimlilik

Denetim döngüsü yanıt süresi sorununa yönelik olası bir iş, daha fazla yoklama eklemektir. Bu işlem, yanıt verme süresini iyileştirir, ancak yine de sabit bir en kötü durum yanıt süresi garantisi vermez ve uygulamanın gelecekteki bir şekilde değiştirilmesini artırmaya hiçbir şey yapmaz. Ayrıca, işlemci artık fazladan yoklama nedeniyle daha gereksiz işlemler gerçekleştiriyor. Bu gereksiz işlemenin hepsi sistemin genel verimini azaltır.

Ek yükün ilgi çekici bir noktası, birçok geliştiricinin ThreadX gibi çok iş parçacıklı ortamların yük yükünü artırdığı ve toplam sistem verimlilik üzerinde olumsuz bir etkiye sahip olduğunu varsaymaktadır. Ancak bazı durumlarda, çoklu iş parçacığı denetim döngüsü ortamlarında oluşan tüm gereksiz yoklamayı ortadan kaldırarak yükü azaltır. Çok iş parçacıklı çekirdekler ile ilişkili ek yük, genellikle bağlam değiştirme için gereken sürenin bir işlevidir. Bağlam anahtarı süresi yoklama sürecinden küçükse ThreadX, daha az ek yük ve daha fazla verimlilik sağlayan bir çözüm sağlar. Bu, ThreadX ' i herhangi bir karmaşıklık veya boyut gerektiren uygulamalar için belirgin bir seçenek haline getirir.

### <a name="processor-isolation"></a>İşlemci yalıtımı

ThreadX, uygulama ile temel alınan işlemci arasında sağlam bir işlemcinin bağımsız arabirimi sağlar. Bu, geliştiricilerin önemli miktarda zaman öğrenme donanım ayrıntıları harcamasını yerine uygulamaya odaklanmasını sağlar.

### <a name="dividing-the-application"></a>Uygulamayı bölme

Denetim döngüsü tabanlı uygulamalarda, her geliştiricinin tüm uygulamanın çalışma zamanı davranışı ve gereksinimleri hakkında bir intimate bilgisine sahip olması gerekir. Bunun nedeni, işlemci ayırma mantığının tüm uygulama genelinde yayılmasının nedeni. Bir uygulamanın boyutu veya karmaşıklığı arttıkça, tüm geliştiricilerin uygulamanın tamamına yönelik kesin işleme gereksinimlerini anımsamasını imkansız hale gelir.

ThreadX, her geliştiriciyi işlemci ayırması ile ilişkili olan worrıes 'nin serbest bırakır ve ekli uygulamanın belirli parçaları üzerinde yoğunlaşmasını sağlar. Ayrıca, ThreadX, uygulamayı açıkça tanımlanmış iş parçacığına bölünmeye zorlar. Tek başına, uygulamanın iş parçacıkları için bu bölümü geliştirmeyi çok daha kolay hale getirir.

### <a name="ease-of-use"></a>Kullanım kolaylığı

ThreadX, uygulama geliştiricisi göz önünde bulundurularak tasarlanmıştır. ThreadX mimarisi ve hizmet çağrısı arabirimi kolayca anlaşılması için tasarlanmıştır. Sonuç olarak, ThreadX geliştiricileri gelişmiş özelliklerini hızlı bir şekilde kullanabilir.

### <a name="improve-time-to-market"></a>Pazarlamaya ulaşma süresini geliştirme

ThreadX 'in tüm avantajları yazılım geliştirme sürecini hızlandırır. ThreadX, çoğu işlemci sorununu ve en sık karşılaşılan güvenlik sertifikalarını ve bu çabayı geliştirme zamanlamalarından kaldırır. Tüm bu, pazara daha hızlı bir zaman sağlar!

### <a name="protecting-the-software-investment"></a>Yazılım yatırımınızı koruma

Mimarinin mimarisi nedeniyle, ThreadX yeni işlemci ve/veya geliştirme aracı ortamlarına kolayca gönderilir. Bu, ThreadX 'in uygulamaları temeldeki işlemcilerin ayrıntılarından yalıtılmış hale getiren olgusuna bağlı olarak, ThreadX uygulamalarının yüksek oranda taşınabilir olmasını sağlar. Sonuç olarak, uygulamanın geçiş yolu garanti edilir ve orijinal geliştirme yatırımı korunur.
