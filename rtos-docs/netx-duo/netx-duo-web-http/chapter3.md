---
title: Bölüm 3-HTTP hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Web HTTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 0357afe7f997c84a5d031ca71dc524e381734b4a
ms.sourcegitcommit: 62cfdf02628530807f4d9c390d6ab623e2973fee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/05/2021
ms.locfileid: "115178196"
---
# <a name="chapter-3---description-of-http-services"></a>Bölüm 3-HTTP hizmetlerinin açıklaması

Bu bölüm, tüm NetX Web HTTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

> [!NOTE]
> Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

## <a name="http-and-https-client-api"></a>HTTP ve HTTPS Istemci API 'SI

## <a name="nx_web_http_client_connect"></a>nx_web_http_client_connect

Özel istekler için bir HTTP sunucusuna düz metin yuvası açma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_connect(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip,
    UINT server_port, ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **düz metin** http içindir.

Bu hizmet bir HTTP sunucusuna düz metin TCP yuvası açar, ancak hiçbir istek göndermez. İstekler n *x_web_http_client_request_initialize ()* ile oluşturulur ve *nx_web_http_client_request_send ()* kullanılarak gönderilir. *Nx_web_http_client_request_header_add ()* kullanılarak Isteğe özel http üstbilgileri eklenebilir.

Bu hizmetin kullanılması, bir uygulamanın isteğe herhangi sayıda özel üst bilgi eklemesini sağlar. **Bu, belirli uygulamalar için tasarlanan özelleştirilmiş HTTP isteklerine izin verir.**

> [!NOTE]
> Nx_web_http_client_ * _start yöntemleri kolaylık sağlaması için sunulmaktadır (örn. *nx_web_http_client_get_start*()) ve istek oluşturma ve yuva bağlantısını işleyebilir. İsteklerinize özel HTTP üstbilgileri gerekmiyorsa, *nx_web_http_client_connect ()* yerine bu hizmetleri ve ilgili yordamları kullanabilirsiniz.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **server_ip** Uzak HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası (örneğin, HTTP için 80).
- **wait_option** Hizmetin temel alınan ağ işlemleri için ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) TCP yuvasının başarılı bağlantısı.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_WEB_HTTP_NOT_READY (0x3000A) başka bir istek zaten devam ediyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NXD_ADDRESS server_ip_addr;

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

nx_web_http_client_connect(&my_client, &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get* until the entire response is retrieved. */

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);
    /* Process response packets… */
}
```

## <a name="nx_web_http_client_create"></a>nx_web_http_client_create

HTTP Istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_create(NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr,
    ULONG window_size);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneğinde bir HTTP Istemci örneği oluşturur. Istemci örneği, HTTP ya da HTTPS için kullanılabilir. HTTP veya HTTPS örneği başlatma hakkında daha fazla bilgi için bkz. *nx_web_http_client_connect ()* ve *nx_web_http_client_secure_connect ()* . Ayrıca, GET, PUT ve POST yöntemlerinin basit etkinleştirmeleri için nx_web_http_client_post_ nx_web_http_client_get_ * *, *nx_web_http_client_put_ * ** için API 'ye de bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **client_name** HTTP Istemci örneğinin adı.
- **ip_ptr** IP örneği işaretçisi.
- **pool_ptr** Varsayılan paket havuzu işaretçisi. Bu havuzdaki paketlerin, tüm yanıt üst bilgisini işleyecek kadar büyük bir yükün olması gerektiğini unutmayın. Bu, *nx_web_http_client. h* içinde *NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE* tarafından tanımlanır.
- **window_size** Istemcinin TCP yuvası alma penceresinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı http istemcisi oluşturma
- NX_PTR_ERROR (0x16) geçersiz HTTP, ip_ptr veya paket havuzu işaretçisi
- NX_WEB_HTTP_POOL_ERROR (0x30009) paket havuzunda geçersiz yük boyutu

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Create the HTTP Client instance "my_client" on "ip_0". */
status = nx_web_http_client_create(&my_client, "my client", &ip_0, &pool_0, 8192);

/* If status is NX_SUCCESS an HTTP Client instance was successfully
    created. */
```

## <a name="nx_web_http_client_delete"></a>nx_web_http_client_delete

HTTP Istemci örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_delete(NX_WEB_HTTP_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir HTTP Istemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı http istemcisi silme
- NX_PTR_ERROR (0x16) geçersiz HTTP işaretçisi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete the HTTP Client instance "my_client." */
status = nx_web_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully
    deleted. */
```

## <a name="nx_web_http_client_delete_start"></a>nx_web_http_client_delete_start

Düz metin HTTP SILME isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_delete_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **düz metin** http içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynak için SILME isteği gönderme girişiminde bulunur. Bu yordam NX_SUCCESS döndürürse, uygulama daha sonra sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilirler.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu API kullanım dışıdır. Geliştiricilerin *nx_web_http_client_delete_start_extended ()* kullanması önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemcisi silme Isteği iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_start(&my_client, &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_delete_start_extended"></a>nx_web_http_client_delete_start_extended

Düz metin HTTP SILME isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_delete_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **düz metin** http içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynak için SILME isteği gönderme girişiminde bulunur. Bu yordam NX_SUCCESS döndürürse, uygulama daha sonra sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilirler.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Kaynak, konak, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.

Bu hizmet *nx_web_http_client_delete_start* () yerini alır. Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **host_length** Konağın dize uzunluğu.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemcisi silme Isteği iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_start_extended(&my_client,
    &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_delete_secure_start"></a>nx_web_http_client_delete_secure_start

Şifrelenmiş bir HTTPS SILME isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_delete_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli** https içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynak için SILME isteği gönderme girişiminde bulunur. Bu yordam NX_SUCCESS döndürürse, uygulama daha sonra sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilirler.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_web_http_client_delete_secure_start_extended ()* kullanması önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi. Kaynak, NULL ile sonlandırılmış olmalıdır.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma. Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemcisi silme Isteği iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_delete_secure_start_extended"></a>nx_web_http_client_delete_secure_start_extended

Şifrelenmiş bir HTTPS SILME isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_delete_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli** https içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynak için SILME isteği gönderme girişiminde bulunur. Bu yordam NX_SUCCESS döndürürse, uygulama daha sonra sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilirler.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.

Bu hizmet *nx_web_http_client_delete_secure_start*() yerini alır. Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi. Kaynak, NULL ile sonlandırılmış olmalıdır.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **host_length** Konağın dize uzunluğu.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma. Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemcisi silme Isteği iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.


### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_secure_start_extended(&my_client,
    &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_get_start"></a>nx_web_http_client_get_start

Düz metin HTTP GET isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_get_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **düz metin** http içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_web_http_client_response_body_get ()* öğesine birden çok çağrı yapabilir.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_web_http_client_get_start_extended ()* kullanması önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    multiple times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_start_extended"></a>nx_web_http_client_get_start_extended

Düz metin HTTP GET isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_get_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **düz metin** http içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_web_http_client_response_body_get ()* öğesine birden çok çağrı yapabilir.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Kaynak, konak, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.

Bu hizmet *nx_web_http_client_get_start*() yerini alır. Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **host_length** Konağın dize uzunluğu.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_start_extended(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    multiple times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_secure_start"></a>nx_web_http_client_get_secure_start

Şifrelenmiş bir HTTPS GET isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_get_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
        NX_SECURE_TLS_SESSION *tls_session),
        ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli** https içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_web_http_client_response_body_get ()* öğesine birden çok çağrı yapabilir.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_web_http_client_get_secure_start_extended ()* kullanması önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma. Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started
    and is so far successful. The client must now call
    *nx_web_http_client_response_body_get()* multiple times to
    retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_secure_start_extended"></a>nx_web_http_client_get_secure_start_extended

Şifrelenmiş bir HTTPS GET isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_get_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli** https içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_web_http_client_response_body_get ()* öğesine birden çok çağrı yapabilir.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Kaynak, konak, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.

Bu hizmet *nx_web_http_client_secure_start*() yerini alır. Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **host_length** Konağın dize uzunluğu.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma. Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM
    is started and is so far successful. The client must now call
    *nx_web_http_client_response_body_get()* multiple times to retrieve
    the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_head_start"></a>nx_web_http_client_head_start

Düz metin HTTP HEAD isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_head_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **düz metin** http içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağın baş meta verilerini almaya çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama yanıt almak için *nx_web_http_client_response_body_get ()* çağırabilir.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_web_http_client_head_start_extended ()* kullanması önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemci Head Isteği iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_head_start_extended"></a>nx_web_http_client_head_start_extended

Düz metin HTTP HEAD isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_head_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **düz metin** http içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağın baş meta verilerini almaya çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama yanıt almak için *nx_web_http_client_response_body_get ()* çağırabilir.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.

Bu hizmet *nx_web_http_client_head_start*() yerini alır. Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **host_length** Konağın dize uzunluğu.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemci Head Isteği iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_head_secure_start"></a>nx_web_http_client_head_secure_start

Şifrelenmiş bir HTTPS HEAD isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_head_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli** https içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağın baş meta verilerini almaya çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilir.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_web_http_client_head_secure_start_extended ()* kullanması önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma. Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http istemci Head Isteği iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- **NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_head_secure_start_extended"></a>nx_web_http_client_head_secure_start_extended

Şifrelenmiş bir HTTPS HEAD isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_head_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli** https içindir.

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağın baş meta verilerini almaya çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilir.

Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Kaynak, konak, kullanıcı adı ve parola dizeleri NULL olarak sonlandırılmalı ve her dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukta olmalıdır.

Bu hizmet , *() nx_web_http_client_head_secure_start* değiştirir. Bu sürüm, çağıranların işleve uzunluk bilgileri teminsini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **server_port** Uzak HTTP Sunucusunda bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesi işaretçisi.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **konak** Sunucunun etki alanı adının null sonlandırıldı dizesi. Bu dize HTTP Ana Bilgisayar üst bilgisi alanında iletildi. Konak dizesi NULL olamaz.
- **host_length** Ana bilgisayar dize uzunluğu.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **username_length** Kimlik doğrulaması için kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **tls_setup** TLS yapılandırmasını kurulumu için kullanılan geri çağırma. Uygulama, TLS şifrelemesi ve kimlik bilgilerini (örneğin sertifikalar) başlatmak için bu geri çağırmayı tanımlar.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Http İstemciSI HEAD istek iletisi başarıyla gönderildi
- **NX_WEB_HTTP_ERROR** (0x30000) İç HTTP İstemcisi hatası
- **NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP İstemcisi hazır değil
- **NX_WEB_HTTP_FAILED** (0x30002) HTTP Sunucusu ile iletişim kurarken HTTP İstemcisi hatası.
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_request_packet_allocate"></a>nx_web_http_client_request_packet_allocate

HTTP(S) paketi ayırma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_request_packet_allocate(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, İstemci HTTP'leri için bir paket ayırmaya çalışır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **packet_ptr** Ayrılan paketin işaretçisi.
- **wait_option** Paket havuzunda kullanılabilir paket yoksa, bekleme süresi tıklar içinde tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **NX_NO_WAIT** (0x00000000)
  - **NX_WAIT_FOREVER** (0xFFFFFFFF)
  - **tıklar içinde zaman aşımı** (0x00000001 aracılığıyla 0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı paket ayırma
- **NX_NO_PACKET** (0x01) Paket yok
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma isteği, *tx_thread_wait_abort.*
- **NX_INVALID_PARAMETERS** (0x4D) Paket boyutu protokolü destekleyem yok.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Allocate a packet for HTTP(S) Client and suspend for a maximum of 5 timer
    ticks if the pool is empty. */
status = nx_web_http_client_request_packet_allocate(&my_client, &packet_ptr, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
    variable packet_ptr. */
```

## <a name="nx_web_http_client_post_start"></a>nx_web_http_client_post_start

HTTP POST isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_post_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host,
    CHAR *username, CHAR *password,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem düz metin **HTTP'ye** göredir.

Bu hizmet, belirtilen kaynakla birlikte verilen IP adresi ve bağlantı noktası üzerinden HTTP Sunucusuna bir POST isteği göndermeye çalışır. Bu yordam başarılı olursa, uygulama kodu kaynak içeriklerini HTTP Sunucusuna *göndermek nx_web_http_client_put_packet* yordama başarıyla çağrılar yapmalı.

Kaynak dizesinin "/index.htm" gibi yerel bir dosyaya başvurarak veya başka bir URL'ye başvurabilirsiniz. Örneğin HTTP Sunucusu, PUT isteklerini desteklediğini `http://abc.website.com/index.htm` gösteriyorsa.

Bu hizmet kullanım dışıdır. Geliştiricilerin *nx_web_http_client_post_start_extended() kullanmaları teşvik edilecektir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **server_port** Uzak HTTP SunucusundaKI TCP bağlantı noktası.
- **kaynak** Kaynağın Sunucuya göndermesi için URL dizesinin işaretçisi.
- **konak** Sunucunun etki alanı adının null sonlandırıldı dizesi. Bu dize HTTP Ana Bilgisayar üst bilgisi alanında iletildi. Konak dizesi NULL olamaz.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **total_bytes** Gönderilen kaynağın toplam bayt sayısı. Sonraki nx_web_http_client_put_packet() çağrıları aracılığıyla gönderilen tüm paketlerin birleşik *uzunluğunun bu değere* eşit olması gerektiğini unutmayın.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarıyla gönderilen POST isteği
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için fazla büyük
- **NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP İstemcisi hazır değil
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Kaynağın toplam boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start an HTTP POST to post the 20-byte resource "/TEST.HTM" to the HTTP Server
    at IP address 1.2.3.5. */
status = nx_web_http_client_post_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_start_extended"></a>nx_web_http_client_post_start_extended

HTTP POST isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_post_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem düz metin **HTTP'ye** göredir.

Bu hizmet, belirtilen kaynakla birlikte verilen IP adresi ve bağlantı noktası üzerinden HTTP Sunucusuna bir POST isteği göndermeye çalışır. Bu yordam başarılı olursa, uygulama kodu kaynak içeriklerini HTTP Sunucusuna *göndermek nx_web_http_client_put_packet* yordama başarıyla çağrılar yapmalı.

Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.

Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.

Bu hizmet *nx_web_http_client_post_start* () yerini alır. Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **host_length** Konağın dize uzunluğu.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **total_bytes** Gönderilen toplam kaynak bayt sayısı. *Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) post isteği başarıyla gönderildi
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start an HTTP POST to post the 20-byte resource "/TEST.HTM" to the HTTP Server
    at IP address 1.2.3.5. */
status = nx_web_http_client_post_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_secure_start"></a>nx_web_http_client_post_secure_start

Şifrelenmiş bir HTTPS POST isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_post_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli** https içindir.

Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTPS sunucusuna belirtilen kaynağa sahip bir POST isteği gönderme girişiminde bulunur. Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.

Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_web_http_client_post_secure_start_extended ()* kullanması önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.
- **kaynak** Sunucuya gönderilen kaynağın URL dizesi işaretçisi.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **total_bytes** Gönderilen toplam kaynak bayt sayısı. *Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.
- **tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma. Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.
- **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) post isteği başarıyla gönderildi
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük
- **NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_secure_start_extended"></a>nx_web_http_client_post_secure_start_extended

Şifrelenmiş bir HTTPS POST isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_post_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli** https içindir.

Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTPS sunucusuna belirtilen kaynağa sahip bir POST isteği gönderme girişiminde bulunur. Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.

Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.

Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.

Bu hizmet *nx_web_http_client_post_secure_start* () yerini alır. Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
- **ip_address** HTTP sunucusunun IP adresi.
- **SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi. Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir. Ana bilgisayar dizesi NULL olamaz.
- **host_length** Konağın dize uzunluğu.
- **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
- **username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **total_bytes** Gönderilen toplam kaynak bayt sayısı. *Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.
- **tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma. Uygulama, TLS şifrelemesi ve kimlik bilgilerini (örneğin sertifikalar) başlatmak için bu geri çağırmayı tanımlar.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarıyla gönderilen POST isteği
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için fazla büyük
- **NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP İstemcisi hazır değil
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Kaynağın toplam boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_start"></a>nx_web_http_client_put_start

HTTP PUT isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_put_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem düz metin **HTTP'ye** göredir.

Bu hizmet, belirtilen kaynakla birlikte verilen IP adresi ve bağlantı noktası üzerinden HTTP Sunucusuna bir PUT isteği göndermeyi dener. Bu yordam başarılı olursa, uygulama kodu kaynak içeriklerini HTTP Sunucusuna göndermek için *nx_web_http_client_put_packet() yordamına* başarılı çağrılar göndermektedir.

Kaynak dizesinin "/index.htm" gibi yerel bir dosyaya başvurarak veya başka bir URL'ye başvurabilirsiniz. Örneğin HTTP Sunucusu, PUT isteklerini desteklediğini `http://abc.website.com/index.htm` gösteriyorsa.

Bu hizmet kullanım dışıdır. Geliştiricilerin *nx_web_http_client_put_start_extended() kullanmaları teşvik edilecektir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **server_port** Uzak HTTP SunucusundaKI TCP bağlantı noktası.
- **kaynak** Kaynağın Sunucuya göndermesi için URL dizesinin işaretçisi.
- **konak** Sunucunun etki alanı adının null sonlandırıldı dizesi. Bu dize HTTP Ana Bilgisayar üst bilgisi alanında iletildi. Konak dizesi NULL olamaz.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **total_bytes** Gönderilen kaynağın toplam bayt sayısı. Sonraki nx_web_http_client_put_packet() çağrıları aracılığıyla gönderilen tüm paketlerin birleşik *uzunluğunun bu değere* eşit olması gerektiğini unutmayın.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Put isteği başarıyla gönderildi
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için fazla büyük
- **NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP İstemcisi hazır değil
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Kaynağın toplam boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTP Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_start_extended"></a>nx_web_http_client_put_start_extended

HTTP PUT isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_put_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem düz metin **HTTP'ye** göredir.

Bu hizmet, belirtilen kaynakla birlikte verilen IP adresi ve bağlantı noktası üzerinden HTTP Sunucusuna bir PUT isteği göndermeyi dener. Bu yordam başarılı olursa, uygulama kodu kaynak içeriklerini HTTP Sunucusuna göndermek için *nx_web_http_client_put_packet() yordamına* başarılı çağrılar göndermektedir.

Kaynak dizesinin "/index.htm" gibi yerel bir dosyaya başvurarak veya başka bir URL'ye başvurabilirsiniz. Örneğin HTTP Sunucusu, PUT isteklerini desteklediğini `http://abc.website.com/index.htm` gösteriyorsa.

Kaynak, konak, kullanıcı adı ve parola dizeleri NULL olarak sonlandırılmalı ve her dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukta olmalıdır.

Bu hizmet , *() nx_web_http_client_put_start* değiştirir. Bu sürüm, çağıranların işleve uzunluk bilgileri teminsini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **server_port** Uzak HTTP SunucusundaKI TCP bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesi işaretçisi.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **konak** Sunucunun etki alanı adının null sonlandırıldı dizesi. Bu dize HTTP Ana Bilgisayar üst bilgisi alanında iletildi. Konak dizesi NULL olamaz.
- **host_length** Ana bilgisayar dize uzunluğu.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **username_length** Kimlik doğrulaması için kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **total_bytes** Gönderilen kaynağın toplam bayt sayısı. Sonraki nx_web_http_client_put_packet() çağrıları aracılığıyla gönderilen tüm paketlerin birleşik *uzunluğunun bu değere* eşit olması gerektiğini unutmayın.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Put isteği başarıyla gönderildi
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için fazla büyük
- **NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP İstemcisi hazır değil
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Kaynağın toplam boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTP Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_secure_start"></a>nx_web_http_client_put_secure_start

Şifrelenmiş bir HTTPS PUT isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_put_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli HTTPS'ye** göredir.

Bu hizmet, belirtilen kaynakla birlikte VERILEN IP adresi ve bağlantı noktası üzerinden HTTPS Sunucusuna bir PUT isteği göndermeye çalışır. Bu yordam başarılı olursa, uygulama kodu kaynak içeriklerini HTTP Sunucusuna göndermek için *nx_web_http_client_put_packet() yordamına* başarılı çağrılar göndermektedir.

Kaynak dizesinin "/index.htm" gibi yerel bir dosyaya başvurarak veya başka bir URL'ye başvurabilirsiniz. Örneğin HTTP Sunucusu, PUT isteklerini desteklediğini `http://abc.website.com/index.htm` gösteriyorsa.

Bu hizmet kullanım dışıdır. Geliştiricilerin *nx_web_http_client_put_secure_start_extended() kullanmaları teşvik edilecektir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **server_port** Uzak HTTP SunucusundaKI TCP bağlantı noktası.
- **kaynak** Kaynağın Sunucuya göndermesi için URL dizesinin işaretçisi.
- **konak** Sunucunun etki alanı adının null sonlandırıldı dizesi. Bu dize HTTP Ana Bilgisayar üst bilgisi alanında iletildi. Konak dizesi NULL olamaz.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **total_bytes** Gönderilen kaynağın toplam bayt sayısı. Sonraki nx_web_http_client_put_packet() çağrıları aracılığıyla gönderilen tüm paketlerin birleşik *uzunluğunun bu değere* eşit olması gerektiğini unutmayın.
- **tls_setup** TLS yapılandırmasını kurulumu için kullanılan geri çağırma. Uygulama, TLS şifrelemesi ve kimlik bilgilerini (örneğin sertifikalar) başlatmak için bu geri çağırmayı tanımlar.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Put isteği başarıyla gönderildi
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için fazla büyük
- **NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP İstemcisi hazır değil
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Kaynağın toplam boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_secure_start_extended"></a>nx_web_http_client_put_secure_start_extended

Şifrelenmiş bir HTTPS PUT isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_put_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli HTTPS'ye** göredir.

Bu hizmet, belirtilen kaynakla birlikte VERILEN IP adresi ve bağlantı noktası üzerinden HTTPS Sunucusuna bir PUT isteği göndermeye çalışır. Bu yordam başarılı olursa, uygulama kodu kaynak içeriklerini HTTP Sunucusuna göndermek için *nx_web_http_client_put_packet() yordamına* başarılı çağrılar göndermektedir.

Kaynak dizesinin "/index.htm" gibi yerel bir dosyaya başvurarak veya başka bir URL'ye başvurabilirsiniz. Örneğin HTTP Sunucusu, PUT isteklerini desteklediğini `http://abc.website.com/index.htm` gösteriyorsa.

Kaynak, konak, kullanıcı adı ve parola dizeleri NULL olarak sonlandırılmalı ve her dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukta olmalıdır.

Bu hizmet , *() nx_web_http_client_put_secure_start* değiştirir. Bu sürüm, çağıranların işleve uzunluk bilgileri teminsini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **server_port** Uzak HTTP SunucusundaKI TCP bağlantı noktası.
- **kaynak** İstenen kaynak için URL dizesi işaretçisi.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **konak** Sunucunun etki alanı adının null sonlandırıldı dizesi. Bu dize HTTP Ana Bilgisayar üst bilgisi alanında iletildi. Konak dizesi NULL olamaz.
- **host_length** Ana bilgisayar dize uzunluğu.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **username_length** Kimlik doğrulaması için kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **total_bytes** Gönderilen kaynağın toplam bayt sayısı. Sonraki nx_web_http_client_put_packet() çağrıları aracılığıyla gönderilen tüm paketlerin birleşik *uzunluğunun bu değere* eşit olması gerektiğini unutmayın.
- **tls_setup** TLS yapılandırmasını kurulumu için kullanılan geri çağırma. Uygulama, TLS şifrelemesi ve kimlik bilgilerini (örneğin sertifikalar) başlatmak için bu geri çağırmayı tanımlar.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Put isteği başarıyla gönderildi
- **NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için fazla büyük
- **NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP İstemcisi hazır değil
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Kaynağın toplam boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_packet"></a>nx_web_http_client_put_packet

Sonraki kaynak veri paketini gönder

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_put_packet(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, hem PUT hem de POST işlemleri için BIR sonraki kaynak içeriği paketini HTTP Sunucusuna göndermeye çalışır. Bu yordamın, gönderilen paketlerin birleşik uzunluğu önceki nx_web_http_client_put_start() veya *nx_web_http_client_post_start()* çağrısında (veya karşılık gelen güvenli sürümlerinde) belirtilen *"total_bytes"* ile eşit olana kadar tekrar tekrar çağrıl gerektiğini unutmayın.

Bu hizmet ayrıca HTTP (veya HTTPS) bağlantısı kurulurken sorun olması durumunda sunucudan gelen yanıtı da denetler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **packet_ptr** HTTP Sunucusuna gönderilecek kaynağın sonraki içeriğinin işaretçisi.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Http İstemci paketi başarıyla gönderildi.
- **NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP İstemcisi hazır değil
- **NX_WEB_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0x3000E) Sunucu hata kodu alındı**
- **NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000D) Geçersiz paket uzunluğu
- **NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Geçersiz ad ve/veya Parola
- **NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000F) Sunucusu PUT tamamlandıktan önce yanıt verir
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_INVALID_PACKET (0x12) Paketi TCP üst bilgisi için çok küçük
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send a 20-byte packet representing the content of the resource
    "/TEST.HTM" to the HTTP Server. */

status = nx_web_http_client_put_packet(&client_ptr, packet_ptr, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM has
    successfully been sent. */
```

## <a name="nx_web_http_client_request_chunked_set"></a>nx_web_http_client_request_chunked_set

HTTP (S) isteği için öbekli aktarım ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_request_chunked_set(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT chunk_size, NX_PACKET *packet_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce uzak ana bilgisayara yuva bağlantısını kuran *nx_web_http_client_connect()* veya *nx_web_http_client_secure_connect()* çağrısında belirtilen sunucuya özel bir HTTP(S) isteği göndermek için öbekli aktarım kodlaması kullanır.

> [!NOTE]
> Uygulama bir istek veri paketi göndermek için öbekli aktarım kodlaması kullanıyorsa, *nx_web_http_client_request_packet_allocate*() çağrısından sonra ve nx_web_http_client_reqeust_packet_send () çağrısından önce bu *hizmeti çağırmış* olması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **chunk_size** Sekizli aylarda öbek verisi boyutu.
- **packet_ptr** HTTP(S) istek veri paketi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Öbekli olarak ayarlayın.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTPS server. */

nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a PUT request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_PUT,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_TRUE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the PUT operation. */
nx_web_http_client_request_send(&my_client, 1000);

/* Create a new data packet request on the HTTP(S) client instance. */
nx_web_http_client_request_packet_allocate(&my_client,
    &my_packet,
    NX_WAIT_FOREVER);

/* Set the chunked transfer. */
status = nx_web_http_client_request_chunked_set(&my_client, 128, my_packet);

/* At this point, user can fill the data into my_packet. */
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet request to server. */
nx_web_http_client_request_packet_send(&my_client, my_packet,
    0, NX_WAIT_FOREVER);
```

## <a name="nx_web_http_client_request_header_add"></a>nx_web_http_client_request_header_add

Özel HTTP isteğine özel üst bilgi ekleme

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_request_header_add(
    NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *field_name, UINT name_length,
    CHAR *field_value, UINT value_length,
    UINT wait_option);
```

### <a name="description"></a>Description

Bu hizmet, n x_web_http_client_request_initialize() ile oluşturulan özel bir HTTP isteğine özel bir üst bilgi (alan adı ve *değer şeklinde) ekler.*

Bu hizmetin kullanımı, bir uygulamanın i isteğine herhangi bir sayıda özel üst bilgi eklemeye olanak sağlar. **Bu, belirli uygulamalara yönelik özelleştirilmiş HTTP isteklerine olanak sağlar.**

> [!NOTE]
> Kolaylık nx_web_http_client_ \* _start yöntemleri sağlanır. Bu işlevlerin hepsi http istekleri oluşturmak ve göndermek *için bu yordamı dahili olarak (nx_web_http_client_request_initialize())* kullanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **field_name** Alan adı dizesi (ör. "Content-Type").
- **name_length** Alan adı dizesinin bayt cinsinden uzunluğu.
- **field_value** Alan değeri dizesi ("application/octet-stream" gibi).
- **value_length** Değer dizesinin bayt cinsinden uzunluğu.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstekte üst bilgi başarıyla ekleme.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */

nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server
    by repeatedly calling *nx_web_http_client_response_body_get()*
    until the entire response is retrieved. */

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_initialize"></a>nx_web_http_client_request_initialize

Özel HTTP isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_request_initialize(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT method, CHAR *resource, CHAR *host,
    UINT input_size, UINT transfer_encoding_trunked,
    CHAR *username, CHAR *password, UINT wait_option);
```

### <a name="description"></a>Description

Bu hizmet özel bir HTTP isteği oluşturur ve bu isteği HTTP İstemcisi örneğiyle ilişkilendirmektedir. *Basit nx_web_http_client_get_start()* (PUT, POST ve bu API'nin ilişkili güvenli sürümleriyle birlikte) aksine, *nx_web_http_client_request_send()* hizmeti çağrılana kadar özel istek gönderilmez.

Bu hizmetin kullanılması, bir uygulamanın nx_web_http_client_request_header_add() hizmetini kullanarak i isteğine herhangi bir sayıda ***özel üst bilgi eklemeye olanak*** sağlar. Bu, belirli uygulamalara yönelik özelleştirilmiş HTTP isteklerine olanak sağlar.

> [!NOTE]
> Kolaylık nx_web_http_client_ \* _start yöntemleri sağlanır. Bu işlevlerin hepsi http istekleri oluşturmak ve göndermek *için bu yordamı dahili olarak (nx_web_http_client_request_send())* kullanır.

Bu hizmet kullanım dışıdır. Geliştiricilerin *nx_web_http_client_request_initialize_extended() kullanmaları teşvik edilecektir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **yöntem** Kullanmak için HTTP isteği yöntemi. Seçenekler aşağıdaki gibi tanımlanır:
  - **NX_WEB_HTTP_METHOD_NONE (0x0)**
  - **NX_WEB_HTTP_METHOD_GET (0x1)**
  - **NX_WEB_HTTP_METHOD_PUT (0x2)**
  - **NX_WEB_HTTP_METHOD_POST (0x3)**
  - **NX_WEB_HTTP_METHOD_DELETE (0x4)**
  - **NX_WEB_HTTP_METHOD_HEAD (0x5)**
- **kaynak** Aktarılan kaynağın adı.
- **konak** Sunucunun etki alanı adının null sonlandırıldı dizesi. Bu dize HTTP Ana Bilgisayar üst bilgisi alanında iletildi. Konak dizesi NULL olamaz.
- **input_size** PUT ve POST için giriş verileri boyutu. Diğer işlemler için 0 geçişi.
- **transfer_encoding_trunked** Gelecekteki gövdeli aktarım desteği için ayrılmış parametre.
- **kullanıcı adı** Korumalı kaynaklar için kullanıcı adı.
- **parola** Korumalı kaynaklar için parola.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İsteğin başarıyla başlatılama.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_WEB_HTTP_METHOD_ERROR (0x30014) Bazı gerekli bilgiler eksikti (put veya POST input_size gibi).

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */

status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get()* until the entire response is retrieved. */
get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_initialize_extended"></a>nx_web_http_client_request_initialize_extended

Özel HTTP isteği başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_request_initialize_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, UINT method,
    CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length,
    UINT input_size, UINT transfer_encoding_trunked,
    CHAR *username, UINT username_length,
    CHAR *password, UINT password_length, UINT wait_option);
```

### <a name="description"></a>Description

Bu hizmet özel bir HTTP isteği oluşturur ve bu isteği HTTP İstemcisi örneğiyle ilişkilendirmektedir. *Basit nx_web_http_client_get_start()* (PUT, POST ve bu API'nin ilişkili güvenli sürümleriyle birlikte) aksine, *nx_web_http_client_request_send()* hizmeti çağrılana kadar özel istek gönderilmez.

Bu hizmetin kullanılması, bir uygulamanın nx_web_http_client_request_header_add() hizmetini kullanarak i isteğine herhangi bir sayıda ***özel üst bilgi eklemeye olanak*** sağlar. Bu, belirli uygulamalara yönelik özelleştirilmiş HTTP isteklerine olanak sağlar.

> [!NOTE]
> Kolaylık nx_web_http_client_ \* _start yöntemleri sağlanır. Bu işlevlerin hepsi http istekleri oluşturmak ve göndermek *için bu yordamı dahili olarak (nx_web_http_client_request_send())* kullanır.

Kaynak, konak, kullanıcı adı ve parola dizeleri NULL olarak sonlandırılmalı ve her dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukta olmalıdır.

Bu hizmet, *nx_web_http_client_request_initialize*() değiştirir. Bu sürüm, çağıranların işleve uzunluk bilgileri teminsini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **yöntem** Kullanmak için HTTP isteği yöntemi. Seçenekler aşağıdaki gibi tanımlanır:
  - **NX_WEB_HTTP_METHOD_NONE (0x0)**
  - **NX_WEB_HTTP_METHOD_GET (0x1)**
  - **NX_WEB_HTTP_METHOD_PUT (0x2)**
  - **NX_WEB_HTTP_METHOD_POST (0x3)**
  - **NX_WEB_HTTP_METHOD_DELETE (0x4)**
  - **NX_WEB_HTTP_METHOD_HEAD (0x5)**
- **kaynak** Aktarılan kaynağın adı.
- **resource_length** İstenen kaynağın dize uzunluğu.
- **konak** Sunucunun etki alanı adının null sonlandırıldı dizesi. Bu dize HTTP Ana Bilgisayar üst bilgisi alanında iletildi. Konak dizesi NULL olamaz.
- **host_length** Ana bilgisayar dize uzunluğu.
- **input_size** PUT ve POST için giriş verileri boyutu. Diğer işlemler için 0 geçişi.
- **transfer_encoding_trunked** Gelecekteki gövdeli aktarım desteği için ayrılmış parametre.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **username_length** Kimlik doğrulaması için kullanıcı adının dize uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için parolanın dize uzunluğu.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İsteğin başarıyla başlatılama.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_WEB_HTTP_METHOD_ERROR (0x30014) Bazı gerekli bilgiler eksikti (put veya POST input_size gibi).

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize_extended(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "test.txt ", sizeof("test.txt ") – 1,
    "host.com", sizeof("host.com") – 1,
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    0,
    NX_NULL, /* password */
    0,
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);


/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get()* until the entire response is retrieved. */
get_status = NX_SUCCESS;
while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_packet_send"></a>nx_web_http_client_request_packet_send

HTTP(S) isteği veri paketini uzak sunucuya gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_request_packet_send(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET *packet_ptr, UINT more_date,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, *nx_web_http_client_request_packet_allocate* () ile oluşturulan özel bir HTTP(S) istek veri paketini daha önce uzak ana bilgisayara yuva bağlantısı kuran *nx_web_http_client_connect()* veya *nx_web_http_client_secure_connect()* çağrısında belirtilen sunucuya gönderir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **packet_ptr** HTTP(S) istek veri paketi işaretçisi.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstek veri paketinin başarılı bir şekilde göndermesi.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a PUT request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_PUT,
    "https://192.168.1.150/test.txt ", "host.com",
    128, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the PUT operation. */
nx_web_http_client_request_send(&my_client, 1000);

/* Create a new data packet request on the HTTP(S) client instance. */
nx_web_http_client_request_packet_allocate(&my_client,
    &my_packet,
    NX_WAIT_FOREVER);

/* At this point, user can fill the data into my_packet. */
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet request to server. */
status = nx_web_http_client_request_packet_send(&my_client,
    my_packet,
    0,
    NX_WAIT_FOREVER);
```

## <a name="nx_web_http_client_request_send"></a>nx_web_http_client_request_send

Özel HTTP isteği gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_request_send(NX_WEB_HTTP_CLIENT *client_ptr,
    UINT wait_option);
```

### <a name="description"></a>Description

Bu hizmet, *nx_web_http_client_request_initialize()* ile oluşturulan özel bir HTTP isteğini *nx_web_http_client_connect()* veya *nx_web_http_client_secure_connect()* içinde belirtilen sunucuya gönderir ve her ikisi de daha önce uzak ana bilgisayarla yuva bağlantısını kurarak bu isteklerden her ikisini de sağlar.

Bu hizmetin kullanılması, bir uygulamanın nx_web_http_client_request_header_add() hizmetini kullanarak i isteğine herhangi bir sayıda ***özel üst bilgi eklemeye olanak*** sağlar. Bu, belirli uygulamalara yönelik özelleştirilmiş HTTP isteklerine olanak sağlar.

> [!NOTE]
> Kolaylık nx_web_http_client_ \* _start yöntemleri sağlanır. Bu işlevlerin hepsi http istekleri oluşturmak ve göndermek *için bu yordamı dahili olarak (nx_web_http_client_request_initialize())* kullanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstek başarıyla gönderildi.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by
    repeatedly calling *nx_web_http_client_response_body_get* until
    the entire response is retrieved. */

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_response_body_get"></a>nx_web_http_client_response_body_get

Sonraki kaynak veri paketini alın

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_response_body_get(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET **packet_ptr, ULONG
    wait_option);
```

### <a name="description"></a>Description

Bu hizmet, önceki istek tarafından istenen kaynağın sonraki içerik paketini alır. Bu yordama yapılan başarılı çağrılar, uygulamanın dönüş durumu alınana NX_WEB_HTTP_GET_DONE gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **packet_ptr** Kısmi kaynak içeriği içeren paket işaretçisi için hedef.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) HTTP İstemci paketi başarıyla alındı.
- **NX_WEB_HTTP_GET_DONE** (0x3000C) HTTP İstemcisi get paketi bitti
- **NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP İstemcisi get modunda değil.
- **NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000D) Geçersiz paket uzunluğu
- **NX_WEB_HTTP_STATUS_CODE_CONTINUE** (0x3001A) HTTP durum kodu 100 Devam
- **NX_WEB_HTTP_STATUS_CODE_SWITCHING_PROTOCOLS** (0x3001B) HTTP durum kodu 101 Geçiş Protokolleri
- **NX_WEB_HTTP_STATUS_CODE_CREATED** (0x3001C) HTTP durum kodu 201 Oluşturuldu
- **NX_WEB_HTTP_STATUS_CODE_ACCEPTED** (0x3001D) HTTP durum kodu 202 Kabul Edildi
- **NX_WEB_HTTP_STATUS_CODE_NON_AUTH_INFO** (0x3001E) HTTP durum kodu 203 Yetkili Olmayan Bilgiler
- **NX_WEB_HTTP_STATUS_CODE_NO_CONTENT** (0x3001F) HTTP durum kodu 204 İçerik Yok
- **NX_WEB_HTTP_STATUS_CODE_RESET_CONTENT** (0x30020) HTTP durum kodu 205 İçeriği Sıfırla
- **NX_WEB_HTTP_STATUS_CODE_PARTIAL_CONTENT** (0x30021) HTTP durum kodu 206 Kısmi İçerik
- **NX_WEB_HTTP_STATUS_CODE_MULTIPLE_CHOICES** (0x30022) HTTP durum kodu 300 Birden Çok Seçenek
- **NX_WEB_HTTP_STATUS_CODE_MOVED_PERMANETLY** (0x30023) HTTP durum kodu 301 Kalıcı Olarak Taşındı
- **NX_WEB_HTTP_STATUS_CODE_FOUND** (0x30024) HTTP durum kodu 302 Bulundu
- **NX_WEB_HTTP_STATUS_CODE_SEE_OTHER** (0x30025) HTTP durum kodu 303 Bkz. Diğer
- **NX_WEB_HTTP_STATUS_CODE_NOT_MODIFIED** (0x30026) HTTP durum kodu 304 Değiştirilmedi
- **NX_WEB_HTTP_STATUS_CODE_USE_PROXY** (0x30027) HTTP durum kodu 305 Ara Sunucu Kullan
- **NX_WEB_HTTP_STATUS_CODE_TEMPORARY_REDIRECT** (0x30028) HTTP durum kodu 307 Geçici Yeniden Yönlendirme
- **NX_WEB_HTTP_STATUS_CODE_BAD_REQUEST** (0x30029) HTTP durum kodu 400 Hatalı İstek
- **NX_WEB_HTTP_STATUS_CODE_UNAUTHORIZED** (0x3002A) HTTP durum kodu 401 Yetkisiz
- **NX_WEB_HTTP_STATUS_CODE_PAYMENT_REQUIRED** (0x3002B) HTTP durum kodu 402 Ödeme Gerekiyor
- **NX_WEB_HTTP_STATUS_CODE_FORBIDDEN** (0x3002C) HTTP durum kodu 403 Yasak
- **NX_WEB_HTTP_STATUS_CODE_NOT_FOUND** (0x3002D) HTTP durum kodu 404 Bulunamadı
- **NX_WEB_HTTP_STATUS_CODE_METHOD_NOT_ALLOWED** (0x3002E) HTTP durum kodu 405 Yöntemine İzin Verilmiyor
- **NX_WEB_HTTP_STATUS_CODE_NOT_ACCEPTABLE** (0x3002F) HTTP durum kodu 406 Kabul Edilemez
- **NX_WEB_HTTP_STATUS_CODE_PROXY_AUTH_REQUIRED** (0x30030) HTTP durum kodu 407 Ara Sunucu Kimlik Doğrulaması Gerekiyor
- **NX_WEB_HTTP_STATUS_CODE_REQUEST_TIMEOUT** (0x30031) HTTP durum kodu 408 İstek Zaman Out
- **NX_WEB_HTTP_STATUS_CODE_CONFLICT** (0x30032) HTTP durum kodu 409 Çakışması
- **NX_WEB_HTTP_STATUS_CODE_GONE** (0x30033) HTTP durum kodu 410 Kayboldu
- **NX_WEB_HTTP_STATUS_CODE_LENGTH_REQUIRED** (0x30034) HTTP durum kodu 411 Uzunluğu Gerekiyor
- **NX_WEB_HTTP_STATUS_CODE_PRECONDITION_FAILED** (0x30035) HTTP durum kodu 412 Önkoşul Başarısız Oldu
- **NX_WEB_HTTP_STATUS_CODE_ENTITY_TOO_LARGE** (0x30036) HTTP durum kodu 413 İstek Varlığı Çok Büyük
- **NX_WEB_HTTP_STATUS_CODE_URL_TOO_LARGE** (0x30037) HTTP durum kodu 414 İstek URL'si Çok Büyük
- **NX_WEB_HTTP_STATUS_CODE_UNSUPPORTED_MEDIA** (0x30038) HTTP durum kodu 415 Desteklenmeyen Medya Türü
- **NX_WEB_HTTP_STATUS_CODE_RANGE_NOT_SATISFY** (0x30039) HTTP durum kodu 416 İstenen aralık doğrulanabilir değil
- **NX_WEB_HTTP_STATUS_CODE_EXPECTATION_FAILED** (0x3003A) HTTP durum kodu 417 Beklenti Başarısız Oldu
- **NX_WEB_HTTP_STATUS_CODE_INTERNAL_ERROR** (0x3003B) HTTP durum kodu 500 İç Sunucu Hatası
- **NX_WEB_HTTP_STATUS_CODE_NOT_IMPLEMENTED** (0x3003C) HTTP durum kodu 501 Uygulanmadı
- **NX_WEB_HTTP_STATUS_CODE_BAD_GATEWAY** (0x3003D) HTTP durum kodu 502 Hatalı Ağ Geçidi
- **NX_WEB_HTTP_STATUS_CODE_SERVICE_UNAVAILABLE** (0x3003E) HTTP durum kodu 503 Hizmet Kullanılamıyor
- **NX_WEB_HTTP_STATUS_CODE_GATEWAY_TIMEOUT** (0x3003F) HTTP durum kodu 504 Ağ Geçidi Zaman Out
- **NX_WEB_HTTP_STATUS_CODE_VERSION_ERROR** (0x30040) HTTP durum kodu 505 HTTP Sürümü desteklenmiyor
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Get the next packet of resource content on the HTTP Client "my_client."
    Note that the nx_web_http_client_get_start() routine must have been called
    previously. */
status = nx_web_http_client_response_body_get(&my_client, &next_packet, 1000);

/* If status is NX_SUCCESS, the next packet of content is pointed to
    by "next_packet". */
```

## <a name="nx_web_http_client_response_header_callback_set"></a>nx_web_http_client_response_header_callback_set

HTTP üst bilgileri işleme sırasında çağırmak için geri çağırmayı ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_response_header_callback_set(
    NX_WEB_HTTP_CLIENT *client_ptr,
    VOID (*callback_function)(NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *field_name, UINT field_name_length,
    CHAR *field_value, UINT field_value_length));
```

### <a name="description"></a>Description

Bu hizmet, NetX Web HTTP İstemcisi uzak bir HTTP sunucusundan gelen yanıtta bir HTTP üst bilgisi işlemesi sırasında çağrılan bir geri çağırma atar. Yanıtta işlenen her üst bilgi için geri çağırma bir kez çağrılır. Geri çağırma, bir HTTP İstemcisi uygulamasının, NetX Web HTTP İstemcisi'nin yaptığı temel işlemenin ötesinde istenen eylemleri yapmak için HTTP sunucusu yanıtını kullanan üst bilgilere erişmesini sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

**client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.

**callback_function** Yanıt üst bilgisi işleme sırasında çağrılan geri çağırma. Geri çağırma, alan adı ve değeri dize (ve uzunlukları) olarak çağrılır. Örneğin, "Content-Length: 100" üst bilgisi, *işlevin field_name* için "Content-Length" ile ve field_value için "100" dizesiyle çağrılmalarını *sağlar.*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Geri çağırma başarılı ataması.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Setup a callback to print out header information as it is processed. */
VOID http_response_callback(NX_WEB_HTTP_CLIENT *client_ptr, CHAR *field_name,
    UINT field_name_length, CHAR *field_value,
    UINT field_value_length)
{
    CHAR name[100];
    CHAR value[100];
    memset(name, 0, sizeof(name));

    memset(value, 0, sizeof(value));

    strncpy(name, field_name, field_name_length);
    strncpy(value, field_value, field_value_length);

    printf("Received header: \n");
    printf("\tField name: %s (%d bytes)\n", name, field_name_length);
    printf("\tValue: %s (%d bytes)\n\n", value, field_value_length);
}

/* Assign the callback to the HTTP client instance. */
nx_web_http_client_response_header_callback_set(&my_client,
    http_response_callback);

/* Start a GET operation to get a response from the HTTP server. */
status = nx_web_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "myname", "mypassword", 1000);

/* When the HTTP server returns a response to the GET request, NetX Web HTTP
    Client will invoke the http_response_callback function for each header
    processed in the HTTP response. */
```

## <a name="nx_web_http_client_secure_connect"></a>nx_web_http_client_secure_connect

Özel istekler için BIR HTTPS sunucusuna TLS oturumu açma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_client_secure_connect(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls),
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu yöntem **TLS ile güvenli HTTPS'ye** göredir.

Bu hizmet, bir HTTPS sunucusuna güvenli bir TLS oturumu açar ancak herhangi bir istek göndermez. İstekler n *x_web_http_client_request_initialize() ile oluşturulur* ve *nx_web_http_client_request_send() kullanılarak gönderilir.* özel HTTP üst bilgileri *nx_web_http_client_request_header_add() kullanılarak i nx_web_http_client_request_header_add eklenebilir.*

Bu hizmetin kullanımı, bir uygulamanın i isteğine herhangi bir sayıda özel üst bilgi eklemeye olanak sağlar. **Bu, belirli uygulamalara yönelik özelleştirilmiş HTTP isteklerine olanak sağlar.**

> [!NOTE]
> Kolaylık nx_web_http_client_ \* _start yöntemleri sağlanır. Bu işlevlerin hepsi http istekleri oluşturmak ve göndermek *için bu yordamı dahili olarak (nx_web_http_client_request_initialize())* kullanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **server_ip** Uzak HTTPS sunucusunun IP adresi.
- **server_port** Uzak HTTPS sunucusunda bağlantı noktası (örneğin, HTTPS için 443).
- **tls_setup** TLS yapılandırmasını kurulumu için kullanılan geri çağırma. Uygulama, TLS şifrelemesi ve kimlik bilgilerini (örneğin sertifikalar) başlatmak için bu geri çağırmayı tanımlar.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 0xFFFFFFFE) Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
  - **NX_WAIT_FOREVER** (0xFFFFFFFF) NX_WAIT_FOREVER, HTTP Sunucusu itene yanıt verene kadar çağrı iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) TLS oturumunun başarılı bağlantısı.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_WEB_HTTP_NOT_READY (0x3000A) Başka bir istek zaten devam ediyor.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Connect to a remote HTTPS server. */
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

nx_web_http_client_secure_connect(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get* until the entire response is retrieved. */

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);
    /* Process response packets… */
}
```

## <a name="http-and-https-server-api"></a>HTTP ve HTTPS Sunucusu API'si

## <a name="nx_web_http_server_cache_info_callback_set"></a>nx_web_http_server_cache_info_callback_set

En fazla yaş ve tarih URL'sini almak için geri çağırmayı ayarlayın

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_cache_info_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT (*cache_info_get)(CHAR *resource,
    UINT *max_age,
    NX_WEB_HTTP_SERVER_DATE *date));
```

### <a name="description"></a>Description

Bu hizmet, belirtilen kaynağın en uzun yaş ve son değiştirme tarihini almak için çağrılan geri çağırma hizmetini ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **cache_info_get** Geri çağırma işaretçisi
- **max_age** Bir kaynağın yaş üst sınırı işaretçisi
- **veriler** Döndürülen son değiştirme tarihini gösteren işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Geri çağırmayı başarıyla ayarlama
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

Başlatma

### <a name="example"></a>Örnek

```C
NX_WEB_HTTP_SERVER my_server;

UINT cache_info_get(CHAR *resource, UINT *max_age,
    NX_WEB_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_web_http_server_create and before the HTTP
    server is set by nx_web_http_server_start(), set the cache info callback: */
status = nx_web_http_server_cache_info_callback_set(&my_server, cache_info_get);

/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_web_http_server_callback_data_send"></a>nx_web_http_server_callback_data_send

Geri çağırma işlevinden veri gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_callback_data_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID *data_ptr, ULONG data_length);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan pakette yer alan verileri uygulamanın geri çağırma yordamından gönderir. Bu genellikle GET/POST istekleriyle ilişkili dinamik verileri göndermek için kullanılır. Bu işlev kullanılırsa, yanıtın tamamının düzgün biçimde gönderilmesi geri çağırma yordamının sorumluluğundadır. Buna ek olarak, geri çağırma yordamı, geri çağırma yordamının NX_WEB_HTTP_CALLBACK_COMPLETED.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **data_ptr** Gönderilen verilerin işaretçisi.
- **data_length** Gönderilen bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sunucu verileri başarıyla gönderildi
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* Found it, override the GET processing by sending the resource
            contents directly. */
        nx_web_http_server_callback_data_send(server_ptr,
            "HTTP/1.0 200 \r\nContent-Length:" "103\r\nContent-Type: text/html\r\n\r\n",
            63);

        nx_web_http_server_callback_data_send(server_ptr, "<HTML>\r\n<HEAD><TITLE>NetX"
            "HTTP Test </TITLE></HEAD>\r\n"
            :<BODY>\r\n<H1>NetX Test Page"
            "</H1>\r\n</BODY>\r\n</HTML>\r\n", 103);

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_callback_generate_response_header"></a>nx_web_http_server_callback_generate_response_header

Geri çağırma işlevinde yanıt üst bilgisi oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_callback_generate_response_header(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    CHAR *status_code, UINT content_length,
    CHAR *content_type, CHAR* additional_header);
```

### <a name="description"></a>Description

Bu hizmet HTTP yanıt üst bilgisi oluşturmak için HTTP (S) sunucu geri çağırma yordamında (uygulama tarafından tanımlanır) kullanılır. HTTP sunucusu, HTTP yanıtı gerektiren İstemci GET, PUT ve DELETE isteklerine yanıt verdiği zaman sunucu geri çağırma yordamı çağrılır. Bu işlev, uygulamanın yanıt bilgilerini alır ve uygun yanıt üst bilgisini üretir. Sunucu isteği geri çağırma yordamı hakkında daha fazla bilgi için bkz. service *nx_web_http_server_create()* .

Bu API kullanım dışıdır. Geliştiricilerin *nx_web_http_server_callback_generate_response_header_extended() kullanmaları teşvik edilecektir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi
- **status_code** Kaynağın durumunu gösterir. Örnekler:
  - **NX_WEB_HTTP_STATUS_OK**
  - **NX_WEB_HTTP_STATUS_MODIFIED**
  - **NX_WEB_HTTP_STATUS_INTERNAL_ERROR**
- **content_length** İçeriğin bayt cinsinden boyutu
- **content_type** HTTP türü ( "text/plain" gibi)
- **additional_header** Ek üst bilgi metni işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Html üst bilgisi başarıyla oluşturuldu
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
CHAR demotestbuffer[] = "<html>> r\n\r\n<head>> r\n\r\n<title>Main \
    Window</title>> r\n</head>> r\n\r\n<body>Test message\r\n \ </body>> r\n</html>> r\n";

/* my_request_notify* is the application request notify callback registered
    with the HTTP server in *nx_web_http_server_create*,
    creates a response to the received Client request. */

UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET *resp_packet_ptr;
    ULONG string_length;
    CHAR temp_string[30];
    ULONG length = 0;
    length = strlen(&demotestbuffer[0]);

    /* Derive the client request type from the client request. */
    nx_web_http_server_type_extract(server_ptr,
        server_ptr -> nx_web_http_server_request_resource,
        temp_string, sizeof(temp_string), &string_length);

    /* Null terminate the string. */
    temp_string[string_length] = 0;

    /* Now build a response header with server status is OK and no additional header info. */
    status = nx_web_http_server_callback_generate_response_header(http_server_ptr,
        &resp_packet_ptr, NX_WEB_HTTP_STATUS_OK,
        length, temp_string, NX_NULL);

    /* If status is NX_SUCCESS, the header was successfully appended. */

    /* Now add data to the packet. */
    status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
        strlen(&demotestbuffer[0]), server_ptr >>
        nx_web_http_server_packet_pool_ptr, NX_WAIT_FOREVER);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Now send the packet! */
    status = nx_web_http_server_callback_packet_send(
        &(server_ptr -> nx_web_http_server_socket),
        resp_packet_ptr);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Let HTTP server know the response has been sent. */
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);
}
```

## <a name="nx_web_http_server_callback_generate_response_header_extended"></a>nx_web_http_server_callback_generate_response_header_extended

Geri çağırma işlevinde yanıt üst bilgisi oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_callback_generate_response_header_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    CHAR *status_code, UINT status_code_length,
    UINT content_length, CHAR *content_type,
    UINT content_type_length,
    CHAR* additional_header,
    UINT additional_header_length);
```

### <a name="description"></a>Description

Bu hizmet HTTP yanıt üst bilgisi oluşturmak için HTTP (S) sunucu geri çağırma yordamında (uygulama tarafından tanımlanır) kullanılır. HTTP sunucusu, HTTP yanıtı gerektiren İstemci GET, PUT ve DELETE isteklerine yanıt verdiği zaman sunucu geri çağırma yordamı çağrılır. Bu işlev, uygulamanın yanıt bilgilerini alır ve uygun yanıt üst bilgisini üretir. Sunucu isteği geri çağırma yordamı hakkında daha fazla bilgi için bkz. service *nx_web_http_server_create()* .

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi
- **status_code** Kaynağın durumunu gösterir. Örnekler:
  - **NX_WEB_HTTP_STATUS_OK**
  - **NX_WEB_HTTP_STATUS_MODIFIED**
  - **NX_WEB_HTTP_STATUS_INTERNAL_ERROR**
- **status_code_length** Durum kodunun dize uzunluğu
- **content_length** İçeriğin bayt cinsinden boyutu
- **content_type** HTTP türü ( "text/plain" gibi)
- **content_type_length** İçerik türünün dize uzunluğu
- **additional_header** Ek üst bilgi metni işaretçisi
- **additional_header_length** Ek üst bilgi metninin uzunluğu

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Html üst bilgisi başarıyla oluşturuldu
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
CHAR demotestbuffer[] = "<html>> r\n\r\n<head>> r\n\r\n<title>Main \
    Window</title>> r\n</head>> r\n\r\n<body>Test message\r\n \ </body>> r\n</html>> r\n";

/* my_request_notify* is the application request notify callback
    registered with the HTTP server in *nx_web_http_server_create*,
    creates a response to the received Client request. */

UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET *resp_packet_ptr;
    ULONG string_length;
    CHAR temp_string[30];
    ULONG length = 0;
    length = strlen(&demotestbuffer[0]);

    /* Derive the client request type from the client request. */
    nx_web_http_server_type_extract(server_ptr,
        server_ptr -> nx_web_http_server_request_resource,
        temp_string, sizeof(temp_string), &string_length);

    /* Null terminate the string. */
    temp_string[string_length] = 0;

    /* Now build a response header with server status is OK and no additional header info. */
    status = nx_web_http_server_callback_generate_response_header_extended(http_server_ptr,
        &resp_packet_ptr, NX_WEB_HTTP_STATUS_OK,
        sizeof(NX_WEB_HTTP_STATUS_OK) – 1,
        length, temp_string, string_length NX_NULL, 0);

    /* If status is NX_SUCCESS, the header was successfully appended. */

    /* Now add data to the packet. */
    status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
        strlen(&demotestbuffer[0]), server_ptr >>
        nx_web_http_server_packet_pool_ptr, NX_WAIT_FOREVER);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Now send the packet! */
    status = nx_web_http_server_callback_packet_send(
        &(server_ptr -> nx_web_http_server_socket),
        resp_packet_ptr);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Let HTTP server know the response has been sent. */
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);

}
```

## <a name="nx_web_http_server_callback_packet_send"></a>nx_web_http_server_callback_packet_send

Geri çağırma işlevinden HTTP paketi gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_callback_packet_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr);
```

### <a name="description"></a>Description

Bu hizmet, bir HTTP geri çağırmadan tam bir HTTP sunucusu yanıtı gönderir. HTTP sunucusu paketi NX_WEB_HTTP_SERVER _TIMEOUT_SEND. HTTP üst bilgisi ve verileri pakete ek gerekir. Dönüş durumu bir hata gösteriyorsa, HTTP uygulamasının paketi serbest bırakması gerekir.

Geri çağırma, geri çağırmayı NX_WEB_HTTP_CALLBACK_COMPLETED.

Daha ayrıntılı nx_web_http_server_callback_generate_response_header için bkz. *nx_web_http_server_callback_generate_response_header()* .

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi
- **packet_ptr** Göndermek için paket işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Http Sunucusu paketi başarıyla gönderildi
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* The packet is appended with HTTP header and data
    and is ready to send to the Client directly. */
status = nx_web_http_server_callback_packet_send(server_ptr, packet_ptr);

if (status != NX_SUCCESS)
{
    nx_packet_release(packet_ptr);
}

return(NX_WEB_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_web_http_server_callback_response_send"></a>nx_web_http_server_callback_response_send

Geri çağırma işlevinden yanıt gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_callback_response_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    CHAR *header,
    CHAR *information,
    CHAR additional_info);
```

### <a name="description"></a>Description

Bu hizmet, uygulamanın geri çağırma yordamından sağlanan yanıt bilgilerini gönderir. Bu genellikle GET/POST istekleriyle ilişkili özel yanıtlar göndermek için kullanılır. Bu işlev kullanılırsa, geri çağırma yordamının NX_WEB_HTTP_CALLBACK_COMPLETED.

Bu hizmet kullanım dışıdır. Geliştiricilerin *nx_web_http_server_callback_response_send_extended() kullanmaları teşvik edilecektir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.
- **bilgi** Bilgi dizesinin işaretçisi.
- **additional_info** Ek bilgi dizesinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) HTTP Sunucusu yanıtı başarıyla gönderildi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
            a resource not found response. */
        nx_web_http_server_callback_response_send(server_ptr,
            "HTTP/1.0 404 ",
            "NetX HTTP Server unable to find file: ",
            resource);

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_callback_response_send_extended"></a>nx_web_http_server_callback_response_send_extended

Geri çağırma işlevinden yanıt gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_callback_response_send_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    CHAR *header, UINT header_length,
    CHAR *information,
    UINT information_length,
    CHAR additional_info,
    UINT additional_info_length);
```

### <a name="description"></a>Description

Bu hizmet, uygulamanın geri çağırma yordamından sağlanan yanıt bilgilerini gönderir. Bu genellikle GET/POST istekleriyle ilişkili özel yanıtlar göndermek için kullanılır. Bu işlev kullanılırsa, geri çağırma yordamının NX_WEB_HTTP_CALLBACK_COMPLETED.

Üst bilgi, bilgi ve additional_info dizeleri NULL olarak sonlandırılmalı ve her dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukta olmalıdır.

Bu hizmet, *nx_web_http_server_callback_response_send*() değiştirir. Bu sürüm, çağıranların işleve uzunluk bilgileri teminsini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.
- **header_length** Yanıt üst bilgisi dizesinin uzunluğu.
- **bilgi** Bilgi dizesinin işaretçisi.
- **Information_length** Bilgi dizesinin uzunluğu.
- **additional_info** Ek bilgi dizesinin işaretçisi.
- **additional_info_length** Ek bilgi dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) HTTP Sunucusu yanıtı başarıyla gönderildi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
            a resource not found response. */
        nx_web_http_server_callback_response_send_extended(server_ptr,
            "HTTP/1.0 404 ",
            sizeof("HTTP/1.0 404 ") – 1,
            "NetX HTTP Server unable to find file: ",
            sizeof("NetX HTTP Server unable to find file: ") – 1,
            resource, strlen(resource));

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_content_get"></a>nx_web_http_server_content_get

İstekten içerik al

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_content_get(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr,
    ULONG byte_offset,
    CHAR *destination_ptr,
    UINT destination_size,
    UINT *actual_size);
```

### <a name="description"></a>Description

Bu hizmet, POST veya PUT HTTP İstemcisi isteğinden belirtilen miktarda içeriği almaya çalışır. Http Sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağırmadan çağrılmalı (*nx_web_http_server_create()*).

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **packet_ptr** HTTP İstemcisi istek paketinin işaretçisi. Bu paketin istek bildirim geri çağırma tarafından serbest bırakması gerektiğini unutmayın.
- **byte_offset** İçerik alanına uzaklığı yapılan bayt sayısı.
- **destination_ptr** İçerik için hedef alana işaretçi.
- **destination_size** Hedef alanda kullanılabilen maksimum bayt sayısı.
- **actual_size** Kopyalanan içeriğin gerçek boyutuna ayarilecek hedef değişkenin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı HTTP Sunucusu içeriği Al
- **NX_WEB_HTTP_ERROR** (0x30000) HTTP Sunucusu iç hatası
- **NX_WEB_HTTP_DATA_END** (0x30007) İstek içeriği sonu
- **NX_WEB_HTTP_TIMEOUT** paketi 0x30001 http sunucusu zaman aşımına (veya zaman aşımına) neden oluyor
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Assuming we are in the application’s request notify callback
    routine, retrieve up to 100 bytes of content starting at offset
    0. */
status = nx_web_http_server_content_get(&my_server, packet_ptr,
    0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, "my_buffer" contains "actual_size" bytes of
    request content. */
```

## <a name="nx_web_http_server_content_get_extended"></a>nx_web_http_server_content_get_extended

İstekten içerik al/sıfır uzunluğunu destekler İçerik Uzunluğu

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_content_get_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr,
    ULONG byte_offset,
    CHAR *destination_ptr,
    UINT destination_size,
    UINT *actual_size);
```

### <a name="description"></a>Description

Bu hizmet, *nx_web_http_server_content_get() ile neredeyse aynıdır;* POST veya PUT HTTP İstemcisi isteğinden belirtilen miktarda içeriği almaya çalışır. Ancak, İçerik Uzunluğu sıfır değere ('boş istek') sahip istekleri geçerli bir istek olarak işler. Http Sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağırmadan çağrılmalı (*nx_web_http_server_create()*).

Bu hizmet , *() nx_web_http_server_content_get* değiştirir. Bu sürüm, çağıranların işleve uzunluk bilgileri teminsini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **packet_ptr** HTTP İstemcisi istek paketinin işaretçisi. Bu paketin istek bildirim geri çağırma tarafından serbest bırakması gerektiğini unutmayın.
- **byte_offset** İçerik alanına uzaklığı yapılan bayt sayısı.
- **destination_ptr** İçerik için hedef alana işaretçi.
- **destination_size** Hedef alanda kullanılabilen maksimum bayt sayısı.
- **actual_size** Kopyalanan içeriğin gerçek boyutuna ayarilecek hedef değişkenin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı HTTP içeriği get
- **NX_WEB_HTTP_ERROR** (0x30000) HTTP Sunucusu iç hatası
- **NX_WEB_HTTP_DATA_END** (0x30007) İstek içeriği sonu
- **NX_WEB_HTTP_TIMEOUT** paketi 0x30001 http sunucusu zaman aşımına (genel)
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Assuming we are in the application’s request notify callback
    routine, retrieve up to 100 bytes of content starting at offset
    0. */
status = nx_web_http_server_content_get_extended(&my_server, packet_ptr,
    0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, "my_buffer" contains "actual_size" bytes of
    request content. */
```

## <a name="nx_web_http_server_content_length_get"></a>nx_web_http_server_content_length_get

İstekte içeriğin uzunluğunu al/İçerik Uzunluğunu sıfır değeriyle destekler

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_content_length_get(
    NX_PACKET *packet_ptr,
    UINT *content_length);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan pakette HTTP içerik uzunluğunu almaya çalışır. Dönüş değeri başarılı tamamlanma durumunu gösterir ve giriş işaretçisinde gerçek uzunluk değeri content_length. HTTP içeriği/İçerik Uzunluğu = 0 yoksa, bu yordam yine de başarılı bir tamamlanma durumu döndürür ve content_length giriş işaretçisi geçerli bir uzunluğu (sıfır) işaret eder. Http Sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağırmadan çağrılmalı (*nx_web_http_server_create()*).

### <a name="input-parameters"></a>Giriş Parametreleri

- **packet_ptr** HTTP İstemcisi istek paketinin işaretçisi. Bu paketin istek bildirim geri çağırma tarafından serbest bırakması gerektiğini unutmayın.
- **content_length** İçerik Uzunluğu alanından alınan değer işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı HTTP Sunucusu İçerik Uzunluğu Al
- **NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000F) Hatalı HTTP üst bilgisi biçimi
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Assuming we are in the application’s request notify callback
    routine, get the content length of the HTTP Client request. */

ULONG content_length;
status = nx_web_http_server_content_length_get(packet_ptr, &content_length);

/* If the "status" variable indicates successful completion, the "length"
    Variable contains the length of the HTTP Client request content area. */
```

## <a name="nx_web_http_server_create"></a>nx_web_http_server_create

HTTP sunucusu örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_create(NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *http_server_name, NX_IP *ip_ptr, UINT server_port,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*authentication_check)(NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type, CHAR *resource, CHAR **name,
        CHAR **password, CHAR **realm),
    UINT (*request_notify)(NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type, CHAR *resource, NX_PACKET *packet_ptr));
```

### <a name="description"></a>Description

Bu hizmet kendi ThreadX iş parçacığı bağlamında çalışan bir HTTP sunucu örneği oluşturur. İsteğe bağlı *authentication_check* ve *request_notify* uygulama GERI çağırma yordamları, HTTP sunucusunun temel işlemleri üzerinde uygulama yazılım denetimi sağlar.

Bu hizmet, hem düz metin HTTP sunucuları hem de TLS ile güvenli HTTPS sunucuları oluşturmak için kullanılır. TLS kullanarak HTTPS 'yi etkinleştirmek için *nx_web_http_server_secure_configure ()* hizmetine bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **http_server_ptr** HTTP sunucu denetim bloğu işaretçisi.
- **http_server_name** HTTP sunucusu adı işaretçisi.
- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **SERVER_PORT** Sunucu örneği için TCP dinleme bağlantı noktası.
- **media_ptr** Daha önce oluşturulan FileX medya örneğine yönelik işaretçi.
- **stack_ptr** HTTP sunucusu iş parçacığı yığın alanı işaretçisi.
- **stack_size** HTTP sunucusu iş parçacığı yığın boyutu işaretçisi.
- **authentication_check** Uygulamanın kimlik doğrulama denetimi yordamına yönelik işlev işaretçisi. Belirtilmişse, bu yordam her HTTP Istemci isteği için çağırılır. Bu parametre NULL ise, kimlik doğrulaması gerçekleştirilmez. Bu parametre kullanım dışıdır. Bunun yerine *nx_web_http_server_authenticate_check_set*() çağırın.
- **request_notify** Uygulamanın istek bildirim yordamına yönelik işlev işaretçisi. Belirtilmişse, bu yordam isteğin HTTP sunucu işlemeden önce çağırılır. Bu, HTTP Istemci isteği tamamlanmadan önce kaynak adının yeniden yönlendirilmesine veya bir kaynak içindeki alanların güncelleştirilmesini sağlar.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı http sunucusu oluşturma.
- NX_PTR_ERROR (0x07) geçersiz HTTP sunucusu, IP, medya, yığın veya paket havuzu işaretçisi.
- NX_WEB_HTTP_POOL_ERROR (0x30009) havuzun paket yükü, tüm HTTP isteklerini içerecek kadar büyük değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Create an HTTP Server instance called "my_server." */
status = nx_web_http_server_create(&my_server, "my server", &ip_0,
    NX_WEB_HTTPS_SERVER_PORT, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_web_http_server_delete"></a>nx_web_http_server_delete

HTTP sunucusu örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_delete(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir HTTP sunucusu örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **http_server_ptr** HTTP sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı http sunucusu silme
- NX_PTR_ERROR (0x07) geçersiz HTTP sunucusu işaretçisi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete the HTTP Server instance called "my_server." */
status = nx_web_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_web_http_server_get_entity_content"></a>nx_web_http_server_get_entity_content

Varlık verilerinin konumunu ve uzunluğunu alma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_get_entity_content(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    ULONG *available_offset,
    ULONG *available_length);
```

### <a name="description"></a>Description

Bu hizmet, alınan Istemci iletilerindeki geçerli çok parçalı varlıktaki verilerin başlangıç konumunu ve sınır dizesini dahil olmayan veri uzunluğunu belirler. Dahili olarak, HTTP sunucusu, bu işlevin birden çok varlık içeren iletiler için aynı Istemci veri biriminde tekrar çağrılabilmesi için kendi uzaklıklarını güncelleştirir. Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.

Bu hizmeti kullanmak için NX_WEB_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerektiğini unutmayın. Ayrıca, uygulamanın packet_pptr tarafından işaret edilen paketi serbest bırakmadığını unutmayın. Bu, HTTP sunucusu tarafından dahili olarak yapılır.

Daha fazla ayrıntı için bkz. *nx_web_http_server_get_entity_header ()* .

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP sunucusu işaretçisi
- **packet_pptr** Paket işaretçisinin konumu işaretçisi. Uygulamanın bu paketi serbest bırakmadığını unutmayın
- **available_offset** Paket önüne işaretçisinden varlık verilerinin uzaklığa yönelik işaretçi
- **available_length** Varlık verisi uzunluğu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) varlık içeriğinin boyutunu ve konumunu başarıyla aldı
- HTTP sunucusu iç parçalı işaretçiler için **NX_WEB_HTTP_BOUNDARY_ALREADY_FOUND** (0x30016) içeriği zaten var
- NX_WEB_HTTP_ERROR (0x30000) HTTP sunucusu iç hatası
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_WEB_HTTP_SERVER my_server;
UINT offset, length;
NX_PACKET *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
    the entity header to determine details about the multipart data. If
    successful, it then calls this service to get the location of entity data: */
status = nx_web_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
    &length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
    entity data. */
```

## <a name="nx_web_http_server_get_entity_header"></a>nx_web_http_server_get_entity_header

Varlık üstbilgisinin içeriğini alma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_get_entity_header(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    UCHAR *entity_header_buffer,
    ULONG buffer_size);
```

### <a name="description"></a>Description

Bu hizmet varlık üstbilgisini belirtilen arabelleğe alır. Dahili HTTP sunucusu, birden çok varlık üst bilgilerine sahip bir Istemci veri biriminde bir sonraki çok parçalı varlığı bulmak için kendi işaretçilerini güncelleştirir. Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.

Bu hizmeti kullanmak için NX_WEB_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerektiğini unutmayın. Ayrıca, uygulamanın packet_pptr tarafından işaret edilen paketi serbest bırakmadığını unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP sunucusu işaretçisi
- **packet_pptr** Paket işaretçisinin konumu işaretçisi. Uygulamanın bu paketi serbest bırakmadığını unutmayın
- **entity_header_buffer** Varlık üstbilgisinin depolanacak konuma işaretçi
- **Buffer_size** Giriş arabelleğinin boyutu

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) varlık üstbilgisi başarıyla alındı
- **NX_WEB_HTTP_NOT_FOUND** (0x30006) varlık üst bilgisi alanı bulunamadı
- **NX_WEB_HTTP_TIMEOUT** (0x30001) çok paket istemci iletisi için sonraki paketi almak üzere zaman aşımına uğradı
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı
- NX_WEB_HTTP_ERROR (0x30000) Iç HTTP hatası

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Buffer to hold data we are extracting from the request. */
UCHAR buffer[1440];

/* *my_request_notify()* is the application request notify callback
    registered with the HTTP server in *nx_web_http_server_create()*,
    creates a response to the received Client request. */
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    UINT offset, length;
    NX_PACKET *response_pkt;

    /* Process multipart data. */
    if(request_type == NX_WEB_HTTP_SERVER_POST_REQUEST)
    {
        /* Get the content header. */
        while(nx_web_http_server_get_entity_header(server_ptr, &packet_ptr, buffer,
            sizeof(buffer)) == NX_SUCCESS)
        {
            /* Header obtained successfully. Get the content data location. */
            while(nx_web_http_server_get_entity_content(server_ptr,
                &packet_ptr, &offset, &length) == NX_SUCCESS)
            {
                /* Write content data to buffer. */
                nx_packet_data_extract_offset(packet_ptr, offset, buffer, length,
                    &length);
                buffer[length] = 0;
            }
        }

        /* Generate HTTP header. */
        status = nx_web_http_server_callback_generate_response_header(server_ptr,
            &response_pkt, NX_WEB_HTTP_STATUS_OK, 800, "text/html",
            "Server: NetX WEB HTTP 5.10\r\n");

        if(status == NX_SUCCESS)
        {
            if(nx_web_http_server_callback_packet_send(server_ptr, response_pkt) !=
                NX_SUCCESS)
            {
                nx_packet_release(response_pkt);
            }
        }
    }
    else
    {
        /* Indicate we have not processed the response to client yet.*/
        return(NX_SUCCESS);
    }

    /* Indicate the response to client is transmitted. */
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);
}

```

## <a name="nx_web_http_server_gmt_callback_set"></a>nx_web_http_server_gmt_callback_set

GMT Tarih ve saati almak için geri aramayı ayarlayın

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_gmt_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID (*gmt_get)(NX_WEB_HTTP_SERVER_DATE *date);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir HTTP sunucusu ile GMT Tarih ve saati alacak şekilde geri aramayı ayarlar. Bu hizmet HTTP sunucusu, Istemciye HTTP sunucu yanıtlarında bir üst bilgi oluşturuyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP sunucusu işaretçisi
- **gmt_get** GMT geri çağırması işaretçisi
- **Tarih** Alınan tarihin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
- NX_PTR_ERROR (0x07) geçersiz paket veya parametre işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_WEB_HTTP_SERVER my_server;

VOID get_gmt(NX_WEB_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_web_http_server_create(),
    and before starting HTTP services when nx_web_http_server_start() is called,
    set the GMT retrieve callback: */
status = nx_web_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
    response header date. */
```

## <a name="nx_web_http_server_invalid_userpassword_notify_set"></a>nx_web_http_server_invalid_userpassword_notify_set

Geçersiz Kullanıcı/parola işlemek için geri çağırma ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_invalid_userpassword_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*invalid_username_password_callback)
        (CHAR *resource,
        ULONG client_address,
        UINT request_type));
```

### <a name="description"></a>Description

Bu hizmet, bir Istemci alma, yerleştirme veya silme isteğinde, Özet veya temel kimlik doğrulamasından göre geçersiz bir Kullanıcı adı ve parola alındığında çağrılan geri aramayı ayarlar. HTTP sunucusu daha önce oluşturulmuş olmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP sunucusu işaretçisi
- **invalid_username_password_callback** Geçersiz Kullanıcı/geçiş geri çağırması işaretçisi
- **kaynak** İstemci tarafından belirtilen kaynak işaretçisi
- **client_address** İstemci adresi
- **request_type** İstemci isteği türünü gösterir. Belki:
  - *NX_WEB_HTTP_SERVER_GET_REQUEST*
  - *NX_WEB_HTTP_SERVER_POST_REQUEST NX_WEB_HTTP_SERVER_HEAD_REQUEST*
  - *NX_WEB_HTTP_SERVER_PUT_REQUEST NX_WEB_HTTP_SERVER_DELETE_REQUEST*

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
NX_WEB_HTTP_SERVER my_server;

VOID invalid_username_password_callback(NX_CHAR *resource,
    ULONG client_address,
    UINT request_type);

/* After the HTTP server is created by calling nx_web_http_server_create,
    and before starting HTTP services when nx_web_http_server_start() is called,
    set the invalid username password callback: */

status = nx_web_http_server_invalid_userpassword_notify_set( (&my_server,
    invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
    will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_web_http_server_mime_maps_additional_set"></a>nx_web_http_server_mime_maps_additional_set

HTML için ek MIME haritaları ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_mime_maps_additional_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_WEB_HTTP_SERVER_MIME_MAP *mime_maps,
    UINT mime_maps_num);
```

### <a name="description"></a>Description

Bu hizmet, HTTP uygulama geliştiricisinin NetX Web HTTP sunucusu tarafından sağlanan varsayılan MIME türlerinden ek MIME türleri eklemesine izin verir. Tanımlı türlerin listesi için bkz. *nx_web_http_server_get_type ()* .

Bir istemci isteği alındığında, örneğin, bir GET isteği, http üst bilgisinden istenen dosya türünü, tercihe bağlı olarak ek MIME eşleme kümesini kullanarak ayrıştırır ve bulunursa eşleşme yoksa, HTTP sunucusunun varsayılan MIME eşlemesinde bir eşleşme arar. Eşleşme bulunmazsa, MIME türü varsayılan olarak "metin/düz" olarak ayarlanır.

İstek bildirimi işlevi HTTP sunucusuna kayıtlıysa, istek bildirimi geri araması dosya türünü ayrıştırmak için *nx_web_http_server_type_get_extended ()* çağırabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP sunucusu örneğine yönelik işaretçi
- **mime_maps** MIME eşleme dizisine yönelik işaretçi
- **mime_map_num** Dizideki MIME haritaları sayısı

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı http sunucusu MIME eşleme kümesi
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* my_server is an NX_WEB_HTTP_SERVER previously created. */
static NX_WEB_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc", "yourtype/abc"},
    {"xyz", "mytype/xyz"},
};

status = nx_web_http_server_mime_maps_additional_set(&my_server,
    &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP
    server MIME map set." */
```

## <a name="nx_web_http_server_response_packet_allocate"></a>nx_web_http_server_response_packet_allocate

HTTP (S) paketi ayır

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_response_packet_allocate(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, HTTP (S) sunucusu için bir paket ayırır.

Sonraki bir NetX veya bu paketi giriş olarak kullanan bir HTTP sunucu API 'SI nx_packet_data_append veya * * nx_web_http_server_callback_packet_send gibi **başarısız olursa**, uygulamanın paketi serbest bırakmasından sorumlu olduğunu unutmayın. **

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
- **packet_ptr** Ayrılan pakete yönelik işaretçi.
- **wait_option** Paket havuzunda kullanılabilir bir paket yoksa, zaman işaretleri cinsinden bekleme süresini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **NX_NO_WAIT** (0x00000000) NX_NO_WAIT seçilmesi çağıran iş parçacığının istek karşılanmıyorsa hemen dönmesini sağlar.
  - **NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket ayırma
- **NX_NO_PACKET** (0x01) kullanılabilir paket yok
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği *tx_thread_wait_abort* bir çağrı tarafından iptal edildi.
- **NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Allocate a packet for HTTP(S) Server and suspend for a maximum of 5 timer
    ticks if the pool is empty. */
status = nx_web_http_server_response_packet_allocate(&my_client, &packet_ptr, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
    variable packet_ptr. */
```

## <a name="nx_web_http_server_packet_content_find"></a>nx_web_http_server_packet_content_find

İçerik uzunluğunu Ayıkla ve veri başına işaretçiyi ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_packet_content_find(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr,
    UINT *content_length);
```

### <a name="description"></a>Description

Bu hizmet, HTTP üstbilgisinden içerik uzunluğunu ayıklar. Ayrıca, sağlanan paketi aşağıdaki gibi güncelleştirir: paket önüne işaretçisi (yazılacak paket arabelleğinin konumu), http içeriğine (veri) yalnızca http üst bilgisini geçirilmiş şekilde ayarlanır.

İçeriğin başlangıcı geçerli pakette bulunmazsa, işlev, sonraki paketin NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE bekle seçeneği kullanılarak alınmasını bekler.

Bu, *nx_web_http_server_get_entity_header ()* çağrılmadan önce çağrılmamalıdır; çünkü bu, varlık üstbilgisinin ötesinde paket önüne işaretçisini değiştirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP sunucusu örneğine yönelik işaretçi
- **packet_ptr** Güncelleştirilmiş önüne işaretçisine sahip paketi döndürmek için paket işaretçisi işaretçisi
- **CONTENT_LENGTH** Ayıklanan content_length işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) http içerik uzunluğu bulundu ve paket başarıyla güncelleştirildi
- **NX_WEB_HTTP_TIMEOUT** (0x30001) sonraki pakette bekleme süresi geçildi
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
    The server has received a Client request packet, recv_packet_ptr,
    and the packet content find service is called from the request notify callback
    function registered with the HTTP server. */

UINT content_length;

status = nx_web_http_server_packet_content_find(server_ptr, recv_packet_ptr,
    &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
    and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_web_http_server_packet_get"></a>nx_web_http_server_packet_get

Sonraki HTTP paketini al

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_packet_get(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr);
```

### <a name="description"></a>Description

Bu hizmet, HTTP sunucusu yuvasında alınan bir sonraki paketi döndürür. Bir paket almak için bekle seçeneği NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE.

Başarılı olursa uygulamanın paketi serbest bırakmakla sorumlu olduğunu unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr** HTTP sunucusu örneğine işaretçi
- **packet_ptr** Alınan paketin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sonraki HTTP paketi başarıyla alındı
- **NX_WEB_HTTP_TIMEOUT** (0x30001) Sonraki Pakette bekleme süresi doldu
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* The HTTP server pointed to by server_ptr is previously created and started. */
UINT content_length;
NX_PACKET *recv_packet_ptr;

status = nx_web_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_web_http_server_param_get"></a>nx_web_http_server_param_get

İstekten parametreyi al

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_param_get(NX_PACKET *packet_ptr,
    UINT param_number, CHAR *param_ptr,
    UINT *param_size, UINT max_param_size);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL parametresini almaya çalışır. İstenen HTTP parametresi mevcutsa, bu yordam NX_WEB_HTTP_NOT_FOUND. Bu yordam, HTTP Sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirim geri çağrısından çağrıl *nx_web_http_server_create()*).

### <a name="input-parameters"></a>Giriş Parametreleri

- **packet_ptr** HTTP İstemcisi istek paketinin işaretçisi. Uygulamanın bu paketi serbest bırakması gerektiğini unutmayın.
- **param_number** Parametre listesinde soldan sağa sıfırdan başlayarak parametrenin mantıksal sayısı.
- **param_ptr** Parametreyi kopyalamak için hedef alan.
- **param_size** Toplam parametre veri uzunluğunu (bayt cinsinden) dönüş.
- **max_param_size** Parametre hedef alanı için en büyük boyut.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı HTTP Sunucusu parametresi get
- **NX_WEB_HTTP_NOT_FOUND** (0x30006) Belirtilen parametre bulunamadı
- **NX_WEB_HTTP_IMPROPERLY_TERMINATED_PARAM** (0x30015) Request parametresi düzgün bir şekilde sonlandırılmadı
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Assuming we are in the application’s request notify callback
    routine, get the first parameter of the HTTP Client request. */

status = nx_web_http_server_param_get(request_packet_ptr, 0, param_destination,
    &param_size, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
    in "param_destination" and the size of that string can be found
    in the variable "param_size." */
```

## <a name="nx_web_http_server_query_get"></a>nx_web_http_server_query_get

İstekten sorgu al

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_query_get(NX_PACKET *packet_ptr,
    UINT query_number,
    CHAR *query_ptr,
    CHAR *query_size,
    UINT max_query_size);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL sorgusunu almaya çalışır. İstenen HTTP sorgusu yoksa, bu yordam sorgunun durumunu NX_WEB_HTTP_NOT_FOUND. Bu yordam, HTTP Sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirim geri çağrısından çağrıl *nx_web_http_server_create()*).

### <a name="input-parameters"></a>Giriş Parametreleri

- **packet_ptr** HTTP İstemcisi istek paketinin işaretçisi. Uygulamanın bu paketi serbest bırakması gerektiğini unutmayın.
- **query_number** Sorgu listesinde soldan sağa sıfırdan başlayan parametrenin mantıksal sayısı.
- **query_ptr** Sorguyu kopyalamak için hedef alan.
- **query_size** Sorgu veri boyutunu (bayt cinsinden) iade eder.
- **max_query_size** Sorgu hedefinin en büyük boyutu

Alan.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı HTTP Sunucusu sorgusu get
- **NX_WEB_HTTP_FAILED** (0x30002) Sorgu boyutu çok küçük.
- **NX_WEB_HTTP_NOT_FOUND** (0x30006) Belirtilen sorgu bulunamadı
- **NX_WEB_HTTP_NO_QUERY_PARSED** (0x30013) İstemci isteğinde sorgu yok
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Assuming we are in the application’s request notify callback
    routine, get the first query of the HTTP Client request. */

status = nx_web_http_server_query_get(request_packet_ptr, 0,
    query_destination, &query_size, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
    in "query_destination" and the length of that string can be found in the
    variable "query_size". */
```

## <a name="nx_web_http_server_response_chunked_set"></a>nx_web_http_server_response_chunked_set

HTTP (S) yanıtı için öbekli aktarım ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_response_chunked_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT chunk_size, NX_PACKET *packet_ptr);
```

### <a name="description"></a>Description

Bu hizmet, nx_web_http_server_response_packet_allocate () ile oluşturulmuş özel bir HTTP(S) yanıt veri paketini istemciye *göndermek için öbekli* aktarım kodlaması kullanır.

> [!NOTE]
> Uygulama bir yanıt veri paketi göndermek için öbekli aktarım kodlaması kullanıyorsa, *nx_web_http_server_response_packet_allocate*() çağrısından sonra ve nx_web_http_server_callback_packet_send () çağrısından önce bu *hizmeti çağırmış* olması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **chunk_size** Sekizli aylarda öbek verisi boyutu.
- **packet_ptr** HTTP(S) istek veri paketi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı küme öbekli.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Generate HTTP header. */
nx_web_http_server_callback_generate_response_header(server_ptr,
    &response_pkt, NX_WEB_HTTP_STATUS_OK, 0, "text/html",
    "Transfer-Encoding: chunked\r\n");

/* Create a new data packet response on the HTTP(S) Server instance. */
nx_web_http_server_response_packet_allocate(&my_server, &my_packet, NX_WAIT_FOREVER);

/* Set the chunked transfer. */
status = nx_web_http_server_response_chunked_set(&my_server, 128, my_packet)

/* At this point, user can fill the data into my_packet. */
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet response to client. */
nx_web_http_server_callback_packet_send(&my_server, my_packet);
```

## <a name="nx_web_http_server_secure_configure"></a>nx_web_http_server_secure_configure

Güvenli HTTPS için TLS kullanmak üzere bir HTTP Sunucusu yapılandırma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_secure_configure(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    const NX_SECURE_TLS_CRYPTO *crypto_table,
    VOID *metadata_buffer, ULONG metadata_size,
    UCHAR* packet_buffer, UINT packet_buffer_size,
    NX_SECURE_X509_CERT *identity_certificate,
    NX_SECURE_X509_CERT *trusted_certificates[],
    UINT trusted_certs_num,
    NX_SECURE_X509_CERT *remote_certificates[],
    UINT remote_certs_num,
    UCHAR *remote_certificate_buffer,
    UINT remote_cert_buffer_size);
```

### <a name="description"></a>Description

Bu hizmet, güvenli HTTPS iletişimleri için TLS kullanmak üzere önceden oluşturulmuş bir NetX Web HTTP sunucusu örneğini yapılandırmaktadır. Parametreler, tüm olası TLS oturumlarını aynı durumla yapılandırarak gelen her BIR HTTPS İstemcisi'nin tutarlı bir davranışa sahip olması için kullanılır. TLS oturumlarının sayısı, makro oturumları kullanılarak NX_WEB_HTTP_SESSION_MAX.

Şifreleme yordamı tablosu (şifreleme tablosu), yalnızca işlev işaretçileri içerdiği için tüm TLS oturumları arasında paylaşılır.

Meta veriler ve paket yeniden değerlendirme arabelleklerinin her biri tüm TLS oturumları arasında eşit olarak bölündü. Arabellek boyutu, oturum sayısına eşit bölünene kadar bölünene kadar kalan kısım kullanılamaz.

Geçirilen kimlik sertifikası tüm oturumlar tarafından kullanılır. TLS işlemi sırasında sunucu kimlik sertifikası yalnızca 'den okunur, bu nedenle her oturum için kopya gerekmez.

Güvenilen sertifikalar HTTPS Sunucusundaki her TLS oturumuna eklenir. Bunlar, uzak sertifika alanı sağlanıyorsa otomatik olarak etkinleştiren İstemci sertifikası kimlik doğrulaması için kullanılır.

Uzak sertifika dizisi ve arabellek varsayılan olarak tüm TLS oturumları arasında paylaşılır. Uzak sertifikalar, uzak sertifika sayısı sıfırdan farklı olduğunda otomatik olarak etkinleştiren İstemci sertifikası kimlik doğrulaması için kullanılır. Arabelleğin paylaşılıyor olması nedeniyle sertifika doğrulaması sırasında bazı oturumlar engellenmiş olabilir.

İstemci sertifikası kimlik doğrulamasını devre dışı bırakmak için NX_NULL parametresi için remote_certificates ve remote_certs_num parametresi için 0 değerini girin.

Dönüş değerleri, TLS oturumlarının yapılandırmasında ortaya çıkan sorunlar nedeniyle ortaya çıkan tüm TLS hata kodlarını içerir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi.
- **crypto_table** TLS şifreleme tablosu işaretçisi.
- **metadata_buffer** Şifreleme meta veri arabelleği işaretçisi.
- **metadata_size** Şifreleme meta verileri arabelleğinin boyutu.
- **packet_buffer** TLS paketi yeniden değerlendirme arabelleği.
- **packet_buffer** TLS paket arabelleğinin boyutu – eşit olmalı (<TLS arabellek boyutu* NX_WEB_HTTP_SESSION_MAX).
- **identity_certificate** TLS sunucu kimliği sertifikası – tüm HTTPS sunucusu oturumları için kullanılır.
- **trusted_certificates** remote_certs_num parametresi için sıfır olmayan bir değer geçerek istemci sertifikası kimlik doğrulaması etkinse, gelen istemci sertifikalarını doğrulamak için kullanılan NX_SECURE_X509_CERT *nesneleri dizisinin işaretçisi.*
- **trusted_certs_num** Trusted_certificates dizisinde güvenilen *trusted_certificates* sayısı.
- **remote_certificates** Gelen istemci sertifikaları NX_SECURE_X509_CERT nesne dizisi işaretçisi.
- **remote_certs_num** Uzak sertifika sayısı. İstemcilerden beklenen en fazla sertifika sayısı olması gerekir. İstemci sertifikası kimlik doğrulaması, sıfır olmayan bir durumda otomatik olarak etkinleştirilir.
- **remote_certificate_buffer** İstemci sertifikası kimlik doğrulaması etkinse istemcilerden gelen uzak sertifikaları içeren arabelleğe alma. remote_cert_buffer_size uzak sertifika arabelleğinin boyutu. Eşit (beklenen en <sertifika boyutu üst \* remote_certs_num).


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) TLS oturumunun başarıyla başlatılıyor.
- **NX_NOT_CONNECTED** (0x38) Temel ALıNAN TCP yuvası artık bağlı değil.
- **NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) Alınan TLS ileti türü yanlış.
- **NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) Uzak konak tarafından sağlanan bir şifreleme desteklenmiyor.
- **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) TLS el sıkışması sırasında ileti işleme başarısız oldu.
- **NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Gelen ileti bir karma MAC denetimi başarısız oldu.
- **NX_SECURE_TLS_TCP_SEND_FAILE** (0x109) Temel alınan bir TCP yuvası gönderme işlemi başarısız oldu.
- **NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Gelen iletinin uzunluk alanı geçersizdi.
- **NX_SECURE_TLS_BAD_CIPHERSPE** (0x10B) Gelen bir ChangeCipherSpec iletisi yanlış.
- **NX_SECURE_TLS_INVALID_SERVER_CER** (0x10C) Gelen bir TLS sertifikası, uzak TLS sunucusunu tanımlamak için kullanılamaz.
- **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) Uzak konak tarafından sağlanan ortak anahtar şifrelemesi desteklenmez.
- **NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) Uzak konak NetX Secure TLS yığını tarafından desteklenen şifreleme olmadığını belirtti.
- **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Alınan bir TLS iletisi üst bilgisinde bilinmeyen bir TLS sürümüne sahipti.
- **NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) alınan bir TLS iletisi üst bilgisinde bilinen ancak desteklenmeyen bir TLS sürümüne sahipti.
- **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) bir iç TLS paket ayırması başarısız oldu.
- **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) Uzak konak geçersiz bir sertifika sağladı.
- **NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Uzak konak bir hata belirten bir uyarı gönderdi ve TLS oturumunu sonlandı.
- **NX_PTR_ERROR** (0x07) Geçersiz bir işaretçi kullanmayı denedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Create the HTTPS Server. */

status = nx_web_http_server_create(&my_server, "My HTTP Server",
    &ip_0, &ram_disk, &server_stack, sizeof(server_stack),
    &pool_0, authentication_check, server_request_callback);

/* Initialize device certificate (used for all sessions in HTTPS server). */
nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
    device_cert_der_len, NX_NULL, 0,
    device_cert_key_der, device_cert_key_der_len,
    NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

/* Setup TLS session for the HTTPS server.
    Note that since the remote_certs_num parameter is 0,
    no trusted certificates are needed, and Client certificate authentication is disabled. */
status = nx_web_http_server_secure_configure(&my_server, &nx_crypto_tls_ciphers,
    crypto_metadata,
    sizeof(crypto_metadata),
    tls_packet_buffer, sizeof(tls_packet_buffer),
    &certificate, NX_NULL, 0, NX_NULL, 0, NX_NULL, 0);

/* Start an HTTPS Server with TLS. */
status = nx_web_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_web_http_server_start"></a>nx_web_http_server_start

HTTP Sunucusunu başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_start(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir HTTP veya HTTPS Sunucusu örneğini başlatır.

HTTPS sunucuları HTTP ile aynı API'yi paylaşır. HTTP sunucusunda TLS kullanarak HTTPS'yi etkinleştirmek için bkz. *nx_web_http_server_secure_configure() .*

### <a name="input-parameters"></a>Giriş Parametreleri

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı HTTP Sunucusu Başlangıcı
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start the HTTP Server instance "my_server." */
status = nx_web_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_web_http_server_stop"></a>nx_web_http_server_stop

HTTP Sunucusunu Durdurma

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_stop(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulan HTTP Sunucusu örneğini durdurur. Bu yordam, bir HTTP Sunucusu örneği silmeden önce çağrılmalı.

### <a name="input-parameters"></a>Giriş Parametreleri

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı HTTP Sunucusu Durdurma
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Stop the HTTP Server instance "my_server." */
status = nx_web_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_web_http_server_type_get"></a>nx_web_http_server_type_get

İstemci HTTP isteğinden dosya türünü ayıklama

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_type_get(NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *name, CHAR *http_type_string,
    UINT *string_size);
```

### <a name="description"></a>Description

> [!NOTE]
> Bu hizmet kullanım dışıdır. Kullanıcıların *nx_web_http_server_type_get_extended() hizmetini kullanmaları teşvik edilecektir.*

Bu hizmet, arabellek http_type_string HTTP istek türünü *ve* string_size  adı *olan* URL'den ayıklar. MiME eşlemesi bulunamazsa varsayılan olarak "text/plain" türü kullanılır. Aksi takdirde, ayıklanan türü bir eşleşme için HTTP Sunucusu varsayılan MIME eşlemeleri ile karşılaştırıldığında. NetX Web HTTP Sunucusu'daki varsayılan MIME eşlemeleri:

- html metni/html
- html metin/html
- txt metni/düz
- gif görüntüsü/gif
- jpg image/jpeg
- ico görüntüsü/x-icon

Sağlanırsa, kullanıcı tanımlı bir dizi ek MIME eşlemesi de aranacak. Kullanıcı tanımlı nx_web_http_server_mime_maps_addtional_set hakkında daha fazla bilgi için bkz. *nx_web_http_server_mime_maps_addtional_set()* .

### <a name="input-parameters"></a>Giriş Parametreleri

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi
- **name** Arama için arabelleğe işaretçi
- **http_type_string** Ayıklanan HTML türü dizesinin işaretçisi
- **string_size** Ayıklanan HTML türü dize uzunluğunun dönüş işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Türün başarılı bir şekilde ayıklaması
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- **NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) Varsayılan "metin/düz" döndürülür.

### <a name="allowed-from"></a>İzin Verilen

Uygulama

### <a name="example"></a>Örnek

```C
/* my_server is a previously created HTTP server, which starts accepting client
    requests when *nx_web_http_server_start* is called */

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
string_length = nx_web_http_server_type_get(&my_server_ptr,
    my_server.nx_web_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
    For a more detailed example, see the description for
    *nx_web_http_server_callback_generate_response_header().*
```

## <a name="nx_web_http_server_type_get_extended"></a>nx_web_http_server_type_get_extended

İstemci HTTP isteğinden dosya türünü ayıklama

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_type_get_extended(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *name, UINT name_length,
    CHAR *http_type_string,
    UINT http_type_string_max_size,
    UINT *string_size);
```

### <a name="description"></a>Description

Bu hizmet, arabellek http_type_string HTTP istek türünü *ve* string_size  adı *olan* URL'den ayıklar. MiME eşlemesi bulunamazsa varsayılan olarak "text/plain" türü kullanılır. Aksi takdirde, ayıklanan türü bir eşleşme için HTTP Sunucusu varsayılan MIME eşlemeleri ile karşılaştırıldığında. NetX Web HTTP Sunucusu'daki varsayılan MIME eşlemeleri:

- html metni/html
- html metin/html
- txt metni/düz
- gif görüntüsü/gif
- jpg image/jpeg
- ico görüntüsü/x-icon

Sağlanırsa, kullanıcı tanımlı bir dizi ek MIME eşlemesi de aranacak. Kullanıcı tanımlı nx_web_http_server_mime_maps_addtional_set hakkında daha fazla bilgi için bkz. *nx_web_http_server_mime_maps_addtional_set()* .

Bu hizmet, *nx_web_http_server_type_get*() değiştirir. Bu sürüm, çağıranların işleve uzunluk bilgileri teminsini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi
- **name** Arama için arabelleğe işaretçi
- **name_length** Ad uzunluğu
- **http_type_string** Ayıklanan HTML türü dizesinin işaretçisi
- **http_type_string_max_size** Arabellek boyutunun http_type_string boyutu
- **string_size** Ayıklanan HTML türü dizesini iade etmek için işaretçi

Uzun -luğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Türün başarılı bir şekilde ayıklaması
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- **NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) Varsayılan "metin/düz" döndürülür.

### <a name="allowed-from"></a>İzin Verilen

Uygulama

### <a name="example"></a>Örnek

```C
/* my_server is a previously created HTTP server, which starts accepting client
    requests when *nx_web_http_server_start* is called */

CHAR temp_string[20];
UINT string_length;
UINT ret;

/* Extract the HTTP type. */
ret = nx_web_http_server_type_get_extended(&my_server_ptr,
    my_server.nx_web_http_server_request_resource,
    strlen(my_server.nx_web_http_server_request_resource),
    temp_string,sizeof(temp_string), &string_length);

/* If string_length is non zero, the HTTP string is extracted. */
    For a more detailed example, see the description for
    *nx_web_http_server_callback_generate_response_header().*
```

## <a name="nx_web_http_server_digest_authenticate_notify_set"></a>nx_web_http_server_digest_authenticate_notify_set

Özet kimlik doğrulaması geri çağırma işlevini ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_digest_authenticate_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*digest_authenticate_callback)(NX_WEB_HTTP_SERVER *server_ptr,
        CHAR *name_ptr,
        CHAR *realm_ptr,
        CHAR *password_ptr,
        CHAR *method,
        CHAR *authorization_uri,
        CHAR *authorization_nc,
        CHAR *authorization_cnonce));
```

### <a name="description"></a>Description

Bu hizmet özet kimlik doğrulaması gerçekleştirilirken çağrılan geri çağırmayı ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi
- **digest_authenticate_callback** Özet kimlik doğrulaması geri çağırma işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Geri çağırmayı başarıyla ayarlama
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_NOT_SUPPORTED (0x4B) Özet kimlik doğrulaması etkinleştirilmedi

### <a name="allowed-from"></a>İzin Verilen

Uygulama

### <a name="example"></a>Örnek

```C
UINT digest_authenticate_callback(NX_WEB_HTTP_SERVER *server_ptr, CHAR *name_ptr,
    CHAR *realm_ptr, CHAR *password_ptr, CHAR *method,
    CHAR *authorization_uri, CHAR *authorization_nc,
    CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_WEB_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_web_http_server_create, and
    before starting HTTP services when nx_web_http_server_start is called, set the digest authenticate callback: */
status = nx_web_http_server_digest_authenticate_notify_set(&my_server,
    digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
    will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_web_http_server_authenticate_check_set"></a>nx_web_http_server_authenticate_check_set

Özet kimlik doğrulaması geri çağırma işlevini ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_web_http_server_digest_authenticate_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*authentication_check_extended)(
        NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type,
        CHAR *resource,
        CHAR **name,
        UINT *name_length,
        CHAR **password,
        UINT password_length,
        CHAR **realm,
        UINT *realm_length));
```

### <a name="description"></a>Description

Bu hizmet, kimlik doğrulaması denetimi gerçekleştirilirken çağrılan geri çağırmayı ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi
- **authenticate_check_externded** Denetim geri çağırma kimliğini doğrulamak için işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Geri çağırmayı başarıyla ayarlama
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

Uygulama

### <a name="example"></a>Örnek

```C
UINT authenticate_check_callback(NX_WEB_HTTP_SERVER *server_ptr,
    UINT request_type,
    CHAR *name_ptr, UCHAR *resource, UCHAR **name,
    UINT *name_length, UCHAR **password,
    UINT *password_length, UCHAR **realm,
    UINT *realm_length)
{
    *name = "name";
    *name_length = 4;
    *password = "password";
    *password_length = 8;
    *realm = "realm";
    *realm_length = 5;
    return(NX_SUCCESS);
}

NX_WEB_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_web_http_server_create, and
    before starting HTTP services when nx_web_http_server_start is called, set the authenticate check callback: */

status = nx_web_http_digest_authenticate_check_set (&my_server,
    authenticate_check_callback);

/* If status equals NX_SUCCESS, the authenticate_check_callback function
    will be called when the HTTP server performs authenticate check. */
```
