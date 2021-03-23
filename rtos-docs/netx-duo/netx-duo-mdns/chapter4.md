---
title: Bölüm 4-mDNS hizmetlerinin açıklaması
description: Bu bölümde tüm NetX mDNS hizmetlerinin açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 89df0ab5f09be8ad50a27d23bae8b20d71caa0b4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825918"
---
# <a name="chapter-4---description-of-mdns-services"></a>Bölüm 4-mDNS hizmetlerinin açıklaması

Bu bölüm tüm NetX mDNS hizmetlerinin (aşağıda listelenmiştir) bir açıklamasını içerir.

> [!NOTE]
> Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

## <a name="nx_mdns_create"></a>nx_mdns_create

MDNS örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_create(NX_MDNS *mdns_ptr, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool,
    UINT priority, VOID *stack_ptr,
    UINT stack_size, UCHAR *host_name,
    VOID *local_service_cache,
    UINT local_service_cache_size,
    VOID *peer_service_cache,
    UINT peer_service_cache_size,
    VOID (*probing_notify)(NX_MDNS *mdns_ptr,
        UCHAR *name, UINT probing_state));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirli IP örneğinde ve ilişkili kaynaklarda bir mDNS örneği oluşturur. Ayrıca, gelen mDNS iletilerini işlemek, sorgulara yanıt vermek ve sorgu iletilerini düzenli olarak iletmek için bir iş parçacığı oluşturulur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **ip_ptr** İlişkili IP örneğine yönelik işaretçi.
- **packet_pool** Geçerli bir paket havuzu işaretçisi.
- **Öncelik** MDNS iş parçacığının önceliği.
- **stack_ptr** MDNS iş parçacığı için yığın alanı işaretçisi
- **stack_size** Yığın alanının boyutu.
- **host_name** Bu düğüme atanan konak adı.
- **local_service_cache** Yerel kayıtlı hizmetler için depolama alanı.
- **local_service_cache_size** Yerel hizmet önbelleğinin boyutu.
- **peer_service_cache** Alınan hizmet bilgileri için depolama alanı
- **peer_service_cache_size** Eş hizmeti önbelleğinin boyutu
- **probing_notify** Araştırma işleminin sonunda çağrılan isteğe bağlı geri çağırma işlevi. Ana bilgisayar adı (yerel bir arabirimde mDNS etkinleştirildiğinde) veya hizmet adı (hizmet kaydedildikten sonra) benzersiz olup olmadığını uygulamaya bildirir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) mdıdns örneğini başarıyla oluşturdu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
UCHAR stack_ptr[2048];
UCHAR local_cache_ptr[2048];
UCHAR peer_cache_ptr[8192];

/* Create a mDNS instance. */
status = nx_mdns_create(&my_mdns, &ip_0, &pool_0,
    3, stack_ptr, 2048,
    “NETX-MDNS-HOST”,
    local_cache_ptr, 2048,
    peer_cache_ptr, 8192,
    probing_notify);

/* If status is NX_SUCCESS, mDNS instance was created. */
```

## <a name="nx_mdns_delete"></a>nx_mdns_delete

MDNS örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_delete(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, mDNS örneğini siler ve kaynaklarını serbest bırakır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00), MDNs örneğini başarıyla sildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete a previously created mDNS instance. */

status = nx_mdns_delete(&my_mdns);

/* If status is NX_SUCCESS, the mDNS instance has been deleted. */
```

## <a name="nx_mdns_enable"></a>nx_mdns_enable

MDNS hizmetini başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_enable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu API, belirli fiziksel arabirimde mDNS hizmetini mümkün bir şekilde sunar. Hizmet etkinleştirildikten sonra, mDNS modülü, arabirimde alınan sorgulara yanıt vermeden önce ağ üzerindeki tüm benzersiz hizmet adlarını yoklamaları.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS örnek denetimi bloğuna yönelik işaretçi.
- **interface_index** Hizmetin etkinleştirildiği arabirimin dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) hizmeti başarıyla etkinleştirdi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Enable mDNS service on specific interface. */

status = nx_mdns_enable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was enabled. */
```

## <a name="nx_mdns_disable"></a>nx_mdns_disable

MDNS hizmetini devre dışı bırakma

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_disable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu API, belirli fiziksel arabirimde mDNS hizmetini devre dışı bırakır. Hizmet devre dışı bırakıldıktan sonra, mDNS her yerel hizmet için arabirime bağlı olan ağa "güle" iletileri gönderir, böylece komşu düğümler bilgilendirilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **interface_index** Hizmetin devre dışı bırakıldığı arabirimin dizini

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) hizmeti başarıyla devre dışı bıraktı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Disable mDNS service on specific interface. */

status = nx_mdns_disable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was disabled. */
```

## <a name="nx_mdns_cache_notify_set"></a>nx_mdns_cache_notify_set

MDNS önbelleği tam bildirim işlevini yükleme

### <a name="prototype"></a>Prototype

```c
UINT nx_mdns_cache_notify_set(NX_MDNS *mdns_ptr,
    VOID (*cache_full_notify_cb)(NX_MDNS *mdns_ptr,
        UINT state, UINT cache_type));
```

### <a name="description"></a>Açıklama

Bu hizmet, yerel hizmet önbelleği veya eş hizmet Önbelleği dolduğunda çağrılan, Kullanıcı tarafından sağlanan bir geri çağırma işlevi yüklüyor. Hizmet Önbelleği dolduğunda, daha fazla mDNS kaynak kaydı eklenemez. Farklı dize uzunluklarına sahip hizmetler eklendiğinde ve kaldırıldığında, hizmet önbelleğinin iç parçalanma sonucu olarak tam hale gelebileceğini unutmayın. Eş hizmeti önbelleğinde önbellek tam bildirimi alındığında, uygulama "*nx_mdns_service_cache_clear"* hizmetini kullanarak eş hizmeti önbelleğindeki tüm girdileri silebilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) MDNs önbellek bildirimi geri arama işlevini başarıyla yükledi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set mDNS cache notify callback. */

status = nx_mdns_cache_notify_set(&my_mdns, cache_full_nofiy_cb);

/* If status is NX_SUCCESS, mDNS cache notify callback was set. */
```

## <a name="nx_mdns_cache_notify_clear"></a>nx_mdns_cache_notify_clear

MDNS hizmet önbelleği tam bildirim işlevini temizle

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_cache_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, Kullanıcı tarafından sağlanan bir hizmet önbelleği bildirme geri arama işlevini temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğuna yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00), MDNs hizmeti önbellek bildirimi geri arama işlevini başarıyla temizledi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Clear mDNS cache notify callback. */

status = nx_mdns_cache_notify_clear(&my_mdns);

/* If status is NX_SUCCESS, mDNS cache notify callback clear. */
```

## <a name="nx_mdns_domain_name_set"></a>nx_mdns_domain_name_set

Etki alanı adını ayarlar

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_domain_name_set(NX_MDNS *mdns_ptr, CHAR *domain_name);
```

### <a name="description"></a>Açıklama

Bu hizmet varsayılan yerel etki alanı adını ayarlar. MDNS örneği oluşturulduğunda, varsayılan yerel etki alanı adı ". Local" olarak ayarlanır. Bu API, bir uygulamanın varsayılan yerel etki alanı adının üzerine yazılmasına izin verir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **domain_name** Kullanılacak etki alanı adı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) yerel etki alanı başarıyla yapılandırıldı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the domain name. */

status = nx_mdns_domain_name_set(&my_mdns, “home”);

/* If status is NX_SUCCESS, the “home” domain name was set. */
```

## <a name="nx_mdns_service_announcement_timing_set"></a>nx_mdns_service_announcement_timing_set

Hizmet duyurusu iletileri için zamanlama parametrelerini ayarlar

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_announcement_timing_set(NX_MDNS *mdns_ptr,
    UINT t, UINT p, UINT k, UINT retrans_interval,
    UINT period_interval, UINT max_time);
```

### <a name="description"></a>Açıklama

Bu hizmet, hizmet duyuruları gönderilirken mDNS tarafından çalıştırılan zamanlama parametrelerini yeniden yapılandırır. Yayımlama dönemi *t* işaretleri ' nden başlar ve *k* faktörü 'nin gücünden 2 ile telescop'e göre genişletilebilir. Tanıtım başına gün sayısı *p*, yinelenen her reklam arasındaki Aralık *Aralık* işaretleri ve duyuru dönemi sayısı max_time. Varsayılan olarak, başlangıç dönemi 1 saniye, k = 1 ile ayarlanır (her seferinde nokta iki katına çıkar), *p = 1* (yineleme yok), retrans_interval = 0 (zaman aralığı yok), Period_interval = 0xFFFFFFFF (en fazla süre aralığı) ve max_time = 3 (reklam sayısı).

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- başlangıç dönemi için **t** onay işareti sayısı. 1 saniye için varsayılan değer 100 ' dir.
- **p** Tekrarlamaların sayısı. Varsayılan değer 1 ' dir.
- **k** Telescopic faktörü. Varsayılan değer 1 ' dir.
- **retrans_interval** Yinelenen duyuru iletileri gönderilmeden önce beklenecek onay işareti sayısı. Varsayılan değer 0 ' dır.
- **period_interval** İki duyuru dönemi arasındaki onay işareti sayısı. Varsayılan değer 0xFFFFFFFF ' dir.
- **max_time** Tanıtım için kullanılacak duyuru dönemi sayısı. *Max_time* duyuru dönemlerinde daha fazla duyuru iletisi gönderilmez. Varsayılan değer 3’tür.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) zamanlama değerlerini başarıyla ayarlıyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the service announcement timing. */

status = nx_mdns_service_announcement_timing_set(&my_mdns, 100,
    1, 1, 0, 0xFFFFFFFF, 3);

/* If status is NX_SUCCESS, the service announcement timing was set. */
```

## <a name="nx_mdns_service_add"></a>nx_mdns_service_add

Yerel hizmet ekleme

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_add(NX_MDNS *mdns_ptr, CHAR *instance,
    CHAR *service, CHAR *subtype, UINT ttl, USHORT priority,
    USHORT weight, USHORT port, UCHAR *text, UCHAR is_unique,
    UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu API, uygulama tarafından sunulan bir hizmeti kaydeder. Bayrak *is_unique* ayarlandıysa, MDNs, ağdaki hizmeti duyurmadan önce yerel ağda benzersiz olduğundan emin olmak için hizmet adını yoklayın. *Örnek* , hizmet adının örnek bölümüdür. Hizmet *,* hizmet adının hizmet bölümüdür. Örneğin, "_HTTP. _tcp" bir hizmettir. Alt türe sahip bir hizmeti anlatmak için çağıranın *Subtype* parametresini kullanması gerekir. Örneğin, istenen hizmet "_printer. _sub. _HTTP. _tcp" ise, hizmet alanı "_HTTP. _tcp:" ve alt tür alanı "_printer" olur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **örnek** Hizmetin örnek adına yönelik işaretçi.
- **hizmet** Alt tür bilgileri hariç mDNS hizmet türüne yönelik işaretçi.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.
- **Öncelik** Hizmet önceliği
- **ağırlığı** Hizmet ağırlığı
- **bağlantı noktası** Hizmetin kullandığı TCP veya UDP bağlantı noktası numarası
- **metin** Ek metin bilgileri
- **is_unique** Hizmetin paylaşılıp paylaşılmadığını veya benzersiz olduğunu belirten Boole bayrağı. Benzersiz olarak kaydedilen hizmetler için mDNS, servisi sunmaya başlamadan önce ağdaki hizmeti araştırmalıdır.
- **Interface_index** Hizmetin sunduğu fiziksel arabirim. İliştirilmiş hizmetlerden herhangi biri üzerinden sunulan bir hizmet için *NX_MDNS_ALL_INTERFACES* değer kullanılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) hizmet başarıyla kaydedildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Add local service. */

status = nx_mdns_service_add(&my_mdns, “NETX-SERVICE”,
    “_http._tcp”, NX_NULL,
    NX_NULL, 0, 0, 0, 80, NX_TRUE, 0);

/* If status is NX_SUCCESS, The service (NetX-SERVICE._http._tcp.local) was added. */
```

## <a name="nx_mdns_service_delete"></a>nx_mdns_service_delete

Önceki kayıtlı bir hizmeti Kaldır

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_delete(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service,
    CHAR *subtype);
```

### <a name="description"></a>Açıklama

Bu API, önceki kayıtlı bir hizmeti siler. Hizmet silindiğinden, komşu düğümlerin bildirilmesi için yerel ağa "güle" iletileri gönderilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **örnek** Hizmetin örnek adına yönelik işaretçi.
- **hizmet** Alt tür bilgileri hariç mDNS hizmet türüne yönelik işaretçi.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) hizmeti başarıyla sildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete local service. */

status = nx_mdns_service_delete(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The service (NetX-SERVICE._http._tcp.local) was deleted. */
```

## <a name="nx_mdns_service_one_shot_query"></a>nx_mdns_service_one_shot_query

Tek basamaklı hizmet bulma başlatın

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_one_shot_query(NX_MDNS *mdns_ptr,
    UCHAR *instance,
    UCHAR *service,
    UCHAR *subtype,
    NX_MDNS_SERVICE *service_ptr, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, tek seferlik bir mDNS sorgusu gerçekleştirir. Belirtilen hizmet eş hizmeti önbelleğinde bulunursa, ilk örnek döndürülür. Yerel eş hizmeti önbelleğinde hiçbir hizmet bulunmazsa, mDNS modülü bir sorgu komutu yayınlar ve yanıt bekler. İlk yanıt alınana veya sorgu zaman aşımına uğrayana kadar hizmet engellenir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **örnek** Varsa hizmetin örnek adının işaretçisi.
- **hizmet** Alt tür bilgileri hariç mDNS hizmet türüne yönelik işaretçi. uygulamanın hizmet türünü belirtmesi gerekir.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.
- **service_ptr** Kullanıcı tarafından sorgu sonuçlarını depolayan NX_MDNS_SERVICE yapısına yönelik işaretçi.
- **wait_option** Bir yanıt için beklemek için zaman işaretleri cinsinden süre miktarı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) hizmet bilgilerini başarıyla aldı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start service one shot query. */

status = nx_mdns_service_one_shot_query(&my_mdns, “NETX-SERVICE”, “_http._tcp”,
    NX_NULL, service_ptr, 500);

/* If status is NX_SUCCESS, The query with
    name: NetX-SERVICE._http._tcp.local,
     type: ANY (SRV and TXT) was sent.
    And the answer was stored in service_ptr if success. */
```

## <a name="nx_mdns_service_continuous_query"></a>nx_mdns_service_continuous_query

Sürekli hizmet bulmayı Başlat

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_continous_query(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a>Açıklama

Bu hizmet sürekli bir sorgu başlatır. Hizmetin hemen geri döndüğünü unutmayın. Sürekli bir sorgu yayınladıktan sonra, uygulama API *nx_mdns_service_lookup* kullanarak hizmet kaydını alabilir. Sürekli sorguyu durdurmak için, uygulama API 'YI kullanabilir *nx_mdns_service_query_stop*

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **örnek** Varsa hizmetin örnek adının işaretçisi.
- **hizmet** Varsa, alt tür bilgisi hariç olmak üzere mDNS hizmet türüne yönelik işaretçi.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarıyla başlatıldı sorgusu devam ediyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start service continuous query. */

status = nx_mdns_service_continuous_query(&my_mdns,
    “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The continuous query with
    name: NetX-SERVICE._http._tcp.local,
    type: ANY (SRV and TXT) was added.
    And the query will be periodically sent. */
```

## <a name="nx_mdns_service_query_stop"></a>nx_mdns_service_query_stop

Daha önce verilen bir sürekli hizmet bulmayı sona erdirin

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_query_stop(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a>Açıklama

Bu API, önceki yayımlanmış bir sürekli hizmet bulmayı sonlandırır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **örnek** Hizmetin örnek adına yönelik işaretçi.
- **hizmet** MDNS hizmet türü, alt tür bilgisi işaretçisi.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) devam eden sorgu başarıyla durduruldu.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Stop service continuous query. */

status = nx_mdns_service_query_stop(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The continuous query with
    name: NetX-SERVICE._http._tcp.local,
    type: ANY (SRV and TXT) was stopped. */
```

## <a name="nx_mdns_service_lookup"></a>nx_mdns_service_lookup

Hizmeti yerel eş hizmeti önbelleğinden alır

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_lookup(NXD_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service,
    CHAR *subtype, UINT instance_index,
    NXD_MDNS_SERVICE *service_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, örnek adıyla eşleşen Hizmetleri (sağlanmışsa) ve yerel eş hizmeti önbelleğindeki hizmet türünü arar. Uygulama, açıklama ile eşleşen önbellekteki ilk hizmet için *instance_index* ayarlanmış olan hizmet aramasını başlatacak. Uygulama, önbelleğin sonunu gösteren *NX_NO_MORE_ENTRIES* döndürdüğünden, bu hizmeti önbellekte bulunan ek hizmetler için artan *instance_index* değerle kullanmaya devam ediyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **örnek** Varsa hizmetin örnek adının işaretçisi.
- **hizmet** Varsa, alt tür bilgisi hariç olmak üzere mDNS hizmet türüne yönelik işaretçi.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.
- **Instance_index** Döndürülecek örneğe Dizin numarası.
- **service_ptr** Kullanıcı, arama sonuçlarını depolayan NX_MDNS_SERVICE yapısına işaret eden işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) hizmet başarıyla alındı
- **NX_NO_MORE_ENTRIES** (0x17) belirtilen dizin numarasında hizmet girdisi bulunamadı. Bu hata kodu aramanın sonunu gösterir.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Lookup the service on specific index. */

status = nx_mdns_service_lookup(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL,
    0, service_ptr);

/* If status is NX_SUCCESS, The service with
    name: NetX-SERVICE._http._tcp.local, was retrieved. */
```

## <a name="nx_mdns_service_ignore_set"></a>nx_mdns_service_ignore_set

Bir hizmet yoksayma kümesini yapılandırır

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_ignore_set(NX_MDNS *mdns_ptr, ULONG service_mask);
```

### <a name="description"></a>Açıklama

Bu API, *service_mask* bit maskesi tarafından belirtilen hizmetleri yoksayacak bir maske yapılandırır. Kullanıcı isteğe bağlı olarak, önbelleğe alınmasını istemediğiniz hizmet türlerini seçmek için service_mask kullanabilir. *Nxd_mdns. c* ' de *nx_mdns_service_types* tabloda tanımlanmış bir hizmet listesi. Nx_mdns_service_types [] içindeki ilk hizmet türünün karşılık gelen maskesi 0x00000001, ikinci hizmet türünün maskesi 0x00000002 ve bu şekilde devam eder.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **service_mask** Yok sayılacak Kullanıcı tanımlı hizmet türleri. Maske, 32 bitlik bir ULONG türüdür. Her bit, Kullanıcı tanımlı *nx_mdns_service_types* dizisindeki bir girişi temsil eder. Bir bit ayarlandıysa, *nx_mdns_service_type* dizisinde belirtilen karşılık gelen hizmet türü, eş hizmeti önbelleğinde depoolmaz.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) hizmeti yoksayma maskesini başarıyla ayarlıyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the service mask to ignore the specified service. */

status = nx_mdns_service_ignore_set(&my_mdns, 0x00000003);

/* If status is NX_SUCCESS, The service with
    type “_device-info” and “_http” will be ignored. */
```

## <a name="nx_mdns_service_notify_set"></a>nx_mdns_service_notify_set

Bir hizmet değişikliği bildirme geri arama işlevini yapılandırır

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_notify_set(NX_MDNS *mdns_ptr, ULONG service_mask,
    VOID (*service_change_notify)(NX_MDNS *mdns_ptr,
    NX_MDNS_SERVICE *service_ptr, UINT state));
```

### <a name="description"></a>Açıklama

Bu API, bir hizmet değişikliği bildirme geri arama işlevini yapılandırır. Bu geri çağırma işlevi, ağdaki diğer düğümler tarafından sunulan bir hizmet eklendiğinde, değiştirildiğinde veya artık kullanılabilir olmadığında çağrılır. Kullanıcı, izlemek istediği hizmet türlerini seçmek için isteğe bağlı olarak service_mask kullanabilir. İzlenen hizmetlerin bir listesi, *nxd_mdns. c* içindeki *nx_mdns_service_types* tabloda sabit kodludur.

Nx_mdns_service_types [] içindeki ilk hizmet türünün karşılık gelen maskesi 0x00000001, ikinci hizmet türünün maskesi 0x00000002 ve bu şekilde devam eder.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **service_mask** İzlenecek Kullanıcı tanımlı hizmet türleri. Maske, 32 bitlik bir ULONG türüdür. Her bit *nx_mdns_service_types* dizideki bir girişi temsil eder.
- **service_change_notify** Belirtilen hizmet değiştirildiğinde çağrılacak geri çağırma işlevi. Ayrıntılı hizmet bilgileri service_ptr tarafından işaret edilen bellekte döndürülür *.* Geri aramayı bildir işlevinden döndükten sonra bellekteki içeriğin geçersiz olduğunu unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) geri çağırma işlevi başarıyla yüklendi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the service mask to notify the specified service. */

status = nx_mdns_service_notify_set(&my_mdns, 0x00000002, service_change_notify);

/* If status is NX_SUCCESS, the callback will be called
    if received the service with type “_http”. */
```

## <a name="nx_mdns_service_notify_clear"></a>nx_mdns_service_notify_clear

Hizmet değiştirme bildirimi geri arama işlevini temizle

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Açıklama

Bu API, hizmet değişikliği bildirme geri arama işlevini ve öğesini temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi..

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) geri çağırma işlevini başarıyla temizledi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Clear the service notify. */

status = nx_mdns_service_notify_clear(&my_mdns);

/* If status is NX_SUCCESS, the service notify function clear. */
```

## <a name="nx_mdns_host_address_get"></a>nx_mdns_host_address_get

Konak adresini al

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_host_address_get(NX_MDNS *mdns_ptr,
    UCHAR *host_name, ULONG *ipv4_address,
    ULONG *ipv6_address, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, ana bilgisayar IPv4 ve IPv6 adresleri üzerinde bir mDNS sorgusu gerçekleştirir. Belirtilen ana bilgisayar adının adresi eş hizmeti önbelleğinde bulunursa, adres döndürülür. Eş hizmeti önbelleğinde bir adres bulunmazsa, mDNS modülü A ve AAAA tür sorgularını yayınlar ve yanıt bekler. Bu API, bir yanıt alınana ya da sorgu zaman aşımına uğrayana kadar engeller.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **host_name** Ana bilgisayar adı işaretçisi.
- **ipv4_address** IPv4 adresi depolama alanı için 4 baytlık hizalanmış bir adrese yönelik işaretçi. Kullanıcı IPv4 adresi için 4 bayt alan ayırsın. Uygulamanın IPv4 adresini alması gerekmiyorsa NX_NULL adresi bu API 'ye geçirilebilir.
- **ipv6_address** IPv6 adresi depolama alanı için 4 baytlık hizalanmış adrese yönelik işaretçi. Kullanıcı-IPv6 adresi için 16 bayt alan ayırır. Uygulamanın IPv6 adresini alması gerekmiyorsa, bu API 'ye NX_NULL adresi geçirilebilir.
- **wait_option** Bir yanıt için beklemek için zaman işaretleri cinsinden süre miktarı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00), ana bilgisayar adresini başarıyla aldı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
ULONG ipv4_address;
ULONG ipv6_address[4];

/* Get the IP address of specified host. */
status = nx_mdns_host_address_get(&my_mdns, “MDNS-Host”, &ipv4_address, ipv6_address, 500);

/* If status is NX_SUCCESS, the IP address of specified host was retrieved. */
```

## <a name="nx_mdns_local_cache_clear"></a>nx_mdns_local_cache_clear

Tüm yerel Hizmetleri Sil

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_local_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, güle iletisini gönderdikten sonra yerel hizmet önbelleğindeki tüm girişleri temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) önbellekteki tüm girdileri başarıyla sildiniz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Clear the local cache, delete all local service. */

status = nx_mdns_local_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of local cache were deleted. */
```

## <a name="nx_mdns_peer_cache_clear"></a>nx_mdns_peer_cache_clear

Bulunan tüm hizmetleri Sil

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_peer_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, eş hizmeti önbelleğindeki tüm girdileri temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) önbellekteki tüm girdileri başarıyla sildiniz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Clear the peer cache, delete all peer service. */

status = nx_mdns_peer_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of peer cache were deleted. */
```
