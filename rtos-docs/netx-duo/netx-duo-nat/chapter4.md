---
title: Bölüm 4-NAT hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo NAT API hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: dbe2cb25607162b62b048251927bdc7671c5884d2a3b45b6b24bae539e08d24a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797305"
---
# <a name="chapter-4---description-of-nat-services"></a>Bölüm 4-NAT hizmetlerinin açıklaması

Bu bölüm, tüm NetX Duo NAT API hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

> [!NOTE]
> Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

## <a name="nx_nat_create"></a>nx_nat_create

NAT sunucusu oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_nat_create(NX_NAT_DEVICE *nat_ptr, NX_IP *ip_ptr,
    UINT global_interface_index,
    VOID *dynamic_cache_memory,
    UINT dynamic_cache_size);
```

### <a name="description"></a>Description

Bu hizmet NAT sunucusunun bir örneğini oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nat_ptr** Oluşturulacak NAT örneğine yönelik işaretçi
- IP örneğine **Ip_ptr işaretçisi**
- **global_interface_index** Genel ağ arabiriminin dizini
- **dynamic_cache_memory** İşaretçi bellek alanını NAT tablosuna
- **dynamic_cache_size** NAT tablosu için bellek alanı boyutu

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) NAT sunucusu başarıyla oluşturuldu
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi
- NX_NAT_PARAM_ERROR (0xD01) geçersiz işaretçi girişi
- NX_NAT_CACHE_ERROR (0xD02) geçersiz önbellek işaretçisi girişi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
#define NX_NAT_ENTRY_CACHE_SIZE 20480

static UCHAR nat_cache[NX_NAT_ENTRY_CACHE_SIZE];
UINT global_interface_index = 0;

/* Create a NAT Server and cache with a global interface index. */
status = nx_nat_create(nat_ptr, ip_ptr, global_interface_index,
    nat_cache, NX_NAT_ENTRY_CACHE_SIZE);

/* If status = NX_SUCCESS, the NAT instance was successfully
    created. */
```

## <a name="nx_nat_delete"></a>nx_nat_delete

Bir NAT sunucusunu silme

### <a name="prototype"></a>Prototype

```C
UINT nx_nat_delete(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir NAT sunucusunu siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nat_ptr** Silinecek NAT örneğine yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) NAT başarıyla silindi
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Delete the NAT instance. */
status = nx_nat_delete (nat_ptr);

/* If the NAT instance was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_nat_enable"></a>nx_nat_enable

NAT için IP örneğini etkinleştirme

### <a name="prototype"></a>Prototype

```C
UINT nx_nat_enable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a>Description

Bu hizmet NAT için IP örneğini (örn. alınan paketleri NAT sunucusuna ilet) sağlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nat_ptr** NAT örneğine yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) NAT başarıyla etkinleştirildi
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Enable the NAT server. */
status = nx_nat_enable (nat_ptr);

/* If status = NX_SUCCESS, the IP instance was successfully enabled for NAT. */
```

## <a name="nx_nat_disable"></a>nx_nat_disable

NAT için IP örneğini devre dışı bırakma

### <a name="prototype"></a>Prototype

```C
UINT nx_nat_disable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a>Description

Bu hizmet, IP örneğinde NAT 'yi devre dışı bırakır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nat_ptr** NAT örneğine yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) NAT başarıyla devre dışı bırakıldı
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Disable the NAT server. */
status = nx_nat_disable (nat_ptr);

/* If status = NX_SUCCESS the NAT operation successfully disable. */
```

## <a name="nx_nat_cache_notify_set"></a>nx_nat_cache_notify_set

Önbellek tam bildirimi geri arama işlevini ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_nat_cache_notify_set(NX_NAT_DEVICE *nat_ptr,
    VOID (*cache_full_notify_cb)
    (NX_NAT_DEVICE *nat_ptr)));
```

### <a name="description"></a>Description

Bu hizmet, Kullanıcı tanımlı önbellek tam bildirim işlevine işaret eden cache_full_notify_cb giriş işlevi işaretçisi ile önbellek tam geri çağırma işlemini kaydeder.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nat_ptr** NAT örneğine yönelik işaretçi
- **cache_full_notify_cb** Cache Full NOTIFY işlevi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) önbellek tam bildirme işlevi başarıyla ayarlandı
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi
- NX_NAT_PARAM_ERROR (0xD01) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Set the cache full notify callback function to the NAT instance. */
status = nx_nat_cache_notify_set(nat_ptr, cache_full_notify_cb);

/* If status = NX_SUCCESS the callback function was successfully set. */
```

## <a name="nx_nat_inbound_entry_create"></a>nx_nat_inbound_entry_create

NAT çeviri tablosunda bir gelen giriş oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_nat_inbound_entry_create(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *entry_ptr
    ULONG local_ip_address,
    USHORT external_port,
    USHORT local_port, UCHAR protocol);
```

### <a name="description"></a>Description

Bu hizmet, bir gelen girişi statik (kalıcı giriş, süresiz) olarak oluşturur ve NAT çeviri tablosuna ekler. Bu girişler genellikle, dış ağdaki bir konaktan bir bağlantının başlatıldığı yerel ana bilgisayar sunucuları için oluşturulur. NAT sunucusu, dış bağlantı noktasının çeviri tablosunda zaten kullanımda olmadığını veya aynı protokolün daha önce var olan bir NetX Duo yuvasına göre bağlandığını denetler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nat_ptr** NAT örneğine yönelik işaretçi
- **entry_ptr** Çeviri girdisi işaretçisi
- **local_ip_address** Yerel ana bilgisayar IP adresi
- **external_port** Dış ağdaki hedef bağlantı noktası
- **local_port** Kaynak (yerel ana bilgisayar) bağlantı noktası
- **protokol** Paket Protokolü (örn. TCP)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) girdisi başarıyla oluşturuldu
- **NX_NAT_PORT_UNAVAILABLE** (0XD0D) geçersiz dış bağlantı noktası
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi
- NX_NAT_PARAM_ERROR (0xD01) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Create an entry for an inbound TCP packet. */
status = nx_nat_inbound_entry_create(nat_ptr, entry_ptr,
    IP_ADDRESS(192,168,2,2), 5001, 5001,
    NX_PROTOCOL_TCP);

/* If status = NX_SUCCESS the entry was successfully created. */
```

## <a name="nx_nat_inbound_entry_delete"></a>nx_nat_inbound_entry_delete

NAT çeviri tablosunda bir gelen girişi silme

### <a name="prototype"></a>Prototype

```C
UINT nx_nat_inbound_entry_delete(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *delete_entry_ptr)
```

### <a name="description"></a>Description

Bu hizmet, belirtilen gelen girdiyi çeviri tablosundan siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **nat_ptr** NAT örneğine yönelik işaretçi
- **delete_entry_ptr** NAT çeviri girdisi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) girdisi başarıyla silindi
- **NX_NAT_ENTRY_NOT_FOUND** (0xd04) girişi bulunamadı
- NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi
- NX_NAT_ENTRY_TYPE_ERROR (0xD0C) geçersiz çeviri türü

### <a name="allowed-from"></a>İzin verilen

Uygulama kodu

### <a name="example"></a>Örnek

```C
/* Delete the specified static entry from the translation table. */
status = nx_nat_inbound_entry_delete(nat_ptr, delete_entry_ptr);

/* If status = NX_SUCCESS the entry was successfully deleted. */
```
