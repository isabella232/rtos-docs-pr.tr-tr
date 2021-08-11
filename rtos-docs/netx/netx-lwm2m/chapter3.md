---
title: Bölüm 3 - NetX LWM2M Azure RTOS işlevsel açıklaması
description: Bu bölümde NetX LWM2M Azure RTOS işlevsel bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6424023a02aedf43c7433c9adc09231b8c146af13b9bddc15ebd1f2fc02e8c8a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784946"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-lwm2m"></a>Bölüm 3 - NetX LWM2M Azure RTOS işlevsel açıklaması

Bu bölümde NetX LWM2M Azure RTOS işlevsel bir açıklama yer almaktadır.

## <a name="lwm2m-client-initialization"></a>LWM2M İstemci Başlatma

LWM2M İstemcisi, nx_lwm2m_client_create ***başlatılır.*** LWM2M İstemcisi kendi iş parçacığında çalışır ve geri çağırmaları kullanarak veya uygulama tarafından uygulanan özel nesnelerin yöntemlerini çağırarak uygulamaya bazı olayları bildirebilir.

Ayrıca LWM2M İstemci Oturumları, bir veya ***daha fazla nx_lwm2m_client_session_create*** iletişimin etkinleştirilmesi için özel çağrılarak oluşturularak oluşturulacak. Bir oturum iki farklı sunucu türüyle iletişim kurabilir: Bir Bootstrap Sunucusu veya LWM2M Sunucusu (Cihaz Yönetimi).

### <a name="bootstrap-server-session"></a>Bootstrap Sunucusu Oturumu

LWM2M İstemcisi'nin bir veya daha fazla LWM2M Sunucusuna "Kaydetme" işlemini gerçekleştirmesini sağlamak üzere LWM2M İstemcisine temel bilgileri sağlamak için Bootstrap Sunucusu ile bir iletişim oturumu kullanılır. Bu sunucu türü İstemci Tarafından Başlatılan ve Sunucu Tarafından Başlatılan Önyükleme modları sırasında kullanılır.

Uygulama * nx_lwm2m_client_session_bootstrap _ **veya** _*_nx_lwm2m_client_session_bootstrap_dtls_*_ çağırarak bir Bootstrap oturumu başlatabiliyor, sunucunun IP adresini ve bağlantı noktası numarasını ve isteğe bağlı bir Güvenlik Nesnesi Örneği Kimliğini sağlayabiliyor. Bu _*_nx_lwm2m_client_session_bootstrap_*_ güvenli olmayan iletişim kullanırken _ *_nx_lwm2m_client_session_bootstrap_dtls_** sunucuyla güvenli bir DTLS bağlantısı kurulmasını sağlar.

Bootstrap işlemi başarılı olursa, Bootstrap sunucusunun Bootstrap ve LWM2M Sunucuları için Güvenlik Nesnesi Örnekleri ve LWM2M Sunucuları için Sunucu Nesnesi Örnekleri oluşturması gerekir. Uygulamanın LWM2M Sunucularla oturum kurmak için bu bilgileri kullanması gerekir.

Cihazın bir sonraki yeniden başlatılmasında LWM2M İstemcisi'nin yapılandırılması için Bootstrap verileri uygulama tarafından geçici olmayan belleğe kaydedılmalıdır.

### <a name="lwm2m-server-session"></a>LWM2M Sunucu Oturumu

Kayıt, Güvenlik Ve Hizmet Etkinleştirme için LWM2M Sunucusu ile Cihaz Yönetimi oturumu kullanılır.

Uygulama , ***nx_lwm2m_client_session_register** _ veya _*_nx_lwm2m_client_session_register_dtls_*_ çağırarak LWM2M İstemcisini bir sunucuya kaydedebilir, sunucunun IP adresini ve bağlantı noktası numarasını ve mevcut Sunucu Nesne Örneğine karşılık gelen Kısa Sunucu Kimliğini sağlasa gerekir. Bu _*_nx_lwm2m_client_session_register_*_ güvenli olmayan iletişim kullanırken _ *_nx_lwm2m_client_session_register_dtls_** sunucuyla güvenli bir DTLS bağlantısı kurulmasını sağlar.

Uygulama ***nx_lwm2m_client_session_deregister** _ çağırarak LWM2M İstemcisi'nin kaydını sildi ve _* nx_lwm2m_client_session_update ** çağrısıyla istemciden bir 'Güncelleştir'_iletisi göndermesini_ isteyebilir.

### <a name="session-state-callback"></a>Oturum Durumu Geri Çağırma

Uygulama, oturumun durumu güncelleştirildiğinde çağrılan bir oturumun oluşturulması sırasında bir geri çağırmayı kaydediyor. Geri çağırma işlevi NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK prototipe sahiptir:

```c
typedef VOID (*NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK)
        (NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state);
```

Aşağıdaki eyaletler tanımlanmıştır:

- **NX_LWM2M_CLIENT_SESSION_INIT:** Oturum oluşturma sonrasındaki ilk durum.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING:** İstemci , 'Kapalı Tut' süreölçeri veya Sunucu Tarafından Başlatılan Önyükleme'nin süresinin dolması için bekliyor.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING:** İstemci, Bootstrap Sunucusuna bir 'İstek' iletisi gönderdi (İstemci Tarafından Başlatılan Bootstrap).

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED:** İstemci, Bootstrap Sunucusundan veri alıyor.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:** Bootstrap Sunucusu bir 'Bitti' iletisi gönderdi.

- **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:** Önyükleme oturumu başarısız oldu.

- **NX_LWM2M_CLIENT_SESSION_REGISTERING:** İstemci LWM2M Sunucusuna bir 'Kaydetme' iletisi gönderdi.

- **NX_LWM2M_CLIENT_SESSION_REGISTERED:** İstemci LWM2M Sunucusuna kaydedilir.

- **NX_LWM2M_CLIENT_SESSION_UPDATING:** İstemci LWM2M Sunucusuna bir 'Güncelleştir' iletisi gönderdi.

- **NX_LWM2M_CLIENT_SESSION_DEREGISTERING:** İstemci LWM2M Sunucusuna bir 'Kaydı Geri Gönder' iletisi gönderdi.

- **NX_LWM2M_CLIENT_SESSION_DEREGISTERED:** İstemci LWM2M Sunucusundan kaydı kaldırıldı.

- **NX_LWM2M_CLIENT_SESSION_DISABLED:** LWM2M Sunucusu devre dışı bırakıldı. Devre dışı bırakma süreölçeri sona erdikten sonra bir 'Register' gönderilir.

- **NX_LWM2M_CLIENT_SESSION_ERROR:** LWM2M Sunucusuna kayıt veya güncelleştirme işlemi başarısız oldu.

- **NX_LWM2M_CLIENT_SESSION_DELETED:** LWM2M Sunucusuna karşılık gelen Sunucu Nesne Örneği silindi. Hata durumunda uygulama, hatanın nedenini almak için **_nx_lwm2m_client_session_error_get._**

## <a name="local-device-management"></a>Yerel Cihaz Yönetimi

Uygulama, yerel cihaz yönetimi işlevlerini kullanarak LWM2M İstemcisi Nesneleri'ne erişebilir. Aşağıdaki işlevler sağlanır:

- ***nx_lwm2m_client_object_read:*** Bir Nesne Örneğinden kaynakları okuyun.

- ***nx_lwm2m_client_object_discover:*** Nesne Örneğinin kaynaklarının listesini al.

- ***nx_lwm2m_client_object_write:*** Nesne Örneğine kaynak yazma

- ***nx_lwm2m_client_object_execute:*** Nesne Örneğinin kaynağında Yürütme işlemini gerçekleştirin.

- ***nx_lwm2m_client_object_create:*** Yeni bir Nesne Örneği oluşturun.

- ***nx_lwm2m_client_object_delete:*** Var olan bir Nesne Örneğini silin.

- ***nx_lwm2m_client_object_get_next:*** LWM2M İstemcisi tarafından uygulanan sonraki Nesne Kimliğini al.

- ***nx_lwm2m_client_object_instance_get_next:*** Bir Nesnenin sonraki Örneğini al.

## <a name="resource-information"></a>Kaynak Bilgileri

Nesnelerden okuma ve Nesnelere yazma, kaynak yapısı tarafından NX_LWM2M_RESOURCE temsil eder. Bu yapı, Kaynağın/Örneğin kimliğini ve değerini içerir. Değerin kodlaması türüne ve kaynağına (uygulama veya ağ) bağlıdır.

NX_LWM2M_RESOURCE yapısı aşağıdaki tanımlara sahiptir:

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

- **nx_lwm2m_resource_id:** Kaynağın veya Örneğin Kimliği.
- **nx_lwm2m_resource_type:** Değerin türü, aşağıya bakın.
- **nx_lwm2m_resource_value:** Kaynağın değeri, değerin türüne bağlıdır.

Aşağıdaki değer türü tanımlanmıştır:

- **NX_LWM2M_RESOURCE_NONE:** Boş kaynak.

- **NX_LWM2M_RESOURCE_STRING:** içinde depolanan null sonlandırılan UTF-8 dize *nx_lwm2m_resource_stringdata.*

- **NX_LWM2M_RESOURCE_INTEGER32:** içinde depolanan 32 Bit tamsayı *nx_lwm2m_resource_integer32data.*

- **NX_LWM2M_RESOURCE_INTEGER64:** içinde depolanan 64 Bit tamsayı *nx_lwm2m_resource_integer64data.*

- **NX_LWM2M_RESOURCE_FLOAT32:** içinde depolanan 32 Bit Kayan Nokta *nx_lwm2m_resource_float32data.*

- **NX_LWM2M_RESOURCE_FLOAT64:** içinde depolanan 64 Bit Kayan Nokta *nx_lwm2m_resource_float64data.*

- **NX_LWM2M_RESOURCE_BOOLEAN:** içinde depolanan bir Boole *değeri nx_lwm2m_resource_booleandata.*

- **NX_LWM2M_RESOURCE_OPAQUE:** tarafından tanımlanan opak bir *nx_lwm2m_resource_bufferdata.*

- **NX_LWM2M_RESOURCE_OBJLNK:** içinde depolanan bir Nesne Bağlantısı *nx_lwm2m_resource_objlnkdata.*

- **NX_LWM2M_RESOURCE_TLV:** ile tanımlanan TLV kodlanmış *nx_lwm2m_resource_bufferdata.*

- **NX_LWM2M_RESOURCE_TEXT:** Plain-Text tarafından tanımlanan bir *kodlanmış* nx_lwm2m_resource_bufferdata.

- **NX_LWM2M_RESOURCE_MULTIPLE:** tarafından tanımlanan Birden Çok *Kaynak nx_lwm2m_resource_multipledata.* *nx_lwm2m_resource_multiple_ptr,* her Kaynak Örneği hakkında **bilgi NX_LWM2M_RESOURCE** bir dizi farklı yapının işaretçisidir.

- **NX_LWM2M_RESOURCE_MULTIPLE_TLV:** tarafından tanımlanan Birden Çok *Kaynak nx_lwm2m_resource_multipledata.* *nx_lwm2m_resource_multiple_ptr* TLV kodlanmış arabelleğinin işaretçisi.

Değeri almak ve türünü kontrol etmek için kullanışlı işlevler sağlanır.  Uygulama, nx_lwm2m_resource_value yapısından bir değer alırken hiçbir zaman NX_LWM2M_RESOURCE erişmez. Aşağıdaki işlevler tanımlanmıştır:

- ***nx_lwm2m_resource_get_:*** Verilen türe sahip bir değer elde.
- ***nx_lwm2m_resource_multiple_get_:*** Birden Çok Kaynak'tan verilen türe sahip bir değer elde.

Makro **NX_LWM2M_RESOURCE_IS_MULTIPLE**(tür) bir kaynak türünün Birden Çok Kaynak olup olduğunu kontrol etmek için kullanılabilir.

## <a name="object-implementation"></a>Nesne Uygulama

LWM2M İstemcisi zorunlu OMA LWM2M Nesnelerini kullanır: Güvenlik (0), Sunucu (1), Access Control (2) ve Cihaz (3). Cihaza özgü diğer nesneler uygulama tarafından uygulanarak uygulanarak.

Nesne tanımlamak için iki veri yapısı kullanılır: NX_LWM2M_OBJECT yapısı Nesne Kimliği ve nesne yöntemleri de dahil olmak üzere Nesne uygulamasını tanımlar ve NX_LWM2M_OBJECT_INSTANCE yapısı bir Nesne Örneğinin verilerini içerir.

Bu NX_LWM2M_OBJECT aşağıdaki tanımı içerir:

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

- **nx_lwm2m_object_next:** Listede sonraki nesne.
- **nx_lwm2m_object_id:** Nesne Kimliği.
- **nx_lwm2m_object_read:**'Read' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_discover:**'Discover' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_write:**'Write' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_execute:**'Execute' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_create:**'Create' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_delete:**'Delete' yöntemi, aşağıya bakın.
- **nx_lwm2m_object_instances:** Nesne örneklerinin NULL ile sonlandırılan listesi.

NX_LWM2M_OBJECT_INSTANCE yapısı aşağıdaki tanımlara sahiptir:

```c
typedef struct NX_LWM2M_OBJECT_INSTANCE_STRUCT
{
    NX_LWM2M_OBJECT_INSTANCE * nx_lwm2m_object_instance_next;
    NX_LWM2M_ID nx_lwm2m_object_instance_id;
} NX_LWM2M_OBJECT_INSTANCE;
```

- **nx_lwm2m_object_instance_next:** Listenin sonraki örneği.
- **nx_lwm2m_object_instance_id:** Nesne Örneği Kimliği.

Nesne LWM2M Cihaz Yönetimi Arabirimi tarafından tanımlanan işlemlere karşılık gelen yöntemleri uygulamalı: 'Okuma', 'Bulma', 'Yazma', 'Yürüt', 'Oluştur' ve 'Sil'. Nesne örneklerin dinamik olarak oluşturulmasını desteklemezse 'Oluştur' ve 'Sil' yöntemleri NULL olarak ayarilebilir.

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
