---
title: Bölüm 4 - mDNS hizmetlerinin açıklaması
description: Bu bölümde tüm NetX mDNS hizmetlerinin açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6e37698ac6023b4cff6cb4fc05330a73b678ef3d2a813a706c9b821381e123db
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797577"
---
# <a name="chapter-4---description-of-mdns-services"></a>Bölüm 4 - mDNS hizmetlerinin açıklaması

Bu bölümde tüm NetX mDNS hizmetlerinin açıklaması yer alır (aşağıda listelenmiştir).

> [!NOTE]
> Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

## <a name="nx_mdns_create"></a>nx_mdns_create

mDNS örneği oluşturma

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

### <a name="description"></a>Description

Bu hizmet, belirli IP örneğinde ve ilişkili kaynaklarda bir mDNS örneği oluşturur. Gelen mDNS iletilerini işlemek, sorgulara yanıt vermek ve sorgu iletilerini düzenli aralıklarla iletmek için de bir iş parçacığı oluşturulur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.
- **ip_ptr** İlişkili IP örneğinin işaretçisi.
- **packet_pool** Geçerli bir paket havuzunun işaretçisi.
- **öncelik** mDNS iş parçacığının önceliği.
- **stack_ptr** mDNS iş parçacığı için yığın alanına işaretçi
- **stack_size** Yığın alanı boyutu.
- **host_name** Bu düğüme atanan konak adı.
- **local_service_cache** Depolama hizmetler için daha fazla alan.
- **local_service_cache_size** Yerel hizmet önbelleğinin boyutu.
- **peer_service_cache** Depolama bilgileri için bir alan daha
- **peer_service_cache_size** Eş hizmet önbelleğinin boyutu
- **probing_notify** Yoklama işlemi sonunda çağrılan isteğe bağlı geri çağırma işlevi. Ana bilgisayar adının (yerel arabirimde mDNS'yi etkinleştirerek) veya hizmet adının (bir hizmeti kaydettikten sonra) benzersiz olup olmadığını uygulamaya iletir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) mDNS örneği başarıyla oluşturuldu.

### <a name="allowed-from"></a>İzin Verilen

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

mDNS örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_delete(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Description

Bu hizmet mDNS örneğini siler ve kaynaklarını serbest bıraktır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) mDNS örneği başarıyla silindi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete a previously created mDNS instance. */

status = nx_mdns_delete(&my_mdns);

/* If status is NX_SUCCESS, the mDNS instance has been deleted. */
```

## <a name="nx_mdns_enable"></a>nx_mdns_enable

mDNS hizmetini başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_enable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a>Description

Bu API, mDNS hizmetini belirli bir fiziksel arabirimde sağlar. Hizmet etkinleştirildikten sonra mDNS modülü, arabirimde alınan sorgulara yanıt vermeden önce ağ üzerinde tüm benzersiz hizmet adlarını yoklar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS örneği denetim bloğuna işaretçi.
- **interface_index** Hizmetin etkinleştirildikten sonra arabirime dizin oluşturma

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Hizmet başarıyla etkinleştirildi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Enable mDNS service on specific interface. */

status = nx_mdns_enable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was enabled. */
```

## <a name="nx_mdns_disable"></a>nx_mdns_disable

mDNS hizmetini devre dışı bırakma

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_disable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a>Description

Bu API, mDNS hizmetini belirli bir fiziksel arabirimde devre dışı bırakıyor. Hizmet devre dışı bırakılmıştır, mDNS arabirime bağlı ağa her yerel hizmet için "güle güle" iletileri gönderir, böylece komşu düğümler bilgi verir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.
- **interface_index** Hizmetin devre dışı bırakılacak olduğu arabirime dizin oluşturma

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Hizmeti başarıyla devre dışı bırakmıştır.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Disable mDNS service on specific interface. */

status = nx_mdns_disable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was disabled. */
```

## <a name="nx_mdns_cache_notify_set"></a>nx_mdns_cache_notify_set

mDNS önbelleği tam notify işlevini yükleme

### <a name="prototype"></a>Prototype

```c
UINT nx_mdns_cache_notify_set(NX_MDNS *mdns_ptr,
    VOID (*cache_full_notify_cb)(NX_MDNS *mdns_ptr,
        UINT state, UINT cache_type));
```

### <a name="description"></a>Description

Bu hizmet, yerel hizmet önbelleği veya eş hizmet önbelleği dolu olduğunda çağrılan, kullanıcı tarafından sağlanan bir geri çağırma işlevi yüklenir. Hizmet önbelleği dolu olduğunda, daha fazla mDNS Kaynak Kaydı ek edilemez. Çeşitli dize uzunluklarına sahip hizmetler ekleniyor ve kaldırılıyorsa, iç parçalanma nedeniyle hizmet önbelleğinin dolabilirsiniz. Eş hizmet önbelleğinde bir önbellek tam bildirimi aldıktan sonra, uygulama eş hizmet *önbelleğinde tüm girişleri silmek için "nx_mdns_service_cache_clear"* hizmetini kullanabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) mDNS önbelleği bildirim geri çağırma işlevi başarıyla yüklendi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set mDNS cache notify callback. */

status = nx_mdns_cache_notify_set(&my_mdns, cache_full_nofiy_cb);

/* If status is NX_SUCCESS, mDNS cache notify callback was set. */
```

## <a name="nx_mdns_cache_notify_clear"></a>nx_mdns_cache_notify_clear

mDNS hizmet önbelleği tam notify işlevini temizleme

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_cache_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Description

Bu hizmet, kullanıcı tarafından sağlanan hizmet önbelleği bildirim geri çağırma işlevini temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) mDNS hizmet önbelleği bildirim geri çağırma işlevi başarıyla temizlendi.

### <a name="allowed-from"></a>İzin Verilen

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

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

### <a name="description"></a>Description

Bu hizmet, tek seferlik bir mDNS sorgusu gerçekleştirir. Belirtilen hizmet eş hizmeti önbelleğinde bulunursa, ilk örnek döndürülür. Yerel eş hizmeti önbelleğinde hiçbir hizmet bulunmazsa, mDNS modülü bir sorgu komutu yayınlar ve yanıt bekler. İlk yanıt alınana veya sorgu zaman aşımına uğrayana kadar hizmet engellenir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** MDNS denetim bloğu işaretçisi.
- **örnek** Varsa hizmetin örnek adının işaretçisi.
- **hizmet** Alt tür bilgileri hariç mDNS hizmet türüne yönelik işaretçi. uygulamanın hizmet türünü belirtmesi gerekir.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.
- **service_ptr** Kullanıcı tarafından sorgu sonuçlarını depolayan NX_MDNS_SERVICE yapısına yönelik işaretçi.
- **wait_option** Yanıt için bekleme süresi (tıklar) miktarı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Hizmet bilgileri başarıyla edinildi.

### <a name="allowed-from"></a>İzin Verilen

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

Sürekli hizmet bulma başlatma

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_continous_query(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a>Description

Bu hizmet sürekli sorgu başlatır. Hizmetin hemen döndür olduğunu unutmayın. Sürekli sorgu verdikten sonra, uygulama api'sini kullanarak hizmet kaydını *nx_mdns_service_lookup.* Uygulama, sürekli sorguyu durdurmak için  API nx_mdns_service_query_stop

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.
- **örnek** Varsa hizmetin örnek adına işaretçi.
- **hizmet** Varsa alt tür bilgileri hariç olmak üzere mDNS hizmet türünün işaretçisi.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sorgu başarıyla başlatıldı.

### <a name="allowed-from"></a>İzin Verilen

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

Daha önce verilen sürekli hizmet keşfini durdurma

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_query_stop(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a>Description

Bu API, daha önce verilen sürekli hizmet bulmasını sonlandırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.
- **örnek** Hizmetin örnek adına işaretçi.
- **hizmet** mDNS hizmet türü, alt tür bilgileri işaretçisi.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sorgu başarıyla durduruldu.

### <a name="allowed-from"></a>İzin Verilen

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

Hizmeti yerel eş hizmet önbelleğinden alma

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_lookup(NXD_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service,
    CHAR *subtype, UINT instance_index,
    NXD_MDNS_SERVICE *service_ptr);
```

### <a name="description"></a>Description

Bu hizmet, örnek adıyla (sağlandı ise) eşleşen hizmetleri ve yerel eş hizmet önbelleğinde hizmet türünü aramaz. Uygulama, önbellekte *açıklamayla instance_index* ilk hizmet için sıfır olarak ayarlanmış şekilde hizmet aramayı başlatıyor olmalıdır. Uygulama, önbellekte bulunan ek *hizmetlerin instance_index* değeri artarak bu hizmeti kullanmaya devam NX_NO_MORE_ENTRIES , önbelleğin sonunu gösterir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.
- **örnek** Varsa hizmetin örnek adına işaretçi.
- **hizmet** Varsa alt tür bilgileri hariç olmak üzere mDNS hizmet türünün işaretçisi.
- **alt tür** Varsa mDNS hizmetinin alt tür kısmının işaretçisi.
- **Instance_index** Döndürülen örneğin dizin numarası.
- **service_ptr** Kullanıcı, arama sonuçlarını NX_MDNS_SERVICE yapısına işaretçi sağladı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Hizmet başarıyla alındı
- **NX_NO_MORE_ENTRIES** (0x17) Belirtilen dizin numarasında hiçbir hizmet girişi bulunamadı. Bu hata kodu aramanın sonunu gösterir.

### <a name="allowed-from"></a>İzin Verilen

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

Hizmet yoksayma kümesi yapılandırıyor

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_ignore_set(NX_MDNS *mdns_ptr, ULONG service_mask);
```

### <a name="description"></a>Description

Bu API, belirli bir bit maskesi tarafından belirtilen hizmetleri *yoksaymak service_mask* yapılandırıyor. Kullanıcı isteğe bağlı olarak service_mask önbelleğe alınmak zorunda olmadığını hizmet türlerini seçmek için bu hizmeti kullanabilir. nxd_mdns.c'de *yer alan nx_mdns_service_types* bir *hizmet listesi tanımlanır.* nx_mdns_service_types[] içinde ilk hizmet türünün ilgili maskesi 0x00000001, ikinci hizmet türünün maskesi 0x00000002 maskedir ve bu şekilde devam etti.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.
- **service_mask** Yoksaymak için kullanıcı tanımlı hizmet türleri. Maske 32 bit ULONG türündedir. Her bit, kullanıcı tanımlı nx_mdns_service_types *temsil* eder. Bir bit ayarlanırsa, nx_mdns_service_type dizisinde *belirtilen* karşılık gelen hizmet türü eş hizmet önbelleğinde depolanmaz.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Hizmetin yoksayma maskesini başarıyla ayarlar.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the service mask to ignore the specified service. */

status = nx_mdns_service_ignore_set(&my_mdns, 0x00000003);

/* If status is NX_SUCCESS, The service with
    type “_device-info” and “_http” will be ignored. */
```

## <a name="nx_mdns_service_notify_set"></a>nx_mdns_service_notify_set

Hizmet değişikliği bildirim geri çağırma işlevini yapılandırıyor

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_notify_set(NX_MDNS *mdns_ptr, ULONG service_mask,
    VOID (*service_change_notify)(NX_MDNS *mdns_ptr,
    NX_MDNS_SERVICE *service_ptr, UINT state));
```

### <a name="description"></a>Description

Bu API bir hizmet değişikliği bildirim geri çağırma işlevini yapılandırıyor. Bu geri çağırma işlevi, ağ üzerinde diğer düğümler tarafından sunulan bir hizmet ekleniyor, değiştirildi veya artık kullanılamıyorsa çağrılır. Kullanıcı, izlemek istediği hizmet service_mask seçmek için isteğe bağlı olarak bu hizmeti kullanabilir. izlenen hizmetlerin listesi, nxd_mdns.c'de *nx_mdns_service_types* sabit olarak *kodlandı.*

nx_mdns_service_types[] içinde ilk hizmet türünün ilgili maskesi 0x00000001, ikinci hizmet türünün maskesi 0x00000002 maskedir ve bu şekilde devam etti.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.
- **service_mask** İzlemek için kullanıcı tanımlı hizmet türleri. Maske 32 bit ULONG türündedir. Her bit, nx_mdns_service_types *dizisinde bir girdiyi temsil* eder.
- **service_change_notify** Belirtilen hizmet değiştiriliyorken çağrılan geri çağırma işlevi. Ayrıntılı hizmet bilgileri, uygulama tarafından işaret eden *bellekte service_ptr.* notify callback işlevinden döndüren bellek içeriğinin geçersiz olduğunu unutmayın.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Geri çağırma işlevi başarıyla yüklendi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the service mask to notify the specified service. */

status = nx_mdns_service_notify_set(&my_mdns, 0x00000002, service_change_notify);

/* If status is NX_SUCCESS, the callback will be called
    if received the service with type “_http”. */
```

## <a name="nx_mdns_service_notify_clear"></a>nx_mdns_service_notify_clear

Hizmet değişikliği bildirim geri çağırma işlevini temizleme

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_service_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Description

Bu API, hizmet değişikliği bildirim geri çağırma işlevini ve 'yi temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Geri çağırma işlevi başarıyla temizlendi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Clear the service notify. */

status = nx_mdns_service_notify_clear(&my_mdns);

/* If status is NX_SUCCESS, the service notify function clear. */
```

## <a name="nx_mdns_host_address_get"></a>nx_mdns_host_address_get

Ana bilgisayar adresini al

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_host_address_get(NX_MDNS *mdns_ptr,
    UCHAR *host_name, ULONG *ipv4_address,
    ULONG *ipv6_address, ULONG wait_option);
```

### <a name="description"></a>Description

Bu hizmet, konak IPv4 ve IPv6 adreslerinde bir mDNS sorgusu gerçekleştirir. Belirtilen konak adının adresi eş hizmet önbelleğinde bulunursa adres döndürülür. Eş hizmet önbelleğinde adres bulunamıyorsa mDNS modülü A ve AAAA türü sorgular göndermektedir ve yanıt bekler. Bu API, yanıt alınana veya sorgu zaman atana kadar engeller.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.
- **host_name** Ana bilgisayar adı işaretçisi.
- **ipv4_address** IPv4 adres depolama alanı için 4 bayta hizalı bir adresin işaretçisi. Kullanıcı, IPv4 - adresi için 4 bayt alan ayıracak. NX_NULL, uygulamanın IPv4 adresini alma ihtiyacı yoksa bu API'ye geçirebilirsiniz.
- **ipv6_address** IPv6 adres depolama alanı için 4 bayta hizalanmış adresin işaretçisi. Kullanıcı, - IPv6 adresi için 16 bayt alan ayıracak. NX_NULL, uygulamanın IPv6 adresini almaya ihtiyacı yoksa bu API'ye geçirebilirsiniz.
- **wait_option** Yanıt için bekleme süresi (tıklar) miktarı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarıyla ana bilgisayar adresi alındı.

### <a name="allowed-from"></a>İzin Verilen

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

Tüm yerel hizmetleri silme

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_local_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Description

Bu hizmet, Güle Güle iletisi gönderdikten sonra yerel hizmet önbelleğinde tüm girdileri temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Önbellekte tüm girişler başarıyla silindi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Clear the local cache, delete all local service. */

status = nx_mdns_local_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of local cache were deleted. */
```

## <a name="nx_mdns_peer_cache_clear"></a>nx_mdns_peer_cache_clear

Bulunan tüm hizmetleri silme

### <a name="prototype"></a>Prototype

```C
UINT nx_mdns_peer_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Description

Bu hizmet eş hizmet önbelleğinde tüm girişleri temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **mdns_ptr** mDNS denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Önbellekte tüm girişler başarıyla silindi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Clear the peer cache, delete all peer service. */

status = nx_mdns_peer_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of peer cache were deleted. */
```
