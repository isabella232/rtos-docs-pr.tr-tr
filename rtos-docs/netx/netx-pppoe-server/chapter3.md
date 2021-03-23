---
title: Bölüm 3-Azure RTOS NetX PPPoE sunucu hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX PPPoE sunucu hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d1137fae4dfea428d50e2defed94de6a838b01c6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826602"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-server-services"></a>Bölüm 3-Azure RTOS NetX PPPoE sunucu hizmetlerinin açıklaması

Bu bölüm, tüm Azure RTOS NetX PPPoE sunucu hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_pppoe_server_create**: *bir PPPoE sunucu örneği oluşturma*

- **nx_pppoe_server_ac_name_set**: *erişim yoğunlaştırıcı adını ayarla*

- **nx_pppoe_server_delete**: *bir PPPoE sunucu örneğini silme*

- **nx_pppoe_server_enable**: *PPPoE sunucu hizmetlerini etkinleştirme*

- **nx_pppoe_server_disable**: *PPPoE sunucu hizmetlerini devre dışı bırak*

- **nx_pppoe_server_callback_notify_set**: *PPPoE sunucusu geri çağırma bildirim işlevlerini ayarla*

- **nx_pppoe_server_service_name_set**: *PPPoE sunucu hizmeti adını ayarla*

- **nx_pppoe_server_session_send**: *PPPoE sunucu verilerini belirtilen oturuma gönder*

- **nx_pppoe_server_session_packet_send**: *PPPoE sunucu paketini belirtilen oturuma gönder*

- **nx_pppoe_server_session_terminate**: *belirtilen PPPoE oturumunu Sonlandır*

- **nx_pppoe_server_session_get**: *belirtilen oturum bilgilerini al*

## <a name="nx_pppoe_server_create"></a>nx_pppoe_server_create

Bir PPPoE sunucu örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_create(NX_PPPOE_SERVER *pppoe_server_ptr,
                            CHAR *name, NX_IP *ip_ptr,
                            UINT interface_index,
                            VOID (*pppoe_link_driver)
                            (struct NX_IP_DRIVER_STRUCT *)
                            NX_PACKET_POOL *pool_ptr,
                            VOID *stack_ptr, ULONG stack_size,
                            UINT priority);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen NetX IP örneği için Kullanıcı tarafından sağlanan bağlantı sürücüsüyle bir PPPoE sunucu örneği oluşturur. Bağlantı sürücüsü başlatılmamış ve etkin değilse, PPPoE sunucu yazılımı bağlantı sürücüsünü başlatmaktan sorumludur.

Ayrıca, uygulamanın, iç paket ayırma için kullanması için, PPPoE sunucu örneği için önceden oluşturulmuş bir paket havuzu sağlaması gerekir.

Genellikle NetX IP iş parçacığını, PPPoE sunucu iş parçacığı önceliğinden daha yüksek bir önceliğe göre oluşturmak iyi bir fikir olduğunu unutmayın. IP iş parçacığı önceliğini belirtme hakkında daha fazla bilgi için lütfen *nx_ip_create* hizmetine bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.
- **ad**: Bu PPPoE sunucu örneğinin adı.
- **ip_ptr**: IP örneği için denetim bloğuna yönelik işaretçi.
- **interface_index**: arabirim dizini.
- **pppoe_link_driver**: Kullanıcı tarafından sağlanan bağlantı sürücüsü.
- **pool_ptr**: paket havuzuna yönelik işaretçi.
- **stack_ptr**: PPPoE sunucu iş parçacığının yığın alanının başlangıcı işaretçisi.
- **stack_size**: iş parçacığının yığınında bayt cinsinden boyut.
- **Öncelik**: Iç PPPoE sunucu iş parçacıklarının önceliği (1-31).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı bir PPPoE sunucu oluştur.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucusu, IP, paket havuzu veya yığın işaretçisi.
- NX_PPPOE_SERVER_INVALID_INTERFACE: (0xC2) geçersiz arabirim.
- NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) paket havuzunun yük boyutu geçersiz.
- NX_PPPOE_SERVER_MEMORY_SIZE_ERROR: (0xC4) geçersiz bellek boyutu.
- NX_PPPOE_SERVER_PRIORITY_ERROR: (0xC5) PPPoE sunucu iş parçacığının geçersiz önceliği.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create "my_pppoe_server" for IP instance "my_ip". */
status = nx_pppoe_server_create(&my_pppoe_server, "my PPPoE Server", &my_ip,
                                &my_pool, stack_start, 1024, 2);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully created. */
```

## <a name="nx_pppoe_server_delete"></a>nx_pppoe_server_delete

Bir PPPoE sunucu örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_delete(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş olan PPPoE sunucu örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_delete(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully deleted. */
```

## <a name="nx_pppoe_server_enable"></a>nx_pppoe_server_enable

PPPoE sunucu hizmetini etkinleştir

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_enable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, PPPoE sunucu hizmetlerini sunar.

> [!NOTE]
> Bu işlev, *nx_pppoe_server_create* ve *nx_pppoe_server_callback_notify_set* sonra çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Enable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_enable(&my_pppoe_server);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has enabled. */
```

## <a name="nx_pppoe_server_disable"></a>nx_pppoe_server_disable

PPPoE sunucu hizmetini devre dışı bırak

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_disable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, PPPoE sunucu hizmetlerini devre dışı bırakır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Disable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_disable(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has disabled. */
```

## <a name="nx_pppoe_server_callback_notify_set"></a>nx_pppoe_server_callback_notify_set

PPPoE sunucusu geri çağırma bildirim işlevlerini ayarla 

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_callback_notify_set(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        VOID (* pppoe_discover_initiation_notify)(UINT session_index,
                ULONG length, UCHAR *data),
        VOID (* pppoe_discover_request_notify)(UINT session_index),
        VOID (* pppoe_discover_terminate_notify)(UINT session_index),
        VOID (* pppoe_discover_terminate_confirm)(UINT session_index),
        VOID (* pppoe_data_receive_notify)(UINT session_index,
                ULONG length, UCHAR *data, UINT packet_id),
        VOID (* pppoe_discover_notify)(UINT session_index, UCHAR *data))
```

### <a name="description"></a>Açıklama

Bu hizmet, PPPoE sunucu geri çağırma bildirim işlevlerini ayarlar.

> [!NOTE]
> Bu işlev nx_pppoe_server_enabl önce çağrılmalıdır *ve* pppoe_data_receive_notify işlev işaretçisinin ayarlanması gerekir, aksi takdirde *nx_pppoe_server_enable* hata olur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.
- **pppoe_discover_initiation_notify**: her PPPoE bulma başlatma iletisi alındığında çağrılan uygulama işlevi. Bu değer NULL ise, başlatma geri çağırma işlevini bul seçeneği devre dışı bırakılır.
- **pppoe_discover_request_notify**: PPPoE bulma isteği iletisi alındığında çağrılan uygulama işlevi. Bu değer NULL ise, bulma isteği geri çağırma işlevi devre dışı bırakılır.
- **pppoe_discover_terminate_notify**: PPPoE bulma sonlandırma iletisi alındığında çağrılan uygulama işlevi. Bu değer NULL ise, bulma Sonlandır geri aramayı bul işlevi devre dışı bırakılır.
- **pppoe_discover_terminate_confirm**: PPPoE her sonlandırma iletisi gönderildiğinde çağrılan uygulama işlevi. Bu değer NULL ise, bulma Sonlandır geri aramayı bul işlevi devre dışı bırakılır.
- **pppoe_data_receive_notify**: PPPoE veri iletisi alındığında çağrılan uygulama işlevi. Bu değer sıfır olmamalıdır.
- **pppoe_data_send_notify**: PPPoE veri iletisi gönderildiğinde çağrılan uygulama işlevi. Bu değer NULL ise, veri geri arama gönder işlevi devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi veya işlev işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set PPPoE Server callback notify functions, PPPoE Server instance "my_pppoe_server". */

status = nx_pppoe_server_disable(&my_pppoe_server,
                pppoe_discovery_initiation_notify,
                pppoe_discovery_request_notify,
                pppoe_discovery_terminate_notify,
                pppoe_discovery_terminate_confirm,
                pppoe_data_receive_notify,
                pppoe_data_send_notify);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the callback notify functions for "my_pppoe_server" service has set. */
```

## <a name="nx_pppoe_server_ac_name_set"></a>nx_pppoe_server_ac_name_set

Erişim yoğunlaştırıcı adını ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_ac_name_set(
    NX_PPPOE_SERVER *pppoe_server_ptr,
    CHAR *ac_name, UINT ac_name_length,
);
```

### <a name="description"></a>Açıklama

Bu işlev, erişim yoğunlaştırıcı adı işlev çağrısını ayarladı.

> [!NOTE]
> Ac_name dizesi NULL sonlandırılmış olmalı ve ac_name uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşiyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.
- **ac_name**: erişim yoğunlaştırıcı adı.
- **ac_name_length**: ac_ame uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı bir PPPoE sunucu kümesi.
- **NX_PPPOE_SERVER_PTR_ERROR**: (0xC1) geçersiz PPPoE sunucusu, IP, paket havuzu veya yığın işaretçisi.
- **NX_SIZE_ERROR**: (0x09) denetim name_length başarısız oldu.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Set "my PPPoE ac name" for Server instance "my_pppoe_server". */
status = nx_pppoe_server_ac_name_set(&my_pppoe_server, "my PPPoE ac name",16);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my PPPoE ac name" was successfully set. */
```

## <a name="nx_pppoe_server_service_name_set"></a>nx_pppoe_server_service_name_set

PPPoE sunucu hizmeti adını ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_service_name_set(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UCHAR **service_name, UINT service_name_count);
```

### <a name="description"></a>Açıklama

Bu hizmet, PPPoE sunucu hizmeti adını ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
CHAR *nx_pppoe_service_name[] =
{
    "XBB",
    "PRINTER",
    NX_NULL
};

/* Set service name for PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_service_namet_set(&my_pppoe_server,
                                    nx_pppoe_service_name, 2);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service name has set. */
```

## <a name="nx_pppoe_server_session_send"></a>nx_pppoe_server_session_send

PPPoE sunucu verilerini belirtilen oturuma gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_session_send (NX_PPPOE_SERVER *pppoe_server_ptr,
                UINT session_index, UCHAR *data_ptr, UINT data_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen oturum KIMLIĞINI kullanarak PPPoE çerçevesini gönderir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.
- **session_index**: oturumun dizini.
- **data_ptr**: PPPoE sunucu veri çerçevesinin başlangıcı işaretçisi.
- **data_length**: PPPoE sunucu veri çerçevesinin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.
- NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE sunucu hizmeti etkin değil.
- NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) geçersiz PPPoE oturum dizini.
- NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE oturumu kurulmadı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Send PPPoE Server data to specified session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_send(&my_pppoe_server, 0, my_data_ptr, 1400);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" data has sent. */
```

## <a name="nx_pppoe_server_session_packet_send"></a>nx_pppoe_server_session_packet_send

PPPoE sunucu paketini belirtilen oturuma gönder

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_session_packet_send (
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UINT session_index, NX_PACKET *packet_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen oturum KIMLIĞINI kullanarak PPPoE paketi gönderir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.
- **session_index**: oturumun dizini.
- **packet_ptr**: PPPoE paketine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.
- NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) geçersiz PPPoE sunucu paketi.
- NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE sunucu hizmeti etkin değil.
- NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) geçersiz PPPoE oturum dizini.
- NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE oturumu kurulmadı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Send PPPoE Server data to specified session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_packet_send(&my_pppoe_server, 0, packet_ptr);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" packet has sent. */
```

## <a name="nx_pppoe_server_session_terminate"></a>nx_pppoe_server_session_terminate

Belirtilen PPPoE oturumunu Sonlandır

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_session_terminate(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UINT session_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen PPPoE oturumunu sonlandırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.
- **session_index**: oturumun dizini.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.
- NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE sunucu hizmeti etkin değil.
- NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) geçersiz PPPoE oturum dizini.
- NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE oturumu kurulmadı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Terminates the specified PPPoE session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_send(&my_pppoe_server, 0);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the session indexed with 0 has terminated. */
```

## <a name="nx_pppoe_server_session_get"></a>nx_pppoe_server_session_get

Belirtilen PPPoE oturum bilgilerini al

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_session_get(NX_PPPOE_SERVER *pppoe_server_ptr,
                                UINT session_index
                                ULONG *client_mac_msw,
                                ULONG *client_mac_lsw,
                                ULONG *session_id);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen PPPoE oturum bilgilerini, istemci fiziksel adresini ve oturum kimliğini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.
- **session_index**: oturumun dizini.
- **client_mac_msw**: istemci fiziksel adresi MSW işaretçisi.
- **client_mac_lsw**: istemci fiziksel adresi MSW işaretçisi.
- **session_id**: oturum kimliği işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.
- NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) geçersiz PPPoE oturum dizini.
- NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE oturumu kurulmadı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Gets the specified PPPoE session information, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_get (&my_pppoe_server, 0, &client_mac_msw, &client_mac_lsw, &session_id);

/* If status is NX_PPPOE_SERVER_SUCCESS, the client physical address and session id of the session indexed with 0 has got. */
```

## <a name="pppinitind"></a>PppInitInd

Varsayılan hizmet adını yapılandırın

### <a name="prototype"></a>Prototype

```c
VOID PppInitnd(UINT length, UCHAR *aData);
```

### <a name="description"></a>Açıklama

Bu işlevin, TTP 'nin, PPPoE 'nin gelen PADI isteklerini filtrelemek için kullanması gereken ' varsayılan hizmet adı ' öğesini yapılandırmasına izin vermek için bu işlevi kullanıma sunacaktır. PPPoE yazılımı bu bilgileri unutmalıdır ve eşleşen bir hizmet adı içeren bir PADI paketi alınmışsa PppDiscoverReq öğesini çağırmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **uzunluk**: varsayılan hizmet adının uzunluğu.
- **ADATA**: varsayılan hizmet adı.

### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Configure the default Service Name. */
PppInitInd (3, "XBB");
```

## <a name="pppdiscovercnf"></a>PppDiscoverCnf

PADO paketinin hizmet adı alanını tanımlayın

### <a name="prototype"></a>Prototype

```c
VOID PppDiscoverCnf (UINT length, UCHAR *aData, UINT interfaceHandle);
```

### <a name="description"></a>Açıklama

PPPoE yazılımı, TTP yazılımının PADO paketinin hizmet adı alanını tanımlamasına izin vermek için bu işlevi kullanıma sunar. PppDiscoverCnf çağrıldığında, PPPoE yazılımı PADO 'yi göndermemelidir.

PADO paketi, PPPoE yazılımının başlatılabilir bölümünde tanımlanan bir erişim yoğunlaştırıcısı adı (RFC2516 ' de tanımlanan # 2 etiket kimliği kullanılarak) içerir.

Her ad null olarak sonlandırıldığından, aData içinde birden çok hizmet adı geçirilebilir.

Diğer komutların hizmet adının bir parçası olarak geçirilmesi gereken durumlarda, en yüksek esnekliği sağlamak için null karakter kullanılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **uzunluk**: varsayılan hizmet adının uzunluğu.
- **ADATA**: varsayılan hizmet adı.
- **ınterfacehandle**: arabirim tanıtıcısı.

### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Define the Service Name field of the PADO packet. */
PppDiscoverCnf (3, "XBB", 0);
```

## <a name="pppopencnf"></a>PppOpenCnf

PPPoE oturumunu kabul etme veya reddetme

### <a name="prototype"></a>Prototype

```c
VOID PppOpenCnf (UCHAR accept, UINT interfaceHandle);
```

### <a name="description"></a>Açıklama

PPPoE yazılımı, TTP 'nin yazılım PPPoE oturumunu kabul etmesine veya reddetmesine izin vermek için bu işlevi kullanıma sunar.  Buna yanıt olarak, PPPoE yığını bağlantıyı kabul etmeli ve ınterfacehandle ile ilişkili benzersiz bir PPPoE Session_ID numarası atamalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **kabul et**: bağlantının kabul edileceği NX_TRUE.
- **ınterfacehandle**: arabirim tanıtıcısı.

### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Accept the connection. */
PppOpenCnf(NX_TRUE, 0);
```

## <a name="pppcloseind"></a>PppCloseInd

Bir PPPoE oturumunu kapatma

### <a name="prototype"></a>Prototype

```c
VOID PppCloseInd (UINT interfaceHandle, UCHAR *causeCode);
```

### <a name="description"></a>Açıklama

Bu işlev, TTP 'nin yazılımının bir PPPoE oturumunu kapatmasını sağlamak için bu işlevi açığa çıkarır.

PPPoE yazılımı, TıT iletisindeki Generic-Error etiketinde neden kod dizesinin (0x0203) olduğunu gösterir

### <a name="input-parameters"></a>Giriş Parametreleri

- **ınterfacehandle**: arabirim tanıtıcısı.
- **Causecode**: PPPoE sunucusundan bağlantı kapatma nedeni hakkında bilgi göndermek için null sonlandırılmış dize.

### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Close a PPPoE session. */
PppCloseInd(0, NX_NULL);
```

## <a name="pppclosecnf"></a>PppCloseCnf

Tanıtıcının serbest bırakılmış olduğunu onaylayın

### <a name="prototype"></a>Prototype

```c
VOID PppCloseCnf (UINT interfaceHandle);
```

### <a name="description"></a>Açıklama

PPPoE yazılımı, bu işlevi, TTP 'nin yazılımın, tanıtıcının serbest bırakılmış olduğunu onaylamasını sağlamak için kullanıma sunar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ınterfacehandle**: arabirim tanıtıcısı.

### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Confirm that the handle has been freed. */
PppCloseCnf(0);
```

## <a name="ppptransmitdatacnf"></a>PppTransmitDataCnf

Önceki PPP verilerinin onaylaneklenmesine izin ver

### <a name="prototype"></a>Prototype

```c
VOID PppTransmitDataCnf (UINT interfaceHandle, UCHAR *aData,
                        UINT packet_id);
```

### <a name="description"></a>Açıklama

PPPoE yazılımı, önceki bir PppTransmitDataReq 'ın onaylanmasına izin vermek için bu işlevi kullanıma sunacaktır.  Bu, TTP 'nin, PPPoE 'den yeni bir PPP çerçevesi için hazırlandığını gösterir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **ınterfacehandle**: arabirim tanıtıcısı.
- **ADATA**: işaretçi kabul edilen PPP veri arabelleğinin işaretçisi.
- **Packet_id**: paket tanımlayıcısı.

### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
UINT packet_id = 0x20015429

/* Allow a preceding PPP data to be acknowledged, let PPPoE Server release the packet with same packet identifier. */
PppTransmitDataCnf(0, NX_NULL, packet_id);
```

## <a name="pppreceivedataind"></a>PppReceiveDataInd

Ethernet üzerinden aktarımdan veri al

### <a name="prototype"></a>Prototype

```c
VOID PppReceiveDataInd(UINT interfaceHandle, UINT length, UCHAR *aData);
```

### <a name="description"></a>Açıklama

PPPoE yazılımı, Ethernet üzerinden iletilmek üzere veri almak için bu işlevi kullanıma sunacaktır

### <a name="input-parameters"></a>Giriş Parametreleri

- **ınterfacehandle**: arabirim tanıtıcısı.
- **uzunluk**: ADATA 'daki bayt sayısı.
- **ADATA**: PPP verilerinin çerçevesini içeren veri arabelleği.

### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Receive data from transmission over Ethernet, data start pointer is aData.
The number of bytes in aData is 1480. */
PppReceiveDataInd (0, 1480, aData);
```