---
title: Bölüm 1 - NetX Duo Azure RTOS Giriş
description: Bu bölümde NetX Duo'Azure RTOS giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8f45d32afcc2edbd5b851f1b7fb03e7fa2430ebc
ms.sourcegitcommit: 20a136b06a25e31bbde718b4d12a03ddd8db9051
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2021
ms.locfileid: "123552373"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo"></a>Bölüm 1 - NetX Duo Azure RTOS Giriş

Azure RTOS NetX Duo, özel olarak yerleşik threadX tabanlı uygulamalar için tasarlanmış TCP/IP standartlarının yüksek performanslı Azure RTOS gerçek zamanlı uygulamasıdır. Bu bölümde NetX Duo'ya giriş ve uygulamalarının ve avantajlarının açıklaması yer almaktadır. 

## <a name="netx-duo-unique-features"></a>NetX Duo Benzersiz Özellikleri

Diğer TCP/IP uygulamalarından farklı olarak NetX Duo, küçük mikro denetleyici tabanlı uygulamalardan güçlü RISC ve DSP işlemcileri kullanan uygulamalara kolayca ölçeklendirilen çok yönlü olacak şekilde tasarlanmıştır. Bu, ilk olarak iş istasyonu ortamlarına yönelik genel etki alanı veya diğer ticari uygulamalara karşı net bir karşıtlıktır ancak daha sonra eklenmiş tasarımlara dahil edilmiştir.

### <a name="piconettrade-architecture"></a>Piconet &trade; Mimarisi

NetX Duo'nun üstün ölçeklenebilirliği ve performansı, özellikle tümleşik sistemler için tasarlanmış bir yazılım mimarisi olan <em>Piconet'tir.</em> Piconet mimarisi, NetX Duo hizmetlerini C kitaplığı olarak kullanarak ölçeklenebilirliği en üst düzeye çıkarmaktadır. Bu şekilde, yalnızca uygulama tarafından kullanılan hizmetler son çalışma zamanı görüntüsüne getiri. Bu nedenle NetX Duo'nın gerçek boyutu uygulama tarafından belirlenir. Çoğu uygulama için NetX Duo'daki yönerge görüntüsü gereksinimleri 5 KBayt ile 30 KBayt arasında bir boyuta sahiptir. IPv6 adres yapılandırması ve komşu bulma protokolleri için IPv6 ve ICMPv6 etkinleştirildiğinde NetX Duo boyutu 30 kbayt ile 45 kbayt arasında değişebilir.

NetX Duo, yalnızca gerektiğinde iç bileşen işlev çağrılarını katmanlamayla üstün ağ performansı elde eder. Buna ek olarak, NetX Duo işlemenin büyük bölümü doğrudan satır içinde kullanılmaktadır ve bu da geçmişte ekli tasarımlarda kullanılan iş istasyonu ağ yazılımına göre olağanüstü performans avantajları sağlar.

### <a name="zero-copy-implementation"></a>Sıfır KopyaLı Uygulama

NetX Duo, TCP/IP'nin paket tabanlı, sıfır kopyalı bir uygulamasını sağlar. Sıfır kopyalama, uygulamanın paket arabelleğinde bulunan verilerin hiçbir zaman NetX Duo'nun içine kopyalanmayacağı anlamına gelir. Bu, performansı büyük ölçüde artırır ve değerli işlemci döngülerini uygulamaya serbest bırakarak ekli uygulamalarda önemlidir.

### <a name="udp-fast-pathtrade-technology"></a>UDP Hızlı Yol &trade; Teknolojisi

UDP <em>Hızlı Yol Teknolojisi ile</em>NetX Duo mümkün olan en hızlı UDP işlemeyi sağlar. Gönderme tarafında, isteğe bağlı UDP sağlama toplamları da dahil olmak üzere UDP işlemesi, nx_udp_socket_send <em>**içerir.**</em> Paket iç NetX Duo IP gönderme yordamı aracılığıyla gönderilmeye hazır olana kadar ek işlev çağrısı gönderilmez. Bu yordam aynı zamanda düzdür (yani işlev çağrısını iç içe yerleştirme en düşük düzeydedir) bu nedenle paket uygulamanın ağ sürücüsüne hızla sevk edilir. UDP paketi alınırken, NetX Duo paket alma işlemi paketi doğrudan uygun UDP yuvasının alma kuyruğuna yer verir veya UDP yuvasının alma kuyruğundan bir alma paketi beklerken askıya alınan ilk iş parçacığına verir. Ek ThreadX bağlam anahtarı gerekmez.

### <a name="ansi-c-source-code"></a>ANSI C Kaynak Kodu

NetX Duo tamamen ANSI C ile yazılmıştır ve ANSI C derleyicisi ve ThreadX desteğine sahip neredeyse tüm işlemci mimarileri için taşınabilir. 

### <a name="not-a-black-box"></a>Kara Kutu Değil

NetX Duo dağıtımlarının çoğunda tam C kaynak kodu yer almaktadır. Bu, birçok ticari ağ yığınında oluşan "kara kutu" sorunlarını ortadan kaldırıyor. NetX Duo'yı kullanarak, uygulama geliştiricileri ağ yığınının tam olarak ne yaptığını görebilir; hiçbir şey olmaz!

Kaynak kodun olması, uygulamaya özgü değişikliklere de olanak sağlar. Önerilmez, ancak gerekirse ağ yığınını değiştirebilme özelliğine sahip olmak faydalıdır.

Bu özellikler özellikle, kendi içinde veya genel etki alanı ağ yığınları ile çalışmaya alışkın olan geliştiricileri rahatlatıyor. Kaynak koduna ve kodu değiştirme özelliğine sahip olmasını beklerler. NetX Duo, bu tür geliştiriciler için en üst düzey ağ yazılımıdır.

### <a name="bsd-compatible-socket-api"></a>BSD-Compatible Yuvası API'si

Eski uygulamalar için NetX Duo, altta yüksek performanslı NetX Duo API'sini çağıran BSD uyumlu bir yuva arabirimi de sağlar. Bu, var olan ağ uygulaması kodunun NetX Duo'ya(NetX Duo)'ya (NetX Duo' ))/NetX Duo'ya (NetX Duo) (NetX Duo'ya) (Net

## <a name="rfcs-supported-by-netx-duo"></a>NetX Duo Tarafından Desteklenen RFC'ler

Temel ağ protokollerini açıklayan RFC'ler için NetX Duo desteği, aşağıdaki ağ protokollerini içerir ancak bunlarla sınırlı değildir. NetX Duo, küçük bellek ayak izine ve verimli yürütmeye sahip gerçek zamanlı bir işletim sisteminin kısıtlamaları dahilinde tüm genel önerileri ve temel gereksinimleri izler.

| **RFC**  | **Açıklama**                                        |
| -------- | ------------------------------------------------------ |
|RFC 1112 | IP Çok Noktaya Yayın için Konak Uzantıları (IGMPv1)           |
|RFC 1122 | İnternet Konakları Için Gereksinimler - İletişim Katmanları |
|RFC 2236 | İnternet Grup Yönetimi Protokolü, Sürüm 2          |
|RFC 768  | Kullanıcı Veri Birimi Protokolü (UDP)                           |
|RFC 791  | İnternet Protokolü (IP)                                 |
|RFC 792  | İnternet Denetim İletisi Protokolü (ICMP)               |
|RFC 793  | İletim Denetimi Protokolü (TCP)                    |
|RFC 826  | Ethernet Adres Çözümleme Protokolü (ARP) |
|RFC 903  | Ters Adres Çözümleme Protokolü (RARP) |
|RFC 5681 | TCP Tıkanıklığı Denetimi                     |

Aşağıda NetX Duo tarafından desteklenen IPv6 ile ilgili RFC'ler verilmiştir.

|**RFC** |**Açıklama**|
-------- | ------------------------------------------ |
|RFC 1981 |İnternet Protokolü v6 (IPv6) için Yol MTU Bulma|
|RFC 2460 | İnternet Protokolü v6 (IPv6) Belirtimi|
|RFC 2464 |Ethernet Ağları üzerinden IPv6 Paketlerinin İletimi|
|RFC 4291 |İnternet Protokolü v6 (IPv6) Adres mimarisi|
|RFC 4443 |İnternet Protokolü v6 (IPv6) Belirtimi için İnternet Denetim İletisi Protokolü (ICMPv6)|
|RFC 4861 |IP v6 için Komşu Bulma|
|RFC 4862 |IPv6 Durum Bilgisiz Adres Otomatik Yapılandırması|

## <a name="embedded-network-applications"></a>Katıştırılmış Ağ Uygulamaları

Katıştırılmış ağ uygulamaları cep telefonu, iletişim ekipmanı, otomotiv motorları, yazıcılar, tıbbi cihazlar vb. ürünlerin içinde gizli mikro işlemciler üzerinde ağ erişimi ve yürütmesi gereken uygulamalardır. Bu tür uygulamalar neredeyse her zaman bazı bellek ve performans kısıtlamalarına sahiptir. Ekli ağ uygulamalarının bir diğer farkı da yazılım ve donanımlarının ayrılmış bir amacının olduğudır.

İşlemlerini tam bir süre içinde gerçekleştirmesi gereken   ağ yazılımına gerçek zamanlı ağ yazılımı denir ve ağ uygulamalarına zaman kısıtlamaları uygulanarak gerçek zamanlı uygulamalar olarak sınıflandırılır. Katıştırılmış ağ uygulamaları, dış dünyayla doğal etkileşimi nedeniyle neredeyse her zaman gerçek zamanlıdır.

## <a name="netx-duo-benefits"></a>NetX Duo Avantajları

Ekli uygulamalar için NetX Duo kullanmanın temel avantajları, yüksek hızlı İnternet bağlantısı ve küçük bellek gereksinimleridir. NetX Duo, yüksek performanslı, çok görevli ThreadX gerçek zamanlı işletim sistemiyle de tümleştirilmiştir.

### <a name="improved-responsiveness"></a>Geliştirilmiş Yanıt Hızı

Yüksek performanslı NetX Duo protokol yığını, tümleşik ağ uygulamalarının hiç bu kadar hızlı yanıt vermesini sağlar. Bu özellikle, önemli miktarda ağ trafiğine veya tek bir pakette sıkı işleme gereksinimlerine sahip katıştırılmış uygulamalar için önemlidir.

### <a name="software-maintenance"></a>Yazılım Bakımı

NetX Duo kullanmak, geliştiricilerin ekli uygulamalarının ağ yönlerini kolayca bölümlemelerine olanak sağlar. Bu bölümleme, geliştirme sürecinin tamamını kolaylaştırır ve gelecekteki yazılım bakımını önemli ölçüde iyiler.

### <a name="increased-throughput"></a>Artan Aktarım Hızı

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