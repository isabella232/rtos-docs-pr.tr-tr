---
title: Bölüm 3-Azure RTOS NetX LWM2M 'ın Işlevsel açıklaması
description: Bu bölümde, Azure RTOS NetX LWM2M 'in işlevsel bir açıklaması bulunmaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f49a4f5f4c899dfa461a9d57a8b56e4503d6acd4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826680"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-lwm2m"></a>Bölüm 3-Azure RTOS NetX LWM2M 'ın Işlevsel açıklaması

Bu bölümde, Azure RTOS NetX LWM2M 'in işlevsel bir açıklaması bulunmaktadır.

## <a name="lwm2m-client-initialization"></a>LWM2M Istemci başlatması

LWM2M Istemcisi ***nx_lwm2m_client_create*** hizmeti çağırarak başlatılır. LWM2M Istemcisi kendi iş parçacığında çalışır ve geri çağırmalar kullanılarak veya uygulama tarafından uygulanan özel nesnelerin yöntemlerini çağırarak uygulamaya bazı olayları bildirebilir.

Ayrıca, bir veya daha fazla sunucuyla iletişimi etkinleştirmek için ***nx_lwm2m_client_session_create*** çağırarak LWM2M istemci oturumlarının oluşturulması gerekir. Bir oturum iki farklı sunucu türüyle iletişim kurabilir: bir önyükleme sunucusu veya LWM2M sunucusu (cihaz yönetimi).

### <a name="bootstrap-server-session"></a>Önyükleme sunucusu oturumu

LWM2M Istemcisinin, bir veya daha fazla LWM2M sunucusuyla "Register" işlemini gerçekleştirmesini sağlamak için, LWM2M Istemcisine bir iletişim oturumu, bir önyükleme sunucusu ile ilgili bilgi sağlamak için kullanılır. Istemci tarafından başlatılan ve sunucu tarafından başlatılan önyükleme modlarında bu tür bir sunucu kullanılır.

Uygulama, ***nx_lwm2m_client_session_bootstrap** _ veya _*_Nx_lwm2m_client_session_bootstrap_dtls_*_ çağırarak bir önyükleme oturumu başlatabilir, sunucunun IP adresini ve bağlantı noktası numarasını ve Isteğe bağlı BIR güvenlik nesnesi örnek kimliğini sağlamalıdır. _*_Nx_lwm2m_client_session_bootstrap_*_ işlevi güvenli olmayan iletişim kullanır, ancak _ *_nx_lwm2m_client_session_bootstrap_dtls_** sunucuyla güvenli bir DTLS bağlantısı kurar.

Önyükleme işlemi başarılı olursa, önyükleme sunucusu, önyükleme ve LWM2M sunucuları için güvenlik nesne örnekleri ve LWM2M sunucuları için sunucu nesne örnekleri oluşturmuş olmalıdır. Uygulamanın, LWM2M sunucuları ile oturum oluşturmak için bu bilgileri kullanması gerekir.

Önyükleme verileri, cihazın bir sonraki yeniden başlatmada LWM2M Istemcisini yapılandırmak için uygulama tarafından geçici olmayan belleğe kaydedilmelidir.

### <a name="lwm2m-server-session"></a>LWM2M sunucusu oturumu

Kayıt, cihaz yönetimi ve hizmet etkinleştirme için bir LWM2M sunucusuyla iletişim oturumu kullanılır.

Uygulama, LWM2M Istemcisini ***nx_lwm2m_client_session_register** _ veya _*_nx_lwm2m_client_session_register_dtls_*_ çağırarak sunucuya kaydedebilir, sunucunun IP adresini ve bağlantı noktası numarasını ve var olan bir sunucu nesnesi örneğine KARŞıLıK gelen kısa sunucu kimliğini sağlamalıdır. _*_Nx_lwm2m_client_session_register_*_ işlevi güvenli olmayan iletişim kullanır, ancak _ *_nx_lwm2m_client_session_register_dtls_** sunucuyla güvenli bir DTLS bağlantısı kurar.

Uygulama, ***nx_lwm2m_client_session_deregister** _ ' i çağırarak LWM2M istemcisini kaydedebilir ve istemciden _ *_nx_lwm2m_client_session_update_* * çağırarak bir ' güncelleştirme ' iletisi göndermesini ister.

### <a name="session-state-callback"></a>Oturum durumu geri çağırma

Uygulama, oturum durumu güncellendiğinde çağrılan bir oturum oluşturma sırasında bir geri çağırma kaydeder, geri çağırma işlevi NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK aşağıdaki prototiple sahiptir:

```c
typedef VOID (*NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK)
        (NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state);
```

Aşağıdaki durumlar tanımlanmıştır:

- **NX_LWM2M_CLIENT_SESSION_INIT**: oturum oluşturulduktan sonra ilk durum.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING**: istemci, ' bekletme ' süreölçeri veya sunucu tarafından başlatılan önyükleme işleminin sona erme süresini bekliyor.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**: Istemci önyükleme sunucusuna bir ' istek ' iletisi gönderdi (Istemci tarafından başlatılan önyükleme).

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**: Istemci, önyükleme sunucusundan veri alıyor.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED**: önyükleme sunucusu ' FINISHED ' iletisi gönderdi.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR**: önyükleme oturumu başarısız oldu.

- **NX_LWM2M_CLIENT_SESSION_REGISTERING**: ISTEMCI, LWM2M sunucusuna bir ' Register ' iletisi gönderdi.

- **NX_LWM2M_CLIENT_SESSION_REGISTERED**: Istemci LWM2M sunucusuna kaydedilir.

- **NX_LWM2M_CLIENT_SESSION_UPDATING**: ISTEMCI, LWM2M sunucusuna bir ' Update ' iletisi gönderdi.

- **NX_LWM2M_CLIENT_SESSION_DEREGISTERING**: ISTEMCI, LWM2M sunucusuna ' de Register ' iletisi gönderdi.

- **NX_LWM2M_CLIENT_SESSION_DEREGISTERED**: ISTEMCI, LWM2M sunucusundan de kayıtlı.

- **NX_LWM2M_CLIENT_SESSION_DISABLED**: LWM2M sunucusu devre dışı bırakıldı. Devre dışı bırakma süreölçeri sona erdikten sonra bir ' Register ' gönderilir.

- **NX_LWM2M_CLIENT_SESSION_ERROR**: LWM2M sunucusuna kaydolma veya güncelleştirme işlemi başarısız oldu.

- **NX_LWM2M_CLIENT_SESSION_DELETED**: LWM2M sunucusuna karşılık gelen sunucu nesnesi örneği silindi. Hata durumunda uygulamanın, **_nx_lwm2m_client_session_error_get_** çağırarak hatanın nedenini elde edebilir.

## <a name="local-device-management"></a>Yerel cihaz yönetimi

Uygulama, yerel cihaz yönetimi işlevlerini kullanarak LWM2M Istemcisinin nesnelerine erişebilir. Aşağıdaki işlevler verilmiştir:

- ***nx_lwm2m_client_object_read***: bir nesne örneğinden kaynakları okuyun.

- ***nx_lwm2m_client_object_discover***: bir nesne örneğinin kaynak listesini alın.

- ***nx_lwm2m_client_object_write***: kaynakları bir nesne örneğine yazma

- ***nx_lwm2m_client_object_execute***: bir nesne örneğinin kaynağında yürütme işlemi gerçekleştirin.

- ***nx_lwm2m_client_object_create***: yeni bir nesne örneği oluşturun.

- ***nx_lwm2m_client_object_delete***: varolan bir nesne örneğini silin.

- ***nx_lwm2m_client_object_get_next***: lwm2m istemcisi tarafından uygulanan sonrakı nesne kimliğini alın.

- ***nx_lwm2m_client_object_instance_get_next***: bir nesnenin sonraki örneğini al.

## <a name="resource-information"></a>Kaynak bilgileri

Nesneleri okuma ve nesnelere yazma sırasında bir kaynak NX_LWM2M_RESOURCE yapısıyla temsil edilir. Bu yapı, kaynak/örnek KIMLIĞINI ve değerini içerir. Değerin kodlaması türüne ve kaynağına (uygulama veya ağ) bağlıdır.

NX_LWM2M_RESOURCE yapısı aşağıdaki tanıma sahiptir:

```c
typedef struct NX_LWM2M_RESOURCE_STRUCT
{
    NX_LWM2M_ID     nx_lwm2m_resource_id;
    UCHAR           nx_lwm2m_resource_type;
    union
    {
        struct
        {
            const VOID *     nx_lwm2m_resource_buffer_ptr;
            UINT             nx_lwm2m_resource_buffer_length;
        } nx_lwm2m_resource_bufferdata;
        const CHAR *         nx_lwm2m_resource_stringdata;
        NX_LWM2M_INT32       nx_lwm2m_resource_integer32data;
        NX_LWM2M_INT64       nx_lwm2m_resource_integer64data;
        NX_LWM2M_FLOAT32     nx_lwm2m_resource_float32data;
        NX_LWM2M_FLOAT64     nx_lwm2m_resource_float64data;
        NX_LWM2M_BOOL        nx_lwm2m_resource_booleandata;
        NX_LWM2M_OBJLNK      nx_lwm2m_resource_objlnkdata;
        
        struct
        {
            const VOID *     nx_lwm2m_resource_multiple_ptr;
            UINT             nx_lwm2m_resource_multiple_dim;
        } nx_lwm2m_resource_multipledata;
    } nx_lwm2m_resource_value;
} NX_LWM2M_RESOURCE;
```

- **nx_lwm2m_resource_id**: kaynağın veya örneğin kimliği.
- **nx_lwm2m_resource_type**: değerin türü, aşağıya bakın.
- **nx_lwm2m_resource_value**: kaynağın değeri, değerin türüne bağlıdır.

Aşağıdaki değer türleri tanımlanmıştır:

- **NX_LWM2M_RESOURCE_NONE**: boş kaynak.

- **NX_LWM2M_RESOURCE_STRING**: *nx_lwm2m_resource_stringdata* içinde depolanan, null ile sonlandırılmış bir UTF-8 dize değeri.

- **NX_LWM2M_RESOURCE_INTEGER32**: *Nx_lwm2m_resource_integer32data* depolanan 32 bitlik bir tamsayı değeri.

- **NX_LWM2M_RESOURCE_INTEGER64**: *Nx_lwm2m_resource_integer64data* depolanan 64 bitlik bir tamsayı değeri.

- **NX_LWM2M_RESOURCE_FLOAT32**: *Nx_lwm2m_resource_float32data* depolanan 32 bitlik kayan nokta değeri.

- **NX_LWM2M_RESOURCE_FLOAT64**: *Nx_lwm2m_resource_float64data* depolanan 64 bitlik kayan nokta değeri.

- **NX_LWM2M_RESOURCE_BOOLEAN**: *Nx_lwm2m_resource_booleandata* depolanan bir Boole değeri.

- **NX_LWM2M_RESOURCE_OPAQUE**: *Nx_lwm2m_resource_bufferdata* tarafından tanımlanan donuk bir değer.

- **NX_LWM2M_RESOURCE_OBJLNK**: *Nx_lwm2m_resource_objlnkdata* depolanan bir nesne bağlantı değeri.

- **NX_LWM2M_RESOURCE_TLV**: *nx_lwm2m_resource_bufferdata* tarafından tanımlanan bir TLV şifreli değeri.

- **NX_LWM2M_RESOURCE_TEXT**: *nx_lwm2m_resource_bufferdata* tarafından tanımlanan Plain-Text kodlanmış bir değer.

- **NX_LWM2M_RESOURCE_MULTIPLE**: *Nx_lwm2m_resource_multipledata* tarafından tanımlanan birden çok kaynak. *nx_lwm2m_resource_multiple_ptr* , her kaynak örneği hakkında bilgi içeren bir **NX_LWM2M_RESOURCE** yapıları dizisinin bir işaretçisidir.

- **NX_LWM2M_RESOURCE_MULTIPLE_TLV**: *Nx_lwm2m_resource_multipledata* tarafından tanımlanan birden çok kaynak. *nx_lwm2m_resource_multiple_ptr* , TLV kodlamalı arabelleğin bir işaretçisidir.

Değer almak ve türünü denetlemek için kullanışlı işlevler, NX_LWM2M_RESOURCE yapısından bir değer alırken uygulama asla *nx_lwm2m_resource_value* alana doğrudan erişmemelidir. Aşağıdaki işlevler tanımlanmıştır:

- ***nx_lwm2m_resource_get_***: verilen türe sahip bir değer alın.
- ***nx_lwm2m_resource_multiple_get_***: birden fazla kaynaktan verilen türe sahip bir değer alın.

Makro **NX_LWM2M_RESOURCE_IS_MULTIPLE**(tür), bir kaynak türünün birden çok kaynak olup olmadığını denetlemek için kullanılabilir.

## <a name="object-implementation"></a>Nesne uygulama

LWM2M Istemcisi zorunlu OMA LWM2M nesnelerini uygular: güvenlik (0), sunucu (1), Access Control (2) ve cihaz (3). Diğer cihaza özgü nesnelerin uygulama tarafından uygulanması gerekir.

Bir nesneyi tanımlamak için iki veri yapısı kullanılır: NX_LWM2M_OBJECT yapısı, nesne KIMLIĞI ve nesne yöntemleri de dahil olmak üzere nesne uygulamasını tanımlar ve NX_LWM2M_OBJECT_INSTANCE yapısı bir nesne örneğinin verilerini içerir.

NX_LWM2M_OBJECT yapısı aşağıdaki tanıma sahiptir:

```c
typedef struct NX_LWM2M_OBJECT_STRUCT
{
    NX_LWM2M_OBJECT * nx_lwm2m_object_next;
    NX_LWM2M_ID nx_lwm2m_object_id;
    UINT (*nx_lwm2m_object_read)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
        NX_LWM2M_RESOURCE *values);
    UINT (*nx_lwm2m_object_discover)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT *num_resources,
        NX_LWM2M_RESOURCE_INFO *resources);
    UINT (*nx_lwm2m_object_write)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values, const
        NX_LWM2M_RESOURCE *values, UINT write_op);
    UINT (*nx_lwm2m_object_execute)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
        const CHAR *args_ptr, UINT args_length);
    UINT (*nx_lwm2m_object_create)(NX_LWM2M_OBJECT * object_ptr,
        NX_LWM2M_ID instance_id, UINT num_values, const NX_LWM2M_RESOURCE
        *values, NX_LWM2M_OBJECT_INSTANCE **instance_ptr);
    UINT (*nx_lwm2m_object_delete)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr);
    NX_LWM2M_OBJECT_INSTANCE * nx_lwm2m_object_instances;
} NX_LWM2M_OBJECT;
```

- **nx_lwm2m_object_next**: listedeki bir sonraki nesne.
- **nx_lwm2m_object_id**: nesne kimliği.
- **nx_lwm2m_object_read**: ' Read ' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_discover**: ' bul ' yöntemi aşağıya bakın.
- **nx_lwm2m_object_write**: ' Write ' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_execute**: ' Execute ' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_create**: ' Create ' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_delete**: ' DELETE ' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_instances**: nesne örneklerinin null ile sonlandırılmış listesi.

NX_LWM2M_OBJECT_INSTANCE yapısı aşağıdaki tanıma sahiptir:

```c
typedef struct NX_LWM2M_OBJECT_INSTANCE_STRUCT
{
    NX_LWM2M_OBJECT_INSTANCE * nx_lwm2m_object_instance_next;
    NX_LWM2M_ID nx_lwm2m_object_instance_id;
} NX_LWM2M_OBJECT_INSTANCE;
```

- **nx_lwm2m_object_instance_next**: listedeki bir sonraki örnek.
- **nx_lwm2m_object_instance_id**: nesne örneği kimliği.

Nesne, LWM2M cihaz yönetimi arabirimi tarafından tanımlanan işlemlere karşılık gelen yöntemleri uygulamalıdır: ' Read ', ' Discover ', ' Write ', ' Execute ', ' Create ' ve ' DELETE '. ' Create ' ve ' DELETE ' yöntemleri, nesne örneklerin dinamik olarak oluşturulmasını desteklemiyorsa NULL olarak ayarlanabilir.

### <a name="the-read-method"></a>' Read ' yöntemi

' Read ' yöntemi, bir nesne örneğinden kaynak değerlerini okumak için kullanılır, işlev aşağıdaki tanıma sahiptir:

```c
UINT nx_lwm2m_object_read(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    NX_LWM2M_RESOURCE *values_ptr);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

- **object_ptr**: nesne uygulamasına yönelik işaretçi.

- **instance_ptr**: nesne örneğine yönelik işaretçi.

- **num_values**: okunacak kaynak sayısı.

- **values_ptr**: okunacak kaynakların kimliklerini içeren bir NX_LWM2M_RESOURCE dizisine yönelik işaretçi. Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.

### <a name="the-discover-method"></a>' Keşfet ' yöntemi

' Keşfet ' yöntemi, bir nesne tarafından uygulanan tüm kaynakların listesini almak için kullanılır, işlev aşağıdaki tanıma sahiptir:

```c
UINT nx_lwm2m_object_discover(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT *num_resources_ptr,
    NX_LWM2M_RESOURCE_INFO *resources_ptr);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

- **object_ptr**: nesne uygulamasına yönelik işaretçi.

- **instance_ptr**: nesne örneğine yönelik işaretçi.

- **num_resources_ptr**: giriş, hedef arabelleğin boyutunun çıktıda, arabelleğe yazıldı.

- **resources_ptr**: hedef arabelleğin işaretçisi.

Kaynak bilgileri aşağıdaki şekilde tanımlanan bir NX_LWM2M_RESOURCE_INFO yapısında döndürülür:

```c
typedef struct NX_LWM2M_RESOURCE_INFO_STRUCT
{
    NX_LWM2M_ID     nx_lwm2m_resource_info_id;
    USHORT          nx_lwm2m_resource_info_flags;
    UINT            nx_lwm2m_resource_info_dim;
} NX_LWM2M_RESOURCE_INFO;
```

- **nx_lwm2m_resource_info_id**: kaynağın kimliği.

- **nx_lwm2m_resource_info_flags**: aşağıya bakın.

- **nx_lwm2m_resource_info_dim**: bayrak NX_LWM2M_RESOURCE_INFO_MULTIPLE ayarlandıysa birden çok kaynağın boyutu.

*Nx_lwm2m_resource_flags* alan aşağıdaki değerlere sahip olabilir:

- 0: tek okunabilir kaynak.

- **NX_LWM2M_RESOURCE_INFO_MULTIPLE**: birden çok kaynak, *nx_lwm2m_resource_info_dim* tanımlanmalıdır.

- **NX_LWM2M_RESOURCE_INFO_EXECUTABLE**: çalıştırılabilir veya okunabilir olmayan kaynak.

### <a name="the-write-method"></a>' Write ' yöntemi

' Write ' yöntemi bir nesne örneğinin kaynaklarını güncelleştirmek ya da değiştirmek için kullanılır, işlevin aşağıdaki tanımı vardır:

```c
UINT nx_lwm2m_object_write(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr, UINT write_op);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

- **object_ptr**: nesne uygulamasına yönelik işaretçi.
- **instance_ptr**: nesne örneğine yönelik işaretçi.
- **num_values**: yazılacak kaynak sayısı.
- **values_ptr**: kaynak değerlerine yönelik işaretçi.
- **write_op**: yazma işlemlerinin türü.

*Write_op* parametresine aşağıdaki yazma işlemleri de belirtilebilir:

- 0 &mdash; Kısmi güncelleştirme: yeni değerde belirtilen kaynakları ekler veya güncelleştirir ve diğer mevcut kaynakları değiştirmeden bırakır,

- **NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Örnek Değiştir: nesne örneğini, yeni sağlanmış kaynak değerleriyle değiştirir.

- **NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Kaynağı değiştir: kaynakları, belirtilen yeni kaynak değerleriyle (birden çok kaynağı değiştirmek için kullanılır) değiştirir.

- **NX_LWM2M_OBJECT_WRITE_CREATE** &mdash; Örnek oluştur: yeni oluşturulan nesne örneğini, belirtilen kaynak değerleriyle ( *nx_lwm2m_object_create* yönteminden çağırılır) başlatır.

- **NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap yazma: önyükleme sırası sırasında çağırılır.

### <a name="the-execute-method"></a>' Execute ' yöntemi

' Execute ' yöntemi bir nesne kaynağının yürütülmesini uygular, işlev aşağıdaki tanıma sahiptir:

```c
UINT nx_lwm2m_object_execute(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

- **object_ptr**: nesne uygulamasına yönelik işaretçi
- **instance_ptr**: nesne örneğine yönelik işaretçi.
- **resource_id**: kaynak kimliği.
- **arguments_ptr**: yürütme işleminin bağımsız değişkenlerine yönelik işaretçi. *Arguments_length* sıfırsa null olabilir.
- **arguments_length**: bağımsız değişkenlerin uzunluğu.

Kaynak KIMLIĞI yoksa işlevin NX_LWM2M_NOT_FOUND döndürmesi veya yürütmeyi desteklememesi durumunda NX_LWM2M_METHOD_NOT_ALLOWED gerekir.

### <a name="the-create-method"></a>' Create ' yöntemi

' Create ' yöntemi, yeni bir nesne örneği oluşturulmasını uygular, işlev aşağıdaki tanıma sahiptir:

```c
UINT nx_lwm2m_object_create(NX_LWM2M_OBJECT * object_ptr,
    NX_LWM2M_ID instance_id, UINT num_values, const NX_LWM2M_RESOURCE *values_ptr,
    NX_LWM2M_OBJECT_INSTANCE **instance_ptr, NX_LWM2M_BOOL bootstrap);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

- **object_ptr**: nesne uygulamasına yönelik işaretçi.
- **instance_id**: yenı örneğin kimliği.
- **num_values**: başlatılacak kaynak sayısı.
- **values_ptr**: kaynak değerlerine yönelik işaretçi.
- **instance_ptr**: oluşturulan örneğin hedef işaretçisine yönelik işaretçi.
- **bootstrap**: önyükleme sırasından çağrılırsa true.

Nesne, belirtilen kaynak değerleri listesini kullanarak yeni bir nesne örneği ayırmalıdır ve bu örneğe yeniden başlatılabilir.

### <a name="the-delete-method"></a>' DELETE ' yöntemi

' DELETE ' yöntemi bir nesne örneğinin silinmesini uygular, işlev aşağıdaki tanıma sahiptir:

```c
UINT nx_lwm2m_object_delete(NX_LWM2M_OBJECT *object_ptr,
                NX_LWM2M_OBJECT_INSTANCE *instance_ptr);
```

Giriş parametreleri aşağıdaki gibi tanımlanır:

- **object_ptr**: nesne uygulamasına yönelik işaretçi.
- **instance_ptr**: nesne örneğine yönelik işaretçi.

Başarılı olduğunda, nesne örnek verilerini ve örnek tarafından ayrılan diğer kaynakları serbest bırakmalıdır.

### <a name="adding-object-implementations-and-instances-to-the-lwm2m-client"></a>LWM2M Istemcisine nesne uygulamaları ve örnekler ekleme

Uygulama, ***nx_lwm2m_client_object_add*** HIZMETINI çağırarak LWM2M istemcisine yeni nesne uygulaması ekleyebilir.

Nesnesi dinamik örnek oluşturmayı desteklemiyorsa örneğin yalnızca tek örnekli bir nesne ise, nesne yapısının *nx_lwm2m_object_instances* alanı statik örnekler yapıları listesine işaret etmelidir.

Nesne dinamik örnek oluşturmayı destekliyorsa, *NX_LWM2M_OBJECT_INSTANCES* null olarak ayarlanmalıdır ve nesnenin ' Create ' metodunu çağırmak için bunun yerine ***nx_lwm2m_client_object_create*** hizmeti kullanılmalıdır.

## <a name="example-of-lwm2m-client-application"></a>LWM2M Istemci uygulaması örneği

Aşağıdaki kod, bir sıcaklık sensörden ve hafif anahtardan oluşan özel bir cihaz uygulayan basit bir LWM2M Istemci uygulamasına bir örnektir.

Cihaz, bir sunucunun ısı algılayıcısı değerini ve ışık anahtarının Boole durumunu okumasına izin verir ve ışığı açık/kapalı olarak ayarlar.

```c
#include "nx_lwm2m_client.h"

/* Custom Object implementation */
/* Define the Custom Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_OBJECT_INSTANCE     lwm2m;

    /* Resources Data */
    NX_LWM2M_FLOAT32             temperature;
    NX_LWM2M_BOOL                light;
} MYOBJECT_INSTANCE;

/* Define the Resources IDs */
#define MYOBJECT_RES_TEMPERATURE     0 /* temperature sensor */
#define MYOBJECT_RES_LIGHT           1 /* light switch */

/* Define the 'Read' Method */
UINT myobject_read(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr,
    UINT num_values, NX_LWM2M_RESOURCE *values)
{
    UINT i;
    for (i=0; i<num_values; i++)
    {
        switch (values[i].nx_lwm2m_resource_id)
        {
        case MYOBJECT_RES_TEMPERATURE:

            /* return the temperature value */
            values[i].nx_lwm2m_resource_type = NX_LWM2M_RESOURCE_FLOAT32;
            values[i].nx_lwm2m_resource_value.nx_lwm2m_resource_float32data =
                ((MYOBJECT_INSTANCE *) instance_ptr)->temperature;
            break;
        case MYOBJECT_RES_LIGHT:

            /* return the state of the light switch */
            values[i].nx_lwm2m_resource_type = NX_LWM2M_RESOURCE_BOOLEAN;
            values[i].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata =
                ((MYOBJECT_INSTANCE *) instance_ptr)->light;
            break;

        default:

            /* unknown resource ID */
            return NX_LWM2M_NOT_FOUND;
        }
    }
    return NX_SUCCESS;
}

/* Define the 'Discover' method */
UINT myobject_discover(NX_LWM2M_OBJECT *object_ptr, NX_LWM2M_OBJECT_INSTANCE *instance_ptr,
                                    UINT *num_resources, NX_LWM2M_RESOURCE_INFO *resources)
{
    if (*num_resources < 2)
    {
        return NX_LWM2M_BUFFER_TOO_SMALL;
    }

    /* return the list of supported resources IDs */
    *num_resources = 2;
    resources[0].nx_lwm2m_resource_info_id        = MYOBJECT_RES_TEMPERATURE;
    resources[0].nx_lwm2m_resource_info_flags     = 0;
    resources[1].nx_lwm2m_resource_info_id        = MYOBJECT_RES_LIGHT;
    resources[1].nx_lwm2m_resource_info_flags     = 0;
    return NX_SUCCESS;
}

/* Define the 'Write' method */
UINT myobject_write(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    const NX_LWM2M_RESOURCE *values, UINT flags)
{
    UINT i;
    for (i=0; i<num_values; i++)
    {
        UINT ret;
        switch (values[i].nx_lwm2m_resource_id)
        {

        case MYOBJECT_RES_TEMPERATURE:

            /* read-only resource */
            return NX_LWM2M_METHOD_NOT_ALLOWED;

        case MYOBJECT_RES_LIGHT:

            /* assign boolean value */

            ret = nx_lwm2m_resource_get_boolean(&values[i],
                &((MYOBJECT_INSTANCE *) instance_ptr)->light);

            if (ret != NX_SUCCESS)
            {

                /* invalid value type */
                return ret;
            }
            break;

        default:

            /* unknown resource ID */
            return NX_LWM2M_NOT_FOUND;
        }
    }
    return NX_SUCCESS;
}

/* Define the 'Execute' method */
UINT myobject_execute(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
    const CHAR *args_ptr, UINT args_length)
{
    switch (resource_id)
    {

    case MYOBJECT_RES_TEMPERATURE:
    case MYOBJECT_RES_LIGHT:

        /* read-only resource */
        return NX_LWM2M_METHOD_NOT_ALLOWED;

    default:

        /* unknown resource ID */
        return NX_LWM2M_NOT_FOUND;

    }
}

/* NetX data */
NX_IP                       ip;
NX_PACKET_POOL              packet_pool;

/* LWM2M Client data */
NX_LWM2M_CLIENT             client;
ULONG                       client_stack[4096 / sizeof(ULONG)];
NX_LWM2M_CLIENT_SESSION     session;

/* Custom Object Data */
NX_LWM2M_OBJECT             myobject;
MYOBJECT_INSTANCE           myinstance;

/* Define the session state callback */
void session_callback(NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state)
{
    switch (state)
    {

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:

        /* Bootstrap session done, we can register to the LWM2M Server */
        {
            NX_LWM2M_ID security_id;

            /* find the Security Object Instance of the LWM2M Server */
            security_id = NX_LWM2M_RESERVED_ID;
            while (nx_lwm2m_client_object_instance_get_next(&client,
                NX_LWM2M_SECURITY_OBJECT_ID, &security_id) == NX_SUCCESS)
            {
                NX_LWM2M_RESOURCE res[3];

                /* retrieve instance data: */
                /* Bootstrap server flag */
                res[0].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_BOOTSTRAP_ID;

                /* URI of server */
                res[1].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_URI_ID;

                /* Short Server ID */
                res[2].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_SHORT_SERVER_ID;

                /* Read Object Instance: */
                nx_lwm2m_client_object_read(&client,
                    NX_LWM2M_SECURITY_OBJECT_ID, security_id, 3, res);

                /* Not a bootstrap server? */
                if (!res[0].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata)
                {
                    ULONG ip_addr;
                    UINT udp_port;

                    /* get IP address and UDP port from server URI */
                    parse_uri(res[1].nx_lwm2m_resource_value.nx_lwm2m_resource_stringdata, &ip_addr, &udp_port);

                    /* Start registration to the LWM2M server */
                    nx_lwm2m_client_session_register(&session,
                        (NX_LWM2M_ID) res[2].nx_lwm2m_resource_value.
                        nx_lwm2m_resource_integer32data,
                        ip_addr, udp_port);
                    break;
                }
            }
        }
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:

        /* Failed to Bootstrap the LWM2M Client. */
        break;

    case NX_LWM2M_CLIENT_SESSION_REGISTERED:

        /* Registration to the LWM2M Client done. */
        break;

    case NX_LWM2M_CLIENT_SESSION_ERROR:

        /* Failed to register to the LWM2M Client. */
        break;
    }
}

/* Application main thread */
void application_thread(ULONG info)
{
    NX_LWM2M_RESOURCE res[4];
    NX_LWM2M_ID security_id;

    /* Create the LWM2M client */
    nx_lwm2m_client_create(&client, &ip, &packet_pool, NX_LWM2M_COAP_PORT,
        "mylwm2mclient", NULL, NX_LWM2M_BINDING_U,
        client_stack, sizeof(client_stack));

    /* Define our custom object */
    myobject.nx_lwm2m_object_id           = 1024;
    myobject.nx_lwm2m_object_read         = myobject_read;
    myobject.nx_lwm2m_object_discover     = myobject_discover;
    myobject.nx_lwm2m_object_write        = myobject_write;
    myobject.nx_lwm2m_object_execute      = myobject_execute;
    myobject.nx_lwm2m_object_create       = NULL;
    myobject.nx_lwm2m_object_delete       = NULL;

    /* Define a single instance */
    myobject.nx_lwm2m_object_instances             = (NX_LWM2M_OBJECT_INSTANCE *) &myinstance;
    myinstance.lwm2m.nx_lwm2m_object_instance_id   = 0;
    myinstance.lwm2m.nx_lwm2m_object_instance_next = NULL;
    myinstance.temperature                         = 22.5f;
    myinstance.light                               = NX_FALSE;

    /* Add the object to the LWM2M Client */
    nx_lwm2m_client_object_add(&client, &myobject);

    /* Create a security entry for the bootstrap server */
    security_id = 0;

    /* set the URI of the server */
    res[0].nx_lwm2m_resource_id                                 = NX_LWM2M_SECURITY_URI_ID;
    res[0].nx_lwm2m_resource_type                               = NX_LWM2M_RESOURCE_STRING;
    res[0].nx_lwm2m_resource_value.nx_lwm2m_resource_stringdata = "coap://1.2.3.4";

    /* set the Bootstrap flag */
    res[1].nx_lwm2m_resource_id                                  = NX_LWM2M_SECURITY_BOOTSTRAP_ID;
    res[1].nx_lwm2m_resource_type                                = NX_LWM2M_RESOURCE_BOOLEAN;
    res[1].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata = NX_TRUE;

    /* set the security mode */
    res[2].nx_lwm2m_resource_id                                    = NX_LWM2M_SECURITY_MODE_ID;
    res[2].nx_lwm2m_resource_type                                  = NX_LWM2M_RESOURCE_INTEGER32;
    res[2].nx_lwm2m_resource_value.nx_lwm2m_resource_integer32data =
    NX_LWM2M_SECURITY_MODE_NOSEC;

    /* set the Hold Off timer */
    res[3].nx_lwm2m_resource_id                                    = NX_LWM2M_SECURITY_HOLD_OFF_ID;
    res[3].nx_lwm2m_resource_type                                  = NX_LWM2M_RESOURCE_INTEGER32;
    res[3].nx_lwm2m_resource_value.nx_lwm2m_resource_integer32data = 10;
    nx_lwm2m_client_object_create(&client, NX_LWM2M_SECURITY_OBJECT_ID,
        &security_id, 4, res);

    /* Create a session */
    nx_lwm2m_client_session_create(&session, &client, session_callback);

    /* start bootstrap session */
    nx_lwm2m_client_session_bootstrap(&session, security_id,
                            IP_ADDRESS(1, 2, 3, 4), 5683);

    /* Application main loop */
    while (1)
    {
        /* ...application code... */
    }

    /* Terminate the LWM2M Client */
    nx_lwm2m_client_delete(&client);
}
```
