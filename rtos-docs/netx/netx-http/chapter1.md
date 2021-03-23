---
title: Bölüm 1-NetX HTTP 'ye giriş
description: Bu belge, HTTP 'nin Web 'de içerik aktarmak için tasarlanan bir protokol olduğunu açıklayacak.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6137cc0d8deb753d784be844d5abc7778dd62295
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826717"
---
# <a name="chapter-1---introduction-to-netx-http"></a>Bölüm 1-NetX HTTP 'ye giriş

Köprü Metni Aktarım Protokolü (HTTP), Web üzerinde içerik aktarmak için tasarlanan bir protokoldür. HTTP, içerik aktarım işlevini gerçekleştirmek için güvenilir Iletim Denetimi Protokolü (TCP) hizmetlerinden yararlanan basit bir protokoldür. Bu nedenle, HTTP son derece güvenilir bir içerik aktarım protokolüdür. HTTP, en çok kullanılan uygulama protokollerinden biridir. Web 'deki tüm işlemler HTTP protokolünü kullanır.

## <a name="http-requirements"></a>HTTP gereksinimleri

NetX HTTP paketi, düzgün çalışması için bir NetX (sürüm 5,2 veya üzeri) yüklü olmasını gerektirir. Buna ek olarak, bir IP örneği zaten oluşturulmalı ve TCP 'nin aynı IP örneğinde etkinleştirilmesi gerekir. Bölüm **2** ' de "küçük örnek sistem" bölümündeki tanıtım dosyası bunun nasıl yapıldığını gösterir.

NetX HTTP paketinin HTTP Istemci bölümünün başka gereksinimi yoktur.

NetX HTTP paketinin HTTP Sunucusu bölümünde birkaç ek gereksinim vardır. İlk olarak, tüm Istemci HTTP isteklerini işlemek için TCP 'nin *iyi bilinen bağlantı noktası 80* ' e tam erişim gerektirir. HTTP sunucusu Ayrıca, FileX Embedded dosya sistemiyle kullanılmak üzere tasarlanmıştır. FileX yoksa, Kullanıcı kendi ortamlarında kullanılan FileX bölümlerinin bağlantı noktasını alabilir. Bu, bu kılavuzun sonraki bölümlerinde ele alınmıştır.

## <a name="http-constraints"></a>HTTP kısıtlamaları 

NetX HTTP protokolü, HTTP 1,0 standardını uygular. Ancak, aşağıdaki kısıtlamalar vardır:

1.  Kalıcı bağlantılar desteklenmiyor

2.  İstek ardışık düzen oluşturma desteklenmiyor

3.  HTTP sunucusu hem temel hem de MD5 Özet kimlik doğrulamasını destekler, ancak MD5-sess içermez. Mevcut olduğunda, HTTP Istemcisi yalnızca temel kimlik doğrulamasını destekler.

4.  İçerik sıkıştırması desteklenmez.

5.  Izleme, Seçenekler ve bağlantı istekleri desteklenmez.

6.  HTTP sunucusu veya Istemcisiyle ilişkili paket havuzu, HTTP üst bilgisinin tamamını tutabilecek kadar büyük olmalıdır.

7.  HTTP Istemci Hizmetleri yalnızca içerik aktarımına yöneliktir; Bu pakette sunulan bir görüntüleme yardımcı programı yoktur.

## <a name="http-url-resource-names"></a>HTTP URL 'SI (kaynak adları)

HTTP protokolü, Web 'de içerik aktarmak için tasarlanmıştır. İstenen içerik Evrensel Kaynak Bulucu (URL) tarafından belirtilir. Bu, her HTTP isteğinin birincil bileşenidir. URL 'Ler her zaman bir "/" karakteriyle başlar ve genellikle HTTP sunucusundaki dosyalara karşılık gelir. Ortak HTTP dosya uzantıları aşağıda gösterilmiştir:

- **. htm (veya. html)** Köprü Metni Biçimlendirme Dili (HTML)
- **. txt** Düz ASCII metni
- **. gif** İkili GIF resmi
- **. XBM** İkili Xbit eşlem resmi

## <a name="http-client-requests"></a>HTTP Istemci Istekleri

HTTP, Web içeriği istemek için basit bir mekanizmaya sahiptir. Temel olarak *BILINEN TCP bağlantı noktası 80*' de bir bağlantı başarıyla kurulduktan sonra istemci tarafından VERILEN standart http komutları kümesi vardır. Aşağıdakiler, temel HTTP komutlarının bazılarını göstermektedir:

- Kaynağı al HTTP/1.0 *belirtilen kaynağı al*
- Kaynak SONRASı HTTP/1.0 *belirtilen kaynağı al ve ekli GIRIŞI http sunucusuna geçir*
- BAŞ kaynak HTTP/1.0 *, http sunucusu tarafından BIR Get, ancak içerik döndürülmüyor gibi değerlendirildi*
- Kaynak YERLEŞTIRME HTTP/1.0 *kaynak kaynağı http sunucusuna*
- Kaynağı SIL HTTP/1.0 *sunucuda kaynağı Sil*

Bu ASCII komutları, HTTP sunucusu ile HTTP işlemleri gerçekleştirmek için Web tarayıcıları ve NetX HTTP Istemci Hizmetleri tarafından dahili olarak oluşturulur.

>[!NOTE] 
> HTTP Istemci uygulaması varsayılan bağlantı noktası 80 ' dir. Ancak, *nx_http_client_set_connect_port* hizmetini kullanarak çalışma zamanında bağlantı bağlantı noktasını http sunucusu ile değiştirebilir. Bu hizmetin daha fazla ayrıntı için bkz. Bölüm 4. Bu, zaman zaman Istemci bağlantıları için alternatif bağlantı noktaları kullanan Web sunucularına uyum sağlar.

## <a name="http-server-responses"></a>HTTP sunucusu yanıtları

HTTP sunucusu, Istemci komut yanıtlarını göndermek için *TANıNMıŞ TCP bağlantı noktası 80* ' ü kullanır. HTTP sunucusu Client komutunu işlediğinde, 3 basamaklı bir sayısal durum kodu içeren bir ASCII yanıt dizesi döndürür. Sayısal yanıt, HTTP Istemci yazılımı tarafından işlemin başarılı veya başarısız olup olmadığını tespit etmek için kullanılır. Istemci komutlarına yönelik çeşitli HTTP sunucu yanıtlarının listesi aşağıda verilmiştir:

- 200 *isteği başarılı* oldu
- 400 *isteği düzgün biçimlendirilmemiş*
- 401 *yetkisiz istek, istemcinin kimlik doğrulaması gönderebilmesi gerekir*
- 404 *belirtilen kaynak bulunamadı*
- 500 *Iç http sunucusu hatası*
- 501 *ISTEğI http sunucusu tarafından uygulanmadı*
- 502 *hizmeti kullanılamıyor*

Örneğin, "test.htm" dosyasını yERLEşTIRMEk için başarılı bir Istemci isteği "HTTP/1.0 200 Tamam" iletisiyle yanıt verdi.

## <a name="http-communication"></a>HTTP Iletişimi

Daha önce belirtildiği gibi, HTTP sunucusu, Istemci isteklerini alan *iyi BILINEN TCP bağlantı noktası 80* ' ü kullanır. HTTP Istemcileri, kullanılabilir herhangi bir TCP bağlantı noktasını kullanabilir. HTTP olaylarının genel sırası aşağıdaki gibidir:

**Http get isteği**:

1.  İstemci, 80 numaralı sunucu bağlantı noktasına TCP Connect sorunları.

2.  İstemci "**Get Resource http/1.0**" isteği gönderir (diğer üst bilgi bilgileriyle birlikte).

3.  Sunucu "**http/1.0 200 Tamam**" iletisini, daha sonra kaynak içeriği (varsa) tarafından hemen izlenir.

4.  Sunucu bir bağlantı kesmeyi gerçekleştiriyor.

5.  İstemci bir bağlantı kesilmesi gerçekleştirir.

**Http put isteği**:

1. İstemci, 80 numaralı sunucu bağlantı noktasına TCP Connect sorunları.

2. İstemci "**PUT Resource http/1.0**" isteği ve diğer başlık bilgilerini ve ardından kaynak içeriğini gönderir.

3. Sunucu, daha sonra kaynak içeriği tarafından izlenen ek bilgiler içeren bir "**http/1.0 200 Tamam**" iletisi oluşturur.

4. Sunucu bir bağlantı kesmeyi gerçekleştiriyor.

5. İstemci bir bağlantı kesilmesi gerçekleştirir.

>[!NOTE] 
> Daha önce bahsedildiği gibi, HTTP Istemcisi varsayılan bağlantı bağlantı noktasını 80 ' dan başka bir bağlantı noktasına değiştirerek istemcilere bağlanmak için alternatif bağlantı noktaları kullanan Web sunucularının *nx_http_client_set_connect_port* .

## <a name="http-authentication"></a>HTTP kimlik doğrulaması

HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web istekleri için gerekli değildir. *Temel* ve *Özet* gibi iki kimlik doğrulama özelliği vardır. Temel kimlik doğrulaması, birçok protokolde bulunan *ad* ve *parola* kimlik doğrulamasına eşdeğerdir. HTTP temel kimlik doğrulamasında ad ve parolalar, Base64 biçiminde birleştirilir ve kodlanır. Temel kimlik doğrulamasının ana dezavantajı, bu ad ve parolanın istekte openly olarak aktarılmasıdır. Bu, ad ve parolanın çalınabilmesini kolaylaştırır. Özet kimlik doğrulaması, istekte hiçbir şekilde adı ve parolayı ileterek bu sorunu giderir. Bunun yerine, ad, parola ve diğer bilgilerden 128 bitlik bir anahtar veya Özet türetmek için bir algoritma kullanılır. NetX HTTP sunucusu standart MD5 Özet algoritmasını destekler.

Kimlik doğrulaması ne zaman gerekir? Temel olarak, HTTP sunucusu, istenen bir kaynağın kimlik doğrulaması gerektirip gerektirmediğini belirler. Kimlik doğrulaması gerekliyse ve Istemci isteği uygun kimlik doğrulamasını içermiyorsa, gerekli kimlik doğrulama türüne sahip "HTTP/1.0 401 Yetkisiz" yanıtı Istemciye gönderilir. Daha sonra Istemci, doğru kimlik doğrulamasıyla yeni bir istek oluşturacak şekilde beklenir.

## <a name="http-authentication-callback"></a>HTTP kimlik doğrulaması geri araması

Daha önce belirtildiği gibi, HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web aktarımları için gerekli değildir. Ayrıca, kimlik doğrulama genellikle kaynağa bağımlıdır. Sunucu üzerindeki bazı kaynaklara erişim için kimlik doğrulaması gerekir, diğerleri desteklemez. NetX HTTP sunucu paketi, uygulamanın, her HTTP Istemci isteğini işlemenin başlangıcında çağrılan bir kimlik doğrulama geri çağırma yordamı ( ***nx_http_server_create*** çağrısı aracılığıyla) belirtmesini sağlar.

Geri arama yordamı, NetX HTTP sunucusunu kaynakla ilişkili Kullanıcı adı, parola ve bölge dizeleri sağlar ve gereken kimlik doğrulaması türünü döndürür. Kaynak için kimlik doğrulaması gerekli değilse, kimlik doğrulama geri araması **NX_HTTP_DONT_AUTHENTICATE** değerini döndürmelidir. Aksi halde, belirtilen kaynak için temel kimlik doğrulaması gerekliyse, yordam **NX_HTTP_BASIC_AUTHENTICATE** döndürmelidir. Son olarak, MD5 Özet kimlik doğrulaması gerekliyse, geri arama yordamı **NX_HTTP_DIGEST_AUTHENTICATE** döndürmelidir. HTTP sunucusu tarafından sunulan herhangi bir kaynak için kimlik doğrulaması gerekmiyorsa, geri çağırma gerekmez ve HTTP sunucusu oluşturma çağrısına boş bir işaretçi sağlanması gerekir.

Uygulama kimlik doğrulaması geri arama yordamının biçimi çok basittir ve aşağıda tanımlanmıştır:

```c
UINT nx_http_server_authentication_check (NX_HTTP_SERVER *server_ptr,
                                         UINT request_type, CHAR *resource,
                                         CHAR **name, CHAR **password,
                                         CHAR **realm);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

- *request_type* HTTP Istemci isteğini belirtir, geçerli istekler şu şekilde tanımlanır:
  - **NX_HTTP_SERVER_GET_REQUEST**
  - **NX_HTTP_SERVER_POST_REQUEST**
  - **NX_HTTP_SERVER_HEAD_REQUEST**
  - **NX_HTTP_SERVER_PUT_REQUEST**
  - **NX_HTTP_SERVER_DELETE_REQUEST**
- *kaynak* Belirli bir kaynak istendi.
- *ad* Gerekli Kullanıcı adına işaretçinin hedefi.
- *parola* Gerekli parolaya yönelik işaretçinin hedefi.
- *bölge* Bu kimlik doğrulaması için bölge işaretçisinin hedefi.

Kimlik doğrulama yordamının dönüş değeri, kimlik doğrulamasının gerekli olup olmadığını belirtir. kimlik doğrulama geri çağırma yordamı tarafından **NX_HTTP_DONT_AUTHENTICATE** döndürülürse ad, parola ve bölge işaretçileri kullanılmaz. Aksi halde, HTTP sunucu geliştiricisi, *nx_http_server. h* içinde tanımlanan **NX_HTTP_MAX_USERNAME** ve **NX_HTTP_MAX_PASSWORD** kimlik doğrulama geri aramasında belirtilen Kullanıcı adı ve parola için yeterince büyük olduğundan emin olmalıdır. Bunların ikisi de varsayılan olarak 20 karakter olacak şekilde ayarlanır.

## <a name="http-invalid-usernamepassword-callback"></a>HTTP geçersiz Kullanıcı adı/parola geri çağırması

HTTP sunucusu bir Istemci isteğinde geçersiz bir Kullanıcı adı ve parola birleşimi alırsa NetX HTTP sunucusunda isteğe bağlı geçersiz Kullanıcı adı/parola geri çağırması çağrılır. HTTP sunucusu uygulaması HTTP sunucusu ile bir geri çağırma kaydederse, *nx_http_server_get_process*, *nx_http_server_put_process* veya nx_http_server_delete_process ' de temel veya Özet kimlik doğrulaması başarısız olursa çağrılacaktır *.*

HTTP sunucusuyla bir geri çağırma kaydetmek için, NetX HTTP sunucusunda aşağıdaki hizmet tanımlanmıştır.

```c
UINT nx_http_server_invalid_userpassword_notify_set (NX_HTTP_SERVER *http_server_ptr,
                                                    UINT *invalid_username_password_callback)
                                                    (CHAR *resource,
                                                    ULONG *client_nx_address,
                                                    UINT request_type));
```
İstek türleri aşağıdaki gibi tanımlanır:

- **NX_HTTP_SERVER_GET_REQUEST**
- **NX_HTTP_SERVER_POST_REQUEST**
- **NX_HTTP_SERVER_HEAD_REQUEST**
- **NX_HTTP_SERVER_PUT_REQUEST**
- **NX_HTTP_SERVER_DELETE_REQUEST**

## <a name="http-insert-gmt-date-header-callback"></a>HTTP ekleme GMT Tarih üst bilgisi geri araması

NetX HTTP sunucusunda, yanıt iletilerinde bir tarih üst bilgisi eklemek için isteğe bağlı bir geri çağırma vardır. HTTP sunucusu bir put veya GET isteğine yanıt vermediğinde bu geri çağırma çağrılır

HTTP sunucusuna bir GMT Tarih geri çağırması kaydetmek için, NetX HTTP sunucusunda aşağıdaki hizmet tanımlanmıştır.

```c
UINT _nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                                     VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

NX_HTTP_SERVER_DATE veri türü aşağıdaki gibi tanımlanır:

```c
typedef struct NX_HTTP_SERVER_DATE_STRUCT
{
    USHORT     nx_http_server_year;         /* Year        */
    UCHAR      nx_http_server_month;        /* Month       */
    UCHAR      nx_http_server_day;          /* Day         */
    UCHAR      nx_http_server_hour;         /* Hour        */
    UCHAR      nx_http_server_minute;       /* Minute      */
    UCHAR      nx_http_server_second;       /* Second      */
    UCHAR      nx_http_server_weekday;      /* Weekday     */
} NX_HTTP_SERVER_DATE;
```

## <a name="http-cache-info-get-callback"></a>HTTP önbellek bilgileri geri çağırma al

HTTP sunucusu, belirli bir kaynak için HTTP uygulamasından maksimum yaş ve Tarih istemek üzere bir geri çağırma işlemi içerir. Bu bilgiler, HTTP sunucusunun bir Istemci GET isteğine yanıt olarak tüm sayfayı gönderip göndermediğini tespit etmek için kullanılır. Istemci isteğindeki "değiştirilme sonrasında" veya alma önbelleği geri araması tarafından döndürülen "son değiştirilme" tarihi ile eşleşmiyorsa, sayfanın tamamı gönderilir.

Geri aramayı HTTP sunucusuna kaydetmek için aşağıdaki hizmet tanımlanmıştır:

```c
UINT _nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                                            UINT (*cache_info_get)
                                            (CHAR *, UINT *, NX_HTTP_SERVER_DATE *));
```

## <a name="http-multipart-support"></a>HTTP çok parçalı desteği

Çok amaçlı Internet posta uzantıları (MIME) başlangıçta SMTP protokolüne yöneliktir, ancak kullanımı HTTP 'ye yayılmıştır. MIME, iletilerin aynı ileti içinde karma ileti türlerini (ör. image/jpg ve metin/düz) içermesini sağlar. NetX HTTP sunucusu, Istemciden MIME içeren HTTP iletilerindeki içerik türünü belirlemede hizmetler ekledi. HTTP çok parçalı desteğini etkinleştirmek ve bu hizmetleri kullanmak için **NX_HTTP_MULTIPART_ENABLE** yapılandırma seçeneğinin tanımlanması gerekir.

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                     NX_PACKET **packet_pptr,
                                     UCHAR *entity_header_buffer,
                                     ULONG buffer_size);

UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      ULONG *available_offset,
                                      ULONG *available_length);
```

Bu hizmetlerin kullanımı hakkında daha fazla bilgi için, Bölüm 3 "HTTP hizmetlerinin açıklaması" bölümünde açıklamasına bakın.

## <a name="http-multi-thread-support"></a>HTTP çoklu Iş parçacığı desteği

NetX HTTP Istemci Hizmetleri birden çok iş parçacığından aynı anda çağrılabilir. Ancak, belirli bir HTTP Istemci örneği için okuma veya yazma istekleri aynı iş parçacığından sırayla yapılmalıdır.

## <a name="http-rfcs"></a>HTTP RFC 'Leri

NetX HTTP, RFC1945 "Hypertext Transfer Protocol/1.0", RFC 2581 "TCP tıkanıklık denetimi", RFC 1122 "Internet konakları için gereksinimler" ve ilgili RFC 'Ler ile uyumludur.