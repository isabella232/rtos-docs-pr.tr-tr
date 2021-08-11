---
title: Bölüm 3 - LWM2M İstemcisi İşlevsel Açıklaması
description: Bu bölümde LWM2M İstemcisi'nin işlevsel bir açıklaması yer almaktadır.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: be6d9d854ce89140ce749fbeb0364678077337bf19ddc1055d286d0f624e8bd5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783467"
---
# <a name="chapter-3--functional-description-of-lwm2m-client"></a>Bölüm 3 LWM2M İstemcisi İşlevsel Açıklaması

> Bu bölümde LWM2M İstemcisi'nin işlevsel bir açıklaması yer almaktadır.

## <a name="lwm2m-client-initialization"></a>LWM2M İstemci Başlatma

LWM2M İstemcisi, nx_lwm2m_client_create ***başlatılır.*** LWM2M İstemcisi kendi iş parçacığında çalışır ve geri çağırmaları kullanarak veya uygulama tarafından uygulanan özel nesnelerin yöntemlerini çağırarak uygulamaya bazı olayları bildirebilir.

Ayrıca LWM2M İstemci Oturumları, bir veya ***daha fazla nx_lwm2m_client_session_create*** iletişimin etkinleştirilmesi için özel çağrılarak oluşturularak oluşturulacak. Bir oturum iki farklı sunucu türüyle iletişim kurabilir: Bir Bootstrap Sunucusu veya LWM2M Sunucusu (Cihaz Yönetimi).

### <a name="bootstrap-server-session"></a>Bootstrap Sunucusu Oturumu

LWM2M İstemcisi'nin bir veya daha fazla LWM2M Sunucusuna "Kaydetme" işlemini gerçekleştirmesini sağlamak üzere LWM2M İstemcisine temel bilgileri sağlamak için Bootstrap Sunucusu ile bir iletişim oturumu kullanılır. Bu sunucu türü İstemci Tarafından Başlatılan ve Sunucu Tarafından Başlatılan Önyükleme modları sırasında kullanılır.

Uygulama * nx_lwm2m_client_session_bootstrap _ **veya** _*_nx_lwm2m_client_session_bootstrap_dtls_*_ çağırarak bir Bootstrap oturumu başlatabiliyor, sunucunun IP adresini ve bağlantı noktası numarasını ve isteğe bağlı bir Güvenlik Nesnesi Örneği Kimliğini sağlayabiliyor. Bu _*_nx_lwm2m_client_session_bootstrap_*_ güvenli olmayan iletişim kullanırken _ *_nx_lwm2m_client_session_bootstrap_dtls_** sunucuyla güvenli bir DTLS bağlantısı kurulmasını sağlar.

Bootstrap işlemi başarılı olursa, Bootstrap sunucusunun Bootstrap ve LWM2M Sunucuları için Güvenlik Nesnesi Örnekleri ve LWM2M Sunucuları için Sunucu Nesnesi Örnekleri oluşturması gerekir. Uygulama LWM2M ***Nx_lwm2m_client_session_register_info_get*** bilgilerini almak için nx_lwm2m_client_session_register_info_get'ı çağırarak LWM2M Sunucularla oturum kurmak için bu bilgileri kullanabilir.

Bootstrap verileri, cihazın bir sonraki yeniden başlatılmasında LWM2M İstemcisi'nin yapılandırılması için uygulama tarafından geçici olmayan belleğe kaydedılmalıdır.

### <a name="lwm2m-server-session"></a>LWM2M Sunucu Oturumu

Kayıt, Güvenlik Ve Hizmet Etkinleştirme için LWM2M Sunucusu ile Cihaz Yönetimi oturumu kullanılır.

Uygulama , ***nx_lwm2m_client_session_register** _ veya _*_nx_lwm2m_client_session_register_dtls_*_ çağırarak LWM2M İstemcisini bir sunucuya kaydedebilir, sunucunun IP adresini ve bağlantı noktası numarasını ve mevcut Sunucu Nesne Örneğine karşılık gelen Kısa Sunucu Kimliğini sağlasa gerekir. Bu _*_nx_lwm2m_client_session_register_*_ güvenli olmayan iletişim kullanırken _ *_nx_lwm2m_client_session_register_dtls_** sunucuyla güvenli bir DTLS bağlantısı kurulmasını sağlar.

Uygulama ***nx_lwm2m_client_session_deregister** _ çağırarak LWM2M İstemcisi'nin kaydını sildi ve _* nx_lwm2m_client_session_update ** çağrısıyla istemciden bir 'Güncelleştir'_iletisi göndermesini_ isteyebilir.

### <a name="session-state-callback"></a>Oturum Durumu Geri Çağırma

Uygulama, oturumun durumu güncelleştirildiğinde çağrılan bir oturumun oluşturulması sırasında bir geri çağırmayı kaydediyor. Geri çağırma **işlevi NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK** prototipe sahiptir.

typedef VOID ( \* NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK)(NX_LWM2M_CLIENT_SESSION \* session_ptr,UINT durumu);

Aşağıdaki eyaletler tanımlanmıştır.

| Oturum &nbsp; Durumu | Description |
| --- | --- |
| **NX_LWM2M_CLIENT_SESSION_INIT** | Oturum oluşturma sonrasındaki ilk durum. |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING** | İstemci , 'Kapalı Tut' süreölçeri veya Sunucu Tarafından Başlatılan Önyükleme'nin süresinin dolması için bekliyor. |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING** | İstemci, Bootstrap Sunucusuna bir 'İstek' iletisi gönderdi (İstemci Tarafından Başlatılan Bootstrap). |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED** | İstemci Bootstrap Sunucusundan veri alıyor. |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED** | Bootstrap Sunucusu bir 'Bitti' iletisi gönderdi. |
| **NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR** | Önyükleme oturumu başarısız oldu. |
| **NX_LWM2M_CLIENT_SESSION_REGISTERING** | İstemci LWM2M Sunucusuna bir 'Register' iletisi gönderdi. |
| **NX_LWM2M_CLIENT_SESSION_REGISTERED** | İstemci LWM2M Sunucusuna kaydedilir. |
| **NX_LWM2M_CLIENT_SESSION_UPDATING** | İstemci LWM2M Sunucusuna bir 'Güncelleştirme' iletisi gönderdi. |
| **NX_LWM2M_CLIENT_SESSION_DEREGISTERING** | İstemci, LWM2M Sunucusuna bir 'De-register' iletisi gönderdi. |
| **NX_LWM2M_CLIENT_SESSION_DEREGISTERED** | İstemci LWM2M Sunucusundan kaydı kaldırıldı. |
| **NX_LWM2M_CLIENT_SESSION_DISABLED** | LWM2M Sunucusu devre dışı bırakıldı. Devre dışı bırakma süreölçeri sona erdikten sonra bir 'Register' gönderilir. |
| **NX_LWM2M_CLIENT_SESSION_ERROR** | LWM2M Sunucusuna kayıt veya güncelleştirme işlemi başarısız oldu. |
| **NX_LWM2M_CLIENT_SESSION_DELETED** | LWM2M Sunucusuna karşılık gelen Sunucu Nesne Örneği silindi. |

Hata durumunda uygulama, hatanın nedenini almak için ***nx_lwm2m_client_session_error_get.***

## <a name="local-device-management"></a>Yerel Cihaz Yönetimi

Uygulama, yerel cihaz yönetimi işlevlerini kullanarak LWM2M İstemcisi Nesneleri'ne erişebilir. Aşağıdaki işlevler sağlanmıştır.

| İşlev &nbsp; Adı | Description |
| --- | --- |
| ***nx_lwm2m_client_object_read*** | Nesne Örneğinden kaynakları okuma. |
| ***nx_lwm2m_client_object_discover*** | Nesne Örneğinin kaynaklarının listesini al.
| ***nx_lwm2m_client_object_write*** | Bir Nesne Örneğine kaynak yazma. |
| ***nx_lwm2m_client_object_execute*** | Nesne Örneğinin kaynağında Yürütme işlemini gerçekleştirin. |
| ***nx_lwm2m_client_object_create*** | Yeni bir Nesne Örneği oluşturun. |
| ***nx_lwm2m_client_object_delete*** | Var olan bir Nesne Örneğini silin. |
| ***nx_lwm2m_client_object_next_get*** | LWM2M İstemcisi tarafından bir sonraki Nesne Kimliği'ne sahip olur. |
| ***nx_lwm2m_client_object_instance_next_get*** | Bir nesnenin sonraki Örneğini elde edersiniz. |

## <a name="resource-information"></a>Kaynak Bilgileri

Nesnelerden okuma ve Nesnelere yazma, kaynak yapısı tarafından NX_LWM2M_CLIENT_RESOURCE temsil eder. Bu yapı, Kaynağın/Örneğin kimliğini ve değerini içerir.

Kaynak bilgilerini ve değerini ayarlamaya için aşağıdaki işlevler sağlanmıştır.

| İşlev &nbsp; Adı | Description |
| --- | --- |
| ***nx_lwm2m_client_resource_info_set*** | Kaynak bilgilerini ayarlama: kaynak kimliği ve işlemi: OKUMA, YAZMA, YÜRÜTÜLEBILIR. |
| ***nx_lwm2m_client_resource_string_set*** | Kaynak değerini dize olarak ayarlayın. |
| ***nx_lwm2m_client_resource_integer32_set*** | Kaynak değerini 32 Bit tamsayı olarak ayarlayın. |
| ***nx_lwm2m_client_resource_integer64_set*** | Kaynak değerini 64 Bit tamsayı olarak ayarlayın. |
| ***nx_lwm2m_client_resource_float32_set*** | Kaynak değerini 32 Bit float olarak ayarlayın. |
| ***nx_lwm2m_client_resource_float64_set*** | Kaynak değerini 64 Bit float olarak ayarlayın. |
| ***nx_lwm2m_client_resource_boolean_set*** | Kaynak değerini boole olarak ayarlayın. |
| ***nx_lwm2m_client_resource_objlnk_set*** | Kaynak değerini nesne bağlantısı olarak ayarlayın. |
| ***nx_lwm2m_client_resource_opaque_set*** | Kaynak değerini donuk olarak ayarlayın. |
| ***nx_lwm2m_client_resource_instance_set*** | Birden çok kaynak için kaynak değerini örnek olarak ayarlayın. |
| ***nx_lwm2m_client_resource_dim_set*** | Bulma için birden çok kaynak için kaynak boyutunu ayarlayın. |

Kaynak bilgilerini ve değerini almak için aşağıdaki işlevler verilmiştir.

| İşlev &nbsp; adı | Description |
| --- | --- |
| ***nx_lwm2m_client_resource_info_get*** | Kaynak bilgilerini al: kaynak kimliği ve işlemi: okuma, yazma, ÇALıŞTıRıLABILIR. |
| ***nx_lwm2m_client_resource_string_get*** | Bir dize kaynağının değerini alır. |
| ***nx_lwm2m_client_resource_integer32_get*** | 32 bitlik bir tamsayı kaynağının değerini alır. |
| ***nx_lwm2m_client_resource_integer64_get*** | B4 bitlik bir tamsayı kaynağının değerini alır. |
| ***nx_lwm2m_client_resource_float32_get*** | 32 bitlik bir float kaynağının değerini alır. |
| ***nx_lwm2m_client_resource_float64_get*** | 64 bitlik bir float kaynağının değerini alır. |
| ***nx_lwm2m_client_resource_boolean_get*** | Boole kaynağının değerini alır. |
| ***nx_lwm2m_client_resource_objlnk_get*** | Bir nesne bağlantı kaynağının değerini alır. |
| ***nx_lwm2m_client_resource_opaque_get*** | Donuk bir kaynağın değerini alın. |
| ***nx_lwm2m_client_resource_instance_get*** | Birden çok kaynak için kaynak örneğini alın. |
| ***nx_lwm2m_client_resource_dim_get*** | Birden çok kaynak için kaynak boyutunu alın. |

## <a name="object-implementation"></a>Nesne uygulama

LWM2M Istemcisi zorunlu OMA LWM2M nesnelerini uygular: güvenlik (0), sunucu (1), Access Control (2) ve cihaz (3). Diğer cihaza özgü nesnelerin uygulama tarafından uygulanması gerekir.

Bir nesneyi tanımlamak için iki veri yapısı kullanılır: NX_LWM2M_CLIENT_OBJECT yapısı, nesne KIMLIĞI ve nesne yöntemleri de dahil olmak üzere nesne uygulamasını tanımlar ve NX_LWM2M_CLIENT_OBJECT_INSTANCE yapısı bir nesne örneğinin verilerini içerir.

Aşağıdaki işlevler verilmiştir.

| İşlev &nbsp; adı | Description |
| --- | --- |
| ***nx_lwm2m_client_object_add*** | LwM2M Istemcisine nesne uygulamasını ekleyin. |
| ***nx_lwm2m_client_object_remove*** | LwM2M Istemcisinden nesne uygulamasını kaldırın. |
| ***nx_lwm2m_client_object_instance_add*** | Nesneye nesne örneği ekleyin. |
| ***nx_lwm2m_client_object_instance_remove*** | Nesne örneğini nesneden kaldırın. |

Nesne yöntemi geri çağırma işlevinin aşağıda gösterilen imzası vardır.

```c
typedef UINT (*NX_LWM2M_CLIENT_OBJECT_OPERATION_CALLBACK)(
    UINT operation, 
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr,
    NX_LWM2M_CLIENT_RESOURCE *resource,
    UINT *resource_count,
    VOID *args_ptr,
    UINT args_length);
```

### <a name="the-read-method"></a>' Read ' yöntemi

' Read ' yöntemi, kaynak değerlerini bir nesne örneğinden okumak için kullanılır. Parametreleri aşağıdaki gibi tanımlanır.

| Parametre | Açıklama |
| --- | --- |
| **çalışmasını** | **NX_LWM2M_CLIENT_OBJECT_READ** |
| **object_ptr** | Nesne uygulamasına yönelik işaretçi. |
| **instance_ptr** | Nesne örneği işaretçisi. |
| **kaynak** | Okunacak kaynakların kimliklerini içeren **NX_LWM2M_CLIENT_RESOURCE** dizisine yönelik işaretçi. Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur. |
| **resource_count** | Okunacak kaynak sayısına yönelik işaretçi. |
| **args_ptr** | Okuma için kullanılmayan parametre. |
| **args_length** | Okuma için kullanılmayan parametre. |

### <a name="the-discover-method"></a>' Keşfet ' yöntemi

' Keşfet ' yöntemi, bir nesne tarafından uygulanan tüm kaynakların listesini almak için kullanılır. Parametreleri aşağıdaki gibi tanımlanır.

| Parametre | Açıklama |
| --- | --- |
| **çalışmasını** | **NX_LWM2M_CLIENT_OBJECT_DISCOVER** |
| **object_ptr** | Nesne uygulamasına yönelik işaretçi. |
| **instance_ptr** | Nesne örneği işaretçisi. |
| **kaynak** | NX_LWM2M_CLIENT_RESOURCE dizisine yönelik işaretçi. Dönüş sırasında dizi karşılık gelen kaynak bilgileriyle doldurulur. |
| **resource_count** | Bulunacak kaynak sayısına yönelik işaretçi. Dönüş sırasında bu parametrenin doğru değer olarak güncellenmesi gerekir. |
| **args_ptr** | Bulma için kullanılmamış parametre. |
| **args_length** | Bulma için kullanılmamış parametre. |

### <a name="the-write-method"></a>' Write ' yöntemi

' Write ' yöntemi, bir nesne örneğinin kaynaklarını güncelleştirmek veya değiştirmek için kullanılır. Parametreleri aşağıdaki gibi tanımlanır.

| Parametre  | Açıklama |
| --- | --- |
| **çalışmasını** | **NX_LWM2M_CLIENT_OBJECT_WRITE** |
| **object_ptr** | Nesne uygulamasına yönelik işaretçi. |
| **instance_ptr** | Nesne örneği işaretçisi. |
| **kaynak** | Okunan kaynakların **NX_LWM2M_CLIENT_RESOURCE** içeren bir dizi dosyanın işaretçisi. dönüşte, dizi karşılık gelen türler ve değerlerle doldurulur. |
| **resource_count** | Keşfedilen kaynak sayısının işaretçisi. |
| **args_ptr** | Bayraklar yazın. |
| **args_length** | Bağımsız değişkenlerin uzunluğu. |

Aşağıdaki yazma işlemleri flag parametresine *belirtilebilir.*

| İşlem | Eylem | Açıklama |
| --- | ---| --- |
| 0 | Kısmi Güncelleştirme | Sağlanan kaynakları yeni değere ekler veya günceller ve diğer mevcut Kaynakları olduğu gibi bırakır.
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE** | Örneği Değiştir | Nesne Örneğini yeni sağlanan kaynak değerleriyle değiştirir.
| **NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE** |  Kaynağı Değiştir | Resources yerine sağlanan yeni kaynak değerlerini (Birden Çok Kaynağı değiştirmek için kullanılır) değiştirir. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_CREATE** | Örnek Oluşturma | Yeni oluşturulan Nesne Örneğini sağlanan kaynak değerleriyle (nx_lwm2m_object_create **_yönteminden çağrılır)_** başlatılır. |
| **NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP** | Bootstrap Yazma | Bootstrap sırasında çağrılır. |

### <a name="the-execute-method"></a>'Execute' Yöntemi

'Execute' yöntemi, nesne kaynağının yürütülmesini sağlar.

Giriş parametreleri aşağıdaki gibi tanımlanır.

| Parametre  | Açıklama |
| --- | --- |
| **Işlem** | NX_LWM2M_CLIENT_OBJECT_EXECUTE |
| **object_ptr** | Nesne uygulaması işaretçisi. |
| **instance_ptr** | Nesne Örneğinin işaretçisi. |
| **kaynak** | Okunan kaynakların **NX_LWM2M_CLIENT_RESOURCE** içeren bir dizi dosyanın işaretçisi. dönüşte, dizi karşılık gelen türler ve değerlerle doldurulur. |
| **resource_count** | Keşfedilen kaynak sayısının işaretçisi. |
| **args_ptr** | Bağımsız değişkenlerin işaretçisi. |
| **args_length** | Bağımsız değişkenlerin uzunluğu.  |

Kaynak kimliği **NX_LWM2M_CLIENT_NOT_FOUND** işlevi, yürütmeyi **desteklemezse NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** işlevinin bir geri dönüş koduna sahip olması gerekir.

### <a name="the-create-method"></a>'Create' Yöntemi

'Create' yöntemi, yeni bir Nesne Örneği oluşturma işlemi gerçekleştirin.

Giriş parametreleri aşağıdaki gibi tanımlanır.

| Parametre  | Açıklama |
| --- | --- |
| **Işlem** | **NX_LWM2M_CLIENT_OBJECT_CREATE** |
| **object_ptr** | Nesne uygulaması işaretçisi. |
| **instance_ptr** | Kullanılmayan parametre. |
| **kaynak** | Okunan kaynakların **NX_LWM2M_CLIENT_RESOURCE** içeren bir dizi dosyanın işaretçisi. dönüşte, dizi karşılık gelen türler ve değerlerle doldurulur. |
| **resource_count** | Keşfedilen kaynak sayısının işaretçisi. |
| **args_ptr** | Nesne örneği kimliği. |
| **args_length** | Bağımsız değişkenlerin uzunluğu. |

### <a name="the-delete-method"></a>'Delete' Yöntemi

'Delete' yöntemi bir nesne örneğinin silinmesini sağlar, giriş parametreleri aşağıdaki gibi tanımlanır.

| Parametre  | Açıklama |
| --- | --- |
| **Işlem** | NX_LWM2M_CLIENT_OBJECT_DELETE |
| **object_ptr** | Nesne uygulaması işaretçisi. |
| **instance_ptr** | Nesne Örneğinin işaretçisi. |
| **kaynak** | Kullanılmayan parametre. |
| **resource_count** | Kullanılmayan parametre. |
| **args_ptr** | Kullanılmayan parametre. |
| **args_length** | Kullanılmayan parametre. |

Başarılı olması için Nesne, Nesne Örneği verilerini ve örnek tarafından ayrılan diğer tüm kaynakları serbest bırakmalı.

## <a name="example-of-lwm2m-client-application"></a>LWM2M İstemci Uygulaması Örneği

Aşağıdaki kod, sıcaklık sensörü ve ışık anahtarı bulunan özel bir cihaz uygulayan basit bir LWM2M İstemci Uygulaması örneğidir.

Cihaz, bir sunucunun sıcaklık algılayıcısı değerini ve ışık anahtarının boole durumunu okumasını ve ışık anahtarını açık/kapalı olarak ayarlamasını sağlar.

```c
#include "nx_lwm2m_client.h"


/* Custom Object implementation. */

/* Temperature Object ID and resource IDs. */
#define IPSO_TEMPERATURE_OBJECT_ID   3303

#define IPSO_RESOURCE_MIN_VALUE      5601
#define IPSO_RESOURCE_MAX_VALUE      5602
#define IPSO_RESOURCE_RESET_MINMAX   5605
#define IPSO_RESOURCE_VALUE          5700
#define IPSO_RESOURCE_UNITS          5701

/* Actuation Object ID and resource IDs. */
#define IPSO_ACTUATION_OBJECT_ID     3306

#define IPSO_RESOURCE_ONOFF          5850

/* Define the Temperature Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_CLIENT_OBJECT_INSTANCE    object_instance;

    /* Resources Data */
    NX_LWM2M_FLOAT32                   temperature;
    NX_LWM2M_FLOAT32                   min_temperature;
    NX_LWM2M_FLOAT32                   max_temperature;

} IPSO_TEMPERATURE_INSTANCE;

/* Define the Actuation Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_CLIENT_OBJECT_INSTANCE    object_instance;

    /* Resources Data */
    NX_LWM2M_BOOL                      onoff;

} IPSO_ACTUATION_INSTANCE;

/* IPSO Temperature */
/* Define the 'Read' Method */
UINT ipso_temperature_read(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count)
{
IPSO_TEMPERATURE_INSTANCE *temp = ((IPSO_TEMPERATURE_INSTANCE *) instance_ptr);
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_MIN_VALUE:

            /* return the minimum measured temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> min_temperature);
            break;

        case IPSO_RESOURCE_MAX_VALUE:

            /* return the maximum measured temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> max_temperature);
            break;

        case IPSO_RESOURCE_VALUE:

            /* return the temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> temperature);
            break;

        case IPSO_RESOURCE_RESET_MINMAX:

            /* Not readable */
            return(NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED);

        case IPSO_RESOURCE_UNITS:

            /* return the temperature units */
            nx_lwm2m_client_resource_string_set(&resource[i], "Cel", 3);
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}

/* Define the 'Discover' method */
UINT ipso_temperature_discover(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resources, UINT *resource_count)
{
    if (*resource_count < 5)
    {
        return(NX_LWM2M_CLIENT_BUFFER_TOO_SMALL);
    }

    /* return the list of supported resources IDs */
    *resource_count = 5;
    nx_lwm2m_client_resource_info_set(&resources[0], IPSO_RESOURCE_MIN_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[1], IPSO_RESOURCE_MAX_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[2], IPSO_RESOURCE_RESET_MINMAX, NX_LWM2M_CLIENT_RESOURCE_OPERATION_EXECUTABLE);
    nx_lwm2m_client_resource_info_set(&resources[3], IPSO_RESOURCE_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[4], IPSO_RESOURCE_UNITS, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);

    return(NX_SUCCESS);
}

/* Define the 'Execute' method */
UINT ipso_temperature_execute(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, const CHAR *args_ptr, UINT args_length)
{
IPSO_TEMPERATURE_INSTANCE *temp = ((IPSO_TEMPERATURE_INSTANCE *) instance_ptr);
NX_LWM2M_CLIENT_RESOURCE value;
NX_LWM2M_ID resource_id;

    /* Get resource id */
    nx_lwm2m_client_resource_info_get(resource, &resource_id, NX_NULL);

    switch (resource_id)
    {

    case IPSO_RESOURCE_MIN_VALUE:
    case IPSO_RESOURCE_MAX_VALUE:
    case IPSO_RESOURCE_VALUE:
    case IPSO_RESOURCE_UNITS:

        /* read-only resource */
        return(NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED);

    case IPSO_RESOURCE_RESET_MINMAX:

        /* reset min/max values to current temperature */
        nx_lwm2m_client_resource_float32_set(&value, temp -> temperature);
        if (temp -> min_temperature != temp -> temperature)
        {
            temp -> min_temperature = temp -> temperature;
            nx_lwm2m_client_resource_info_set(&value, IPSO_RESOURCE_MIN_VALUE, NX_NULL);
            nx_lwm2m_client_object_resource_changed(object_ptr, instance_ptr, &value);
        }
        if (temp -> max_temperature != temp -> temperature)
        {
            temp -> max_temperature = temp -> temperature;
            nx_lwm2m_client_resource_info_set(&value, IPSO_RESOURCE_MAX_VALUE, NX_NULL);
            nx_lwm2m_client_object_resource_changed(object_ptr, instance_ptr, &value);
        }

        break;

    default:

        /* unknown resource ID */
        return(NX_LWM2M_CLIENT_NOT_FOUND);
    }

    return(NX_SUCCESS);
}

/* Define the operation callback function of Temperature Object */
UINT ipso_temperature_operation(UINT operation, NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT *resource_count, VOID *args_ptr, UINT args_length)
{

    switch (operation)
    {
    case NX_LWM2M_CLIENT_OBJECT_READ:

        /* Call read function */
        return ipso_temperature_read(object_ptr, object_instance_ptr, resource, *resource_count);
    case NX_LWM2M_CLIENT_OBJECT_DISCOVER:

        /* Call discover function */
        return ipso_temperature_discover(object_ptr, object_instance_ptr, resource, resource_count);

    case NX_LWM2M_CLIENT_OBJECT_EXECUTE:

        /* Call execute function */
        return ipso_temperature_execute(object_ptr, object_instance_ptr, resource, args_ptr, args_length);
    default:

        /*Unsupported operation */
        return(NX_LWM2M_CLIENT_NOT_SUPPORTED);
    }
}


/* IPSO Actuation */
/* Define the 'Read' Method */
UINT ipso_actuation_read(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count)
{
IPSO_ACTUATION_INSTANCE *act = ((IPSO_ACTUATION_INSTANCE *) instance_ptr);
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_ONOFF:

            /* return the on/off value */
            nx_lwm2m_client_resource_boolean_set(&resource[i], act -> onoff);
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}


/* Define the 'Discover' method */
UINT ipso_actuation_discover(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resources, UINT *resource_count)
{
    if (*resource_count < 1)
    {
        return(NX_LWM2M_CLIENT_BUFFER_TOO_SMALL);
    }

    /* return the list of supported resources IDs */
    *resource_count = 1;
    nx_lwm2m_client_resource_info_set(&resources[0], IPSO_RESOURCE_ONOFF, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ_WRITE);

    return(NX_SUCCESS);
}

/* Define the 'Write' method */
UINT ipso_actuation_write(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count, UINT flags)
{
IPSO_ACTUATION_INSTANCE *act = ((IPSO_ACTUATION_INSTANCE *) instance_ptr);
UINT ret;
NX_LWM2M_BOOL onoff;
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_ONOFF:

            /* assign on/off boolean value */
            ret = nx_lwm2m_client_resource_boolean_get(&resource[i], &onoff);
            if (ret != NX_SUCCESS)
            {
                /* invalid value type */
                return(ret);
            }
            if (onoff != act->onoff)
            {
                act->onoff = onoff;

                printf("Set actuation switch %s\n", onoff ? "On" : "Off");
            }
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}

/* Define the operation callback function of Actuation Object */
UINT ipso_actuation_operation(UINT operation, NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT *resource_count, VOID *args_ptr, UINT args_length)
{
UINT write_op;

    switch (operation)
    {
    case NX_LWM2M_CLIENT_OBJECT_READ:

        /* Call read function */
        return ipso_actuation_read(object_ptr, object_instance_ptr, resource, *resource_count);
    case NX_LWM2M_CLIENT_OBJECT_DISCOVER:

        /* Call discover function */
        return ipso_actuation_discover(object_ptr, object_instance_ptr, resource, resource_count);
    case NX_LWM2M_CLIENT_OBJECT_WRITE:

        /* Get the type of write operation */
        write_op = *(UINT *)args_ptr;

        /* Call write function */
        return ipso_actuation_write(object_ptr, object_instance_ptr, resource, *resource_count, write_op);
    default:

        /* Unsupported operation */
        return(NX_LWM2M_CLIENT_NOT_SUPPORTED);
    }
}


/* NetX data.  */
NX_IP                   ip_0;
NX_PACKET_POOL          pool_0;

/* LWM2M Client data.  */
NX_LWM2M_CLIENT         client;
ULONG                   client_stack[4096 / sizeof(ULONG)];
NX_LWM2M_CLIENT_SESSION session;

/* Objects and instances.  */
NX_LWM2M_CLIENT_OBJECT      temperature_object;
NX_LWM2M_CLIENT_OBJECT      actuation_object;
IPSO_TEMPERATURE_INSTANCE   temperature_instance;
IPSO_ACTUATION_INSTANCE     actuation_instance;

/* Define the session state callback */
void session_callback(NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state)
{
    printf("LWM2M Callback: -> %d\n", state);

    switch (state)
    {

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING:

        printf("Start client initiated bootstrap\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED:

        printf("Got message from boostrap server\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:

         /* Bootstrap session done, we can register to the LWM2M Server */
        printf( "Boostrap finished.\n");
#ifdef BOOTSTRAP
        tx_semaphore_put(&semaphore_bootstarp_finish);
#endif
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:

        /* Failed to Bootstrap the LWM2M Client. */
        printf( "Failed to boostrap device, error=%02x\n", nx_lwm2m_client_session_error_get(session_ptr));
        break;

    case NX_LWM2M_CLIENT_SESSION_REGISTERED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device registered.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_DISABLED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device disabled.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_DEREGISTERED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device deregistered.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_ERROR:

        /* Failed to register to the LWM2M Client. */
        printf( "Failed to register device, error=%02x\n", nx_lwm2m_client_session_error_get(session_ptr));
        break;
    }
}


/* Application main thread */
void application_thread(ULONG info)
{

UINT status;
NX_LWM2M_ID server_id = 0;
NXD_ADDRESS server_addr;
CHAR *server_uri = NX_NULL;
UINT server_uri_len = 0;
UCHAR security_mode = 0;
   
    /* Create the LWM2M client */
    status = nx_lwm2m_client_create(&client, &ip_0, &pool_0, "nxlwm2mclient", sizeof("nxlwm2mclient") - 1, NX_NULL, 0, NX_LWM2M_CLIENT_BINDING_U, client_stack, sizeof(client_stack), 4);
    if (status)
    {
        return;
    }

    /* Define our custom objects: */
    /* Add Temperature Object */
    status = nx_lwm2m_client_object_add(&client, &temperature_object, IPSO_TEMPERATURE_OBJECT_ID, ipso_temperature_operation);
    if (status)
    {
        return;
    }

    /* Define a single instance */
    temperature_instance.temperature = 22.5f;
    temperature_instance.min_temperature = temperature_instance.temperature;
    temperature_instance.max_temperature = temperature_instance.temperature;
    status = nx_lwm2m_client_object_instance_add(&temperature_object, &temperature_instance.object_instance, NX_NULL);
    if (status)
    {
        return;
    }

    /* Add Actuation Object */
    status = nx_lwm2m_client_object_add(&client, &actuation_object, IPSO_ACTUATION_OBJECT_ID, ipso_actuation_operation);
    if (status)
    {
        return;
    }

    /* Define a single instance */
    actuation_instance.onoff = NX_FALSE;
    status = nx_lwm2m_client_object_instance_add(&actuation_object, &actuation_instance.object_instance, NX_NULL);
    if (status)
    {
        return;
    }

    /* Create a session */
    status = nx_lwm2m_client_session_create(&session, &client, session_callback);
    if (status)
    {
        return;
}

    /* Set bootstrap server address.  */
    server_addr.nxd_ip_version = NX_IP_VERSION_V4;
    server_addr.nxd_ip_address.v4 = IP_ADDRESS(23, 97, 187, 154);

    printf("Start boostraping\r\n");
    status = nx_lwm2m_client_session_bootstrap(&session, 0, &server_addr, 5783);
    if (status)
    {
        return;
    }

    status = nx_lwm2m_client_session_register_info_get(&session, NX_LWM2M_CLIENT_RESERVED_ID, &server_id, &server_uri, &server_uri_len, &security_mode, NX_NULL, NX_NULL, NX_NULL, NX_NULL, NX_NULL, NX_NULL);
    if (status || (security_mode != NX_LWM2M_CLIENT_SECURITY_MODE_NOSEC))
    {
        return;
    }

printf("Register to LWM2M server\r\n");
status = nx_lwm2m_client_session_register(&session, server_id, &server_addr, 5683);

    if (status)
    {
        return;
    }

    /* Application main loop */
    while (1)
    {

        /* application code... */
        tx_thread_sleep(NX_IP_PERIODIC_RATE);
    }

    /* Terminate the LWM2M Client */
    nx_lwm2m_client_delete(&client);
}

```