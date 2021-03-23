---
title: Bölüm 1-Azure RTOS NetX Duo SNTP 'e giriş
description: Azure RTOS NetX basit ağ zaman Protokolü (SNTP), Internet üzerinden saatleri eşitlemek için tasarlanan bir protokoldür.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b3e1170197c6c4981060459104da80e354fac5db
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825751"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-sntp"></a>Bölüm 1-Azure RTOS NetX Duo SNTP 'e giriş 

Azure RTOS NetX basit ağ zaman Protokolü (SNTP), Internet üzerinden saatleri eşitlemek için tasarlanan bir protokoldür. SNTP sürüm 4, ağ zaman Protokolü (NTP) tabanlı bir Basitleştirilmiş protokoldür. Basit, durumsuz bir protokolde zaman güncelleştirmelerini gerçekleştirmek için Kullanıcı Datagram Protokolü (UDP) hizmetlerinden yararlanır. NTP olarak karmaşık olmasa da, SNTP son derece güvenilir ve doğru. Günümüzde Internet 'in çoğu yerde, SNTP, eşitleme kaynağı ve ağ yollarının özelliklerine bağlı olarak accuracies of 1-50 milisaniyesi sağlar. SNTP 'in zaman güncelleştirmelerini alma güvenilirliğini sağlamak için birçok seçeneği vardır. Alternatif sunuculara geçiş yapma, yoklama algoritmalarının geri dönmesi ve otomatik zaman sunucu keşfi uygulamak, bir SNTP istemcisinin değişken Internet zaman hizmeti ortamını işlemesi için gereken yollardan biridir. Kesinliği, basitliği ve uygulama kolaylığını sağlar. SNTP, öncelikli olarak ulusal saat ve sıklık dağıtımını yapma (örneğin, NTP sunucusu) hizmetlerine erişmek için kapsamlı mekanizmalar sağlamaya yöneliktir.

## <a name="netx-duo-sntp-client-requirements"></a>NetX Duo SNTP Istemci gereksinimleri

NetX Duo SNTP Istemcisi bir IP örneğinin zaten oluşturulmuş olmasını gerektirir. Ayrıca, aynı IP örneğinde UDP etkinleştirilmeli ve bir SNTP sunucusuna zaman verileri göndermek için 123 *iyi bilinen* bağlantı noktasına erişimi olması gerekir, ancak alternatif bağlantı noktaları da çalışacaktır. Yayın istemcileri, yayın sunucusunun gönderdiği UDP bağlantı noktasını, genellikle 123 ' ye bağlamalıdır. NetX Duo SNTP Istemci uygulamasının bir veya daha fazla IP SNTP sunucu adresi olmalıdır.

## <a name="netx-duo-sntp-client-limitations"></a>NetX Duo SNTP Istemci sınırlamaları 

SNTP Istemci API 'SI tarafından işlenen NTP zaman güncelleştirmelerinde yerel zaman gösterimindeki duyarlık, milisaniyelik çözünürlükle sınırlıdır.

SNTP Istemcisi istediğiniz zaman yalnızca tek bir SNTP sunucu adresini barındırır. Bu sunucu artık geçerli değilse, uygulamanın SNTP Istemci görevini durdurması ve yayın ya da tek noktaya yayın SNTP iletişimini kullanarak başka bir SNTP sunucu adresiyle yeniden başlatılması gerekir.

SNTP Istemcisi, manycast 'yi desteklemez.

NetX Duo SNTP Istemcisi alınan paket verilerini doğrulamak için kimlik doğrulama mekanizmalarını desteklemez.

## <a name="netx-duo-sntp-client-operation"></a>NetX Duo SNTP Istemci Işlemi

RFC 4330, SNTP istemcilerinin yalnızca yerel ağının en yüksek katman ve tercihen bir NTP veya SNTP istemcisinin eşitlemeye bağımlı olmadığı yapılandırmalarda çalışabilmesini öneriyor. Katman düzeyi NTP zaman hiyerarşisinde, katman 1 ' in en üst düzey (bir kök saat sunucusu) ve 15 izin verilen en düşük düzeyde (örn. istemci) bulunduğu ana bilgisayar konumunu yansıtır. SNTP Istemci varsayılan en düşük katman 2 ' dir.

NetX Duo SNTP Istemcisi, Internet üzerinden zaman alabilmesini sağlamak için iki temel moddan birinde, tek noktaya yayın veya Yayınla çalışabilir. Tek noktaya yayın modunda, Istemci SNTP sunucusunu düzenli aralıklarla yoklar ve bu sunucudan bir yanıt almayı bekler. Bir tane alındığında, Istemci, RFC 4330 tarafından önerilen bir ' Sanity denetimleri ' kümesi uygulayarak yanıtın geçerli bir zaman güncelleştirmesi içerdiğini doğrular. Istemci daha sonra, varsa, sunucu saatinin yerel saatine göre zaman farkını uygular. Yayın modunda, istemci yalnızca zaman güncelleştirme yayınlarını dinler ve güncelleştirme zamanı verilerini doğrulamak üzere benzer bir sağlamlık denetimleri uyguladıktan sonra yerel saatini korur. Sanity denetimleri, aşağıdaki **SNTP Sanity denetimleri** bölümünde ayrıntılı olarak açıklanmıştır.

Istemci her iki modda da çalışmadan önce, işletim parametrelerini kurması gerekir. Bu, sırasıyla tek noktaya veya yayın modlarında *nx_sntp_client_initialize_unicast* ya da *nx_sntp_client_initialize_broadcast* çağırarak yapılır. Bu işlem, geçerli bir güncelleştirme olmadan en uzun süre atlama süresini, alınan birbirini izleyen geçersiz güncelleştirmelerin sınırını, tek noktaya yayın modu için bir yoklama aralığı, işlem modunu (örneğin, tek noktaya vs. Broadcast ve SNTP sunucusu) ayarlar.

Alınan en fazla zaman atlama süresi veya en fazla geçersiz güncelleştirme aşılırsa, SNTP Istemcisi çalışmaya devam eder ancak geçerli SNTP sunucu durumunu geçersiz olarak ayarlar. Uygulama, SNTP sunucusunun hala geçerli güncelleştirmeler gönderdiğini doğrulamak için *nx_sntp_client_receiving_updates* HIZMETINI kullanarak SNTP istemcisini yoklayabilirler. Aksi takdirde, *nx_sntp_client_stop* HIZMETINI kullanarak SNTP istemci iş parçacığını durdurmalı ve başka bir SNTP sunucu adresi ayarlamak için iki başlatma hizmetinden birini çağırmalıdır. SNTP Istemcisini yeniden başlatmak için uygulama *nx_sntp_client_run_broadcast* veya *nx_sntp_client_run_unicast* çağırır. Uygulamanın, başlatma çağrısında SNTP Istemci işletim modunu, istediğiniz şekilde tek noktaya veya yayına geçiş yapmak için değiştirebileceğini unutmayın.

### <a name="local-clock-operation"></a>Yerel Saat Işlemi

Ana NTP saatindeki saniye sayısına veya ilk NTP dönemi içinde geçen saniye sayısına göre SNTP saati (örn. Ocak **1900 00:00:00** , 1 **1999 00:00:00**). 01-01-1999 önem artışı, son geçen ikinci oluşma gerçekleşti. Bu değer aşağıdaki gibi tanımlanır:

\#NTP_SECONDS_AT_01011999 0xBA368E80 tanımlama

SNTP Istemcisi çalışmadan önce, uygulama isteğe bağlı olarak Istemcinin temel zaman olarak kullanacağı SNTP Istemci yerel saatini başlatabilir. Bunu yapmak için *nx_sntp_client_set_local_time* hizmetini kullanması gerekir. Bu süre, NTP biçimi, saniyeler ve kesir olarak zaman alır; burada kesir, NTP dar saat içinde milisaniyedir. İdeal olarak, uygulama bağımsız bir kaynaktan bir SNTP saati elde edebilir. NetX Duo SNTP Istemcisinde bir NTP zamanına yıl, ay, tarih ve saat dönüştürme API 'SI yoktur. NTP saat biçiminin açıklaması için, *RFC4330 "IPv4, IPv6 ve OSI Için basit ağ zaman Protokolü (SNTP) sürüm 4* ' e bakın.

SNTP Istemcisi başladığında temel bir yerel saat sağlanmazsa, SNTP Istemcisi ilk güncelleştirmedeki yerel saatine göre, SNTP güncelleştirmelerini kabul eder. Bundan sonra, kendi yerel saatini değiştirip değiştirmediğine göre, en yüksek ve en düşük zaman güncelleştirme değerlerini uygular.

Uygulama, SNTP Istemci yerel saatini elde etmek için *nx_sntp_client_get_local_time_extended* hizmetini kullanabilir.

### <a name="sntp-sanity-checks"></a>SNTP Sanity denetimleri 

Istemci, aşağıdaki ölçütler için gelen paketi inceler:

  - Kaynak IP adresi geçerli sunucu IP adresi ile aynı olmalıdır.

  - Gönderen kaynak bağlantı noktası, geçerli sunucu kaynağı bağlantı noktasıyla eşleşmelidir.

  - Paket uzunluğu, bir SNTP zaman iletisini tutacak en düşük uzunluk olmalıdır.

Sonra, zaman verileri Istemcinin daha sonra belirli bir ' Sanity denetimleri ' kümesi uyguladığı paket arabelleğinden ayıklanır:

  - 3 olarak ayarlanan artık gösterge, sunucunun eşitlenmediğini gösterir. Istemci alternatif bir sunucu bulmayı denemelidir.

  - Sıfıra ayarlanmış bir katman alanı, bir KISS ölüm (kod) paketi olarak bilinir. Bu durum için SMTP Istemci KOD işleyicisi, Kullanıcı tanımlı bir geri çağırmasıdır. Küçük örnek Tanıtım dosyası, bu durum için basit bir KOD işleyicisi içerir. Başvuru KIMLIĞI alanı isteğe bağlı olarak, kod yanıtının nedenini belirten bir kod içerir. Herhangi bir hızda, KOD işleyicisi, SNTP sunucusundan bir KISS 'nin bir ölüm alma işlemlerinin nasıl yapılacağını belirtmelidir. Genellikle, SNTP Istemcisini başka bir SNTP sunucusuyla yeniden başlatmak isteyeceksiniz.

  - Sunucu SNTP sürümü, katman ve işlem modu istemci hizmetiyle eşleşmelidir.

  - Istemci, sunucu saati dağılım üst sınırı ile yapılandırıldıysa Istemci, yalnızca alınan ilk güncelleştirmede sunucu saati dağılımı denetler ve Istemci en yüksek değerini aşarsa, Istemci sunucuyu reddeder.

  - Sunucu zaman damgası alanları da belirli denetimleri iletmelidir. Tek noktaya yayın sunucusu için, tüm zaman alanları doldurulmalıdır ve NULL olamaz. Özgün zaman damgası, Istemcinin SNTP zaman ileti isteğindeki Iletim zaman damgasına eşit olmalıdır. Bu, Istemciyi kötü amaçlı saldırganlar ve standart dışı sunucu davranışından korur. Yayın sunucusu yalnızca Iletme zaman damgasını doldurmanız gerekir. Istemciden hiçbir şey almadığından, doldurulacak alma veya alma alanı yoktur.

    Başarısız bir sağlamlık denetimi, zaman güncelleştirmesini geçersiz bir saat güncelleştirmesi olarak markalımıştır. SNTP Istemci tasdikliği denetim hizmeti, aynı sunucudan alınan ardışık geçersiz zaman güncelleştirme sayısını izler.

SNTP Istemci iş parçacığı görevi, yerel SNTP Istemci zamanına uygulama için bir SNTP paketinin geçerliliğini denetlediğinde, SNTP Istemcisinin sayısını artırır ve `nx_sntp_client_invalid_time_updates.` Bu da çağırana bir hata durumu döndürür ancak bu, tüm iç işleme olur, böylece uygulama için hemen görünür olmaz. Başarısız zaman güncelleştirmelerini algılamanın yolu, `nx_sntp_client_invalid_time_updates` SNTP sunucu zamanı güncelleştirmelerini aldıktan sonra SNTP istemcisinin değerini sorgulamadır.

Sunucu saati güncelleştirmesi, tasdiklik denetimlerini geçerse Istemci, zaman verilerini yerel saatine göre işlemeye çalışır. Istemci, gidiş dönüş hesaplaması için yapılandırılmışsa, örneğin bir güncelleştirme isteği bir kez alındığında, gidiş dönüş süresi hesaplanır. Bu değer durur ve sunucunun saatine eklenir.

Bundan sonra, geçerli SNTP sunucusundan alınan ilk güncelleştirmedir, SNTP Istemcisi sunucu ile Istemci yerel saati arasındaki farkı yoksayıp saymasının gerekip gerekmediğini belirler. Bundan sonra, SNTP sunucusundan gelen tüm güncelleştirmeler Istemci yerel saatine göre farklılık olarak değerlendirilir.

Istemci ile sunucu saati arasındaki fark ile karşılaştırılır `NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT` . Bu değeri aşarsa, veriler oluşturulur. Fark, fark nedeniyle daha küçükse, `NX_SNTP_CLIENT_MIN_TIME_ADJUSTMENT` ayarlama gerektirecek kadar küçük olarak değerlendirilir.

Tüm bu denetimleri geçirerek, zaman güncelleştirme, SNTP Istemcisine, iç SNTP Istemci işlemede gecikme için bazı düzeltmeler ile uygulanır.

### <a name="sntp-asynchronous-unicast-requests"></a>SNTP zaman uyumsuz tek noktaya yayın Istekleri 

SNTP Istemcisi, ana bilgisayar uygulamasının NTP sunucusundan geçerli saate yönelik zaman uyumsuz bir tek noktaya yayın isteği göndermesini sağlar.

```C
UINT _nx_sntp_client_request_unicast_time(
NX_SNTP_CLIENT *client_ptr, 
UINT wait_option)
```

Bekle seçeneği, yanıt için beklenecek süre sonu ' dur.

NTP sunucusu yanıt verirse, paket, SNTP Istemci yerel saatini güncelleştirmeden önce, önceki bölümde açıklandığı gibi aynı işleme ve tasity denetimlerine tabi.

Çağrı başarılı tamamlamayı döndürürse, uygulama güncelleştirilmiş yerel saat için *nx_sntp_client_utility_display_date_time* veya *nx_sntp_client_get_local_time_extended* çağırabilir.

Bu tek noktaya yayın istekleri, sonraki tek noktaya yayın isteğini göndermek için normal SNTP Istemci zamanlamasını veya yayın modunda, sonraki NTP yayınını ne zaman bekleeceğini engellemez.

### <a name="periodic-local-time-updates"></a>Düzenli yerel saat güncelleştirmeleri

NX_SNTP_CLIENT_MAX_TIME_ADJUSTMENT seçeneğinde (milisaniye olarak), yerel saate göre en yüksek ayarlama ayarlanır. Tek noktaya yayın SNTP Istemci işlemleri için yoklama güncelleştirme aralığı NX_SNTP_CLIENT_UNICAST_POLL_INTERVAL seçeneğinde ayarlanır (saniye cinsinden). Yoklama aralığı, en yüksek ayarlamadan büyükse, ilk sunucu güncelleştirmesinden sonra sonraki sunucu güncelleştirmeleri reddedilir. Bunu engellemek için, SNTP Istemcisi, düzenli aralıklarla NX_SNTP_UPDATE_TIMEOUT_INTERVAL olarak tanımlanan yerel saati güncelleştirir. 

Panonuz RTC ve sunucu saati (SNTP Istemci yerel saatinin olarak ayarlanması gereken) arasında bir fark varsa, RTC 'nin SNTP Istemci saatine eşitilmesi gerekir (bu kullanıcı kılavuzunda bu işlemi göstermemelisiniz).

SNTP sunucu güncelleştirmeleri saat başına birden çok kez gerçekleşmediğinden, SNTP Istemcisinin sunucu güncelleştirmeleri veya sunucu durumu için bu değerden daha sık olarak yoklanmasından çok yararlı değildir. Ancak, SNTP Istemcisinin, en yüksek zaman ayarlama parametresinden NX_SNTP_CLIENT_MAX_TIME_LAPSE daha fazla düşmemek için, kendi yerel saatini genellikle güncelleştirmesi gerekir.

Alternatif olarak, en yüksek ayarlama NX_SNTP_CLIENT_MAX_TIME_LAPSE tek noktaya yayın yoklama güncelleştirmesinden (veya beklenen yayın aralıklarıyla) daha büyük olarak ayarlanabilir. İkinci, bağımsız bir gerçek zaman saatinin gereksinimini ortadan kaldırır. Ancak, SNTP protokolünün amacı yerel RTC veya ağ zaman güncelleştirmelerinde toplam güvenüyi önlemek için kullanılır. Diğer bir deyişle, SNTP sunucu güncelleştirmeleri yerel saat düzeninde DRFT 'i engellemeye yöneliktir.

## <a name="multiple-network-interfaces"></a>Birden çok ağ arabirimi

NetX Duo SNTP Istemcisi, bu ağlar IP örneğiyle kaydedildiği sürece ikincil ağlarda çalışacak şekilde yapılandırılabilir. İkincil ağların nasıl kaydedileceği hakkında daha fazla bilgi için bkz. NetX Duo veya NetX Kullanıcı Kılavuzu.

*Nx_sntp_client_create* çağrısında, üçüncü girişi IFACE_INDEX, SNTP istemcisinin zaman güncelleştirmelerini alacağı ağ dizinine ayarlayın. Birincil arabirim her zaman dizin 0 ' dır. NetX Duo SNTP Istemcisi, aynı anda birden çok ağ arabirimindeki zaman güncelleştirmelerini desteklemez.

## <a name="sntp-and-ntp-rfcs"></a>SNTP ve NTP RFC 'Leri

NetX Duo SNTP istemcisi, IPv4, IPv6 ve OSı için RFC4330 "basit ağ zaman Protokolü (SNTP) sürüm 4" ve ilgili RFC 'Ler ile uyumludur.