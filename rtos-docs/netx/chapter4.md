---
title: Bölüm 4-Azure RTOS NetX hizmetlerinin açıklaması
description: Bu bölümde, tüm Azure RTOS NetX Hizmetleri alfabetik sırada bir açıklama bulunur.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 720e573b53070a754618830134f63a8421b9fd29
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825642"
---
# <a name="chapter-4---description-of-azure-rtos-netx-services"></a>Bölüm 4-Azure RTOS NetX hizmetlerinin açıklaması

Bu bölümde, tüm Azure RTOS NetX Hizmetleri alfabetik sırada bir açıklama bulunur. Hizmet adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır. Örneğin, bu bölümün başlangıcında tüm ARP hizmetleri bulunur.

> [!NOTE]
> *Yüksek performanslı NetX API 'den tam olarak yararlanmayan eski uygulama kodu için BSD-Compatible yuva API 'SI kullanılabilir olduğunu unutmayın. BSD-Compatible yuva API 'SI hakkında daha fazla bilgi için ek D 'ye bakın.*

Her açıklamanın "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan NX_DISABLE_ERROR_CHECKING seçeneğinden etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır. "Izin verilen" bölümler, her bir NetX hizmetinin çağrılabilecek olduğunu gösterir.

## <a name="nx_arp_dynamic_entries_invalidate"></a>nx_arp_dynamic_entries_invalidate

ARP önbelleğindeki tüm dinamik girdileri geçersiz kıl

### <a name="prototype"></a>Prototype

```C
UINT nx_arp_dynamic_entries_invalidate(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, şu anda ARP önbelleğindeki tüm dinamik ARP girdilerini geçersiz kılar.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP önbelleği geçersiz kılar.
- **NX_NOT_ENABLED** (0x14) ARP etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz IP adresi.
- **NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```c
/* Invalidate all dynamic entries in the ARP cache. */
status = nx_arp_dynamic_entries_invalidate(&ip_0);
/* If status is NX_SUCCESS the dynamic ARP entries were successfully invalidated. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entry_set, nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_dynamic_entry_set"></a>nx_arp_dynamic_entry_set

Dinamik ARP girdisi ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_arp_dynamic_entry_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a>Açıklama

Bu hizmet ARP önbelleğinden dinamik bir giriş ayırır ve belirtilen IP 'yi fiziksel adres eşlemesi olarak ayarlar. Sıfır fiziksel adresi belirtilmişse, fiziksel adresin çözülebilmesi için ağa gerçek bir ARP isteği gönderilir. Ayrıca, ARP eskime etkin olduğunda veya ARP önbelleği tükenirse ve en son kullanılan ARP girişi ise bu girişin kaldırılacağını unutmayın.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** Eşlenecek IP adresi.
- **physical_msw** Fiziksel adresin ilk 16 bit (47-32).
- **physical_lsw** Fiziksel adresin düşük 32 bitleri (31-0).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP dinamik giriş kümesi.
- **NX_NO_MORE_ENTRIES** (0x17) ARP önbelleğinde daha fazla ARP girişi bulunmamaktadır.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_PTR_ERROR** (0x07) geçersiz IP örneği işaretçisi.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Setup a dynamic ARP entry on the previously created IP Instance 0. */
status = nx_arp_dynamic_entry_set(&ip_0, IP_ADDRESS(1,2,3,4),
    0x1022, 0x1234);
/* If status is NX_SUCCESS, there is now a dynamic mapping between
    the IP address of 1.2.3.4 and the physical hardware address of
    10:22:00:00:12:34. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate, nx_arp_enable,
- nx_arp_gratuitous_send, nx_arp_hardware_address_find,
- nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_enable"></a>nx_arp_enable

Adres Çözümleme Protokolü (ARP) etkinleştirilir.

### <a name="prototype"></a>Prototype

```C
UINT nx_arp_enable(
    NX_IP *ip_ptr, 
    VOID *arp_cache_memory, 
    ULONG arp_cache_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirli IP örneği için NetX ARP bileşenini başlatır. ARP başlatma, ARP iletilerinin gönderilmesi ve alınması için gereken ARP önbelleğini ve çeşitli ARP işleme yordamlarını ayarlamayı içerir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **arp_cache_memory** ARP önbelleğinin yerleştirileceği bellek alanı işaretçisi.
- **arp_cache_size** Her ARP girişi 52 bayttır, ARP girişlerinin toplam sayısı, bu nedenle boyut 52 ' ye bölünür.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya önbellek bellek işaretçisi.
- **NX_SIZE_ERROR** (0x09) Kullanıcı tarafından sağlanan ARP önbelleği belleği çok küçük.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_ALREADY_ENABLED** (0x15) Bu bileşen zaten etkinleştirilmiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable ARP and supply 1024 bytes of ARP cache memory for
    previously created IP Instance ip_0. */
status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
/* If status is NX_SUCCESS, ARP was successfully enabled for this IP instance.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_gratuitous_send, nx_arp_hardware_address_find,
- nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_gratuitous_send"></a>nx_arp_gratuitous_send

Gereksiz ARP isteği gönder

### <a name="prototype"></a>Prototype

```C
UINT nx_arp_gratuitous_send(
    NX_IP *ip_ptr,
    VOID (*response_handler) (NX_IP *ip_ptr, NX_PACKET *packet_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet, arabirim IP adresi geçerli olduğu sürece gereksiz ARP isteklerini iletmek için tüm fiziksel arabirimlerin üzerinden geçer. Bir ARP yanıtı alındıktan sonra, sağlanan yanıt işleyicisi, gereksiz ARP için yanıtı işlemek üzere çağırılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **response_handler** Yanıt işleme işlevine yönelik işaretçi. NX_NULL sağlanırsa, yanıtlar yok sayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı gereksiz ARP gönderme.
- **NX_NO_PACKET** (0x01) kullanılabilir paket yok.
- **NX_NOT_ENABLED** (0x14) ARP etkin değil.
- **NX_IP_ADDRESS_ERROR** (0x21) geçerli IP adresi geçersiz.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Send gratuitous ARP without any response handler. */
status = nx_arp_gratuitous_send(&ip_0, NX_NULL);

/* If status is NX_SUCCESS the gratuitous ARP was successfully sent. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_hardware_address_find"></a>nx_arp_hardware_address_find

Bir IP adresi verilen fiziksel donanım adresini bulma

### <a name="prototype"></a>Prototype

```C
UINT nx_arp_hardware_address_find(
    NX_IP *ip_ptr,
    ULONG ip_address, 
    ULONG *physical_msw, 
    ULONG *physical_lsw);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP adresiyle ilişkili ARP önbelleğinde fiziksel bir donanım adresi bulmaya çalışır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** Aranacak IP adresi.
- **physical_msw** Fiziksel adresin ilk 16 bitini (47-32) döndürmek için değişkene yönelik işaretçi.
- **physical_lsw** Fiziksel adresin alt 32 bitlerini (31-0) döndürmek için değişkene yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP donanım adresi bul.
- **NX_ENTRY_NOT_FOUND** (0x16) eşleme ARP önbelleğinde bulunamadı.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya bellek işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Search for the hardware address associated with the IP address of
    1.2.3.4 in the ARP cache of the previously created IP
    Instance 0. */
status = nx_arp_hardware_address_find(
    &ip_0, 
    IP_ADDRESS(1,2,3,4),
    &physical_msw, 
    &physical_lsw);

/* If status is NX_SUCCESS, the variables physical_msw and
    physical_lsw contain the hardware address.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_info_get"></a>nx_arp_info_get

ARP etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype

```C
UINT nx_arp_info_get(
    NX_IP *ip_ptr,
    ULONG *arp_requests_sent,
    ULONG *arp_requests_received,
    ULONG *arp_responses_sent,
    ULONG *arp_responses_received,
    ULONG *arp_dynamic_entries,
    ULONG *arp_static_entries,
    ULONG *arp_aged_entries,
    ULONG *arp_invalid_messages);
```

### <a name="description"></a>Açıklama

Bu hizmet, ilişkili IP örneği için ARP etkinlikleri hakkında bilgi alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **arp_requests_sent** Bu IP örneğinden gönderilen toplam ARP isteği için hedef işaretçisi.
- **arp_requests_received** Ağdan alınan toplam ARP istekleri için hedef işaretçisi.
- **arp_responses_sent** Bu IP örneğinden gönderilen toplam ARP yanıtlarının hedefi işaretçisi.
- **arp_responses_received** Ağdan alınan toplam ARP yanıtlarının hedefe yönelik işaretçisi.
- **arp_dynamic_entries** Geçerli dinamik ARP girişi sayısı için hedef işaretçisi.
- **arp_static_entries** Geçerli statik ARP girişi sayısı için hedef işaretçisi.
- **arp_aged_entries** Eski olan ve geçersiz duruma gelen toplam ARP girişi sayısının hedefi işaretçisi.
- **arp_invalid_messages** Alınan toplam geçersiz ARP iletisi hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP bilgisi alma.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Pickup ARP information for ip_0. */
status = nx_arp_info_get(
    &ip_0, 
    &arp_requests_sent,
    &arp_requests_received,
    &arp_responses_sent,
    &arp_responses_received,
    &arp_dynamic_entries,
    &arp_static_entries,
    &arp_aged_entries,
    &arp_invalid_messages);
/* If status is NX_SUCCESS, the ARP information has been stored in
    the supplied variables. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_ip_address_find,
- nx_arp_static_entries_delete, nx_arp_static_entry_create,
- nx_arp_static_entry_delete

## <a name="nx_arp_ip_address_find"></a>nx_arp_ip_address_find

Fiziksel bir adres verilen IP adresini bulma

### <a name="prototype"></a>Prototype

```C
UINT nx_arp_ip_address_find(
    NX_IP *ip_ptr, 
    ULONG *ip_address,
    ULONG physical_msw, 
    ULONG physical_lsw);
```

### <a name="description"></a>Açıklama

Bu hizmet, ARP önbelleğinde sağlanan fiziksel adresle ilişkili bir IP adresi bulmaya çalışır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** Eşlenen IP adresi işaretçisi, eşlenmiş bir değer bulundu.
- **physical_msw** Aranacak fiziksel adresin ilk 16 bit (47-32).
- **physical_lsw** Aranacak fiziksel adresin düşük 32 bitleri (31-0).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP IP adresi bulma
- **NX_ENTRY_NOT_FOUND** (0x16) eşleme ARP önbelleğinde bulunamadı.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya bellek işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_INVALID_PARAMETERS** (0x4D) Physical_msw ve physical_lsw ikisi de 0 ' dır.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Search for the IP address associated with the hardware address of
    0x0:0x01234 in the ARP cache of the previously created IP
    Instance ip_0. */
status = nx_arp_ip_address_find(&ip_0, &ip_address, 0x0, 0x1234);

/* If status is NX_SUCCESS, the variables ip_address contains the
    associated IP address.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_static_entries_delete, nx_arp_static_entry_create,
- nx_arp_static_entry_delete

## <a name="nx_arp_static_entries_delete"></a>nx_arp_static_entries_delete

Tüm statik ARP girdilerini Sil

### <a name="prototype"></a>Prototype

```C
UINT nx_arp_static_entries_delete(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet ARP önbelleğindeki tüm statik girişleri siler.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) statik girdileri silinir.
- **NX_PTR_ERROR** (0x07) geçersiz ip_ptr işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Delete all the static ARP entries for IP Instance 0, assuming
    "ip_0" is the NX_IP structure for IP Instance 0. */

status = nx_arp_static_entries_delete(&ip_0);

/* If status is NX_SUCCESS all static ARP entries in the ARP cache
have been deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entry_create,
- nx_arp_static_entry_delete

## <a name="nx_arp_static_entry_create"></a>nx_arp_static_entry_create

ARP önbelleğinde donanım eşlemeye statik IP oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_arp_static_entry_create(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için ARP önbelleğinde statik bir IP-fiziksel adres eşlemesi oluşturur. Statik ARP girdileri ARP düzenli güncelleştirmelerine tabi değildir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** Eşlenecek IP adresi.
- **physical_msw** Eşlenecek fiziksel adresin ilk 16 bit (47-32).
- **physical_lsw** Eşlenecek fiziksel adresin düşük 32 bitleri (31-0).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP statik girdisi oluştur.
- **NX_NO_MORE_ENTRIES** (0x17) ARP önbelleğinde daha fazla ARP girişi bulunmamaktadır.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_INVALID_PARAMETERS** (0x4D) Physical_msw ve physical_lsw ikisi de 0 ' dır.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Create a static ARP entry on the previously created IP
    Instance 0. */

status = nx_arp_static_entry_create(&ip_0, IP_ADDRESS(1,2,3,4),
    0x0, 0x1234);

/* If status is NX_SUCCESS, there is now a static mapping between
    the IP address of 1.2.3.4 and the physical hardware address of
    00:00:00:00:12:34. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_delete

## <a name="nx_arp_static_entry_delete"></a>nx_arp_static_entry_delete

ARP önbelleğindeki statik IP 'yi donanım eşleştirmeye silme


### <a name="prototype"></a>Prototype

```C
UINT nx_arp_static_entry_delete(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için ARP önbelleğinde önceden oluşturulmuş bir statik IP-fiziksel adres eşlemeyi bulur ve siler.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** Statik olarak eşlenmiş IP adresi.
- **physical_msw** Statik olarak eşlenmiş fiziksel adresin ilk 16 bit (47-32).
- **physical_lsw** Statik olarak eşlenmiş fiziksel adresin düşük 32 bitleri (31-0).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP statik girdisi silme.
- **NX_ENTRY_NOT_FOUND** (0x16) ARP ÖNBELLEĞINDE statik ARP girdisi bulunamadı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_INVALID_PARAMETERS** (0x4D) Physical_msw ve physical_lsw ikisi de 0 ' dır.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Delete a static ARP entry on the previously created IP
    instance ip_0. */
status = nx_arp_static_entry_delete(&ip_0, IP_ADDRESS(1,2,3,4),
    0x0, 0x1234);
/* If status is NX_SUCCESS, the previously created static ARP entry
    was successfully deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create

## <a name="nx_icmp_enable"></a>nx_icmp_enable

Internet Denetim Iletisi Protokolü 'Nü (ıCMP) etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT nx_icmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için ıCMP bileşenini sunar.
ICMP bileşeni, Internet hata iletilerini ve ping isteklerini ve yanıtlarını işlemekten sorumludur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ICMP etkinleştirmesi.
- **NX_ALREADY_ENABLED** (0x15) ICMP zaten etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable ICMP on the previously created IP Instance ip_0. */
status = nx_icmp_enable(&ip_0);

/* If status is NX_SUCCESS, ICMP is enabled. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_icmp_info_get, nx_icmp_ping

## <a name="nx_icmp_info_get"></a>nx_icmp_info_get

ICMP etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype

```C
UINT nx_icmp_info_get(
    NX_IP *ip_ptr,
    ULONG *pings_sent,
    ULONG *ping_timeouts,
    ULONG *ping_threads_suspended,
    ULONG *ping_responses_received,
    ULONG *icmp_checksum_errors,
    ULONG *icmp_unhandled_messages);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için ıCMP etkinlikleri hakkında bilgi alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **pings_sent** Gönderilen toplam ping sayısı için hedef işaretçisi.
- **ping_timeouts** Toplam ping zaman aşımı sayısı için hedef işaretçisi.
- **ping_threads_suspended** Ping isteklerinde askıya alınan toplam iş parçacığı sayısının hedefi işaretçisi.
- **ping_responses_received** Alınan toplam ping yanıtı sayısının hedef işaretçisi.
- **icmp_checksum_errors** Toplam ıCMP sağlama toplamı hatası sayısının hedefi işaretçisi.
- **icmp_unhandled_messages** İşlenmemiş ıCMP iletilerinin toplam sayısının hedef işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ICMP bilgisi alma.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve ICMP information from previously created IP
    instance ip_0. */
status = nx_icmp_info_get(
    &ip_0, 
    &pings_sent, 
    &ping_timeouts,
    &ping_threads_suspended,
    &ping_responses_received,
    &icmp_checksum_errors,
    &icmp_unhandled_messages);

/* If status is NX_SUCCESS, ICMP information was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_icmp_enable, nx_icmp_ping

## <a name="nx_icmp_ping"></a>nx_icmp_ping

Belirtilen IP adresine ping isteği gönder

### <a name="prototype"></a>Prototype

```C
UINT nx_icmp_ping(
    NX_IP *ip_ptr,
    ULONG ip_address,
    CHAR *data, ULONG data_size,
    NX_PACKET **response_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP adresine bir ping isteği gönderir ve bir ping yanıtı iletisi için belirtilen süre için bekler. Yanıt alınmadığında bir hata döndürülür. Aksi takdirde, tüm yanıt iletisi response_ptr tarafından işaret edilen değişkende döndürülür.

*NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** Ping yapılacak ana bilgisayar bayt sırasındaki IP adresi. ping iletisi için veri alanına veri Işaretçisi.
- **data_size** Ping verilerinde bayt sayısı
- **response_ptr** İçindeki ping yanıt iletisini döndürecek paket işaretçisi işaretçisi.
- **wait_option** Bir ping yanıtı için ne kadar bekleneceğini tanımlar. bekleme seçenekleri aşağıdaki gibi tanımlanır:

  - NX_NO_WAIT (0x00000000)
  - NX_WAIT_FOREVER (0xFFFFFFFF)
  - ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ping. Yanıt iletisi işaretçisi, response_ptr tarafından işaret edilen değişkene yerleştirildi.
- **NX_NO_PACKET** (0x01) bir ping isteği paketi ayrılamıyor.
- **NX_OVERFLOW** (0x03) belirtilen veri alanı, bu IP örneği için varsayılan paket boyutunu aşıyor.
- **NX_NO_RESPONSE** (0x29) istenen IP yanıt vermedi.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya Yanıt işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Issue a ping to IP address 1.2.3.5 from the previously created IP
    Instance ip_0. */
status = nx_icmp_ping(&ip_0, IP_ADDRESS(1,2,3,5), "abcd", 4,
    &response_ptr, 10);

/* If status is NX_SUCCESS, a ping response was received from IP
    address 1.2.3.5 and the response packet is contained in the
    packet pointed to by response_ptr. It should have the same "abcd"
    four bytes of data. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_icmp_enable, nx_icmp_info_get

## <a name="nx_igmp_enable"></a>nx_igmp_enable

Internet Grubu Yönetim Protokolü 'Nü (ıGMP) etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT nx_igmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneğindeki ıGMP bileşenini sunar.
IGMP bileşeni, IP çok noktaya yayın grup yönetimi işlemlerine yönelik destek sağlamaktan sorumludur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarıyla IGMP etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_ALREADY_ENABLED** (0x15) Bu bileşen zaten etkinleştirilmiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable IGMP on the previously created IP Instance ip_0. */
status = nx_igmp_enable(&ip_0);

/* If status is NX_SUCCESS, IGMP is enabled. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_info_get, nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,
- nx_igmp_multicast_join, nx_igmp_multicast_leave

## <a name="nx_igmp_info_get"></a>nx_igmp_info_get

IGMP etkinlikleri hakkında bilgi alma

### <a name="prototype"></a>Prototype

```C
UINT nx_igmp_info_get(
    NX_IP *ip_ptr,
    ULONG *igmp_reports_sent,
    ULONG *igmp_queries_received,
    ULONG *igmp_checksum_errors,
    ULONG *current_groups_joined);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için ıGMP etkinlikleri hakkında bilgi alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **igmp_reports_sent** Gönderilen toplam ıCMP raporu sayısı için hedef işaretçisi.
- **igmp_queries_received** Çok noktaya yayın yönlendiricisi tarafından alınan toplam sorgu sayısı için hedef işaretçisi.
- **igmp_checksum_errors** Alma paketlerindeki toplam ıGMP sağlama toplamı hatalarının hedefi işaretçisi.
- **current_groups_joined** Bu IP örneğine katılmış geçerli grup sayısının hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarıyla IGMP bilgileri alma.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve IGMP information
    from previously created IP Instance ip_0. */
status = nx_igmp_info_get(
    &ip_0, 
    &igmp_reports_sent,
    &igmp_queries_received,
    &igmp_checksum_errors,
    &current_groups_joined);
/* If status is NX_SUCCESS, IGMP information was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable, nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,
- nx_igmp_multicast_join, nx_igmp_multicast_leave

## <a name="nx_igmp_loopback_disable"></a>nx_igmp_loopback_disable

IGMP geri döngüsünü devre dışı bırak

### <a name="prototype"></a>Prototype

```C
UINT nx_igmp_loopback_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, sonraki tüm çok noktaya yayın gruplarına katılmış ıGMP geri döngüsünü devre dışı bırakır

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarıyla IGMP geri döngü devre dışı.
- **NX_NOT_ENABLED** (0x14) IGMP etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Disable IGMP loopback for all subsequent multicast groups joined. */
status = nx_igmp_loopback_disable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is disabled. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_enable,
- nx_igmp_multicast_interface_join, nx_igmp_multicast_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_loopback_enable"></a>nx_igmp_loopback_enable

IGMP geri döngüsünü etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT nx_igmp_loopback_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, sonraki tüm çok noktaya yayın gruplarına katılmış ıGMP geri döngüsüne izin vermez.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarıyla IGMP geri döngü devre dışı.
- **NX_NOT_ENABLED** (0x14) IGMP etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable IGMP loopback for all subsequent multicast groups joined. */
status = nx_igmp_loopback_enable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is enabled. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,
- nx_igmp_multicast_interface_join, nx_igmp_multicast_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_multicast_interface_join"></a>nx_igmp_multicast_interface_join

IP örneğini bir arabirim aracılığıyla belirtilen çok noktaya yayın grubuna ekleyin

### <a name="prototype"></a>Prototype

```C
UINT nx_igmp_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ağ arabirimi aracılığıyla bir IP örneğini belirtilen çok noktaya yayın grubuna birleştirir. Aynı grubun kaç kez katıldığını izlemek için bir iç sayaç tutulur. Çok noktaya yayın grubuna katıldıktan sonra, ıGMP bileşeni, belirtilen ağ arabirimi aracılığıyla bu grup adresiyle IP paketlerinin alımına ve ayrıca bu IP 'nin bu çok noktaya yayın grubunun bir üyesi olduğu yönlendiricilere rapor vermeyecektir. IGMP üyelik birleşimi, rapor ve çıkış iletileri belirtilen ağ arabirimi aracılığıyla da gönderilir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **group_address** Ana bilgisayar bayt düzeninde katılacak sınıf D IP çok noktaya yayın grubu adresi.
- **interface_index** NetX örneğine iliştirilmiş arabirimin dizini.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı çok noktaya yayın grubu katılımı.
- **NX_NO_MORE_ENTRIES** (0x17) daha fazla çok noktaya yayın grubu birleştirilemez, en fazla sınır aşıldı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_INVALID_INTERFACE** (0x4C) cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.
- **NX_IP_ADDRESS_ERROR** (0x21) belirtilen çok noktaya yayın grubu adresi geçerli bir sınıf D adresi değil.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) IP çok noktaya yayın desteği etkin değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Previously created IP Instance joins the multicast group
    244.0.0.200, via the interface at index 1 in the IP interface list. */
#define INTERFACE_INDEX 1
status = nx_igmp_multicast_interface_join
    (&ip, IP_ADDRESS(244,0,0,200),
    INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully joined
    the multicast group. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_multicast_join"></a>nx_igmp_multicast_join

IP örneğini belirtilen çok noktaya yayın grubuna ekleyin

### <a name="prototype"></a>Prototype

```C
UINT nx_igmp_multicast_join(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir IP örneğini belirtilen çok noktaya yayın grubuna birleştirir. Aynı grubun kaç kez katıldığını izlemek için bir iç sayaç tutulur. Bu, konağın gruba katılması için bir ağ üzerinde ilk JOIN isteği olduğunu belirten bir ıGMP raporu göndermek için kullanılır. Birleştirme sonrasında, ıGMP bileşeni, bu IP 'nin bu çok noktaya yayın grubunun üyesi olduğu yönlendiricilerle bu grup adresi ve raporla IP paketleri alımına izin verir.

> [!NOTE]
> *Birincil olmayan bir cihazdaki çok noktaya yayın grubuna katmak için, hizmet **nx_igmp_multicast_interface_join kullanın.***

- **Parametreler**

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **group_address** Katılacak sınıf D IP çok noktaya yayın grubu adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı çok noktaya yayın grubu katılımı.
- **NX_NO_MORE_ENTRIES** (0x17) daha fazla çok noktaya yayın grubu birleştirilemez, en fazla sınır aşıldı.
- **NX_INVALID_INTERFACE** (0x4C) cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP grubu adresi.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Previously created IP Instance ip_0 joins the multicast group
    224.0.0.200. */
status = nx_igmp_multicast_join(&ip_0, IP_ADDRESS(224,0,0,200));

/* If status is NX_SUCCESS, this IP instance has successfully
    joined the multicast group 224.0.0.200. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_multicast_leave"></a>nx_igmp_multicast_leave

IP örneğinin belirtilen çok noktaya yayın grubuna ayrılma nedeni

### <a name="prototype"></a>Prototype

```C
UINT nx_igmp_multicast_leave(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, çıkış isteklerinin sayısı, JOIN isteklerinin sayısı ile eşleşiyorsa bir IP örneğinin belirtilen çok noktaya yayın grubunu bırakmasını sağlar. Aksi takdirde, iç ekleme sayısı yalnızca azaltılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **group_address** Bırakılacak çok noktaya yayın grubu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı çok noktaya yayın grubu katılımı.
- **NX_ENTRY_NOT_FOUND** (0x16) önceki JOIN isteği bulunamadı.
- **NX_INVALID_INTERFACE** (0x4C) cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP grubu adresi.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Cause IP instance to leave the multicast group 224.0.0.200. */
status = nx_igmp_multicast_leave(&ip_0, IP_ADDRESS(224,0,0,200);

/* If status is NX_SUCCESS, this IP instance has successfully left
    the multicast group 224.0.0.200. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,
- nx_igmp_multicast_join

## <a name="nx_ip_address_change_notifiy"></a>nx_ip_address_change_notifiy

IP adresi değişirse uygulamayı bilgilendir


### <a name="prototype"></a>Prototype

```C
UINT nx_ip_address_change_notify(
    NX_IP *ip_ptr,
    VOID(*change_notify)(NX_IP *,VOID *),
    VOID *additional_info);
```

### <a name="description"></a>Açıklama

Bu hizmet, IP adresi her değiştirildiğinde çağrılan bir uygulama bildirim işlevini kaydeder.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **change_notify** IP değişikliği bildirim işlevine yönelik işaretçi. Bu parametre NX_NULL, IP adresi değişiklik bildirimi devre dışı bırakılır.
- **additional_info** IP adresi değiştirildiğinde bildirim işlevine de sağlanan isteğe bağlı ek bilgilere yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP adresi değişikliği bildirimi.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Register the function "my_ip_changed" to be called whenever
the IP address is changed. */
status = nx_ip_address_change_notify(&ip_0, my_ip_changed, NX_NULL);

/* If status is NX_SUCCESS, the "my_ip_changed" function will be
    called whenever the IP address changes. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_get, nx_ip_address_set, nx_ip_create, nx_ip_delete,
- nx_ip_driver_direct_command, nx_ip_driver_interface_direct_command,
- nx_ip_forwarding_disable, nx_ip_forwarding_enable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_address_get"></a>nx_ip_address_get

IP adresi ve ağ maskesini al

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_address_get(
    NX_IP *ip_ptr,
    ULONG *ip_address,
    ULONG *network_mask);
```

### <a name="description"></a>Açıklama

Bu hizmet, birincil ağ arabiriminin IP adresini ve alt ağ maskesini alır.

* İkincil cihaz hakkında bilgi edinmek için hizmetini kullanın
- **nx_ip_interface_address_get**. *

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** IP adresi için hedef işaretçisi.
- **network_mask** Ağ maskesi için hedef işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP adresi al.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya dönüş değişkeni işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Get the IP address and network mask from the previously created
    IP Instance ip_0. */
status = nx_ip_address_get(&ip_0,
    &ip_address, &network_mask);

/* If status is NX_SUCCESS, the variables ip_address and
    network_mask contain the IP and network mask respectively. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_set, nx_ip_create,
- nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,
- nx_system_initialize

## <a name="nx_ip_address_set"></a>nx_ip_address_set

IP adresi ve ağ maskesini ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_address_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a>Açıklama

Bu hizmet, birincil ağ arabirimi için IP adresi ve ağ maskesini ayarlar.

*İkincil cihaz için IP adresi ve ağ maskesini ayarlamak için, hizmet **nx_ip_interface_address_set** kullanın.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** Yeni IP adresi.
- **network_mask** Yeni ağ maskesi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP adresi kümesi.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Set the IP address and network mask to 1.2.3.4 and 0xFFFFFF00
    for the previously created IP Instance ip_0. */
status = nx_ip_address_set(&ip_0, IP_ADDRESS(1,2,3,4), 0xFFFFFF00UL);

/* If status is NX_SUCCESS, the IP instance now has an IP address
    of 1.2.3.4 and a network mask of 0xFFFFFF00. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_create,
- nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,
- nx_system_initialize

## <a name="nx_ip_create"></a>nx_ip_create

IP örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_create(
    NX_IP *ip_ptr, 
    CHAR *name, 
    ULONG ip_address,
    ULONG network_mask, 
    NX_PACKET_POOL *default_pool,
    VOID (*ip_network_driver)(NX_IP_DRIVER *),
    VOID *memory_ptr, 
    ULONG memory_size,
    UINT priority);
```

### <a name="description"></a>Açıklama

Bu hizmet, Kullanıcı tarafından sağlanan IP adresi ve ağ sürücüsüne sahip bir IP örneği oluşturur. Ayrıca, uygulamanın, iç paket ayırması için kullanacağı IP örneği için önceden oluşturulmuş bir paket havuzu sağlaması gerekir. Sağlanan uygulama ağ sürücüsünün bu IP iş parçacığı yürütülene kadar çağrılmadığını unutmayın.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Yeni bir IP örneği oluşturmak için denetim bloğu işaretçisi.
- **ad** Bu yeni IP örneğinin adı.
- **ip_address** Bu yeni IP örneğinin IP adresi.
- **network_mask** Alt ağ ve süper netme kullanımları için IP adresinin ağ bölümünü maskelemek için maske.
- **default_pool** Daha önce oluşturulmuş NetX paket havuzunun denetim bloğuna yönelik işaretçi.
- **ip_network_driver** IP paketleri göndermek ve almak için kullanılan Kullanıcı tarafından sağlanan ağ sürücüsü.
- **memory_ptr** IP Yardımcısı iş parçacığının yığın alanı için bellek alanı işaretçisi.
- **memory_size** IP Yardımcısı iş parçacığı yığınının bellek alanındaki bayt sayısı.
- **Öncelik** IP Yardımcısı iş parçacığının önceliği.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı IP örneği oluşturma.
- **NX_NOT_IMPLEMENTED** (0x4A) NETX kitaplığı yanlış yapılandırılmış.
- **NX_PTR_ERROR** (0x07) geçersiz IP, ağ sürücüsü işlev işaretçisi, paket havuzu veya bellek işaretçisi.
- **NX_SIZE_ERROR** (0x09) sağlanan yığın boyutu çok küçük.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_IP_ADDRESS_ERROR** (0x21) sağlanan IP adresi geçersiz.
- **NX_OPTION_ERROR** (0x21) sağlanan IP iş parçacığı önceliği geçersiz.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Create an IP instance with an IP address of 1.2.3.4 and a network
    mask of 0xFFFFFF00UL. The "ethernet_driver" specifies the entry
    point of the application specific network driver and the
    "stack_memory_ptr" specifies the start of a 1024 byte memory
    area that is used for this IP instance’s helper thread.  */
status = nx_ip_create(
    &ip_0, 
    "NetX IP Instance ip_0",
    IP_ADDRESS(1, 2, 3, 4),
    0xFFFFFF00UL, &pool_0, 
    ethernet_driver,
    stack_memory_ptr, 
    1024, 
    1);

/* If status is NX_SUCCESS, the IP instance has been created. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,
- nx_system_initialize

## <a name="nx_ip_delete"></a>nx_ip_delete

Önceden oluşturulan IP örneğini Sil


### <a name="prototype"></a>Prototype

```C
UINT nx_ip_delete(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir IP örneğini siler ve IP örneğinin sahip olduğu tüm sistem kaynaklarını serbest bırakır.

### <a name="parameters"></a>Parametreler
- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP silme işlemi.
- **NX_SOCKETS_BOUND** (0x28) bu IP örneğine, bağımlı UDP veya TCP yuvaları hala sahip. IP örneği silinmeden önce tüm yuvaların bağlantısı kesildi ve silinmemelidir.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```C
/* Delete a previously created IP instance. */
status = nx_ip_delete(&ip_0);

/* If status is NX_SUCCESS, the IP instance has been deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,
- nx_system_initialize

## <a name="nx_ip_driver_direct_command"></a>nx_ip_driver_direct_command

Ağ sürücüsüne komut verme

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_driver_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    ULONG *return_value_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, uygulamanın ***nx_ip_create*** çağrısı sırasında belirtilen birincil ağ arabirimi sürücüsüne doğrudan bir arabirim sağlar.

Uygulamaya özgü komutlar, sayısal değerleri NX_LINK_USER_COMMAND daha büyük veya eşit bir değere göre kullanılabilir.

*İkincil cihaz için komut vermek üzere **nx_ip_driver_interface_direct_command** hizmetini kullanın.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **komut** Sayısal komut kodu. Standart komutlar aşağıdaki gibi tanımlanır:

- NX_LINK_GET_STATUS (10)
- NX_LINK_GET_SPEED (11)
- NX_LINK_GET_DUPLEX_TYPE (12)
- NX_LINK_GET_ERROR_COUNT (13)
- NX_LINK_GET_RX_COUNT (14)
- NX_LINK_GET_TX_COUNT (15)
- NX_LINK_GET_ALLOC_ERRORS (16)
- NX_LINK_USER_COMMAND (50)

- **return_value_ptr** Çağıran değişkenin dönüş işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) ağ sürücüsü doğrudan komutu başarıyla açıldı.
- **NX_UNHANDLED_COMMAND** (0x44) işlenmemiş veya uygulanmayan ağ sürücüsü komutu.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya dönüş değeri işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_INVALID_INTERFACE** (0x4C) geçersiz arabirim dizini.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

- **Önalım mümkün**

Hayır

### <a name="example"></a>Örnek

```C
/* Make a direct call to the application-specific network driver
    for the previously created IP instance. For this example, the
    network driver is interrogated for the link status. */
status = nx_ip_driver_direct_command(
    &ip_0, NX_LINK_GET_STATUS,
    &link_status);

/* If status is NX_SUCCESS, the link_status variable contains a
    NX_TRUE or NX_FALSE value representing the status of the
    physical link. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_interface_direct_command,
- nx_ip_forwarding_disable, nx_ip_forwarding_enable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_driver_interface_direct_command"></a>nx_ip_driver_interface_direct_command

Ağ sürücüsüne komut verme

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_driver_interface_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    UINT interface_index,
    ULONG *return_value_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, IP örneğindeki uygulamanın ağ aygıtı sürücüsüne doğrudan bir komut sağlar. Uygulamaya özgü komutlar, sayısal değerleri *NX_LINK_USER_COMMAND* daha büyük veya eşit bir değere göre kullanılabilir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **komut** Sayısal komut kodu. Standart komutlar aşağıdaki gibi tanımlanır:
- NX_LINK_GET_STATUS (10)
- NX_LINK_GET_SPEED (11)
- NX_LINK_GET_DUPLEX_TYPE (12)
- NX_LINK_GET_ERROR_COUNT (13)
- NX_LINK_GET_RX_COUNT (14)
- NX_LINK_GET_TX_COUNT (15)
- NX_LINK_GET_ALLOC_ERRORS (16)
- NX_LINK_USER_COMMAND (50)
- **interface_index** Komutun gönderilmesi gereken ağ arabiriminin dizini.
- **return_value_ptr** Çağıran değişkenin dönüş işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) ağ sürücüsü doğrudan komutu başarıyla açıldı.
- **NX_UNHANDLED_COMMAND** (0x44) işlenmemiş veya uygulanmayan ağ sürücüsü komutu.
- **NX_INVALID_INTERFACE** (0x4C) geçersiz arabirim dizini
- **NX_PTR_ERROR** (0x07) geçersiz IP veya dönüş değeri işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Make a direct call to the application-specific network driver
    for the previously created IP instance. For this example, the
    network driver is interrogated for the link status. */

/* Set the interface index to the primary device. */
UINT interface_index = 0;
    status = nx_ip_driver_interface_direct_command(&ip_0,
    NX_LINK_GET_STATUS,
    interface_index,
    &link_status);
/* If status is NX_SUCCESS, the link_status variable contains a
    NX_TRUE or NX_FALSE value representing the status of the
    physical link. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_forwarding_disable, nx_ip_forwarding_enable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_forwarding_disable"></a>nx_ip_forwarding_disable

IP paket iletmeyi devre dışı bırak

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_forwarding_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, IP paketlerinin NetX IP bileşeni içinde iletilmesini devre dışı bırakır. Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP iletimi devre dışı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Disable IP forwarding on this IP instance. */
status = nx_ip_forwarding_disable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been disabled on the
    previously created IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_enable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_forwarding_enable"></a>nx_ip_forwarding_enable

IP paket iletmeyi etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_forwarding_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, IP paketlerinin NetX IP bileşeni içinde iletilmesine izin vermez. Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı IP iletimi etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable IP forwarding on this IP instance. */
status = nx_ip_forwarding_enable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been enabled on the
    previously created IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_fragment_disable"></a>nx_ip_fragment_disable

IP paketi fragmenting devre dışı bırak

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_fragment_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, IP paketi fragmenting devre dışı bırakır ve işlevselliği yeniden birleştirir. Yeniden birleştirilme bekleyen paketler için, bu hizmet bu paketleri yayınlar. Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı IP parçası devre dışı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) IP örneğinde IP parçalanması etkin değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Disable IP fragmenting on this IP instance. */
status = nx_ip_fragment_disable(&ip_0);

/* If status is NX_SUCCESS, disables IP fragmenting on the
    previously created IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_fragment_enable"></a>nx_ip_fragment_enable

IP paketi fragmenting etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_fragment_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, IP paketi fragmenting ve yeniden birleştirilen işlevselliği sunar. Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP parçası etkinleştirme.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) IP parçalanma özellikleri NETX olarak derlenmedi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable IP fragmenting on this IP instance. */
status = nx_ip_fragment_enable(&ip_0);

/* If status is NX_SUCCESS, IP fragmenting has been enabled on the
    previously created IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_gateway_address_set"></a>nx_ip_gateway_address_set

Ağ geçidi IP adresi ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_gateway_address_set(
    NX_IP *ip_ptr, 
    ULONG ip_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, IP ağ geçidi IP adresini ayarlar. Tüm ağ dışı trafik, iletim için bu ağ geçidine yönlendirilir. Ağ geçidine ağ arabirimlerinden biri aracılığıyla doğrudan erişilebilir olması gerekir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** Ağ geçidinin IP adresi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ağ geçidi IP adresi kümesi.
- **NX_PTR_ERROR** (0x07) geçersiz IP örneği işaretçisi.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacığı

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Setup the Gateway address for previously created IP
    Instance ip_0. */
status = nx_ip_gateway_address_set(&ip_0, IP_ADDRESS(1,2,3,99));

/* If status is NX_SUCCESS, all out-of-network send requests are
    routed to 1.2.3.99. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_info_get, nx_ip_static_route_add, nx_ip_static_route_delete

## <a name="nx_ip_info_get"></a>nx_ip_info_get

IP etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_info_get(
    NX_IP *ip_ptr,
    ULONG *ip_total_packets_sent,
    ULONG *ip_total_bytes_sent,
    ULONG *ip_total_packets_received,
    ULONG *ip_total_bytes_received,
    ULONG *ip_invalid_packets,
    ULONG *ip_receive_packets_dropped,
    ULONG *ip_receive_checksum_errors,
    ULONG *ip_send_packets_dropped,
    ULONG *ip_total_fragments_sent,
    ULONG *ip_total_fragments_received);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için IP etkinlikleri hakkında bilgi alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_total_packets_sent** Gönderilen IP paketlerinin toplam sayısı için hedef işaretçisi.
- **ip_total_bytes_sent** Gönderilen toplam bayt sayısı için hedef işaretçisi.
- **ip_total_packets_received** IP alma paketlerinin toplam sayısının hedefi işaretçisi.
- **ip_total_bytes_received** Alınan IP baytlarının toplam sayısının hedefi işaretçisi.
- **ip_invalid_packets** Toplam geçersiz IP paketi sayısının hedefi işaretçisi.
- **ip_receive_packets_dropped** Bırakılan toplam alım paketi sayısının hedefi işaretçisi.
- **ip_receive_checksum_errors** Alma paketlerindeki toplam sağlama toplamı hatalarının hedefi işaretçisi.
- **ip_send_packets_dropped** Bırakılan Toplam gönderme paketi sayısının hedefi işaretçisi.
- **ip_total_fragments_sent** Gönderilen toplam parçacık sayısının hedefi işaretçisi.
- **ip_total_fragments_received** Toplam alınan parçacık sayısının hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP bilgisi alma.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve IP information from previously created IP
Instance 0. */
status = nx_ip_info_get(&ip_0,
    &ip_total_packets_sent,
    &ip_total_bytes_sent,
    &ip_total_packets_received,
    &ip_total_bytes_received,
    &ip_invalid_packets,
    &ip_receive_packets_dropped,
    &ip_receive_checksum_errors,
    &ip_send_packets_dropped,
    &ip_total_fragments_sent,
    &ip_total_fragments_received);

/* If status is NX_SUCCESS, IP information was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_interface_address_get"></a>nx_ip_interface_address_get

Arabirim IP adresini al

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_interface_address_get (
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *ip_address,
    ULONG *network_mask);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ağ arabiriminin IP adresini alır.

*Birincil cihaz değilse belirtilen cihaz, daha önce IP örneğine eklenmiş olmalıdır.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **interface_index** Arabirim dizini, IP örneğine iliştirilmiş ağ arabiriminin diziniyle aynı değer.
- **ip_address** Cihaz arabirimi IP adresi için hedef işaretçisi.
- **network_mask** Cihaz arabirimi ağ maskesi için hedef işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP adresi al.
- **NX_INVALID_INTERFACE** (0x4C) belirtilen ağ arabirimi geçersiz.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
#define INTERFACE_INDEX 1
/* Get device IP address and network mask for the specified
    interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_get(ip_ptr,INTERFACE_INDEX,
    &ip_address, &network_mask);

/* If status is NX_SUCCESS the interface address was successfully
    retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_set, nx_ip_interface_attach,
- nx_ip_interface_info_get, nx_ip_interface_status_check,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_address_set"></a>nx_ip_interface_address_set

Arabirim IP adresi ve ağ maskesini ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP arabirimi için IP adresini ve ağ maskesini ayarlar.

*Belirtilen arabirim daha önce IP örneğine eklenmiş olmalıdır.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **interface_index** NetX örneğine iliştirilmiş arabirimin dizini.
- **ip_address** Yeni ağ arabirimi IP adresi.
- **network_mask** Yeni Arabirim ağ maskesi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP adresi kümesi.
- **NX_INVALID_INTERFACE** (0x4C) belirtilen ağ arabirimi geçersiz.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçiler.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
#define INTERFACE_INDEX 1
/* Set device IP address and network mask for the specified
    interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_set(ip_ptr, INTERFACE_INDEX,
    ip_address, network_mask);

/* If status is NX_SUCCESS the interface IP address and mask was
successfully set. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get, nx_ip_interface_attach,
- nx_ip_interface_info_get, nx_ip_interface_status_check,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_attach"></a>nx_ip_interface_attach

Ağ arabirimini IP örneğine Ekle

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_interface_attach(
    NX_IP *ip_ptr, 
    CHAR *interface_name,
    ULONG ip_address,
    ULONG network_mask,
    VOID(*ip_link_driver)
    (struct NX_IP_DRIVER_STRUCT *));
```

### <a name="description"></a>Açıklama

Bu hizmet, IP arabirimine bir fiziksel ağ arabirimi ekler. Bu durumda, her ek arabirimin birincil arabirime ikincil olması için, IP örneğinin birincil arabirimle oluşturulduğunu aklınızda bulunur. IP örneğine (birincil arabirim dahil) bağlı olan ağ arabirimlerinin toplam sayısı **NX_MAX_PHYSICAL_INTERFACES** aşamaz.

IP iş parçacığı henüz çalışmıyorsa, ikincil arabirimler tüm fiziksel arabirimleri Başlatan IP iş parçacığı başlatma sürecinin bir parçası olarak başlatılır.

IP iş parçacığı henüz çalışmıyorsa, ikincil arabirim ***nx_ip_interface_attach*** hizmetin bir parçası olarak başlatılır.

*ip_ptr geçerli bir NetX IP yapısına işaret etmelidir.*

- *IP örneği için ağ arabirimlerinin sayısı için **NX_MAX_PHYSICAL_INTERFACES** yapılandırılması gerekir. Varsayılan değer bir değeridir.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **interface_name** Arabirim adı dizesinin işaretçisi.
- **ip_address** Konak bayt düzeninde cihaz IP adresi.
- **network_mask** Konak bayt düzeninde cihaz ağ maskesi.
- **ip_link_driver** Arabirim için Ethernet sürücüsü.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) girişi statik yönlendirme tablosuna eklenir.
- **NX_NO_MORE_ENTRIES** (0x17) en fazla arabirim sayısı.
- **NX_MAX_PHYSICAL_INTERFACES** aşıldı.
- **NX_DUPLICATED_ENTRY** (0x52) sağlanan IP adresı bu IP örneğinde zaten kullanılıyor.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi girişi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Attach secondary device for device IP address 192.168.1.68 with
    the specified Ethernet driver. */
status = nx_ip_interface_attach(ip_ptr, “secondary_port”,
    IP_ADDRESS(192,168,1,68),
    0xFFFFFF00UL,
    nx_etherDriver);
/* If status is NX_SUCCESS the interface was successfully added to
    the IP instance interface table. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get, nx_ip_interface_address_set,
- nx_ip_interface_info_get, nx_ip_interface_status_check,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_info_get"></a>nx_ip_interface_info_get

Ağ arabirimi parametrelerini al


### <a name="prototype"></a>Prototype

```C
UINT nx_ip_interface_info_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    CHAR **interface_name,
    ULONG *ip_address,
    ULONG *network_mask,
    ULONG *mtu_size,
    ULONG *physical_address_msw,
    ULONG *physical_address_lsw);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen ağ arabirimi için ağ parametreleriyle ilgili bilgileri alır. Tüm veriler ana bilgisayar bayt düzeninde alınır.

*ip_ptr geçerli bir NetX IP yapısına işaret etmelidir. Belirtilen arabirim, birincil arabirim değilse, daha önce IP örneğine eklenmelidir.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **interface_index** Ağ arabirimini belirten Dizin.
- **interface_name** Ağ arabiriminin adını tutan arabelleğin işaretçisi.
- **ip_address** Arabirimin IP adresi için hedefin işaretçisi.
- **network_mask** Ağ maskesi için hedef işaretçisi.
- **mtu_size** Bu arabirim için en fazla aktarım birimi için hedef işaretçisi.
- **physical_address_msw** Cihaz MAC adresi için en iyi 16 bit için hedef işaretçisi.
- **physical_address_lsw** Cihaz MAC adresinin daha düşük 32 bitleri için hedef işaretçisi.


### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) arabirim bilgisi alındı.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi.
- **NX_INVALID_INTERFACE** (0x4C) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve interface parameters for the specified interface (index
    1 in IP instance list of interfaces). */
#define INTERFACE_INDEX 1

status = nx_ip_interface_info_get(ip_ptr, INTERFACE_INDEX,
    &name_ptr, &ip_address,
    &network_mask,
    &mtu_size,
    &physical_address_msw,
    &physical_address_lsw);

/* If status is NX_SUCCESS the interface information is
    successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get, nx_ip_interface_address_set,
- nx_ip_interface_attach, nx_ip_interface_status_check,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_status_check"></a>nx_ip_interface_status_check

Bir IP örneğinin durumunu denetleme


### <a name="prototype"></a>Prototype

```C
UINT nx_ip_interface_status_check(
    NX_IP *ip_ptr,
    UINT interface_index
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş bir IP örneğinin ağ arabiriminin belirtilen durumunu denetler ve isteğe bağlı olarak bekler.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **interface_index** Arabirim dizin numarası
- **needed_status** Aşağıdaki gibi bit eşleme biçiminde tanımlanan IP durumu istendi:
    - NX_IP_INITIALIZE_DONE (0x0001)
    - NX_IP_ADDRESS_RESOLVED (0x0002)
    - NX_IP_LINK_ENABLED (0x0004)
    - NX_IP_ARP_ENABLED (0x0008)
    - NX_IP_UDP_ENABLED (0x0010)
    - NX_IP_TCP_ENABLED (0x0020)
    - NX_IP_IGMP_ENABLED (0x0040)
    - NX_IP_RARP_COMPLETE (0x0080)
    - NX_IP_INTERFACE_LINK_ENABLED (0x0100)
- **actual_status** Gerçek bitler kümesinin hedefi işaretçisi.
- **wait_option** İstenen durum bitleri yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - NX_NO_WAIT (0x00000000)
    - NX_WAIT_FOREVER (0xFFFFFFFF)
    - ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP durum denetimi.
- **NX_NOT_SUCCESSFUL** (0x43) durum isteği belirtilen zaman aşımı süresi içinde karşılanmadı.
- **NX_PTR_ERROR** (0x07) IP işaretçisi veya geçersiz hale geldi ya da gerçek durum işaretçisi geçersiz.
- **NX_OPTION_ERROR** (0X0a) geçersiz gerekli durum seçeneği.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_INVALID_INTERFACE** (0x4C) Interface_index Aralık dışında. ya da arabirim geçerli değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Wait 10 ticks for the link up status on the previously created IP
    instance. */
status = nx_ip_interface_status_check(&ip_0, 1, NX_IP_LINK_ENABLED,
    &actual_status, 10);

/* If status is NX_SUCCESS, the secondary link for the specified IP
    instance is up. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get, nx_ip_interface_address_set,
- nx_ip_interface_attach, nx_ip_interface_info_get,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_link_status_change_notify_set"></a>nx_ip_link_status_change_notify_set

Bağlantı durumu değiştirme bildirimi geri arama işlevini ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_link_status_change_notify_set(
    NX_IP *ip_ptr,
    VOID (*link_status_change_notify)(NX_IP *ip_ptr, UINT interface_index, UINT link_up));
```

### <a name="description"></a>Açıklama

Bu hizmet bağlantı durumu değişikliği bildirim geri arama işlevini yapılandırır. Kullanıcı tarafından sağlanan *link_status_change_notify* yordamı, birincil veya ikincil arabirim durumu DEĞIŞTIRILDIĞINDE (IP adresi değiştirildiğinde) çağrılır. *LINK_STATUS_CHANGE_NOTIFY* null ise, bağlantı durumu değiştirme bildirimi geri arama özelliği devre dışıdır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **link_status_change_notify** Fiziksel arabirimde bir değişiklikten sonra çağrılacak Kullanıcı tarafından sağlanan geri arama işlevi.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı küme
- **NX_PTR_ERROR** (0x07) geçersiz IP denetim bloğu işaretçisi veya yeni fiziksel adres işaretçisi
- **NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.


### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Configure a callback function to be used when the physical
    interface status is changed. */
status = nx_ip_link_status_change_notify_set(&ip_0, my_change_cb);

/* If status == NX_SUCCESS, the link status change notify function
    is set. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get, nx_ip_interface_address_set,
- nx_ip_interface_attach, nx_ip_interface_info_get,
- nx_ip_interface_status_check

## <a name="nx_ip_raw_packet_disable"></a>nx_ip_raw_packet_disable

Ham paket göndermeyi/almayı devre dışı bırak


### <a name="prototype"></a>Prototype

```C
UINT nx_ip_raw_packet_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu IP örneği için ham IP paketlerinin aktarımını ve alımını devre dışı bırakır. Ham paket hizmeti önceden etkinleştirildiyse ve alma kuyruğunda ham paketler varsa, bu hizmet alınan tüm ham paketleri serbest bırakabilir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP ham paket devre dışı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Disable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_disable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
    been disabled for the previously created IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_enable, nx_ip_raw_packet_receive,
- nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send

## <a name="nx_ip_raw_packet_enable"></a>nx_ip_raw_packet_enable

Ham paket işlemeyi etkinleştir


### <a name="prototype"></a>Prototype

```C
UINT nx_ip_raw_packet_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu IP örneği için ham IP paketleri aktarımına ve alımına izin vermez. Gelen TCP, UDP, ıCMP ve ıGMP paketleri hala NetX tarafından işlenir. Bilinmeyen üst katman protokol türlerine sahip paketler, ham paket alma yordamına göre işlenir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP ham paket etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_enable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
    been enabled for the previously created IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable, nx_ip_raw_packet_receive,
- nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send

## <a name="nx_ip_raw_packet_interface_send"></a>nx_ip_raw_packet_interface_send

Belirtilen ağ arabirimi aracılığıyla ham IP paketi gönder

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_raw_packet_interface_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    UINT address_index,
    ULONG type_of_service);
```

### <a name="description"></a>Açıklama

Bu hizmet, kaynak adres olarak belirtilen yerel IP adresini ve ilişkili ağ arabirimini kullanarak hedef IP adresine bir ham IP paketi gönderir. Bu yordamın hemen geri döndüğüne ve bu nedenle, IP paketinin gerçekten gönderildiyse bilinmediğini unutmayın. Ağ sürücüsü, iletim tamamlandığında paketin serbest bırakılmasından sorumlu olacaktır. Bu hizmet, paketin gerçekten gönderilip gönderilmediğini bilmenin bir yolu olmadığından diğer hizmetlerden farklıdır. Internet 'te kaybolabilir.

*Ham IP işlemenin etkin olması gerektiğini unutmayın.*

*Bu hizmet **nx_ip_raw_packet_send** benzerdir, ancak bu hizmet, bir uygulamanın belirtilen fiziksel ARABIRIMLERDEN ham IP paketi göndermesini sağlar.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP görevi işaretçisi.
- **packet_ptr** İletilecek paket işaretçisi.
- **destination_ip** Paketin gönderileceği IP adresi.
- **address_index** Paketin dışına gönderilmesi için arabirim adresinin dizini.
- **Type_of_service** Paket için hizmet türü.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) paketi başarıyla iletildi.
- **NX_IP_ADDRESS_ERROR** (0x21) uygun bir giden arabirim yok.
- **NX_NOT_ENABLED** (0x14) ham IP paket işleme etkin değil.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi.
- **NX_OPTION_ERROR** (0X0a) geçersiz hizmet türü belirtildi.
- **NX_OVERFLOW** (0x03) geçersiz paket önüne işaretçisi.
- **NX_UNDERFLOW** (0x02) geçersiz paket önüne işaretçisi.
- **NX_INVALID_INTERFACE** (0x4C) geçersiz arabirim dizini belirtildi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
#define ADDRESS_IDNEX 1
/* Send packet out on interface 1 with normal type of service. */
status = nx_ip_raw_packet_interface_send(ip_ptr, packet_ptr,
    destination_ip,
    ADDRESS_INDEX,
    NX_IP_NORMAL);
/* If status is NX_SUCCESS the packet was successfully transmitted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,
- nx_ip_raw_packet_receive, nx_ip_raw_packet_send

## <a name="nx_ip_raw_packet_receive"></a>nx_ip_raw_packet_receive

Ham IP paketi al

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_raw_packet_receive(
    NX_IP *ip_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneğinden bir ham IP paketi alır. Ham paket alma kuyruğunda IP paketleri varsa, arayana ilk (en eski) paket döndürülür. Aksi takdirde, kullanılabilir bir paket yoksa, çağıran bekleme seçeneğinde belirtilen şekilde askıya alabilir.

*NX_SUCCESS, döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **packet_ptr** Alınan ham IP paketinin yerleştirileceği işaretçiye işaretçi.
- **wait_option** Kullanılabilir ham IP paketleri yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP ham paket alma.
- **NX_NO_PACKET** (0x01) kullanılabilir paket yok.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya dönüş paketi işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Receive a raw IP packet for this IP instance, wait for a maximum
    of 4 timer ticks. */
status = nx_ip_raw_packet_receive(&ip_0, &packet_ptr, 4);

/* If status is NX_SUCCESS, the raw IP packet pointer is in the
    variable packet_ptr. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,
- nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send

## <a name="nx_ip_raw_packet_send"></a>nx_ip_raw_packet_send

Ham IP paketi gönder

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_raw_packet_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    ULONG type_of_service);
```

### <a name="description"></a>Açıklama

Bu hizmet hedef IP adresine bir ham IP paketi gönderir. Bu yordamın hemen geri döndüğüne ve bu nedenle IP paketinin gerçekten gönderilip gönderilmediğini bilinmediğini unutmayın. Ağ sürücüsü, iletim tamamlandığında paketin serbest bırakılmasından sorumlu olacaktır.

NetX, çok ana bir sistem için hedef IP adresini kullanarak uygun bir ağ arabirimi bulur ve arabirimin IP adresini kaynak adres olarak kullanır. Hedef IP adresi yayın veya çok noktaya yayın ise, ilk geçerli arabirim kullanılır. Uygulamalar bu durumda ***nx_ip_raw_packet_interface_send*** kullanır.

*Bir hata döndürülmediği takdirde, uygulama bu çağrıdan sonra paketi serbest bırakmamalıdır. Bunu yapmak öngörülemeyen sonuçlara neden olur çünkü ağ sürücüsü iletim sonrasında paketi serbest bırakacaktır.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **packet_ptr** Gönderilen ham IP paketinin işaretçisi.
- **destination_ip** Hedef IP adresi, belirli bir ana bilgisayar IP adresi, bir ağ yayını, iç geri döngü veya çok noktaya yayın adresi olabilir.
- **Type_of_service** İletim için hizmet türünü tanımlar, yasal değerler aşağıdaki gibidir:
- NX_IP_NORMAL (0x00000000)
- NX_IP_MIN_DELAY (0x00100000)
- NX_IP_MAX_DATA (0x00080000)
- NX_IP_MAX_RELIABLE (0x00040000)
- NX_IP_MIN_COST (0x00020000)


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP ham paket gönderimi başlatıldı.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_NOT_ENABLED** (0x14) ham IP özelliği etkin değil.
- **NX_OPTION_ERROR** (0X0a) geçersiz hizmet türü.
- **NX_UNDERFLOW** (0x02) pakette bir IP üst bilgisini eklemek için yeterli yer yok.
- **NX_OVERFLOW** (0x03) paket ekleme işaretçisi geçersiz.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya paket işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Send a raw IP packet to IP address 1.2.3.5. */
status = nx_ip_raw_packet_send(&ip_0, packet_ptr,
    IP_ADDRESS(1,2,3,5),
    NX_IP_NORMAL);

/* If status is NX_SUCCESS, the raw IP packet pointed to by
    packet_ptr has been sent. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,
- nx_ip_raw_packet_receive, nx_ip_raw_packet_send,
- nx_ip_raw_packet_interface_send

## <a name="nx_ip_static_route_add"></a>nx_ip_static_route_add

Yönlendirme tablosuna statik yol ekleme

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_static_route_add(
    NX_IP *ip_ptr,
    ULONG network_address,
    ULONG net_mask,
    ULONG next_hop);
```

### <a name="description"></a>Açıklama

Bu hizmet, statik yönlendirme tablosuna bir giriş ekler. *Next_hop* adresine yerel ağ aygıtlarından birinden doğrudan erişilebilir olması gerektiğini unutmayın.

*İp_ptr geçerli bir NetX IP yapısına işaret etmelidir ve NetX kitaplığı bu hizmeti kullanmak için tanımlanan NX_ENABLE_IP_STATIC_ROUTING oluşturulmuş olmalıdır. Varsayılan olarak NetX, NX_ENABLE_IP_STATIC_ROUTING tanımlı olmadan oluşturulur.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **network_address** Konak bayt düzeninde hedef ağ adresi
- **net_mask** Konak bayt düzeninde hedef ağ maskesi
- **next_hop** Hedef ağ için, ana bilgisayar bayt düzeninde sonraki atlama adresi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) girişi statik yönlendirme tablosuna eklenir.
- **NX_OVERFLOW** (0x03) statik yönlendirme tablosu dolu.
- **NX_NOT_SUPPORTED** (0x4b) Bu özellik ' de derlenmiyor.
- **NX_IP_ADDRESS_ERROR** (0x21) sonraki atlama, yerel arabirimler aracılığıyla doğrudan erişilemez.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_PTR_ERROR** (0x07) geçersiz ip_ptr işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Specify the next hop for the 192.168.10.0 through the gateway
    192.168.1.1. */
status = nx_ip_static_route_add(ip_ptr, IP_ADDRESS(192,168,10,0),
    0xFFFFFF00UL,
    IP_ADDRESS(192,168,1,1));

/* If status is NX_SUCCESS the route was successfully added to the
    static routing table. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_delete

## <a name="nx_ip_static_route_delete"></a>nx_ip_static_route_delete

Yönlendirme tablosundan statik yolu Sil

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_static_route_delete(
    NX_IP *ip_ptr,
    ULONG network_address, 
    ULONG net_mask);
```

### <a name="description"></a>Açıklama

Bu hizmet, statik yönlendirme tablosundan bir girişi siler.

*İp_ptr geçerli bir NetX IP yapısına işaret etmelidir ve NetX kitaplığı bu hizmeti kullanmak için tanımlanan NX_ENABLE_IP_STATIC_ROUTING oluşturulmuş olmalıdır. Varsayılan olarak NetX, NX_ENABLE_IP_STATIC_ROUTING tanımlı olmadan oluşturulur.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **network_address** Konak bayt düzeninde hedef ağ adresi.
- **net_mask** Konak bayt düzeninde hedef ağ maskesi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Remove the static route for 192.168.10.0 from the routing table.*/
status = nx_ip_static_route_delete(ip_ptr,
    IP_ADDRESS(192,168,10,0), 0xFFFFFF00UL,);

/* If status is NX_SUCCESS the route was successfully removed from
    the static routing table. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_add

## <a name="nx_ip_status_check"></a>nx_ip_status_check

Bir IP örneğinin durumunu denetleme

### <a name="prototype"></a>Prototype

```C
UINT nx_ip_status_check(
    NX_IP *ip_ptr,
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş bir IP örneğinin birincil ağ arabiriminin belirtilen durumunu denetler ve isteğe bağlı olarak bekler. İkincil arabirimlerde durum almak için, uygulamalar hizmeti ***nx_ip_interface_status_check kullanacaktır.***

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **needed_status** Aşağıdaki gibi bit eşleme biçiminde tanımlanan IP durumu istendi:
- NX_IP_INITIALIZE_DONE (0x0001)
- NX_IP_ADDRESS_RESOLVED (0x0002)
- NX_IP_LINK_ENABLED (0x0004)
- NX_IP_ARP_ENABLED (0x0008)
- NX_IP_UDP_ENABLED (0x0010)
- NX_IP_TCP_ENABLED (0x0020)
- NX_IP_IGMP_ENABLED (0x0040)
- NX_IP_RARP_COMPLETE (0x0080)
- NX_IP_INTERFACE_LINK_ENABLED (0x0100)
- **actual_status** Gerçek bitler kümesinin hedefi işaretçisi.
- **wait_option** İstenen durum bitleri yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı IP durum denetimi.
- **NX_NOT_SUCCESSFUL** (0x43) durum isteği belirtilen zaman aşımı süresi içinde karşılanmadı.
- **NX_PTR_ERROR** (0x07) IP işaretçisi veya geçersiz hale geldi ya da gerçek durum işaretçisi geçersiz.
- **NX_OPTION_ERROR** (0X0a) geçersiz gerekli durum seçeneği.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Wait 10 ticks for the link up status on the previously created IP
    instance. */
status = nx_ip_status_check(&ip_0, NX_IP_LINK_ENABLED,
    &actual_status, 10);

/* If status is NX_SUCCESS, the link for the specified IP instance
    is up. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_system_initialize

## <a name="nx_packet_allocate"></a>nx_packet_allocate

Belirtilen havuzdan paket ayır

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_allocate(
    NX_PACKET_POOL *pool_ptr,
    NX_PACKET **packet_ptr,
    ULONG packet_type,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet belirtilen havuzdan bir paket ayırır ve belirtilen paket türüne göre paketteki preppointer 'ı ayarlar. Kullanılabilir bir paket yoksa hizmet, sağlanan bekleme seçeneğine göre askıya alır.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Daha önce oluşturulan paket havuzuna yönelik işaretçi.
- **packet_ptr** Ayrılan paket işaretçisinin işaretçisine yönelik işaretçi.
- **packet_type** İstenen paket türünü tanımlar. Desteklenen paket türlerinin listesi için, Bölüm 3 ' teki "Paket havuzları 49" bölümüne bakın.
- **wait_option** Paket havuzunda kullanılabilir bir paket yoksa, zaman işaretleri cinsinden bekleme süresini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket ayırması.
- **NX_NO_PACKET** (0x01) kullanılabilir paket yok.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.
- **NX_OPTION_ERROR** (0X0a) geçersiz paket türü.
- **NX_PTR_ERROR** (0x07) geçersiz havuz veya paket döndürme işaretçisi.
- **NX_CALLER_ERROR** (0x11) Iş parçacığından geçersiz bekleme seçeneği.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs (uygulama ağ sürücüleri). Wait seçeneği, ıSR 'de veya zamanlayıcı bağlamında kullanıldığında NX_NO_WAIT olmalıdır.

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Allocate a new UDP packet from the previously created packet pool
    and suspend for a maximum of 5 timer ticks if the pool is
    empty. */
status = nx_packet_allocate(&pool_0, &packet_ptr, NX_UDP_PACKET, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is
    found in the variable packet_ptr. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_copy"></a>nx_packet_copy

Paketi Kopyala

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_copy(
    NX_PACKET *packet_ptr,
    NX_PACKET **new_packet_ptr,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, sağlanan paketteki bilgileri sağlanan paket havuzundan ayrılan bir veya daha fazla yeni pakete kopyalar. Başarılı olursa, yeni pakete yönelik işaretçi **new_packet_ptr** tarafından işaret edilen hedefte döndürülür.

### <a name="parameters"></a>Parametreler

- **packet_ptr** Kaynak paketine yönelik işaretçi.
- **new_packet_ptr** Paketin yeni kopyasına işaretçinin nereye dönebileceği hedefe yönelik işaretçi.
- **pool_ptr** Kopya için bir veya daha fazla paket ayırmak için kullanılan önceden oluşturulmuş paket havuzuna yönelik işaretçi.
- **wait_option** Kullanılabilir bir paket yoksa hizmetin nasıl bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı paket kopyası.
- **NX_NO_PACKET** (0x01) paketi kopyalama için kullanılamaz.
- **NX_INVALID_PACKET** (0x12) boş kaynak paketi veya kopyalama başarısız oldu.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.
- **NX_PTR_ERROR** (0x07) geçersiz havuz, paket veya hedef işaretçisi.
- **NX_UNDERFLOW** (0x02) geçersiz paket önüne işaretçisi.
- **NX_OVERFLOW** (0x03) geçersiz paket ekleme işaretçisi.
- **NX_CALLER_ERROR** (0x11) başlatma veya ISR içinde bir bekleme seçeneği belirtildi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
NX_PACKET *new_copy_ptr;

/* Copy packet pointed to by "old_packet_ptr" using packets from
    previously created packet pool_0. */
status = nx_packet_copy(old_packet, &new_copy_ptr, &pool_0, 20);

/* If status is NX_SUCCESS, new_copy_ptr points to the packet copy. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_data_append"></a>nx_packet_data_append

Paketi sonuna veri Ekle

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_data_append(
    NX_PACKET *packet_ptr,
    VOID *data_start, 
    ULONG data_size,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, verileri belirtilen paketin sonuna ekler. Sağlanan veri alanı pakete kopyalanır. Yeterli kullanılabilir bellek yoksa ve zincirleme paket özelliği etkinse, isteği karşılamak için bir veya daha fazla paket ayrılır. Zincirleme paket özelliği etkinleştirilmemişse, *NX_SIZE_ERROR* döndürülür.

### <a name="parameters"></a>Parametreler

- **packet_ptr** Paket işaretçisi.
- **data_start** Pakete eklenecek kullanıcının veri alanının başlangıcına yönelik işaretçi.
- **data_size** Kullanıcının veri alanının boyutu.
- **pool_ptr** Geçerli pakette yeterli alan yoksa başka bir paketin ayırabileceği paket havuzu işaretçisi.
- **wait_option** Kullanılabilir bir paket yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket ekleme.
- **NX_NO_PACKET** (0x01) kullanılabilir paket yok.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği *tx_thread_wait_abort* bir çağrı tarafından iptal edildi.
- **NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.
- **NX_UNDERFLOW** (0x02) Prepend işaretçisi yük başlangıcından daha küçüktür.
- **NX_OVERFLOW** (0x03) ekleme işaretçisi yük ucundan daha büyük.
- **NX_PTR_ERROR** (0x07) geçersiz havuz, paket veya veri işaretçisi.
- **NX_SIZE_ERROR** (0x09) geçersiz veri boyutu.
- **NX_CALLER_ERROR** (0x11) Iş parçacığından geçersiz bekleme seçeneği.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs (uygulama ağ sürücüleri)

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Append "abcd" to the specified packet. */
status = nx_packet_data_append(packet_ptr, "abcd", 4, &pool_0, 5);

/* If status is NX_SUCCESS, the additional four bytes "abcd" have
    been appended to the packet. */
```


### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_copy, nx_packet_data_extract_offset,
- nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,
- nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_data_extract_offset"></a>nx_packet_data_extract_offset

Bir sapmayı kullanarak paketten veri ayıklama

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_data_extract_offset(
    NX_PACKET *packet_ptr,
    ULONG offset,
    VOID *buffer_start,
    ULONG buffer_length,
    ULONG *bytes_copied);
```

### <a name="description"></a>Açıklama

Bu hizmet bir NetX paketinden (veya paket zincirinden), belirtilen boyutun bayt cinsinden belirtilen baytından başlayarak belirtilen bir arabellekteki verileri kopyalar. Gerçekten kopyalanmış olan bayt sayısı *bytes_copied döndürülür.* Bu hizmet, paketten verileri kaldırmaz veya önüne işaretçisini veya diğer iç durum bilgilerini ayarlar.

### <a name="parameters"></a>Parametreler

- **packet_ptr** Ayıklanacak paket işaretçisi
- **konum** Geçerli önüne işaretçisinden gelen fark.
- **buffer_start** Kaydetme arabelleğinin başlangıcı işaretçisi
- **BUFFER_LENGTH** Kopyalanacak bayt sayısı
- **bytes_copied** Gerçekten kopyalandığı bayt sayısı

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket kopyası
- **NX_PACKET_OFFSET_ERROR** (0x53) geçersiz fark değeri sağlandı
- **NX_PTR_ERROR** (0x07) geçersiz paket işaretçisi veya arabellek işaretçisi

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Extract 10 bytes from the start of the received packet buffer
    into the specified memory area. */
status = nx_packet_data_extract_offset(my_packet, 0, &data[0], 10,
    &bytes_copied);

/* If status is NX_SUCCESS, 10 bytes were successfully copied into
    the data buffer. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,
- nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_data_retrieve"></a>nx_packet_data_retrieve

Paketten veri al

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_data_retrieve(
    NX_PACKET *packet_ptr,
    VOID *buffer_start, 
    ULONG *bytes_copied);
```

### <a name="description"></a>Açıklama

Bu hizmet, sağlanan paketten verileri sağlanan arabelleğe kopyalar. Hedef, **bytes_copied** tarafından işaret edilen hedefte döndürülen gerçek bayt sayısı.

Bu hizmetin paketin iç durumunu değiştirmediğini unutmayın. Alınmakta olan veriler pakette hala kullanılabilir durumda.

*Hedef arabelleğinin paketin içeriğini tutabilecek kadar büyük olması gerekir. Aksi takdirde, bellek bozulması öngörülemeyen sonuçlara neden olur.*

### <a name="parameters"></a>Parametreler

- **packet_ptr** Kaynak paketine yönelik işaretçi.
- **buffer_start** Arabellek alanının başlangıcına yönelik işaretçi.
- **bytes_copied** Kopyalanmış bayt sayısı için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket verileri alma.
- **NX_INVALID_PACKET** (0x12) geçersiz paket.
- **NX_PTR_ERROR** (0x07) geçersiz paket, arabellek başlangıcı veya bayt kopyalanmış işaretçi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
UCHAR buffer[512];
ULONG bytes_copied;

/* Retrieve data from packet pointed to by "packet_ptr". */
status = nx_packet_data_retrieve(packet_ptr, buffer, &bytes_copied);

/* If status is NX_SUCCESS, buffer contains the contents of the
    packet, the size of which is contained in "bytes_copied." */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_length_get,
- nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_length_get"></a>nx_packet_length_get

Paket verilerinin uzunluğunu al

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_length_get(
    NX_PACKET *packet_ptr, 
    ULONG *length);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen paketteki verilerin uzunluğunu alır.

### <a name="parameters"></a>Parametreler

- **packet_ptr** Pakete yönelik işaretçi.
- **uzunluk** Paket uzunluğu için hedef.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Get the length of the data in "my_packet." */
status = nx_packet_length_get(my_packet, &my_length);

/* If status is NX_SUCCESS, data length is in "my_length". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_pool_create"></a>nx_packet_pool_create

Belirtilen bellek alanında paket havuzu oluştur

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_pool_create(
    NX_PACKET_POOL *pool_ptr,
    CHAR *name,
    ULONG payload_size,
    VOID *memory_ptr,
    ULONG memory_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, Kullanıcı tarafından sağlanan bellek alanında belirtilen paket boyutunun bir paket havuzunu oluşturur.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Paket havuzu denetim bloğu işaretçisi.
- **ad** Paket havuzu için uygulama adı işaretçisi.
- **payload_size** Havuzdaki her paketteki bayt sayısı. Bu değer en az 40 bayt olmalıdır ve ayrıca 4 ile eşit olarak bölünebilmelidir.
- **memory_ptr** Paket havuzunun yerleştirileceği bellek alanına yönelik işaretçi. İşaretçi bir ULONG sınırında hizalanmalıdır.
- **memory_size** Havuz belleği alanının boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket havuzu oluşturma.
- **NX_PTR_ERROR** (0x07) geçersiz havuz veya bellek işaretçisi.
- **NX_SIZE_ERROR** (0x09) geçersiz blok veya bellek boyutu.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Create a packet pool of 32000 bytes starting at physical
    address 0x10000000. */
status = nx_packet_pool_create(&pool_0, "Default Pool", 128,
    (void *) 0x10000000, 32000);

/* If status is NX_SUCCESS, the packet pool has been successfully
    created. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_delete, nx_packet_pool_info_get,
- nx_packet_release, nx_packet_transmit_release

## <a name="nx_packet_pool_delete"></a>nx_packet_pool_delete

Önceden oluşturulmuş paket havuzunu Sil

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_pool_delete(NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir paket havuzunu siler. NetX, paket havuzundaki paketlerde Şu anda askıya alınmış olan her iş parçacığını denetler ve askıya alınma 'yi temizler.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Paket havuzu denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket havuzu silme.
- **NX_PTR_ERROR** (0x07) geçersiz havuz işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```C
/* Delete a previously created packet pool. */
status = nx_packet_pool_delete(&pool_0);

/* If status is NX_SUCCESS, the packet pool has been successfully
    deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_pool_info_get"></a>nx_packet_pool_info_get

Bir paket havuzu hakkında bilgi alma

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_pool_info_get(
    NX_PACKET_POOL *pool_ptr,
    ULONG *total_packets,
    ULONG *free_packets,
    ULONG *empty_pool_requests,
    ULONG *empty_pool_suspensions,
    ULONG *invalid_packet_releases);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen paket havuzu hakkında bilgi alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **pool_ptr** Daha önce oluşturulan paket havuzuna yönelik işaretçi.
- **total_packets** Havuzdaki toplam paket sayısı için hedef işaretçisi.
- **free_packets** Şu anda boş olan paketlerin toplam sayısı için hedef işaretçisi.
- **empty_pool_requests** Havuz boş olduğunda toplam ayırma isteği sayısının hedefi işaretçisi.
- **empty_pool_suspensions** Boş havuz getirilmesi toplam sayısının hedefi işaretçisi.
- **invalid_packet_releases** Toplam geçersiz paket sürümü sayısının hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket havuzu bilgileri alma.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve packet pool information. */
status = nx_packet_pool_info_get(&pool_0,
    &total_packets,
    &free_packets,
    &empty_pool_requests,
    &empty_pool_suspensions,
    &invalid_packet_releases);

/* If status is NX_SUCCESS, packet pool information was
    retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete
- nx_packet_release, nx_packet_transmit_release

## <a name="nx_packet_release"></a>nx_packet_release

Önceden ayrılmış paketi serbest bırak

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen pakete zincirleme ek paketler de dahil olmak üzere bir paket yayınlar. Paket ayırma üzerinde başka bir iş parçacığı engellenirse, paket verilir ve sürdürülür.

*Uygulamanın, bir paketin birden çok kez serbest bırakılmasını önlemesi gerekir, çünkü bunu yapmak öngörülemeyen sonuçlara neden olur.*

### <a name="parameters"></a>Parametreler

- **packet_ptr** Paket işaretçisi.


### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı paket sürümü.
- **NX_PTR_ERROR** (0x07) geçersiz paket işaretçisi.
- **NX_UNDERFLOW** (0x02) Prepend işaretçisi yük başlangıcından daha küçüktür.
- **NX_OVERFLOW** (0x03) ekleme işaretçisi yük ucundan daha büyük.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs (uygulama ağ sürücüleri)

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```C
/* Release a previously allocated packet. */
status = nx_packet_release(packet_ptr);

/* If status is NX_SUCCESS, the packet has been returned to the
    packet pool it was allocated from. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_transmit_release

## <a name="nx_packet_transmit_release"></a>nx_packet_transmit_release

İletilen bir paketi serbest bırakma

### <a name="prototype"></a>Prototype

```C
UINT nx_packet_transmit_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, TCP olmayan paketler için, belirtilen pakete zincirleme ek paketler de dahil olmak üzere, iletilen bir paket yayınlar. Paket ayırma üzerinde başka bir iş parçacığı engellenirse, paket verilir ve sürdürülür. İletilen bir TCP paketi için paket aktarılmakta olarak işaretlenir ancak paket onaylanana kadar serbest bırakılmaz. Bu hizmet genellikle bir paket iletildikten sonra uygulamanın ağ sürücüsünden çağrılır.

*Ağ sürücüsünün fiziksel medya üstbilgisini kaldırması ve bu hizmeti çağırmadan önce paketin uzunluğunu ayarlaması gerekir.*

### <a name="parameters"></a>Parametreler

- **packet_ptr** Paket işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı iletme paketi sürümü.
- **NX_PTR_ERROR** (0x07) geçersiz paket işaretçisi.
- **NX_UNDERFLOW** (0x02) Prepend işaretçisi yük başlangıcından daha küçüktür.
- **NX_OVERFLOW** (0x03) ekleme işaretçisi yük ucundan daha büyük.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, uygulama ağ sürücüleri (ISRS dahil)

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```C
/* Release a previously allocated packet that was just transmitted
    from the application network driver. */
status = nx_packet_transmit_release(packet_ptr);

/* If status is NX_SUCCESS, the transmitted packet has been
    returned to the packet pool it was allocated from. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release

## <a name="nx_rarp_disable"></a>nx_rarp_disable

Ters adres çözümleme protokolünü devre dışı bırak (RARP)

### <a name="prototype"></a>Prototype

```C
UINT nx_rarp_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirli IP örneği için NetX 'in RARP bileşenini devre dışı bırakır. Bu hizmet, çok ana bir sistem için tüm arabirimlerde RARP 'yi devre dışı bırakır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı RARP devre dışı.
- **NX_NOT_ENABLED** (0x14) RARP etkin değildi.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Disable RARP on the previously created IP instance. */
status = nx_rarp_disable(&ip_0);

/* If status is NX_SUCCESS, RARP is disabled. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_rarp_enable, nx_rarp_info_get

## <a name="nx_rarp_enable"></a>nx_rarp_enable

Ters adres çözümleme protokolünü etkinleştir (RARP)

### <a name="prototype"></a>Prototype

```C
UINT nx_rarp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirli IP örneği için NetX 'in RARP bileşenini sunar. RARP bileşenleri, sıfır IP adresi için tüm bağlı ağ arabirimlerini arar. Sıfır IP adresi, arabirimin henüz IP adresi ataması olmadığını gösterir. RARP, bu arabirimde RARP işlemini etkinleştirerek IP adresini çözümlemeye çalışır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı RARP etkinleştirmesi.
- **NX_IP_ADDRESS_ERROR** (0x21) IP adresi zaten geçerli.
- **NX_ALREADY_ENABLED** (0x15) RARP zaten etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable RARP on the previously created IP instance. */
status = nx_rarp_enable(&ip_0);

/* If status is NX_SUCCESS, RARP is enabled and is attempting to
    resolve this IP instance’s address by querying the network. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_rarp_disable, nx_rarp_info_get

## <a name="nx_rarp_info_get"></a>nx_rarp_info_get

RARP etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype

```C
UINT nx_rarp_info_get(
    NX_IP *ip_ptr,
    ULONG *rarp_requests_sent,
    ULONG *rarp_responses_received,
    ULONG *rarp_invalid_messages);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için RARP etkinlikleriyle ilgili bilgileri alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **rarp_requests_sent** Gönderilen toplam RARP isteği sayısı için hedef işaretçisi.
- **rarp_responses_received** Alınan toplam RARP yanıtı sayısı için hedef işaretçisi.
- **rarp_invalid_messages** Toplam geçersiz ileti sayısının hedefi işaretçisi.


### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı bir RARP bilgileri alma.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve RARP information from previously created IP
    Instance 0. */
status = nx_rarp_info_get(&ip_0,
    &rarp_requests_sent,
    &rarp_responses_received,
    &rarp_invalid_messages);

/* If status is NX_SUCCESS, RARP information was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_rarp_disable, nx_rarp_enable

## <a name="nx_system_initialize"></a>nx_system_initialize

NetX sistemini Başlat

### <a name="prototype"></a>Prototype

```C
VOID nx_system_initialize(VOID);
```

### <a name="description"></a>Açıklama

Bu hizmet, kullanıma hazırlık aşamasında temel NetX sistem kaynaklarını başlatır. Başlatma sırasında ve diğer bir NetX çağrısının yapılabilmesi için uygulama tarafından çağrılmalıdır.

### <a name="parameters"></a>Parametreler

Hiçbiri

### <a name="return-values"></a>Dönüş Değerleri

Yok

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Initialize NetX for operation. */
nx_system_initialize();

/* At this point, NetX is ready for IP creation and all subsequent
    network operations. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check

## <a name="nx_tcp_client_socket_bind"></a>nx_tcp_client_socket_bind

İstemci TCP yuvasını TCP bağlantı noktasına bağlama

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_client_socket_bind(
    NX_TCP_SOCKET *socket_ptr,
    UINT port, ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulan TCP istemci yuvasını belirtilen TCP bağlantı noktasına bağlar. Geçerli TCP Yuvaları 0 ile 0xFFFF arasındadır. Belirtilen TCP bağlantı noktası kullanılamıyorsa, hizmet sağlanan bekleme seçeneğine göre askıya alınır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.
- **bağlantı noktası** Bağlanacak bağlantı noktası numarası (1 ile 0xFFFF arasında). Bağlantı noktası numarası NX_ANY_PORT (0x0000) ise, IP örneği bir sonraki boş bağlantı noktasını arar ve bu bağlantıyı bağlama için kullanır.
- **wait_option** Bağlantı noktası zaten başka bir yuvaya bağlanmışsa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlaması.
- **NX_ALREADY_BOUND** (0x22) bu yuva zaten başka bir TCP bağlantı noktasına bağlıydı.
- **NX_PORT_UNAVAILABLE** (0x23) bağlantı noktası zaten farklı bir yuvaya bağlıydı.
- **NX_NO_FREE_PORTS** (0x45) boş bağlantı noktası yok.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği *tx_thread_wait_abort* bir çağrı tarafından iptal edildi.
- **NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Bind a previously created client socket to port 12 and wait for 7
    timer ticks for the bind to complete. */
status = nx_tcp_client_socket_bind(&client_socket, 12, 7);

/* If status is NX_SUCCESS, the previously created client_socket is
    bound to port 12 on the associated IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_connect, nx_tcp_client_socket_port_get,
- nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,
- nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_client_socket_connect"></a>nx_tcp_client_socket_connect

İstemci TCP yuvasını bağlama

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_client_socket_connect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG server_ip,
    UINT server_port,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş ve bağlı TCP istemci yuvasını belirtilen sunucunun bağlantı noktasına bağlar. Geçerli TCP sunucusu bağlantı noktaları 0 ile 0xFFFF arasındadır. Bağlantı hemen tamamlanmazsa, hizmet sağlanan bekleme seçeneğine göre askıya alınır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.
- **server_ip** Sunucunun IP adresi.
- **SERVER_PORT** Bağlanılacak sunucu bağlantı noktası numarası (1 ile 0xFFFF arasında).
- **wait_option** Bağlantı kurulurken hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlantısı.
- **NX_NOT_BOUND** (0x24) yuva bağlanmadı.
- **NX_NOT_CLOSED** (0x35) yuva kapalı durumda değil.
- **NX_IN_PROGRESS** (0x37) bekleme belirtilmedi, bağlantı girişimi devam ediyor.
- **NX_INVALID_INTERFACE** (0x4C) geçersiz arabirim sağlandı.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ sunucu IP adresi.
- **NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Initiate a TCP connection from a previously created and bound
    client socket. The connection requested in this example is to
    port 12 on the server with the IP address of 1.2.3.5. This
    service will wait 300 timer ticks for the connection to take
    place before giving up. */
status = nx_tcp_client_socket_connect(&client_socket,
    IP_ADDRESS(1,2,3,5), 12, 300);

/* If status is NX_SUCCESS, the previously created and bound
    client_socket is connected to port 12 on IP 1.2.3.5. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_port_get,
- nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,
- nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_client_socket_port_get"></a>nx_tcp_client_socket_port_get

İstemci TCP yuvasına bağlantı noktası numarasını al

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_client_socket_port_get(
    NX_TCP_SOCKET *socket_ptr,
    UINT *port_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, yuvanın bağlandığı zamanda NX_ANY_PORT belirtildiği durumlarda NetX tarafından ayrılan bağlantı noktasını bulmak için yararlı olan yuva ile ilişkili bağlantı noktası numarasını alır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.
- **port_ptr** Dönüş bağlantı noktası numarası için hedef işaretçisi. Geçerli bağlantı noktası numaraları (1 ile 0xFFFF arasında).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlaması.
- **NX_NOT_BOUND** (0x24) bu yuva bir bağlantı noktasına bağlanmamış.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi veya bağlantı noktası döndürme işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Get the port number of previously created and bound client
    socket. */
status = nx_tcp_client_socket_port_get(&client_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
    socket is bound to. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,
- nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_client_socket_unbind"></a>nx_tcp_client_socket_unbind

TCP bağlantı noktasından TCP istemci yuvasının bağlantısını kaldır

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_client_socket_unbind(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet TCP istemci yuvası ile bir TCP bağlantı noktası arasındaki bağlamayı yayınlar. Başka bir yuvayı aynı bağlantı noktası numarasına bağlamayı bekleyen başka iş parçacıkları varsa, ilk askıya alınan iş parçacığı bu bağlantı noktasına bağlanır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlantısı kesiliyor.
- **NX_NOT_BOUND** (0x24) yuva herhangi bir bağlantı noktasına bağlanmadı.
- **NX_NOT_CLOSED** (0x35) yuvasının bağlantısı kesilmedi.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```C
/* Unbind a previously created and bound client TCP socket. */
status = nx_tcp_client_socket_unbind(&client_socket);

/* If status is NX_SUCCESS, the client socket is no longer
    bound. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_enable, nx_tcp_free_port_find,
- nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_enable"></a>nx_tcp_enable

NetX TCP bileşenini etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, NetX 'in Iletim Denetim Protokolü (TCP) bileşenini sunar. Etkinleştirildikten sonra, uygulama tarafından TCP bağlantıları kurulabilir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı TCP etkin.
- **NX_ALREADY_ENABLED** (0x15) TCP zaten etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable TCP on a previously created IP instance ip_0. */
status = nx_tcp_enable(&ip_0);

/* If status is NX_SUCCESS, TCP is enabled on the IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_free_port_find"></a>nx_tcp_free_port_find

Sonraki kullanılabilir TCP bağlantı noktasını bul

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_free_port_find(
    NX_IP *ip_ptr,
    UINT port, UINT *free_port_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, uygulama tarafından sağlanan bağlantı noktasından başlayarak ücretsiz bir TCP bağlantı noktasını (ilişkisiz) bulmaya çalışır. Arama mantığı, en fazla 0xFFFF bağlantı noktası değerine ulaşmak için arama gerçekleşeceği gibi kaydırılır. Arama başarılı olursa, *free_port_ptr* tarafından işaret edilen değişkende boş bağlantı noktası döndürülür.

*Bu hizmet başka bir iş parçacığından çağrılabilir ve aynı bağlantı noktasına sahip olabilir. Bu yarış durumunu engellemek için, uygulama bu hizmeti ve gerçek istemci yuvasını bir mutex 'in koruması altına yerleştirmek isteyebilir.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **bağlantı noktası** Aramaya başlamak için bağlantı noktası numarası (1 ile 0xFFFF arasında).
- **free_port_ptr** Hedef boş bağlantı noktası dönüş değeri işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı boş bağlantı noktası bul.
- **NX_NO_FREE_PORTS** (0x45) boş bağlantı noktası bulunamadı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_INVALID_PORT** (0x46) belirtilen bağlantı noktası numarası geçersiz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Locate a free TCP port, starting at port 12, on a previously
    created IP instance. */
status = nx_tcp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS, "free_port" contains the next free port
    on the IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_info_get"></a>nx_tcp_info_get

TCP etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_info_get(
    NX_IP *ip_ptr,
    ULONG *tcp_packets_sent,
    ULONG *tcp_bytes_sent,
    ULONG *tcp_packets_received,
    ULONG *tcp_bytes_received,
    ULONG *tcp_invalid_packets,
    ULONG *tcp_receive_packets_dropped,
    ULONG *tcp_checksum_errors,
    ULONG *tcp_connections,
    ULONG *tcp_disconnections,
    ULONG *tcp_connections_dropped,
    ULONG *tcp_retransmit_packets);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için TCP etkinlikleri hakkında bilgi alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **tcp_packets_sent** Gönderilen toplam TCP paketi sayısı için hedef işaretçisi.
- **tcp_bytes_sent** Gönderilen TCP baytlarının toplam sayısı için hedef işaretçisi.
- **tcp_packets_received** Alınan toplam TCP paketi sayısının hedefi işaretçisi.
- **tcp_bytes_received** Alınan TCP baytlarının toplam sayısının hedefi işaretçisi.
- **tcp_invalid_packets** Geçersiz TCP paketlerinin toplam sayısının hedefi işaretçisi.
- **tcp_receive_packets_dropped** Bırakılan TCP alma paketlerinin toplam sayısının hedefi işaretçisi.
- **tcp_checksum_errors** Toplam TCP paketi sayısının sağlama toplamı hataları olan hedefi işaretçisi.
- **tcp_connections** Toplam TCP bağlantısı sayısının hedefi işaretçisi.
- **tcp_disconnections** Toplam TCP bağlantısı sayısının hedefi işaretçisi.
- **tcp_connections_dropped** Bırakılan toplam TCP bağlantısı sayısının hedefi işaretçisi.
- **tcp_retransmit_packets** Yeniden iletilen TCP paketlerinin toplam sayısının hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) TCP bilgilerinin başarıyla alımı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve TCP information from previously created IP Instance ip_0. */
status = nx_tcp_info_get(&ip_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_invalid_packets,
    &tcp_receive_packets_dropped,
    &tcp_checksum_errors,
    &tcp_connections,
    &tcp_disconnections
    &tcp_connections_dropped,
    &tcp_retransmit_packets);

/* If status is NX_SUCCESS, TCP information was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_accept"></a>nx_tcp_server_socket_accept

TCP bağlantısını kabul et

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_server_socket_accept(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce dinlemek üzere ayarlanmış bir bağlantı noktası için TCP istemci yuvası bağlantı isteğini kabul eder (veya kabul edilmeye hazırlanır). Bu hizmet, uygulama dinlemesi veya yeniden dinleme hizmetini çağırırsa ya da istemci bağlantısı gerçekten mevcut olduğunda dinleme geri çağırma yordamından çağrıldıktan sonra çağrılabilir. Bağlantı hemen kurulamazsa, hizmet sağlanan bekleme seçeneğine göre askıya alınır.

*Sunucu yuvasının sunucu bağlantı noktasına bağlamasını kaldırmak için bağlantı artık gerekmiyorsa, uygulamanın **nx_tcp_server_socket_unaccept** çağrısı gerekir.*

*Uygulama geri çağırma yordamları, IP 'nin yardımcı iş parçacığı içinden çağrılır.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** TCP sunucusu yuva denetim bloğu işaretçisi.
- **wait_option** Bağlantı kurulurken hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)


### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı TCP sunucusu yuvası kabulü (pasif bağlantı).
- **NX_NOT_LISTEN_STATE** (0x36) sağlanan sunucu yuvası bir dinleme durumunda değil.
- **NX_IN_PROGRESS** (0x37) bekleme belirtilmedi, bağlantı girişimi devam ediyor.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği *tx_thread_wait_abort* bir çağrı tarafından iptal edildi.
- **NX_PTR_ERROR** (0x07) yuva işaretçisi hatası.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;
void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This
    example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;
    /* Assuming that:
        "port_12_semaphore" has already been created with an
        initial count of 0 "my_ip" has already been created and the
        link is enabled "my_pool" packet pool has already been
        created */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to each client and then disconnecting.*/
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
            request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
            complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye"
                message */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is called
            even if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket
            again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }

    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_listen"></a>nx_tcp_server_socket_listen

TCP bağlantı noktasında istemci bağlantısı dinlemeyi etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_server_socket_listen(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr,
    UINT listen_queue_size,
    VOID (*listen_callback)(NX_TCP_SOCKET *socket_ptr, UINT port));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen TCP bağlantı noktasında istemci bağlantı isteği dinlemeyi mümkün. İstemci bağlantı isteği alındığında, sağlanan sunucu yuvası belirtilen bağlantı noktasına bağlanır ve sağlanan dinleme geri çağırma işlevi çağırılır.

Dinleme geri çağırma yordamının işlenmesi tamamen uygulamaya göre yapılır. Daha sonra kabul etme işlemini gerçekleştiren bir uygulama iş parçacığını uyandırma mantığını içerebilir. Uygulamanın bu yuva için kabul etme sırasında askıya alınmış bir iş parçacığı zaten varsa, dinleme geri çağırma yordamına gerek duyulmayabilir.

Uygulama aynı bağlantı noktasında ek istemci bağlantılarını ele istiyorsa, bir sonraki bağlantı için ***nx_tcp_server_socket_relisten*** kullanılabilir bir yuva (kapalı durumda olan bir yuva) ile çağrılmalıdır. Yeniden dinleme hizmeti çağrılana kadar, ek istemci bağlantıları sıraya alınır. Maksimum sıra derinliği aşıldığında, en eski bağlantı isteği yeni bağlantı isteğini sıraya alma lehine bırakılır. En yüksek sıra derinliği bu hizmet tarafından belirtilir.

*Uygulama geri çağırma yordamları iç IP Yardımcısı iş parçacığından çağırılır.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **bağlantı noktası** Dinlenecek bağlantı noktası numarası (1 ile 0xFFFF arasında).
- **socket_ptr** Bağlantı için kullanılacak yuva işaretçisi.
- **listen_queue_size** Sıraya alınabilen istemci bağlantı isteği sayısı.
- **listen_callback** Bağlantı alındığında çağrılacak uygulama işlevi. NULL belirtilirse, geri arama dinlemesi özelliği devre dışıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı TCP bağlantı noktası dinleme etkinleştirmesi.
- **NX_MAX_LISTEN** (0x33) daha fazla dinleme isteği yapısı yok. Nx_api. h içindeki sabit NX_MAX_LISTEN_REQUESTS, kaç tane etkin dinleme isteğinin mümkün olduğunu tanımlar.
- **NX_NOT_CLOSED** (0x35) sağlanan sunucu yuvası kapalı durumda değil.
- **NX_ALREADY_BOUND** (0x22) sağlanan sunucu yuvası bir bağlantı noktasına zaten bağlıydı.
- **NX_DUPLICATE_LISTEN** (0x34) Bu bağlantı noktası için zaten etkin bir dinleme isteği var.
- **NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası belirtildi.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread.*/
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket.
        This example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an
        initial count of 0 "my_ip" has already been created
        and the link is enabled "my_pool" packet pool has already
        been created.
    */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server
        Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to
        each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
            request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

    /* Wait for 200 ticks for the client socket connection
        to complete. */
    status = nx_tcp_server_socket_accept(&server_socket, 200);

    /* Check for a successful connection. */
    if (status == NX_SUCCESS)
    {
        /* Allocate a packet for the "Hello_and_Goodbye"
            message. */
        nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
            NX_WAIT_FOREVER);

        /* Place "Hello_and_Goodbye" in the packet. */
        nx_packet_data_append(my_packet, "Hello_and_Goodbye",
            sizeof("Hello_and_Goodbye"),
            &my_pool,
            NX_WAIT_FOREVER);

        /* Send "Hello_and_Goodbye" to client. */
        nx_tcp_socket_send(&server_socket, my_packet, 200);

        /* Check for an error. */
        if (status)
        {
            /* Error, release the packet. */
            nx_packet_release(my_packet);
        }
        /* Now disconnect the server socket from the client. */
        nx_tcp_socket_disconnect(&server_socket, 200);
    }

    /* Unaccept the server socket. Note that unaccept is called
        even if disconnect or accept fails. */
    nx_tcp_server_socket_unaccept(&server_socket);

    /* Setup server socket for listening with this socket
    again. */
    nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
}

/* We are now done so unlisten on server port 12. */
nx_tcp_server_socket_unlisten(&my_ip, 12);

/* Delete the server socket. */
nx_tcp_socket_delete(&server_socket);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_relisten"></a>nx_tcp_server_socket_relisten

TCP bağlantı noktasındaki istemci bağlantısını yeniden dinle

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_server_socket_relisten(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce dinlemek üzere ayarlanan bir bağlantı noktasında bir bağlantı alındıktan sonra çağrılır. Bu hizmetin ana amacı, sonraki istemci bağlantısı için yeni bir sunucu yuvası sağlamaktır. Bir bağlantı isteği sıraya alınmışsa, bu hizmet çağrısı sırasında bağlantı hemen işlenir.

*Özgün dinleme isteği tarafından belirtilen geri arama yordamı, bu yeni sunucu yuvası için bir bağlantı olduğunda da çağırılır.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **bağlantı noktası** Yeniden dinlemek için bağlantı noktası numarası (1 ile 0xFFFF arasında).
- **socket_ptr** Sonraki istemci bağlantısı için kullanılacak yuva.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı TCP bağlantı noktası yeniden dinleme.
- **NX_NOT_CLOSED** (0x35) sağlanan sunucu yuvası kapalı durumda değil.
- **NX_ALREADY_BOUND** (0x22) sağlanan sunucu yuvası bir bağlantı noktasına zaten bağlıydı.
- **NX_INVALID_RELISTEN** (0x47) Bu bağlantı noktası için zaten geçerli bir yuva işaretçisi var veya belirtilen bağlantı noktasında bir dinleme isteği etkin değil.
- Sıraya alınmış bir bağlantı isteği olduğundan ve bu çağrı sırasında işlendiği için, NX_SUCCESS ile aynı **NX_CONNECTION_PENDING** (0x48).
- **NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası belirtildi.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya dinleme geri çağırma işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread.*/
    tx_semaphore_put(&port_12_semaphore);
    }

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This
    example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
    "port_12_semaphore" has already been created with an initial
        count of 0.
        "my_ip" has already been created and the link is enabled.
        "my_pool" packet pool has already been created. */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL,
        port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);
    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to each client then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
        request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
        complete. */
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye"
            message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is
        called even if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket
        again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_unaccept"></a>nx_tcp_server_socket_unaccept

Yuva ilişkilendirmesini dinleme bağlantı noktasıyla kaldır

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_server_socket_unaccept(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bu sunucu yuvası ile belirtilen sunucu bağlantı noktası arasındaki ilişkiyi kaldırır. Uygulamanın, bir bağlantının kesilmesi veya bir başarısız kabul çağrısından sonra bu hizmeti çağırması gerekir.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce kurulum sunucusu yuva örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı sunucu yuvası kabul iptali.
- **NX_NOT_LISTEN_STATE** (0x36) sunucu yuvası yanlış bir durumda ve muhtemelen kesilmemelidir.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This example
    doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an initial count
        of 0 "my_ip" has already been created and the link is enabled
        "my_pool" packet pool has already been created
        */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,NX_NULL,
        port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye"
        to each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection request
            is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
            complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye" message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet,
                "Hello_and_Goodbye",sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is called even
            if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind, nx_tcp_enable,
- nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_unlisten"></a>nx_tcp_server_socket_unlisten

TCP bağlantı noktasındaki istemci bağlantısını dinlemeyi devre dışı bırak

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_server_socket_unlisten(NX_IP *ip_ptr, UINT port);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen TCP bağlantı noktasındaki istemci bağlantı isteğini dinlemeyi devre dışı bırakır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **bağlantı noktası** Dinlemeyi devre dışı bırakılacak bağlantı noktası sayısı (0 ile 0xFFFF arasında).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı TCP dinlemesi devre dışı.
- **NX_ENTRY_NOT_FOUND** (0x16) dinleme, belirtilen bağlantı noktası için etkinleştirilmemiş.
- **NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası belirtildi.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This example
    doesn't use this callback.*/
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an initial count
        of 0 "my_ip" has already been created and the link is enabled
        "my_pool" packet pool has already been created
    */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye" to
        each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection request is
            present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye" message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"), &my_pool,
                NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }
            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }
        /* Unaccept the server socket. Note that unaccept is called even if
        disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_bytes_available"></a>nx_tcp_socket_bytes_available

Alma için kullanılabilir bayt sayısını alır

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_bytes_available(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen TCP yuvasında alınabilmeleri için kullanılabilen bayt sayısını alır. TCP yuvasının zaten bağlı olması gerektiğini unutmayın.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Önceden oluşturulmuş ve bağlı TCP yuvasına yönelik işaretçi.
- **bytes_available** Kullanılabilir baytlar için hedef işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) hizmeti başarıyla çalıştırılır. Okuma için kullanılabilir bayt sayısı çağırana döndürülür.
- **NX_NOT_CONNECTED** (0x38) yuva bağlı durumda değil.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçiler.
- **NX_NOT_ENABLED** (0x14) TCP etkin değil.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Get the bytes available for retrieval on the specified socket. */
status = nx_tcp_socket_bytes_available(&my_socket,
    &bytes_available);

/* Is status = NX_SUCCESS, the available bytes is returned in
    bytes_available. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_create"></a>nx_tcp_socket_create

TCP istemcisi veya sunucu yuvası oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_create(
    NX_IP *ip_ptr, 
    NX_TCP_SOCKET *socket_ptr,
    CHAR *name, ULONG type_of_service, 
    ULONG fragment,
    UINT time_to_live, 
    ULONG window_size,
    VOID (*urgent_data_callback)(NX_TCP_SOCKET *socket_ptr),
    VOID (*disconnect_callback)(NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için bir TCP istemcisi veya sunucu yuvası oluşturur.

*Uygulama geri çağırma yordamları, bu IP örneğiyle ilişkili iş parçacığından çağırılır.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **socket_ptr** Yeni TCP yuvası denetim bloğu işaretçisi.
- **ad** Bu TCP yuvasının uygulama adı.
- **Type_of_service** İletim için hizmet türünü tanımlar, yasal değerler aşağıdaki gibidir:

- NX_IP_NORMAL (0x00000000)
- NX_IP_MIN_DELAY (0x00100000)
- NX_IP_MAX_DATA (0x00080000)
- NX_IP_MAX_RELIABLE (0x00040000)
- NX_IP_MIN_COST (0x00020000)

- **parça**  IP fragmenting izin verilip verilmeyeceğini belirtir. NX_FRAGMENT_OKAY (0x0) belirtilmişse, IP fragmenting izin verilir. NX_DONT_FRAGMENT (0x4000) belirtilirse, IP fragmenting devre dışı bırakılır.
- **Time_to_live** Bu paketin oluşturulmadan önce kaç yönlendirici geçebileceğini tanımlayan 8 bitlik değeri belirtir. Varsayılan değer NX_IP_TIME_TO_LIVE tarafından belirtilir.
- **window_size** Bu yuva için alma sırasında izin verilen en fazla bayt sayısını tanımlar
- **urgent_data_callback** Alma akışında acil verilerin her ne zaman algılandığına çağrılan uygulama işlevi. Bu değer NX_NULL, acil veriler yok sayılır.
- **disconnect_callback** Bağlantının diğer ucundaki yuva tarafından her bir bağlantı kesilmesi verildiğinde çağrılan uygulama işlevi. Bu değer NX_NULL ise, bağlantıyı kes geri çağırma işlevi devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı TCP istemci yuvası oluşturma.
- **NX_OPTION_ERROR** (0X0a) geçersiz hizmet türü, parça, geçersiz pencere boyutu veya zaman tolive seçeneği.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve Iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Create a TCP client socket on the previously created IP instance,
    with normal delivery, IP fragmentation enabled, 0x80 time to
    live, a 200-byte receive window, no urgent callback routine, and
    the "client_disconnect" routine to handle disconnection initiated
    from the other end of the connection. */
status = nx_tcp_socket_create(&ip_0, &client_socket,
    "Client Socket",
    NX_IP_NORMAL, NX_FRAGMENT_OKAY,
    0x80, 200, NX_NULL
    client_disconnect);

/* If status is NX_SUCCESS, the client socket is created and ready
    to be bound. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_delete"></a>nx_tcp_socket_delete

TCP yuvasını Sil

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_delete(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir TCP yuvasını siler. Yuva hala bağlı veya bağlı ise, hizmet bir hata kodu döndürür.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Önceden oluşturulmuş TCP yuvası

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva silme.
- **NX_NOT_CREATED** (0x27) yuva oluşturulmadı.
- **NX_STILL_BOUND** (0x42) yuva hala bağımlı.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Delete a previously created TCP client socket. */
status = nx_tcp_socket_delete(&client_socket);

/* If status is NX_SUCCESS, the client socket is deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_disconnect"></a>nx_tcp_socket_disconnect

İstemci ve sunucu yuvası bağlantılarının bağlantısını kes

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_disconnect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, kurulan bir istemci veya sunucu yuvası bağlantısını keser. Sunucu yuvasının bağlantısının kesilmesi, geri kabul edilmemiş bir istek gelmelidir, ancak bağlantısı kesilen bir istemci yuvası, başka bir bağlantı isteği için bir durumda bırakılır. Bağlantıyı kesme işlemi hemen tamamlanmazsa, hizmet sağlanan bekleme seçeneğine göre askıya alınır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı olan istemci veya sunucu yuvası örneği işaretçisi.
- **wait_option** Bağlantının kesilmesi devam ederken hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlantısı kesilemedi.
- **NX_NOT_CONNECTED** (0x38) belirtilen yuva bağlı değil.
- **NX_IN_PROGRESS** (0x37) bağlantı kesilmesi devam ediyor, hiçbir bekleme belirtilmedi.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```C
/* Disconnect from a previously established connection and wait a
    maximum of 400 timer ticks. */
status = nx_tcp_socket_disconnect(&client_socket, 400);

/* If status is NX_SUCCESS, the previously connected socket (either
    as a result of the client socket connect or the server accept) is
    disconnected. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_info_get,
- nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,
- nx_tcp_socket_send, nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_disconnect_complete_notify"></a>nx_tcp_socket_disconnect_complete_notify

TCP bağlantı kesmeyi yüklemeyi bildirme geri çağırma işlevi

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_disconnect_complete_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_disconnect_complete_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet, bir yuva bağlantı kesme işlemi tamamlandıktan sonra çağrılan bir geri arama işlevini kaydeder. NetX seçeneği ile derlenip, TCP yuvası bağlantı kesme tamam geri çağırma işlevi kullanılabilir

- ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** tanımlandı.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı olan istemci veya sunucu yuvası örneği işaretçisi.
- **tcp_disconnect_complete_notify** Yüklenecek geri çağırma işlevi.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) geri çağırma işlevi başarıyla kaydedildi.
- **NX_NOT_SUPPORTED** (0x4b) genişletilmiş bildirim özelliği NETX kitaplığında yerleşik değildir
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Install the disconnect complete notify callback function. */
status = nx_tcp_socket_disconnect_complete_notify(&client_socket,
    callback);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create, nx_tcp_socket_establish_notify,
- nx_tcp_socket_mss_get, nx_tcp_socket_mss_peer_get,
- nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_establish_notify"></a>nx_tcp_socket_establish_notify

TCP kurma bildirimi geri aramasını ayarla işlevi

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_establish_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_establish_notify)(NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet, bir TCP yuvası bağlantı yaptığında çağrılan bir geri arama işlevini kaydeder. NetX, ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** tanımlı seçeneği ile DERLENIP, TCP yuvası oluşturma geri çağırma işlevi kullanılabilir.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı olan istemci veya sunucu yuvası örneği işaretçisi.
- **tcp_establish_notify** Bir TCP bağlantısı kurulduktan sonra geri çağırma işlevi başlatıldı.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00), bildirim işlevini başarıyla ayarlıyor.
- **NX_NOT_SUPPORTED** (0x4b) genişletilmiş bildirim özelliği NETX kitaplığında yerleşik değildir
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) TCP, uygulama tarafından etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Set the function pointer "callback" as the notify function NetX
will call when the connection is in the established state. */
status = nx_tcp_socket_establish_notify(&client_socket, callback);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,
- nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_info_get"></a>nx_tcp_socket_info_get

TCP yuva etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *tcp_packets_sent,
    ULONG *tcp_bytes_sent,
    ULONG *tcp_packets_received,
    ULONG *tcp_bytes_received,
    ULONG *tcp_retransmit_packets,
    ULONG *tcp_packets_queued,
    ULONG *tcp_checksum_errors,
    ULONG *tcp_socket_state,
    ULONG *tcp_transmit_queue_depth,
    ULONG *tcp_transmit_window,
    ULONG *tcp_receive_window);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen TCP yuvası örneği için TCP yuva etkinlikleri hakkında bilgi alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.
- **tcp_packets_sent** Yuvada Gönderilen TCP paketlerinin toplam sayısı için hedef işaretçisi.
- **tcp_bytes_sent** Yuvada Gönderilen TCP baytlarının toplam sayısı için hedef işaretçisi.
- **tcp_packets_received** Yuvada alınan toplam TCP paketi sayısının hedefi işaretçisi.
- **tcp_bytes_received** Yuvada alınan TCP baytlarının toplam sayısının hedefi işaretçisi.
- **tcp_retransmit_packets** Toplam TCP paketi yeniden aktarımlar sayısının hedefi işaretçisi.
- **tcp_packets_queued** Yuvada sıraya alınan TCP paketlerinin toplam sayısının hedefi işaretçisi.
- **tcp_checksum_errors** Yuvada sağlama toplamı hataları olan toplam TCP paketi sayısının hedefi işaretçisi.
- **tcp_socket_state** Yuvanın geçerli durumunun hedefi işaretçisi.
- **tcp_transmit_queue_depth** Toplam iletim paketi sayısının hedefe yönelik işaretçisi, hala ACK için bekleyen sıraya alındı.
- **tcp_transmit_window** Geçerli iletme penceresi boyutunun hedefi işaretçisi.
- **tcp_receive_window** Geçerli alma penceresi boyutunun hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) TCP yuvası bilgilerinin alımı başarılı oldu.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="return-values"></a>Dönüş Değerleri

```C
/* Retrieve TCP socket information from previously created socket_0.*/
status = nx_tcp_socket_info_get(&socket_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_retransmit_packets,
    &tcp_packets_queued,
    &tcp_checksum_errors,
    &tcp_socket_state,
    &tcp_transmit_queue_depth,
    &tcp_transmit_window,
    &tcp_receive_window);

/* If status is NX_SUCCESS, TCP socket information was retrieved. */
```

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve TCP socket information from previously created socket_0.*/
status = nx_tcp_socket_info_get(&socket_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_retransmit_packets,
    &tcp_packets_queued,
    &tcp_checksum_errors,
    &tcp_socket_state,
    &tcp_transmit_queue_depth,
    &tcp_transmit_window,
    &tcp_receive_window);

/* If status is NX_SUCCESS, TCP socket information was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,
- nx_tcp_socket_send, nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_mss_get"></a>nx_tcp_socket_mss_get

Yuvanın düzeyini al

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_mss_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen yuvanın yerel en büyük kesim boyutunu (Bu) alır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulmuş yuvanın işaretçisi.
-  , ' İ döndürmek için hedef.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı bir wget al.
- **NX_PTR_ERROR** (0x07) geçersiz yuva veya kaynak hedefi işaretçisi.
- **NX_NOT_ENABLED** (0x14) TCP etkin değil.
- **NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Get the MSS for the socket "my_socket". */
status = nx_tcp_socket_mss_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
    socket's current MSS value. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_peer_get,
- nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_mss_peer_get"></a>nx_tcp_socket_mss_peer_get

Eş TCP yuvasının düzeyini alın

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_mss_peer_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a>Açıklama

Bu hizmet, Eş yuva tarafından tanıtılan en büyük kesim boyutunu (,) alır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulmuş ve bağlı yuva işaretçisi.
-  , ' İ döndürmek için hedef.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı eş ve Get.
- **NX_PTR_ERROR** (0x07) geçersiz yuva veya kaynak hedefi işaretçisi.
- **NX_NOT_ENABLED** (0x14) TCP etkin değil.
- **NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Get the MSS of the connected peer to the socket "my_socket". */
status = nx_tcp_socket_mss_peer_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
    socket peer’s advertised MSS value. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_mss_set"></a>nx_tcp_socket_mss_set

Yuvanın düzeyini ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_mss_set(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG mss);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen yuvanın en büyük kesim boyutunu (Bu) ayarlar. Bu değer, IP ve TCP üstbilgileri için odaya izin veren ağ arabirimi IP MTU 'SU içinde olmalıdır.

Bu hizmet, TCP yuvası bağlantı işlemini başlatılmadan önce kullanılmalıdır. Hizmet bir TCP bağlantısı kurulduktan sonra kullanılıyorsa, yeni değerin bağlantı üzerinde hiçbir etkisi olmaz.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulmuş yuvanın işaretçisi.
-  , Ayarlanacak bir sahip değeri.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı bir Wonu kümesi.
- **NX_SIZE_ERROR** (0x09) belirtilen '% ' değeri çok büyük.
- **NX_NOT_CONNECTED** (0x38) TCP bağlantısı kurulmadı
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_NOT_ENABLED** (0x14) TCP etkin değil.
- **NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Set the MSS of the socket "my_socket" to 1000 bytes. */
status = nx_tcp_socket_mss_set(&my_socket, 1000);

/* If status is NX_SUCCESS, the MSS of "my_socket" is 1000 bytes. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_peer_info_get,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_peer_info_get"></a>nx_tcp_socket_peer_info_get

Eş TCP soketi hakkında bilgi alın

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_peer_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *peer_ip_address, 
    ULONG *peer_port);
```

### <a name="description"></a>Açıklama

Bu hizmet, bağlı TCP yuvasının IP ağı üzerinden eş IP adresini ve bağlantı noktası bilgilerini alır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuvasına yönelik işaretçi.
- **peer_ip_address** Konak bayt düzeninde eş IP adresi hedefi işaretçisi.
- **peer_port** Ana bilgisayar bayt düzeninde eş bağlantı noktası numarası için hedef işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) hizmeti başarıyla çalıştırılır. Eş IP adresi ve bağlantı noktası numarası çağırana döndürülür.
- **NX_NOT_CONNECTED** (0x38) yuva bağlı durumda değil.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçiler.
- **NX_NOT_ENABLED** (0x14) TCP etkin değil.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Obtain peer IP address and port on the specified TCP socket. */
status = nx_tcp_socket_peer_info_get(&my_socket, &peer_ip_address,
    &peer_port);

/* If status = NX_SUCCESS, the data was successfully obtained. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_receive"></a>nx_tcp_socket_receive

TCP yuvasından veri al

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_receive(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen yuvadan TCP verileri alır. Belirtilen yuvada hiçbir veri sıraya alınmaz, çağıran, sağlanan bekleme seçeneğine göre askıya alır.

*NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.
- **packet_ptr** TCP paket işaretçisine yönelik işaretçi.
- **wait_option** Şu anda bu yuvada sıraya alınmış veri yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı yuva verileri alma.
- **NX_NOT_BOUND** (0x24) yuva henüz bağlanmamış.
- **NX_NO_PACKET** (0x01) veri alınmadı.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_NOT_CONNECTED** (0x38) yuva artık bağlı değil.
- **NX_PTR_ERROR** (0x07) geçersiz yuva veya dönüş paketi işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

/* Önceden oluşturulmuş ve bağlı TCP istemci yuvasından bir paket alın. Kullanılabilir bir paket yoksa, vermeden önce 200 Zamanlayıcı onay işareti bekleyin. */Status = nx_tcp_socket_receive (&client_socket, &packet_ptr, 200);

/* Durum NX_SUCCESS ise, alınan paket "packet_ptr" tarafından işaret edilir. */

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive_queue_max_set,
- nx_tcp_socket_send, nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_receive_notify"></a>nx_tcp_socket_receive_notify

Alınan paketlerin uygulamasına bildirme


### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_receive_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_receive_notify) (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet, bildirim al işlev işaretçisini uygulama tarafından belirtilen geri çağırma işleviyle yapılandırır. Bu geri çağırma işlevi, daha sonra yuvada bir veya daha fazla paket alındığında çağrılır. NX_NULL bir işaretçi sağlanırsa, bildir işlevi devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** TCP yuvasına yönelik işaretçi.
- **tcp_receive_notify** Yuvada bir veya daha fazla paket alındığında çağrılan uygulama geri çağırma işlev işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva alma bildirimi.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Setup a receive packet callback function for the "client_socket"
socket. */
status = nx_tcp_socket_receive_notify(&client_socket,
    my_receive_notify);

/* If status is NX_SUCCESS, NetX will call the function named
    "my_receive_notify" whenever one or more packets are received for
    "client_socket". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_send"></a>nx_tcp_socket_send

TCP yuvası üzerinden veri gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_send(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, TCP verilerini daha önce bağlı bir TCP yuvası üzerinden gönderir. Alıcının en son tanıtılan pencere boyutu bu istekten azsa, hizmet isteğe bağlı olarak, belirtilen bekleme seçeneğine göre askıya alınır. Bu hizmet, IP katmanına, \ ' dan daha büyük bir paket verisi gönderilmesini güvence altına alır.

*Bir hata döndürülmediği takdirde, uygulama bu çağrıdan sonra paketi serbest bırakmamalıdır. Bunu yapmak öngörülemeyen sonuçlara neden olur çünkü ağ sürücüsü iletim sonrasında paketi serbest bırakmaya da çalışacaktır.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı TCP yuvası örneğine yönelik işaretçi.
- **packet_ptr** TCP veri paketi işaretçisi.
- **wait_option** İstek alıcının pencere boyutundan fazlaysa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva gönderme.
- **NX_NOT_BOUND** (0x24) yuva herhangi bir bağlantı noktasına bağlanmadı.
- **NX_NO_INTERFACE_ADDRESS** (0x50) uygun giden arabirim bulunamadı.
- **NX_NOT_CONNECTED** (0x38) yuva artık bağlı değil.
- **NX_WINDOW_OVERFLOW** (0x39) isteği, alıcının tanıtılan pencere boyutundan bayt cinsinden daha büyük.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_INVALID_PACKET** (0x12) paketi ayrılmadı.
- **NX_TX_QUEUE_DEPTH** (0x49) en yüksek iletim sırası derinliğine ulaşıldı.
- **NX_OVERFLOW** (0x03) paket ekleme işaretçisi geçersiz.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_UNDERFLOW** (0x02) paket önüne işaretçisi geçersiz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Send a packet out on the previously created and connected TCP
    socket. If the receive window on the other side of the connection
    is less than the packet size, wait 200 timer ticks before giving up. */
status = nx_tcp_socket_send(&client_socket, packet_ptr, 200);

/* If status is NX_SUCCESS, the packet has been sent! */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_state_wait

### <a name="nx_tcp_socket_state_wait"></a>nx_tcp_socket_state_wait

TCP yuvasının belirli bir durumu girmesini bekleyin

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_state_wait(
    NX_TCP_SOCKET *socket_ptr,
    UINT desired_state, 
    ULONG wait_option);
```
### <a name="description"></a>Açıklama

Bu hizmet, yuvanın istenen durumu girmesini bekler. Yuva istenen durumda değilse, hizmet sağlanan bekleme seçeneğine göre askıya alınır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı TCP yuvası örneğine yönelik işaretçi.
- **desired_state** İstenen TCP durumu. Geçerli TCP yuvası durumları şu şekilde tanımlanır:
- NX_TCP_CLOSED (0x01)
- NX_TCP_LISTEN_STATE (0x02)
- NX_TCP_SYN_SENT (0x03)
- NX_TCP_SYN_RECEIVED (0x04)
- NX_TCP_ESTABLISHED (0x05)
- NX_TCP_CLOSE_WAIT (0x06)
- NX_TCP_FIN_WAIT_1 (0x07)
- NX_TCP_FIN_WAIT_2 (0x08)
- NX_TCP_CLOSING (0x09)
- NX_TCP_TIMED_WAIT (0x0A)
- NX_TCP_LAST_ACK (0x0B)
- **wait_option** İstenen durum yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı durum bekleme.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_NOT_SUCCESSFUL** (0x43) belirtilen bekleme süresi içinde mevcut değil.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_OPTION_ERROR** (0x0A) istenen yuva durumu geçersiz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Wait 300 timer ticks for the previously created socket to enter
    the established state in the TCP state machine. */
status = nx_tcp_socket_state_wait(&client_socket,
    NX_TCP_ESTABLISHED, 300);

/* If status is NX_SUCCESS, the socket is now in the established
    state! */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send

## <a name="nx_tcp_socket_timed_wait_callback"></a>nx_tcp_socket_timed_wait_callback

Zamanlanmış bekleme durumu için geri çağırma 'yi yükler

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_timed_wait_callback(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_timed_wait_callback) (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet, TCP yuvası zamanlanmış bekleme durumunda olduğunda çağrılan bir geri arama işlevini kaydeder. Bu hizmeti kullanmak için, NetX kitaplığı tanımlı ***NX_ENABLE_EXTENDED_NOTIFY*** seçeneği ile oluşturulmalıdır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı olan istemci veya sunucu yuvası örneği işaretçisi.
- **tcp_timed_wait_callback** Zamanlanmış geri çağırma işlevi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) geri çağırma Işlevi yuvasını başarıyla kaydeder
- **NX_NOT_SUPPORTED** (0x4b) NETX kitaplığı, genişletilmiş bildirim özelliği etkin olmadan oluşturulmuştur.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Install the timed wait callback function */
nx_tcp_socket_timed_wait_callback(&client_socket, callback);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_transmit_configure"></a>nx_tcp_socket_transmit_configure

Yuvanın iletim parametrelerini Yapılandır

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_transmit_configure(
    NX_TCP_SOCKET *socket_ptr,
    ULONG max_queue_depth,
    ULONG timeout,
    ULONG max_retries,
    ULONG timeout_shift);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen TCP yuvasının çeşitli iletim parametrelerini yapılandırır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** TCP yuvasına yönelik işaretçi.
- **max_queue_depth** İletim için sıraya izin verilen en fazla paket sayısı.
- **zaman aşımı** Paket yeniden gönderilmeden önce bir ACK değeri için ThreadX Zamanlayıcı onay işareti sayısı bekleniyor.
- **max_retries** İzin verilen en fazla yeniden deneme sayısı.
- **timeout_shift** Sonraki yeniden denemelerde zaman aşımını kaydırmak için değer. 0 değeri, sonraki yeniden denemeler arasındaki aynı zaman aşımı ile sonuçlanır. 1 değeri, yeniden denemeler arasındaki zaman aşımını iki katına çıkarır.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) başarılı iletme yuvası yapılandırması.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_OPTION_ERROR** (0x0A) sıra derinliği seçeneği geçersiz.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Configure the "client_socket" for a maximum transmit queue depth
    of 12, 100 tick timeouts, a maximum of 20 retries, and a timeout
    double on each successive retry. */
status = nx_tcp_socket_transmit_configure(&client_socket,
    12,100,20, 1);

/* If status is NX_SUCCESS, the socket’s transmit retry has been
    configured. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,
- nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_window_update_notify_set"></a>nx_tcp_socket_window_update_notify_set

Pencere boyutu güncelleştirmelerinin uygulamasını bilgilendir

### <a name="prototype"></a>Prototype

```C
UINT nx_tcp_socket_window_update_notify_set(
    NX_TCP_SOCKET
    *socket_ptr,
    VOID (*tcp_window_update_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet, bir yuva penceresi güncelleştirme geri arama yordamını yüklüyor. Bu yordam, belirtilen yuva uzak konağın pencere boyutunda bir artışı gösteren bir paket aldığında otomatik olarak çağrılır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuvasına yönelik işaretçi.
- **tcp_window_update_notify** Pencere boyutu değiştiğinde çağrılacak geri arama yordamı. NULL değeri, pencere değişikliğini güncelleştirmeyi devre dışı bırakır.

### <a name="return-values"></a>Dönüş Değerleri
- **NX_SUCCESS** (0x00) geri çağırma yordamı yuvaya yüklendi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçiler.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.


### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Set the function pointer to the windows update callback after creating the
socket. */
status = nx_tcp_socket_window_update_notify_set(&data_socket,
    my_windows_update_callback);

/* Define the window callback function in the host application. */
void my_windows_update_callback(NX_TCP_SCOCKET *data_socket)
{
    /* Process update on increase TCP transmit socket window size. */
    return;
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,
- nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure

## <a name="nx_udp_enable"></a>nx_udp_enable

NetX 'in UDP bileşenini etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, NetX 'in Kullanıcı Datagram Protokolü (UDP) bileşenini sunar. Etkinleştirildikten sonra, uygulama tarafından UDP veri birimleri gönderilebilir ve alınabilir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarıyla UDP etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_ALREADY_ENABLED** (0x15) Bu bileşen zaten etkinleştirilmiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable UDP on the previously created IP instance. */
status = nx_udp_enable(&ip_0);

/* If status is NX_SUCCESS, UDP is now enabled on the specified IP
    instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_free_port_find, nx_udp_info_get, nx_udp_packet_info_extract,
- nx_udp_socket_bind, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_free_port_find"></a>nx_udp_free_port_find

Sonraki kullanılabilir UDP bağlantı noktasını bul

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_free_port_find(
    NX_IP *ip_ptr, 
    UINT port,
    UINT *free_port_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, uygulama tarafından sağlanan bağlantı noktası numarasından başlayarak ücretsiz bir UDP bağlantı noktası (ilişkisiz) arar. Arama mantığı, en fazla 0xFFFF bağlantı noktası değerine ulaşırsa, arama mantığı sarmalacaktır. Arama başarılı olursa, *free_port_ptr* tarafından işaret edilen değişkende boş bağlantı noktası döndürülür.

*Bu hizmet başka bir iş parçacığından çağrılabilir ve aynı bağlantı noktasına geri dönüş yapılabilir. Bu yarış durumunu engellemek için, uygulama bu hizmeti ve gerçek yuva bağlamasını bir mutex 'in altına yerleştirmek isteyebilir.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **bağlantı noktası** Aramaya başlamak için bağlantı noktası numarası (1 ile 0xFFFF arasında).
- **free_port_ptr** Hedef boş bağlantı noktası dönüş değişkenine yönelik işaretçi.


### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı boş bağlantı noktası bul.
- **NX_NO_FREE_PORTS** (0x45) boş bağlantı noktası bulunamadı.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.
- **NX_INVALID_PORT** (0x46) belirtilen bağlantı noktası numarası geçersiz.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Locate a free UDP port, starting at port 12, on a previously
    created IP instance. */
status = nx_udp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS pointer, "free_port" identifies the next
    free UDP port on the IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_info_get, nx_udp_packet_info_extract,
- nx_udp_socket_bind, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_info_get"></a>nx_udp_info_get

UDP etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_info_get(
    NX_IP *ip_ptr,
    ULONG *udp_packets_sent,
    ULONG *udp_bytes_sent,
    ULONG *udp_packets_received,
    ULONG *udp_bytes_received,
    ULONG *udp_invalid_packets,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için UDP etkinlikleriyle ilgili bilgileri alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **udp_packets_sent** Gönderilen toplam UDP paketi sayısı için hedef işaretçisi.
- **udp_bytes_sent** Gönderilen toplam UDP bayt sayısı için hedef işaretçisi.
- **udp_packets_received** Alınan toplam UDP paketi sayısının hedefi işaretçisi.
- **udp_bytes_received** Alınan UDP baytlarının toplam sayısının hedefi işaretçisi.
- **udp_invalid_packets** Toplam geçersiz UDP paketi sayısının hedefi işaretçisi.
- **udp_receive_packets_dropped** Bırakılan UDP alma paketlerinin toplam sayısının hedefi işaretçisi.
- **udp_checksum_errors** Toplam UDP paketi sayısının sağlama toplamı hataları olan hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı UDP bilgisi alma.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.


### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve UDP information from previously created IP Instance ip_0. */
status = nx_udp_info_get(&ip_0, &udp_packets_sent,
    &udp_bytes_sent,
    &udp_packets_received,
    &udp_bytes_received,
    &udp_invalid_packets,
    &udp_receive_packets_dropped,
    &udp_checksum_errors);

/* If status is NX_SUCCESS, UDP information was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_packet_info_extract,
- nx_udp_socket_bind, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_packet_info_extract"></a>nx_udp_packet_info_extract

UDP paketindeki ağ parametrelerini Ayıkla

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_packet_info_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address,
    UINT *protocol,
    UINT *port,
    UINT *interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, IP adresi, eş bağlantı noktası numarası, protokol türü (Bu hizmet her zaman UDP türünü döndürür) gibi ağ parametrelerini, gelen bir arabirimde alınan bir paketten ayıklar.

### <a name="parameters"></a>Parametreler

- **packet_ptr** Paket işaretçisi.
- **ip_address** Gönderenin IP adresi işaretçisi.
- **protokol** Protokol işaretçisi (UDP).
- **bağlantı noktası** Gönderenin bağlantı noktası numarası işaretçisi.
- **interface_index** Arabirim dizini alma işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) paket arabirimi verileri başarıyla ayıklandı.
- **NX_INVALID_PACKET** (0x12) PAKETI, IP çerçevesi içermiyor.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Extract network data from UDP packet interface.*/
status = nx_udp_packet_info_extract( packet_ptr, &ip_address,
    &protocol, &port,
    &interface_index);

/* If status is NX_SUCCESS packet data was successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_socket_bind, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_bind"></a>nx_udp_socket_bind

UDP yuvasını UDP bağlantı noktasına bağla

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_bind(
    NX_UDP_SOCKET *socket_ptr, 
    UINT port,
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulan UDP yuvasını belirtilen UDP bağlantı noktasına bağlar. Geçerli UDP yuvaları 0 ile 0xFFFF arasındadır. İstenen bağlantı noktası numarası başka bir yuvaya bağlıysa, bu hizmet, yuvanın bağlantı noktası numarasından bağlantısını kesmek için belirtilen süre boyunca bekler.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.
- **bağlantı noktası** Bağlanacak bağlantı noktası numarası (1 ile 0xFFFF arasında). Bağlantı noktası numarası NX_ANY_PORT (0x0000) ise, IP örneği bir sonraki boş bağlantı noktasını arar ve bu bağlantıyı bağlama için kullanır.
- **wait_option** Bağlantı noktası zaten başka bir yuvaya bağlanmışsa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlaması.
- **NX_ALREADY_BOUND** (0x22) bu yuva zaten başka bir bağlantı noktasına bağlıydı.
- **NX_PORT_UNAVAILABLE** (0x23) bağlantı noktası zaten farklı bir yuvaya bağlıydı.
- **NX_NO_FREE_PORTS** (0x45) boş bağlantı noktası yok.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası belirtildi.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Bind the previously created UDP socket to port 12 on the
    previously created IP instance. If the port is already bound,
    wait for 300 timer ticks before giving up. */
status = nx_udp_socket_bind(&udp_socket, 12, 300);

/* If status is NX_SUCCESS, the UDP socket is now bound to
    port 12.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_bytes_available"></a>nx_udp_socket_bytes_available

Alma için kullanılabilir bayt sayısını alır

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_bytes_available(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen UDP yuvasında alım için kullanılabilen bayt sayısını alır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuvasına yönelik işaretçi.
- **bytes_available** Kullanılabilir baytlar için hedef işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı bayt kullanılabilir alma.
- **NX_NOT_SUCCESSFUL** (0x43) yuva bir bağlantı noktasına bağlanmadı.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçiler.
- **NX_NOT_ENABLED** (0x14) UDP özelliği etkin değil.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Get the bytes available for retrieval from the UDP socket. */
status = nx_udp_socket_bytes_available(&my_socket, &bytes_available);

/* If status == NX_SUCCESS, the number of bytes was successfully
    retrieved.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_checksum_disable"></a>nx_udp_socket_checksum_disable

UDP yuvası için sağlama toplamını devre dışı bırak

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_checksum_disable(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen UDP yuvasında paketleri göndermek ve almak için sağlama toplamı mantığını devre dışı bırakır. Sağlama toplamı mantığı devre dışı bırakıldığında, bu yuva aracılığıyla gönderilen tüm paketler için UDP üstbilgisinin sağlama toplamı alanına sıfır değeri yüklenir. UDP üst bilgisindeki sıfır değerli sağlama toplamı değeri, bu paket için sağlama toplamı hesaplanmayan alıcıyı işaret eder.

Ayrıca, sırasıyla UDP paketlerini alırken ve gönderirken, bu, ***NX_DISABLE_UDP_RX_CHECKSUM** _ ve _ *_NX_DISABLE_UDP_TX_CHECKSUM_** tanımlı bir etkiye sahip olmadığına de unutmayın.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva sağlama toplamı devre dışı.
- **NX_NOT_BOUND** (0x24) yuva bağlanmadı.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, süreölçer

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Disable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_disable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will not have a checksum
    calculated. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_checksum_enable"></a>nx_udp_socket_checksum_enable

UDP yuvası için sağlama toplamını etkinleştir

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_checksum_enable(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen UDP yuvasında paket göndermek ve almak için sağlama toplamı mantığını sunar. Sağlama toplamı, tüm UDP veri alanının yanı sıra sözde IP üst bilgisini de içerir.

Ayrıca, **NX_DISABLE_UDP_RX_CHECKSUM** ve **NX_DISABLE_UDP_TX_CHECKSUM** , sırasıyla UDP paketlerini alırken ve gönderirken tanımlanmış bir etkiye sahip olmadığını unutmayın.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva sağlama toplamı etkin.
- **NX_NOT_BOUND** (0x24) yuva bağlanmadı.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, süreölçer

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Enable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_enable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will have a checksum
    calculated. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_create"></a>nx_udp_socket_create

UDP yuvası oluşturun.

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_create(
    NX_IP *ip_ptr,
    NX_UDP_SOCKET *socket_ptr, CHAR *name,
    ULONG type_of_service, ULONG fragment,
    UINT time_to_live, ULONG queue_maximum);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneği için bir UDP yuvası oluşturur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **socket_ptr** Yeni UDP yuva denetimi Bloc işaretçisi.
- **ad** Bu UDP yuvasının uygulama adı.
- **Type_of_service** İletim için hizmet türünü tanımlar, yasal değerler aşağıdaki gibidir:
    - NX_IP_NORMAL (0x00000000)
    - NX_IP_MIN_DELAY (0x00100000)
    - NX_IP_MAX_DATA (0x00080000)
    - NX_IP_MAX_RELIABLE (0x00040000)
    - NX_IP_MIN_COST (0x00020000)
- **parça** IP fragmenting izin verilip verilmeyeceğini belirtir. NX_FRAGMENT_OKAY (0x0) belirtilmişse, IP fragmenting izin verilir. NX_DONT_FRAGMENT (0x4000) belirtilirse, IP fragmenting devre dışı bırakılır.
- **Time_to_live** Bu paketin oluşturulmadan önce kaç yönlendirici geçebileceğini tanımlayan 8 bitlik değeri belirtir. Varsayılan değer NX_IP_TIME_TO_LIVE tarafından belirtilir.
- **queue_maximum** Bu yuva için sıraya alınabilen en fazla UDP veri birimi sayısını tanımlar. Kuyruk sınırına ulaşıldığında, alınan her yeni paket için en eski UDP paketi yayımlanır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı UDP yuvası oluşturma.
- **NX_OPTION_ERROR** (0X0a) geçersiz hizmet türü, parça veya yaşam süresi seçeneği.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma ve Iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Create a UDP socket with a maximum receive queue of 30 packets.*/
status = nx_udp_socket_create(&ip_0, &udp_socket, "Sample UDP Socket",
    NX_IP_NORMAL, NX_FRAGMENT_OKAY, 0x80, 30);

/* If status is NX_SUCCESS, the new UDP socket has been created and
    is ready for binding. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_delete,
- nx_udp_socket_info_get, nx_udp_socket_port_get,
- nx_udp_socket_receive, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_delete"></a>nx_udp_socket_delete

UDP yuvasını Sil

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_delete(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir UDP yuvasını siler. Yuva bir bağlantı noktasına bağlıysa, önce yuvanın bağlantısı kaldırılmalıdır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva silme.
- **NX_STILL_BOUND** (0x42) yuva hala bağımlı.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Delete a previously created UDP socket. */
status = nx_udp_socket_delete(&udp_socket);

/* If status is NX_SUCCESS, the previously created UDP socket has
    been deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_info_get, nx_udp_socket_port_get,
- nx_udp_socket_receive, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_info_get"></a>nx_udp_socket_info_get

UDP yuva etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_info_get(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *udp_packets_sent,
    ULONG *udp_bytes_sent,
    ULONG *udp_packets_received,
    ULONG *udp_bytes_received,
    ULONG *udp_packets_queued,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen UDP yuva örneği için UDP yuva etkinlikleri hakkında bilgi alır.

*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** Önceden oluşturulmuş UDP yuva örneğine yönelik işaretçi.
- **udp_packets_sent** Yuvada gönderilen toplam UDP paketi sayısı için hedef işaretçisi.
- **udp_bytes_sent** Yuvada gönderilen UDP baytlarının toplam sayısı için hedef işaretçisi.
- **udp_packets_received** Yuvada alınan UDP paketlerinin toplam sayısının hedefi işaretçisi.
- **udp_bytes_received** Yuvada alınan UDP baytlarının toplam sayısının hedefi işaretçisi.
- **udp_packets_queued** Yuva üzerindeki toplam sıraya alınmış UDP paketi sayısının hedefi işaretçisi.
- **udp_receive_packets_dropped** Sıra boyutunun aşılması nedeniyle yuva için bırakılan toplam UDP alma paketi sayısının hedefi işaretçisi.
- **udp_checksum_errors** Yuvada sağlama toplamı hataları olan toplam UDP paketi sayısının hedefi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı UDP yuvası bilgileri alma.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları ve zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Retrieve UDP socket information from socket 0.*/
status = nx_udp_socket_info_get(&socket_0,
    &udp_packets_sent,
    &udp_bytes_sent,
    &udp_packets_received,
    &udp_bytes_received,
    &udp_queued_packets,
    &udp_receive_packets_dropped,
    &udp_checksum_errors);

/* If status is NX_SUCCESS, UDP socket information was retrieved.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_port_get,
- nx_udp_socket_receive, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_port_get"></a>nx_udp_socket_port_get

UDP yuvasına göre bağlantı noktası numarasını seçin

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_port_get(NX_UDP_SOCKET *socket_ptr, UINT *port_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, yuvanın bağlandığı zamanda NX_ANY_PORT belirtildiği durumlarda NetX tarafından ayrılan bağlantı noktasını bulmak için yararlı olan yuva ile ilişkili bağlantı noktası numarasını alır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.
- **port_ptr** Dönüş bağlantı noktası numarası için hedef işaretçisi. Geçerli bağlantı noktası numaraları (1-0xFFFF).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlaması.
- **NX_NOT_BOUND** (0x24) bu yuva bir bağlantı noktasına bağlanmamış.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi veya bağlantı noktası döndürme işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Get the port number of created and bound UDP socket. */
status = nx_udp_socket_port_get(&udp_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
    socket is bound to. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_receive, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_receive"></a>nx_udp_socket_receive

UDP yuvasından veri birimi al

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_receive(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen yuvadan bir UDP veri birimi alır. Belirtilen yuvada hiçbir veri birimi sıraya alınmaz, çağıran, sağlanan bekleme seçeneğine göre askıya alır.

*NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.
- **packet_ptr** UDP veri birimi paket işaretçisine yönelik işaretçi.
- **wait_option** Bir veri birimi şu anda bu yuvada sıraya alınmışsa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Receive a packet from a previously created and bound UDP socket.
    If no packets are currently available, wait for 500 timer ticks
    before giving up. */
status = nx_udp_socket_receive(&udp_socket, &packet_ptr, 500);

/* If status is NX_SUCCESS, the received UDP packet is pointed to by
    packet_ptr. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_receive_notify"></a>nx_udp_socket_receive_notify

Alınan her paketin uygulamasını bilgilendir

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_receive_notify(
    NX_UDP_SOCKET *socket_ptr,
    VOID (*udp_receive_notify)
    (NX_UDP_SOCKET *socket_ptr));
```

### <a name="description"></a>Açıklama

Bu hizmet, bildirim al işlev işaretçisini uygulama tarafından belirtilen geri çağırma işlevine ayarlar. Bu geri çağırma işlevi, yuva üzerinde her paket alındığında çağrılır. NX_NULL bir işaretçi sağlanırsa, alma bildirme işlevi devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** UDP yuvasının işaretçisi.
- **udp_receive_notify** Yuvada bir paket alındığında çağrılan uygulama geri çağırma işlev işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Setup a receive packet callback function for the "udp_socket"
socket. */
status = nx_udp_socket_receive_notify(&udp_socket,
    my_receive_notify);

/* If status is NX_SUCCESS, NetX will call the function named
    "my_receive_notify" whenever a packet is received for
    "udp_socket". */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_send"></a>nx_udp_socket_send

UDP veri birimi gönder

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş ve bağlantılı bir UDP yuvası aracılığıyla bir UDP datagramı gönderir. NetX, hedef IP adresini temel alarak kaynak adresi olarak uygun bir yerel IP adresi bulur. Belirli bir arabirim ve kaynak IP adresi belirtmek için, uygulamanın **nx_udp_socket_interface_send** hizmetini kullanması gerekir.

Bu hizmetin UDP veri biriminin başarıyla gönderilip gönderilmediğini ne olursa olsun, hemen geri dönmediğine unutmayın.

Yuva yerel bir bağlantı noktasına bağlanmalıdır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Önceden oluşturulan UDP yuva örneği işaretçisi
- **packet_ptr** UDP veri birimi paket işaretçisi
- **ip_address** Hedef IP adresi
- **bağlantı noktası** Ana bilgisayar bayt düzeninde geçerli hedef bağlantı noktası numarası 1 ile 0xFFFF arasında)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı UDP yuvası gönderme
- **NX_NOT_BOUND** (0x24) yuva herhangi bir bağlantı noktasına bağlanmadı
- **NX_NO_INTERFACE_ADDRESS** (0x50) uygun bir giden arabirim bulunamıyor.
- **NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ sunucu IP adresi
- **NX_UNDERFLOW** (0x02) paketteki UDP üst bilgisi için yeterli yer yok
- **NX_OVERFLOW** (0x03) paket ekleme işaretçisi geçersiz
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı
- **NX_NOT_ENABLED** (0x14) UDP etkin değil
- **NX_INVALID_PORT** (0x46) bağlantı noktası numarası geçerli bir Aralık içinde değil

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
ULONG server_address;

/* Set the UDP Client IP address. */
server_address = IP_ADDRESS(1,2,3,5);

/* Send a packet to the UDP server at server_address on port 12. */
status = nx_udp_socket_send(&client_socket, packet_ptr,
    server_address, 12);

/* If status == NX_SUCCESS, the application successfully transmitted
    the packet out the UDP socket to its peer. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_interface_send"></a>nx_udp_socket_interface_send

UDP yuvası üzerinden veri birimi gönderin.

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_interface_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port,
    UINT address_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, kaynak adresi olarak belirtilen IP adresine sahip ağ arabirimi aracılığıyla daha önce oluşturulmuş ve bağlantılı bir UDP yuvası aracılığıyla bir UDP datagramı gönderir. UDP veri biriminin başarıyla gönderilip gönderilmediğini ne olursa olsun hizmetin hemen geri döndüğünü unutmayın.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Paketin üzerine iletilmesi için yuva.
- **packet_ptr** İletilecek paket işaretçisi.
- **ip_address** Paketin gönderileceği hedef IP adresi.
- **bağlantı noktası** Hedef bağlantı noktası.
- **address_index** Paketin gönderileceği arabirimle ilişkili adresin dizini.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) paketi başarıyla gönderildi.
- **NX_NOT_BOUND** (0x24) yuva bir bağlantı noktasına bağlanmadı.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_NOT_ENABLED** (0x14) UDP işleme etkin değil.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi.
- **NX_OVERFLOW** (0x03) geçersiz paket ekleme işaretçisi.
- **NX_UNDERFLOW** (0x02) geçersiz paket önüne işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_INVALID_INTERFACE** (0x4C) geçersiz adres dizini.
- **NX_INVALID_PORT** (0x46) bağlantı noktası numarası en fazla bağlantı noktası numarasını aşıyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
#define ADDRESS_INDEX 1

/* Send packet out on port 80 to the specified destination IP on the
interface at index 1 in the IP task interface list. */
status = nx_udp_packet_interface_send(socket_ptr, packet_ptr,
    destination_ip, 80,
    ADDRESS_INDEX);

/* If status is NX_SUCCESS packet was successfully transmitted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_unbind

## <a name="nx_udp_socket_unbind"></a>nx_udp_socket_unbind

UDP bağlantı noktasından UDP yuvasının bağlantısını kaldır.

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_socket_unbind(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, UDP yuvası ile UDP bağlantı noktası arasındaki bağlamayı yayınlar. Alma sırasında depolanan tüm alınan paketler, ciltten çıkarma işleminin bir parçası olarak serbest bırakılır.

İlişkisiz bağlantı noktasına başka bir yuva bağlamayı bekleyen başka iş parçacıkları varsa, ilk askıya alınan iş parçacığı daha sonra yeni ilişkisiz bağlantı noktasına bağlanır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlantısı kesiliyor.
- **NX_NOT_BOUND** (0x24) yuva herhangi bir bağlantı noktasına bağlanmadı.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

Yes

### <a name="example"></a>Örnek

```C
/* Unbind the previously bound UDP socket. */
status = nx_udp_socket_unbind(&udp_socket);

/* If status is NX_SUCCESS, the previously bound socket is now
    unbound. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_source_extract

## <a name="nx_udp_source_extract"></a>nx_udp_source_extract

UDP veri kaynağından IP ve gönderme bağlantı noktasını Ayıkla

### <a name="prototype"></a>Prototype

```C
UINT nx_udp_source_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address, UINT *port);
```

### <a name="description"></a>Açıklama

Bu hizmet, gönderenin IP ve bağlantı noktası numarasını, sağlanan UDP veri biriminin IP ve UDP üst bilgilerinden ayıklar.

### <a name="parameters"></a>Parametreler

- **packet_ptr** UDP veri birimi paket işaretçisi.
- **ip_address** Dönüş IP adresi değişkenine yönelik geçerli işaretçi.
- **bağlantı noktası** Dönüş bağlantı noktası değişkenine geçerli işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı kaynak IP/bağlantı noktası ayıklama.
- **NX_INVALID_PACKET** (0x12) sağlanan paket geçersiz.
- **NX_PTR_ERROR** (0x07) geçersiz paket veya IP veya bağlantı noktası hedefi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ıSR

### <a name="preemption-possible"></a>Önalım mümkün

Hayır

### <a name="example"></a>Örnek

```C
/* Extract the IP and port information from the sender of the UPD
    packet. */
status = nx_udp_source_extract(packet_ptr, &sender_ip_address,
    &sender_port);

/* If status is NX_SUCCESS, the sender IP and port information has
    been stored in sender_ip_address and sender_port respectively.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind