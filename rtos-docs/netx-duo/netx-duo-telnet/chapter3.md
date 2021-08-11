---
title: Bölüm 3 - NetX Duo Azure RTOS hizmetlerinin açıklaması
description: Bu bölümde Tüm NetX Duo Telnet Services Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 70bf4016793572d7327d12be182750316659c3c4260d2f7db8acddbba00c5601
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792001"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-telnet-services"></a>Bölüm 3 - NetX Duo Azure RTOS hizmetlerinin açıklaması

Bu bölümde Tüm NetX Duo Telnet Services Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_telnet_client_connect:** Bağlan *IPv4 adresine sahip bir Telnet İstemcisi'ne sahip*
- **nxd_telnet_client_connect:** Bağlan *IPv6 adresine sahip bir IPv6 Telnet İstemcisi'ne sahip*
- **nx_telnet_client_create:** *Telnet İstemcisi Oluşturma*
- **nx_telnet_client_delete:** *Telnet İstemcisini Silme*
- **nx_telnet_client_disconnect:** *Telnet İstemcisi Bağlantısını Kesme*
- **nx_telnet_client_packet_receive:** *Telnet İstemcisi aracılığıyla paket alma*
- **nx_telnet_client_packet_send:** *Telnet İstemcisi aracılığıyla paket gönderme*
- **nx_telnet_server_create:** *Telnet Sunucusu Oluşturma*
- **nx_telnet_server_delete:** *Telnet Sunucusunu Silme*
- **nx_telnet_server_disconnect:** *Telnet İstemcisi Bağlantısını Kesme*
- **nx_telnet_server_get_open_connection_count:** Açık *bağlantı sayısını alma*
- **nx_telnet_server_packet_send:** Paketi *İstemci bağlantısı üzerinden gönderme*
- **nx_telnet_server_packet_pool_set:** Paket *havuzunu Telnet Sunucusu paket havuzu olarak ayarlayın*
- **nx_telnet_server_start:** *Telnet Sunucusu Başlatma*
- **nx_telnet_server_stop:** *Telnet Sunucusunu Durdurma*

## <a name="nx_telnet_client_connect"></a>nx_telnet_client_connect

Bağlan IPv4 adresine sahip bir Telnet İstemcisi ekleme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                              ULONG server_ip, UINT server_port, 
                              ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, telnet sunucusu için bir IPv4 adresi kullanarak önceden oluşturulmuş Telnet İstemci örneğini belirtilen IP ve bağlantı noktası üzerinden Sunucuya bağlamaya çalışır. Bu hizmet, ULONG sunucusu IP adresini bir NXD_ADDRESS denetim bloğuna ekler ve aşağıda  açıklanan nxd_telnet_client_connect çağırmadan önce IP sürümünü 4 olarak ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr:** Telnet İstemcisi denetim bloğuna işaretçi.
- **server_ip:** Telnet Sunucusunun IPv4 Adresi.
- **server_port:** Sunucunun TCP Bağlantı Noktası (Telnet Server, bağlantı noktası 23'tir).
- **wait_option:** Hizmetin Telnet İstemcisi'nin bağlanmasını ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

    - **zaman aşımı değeri:**(0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçerek Telnet Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
    - **TX_WAIT_FOREVER:**(0xFFFFFFFF)TX_WAIT_FOREVER telnet sunucusu i isteği yanıtlayana kadar çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı İstemci bağlantısı.
- **NX_TELNET_NOT_DISCONNECTED:**(0xF4) İstemci zaten bağlı.
- NX_PTR_ERROR: (0x07) Geçersiz İstemci işaretçisi.
- NX_IP_ADDRESS_ERROR: (0x21) Geçersiz IP adresi.
- NX_CALLER_ERROR: (0x11) Geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin Verilen

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

Bağlan IPv6 veya IPv4 adresine sahip bir Telnet İstemcisi'ne sahip

### <a name="prototype"></a>Prototype

```c
UINT nxd_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                               NXD_ADDRESS *server_ip_address, 
                               UINT server_port, 
                               ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş Telnet İstemcisi örneğini, Telnet Sunucusunun IPv6 adresini kullanarak belirtilen IP ve bağlantı noktası üzerinden Sunucuya bağlamaya çalışır. Bu hizmet bir IPv4 veya IPv6 adresi aldırabilirsiniz, ancak bu adres bir NXD_ADDRESS içinde *server_ip_address.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr:** Telnet İstemcisi denetim bloğuna işaretçi.
- **server_ip_address:** Sunucunun IP Adresi.
- **server_port:** Sunucunun TCP Bağlantı Noktası (Telnet Server, bağlantı noktası 23'tir).
- **wait_option:** Hizmetin Telnet İstemcisi'nin bağlanmasını ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

    - **zaman aşımı değeri:**(0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçerek Telnet Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
    - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER telnet sunucusu itene yanıt verene kadar çağrıyı çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı İstemci bağlantısı.
- **NX_TELNET_ERROR:**(0xF0) İstemci bağlantısı hatası.
- **NX_TELNET_NOT_DISCONNECTED:**(0xF4) İstemci zaten bağlı.
- NX_PTR_ERROR: (0x07) Geçersiz İstemci işaretçisi.
- NX_CALLER_ERROR: (0x11) Geçersiz hizmet çağıranı.
- NX_TELNET_INVALID_PARAMETER: (0xF5) İşaretçi olmayan giriş geçersiz

### <a name="allowed-from"></a>İzin Verilen

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

Telnet İstemcisi Oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_create(NX_TELNET_CLIENT *client_ptr, 
                             CHAR *client_name, NX_IP *ip_ptr, 
                             ULONG window_size);
```

### <a name="description"></a>Description

Bu hizmet bir Telnet İstemcisi örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr:** Telnet İstemcisi denetim bloğuna işaretçi.
- **client_name:** İstemci örneğinin adı.
- **ip_ptr:** IP örneğine işaretçi.
- **window_size:** Bu İstemci için TCP alma penceresinin boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı İstemci oluşturma.
- **NX_TELNET_ERROR:**(0xF0) Yuva oluşturma hatası.
- NX_PTR_ERROR: (0x07) Geçersiz İstemci veya IP işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Create the Telnet Client instance “my_client” on the IP instance “ip_0”.  */
status =  nx_telnet_client_create(&my_client, “My Telnet Client”, &ip_0, 2048);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   created.  */
```
## <a name="nx_telnet_client_delete"></a>nx_telnet_client_delete

Telnet İstemcisini Silme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_delete(NX_TELNET_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir Telnet İstemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr:** Telnet İstemcisi denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı İstemci silme.
- **NX_TELNET_NOT_DISCONNECTED:**(0xF4) İstemci hala bağlı.
- NX_PTR_ERROR: (0x07) Geçersiz İstemci işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_delete(&my_client);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   deleted.  */
```

## <a name="nx_telnet_client_disconnect"></a>nx_telnet_client_disconnect

Telnet İstemcisi Bağlantısını Kesme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_disconnect(NX_TELNET_CLIENT *client_ptr, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, daha önce bağlanan bir Telnet İstemcisi örneğinin bağlantısını keser.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr:** Telnet İstemcisi denetim bloğuna işaretçi.
- **wait_option:** Hizmetin Telnet İstemci bağlantısının ne kadar süreyle bağlantısının kesilmesini bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

    - **zaman aşımı değeri:**(0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçerek Telnet Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
    - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER telnet sunucusu itene yanıt verene kadar çağrıyı çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı İstemci bağlantısı kesildi.
- **NX_TELNET_NOT_CONNECTED:**(0xF3) İstemci bağlı değil.
- NX_PTR_ERROR: (0x07) Geçersiz İstemci işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.


### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

/* Disconnect the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_disconnect(&my_client, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   disconnected.  */
```

## <a name="nx_telnet_client_packet_receive"></a>nx_telnet_client_packet_receive

Telnet İstemcisi aracılığıyla paket alma

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_packet_receive(NX_TELNET_CLIENT *client_ptr, 
                                     NX_PACKET **packet_ptr, 
                                     ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, daha önce bağlanan Telnet İstemci örneğinden bir paket alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr:** Telnet İstemcisi denetim bloğuna işaretçi.
- **packet_ptr:** Alınan paket için hedefin işaretçisi.
- **wait_option:** Hizmetin Telnet İstemci paketinin ne kadar süreyle alınıp alınmayacaklarını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri:**(0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçerek Telnet Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
    - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER telnet sunucusu itene yanıt verene kadar çağrıyı çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı İstemci paketi alma.
- NX_PTR_ERROR: (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) Geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c

/* Receive a packet from the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_receive(&my_client, &my_packet, 100);

/* If status is NX_SUCCESS the “my_packet” pointer contains data received from
   the Telnet Client connection.  */
```
## <a name="nx_telnet_client_packet_send"></a>nx_telnet_client_packet_send

Telnet İstemcisi aracılığıyla paket gönderme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_client_packet_send(NX_TELNET_CLIENT *client_ptr, 
                                  NX_PACKET *packet_ptr, 
                                  ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, daha önce bağlanan Telnet İstemci örneği üzerinden bir paket gönderir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr:** Telnet İstemcisi denetim bloğuna işaretçi.
- **packet_ptr:** Göndermek için paketin işaretçisi.
- **wait_option:** Hizmetin Telnet İstemci paketi göndermesini ne kadar bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **zaman aşımı değeri:**(0x00000001 0xFFFFFFFE) Sayısal bir değer (1-0xFFFFFFFE) seçerek Telnet Sunucusu yanıtı beklerken askıya alınacak zamanlayıcı saat sayısı üst sayısını belirtir.
    - **TX_WAIT_FOREVER:**(0xFFFFFFFF) TX_WAIT_FOREVER telnet sunucusu itene yanıt verene kadar çağrıyı çağıran iş parçacığının süresiz olarak askıya alınmasına neden olur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı İstemci paketi gönderme.
- **NX_TELNET_ERROR:**(0xF0) Paketi gönderme başarısız oldu – paketi serbest bırakmak çağıranın sorumluluğundadır.
- NX_PTR_ERROR: (0x07) Geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) Geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Send a packet via the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_send(&my_client, my_packet, 100);
/* If status is NX_SUCCESS the packet was successfully sent.  */

```

## <a name="nx_telnet_server_create"></a>nx_telnet_server_create

Telnet Sunucusu oluşturma

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

### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneğinde bir Telnet Sunucusu örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr:** Telnet Sunucusu denetim bloğuna işaretçi.
- **server_name:** Telnet Sunucusu örneğinin adı.
- **ip_ptr:** İlişkili IP örneğinin işaretçisi.
- **stack_ptr:** İç Sunucu iş parçacığı için yığın işaretçisi.
- **sack_size:** Yığının bayt cinsinden boyutu.
- **new_connection:** Uygulama geri çağırma yordamı işlev işaretçisi. Bu yordam, Sunucu tarafından yeni bir Telnet İstemcisi bağlantı isteği algılandığında çağrılır.
- **receive_data:** Uygulama geri çağırma yordamı işlev işaretçisi. Bu yordam, bağlantıda yeni bir Telnet İstemcisi verisi mevcut olduğunda çağrılır. Bu yordam paketi serbest bırakmakla sorumludur.
- **end_connection:** Uygulama geri çağırma yordamı işlev işaretçisi. Bu yordam, İstemci tarafından Telnet İstemcisi bağlantısının kesildiğinde veya İstemci bağlantısının zaman aşımına (etkinlik zaman aşımı" süresi dolduğunda) çağrılır. Sunucu ayrıca aşağıda açıklanan nx_telnet_server_disconnect *bağlantısı* kesebilirsiniz.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı Sunucu oluşturma.
- NX_PTR_ERROR: (0x07) Geçersiz Sunucu, IP, yığın veya uygulama geri çağırma işaretçileri.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Create a Telnet Server instance “my_server”.  */
status =  nx_telnet_server_create(&my_server, "Telnet Server", &ip_0, 
                                   pointer, 2048, telnet_new_connection, 
                                   telnet_receive_data, telnet_connection_end);


/* If status is NX_SUCCESS the Telnet Server was successfully created.  */
```
## <a name="nx_telnet_server_delete"></a>nx_telnet_server_delete

Telnet Sunucusunu silme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_delete(NX_TELNET_SERVER *server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir Telnet Server örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **server_ptr:** Telnet Sunucusu denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı Sunucu silme.
- NX_PTR_ERROR: (0x07) Geçersiz Sunucu işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_delete(&my_server);

/* If status is NX_SUCCESS the Telnet Server was successfully deleted.  */
```

## <a name="nx_telnet_server_disconnect"></a>nx_telnet_server_disconnect

Telnet İstemcisi Bağlantısını Kesme

### <a name="prototype"></a>Prototype

```c
UINT nx_telnet_server_disconnect(NX_TELNET_SERVER *server_ptr, UINT logical_connection);
```

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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