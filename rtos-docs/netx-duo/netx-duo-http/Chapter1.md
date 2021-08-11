---
title: Bölüm 1-Azure RTOS NetX Duo HTTP 'ye giriş
description: Bu bölümde, Azure RTOS NetX Duo HTTP modülü tanıtılmaktadır.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 45f35f2c1bec142e10d29eedb6e5a88a8eb74771e5d4adf1d85b04a87ad59ab7
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796217"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-http"></a>Bölüm 1-Azure RTOS NetX Duo HTTP 'ye giriş

Köprü Metni Aktarım Protokolü (HTTP), Web üzerinde içerik aktarmak için tasarlanan bir protokoldür. HTTP, içerik aktarım işlevini gerçekleştirmek için güvenilir Iletim Denetimi Protokolü (TCP) hizmetlerinden yararlanan basit bir protokoldür. Bu nedenle, HTTP son derece güvenilir bir içerik aktarım protokolüdür. HTTP, en çok kullanılan uygulama protokollerinden biridir. Web 'deki tüm işlemler HTTP protokolünü kullanır. Azure RTOS NetX Duo HTTP hem IPv4 hem de IPv6 ağlarını karşılar. Özgün Azure RTOS NetX HTTP API 'sindeki bazı değişiklikler IPv6 'Yı barındırmak için gereklidir ve bu belgede açıklanacak olsa da, IPv6 HTTP protokolünü doğrudan değiştirmez.

## <a name="http-requirements"></a>HTTP gereksinimleri

NetX Duo HTTP paketi, düzgün çalışması için bir NetX Duo (sürüm 5,2 veya üzeri) yüklü olmasını gerektirir. Ayrıca, bir IP örneğinin zaten oluşturulması ve TCP 'nin aynı IP örneğinde etkinleştirilmiş olması gerekir. IPv6 ana bilgisayar uygulamasının, IPv6 API ve/veya DHCPv6 kullanarak bağlantısını yerel ve genel IPv6 adresi ayarlaması gerekir. Bölüm **2** ' de "küçük örnek sistem" bölümündeki tanıtım dosyası bunun nasıl yapıldığını gösterir.

NetX Duo HTTP paketinin HTTP Istemci bölümünün başka gereksinimi yoktur.

NetX Duo HTTP paketinin HTTP sunucusu bölümü bazı ek gereksinimlere sahiptir. İlk olarak, tüm Istemci HTTP isteklerini işlemek için TCP 'nin iyi bilinen bağlantı noktası 80 ' e tam erişim gerektirir. HTTP sunucusu Ayrıca dosya Embedded dosya sistemiyle kullanılmak üzere tasarlanmıştır. FileX yoksa, Kullanıcı kendi ortamlarında kullanılan FileX bölümlerinin bağlantı noktasını alabilir. Bu, bu kılavuzun sonraki bölümlerinde ele alınmıştır.

## <a name="http-constraints"></a>HTTP kısıtlamaları

NetX Duo HTTP protokolü, HTTP 1,0 standardını uygular. Ancak, aşağıdaki kısıtlamalar vardır:

1.  Kalıcı bağlantılar desteklenmiyor
2.  İstek ardışık düzen oluşturma desteklenmiyor
3.  HTTP sunucusu hem temel hem de MD5 Özet kimlik doğrulamasını destekler, ancak MD5-sess içermez. Mevcut olduğunda, HTTP Istemcisi yalnızca temel kimlik doğrulamasını destekler.
4.  İçerik sıkıştırması desteklenmez.
5.  Izleme, Seçenekler ve bağlantı istekleri desteklenmez.
6.  HTTP sunucusu veya Istemcisiyle ilişkili paket havuzu, HTTP üst bilgisinin tamamını tutabilecek kadar büyük olmalıdır.
7.  HTTP Istemci Hizmetleri yalnızca içerik aktarımına yöneliktir; Bu pakette sunulan bir görüntüleme yardımcı programı yoktur.

## <a name="http-url-resource-names"></a>HTTP URL 'SI (kaynak adları)

HTTP protokolü, Web 'de içerik aktarmak için tasarlanmıştır. İstenen içerik Evrensel Kaynak Bulucu (URL) tarafından belirtilir. Bu, her HTTP isteğinin birincil bileşenidir. URL 'Ler her zaman bir *"/"* karakteriyle başlar ve genellikle HTTP sunucusundaki dosyalara karşılık gelir. Ortak HTTP dosya uzantıları aşağıda gösterilmiştir:

| Dahili numara | Anlamı |
| --------- | ------- |
| .htm (veya .html) | Köprü Metni Biçimlendirme Dili (HTML) |
| .txt | Düz ASCII metni |
| .gif | İkili GIF resmi |
| . XBM | İkili Xbit eşlem resmi |

## <a name="http-client-requests"></a>HTTP Istemci Istekleri

HTTP, Web içeriği istemek için basit bir mekanizmaya sahiptir. Temel olarak *BILINEN TCP bağlantı noktası 80*' de bir bağlantı başarıyla kurulduktan sonra istemci tarafından VERILEN standart http komutları kümesi vardır. Aşağıdakiler, temel HTTP komutlarının bazılarını göstermektedir:

| HTTP komutu | Anlamı |
| ------------ | ------- |
| Kaynağı al HTTP/1.0 | *Belirtilen kaynağı al* |
| POST kaynağı HTTP/1.0 | *Belirtilen kaynağı alın ve HTTP hizmeti 'ne ekli girişi geçirin* |
| BAŞ kaynak HTTP/1.0 | *HTTP sunucusu tarafından GET, ancak içerik değil olarak kabul edildi* |
| Kaynağı koy HTTP/1.0 | *Kaynağı HTTP sunucusuna yerleştir* |
| Kaynağı SIL HTTP/1.0 | *Sunucuda kaynağı Sil* |

Bu ASCII komutları, HTTP sunucusu ile HTTP işlemleri gerçekleştirmek için Web tarayıcıları ve NetX HTTP Istemci Hizmetleri tarafından dahili olarak oluşturulur.

> [!NOTE]
> HTTP Istemci uygulaması varsayılan bağlantı noktası 80 ' dir. Ancak, nx_http_client_set_connect_port hizmetini kullanarak çalışma zamanında bağlantı bağlantı noktasını HTTP sunucusu ile değiştirebilir. Bu hizmetin daha fazla ayrıntı için bkz. Bölüm 4. Bu, zaman zaman Istemci bağlantıları için alternatif bağlantı noktaları kullanan Web sunucularına uyum sağlar.

## <a name="http-server-responses"></a>HTTP sunucusu yanıtları

HTTP sunucusu, Istemci komut yanıtlarını göndermek için *TANıNMıŞ TCP bağlantı noktası 80* ' ü kullanır. HTTP sunucusu Client komutunu işlediğinde, 3 basamaklı bir sayısal durum kodu içeren bir ASCII yanıt dizesi döndürür. Sayısal yanıt, HTTP Istemci yazılımı tarafından işlemin başarılı veya başarısız olup olmadığını tespit etmek için kullanılır. Istemci komutlarına yönelik çeşitli HTTP sunucu yanıtlarının listesi aşağıda verilmiştir:

| Sayısal alan | Anlamı |
| ------------- | ------- |
| *200* | *İstek başarılı oldu* |
| *400* |   *İstek düzgün biçimlendirilmemiş* |
| *401* | *Yetkisiz istek, istemcinin kimlik doğrulaması gönderebilmesi gerekir* |
| *404* | *İstekteki belirtilen kaynak bulunamadı* |
| *500* | *İç HTTP sunucusu hatası* |
| *501* | *İstek HTTP sunucusu tarafından uygulanmadı* |
| *502* | *Hizmet kullanılamıyor* |

Örneğin, "test.htm" dosyasını yERLEşTIRMEk için başarılı bir Istemci isteği "HTTP/1.0 200 Tamam" iletisiyle yanıt verdi.

## <a name="http-communication"></a>HTTP Iletişimi

Daha önce belirtildiği gibi, HTTP sunucusu, Istemci isteklerini alan iyi bilinen TCP bağlantı noktası 80 ' ü kullanır. HTTP Istemcileri, kullanılabilir herhangi bir TCP bağlantı noktasını kullanabilir. HTTP olaylarının genel sırası aşağıdaki gibidir:

### <a name="http-get-request"></a>HTTP GET Isteği:

1.  İstemci, 80 numaralı sunucu bağlantı noktasına TCP Connect sorunları.
2.  İstemci "**Get Resource http/1.0**" isteği gönderir (diğer üst bilgi bilgileriyle birlikte).
3.  Sunucu "**http/1.0 200 Tamam**" iletisini, daha sonra kaynak içeriği (varsa) tarafından hemen izlenir.
4.  Sunucu bir bağlantı kesmeyi gerçekleştiriyor.
5.  İstemci bağlantıyı keser.

### <a name="http-put-request"></a>HTTP PUT İsteği:

1.  İstemci, SUNUCU bağlantı noktası 80'e TCP bağlantısı verir.
2.  İstemci diğer üst bilgi bilgileriyle birlikte " PUT kaynağı **HTTP/1.0**" isteğini ve ardından kaynak içeriğini gönderir.
3.  Sunucu, ek bilgilerle birlikte hemen kaynak içeriğinin takip ettiği bir "**HTTP/1.0 200 Tamam"** iletisi derleme.
4.  Sunucu bağlantıyı keser.
5.  İstemci bağlantıyı keser.

> [!NOTE]
>Daha önce belirtildiği gibi HTTP İstemcisi, istemcilere bağlanmak için alternatif  bağlantı noktaları kullanan web sunucularının nx_http_client_set_connect_port bağlantı noktasını kullanarak varsayılan bağlantı noktasını 80'den başka bir bağlantı noktasına değiştirebilir.

## <a name="http-authentication"></a>HTTP Kimlik Doğrulaması

HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web istekleri için gerekli değildir. Kimlik doğrulamasının iki çeşidi vardır: temel ve özet. Temel kimlik doğrulaması, birçok protokolde bulunan ad ve parola kimlik doğrulaması ile eşdeğerdir. HTTP temel kimlik doğrulamasında ad ve parolalar base64 biçiminde bir olur ve kodlanmış olur. Temel kimlik doğrulamasının temel dezavantajı, istekte açık bir şekilde iletilen ad ve paroladır. Bu, ad ve parolanın çalınmalarını biraz kolaylaştırır. Özet kimlik doğrulaması, istekte adı ve parolayı hiçbir zaman ileterek bu sorunu çözmektedir. Bunun yerine, ad, parola ve diğer bilgilerden 128 bitlik bir anahtar veya özet türetmek için bir algoritma kullanılır. NetX HTTP Sunucusu standart MD5 özet algoritmasını destekler.

Kimlik doğrulaması ne zaman gereklidir? Temelde HTTP Sunucusu istenen bir kaynağın kimlik doğrulaması gerektir olup olduğuna karar verir. Kimlik doğrulaması gerekli ise ve İstemci isteği doğru kimlik doğrulamasını içermezse, gerekli kimlik doğrulaması türüne sahip bir "HTTP/1.0 401 Yetkisiz" yanıtı İstemciye gönderilir. İstemcinin daha sonra uygun kimlik doğrulamasıyla yeni bir istek oluşturması beklenir.

## <a name="http-authentication-callback"></a>HTTP Kimlik Doğrulaması Geri Çağırma

Daha önce belirtildiği gibi HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web aktarımları için gerekli değildir. Ayrıca kimlik doğrulaması genellikle kaynağa bağımlıdır. Sunucu'da bazı kaynaklara erişim kimlik doğrulaması gerektirirken diğerleri kimlik doğrulaması gerektirmez. NetX HTTP Server paketi, uygulamanın her HTTP İstemcisi isteğini *işlemenin* başında çağrılır bir kimlik doğrulama geri çağırma yordamı (nx_http_server_create çağrısı aracılığıyla) belirtmesini sağlar.

Geri çağırma yordamı, NetX HTTP Sunucusuna kaynakla ilişkili kullanıcı adı, parola ve alan dizelerini sağlar ve gerekli kimlik doğrulama türünü geri gönderir. Kaynak için kimlik doğrulaması gerekli yoksa, kimlik doğrulaması geri çağırma değeri olarak **NX_HTTP_DONT_AUTHENTICATE.** Aksi takdirde, belirtilen kaynak için temel kimlik doğrulaması gerekli ise, yordam **NX_HTTP_BASIC_AUTHENTICATE.** Son olarak, MD5 özet kimlik doğrulaması gerekli ise, geri çağırma yordamı **NX_HTTP_DIGEST_AUTHENTICATE.** HTTP Sunucusu tarafından sağlanan herhangi bir kaynak için kimlik doğrulaması gerekmiyorsa, geri çağırma gerekmez ve HTTP Sunucusu oluşturma çağrısına NULL işaretçisi sağlanmalıdır.

Uygulama kimlik doğrulaması geri çağırma yordamının biçimi çok basittir ve aşağıda tanımlanmıştır:

```c
UINT nx_http_server_authentication_check(NX_HTTP_SERVER *server_ptr,
                                          UINT request_type, CHAR *resource,
                                          CHAR **name, CHAR **password,
                                          CHAR **realm);
```
Giriş parametreleri aşağıdaki gibi tanımlanır:

| Parametre | Anlamı |
| --------- | --------|
| *request_type* | HTTP İstemcisi isteğini belirtir, geçerli istekler şu şekilde tanımlanır: <br/> **NX_HTTP_SERVER_GET_REQUEST**<br/>**NX_HTTP_SERVER_POST_REQUEST**<br/>**NX_HTTP_SERVER_HEAD_REQUEST**<br/>**NX_HTTP_SERVER_PUT_REQUEST**<br/>**NX_HTTP_SERVER_DELETE_REQUEST** |
| *kaynak* | Belirli bir kaynak isteği. |
| *Adı* | Gerekli kullanıcı adı işaretçisi için hedef. |
| *parola* | Gerekli parolanın işaretçisi için hedef. |
| *Bölge* | Bu kimlik doğrulaması için alelade işaretçinin hedefi. |

Kimlik doğrulama yordamının dönüş değeri, kimlik doğrulamasının gerekli olup olduğunu belirtir. ```name, password, and realm``` kimlik doğrulama geri çağırma **yordamı NX_HTTP_DONT_AUTHENTICATE** işaretçiler kullanılamaz. Aksi takdirde HTTP sunucusu **geliştiricisi, nxd_http_server.h'de** tanımlanan NX_HTTP_MAX_USERNAME ve *NX_HTTP_MAX_PASSWORD'ların* kimlik doğrulama geri çağırmada belirtilen kullanıcı adı ve parola için yeterince büyük olduğundan emin olması gerekir.  Bunların ikisi de varsayılan olarak 20 karakter boyutundadır.

## <a name="http-invalid-usernamepassword-callback"></a>HTTP Geçersiz Kullanıcı Adı/Parola Geri Çağırma

HTTP sunucusu bir İstemci isteğinde geçersiz kullanıcı adı ve parola birleşimi aldığında NetX HTTP Sunucusunda isteğe bağlı geçersiz kullanıcı adı/parola geri çağırma çağrılır. HTTP sunucusu uygulaması HTTP sunucusuna bir geri çağırma kaydettirilirse, temel veya özet kimlik doğrulaması nx_http_server_get_process , *nx_http_server_put_process* *veya* içinde başarısız olursa *nx_http_server_delete_process.*

HTTP sunucusuna geri arama kaydetmek için NetX Duo HTTP Sunucusu'da aşağıdaki hizmet tanımlanmıştır.

```c
UINT nx_http_server_invalid_userpassword_notify_set(
                   NX_HTTP_SERVER *http_server_ptr,
                   UINT *invalid_username_password_callback)
                            (CHAR *resource,
                             NXD_ADDRESS *client_nxd_address,
                             UINT request_type))
```

İstek türleri aşağıdaki gibi tanımlanır:
 - **NX_HTTP_SERVER_GET_REQUEST**
 - **NX_HTTP_SERVER_POST_REQUEST**
 - **NX_HTTP_SERVER_HEAD_REQUEST**
 - **NX_HTTP_SERVER_PUT_REQUEST**
 - **NX_HTTP_SERVER_DELETE_REQUEST**

## <a name="http-insert-gmt-date-header-callback"></a>HTTP Insert GMT Date Header Callback

NetX Duo HTTP Sunucusunda yanıt iletilerine tarih üst bilgisi eklemek için isteğe bağlı bir geri çağırma vardır. HTTP Sunucusu bir put veya get isteğine yanıt veriyorsa bu geri çağırma çağrılır

NetX Duo HTTP Sunucusunda yanıt iletilerine tarih üst bilgisi eklemek için isteğe bağlı bir geri çağırma vardır. HTTP Sunucusu bir put veya get isteğine yanıt veriyorsa bu geri çağırma çağrılır

BIR GMT tarih geri aramasını HTTP sunucusuna kaydetmek için NetX Duo HTTP Sunucusunda aşağıdaki hizmet tanımlanır.

```c
UINT  _nx_http_server_gmt_callback_set(
                    NX_HTTP_SERVER *server_ptr,
                    VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date)
```

Veri NX_HTTP_SERVER_DATE türü aşağıdaki gibi tanımlanır:

```c
typedef struct NX_HTTP_SERVER_DATE_STRUCT
{
    USHORT          nx_http_server_year;           /* Year                 */
    UCHAR           nx_http_server_month;          /* Month                */
    UCHAR           nx_http_server_day;            /* Day                  */
    UCHAR           nx_http_server_hour;           /* Hour              */
    UCHAR           nx_http_server_minute;         /* Minute               */
    UCHAR           nx_http_server_second;         /* Second               */
    UCHAR           nx_http_server_weekday;        /* Weekday              */
} NX_HTTP_SERVER_DATE;
```

## <a name="http-cache-info-get-callback"></a>HTTP Önbellek Bilgileri Geri Çağırma Alma

HTTP Sunucusunun belirli bir kaynak için HTTP uygulamasından en yüksek yaş ve tarihi talep etmek için bir geri çağırması vardır. Bu bilgiler, HTTP sunucusunun bir İstemci Get isteğine yanıt olarak sayfanın tamamını gönder olup olmadığını belirlemek için kullanılır. İstemci isteğinde "bu tarihten sonra değiştirildiyse" bulunamasa veya get önbelleği geri çağırma tarafından döndürülen "son değiştirme" tarihiyle eşlenemezse, sayfanın tamamı gönderilir.

Geri çağırmayı HTTP sunucusuna kaydetmek için aşağıdaki hizmet tanımlanır:

```c
UINT  _nx_http_server_cache_info_callback_set(
                              NX_HTTP_SERVER *server_ptr,
                              UINT (*cache_info_get)
                                    (CHAR *, UINT *, NX_HTTP_SERVER_DATE *))
```

## <a name="http-multipart-support"></a>HTTP Çok Parçalı Desteği

Çok Amaçlı İnternet Posta Uzantıları (MIME) başlangıçta SMTP protokolü için tasarlanmıştır, ancak kullanımı HTTP'ye yayılmıştır. MIME, iletilerin aynı ileti içinde karışık ileti türleri (görüntü/jpg ve metin/düz gibi) içermesini sağlar. NetX Duo HTTP Sunucusu, İstemciden MIME içeren HTTP iletilerinden içerik türünü belirlemek için hizmetler ekledi. HTTP çok parçalı desteğini etkinleştirmek ve bu hizmetleri kullanmak için, NX_HTTP_MULTIPART_ENABLE **yapılandırma** seçeneği tanımlanmalıdır.

```c
UINT  nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_pptr,
                                       UCHAR *entity_header_buffer,
                                       ULONG buffer_size);

UINT  nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET **packet_pptr,
                                        ULONG *available_offset,
                                        ULONG *available_length)
```

Bu hizmetlerin kullanımı hakkında daha fazla ayrıntı için 3. Bölüm "HTTP Hizmetlerinin Açıklaması" bölümünde açıklamalarına bakın.

## <a name="http-multi-thread-support"></a>HTTP Çoklu İş Parçacığı Desteği

NetX HTTP İstemcisi hizmetleri aynı anda birden çok iş parçacığından çağrılabilirsiniz. Ancak, belirli bir HTTP İstemcisi örneğine yönelik okuma veya yazma istekleri aynı iş parçacığından sırasıyla yapılmalı.

## <a name="http-rfcs"></a>HTTP RFC'leri

NetX HTTP RFC1945 "Köprü Metni Aktarım Protokolü/1.0, RFC 2581 "TCP Tıkanıklığı Denetimi", RFC 1122 "İnternet Konakları için Gereksinimler" ve ilgili RFC'ler ile uyumludur.
