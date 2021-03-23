---
title: Bölüm 4-Azure RTOS NetX LWM2M Services açıklaması
description: Bu bölüm, tüm Azure RTOS NetX LWM2M hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d5a402790387c2720db304fe93d74252494d7638
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826674"
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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisi tarafından işlenmeyen LWM2M cihaz nesnesi kaynaklarına işlem uygulamak için uygulama geri çağırmaları yüklüyor.

LWM2M Istemcisi şu kaynakları uygular: hata kodu (11), sıfırlama hata kodu (12) ve desteklenen bağlama ve modlar (16), diğer kaynaklara yönelik işlemler uygulamaya yeniden yönlendirilir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **read_callback**: ' Read ' metodu geri çağırması.
- **discover_callback**: ' keşfet ' metodu geri çağırması.
- **write_callback**: ' Write ' metodu geri çağırması.
- **execute_callback**: ' Execute ' metodu geri çağırması.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_device_error_push"></a>nx_lwm2m_client_device_error_push

Cihaz nesnesine hata kodu ekle

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_error_push(NX_LWM2M_CLIENT *client_ptr, UCHAR code);
```

### <a name="description"></a>Açıklama

Bu hizmet, nesne cihazının hata kodu (11) kaynağına yeni bir örnek ekler.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **kod**: yeni hata kodu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BUFFER_TOO_SMALL**: en fazla depolanan hata kodu sayısına ulaşıldı.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_device_error_reset"></a>nx_lwm2m_client_device_error_reset

Cihaz nesnesinin hata kodlarını Sıfırla

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, tüm hata kodu kaynak örneklerini cihaz nesnesinden siler. Bu, kaynak sıfırlama hata kodunu (12) çalıştırmaya eşdeğerdir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_device_resource_changed"></a>nx_lwm2m_client_device_resource_changed

Cihaz nesnesi kaynağının sinyal değişikliği

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_device_resource_changed(NX_LWM2M_CLIENT *client_ptr,
                                    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a>Açıklama

Hizmet, uygulama tarafından, nesne cihazının bir kaynağının değiştiği LWM2M Istemcisine işaret etmek için kullanılır. LWM2M Istemcisi, kaynak bir LWM2M sunucusu tarafından gözlemleniyorsa bir bildirim gönderir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **kaynak**: değiştirilen kaynağı açıklayan yapıya yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_lock"></a>nx_lwm2m_client_lock

LWM2M Istemcisini kilitle

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_lock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M nesnelerine sunuculardan veya başka bir uygulama iş parçacığından sürekli erişimi engellemek için LWM2M Istemcisini kilitler.

LWM2M Istemcisi Şu anda başka bir iş parçacığı tarafından kilitliyse, LWM2M Istemcisinin kilidi açana kadar işlev engellenir.

Nx_lwm2m_client_lock ()/nx_lwm2m_client_unlock () çiftlerine yapılan çağrılar iç içe olabilir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_add"></a>nx_lwm2m_client_object_add

LWM2M Istemcisine nesne uygulamasını ekleme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_add(NX_LWM2M_CLIENT *client_ptr,
                                NX_LWM2M_OBJECT *object_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisine yeni bir nesne uygulamasını ekler.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **object_ptr**: nesne uygulamasını tanımlayan yapıya yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_ALREADY_EXIST**: nesne kimliği zaten var.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_create"></a>nx_lwm2m_client_object_create

Yeni bir nesne örneği oluştur

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_create(NX_LWM2M_CLIENT *client_ptr,
            NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr,
            UINT num_values, const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, yeni bir nesne örneği oluşturmak için LWM2M Istemcisinin bir nesnesi üzerinde bir ' Create ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **object_id**: nesne kimliği.
- **instance_id_ptr**: LWM2M Istemcisinin BIR örnek kimliği ataması gerekiyorsa, yenı örneğin kimliğine YÖNELIK işaretçi null olabilir. KIMLIK ayrılmış 65535 ise, LWM2M Istemcisi bir örnek KIMLIĞI atayacaktır. NULL değilse, çağrının ardından atanan KIMLIK döndürülür.
- **num_values**: ayarlanacak değer sayısı.
- **values_ptr**: yeni nesne örneğini başlatmak için kaynak değerleri dizisine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_ALREADY_EXIST**: nesne örneği kimliği zaten var.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: nesne, örnek oluşturmayı desteklemiyor.
- **NX_LWM2M_NO_MEMORY**: yeni örneği depolamak için bellek ayrılamıyor.
- **NX_LWM2M_NOT_FOUND**: nesne kimliği yok.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_delete"></a>nx_lwm2m_client_object_delete

Bir nesne örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_delete(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin nesne örneği üzerinde bir ' DELETE ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **object_id**: nesne kimliği.
- **instance_id**: nesne örneği kimliği.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: nesne, örnek silmeyi desteklemiyor.
- **NX_LWM2M_NOT_FOUND**: nesne kimliği veya nesne örneği kimliği yok.
- Geçersiz NX_PTR_ERROR işaretçisi.

## <a name="nx_lwm2m_client_object_discover"></a>nx_lwm2m_client_object_discover

Bir nesne örneğinin kaynaklarını bulma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_discover(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT *num_resources_ptr, NX_LWM2M_RESOURCE_INFO *resources_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde bir ' bul ' işlemi gerçekleştirir, bu, nesne tarafından uygulanan kaynakların listesini döndürür.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **object_id**: nesne kimliği.
- **instance_id**: nesne örneği kimliği.
- **num_resources_ptr**: giriş, hedef arabelleğin boyutunun çıktıda, arabelleğe yazıldı.
- **resources_ptr**: hedef arabelleğin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem..
- **NX_LWM2M_BUFFER_TOO_SMALL**: kaynak arabelleği, kaynak listesini depolamak için çok küçük.
- **NX_LWM2M_NOT_FOUND**: nesne kimliği veya nesne örneği kimliği yok.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_execute"></a>nx_lwm2m_client_object_execute

Bir nesne örneğinin kaynağını yürütün

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_execute(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr, UINT arguments_length);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin nesne örneği kaynağında ' Execute ' işlemini gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **object_id**: nesne kimliği.
- **instance_id**: nesne örneği kimliği.
- **resource_id**: kaynak kimliği.
- **arguments_ptr**: yürütme işleminin bağımsız değişkenlerine yönelik işaretçi. Arguments_length sıfırsa NULL olabilir.
- **arguments_length**: bağımsız değişkenlerin uzunluğu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: kaynak yürütme işlemini desteklemiyor.
- **NX_LWM2M_NOT_FOUND**: nesne kimliği, nesne örneği kimliği veya kaynak kimliği yok.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_get_next"></a>nx_lwm2m_client_object_get_next

LWM2M Istemcisi tarafından uygulanan nesne listesini al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_get_next(NX_LWM2M_CLIENT *client_ptr,
                                    NX_LWM2M_ID *object_id_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisi tarafından uygulanan bir sonraki nesnenin KIMLIĞINI döndürür. Geçerli nesne KIMLIĞI NX_LWM2M_RESERVED_ID olarak ayarlandıysa (65535) ilk nesne KIMLIĞI döndürülür.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **object_id_ptr**: GEÇERLI nesne kimliğine yönelik işaretçi. Dönüşte, LWM2M Istemcisi tarafından uygulanan bir sonraki nesne KIMLIĞINI içerir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem..
- **NX_LWM2M_NOT_FOUND**: VERILEN nesne kimliği veritabanının son sayısıdır.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_instance_get_next"></a>nx_lwm2m_client_object_instance_get_next

Bir nesnenin örneklerinin listesini al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_instance_get_next(NX_LWM2M_CLIENT *client_ptr,
                    NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen nesnenin sonraki nesne örneğinin KIMLIĞINI döndürür. Geçerli örnek KIMLIĞI NX_LWM2M_RESERVED_ID olarak ayarlandıysa (65535) ilk Örneğin KIMLIĞI döndürülür.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **object_id**: nesne kimliği.
- **instance_id_ptr**: geçerli nesne örneği kimliğine yönelik işaretçi. Dönüş sırasında nesnenin sonraki örnek KIMLIĞINI içerir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem..
- **NX_LWM2M_NOT_FOUND**: VERILEN örnek kimliği nesnenin son, veya nesne kimliği uygulanmadı.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_read"></a>nx_lwm2m_client_object_read

Bir nesne örneğinin kaynak değerlerini oku

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_read(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT num_values, NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde ' Read ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **object_id**: nesne kimliği.
- **instance_id**: nesne örneği kimliği.
- **num_values**: okunacak kaynak sayısı.
- **values_ptr**: okunacak kaynakların kimliklerini içeren bir NX_LWM2M_RESOURCE dizisine yönelik işaretçi. Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_METHOD_NOT_ALLOWED**: bir kaynak okuma işlemini desteklemiyor.
- **NX_LWM2M_NOT_FOUND**: nesne kimliği, nesne örneği kimliği veya kaynak kimliği yok.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_object_write"></a>nx_lwm2m_client_object_write

Bir nesne örneğinin kaynak değerlerini değiştirme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_object_write(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, UINT num_values,
        const NX_LWM2M_RESOURCE *values_ptr, UINT write_op);
```

### <a name="description"></a>Açıklama

Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde ' Write ' işlemi gerçekleştirir.

*Write_op* parametresine aşağıdaki yazma işlemleri de belirtilebilir:

- **0** &mdash; Kısmi güncelleştirme: yeni değerde belirtilen kaynakları ekler veya güncelleştirir ve diğer mevcut kaynakları değiştirmeden bırakır,

- **NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Örnek Değiştir: nesne örneğini, yeni sağlanmış kaynak değerleriyle değiştirir.

- **NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Kaynağı değiştir: kaynakları, belirtilen yeni kaynak değerleriyle (birden çok kaynağı değiştirmek için kullanılır) değiştirir.

- **NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Önyükleme yazma: bir önyükleme dizisinin çağrısını gösterir.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.
- **object_id**: nesne kimliği.
- **instance_id**: nesne örneği kimliği.
- **num_values**: yazılacak kaynak sayısı.
- **values_ptr**: kaynak kimliklerini, türleri ve yazılacak değerleri içeren bir NX_LWM2M_RESOURCE dizisine yönelik işaretçi.
- **write_op**: yazma işlemi türü.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

Bu hizmet, oturum bir hata durumundayken oturumun hata kodunu döndürür.

### <a name="parameters"></a>Parametreler

- **session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: oturum hata durumunda değil.
- **NX_LWM2M_ADDRESS_ERROR**: geçersiz sunucu adresi.
- **NX_LWM2M_BUFFER_TOO_SMALL**: istek yükü ağ arabelleğine uymuyor.
- **NX_LWM2M_DTLS_ERROR**: sunucuyla güvenli bağlantı kurulamadı.
- **NX_LWM2M_ERROR**: belirtilmeyen hata.
- **NX_LWM2M_FORBIDDEN**: kayıt sunucu tarafından reddedildi.
- **NX_LWM2M_NOT_FOUND**: güncelleştirme/kaydını kaldırmak, istemci sunucu tarafından bulunamadı.
- **NX_LWM2M_SERVER_INSTANCE_DELETED**: oturuma karşılık gelen sunucu nesnesi örneği silindi.
- **NX_LWM2M_TIMED_OUT**: sunucudan yanıt yok.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_register"></a>nx_lwm2m_client_session_register

LWM2M sunucusu ile oturum başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_register(NX_LWM2M_CLIENT_SESSION *session_ptr,
                    NX_LWM2M_ID server_id, ULONG ip_address, UINT port);
```

### <a name="description"></a>Açıklama

Bu hizmet bir LWM2M sunucusuna ' Register ' işlemi gerçekleştirir. Sunucu, sunucu nesnesinde karşılık gelen bir sunucu örneğine sahip olmalıdır.

Kayıt başarılı olursa, LWM2M Istemcisi sunucudan daha fazla işlem gerçekleştirir ve istemci kayıtlı olana kadar düzenli olarak ' güncelleştirme ' iletileri gönderir.

Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni LWM2M Server oturumu tarafından değiştirilmiştir.

### <a name="parameters"></a>Parametreler

- **session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.
- **server_id**: LWM2M sunucusunun kısa sunucu kimliği.
- **ip_address**: sunucunun IP adresi.
- **bağlantı noktası**: sunucunun UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem..
- **NX_LWM2M_NOT_FOUND**: kısa sunucu kimliğine karşılık gelen sunucu nesnesi örneği yok.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_register_dtls"></a>nx_lwm2m_client_session_register_dtls

LWM2M sunucusu ile güvenli bir oturum başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_register_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID server_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a>Açıklama

Bu hizmet, güvenli bir DTLS bağlantısı kullanarak bir LWM2M sunucusuna ' Register ' işlemi gerçekleştirir. Sunucu, sunucu nesnesinde karşılık gelen bir sunucu örneğine sahip olmalıdır.

DTLS oturumunun, bu işlev çağrılmadan önce uygun şifre paketleri ve anahtar malzemeyle yapılandırılmış olması gerekir. NX_SECURE_ENABLE_DTLS tanımlanmalıdır.

Her DTLS oturumu, iletişim için kendi UDP yuvasını kullanır, bu nedenle uygulama birkaç güvenli oturum oluşturduğunda her oturum için yerel bağlantı noktası dtls_local_port farklı olmalıdır.

Kayıt başarılı olursa, LWM2M Istemcisi sunucudan daha fazla işlem gerçekleştirir ve istemci kayıtlı olana kadar düzenli olarak ' güncelleştirme ' iletileri gönderir.

Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni LWM2M Server oturumu tarafından değiştirilmiştir.

### <a name="parameters"></a>Parametreler

- **session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.
- **server_id**: LWM2M sunucusunun kısa sunucu kimliği.
- **ip_address**: sunucunun IP adresi.
- **bağlantı noktası**: sunucunun UDP bağlantı noktası.
- **dtls_session_ptr**: LWM2M oturumu için kullanılacak DTLS oturumu.
- **dtls_local_port**: DTLS oturumu için kullanılan yerel UDP bağlantı noktası.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_NOT_FOUND**: kısa sunucu kimliğine karşılık gelen sunucu nesnesi örneği yok.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_session_update"></a>nx_lwm2m_client_session_update

LWM2M sunucusu ile oturum güncelleştirme

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir LWM2M sunucusuna ' Update ' işlemi gerçekleştirir.

### <a name="parameters"></a>Parametreler

- **session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_NOT_REGISTERED**: istemci sunucuya kayıtlı değil.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_client_unlock"></a>nx_lwm2m_client_unlock

LWM2M Istemcisinin kilidini aç

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, nx_lwm2m_client_unlock () çağrısıyla kilitlenmiş LWM2M Client previoulsy 'in kilidini açar.

### <a name="parameters"></a>Parametreler

- **client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_firmware_create"></a>nx_lwm2m_firmware_create

Bellenim güncelleştirme nesnesi oluştur

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_firmware_create(NX_LWM2M_FIRMWARE *firmware_ptr,
    NX_LWM2M_CLIENT *client_ptr, UINT protocols,
    NX_LWM2M_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_FIRMWARE_UPDATE_CALLBACK update_callback);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir bellenim güncelleştirme nesnesini başlatır ve nesneyi daha önce oluşturulmuş bir LWM2M Istemcisine ekler. Üretici yazılımı güncelleştirme nesnesi, bir LWM2M sunucusuyla iletişim kurmak için kaynakları uygular, ancak uygulamanın üretici yazılımında gerçek işlemleri uygulamak için geri çağrılar sağlaması gerekir (söz konusu bellenimi yükleme, depolama ve güncelleştirme).

Protocols parametresi, ' paket URI 'SI ' kaynağıyla bellenimi almak için uygulama tarafından hangi protokollerin desteklendiğini belirtir, aşağıdaki bayraklar tanımlanmıştır:

NX_LWM2M_FIRMWARE_PROTOCOL_COAP, NX_LWM2M_FIRMWARE_PROTOCOL_COAPS, NX_LWM2M_FIRMWARE_PROTOCOL_HTTP NX_LWM2M_FIRMWARE_PROTOCOL_HTPPS.

### <a name="parameters"></a>Parametreler

- **firmware_ptr**: bellenim nesne denetim bloğuna yönelik işaretçi.
- **client_ptr**: önceden oluşturulan LWM2M istemcisi işaretçisi.
- **protokoller**: paket URI 'si kaynağı tarafından hangi protokollerin desteklendiğini belirten bayraklar.
- **package_callback**: null [TBD] olmalıdır.
- **package_uri_callback**: paket URI kaynağını uygulamak için kullanılan geri çağırma.
- **update_callback**: güncelleştirme kaynağını uygulamak için kullanılan geri çağırma.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- NX_PTR_ERROR: geçersiz işaretçi.

## <a name="nx_lwm2m_firmware_package_info_set"></a>nx_lwm2m_firmware_package_info_set

Bellenim güncelleştirme paketi bilgilerini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_firmware_package_info_set(NX_LWM2M_FIRMWARE *firmware_ptr,
                                const CHAR *name, const CHAR *version);
```

### <a name="description"></a>Açıklama

Bu hizmet, bellenim güncelleştirme nesnesinin ' PkgName ' (6) ve ' PkgVersion ' (7) kaynaklarının değerlerini değiştirir.

### <a name="parameters"></a>Parametreler

- **firmware_ptr**: bellenim güncelleştirme nesnesine yönelik işaretçi.
- **ad**: paket adının yeni değeri.
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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

Hizmet, bir nesne bağlantı kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **değer**: kaynak değer açıklamasına yönelik işaretçi.
- **objlnk_ptr**: hedef nesne bağlantı değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_ENCODING**: kaynak değeri bir nesne bağlantı değeri değil.

## <a name="nx_lwm2m_resource_get_opaque"></a>nx_lwm2m_resource_get_opaque

Donuk bir kaynağın değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_opaque(const NX_LWM2M_RESOURCE *value,
            const VOID **opaque_ptr_ptr, UINT *opaque_length_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, donuk bir kaynağın değerini alır.

Donuk bir kaynak değeri, arabelleğin ve uzunluğun bir işaretçisinden oluşur.

### <a name="parameters"></a>Parametreler

- **değer**: kaynak değer açıklamasına yönelik işaretçi.
- **opaque_ptr_ptr**: hedef donuk arabellek işaretçisine yönelik işaretçi.
- **opaque_length_ptr**: hedef donuk arabellek uzunluğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_ENCODING**: kaynak değeri donuk bir değer değil.

## <a name="nx_lwm2m_resource_get_string"></a>nx_lwm2m_resource_get_string

Bir dize kaynağının değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_get_string(const NX_LWM2M_RESOURCE *value,
            const CHAR **string_ptr_ptr, UINT *string_length_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, bir dize kaynağının değerini alır.

### <a name="parameters"></a>Parametreler

- **değer**: kaynak değer açıklamasına yönelik işaretçi.
- **string_ptr_ptr**: hedef dize işaretçisine yönelik işaretçi.
- **string_length_ptr**: hedef dize uzunluğuna yönelik işaretçi. Dize null sonlandırılırsa NULL olabilir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_ENCODING**: kaynak değeri bir dize değeri değil.

## <a name="nx_lwm2m_resource_multiple_get_boolean"></a>nx_lwm2m_resource_multiple_get_boolean

Bir Boole kaynağı için birden çok kaynak örneği değeri alın

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_boolean(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, bir Boolean kaynak örneğinin değerini birden çok kaynaktan alır.

### <a name="parameters"></a>Parametreler

- **değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.
- **Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.
- **instance_id_ptr**: hedef örnek kimliği işaretçisi.
- **bool_ptr**: hedef Boolean değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir Boole değeri değil.

## <a name="nx_lwm2m_resource_multiple_get_float32"></a>nx_lwm2m_resource_multiple_get_float32

32 bitlik kayan nokta çoklu kaynak örneği değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_float32(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, 32 bitlik bir kayan nokta kaynak örneğinin değerini birden çok kaynaktan alır.

### <a name="parameters"></a>Parametreler

- **değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.
- **Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.
- **instance_id_ptr**: hedef örnek kimliği işaretçisi.
- **float32_ptr**: hedef 32 bit kayan nokta değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir kayan nokta değeri değil.

## <a name="nx_lwm2m_resource_multiple_get_float64"></a>nx_lwm2m_resource_multiple_get_float64

64 bitlik kayan nokta çoklu kaynak örneği değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_float64(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, 64 bitlik bir kayan nokta kaynak örneğinin değerini birden çok kaynaktan alır.

### <a name="parameters"></a>Parametreler

- **değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.
- **Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.
- **instance_id_ptr**: hedef örnek kimliği işaretçisi.
- **float64_ptr**: hedef 64 bit kayan nokta değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir kayan nokta değeri değil.

## <a name="nx_lwm2m_resource_multiple_get_integer32"></a>nx_lwm2m_resource_multiple_get_integer32

32 bitlik bir tamsayı birden çok kaynak örneğinin değerini alır

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_integer32(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, 32 bitlik bir tamsayı kaynak örneğinin değerini birden çok kaynaktan alır.

### <a name="parameters"></a>Parametreler

- **değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.
- **Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.
- **instance_id_ptr**: hedef örnek kimliği işaretçisi.
- **int32_ptr**: hedef 32-bit tamsayı değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir tamsayı değer değil veya tamsayı değeri 32 bitlik bir numaraya uymuyor.

## <a name="nx_lwm2m_resource_multiple_get_integer64"></a>nx_lwm2m_resource_multiple_get_integer64

64 bitlik bir tamsayı birden çok kaynak örneğinin değerini alır

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_integer64(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, 64 bitlik bir tamsayı kaynak örneğinin değerini birden çok kaynaktan alır.

### <a name="parameters"></a>Parametreler

- **değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.
- **Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.
- **instance_id_ptr**: hedef örnek kimliği işaretçisi.
- **int64_ptr**: hedef 64-bit tamsayı değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir tamsayı değeri değil.

## <a name="nx_lwm2m_resource_multiple_get_objlnk"></a>nx_lwm2m_resource_multiple_get_objlnk

Birden çok kaynak örneğinin bir nesne bağlantısının değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_objlnk(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, bir nesne bağlantı kaynağı örneğinin değerini birden çok kaynaktan alır.

### <a name="parameters"></a>Parametreler

- **değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.
- **Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.
- **instance_id_ptr**: hedef örnek kimliği işaretçisi.
- **objlnk_ptr**: hedef nesne bağlantı değerine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir nesne bağlantı değeri değil.

## <a name="nx_lwm2m_resource_multiple_get_opaque"></a>nx_lwm2m_resource_multiple_get_opaque

Donuk birden çok kaynak örneğinin değerini Al

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_opaque(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const VOID **opaque_ptr_ptr,
    UINT *opaque_length_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, bir donuk kaynak örneğinin değerini birden çok kaynaktan alır.

Donuk bir kaynak değeri, arabelleğin ve uzunluğun bir işaretçisinden oluşur.

### <a name="parameters"></a>Parametreler

- **değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.
- **Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.
- **instance_id_ptr**: hedef örnek kimliği işaretçisi.
- **opaque_ptr_ptr**: hedef donuk arabellek işaretçisine yönelik işaretçi.
- **opaque_length_ptr**: hedef donuk arabellek uzunluğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri donuk bir değer değil.

## <a name="nx_lwm2m_resource_multiple_get_string"></a>nx_lwm2m_resource_multiple_get_string

Birden çok kaynak örneğinin bir dize değerini alır

### <a name="prototype"></a>Prototype

```c
UINT nx_lwm2m_resource_multiple_get_string(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const CHAR **string_ptr_ptr,
    UINT *string_length_ptr);
```

### <a name="description"></a>Açıklama

Hizmet, bir dize kaynak örneğinin değerini birden çok kaynaktan alır.

### <a name="parameters"></a>Parametreler

- **değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.
- **Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.
- **instance_id_ptr**: hedef örnek kimliği işaretçisi.
- **string_ptr_ptr**: hedef dize işaretçisine yönelik işaretçi.
- **string_length_ptr**: hedef dize uzunluğuna yönelik işaretçi. Dize null sonlandırılırsa NULL olabilir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: başarılı işlem.
- **NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.
- **NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya örnek değeri bir dize değeri değil.
