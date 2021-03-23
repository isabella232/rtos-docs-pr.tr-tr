---
title: Bölüm 3-Azure RTOS NetX Duo HTTP hizmetlerinin açıklaması
description: Bu bölümde, aynı hizmetin ' NetX ' (yalnızca IPv4) eşdeğeri olarak eşleştirilmiş olması dışında tüm Azure RTOS NetX Duo HTTP Hizmetleri (aşağıda listelenmiştir) alfabetik sırada bir açıklama bulunur.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 703071cd5a1d0677a3e995fccfe35d8b1dbbd9f3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825967"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-http-services"></a>Bölüm 3-Azure RTOS NetX Duo HTTP hizmetlerinin açıklaması

Bu bölümde, aynı hizmetin ' NetX ' (yalnızca IPv4) eşdeğeri olarak eşleştirilmiş olması dışında tüm Azure RTOS NetX Duo HTTP Hizmetleri (aşağıda listelenmiştir) alfabetik sırada bir açıklama bulunur.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, KALıN olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

**HTTP Istemci Hizmetleri:**

- **NX_HTTP_CLIENT_CREATE** *http istemci örneği oluşturma*
-  *http istemci örneğini silme* nx_http_client_delete
-  *http get isteği başlatmak Nx_http_client_get_start (yalnızca IPv4)*
-  *http get isteği başlatmak Nx_http_client_get_start_extended (yalnızca IPv4)*
-  *http get isteği başlatma nxd_http_client_get_start (IPv4 veya IPv6)*
-  *http get isteği başlatma nxd_http_client_get_start_extended (IPv4 veya IPv6)*
-  *sonraki kaynak veri paketini al* nx_http_client_get_packet
-  *http put isteği başlatmak Nx_http_client_put_start (yalnızca IPv4)*
-  *http put isteği başlatmak Nx_http_client_put_start_extended (yalnızca IPv4)*
-  *http put isteği başlatma nxd_http_client_put_start (IPv4 veya IPv6)*
-  *http put isteği başlatma nxd_http_client_put_start_extended (IPv4 veya IPv6)*
-  *sonraki kaynak veri paketini nx_http_client_put_packet gönder*
-  *http sunucusuna bağlanmak için bağlantı noktasını değiştirme* nx_http_client_set_connect_port

**HTTP sunucusu Hizmetleri:**

-  *belirtilen URL 'nin yaş ve son değiştirilme tarihini almak için geri çağırma* nx_http_server_cache_info_callback_set
-  *GERI çağırma işlevinden http verileri gönderme* nx_http_server_callback_data_send
-  *geri çağırma işlevlerinde yanıt üst bilgisi oluşturma* nx_http_server_callback_generate_response_header
-  *geri çağırma işlevlerinde yanıt üst bilgisi oluşturma* nx_http_server_callback_generate_response_header_extended
-  *HTTP geri çağrısından http paketi gönderme* nx_http_server_callback_packet_send
-  *geri çağırma işlevinden yanıt gönder* nx_http_server_callback_response_send
-  *geri çağırma işlevinden yanıt gönder* nx_http_server_callback_response_send_extended
-  *istekten içerik al* nx_http_server_content_get
-  *istekten içerik al nx_http_server_content_get_extended; boş (sıfır içerik uzunluğu) isteklerini destekler*
- **nx_http_server_content_length_get** *istekteki içeriğin uzunluğunu al*
-  *istekteki içeriğin uzunluğunu nx_http_server_content_length_get_extended; boş (sıfır içerik uzunluğu) istekleri destekler*
- **NX_HTTP_SERVER_CREATE** *http sunucu örneği oluşturma*
- **nx_http_server_delete** * bir http sunucu örneğini silme *
- **nx_http_server_get_entity_content** *, URL 'deki varlık içeriğinin boyutunu ve konumunu döndürür*
-  *URL varlık üst bilgisini belirtilen arabelleğe nx_http_server_get_entity_header Ayıkla*
- **NX_HTTP_SERVER_GMT_CALLBACK_SET** *GMT Tarih ve saatini almak için geri çağırma ayarla*
-  *istemci isteğinde geçersiz Kullanıcı adı ve parola alındığında geri çağırma* nx_http_server_invalid_userpassword_notify_set
-  *HTML için ek mıme haritaları tanımlama* nx_http_server_mime_maps_additional_set
-  *http üstbilgisindeki içerik uzunluğunu ayıklama nx_http_server_packet_content_find ve içerik verilerinin başlangıcına işaretçiyi ayarla*
-  *istemci paketini doğrudan almak* nx_http_server_packet_get
-  *istekten parametre al* nx_http_server_param_get
-  *istekten sorgu al* nx_http_server_query_get
-  *http sunucusunu nx_http_server_start başlatın*
-  *http sunucusunu nx_http_server_stop durdur*
- **nx_http_server_type_get (kullanım dışı)** *http türünü (örneğin, metin/düz üstbilgi) Ayıkla*
-  *http türünü (örneğin, metin/düz üstbilgi) Ayıkla* nx_http_server_type_get_extended
- **nx_http_server_digest_authenticate_notify_set** *Özet kimlik doğrulaması geri arama işlevini ayarla*
- **nx_http_server_authentication_check_set** *kimlik doğrulaması denetim geri arama işlevini ayarla*

## <a name="nx_http_client_create"></a>nx_http_client_create

Bir PPPoE Istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_client_create(NX_HTTP_CLIENT *client_ptr,
            CHAR *client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr,
            ULONG window_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneğinde bir HTTP Istemci örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **client_name** HTTP Istemci örneğinin adı.
 - **ip_ptr** IP örneği işaretçisi.
 - **pool_ptr** Varsayılan paket havuzu işaretçisi. Bu havuzdaki paketlerin, tüm yanıt üst bilgisini işleyecek kadar büyük bir yükün olması gerektiğini unutmayın. Bu, *nx_http. h* içinde NX_HTTP_CLIENT_MIN_PACKET_SIZE tarafından tanımlanır.
 - **window_size** Istemcinin TCP yuvası alma penceresinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı http istemcisi oluşturma
 - NX_PTR_ERROR (0x07) geçersiz HTTP, ip_ptr veya paket havuzu işaretçisi
 - NX_HTTP_POOL_ERROR (0xE9) paket havuzunda geçersiz yük boyutu

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create the HTTP Client instance “my_client” on “ip_0”. */
status =  nx_http_client_create(&my_client, “my client”, &ip_0, &pool_0, 100);

/* If status is NX_SUCCESS an HTTP Client instance was successfully created. */
```

## <a name="nx_http_client_delete"></a>nx_http_client_delete

HTTP Istemci örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_http_client_delete(NX_HTTP_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir HTTP Istemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı http istemcisi silme
 - NX_PTR_ERROR (0x07) geçersiz HTTP işaretçisi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the HTTP Client instance “my_client.”  */
status =  nx_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully deleted. */
```

## <a name="nx_http_client_get_start"></a>nx_http_client_get_start

IPv4 üzerinden HTTP GET isteği başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, CHAR *input_ptr,
            UINT input_size, CHAR *username, CHAR *password,
            ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynakla bir GET isteği oluşturmaya ve gönderilmeye çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.

> [!NOTE]
> Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, ÖRNEĞIN ```http://abc.website.com/index.htm``` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu hizmet yalnızca IPv4 ağı üzerinden kullanılabilir. IPv6 ağına bağlanması gereken uygulamalar için *nxd_http_client_get_start_extended ()* kullanılmalıdır.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_http_client_get_start_extended ()* veya *nxd_http_client_get_start_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **ip_address** HTTP sunucusunun IP adresi.
 - **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
 - **input_ptr** GET isteği için ek verilere yönelik işaretçi. Bu isteğe bağlıdır. Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.
 - **input_size** İsteğe bağlı ek girişte tarafından işaret edilen bayt sayısı ```input_ptr``` .
 - **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
 - **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
 - **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) http istemcisi başarıyla gönderildi. Başlangıç iletisi al.
 - **NX_HTTP_ERROR** (0xE0) Iç http istemcisi hatası
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor
 - **NX_HTTP_FAILED** (0xE2) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xeb) adı ve/veya parolası geçersiz.
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                           NX_NULL, 0, “myname”, “mypassword”, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */


#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                            POST_MESSAGE, sizeof(POST_MESSAGE),
                            “myname”, “mypassword”, 1000);


/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST request
   for TEST.HTM and successfully sent. */
```

## <a name="nx_http_client_get_start_extended"></a>nx_http_client_get_start_extended

IPv4 üzerinden HTTP GET isteği başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, UINT resource_length,
            CHAR *input_ptr, UINT input_size, CHAR *username,
            UINT username_length, CHAR *password, UINT password_length,
            ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynakla bir GET isteği oluşturmaya ve gönderilmeye çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.

> [!NOTE]
> Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, ÖRNEĞIN ```http://abc.website.com/index.htm``` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu hizmet yalnızca IPv4 ağı üzerinden kullanılabilir. IPv6 ağına bağlanması gereken uygulamalar için *nxd_http_client_get_start_extended ()* kullanılmalıdır.

Bu hizmet *nx_http_client_get_start ()* yerini alır. Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **ip_address** HTTP sunucusunun IP adresi.
 - istenen kaynağın URL dizesine yönelik **kaynak işaretçisi** .
 - **resource_length** İstenen kaynak için URL dizesi uzunluğu.
 - **input_ptr** GET isteği için ek verilere yönelik işaretçi. Bu isteğe bağlıdır. Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.
 - **input_size** İsteğe bağlı ek girişte tarafından işaret edilen bayt sayısı ```input_ptr``` .
 - **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
 - **username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.
 - **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
 - **password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.
 - **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) http istemcisi başarıyla gönderildi. Başlangıç iletisi al
 - **NX_HTTP_ERROR** (0xE0) Iç http istemcisi hatası
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor
 - **NX_HTTP_FAILED** (0xE2) http sunucusuyla ILETIŞIM kurarken http istemci hatası.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xeb) adı ve/veya parolası geçersiz.
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */


#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                     9, POST_MESSAGE, sizeof(POST_MESSAGE),
                                     “myname”, 6, “mypassword”, 10, 1000);


/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST request
   for TEST.HTM and successfully sent. */
```

## <a name="nxd_http_client_get_start"></a>nxd_http_client_get_start

HTTP GET isteği gönderme (IPv4 veya IPv6)

### <a name="prototype"></a>Prototype

```c
UINT nxd_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
                NXD_ADDRESS *server_ip, CHAR *resource,
                CHAR *input_ptr, UINT input_size, CHAR *username, CHAR *password, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynakla bir GET isteği oluşturmaya ve gönderilmeye çalışır. Bu, IPv4 veya IPv6 ağına bağlanmak için kullanılabilir. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.

> [!NOTE]
>Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, ÖRNEĞIN ```http://abc.website.com/index.htm``` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nxd_http_client_get_start_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **Server_ip** HTTP sunucusunun IP adresi.
 - **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
 - **input_ptr** GET isteği için ek verilere yönelik işaretçi. Bu isteğe bağlıdır. Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.
 - **input_size** İsteğe bağlı ek girişte tarafından işaret edilen bayt sayısı ```input_ptr``` .
 - **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
 - **username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.
 - **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
 - **password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.
 - **wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) GET isteği başarıyla gönderildi
 - **NX_HTTP_PASSWORD_TOO_LONG** (0xf0) parolası arabellek boyutunu aşıyor
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor
 - **NX_HTTP_FAILED** (0xE2) geçersiz paket parametreleri.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xeb) geçersiz ad veya parola
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;


/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nxd_http_client_get_start(&my_client, server_ip_address, “/TEST.HTM”,
NX_NULL, 0, “myname”, “mypassword”, 1000);


/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */
```

## <a name="nxd_http_client_get_start_extended"></a>nxd_http_client_get_start_extended

HTTP GET isteği gönderme (IPv4 veya IPv6)

### <a name="prototype"></a>Prototype

```c
UINT nxd_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
                NXD_ADDRESS *server_ip, CHAR *resource,
                UINT resource_length, CHAR *input_ptr,
                UINT input_size, CHAR *username, UINT
                username_length, CHAR *password, UINT
                password_length, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynakla bir GET isteği oluşturmaya ve gönderilmeye çalışır. Bu, IPv4 veya IPv6 ağına bağlanmak için kullanılabilir. Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.

> [!NOTE]
> Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, ÖRNEĞIN ```http://abc.website.com/index.htm``` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.

Bu hizmet *nxd_http_client_get_start ()* yerini alır. Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **Server_ip** HTTP sunucusunun IP adresi.
 - **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
 - **resource_length** İstenen kaynak için URL dizesi uzunluğu.
 - **input_ptr** GET isteği için ek verilere yönelik işaretçi. Bu isteğe bağlıdır. Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.
 - **input_size** İsteğe bağlı ek girişte tarafından işaret edilen bayt sayısı ```input_ptr``` .
 - **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
 - **username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.
 - **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
 - **password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.
 - **wait_option** Hizmetin HTTP Istemcisi alma başlangıcını işlemek için dahili olarak bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) GET isteği başarıyla gönderildi
 - **NX_HTTP_PASSWORD_TOO_LONG** (0xf0) parolası arabellek boyutunu aşıyor
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor
 - **NX_HTTP_FAILED** (0xE2) geçersiz paket parametreleri.
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xeb) geçersiz ad veya parola
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;


/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nxd_http_client_get_start_extended(&my_client, server_ip_address,
                                             “/TEST.HTM”, 9, NX_NULL, 0, “myname”,
        6, “mypassword”, 10, 1000);


/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_http_client_get_packet"></a>nx_http_client_get_packet

Sonraki kaynak veri paketini al

### <a name="prototype"></a>Prototype

```c
UINT nx_http_client_get_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET **packet_ptr, ULONG
                               wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceki *nx_http_client_get_start* çağrısı tarafından istenen kaynağın sonraki içerik paketini alır. NX_HTTP_GET_DONE geri dönüş durumu alınana kadar bu yordama yönelik ardışık çağrılar yapılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **packet_ptr** Kısmi kaynak içeriği içeren paket işaretçisi hedefi.
 - **wait_option** Hizmetin HTTP Istemcisi alma paketi için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı http istemcisi Get paketi.
 - **NX_HTTP_GET_DONE** (0xEC) http istemcisi Get paketi bitti
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi Get modunda değil.
 - **NX_HTTP_BAD_PACKET_LENGTH** (0faksla) geçersiz paket uzunluğu
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the next packet of resource content on the HTTP Client “my_client.”
   Note that the nx_http_client_get_start routine must have been called
   previously. */
status =  nx_http_client_get_packet(&my_client, &next_packet, 1000);


/* If status is NX_SUCCESS, the next packet of content is pointed to
   by “next_packet”. */
```

## <a name="nx_http_client_put_start"></a>nx_http_client_put_start

IPv4 üzerinden HTTP PUT isteği başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                               ULONG ip_address, CHAR *resource,
                               CHAR *username, CHAR *password,
                               ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP adresindeki HTTP sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur. Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.

> [!NOTE]
> Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, örneğin ```http://abc.website.com/index.htm``` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nxd_http_client_put_start_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **ip_address** HTTP sunucusunun IP adresi.
 - **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
 - **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
 - **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
 - **total_bytes** Gönderilen toplam kaynak bayt sayısı. *Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.
 - **wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer seçilmesi (0x1-0xFFFFFFFE), HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı sayısını belirtir

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi
 - **NX_HTTP_USERNAME_TOO_LONG** (0xf1) Kullanıcı adı arabellek için çok büyük
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP Server
   at IP address 1.2.3.5. */
status =  nx_http_client_put_start(&my_client, IP_ADDRESS(1, 2, 3, 5),
“/TEST.HTM”, “myname”, “mypassword”, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
   started. */
```

## <a name="nx_http_client_put_start_extended"></a>nx_http_client_put_start_extended

IPv4 üzerinden HTTP PUT isteği başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
           ULONG ip_address, CHAR *resource, UINT resource_length,
           CHAR *username,UINT username_length, CHAR *password,
           UINT password_length, ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP adresindeki HTTP sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur. Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.

> [!NOTE]
> Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, örneğin ```http://abc.website.com/index.htm``` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.

Bu hizmet *nx_http_client_put_start ()* yerini alır. Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **ip_address** HTTP sunucusunun IP adresi.
 - **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
 - **resource_length** Sunucuya gönderilen kaynağın URL dizesi uzunluğu.
 - **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
 - **username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.
 - **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
 - **password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.
 - **total_bytes** Gönderilen toplam kaynak bayt sayısı. *Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.
 - **wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi
 - **NX_HTTP_USERNAME_TOO_LONG** (0xf1) Kullanıcı adı arabellek için çok büyük
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP Server
   at IP address 1.2.3.5. */
status =  nx_http_client_put_start_extended(&my_client, IP_ADDRESS(1, 2, 3, 5),
“/TEST.HTM”, 9, “myname”, 6, “mypassword”, 10, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
   started. */
```

## <a name="nxd_http_client_put_start"></a>nxd_http_client_put_start

HTTP PUT isteği (IPv4 veya IPv6) başlatma

### <a name="prototype"></a>Prototype

```c
UINT nxd_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                               NXD_ADDRESS *server_ip, CHAR *resource,
                               CHAR *username, CHAR *password,
                               ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen kaynağı HTTP sunucusunda IPv6 üzerinden sağlanan IP adresine (gönderme) (Gönderen) yüklemeye çalışır. Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.

> [!NOTE]
> Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, örneğin ```http://abc.website.com/index.htm``` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nxd_http_client_put_start_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **server_ip** HTTP sunucusunun IP adresi.
 - **kaynak** Sunucuya gönderilen kaynağın URL dizesi işaretçisi.
 - **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
 - **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
 - **total_bytes** Gönderilen toplam kaynak bayt sayısı. *Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.
 - **wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) http istemcisi PUT isteği başarıyla gönderildi
 - **NX_HTTP_ERROR** (0xE0) http istemcisi iç hatası
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor
 - **NX_HTTP_FAILED** (0xE2) http sunucusuyla ILETIŞIM kurarken http istemci hatası
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;

/* Start an HTTP PUT to place the 20-byte resource Client_test.HTM” on the HTTPv6  
   Server. */
status =  nxd_http_client_put_start(&my_client, &server_ip_address,
                                    "/client_test.htm", "name", "password", 103, 50);

/* If status is NX_SUCCESS, the PUT operation for Client_test.HTM has successfully
   been started. */
```

## <a name="nxd_http_client_put_start_extended"></a>nxd_http_client_put_start_extended

HTTP PUT isteği (IPv4 veya IPv6) başlatma

### <a name="prototype"></a>Prototype

```c
UINT nxd_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
          NXD_ADDRESS *server_ip, CHAR *resource, UINT resource_length,
          CHAR *username, UINT username_length, CHAR *password,
          UINT password_length, ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen kaynağı HTTP sunucusunda IPv6 üzerinden sağlanan IP adresine (gönderme) (Gönderen) yüklemeye çalışır. Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.

> [!NOTE]
> Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, örneğin ```http://abc.website.com/index.htm``` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.

Bu hizmet *nxd_http_client_put_start ()* yerini alır. Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **ip_address** HTTP sunucusunun IP adresi.
 - **kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.
 - **resource_length** Sunucuya gönderilen kaynağın URL dizesi uzunluğu.
 - **Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.
 - **username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.
 - **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
 - **password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.
 - **total_bytes** Gönderilen toplam kaynak bayt sayısı. *Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.
 - **wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) http istemcisi PUT isteği başarıyla gönderildi
 - **NX_HTTP_ERROR** (0xE0) http istemcisi iç hatası
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor
 - NX_HTTP_FAILED (0xE2) http sunucusuyla iletişim kurarken HTTP Istemci hatası
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;

/* Start an HTTP PUT to place the 20-byte resource Client_test.HTM” on the HTTPv6  
   Server. */
status =  nxd_http_client_put_start_extended(&my_client, &server_ip_address,
                                            "/client_test.htm", 16, "name", 4, "password", 8, 103, 50);

/* If status is NX_SUCCESS, the PUT operation for Client_test.HTM has successfully
   been started. */
```

## <a name="nx_http_client_put_packet"></a>nx_http_client_put_packet

Sonraki kaynak veri paketini gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET *packet_ptr,
                               ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, kaynak içeriğinin bir sonraki paketini HTTP sunucusuna gönderilmeye çalışır.

> [!NOTE]
> Bu yordam, gönderilen paketlerin Birleşik uzunluğu önceki *nx_http_client_put_start* çağrısında belirtilen "total_bytes" değerine eşit olana kadar kaldı çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **packet_ptr** HTTP sunucusuna gönderilen kaynağın bir sonraki içeriğine yönelik işaretçi.
 - **wait_option** Hizmetin, iç olarak HTTP Istemcisi PUT paketini işlemesini ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
    - **TX_WAIT_FOREVER** (0xffffffff)

    TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

    Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) http Istemci paketini başarıyla gönderdi.
 - **NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor
 - **NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0xEE) sunucu hata kodu aldı
 - **NX_HTTP_BAD_PACKET_LENGTH** (0faksla) geçersiz paket uzunluğu
 - **NX_HTTP_AUTHENTICATION_ERROR** (0xeb) geçersiz ad ve/veya parola
 - **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) sunucu, put tamamlanmadan önce yanıt veriyor
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_INVALID_PACKET (0x12) paketi TCP üst bilgisi için çok küçük
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Send a 20-byte packet representing the content of the resource
   “/TEST.HTM” to the HTTP Server. */
status =  nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr, NX_PACKET *packet_ptr, ULONG wait_option);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM has
   successfully been sent. */
```

## <a name="nx_http_client_set_connect_port"></a>nx_http_client_set_connect_port

Bağlantı noktasını sunucuya ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_http_client_set_connect_port(NX_HTTP_CLIENT *client_ptr,
                                      UINT port);
```

### <a name="description"></a>Açıklama

Bu hizmet, HTTP sunucusuna, çalışma zamanında belirtilen bağlantı noktasına bağlanırken bağlantı noktasını değiştirir. Aksi takdirde, bağlantı noktası varsayılan olarak 80 ' dir. Bunun *nx_http_client_get_start ()* ve *nx_http_client_put_start ()* öncesinde ÇAĞRıLMASı gerekir, örneğin http istemcisi sunucusuyla bağlanır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **client_ptr** HTTP Istemci denetim bloğu işaretçisi.
 - **bağlantı noktası** Sunucuya bağlanmak için bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) bağlantı noktası başarıyla değiştirilir
 - NX_INVALID_PORT (0x46) bağlantı noktası en büyük değeri (0xFFFF) aşıyor veya sıfır
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
NX_HTTP_CLIENT *client_ptr;

/* Change the connect port to 114. */
status =  nx_http_client_set_connect_port(client_ptr, 114);

/* If status is NX_SUCCESS, the connect port is successfully changed. */
```

## <a name="nx_http_server_cache_info_callback_set"></a>nx_http_server_cache_info_callback_set

URL 'YI en yüksek yaş ve tarihi almak için geri aramayı ayarlayın

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                         UINT (*cache_info_get)(CHAR *resource,
                                                 UINT *max_age,
                                                 NX_HTTP_SERVER_DATE
                                                      *date));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen kaynağın yaş ve son değiştirilme tarihini elde etmek için çağrılan geri çağırma hizmetini ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **cache_info_get** Geri çağırma işaretçisi
 - **max_age** Bir kaynağın maksimum yaşı işaretçisi
 - **veri** Son değiştirme tarihine yönelik işaretçi döndürüldü.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Başlatma

### <a name="example"></a>Örnek

```c
NX_HTTP_SERVER my_server;

UINT cache_info_get(CHAR *resource, UINT *max_age,
                           NX_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_http_server_create and before the HTTP  
   server is set by nx_http_server_start(), set the cache info callback: */

status = nx_http_server_cache_info_callback_set(&my_server, cache_info_get);


/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_http_server_callback_data_send"></a>nx_http_server_callback_data_send

Geri çağırma işlevinden veri Gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_callback_data_send(NX_HTTP_SERVER *server_ptr,
                                       VOID *data_ptr,
                                       ULONG data_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, sağlanan paketteki verileri uygulamanın geri arama yordamından gönderir. Bu, genellikle GET/POST istekleri ile ilişkili dinamik verileri göndermek için kullanılır.

> [!NOTE]
> Bu işlev kullanılıyorsa, tüm yanıtın doğru biçimde gönderilmesi için geri çağırma yordamı sorumludur. Ayrıca, geri arama yordamı NX_HTTP_CALLBACK_COMPLETED durumunu döndürmelidir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **data_ptr** Gönderilen verilerin işaretçisi.
 - **data_length**  Gönderilen bayt sayısı.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) sunucu verilerini başarıyla gönderdi
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
  CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
                (strcmp(resource, "/test.htm") == 0))
    {

        /* Found it, override the GET processing by sending the resource
    contents directly. */

        nx_http_server_callback_data_send(server_ptr,
    "HTTP/1.0 200 \r\nContent-Length:
    103\r\nContent-Type: text/html\r\n\r\n",
    63);

        nx_http_server_callback_data_send(server_ptr, "<HTML>\r\n<HEAD><TITLE>NetX
    HTTP Test </TITLE></HEAD>\r\n
    <BODY>\r\n<H1>NetX Test Page
    </H1>\r\n</BODY>\r\n</HTML>\r\n", 103);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_generate_response_header"></a>nx_http_server_callback_generate_response_header

Geri arama işlevinde yanıt üst bilgisi oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_callback_generate_response_header(
                        NX_HTTP_SERVER *server_ptr,
                        NX_PACKET **packet_pptr,
                        CHAR *status_code, UINT content_length,
                        CHAR *content_type, CHAR* additional_header);
```

### <a name="description"></a>Açıklama

Bu hizmet, HTTP sunucusu Istemci GET, put ve DELETE isteklerine yanıt verdiğinde iç işlevi *_nx_http_server_generate_response_header* çağırır. HTTP sunucusu uygulaması Istemciye yanıtını tasarlarken HTTP sunucusu geri çağırma işlevlerinde kullanılmak üzere tasarlanmıştır.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nxd_http_server_callback_generate_response_header_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi
 - **status_code** Kaynağın durumunu belirtin. Örnekler:
    - **NX_HTTP_STATUS_OK**
    - **NX_HTTP_STATUS_MODIFIED**
    - **NX_HTTP_STATUS_INTERNAL_ERROR**
 - **CONTENT_LENGTH** İçerik boyutu (bayt)
 - **content_type** HTTP türü, örneğin "metin/düz"
 - **additional_header** Ek üst bilgi metnine yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarıyla oluşturuldu üst bilgisi
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
CHAR demotestbuffer[] = "<html>\r\n\r\n<head>\r\n\r\n<title>Main   \
            Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n   \  </body>\r\n</html>\r\n";

     /* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
 CHAR *resource, NX_PACKET *recv_packet_ptr)
      {

NX_PACKET   *sresp_packet_ptr;
ULONG       string_length;
CHAR        temp_string[30];
ULONG       length = 0;


   length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length =  (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr ->
nx_http_server_request_resource, temp_string,
sizeof(temp_string));

       /* Null terminate the string. */
   temp_string[temp] = 0;

       /* Now build a response header with server status is OK and no additional header  
          info. */
   status = nx_http_server_callback_generate_response_header(http_server_ptr,
                  &resp_packet_ptr, NX_HTTP_STATUS_OK,
                  length, temp_string, NX_NULL);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
                 length,  server_ptr ->
                 nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
   if (status != NX_SUCCESS)
   {
       nx_packet_release(resp_packet_ptr);
       return status;
   }



/* Now send the packet! */
           status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
                                      resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);

   if (status != NX_SUCCESS)
   {
      nx_packet_release(resp_packet_ptr);

      return status;
   }

/* Let HTTP server know the response has been sent. */
  return NX_HTTP_CALLBACK_COMPLETED;

     }
```

## <a name="nx_http_server_callback_generate_response_header_extended"></a>nx_http_server_callback_generate_response_header_extended

Geri arama işlevinde yanıt üst bilgisi oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_callback_generate_response_header_extended(
                        NX_HTTP_SERVER *server_ptr,
                        NX_PACKET **packet_pptr,
                        CHAR *status_code, UINT status_code_length,
                        UINT content_length,
                        CHAR *content_type, UINT content_type_length,
                        CHAR *additional_header,
                        UINT additional_header_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, HTTP sunucusu Istemci GET, put ve DELETE isteklerine yanıt verdiğinde *_nx_http_server_generate_response_header ()* iç işlevini çağırır. HTTP sunucusu uygulaması Istemciye yanıtını tasarlarken HTTP sunucusu geri çağırma işlevlerinde kullanılmak üzere tasarlanmıştır.

Bu hizmet *nx_http_server_callback_generate_response_header ()* yerini alır. Bu sürüm, geri çağırma işlevine ek uzunluk bilgileri sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi
 - **status_code** Kaynağın durumunu belirtin. Örnekler:
    - **NX_HTTP_STATUS_OK**
    - **NX_HTTP_STATUS_MODIFIED**
    - **NX_HTTP_STATUS_INTERNAL_ERROR**
 - **status_code** Durum kodu uzunluğu
 - **CONTENT_LENGTH** İçerik boyutu (bayt)
 - **content_type** HTTP türü, örneğin "metin/düz"
 - **content_type_length** HTTP türünün uzunluğu
 - **additional_header** Ek üst bilgi metnine yönelik işaretçi
 - **additional_header_length** Ek üst bilgi metninin uzunluğu

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarıyla oluşturuldu üst bilgisi
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
CHAR demotestbuffer[] = "<html>\r\n\r\n<head>\r\n\r\n<title>Main   \
     Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n   \  </body>\r\n</html>\r\n";

     /* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
 CHAR *resource, NX_PACKET *recv_packet_ptr)
      {

NX_PACKET   *sresp_packet_ptr;
ULONG       string_length;
CHAR        temp_string[30];
ULONG       length = 0;


   length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length =  (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr ->
nx_http_server_request_resource, temp_string,
sizeof(temp_string));

       /* Null terminate the string. */
   temp_string[temp] = 0;

       /* Now build a response header with server status is OK and no additional header  
          info. */
   status = nx_http_server_callback_generate_response_header_extended(
                             http_server_ptr, &resp_packet_ptr, NX_HTTP_STATUS_OK,
              sizeof(NX_HTTP_STATUS_OK) - 1, length,
              temp_string, string_length, NX_NULL, 0);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
                 length,  server_ptr ->
                 nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
   if (status != NX_SUCCESS)
   {
       nx_packet_release(resp_packet_ptr);
       return status;
   }



/* Now send the packet! */
           status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
                                      resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);

   if (status != NX_SUCCESS)
   {
      nx_packet_release(resp_packet_ptr);

      return status;
   }

/* Let HTTP server know the response has been sent. */
  return NX_HTTP_CALLBACK_COMPLETED;

     }
```

## <a name="nx_http_server_callback_packet_send"></a>nx_http_server_callback_packet_send

Geri çağırma işlevinden HTTP paketi gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_callback_packet_send(NX_HTTP_SERVER *server_ptr,
                                         NX_PACKET *packet_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, HTTP geri çağrısından gelen bir HTTP Sunucu yanıtı gönderir. HTTP sunucusu, paketi NX_HTTP_SERVER _TIMEOUT_SEND gönderecek. HTTP üst bilgisi ve verilerinin pakete eklenmesi gerekir. Dönüş durumu bir hata gösteriyorsa, HTTP uygulaması paketi serbest bırakmalıdır.

Geri çağırma NX_HTTP_CALLBACK_COMPLETED döndürmelidir.

Daha ayrıntılı bir örnek için bkz. *nx_http_server_callback_generate_response_header ()* .

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **packet_ptr** Gönderilmek üzere paket işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) sunucu paketi başarıyla gönderildi
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* The packet is appended with HTTP header and data and is ready to send to the
   Client directly. */

   status = nx_http_server_callback_response_send(server_ptr, packet_ptr);

   if (status != NX_SUCCESS)
   {

    nx_packet_release(packet_ptr);
   }

    return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_callback_response_send"></a>nx_http_server_callback_response_send

Geri çağırma işlevinden yanıt gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_callback_response_send(NX_HTTP_SERVER *server_ptr,
                                           CHAR *header,
                                           CHAR *information,
                                           CHAR additional_info);
```

### <a name="description"></a>Açıklama

Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir. Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır.

> [!NOTE]
> Bu işlev kullanılırsa, geri çağırma yordamının NX_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerekir.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nxd_http_server_callback_response_send_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.
 - **bilgi** Bilgi dizesinin işaretçisi.
 - **additional_info** Ek bilgi dizesinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) sunucu yanıtı başarıyla gönderildi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                        CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
               (strcmp(resource, "/test.htm") == 0))
    {

        /* In this example, we will complete the GET processing with
           a resource not found response. */
     nx_http_server_callback_response_send(server_ptr,
                      "HTTP/1.0 404 ",
                      "NetX HTTP Server unable to find  
                       file: ", resource);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_response_send_extended"></a>nx_http_server_callback_response_send_extended

Geri çağırma işlevinden yanıt gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_callback_response_send_extended(
                                          NX_HTTP_SERVER *server_ptr,
                                          CHAR *header,
                                          UINT header_length,
                                          CHAR *information,
                                          UINT information_length,
                                          CHAR *additional_info,
                                          UINT additional_info_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir. Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır.

> [!NOTE]
> Bu işlev kullanılırsa, geri çağırma yordamının NX_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerekir.

Bu hizmet *nx_http_server_callback_response_send ()* yerini alır. Bu sürüm, ek uzunluk bilgilerini bağımsız değişken olarak alır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.
 - **header_length** Yanıt üst bilgisi dizesinin uzunluğu.
 - **bilgi** Bilgi dizesinin işaretçisi.
 - **information_length** Bilgi dizesinin uzunluğu.
 - **additional_info** Ek bilgi dizesinin işaretçisi.
 - **additional_info_length** Ek bilgi dizesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) sunucu yanıtı başarıyla gönderildi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                        CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
               (strcmp(resource, "/test.htm") == 0))
    {

        /* In this example, we will complete the GET processing with
           a resource not found response. */
     nx_http_server_callback_response_send_extended(
                                             server_ptr,
                      "HTTP/1.0 404 ", 12,
                      "NetX HTTP Server unable to find  
                       file: ", 38, resource, 9);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_content_get"></a>nx_http_server_content_get

İstekten içerik al

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_content_get(NX_HTTP_SERVER *server_ptr,
                                NX_PACKET *packet_ptr,
                                ULONG byte_offset,
                                CHAR *destination_ptr,
                                UINT destination_size,
                                UINT *actual_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, POST veya PUT HTTP Client isteğinden belirtilen miktarda içeriği almaya çalışır. HTTP sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağrısından (*nx_http_server_create*) çağrılmalıdır.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_http_server_content_get_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi. Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.
 - **byte_offset** İçerik alanına kaydırılacağı bayt sayısı.
 - **destination_ptr** İçerik için hedef alana yönelik işaretçi.
 - **destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.
 - **actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı http sunucusu içerik al
 - **NX_HTTP_ERROR** (0xE0) http sunucusu iç hatası
 - **NX_HTTP_DATA_END** (0xE7) Istek içeriğinin sonu
 - **NX_HTTP_TIMEOUT** (0XE1) sonraki içerik paketini alma sırasında http sunucusu zaman aşımı
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Assuming we are in the application’s request notify callback
   routine, retrieve up to 100 bytes of content starting at offset
   0. */
status =  nx_http_server_content_get(&my_server, packet_ptr,
                      0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
   request content. */
```

## <a name="nx_http_server_content_get_extended"></a>nx_http_server_content_get_extended

İstekten içerik al/sıfır uzunlukta Içerik uzunluğunu destekler

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_content_get_extended(NX_HTTP_SERVER *server_ptr,
                                         NX_PACKET *packet_ptr,
                                         ULONG byte_offset,
                                         CHAR *destination_ptr,
                                         UINT destination_size,
                                         UINT *actual_size);
```

### <a name="description"></a>Açıklama

Bu hizmet neredeyse *nx_http_server_content_get ()* ile AYNıDıR; Post veya put http Client isteğinden belirtilen miktarda içeriği almaya çalışır. Ancak, geçerli bir istek olarak sıfır değeri (' boş istek ') Içerik uzunluğundaki istekleri işler. Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.

Bu hizmet *nx_http_server_content_get ()* yerini alır. Bu sürüm, çağıranın ek uzunluk bilgileri sağlaması için gereklidir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi. Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.
 - **byte_offset** İçerik alanına kaydırılacağı bayt sayısı.
 - **destination_ptr** İçerik için hedef alana yönelik işaretçi.
 - **destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.
 - **actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı http içerik al
 - **NX_HTTP_ERROR** (0xE0) http sunucusu iç hatası
 - **NX_HTTP_DATA_END** (0xE7) Istek içeriğinin sonu
 - **NX_HTTP_TIMEOUT** (0XE1) sonraki paketi alma sırasında http sunucusu zaman aşımı
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Assuming we are in the application’s request notify callback
   routine, retrieve up to 100 bytes of content starting at offset
   0. */
status =  nx_http_server_content_get_extended(&my_server, packet_ptr,
                               0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
   request content. */
```

## <a name="nx_http_server_content_length_get"></a>nx_http_server_content_length_get

İstekteki içerik uzunluğunu al

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_content_length_get(NX_PACKET *packet_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, sağlanan paketteki HTTP içerik uzunluğunu almaya çalışır. HTTP içeriği yoksa, bu yordam sıfır değerini döndürür. Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_http_server_content_length_get_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi. Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.

### <a name="return-values"></a>Dönüş Değerleri

 - **içerik uzunluğu** Hatada, sıfır değeri döndürülür  

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Assuming we are in the application’s request notify callback
   routine, get the content length of the HTTP Client request. */
length =  nx_http_server_content_length_get(packet_ptr);

/* The “length” variable now contains the length of the HTTP Client
   request content area. */
```

## <a name="nx_http_server_content_length_get_extended"></a>nx_http_server_content_length_get_extended

İstekteki içerik uzunluğunu al/sıfır değerinin Içerik uzunluğunu destekler

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_content_length_get_extended(NX_PACKET *packet_ptr,
                                                UINT *content_length);
```

### <a name="description"></a>Açıklama

Bu hizmet *nx_http_server_content_length_get benzerdir;* sağlanan paketteki http içerik uzunluğunu alma girişiminde bulunur. Ancak, dönüş değeri başarıyla tamamlanma durumunu gösterir ve giriş İşaretçisinde gerçek uzunluk değeri döndürülür ```content_length``` . HTTP içeriği/Içerik uzunluğu = 0 yoksa, bu yordam yine de başarılı bir tamamlanma durumu döndürür ve content_length giriş işaretçisi geçerli bir uzunluğa (sıfır) işaret eder. HTTP sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağrısından (*nx_http_server_create*) çağrılmalıdır.

Bu hizmet *nx_http_server_content_length_get ()* yerini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi. Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.
 - **CONTENT_LENGTH** Içerik uzunluğu alanından alınan değer işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı sunucu içeriği al
 - **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) yanlış http üst bilgi biçimi
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Assuming we are in the application’s request notify callback
   routine, get the content length of the HTTP Client request. */
ULONG content_length;

status =  nx_http_server_content_length_get_extended(packet_ptr, &content_length);

/* If the “status” variable indicates successful completion, the“length” variable
   contains the length of the HTTP Client request content area. */
```

## <a name="nx_http_server_create"></a>nx_http_server_create

HTTP sunucusu örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_create(NX_HTTP_SERVER *http_server_ptr,
      CHAR *http_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr,
      VOID *stack_ptr, ULONG stack_size, NX_PACKET_POOL *pool_ptr,
      UINT (*authentication_check)(NX_HTTP_SERVER *server_ptr,
            UINT request_type, CHAR *resource, CHAR **name,
            CHAR **password, CHAR **realm),
      UINT (*request_notify)(NX_HTTP_SERVER *server_ptr,
            UINT request_type, CHAR *resource, NX_PACKET *packet_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet kendi ThreadX iş parçacığı bağlamında çalışan bir HTTP sunucu örneği oluşturur. İsteğe bağlı *authentication_check* ve request_notify uygulama geri çağırma yordamları, HTTP sunucusunun temel işlemleri üzerinde uygulama yazılım denetimi sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **http_server_ptr** HTTP sunucu denetim bloğu işaretçisi.
 - **http_server_name** HTTP sunucusu adı işaretçisi.
 - **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
 - **media_ptr** Daha önce oluşturulan FileX medya örneğine yönelik işaretçi.
 - **stack_ptr** HTTP sunucusu iş parçacığı yığın alanı işaretçisi.
 - **stack_size** HTTP sunucusu iş parçacığı yığın boyutu işaretçisi.
 - **authentication_check** Uygulamanın kimlik doğrulama denetimi yordamına yönelik işlev işaretçisi. Belirtilmişse, bu yordam her HTTP Istemci isteği için çağırılır. Bu parametre NULL ise, kimlik doğrulaması gerçekleştirilmez.
 - **request_notify** Uygulamanın istek bildirim yordamına yönelik işlev işaretçisi. Belirtilmişse, bu yordam isteğin HTTP sunucu işlemeden önce çağırılır. Bu, HTTP Istemci isteği tamamlanmadan önce kaynak adının yeniden yönlendirilmesine veya bir kaynak içindeki alanların güncelleştirilmesini sağlar.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı http sunucusu oluşturma.
 - NX_PTR_ERROR (0x07) geçersiz HTTP sunucusu, IP, medya, yığın veya paket havuzu işaretçisi.
 - NX_HTTP_POOL_ERROR (0xE9) havuzun paket yükü, tüm HTTP isteklerini içerecek kadar büyük değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create an HTTP Server instance called “my_server.”  */
status =  nx_http_server_create(&my_server, “my server”, &ip_0, &ram_disk,
              stack_ptr, stack_size, &pool_0,
              my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_http_server_delete"></a>nx_http_server_delete

HTTP sunucusu örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_delete(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Açıklama

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

```c
/* Delete the HTTP Server instance called “my_server.”  */
status =  nx_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_http_server_get_entity_content"></a>nx_http_server_get_entity_content

Varlık verilerinin konumunu ve uzunluğunu alma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_pptr,
                                       ULONG *available_offset,
                                       ULONG *available_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, alınan Istemci iletilerindeki geçerli çok parçalı varlıktaki verilerin başlangıç konumunu ve sınır dizesini dahil olmayan veri uzunluğunu belirler. Dahili HTTP sunucusu, bu işlevin birden çok varlığa sahip iletiler için aynı Istemci veri biriminde yeniden çağrılabilmesi için kendi uzaklıklarını güncelleştirir. Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.

> [!NOTE]
> Bu hizmeti kullanmak için NX_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerekir.

Daha fazla bilgi için bkz. [*nx_http_server_get_entity_header*](#nx_http_server_get_entity_header) .

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucusu işaretçisi
 - **packet_pptr** Paket işaretçisinin konumu işaretçisi. Uygulamanın bu paketi serbest bırakmadığını unutmayın.
 - **available_offset** Paket önüne işaretçisinden varlık verilerinin uzaklığa yönelik işaretçi
 - **available_length** Varlık verisi uzunluğu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) varlık içeriğinin boyutunu ve konumunu başarıyla aldı
 - HTTP sunucusu iç çok parçalı işaretçiler için **NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xf4) içeriği zaten var
 - NX_HTTP_ERROR (0xE0) Iç HTTP hatası
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_HTTP_SERVER my_server;

UINT        offset, length;
NX_PACKET  *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
   the entity header to determine details about the multipart data. If
   successful, it then calls this service to get the location of entity data: */

status =  nx_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
&length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
   entity data. */
```

## <a name="nx_http_server_get_entity_header"></a>nx_http_server_get_entity_header

Varlık üstbilgisinin içeriğini alma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      UCHAR *entity_header_buffer,
                                      ULONG buffer_size);
```

### <a name="description"></a>Açıklama

Bu hizmet varlık üstbilgisini belirtilen arabelleğe alır. Dahili HTTP sunucusu, birden çok varlık üst bilgilerine sahip bir Istemci veri biriminde bir sonraki çok parçalı varlığı bulmak için kendi işaretçilerini güncelleştirir. Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.

> [!NOTE]
> Bu hizmeti kullanmak için NX_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucusu işaretçisi
 - **packet_pptr** Paket işaretçisinin konumu işaretçisi. Uygulamanın bu paketi serbest bırakmadığını unutmayın.
 - **entity_header_buffer** Varlık üstbilgisinin depolanacak konuma işaretçi
 - **Buffer_size** Giriş arabelleğinin boyutu

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) varlık Heade başarıyla alındı
 - **NX_HTTP_NOT_FOUND** **(0xE6)** varlık üst bilgisi alanı bulunamadı
 - Çok müşterili istemci ileti için sonraki paketi almak üzere **NX_HTTP_TIMEOUT** **(0XE1)** süresi geçildi
 - NX_HTTP_ERROR (0xE0) Iç HTTP hatası
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                              CHAR *resource, NX_PACKET *packet_ptr)
      {

        NX_PACKET   *sresp_packet_ptr;
        UINT        offset, length;
        NX_PACKET   *response_pkt;
        UCHAR       buffer[1440];

        /* Process multipart data. */
        if(request_type == NX_HTTP_SERVER_POST_REQUEST)
        {

       /* Get the content header. */
       while(nx_http_server_get_entity_header(server_ptr, &packet_ptr, buffer,
                                         sizeof(buffer)) == NX_SUCCESS)
   {

      /* Header obtained successfully. Get the content data location. */
      while(nx_http_server_get_entity_content(server_ptr, &packet_ptr, &offset,
                                              &length) == NX_SUCCESS)
      {
           /* Write content data to buffer. */
           nx_packet_data_extract_offset(packet_ptr, offset, buffer, length,
                                         &length);
           buffer[length] = 0;
      }

    }

    /* Generate HTTP header. */
    status = nx_http_server_callback_generate_response_header(server_ptr,
                         &response_pkt, NX_HTTP_STATUS_OK, 800, "text/html",
                         "Server: NetXDuo HTTP 5.3\r\n");

    if(status == NX_SUCCESS)
    {
        if(nx_http_server_callback_packet_send(server_ptr, response_pkt) !=
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
return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_gmt_callback_set"></a>nx_http_server_gmt_callback_set

GMT Tarih ve saati almak için geri aramayı ayarlayın

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                     VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş bir HTTP sunucusu ile GMT Tarih ve saati alacak şekilde geri aramayı ayarlar. Bu hizmet HTTP sunucusu, Istemciye HTTP sunucu yanıtlarında bir üst bilgi oluşturuyor.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucusu işaretçisi
 - **gmt_getv** GMT geri çağırması işaretçisi
 - **Tarih v** Alınan tarihin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
 - NX_PTR_ERROR (0x07) geçersiz paket veya parametre işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_HTTP_SERVER my_server;

VOID get_gmt(NX_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the GMT
   retrieve callback: */

status =  nx_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
   response header date. */
```

## <a name="nx_http_server_invalid_userpassword_notify_set"></a>nx_http_server_invalid_userpassword_notify_set

Geri çağırma işlemini geçersiz kullanıcı/parola işleyecek şekilde ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_invalid_userpassword_notify_set(
            NX_HTTP_SERVER *http_server_ptr,
            UINT (*invalid_username_password_callback)
                        (CHAR *resource,
                        NXD_ADDRESS *client_address,
                        UINT request_type));
```

### <a name="description"></a>Açıklama

Bu hizmet, bir Istemci alma, yerleştirme veya silme isteğinde, Özet veya temel kimlik doğrulamasından göre geçersiz bir Kullanıcı adı ve parola alındığında çağrılan geri aramayı ayarlar. HTTP sunucusu daha önce oluşturulmuş olmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucusu işaretçisi
 - **invalid_username_password_callback** Geçersiz Kullanıcı/geçiş geri çağırması işaretçisi
 - **kaynak** İstemci tarafından belirtilen kaynak işaretçisi
 - **client_address** İstemci adresi işaretçisi. IPv4 veya IPv6 olabilir
 - **request_type** İstemci isteği türünü gösterir. Belki:
    - NX_HTTP_SERVER_GET_REQUEST
    - NX_HTTP_SERVER_POST_REQUEST
    - NX_HTTP_SERVER_HEAD_REQUEST
    - NX_HTTP_SERVER_PUT_REQUEST
    - NX_HTTP_SERVER_DELETE_REQUEST

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NX_HTTP_SERVER my_server;
VOID invalid_username_password_callback (NX_ CHAR *resource,
                                         NXD_ADDRESS *client_address,
                                         UINT   request_type);

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the invalid
   username password callback: */

status =  nx_http_server_gmt_callback_set(&my_server,
                                          invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
   will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_http_server_mime_maps_additional_set"></a>nx_http_server_mime_maps_additional_set

HTML için ek MIME haritaları ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_mime_maps_additional_set(
                        NX_HTTP_SERVER *server_ptr,
                        NX_HTTP_SERVER_MIME_MAP *mime_maps,
                        UINT mime_maps_num);
```

### <a name="description"></a>Açıklama

Bu hizmet, HTTP uygulama geliştiricisinin NetX Duo HTTP sunucusu tarafından sağlanan varsayılan MIME türlerinden ek MIME türleri eklemesine izin verir (tanımlı türlerin listesi için bkz. *nx_http_server_get_type* ).

Bir istemci isteği alındığında, örneğin, bir GET isteği, http üst bilgisinden istenen dosya türünü, tercihe bağlı olarak ek MIME eşleme kümesini kullanarak ayrıştırır ve bulunursa eşleşme yoksa, HTTP sunucusunun varsayılan MIME eşlemesinde bir eşleşme arar. Eşleşme bulunmazsa, MIME türü varsayılan olarak "metin/düz" olarak ayarlanır.

İstek bildirimi işlevi HTTP sunucusuna kayıtlıysa, istek bildirimi geri araması dosya türünü ayrıştırmak için *nx_http_server_type_retrieve ()* çağırabilir.

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

```c
/* my_server is an NX_HTTP_SERVER previously created. */

NX_HTTP_SERVER_MIME_MAP my_mime_maps [2];

static NX_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc",      "yourtype/abc"},
    {"xyz",      "mytype/xyz"},
};

status =  nx_http_server_mime_maps_additional_set(&my_server,
                                                  &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP  
  server MIME map set.” */
```

## <a name="nx_http_server_packet_content_find"></a>nx_http_server_packet_content_find

İçerik uzunluğunu Ayıkla ve veri başına işaretçiyi ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_packet_content_find(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET **packet_ptr,
                                        UINT *content_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, HTTP üstbilgisinden içerik uzunluğunu ayıklar. Ayrıca, sağlanan paketi aşağıdaki gibi güncelleştirir: paket önüne işaretçisi (yazılacak paket arabelleğinin konumu), http içeriğine (veri) yalnızca http üst bilgisini geçirilmiş şekilde ayarlanır.

İçeriğin başlangıcı geçerli pakette bulunmazsa, işlev, sonraki paketin NX_HTTP_SERVER_TIMEOUT_RECEIVE bekle seçeneği kullanılarak alınmasını bekler.

> [!NOTE]
> Bu, *nx_http_server_get_entity_header* çağrılmadan önce çağrılmamalıdır çünkü varlık üstbilgisinin sonundaki önüne işaretçisini değiştirir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucusu örneğine yönelik işaretçi
 - **packet_ptr** Güncelleştirilmiş önüne işaretçisine sahip paketi döndürmek için paket işaretçisi işaretçisi
 - **CONTENT_LENGTH** Ayıklanan işaretçi ```content_length```

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) http içerik uzunluğu bulundu ve paket başarıyla güncelleştirildi
 - **NX_HTTP_TIMEOUT** (0XE1) süre süresi dolduğunda sonraki pakette bekliyor
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
The server has received a Client request packet, recv_packet_ptr, and the packet
content find service is called from the request notify callback function
registered with the HTTP server. */

UINT content_length;

status =  nx_http_server_packet_content_find(server_ptr, recv_packet_ptr,
                                             &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
   and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_http_server_packet_get"></a>nx_http_server_packet_get

Sonraki HTTP paketini al

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_packet_get(NX_HTTP_SERVER *server_ptr,
                              NX_PACKET **packet_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, HTTP sunucusu yuvasında alınan bir sonraki paketi döndürür. Bir paket almak için bekle seçeneği NX_HTTP_SERVER_TIMEOUT_RECEIVE.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **server_ptr** HTTP sunucusu örneğine yönelik işaretçi
 - **packet_ptr** Alınan paket işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) sonraki paket başarıyla alındı
 - **NX_HTTP_TIMEOUT** (0XE1) süre süresi dolduğunda sonraki pakette bekliyor
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* The HTTP server pointed to by server_ptr is previously created and started. */

UINT content_length;
NX_PACKET *recv_packet_ptr;

status =  nx_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_http_server_param_get"></a>nx_http_server_param_get

İstekten parametre al

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_param_get(NX_PACKET *packet_ptr,
                              UINT param_number, CHAR *param_ptr,
                              UINT max_param_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL parametresini almaya çalışıyor. İstenen HTTP parametresi yoksa, bu yordam NX_HTTP_NOT_FOUND durumunu döndürür. Bu yordam, HTTP sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağrısından çağrılmalıdır (*nx_http_server_create*).

### <a name="input-parameters"></a>Giriş Parametreleri

 - **packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi. Uygulamanın bu paketi serbest bırakmadığını unutmayın.
 - **param_number** Parametre listesinde soldan sağa sıfırdan başlayan parametrenin mantıksal numarası.
 - **param_ptr** Parametreyi kopyalamak için hedef alan.
 - **max_param_size** Parametre hedefi alanının maksimum boyutu.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı http sunucusu parametre al
 - **NX_HTTP_NOT_FOUND** (0xE6) belirtilen parametre bulunamadı
 - **NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) istek parametresi düzgün sonlandırılmadı
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Assuming we are in the application’s request notify callback
   routine, get the first parameter of the HTTP Client request. */

status =  nx_http_server_param_get(request_packet_ptr, 0, param_destination,
               30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
   in “param_destination.” */
```

## <a name="nx_http_server_query_get"></a>nx_http_server_query_get

İstekten sorgu al

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_query_get(NX_PACKET *packet_ptr, UINT query_number,
                   CHAR *query_ptr, UINT max_query_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL sorgusunu almaya çalışıyor. İstenen HTTP sorgusu yoksa, bu yordam NX_HTTP_NOT_FOUND durumunu döndürür. Bu yordam, HTTP sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağrısından çağrılmalıdır (*nx_http_server_create*).

### <a name="input-parameters"></a>Giriş Parametreleri

 - **packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi. Uygulamanın bu paketi serbest bırakmadığını unutmayın.
 - **query_number** Sıfırdan başlayan parametrenin mantıksal numarası, sorgu listesinde soldan sağa.
 - **query_ptr** Sorguyu kopyalamak için hedef alan.
 - **max_query_size** Sorgu hedefi alanının maksimum boyutu.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı http sunucusu sorgusu al
 - **NX_HTTP_FAILED** (0xE2) sorgu boyutu çok küçük.
 - **NX_HTTP_NOT_FOUND** (0xE6) belirtilen sorgu bulunamadı
 - **NX_HTTP_NO_QUERY_PARSED** (0xF2) istemci Isteğinde sorgu yok
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Assuming we are in the application’s request notify callback
   routine, get the first query of the HTTP Client request. */
status =  nx_http_server_query_get(request_packet_ptr, 0, query_destination,
                30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
   in “query_destination.” */
```

## <a name="nx_http_server_start"></a>nx_http_server_start

HTTP sunucusunu başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_start(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturma HTTP sunucu örneğini başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı sunucu başlatması
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the HTTP Server instance “my_server.”  */
status =  nx_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_http_server_stop"></a>nx_http_server_stop

HTTP sunucusunu durdur

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_stop(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturma HTTP sunucu örneğini durduruyor. Bu yordam, bir HTTP sunucu örneği silinmeden önce çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) başarılı sunucu durdu
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the HTTP Server instance “my_server.”  */
status =  nx_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_http_server_type_get"></a>nx_http_server_type_get

Istemci HTTP isteğinden dosya türünü Ayıkla

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_type_get(NX_HTTP_SERVER *http_server_ptr,
                             CHAR *name, CHAR *http_type_string);
```

### <a name="description"></a>Açıklama

> [!NOTE]
> Bu hizmet kullanımdan kaldırılmıştır. Kullanıcıların *nx_http_server_type_retrieve ()* hizmetini kullanması önerilir.

Bu hizmet, arabellek http_type_string HTTP istek türünü ve giriş arabelleği adından (genellikle URL) gelen dönüş değerindeki uzunluğu ayıklar. MIME eşlemesi bulunmazsa, varsayılan olarak "metin/düz" tür olur. Aksi takdirde, bir eşleşme için ayıklanan tür, HTTP sunucusu varsayılan MIME eşlemeleriyle karşılaştırılır. NetX Duo HTTP sunucusundaki varsayılan MIME haritaları şunlardır:

 - **HTML** metni/HTML
 - **htm** metin/html
 - **txt** metin/düz
 - **GIF** resmi/GIF
 - **jpg** resmi/JPEG
 - **ICO** resmi/x-simgesi

Sağlanırsa, Kullanıcı tanımlı ek MIME haritaları kümesi de arar. Kullanıcı tanımlı haritalar hakkında daha fazla bilgi için bkz. *nx_http_server_mime_maps_addtional_set ()* .

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_http_server_type_get_extended ()* uygulamasına geçirilmesi önerilir.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi
 - Aranacak arabelleğe yönelik **işaretçiyi adlandırın**
 - **http_type_string** (ayıklanan HTML türüne yönelik işaretçi)

### <a name="return-values"></a>Dönüş Değerleri

 - **Bayt cinsinden dize uzunluğu** Sıfır olmayan değer başarılı. Sıfır hatayı gösterir.

### <a name="allowed-from"></a>İzin verilen

Uygulama

### <a name="example"></a>Örnek

```c
/* my_server is a previously created HTTP server, which starts accepting client
   requests when nx_http_server_start is called*/

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
    string_length =  nx_http_server_type_get(&my_server_ptr,
                my_server.nx_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
```

## <a name="nx_http_server_type_get_extended"></a>nx_http_server_type_get_extended

Istemci HTTP isteğinden dosya türünü Ayıkla

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_type_get_extended(
                                    NX_HTTP_SERVER *http_server_ptr,
                                    CHAR *name, CHAR *http_type_string,
                                    UINT http_type_string_max_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, arabellek *HTTP_TYPE_STRING* http istek türünü ve giriş arabelleği *ADıNDAN*(genellikle URL) gelen dönüş değerindeki uzunluğu ayıklar. MIME eşlemesi bulunmazsa, varsayılan olarak "metin/düz" tür olur. Aksi takdirde, bir eşleşme için ayıklanan tür, HTTP sunucusu varsayılan MIME eşlemeleriyle karşılaştırılır. NetX Duo HTTP sunucusundaki varsayılan MIME haritaları şunlardır:

 - **HTML** metni/HTML
 - **htm** metin/html
 - **txt** metin/düz
 - **GIF** resmi/GIF
 - **jpg** resmi/JPEG
 - **ICO** resmi/x-simgesi

Sağlanırsa, Kullanıcı tanımlı ek MIME haritaları kümesi de arar. Kullanıcı tanımlı haritalar hakkında daha fazla bilgi için bkz. *nx_http_server_mime_maps_addtional_set ()* .

Bu hizmet *nx_http_server_type_get ()* yerini alır. Bu sürüm, ek uzunluk bilgilerini sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi
 - **ad** Aranacak arabelleğin işaretçisi
 - **name_length** Aranacak arabelleğin uzunluğu
 - **http_type_string** (ayıklanan HTML türüne yönelik işaretçi)
 - **http_type_string_max_size** Http_type_string arabelleğinin boyutu

### <a name="return-values"></a>Dönüş Değerleri

 - **Bayt cinsinden dize uzunluğu** Sıfır olmayan değer başarılı. Sıfır hatayı gösterir.

### <a name="allowed-from"></a>İzin verilen

Uygulama

### <a name="example"></a>Örnek

```c
/* my_server is a previously created HTTP server, which starts accepting client
   requests when nx_http_server_start is called*/

CHAR temp_string[20];
UINT string_length;

/* Get the length of request resource. */
    if (_nx_utility_string_length_check(
                    my_server.nx_http_server_request_resource, &resource_length,
                    sizeof(my_server.nx_http_server_request_resource) - 1))
           {
               return;
           }

/* Extract the HTTP type. */
    string_length =  nx_http_server_type_get_extended(&my_server,
               my_server.nx_http_server_request_resource, resource_length,
               temp_string, sizeof(temp_string));

/* If string_length is non zero, the HTTP string is extracted. */
```

Daha ayrıntılı bir örnek için [*nx_http_server_callback_generate_response_header*](#nx_http_server_callback_generate_response_header)açıklamasına bakın.

## <a name="nx_http_server_digest_authenticate_notify_set"></a>nx_http_server_digest_authenticate_notify_set

Özet kimlik doğrulaması geri arama işlevini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_digest_authenticate_notify_set(
       NX_HTTP_SERVER *http_server_ptr,
       UINT (*digest_authenticate_callback)(NX_HTTP_SERVER *server_ptr,
                                            CHAR *name_ptr,
                                            CHAR *realm_ptr,
                                            CHAR *password_ptr,
                                            CHAR *method,
                                            CHAR *authorization_uri,
                                            CHAR *authorization_nc,
                                            CHAR *authorization_cnonce
                                           ));
```

### <a name="description"></a>Açıklama

Bu hizmet Özet kimlik doğrulaması gerçekleştirildiğinde çağrılan geri aramayı ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi
 - **digest_authenticate_callback** Özet kimlik doğrulaması geri çağırma işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
 - NX_NOT_SUPPORTED (0x4B) Özet kimlik doğrulaması etkin değil

### <a name="allowed-from"></a>İzin verilen

Uygulama

### <a name="example"></a>Örnek

```c
UINT digest_authenticate_callback(NX_HTTP_SERVER *server_ptr, CHAR *name_ptr,
                                  CHAR *realm_ptr, CHAR *password_ptr, CHAR *method,
                                  CHAR *authorization_uri, CHAR *authorization_nc,
                                  CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the digest authenticate callback: */

status =  nx_http_server_digest_authenticate_notify_set (&my_server,
    digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
   will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_http_server_authentication_check_set"></a>nx_http_server_authentication_check_set

Kimlik doğrulama denetimi geri arama işlevini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_http_server_authentication_check_set(
       NX_HTTP_SERVER *http_server_ptr,
       UINT (*authentication_check_extended)(
                                            NX_HTTP_SERVER *server_ptr,
                                            UINT request_type,
                                            CHAR *resource,
                                            CHAR **name,
                                            UINT *name_length,
                                            CHAR **password,
                                            UINT *password_length,
                                            CHAR **realm,
                                            UINT *realm_length
                                            ));
```

### <a name="description"></a>Açıklama

Bu hizmet, kimlik doğrulama denetiminin geri çağırma işlevini ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

 - **http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi
 - **authentication_check_extended** Uygulamanın kimlik doğrulama denetimi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

 - **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
 - NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Uygulama

### <a name="example"></a>Örnek

```c
static UINT  authentication_check_extended(NX_HTTP_SERVER *server_ptr,
                                           UINT request_type, CHAR *resource,
                                           CHAR **name, UINT *name_length,
                                           CHAR **password, UINT *password_length,
                                           CHAR **realm, UINT *realm_length)
{

    /* Just use a simple name, password, and realm for all
       requests and resources. */
    *name =     "name";
    *password = "password";
    *realm =    "NetX Duo HTTP demo";
    *name_length = 4;
    *password_length = 8;
    *realm_length = 18;

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the
   authentication checking callback: */

nx_http_server_authentication_check_set (&my_server,
                                         authentication_check_extended);
```
