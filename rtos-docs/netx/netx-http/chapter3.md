---
title: Bölüm 3 - NetX HTTP hizmetlerinin açıklaması
description: Bu bölümde, tüm NetX HTTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: eabb455b6e21b4fe51db944a0da12afa85ee390a78db633ee670de5aadcde07b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791525"
---
# <a name="chapter-3---description-of-netx-http-services"></a>Bölüm 3 - NetX HTTP hizmetlerinin açıklaması

Bu bölümde, tüm NetX HTTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

**HTTP İstemcisi hizmetleri:**

- nx_http_client_create HTTP *İstemci Örneği Oluşturma*
- nx_http_client_delete HTTP *İstemcisi örneğini silme*
- nx_http_client_get_start HTTP *GET isteği başlatma*
- nx_http_client_get_start_extended HTTP *GET isteği başlatma*
- nx_http_client_get_packet *kaynak veri paketini al*
- nx_http_client_put_start HTTP *PUT isteği başlatma*
- nx_http_client_put_start_extended HTTP *PUT isteği başlatma*
- nx_http_client_put_packet kaynak *veri paketini gönder'i seçin*
- *nx_http_client_set_connect_port* *HTTP Sunucusuna bağlanmak için bağlantı noktasını değiştirme*

**HTTP Sunucusu hizmetleri:**

- nx_http_server_cache_info_callback_set *URL'nin yaş ve son değiştirme tarihini almak için geri çağırmayı ayarlayın*
- nx_http_server_callback_data_send *işlevinden HTTP verileri gönderme*
- nx_http_server_callback_generate_response_header *işlevlerinde yanıt üst bilgisi oluşturma*
- nx_http_server_callback_generate_response_header_extended *işlevlerinde yanıt üst bilgisi oluşturma*
- nx_http_server_callback_packet_send *HTTP geri çağırmadan HTTP paketi gönderme*
- nx_http_server_callback_response_send *işlevinden yanıt gönderme*
- nx_http_server_callback_response_send_extended *işlevinden yanıt gönderme*
- nx_http_server_content_get içeriği *al'a*
- nx_http_server_content_get_extended içeriği *al; boş (sıfır İçerik Uzunluğu) isteklerini destekler*
- nx_http_server_content_length_get *içeriğinin uzunluğunu al*
- nx_http_server_content_length_get_extended *içeriğinin uzunluğunu al; boş (sıfır İçerik Uzunluğu) isteklerini destekler*
- nx_http_server_create HTTP *Sunucusu örneği oluşturma*
- nx_http_server_delete HTTP *Sunucusu örneğini silme*
- nx_http_server_get_entity_content *URL'de varlık içeriğinin dönüş boyutu ve konumu*
- nx_http_server_get_entity_header *URL varlık üst bilgilerini belirtilen arabelleğe ayıklama*
- nx_http_server_gmt_callback_set *GMT tarih ve saati almak için geri çağırmayı ayarlama*
- nx_http_server_invalid_userpassword_notify_set İstemci *isteğinde geçersiz kullanıcı adı ve parolanın ne zaman* alın aldığına göre geri çağırmayı ayarlayın
- nx_http_server_mime_maps_additional_set HTML *için ek mime eşlemeleri tanımlama*
- nx_http_server_packet_content_find *HTTP üst bilgisinde içerik uzunluğunu ayıkla ve içerik verilerini başlatmak için işaretçiyi ayarla*
- nx_http_server_packet_get istemci *paketini doğrudan alma*
- nx_http_server_param_get get *parametresini kullanın*
- nx_http_server_query_get *sorguyu al*
- nx_http_server_start *HTTP Sunucusunu Başlat*
- nx_http_server_stop Http *Sunucusunu Durdur*
- nx_http_server_type_get HTTP *türünü ayıkla (ör. üst bilgiden text/plain)*
- nx_http_server_type_get_extended *HTTP türünü ayıkla (ör. üst bilgiden text/plain)*
- nx_http_server_digest_authenticate_notify_set Özet *kimlik doğrulaması geri çağırma işlevini ayarlama*
- nx_http_server_authentication_check_set *doğrulama denetimi geri çağırma işlevini ayarlama*

## <a name="nx_http_client_create"></a>nx_http_client_create

### <a name="create-an-http-client-instance"></a>HTTP İstemci Örneği oluşturma

**Prototip**

```c
UINT nx_http_client_create(NX_HTTP_CLIENT *client_ptr,
                          CHAR *client_name, NX_IP *ip_ptr, 
                          NX_PACKET_POOL *pool_ptr,
                          ULONG window_size);
```

**Açıklama**

Bu hizmet, belirtilen IP örneğinde bir HTTP İstemcisi örneği oluşturur.

**Giriş Parametreleri**

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **client_name** HTTP İstemcisi örneğinin adı.
- **ip_ptr** IP örneğine işaretçi.
- **pool_ptr** Varsayılan paket havuzunun işaretçisi. Bu havuza gelen paketlerin tam yanıt üst bilgisini işlemek için yeterince büyük bir yüke sahip olması gerektiğini unutmayın. Bu, *nx_http_client.h* NX_HTTP_CLIENT_MIN_PACKET_SIZE tarafından tanımlanır.
- **window_size** İstemcinin TCP yuvası alma penceresinin boyutu.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Başarılı HTTP İstemcisi oluşturma
- NX_PTR_ERROR (0x16) Geçersiz HTTP, ip_ptr veya paket havuzu işaretçisi
- NX_HTTP_POOL_ERROR(0xE9) Paket havuzunda geçersiz yük boyutu

**İzin Verilen**

Başlatma, İş Parçacıkları

**Örnek**

```c
/* Create the HTTP Client instance “my_client” on “ip_0”. */
status = nx_http_client_create(&my_client, “my client”, &ip_0, &pool_0, 100);
  
/* If status is NX_SUCCESS an HTTP Client instance was successfully  created. */
```

## <a name="nx_http_client_delete"></a>nx_http_client_delete

### <a name="delete-an-http-client-instance"></a>HTTP İstemci Örneğini Silme

**Prototip**

```c
UINT nx_http_client_delete(NX_HTTP_CLIENT *client_ptr);
```

**Açıklama**

Bu hizmet, daha önce oluşturulmuş bir HTTP İstemcisi örneğini siler.

**Giriş Parametreleri**

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Başarılı HTTP İstemcisi silme
- NX_PTR_ERROR (0x16) Geçersiz HTTP işaretçisi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
/* Delete the HTTP Client instance “my_client.” */
status = nx_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully  deleted. */
```

## <a name="nx_http_client_get_start"></a>nx_http_client_get_start

### <a name="start-an-http-get-request"></a>HTTP GET isteği başlatma

**Prototip**

```c
UINT nx_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
                             ULONG ip_address, CHAR *resource, CHAR *input_ptr,
                             UINT input_size, CHAR *username, CHAR *password,
                             ULONG wait_option);
```

**Açıklama**

Bu hizmet, daha önce oluşturulan HTTP İstemcisi örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı ALMAYA çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama istenen kaynak *içeriğine karşılık gelen veri paketlerini nx_http_client_get_packet* için birden çok çağrı nx_http_client_get_packet çağrısında olabilir.

Kaynak dizesinin "/index.htm" gibi yerel bir dosyaya başvurana veya başka bir URL'ye başvura(örneğin, HTTP Sunucusu başvurulan GET isteklerini desteklediğini gösteriyorsa) dikkat `http://abc.website.com/index.htm` edin.

Bu hizmet kullanım dışıdır. Geliştiricilerin *nx_http_client_get_start_extended() nx_http_client_get_start_extended*

**Giriş Parametreleri**

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **kaynak** İstenen kaynak için URL dizesi işaretçisi.
- **input_ptr** GET isteği için ek verilerin işaretçisi. Bu isteğe bağlıdır. Geçerli ise, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine post kullanılır.
- **input_size** Isteğe bağlı ek girişte yer alan bayt sayısı, input_ptr.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
-**wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman out değeri** (0x00000001 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />Bu TX_WAIT_FOREVER, HTTP Sunucusu i isteği yanıtlayana kadar çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.<br />Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtını beklerken askıya alınan süreölçer saat sayısı üst sayısını belirtir.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Başarıyla gönderilen HTTP İstemcisi GET başlangıç iletisi
- **NX_HTTP_ERROR** (0xE0) İç HTTP İstemcisi hatası
- **NX_HTTP_NOT_READY** (0xEA) HTTP İstemcisi hazır değil
- **NX_HTTP_FAILED** (0xE2) HTTP Sunucusu ile iletişim kurarken HTTP İstemcisi hatası.
- **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                  NX_NULL, 0, “myname”, “mypassword”, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
far successful. The client must now call *nx_http_client_get_packet* multiple
times to retrieve the content associated with TEST.HTM. */

#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                  POST_MESSAGE, sizeof(POST_MESSAGE),
                                  “myname”, “mypassword”, 1000);
 
/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST 
request for TEST.HTM and successfully sent. */
```


## <a name="nx_http_client_get_start_extended"></a>nx_http_client_get_start_extended

### <a name="start-an-http-get-request"></a>HTTP GET isteği başlatma

**Prototip**

```c
UINT nx_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
     ULONG ip_address, CHAR *resource, UINT resource_length,
     CHAR *input_ptr, UINT input_size, CHAR *username,
     UINT username_length, CHAR *password, UINT password_length,
     ULONG wait_option);
```

**Açıklama**

Bu hizmet, daha önce oluşturulan HTTP İstemcisi örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı ALMAYA çalışır. Bu yordam NX_SUCCESS döndürürse, uygulama istenen kaynak *içeriğine karşılık gelen veri paketlerini nx_http_client_get_packet* için birden çok çağrı nx_http_client_get_packet çağrısında olabilir.

Kaynak dizesinin "/index.htm" gibi yerel bir dosyaya başvurana veya başka bir URL'ye başvura(örneğin, HTTP Sunucusu başvurulan GET isteklerini desteklediğini gösteriyorsa) dikkat `http://abc.website.com/index.htm` edin.

Bu hizmet, *nx_http_client_get_start() ile değiştirilir.* Çağıranın kaynağın uzunluğunu, kullanıcı adını ve parolayı belirtmesini gerektirir.

**Giriş Parametreleri**

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **kaynak** İstenen kaynak için URL dizesi işaretçisi.
- **resource_length** İstenen kaynak için URL dizesinin uzunluğu.
- **input_ptr** GET isteği için ek verilerin işaretçisi. Bu isteğe bağlıdır. Geçerli ise, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine post kullanılır.
- **input_size** Isteğe bağlı ek girişte yer alan bayt sayısı, input_ptr.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için isteğe bağlı parola uzunluğu.
- **wait_option** Hizmetin HTTP İstemcisi'nin başlangıç isteğini ne kadar süre bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman out değeri** (0x00000001 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />Bu TX_WAIT_FOREVER, HTTP Sunucusu i isteği yanıtlayana kadar çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.<br />Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtını beklerken askıya alınan süreölçer saat sayısı üst sayısını belirtir.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Başarıyla gönderilen HTTP İstemcisi GET başlangıç iletisi
- **NX_HTTP_ERROR** (0xE0) İç HTTP İstemcisi hatası
- **NX_HTTP_NOT_READY** (0xEA) HTTP İstemcisi hazır değil
- **NX_HTTP_FAILED** (0xE2) HTTP Sunucusu ile iletişim kurarken HTTP İstemcisi hatası.
- **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Geçersiz ad ve/veya parola.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz.

**İzin Verilen**

İş Parçacıkları

**Örnek**
            
```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5),
                                           “/TEST.HTM”,
                                           9, NX_NULL, 0, “myname”, 6,
                                           “mypassword”, 10, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
far successful. The client must now call *nx_http_client_get_packet* multiple
times to retrieve the content associated with TEST.HTM. */

#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5), 
                                           “/TEST.HTM”,
                                           9, POST_MESSAGE, sizeof(POST_MESSAGE),
                                           “myname”, 6, “mypassword”, 10, 1000);

/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST 
request for TEST.HTM and successfully sent. */
```

## <a name="nx_http_client_get_packet"></a>nx_http_client_get_packet

### <a name="get-next-resource-data-packet"></a>Sonraki kaynak veri paketini alın

**Prototip**

```c
UINT nx_http_client_get_packet(NX_HTTP_CLIENT *client_ptr,
                              NX_PACKET **packet_ptr,
                              ULONG wait_option);
```

**Açıklama**

Bu hizmet, önceki nx_http_client_get_start çağrısı tarafından istenen kaynağın sonraki *içerik nx_http_client_get_start* alınır. Bu yordama yapılan başarılı çağrılar, uygulamanın dönüş durumu alınana NX_HTTP_GET_DONE gerekir.

**Giriş Parametreleri**

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **packet_ptr** Kısmi kaynak içeriği içeren paket işaretçisi için hedef.
- **wait_option** Hizmetin HTTP İstemcisi paket almak için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />Bu TX_WAIT_FOREVER, HTTP Sunucusu i isteği yanıtlayana kadar çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.<br />Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtını beklerken askıya alınan süreölçer saat sayısı üst sayısını belirtir.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Başarılı HTTP İstemcisi get paketi.
- **NX_HTTP_GET_DONE** (0xEC) HTTP İstemcisi get paketi bitti
- **NX_HTTP_NOT_READY** (0xEA) HTTP İstemcisi get modunda değil.
- **NX_HTTP_BAD_PACKET_LENGTH** (0xED) Geçersiz paket uzunluğu
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
/* Get the next packet of resource content on the HTTP Client “my_client.”
Note that the nx_http_client_get_start routine must have been called
previously. */
status = nx_http_client_get_packet(&my_client, &next_packet, 1000);
 
/* If status is NX_SUCCESS, the next packet of content is pointed to by 
“next_packet”. */
```

## <a name="nx_http_client_put_start"></a>nx_http_client_put_start

### <a name="start-an-http-put-request"></a>HTTP PUT isteği başlatma 

**Prototip**

```c
UINT nx_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                             ULONG ip_address, CHAR *resource,
                             CHAR *username, CHAR *password,
                             ULONG total_bytes, ULONG wait_option);
```

**Açıklama**

Bu hizmet, belirtilen kaynağa sahip bir PUT isteğini sağlanan IP adresinden HTTP Sunucusuna göndermeye çalışır. Bu yordam başarılı olursa, kaynak içeriklerini HTTP Sunucusuna göndermek *için uygulama nx_http_client_put_packet* yordama başarıyla çağrılar yapmaları gerekir.

Kaynak dizesinin "/index.htm" gibi yerel bir dosyaya başvurarak veya başka bir URL'ye başvurabilirsiniz. Örneğin HTTP Sunucusu, PUT isteklerini desteklediğini `http://abc.website.com/index.htm` gösteriyorsa.

Bu hizmet kullanım dışıdır. Geliştiricilerin *nx_http_client_put_start_extended() 'a geçişleri teşvik edilecektir.*

**Giriş Parametreleri**

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **kaynak** Kaynağın Sunucuya göndermesi için URL dizesinin işaretçisi.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **total_bytes** Gönderilen kaynağın toplam bayt sayısı. Sonraki çağrılar aracılığıyla gönderilen tüm paketlerin birleşik uzunluğunun nx_http_client_put_packet *bu* değere eşit olması gerektiğini unutmayın.
- **wait_option** Hizmetin HTTP İstemcisi PUT başlatması için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />Bu TX_WAIT_FOREVER, HTTP Sunucusu i isteği yanıtlayana kadar çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.<br />Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtını beklerken askıya alınan süreölçer saat sayısı üst sayısını belirtir.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Put isteği başarıyla gönderildi
- **NX_HTTP_USERNAME_TOO_LONG**
- **(0xF1) Kullanıcı adı arabellek için fazla büyük**
- **NX_HTTP_NOT_READY** (0xEA) HTTP İstemcisi hazır değil
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Kaynağın toplam boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP 
Server at IP address 1.2.3.5. */
status = nx_http_client_put_start(&my_client, IP_ADDRESS(1, 2, 3, 5),
                                 “/TEST.HTM”, “myname”, “mypassword”, 20, 
                                 NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully 
been started. */
```

## <a name="nx_http_client_put_start_extended"></a>nx_http_client_put_start_extended

### <a name="start-an-http-put-request"></a>HTTP PUT isteği başlatma

**Prototip**

```c
UINT nx_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
     ULONG ip_address, CHAR *resource, UINT resource_length,
     CHAR *username,UINT username_length, CHAR *password,
     UINT password_length, ULONG total_bytes, ULONG wait_option);
```

**Açıklama**

Bu hizmet, belirtilen kaynağa sahip bir PUT isteğini sağlanan IP adresinden HTTP Sunucusuna göndermeye çalışır. Bu yordam başarılı olursa, kaynak içeriklerini HTTP Sunucusuna göndermek *için uygulama nx_http_client_put_packet* yordama başarıyla çağrılar yapmaları gerekir.

Kaynak dizesinin "/index.htm" gibi yerel bir dosyaya başvurarak veya başka bir URL'ye başvurabilirsiniz. Örneğin HTTP Sunucusu, PUT isteklerini desteklediğini `http://abc.website.com/index.htm` gösteriyorsa.

Bu hizmet, *nx_http_client_put_start() ile değiştirilir.* Çağıranın kaynağın uzunluğunu, kullanıcı adını ve parolayı belirtmesini gerektirir.

**Giriş Parametreleri**

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **ip_address** HTTP Sunucusunun IP adresi.
- **kaynak** Kaynağın Sunucuya göndermesi için URL dizesinin işaretçisi.
- **resource_length** Sunucuya göndermek istediğiniz kaynağın URL dizesinin uzunluğu.
- **kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adının işaretçisi.
- **username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.
- **parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.
- **password_length** Kimlik doğrulaması için isteğe bağlı parola uzunluğu.
- **total_bytes** Gönderilen kaynağın toplam bayt sayısı. Sonraki çağrılar aracılığıyla gönderilen tüm paketlerin birleşik uzunluğunun nx_http_client_put_packet *bu* değere eşit olması gerektiğini unutmayın.
- **wait_option** Hizmetin HTTP İstemcisi PUT başlatması için ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />Bu TX_WAIT_FOREVER, HTTP Sunucusu i isteği yanıtlayana kadar çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.<br />Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtını beklerken askıya alınan süreölçer saat sayısı üst sayısını belirtir.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Put isteği başarıyla gönderildi
- **NX_HTTP_USERNAME_TOO_LONG** (0xF1) Kullanıcı Adı arabellek için fazla büyük
- **NX_HTTP_NOT_READY** (0xEA) HTTP İstemcisi hazır değil
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_SIZE_ERROR (0x09) Kaynağın toplam boyutu geçersiz
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP 
Server at IP address 1.2.3.5. */
status = nx_http_client_put_start_extended(&my_client, IP_ADDRESS(1, 2, 3, 5),
                                          “/TEST.HTM”, 9, “myname”, 6, 
                                          “mypassword”, 
                                          10, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully 
been started. */
```

## <a name="nx_http_client_put_packet"></a>nx_http_client_put_packet

### <a name="send-next-resource-data-packet"></a>Sonraki kaynak veri paketini gönder

**Prototip**

```c
UINT nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                              NX_PACKET *packet_ptr,
                              ULONG wait_option);
```

**Açıklama**

Bu hizmet, bir sonraki kaynak içeriği paketini HTTP Sunucusuna göndermeye çalışır. Bu yordamın, gönderilen paketlerin birleşik uzunluğu önceki nx_http_client_put_start() çağrısında belirtilen "total_bytes" ile eşit olana kadar tekrar tekrar *çağrıl* gerektiğini unutmayın.

**Giriş Parametreleri**

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **packet_ptr** HTTP Sunucusuna gönderilecek kaynağın sonraki içeriğinin işaretçisi.
- **wait_option** Hizmetin HTTP İstemcisi PUT paketini işlemesi için dahili olarak ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />Bu TX_WAIT_FOREVER, HTTP Sunucusu i isteği yanıtlayana kadar çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.<br /> Sayısal bir değer (0x1-0xFFFFFFFE) seçmek, HTTP Sunucusu yanıtını beklerken askıya alınan süreölçer saat sayısı üst sayısını belirtir.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Http İstemci paketi başarıyla gönderildi.
- **NX_HTTP_NOT_READY** (0xEA) HTTP İstemcisi hazır değil
- **NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0xEE) Alınan Sunucu hata kodu** -**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Geçersiz paket uzunluğu
- **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Geçersiz ad ve/veya Parola
- **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Sunucusu PUT Tamamlandıktan önce yanıt verir
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_INVALID_PACKET (0x12) Paketi TCP üst bilgisi için çok küçük
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
/* Send a 20-byte packet representing the content of the resource
“/TEST.HTM” to the HTTP Server. */
status = nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                                  NX_PACKET *packet_ptr,
                                  ULONG wait_option);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM
has successfully been sent. */
```

## <a name="nx_http_client_set_connect_port"></a>nx_http_client_set_connect_port

### <a name="set-the-connection-port-to-the-server"></a>Bağlantı bağlantı noktasını Sunucu olarak ayarlayın

**Prototip**

```c
UINT nx_http_client_set_connect_port(NX_HTTP_CLIENT *client_ptr,
                                    UINT port);
```

**Açıklama**

Bu hizmet, http sunucusuna çalışma zamanında belirtilen bağlantı noktasına bağlanırken bağlantı noktasını değiştirir. Aksi takdirde bağlantı noktası varsayılan olarak 80'i kullanır. Http İstemcisi *Sunucuyla bağlantı nx_http_client_get_start*() *nx_http_client_put_start*() ve daha önce çağrılmaları gerekir.

**Giriş Parametreleri**

- **client_ptr** HTTP İstemcisi denetim bloğu işaretçisi.
- **bağlantı noktası** Sunucuya bağlanmak için bağlantı noktası.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Bağlantı noktası başarıyla değiştirildi
- **NX_INVALID_PORT** (0x46) Bağlantı noktası üst sınırı (0xFFFF) veya sıfırdır.
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

**İzin Verilen**

İş Parçacıkları, Başlatma

**Örnek**

```c
NX_HTTP_CLIENT *client_ptr;

/* Change the connect port to 114. */
status = nx_http_client_set_connect_port(client_ptr, 114);

/* If status is NX_SUCCESS, the connect port is successfully changed. */
```

## <a name="nx_http_server_cache_info_callback_set"></a>nx_http_server_cache_info_callback_set

### <a name="set-the-callback-to-retrieve-url-max-age-and-date"></a>En fazla yaş ve tarih URL'sini almak için geri çağırmayı ayarlayın

**Prototip**

```c
UINT nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                                           UINT (*cache_info_get)(CHAR *resource,
                                           UINT *max_age,
                                           NX_HTTP_SERVER_DATE *date));
```

**Açıklama**

Bu hizmet, belirtilen kaynağın en uzun yaş ve son değiştirme tarihini almak için çağrılan geri çağırma hizmetini ayarlar.

**Giriş Parametreleri**

- **server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **cache_info_get** Geri çağırma işaretçisi
- **max_age** Bir kaynağın maksimum yaşı işaretçisi
- **veri** Son değiştirme tarihine yönelik işaretçi döndürüldü.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi

**İzin verilen**

Başlatma

**Örnek**

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

### <a name="send-data-from-callback-function"></a>Geri çağırma işlevinden veri Gönder

**Örneğini**

```c
UINT nx_http_server_callback_data_send(NX_HTTP_SERVER *server_ptr,
                                      VOID *data_ptr,
                                      ULONG data_length);
```

**Açıklama**

Bu hizmet, sağlanan paketteki verileri uygulamanın geri arama yordamından gönderir. Bu, genellikle GET/POST istekleri ile ilişkili dinamik verileri göndermek için kullanılır. Bu işlev kullanıldığında, tüm yanıtın doğru biçimde gönderilmesi için geri çağırma yordamının sorumlu olduğunu unutmayın. Ayrıca, geri arama yordamı NX_HTTP_CALLBACK_COMPLETED durumunu döndürmelidir.

**Giriş parametreleri**

- **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
- **data_ptr** Gönderilen verilerin işaretçisi.
- **data_length** Gönderilen bayt sayısı.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu verilerini başarıyla gönderdi
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
       (strcmp(resource, "/test.htm") == 0))
    {
        /* Found it, override the GET processing by sending the resource
        contents directly. */

        nx_http_server_callback_data_send(server_ptr,
                                         "HTTP/1.0 200 \r\nContent-Length:
                                         103\r\nContent-Type: text/html\r\n\r\n",
                                         63);
        nx_http_server_callback_data_send(server_ptr, "<HTML>> r\n<HEAD><TITLE>NetX
                                         HTTP Test </TITLE></HEAD>\r\n
                                         <BODY>\r\n<H1>NetX Test Page
                                         </H1>\r\n</BODY>> r\n</HTML>\r\n", 103);
        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }
    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_generate_response_header"></a>nx_http_server_callback_generate_response_header

### <a name="create-a-response-header-in-a-callback-function"></a>Geri arama işlevinde yanıt üst bilgisi oluşturma

**Örneğini**

```c
UINT nx_http_server_callback_generate_response_header(NX_HTTP_SERVER *server_ptr,
     NX_PACKET **packet_pptr, CHAR *status_code, UINT content_length,
     CHAR *content_type, CHAR* additional_header);
```

**Açıklama**

HTTP sunucusu Istemci GET, put ve DELETE isteklerine yanıt verdiğinde, bu hizmet _ *nx_http_server_generate_response_header* iç işlevini çağırır. HTTP sunucusu uygulaması Istemciye yanıtını tasarlarken HTTP sunucusu geri çağırma işlevlerinde kullanılmak üzere tasarlanmıştır.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nxd_http_server_callback_generate_response_header_extended ()* uygulamasına geçirilmesi önerilir.

**Giriş parametreleri**

- **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
- **packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi
- **status_code** Kaynağın durumunu belirtin. Örnekler:
- **NX_HTTP_STATUS_OK**
- **NX_HTTP_STATUS_MODIFIED**
- **NX_HTTP_STATUS_INTERNAL_ERROR**
- **CONTENT_LENGTH** İçerik boyutu (bayt)
- **content_type** HTTP türü, örneğin "metin/düz"
- **additional_header** Ek üst bilgi metnine yönelik işaretçi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) HTML üst bilgisi başarıyla oluşturuldu
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
CHAR demotestbuffer[] = “<html>\r\n\r\n<head> r\n\r\n<title>Main                 \
                        Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n  \ 
                        </body>\r\n</html>\r\n";

/* my_request_notify is the application request notify callback registered with
the HTTP server in nx_http_server_create, creates a response to the received
Client request. */

UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET     *sresp_packet_ptr;
    ULONG         string_length;
    CHAR          temp_string[30];
    ULONG         length = 0;

        length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length = (ULONG) nx_http_server_type_get(server_ptr, server_ptr ->
                   nx_http_server_request_resource, temp_string);

/* Null terminate the string. */
   temp_string[temp] = 0;

/* Now build a response header with server status is OK and no additional header info. */
   status = nx_http_server_callback_generate_response_header(http_server_ptr,
            &resp_packet_ptr, NX_HTTP_STATUS_OK,
            length, temp_string, NX_NULL);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
            length, server_ptr >>
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

### <a name="create-a-response-header-in-a-callback-function"></a>Geri arama işlevinde yanıt üst bilgisi oluşturma

**Örneğini**

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

**Açıklama**

Bu hizmet, HTTP sunucusu Istemci GET, put ve DELETE isteklerine yanıt verdiğinde _ *nx_http_server_generate_response_header ()* iç işlevini çağırır. HTTP sunucusu uygulaması Istemciye yanıtını tasarlarken HTTP sunucusu geri çağırma işlevlerinde kullanılmak üzere tasarlanmıştır.

Bu hizmet *nx_http_server_callback_generate_response_header ()* yerini alır. Bu sürüm, geri çağırma işlevine ek uzunluk bilgileri sağlar.

**Giriş parametreleri**

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

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) başarıyla oluşturuldu üst bilgisi
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
  CHAR demotestbuffer[] = “<html>\r\n\r\n<head>\r\n\r\n<title>Main                    \
                          Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n     \
                          </body>\r\n</html>\r\n";

/* my_request_notify is the application request notify callback registered with
   the HTTP server in nx_http_server_create, creates a response to the received
   Client request. */

   UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                         CHAR *resource, NX_PACKET *recv_packet_ptr)
   {
     NX_PACKET *sresp_packet_ptr;
     ULONG string_length;
     CHAR temp_string[30];
     ULONG length = 0;

     length = sizeof(demotestbuffer) - 1;

    /* Derive the client request type from the client request. */
       string_length = (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr >>
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
                length, server_ptr ->
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

### <a name="send-an-http-packet-from-callback-function"></a>Geri çağırma işlevinden HTTP paketi gönder

**Örneğini**

```c
UINT nx_http_server_callback_packet_send(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET *packet_ptr);
```

**Açıklama**

Bu hizmet, HTTP geri çağrısından gelen bir HTTP Sunucu yanıtı gönderir. HTTP sunucusu, paketi NX_HTTP_SERVER _TIMEOUT_SEND gönderecek. HTTP üst bilgisi ve verilerinin pakete eklenmesi gerekir. Dönüş durumu bir hata gösteriyorsa, HTTP uygulaması paketi serbest bırakmalıdır.

Geri çağırma NX_HTTP_CALLBACK_COMPLETED döndürmelidir.

Daha ayrıntılı bir örnek için bkz. *nx_http_server_callback_generate_response_header ()* .

**Giriş parametreleri**

- **server_ptr** HTTP sunucu denetim bloğu işaretçisi
- **packet_ptr** Gönderilmek üzere paket işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) http sunucusu paketini başarıyla gönderdi
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
/* The packet is appended with HTTP header and data and is ready to send to the
Client directly. */

   status = nx_http_server_callback_response_send**(server_ptr, packet_ptr);
   
   if (status != NX_SUCCESS)
   {
        nx_packet_release(packet_ptr);
   }
    return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_callback_response_send"></a>nx_http_server_callback_response_send

### <a name="send-response-from-callback-function"></a>Geri çağırma işlevinden yanıt gönder

**Örneğini**

```c
UINT nx_http_server_callback_response_send(NX_HTTP_SERVER *server_ptr,
     CHAR *header, CHAR *information, CHAR additional_info);
```

**Açıklama**

Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir. Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır. Bu işlev kullanıldığında, geri çağırma yordamının NX_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerektiğini unutmayın.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_http_server_callback_response_send_extended ()* uygulamasına geçirilmesi önerilir.

**Giriş parametreleri**

- **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
- **üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.
- **bilgi** Bilgi dizesinin işaretçisi.
- **additional_info** Ek bilgi dizesinin işaretçisi.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) http sunucusu yanıtı başarıyla gönderildi

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
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

### <a name="send-response-from-callback-function"></a>Geri çağırma işlevinden yanıt gönder

**Örneğini**

```c
UINT nx_http_server_callback_response_send_extended(
     NX_HTTP_SERVER *server_ptr, CHAR *heade
     UINT header_length, CHAR *information,
     UINT information_length, CHAR *additional_info,
     UINT additional_info_length);
```

**Açıklama**

Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir. Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır. Bu işlev kullanıldığında, geri çağırma yordamının NX_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerektiğini unutmayın.

Bu hizmet *nx_http_server_callback_response_send ()* yerini alır. Bu sürüm, uzunluk bilgilerini giriş bağımsız değişkeni olarak alır.

**Giriş parametreleri**

- **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
- **üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.
- **header_length** Yanıt üst bilgisi dizesinin uzunluğu.
- **bilgi** Bilgi dizesinin işaretçisi.
- **information_length** Bilgi dizesinin uzunluğu.
- **additional_info** Ek bilgi dizesinin işaretçisi.
- **additional_info_length** Ek bilgi dizesinin uzunluğu.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sunucu yanıtı başarıyla gönderildi

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
       if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
          (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
           a resource not found response. */
           nx_http_server_callback_response_send_extended(server_ptr,
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

### <a name="get-content-from-the-request"></a>İstekten içerik al

**Örneğini**

```c
UINT nx_http_server_content_get(NX_HTTP_SERVER *server_ptr,
                                NX_PACKET *packet_ptr,
                                ULONG byte_offset,
                                CHAR *destination_ptr,
                                UINT destination_size,
                                UINT *actual_size);
```

**Açıklama**

Bu hizmet, POST veya PUT HTTP Client isteğinden belirtilen miktarda içeriği almaya çalışır. Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin nx_http_server_content_get_extended () uygulamasına geçirilmesi önerilir.

**Giriş parametreleri**

- **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
- **packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi. Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.
- **byte_offset** İçerik alanına kaydırılacağı bayt sayısı.
- **destination_ptr** İçerik için hedef alana yönelik işaretçi.
- **destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.
- **actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) başarılı http sunucusu içerik al
- **NX_HTTP_ERROR** (0xE0) http sunucusu iç hatası
- **NX_HTTP_DATA_END** (0xE7) Istek içeriğinin sonu
- **NX_HTTP_TIMEOUT** (0XE1) sonraki içerik paketini alma sırasında http sunucusu zaman aşımı
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
/* Assuming we are in the application’s request notify callback
routine, retrieve up to 100 bytes of content starting at offset 0. */
status = nx_http_server_content_get(&my_server, packet_ptr,
                                   0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
request content. */
```

## <a name="nx_http_server_content_get_extended"></a>nx_http_server_content_get_extended

### <a name="get-content-from-the-requestsupports-zero-length-content-length"></a>İstekten içerik al/sıfır uzunlukta Içerik uzunluğunu destekler

**Örneğini**

```c
UINT nx_http_server_content_get_extended(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET *packet_ptr,
                                        ULONG byte_offset,
                                        CHAR *destination_ptr,
                                        UINT destination_size,
                                        UINT *actual_size);
```

**Açıklama**

Bu hizmet *nx_http_server_content_get ()* ile neredeyse aynıdır; POST veya PUT HTTP Client isteğinden belirtilen miktarda içeriği almaya çalışır. Ancak, geçerli bir istek olarak sıfır değeri (' boş istek ') Içerik uzunluğundaki istekleri işler. Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.

Bu hizmet *nx_http_server_content_get ()* yerini alır. Bu sürüm, çağıranın ek uzunluk bilgileri sağlaması için gereklidir.

**Giriş parametreleri**

- **server_ptr** HTTP sunucu denetim bloğu işaretçisi.
- **packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi. Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.
- **byte_offset** İçerik alanına kaydırılacağı bayt sayısı.
- **destination_ptr** İçerik için hedef alana yönelik işaretçi.
- **destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.
- **actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) başarılı http içerik al
- **NX_HTTP_ERROR** (0xE0) http sunucusu iç hatası
- **NX_HTTP_DATA_END** (0xE7) Istek içeriğinin sonu
- **NX_HTTP_TIMEOUT** (0XE1) sonraki paketi alma sırasında http sunucusu zaman aşımı
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
/* Assuming we are in the application’s request notify callback
routine, retrieve up to 100 bytes of content starting at offset 0. */
status = nx_http_server_content_get_extended(&my_server, packet_ptr,
                                            0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
request content. */
```

## <a name="nx_http_server_content_length_get"></a>nx_http_server_content_length_get

### <a name="get-length-of-content-in-the-request"></a>İstekteki içerik uzunluğunu al

**Örneğini**

```c
UINT nx_http_server_content_length_get(NX_PACKET *packet_ptr);
```
**Açıklama**

Bu hizmet, sağlanan paketteki HTTP içerik uzunluğunu almaya çalışır. HTTP içeriği yoksa, bu yordam sıfır değerini döndürür. Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin nx_http_server_content_length_get_extended() geçişleri teşvik edilecektir.

**Giriş Parametreleri**

- **packet_ptr** HTTP İstemcisi istek paketinin işaretçisi. Bu paketin istek bildirim geri çağırma tarafından serbest bırakması gerektiğini unutmayın.

**Dönüş Değerleri**

- **içerik uzunluğu** Hatada sıfır değeri döndürülür

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
/* Assuming we are in the application’s request notify callback
routine, get the content length of the HTTP Client request. */
length = nx_http_server_content_length_get(packet_ptr);

/* The “length” variable now contains the length of the HTTP Client
request content area. */
```

## <a name="nx_http_server_content_length_get_extended"></a>nx_http_server_content_length_get_extended

### <a name="get-length-of-content-in-the-requestsupports-content-length-of-zero-value"></a>İstekte içeriğin uzunluğunu al/İçerik Uzunluğunu sıfır değeriyle destekler

**Prototip**

```c
UINT nx_http_server_content_length_get_extended(NX_PACKET *packet_ptr,
                                               UINT *content_length);
```

**Açıklama**

Bu hizmet, *nx_http_server_content_length_get() ile benzerdir;* , sağlanan pakette HTTP içerik uzunluğunu almaya çalışır. Ancak, dönüş değeri başarılı tamamlanma durumunu gösterir ve giriş işaretçisinde gerçek uzunluk değeri content_length. HTTP içeriği/İçerik Uzunluğu = 0 yoksa, bu yordam yine de başarılı bir tamamlanma durumu döndürür ve content_length giriş işaretçisi geçerli bir uzunluğu (sıfır) işaret eder. Http Sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirim geri çağrısından çağrılmalı (*nx_http_server_create()*).

Bu hizmet, *nx_http_server_content_length_get*() değiştirir.

**Giriş Parametreleri**

- **packet_ptr** HTTP İstemcisi istek paketinin işaretçisi. Bu paketin istek bildirim geri çağırma tarafından serbest bırakması gerektiğini unutmayın.
- **content_length** İçerik Uzunluğu alanından alınan değer işaretçisi

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Başarılı HTTP Sunucusu içeriği
- **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Hatalı HTTP üst bilgisi biçimi
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
/* Assuming we are in the application’s request notify callback
routine, get the content length of the HTTP Client request. */
ULONG content_length;

status = nx_http_server_content_length_get_extended(packet_ptr, &content_length);

/* If the “status” variable indicates successful completion, the“length” variable
contains the length of the HTTP Client request content area. */
```

## <a name="nx_http_server_create"></a>nx_http_server_create

### <a name="create-an-http-server-instance"></a>HTTP Sunucusu örneği oluşturma

**Prototip**

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

**Açıklama**

Bu hizmet, kendi ThreadX iş parçacığı bağlamında çalışan bir HTTP Sunucusu örneği oluşturur. İsteğe *authentication_check* ve *request_notify* geri çağırma yordamları, uygulama yazılım denetimine HTTP Sunucusunun temel işlemleri üzerinde denetim verir.

**Giriş Parametreleri**

- **http_server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.
- **http_server_name** HTTP Sunucusunun adının işaretçisi.
- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **media_ptr** Daha önce oluşturulan FileX medya örneğinin işaretçisi.
- **stack_ptr** HTTP Sunucusu iş parçacığı yığın alanı işaretçisi.
- **stack_size** HTTP Sunucusu iş parçacığı yığını boyutunun işaretçisi.
- **authentication_check** Uygulamanın kimlik doğrulama denetimi yordamına işlev işaretçisi. Belirtilirse, bu yordam her HTTP İstemcisi isteği için çağrılır. Bu parametre NULL ise hiçbir kimlik doğrulaması gerçekleştirilecek.
- **request_notify** Uygulamanın istek bildirim yordamına işlev işaretçisi. Belirtilirse, bu yordam isteğin HTTP sunucusu işlemeden önce çağrılır. Bu, kaynak adının yeniden yönlendirilmesine veya HTTP İstemcisi isteğini tamamlamadan önce bir kaynak içindeki alanların güncelleştirilmesini sağlar.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Başarılı HTTP Sunucusu oluşturma.
- NX_PTR_ERROR (0x07) Geçersiz HTTP Sunucusu, IP, medya, yığın veya paket havuzu işaretçisi.
- NX_HTTP_POOL_ERROR (0xE9) Havuzun paket yükü, tam HTTP isteğini içerecek kadar büyük değil.

**İzin Verilen**

Başlatma, İş Parçacıkları

**Örnek**

```c
/* Create an HTTP Server instance called “my_server.” */
status = nx_http_server_create(&my_server, “my server”, &ip_0, &ram_disk,
                              stack_ptr, stack_size, &pool_0,
                              my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_http_server_delete"></a>nx_http_server_delete

### <a name="delete-an-http-server-instance"></a>HTTP Sunucusu örneğini silme

**Prototip**

```c
UINT nx_http_server_delete(NX_HTTP_SERVER *http_server_ptr);
```

**Açıklama**

Bu hizmet, daha önce oluşturulmuş bir HTTP Sunucusu örneğini siler.

**Giriş Parametreleri**

- **http_server_ptr** HTTP Sunucusu denetim bloğu işaretçisi.

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Başarılı HTTP Sunucusu silme
- NX_PTR_ERROR (0x07) Geçersiz HTTP Sunucusu işaretçisi
- NX_CALLER_ERROR (0x11) Bu hizmetin çağıranı geçersiz

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
/* Delete the HTTP Server instance called “my_server.” */
status = nx_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_http_server_get_entity_content"></a>nx_http_server_get_entity_content

### <a name="retrieve-the-location-and-length-of-entity-data"></a>Varlık verisi konumunu ve uzunluğunu alma

**Prototip**

```c
UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      ULONG *available_offset,
                                      ULONG *available_length);
```

**Açıklama**

Bu hizmet, alınan İstemci iletisinde geçerli çok parçalı varlık içindeki veri başlangıcının konumunu ve sınır dizesi dahil değil veri uzunluğunu belirler. Dahili OLARAK HTTP sunucusu, kendi uzaklıklarını günceller, böylece bu işlev birden çok varlık içeren iletiler için aynı İstemci veri birimi üzerinde yeniden çağrılabilirsiniz. Paket işaretçisi, İstemci iletisi çok paketli bir veri birimi olduğu bir sonraki pakete güncelleştirilir.

Bu NX_HTTP_MULTIPART_ENABLE için etkinleştirilmesi gerektiğini unutmayın.

Daha *nx_http_server_get_entity_header* için bkz.

**Giriş Parametreleri**

- **server_ptr** HTTP Sunucusu İşaretçisi
- **packet_pptr** Paket işaretçisinin konumu için işaretçi. Uygulamanın bu paketi serbest bırakması gerektiğini unutmayın.
- **available_offset** Paket ön uç işaretçisinde varlık verilerini kaydırma işaretçisi
- **available_length** Varlık verisi uzunluğu işaretçisi

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Varlık içeriğinin boyutu ve konumu başarıyla alındı
- **NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) HTTP sunucusu iç çok parçalı işaretçileri için içerik zaten bulundu
- NX_HTTP_ERROR (0xE0) HTTP Sunucusu iç hatası
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

**İzin Verilen**

İş Parçacıkları

**Örnek**

```c
NX_HTTP_SERVER my_server;

UINT         offset, length;
NX_PACKET    *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
the entity header to determine details about the multipart data. If
successful, it then calls this service to get the location of entity data: */
status = nx_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
                                          &length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
entity data. */
```

## <a name="nx_http_server_get_entity_header"></a>nx_http_server_get_entity_header

### <a name="retrieve-the-contents-of-entity-header"></a>Varlık üst bilgisi içeriğini alma

**Prototip**

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                     NX_PACKET **packet_pptr,
                                     UCHAR *entity_header_buffer,
                                     ULONG buffer_size);
```

**Açıklama**

Bu hizmet varlık üst bilgilerini belirtilen arabelleğe alır. Dahili OLARAK HTTP Sunucusu, birden çok varlık üst bilgisi olan bir İstemci veri biriminde bir sonraki çok parçalı varlığı bulmak için kendi işaretçilerini günceller. Paket işaretçisi, İstemci iletisi çok paketli bir veri birimi olduğu bir sonraki pakete güncelleştirilir.

Bu NX_HTTP_MULTIPART_ENABLE için etkinleştirilmesi gerektiğini unutmayın.

**Giriş parametreleri**

- **server_ptr** HTTP sunucusu işaretçisi
- **packet_pptr** Paket işaretçisinin konumu işaretçisi. Uygulamanın bu paketi serbest bırakmadığını unutmayın.
- **entity_header_buffer** Varlık üstbilgisinin depolanacak konuma işaretçi
- **Buffer_size** Giriş arabelleğinin boyutu

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) varlık Heade başarıyla alındı
- **NX_HTTP_NOT_FOUND (0xE6)** Varlık üst bilgisi alanı bulunamadı
- **NX_HTTP_TIMEOUT (0xE1)** Çok paket istemci iletisi için sonraki paketin alınacağı sürenin süresi geçildi 
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı
- NX_HTTP_ERROR (0xE0) Iç HTTP hatası

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
/* my_request_notify* is the application request notify callback registered with
the HTTP server in *nx_http_server_create,* creates a response to the received
Client request. */

UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

NX_PACKET     *sresp_packet_ptr;
UINT          offset, length;**
NX_PACKET     *response_pkt;
UCHAR         buffer[1440];

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
             "Server: NetX HTTP 5.3\r\n");

    if(status == NX_SUCCESS)
    {
        if(nx_http_server_callback_packet_send(server_ptr, response_pkt) !=
                                              NX_SUCCESS)
        {
            nx_packet_release(response_pkt);
        }
    }
}
Else
{

        /* Indicate we have not processed the response to client yet.*/        
        return(NX_SUCCESS);
}

/* Indicate the response to client is transmitted. */
return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_gmt_callback_set"></a>nx_http_server_gmt_callback_set

### <a name="set-the-callback-to-obtain-gmt-date-and-time"></a>GMT Tarih ve saati almak için geri aramayı ayarlayın

**Örneğini**

```c
UINT nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                                    VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

**Açıklama**

Bu hizmet, daha önce oluşturulmuş bir HTTP sunucusu ile GMT Tarih ve saati alacak şekilde geri aramayı ayarlar. Bu hizmet HTTP sunucusu, Istemciye HTTP sunucu yanıtlarında bir üst bilgi oluşturuyor.

**Giriş parametreleri**

- **server_ptr** HTTP sunucusu işaretçisi
- **gmt_get** GMT geri çağırması işaretçisi
- **Tarih** Alınan tarihin işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
- NX_PTR_ERROR (0x07) geçersiz paket veya parametre işaretçisi.

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
NX_HTTP_SERVER my_server;

VOID get_gmt(NX_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_http_server_create, and before
starting HTTP services when nx_http_server_start is called, set the GMT
retrieve callback: */

status = nx_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
response header date. */
```

## <a name="nx_http_server_invalid_userpassword_notify_set"></a>nx_http_server_invalid_userpassword_notify_set

### <a name="set-the-callback-to-to-handle-invalid-userpassword"></a>Geri çağırma işlemini geçersiz kullanıcı/parola işleyecek şekilde ayarla

**Örneğini**

```c
UINT nx_http_server_invalid_userpassword_notify_set(
     NX_HTTP_SERVER *http_server_ptr,
     UINT (*invalid_username_password_callback)
     (CHAR *resource,
     ULONG client_address,
     UINT request_type));
```

**Açıklama**

Bu hizmet, bir Istemci alma, yerleştirme veya silme isteğinde, Özet veya temel kimlik doğrulamasından göre geçersiz bir Kullanıcı adı ve parola alındığında çağrılan geri aramayı ayarlar. HTTP sunucusu daha önce oluşturulmuş olmalıdır.

**Giriş parametreleri**

- **server_ptr** HTTP sunucusu işaretçisi
- **invalid_username_password_callback** Geçersiz Kullanıcı/geçiş geri çağırması işaretçisi
- **kaynak** İstemci tarafından belirtilen kaynak işaretçisi
- **client_address** İstemci adresi
- **request_type** İstemci isteği türünü gösterir. Belki:
  - NX_HTTP_SERVER_GET_REQUEST
  - NX_HTTP_SERVER_POST_REQUEST NX_HTTP_SERVER_HEAD_REQUEST
  - NX_HTTP_SERVER_PUT_REQUEST NX_HTTP_SERVER_DELETE_REQUEST

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
NX_HTTP_SERVER my_server;
VOID invalid_username_password_callback (NX_ CHAR *resource,
                                        ULONG client_address,
                                        UINT request_type);

/* After the HTTP server is created by calling nx_http_server_create, and before
starting HTTP services when nx_http_server_start is called, set the invalid
username password callback: */

status = nx_http_server_gmt_callback_set(&my_server,
                                        invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_http_server_mime_maps_additional_set"></a>nx_http_server_mime_maps_additional_set

### <a name="set-additional-mime-maps-for-html"></a>HTML için ek MIME haritaları ayarlama 

**Örneğini**

```c
UINT nx_http_server_mime_maps_additional_set(
     NX_HTTP_SERVER *server_ptr,
     NX_HTTP_SERVER_MIME_MAP *mime_maps,
     UINT mime_maps_num);
```

**Açıklama**

Bu hizmet, HTTP uygulama geliştiricisinin NetX HTTP sunucusu tarafından sağlanan varsayılan MIME türlerinden ek MIME türleri eklemesine izin verir (tanımlı türlerin listesi için bkz. *nx_http_server_get_type* ).

Bir istemci isteği alındığında, örneğin, bir GET isteği, http üst bilgisinden istenen dosya türünü, tercihe bağlı olarak ek MIME eşleme kümesini kullanarak ayrıştırır ve bulunursa eşleşme yoksa, HTTP sunucusunun varsayılan MIME eşlemesinde bir eşleşme arar. Eşleşme bulunmazsa, MIME türü varsayılan olarak "metin/düz" olarak ayarlanır.

İstek bildirimi işlevi HTTP sunucusuna kayıtlıysa, istek bildirimi geri araması dosya türünü ayrıştırmak için *nx_http_server_type_get* çağırabilir.

**Giriş parametreleri**

- **server_ptr** HTTP sunucusu örneğine yönelik işaretçi
- **mime_maps** MIME eşleme dizisine yönelik işaretçi
- **mime_map_num** Dizideki MIME haritaları sayısı

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) başarılı http sunucusu MIME eşleme kümesi
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

**İzin verilen**

Başlatma, Iş parçacıkları

**Örnek**

```c
/* my_server is an NX_HTTP_SERVER previously created. */

NX_HTTP_SERVER_MIME_MAP my_mime_maps [2];

static NX_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc", "yourtype/abc"},
    {"xyz", "mytype/xyz"},
};

status = nx_http_server_mime_maps_additional_set(&my_server,
                                                &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP
server MIME map set.” */
```

## <a name="nx_http_server_packet_content_find"></a>nx_http_server_packet_content_find

### <a name="extract-content-length-and-set-pointer-to-start-of-data"></a>İçerik uzunluğunu Ayıkla ve veri başına işaretçiyi ayarla

**Örneğini**

```c
UINT nx_http_server_packet_content_find(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_ptr,
                                       UINT *content_length);
```

**Açıklama**

Bu hizmet, HTTP üstbilgisinden içerik uzunluğunu ayıklar. Ayrıca, sağlanan paketi aşağıdaki gibi güncelleştirir: paket önüne işaretçisi (yazılacak paket arabelleğinin konumu), http içeriğine (veri) yalnızca http üst bilgisini geçirilmiş şekilde ayarlanır.

İçeriğin başlangıcı geçerli pakette bulunmazsa, işlev, sonraki paketin NX_HTTP_SERVER_TIMEOUT_RECEIVE bekle seçeneği kullanılarak alınmasını bekler.

Bu, *nx_http_server_get_entity_header ()* çağrılmadan önce çağrılmamalıdır; çünkü varlık üstbilgisinin sonundaki önüne işaretçisini değiştirir.

**Giriş parametreleri**

- **server_ptr** HTTP sunucusu örneğine yönelik işaretçi
- **packet_ptr** Güncelleştirilmiş önüne işaretçisine sahip paketi döndürmek için paket işaretçisi işaretçisi
- **CONTENT_LENGTH** Ayıklanan content_length işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) http içerik uzunluğu bulundu ve paket başarıyla güncelleştirildi
- **NX_HTTP_TIMEOUT** (0XE1) süre süresi dolduğunda sonraki pakette bekliyor
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
The server has received a Client request packet, recv_packet_ptr, and the packet
content find service is called from the request notify callback function 
registere with the HTTP server. */

UINT content_length;

status = nx_http_server_packet_content_find(server_ptr, recv_packet_ptr,
                                           &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_http_server_packet_get"></a>nx_http_server_packet_get

### <a name="receive-the-next-http-packet"></a>Sonraki HTTP paketini al

**Örneğini**

```c
UINT nx_http_server_packet_get(NX_HTTP_SERVER *server_ptr,
                              NX_PACKET **packet_ptr);
```

**Açıklama**

Bu hizmet, HTTP sunucusu yuvasında alınan bir sonraki paketi döndürür. Bir paket almak için bekle seçeneği NX_HTTP_SERVER_TIMEOUT_RECEIVE.

**Giriş parametreleri**

- **server_ptr** HTTP sunucusu örneğine yönelik işaretçi
- **packet_ptr** Alınan paket işaretçisi

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) sonraki http paketi başarıyla alındı
- **NX_HTTP_TIMEOUT** (0XE1) süre süresi dolduğunda sonraki pakette bekliyor
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
/* The HTTP server pointed to by server_ptr is previously created and started. */

UINT content_length;
NX_PACKET *recv_packet_ptr;

status = nx_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_http_server_param_get"></a>nx_http_server_param_get

### <a name="get-parameter-from-the-request"></a>İstekten parametre al

**Örneğini**

```c
UINT nx_http_server_param_get(NX_PACKET *packet_ptr,
                             UINT param_number, CHAR *param_ptr,
                             UINT max_param_size);
```

**Açıklama**

Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL parametresini almaya çalışıyor. İstenen HTTP parametresi yoksa, bu yordam NX_HTTP_NOT_FOUND durumunu döndürür. Bu yordam, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.

**Giriş parametreleri**

- **packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi. Uygulamanın bu paketi serbest bırakmadığını unutmayın.
- **param_number** Parametre listesinde soldan sağa sıfırdan başlayan parametrenin mantıksal numarası.
- **param_ptr** Parametreyi kopyalamak için hedef alan.
- **max_param_size** Parametre hedefi alanının maksimum boyutu.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) başarılı http sunucusu parametre al
- **NX_HTTP_NOT_FOUND** (0xE6) belirtilen parametre bulunamadı
- **NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) istek parametresi düzgün sonlandırılmadı
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
/* Assuming we are in the application’s request notify callback
routine, get the first parameter of the HTTP Client request. */

status = nx_http_server_param_get(request_packet_ptr, 0, param_destination, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
in “param_destination.” */
```

## <a name="nx_http_server_query_get"></a>nx_http_server_query_get

### <a name="get-query-from-the-request"></a>İstekten sorgu al

**Örneğini**

```c
UINT nx_http_server_query_get(NX_PACKET *packet_ptr, UINT query_number,
                             CHAR *query_ptr, UINT max_query_size);
```

**Açıklama**

Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL sorgusunu almaya çalışıyor. İstenen HTTP sorgusu yoksa, bu yordam NX_HTTP_NOT_FOUND durumunu döndürür. Bu yordam, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.

**Giriş parametreleri**

- **packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi. Uygulamanın bu paketi serbest bırakmadığını unutmayın.
- **query_number** Sıfırdan başlayan parametrenin mantıksal numarası, sorgu listesinde soldan sağa.
- **query_ptr** Sorguyu kopyalamak için hedef alan.
- **max_query_size** Sorgu hedefi alanının maksimum boyutu.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) başarılı http sunucusu sorgusu al
- **NX_HTTP_FAILED** (0xE2) sorgu boyutu çok küçük.
- **NX_HTTP_NOT_FOUND** (0xE6) belirtilen sorgu bulunamadı
- **NX_HTTP_NO_QUERY_PARSED** (0xF2) istemci Isteğinde sorgu yok
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
/* Assuming we are in the application’s request notify callback
routine, get the first query of the HTTP Client request. */
status = nx_http_server_query_get(request_packet_ptr, 0, query_destination, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
in “query_destination.” */
```

##   
nx_http_server_start

### <a name="start-the-http-server"></a>HTTP sunucusunu başlatma

**Örneğini**

```c
UINT nx_http_server_start(NX_HTTP_SERVER *http_server_ptr);
```

**Açıklama**

Bu hizmet, önceden oluşturma HTTP sunucu örneğini başlatır.

**Giriş parametreleri**

- **http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) başarılı http sunucusu başlatması
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

**İzin verilen**

Başlatma, Iş parçacıkları

**Örnek**

```c
/* Start the HTTP Server instance “my_server.” */
status = nx_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_http_server_stop"></a>nx_http_server_stop

### <a name="stop-the-http-server"></a>HTTP sunucusunu durdur

**Örneğini**

```c
UINT nx_http_server_stop(NX_HTTP_SERVER *http_server_ptr);
```

**Açıklama**

Bu hizmet, önceden oluşturma HTTP sunucu örneğini durduruyor. Bu yordam, bir HTTP sunucu örneği silinmeden önce çağrılmalıdır.

**Giriş parametreleri**

- **http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.

**Dönüş değerleri**

- **NX_SUCCESS** (0x00) başarılı http sunucusu durdur
- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı

**İzin verilen**

İş Parçacıkları

**Örnek**

```c
/* Stop the HTTP Server instance “my_server.” */

status = nx_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_http_server_type_get"></a>nx_http_server_type_get

### <a name="extract-file-type-from-client-http-request"></a>Istemci HTTP isteğinden dosya türünü Ayıkla

**Örneğini**

```c
UINT nx_http_server_type_get(NX_HTTP_SERVER *http_server_ptr,
                            CHAR *name, CHAR *http_type_string);
```

**Açıklama**

Bu hizmet, arabellek *HTTP_TYPE_STRING* http istek türünü ve giriş arabelleği *ADıNDAN*(genellikle URL) gelen dönüş değerindeki uzunluğu ayıklar. MIME eşlemesi bulunmazsa, varsayılan olarak "metin/düz" tür olur. Aksi takdirde, bir eşleşme için ayıklanan tür, HTTP sunucusu varsayılan MIME eşlemeleriyle karşılaştırılır. NetX HTTP sunucusundaki varsayılan MIME haritaları şunlardır:

- HTML metni/HTML
- htm metin/html
- txt metin/düz
- GIF resmi/GIF
- jpg resmi/JPEG
- ICO resmi/x-simgesi

Sağlanırsa, Kullanıcı tanımlı ek MIME haritaları kümesi de arar. Kullanıcı tanımlı haritalar hakkında daha fazla bilgi için bkz. *nx_http_server_mime_maps_addtional_set ()* .

Bu hizmet kullanımdan kaldırılmıştır. Geliştiricilerin *nx_http_server_type_get_extended ()* uygulamasına geçirilmesi önerilir.

**Giriş parametreleri**

- **http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi
- **name** Arama için arabelleğe işaretçi
- **http_type_string** (Ayıklanan HTML türüne işaretçi)

**Dönüş Değerleri**

- **Bayt cinsinden dize uzunluğu** Sıfır olmayan değer başarılı
- **Sıfır, hatayı gösterir**

**İzin Verilen**

Uygulama

**Örnek**

```c
/* my_server is a previously created HTTP server, which starts accepting 
client requests when *nx_http_server_start* is called*/

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
string_length = nx_http_server_type_get(&my_server_ptr,
                my_server.nx_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
```

Daha ayrıntılı bir örnek için şu açıklamaya bakın:

*nx_http_server_callback_generate_response_header.*

## <a name="nx_http_server_type_get_extended"></a>nx_http_server_type_get_extended

### <a name="extract-file-type-from-client-http-request"></a>İstemci HTTP isteğinden dosya türünü ayıklama

**Prototip**

```c
UINT nx_http_server_type_get_extended(
     NX_HTTP_SERVER *http_server_ptr,
     CHAR *name, CHAR *http_type_string,
     UINT http_type_string_max_size);
```

**Açıklama**

Bu hizmet, arabelleğin içinde HTTP istek *türünü http_type_string* ve dönüş değerindeki uzunluğunu giriş arabelleği *adıyla*(genellikle URL) ayıklar. MiME eşlemesi bulunamazsa varsayılan olarak "text/plain" türü kullanılır. Aksi takdirde, ayıklanan türü bir eşleşme için HTTP Sunucusu varsayılan MIME eşlemeleri ile karşılaştırıldığında. NetX Duo HTTP Sunucusu'daki varsayılan MIME eşlemeleri:

- html metni/html
- html metin/html
- txt metni/düz
- gif görüntüsü/gif
- jpg image/jpeg
- ico görüntüsü/x-icon

Sağlanırsa, kullanıcı tanımlı bir dizi ek MIME eşlemesi de aranacak. Kullanıcı tanımlı nx_http_server_mime_maps_addtional_set hakkında daha fazla bilgi için bkz. *nx_http_server_mime_maps_addtional_set()* .

Bu hizmet *nx_http_server_type_get() ile değiştirilir.* Bu sürüm ek uzunluk bilgileri sağlar.

**Giriş Parametreleri**

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi
- **name** Arama için arabelleğe işaretçi
- **name_length** Aranacak arabelleğin uzunluğu
- **http_type_string** (Ayıklanan HTML türüne işaretçi)
- **http_type_string_max_size**

Http_type_string *arabelleğinin* boyutu

**Dönüş Değerleri**

- **Bayt cinsinden dize uzunluğu** Sıfır olmayan değer başarılı<br />Sıfır, hatayı gösterir

**İzin Verilen**

Uygulama

**Örnek**

```c
/* my_server is a previously created HTTP server, which starts accepting 
client requests when *nx_http_server_start* is called*/

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
string_length = nx_http_server_type_get_extended(&my_server,
                my_server.nx_http_server_request_resource, resource_length,
                temp_string, sizeof(temp_string));

/* If string_length is non zero, the HTTP string is extracted. */
```

Daha ayrıntılı bir örnek için şu açıklamaya bakın:

*nx_http_server_callback_generate_response_header.*

## <a name="nx_http_server_digest_authenticate_notify_set"></a>nx_http_server_digest_authenticate_notify_set

### <a name="set-digest-authenticate-callback-function"></a>Özet kimlik doğrulaması geri çağırma işlevini ayarlama

**Prototip**

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

**Açıklama**

Bu hizmet özet kimlik doğrulaması gerçekleştirilirken çağrılan geri çağırmayı ayarlar.

**Giriş Parametreleri**

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi
- **digest_authenticate_callback** Özet kimlik doğrulaması geri çağırma işaretçisi

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Geri çağırmayı başarıyla ayarlama
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi
- NX_NOT_SUPPORTED (0x4B) Özet kimlik doğrulaması etkinleştirilmedi

**İzin Verilen**

Uygulama

**Örnek**

```c
UINT digest_authenticate_callback(NX_HTTP_SERVER *server_ptr, CHAR *name_ptr,
                                 CHAR *realm_ptr, CHAR *password_ptr,
                                 CHAR *method,CHAR *authorization_uri,
                                 CHAR *authorization_nc,
                                 CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and
before starting HTTP services when nx_http_server_start is called, set the
digest authenticate callback: */

status = nx_http_server_digest_authenticate_notify_set (&my_server,
                                                       digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_http_server_authentication_check_set"></a>nx_http_server_authentication_check_set

### <a name="set-authentication-checking-callback-function"></a>Kimlik doğrulama denetimi geri çağırma işlevini ayarlama

**Prototip**

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

**Açıklama**

Bu hizmet, kimlik doğrulama denetimi için geri çağırma işlevini ayarlar.

**Giriş Parametreleri**

- **http_server_ptr** HTTP Sunucusu örneğine işaretçi
- **authentication_check_extended** Uygulamanın kimlik doğrulama denetimi işaretçisi

**Dönüş Değerleri**

- **NX_SUCCESS** (0x00) Geri çağırmayı başarıyla ayarlama
- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

**İzin Verilen**

Uygulama

**Örnek**

```c
static UINT authentication_check_extended(NX_HTTP_SERVER *server_ptr,
                                         UINT request_type, CHAR *resource,
                                         CHAR **name, UINT *name_length,
                                         CHAR **password, 
                                         UINT *password_length,
                                         CHAR **realm, UINT *realm_length)
{

    /* Just use a simple name, password, and realm for all
    requests and resources. */

    *name = "name";
    *password = "password";
    *realm = "NetX Duo HTTP demo";
    *name_length = 4;
    *password_length = 8;
    *realm_length = 18;

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and
before starting HTTP services when nx_http_server_start is called, set 
the authentication checking callback: */

nx_http_server_authentication_check_set (&my_server,
                                        authentication_check_extended);
```