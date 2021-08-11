---
title: Bölüm 4-Azure RTOS NetX LWM2M Services açıklaması
description: Bu bölüm, tüm Azure RTOS NetX LWM2M hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 171f8577d252027548c24ec92f11f03c1fae768f1676f476256c13b8e8dc4175
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799090"
---
# <a name="chapter-4---description-of-azure-rtos-netx-lwm2m-services"></a>Bölüm 4-Azure RTOS NetX LWM2M Services açıklaması

Bu bölüm, tüm Azure RTOS NetX LWM2M hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

### <a name="lwm2m-client-management"></a>LWM2M Istemci yönetimi

- **nx_lwm2m_client_create**: *lwm2m istemcisi oluşturma*
- **nx_lwm2m_client_delete**: *lwm2m istemcisini Sil*
- **nx_lwm2m_client_lock**: *lwm2m istemcisini kilitle*
- **nx_lwm2m_client_object_add**: *lwm2m istemcisine nesne uygulamasını ekleme*
- **nx_lwm2m_client_unlock**: *lwm2m istemcisinin kilidini aç*

### <a name="lwm2m-client-session-management"></a>LWM2M Istemci oturumu yönetimi

- **nx_lwm2m_client_session_bootstrap**: *bir önyükleme sunucusu ile oturum başlatma*
- **nx_lwm2m_client_session_bootstrap_dtls**: *bir önyükleme sunucusu ile güvenli bir oturum başlatma*
- **nx_lwm2m_client_session_create**: *lwm2m istemci oturumu oluştur*
- **nx_lwm2m_client_session_delete**: *lwm2m istemci oturumunu Sil*
- **nx_lwm2m_client_session_deregister**: BIR *oturumu lwm2m sunucusu ile sonlandırma*
- **nx_lwm2m_client_session_error_get**: *bir oturumun son hatasını al*
- **nx_lwm2m_client_session_register**: *lwm2m sunucusu ile oturum başlatma*
- **nx_lwm2m_client_session_register_dtls**: *lwm2m sunucusu ile güvenli bir oturum başlatma*
- **nx_lwm2m_client_session_update**: *bir oturumu lwm2m sunucusuyla güncelleştirme*

### <a name="security-object-implementation"></a>Güvenlik nesnesi uygulama

- **nx_lwm2m_client_security_key_callbacks_set**: *güvenlik anahtarı yönetimi geri çağırmaları ayarla*

### <a name="device-object-implementation"></a>Cihaz nesnesi uygulama

- **nx_lwm2m_client_device_callbacks_set**: *cihaz nesnesi uygulama geri çağırmaları ayarla*
- **nx_lwm2m_client_device_error_push**: *cihaz nesnesine hata kodu ekleyin*
- **nx_lwm2m_client_device_error_reset**: *cihaz nesnesinin hata kodlarını sıfırlayın*
- **nx_lwm2m_client_device_resource_changed**: *cihaz nesne kaynağının sinyal değişikliği*

### <a name="custom-objects-implementation"></a>Özel nesne uygulamaları

- **nx_lwm2m_object_resource_changed**: bir *nesne örneğinin kaynak değeri için sinyal değişikliği*

### <a name="local-device-management"></a>Yerel cihaz yönetimi

- **nx_lwm2m_client_object_create**: *Yeni bir nesne örneği oluştur*
- **nx_lwm2m_client_object_delete**: *bir nesne örneğini silme*
- **nx_lwm2m_client_object_discover**: *bir nesne örneğinin kaynaklarını bulma*
- **nx_lwm2m_client_object_execute**: *bir nesne örneğinin kaynağını yürütün*
- **nx_lwm2m_client_object_get_next**: *lwm2m Istemcisi tarafından uygulanan nesne listesini al*
- **nx_lwm2m_client_object_instance_get_next**: *bir nesnenin örneklerinin listesini al*
- **nx_lwm2m_client_object_read**: *bir nesne örneğinin kaynak değerlerini oku*
- **nx_lwm2m_client_object_write**: *bir nesne örneğinin kaynak değerlerini değiştirme*

### <a name="resources-values-decoding"></a>Kaynak değerlerinin kodunu çözme

- **nx_lwm2m_resource_get_boolean**: *bir Boole kaynağının değerini Al*
- **nx_lwm2m_resource_get_float32**: *32 bitlik kayan nokta kaynağının değerini Al*
- **nx_lwm2m_resource_get_float64**: *64 bitlik kayan nokta kaynağının değerini Al*
- **nx_lwm2m_resource_get_integer32**: *32 bitlik bir tamsayı kaynağının değerini Al*
- **nx_lwm2m_resource_get_integer64**: *64 bitlik bir tamsayı kaynağının değerini Al*
- **nx_lwm2m_resource_get_objlnk**: *nesne bağlantı kaynağının değerini Al*
- **nx_lwm2m_resource_get_opaque**: *donuk bir kaynağın değerini Al*
- **nx_lwm2m_resource_get_string**: *bir dize kaynağının değerini Al*
- **nx_lwm2m_resource_multiple_get_boolean**: *bir Boole kaynağı birden çok kaynak örneği değeri alın*
- **nx_lwm2m_resource_multiple_get_float32**: *32 bitlik kayan nokta çoklu kaynak örneği değerini Al*
- **nx_lwm2m_resource_multiple_get_float64**: *64 bitlik kayan nokta çoklu kaynak örneği değerini Al*
- **nx_lwm2m_resource_multiple_get_integer32**: *32 bitlik bir tamsayı birden çok kaynak örneğinin değerini Al*
- **nx_lwm2m_resource_multiple_get_integer64**: *64 bitlik bir tamsayı birden çok kaynak örneğinin değerini Al*
- **nx_lwm2m_resource_multiple_get_objlnk**: *birden çok kaynak örneği Için bir nesne bağlantısı değeri alın*
- **nx_lwm2m_resource_multiple_get_opaque**: *donuk birden çok kaynak örneğinin değerini Al*
- **nx_lwm2m_resource_multiple_get_string**: *dize çoklu kaynak örneği değerini Al*

### <a name="firmware-update-object"></a>Bellenim güncelleştirme nesnesi

- **nx_lwm2m_firmware_create**: *bellenim güncelleştirme nesnesi oluştur*
- **nx_lwm2m_firmware_package_info_set**: *bellenim güncelleştirme paketi bilgilerini ayarla*
- **nx_lwm2m_firmware_result_set**: *bellenim güncelleştirme sonucunu ayarla*
- **nx_lwm2m_firmware_state_set**: *bellenim güncelleştirme durumunu ayarla*

## <a name="nx_lwm2m_client_create"></a>nx_lwm2m_client_create

LWM2M Istemcisi oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_create(NX_LWM2M_CLIENT *client_ptr, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr, UINT local_port, const CHAR *name_ptr,
    const CHAR *msisdn_ptr, UCHAR binding_modes, VOID *stack_ptr, ULONG stack_size);
```

### <a name="description"></a>Description

Bu hizmet kendi ThreadX iş parçacığı bağlamında çalışan bir LWM2M Istemci örneği oluşturur.

LWM2M Istemcisi şu OMA LWM2M nesnelerini uygular: güvenlik (0), sunucu (1), Access Control (2) ve cihaz (3). Diğer nesneler uygulamaları, uygulama tarafından eklenmelidir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **ip_ptr**: daha önce oluşturulan IP örneğine yönelik işaretçi.
- **packet_pool_ptr**: Bu LWM2M istemcisi için varsayılan paket havuzuna yönelik işaretçi.
- **local_port**: güvenli olmayan iletişim için kullanılan yerel UDP bağlantı noktası.
- **name_ptr**: LWM2M istemci uç noktası adı işaretçisi.
- **msisdn_ptr**: LWM2M istemcisine SMS bağlaması ile kullanım için ULAŞıLABILDIĞI MSISDN IŞARETÇISINE, SMS bağlaması desteklenmiyorsa null olabilir.
- **binding_modes**: LWM2M istemcisi tarafından desteklenen bağlama ve modlar NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S ve NX_LWM2M_BINDING_SQ bayraklarının bir birleşimi olmalıdır.
- **stack_ptr**: Işaretçi LWM2M istemci iş parçacığı yığın alanı.
- **stack_size**: LWM2M istemci iş parçacığı yığın boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: LWM2M istemcisi başarıyla oluşturuldu.
- **NX_LWM2M_ERROR**: LWM2M istemcisi oluşturma hatası.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_delete"></a>nx_lwm2m_client_delete

LWM2M Istemcisini Sil

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir LWM2M Istemci örneğini siler.

O anda istemcinin bağlı olduğu tüm oturumlar bu çağrı tarafından da silinir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: LWM2M istemcisi başarıyla silindi.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_device_callbacks_set"></a>nx_lwm2m_client_device_callbacks_set

Cihaz nesnesi uygulama geri çağırmaları ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_READ_CALLBACK read_callback,
    NX_LWM2M_CLIENT_DEVICE_DISCOVER_CALLBACK discover_callback,
    NX_LWM2M_CLIENT_DEVICE_WRITE_CALLBACK write_callback,
    NX_LWM2M_CLIENT_DEVICE_EXECUTE_CALLBACK execute_callback);
```

### <a name="description"></a>Description

Bu hizmet, LWM2M Istemcisi tarafından işlenmeyen LWM2M cihaz nesnesi kaynaklarına işlem uygulamak için uygulama geri çağırmaları yüklüyor.

LWM2M Istemcisi şu kaynakları uygular: hata kodu (11), sıfırlama hata kodu (12) ve desteklenen bağlama ve modlar (16), diğer kaynaklara yönelik işlemler uygulamaya yeniden yönlendirilir.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **read_callback:**'Read' yöntemi geri çağırma.
- **discover_callback:**'Discover' yöntemi geri çağırma.
- **write_callback:**'Write' yöntemi geri çağırma.
- **execute_callback:**'Execute' yöntemi geri çağırma.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_device_error_push"></a>nx_lwm2m_client_device_error_push

Cihaz Nesnesine hata kodu ekleme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_error_push(NX_LWM2M_CLIENT *client_ptr, UCHAR code);
```

### <a name="description"></a>Description

Bu hizmet, Nesne Cihazı'nın Hata Kodu (11) kaynağına yeni bir örnek ekler.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **code:** Yeni hata kodu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BUFFER_TOO_SMALL:** Depolanan hata kodu sayısı üst sayısına ulaşıldı.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_device_error_reset"></a>nx_lwm2m_client_device_error_reset

Cihaz Nesnesinin hata kodlarını sıfırlama

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, Cihaz Nesnesinden tüm hata kodu kaynak örneklerini siler. Bu, kaynak Sıfırlama Hata Kodunu (12) yürütmeye eşdeğerdir.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_device_resource_changed"></a>nx_lwm2m_client_device_resource_changed

Cihaz Nesnesi kaynağının sinyal değişikliği

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_resource_changed(NX_LWM2M_CLIENT *client_ptr,
                                    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Description

Hizmet, uygulama tarafından LWM2M İstemcisi'ne Nesne Cihazı kaynağının değiştiğini sinyal olarak verir. Kaynak bir LWM2M Sunucusu tarafından gözlemlenirse LWM2M İstemcisi bir bildirim gönderir.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **resource:** Değiştirilen kaynağı açıklayan yapının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_lock"></a>nx_lwm2m_client_lock

LWM2M İstemcisini Kilitleme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_lock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, sunuculardan veya başka bir uygulama iş parçacığından LWM2M nesnelerine eşzamanlı erişimi önlemek için LWM2M İstemcisini kilitler.

LWM2M İstemcisi şu anda başka bir iş parçacığı tarafından kilitlenmişse, LWM2M İstemcisi kilidi açıncaya kadar işlev engellenir.

nx_lwm2m_client_lock()/nx_lwm2m_client_unlock() çiftleri için çağrılar iç içe geçmiş olabilir.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_add"></a>nx_lwm2m_client_object_add

LWM2M İstemcisi'ne Nesne uygulaması ekleme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_add(NX_LWM2M_CLIENT *client_ptr,
                                NX_LWM2M_OBJECT *object_ptr);
```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'ne yeni bir Nesne uygulaması ekler.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **object_ptr:** Nesne uygulamasını tanımlayan yapının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_ALREADY_EXIST:** Nesne Kimliği zaten var.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_create"></a>nx_lwm2m_client_object_create

Yeni bir Nesne Örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_create(NX_LWM2M_CLIENT *client_ptr,
            NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr,
            UINT num_values, const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a>Description

Bu hizmet, yeni bir Nesne Örneği oluşturmak için LWM2M İstemcisi'nin Nesnesi üzerinde bir 'Oluştur' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id:** Nesne Kimliği.
- **instance_id_ptr:** LWM2M İstemcisinin örnek kimliği ataması gerekirse yeni örneğin kimliğine işaretçi NULL olabilir. Kimlik 65535 ayrılmış değeri ise LWM2M İstemcisi bir Örnek Kimliği atar. NULL değeri yoksa, atanan kimlik çağrıdan sonra döndürülür.
- **num_values:** Ayar için değer sayısı.
- **values_ptr:** Yeni Nesne Örneğini başlatmak için bir kaynak değerleri dizisinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_ALREADY_EXIST:** Nesne Örneği Kimliği zaten var.
- **NX_LWM2M_METHOD_NOT_ALLOWED:** Nesne, örnek oluşturma desteğine sahip değil.
- **NX_LWM2M_NO_MEMORY:** Yeni örneği depolamak için bellek ayrılamaz.
- **NX_LWM2M_NOT_FOUND:** Nesne Kimliği yok.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_delete"></a>nx_lwm2m_client_object_delete

Nesne Örneğini Silme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_delete(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id);
```

### <a name="description"></a>Description

Bu hizmet, LWM2M İstemcisi'nin Nesne Örneğinde bir 'Sil' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id:** Nesne Kimliği.
- **instance_id:** Nesne Örneği Kimliği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_METHOD_NOT_ALLOWED:** Nesne, örnek silmeyi desteklemez.
- **NX_LWM2M_NOT_FOUND:** Nesne Kimliği veya Nesne Örneği Kimliği yok.
- NX_PTR_ERROR İşaretçi geçersiz.

## <a name="nx_lwm2m_client_object_discover"></a>nx_lwm2m_client_object_discover

Nesne Örneğinin kaynaklarını bulma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_discover(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT *num_resources_ptr, NX_LWM2M_RESOURCE_INFO *resources_ptr);
```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'nin Nesne Örneğinde bir 'Bulma' işlemi gerçekleştirir; bu, Nesne tarafından uygulanan kaynakların listesini döndürür.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id:** Nesne Kimliği.
- **instance_id:** Nesne Örneği Kimliği.
- **num_resources_ptr:** Girişte hedef arabelleğin boyutunu girin, çıkışta arabelleğe yazacak öğe sayısı.
- **resources_ptr:** Hedef arabelleğin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem..
- **NX_LWM2M_BUFFER_TOO_SMALL:** Kaynak arabelleği, kaynak listesini depolamak için çok küçük.
- **NX_LWM2M_NOT_FOUND:** Nesne Kimliği veya Nesne Örneği Kimliği yok.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_execute"></a>nx_lwm2m_client_object_execute

Nesne Örneğinin kaynağını yürütme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_execute(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr, UINT arguments_length);
```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'nin Nesne Örneği Kaynağında 'Yürüt' işlemini gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id:** Nesne Kimliği.
- **instance_id:** Nesne Örneği Kimliği.
- **resource_id:** Kaynak Kimliği.
- **arguments_ptr:** Yürütme işlemi bağımsız değişkenlerinin işaretçisi. Sıfır ise NULL arguments_length olabilir.
- **arguments_length:** Bağımsız değişkenlerin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_METHOD_NOT_ALLOWED:** Kaynak, yürütmeyi desteklemez.
- **NX_LWM2M_NOT_FOUND:** Nesne Kimliği, Nesne Örneği Kimliği veya kaynak kimliği yok.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_get_next"></a>nx_lwm2m_client_object_get_next

LWM2M İstemcisi tarafından uygulanan Nesnelerin listesini al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_get_next(NX_LWM2M_CLIENT *client_ptr,
                                    NX_LWM2M_ID *object_id_ptr);
```

### <a name="description"></a>Description

Bu hizmet, LWM2M İstemcisi tarafından uygulanan sonraki Nesnenin kimliğini döndürür. Geçerli Nesne Kimliği NX_LWM2M_RESERVED_ID (65535) olarak ayarlanırsa ilk Nesne Kimliği döndürülür.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id_ptr:** Geçerli Nesne Kimliğinin işaretçisi. dönüşte, LWM2M İstemcisi tarafından uygulanan sonraki Nesne Kimliğini içerir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem..
- **NX_LWM2M_NOT_FOUND:** Verilen Nesne Kimliği, veritabanının son kimliğidir.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_instance_get_next"></a>nx_lwm2m_client_object_instance_get_next

Bir Nesnenin Örneklerinin listesini al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_instance_get_next(NX_LWM2M_CLIENT *client_ptr,
                    NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a>Description

Bu hizmet, verilen Nesnenin sonraki Nesne Örneğinin kimliğini döndürür. Geçerli Örnek Kimliği NX_LWM2M_RESERVED_ID (65535) olarak ayarlanırsa ilk örneğin kimliği döndürülür.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id:** Nesne Kimliği.
- **instance_id_ptr:** Geçerli Nesne Örneği Kimliğinin işaretçisi. dönüşte nesnesinin bir sonraki Örnek Kimliği vardır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem..
- **NX_LWM2M_NOT_FOUND:** Verilen Örnek Kimliği nesnenin son örneğidir veya Nesne Kimliği uygulanmaz.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_read"></a>nx_lwm2m_client_object_read

Nesne Örneğinin kaynak değerlerini okuma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_read(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT num_values, NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'nin Nesne Örneğinde 'Okuma' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id:** Nesne Kimliği.
- **instance_id:** Nesne Örneği Kimliği.
- **num_values:** Okunan kaynak sayısı.
- **values_ptr:** Okunan kaynakların NX_LWM2M_RESOURCE içeren bir dizi dosyanın işaretçisi. dönüşte, dizi karşılık gelen türler ve değerlerle doldurulur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_METHOD_NOT_ALLOWED:** Bir kaynak, okuma işlemi desteklemez.
- **NX_LWM2M_NOT_FOUND:** Nesne Kimliği, Nesne Örneği Kimliği veya kaynak kimliği yok.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_write"></a>nx_lwm2m_client_object_write

Nesne örneğinin kaynak değerlerini değiştirme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_write(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, UINT num_values,
        const NX_LWM2M_RESOURCE *values_ptr, UINT write_op);
```

### <a name="description"></a>Description

Bu hizmet LWM2M İstemcisi'nin Nesne Örneğinde 'Yazma' işlemi gerçekleştirir.

Aşağıdaki yazma işlemleri write_op *belirtilebilir:*

- **0** Kısmi Güncelleştirme: Yeni değerde sağlanan Kaynakları ekler veya &mdash; günceller ve diğer mevcut Kaynakları olduğu gibi bırakır,

- **NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Örneği Değiştir: Nesne Örneğini yeni sağlanan kaynak değerleriyle değiştirir.

- **NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Kaynağı Değiştir: , Kaynaklar'ın yerine sağlanan yeni kaynak değerlerini (Birden Çok Kaynağı değiştirmek için kullanılır) alır.

- **NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap Yazma: Bir Bootstrap dizisini gösterir.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.
- **object_id:** Nesne Kimliği.
- **instance_id:** Nesne Örneği Kimliği.
- **num_values:** Yazacak kaynak sayısı.
- **values_ptr:** Kaynakların kimliklerini, NX_LWM2M_RESOURCE ve yazacak değerleri içeren bir dizi dosyanın işaretçisi.
- **write_op:** Yazma işlemi türü.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_ENCODING**: kaynak türü geçerli değil.
- **NX_LWM2M_BUFFER_TOO_SMALL**: bir değerin uzunluğu, örnekte depolanamayacak kadar büyük.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: bir kaynak yazma işlemini desteklemiyor.
- **NX_LWM2M_NO_MEMORY**: bir kaynak değeri depolamak için bellek ayrılamıyor.
- **NX_LWM2M_NOT_ACCEPTABLE**: bir kaynağın değeri geçerli değil.
- **NX_LWM2M_NOT_FOUND**: nesne kimliği, nesne örneği kimliği veya kaynak kimliği yok.
- NX_OPTION_ERROR: geçersiz yazma işlemi türü.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_security_key_callbacks_set"></a>nx_lwm2m_client_security_key_callbacks_set

Güvenlik nesnesi anahtar yönetimi geri çağırmaları ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_security_key_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_CLIENT_SECURITY_KEY_WRITE_CALLBACK write_callback,
                NX_LWM2M_CLIENT_SECURITY_KEY_DELETE_CALLBACK delete_callback);
```

### <a name="description"></a>Description

Bu hizmet, güvenlik anahtarlarıyla ilgili LWM2M güvenlik nesnesi kaynakları üzerinde işlem uygulamak için uygulama geri çağırmaları yüklüyor.

LWM2M Istemcisi, önyükleme oturumları sırasında güvenlik anahtarı yönetimini uygulamaya devreder, önyükleme sunucusu bir güvenlik nesnesi örneğinde aşağıdaki kaynakları yazdığında veya sildiği geri çağrılar çağrılır: ortak anahtar veya kimlik (3), sunucu ortak anahtar (4), gizli anahtar (5).

Uygulama, anahtar verilerinin depolanmasından ve LWM2M istemcisi tarafından kullanılan DTLS oturumlarını yapılandırmadan sorumludur.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **write_callback**: ' Write ' anahtar yöntemi geri çağırması.
- **delete_callback**: ' DELETE ' anahtar yöntemi geri çağırması.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_bootstrap"></a>nx_lwm2m_client_session_bootstrap

Önyükleme sunucusu ile oturum başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_bootstrap(NX_LWM2M_CLIENT_SESSION
    *session_ptr, NX_LWM2M_ID security_id, ULONG ip_address, UINT port);
```

### <a name="description"></a>Description

Bu hizmet, bir önyükleme sunucusu ile oturum başlatır. Sunucu, güvenlik nesnesinde karşılık gelen bir güvenlik örneğine sahip olmalıdır.

' Kapalı ' kaynağı bu sunucuyla ilişkili güvenlik örneğinde sıfırdan farklıysa, bu süre sonunda Istemci tarafından başlatılan bir önyükleme yoksa, oturum sunucu tarafından başlatılan bir önyükleme için bekler.

Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni önyükleme sunucusu oturumuyla değiştirilmiştir.

### <a name="parameters"></a>Parametreler

- **session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.
- **security_id**: önyükleme sunucusunda tanımlı güvenlik örneği yoksa önyükleme sunucusunun GÜVENLIK örneği kimliği NX_LWM2M_RESERVED_ID (65535) olarak ayarlanmalıdır.
- **ip_address**: sunucunun IP adresi.
- **bağlantı noktası**: sunucunun UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_NOT_FOUND**: güvenlık örneği kimliğine karşılık gelen bir güvenlik nesnesi örneği yok.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_bootstrap_dtls"></a>nx_lwm2m_client_session_bootstrap_dtls

Önyükleme sunucusu ile güvenli bir oturum başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_bootstrap_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID security_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a>Description

Bu hizmet, güvenli bir DTLS bağlantısı kullanarak önyükleme sunucusuyla bir oturum başlatır. Sunucu, güvenlik nesnesinde karşılık gelen bir güvenlik örneğine sahip olmalıdır.

DTLS oturumunun, bu işlev çağrılmadan önce uygun şifre paketleri ve anahtar malzemeyle yapılandırılmış olması gerekir. NX_SECURE_ENABLE_DTLS tanımlanmalıdır.

' Kapalı ' kaynağı bu sunucuyla ilişkili güvenlik örneğinde sıfırdan farklıysa, bu süre sonunda Istemci tarafından başlatılan bir önyükleme yoksa, oturum sunucu tarafından başlatılan bir önyükleme için bekler.

Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni önyükleme sunucusu oturumuyla değiştirilmiştir.

### <a name="parameters"></a>Parametreler

- **session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.
- **security_id**: önyükleme sunucusunda tanımlı güvenlik örneği yoksa önyükleme sunucusunun GÜVENLIK örneği kimliği NX_LWM2M_RESERVED_ID (65535) olarak ayarlanmalıdır.
- **ip_address**: sunucunun IP adresi.
- **bağlantı noktası**: sunucunun UDP bağlantı noktası.
- **dtls_session_ptr**: önyükleme oturumu için kullanılacak DTLS oturumu.
- **dtls_local_port**: DTLS oturumu için kullanılan yerel UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_NOT_FOUND**: güvenlık örneği kimliğine karşılık gelen bir güvenlik nesnesi örneği yok.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_create"></a>nx_lwm2m_client_session_create

LWM2M Istemci oturumu oluştur

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_create(NX_LWM2M_CLIENT_SESSION *session_ptr,
         NX_LWM2M_CLIENT *client_ptr,
         NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK state_callback);
```

### <a name="description"></a>Description

Bu hizmet, var olan bir LWM2M Istemcisine bağlı yeni bir LWM2M Istemci oturumu oluşturur. Oturum, bir önyükleme sunucusuyla veya bir LWM2M sunucusuyla iletişim kurmak için LWM2M Istemcisi tarafından kullanılır.

Uygulama, oturumun durumu güncellendiği zaman çağrılacak bir geri çağırma işlevi sağlamalıdır.

### <a name="parameters"></a>Parametreler

- **session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.
- **client_ptr**: daha önce oluşturulan LWM2M istemcisine yönelik işaretçi.
- **state_callback**: oturumun durumu değiştiğinde çağrılan uygulama geri çağırması.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_delete"></a>nx_lwm2m_client_session_delete

LWM2M Istemci oturumunu Sil

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_delete(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir LWM2M Istemci oturumunu siler.

Nx_lwm2m_client_delete çağırarak bir LWM2M Istemcisi silindiğinde, istemciye bağlı tüm oturumlar da silinir.

### <a name="parameters"></a>Parametreler

- **session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_deregister"></a>nx_lwm2m_client_session_deregister

LWM2M sunucusu ile bir oturumu sonlandırma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_deregister(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir LWM2M sunucusuna ' de Register ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_NOT_REGISTERED**: istemci sunucuya kayıtlı değil.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_error_get"></a>nx_lwm2m_client_session_error_get

Bir oturumun son hatasını al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_error_get(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet, oturum hata durumuna geldiğinde oturumun hata kodunu döndürür.

### <a name="parameters"></a>Parametreler

- **session_ptr:** LWM2M İstemci Oturumu denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Oturum hata durumda değil.
- **NX_LWM2M_ADDRESS_ERROR:** Geçersiz sunucu adresi.
- **NX_LWM2M_BUFFER_TOO_SMALL:** İstek yükü ağ arabelleğine sığmıyor.
- **NX_LWM2M_DTLS_ERROR:** Sunucuyla güvenli bağlantı kurulamadı.
- **NX_LWM2M_ERROR:** Belirtilmeyen hata.
- **NX_LWM2M_FORBIDDEN:** Sunucu tarafından kayıt reddedildi.
- **NX_LWM2M_NOT_FOUND:** İstemci güncelleştiriliyor/kaydı kaldırıyorken sunucu tarafından bulunamadı.
- **NX_LWM2M_SERVER_INSTANCE_DELETED:** Oturuma karşılık gelen Sunucu Nesne Örneği silindi.
- **NX_LWM2M_TIMED_OUT:** Sunucudan yanıt yok.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_register"></a>nx_lwm2m_client_session_register

LWM2M Sunucusu ile oturum başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_register(NX_LWM2M_CLIENT_SESSION *session_ptr,
                    NX_LWM2M_ID server_id, ULONG ip_address, UINT port);
```

### <a name="description"></a>Description

Bu hizmet bir LWM2M Sunucusuna 'Kaydetme' işlemi gerçekleştirir. Sunucunun Sunucu Nesnesi'ne karşılık gelen bir sunucu örneği olması gerekir.

Kayıt başarılı olursa LWM2M İstemcisi, sunucudan diğer işlemleri işler ve istemci kaydı geri alınıncaya kadar düzenli aralıklarla 'Güncelleştirme' iletileri gönderir.

Geçerli etkin oturumlar bu çağrı tarafından iptal edilir ve yeni LWM2M Sunucusu oturumuyla değiştirilir.

### <a name="parameters"></a>Parametreler

- **session_ptr:** LWM2M İstemci Oturumu denetim bloğuna işaretçi.
- **server_id:** LWM2M Sunucusunun Kısa Sunucu Kimliği.
- **ip_address:** Sunucunun IP adresi.
- **bağlantı** noktası: Sunucunun UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem..
- **NX_LWM2M_NOT_FOUND:** Kısa Sunucu Kimliğine karşılık gelen Sunucu Nesnesi örneği yok.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_register_dtls"></a>nx_lwm2m_client_session_register_dtls

LWM2M Sunucusu ile güvenli bir oturum başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_register_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID server_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a>Description

Bu hizmet, güvenli bir DTLS bağlantısı kullanarak LWM2M Sunucusuna 'Kaydetme' işlemi gerçekleştirir. Sunucunun Sunucu Nesnesi'ne karşılık gelen bir sunucu örneği olması gerekir.

Bu işlevi çağırmadan önce DTLS oturumunun uygun şifre paketleri ve anahtar malzemeleriyle yapılandırılmış olması gerekir. NX_SECURE_ENABLE_DTLS tanımlanmalıdır.

Her DTLS oturumu iletişim için kendi UDP yuvasını kullanır, bu nedenle dtls_local_port güvenli oturumlar oluşturursa yerel bağlantı noktası dtls_local_port her oturum için farklı olması gerekir.

Kayıt başarılı olursa LWM2M İstemcisi, sunucudan diğer işlemleri işler ve istemci kaydı geri alınıncaya kadar düzenli aralıklarla 'Güncelleştirme' iletileri gönderir.

Geçerli etkin oturumlar bu çağrı tarafından iptal edilir ve yeni LWM2M Sunucusu oturumuyla değiştirilir.

### <a name="parameters"></a>Parametreler

- **session_ptr:** LWM2M İstemci Oturumu denetim bloğuna işaretçi.
- **server_id:** LWM2M Sunucusunun Kısa Sunucu Kimliği.
- **ip_address:** Sunucunun IP adresi.
- **bağlantı** noktası: Sunucunun UDP bağlantı noktası.
- **dtls_session_ptr:** LWM2M oturumu için kullanmak üzere DTLS oturumu.
- **dtls_local_port:** DTLS oturumu için kullanılan yerel UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_NOT_FOUND:** Kısa Sunucu Kimliğine karşılık gelen Sunucu Nesnesi örneği yok.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_update"></a>nx_lwm2m_client_session_update

LWM2M Sunucusu ile oturum güncelleştirme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Description

Bu hizmet LWM2M Sunucusuna bir 'Güncelleştirme' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **session_ptr:** LWM2M İstemci Oturumu denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_NOT_REGISTERED:** İstemci sunucuya kayıtlı değil.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_client_unlock"></a>nx_lwm2m_client_unlock

LWM2M İstemcisi'nin Kilidini Açma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, nx_lwm2m_client_unlock() çağrısıyla kilitlenmiş LWM2M İstemcisi'nin kilidini nx_lwm2m_client_unlock.

### <a name="parameters"></a>Parametreler

- **client_ptr:** LWM2M İstemci denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_firmware_create"></a>nx_lwm2m_firmware_create

Üretici Yazılımı Güncelleştirme Nesnesi Oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_firmware_create(NX_LWM2M_FIRMWARE *firmware_ptr,
    NX_LWM2M_CLIENT *client_ptr, UINT protocols,
    NX_LWM2M_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_FIRMWARE_UPDATE_CALLBACK update_callback);
```

### <a name="description"></a>Description

Bu hizmet bir Üretici Yazılımı Güncelleştirme Nesnesi başlatıyor ve Nesneyi daha önce oluşturulmuş bir LWM2M İstemcisi'ne ekliyor. Üretici Yazılımı Güncelleştirme Nesnesi, LWM2M Sunucusu ile iletişim kurmak için kaynakları uygulamaya alır, ancak uygulamanın üretici yazılımında gerçek işlemleri uygulamak için geri çağırmalar sağlaması gerekir (üretici yazılımını yükleme, depolama ve güncelleştirme).

Protocols parametresi, 'Package URI' kaynağıyla üretici yazılımını almak için uygulama tarafından hangi protokollerin desteklen olduğunu belirtir; aşağıdaki bayraklar tanımlanmıştır:

NX_LWM2M_FIRMWARE_PROTOCOL_COAP, NX_LWM2M_FIRMWARE_PROTOCOL_COAPS, NX_LWM2M_FIRMWARE_PROTOCOL_HTTP, NX_LWM2M_FIRMWARE_PROTOCOL_HTPPS.

### <a name="parameters"></a>Parametreler

- **firmware_ptr:** Üretici Yazılımı Nesnesi denetim bloğuna işaretçi.
- **client_ptr:** Önceden oluşturulmuş LWM2M İstemcisi'nin işaretçisi.
- **protokoller:** Paket URI kaynağı tarafından desteklenen protokolleri gösteren bayraklar.
- **package_callback:** NULL [TBD] olmalıdır.
- **package_uri_callback:** Paket URI kaynağını uygulamak için kullanılan geri çağırma.
- **update_callback:** Güncelleştirme kaynağını uygulamak için kullanılan geri çağırma.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- NX_PTR_ERROR: Geçersiz işaretçi.

## <a name="nx_lwm2m_firmware_package_info_set"></a>nx_lwm2m_firmware_package_info_set

Üretici Yazılımı Güncelleştirme Paketi Bilgilerini Ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_firmware_package_info_set(NX_LWM2M_FIRMWARE *firmware_ptr,
                                const CHAR *name, const CHAR *version);
```

### <a name="description"></a>Description

Bu hizmet, Üretici Yazılımı Güncelleştirme Nesnesi'nin 'PkgName' (6) ve 'PkgVersion' (7) kaynaklarının değerlerini değiştirir.

### <a name="parameters"></a>Parametreler

- **firmware_ptr:** Üretici Yazılımı Güncelleştirme Nesnesinin İşaretçisi.
- **name:** Paket Adı'nın yeni değeri.
- **Sürüm**: paket sürümünün yeni değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_firmware_result_set"></a>nx_lwm2m_firmware_result_set

Bellenim güncelleştirme sonucunu ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_firmware_result_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR result);
```

### <a name="description"></a>Description

Bu hizmet, bellenim güncelleştirme nesnesinin ' güncelleştirme sonucu ' (5) kaynağının değerini değiştirir.

### <a name="parameters"></a>Parametreler

- **firmware_ptr**: bellenim güncelleştirme nesnesine yönelik işaretçi.
- **sonuç**: güncelleştirme sonucu kaynağının yeni değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_firmware_state_set"></a>nx_lwm2m_firmware_state_set

Üretici yazılımı güncelleştirme durumunu ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_firmware_state_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR state);
```

### <a name="description"></a>Description

Bu hizmet, bellenim güncelleştirme nesnesinin ' durum ' (3) kaynağının değerini değiştirir.

### <a name="parameters"></a>Parametreler

- **firmware_ptr**: bellenim güncelleştirme nesnesine yönelik işaretçi.
- **durum**: durum kaynağının yeni değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_object_resource_changed"></a>nx_lwm2m_object_resource_changed

Bir nesne örneğinin kaynak değeri için sinyal değişikliği

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_object_resource_changed(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Description

Bu hizmet bir nesne uygulama tarafından, kaynak değerinden birinin değiştiğini LWM2M Istemcisine işaret etmek için kullanılır. LWM2M Istemcisi, kaynak bir LWM2M sunucusu tarafından gözlemleniyorsa bir bildirim gönderir.

### <a name="parameters"></a>Parametreler

- **object_ptr**: nesne uygulamasına yönelik işaretçi.
- **instance_ptr**: nesne örneğine yönelik işaretçi.
- **kaynak**: değiştirilen kaynağı açıklayan yapıya yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_resource_get_boolean"></a>nx_lwm2m_resource_get_boolean

Boole kaynağının değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_boolean(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a>Description

Hizmet bir Boole kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **değer**: kaynak değer açıklamasına yönelik işaretçi.
- **bool_ptr**: hedef Boolean değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_ENCODING**: kaynak değeri bir Boole değeri değil.

## <a name="nx_lwm2m_resource_get_float32"></a>nx_lwm2m_resource_get_float32

32 bitlik kayan nokta kaynağının değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_float32(const NX_LWM2M_RESOURCE *value,
                                NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a>Description

Hizmet, 32 bitlik bir kayan nokta kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **değer**: kaynak değer açıklamasına yönelik işaretçi.
- **float32_ptr**: hedef 32 bit kayan nokta değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_ENCODING**: kaynak değeri bir kayan nokta değeri değil.

## <a name="nx_lwm2m_resource_get_float64"></a>nx_lwm2m_resource_get_float64

64 bitlik kayan nokta kaynağının değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_float64(const NX_LWM2M_RESOURCE *value,
                                NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a>Description

Hizmet, 64 bitlik bir kayan nokta kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **değer**: kaynak değer açıklamasına yönelik işaretçi.
- **float64_ptr**: hedef 64 bit kayan nokta değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_ENCODING**: kaynak değeri bir kayan nokta değeri değil.

## <a name="nx_lwm2m_resource_get_integer32"></a>nx_lwm2m_resource_get_integer32

32 bitlik bir tamsayı kaynağının değerini alır

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_integer32(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a>Description

Hizmet, 32 bitlik bir tamsayı kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **değer**: kaynak değer açıklamasına yönelik işaretçi.
- **int32_ptr**: hedef 32-bit tamsayı değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_ENCODING**: kaynak değeri bir tamsayı değer değil veya tamsayı değeri 32 bitlik bir numaraya uymuyor.

## <a name="nx_lwm2m_resource_get_integer64"></a>nx_lwm2m_resource_get_integer64

64 bitlik bir tamsayı kaynağının değerini alır

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_integer64(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a>Description

Hizmet, 64 bitlik bir tamsayı kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **değer**: kaynak değer açıklamasına yönelik işaretçi.
- **int64_ptr**: hedef 64-bit tamsayı değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_ENCODING**: kaynak değeri bir tamsayı değeri değil.

## <a name="nx_lwm2m_resource_get_objlnk"></a>nx_lwm2m_resource_get_objlnk

Nesne bağlantı kaynağının değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_objlnk(const NX_LWM2M_RESOURCE *value,
                                    NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a>Description

Hizmet, bir nesne bağlantı kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **value:** Kaynak değeri açıklama işaretçisi.
- **objlnk_ptr:** Hedef Nesne Bağlantısı değerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_ENCODING:** Kaynak değeri bir Nesne Bağlantısı değeri değildir.

## <a name="nx_lwm2m_resource_get_opaque"></a>nx_lwm2m_resource_get_opaque

Opak Kaynağın değerini al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_opaque(const NX_LWM2M_RESOURCE *value,
            const VOID **opaque_ptr_ptr, UINT *opaque_length_ptr);
```

### <a name="description"></a>Description

Hizmet, Opak Bir Kaynağın değerini verir.

Opak bir kaynak değeri, bir arabellek işaretçisi ve bir uzunluktan oluşur.

### <a name="parameters"></a>Parametreler

- **value:** Kaynak değeri açıklama işaretçisi.
- **opaque_ptr_ptr:** Hedef opak arabellek işaretçisinin işaretçisi.
- **opaque_length_ptr:** Hedef opak arabellek uzunluğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_ENCODING:** Kaynak değeri Opak bir değer değildir.

## <a name="nx_lwm2m_resource_get_string"></a>nx_lwm2m_resource_get_string

Dize Kaynağının değerini alır

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_string(const NX_LWM2M_RESOURCE *value,
            const CHAR **string_ptr_ptr, UINT *string_length_ptr);
```

### <a name="description"></a>Description

Hizmet, dize kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **value:** Kaynak değeri açıklama işaretçisi.
- **string_ptr_ptr:** Hedef dize işaretçisinin işaretçisi.
- **string_length_ptr:** Hedef dize uzunluğunun işaretçisi. Dize null sonlandırılırsa NULL olabilir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_ENCODING:** Kaynak değeri bir Dize değeri değildir.

## <a name="nx_lwm2m_resource_multiple_get_boolean"></a>nx_lwm2m_resource_multiple_get_boolean

Boole Kaynağı Birden Çok Kaynak Örneğinin değerini al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_boolean(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a>Description

Hizmet, Birden Çok Kaynak'tan Boole Kaynak Örneği'nin değerini verir.

### <a name="parameters"></a>Parametreler

- **value:** Birden Çok Kaynak değeri açıklamasının işaretçisi.
- **index:** Kaynak değeri dizisinde alınan Örneğin dizini.
- **instance_id_ptr:** Hedef Örnek Kimliğine işaretçi.
- **bool_ptr:** Hedef Boole değerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER:** Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING:** Kaynak birden çok kaynak değildir veya kaynak değeri bir Boole değeri değildir.

## <a name="nx_lwm2m_resource_multiple_get_float32"></a>nx_lwm2m_resource_multiple_get_float32

32 bit Kayan Nokta Birden Çok Kaynak Örneğinin değerini al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_float32(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a>Description

Hizmet, 32 bit Kayan Nokta Kaynak Örneğinin değerini Birden Çok Kaynaktan almaktadır.

### <a name="parameters"></a>Parametreler

- **value:** Birden Çok Kaynak değeri açıklamasının işaretçisi.
- **index:** Kaynak değeri dizisinde alınan Örneğin dizini.
- **instance_id_ptr:** Hedef Örnek Kimliğine işaretçi.
- **float32_ptr:** Hedef 32 Bit Kayan Nokta değerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER:** Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING:** Kaynak birden çok kaynak değildir veya kaynak değeri Kayan Nokta değeri değildir.

## <a name="nx_lwm2m_resource_multiple_get_float64"></a>nx_lwm2m_resource_multiple_get_float64

64 bit Kayan Nokta Birden Çok Kaynak Örneğinin değerini al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_float64(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a>Description

Hizmet, 64 bit Kayan Nokta Kaynak Örneğinin değerini Birden Çok Kaynaktan almaktadır.

### <a name="parameters"></a>Parametreler

- **value:** Birden Çok Kaynak değeri açıklamasının işaretçisi.
- **index:** Kaynak değeri dizisinde alınan Örneğin dizini.
- **instance_id_ptr:** Hedef Örnek Kimliğine işaretçi.
- **float64_ptr:** Hedef 64 Bit Kayan Nokta değerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER:** Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING:** Kaynak birden çok kaynak değildir veya kaynak değeri Kayan Nokta değeri değildir.

## <a name="nx_lwm2m_resource_multiple_get_integer32"></a>nx_lwm2m_resource_multiple_get_integer32

32 Bit Tamsayı Birden Çok Kaynak Örneğinin değerini elde eder

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_integer32(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a>Description

Hizmet, 32 Bit Tamsayı Kaynak Örneğinin değerini Birden Çok Kaynaktan döndürür.

### <a name="parameters"></a>Parametreler

- **value:** Birden Çok Kaynak değeri açıklamasının işaretçisi.
- **index:** Kaynak değeri dizisinde alınan Örneğin dizini.
- **instance_id_ptr:** Hedef Örnek Kimliğine işaretçi.
- **int32_ptr:** Hedef 32 Bit Tamsayı değerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER:** Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING:** Kaynak birden çok kaynak değildir veya kaynak değeri bir Tamsayı değeri değildir veya Tamsayı değeri 32 Bit sayıya sığmaz.

## <a name="nx_lwm2m_resource_multiple_get_integer64"></a>nx_lwm2m_resource_multiple_get_integer64

64 Bit Tamsayı Birden Çok Kaynak Örneğinin değerini elde eder

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_integer64(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a>Description

Hizmet, 64 Bit Tamsayı Kaynak Örneğinin değerini Birden Çok Kaynaktan döndürür.

### <a name="parameters"></a>Parametreler

- **value:** Birden Çok Kaynak değeri açıklamasının işaretçisi.
- **index:** Kaynak değeri dizisinde alınan Örneğin dizini.
- **instance_id_ptr:** Hedef Örnek Kimliğine işaretçi.
- **int64_ptr:** Hedef 64 Bit Tamsayı değerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER:** Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING:** Kaynak birden çok kaynak değildir veya kaynak değeri bir Tamsayı değeri değildir.

## <a name="nx_lwm2m_resource_multiple_get_objlnk"></a>nx_lwm2m_resource_multiple_get_objlnk

Nesne Bağlantısı Birden Çok Kaynak Örneğinin değerini elde edin

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_objlnk(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a>Description

Hizmet, Bir Nesne Bağlantısı Kaynak Örneği'nin değerini Birden Çok Kaynaktan almaktadır.

### <a name="parameters"></a>Parametreler

- **value:** Birden Çok Kaynak değeri açıklamasının işaretçisi.
- **index:** Kaynak değeri dizisinde alınan Örneğin dizini.
- **instance_id_ptr:** Hedef Örnek Kimliğine işaretçi.
- **objlnk_ptr:** Hedef Nesne Bağlantısı değerinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER:** Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING:** Kaynak birden çok kaynak değil veya kaynak değeri bir Nesne Bağlantısı değeri değil.

## <a name="nx_lwm2m_resource_multiple_get_opaque"></a>nx_lwm2m_resource_multiple_get_opaque

Opak Birden Çok Kaynak Örneğinin değerini al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_opaque(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const VOID **opaque_ptr_ptr,
    UINT *opaque_length_ptr);
```

### <a name="description"></a>Description

Hizmet, Birden Çok Kaynaktan Opak Bir Kaynak Örneğinin değerini verir.

Opak bir kaynak değeri, bir arabellek işaretçisi ve bir uzunluktan oluşur.

### <a name="parameters"></a>Parametreler

- **value:** Birden Çok Kaynak değeri açıklamasının işaretçisi.
- **index:** Kaynak değeri dizisinde alınan Örneğin dizini.
- **instance_id_ptr:** Hedef Örnek Kimliğine işaretçi.
- **opaque_ptr_ptr:** Hedef opak arabellek işaretçisinin işaretçisi.
- **opaque_length_ptr:** Hedef opak arabellek uzunluğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER:** Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING:** Kaynak birden çok kaynak değildir veya kaynak değeri opak bir değer değildir.

## <a name="nx_lwm2m_resource_multiple_get_string"></a>nx_lwm2m_resource_multiple_get_string

Bir Dize Birden Çok Kaynak Örneğinin değerini alır

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_string(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const CHAR **string_ptr_ptr,
    UINT *string_length_ptr);
```

### <a name="description"></a>Description

Hizmet, Bir Dize Kaynağı Örneğinin değerini Birden Çok Kaynaktan alır.

### <a name="parameters"></a>Parametreler

- **value:** Birden Çok Kaynak değeri açıklamasının işaretçisi.
- **index:** Kaynak değeri dizisinde alınan Örneğin dizini.
- **instance_id_ptr:** Hedef Örnek Kimliğine işaretçi.
- **string_ptr_ptr:** Hedef dize işaretçisinin işaretçisi.
- **string_length_ptr:** Hedef dize uzunluğunun işaretçisi. Dize null sonlandırılırsa NULL olabilir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:** Başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER:** Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING:** Kaynak birden çok kaynak değildir veya örnek değeri bir Dize değeri değildir.
