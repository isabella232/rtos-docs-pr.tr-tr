---
title: Bölüm 3-Azure RTOS NetX Duo Telnet hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX Duo Telnet hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 991ec53aaba052b4f42da6e5a541151953121e76
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825714"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-telnet-services"></a>Bölüm 3-Azure RTOS NetX Duo Telnet hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX Duo Telnet hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_telnet_client_connect**: *bir Telnet istemcisini IPv4 adresiyle bağlama*
- **nxd_telnet_client_connect**: IPv6 *bir IPv6 Telnet istemcisini IPv6 adresiyle bağlama*
- **nx_telnet_client_create**: *bir Telnet istemcisi oluşturma*
- **nx_telnet_client_delete**: *bir Telnet istemcisini silme*
- **nx_telnet_client_disconnect**: *bir Telnet istemcisinin bağlantısını kesme*
- **nx_telnet_client_packet_receive**: *Telnet istemcisi aracılığıyla paket alma*
- **nx_telnet_client_packet_send**: *Telnet istemcisi aracılığıyla paket gönder*
- **nx_telnet_server_create**: *bir Telnet sunucusu oluşturma*
- **nx_telnet_server_delete**: *bir Telnet sunucusunu silme*
- **nx_telnet_server_disconnect**: *bir Telnet istemcisinin bağlantısını kesme*
- **nx_telnet_server_get_open_connection_count**: *açık bağlantı sayısını alma*
- **nx_telnet_server_packet_send**: *istemci bağlantısı aracılığıyla paket gönder*
- **nx_telnet_server_packet_pool_set**: *paket havuzunu Telnet sunucusu paket havuzu olarak ayarla*
- **nx_telnet_server_start**: *bir Telnet sunucusu başlatın*
- **nx_telnet_server_stop**: *bir Telnet sunucusunu durdur*

## <a name="nx_telnet_client_connect"></a>nx_telnet_client_connect

Bir Telnet Istemcisini IPv4 adresiyle bağlama

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                              ULONG server_ip, UINT server_port, 
                              ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulan Telnet Istemci örneğini, Telnet sunucusu için bir IPv4 adresi kullanarak belirtilen IP ve bağlantı noktasındaki sunucuya bağlamayı dener. Bu hizmet, bir NXD_ADDRESS denetim bloğunda ULONG sunucu IP adresini ekler ve aşağıda açıklanan *nxd_telnet_client_connect* hizmeti ÇAĞRıLMADAN önce IP sürümünü 4 ' e ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: Telnet istemci denetim bloğu işaretçisi.
- **server_ip**: Telnet sunucusunun IPv4 adresi.
- **SERVER_PORT**: sunucu TCP bağlantı noktası (Telnet sunucusu bağlantı noktası 23 ' dir).
- **wait_option**: hizmetin Telnet istemcisi bağlantısı için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

    - **zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
    - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) Istemci bağlantısı başarılı oldu.
- **NX_TELNET_NOT_DISCONNECTED**: (0xf4) istemci zaten bağlı.
- NX_PTR_ERROR: (0x07) geçersiz Istemci işaretçisi.
- NX_IP_ADDRESS_ERROR: (0x21) geçersiz IP adresi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Connect the Telnet Client instance “my_client” to the Server at 
   IP address 1.2.3.4 and port 23.  */
status =  nx_telnet_client_connect(&my_client, IP_ADDRESS(1,2,3,4), 23, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   connected to the Telnet Server.  */
```

## <a name="nxd_telnet_client_connect"></a>nxd_telnet_client_connect

Bir Telnet Istemcisini IPv6 veya IPv4 adresiyle bağlama

### <a name="prototype"></a>Prototype

```c
UINT nxd_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                               NXD_ADDRESS *server_ip_address, 
                               UINT server_port, 
                               ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulan Telnet Istemci örneğini, Telnet sunucusunun IPv6 adresini kullanarak belirtilen IP ve bağlantı noktasındaki sunucuya bağlamayı dener. Bu hizmet bir IPv4 veya IPv6 adresi alabilir, ancak NXD_ADDRESS değişken *server_ip_address içermeli.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: Telnet istemci denetim bloğu işaretçisi.
- **server_ip_address**: sunucunun IP adresi.
- **SERVER_PORT**: sunucu TCP bağlantı noktası (Telnet sunucusu bağlantı noktası 23 ' dir).
- **wait_option**: hizmetin Telnet istemcisi bağlantısı için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

    - **zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
    - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) Istemci bağlantısı başarılı oldu.
- **NX_TELNET_ERROR**: (0Xf0) istemci bağlantı hatası.
- **NX_TELNET_NOT_DISCONNECTED**: (0xf4) istemci zaten bağlı.
- NX_PTR_ERROR: (0x07) geçersiz Istemci işaretçisi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.
- NX_TELNET_INVALID_PARAMETER: (0xF5) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Connect the Telnet Client instance “my_client” to the Server at 
   IPv6 address 20010db1:0:f101::101 and port 23.  */
status =  nxd_telnet_client_connect(&my_client, &server_ip_address, 23, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   connected to the Telnet Server.  */
```

## <a name="nx_telnet_client_create"></a>nx_telnet_client_create

Telnet Istemcisi oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_create(NX_TELNET_CLIENT *client_ptr, 
                             CHAR *client_name, NX_IP *ip_ptr, 
                             ULONG window_size);
```

### <a name="description"></a>Açıklama

Bu hizmet bir Telnet Istemci örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: Telnet istemci denetim bloğu işaretçisi.
- **client_name**: istemci örneğinin adı.
- **ip_ptr**: IP örneğine yönelik işaretçi.
- **window_size**: Bu ISTEMCI için TCP alma penceresinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) Istemci oluşturma başarılı.
- **NX_TELNET_ERROR**: (0Xf0) yuva oluşturma hatası.
- NX_PTR_ERROR: (0x07) geçersiz Istemci veya IP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create the Telnet Client instance “my_client” on the IP instance “ip_0”.  */
status =  nx_telnet_client_create(&my_client, “My Telnet Client”, &ip_0, 2048);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   created.  */
```
## <a name="nx_telnet_client_delete"></a>nx_telnet_client_delete

Bir Telnet Istemcisini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_delete(NX_TELNET_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir Telnet Istemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: Telnet istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) Istemci silme başarılı.
- **NX_TELNET_NOT_DISCONNECTED**: (0xf4) istemci hala bağlı.
- NX_PTR_ERROR: (0x07) geçersiz Istemci işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_delete(&my_client);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   deleted.  */
```

## <a name="nx_telnet_client_disconnect"></a>nx_telnet_client_disconnect

Telnet Istemcisinin bağlantısını kesme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_disconnect(NX_TELNET_CLIENT *client_ptr, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce bağlı bir Telnet Istemci örneğinin bağlantısını keser.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: Telnet istemci denetim bloğu işaretçisi.
- **wait_option**: hizmetin Telnet istemcisinin bağlantısını kesmek için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

    - **zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
    - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) Istemci bağlantısının başarıyla kesilmesi.
- **NX_TELNET_NOT_CONNECTED**: (0Xf3) istemci bağlı değil.
- NX_PTR_ERROR: (0x07) geçersiz Istemci işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.


### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

/* Disconnect the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_disconnect(&my_client, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   disconnected.  */
```

## <a name="nx_telnet_client_packet_receive"></a>nx_telnet_client_packet_receive

Telnet Istemcisi aracılığıyla paket alma

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_packet_receive(NX_TELNET_CLIENT *client_ptr, 
                                     NX_PACKET **packet_ptr, 
                                     ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce bağlı olan Telnet Istemci örneğinden bir paket alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: Telnet istemci denetim bloğu işaretçisi.
- **packet_ptr**: alınan paket için hedef işaretçisi.
- **wait_option**: hizmetin Telnet istemci paketi alma süresini ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
    - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) istemci paketi alma başarılı.
- NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

/* Receive a packet from the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_receive(&my_client, &my_packet, 100);

/* If status is NX_SUCCESS the “my_packet” pointer contains data received from
   the Telnet Client connection.  */
```
## <a name="nx_telnet_client_packet_send"></a>nx_telnet_client_packet_send

Telnet Istemcisi aracılığıyla paket gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_packet_send(NX_TELNET_CLIENT *client_ptr, 
                                  NX_PACKET *packet_ptr, 
                                  ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce bağlı olan Telnet Istemci örneği aracılığıyla bir paket gönderir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr**: Telnet istemci denetim bloğu işaretçisi.
- **packet_ptr**: gönderileceği pakete yönelik işaretçi.
- **wait_option**: hizmetin Telnet istemci paketinin gönderilmesi için bekleyeceği süreyi tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
    - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı istemci paketi gönderme.
- **NX_TELNET_ERROR**: (0Xf0) paket gönderme başarısız oldu – çağıran, paketi serbest bırakmaktan sorumludur.
- NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Send a packet via the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_send(&my_client, my_packet, 100);
/* If status is NX_SUCCESS the packet was successfully sent.  */

```

## <a name="nx_telnet_server_create"></a>nx_telnet_server_create

Telnet sunucusu oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_create(NX_TELNET_SERVER *server_ptr, CHAR *server_name, NX_IP *ip_ptr, 
                             VOID *stack_ptr, ULONG stack_size, 
                             void (*new_connection)(struct NX_TELNET_SERVER_STRUCT*telnet_server_ptr, 
                                                    UINT logical_connection), 
                             void (*receive_data)(struct NX_TELNET_SERVER_STRUCT *telnet_server_ptr, 
                                                  UINT logical_connection, NX_PACKET *packet_ptr), 
                             void (*connection_end)(struct NX_TELNET_SERVER_STRUCT *telnet_server_ptr, 
                                                    UINT logical_connection));

```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneğinde bir Telnet Server örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: Telnet sunucu denetim bloğu işaretçisi.
- **SERVER_NAME**: Telnet sunucu örneğinin adı.
- **ip_ptr**: ilişkili IP örneğine yönelik işaretçi.
- **stack_ptr**: iç sunucu iş parçacığı için yığın işaretçisi.
- **sack_size**: yığının bayt cinsinden boyutu.
- **new_connection**: uygulama geri çağırma yordamı işlev işaretçisi. Bu yordam, sunucu tarafından her yeni bir Telnet Istemci bağlantı isteği algılandığında çağrılır.
- **receive_data**: uygulama geri çağırma yordamı işlev işaretçisi. Bu yordam, bağlantıda her yeni bir Telnet Istemci verisi olduğunda çağrılır. Bu yordam, paketin serbest bırakılmasından sorumludur.
- **end_connection**: uygulama geri çağırma yordamı işlev işaretçisi. Bu yordam, bir Telnet Istemci bağlantısının Istemci tarafından bağlantısı kesildiğinde veya Istemci bağlantısı zaman aşımına uğradığında ("etkinlik zaman aşımı" süresi dolduğunda) çağrılır. Sunucu ayrıca aşağıda açıklanan *nx_telnet_server_disconnect* hizmeti aracılığıyla bağlantısını kesebilir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) sunucu oluşturma başarılı.
- NX_PTR_ERROR: (0x07) sunucu, IP, yığın veya uygulama geri çağırma işaretçileri geçersiz.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create a Telnet Server instance “my_server”.  */
status =  nx_telnet_server_create(&my_server, "Telnet Server", &ip_0, 
                                   pointer, 2048, telnet_new_connection, 
                                   telnet_receive_data, telnet_connection_end);


/* If status is NX_SUCCESS the Telnet Server was successfully created.  */
```
## <a name="nx_telnet_server_delete"></a>nx_telnet_server_delete

Bir Telnet sunucusunu silme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_delete(NX_TELNET_SERVER *server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir Telnet sunucusu örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: Telnet sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) sunucu başarıyla silindi.
- NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_delete(&my_server);

/* If status is NX_SUCCESS the Telnet Server was successfully deleted.  */
```

## <a name="nx_telnet_server_disconnect"></a>nx_telnet_server_disconnect

Telnet Istemcisinin bağlantısını kesme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_disconnect(NX_TELNET_SERVER *server_ptr, UINT logical_connection);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu Telnet sunucu örneğindeki daha önce bağlı bir Istemcinin bağlantısını keser. Bu yordam tipik olarak, alınan verilerde algılanan bir koşula yanıt olarak uygulamanın veri geri çağırma işlevinden çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: Telnet sunucu denetim bloğu işaretçisi.
- **logical_connection**: Bu sunucudaki istemci bağlantısına karşılık gelen mantıksal bağlantı. 0 ile NX_TELENET_MAX_CLIENTS arasında geçerli değer aralığı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) sunucu bağlantısı başarıyla kesilir.
- **NX_TELNET_ERROR**: (0Xf0) sunucu bağlantısı kesilemedi.
- NX_OPTION_ERROR: (0x0A) geçersiz mantıksal bağlantı.
- NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

/* Disconnect the Telnet Client associated with logical connection 2 on 
   the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_disconnect(&my_server, 2);

/* If status is NX_SUCCESS the Client on logical connection 2 was 
   disconnected.  */
```

## <a name="nx_telnet_server_get_open_connection_count"></a>nx_telnet_server_get_open_connection_count

Açık durumdaki bağlantıların geri dönüş sayısı

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_get_open_connection_count(NX_TELNET_SERVER *server_ptr, UINT *connection_count);
```

### <a name="description"></a>Açıklama

Bu hizmet, şu anda bağlı olan Telnet Istemcilerinin sayısını döndürür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: Telnet sunucu denetim bloğu işaretçisi.
- **Connection_count**: bağlantı sayısını depolamak için bellek işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı tamamlama.
- NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Get the number of Telnet Clients connected to the Server. */

status =  nx_telnet_server_get_open_connection_count(&my_server, &conn_count);

/* If status is NX_SUCCESS the conn_count holds the number of open connections.  */

```

## <a name="nx_telnet_server_packet_send"></a>nx_telnet_server_packet_send

Istemci bağlantısı aracılığıyla paket gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_packet_send(NX_TELNET_SERVER *server_ptr, 
                                  UINT logical_connection, 
                                  NX_PACKET *packet_ptr, 
                                  ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu Telnet sunucu örneğindeki Istemci bağlantısına bir paket gönderir. Bu yordam tipik olarak, alınan verilerde algılanan bir koşula yanıt olarak uygulamanın veri geri çağırma işlevinden çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: Telnet sunucu denetim bloğu işaretçisi.
- **logical_connection**: Bu sunucudaki istemci bağlantısına karşılık gelen mantıksal bağlantı. 0 ile NX_TELENET_MAX_CLIENTS arasında geçerli değer aralığı.
- **packet_ptr**: alınan pakete yönelik işaretçi.
- **wait_option**: hizmetin Telnet sunucusu paketini gönderme süresini ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.
    - **TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur. 

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı paket gönderme.
- **NX_TELNET_FAILED**: (0Xf2) TCP yuvası gönderme başarısız oldu.
- NX_OPTION_ERROR: (0x0A) geçersiz mantıksal bağlantı.
- NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Send a packet to the Telnet Client associated with logical connection 2 on 
   the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_packet_send(&my_server, 2, my_packet, 100);

/* If status is NX_SUCCESS the packet was sent to the Client on logical 
   connection 2.  */
```

## <a name="nx_telnet_server_packet_pool_set"></a>nx_telnet_server_packet_pool_set

Daha önce oluşturulan paket havuzunu Telnet sunucu havuzu olarak ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_packet_pool_set(NX_TELNET_SERVER *server_ptr, NX_PACKET_POOL *packet_pool_ptr);

```

### <a name="description"></a>Açıklama

Bu hizmet, NX_TELNET_SERVER_USER_CREATE_PACKET_POOL tanımlanmışsa, daha önce oluşturulmuş bir paket havuzunu Telnet sunucusu paket havuzu olarak ayarlar. Ayrıca, Telnet sunucusunun Telnet istemcilerine Telnet seçeneklerini iletmek için bir paket havuzuna ihtiyacı olacak şekilde NX_TELNET_SERVER_OPTION_DISABLE tanımlanmamalıdır.

Bu, uygulamaların paket havuzunu farklı bellekte oluşturmasına izin verir, örneğin, önbellek belleği, Telnet sunucu yığınından daha fazla. Bu işlev, Telnet sunucusu paket havuzunun zaten ayarlanmış olup olmadığını denetlemez. Null olmayan bir Telnet sunucusu paket havuzu işaretçisi üzerinde çağrılırsa, üzerine yazar ve giriş işaretçisi tarafından işaret edilen paket havuzu ile var olan paket havuzunu değiştirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: Telnet sunucu denetim bloğu işaretçisi
- **packet_pool_ptr**: daha önce oluşturulmuş olan paket havuzuna yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) havuz başarıyla ayarlandı.
- NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Init, Iş parçacıkları

### <a name="example"></a>Örnek

```c
status =  nx_packet_pool_create(&telnet_server_packet_pool, 
                                "Telnet Server Packet Pool", 
                                telnet_server_pool_area, 600*10);

/* Set the packet pool as the Telnet Server packet pool.   */
status =  nx_telnet_server_packet_pool_set(&my_server, &telnet_server_packet_pool);

/* If status is NX_SUCCESS the packet pool is set as Telnet Server pool.  */
```
## <a name="nx_telnet_server_start"></a>nx_telnet_server_start

Telnet sunucusu başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_start(NX_TELNET_SERVER *server_ptr);

```

### <a name="description"></a>Açıklama

Bu hizmet önceden oluşturulmuş bir Telnet sunucu örneğini başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: Telnet sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarıyla başlatıldı.
- **NX_TELNET_NO_PACKET_POOL**: (0Xf6) paket havuzu ayarlanmadı
- NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_start(&my_server);

/* If status is NX_SUCCESS the Server was started.  */
```

## <a name="nx_telnet_server_stop"></a>nx_telnet_server_stop

Bir Telnet sunucusunu durdur

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_stop(NX_TELNET_SERVER *server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet önceden oluşturulmuş ve başlatılmış bir Telnet sunucu örneğini durduruyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr**: Telnet sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarıyla durduruldu
- NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_stop(&my_server);

/* If status is NX_SUCCESS the Server was stopped.  */
```