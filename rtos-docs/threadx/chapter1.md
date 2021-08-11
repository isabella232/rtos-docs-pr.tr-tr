---
title: Bölüm 1 - Azure RTOS ThreadX'e Giriş
description: Bu bölümde, Azure RTOS ThreadX'e giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 536b2d59bf9f2cf15d320b91277f0efc7bf96097329f690b0849b2145c5a3abc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802076"
---
# <a name="chapter-1---introduction-to-azure-rtos-threadx"></a>Bölüm 1 - Azure RTOS ThreadX'e Giriş

Azure RTOS ThreadX, özellikle katıştırılmış uygulamalar için tasarlanmış yüksek performanslı bir gerçek zamanlı çekirdektir. Bu bölümde ürüne giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır.

## <a name="threadx-unique-features"></a>ThreadX Benzersiz Özellikleri

Diğer gerçek zamanlı çekirdeklerin aksine ThreadX, güçlü CISC, RISC ve DSP işlemcileri kullananlar aracılığıyla küçük mikrodenetleyici tabanlı uygulamalar arasında kolayca ölçeklendirme yapmak için çok yönlü olacak şekilde tasarlanmıştır.

ThreadX, temel alınan mimarisine göre ölçeklenebilir. ThreadX hizmetleri bir C kitaplığı olarak uygulana olduğundan, yalnızca uygulama tarafından kullanılan hizmetler çalışma zamanı görüntüsüne getiri. Bu nedenle, ThreadX'in gerçek boyutu uygulama tarafından tamamen belirlenir. Çoğu uygulama için ThreadX'in yönerge görüntüsü 2 KBayt ile 15 KBayt arasında bir boyuta sahiptir.

### <a name="picokerneltrade-architecture"></a>*picokernel &trade; Mimarisi*

ThreadX hizmetleri, geleneksel mikro kanal mimarileri gibi çekirdek işlevlerini birbirinin üzerine katmanlama yerine doğrudan çekirdeğine taktırır.  Bu, mümkün olan en hızlı bağlam değiştirme ve hizmet çağrısı performansıyla sonuç verir. Bu katman olmayan tasarıma *picokernel mimarisi çağrılır.*

### <a name="ansi-c-source-code"></a>ANSI C Kaynak Kodu

ThreadX öncelikli olarak ANSI C'de yazılır. Çekirdeği temel alınan hedef işlemciye uyarlamak için az miktarda derleme dili gerekir. Bu tasarım, ThreadX'i yeni bir işlemci ailesine çok kısa bir sürede (genellikle haftalar içinde) bağlantı noktası olarak mümkün yapar!

### <a name="advanced-technology"></a>Gelişmiş Teknoloji

Aşağıda, ThreadX gelişmiş teknolojisinin öne çıkan özellikleri yer almaktadır.
- Basit *picokernel* mimarisi
- Otomatik ölçeklendirme (küçük ayak izi)
- Belirlenmci işleme
- Hızlı gerçek zamanlı performans
- Preemptive ve işbirliğine açık zamanlama
- Esnek iş parçacığı öncelik desteği
- Dinamik sistem nesnesi oluşturma
- Sınırsız sayıda sistem nesnesi
- İyileştirilmiş kesme işleme
- Önmzeyde-eşik&trade;
- Öncelik devralma
- Olay zinciri&trade;
- Hızlı yazılım süreçerleri
- Çalışma zamanı bellek yönetimi
- Çalışma zamanı performans izleme
- Çalışma zamanı yığın analizi
- Yerleşik sistem izlemesi
- Geniş işlemci desteği
- Geniş geliştirme aracı desteği
- Tamamen endian nötr

### <a name="not-a-black-box"></a>Kara Kutu Değil

ThreadX'in çoğu dağıtımı, tam C kaynak kodunun yanı sıra işlemciye özgü derleme dilini içerir. Bu, birçok ticari çekirdekte oluşan "kara kutu" sorunlarını ortadan kaldırıyor. ThreadX ile uygulama geliştiricileri çekirdeğin tam olarak ne yaptığını görebilir; hiçbir şey olmaz!

Kaynak kod uygulamaya özgü değişikliklere de izin verir. Önerilmez, ancak kesinlikle gerekli ise çekirdeği değiştirme becerisine sahip olmak kesinlikle yararlıdır.

Bu özellikler özellikle kendi kendi çekirdekleriyle çalışmaya alışkın olan *geliştiricileri rahatlatıyor.* Kaynak koduna ve çekirdeği değiştirme özelliğine sahip olmasını beklerler. ThreadX, bu tür geliştiriciler için nihai çekirdektir.

### <a name="the-rtos-standard"></a>The RTOS Standard

Çok yönlülüğü, yüksek performanslı *picokernel* mimarisi, gelişmiş teknolojisi ve taşınabilirliği gösterdiğinden ThreadX bugün iki milyardan fazla cihaza dağıtılmıştır. Bu, ThreadX'i derinden eklenmiş uygulamalar için RTOS standardı yapar.

## <a name="safety-certifications"></a>Güvenlik Sertifikaları

### <a name="tv-certification"></a>TÜV Sertifikası

ThreadX, IEC61508 ve IEC-62304'e göre, güvenlik açısından kritik sistemlerde kullanım için VELA-TÜV Saar tarafından onaylandı. Sertifikasyon, ThreadX'in "Elektrik, elektronik ve programlanabilir elektronik güvenlikle ilgili sistemlerin İşlevsel Güvenliği" için Uluslararası Elektroteknik Komisyonu (IEC) 61508 ve IEC 62304'te en yüksek güvenlik bütünlüğü düzeyleri için güvenlikle ilgili yazılımların geliştirilmesinde kullanılab olduğunu onaylar. Almanya'nınGROUPgroup ve TÜV Saarland'ın ortak girişimiyle oluşturulan VEPÜS-TÜV Saar, dünya çapında güvenlikle ilgili sistemler için ekli yazılımları test etme, denetleme, doğrulama ve onaylama konusunda yetkilendirilmiş, bağımsız lider şirket haline geldi. Endüstriyel güvenlik standardı IEC 61508 ve IEC 62304 dahil olmak üzere bundan türetilen tüm standartlar elektrik, elektronik ve programlanabilir elektronik güvenlikle ilgili tıbbi cihazlar, süreç denetim sistemleri, endüstriyel makineler ve demir yolu kontrol sistemlerinin işlevsel güvenliğini sağlamak için kullanılır.

WINDOWS-TÜV Saar, ISO 26262 standardına göre güvenlik açısından kritik otomobil sistemlerinde kullanılacak ThreadX sertifikasına sahiptir. Ayrıca ThreadX, en yüksek ISO 26262 sertifika düzeyini temsil eden Otomotiv Güvenlik Bütünlüğü Düzeyi (VERIM) D sertifikasına da sahiptir.

Buna ek olarak, SAFETY-TÜV Saar, güvenliği kritik demir yolu uygulamalarında kullanılacak ve SW-SIL 4'e kadar EN 50128 standardına uygun olacak şekilde threadX sertifikasına sahiptir.

![TÜV Sertifikası](./media/overview-threadx/partener-logo-sgs-tuv-saar-2.png)

* SIL 4'e kadar IEC 61508

* SW güvenliği Sınıfı C'ye kadar IEC 62304

* ISO 26262İİSNA D

* EN 50128 SW-SIL 4

> [!NOTE]
> *ThreadX'in hangi sürümünün TÜV tarafından onaylandı veya test raporları, sertifikalar ve ilişkili belgelerin kullanılabilirliği hakkında daha fazla bilgi için lütfen bizimle iletişime geçin.*

### <a name="misra-c-compliant"></a>MISRA C Uyumlu

MISRA C, C programlama dilini kullanan kritik sistemler için bir dizi programlama kılavuzudur. Özgün MISRA C yönergeleri öncelikli olarak otomotiv uygulamalarına yönelikti; ancak, MISRA C artık güvenlik açısından kritik herhangi bir uygulama için geçerli olduğu yaygın olarak kabul ediliyor. ThreadX, MISRA-C:2004 ve MISRA C:2012'nin tüm "gerekli" ve "zorunlu" kurallarıyla uyumludur. ThreadX ayrıca üç "danışmanlık" kuralıyla da uyumludur. Diğer ayrıntılar için ***ThreadX_MISRA_Compliance.pdf*** belgeye bakın.

### <a name="ul-certification"></a>UL Sertifikası

ThreadX, UL 60730-1 Ek H, CSA E60730-1 Ek H, IEC 60730-1 Ek H, UL 60335-1 Ek R, IEC 60335-1 Ek R ve programlanabilir bileşenlerde yazılım için UL 1998 güvenlik standartları ile uyumluluk için UL tarafından onaylandı. IEC/UL 60730-1 ile birlikte, Ek H'de "Yazılım Kullanan Denetimler" için gereksinimlere sahip olan IEC 60335-1 standardı, Ek R'de "Programlanabilir Elektronik Devreler" için gereksinimleri açıklar. IEC 60730 Ek H ve IEC 60335-1 Ek R; makine, makine, alet, bilgisayar gibi gereçlerde kullanılan MCU donanım ve yazılım güvenliğini ele alır.

![UL Sertifikası](./media/overview-threadx/partener-logo-c-ru-us-2.png)

*UL/IEC 60730, UL/IEC 60335, UL 1998*

> [!NOTE]
> *ThreadX'in hangi sürümünün TÜV tarafından onaylandı veya test raporları, sertifikalar ve ilişkili belgelerin kullanılabilirliği hakkında daha fazla bilgi için lütfen Microsoft'a başvurun.*

### <a name="certification-pack"></a>Sertifika Paketi

ThreadX Sertifika Paketi, ThreadX tabanlı ürünü güvenlik açısından kritik Havacılık, Tıbbi ve Endüstriyel sistemler için gereken en yüksek güvenilirlik ve kritiklik düzeylerine sertifika veya başarıyla göndermek için gereken tüm ThreadX kanıtlarını sağlayan % 100 eksiksiz, anahtar teslim, sektöre özgü, tek başına bir &trade; pakettir. Desteklenen sertifikalar DO-178B, ED-12B, DO-278,CF510(k), IEC62304, IEC-60601, ISO-14971, UL-1998, IEC-61508, CENELEC EN50128, BS50128 ve 49CFR236'dır. Sertifikasyon Paketi hakkında daha fazla bilgi için lütfen Microsoft'a ulaşın.

## <a name="embedded-applications"></a>Katıştırılmış Uygulamalar

Katıştırılmış uygulamalar kablosuz iletişim cihazları, otomobil motorları, lazer yazıcılar, tıbbi cihazlar vb. ürünlerin içinde gömülü mikro işlemciler üzerinde yürütülür. Ekli uygulamaların bir diğer farkı da yazılım ve donanımlarının ayrılmış bir amacının yermasıdır.

### <a name="real-time-software"></a>Gerçek Zamanlı Yazılım

Uygulama yazılımına zaman kısıtlamaları uygulanıyorsa, buna gerçek zamanlı *yazılım denir.* Katıştırılmış uygulamalar, dış olaylarla doğal etkileşimi nedeniyle neredeyse her zaman gerçek zamanlıdır.

### <a name="multitasking"></a>Çok görevli

Daha önce belirtildiği gibi, katıştırılmış uygulamaların ayrılmış bir amacı vardır. Bu amacı yerine getirmek için yazılımın çeşitli görevler gerçekleştirmesi *gerekir.* Görev, uygulamanın belirli bir görevi yerine taşıyan yarı bağımsız bir kısmıdır. Ayrıca bazı görevlerin diğer görevlerden daha önemli olduğu da bir durum vardır. Katıştırılmış uygulamanın başlıca güçlüklerinden biri, çeşitli uygulama görevleri arasında işlemcinin ayırmasıdır. Rakip görevler arasında bu işleme ayırması, ThreadX'in birincil amacıdır.

### <a name="tasks-vs-threads"></a>Görevler ve İş Parçacıkları karşılaştırması

Görevler arasındaki bir diğer fark da görev *teriminin* çeşitli yollarla kullanılmıştır. Bazen ayrı olarak yüklenebilir bir program anlamına gelir. Diğer örneklerde, bir iç program segmentini ifade ediyor olabilir. Bu nedenle, işletim sistemlerinde görev kullanımının yerini daha fazla veya daha az alan iki terim vardır: *işlem ve iş* *parçacığı.* Bir *işlem,* kendi adres alanı olan tamamen bağımsız bir programdır, *iş* parçacığı ise bir işlem içinde yürütülen yarı bağımsız bir program kesimidir. İş parçacıkları aynı işlem adres alanı paylaşır. İş parçacığı yönetimiyle ilişkili ek yük çok azdır.

Çoğu ekli uygulama, tam performanslı işlem odaklı bir işletim sistemiyle ilişkili ek yükü (hem bellek hem de performans) karşılayamaz. Ayrıca, küçük mikro işlemciler gerçek bir işlem odaklı işletim sistemini destekleyecek donanım mimarisine sahip değildir. Bu nedenlerle ThreadX, gerçek zamanlı katıştırılmış uygulamaların çoğu için son derece verimli ve pratik olan bir iş parçacığı modeli uygulamaya almaktadır.

Karışıklığı önlemek için ThreadX görevi terimini *kullanmaz.* Bunun yerine, daha açıklayıcı ve açıklayıcı ad *iş parçacığı* kullanılır.

## <a name="threadx-benefits"></a>ThreadX Avantajları

ThreadX'in kullanımı, katıştırılmış uygulamalara birçok avantaj sağlar. Elbette birincil avantajı, katıştırılmış uygulama iş parçacıklarının işleme süresine nasıl ayrılmış olduğuyla ilgilidir.

### <a name="improved-responsiveness"></a>Geliştirilmiş Yanıt Hızı

ThreadX gibi gerçek zamanlı çekirdeklerden önce, çoğu katıştırılmış uygulama işlem süresine genellikle C ana işlevinden basit bir denetim *döngüsüyle ayrılmıştır.* Bu yaklaşım hala çok küçük veya basit uygulamalarda kullanılır. Ancak büyük veya karmaşık uygulamalarda, herhangi bir etkinliğe yanıt süresi denetim döngüsünde bir geçişin en kötü durum işleme süresine sahip bir işlev olduğundan pratik değildir. 

Daha da kötüsü, denetim döngüsünde değişiklikler yapılan her durumda uygulamanın zamanlama özellikleri değişir. Bu, uygulamanın doğal olarak kararsız ve bakımının ve geliştirmesini zorlaştırarak.

ThreadX, önemli dış olaylara hızlı ve belirleyici yanıt süreleri sağlar. ThreadX bunu, yüksek öncelikli bir iş parçacığının daha düşük öncelikli bir iş parçacığını yürütmesini önlayan, öncelik tabanlı zamanlama algoritması aracılığıyla gerçekleştirmektedir. Sonuç olarak, en kötü durum yanıt süresi bağlam anahtarını gerçekleştirmek için gereken süreye yaklaşıyor. Bu yalnızca belirlenmci değildir, aynı zamanda son derece hızlıdır.

### <a name="software-maintenance"></a>Yazılım Bakımı

ThreadX çekirdeği, uygulama geliştiricilerinin uygulamanın diğer alanlarının zamanlamasını değiştirmek zorunda kalmadan uygulama iş parçacıklarının belirli gereksinimlerine odaklanmalarını sağlar. Bu özellik, ThreadX kullanan bir uygulamayı onarmayı veya geliştirmeyi de çok daha kolay hale getirir.

### <a name="increased-throughput"></a>Artan Aktarım Hızı

Denetim döngüsü yanıt süresi sorununa olası bir çözüm, daha fazla yoklama eklemektir. Bu, yanıt hızını artırsa da sabit bir en kötü durum yanıt süresi garanti etmemektedir ve uygulamanın gelecekteki değişikliklerini geliştirmek için hiçbir şey yapmaz. Ayrıca, fazladan yoklama nedeniyle işlemci artık daha da gereksiz işleme gerçekleştirmektedir. Tüm bu gereksiz işleme, sistemin genel aktarım hızını azaltır.

Ek yükle ilgili ilginç bir nokta, birçok geliştiricinin ThreadX gibi çok iş parçacıklı ortamların ek yükü artırarak toplam sistem aktarım hızı üzerinde olumsuz bir etkisi olduğunu varsaymadır. Ancak bazı durumlarda çoklu iş parçacığı kullanımı, denetim döngüsü ortamlarında oluşan tüm gereksiz yoklamaları ortadan kaldırarak ek yükü azaltır. Çok iş parçacıklı çekirdeklerle ilişkili ek yük genellikle bağlam değiştirme için gereken sürenin bir işlevidir. Bağlam değiştirme süresi yoklama işleminin altında ise ThreadX, daha az ek yük ve daha fazla aktarım hızı potansiyeline sahip bir çözüm sağlar. Bu, ThreadX'i herhangi bir derecede karmaşıklık veya boyuta sahip uygulamalar için belirgin bir seçenek yapar.

### <a name="processor-isolation"></a>İşlemci Yalıtımı

ThreadX, uygulama ve temel işlemci arasında güçlü ve işlemciden bağımsız bir arabirim sağlar. Bu, geliştiricilerin önemli miktarda zaman harcayarak donanım ayrıntılarını öğrenmek yerine uygulamaya odaklanmalarını sağlar.

### <a name="dividing-the-application"></a>Uygulamayı Bölme

Denetim döngüsü tabanlı uygulamalarda, her geliştiricinin tüm uygulamanın çalışma zamanı davranışı ve gereksinimleri hakkında bilgi sahibi olması gerekir. Bunun nedeni, işlemci ayırma mantığının uygulamanın tamamına dağılmış durumdan kaynaklandı. Bir uygulamanın boyutu veya karmaşıklığı arttıkça, tüm geliştiricilerin uygulamanın tamamının hassas işleme gereksinimlerini hatırlaması imkansız hale gelir.

ThreadX, her geliştiriciyi işlemci ayırmayla ilgili endişelerden serbest bırakarak ekli uygulamanın belirli bir parçasına odaklanmalarına olanak sağlar. Ayrıca ThreadX, uygulamayı net bir şekilde tanımlanmış iş parçacıklarına bölünmeye de neden olur. Tek başına, uygulamanın iş parçacıklarına bölünmesi geliştirmeyi çok daha basit hale getirir.

### <a name="ease-of-use"></a>Kullanım Kolaylığı

ThreadX, uygulama geliştiricisi tarafından tasarlanmıştır. ThreadX mimarisi ve hizmet çağrısı arabirimi, kolayca anlaşılacak şekilde tasarlanmıştır. Sonuç olarak, ThreadX geliştiricileri gelişmiş özelliklerini hızlı bir şekilde kullanabilir.

### <a name="improve-time-to-market"></a>Pazara satış sürelerini geliştirme

ThreadX'in tüm avantajları yazılım geliştirme sürecini hızlandırır. ThreadX, çoğu işlemci sorunuyla ve en yaygın güvenlik sertifikalarını ele alır, böylece bu çabayı geliştirme zaman çizelgesinden çıkarır. Bunların hepsi pazara daha hızlı bir şekilde devam ediyor!

### <a name="protecting-the-software-investment"></a>Yazılım Yatırımlarını Koruma

Mimarisi nedeniyle ThreadX, yeni işlemci ve/veya geliştirme aracı ortamlarına kolayca taşınabilir. Bu, ThreadX'in temel işlemcilerin ayrıntılarından uygulamaları dayanıklı bir şekilde bir parçası olarak, ThreadX uygulamalarını yüksek oranda taşınabilir yapar. Sonuç olarak, uygulamanın geçiş yolu garanti olur ve özgün geliştirme yatırımı korunur.
