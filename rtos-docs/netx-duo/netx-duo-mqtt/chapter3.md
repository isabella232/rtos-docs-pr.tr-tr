---
title: Bölüm 3-Azure RTOS NetX Duo MQTT Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo MQTT Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9cbb65946c45bfbc476091f7c604346e839a42fc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825895"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-mqtt-client-services"></a>Bölüm 3-Azure RTOS NetX Duo MQTT istemci hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX Duo MQTT istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

-  *MQTT istemci örneği nxd_mqtt_client_create oluştur*
- **nxd_mqtt_client_will_message_set** *iletiyi ayarla*
- **nxd_mqtt_client_client_login_set** *MQTT istemci oturum açma Kullanıcı adı ve parolasını ayarlama*
-  *MQTT istemcisini aracıya bağlama* nxd_mqtt_client_connect
- **nxd_mqtt_client_secure_connect** *MQTT istemcisini, TLS güvenliği ile aracıya bağlama*
- **nxd_mqtt_client_publish** *aracı aracılığıyla bir ileti yayımlayın.*
- **nxd_mqtt_client_subscribe** *bir konuya abone olma*
- **nxd_mqtt_client_unsubscribe** *bir konuyla aboneliğinizi kaldırma*
-  *MQTT ileti alma geri arama işlevini nxd_mqtt_client_receive_notify_set ayarlama*
- **nxd_mqtt_client_message_get** *aracıdan ileti alma*
-  *MQTT iletisi bağlantısını kesme geri arama işlevini nxd_mqtt_client_disconnect_notify_set ayarla*
- **nxd_mqtt_client_disconnect** *, aracıdan MQTT istemcisinin bağlantısını keser*
-  *MQTT istemci örneğini silmek* nxd_mqtt_client_delete

## <a name="nxd_mqtt_client_create"></a>nxd_mqtt_client_create

MQTT Istemci örneği oluştur

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_create(NXD_MQTT_CLIENT *client_ptr,
    CHAR *client_name, CHAR *client_id,
    UINT client_id_length, NX_IP *ip_ptr, NX_PACKET_POOL
    *pool_ptr, VOID *stack_ptr, ULONG stack_size, UINT
    mqtt_thread_priority,
    VOID *memory_ptr, ULONG memory_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneğinde bir MQTT Istemci örneği oluşturur. *Client_id* dize, *Istemci tanımlayıcısı (ClientID)* olarak MQTT bağlantı aşamasında sunucuya geçirilir. Ayrıca, gerekli ThreadX kaynaklarını (MQTT Istemci görevi iş parçacığı, mutex, olay bayrağı grubu ve TCP yuvası) oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **client_name** İstemci adı dizesi.
- **client_id** Bağlantı aşamasında kullanılan istemci KIMLIĞI dizesi. MQTT Aracısı, bir istemciyi benzersiz şekilde tanımlamak için bu client_id kullanır.
- **client_id_length** İstemci KIMLIĞI dizesinin bayt cinsinden uzunluğu.
- **ip_ptr** IP örneği işaretçisi.
- **pool_ptr** MQTT istemcisinin işlem için kullandığı paket havuzu işaretçisi.
- **stack_ptr** MQTT Istemci iş parçacığı için yığın alanı.
- **stack_size** Yığın alanının bayt cinsinden boyutu.
- **mqtt_thread_priority** MQTT Iş parçacığının önceliği.
- **memory_ptr** Kullanım dışı. Artık kullanılmıyor.
- **memory_size** Kullanım dışı. Artık kullanılmıyor.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00) MQTT istemcisini başarıyla oluşturdu.
- **NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi.
- NXD_MQTT_INVALID_PARAMETER (0x10009), konu başlığı dizesi, will_retrain_flag veya will_QoS değeri geçersiz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
#define CLIENT_ID_STRING "My Test Client"

#define MQTT_THREAD_PRIORITY 2

NXD_MQTT_CLIENT my_client;
NX_IP ip_0; /* Assume ip_0 is created prior to MQTT client creation. */
NX_PACKET_POOL pool_0;/* Assume pool_0 is created prior to MQTT client creation. */
UCHAR mqtt_thread_stack[STACK_SIZE];

/* Create the MQTT Client instance on "ip_0". */
status = **nxd_mqtt_client_create**(&my_client, "my client",
    CLIENT_ID_STRING, stlren(CLIENT_ID_STRING),
    &ip_0, &pool_0, (VOID*)mqtt_thread_stack, STACK_SIZE,
    MQTT_THREAD_PRIORITY, NX_NULL, 0);

/* If status is NXD_MQTT_SUCCESS an MQTT Client instance was successfully created. */
```

## <a name="nxd_mqtt_client_will_message_set"></a>nxd_mqtt_client_will_message_set

Yapılacak iletileri ayarlar

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_will_message_set(NXD_MQTT_CLIENT
    *client_ptr,
    Const UCHAR *will_topic,
    UINT will_topic_length
    Const UCHAR *will_message,
    UINT will_message_length,
    UINT will_retain_flag,
    UINT will_QoS);
```

### <a name="description"></a>Açıklama

Bu hizmet, istemci sunucuya bağlanmadan önce isteğe bağlı olarak yapılacak konuyu ve iletiyi ayarlar. Bu konu başlığı UTF-8 kodlu dize olmalıdır.

, Ayarlandıysa, CONNECT iletisinin bir parçası olarak aracısına iletilir iletisi gönderilir. Bu nedenle, kullanmak isteyen uygulamanın MQTT bağlantısı yapmadan önce bu hizmeti kullanması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **will_topic** UTF-8 kodlu, konu dizesi. Konunun mevcut olması gerekir. Çağıran, *nx_mqtt_client_connect* çağrısının yapılana kadar will_topic dizenin geçerli kalması gerekir.
- **will_topic_length** Bu konu başlığı dizesindeki bayt sayısı
- **will_message** Uygulama tanımlı olacaktır iletisi. İleti gerekli değilse, uygulama bu alanı NX_NULL olarak ayarlayabilir *.*
- **will_message_length** İleti dizesindeki bayt sayısı. Will_message NULL olarak ayarlandıysa, will_message_length 0 olarak ayarlanmalıdır.
- **will_retain_flag** Sunucunun, iletileri bir tutulan ileti olarak yayınlayıp yayımlamayacağını belirtir. Geçerli değerler *NX_TRUE* veya *NX_FALSE.*
- **will_QoS** İleti gönderilirken sunucu tarafından kullanılan QoS değeri. Geçerli değerler 0 veya 1 ' dir.  

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00), iletileri başarıyla ayarlıyor.
- **NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000c) QoS düzey 2 iletileri desteklenmez.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu.
- NXD_MQTT_INVALID_PARAMETER (0x10009), konu başlığı dizesi, will_retrain_flag veya will_QoS değeri geçersiz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
#define WILL_TOPIC "my_will_topic"

#define WILL_MESSAGE "my will message"

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_will_message_set(&my_client,
    WILL_TOPIC, STRLEN(WILL_TOPIC),
    WILL_MESSAGE, STRLEN(WILL_MESSAGE),
    NX_TRUE, 0);

/* If status is NXD_MQTT_SUCCESS the will message is properly
configured for the session. It will be transmitted to the server
during MQTT connection. */
```

## <a name="nxd_mqtt_client_login_set"></a>nxd_mqtt_client_login_set

MQTT istemci oturum açma Kullanıcı adı ve parolasını ayarlar

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_login_set(NXD_MQTT_CLIENT *client_ptr,
    Const UCHAR *username,
    UINT username_length
    Const UCHAR *password,
    UINT password_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, kimlik doğrulama amacıyla MQTT bağlantı aşamasında kullanılan Kullanıcı adını ve parolayı ayarlar.

Kullanıcı adı ve parolayla MQTT istemci oturumu açma isteğe bağlıdır. Sunucunun Kullanıcı adı ve parola gerektirdiği durumlarda, bağlantı oluşturulmadan önce Kullanıcı adı ve parolanın ayarlanması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **Kullanıcı adı** UTF-8 kodlu Kullanıcı adı dizesi. Çağıran, *nx_mqtt_client_connect* çağrısı yapıldığından Kullanıcı adı dizesinin geçerli kalmasını sağlamalıdır.
- **username_length** Kullanıcı adı dizesindeki bayt sayısı
- **parola** Parola dizesi. Parola gerekmiyorsa, bu alan NX_NULL olarak ayarlanabilir.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00), iletileri başarıyla ayarlıyor.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu.
- NXD_MQTT_INVALID_PARAMETER (0x10009) geçersiz Kullanıcı adı dizesi veya parola dizesi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
#define USERNAME "MY_NAME"

#define PASSWORD "MY_LOGIN_SECRET"

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_login_set(&my_client,
    USERNAME, STRLEN(USERNAME),
    PASSWORD, STRLEN(PASSWORD));

/* If status is NXD_MQTT_SUCCESS the username and the password 
are set for the session. This information will be 
transmitted to the server during MQTT connection. */
```

## <a name="nxd_mqtt_client_connect"></a>nxd_mqtt_client_connect

MQTT Istemcisini aracıya bağlama

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_connect(NXD_MQTT_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT keepalive, UINT clean_session, ULONG wait_option));
```

### <a name="description"></a>Açıklama

Bu hizmet, aracıya bir bağlantı başlatır. İlk olarak bir TCP yuvasını bağlar ve bir TCP bağlantısı yapar. Başarılı olduğunu varsayarsak, MQTT canlı tut özelliği etkinse bir zamanlayıcı oluşturur. Ardından MQTT sunucusu (Broker) ile bağlanır.

Bu hizmetin TLS koruması olmayan bir MQTT bağlantısı oluşturduğunu unutmayın. Güvenli bir MQTT bağlantısı oluşturmak için, uygulama ***nxd_mqtt_client_secure_connect ()*** hizmetini kullanır.

Bağlantı kurulduğunda, istemci *clean_session* NX_FALSE olarak ayarlarsa, istemci henüz kabul edilmemiş olan tüm iletileri yeniden gönderilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **server_ip** Aracı IP adresi.
- **SERVER_PORT** Aracı bağlantı noktası numarası. MQTT için varsayılan bağlantı noktası **_NXD_MQTT_PORT_** (1883) olarak tanımlanmıştır.
- **keep_alive** Oturum sırasında kullanılmak üzere etkin tut değeri (saniye cinsinden). Değer, aracı bu istemcinin zaman aşımına uğramadan önce aracıya gönderilen iki MQTT denetim iletisi arasındaki en uzun süreyi gösterir. 0 değeri, etkin tut özelliğini kapatır.
- **clean_session** Sunucunun bu oturumu Temizleme işleminin başlatılıp başlatılmayacağını belirtir. Geçerli seçenekler şunlardır **_NX_TRUE_*_ veya _*_NX_FALSE._**
- **wait_option** Bağlantı bekleme süresi.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00) başarılı MQTT bağlantısı
- **NXD_MQTT_ALREADY_CONNECTED** (0x10001) istemci, aracıya zaten bağlı.
- **NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX elde edilemedi 
- **NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası
- **NXD_MQTT_CONNECT_FAILURE** (0x10005) aracıya bağlanılamadı.
- **NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) aracıya ileti gönderilemiyor.
- **NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) sunucu hatayla yanıtladı
- **NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081) sunucu yanıt kodu
- **NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082) sunucu yanıt kodu
- **NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083) sunucu yanıt kodu
- **NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084) sunucu yanıt kodu
- **NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085) sunucu yanıt kodu
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
NXD_ADDRESS broker_address;

/* Set up broker IP address */
broker_address.nxd_ip_version = 4;
broker_address.nxd_ip_address.v4 = MQTT_BROKER_ADDRESS;

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_connect(&my_client, &broker_address,
    NXD_MQTT_PORT,
    0, /* Turn off keepalive */
    NX_TRUE, /* Clean session flag set */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS a connection to the broker is successfully established. */
```

## <a name="nxd_mqtt_client_secure_connect"></a>nxd_mqtt_client_secure_connect

MQTT istemcisini TLS güvenliği ile aracıya bağlama

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_secure_connect(NXD_MQTT_CLIENT
    *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT (*tls_setup)(NXD_MQTT_CLIENT *,
        NX_SECURE_TLS_SESISON *,
        NX_SECURE_TLS_CERTIFICATE *,
        NX_SECURE_TLS_CERTIFICATE *),
    UINT keepalive, UINT connection_flag,
    UINT clean_session, ULONG wait_option));
```

### <a name="description"></a>Açıklama

Bu hizmet, bağlantı TCP yerine TLS katmanından geçilerek ***nxd_mqtt_client_connect*** aynıdır. Bu nedenle, istemci ile aracı arasındaki iletişim güvenli hale getirilir.

Kullanıcı tanımlı *tls_setup* , MQTT istemcisinin MQTT istemci bağlantısı yapmadan önce kullandığı bir geri çağırma işlevidir. Uygulama NetX güvenli TLS 'yi başlatır, güvenlik parametrelerini yapılandırır ve TLS el sıkışması sırasında kullanılacak ilgili sertifikaları yükler. Asıl TLS el sıkışması, aracının MQTT TLS bağlantı noktasında bir TCP bağlantısı kurulduktan sonra olur (varsayılan TCP bağlantı noktası 8883). TLS el sıkışması başarılı olduktan sonra MQTT CONNECT denetim paketi TLS aracılığıyla gönderilir.

Güvenli bağlantılar oluşturmak için, NetX güvenli TLS kitaplığı kullanılabilir olmalıdır ve NetX Duo MQTT istemcisinin tanımlanmış ***NX_SECURE_ENABLE*** oluşturulması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **server_ip** Aracı IP adresi.
- **SERVER_PORT** Aracı bağlantı noktası numarası. MQTT için varsayılan bağlantı noktası **_NXD_MQTT_TLS_PORT_** olarak tanımlanır (8883).
- **tls_setup** Kullanıcı tarafından sunulan TLS kurulum geri çağırma işlevi. Bu geri çağırma işlevi, TLS istemci bağlantı parametrelerini ayarlamak için çağrılır.
- **keep_alive** Oturum sırasında kullanılacak etkin tut değeri. 0 değeri, etkin tut özelliğini kapatır.
- **clean_session** Sunucunun bu oturumu Temizleme işleminin başlatılıp başlatılmayacağını belirtir. Geçerli seçenekler şunlardır **_NX_TRUE_*_ veya _*_NX_FALSE._**
- **wait_option** Bağlantı bekleme süresi.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00) TLS aracılığıyla kurulan başarılı MQTT istemci bağlantısı.
- **NXD_MQTT_ALREADY_CONNECTED** (0x10001) istemci, aracıya zaten bağlı.
- **NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX elde edilemedi 
- **NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası
- **NXD_MQTT_CONNECT_FAILURE** (0x10005) aracıya bağlanılamadı.
- **NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) aracıya ileti gönderilemiyor.
- **NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) sunucusu hata iletisiyle yanıtladı.
- **NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081) sunucu yanıt kodu
- **NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082) sunucu yanıt kodu
- **NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083) sunucu yanıt kodu
- **NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084) sunucu yanıt kodu
- **NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085) sunucu yanıt kodu
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu veya sunucu adresi yapısı.
- NX_INVALID_PORT (0x46) sunucu bağlantı noktası 0 olamaz.
- NXD_MQTT_INVALID_PARAMETER (0x10009) giriş parametresi hatası
- NXD_MQTT_CLIENT_NOT_RUNNING (0x1000E) MQTT Iş parçacığı henüz çalışmaya başlamadı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* TLS setup routine. This function is responsible for setting up TLS parameters.*/
UINT tls_setup_callback(NXD_MQTT_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certificate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_certificate,
    UINT timeout)
{
/* Note this routine is simplified to highlight the
necessary steps to setup a TLS session. Each
application may employ different procedures suitable for
its TLS settings, such as cipher suite, certificates. */

/* Create a TLS session for the MQTT connection, and pass
in various crypto methods this session can use for the
initial TLS handshake. */

/* Load appropriate certificates, or set up session key for Pre-share key operation. */

/* Start the TLS session */

/* Return NX_SUCCESS if the TLS session is established. */
    return(NX_SUCCESS);
}

NXD_ADDRESS broker_address;

/* Set up broker IP address */
broker_address.nxd_ip_version = 4;
broker_address.nxd_ip_address.v4 = MQTT_BROKER_ADDRESS;

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_secure_connect(&my_client,
    &server_address, NXD_MQTT_TLS_PORT, tls_setup_callback,
    0, /* Turn off keepalive */
    NX_TRUE, /* Clean session set */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS the MQTT Client was successfully connected to the broker via TLS. */
```

## <a name="nxd_mqtt_client_publish"></a>nxd_mqtt_client_publish

Aracı aracılığıyla bir ileti yayımlayın

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_publish(NXD_MQTT_CLIENT *client_ptr,
    CHAR *topic_name, UINT topic_name_length, CHAR *message, UINT
    message_length,
    UINT retain, UINT QoS, ULONG timeout);
```

### <a name="description"></a>Açıklama

Bu hizmet, aracı aracılığıyla bir ileti yayımlar. QoS düzey 2 iletilerinin yayımlanması henüz desteklenmiyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **topic_name** ' De yayımlanacak konu.
- **topic_name_length** Konunun uzunluğu (bayt).
- **ileti** İleti arabelleğinin işaretçisi.
- **message_length** İletinin bayt cinsinden boyutu
- **sakla** Aracının iletiyi tutyacağını belirler.
- **QoS** İstenen QoS değeri: 0 veya 1.
- **zaman aşımı** Zaman aşımı değeri

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00) başarılı MQTT istemci oluşturma
- **NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası.
- **NXD_MQTT_PACKET_POOL_FAILURE** (0x10006) paket havuzundan paket alamadı.
- **NXD_MQTT_COMMUNICATION_FAILURE** (0x10007), aracıyla iletişim kuramadı.
- **NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000c) QoS düzey 2 iletileri desteklenmez.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi
- NXD_MQTT_INVALID_PARAMETER (0x10009) giriş parametresi hatası

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
CHAR *topic = "temperature";
CHAR *message = "100";

/* Publish the temperature value. */
status = nxd_mqtt_client_publish(&my_client,
    topic, STRLEN(topic),
    message, STRLEN(message),
    NX_TRUE, /* Server retains message. */);
    0, /* QOS */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS the message has been 
successfully sent to the broker. */
```

## <a name="nxd_mqtt_client_subscribe"></a>nxd_mqtt_client_subscribe

Bir konuya abone olma

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_subscribe(NXD_MQTT_CLIENT
    *mqtt_client_ptr, CHAR *topic_name,
    UINT topic_name_length, UINT QoS);
```

### <a name="description"></a>Açıklama

Bu hizmet belirli bir konuya abone olur. QoS düzey 2 iletilerine abone olma henüz desteklenmiyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **topic_name** ' De yayımlanacak konu.
- **topic_name_length** Konunun uzunluğu (bayt).
- **QoS Istenen QoS düzeyi:** 0 veya 1.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00) konuya başarıyla abone oldu.
- **NXD_MQTT_NOT_CONNECTED** (0x10002) istemci, aracıya bağlı değil.
- **NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX elde edilemedi
- **NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası
- **NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) aracıya ileti gönderilemiyor.
- **NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000c) QoS düzey 2 iletileri desteklenmez.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi
- NXD_MQTT_INVALID_PARAMETER (0x10009) topic_name ayarlı değil veya topic_name_length sıfır ya da QoS değeri geçersiz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Subscribe to the topic "temperature" with QoS level 0 */
CHAR *topic = "temperature";

status = nxd_mqtt_client_subscribe(&my_client, topic,
    STRLEN(topic), 0);

/* If status is NXD_MQTT_SUCCESS, the client successfully
subscribes to the topic "temperate". At this point the client
is ready for receiving messages from the broker. */
```

## <a name="nxd_mqtt_client_unsubscribe"></a>nxd_mqtt_client_unsubscribe

Bir konuyla abonelik kaldırma

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_unsubscribe(NXD_MQTT_CLIENT
    *mqtt_client_pr,
    CHAR *topic_name,
    UINT topic_name_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir konudan aboneliği kaldırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **topic_name** Aboneliği kaldırma konusu.
- **topic_name_length** Konunun uzunluğu (bayt).

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00), konunun aboneliği başarıyla kaldırıldı.
- **NXD_MQTT_NOT_CONNECTED** (0x10002) istemci, aracıya bağlı değil.
- **NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX 'i alamadı.
- **NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası
- **NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) aracıya ileti gönderilemiyor.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu işaretçisi
- NXD_MQTT_INVALID_PARAMETER (0x10009) topic_name ayarlı değil veya topic_name_length sıfır.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Subscribe to the topic "temperature" with QoS level 0 */
CHAR *topic = "temperature";

status = nxd_mqtt_client_unsubscribe(&my_client, topic,
    STRLEN(topic));

/* If status is NXD_MQTT_SUCCESS, the client successfully
unsubscribes the topic "temperate". */
```

## <a name="nxd_mqtt_client_receive_notify_set"></a>nxd_mqtt_client_receive_notify_set

MQTT ileti alma geri arama işlevini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_receive_notify_set(NXD_MQTT_CLIENT
    *client_ptr,
    VOID(*receive_notify)(NXD_MQTT_CLIENT* client_ptr,
    UINT message_count));
```

### <a name="description"></a>Açıklama

Bu hizmet MQTT istemcisiyle bir geri çağırma işlevi kaydeder. Aracı tarafından yayınlanan bir ileti alındıktan sonra MQTT istemcisi iletiyi alma kuyruğunda depolar. Geri çağırma işlevi ayarlandıysa, uygulamaya bir iletinin alınmaya hazırlandığını bildirmek için geri çağırma işlevi çağırılır. Alma bildirme işlevi MQTT istemci denetim bloğuna bir işaretçi alır ve alma sırasındaki ileti sayısını belirten bir *message_count* . Bu sayı, zaman aralığında ulaşan yeni iletiler geldiği için alma bildirimi ve uygulamanın bu iletileri aldığı zaman arasında değişebileceğini unutmayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **receive_notify** Kullanıcının bir ileti alındığında çağrılması için geri arama işlevi sağlandı.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00) alma bildirim işlevini başarıyla ayarladı.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Sample MQTT receive notify function. */

VOID my_notify_func(NXD_MQTT_CLIENT* client_ptr,
    UINT message_count)
{

/* On receiving a message, set an event flag to wake up the
application thread. The message will be received and
processed in the application thread. */
tx_event_flags_set(&mqtt_app_flag,
    MESSAGE_RECEIVED_EVENT, TX_OR);

/* All done. Return to the caller. */
    return;
}

/* Set the receive callback function. */
status = **nxd_mqtt_client_receive_notify_set**(&my_client,
    my_notify_func);

/* If status is NXD_MQTT_SUCCESS the notify function is properly set. */
```

## <a name="nxd_mqtt_client_message_get"></a>nxd_mqtt_client_message_get

Aracıdan bir ileti alma

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_message_get(NXD_MQTT_CLIENT
    *client_ptr,
    UCHAR *topic_buffer, UINT topic_buffer_size,
    UINT *actual_topic_length, UCHAR *message_buffer,
    UINT message_buffer_size, UINT *actual_message_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, aracı tarafından yayınlanan bir iletiyi alır. Gelen tüm iletiler alma sırasında depolanır. Uygulama bu hizmeti bu iletileri almak için kullanır. Bu çağrı engellenmemiş. Alma sırası boşsa, bu hizmet ***NXD_MQTT_NO_MESSAGE** _ döndürür. Gelen ileti hakkında bildirim almak isteyen bir uygulama, alma geri araması işlevini kaydetmek için _ *_nxd_mqtt_client_receive_notify_set_** hizmetini çağırabilir.

Çağıranın, konu dizesi ve ileti gövdesi için bellek alanı sağlaması gerekir. Bu iki arabelleğe ait boyutlar *topic_buffer_size* ve *message_buffer_size* kullanılarak geçirilir. Konu dizesindeki gerçek bayt sayısı ve ileti gövdesi *actual_topic_length* ve *actual_message_length* döndürülür. Konu uzunluğu veya maszu uzunluğu, girilen arabellek alanından büyükse, bu hizmet *NXD_MQTT_INSUFFICIENT_BUFFER_SIZE* hata kodunu döndürür.

Uygulama daha büyük bir arabellek ayırır ve yeniden deneyin.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **topic_buffer** Konu dizesinin kopyalandığı bellek konumunun işaretçisi.
- **topic_buffer_size** Konu arabelleğinin boyutu.
- **actual_topic_length** Gerçek konu uzunluğunun döndürüldüğü bellek konumunun işaretçisi.
- **message_buffer** İleti dizesinin kopyalandığı bellek konumunun işaretçisi.
- **message_buffer_size** İleti arabelleğinin boyutu.
- **actual_message_length** İleti uzunluğunun döndürüldüğü bellek konumunun işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00) ileti başarıyla alındı.
- **NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası
- **NXD_MQTT_NO_MESSAGE** (0x1000a) alma kuyruğu boştur.
- **NXD_MQTT_INSUFFICIENT_BUFFER_SIZE** (0x1000d) konu arabelleği veya ileti arabelleği konu başlığı veya ileti için çok küçük.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi
- NXD_MQTT_INVALID_PARAMETER (0x10009) message_buffer veya topic_buffer işaretçi NULL

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
UCHAR topic[MAX_TOPIC_SIZE];
UCHAR message[MAX_TOPIC_SIZE];
UINT topic_length;
UINT message_length;

/* Retrieve a message from MQTT client receive queue. */
status = nxd_mqtt_client_message_get(&my_client, topic,
    sizeof(topic), &topic_length, message, sizeof(message),
    &message_length);

/* Check the return value. */
if(status == NXD_MQTT_SUCCESS)
{
/* A message is received. All done. */
}
else if (status == NXD_MQTT_NO_MESSAGE)
{
/* No more messages in the receive queue. All done. */
}
else
{
/* Receive error. */
}
```

## <a name="nxd_mqtt_client_disconnect_notify_set"></a>nxd_mqtt_client_disconnect_notify_set

MQTT iletisi bağlantısını kes bildirimi geri arama işlevini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_disconnect_notify_set(
    NXD_MQTT_CLIENT *client_ptr,
    VOID(*disconnect_notify)(NXD_MQTT_CLIENT* client_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet MQTT istemcisiyle bir geri çağırma işlevi kaydeder. MQTT, aracı bağlantısını algıladığında, uygulamayı uyarmak için bu bildirim işlevini çağırır. Bu nedenle uygulama, kayıp bir bağlantıyı algılamak ve aracıya yeniden bağlantı kurmak için bu geri çağırma işlevini kullanabilir.

```c
VOID callback_func(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.
- **disconnect_notify** MQTT, aracı bağlantısını algıladığında, çağrılacak Kullanıcı tarafından sağlanan geri arama işlevi kaybolur.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00), bağlantı kesme bildirimi işlevini başarıyla ayarladı.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
VOID disconnect_notify(NXD_MQTT_CLIENT *client_ptr)
{
/* MQTT client is disconnected from the broker. Notify the application so it can re-connect to the broker. */
}

status = nxd_mqtt_client_disconnect_notify_set(client_ptr,
    disconnect_notify);
```

## <a name="nxd_mqtt_client_disconnect"></a>nxd_mqtt_client_disconnect

MQTT istemcisinin aracıdan bağlantısını kesme

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_disconnect(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, istemcinin aracısından bağlantısını keser. Alma sırasındaki iletilerin serbest bırakıldığını unutmayın. İletme sırasındaki QoS 1 olan iletiler serbest bırakılır. İstemci sunucuya yeniden bağlandıktan sonra, istemci sunucuya yeniden bağlanmadığı müddetçe, *clean_session* bayrağı ***NX_TRUE*** olarak ayarlanan QoS 1 iletileri işlenebilir.

Bağlantı TLS güvenlik koruması ile yapılmışsa, bu hizmet TCP bağlantısının bağlantısını kesmeden önce TLS oturumunu kapatır.

Gerçek TCP yuvası bağlantı kesilmesi çağrısının NXD_MQTT_SOCKET_TIMEOUT (süreölçer işaretleri) tarafından tanımlanan bir bekleme seçeneği vardır. Varsayılan değer NX_WAIT_FOREVER. Ağ bağlantısının kaybolması veya sunucunun yanıt vermemesi durumunda sınırsız askıya alma önlemek için bu seçeneği sınırlı bir değere ayarlayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00) aracısının bağlantısı başarıyla kesildi
- **NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX 'i alamadı.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Disconnect from the broker. */
status = nxd_mqtt_client_disconnect(&my_client);

/* If status is NXD_MQTT_SUCCESS the client is successfully
disconnected from the broker. */
```

## <a name="nxd_mqtt_client_delete"></a>nxd_mqtt_client_delete

MQTT istemci örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nxd_mqtt_client_delete(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet MQTT istemci örneğini siler ve iç kaynakları yayınlar. Bu hizmet hala bağlıysa, istemcinin aracısının bağlantısını otomatik olarak keser. Henüz iletilmemiş veya onaylanmamış iletiler serbest bırakılır. Alınan ancak uygulama tarafından alınmayan iletiler de serbest bırakılır.

Bağlantı TLS güvenlik koruması ile yapılmışsa, bu hizmet TCP bağlantısının bağlantısını kesmeden önce TLS oturumunu kapatır.

İstemci silindikten sonra MQTT hizmetini kullanmak isteyen bir uygulamanın yeni bir örnek oluşturması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** MQTT Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NXD_MQTT_SUCCESS** (0x00) MQTT istemcisini başarıyla sildi.
- NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the MQTT client instance. */
status = nxd_mqtt_client_delete(&my_client);

/* If status is NXD_MQTT_SUCCESS the client is successfully
deleted from the system. */
```
