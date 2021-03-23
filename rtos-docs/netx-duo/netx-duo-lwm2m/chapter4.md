---
title: Bölüm 4-LWM2M ISTEMCI hizmetlerinin açıklaması
description: Bu bölüm, tüm LWM2M Istemci hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 825a215ba756b39b6d76e6cc773c288e8b8aab01
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825930"
---
# <a name="chapter-4--description-of-lwm2m-client-services"></a>Bölüm 4 LWM2M ISTEMCI hizmetlerinin açıklaması

Bu bölüm, aşağıda listelenen tüm LWM2M Istemci hizmetlerinin alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan  **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

**LWM2M Istemci yönetimi:**

- nx_lwm2m_client_create: *Lwm2m Istemcisi oluşturma*

- nx_lwm2m_client_delete: *Lwm2m Istemcisini Sil*

- nx_lwm2m_client_lock: *Lwm2m Istemcisini kilitle*

- nx_lwm2m_client_unlock: *Lwm2m Istemcisinin kilidini aç*

**LWM2M Istemci oturumu yönetimi:**

- nx_lwm2m_client_session_create: *Lwm2m Istemci oturumu oluştur*

- nx_lwm2m_client_session_delete: *Lwm2m Istemci oturumunu Sil*

- nx_lwm2m_client_session_bootstrap: *bir önyükleme sunucusu ile oturum başlatma*

- nx_lwm2m_client_session_bootstrap_dtls: *bir önyükleme sunucusu ile güvenli bir oturum başlatma*

- nx_lwm2m_client_session_register_info_get: *Lwm2m Server kayıt bilgilerini al*

- nx_lwm2m_client_session_register: *Lwm2m sunucusu ile oturum başlatma*

- nx_lwm2m_client_session_register_dtls: *Lwm2m sunucusu ile güvenli bir oturum başlatma*

- nx_lwm2m_client_session_update: *bir oturumu Lwm2m sunucusuyla güncelleştirme*

- nx_lwm2m_client_session_deregister: bir *oturumu Lwm2m sunucusu Ile sonlandırma*

- nx_lwm2m_client_session_error_get: *bir oturumun son hatasını al*

**Cihaz nesnesi uygulama:**

- nx_lwm2m_client_device_callbacks_set: *cihaz nesnesi uygulama geri çağırmaları ayarla*

- nx_lwm2m_client_device_error_push: *cihaz nesnesine hata kodu ekleyin*

- nx_lwm2m_client_device_error_reset: *cihaz nesnesinin hata kodlarını sıfırlayın*

- nx_lwm2m_client_device_resource_changed: *cihaz nesne kaynağının sinyal değişikliği*

**Üretici yazılımı güncelleştirme nesne uygulama:**

- nx_lwm2m_firmware_create: *bellenim güncelleştirme nesnesi oluştur*

- nx_lwm2m_firmware_package_info_set: *bellenim güncelleştirme paketi bilgilerini ayarla*

- nx_lwm2m_firmware_result_set: *bellenim güncelleştirme sonucunu ayarla*

- nx_lwm2m_firmware_state_set: *bellenim güncelleştirme durumunu ayarla*

**Özel nesne uygulamaları:**

- nx_lwm2m_client_object_add: *Lwm2m Istemcisine nesne uygulamasını ekleme*

- nx_lwm2m_client_object_remove: *Lwm2m Istemcisinden nesne uygulamasını kaldırma*

- nx_lwm2m_client_object_instance_add: *Lwm2m Istemcisine nesne örneği ekleme*

- nx_lwm2m_client_object_instance_remove: *nesne ÖRNEĞINI Lwm2m Istemcisinden kaldır*

- nx_lwm2m_object_resource_changed: bir *nesne örneğinin kaynak değeri Için sinyal değişikliği*

**Yerel cihaz yönetimi**

- nx_lwm2m_client_object_create: *Yeni bir nesne örneği oluştur*

- nx_lwm2m_client_object_delete: *bir nesne örneğini silme*

- nx_lwm2m_client_object_discover: *bir nesne örneğinin kaynaklarını bulma*

- nx_lwm2m_client_object_execute: *bir nesne örneğinin kaynağını yürütün*

- nx_lwm2m_client_object_next_get: *Lwm2m istemcisi tarafından uygulanan nesne listesini al*

- nx_lwm2m_client_object_instance_next_get: *bir nesnenin örneklerinin listesini al*

- nx_lwm2m_client_object_read: *bir nesne örneğinin kaynak değerlerini oku*

- nx_lwm2m_client_object_write: *bir nesne örneğinin kaynak değerlerini değiştirme*

**Kaynak bilgileri ve değerler ayarı:**

- nx_lwm2m_client_resource_info_set: *kaynak bilgilerini ayarlama*

- nx_lwm2m_client_resource_string_set: *kaynak değerini dize olarak ayarla*

- nx_lwm2m_client_resource_integer32_set: *kaynak değerini 32-bit tamsayı olarak ayarlayın*

- nx_lwm2m_client_resource_integer64_set: *kaynak değerini 64-bit tamsayı olarak ayarlayın*

- nx_lwm2m_client_resource_float32_set: *kaynak değerini 32-bit float olarak ayarlayın*

- nx_lwm2m_client_resource_float64_set: *kaynak değerini 64-bit float olarak ayarlayın*

- nx_lwm2m_client_resource_boolean_set: *kaynak değerini Boole olarak ayarlayın*

- nx_lwm2m_client_resource_objlnk_set: *kaynak değerini nesne bağlantısı olarak ayarla*

- nx_lwm2m_client_resource_opaque_set: *kaynak değerini donuk olarak ayarlayın*

- nx_lwm2m_client_resource_instance_set: *birden çok kaynak için kaynak değerini örnek olarak ayarla*
-
- nx_lwm2m_client_resource_dim_set: *birden çok kaynak için kaynak boyutunu ayarlayın.*

**Kaynak bilgileri ve değerleri alma:**

- nx_lwm2m_client_resource_info_get: *kaynak bilgilerini al*

- nx_lwm2m_client_resource_string_get: *bir dize kaynağının değerini Al*

- nx_lwm2m_client_resource_integer32_get: *32 bitlik bir tamsayı kaynağının değerini Al*

- nx_lwm2m_client_resource_integer64_get: *64 bitlik bir tamsayı kaynağının değerini Al*

- nx_lwm2m_client_resource_float32_get: *32 bitlik bir kayan kaynağın değerini alın*

- nx_lwm2m_client_resource_float64_get: *64 bitlik bir kayan kaynağın değerini alın*

- nx_lwm2m_client_resource_boolean_get: *bir Boole kaynağının değerini Al*

- nx_lwm2m_client_resource_objlnk_get: *nesne bağlantı kaynağının değerini Al*

- nx_lwm2m_client_resource_opaque_get: *donuk bir kaynağın değerini Al*

- nx_lwm2m_client_resource_instance_get: *birden çok kaynak için kaynak örneğini al*

- nx_lwm2m_client_resource_dim_get: *birden çok kaynak için kaynak boyutunu alın.*

## <a name="nx_lwm2m_client_create"></a>nx_lwm2m_client_create

Bir LWM2M istemcisi oluşturur.

### <a name="prototype"></a>Prototype

```C
UINT nx_lwm2m_client_create(
    NX_LWM2M_CLIENT client_ptr,
    NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    const CHAR *name_ptr,
    UINT name_length,
    const CHAR *msisdn_ptr,
    UINT msisdn_length,
    UCHAR binding_modes,
    VOID *stack_ptr,
    ULONG stack_size,
    UINT priority);
```

### <a name="description"></a>Açıklama

Bu hizmet kendi ThreadX iş parçacığı bağlamında çalışan bir LWM2M Istemci örneği oluşturur.

LWM2M Istemcisi şu OMA LWM2M nesnelerini uygular: güvenlik (0), sunucu (1), Access Control (2) ve cihaz (3). Diğer nesneler uygulamaları, uygulama tarafından eklenmelidir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **packet_pool_ptr** Bu LWM2M Istemcisi için varsayılan paket havuzuna yönelik işaretçi.
- **name_ptr** LWM2M Istemci uç noktası adı işaretçisi.
- **name_length** LWM2M Istemci uç noktası adının uzunluğu.
- **msisdn_ptr** SMS bağlaması ile kullanım için LWM2M Istemcisine ulaşılabileceği MSıSDN işaretçisine, SMS bağlama desteklenmiyorsa NULL olabilir.
- **msisdn_length** MSıSDN numarası uzunluğu.
- **binding_modes** LWM2M Istemcisi tarafından desteklenen bağlama ve modlar, NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S ve NX_LWM2M_BINDING_SQ bayraklarının bir birleşimi olmalıdır.
- **stack_ptr** LWM2M Istemci iş parçacığı yığın alanı işaretçisi.
- **stack_size** LWM2M Istemci iş parçacığı yığın boyutu.
- **Öncelik** LWM2M Istemcisinin önceliği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** LWM2M Istemcisi başarıyla oluşturuldu.
- **NX_LWM2M_CLIENT_ERROR** LWM2M Istemcisi oluşturma hatası.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.
- **NX_PTR_ERROR** Geçersiz işaretçi.
- **NX_SIZE_ERROR** Geçersiz yığın boyutu.
- **NX_OPTION_ERROR** Geçersiz öncelik.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```C
/* Create LWM2M Client instance.  */
status = nx_lwm2m_client_create(&lwm2m_client, &ip_0, &pool_0, 
  "netxlwm2mclient", sizeof("netxlwm2mclient") - 1,           
                                NX_NULL, 0, NX_LWM2M_CLIENT_BINDING_U, 
                                stack_ptr, stack_size, priority);

/* If status is NX_SUCCESS a LWM2M Client instance was successfully created.  */
```

## <a name="nx_lwm2m_client_delete"></a>nx_lwm2m_client_delete

Bir LWM2M Istemcisini siler.

### <a name="prototype"></a>Prototype

```C
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş bir LWM2M Istemci örneğini siler.

O anda istemcinin bağlı olduğu tüm oturumlar bu çağrı tarafından da silinir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** LWM2M Istemcisi başarıyla silindi.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Delete the LWM2M Client instance.  */
status = nx_lwm2m_client_create(&lwm2m_client);

/* If status is NX_SUCCESS a LWM2M Client instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_device_callback_set"></a>nx_lwm2m_client_device_callback_set

Bir cihaz nesnesinin uygulama geri aramasını ayarlar.

### <a name="prototype"></a>Prototype

```C
UINT **nx_lwm2m_client_device_callback_set**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_OPERATION_CALLBACK operation_callback);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisi tarafından işlenmeyen LWM2M cihaz nesnesi kaynaklarına işlem uygulamak için uygulama geri aramasını kurar.

LWM2M Istemcisi şu kaynakları uygular: hata kodu (11), sıfırlama hata kodu (12) ve desteklenen bağlama ve modlar (16), diğer kaynaklara yönelik işlemler uygulamaya yeniden yönlendirilir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **operation_callback** "Oku", "Keşfet", "Write" ve "Execute" için işlem geri çağırması.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem geri çağırması başarıyla ayarlandı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set device callback.  */
status = nx_lwm2m_client_device_callback_set(&lwm2m_client, device_operation);

/* If status is NX_SUCCESS a device callback was successfully set.  */
```

## <a name="nx_lwm2m_client_device_error_push"></a>nx_lwm2m_client_device_error_push
Bir cihaz nesnesine bir hata kodu ekler.

### <a name="prototype"></a>Prototype

```C
UINT **nx_lwm2m_client_device_error_push**(
    NX_LWM2M_CLIENT *client_ptr,
    UCHAR code);
```

### <a name="description"></a>Açıklama

Bu hizmet, nesne cihazının hata kodu (11) kaynağına yeni bir örnek ekler.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **kod** Yeni hata kodu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL**

En fazla depolanan hata kodu sayısı

ulaşıldı.

Geçersiz NX_PTR_ERROR işaretçisi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```C
/* Push device error 1 (Low battery power) to server.  */
status = nx_lwm2m_client_device_error_push(&lwm2m_client, 1);

/* If status is NX_SUCCESS a device error was successfully pushed.  */
```

## <a name="nx_lwm2m_client_device_error_reset"></a>nx_lwm2m_client_device_error_reset

Cihaz nesnesinin hata kodlarını sıfırlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, tüm hata kodu kaynak örneklerini cihaz nesnesinden siler. Bu, kaynak sıfırlama hata kodunu (12) çalıştırmaya eşdeğerdir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Delete all device error code.  */
status = nx_lwm2m_client_device_error_reset(&lwm2m_client);

/* If status is NX_SUCCESS, reset device error successfully.  */
```

## <a name="nx_lwm2m_client_device_resource_changed"></a>nx_lwm2m_client_device_resource_changed

Bir cihaz nesne kaynağında değişikliğe işaret eder.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_resource_changed(
    NX_LWM2M_CLIENT *client_ptr, 
    const NX_LWM2M_RESOURCE *resource);

```

### <a name="description"></a>Açıklama

Hizmet, uygulama tarafından, nesne cihazının bir kaynağının değiştiği LWM2M Istemcisine işaret etmek için kullanılır. LWM2M Istemcisi, kaynak bir LWM2M sunucusu tarafından gözlemleniyorsa bir bildirim gönderir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **kaynak** Değiştirilen kaynağı açıklayan yapıya yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Change device resource.  */
status = nx_lwm2m_client_device_resource_changed(&lwm2m_client, &resource);

/* If status is NX_SUCCESS, a device resource was successfully changed.  */
```

##  <a name="nx_lwm2m_client_firmware_create"></a>nx_lwm2m_client_firmware_create

LWM2M Istemci üretici yazılımı nesnesi oluşturun. 

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_firmware_create(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    NX_LWM2M_CLIENT *client_ptr, 
    UINT protocols,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_URI_CALLBACK update_callback);
```

### <a name="description"></a>Açıklama

Hizmet, uygulama tarafından bellenim nesnesi oluşturmak için kullanılır.

### <a name="parameters"></a>Parametreler

- **firmware_ptr** LWM2M Istemci üretici yazılımı nesnesi işaretçisi.
- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **protokoller** Desteklenen protokoller.
- **package_callback** Paket geri çağırması.
- **package_uri_callback** Paket URI geri çağırması.
- **update_callback** Güncelleştirme geri çağırması.

### <a name="return-values"></a>Dönüş Değerleri

**NX_SUCCESS** İşlem başarılı.
**NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Create firmware object.  */
status = nx_lwm2m_client_firmware_create(&firmware, &lwm2m_client,     
                                         NX_LWM2M_CLIENT_FIRMWARE_PROTOCOL_HTTP, 
                                         NX_NULL, firmware_packet_uri,
                                         firmware_update);

/* If status is NX_SUCCESS, firmware object was successfully created.  */
```

##  <a name="nx_lwm2m_client_firmware_package_info_set"></a>nx_lwm2m_client_firmware_package_info_set

LWM2M Istemci üretici yazılımı paket bilgilerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_firmware_package_info_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    const CHAR *name, 
    UINT name_length, 
    const CHAR *version, 
    UINT version_length);
```

### <a name="description"></a>Açıklama

Hizmet, uygulama tarafından bellenim güncelleştirme nesnesinin paket bilgi kaynaklarını ayarlamak için kullanılır.

### <a name="parameters"></a>Parametreler

- **firmware_ptr** LWM2M Istemci üretici yazılımı nesnesi işaretçisi.
- **ad** Üretici yazılımı paketinin adı.
- **name_length** Ad uzunluğu.
- **sürümü** Üretici yazılımı paketinin sürümü.
- **version_length** Sürüm uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the package information resources of the firmware object.  */
status = nx_lwm2m_client_firmware_package_info_set(&firmware, 2m_client,     
                                    “LWM2M Firmware”, sizeof(“LWM2M Firmware”) -1,
                                    “1.0.0.0”, sizeof(“1.0.0.0”) - 1);

/* If status is NX_SUCCESS, package information resources was successfully set. */
```

##  <a name="nx_lwm2m_client_firmware_result_set"></a>nx_lwm2m_client_firmware_result_set

Bellenim güncelleştirme nesnesinin güncelleştirme sonucu kaynağını ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_firmware_result_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a>Açıklama

Hizmet, uygulama tarafından bellenim güncelleştirme nesnesinin güncelleştirme sonucu kaynağını ayarlamak için kullanılır.

### <a name="parameters"></a>Parametreler

- **firmware_ptr** LWM2M Istemci üretici yazılımı nesnesi işaretçisi.
- **sonuç** Güncelleştirme sonucu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the update result resource of the firmware object.  */
status = nx_lwm2m_client_firmware_result_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_RESULT_SUCCESS);

/* If status is NX_SUCCESS, the update result resource was successfully set.  */
```

##  <a name="nx_lwm2m_client_firmware_state_set"></a>nx_lwm2m_client_firmware_state_set

Bellenim güncelleştirme nesnesinin güncelleştirme sonucu kaynağını ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_firmware_state_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a>Açıklama

Hizmet, uygulama tarafından bellenim güncelleştirme nesnesinin durumunu ayarlamak için kullanılır.

### <a name="parameters"></a>Parametreler

- **firmware_ptr** LWM2M Istemci üretici yazılımı nesnesi işaretçisi.
- **durum** Bellenim nesnesinin durumu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the state of the firmware object.  */
status = nx_lwm2m_client_firmware_state_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_STATE_IDLE);

/* If status is NX_SUCCESS, the state was successfully set.  */
```

## <a name="nx_lwm2m_client_lock"></a>nx_lwm2m_client_lock

LWM2M Istemcisini kilitler.

### <a name="prototype"></a>Prototype

```c
UINT **nx_lwm2m_client_lock**(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M nesnelerine sunuculardan veya başka bir uygulama iş parçacığından eş zamanlı erişimi engellemek için LWM2M Istemcisini kilitler.

LWM2M Istemcisi Şu anda başka bir iş parçacığı tarafından kilitliyse, LWM2M Istemcisinin kilidi açana kadar işlev engellenir.

***Nx_lwm2m_client_lock** _/_ *_nx_lwm2m_client_unlock_** çiftlerine yapılan çağrılar iç içe olabilir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Lock the LWM2M client.  */
status = nx_lwm2m_client_lock(&lwm2m_client);

/* If status is NX_SUCCESS, lwm2m client was successfully locked.  */
```

## <a name="nx_lwm2m_client_object_add"></a>nx_lwm2m_client_object_add

LWM2M Istemcisine bir nesne uygulamasını ekler.

### <a name="prototype"></a>Prototype

```c
UINT **nx_lwm2m_client_object_add**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_CLIENT_OBJECT_OPERATION_CALLBACK object_operation);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisine yeni bir nesne uygulamasını ekler.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_ptr** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.
- **object_id** Nesne kimliği.
- **object_operation** Nesne işlemi geri çağırma işlevi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne KIMLIĞI zaten var.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Add new object to the lwm2m client.  */
status = nx_lwm2m_client_object_add(&lwm2m_client, &object, 
                                    3303, object_operation);

/* If status is NX_SUCCESS, the new object was successfully added.  */
```

## <a name="nx_lwm2m_client_object_create"></a>nx_lwm2m_client_object_create

Yeni bir nesne örneği oluşturur.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_create(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID *instance_id_ptr,
    UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, yeni bir nesne örneği oluşturmak için LWM2M Istemcisinin bir nesnesi üzerinde bir ' Create ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_id** Nesne KIMLIĞI.
- **instance_id_ptr** LWM2M Istemcisinin bir örnek KIMLIĞI ataması gerekiyorsa, yeni örneğin KIMLIĞINE yönelik işaretçi **null** olabilir. KIMLIK ayrılmış 65535 ise, LWM2M Istemcisi bir örnek KIMLIĞI atayacaktır. NULL değilse, çağrının ardından atanan KIMLIK döndürülür.
- **num_values** Ayarlanacak değer sayısı.
- **values_ptr** Yeni nesne örneğini başlatmak için kaynak değerleri dizisine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne örneği KIMLIĞI zaten var.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Nesne, örnek oluşturmayı desteklemiyor.
- **NX_LWM2M_CLIENT_NO_MEMORY** Yeni örneği depolamak için bellek ayrılamıyor.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Create new object instance.  */
status = nx_lwm2m_client_object_create(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, a new object instance was successfully created.  */
```

## <a name="nx_lwm2m_client_object_delete"></a>nx_lwm2m_client_object_delete

Bir nesne örneğini siler.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_delete(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin nesne örneği üzerinde bir ' DELETE ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_id** Nesne KIMLIĞI.
- **instance_id** Nesne örneği KIMLIĞI.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Nesne, örnek silmeyi desteklemiyor.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI veya nesne örneği KIMLIĞI yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Delete an object instance.  */
status = nx_lwm2m_client_object_delete(&lwm2m_client, 3303, 0);

/* If status is NX_SUCCESS, an object instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_object_discover"></a>nx_lwm2m_client_object_discover

Bir nesne örneğinin kaynaklarını bulur.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_discover(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT *num_resources,
    NX_LWM2M_CLIENT_RESOURCE *resources);

```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde bir ' bul ' işlemi gerçekleştirir, bu, nesne tarafından uygulanan kaynakların listesini döndürür.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_id** Nesne KIMLIĞI.
- **instance_id** Nesne örneği KIMLIĞI.
- **num_resources** Hedef arabelleğin boyutunu girişte, arabelleğe yazılan öğelerin sayısı çıktı olarak.
- **kaynaklar** Hedef arabelleğin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- Başarılı bir işlem *NX_SUCCESS*.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Kaynak ara belleği, kaynak listesini depolamak için çok küçük.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI veya nesne örneği KIMLIĞI yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
NX_LWM2M_CLIENT_RESOURCE resources[10]
UINT num_resources = 10;

/* Discover object resources.  */
status = nx_lwm2m_client_object_discover(&lwm2m_client, 3303, 0, 
                                         &num_resources, resource);

/* If status is NX_SUCCESS, discover object resources successfully.  */
```

## <a name="nx_lwm2m_client_object_execute"></a>nx_lwm2m_client_object_execute

Bir nesne örneğinin kaynağında ' Execute ' işlemi gerçekleştirir.

### <a name="prototype"></a>Prototype

```C
UINT **nx_lwm2m_client_object_execute**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr,
    UINT arguments_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin nesne örneği kaynağında ' Execute ' işlemini gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_id** Nesne KIMLIĞI.
- **instance_id** Nesne örneği KIMLIĞI.
- **resource_id** Kaynak KIMLIĞI.
- **arguments_ptr** Yürütme işleminin bağımsız değişkenlerine yönelik işaretçi. Arguments_length sıfırsa NULL olabilir.
- **arguments_length** Bağımsız değişkenlerin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Kaynak ara belleği, kaynak listesini depolamak için çok küçük.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI veya nesne örneği KIMLIĞI yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Execute object resource.  */
status = nx_lwm2m_client_object_execute (&lwm2m_client, 3303, 0, 0,  
                                         “5”, 1);

/* If status is NX_SUCCESS, an object resource was successfully executed.  */
```

## <a name="nx_lwm2m_client_object_instance_add"></a>nx_lwm2m_client_object_instance_add

Nesnesine bir nesne örneği uygulama ekler.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_instance_add(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisine yeni bir nesne örneği uygulamasını ekler. İnstance_id_ptr değeri **NX_LWM2M_CLIENT_RESERVED_ID**, LWM2M Client kullanılmamış bir örnek kimliğini otomatik olarak atayacaktır, aksi takdırde, LWM2M istemcisi uygulama kümesi değer kullanacaktır. Yeni örnek başarıyla eklendikten sonra, instance_id uygulamaya geri dönmek için instance_id_ptr doldurulur.

### <a name="parameters"></a>Parametreler

- **object_ptr** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.
- **instance_ptr** Nesne örneği uygulamasını tanımlayan yapıya yönelik işaretçi.
- **instance_id_ptr** Nesne örneği kimliğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_CLIENT_LWM2M_ALREADY_EXIST** Nesne KIMLIĞI zaten var.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Add new object instance to the object.  */
status = nx_lwm2m_client_object_instance_add(&object, &object_instance,
                                             &instance_id);

/* If status is NX_SUCCESS, the new object instance was successfully added.  */
```

## <a name="nx_lwm2m_client_object_instance_next_get"></a>nx_lwm2m_client_object_instance_next_get

Bir nesnenin sonraki örneğini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_instance_next_get(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen nesnenin sonraki nesne örneğinin KIMLIĞINI döndürür. Geçerli örnek KIMLIĞI NX_LWM2M_RESERVED_ID olarak ayarlandıysa (65535) ilk Örneğin KIMLIĞI döndürülür.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_id** Nesne KIMLIĞI.
- **instance_id_ptr** Geçerli nesne örneği KIMLIĞINE yönelik işaretçi. Dönüş sırasında nesnenin sonraki örnek KIMLIĞINI içerir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_CLIENT_LWM2M_NOT_FOUND** Verilen örnek KIMLIĞI nesnenin son, veya nesne KIMLIĞI uygulanmadı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the next instance of an object.  */
status = nx_lwm2m_client_object_instance_next_get(&lwm2m_client, 3303, 
                                                  &instance_id);

/* If status is NX_SUCCESS, get the next instance successfully.  */
```

## <a name="nx_lwm2m_client_object_instance_remove"></a>nx_lwm2m_client_object_instance_remove

Nesne örneği uygulamasını nesnesinden kaldırır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_instance_remove(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir nesneden nesne örneğini kaldırır.

### <a name="parameters"></a>Parametreler

- ***object_ptr*** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.
- **instance_ptr** Nesne örneği uygulamasını tanımlayan yapıya yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne KIMLIĞI zaten var.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Remove object instance from an object.  */
status = nx_lwm2m_client_object_instance_remove(&object, &object_instance);

/* If status is NX_SUCCESS, the object instance was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_next_get"></a>nx_lwm2m_client_object_next_get

LWM2M Istemcisinin bir sonraki nesnesini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_next_get(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID \*object_id_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisi tarafından uygulanan bir sonraki nesnenin KIMLIĞINI döndürür. Geçerli nesne KIMLIĞI NX_LWM2M_RESERVED_ID olarak ayarlandıysa (65535) ilk nesne KIMLIĞI döndürülür.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_id_ptr** Geçerli nesne KIMLIĞINE yönelik işaretçi. Dönüşte, LWM2M Istemcisi tarafından uygulanan bir sonraki nesne KIMLIĞINI içerir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_NOT_FOUND** Verilen nesne KIMLIĞI, veritabanının son nesnesidir.
**NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the next object of lwm2m client.  */
status = nx_lwm2m_client_object_next_get(&lwm2m_client, &object_id);

/* If status is NX_SUCCESS, get the next object successfully.  */
```

## <a name="nx_lwm2m_client_object_read"></a>nx_lwm2m_client_object_read

Bir nesne örneğinin resourcevalues değerlerini okur.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_read(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT num_values,
    NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde ' Read ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_id** Nesne KIMLIĞI.
- **instance_id** Nesne örneği KIMLIĞI.
- **num_values** Okunacak kaynak sayısı.
- **values_ptr** Okunacak kaynakların kimliklerini içeren NX_LWM2M_RESOURCE dizisine yönelik işaretçi. Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Bir kaynak okuma işlemini desteklemiyor.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI, nesne örneği KIMLIĞI veya kaynak KIMLIĞI yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Read the object resources.  */
status = nx_lwm2m_client_object_read(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, the resources were successfully read.  */
```

## <a name="nx_lwm2m_client_object_remove"></a>nx_lwm2m_client_object_remove

Nesne örneği uygulamasını nesnesinden kaldırır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_remove(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir nesneyi LWM2M Istemcisinden kaldırır.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_ptr** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne KIMLIĞI zaten var.
- **NX_PTR_ERROR** Geçersiz işaretçi.
- **NX_LWM2M_CLIENT_FORBIDDEN** İç nesne kaldırılmaya izin verilmiyor.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Remove object from lwm2m client.  */
status = nx_lwm2m_client_object_remove(&lwm2m_client, &object);

/* If status is NX_SUCCESS, the object was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_resource_changed"></a>nx_lwm2m_client_object_resource_changed

Bir nesne kaynağının değişikliğine işaret eder.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_resource_changed(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Açıklama

Hizmet, uygulama tarafından nesne kaynağının değiştiği LWM2M Istemcisine işaret etmek için kullanılır. LWM2M Istemcisi, kaynak bir LWM2M sunucusu tarafından gözlemleniyorsa bir bildirim gönderir.

### <a name="parameters"></a>Parametreler

- **object_ptr** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.
- ***instance_ptr*** Nesne örneği uygulamasını tanımlayan yapıya yönelik işaretçi.
- **kaynak** Değiştirilen kaynağı açıklayan yapıya yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Change object resource.  */
status = nx_lwm2m_client_object_resource_changed(&object, &instance, &resource);

/* If status is NX_SUCCESS, a resource was successfully changed.  */
```

## <a name="nx_lwm2m_client_object_write"></a>nx_lwm2m_client_object_write

Kaynak bir nesne örneğinin değerlerini değiştirir.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_write(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr,
    UINT write_op);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde ' Write ' işlemi gerçekleştirir.

*Write_op* parametresine aşağıdaki yazma işlemleri de belirtilebilir.

| Değer | Yazma &nbsp; işlemi | Açıklama |
| --- | ---| --- |
| 0 | Kısmi güncelleştirme | Yeni değerde belirtilen kaynakları ekler veya güncelleştirir ve diğer mevcut kaynakları değişmeden bırakır. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE** | Örneği Değiştir | Nesne örneğini, belirtilen yeni kaynak değerleriyle değiştirir. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE** | Kaynağı değiştir | Kaynakları, belirtilen yeni kaynak değerleriyle (birden çok kaynağı değiştirmek için kullanılır) değiştirir. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP** | Önyükleme yazma | Bir önyükleme dizisinin çağrısını gösterir. |

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.
- **object_id** Nesne KIMLIĞI.
- **instance_id** Nesne örneği KIMLIĞI.
- **num_values** Yazılacak kaynak sayısı.
- **values_ptr** Kaynak kimliklerini, türleri ve yazılacak değerleri içeren bir NX_LWM2M_RESOURCE dizisine yönelik işaretçi.
- **write_op** Yazma işlemi türü.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak türü geçerli değil.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Değerin uzunluğu, örnekte depolanamayacak kadar büyük.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Kaynak, yazma işlemini desteklemez.
- **NX_LWM2M_CLIENT_NO_MEMORY** Kaynak değeri depolamak için bellek ayrılamıyor.
- **NX_LWM2M_CLIENT_NOT_ACCEPTABLE** Kaynağın değeri geçerli değil.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI, nesne örneği KIMLIĞI veya kaynak KIMLIĞI yok.
- **NX_OPTION_ERROR** Geçersiz yazma işlemi türü. 
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Write object resources.  */
status = nx_lwm2m_client_object_write(&lwm2m_client, 3303, 0, 2, &resource,
                                      NX_LWM2M_CLIENT_OBJECT_WRITE_UPDATE);

/* If status is NX_SUCCESS, write object resources successfully.  */
```

## <a name="nx_lwm2m_client_resource_boolean_get"></a>nx_lwm2m_client_resource_boolean_get

Boole kaynağının değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_boolean_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a>Açıklama

Hizmet bir Boole kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak değeri açıklaması işaretçisi.
- **bool_ptr** Hedef Boolean değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir Boole değeri değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of a Boolean resource.  */
status = nx_lwm2m_client_resource_boolean_get(&resource, &bool);

/* If status is NX_SUCCESS, the value of Boolean resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_boolean_set"></a>nx_lwm2m_client_resource_boolean_set

Boole kaynağının değerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_boolean_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_BOOL bool_data);
```

### <a name="description"></a>Açıklama

Hizmet bir Boole kaynağının değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **bool_data** Boole verileri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of a Boolean resource.  */
status = nx_lwm2m_client_resource_boolean_set(&resource, NX_TRUE);

/* If status is NX_SUCCESS, the value of Boolean resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_dim_get"></a>nx_lwm2m_client_resource_dim_get

Birden çok kaynak için kaynak boyutunu alır

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_dim_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    UCHAR *dim);
```

### <a name="description"></a>Açıklama

Hizmet, birden fazla kaynak için kaynak boyutunu alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- hedef boyutun **karartma** işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir Boole değeri değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the resource dimension for multiple resource.  */
status = nx_lwm2m_client_resource_dim_get(&resource, &dim);

/* If status is NX_SUCCESS, the resource dimension was successfully get. */
```

## <a name="nx_lwm2m_client_resource_dim_set"></a>nx_lwm2m_client_resource_dim_set

Birden çok kaynak için kaynak boyutunu ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_dim_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    CHAR dim);
```

### <a name="description"></a>Açıklama

Hizmet, birden fazla kaynak için kaynak boyutunu ayarlar.

### <a name="parameters"></a>Parametreler

- **değer** Kaynak değeri açıklaması işaretçisi.
- **Dim** boyut değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the resource dimension.  */
status = nx_lwm2m_client_resource_dim_set(&resource, 3);

/* If status is NX_SUCCESS, the resource dimension was successfully set. */
```

## <a name="nx_lwm2m_client_resource_float32_get"></a>nx_lwm2m_client_resource_float32_get

32 bitlik bir **float** kaynağının değerini alır

### <a name="prototype"></a>Prototype

```C
UINT nx_lwm2m_client_resource_float32_get(
    NX_LWM2M_CLIENT_RESOURCE *resource,
    NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, 32 bitlik bir **float** kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **float32_ptr** Hedef 32-bit **kayan** değer işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir Boole değeri değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```C
/* Get the value of a 32-Bit float resource.  */
status = nx_lwm2m_client_resource_float32_get(&resource, &float32);

/* If status is NX_SUCCESS, the value of 32-Bit float resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_float32_set"></a>nx_lwm2m_client_resource_float32_set

32 bitlik bir **float** kaynağının değerini ayarlar

### <a name="prototype"></a>Prototype

```C
UINT nx_lwm2m_client_resource_float32_set(
    NX_LWM2M_CLIENT_RESOURCE *resource,
    NX_LWM2M_FLOAT32 float32_data);
```

### <a name="description"></a>Açıklama

Hizmet, 32 bitlik bir **float** kaynağının değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **float32_data** 32 bit **kayan** verileri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of a 32-Bit float resource.  */
status = nx_lwm2m_client_resource_float32_set(&resource, 1.24);

/* If status is NX_SUCCESS, the value of 32-Bit float resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_float64_get"></a>nx_lwm2m_client_resource_float64_get

64 bitlik bir float kaynağının değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_float64_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, 64 bitlik bir **float** kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **float64_ptr** Hedef 64-bit **kayan** değer işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir float değeri değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of a 64-Bit float resource.  */
status = nx_lwm2m_client_resource_float64_get(&resource, &float64);

/* If status is NX_SUCCESS, the value of 64-Bit float resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_float64_set"></a>nx_lwm2m_client_resource_float64_set

64 bitlik bir **float** kaynağının değerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_float64_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_FLOAT64 float64_data);
```

### <a name="description"></a>Açıklama

Hizmet, 64 bitlik bir **float** kaynağının değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **float64_data** 64 bit **kayan** verileri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of a 64-Bit float resource.  */
status = nx_lwm2m_client_resource_float64_set(&resource, 1.24);

/* If status is NX_SUCCESS, the value of 64-Bit float resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_info_get"></a>nx_lwm2m_client_resource_info_get

Kaynak bilgisini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_info_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_ID *resource_id, 
    ULONG *operation);
```

### <a name="description"></a>Açıklama

Hizmet, kaynağın kaynak bilgilerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **resource_id** Hedef kaynak KIMLIĞI işaretçisi.
- **işlem** Hedef kaynak işlemine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the resource information.  */
status = nx_lwm2m_client_resource_info_get(&resource, &resource_id, &operation);

/* If status is NX_SUCCESS, the resource information was successfully get. */
```

## <a name="nx_lwm2m_client_resource_info_set"></a>nx_lwm2m_client_resource_info_set

Kaynak bilgilerini ayarlar.

### <a name="prototype"></a>Prototype

```C
UINT nx_lwm2m_client_resource_info_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    NX_LWM2M_FLOAT64 float64_data);
```

### <a name="description"></a>Açıklama

Hizmet, kaynak bilgilerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **resource_id** Kaynağın KIMLIĞI.
- **işlem** Kaynağın işlemi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the resource information.  */
status = nx_lwm2m_client_resource_info_set(&resource, 0, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);

/* If status is NX_SUCCESS, the resource information was successfully set. */
```

## <a name="nx_lwm2m_client_resource_instances_get"></a>nx_lwm2m_client_resource_instances_get

Birden çok kaynağın örneğini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_instances_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_CLIENT_RESOURCE *resource_instances, 
    UINT *count);
```

### <a name="description"></a>Açıklama

Hizmet, kaynağın kaynak bilgilerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **resource_instances** Hedef kaynak KIMLIĞI işaretçisi.
- **sayı** Sayı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir Boole değeri değil.
- **NX_LWM2M_CLIENT_NO_MEMORY** Örnekleri doldurulacak bellek yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the resource information.  */
status = nx_lwm2m_client_resource_instances_get(&resource, &resource_instances,
                                                &count);

/* If status is NX_SUCCESS, the instances of multiple resource information were successfully get. */
```

## <a name="nx_lwm2m_client_resource_instances_set"></a>nx_lwm2m_client_resource_instances_set

Kaynak örneklerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_instances_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_CLIENT_RESOURCE *resource_instances, 
    UINT count);
```
### <a name="description"></a>Açıklama

Hizmet, birden fazla kaynağın kaynak örneklerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **resource_instance** Kaynak örnekleri işaretçisi.
- **sayı** Kaynak örneklerinin sayısı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the resource information.  */
status = nx_lwm2m_client_resource_instances_set(&resource, &resource_instance, 2);

/* If status is NX_SUCCESS, the resource instances were successfully set. */
```

## <a name="nx_lwm2m_client_resource_integer32_get"></a>nx_lwm2m_client_resource_integer32_get

32 bitlik bir tamsayı kaynağının değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_integer32_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER32 *integer32_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, 32 bitlik bir tamsayı kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **integer32_ptr** 32 bitlik tamsayı değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri tamsayı değeri değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_get(&resource, &integer32);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer32_set"></a>nx_lwm2m_client_resource_integer32_set

32 bitlik bir tamsayı kaynağının değerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_integer32_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER32 integer32_data);
```

### <a name="description"></a>Açıklama

Hizmet, 32 bitlik bir tamsayı kaynağının değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **integer32_data** 32 bit tamsayı verileri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_set(&resource, 8);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_integer64_get"></a>nx_lwm2m_client_resource_integer64_get

64 bitlik bir tamsayı kaynağının değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_integer64_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 *integer64_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, 64 bitlik bir tamsayı kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **integer64_ptr** 64 bitlik tamsayı değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri 64 bitlik bir tamsayı değeri değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_get(&resource, &integer64);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer64_set"></a>nx_lwm2m_client_resource_integer64_set

## <a name="set-the-value-of-a-64-bit-integer-resource"></a>64 bitlik bir tamsayı kaynağının değerini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_integer64_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 integer64_data);
```

### <a name="description"></a>Açıklama

Hizmet, 64 bitlik bir tamsayı kaynağının değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **integer64_data** 64 bit tamsayı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_set(&resource, 32323);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully set. */
```

##  <a name="nx_lwm2m_client_resource_objlnk_get"></a>nx_lwm2m_client_resource_objlnk_get

Bir nesne bağlantı kaynağının değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_objlnk_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_ID *object_id, 
    NX_LWM2M_ID *instance_id);
```

### <a name="description"></a>Açıklama

Hizmet, nesne bağlantısının değerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **object_id** Nesne KIMLIĞINE yönelik işaretçi.
- **instance_id** Nesne örneği KIMLIĞINE yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir nesne bağlantı değeri değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of the object link resource.  */
status = nx_lwm2m_client_resource_objlnk_get(&resource, &object_id, &instance_id);

/* If status is NX_SUCCESS, the object link value was successfully get. */
```

## <a name="nx_lwm2m_client_resource_objlnk_set"></a>nx_lwm2m_client_resource_objlnk_set

Kaynak örneklerini ayarlar

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_objlnk_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    NX_LWM2M_ID object_id, 
    NX_LWM2M_ID instance_id);
```

### <a name="description"></a>Açıklama

Hizmet, nesne bağlantısı kaynağının değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **object_id** Nesne KIMLIĞI.
- **instance_id** Nesne örneği KIMLIĞI.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of object link resource.  */
status = nx_lwm2m_client_resource_objlnk_set(&resource, 3303, 2);

/* If status is NX_SUCCESS, the value of object link resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_opaque_get"></a>nx_lwm2m_client_resource_opaque_get

Donuk bir kaynağın değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_opaque_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    const VOID **opaque_ptr, 
    UINT \*opaque_length);
```


### <a name="description"></a>Açıklama

Hizmet, donuk bir kaynağın değerini alır. Donuk bir kaynak değeri, arabelleğin ve uzunluğun bir işaretçisinden oluşur.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **opaque_ptr** Donuk verilerin işaretçisi.
- **opaque_length** Donuk veri uzunluğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri donuk bir kaynak değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of an opaque resource.  */
status = nx_lwm2m_client_resource_opaque_get(&resource, &opaque_ptr, &opaque_length);

/* If status is NX_SUCCESS, the value of opaque resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_opaque_set"></a>nx_lwm2m_client_resource_opaque_set

Donuk bir kaynağın değerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_opaque_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    VOID *opaque_ptr, 
    UINT opaque_length);
```

### <a name="description"></a>Açıklama

Hizmet, donuk bir kaynağın değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **opaque_ptr** Donuk verilerin işaretçisi.
- **opaque_length** Donuk verilerin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of an opaque resource.  */
status = nx_lwm2m_client_resource_opaque_set(&resource, “AQIDBAU=”, 8);

/* If status is NX_SUCCESS, the value of opaque resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_string_get"></a>nx_lwm2m_client_resource_string_get

Bir dize kaynağının değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_string_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    const CHAR **string_ptr, 
    UINT *string_length);
```

### <a name="description"></a>Açıklama

Hizmet, bir dize kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **string_ptr** Hedef dize işaretçisine yönelik işaretçi.
- **string_length** Hedef dize uzunluğuna yönelik işaretçi. Dize null sonlandırılırsa **null** olabilir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir dize değeri değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of a string resource.  */
status = nx_lwm2m_client_resource_string_get(&resource, &string_ptr, &string_length);

/* If status is NX_SUCCESS, the value of string resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_string_set"></a>nx_lwm2m_client_resource_string_set

Bir dize kaynağının değerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_string_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    CHAR *string_ptr, 
    UINT string_length);
```

### <a name="description"></a>Açıklama

Hizmet, 64 bitlik bir tamsayı kaynağının değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **string_ptr** Dize işaretçisi.
- **string_length** Dizenin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of a string resource.  */
status = nx_lwm2m_client_resource_string_set(&resource, “test”, sizeof(“test”) - 1);

/* If status is NX_SUCCESS, the value of string resource was successfully set. */
```

## <a name="nx_lwm2m_client_session_bootstrap"></a>nx_lwm2m_client_session_bootstrap

Bir önyükleme sunucusu ile oturum başlatır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_bootstrap(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID security_id, 
    ULONG ip_address, 
    UINT port);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir önyükleme sunucusu ile oturum başlatır. Sunucu, güvenlik nesnesinde karşılık gelen bir güvenlik örneğine sahip olmalıdır.

' Kapalı ' kaynağı bu sunucuyla ilişkili güvenlik örneğinde sıfırdan farklıysa, bu süre sonunda Istemci tarafından başlatılan bir önyükleme yoksa, oturum sunucu tarafından başlatılan bir önyükleme için bekler.

Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni önyükleme sunucusu oturumuyla değiştirilmiştir.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.
- **security_id** Önyükleme sunucusunda tanımlı güvenlik örneği yoksa, önyükleme sunucusunun güvenlik örneği KIMLIĞI NX_LWM2M_RESERVED_ID (65535) olarak ayarlanmalıdır.
- **ip_address** Sunucunun IP adresi.
- **bağlantı noktası** Sunucunun UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_ERROR** Önyükleme hatası.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Start bootstrap.  */
status = nx_lwm2m_client_session_bootstrap(&lwm2m_client, 0, &ip_address, 5783);

/* If status is NX_SUCCESS, start bootstrap successfully.  */
```

## <a name="nx_lwm2m_client_session_bootstrap_dtls"></a>nx_lwm2m_client_session_bootstrap_dtls

Bir önyükleme sunucusu ile güvenli bir oturum başlatır

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_bootstrap_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID security_id, 
    ULONG ip_address, 
    UINT port, 
    NX_SECURE_DTLS_SESSION *dtls_session_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, güvenli bir DTLS bağlantısı kullanarak önyükleme sunucusuyla bir oturum başlatır. Sunucu, güvenlik nesnesinde karşılık gelen bir güvenlik örneğine sahip olmalıdır.

DTLS oturumunun, bu işlev çağrılmadan önce uygun şifre paketleri ve anahtar malzemeyle yapılandırılmış olması gerekir. **NX_SECURE_ENABLE_DTLS** tanımlanmalıdır.

' Kapalı ' kaynağı bu sunucuyla ilişkili güvenlik örneğinde sıfırdan farklıysa, bu süre sonunda Istemci tarafından başlatılan bir önyükleme yoksa, oturum sunucu tarafından başlatılan bir önyükleme için bekler. 

Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni önyükleme sunucusu oturumuyla değiştirilmiştir.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.
- **security_id** Önyükleme sunucusunda tanımlı güvenlik örneği yoksa, önyükleme sunucusunun güvenlik örneği KIMLIĞI **NX_LWM2M_RESERVED_ID** (65535) olarak ayarlanmalıdır.
- **ip_address** Sunucunun IP adresi.
- **bağlantı noktası** Sunucunun UDP bağlantı noktası.
- **dtls_session_ptr** Önyükleme oturumu için kullanılacak DTLS oturumu.
- **dtls_local_port** DTLS oturumu için kullanılan yerel UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_ERROR** Önyükleme hatası.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Start bootstrap with DTLS.  */
status = nx_lwm2m_client_session_bootstrap_dtls(&lwm2m_client, 0, &ip_address, 5784, &dtls_session);

/* If status is NX_SUCCESS, start bootstrap successfully.  */
```

## <a name="nx_lwm2m_client_session_create"></a>nx_lwm2m_client_session_create

Bir LWM2M Istemci oturumu oluşturur.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_create(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK state_callback);
```

### <a name="description"></a>Açıklama

Bu hizmet, var olan bir LWM2M Istemcisine bağlı yeni bir LWM2M Istemci oturumu oluşturur. Oturum, bir önyükleme sunucusuyla veya bir LWM2M sunucusuyla iletişim kurmak için LWM2M Istemcisi tarafından kullanılır. 

Uygulama, oturumun durumu güncellendiği zaman çağrılacak bir geri çağırma işlevi sağlamalıdır.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.
- **client_ptr** Daha önce oluşturulan LWM2M Istemcisine yönelik işaretçi.
- **state_callback** Oturumun durumu değiştiğinde çağrılan uygulama geri çağırma.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Create session.  */
status = nx_lwm2m_client_session_create(&session, &lwm2m_client, session_callback);

/* If status is NX_SUCCESS, a session was successfully created.  */
```

## <a name="nx_lwm2m_client_session_delete"></a>nx_lwm2m_client_session_delete

Bir LWM2M Istemci oturumunu siler.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_delete(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir LWM2M Istemci oturumunu siler.

Nx_lwm2m_client_delete çağırarak bir LWM2M Istemcisi silindiğinde, istemciye bağlı tüm oturumlar da silinir.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Delete session.  */
status = nx_lwm2m_client_session_delete(&session);

/* If status is NX_SUCCESS, a session was successfully deleted.  */
```

## <a name="nx_lwm2m_client_session_deregister"></a>nx_lwm2m_client_session_deregister

Bir LWM2M sunucusuyla oturumu sonlandırır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_deregister(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir LWM2M sunucusuna ' de Register ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_NOT_REGISTERED** İstemci sunucuya kayıtlı değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* De-register session.  */
status = nx_lwm2m_client_session_deregister(&session);

/* If status is NX_SUCCESS, session was successfully de-registered.  */
```

## <a name="nx_lwm2m_client_session_error_get"></a>nx_lwm2m_client_session_error_get

Bir oturumun son hatasını alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_error_get(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, oturum bir hata durumundayken oturumun hata kodunu döndürür.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** Oturum hata durumunda değil.
- **NX_LWM2M_CLIENT_ADDRESS_ERROR** Geçersiz sunucu adresi.
- **NX_LWM2M_ CLIENT_BUFFER_TOO_SMALL** İsteğin yükü ağ arabelleğine uymuyor.
- **NX_LWM2M_ CLIENT_DTLS_ERROR** Sunucuyla güvenli bağlantı kurulamadı.
- **NX_LWM2M_ CLIENT_ERROR** Belirtilmeyen hata.
- **NX_LWM2M_ CLIENT_FORBIDDEN** Kayıt sunucu tarafından reddedildi.
- **NX_LWM2M_ CLIENT_NOT_FOUND** Güncelleştirme/kaydını kaldırmak, istemci sunucu tarafından bulunamadı.
- **NX_LWM2M_ CLIENT_SERVER_INSTANCE_DELETED** Oturuma karşılık gelen sunucu nesnesi örneği silindi.
- **NX_LWM2M_ CLIENT_TIMED_OUT** Sunucudan yanıt yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the error.  */
status = nx_lwm2m_client_session_error_get(&session);
```
## <a name="nx_lwm2m_client_session_register"></a>nx_lwm2m_client_session_register

Bir LWM2M sunucusuyla oturum başlatır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_register(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID server_id, 
    ULONG ip_address, 
    UINT port);
```


### <a name="description"></a>Açıklama

Bu hizmet bir LWM2M sunucusuna ' Register ' işlemi gerçekleştirir. Sunucu, sunucu nesnesinde karşılık gelen bir sunucu örneğine sahip olmalıdır.

Kayıt başarılı bir şekilde LWM2M Istemcisi, sunucudan daha fazla işlem gerçekleştirir ve istemci kayıtlı olana kadar düzenli olarak ' güncelleştirme ' iletileri gönderir.

Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni LWM2M Server oturumu tarafından değiştirilmiştir.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.
- **server_id** LWM2M sunucusunun kısa sunucu KIMLIĞI.
- **ip_address** Sunucunun IP adresi.
- **bağlantı noktası** Sunucunun UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_ERROR** Önyükleme hatası.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Start register.  */
status = nx_lwm2m_client_session_register (&lwm2m_client, 123, &ip_address, 5683);

/* If status is NX_SUCCESS, start register successfully.  */
```

## <a name="nx_lwm2m_client_session_register_dtls"></a>nx_lwm2m_client_session_register_dtls

LWM2M sunucusu ile güvenli bir oturum başlatır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_register_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID server_id, 
    ULONG ip_address, 
    UINT port,
    NX_SECURE_DTLS_SESSION *dtls_session_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, güvenli bir DTLS bağlantısı kullanarak bir LWM2M sunucusuna ' Register ' işlemi gerçekleştirir. Sunucu, sunucu nesnesinde karşılık gelen bir sunucu örneğine sahip olmalıdır.

DTLS oturumunun, bu işlev çağrılmadan önce uygun şifre paketleri ve anahtar malzemeyle yapılandırılmış olması gerekir. **NX_SECURE_ENABLE_DTLS** tanımlanmalıdır.

Kayıt başarılı bir şekilde LWM2M Istemcisi, sunucudan daha fazla işlem gerçekleştirir ve istemci kayıtlı olana kadar düzenli olarak ' güncelleştirme ' iletileri gönderir.

Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni LWM2M Server oturumu tarafından değiştirilmiştir.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.
- **server_id** LWM2M sunucusunun kısa sunucu KIMLIĞI.
- **ip_address** Sunucunun IP adresi.
- **bağlantı noktası** Sunucunun UDP bağlantı noktası.
- **dtls_session_ptr** LWM2M oturumu için kullanılacak DTLS oturumu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_ERROR** Önyükleme hatası.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Start register with DTLS.  */
status = nx_lwm2m_client_session_register_dtls(&lwm2m_client, 123, &ip_address, 5683, &dtls_session);

/* If status is NX_SUCCESS, start register with DTLS successfully.  */
```

## <a name="nx_lwm2m_client_session_register_info_get"></a>nx_lwm2m_client_session_register_info_get

LWM2M sunucusu ile güvenli bir oturum başlatır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_register_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    UINT security_instance_id, 
    NX_LWM2M_ID *server_id,
    CHAR **server_uri, 
    UINT *server_uri_length, 
    UCHAR *security_mode, 
    UCHAR **pub_key_or_id, 
    UINT *pub_key_or_id_len, 
    UCHAR **server_pub_key, 
    UINT *server_pub_key_len, 
    UCHAR **secret_key, 
    UINT *secret_key_len);
```

### <a name="description"></a>Açıklama

Bir önyükleme sunucusuyla iletişim oturumu kurulduktan sonra. Uygulama, sonraki kayıt adımı için sunucu ve güvenlik bilgilerini almak üzere bu API 'yi çağırabilir.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.
- **security_instance_id** Güvenlik örneği KIMLIĞI.
- **server_id** Hedef sunucu KIMLIĞI işaretçisi.
- **server_uri** Hedef sunucu URI 'si işaretçisi.
- **server_uri_len** Hedef sunucu URI uzunluğu işaretçisi.
- **security_mode** Hedef güvenlik modu işaretçisi.
- **pub_key_or_id** Hedef ortak anahtar veya kimlik işaretçisi.
- **pub_key_or_id_len** Hedef ortak anahtar veya kimlik uzunluğu işaretçisi.
- **server_pub_key** Hedef sunucu ortak anahtarı işaretçisi.
- **server_pub_key_len** Hedef sunucu ortak anahtar uzunluğu işaretçisi.
- **secret_key** Hedef gizli anahtar işaretçisi.
- **secret_key_len** Hedef gizli anahtar uzunluğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_NOT_FOUND** Güvenlik nesnesi örneği yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Get the register information.  */
status = nx_lwm2m_client_session_register_info_get(&session, NX_LWM2M_CLIENT_RESERVED_ID, &server_id, &server_uri, &server_uri_length, &security_mode, &pub_key_or_id, &pub_key_or_id_len, NX_NULL, NX_NULL, &secret_key, &secret_key_len);

/* If status is NX_SUCCESS, the register information was successfully gotten.  */
```

## <a name="nx_lwm2m_client_session_update"></a>nx_lwm2m_client_session_update

Bir oturumu LWM2M sunucusu ile güncelleştirir.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir LWM2M sunucusuna ' Update ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_NOT_REGISTERED** İstemci sunucuya kayıtlı değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Update a session.  */
status = nx_lwm2m_client_session_update(&session);

/* If status is NX_SUCCESS, a session was successfully updated.  */
```

## <a name="nx_lwm2m_client_unlock"></a>nx_lwm2m_client_unlock

Bir LWM2M Istemcisinin kilidini açar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce bir ***nx_lwm2m_client_unlock*** ÇAĞRıSıYLA kilitlenen LWM2M istemcisinin kilidini açar.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M Istemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, başlatma

### <a name="example"></a>Örnek

```c
/* Unlock lwm2m client.  */
status = nx_lwm2m_client_unlock(&lwm2m_client);

/* If status is NX_SUCCESS, unlock lwm2m client successfully.  */
```