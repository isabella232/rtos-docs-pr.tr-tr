---
title: Bölüm 3-Azure RTOS NetX güvenliği için Işlevsel açıklama
description: Bu bölüm, NetX güvenli TLS 'nin işlevsel bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 711195e60771ebd467c69df49ef7665f32e13a17c21ca839404e829449cf1401
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797976"
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

netx güvenli TLS için, X. 509.440 sertifikası ASN. 1 ' in Distinguished Encoding Rules (DER) biçimi kullanılarak ikili kodlanmış olmalıdır. DER, sertifikalar için Standart TLS-kablolu ikili biçimidir.

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

### <a name="tls-session-start"></a>TLS Oturumu Başlatma

TLS'nin çalışması için temel alınan bir aktarım katmanı ağ protokolü gerekir. Kullanılan protokol genellikle TCP'dir. NetX Güvenli TLS oturumu oluşturmak için NetX/NetXDuo TCP API'si kullanılarak bir TCP bağlantısı kurulması gerekir. Bir **NX_TCP_SOCKET** ve nx_tcp_server_socket_listen _ ve _ nx_tcp_server_socket_accept _ hizmetleri ***(TLS Sunucusu için)*** veya _ nx_tcp_client_socket_connect hizmeti (TLS İstemcisi için) kullanılarak bir bağlantı oluşturularak oluşturulmuş olması gerekir.

TCP bağlantısı kurulduktan sonra TCP yuvası, tcp nx_secure_tls_session_start ***geçirebilirsiniz.***

### <a name="tls-packet-allocation"></a>TLS Paket Ayırma

NetX Secure TLS, NetX/NetXDuo TCP (***NX_PACKET** _) ile aynı paket yapısını kullanır. Tek tek _*_durum, nx_packet_allocate_*_ hizmetinin çağrılması yerine _ *_nx_secure_tls_packet_allocate_** hizmetinin çağrılması ve TLS üst bilgisi için alan doğru şekilde ayrılmış olmasıdır.

### <a name="tls-session-send"></a>TLS Oturum Gönderme

TLS oturumu başlatıldıktan sonra uygulama , * nx_secure_tls_session_send _ **hizmetini** kullanarak veri gönderebilir. Gönderme hizmeti, gönderilen verileri içeren _*_bir NX_PACKET_*_ veri _**_ yapısını alarak nx_tcp_socket_send hizmetiyle aynıdır; yalnızca bu veriler gönderilmeden önce NX Güvenli TLS yığını tarafından şifrelenir ve paket _* nx_secure_tls_packet_allocate **_kullanılarak ayrılır._

### <a name="tls-session-receive"></a>TLS Oturumu Alma

TLS oturumu başlatıldıktan sonra uygulama , * nx_secure_tls_session_receive _ **hizmetini kullanarak veri almaya** başlayabilir. TLS Oturumu gönderme işlemi gibi bu hizmet de _*_nx_tcp_socket_receive_** ile aynıdır, ancak gelen verilerin şifresi çözülmüş ve paket yapısında döndürülmeden önce TLS yığını tarafından doğrulanmıştır.

### <a name="tls-session-close"></a>TLS Oturumu Kapatma

Bir TLS oturumu tamamlandıktan sonra hem TLS istemcisinin hem de sunucunun oturumu kapatmak için diğer tarafa bir CloseNotify uyarısı göndermesi gerekir. Oturumun başarıyla kapatılması için her iki taraf da uyarıyı almalı ve işlemeli.

Uzak konak bir CloseNotify uyarısı gönderirse, ***nx_secure_tls_session_receive** _ hizmetine yapılan çağrılar uyarıyı işler, ilgili uyarıyı uzak ana bilgisayara geri gönderir ve _* NX_SECURE_TLS_SESSION_CLOSED **_değerini_ geri gönderir. Oturum kapatıldıktan sonra, bu TLS oturumuyla başka veri gönderme veya alma girişimleri başarısız olur.

Uygulama TLS oturumunu kapatmak isterse ***** nx_secure_tls_session_end _ hizmetinin çağrılsı gerekir. Hizmet CloseNotify uyarıyı gönderir ve CloseNotify yanıtını işler. Yanıt alınmazsa, TLS *_oturumunun_* temiz bir şekilde kapatılamayarak olası bir güvenlik ihlali olduğunu belirten _ NX_SECURE_TLS_SESSION_CLOSE_FAIL * hata değeri döndürülür.

### <a name="tls-alerts"></a>TLS Uyarıları

TLS maksimum güvenlik sağlayacak şekilde tasarlanmıştır, bu nedenle protokolde herhangi bir hata davranışı olası bir güvenlik ihlali olarak kabul edilir. Bu nedenle, ileti işleme veya şifreleme/şifre çözme hataları el sıkışmayı veya oturumu hemen sonlandıran önemli hatalar olarak kabul edilir.

Yerel bir uygulamanın hatalarını işlemek nispeten basit bir işlemdir ancak uzak ana bilgisayarın durumu düzgün bir şekilde ele almak ve olası güvenlik ihlallerini önlemek için bir hata olduğunu biliyor olması gerekir. Bu nedenle TLS, herhangi bir hata *üzerine* uzak ana bilgisayara bir Uyarı iletisi gönderir.

Uyarılar diğer TLS iletileriyle aynı şekilde ele alınarak, bir saldırganın sağlanan uyarı türünden bilgi toplamasını önlemek için oturum sırasında şifrelenir. El sıkışma sırasında, olası bir saldırgan tarafından elde edilecek bilgi miktarını sınırlamak için gönderilen uyarılar kapsamda sınırlıdır.

TLS oturumunu kapatmak için kullanılan CloseNotify uyarısı, önemli olmayan tek uyarıdır. Uyarı olarak kabul edilir ve uyarı iletisi olarak gönderilir ancak CloseNotify, hata olduğunu belirten diğer uyarılara benze değildir.

Uyarı değeri ve "düzey" (düzeyler "uyarı" ve "önemlidir" – çoğu TLS uyarısı "önemli") TLS RFC'lerinde tanımlanır ve meydana gelen hata türünü belirtir. CloseNotify dışında çoğu TLS Uyarısı olası bir güvenlik sorunu göstergesi olarak kabul edilir ve TLS oturumu veya el sıkışması durdurularak sonuçlandırılacaktır. Herhangi bir TLS API çağrısı **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) döndürürse, api hizmeti **_nx_secure_tls_session_alert_value_get_** (NetX Güvenli TLS sürüm 5.12'de yeni) uygulamanın güvenlik sorunlarına yanıtlarla ilgili kararlar için kullanabileceği TLS uyarı değerini ve düzeyini almak için kullanılabilir. Çoğu durumda CloseNotify dışında uzak konaktan alınan herhangi bir uyarı önemli bir hata olarak kabul edilir, ancak bazı alıntılar vardır; daha fazla bilgi için bkz. TLS RFC'leri.

### <a name="tls-session-renegotiation"></a>TLS Oturumu Yeniden Görüşme

TLS, tlS oturum parametrelerinin mevcut bir TLS oturumu bağlamında yeniden yapılan bir yeniden görüşme olduğu "yeniden görüşme" ifadesini destekler. Bu, uygulamada yeni el sıkışma iletilerinin mevcut oturum kullanılarak şifrelenir ve kimlik doğrulamasının doğrulandığı anlamına gelir. Yeniden görüşme, bir TLS ana bilgisayarı mevcut oturumu tamamlamak zorunda kalmadan yeni oturum parametreleri (örneğin, yeni TLS oturum anahtarları oluşturmak) oluşturmak istiyorsa kullanılır. Örneğin, bir uygulamanın güvenlik ilkeleri oturum anahtarlarının yalnızca sınırlı bir süre için kullanılmaya devam etmekle birlikte TLS oturumunun o sürenin ötesinde etkin kalmasını dikte ettiği zaman yeniden görüşme tercih edilebilir.

Oturum yeniden görüşmeyle ilgili sorunlardan biri, TLS'yi belirli bir Ortadaki Adam saldırısına karşı savunmasız hale gelen ve bir saldırganın bir sunucuyu yeni parametrelerle yeniden görüşme başlatmaya ikna etme ve böylece saldırganın TLS oturumunu ele geçirerek buna izin vermesidir. Bu sorunu gidermek için Güvenli Yeniden Yapılanma Göstergesi uzantısı tanıtıldı (bkz. **Hata! Başvuru kaynağı bulunamadı.** bölümünü seçin.

NetX Secure TLS, oturum yeniden anlaşması ve Güvenli Yeniden Görüşme Göstergesi uzantısını tamamen destekler.

Uzak bir konaktan veri alırken, yeniden toplamalar (ve uzantı) uygulama etkileşimi olmadan otomatik olarak işlenir. Oturum yeniden görüşmeleriyle ilgili bildirim istenirse, nx_secure_tls_session_renegotiate_callback_set hizmetiyle yeniden *nx_secure_tls_session_renegotiate_callback_set* sağlanmalıdır. Uzak konak tarafından yeniden bir yeniden yapılanma istenğında geri çağırma çağrılır ve uygulamanın istenirse işlem uygulamasına izin verme.

Etkin bir TLS oturumundan yeniden görüşme başlatmak için, istenen TLS *oturumunda nx_secure_tls_session_renegotiate* hizmeti çağırman gerekir.

### <a name="tls-session-resumption"></a>TLS Oturumu Yeniden Verme

TlS oturumu yeniden verme, bazı benzerliklere rağmen oturum yeniden görüşmeleriyle karıştırılmamalıdır. Oturum *yeniden görüşmenin* mevcut bir TLS oturumunda yeni bir el  sıkışmayı başlatmayı içerdiği yerde, oturum yeniden başlatma tamamen isteğe bağlı bir özelliktir ve tam bir TLS el sıkışması yapmadan kapalı TLS oturumunun yeniden başlatılmasını içerir. Bunu başarmak için TLS uygulaması oturum parametrelerini ve anahtarlarını önbelleğe alarak  bunları özgün el sıkışmada sağlanan benzersiz bir tanımlayıcı olan oturum kimliğiyle eşler. Bir TLS sunucusuna oturum kimliği sağlamak, konaklar arasında önceki bir TLS oturumunun geçmişte var olduğunu ve bir süre tamamlandıktan sonra istemcinin hala azaltılmış bir el sıkışma ile oturumu yeniden kurma durumuna sahip olduğunu gösterir. Oturum anahtarları teorik olarak hala gizli ve yalnızca iletişimde olan iki konak tarafından bilindiği için sunucu yeni bir TLS oturumu başlatarak normal el sıkışmanın çoğunu atlar.

Oturum sürdürme, anahtar oluşturma ana gizli anahtarını paylaşmak ve sertifika imzalarını doğrulamak için kullanılan pahalı olabilecek ortak anahtar işlemlerini önlemek için yararlı olabilir, ancak aynı zamanda tüm olası oturumlar için oturum parametrelerinin, anahtarların ve şifreleme durumunun bellekte korunmasını gerektirir (en azından yapılandırılabilir bir zaman penceresi için).

NetX Secure TLS'nin geçerli sürümü oturum sürdürmeyi desteklemez. Oturum kimliği TLS sunucuları tarafından yok sayılır ve TLS istemcileri her zaman tam bir el sıkışması gerçekleştirmesi için sunucudan bir NULL oturum kimliği sağlar. Tamamen isteğe bağlı bir özellik olduğu ve oturum kimliğinin NULL olması veya tanınmamış olması gerekirken tüm TLS uygulamaları varsayılan olarak tam bir el sıkışması olarak ayarlandıktan sonra oturum yeniden vermenin olmaması, işlenenler arası soruna neden olmamalıdır.

### <a name="protocol-layering"></a>Protokol Katmanlama

TLS protokolü, aktarım katmanı (tcp gibi) ile uygulama katmanı arasındaki ağ yığınına uyar. TLS bazen aktarım katmanı protokolü (dolayısıyla Aktarım Katmanı Güvenliği) olarak kabul edilir, ancak temel alınan ağ protokolleri (TCP gibi) açısından bir uygulama olarak hareket eder ve bazen uygulama katmanında gruplandırılan bir uygulamadır. 

TLS, TCP gibi sırayla ve kayıpsız teslimi destekleyen bir aktarım katmanı protokolü gerektirir. UDP veri birimlerinin teslimi garanti edilemez çünkü bu gereksinim nedeniyle TLS UDP üzerinde çalıştıramaz. TLS'nin değiştirilmiş bir sürümü olan *DTLS* adlı ayrı bir protokol, UDP gibi bir veri birimi protokolü üzerinde TLS güvenliğine ihtiyaç olan uygulamalar için kullanılır. NetX Secure DTLS'i destekler, ancak DTLS belgeleri bu belgeden ayrıdır.

![TCP/IP ve TLS protokol katmanlarının diyagramı.](media/image6.png)

Şekil 5- TCP/IP ve TLS protokol katmanları

## <a name="network-communications-security"></a>Ağ İletişimi Güvenliği

Ortak ağlar ve İnternet üzerinden iletişimin güvenliğini sağlamak, çok sayıda kitap, makale ve çözümün konusu ve kritik öneme sahip bir konudur. Bu konu oldukça karmaşıktır, ancak basit bir fikirle azaltabilirsiniz: yalnızca hedeflenen hedefin bu bilgilere erişmesi veya bu bilgileri değiştirerek bir ağ üzerinden bilgi gönderme. Bu, üç önemli kavrama neden olur: gizlilik, bütünlük ve kimlik doğrulaması. TLS protokolü üçü için de çözümler sağlar.

### <a name="secrecy"></a>Gizli -lik

Bir ağ üzerinden veri gönderirken, verilerin kötü amaçlı bir varlık tarafından alınamaz olması genellikle önemlidir. Veriler bir TCP/IP bağlantısı üzerinden gönderilirse, ağa erişimi olan herkes kolayca kullanılabilir ağ araçlarını kullanarak bu verileri okuyabilir. Verilerin elde edepsini önlemek için, hedeflenen hedef dışında okunacak şekilde kodlanması *gerekir; bu gizliliktir.* TLS'de RSA ve AES gibi şifreleme algoritmaları gizlilik sağlar.

### <a name="integrity"></a>Bütünlük

Bazen, gizlilik bir ağ üzerinden veri koruma için yeterli değildir. Bazı durumlarda kötü amaçlı bir varlığın, paketin ne içerdiğini bilmek zorunda kalmadan TCP paketinin içeriğini değiştirmesi mümkün olabilir. Şifrelenmiş veriler değiştirilemez, şifre çözme geçersiz hale gelir veya iletinin parametreleri değiştirerek saldırganın elde etmek ilgilenebilecekleri bir sonuç elde edilir. Ağ üzerinde, bir saldırganın taşımadaki verileri değiştirmesini engelleyene, ancak verilerin değişip değişmediğini bilmek için bir mekanizma s sağlamamız gerekir. Veriler taşıma sırasında değiştirilirse bu veriler bilinir ve reddedilir. Bu kavram *bütünlük kavramıdır.* TLS'de bütünlük, karma işlevler olarak bilinen bir şifreleme yordamları *sınıfı tarafından sağlanır.* Karma işlevlere bazı örnekler MD5 ve SHA-1'tir.

### <a name="authentication"></a>Kimlik Doğrulaması

Ağ iletişim güvenliğinde üçüncü önemli kavram, verilerin yalnızca hedeflenen hedefle iletişim kurması gerektiği fikridir. Saldırgan, başka bir ana bilgisayar için amaçlanan verileri almak için meşru bir varlık olarak poz verebiliyor. Veriler gizlilik ve bütünlük mekanizmalarıyla gönderilebilirse bile, saldırgan bu yanılgı üzerinden istenen sonucu (güvenli iletişimlerin tehlikeye atarak) yine de elde etmiş olabilir. Bunu önlemek için, herhangi bir hassas veri gönderilmeden önce uzak bir ana bilgisayarın kimliğini kanıtlamak için bir mekanizma gerekir. Uzak ana bilgisayarın kimliğini kanıtlama işlemi kimlik *doğrulamasıdır.* TLS'de kimlik doğrulaması dijital sertifikalar, karma işlevler  ve ortak anahtar şifreleme özelliğini kullanan dijital imzalar adlı bir mekanizma kullanılarak sağlanır (aşağıda açıklanmıştır). Önceden paylaşılan bir anahtar (PSK) ile sınırlı ama *kullanışlı bir kimlik doğrulaması* biçimi de sağlanıyor.

## <a name="tls-encryption"></a>TLS Şifrelemesi

TLS protokolü, şifreleme kullanarak İnternet üzerinden güvenli ağ iletişimleri sağlamak için kullanılan bir çerçevedir. Şifreleme genellikle verileri özgün verileri (veya bu veriler hakkında bilgileri) almak için anahtar olmadan çok zor olacak şekilde kodlama işlemi olarak *tanımlanır.* Bilgisayar sistemlerinde şifreleme, sonlu alanlar gibi karmaşık matematikleri temel alır  ve iki tür olarak sınıflandırılabilir: özel anahtar (veya simetrik *şifreleme)* ve ortak anahtar *(veya* *asimetrik şifreleme).* Özel anahtar şifrelemesi örnekleri AES (Gelişmiş Şifreleme Standardı) ve RC4 (Rivest Cipher 4) örnekleridir. Ortak anahtar şifrelemesi örnekleri RSA (Rivest, Shamir, Adleson) ve Diffie-Hellman şifrelemedir.

TLS protokolü, performans, güvenlik ve esneklik arasında bir denge sağlamak için hem özel anahtar hem de ortak anahtar şifreleme yordamlarını kullanır.

### <a name="private-key-encryption"></a>Private-Key Şifrelemesi

Özel anahtar şifrelemesi binlerce yıldır kullanılır. Temel değiştirme şifrelemeleri (bir harfin veya sözcüğün başka bir ilgisiz harf veya sözcükle değiştirdiği), bilinen en eski şifreleme örnekleridir, ancak bilgi yaşı özel anahtar şifrelemesi gelişiyle birlikte önemli ölçüde geliştirilmiştir.

Özel anahtar şifrelemesi, yalnızca bu anahtara erişimi olan bir varlığın verilerin kodunu anlamlı bir şekilde çöze bir şekilde bazı verileri kodlamak için kullanılan bir değer (genel durumda bir sözcük, tümcecik veya sayı olabilir) olan bir "anahtar" kullanır. Anahtar, verilerin şifrelerinin şifrelerinin çözülmesi ve şifrelerinin çözülmesi için kullanılır; bu nedenle diğer adı *simetrik şifrelemedir.*

Özel anahtar şifrelemeleri, söz konusu matematikler çok karmaşık olsa bile genellikle hızlı ve oldukça basittir. Bu nedenle TLS, güvenli iletişimler için özel anahtar şifrelemeleri kullanır.

Ancak özel anahtar şifrelemesi, genel bilgisayar ağı iletişimleri için geçerli olmaya çalışılırken bir soruna neden olur: Anahtarın iletişim kurmaya çalışan her iki makine arasında paylaşılması gerekir. Genel durumda, İnternet'te iki makine arasında güvenli bir şekilde özel anahtar iletişim kurmak pratik değildir ve genellikle imkansızdır çünkü ağ trafiğinin, verilerin İnternet üzerinden yönlendirilen çeşitli atlamalarda yer alan çeşitli atlamalarda yer alan herhangi bir sayıda varlık tarafından alınıp alınalığa sahip olduğu varsayılır. Anahtar kötü amaçlı bir varlık tarafından elde edilirse, bu anahtar kullanılarak şifrelenen tüm verilerin güvenliği tehlikeye girer. İnternet'e bağlı makinelerin çoğu yalnızca bir ağ bağlantısına sahip olduğu için ve iletişim için başka bir güvenli kanala sahip değil, ağ üzerinden anahtar göndermek, verileri şifrelenmemiş olarak göndermek için bir yalıtılmaz; güvenlik sağlamaz.

Bu nedenle, özel anahtar şifrelemesi genel amaçlı bir ağ iletişim güvenliği protokolü uygulamak için yeterli değildir. Ortak Anahtar şifrelemesi bu noktada yardımcı olabilir.

NetX Secure TLS, AES özel anahtar şifrelemeyi destekler.

### <a name="public-key-encryption"></a>Public-Key Şifrelemesi

Özel anahtar şifrelemeden farklı olarak, ortak anahtar şifrelemesi 1970'lerde geliştirilmiş olan oldukça yeni bir kavramdır. Matematikte "tuzak kapı işlevleri" olarak bilinen bir kavram kullanılarak, o zaman şifrelenmiş verilerin güvenliğinden ödün vermeden bir ağ üzerinden anahtar paylaşmanın bir yolu olduğu keşfedildi.

Ortak anahtar şifrelemenin çalışma yolu, anahtarın (yukarıda açıklanan özel anahtar şifreleme anlamlısı  içinde) ortak anahtar şifrelemenin adını alan özel anahtar ve ortak anahtar olmak üzere iki parçaya bölünmesidir. Bu anahtarlardan birinin (genellikle ortak anahtar) şifreleme için, diğer anahtar ise şifre çözme için kullanılır. Anahtarların bu asimetrisi, ortak anahtar şifrelemesi için diğer adıdır: *asimetrik şifreleme.*

Ortak anahtar şifrelemenin ardındaki matematik oldukça karmaşıktır, ancak ortak  anahtarın yalnızca şifreleme için kullanıla biliyor olması ve bu anahtarın elde ediş şifrelenmiş verilerin elde edişlerine izin vermeyiş olmasıdır. Buna karşılık özel anahtar, ortak anahtar kullanılarak şifrelenmiş verilerin şifresini çözmenin tek yolu olur. Bu nedenle, özel anahtar gizli anahtarını saklayarak, bu özel anahtarın sahibiyle güvenli bir şekilde iletişim kurmak isteyen herkesin verilerini yalnızca ilgili ortak anahtarla şifrelemesi ve yalnızca bu özel anahtara sahip olan birinin güvenli verileri edine bilgisi olması gerekir.

NetX Secure TLS, RSA ortak anahtar şifrelemeyi destekler.

> [!IMPORTANT] 
> *Yazılım RSA uygulaması kullanılıyorsa RSA çok işlemci yoğun bir işlemdir. Daha büyük anahtar boyutları, kare faktörü için gereken işleme gücünü artırarak anahtar boyutunun 2 kat artması için 4 kat daha yavaştır.*

### <a name="public-key-authentication"></a>Public-Key Kimlik Doğrulaması

Ortak anahtar şifreleme kavramının ilginç bir yan etkisi, kimlik doğrulaması ve şifreleme sağlamak için kullanılabilir olmasıdır.  Bu işlem ters şekilde kullanılmaktadır: özel anahtarı kullanarak şifreleme ve ortak anahtarı kullanarak şifre *çözme.* Bunu yapmak için gerçek mekanizma kullanılan ortak anahtar algoritmasına bağlıdır, ancak kavram aynıdır.

Ortak anahtar kimlik doğrulaması kullanarak kimlik doğrulaması yapmak için, özel anahtarın sahibi bir veri parçasını (genellikle kimlik doğrulaması yapılan verilerin şifreleme karması) bu özel anahtarı kullanarak şifreler. Ardından, verilerin özel anahtarın sahibinden geldiğini doğrulamak isteyen birisi verilerin şifresini çözmek için ilişkili ortak anahtarı kullanır. Şifre çözme başarılı olursa ve kullanıcının bu ortak anahtarın geçerliliğine güvendiği varsayılacak olursa, kullanıcı verilerin özel anahtarın sahibinden geldiğinden emin olabilir.

TLS'de ortak anahtar kimlik doğrulaması, güvenilen sertifika deposu ortak anahtarlarını kullanarak bir TLS sunucusu (ve isteğe bağlı olarak TLS istemcisi) tarafından sağlanan bir dijital sertifikanın geçerliliğini doğrulamak için kullanılır. Sertifika, depoda ortak anahtara karşı denetlenir ve sertifikada bulunan veriler sunucunun kimliğini kontrol etmek için kullanılır.

NetX Secure TLS, RSA kimlik doğrulamasını destekler.

### <a name="cryptographic-hashing"></a>Şifreleme Karması

Şifreleme, TLS'de kullanılan tek şifreleme işlemi değildir. TLS oturumu sırasında ileti bütünlüğünü sağlamak için, ileti içeriklerinin üzerinde oynanmamasını sağlamak için sağlama tablosu gerekir. Ancak, bilgi sahibi bir saldırgan tarafından kolayca ters çevirilene kadar kabul edilebilir bir bütünlük düzeyini garanti etmek için basit sağlama sağlamalarının (TCP'de olduğu gibi) yeterli değildir. TLS tarafından ileti bütünlüğünü sağlamak için kullanılan mekanizma, şifreleme *karması olarak bilinir.*

Şifreleme 1:1 kodlamadır; diğer bir ifadeyle özgün verilerin tamamı şifrelenmiş verilerden elde edilir. Ancak karma, tıpkı sağlama toplamları gibi rastgele bir veri miktarını sabit bir boyut değeriyle eşler. Basit sağlama toplamadan farklı olarak karma, farklı giriş verileriyle aynı çıkışa neden olan çakışmaları azaltmak için özel olarak tasarlanmıştır. Basit sağlama tam olarak, bir bit 1'den 0'a ve 0'dan 1'e başka bir bit çevrilse sağlamalar aynı olur. Şifreleme karması ile çıkış önemli ölçüde farklılık gösterebilir ve bu da saldırganın karma verileri değiştirmesini ve değiştirilen veriler üzerinde karma işlemi yine de aynı değere neden olur (ve bu nedenle bu verilerin bütünlüğünü hatalı bir şekilde doğrulamasını) zorlaştırabilir.

TLS, iletilerin bütünlüğünü sağlamak için hem uygulama iletileri hem de TLS denetim iletileri olmak üzere bir dizi farklı karma algoritması kullanır. Bunlar MD5, SHA-1 ve SHA-256'dır.

NetX Secure TLS MD5, SHA-1 ve SHA-256 karmasını destekler.

## <a name="tls-extensions"></a>TLS Uzantıları

TLS, belirli uygulamalar için ek işlevsellik sağlayan bir dizi uzantı sağlar. Bu uzantılar genellikle ClientHello veya ServerHello iletilerinin bir parçası olarak gönderilir ve uzak bir ana bilgisayara uzantı kullanma isteğini ya da güvenli TLS oturumunun kurulması için ek ayrıntılar sağlamayı gösterir.

Genel olarak uzantılar, devam işlemlerine yol sağlayan el sıkışmanın başında TLS'ye isteğe bağlı parametreler sağlar. Bazı uzantılar uygulama girişi veya karar verme gerektirirken diğerleri otomatik olarak işlenir.

Aşağıdaki tabloda şu anda NetX Secure TLS tarafından desteklenen TLS uzantıları açıklandı:

| **Uzantı Adı**              | **Açıklama**              |
| ------------------------------- |----------------------------- |
| Güvenli Yeniden Yapılanma Göstergesi | Bu uzantı, yeniden anlaşma sırasında ortaya çıkabilir bir Ortadaki Adam saldırı güvenlik açığını hafifletebilir.|
| Sunucu Adı Belirtme          | Bu uzantı, bir TLS İstemcisi'nin TLS Sunucusuna belirli bir DNS adı sağlayarak sunucunun doğru kimlik bilgilerini seçmesini sağlar (sunucunun birden çok kimlik sertifikası ve ağ giriş noktası olduğu varsayılıyor). |
| İmza Algoritmaları            | Bu uzantı, TLS İstemcisi'nin TLS Sunucusuna kabul edilebilir imza ve karma algoritmalarının listesini sağlamasını sağlar. |

Desteklenen TLS Uzantılarına Genel Bakış

### <a name="secure-renegotiation-indication"></a>Güvenli Yeniden Yapılanma Göstergesi

TLS, mevcut bir TLS oturumunda el sıkışma gerçekleştirmeyi, böylece el sıkışma iletilerini şifrelemek için kurulan oturumu kullanmayı destekler. Bu işlem, şifreleme oturumu anahtarlarının TLS oturumunu sonlandırmadan yeniden kurulmasına olanak sağlar ("TLS Oturum Yeniden Görüşme" bölümüne bakın).

Ne yazık ki TLS bir süredir yeniden yapılanması kullandıktan sonra, yeniden yapılanma özelliğini kullanan OrtaDaki Adam saldırılarında bir güvenlik açığı olduğu keşfedildi. Güvenlik açığını kapatmak için Güvenli Yeniden Yapılanma Göstergesi uzantısı tanıtıldı. Temelde, Güvenli Yeniden Anlaşma uzantısı, özgün konakların yeniden anlaşma el sıkışmasına katıldığını doğrulamak için, kurulan bağlantıdan Bitti ileti karması kullanır; temelde karma, bir saldırganın karmayı (oturum anahtarları için erişim gerektirecektir) oluşturulamayacak varsayımı kapsamında doğrulama belirteci olarak kullanılır.

NetX Secure TLS yeniden anlaşması otomatik olarak ele almaktadır ve Güvenli Yeniden Anlaşması Uzantısını varsayılan olarak kullanır. Uygulama etkileşimi gerekmez.

### <a name="server-name-indication"></a>Sunucu Adı Belirtme

TLS İstemcisi, TLS el sıkışması sırasında, istemcinin sunucunun kimliğini doğrulayana kadar bir kimlik sertifikası sağlamak için uzak bir sunucu bekler. Ancak, bir sunucunun her biri benzersiz kimliklere sahip farklı "sanal" sunuculara sahip birden çok farklı hizmet sağlaysa da bazı durumlar olabilir. Birden çok kimliği olan tek bir sunucu olması durumunda, TLS istemcisi sunucunun uygun kimlik bilgilerini seçmek için kullanabileceği belirli bir DNS adını sağlar; bu adı sağlamak için mekanizma Sunucu Adı Belirtme (SNI) uzantısıdır.

SNI uzantısını kullanan bir uygulama için bazı etkileşimler gerekir. TLS İstemcileri için, uygulamanın uzak sunucuya gönderilecek bir DNS adı göndermesi gerekir. TLS Sunucuları için, uygulamanın uzantıdan DNS adını okuması ve istemciye geri göndermek için uygun bir sertifika seçmesi gerekir.

Aşağıdaki bölümlerde, NetX Secure TLS'de SNI uzantısının nasıl kullanımı hakkında daha fazla ayrıntı sağlanmıştır.

### <a name="sni-extension--tls-client"></a>SNI Uzantısı – TLS İstemcisi

SNI uzantısını kullanmak isteyen bir NetX Güvenli TLS İstemcisi, el sıkışma sırasında TLS'ye sağlanmalıdır. Uzantı, el sıkışma işlemini başlatan ClientHello iletisinde gönderildiği için bu ad bir TLS oturumu başlatılmadan önce başlatılmış ve sağlanmalıdır.

Aşağıdaki kod parçacığı uzantısının kullanımını göstermektedir. İlk olarak, NX_SECURE_X509_DNS_NAME sunucu adı ile bir nesne başlatılır. Ardından, TLS oturumu başlamadan önce ad, SNI uzantısı API'si kullanılarak TLS'ye sağlanır. Ad ayardan sonra başka bir eylem gerekmez. 4. Bölüm'de API başvurusuna bakın  
  
Tek tek işlevler hakkında daha fazla bilgi için NetX Secure Services'ın açıklaması.

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
### <a name="sni-extension--tls-server"></a>SNI Uzantısı – TLS Sunucusu

TLS Sunucusu tarafında SNI uzantısı, el sıkışma sırasında uzak istemciye sağılacak uygun kimlik bilgilerini (örneğin sertifika) seçmek için uygulama tarafından işlenebilir. Bunu yapmak için uygulamanın ClientHello iletisinin alınmasından sonra çağrılan bir oturum geri çağırması göndermesi gerekir.

nx_secure_tls_session_server_callback_set API'si (bkz. sayfa 122) için örnek kod, sunucu geri çağırma kullanarak gelen SNI uzantısının ayrıştırıcısını gösterir. Temelde TLS Sunucusu bir ClientHello alır ve geri çağırmayı çağırır. Ardından *uygulama, SNI* uzantısını bulmak ve sağlanan DNS adını geri dönmek için geri çağırmaya sağlanan uzantı verilerini ayrıştırmak için nx_secure_tls_session_sni_extension_parse API'sini kullanır (uzantının yalnızca tek bir DNS adını desteklediğini unutmayın). Ad alındıktan sonra, uygulama uygun sunucu kimliği sertifikasını (ve varsa sertifikayı verir zincirini) bulmak ve göndermek için bunu kullanır.

### <a name="signature-algorithms-extension"></a>İmza Algoritmaları Uzantısı

Bu uzantı TLS 1.2'ye özeldir ve bir TLS İstemcisi'nin dijital imza oluşturma ve doğrulamada kullanım için kabul edilebilir kabul edilebilir imza ve karma algoritma çiftlerinin bir listesini sağlamasını sağlar. Liste, tls İstemcileri için NetX Secure TLS tarafından otomatik olarak oluşturulur ve bu, *nx_secure_tls_session_create.* Uygulama etkileşimi gerekmez.

## <a name="authentication-methods"></a>Kimlik Doğrulaması Yöntemleri

TLS, güvenli olmayan bir ağ üzerinden iki cihaz arasında güvenli bağlantı kurma çerçevesini sağlar, ancak sorunun bir parçası, bu bağlantının diğer ucundaki cihazın kimliğini bilmektir. Uzak ana bilgisayarların kimliğini doğrulamak için bir mekanizma olmadan, saldırganın güvenilen bir cihaz olarak oluşturabileceği önemsiz bir işlem haline gelir.

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

Sertifikalar için en yaygın biçimler DER ve Peg ' dir. DER ( *Distinguished Encoding Rules* için bir ASN. 1 biçimi), ilk el sıkışma gerçekleştirilirken TLS tarafından kullanılan ikili biçimdir. Peg ( *Gizlilik Gelişmiş posta*'ten), Web 'de http üzerinden gönderme veya gönderme için uygun olan der biçiminin base-64 kodlu bir sürümüdür. Farklı satıcılar, sertifika için ". pek" veya ". CRT" gibi farklı dosya adı uzantılarını ve DER sertifikaları için ". der" kullanır. Bir sertifikanız varsa ve bu, hangi biçimin kullanıldığını temizleyemiyorsa, dosyayı bir metin düzenleyicisinde açmak, DER dosyaları kodlanmış ikiliden itibaren türü belirlemenizi sağlar ve pek dosyaları, "-----başlangıç SERTIFIKASı-----" üstbilgisiyle başlayan normal ASCII metinlerdir.

NetX güvenli, sertifikanızın ikili DER biçiminde olmasını gerektirir, bu nedenle içeri aktarmadan önce sertifikanızı DER biçimine dönüştürmeniz gerekir. Bu, OpenSSL gibi kullanıma hazır araçlarla yapılabilir.

Uygulamanız için özel bir anahtara ihtiyacınız varsa, anahtar dosya belirli bir biçimde ped veya DER kullanılarak kodlanır (RSA için PKCS # 1, ECC için RFC 5915). Özel anahtar dosyasının içeri aktarılmadan önce DER olarak dönüştürülmesi gerekir.

Aşağıdaki OpenSSL komutları, sertifikaları ve RSA anahtar dosyalarını NetX Secure (ECC benzerdir – OpenSSL belgelerine bakın) için gereken DER biçimine dönüştürmeye yönelik bir örnek olarak verilmiştir.

```C
openssl x509 -inform PEM -in <certificate> -outform DER -out cert.der
openssl x509 -inform PEM -in <root CA cert> -outform DER -out CA_cert.der
openssl rsa -inform PEM -in <private key> -outform DER -out private.key
```
### <a name="private-keys-and-certificates"></a>Özel anahtarlar ve sertifikalar

Bir cihazı tanımlayan sertifikalar için, ilişkili özel anahtarın sertifikayla birlikte yüklenmesi gerekir. Özel anahtar (RSA, Diffie-Hellman veya Elliptic-Curve Cryptography gibi ortak anahtar algoritmalarından biri olabilir), bir TLS sunucusu tarafından, gelen anahtar malzemesinin ("Ana Gizlilik") bir TLS istemcisinden şifresini çözmek için kullanılır ve bu sayede istemcinin kimliğini kimlik doğrulamasını sağlar. Bir TLS Istemcisi için, bir kimlik sertifikası (ilişkili özel anahtarı olan bir sertifika) sağlanmışsa ve bir sunucu bir istemci sertifikası isterse, istemcinin kimliğini doğrulamak için özel anahtar kullanılır. RSA, istemci, istemcinin ortak anahtarını kullanarak sunucu şifresini çözdüğü özel anahtarı kullanarak bir belirteci şifreler,  istemci sertifikasında belirtilen (Diffie-Hellman ve ECC kimlik doğrulaması benzer bir şekilde gerçekleşir, ancak Ayrıntılar biraz farklıdır).

NetX güvenli ' te, Service *nx_secure_x509_certificate_initialize* bir X. 509.440 sertifikası başlatmak için kullanılır (daha fazla bilgi için bkz. "cihazınıza sertifika yükleme" bölümüne bakın) ve isteğe bağlı olarak özel bir anahtarı bu sertifikayla ilişkilendirin.

Özel anahtar sağlanırsa, sertifika, cihazı tanımlamak için kullanılan "kimlik" sertifikası olarak işaretlenir. Anahtar bitişik bir ikili blob ve bir uzunluğu, ilişkili anahtar türü olarak geçirilir. Anahtar türü anahtarın türüne (ör. RSA, ECC, vb.) ve biçimde (örn. PKCS # 1 DER) bağlıdır. Anahtar sağlanmazsa, hiçbir anahtar sağlanmakta olmadığını göstermek için NX_SECURE_X509_KEY_TYPE_NONE (değer 0x0) değeri geçirilebilir (0 uzunluğu ve veri parametresi için bir NX_NULL işaretçisi aynı etkiye ulaşacaktır).

Aşağıdaki tabloda NetX güvenli olarak bilinen anahtar türleri ve *nx_secure_x509_certificate_initialize* geçirilecek ilişkili tür tanımlayıcısı gösterilmektedir. NetX güvenli 'ye daha fazla şifreleme algoritması eklendikçe ek anahtar türleri eklenecektir.

| Tanımlayıcı                              | Algoritma | Biçimlendir   | Encoding | Değer |
| --------------------------------------- | --------- | -------- | -------- | ----- |
| NX_SECURE_X509_KEY_TYPE_NONE            | Hiçbiri      | Yok      | Yok      | 'dır   |
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

### <a name="basic-x509-validation"></a>Temel X.509 Doğrulaması

Herhangi bir gelen sertifika için NetX Secure TLS temel X.509 yol doğrulamasını gerçekleştirecek. Bu işlem, her bir sertifikanın dijital imzasını, uzak konak tarafından sağlansa veya güvenilen sertifika depolamada yer alsa da sertifikayı sertifikayı içeren sertifikaya karşı denetlemeyi içerir (güvenilen sertifikaları içeri aktarma hakkında daha fazla bilgi için "X.509 sertifikalarını NetX Secure'ye aktarma" bölümüne bakın). Doğrulama işlemi, güvenilir bir sertifikaya ulaşıncaya veya zincir sona erinceye kadar (otomatik olarak imzalanan sertifika veya eksik bir sertifika ile) sertifikayı alan sertifikalarda özyinelemeli olarak yinelenir. Güvenilen bir sertifikaya ulaşıldı ise sertifika doğrulanır, aksi takdirde reddedilir. Ayrıca, doğrulama işleminin her aşamasında her sertifikanın sona erme tarihi, uygulama zaman damgası işlevi tarafından sağlanan süreye göre denetlenir (daha fazla bilgi için "nx_secure_tls_session_time_function_set" hizmetine bakın).

X.509 belirtimi, yol doğrulaması sırasında denetlenen bir X.509 uzantısında bulunan tanımlayıcılar olan "ilkeleri" desteklemeye yönelik bir algoritma da sağlar. NetX Secure şu anda X.509 sertifikalarını "anyPolicy" seçeneği tanımlanmış gibi kabul eder; yani tüm ilkeler kabul edilebilir ve isteğe bağlı ilke denetimi gerçekleştirilemez. NetX Secure X.509 uygulaması, gelecek bir sürümde bu özellikle artırılmış olabilir. Şimdilik ilke uzantısı, api'sini kullanarak bir sertifikadan *nx_secure_x509_extension_find* olabilir.

Temel yol doğrulaması tamamlandıktan sonra TLS, uygulama tarafından sağlanan sertifika doğrulama geri çağrısını *api'sini nx_secure_tls_session_certificate_callback_set* çağırır. Geri arama sağlanmadı ise, başarılı yol doğrulamasının ardından sertifikaya güvenilir olarak kabul edilir. Bir geri çağırma sağlanırsa, geri çağırma uygulama için gereken sertifikanın ek doğrulamasını gerçekleştirecek. Geri çağırmadan dönüş değeri TLS el sıkışması ile devam etmek veya doğrulama hatası nedeniyle el sıkışmayı durdurmak için kullanılır.

Geri çağırma, ilgili TLS oturumunun işaretçisi ve doğrulanması NX_SECURE_X509_CERT bir işaretçisi ile çağrılır. TLS oturumu ile sertifika arasında, uygulama ek doğrulama denetimleri gerçekleştirmek için TLS'den gereken tüm verilere sahip olur.

Ek doğrulamaya yardımcı olmak için NetX Secure, DNS doğrulaması ve Sertifika İptal Listesi denetimi de dahil olmak üzere bazı yaygın doğrulama işlemleri için X.509 yordamları sağlar. Bu yordamların hepsi sertifika doğrulama geri çağırmada kullanılmaya uygundur, ancak X.509 sertifikalarının satır dışı denetlenmelerini gerçekleştirmek için de kullanılabilir.

Aşağıdaki tabloda, X.509 sertifika işleme için kullanılabilir yardımcı işlevler özetlenmiştir. İşlemler için daha ayrıntılı açıklamalar aşağıdaki bölümlerde ve 4. Bölümdeki API başvurusunda bulunabilir  
  
NetX Secure Services açıklaması, belirli yordamlarla ilgili ek ayrıntılar sağlar.

| **API Adı**                             | **Açıklama**                               |
| ---------------------------------------- | -------------------------------------- |
| nx_secure_x509_common_name_dns_check               | X.509 konu Ortak Adı ve SubjectAltName konularını beklenen bir DNS adıyla karşıdan kontrol edin |
| nx_secure_x509_crl_revocation_check                 | X.509 Sertifika İptal Listesi'ne (CRL) iptal edilmiş bir sertifikayı denetleme       |
| nx_secure_x509_extended_key_usage_extension_parse | Sertifikada belirli bir genişletilmiş anahtar kullanımı OID'lerini ayrıştırma ve bulma                   |
| nx_secure_x509_key_usage_extension_parse           | Sertifikada anahtar kullanımı bit alanı ayrıştırma ve iade                            |
| nx_secure_x509_extension_find                        | Belirli bir uzantı için ham DER ile kodlanmış ASN.1 verilerini bulup iade et.            |

Sertifika doğrulama geri çağırmada kullanmak için X.509 yardımcı işlevleri

### <a name="x509-extensions"></a>X.509 Uzantıları

X.509 belirtimi, sertifikaların doğrulanmasında kullanılmaktadır ek bilgi sağlamak için kullanılan bir dizi "uzantıyı" açıklar. Bu uzantılar çoğu zaman isteğe bağlıdır ve güvenilir bir kök sertifikaya karşı bir dijital sertifikanın güvenli doğrulaması için gerekli değildir. Ancak NetX Secure bazı temel uzantıları destekler. Gelecek sürümlerde ek uzantı desteği eklenebilir.

Şu anda desteklenen uzantılar aşağıdaki tabloda listelenmiştir:

| Uzantı Adı           | Description                                                                   | İlgili API                                             |
| ------------------------ | ----------------------------------------------------------------------------- | -------------------------------------------------------- |
| Anahtar Kullanımı                | Bit araklı bir sertifikanın ortak anahtarı için kabul edilebilir kullanımlar sağlar         | nx_secure_x509_key_usage_extension_parse           |
| Genişletilmiş Anahtar Kullanımı       | OID'leri kullanarak bir sertifikanın ortak anahtarı için ek kabul edilebilir kullanımlar sağlar | nx_secure_x509_extended_key_usage_extension_parse |
| Konu Diğer Adı | Sertifika tarafından da temsil edilen alternatif DNS adları sağlar   | nx_secure_x509_common_name_dns_check               |

### <a name="unsupported-x509-extensions"></a>Desteklenmeyen X.509 Uzantıları

NetX Secure'in X.509 işlemesi desteklenmeyen uzantıları ayıklamak için de bir hizmet sağlar: *nx_secure_x509_extension_find.* Bu API, döndürülen verileri ayrıştırmak için DER ile kodlanmış ASN.1 bilgisi gerektirdiği için ileri düzey kullanıcılara yöneliktir. Desteklenen uzantıları ayıklamak için dahili olarak kullanılır, ancak X.509 uzantıları için özelleştirilmiş destek geliştirmede kolaylık sağlamak için sağlanır.

Bu nx_secure_x509_extension_find için, NX_SECURE_X509_EXTENSION sertifika ve uzantı kimliği ile birlikte bilinen bir uzantı türü için değişken uzunluğu OID dizesinin tamsayı gösterimi olan bir uzantı kimliği geçirildi. X.509 uzantıları için desteklenen OID'lerin tam listesi, sayfa 178'deki nx_secure_x509_extension_find API başvurusunda sağlanır.

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
Hizmet başarıyla döndüğünde yapı, sertifikadan gelen ilgili verilerle doldurulur. Nx_secure_x509_extension_id alanı genellikle iç amaçlar için kullanılır, ancak ilgili OID tamsayı gösterimiyle doldurulur. Nx_secure_x509_extension_critical alanı X.509 kritik uzantı bayrağı değerini (Boole) ortaya çıkarır. Nx_secure_x509_extension_data ve nx_secure_x509_extension_data_length alanları, uzantı için DER ile kodlanmış ASN.1 verilerine ve bu verilerin uzunluğuna bir işaretçi içerir.

Uzantı ASN.1 verilerini gerçek olarak ayrıştırma bu belgenin kapsamının dışındadır, ancak NetX Secure TLS kaynağına erişiminiz varsa, desteklenen uzantılar için her zaman her nx_secure_x509_extension_find ayrıştırmanın nasıl nx_secure_x509_extension_find olduğunu görebilirsiniz.

### <a name="x509-dns-validation"></a>X.509 DNS Doğrulaması

TLS'de yaygın bir sertifika doğrulama işlemi, uzak bir ana bilgisayarın Top-Level Etki Alanı (TLD) adını TLS el sıkışması sırasında bu konak tarafından sağlanan X.509 sertifikasıyla denetlemeyi içerir. Bu işlem, DNS aramanın güvenilir olduğu varsayıldık, sertifikanın gerçekten de sertifikayı sağlanan ana bilgisayar sunucusuyla eşleyemelerini sağlamaya yardımcı olur. NetX Secure TLS'de bu işlevsellik, sertifikayı **ve** ana bilgisayar erişimi için kullanılan URL'nin TLD bölümünü içeren bir dizeyi alan hizmet nx_secure_x509_common_name_dns_check tarafından sağlanır. TLD, sertifikanın Ortak Ad alanıyla karşılaştırıldı ve eşdüzdü NX_SUCCESS döndürülür. Ortak Ad eşleşmezse yordam, *subjectAltName* adlı X.509 sertifika uzantısının varlığını da kontrol eder. SubjectAltName varsa, uzantıda tüm DNSName girdileri de sağlanan TLD'ye karşı denetlenir. Yine, herhangi bir eşleşme NX_SUCCESS döndürülür. Eşleşme bulunamasa, sertifika doğrulama geri çağırmadan dönmek için uygun bir hata döndürülür.

### <a name="x509-key-usage-and-extended-key-usage-extensions"></a>X.509 Anahtar Kullanımı ve Genişletilmiş Anahtar Kullanımı Uzantıları

X.509 Anahtar Kullanımı ve Genişletilmiş Anahtar Kullanımı uzantıları, bir sertifikanın ortak anahtarının bu sertifikanın kimlik doğrulamasını nasıl kullanılası hakkında bilgi sağlar. Anahtar kullanımı, sertifika imzalandı ve verildikleri zaman sertifikayı imzalayan tarafından sağlanır. Anahtar kullanımı, bir TLS ana bilgisayarı tarafından sertifikanın uzak BIR TLS ana bilgisayarının kimliğini doğrulamak ve diğer işlemleri gerçekleştirmek için kullanılma yetkisine sahip olup olamay için kullanılabilir.

Anahtar Kullanımı uzantısı, bitlerin her biri belirli bir anahtar kullanımını temsil eden basit bir bitfield'den oluşur. Bu değerlerin tam listesi, sayfa 183'te *nx_secure_x509_key_usage_extension_parse* API başvurusunda verilmektedir. Anahtar kullanım bitlerinin ve anlamlarının daha eksiksiz bir açıklaması için RFC 5280, bölüm 4.2.1.3'e bakın.

Anahtar Kullanımı uzantısı gibi Genişletilmiş Anahtar Kullanımı uzantısı da kabul edilebilir anahtar kullanımı bilgileri sağlar. Ancak, Genişletilmiş Anahtar Kullanımı uzantısı rastgele kullanımları desteklemek için bit alanı yerine OID'leri kullanır. NetX Secure X.509'da Genişletilmiş Anahtar Kullanımı uzantısı ayrıştırılırken, uygulama tarafından OID'yi temsil eden bir tamsayı sağlanır; nx_secure_x509_extended_key_usage_extension_parse hizmeti bu *OID'nin* mevcut olup olmadığını döndürür. Genişletilmiş Anahtar kullanımı için desteklenen OID'lerin tam listesi,  sayfa 175'te nx_secure_x509_extended_key_usage_extension_parse API başvurusunda verilmektedir. OID'ler ve anlamlarının daha eksiksiz bir açıklaması için 4.2.1.12 bölümü olan RFC 5280 bölümüne bakın.

### <a name="x509-crl-revocation-status-checking"></a>X.509 CRL İptal Durumu Denetimi

X.509, dijital sertifika  imzalama yetkilisinin imza verdiği sertifikaların geçerliliğini iptal etmelerini sağlayan Sertifika İptal Listesi (CRL) adlı bir mekanizma sağlar. İmzalama yetkililerinden sertifikaları doğrulaması gereken tüm uygulama bir CRL edinebilir ve herhangi bir nedenden dolayı durumlarının iptal edil olup (güvenliği tehlikeye atılmış özel anahtar gibi) olup o yetkili (sertifikayılayan) tarafından imzalanan sertifikaları CRL ile karşılaştırabilirsiniz. Bu şekilde, uygulama diğer sertifika doğrulama denetimlerini geçen tehlikeli olabilecek sertifikaları kullanmaktan kaçınabilirsiniz.

CRL elde etmek, der kodlanmış listesini önceden tanımlanmış bir sunucudan veya başka bir şekilde indirerek bir uygulama tarafından yapılır. Gerçek kurulum, sertifikayı sağlayandan sertifikayı sağlayana kadar değişir, bu nedenle NetX Secure CRL'leri almak için bir mekanizma sağlamaz, ancak CRL'ye karşı sertifikayı denetlemeye yönelik bir yordam sağlar ve **nx_secure_x509_crl_revocation_check.**

API, denetlenecek DER kodlanmış CRL,sertifika deposu (TLS oturumunda bulunan gibi) ve denetlenecek sertifikayı alır. Yordam ilk olarak CRL'nin kendisini güvenilir depoya karşı doğrular (uygulama tarafından sağlanan sertifika deposunun bir parçası). Bu, Hizmet Reddi saldırılarında kullanılan sahte CRL'lere karşı koruma sağlar ve CRL'nin gerçekten uygun bir sağlayıcıdan olduğunu tespit etmektir. CRL doğrulamasının ardından, sertifikayı teslim eden denetlenir; CRL'nin sertifikayı teslim edenle eşleşmezse CRL bu sertifika için geçerli değildir ve bir hata döndürülür. TLS el sıkışması bu noktada devam edip edesin mi olduğunu belirlemek uygulamaya bağlı. Sertifikayı alanlar eşlese CRL, doğrulanmış olan sertifikanın seri numarası için aranır. Seri numarası listede varsa, sertifikanın iptal edildiğini belirten bir hata döndürülür. Eşleşme bulunamasa NX_SUCCESS döndürülür.

## <a name="client-certificate-authentication-in-netx-secure-tls"></a>NetX Secure TLS'de İstemci Sertifikası Kimlik Doğrulaması

X.509 sertifika kimlik doğrulaması kullanılırken TLS protokolü, TLS Sunucusu örneğinin tanımlama için bir sertifika sağlamasını gerektirir, ancak varsayılan olarak TLS İstemci örneğinin kimlik doğrulaması için başka bir kimlik doğrulaması biçimi (kullanıcı adı/parola bileşimi gibi) kullanarak bir sertifika sağlaması gerekli değildir. Bu, Web siteleri için internet üzerinde en yaygın TLS kullanımıyla eştir. Örneğin, bir çevrimiçi perakende satış sitesi, web tarayıcısı kullanan potansiyel bir müşteriye sunucunun meşru olduğunu kanıtlamalı, ancak kullanıcı belirli bir hesaba erişmek için bir oturum açma/parola kullanır.

Ancak, varsayılan durum her zaman tercih edilmez, bu nedenle TLS isteğe bağlı olarak TLS Sunucusu örneğinin uzak İstemciden sertifika isteğine izin verir. Bu özellik etkinleştirildiğinde TLS Sunucusu, el sıkışma sırasında TLS İstemcisi'ne bir CertificateRequest iletisi gönderir. İstemci, kendi sertifikası ve İstemcinin bu sertifikayla ilişkilendirilmiş eşleşen özel anahtara sahip olduğunu kanıtlayan bir şifreleme belirteci içeren bir CertificateVerify iletisiyle yanıt ver ver versin. Doğrulama başarısız olursa veya sertifika Sunucu'da güvenilir bir sertifikaya bağlı olmazsa TLS el sıkışması başarısız olur.

TLS'de İstemci Sertifikası Kimlik Doğrulaması için iki ayrı durum vardır; aşağıdaki bölümlerde her iki durum da yer almaktadır.

### <a name="client-certificate-authentication-for-tls-clients"></a>TLS İstemcileri için İstemci Sertifikası Kimlik Doğrulaması

TLS İstemcisi, istemci kimlik doğrulaması için sertifika talep etmek için sunucuyla bağlantı girişiminde olabilir. Bu durumda İstemcinin sunucuya bir sertifika sağlaması ve eşleşen özel anahtarın sahibi olduğunu doğrulaması gerekir, yoksa Sunucu TLS el sıkışmasını sonlandırılır.

NetX Secure TLS'de bu özelliği destekleyecek özel bir yapılandırma yoktur, ancak uygulamanın nx_secure_tls_local_certificate_add hizmetini kullanarak TLS İstemci örneği için yerel bir *kimlik sertifikası sağlaması* gerekir. Uygulama tarafından sertifika sağlanıyorsa ama uzak sunucu İstemci Sertifikası Kimlik Doğrulaması kullanıyorsa ve bir sertifika talep ediyorsa, TLS el sıkışması başarısız olur. TLS Oturumu'nx_secure_tls_local_certificate_add tls  el sıkışmasını tamamlamak için uzak sunucu tarafından tanınması gerekir.

### <a name="client-certificate-authentication-for-tls-servers"></a>TLS Sunucuları için İstemci Sertifikası Kimlik Doğrulaması

İstemci Sertifikası Kimlik Doğrulaması için TLS Sunucusu durumu, özelliğin isteğe bağlı olması nedeniyle TLS İstemcisi örneğinden biraz daha karmaşıktır. Bu durumda, TLS Sunucusunun özellikle uzak TLS İstemcisi'den bir sertifika isteğinde olması, ardından uzak İstemcinin eşleşen özel anahtara sahip olduğunu doğrulamak için CertificateVerify iletiyi işlemesi gerekir ve ardından Sunucu, İstemci tarafından sağlanan sertifikanın yerel güvenilen sertifika depolama alanı içinde bir sertifikaya izlenebilir olup olamı gerektiğini denetlemesi gerekir.

NetX Güvenli TLS Sunucusu örneklerde İstemci Sertifikası Kimlik Doğrulaması tarafından denetlenmektedir <br>
*nx <span class="underline"> _</span> secure <span class="underline">_</span>tls <span class="underline"> _</span> oturum istemcisinin <span class="underline">_</span>etkinleştirme <span class="underline"> _</span> ve <span class="underline">_</span>doğrulama*<br>
*nx <span class="underline"> _</span> secure <span class="underline">_</span>tls <span class="underline"> _</span> oturum istemcisi doğrulama <span class="underline">_</span>hizmetleri <span class="underline"> _</span> devre <span class="underline">_</span>dışı* bırak.

İstemci Sertifikası Kimlik Doğrulamasını etkinleştirmek için bir uygulamanın çağrısı gerekir<br>
*nx <span class="underline"> _</span> secure <span class="underline">_</span>tls <span class="underline"> _</span> session client <span class="underline">_</span>verify <span class="underline"> _</span> enable <span class="underline">_</span>* with the TLS Server session instance before calling *nx_secure_tls_session_start.* Bu hizmeti TLS İstemci bağlantıları için kullanılan bir TLS Oturumunda çağırmanın hiçbir etkisi olmaz.

İstemci Sertifikası Kimlik Doğrulaması etkinleştirildiğinde, TLS Sunucusu, TLS el sıkışması sırasında uzak TLS İstemcisi'den bir sertifika talepte bulunduracak. NetX Güvenli TLS Sunucusu'da İstemci sertifikası, X.509 sertifikayı teslim eden zincirinin ardından *nx <span class="underline"> _</span> secure_tls <span class="underline">_</span><span class="underline"> _</span> <span class="underline">_</span>* güvenilen sertifika ekleme ile oluşturulan güvenilen sertifika deposuna karşı denetlenir. Uzak İstemcinin kimlik sertifikasını güvenilen depoda bir sertifikaya bağlayan bir zincir sağlaması gerekir, yoksa TLS el sıkışması başarısız olur. Ayrıca CertificateVerify ileti işlemesi başarısız olursa TLS el sıkışması da başarısız olur.

CertificateVerify yöntemi için kullanılan imza yöntemleri TLS sürüm 1.0 ve TLS sürüm 1.1 için sabittir ve TLS sunucusu tarafından TLS sürüm 1.2'de belirtilir. TLS 1.2 için desteklenen imza yöntemleri genellikle şifreleme yöntemi tablosunda sağlanan ilgili yöntemleri kullanır, ancak genellikle SHA-256 ile RSA 'yı kullanır (şifreleme yöntemleriyle TLS'yi başlatma hakkında daha fazla bilgi için "NetX Secure TLS'de şifreleme" bölümüne bakın).

## <a name="cryptography-in-netx-secure-tls"></a>NetX Secure TLS'de şifreleme

TLS, şifrelemenin ağ iletişimlerini güvenli hale almak için kullanıla bir protokol tanımlar. Bu nedenle, kullanılacak gerçek şifrelemeyi TLS kullanıcıları için oldukça açık bırakır. Belirtim için yalnızca tek bir şifrelemenin uygulanması gerekir. TLS 1.2 olması durumunda bu şifreleme TLS_RSA_WITH_AES_128_CBC_SHA şeklindedir ve ortak anahtar işlemleri için RSA, oturum şifrelemesi için 128 bit anahtarlı CBC modunda AES ve ileti kimlik doğrulama karmaları için SHA-1 kullanılır.

TLS 1.2 ile uyumlu olan NetX Secure, varsayılan olarak zorunlu TLS_RSA_WITH_AES_128_CBC_SHA şifrelemesini sağlar ancak donanım özellikleri ve diğer önemli noktalar nedeniyle şifreleme yöntemlerinin her biri için olası uygulama sayısı göz önünde bulundurularak NetX Secure, kullanıcının TLS ile hangi şifreleme yöntemlerinin kullanılamayacaklarını belirtmesini sağlayan genel bir şifreleme API'si sağlar.

NOT: Genel şifreleme API'si mekanizması kullanıcıların kendi şifrelerini uygulamasına da olanak sağlar, ancak bu, TLS şifre birimlerini ve uzantılarını bilen ileri düzey kullanıcılar için önerilir. Kendi şifrelerinizi desteklemekle ilgileniyorsanız lütfen Express Logic temsilcinize başvurun.

### <a name="cryptographic-methods"></a>Şifreleme Yöntemleri

NetX Secure TLS, belirli donanım platformları için donanım sürücülerine sahip yazılımlarda DES, 3DES, AES, MD5, HMAC-MD5, SHA-1, HMAC-SHA1, SHA-256, HMAC-SHA256, RSA ve ECC (seçili eğriler) uygulamalarını sağlar. Bir uygulama, NetX Secure ile sağlanan şifreleme yordamlarını veya son kullanıcı veya üçüncü taraflar tarafından sağlanan özel yordamları kullanabilir.

Bu *NX_CRYPTO_METHOD,* NetX Secure TLS ile kullanılacak şifreleme algoritmasının belirli bir uygulamasını açıklamak üzere bir uygulama için tasarlanmış bir denetim bloğu değildir. Uygulama, *NX_CRYPTO_METHOD kendi* şifreleme uygulamasını NetX Secure ile kolayca tümleştirebilir. NX_CRYPTO_METHOD  yapısı şu şekilde bildirildi:

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

Aşağıda, veri yapısında yer alan her *öğenin NX_CRYPTO_METHOD* verilmiştir:

- nx_crypto_algorithm: Bu alan değişken yönteminde açıklanan  algoritmayı tanımlar NetX Secure TLS için bazı geçerli değerler aşağıdaki gibidir (belirli değerler için nx_crypto_const.h'ye bakın):
    
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

- nx_crypto_IV_size_in_bits: Bu alan Başlatma Vektörü 'nin (IV) boyutunu belirtir. Çoğu durumda IV bloğu yalnızca şifreleme/şifre çözme algoritmaları için kullanılır. Kimlik doğrulama ve doğrulama algoritmaları bu alanı nadiren kullanır.

- nx_crypto_ICV_size_in_bits: Bu alan, Bütünlük Denetimi Değeri (ICV) bloğu boyutunu belirtir. NOT: Bu blok IPsec kullanımına bağlıdır ve TLS'de kullanılmaz. Daha fazla bilgi için bkz. NetX Duo IPsec.

- nx_crypto_block_size_in_bytes: Bu alan, blok tabanlı şifrelemeler için şifreleme algoritması bloğu boyutunu bayt cinsinden belirtir. Çoğu durumda bu, şifreleme yordamları tarafından ve nadiren kimlik doğrulama yordamları tarafından kullanılır.

- nx_crypto_metadata_area_size: Bu alan, bu yöntemin gerektirdiği meta veri alanı boyutunu belirtir. Her uygulama, durum bilgilerini depolamak ya da ara verileri (anahtar dönüştürme malzemeleri gibi) depolamak veya karalama alanı olarak kullanmak için belirli bir bellek gerektirir. Bir uygulama için gereken alan miktarı bu alanda belirtilir. Uygulama, TLS oturumu oluştururken bellek alanı sağlar. Şifreleme işlevi bu meta veri alanı yönetiminden sorumludur.

- nx_crypto_init: Şifreleme algoritması için başlatma işlevidir. Başlatma yordamı gerektiren bir uygulama için, bu alan bir NX_NULL. Başlatma işlevinin tipik bir kullanımı, algoritma için iç veri yapısını başlatmaktır. NetX Secure TLS, bu işlevi dahili olarak çağırarak şifreleme yordamının başlatmasını işlemektedir.

Başlatma işlevinin prototipi şudur:

```C
UINT crypto_init_function(NX_CRYPTO_METHOD *method, 
                          UCHAR *key, 
                          UINT  key_size_in_bits, 
                          VOID  **handle, 
                          VOID  *crypto_metadata_area, 
                          ULONG crypto_metadata_area_size);
```

  - yöntemi, şifreleme yöntemi denetim bloğuna bir işaretçidir.

  - key, veri paketlerinin iş için gizli anahtar dizesidir.

  - key_size_in_bits gizli anahtarın boyutunu bitler olarak tanımlar.

  - handle, belirli bir şifreleme oturumunu tanımlayan uygulama tanımlı bir öğedir. değer başlatma yordamı tarafından oluşturulur ve çağırana geri geçirilir. Sonraki şifreleme işlemi veya temizleme yordamı oturumu tanımlamak için bu tanıtıcıyı kullanır.

  - crypto_metadata, bu algoritmanın uygulanması için gereken meta veri alanına yönelik bir işaretçidir. Meta veri alanına ihtiyacı olan algoritmalar için bu alan NX_NULL olarak ayarlanır ve başlatma yordamı meta veri alanına erişmez.

  - crypto_metadata_size meta veri alanı boyutunu belirtir. Meta veri alanı olmadan oluşturulan SA'lar için bu alan sıfır olarak ayarlanır ve başlatma yordamının meta veri alanına erişmesi gerekir.

  - Başlatma işlemi başarılı *NX_SUCCESS* bu yordamda geri dönüş gerekir. Çağıran, diğer herhangi bir dönüş değerini hata olarak davranır.

- nx_crypto_cleanup: Bu, bir şifreleme algoritmasının uygulanması için tanımlanan temizleme yordamıdır. TlS oturumu silindiğinde veya yeniden başlatıldığında çağrılır.

Temizleme işlevinin prototipi şudur:

```C
UINT crypto_cleanup_function(VOID *handle);
```
- tanıtıcı, çağıranın temizleme işlevine geçirilir. Tanıtıcı, şifreleme başlatma yordamı tarafından başlatılır ve şifreleme algoritması durumunu tanımlamak için kullanılır.

- Temizleme işlemi başarılı *NX_SUCCESS* bu yordam geri dönüş yapabilir. Çağıran, diğer herhangi bir dönüş değerini hata olarak davranır.

- nx_crypto_operation: Bu, gerçek şifreleme, şifre çözme ve kimlik doğrulama hizmetlerini gerçekleştiren yordamdır. İşlem yordamının işlev prototipi şöyledir:

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

- op, bu yordamın gerçekleştireceği işlem türünü gösterir. Geçerli değerler:
    
    - NX_CRYPTO_ENCRYPT
    - NX_CRYPTO_DECRYPT
    - NX_CRYPTO_AUTHENTICATE
    - NX_CRYPTO_VERIFY

- tanıtıcı, çağıranın işlem işlevine geçirilir. Şifreleme başlatma yordamı tarafından oluşturulur.
- yöntem, şifreleme yöntemi denetim bloğuna
- anahtar, bu işlem için kullanılan gizli anahtara yöneliktir
- key_size_in_bits, bitler içinde gizli anahtarın boyutudur
- input, üzerinde çalıştırılan iletinin başlangıcına bir işaretçidir.
- input_length_in_byte, çalıştırılan iletinin boyutunu belirtmek için çağrıyı yapan tarafından geçirilir.
- iv_ptr, bir IV bloğun başlangıcına işaret etmek için çağıranın ayarlamasıdır. IV bloğu için belleğin çağıranın sağladığını unutmayın. Şifreleme için, işlem işlevi IV bilgilerini bu bellek bloğuna yazmalı; şifre çözme için işlem işlevinin bu bellek bloğundan IV bilgilerini alması gerekir. Kimlik doğrulama ve doğrulama işlemi algoritmaları genellikle başlatma vektörü kullanmaz.
- output, çağıranın bir çıkış arabelleğine işaret etmek için kurulumu sağlar. Çıkış arabelleğinin belleğinin çağıranın sağladığını unutmayın. Şifreleme için, işlem işlevinin çıkış arabelleğine şifreleme metnini yazması gerekir; şifre çözme için işlem, çıkış arabelleğine deşifre metni (şifresiz metin) yazmalı; kimlik doğrulaması için karma değeri çıkış arabelleğine yazıldığına göre. Doğrulama için, karma bilgileri depolamak için çıkış arabelleği kullanılır.
- output_length_in_byte, çıkış arabelleğinin boyutunu gösterir
- crypto_metadata şifreleme işlemi tarafından kullanılacak meta veri alanına yöneliktir. Şifreleme meta verileri alanı genellikle veri kaynağı tarafından crypto_init_function.
- crypto_metadata_size meta veri alanı boyutunu gösterir.
- bu yordam, *NX_SUCCESS* başarılı olursa bu yordamın geri dönmesini sağlar. Çağıran, diğer herhangi bir dönüş değerini hata olarak davranır.
- packet_ptr: İşlenen verileri içeren paket. NOT: Bu parametre TLS tarafından kullanılmamış ve bu parametre NX_NULL.
- nx_crypto_hw_process_callback: Şifreleme yöntemi tarafından sağlanan bir geri çağırma işlevi. Şifreleme işlevi donanım tarafından sağlanıyorsa ve bir geri çağırma yordamı gerektiriyorsa bu kullanılır.

NetX Secure TLS aşağıdaki şifreleme yöntemlerini sağlar:

- *AES*  
- *Rsa*  
- *Null*

NetX Secure TLS aşağıdaki kimlik doğrulama yöntemlerini sağlar:

- *HMAC-MD5*  
- *HMAC-SHA1*  
- *HMAC-SHA256*

Aşağıdaki örnekler, NetX Duo IPsec *NX_CRYPTO_METHOD* şifreleme ve kimlik doğrulama yöntemlerini kullanmak için yapılandırmayı göstermektedir.

***Aes:***

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
***Null***

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
***Hiçbiri***

IPsec **NX_CRYPTO_NONE** şifreleme veya kimlik doğrulama hizmetinin gerekli olmadığının sinyallerini sağlamak için özel bir yöntem kullanılır. Aşağıdaki gibi yapılandırılır:

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
### <a name="initializing-tls-with-cryptographic-methods"></a>Şifreleme Yöntemleriyle TLS'yi Başlatma

Önceki bölümde açıklanan şifreleme yöntemi imzalarına uygun şifreleme yordamlarınızı oluşturduktan sonra, yeni bir denetim bloğu NX_SECURE_TLS_SESSION gerekir. Bu, TLS hizmet hizmet nx_secure_tls_session_create:

```C
UINT  nx_secure_tls_session_create(
              NX_SECURE_TLS_SESSION*     session_ptr,
              const NX_SECURE_TLS_CRYPTO*    tls_cipher_table,
              VOID*                encryption_metadata_area,
              ULONG                 encryption_metadata_size
);
```
- session_pointer, denetim bloğuna NX_SECURE_TLS_SESSION işaretçidir.
- tls_cipher_table, aşağıda açıklanan bir NX_SECURE_TLS_CRYPTO denetim bloğuna bir işaretçidir.
- encryption_metadata_area TLS'de şifreleme yordamları tarafından kullanılan alana bakın.
- encryption_metadata_size, meta veri alanı boyutunu bayt cinsinden belirtir.

### <a name="elliptic-curve-cryptography-ecc-in-netx-secure-tls"></a>NetX Secure TLS'de Eliptik Eğri Şifrelemesi (ECC)

Eliptik Eğri Şifrelemesi (ECC), RSA yerine kullanılan bir ortak anahtar şifreleme şeması sağlar. ECC genellikle daha hızlıdır ve ekli TLS için değerli bir seçenek olması için RSA'dan daha küçük anahtarlar kullanır. Azure RTOS 6.0'dan önceki X-Ware sürümlerinde, ECC bir eklenti olarak gönderildi ve bu nedenle ECC kaynak kodunun projenize yüklenmesi gerektirildi. Azure RTOS 6.0 tümleşik ECC'nin ana satır kod tabanına yüklenmesine gerek kalmadan 6.0 ile tümleştirilmiştir. Ancak, ECC yine de önceki sürümlerle aynı başlatmayı gerektirir.

### <a name="supported-ecc-curves"></a>Desteklenen ECC eğrileri

NetX Secure, eğrilerin bölümlerine göre <http://www.secg.org/sec2-v2.pdf> uygulanır. Aşağıdaki eğriler<sup>18'i destekler:</sup>

  - secp256r1 
  - secp384r1 
  - secp521r1 

Diğer ECC eğrileri kullanılırsa *nx_secure_tls_session_start()* yordamı, desteklenmeyen eğrilerin NX_SECURE_TLS_NO_SUPPORTED_CIPHERS hata iletisini döndürür.

TLS sertifika zincirinin ECC algoritmaları tarafından da şifrelenmiş olduğunu unutmayın. TLS İstemcisi tarafından sağlanan eğriler desteklenmiş olsa da, sertifika zincirinde kullanılan ECC eğrisi desteklenmiyor olabilir. Bu durumda, *nx_secure_tls_session_start* işlevi NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER.

ECC için varsayılan bir şifreleme tablosu örneği nx_crypto_generic_ciphersuites.c.'de sağlanmıştır. Şifreleme tabloları hakkında daha fazla bilgi için "TLS Şifreleme Şifreleme Tablosu" bölümüne bakın.

18. Eski uygulamalar için secp192r1 ve secp224r1 eğrileri için uygulamaların da sağlanmıştır. Ancak bu eğriler artık zayıf olarak kabul edilir ve yeni uygulama geliştirme için KULLANIMMAMALI.

### <a name="crypto-methods-for-ecc"></a>ECC için Şifreleme Yöntemleri

Eliptik Eğri grupları için şifreleme yöntemleri:

- NX_CRYPTO_METHOD crypto_method_ec_secp192<sup>15;</sup>  
- NX_CRYPTO_METHOD crypto_method_ec_secp224<sup>15;</sup>  
- NX_CRYPTO_METHOD crypto_method_ec_secp256;  
- NX_CRYPTO_METHOD crypto_method_ec_secp384;  
- NX_CRYPTO_METHOD crypto_method_ec_secp521;

ECC eğrileri için şifreleme yöntemleri nx_crypto_generic_ciphersuites.c.

ECDHE için şifreleme yöntemi:

- NX_CRYPTO_METHOD crypto_method_ecdhe;

ECDSA için şifreleme yöntemi:

- NX_CRYPTO_METHOD crypto_method_ecdsa;

ECDSA ve ECDHE şifreleme yöntemleri nx_crypto_generic_ciphersuites.c.

RSA, SHA, AES gibi diğer şifreleme yöntemleriyle birlikte, şifreleme arama tablosu için yapı taşları olarak kullanılabilirler.

### <a name="enabling-ecc-support-for-tls"></a>TLS için ECC Desteğini Etkinleştirme

TLS için ECC varsayılan olarak etkindir. ECC desteğini devre dışı bırakmak için NX_SECURE_DISABLE_ECC_CIPHERSUITE simgesi tanımlanmalıdır.

Değişikliğin etkili olmak için NetX Güvenli Kitaplığını ve bu kitaplığı kullanan tüm uygulamaları yeniden oluşturmanız gerekir.

Uygulama kodunda, TLS *oturumu oluşturulduktan sonra* api n x_secure_tls_ecc_initialize() çağrılabilir. Bu API, TLS anahtar değişimi işlemleri ve sertifika doğrulaması için kullanılacak eğri türünün TLS oturumuna bilgi sağlar. TLS el sıkışması aşamasında, bir ECC algoritması seçilirse istemci ve sunucu, hangi eğriyi kullanmak üzere karar vermek için ECC eğrisi ile ilgili parametreleri kullanır.

Aşağıdaki kod kesimi, API'nin nasıl kullanıla bir şekilde gösterildiğini gösterir. bağımsız değişkenlerini *(nx_crypto_ecc_supported_groups, nx_crypto_ecc_supported_groups_size ve nx_crypto_ecc_curves)* *nx_crypto_generic_ciphersuites.c içinde tanımladı.* Bu nedenle bu semboller doğrudan kullanılabilir.

```C
status = nx_secure_tls_ecc_initialize(&tls_session,     
                    nx_crypto_ecc_supported_groups,      
                    nx_crypto_ecc_supported_groups_size,     
                    nx_crypto_ecc_curves);
```
nx_crypto_generic_ciphersuites.c'de örnek yapılandırma, ECC etkinleştirildiğinde kullanılan bir ECC şifreleme arama tablosu içerir. ECC'yi kullanmak için, nx_crypto_tls_ciphers_ecc ile TLS oturumları oluştururken şifreleme tablosu parametresi olarak nx_secure_tls_session_create. Örnek tablo hem ECC hem de ECC olmayan şifrelemeleri içerir.

### <a name="tls-cryptographic-cipher-table"></a>TLS Şifreleme Şifreleme Tablosu

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
Tablo, bu yapı için girdileri NetX Secure TLS projesi içinde bulunan ve genellikle şifreleme yordamları ve modüllerle birlikte bulunan statik bir sabitte doldurularak oluşturulur.

Örneğin, NetX Secure ile sağlanan yalnızca yazılım ("genel") şifreleme kitaplığı aşağıdaki tablo tanımını içerir (ECC dışı şifreleme desteği<sup>için 19):</sup>

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
Yapıda ilk giriş TLS şifreleme tablosudur. Bu NX_SECURE_TLS_CIPHERSUITE_INFO, şifreleme yordamlarını (NX_CRYPTO_METHOD işaretçileri şeklinde) TLS belirtimleri içinde tanımlanan belirli şifrelemelere eşler. İkinci değer, tablodaki ilk alanın işaret ettiği giriş sayısıdır.

Sonraki alan, X.509 tarafından dijital sertifikalar işleme sırasında kullanılan yordamların bir tablosuna ve NX_SECURE_X509_CRYPTO yapısı, X.509'a NX_SECURE_TLS_CIPHERSUITE_INFO. Aşağıdaki alan, tablodaki girdilerin sayısıdır.

Arama tablosunun ardından TLS'nin belirli sürümleri için gereken bir dizi yordam vardır. Örneğin TLS sürüm 1.2'den önce anahtar oluşturma ve el sıkışma karma yordamları SHA-1 ve MD5'in bir birleşimini kullanmak üzere düzeltildi. Bu yordamlara yönelik yöntemler, belirli şifrelere bağlı olmayan şifreleme yapısında özel olarak çağrılır. TLS sürüm 1.2'de anahtar oluşturma ve karma yordamları şifreleme tarafından seçilir, ancak kullanılacak yordamları belirtmeden şifrelemeler için SHA-256 karma yöntemi kullanılır ve şifreleme yapısı bu yordamı özellikle belirtir.

TLS 1.3, çeşitli işlemler için birkaç ek özel şifreleme gerektirir.

19. TLS 1.3 desteğinin ECC gerektirdiğini unutmayın; TLS 1.3 nx_crypto_tls_ciphers_ecc etkinse bu desteği kullanın.

### <a name="tls-ciphersuite-lookup-table"></a>TLS Şifreleme Arama Tablosu

TLS şifreleme tablosunu doldurmak için şifreleme yordamlarını belirli şifreleme tanımlayıcılarına eşleen bir şifreleme arama tablosu da oluşturmanız gerekir. Tanımlayıcılar, evrensel IANA'ya kayıtlı değerlerdir. Daha fazla bilgi için bkz. TLS RFC'leri. Yordamlar her bir şifrede kullanılan 5 ayrı yöntemi temsil ediyor (bazı şifrelemeler 5'ini de kullanmayabiliyor): ortak şifreleme, ortak anahtar kimlik doğrulaması, oturum şifrelemesi, oturum karma yordamı ve TLS Pseudo-Random İşlevi (PRF). Aşağıdaki tabloda 5 yöntemin her biri açık almaktadır:

| **Rutin kategori**      | **Açıklama**                                                                                       | **Örnek algoritmalar**                                            |
| ------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Genel şifreleme             | TLS el sıkışması sırasında anahtarları takas etmek için kullanılır                                                        | RSA, Diffie-Hellman, ECC                                          |
| Ortak anahtar kimlik doğrulaması | TLS el sıkışması sırasında verilerin kimliğini doğrulamak veya imzalamak için kullanılır                                            | RSA, DSS                                                          |
| Oturum şifrelemesi            | TLS oturumu sırasında uygulama verilerini şifrelemek için kullanılan simetrik anahtar algoritması                       | AES, RC4                                                          |
| Oturum karması              | TLS oturumu sırasında iletilerin bütünlüğünü korumak için kullanılır (verilerin değişmediğini garantiler) | SHA-1, SHA-256                                                    |
| TLS PRF                   | TLS el sıkışması içinde anahtar malzeme ve el sıkışma karması oluşturmak için kullanılır                          | PRF karma yordamlarını temel almaktadır : SHA-1 + MD5, SHA-256, SHA-512 |

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
Bu nx_secure_tls_ciphersuite IANA şifreleme değerini içerir ve NX_CRYPTO_METHOD işaretçileri bu şifreleme tarafından kullanılan 5 yöntemi temsil ediyor. Skaler değerler (nx_secure_tls_iv_size, nx_secure_tls_key_size ve nx_secure_tls_hash_size), veri girişlerinde mevcut NX_CRYPTO_METHOD sağlar.

Örneğin TLS, TLS_RSA_WITH_AES_128_CBC_SHA için varsayılan şifrelemeye bakarak RSA, 128 bit anahtarlı AES-CBC ve oturum karma için SHA-1 kullanımını belirtir. Bu şifreleme için TLS PRF belirtilmez, bu nedenle TLSv1.2 modunda varsayılan SHA-256 PRF'yi kullanır. Tabloda belirtilen PRF'den bağımsız olarak tüm şifrelemelerin TLS 1.0 ve 1.1'de SHA-1+MD5 PRF'lerini kullana olduğunu unutmayın.

Genel şifreleme NX_SECURE_TLS_CIPHERSUITE_INFO tablodaki giriş aşağıdaki gibi tanımlanır:

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

Oturum şifrelemesi için anahtar boyutunun şifreleme tarafından belirlendiği, ancak ortak anahtar yöntemleri için ortak anahtarlar el sıkışma sırasında alışveriş yapılan dijital sertifikalarda yer alan tlS el sıkışması devam edinceye kadar anahtar boyutu bilinmemektedir.

### <a name="x509-cipher-lookup-table"></a>X.509 Şifreleme Arama Tablosu

Aşağıdaki tabloda NX_SECURE_TLS_CIPHERSUITE_INFO, şifreleme NX_SECURE_X509_CRYPTO bilinen değerlerle eşler. X.509 durumunda tanımlayıcılar aslında X.509 tarafından tanımlanan ve ISO ve ITU standartları gövdeleriyle kaydedilmiş OID'lerdir. OID'ler, dijital sertifikalarda kullanılan şifreleme yordamları da dahil olmak üzere çeşitli telekomünikasyon standartlarında çeşitli bilgileri benzersiz olarak tanımlamak için tasarlanmış değişken uzunluklu çoklu bayt değerleridir. OID'ler değişken uzunlukta olduğu için NetX Secure TLS, resmi OID değerlerini dahili olarak kullanılan sabit uzunluklu sabitlerle eşler (bkz. nx_secure_x509.h). Bu sabitler, NX_SECURE_X509_CRYPTO şekilde tanımlanan bir yapıda kullanılır:

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

İlk alan olan *nx_secure_x509_crypto_identifier,* NetX Secure tarafından kullanılan iç OID gösterimidir.

İkinci ve üçüncü alanlar, NX_CRYPTO_METHOD bir karma yordamla eşleştirilmiş ortak anahtar işlemi olan OID tarafından tanımlanan şifreleme yöntemlerini temsil eden nesnelere işaret eder. Her dijital sertifikanın şifreleme yordamları için birden fazla OID'ye sahip olduğunu unutmayın.

X.509 için yöntem tablosu, şifreleme arama tablosuyla aynı şekilde oluşturulur. Örnek olarak, OID'ye RSA_SHA1. Bu durum için gerçek RSA_SHA1 OID şu şekildedir:

```C
{iso(1) member-body(2) us(840) rsadsi(113549) pkcs(1) pkcs-1(1) sha1-with-rsa-
signature(5)}
```
OID ASN.1 söz dizimsinde temsil edilen ve 1.2.840.113549.1.1.5 sayısal değerine sahip. Bu değer daha sonra ikili biçimde kodlanmış ve aşağıdaki baytlar oluşturulur:

```C
UCHAR RSA_SHA1_OID = { 0x2A, 0x86, 0x48, 0x86, 0xF7, 0x0D, 0x01, 0x01, 0x05 };
```
ASN.1'den ikili biçime gerçek dönüştürme bu belgenin kapsamının dışındadır. Daha fazla bilgi için OID'ler için ASN.1 kodlamalarını ara. NetX Secure tarafından desteklenen OID'lerin ikili gösterimi, *nx_secure_x509.c dosyasında bulunabilir.*

Gerçek OID'nin dahili olarak tanınan bir sabitle eşlenimi oluşturdukktan sonra, aşağıdaki tabloda RSA_SHA1 için NX_SECURE_X509_CRYPTO oluşturabiliriz:

```C
{ 
    NX_SECURE_TLS_X509_TYPE_RSA_SHA_1,    /* Internal OID constant. */
    &crypto_method_rsa,                   /* RSA method (NX_CRYPTO_METHOD). */ 
    &crypto_method_sha1                   /* SHA-1 method (NX_CRYPTO_METHOD). */
}, 
```
### <a name="default-tls-routines"></a>Varsayılan TLS Yordamları

Yukarıda belirtildiği gibi TLS, el sıkışma sırasında anahtar oluşturma ve ileti doğrulama için bazı varsayılan yordamlar gerektirir. Birincil yordam TLS Pseudo-Random İşlevi veya PRF'dir. PRF karma yordamları temel almaktadır ve anahtar oluşturma veya diğer amaçlar için rastgele miktarda sözde rastgele<sup>veri 20</sup> oluşturmak için kullanılabilir.

PRF'ye ek olarak, her TLS sürümü de sağlanacak varsayılan karma yordamları kullanır. TLS sürüm 1.0 ve 1.1 için bu karma yordamlar MD5 ve SHA-1'dir. TLS sürüm 1.2 yalnızca SHA-256 gerektirir.

NX_SECURE_TLS_CRYPTO yapısında MD5, SHA-1, SHA-256, TLS sürüm 1.0/1.1 PRF ve varsayılan TLS 1.2 PRF için NX_CRYPTO_METHOD işaretçileri vardır.

TLS 1.3 desteği HKDF (anahtar oluşturma), HMAC (el sıkışma sırasında kullanılan belirli karma işlemleri için) ve ECDHE (TLS 1.3 işlevselliği için gereklidir) alanları ekler.

Genel yazılım şifreleme kitaplığında sağlanan, TLS PRF'nin yazılım sürümleridir. TLS 1.0/1.1 için bu işlev *nx_crypto_tls_prf_1.* TLS 1.2 için işlevi *nx_secure_tls_prf_sha256.* "1" soneki eski TLS 1.0 PRF'yi temsil eder ve "sha256" soneki, TLS 1.2 varsayılan PRF'si SHA-256'yı temel alır. Diğer PRF yordamları için destek gerektiğinde, bu yordamların son eki kullanılan karma yöntemi yansıtacak. PRF yordamları karma yöntemleri temel alarak, temel karma yordamları farklı hedef platformlarda bağımsız olarak donanım hızlandırmalı olabilir.

TLS şifrelemesi ve X.509 arama tablolarına ek olarak, varsayılan PRF ve karma yordamları NX_SECURE_TLS_CRYPTO yapısıyla doldurularak bir TLS oturumu başlatmak için kullanılabilir.

20. "Sözde rastgele", PRF'nin belirlenimci olduğunu, yani her zaman aynı girişe göre aynı çıkışı üretecek ancak çıkışın tahmin edilebilir olmadığının rastgele olduğunu ifade eder. TLS, RSA gibi ortak anahtar şifrelemesi kullanılarak el sıkışma sırasında alışveriş yapılan ana gizli anahtarla birleştirilmiş çeşitli genel verilerden oturum anahtarlarını oluşturmak için PRF'nin bu özelliğini kullanır.

### <a name="cryptographic-metadata"></a>Şifreleme Meta Verileri

NX_SECURE_TLS_CRYPTO tablosuyla TLS oturumunu başlatamadan önce şifreleme yordamı meta verileri için arabellek alanı ayırmamız gerekir. Meta veriler, denetim bloğuyla temsil edilen belirli bir yordamla ilişkili tüm durumu depolamak için kullanılır. Her *nx_crypto_metadata_area_size* alanı NX_CRYPTO_METHOD bu yordamla ilişkili denetim yapısının boyutuna ayar olmalıdır; yoksa TLS başlatması gereken alan için düzgün bir şekilde hesap başarısız olur ve bu da arabellek taşması sorunlarına neden olabilir.

TLS oturumu oluşturulmadan önce meta veri arabelleği ayrılarak. Arabelleğe otomatik olarak nx_secure_tls_session_create ve şifreleme yöntemi tablosunda sağlanan yordamların her biri için alan ayrılır. TLS oturumunda aynı anda yalnızca bir şifreleme etkin olduğu için desteklenen şifreleme sayısının gerekli meta veri alanını etkilemeyeceğini unutmayın. 5 şifreleme yordamının her biri için, şifreleme arama tablosunda bu kategoriye ait maksimum denetim bloğu boyutu kullanılarak alan ayrılmıştır.

Meta veri arabelleği boyutunun kolayca hesaplanması için hizmet *nx_secure_metadata_size_calculate* aynı hesaplamaları nx_secure_tls_session_create yalnızca bayt cinsinden toplam gerekli meta veri arabelleği boyutunu döndürür.

### <a name="initializing-the-tls-session"></a>TLS oturumunu başlatma

Veri NX_CRYPTO_METHOD NX_SECURE_TLS_CRYPTO ve meta veri alanı ayrılmış olduktan sonra, aşağıdaki gibi bir TLS oturumu başlatabilirsiniz (yukarıdaki örneklerden alınan değerler):

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
