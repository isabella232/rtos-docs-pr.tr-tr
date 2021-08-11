---
title: Bölüm 1-HTTP ve HTTPS 'ye giriş
description: Bu bölüm, Web için Azure RTOS NetX Duo HTTP/HTTPS modülünü tanıtır.
author: philmea
ms.author: philmea
ms.date: 07/24/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e5f50419be3171d3df8544d1b34d603822f339785923f8a8199dc5b5ddcac281
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801775"
---
# <a name="chapter-1---introduction-to-http-and-https"></a>Bölüm 1-HTTP ve HTTPS 'ye giriş

Köprü Metni Aktarım Protokolü (HTTP), Web üzerinde içerik aktarmak için tasarlanan bir protokoldür. HTTP, içerik aktarım işlevini gerçekleştirmek için güvenilir Iletim Denetimi Protokolü (TCP) hizmetlerinden yararlanan basit bir protokoldür. Bu nedenle, HTTP son derece güvenilir bir içerik aktarım protokolüdür. HTTP, en çok kullanılan uygulama protokollerinden biridir. Web 'deki tüm işlemler HTTP protokolünü kullanır.

HTTPS, temel TCP bağlantısının güvenliğini sağlamak için Aktarım Katmanı Güvenliği (TLS) kullanarak HTTP 'yi uygulayan, HTTP protokolünün Güvenli sürümüdür. TLS ayarlamak için gereken ek yapılandırma dışında, HTTPS temelde kullanımda olan HTTP ile aynıdır.

## <a name="general-http-requirements"></a>Genel HTTP gereksinimleri

NetX Web HTTP paketi düzgün çalışması için NetX Duo (sürüm 5,10 veya üzeri) yüklü olmasını gerektirir. Ayrıca, bir IP örneğinin oluşturulması ve TCP 'nin aynı IP örneğinde etkinleştirilmesi gerekir. HTTPS desteği için, NetX güvenli TLS (sürüm 5,11 veya üzeri) de yüklü olmalıdır (sonraki bölüme bakın). Bölüm **2** ' de "küçük örnek sistem" bölümündeki tanıtım dosyası bunun nasıl yapıldığını gösterir.

NetX Web HTTP paketinin HTTP Istemci bölümünün başka gereksinimi yoktur.

NetX Web HTTP paketinin HTTP Sunucusu bölümünde birkaç ek gereksinim vardır. İlk olarak, tüm Istemci HTTP isteklerini işlemek için TCP *iyi bilinen bağlantı noktası 80* ' e tam erişim gerektirir (Bu, uygulama tarafından herhangi BIR geçerli TCP bağlantı noktasına değiştirilebilir). HTTP sunucusu Ayrıca, FileX Embedded dosya sistemiyle kullanılmak üzere tasarlanmıştır. FileX yoksa, Kullanıcı kendi ortamlarında kullanılan FileX bölümlerinin bağlantı noktasını alabilir. Bu, bu kılavuzun sonraki bölümlerinde ele alınmıştır.

## <a name="https-requirements"></a>HTTPS gereksinimleri

HTTPS 'nin düzgün çalışması için, NetX Web HTTP paketi NetX Duo (sürüm 5,10 veya üzeri) ve NetX güvenli TLS (sürüm 5,11 veya üzeri) yüklü olmasını gerektirir. Ayrıca, bir IP örneğinin oluşturulması ve TCP 'nin aynı IP örneğinde TLS ile kullanılması için etkin olması gerekir. TLS el sıkışması sırasında uzak sunucu konakları tarafından sağlanacak sertifikalar için uygun şifreleme yordamlarına, güvenilen bir CA sertifikasına ve alana sahip olmak üzere TLS oturumunun başlatılması gerekir. Bölüm **2** ' de "küçük örnek https sistemi" bölümündeki demo dosyası bunun nasıl yapıldığını gösterir.

NetX Web HTTP paketinin HTTPS Istemci bölümünün başka gereksinimi yoktur.

NetX Web HTTP paketinin HTTPS sunucu bölümü bazı ek gereksinimlere sahiptir. İlk olarak, tüm Istemci HTTPS isteklerini (düz metin HTTP ile olduğu gibi) işlemek için, TCP 'nin *iyi bilinen bağlantı noktası 443* ' e tam erişim gerektirir (Bu bağlantı noktası uygulama tarafından değiştirilebilir). İkincisi, TLS oturumunun doğru şifreleme yordamları ve sunucu kimlik sertifikası (veya önceden paylaşılan anahtar) ile başlatılması gerekir. HTTPS sunucusu Ayrıca, FileX Embedded dosya sistemiyle kullanılmak üzere tasarlanmıştır. FileX yoksa, Kullanıcı kendi ortamlarında kullanılan FileX bölümlerinin bağlantı noktasını alabilir. FileX kullanımı, bu kılavuzun sonraki bölümlerinde anlatılmaktadır.

TLS için yapılandırma seçenekleri hakkında daha fazla bilgi için NetX güvenli belgeleri bölümüne bakın.

Aksi belirtilmedikçe, bu belgede açıklanan tüm HTTP işlevleri de HTTPS için geçerlidir.

## <a name="http-and-https-constraints"></a>HTTP ve HTTPS kısıtlamaları

NetX Web HTTP, HTTP 1,1 standardını uygular. Bununla birlikte, aşağıdaki kısıtlamalar aşağıda verilmiştir:

1. İstek ardışık düzen oluşturma desteklenmiyor
1. HTTP sunucusu hem temel hem de MD5 Özet kimlik doğrulamasını destekler, ancak MD5-sess içermez. Mevcut olduğunda, HTTP Istemcisi yalnızca temel kimlik doğrulamasını destekler. HTTPS için TLS kullanıldığında, HTTP kimlik doğrulaması yine de kullanılıyor olabilir.
1. İçerik sıkıştırması desteklenmez.
1. Izleme, Seçenekler ve bağlantı istekleri desteklenmez.
1. HTTP sunucusu veya Istemcisiyle ilişkili paket havuzu, HTTP üst bilgisinin tamamını tutabilecek kadar büyük olmalıdır.
1. HTTP Istemci Hizmetleri yalnızca içerik aktarımına yöneliktir; Bu pakette sunulan bir görüntüleme yardımcı programı yoktur.

## <a name="http-url-resource-names"></a>HTTP URL 'SI (kaynak adları)

HTTP protokolü, Web 'de içerik aktarmak için tasarlanmıştır. İstenen içerik Evrensel Kaynak Bulucu (URL) tarafından belirtilir. Bu, her HTTP isteğinin birincil bileşenidir. URL 'Ler her zaman bir "/" karakteriyle başlar ve genellikle HTTP sunucusundaki dosyalara karşılık gelir. Ortak HTTP dosya uzantıları aşağıda gösterilmiştir:

- **.htm** (veya **.html**) köprü metni biçimlendirme dili (HTML)
- **.txt** Düz ASCII metni
- **.gif** İkili GIF resmi
- **. XBM** İkili Xbit eşlem resmi

## <a name="http-client-requests"></a>HTTP Istemci Istekleri

HTTP, Web içeriği istemek için basit bir mekanizmaya sahiptir. TCP *iyi bilinen bağlantı noktası 80 (https için bağlantı noktası 443)* üzerinde bir bağlantı başarıyla kurulduktan sonra istemci tarafından VERILEN standart http komutları kümesi vardır. Aşağıdakiler, temel HTTP komutlarının bazılarını göstermektedir:

- ***Kaynağı* al http/1.1** Belirtilen kaynağı al
- **Post *kaynağı* http/1.1** Belirtilen kaynağı al ve ekli girişi HTTP sunucusuna geçir
- **Baş *kaynak* http/1.1** HTTP sunucusu tarafından GET, ancak içerik değil olarak kabul edildi
- ***Kaynağı* koy http/1.1** Kaynağı HTTP sunucusuna yerleştir
- ***Kaynağı* Sil http/1.1** Sunucuda kaynağı Sil

Bu ASCII komutları, HTTP sunucusu ile HTTP işlemleri gerçekleştirmek için Web tarayıcıları ve NetX Web HTTP Istemci Hizmetleri tarafından dahili olarak oluşturulur.

HTTP Istemci uygulamasının 80 bağlantı noktasını veya HTTPS kullanılıyorsa bağlantı noktası 443 ' i kullanması gerektiğini unutmayın. Hem Istemci hem de sunucu HTTP API 'Leri bağlantı noktasını bir parametre olarak alır – makrolar NX_WEB_HTTP_SERVER_PORT (bağlantı noktası 80) ve NX_WEB_HTTPS_SERVER_PORT (bağlantı noktası 443) kolaylık sağlaması için tanımlanır. HTTP sunucusu bağlantı noktası, *nx_web_http_client_set_connect_port ()* hizmeti kullanılarak çalışma zamanında da değiştirilebilir. Bu hizmetle ilgili daha fazla ayrıntı için Bölüm 4 ' ü inceleyin.

## <a name="http-server-responses"></a>HTTP sunucusu yanıtları

HTTP sunucusu, Istemci komut yanıtlarını göndermek için aynı *iyi BILINEN TCP bağlantı noktası 80 ' i (https için 443)* kullanır. HTTP sunucusu Client komutunu işlediğinde, 3 basamaklı bir sayısal durum kodu içeren bir ASCII yanıt dizesi döndürür. Sayısal yanıt, HTTP Istemci yazılımı tarafından işlemin başarılı veya başarısız olup olmadığını tespit etmek için kullanılır. Istemci komutlarına yönelik çeşitli HTTP sunucu yanıtlarının listesi aşağıda verilmiştir:

- **200** isteği başarılı oldu
- **400** isteği düzgün biçimlendirilmemiş
- **401** yetkisiz istek, istemcinin kimlik doğrulaması gönderebilmesi gerekir
- **404** belirtilen kaynak bulunamadı
- **500** Iç http sunucusu hatası
- **501** Isteği http sunucusu tarafından uygulanmadı
- **502** hizmeti kullanılamıyor

Örneğin, "test.htm" dosyasını yERLEşTIRMEk için başarılı bir Istemci isteği "HTTP/1.1 200 Tamam" iletisiyle yanıt verdi.

## <a name="http-communication"></a>HTTP Iletişimi

Daha önce belirtildiği gibi, HTTP sunucusu, alan Istemci isteklerine yönelik *iyi BILINEN TCP bağlantı noktası 80 ' i (https için 443)* kullanır. HTTP Istemcileri, giden bağlantılar için kullanılabilir herhangi bir TCP bağlantı noktasını kullanabilir. HTTP olaylarının genel sırası aşağıdaki gibidir:

**Http get isteği**:

1. İstemci, sunucu bağlantı noktası 80 ' e TCP Connect (veya HTTPS için 443) yayınlar.
1. HTTPS kullanılıyorsa, TCP bağlantısının ardından sunucunun kimliğini doğrulamak ve güvenli bir kanal oluşturmak için bir TLS el sıkışması gelir.
1. İstemci "**Get *Resource* http/1.1**" isteği gönderir (diğer üst bilgi bilgileriyle birlikte).
1. Sunucu "**http/1.1 200 Tamam**" iletisini, daha sonra kaynak içeriği (varsa) tarafından hemen izlenir.
1. Sunucu istemcinin bağlantısını keser (HTTPS kullanılıyorsa TLS kapanır).
1. İstemci, soket bağlantısını keser (bağlantı kesme uyarısı sunucudan sonra TLS kapanır).

**Http put isteği**:

1. İstemci, 80 sunucu bağlantı noktasına (veya 443) TCP bağlantısı verir.
1. HTTPS kullanılıyorsa, TCP bağlantısının ardından sunucunun kimliğini doğrulamak ve güvenli bir kanal oluşturmak için bir TLS el sıkışması gelir.
1. İstemci "PUT Resource HTTP/1.1" isteği gönderir ve diğer üst bilgi bilgileriyle birlikte kaynak içeriği izler.
1. Sunucu, ek bilgiler içeren bir "HTTP/1.1 200 Tamam" iletisi oluşturur ve hemen ardından kaynak içeriği gelir.
1. Sunucu bir bağlantı kesmeyi gerçekleştiriyor.
1. İstemci bağlantıyı keser.

> [!NOTE]
> Daha önce belirtildiği gibi HTTP Sunucusu, istemcilere bağlanmak için alternatif bağlantı noktaları kullanan web sunucuları için *nx_web_http_client_set_connect_port()* kullanarak çalışma zamanında varsayılan bağlantı noktasını (80 veya 443) değiştirebilir.

## <a name="http-authentication"></a>HTTP Kimlik Doğrulaması

HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web istekleri için gerekli değildir. Kimlik doğrulamasının iki çeşidi vardır: temel *ve özet.*  Temel kimlik doğrulaması, birçok *protokolde bulunan* *ad ve* parola kimlik doğrulaması ile eşdeğerdir. HTTP temel kimlik doğrulamasında ad ve parolalar base64 biçiminde bir olur ve kodlanmış olur. Temel kimlik doğrulamasının temel dezavantajı, istekte açık bir şekilde iletilen ad ve paroladır. Bu, ad ve parolanın çalınmalarını biraz kolaylaştırır. Özet kimlik doğrulaması, istekte adı ve parolayı hiçbir zaman ileterek bu sorunu çözmektedir. Bunun yerine, ad, parola ve diğer bilgilerden 128 bit özet türetmek için bir algoritma kullanılır. NetX Web HTTP Sunucusu standart MD5 özet algoritmasını destekler.

Kimlik doğrulaması ne zaman gereklidir? HTTP Sunucusu, istenen bir kaynağın kimlik doğrulaması gerektir olup olduğuna karar verir. Kimlik doğrulaması gerekli ise ve İstemci isteği doğru kimlik doğrulamasını içermezse, gerekli kimlik doğrulaması türüne sahip bir "HTTP/1.1 401 Yetkisiz" yanıtı İstemciye gönderilir. İstemcinin daha sonra uygun kimlik doğrulamasıyla yeni bir istek oluşturması beklenir.

HTTPS kullanılırken, HTTPS Sunucusu YINE DE HTTP kimlik doğrulamasını kullanabilir. Bu durumda TLS tüm HTTP trafiğini şifrelemek için kullanılır, bu nedenle *temel* HTTP kimlik doğrulamasının kullanımı bir güvenlik riski oluşturmaz. *Özet* kimlik doğrulamasına da izin verilir, ancak TLS üzerinden temel kimlik doğrulaması üzerinde önemli bir güvenlik geliştirmesi yoktur.

## <a name="http-authentication-callback"></a>HTTP Kimlik Doğrulaması Geri Çağırma

Daha önce belirtildiği gibi HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web aktarımları için gerekli değildir. Ayrıca kimlik doğrulaması genellikle kaynağa bağımlıdır. Sunucu'da bazı kaynaklara erişim kimlik doğrulaması gerektirirken diğerleri kimlik doğrulaması gerektirmez. NetX Web HTTP Sunucusu paketi, uygulamanın her HTTP İstemcisi isteğini ***işlemenin*** başında çağrılır bir kimlik doğrulama geri çağırma yordamı (nx_web_http_server_create çağrısı aracılığıyla) belirtmesini sağlar.

Geri çağırma yordamı NetX Web HTTP Sunucusuna kaynakla ilişkili kullanıcı adı, parola ve alan dizelerini sağlar ve gerekli kimlik doğrulama türünü geri gönderir. Kaynak için kimlik doğrulaması gerekli yoksa, kimlik doğrulaması geri çağırma değeri olarak **NX_WEB_HTTP_DONT_AUTHENTICATE.** Aksi takdirde, belirtilen kaynak için temel kimlik doğrulaması gerekli ise, yordam **NX_WEB_HTTP_BASIC_AUTHENTICATE.** Son olarak, MD5 özet kimlik doğrulaması gerekli ise, geri çağırma yordamı **NX_WEB_HTTP_DIGEST_AUTHENTICATE.** HTTP Sunucusu tarafından sağlanan herhangi bir kaynak için kimlik doğrulaması gerekmiyorsa, geri çağırma gerekmez ve HTTP Sunucusu oluşturma çağrısına NULL işaretçisi sağlanmalıdır.

Uygulama kimlik doğrulaması geri çağırma yordamının biçimi çok basittir ve aşağıda tanımlanmıştır:

```C
UINT nx_web_http_server_authentication_check(NX_WEB_HTTP_SERVER *server_ptr,
    UINT request_type, CHAR *resource,
    CHAR **name, CHAR **password,
    CHAR **realm);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

- **request_type** HTTP İstemcisi isteğini belirtir, geçerli istekler şu şekilde tanımlanır:
  - **NX_WEB_HTTP_SERVER_GET_REQUEST**
  - **NX_WEB_HTTP_SERVER_POST_REQUEST**
  - **NX_WEB_HTTP_SERVER_HEAD_REQUEST**
  - **NX_WEB_HTTP_SERVER_PUT_REQUEST**
  - **NX_WEB_HTTP_SERVER_DELETE_REQUEST**
- **kaynak** Belirli bir kaynak isteği.
- **name** Gerekli kullanıcı adı işaretçisi için hedef.
- **parola** Gerekli parolanın işaretçisi için hedef.
- **alan** Bu kimlik doğrulaması için alelade işaretçinin hedefi.

Kimlik doğrulama yordamının dönüş değeri, kimlik doğrulamasının gerekli olup olduğunu belirtir. Kimlik doğrulama geri çağırma yordamı tarafından döndürülen ad, **parola ve NX_WEB_HTTP_DONT_AUTHENTICATE** işaretçileri kullanılamaz. Aksi takdirde HTTP sunucusu geliştiricisi,  nx_web_http_server **NX_WEB_HTTP_MAX_USERNAME.h'NX_WEB_HTTP_MAX_PASSWORD** tanımlanan NX_WEB_HTTP_MAX_PASSWORD kimlik doğrulaması geri *çağırmada* belirtilen kullanıcı adı ve parola için yeterince büyük olduğundan emin olmalı. Bunların her ikisi de varsayılan olarak 20 karakter uzunluğundadır.

## <a name="http-invalid-usernamepassword-callback"></a>HTTP Geçersiz Kullanıcı Adı/Parola Geri Çağırma

HTTP sunucusu bir İstemci isteğinde geçersiz bir kullanıcı adı ve parola birleşimi aldığında NetX Web HTTP Sunucusunda isteğe bağlı geçersiz kullanıcı adı/parola geri çağırma çağrılır. HTTP sunucusu uygulaması HTTP sunucusuna bir geri arama kaydettirilirse, temel veya özet kimlik doğrulaması nx_web_http_server_get_process() , *nx_web_http_server_put_process()* içinde veya *nx_web_http_server_delete_process()* içinde başarısız olursa *çağrılır.*

HTTP sunucusuna geri arama kaydetmek için NetX Web HTTP Sunucusu için aşağıdaki hizmet tanımlanır.

```C
UINT nx_web_http_server_invalid_userpassword_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*invalid_username_password_callback)
        (CHAR *resource, ULONG *client_nx_address,
        UINT request_type));
```

İstek türleri aşağıdaki gibi tanımlanır:

- **NX_WEB_HTTP_SERVER_GET_REQUEST**
- **NX_WEB_HTTP_SERVER_POST_REQUEST**
- **NX_WEB_HTTP_SERVER_HEAD_REQUEST**
- **NX_WEB_HTTP_SERVER_PUT_REQUEST**
- **NX_WEB_HTTP_SERVER_DELETE_REQUEST**

## <a name="http-insert-gmt-date-header-callback"></a>HTTP Insert GMT Date Header Callback

NetX Web HTTP Sunucusunda yanıt iletilerine tarih üst bilgisi eklemek için isteğe bağlı bir geri çağırma vardır. HTTP Sunucusu bir put veya get isteğine yanıt veriyorsa bu geri çağırma çağrılır

BIR GMT tarih geri aramasını HTTP Sunucusuna kaydetmek için aşağıdaki hizmet tanımlanır.

```C
UINT nx_web_http_server_gmt_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID (*gmt_get)(NX_WEB_HTTP_SERVER_DATE *date);
```

Veri NX_WEB_HTTP_SERVER_DATE türü aşağıdaki gibi tanımlanır:

```C
typedef struct NX_WEB_HTTP_SERVER_DATE_STRUCT
{
    USHORT nx_web_http_server_year; /* Year */
    UCHAR nx_web_http_server_month; /* Month */
    UCHAR nx_web_http_server_day; /* Day */
    UCHAR nx_web_http_server_hour; /* Hour */
    UCHAR nx_web_http_server_minute; /* Minute */
    UCHAR nx_web_http_server_second; /* Second */
    UCHAR nx_web_http_server_weekday; /* Weekday */
} NX_WEB_HTTP_SERVER_DATE;
```

## <a name="http-cache-info-get-callback"></a>HTTP Önbellek Bilgileri Geri Çağırma Alma

HTTP Sunucusunun belirli bir kaynak için HTTP uygulamasından en fazla yaş ve tarihi talep etmek için bir geri çağırması vardır. Bu bilgiler, HTTP sunucusunun bir İstemci Get isteğine yanıt olarak bir sayfanın tamamını gönderp gönderme olmadığını belirlemek için kullanılır. İstemci isteğinde "bu tarihten sonra değiştirildiyse" bulunamasa veya get önbelleği geri çağırma tarafından döndürülen "son değiştirme" tarihiyle eşlenemezse, sayfanın tamamı gönderilir.

Geri çağırmayı HTTP sunucusuna kaydetmek için aşağıdaki hizmet tanımlanır:

```C
UINT nx_web_http_server_cache_info_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT (*cache_info_get)
    (CHAR *, UINT *, NX_WEB_HTTP_SERVER_DATE *));
```

## <a name="http-chunked-transfer-coding-support"></a>HTTP Öbekli Aktarım Kodlama Desteği

Göndermeden önce HTTP iletinin toplam uzunluğu belirlenene zaman, Öbekli Aktarım Kodlaması özelliği iletileri "content-Length" üst bilgisi alanı olmadan öbek dizisi olarak göndermek için kullanılabilir. Bu özellik tüm HTTP isteği ve yanıt iletisinde de kullanılabilir. Alıcı olarak bu özellik de destekleniyor ve öbek üst bilgisi iç mantık tarafından şeffaf bir şekilde işlenir. Gönderici olarak API *nx_web_http_client_request_chunked_set* ve *nx_web_http_server_response_chunked_set* sırasıyla istemci ve sunucu tarafından çağrılmalı.

```C
UINT nx_web_http_client_request_chunked_set(NX_WEB_HTTP_CLIENT *client_ptr,
    UINT chunk_size,
    NX_PACKET *packet_ptr);

UINT nx_web_http_server_response_chunked_set(NX_WEB_HTTP_SERVER *server_ptr,
    UINT chunk_size,
    NX_PACKET *packet_ptr);
```

Bu hizmetler hakkında daha fazla ayrıntı için 3. Bölüm "HTTP Hizmetlerinin Açıklaması" bölümünde bu hizmetlerin açıklamalarına bakın.

## <a name="http-multipart-support"></a>HTTP Çok Parçalı Desteği

Çok Amaçlı İnternet Posta Uzantıları (MIME) başlangıçta SMTP protokolü için tasarlanmıştır, ancak kullanımı HTTP'ye yayılmıştır. MIME, iletilerin aynı ileti içinde karışık ileti türleri (görüntü/jpg ve metin/düz gibi) içermesini sağlar. NetX Web HTTP Sunucusu, İstemciden MIME içeren HTTP iletilerinden içerik türünü belirlemek için hizmetlere sahip. HTTP çok parçalı desteğini etkinleştirmek ve bu hizmetleri kullanmak için, NX_WEB_HTTP_MULTIPART_ENABLE **yapılandırma** seçeneği tanımlanmalıdır.

```C
UINT nx_web_http_server_get_entity_header(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    UCHAR *entity_header_buffer,
    ULONG buffer_size);

UINT nx_web_http_server_get_entity_content(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    ULONG *available_offset,
    ULONG *available_length);
```

Bu hizmetlerin kullanımı hakkında daha fazla ayrıntı için 3. Bölüm "HTTP Hizmetlerinin Açıklaması" bölümünde açıklamalarına bakın.

## <a name="http-multi-thread-support"></a>HTTP Çoklu İş Parçacığı Desteği

NetX Web HTTP İstemcisi hizmetleri aynı anda birden çok iş parçacığından çağrılabilirsiniz. Ancak, belirli bir HTTP İstemcisi örneğine yönelik okuma veya yazma istekleri aynı iş parçacığından sırasıyla yapılmalı.

HTTPS kullanıyorsanız, NetX Web HTTP İstemcisi hizmetleri birden çok iş parçacığından çağrılabiliyor olabilir, ancak temel TLS işlevinin ek karmaşıklığı nedeniyle her iş parçacığının tek, bağımsız bir HTTP İstemcisi örneği (NX_WEB_HTTP_CLIENT yapısı) olması gerekir.

## <a name="http-rfcs"></a>HTTP RFC'leri

NetX Web HTTP RFC1945 "Köprü Metni Aktarım Protokolü/1.0", RFC 2616 "Köprü Metni Aktarım Protokolü – HTTP/1.1", RFC 2581 "TCP Tıkanıklığı Denetimi", RFC 1122 "İnternet Konakları için Gereksinimler" ve ilgili RFC'ler ile uyumludur.

HTTPS için NetX Web HTTP, RFC 2818 "TLS üzerinden HTTP" ile uyumludur.
