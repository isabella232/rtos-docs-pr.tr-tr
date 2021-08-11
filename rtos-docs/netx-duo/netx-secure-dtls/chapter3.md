---
title: Bölüm 3-Azure RTOS NetX güvenli DTLS 'nin Işlevsel açıklaması
description: Bu bölümde, Azure RTOS NetX güvenli DTLS 'nin işlevsel bir açıklaması bulunmaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7db319e45c6d1f4a2030734fc01fefc4f3907aebeec1b3f47a5bde57dd5bfcc4
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797100"
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

Istemci DTLS sunucusuna bir *ClientHello* iletisi GÖNDERDIĞINDE DTLS el sıkışması başlar ve bunu BIR DTLS oturumu başlatmak zorunda olduğunu gösterir. İleti, istemci oturum için kullanmak istediğiniz şifreleme hakkında bilgiler içerir ve bu da oturum anahtarlarını daha sonra el ile oluşturmak için kullanılan bilgilerle birlikte. Oturum anahtarları oluşturulana kadar DTLS el sıkışması içinde yer alan tüm iletiler şifrelenmez. Yukarıda belirtildiği gibi DTLS Sunucusu ClientHello'ya yanıt olarak bir HelloVerifyRequest gönderebilir ve istemciyi güncelleştirilmiş ikinci bir ClientHello ile yanıt vermeye zorlar.

İkinci ClientHello iletisi aldıktan sonra DTLS Sunucusu tanımlama bilgisini doğrular ve doğruysa istemci tarafından sağlanan şifreleme seçeneklerinden bir seçim olduğunu belirten bir ServerHello iletisiyle yanıt verir. ServerHello'nun ardından, sunucunun istemciye kimliğini doğrulamak için bir dijital sertifika sağladığı (X.509 doğrulaması kullanılırsa) bir Sertifika iletisi takip ediyor. Son olarak, sunucu bir ServerHelloDone iletisi gönderebilirsiniz. Sunucu isteğe bağlı olarak ServerHello'dan sonra başka iletiler gönderebilir ve bazı durumlarda bir Sertifika iletisi (örneğin, Önceden Paylaşılan Anahtarlar kullanılırken) göndermeyebilirsiniz, bu nedenle ServerHelloDone iletisine ihtiyaç vardır.

İstemci tüm sunucu iletilerini aldıktan sonra, oturum anahtarlarını oluşturmak için yeterli bilgiye sahip olur. TLS/DTLS bunu, sabit boyutlu olan ve şifreleme etkinleştirildikten sonra gereken tüm anahtarları oluşturmak için çekirdek olarak kullanılan Ana Gizli Anahtar Öncesi adlı paylaşılan bir rastgele veri biti oluşturarak yapar. Ana Anahtar Öncesi Gizli Anahtar, Hello iletisinde belirtilen ortak anahtar algoritması (örneğin RSA) kullanılarak şifrelenir (ortak anahtar algoritmaları hakkında bilgi için aşağıya bakın) ve sertifikada sunucu tarafından sağlanan ortak anahtar. Önceden Paylaşılan Anahtarlar (PSK) adlı isteğe bağlı bir TLS/DTLS özelliği, sertifika kullanmayan ancak bunun yerine konaklar arasında paylaşılan bir gizli anahtar değeri (genellikle fiziksel aktarım veya diğer güvenli yöntemler aracılığıyla) kullanan şifrelemeleri sağlar. PSK etkinleştirildiğinde, Ana Gizli Anahtar Öncesi oluşturmak için önceden paylaşılan gizli anahtar kullanılır. Aşağıdaki "Kimlik Doğrulama Yöntemleri" içinde Önceden Paylaşılan Anahtarlar bölümüne bakın.

Normal bir TLS/DTLS el sıkışması içinde, şifrelenmiş Ana Anahtar Öncesi Gizli Anahtar ClientKeyExchange iletisinde sunucuya gönderilir. Sunucu, ClientKeyExchange iletisi aldıktan sonra özel anahtarını kullanarak Ana Ana Gizli Anahtarın şifresini çözebilir ve TLS/DTLS istemcisiyle paralel olarak oturum anahtarları oluşturmak için devam eder.

Oturum anahtarları oluşturulurken, diğer tüm iletiler Hello iletisinde seçilen özel anahtar algoritması (örneğin AES) kullanılarak şifrelenir. ChangeCipherSpec adlı son bir şifresiz ileti hem istemci hem de sunucu tarafından göndererek diğer tüm iletilerin şifrelenir olduğunu gösterir.

Hem istemci hem de sunucu tarafından gönderilen ilk şifrelenmiş ileti de Son TLS el sıkışma iletisidir ve Bitti olarak adlandırılan son iletidir. Bu ileti, alınan ve gönderilen tüm el sıkışma iletilerinin karması içerir. Bu karma, el sıkışmada iletilerden hiçbirinin üzerinde oynanmadığını veya bozulmuş olmadığını doğrulamak için kullanılır (güvenlik ihlaline neden olabilir).

Bitti iletileri alındıktan ve el sıkışma karmaları doğrulandıktan sonra TLS/DTLS oturumu başlar ve uygulama veri göndererek almaya başlar. TLS/DTLS oturumu sırasında her iki taraf tarafından gönderilen tüm veriler ilk olarak Hello iletilerde seçilen karma algoritması kullanılarak karma (ileti bütünlüğü sağlamak için) ve oluşturulan oturum anahtarları ile seçilen özel anahtar algoritması kullanılarak şifrelenir.

Son olarak, TLS/DTLS oturumu yalnızca İstemci veya Sunucu bunu seçerse başarıyla sona erer. Kesilmiş bir oturum bir güvenlik ihlali olarak kabul edilir (bir saldırgan gönderilen tüm verilerin alınabilmesini engellemeye çalışsa da), bu nedenle her iki taraf da oturumu sona erdirerek CloseNotify uyarısı olarak adlandırılan özel bir bildirim gönderilir. Başarılı bir oturum kapatma işlemi için hem istemci hem de sunucu bir CloseNotify uyarısı göndermeli ve işlemeli.

![Tipik bir DTLS el sıkışma oturumunun diyagramı.](media/image4.png)

**Şekil 3- Tipik DTLS el sıkışması**

### <a name="initialization"></a>Başlatma

NetX Veya NetXDuo yığını, NetX Secure DTLS'nin kullanımından önce başlatılmış olması gerekir. UDP işlemi için TCP/IP yığınını düzgün bir şekilde başlatma hakkında bilgi için NetX veya NetXDuo Kullanıcı Kılavuzu'na bakın.

NetX UDP başlatıldıktan sonra DTLS etkinleştirilebilir. Dahili olarak, tüm DTLS ağ trafiği ve işlemesi, kullanıcı müdahalesi gerektirmeden NetX/NetXDuo yığını tarafından işlanır. Ancak, DTLS'nin temel ağ yığınından ayrı olarak ele alınmalıdır bazı özel gereksinimleri vardır. DTLS İstemcisi işlemi Bu parametreler * NX_SECURE_DTLS_SESSION _ adlı DTLS **denetim bloğuna** atanır. DTLS Sunucusu işlemi için denetim bloğu _ *_NX_SECURE_DTLS_SERVER_** olarak adlandırılır ve tek bir UDP bağlantı noktası üzerinde birden çok DTLS oturumunu işlemek için gereken altyapıyı içerir. Bunun her TLS oturumunun tek bir TCP bağlantı noktasına bağlı olduğu TLS'den farklı olduğunu unutmayın.

İki DTLS modu (Sunucu ve İstemci) bir uygulamada etkinleştirilebilir (netX yuvası başına yalnızca bir mod) ve her birinin aşağıda ayrıntılı olarak açıklanmıştır kendi özel gereksinimleri vardır.

### <a name="initialization--dtls-server"></a>Başlatma – DTLS Sunucusu

Temel ağ aktarım protokolü için UDP kullanımından dolayı NetX Güvenli DTLS Sunucusu modu TLS Sunucu modundan farklıdır. TCP ile, bağlantı noktası TLS oturumu süresince tek bir uzak ana bilgisayara bağlı olur. UDP'nin uzak ana bilgisayar ile ilgili durum diye bir durumu yoktur, bu nedenle farklı konaklardan gelen DTLS isteklerinin hepsi aynı UDP arabiriminde alınmıştır. Bu nedenle DTLS, TLS ve TCP ile olduğu gibi yuvaya güvenmek yerine oturum durumunu korumalı. Bu nedenle DTLS Sunucu denetim bloğu (NX_SECURE_DTLS_SERVER), uzak konak bilgileri (IP adresi ve bağlantı noktası) ile DTLS oturumlarının eşlemesini sürdürür. Bir DTLS Sunucusuna atanan UDP yuvasında gelen tüm veriler, uzak ana bilgisayarı temel alan mevcut veya yeni bir DTLS oturumuna eşlenmiş olur. Bu nedenle DTLS sunucusu oluşturma işlemi TLS ve DTLS İstemcisi'nin ihtiyaçlarının ötesinde birkaç ek parametre gerektirir.

DTLS Sunucu denetim bloğuna, TLS şifrelemelerine ve şifreleme karalama alanı/meta veri arabelleğine ek olarak, DTLS Sunucularının DTLS oturumlarını korumak için bir arabellek ve gelen DTLS kayıtlarının şifresini çözmek için kullanılan bir paket yeniden değerlendirme arabelleği gerekir.

DTLS Sunucuları, oturum arabelleklerinin yanı sıra, bağlanan TLS istemcisine TLS sunucusunu ve genellikle RSA şifreleme algoritması için karşılık gelen özel anahtarı tanımlamak için kullanılan bir belge olan Dijital Sertifika gerektirir. International Telecommunications Union X.509 standardı TLS/DTLS tarafından kullanılan sertifika biçimini belirtir ve X.509 dijital sertifikaları oluşturmak için birçok yardımcı program vardır.

NetX Secure DTLS için, X.509 sertifikası ASN.1'in Distinguished Encoding Rules (DER) biçimi kullanılarak ikili olarak kodlanmış olmalıdır. DER, sertifikalar için standart tlS over-the-wire ikili biçimidir.

Sağlanan sertifikayla ilişkilendirilmiş özel anahtar PKCS#1 DER-Encoded biçiminde olmalıdır. Özel anahtar yalnızca cihazda kullanılır ve hiçbir zaman kablo üzerinden aktarılamayacak. TLS/DTLS iletişimleri için güvenlik sağlarken özel anahtarları güvende tutma!

DTLS Sunucusu sertifikasını başlatmak için uygulamanın DER ile kodlanmış X.509 sertifikasını içeren bir arabelleğe ve ***nx_secure_x509_certificate_intialize*** hizmetini kullanarak isteğe bağlı DER ile kodlanmış PKCS#1 RSA özel anahtar verilerini içeren bir arabelleğe işaretçisi sağlaması gerekir. Bu, **NX_SECURE_X509_CERT** yapısını TLS tarafından kullanmak üzere uygun sertifika verileriyle doldurmak için kullanılır.

Sunucu sertifikası başlatıldıktan sonra, nx_secure_dtls_server_local_certificate_add hizmeti kullanılarak TLS denetim ***bloğuna eklenmiştir.***

Sunucunun sertifikası DTLS Sunucusu denetim bloğuna eklendiktan sonra, sunucu güvenli DTLS iletişimleri için kullanılabilir (yukarıdaki örneğine bakın).

### <a name="initialization--dtls-client"></a>Başlatma – DTLS İstemcisi

UDP yuvası üzerinden uzak ana bilgisayara yalnızca tek bir giden bağlantı olduğu için NetX Güvenli DTLS İstemci modu, DTLS sunucusuna kıyasla basittir.

Bir DTLS İstemcisi'nin kurulumu için güvenilen Sertifika Yetkililerinden (CA) X.509 ile kodlanmış dijital sertifika koleksiyonu olan Güvenilen Sertifika Deposu gerekir. Bu sertifikalar, DTLS protokolü tarafından "güvenilir" olduğu varsayılır ve DTLS sunucu varlıkları tarafından NetX Secure DTLS İstemci uygulamasına sağlanan sertifikaların kimlik doğrulamasını sağlamak için temel olarak kullanılır.

Güvenilen CA sertifikası, otomatik *olarak* imzalanan veya başka bir CA tarafından imzalanmış olabilir; bu durumda sertifika Ara *CA* (ICA) olarak çağrılır. Tipik bir TLS/DTLS uygulamasında sunucu, sunucu sertifikasıyla birlikte ICA sertifikalarını sağlar, ancak başarılı kimlik doğrulaması için tek gereksinim, sertifika verenler zincirinin (diğer sertifikaları imzalamak için kullanılan sertifikalar) sunucu sertifikasından Güvenilen Sertifika Deposu'na güvenilen bir CA sertifikasına geri izlenebilir olmasıdır. Bu zincir güven zinciri veya *sertifika zinciri* *olarak bilinir.*

Güvenilen bir CA veya ICA sertifikası başlatmak için, uygulama ***nx_secure_x509_certificate_intialize** _ hizmetini kullanarak DER kodlanmış X.509 sertifikasını içeren bir arabelleğe işaretçi sağlamış olmalı ve _ *NX_SECURE_X509_CERT** yapısını TLS tarafından kullanım için uygun sertifika verileriyle doldurmaktadır.

DTLS İstemcisi ayrıca gelen sunucu sertifikasının ayrılacağı (Önceden Paylaşılan Anahtar modunun kullanılmayacağı varsayılır) ve paketlerin DTLS kayıtlarına birleştirerek şifresinin çözülmesi için bir arabellek gerekir. Bu arabellekler, nx_secure_dtls_session_create ***hizmetine*** parametre olarak geçirildi (daha fazla bilgi için bkz. API başvurusu).

Başlatılan güvenilen sertifikalar daha sonra oluşturulan DTLS oturum denetim bloğuna, nx_secure_dtls_session_trusted_certificate_add ***eklenir.*** DTLS protokolünün uzak sunucu konakları için kimlik doğrulaması yapma yolu olmayacaktır. Sertifikanın eklenene kadar başarısız olması DTLS İstemcisi oturumunun başarısız olmasına neden olur.

Güvenilen Sertifika Deposu oluşturulduktan sonra, güvenli bir TLS İstemci bağlantısı kurmak için oturum kullanılabilir.

### <a name="application-interface-calls"></a>Uygulama Arabirimi Çağrıları

NetX Güvenli DTLS uygulamaları genellikle ThreadX RTOS altında çalışan uygulama iş parçacıklarının içinde işlev çağrıları yapacaktır. Özellikle temel ağ iletişim protokolleri (UDP ve IP gibi) için bazı başlatmalar * ağ iletişim **protokollerinden* tx_application_define* olabilir.** Ağ iletişimlerini başlatma hakkında daha fazla bilgi için bkz. NetX/NetXDuo Kullanıcı Kılavuzu.

DTLS, yoğun işlemci kullanan işlemler olan şifreleme yordamlarını yoğun olarak kullanır. Genellikle, bu işlemler çağıran iş parçacığı bağlamında gerçekleştirilir.

### <a name="dtls-session-start"></a>DTLS Oturum Başlatma

DTLS'nin çalışması için temel alınan bir aktarım katmanı ağ protokolü gerekir. Kullanılan protokol genellikle TCP'dir. NetX Secure TLS oturumu kurmak için bir **NX_UDP_SOCKET** DTLS İstemcileri için **_nx_secure_dtls_client_session_start_** hizmetine geçir gerekir.

DTLS Sunucuları farklı çalışır. Gelen DTLS İstemci istekleri için kullanılan UDP yuvası, NX_SECURE_DTLS_SERVER denetim bloğunda yer alır ve yerel UDP bağlantı noktasını parametre olarak alan ***nx_secure_dtls_server_create** _ çağrısında başlatılır. Bu _*_nx_secure_dtls_server_start_*_ gelen istekleri işlemek üzere DTLS Sunucusunu başlatmak için kullanılır. Tüm gelen istekler, biri bağlantılar ve biri de alma bildirimleri için olmak nx_secure_dtls_server_create* için sağlanan geri çağırma _yordamlarında ele alır. Bir bağlantı bildirimi_(bağlantı bildirimi geri çağırma DTLS tarafından çağrılır) * veya çağrısıyla DTLS oturumunun başlatılacak şekilde nx_secure_dtls_server_session_start. Ayrıca , _* çağrısıyla alma bildirimi geri çağırma çağrıldığında (tamamlanmış bir DTLS el sıkışmasını izleyen) gelen verileri de _işlemesi_ nx_secure_dtls_session_receive ** . Bunun ayrıntıları yukarıdaki örnekte ve yukarıda belirtilen hizmetlerin her biri için API başvurusunda sağlanmıştır.

### <a name="dtls-packet-allocation"></a>DTLS Paket Ayırma

NetX Secure DTLS, NetX/NetXDuo TCP (***NX_PACKET** _) ile aynı paket yapısını kullanır. Bunun _*_dışında, nx_packet_allocate_*_ hizmetinin çağrılması yerine _ *_nx_secure_dtls_packet_allocate_** hizmetinin çağrılması gerekir. Bu nedenle DTLS üst bilgisi için alan düzgün bir şekilde ayrılır.

### <a name="dtls-session-send"></a>DTLS Oturum Gönderme

TLS oturumu başlatıldıktan sonra uygulama, nx_secure_dtls_session_send hizmetini ***kullanarak veri*** gönderebilir. Gönderme hizmeti, gönderilen verileri içeren bir _ **NX_PACKET*** veri yapısını, bir hedef IP adresini ve hedef UDP bağlantı noktasını alarak **_nx_udp_socket_send_* _ hizmetiyle kullanımda aynıdır.

> [!IMPORTANT]
> nx_secure_dtls_session_send kullanarak veri gönderirken, oturumu yeni bir adrese ve udp bağlantı noktasına hareket sırasında taşımak için bir mekanizma yoksa DTLS oturumunu kurmak için kullanılan aynı IP adresini ve bağlantı noktasını kullanmak önemlidir (bu yaygın değildir).

DTLS üzerinden gönderilen tüm veriler, gönderilmeden önce NX Güvenli DTLS yığını ve yapılandırılmış şifreleme yordamları tarafından şifrelenir.

### <a name="dtls-session-receive"></a>DTLS Oturumu Alma

DTLS oturumu başlatıldıktan sonra uygulama , * nx_secure_Dtls_session_receive _ **hizmetini kullanarak veri almaya** başlayabilir. DTLS Oturumu gönderme işlemi gibi bu hizmet de _*_nx_udp_socket_receive_** ile aynıdır, ancak gelen verilerin şifresi çözülerek paket yapısında döndürülmeden önce DTLS yığını tarafından doğrulanır.

### <a name="tls-session-close"></a>TLS Oturumu Kapatma

DTLS oturumu tamamlandıktan sonra, hem DTLS istemcisinin hem de sunucusunun oturumu kapatmak için diğer tarafa bir CloseNotify uyarısı göndermesi gerekir. Oturumun başarıyla kapatılması için her iki taraf da uyarıyı almalı ve işlemeli.

Uzak konak bir CloseNotify uyarısı gönderirse, ***nx_secure_dtls_session_receive** _ hizmetine yapılan tüm çağrılar uyarıyı işler, ilgili uyarıyı uzak ana bilgisayara geri gönderir ve __*_ NX_SECURE_TLS_SESSION_CLOSED **. Oturum kapatılana kadar bu DTLS oturumuyla veri gönderme veya alma girişimleri başarısız olur.

Uygulama TLS oturumunu kapatmak isterse ***** nx_secure_dtls_session_end _ hizmetinin çağrılsı gerekir. Hizmet CloseNotify uyarıyı gönderir ve CloseNotify yanıtını işler. Yanıt alınmıyorsa, DTLS oturumunun hatalı bir güvenlik ihlali olup olmadığını belirten bir _ *_NX_SECURE_TLS_SESSION_CLOSE_FAIL_** hata değeri döndürülür.

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

NetX Secure, psk şifrelemelerinin ikinci formunu destekler ve uygulamaların tüm ortak anahtar şifreleme kodunu ve bellek kullanımını kaldırmasını sağlar. PSK'nin kendisi bir AES anahtarı değildir, ancak gerçek anahtarların oluşturularak oluşturulan bir parola gibi kabul edilir. PSK değerinin ne olduğuyla ilgili birkaç kısıtlama vardır, ancak daha uzun değerler daha fazla güvenlik sağlar (parolalarla aynı şekilde).

PSK'yi NetX Secure uygulamanıza kullanmak için öncelikle ile genel **makroyu** NX_SECURE_ENABLE_PSK_CIPHERSUITES. Bu genellikle derleyici ayarlarınız aracılığıyla yapılır, ancak tanım nx_secure_tls.h üst bilgi dosyasına da yer değiştirebilir. Makro tanımlandığı zaman PSK şifreleme desteği NetX Secure DTLS uygulamanıza derlenmiş olur.

PSK desteği etkinleştirildiğinde, uygulamanıza PSK'leri ayarlamak için DTLS API'sini kullanabilirsiniz. Her PSK için bir PSK değeri (gerçek gizli "anahtar" – bu değeri güvende tutma), belirli PSK'yi tanımlamak için kullanılan "kimlik" değeri ve belirli bir PSK değerini seçmek için TLS sunucusu tarafından kullanılan bir "kimlik ipucu" gerekir.

PSK'nin kendisi herhangi bir ikili değer olabilir çünkü hiçbir zaman bir ağ bağlantısı üzerinden gönderilmez. PSK, 64 bayt'a kadar herhangi bir değer olabilir.

Kimlik ve ipucu, UTF-8 kullanılarak biçimlendirilmiş yazdırılabilir karakter dizeleri olmalıdır. Kimlik ve ipucu değerleri en fazla 128 bayt uzunluğunda olabilir.

Kimlik ve PSK, ağ üzerinde birbirleriyle iletişim kurması gereken her cihaza yüklenen benzersiz bir çifttir.

"İpucu" öncelikli olarak işleve veya hizmete göre PSK'leri gruplayarak belirli uygulama profillerini tanımlamak için kullanılır. Bu değerler önceden kabul edilir ve uygulamaya bağımlıdır. Örneğin, OpenSSL komut satırı sunucu uygulaması (PSK etkinken) TLS el sıkışması ile devam etmek için bir TLS istemcisi tarafından sağlanmalıdır varsayılan "Client_identity" dizesini kullanır.

PSK'ler hakkında daha fazla bilgi için şu hizmetler için NetX Güvenli API başvurusuna bakın: nx_secure_dtls_psk_add, nx_secure_dtls_server_psk_add.

## <a name="importing-x509-certificates-into-netx-secure"></a>X.509 sertifikalarını NetX Secure'e aktarma

İnternet'e bağlı çoğu TLS bağlantısı için dijital sertifikalar gereklidir. Sertifikalar, genellikle Sertifika Yetkilileri veya CA'lar olarak adlandırılan güvenilir aracılar  aracılığıyla İnternet üzerinden önceden bilinmeyen konakların kimliklerini doğrulamaya yönelik bir yöntem sağlar. NetX Secure cihazınızı ticari bir bulut hizmetine (Amazon Web Services gibi) bağlamak için, sertifikaları cihazınıza yükerek uygulamanıza aktarmanız gerekir.

Sertifikalarla birlikte, bazen sertifikanız ile *ilişkili bir* özel anahtar da gerekir. Bazı uygulamalarda (İstemci Sertifikası Kimlik Doğrulaması kullanılmazken TLS İstemcisi gibi) yalnızca sertifika yeterli olacaktır, ancak sertifikanız cihazınızı tanımlamak için kullanılıyorsa özel bir anahtara ihtiyacınız olacaktır. Özel anahtarlar genellikle sertifikanızı 7.000.000'e kadar olan bir dosyada depolarsanız ve genellikle parolayla şifrelenirseniz oluşturulur.

Sertifikaları NetX Secure uygulamalarına aktarmanın ayrıntılı açıklaması için lütfen NetX Güvenli TLS Kullanıcı Kılavuzu'nın 3. Bölüm'e bakın.

## <a name="client-certificate-authentication-in-netx-secure-tls"></a>NetX Secure TLS'de İstemci Sertifikası Kimlik Doğrulaması

X.509 sertifika kimlik doğrulaması kullanılırken TLS/DTLS protokolü, DTLS Sunucusu örneğinin kimlik doğrulaması için bir sertifika sağlamasını gerektirir, ancak varsayılan olarak DTLS İstemci örneğinin kimlik doğrulaması için başka bir kimlik doğrulaması biçimi (kullanıcı adı/parola bileşimi gibi) sağlamak zorunda değildir. Bu, Web siteleri için internet üzerinde en yaygın TLS kullanımıyla eştir. Örneğin, bir çevrimiçi perakende satış sitesi, web tarayıcısı kullanan potansiyel bir müşteriye sunucunun meşru olduğunu kanıtlamalı, ancak kullanıcı belirli bir hesaba erişmek için bir oturum açma/parola kullanır.

Ancak, varsayılan durum her zaman tercih edilmez, bu nedenle TLS/DTLS isteğe bağlı olarak DTLS Sunucu örneğinin uzak İstemciden sertifika isteğine izin verir. Bu özellik etkinleştirildiğinde, DTLS Sunucusu el sıkışma sırasında DTLS İstemcisi'ne bir CertificateRequest iletisi gönderir. İstemci, kendi sertifikası ve İstemcinin bu sertifikayla ilişkilendirilmiş eşleşen özel anahtara sahip olduğunu kanıtlayan bir şifreleme belirteci içeren bir CertificateVerify iletisiyle yanıt ver ver versin. Doğrulama başarısız olursa veya sertifika Sunucu'da güvenilir bir sertifikaya bağlı olmazsa TLS el sıkışması başarısız olur.

TLS'de İstemci Sertifikası Kimlik Doğrulaması için iki ayrı durum vardır; aşağıdaki bölümlerde her iki durum da yer almaktadır.

### <a name="client-certificate-authentication-for-dtls-clients"></a>DTLS İstemcileri için İstemci Sertifikası Kimlik Doğrulaması

DTLS İstemcisi, istemci kimlik doğrulaması için sertifika talep etmek için sunucuyla bağlantı girişiminde olabilir. Bu durumda İstemcinin sunucuya bir sertifika sağlaması ve eşleşen özel anahtara sahip olduğunu doğrulaması gerekir, yoksa Sunucu DTLS el sıkışmasını sonlandırılır.

NetX Secure DTLS'de bu özelliği destekleyecek özel bir yapılandırma yoktur, ancak uygulamanın nx_secure_tls_session_local_certificate_add hizmetini kullanarak TLS İstemci örneği için yerel bir *kimlik sertifikası sağlaması* gerekir. Uygulama tarafından sertifika sağlanıyorsa ama uzak sunucu İstemci Sertifikası Kimlik Doğrulaması kullanıyorsa ve bir sertifika talep ediyorsa, DTLS el sıkışması başarısız olur. DTLS el sıkışmasını *tamamlamak için nx_secure_dtls_session_local_certificate_add* ile DTLS Oturumuna sağlanan sertifikanın uzak sunucu tarafından tanınması gerekir.

### <a name="client-certificate-authentication-for-tls-servers"></a>TLS Sunucuları için İstemci Sertifikası Kimlik Doğrulaması

İstemci Sertifikası Kimlik Doğrulaması için DTLS Sunucusu durumu, özelliğin isteğe bağlı olması nedeniyle DTLS İstemcisi örneğinden biraz daha karmaşıktır. Bu durumda, TLS Sunucusunun özellikle uzak TLS İstemcisi'den bir sertifika isteğinde olması, ardından uzak İstemcinin eşleşen özel anahtara sahip olduğunu doğrulamak için CertificateVerify iletiyi işlemesi gerekir ve ardından Sunucu, İstemci tarafından sağlanan sertifikanın yerel güvenilen sertifika depolama alanı içinde bir sertifikaya izlenebilir olup olamı gerektiğini denetlemesi gerekir.

NetX Güvenli TLS Sunucusu örneklerde İstemci Sertifikası Kimlik Doğrulaması, nx_secure_dtls_server_x509_client_verify_configure *ve* *nx_secure_dtls_server_x509_client_verify_disable* denetlenmektedir.

İstemci Sertifikası Kimlik Doğrulamasını etkinleştirmek için, bir *uygulamanın* nx_secure_dtls_server_x509_client_verify_configure çağırmadan önce DTLS Sunucusu oturum *örneğiyle* nx_secure_dtls_server_start. Doğrulama, gelen istemci sertifikaları için ayrılan alan gerektirir ve bu da sertifikayı *nx_secure_dtls_server_x509_client_verify_configure.* Arabelleğin, istemci tarafından sağlanan en büyük boyutlu sertifika zincirini *DTLS* sunucu oturumlarının sayısını kat kat tutacak kadar büyük olması gerektiğini unutmayın. Her sunucu oturumu için, sağlanan tek arabellekten ayrılan alan gerekir. Arabelleğin yeterince büyük olduğundan emin olun veya sağlanan İstemci sertifika zinciri çok büyükse bir hata oluşur.

İstemci Sertifikası Kimlik Doğrulaması etkinleştirildiğinde, DTLS Sunucusu DTLS el sıkışması sırasında uzak DTLS İstemcisi'den bir sertifika isteği gönderir. NetX Secure DTLS Server'da İstemci sertifikası, X.509 sertifikayı nx_secure_dtls_server_trusted_certificate_add ile oluşturulan güvenilen sertifika deposuna karşı denetlenir.  Uzak İstemcinin kimlik sertifikasını güvenilen depoda bir sertifikaya bağlayan bir zincir sağlaması gerekir, yoksa DTLS el sıkışması başarısız olur. Ayrıca CertificateVerify ileti işlemesi başarısız olursa DTLS el sıkışması da başarısız olur.

CertificateVerify yöntemi için kullanılan imza yöntemleri TLS sürüm 1.0 ve TLS sürüm 1.1 için sabittir ve NetX Secure DTLS'nin temel olduğu TLS sürüm 1.2'de TLS Sunucusu tarafından belirtilir. DTLS 1.2 için desteklenen imza yöntemleri genellikle şifreleme yöntemi tablosunda sağlanan ilgili yöntemleri kullanır, ancak genellikle SHA-256 ile RSA 'yı kullanır (şifreleme yöntemleriyle TLS'yi başlatma hakkında daha fazla bilgi için "NetX Secure TLS'de şifreleme" bölümüne bakın).

## <a name="cryptography-in-netx-secure-tls"></a>NetX Secure TLS'de şifreleme

TLS, şifrelemenin ağ iletişimlerini güvenli hale almak için kullanıla bir protokol tanımlar. Bu nedenle, kullanılacak gerçek şifrelemeyi TLS kullanıcıları için oldukça açık bırakır. Belirtim için yalnızca tek bir şifrelemenin uygulanması gerekir. TLS 1.2 olması durumunda bu şifreleme TLS_RSA_WITH_AES_128_CBC_SHA şeklindedir ve ortak anahtar işlemleri için RSA, oturum şifrelemesi için 128 bit anahtarlı CBC modunda AES ve ileti kimlik doğrulama karmaları için SHA-1 kullanılır.

TLS 1.2 ile uyumlu olan NetX Secure, varsayılan olarak zorunlu TLS_RSA_WITH_AES_128_CBC_SHA şifrelemesini sağlar ancak donanım özellikleri ve diğer önemli noktalar nedeniyle şifreleme yöntemlerinin her biri için olası uygulama sayısı göz önünde bulundurularak NetX Secure, kullanıcının TLS ile hangi şifreleme yöntemlerinin kullanılamayacaklarını belirtmesini sağlayan genel bir şifreleme API'si sağlar.

> [!NOTE]
> Genel şifreleme API'si mekanizması kullanıcıların kendi şifrelerini uygulamasına da olanak sağlar, ancak bu, TLS şifrelemeleri ve uzantıları hakkında bilgi sahibi olan ileri düzey kullanıcılar için önerilir. Kendi şifrelerinizi desteklemekle ilgileniyorsanız lütfen Express Logic temsilcinize başvurun.

DTLS şifreleme yöntemlerini yapılandırma hakkında ayrıntılı bilgi için lütfen NetX Güvenli TLS Kullanıcı Kılavuzu Bölüm 3'e bakın. Aynı işlem hem TLS hem de DTLS için geçerlidir.
