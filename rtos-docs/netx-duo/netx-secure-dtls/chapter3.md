---
title: Bölüm 3-Azure RTOS NetX güvenli DTLS 'nin Işlevsel açıklaması
description: Bu bölümde, Azure RTOS NetX güvenli DTLS 'nin işlevsel bir açıklaması bulunmaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 347bd83fa8c72ced2e8678a92ec5c5f8393c136d
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550210"
---
# <a name="chapter-3-functional-description-of-azure-rtos-netx-secure-dtls"></a>Bölüm 3: Azure RTOS NetX güvenli DTLS 'nin Işlevsel açıklaması

## <a name="execution-overview"></a>Yürütmeye genel bakış

Bu bölümde, Azure RTOS NetX güvenli DTLS 'nin işlevsel bir açıklaması bulunmaktadır. NetX güvenli DTLS uygulamasında iki birincil program yürütme türü vardır: başlatma ve uygulama arabirimi çağrıları. 

NetX güvenli, ThreadX ve NetX/NetXDuo 'un varlığını varsayar. ThreadX ' ten, iş parçacığı yürütme, askıya alma, dönemsel zamanlayıcılar ve karşılıklı dışlama olanakları gerekir. NetX/NetXDuo 'dan UDP ve IP ağ tesislerini ve sürücülerini gerektirir.

## <a name="datagram-transport-layer-security-dtls-and-transport-layer-security-tls"></a>Veri birimi Aktarım Katmanı Güvenliği (DTLS) ve Aktarım Katmanı Güvenliği (TLS)

NetX güvenli DTLS, RFC 6347 ' de tanımlanan veri birimi Aktarım Katmanı Güvenlik Protokolü sürüm 1,2 ' ü uygular. DTLS sürüm 1,0, RFC 4347 ' de tanımlanmıştır ve TLS sürüm 1,1 ' ye karşılık gelen. DTLS 'lerin TLS 'ye uzantısı olması nedeniyle, sonraki sürümün karşılık gelen TLS sürümü ile aynı sürüm numarasını kullanması gerektiğine karar verdi. Bu nedenle, DTLS sürüm 1,2 ' nin TLS sürüm 1,2 ' ye karşılık geldiği için DTLS sürüm 1,1 yoktur.

> [!NOTE]
> NetX Secure, DTLS 1,2 sürümünü destekler. DTLS 1,0 (RFC 4347) şu **anda desteklenmiyor** .

*Güvenli Yuva Katmanı* (SSL), RFC 2246 ' de standart hale gelmeden önce TLS adının özgün adı ve "SSL" genellikle TLS protokolleri için genel bir ad olarak kullanılır. SSL 'nin son sürümü 3,0 idi ve TLS 1,0 bazen SSL sürüm 3,1 olarak adlandırılır. Resmi "SSL" protokolünün tüm sürümleri artık kullanılmıyor ve güvenli olmayan olarak kabul edilir ve şu anda NetX güvenli bir SSL uygulamasını sağlamıyor.

TLS, TLS istemcisi ile sunucu arasındaki TLS *el sıkışması* sırasında oluşturulan *oturum anahtarları* oluşturmak için bir protokol BELIRTIR ve bu anahtarlar TLS oturumu sırasında uygulama tarafından gönderilen verileri şifrelemek için kullanılır *.*

Temeldeki güvenlik mekanizması protokoller arasında paylaşıldığından DTLS, TLS ile yakından ilişkilidir. Ancak TLS, Paket teslimi ve siparişi (neredeyse her zaman TCP uygulaması) hakkında garanti sağlayan bir aktarım katmanı protokolü üzerinden çalışacak şekilde tasarlanmıştır ve UDP gibi güvenilir olmayan bir protokolde çalışmaz. Bu, DTLS 'in tanıtıldığı UDP 'nin bir tam nedeni olarak tasarlanmıştır: DTLS, güvenilir olmayan IP ve benzer protokollerin yapısını idare edin. Bu, TCP gibi güvenilir protokollere benzer sıralama ve güvenilirlik mantığını (örneğin, bırakılan verilerin yeniden iletilmesi) dahil ederek yapar.

Bu belge, TLS ve DTLS arasındaki farklılıklara odaklanarak, bu belgenin TLS ile güvenli TLS kullanım kılavuzunun 2. bölümünde bulunur.

### <a name="dtls-record-header"></a>DTLS kayıt üstbilgisi

Şekil 1 ' de gösterildiği gibi geçerli DTLS kayıtları bir DTLS üst bilgisine sahip olmalıdır. Üst bilgi, iki yeni alanın eklenmesiyle aynı TLS ile aynıdır: aşağıda açıklanan 16 bit *Dönem* ve 48 bitlik *sıra numarası*.

![DTLS kayıt üstbilgisinin diyagramı.](media/image2.png)

**Şekil 1-DTLS kayıt üstbilgisi**

TLS kayıt üstbilgisinin alanları aşağıdaki gibi tanımlanır:

| TLS üst bilgi alanı | Amaç  |
| ---------------- | --------- |
| **8 bit Ileti türü** | Bu alan, gönderilmekte olan DTLS kaydının türünü içerir. Geçerli türler şunlardır:<br />-Changecbir spec: 0x14<br />-Uyarı: 0x15<br />-Handshake: 0x16<br />-Uygulama verileri: 0x17<br /> |
| **16 bit protokol sürümü** | Bu alan DTLS protokol sürümünü içerir. Geçerli değerler aşağıdaki gibidir:<br />-DTLS 1,1:0xFEFD |
|  **16 bit dönem** |  Bu alan, şifreleme durumunun her değiştirildiği her seferinde arttırılan bir sayaç olan DTLS "dönemini" içerir (örneğin, yeni oturum anahtarları oluştururken).  |
|  **48-bit sıra numarası** |  Bu alan, bu özel kaydı tanımlayan bir sıra numarası içerir. Kayıt sıralamasını sürdürmek ve yeniden aktarım gereksinimini denetlemek için DTLS tarafından kullanılır. |
|  **16 bit uzunluğu** |  Bu alan, DTLS kaydında kapsüllenmiş verilerin uzunluğunu içerir.  |

### <a name="dtls-handshake-record-header"></a>DTLS el sıkışma kayıt üstbilgisi

Tüm geçerli DTLS el sıkışma kayıtları, Şekil 2 ' de gösterildiği gibi DTLS el sıkışma üstbilgisine sahip olmalıdır.

![DTLS el sıkışma kayıt üstbilgisinin diyagramı.](media/image3.png)

**Şekil 2-DTLS el sıkışma kayıt üstbilgisi**

DTLS el sıkışma kayıt üstbilgisinin alanları aşağıdaki gibi tanımlanır:

| TLS üst bilgi alanı | Amaç  |
| ---------------- | ------------------------------------------------ |
| **8 bit Ileti türü** | Bu alan, gönderilmekte olan DTLS kaydının türünü içerir. Geçerli türler şunlardır:<br />-Changecbir spec: 0x14<br />-Uyarı: 0x15<br />-Handshake: 0x16<br />-Uygulama verileri: 0x17 |
|  **16 bit dönem** | Bu alan, şifreleme durumunun her değiştirildiği her seferinde arttırılan bir sayaç olan DTLS "dönemini" içerir (örneğin, yeni oturum anahtarları oluştururken). |
|  **48-bit sıra numarası** | Bu alan, bu özel kaydı tanımlayan bir sıra numarası içerir. Kayıt sıralamasını sürdürmek ve yeniden aktarım gereksinimini denetlemek için DTLS tarafından kullanılır. |
|  **16 bit protokol sürümü** | Bu alan DTLS protokol sürümünü içerir. Geçerli değerler aşağıdaki gibidir:<br />-DTLS 1,1:0xFEFD |
| **16 bit uzunluğu** | Bu alan, DTLS kaydında kapsüllenmiş verilerin uzunluğunu içerir. |
| **8 bit el sıkışma türü** | Bu alan, el sıkışma ileti türünü içerir. Geçerli değerler aşağıdaki gibidir:<br />-Merhaba Istek: 0x00<br />-ClientHello: 0x01<br />-ServerHello: 0x02<br />-Sertifika: 0x0B<br />-ServerKeyExchange: 0x0C<br />-CertificateRequest: 0x0D<br />-ServerHelloDone: 0x0E<br />-CertificateVerify: 0x0F<br />-ClientKeyExchange: 0x10<br />-Tamamlandı: 0x14 |
| **24 bit uzunluğu** | Bu alan, el sıkışma ileti verilerinin uzunluğunu içerir. |
| **16 bit sıra numarası** | Bu alan bir sıra numarası içerir. |

### <a name="the-dtls-handshake-and-dtls-session"></a>DTLS el sıkışma ve DTLS oturumu

Şekil 3 ' te tipik bir DTLS el sıkışması gösterilmektedir. Genellikle önemli bir farka sahip olan tipik TLS el sıkışması ile neredeyse aynıdır: ClientHello iletisi ilk gönderildiğinde, sunucu yeni bir DTLS-özel iletisiyle yanıt verir, "tanımlama bilgisi" içeren bir *Helloverifyrequest* . DTLS Istemcisi, el sıkışma devam etmeden önce bu tanımlama bilgisini içeren ikinci bir ClientHello iletisiyle yanıt vermelidir. Bu mekanizma, UDP 'nin bağlantısız bir protokol olduğundan, belirli hizmet reddi (DoS) saldırılarını engellemek için DTLS 'e eklenmiştir (TCP 'nin aynı sorundan devam edebilmesi için adanmış bir bağlantı/bağlantı noktası olması gerekir).

Istemci DTLS sunucusuna bir *ClientHello* iletisi GÖNDERDIĞINDE DTLS el sıkışması başlar ve bunu BIR DTLS oturumu başlatmak zorunda olduğunu gösterir. İleti, istemci oturum için kullanmak istediğiniz şifreleme hakkında bilgiler içerir ve bu da oturum anahtarlarını daha sonra el ile oluşturmak için kullanılan bilgilerle birlikte. Oturum anahtarları üretilene kadar DTLS el sıkışmasının içindeki tüm iletiler şifrelenmez. Yukarıda belirtildiği gibi, DTLS sunucusu ClientHello yanıt olarak, istemciyi ikinci bir güncelleştirilmiş ClientHello ile yanıt vermeye zorlayarak bir HelloVerifyRequest gönderebilir.

İkinci ClientHello iletisini aldıktan sonra DTLS sunucusu tanımlama bilgisini doğrular ve doğru olursa, istemci tarafından sunulan şifreleme seçeneklerinden seçim gösteren bir ServerHello iletisi ile yanıt verir. ServerHello, sunucunun kimliğini istemciye kimliğini doğrulamak için dijital bir sertifika sağladığı bir sertifika iletisi (X. 509.440 doğrulaması kullanılırsa) tarafından izlenir. Son olarak, sunucu gönderilecek daha fazla ileti olmadığını göstermek için bir ServerHelloDone iletisi gönderir. Sunucu isteğe bağlı olarak Sunucushello 'yu izleyen diğer iletileri gönderebilir ve bazı durumlarda bir sertifika iletisi gönderemeyebilir (örneğin, önceden paylaşılan anahtarlar kullanıldığında), bu nedenle ServerHelloDone iletisi gerekir.

İstemci tüm sunucu iletilerini aldıktan sonra, oturum anahtarlarını oluşturmak için yeterli bilgiye sahip olur. TLS/DTLS bunu, sabit boyutlu *gizli anahtar* adı verilen ve şifreli olarak bilinen ve şifreleme etkinleştirildikten sonra gereken tüm anahtarları oluşturmak için bir çekirdek olarak kullanılan, paylaşılan bir bit olarak adlandırılan bir rastgele verileri oluşturarak yapar. Asıl ön gizlilik, Merhaba iletilerde belirtilen ortak anahtar algoritması (ör. RSA) kullanılarak şifrelenir (ortak anahtar algoritmaları hakkında bilgi için aşağıya bakın) ve sertifikasında sunucu tarafından sağlanmış ortak anahtar. Önceden paylaşılan anahtarlar (PSK) adlı isteğe bağlı bir TLS/DTLS özelliği, sertifika kullanmayan cipherpaketlerine izin verebilir, bunun yerine ana bilgisayarlar arasında paylaşılan bir gizli değer (genellikle fiziksel aktarım veya diğer güvenli yöntem aracılığıyla) kullanır. PSK etkin olduğunda, önceden paylaşılan gizli anahtar, ön yönetici gizli anahtarı oluşturmak için kullanılır. Aşağıdaki "kimlik doğrulama metotları" bölümünde önceden paylaşılan anahtarlar hakkında bölümüne bakın.

Olağan bir TLS/DTLS anlaşmasında, şifrelenmiş ön ana gizlilik parolası ClientKeyExchange iletisindeki sunucusuna gönderilir. Sunucu, ClientKeyExchange iletisini aldıktan sonra, özel anahtarını kullanarak ana ön parolanın şifresini çözer ve oturum anahtarlarını TLS/DTLS istemcisiyle paralel olarak oluşturmaya devam eder.

Oturum anahtarları oluşturulduktan sonra, diğer tüm iletiler, Merhaba iletilerde seçili olan özel anahtar algoritması (ör. AES) kullanılarak şifrelenir. Diğer tüm iletilerin şifrelendiğini belirtmek için hem istemci hem de sunucu tarafından, Changeccrypspec adlı bir son şifreli ileti gönderilir.

Hem istemci hem de sunucu tarafından gönderilen ilk şifreli ileti ayrıca, tamamlandı olarak adlandırılan son TLS el sıkışma iletisidir. Bu ileti alınan ve gönderilen tüm el sıkışma iletilerinin karmasını içerir. Bu karma, el sıkışmasının hiçbir iletiden değiştirilmediğini veya bozulmadığını (güvenlik ihlali olasılığı olduğunu gösterir) doğrulamak için kullanılır.

Tamamlanan iletiler alındıktan ve el sıkışma karmaları doğrulandıktan sonra, TLS/DTLS oturumu başlar ve uygulama veri göndermeye ve almaya başlar. TLS/DTLS oturumu sırasında her iki taraf tarafından gönderilen tüm veriler öncelikle, oluşturulan oturum anahtarlarına sahip seçili özel anahtar algoritması kullanılarak, Merhaba iletilerde seçilen karma algoritma (ileti bütünlüğü sağlamak için) kullanılarak karma hale getirilir.

Son olarak, bir TLS/DTLS oturumu yalnızca Istemci veya sunucu bunu yapmayı seçerse başarılı bir şekilde sonlandırgirebilir. Kesilen oturum, bir güvenlik ihlali olarak değerlendirilir (bir saldırgan tüm verilerin alınmasını engellemeye çalışıyor olabilir), bu nedenle her iki taraf da oturumu sonlandırmak istediğinde, bir CloseNotify uyarısı olarak adlandırılan özel bir bildirim gönderilir. Başarılı bir oturum kapatması için hem istemci hem de sunucu bir CloseNotify uyarısı göndermelidir ve işlemelidir.

![Tipik bir DTLS el sıkışma oturumunun diyagramı.](media/image4.png)

**Şekil 3-tipik DTLS el sıkışma**

### <a name="initialization"></a>Başlatma

NETX ve NetXDuo yığınının NetX güvenli DTLS kullanılmadan önce başlatılması gerekir. UDP işlemi için TCP/IP yığınını doğru şekilde başlatma hakkında bilgi için NetX veya NetXDuo Kullanıcı kılavuzuna bakın.

NetX UDP başlatıldıktan sonra DTLS etkinleştirilebilir. Dahili olarak, tüm DTLS ağ trafiği ve işleme, kullanıcı müdahalesine gerek kalmadan NetX/NetXDuo Stack tarafından işlenir. Ancak, DTLS, temel ağ yığınından ayrı olarak işlenmesi gereken bazı özel gereksinimlere sahiptir. DTLS Istemci işlemi bu parametreler, ***NX_SECURE_DTLS_SESSION** _ ADLı DTLS denetim bloğuna atanır. DTLS sunucu işlemi için, denetim bloğu _ *_NX_SECURE_DTLS_SERVER_** olarak adlandırılır ve tek bir UDP bağlantı noktasında birden çok DTLS oturumunu işlemek için gereken altyapıyı içerir – bu, her bir TLS oturumunun tek bir TCP bağlantı noktasına bağlandığı TLS 'den farklı olduğunu unutmayın.

İki DTLS modu, sunucu ve Istemci, bir uygulamada etkinleştirilebilir (ancak NetX yuvası başına yalnızca bir mod) ve her birinin aşağıda ayrıntılı olarak belirli gereksinimleri vardır.

### <a name="initialization--dtls-server"></a>Başlatma – DTLS sunucusu

NetX güvenli DTLS sunucu modu, temeldeki ağ aktarım protokolü için UDP kullanılması nedeniyle TLS sunucu modundan farklıdır. TCP ile bağlantı noktası, TLS oturumu süresince tek bir uzak ana bilgisayara bağlanır. UDP, uzak ana bilgisayarla ilgili olarak bir durum kavramı yoktur, bu nedenle farklı konaklardaki DTLS isteklerinin hepsi aynı UDP arabiriminde alınır. Bu nedenle, DTLS 'in, TLS ve TCP gibi yuvaya güvenmek yerine oturum durumu koruması gerekir. Bu nedenle, DTLS sunucu denetim bloğu (NX_SECURE_DTLS_SERVER), uzak ana bilgisayar bilgilerinin (IP adresi ve bağlantı noktası) DTLS oturumlarına eşleşmesini sağlar. Bir DTLS sunucusuna atanan UDP yuvasında tüm gelen veriler, uzak ana bilgisayara bağlı olarak mevcut veya yeni bir DTLS oturumuna eşlenir. Bu nedenle, DTLS sunucusu oluşturma, TLS ve DTLS Istemcisinin gerek duyduğu birkaç ek parametre gerektirir.

DTLS sunucu denetim bloğu, TLS cipherpaketlerine ve şifre karalama alanı/meta veri arabelleğinin yanı sıra DTLS sunucuları, DTLS oturumlarını sürdürmek için bir arabellek ve gelen DTLS kayıtlarının şifresini çözmek için kullanılan bir paket yeniden birleştirme arabelleği gerektirir.

DTLS sunucuları, oturum arabelleklerine ek olarak, bağlanan TLS istemcisine TLS sunucusunu tanımlamak için kullanılan bir belge olan *dijital bir sertifika* ve genellikle RSA şifreleme algoritması için de karşılık gelen *özel anahtarı* gerektirir. International Telekomünikasyon Birliği X. 509.440 standart, TLS/DTLS tarafından kullanılan sertifika biçimini belirtir ve X. 509.952 dijital sertifikaları oluşturmak için çok sayıda yardımcı program vardır.

NetX güvenli DTLS için, X. 509.440 sertifikası ASN. 1 ' in Distinguished Encoding Rules (DER) biçimi kullanılarak ikili kodlanmış olmalıdır. DER, sertifikalar için Standart TLS-kablolu ikili biçimidir.

Belirtilen sertifikayla ilişkili özel anahtar DER-Encoded PKCS # 1 biçiminde olmalıdır. Özel anahtar yalnızca cihazda kullanılır ve hiçbir şekilde kablo üzerinden aktarılmaz. TLS/DTLS iletişimleri için güvenlik sağlayan özel anahtarları güvende tutun!

DTLS sunucu sertifikasını başlatmak için, uygulama DER ile kodlanmış X. 509.952 sertifikasını ve isteğe bağlı DER kodlu PKCS # 1 RSA özel anahtar verilerini, ***nx_secure_x509_certificate_intialize*** hizmetini kullanarak, **NX_SECURE_X509_CERT** yapısını TLS tarafından kullanılmak üzere uygun sertifika verileriyle dolduran bir arabelleğe işaretçi sağlamalıdır.

Sunucu sertifikası başlatıldıktan sonra, ***nx_secure_dtls_server_local_certificate_add*** HIZMETI kullanılarak TLS denetim bloğuna eklenmelidir.

Sunucunun sertifikası DTLS sunucu denetim bloğuna eklendikten sonra, sunucu güvenli DTLS iletişimleri için kullanılabilir (Yukarıdaki örneğe bakın).

### <a name="initialization--dtls-client"></a>Başlatma – DTLS Istemcisi

UDP yuvası üzerinden uzak ana bilgisayara yalnızca tek bir giden bağlantı olduğundan, NetX güvenli DTLS Istemci modu, DTLS sunucusuyla karşılaştırıldığında basit bir işlemdir.

Bir DTLS Istemcisini ayarlamak için, güvenilen sertifika yetkililerinden (CA 'lar) X. 509.952 kodlu dijital sertifikaların bir koleksiyonu olan *Güvenilen bir sertifika deposu* gerekir. Bu sertifikaların, DTLS protokolünün "güvenilir" olması ve DTLS sunucu varlıklarının NetX güvenli DTLS Istemci uygulamasına verdiği sertifikaların kimlik doğrulaması için temel olarak kabul edilir.

Güvenilen CA sertifikası, başka bir CA tarafından *otomatik olarak imzalanmış* veya imzalı olabilir, bu durumda sertifikaya BIR *ara CA* (ICA) denir. Tipik bir TLS/DTLS uygulamasında sunucu, sunucu sertifikasıyla birlikte ICA sertifikalarını sağlar, ancak başarılı kimlik doğrulaması için tek gereksinim, sunucu sertifikasından güvenilen sertifika deposundaki güvenilir bir CA sertifikasına geri doğru şekilde izlenebilir. Bu zincir bir *güven zinciri* veya *sertifika zinciri* olarak bilinir.

Güvenilen bir CA veya ICA sertifikası başlatmak için, uygulamanın, _ *NX_SECURE_X509_CERT** yapısını TLS tarafından kullanılmak üzere uygun sertifika verileriyle dolduran, ***nx_secure_x509_certificate_intialize** _ hizmetini kullanarak der kodlu X. 509.440 sertifikasını içeren bir arabellek işaretçisi sağlaması gerekir.

DTLS Istemcisinin Ayrıca gelen sunucu sertifikasının ayrılması için (önceden paylaşılan anahtar modunun kullanılmadığını varsayarak) ve paketlerin Şifresi çözülecek DTLS kayıtlarına paket montajı için alan bulunması gerekir. Bu arabellekler ***nx_secure_dtls_session_create*** hizmetine parametreler olarak geçirilir (daha fazla bilgi için bkz. API Başvurusu).

Başlatılmış olan güvenilen sertifikalar, ***nx_secure_dtls_session_trusted_certificate_add*** hizmeti kullanılarak oluşturulan DTLS oturum denetim bloğuna eklenir. Bir sertifika eklenemedi DTLS Istemci oturumunun, uzak sunucu konaklarının kimliğini doğrulamak için DTLS protokolünün bir yolu olacağı için başarısız olmasına neden olur.

Güvenilen sertifika deposu oluşturulduktan sonra, oturum güvenli bir TLS Istemci bağlantısı kurmak için kullanılabilir.

### <a name="application-interface-calls"></a>Uygulama arabirimi çağrıları

NetX güvenli DTLS uygulamaları, genellikle ThreadX RTOS altında çalışan uygulama iş parçacıklarında işlev çağrıları yapar. Özellikle temel ağ iletişim protokolleri (örn. UDP ve IP) için bazı başlatma, ***tx_application_define *** öğesinden çağrılabilir. Ağ iletişimlerini başlatma hakkında daha fazla bilgi için bkz. NetX/NetXDuo Kullanıcı Kılavuzu.

DTLS, işlemci yoğunluklu işlemler olan şifreleme yordamlarının yoğun bir şekilde kullanılmasını sağlar. Genellikle, bu işlemler çağıran iş parçacığı bağlamında gerçekleştirilir.

### <a name="dtls-session-start"></a>DTLS oturum başlangıcı

DTLS, çalışması için temeldeki bir aktarım katmanı ağı Protokolü gerektirir. Genellikle kullanılan protokol TCP 'dir. NetX güvenli TLS oturumu oluşturmak için, DTLS Istemcileri için **_nx_secure_dtls_client_session_start_** hizmetine bir **NX_UDP_SOCKET** oluşturulması ve geçirilmesi gerekir.

DTLS sunucuları farklı şekilde çalışır. Gelen DTLS Istemci istekleri için kullanılan UDP yuvası NX_SECURE_DTLS_SERVER denetim bloğunda bulunur ve yerel UDP bağlantı noktasını parametre olarak alan ***nx_secure_dtls_server_create** _ çağrısıyla başlatılır. Daha sonra hizmet _*_nx_secure_dtls_server_start_*_ , gelen istekleri işlemek için DTLS sunucusunu başlatmak üzere kullanılır. Tüm gelen istekler, _nx_secure_dtls_server_create *: biri bağlantılar ve diğeri alma bildirimleri için sunulan geri çağırma yordamlarında işlenir. Bir bağlantı bildirimi alındığında DTLS oturumunun başlamasını işleyecek uygulamanın (Connect Notification geri araması DTLS tarafından çağrılır), ***nx_secure_dtls_server_session_start** çağırarak uygulamaya kadar_ olur. Ayrıca, _ *_nx_secure_dtls_session_receive_* * çağırarak, alma bildirimi geri araması çağrıldığında (tamamlanmış bir DTLS el sıkışmasını izleyen) uygulamanın gelen verileri işlemesi gerekir. Bunun Ayrıntıları yukarıdaki örnekte ve yukarıda bahsedilen hizmetlerin her biri için API başvurusunda verilmiştir.

### <a name="dtls-packet-allocation"></a>DTLS paket ayırması

NetX güvenli DTLS, _*_nx_packet_allocate_*_ hizmetini çağırmak yerine NETX/NetXDuo TCP (***NX_PACKET** _) ile aynı paket yapısını kullanır; bu nedenle, DTLS üst bilgisi için alanın doğru ayrılabileceği şekilde _ *_nx_secure_dtls_packet_allocate_** hizmetinin çağrılması gerekir.

### <a name="dtls-session-send"></a>DTLS oturum gönderme

TLS oturumu başladıktan sonra, uygulama ***nx_secure_dtls_session_send*** hizmetini kullanarak veri gönderebilir. Gönderme hizmeti, gönderilen verileri, hedef IP adresini ve hedef UDP bağlantı noktasını içeren bir _ *_NX_PACKET_** veri yapısı alarak, ***nx_udp_socket_send** _ hizmetinde kullanılan ile aynıdır.

> [!IMPORTANT]
> Nx_secure_dtls_session_send kullanarak veri gönderirken, oturumu yeni bir adrese ve UDP bağlantı noktasına (yaygın değil) taşımak için bir mekanizma olmadıkça, DTLS oturumunu kurmak için kullanılan aynı IP adresi ve bağlantı noktasının kullanılması önemlidir.

DTLS üzerinden gönderilen tüm veriler NX güvenli DTLS yığını ve gönderilmeden önce yapılandırılan şifreleme yordamları tarafından şifrelenir.

### <a name="dtls-session-receive"></a>DTLS oturum alma

DTLS oturumu başlatıldıktan sonra uygulama, ***nx_secure_Dtls_session_receive** _ hizmetini kullanarak veri almaya başlayabilir. DTLS oturumunun gönderilmesi gibi, bu hizmet, gelen verilerin, paket yapısına döndürülmeden önce DTLS Stack tarafından çözülmesi ve doğrulanması dışında _ *_nx_udp_socket_receive_* * ile aynıdır.

### <a name="tls-session-close"></a>TLS oturumu kapatma

DTLS oturumu tamamlandıktan sonra, her iki DTLS istemcisi ve sunucusu, oturumu kapatmak için diğer tarafa bir CloseNotify uyarısı göndermelidir. Başarılı bir oturumun kapatılmasını sağlamak için her iki taraf da uyarıyı alıp işlemelidir.

Uzak ana bilgisayar bir CloseNotify uyarısı gönderirse, ***nx_secure_dtls_session_receive** _ hizmetine yapılan tüm çağrılar uyarıyı işler, karşılık gelen uyarıyı uzak ana bilgisayara geri gönderir ve _ *_NX_SECURE_TLS_SESSION_CLOSED_* * değerini döndürür. Oturum kapatıldıktan sonra, bu DTLS oturumunda veri gönderme veya alma girişimleri başarısız olur.

Uygulama TLS oturumunu kapatmayı istiyorsa, ***nx_secure_dtls_session_end** _ hizmeti çağrılmalıdır. Hizmet, CloseNotify uyarısını gönderir ve yanıt CloseNotify 'ı işler. Yanıt alınmıyorsa, DTLS oturumunun hatalı bir güvenlik ihlali olup olmadığını belirten bir _ *_NX_SECURE_TLS_SESSION_CLOSE_FAIL_** hata değeri döndürülür.

### <a name="tlsdtls-alerts"></a>TLS/DTLS uyarıları

TLS/DTLS, en yüksek güvenliği sağlamak üzere tasarlanmıştır, bu nedenle protokoldeki tüm hatalı davranışlar olası bir güvenlik ihlali olarak kabul edilir. Bu nedenle, ileti işleme veya şifreleme/şifre çözme işlemlerinin her türlü hatası, el sıkışma veya oturumu hemen sonlandıran önemli hatalar olarak değerlendirilir.

Yerel bir uygulamadaki hataların işlenmesi oldukça basittir, uzak Konağın durumu düzgün bir şekilde işlemek ve olası güvenlik ihlallerinin oluşmasını engellemek için bir hata oluştuğunu bilmesi gerekir. Bu nedenle, TLS/DTLS herhangi bir hata durumunda uzak ana bilgisayara bir *Uyarı* iletisi gönderir.

Uyarılar, diğer TLS/DTLS iletileriyle aynı şekilde işlenir ve bir saldırganın, belirtilen uyarı türünden bilgi toplamasını engellemek için oturum sırasında şifrelenir. El sıkışma sırasında gönderilen uyarılar, olası bir saldırgan tarafından elde edilen bilgi miktarını sınırlamak için kapsamda sınırlanır.

TLS/DTLS oturumunu kapatmak için kullanılan CloseNotify uyarısı, önemli olmayan tek uyarıdır. Bir uyarı olarak kabul edildiği ve uyarı iletisi olarak gönderildiği sürece bir CloseNotify, bir hata oluştuğunu belirtmeyen diğer uyarıların aksine.

### <a name="tlsdtls-session-renegotiation-and-resumption"></a>TLS/DTLS oturumu yeniden anlaşması ve sürdürme

TLS, mevcut bir TLS oturumu bağlamında yalnızca TLS oturum parametrelerinin yeniden anlaşması olan "yeniden anlaşma" kavramını destekler.

TLS oturum *sürdürme* , bazı benzerlikler olmasına rağmen oturum yeniden *anlaşması* ile karıştırılmamalıdır. Oturum yeniden *anlaşması* , mevcut bir TLS oturumunda yeni bir el sıkışma başlatmayı da içerir. oturum *sürdürme* , tam bir TLS el SıKıŞMASı yapmadan kapalı bir TLS oturumunun yeniden başlatılmasını içeren tamamen isteğe bağlı bir özelliktir.

NX güvenli DTLS, uzak ana bilgisayarlardan gelen yeniden anlaşma isteklerini işler. Oturum sürdürme **desteklemez.** Bu özelliklerin daha kapsamlı bir tartışması NetX güvenli TLS Kullanıcı kılavuzunun Bölüm 3 ' te bulunabilir.

### <a name="protocol-layering"></a>Protokol katmanlama

TLS Protokolü (ve dolayısıyla DTLS), Aktarım Katmanı (örn. TCP veya UDP) ile uygulama katmanı arasındaki ağ yığınına uyar. TLS bazen bir Aktarım Katmanı Protokolü (Bu nedenle *Aktarım katmanı* güvenliği) olarak kabul edilir, ancak temel alınan ağ protokolleriyle ilgili bir uygulama olarak davrandığı için bazen uygulama katmanında gruplandırılır.

TLS, TCP gibi sıralı ve kayıpsız teslimi destekleyen bir aktarım katmanı protokolü gerektirir. Bu gereksinim nedeniyle, UDP veri birimlerinin teslimini garanti edemediğinden TLS UDP üzerinde çalıştırılamaz. *DTLS* , bir TLS sürümü olarak, UDP gibi bir veri birimi protokolü üzerinden TLS güvenliği gerektiren uygulamalar için kullanılır.

![TLS protokolü katmanlama diyagramı.](media/image6.png)

**Şekil 4-TCP/IP, UDP ve TLS/DTLS protokol katmanları**

## <a name="network-communications-security-and-encryption"></a>Ağ Iletişimi güvenliği ve şifreleme

Kamu ağları ve Internet üzerinden iletişimin güvenliğini sağlamak, çok sayıda kitap, makale ve çözüm konusunun önemli öneme sahip bir konudur. Bu konu göz önünde bulundurularak, ancak yalnızca hedeflenen hedefin bu bilgileri erişebileceği veya değiştirebilmesini sağlamak için bir ağ üzerinden bilgi gönderilirken daha kolay bir fikir olabilir. Bu üç önemli kavrama bölünür: Gizlilik, bütünlük ve kimlik doğrulama. TLS/DTLS Protokolü, her üç için çözüm sağlar.

Şifreleme, TLS ve DTLS protokolleri içinde gizlilik, bütünlük ve kimlik doğrulaması sağlamak için farklı yollarla kullanılır. TLS ya da bir oturum veya sunucu örneği oluşturulduktan sonra şifreleme, şifrelemeyi kullanmak için esnek bir çerçeve sağladığından şifrelemenin TLS 'e veya DTLS 'e sağlanması gerekir. NetX güvenli DTLS çoğu uygulama için gerekli şifreleme yordamlarını sağlar, böylece uygun şifrelemeyi bulma konusunda endişe etmeniz gerekmez.

Bu konuların daha ayrıntılı bir açıklaması NetX güvenli TLS Kullanıcı kılavuzunun Bölüm 3 ' te bulunabilir.

## <a name="tls-and-dtls-extensions"></a>TLS ve DTLS uzantıları

TLS (ve bu nedenle DTLS), belirli uygulamalar için ek işlevler sağlayan çeşitli uzantılar sağlar. Bu uzantılar tipik olarak, bir uzak ana bilgisayara bir uzantı kullanmayı veya güvenli TLS oturumu oluştururken kullanılmak üzere ek ayrıntılar sağlamayı belirten ClientHello veya ServerHello iletilerinin bir parçası olarak gönderilir.

NETX güvenli DTLS, NetX güvenli TLS 'de bulunan tüm uzantıları destekler ve NetX güvenli TLS kullanıcı kılavuzunda, Bölüm 3 ' te bulunabilir.

## <a name="authentication-methods"></a>Kimlik Doğrulaması Yöntemleri

TLS ve DTLS, güvenli olmayan bir ağ üzerinden iki cihaz arasında güvenli bir bağlantı kurmak için çerçeve sağlar, ancak sorunun bir parçası bu bağlantının diğer ucundaki cihazın kimliğini öğrenmektir. Uzak ana bilgisayarların kimliğini doğrulamak için bir mekanizma olmadan, saldırganın güvenilen bir cihaz olarak oluşturabileceği önemsiz bir işlem haline gelir.

Başlangıçta, IP adreslerini, donanım MAC adreslerini veya DNS 'yi kullanarak, bir ağdaki Konakları tanımlamak için görece yüksek düzeyde güven sağlayabilir, ancak TCP/IP teknolojisinin doğası ve adreslerin sızması ve DNS girdilerinin bozulmuş olması (örneğin, DNS önbelleği kirlenmesi aracılığıyla), TLS 'nin sahte kimliklere karşı ek bir koruma katmanı gerektirdiğinden emin olur.

Bu ek kimlik doğrulama katmanını TLS için sağlayabilecek çeşitli mekanizmalar vardır ancak en sık kullanılan *dijital sertifikadır.* Diğer mekanizmalarda önceden paylaşılan anahtarlar (PSK) ve parola şemaları bulunur.

### <a name="digital-cerificates"></a>Dijital sertifika

Dijital sertifikalar, TLS 'de uzak ana bilgisayarın kimliğini doğrulamak için en sık kullanılan yöntemdir. Esas olarak, dijital sertifika, bir bilgisayar ağındaki bir cihaz için kimlik bilgileri sağlayan belirli bir biçimlendirmeye sahip bir belgedir.

TLS, normalde Uluslararası Telekomünikasyon birleşimi tarafından geliştirilen standart olan X. 509.440 adlı bir biçim kullanır, ancak TLS ana bilgisayarları kullanılan biçimde kabul ediyorsanız başka sertifika biçimleri de kullanılabilir. X. 509.440, sertifikalar için belirli bir biçimi ve dijital bir belge oluşturmak için kullanılabilecek çeşitli kodlamaları tanımlar. TLS ile kullanılan en X. 509.440 sertifikaları, farklı bir telekomünikasyon standardı olan ASN. 1 ' in bir türevi kullanılarak kodlanır. ASN. 1 içinde çeşitli dijital kodlamalar vardır ancak TLS sertifikaları için en yaygın kodlama Distinguished Encoding Rules (DER) standardıdır. DER, ASN. 1 temel kodlama kuralları 'nın (BER), belirsiz olacak şekilde tasarlanan, ayrıştırmayı kolaylaştırmak için basitleştirilmiş bir alt kümesidir. Kablo üzerinden, TLS sertifikaları genellikle ikili DER olarak kodlanır ve bu, NetX Secure 'ın X. 509.440 sertifikalarını beklediği biçimdedir.

DER biçimli ikili sertifikalar gerçek TLS protokolünde kullanılıyor olsa da, bunlar. pek,. CRT ve. p12 gibi dosya uzantılarına sahip bir dizi farklı kodlarda oluşturulup depolanabilir. Farklı çeşitler farklı üreticilerin farklı uygulamaları tarafından kullanılır, ancak genel kullanıma sunulan araçlar kullanılarak tüm geliştiriciler DER 'a dönüştürülebilir.

Alternatif sertifika kodlamaları en yaygın olarak ped 'dir. PEK biçimi (Privacy-Enhanced mail 'den), kodlama, e-posta veya Web tabanlı protokoller kullanılarak kolayca gönderilebilecek yazdırılabilir metinle sonuçlandığından, genellikle kullanılan DER kodlamasının temel 64 kodlu bir sürümüdür.

NetX güvenli uygulamanız için bir sertifika oluşturmak, genel olarak bu el ile kapsam dışındadır, ancak OpenSSL komut satırı aracı ([www.OpenSSL.org](http://www.openssl.org)) yaygın olarak kullanılabilir ve çoğu biçim arasında dönüştürülebilir.

Uygulamanıza bağlı olarak, kendi sertifikalarınızı oluşturabilir, bir üretici veya devlet kurumuna sertifika verebilir veya ticari bir sertifika yetkilisinden sertifika satın alabilirsiniz.

NetX güvenli uygulamanızda dijital bir sertifika kullanmak için, önce sertifikanızı bir ikili DER biçimine dönüştürmeniz ve isteğe bağlı olarak ilişkili özel anahtarı (RSA için "Private üs") ikili biçime dönüştürmeniz gerekir, genellikle PKCS # 1 biçimli, DER kodlu bir RSA anahtarı. Dönüştürme işlemi tamamlandıktan sonra, sertifikayı ve özel anahtarı cihaza yüklemeniz gerekir. Olası seçenekler, Flash tabanlı bir dosya sistemi kullanmayı veya verilerden bir C dizisi oluşturmayı (Linux 'tan "XXD" gibi bir araç kullanarak) ve sertifikayı ve anahtarı sabit veri olarak uygulamanıza derlemeyi içerir.

Sertifikanız cihaza yüklendikten sonra DTLS API 'SI, sertifikanızı bir DTLS oturumu veya sunucusuyla ilişkilendirmek için kullanılabilir.

NetX güvenli DTLS ile X. 509.440 sertifikalarının nasıl kullanılacağına ilişkin ayrıntılar ve örnekler için, NetX güvenli TLS Kullanıcı Kılavuzunda "X. 509.440 sertifikalarını NetX güvenli olarak Içeri aktarma" bölümüne bakın.

Daha fazla bilgi için API başvurusunda aşağıdaki DTLS hizmetlerine başvurun:

- nx_secure_x509_certificate_initialize,
- nx_secure_dtls_session_local_certificate_add,
- nx_secure_dtls_server_local_certificate_add,
- nx_secure_dtls_session_local_certificate_remove,
- nx_secure_dtls_server_local_certificate_remove,
- nx_secure_dtls_session_trusted_certificate_add,
- nx_secure_dtls_server_trusted_certificate_add,
- nx_secure_dtls_session_trusted_certificate_remove
- nx_secure_dtls_server_trusted_certificate_remove

### <a name="tls-client-certificate-specifics"></a>TLS Istemci sertifikası özellikleri

DTLS Istemci uygulamaları genellikle cihaza yerel bir sertifika yüklenmesini gerektirmez. Yerel sertifika, yerel cihazı tanımlayan bir sertifikadır. Özellikle, yerel bir sertifika, TLS/DTLS uygulamasının yüklendiği cihaz için kimlik bilgileri sağlar. Bunun özel durumu, Istemci sertifikası kimlik doğrulamasının etkinleştirilme durumdur, ancak bu daha az yaygındır.

DTLS Istemcisi için en az bir Güvenilen sertifikanın yüklenmesi gerekir (gerekirse daha fazla yüklenebilir) ve uzak bir sertifikanın ayrılması için yer vardır. Güvenilen sertifika, uzak cihazın doğrudan veya bir ortak anahtar altyapısı (PKI) ile güven ve kimlik doğrulaması için temel sağlayan bir sertifikadır. Güven zincirinin köküne genellikle sertifika yetkilisi veya CA sertifikası denir. Uzak bir sertifika, TLS el sıkışması sırasında uzak ana bilgisayar tarafından gönderilen sertifikaya başvurur. Bu uzak ana bilgisayar için kimlik sağlar ve yerel cihazdaki güvenilen sertifikayla karşılaştırarak kimlik doğrulaması yapılır.

Güvenilen Sertifikalar ekleme ve uzak sertifikalara alan ayırma hakkında daha fazla bilgi için, şu hizmetler için TLS API başvurusuna bakın: nx_secure_dtls_session_create, nx_secure_dtls_session_trusted_certificate_add.

### <a name="tlsdtls-server-certificate-specifics"></a>TLS/DTLS sunucu sertifikası özellikleri

DTLS sunucu uygulamaları genellikle "güvenilen" sertifikaların ayrılacak cihaza veya uzak sertifikalara yüklenmesini gerektirmez. Istemci sertifikası kimlik doğrulaması etkinleştirildiğinde Bunun istisnası.

Bir TLS sunucusu bir "yerel" (veya "kimlik") sertifikasının yüklenmesini gerektirir, böylece sunucu istemciye kimlik doğrulaması yapmak için TLS el sıkışma sırasında bunu uzak istemciye sağlayabilir.

NetX TLS sunucu uygulamalarıyla kullanılmak üzere yerel sertifikaları yükleme hakkında daha fazla bilgi için, şu hizmetlere yönelik API başvurusuna bakın: nx_secure_dtls_server_local_certificate_add, nx_secure_dtls_server_local_certificate_remove.


### <a name="pre-shared-keys-psk"></a>Önceden paylaşılan anahtarlar (PSK)

TLS 'de kimlik doğrulaması sağlamaya yönelik alternatif bir mekanizma, önceden paylaşılan anahtarların (PSK) kavramsıdır. Bir PSK ciphersuite kullanılması, kaynak kısıtlı gömülü cihazlar için bir Boon, yoğun işlemci yoğunluklu ortak anahtar şifreleme işlemleri gereksinimini ortadan kaldırır. PSK, TLS/DTLS el sıkışmasındaki sertifikayı değiştirir ve TLS/DTLS oturum anahtarı oluşturma için şifrelenmiş ön ana gizli dizi yerine kullanılır.

PSK ciphersuites, bir TLS/DTLS oturumunun yapılabilmesi için her iki cihazda de paylaşılan bir gizliliğin olması gerektiğini anlamıştır. Bu, cihazların bir TLS PSK bağlantısı dışında bazı güvenli bir şekilde yüklenmiş olması gerektiği anlamına gelir. PSKs bir TLS PSK bağlantısı üzerinden güncelleştirilemeyebilir, ancak cihazın başka bir mekanizma aracılığıyla yüklenen bir PSK ile başlaması gerekir. Örneğin, bir algılayıcı aygıtı ve ağ geçidi cihazı, sevk etmeden önce fabrikada PSKs ile veya PSK 'yi yüklemek için standart bir TLS bağlantısı (bir sertifika ile) kullanılabilir.

PSK ciphersuites, RFC 4279 ' de açıklanan çeşitli biçimlerde gelir. İlki, Standart TLS el sıkışmaları içinde sertifikada aktarılan ortak anahtarlarla aynı şekilde kullanılan RSA veya Diffie-Hellman anahtarlarını kullanır. Kaynak kısıtlı bir ortamda daha fazla kullanılan ikinci form, oturum anahtarlarını doğrudan oluşturmak için kullanılan bir PSK kullanır (örneğin, AES tarafından kullanılmak üzere), pahalı RSA veya Diffie-Hellman işlemlerinin kullanılmasını önler.

NetX güvenli,, uygulamaların tüm ortak anahtar şifreleme kodunu ve bellek kullanımını kaldırmasını sağlayan PSK ciphersuites 'in ikinci biçimini destekler. PSK kendisi bir AES anahtarı değil, ancak gerçek anahtarların oluşturulduğu bir parola gibi kabul edilebilir. PSK değeri ile ilgili olarak daha uzun değerler daha fazla güvenlik (parolalarla aynı şekilde) sağlayabilse de daha fazla kısıtlama vardır.

NetX güvenli uygulamanızla PSK 'yi kullanmak için, önce genel makro **NX_SECURE_ENABLE_PSK_CIPHERSUITES** tanımlamanız gerekir. Bu genellikle derleyici ayarlarınız aracılığıyla yapılır, ancak tanım nx_secure_tls. h üst bilgi dosyasına da yerleştirilebilirler. Tanımlanan makro ile, PSK ciphersuite desteği NetX güvenli DTLS uygulamanıza derlenir.

PSK desteği etkinken, uygulamanız için PSKs 'i kurmak üzere DTLS API 'sini kullanabilirsiniz. Her PSK için bir PSK değeri (gerçek gizli anahtar "anahtarı" – Bu değeri güvenli tut), belirli bir PSK 'yi tanımlamak için kullanılan bir "Identity" değeri ve bir TLS sunucusu tarafından belirli bir PSK değeri seçmek için kullanılan bir "kimlik ipucu" gerekir.

PSK, bir ağ bağlantısı üzerinden hiçbir şekilde gönderilmediğinden herhangi bir ikili değer olabilir. PSK, 64 bayta kadar olan herhangi bir değer olabilir.

Kimliğin ve ipucunun UTF-8 kullanılarak biçimlendirilen yazdırılabilir karakter dizeleri olması gerekir. Kimlik ve ipucu değerleri 128 bayta kadar olan uzunlukta olabilir.

Identity ve PSK, ağdaki bir birbirleriyle iletişim kurması gereken her cihaza yüklenen benzersiz bir çift oluşturur.

"İpucu", birincil olarak, bir işlev veya hizmete göre PSKs 'leri gruplandırmak için belirli uygulama profillerinin tanımlanması için kullanılır. Bu değerler önceden anlaşılmalıdır ve uygulamaya bağımlı olur. Örnek olarak, OpenSSL komut satırı sunucu uygulaması (PSK etkin ile), TLS el sıkışması ile devam edebilmek için bir TLS istemcisi tarafından sağlanması gereken varsayılan "Client_identity" dizesini kullanır.

PSKs hakkında daha fazla bilgi için, aşağıdaki hizmetler için NetX Secure API başvurusuna bakın: nx_secure_dtls_psk_add, nx_secure_dtls_server_psk_add.

## <a name="importing-x509-certificates-into-netx-secure"></a>X. 509.440 sertifikalarını NetX ile alma güvenli

Internet üzerindeki çoğu TLS bağlantısı için dijital sertifikalar gerekir. Sertifikalar, genellikle *sertifika yetkilileri* veya CA olarak adlandırılan güvenilen Aracılar kullanılarak Internet üzerinden daha önce bilinmeyen Konakları kimlik doğrulaması için bir yöntem sağlar. NetX güvenli cihazınızı ticari bir bulut hizmetiyle (örneğin, Amazon Web Services) bağlamak için, bu sertifikaları cihazınıza yükleyerek uygulamanıza aktarmanız gerekir.

Sertifikalarla birlikte, bazen sertifikalarınızla ilişkili bir *özel anahtara* da ihtiyacınız olacaktır. Bazı uygulamalarda (Istemci sertifikası kimlik doğrulaması kullanılmazsa TLS Istemcisi gibi), sertifika tek başına yeterli olacaktır, ancak sertifikanız cihazınızı tanımlamak için kullanılıyorsa özel bir anahtara ihtiyacınız olur. Özel anahtarlar genellikle sertifikanızı oluşturduğunuzda oluşturulur ve genellikle bir parolayla şifrelenir ve ayrı bir dosyada depolanır.

Sertifikaları NetX güvenli uygulamalarına aktarma hakkında ayrıntılı bir açıklama için lütfen NetX güvenli TLS kullanıcı kılavuzunda Bölüm 3 ' e başvurun.

## <a name="client-certificate-authentication-in-netx-secure-tls"></a>NetX güvenli TLS 'de istemci sertifikası kimlik doğrulaması

X. 509.440 sertifika kimlik doğrulaması kullanılırken, TLS/DTLS Protokolü, DTLS sunucu örneğinin kimlik için bir sertifika sağlamasını gerektirir, ancak varsayılan olarak DTLS Istemci örneğinin kimlik doğrulama için bir sertifika sağlaması gerekmez (örn. bir Kullanıcı adı/parola birleşimi). Bu, Web siteleri için Internet 'te en yaygın TLS kullanımıyla eşleşir. Örneğin, bir çevrimiçi perakende sitesi, sunucunun meşru olduğunu bir Web tarayıcısı kullanarak potansiyel bir müşteriyi kanıtlamaları gerekir, ancak kullanıcı belirli bir hesaba erişmek için bir oturum açma/parola kullanacaktır.

Ancak, varsayılan durum her zaman tercih edilmez, bu nedenle TLS/DTLS isteğe bağlı olarak DTLS sunucu örneğinin uzak Istemciden bir sertifika istemesine izin verir. Bu özellik etkinleştirildiğinde, DTLS sunucusu el sıkışma sırasında DTLS Istemcisine bir CertificateRequest iletisi gönderir. Istemci kendi sertifikası ile yanıt vermelidir ve Istemcinin bu sertifikayla ilişkili eşleşen özel anahtara sahip olduğunu belirten bir şifreleme belirteci içeren bir CertificateVerify iletisi. Doğrulama başarısız olursa veya sertifika sunucuda güvenilir bir sertifikaya bağlı değilse, TLS el sıkışması başarısız olur.

TLS 'de Istemci sertifikası kimlik doğrulaması için iki ayrı durum vardır: aşağıdaki bölümlerde her iki durum da ele alınmaktadır.

### <a name="client-certificate-authentication-for-dtls-clients"></a>DTLS Istemcileri için istemci sertifikası kimlik doğrulaması

DTLS Istemcisi, istemci kimlik doğrulaması için bir sertifika isteyen bir sunucuya bağlantı deneyebilir. Bu durumda, Istemcinin sunucuya bir sertifika sağlaması ve eşleşen özel anahtara sahip olduğunu doğrulaması gerekir ya da sunucu DTLS el sıkışmasını sonlandırır.

NetX güvenli DTLS 'de, bu özelliği desteklemeye yönelik özel bir yapılandırma yoktur, ancak uygulamanın *nx_secure_tls_session_local_certificate_add* HIZMETINI kullanarak TLS istemci örneği için bir yerel kimlik sertifikası sağlaması gerekecektir. Uygulama tarafından bir sertifika sağlanmazsa ancak uzak sunucu Istemci sertifikası kimlik doğrulamasını kullanıyorsa ve bir sertifika isterse, DTLS el sıkışması başarısız olur. DTLS oturumu *nx_secure_dtls_session_local_certificate_add* Ile DTLS oturumuna sunulan sertifika, DTLS el sıkışma 'nı tamamlayabilmeniz için uzak sunucu tarafından tanınmalıdır.

### <a name="client-certificate-authentication-for-tls-servers"></a>TLS sunucuları için istemci sertifikası kimlik doğrulaması

Istemci sertifikası kimlik doğrulaması için DTLS sunucu durumu, özelliğin isteğe bağlı olması nedeniyle DTLS Istemci durumundan biraz daha karmaşıktır. Bu durumda, TLS sunucusunun özel olarak uzak TLS Istemcisinden bir sertifika istemesi, ardından uzak Istemcinin eşleşen özel anahtara sahip olduğunu doğrulamak için CertificateVerify iletisini işlemesi gerekir ve ardından sunucu, Istemci tarafından belirtilen sertifikanın, yerel güvenilen sertifika deposundaki bir sertifikaya izlenip izlenmeyeceğini denetmelidir.

NetX güvenli TLS sunucusu örneklerinde, Istemci sertifikası kimlik doğrulaması *nx_secure_dtls_server_x509_client_verify_configure* ve *nx_secure_dtls_server_x509_client_verify_disable* Hizmetleri tarafından denetlenir.

Istemci sertifikası kimlik doğrulamasını etkinleştirmek için bir uygulamanın, *nx_secure_dtls_server_start* çağrılmadan önce DTLS sunucusu oturum örneğiyle birlikte *nx_secure_dtls_server_x509_client_verify_configure* çağırması gerekir. Doğrulamanın, nx_secure_dtls_server_x509_client_verify_configure için bir parametre olarak belirtilen gelen istemci sertifikaları için ayrılan alan olması gerekir *.* Arabelleğin, *DTLS sunucu oturumlarının sayısı* tarafından verilen maksimum boyut sertifika zincirini tutabilecek kadar büyük olması gerektiğini unutmayın. Her sunucu oturumu için, tek bir belirtilen arabellekten ayrılacak alan gerekir. Arabelleğin yeterince büyük olduğundan emin olun veya belirtilen Istemci sertifikası zinciri çok büyükse bir hata meydana gelir.

Istemci sertifikası kimlik doğrulaması etkinleştirildiğinde, DTLS sunucusu, DTLS el sıkışması sırasında uzak DTLS Istemcisinden bir sertifika ister. NetX güvenli DTLS sunucusunda, Istemci sertifikası X. 509.952 Issuer zincirini izleyerek *nx_secure_dtls_server_trusted_certificate_add* oluşturulan güvenilir sertifikaların deposuna karşı denetlenir. Uzak Istemci, kimlik sertifikasını Güvenilen depodaki bir sertifikaya bağlayan bir zincir sağlamalıdır veya DTLS el sıkışması başarısız olur. Ayrıca, CertificateVerify iletisi işlemi başarısız olursa DTLS el sıkışması da başarısız olur.

CertificateVerify yöntemi için kullanılan imza yöntemleri TLS sürüm 1,0 ve TLS sürüm 1,1 için düzeltilir ve bu, ağ düzeyinde güvenli DTLS 'lerin temel aldığı TLS sürümü 1,2. DTLS 1,2 için, desteklenen imza yöntemleri genellikle şifreleme yöntemi tablosunda sağlanan ilgili yöntemleri izler, ancak genellikle SHA-256 ile RSA (şifreleme yöntemleriyle TLS başlatma hakkında daha fazla bilgi için bkz. "NetX güvenli TLS 'de şifreleme" bölümüne bakın).

## <a name="cryptography-in-netx-secure-tls"></a>NetX güvenli TLS 'de şifreleme

TLS, ağ iletişimlerini güvenli hale getirmek için şifreleme kullanılabilecek bir protokol tanımlar. Bu nedenle, TLS kullanıcıları için oldukça geniş kapsamlı açık kullanılacak şekilde gerçek şifrelemeyi bırakır. Belirtim yalnızca tek bir ciphersuite 'in uygulanması için gereklidir; TLS 1,2 olması durumunda bu ciphersuite TLS_RSA_WITH_AES_128_CBC_SHA, ortak anahtar işlemleri için RSA kullanımını ve oturum şifreleme için 128 bit anahtarlarla CBC modunda AES modunu ve ileti kimlik doğrulama karmaları için SHA-1 ' i belirtir.

TLS 1,2 uyumlu olduğu, NetX güvenliği, zorunlu TLS_RSA_WITH_AES_128_CBC_SHA ciphersuite 'i varsayılan olarak sağlar, ancak donanım özellikleri ve diğer hususlar nedeniyle her bir şifreleme yöntemi için olası uygulama sayısına veriliyorsa, NetX güvenliği, kullanıcının TLS ile hangi şifreleme yöntemlerinin kullanılacağını belirtmesini sağlayan bir genel şifreleme API 'SI sağlar.

> [!NOTE]
> Genel şifreleme API mekanizması, kullanıcıların kendi ciphersuites 'leri uygulamasına izin verir, ancak bu, TLS cipherpaketlerine ve uzantılarına alışkın olan ileri düzey kullanıcılar için önerilir. Kendi cipherpaketlerinizi desteklemeye ilgileniyorsanız lütfen hızlı mantık temsilcinizle iletişime geçin.

Lütfen DTLS için şifreleme yöntemlerinin nasıl yapılandırılacağı hakkında ayrıntılı bir tartışma için bkz. NetX güvenli TLS Kullanıcı Kılavuzu, Bölüm 3. Aynı işlem hem TLS hem de DTLS için geçerlidir.
