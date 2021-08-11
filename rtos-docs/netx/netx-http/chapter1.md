---
title: Bölüm 1 - NetX HTTP'ye Giriş
description: Bu belgede, HTTP'nin Web'de içerik aktarmak için tasarlanmış bir protokol olduğu açıklayacak.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1e37328ab9cff0ab635a00113a83ee256c39303ce24b0cb292b6c2eaa71236f5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799396"
---
# <a name="chapter-1---introduction-to-netx-http"></a>Bölüm 1 - NetX HTTP'ye Giriş

Köprü Metni Aktarım Protokolü (HTTP), Web'de içerik aktarmak için tasarlanmış bir protokoldür. HTTP, içerik aktarım işlevini gerçekleştirmek için güvenilir İletim Denetimi Protokolü (TCP) hizmetlerini kullanan basit bir protokoldür. Bu nedenle, HTTP son derece güvenilir bir içerik aktarım protokolüdür. HTTP, en çok kullanılan uygulama protokollerindendir. Web'de yapılan tüm işlemler HTTP protokolünü kullanır.

## <a name="http-requirements"></a>HTTP Gereksinimleri

NetX HTTP paketinin düzgün çalışması için bir NetX (sürüm 5.2 veya sonrası) yüklü olması gerekir. Ayrıca, bir IP örneği zaten oluşturularak aynı IP örneğinde TCP etkinleştirilmelidir. Bölüm **2'nin** "Küçük Örnek Sistem" bölümünde yer alan tanıtım dosyası bunun nasıl tamam olduğunu gösteriyor.

NetX HTTP paketinin HTTP İstemcisi bölümünün başka bir gereksinimleri yoktur.

NetX HTTP paketinin HTTP Sunucusu bölümünün birkaç ek gereksinimleri vardır. İlk olarak, tüm İstemci HTTP isteklerinin işlenmesi için iyi bilinen *80* tcp bağlantı noktasına tam erişim gerektirir. HTTP Sunucusu, FileX ekli dosya sistemiyle kullanım için de tasarlanmıştır. FileX kullanılamıyorsa, kullanıcı kullanılan FileX bölümlerini kendi ortamına taşınabilir. Bu, bu kılavuzun sonraki bölümlerinde ele alınmıştır.

## <a name="http-constraints"></a>HTTP Kısıtlamaları 

NetX HTTP protokolü HTTP 1.0 standardını uygulamaya almaktadır. Ancak, aşağıdaki kısıtlamalar vardır:

1.  Kalıcı bağlantılar desteklenmiyor

2.  İstek yöneltme desteklenmiyor

3.  HTTP Sunucusu hem temel hem de MD5 özet kimlik doğrulamasını destekler, ancak MD5-sess'i desteklemez. Şu anda HTTP İstemcisi yalnızca temel kimlik doğrulamasını destekler.

4.  İçerik sıkıştırması desteklenmiyor.

5.  TRACE, OPTIONS ve CONNECT istekleri desteklenmiyor.

6.  HTTP Sunucusu veya İstemcisi ile ilişkili paket havuzu, tam HTTP üst bilgisini tutacak kadar büyük olmalı.

7.  HTTP İstemci hizmetleri yalnızca içerik aktarımına açıktır; bu pakette hiçbir görüntü yardımcı programı sağlanamıyor.

## <a name="http-url-resource-names"></a>HTTP URL'si (Kaynak Adları)

HTTP protokolü, Web'de içerik aktarımı için tasarlanmıştır. İstenen içerik Evrensel Kaynak Bulucu (URL) tarafından belirtilir. Bu, her HTTP isteğinin birincil bileşenidir. URL'ler her zaman "/" karakteriyle başlar ve genellikle HTTP Sunucusundaki dosyalara karşılık gelen dosyalardır. Yaygın HTTP dosya uzantıları aşağıda gösterilmiştir:

- **.htm (veya .html)** Köprü Metni Biçimlendirme Dili (HTML)
- **.txt** Düz ASCII metni
- **.gif** İkili GIF görüntüsü
- **.xbm** İkili Xbitmap görüntüsü

## <a name="http-client-requests"></a>HTTP İstemci İstekleri

HTTP, Web içeriği isteği için basit bir mekanizmaya sahiptir. Temel olarak, iyi bilinen TCP bağlantı noktası *80'de* başarıyla bağlantı kurulduktan sonra İstemci tarafından verilen bir dizi standart HTTP komutu vardır. Aşağıda temel HTTP komutlarının bazıları ve ardından aşağıdakiler ve daha fazla bilgi ve açıklama yer alazıdır:

- GET kaynağı HTTP/1.0 *Belirtilen kaynağı al*
- POST kaynağı HTTP/1.0 *Belirtilen kaynağı al ve HTTP Sunucusuna eklenmiş girişi geç*
- HEAD kaynağı HTTP/1.0 GET olarak kabul edilir, ancak içerik *HTTP Sunucusu tarafından döndürülz*
- PUT kaynağı HTTP/1.0 *HTTP Sunucusuna kaynak koyma*
- DELETE kaynağı HTTP/1.0 *Sunucuda kaynağı silme*

Bu ASCII komutları, bir HTTP Sunucusu ile HTTP işlemleri gerçekleştirmek için Web tarayıcıları ve NetX HTTP İstemcisi hizmetleri tarafından dahili olarak oluşturulur.

>[!NOTE] 
> HTTP İstemcisi uygulaması varsayılan olarak 80 bağlantı noktasını kullanır. Ancak, nx_http_client_set_connect_port hizmetini kullanarak çalışma zamanında HTTP Sunucusu'nda *bağlantı nx_http_client_set_connect_port* değiştirebilir. Bu hizmetin diğer ayrıntıları için 4. Bölüm'e bakın. Bu, ara sıra İstemci bağlantıları için alternatif bağlantı noktaları kullanan web sunucularını barındırıyor.

## <a name="http-server-responses"></a>HTTP Sunucusu Yanıtları

HTTP Sunucusu, İstemci komut yanıtlarını göndermek için aynı iyi bilinen TCP bağlantı noktası *80'i* kullanır. HTTP Sunucusu İstemci komutunu işlemenin ardından, 3 basamaklı sayısal durum kodu içeren bir ASCII yanıt dizesi döndürür. Sayısal yanıt HTTP İstemcisi yazılımı tarafından, işlemi başarılı veya başarısız olup olmadığını belirlemek için kullanılır. Aşağıda, İstemci komutlarına çeşitli HTTP Sunucusu yanıtlarının listesi ve ardından yer almaktadır:

- 200 *İstek başarılı oldu*
- 400 *İstek düzgün şekilde oluşturulmuş değil*
- 401 *Yetkisiz istek, istemcinin kimlik doğrulaması göndermesi gerekiyor*
- 404 *İstekte belirtilen kaynak bulunamadı*
- 500 *İç HTTP Sunucusu hatası*
- 501 *İstek HTTP Sunucusu tarafından uygulanmadı*
- 502 *Hizmeti kullanılamıyor*

Örneğin, "test.htm" dosyasını PUT'a yapılan başarılı bir İstemci isteği"HTTP/1.0 200 Tamam" iletisiyle yanıt verir.

## <a name="http-communication"></a>HTTP İletişimi

Daha önce belirtildiği gibi, HTTP Sunucusu İstemci isteklerini alan için *iyi bilinen TCP bağlantı noktası 80'i* kullanır. HTTP İstemcileri kullanılabilir herhangi bir TCP bağlantı noktasını kullanabilir. HTTP olaylarının genel sırası aşağıdaki gibidir:

**HTTP GET İsteği:**

1.  İstemci, SUNUCU bağlantı noktası 80'e TCP bağlantısı verir.

2.  İstemci , "**GET resource HTTP/1.0**" isteğini (diğer üst bilgi bilgileriyle birlikte) gönderir.

3.  Sunucu, ek bilgilerle birlikte hemen ardından kaynak içeriği (varsa) gelen bir "**HTTP/1.0 200 Tamam"** iletisi derler.

4.  Sunucu bağlantıyı keser.

5.  İstemci bağlantıyı keser.

**HTTP PUT İsteği:**

1. İstemci, SUNUCU bağlantı noktası 80'e TCP bağlantısı verir.

2. İstemci diğer üst bilgi bilgileriyle birlikte " PUT kaynağı **HTTP/1.0**" isteğini ve ardından kaynak içeriğini gönderir.

3. Sunucu, ek bilgilerle birlikte hemen kaynak içeriğinin takip ettiği bir "**HTTP/1.0 200 Tamam"** iletisi derleme.

4. Sunucu bağlantıyı keser.

5. İstemci bağlantıyı keser.

>[!NOTE] 
> Daha önce belirtildiği gibi HTTP İstemcisi, istemcilere bağlanmak için alternatif  bağlantı noktaları kullanan web sunucularının nx_http_client_set_connect_port bağlantı noktasını kullanarak varsayılan bağlantı noktasını 80'den başka bir bağlantı noktasına değiştirebilir.

## <a name="http-authentication"></a>HTTP Kimlik Doğrulaması

HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web istekleri için gerekli değildir. Kimlik doğrulamasının iki çeşidi vardır: temel *ve özet.*  Temel kimlik doğrulaması, birçok *protokolde bulunan* *ad ve* parola kimlik doğrulaması ile eşdeğerdir. HTTP temel kimlik doğrulamasında ad ve parolalar base64 biçiminde bir olur ve kodlanmış olur. Temel kimlik doğrulamasının temel dezavantajı, istekte açık bir şekilde iletilen ad ve paroladır. Bu, ad ve parolanın çalınmalarını biraz kolaylaştırır. Özet kimlik doğrulaması, istekte adı ve parolayı hiçbir zaman ileterek bu sorunu çözmektedir. Bunun yerine, ad, parola ve diğer bilgilerden 128 bitlik bir anahtar veya özet türetmek için bir algoritma kullanılır. NetX HTTP Sunucusu standart MD5 özet algoritmasını destekler.

Kimlik doğrulaması ne zaman gereklidir? Temelde HTTP Sunucusu istenen bir kaynağın kimlik doğrulaması gerektir olup olduğuna karar verir. Kimlik doğrulaması gerekli ise ve İstemci isteği doğru kimlik doğrulamasını içermezse, gerekli kimlik doğrulaması türüne sahip bir "HTTP/1.0 401 Yetkisiz" yanıtı İstemciye gönderilir. İstemcinin daha sonra uygun kimlik doğrulamasıyla yeni bir istek oluşturması beklenir.

## <a name="http-authentication-callback"></a>HTTP Kimlik Doğrulaması Geri Çağırma

Daha önce belirtildiği gibi HTTP kimlik doğrulaması isteğe bağlıdır ve tüm Web aktarımları için gerekli değildir. Ayrıca kimlik doğrulaması genellikle kaynağa bağımlıdır. Sunucu üzerindeki bazı kaynaklara erişim için kimlik doğrulaması gerekir, diğerleri desteklemez. NetX HTTP sunucu paketi, uygulamanın, her HTTP Istemci isteğini işlemenin başlangıcında çağrılan bir kimlik doğrulama geri çağırma yordamı ( ***nx_http_server_create*** çağrısı aracılığıyla) belirtmesini sağlar.

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