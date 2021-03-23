---
title: Bölüm 1-Azure RTOS NetX Duo 'e giriş
description: Bu bölümde, Azure RTOS NetX Duo 'e giriş ve uygulamalarının ve avantajlarından ilgili bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 91dfd0e62cb565f677faa7d52fe22abc1f0e19a1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826224"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo"></a>Bölüm 1-Azure RTOS NetX Duo 'e giriş

Azure RTOS NetX Duo, katıştırılmış Azure RTOS ThreadX tabanlı uygulamalar için özel olarak tasarlanmış TCP/IP standartlarının yüksek performanslı gerçek zamanlı uygulamasıdır. Bu bölüm NetX Duo 'e giriş ve uygulamalarının ve avantajlarından oluşan bir açıklama içerir. 

## <a name="netx-duo-unique-features"></a>NetX Duo benzersiz özellikleri

NetX Duo, diğer TCP/IP uygulamalarından farklı olarak, küçük mikro denetleyici tabanlı uygulamalardan güçlü RıSC ve DSP işlemcileri kullanan uygulamalara kolayca ölçeklenirken çok yönlü olacak şekilde tasarlanmıştır. Bu, başlangıçta iş istasyonu ortamları için tasarlanan, ancak ekli tasarımlara sıkıştırılan genel etki alanı veya diğer ticari uygulamalar için keskin karşıtlığa sahiptir.

### <a name="piconettrade-architecture"></a>Piconet &trade; mimarisi

NetX Duo 'un üstün ölçeklenebilirlik ve performansının temelindeki <em>piconet</em>, özellikle katıştırılmış sistemler için tasarlanmış bir yazılım mimarisidir. Piconet mimarisi, NetX Duo hizmetlerini C Kitaplığı olarak uygulayarak ölçeklenebilirliği en üst düzeye çıkarır. Bu şekilde, yalnızca uygulama tarafından kullanılan hizmetler son çalışma zamanı görüntüsüne getirilir. Bu nedenle, NetX Duo gerçek boyutu uygulama tarafından belirlenir. Çoğu uygulama için, NetX Duo yönerge görüntüsü gereksinimleri 5 Kbayt ile 30 kilobayt arasında değişir. IPv6 adres yapılandırması ve komşu bulma protokolleri için IPv6 ve ICMPv6 etkinken NetX Duo, 30 Kbayt ila 45 Kbayt boyutunda.

NetX Duo, iç bileşen işlev çağrılarını yalnızca gerekli olduğunda katmanlayarak üstün ağ performansına erişir. Ayrıca, NetX Duo işlemenin çoğu doğrudan satır içinde gerçekleştirilir ve bu, geçmişte yerleşik tasarımlarda kullanılan iş istasyonu ağ yazılımının üstün performans avantajları elde edilir.

### <a name="zero-copy-implementation"></a>Sıfır-uygulama kopyalama

NetX Duo, TCP/IP 'nin paket tabanlı, sıfır kopya bir uygulamasını sağlar. Sıfır kopya, uygulamanın paket arabelleğindeki verilerin hiçbir şekilde NetX Duo içinde kopyalanmadığı anlamına gelir. Bu, performansı önemli ölçüde artırır ve uygulama için, katıştırılmış uygulamalarda önemli olan değerli işlemci döngülerini serbest bırakır.

### <a name="udp-fast-pathtrade-technology"></a>UDP hızlı yol &trade; teknolojisi

NETX Duo, <em>UDP hızlı yol teknolojisi</em>ile en hızlı olası UDP işlemesini sağlar. Gönderme tarafında, isteğe bağlı UDP sağlama toplamı da dahil olmak üzere UDP işleme, <em>**nx_udp_socket_send**</em> hizmeti içinde yer alır. Paket, iç NetX Duo IP gönderme yordamı aracılığıyla gönderilmeye hazırlanana kadar başka hiçbir işlev çağrısı yapılmaz. Bu yordam ayrıca düz (yani, işlev çağrısı iç içe geçme en az bir deyişle, paket uygulamanın ağ sürücüsüne hızlı bir şekilde gönderilir. UDP paketi alındığında, NetX Duo paket alma işlemi, paketi doğrudan uygun UDP yuvasının alma kuyruğuna koyar veya UDP yuvasının alma sırasından alınan bir alma paketi için bekleyen ilk iş parçacığına izin verir. Ek bir ThreadX bağlam anahtarı gerekmez.

### <a name="ansi-c-source-cod"></a>ANSI C kaynak COD

NetX Duo, ANSI C 'de tamamen yazılır ve doğrudan bir ANSI C derleyicisi ve ThreadX desteği olan tüm işlemci mimarisine taşınabilir. 

### <a name="not-a-black-box"></a>Siyah kutu değil

NetX Duo dağıtımların çoğu, tüm C kaynak kodunu içerir. Bu, birçok ticari ağ yığınlarıyla oluşan "siyah kutu" sorunlarını ortadan kaldırır. NetX Duo kullanarak, uygulamalar, ağ yığınının tam olarak neler yaptığını görebilir; herhangi bir gizleyebilmektir!

Kaynak kodun olması, uygulamaya özgü değişikliklere de izin verir. Önerilmese de, gerekirse ağ yığınını değiştirme imkanına sahip olmanız yararlı olur.

Bu özellikler özellikle, şirket içi veya genel etki alanı ağ yığınları ile çalışmaya alışkın olan geliştiricilere Comforting. Bunlar, kaynak kodu ve değişiklik yapabilme yeteneğinin olmasını bekler. NetX Duo, bu tür geliştiriciler için en son ağ yazılımıdır.

### <a name="bsd-compatible-socket-api"></a>BSD-Compatible yuva API 'SI

Eski uygulamalarda NetX Duo, altında yüksek performanslı NetX Duo API 'sine çağrı yapan bir BSD uyumlu yuva arabirimi de sağlar. Bu, var olan ağ uygulama kodunu NetX Duo 'e geçirmeye yardımcı olur.

## <a name="rfcs-supported-by-netx-duo"></a>NetX Duo tarafından desteklenen RFC 'Ler

Temel ağ protokollerini tanımlayan RFC 'Lerde NetX Duo desteği, ancak aşağıdaki ağ protokolleriyle sınırlı değildir. NetX Duo, küçük bellek ayak ve verimli yürütme ile gerçek zamanlı bir işletim sisteminin kısıtlamaları dahilinde tüm genel önerilere ve temel gereksinimlere uyar.

| **RFC**  | **Açıklama**                                        |
| -------- | ------------------------------------------------------ |
|RFC 1112 | IP çok noktaya yayın için konak uzantıları (IGMPv1)           |
|RFC 1122 | Internet konakları için gereksinimler-Iletişim katmanları |
|RFC 2236 | Internet Grup Yönetimi Protokolü, sürüm 2          |
|RFC 768  | Kullanıcı veri birimi Protokolü (UDP)                           |
|RFC 791  | Internet Protokolü (IP)                                 |
|RFC 792  | Internet Denetim Iletisi Protokolü (ıCMP)               |
|RFC 793  | İletim Denetimi Protokolü (TCP)                    |
|RFC 826  | Ethernet Adres Çözümleme Protokolü (ARP) |
|RFC 903  | Ters Adres Çözümleme Protokolü (RARP) |
|RFC 5681 | TCP tıkanıklık denetimi                     |

NetX Duo tarafından desteklenen IPv6 ile ilgili RFC 'Ler aşağıda verilmiştir.

|**RFC** |**Açıklama**|
-------- | ------------------------------------------ |
|RFC 1981 |Internet Protokolü V6 için yol MTU Keşfi (IPv6)|
|RFC 2460 | Internet Protokolü V6 (IPv6) belirtimi|
|RFC 2464 |Ethernet ağları üzerinden IPv6 paketlerinin iletimi|
|RFC 4291 |Internet Protokolü V6 (IPv6) adresleme mimarisi|
|RFC 4443 |Internet Protokolü V6 (IPv6) belirtimi için Internet Denetim Iletisi Protokolü (Icmpv6)|
|RFC 4861 |IP V6 için komşu bulma|
|RFC 4862 |IPv6 durum bilgisiz adresi otomatik yapılandırması|

## <a name="embedded-network-applications"></a>Katıştırılmış ağ uygulamaları

Katıştırılmış ağ uygulamaları, cep telefonları, iletişim donatımı, oto motor, lazer yazıcılar, tıbbi cihazlar vb. gibi ürünlerin içinde gizlenen mikro işlemcilerde ağ erişimi ve yürütme gerektiren uygulamalardır. Bu uygulamalarda neredeyse her zaman bazı bellek ve performans kısıtlamaları vardır. Katıştırılmış ağ uygulamalarının başka bir ayrım, yazılım ve donanımının özel bir amaca sahip olması olabilir.

İşlemesini tam bir süre içinde gerçekleştirmesi gereken ağ yazılımlarına *gerçek* zamanlı *ağ* yazılımı denir ve ağ uygulamalarına zaman kısıtlamaları eklendiğinde bunlar gerçek zamanlı uygulamalar olarak sınıflandırılır. Gömülü ağ uygulamaları, dış dünya ile ilgili etkileşimlerinden dolayı neredeyse her zaman gerçek zamanlı olarak gerçekleştirilir.

## <a name="netx-duo-benefits"></a>NetX Duo avantajları

Gömülü uygulamalar için NetX Duo kullanmanın başlıca avantajları, yüksek hızlı Internet bağlantısı ve küçük bellek gereksinimleridir. NetX Duo, yüksek performanslı, çok görevli ThreadX gerçek zamanlı işletim sistemiyle de tümleşiktir.

### <a name="improved-responsiveness"></a>İyileştirilmiş yanıt hızı

Yüksek performanslı NetX Duo protokol yığını, katıştırılmış ağ uygulamalarının daha önce hiç olmadığı kadar hızlı yanıt vermesini sağlar. Bu özellikle, tek bir pakette önemli miktarda ağ trafiği veya katı işleme gereksinimi olan eklenmiş uygulamalar için önemlidir.

### <a name="software-maintenance"></a>Yazılım Bakımı

NetX Duo kullanımı, geliştiricilerin katıştırılmış uygulamalarının ağ yönlerini kolayca bölümlememesini sağlar. Bu bölümlendirme, tüm geliştirme sürecini kolaylaştırır ve gelecekteki yazılım bakımını önemli ölçüde geliştirir.

### <a name="increased-throughput"></a>Artan verimlilik

NetX Duo, en düşük düzeyde paket işleme yükü tarafından elde edilen en yüksek performanslı ağı sağlar. Bu, daha fazla verim artışı da sunar.

### <a name="processor-isolation"></a>İşlemci yalıtımı

NetX Duo, uygulama ile temel alınan işlemci ve ağ donanımı arasında sağlam, işlemcinin bağımsız bir arabirim sağlar. Bu, geliştiricilerin, ağ iletişimini doğrudan etkileyen donanım sorunlarıyla ilgili ek süre harcamak yerine uygulamanın ağ yönlerini yoğunlaşmasını sağlar.

### <a name="ease-of-use"></a>Kullanım kolaylığı

NetX Duo, uygulama geliştiricisi göz önünde bulundurularak tasarlanmıştır. NetX Duo mimarisi ve hizmet çağrısı arabirimine kolayca anlaşılır. Sonuç olarak, NetX Duo geliştiricileri gelişmiş özelliklerini hızlı bir şekilde kullanabilir.

### <a name="improve-time-to-market"></a>Pazara ulaşma süresini iyileştirme

NetX Duo 'un güçlü özellikleri yazılım geliştirme sürecini hızlandırır. NetX Duo çoğu işlemci ve ağ donanımı sorunlarını soyutlar, böylece bu konular uygulamanın ağa özgü alanlarından birçoğundan kaldırılıyor. Bu, kullanımı kolaylaştırma ve gelişmiş özellik kümesiyle birlikte kullanıldığında pazara daha hızlı bir süre içinde sonuçlanır!

### <a name="protecting-the-software-investment"></a>Yazılım yatırımınızı koruma

NetX Duo, ANSI C 'de özel olarak yazılır ve ThreadX gerçek zamanlı işletim sistemiyle tamamen tümleşiktir. Bu, NetX Duo uygulamalarının tüm ThreadX desteklenen işlemcilere anında taşınabilir olduğunu gösterir. Yine de daha iyi, yeni bir işlemci mimarisi, bir hafta içinde ThreadX ile desteklenebilir. Sonuç olarak, NetX Duo kullanımı uygulamanın geçiş yolunu sağlar ve orijinal geliştirme yatırımını korur.

## <a name="ipv6-ready-logo-certification"></a>IPv6 Ready Logo sertifikası

NetX Duo "IPv6 hazır" sertifikası, IPv6 'Ya hazır kuruluştan erişilebilen "IPv6 Core Protocol (Aşama 2) self test" paketiyle alındı. Test platformu ve test çalışmaları hakkında daha fazla bilgi için aşağıdaki IPv6-Ready Project Web sitelerine bakın:[**https://www.ipv6ready.org/**](https://www.ipv6ready.org/)

Phase 2 IPv6 Core Protocol Self Test Suite, bir IPv6 yığınının, kapsamlı test ile aşağıdaki RFC 'lerde ayarlanan gereksinimleri kullandığını doğrular:  
Bölüm 1: RFC 2460  
Bölüm 2: RFC 4861  
Bölüm 3: RFC 4862  
Bölüm 4: RFC 1981  
Bölüm 5: RFC 4443  

## <a name="ixanvl-test"></a>IxANVL testi

NetX Duo, IXIA 'ten IxANVL ile test edilmiştir. IxANVL, otomatik ağ ve protokol doğrulaması için endüstri standardıdır. IxANVL hakkında daha fazla bilgiyi şurada bulabilirsiniz: [**https://www.ixiacom.com/products/ixanvl**](https://www.ipv6ready.org/)

Özellikle aşağıdaki NetX Duo modülleri IxANVL ile test edilmiştir:

|**Modül** | **Standart** |
| --------- | ------------ |
|IP | RFC791 </br> RFC1122 </br> RFC894|
|ICMP | RFC792 </br> RFC1122 </br> RFC1812|
|UDP | RFC768 </br> RFC1122|
|TCP-Core| RFC793 </br> RFC1122 </br> RFC2460|
|TCP-Advanced| RFC1981</br>RFC2001</br>RFC2385</br>RFC2463</br>RFC813</br>RFC896|
|TCP-Performance| RFC793</br>RFC1323</br>RFC2018|

## <a name="safety-certifications"></a>Güvenlik sertifikaları

### <a name="tv-certification"></a>TÜV Sertifikası  

NetX Duo, IEC61508 ve ıEC-62304 ' e göre güvenlik açısından kritik sistemlerde kullanılmak üzere SGS-TÜV Saar tarafından sertifikalandırilmiştir. Sertifika NetX Duo 'in, "elektrik, elektronik ve programlanabilir elektronik güvenliği ile ilgili sistemlerin Işlevsel güvenliği" için Uluslararası Elektroteknik Komisyonu (ıEC) 61508 ve ıEC 62304 ' nin en yüksek güvenlik bütünlüğü düzeyleri için güvenlik ile ilgili yazılımların geliştirilmesinde kullanılabileceğini onaylar. Almanya 'nun sgsgroup ve TÜV Saarland 'ın bir Joint girişim aracılığıyla oluşturulan SGS-TÜV Saar, dünya çapındaki güvenlikle ilgili sistemler için katıştırılmış yazılımları test etmek, denetlemek, doğrulamak ve sertifika almak için önde gelen acalacak, bağımsız şirket haline geldi. Endüstriyel güvenlik standardı IEC 61508 ve bundan türetilmiş tüm standartlar, 62304 IEC, elektronik ve programlanabilir elektronik güvenliği ile ilgili tıbbi cihazların, işlem denetim sistemlerinin, endüstriyel makinelerin ve demiryolu denetim sistemlerinin işlevsel güvenliğini güvence altına almak için kullanılır. 

SGS-TÜV Saar, ISO 26262 standardına göre güvenlik açısından kritik bir oto dili sisteminde kullanılmak üzere sertifikalı NetX Duo 'e sahiptir. NetX Duo 'in yanı sıra, en yüksek ISO 26262 sertifikası düzeyini temsil eden, oto ve güvenlik bütünlüğü düzeyi (asıl) D 'ye sertifikalıdır. 

Buna ek olarak, SGS-TÜV Saar sertifikalı NETX Duo 'e, en çok 50128 standart ile SW-SIL 4 ' e kadar olan güvenlik açısından kritik demiryolu uygulamalarında de kullanılır.

![SGS-TÜV Saar sertifika logosu diyagramı.](./media/user-guide/sgs-tuv-saar-logo.png)

IEC 61508, SIL 4 ' e kadar  
IEC 62304 en fazla SW güvenlik sınıfı C ISO 26262 ASııL D EN 50128 yazılım-SIL 4

> [!IMPORTANT]
> *NetX Duo 'un hangi sürümlerinin TÜV veya test raporlarının, sertifikaların ve ilişkili belgelerin kullanılabilirliği hakkında daha fazla bilgi için lütfen Microsoft 'a başvurun.*

### <a name="ul-certification"></a>UL sertifikası

NetX Duo,, programlanabilir bileşenlerinde yazılım için ul 60730-1 Ek H, CSA E60730-1 Ek H, ıEC 60730-1 Ek H, UL 60335-1 ek R, ıEC 60335-1 ek R ve UL 1998 güvenlik standartları ile uyumlu bir şekilde sertifikalandırilmiştir. Ek H 'de "yazılım kullanan denetimler" için gereksinimleri olan ıEC/UL 60730-1 ile birlikte ıEC 60335-1 standardı, ek R. ıEC 60730 ek H ve ıEC 60335-1 ek R içindeki "programlanabilir elektronik devreler" için gereksinimleri açıklar. Örneğin, yıkama makineleri, dishörler, kurutma, kurutıcılar, freezers ve ovens gibi gereçlerde kullanılan MCU donanım ve yazılımlarının güvenliğini ele.

![UL sertifika logosunun diyagramı.](./media/user-guide/c-ru-us-logo.png)

*UL/ıEC 60730, UL/ıEC 60335, UL 1998*

> [!IMPORTANT]  
> *NetX Duo sürümü, UL tarafından sertifikalı veya test raporlarının, sertifikaların ve ilişkili belgelerin kullanılabilirliği hakkında daha fazla bilgi için lütfen Microsoft 'a başvurun.*