---
title: Bölüm 1 - Azure RTOS ThreadX SMP'ye Giriş
description: Bu bölümde ürüne giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9b9fb7b08691930abcf57df77fff27e619bb7a554a6235d4e234889b7c80945e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802263"
---
# <a name="chapter-1-introduction-to-azure-rtos-threadx-smp"></a>Bölüm 1: Azure RTOS ThreadX SMP'ye Giriş

Azure RTOS ThreadX SMP, özellikle katıştırılmış uygulamalar için tasarlanmış yüksek performanslı gerçek zamanlı bir SMP çekirdeğidir. Bu bölümde ürüne giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır.

## <a name="threadx-smp-unique-features"></a>ThreadX SMP Benzersiz Özellikleri

ThreadX SMP, ekli uygulamalara Simetrik Çoklu İşleme (SMP) teknolojisi getirir. "HAZıR" olan ThreadX SMP uygulama iş parçacıkları (değişen önceliğe sahiptir) zamanlama sırasında kullanılabilir işlemci çekirdekleri için dinamik olarak ayrılır. Bu, tüm kullanılabilir işlemci çekirdeklerinde uygulama iş parçacığı yürütmesinin otomatik yük dengelemesi de dahil olmak üzere gerçek SMP işleme ile sonuç verir.

Diğer gerçek zamanlı çekirdeklerin aksine ThreadX SMP, güçlü CISC, RISC ve DSP işlemcileri kullananlar aracılığıyla küçük mikro denetleyici tabanlı uygulamalar arasında kolayca ölçeklendirme yapmak için çok yönlü olacak şekilde tasarlanmıştır.

ThreadX SMP, temel alınan mimarisine göre ölçeklenebilir. ThreadX SMP hizmetleri bir C kitaplığı olarak uygulana olduğundan, yalnızca uygulama tarafından kullanılan hizmetler çalışma zamanı görüntüsüne getiri. Bu nedenle, ThreadX SMP'nin gerçek boyutu uygulama tarafından tamamen belirlenir. Çoğu uygulama için ThreadX SMP'nin yönerge görüntüsü 5 KBayt ile 20 KBayt arasında bir boyuta sahiptir.

### <a name="picokernel-architecture"></a>picokernel™ Mimarisi 
ThreadX SMP hizmetleri, çekirdek işlevlerini geleneksel mikro *kanal* mimarileri gibi birbirinin üzerine katmanlama yerine doğrudan çekirdeğine takmaktadır. Bu, mümkün olan en hızlı bağlam değiştirme ve hizmet çağrısı performansıyla sonuç verir. Bu katmanlı olmayan tasarıma *picokernel mimarisi çağrılır.*

### <a name="ansi-c-source-code"></a>ANSI C Kaynak Kodu 
ThreadX SMP öncelikli olarak ANSI C'de yazılır. Çekirdeği temel alınan hedef işlemciye uyarlamak için az miktarda derleme dili gerekir. Bu tasarım, ThreadX SMP'nin yeni bir işlemci ailesine çok kısa bir sürede (genellikle haftalar içinde) bağlantı noktasını mümkün kılan bir tasarımdır!

### <a name="advanced-technology"></a>Gelişmiş Teknoloji 
Aşağıda, ThreadX SMP gelişmiş teknolojisinin öne çıkan özellikleri ve ardından yer almaktadır:

  - Basit *picokernel* mimarisi
  - Otomatik yük dengeleme
  - İş parçacığı başına işlemci dışlama
  - Otomatik ölçeklendirme (küçük ayak izi)
  - Belirlenmci işleme
  - Hızlı gerçek zamanlı performans
  - Preemptive ve işbirliğine açık zamanlama
  - Esnek iş parçacığı öncelik desteği (32-1024)
  - Dinamik sistem nesnesi oluşturma
  - Sınırsız sayıda sistem nesnesi
  - İyileştirilmiş kesme işleme
  - Önk eşik™
  - Öncelik devralma
  - Olay zincirleme™
  - Hızlı yazılım süreçerleri
  - Çalışma zamanı bellek yönetimi
  - Çalışma zamanı performans izleme
  - Çalışma zamanı yığın analizi
  - Yerleşik sistem izlemesi
  - Geniş işlemci desteği
  - Geniş geliştirme aracı desteği
  - Tamamen endian nötr

### <a name="not-a-black-box"></a>Kara Kutu Değil
ThreadX SMP'nin çoğu dağıtımı, tam C kaynak kodunun yanı sıra işlemcilere özel derleme dilini içerir. Bu, birçok ticari çekirdekte oluşan "kara kutu" sorunlarını ortadan kaldırıyor. ThreadX SMP ile uygulama geliştiricileri çekirdeğin tam olarak ne yaptığını görebilir; hiçbir şey olmaz!

Kaynak kod uygulamaya özgü değişikliklere de izin verir. Önerilmez, ancak kesinlikle gerekli ise çekirdeği değiştirme becerisine sahip olmak kesinlikle yararlıdır.

Bu özellikler özellikle kendi çekirdekleriyle çalışmaya alışkın olan geliştiricileri *rahatlatıyor.* Kaynak koduna ve çekirdeği değiştirme özelliğine sahip olmasını beklerler. ThreadX SMP, bu tür geliştiriciler için nihai çekirdektir.

### <a name="the-rtos-standard"></a>The RTOS Standard
ThreadX SMP, çok yönlülüğü, yüksek performanslı *picokernel* mimarisi, gelişmiş teknoloji ve taşınabilirliği gösterdiğinden bugün iki milyardan fazla cihaza dağıtılmıştır. Bu, ThreadX SMP'i derinden eklenmiş uygulamalar için RTOS standardı yapar.

## <a name="safety-certifications"></a>Güvenlik Sertifikaları

### <a name="tv-certification"></a>TÜV Sertifikası  
ThreadX SMP, IEC61508 ve IEC-62304'e göre, güvenlik açısından kritik sistemlerde kullanım için VELA-TÜV Saar tarafından onaylandı. Sertifikasyon, "Elektrik, elektronik ve programlanabilir elektronik güvenlikle ilgili sistemlerin İşlevsel Güvenliği" için Uluslararası Elektroteknik Komisyonu (IEC) 61508 ve IEC 62304'te en yüksek güvenlik bütünlüğü düzeyleri için güvenlikle ilgili yazılımların geliştirilmesinde ThreadX SMP'nin kullanılab olduğunu onaylar. Almanya'nın SGS-Group ve TÜV Saarland ortak girişimiyle oluşturulan VEPÜS-TÜV Saar, dünya çapında güvenlikle ilgili sistemler için ekli yazılımları test etme, denetleme, doğrulama ve onaylama konusunda yetkilendirilmiş, bağımsız lider şirket haline geldi. Endüstriyel güvenlik standardı IEC 61508 ve IEC 62304 dahil olmak üzere bundan türetilen tüm standartlar elektrik, elektronik ve programlanabilir elektronik güvenlikle ilgili tıbbi cihazlar, süreç denetim sistemleri, endüstriyel makineler ve demir yolu kontrol sistemlerinin işlevsel güvenliğini sağlamak için kullanılır.

SAFETY-TÜV Saar, ISO 26262 standardına göre güvenlik açısından kritik olan otomotiv sistemlerinde kullanılacak ThreadX SMP sertifikasına sahiptir. Ayrıca ThreadX SMP, en yüksek ISO 26262 sertifika düzeyini temsil eden Otomotiv Güvenlik Bütünlüğü Düzeyi (VERIM) D sertifikasına sahiptir.

Buna ek olarak, SAFETY-TÜV Saar, güvenliği kritik demir yolu uygulamalarında kullanılacak ve SW-SIL 4'e kadar EN 50128 standardına uygun olacak şekilde ThreadX SMP sertifikasına sahiptir.

![TÜV Sertifikası](media/image2.png)

SIL 4'e kadar IEC 61508  
SW güvenliği Sınıfı C'ye kadar IEC 62304  
ISO 26262İİSNA D  
EN 50128 SW-SIL 4  

> [!IMPORTANT]
> ThreadX SMP'nin hangi sürümlerinin TÜV tarafından onaylandı olduğu veya test raporlarının, sertifikaların ve ilişkili belgelerin kullanılabilirliği hakkında daha fazla [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) bilgi için lütfen başvurun.

### <a name="misra-c-compliant"></a>MISRA C Uyumlu 
MISRA C, C programlama dilini kullanan kritik sistemler için bir dizi programlama kılavuzudur. Özgün MISRA C yönergeleri öncelikli olarak otomotiv uygulamalarına yönelikti; ancak, MISRA C artık güvenlik açısından kritik herhangi bir uygulama için geçerli olduğu yaygın olarak kabul ediliyor. ThreadX SMP, MISRA-C:2004 ve MISRA C:2012'nin tüm "gerekli" ve "zorunlu" kurallarıyla uyumludur. ThreadX SMP üç "danışmanlık" kuralıyla da uyumludur. Diğer ayrıntılar için ***ThreadX_MISRA_Compliance.pdf*** belgeye bakın.

### <a name="ul-certification"></a>UL Sertifikası 
ThreadX SMP, UL 60730-1 Ek H, CSA E607301 Ek H, IEC 60730-1 Ek H, UL 60335-1 Ek R, IEC 60335-1 Ek R ve programlanabilir bileşenlerde yazılım için UL 1998 güvenlik standartları ile uyumluluk için UL sertifikasına sahiptir. IEC/UL 60730-1 ile birlikte, Ek H'de "Yazılım Kullanan Denetimler" için gereksinimlere sahip olan IEC 60335-1 standardı, Ek R'de "Programlanabilir Elektronik Devreler" için gereksinimleri açıklar. IEC 60730 Ek H ve IEC 60335-1 Ek R; makine, makine, alet, bilgisayar gibi gereçlerde kullanılan MCU donanım ve yazılım güvenliğini ele alır.

![UL Sertifikası](media/image3.png) 

*UL/IEC 60730, UL/IEC 60335, UL 1998*

> [!IMPORTANT]
> ThreadX SMP'nin hangi sürümlerinin TÜV tarafından onaylandı olduğu veya test raporlarının, sertifikaların ve ilişkili belgelerin kullanılabilirliği hakkında daha fazla [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) bilgi için lütfen başvurun.

### <a name="certification-pack"></a>Sertifika Paketi

ThreadX SMP Sertifika Paketi™ ThreadX SMP tabanlı ürünü sertifikalamanız veya başarıyla göndermeniz için gereken tüm ThreadX SMP kanıtlarını güvenlik açısından kritik Havacılık, Tıbbi ve Endüstriyel sistemler için gereken en yüksek güvenilirlik ve kritiklik düzeylerine sağlayan % 100 eksiksiz, anahtar teslim, sektöre özgü, tek başına bir pakettir. Desteklenen sertifikalar DO-178B, ED-12B, DO-278,CF510(k), IEC-62304, IEC-60601, ISO- 14971, UL-1998, IEC-61508, CENELEC EN50128, BS50128 ve 49CFR236. Sertifikasyon Paketi sales@expresslogic.com hakkında daha fazla bilgi için lütfen iletişime geçin.

## <a name="embedded-applications"></a>Katıştırılmış Uygulamalar

Katıştırılmış uygulamalar kablosuz iletişim cihazları, otomobil motorları, lazer yazıcılar, tıbbi cihazlar vb. ürünlerin içinde gömülü mikro işlemciler üzerinde yürütülür. Ekli uygulamaların bir diğer farkı da yazılım ve donanımlarının ayrılmış bir amacının yermasıdır.

### <a name="real-time-software"></a>Gerçek Zamanlı Yazılım 
Uygulama yazılımına zaman kısıtlamaları uygulanıyorsa, buna gerçek zamanlı *yazılım denir.* Temelde, işlemesini tam olarak bir süre içinde gerçekleştirmesi gereken yazılıma gerçek zamanlı *yazılım denir.* Katıştırılmış uygulamalar, dış olaylarla doğal etkileşimi nedeniyle neredeyse her zaman gerçek zamanlıdır.

### <a name="multitasking"></a>Çok görevli  
Daha önce belirtildiği gibi, katıştırılmış uygulamaların ayrılmış bir amacı vardır. Bu amacı yerine getirmek için yazılımın çeşitli görevler gerçekleştirmesi *gerekir.* Görev, uygulamanın belirli bir görevi yerine taşıyan yarı bağımsız bir kısmıdır. Ayrıca bazı görevlerin diğer görevlerden daha önemli olduğu da bir durum vardır. Katıştırılmış uygulamanın başlıca güçlüklerinden biri, çeşitli uygulama görevleri arasında işlemcinin ayırmasıdır. Rakip görevler arasında bu işleme ayırması, ThreadX SMP'nin birincil amacıdır.

### <a name="tasks-vs-threads"></a>Görevler ve İş Parçacıkları karşılaştırması 
Görevlerle ilgili başka bir ayrım gerçekleştirin. Görev terimi çeşitli yollarla kullanılır. Bazen ayrı olarak yüklenebilir bir program anlamına gelir. Diğer örneklerde, bir iç program segmentini ifade ediyor olabilir.

İşletim sistemi tartışmalarında, görevin kullanımının yerini daha fazla veya daha az alan iki terim vardır: *işlem ve iş* *parçacığı.* Bir *işlem,* kendi adres alanı olan tamamen bağımsız bir programdır, *iş* parçacığı ise bir işlem içinde yürütülen yarı bağımsız bir program kesimidir. İş parçacıkları aynı işlem adres alanı paylaşır. İş parçacığı yönetimiyle ilişkili ek yük çok azdır.

Çoğu ekli uygulama, tam performanslı işlem odaklı bir işletim sistemiyle ilişkili ek yükü (hem bellek hem de performans) karşılayamaz. Ayrıca, küçük mikro işlemciler gerçek bir işlem odaklı işletim sistemini destekleyecek donanım mimarisine sahip değildir. Bu nedenlerden dolayı ThreadX SMP, gerçek zamanlı katıştırılmış uygulamaların çoğu için son derece verimli ve pratik olan bir iş parçacığı modeli uygulamaya almaktadır.

Karışıklığı önlemek için ThreadX SMP görevi terimini *kullanmaz.* Bunun yerine, daha açıklayıcı ve açıklayıcı ad *iş parçacığı* kullanılır.

## <a name="threadx-smp-benefits"></a>ThreadX SMP Avantajları

ThreadX SMP'nin kullanımı, katıştırılmış uygulamalara birçok avantaj sağlar. Elbette birincil avantajı, katıştırılmış uygulama iş parçacıklarının işleme süresine nasıl ayrılmış olduğuyla ilgilidir.

### <a name="automatic-load-balancing"></a>Otomatik Yük Dengeleme  
ThreadX SMP, çok çekirdekli işlemcileri mümkün olduğunca kolay bir şekilde kullanan otomatik yük dengeleme (kullanılabilir çekirdeklerde iş parçacığı yürütme) sağlar. 

### <a name="improved-responsiveness"></a>Geliştirilmiş Yanıt Hızı  
ThreadX SMP gibi gerçek zamanlı çekirdeklerden önce, çoğu katıştırılmış uygulama işleme süresine genellikle C ana işlevinden basit bir denetim *döngüsüyle ayrılmıştır.* Bu yaklaşım hala çok küçük veya basit uygulamalarda kullanılır. Ancak büyük veya karmaşık uygulamalarda, herhangi bir etkinliğe yanıt süresi denetim döngüsünde bir geçişin en kötü harf işleme süresi işlevi olduğundan pratik değildir.

Daha da kötüsü, denetim döngüsünde değişiklikler yapılan her durumda uygulamanın zamanlama özellikleri değişir. Bu, uygulamanın doğal olarak kararsız ve bakımının ve geliştirmesini zorlaştırarak.

ThreadX SMP, önemli dış olaylara hızlı ve belirleyici yanıt süreleri sağlar. ThreadX SMP, daha yüksek öncelikli bir iş parçacığının düşük öncelikli bir iş parçacığını yürütmesini önlesine olanak sağlayan preemptive, priority-based scheduling algoritması aracılığıyla bunu gerçekleştirmektedir. Sonuç olarak, en kötü durum yanıt süresi bağlam anahtarını gerçekleştirmek için gereken süreye yaklaşıyor. Bu yalnızca belirlenmci değildir, aynı zamanda son derece hızlıdır.

### <a name="software-maintenance"></a>Yazılım Bakımı  
ThreadX SMP çekirdeği, uygulama geliştiricilerinin uygulamanın diğer alanlarının zamanlamasını değiştirmek zorunda kalmadan uygulama iş parçacıklarının belirli gereksinimlerine odaklanmalarını sağlar. Bu özellik, ThreadX SMP kullanan bir uygulamayı onarmayı veya geliştirmeyi de çok daha kolay hale getirir.

### <a name="increased-throughput"></a>Artan Aktarım Hızı  
Denetim döngüsü yanıt süresi sorununa olası bir çözüm, daha fazla yoklama eklemektir. Bu, yanıt hızını artırsa da sabit bir en kötü durum yanıt süresi garanti etmemektedir ve uygulamanın gelecekteki değişikliklerini geliştirmek için hiçbir şey yapmaz. Ayrıca, fazladan yoklama nedeniyle işlemci artık daha da gereksiz işleme gerçekleştirmektedir. Tüm bu gereksiz işleme, sistemin genel aktarım hızını azaltır.

Ek yükle ilgili ilginç bir nokta, birçok geliştiricinin ThreadX SMP gibi çok iş parçacıklı ortamların ek yükü artırarak toplam sistem aktarım hızı üzerinde olumsuz bir etkisi olduğunu varsaymadır. Ancak bazı durumlarda çoklu iş parçacığı kullanımı, denetim döngüsü ortamlarında oluşan tüm gereksiz yoklamaları ortadan kaldırarak ek yükü azaltır. Çok iş parçacıklı çekirdeklerle ilişkili ek yük genellikle bağlam değiştirme için gereken sürenin bir işlevidir. Bağlam değiştirme süresi yoklama işleminin altında ise ThreadX SMP, daha az ek yük ve daha fazla aktarım hızı potansiyeline sahip bir çözüm sağlar. Bu, ThreadX SMP'nin herhangi bir derecede karmaşıklık veya boyuta sahip uygulamalar için bariz bir seçim olduğunu gösterir.

### <a name="processor-isolation"></a>İşlemci Yalıtımı  
ThreadX SMP, uygulama ile temel işlemci arasında sağlam bir işlemci bağımsız arabirimi sağlar. Bu, geliştiricilerin önemli miktarda zaman harcayarak donanım ayrıntılarını öğrenmek yerine uygulamaya odaklanmalarını sağlar. 

### <a name="dividing-the-application"></a>Uygulamayı Bölme  
Denetim döngüsü tabanlı uygulamalarda, her geliştiricinin tüm uygulamanın çalışma zamanı davranışı ve gereksinimleri hakkında bilgi sahibi olması gerekir. Bunun nedeni, işlemci ayırma mantığının uygulamanın tamamına dağılmış durumdan kaynaklandı. Bir uygulamanın boyutu veya karmaşıklığı arttıkça, tüm geliştiricilerin uygulamanın tamamının hassas işleme gereksinimlerini hatırlaması imkansız hale gelir.

ThreadX SMP, her geliştiriciyi işlemci ayırmayla ilgili endişelerden serbest bırakarak ekli uygulamanın belirli bir parçasına odaklanmalarına olanak sağlar. Ayrıca ThreadX SMP, uygulamayı açıkça tanımlanmış iş parçacıklarına bölünmeye de neden olur. Tek başına, uygulamanın iş parçacıklarına bölünmesi geliştirmeyi çok daha basit hale getirir.

### <a name="ease-of-use"></a>Kullanım Kolaylığı  
ThreadX SMP, uygulama geliştiricisi ile birlikte tasarlanmıştır. ThreadX SMP mimarisi ve hizmet çağrısı arabirimi kolayca anlaşılacak şekilde tasarlanmıştır. Sonuç olarak, ThreadX SMP geliştiricileri gelişmiş özelliklerini hızlı bir şekilde kullanabilir.  

### <a name="improve-time-to-market"></a>Pazara satış sürelerini geliştirme  
ThreadX SMP'nin tüm avantajları, yazılım geliştirme sürecini hızlandırır. ThreadX SMP, çoğu işlemci sorunuyla ve en yaygın güvenlik sertifikalarını ele alır, böylece bu çabayı geliştirme zaman çizelgesinden çıkarır. Bunların hepsi pazara daha hızlı bir şekilde devam ediyor!  

### <a name="protecting-the-software-investment"></a>Yazılım Yatırımlarını Koruma  
Mimarisi nedeniyle ThreadX SMP, yeni işlemci ve/veya geliştirme aracı ortamlarına kolayca taşınabilir. Bu, ThreadX SMP'nin temel işlemcilerin ayrıntılarından uygulamaları dayanıklı olduğu gerçeğiyle birlikte, ThreadX SMP uygulamalarını yüksek oranda taşınabilir yapar. Sonuç olarak, uygulamanın geçiş yolu garanti olur ve özgün geliştirme yatırımı korunur.