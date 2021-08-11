---
title: Bölüm 3 - NetX Duo Azure RTOS SNTP İstemci Hizmetlerinin Açıklaması
description: Bu bölümde, tüm NetX Duo SNTP İstemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7aee18642e480ec61488515164c8a6816753dca86eb8f6d146ea22d4956e037a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791678"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-sntp-client-services"></a>Bölüm 3 - NetX Duo Azure RTOS SNTP İstemci Hizmetlerinin Açıklaması

Bu bölümde tüm NetX Duo SNTP Azure RTOS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_sntp_client_create:** *SNTP İstemcisi Oluşturma*
- **nx_sntp_client_delete:** *SNTP İstemcisini Silme*
- **nx_sntp_client_get_local_time:** *SNTP İstemcisi yerel saati al*
- **nx_sntp_client_get_local_time_extended:** *SNTP İstemcisi yerel saati al*
- **nx_sntp_client_initialize_broadcast:** *IPv4 yayın işlemi için İstemci başlatma*
- **nxd_sntp_client_initialize_broadcast:** *IPv6 veya IPv4 yayın işlemi için İstemci başlatma*
- **nx_sntp_client_initialize_unicast:** *IPv4 tek noktaya yayın işlemi için İstemci başlatma*
- **nxd_sntp_client_initialize_unicast:** *IPv4 veya IPv6 tek noktaya* yayın işlemi için İstemci başlatma
- **nx_sntp_client_receiving_udpates:** İstemci *şu anda geçerli SNTP güncelleştirmeleri alıyor*
- **nx_sntp_client_request_unicast_time:** Doğrudan *NTP Sunucusuna tek noktaya yayın isteği gönderme*
- **nx_sntp_client_run_broadcast:** *İstemciyi yayın modunda çalıştırma*
- **nx_sntp_client_run_unicast:** *İstemciyi tek noktaya yayın modunda çalıştırma*
- **nx_sntp_client_set_local_time:** *SNTP İstemcisi ilk yerel saati ayarlayın*
- **nx_sntp_client_set_time_update_notify:** *SNTP güncelleştirme geri aramasını ayarlama*
- **nx_sntp_client_stop:** *SNTP İstemcisi iş parçacığını durdurun*
- **nx_sntp_client_utility_display_date_and_time:** *NTP süresi saniye olarak görüntülenir*
- **nx_sntp_client_utility_msecs_to_fraction:** *Milisaniyeleri NTP kesir bileşenine dönüştürme*
- **nx_sntp_client_utility_usecs_to_fraction:** *Mikrosaniyeleri NTP kesir bileşenine dönüştürme*
- **nx_sntp_client_utility_fraction_to_usecs:** *NTP kesir bileşenini mikrosaniyeye dönüştürme*


## <a name="nx_sntp_client_create"></a>nx_sntp_client_create

SNTP İstemcisi Oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_create(NX_SNTP_CLIENT *client_ptr, NX_IP *ip_ptr,  
                                     UINT iface_index, 
                                     NX_PACKET_POOL *packet_pool_ptr, 
UINT (*leap_second_handler)(NX_SNTP_CLIENT *client_ptr, 
                                        UINT indicator), 
UINT (*kiss_of_death_handler)(NX_SNTP_CLIENT *client_ptr, 
                               NX_SNTP_TIME_MESSAGE *server_time_msg),
VOID (random_number_generator)(struct NX_SNTP_CLIENT_STRUCT 
                                *client_ptr, ULONG *rand));

```

### <a name="description"></a>Description

Bu hizmet bir SNTP İstemci örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP İstemcisi denetim bloğu işaretçisi

- **ip_ptr** İstemci IP örneğine işaretçi

- **iface_index** SNTP ağ arabirimine dizin oluşturma

- **packet_pool_ptr** İstemci paket havuzu işaretçisi

- **leap_second_handler** Yaklaşan artık saniyeye uygulama yanıtı için geri çağırma

- **kiss_of_death_handler** Ölüm Paketi almaya uygulama yanıtı için geri çağırma

- **random_number_generator** Rastgele sayı oluşturucu hizmetine geri çağrı

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı İstemci oluşturma

- **NX_SNTP_INSUFFICIENT_PACKET_PAYLOAD** (0xD2A) İşaretçi olmayan giriş geçersiz

- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

- NX_INVALID_INTERFACE (0x4C) Geçersiz ağ arabirimi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Create the SNTP Client on the primary interface. */
UINT iface_index = 0;
status =  nx_sntp_client_create(&demo_client, 
                     iface_index, &client_ip, 
&client_packet_pool, leap_second_handler, 
                    kiss_of_death_handler, 
NULL /* no random_number_generator callback */);

/* If status is NX_SUCCESS an SNTP Client instance was successfully
   created.  */

```

## <a name="nx_sntp_client_delete"></a>nx_sntp_client_delete

SNTP İstemcisini Silme

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_delete(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir SNTP İstemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP İstemcisi denetim bloğu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı İstemci oluşturma

- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) Geçersiz hizmet çağıran

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete the SNTP Client. */
status =  nx_sntp_client_delete(&demo_client);

/* If status is NX_SUCCESS an SNTP Client 
   instance was successfully deleted.  */

```

## <a name="nx_sntp_client_get_local_time"></a>nx_sntp_client_get_local_time

SNTP İstemcisi yerel saati al

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_get_local_time(NX_SNTP_CLIENT *client_ptr , 
                                                ULONG *seconds, 
                                                ULONG *fraction, 
                                                CHAR *buffer);

```

### <a name="description"></a>Description

Bu hizmet, dize iletisi biçimindeki verileri almak için bir seçenek arabellek işaretçisi girişi ile SNTP İstemcisi yerel saat alır.

Bu hizmet kullanım dışıdır. Geliştiricilerin nx_sntp_client_get_local_time_extended () *geçişleri* teşvik edilecektir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP İstemcisi denetim bloğu işaretçisi

- **saniye** Yerel saat saniye işaretçisi

- **kesir** Yerel saat kesir bileşeni

- **buffer (arabellek)** Yazma zamanı verilerini arabelleğe alma işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı İstemci oluşturma

- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) Geçersiz hizmet çağıran

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Get the SNTP Client local time without the 
   string message option. */

ULONG base_seconds;
ULONG base_fraction;

status =  nx_sntp_client_get_local_time(&demo_client, 
                                       &base_seconds, 
                                       &base_fraction, 
                                       NX_NULL);
/* If status is NX_SUCCESS an SNTP Client time was successfully
   retrieved.  */

```

## <a name="nx_sntp_client_get_local_time_extended"></a>nx_sntp_client_get_local_time_extended

Genişletilmiş SNTP İstemcisi yerel saatlerini al

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_get_local_time_extended(
                 NX_SNTP_CLIENT *client_ptr,
                 ULONG *seconds, 
                 ULONG *fraction, 
                 CHAR *buffer
                 UINT buffer_size);

```

### <a name="description"></a>Description

Bu hizmet, dize iletisi biçimindeki verileri almak için bir seçenek arabellek işaretçisi girişi ile genişletilmiş SNTP İstemcisi yerel saat alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP İstemcisi denetim bloğu işaretçisi

- **saniye** Yerel saat saniye işaretçisi

- **kesir** Kesir bileşeni işaretçisi

- **buffer (arabellek)** Yazma zamanı verilerini arabelleğe alma işaretçisi

- **buffer_size** Arabellek uzunluğu

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı İstemci oluşturma

- NX_PTR_ERROR (0x07) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) Geçersiz hizmet çağıran

- NX_SIZE_ERROR (0x09) Başarısız buffer_size denetleme

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Get the SNTP Client local time without the 
   string message option. */

#define BUFSIZE 50

ULONG seconds;
ULONG fraction;
CHAR  buffer[BUFSIZE];

status =  nx_sntp_client_get_local_time_extended(&demo_client, 
                                                &seconds, 
                                                &fraction, 
                                                buffer, 
                                                BUFSIZE);

/* If status is NX_SUCCESS an SNTP Client 
   time was successfully retrieved.  */

```

## <a name="nx_sntp_client_initialize_broadcast"></a>nx_sntp_client_initialize_broadcast

Yayın işlemi için İstemciyi başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_initialize_broadcast(NX_SNTP_CLIENT *client_ptr,
                                    ULONG multicast_server_address, 
                                    ULONG broadcast_time_servers);


```

### <a name="description"></a>Description

Bu hizmet, SNTP sunucu IP adresini ayarlayarak ve SNTP başlangıç parametrelerini ve zaman aşımlarını başlatarak, yayın için Istemciyi başlatır. Hem çok noktaya yayın hem de yayın adresleri null değilse, çok noktaya yayın adresi seçilir. Her iki adres null ise bir hata döndürülür. Bu, yalnızca IPv4 sunucu adreslerini destekler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi

- **multicast_server_address** SNTP çok noktaya yayın adresi

- **broadcast_time_server** SNTP sunucusu yayın adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Istemci oluşturma başarılı

- **NX_INVALID_PARAMETERS** (0x4D) geçersiz işaretçi girişi

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Initialize the client for broadcast operation.  */
status =  nx_sntp_client_initialize_broadcast(client_ptr,0x0,
                            NX_NULL, IP_ADDRESS(192,2,2,255);

/* If status is NX_SUCCESS the Client 
   was successfully initialized.  */

```

## <a name="nxd_sntp_client_initialize_broadcast"></a>nxd_sntp_client_initialize_broadcast

IPv4 veya IPv6 yayın işlemi için Istemciyi başlatma

### <a name="prototype"></a>Prototype

```C
UINT nxd_sntp_client_initialize_broadcast(NX_SNTP_CLIENT *client_ptr,
                            NXD_ADDRESS *multicast_server_address, 
                            NXD_ADDRESS *broadcast_server_address);

```

### <a name="description"></a>Description

Bu hizmet, SNTP sunucu IP adresini ayarlayıp SNTP başlangıç parametrelerini ve zaman aşımlarını başlatarak yayın için Istemciyi başlatır. Hem yayın hem çok noktaya yayın adres işaretçileri null değilse, çok noktaya yayın adresi seçilir. Her iki adres işaretçisi de null ise bir hata döndürülür. Bu, hem IPv4 hem de IPv6 adres türlerini destekler. IPv6 yayını desteklemez, bu nedenle yayın adresi işaretçisi IPv6 olarak ayarlanır, bir hata döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi

- **multicast_server_address** SNTP sunucu çok noktaya yayın adresi

- **broadcast_server_address** SNTP sunucusu yayın adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla başlatıldı

- NX_SNTP_PARAM_ERROR (0xD0D) geçersiz işaretçi girişi

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı


### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Initialize the client for broadcast operation.  */
NXD_ADDRESS broadcast_server;

Broadcast_server.nxd_ip_address = NX_IP_VERSION_V6;
Broadcast_server.nxd_ip_address.v6[0] = 0x20010db1;
Broadcast_server.nxd_ip_address.v6[1] = 0x0f101;
Broadcast_server.nxd_ip_address.v6[2] = 0x0;
Broadcast_server.nxd_ip_address.v6[3] = 0x101;

status =  nxd_sntp_client_initialize_broadcast(client_ptr,0x0,
                                  NX_NULL, &broadcast_server)


/* If status is NX_SUCCESS the Client 
   was successfully initialized.  */

```

## <a name="nx_sntp_client_initialize_unicast"></a>nx_sntp_client_initialize_unicast

Tek noktaya yayın içinde çalışacak SNTP Istemcisini ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                        ULONG unicast_time_server);

```
### <a name="description"></a>Description

Bu hizmet, SNTP sunucu IP adresini ayarlayarak ve SNTP başlangıç parametrelerini ve zaman aşımlarını başlatarak tek noktaya yayın işlemi için Istemciyi başlatır. Bu, yalnızca IPv4 sunucu adreslerini destekler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi

- **unicast_time_server** SNTP sunucu IP adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla başlatıldı

- NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Initialize the Client for unicast operation.  */
status =  nx_sntp_client_initialize_unicast(&client_ptr, 
                                 IP_ADDRESS(192,2,2,1));


/* If status is NX_SUCCESS the Client 
   is initialized for unicast operation.  */

```


## <a name="nxd_sntp_client_initialize_unicast"></a>nxd_sntp_client_initialize_unicast

SNTP Istemcisini IPv4 veya IPv6 tek noktaya yayın içinde çalışacak şekilde ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nxd_sntp_client_initialize_unicast(NX_SNTP_CLIENT * client_ptr, 
                                  NXD_ADDRESS *unicast_time_server);

```

### <a name="description"></a>Description

Bu hizmet, SNTP sunucu IP adresini ayarlayıp SNTP başlangıç parametrelerini ve zaman aşımlarını başlatarak tek noktaya yayın işlemi için Istemciyi başlatır. Bu, hem IPv4 hem de IPv6 adres türlerini destekler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi

- **unicast_time_server** SNTP sunucu IP adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla başlatıldı

- NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Initialize the Client for unicast operation.  */
NXD_ADDRESS unicast_server;

unicast _server.nxd_ip_address = NX_IP_VERSION_V6;
unicast _server.nxd_ip_address.v6[0] = 0x20010db1;
unicast _server.nxd_ip_address.v6[1] = 0x0f101;
unicast _server.nxd_ip_address.v6[2] = 0x0;
unicast _server.nxd_ip_address.v6[3] = 0x101;

status =  nxd_sntp_client_initialize_unicast(&client_ptr, 
                                        *unicast_server); 


/* If status is NX_SUCCESS the Client 
   is initialized for unicast operation.  */

```

## <a name="nx_sntp_client_receiving_updates"></a>nx_sntp_client_receiving_updates

Istemcinin geçerli güncelleştirmeleri aldığını belirtin

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_receiving_updates(NX_SNTP_CLIENT *client_ptr, 
                                           UINT *receive_status);

```

### <a name="description"></a>Description

Bu hizmet, Istemcinin geçerli SNTP güncelleştirmelerini alıp almadığını gösterir. En uzun süre geçerli bir güncelleştirme olmadan veya birbirini izleyen geçersiz güncelleştirmeler için sınır aşıldıysa, alma durumu false olarak döndürülür. SNTP Istemcisinin hala çalıştığını ve uygulamanın başka bir tek noktaya yayın veya yayın/çok noktaya yayın sunucusu ile SNTP Istemcisini yeniden başlatmasını isterse *nx_sntp_client_stop* HIZMETINI kullanarak SNTP istemcisini durdurması gerekir, başka bir sunucu ile başlatma hizmetlerinden birini kullanarak istemciyi yeniden başlatın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi.

- **receive_status** Istemci geçerli güncelleştirmeleri alıyorsa, gösterge işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci güncelleştirme durumunu başarıyla aldı

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```C
/* Determine if the SNTP Client is receiving valid udpates.  */
UINT receive_status;

status =  nx_sntp_client_receiving_updates(client_ptr, 
                                     &receive_status);

/* If status is NX_SUCCESS and receive_status is NX_TRUE, 
   the client is currently receiving valid updates.  */

```

## <a name="nx_sntp_client_request_unicast_time"></a>nx_sntp_client_request_unicast_time

Doğrudan NTP sunucusuna bir tek noktaya yayın isteği gönderin


### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_request_unicast_time(NX_SNTP_CLIENT *client_ptr, 
                                                  UINT wait_option);
```

### <a name="description"></a>Description

Bu hizmet, uygulamanın bir tek noktaya yayın isteğini, SNTP Istemci iş parçacığı görevinin zaman uyumsuz olarak NTP sunucusuna doğrudan göndermesini sağlar. Bekle seçeneği, yanıt için ne kadar bekleneceğini belirtir. Başarılı olursa, uygulama, en son saati elde etmek için diğer SNTP Istemci hizmetlerini kullanabilir. Daha fazla ayrıntı için bkz. **SNTP zaman uyumsuz tek noktaya yayın istekleri** .

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi.

- **Wait_option** Zamanlayıcı Tick 'ındaki NTP yanıtı için bekleme seçeneği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci tek noktaya yayın güncelleştirmesini başarıyla gönderiyor ve alıyor

- **NX_SNTP_CLIENT_NOT_STARTED** (0xd0b) istemci iş parçacığı başlatılmadı

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Determine if the SNTP Client is receiving valid udpates.  */
UINT receive_status;

status =  nx_sntp_client_request_unicast_time(client_ptr, 400);

/* If status is NX_SUCCESS and receive_status is NX_TRUE, 
   the client is received a valid response to the unicast request.  */

```

## <a name="nx_sntp_client_run_broadcast"></a>nx_sntp_client_run_broadcast

Istemciyi yayın modunda çalıştır

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_run_broadcast(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, Istemci, SNTP sunucusundan yayınlar almak için bekleyeceği, yayın modunda başlatılır. Geçerli bir, SNTP iletisi alınmışsa, bir güncelleştirme olmadan maksimum lapken için SNTP istemci zaman aşımı ve alınan birbirini izleyen geçersiz iletilerin sayısı sıfırlanır. Bu limitlerden herhangi biri aşılırsa, SNTP Istemcisi sunucu durumunu geçersiz olarak ayarlar, ancak yine de güncelleştirmeleri almaya bekleyecek. Uygulama, sunucu durumu için SNTP Istemci görevini yoklayabiliyor ve geçersiz SNTP Istemcisini durdurup başka bir SNTP yayın adresiyle yeniden başlatın. Ayrıca tek noktaya yayın SNTP sunucusuna geçiş yapabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **durum** --------fiili tamamlanma durumu

- **NX_SNTP_CLIENT_ALREADY_STARTED** (0xd0c) istemcisi zaten başlatılmış

- **NX_SNTP_CLIENT_NOT_INITIALIZED** (0xd01) istemci başlatılmadı

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start Client running in broadcast mode.  */
status =  nx_sntp_client_run_broadcast(client_ptr);

/* If status is NX_SUCCESS, the client is successfully started.  */

```

## <a name="nx_sntp_client_run_unicast"></a>nx_sntp_client_run_unicast

Istemciyi tek noktaya yayın modunda çalıştırma

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_run_unicast(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, Istemciyi bir zaman güncelleştirmesi için düzenli olarak SNTP sunucusuna bir tek noktaya yayın isteği gönderdiği tek noktaya yayın modunda başlatır. Geçerli bir SNTP iletisi alınmışsa, güncelleştirme olmadan maksimum lapken için SNTP istemci zaman aşımı, ilk yoklama aralığı ve alınan ardışık geçersiz ileti sayısı sıfırlanır. Bu limitlerden herhangi biri aşılırsa, SNTP Istemcisi sunucu durumunu geçersiz olarak ayarlar, ancak yine de yoklama yapar ve güncelleştirmeleri almaya bekler. Uygulama, sunucu durumu için SNTP Istemci görevini yoklayabiliyor ve geçersiz SNTP Istemcisini durdurup başka bir SNTP tek noktaya yayın adresiyle yeniden başlatın. Ayrıca, bir yayın SNTP sunucusuna geçiş yapabilir.

.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci tek noktaya yayın modunda başarıyla başlatıldı

- **NX_SNTP_CLIENT_ALREADY_STARTED** (0xd0c) istemcisi zaten başlatılmış

- **NX_SNTP_CLIENT_NOT_INITIALIZED** (0xd01) istemci başlatılmadı

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı


### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start the Client in unicast mode. */
status =  nx_sntp_client_run_unicast(client_ptr);

/* If status = NX_SUCCESS, the Client was successfully started.  */

```

## <a name="nx_sntp_client_set_local_time"></a>nx_sntp_client_set_local_time

SNTP Istemci yerel saatini ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_set_local_time(NX_SNTP_CLIENT *client_ptr , 
                                ULONG seconds, ULONG fraction);

```

### <a name="description"></a>Description

Bu hizmet, SNTP Istemci yerel saati ' ni, değer olarak ondalık biçimde (örneğin, saniye ve ' kesir '), onaltılı biçimde bir saniyede yerleştirmek için biçim olan SNTP biçiminde ayarlar. Gerçek zamanlı bir zaman ile (örn. gerçek zamanlı olarak) SNTP Istemci yerel saati 'nin güncelleştirilmesi amaçlanmıştır. SNTP protokolü, yerel saat zamanını ' dritaslağı ' üzerinden tutmak için SNTP zaman güncelleştirmelerine yöneliktir. SNTP sunucu saati güncelleştirmeleri olabilir, ancak uygulama cihazında bağımsız bir zaman Man yoksa, SNTP Istemci yerel saatine tek giriş olarak atanmamıştır.

Bu API, SNTP istemci iş parçacığını başlatmadan önce SNTP Istemcisine temel bir zaman vermek için de kullanılabilir. SNTP Istemci yerel saati, geçerli saat verileri için alınan güncelleştirmelerle karşılaştırılır. İlk kez güncelleştirme alındığında çok büyük bir tutarsızlık olabilir. Bu nedenle, SNTP Istemcisinin ilk güncelleştirmedeki tutarsızlığı yoksaymasına yönelik bir seçenek vardır. Bu şekilde, SNTP Istemcisi temel saat olmadan başlayabilir. Giriş saati, bilinen dönem sürelerinden elde edilebilir (genellikle Internet 'te kullanılabilir) ve 1 Ocak 1900 ' den itibaren geçen saniye sayısı (yeni bir ' dönem ' başlatıldığında 2036 ' i) olarak hesaplanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi

- **saniyeler** Süre girişinin saniye bileşeni

- **kesir** SNTP kesir biçimindeki alt saniyeler bileşeni

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) yerel saati başarıyla ayarla

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Başlatma

### <a name="example"></a>Örnek

```C
/* Set the SNTP Client local time. */
base_seconds =  0xd2c50b71;
base_fraction = 0xa132db1e;

status =  nx_sntp_client_set_local_time(&demo_client, 
                                        base_seconds, 
                                        base_fraction);

/* If status is NX_SUCCESS an SNTP Client time 
   was successfully set.  */

```

## <a name="nx_sntp_client_set_time_update_notify"></a>nx_sntp_client_set_time_update_notify

SNTP güncelleştirme geri aramasını ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_set_time_update_notify(NX_SNTP_CLIENT *client_ptr, 
                           VOID (time_update_cb)(NX_SNTP_TIME_MESSAGE 
                        *time_update_ptr, NX_SNTP_TIME *local_time)));

```

### <a name="description"></a>Description

Bu hizmet, SNTP Istemcisi geçerli bir saat güncelleştirmesi aldığında uygulamayı bilgilendirmek için geri çağırma işlemini ayarlar. Gerçek SNTP iletisini ve SNTP Istemcisinin yerel saatini (genellikle aynı) NTP biçiminde sağlar. Uygulama, NTP verilerini doğrudan kullanabilir veya *nx_sntp_client_utility_display_date_time hizmetini* arayarak zaman okunabilir biçime dönüştürebilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi

- **time_update_cb** Geri çağırma işlevine işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Başlatma

### <a name="example"></a>Örnek

```C
/* Set the SNTP Client time update callback. */
VOID client_time_update_notify(NX_SNTP_TIME_MESSAGE *time_update_ptr, 
                                           NX_SNTP_TIME *local time);

NX_SNTP_CLIENT demo_client;


status = nx_sntp_client_set_time_update_notify(&demo_client, 
                                            time_update_cb);

/* If status is NX_SUCCESS an SNTP Client 
   time update callback was successfully set.  */

```

## <a name="nx_sntp_client_stop"></a>nx_sntp_client_stop

SNTP Istemci iş parçacığını durdur

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_stop(NX_SNTP_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, SNTP Istemci iş parçacığını durduruyor. Sonsuz bir döngüde çalışan SNTP Istemci iş parçacığı görevleri, SNTP istemci durumunun denetimini serbest bırakma ve uygulamaların SNTP Istemcisinde API çağrıları yapmasına izin veren her yinelemede duraklatılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **client_ptr** SNTP Istemci denetim bloğu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı durdurulan istemci iş parçacığı

- **NX_SNTP_CLIENT_NOT_STARTED** (0xDB) SNTP istemci iş parçacığı başlatılmadı

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Stop the SNTP Client. */
status =  nx_sntp_client_stop(&demo_client);

/* If status is NX_SUCCESS an SNTP 
   Client instance was successfully stopped.  */

```

## <a name="nx_sntp_client_utility_display_date_time"></a>nx_sntp_client_utility_display_date_time

NTP Saat'i Tarih ve Saat dizesine dönüştürme

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_utility_display_date_time (NX_SNTP_CLIENT 
                      *client_ptr, CHAR *buffer, UINT length);

```

### <a name="description"></a>Description

Bu hizmet, SNTP İstemcisi yerel saatlerini yıl ay tarih biçimine dönüştürür ve sağlanan arabellekteki tarihi döndürür. NX_SNTP_CURRENT_YEAR, geçerli İstemci saati ile aynı yıl değil, tanımlanmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **SNTP İstemcisi client_ptr İşaretçisi**

- **buffer (arabellek)** Depolama tarihi için arabelleğe işaretçi

- **uzunluk** Giriş arabelleğinin boyutu

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı dönüştürme

- **NX_SNTP_ERROR_CONVERTING_DATETIME** (0xD08) NX_SNTP_CURRENT_YEAR veya hiçbir yerel istemci zamanı kurulmamış

- **NX_SNTP_INVALID_DATETIME_BUFFER** (0xD07) Yetersiz arabellek uzunluğu


### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Convert and display the Client’s local time. */

status =  nx_sntp_client_utility_display_date_time(client_ptr , 
                                        buffer, sizeof(buffer));

/* If status is NX_SUCCESS, 
   date was successfully written to buffer.  */

```

## <a name="nx_sntp_client_utility_msecs_to_fraction"></a>nx_sntp_client_utility_msecs_to_fraction

Milisaniyeyi NTP kesir bileşenine dönüştürme

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_utility_msecs_to_fraction (ULONG milliseconds,   
                                                 ULONG *fraction);

```

### <a name="description"></a>Description

Bu hizmet, girdi milisaniyesini NTP kesir bileşenine dönüştürür. SNTP İstemcisi için başlangıç temel süresi olan ancak NTP saniye/kesir biçiminde olmayan uygulamalarla kullanılmak üzere tasarlanmıştır. Geçerli bir kesir yapmak için milisaniye sayısı 1000'den az olmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dönüştürülecek milisaniye milisaniye**

- **kesir** Milisaniye işaretçisi kesir olarak dönüştürülür

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı dönüştürme

- **NX_SNTP_OVERFLOW_ERROR** (0xD32) Saati tarihe dönüştürme hatası

- NX_SNTP_INVALID_TIME (0xD30) Geçersiz SNTP veri girişi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Convert the milliseconds to a fraction. */


status =  nx_sntp_client_utility_msecs_to_fraction(milliseconds, 
                                                     &fraction);

/* If status is NX_SUCCESS, 
   data was successfully converted.  */

```

## <a name="nx_sntp_client_utility_usecs_to_fraction"></a>nx_sntp_client_utility_usecs_to_fraction

Mikro saniyeleri NTP kesir bileşenine dönüştürme

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_utility_usecs_to_fraction (ULONG microseconds,   
                                                 ULONG *fraction);

```
### <a name="description"></a>Description

Bu hizmet, giriş mikro saniyesini NTP kesir bileşenine dönüştürür. SNTP İstemcisi için başlangıç temel süresi olan ancak NTP saniye/kesir biçiminde olmayan uygulamalarla kullanılmak üzere tasarlanmıştır. Geçerli bir kesir yapmak için mikro saniye sayısı 10000000'den az olmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **microseconds** Dönüştürülecek mikrosaniye

- **kesir** Mikrosaniye işaretçisi kesir olarak dönüştürülür

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı dönüştürme

- **NX_SNTP_OVERFLOW_ERROR** (0xD32) Saati tarihe dönüştürme hatası

- NX_SNTP_INVALID_TIME (0xD30) Geçersiz SNTP veri girişi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Convert the microseconds to a fraction. */


status =  nx_sntp_client_utility_msecs_to_fraction(microseconds, 
                                                     &fraction);

/* If status is NX_SUCCESS, data was successfully converted.  */

```

## <a name="nx_sntp_client_utility_fraction_to_usecs"></a>nx_sntp_client_utility_fraction_to_usecs

NTP kesir bileşenini mikrosaniyeye dönüştürme

### <a name="prototype"></a>Prototype

```C
UINT nx_sntp_client_utility_fraction_to_usecs (ULONG fraction,   
                                         ULONG *microseconds);

```

### <a name="description"></a>Description

Bu hizmet, giriş NTP kesir bileşenini mikrosaniyeye dönüştürür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dönüştürülecek kesir kesir**

- **microseconds** Mikrosaniyeye dönüştürülen kesir işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı dönüştürme

- NX_SNTP_INVALID_TIME (0xD30) Geçersiz SNTP veri girişi

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Convert the fraction to microseconds. */


status =  nx_sntp_client_utility_fraction_to_msecs(fraction, 
                                             &microseconds);

/* If status is NX_SUCCESS, data was successfully converted.  */
```