---
title: Bölüm 1-Azure RTOS NetX 'e giriş
description: Bu bölümde, Azure RTOS NetX 'e giriş ve uygulamalarının ve avantajlarından ilgili bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 48be6a7ecddc53b36b3cc1a9ecfb50a11e285881
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826891"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx"></a>Bölüm 1-Azure RTOS NetX 'e giriş

Azure RTOS NetX, katıştırılmış ThreadX tabanlı uygulamalar için özel olarak tasarlanmış TCP/IP standartları için yüksek performanslı gerçek zamanlı bir uygulama. Bu bölüm NetX 'e giriş ve uygulamalarının ve avantajlarından oluşan bir açıklama içerir.

## <a name="netx-unique-features"></a>NetX benzersiz özellikleri

NetX, diğer TCP/IP uygulamalarından farklı olarak, küçük mikro denetleyici tabanlı uygulamalardan güçlü RıSC ve DSP işlemcileri kullanan uygulamalara kolayca ölçeklendirilmesi için tasarlanmıştır. Bu, başlangıçta iş istasyonu ortamları için tasarlanan, ancak ekli tasarımlara sıkıştırılan genel etki alanı veya diğer ticari uygulamalar için keskin karşıtlığa sahiptir.

### <a name="piconettrade-architecture"></a>Piconet &trade; mimarisi

Özellikle gömülü sistemler için tasarlanmış bir yazılım mimarisi olan NetX 'in üstün ölçeklenebilirlik ve performansını temel alan *piconet*. Piconet mimarisi, NetX hizmetlerini C Kitaplığı olarak uygulayarak ölçeklenebilirliği en üst düzeye çıkarır. Bu şekilde, yalnızca uygulama tarafından kullanılan hizmetler son çalışma zamanı görüntüsüne getirilir. Bu nedenle, NetX 'in gerçek boyutu uygulama tarafından tamamen belirlenir. Çoğu uygulama için, NetX 'in resim boyutu gereksinimleri 5 Kbayt ile 30 kilobayt arasında değişir.

NetX, iç bileşen işlev çağrılarını yalnızca kesinlikle gerekli olduğunda katmanlayarak üstün ağ performansına erişir. Ayrıca, NetX işlemlerinin çoğu doğrudan satır içinde gerçekleştirilir ve bu, geçmişte yerleşik tasarımlarda sık kullanılan iş istasyonu ağ yazılımı üzerinde üstün performans avantajları elde edilir.</th>

### <a name="zero-copy-implementation"></a>Sıfır-uygulama kopyalama

NetX, TCP/IP 'nin paket tabanlı, *sıfır kopya* bir uygulamasını sağlar. Sıfır kopya, uygulamanın paket arabelleğindeki verilerin hiçbir şekilde NetX içinde kopyalanmadığı anlamına gelir. Bu, performansı önemli ölçüde artırır ve uygulama için önemli işlemci döngülerini serbest bırakır ve bu, katıştırılmış uygulamalarda son derece önemlidir.

### <a name="udp-fast-pathtrade-technology"></a>UDP hızlı yol &trade; teknolojisi

NETX, *UDP hızlı yol teknolojisi* ile en hızlı olası UDP işleme sağlar. Gönderme tarafında, isteğe bağlı UDP sağlama toplamı da dahil olmak üzere UDP işleme, ***nx_udp_socket_send*** hizmeti içinde tamamen bulunur. Paket, iç NetX IP gönderme yordamı aracılığıyla gönderilmeye hazırlanana kadar başka hiçbir işlev çağrısı yapılmaz. Bu yordam ayrıca düz (yani, işlev çağrısı iç içe geçidir), bu nedenle paket uygulamanın ağ sürücüsüne hızlı bir şekilde gönderilir. UDP paketi alındığında, NetX paket alma işlemi, paketi doğrudan uygun UDP yuvasının alma kuyruğuna koyar veya UDP yuvasının alma sırasından alınan bir alma paketi için bekleyen ilk iş parçacığına izin verir. Ek bir ThreadX bağlam anahtarı gerekmez.

### <a name="ansi-c-source-code"></a>ANSI C kaynak kodu

NetX, ANSI C 'de tamamen yazılır ve doğrudan bir ANSI C derleyicisi ve ThreadX desteği olan tüm işlemci mimarisine taşınabilir.

### <a name="not-a-black-box"></a>Siyah kutu değil

NetX dağıtımları, tüm C kaynak kodunu içerir. Bu, birçok ticari ağ yığınlarıyla oluşan "siyah kutu" sorunlarını ortadan kaldırır. NetX kullanarak uygulamalar, ağ yığınının tam olarak neler yaptığını görebilir, hiçbir gizleyebilmektir!
  
Kaynak kodun olması, uygulamaya özgü değişikliklere de izin verir. Önerilmese de, gerekli olduğunda ağ yığınını değiştirme imkanına kesinlikle yarar vardır.  

Bu özellikler özellikle, şirket içi veya genel etki alanı ağ yığınları ile çalışmaya alışkın olan geliştiricilere Comforting. Bunlar, kaynak kodu ve değişiklik yapabilme yeteneğinin olmasını bekler. NetX, bu tür geliştiriciler için en son ağ yazılımıdır.

### <a name="bsd-compatible-socket-api"></a>BSD-Compatible yuva API 'SI

Eski uygulamalarda NetX, altında yüksek performanslı NetX API 'sine çağrı yapan bir BSD uyumlu yuva arabirimi sağlar. Bu, var olan ağ uygulama kodunu NetX 'e geçirmeye yardımcı olur.

## <a name="rfcs-supported-by-netx"></a>NetX tarafından desteklenen RFC 'Ler

Temel ağ protokollerini açıklayan RFC 'lerin NetX desteği aşağıdakileri içerir, ancak aşağıdaki ağ protokolleriyle sınırlı değildir. NetX, küçük bellek ayak ve verimli yürütme ile gerçek zamanlı bir işletim sisteminin kısıtlamaları dahilinde tüm genel önerilere ve temel gereksinimlere uyar.

| RFC      | Açıklama                                            |
|----------|--------------------------------------------------------|
| RFC 1112 | IP çok noktaya yayın için konak uzantıları (IGMPv1)           |
| RFC 1122 | Internet konakları için gereksinimler-Iletişim katmanları |
| RFC 2236 | Internet Grup Yönetimi Protokolü, sürüm 2          |
| RFC 768  | Kullanıcı veri birimi Protokolü (UDP)                           |
| RFC 791  | Internet Protokolü (IP)                                 |
| RFC 792  | Internet Denetim Iletisi Protokolü (ıCMP)               |
| RFC 793  | İletim Denetimi Protokolü (TCP)                    |
| RFC 826  | Ethernet Adres Çözümleme Protokolü (ARP)             |
| RFC 903  | Ters Adres Çözümleme Protokolü (RARP)             |
|          |                                                        |

## <a name="embedded-network-applications"></a>Katıştırılmış ağ uygulamaları

Katıştırılmış ağ uygulamaları, cep telefonları, iletişim donatımı, oto motor, lazer yazıcılar, tıbbi cihazlar vb. gibi ürünlerin içinde gizlenen mikro işlemcilerde ağ erişimi ve yürütme gerektiren uygulamalardır. Bu uygulamalarda neredeyse her zaman bazı bellek ve performans kısıtlamaları vardır. Katıştırılmış ağ uygulamalarının başka bir ayrım, yazılım ve donanımının özel bir amaca sahip olması olabilir.

### <a name="real-time-network-software"></a>Gerçek zamanlı ağ yazılımı  

Temelde, işlemesini tam bir süre içinde gerçekleştirmesi gereken ağ yazılımlarına *gerçek* zamanlı *ağ* yazılımı denir ve ağ uygulamalarına zaman kısıtlamaları eklendiğinde bunlar gerçek zamanlı uygulamalar olarak sınıflandırılır. Gömülü ağ uygulamaları, dış dünyanın kendilerine ait etkileşimi nedeniyle neredeyse her zaman gerçek zamanlı olarak gerçekleştirilir.

## <a name="netx-benefits"></a>NetX avantajları

Ekli uygulamalar için NetX kullanmanın başlıca avantajları yüksek hızlı Internet bağlantısı ve çok küçük bellek gereksinimleridir. NetX, yüksek performanslı, çok görevli ThreadX gerçek zamanlı işletim sistemiyle de tamamen tümleşiktir.

### <a name="improved-responsiveness"></a>İyileştirilmiş yanıt hızı  

Yüksek performanslı NetX protokol yığını, katıştırılmış ağ uygulamalarının daha önce hiç olmadığı kadar hızlı yanıt vermesini sağlar. Bu özellikle, tek bir pakette önemli miktarda ağ trafiği veya katı işleme gereksinimi olan eklenmiş uygulamalar için önemlidir.

### <a name="software-maintenance"></a>Yazılım Bakımı

NetX kullanmak, geliştiricilerin katıştırılmış uygulamalarının ağ yönlerini kolayca bölümlememesini sağlar. Bu bölümlendirme, tüm geliştirme sürecini kolaylaştırır ve gelecekteki yazılım bakımını önemli ölçüde geliştirir.

### <a name="increased-throughput"></a>Artan verimlilik

NetX, en düşük düzeyde paket işleme yükü tarafından elde edilen en yüksek performanslı ağı sağlar. Bu, daha fazla verim artışı da sunar.

### <a name="processor-isolation"></a>İşlemci yalıtımı

NetX, uygulama ile temel alınan işlemci ve ağ donanımı arasında sağlam, işlemcinin bağımsız bir arabirim sağlar. Bu, geliştiricilerin, ağ iletişimini doğrudan etkileyen donanım sorunlarıyla ilgili ek süre harcamak yerine uygulamanın ağ yönlerini yoğunlaşmasını sağlar.

### <a name="ease-of-use"></a>Kullanım kolaylığı

NetX, uygulama geliştiricisi göz önünde bulundurularak tasarlanmıştır. NetX mimarisi ve hizmet çağrısı arabirimine kolayca anlaşılır. Sonuç olarak, NetX geliştiricileri gelişmiş özelliklerini hızlı bir şekilde kullanabilir.

### <a name="improve-time-to-market"></a>Pazara ulaşma süresini iyileştirme

NetX 'in güçlü özellikleri yazılım geliştirme sürecini hızlandırır. NetX, çoğu işlemci ve ağ donanımı sorunlarını soyutlar, böylece bu konular uygulamanın ağa özgü alanlarından birçoğundan kaldırılıyor. Bu, kullanımı kolaylaştırma ve gelişmiş özellik kümesiyle birlikte, pazara daha hızlı bir süre içinde sonuçlanır.

### <a name="protecting-the-software-investment"></a>Yazılım yatırımınızı koruma

NetX, ANSI C 'de özel olarak yazılır ve ThreadX gerçek zamanlı işletim sistemiyle tamamen tümleşiktir. Bu, NetX uygulamalarının tüm ThreadX desteklenen işlemcilere anında taşınabilir olduğunu gösterir. Yine de daha iyi, her hafta için ThreadX ile tamamen yeni bir işlemci mimarisi desteklenebilir. Sonuç olarak, NetX kullanılması uygulamanın geçiş yolunu sağlar ve orijinal geliştirme yatırımını korur.
