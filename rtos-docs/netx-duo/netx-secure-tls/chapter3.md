---
title: Bölüm 3-Azure RTOS NetX güvenliği için Işlevsel açıklama
description: Bu bölüm, NetX güvenli TLS 'nin işlevsel bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c28ad0255f99986a4ddfe5faefad81e70840e5e0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825685"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-secure"></a>Bölüm 3-Azure RTOS NetX güvenliği için Işlevsel açıklama

## <a name="execution-overview"></a>Yürütmeye genel bakış

Bu bölümde, Azure RTOS NetX güvenli TLS 'nin işlevsel bir açıklaması bulunmaktadır. NetX güvenli TLS uygulamasında iki birincil program yürütme türü vardır: başlatma ve uygulama arabirimi çağrıları. 

*NetX güvenli, ThreadX ve NetX/NetXDuo 'un varlığını varsayar. ThreadX ' ten, iş parçacığı yürütme, askıya alma, dönemsel zamanlayıcılar ve karşılıklı dışlama olanakları gerekir. NetX/NetXDuo 'ten TCP/IP ağ tesislerini ve sürücülerini gerektirir.*

## <a name="transport-layer-security-tls-and-secure-sockets-layer-ssl"></a>Aktarım Katmanı Güvenliği (TLS) ve Güvenli Yuva Katmanı (SSL)

NetX güvenli ağ protokolü bileşeni, RFC 2246 (sürüm 1,0), 4346 (sürüm 1,1), 5246 (sürüm 1,2) ve 8446 (sürüm 1,3) bölümünde açıklandığı gibi Aktarım Katmanı Güvenliği (TLS) protokolünün bir uygulamasıdır. Ayrıca temel X. 509.440 (RFC 5280) için destek yordamları da mevcuttur.

NetX güvenli TLS, 1,2 ve 1,3 TLS sürümlerini destekler. Uygulamalar, şimdi kullanımdan kaldırılan TLS 1,0 ve TLS 1,1 için sağlanır, ancak açık bir şekilde başlatılmalı ve yeni ürünlerde kullanılması önerilmez.

*Güvenli Yuva Katmanı* (SSL), RFC 2246 ' de standart hale gelmeden önce TLS adının özgün adı ve "SSL" genellikle TLS protokolleri için genel bir ad olarak kullanılır. SSL 'nin son sürümü 3,0 idi ve TLS 1,0 bazen SSL sürüm 3,1 olarak adlandırılır. Resmi "SSL" protokolünün tüm sürümleri artık kullanılmıyor ve güvenli olmayan olarak kabul edilir ve şu anda NetX güvenli bir SSL uygulamasını sağlamıyor.

TLS, TLS istemcisi ile sunucu arasındaki TLS *el sıkışması* sırasında oluşturulan *oturum anahtarları* oluşturmak için bir protokol BELIRTIR ve bu anahtarlar TLS oturumu sırasında uygulama tarafından gönderilen verileri şifrelemek için kullanılır *.*

TLS verileri, bir TCP paketine yönelik kavramla eşdeğer olan *kayıtlara* ayrılmıştır. Her TLS kaydı bir üst bilgiye sahiptir ve TLS şifreli kayıtlarının de bir altbilgisi vardır (sağlama toplamı karması). TLS el sıkışma kayıtları, daha büyük TLS kaydı içinde kapsüllenmiş ek bir üstbilgiye sahiptir. TLS kaydı, aktarım katmanı ağ protokolü tarafından bir TCP paketinin bir IP paketiyle kapsüllendiği şekilde kapsüllenir.

### <a name="tls-13"></a>TLS 1,3

Ağustos 2018 ' de, TLS 1,3 belirtimi sonlandırılmıştı. Protokolün yeni sürümü, TLS 'nin temel güvenlik ve performansının bazı temel yönlerini değiştiren oldukça önemli bir güncelleştirmedir. Ancak, bu değişiklikler genellikle TLS el sıkışma durum makinesine ve oturum anahtarı oluşturmaya uygulandıklarından tipik TLS kullanıcısına büyük ölçüde görünmez. Birçok isteğe bağlı özellik ve uzantı de eklenmiştir. Aşağıda, değişikliklerin bir özeti ve TLS işlevlerini nasıl etkilediği gösterilmiştir.

- El Sıkışma durumu makinesi, tüm ileti değişimini sunucu tarafından kaldırarak iyileştirildi.
- Anahtar oluşturma, HKDF (HMAC tabanlı anahtar türetme Işlevi) adlı standartlaştırılmış bir yordamı kullanacak şekilde güncelleştirildi ve oturum anahtarlarını tüm el sıkışma iletilerine (birkaç Select parametresi yerine) bağlıdır.
- Tüm TLS 1,2 ve önceki ciphersuites kullanım dışıdır ve TLS 1,3 ile uyumsuzdur. Benzer şekilde, tüm TLS 1,3 ciphersuites, önceki sürümlerle kullanılamaz.
- Tüm TLS 1,3 ciphersuites, kısa ömürlü anahtarlar kullanarak kusursuz Iletme gizliliği (PFS) sağlar<sup>6</sup> 
- TLS 1,3, AEAD<sup>7</sup> şifrelemeleri kullanarak her bir kayıttaki "ileti kimlik doğrulama kodunu" (Mac) kaldırır
- Uygulama verilerinin el sıkışma sırasında gönderilmesini sağlayan 0-RTT (sıfır gidiş dönüş süresi) dahil olmak üzere bazı ek isteğe bağlı özellikler eklenmiştir. 0-RTT yalnızca isteğe bağlıdır ve Azure RTOS TLS 'de Şu anda desteklenmemektedir.

TLS 1,3, Kullanıcı uygulamalarını önemli ölçüde etkilemez. API, sürümler arasında tam olarak aynı kalır ve ciphersuites, tek bir ciphersuite tablosu kullanılabilir olacak şekilde işaretlenir.

TLS 1,3 kullanmak için makro NX_SECURE_TLS_ENABLE_TLS_1_3 genel olarak tanımlanmış olmalıdır. TLS 1,3, Azure RTOS TLS 'de varsayılan olarak devre dışıdır.

6. "Kısa ömürlü" anahtarlar, TLS el sıkışması sırasında oluşturulan ve yalnızca bu oturum için gizli dizi değişim için kullanılan asimetrik anahtar çiftleridir. Bu anahtar çifti kullanıldıktan sonra atılır. Bu, bir saldırganın, bir sertifika özel anahtarı ileride, "kusursuz Iletme gizliliği" ile aynı anda tehlikede olsa, kayıtlı bir TLS oturumunda şifrelenmiş verilere erişmesini önler.

7. Ilişkili verilerle kimliği doğrulanmış şifreleme – tek bir işlemde şifreleme ve bütünlük denetimini birleştiren AES gibi şifrelemeler için bir mod; bütünlük denetimi için verilerin ayrı bir karması gereksinimini ortadan kaldırır.

### <a name="tls-record-header"></a>TLS kayıt üstbilgisi

Geçerli bir TLS kaydı, hata bölümünde gösterildiği gibi bir TLS başlığına sahip olmalıdır! Başvuru kaynağı bulunamadı.

![Bir TLS kayıt üstbilgisinin diyagramı.](media/image2.png)

Şekil 1-TLS kayıt üstbilgisi

TLS kayıt üstbilgisinin alanları aşağıdaki gibi tanımlanır:

| TLS üst bilgi alanı | Amaç     |
| ---------------- | ------------- |
| **8 bit Ileti türü** | Bu alan, gönderilmekte olan TLS kaydının türünü içerir. Geçerli türler şunlardır:<br />-Changecçözülemez spec<sup>8</sup>: 0x14<br />-Uyarı: 0x15<br />-Handshake: 0x16<br />-Uygulama verileri: 0x17 |
| **16 bit protokol sürümü** | Bu alan TLS protokol sürümünü içerir. Geçerli değerler aşağıdaki gibidir:<br />-SSL 3,0:0x0300<br />-TLS 1,0:0x0301<br />-TLS 1,1:0x0302<br />-TLS 1,2:0x0303<br />- **TLS 1,3 <sup>9</sup>**: **0x0303** |
| **16 bit uzunluğu** | Bu alan, TLS kaydında Kapsüllenen verilerin uzunluğunu içerir. |

8. TLS 1,3 ' de Changeclerspec iletisi artık kullanılmamaktadır, ancak yine de ileti yok sayılır, bu durumda uyumluluk nedenleriyle gönderilebilir.

9. TLS 1,3, bu düzen devam ettirmeye devam etseydi, ancak protokol bir uzantıdaki gerçek protokol sürümüne sahip olacak şekilde değiştirildiyse, TLS 1,3 kayıtları geriye dönük uyumluluk için protokol sürümü alanlarında 0x0303 kullanır.

### <a name="tls-handshake-record-header"></a>TLS el sıkışma kayıt üstbilgisi

Geçerli bir TLS el sıkışma kaydı, Şekil 2 ' de gösterildiği gibi bir TLS Handshake üst bilgisine sahip olmalıdır.

![TLS el sıkışma kayıt üstbilgisinin diyagramı.](media/image3.png)

Şekil 2-TLS el sıkışma kayıt üstbilgisi

TLS el sıkışma kayıt üstbilgisinin alanları aşağıdaki gibi tanımlanır:

| TLS üst bilgi alanı | Amaç |
| ---------------- |----------------------- |
| **8 bit Ileti türü** | Bu alan, gönderilmekte olan TLS kaydının türünü içerir. Geçerli türler şunlardır:<br />-Changecçözülemez spec<sup>10</sup>: 0x14<br />-Uyarı: 0x15<br />-Handshake: 0x16<br />-Uygulama verileri: 0x17 |
| **16 bit protokol sürümü** | Bu alan TLS protokol sürümünü içerir. Geçerli değerler aşağıdaki gibidir:<br />-SSL 3,0:0x0300<br />-TLS 1,0:0x0301<br />-TLS 1,1:0x0302<br />-TLS 1,2:0x0303<br />- **TLS 1,3 <sup>11</sup>**: **0x0303** |
| **16 bit uzunluğu**    | Bu alan, TLS kaydında Kapsüllenen verilerin uzunluğunu içerir. |
| **8 bit el sıkışma türü** | Bu alan, el sıkışma ileti türünü içerir. Geçerli değerler aşağıdaki gibidir (*, 1,3 ile **yazılan** iletiler TLS ' ye eklenmiştir):<br />-Merhaba Istek: 0x00<br />-ClientHello: 0x01<br />-ServerHello: 0x02<br />- **Helloverifyrequest**: **0x03**<br />- **Newsessionbilet**: **0x04**<br />- **Endoyuma verileri**: **0x05**<br />- **EncryptedExtensions**: **0x08**<br />-Sertifika: 0x0B<br />-ServerKeyExchange: 0x0C<br />-CertificateRequest: 0x0D<br />-ServerHelloDone: 0x0E<br />-CertificateVerify: 0x0F<br />-ClientKeyExchange: 0x10<br />-Tamamlandı: 0x14<br />- **KeyUpdate**: **0x18**<br />- **Messagehash**: **0xFE** |
| **24 bit uzunluğu**    | Bu alan, el sıkışma ileti verilerinin uzunluğunu içerir. |

10. TLS 1,3 ' de Changeclerspec iletisi artık kullanılmamaktadır, ancak yine de ileti yok sayılır, bu durumda uyumluluk nedenleriyle gönderilebilir.

11. TLS 1,3, bu düzen devam ettirmeye devam etseydi, ancak protokol bir uzantıdaki gerçek protokol sürümüne sahip olacak şekilde değiştirildiyse, TLS 1,3 kayıtları geriye dönük uyumluluk için protokol sürümü alanlarında 0x0303 kullanır.

### <a name="the-tls-handshake-and-tls-session"></a>TLS el sıkışma ve TLS oturumu

Şekil 3 ' te tipik bir TLS anlaşması (sürüm 1.0-1.2) gösterilmektedir. TLS Istemcisi bir TLS sunucusuna bir *ClientHello* iletisi gönderdiğinde TLS el sıkışması başlar ve bunu bir TLS oturumu başlatmak zorunda olduğunu gösterir. İleti, istemci oturum için kullanmak istediğiniz şifreleme hakkında bilgiler içerir ve bu da oturum anahtarlarını daha sonra el ile oluşturmak için kullanılan bilgilerle birlikte. Oturum anahtarları üretilene kadar, TLS el sıkışmasındaki tüm iletiler şifrelenmez. TLS 1,3 el sıkışmasını değiştirir. Ayrıntılar sonraki bölümde sunulmaktadır.

TLS sunucusu, istemci tarafından sunulan şifreleme seçeneklerinden seçim gösteren bir ServerHello iletisi ile ClientHello 'e yanıt verir. ServerHello, sunucunun kimliğini istemciye kimliğini doğrulamak için dijital bir sertifika sağladığı bir sertifika iletisi tarafından izlenir. Son olarak, sunucu gönderilecek daha fazla ileti olmadığını göstermek için bir ServerHelloDone iletisi gönderir. Sunucu isteğe bağlı olarak Sunucushello 'yu izleyen diğer iletileri gönderebilir ve bazı durumlarda bir sertifika iletisi gönderemeyebilir ve bu nedenle ServerHelloDone iletisine gerek kalmaz.

İstemci tüm sunucu iletilerini aldıktan sonra, oturum anahtarlarını oluşturmak için yeterli bilgiye sahip olur. Bu, sabit boyutlu olan ve şifreli olmayan *gizli* anahtar olarak adlandırılan ve şifreleme etkinleştirildikten sonra gereken tüm anahtarları oluşturmak için çekirdek olarak kullanılan, paylaşılan bir rastgele veri adı oluşturarak bunu yapar. Asıl ön gizlilik, Merhaba iletilerde belirtilen ortak anahtar algoritması (ör. RSA) kullanılarak şifrelenir (ortak anahtar algoritmaları hakkında bilgi için aşağıya bakın) ve sertifikasında sunucu tarafından sağlanmış ortak anahtar. Önceden paylaşılan anahtarlar (PSK) adlı isteğe bağlı bir TLS özelliği, bir sertifika kullanmayan cipherpaketlerine izin verebilir, bunun yerine ana bilgisayarlar arasında paylaşılan bir gizli değer (genellikle fiziksel aktarım veya diğer güvenli yöntem aracılığıyla) kullanır. Paylaşılan gizlilik, ana ön gizliliği göndermek için şifrelenmiş bir ileti kullanmak yerine, önceden ana gizli dizi oluşturmak için kullanılır. Aşağıdaki önceden paylaşılan anahtarlar hakkında bölümüne bakın.

Şifrelenmiş ön ana gizli anahtar, ClientKeyExchange iletisindeki sunucusuna gönderilir. Sunucu, ClientKeyExchange iletisini aldıktan sonra, özel anahtarını kullanarak ana ön parolanın şifresini çözer ve oturum anahtarlarını TLS istemcisiyle paralel olarak oluşturmaya devam eder.

Oturum anahtarları oluşturulduktan sonra, diğer tüm iletiler, Merhaba iletilerde seçili olan özel anahtar algoritması (ör. AES) kullanılarak şifrelenir. Diğer tüm iletilerin şifrelendiğini belirtmek için hem istemci hem de sunucu tarafından, Changeccrypspec adlı bir son şifreli ileti gönderilir.

Hem istemci hem de sunucu tarafından gönderilen ilk şifreli ileti ayrıca, tamamlandı olarak adlandırılan son TLS el sıkışma iletisidir. Bu ileti alınan ve gönderilen tüm el sıkışma iletilerinin karmasını içerir. Bu karma, el sıkışmasının hiçbir iletiden değiştirilmediğini veya bozulmadığını (güvenlik ihlali olasılığı olduğunu gösterir) doğrulamak için kullanılır.

Tamamlanan iletiler alındıktan ve el sıkışma karmaları doğrulandıktan sonra, TLS oturumu başlar ve uygulama veri göndermeye ve almaya başlar. TLS oturumu sırasında her iki taraf tarafından gönderilen tüm veriler ilk olarak, oluşturulan oturum anahtarlarına sahip seçili özel anahtar algoritması kullanılarak, Merhaba iletilerde seçilen karma algoritma kullanılarak (ileti bütünlüğü sağlamak için) ve şifreli olarak şifrelenir.

Son olarak, bir TLS oturumu yalnızca Istemci veya sunucu bunu yapmayı seçerse başarılı bir şekilde sonlandırgirebilir. Kesilen oturum, bir güvenlik ihlali olarak değerlendirilir (bir saldırgan tüm verilerin alınmasını engellemeye çalışıyor olabilir), bu nedenle her iki taraf da oturumu sonlandırmak istediğinde, bir CloseNotify uyarısı olarak adlandırılan özel bir bildirim gönderilir. Başarılı bir oturum kapatması için hem istemci hem de sunucu bir CloseNotify uyarısı göndermelidir ve işlemelidir.

![Tipik bir TLS el sıkışma diyagramı.](media/image4.png)

Şekil 3-tipik TLS el sıkışması

### <a name="tls-13-handshake"></a>TLS 1,3 el sıkışma

TLS 1,3, TLS protokolünün oldukça büyük bir fazla yer taşıdır. Güvenlik ve performansı artırmak için el sıkışma üzerinde yapılan değişikliklerin büyük çoğunluğu yapılmıştır. Şekil 4 ' te tipik bir TLS 1,3 anlaşması gösterilmektedir. Birincil fark, sunucu ve istemci arasındaki değişim sayısında görülebilir.

TLS 1,2 ve önceki sürümlerde, sunucu iki adet fışıkla<sup>12</sup> ileti gönderir: Ilk olarak serverhello ve ardından bir changeccrypspec iletisi göndererek el sıkışmasını sonlandıran şifreli tamamlanmış iletiyi göndermeden önce. TLS 1,3 ' de, sunucu her şeyi ilk uçuşa – ServerHello, Extensions, Certificate ve finished olarak gönderir. Changecrelaspec iletisi çıkarıldı ve sunucu oturum anahtarlarını oluşturur ve Sunucuhello sonrasında el sıkışma iletilerini şifrelemeyi başlatır.

Yeni düzenleme, bir saldırganın erişebileceği düz metin veri miktarını sınırlayarak TLS el sıkışmasının daha fazla şifreleme ile korunduğu anlamına gelir. Buna ek olarak, ikinci sunucu uçuş işleminin (yalnızca bir Changecbir özellik olan) kaldırılması, bir TLS istemcisinin artık uygulama verilerini iletmeye başlamasını beklemek zorunda olmadığı anlamına gelir. Bu, istemci kendi tamamlanmış iletisini gönderdiğinde oturum başlatılır.

12. Uçuş, tek bir grupta aynı anda gönderilen TLS iletileri koleksiyonudur.

![TLS 1,3 el sıkışma diyagramı.](media/image5.png)

Şekil 4-TLS 1,3 el sıkışma

> [!NOTE]
> *TLS 1,3 Ayrıca, bazı uygulama verilerinin ilk ileti uçuşunda gönderilebileceği anlamına gelen "erken veri" ve 0-RTT (sıfır gidiş dönüş süresi) kavramını ortaya sunmuştur. Bu isteğe bağlı özellik öncelikle web tarayıcısı yanıt verme iyileştirmesi (örn. bir sayfa işlemeye başlamak için erken HTTP üstbilgileri göndermek için) olarak eklenmiştir. Azure RTOS 6,0 itibariyle bu özellik desteklenmez.*

### <a name="initialization"></a>Başlatma

NETX güvenli TLS kullanılmadan önce NetX veya NetXDuo TCP/IP yığınının başlatılması gerekir. TCP/IP yığınını düzgün bir şekilde başlatma hakkında bilgi için NetX veya NetXDuo Kullanıcı kılavuzuna bakın.

NetX TCP/IP yığını başlatıldıktan sonra, TLS etkinleştirilebilir. Dahili olarak, tüm TLS ağ trafiği ve işleme, Kullanıcı müdahalesi gerektirmeden NetX/NetXDuo Stack tarafından işlenir. Ancak, TLS, temel ağ yığınından ayrı olarak işlenmesi gereken bazı özel gereksinimlere sahiptir. Bu parametreler _ *_nx_secure_tls_session_create_** hizmeti kullanılarak ***NX_SECURE_TLS_SESSION** _ adlı TLS denetim bloğuna atanır.

TLS, iki mod, sunucu ve Istemciye sahiptir, bunlardan biri bir uygulamada etkinleştirilebilir (ancak NetX yuvası başına yalnızca bir mod) ve her biri aşağıda ayrıntılı şekilde kendi özel gereksinimlerine sahiptir.

Her iki modda da NetX güvenli TLS, uzak ana bilgisayar ile bir TCP yuvası (***NX_TCP_SOCKET** _) OLUŞTURULMASıNı ve TCP iletişimleri için ayarlanmasını gerektirir. TCP yuvası, aşağıda ayrıntılı olarak açıklanan _ *_nx_secure_tls_session_start_** HIZMETIYLE bir TLS oturum örneğine atanır.

### <a name="initialization--tls-server"></a>Başlatma – TLS sunucusu

Bir TCP yuvasına ek olarak, NetX güvenli TLS sunucu modu, bağlanan TLS istemcisine TLS sunucusunu tanımlamak için kullanılan bir belge olan *dijital bir sertifika* ve genellikle RSA şifreleme algoritması için karşılık gelen *özel anahtarı* sertifikalar gerektirir. International Telekomünikasyon Birliği X. 509.440 standart, TLS tarafından kullanılan sertifika biçimini belirtir ve X. 509.952 dijital sertifikaları oluşturmak için çok sayıda yardımcı program vardır.

NetX güvenli TLS için, X. 509.440 sertifikası ASN. 1 ' in Distinguished Encoding Rules (DER) biçimi kullanılarak ikili kodlanmış olmalıdır. DER, sertifikalar için Standart TLS-kablolu ikili biçimidir.

Belirtilen sertifikayla ilişkili özel anahtar DER-Encoded PKCS # 1 biçiminde olmalıdır. Özel anahtar yalnızca cihazda kullanılır ve hiçbir şekilde kablo üzerinden aktarılmaz. TLS iletişimleri için güvenlik sağlayan özel anahtarları güvende tutun!

TLS sunucu sertifikasını başlatmak için, uygulamanın, _ *NX_SECURE_X509_CERT** yapısını TLS tarafından kullanılmak üzere uygun sertifika verileriyle dolduran, der kodlu X. 509.952 sertifikasını ve Isteğe bağlı der kodlu PKCS # 1 RSA özel anahtar **nx_secure_x509_certificate_intialize** verilerini içeren bir arabellek işaretçisi sağlaması gerekir.

Sunucu sertifikası başlatıldıktan sonra, ***nx_secure_tls_local_certificate_add*** HIZMETI kullanılarak TLS denetim bloğuna eklenmelidir.

Sunucunun sertifikası TLS denetim bloğuna eklendikten sonra, yuva güvenli bir TLS sunucu bağlantısı kurmak için kullanılabilir.

### <a name="initialization--tls-client"></a>Başlatma – TLS Istemcisi

NetX güvenli TLS Istemci modu, güvenilen sertifika yetkililerinden (CA 'lar) bulunan X. 509.440 kodlu dijital sertifikaların bir koleksiyonu olan *Güvenilen bir sertifika deposu* gerektirir. Bu sertifikalar TLS protokolünün "güvenilir" olarak kabul edilir ve TLS sunucu varlıkları tarafından belirtilen sertifikaların kimliğini NetX güvenli TLS Istemcisine doğrulamak için temel olarak görev yapar.

Güvenilen CA sertifikası, başka bir CA tarafından *otomatik olarak imzalanmış* veya imzalı olabilir, bu durumda sertifikaya BIR *ara CA* (ICA) denir. Tipik bir TLS uygulamasında sunucu, sunucu sertifikasıyla birlikte ICA sertifikalarını sağlar, ancak başarılı kimlik doğrulaması için tek gereksinim, sunucu sertifikasından güvenilen sertifika deposundaki güvenilir bir CA sertifikasına geri doğru bir şekilde izlenebilir. Bu zincir bir  *güven zinciri* veya *sertifika zinciri* olarak bilinir.

Güvenilen bir CA veya ICA sertifikası başlatmak için, uygulamanın, _ *NX_SECURE_X509_CERT** yapısını TLS tarafından kullanılmak üzere uygun sertifika verileriyle dolduran, ***nx_secure_x509_certificate_intialize** _ hizmetini kullanarak der kodlu X. 509.440 sertifikasını içeren bir arabellek işaretçisi sağlaması gerekir.

Başlatılmış olan güvenilen sertifikalar, ***nx_secure_tls_trusted_certificate_add*** HIZMETI kullanılarak TLS denetim bloğuna eklenir. Bir sertifika eklenemedi TLS Istemci oturumunun başarısız olmasına neden olur, çünkü TLS protokolünün uzak TLS sunucu konaklarının kimliğini doğrulamak için bir yol olmayacaktır.

TLS Istemcisinde Ayrıca gelen sunucu sertifikasının ayrılması için alan gerekir (önceden paylaşılan bir anahtar modunun kullanılmakta olduğu varsayılırsa). NetX güvenli TLS 5,12 itibariyle, uygulamanın uzak sertifika için alan ayırması artık gerekli değildir. Ancak, bir sunucu sertifikası için alan ayırma eski seçeneği hala kullanılabilir ve iç sertifika arabelleği en iyi duruma getirme <sup>13</sup> ' den önce Kullanıcı tarafından ayrılan sertifikalar kullanılır. daha fazla bilgi için ***nx_secure_tls_remote_certificate_allocate*** hizmetine bakın.

Güvenilen sertifika deposu oluşturulduktan ve sunucu sertifikası için alan ayrıldıktan sonra, yuva güvenli bir TLS Istemci bağlantısı kurmak için kullanılabilir.

13. İyileştirme, daha önce NetX güvenli TLS 'in daha önceki sürümlerinde kullanılan Kullanıcı tarafından sağlanan yapıları kullanmak yerine, Kullanıcı uygulaması tarafından TLS *nx_secure_tls_session_packet_buffer_set* oturumuna tarafından sağlanan "paket arabelleğini" kullanır. Paket arabelleğinin boyutunu aşan bir sertifika zinciri, paket arabelleği boyutu artmış olabilir veya *nx_secure_tls _remote_certificate_allocate* sertifika zinciri için daha fazla alan ayırmak üzere kullanılabilir.

### <a name="application-interface-calls"></a>Uygulama arabirimi çağrıları

NetX güvenli TLS uygulamaları, genellikle ThreadX RTOS altında çalışan uygulama iş parçacıklarının içinden işlev çağrıları yapar. Özellikle temel ağ iletişim protokolleri (örn. TCP ve IP) için bazı başlatma, ***tx_application_define *** öğesinden çağrılabilir. Ağ iletişimlerini başlatma hakkında daha fazla bilgi için bkz. NetX/NetXDuo Kullanıcı Kılavuzu.

TLS, işlemci yoğunluklu işlemler olan şifreleme yordamlarının yoğun bir şekilde kullanılmasını sağlar. Genellikle, bu işlemler çağıran iş parçacığı bağlamında gerçekleştirilir.

### <a name="tls-session-start"></a>TLS oturumu başlatma

TLS, çalışması için temeldeki bir aktarım katmanı ağı Protokolü gerektirir. Genellikle kullanılan protokol TCP 'dir. NetX güvenli bir TLS oturumu oluşturmak için, NetX/NetXDuo TCP API 'SI kullanılarak bir TCP bağlantısı kurulması gerekir. Bir **NX_TCP_SOCKET** oluşturulmalı ve bir bağlantı oluşturulması gerekir **_nx_tcp_server_socket_listen_*_ ve _*_nx_tcp_server_socket_accept_*_ Hizmetleri (TLS sunucusu için) veya _*_nx_tcp_client_socket_connect_** hizmeti (TLS istemcisi için).

TCP bağlantısı kurulduktan sonra, TCP yuvası ***nx_secure_tls_session_start*** hizmetine geçirilir.

### <a name="tls-packet-allocation"></a>TLS paket ayırma

NetX güvenli TLS, _*_nx_packet_allocate_*_ hizmetini çağırmak yerine NETX/NetXDuo TCP (***NX_PACKET** _) ile aynı paket yapısını kullanır. bu nedenle, TLS üstbilgisi için alanın doğru ayrılabileceği şekilde _ *_nx_secure_tls_packet_allocate_** hizmetinin çağrılması gerekir.

### <a name="tls-session-send"></a>TLS oturumu gönderme

TLS oturumu başladıktan sonra uygulama, ***nx_secure_tls_session_send** _ hizmetini kullanarak veri gönderebilir. Gönderme hizmeti, gönderilen verileri içeren bir _*_NX_PACKET_*_ veri yapısı alarak _*_nx_tcp_socket_send_*_ hizmeti için kullanılan özdeş, yalnızca bu veriler GÖNDERILMEDEN önce NX güvenli TLS yığını tarafından şifrelenir ve bu paket _ *_nx_secure_tls_packet_allocate_* * kullanılarak ayrılmalıdır.

### <a name="tls-session-receive"></a>TLS oturum alma

TLS oturumu başladıktan sonra uygulama, ***nx_secure_tls_session_receive** _ hizmetini kullanarak veri almaya başlayabilir. TLS oturumu gönderme gibi, bu hizmet, gelen verilerin, paket yapısına döndürülmeden önce TLS yığını tarafından şifresinin çözülmesi ve doğrulanması dışında _ *_nx_tcp_socket_receive_* * ile aynıdır.

### <a name="tls-session-close"></a>TLS oturumu kapatma

Bir TLS oturumu tamamlandıktan sonra, oturumu kapatmak için hem TLS istemcisi hem de sunucunun diğer tarafa bir CloseNotify uyarısı gönderebilmesi gerekir. Başarılı bir oturumun kapatılmasını sağlamak için her iki taraf da uyarıyı alıp işlemelidir.

Uzak ana bilgisayar bir CloseNotify uyarısı gönderirse, ***nx_secure_tls_session_receive** _ hizmetine yapılan tüm çağrılar uyarıyı işler, karşılık gelen uyarıyı uzak ana bilgisayara geri gönderir ve _ *_NX_SECURE_TLS_SESSION_CLOSED_* * değerini döndürür. Oturum kapatıldıktan sonra, bu TLS oturumuyla veri gönderme veya alma girişimleri başarısız olur.

Uygulama TLS oturumunu kapatmayı istiyorsa, ***nx_secure_tls_session_end** _ hizmeti çağrılmalıdır. Hizmet, CloseNotify uyarısını gönderir ve yanıt CloseNotify 'ı işler. Yanıt alınmıyorsa, TLS oturumunun düzgün kapatılmadığını belirten bir hata değeri olan _ *_NX_SECURE_TLS_SESSION_CLOSE_FAIL_** döndürülür.

### <a name="tls-alerts"></a>TLS uyarıları

TLS, en yüksek güvenliği sağlamak üzere tasarlanmıştır, bu nedenle protokoldeki tüm hatalı davranışlar olası bir güvenlik ihlali olarak kabul edilir. Bu nedenle, ileti işleme veya şifreleme/şifre çözme işlemlerinin her türlü hatası, el sıkışma veya oturumu hemen sonlandıran önemli hatalar olarak değerlendirilir.

Yerel bir uygulamadaki hataların işlenmesi oldukça basittir, uzak Konağın durumu düzgün bir şekilde işlemek ve olası güvenlik ihlallerinin oluşmasını engellemek için bir hata oluştuğunu bilmesi gerekir. Bu nedenle, TLS uzak ana bilgisayara herhangi bir hata üzerine bir *Uyarı* iletisi gönderir.

Uyarılar, diğer TLS iletileriyle aynı şekilde değerlendirilir ve bir saldırganın, belirtilen uyarı türünden bilgi toplamasını engellemek için oturum sırasında şifrelenir. El sıkışma sırasında gönderilen uyarılar, olası bir saldırgan tarafından elde edilen bilgi miktarını sınırlamak için kapsamda sınırlanır.

TLS oturumunu kapatmak için kullanılan CloseNotify uyarısı, önemli olmayan tek uyarıdır. Bir uyarı olarak kabul edildiği ve uyarı iletisi olarak gönderildiği sürece bir CloseNotify, bir hata oluştuğunu belirtmeyen diğer uyarıların aksine.

Uyarı değeri ve "düzey" (düzeyler "uyarı" ve "önemli", TLS uyarıları en çok "önemli"), TLS RFC 'lerde tanımlanmıştır ve oluşan hata türünü gösterir. CloseNotify dışındaki çoğu TLS uyarısı, olası bir güvenlik sorunu göstergesi olarak düşünülebilir ve TLS oturumunun veya el sıkışmasının iptal edilmesine neden olur. Herhangi bir TLS API çağrısı **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) DÖNDÜRÜRSE, apı hizmeti **_Nx_secure_tls_session_alert_value_get_** (NETX güvenli TLS sürüm 5,12 ' de yenidir), güvenlik sorunlarına yönelik yanıtlarla ilgili herhangi bir kararta kullanılacak şekilde, uygulamanın TLS uyarı değerini ve düzeyini almak için kullanılabilir. Çoğu durumda, CloseNotify dışındaki uzak ana bilgisayardan alınan tüm uyarılar önemli bir hata olarak düşünülmelidir, ancak bazı excptions vardır. daha fazla bilgi için bkz. TLS RFC 'Leri.

### <a name="tls-session-renegotiation"></a>TLS oturumu yeniden anlaşması

TLS, mevcut bir TLS oturumu bağlamında yalnızca TLS oturum parametrelerinin yeniden anlaşması olan "yeniden anlaşma" kavramını destekler. Bu yöntem, yeni el sıkışma iletilerinin mevcut oturum kullanılarak şifrelenme ve kimliğinin doğrulanmasıdır. Bir TLS ana bilgisayarı, mevcut oturumu tamamlamaya gerek kalmadan yeni oturum parametreleri (ör. yeni TLS oturum anahtarları oluşturma) oluşturmak istediğinde yeniden anlaşma kullanılır. Örneğin, bir uygulamanın güvenlik ilkeleri yalnızca sınırlı bir süre için kullanıldığında yeniden anlaşma istenebilir, ancak bu sürenin ötesinde bir TLS oturumu etkin kalır.

Oturum yeniden anlaşması ile ilgili bir sorun, bir saldırganın bir sunucuyu yeni parametrelerle yeniden anlaşma başlatmaya ikna edebilmesine ve böylece saldırganın TLS oturumuna izin vermesini sağlayan belirli bir noktadan adam saldırısından yararlanmasına neden olur. Bu sorunu azaltmak için, güvenli yeniden anlaşma gösterge uzantısı eklenmiştir (bkz. bölüm **hatası! Başvuru kaynağı bulunamadı.** Bölüm).

NetX güvenli TLS, oturum yeniden anlaşmasını ve güvenli yeniden anlaşma gösterge uzantısını tamamen destekler.

Uzak bir ana bilgisayardan veri alırken, renegotations (ve Extension), uygulama etkileşimi olmadan otomatik olarak işlenir. Oturum yeniden anlaşması hakkında bildirim istenirse *nx_secure_tls_session_renegotiate_callback_set* hizmetiyle bir yeniden anlaşma geri araması sağlanabilir. Geri çağırma, uzak ana bilgisayar tarafından her yeniden anlaşma istendiğinde, uygulamanın istenirse işlem yapmasına izin vermek için çağrılır.

Etkin bir TLS oturumundan yeniden anlaşma başlatmak için, istenen TLS oturumunda *nx_secure_tls_session_renegotiate* hizmetini çağırmanız yeterlidir.

### <a name="tls-session-resumption"></a>TLS oturum sürdürme

TLS oturum sürdürme, bazı benzerlikler olmasına rağmen oturum yeniden anlaşması ile karıştırılmamalıdır. Oturum yeniden *anlaşması* , mevcut bir TLS oturumunda yeni bir el sıkışma başlatmayı da içerir. oturum *sürdürme* , tam bir TLS el SıKıŞMASı yapmadan kapalı bir TLS oturumunun yeniden başlatılmasını içeren tamamen isteğe bağlı bir özelliktir. Bunu başarmak için bir TLS uygulama, oturum parametreleri ve anahtarlarını önbelleğe alabilir ve bunları bir *oturum kimliğiyle* ilişkilendirerek, özgün el sıkışma içinde sağlanan benzersiz bir tanımlayıcıdır. Bir TLS sunucusuna bir oturum KIMLIĞI sağlayarak, istemci, daha önce konaklar arasındaki önceki bir TLS oturumunun var olduğunu ve bir süre sonra tamamlandığını ve istemcinin daha düşük bir el sıkışması ile oturumu yeniden kurması için hala duruma sahip olduğunu gösterir. Oturum anahtarları teorik olarak hala gizli ve yalnızca iki iletişim kuran ana bilgisayar tarafından bilindiğinden, sunucu yeni bir TLS oturumu başlatabilir ve normal El sıkışmanın çoğunu atlayabilir.

Oturum sürdürme, anahtar oluşturma ana gizliliğini paylaşmak ve sertifika imzalarını doğrulamak için kullanılan, pahalı olabilecek ortak anahtar işlemlerini önlemek için kullanışlı olabilir, ancak aynı zamanda oturum parametreleri, anahtarlar ve crypotgraphic durumunun tüm olası oturumlar için bellekte tutulmasını (en azından yapılandırılabilir bir zaman penceresi için) gerekir.

NetX güvenli TLS 'nin geçerli sürümü Session sürdürme 'ı desteklemez. oturum KIMLIĞI yalnızca TLS sunucuları tarafından yok sayılır ve TLS istemcileri her zaman sunucuya bir el sıkışma gerçekleştirmesini isteyen NULL bir oturum KIMLIĞI sağlar. Oturum sürdürme olmaması, tamamen isteğe bağlı bir özellik olduğundan ve tüm TLS uygulamalarının tam bir el sıkışma olması halinde, oturum KIMLIĞININ NULL veya tanınmayan olması gerekir.

### <a name="protocol-layering"></a>Protokol katmanlama

TLS protokolü, Aktarım Katmanı (örn. TCP) ve uygulama katmanı arasındaki ağ yığınına uyar. TLS bazen bir Aktarım Katmanı Protokolü (Bu nedenle *Aktarım katmanı* güvenliği) olarak kabul edilir, ancak temel ağ PROTOKOLLERIYLE (TCP gibi) ilgili bir uygulama gibi davrandığı için bazen uygulama katmanında gruplandırılmıştır.

TLS, TCP gibi sıralı ve kayıpsız teslimi destekleyen bir aktarım katmanı protokolü gerektirir. Bu gereksinim nedeniyle, UDP veri birimlerinin teslimini garanti edemediğinden TLS UDP üzerinde çalıştırılamaz. TLS 'nin değiştirilmiş bir sürümü olan *DTLS* adlı ayrı bir protokol, UDP gibi bir veri birimi protokolü üzerinden TLS güvenliği gerektiren uygulamalar için kullanılır. NetX güvenliği DTLS 'yi destekler, ancak DTLS belgeleri bu belgeden ayrıdır.

![TCP/IP ve TLS protokol katmanlarının diyagramı.](media/image6.png)

Şekil 5-TCP/IP ve TLS protokol katmanları

## <a name="network-communications-security"></a>Ağ Iletişimi güvenliği

Kamu ağları ve Internet üzerinden iletişimin güvenliğini sağlamak, çok sayıda kitap, makale ve çözüm konusunun önemli öneme sahip bir konudur. Bu konu göz önünde bulundurularak, ancak yalnızca hedeflenen hedefin bu bilgileri erişebileceği veya değiştirebilmesini sağlamak için bir ağ üzerinden bilgi gönderilirken daha kolay bir fikir olabilir. Bu üç önemli kavrama bölünür: Gizlilik, bütünlük ve kimlik doğrulama. TLS protokolü, her üç için çözüm sağlar.

### <a name="secrecy"></a>Gizliliğinin

Ağ üzerinden veri gönderirken genellikle verilerin kötü amaçlı bir varlık tarafından alınmaması önemlidir. Veriler bir TCP/IP bağlantısı üzerinden gönderiliyorsa, ağa erişimi olan herkes, kolayca kullanılabilir ağ araçlarını kullanarak bu verileri okuyabilecektir. Bu verilerin elde edilmesine engel olmak için, hedeflenen hedef tarafından okunamayacak şekilde kodlanmalıdır: Bu Gizlilik *.* TLS 'de, RSA ve AES gibi şifreleme algoritmaları gizliliği sağlar.

### <a name="integrity"></a>Bütünlük

Bazen, gizlilik, ağ üzerinden veri gezini korumak için yeterli değildir. Bazı durumlarda, kötü amaçlı bir varlık bir TCP paketinin içeriğini, paketin neleri içerdiğini bilmeden değiştirmek mümkün olabilir. Şifrelenmiş veriler değiştirilebilir, şifre çözme işlemi geçersiz hale gelebilir veya ileti başındaki parametreler, saldırganın ilgilendiği herhangi bir sonuçla değiştirilebilir. Ağda, bir saldırganın geçiş sırasında verileri değiştirmesini engelleyemedik, ancak verilerin değiştirilip değiştirilmediğini bilen bir mekanizma sağlayabiliriz. Veriler aktarım sırasında değiştirildiğinde, bilinirler ve veriler reddedilebilir. Bu kavram *bütünlüğü*. TLS 'de, bütünlük, *Karma işlevler* olarak bilinen bir şifreleme yordamları sınıfı tarafından sağlanır. Karma işlevlere bazı örnekler MD5 ve SHA-1 ' dir.

### <a name="authentication"></a>Kimlik Doğrulaması

Ağ iletişimi güvenliği açısından üçüncü önemli kavram, verilerin yalnızca amaçlanan hedefe bildirilmesi gerektiğine yönelik bir fikirdir. Saldırgan, başka bir konağa yönelik verileri almak için meşru bir varlık olarak hazırlanmanıza çalışabilir. Veriler, gizliliği ve bütünlük mekanizmalarına sahip olsa bile, saldırgan bu gözden geçir aracılığıyla istenen sonuca (güvenli iletişim güvenliğinin aşılmasına karşı) yine de ulaşabiliyor olabilir. Bunu engellemek için, herhangi bir hassas veri gönderilmeden önce uzak ana bilgisayarın kimliğini kanıtlamak için bir mekanizma gerekir. Bir uzak konağın kimliğini kanıtlama işlemi *kimlik doğrulaması olur.* TLS 'de kimlik doğrulaması, dijital sertifikalar, karma işlevler ve bir ortak anahtar şifreleme özelliğinden yararlanan *dijital imzalar* adlı bir mekanizma (aşağıda açıklanmıştır) kullanılarak sağlanır. Bir *önceden paylaşılan anahtar* (PSK) ile sınırlı ancak yararlı bir kimlik doğrulama biçimi de sağlayabilirsiniz.

## <a name="tls-encryption"></a>TLS şifreleme

TLS protokolü, şifreleme kullanan Internet üzerinden güvenli ağ iletişimleri sağlamaya yönelik bir çerçevedir. Şifreleme genellikle, verileri özgün verileri (veya ilgili veriler hakkındaki bilgileri) elde etmek için bir *anahtar* olmadan bu şekilde bir şekilde kodlama işlemi olarak tanımlanır. Bilgisayar sistemleri şifrelemesi, sınırlı alanlar gibi karmaşık matematik ve iki tür olarak sınıflandırılabilirler: *özel anahtar* (veya *simetrik şifreleme*) ve *ortak anahtar* (veya *asimetrik şifreleme*). Özel anahtar şifreleme örnekleri AES (Gelişmiş Şifreleme Standardı) ve RC4 (Rivest şifre 4). Ortak anahtar şifreleme örnekleri RSA (Rivest, Shamir, Adleson) ve Diffie-Hellman şifrelemeler.

TLS protokolü, performans, güvenlik ve esneklik dengelemesi sağlamak için hem özel anahtar hem de ortak anahtar şifreleme yordamlarını kullanır.

### <a name="private-key-encryption"></a>Private-Key şifreleme

Özel anahtar şifreleme, binlerce yıl boyunca kullanımda. Temel değiştirme şifrelemeleri (bir harf veya sözcük başka bir ilgisiz harf veya Word tarafından değiştirilmiştir) en erken bilinen şifreleme örnekleridir, ancak bilgi yaşı özel anahtar şifrelemesi 'nin bir yandan büyük ölçüde iyileşmesi önerilir.

Özel anahtar şifresi, bazı verileri bir arada kodlamak için kullanılan bir değer olan bir "anahtar" (genel durumda bir sözcük, tümcecik veya sayı olabilir) kullanır. böylece, yalnızca bu anahtara erişimi olan bir varlığın verileri anlamlı bir şekilde çözebilmesini sağlayabilirsiniz. Anahtar, verilerin şifrelenmesi ve şifresinin çözülmesi için kullanılır, bu nedenle diğer ad *simetrik şifreleme*.

Özel anahtar şifrelemeleri genellikle hızlı ve oldukça basittir. Bu, matematik ve ilgili karmaşık bir karmaşıksa bile uygulanır. Bu nedenle TLS, güvenli iletişimler toplu olarak özel anahtar şifrelemeleri kullanır.

Bununla birlikte, genel bilgisayar ağı iletişimine uygulamayı denerken özel anahtar şifrelemesi bir sorunla karşılaştı: anahtarın, iletişim kurmaya çalışan her iki makine arasında paylaşılması gerekir. Genel durumda, ağ trafiğinin Internet üzerinden yönlendirilirken yaptığı çeşitli tür varlıkların herhangi bir sayıda varlık tarafından alınabileceğini varsayabileceği için, Internet 'teki iki makine arasında güvenli bir şekilde iletişim kurmak pratik ve genellikle imkansızdır. Anahtar kötü amaçlı bir varlık tarafından elde edilirse, bu anahtar kullanılarak şifrelenen tüm verilerin güvenliği aşılmış olur. Internet üzerindeki makinelerin çoğu iletişim için yalnızca bir ağ bağlantısına sahip olduğu ve iletişim için başka bir güvenli kanal olmadığından, ağ üzerinden anahtar gönderilmesi, verileri şifrelenmemiş olarak göndermek için bir güvenlik sağlar.

Bu nedenle, özel anahtar şifrelemesi, genel amaçlı bir ağ iletişimi güvenlik protokolü uygulamak için yeterli değildir. Bu, ortak anahtar şifrelemenin yardımcı olabilir.

NetX güvenli TLS, AES özel anahtar şifrelemesini destekler.

### <a name="public-key-encryption"></a>Public-Key şifreleme

Özel anahtar şifrelemenin aksine, ortak anahtar şifrelemesi, 1970 ' te geliştirilen oldukça yeni bir kavramdır. "Tuzak kapısı işlevleri" olarak bilinen bir kavramı kullanarak, daha sonra şifrelenen verilerin güvenliğine güvenmeden bir ağ üzerinde bir anahtar paylaşmanın bir yolu vardı.

Ortak anahtar şifrelemenin çalışma şekli, anahtarın (yukarıda açıklanan özel anahtar şifreleme algılaması) iki parçaya, *özel bir anahtara* *ve ortak anahtara*(ortak anahtar şifrelemeden) göre bölündüğü yerdir. Kavram şifre çözme için kullanıldığında, bu anahtarlardan biri şifreleme için kullanılır (genellikle ortak anahtardır). Bu anahtar asymmetry, ortak anahtar şifrelemesi için diğer adın nedenidir: *asimetrik şifreleme*.

Ortak anahtar şifrelemesi, büyük bir karmaşıkdır, ancak genel anahtar şifreleme için *yalnızca* şifreleme için kullanılabilir ve bu anahtarın, şifrelenmiş verilerin elde etmesine izin vermez. Özel anahtar, sırasıyla ortak anahtar kullanılarak şifrelenmiş verilerin şifresinin çözülmesi için tek yoldur. Bu nedenle, özel anahtar gizliliğini koruyarak, bu özel anahtarın sahibi ile güvenli bir şekilde iletişim kurmak isteyen herkes yalnızca ilgili ortak anahtarla verilerini, yalnızca söz konusu özel anahtarı elinde bulunan birinin güvenli verileri elde edebilir.

NetX güvenli TLS, RSA ortak anahtar şifrelemesini destekler.

> [!IMPORTANT] 
> *RSA, yazılım RSA uygulamasının kullanılması durumunda işlemciyi yoğun bir işlemdir. Daha büyük anahtar boyutları, anahtar boyutunda 2X artışla daha yavaş bir kare faktörü için gereken işlem gücünü artırır.*

### <a name="public-key-authentication"></a>Public-Key kimlik doğrulaması

Ortak anahtar şifreleme kavramının ilgi çekici bir etkisi, işlemi tersten yaparak, kimlik doğrulamanın yanı sıra, *özel* anahtar kullanarak şifreleme ve *ortak* anahtar kullanarak şifre çözme sağlamak için de kullanılabilir. Bunu yapmanın gerçek mekanizması, kullanılan ortak anahtar algoritmasına bağlıdır, ancak kavram aynıdır.

Ortak anahtar kimlik doğrulamasını kullanarak kimlik doğrulaması yapmak için, özel bir anahtarın sahibi, bu özel anahtarı kullanarak bazı veri parçasını (genellikle kimlik doğrulaması yapılacak verilerin bir şifreleme karması) şifreler. Daha sonra, verilerin şifresini çözmek için ilişkili ortak anahtarı kullanır. şifre çözme başarılı olursa ve kullanıcının bu ortak anahtarın geçerliliğini güvenilir kabul edersek, Kullanıcı, verilerin özel anahtar sahibinden geldiğinden emin olabilir ve bu durumda Kullanıcı, verilerin özel anahtarın sahibinden geldiğinden emin olabilir.

TLS 'de ortak anahtar kimlik doğrulaması, güvenilen sertifika deposundan ortak anahtarları kullanarak bir TLS sunucusu (ve isteğe bağlı olarak TLS istemcisi) tarafından belirtilen dijital sertifikanın geçerliliğini doğrulamak için kullanılır. Sertifika, depodaki bir ortak anahtara göre denetlenir ve sertifikadaki veriler sunucunun kimliğini denetlemek için kullanılır.

NetX güvenli TLS, RSA kimlik doğrulamasını destekler.

### <a name="cryptographic-hashing"></a>Şifreleme karması

Şifreleme, TLS 'de kullanılan tek şifreleme işlemi değildir. Bir TLS oturumu sırasında ileti bütünlüğü sağlamak için ileti içeriğinin değiştirilmediğinden emin olmak için bir sağlama toplamı gerekir. Ancak, basit bir sağlama toplamı (TCP 'de kullanıldığı gibi), güvenli olmayan bir saldırgan tarafından kolayca bir şekilde sallandığından, kabul edilebilir bir bütünlük düzeyini güvence altına almak için yetersizdir. TLS tarafından ileti bütünlüğü sağlamak için kullanılan mekanizma *şifreleme karması* olarak bilinir.

Şifreleme bir 1:1 kodlamadır. Yani, özgün verilerin tamamı şifrelenmiş verilerden elde edilebilir. Ancak, karma, bir sağlama toplamı gibi rastgele bir veri miktarını sabit boyutlu bir değere eşler. Basit bir sağlama sağlamasının aksine, karma özellikle, farklı giriş verilerinin aynı çıkışa neden olduğu *çarpışmaları* azaltmak için tasarlanmıştır. Basit bir sağlama toplamı içinde, bir bit 1 ' den 0 ' a ve 0 ' dan 1 ' e kadar bir bit 'e çevrilayarlanırsa, sağlama toplamı aynı olur. Bir şifreleme karması sayesinde, çıkış önemli ölçüde farklılık gösterir, böylece bir saldırgan karma verileri değiştirebilir ve değiştirilen verilerde karma işlemin yine de aynı değer elde edilmesine (ve bu sayede bu verilerin bütünlüğünü doğrulamaya) olanak sağlar.

TLS, her iki uygulama iletisi ve TLS denetim iletisi iletileri için bütünlük sağlamak üzere birçok farklı karma algoritma kullanır. Bunlara MD5, SHA-1 ve SHA-256 dahildir.

NetX güvenli TLS, MD5, SHA-1 ve SHA-256 karma 'ı destekler.

## <a name="tls-extensions"></a>TLS uzantıları

TLS, belirli uygulamalar için ek işlevsellik sağlayan birkaç uzantı sağlar. Bu uzantılar tipik olarak, bir uzak ana bilgisayara bir uzantı kullanmayı veya güvenli TLS oturumu oluştururken kullanılmak üzere ek ayrıntılar sağlamayı belirten ClientHello veya ServerHello iletilerinin bir parçası olarak gönderilir.

Genel olarak, uzantılar, işlem işlemlerine kılavuzluk eden el sıkışma başlangıcında TLS için isteğe bağlı parametreler sağlar. Bazı uzantılar uygulama girişi veya karar oluşturma gerektirir, diğerleri otomatik olarak işlenir.

Aşağıdaki tabloda, şu anda NetX güvenli TLS tarafından desteklenen TLS uzantıları açıklanmaktadır:

| **Uzantı adı**              | **Açıklama**              |
| ------------------------------- |----------------------------- |
| Güvenli yeniden anlaşma gösterimi | Bu uzantı, bir yeniden anlaşma el sıkışması sırasında oluşabilecek bir ortadaki adam saldırısı güvenlik açığını azaltır.|
| Sunucu Adı Belirtme          | Bu uzantı, bir TLS Istemcisinin bir TLS sunucusuna belirli bir DNS adı sağlamasına izin vererek sunucunun doğru kimlik bilgilerini seçmesini sağlar (sunucunun birden çok kimlik sertifikası ve ağ entryPoints olduğunu varsayar). |
| İmza algoritmaları            | Bu uzantı, TLS Istemcisinin kabul edilebilir imza ve karma algoritmalarının bir TLS sunucusuna bir listesini sağlamasını sağlar. |

Desteklenen TLS uzantılarına genel bakış

### <a name="secure-renegotiation-indication"></a>Güvenli yeniden anlaşma gösterimi

TLS, mevcut bir TLS oturumunda el sıkışma gerçekleştirme kavramını destekler, böylece el sıkışma iletilerini şifrelemek için belirlenen oturum vardır. Bu işlem, şifreleme oturumu anahtarlarının TLS oturumunu sonlandırmadan yeniden oluşturulmasına izin verir (bkz. "TLS oturumu yeniden anlaşması").

Ne yazık ki, TLS yeniden anlaşma bir süre kullandıktan sonra, yeniden anlaşma özelliğinden yararlanan bir ortadaki adam saldırısında bir güvenlik açığı olduğunu bulmuştur. Güvenlik açığını kapatmak için, güvenli yeniden anlaşma gösterge uzantısı eklenmiştir. Temelde, güvenli yeniden anlaşma uzantısı, başlangıçtaki ana bilgisayarların yeniden anlaşma el sıkışmasına katıldığını doğrulamak için, oluşturulan bağlantıdan tamamlanmış ileti karmasını kullanır – aslında karma, bir saldırganın karmayı yasaklayacağından (oturum anahtarlarına erişim gerektirir) bir doğrulama belirteci olarak kullanılır.

NetX güvenli TLS yeniden anlaşmayı otomatik olarak işler ve varsayılan olarak güvenli yeniden anlaşma uzantısını kullanır. Uygulama etkileşimi gerekmez.

### <a name="server-name-indication"></a>Sunucu Adı Belirtme

TLS anlaşması sırasında, bir TLS Istemcisi, istemcinin kimliğini doğrulayabilmesi için uzak sunucunun kimlik sertifikası sağlamasını bekler. Ancak, bir sunucunun benzersiz kimliklere sahip farklı "sanal" sunucularla birden çok farklı hizmet sağlayacağı bazı durumlar olabilir. Birden çok kimliği olan tek bir sunucu söz konusu olduğunda, bir TLS istemcisi sunucunun uygun kimlik bilgilerini seçmek için kullanacağı belirli bir DNS adı sağlayabilir. bu adı sağlamaya yönelik mekanizma Sunucu Adı Belirtme (SNı) uzantısıdır.

SNı uzantısını kullanan bir uygulama için bazı etkileşimler gereklidir. TLS Istemcileri için, uygulamanın uzak sunucuya gönderilmesi için bir DNS adı sağlaması gerekir. TLS sunucuları için, uygulamanın uzantısından DNS adını okuması ve istemciye geri göndermek için uygun bir sertifika seçmeniz gerekir.

Aşağıdaki bölümler NetX güvenli TLS 'de SNı uzantısının nasıl kullanılacağına ilişkin daha fazla ayrıntı sağlar.

### <a name="sni-extension--tls-client"></a>SNı uzantısı – TLS Istemcisi

SNı uzantısını kullanmak isteyen bir NetX güvenli TLS Istemcisinin, el sıkışma sırasında sağlanacak bir DNS adını, TLS 'ye sağlaması gerekir. Uzantı, el sıkışma işlemini başlatan ClientHello iletisinde gönderildiği için, bir TLS oturumu başlatılmadan önce bu adın başlatılmış ve sağlanması gerekir.

Aşağıdaki kod parçacığı, uzantısının kullanımını gösterir. İlk olarak, NX_SECURE_X509_DNS_NAME bir nesne istenen sunucu adı ile başlatılır. Daha sonra, TLS oturumuna başlamadan önce, adı SNı uzantısı API 'SI kullanılarak TLS olarak sağlanır. Ad ayarlandıktan sonra, başka bir eylem gerekmez. Bölüm 4 ' te API başvurusuna bakın  
  
Ayrı işlevler hakkında daha fazla bilgi için NetX güvenli hizmetlerinin açıklaması.

```C
/* The dns_name variable will contain our desired server name. */
UINT status;
NX_SECURE_X509_DNS_NAME dns_name;

/* Initialize the server DNS name. */
status = nx_secure_x509_dns_name_initialize(&dns_name, "www.example.com", 
                                            strlen("www.example.com"));


/* Initialize SNI extension in previously-initialized TLS Session. */
status = nx_secure_tls_session_sni_extension_set(&client_tls_session, &dns_name);

/* Now start the TLS session, starting with establishing the TCP connection – if 
   TLS is started before initializing the SNI extension, the extension will not be 
   sent in the ClientHello message! */
status = nx_tcp_client_socket_connect(&client_socket, IP_ADDRESS(1, 2, 3, 4), 443, 
                                      5 * NX_IP_PERIODIC_RATE);

status = nx_secure_tls_session_start(&client_tls_session, &client_socket, 
                                     NX_WAIT_FOREVER);
```
### <a name="sni-extension--tls-server"></a>SNı uzantısı – TLS sunucusu

TLS sunucu tarafında, el sıkışma sırasında uzak istemciye sağlanacak uygun kimlik bilgilerini (örn. sertifika) seçmek için, SNı uzantısı uygulama tarafından işlenebilir. Bunu yapmak için, uygulamanın bir ClientHello iletisinin alındığını izleyerek çağrılan bir oturum geri çağırması sağlaması gerekir.

Nx_secure_tls_session_server_callback_set API 'sinin örnek kodu (bkz. sayfa 122), bir sunucu geri çağırması kullanılarak gelen bir SNı uzantısının ayrıştırılmasını gösterir. Temelde, TLS sunucusu bir ClientHello alır ve geri çağırma işlemini çağırır. Ardından uygulama, SNı uzantısını bulmak için geri aramaya sağlanan uzantı verilerini ayrıştırmak ve sağlanan DNS adını döndürmek için *nx_secure_tls_session_sni_extension_parse* API 'sini kullanır (uzantının yalnızca tek bir DNS adını desteklediğini unutmayın). Ad alındıktan sonra uygulama, uygun sunucu kimlik sertifikasını (ve uygulanabilirse veren zincirini) bulmak ve göndermek için onu kullanır.

### <a name="signature-algorithms-extension"></a>İmza algoritmaları uzantısı

Bu uzantı TLS 1,2 ' e özgüdür ve bir TLS Istemcisinin dijital imzaları oluşturma ve doğrulama için kabul edilebilir kabul edilebilir imza ve karma algoritma çiftlerinin bir listesini sağlamasına izin verir. Liste, *nx_secure_tls_session_create* için sağlanan şifre tablosunu kullanan TLS Istemcileri Için NETX güvenli TLS tarafından otomatik olarak oluşturulur. Uygulama etkileşimi gerekmez.

## <a name="authentication-methods"></a>Kimlik Doğrulaması Yöntemleri

TLS, güvenli olmayan bir ağ üzerinden iki cihaz arasında güvenli bir bağlantı kurmak için çerçeve sağlar, ancak sorunun bir parçası bu bağlantının diğer ucundaki cihazın kimliğini öğrenmektir. Uzak ana bilgisayarların kimliğini doğrulamak için bir mekanizma olmadan, saldırganın güvenilen bir cihaz olarak oluşturabileceği önemsiz bir işlem haline gelir.

Başlangıçta, IP adreslerini, donanım MAC adreslerini veya DNS 'yi kullanarak, bir ağdaki Konakları tanımlamak için görece yüksek düzeyde güven sağlayabilir, ancak TCP/IP teknolojisinin doğası ve adreslerin sızması ve DNS girdilerinin bozulmuş olması (örneğin, DNS önbelleği kirlenmesi aracılığıyla), TLS 'nin sahte kimliklere karşı ek bir koruma katmanı gerektirdiğinden emin olur.

Bu ek kimlik doğrulama katmanını TLS için sağlayabilecek çeşitli mekanizmalar vardır ancak en sık kullanılan *dijital sertifikadır.* Diğer mekanizmalarda önceden paylaşılan anahtarlar (PSK) ve parola şemaları bulunur.

### <a name="digital-cerificates"></a>Dijital sertifika

Dijital sertifikalar, TLS 'de uzak ana bilgisayarın kimliğini doğrulamak için en sık kullanılan yöntemdir. Esas olarak, dijital sertifika, bir bilgisayar ağındaki bir cihaz için kimlik bilgileri sağlayan belirli bir biçimlendirmeye sahip bir belgedir.

TLS, normalde Uluslararası Telekomünikasyon birleşimi tarafından geliştirilen standart olan X. 509.440 adlı bir biçim kullanır, ancak TLS ana bilgisayarları kullanılan biçimde kabul ediyorsanız başka sertifika biçimleri de kullanılabilir. X. 509.440, sertifikalar için belirli bir biçimi ve dijital bir belge oluşturmak için kullanılabilecek çeşitli kodlamaları tanımlar. TLS ile kullanılan en X. 509.440 sertifikaları, farklı bir telekomünikasyon standardı olan ASN. 1 ' in bir türevi kullanılarak kodlanır. ASN. 1 içinde çeşitli dijital kodlamalar vardır ancak TLS sertifikaları için en yaygın kodlama Distinguished Encoding Rules (DER) standardıdır. DER, ASN. 1 temel kodlama kuralları 'nın (BER), belirsiz olacak şekilde tasarlanan, ayrıştırmayı kolaylaştırmak için basitleştirilmiş bir alt kümesidir. Kablo üzerinden, TLS sertifikaları genellikle ikili DER olarak kodlanır ve bu, NetX Secure 'ın X. 509.440 sertifikalarını beklediği biçimdedir.

DER biçimli ikili sertifikalar gerçek TLS protokolünde kullanılıyor olsa da, bunlar. pek,. CRT ve. p12 gibi dosya uzantılarına sahip bir dizi farklı kodlarda oluşturulup depolanabilir. Farklı çeşitler farklı üreticilerin farklı uygulamaları tarafından kullanılır, ancak genel kullanıma sunulan araçlar kullanılarak tüm geliştiriciler DER 'a dönüştürülebilir.

Alternatif sertifika kodlamaları en yaygın olarak ped 'dir. PEK biçimi (Privacy-Enhanced mail 'den), kodlama, e-posta veya Web tabanlı protokoller kullanılarak kolayca gönderilebilecek yazdırılabilir metinle sonuçlandığından, genellikle kullanılan DER kodlamasının temel 64 kodlu bir sürümüdür.

NetX güvenli uygulamanız için bir sertifika oluşturmak, genel olarak bu el ile kapsam dışındadır, ancak OpenSSL komut satırı aracı ([www.OpenSSL.org](http://www.openssl.org)) yaygın olarak kullanılabilir ve çoğu biçim arasında dönüştürülebilir.

Uygulamanıza bağlı olarak, kendi sertifikalarınızı oluşturabilir, bir üretici veya devlet kurumuna sertifika verebilir veya ticari bir sertifika yetkilisinden sertifika satın alabilirsiniz.

NetX güvenli uygulamanızda dijital bir sertifika kullanmak için, önce sertifikanızı bir ikili DER biçimine dönüştürmeniz ve isteğe bağlı olarak, ilişkili özel anahtarı (RSA için "Private üs" i) ikili biçime, genellikle PKCS # 1 biçimli, DER kodlu bir RSA anahtarını veya DER kodlu bir ECC anahtarını dönüştürmeniz gerekir. Dönüştürme işlemi tamamlandıktan sonra, sertifikayı ve özel anahtarı cihaza yüklemeniz gerekir. Olası seçenekler, Flash tabanlı bir dosya sistemi kullanmayı veya verilerden bir C dizisi oluşturmayı (Linux 'tan "XXD" gibi bir araç kullanarak) ve sertifikayı ve anahtarı sabit veri olarak uygulamanıza derlemeyi içerir.

Sertifikanız cihaza yüklendikten sonra, sertifikanızı bir TLS oturumuyla ilişkilendirmek için TLS API 'SI kullanılabilir.

X. 509.440 sertifikalarının NetX güvenli TLS ile nasıl kullanılacağına ilişkin ayrıntılar ve örnekler için, "X. 509.440 sertifikalarını NetX güvenli olarak Içeri aktarma" bölümüne bakın.

Daha fazla bilgi için API başvurusunda aşağıdaki TLS hizmetlerine başvurun:

- nx_secure_x509_certificate_initialize
- nx_secure_tls_local_certificate_add
- nx_secure_tls_local_certificate_remove
- nx_secure_tls_remote_certificate_allocate
- nx_secure_tls_trusted_certificate_add
- nx_secure_trusted_certificate_remove

### <a name="tls-client-certificate-specifics"></a>TLS Istemci sertifikası özellikleri

TLS Istemci uygulamaları genellikle cihaza bir "yerel" sertifika<sup>14</sup> ' ün yüklenmesini gerektirmez. Bunun özel durumu, Istemci sertifikası kimlik doğrulamasının etkinleştirilme durumdur, ancak bu çok daha az yaygındır.

TLS Istemcisi, en az bir "güvenilir" sertifika<sup>15</sup> ' in yüklenmesini (gerekirse daha fazla yüklenebilir) ve bir "uzak" sertifika<sup>16</sup> ' nın ayrılması için boşluk gerektirir.

Güvenilen Sertifikalar ekleme ve uzak sertifikalara alan ayırma hakkında daha fazla bilgi için, şu hizmetler için TLS API başvurusuna bakın: nx_secure_tls_remote_certificate_allocate, nx_secure_tls_trusted_certificate_add.

14. "Yerel" sertifika, yerel cihazı tanımlayan bir sertifikadır; diğer bir deyişle, TLS uygulamasının yüklendiği cihaz için kimlik bilgileri sağlar.

15. "Güvenilir" sertifika, uzak cihazın doğrudan veya bir ortak anahtar altyapısı (PKI) ile güven ve kimlik doğrulaması için temel sağlayan bir sertifikadır. Güven zincirinin köküne genellikle "sertifika yetkilisi" veya CA sertifikası denir.

16. "Uzak" sertifika, TLS el sıkışması sırasında uzak ana bilgisayar tarafından gönderilen sertifikaya başvurur. Bu uzak ana bilgisayar için kimlik sağlar ve yerel cihazdaki "güvenilir" bir sertifikayla karşılaştırarak doğrulanır.

### <a name="tls-server-certificate-specifics"></a>TLS sunucu sertifikası özellikleri

TLS sunucu uygulamaları genellikle "güvenilen" sertifikaların ayrılacak cihaza veya uzak sertifikalara yüklenmesini gerektirmez. Istemci sertifikası kimlik doğrulaması etkinleştirildiğinde bunun özel durumu (daha az yaygın).

Bir TLS sunucusu, sunucunun kimliğini istemci için doğrulamak üzere TLS el sıkışması sırasında uzak istemciye sağlayabilmesi için bir "yerel" sertifikanın yüklenmesini gerektirir.

NetX TLS sunucu uygulamalarıyla kullanılmak üzere yerel sertifikaları yükleme hakkında daha fazla bilgi için, aşağıdaki hizmetler için API başvurusuna bakın: 
- nx_secure_tls_local_certificate_add, 
- nx_secure_tls_local_certificate_remove.

### <a name="pre-shared-keys-psk"></a>Önceden paylaşılan anahtarlar (PSK)

TLS 'de kimlik doğrulaması sağlamaya yönelik alternatif bir mekanizma, önceden paylaşılan anahtarların (PSK) kavramsıdır. Bir PSK ciphersuite kullanılması, kaynak kısıtlı gömülü cihazlar için bir Boon, yoğun işlemci yoğunluklu ortak anahtar şifreleme işlemleri gereksinimini ortadan kaldırır. PSK, TLS el sıkışmasındaki sertifikayı değiştirir ve TLS oturum anahtarı oluşturma için şifrelenmiş ön ana gizli dizi yerine kullanılır.

PSK ciphersuites, bir TLS oturumu oluşturulmadan önce her iki cihazda de paylaşılan bir gizliliğin olması gerektiğini anlamıştır. Bu, cihazların bir TLS PSK bağlantısı dışında bazı güvenli bir şekilde yüklenmiş olması gerektiği anlamına gelir. PSKs bir TLS PSK bağlantısı üzerinden güncelleştirilemeyebilir, ancak cihazın başka bir mekanizma aracılığıyla yüklenen bir PSK ile başlaması gerekir. Örneğin, bir algılayıcı aygıtı ve ağ geçidi cihazı, sevk etmeden önce fabrikada PSKs ile veya PSK 'yi yüklemek için standart bir TLS bağlantısı (bir sertifika ile) kullanılabilir.

PSK ciphersuites, RFC 4279 ' de açıklanan çeşitli biçimlerde gelir. İlki, Standart TLS el sıkışmaları içinde sertifikada aktarılan ortak anahtarlarla aynı şekilde kullanılan RSA veya Diffie-Hellman anahtarlarını kullanır. Kaynak kısıtlı bir ortamda daha fazla kullanılan ikinci form, oturum anahtarlarını doğrudan oluşturmak için kullanılan bir PSK kullanır (örneğin, AES tarafından kullanılmak üzere), pahalı RSA veya Diffie-Hellman işlemlerinin kullanılmasını önler.

NetX güvenli,, uygulamaların tüm ortak anahtar şifreleme kodunu ve bellek kullanımını kaldırmasını sağlayan PSK ciphersuites 'in ikinci biçimini destekler. PSK kendisi bir AES anahtarı değil, ancak gerçek anahtarların oluşturulduğu bir parola gibi kabul edilebilir. PSK değeri ile ilgili olarak daha uzun değerler daha fazla güvenlik (parolalarla aynı şekilde) sağlayabilse de daha fazla kısıtlama vardır.

NetX güvenli uygulamanızla PSK 'yi kullanmak için, önce genel makro **NX_SECURE_ENABLE_PSK_CIPHERSUITES** tanımlamanız gerekir. Bu genellikle derleyici ayarlarınız aracılığıyla yapılır, ancak tanım nx_secure_tls. h üst bilgi dosyasına da yerleştirilebilirler. Tanımlanan makro ile, PSK ciphersuite desteği NetX güvenli TLS uygulamanıza Derlenecek.

PSK desteği etkinken, uygulamanız için PSKs 'leri kurmak üzere TLS API 'sini kullanabilirsiniz. Her PSK için bir PSK değeri (gerçek gizli anahtar "anahtarı" – Bu değeri güvenli tut), belirli bir PSK 'yi tanımlamak için kullanılan bir "Identity" değeri ve bir TLS sunucusu tarafından belirli bir PSK değeri seçmek için kullanılan bir "kimlik ipucu" gerekir.

PSK, bir ağ bağlantısı üzerinden hiçbir şekilde gönderilmediğinden herhangi bir ikili değer olabilir. PSK, 64 bayta kadar olan herhangi bir değer olabilir.

Kimliğin ve ipucunun UTF-8 kullanılarak biçimlendirilen yazdırılabilir karakter dizeleri olması gerekir. Kimlik ve ipucu değerleri 128 bayta kadar olan uzunlukta olabilir.

Identity ve PSK, ağdaki bir birbirleriyle iletişim kurması gereken her cihaza yüklenen benzersiz bir çift oluşturur.

"İpucu", birincil olarak, bir işlev veya hizmete göre PSKs 'leri gruplandırmak için belirli uygulama profillerinin tanımlanması için kullanılır. Bu değerler önceden anlaşılmalıdır ve uygulamaya bağımlı olur. Örnek olarak, OpenSSL komut satırı sunucu uygulaması (PSK etkin ile), TLS el sıkışması ile devam edebilmek için bir TLS istemcisi tarafından sağlanması gereken varsayılan "Client_identity" dizesini kullanır.

PSKs hakkında daha fazla bilgi için, aşağıdaki hizmetler için NetX Secure API başvurusuna bakın: nx_secure_tls_client_psk_set, nx_secure_tls_psk_add.

## <a name="importing-x509-certificates-into-netx-secure"></a>X. 509.440 sertifikalarını NetX ile alma güvenli

Internet üzerindeki çoğu TLS bağlantısı için dijital sertifikalar gerekir. Sertifikalar, genellikle *sertifika yetkilileri* veya CA olarak adlandırılan güvenilen Aracılar kullanılarak Internet üzerinden daha önce bilinmeyen Konakları kimlik doğrulaması için bir yöntem sağlar. NetX güvenli cihazınızı ticari bir bulut hizmetiyle (örneğin, Amazon Web Services) bağlamak için, bu sertifikaları cihazınıza yükleyerek uygulamanıza aktarmanız gerekir.

Sertifikalarla birlikte, bazen sertifikalarınızla ilişkili bir *özel anahtara* da ihtiyacınız olacaktır. Bazı uygulamalarda (Istemci sertifikası kimlik doğrulaması kullanılmazsa TLS Istemcisi gibi), sertifika tek başına yeterli olacaktır, ancak sertifikanız cihazınızı tanımlamak için kullanılıyorsa özel bir anahtara ihtiyacınız olur. Özel anahtarlar genellikle sertifikanızı oluşturduğunuzda oluşturulur ve genellikle bir parolayla şifrelenir ve ayrı bir dosyada depolanır.

### <a name="certificate-types"></a>Sertifika Türleri

Dijital sertifikalar genellikle bir ağdaki varlıkları tanımlamak için kullanılır, ancak uygulamalarının ne kadar farklı özelliklerine sahip olacaklarına bağlıdır.

### <a name="local-certificates"></a>Yerel sertifikalar

Bu belgelerin amaçları doğrultusunda, yerel cihazımız için bir kimlik sağlayan bu sertifikalar olarak "yerel Sertifikalar" a başvuracağız (başka bir olası ad "cihaz sertifikası" olabilir). Bu sertifikalar uzak ana bilgisayar yerel cihazın kimliğini doğrulamak için bir uzak ana bilgisayara sağlanacak.

### <a name="remote-certificates"></a>Uzak sertifikalar

Bu belgelerde, "uzak sertifikalar", uygun olduğunda TLS el sıkışması sırasında uzak bir ana bilgisayar tarafından verilen sertifikaları ifade eder. Bu sertifikaların alanı ayrılmalı veya NetX güvenli hale gelmelidir ve TLS el sıkışması tamamlanamayacak.

### <a name="signing-certificates"></a>İmzalama sertifikaları

Kimlik doğrulama amacıyla diğer sertifikaları veya verileri dijital olarak imzalamak için "imzalama sertifikası" kullanılır. Bu sertifikalar bir ortak anahtar altyapısında (PKI) ara veya kök sertifikalar olabilir ve genellikle tek tek cihazları veya Konakları tanımlamak için kullanılmaz.

### <a name="root-ca-certificates"></a>Kök CA sertifikaları

"Kök CA sertifikaları", bir PKI 'nın temelini oluşturan ve başka bir imzalama sertifikası tarafından imzalanmak yerine kendinden imzalı olan imzalama sertifikalardır. Bir TLS Istemcisinin uzak sunucuları doğrulaması için en az bir kök CA sertifikası gereklidir.

### <a name="certificate-formats"></a>Sertifika biçimleri

Dijital sertifikalar yalnızca ASN. 1 sözdizimi kullanılarak kodlanan yapılandırılmış verileri içeren dosyalardır. Ancak, sertifikaların depolanabileceği çeşitli biçimler vardır ve bir sertifikayı NetX güvenli uygulamasına yüklemeden önce doğru biçime sahip olmak önemlidir.

Sertifikalar için en yaygın biçimler DER ve Peg ' dir. DER ( *Distinguished Encoding Rules* IÇIN bir ASN. 1 biçimi), ilk el SıKıŞMA gerçekleştirilirken TLS tarafından kullanılan ikili biçimdir. Peg ( *Gizlilik Gelişmiş posta*'ten), Web 'de http üzerinden gönderme veya gönderme için uygun olan der biçiminin base-64 kodlu bir sürümüdür. Farklı satıcılar, sertifika için ". pek" veya ". CRT" gibi farklı dosya adı uzantılarını ve DER sertifikaları için ". der" kullanır. Bir sertifikanız varsa ve bu, hangi biçimin kullanıldığını temizleyemiyorsa, dosyayı bir metin düzenleyicisinde açmak, DER dosyaları kodlanmış ikiliden itibaren türü belirlemenizi sağlar ve pek dosyaları, "-----başlangıç SERTIFIKASı-----" üstbilgisiyle başlayan normal ASCII metinlerdir.

NetX güvenli, sertifikanızın ikili DER biçiminde olmasını gerektirir, bu nedenle içeri aktarmadan önce sertifikanızı DER biçimine dönüştürmeniz gerekir. Bu, OpenSSL gibi kullanıma hazır araçlarla yapılabilir.

Uygulamanız için özel bir anahtara ihtiyacınız varsa, anahtar dosya belirli bir biçimde ped veya DER kullanılarak kodlanır (RSA için PKCS # 1, ECC için RFC 5915). Özel anahtar dosyasının içeri aktarılmadan önce DER olarak dönüştürülmesi gerekir.

Aşağıdaki OpenSSL komutları, sertifikaları ve RSA anahtar dosyalarını NetX Secure (ECC benzerdir – OpenSSL belgelerine bakın) için gereken DER biçimine dönüştürmeye yönelik bir örnek olarak verilmiştir.

```C
openssl x509 -inform PEM -in <certificate> -outform DER -out cert.der
openssl x509 -inform PEM -in <root CA cert> -outform DER -out CA_cert.der
openssl rsa -inform PEM -in <private key> -outform DER -out private.key
```
### <a name="private-keys-and-certificates"></a>Özel anahtarlar ve sertifikalar

Bir cihazı tanımlayan sertifikalar için, ilişkili özel anahtarın sertifikayla birlikte yüklenmesi gerekir. Özel anahtar (RSA, Diffie-Hellman veya Elliptic-Curve Cryptography gibi ortak anahtar algoritmalarından biri olabilir), bir TLS sunucusu tarafından, gelen anahtar malzemesinin ("Ana Gizlilik") bir TLS istemcisinden şifresini çözmek için kullanılır ve bu sayede istemcinin kimliğini kimlik doğrulamasını sağlar. Bir TLS Istemcisi için, bir kimlik sertifikası (ilişkili özel anahtarı olan bir sertifika) sağlanmışsa ve sunucu bir istemci sertifikası isterse, özel anahtar istemcinin kimliğini doğrulamak için kullanılır. RSA, istemci sertifikada belirtilen özel anahtarı kullanarak bir belirteci şifreler (Diffie-Hellman ve ECC kimlik doğrulaması benzer bir şekilde gerçekleşir, ancak Ayrıntılar bit farklıdır)).

NetX güvenli ' te, Service *nx_secure_x509_certificate_initialize* bir X. 509.440 sertifikası başlatmak için kullanılır (daha fazla bilgi için bkz. "cihazınıza sertifika yükleme" bölümüne bakın) ve isteğe bağlı olarak özel bir anahtarı bu sertifikayla ilişkilendirin.

Özel anahtar sağlanırsa, sertifika, cihazı tanımlamak için kullanılan "kimlik" sertifikası olarak işaretlenir. Anahtar bitişik bir ikili blob ve bir uzunluğu, ilişkili anahtar türü olarak geçirilir. Anahtar türü anahtarın türüne (ör. RSA, ECC, vb.) ve biçimde (örn. PKCS # 1 DER) bağlıdır. Anahtar sağlanmazsa, hiçbir anahtar sağlanmakta olmadığını göstermek için NX_SECURE_X509_KEY_TYPE_NONE (değer 0x0) değeri geçirilebilir (0 uzunluğu ve veri parametresi için bir NX_NULL işaretçisi aynı etkiye ulaşacaktır).

Aşağıdaki tabloda NetX güvenli olarak bilinen anahtar türleri ve *nx_secure_x509_certificate_initialize* geçirilecek ilişkili tür tanımlayıcısı gösterilmektedir. NetX güvenli 'ye daha fazla şifreleme algoritması eklendikçe ek anahtar türleri eklenecektir.

| Tanımlayıcı                              | Algoritma | Biçimlendir   | Encoding | Değer |
| --------------------------------------- | --------- | -------- | -------- | ----- |
| NX_SECURE_X509_KEY_TYPE_NONE            | Yok      | Yok      | Yok      | 'dır   |
| NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER   | RSA       | PKCS # 1   | CÜ      | 0x1   |
| NX_SECURE_X509_KEY_TYPE_EC_DER          | ECDSA     | RFC 5915 | CÜ      | 0x2   |

### <a name="user-defined-private-key-types"></a>Kullanıcı tanımlı özel anahtar türleri

*Nx_secure_x509_certificate_initialize* hizmeti için anahtar türü tanımlayıcılarının değerleri, özel anahtar sağlandığında gerçekleştirilecek eylemleri yönetir. Bilinen türler için değerler 0x0000 0000 – 0x0000 FFFF aralığındadır (32 bit işaretsiz tamsayının alt 16 bitleridir). Özel anahtar türleri<sup>17</sup> olan platformlar için (bazı donanım tabanlı şifreleme altyapılarında olduğu gibi), anahtar türü olarak 0x0000 1000-0xFFFF ffff (ilk 16 bit sıfır olmayan) aralığında Kullanıcı tanımlı bir anahtar türü geçirilebilir. Anahtar türünün en üstteki 16 biti ayarlandıysa, özel anahtar verileri TLS ciphersuite tablosunda sağlanan uygun şifreleme yordamına (ör. RSA) doğrudan geçirilir. Kullanıcı tanımlı anahtar türleri ayrıştırılmaz veya şifreleme yordamına geçirilmeden önce işlenmemiştir. Ayrıca, Kullanıcı tanımlı anahtar türü de şifreleme yordamına geçirilir, böylece ilgili işlem o düzeyde işlenebilir.

Kullanıcı tanımlı anahtar türlerinin, özel (Belki de şifrelenmiş) anahtar verileri kullanan belirli donanım platformları için genellikle kullanıldığını unutmayın. Genellikle bu, anahtar verilerinin, bu donanım satıcısına özgü bir mekanizma kullanılarak oluşturulduğu veya kodlandığı anlamına gelir (veya PKCS # 11 gibi bir standart olması durumunda belirli bir standart). Daha fazla bilgi için donanım platformu belgelerinize başvurun.

17. Kullanıcı tanımlı anahtar türleri, özel anahtar biçimini işlemek için karşılık gelen özel bir şifreleme yordamını gerektirir. Şifreleme yordamının eşleşen bir algoritması (ör. RSA) olması ve ciphersuite tablosunda TLS 'ye geçirilmesi gerekir. 

### <a name="loading-certificates-onto-your-device"></a>Cihazınıza sertifika yükleme

Cihazınıza dosya yüklemeye yönelik herhangi bir yöntem, sertifikalarınızı içeri aktarmak için yeterli olacaktır.

Bir sertifikayı yüklemek için en basit yöntem, ikili DER kodlu verileri bir C dizisine dönüştürmeli ve bunu uygulamanızda bir sabit olarak derler. Bu, Linux 'ta "XXD" gibi araçlarla kolayca yapılabilir ("-i" seçeneği ile).

Alternatif olarak, sertifika verilerine yönelik bir işaretçiyi NetX güvenli API 'ye geçirebilmeniz koşuluyla, sertifikanızı bir Flash FileSystem veya diğer depolama seçeneklerine yükleyebilirsiniz.

### <a name="certificate-files-needed-for-netx-secure"></a>NetX güvenli için gereken sertifika dosyaları

İçeri aktarmanız gereken sertifika dosyaları uygulamanıza bağlıdır. Genel olarak, TLS sunucuları cihazı tanımlamak için bir sertifika gerektirir ve TLS Istemcileri uzak sunucuların kimliğini doğrulamak için bir veya daha fazla *Güvenilen sertifika* gerektirir. Aşağıdaki tabloda bazı farklı TLS uygulamaları için gereken sertifikalar gösterilmektedir.

| **TLS işlevselliği/seçenekleri**                     | **Gerekli sertifikalar/anahtarlar (minimum)**              |
| ------------------------------------------------- | --------------------------------------------------- |
| TLS Istemcisi                                        | Kök CA sertifikası                                 |
| TLS sunucusu                                        | Yerel sertifika, bu sertifika için özel anahtar |
| Istemci sertifikası kimlik doğrulaması ile TLS sunucusu | Yerel sertifika, özel anahtar, kök CA             |
| Istemci sertifikası kimlik doğrulaması ile TLS Istemcisi | Yerel sertifika, özel anahtar, kök CA             |
| Yalnızca önceden paylaşılan anahtarları olan TLS Istemcisi veya sunucusu    | Hiçbiri (sertifikalar yerine PSK kullanıldı)             |

Sertifikaları yüklemek için ilgili hizmetler aşağıdaki gibidir:

| **API adı**                                   | **Amaç**                                            |
| ---------------------------------------------- |------------------------------------------------------- |
| nx_secure_x509_certificate_initialize      | , NX_SECURE_X509_CERT yapısını sertifika verilerinize ve özel anahtarınızla doldurmak için tüm sertifikaların çağrılması gerekir. |
| nx_secure_tls_local_certificate_add       | Cihazınızı tanımlamak için bir TLS oturumuna yerel sertifika ekleyin.                                                                |
| nx_secure_tls_local_certificate_remove    | Bir TLS oturumundan yerel bir sertifikayı kaldırın.                                                                                   |
| nx_secure_tls_remote_certificate_allocate | Uzak bir sertifika için alan ayırır (başlatılmamış NX_SECURE_X509_CERT ile çağırılır).                                   |
| nx_secure_tls_trusted_certificate_add     | Uzak konaklara kimlik doğrulaması için güvenilen bir sertifika olarak bir TLS oturumuna sertifika ekleyin.                                     |
| nx_secure_tls_trusted_certificate_remove  | Bir TLS oturumundan güvenilir bir sertifikayı kaldırın.                                                                                 |

### <a name="working-with-aws-iot-certificates"></a>AWS IoT sertifikalarıyla çalışma

Amazon Web Services IoT arabiriminde, kenar çubuğu menüsünden "güvenlik" i seçin ve "Sertifikalar" ı seçin. Yeni bir sertifika oluşturun ve yeni cihaz sertifikanızı indirmek için yönergeleri izleyin.

Sertifikalarınızı indirdikten sonra, OpenSSL veya benzer bir yardımcı program kullanarak bunları DER biçimine dönüştürmeniz gerekir.

NOTE: AWS ortak anahtar dosyası da sağlar. Ortak anahtar, yerel cihaz sertifikası içinde bulunur, bu nedenle uygulamanıza aktarılmaları gerekmez.

Örnek olarak, yerel cihaz sertifikasını ve özel anahtarını NetX güvenli ile kullanmak üzere DER biçimine dönüştürmek için komutlar aşağıda verilmiştir:

```C
openssl x509 -inform PEM -in <certificate> -outform DER -out cert.der
openssl x509 -inform PEM -in <root CA cert> -outform DER -out CA_cert.der
openssl rsa -inform PEM -in <private key> -outform DER -out private.key
```
Dönüştürülen dosyalar, yukarıdaki yönergeleri izleyerek uygulamanıza aktarılabilir.

## <a name="x509-certificate-validation-in-netx-secure"></a>NetX 'te X. 509.440 sertifika doğrulaması güvenli 

Ana bilgisayar tanımlama ve doğrulama için X. 509.440 sertifikalarıyla TLS kullanırken, bu sertifikaların gerçekten nasıl doğrulandığını anlamak önemlidir. TLS belirtimi bir sertifikanın nasıl doğrulanacağı hakkında ayrıntılı yönergeler sağlamıyorsa, bu, X. 509.440 belirtimine (RFC 5280) başvurur. Genel olarak, TLS 'nin gelen sertifikalarda en az temel doğrulama gerçekleştirmesini (TLS el sıkışması sırasında uzak ana bilgisayar tarafından sağlanan sertifikalar) ve NetX güvenli TLS 'in farklı olmaması beklenmektedir.

### <a name="basic-x509-validation"></a>Temel X. 509.440 doğrulaması

Tüm gelen sertifikalar için NetX güvenli TLS, temel X. 509.440 yol doğrulamasını gerçekleştirir. İşlem, güvenilen sertifikaları içeri aktarma hakkında daha fazla bilgi için, her sertifikanın dijital imzasını veren sertifikasına karşı denetlemeyi içerir. Bu, uzak ana bilgisayar tarafından sağlanabiliyor veya güvenilen sertifika deposunda yer alıyor (güvenilen sertifikaları alma hakkında daha fazla bilgi için "X. 509.952 sertifikalarını NetX 'e aktarma" bölümüne bakın). Doğrulama işlemi, güvenilen sertifikaya ulaşılana veya zincir sona erene kadar (otomatik olarak imzalanan bir sertifika veya eksik veren sertifikayla) veren sertifikalarda yinelemeli olarak yinelenir. Güvenilen sertifikaya ulaşıldığında, sertifika doğrulanır, aksi takdirde reddedilir. Ayrıca, doğrulama işlemindeki her aşamada her bir sertifikanın sona erme tarihi, uygulama zaman damgası işlevi tarafından belirtilen zamana göre denetlenir (daha fazla bilgi için "nx_secure_tls_session_time_function_set" hizmetine bakın).

X. 509.440 belirtimi, yol doğrulaması sırasında denetlenebilir bir X. 509.952 uzantısında bulunan tanımlayıcılar olan "ilkeleri" desteklemek için bir algoritma da sunar. NetX Secure Şu anda X. 509.440 sertifikalarını "anyPolicy" seçeneği tanımlanmış olsa da kabul eder; yani, tüm ilkeler kabul edilebilir ve isteğe bağlı ilke denetimi gerçekleştirilmez. NetX Secure X. 509.440 uygulamasının daha sonraki bir sürümde bu özellikle Genişletilebilir olması olabilir. Şimdilik, ilke uzantısı *nx_secure_x509_extension_find* API kullanarak bir sertifikadan elde edilebilir.

Temel yol doğrulaması tamamlandıktan sonra, TLS *nx_secure_tls_session_certificate_callback_set* API kullanılarak uygulama tarafından sağlanan sertifika doğrulama geri aramasını çağırır. Geri arama sağlanmadığında, sertifikanın başarılı yol doğrulamasından sonra güvenilir olduğu kabul edilir. Bir geri çağırma sağlanırsa, geri arama, uygulamanın gerektirdiği sertifikanın ek doğrulamasını gerçekleştirir. Geri aramadan gelen dönüş değeri, TLS el sıkışması ile devam edilip edilmeyeceğini veya bir doğrulama hatası nedeniyle el sıkışmasını durdurmayı belirlemekte kullanılır.

Geri çağırma, ilgili TLS oturumuna yönelik bir işaretçi ve doğrulanacak sertifikaya yönelik NX_SECURE_X509_CERT işaretçisi ile çağrılır. TLS oturumu ve sertifika arasında, uygulamanın ek doğrulama denetimleri gerçekleştirmesi için gereken tüm verileri TLS 'den yapması gerekir.

NetX Secure, ek doğrulamaya yardımcı olmak için DNS doğrulaması ve sertifika Iptal listesi denetimi dahil bazı yaygın doğrulama işlemleri için X. 509.440 yordamlarını sağlar. Bu yordamların hepsi, sertifika doğrulama geri aramasında kullanılmak üzere uygundur, ancak X. 509.440 sertifikalarının çevrimdışı denetimini gerçekleştirmek için de kullanılabilir.

Aşağıdaki tabloda X. 509.440 sertifika işleme için kullanılabilir yardımcı işlevler özetlenmektedir. İşlemler için daha ayrıntılı açıklamalar, Bölüm 4 ' te aşağıdaki bölümlerde ve API başvurusunda bulunabilir  
  
NetX güvenli hizmetlerinin açıklaması, belirli yordamlar hakkında ek ayrıntılar sağlar.

| **API adı**                             | **Açıklama**                               |
| ---------------------------------------- | -------------------------------------- |
| nx_secure_x509_common_name_dns_check               | X. 509.952 Subject ortak adı ve SubjectAltName ' i beklenen bir DNS adına göre denetleyin |
| nx_secure_x509_crl_revocation_check                 | Bir X. 509.440 sertifika Iptal listesindeki (CRL) iptal edilmiş bir sertifika olup olmadığını denetleyin       |
| nx_secure_x509_extended_key_usage_extension_parse | Bir sertifikada belirli bir genişletilmiş anahtar kullanımı OID 'sini ayrıştırma ve bulma                   |
| nx_secure_x509_key_usage_extension_parse           | Bir sertifikadaki anahtar kullanımı bitalanını ayrıştırın ve döndürün                            |
| nx_secure_x509_extension_find                        | Belirli bir uzantı için ham DER kodlu ASN. 1 verilerini bulun ve döndürün.            |

Sertifika doğrulama geri aramasında kullanılacak X. 509.440 yardımcı işlevleri

### <a name="x509-extensions"></a>X. 509.440 uzantıları

X. 509.440 belirtimi, sertifikaların Doğrulanmakta kullanılabilecek ek bilgiler sağlamak için kullanılabilen bir dizi "uzantıyı" tanımlar. Çoğu bölüm için bu uzantılar isteğe bağlıdır ve bir dijital sertifikanın güvenilen bir kök sertifikaya karşı güvenli doğrulanması için gerekli değildir. Ancak NetX Secure, bazı temel uzantıları destekler. Ek uzantılar için destek gelecekteki sürümlerde eklenebilir.

Şu anda desteklenen uzantılar aşağıdaki tabloda listelenmiştir:

| Uzantı adı           | Açıklama                                                                   | İlgili API                                             |
| ------------------------ | ----------------------------------------------------------------------------- | -------------------------------------------------------- |
| Anahtar Kullanımı                | Bir bit alanından içindeki bir sertifikanın ortak anahtarı için kabul edilebilir kullanımlar sağlar         | nx_secure_x509_key_usage_extension_parse           |
| Genişletilmiş Anahtar Kullanımı       | , Bir sertifikanın OID kullanarak ortak anahtarı için kabul edilebilir ek kullanımlar sağlar | nx_secure_x509_extended_key_usage_extension_parse |
| Konu Diğer Adı | Sertifika tarafından da temsil edilen alternatif DNS adları sağlar   | nx_secure_x509_common_name_dns_check               |

### <a name="unsupported-x509-extensions"></a>Desteklenmeyen X. 509.440 uzantıları

NetX Secure 'ın X. 509.440, desteklenmeyen uzantıları ayıklamak için de bir hizmet sağlar: *nx_secure_x509_extension_find*. Bu API, döndürülen verileri ayrıştırmak için DER kodlu ASN. 1 bilgisine ihtiyaç duyan gelişmiş kullanıcılara yöneliktir. Bu BT, desteklenen uzantıları ayıklamak için dahili olarak kullanılır, ancak X. 509.440 uzantıları için özelleştirilmiş destek geliştirme konusunda kolaylık sağlaması için sağlanır.

Nx_secure_x509_extension_find kullanmak için, sertifika ve uzantı KIMLIĞIYLE birlikte bir NX_SECURE_X509_EXTENSION geçirilir. Bu, bilinen bir uzantı türü için değişken uzunluklu OID dizesinin tamsayı gösterimidir. X. 509.440 uzantıları için desteklenen OID 'lerin tamamı, sayfa 178 ' de nx_secure_x509_extension_find için API başvurusunda verilmiştir.

NX_SECURE_X509_EXTENSION yapısı aşağıdaki gibi tanımlanır:

```C
typedef struct NX_SECURE_X509_EXTENSION_STRUCT
{
    /* Identifier (maps to OID) for this extension. */
    USHORT nx_secure_x509_extension_id;

    /* Critical flag - boolean value. */
    USHORT nx_secure_x509_extension_critical;

    /* Pointer to DER-encoded extension data. */
    const UCHAR *nx_secure_x509_extension_data;
    ULONG        nx_secure_x509_extension_data_length;
} NX_SECURE_X509_EXTENSION;
```
Hizmet başarıyla geri döndüğünde, yapı sertifikadaki ilgili verilerle doldurulur. Nx_secure_x509_extension_id alanı genellikle dahili amaçlar için kullanılır, ancak ilgili OID tamsayı temsili ile doldurulur. Nx_secure_x509_extension_critical alanı X. 509.440 kritik uzantı bayrak değerini (Boolean) kullanıma sunar. Nx_secure_x509_extension_data ve nx_secure_x509_extension_data_length alanları, uzantı için DER ile kodlanmış ASN. 1 verisi ve bu verilerin sırasıyla uzunluğu ile ilgili bir işaretçi içerir.

ASN. 1 veri uzantısının gerçek ayrıştırması bu belgenin kapsamının ötesinde, ancak NetX güvenli TLS kaynağına erişiminiz varsa, desteklenen uzantılar için nx_secure_x509_extension_find çağrıldığı her yerde ayrıştırmayı nasıl yapılacağını görebilirsiniz.

### <a name="x509-dns-validation"></a>X. 509.440 DNS doğrulaması

TLS 'de ortak bir sertifika doğrulama işlemi, uzak bir ana bilgisayarın Top-Level etki alanı (TLD) adının TLS el sıkışması sırasında bu konak tarafından sağlanmış X. 509.440 sertifikasına göre denetlenmesini içerir. Bu işlem, DNS aramasına güvenildiğini varsayarak sertifikanın gerçekten onu sağlayan ana bilgisayar sunucusuyla eşleştiğinden emin olmaya yardımcı olur. NetX güvenli TLS 'de, bu işlevsellik, sertifikayı ve konağa erişmek için kullanılan URL 'nin TLD bölümünü içeren bir dizeyi alan hizmet **nx_secure_x509_common_name_dns_check** tarafından sağlanır. TLD, sertifikanın ortak ad alanıyla karşılaştırılır ve eşleşiyorsa NX_SUCCESS döndürülür. Ortak ad eşleşmiyorsa, yordam ayrıca X. 509.440 sertifika uzantısının *SubjectAltName* olup olmadığını denetler. Bir subjectAltName varsa, uzantıdaki herhangi bir DNSName girdisi de belirtilen TLD 'ye karşı denetlenir. Bir eşleşme varsa, NX_SUCCESS döndürülür. Eşleşme bulunmazsa, sertifika doğrulama geri çağrısından dönmek için uygun bir hata döndürülür.

### <a name="x509-key-usage-and-extended-key-usage-extensions"></a>X. 509.440 anahtar kullanımı ve genişletilmiş anahtar kullanımı uzantıları

X. 509.952 anahtar kullanımı ve genişletilmiş anahtar kullanımı uzantıları, sertifikanın kimliğini doğrularken sertifikanın ortak anahtarının nasıl kullanılabileceği hakkında bilgi sağlar. Anahtar kullanımı, sertifika imzalanmışsa ve verildiğinde sertifikanın veren tarafından sağlanır. Anahtar kullanımı, bir TLS ana bilgisayarı tarafından uzak bir TLS ana bilgisayarının kimliğini doğrulamak ve diğer işlemleri gerçekleştirmek için kullanılacak yetkiye sahip olup olmadığını denetlemek için kullanılabilir.

Anahtar kullanımı uzantısı, her bir bitlerin belirli bir anahtar kullanımını temsil ettiği bir basit bitalanından oluşur. Bu değerlerin tüm listesi, 183 sayfasında *nx_secure_x509_key_usage_extension_parse* için API başvurusunda verilmiştir. Anahtar kullanımı bitlerinin ve anlamları hakkında daha ayrıntılı bir açıklama için bkz. RFC 5280, Bölüm 4.2.1.3.

Anahtar kullanımı uzantısı gibi genişletilmiş anahtar kullanımı uzantısı, kabul edilebilir anahtar kullanımı bilgilerini sağlar. Ancak, rastgele kullanımları desteklemek için, genişletilmiş anahtar kullanımı uzantısı bir bit alanı yerine OID 'leri kullanır. NetX güvenli X. 509.440 içinde genişletilmiş anahtar kullanımı uzantısını ayrıştırırken, uygulama tarafından OID 'yi temsil eden bir tamsayı sağlanır. *nx_secure_x509_extended_key_usage_extension_parse* hizmet daha sonra bu OID 'nin mevcut olup olmadığını döndürür. Genişletilmiş anahtar kullanımı için desteklenen OID 'lerin tamamı, sayfa 175 ' de *nx_secure_x509_extended_key_usage_extension_parse* için API başvurusunda verilmiştir. OID 'lerin ve anlamları hakkında daha ayrıntılı bir açıklama için, RFC 5280, Bölüm 4.2.1.12 bakın.

### <a name="x509-crl-revocation-status-checking"></a>X. 509.440 CRL Iptal durumu denetimi

X. 509.440, dijital bir sertifika imzalama yetkilisinin imzalandığı sertifikaların geçerliliğini iptal etmesine izin veren, *sertifika Iptal listesi* (CRL) adlı bir mekanizma sağlar. İmza yetkilisinden sertifikaları doğrulaması gereken herhangi bir uygulama, bir CRL alabilir ve bu yetkilinin (veren), belirli bir nedenden dolayı (güvenliği aşılmış özel anahtar gibi) durumunun iptal edilip edilmediğini görmek için CRL 'ye karşı imzalanan tüm sertifikaları karşılaştırabilir. Bu şekilde, uygulama diğer sertifika doğrulama denetimlerini geçiren potansiyel olarak tehlikeli sertifikaları kullanmaktan kaçınabilir.

Bir CRL alma, bir uygulama tarafından, önceden tanımlanmış bir sunucudan ya da başka bir yöntemle DER kodlu liste indirerek yapılır. Asıl kurulum, verenin sertifikayı verene göre farklılık gösterir. bu nedenle, NetX güvenliği CRL 'Leri almak için bir mekanizma sağlamaz, ancak bir CRL 'ye karşı sertifikayı denetlemek için bir yordam sağlar, **nx_secure_x509_crl_revocation_check**.

API, DER ile kodlanmış bir CRL, bir sertifika deposu (bir TLS oturumunda olduğu gibi) ve denetlenecek sertifikayı alır. Bu yordam ilk olarak CRL 'YI güvenilir depoya (uygulama tarafından belirtilen sertifika deposunun parçası) karşı doğrular. Bu, hizmet reddi saldırıları için kullanılan sahte CRL 'Lere karşı koruma için önemlidir ve CRL 'nin gerçekten uygun veren tarafından geldiğinden emin olur. CRL doğrulamasından sonra, veren denetlenir: CRL veren, sertifikanın verenle eşleşmiyorsa, CRL Bu sertifika için geçerli değildir ve bir hata döndürülür. Bu noktada TLS el sıkışma 'nın devam edip edemeyeceğini tespit etmek için uygulamaya gidin. Verenler eşleşiyorsa, doğrulanan sertifikanın seri numarası için CRL aranır. Listede seri numarası varsa, sertifikanın iptal edildiğini belirten bir hata döndürülür. Eşleşme bulunmazsa NX_SUCCESS döndürülür.

## <a name="client-certificate-authentication-in-netx-secure-tls"></a>NetX güvenli TLS 'de istemci sertifikası kimlik doğrulaması

X. 509.440 sertifika kimlik doğrulaması kullanılırken, TLS protokolü, TLS sunucu örneğinin tanımlama için bir sertifika sağlamasını gerektirir, ancak varsayılan olarak TLS Istemci örneğinin kimlik doğrulama için bir sertifika sağlaması gerekmez, bunun yerine başka bir kimlik doğrulama biçimi (örn. bir Kullanıcı adı/parola birleşimi) kullanın. Bu, Web siteleri için Internet 'te en yaygın TLS kullanımıyla eşleşir. Örneğin, bir çevrimiçi perakende sitesi, sunucunun meşru olduğunu bir Web tarayıcısı kullanarak potansiyel bir müşteriyi kanıtlamaları gerekir, ancak kullanıcı belirli bir hesaba erişmek için bir oturum açma/parola kullanacaktır.

Ancak, varsayılan durum her zaman tercih edilmez, bu nedenle TLS sunucu örneğinin uzak Istemciden bir sertifika istemesine izin verir. Bu özellik etkinleştirildiğinde, TLS sunucusu el sıkışma sırasında TLS Istemcisine bir CertificateRequest iletisi gönderir. Istemci kendi sertifikası ile yanıt vermelidir ve Istemcinin bu sertifikayla ilişkili eşleşen özel anahtara sahip olduğunu belirten bir şifreleme belirteci içeren bir CertificateVerify iletisi. Doğrulama başarısız olursa veya sertifika sunucuda güvenilir bir sertifikaya bağlı değilse, TLS el sıkışması başarısız olur.

TLS 'de Istemci sertifikası kimlik doğrulaması için iki ayrı durum vardır: aşağıdaki bölümlerde her iki durum da ele alınmaktadır.

### <a name="client-certificate-authentication-for-tls-clients"></a>TLS Istemcileri için istemci sertifikası kimlik doğrulaması

TLS Istemcisi, istemci kimlik doğrulaması için bir sertifika isteyen bir sunucuyla bağlantı kurmayı deneyebilir. Bu durumda, Istemcinin sunucuya bir sertifika sağlaması ve eşleşen özel anahtara sahip olduğunu doğrulaması gerekir ya da sunucu, TLS el sıkışmasını sonlandırır.

NetX güvenli TLS 'de, bu özelliği desteklemeye yönelik özel bir yapılandırma yoktur, ancak uygulamanın *nx_secure_tls_local_certificate_add* HIZMETINI kullanarak TLS istemci örneği için bir yerel kimlik sertifikası sağlaması gerekecektir. Uygulama tarafından bir sertifika sağlanmazsa ancak uzak sunucu Istemci sertifikası kimlik doğrulamasını kullanıyorsa ve bir sertifika isterse, TLS el sıkışması başarısız olur. *Nx_secure_tls_local_certificate_add* Ile tls oturumuna girilen SERTIFIKA, TLS el sıkışma 'nı tamamlayabilmeniz için uzak sunucu tarafından tanınmalıdır.

### <a name="client-certificate-authentication-for-tls-servers"></a>TLS sunucuları için istemci sertifikası kimlik doğrulaması

Istemci sertifikası kimlik doğrulaması için TLS sunucu durumu, özelliğin isteğe bağlı olması nedeniyle TLS Istemci durumundan biraz daha karmaşıktır. Bu durumda, TLS sunucusunun özel olarak uzak TLS Istemcisinden bir sertifika istemesi, ardından uzak Istemcinin eşleşen özel anahtara sahip olduğunu doğrulamak için CertificateVerify iletisini işlemesi gerekir ve ardından sunucu, Istemci tarafından belirtilen sertifikanın, yerel güvenilen sertifika deposundaki bir sertifikaya izlenip izlenmeyeceğini denetmelidir.

NetX güvenli TLS sunucu örneklerinde Istemci sertifikası kimlik doğrulaması tarafından denetlenir <br>
*NX <span class="underline"> _</span> güvenli <span class="underline">_</span>TLS <span class="underline"> _</span> oturumu <span class="underline">_</span>istemcisi <span class="underline"> _</span> doğrulama <span class="underline">_</span>etkinleştirme* ve<br>
*NX <span class="underline"> _</span> güvenli <span class="underline">_</span>TLS <span class="underline"> _</span> oturum <span class="underline">_</span>istemcisi <span class="underline"> _</span> Doğrula <span class="underline">_</span>hizmetleri devre dışı bırak* .

Istemci sertifikası kimlik doğrulamasını etkinleştirmek için bir uygulamanın şunu çağırması gerekir<br>
*NX <span class="underline"> _</span> güvenli <span class="underline">_</span>tls <span class="underline"> _</span> oturum <span class="underline">_</span>istemcisi <span class="underline"> _</span> Verify <span class="underline">_</span>* *nx_secure_tls_session_start* çağrılmadan önce TLS sunucusu oturum örneğiyle etkinleştirin. Bu hizmeti TLS Istemci bağlantıları için kullanılan bir TLS oturumunda çağırmanın hiçbir etkisi olmayacaktır.

Istemci sertifikası kimlik doğrulaması etkinleştirildiğinde, TLS sunucusu, TLS el sıkışması sırasında uzak TLS Istemcisinden bir sertifika ister. NetX güvenli TLS sunucusunda, Istemci sertifikası *nx <span class="underline"> _</span> <span class="underline">_ secure_tls</span>güvenilen <span class="underline"> _</span> <span class="underline">_ sertifika</span>* ile oluşturulan güvenilen sertifikaların deposuna göre denetlenir ve X. 509.440 veren zincirini aşağıdaki şekilde ekleyin. Uzak Istemci, kimlik sertifikasını Güvenilen depodaki bir sertifikaya bağlayan bir zincir sağlamalıdır veya TLS el sıkışması başarısız olur. Ayrıca, CertificateVerify iletisi işlemi başarısız olursa, TLS el sıkışması da başarısız olur.

CertificateVerify yöntemi için kullanılan imza yöntemleri TLS sürüm 1,0 ve TLS sürüm 1,1 için düzeltilir ve TLS sunucusu tarafından TLS sürümü 1,2 olarak belirtilir. TLS 1,2 için, desteklenen imza yöntemleri genellikle şifreleme yöntemi tablosunda sağlanan ilgili yöntemleri izler, ancak genellikle SHA-256 ile RSA (şifreleme yöntemleriyle TLS başlatma hakkında daha fazla bilgi için bkz. "NetX güvenli TLS 'de şifreleme" bölümüne bakın).

## <a name="cryptography-in-netx-secure-tls"></a>NetX güvenli TLS 'de şifreleme

TLS, ağ iletişimlerini güvenli hale getirmek için şifreleme kullanılabilecek bir protokol tanımlar. Bu nedenle, TLS kullanıcıları için oldukça geniş kapsamlı açık kullanılacak şekilde gerçek şifrelemeyi bırakır. Belirtim yalnızca tek bir ciphersuite 'in uygulanması için gereklidir; TLS 1,2 olması durumunda bu ciphersuite TLS_RSA_WITH_AES_128_CBC_SHA, ortak anahtar işlemleri için RSA kullanımını ve oturum şifreleme için 128 bit anahtarlarla CBC modunda AES modunu ve ileti kimlik doğrulama karmaları için SHA-1 ' i belirtir.

TLS 1,2 uyumlu olduğu, NetX güvenliği, zorunlu TLS_RSA_WITH_AES_128_CBC_SHA ciphersuite 'i varsayılan olarak sağlar, ancak donanım özellikleri ve diğer hususlar nedeniyle her bir şifreleme yöntemi için olası uygulama sayısına veriliyorsa, NetX güvenliği, kullanıcının TLS ile hangi şifreleme yöntemlerinin kullanılacağını belirtmesini sağlayan bir genel şifreleme API 'SI sağlar.

NOTE: genel şifreleme API mekanizması, kullanıcıların kendi cipherpaketlerini uygulamasına olanak tanır, ancak bu, TLS cipherpaketlerine ve uzantılarına alışkın olan ileri düzey kullanıcılar için önerilir. Kendi cipherpaketlerinizi desteklemeye ilgileniyorsanız lütfen hızlı mantık temsilcinizle iletişime geçin.

### <a name="cryptographic-methods"></a>Şifreleme yöntemleri

NetX güvenli TLS, belirli donanım platformları için donanım sürücüleri olan yazılımda DES, 3DES, AES, MD5, HMAC-MD5, SHA-1, HMAC-SHA1, SHA-256, HMAC-SHA256, RSA ve ECC (seçili eğrileri) uygular. Bir uygulama NetX güvenli ile birlikte sunulan şifreleme yordamlarını kullanabilir veya son kullanıcı ya da üçüncü taraflar tarafından sunulan özel yordamları kullanabilir.

*NX_CRYPTO_METHOD* , bir uygulama Için, NETX güvenli TLS ile kullanılmak üzere bir şifreleme algoritmasının belirli bir uygulamasını açıklamaya yönelik olarak tasarlanmış bir denetim bloğudur. NX_CRYPTO_METHOD bir uygulama *,* kendi şifre uygulamasını güvenle NETX güvenli bir şekilde tümleştirebilir. *NX_CRYPTO_METHOD* yapısı şöyle bildirilmiştir:

```C
typedef struct NX_CRYPTO_METHOD_STRUCT
{
    /* Symbolic name of the algorithm. */
    USHORT nx_crypto_algorithm;

    /* Size of the key, in bits. */
    USHORT nx_crypto_key_size_in_bits;

    /* Size of the IV block, in bits, used for encryption. */
    USHORT nx_crypto_IV_size_in_bits;

    /* Size of the ICV block, in bits, used for authentication. */
    USHORT nx_crypto_ICV_size_in_bits;

    /* Size of the crypto block, in bytes. */
    ULONG nx_crypto_block_size_in_bytes;

    /* Size of the metadata area. */
    ULONG nx_crypto_metadata_size;

    /* nx_crypto_init function initializes the crypto method with the
        "secret key" or other state  information. The initialization 
        routine should return a handle to the caller.  This handle is 
        used in subsequent crypto operations to identify the session.  
        */

    UINT (*nx_crypto_init) (NX_CRYPTO_METHOD     *method,
                            UCHAR               *key, 
                            NX_CRYPTO_KEY_SIZE   key_size_in_bits,
                            VOID               **handler,
                            VOID                *crypto_metadata,
                            VOID                 crypto_metadata_size);

    /* NetX Secure calls the nx_crypto_cleanup routine when a TLS
       session is to be deleted (or updated).  Resources allocated 
       during the crypto operation should be released in this routine.  
       */
    UINT (*nx_crypto_cleanup) (VOID *handler);

    /* nx_crypto_operation is the actual crypto or hash operation. Note 
       that both input and output buffers are prepared by the caller. 
       For encryption or decryption operations, the crypto operation 
       routine uses the output buffer for encrypted or decrypted data. 
       For authentication operations, the authentication routine shall 
       use the output buffer for the digest. */
    UINT (*nx_crypto_operation)(UINT  op, 
                  VOID              *handler, 
                  NX_CRYPTO_METHOD  *method,
                  UCHAR             *key,
                  NX_CRYPTO_KEY_SIZE key_size_in_bits,
                  UCHAR             *input,
                  ULONG              input_length_in_byte,
                  UCHAR             *iv_ptr,
                  UCHAR             *output,
                  ULONG              output_length_in_byte,
                  VOID              *crypto_metadata,
                  VOID               crypto_metadata_size,
                  NX_PACKET*         packet_ptr,
                  VOID (*nx_crypto_hw_process_callback(NX_PACKET 
                                                       *packet_ptr, 
                                                        UINT status);
} NX_CRYPTO_METHOD;
```

*NX_CRYPTO_METHOD* yapısındaki her öğenin açıklaması aşağıda verilmiştir:

- nx_crypto_algorithm: Bu alan, değişken *yönteminde* açıklanan algoritmayı tanımlar NETX güvenli TLS için bazı geçerli değerler aşağıdaki gibidir (belirli değerler için nx_crypto_const. h öğesine bakın):
    
  - NX_CRYPTO_NONE    
  - NX_CRYPTO_ENCRYPTION_NULL    
  - NX_CRYPTO_ENCRYPTION_AES_CBC    
  - NX_CRYPTO_AUTHENTICATION_NONE    
  - TLS_HASH_SHA_1    
  - TLS_HASH_SHA_256    
  - TLS_HASH_MD5    
  - TLS_CIPHER_RSA    
  - TLS_CIPHER_NULL

- nx_crypto_key_size_in_bits: Bu alan, yöntemi tarafından kullanılan gizli anahtarın boyutunu belirtir.

- nx_crypto_IV_size_in_bits: Bu alan, başlatma vektörünün (IV) boyutunu belirtir. Çoğu durumda IV bloğunun yalnızca şifreleme/şifre çözme algoritmaları için kullanıldığını unutmayın. Kimlik doğrulama ve doğrulama algoritmaları nadiren bu alanı kullanır.

- nx_crypto_ICV_size_in_bits: Bu alan, bütünlük denetim değeri (ıCV) bloğunun boyutunu belirtir. NOTE: Bu blok IPSec kullanımına yöneliktir ve TLS 'de kullanılmaz. Daha fazla bilgi için bkz. NetX Duo IPSec.

- nx_crypto_block_size_in_bytes: Bu alan, blok tabanlı şifrelemeler için şifreleme algoritması bloğunun boyutunu bayt cinsinden belirtir. Çoğu durumda bu, şifreleme yordamları ve nadiren kimlik doğrulama yordamları tarafından kullanılır.

- nx_crypto_metadata_area_size: Bu alan, bu yöntemin gerektirdiği meta veri alanının boyutunu belirtir. Her uygulama, bazı belleğin durum bilgilerini depolamasını veya ara verileri (örneğin, anahtar dönüştürme malzemesi) depolamasını veya bir karalama alanı olarak kullanılmasını gerektirebilir. Bu alanda bir uygulama için gereken alan miktarı belirtilir. Uygulama, bir TLS oturumu oluştururken bellek alanı sağlar. Bu meta veri alanını yönetmeden şifreleme işlevi sorumludur.

- nx_crypto_init: Bu, şifreleme algoritmasının başlatma işlevidir. Başlatma yordamına gerek gerektirmeyen bir uygulama için, bu alan NX_NULL olarak ayarlanabilir. Başlatma işlevinin tipik kullanımı, algoritmanın iç veri yapısını başlatmasıdır. NetX güvenli TLS, bu işlevi dahili olarak çağırarak şifreleme yordamının başlatılmasını işleymeyecektir.

Başlatma işlevinin prototipi şunlardır:

```C
UINT crypto_init_function(NX_CRYPTO_METHOD *method, 
                          UCHAR *key, 
                          UINT  key_size_in_bits, 
                          VOID  **handle, 
                          VOID  *crypto_metadata_area, 
                          ULONG crypto_metadata_area_size);
```

  - yöntemi, şifreleme yöntemi denetim bloğunun bir işaretçisidir.

  - anahtar, veri paketlerini işlemek için gizli anahtar dizesidir.

  - key_size_in_bits, gizli anahtarın bit cinsinden boyutunu tanımlar.

  - tanıtıcı, belirli bir şifre oturumunu tanımlayan uygulama tanımlı bir öğedir. Değer, başlatma yordamı tarafından oluşturulur ve çağırana geri geçirilir. Sonraki şifreleme işlemi veya temizleme yordamı, oturumu belirlemek için bu tanıtıcıyı kullanır.

  - crypto_metadata, bu algoritmanın uygulanması için gerekli olan meta veri alanına yönelik bir işaretçidir. Meta veri alanı gerektirmeyen algoritmalar için bu alan NX_NULL olarak ayarlanır ve başlatma yordamı meta veri alanına erişmemelidir.

  - crypto_metadata_size meta veri alanının boyutunu belirtir. Meta veri alanı olmadan oluşturulan SAs için, bu alan sıfır olarak ayarlanır ve başlatma yordamı meta veri alanına erişmemelidir.

  - Başlatma işlemi başarılı olursa bu yordam *NX_SUCCESS* döndürür. Çağıran, diğer tüm dönüş değerlerini hata olarak değerlendirir.

- nx_crypto_cleanup: Bu, bir şifreleme algoritmasının uygulanması için tanımlanan Temizleme yordamlamasıdır. Bir TLS oturumu silindiğinde veya yeniden başlatıldığında çağrılır.

Temizleme işlevinin prototipi şunlardır:

```C
UINT crypto_cleanup_function(VOID *handle);
```
- tanıtıcı, çağıran tarafından Temizleme işlevine geçirilir. Tanıtıcı, şifreleme başlatma yordamı tarafından başlatılır ve şifreleme algoritması durumunu tanımlamak için kullanılır.

- Temizleme işlemi başarılı olursa bu yordam *NX_SUCCESS* döndürür. Çağıran, diğer tüm dönüş değerlerini hata olarak değerlendirir.

- nx_crypto_operation: Bu, gerçek şifreleme, şifre çözme ve kimlik doğrulama hizmetlerini gerçekleştiren bir yordamdır. İşlem yordamının işlev prototipi şunlardır:

```C
UINT crypto_operation_function(UINT   op,
          VOID  *handle,  
          NX_CRYPTO_METHOD* method,
          UCHAR *key,
          UCHAR  key_size_in_bits,
          UCHAR* input,
          ULONG  input_length_in_byte,
          UCHAR* iv_ptr,
          UCHAR* output,
          ULONG  output_length_in_byte,
          VOID *crypto_metadata,
          ULONG crypto_metadata_size,
          NX_PACKET *packet_ptr,
          VOID (*nx_crypto_hw_process_callback)(NX_PACKET 
                          *packet_ptr, UINT status));
```

- Op, bu yordamın yürütülmesi beklenen işlem türünü gösterir. Geçerli değerler şunlardır:
    
    - NX_CRYPTO_ENCRYPT
    - NX_CRYPTO_DECRYPT
    - NX_CRYPTO_AUTHENTICATE
    - NX_CRYPTO_VERIFY

- tanıtıcı, çağıran tarafından işlem işlevine geçirilir. Şifre başlatma yordamı tarafından oluşturulur.
- Yöntem, şifreleme yöntemi denetim bloğuna işaret ediyor
- anahtar, bu işlem için kullanılan gizli anahtara işaret ediyor
- key_size_in_bits, bit cinsinden gizli anahtar boyutudur
- Giriş, üzerinde çalışılan iletinin başlangıcına yönelik bir işaretçidir.
- input_length_in_byte, üzerinde işletiedilecek iletinin boyutunu belirtmek için çağıran tarafından geçirilir.
- iv_ptr, çağıran tarafından bir IV bloğunun başlangıcına işaret etmek üzere ayarlanır. IV bloğunun belleğinin arayan tarafından sağlandığını unutmayın. Şifreleme için, işlem işlevi bu bellek bloğuna IV bilgilerini yazmalıdır; şifre çözme için, işlem işlevi bu bellek bloğundan IV bilgilerini almalıdır. Kimlik doğrulama ve doğrulama işlemi algoritmaları genellikle başlatma vektörünü kullanmaz.
- çıktı, çağrı tarafından çıkış arabelleğini işaret etmek üzere ayarlanır. Çıktı arabelleği için bellek, çağıran tarafından sağlanır. Şifreleme için, işlem işlevi şifre metnini çıkış arabelleğine yazmalıdır; şifre çözme için, işlem arabelleğe alınan metni (şifresiz metin) çıkış arabelleğine yazmalıdır; kimlik doğrulaması için, karma değeri çıkış arabelleğine yazılır. Doğrulama için, çıkış arabelleği karma bilgileri depolamak için kullanılır.
- output_length_in_byte, çıkış arabelleğinin boyutunu gösterir
- crypto_metadata, bu şifreleme işlemi tarafından kullanılacak meta veri alanına işaret eder. Şifreleme meta verileri alanı genellikle crypto_init_function tarafından başlatılır.
- crypto_metadata_size meta veri alanının boyutunu gösterir.
- İşlem işlemi başarılı olursa bu yordam *NX_SUCCESS* döndürür. Çağıran, diğer tüm dönüş değerlerini hata olarak değerlendirir.
- packet_ptr: işlenmekte olan verileri içeren paket. NOTE: Bu parametre TLS tarafından kullanılmıyor ve NX_NULL olarak ayarlanmalıdır.
- nx_crypto_hw_process_callback: şifreleme yöntemi tarafından sağlanmış bir geri çağırma işlevi. Bu, şifreleme işlevi donanım tarafından sağlandıysa ve bir geri çağırma yordamı gerektiriyorsa kullanılır.

NetX güvenli TLS aşağıdaki şifreleme yöntemlerini sağlar:

- *AES*  
- *RSA*  
- *DEĞER*

NetX güvenli TLS aşağıdaki kimlik doğrulama yöntemlerini sağlar:

- *HMAC-MD5*  
- *HMAC-SHA1*  
- *HMAC-SHA256*

Aşağıdaki örneklerde, *NX_CRYPTO_METHOD* yapısının NETX Duo IPSec tarafından sunulan şifreleme ve kimlik doğrulama yöntemlerini kullanmak üzere nasıl yapılandırılacağı gösterilmektedir.

***AES***

```C
/* AES-CBC 128. */
NX_CRYPTO_METHOD crypto_method_aes_cbc_128 = 
{
    /* AES crypto algorithm                             */
    NX_CRYPTO_ENCRYPTION_AES_CBC,                       

    /* Key size in bits. For AES-128 this value is 128  */
    NX_CRYPTO_AES_128_KEY_LEN_IN_BITS,              
   
    /* IV size in bits.  For AES-128 this value is 128  */
    NX_CRYPTO_AES_IV_LEN_IN_BITS,

    /* ICV size in bits, not used.                      */
    0,                                              

    /* Block size in bytes.  For AES this value is 16   */
    (NX_CRYPTO_AES_BLOCK_SIZE_IN_BITS >> 3),        

    /* Metadata size in bytes, for AES this value is 262*/
    sizeof(NX_CRYPTO_AES),              

    /* AES-CBC initialization routine.                  */
    _nx_secure_crypto_method_aes_init,               

    /* AES-CBC cleanup routine, not used.               */
    NX_NULL,                                        

    /* AES-CBC operation                                */
    _nx_secure_crypto_method_aes_operation           
};

/* RSA. */
NX_CRYPTO_METHOD crypto_method_rsa = 
{
    /* RSA crypto algorithm                             */
    TLS_CIPHER_RSA,                       

    /* Key size. RSA key sizes vary, so set to 0.         */
    0,              
   
    /* IV size in bits.  RSA does not use an IV.         */
    0,

    /* ICV size in bits, not used.                      */
    0,                                              

    /* Block size in bytes.  RSA does not have a block size. */
    0,        

    /* Metadata size in bytes, for RSA use the control block. */
    sizeof(NX_CRYPTO_RSA),              

    /* RSA initialization routine.                  */
    _nx_secure_crypto_method_rsa_init,               

    /* Cleanup routine, not used.                    */
    NX_NULL,                                        

    /* RSA operation                                */
    _nx_secure_crypto_method_rsa_operation           

};
```
***DEĞER***

```C
/* NULL encryption method. */
NX_CRYPTO_METHOD crypto_method_null = 
{
    NX_CRYPTO_ENCRYPTION_NULL,/* Name of the crypto algorithm  */
    0,                        /* Key size in bits, not used    */
    0,                        /* IV size in bits, not used     */
    0,                        /* ICV size in bits, not used    */
    4,                        /* Block size in bytes           */
    0,                        /* Metadata size in bytes        */
    NX_NULL,                  /* Initialization routine,unused */
    NX_NULL,                  /* Cleanup routine, not used     */
    _nx_secure_crypto_method_null_operation  /* NULL operation  
*/
}; 
```
***HMAC-SHA1***
```C
NX_CRYPTO_METHOD crypto_method_hmac_sha1 = 
{
    /* HMAC SHA1 algorithm                               */
    TLS_HASH_SHA1,            


    /* Key size in bits. For HMAC-SHA1 this value is 160 */ 
    NX_CRYPTO_HMAC_SHA1_KEY_LEN_IN_BITS,              

    /* IV size in bits, not used                         */
    0,                                            

    /* Transmitted ICV size in bits. Unused.             */
    0, 

    /* Block size in bytes, not used                     */
    0,                                            

    /* Metadata size in bytes                            */
    sizeof(NX_SHA1_HMAC),                                            

    /* Initialization routine, not used                  */
    NX_NULL,                                      

    /* Cleanup routine, not used                         */
    NX_NULL,                                          

    /* HMAC SHA1 operation                               */
    _nx_secure_crypto_method_hmac_sha1_operation   
};
```
***SEÇIM***

Şifreleme veya kimlik doğrulama hizmetinin gerekli olmadığı IPSec modülüne işaret etmek için **NX_CRYPTO_NONE** özel bir yöntem kullanılır. Aşağıdaki şekilde yapılandırılır:

```C
/* NX_CRYPTO_NONE means encryption or authentication
   method is not needed.  */
NX_CRYPTO_METHOD crypto_method_none = 
{
    NX_CRYPTO_NONE,       /* Name of the crypto algorithm */
    0,                    /* Key size in bits, not used   */
    0,                    /* IV size in bits, not used    */
    0,                    /* ICV size in bits, not used   */
    0,                    /* Block size in bytes          */
    0,                    /* Metadata size in bytes       */
    NX_NULL,              /* Initialization routine, not used */
    NX_NULL,              /* Cleanup routine, not used    */
    NX_NULL               /* NULL operation               */
};                                               
```
### <a name="initializing-tls-with-cryptographic-methods"></a>Şifreleme yöntemleriyle TLS başlatma

Önceki bölümde açıklanan şifreleme yöntemi imzaları ile uyumlu olan şifreleme yordamlarınızı oluşturduktan sonra, bir NX_SECURE_TLS_SESSION denetim bloğu başlattığınızda bu uygulamaları TLS 'ye geçirmeniz gerekir. Bu işlem TLS hizmeti nx_secure_tls_session_create yapılır:

```C
UINT  nx_secure_tls_session_create(
              NX_SECURE_TLS_SESSION*     session_ptr,
              const NX_SECURE_TLS_CRYPTO*    tls_cipher_table,
              VOID*                encryption_metadata_area,
              ULONG                 encryption_metadata_size
);
```
- session_pointer, NX_SECURE_TLS_SESSION denetim blobunun bir işaretçisidir.
- tls_cipher_table, aşağıda açıklanan NX_SECURE_TLS_CRYPTO denetim bloğunun bir işaretçisidir.
- encryption_metadata_area, TLS 'de şifreleme yordamları tarafından kullanılan alana işaret eder.
- encryption_metadata_size, meta veri alanının bayt cinsinden boyutudur.

### <a name="elliptic-curve-cryptography-ecc-in-netx-secure-tls"></a>NetX güvenli TLS 'de Eliptik Eğri Şifreleme (ECC)

Eliptik Eğri Şifreleme (ECC), RSA yerine kullanılabilecek bir ortak anahtar şifreleme şeması sağlar. ECC genellikle daha hızlıdır ve RSA 'dan daha küçük anahtarlar kullanır, böylece gömülü TLS için değerli bir seçenek olabilir. Azure RTOS 6,0 ' den önceki X-Ware sürümlerinde ECC, ECC kaynak kodunun projenize yüklenmesini gerektiren bir eklenti olarak gönderilmiştir. Azure RTOS 6,0, ana hat kod tabanına tümleştirilmiş ECC dosyalarını yüklemek artık gerekli değildir. Ancak, ECC hala önceki sürümlerle aynı başlatmayı gerektirir.

### <a name="supported-ecc-curves"></a>Desteklenen ECC eğrileri

NetX Secure, eğrilerin parçalarını göre uygular <http://www.secg.org/sec2-v2.pdf> . Aşağıdaki eğriler desteklenir<sup>18</sup>:

  - secp256r1 
  - secp384r1 
  - secp521r1 

Diğer ECC eğrileri kullanılıyorsa, *nx_secure_tls_session_start ()* yordamı, desteklenmeyen eğrilerin kullanıldığını belirten NX_SECURE_TLS_NO_SUPPORTED_CIPHERS hata döndürür.

TLS sertifika zincirinin de ECC algoritmalarıyla şifrelendiğini unutmayın. TLS Istemcisi tarafından sunulan eğriler desteklense de, sertifika zincirinde kullanılan ECC eğrisi desteklenmez. Bu durumda, *nx_secure_tls_session_start* rutin NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER döndürür.

Nx_crypto_generic_ciphersuites. c ' de ECC için varsayılan ciphersuite tablosu örneği verilmiştir. Ciphersuite tabloları hakkında daha fazla bilgi için bkz. "TLS şifreleme şifre tablosu" bölümü.

18. Secp192r1 ve secp224r1are eğrileri için uygulamaların eski uygulamalar için de sağlandığını unutmayın. Ancak bu eğriler artık zayıf olarak değerlendirilir ve yeni uygulama geliştirme için kullanılmamalıdır.

### <a name="crypto-methods-for-ecc"></a>ECC için şifreleme yöntemleri

Eliptik Eğri grupları için şifreleme yöntemleri:

- NX_CRYPTO_METHOD crypto_method_ec_secp192<sup>15</sup>;  
- NX_CRYPTO_METHOD crypto_method_ec_secp224<sup>15</sup>;  
- NX_CRYPTO_METHOD crypto_method_ec_secp256;  
- NX_CRYPTO_METHOD crypto_method_ec_secp384;  
- NX_CRYPTO_METHOD crypto_method_ec_secp521;

ECC eğrilerinin şifre yöntemleri nx_crypto_generic_ciphersuites. c ' de tanımlanmıştır.

ECDHE için şifreleme yöntemi:

- NX_CRYPTO_METHOD crypto_method_ecdhe;

ECDSA için şifreleme yöntemi:

- NX_CRYPTO_METHOD crypto_method_ecdsa;

ECDSA ve ECDHE şifreleme yöntemleri nx_crypto_generic_ciphersuites. c ' de tanımlanmıştır.

RSA, SHA, AES gibi diğer şifre yöntemleriyle birlikte birleştirildiğinde, ciphersuite arama tablosu için yapı taşları olarak kullanılabilirler.

### <a name="enabling-ecc-support-for-tls"></a>TLS için ECC desteğini etkinleştirme

ECC, TLS için varsayılan olarak etkindir. ECC desteğini devre dışı bırakmak için NX_SECURE_DISABLE_ECC_CIPHERSUITE sembol tanımlanmalıdır.

Değişikliğin etkili olması için, NetX güvenli kitaplığını ve bu kitaplığı kullanan tüm uygulamaları yeniden oluşturmanız gerekir.

Uygulama kodunda, TLS oturumu oluşturulduktan sonra API n *x_secure_tls_ecc_initialize ()* çağrılmalıdır. Bu API, TLS anahtar değişimi işlemleri ve sertifika doğrulaması için kullanılacak eğrilerin türünü TLS oturumuna bildirir. TLS el sıkışma aşamasında, bir ECC algoritması seçilirse, hangi eğrinin kullanılacağına karar vermek için istemci ve sunucu Exchange ECC eğrisi ile ilgili parametreleri seçilir.

Aşağıdaki kod segmenti, API 'nin nasıl kullanılacağını gösterir. Bağımsız değişkenlerin (*nx_crypto_ecc_supported_groups, nx_crypto_ecc_supported_groups_size ve nx_crypto_ecc_curves)* tümünün *nx_crypto_generic_ciphersuites. c* içinde tanımlandığını unutmayın. Bu nedenle, bu semboller doğrudan kullanılabilir.

```C
status = nx_secure_tls_ecc_initialize(&tls_session,     
                    nx_crypto_ecc_supported_groups,      
                    nx_crypto_ecc_supported_groups_size,     
                    nx_crypto_ecc_curves);
```
Nx_crypto_generic_ciphersuites. c ' deki örnek yapılandırma, ECC etkinleştirildiğinde kullanılan bir ECC ciphersuite arama tablosu içerir. ECC kullanmak için, nx_secure_tls_session_create ile TLS oturumları oluştururken nx_crypto_tls_ciphers_ecc ciphersuite tablo parametresi olarak geçirin. Örnek tablo hem ECC hem de ECC olmayan cipherpaketleri içerir.

### <a name="tls-cryptographic-cipher-table"></a>TLS şifreleme şifre tablosu

NX_SECURE_TLS_CRYPTO yapısı şu şekilde tanımlanır:

```C
typedef struct NX_SECURE_METHODS_STRUCT
{
    /* Table that maps ciphersuites to crypto methods. */
    NX_SECURE_TLS_CIPHERSUITE_INFO* nx_secure_tls_ciphersuite_lookup_table;
    USHORT nx_secure_tls_ciphersuite_lookup_table_size;

    /* Table that maps X.509 cipher identifiers to crypto methods. */
    NX_SECURE_X509_CRYPTO *nx_secure_tls_x509_cipher_table;
    USHORT nx_secure_tls_x509_cipher_table_size;

    /* Specific routines needed for specific TLS versions. */
#if (NX_SECURE_TLS_TLS_1_0_ENABLED || NX_SECURE_TLS_TLS_1_1_ENABLED)
    NX_CRYPTO_METHOD *nx_secure_tls_handshake_hash_md5_method;
    NX_CRYPTO_METHOD *nx_secure_tls_handshake_hash_sha1_method;
    NX_CRYPTO_METHOD *nx_secure_tls_prf_1_method;
#endif

#if (NX_SECURE_TLS_TLS_1_2_ENABLED)
    NX_CRYPTO_METHOD *nx_secure_tls_handshake_hash_sha256_method;
    NX_CRYPTO_METHOD *nx_secure_tls_prf_sha256_method;
#endif

#if (NX_SECURE_TLS_TLS_1_3_ENABLED)
    const NX_CRYPTO_METHOD *nx_secure_tls_hkdf_method;
    const NX_CRYPTO_METHOD *nx_secure_tls_hmac_method;
    const NX_CRYPTO_METHOD *nx_secure_tls_ecdhe_method;
#endif

} NX_SECURE_TLS_CRYPTO;
```
Tablo, genellikle şifreleme yordamları ve modülleriyle bulunan NetX güvenli TLS projesinde bulunan statik bir Sabitte bu yapının girişlerini doldurarak oluşturulur.

Örneğin, NetX güvenli ile birlikte sunulan yalnızca yazılım ("genel") şifreleme kitaplığı, aşağıdaki tablo tanımını içerir (ECC olmayan ciphersuite desteği için<sup>19</sup>):

```C
/* Define the cipher table object we can pass into TLS. */
const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers =
{
    /* TLS Ciphersuite lookup table and size. */
    _nx_crypto_ciphersuite_lookup_table,
    sizeof(_nx_crypto_ciphersuite_lookup_table) / 
    sizeof(NX_SECURE_TLS_CIPHERSUITE_INFO),

    /* X.509 certificate cipher table and size. */
    _nx_crypto_x509_cipher_lookup_table,
    sizeof(_nx_crypto_x509_cipher_lookup_table) / sizeof(NX_SECURE_X509_CRYPTO),

    /* TLS version-specific methods. */
#if (NX_SECURE_TLS_TLS_1_0_ENABLED || NX_SECURE_TLS_TLS_1_1_ENABLED)
    &crypto_method_md5,
    &crypto_method_sha1,
    &crypto_method_tls_prf_1,
#endif

#if (NX_SECURE_TLS_TLS_1_2_ENABLED)
    &crypto_method_sha256,
    &crypto_method_tls_prf_sha_256
#endif

#if (NX_SECURE_TLS_TLS_1_3_ENABLED)
    &crypto_method_hkdf,
    &crypto_method_hmac,
    &crypto_method_ecdhe,
#endif
};
```
Yapıda, ilk giriş TLS ciphersuite tablosudur. NX_SECURE_TLS_CIPHERSUITE_INFO yapısı, şifreleme yordamlarını (NX_CRYPTO_METHOD işaretçileri biçiminde), TLS belirtimlerinde tanımlandığı şekilde belirli cipherpaketlerine eşler. İkinci değer, tablodaki ilk alan tarafından işaret edilen girdi sayısıdır.

Sonraki alan, dijital sertifikaları işlerken X. 509.440 tarafından kullanılan bir yordamlar tablosuna işaret eder ve yapı NX_SECURE_X509_CRYPTO, NX_SECURE_TLS_CIPHERSUITE_INFO biçiminde benzerdir. Aşağıdaki alan tablodaki girdi sayısıdır.

Aşağıdaki arama tablosu, belirli bir TLS sürümü için gereken bir dizi yordamlardır. Örneğin, TLS sürüm 1,2 ' den önce, anahtar oluşturma ve el sıkışma karma yordamları SHA-1 ve MD5 birleşimini kullanacak şekilde düzeltildi – Bu yordamlar için yöntemler özel cipherpaketlerine bağlı olmadıkları için özel olarak şifre yapısında çağırılır. TLS sürüm 1,2 ' de, anahtar oluşturma ve karma yordamlar ciphersuite tarafından seçilir, ancak kullanılacak yordamları belirtmeyen ciphersuites için SHA-256 karma yöntemi kullanılır ve şifre yapısı bu yordamı özellikle çağırır.

TLS 1,3, çeşitli işlemler için birkaç ek özel şifre gerektirir.

19. TLS 1,3 desteğinin ECC gerektirdiğini, TLS 1,3 etkinse nx_crypto_tls_ciphers_ecc kullanın.

### <a name="tls-ciphersuite-lookup-table"></a>TLS Ciphersuite arama tablosu

TLS için şifreleme tablosunu doldurmanız için, şifreleme yordamlarını belirli ciphersuite tanımlayıcılarıyla eşleyen bir ciphersuite arama tablosu da oluşturmanız gerekir. Tanımlayıcılar, evrensel olan ıANA kayıtlı değerlerdir. Daha fazla bilgi için bkz. TLS RFC 'Leri. Yordamlar her ciphersuite 'de kullanılan 5 ayrı yöntemi temsil eder (bazı cipherpaketleri 5 ' i kullanamaz): ortak şifre, ortak anahtar kimlik doğrulaması, oturum şifresi, oturum karması yordamı ve TLS Pseudo-Random Işlevi (PRF). Aşağıdaki tabloda 5 yöntemi açıklanmaktadır:

| **Rutin kategori**      | **Açıklama**                                                                                       | **Örnek algoritmalar**                                            |
| ------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Ortak şifre             | TLS el sıkışması sırasında anahtar alışverişi yapmak için kullanılır                                                        | RSA, Diffie-Hellman, ECC                                          |
| Ortak anahtar kimlik doğrulaması | TLS el sıkışması sırasında verilerin kimliğini doğrulamak veya imzalamak için kullanılır                                            | RSA, DSS                                                          |
| Oturum şifresi            | TLS oturumu sırasında uygulama verilerini şifrelemek için kullanılan simetrik anahtar algoritması                       | AES, RC4                                                          |
| Oturum karması              | TLS oturumu sırasında iletilerin bütünlüğünü korumak için kullanılır (verilerin değişmediğinden emin olmanızı sağlar) | SHA-1, SHA-256                                                    |
| TLS PRF                   | TLS el sıkışma 'nda anahtar malzeme ve el sıkışma karmasında kullanılır                          | PRF, karma yordamlarını temel alır – SHA-1 + MD5, SHA-256, SHA-512 |

NX_SECURE_TLS_CIPHERSUITE_INFO yapısı aşağıdaki gibi tanımlanır:

```C
typedef struct NX_SECURE_TLS_CIPHERSUITE_INFO_struct
{
    /* The IANA value of the ciphersuite as defined by the TLS spec.*/
    USHORT nx_secure_tls_ciphersuite;

    /* The Public Key operation in this suite - RSA or DH. */
    NX_CRYPTO_METHOD *nx_secure_tls_public_cipher;

    /* The Public Authentication method used for signing data. */
    NX_CRYPTO_METHOD *nx_secure_tls_public_auth;

    /* The session cipher being used - AES, RC4, etc. */
    NX_CRYPTO_METHOD *nx_secure_tls_session_cipher;

    /* The size of the initialization vectors for the session cipher (bytes).*/
    USHORT nx_secure_tls_iv_size;

    /* The key size for the session cipher (bytes). */
    UCHAR nx_secure_tls_session_key_size;

    /* The hash being used - MD5, SHA-1, SHA-256, etc. */
    NX_CRYPTO_METHOD *nx_secure_tls_hash;

    /* The size of the hash being used. SHA-1 is 20 bytes, MD5 is 16 bytes.*/
    USHORT nx_secure_tls_hash_size;

    /* The TLS PRF being used – this is only for TLSv1.2. */
    NX_CRYPTO_METHOD *nx_secure_tls_prf;

} NX_SECURE_TLS_CIPHERSUITE_INFO;
```
Nx_secure_tls_ciphersuite alanı ıANA ciphersuite değerini içerir ve NX_CRYPTO_METHOD işaretçileri, bu ciphersuite tarafından kullanılan 5 yöntemi temsil eder. Skaler değerler (nx_secure_tls_iv_size, nx_secure_tls_key_size ve nx_secure_tls_hash_size), NX_CRYPTO_METHOD girişlerinde kullanılamayan bilgiler sağlayan bilgilendirme amaçlıdır.

Örneğin, TLS için varsayılan ciphersuite, 128 bitlik anahtarlarla AES-CBC ve oturum karma için SHA-1 kullanımını belirten TLS_RSA_WITH_AES_128_CBC_SHA. Bu ciphersuite için TLS PRF belirtilmedi, bu nedenle TLSv 1.2 modunda, varsayılan SHA-256 PRF kullanır. Tüm ciphersuites 'in, tabloda belirtilen PRF 'ten bağımsız olarak, TLS 1,0 ve 1,1 ' de SHA-1 + MD5 PRF 'yi kullandığına unutmayın.

Genel şifreleme kitaplığındaki NX_SECURE_TLS_CIPHERSUITE_INFO tablosundaki giriş aşağıdaki gibi tanımlanır:

```C
{ 
  TLS_RSA_WITH_AES_128_CBC_SHA,     /* Ciphersuite identifier */
  &crypto_method_rsa,               /* Public-key cipher (NX_CRYPTO_METHOD)*/
  &crypto_method_rsa,               /* Authentication method(NX_CRYPTO_METHOD)*/
  &crypto_method_aes_cbc_128,       /* Session cipher method(NX_CRYPTO_METHOD)*/
  16,                               /* Session cipher IV size in bytes */
  16,                               /* Session cipher key size in bytes */
  &crypto_method_hmac_sha1,         /* Session hash routine(NX_CRYPTO_METHOD) */
  20,                               /* Session hash output size in bytes */
  &crypto_method_tls_prf_sha_256    /* TLSv1.2 PRF */
},
```

Oturum şifresi anahtar boyutunun ciphersuite tarafından belirlendiği, ancak ortak anahtar yöntemleri için anahtar boyutunun, el sıkışma sırasında alışverişi yapılan dijital sertifikalarda ortak anahtarlar bulunduğundan, TLS el sıkışması tamamlanana kadar bilinmediğini unutmayın.

### <a name="x509-cipher-lookup-table"></a>X. 509.440 şifre arama tablosu

NX_SECURE_TLS_CIPHERSUITE_INFO tablosu gibi, NX_SECURE_X509_CRYPTO yapısı şifreleme yordamlarını bilinen değerlerle eşler. X. 509.440 durumunda tanımlayıcılar aslında X. 509.440 tarafından tanımlanan ve ISO ve ITU standartları gövdelerinde kayıtlı olan OID 'ler vardır. OID 'ler, dijital sertifikalarda kullanılan şifreleme yordamları dahil çeşitli iletişim standartlarındaki çeşitli bilgileri benzersiz şekilde tanımlamak için tasarlanan değişken uzunlukta çok baytlı değerlerdir. OID 'lerin değişken uzunlukta olması nedeniyle, NetX güvenli TLS resmi OID değerlerini dahili olarak kullanılan sabit uzunluklu sabitlere eşler (bkz. nx_secure_x509. h). Bu sabitler, aşağıdaki gibi tanımlanan NX_SECURE_X509_CRYPTO yapısında kullanılır:

```C
/* Structure to hold X.509 cryptographic routine information. */
typedef struct NX_SECURE_X509_CRYPTO_struct
{
    /* Internal NetX Secure identifier for certificate "ciphersuite" which consists
       of a hash and a public key operation. These can be mapped to OIDs in X.509.
        */
    USHORT nx_secure_x509_crypto_identifier;

    /* Public-Key Cryptographic method used by certificates. */
    NX_CRYPTO_METHOD *nx_secure_x509_public_cipher_method;

    /* Hash method used by certificates. */
    NX_CRYPTO_METHOD *nx_secure_x509_hash_method;
} NX_SECURE_X509_CRYPTO;
```

İlk alan *nx_secure_x509_crypto_identifier*, NETX güvenli tarafından kullanılan iç OID gösterimidir.

İkinci ve üçüncü alanlar, bir karma yordamıyla eşleştirilmiş bir ortak anahtar işlemi olan OID tarafından tanımlanan şifreleme yöntemlerini temsil eden NX_CRYPTO_METHOD nesneleri işaret eder. Her dijital sertifikanın Şifreleme yordamları için birden fazla OID 'ye sahip olabileceğini unutmayın.

X. 509.440 için yöntem tablosu, ciphersuite arama tablosuyla aynı şekilde oluşturulur. Örnek olarak, RSA_SHA1 için OID 'ye bakacağız. RSA_SHA1 için gerçek OID aşağıdaki gibidir:

```C
{iso(1) member-body(2) us(840) rsadsi(113549) pkcs(1) pkcs-1(1) sha1-with-rsa-
signature(5)}
```
OID, ASN. 1 sözdiziminde temsil edilir ve 1.2.840.113549.1.1.5 sayısal bir değere sahiptir. Bu değer daha sonra ikili biçimde kodlanır ve aşağıdaki baytları oluşturur:

```C
UCHAR RSA_SHA1_OID = { 0x2A, 0x86, 0x48, 0x86, 0xF7, 0x0D, 0x01, 0x01, 0x05 };
```
ASN. 1 ' den ikili biçime gerçek dönüştürme, bu belgenin kapsamı dışındadır. Daha fazla bilgi için, OID 'ler için ASN. 1 için arama yapın. NetX güvenli tarafından desteklenen OID 'lerin ikili temsili *nx_secure_x509. c* dosyasında bulunabilir.

Gerçek OID 'yi dahili olarak tanınan bir sabit ile eşleştirdikten sonra, NX_SECURE_X509_CRYPTO tablosunda RSA_SHA1 için bir giriş oluşturuyoruz:

```C
{ 
    NX_SECURE_TLS_X509_TYPE_RSA_SHA_1,    /* Internal OID constant. */
    &crypto_method_rsa,                   /* RSA method (NX_CRYPTO_METHOD). */ 
    &crypto_method_sha1                   /* SHA-1 method (NX_CRYPTO_METHOD). */
}, 
```
### <a name="default-tls-routines"></a>Varsayılan TLS yordamları

Yukarıda belirtildiği gibi TLS, el sıkışma sırasında anahtar oluşturma ve ileti doğrulama için bazı varsayılan yordamlar gerektirir. Birincil yordam, TLS Pseudo-Random Işlevi veya PRF 'dir. PRF, karma yordamlarını temel alır ve anahtar oluşturma veya başka amaçlar için rastgele bir sözde rastgele veri miktarı<sup>oluşturmak için kullanılabilir</sup> .

PRF 'nin yanı sıra, her TLS sürümü de sağlanması gereken varsayılan karma yordamlar kullanır. 1,0 ve 1,1 TLS sürümleri için bu karma yordamlar, MD5 ve SHA-1 ' dir. TLS sürüm 1,2 yalnızca SHA-256 gerektirir.

NX_SECURE_TLS_CRYPTO yapısında, MD5, SHA-1, SHA-256, TLS sürüm 1.0/1.1 PRF ve varsayılan TLS 1,2 PRF için NX_CRYPTO_METHOD işaretçiler vardır.

TLS 1,3 desteği, HKDF (anahtar oluşturma), HMAC (el sıkışma sırasında kullanılan belirli karma işlemler için) ve ECDHE (TLS 1,3 işlevselliği için gereklidir) için alanlar ekler.

Genel yazılım şifreleme kitaplığı 'nda belirtilen TLS PRF yazılım sürümleridir. TLS 1.0/1.1 için, bu işleve *nx_crypto_tls_prf_1* denir. TLS 1,2 için işlev *nx_secure_tls_prf_sha256* olarak adlandırılır. "1" soneki eski TLS 1,0 PRF 'yi temsil eder ve "SHA256" soneki, TLS 1,2 varsayılan PRF 'in SHA-256 ' ı temel aldığı olguyu ifade eder. Diğer PRF yordamları için destek gerektiğinde, bu yordamların soneki kullanılan karma yöntemi yansıtır. PRF yordamları karma yöntemlere dayalı olduğundan, temeldeki karma yordamlar farklı hedef platformlarda bağımsız donanım hızlandırmalı olabilir.

TLS ciphersuite ve X. 509.440 arama tablolarına ek olarak, NX_SECURE_TLS_CRYPTO yapısında doldurulan varsayılan PRF ve karma yordamlar, bir TLS oturumu başlatmak için doldurulabilir ve kullanılabilir.

20. "Sözde rastgele", PRF 'nin belirleyici olduğunu ifade eder, yani aynı girişe verilen çıktıyı her zaman üretir, ancak çıktının tahmin edilebilir olmadığı konusunda rastgele olur. TLS, bu PRF özelliğini kullanarak, el sıkışma sırasında RSA gibi bir ortak anahtar şifresi kullanılarak yapılan ana gizli dizi ile birleştirilmiş çeşitli genel verilerden oturum anahtarları oluşturur.

### <a name="cryptographic-metadata"></a>Şifreleme meta verileri

NX_SECURE_TLS_CRYPTO tablosu ile TLS oturumunu başlatabilmemiz için, şifreleme yordamı meta verileri için arabellek alanı ayırdık. Meta veriler, denetim bloğu tarafından temsil edilen belirli bir yordam ile ilişkili tüm durumları depolamak için kullanılır. Her bir NX_CRYPTO_METHOD *nx_crypto_metadata_area_size* alanı, bu yordam ile ilişkili denetim yapısının boyutuna AYARLANMALıDıR veya TLS başlatması, gereken alana göre düzgün şekilde hesaba geçmeyecektir ve bu da arabellek taşması sorunlarına neden olabilir.

TLS oturumu oluşturulmadan önce, meta veri arabelleğinin ayrılmış olması gerekir. Arabellek nx_secure_tls_session_create tarafından otomatik olarak bölünür ve şifreleme yöntemi tablosunda sunulan yordamların her biri için boşluk ayrılır. Bir TLS oturumunda aynı anda yalnızca bir ciphersuite etkin olduğundan, desteklenen ciphersuite sayısı gerekli meta veri alanını etkilemez – boşluk, ciphersuite arama tablosunda bu kategori için maksimum denetim blok boyutunu kullanarak 5 ciphersuite yordamlarının her biri için ayrılır.

Meta veri arabellek boyutunu kolay hesaplamayı kolaylaştırmak için, hizmet *nx_secure_metadata_size_calculate* aynı hesaplamaları nx_secure_tls_session_create olarak gerçekleştirir ancak gereken toplam meta veri arabellek boyutunu bayt cinsinden döndürür.

### <a name="initializing-the-tls-session"></a>TLS oturumu başlatılıyor

NX_CRYPTO_METHOD ve NX_SECURE_TLS_CRYPTO nesneleri oluşturulduktan ve meta veri alanı ayrıldıktan sonra, aşağıdaki gibi bir TLS oturumu başlatabiliriz (yukarıdaki örneklerden alınan değerler):

```C
/* Pointer to the platform-specific cipher table. */
extern nx_crypto_tls_ciphers;

/* Cryptographic routine metadata buffer. Size is determined by calling 
nx_secure_tls_metadata_size_calculate with the nx_crypto_tls_ciphers table referenced 
above. */
UCHAR crypto_metadata[4500];

/* Initialize our TLS session using our cipher table and metadata area. Note that we can 
use sizeof for the metadata array because the size parameter expects the size in bytes.*/

nx_secure_tls_session_create(
    &tls_session,            /* Pointer to TLS session.      */
    &nx_crypto_tls_ciphers,  /* Pointer to cipher table.     */
    crypto_metadata,         /* Cryptography metadata buffer.*/
    sizeof(crypto_metadata), /* Size of metadata buffer.     */
);
```
