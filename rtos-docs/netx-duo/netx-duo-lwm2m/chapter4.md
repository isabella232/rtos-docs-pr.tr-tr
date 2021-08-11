---
title: Bölüm 4 - LWM2M CLIENT Services'ın Açıklaması
description: Bu bölümde, tüm LWM2M İstemci hizmetlerinin alfabetik sırada bir açıklaması yer almaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 0956cb43f4fcd87d5bd4d90b2288ce6f8d5295ee0be8b8a9f4719ad842e00b2a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783450"
---
# <a name="chapter-4--description-of-lwm2m-client-services"></a>Bölüm 4 LWM2M CLIENT Services açıklaması

Bu bölümde, aşağıda alfabetik sırada listelenen tüm LWM2M İstemci hizmetlerinin açıklaması yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

**LWM2M İstemci Yönetimi:**

- nx_lwm2m_client_create: *LWM2M İstemcisi Oluşturma*

- nx_lwm2m_client_delete: *LWM2M İstemcisini Silme*

- nx_lwm2m_client_lock: *LWM2M İstemcisini Kilitleme*

- nx_lwm2m_client_unlock: *LWM2M İstemcisi'nin Kilidini Açma*

**LWM2M İstemci Oturumu Yönetimi:**

- nx_lwm2m_client_session_create: *LWM2M İstemci Oturumu Oluşturma*

- nx_lwm2m_client_session_delete: *LWM2M İstemci Oturumunu Silme*

- nx_lwm2m_client_session_bootstrap: *Bootstrap Sunucusu ile oturum başlatma*

- nx_lwm2m_client_session_bootstrap_dtls: *Bootstrap Sunucusu ile güvenli bir oturum başlatma*

- nx_lwm2m_client_session_register_info_get: *LWM2M Sunucusu kayıt bilgilerini al*

- nx_lwm2m_client_session_register: *LWM2M* Sunucusu ile oturum başlatma

- nx_lwm2m_client_session_register_dtls: *LWM2M Sunucusu ile güvenli bir oturum başlatma*

- nx_lwm2m_client_session_update: *LWM2M* Sunucusu ile oturum güncelleştirme

- nx_lwm2m_client_session_deregister: *LWM2M Sunucusu ile oturumu sonlandırma*

- nx_lwm2m_client_session_error_get: *Oturumun son hatasını al*

**Cihaz Nesnesi Uygulaması:**

- nx_lwm2m_client_device_callbacks_set: *Cihaz Nesnesi uygulama geri çağırmalarını ayarlama*

- nx_lwm2m_client_device_error_push: Cihaz *Nesnesine hata kodu ekleme*

- nx_lwm2m_client_device_error_reset: Cihaz *Nesnesinin hata kodlarını sıfırlama*

- nx_lwm2m_client_device_resource_changed: *Cihaz Nesnesi kaynağının sinyal değişikliği*

**Üretici Yazılımı Güncelleştirme Nesnesi Uygulaması:**

- nx_lwm2m_firmware_create: Üretici *Yazılımı Güncelleştirme Nesnesi Oluşturma*

- nx_lwm2m_firmware_package_info_set: Üretici *Yazılımı Güncelleştirme Paketi Bilgilerini Ayarlama*

- nx_lwm2m_firmware_result_set: Üretici *Yazılımı Güncelleştirme Sonucu Ayarlama*

- nx_lwm2m_firmware_state_set: Üretici *Yazılımı Güncelleştirme Durumunu Ayarlama*

**Özel Nesneler Uygulama:**

- nx_lwm2m_client_object_add: *LWM2M İstemcisi'ne Nesne Uygulaması Ekleme*

- nx_lwm2m_client_object_remove: *LWM2M İstemcisi'den Nesne uygulamasını kaldırma*

- nx_lwm2m_client_object_instance_add: *LWM2M İstemcisi'ne Nesne Örneği Ekleme*

- nx_lwm2m_client_object_instance_remove: Nesne *Örneğini LWM2M İstemcisi'den Kaldırma*

- nx_lwm2m_object_resource_changed: Nesne *Örneğinin kaynak değerinin sinyal değişikliği*

**Yerel Cihaz Yönetimi**

- nx_lwm2m_client_object_create: Yeni *bir Nesne Örneği oluşturma*

- nx_lwm2m_client_object_delete: Nesne *Örneğini Silme*

- nx_lwm2m_client_object_discover: Nesne *Örneğinin kaynaklarını bulma*

- nx_lwm2m_client_object_execute: Nesne *Örneğinin kaynağını yürütme*

- nx_lwm2m_client_object_next_get: *LWM2M İstemcisi tarafından uygulanan Nesnelerin listesini al*

- nx_lwm2m_client_object_instance_next_get: *Bir Nesnenin Örneklerinin listesini al*

- nx_lwm2m_client_object_read: Nesne *Örneğinin kaynak değerlerini okuma*

- nx_lwm2m_client_object_write: Nesne *örneğinin kaynak değerlerini değiştirme*

**Kaynaklar Bilgi ve Değerler Ayarı:**

- nx_lwm2m_client_resource_info_set: Kaynak *bilgilerini ayarlama*

- nx_lwm2m_client_resource_string_set: *Kaynak değerini dize olarak ayarlayın*

- nx_lwm2m_client_resource_integer32_set: Kaynak *değerini 32 Bit tamsayı olarak ayarlayın*

- nx_lwm2m_client_resource_integer64_set: Kaynak *değerini 64 Bit tamsayı olarak ayarlayın*

- nx_lwm2m_client_resource_float32_set: Kaynak *değerini 32 Bit float olarak ayarlayın*

- nx_lwm2m_client_resource_float64_set: *Kaynak değerini 64 Bit float olarak ayarlayın*

- nx_lwm2m_client_resource_boolean_set: *Kaynak değerini boole olarak ayarlayın*

- nx_lwm2m_client_resource_objlnk_set: Kaynak *değerini nesne bağlantısı olarak ayarlayın*

- nx_lwm2m_client_resource_opaque_set: Kaynak *değerini opak olarak ayarlayın*

- nx_lwm2m_client_resource_instance_set: Kaynak *değerini birden çok kaynak için örnek olarak ayarlayın*
-
- nx_lwm2m_client_resource_dim_set: Birden *çok kaynak için kaynak boyutunu ayarlayın.*

**Kaynak Bilgileri ve Değerleri Alma:**

- nx_lwm2m_client_resource_info_get: Kaynak *bilgilerini al*

- nx_lwm2m_client_resource_string_get: Dize *kaynağının değerini alır*

- nx_lwm2m_client_resource_integer32_get: *32 Bit tamsayı kaynağının değerini al*

- nx_lwm2m_client_resource_integer64_get: *64 Bit tamsayı kaynağının değerini al*

- nx_lwm2m_client_resource_float32_get: *32 Bit float kaynağının değerini al*

- nx_lwm2m_client_resource_float64_get: *64 Bit float kaynağının değerini al*

- nx_lwm2m_client_resource_boolean_get: *Boole kaynağının değerini al*

- nx_lwm2m_client_resource_objlnk_get: Nesne *bağlantısı kaynağının değerini al*

- nx_lwm2m_client_resource_opaque_get: *Opak bir kaynağın değerini al*

- nx_lwm2m_client_resource_instance_get: Birden *çok kaynak için kaynak örneğini al*

- nx_lwm2m_client_resource_dim_get: Birden *çok kaynağın kaynak boyutunu al.*

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

### <a name="description"></a>Description

Bu hizmet, kendi ThreadX iş parçacığı bağlamında çalışan bir LWM2M İstemci örneği oluşturur.

LWM2M İstemcisi şu OMA LWM2M Nesnelerini kullanır: Güvenlik (0), Sunucu (1), Access Control (2) ve Cihaz (3). Diğer nesne uygulamaları uygulama tarafından eklenmiştir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **packet_pool_ptr** Bu LWM2M İstemcisi için varsayılan paket havuzunun işaretçisi.
- **name_ptr** LWM2M İstemci uç noktası adı işaretçisi.
- **name_length** LWM2M İstemci uç noktası adının uzunluğu.
- **msisdn_ptr** SMS bağlaması desteklenmiyorsa, LWM2M İstemcisi'nin SMS bağlaması ile birlikte kullanmak üzere ulaşılab olduğu MSISDN işaretçisi NULL olabilir.
- **msisdn_length** MSISDN numarasının uzunluğu.
- **binding_modes** LWM2M İstemcisi tarafından desteklenen bağlama ve modlar, NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S ve NX_LWM2M_BINDING_SQ olabilir.
- **stack_ptr** LWM2M İstemci iş parçacığı yığın alanı işaretçisi.
- **stack_size** LWM2M İstemcisi iş parçacığı yığını boyutu.
- **öncelik** LWM2M İstemcisi önceliği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** LWM2M İstemcisi başarıyla oluşturuldu.
- **NX_LWM2M_CLIENT_ERROR** LWM2M İstemcisi oluşturma hatası.
- **NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.
- **NX_PTR_ERROR** Geçersiz işaretçi.
- **NX_SIZE_ERROR** Geçersiz yığın boyutu.
- **NX_OPTION_ERROR** Geçersiz öncelik.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

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

LWM2M İstemcisini siler.

### <a name="prototype"></a>Prototype

```C
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir LWM2M İstemci örneğini siler.

İstemciye şu anda eklenmiş olan tüm oturumlar da bu çağrı tarafından silinir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** LWM2M İstemcisi başarıyla silindi.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Delete the LWM2M Client instance.  */
status = nx_lwm2m_client_create(&lwm2m_client);

/* If status is NX_SUCCESS a LWM2M Client instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_device_callback_set"></a>nx_lwm2m_client_device_callback_set

Bir cihaz nesnesinin uygulama geri çağrısını ayarlar.

### <a name="prototype"></a>Prototype

```C
UINT **nx_lwm2m_client_device_callback_set**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_OPERATION_CALLBACK operation_callback);
```

### <a name="description"></a>Description

Bu hizmet, LWM2M İstemcisi tarafından işilmemiş LWM2M Cihaz Nesnesi kaynaklarına işlem uygulamak için uygulama geri çağrısını yüklür.

LWM2M İstemcisi şu kaynakları uygulamaya alır: Hata Kodu (11), Hata Kodunu Sıfırlama (12) ve Desteklenen Bağlama ve Modlar (16), diğer kaynaklara yapılan işlemler uygulamaya yeniden yönlendirildi.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **operation_callback** "Read", "Discover", "Write" ve "Execute" için işlem geri çağırma.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem geri çağırma başarıyla ayarlanmıştır.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Set device callback.  */
status = nx_lwm2m_client_device_callback_set(&lwm2m_client, device_operation);

/* If status is NX_SUCCESS a device callback was successfully set.  */
```

## <a name="nx_lwm2m_client_device_error_push"></a>nx_lwm2m_client_device_error_push
Bir cihaz nesnesine hata kodu ekler.

### <a name="prototype"></a>Prototype

```C
UINT **nx_lwm2m_client_device_error_push**(
    NX_LWM2M_CLIENT *client_ptr,
    UCHAR code);
```

### <a name="description"></a>Description

Bu hizmet, Nesne Cihazı'nın Hata Kodu (11) kaynağına yeni bir örnek ekler.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **kod** Yeni hata kodu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL**

En fazla depolanan hata kodu sayısı

'a ulaşıldı.

NX_PTR_ERROR İşaretçi geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```C
/* Push device error 1 (Low battery power) to server.  */
status = nx_lwm2m_client_device_error_push(&lwm2m_client, 1);

/* If status is NX_SUCCESS a device error was successfully pushed.  */
```

## <a name="nx_lwm2m_client_device_error_reset"></a>nx_lwm2m_client_device_error_reset

Cihaz Nesnesi hata kodlarını sıfırlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, Cihaz Nesnesinden tüm hata kodu kaynak örneklerini siler. Bu, kaynak Sıfırlama Hata Kodunu (12) yürütmeye eşdeğerdir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Delete all device error code.  */
status = nx_lwm2m_client_device_error_reset(&lwm2m_client);

/* If status is NX_SUCCESS, reset device error successfully.  */
```

## <a name="nx_lwm2m_client_device_resource_changed"></a>nx_lwm2m_client_device_resource_changed

Cihaz Nesnesi kaynağında bir değişiklik olduğunu gösterir.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_resource_changed(
    NX_LWM2M_CLIENT *client_ptr, 
    const NX_LWM2M_RESOURCE *resource);

```

### <a name="description"></a>Description

Hizmet, uygulama tarafından LWM2M İstemcisi'ne Nesne Cihazı kaynağının değiştiğini sinyal olarak verir. Kaynak bir LWM2M Sunucusu tarafından gözlemlenirse LWM2M İstemcisi bir bildirim gönderir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **kaynak** Değiştirilen kaynağı açıklayan yapı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Change device resource.  */
status = nx_lwm2m_client_device_resource_changed(&lwm2m_client, &resource);

/* If status is NX_SUCCESS, a device resource was successfully changed.  */
```

##  <a name="nx_lwm2m_client_firmware_create"></a>nx_lwm2m_client_firmware_create

Bir LWM2M İstemci Üretici Yazılımı Nesnesi oluşturun. 

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

### <a name="description"></a>Description

Hizmet, uygulama tarafından üretici yazılımı nesnesi oluşturmak için kullanılır.

### <a name="parameters"></a>Parametreler

- **firmware_ptr** LWM2M İstemci Üretici Yazılımı nesnesinin işaretçisi.
- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **protokoller** Desteklenen protokoller.
- **package_callback** Paket geri çağırma.
- **package_uri_callback** Paket URI geri çağırma.
- **update_callback** Güncelleştirme geri çağırma.

### <a name="return-values"></a>Dönüş Değerleri

**NX_SUCCESS** İşlem başarılı oldu.
**NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

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

LWM2M İstemci Üretici Yazılımı paket bilgilerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_firmware_package_info_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    const CHAR *name, 
    UINT name_length, 
    const CHAR *version, 
    UINT version_length);
```

### <a name="description"></a>Description

Hizmet, uygulama tarafından üretici yazılımı güncelleştirme nesnesinin paket bilgileri kaynaklarını ayarlamak için kullanılır.

### <a name="parameters"></a>Parametreler

- **firmware_ptr** LWM2M İstemci Üretici Yazılımı nesnesinin işaretçisi.
- **name** Üretici yazılımı paketinin adı.
- **name_length** Ad uzunluğu.
- **sürüm** Üretici yazılımı paketinin sürümü.
- **version_length** Sürümün uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Set the package information resources of the firmware object.  */
status = nx_lwm2m_client_firmware_package_info_set(&firmware, 2m_client,     
                                    “LWM2M Firmware”, sizeof(“LWM2M Firmware”) -1,
                                    “1.0.0.0”, sizeof(“1.0.0.0”) - 1);

/* If status is NX_SUCCESS, package information resources was successfully set. */
```

##  <a name="nx_lwm2m_client_firmware_result_set"></a>nx_lwm2m_client_firmware_result_set

Üretici yazılımı güncelleştirme nesnesinin güncelleştirme sonucu kaynağını ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_firmware_result_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a>Description

Hizmet, uygulama tarafından üretici yazılımı güncelleştirme nesnesinin güncelleştirme sonucu kaynağını ayarlamak için kullanılır.

### <a name="parameters"></a>Parametreler

- **firmware_ptr** LWM2M İstemci Üretici Yazılımı nesnesinin işaretçisi.
- **sonuç** Güncelleştirme sonucu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Set the update result resource of the firmware object.  */
status = nx_lwm2m_client_firmware_result_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_RESULT_SUCCESS);

/* If status is NX_SUCCESS, the update result resource was successfully set.  */
```

##  <a name="nx_lwm2m_client_firmware_state_set"></a>nx_lwm2m_client_firmware_state_set

Üretici yazılımı güncelleştirme nesnesinin güncelleştirme sonucu kaynağını ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_firmware_state_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a>Description

Hizmet, uygulama tarafından üretici yazılımı güncelleştirme nesnesinin durumunu ayarlamak için kullanılır.

### <a name="parameters"></a>Parametreler

- **firmware_ptr** LWM2M İstemci Üretici Yazılımı nesnesinin işaretçisi.
- **state (durum)** Üretici yazılımı nesnesinin durumu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Set the state of the firmware object.  */
status = nx_lwm2m_client_firmware_state_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_STATE_IDLE);

/* If status is NX_SUCCESS, the state was successfully set.  */
```

## <a name="nx_lwm2m_client_lock"></a>nx_lwm2m_client_lock

LWM2M İstemcisini kilitler.

### <a name="prototype"></a>Prototype

```c
UINT **nx_lwm2m_client_lock**(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, sunuculardan veya başka bir uygulama iş parçacığından LWM2M nesnelerine eşzamanlı erişimi önlemek için LWM2M İstemcisini kilitler.

LWM2M İstemcisi şu anda başka bir iş parçacığı tarafından kilitlenmişse, LWM2M İstemcisi kilidi açıncaya kadar işlev engellenir.

***çiftleri nx_lwm2m_client_lock** _/_ *_nx_lwm2m_client_unlock_** çiftleri iç içe geçmiş olabilir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Lock the LWM2M client.  */
status = nx_lwm2m_client_lock(&lwm2m_client);

/* If status is NX_SUCCESS, lwm2m client was successfully locked.  */
```

## <a name="nx_lwm2m_client_object_add"></a>nx_lwm2m_client_object_add

LWM2M İstemcisi'ne bir Nesne uygulaması ekler.

### <a name="prototype"></a>Prototype

```c
UINT **nx_lwm2m_client_object_add**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_CLIENT_OBJECT_OPERATION_CALLBACK object_operation);
```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'ne yeni bir Nesne uygulaması ekler.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_ptr** Nesne uygulamasını tanımlayan yapı işaretçisi.
- **object_id** Nesne kimliği.
- **object_operation** Nesne işlemi geri çağırma işlevi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne Kimliği zaten var.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Add new object to the lwm2m client.  */
status = nx_lwm2m_client_object_add(&lwm2m_client, &object, 
                                    3303, object_operation);

/* If status is NX_SUCCESS, the new object was successfully added.  */
```

## <a name="nx_lwm2m_client_object_create"></a>nx_lwm2m_client_object_create

Yeni bir Nesne Örneği oluşturur.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_create(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID *instance_id_ptr,
    UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a>Description

Bu hizmet, yeni bir Nesne Örneği oluşturmak için LWM2M İstemcisi'nin Nesnesi üzerinde bir 'Oluştur' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id** Nesne Kimliği.
- **instance_id_ptr** LWM2M İstemcisinin örnek kimliği ataması gerekirse yeni örneğin kimliğine işaretçi **NULL** olabilir. Kimlik 65535 ayrılmış değeri ise LWM2M İstemcisi bir Örnek Kimliği atar. NULL değeri yoksa, atanan kimlik çağrıdan sonra döndürülür.
- **num_values** Ayar için değer sayısı.
- **values_ptr** Yeni Nesne Örneğini başlatmak için kaynak değerleri dizisinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne Örneği Kimliği zaten var.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Nesne, örnek oluşturma desteğine sahip değil.
- **NX_LWM2M_CLIENT_NO_MEMORY** Yeni örneği depolamak için bellek ayrılamaz.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne Kimliği yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Create new object instance.  */
status = nx_lwm2m_client_object_create(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, a new object instance was successfully created.  */
```

## <a name="nx_lwm2m_client_object_delete"></a>nx_lwm2m_client_object_delete

Nesne Örneğini siler.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_delete(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id);
```

### <a name="description"></a>Description

Bu hizmet, LWM2M İstemcisi'nin Nesne Örneğinde bir 'Sil' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id** Nesne Kimliği.
- **instance_id** Nesne Örneği Kimliği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Nesne, örnek silmeyi desteklemez.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne Kimliği veya Nesne Örneği Kimliği yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Delete an object instance.  */
status = nx_lwm2m_client_object_delete(&lwm2m_client, 3303, 0);

/* If status is NX_SUCCESS, an object instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_object_discover"></a>nx_lwm2m_client_object_discover

Nesne Örneğinin kaynaklarını keşfeder.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_discover(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT *num_resources,
    NX_LWM2M_CLIENT_RESOURCE *resources);

```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'nin Nesne Örneğinde bir 'Bulma' işlemi gerçekleştirir; bu, Nesne tarafından uygulanan kaynakların listesini döndürür.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id** Nesne Kimliği.
- **instance_id** Nesne Örneği Kimliği.
- **num_resources** Girişte hedef arabelleğin boyutu, çıktıda arabelleğe yazılan öğe sayısıdır.
- **kaynaklar** Hedef arabelleğin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- *NX_SUCCESS** Başarılı işlem.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Kaynak arabelleği, kaynak listesini depolamak için çok küçük.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne Kimliği veya Nesne Örneği Kimliği yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

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

Nesne Örneğinin kaynağında bir 'Yürüt' işlemi gerçekleştirir.

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

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'nin Nesne Örneği Kaynağında 'Yürüt' işlemini gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id** Nesne Kimliği.
- **instance_id** Nesne Örneği Kimliği.
- **resource_id** Kaynak Kimliği.
- **arguments_ptr** Yürütme işlemi bağımsız değişkenlerinin işaretçisi. Sıfır ise NULL arguments_length olabilir.
- **arguments_length** Bağımsız değişkenlerin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Kaynak arabelleği, kaynak listesini depolamak için çok küçük.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne Kimliği veya Nesne Örneği Kimliği yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Execute object resource.  */
status = nx_lwm2m_client_object_execute (&lwm2m_client, 3303, 0, 0,  
                                         “5”, 1);

/* If status is NX_SUCCESS, an object resource was successfully executed.  */
```

## <a name="nx_lwm2m_client_object_instance_add"></a>nx_lwm2m_client_object_instance_add

Bir nesneye Nesne örneği uygulaması ekler.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_instance_add(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'ne yeni bir Nesne örneği uygulaması ekler. instance_id_ptr değeri **NX_LWM2M_CLIENT_RESERVED_ID** ise LWM2M İstemcisi otomatik olarak kullanılmayan bir örnek kimliği atar, aksi takdirde LWM2M İstemcisi uygulama kümesi değerini kullanır. Yeni örnek başarıyla eklendi instance_id, uygulamaya geri instance_id_ptr için yeni bir örnek doldurulur.

### <a name="parameters"></a>Parametreler

- **object_ptr** Nesne uygulamasını tanımlayan yapı işaretçisi.
- **instance_ptr** Nesne örneği uygulamasını tanımlayan yapı işaretçisi.
- **instance_id_ptr** Nesne örneği kimliğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_CLIENT_LWM2M_ALREADY_EXIST** Nesne Kimliği zaten var.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

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

### <a name="description"></a>Description

Bu hizmet, verilen Nesnenin sonraki Nesne Örneğinin kimliğini döndürür. Geçerli Örnek Kimliği NX_LWM2M_RESERVED_ID (65535) olarak ayarlanırsa ilk örneğin kimliği döndürülür.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id** Nesne Kimliği.
- **instance_id_ptr** Geçerli Nesne Örneği Kimliğinin işaretçisi. dönüşte nesnesinin bir sonraki Örnek Kimliği vardır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_CLIENT_LWM2M_NOT_FOUND** Verilen Örnek Kimliği nesnenin son kimliğidir veya Nesne Kimliği uygulanmaz.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Get the next instance of an object.  */
status = nx_lwm2m_client_object_instance_next_get(&lwm2m_client, 3303, 
                                                  &instance_id);

/* If status is NX_SUCCESS, get the next instance successfully.  */
```

## <a name="nx_lwm2m_client_object_instance_remove"></a>nx_lwm2m_client_object_instance_remove

Nesne örneği uygulamasını bir nesneden kaldırır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_instance_remove(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir nesneden Nesne örneğini kaldırır.

### <a name="parameters"></a>Parametreler

- ***object_ptr*** Nesne uygulamasını tanımlayan yapı işaretçisi.
- **instance_ptr** Nesne örneği uygulamasını tanımlayan yapı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne Kimliği zaten var.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Remove object instance from an object.  */
status = nx_lwm2m_client_object_instance_remove(&object, &object_instance);

/* If status is NX_SUCCESS, the object instance was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_next_get"></a>nx_lwm2m_client_object_next_get

LWM2M İstemcisi'nin sonraki nesnesini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_next_get(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID \*object_id_ptr);
```

### <a name="description"></a>Description

Bu hizmet, LWM2M İstemcisi tarafından uygulanan sonraki Nesnenin kimliğini döndürür. Geçerli Nesne Kimliği NX_LWM2M_RESERVED_ID (65535) olarak ayarlanırsa ilk Nesne Kimliği döndürülür.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id_ptr** Geçerli Nesne Kimliğinin işaretçisi. dönüşte, LWM2M İstemcisi tarafından uygulanan sonraki Nesne Kimliğini içerir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_NOT_FOUND** Verilen Nesne Kimliği, veritabanının son kimliğidir.
**NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Get the next object of lwm2m client.  */
status = nx_lwm2m_client_object_next_get(&lwm2m_client, &object_id);

/* If status is NX_SUCCESS, get the next object successfully.  */
```

## <a name="nx_lwm2m_client_object_read"></a>nx_lwm2m_client_object_read

Nesne Örneğinin kaynağının değerlerini okur.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_read(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT num_values,
    NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'nin Nesne Örneğinde 'Okuma' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id** Nesne Kimliği.
- **instance_id** Nesne Örneği Kimliği.
- **num_values** Okunan kaynak sayısı.
- **values_ptr** Okunan kaynakların NX_LWM2M_RESOURCE içeren bir dizi dosyanın işaretçisi. dönüşte, dizi karşılık gelen türler ve değerlerle doldurulur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Kaynak, okuma işlemi desteklemez.
- **NX_LWM2M_CLIENT_NOT_FOUND** Nesne Kimliği, Nesne Örneği Kimliği veya kaynak kimliği yok.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Read the object resources.  */
status = nx_lwm2m_client_object_read(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, the resources were successfully read.  */
```

## <a name="nx_lwm2m_client_object_remove"></a>nx_lwm2m_client_object_remove

Nesne örneği uygulamasını bir nesneden kaldırır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_remove(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr);
```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'ne bir Nesnesi kaldırır.

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_ptr** Nesne uygulamasını tanımlayan yapı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne Kimliği zaten var.
- **NX_PTR_ERROR** Geçersiz işaretçi.
- **NX_LWM2M_CLIENT_FORBIDDEN** İç nesnenin kaldırılması yasaktır.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Remove object from lwm2m client.  */
status = nx_lwm2m_client_object_remove(&lwm2m_client, &object);

/* If status is NX_SUCCESS, the object was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_resource_changed"></a>nx_lwm2m_client_object_resource_changed

Nesne kaynağında bir değişikliğin sinyalini verir.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_resource_changed(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Description

Hizmet, uygulama tarafından LWM2M İstemcisi'ne Nesnenin kaynağının değiştiğini sinyal olarak verir. Kaynak bir LWM2M Sunucusu tarafından gözlemlenirse LWM2M İstemcisi bir bildirim gönderir.

### <a name="parameters"></a>Parametreler

- **object_ptr** Nesne uygulamasını tanımlayan yapı işaretçisi.
- ***instance_ptr*** Nesne örneği uygulamasını tanımlayan yapı işaretçisi.
- **kaynak** Değiştirilen kaynağı açıklayan yapı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Change object resource.  */
status = nx_lwm2m_client_object_resource_changed(&object, &instance, &resource);

/* If status is NX_SUCCESS, a resource was successfully changed.  */
```

## <a name="nx_lwm2m_client_object_write"></a>nx_lwm2m_client_object_write

Bir Nesne örneğinin kaynağının değerlerini değiştirir.

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

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'nin Nesne Örneğinde 'Yazma' işlemi gerçekleştirir.

Aşağıdaki yazma işlemleri write_op *belirtilebilir.*

| Değer | Yazma &nbsp; İşlemleri | Açıklama |
| --- | ---| --- |
| 0 | Kısmi Güncelleştirme | Sağlanan kaynakları yeni değere ekler veya günceller ve diğer mevcut Kaynakları olduğu gibi bırakır. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE** | Örneği Değiştir | Nesne Örneğini yeni sağlanan kaynak değerleriyle değiştirir. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE** | Kaynağı Değiştir | Resources yerine sağlanan yeni kaynak değerlerini (Birden Çok Kaynağı değiştirmek için kullanılır) değiştirir. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP** | Bootstrap Yazma | Bootstrap diziden bir çağrı gösterir. |

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id** Nesne Kimliği.
- **instance_id** Nesne Örneği Kimliği.
- **num_values** Yazacak kaynak sayısı.
- **values_ptr** Kaynakların kimliklerini, NX_LWM2M_RESOURCE ve yazacak değerleri içeren bir dizi öğenin işaretçisi.
- **write_op** Yazma işlemi türü.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynağın türü geçerli değil.
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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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
### <a name="description"></a>Description

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

### <a name="description"></a>Description

Hizmet, 32 bitlik bir tamsayı kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak işaretçisi.
- **integer32_ptr** 32 bitlik tamsayı değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri tamsayı değeri değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_get(&resource, &integer32);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer32_set"></a>nx_lwm2m_client_resource_integer32_set

32 Bit kaynak tamsayı değerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_integer32_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER32 integer32_data);
```

### <a name="description"></a>Description

Hizmet, 32 Bit kaynak tamsayı değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak İşaretçisi.
- **integer32_data** 32 Bit tamsayı verileri içerir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_set(&resource, 8);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_integer64_get"></a>nx_lwm2m_client_resource_integer64_get

64 Bit kaynak tamsayı değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_integer64_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 *integer64_ptr);
```

### <a name="description"></a>Description

Hizmet, 64 Bit kaynak tamsayı değerini verir.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak İşaretçisi.
- **integer64_ptr** 64 Bit tamsayı değerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri 64 Bit tamsayı değeri değildir.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_get(&resource, &integer64);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer64_set"></a>nx_lwm2m_client_resource_integer64_set

## <a name="set-the-value-of-a-64-bit-integer-resource"></a>Kaynağın 64 Bit tamsayı değerini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_integer64_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 integer64_data);
```

### <a name="description"></a>Description

Hizmet, 64 Bit kaynak tamsayı değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak İşaretçisi.
- **integer64_data** 64 bit tamsayı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_set(&resource, 32323);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully set. */
```

##  <a name="nx_lwm2m_client_resource_objlnk_get"></a>nx_lwm2m_client_resource_objlnk_get

Nesne bağlantısı kaynağının değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_objlnk_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_ID *object_id, 
    NX_LWM2M_ID *instance_id);
```

### <a name="description"></a>Description

Hizmet, nesne bağlantısının değerini verir.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak İşaretçisi.
- **object_id** Nesne kimliğinin işaretçisi.
- **instance_id** Nesne örneği kimliğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir nesne bağlantı değeri değildir.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

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

### <a name="description"></a>Description

Hizmet, nesne bağlantısı kaynağının değerini ayarlar.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak İşaretçisi.
- **object_id** Nesne Kimliği.
- **instance_id** Nesne örneği kimliği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Set the value of object link resource.  */
status = nx_lwm2m_client_resource_objlnk_set(&resource, 3303, 2);

/* If status is NX_SUCCESS, the value of object link resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_opaque_get"></a>nx_lwm2m_client_resource_opaque_get

Opak bir Kaynağın değerini alır.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_opaque_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    const VOID **opaque_ptr, 
    UINT \*opaque_length);
```


### <a name="description"></a>Description

Hizmet, opak bir Kaynağın değerini verir. Opak bir kaynak değeri, bir arabellek işaretçisi ve bir uzunluktan oluşur.

### <a name="parameters"></a>Parametreler

- **kaynak** Kaynak İşaretçisi.
- **opaque_ptr** Opak verilerin işaretçisi.
- **opaque_length** Opak veri uzunluğunun işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri opak bir kaynak değildir.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Get the value of an opaque resource.  */
status = nx_lwm2m_client_resource_opaque_get(&resource, &opaque_ptr, &opaque_length);

/* If status is NX_SUCCESS, the value of opaque resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_opaque_set"></a>nx_lwm2m_client_resource_opaque_set

Opak bir Kaynağın değerini ayarlar.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_resource_opaque_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    VOID *opaque_ptr, 
    UINT opaque_length);
```

### <a name="description"></a>Description

Hizmet, opak bir Kaynağın değerini ayarlar.

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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


### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

Bootstrap sunucusuyla iletişim oturumu kurulduktan sonra. Uygulama, sonraki kayıt adımına ilişkin sunucu ve güvenlik bilgilerini almak için bu API'yi çağırabilirsiniz.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M İstemci Oturumu denetim bloğuna işaretçi.
- **security_instance_id** Güvenlik örneği kimliği.
- **server_id** Hedef sunucu kimliği işaretçisi.
- **server_uri** Hedef sunucu uri'sinin işaretçisi.
- **server_uri_len** Hedef sunucu uri uzunluğu işaretçisi.
- **security_mode** Hedef güvenlik modu işaretçisi.
- **pub_key_or_id** Hedef ortak anahtar veya kimliğin işaretçisi.
- **pub_key_or_id_len** Hedef ortak anahtar veya kimlik uzunluğu işaretçisi.
- **server_pub_key** Hedef sunucu ortak anahtarının işaretçisi.
- **server_pub_key_len** Hedef sunucu ortak anahtar uzunluğuna işaretçi.
- **secret_key** Hedef gizli anahtar işaretçisi.
- **secret_key_len** Hedef gizli anahtar uzunluğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_NOT_FOUND** Güvenlik Nesnesi örneği yoktur.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Get the register information.  */
status = nx_lwm2m_client_session_register_info_get(&session, NX_LWM2M_CLIENT_RESERVED_ID, &server_id, &server_uri, &server_uri_length, &security_mode, &pub_key_or_id, &pub_key_or_id_len, NX_NULL, NX_NULL, &secret_key, &secret_key_len);

/* If status is NX_SUCCESS, the register information was successfully gotten.  */
```

## <a name="nx_lwm2m_client_session_update"></a>nx_lwm2m_client_session_update

LWM2M Sunucusu ile bir oturumu güncelleştirme.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet LWM2M Sunucusuna bir 'Güncelleştirme' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **session_ptr** LWM2M İstemci Oturumu denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_LWM2M_CLIENT_NOT_REGISTERED** İstemci sunucuya kayıtlı değil.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Update a session.  */
status = nx_lwm2m_client_session_update(&session);

/* If status is NX_SUCCESS, a session was successfully updated.  */
```

## <a name="nx_lwm2m_client_unlock"></a>nx_lwm2m_client_unlock

LWM2M İstemcisi'nin kilidini açma.

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce nx_lwm2m_client_unlock çağrısıyla kilitlenmiş LWM2M ***İstemcisi'nin kilidini nx_lwm2m_client_unlock.***

### <a name="parameters"></a>Parametreler

- **client_ptr** LWM2M İstemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** İşlem başarılı oldu.
- **NX_PTR_ERROR** Geçersiz işaretçi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları, Başlatma

### <a name="example"></a>Örnek

```c
/* Unlock lwm2m client.  */
status = nx_lwm2m_client_unlock(&lwm2m_client);

/* If status is NX_SUCCESS, unlock lwm2m client successfully.  */
```