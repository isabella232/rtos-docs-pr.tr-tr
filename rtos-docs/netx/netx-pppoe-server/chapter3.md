---
title: Bölüm 3 - NetX PPPoE Azure RTOS Hizmetlerinin Açıklaması
description: Bu bölümde, Tüm NetX PPPoE Azure RTOS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d184fc3c5e6ed74ef25045561b1613e280672f77385fbb13b8e84bccf051b301
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782821"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-server-services"></a>Bölüm 3 - NetX PPPoE Azure RTOS Hizmetlerinin Açıklaması

Bu bölümde, Tüm NetX PPPoE Azure RTOS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_pppoe_server_create:** *PPPoE Sunucusu örneği oluşturma*

- **nx_pppoe_server_ac_name_set:** Access *Concentrator adını ayarlama*

- **nx_pppoe_server_delete:** *PPPoE Sunucusu örneğini silme*

- **nx_pppoe_server_enable:** *PPPoE Sunucusu hizmetlerini etkinleştirme*

- **nx_pppoe_server_disable:** *PPPoE Sunucusu hizmetlerini devre dışı bırakma*

- **nx_pppoe_server_callback_notify_set:** *PPPoE Sunucusu geri çağırma bildirimi işlevlerini ayarlama*

- **nx_pppoe_server_service_name_set:** *PPPoE Sunucusu hizmet adını ayarlayın*

- **nx_pppoe_server_session_send:** *PPPoE Sunucusu verilerini belirtilen oturuma gönderme*

- **nx_pppoe_server_session_packet_send:** *PPPoE Sunucusu paketini belirtilen oturuma gönderme*

- **nx_pppoe_server_session_terminate:** Belirtilen *PPPoE oturumunu sonlandırma*

- **nx_pppoe_server_session_get:** Belirtilen *oturum bilgilerini al*

## <a name="nx_pppoe_server_create"></a>nx_pppoe_server_create

PPPoE Sunucusu örneği oluşturma

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

### <a name="description"></a>Description

Bu hizmet, belirtilen NetX IP örneği için kullanıcı tarafından sağlanan bağlantı sürücüsü ile bir PPPoE Sunucusu örneği oluşturur. Bağlantı sürücüsü başlatılmamışsa ve etkinse, bağlantı sürücüsünü başlatmak PPPoE sever yazılımından sorumludur.

Ayrıca, uygulamanın iç paket ayırma için kullanmak üzere PPPoE Sunucusu örneği için önceden oluşturulmuş bir paket havuzu sağlamak gerekir.

NetX IP iş parçacığını PPPoE Sunucusu iş parçacığı önceliklerinden daha yüksek bir önceliğe sahip olarak oluşturmanın genel olarak iyi bir fikir olduğunu unutmayın. IP iş parçacığı *nx_ip_create* belirtme hakkında daha fazla bilgi için lütfen nx_ip_create hizmetine bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr:** PPPoE Sunucusu denetim bloğuna işaretçi.
- **name:** Bu PPPoE Sunucusu örneğinin adı.
- **ip_ptr:** IP örneği için denetim bloğu işaretçisi.
- **interface_index:** Arabirim dizini.
- **pppoe_link_driver:** Kullanıcı tarafından sağlanan bağlantı sürücüsü.
- **pool_ptr:** Paket havuzunun işaretçisi.
- **stack_ptr:** PPPoE Sunucusu iş parçacığının yığın alanı başlangıç işaretçisi.
- **stack_size:** İş parçacığı yığınında bayt cinsinden boyut.
- **öncelik:** İç PPPoE Sunucusu iş parçacıklarının önceliği (1-31).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Başarılı PPPoE Sunucusu oluşturma.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Geçersiz PPPoE Sunucusu, IP, paket havuzu veya yığın işaretçisi.
- NX_PPPOE_SERVER_INVALID_INTERFACE: (0xC2) Geçersiz arabirim.
- NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) Paket havuzunun yük boyutu geçersiz.
- NX_PPPOE_SERVER_MEMORY_SIZE_ERROR: (0xC4) Geçersiz bellek boyutu.
- NX_PPPOE_SERVER_PRIORITY_ERROR: (0xC5) PPPoE Sunucusu iş parçacığının geçersiz önceliği.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create "my_pppoe_server" for IP instance "my_ip". */
status = nx_pppoe_server_create(&my_pppoe_server, "my PPPoE Server", &my_ip,
                                &my_pool, stack_start, 1024, 2);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully created. */
```

## <a name="nx_pppoe_server_delete"></a>nx_pppoe_server_delete

PPPoE Sunucusu örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_delete(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş PPPoE Sunucusu örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr:** PPPoE Sunucusu denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Başarılı PPPoE Sunucusu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Geçersiz PPPoE Sunucusu işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_delete(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully deleted. */
```

## <a name="nx_pppoe_server_enable"></a>nx_pppoe_server_enable

PPPoE Sunucusu hizmetini etkinleştirme

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_enable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet PPPoE Sunucusu hizmetlerini sağlar.

> [!NOTE]
> Bu işlev, nx_pppoe_server_create *ve nx_pppoe_server_callback_notify_set.* 

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr:** PPPoE Sunucusu denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Başarılı PPPoE Sunucusu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Geçersiz PPPoE Sunucusu işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Enable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_enable(&my_pppoe_server);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has enabled. */
```

## <a name="nx_pppoe_server_disable"></a>nx_pppoe_server_disable

PPPoE Sunucusu hizmetini devre dışı bırakma

### <a name="prototype"></a>Prototype

```c
UINT nx_pppoe_server_disable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a>Description

Bu hizmet PPPoE Sunucusu hizmetlerini devre dışı bırakıyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr:** PPPoE Sunucusu denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_PPPOE_SERVER_SUCCESS:**(0x00) Başarılı PPPoE Sunucusu silme.
- NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Geçersiz PPPoE Sunucusu işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Disable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_disable(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has disabled. */
```

## <a name="nx_pppoe_server_callback_notify_set"></a>nx_pppoe_server_callback_notify_set

PPPoE Sunucusu geri çağırma bildirimi işlevlerini ayarlama 

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

### <a name="description"></a>Description

Bu hizmet PPPoE Sunucusu geri çağırma bildirimi işlevlerini ayarlar.

> [!NOTE]
> Bu işlev, nx_pppoe_server_enabl  çağrılmadan önce çağrılır ve pppoe_data_receive_notify işlev işaretçisi *ayarlanmazsa* nx_pppoe_server_enable hata olur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **pppoe_server_ptr:** PPPoE Sunucusu denetim bloğuna işaretçi.
- **pppoe_discover_initiation_notify:** PPPoE bulma başlatan ileti her alınsa çağrılır uygulama işlevi. Bu değer NULL ise, başlatılabilir geri çağırma işlevinin devre dışı bırakılmıştır.
- **pppoe_discover_request_notify:** PPPoE bulma isteği iletisi her alınarak çağrılmış uygulama işlevi. Bu değer NULL ise, istek geri çağırma işlevinin devre dışı bırakılmıştır.
- **pppoe_discover_terminate_notify:** PPPoE discover terminate iletisi her alındında çağrılır uygulama işlevi. Bu değer NULL ise, terminate callback işlevinin devre dışı bırakılmıştır.
- **pppoe_discover_terminate_confirm:** PPPoE discover terminate iletisi her gönderildiği zaman çağrılır. Bu değer NULL ise, bulma Sonlandır geri aramayı bul işlevi devre dışı bırakılır.
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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

Ethernet üzerinden iletimden veri alma

### <a name="prototype"></a>Prototype

```c
VOID PppReceiveDataInd(UINT interfaceHandle, UINT length, UCHAR *aData);
```

### <a name="description"></a>Description

PPPoE yazılımı, Ethernet üzerinden iletim için veri almak için bu işlevi ortaya çıkarır

### <a name="input-parameters"></a>Giriş Parametreleri

- **interfaceHandle:** Arabirim tanıtıcısı.
- **length:** aData'daki bayt sayısı.
- **aData:** PPP veri çerçevesini içeren veri arabelleği.

### <a name="return-values"></a>Dönüş Değerleri

**Hiçbiri**

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Receive data from transmission over Ethernet, data start pointer is aData.
The number of bytes in aData is 1480. */
PppReceiveDataInd (0, 1480, aData);
```