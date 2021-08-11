---
title: Bölüm 4-Azure RTOS NetX Duo hizmetlerinin açıklaması
description: Bu bölümde, tüm Azure RTOS NetX Duo Hizmetleri alfabetik sırada bir açıklama bulunur.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d28ca64a6a655bb3f1ad10c563450a0e65b645a1e1a2a464c4137f9a999815bc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785031"
---
# <a name="chapter-4---description-of-azure-rtos-netx-duo-services"></a>Bölüm 4-Azure RTOS NetX Duo hizmetlerinin açıklaması

Bu bölümde, tüm Azure RTOS NetX Duo Hizmetleri alfabetik sırada bir açıklama bulunur. Hizmet adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır. Örneğin, bu bölümün başlangıcında tüm ARP hizmetleri bulunur. 

NetX Duo 'da IPv6 tabanlı protokolleri ve işlemleri desteklemek için sunulan çok sayıda yeni hizmet vardır. NET Duo 'daki IPv6 özellikli hizmetler, ***NXD**, *, IPv4 ve IPv6 ikili yığın işlemi için tasarlandıklarından emin olabilir.

NetX 'teki mevcut hizmetler NetX Duo içinde tam olarak desteklenmektedir. NetX uygulamaları, en az taşıma çabasıyla NetX Duo 'e geçirilebilir.

> [!NOTE]
> *Yüksek performanslı NetX Duo API 'sinin avantajlarından faydalanmayan eski uygulama kodu için BSD-Compatible soket API 'si kullanılabilir olduğunu unutmayın. BSD-Compatible yuva API 'SI hakkında daha fazla bilgi için ek D 'ye bakın*.

Her açıklamanın "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan NX_DISABLE_ERROR_CHECKING seçeneğinden etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır. "Izin verilen" bölümler, her bir NetX Duo hizmetinin çağrılabilecek olduğunu gösterir.

## <a name="nx_arp_dynamic_entries_invalidate"></a>nx_arp_dynamic_entries_invalidate   
ARP önbelleğindeki tüm dinamik girdileri geçersiz kıl

### <a name="prototype"></a>Prototype     

```c
UINT nx_arp_dynamic_entries_invalidate(NX_IP *ip_ptr);
```

### <a name="description"></a>Description   
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
No

### <a name="example"></a>Örnek

```c
/* Invalidate all dynamic entries in the ARP cache. */
status = nx_arp_dynamic_entries_invalidate(&ip_0);

/* If status is NX_SUCCESS the dynamic ARP entries were
   successfully invalidated. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_dynamic_entry_set"></a>nx_arp_dynamic_entry_set  
Dinamik ARP girdisi ayarla

### <a name="prototype"></a>Prototype  

```c
UINT nx_arp_dynamic_entry_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);  
```

### <a name="description"></a>Description    
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
No

### <a name="example"></a>Örnek

```c
/* Setup a dynamic ARP entry on the previously created IP
   Instance 0. */
status = nx_arp_dynamic_entry_set(&ip_0, IP_ADDRESS(1,2,3,4),
                                  0x1022, 0x1234);

/* If status is NX_SUCCESS, there is now a dynamic mapping between
   the IP address of 1.2.3.4 and the physical hardware address of
   10:22:00:00:12:34. */
```
### <a name="see-also"></a>Ayrıca Bkz. 

- nx_arp_dynamic_entries_invalidate
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_enable"></a>nx_arp_enable  
Adres Çözümleme protokolünü (ARP) etkinleştir

### <a name="prototype"></a>Prototype    

```c
UINT nx_arp_enable(
    NX_IP *ip_ptr, 
    VOID *arp_cache_memory,
    ULONG arp_cache_size);
```

### <a name="description"></a>Description

Bu hizmet, belirli IP örneği için NetX Duo ARP bileşenini başlatır. ARP başlatma, ARP iletilerinin gönderilmesi ve alınması için gereken ARP önbelleğini ve çeşitli ARP işleme yordamlarını ayarlamayı içerir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **arp_cache_memory** ARP önbelleğinin yerleştirileceği bellek alanı işaretçisi.
- **arp_cache_size** Her ARP girişi 52 bayttır, ARP girişlerinin toplam sayısı, bu nedenle boyut 52 ' ye bölünür.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP veya önbellek bellek işaretçisi.
- **NX_SIZE_ERROR** (0x09) Kullanıcı tarafından sağlanan ARP önbelleği belleği çok küçük.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_ALREADY_ENABLED** (0x15) Bu bileşen zaten etkinleştirilmiştir.

### <a name="allowed-from"></a>İzin Verilen   
Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası  
No

### <a name="example"></a>Örnek

```c
/* Enable ARP and supply 1024 bytes of ARP cache memory for
   previously created IP Instance ip_0. */
status = nx_arp_enable(&ip_0, (void *) pointer, 1024);

/* If status is NX_SUCCESS, ARP was successfully enabled for this IP
instance.*/
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_entry_delete"></a>nx_arp_entry_delete   
ARP girişini silme

### <a name="prototype"></a>Prototype  

```c
UINT nx_arp_entry_delete(
    NX_IP *ip_ptr, 
    ULONG ip_address);
```
### <a name="description"></a>Description

Bu hizmet, verilen IP adresi için bir ARP girişini IP iç ARP tablosundan kaldırır.

### <a name="parameters"></a>Parametreler  

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **ip_address** Belirtilen IP adresine sahip ARP girişi silinmelidir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı ARP etkinleştirmesi.
- **NX_ENTRY_NOT_FOUND** (0x16) Belirtilen IP adresine sahip giriş bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz IP veya önbellek bellek işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_IP_ADDRESS_ERROR** (0x21) Belirtilen IP adresi geçersiz.

### <a name="allowed-from"></a>İzin Verilen  
Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası  
No

### <a name="example"></a>Örnek

```c
/* Delete the ARP entry with the IP address 1.2.3.4. */
status = nx_arp_entry_delete(&ip_0, IP_ADDRESS(1, 2, 3, 4));

/* If status is NX_SUCCESS, ARP entry with the specified IP address
   is deleted.*/
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_gratuitous_send"></a>nx_arp_gratuitous_send   
İsteksiz ARP isteği gönderme

### <a name="prototype"></a>Prototype  

```c
UINT nx_arp_gratuitous_send(
    NX_IP *ip_ptr,
    VOID (*response_handler)(NX_IP *ip_ptr, NX_PACKET *packet_ptr));
```                               
### <a name="description"></a>Description

Bu hizmet, arabirim IP adresi geçerli olduğu sürece gratuitous ARP isteklerini iletmek için tüm fiziksel arabirimleri geçen bir hizmettir. Daha sonra bir ARP yanıtı alındıktan sonra, yanıt gratuitous ARP'ye yanıt işlemesi için sağlanan yanıt işleyicisi çağrılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **response_handler** Yanıt işleme işlevinin işaretçisi. Bu NX_NULL yanıt yoksayılır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı gratuitous ARP send.
- **NX_NO_PACKET** (0x01) Paket yok.
- **NX_NOT_ENABLED** (0x14) ARP etkin değil.
- **NX_IP_ADDRESS_ERROR** (0x21) Geçerli IP adresi geçersiz.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Çağıran bir iş parçacığı değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```
/* Send gratuitous ARP without any response handler. */
status = nx_arp_gratuitous_send(&ip_0, NX_NULL);

/* If status is NX_SUCCESS the gratuitous ARP was successfully
   sent. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_hardware_address_find"></a>nx_arp_hardware_address_find
Ip adresi verilen fiziksel donanım adresini bulma

### <a name="prototype"></a>Prototype  

```c
UINT nx_arp_hardware_address_find(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG *physical_msw,
    ULONG *physical_lsw);
```
### <a name="description"></a>Description

Bu hizmet, ARP önbelleğinde sağlanan IP adresiyle ilişkili bir fiziksel donanım adresi bulmaya çalışır.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **ip_address** Aranan IP adresi.
- **physical_msw** Fiziksel adresin ilk 16 biti (47-32) döndüren değişken işaretçisi.
- **physical_lsw** Fiziksel adresin alt 32 biti (31-0) döndüren değişken işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı ARP donanım adresi bulma.
- **NX_ENTRY_NOT_FOUND** (0x16) Eşlemesi ARP önbelleğinde bulunamadı.
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz IP adresi.
- **NX_PTR_ERROR** (0x07) Geçersiz IP veya bellek işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Search for the hardware address associated with the IP address of
   1.2.3.4 in the ARP cache of the previously created IP
   Instance 0. */
status = nx_arp_hardware_address_find(&ip_0, IP_ADDRESS(1,2,3,4),
                                      &physical_msw,
                                      &physical_lsw);

/* If status is NX_SUCCESS, the variables physical_msw and
   physical_lsw contain the hardware address.*/
```   
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_info_get"></a>nx_arp_info_get
ARP etkinlikleri hakkında bilgi alma

### <a name="prototype"></a>Prototype  

```c
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

### <a name="description"></a>Description

Bu hizmet, ilişkili IP örneği için ARP etkinlikleriyle ilgili bilgileri almaktadır.

> [!NOTE]
> *Bir hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülz.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **arp_requests_sent** Bu IP örneğinden gönderilen toplam ARP isteklerinin hedefine işaretçi.
- **arp_requests_received** Ağdan alınan toplam ARP isteklerinin hedefine işaretçi.
- **arp_responses_sent** Bu IP örneğinden gönderilen toplam ARP yanıtları için hedefin işaretçisi.
- **arp_responses_received** Ağdan alınan toplam ARP yanıtları için hedefin işaretçisi.
- **arp_dynamic_entries** Geçerli sayıda dinamik ARP girdisi için hedefin işaretçisi.
- **arp_static_entries** Geçerli statik ARP girdisi sayısı için hedefin işaretçisi.
- **arp_aged_entries** Eski olan ve geçersiz olan toplam ARP girdisi sayısının hedefine işaretçi.
- **arp_invalid_messages** Alınan toplam geçersiz ARP iletilerinin hedefine işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı ARP bilgileri alma.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Pickup ARP information for ip_0. */
status = nx_arp_info_get(&ip_0, &arp_requests_sent,
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

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_ip_address_find"></a>nx_arp_ip_address_find
Fiziksel adres verilen IP adresini bulma

### <a name="prototype"></a>Prototype  

```c
UINT nx_arp_ip_address_find(
    NX_IP *ip_ptr, 
    ULONG *ip_address,
    ULONG physical_msw, 
    ULONG physical_lsw);
```
### <a name="description"></a>Description

Bu hizmet, ARP önbelleğinde sağlanan fiziksel adresle ilişkili bir IP adresi bulmaya çalışır.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **ip_address** Eşlenmiş bir IP adresi bulunursa, dönüş IP adresi işaretçisi.
- **physical_msw** Aranan fiziksel adresin ilk 16 biti (47-32).
- **physical_lsw** Aranecek fiziksel adresin daha düşük 32 biti (31-0).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı ARP IP adresi bulma 
- **NX_ENTRY_NOT_FOUND** (0x16) Eşlemesi ARP önbelleğinde bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz IP veya bellek işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.
- **NX_INVALID_PARAMETERS** (0x4D) Physical_msw physical_lsw 0'dır.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Search for the IP address associated with the hardware address of
   0x0:0x01234 in the ARP cache of the previously created IP
   Instance ip_0. */
status = nx_arp_ip_address_find(&ip_0, &ip_address, 0x0, 0x1234);

/* If status is NX_SUCCESS, the variables ip_address contains the
   associated IP address. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_static_entries_delete"></a>nx_arp_static_entries_delete
Tüm statik ARP girdilerini Sil

### <a name="prototype"></a>Prototype  

```c
UINT nx_arp_static_entries_delete(NX_IP *ip_ptr);
```

### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Delete all the static ARP entries for IP Instance 0, assuming
   "ip_0" is the NX_IP structure for IP Instance 0. */
status = nx_arp_static_entries_delete(&ip_0);

/* If status is NX_SUCCESS all static ARP entries in the ARP cache
   have been deleted. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_static_entry_create"></a>nx_arp_static_entry_create
ARP önbelleğinde donanım eşlemeye statik IP oluşturma

### <a name="prototype"></a>Prototype  

```c
UINT nx_arp_static_entry_create(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Create a static ARP entry on the previously created IP
   Instance 0. */
status = nx_arp_static_entry_create(&ip_0, IP_ADDRESS(1,2,3,4),
                                    0x0, 0x1234);

/* If status is NX_SUCCESS, there is now a static mapping between
   the IP address of 1.2.3.4 and the physical hardware address of
   0x00:0x1234. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_static_entry_delete"></a>nx_arp_static_entry_delete 
ARP önbelleğindeki statik IP 'yi donanım eşleştirmeye silme

### <a name="prototype"></a>Prototype  

```c
UINT nx_arp_static_entry_delete(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için ARP önbelleğinde önceden oluşturulmuş bir statik IP-fiziksel adres eşlemeyi bulur ve siler.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **ip_address** Statik olarak eşlenmiş IP adresi.
- **physical_msw** Statik olarak eşlenmiş fiziksel adresin ilk 16 bit (47-* * 32).
- **physical_lsw** Statik olarak eşlenmiş fiziksel adresin düşük 32 bitleri (31-* * 0).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı ARP statik girdisi silme.
- **NX_ENTRY_NOT_FOUND** (0x16) ARP ÖNBELLEĞINDE statik ARP girdisi bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz IP adresi.
- **NX_INVALID_PARAMETERS** (0x4D) Physical_msw physical_lsw 0'dır.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Delete a static ARP entry on the previously created IP
   instance ip_0. */
status = nx_arp_static_entry_delete(&ip_0, IP_ADDRESS(1,2,3,4),
                                    0x0, 0x1234);

/* If status is NX_SUCCESS, the previously created static ARP entry
   was successfully deleted. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_icmp_enable"></a>nx_icmp_enable
İnternet Denetim İletisi Protokolünü (ICMP) Etkinleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nx_icmp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için ICMP bileşenini sağlar. ICMP bileşeni, İnternet hata iletilerini ve ping isteklerini ve yanıtlarını işlemeden sorumludur. 

> [!IMPORTANT]  
> *Bu hizmet yalnızca IPv4 hizmeti için ICMP'ye olanak sağlar. Uygulamalar hem ICMPv4 hem de ICMPv6'yı etkinleştirmek için nxd_icmp_enable kullandır.*

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı ICMP etkinleştirmesi.
- **NX_ALREADY_ENABLED** (0x15) ICMP zaten etkin.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Enable ICMP on the previously created IP Instance ip_0. */
status = nx_icmp_enable(&ip_0);

/* If status is NX_SUCCESS, ICMP is enabled. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nx_icmp_info_get"></a>nx_icmp_info_get
ICMP etkinlikleri hakkında bilgi alma

### <a name="prototype"></a>Prototype  

```c
UINT nx_icmp_info_get(
    NX_IP *ip_ptr,
    ULONG *pings_sent,
    ULONG *ping_timeouts,
    ULONG *ping_threads_suspended,
    ULONG *ping_responses_received,
    ULONG *icmp_checksum_errors,
    ULONG *icmp_unhandled_messages);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için ICMP etkinlikleri hakkında bilgi almaktadır.

> [!NOTE]  
> *Bir hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülz.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **pings_sent** Gönderilen toplam ping sayısı için hedefin işaretçisi.
- **ping_timeouts** Toplam ping zaman aşımı sayısı için hedefin işaretçisi.
- **ping_threads_suspended** Ping istekleri üzerinde askıya alınan toplam iş parçacığı sayısının hedefine işaretçi.
- **ping_responses_received** Alınan toplam ping yanıtı sayısının hedefine işaret ediyor.
- **icmp_checksum_errors** Toplam ICMP sağlama toplamı hatalarının hedef işaretçisi.
- **icmp_unhandled_messages** Toplam işlanmamış ICMP iletilerinin hedef işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) BAŞARıLı ICMP bilgileri alma.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Retrieve ICMP information from previously created IP
   instance ip_0. */
status = nx_icmp_info_get(&ip_0, &pings_sent, &ping_timeouts,
                          &ping_threads_suspended,
                          &ping_responses_received,
                          &icmp_checksum_errors,
                          &icmp_unhandled_messages);
/* If status is NX_SUCCESS, ICMP information was retrieved. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_icmp_enable
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nx_icmp_ping"></a>nx_icmp_ping  
Belirtilen IP adresine ping isteği gönderme

### <a name="prototype"></a>Prototype  

```c
UINT nx_icmp_ping(
    NX_IP *ip_ptr,
    ULONG ip_address,
    CHAR *data, ULONG data_size,
    NX_PACKET **response_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP adresine bir ping isteği gönderir ve ping yanıt iletisi için belirtilen süre kadar bekler. Yanıt alınamasa bir hata döndürülür. Aksi takdirde yanıt iletisi, yanıt iletisi tarafından işaret response_ptr. 

Uygulamalar, bir IPv6 hedefine ping isteği göndermek için ***nxd_icmp_ping** _ veya *___* nxd_icmp_source_ping * hizmetini kullanacağız.

> [!WARNING]  
> *Bir NX_SUCCESS döndürülürse, uygulama alınan paketi* artık gerekli kalmadan serbest bırakmakla sorumludur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **ip_address** Ping yapmak için konak bayt sırasına göre IP adresi.
- **veriler** Ping iletisi için veri alanına işaretçi.
- **data_size** Ping verisinde bayt sayısı
- **response_ptr** Içinde ping yanıt iletisi dönmek için paket işaretçisi işaretçisi.
- **wait_option** Ping yanıtını beklemek için ThreadX zamanlayıcı tık sayısını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:

| Wait seçeneği            | Değer                           |
| -----------------------|---------------------------------|
| NX_NO_WAIT             | 0xC0000                    |
| ticks içinde zaman aşımı değeri | (0x00000001 aracılığıyla 0xFFFFFFFE) |
| NX_WAIT_FOREVER        | Ffffffff                      |

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

No

### <a name="example"></a>Örnek

```c
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

- nx_icmp_enable
- nx_icmp_info_get
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nx_igmp_enable"></a>nx_igmp_enable
Internet Grubu Yönetim Protokolü 'Nü (ıGMP) etkinleştir

### <a name="prototype"></a>Prototype  

```c
UINT nx_igmp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneğindeki ıGMP bileşenini sunar. IGMP bileşeni, IP çok noktaya yayın grup yönetimi işlemlerine yönelik destek sağlamaktan sorumludur.

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

No

### <a name="example"></a>Örnek

```c
/* Enable IGMP on the previously created IP Instance ip_0. */
status = nx_igmp_enable(&ip_0);

/* If status is NX_SUCCESS, IGMP is enabled. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_info_get"></a>nx_igmp_info_get
IGMP etkinlikleri hakkında bilgi alma

### <a name="prototype"></a>Prototype  

```c
UINT nx_igmp_info_get(
    NX_IP *ip_ptr,
    ULONG *igmp_reports_sent,
    ULONG *igmp_queries_received,
    ULONG *igmp_checksum_errors,
    ULONG *current_groups_joined);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için ıGMP etkinlikleri hakkında bilgi alır.

> [!IMPORTANT]  
> *Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez*.

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

No

### <a name="example"></a>Örnek

```c
/* Retrieve IGMP information from previously created IP Instance ip_0. */
status = nx_igmp_info_get(&ip_0, &igmp_reports_sent,
                          &igmp_queries_received,
                          &igmp_checksum_errors,
                          &current_groups_joined);

/* If status is NX_SUCCESS, IGMP information was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_loopback_disable"></a>nx_igmp_loopback_disable
IGMP geri döngüsünü devre dışı bırak

### <a name="prototype"></a>Prototype  

```c
UINT nx_igmp_loopback_disable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Disable IGMP loopback for all subsequent multicast groups
   joined. */
status = nx_igmp_loopback_disable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is disabled. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_loopback_enable"></a>nx_igmp_loopback_enable
IGMP geri döngüsünü etkinleştir

### <a name="prototype"></a>Prototype  

```c
UINT nx_igmp_loopback_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Enable IGMP loopback for all subsequent multicast
   groups joined. */
status = nx_igmp_loopback_enable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is enabled. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_multicast_interface_join"></a>nx_igmp_multicast_interface_join
IP örneğini bir arabirim aracılığıyla belirtilen çok noktaya yayın grubuna ekleyin

### <a name="prototype"></a>Prototype  

```c
UINT nx_igmp_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen ağ arabirimi aracılığıyla bir IP örneğini belirtilen çok noktaya yayın grubuna birleştirir. Aynı grubun kaç kez katıldığını izlemek için bir iç sayaç tutulur. Çok noktaya yayın grubuna katıldıktan sonra, ıGMP bileşeni, belirtilen ağ arabirimi aracılığıyla bu grup adresiyle IP paketlerinin alımına ve ayrıca bu IP 'nin bu çok noktaya yayın grubunun bir üyesi olduğu yönlendiricilere rapor vermeyecektir. IGMP üyelik birleşimi, rapor ve çıkış iletileri belirtilen ağ arabirimi aracılığıyla da gönderilir. Bir IPv4 çok noktaya yayın grubuna ıGMP grup üyeliği raporu göndermeden katmak için, uygulama hizmeti ***nx_ipv4_multicast_interface_join*** kullanacaktır.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **group_address** Ana bilgisayar bayt düzeninde katılacak sınıf D IP çok noktaya yayın grubu adresi.
- **interface_index** NetX Duo örneğine iliştirilmiş arabirimin dizini.

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

No

### <a name="example"></a>Örnek

```c
/* Previously created IP Instance joins the multicast group
   244.0.0.200, via the interface at index 1 in the IP interface
   list. */
#define INTERFACE_INDEX 1
status = nx_igmp_multicast_interface_join
                                 (&ip IP_ADDRESS(244,0,0,200),
                                  INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully joined
   the multicast group. */
```   
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_multicast_interface_leave"></a>nx_igmp_multicast_interface_leave
Belirtilen çok noktaya yayın grubunu bir arabirim aracılığıyla bırak

### <a name="prototype"></a>Prototype  

```c
UINT nx_igmp_multicast_interface_leave(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```
### <a name="description"></a>Description

Bu hizmet belirtilen ağ arabirimi aracılığıyla belirtilen çok noktaya yayın grubunu bırakır. Bir iç sayaç, aynı grubun bir üyesinin kaç kez bir üyesi olduğunu izlemek için tutulur. Çok noktaya yayın grubundan ayrıldıktan sonra, ıGMP bileşeni uygun üyelik raporunu gönderir ve bu düğümden üye yoksa gruptan ayrılamayabilir. Bir IPv4 çok noktaya yayın grubunu ıGMP grup üyeliği raporu göndermeden bırakmak için, uygulama hizmeti ***nx_ipv4_multicast_interface_leave*** kullanacaktır.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **group_address** Bırakılacak sınıf D IP çok noktaya yayın grubu adresi. IP adresi konak bayt sırasına göredir.
- **interface_index** NetX Duo örneğine eklenen Arabirimin dizini.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı çok noktaya yayın grubu birleştirme.
- **NX_ENTRY_NOT_FOUND** (0x16) Belirtilen çok noktaya yayın grubu adresi yerel çok noktaya yayın tablosunda bulunamıyor.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_INVALID_INTERFACE** (0x4C) Cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.
- **NX_IP_ADDRESS_ERROR** (0x21) Çok Noktaya Yayın grup adresi geçerli bir D sınıfı adres değildir.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) IP çok noktaya yayın desteği etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Leave the multicast group 244.0.0.200. */
#define INTERFACE_INDEX 1
status = nx_igmp_multicast_interface_leave
                                (&ip IP_ADDRESS(244,0,0,200),
                                 INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully leaves
   the multicast group 244.0.0.200. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_multicast_join"></a>nx_igmp_multicast_join
IP örneğini belirtilen çok noktaya yayın grubuna birleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nx_igmp_multicast_join(
    NX_IP *ip_ptr, 
    ULONG group_address);
```
### <a name="description"></a>Description

Bu hizmet, bir IP örneğini belirtilen çok noktaya yayın grubuna katıyor. Aynı grubun katılma sayısını izlemek için bir iç sayaç korunur. Sürücüden, ağ üzerinde ana bilgisayar grubunun katılma amacını belirten ilk birleştirme isteği ise bir IGMP raporu göndermesi komutu kullanılır. Birleştirmeden sonra, IGMP bileşeni bu grup adresine sahip IP paketlerinin alımına ve bu IP'nin bu çok noktaya yayın grubunun üyesi olduğu yönlendiricilere rapora izin verecek. Uygulama, IGMP grup üyeliği raporu göndermeden bir IPv4 çok noktaya yayın grubuna katılmak için ***nx_ipv4_multicast_interface_join.***

> [!NOTE]  
> *Birincil olmayan bir cihazda çok noktaya yayın grubuna katılmak için hizmet **nx_igmp_multicast_interface_join.***

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **group_address** Katılmak için D SıNıFı IP çok noktaya yayın grubu adresi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı çok noktaya yayın grubu birleştirme.
- **NX_NO_MORE_ENTRIES** (0x17) Daha fazla çok noktaya yayın grubu birleştirilemeyecek, maksimum değer aşılır.
- **NX_INVALID_INTERFACE** (0x4C) Cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz IP grubu adresi.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Previously created IP Instance ip_0 joins the multicast group
   224.0.0.200. */
status = nx_igmp_multicast_join(&ip_0, IP_ADDRESS(224,0,0,200);

/* If status is NX_SUCCESS, this IP instance has successfully
   joined the multicast group 224.0.0.200. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_multicast_leave"></a>nx_igmp_multicast_leave
IP örneğinin belirtilen çok noktaya yayın grubundan ayrılmaya neden olur

### <a name="prototype"></a>Prototype  

```c
UINT nx_igmp_multicast_leave(
    NX_IP *ip_ptr, 
    ULONG group_address);
```
### <a name="description"></a>Description

Bu hizmet, bırakma isteği sayısı birleştirme isteklerinin sayısıyla eşiliyorsa ip örneğinin belirtilen çok noktaya yayın grubundan ayrılmasını sağlar. Aksi takdirde, iç birleşim sayısı yalnızca kullanımdan sayılır. IGMP grup üyeliği raporu göndermeden bir IPv4 çok noktaya yayın grubundan ayrılmak için uygulama, IPv4 çok noktaya ***yayın*** nx_ipv4_multicast_interface_leave.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **group_address** Ayrılılacak çok noktaya yayın grubu.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı çok noktaya yayın grubu birleştirme.
- **NX_ENTRY_NOT_FOUND** (0x16) Önceki birleştirme isteği bulunamadı.
- **NX_INVALID_INTERFACE** (0x4C) Cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz IP grubu adresi.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Cause IP instance to leave the multicast group 224.0.0.200. */
status = nx_igmp_multicast_leave(&ip_0, IP_ADDRESS(224,0,0,200);

/* If status is NX_SUCCESS, this IP instance has successfully left
   the multicast group 224.0.0.200. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_ip_address_change_notifiy"></a>nx_ip_address_change_notifiy
IP adresi değişirse uygulamaya bildirme

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_address_change_notify(
    NX_IP *ip_ptr,
    VOID(*change_notify)(NX_IP *, VOID *),
    VOID *additional_info);
```
### <a name="description"></a>Description

Bu hizmet, IPv4 adresi her değiştiriken çağrılan bir uygulama bildirimi işlevini kaydedmektedir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **change_notify** IP değişiklik bildirimi işlevinin işaretçisi. Bu parametre doğru NX_NULL IP adresi değişiklik bildirimi devre dışı bırakılır.
- **additional_info** IP adresi değiştiriken bildirim işlevine de sağlanan isteğe bağlı ek bilgilerin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı IP adresi değişiklik bildirimi.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Register the function "my_ip_changed" to be called whenever the
   IP address is changed. */
status = nx_ip_address_change_notify(&ip_0, my_ip_changed,
                                      NX_NULL);

/* If status is NX_SUCCESS, the "my_ip_changed" function will be
   called whenever the IP address changes. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_address_get"></a>nx_ip_address_get
IPv4 adresini ve ağ maskesini alma

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_address_get(
    NX_IP *ip_ptr,
    ULONG *ip_address,
    ULONG *network_mask);
```
### <a name="description"></a>Description

Bu hizmet, birincil ağ arabiriminin IPv4 adresini ve alt ağ maskesini verir.

> [!IMPORTANT]   
> *İkincil cihazın bilgilerini almak için **nx_ip_interface_address_get** hizmetini kullanın.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **ip_address** IP adresi için hedefin işaretçisi.
- **network_mask** Ağ maskesi için hedefin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı IP adresi get.
- **NX_PTR_ERROR** (0x07) Geçersiz IP veya dönüş değişkeni işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Get the IP address and network mask from the previously created
   IP Instance ip_0. */
status = nx_ip_address_get(&ip_0, &ip_address, &network_mask);

/* If status is NX_SUCCESS, the variables ip_address and
   network_mask contain the IP and network mask respectively. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_address_set"></a>nx_ip_address_set
IPv4 adresini ve ağ maskesini ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_address_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG network_mask);
```
### <a name="description"></a>Description

Bu hizmet, birincil ağ arabirimi için IPv4 adresini ve ağ maskesini ayarlar.

> [!IMPORTANT]  
> *İkincil cihaz için IP adresi ve ağ maskesi ayarlamak üzere **nx_ip_interface_address_set** hizmetini kullanın.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **ip_address** Yeni IP adresi.
- **network_mask** Yeni ağ maskesi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı IP adresi kümesi.
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz IP adresi.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Set the IP address and network mask to 1.2.3.4 and 0xFFFFFF00 for
   the previously created IP Instance ip_0. */
status = nx_ip_address_set(&ip_0, IP_ADDRESS(1,2,3,4),
                           0xFFFFFF00UL);

/* If status is NX_SUCCESS, the IP instance now has an IP address of
   1.2.3.4 and a network mask of 0xFFFFFF00. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_auxiliary_packet_pool_set"></a>nx_ip_auxiliary_packet_pool_set
Yardımcı paket havuzu yapılandırma

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_auxiliary_packet_pool_set(
    NX_IP *ip_ptr,
    NX_PACKET_POOL *aux_pool);
```
### <a name="description"></a>Description

Bu hizmet, IP örneğinde bir yardımcı paket havuzu yapılandırıyor. Bellek kısıtlı bir sistem için kullanıcı, MTU paket boyutuna sahip varsayılan paket havuzunu oluşturarak ve IP iş parçacığının küçük paketleri ile iletecek daha küçük paket boyutuna sahip bir yardımcı paket havuzu oluşturarak bellek verimliliğini artırabilir. Yardımcı havuz için önerilen paket boyutu 256 bayttır. IPv6 ve IPsec'in her ikisi de etkindir.

Varsayılan olarak IP örneği yardımcı paket havuzunu kabul etmez. Bu özelliği etkinleştirmek *NX_DUAL_PACKET_POOL_ENABLE* NetX Duo kitaplığını derlemek için tanımlanmalıdır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **aux_pool** IP örneği için yapılandırılan yardımcı paket havuzu.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı IP adresi kümesi.
- **NX_NOT_SUPPORTED** (0x4B) İkili paket havuzu özelliği kitaplıkta derlenmiş değil.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi veya havuz işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası  

No

### <a name="example"></a>Örnek

```c
#define SMALL_PAYLOAD_SIZE 256
NX_PACKET small_pool;

nx_packet_pool_create(&small_pool, "small pool", SMALL_PAYLOAD_SIZE,
                       small_pool_memory_ptr, small_pool_size);

/* Add the small packet pool to the IP instance. */
status = nx_ip_auxiliary_packet_pool_set(&ip_0, &small_pool);

/* If status is NX_SUCCESS, the IP instance now is able to use the
   small pool for transmitting small datagram. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_ip_create"></a>nx_ip_create
IP örneği oluşturma

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_create(
    NX_IP *ip_ptr, 
    CHAR *name, ULONG ip_address,
    ULONG network_mask, 
    NX_PACKET_POOL *default_pool,
    VOID (*ip_network_driver)(NX_IP_DRIVER *),
    VOID *memory_ptr, 
    ULONG memory_size,
    UINT priority);
```
### <a name="description"></a>Description

Bu hizmet, kullanıcı tarafından sağlanan IP adresi ve ağ sürücüsü ile bir IP örneği oluşturur. Buna ek olarak, uygulamanın IÇ paket ayırma için kullanmak üzere IP örneği için önceden oluşturulmuş bir paket havuzu sağlamak gerekir. Sağlanan uygulama ağ sürücüsünün, bu IP'nin iş parçacığı yürütülene kadar çağrılmay olduğunu unutmayın.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Yeni bir IP örneği oluşturmak için denetim bloğuna işaretçi.
- **name** Bu yeni IP örneğinin adı.
- **ip_address** Bu yeni IP örneğinin IP adresi.
- **network_mask** Alt ve süper olumsuzluk kullanımları için IP adresinin ağ bölümünü ifade etmek için maskeleme.
- **default_pool** Daha önce oluşturulan NetX Duo paket havuzunun denetim bloğuna işaretçi.
- **ip_network_driver** IP paketlerini göndermek ve almak için kullanılan kullanıcı tarafından sağlanan ağ sürücüsü.
- **memory_ptr** IP yardımcı iş parçacığının yığın alanı için bellek alanına işaretçi.
- **memory_size** IP yardımcı iş parçacığı yığını için bellek alanında bayt sayısı.
- **öncelik** IP yardımcı iş parçacığının önceliği.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı IP örneği oluşturma.
- **NX_NOT_IMPLEMENTED** (0x4A) NetX Duo kitaplığı yanlış yapılandırılmış.
- **NX_PTR_ERROR** (0x07) Geçersiz IP, ağ sürücüsü işlev işaretçisi, paket havuzu veya bellek işaretçisi.
- **NX_SIZE_ERROR** (0x09) Sağlanan yığın boyutu çok küçük.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_IP_ADDRESS_ERROR** (0x21) Sağlanan IP adresi geçersiz.
- **NX_OPTION_ERROR** (0x21) Sağlanan IP iş parçacığı önceliği geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Create an IP instance with an IP address of 1.2.3.4 and a network
   mask of 0xFFFFFF00UL. The "ethernet_driver" specifies the entry
   point of the application specific network driver and the
   "stack_memory_ptr" specifies the start of a 1024 byte memory
   area that is used for this IP instance’s helper thread. */
status = nx_ip_create(&ip_0, "NetX IP Instance ip_0",
                      IP_ADDRESS(1, 2, 3, 4),
                      0xFFFFFF00UL, &pool_0, ethernet_driver,
                      stack_memory_ptr, 1024, 1);

/* If status is NX_SUCCESS, the IP instance has been created. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_delete"></a>nx_ip_delete
Önceden oluşturulan IP örneğini Sil

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_delete(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

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

```c
/* Delete a previously created IP instance. */
status = nx_ip_delete(&ip_0);

/* If status is NX_SUCCESS, the IP instance has been deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz. 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_driver_direct_command"></a>nx_ip_driver_direct_command
Ağ sürücüsüne komut verme

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_driver_direct_command
    (NX_IP *ip_ptr,
    UINT command,
    ULONG *return_value_ptr);
```
### <a name="description"></a>Description

Bu hizmet, uygulamanın ***nx_ip_create*** çağrısı sırasında belirtilen birincil ağ arabirimi sürücüsüne doğrudan bir arabirim sağlar. Uygulamaya özgü komutlar, sayısal değerleri NX_LINK_USER_COMMAND daha büyük veya eşit bir değere göre kullanılabilir.

> [!IMPORTANT]  
> *İkincil cihaz için komut vermek üzere **nx_ip_driver_interface_direct_command** hizmetini kullanın*.

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

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Make a direct call to the application-specific network driver
   for the previously created IP instance. For this example, the
   network driver is interrogated for the link status. */
status = nx_ip_driver_direct_command(&ip_0, NX_LINK_GET_STATUS,
                                     &link_status);

/* If status is NX_SUCCESS, the link_status variable contains a
   NX_TRUE or NX_FALSE value representing the status of the
   physical link. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_driver_interface_direct_command"></a>nx_ip_driver_interface_direct_command
Ağ sürücüsüne sorun komutu

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_driver_interface_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    UINT interface_index,
    ULONG *return_value_ptr);
```
### <a name="description"></a>Description

Bu hizmet, IP örneğinde uygulamanın ağ cihazı sürücüsüne doğrudan bir komut sağlar. Uygulamaya özgü komutlar, sayısal değerlerin NX_LINK_USER_COMMAND'den büyük veya *bu değere eşit olması NX_LINK_USER_COMMAND.*

### <a name="parameters"></a>Parametreler  

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **komutu** Sayısal komut kodu. Standart komutlar aşağıdaki gibi tanımlanır:
    - NX_LINK_GET_STATUS (10)
    - NX_LINK_GET_SPEED (11)
    - NX_LINK_GET_DUPLEX_TYPE (12)
    - NX_LINK_GET_ERROR_COUNT (13)
    - NX_LINK_GET_RX_COUNT (14)
    - NX_LINK_GET_TX_COUNT (15)
    - NX_LINK_GET_ALLOC_ERRORS (16)
    - NX_LINK_USER_COMMAND (50)
- **interface_index** Komutun gönder gerektiği ağ arabirimi dizini.
- **return_value_ptr** Çağıranda değişken dönüş işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı ağ sürücüsü doğrudan komutu.
- **NX_UNHANDLED_COMMAND** (0x44) İşsiz veya uygulanmamış ağ sürücüsü komutu.
- **NX_INVALID_INTERFACE** (0x4C) Geçersiz arabirim dizini
- **NX_PTR_ERROR** (0x07) Geçersiz IP veya dönüş değeri işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
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

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_forwarding_disable"></a>nx_ip_forwarding_disable  
IP paketi iletmeyi devre dışı bırakma

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_forwarding_disable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet NetX Duo IP bileşeni içinde IP paketlerini iletmeyi devre dışı bırakıyor. IP görevi oluşturulurken bu hizmet otomatik olarak devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı IP iletme devre dışı bırak.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları, süreerler

### <a name="preemption-possible"></a>Önserme Olası  

No

### <a name="example"></a>Örnek

```c
/* Disable IP forwarding on this IP instance. */
status = nx_ip_forwarding_disable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been disabled on the
   previously created IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.  

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_forwarding_enable"></a>nx_ip_forwarding_enable
IP paket iletmeyi etkinleştir

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_forwarding_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, IP paketlerinin NetX Duo IP bileşeni içinde iletilmesine izin vermez. Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) başarılı IP iletimi etkin.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Enable IP forwarding on this IP instance. */
status = nx_ip_forwarding_enable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been enabled on the
   previously created IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz. 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_fragment_disable"></a>nx_ip_fragment_disable
IP paketi fragmenting devre dışı bırak

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_fragment_disable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, IPv4 ve IPv6 paketi fragmenting devre dışı bırakır ve işlevselliği yeniden birleştirir. Yeniden birleştirilme bekleyen paketler için, bu hizmet bu paketleri yayınlar. Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.

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

No

### <a name="example"></a>Örnek

```c
/* Disable IP fragmenting on this IP instance. */
status = nx_ip_fragment_disable(&ip_0);

/* If status is NX_SUCCESS, disables IP fragmenting on the
   previously created IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.  

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_fragment_enable"></a>nx_ip_fragment_enable
IP paketi fragmenting etkinleştir

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_fragment_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, IPv4 ve IPv6 paketi fragmenting ve yeniden birleştirilen işlevselliği sunar. Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) başarılı IP parçası etkinleştirme.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) IP parçalama özellikleri NETX Duo içine derlenmiyor.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Enable IP fragmenting on this IP instance. */
status = nx_ip_fragment_enable(&ip_0);

/* If status is NX_SUCCESS, IP fragmenting has been enabled on the
   previously created IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.  

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_gateway_address_clear"></a>nx_ip_gateway_address_clear
IPv4 ağ geçidi adresini temizle

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_gateway_address_clear(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, örnekte yapılandırılan IPv4 ağ geçidi adresini temizler. IP örneğinden bir IPv6 varsayılan dıştaki öğesini temizlemek için uygulamalar hizmeti ***nxd_ipv6_default_router_delete kullanacaktır.***

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) IP ağ geçidi adresini başarıyla temizledi.
- **NX_PTR_ERROR** (0x07) geçersiz IP denetim bloğu
- **NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Clear the gateway address of IP instance. */
status = nx_ip_gateway_address_clear(&ip_0);

/* If status == NX_SUCCESS, the gateway address was successfully
   cleared from the IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.

-nx_ip_gateway_address_get-nx_ip_gateway_address_set-nx_ip_info_get-nx_ip_static_route_add-nx_ip_static_route_delete-nxd_ipv6_default_router_add-nxd_ipv6_default_router_delete-nxd_ipv6_default_router_entry_get-nxd_ipv6_default_router_get-nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_gateway_address_get"></a>nx_ip_gateway_address_get
IPv4 ağ geçidi adresini al

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_gateway_address_get(
    NX_IP *ip_ptr, 
    ULONG *ip_address);
```
### <a name="description"></a>Description

Bu hizmet, IP örneğinde yapılandırılan IPv4 ağ geçidi adresini alır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **ip_address** Ağ Geçidi adresinin depolandığı belleğin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı al 
- **NX_PTR_ERROR** (0x07) geçersiz IP denetim bloğu işaretçisi veya IP adresi işaretçisi
- **NX_NOT_FOUND** (0x4E) ağ geçidi adresi bulunamadı
- **NX_CALLER_ERROR** (0x11) S Hizm, sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
ULONG ip_address;

/* Get the gateway address of IP instance. */
status = nx_ip_gateway_address_get(&ip_0, &ip_address);

/* If status == NX_SUCCESS, the gateway address was successfully
   got. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_gateway_address_set"></a>nx_ip_gateway_address_set
Ağ geçidi IP adresi ayarla

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_gateway_address_set(
    NX_IP *ip_ptr, 
    ULONG ip_address);
```
### <a name="description"></a>Description

Bu hizmet, IPv4 ağ geçidi IP adresini ayarlar. Tüm ağ dışı trafik, iletim için bu ağ geçidine yönlendirilir. Ağ geçidine ağ arabirimlerinden biri aracılığıyla doğrudan erişilebilir olması gerekir. IPv6 ağ geçidi adresini yapılandırmak için hizmeti nxd_ipv6_default_router_add kullanın ***.*** 

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

No

### <a name="example"></a>Örnek

```c
/* Setup the Gateway address for previously created IP
   Instance ip_0. */
status = nx_ip_gateway_address_set(&ip_0, IP_ADDRESS(1,2,3,99);

/* If status is NX_SUCCESS, all out-of-network send requests are
   routed to 1.2.3.99. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_info_get"></a>nx_ip_info_get
IP etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype  

```c
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
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için IP etkinlikleri hakkında bilgi alır.

> [!NOTE]  
> *Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez*.

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

No

### <a name="example"></a>Örnek

```c
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

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_interface_address_get"></a>nx_ip_interface_address_get
Arabirim IP adresini al

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_address_get (
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *ip_address,
    ULONG *network_mask);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen ağ arabiriminin IPv4 adresini alır. Uygulama, IPv6 adresini almak için hizmeti kullanır ***nxd_ipv6_address_get***

> [!CAUTION]  
> *Birincil cihaz değilse belirtilen cihaz, daha önce IP örneğine eklenmiş olmalıdır*.

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

No

### <a name="example"></a>Örnek

```c
#define INTERFACE_INDEX 1

/* Get device IP address and network mask for the specified
   interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_get(ip_ptr,INTERFACE_INDEX,
                                     &ip_address,
                                     &network_mask);

/* If status is NX_SUCCESS the interface address was successfully
   retrieved. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_address_mapping_configure"></a>nx_ip_interface_address_mapping_configure
Adres eşlemesinin gerekli olup olmadığını yapılandırma

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_address_mapping_configure(
    NX_IP *ip_ptr,
    UINT interface_index,
    UINT mapping_needed);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen ağ arabirimi için MAC adresi eşlemesinin IP adresinin gerekli olup olmadığını yapılandırır. Bu hizmet genellikle arabirim cihaz sürücüsünden, temel alınan arabirimde IP adresinin katman iki (MAC) adres eşlemesini gerektirip gerektirmediğini bildirmek için kullanılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **interface_index** Ağ arabiriminin dizini
- **mapping_needed** NX_TRUE--adres eşleme gerekli NX_FALSE--adres eşleme gerekli değil

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yapılandırma
- **NX_INVALID_INTERFACE** (0x4C) cihaz dizini geçerli değil
- **NX_PTR_ERROR** (0x07) geçersiz IP denetimi blok işaretçisi
- **NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacığı

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0
UCHAR mapping_needed = NX_TRUE;

/* Configure address mapping needed specified interface. */
status = nx_ip_interface_address_mapping_configure(&ip_0,
                                             PRIMARY_INTERFACE,
                                             mapping_needed);

/* If status == NX_SUCCESS, the address mapping needed was
   successfully configured. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_address_set"></a>nx_ip_interface_address_set
Arabirim IP adresi ve ağ maskesini ayarla

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG ip_address,
    ULONG network_mask);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP arabirimi için IPv4 adresini ve ağ maskesini ayarlar. Uygulama, IPv6 arabirim adresini yapılandırmak için hizmeti ***nxd_ipv6_address_set*** kullanacaktır. 
 
> [!WARNING]  
> *Belirtilen arabirim daha önce IP örneğine eklenmiş olmalıdır*. 

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **interface_index** NetX Duo örneğine iliştirilmiş arabirimin dizini.
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

No

### <a name="example"></a>Örnek

```c
#define INTERFACE_INDEX 1

/* Set device IP address and network mask for the specified
   interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_set(ip_ptr, INTERFACE_INDEX,
                                     ip_address,
                                     network_mask);

/* If status is NX_SUCCESS the interface IP address and mask was
   successfully set. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_attach"></a>nx_ip_interface_attach
Ağ arabirimini IP örneğine Ekle

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_attach(
    NX_IP *ip_ptr, 
    CHAR *interface_name,
    ULONG ip_address,
    ULONG network_mask,
    VOID(*ip_link_driver)(struct NX_IP_DRIVER_STRUCT *));
```
### <a name="description"></a>Description

Bu hizmet, IP arabirimine bir fiziksel ağ arabirimi ekler. Bu durumda, her ek arabirimin birincil arabirime ikincil olması için, IP örneğinin birincil arabirimle oluşturulduğunu aklınızda bulunur. IP örneğine (birincil arabirim dahil) bağlı olan ağ arabirimlerinin toplam sayısı **NX_MAX_PHYSICAL_INTERFACES** aşamaz.

IP iş parçacığı henüz çalışmıyorsa, ikincil arabirimler tüm fiziksel arabirimleri Başlatan IP iş parçacığı başlatma sürecinin bir parçası olarak başlatılır.

IP iş parçacığı henüz çalışmıyorsa, ikincil arabirim ***nx_ip_interface_attach*** hizmetin bir parçası olarak başlatılır.

> [!WARNING]  
> *ip_ptr geçerli bir NetX Duo IP yapısına işaret etmelidir. IP örneği için ağ arabirimlerinin sayısı için **NX_MAX_PHYSICAL_INTERFACES** yapılandırılması gerekir. Varsayılan değer bir değeridir*.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **interface_name** Arabirim adı dizesinin işaretçisi.
- **ip_address** Konak bayt düzeninde cihaz IP adresi.
- **network_mask** Konak bayt düzeninde cihaz ağ maskesi.
- **ip_link_driver** Arabirim için Ethernet sürücüsü.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) girişi statik yönlendirme tablosuna eklenir.
- **NX_NO_MORE_ENTRIES** (0x17) en fazla arabirim sayısı. NX_MAX_PHYSICAL_INTERFACES aşıldı. IPv6 etkinse, bu hata sürücünün IPv6 çok noktaya yayın işlemlerini işlemek için yeterli kaynak olmadığını da belirtebilir.
- **NX_DUPLICATED_ENTRY** (0x52) sağlanan IP adresı bu IP örneğinde zaten kullanılıyor.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi girişi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
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

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_capability_get"></a>nx_ip_interface_capability_get
Arabirim donanımı özelliğini al

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_capability_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *interface_capability_flag);
```
### <a name="description"></a>Description

Bu hizmet, yetenek bayrağını belirtilen ağ arabiriminden verir. Bu hizmeti kullanmak için NetX Duo kitaplığının etkin seçeneğiyle ***NX_ENABLE_INTERFACE_CAPABILITY*** gerekir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **interface_index** Ağ arabirimi dizini
- **interface_capability_flag** Yetenek bayrağı için bellek alanı işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Arabirim yetenek bilgileri başarıyla edinildi.
- **NX_NOT_SUPPORTED** (0x4B) Arabirim özelliği özelliği bu derlemede desteklenmiyor.
- **NX_INVALID_INTERFACE** (0x4C) Arabirim dizini geçerli değil
- **NX_PTR_ERROR** (0x07) Geçersiz IP denetim bloğu işaretçisi veya Geçersiz yetenek bayrağı işaretçisi
- **NX_CALLER_ERROR** (0x11) Hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmaz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0
ULONG       capability_flag;

/* Get the hardware capability flag of specified interface. */
status = nx_ip_interface_capability_get(&ip_0,
                                        PRIMARY_INTERFACE,
                                        &capability_flag);

/* If status == NX_SUCCESS, the capability flag from the primary
   interface was successfully retrieved. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_capability_set"></a>nx_ip_interface_capability_set
Donanım özelliği bayrağını ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_capability_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG interface_capability_flag);
```                           
### <a name="description"></a>Description

Bu hizmet, belirtilen bir ağ arabirimi için yetenek bayrağını yapılandırmak üzere ağ cihazı sürücüsü tarafından kullanılır. Bu hizmeti kullanmak için NetX Duo kitaplığı tanımlandığı gibi seçeneğiyle ***NX_ENABLE_INTERFACE_CAPABILITY*** gerekir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **interface_index** Ağ arabirimi dizini
- **interface_capability_flag** Çıkış için yetenek bayrağı

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Arabirim donanımı yetenek bayrağını başarıyla ayarlayın.
- **NX_NOT_SUPPORTED** (0x4B) Arabirim özelliği özelliği bu derlemede desteklenmiyor.
- **NX_INVALID_INTERFACE** (0x4C) Arabirim dizini geçerli değil 
- **NX_PTR_ERROR** (0x07) Geçersiz IP denetim bloğu işaretçisi 
- **NX_CALLER_ERROR** (0x11) Hata, sistem başlatma veya iş parçacığı bağlamından çağrılmaz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0
ULONG capability_flag = \
                 NX_INTERFACE_CAPABILITY_IPV4_TX_CHECKSUM |\
                 NX_INTERFACE_CAPABILITY_IPV4_RX_CHECKSUM;
UINT device_index = 0;

/* Set the hardware capability flag of specified interface. */
status = nx_ip_interface_capability_set(&ip_0,
                                        PRIMARY_INTERFACE,
                                        capability_flag);

/* If status == NX_SUCCESS, the hardware capability flag was
   successfully set. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_detach"></a>nx_ip_interface_detach
Belirtilen arabirimi IP örneğinden ayırma

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr, 
    UINT index);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP arabirimini IP örneğinden ayırır. Bir arabirim kaldırıldıktan sonra, tüm bağlı TCP yuvaları kapatılır ve bu arabirim için ND önbelleği ve ARP girişleri ilgili tablolarından kaldırılır. Bu arabirim için IGMP üyelikleri kaldırılır.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **dizin** Kaldırılacak arabirimin dizini.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Fiziksel arabirim başarıyla kaldırıldı.
- **NX_INVALID_INTERFACE** (0x4C) Belirtilen ağ arabirimi geçersiz.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçiler.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
#define INTERFACE_INDEX 1

/* Detach interface 1. */
status = nx_ip_interface_detach(&IP_0, INTERFACE_INDEX);

/* If status is NX_SUCCESS the interface is successfully detached
   from the IP instance. */
```

### <a name="see-also"></a>Ayrıca Bkz.  

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_info_get"></a>nx_ip_interface_info_get
Ağ arabirimi parametrelerini al

### <a name="prototype"></a>Prototype  

```c
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
### <a name="description"></a>Description

Bu hizmet, belirtilen ağ arabirimi için ağ parametreleriyle ilgili bilgileri alır. Tüm veriler ana bilgisayar bayt düzeninde alınır. 

> [!WARNING]  
> *ip_ptr geçerli bir NetX Duo IP yapısına işaret etmelidir. Belirtilen arabirim, birincil arabirim değilse, daha önce IP örneğine* eklenmelidir.

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

No

### <a name="example"></a>Örnek

```c
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

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_mtu_set"></a>nx_ip_interface_mtu_set
Bir ağ arabiriminin MTU değerini ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_mtu_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG mtu_size);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen ağ arabirimi için IP MTU değerini yapılandırmak üzere cihaz sürücüsü tarafından kullanılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **interface_index** Ağ arabiriminin dizini
- **mtu_size** IP MTU boyutu

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) MTU değeri başarıyla ayarlandı
- **NX_INVALID_INTERFACE** (0x4C) arabirim dizini geçerli değil
- **NX_PTR_ERROR** (0x07) geçersiz IP denetimi blok işaretçisi
- **NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0
ULONG       mtu_size = 1500;

/* Set the MTU size of specified interface. */
status = nx_ip_interface_mtu_set(&ip_0,
                                 PRIMARY_INTERFACE, mtu_size);

/* If status == NX_SUCCESS, the MTU size was successfully set. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_physical_address_get"></a>nx_ip_interface_physical_address_get
Ağ cihazının fiziksel adresini al

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_physical_address_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *physical_msw,
    ULONG *physical_lsw);
```
### <a name="description"></a>Description

Bu hizmet, IP örneğinden bir ağ arabiriminin fiziksel adresini alır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **interface_index** Ağ arabiriminin dizini
- **physical_msw** Cihaz MAC adresi için en iyi 16 bit için hedef işaretçisi
- **physical_lsw** Cihaz MAC adresinin daha düşük 32 bitleri için hedef işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı al
- **NX_INVALID_INTERFACE** (0x4C) arabirim dizini geçerli değil
- **NX_PTR_ERROR** (0x07) geçersiz IP denetim bloğu işaretçisi veya fiziksel adres işaretçisi
- **NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0
ULONG   physical_msw;
ULONG   physical_lsw;

/* Get the physical address of specified interface. */
status = nx_ip_interface_physical_address_get(&ip_0,
                                              PRIMARY_INTERFACE,
                                              &physical_msw,
                                              &physical_lsw);

/* If status == NX_SUCCESS, the physical address was successfully
   retrieved. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_physical_address_set"></a>nx_ip_interface_physical_address_set
Belirtilen ağ arabirimi için fiziksel adresi ayarla

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_physical_address_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG physical_msw,
    ULONG physical_lsw,
    UINT update_driver);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen ağ arabiriminin MAC adresinin fiziksel adresini yapılandırmak için uygulama veya bir cihaz sürücüsü tarafından kullanılır. Yeni MAC adresi, arabirim yapısının denetim bloğuna uygulanır. ***Update_driver*** bayrağı ayarlandıysa, cihaz sürücüsü bu MAC adresini Ethernet denetleyicisi olarak programlanabilir olarak güncelleştirebilmesi için bir sürücü düzeyi komut çıkarılır.

Tipik bir durumda, bu hizmet, MAC adresinin IP yığınına bildirimde bulunan başlatma aşaması sırasında arabirim cihaz sürücüsünden çağrılır. Bu durumda ***update_driver*** bayrağı ayarlanmamalıdır.

Bu yordam, çalışma zamanında arabirim MAC adresini yeniden yapılandırmak için Kullanıcı uygulamasından da çağrılabilir. Bu kullanım durumunda, yeni MAC adresinin cihaz sürücüsüne uygulanabilmesi için ***update_driver*** bayrağının ayarlanması gerekir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **interface_index** Ağ arabiriminin dizini
- **physical_msw** Cihaz MAC adresi için en iyi 16 bit için hedef işaretçisi
- **physical_lsw** Cihaz MAC adresinin daha düşük 32 bitleri için hedef işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı küme
- **NX_UNHANDLED_COMMAND** (0x4b) komutu sürücü tarafından tanınmıyor
- **NX_INVALID_INTERFACE** (0x4C) arabirim dizini geçerli değil
- **NX_PTR_ERROR** (0x07) geçersiz IP denetimi blok işaretçisi
- **NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0
ULONG       physical_msw = 0x00CF;
ULONG       physical_lsw = 0x01020304;

/* Set the physical address of specified device. */
status = nx_ip_interface_physical_address_set(&ip_0,
                                              PRIMARY_INTERFACE,
                                              physical_msw,
                                              physical_lsw,
                                              NX_TRUE);

/* If status == NX_SUCCESS, the physical address was successfully
   set. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_status_check"></a>nx_ip_interface_status_check
Bir IP örneğinin durumunu denetleme

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_interface_status_check(
    NX_IP *ip_ptr,
    UINT interface_index
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir IP örneğinin ağ arabiriminin belirtilen durumunu denetler ve isteğe bağlı olarak bekler.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **interface_index** Arabirim dizin numarası needed_status istenen IP durumu, bit eşleme biçiminde şu şekilde tanımlanır:
  - **NX_IP_INITIALIZE_DONE** (0x0001)
  - **NX_IP_ADDRESS_RESOLVED** (0x0002)
  - **NX_IP_LINK_ENABLED** (0x0004)
  - **NX_IP_ARP_ENABLED** (0x0008)
  - **NX_IP_UDP_ENABLED** (0x0010)
  - **NX_IP_TCP_ENABLED** (0x0020)
  - **NX_IP_IGMP_ENABLED** (0x0040)
  - **NX_IP_RARP_COMPLETE** (0x0080)
  - **NX_IP_INTERFACE_LINK_ENABLED** (0x0100)
- **actual_status** Gerçek bitler kümesinin hedefi işaretçisi. wait_option, istenen durum bitleri yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **NX_NO_WAIT** (0x00000000)
  - **zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)
  - **NX_WAIT_FOREVER** 0xFFFFFFFF

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

No

### <a name="example"></a>Örnek

```c
/* Wait 10 ticks for the link up status on the previously created IP
   instance. */
status = nx_ip_interface_status_check(&ip_0, 1, NX_IP_LINK_ENABLED,
                                      &actual_status, 10);

/* If status is NX_SUCCESS, the secondary link for the specified IP
   instance is up. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_link_status_change_notify_set"></a>nx_ip_link_status_change_notify_set
Bağlantı durumu değiştirme bildirimi geri arama işlevini ayarla

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_link_status_change_notify_set(
    NX_IP *ip_ptr,
    VOID(*link_status_change_notify)(NX_IP *ip_ptr, UINT interface_index, UINT link_up));
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Configure a callback function to be used when the physical
   interface status is changed. */
status = nx_ip_link_status_change_notify_set(&ip_0,
                                             my_change_cb);

/* If status == NX_SUCCESS, the link status change notify function
   is set. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check

## <a name="nx_ip_max_payload_size_find"></a>nx_ip_max_payload_size_find
İşlem en yüksek paket veri yükü

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_max_payload_size_find(
    NX_IP *ip_ptr,
    NXD_ADDRESS *dest_address,
    UINT if_index,
    UINT src_port,
    UINT dest_port,
    ULONG protocol,
    ULONG *start_offset_ptr,
    ULONG *payload_length_ptr);
```
### <a name="description"></a>Description

Bu hizmet, hedefe ulaşmak için IP parçalanmasını gerektirmeyen en büyük uygulama yükü boyutunu bulur; Örneğin, yük yerel arabirim MTU boyutunun altında veya altında olur. (veya IPv6 yolu MTU Keşfi aracılığıyla elde edilen yol MTU değeri). IP üstbilgisi ve üst uygulama üst bilgi boyutu (TCP veya UDP) Toplam yükten çıkarılır. NetX Duo IPSec Güvenlik Ilkesi bu uç noktaya geçerliyse, IPSec üstbilgileri (ESP/AH) ve Ilk vektör gibi ilişkili ek yük da MTU 'dan çıkarılır. Bu hizmet hem IPv4 hem de IPv6 paketleri için geçerlidir.

*İf_index* parametresi, paketi göndermek için kullanılacak arabirimi belirtir. Çok ana bir sistem için, hedef bir yayın (yalnızca IPv4), çok noktaya yayın veya IPv6 bağlantısı-yerel adresi ise çağıranın *if_index* parametresini belirtmesi gerekir.

Bu hizmet, çağırana iki değer döndürür:

1) start_offset_ptr: TCP/UDP/IP/IPSec başlıklarındaki konumdur;
2) payload_length_ptr: veri uygulama miktarı, MTU aşmadan aktarılamaz.

Eşdeğer bir NetX hizmeti yoktur.

### <a name="restrictions"></a>Kısıtlamalar 

IP örneğinin önceden oluşturulması gerekir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP örneği işaretçisi
- **dest_address** Paket hedef adresi işaretçisi
- **if_index** Kullanılacak arabirimin dizinini belirtir
- **src_port** Kaynak bağlantı noktası numarası
- **dest_port** Hedef bağlantı noktası numarası
- **protokol** Kullanılacak üst katman Protokolü
- **start_offset_ptr** Maksimum paket yükü için veri başına işaretçi
- **payload_length_ptr** Üst bilgi hariç yük boyutu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) yük başarıyla hesaplandı
- **NX_INVALID_INTERFACE** (0x4C) arabirim dizini geçersiz veya arabirim geçerli değil.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi veya geçersiz hedef adresi
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz adres sağlandı 
- **NX_NOT_SUPPORTED** (0X4b) geçersiz protokol (UDP veya TCP değil)
- **NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* The following example determines the maximum payload for UDP
   packet to remote host. */
#define PRIMARY_INTERFACE 0
status = nx_ip_max_payload_size_find(&ip_0,
                                     &dest_ipv6_address,
                                     PRIMARY_INTERFACE,
                                     source_port,
                                     dest_port, NX_PROTOCOL_UDP,
                                     &start_offset,
                                     &payload_length);

/* A return value of NX_SUCCESS indicates the packet payload
   payload_length starting at the offset start_offset is
   successfully computed. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_raw_packet_disable"></a>nx_ip_raw_packet_disable
Ham paket gönderme/alma özelliğini devre dışı bırakma

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_raw_packet_disable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, bu IP örneği için ham IP paketlerinin iletimini ve alımını devre dışı bırakıyor. Ham paket hizmeti daha önce etkinleştirilmişse ve alma kuyruğunda ham paketler varsa, bu hizmet alınan tüm ham paketleri serbest bırakmıştır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı IP ham paketi devre dışı bırakma.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Disable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_disable(&ip_0);
/* If status is NX_SUCCESS, raw IP packet sending/receiving has
   been disabled for the previously created IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_enable"></a>nx_ip_raw_packet_enable
Ham paket işlemeyi etkinleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_raw_packet_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, bu IP örneği için ham IP paketlerinin iletimini ve alımını sağlar. Gelen TCP, UDP, ICMP ve IGMP paketleri NetX Duo tarafından işlenmeye devam ediyor. Bilinmeyen üst katman protokol türlerine sahip paketler ham paket alımı yordamı tarafından işlenir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı IP ham paketi etkinleştirme.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Enable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_enable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
   been enabled for the previously created IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_filter_set"></a>nx_ip_raw_packet_filter_set
Ham IP paket filtresini ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_raw_packet_filter_set(
    NX_IP *ip_ptr,
    UINT (*raw_packet_filter)(NX_IP *, ULONG, NX_PACKET *));
```
### <a name="description"></a>Description

Bu hizmet IP ham paket filtresini yapılandırıyor. Kullanıcı uygulaması tarafından uygulanan ham paket filtresi işlevi, bir uygulamanın kullanıcı tarafından sağlanan ölçütlere göre ham paketleri almalarına olanak sağlar. NetX Duo BSD sarmalayıcı katmanının, BSD katmanında ham yuvayı işlemek için ham paket filtresi özelliğini kullandığını unutmayın. Bu hizmeti kullanmak için NetX Duo kitaplığı, tanımlanan seçenekle ***NX_ENABLE_IP_RAW_PACKET_FILTER*** gerekir.

### <a name="parameters"></a>Parametreler  

- **ip_ptr** IP denetim bloğu işaretçisi
- **raw_packet_filter** Ham paket filtresinin işlev işaretçisi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Ham paket filtresi yordamını başarıyla ayarlama
- **NX_NOT_SUPPORT** (0x4B) Ham paket desteği kullanılamıyor
- **NX_PTR_ERROR** (0x07) Geçersiz IP denetim bloğu işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
UINT raw_packet_filter(NX_IP *ip_ptr, ULONG protocol,
                       NX_PACKET *packet_ptr)
{

/* Simply filter protocol. */
if(protocol == NX_IP_RAW)
   return NX_SUCCESS;
else
   return NX_NOT_SUCCESSFUL;
}

void raw_packet_thread_entry(ULONG id)
{

/* Set the raw packet filter of IP instance. */
status = nx_ip_raw_packet_filter_set(&ip_0,
                                     raw_packet_filter);

/* If status == NX_SUCCESS, the raw packet filter of IP instance
   was successfully set. */
}
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_receive"></a>nx_ip_raw_packet_receive
Ham IP paketi alma

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_raw_packet_receive(
    NX_IP *ip_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneğinden bir ham IP paketi alır. Ham paket alma kuyruğunda IP paketleri varsa, ilk (en eski) paket çağırana döndürülür. Aksi takdirde, kullanılabilir paket yoksa, çağıranı bekleme seçeneği tarafından belirtilen şekilde askıya alabilir.

> [!CAUTION]   
> *Bu NX_SUCCESS döndürülürse,* uygulama artık gerekli olmadığı zaman alınan paketi serbest bırakmakla sorumludur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **packet_ptr** Alınan ham IP paketinin yer aldığı işaretçi.
- **wait_option** Paketler kullanılamıyorsa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
   - **NX_NO_WAIT** (0x00000000)
   - **NX_WAIT_FOREVER** (0xFFFFFFFF)
   - **ticks içinde zaman aşımı değeri** (0x00000001-0xfffffffe)

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

No

### <a name="example"></a>Örnek

```c
/* Receive a raw IP packet for this IP instance, wait for a maximum
   of 4 timer ticks. */
status = nx_ip_raw_packet_receive(&ip_0, &packet_ptr, 4);

/* If status is NX_SUCCESS, the raw IP packet pointer is in the
   variable packet_ptr. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_send"></a>nx_ip_raw_packet_send
Ham IP paketi gönder

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_raw_packet_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    ULONG type_of_service);
```
### <a name="description"></a>Description

Bu hizmet, hedef IP adresine bir ham IPv4 paketi gönderir. Bu yordamın hemen geri döndüğüne ve bu nedenle IP paketinin gerçekten gönderilip gönderilmediğini bilinmediğini unutmayın. Ağ sürücüsü, iletim tamamlandığında paketin serbest bırakılmasından sorumlu olacaktır.

NetX Duo, çok kullanıcılı bir sistem için hedef IP adresini kullanarak uygun bir ağ arabirimi bulur ve arabirimin IP adresini kaynak adres olarak kullanır. Hedef IP adresi yayın veya çok noktaya yayın ise, ilk geçerli arabirim kullanılır. Uygulamalar bu durumda ***nx_ip_raw_packet_source_send*** kullanır.

Ham IPv6 paketini göndermek için uygulama, ***nxd_ip_raw_packet_send,** _ veya _ nxd_ip_raw_packet_source_send hizmetini kullanır *_._**

> [!WARNING]  
> *Bir hata döndürülmediği takdirde, uygulama bu çağrıdan sonra paketi serbest bırakmamalıdır. Bunu yapmak öngörülemeyen sonuçlara neden olur çünkü ağ sürücüsü iletim sonrasında paketi serbest bırakacaktır*.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **packet_ptr** Gönderilen ham IP paketinin işaretçisi.
- **destination_ip** Hedef IP adresi, belirli bir ana bilgisayar IP adresi, bir ağ yayını, iç geri döngü veya çok noktaya yayın adresi olabilir.
- **Type_of_service** İletim için hizmet türünü tanımlar, yasal değerler aşağıdaki gibidir:
    - **NX_IP_NORMAL** (0x00000000)
    - **NX_IP_MIN_DELAY** (0x00100000)
    - **NX_IP_MAX_DATA** (0x00080000)
    - **NX_IP_MAX_RELIABLE** (0x00040000)
    - **NX_IP_MIN_COST** (0x00020000)

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

No

### <a name="example"></a>Örnek

```c
/* Send a raw IP packet to IP address 1.2.3.5. */
status = nx_ip_raw_packet_send(&ip_0, packet_ptr,
                               IP_ADDRESS(1,2,3,5),
                               NX_IP_NORMAL);

/* If status is NX_SUCCESS, the raw IP packet pointed to by
   packet_ptr has been sent. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_source_send"></a>nx_ip_raw_packet_source_send
Belirtilen ağ arabirimi aracılığıyla ham IP paketi gönder

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_raw_packet_source_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    UINT address_index,
    ULONG type_of_service);
```
### <a name="description"></a>Description

Bu hizmet, kaynak adres olarak belirtilen yerel IPv4 adresini ve ilişkili ağ arabirimini kullanarak hedef IP adresine bir ham IP paketi gönderir. Bu yordamın hemen geri döndüğüne ve bu nedenle, IP paketinin gerçekten gönderildiyse bilinmediğini unutmayın. Ağ sürücüsü, iletim tamamlandığında paketin serbest bırakılmasından sorumlu olacaktır. Bu hizmet, paketin gerçekten gönderilip gönderilmediğini bilmenin bir yolu olmadığından diğer hizmetlerden farklıdır. Internet 'te kaybolabilir.

> [!CAUTION]  
> *Ham IP işlemenin etkin olması gerektiğini unutmayın*.

> [!WARNING]  
> Bu *hizmet **nx_ip_raw_packet_send benzerdir,** ancak bu hizmet, bir uygulamanın belirtilen fiziksel arabirimlerden ham IPv4 paketi göndermesini sağlar*.

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

No

### <a name="example"></a>Örnek

```c
#define ADDRESS_IDNEX 1

/* Send packet out on interface 1 with normal type of service. */
status = nx_ip_raw_packet_source_send(ip_ptr, packet_ptr,
                                      destination_ip,
                                      ADDRESS_INDEX,
                                      NX_IP_NORMAL);

/* If status is NX_SUCCESS the packet was successfully
   transmitted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_receive_queue_max_set"></a>nx_ip_raw_receive_queue_max_set
Maksimum ham alma kuyruğu boyutunu ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_raw_receive_queue_max_set(
    NX_IP *ip_ptr, 
    ULONG queue_max);
```
### <a name="description"></a>Description

Bu hizmet IP ham paket alma kuyruğu için en yüksek derinliği yapılandırıyor. IP ham paket alma kuyruğun hem IPv4 hem de IPv6 paketleriyle paylaşılır. Ham paket alma kuyruğu userconfigured maksimum derinliğe ulaştığında, yeni alınan ham paketler bırakılır. Varsayılan IP ham paketi alma kuyruğu derinliği 20'dir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **queue_max** Kuyruk boyutu için yeni değer

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Ham alma kuyruğu maksimum derinliği başarıyla ayarlanmadı
- **NX_PTR_ERROR** (0x07) Geçersiz IP denetim bloğu işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
ULONG queue_max = 10;

/* Set the maximum size of the IP raw packet receive queue. */
status = nx_ip_raw_receive_queue_max_set (&ip_0,
                                          queue_max);

/* If status == NX_SUCCESS, the maximum size of the IP raw packet
   receive queue was successfully set. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_static_route_add"></a>nx_ip_static_route_add
Yönlendirme tablosuna statik yol ekleme

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_static_route_add(
    NX_IP *ip_ptr,
    ULONG network_address,
    ULONG net_mask,
    ULONG next_hop);
```
### <a name="description"></a>Description

Bu hizmet statik yönlendirme tablosuna bir giriş ekler. Yerel ağ *next_hop* doğrudan erişilebilir olması gerektiğini unutmayın.

> [!CAUTION]  
> Bu ip_ptr geçerli bir NetX Duo IP yapısına işaret etmek gerektiğini ve NetX Duo kitaplığının bu hizmeti kullanmak için NX_ENABLE_IP_STATIC_ROUTING ile *birlikte oluşturması gerektiğini unutmayın. Varsayılan olarak NetX Duo, tanımlanmamış NX_ENABLE_IP_STATIC_ROUTING gelir.*

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **network_address** Konak byte sırasına göre hedef ağ adresi 
- **net_mask** Konak byte sırasına göre hedef ağ maskesi
- **next_hop** Hedef ağ için konak byte sırasına göre sonraki atlama adresi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Girişi statik yönlendirme tablosuna eklenir.
- **NX_OVERFLOW** (0x03) Statik yönlendirme tablosu dolu.
- **NX_NOT_SUPPORTED** (0x4B) Bu özellik içinde derlenmiş değildir.
- **NX_IP_ADDRESS_ERROR** (0x21) Sonraki atlamaya yerel arabirimler aracılığıyla doğrudan erişilemez.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_PTR_ERROR** (0x07) Geçersiz ip_ptr işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Specify the next hop for 192.168.1.68 through the gateway
   192.168.1.1. */
status = nx_ip_static_route_add(ip_ptr, IP_ADDRESS(192,168,1,0),
                                0xFFFFFF00UL,
                                IP_ADDRESS(192,168,1,1));

/* If status is NX_SUCCESS the route was successfully added to the
   static routing table. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_static_route_delete"></a>nx_ip_static_route_delete
Yönlendirme tablosundan statik yolu silme

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_static_route_delete(
    NX_IP *ip_ptr,
    ULONG network_address,
    ULONG net_mask);
```
### <a name="description"></a>Description

Bu hizmet, statik yönlendirme tablosundan bir girişi siler.

> [!WARNING]  
> Bu ip_ptr geçerli bir NetX Duo IP yapısına işaret etmek gerektiğini ve NetX Duo kitaplığının bu hizmeti kullanmak için NX_ENABLE_IP_STATIC_ROUTING ile *birlikte oluşturması gerektiğini unutmayın. Varsayılan olarak NetX Duo, tanımlanmamış NX_ENABLE_IP_STATIC_ROUTING gelir.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **network_address** Konak bayt sırasına göre hedef ağ adresi.
- **net_mask** Konak bayt sırasına göre hedef ağ maskesi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Statik yönlendirme tablosundan başarılı silme.
- **NX_NOT_SUCCESSFUL** (0x43) Girişi yönlendirme tablosunda bulunamıyor.
- **NX_NOT_SUPPORTED** (0x4B) Bu özellik içinde derlenmiş değildir.
- **NX_PTR_ERROR** (0x07) Geçersiz ip_ptr işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Remove the static route for 192.168.1.68 from the routing
   table.*/
status = nx_ip_static_route_delete(ip_ptr,
                                   IP_ADDRESS(192,168,1,0),
                                   0xFFFFFF00UL,);

/* If status is NX_SUCCESS the route was successfully removed from
   the static routing table. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_status_check"></a>nx_ip_status_check
Bir IP örneğinin durumunu denetleme

### <a name="prototype"></a>Prototype  

```c
UINT nx_ip_status_check(
    NX_IP *ip_ptr,
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir IP örneğinin birincil ağ arabiriminin belirtilen durumunu denetler ve isteğe bağlı olarak bekler. İkincil arabirimlerde durum almak için, uygulamalar hizmeti ***nx_ip_interface_status_check kullanacaktır.***

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **needed_status** Aşağıdaki gibi bit eşleme biçiminde tanımlanan IP durumu istendi:
  - **NX_IP_INITIALIZE_DONE** (0x0001)
  - **NX_IP_ADDRESS_RESOLVED** (0x0002)
  - **NX_IP_LINK_ENABLED** (0x0004)
  - **NX_IP_ARP_ENABLED** (0x0008)
  - **NX_IP_UDP_ENABLED** (0x0010)
  - **NX_IP_TCP_ENABLED** (0x0020)
  - **NX_IP_IGMP_ENABLED** (0x0040)
  - **NX_IP_RARP_COMPLETE** (0x0080)
  - **NX_IP_INTERFACE_LINK_ENABLED** (0x0100)
- **actual_status** Gerçek bitler kümesinin hedefi işaretçisi.
- **wait_option** İstenen durum bitleri yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **NX_NO_WAIT** 0x00000000)
  - **ticks içinde zaman aşımı değeri** (0x00000001-0xfffffffe)
  - **NX_WAIT_FOREVER** 0xFFFFFFFF

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) başarılı IP durum denetimi.
- **NX_NOT_SUCCESSFUL** (0x43) durum isteği belirtilen zaman aşımı süresi içinde karşılanmadı.
- **NX_PTR_ERROR** (0x07) IP işaretçisi veya geçersiz hale geldi ya da gerçek durum işaretçisi geçersiz.
- **NX_OPTION_ERROR** (0X0a) geçersiz gerekli durum seçeneği.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Wait 10 ticks for the link up status on the previously created IP
   instance. */
status = nx_ip_status_check(&ip_0, NX_IP_LINK_ENABLED,
                            &actual_status, 10);

/* If status is NX_SUCCESS, the link for the specified IP instance
   is up. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ipv4_multicast_interface_join"></a>nx_ipv4_multicast_interface_join
IP örneğini bir arabirim aracılığıyla belirtilen çok noktaya yayın grubuna ekleyin

### <a name="prototype"></a>Prototype  

```c
UINT nx_ipv4_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen ağ arabirimi aracılığıyla bir IP örneğini belirtilen çok noktaya yayın grubuna birleştirir. IP örneği bir çok noktaya yayın grubuna katıldığında, IP alma mantığı, çok noktaya yayın grubundaki veri paketlerini üst katmana iletmeyi başlatır. Bu hizmetin, ıGMP raporları göndermeden çok noktaya yayın grubunu birleştirdiğine unutmayın.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **group_address** Ana bilgisayar bayt düzeninde katılacak sınıf D IP çok noktaya yayın grubu adresi.
- **interface_index** NetX Duo örneğine iliştirilmiş arabirimin dizini.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı çok noktaya yayın grubu katılımı.
- **NX_NO_MORE_ENTRIES** (0x17) daha fazla çok noktaya yayın grubu birleştirilemez, en fazla sınır aşıldı.
- **NX_PTR_ERROR** (0x07) IP örneğine geçersiz IŞARETÇI veya IP örneği geçersiz
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_EANABLED** (0x14) ıGMP bu IP örneğinde etkin değil
- **NX_IP_ADDRESS_ERROR** (0x21) belirtilen çok noktaya yayın grubu adresi geçerli bir sınıf D adresi değil.
- **NX_INVALID_INTERFACE** (0x4C) cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Previously created IP Instance joins the multicast group
   224.0.0.200, via the interface at index 1 in the IP interface
   list. */
#define INTERFACE_INDEX 1
status = nx_ipv4_multicast_interface_join
                                 (&ip IP_ADDRESS(224,0,0,200),
                                  INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully joined
   the multicast group. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_ipv4_multicast_interface_leave"></a>nx_ipv4_multicast_interface_leave
Belirtilen çok noktaya yayın grubunu bir arabirim aracılığıyla bırakın

### <a name="prototype"></a>Prototype  

```c
UINT nx_ipv4_multicast_interface_leave(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen çok noktaya yayın grubunu belirtilen bir ağ arabirimi aracılığıyla bırakır. Gruptan ayrılarak, bu hizmet oluşturulan IGMP iletilerini tetiklemez.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **group_address** Ayrılılacak D IP çok noktaya yayın grubu adresi. IP adresi konak bayt sırasına göredir.
- **interface_index** NetX Duo örneğine eklenen Arabirimin dizini.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı çok noktaya yayın grubu birleştirme.
- **NX_ENTRY_NOT_FOUND** (0x16) Belirtilen çok noktaya yayın grubu adresi yerel çok noktaya yayın tablosunda bulunamıyor.
- **NX_INVALID_INTERFACE** (0x4C) Cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.
- **NX_IP_ADDRESS_ERROR** (0x21) Çok Noktaya Yayın grup adresi geçerli bir D sınıfı adres değildir.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_PTR_ERROR** (0x07) IP örneğine yönelik işaretçi geçersiz veya IP örneği geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Leave the multicast group 224.0.0.200. */
#define INTERFACE_INDEX 1
status = nx_ipv4_multicast_interface_leave
                                (&ip, IP_ADDRESS(224,0,0,200),
                                 INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully leaves
   the multicast group 244.0.0.200. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_packet_allocate"></a>nx_packet_allocate
Belirtilen havuzdan paket ayırma

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_allocate(
    NX_PACKET_POOL *pool_ptr,
    NX_PACKET **packet_ptr,
    ULONG packet_type,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen havuzdan bir paket ayırır ve pakette bulunan ön uç işaretçisini belirtilen paket türüne göre ayarlar. Paket yoksa, hizmet sağlanan bekleme seçeneğine göre askıya alır.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Daha önce oluşturulan paket havuzunun işaretçisi.
- **packet_ptr** Ayrılan paket İşaretçisi'nin İşaretçisi.
- **packet_type** İstenen paket türünü tanımlar. Desteklenen paket türlerinin listesi için Bölüm 3'te sayfa 63'te "Paket Havuzları" sayfasına bakın.
- **wait_option** Paket havuzunda kullanılabilir paket yoksa, bekleme süresi tıklar içinde tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
  - **NX_NO_WAIT** (0x00000000)
  - **NX_WAIT_FOREVER** (0xFFFFFFFF)
  - **tıklar içinde zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı paket ayırma.
- **NX_NO_PACKET** (0x01) Paket yok.
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma isteği, tx_thread_wait_abort.
- **NX_INVALID_PARAMETERS** (0x4D) Paket boyutu protokolü destekleyem yok.
- **NX_OPTION_ERROR** (0x0A) Geçersiz paket türü.
- **NX_PTR_ERROR** (0x07) Geçersiz havuz veya paket dönüş işaretçisi.
- **NX_CALLER_ERROR** (0x11) Okunmamış bekleme seçeneği.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları, sürelerdir ve ISR'ler (uygulama ağ sürücüleri). ISR'de *NX_NO_WAIT* zamanlayıcı bağlamında kullanılırken bekleme seçeneği kullanılabilir.

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Allocate a new UDP packet from the previously created packet pool
   and suspend for a maximum of 5 timer ticks if the pool is
   empty. */
status = nx_packet_allocate(&pool_0, &packet_ptr,
                            NX_UDP_PACKET, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is
   found in the variable packet_ptr. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_copy"></a>nx_packet_copy
Paket kopyalama

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_copy(
    NX_PACKET *packet_ptr,
    NX_PACKET **new_packet_ptr,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan pakette yer alan bilgileri sağlanan paket havuzundan ayrılan bir veya daha fazla yeni pakete kopyalar. Başarılı olursa, yeni paketin işaretçisi, hedef tarafından işaret eden **hedefte new_packet_ptr.**

### <a name="parameters"></a>Parametreler

- **packet_ptr** Kaynak paketin işaretçisi.
- **new_packet_ptr** Paketin yeni kopyasına işaretçinin getirilecek hedefin işaretçisi.
- **pool_ptr** Kopyalama için bir veya daha fazla paket ayırmak için kullanılan önceden oluşturulmuş paket havuzunun işaretçisi.
- **wait_option** Kullanılabilir paket yoksa hizmetin nasıl bekleyeceğini tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **tıklar içinde zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı paket kopyası.
- **NX_NO_PACKET** (0x01) Paketi kopyalanmaz.
- **NX_INVALID_PACKET** (0x12) Boş kaynak paket veya kopyalama başarısız oldu.
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma isteği, tx_thread_wait_abort.
- **NX_INVALID_PARAMETERS** (0x4D) Paket boyutu protokolü destekleyem yok.
- **NX_PTR_ERROR** (0x07) Geçersiz havuz, paket veya hedef işaretçi.
- **NX_UNDERFLOW** (0x02) Geçersiz paket ön uç işaretçisi.
- **NX_OVERFLOW** (0x03) geçersiz paket ekleme işaretçisi.
- **NX_CALLER_ERROR** (0x11) başlatma veya ISR içinde bir bekleme seçeneği belirtildi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
NX_PACKET *new_copy_ptr;

/* Copy packet pointed to by "old_packet_ptr" using packets from
   previously created packet pool_0. */
status = nx_packet_copy(old_packet, &new_copy_ptr, &pool_0, 20);

/* If status is NX_SUCCESS, new_copy_ptr points to the packet copy. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_data_append"></a>nx_packet_data_append
Paketi sonuna veri Ekle

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_data_append(
    NX_PACKET *packet_ptr,
    VOID *data_start, ULONG data_size,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, verileri belirtilen paketin sonuna ekler. Sağlanan veri alanı pakete kopyalanır. Yeterli kullanılabilir bellek yoksa ve zincirleme paket özelliği etkinse, isteği karşılamak için bir veya daha fazla paket ayrılır. Zincirleme paket özelliği etkinleştirilmemişse, *NX_SIZE_ERROR* döndürülür.

### <a name="parameters"></a>Parametreler

- **packet_ptr** Paket işaretçisi.
- **data_start** Pakete eklenecek kullanıcının veri alanının başlangıcına yönelik işaretçi.
- **data_size** Kullanıcının veri alanının boyutu.
- **pool_ptr** Geçerli pakette yeterli alan yoksa başka bir paketin ayırabileceği paket havuzu işaretçisi.
- **wait_option** Kullanılabilir bir paket yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xffffffff)
    - **ticks içinde zaman aşımı değeri** (0x00000001-0xfffffffe)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı paket ekleme.
- **NX_NO_PACKET** (0x01) kullanılabilir paket yok.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.
- **NX_UNDERFLOW** (0x02) Prepend işaretçisi yük başlangıcından daha küçüktür.
- **NX_OVERFLOW** (0x03) ekleme işaretçisi yük ucundan daha büyük.
- **NX_PTR_ERROR** (0x07) geçersiz havuz, paket veya veri işaretçisi.
- **NX_SIZE_ERROR** (0x09) geçersiz veri boyutu.
- **NX_CALLER_ERROR** (0x11) Iş parçacığından geçersiz bekleme seçeneği.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs (uygulama ağ sürücüleri)

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Append "abcd" to the specified packet. */
status = nx_packet_data_append(packet_ptr, "abcd", 4, &pool_0, 5);

/* If status is NX_SUCCESS, the additional four bytes "abcd" have
   been appended to the packet. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release


## <a name="nx_packet_data_extract_offset"></a>nx_packet_data_extract_offset
Bir sapmayı kullanarak paketten veri ayıklama

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_data_extract_offset(
    NX_PACKET *packet_ptr,
    ULONG offset,
    VOID *buffer_start,
    ULONG buffer_length,
    ULONG *bytes_copied);
```
### <a name="description"></a>Description

Bu hizmet bir NETX Duo paketinden (veya paket zincirinden), belirtilen boyutun belirtilen baytdaki paket önüne işaretçisinin belirtilen uzaklığında başlayarak verileri kopyalar. Gerçekten kopyalanmış olan bayt sayısı *bytes_copied döndürülür.* Bu hizmet, paketten verileri kaldırmaz veya önüne işaretçisini veya diğer iç durum bilgilerini ayarlar.

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

No

```c
/* Extract 10 bytes from the start of the received packet buffer
   into the specified memory area. */
status = nx_packet_data_extract_offset(my_packet, 0, &data[0], 10,
                                       &bytes_copied) ;
/* If status is NX_SUCCESS, 10 bytes were successfully copied into
   the data buffer. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_data_retrieve"></a>nx_packet_data_retrieve
Paketten veri al

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_data_retrieve(
    NX_PACKET *packet_ptr,
    VOID *buffer_start,
    ULONG *bytes_copied);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan paketten verileri sağlanan arabelleğe kopyalar. Hedef, **bytes_copied** tarafından işaret edilen hedefte döndürülen gerçek bayt sayısı.

Bu hizmetin paketin iç durumunu değiştirmediğini unutmayın. Alınmakta olan veriler pakette hala kullanılabilir durumda. 

> [!CAUTION]  
> *Hedef arabelleğinin paketin içeriğini tutabilecek kadar büyük olması gerekir. Aksi takdirde, bellek bozulması öngörülemeyen sonuçlara neden* olur.

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

No

### <a name="example"></a>Örnek

```c
UCHAR                 buffer[512];
ULONG                 bytes_copied;

/* Retrieve data from packet pointed to by "packet_ptr". */
status = nx_packet_data_retrieve(packet_ptr, buffer, &bytes_copied);

/* If status is NX_SUCCESS, buffer contains the contents of the
   packet, the size of which is contained in "bytes_copied." */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_length_get"></a>nx_packet_length_get
Paket verilerinin uzunluğunu al

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_length_get(
    NX_PACKET *packet_ptr, 
    ULONG *length);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen paketteki verilerin uzunluğunu alır.

### <a name="parameters"></a>Parametreler

- **packet_ptr** Pakete yönelik işaretçi.
- **uzunluk** Paket uzunluğu için hedef.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) başarılı paket uzunluğu Get.
- **NX_PTR_ERROR** (0x07) geçersiz paket işaretçisi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Get the length of the data in "my_packet." */
status = nx_packet_length_get(my_packet, &my_length);

/* If status is NX_SUCCESS, data length is in "my_length". */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_pool_create"></a>nx_packet_pool_create
Belirtilen bellek alanında paket havuzu oluştur

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_pool_create(
    NX_PACKET_POOL *pool_ptr,
    CHAR *name,
    ULONG payload_size,
    VOID *memory_ptr,
    ULONG memory_size);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Create a packet pool of 32000 bytes starting at physical
   address 0x10000000. */
status = nx_packet_pool_create(&pool_0, "Default Pool", 128,
                               (void *) 0x10000000, 32000);

/* If status is NX_SUCCESS, the packet pool has been successfully
   created. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_pool_delete"></a>nx_packet_pool_delete
Önceden oluşturulmuş paket havuzunu Sil

### <a name="prototype"></a>Prototype  

```c
UINT  nx_packet_pool_delete(NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a>Description

Bu hizmet daha önce oluşturulmuş bir paket havuzunu siler. NetX Duo, paket havuzundaki paketlerde Şu anda askıya alınmış olan her iş parçacığını denetler ve askıya alınma 'yi temizler.

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

```c
/* Delete a previously created packet pool. */
status = nx_packet_pool_delete(&pool_0);

/* If status is NX_SUCCESS, the packet pool has been successfully
   deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_pool_info_get"></a>nx_packet_pool_info_get
Bir paket havuzu hakkında bilgi alma

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_pool_info_get(
    NX_PACKET_POOL *pool_ptr,
    ULONG *total_packets,
    ULONG *free_packets,
    ULONG *empty_pool_requests,
    ULONG *empty_pool_suspensions,
    ULONG *invalid_packet_releases);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen paket havuzu hakkında bilgi alır.

> [!IMPORTANT]  
> *Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez*.

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

No

### <a name="example"></a>Örnek

```c
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

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_pool_low_watermark_set"></a>nx_packet_pool_low_watermark_set
Paket havuzu alt sınır ayarla

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_pool_low_watermark_set(
    NX_PACKET_POOL *pool_ptr,
    ULONG low_watermark);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen paket havuzu için düşük filigranı yapılandırır. Düşük filigran değeri ayarlandıktan sonra, paket havuzundaki kullanılabilir paketlerin sayısı paket havuzunun düşük filigranından azsa, paket havuzunun paketlerin tükenmesini engellemek için, TCP veya UDP alınan paketleri sıraya almamayacaktır. NetX Duo kitaplığı tanımlı ***NX_ENABLE_LOW_WATERMARK*** seçeneği ile derlenip bu hizmet kullanılabilir.

### <a name="parameters"></a>Parametreler

- **pool_ptr** Paket havuzu denetim bloğu işaretçisi.
- **low_watermark** Yapılandırılacak düşük eşik değeri

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) düşük eşik değerini başarıyla ayarladı.
- **NX_NOT_SUPPORTED** (0x4b) düşük filigran özelliği NETX Duo içinde yerleşik değildir.
- **NX_PTR_ERROR** (0x07) geçersiz havuz işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Set pool_0 low watermark value to 2. */
status = nx_packet_pool_create(&pool_0, 2);

/* If status is NX_SUCCESS, the low watermark value is set for
   pool_0.*/
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_release"></a>nx_packet_release
Önceden ayrılmış paketi serbest bırak

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_release(NX_PACKET *packet_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen pakete zincirleme ek paketler de dahil olmak üzere bir paket yayınlar. Paket ayırma üzerinde başka bir iş parçacığı engellenirse, paket verilir ve sürdürülür.

> [!NOTE]  
> *Uygulamanın, bir paketin birden çok kez serbest bırakılmasını önlemesi gerekir, çünkü bunu yapmak öngörülemeyen sonuçlara neden olur*.

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

```c
/* Release a previously allocated packet. */
status = nx_packet_release(packet_ptr);

/* If status is NX_SUCCESS, the packet has been returned to the
   packet pool it was allocated from. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_transmit_release

## <a name="nx_packet_transmit_release"></a>nx_packet_transmit_release
İletilen bir paketi serbest bırakma

### <a name="prototype"></a>Prototype  

```c
UINT nx_packet_transmit_release(NX_PACKET *packet_ptr);
```
### <a name="description"></a>Description

Bu hizmet, TCP olmayan paketler için, belirtilen pakete zincirleme ek paketler de dahil olmak üzere, iletilen bir paket yayınlar. Paket ayırma üzerinde başka bir iş parçacığı engellenirse, paket verilir ve sürdürülür. İletilen bir TCP paketi için paket aktarılmakta olarak işaretlenir ancak paket onaylanana kadar serbest bırakılmaz. Bu hizmet genellikle bir paket iletildikten sonra uygulamanın ağ sürücüsünden çağrılır.

> [!WARNING] 
> *Ağ sürücüsünün fiziksel medya üstbilgisini kaldırması ve bu hizmeti çağırmadan önce paketin uzunluğunu ayarlaması gerekir*.

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

```c
/* Release a previously allocated packet that was just transmitted
   from the application network driver. */
status = nx_packet_transmit_release(packet_ptr);

/* If status is NX_SUCCESS, the transmitted packet has been
   returned to the packet pool it was allocated from. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release

## <a name="nx_rarp_disable"></a>nx_rarp_disable
Ters adres çözümleme protokolünü devre dışı bırak (RARP)

### <a name="prototype"></a>Prototype  

```c
UINT nx_rarp_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Description

Bu hizmet, belirli IP örneği için NetX Duo 'un RARP bileşenini devre dışı bırakır. Bu hizmet, çok ana bir sistem için tüm arabirimlerde RARP 'yi devre dışı bırakır.

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

No

### <a name="example"></a>Örnek

```c
/* Disable RARP on the previously created IP instance. */
status = nx_rarp_disable(&ip_0);

/* If status is NX_SUCCESS, RARP is disabled. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_rarp_enable
- nx_rarp_info_get

## <a name="nx_rarp_enable"></a>nx_rarp_enable
Ters adres çözümleme protokolünü etkinleştir (RARP)

### <a name="prototype"></a>Prototype  

```c
UINT nx_rarp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirli IP örneği için NetX Duo 'un RARP bileşenini sunar. RARP bileşenleri, sıfır IP adresi için tüm bağlı ağ arabirimlerini arar. Sıfır IP adresi, arabirimin henüz IP adresi ataması olmadığını gösterir. RARP, bu arabirimde RARP işlemini etkinleştirerek IP adresini çözümlemeye çalışır.

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

No

### <a name="example"></a>Örnek

```c
/* Enable RARP on the previously created IP instance. */
status = nx_rarp_enable(&ip_0);

/* If status is NX_SUCCESS, RARP is enabled and is attempting to
   resolve this IP instance’s address by querying the network. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_rarp_disable
- nx_rarp_info_get

## <a name="nx_rarp_info_get"></a>nx_rarp_info_get
RARP etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype  

```c
UINT nx_rarp_info_get(
    NX_IP *ip_ptr,
    ULONG *rarp_requests_sent,
    ULONG *rarp_responses_received,
    ULONG *rarp_invalid_messages);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için RARP etkinlikleriyle ilgili bilgileri alır.

> [!IMPORTANT]  
> *Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez*.

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

No

### <a name="example"></a>Örnek

```c
/* Retrieve RARP information from previously created IP
   Instance 0. */
status = nx_rarp_info_get(&ip_0,
                          &rarp_requests_sent,
                          &rarp_responses_received,
                          &rarp_invalid_messages);

/* If status is NX_SUCCESS, RARP information was retrieved. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_rarp_disable
- nx_rarp_enable

## <a name="nx_system_initialize"></a>nx_system_initialize
NetX Duo sistemini Başlat

### <a name="prototype"></a>Prototype  

```c
VOID nx_system_initialize(VOID);
```
### <a name="description"></a>Description

Bu hizmet, kullanıma hazırlık aşamasında temel NetX Duo sistem kaynaklarını başlatır. Başlatma sırasında ve diğer NetX Duo çağrısı yapılmadan önce uygulama tarafından çağrılmalıdır.

### <a name="parameters"></a>Parametreler

Hiçbiri

### <a name="return-values"></a>Dönüş Değerleri

Hiçbiri

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları, zamanlayıcılar, ISRs

### <a name="preemption-possible"></a>Önalım mümkün

No

Sistem Yönetimi

### <a name="example"></a>Örnek

```c
/* Initialize NetX Duo for operation. */
nx_system_initialize();

/* At this point, NetX Duo is ready for IP creation and all
   subsequent network operations. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_tcp_client_socket_bind"></a>nx_tcp_client_socket_bind
İstemci TCP yuvasını TCP bağlantı noktasına bağlama

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_client_socket_bind(
    NX_TCP_SOCKET *socket_ptr,
    UINT port,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, önceden oluşturulan TCP istemci yuvasını belirtilen TCP bağlantı noktasına bağlar. Geçerli TCP Yuvaları 0 ile 0xFFFF arasındadır. Belirtilen TCP bağlantı noktası kullanılamıyorsa, hizmet sağlanan bekleme seçeneğine göre askıya alınır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.
- bağlanacak **bağlantı noktası bağlantı** noktası numarası (1 ile 0xFFFF arasında). Bağlantı noktası numarası NX_ANY_PORT (0x0000) ise, IP örneği bir sonraki boş bağlantı noktasını arar ve bu bağlantıyı bağlama için kullanır.
- **wait_option** Bağlantı noktası zaten başka bir yuvaya bağlanmışsa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
- **NX_NO_WAIT** (0x00000000)
- **NX_WAIT_FOREVER** (0xffffffff)
- **ticks içinde zaman aşımı değeri** (0x00000001-0xfffffffe)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlaması.
- **NX_ALREADY_BOUND** (0x22) bu yuva zaten başka bir TCP bağlantı noktasına bağlıydı.
- **NX_PORT_UNAVAILABLE** (0x23) bağlantı noktası zaten farklı bir yuvaya bağlıydı.
- **NX_NO_FREE_PORTS** (0x45) boş bağlantı noktası yok.
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.
- **NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Bind a previously created client socket to port 12 and wait for 7
   timer ticks for the bind to complete. */
status = nx_tcp_client_socket_bind(&client_socket, 12, 7);

/* If status is NX_SUCCESS, the previously created client_socket is
   bound to port 12 on the associated IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_client_socket_connect"></a>nx_tcp_client_socket_connect
Bağlan TCP yuvası

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_client_socket_connect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG server_ip,
    UINT server_port,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş ve bağlanan TCP istemci yuvalarını belirtilen sunucunun bağlantı noktasına bağlar. Geçerli TCP sunucusu bağlantı noktaları 0 ile 0xFFFF. Bağlantı hemen tamamlanmazsa, hizmet sağlanan bekleme seçeneğine göre askıya alır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuvası örneğinin işaretçisi.
- **server_ip** Sunucunun IP adresi.
- **server_port** Bağlanmak için sunucu bağlantı noktası numarası** (1 ile 0xFFFF).
- **wait_option** Bağlantı kurulurken hizmetin nasıl davrandığını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **tıklar içinde zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı yuva bağlantısı.
- **NX_NOT_BOUND** (0x24) Yuva bağlı değil.
- **NX_NOT_CLOSED** (0x35) Yuva kapalı durumda değil.
- **NX_IN_PROGRESS** (0x37) Bekleme belirtilmedi, bağlantı girişimi devam ediyor.
- **NX_INVALID_INTERFACE** (0x4C) Geçersiz arabirim sağlanmadı.
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma isteği, tx_thread_wait_abort.
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz sunucu IP adresi.
- **NX_INVALID_PORT** (0x46) Geçersiz bağlantı noktası.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Initiate a TCP connection from a previously created and bound
   client socket. The connection requested in this example is to
   port 12 on the server with the IP address of 1.2.3.5. This
   service will wait 300 timer ticks for the connection to take
   place before giving up. */
status = nx_tcp_client_socket_connect(&client_socket,
                                      IP_ADDRESS(1,2,3,5),
                                      12, 300);

/* If status is NX_SUCCESS, the previously created and bound
   client_socket is connected to port 12 on IP 1.2.3.5. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_client_socket_port_get"></a>nx_tcp_client_socket_port_get
İstemci TCP yuvasına bağlı bağlantı noktası numarasını al

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_client_socket_port_get(
    NX_TCP_SOCKET *socket_ptr,
    UINT *port_ptr);
```
### <a name="description"></a>Description

Bu hizmet, yuvayla ilişkilendirilmiş bağlantı noktası numarasını alan bu numara, yuvanın bağlı olduğu sırada NX_ANY_PORT NetX Duo tarafından ayrılan bağlantı noktasını bulmak için kullanışlıdır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuvası örneğinin işaretçisi.
- **port_ptr** Dönüş bağlantı noktası numarası için hedefin işaretçisi. Geçerli bağlantı noktası numaralarıdır (1 ile 0xFFFF).

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı yuva bağlaması.
- **NX_NOT_BOUND** (0x24) Bu yuva bir bağlantı noktasına bağlı değildir.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi veya bağlantı noktası dönüş işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Get the port number of previously created and bound client
   socket. */
status = nx_tcp_client_socket_port_get(&client_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
   socket is bound to. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_client_socket_unbind"></a>nx_tcp_client_socket_unbind
TCP bağlantı noktasından TCP istemci yuvasının bağlantısını kaldır

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_client_socket_unbind(NX_TCP_SOCKET *socket_ptr);
```
### <a name="description"></a>Description

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

```c
/* Unbind a previously created and bound client TCP socket. */
status = nx_tcp_client_socket_unbind(&client_socket);

/* If status is NX_SUCCESS, the client socket is no longer
   bound. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_enable"></a>nx_tcp_enable
NetX Duo 'un TCP bileşenini etkinleştir

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, NetX Duo 'un Iletim Denetim Protokolü (TCP) bileşenini sunar. Etkinleştirildikten sonra, uygulama tarafından TCP bağlantıları kurulabilir.

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

No

### <a name="example"></a>Örnek

```c
/* Enable TCP on a previously created IP instance ip_0. */
status = nx_tcp_enable(&ip_0);

/* If status is NX_SUCCESS, TCP is enabled on the IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_free_port_find"></a>nx_tcp_free_port_find
Sonraki kullanılabilir TCP bağlantı noktasını bul

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_free_port_find(
    NX_IP *ip_ptr,
    UINT port,
    UINT *free_port_ptr);
```
### <a name="description"></a>Description

Bu hizmet, uygulama tarafından sağlanan bağlantı noktasından başlayarak ücretsiz bir TCP bağlantı noktasını (ilişkisiz) bulmaya çalışır. Arama mantığı, en fazla 0xFFFF bağlantı noktası değerine ulaşmak için arama gerçekleşeceği gibi kaydırılır. Arama başarılı olursa, *free_port_ptr* tarafından işaret edilen değişkende boş bağlantı noktası döndürülür.

> [!WARNING]  
> *Bu hizmet başka bir iş parçacığından çağrılabilir ve aynı bağlantı noktasına sahip olabilir. Bu yarış durumunu engellemek için, uygulama bu hizmeti ve gerçek istemci yuvasını bir mutex 'in koruması altına yerleştirmek isteyebilir*.

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

No

### <a name="example"></a>Örnek

```c
/* Locate a free TCP port, starting at port 12, on a previously
   created IP instance. */
status = nx_tcp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS, "free_port" contains the next free port
   on the IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_info_get"></a>nx_tcp_info_get
TCP etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype  

```c
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
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için TCP etkinlikleri hakkında bilgi alır.

> [!IMPORTANT]  
> *Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez*.

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

No

### <a name="example"></a>Örnek

```c
/* Retrieve TCP information from previously created IP Instance
   ip_0. */
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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_accept"></a>nx_tcp_server_socket_accept
TCP bağlantısını kabul etme

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_server_socket_accept(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, daha önce dinleme için ayarlanmış bir bağlantı noktası için bir TCP istemci yuvası bağlantı isteğini kabul eder (veya kabul etmeye hazırlar). Bu hizmet, uygulama dinleme veya yeniden dinleme hizmetini çağıran hemen sonra veya istemci bağlantısı gerçekten mevcut olduğunda dinleme geri çağırma yordamı çağrıldıktan sonra çağrılmalıdır. Bağlantı hemen kurulamazsa, hizmet sağlanan bekleme seçeneğine göre askıya alır.

> [!WARNING]  
> *Sunucu yuvasının **sunucu nx_tcp_server_socket_unaccept** bağlantısını kaldırmak* için bağlantı artık gerekli olmadığı için uygulamanın çağrısı nx_tcp_server_socket_unaccept gerekir.

> [!IMPORTANT]  
> *Uygulama geri çağırma yordamları, IP'nin yardımcı iş parçacığından çağrılır.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** TCP sunucusu yuva denetim bloğuna işaretçi.
- **wait_option** Bağlantı kurulurken hizmetin nasıl davrandığını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **tıklar içinde zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı TCP sunucu yuvası kabul (pasif bağlantı).
- **NX_NOT_LISTEN_STATE** (0x36) Sağlanan sunucu yuvası dinleme durumda değil.
- **NX_IN_PROGRESS** (0x37) Bekleme belirtilmedi, bağlantı girişimi devam ediyor.
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma isteği, tx_thread_wait_abort.
- **NX_PTR_ERROR** (0x07) Yuva işaretçisi hatası.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
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
        created
    */

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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_listen"></a>nx_tcp_server_socket_listen
TCP bağlantı noktası üzerinden istemci bağlantısını dinlemeyi etkinleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_server_socket_listen(
    NX_IP *ip_ptr, UINT port,
    NX_TCP_SOCKET *socket_ptr,
    UINT listen_queue_size,
    VOID (*listen_callback)(NX_TCP_SOCKET *socket_ptr, UINT port));
```
### <a name="description"></a>Description

Bu hizmet, belirtilen TCP bağlantı noktası üzerinde bir istemci bağlantı isteğini dinlemeyi sağlar. Bir istemci bağlantı isteği alınca, sağlanan sunucu yuvası belirtilen bağlantı noktasına bağlı olur ve sağlanan dinleme geri çağırma işlevi çağrılır.

Dinleme geri çağırma yordamının işlemesi tamamen uygulamaya göredir. Daha sonra kabul etme işlemi gerçekleştiren bir uygulama iş parçacığını uyandırma mantığı içerebilir. Uygulamanın bu yuva için kabul işleme sırasında askıya alınmış bir iş parçacığı zaten varsa, dinleme geri çağırma yordamı gerekli olabilir.

Uygulama aynı bağlantı noktası üzerinde ek istemci bağlantılarını işlemek isterse, ***nx_tcp_server_socket_relisten*** sonraki bağlantı için kullanılabilir bir yuvayla (KAPALI durumdaki bir yuva) çağrılmış olması gerekir. Yeniden dinleme hizmeti çağrılana kadar ek istemci bağlantıları kuyruğa eklenir. En yüksek kuyruk derinliği aşılırsa, en eski bağlantı isteği yeni bağlantı isteğini kuyruğa alma tercihi ile bırakılır. En yüksek kuyruk derinliği bu hizmet tarafından belirtilir.

> [!IMPORTANT]  
> *Uygulama geri çağırma yordamları iç IP yardımcı iş parçacığından çağrılır.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **bağlantı noktası** Dinleme için bağlantı noktası numarası (1 ile 0xFFFF).
- **socket_ptr** Bağlantı için kullanmak üzere yuva işaretçisi.
- **listen_queue_size** Kuyruğa alınan istemci bağlantısı isteklerinin sayısı.
- **listen_callback** Bağlantı alınca çağıran uygulama işlevi. NULL belirtilirse, dinleme geri çağırma özelliği devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı TCP bağlantı noktası dinleme etkinleştirmesi.
- **NX_MAX_LISTEN** (0x33) Artık dinleme isteği yapısı yok. **_nx_api.h_** NX_MAX_LISTEN_REQUESTS sabiti kaç etkin dinleme isteğinin mümkün olduğunu tanımlar.
- **NX_NOT_CLOSED** (0x35) Sağlanan sunucu yuvası kapalı durumda değil.
- **NX_ALREADY_BOUND** (0x22) Sağlanan sunucu yuvası zaten bir bağlantı noktasına bağlı.
- **NX_DUPLICATE_LISTEN** (0x34) Bu bağlantı noktası için zaten etkin bir dinleme isteği var.
- **NX_INVALID_PORT** (0x46) Geçersiz bağlantı noktası belirtildi.
- **NX_PTR_ERROR** (0x07) Geçersiz IP veya yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
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
}
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_relisten"></a>nx_tcp_server_socket_relisten
TCP bağlantı noktasındaki istemci bağlantısını yeniden dinle

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_server_socket_relisten(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr);
```
### <a name="description"></a>Description

Bu hizmet, daha önce dinlemek üzere ayarlanan bir bağlantı noktasında bir bağlantı alındıktan sonra çağrılır. Bu hizmetin ana amacı, sonraki istemci bağlantısı için yeni bir sunucu yuvası sağlamaktır. Bir bağlantı isteği sıraya alınmışsa, bu hizmet çağrısı sırasında bağlantı hemen işlenir.

> [!IMPORTANT]  
> *Özgün dinleme isteği tarafından belirtilen geri arama yordamı, bu yeni sunucu yuvası için bir bağlantı olduğunda da çağırılır*.

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

No

### <a name="example"></a>Örnek

```c
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
   nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server Socket",
                                 NX_IP_NORMAL, NX_FRAGMENT_OKAY,
                                 NX_IP_TIME_TO_LIVE, 100,
                                 NX_NULL, port_12_disconnect_request);

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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_unaccept"></a>nx_tcp_server_socket_unaccept
Yuva ilişkilendirmesini dinleme bağlantı noktasıyla kaldır

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_server_socket_unaccept(NX_TCP_SOCKET *socket_ptr);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
NX_PACKET_POOL        my_pool;
NX_IP                 my_ip;
NX_TCP_SOCKET         server_socket;
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

NX_PACKET  *my_packet;
UINT       status, i;

   /* Assuming that:
     "port_12_semaphore" has already been created with an initial count
      of 0 "my_ip" has already been created and the link is enabled
     "my_pool" packet pool has already been created
   */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server
                         Socket",NX_IP_NORMAL, NX_FRAGMENT_OKAY,
                         NX_IP_TIME_TO_LIVE, 100,NX_NULL,
                         port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
                                port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye"
       to
       each client and then disconnecting. */
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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_unlisten"></a>nx_tcp_server_socket_unlisten
TCP bağlantı noktasındaki istemci bağlantısını dinlemeyi devre dışı bırak

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_server_socket_unlisten(
    NX_IP *ip_ptr, 
    UINT port);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
NX_PACKET_POOL       my_pool;
NX_IP                my_ip;
NX_TCP_SOCKET        server_socket;

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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_bytes_available"></a>nx_tcp_socket_bytes_available
Alma için kullanılabilir bayt sayısını alır

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_bytes_available(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Get the bytes available for retrieval on the specified socket. */
status = nx_tcp_socket_bytes_available(&my_socket,&bytes_available);

/* Is status = NX_SUCCESS, the available bytes is returned in
   bytes_available. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_create"></a>nx_tcp_socket_create
TCP istemcisi veya sunucu yuvası oluşturma

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_create(
    NX_IP *ip_ptr, 
    NX_TCP_SOCKET *socket_ptr,
    CHAR *name, 
    ULONG type_of_service, 
    ULONG fragment,
    UINT time_to_live, 
    ULONG window_size,
    VOID (*urgent_data_callback)(NX_TCP_SOCKET *socket_ptr),
    VOID (*disconnect_callback)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için bir TCP istemcisi veya sunucu yuvası oluşturur.

> [!NOTE]  
> *Uygulama geri çağırma yordamları, bu IP örneğiyle ilişkili iş parçacığından çağrılır.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **socket_ptr** Yeni TCP yuva denetim bloğuna işaretçi.
- **name** Bu TCP yuvası için uygulama adı.
- **type_of_service** İletim için hizmet türünü tanımlar, yasal değerler aşağıdaki gibidir:
    - **NX_IP_NORMAL** (0x00000000)
    - **NX_IP_MIN_DELAY** (0x00100000)
    - **NX_IP_MAX_DATA** (0x00080000)
    - **NX_IP_MAX_RELIABLE** (0x00040000)
    - **NX_IP_MIN_COST** (0x00020000)
- **parça** IP parçalanmasına izin verili olup olmadığını belirtir. Ip NX_FRAGMENT_OKAY** (0x0) belirtilirse IP parçalanmasına izin verilir. Ip NX_DONT_FRAGMENT (0x4000) belirtilirse IP parçalanması devre dışı bırakılır.
- **time_to_live** Bu paketin atmadan önce kaç yönlendirici geçeceği tanımlayan 8 bit değerini belirtir. Varsayılan değer, varsayılan değer NX_IP_TIME_TO_LIVE.
- **window_size** Bu yuva için alma kuyruğunda izin verilen en fazla bayt sayısını tanımlar
- **urgent_data_callback** Alma akışında acil veriler algılandığında çağrılması gereken uygulama işlevi. Bu değer önemli NX_NULL acil veriler yoksayılır.
- **disconnect_callback** Bağlantının diğer ucundaki yuva tarafından her bağlantı kesisinde çağrılır uygulama işlevi. Bu değer bir NX_NULL kesme geri çağırma işlevi devre dışı bırakılır.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı TCP istemci yuvası oluşturma.
- **NX_OPTION_ERROR** (0x0A) Geçersiz hizmet türü, parça, geçersiz pencere boyutu veya yaşam süresi seçeneği.
- **NX_PTR_ERROR** (0x07) Geçersiz IP veya yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma ve İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_delete"></a>nx_tcp_socket_delete
TCP yuvayı silme

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_delete(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir TCP yuvayı siler. Yuva hala bağlı veya bağlı ise hizmet bir hata kodu döndürür.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuvası

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı yuva silme.
- **NX_NOT_CREATED** (0x27) Yuvası oluşturulmadı.
- **NX_STILL_BOUND** (0x42) Yuva hala bağlı.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Delete a previously created TCP client socket. */
status = nx_tcp_socket_delete(&client_socket);

/* If status is NX_SUCCESS, the client socket is deleted. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_disconnect"></a>nx_tcp_socket_disconnect
İstemci ve sunucu yuvası bağlantılarının bağlantısını kesme

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_disconnect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, kurulmuş bir istemci veya sunucu yuvası bağlantısını keser. Sunucu yuvası bağlantısının kesilmesini kabul etmeyen bir istek izlenirken bağlantısı kesilmiş bir istemci yuvası başka bir bağlantı isteği için hazır durumda bıraktır. Bağlantı kesme işlemi hemen tamamlanamazsa, hizmet sağlanan bekleme seçeneğine göre askıya alır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı istemci veya sunucu yuvası örneğinin işaretçisi.
- **wait_option** Bağlantı kesme devam ederken hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **tıklar içinde zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Yuva bağlantısının kesilmesi.
- **NX_NOT_CONNECTED** (0x38) Belirtilen yuva bağlı değil.
- **NX_IN_PROGRESS** (0x37) Bağlantı kesiliyor, bekleme belirtilmemiş.
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma isteği, tx_thread_wait_abort.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

Yes 

### <a name="example"></a>Örnek 

```c
/* Disconnect from a previously established connection and wait a
   maximum of 400 timer ticks. */
status = nx_tcp_socket_disconnect(&client_socket, 400);

/* If status is NX_SUCCESS, the previously connected socket (either
   as a result of the client socket connect or the server accept) is
   disconnected. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_disconnect_complete_notify"></a>nx_tcp_socket_disconnect_complete_notify
TCP bağlantısının kesilmesi tamamlandı bildirimi geri çağırma işlevini yükleme
 
### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_disconnect_complete_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_disconnect_complete_notify)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Description

Bu hizmet, yuva bağlantısını kesme işlemi tamamlandıktan sonra çağrılan bir geri çağırma işlevini kaydedmektedir. NetX Duo tanımlandığı gibi bir seçenekle inşa edildiyseniz TCP yuvası tam geri çağırma ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** kullanılabilir.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı istemci veya sunucu yuvası örneğinin işaretçisi.
- **tcp_disconnect_complete_notify** Yüklenmek için geri çağırma işlevi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Geri çağırma işlevini başarıyla kaydetti.
- **NX_NOT_SUPPORTED** (0x4B) Genişletilmiş bildirim özelliği NetX Duo kitaplığında yerleşik değil NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Install the disconnect complete notify callback function. */
status = nx_tcp_socket_disconnect_complete_notify(&client_socket,
                                                  callback);
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_setnx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_establish_notify"></a>nx_tcp_socket_establish_notify
TCP kurma notify callback işlevini ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_establish_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_establish_notify)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Description

Bu hizmet, TCP yuvası bağlantı verdikten sonra çağrılan bir geri çağırma işlevini kaydedmektedir. NetX Duo, tanımlandığı gibi bir seçenekle NX_ENABLE_EXTENDED_NOTIFY_SUPPORT ***kullanılabilir.***

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı istemci veya sunucu yuvası örneğinin işaretçisi.
- **tcp_establish_notify** TCP bağlantısı kurulduktan sonra çağrılan geri çağırma işlevi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) notify işlevini başarıyla ayarlar.
- **NX_NOT_SUPPORTED** (0x4B) Genişletilmiş bildirim özelliği NetX Duo kitaplığında yerleşik değil 
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) TCP uygulama tarafından etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Set the function pointer "callback" as the notify function NetX
   Duo will call when the connection is in the established state. */
status = nx_tcp_socket_establish_notify(&client_socket, callback);
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_info_get"></a>nx_tcp_socket_info_get
TCP yuva etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype  

```c
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
### <a name="description"></a>Description

Bu hizmet, belirtilen TCP yuvası örneği için TCP yuva etkinlikleri hakkında bilgi alır.

> [!NOTE]  
> *Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez*.

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

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Retrieve TCP socket information from previously created
   socket_0.*/
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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_mss_get"></a>nx_tcp_socket_mss_get
Yuvanın düzeyini al

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_mss_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Get the MSS for the socket "my_socket". */
status = nx_tcp_socket_mss_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
   socket's current MSS value. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_mss_peer_get"></a>nx_tcp_socket_mss_peer_get
Eş TCP yuvasının MSS'sini al

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_mss_peer_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *mss);
```
### <a name="description"></a>Description

Bu hizmet, eş yuva tarafından tanıt edilen En Büyük Kesim Boyutunu (MSS) alıyor.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan ve bağlı yuvanın işaretçisi.
- **mss** MSS'nin iade hedefi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı eş MSS get.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva veya MSS hedef işaretçisi.
- **NX_NOT_ENABLED** (0x14) TCP etkin değil.
- **NX_CALLER_ERROR** (0x11) Çağıran bir iş parçacığı veya başlatma değildir.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Get the MSS of the connected peer to the socket "my_socket". */
status = nx_tcp_socket_mss_peer_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
   socket peer’s advertised MSS value. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_mss_set"></a>nx_tcp_socket_mss_set
Yuvanın MSS'lerini ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_mss_set(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG mss);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen yuvanın En Büyük Kesim Boyutunu (MSS) ayarlar. MSS değerinin IP ve TCP üst bilgilerine yer sağlayan ağ arabirimi IP MTU'suna sahip olması gerektiğini unutmayın.

Tcp yuvası bağlantı işlemini başlamadan önce bu hizmet kullanılmalıdır. Tcp bağlantısı kurulduktan sonra hizmet kullanılırsa, yeni değerin bağlantı üzerinde hiçbir etkisi olmaz.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan yuvanın işaretçisi.
- **mss** Ayar için MSS değeri.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı MSS kümesi.
- **NX_SIZE_ERROR** (0x09) Belirtilen MSS değeri çok büyük.
- **NX_NOT_CONNECTED** (0x38) TCP bağlantısı kurulmamış 
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_NOT_ENABLED** (0x14) TCP etkin değil.
- **NX_CALLER_ERROR** (0x11) Çağıran bir iş parçacığı veya başlatma değildir.

### <a name="allowed-from"></a>İzin Verilen

Başlatma ve iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Set the MSS of the socket "my_socket" to 1000 bytes. */
status = nx_tcp_socket_mss_set(&my_socket, 1000);

/* If status is NX_SUCCESS, the MSS of "my_socket" is 1000 bytes. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_peer_info_get"></a>nx_tcp_socket_peer_info_get
Eş TCP yuvası hakkında bilgi alma

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_peer_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *peer_ip_address,
    ULONG *peer_port);
```
### <a name="description"></a>Description

Bu hizmet, IPv4 ağı üzerinden bağlı TCP yuvası için eş IP adresi ve bağlantı noktası bilgilerini verir. IPv6 ağına da destek olan eşdeğer hizmet ***nxd_tcp_socket_peer_info_get.***

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuvasının işaretçisi.
- **peer_ip_address** Eş IP adresi için hedef işaretçisi, konak bayt sırasına göre.
- **peer_port** Eş bağlantı noktası numarası için hedef işaretçisi, konak bayt sırasına göre.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Hizmeti başarıyla yürütülür. Çağrıyı yapana eş IP adresi ve bağlantı noktası numarası döndürülür.
- **NX_NOT_CONNECTED** (0x38) Yuva bağlı durumda değil.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçiler.
- **NX_NOT_ENABLED** (0x14) TCP etkin değil.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Obtain peer IP address and port on the specified TCP socket. */
status = nx_tcp_socket_peer_info_get(&my_socket, &peer_ip_address,
                                     &peer_port);

/* If status = NX_SUCCESS, the data was successfully obtained. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_queue_depth_notify_set"></a>nx_tcp_socket_queue_depth_notify_set
TCP iletme sırası bildirim işlevini ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_queue_depth_notify_set(
              NX_TCP_SOCKET *socket_ptr,
              VOID(*tcp_socket_queue_depth_notify)(NX_TCP_SOCKET *));
```
### <a name="description"></a>Description

Bu hizmet, uygulama tarafından belirtilen iletim sırası derinliği güncelleştirme bildirim işlevini ayarlar ve bu, belirtilen yuva, sıra derinliğinin artık sınırını aşmaması gibi, iletim sırasından paket yayımladığını belirlediğinde çağrılır. Sıra derinliği nedeniyle bir uygulama aktarım sırasında engelleniyorsa, geri çağırma işlevi uygulamaya yeniden iletim başlayabileceği bir bildirim görevi görür. Bu hizmet yalnızca NetX Duo kitaplığı tanımlı ***NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY*** seçeneği ile derlenip kullanılabilir.

### <a name="parameters"></a>Parametreler 

- **socket_ptr** Yuva yapısına yönelik işaretçi 
- **tcp_socket_queue_depth_notify** Yüklenecek bildirim işlevi

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00), bildirim işlevini başarıyla yükledi
- **NX_NOT_SUPPORTED** (0x4b) TCP yuva kuyruğu derinlik bildirimi özelliği NETX Duo kitaplığında yerleşik değildir
- **NX_PTR_ERROR** (0x07) yuva denetim bloğu veya bildirim Işlevi için geçersiz işaretçi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
VOID tcp_socket_queue_depth_notify(NX_TCP_SOCKET *socket_ptr)
{
   /* Notify the application to resume sending. */

}
/* Install the TCP transmit queue notify function .*/
status = nxd_tcp_socket_queue_depth_notify_set(&tcp_socket,
                                  tcp_socket_queue_depth_notify);

/* If status == NX_SUCCESS, the callback function is successfully
   installed. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_receive"></a>nx_tcp_socket_receive
TCP yuvasından veri al

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_receive(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen yuvadan TCP verileri alır. Belirtilen yuvada hiçbir veri sıraya alınmaz, çağıran, sağlanan bekleme seçeneğine göre askıya alır.

> [!CAUTION]  
> *NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur*.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.
- **packet_ptr** TCP paket işaretçisine yönelik işaretçi.
- **wait_option** Şu anda bu yuvada sıraya alınmış veriler varsa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xffffffff)
    - **ticks içinde zaman aşımı değeri** (0x00000001-0xfffffffe)

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

No

### <a name="example"></a>Örnek

```c
/* Receive a packet from the previously created and connected TCP
   client socket. If no packet is available, wait for 200 timer
   ticks before giving up. */
status = nx_tcp_socket_receive(&client_socket, &packet_ptr, 200);

/* If status is NX_SUCCESS, the received packet is pointed to by
   "packet_ptr". */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_receive_notify"></a>nx_tcp_socket_receive_notify
Alınan paketlerin uygulamasına bildirme

### <a name="prototype"></a>Prototype   

```c
UINT nx_tcp_socket_receive_notify(
    NX_TCP_SOCKET *socket_ptr, 
    VOID (*tcp_receive_notify)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Description 

Bu hizmet, bildirim al işlev işaretçisini uygulama tarafından belirtilen geri çağırma işleviyle yapılandırır. Bu geri çağırma işlevi, daha sonra yuvada bir veya daha fazla paket alındığında çağrılır. NX_NULL bir işaretçi sağlanırsa, bildir işlevi devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** TCP yuvasına yönelik işaretçi.
- **tcp_receive_notify** Yuvada bir veya daha fazla paket alındığında çağrılan uygulama geri çağırma işlev işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) başarılı yuva alma bildirimi.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Setup a receive packet callback function for the "client_socket"
   socket. */
status = nx_tcp_socket_receive_notify(&client_socket,
                                      my_receive_notify);

/* If status is NX_SUCCESS, NetX Duo will call the function named
   "my_receive_notify" whenever one or more packets are received for
   "client_socket". */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_send"></a>nx_tcp_socket_send
TCP yuvası üzerinden veri gönderme

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_send(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, TCP verilerini daha önce bağlı bir TCP yuvası üzerinden gönderir. Alıcının son tanıtan pencere boyutu bu istekten küçükse, hizmet belirtilen bekleme seçeneğine göre isteğe bağlı olarak askıya alır. Bu hizmet, IP katmanına MSS'den büyük hiçbir paket verisi gönderilmez. 

> [!WARNING]  
> *Bir hata döndürül olmadığı sürece, uygulama bu çağrıdan sonra paketi serbest bırakmamalı. Bunu yapmak öngörülemeyen sonuçlara neden olur çünkü ağ sürücüsü de iletimden sonra paketi serbest bırakmayı dener.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı olan TCP yuva örneğinin işaretçisi.
- **packet_ptr** TCP veri paketi işaretçisi.
- **wait_option** İstek, alıcının pencere boyutundan büyükse hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **tıklar içinde zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı yuva gönderme.
- **NX_NOT_BOUND** (0x24) Yuva hiçbir bağlantı noktasına bağlı değil.
- **NX_NO_INTERFACE_ADDRESS** (0x50) Uygun giden arabirim bulunamadı.
- **NX_NOT_CONNECTED** (0x38) Yuva artık bağlı değil.
- **NX_WINDOW_OVERFLOW** (0x39) İsteği, alıcının tanıtmış olduğu pencere boyutundan bayt cinsinden büyüktür.
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma isteği, tx_thread_wait_abort.
- **NX_INVALID_PACKET** (0x12) Paketi ayrılır.
- **NX_TX_QUEUE_DEPTH** (0x49) En yüksek aktarım kuyruğu derinliğine ulaşıldı.
- **NX_OVERFLOW** (0x03) Paket ekleme işaretçisi geçersiz.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.
- **NX_UNDERFLOW** (0x02) Paket ön uç işaretçisi geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Send a packet out on the previously created and connected TCP
   socket. If the receive window on the other side of the connection
   is less than the packet size, wait 200 timer ticks before giving
   up. */
status = nx_tcp_socket_send(&client_socket, packet_ptr, 200);

/* If status is NX_SUCCESS, the packet has been sent! */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_state_wait"></a>nx_tcp_socket_state_wait
TCP yuvasının belirli bir durumu girmesini bekleyin

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_state_wait(
    NX_TCP_SOCKET *socket_ptr,
    UINT desired_state,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, yuvanın istenen durumu girmelerini bekler. Yuva istenen durumda yoksa, hizmet sağlanan bekleme seçeneğine göre askıya alır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı olan TCP yuva örneğinin işaretçisi.
- **desired_state** İstenen TCP durumu. Geçerli TCP yuva durumları aşağıdaki gibi tanımlanır:
    - **NX_TCP_CLOSED** (0x01)
    - **NX_TCP_LISTEN_STATE** (0x02)
    - **NX_TCP_SYN_SENT** (0x03)
    - **NX_TCP_SYN_RECEIVED** (0x04)
    - **NX_TCP_ESTABLISHED** (0x05)
    - **NX_TCP_CLOSE_WAIT** (0x06)
    - **NX_TCP_FIN_WAIT_1** (0x07)
    - **NX_TCP_FIN_WAIT_2** (0x08)
    - **NX_TCP_CLOSING** (0x09)
    - **NX_TCP_TIMED_WAIT** (0x0A)
    - **NX_TCP_LAST_ACK** (0x0B)
- **wait_option** İstenen durum yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - Tick (0x00000001 ile 0xFFFFFFFF) **zaman aşımı değeri**

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

No

### <a name="example"></a>Örnek

```c
/* Wait 300 timer ticks for the previously created socket to enter
   the established state in the TCP state machine. */
status = nx_tcp_socket_state_wait(&client_socket,
                                  NX_TCP_ESTABLISHED, 300);

/* If status is NX_SUCCESS, the socket is now in the established
   state! */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_timed_wait_callback"></a>nx_tcp_socket_timed_wait_callback
Zamanlanmış bekleme durumu için geri çağırma 'yi yükler

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_timed_wait_callback(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_timed_wait_callback)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Description

Bu hizmet, TCP yuvası zamanlanmış bekleme durumunda olduğunda çağrılan bir geri arama işlevini kaydeder. Bu hizmeti kullanmak için NetX Duo kitaplığı tanımlı ***NX_ENABLE_EXTENDED_NOTIFY*** seçeneği ile oluşturulmalıdır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce bağlı olan istemci veya sunucu yuvası örneği işaretçisi.
- **tcp_timed_wait_callback** Zamanlanmış geri çağırma işlevi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) geri çağırma Işlevi yuvasını başarıyla kaydeder
- **NX_NOT_SUPPORTED** (0x4b) NETX Duo kitaplığı, genişletilmiş bildirim özelliği etkin olmadan oluşturulmuştur.
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Install the timed wait callback function */
nx_tcp_socket_timed_wait_callback(&client_socket, callback);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_transmit_configure"></a>nx_tcp_socket_transmit_configure
Yuvanın iletim parametrelerini Yapılandır

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_transmit_configure(
    NX_TCP_SOCKET *socket_ptr,
    ULONG max_queue_depth,
    ULONG timeout,
    ULONG max_retries,
    ULONG timeout_shift);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Configure the "client_socket" for a maximum transmit queue depth of
   12, 100 tick timeouts, a maximum of 20 retries, and a timeout double
   on each successive retry. */
status = nx_tcp_socket_transmit_configure(&client_socket,12,100,20,1);

/* If status is NX_SUCCESS, the socket’s transmit retry has been
   configured. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_window_update_notify_set"></a>nx_tcp_socket_window_update_notify_set
Pencere boyutu güncelleştirmelerini uygulamaya bildirme

### <a name="prototype"></a>Prototype  

```c
UINT nx_tcp_socket_window_update_notify_set(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_window_update_notify)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Description

Bu hizmet bir yuva penceresi güncelleştirme geri çağırma yordamını yüklür. Belirtilen yuva uzak ana bilgisayarın pencere boyutunda artış gösteren bir paket aldığında bu yordam otomatik olarak çağrılır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuvasının işaretçisi.
- **tcp_window_update_notify** Pencere boyutu değişirken çağrılmış geri çağırma yordamı. NULL değeri, pencere değişikliği güncelleştirmesini devre dışı bırakıyor.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Geri çağırma yordamı yuvaya yüklenir.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçiler.
- **NX_NOT_ENABLED** (0x14) TCP özelliği etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Set the function pointer to the windows update callback after creating the
   socket. */
status = nx_tcp_socket_window_update_notify_set(&data_socket,
                                                my_windows_update_callback);

/* Define the window callback function in the host application. */
void my_windows_update_callback(&data_socket)
{

/* Process update on increase TCP transmit socket window size. */
   return;
}
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure

## <a name="nx_udp_enable"></a>nx_udp_enable
NetX Duo'da UDP bileşenini etkinleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, NetX Duo'nın Kullanıcı Veri Birimi Protokolü (UDP) bileşenini sağlar. Etkinleştirildikten sonra, UDP veri birimleri uygulama tarafından gönderilebilir ve alınabilirsiniz.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) UDP etkinleştirmesi.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_ALREADY_ENABLED** (0x15) Bu bileşen zaten etkinleştirilmiştir.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları, süreerler

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Enable UDP on the previously created IP instance. */
status = nx_udp_enable(&ip_0);

/* If status is NX_SUCCESS, UDP is now enabled on the specified IP
   instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_free_port_find"></a>nx_udp_free_port_find
Sonraki kullanılabilir UDP bağlantı noktasını bulma

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_free_port_find(
    NX_IP *ip_ptr, 
    UINT port,
    UINT *free_port_ptr);
```
### <a name="description"></a>Description

Bu hizmet, uygulama tarafından sağlanan bağlantı noktası numarasından başlayarak ücretsiz bir UDP bağlantı noktası (sınırsız) için başvurur. Arama, en yüksek bağlantı noktası değerine ulaşırsa arama mantığı 0xFFFF. Arama başarılı olursa boş bağlantı noktası, bağımsız değişken tarafından işaret eden değişkende free_port_ptr.

> [!WARNING]  
> *Bu hizmet başka bir iş parçacığından çağrıl olabilir ve aynı bağlantı noktasının döndürülene sahip olabilir. Bu yarış durumunu önlemek için, uygulama bu hizmeti* ve gerçek yuva bağlamasını bir mutex koruması altına yerleştirin.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **bağlantı noktası** Aramaya başlamak için bağlantı noktası numarası (1 ile 0xFFFF).
- **free_port_ptr** Hedef boş bağlantı noktası dönüş değişkeninin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı ücretsiz bağlantı noktası bulma.
- **NX_NO_FREE_PORTS** (0x45) Boş bağlantı noktası bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.
- **NX_INVALID_PORT** (0x46) Belirtilen bağlantı noktası numarası geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Locate a free UDP port, starting at port 12, on a previously
   created IP instance. */
status = nx_udp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS pointer, "free_port" identifies the next
   free UDP port on the IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_info_get"></a>nx_udp_info_get
UDP etkinlikleri hakkında bilgi alma

### <a name="prototype"></a>Prototype  

```c
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
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için UDP etkinlikleri hakkında bilgi almaktadır.

> [!IMPORTANT]  
> *Bir hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülz.*

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi.
- **udp_packets_sent** Gönderilen toplam UDP paketi sayısı için hedefin işaretçisi.
- **udp_bytes_sent** Gönderilen toplam UDP bayt sayısı için hedefe işaretçi.
- **udp_packets_received** Alınan toplam UDP paketi sayısının hedefine işaretçi.
- **udp_bytes_received** Alınan toplam UDP bayt sayısının hedefine işaretçi.
- **udp_invalid_packets** Toplam geçersiz UDP paketi sayısının hedefine işaretçi.
- **udp_receive_packets_dropped** Bırakılan toplam UDP alma paketlerinin hedef işaretçisi.
- **udp_checksum_errors** Sağlama toplamı hatalarına sahip UDP paketlerinin toplam sayısının hedefine işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı UDP bilgileri alma.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları ve süreerler

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Retrieve UDP information from previously created IP Instance
   ip_0. */
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

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_packet_info_extract"></a>nx_udp_packet_info_extract
UDP paketinden ağ parametrelerini ayıklama

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_packet_info_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address,
    UINT *protocol,
    UINT *port,
    UINT *interface_index);
```
### <a name="description"></a>Description

Bu hizmet, gelen arabirimde alınan bir paketten IPv4 adresi, eş bağlantı noktası numarası, protokol türü (bu hizmet her zaman UDP türünü döndürür) gibi ağ parametrelerini ayıklar. Uygulama, IPv4 veya IPv6 ağına sahip bir paketle ilgili bilgi almak için hizmet ***nxd_udp_packet_info_extract.***

### <a name="parameters"></a>Parametreler

- **packet_ptr** Paket işaretçisi.
- **ip_address** Gönderen IP adresinin işaretçisi.
- **protokol** Protokol işaretçisi (UDP).
- **bağlantı noktası** Gönderenin bağlantı noktası numarasının işaretçisi.
- **interface_index** Arabirim dizinini alma işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Paket arabirimi verileri başarıyla ayıklandı.
- **NX_INVALID_PACKET** (0x12) Paketi IPv4 çerçevesi içermez.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi girişi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Extract network data from UDP packet interface.*/
status = nx_udp_packet_info_extract(packet_ptr, &ip_address,
                                     &protocol, &port,
                                     &interface_index);

/* If status is NX_SUCCESS packet data was successfully
   retrieved. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_bind"></a>nx_udp_socket_bind
UDP yuvasını UDP bağlantı noktasına bağla

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_bind(
    NX_UDP_SOCKET *socket_ptr, 
    UINT port,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, önceden oluşturulan UDP yuvasını belirtilen UDP bağlantı noktasına bağlar. Geçerli UDP yuvaları 0 ile 0xFFFF arasındadır. İstenen bağlantı noktası numarası başka bir yuvaya bağlıysa, bu hizmet, yuvanın bağlantı noktası numarasından bağlantısını kesmek için belirtilen süre boyunca bekler.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.
- **bağlantı noktası** * * (1 ile 0xFFFF arasında) bağlamak için bağlantı noktası numarası. Bağlantı noktası numarası NX_ANY_PORT * * (0x0000) ise, IP örneği sonraki boş bağlantı noktasını arar ve bu bağlantıyı bağlama için kullanır.
- **wait_option** Bağlantı noktası zaten başka bir yuvaya bağlanmışsa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xffffffff)
    - **ticks içinde zaman aşımı değeri** (0x00000001-0xfffffffe)

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

No

### <a name="example"></a>Örnek

```c
/* Bind the previously created UDP socket to port 12 on the
   previously created IP instance. If the port is already bound,
   wait for 300 timer ticks before giving up. */
status = nx_udp_socket_bind(&udp_socket, 12, 300);

/* If status is NX_SUCCESS, the UDP socket is now bound to
   port 12.*/
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_bytes_available"></a>nx_udp_socket_bytes_available
Alma için kullanılabilir bayt sayısını alır

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_bytes_available(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Get the bytes available for retrieval from the UDP socket. */
status = nx_udp_socket_bytes_available(&my_socket,
                                       &bytes_available);

/* If status == NX_SUCCESS, the number of bytes was successfully
   retrieved.*/
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_checksum_disable"></a>nx_udp_socket_checksum_disable
UDP yuvası için sağlamaları devre dışı bırakma

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_checksum_disable(NX_UDP_SOCKET *socket_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen UDP yuvasında paket göndermek ve almak için sağlama alma mantığını devre dışı bıraktır. Sağlama sayısı mantığı devre dışı bırakılmıştır. Bu yuva üzerinden gönderilen tüm paketler için UDP üst bilgisinde sağlama alanı alanına sıfır değeri yüklenir. UDP üst bilgisinde sıfır değer sağlama değeri, alıcıya bu paket için sağlama sağlama değerinin hesaplanmaz olduğunu belirtir.

Ayrıca, UDP paketlerini alırken ve **gönderirken NX_DISABLE_UDP_RX_CHECKSUM** **ve NX_DISABLE_UDP_TX_CHECKSUM** tanımlandığı zaman bunun hiçbir etkisi olmadığını unutmayın,

UDP sağlamaları IPv6 için zorunlu olduğu için bu hizmetin IPv6 ağı üzerindeki paketler üzerinde hiçbir etkisi olmadığını unutmayın.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı yuva sağlamayı devre dışı bırakma.
- **NX_NOT_BOUND** (0x24) Yuva bağlı değil.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları, zamanlayıcı

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Disable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_disable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will not have a checksum
   calculated. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_checksum_enable"></a>nx_udp_socket_checksum_enable
UDP yuvası için sağlamaları etkinleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_checksum_enable(NX_UDP_SOCKET *socket_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen UDP yuvasında paket göndermek ve almak için sağlama alma mantığını sağlar. Sağlama toplama, UDP veri alanı tamamını ve bir sahte IP üst bilgisini kapsar.

Ayrıca, UDP paketlerini alırken ve **gönderirken NX_DISABLE_UDP_RX_CHECKSUM** **ve NX_DISABLE_UDP_TX_CHECKSUM** tanımlandığı zaman bunun hiçbir etkisi olmadığını unutmayın.

Bu hizmetin IPv6 ağı üzerindeki paketler üzerinde hiçbir etkisi olmadığını unutmayın. IPv6'da UDP sağlamaları zorunludur.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğinin işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı yuva sağlamaları etkinleştirme.
- **NX_NOT_BOUND** (0x24) Yuva bağlı değil.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları, zamanlayıcı

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Enable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_enable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will have a checksum
   calculated. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_create"></a>nx_udp_socket_create
UDP yuvası oluştur

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_create(
    NX_IP *ip_ptr,
    NX_UDP_SOCKET *socket_ptr, 
    CHAR *name,
    ULONG type_of_service, 
    ULONG fragment,
    UINT time_to_live, 
    ULONG queue_maximum);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için bir UDP yuvası oluşturur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.
- **socket_ptr** Yeni UDP yuva denetimi Bloc işaretçisi.
- **ad** Bu UDP yuvasının uygulama adı.
- **Type_of_service** İletim için hizmet türünü tanımlar, yasal değerler aşağıdaki gibidir:
    - **NX_IP_NORMAL** (0x00000000)
    - **NX_IP_MIN_DELAY** (0x00100000)
    - **NX_IP_MAX_DATA** (0x00080000)
    - **NX_IP_MAX_RELIABLE** (0x00040000)
    - **NX_IP_MIN_COST** (0x00020000)
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

No

### <a name="example"></a>Örnek

```c
/* Create a UDP socket with a maximum receive queue of 30 packets.*/
status = nx_udp_socket_create(&ip_0, &udp_socket, "Sample UDP Socket",
                              NX_IP_NORMAL, NX_FRAGMENT_OKAY, 0x80,
                              30);

/* If status is NX_SUCCESS, the new UDP socket has been created and
   is ready for binding. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_delete"></a>nx_udp_socket_delete
UDP yuvasını Sil

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_delete(NX_UDP_SOCKET *socket_ptr);
```
### <a name="description"></a>Description

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

No

### <a name="example"></a>Örnek

```c
/* Delete a previously created UDP socket. */
status = nx_udp_socket_delete(&udp_socket);

/* If status is NX_SUCCESS, the previously created UDP socket has
   been deleted. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_info_get"></a>nx_udp_socket_info_get
UDP yuva etkinlikleri hakkında bilgi alın

### <a name="prototype"></a>Prototype  

```c
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
### <a name="description"></a>Description

Bu hizmet, belirtilen UDP yuva örneği için UDP yuva etkinlikleri hakkında bilgi almaktadır.

> [!IMPORTANT]  
> *Bir hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülz.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğinin işaretçisi.
- **udp_packets_sent** Yuvada gönderilen toplam UDP paketi sayısı için hedefe işaretçi.
- **udp_bytes_sent** Yuvada gönderilen toplam UDP bayt sayısı için hedefe işaretçi.
- **udp_packets_received** Yuvada alınan toplam UDP paketlerinin hedef işaretçisi.
- **udp_bytes_received** Yuvada alınan toplam UDP bayt sayısının hedefine işaretçi.
- **udp_packets_queued** Yuvadaki kuyruğa alınan UDP paketlerinin toplam sayısının hedefine işaretçi.
- **udp_receive_packets_dropped** Kuyruk boyutu aşılırken yuva için bırakılan toplam UDP alma paketlerinin hedef işaretçisi.
- **udp_checksum_errors** Yuvada sağlama toplamı hatalarına sahip udp paketlerinin toplam sayısının hedefine işaretçi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı UDP yuva bilgisi alma.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları ve süreerler

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
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

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_port_get"></a>nx_udp_socket_port_get
UDP yuvasına bağlı bağlantı noktası numarasını seçme

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_port_get(
    NX_UDP_SOCKET *socket_ptr,
    UINT *port_ptr);
```
### <a name="description"></a>Description

Bu hizmet, yuvayla ilişkilendirilmiş bağlantı noktası numarasını alan bu numara, yuvanın bağlı olduğu sırada NX_ANY_PORT NetX Duo tarafından ayrılan bağlantı noktasını bulmak için kullanışlıdır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğinin işaretçisi.
- **port_ptr** Dönüş bağlantı noktası numarası için hedefin işaretçisi. Geçerli bağlantı noktası numaraları (1- 0xFFFF).

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı yuva bağlaması.
- **NX_NOT_BOUND** (0x24) Bu yuva bir bağlantı noktasına bağlı değildir.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi veya bağlantı noktası dönüş işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Get the port number of created and bound UDP socket. */
status = nx_udp_socket_port_get(&udp_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
   socket is bound to. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_receive"></a>nx_udp_socket_receive
UDP yuvasından veri birimi alma

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_receive(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen yuvadan bir UDP veri birimi alır. Belirtilen yuvada kuyruğa alınan veri birimi yoksa, çağıran sağlanan bekleme seçeneğine göre askıya alır.

> [!CAUTION]  
> *Bir NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığı zaman alınan paketi serbest bırakmakla sorumludur.*

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğinin işaretçisi.
- **packet_ptr** UDP veri birimi paket işaretçisi işaretçisi.
- **wait_option** Şu anda bu yuvada kuyruğa alınan bir veri birimi yoksa hizmetin nasıl davranacağını tanımlar. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **tıklar içinde zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) Başarılı yuva alma.
- **NX_NOT_BOUND** (0x24) Yuva hiçbir bağlantı noktasına bağlı değil.
- **NX_NO_PACKET** (0x01) Alacak UDP veri birimi yoktu.
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma isteği, tx_thread_wait_abort.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva veya paket dönüş işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz.
- **NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmedi.

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Receive a packet from a previously created and bound UDP socket.
   If no packets are currently available, wait for 500 timer ticks
   before giving up. */
status = nx_udp_socket_receive(&udp_socket, &packet_ptr, 500);

/* If status is NX_SUCCESS, the received UDP packet is pointed to by
   packet_ptr. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_receive_notify"></a>nx_udp_socket_receive_notify
Alınan her paketin uygulamaya bildir

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_receive_notify(
    NX_UDP_SOCKET *socket_ptr,
    VOID (*udp_receive_notify)(NX_UDP_SOCKET *socket_ptr));
```
### <a name="description"></a>Description 

Bu hizmet, uygulama tarafından belirtilen geri çağırma işlevinin alma bildirim işlevi işaretçisini ayarlar. Bu geri çağırma işlevi daha sonra yuvada bir paket her alınarak çağrılır. Bir NX_NULL işaretçisi sağlanırsa, receive notify işlevi devre dışı bırakılır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** UDP yuvasının işaretçisi.
- **udp_receive_notify** Yuvada bir paket alınca çağrılır uygulama geri çağırma işlevi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Yuva alma bildirim işlevini başarıyla ayarlayın.
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları, süreerler ve ISR'ler

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Setup a receive packet callback function for the "udp_socket"
   socket. */
status = nx_udp_socket_receive_notify(&udp_socket,
                                      my_receive_notify);

/* If status is NX_SUCCESS, NetX Duo will call the function named
   "my_receive_notify" whenever a packet is received for
   "udp_socket". */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_send"></a>nx_udp_socket_send
UDP Veri Birimi gönderme

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address, 
    UINT port);
```
### <a name="description"></a>Description

Bu hizmet, IPv4 ağları için önceden oluşturulmuş ve bağlı bir UDP yuvası üzerinden bir UDP veri birimi gönderir. NetX Duo, hedef IP adresine göre kaynak adres olarak uygun bir yerel IP adresi bulur. Uygulama, belirli bir arabirimi ve kaynak IP  adresini belirtmek için nxd_udp_socket_source_send kullanmalıdır.

UDP veri biriminin başarıyla gönderip gönderilmeden bağımsız olarak bu hizmetin hemen döndür olduğunu unutmayın. NetX Duo (IPv4/IPv6) eşdeğer hizmeti ***nxd_udp_socket_send.***

Yuvanın yerel bir bağlantı noktasına bağlı olması gerekir.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğinin işaretçisi
- **packet_ptr** UDP veri birimi paket işaretçisi
- **ip_address** Hedef IPv4 adresi
- **bağlantı noktası** Konak byte sırasına göre 1 ile 0xFFFF arasında geçerli hedef bağlantı noktası numarası

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı UDP yuva gönderme
- **NX_NOT_BOUND** (0x24) Yuva hiçbir bağlantı noktasına bağlı değil
- **NX_NO_INTERFACE_ADDRESS** (0x50) Uygun bir giden arabirim bulunamadı.
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz sunucu IP adresi
- **NX_UNDERFLOW** (0x02) Pakette UDP üst bilgisi için yeterli alan yok
- **NX_OVERFLOW** (0x03) Paket ekleme işaretçisi geçersiz
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı
- **NX_NOT_ENABLED** (0x14) UDP etkin değil
- **NX_INVALID_PORT** (0x46) bağlantı noktası numarası geçerli bir Aralık içinde değil

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
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

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_source_send"></a>nx_udp_socket_source_send
UDP yuvası üzerinden veri birimi gönder

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_source_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port,
    UINT address_index);
```
### <a name="description"></a>Description

Bu hizmet, kaynak adresi olarak belirtilen IP adresine sahip ağ arabirimi aracılığıyla daha önce oluşturulmuş ve bağlantılı bir UDP yuvası aracılığıyla bir UDP datagramı gönderir. UDP veri biriminin başarıyla gönderilip gönderilmediğini ne olursa olsun hizmetin hemen geri döndüğünü unutmayın. ***nxd_udp_socket_source_send*** hem IPv4 hem de IPv6 ağlarında çalışmaktadır.

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

No

### <a name="example"></a>Örnek

```c
#define ADDRESS_INDEX 1

/* Send packet out on port 80 to the specified destination IP on the
   interface at index 1 in the IP task interface list. */
status = nx_udp_socket_source_send(socket_ptr, packet_ptr,
                                   destination_ip, 80,
                                   ADDRESS_INDEX);

/* If status is NX_SUCCESS packet was successfully transmitted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_unbind"></a>nx_udp_socket_unbind
UDP bağlantı noktasından gelen UDP yuvasının bağlantısını kaldır

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_socket_unbind(NX_UDP_SOCKET *socket_ptr);
```
### <a name="description"></a>Description

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

```c
/* Unbind the previously bound UDP socket. */
status = nx_udp_socket_unbind(&udp_socket);

/* If status is NX_SUCCESS, the previously bound socket is now
   unbound. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_source_extract"></a>nx_udp_source_extract
UDP veri kaynağından IP ve gönderme bağlantı noktasını Ayıkla

### <a name="prototype"></a>Prototype  

```c
UINT nx_udp_source_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address, 
    UINT *port);
```
### <a name="description"></a>Description

Bu hizmet, gönderenin IP ve bağlantı noktası numarasını, sağlanan UDP veri biriminin IP ve UDP üst bilgilerinden ayıklar. Hizmet ***Nxd_udp_source_extract*** IPv4 veya IPv6 ağından gelen paketlerle birlikte çalışıp çalışmadığını unutmayın.

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

No

### <a name="example"></a>Örnek

```c
/* Extract the IP and port information from the sender of the UPD packet. */
status = nx_udp_source_extract(packet_ptr, &sender_ip_address, &sender_port);

/* If status is NX_SUCCESS, the sender IP and port information has been stored
   in sender_ip_address and sender_port respectively.*/
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nxd_icmp_enable"></a>nxd_icmp_enable
Icmpv4 ve ICMPv6 hizmetlerini etkinleştir

### <a name="prototype"></a>Prototype  

```c
UINT nxd_icmp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet her iki Icmpv4 ve ICMPv6 hizmetini de sunar ve yalnızca IP örneği oluşturulduktan sonra çağrılabilir. Hizmet, IPv6 etkinleştirilmeden önce ya da sonra etkinleştirilebilir (bkz. *nxd_ipv6_enable*). ICMPv4 Hizmetleri yankı Isteği/yanıtı içerir. ICMPv6 Hizmetleri yankı Isteği/yanıtı, komşu bulma, yinelenen adres algılama, yönlendirici bulma ve durum bilgisiz adresi otomatik yapılandırmasını içerir. NetX 'teki IPv4 eşdeğeri *nx_icmp_enable*.

> [!NOTE] 
> *ICMPv6 etkinleştirilmeden önce IPv6 adresi el ile yapılandırıldıysa, el ile yapılandırılan IPv6, yinelenen adres algılama işlemine tabi değildir*.

*nx_icmp_enable* yalnızca IPv4 IŞLEMLERI için ICMP hizmetlerini başlatır. ICMPv6 hizmetlerini kullanan uygulamalar *nx_icmp_enable* yerine *nxd_icmp_enable* kullanmalıdır.

IPv6 yönlendirici bağlantısı ve IPv6 durum bilgisiz otomatik adres yapılandırmasını kullanmak için, ICMPv6 etkinleştirilmelidir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) ICMP hizmetleri başarıyla etkinleştirildi
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Enable ICMP on the IP instance. */
status = nxd_icmp_enable(&ip_0);

/* A status return of NX_SUCCESS indicates that the IP instance is
   enabled for ICMP services. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_icmp_enable
- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_ping
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nxd_icmp_ping"></a>nxd_icmp_ping
ICMPv4 veya ICMPv6 Yankı Istekleri gerçekleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_icmp_ping(
    NX_IP *ip_ptr, 
    NXD_ADDRESS *ip_address,
    CHAR *data_ptr, 
    ULONG data_size,
    NX_PACKET **response_ptr, 
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet uygun bir fiziksel arabirim aracılığıyla bir ıCMP yankı Isteği paketi gönderir ve hedef konaktan yankı yanıtı bekler. NetX Duo, ping iletisi göndermek için hedef adrese göre uygun arabirimi belirler. Uygulamalar, paket ***iletiminde nxd_icmp_source_ping*** fiziksel arabirimi ve kesin kaynak IP adresini belirtmek için hizmet ip adresini kullanmalıdır.

IP örneği oluşturulmuş olmalı ve ICMPv4/ICMPv6 hizmetleri etkinleştirilmelidir (bkz. ***nxd_icmp_enable).***

> [!WARNING]  
> Bir NX_SUCCESS döndürülürse, uygulama alınan paketi artık gerekli kalmadan serbest bırakmakla sorumludur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP örneğine işaretçi
- **ip_address** Ana bilgisayar byte sırasına göre ping gönderilecek hedef IP adresi
- **data_ptr** Paket veri alanına ping yapmak için işaretçi
- **data_size** Ping verisi bayt sayısı
- **response_ptr** Yanıt paketi işaretçisi İşaretçisi
- **wait_option** Yanıt bekleme zamanı. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **tıklar içinde zaman aşımı değeri** (0x00000001 değeri 
    - **NX_WAIT_FOREVER** 0xFFFFFFFE)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı gönderilen ve alınan ping
- **NX_NOT_SUPPORTED** (0x4B) IPv6 etkin değil
- **NX_OVERFLOW** (0x03) Ping verileri paket yükünü aşıyor
- **NX_NO_RESPONSE** (0x29) Hedef ana bilgisayar yanıt vermedi
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma işlemi tx_thread_wait_abort
- **NX_NO_INTERFACE_ADDRESS** (0x50) Uygun bir giden arabirim bulunamadı.
- **NX_PTR_ERROR** (0x07) Geçersiz IP veya yanıt işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz
- **NX_NOT_ENABLED** (0x14) IP veya ICMP bileşeni etkinleştirilmedi
- **NX_IP_ADDRESS_ERROR** (0x21) Giriş IP adresi geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* The following two examples illustrate how to use this API to send
   ping packets to IPv6 or IPv4 destinations. */

/* The first example: Send a ping packet to an IPv6 host
   2001:1234:5678::1 */
   
/* Declare variable address to hold the destination address. */
NXD_ADDRESS ip_address;

char *buffer = “abcd”;
UINT prefix_length = 10;

/* Set the IPv6 address. */
ip_address.nxd_ip_address_version  = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]    = 0x20011234;
ip_address.nxd_ip_address.v6[1]    = 0x56780000;
ip_address.nxd_ip_address.v6[2]    = 0;
ip_address.nxd_ip_address.v6[3]    = 1;

status = nxd_icmp_ping(&ip_0, &ip_address, buffer,
                       strlen(buffer),&response_ptr,
                       NX_WAIT_FOREVER);

/* A return value of NX_SUCCESS indicates a ping reply has been
   received from IP address 2001:1234:5678::1 and the response
   packet is contained in the packet pointed to by response_ptr.It
   should have the same “abcd” four bytes of data. */

/* The second example: Send a ping packet to an IPv4 host 1.2.3.4 */

/* Program the IPv4 address. */
ip_address.nxd_ip_address_version  = NX_IP_VERSION_V4;
ip_address.nxd_ip_address.v4[0]    = 0x01020304;

status = nxd_icmp_ping(&ip_0, &ip_address, buffer,
                       strlen(buffer),&response_ptr, 10);

/* A return value of NX_SUCCESS indicates a ping reply was received
   from IP address 1.2.3.4 and the response packet is contained in
   the packet pointed to by response_ptr. It should have the same
   “abcd” four bytes of data. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_icmp_enable
- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nxd_icmp_source_ping"></a>nxd_icmp_source_ping
ICMPv4 veya ICMPv6 Yankı İstekleri Gerçekleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_icmp_source_ping(
    NX_IP *ip_ptr, 
    NXD_ADDRESS *ip_address,
    UINT address_index,
    CHAR *data_ptr, 
    ULONG data_size,
    NX_PACKET **response_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, bir IPv4 veya IPv6 adresinin belirtilen dizinini kullanarak ve kaynak adresin ilişkili olduğu ağ arabirimi aracılığıyla bir ICMP Yankı İsteği paketi gönderir ve hedef konaktan bir Yankı Yanıtı bekler. Bu hizmet hem IPv4 hem de IPv6 adresleriyle çalışır. Parametre *address_index* kaynak IPv4 veya IPv6 adresini gösterir. IPv4 adresi için, *address_index* ekli ağ arabirimiyle aynı dizindir. IPv6 için, *address_index* IPv6 adres tablosunda girdiyi gösterir.

IP örneği oluşturulmuş olmalı ve ICMPv4 ve ICMPv6 hizmetleri etkinleştirilmelidir (bkz. *nxd_icmp_enable).*

> [!CAUTION] 
> *Bir NX_SUCCESS döndürülürse, uygulama alınan paketi* artık gerekli kalmadan serbest bırakmakla sorumludur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP örneğine işaretçi
- **ip_address** Ana bilgisayar byte sırasına göre ping gönderilecek hedef IP adresi
- **address_index** Kaynak adres olarak kullanmak üzere IP adresini gösterir
- **data_ptr** Paket veri alanına ping yapmak için işaretçi
- **data_size** Ping verisi bayt sayısı
- **response_ptr** Yanıt paketi işaretçisine işaretçi
- **wait_option** Yanıt bekleme zamanı. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **tıklar içinde zaman aşımı değeri** (0x00000001 aracılığıyla 0xFFFFFFFE
    - **NX_WAIT_FOREVER** 0xFFFFFFFF)

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı gönderilen ve alınan ping
- **NX_NOT_SUPPORTED** (0x4B) IPv6 etkin değil
- **NX_OVERFLOW** (0x03) Ping verileri paket yükünü aşıyor
- **NX_NO_RESPONSE** (0x29) Hedef ana bilgisayar yanıt vermedi
- **NX_WAIT_ABORTED** (0x1A) İstenen askıya alma işlemi tx_thread_wait_abort
- **NX_NO_INTERFACE_ADDRESS** (0x50) Uygun giden arabirim bulunamadı
- **NX_PTR_ERROR** (0x07) Geçersiz IP veya yanıt işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz
- **NX_NOT_ENABLED** (0x14) IP veya ICMP bileşeni etkinleştirilmedi
- **NX_IP_ADDRESS_ERROR** (0x21) Giriş IP adresi geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* The following two examples illustrate how to use this API to send ping
   packets to IPv6 or IPv4 destinations. */

/* The first example: Send a ping packet to an IPv6 host
   FE80::411:7B23:40dc:f181 */

/* Declare variable address to hold the destination address. */

#define PRIMARY_INTERFACE 0
#define GLOBAL_IPv6_ADDRESS 1

NXD_ADDRESS ip_address;
char *buffer = “abcd”;
UINT prefix_length = 10;

/* Set the IPv6 address. */
ip_address.nxd_ip_address_version  = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]    = 0xFE800000;
ip_address.nxd_ip_address.v6[1]    = 0x00000000;
ip_address.nxd_ip_address.v6[2]    = 0x04117B23;
ip_address.nxd_ip_address.v6[3]    = 0x40DCF181;

status = nxd_icmp_source_ping(&ip_0, &ip_address,
                              GLOBAL_IPv6_ADDRESS,
                              buffer,
                              strlen(buffer),
                              &response_ptr,
                              NX_WAIT_FOREVER);

/* A return value of NX_SUCCESS indicates a ping reply has been received
   from IP address FE80::411:7B23:40dc:f181 and the response packet is
   contained in the packet pointed to by response_ptr. It should have the
   same “abcd” four bytes of data. */

/* The second example: Send a ping packet to an IPv4 host 1.2.3.4 */

/* Program the IPv4 address. */
ip_address.nxd_ip_address_version  = NX_IP_VERSION_V4;
ip_address.nxd_ip_address.v4       = 0x01020304;

status = nxd_icmp_source_ping(&ip_0, &ip_address,
                              PRIMARY_INTERFACE,
                              buffer,
                              strlen(buffer),
                              &response_ptr,
                              NX_WAIT_FOREVER);

/* A return value of NX_SUCCESS indicates a ping reply was received from
   IP address 1.2.3.4 and the response packet is contained in the packet
   pointed to by response_ptr. It should have the same “abcd” four bytes
   of data. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_icmp_enable
- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nxd_icmpv6_ra_flag_callback_set"></a>nxd_icmpv6_ra_flag_callback_set
ICMPv6 RA bayrağı değiştirme geri çağırma işlevini ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nxd_icmpv6_ra_flag_callback_set(
    NX_IP *ip_ptr, 
    VOID(*ra_callback)(NX_IP*ip_ptr, UINT ra_flag));
```
### <a name="description"></a>Description

Bu hizmet, ICMPv6 Yönlendirici Tanıtım bayrağı değişiklik geri çağırma işlevini ayarlar. NetX Duo yönlendirici tanıtım iletisi aldığında kullanıcı tarafından sağlanan geri çağırma işlevi çağrılır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP örneğine işaretçi
- **ra_callback** Kullanıcı tarafından sağlanan geri çağırma işlevi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) RA bayrağı geri çağırma işlevini ayarlama başarılı
- **NX_NOT_SUPPORTED** (0x4B) IPv6 etkin değil
- **NX_PTR_ERROR** (0x07) Geçersiz IP
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
VOID icmpv6_ra_flag_callback(NX_IP *ip_ptr, UINT ra_flag)
{
   /* RA flag has changed. The updated value is passed in via the
      ra_flag parameter. */
}

/* Configure the user-defined ICMPv6 RA flag change callback
   function. */
status = nxd_icmpv6_ra_flag_callback_set(&ip_0,
                                         icmpv6_ra_flag_callback);

/* A status return of NX_SUCCESS indicates the callback function has
   been successfully configured. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_icmp_enable
- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmp_source_ping

## <a name="nxd_ip_raw_packet_send"></a>nxd_ip_raw_packet_send
Ham IP Paketi Gönder

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ip_raw_packet_send(
    NX_IP *ip_ptr, 
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *destination
    ULONG protocol, 
    UINT ttl, 
    ULONG tos);
```
### <a name="description"></a>Description

Bu hizmet ham bir IPv4 veya IPv6 paketi gönderir (aktarım katmanı protokol üst bilgileri yoktur). Birden çok girişli bir sistemde, sistem uygun bir arabirim belirleyeeyse (örneğin, hedef IP adresi IPv4 yayını, çok noktaya yayın veya IPv6 çok noktaya yayın adresiyse), birincil cihaz seçilir. Giden bir **nxd_ip_raw_packet_source_send** belirtmek için hizmet * nxd_ip_raw_packet_source_send _ kullanılabilir. NetX eşdeğeri _ *_nx_ip_raw_packet_send._**

IP örneği daha önce oluşturulmalı ve ham IP paketi işleme, nx_ip_raw_packet_enable ***kullanılarak etkinleştirilmelidir.***

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi
- **packet_ptr** İletmek için paket işaretçisi
- **destination_ip** Hedef adres işaretçisi
- **protokol** IP üst bilgisinde depolanan paket protokolü
- **ttl** TTL veya atlama sınırı değeri
- **tos** TOS veya trafik sınıfı ve akış etiketi değeri

### <a name="return-value"></a>Dönüş Değeri 

- **NX_SUCCESS** (0x00) Ham IP paketi başarıyla gönderildi
- **NX_NO_INTERFACE_ADDRESS** (0x50) Uygun giden arabirim bulunamadı
- **NX_NOT_ENABLED** (0x14) Ham IP işleme etkinleştirilmedi
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz IPv4 veya IPv6 adresi
- **NX_UNDERFLOW** (0x02) Pakette IPv4 veya IPv6 üst bilgisi için yeterli alan yok
- **NX_OVERFLOW** (0x03) Paket ekleme işaretçisi geçersiz
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi veya paket işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz
- **NX_INVALID_PARAMETERS** (0x4D) Geçerli değil IPv6 adresi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
NXD_ADDRESS dest_address;

/* Set the destination address,in this case an IPv6 address. */
dest_address.nxd_ip_address_version  = NX_IP_VERSION_V6;
dest_address.nxd_ip_address.v6[0]    = 0x20011234;
dest_address.nxd_ip_address.v6[1]    = 0x56780000;
dest_address.nxd_ip_address.v6[2]    = 0;
dest_address.nxd_ip_address.v6[3]    = 1;

UINT ttl, tos;

ttl = 128;

tos = 0;

/* Enable RAW IP handling on the previously created IP instance.*/
status = nx_raw_ip_packet_enable(&ip_0);

/* Allocate a packet pointed to by packet_ptr from the IP packet
   pool. */
/* Then transmit the packet to the destination address. */

status = nxd_ip_raw_packet_send(&ip_0, packet_ptr, dest_address,
                                NX_PROTOCOL_UDP, ttl, tos);

/* A status return of NX_SUCCESS indicates the packet was
   successfully transmitted. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_source_send

## <a name="nxd_ip_raw_packet_source_send"></a>nxd_ip_raw_packet_source_send
Belirtilen kaynak adresini kullanarak ham paket gönderme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ip_raw_packet_source_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *destination_ip,
    UINT address_index,
    ULONG protocol,
    UINT ttl,
    ULONG tos);
```
### <a name="description"></a>Description

Bu hizmet, kaynak adres olarak belirtilen IPv4 veya IPv6 adresini kullanarak ham bir IPv4 veya IPv6 paketi gönderir. Bu hizmet genellikle, sistem uygun bir arabirimi belirleyeyene (örneğin, hedef IP adresi IPv4 yayını, çok noktaya yayın veya IPv6 çok noktaya yayın adresi ise) çok girişli bir sistemde kullanılır. Bu *address_index,* uygulamanın bu ham paketi gönderirken kullanmak üzere kaynak adresi belirtmesini sağlar.

IP örneği daha önce oluşturulmalı ve ham IP paketi işleme, nx_ip_raw_packet_enable ***kullanılarak etkinleştirilmelidir.***

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP örneği işaretçisi
- **packet_ptr** Göndermek için paket işaretçisi
- **destination_ip** Hedef IP adresi
- **address_index** Kaynak adres olarak kullanmak üzere IPv4 veya IPv6 adreslerine dizinleme.
- **protokol** Protokol alanı için değer
- **ttl** ttl veya atlama sınırı değeri
- **tos** Tos veya trafik sınıfı ve akış etiketi değeri

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Paketi başarıyla gönderildi
- **NX_UNDERFLOW** (0x02) Pakette IPv4 veya IPv6 üst bilgisi için yeterli alan yok
- **NX_OVERFLOW** (0x03) Paket ekleme işaretçisi geçersiz
- **NX_PTR_ERROR** (0x07) IP denetim bloğu, paket veya bağlantı için geçersiz destination_ip
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz
- **NX_NOT_ENABLED** (0x14) Ham işleme etkinleştirilmedi
- **NX_IP_ADDRESS_ERROR** (0x21) Adres hatası
- **NX_INVALID_INTERFACE** (0x4C) Geçersiz arabirim dizini
- **NX_INVALID_PARAMETERS** (0x4D) Geçerli değil IPv6 adresi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacığı

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
#define SOURCE_ADDRESS_INDEX 2

/* Send a raw packet from specified interface. */
status = nxd_ip_raw_packet_source_send(&ip_0, packet_ptr,
                                       dest_ip,
                                       SOURCE_ADDRESS_INDEX,
                                       NX_IP_RAW,
                                       NX_IP_TIME_TO_LIVE,
                                       NX_IP_NORMAL);

/* If status == NX_SUCCESS, raw packet has been sent out on the
   specified interface. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send

## <a name="nxd_ipv6_address_change_notify"></a>nxd_ipv6_address_change_notify
ipv6 adres değişikliği bildirimi ayarlama

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_address_change_notify(
    NX_IP *ip_ptr,
    VOID (*ip_address_change_notify)(NX_IP *, UINT, UINT, UINT, ULONG *));
```
### <a name="description"></a>Description

Bu hizmet, IPv6 Adresi her değiştiriken NetX Duo tarafından çağrılan bir uygulama geri çağırma yordamını kaydedmektedir.

NetX Duo kitaplığını oluşturma seçeneği tanımlandığı zaman ***bu*** NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY kullanılabilir.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** IP denetim bloğu işaretçisi
- **ip_address_change_notify** Uygulama geri çağırma işlevi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) başarılı küme
- **NX_NOT_SUPPORTED** (0x4b) IPv6 adres değişikliği bildirim özelliği NETX Duo kitaplığında yerleşik değil
- **NX_PTR_ERROR** (0x07) geçersiz IP denetimi blok işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı
- **NX_NOT_ENABLED** (0x14) IPv6 adres değişikliği bildirimi derlenmedi

### <a name="allowed-from"></a>İzin verilen

İş Parçacığı

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
VOID ip_address_change_notify(NX_IP *ip_ptr, UINT status,
                              UINT interface_index,
                              UINT address_index,
                              ULONG *ip_address)
{

   /* Do something when ip address changed. */
}

void ip_address_thread_entry(ULONG id)
{

   /* Set the ip address change notify of IP instance. */
   status = nxd_ipv6_address_change_notify (&ip_0, ip_address_change_notify);

/* If status == NX_SUCCESS, the ip address change notify of IP
   instance was successfully set. */
}
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_address_delete"></a>nxd_ipv6_address_delete
IPv6 adresini Sil

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_address_delete(
    NX_IP *ip_ptr, 
    UINT address_index);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneğinin IPv6 adresi tablosundaki belirtilen dizindeki IPv6 adresini siler. NetX eşdeğeri yoktur.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi
- **address_index** Dizinden IP örneği IPv6 adresi tablosu

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) adresi başarıyla silindi
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değil
- **NX_NO_INTERFACE_ADDRESS** (0x50) uygun bir giden arabirim bulunamıyor
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
NXD_ADDRESS ip_address;
UINT        address_index;

/* Delete the IPv6 address at the specified address table index. */
address_index = 1;
status = nxd_ipv6_address_delete(&ip_0, address_index);

/* A status return of NX_SUCCESS indicates that the IP instance
   address is successfully deleted. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_address_get"></a>nxd_ipv6_address_get
IPv6 adresini ve önekini al

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_address_get(
    NX_IP *ip_ptr, 
    UINT address_index, 
    NXD_ADDRESS *ip_address,
    ULONG *prefix_length,
    UINT *interface_index);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneğinin adres tablosundaki belirtilen dizindeki IPv6 adresini ve önekini alır. IPv6 adresinin ilişkilendirildiği fiziksel arabirimin dizini *interface_index* işaretçisine döndürülür. NetX denk Hizmetleri, ***nx_ip_address_get** _ ve _ *_nx_ip_interface_address_get_* * ' dir.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi
- **address_index** IP örnek adresi tablosuna Dizin
- **ip_address** Ayarlanacak adrese yönelik işaretçi
- **prefix_length** Adres ön ekinin uzunluğu (alt ağ maskesi)
- **interface_index** Arabirimin dizinine yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IPv6 başarıyla etkinleştirildi
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değildir.
- **NX_NO_INTERFACE_ADDRESS** (0x50) arabirim adresi yok veya geçersiz address_index
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
NXD_ADDRESS ip_address;
UINT        address_index;
ULONG       prefix_length;
UINT        interface_index;

/* Get the IPv6 address at the specified address table index. If
   found, the address network interface is returned in the
   interface_index input, as well as the address prefix in the
   prefix_length input. */

address_index = 1;
status = nxd_ipv6_address_get(&ip_0, address_index, &ip_address,
                              &prefix_length, &interface_index);

/* A status return of NX_SUCCESS indicates that the IP instance
   address is successfully retrieved. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_address_set"></a>nxd_ipv6_address_set
IPv6 adresini ve önekini ayarla

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_address_set(
    NX_IP *ip_ptr, 
    UINT interface_index,
    NXD_ADDRESS *ip_address,
    ULONG prefix_length,
    UINT *address_index);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan IPv6 adresini ve önekini belirtilen IP örneğine ayarlar. *Address_index* bağımsız değişkeni null değilse, adresin eklendiği IPv6 adres tablosuna olan dizin döndürülür. NetX denk Hizmetleri, ***nx_ip_address_set** _ ve _ *_nx_ip_interface_address_set_* * ' dir.

### <a name="parameters"></a>Parametreler  

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi
- **interface_index** IPv6 adresinin ilişkilendirildiği arabirimin dizini
- **ip_address** Ayarlanacak adrese yönelik işaretçi
- **prefix_length** Adres ön ekinin uzunluğu (alt ağ maskesi)
- **address_index** Adresin eklendiği adres tablosuna Dizin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IPv6 başarıyla etkinleştirildi
- **NX_NO_MORE_ENTRIES** (0x15) IP adresi tablosu dolu
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değildir.
- **NX_DUPLICATED_ENTRY** (0x52) sağlanan IP adresı bu IP örneğinde zaten kullanılıyor
- **NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IPv6 adresi
- **NX_INVALID_INTERFACE** (0x4C) arabirimi geçersiz bir ağ arabirimine işaret ediyor

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
NXD_ADDRESS ip_address;
UINT        address_index;
UINT        interface_index;

ip_address.nxd_ip_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0] = 0x20010000;
ip_address.nxd_ip_address.v6[1] = 0;
ip_address.nxd_ip_address.v6[2] = 0;
ip_address.nxd_ip_address.v6[3] = 1;

/* First create an IP instance with packet pool, source address, and
   driver.*/
status = nx_ip_create(&ip_0, "NetX IP Instance 0",
                     IP_ADDRESS(1,2,3,4),
                     0xFFFFFF00UL, &pool_0,_nx_ram_network_driver,
                     pointer, 2048, 1);

/* Then enable IPv6 on the IP instance. */
status = nxd_ipv6_enable(&ip_0);

/* Set the IPv6 address (a global address as indicated by the 64 bit
   prefix) using the IPv6 address just created on the primary device
   (index zero). The index into the address table is returned in
   address_index. */
interface_index = 0;
status = nxd_ipv6_address_set(&ip_0, interface_index, &ip_address,
                              64,&address_index);

/* A status return of NX_SUCCESS indicates that the IPv6 address is
   successfully assigned to the primary interface (interface 0). */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_default_router_add"></a>nxd_ipv6_default_router_add
Varsayılan yönlendirici tablosuna bir IPv6 yönlendiricisi ekleme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_default_router_add(
    NX_IP *ip_ptr,
    NXD_ADDRESS *router_address,
    ULONG router_lifetime,
    UINT index_index);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen fiziksel arabirime varsayılan yönlendirici tablosuna bir IPv6 varsayılan yönlendiricisi ekler. Eşdeğer NetX IPv4 hizmeti ***nx_ip_gateway_address_set***.

*router_address* geçerli bir IPv6 adresine işaret etmelidir ve yönlendiricinin belirtilen fiziksel arabirimden doğrudan erişilebilir olması gerekir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi
- **router_address** Ana bilgisayar bayt düzeninde varsayılan yönlendirici adresine yönelik işaretçi
- **router_lifetime** Varsayılan yönlendirici yaşam süresi (saniye). Geçerli değerler:
    - **0xFFFF:** Zaman aşımı yok
    - **0-0xFFFE:** Saniye cinsinden zaman aşımı değeri
- **index_index** Yönlendirici üzerinden erişilebileceği ağ dizini dizini için geçerli bellek konumuna işaretçi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) varsayılan yönlendirici başarıyla eklendi
- **NX_NO_MORE_ENTRIES** (0x17) varsayılan yönlendirici tablosunda daha fazla girdi yok.
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz IPv6 adresi
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değildir.
- **NX_INVALID_PARAMETERS** (0x4D) geçerli IPv6 adresi girişi değil
- **NX_PTR_ERROR** (0x07) geçersiz IP örneği veya depolama alanı
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı
- **NX_INVALID_INTERFACE** (0x4C) geçersiz yönlendirici arabirimi dizini

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* This example adds a default router for the primary interface at
   fe80::1219:B9FF:FE37:ac to the default router table. */

#define PRIMARY_INTERFACE 0

NXD_ADDRESS router_address;

/* Set the router address version to IPv6 */
router_address.nxd_ip_version   = NX_IP_VERSION_V6;

/* Set the IPv6 address, in host byte order. */
router_address.nxd_ip_address[0] = 0xfe800000;
router_address.nxd_ip_address[1] = 0x0;
router_address.nxd_ip_address[2] = 0x1219B9FF;
router_address.nxd_ip_address[3] = 0xFE3700AC;

/* Set IPv6 default router. */
status = nxd_ipv6_default_router_add(ip_ptr, &router_address,
                                     0xFFFF, PRIMARY_INTERFACE);

/* Unless invalid pointer input is detected by the error checking
   Service, status return is always NX_SUCCESS. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nxd_ipv6_default_router_delete"></a>nxd_ipv6_default_router_delete
IPv6 yönlendiricisini varsayılan yönlendirici tablosundan kaldır

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_default_router_delete (
    NX_IP *ip_ptr,
    NXD_ADDRESS *router_address);
```
### <a name="description"></a>Description

Bu hizmet varsayılan yönlendirici tablosundan bir IPv6 varsayılan yönlendirici siler. Eşdeğer NetX IPv4 hizmeti ***nx_ip_gateway_address_clear***.

### <a name="restrictions"></a>Kısıtlamalar

IP örneği oluşturuldu. *router_address* geçerli bilgilere işaret etmelidir.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Önceden oluşturulmuş bir IP örneğine yönelik işaretçi
- **router_address** IPv6 varsayılan ağ geçidi adresine yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) yönlendirici başarıyla silindi
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değildir.
- **NX_NOT_FOUND** (0x4E) yönlendirici girişi bulunamıyor
- **NX_PTR_ERROR** (0x07) geçersiz IP örneği veya depolama alanı
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı
- **NX_INVALID_PARAMETERS** (0x82) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/*This example removes a default router:fe80::1219:B9FF:FE37:ac */

NXD_ADDRESS router_address;

/* Set the router_address version to IPv6 */
router_address.nxd_ip_version = NX_IP_VERSION_V6;

/* Program the IPv6 address, in host byte order. */
router_address.nxd_ip_address[0] = 0xfe800000;
router_address.nxd_ip_address[1] = 0x0;
router_address.nxd_ip_address[2] = 0x1219B9FF;
router_address.nxd_ip_address[3] = 0xFE3700AC;

/* Delete the IPv6 default router. */
nxd_ipv6_default_router_delete(ip_ptr, &router_address);
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_clearnx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_getnx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nxd_ipv6_default_router_entry_get"></a>nxd_ipv6_default_router_entry_get
Varsayılan yönlendirici girişini al

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_default_router_entry_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    UINT entry_index,
    NXD_ADDRESS *router_addr,
    ULONG *router_lifetime,
    ULONG *prefix_length,
    ULONG *configuration_method);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen ağ cihazına bağlı varsayılan IPv6 yönlendirme tablosundan bir yönlendirici girişi alır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **interface_index** Ağ arabiriminin dizini
- **entry_index** Giriş dizini
- **router_addr** Yönlendirici IPv6 adresi
- **router_lifetime** Yönlendirici yaşam süresi işaretçisi
- **prefix_length** Önek uzunluğu işaretçisi
- **configuration_method** Girişin nasıl yapılandırıldığına ilişkin bilgi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) başarılı al
- **NX_NOT_FOUND** (0x4E) yönlendirici girdisi bulunamadı
- **NX_INVALID_INTERFACE** (0x4C) arabirim dizini geçerli değil
- **NX_PTR_ERROR** (0x07) geçersiz IP denetimi blok işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0
NXD_ADDRESS            router_addr;
ULONG                  router_lifetime;
ULONG                  prefix_length;
ULONG                  configuration_method;

/* Get the router entry of specified interface. */
status = nxd_ipv6_default_router_entry_get (&ip_0,
                                            PRIMARY_INTERFACE,
                                            entry_index,
                                            &router_addr,
                                            &router_lifetime,
                                            &prefix_length,
                                            &configuration_method);

/* If status == NX_SUCCESS, the router entry was successfully
   got. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nxd_ipv6_default_router_get"></a>nxd_ipv6_default_router_get
Varsayılan yönlendirici tablosundan bir IPv6 yönlendiricisi al

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_default_router_get(
    NX_IP *ip_ptr, 
    UINT interface_index
    NXD_ADDRESS *router_address,
    ULONG *router_lifetime,
    ULONG *prefix_length);
```
### <a name="description"></a>Description

Bu hizmet, varsayılan yönlendirici tablosundan belirtilen fiziksel arabirimdeki IPv6 varsayılan yönlendirici adresini, yaşam süresini ve ön ek uzunluğunu alır. Eşdeğer NetX IPv4 hizmeti, ***nx_ip_gateway_address_get *.**

*router_address* geçerli bir NXD_ADDRESS yapısına işaret etmelidir, bu nedenle bu hizmet varsayılan yönlendiricinin IPv6 adresini doldurabilirler.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi
- **interface_index** Yönlendiricinin erişebileceği ağ arabirimine olan Dizin
- **router_address** Ana bilgisayar bayt düzeninde varsayılan yönlendirici adresinin dönüş değeri için depolama alanı işaretçisi.
- **router_lifetime** Yönlendirici ömrü işaretçisi
- **prefix_length** Yönlendirici adresi önek uzunluğu işaretçisi

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) varsayılan yönlendirici başarıyla eklendi
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değildir.
- **NX_NOT_FOUND** (0x4E) varsayılan yönlendirici bulunamadı
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı
- **NX_INVALID_INTERFACE** (0x4C) geçersiz yönlendirici arabirimi dizini
- **NX_PTR_ERROR** (0x07) geçersiz IP örneği veya depolama alanı

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* This example retrieves a default router for the primary device
   from the default router table. */

#define PRIMARY_INTERFACE 0

NXD_ADDRESS router_address;
ULONG       router_lifetime;
ULONG       prefix_length;

/* Get IPv6 default router. */
status = nxd_ipv6_default_router_get(ip_ptr, PRIMARY_INTERFACE,
                                     &router_address,
                                     &router_lifetime,
                                     &prefix_length);

/* If status returns NX_SUCCESS, the router address and related
   information is returned successfully. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nxd_ipv6_default_router_number_of_entries_get"></a>nxd_ipv6_default_router_number_of_entries_get
Varsayılan IPv6 yönlendiricileri sayısını Al

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_default_router_number_of_entries_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    UINT *num_entries);
```
### <a name="description"></a>Description

Bu hizmet, belirli bir ağ arabiriminde yapılandırılan IPv6 varsayılan yönlendirici sayısını alır.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP denetim bloğu işaretçisi
- **interface_index** Ağ arabiriminin dizini
- **num_entries** Belirtilen ağ cihazında IPv6 yönlendirici sayısı için hedef

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) başarılı al
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değildir.
- **NX_INVALID_INTERFACE** (0x4C) cihaz dizini değeri geçerli değil
- **NX_PTR_ERROR** (0x07) geçersiz IP denetim bloğu işaretçisi veya num_entries işaretçisi

### <a name="allowed-from"></a>İzin verilen

İş Parçacığı

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0
UINT                   num_entries;

/* Get the router entries of specified interface. */
status = nxd_ipv6_default_router_number_of_entries_get(&ip_0,
                                                       PRIMARY_INTERFACE,
                                                       &num_entries);

/* If status == NX_SUCCESS, the router entries was successfully
   retrieved. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get

## <a name="nxd_ipv6_disable"></a>nxd_ipv6_disable
IPv6 özelliğini devre dışı bırak

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_disable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneği için IPv6 'Yı devre dışı bırakır. Ayrıca, varsayılan yönlendirici tablosu, ND önbelleği ve IPv6 adresi tablosunu da temizler, tüm çok noktaya yayın gruplarını bırakır ve Yönlendirici isteme değişkenlerini sıfırlar. IPv6 etkinleştirilmemişse bu hizmetin hiçbir etkisi yoktur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP örnek işaretçisi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) başarılı devre dışı
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değildir.
- **NX_PTR_ERROR** (0x07) geçersiz IP denetimi blok işaretçisi
- **NX_NOT_SUPPORT** (0x4b) IPv6 modülü derlenmedi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* Disable IPv6 feature on this IP instance. */
status = nxd_ipv6_disable(&ip_0);

/* If status == NX_SUCCESS, disables IPv6 feature on IP instance.*/
```
### <a name="see-also"></a>Ayrıca Bkz. 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_enable"></a>nxd_ipv6_enable
IPv6 Hizmetlerini Etkinleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet, IPv6 hizmetlerini sağlar. IPv6 hizmetleri etkinleştirildiğinde, IP örneği tüm düğümlü çok noktaya yayın grubuna (FF02::1) katılır. Bu hizmet, bağlantı yerel adresini veya genel adresini ayarlamaz. Uygulamalar, cihaz *nxd_ipv6_address_set* adreslerini yapılandırmak için ağ iletişimlerini kullan olmalıdır. NetX eşdeğeri yoktur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğinin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) IPv6 başarıyla etkinleştirildi
- **NX_ALREADY_ENABLED** (0x15) IPv6 zaten etkin
- **NX_NOT_SUPPORTED** (0x4B) IPv6 özelliği NetX Duo kitaplığında yerleşik değildir.
- **NX_PTR_ERROR** (0x07) Geçersiz IP işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* First create an IP instance with packet pool, source address, and
   driver.*/
status = nx_ip_create(&ip_0, "NetX IP Instance 0",
                      IP_ADDRESS(1,2,3,4),
                      0xFFFFFF00UL, &pool_0,_nx_ram_network_driver,
                      pointer, 2048, 1);

/* Then enable IPv6 on the IP instance. */
status = nxd_ipv6_enable(&ip_0);

/* A status return of NX_SUCCESS indicates that the IP instance is
   enabled for IPv6 services. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_multicast_interface_join"></a>nxd_ipv6_multicast_interface_join
IPv6 çok noktaya yayın grubuna katılma

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_multicast_interface_join(
    NX_IP *ip_ptr,
    NXD_ADDRESS *group_address,
    UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, bir uygulamanın belirli bir ağ arabiriminde belirli bir IPv6 çok noktaya yayın adresini birleştirmeye olanak sağlar. Bağlantı sürücüsüne çok noktaya yayın adresini eklemesi bildirildi. Bu hizmet, NetX Duo kitaplığı tanımlanan seçenekle ***NX_ENABLE_IPV6_MULTICAST*** kullanılabilir.

### <a name="parameters"></a>Parametreler  

- **ip_ptr** IP örneği işaretçisi
- **group_address** IPv6 çok noktaya yayın adresi
- **interface_index** Çok noktaya yayın grubuyla ilişkili ağ arabiriminin dizini

### <a name="return-values"></a>Dönüş Değerleri  

- **NX_SUCCESS** (0x00) IPv6 çok noktaya yayın adresinin almayı başarıyla etkinleştirmesi
- **NX_NO_MORE_ENTRIES** (0x17) IPv6 çok noktaya yayın tablosunda artık giriş yok.
- **NX_OVERFLOW** (0x03) Cihaz sürücüsünde artık grup adresi yok
- **NX_NOT_SUPPORTED** (0x4B) IPv6 özelliği veya IPv6 çok noktaya yayın özelliği NetX Duo kitaplığında yerleşik değil
- **NX_PTR_ERROR** (0x07) Geçersiz IP denetim bloğu işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz IPv6 adresi
- **NX_INVALID_INTERFACE** (0x4C) Arabirim dizini geçerli değil

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0

/* Join multicast group on this IP instance. */
status = nxd_ipv6_multicast_interface_join(&ip_0,
                                           &group_address,
                                           PRIMARY_INTERFACE);

/* If status == NX_SUCCESS, interface of index on IP instance
   has joined the multicast group. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_leave

## <a name="nxd_ipv6_multicast_interface_leave"></a>nxd_ipv6_multicast_interface_leave
IPv6 çok noktaya yayın grubu bırakma

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_multicast_interface_leave(
    NX_IP *ip_ptr,
    NXD_ADDRESS *group_address,
    UINT interface_index);
```
### <a name="description"></a>Description

Bu hizmet, belirli bir IPv6 çok noktaya yayın adresini belirli bir ağ cihazından kaldırır. Bağlantı sürücüsüne IPv6 çok noktaya yayın adresinin kaldırılması da bildirildi. Bu hizmet, NetX Duo kitaplığı tanımlanan seçenekle ***NX_ENABLE_IPV6_MULTICAST*** kullanılabilir.

### <a name="parameters"></a>Parametreler  

- **ip_ptr** IP örneği işaretçisi
- **group_address** IPv6 çok noktaya yayın adresi
- **interface_index** Grupla ilişkilendirilmiş ağ arabiriminin dizini

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Başarılı çok noktaya yayın bırakma
- **NX_ENTRY_NOT_FOUND** (0x16) Girdisi bulunamadı
- **NX_NOT_SUPPORTED** (0x4B) IPv6 özelliği veya IPv6 çok noktaya yayın özelliği NetX Duo kitaplığında yerleşik değil
- **NX_PTR_ERROR** (0x07) Geçersiz IP denetim bloğu işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz IPv6 adresi
- **NX_INVALID_INTERFACE** (0x4C) Arabirim dizini geçerli değil

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0

/* Leave multicast address on this IP instance. */
status = nxd_ipv6_multicast_interface_leave(&ip_0,
                                            &group_address,
                                            primary_interface);

/* If status == NX_SUCCESS, interface of index on IP instance
   has left the multicast group. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join

## <a name="nxd_ipv6_stateless_address_autoconfig_disable"></a>nxd_ipv6_stateless_address_autoconfig_disable
Durum bilgileri olmayan adres otomatik yapılandırmayı devre dışı bırakma

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_stateless_address_autoconfig_disable(
    NX_IP *ip_ptr,
    UINT interface_index);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen bir ağ cihazında IPv6 durum bilgisiz adres otomatik yapılandırma özelliğini devre dışı bırakıyor. IPv6 adresi yapılandırılmışsa hiçbir etkisi olmaz.

Bu hizmet, NetX Duo kitaplığı tanımlanan seçenekle NX_IPV6_STATELESS_AUTOCONFIG_CONTROL ***kullanılabilir.***

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP örneği işaretçisi
- **interface_index** IPv6 durum bilgisiz adres otomatik yapılandırmasının devre dışı bırakılacak ağ arabirimi dizini.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Durum bilgileri olmayan adres otomatik yapılandırma özelliğini başarıyla devre dışı bırakmıştır.
- **NX_NOT_SUPPORTED** (0x4B) IPv6 özelliği veya IPv6 durum bilgisiz adres otomatik yapılandırma denetimi özelliği NetX Duo kitaplığında yerleşik değil
- **NX_INVALID_INTERFACE** (0x4C) Arabirim dizini geçerli değil
- **NX_PTR_ERROR** (0x07) Geçersiz IP denetim bloğu işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE 0

/* Disable stateless address auto configuration on this IP instance. */
status = nxd_ipv6_stateless_address_autoconfig_disable(&ip_0,
                                                       PRIMARY_INTERFACE);

/* If status == NX_SUCCESS, disables stateless address auto
   configuration on IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz. 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_stateless_address_autoconfig_enable"></a>nxd_ipv6_stateless_address_autoconfig_enable
Durum bilgileri olmayan adres otomatik yapılandırmayı etkinleştirme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_ipv6_stateless_address_autoconfig_enable(
    NX_IP *ip_ptr,
    UINT interface_index);
```
### <a name="description"></a>Description

Bu hizmet, belirtilen bir ağ cihazında IPv6 durum bilgisiz adres otomatik yapılandırma özelliğini sağlar.

Bu hizmet, NetX Duo kitaplığı tanımlanan seçenekle NX_IPV6_STATELESS_AUTOCONFIG_CONTROL ***kullanılabilir.***

### <a name="parameters"></a>Parametreler 

- **ip_ptr** IP örneği işaretçisi
- **interface_index** IPv6 durum bilgisiz adres otomatik yapılandırmasının etkinleştirilmesi gereken ağ arabirimi dizini.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Durum bilgisiz adres otomatik yapılandırma özelliğini başarıyla sağlar.
- **NX_ALREADY_ENABLED** (0x15) Zaten etkin
- **NX_NOT_SUPPORTED** (0x4B) IPv6 özelliği veya IPv6 durum bilgisiz adres otomatik yapılandırma denetimi özelliği NetX Duo kitaplığında yerleşik değil
- **NX_INVALID_INTERFACE** (0x4C) Arabirim dizini geçerli değil
- **NX_PTR_ERROR** (0x07) Geçersiz IP denetim bloğu işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
#define PRIMARY_INTERFACE

/* Enable stateless address auto configuration on this
   IP instance. */
status = nxd_ipv6_stateless_address_autoconfig_enable(&ip_0,
                                                      PRIMARY_INTERFACE);

/* If status == NX_SUCCESS, enables stateless address auto
   configuration on IP instance. */
```
### <a name="see-also"></a>Ayrıca Bkz. 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable

## <a name="nxd_nd_cache_entry_delete"></a>nxd_nd_cache_entry_delete
Komşu Önbelleğinde IPv6 Adresi girişini silme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_nd_cache_entry_delete(
    NX_IP *ip_ptr, 
    ULONG *ip_address);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan IP adresi için bir IPv6 komşu bulma önbelleği girdisini siler. Eşdeğer NetX IPv4 işlevi ***nx_arp_static_entry_delete.***

### <a name="parameters"></a>Parametreler

- **ip_ptr** Daha önce oluşturulan IP örneğine işaretçi
- **ip_address** Silinecek IPv6 adresi işaretçisi, konak byte sırasına göre

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Adresi başarıyla sildi
- **NX_ENTRY_NOT_FOUND** (0x16) Adresi IPv6 komşu önbelleğinde bulunamadı
- **NX_NOT_SUPPORTED** (0x4B) IPv6 özelliği NetX Duo kitaplığında yerleşik değil
- **NX_PTR_ERROR** (0x07) Geçersiz IP örneği veya depolama alanı
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

Başlatma, iş parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* This example deletes an entry from the neighbor cache table. */

NXD_ADDRESS ip_address;

ip_address.nxd_ip_address_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]   = 0x20011234;
ip_address.nxd_ip_address.v6[1]   = 0x56780000;
ip_address.nxd_ip_address.v6[2]   = 0;
ip_address.nxd_ip_address.v6[3]   = 1;

/* Delete an entry in the neighbor cache table with the specified IPv6
   address and hardware address. */
status = nxd_nd_cache_entry_delete(&ip_0,
                                   &ip_address.nxd_ip_address.v6[0]);

/* If status == NX_SUCCESS, the entry was deleted from the neighbor cache
   table. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nxd_nd_cache_entry_set"></a>nxd_nd_cache_entry_set
Komşu Önbelleğine IPv6 Adresi/MAC Eşlemesi Ekleme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_nd_cache_entry_set(
    NX_IP *ip_ptr, 
    NXD_ADDRESS *dest_ip,
    UINT interface_index, 
    char *mac);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen IP adresi için komşu bulma önbelleğine, belirtilen ip_address arabirimi *dizininde* (interface_index) donanım MAC adresine eşlenmiş bir giriş ekler. Eşdeğer NetX IPv4 hizmeti ***nx_arp_static_entry_create.***

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine işaretçi
- **dest_ip** IPv6 adresi örneğine işaretçi
- **interface_index** Hedef IPv6 adresine ulaşılanın fiziksel ağ arabirimini belirten dizin 
- **mac** Donanım adresi işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Girdisi başarıyla eklendi
- **NX_NOT_SUCCESSFUL** (0x43) Geçersiz önbellek veya komşu önbelleği girdisi yok
- **NX_NOT_SUPPORTED** (0x4B) IPv6 özelliği NetX Duo kitaplığında yerleşik değil
- **NX_PTR_ERROR** (0x07) Geçersiz IP örneği veya depolama alanı
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz
- **NX_INVALID_INTERFACE** (0x4C) Geçersiz arabirim dizini değeri.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* This example adds an entry on the primary network interface to
   the neighbor cache table. */

#define PRIMARY_INTEFACE 0

NXD_ADDRESS ip_address;
UCHAR hw_address[6] = {0x0, 0xcf,0x01,0x02, 0x03, 0x04};
CHAR  *mac;

mac = (CHAR *)&hw_address[0];

ip_address.nxd_ip_address_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]   = 0x20011234;
ip_address.nxd_ip_address.v6[1]   = 0x56780000;
ip_address.nxd_ip_address.v6[2]   = 0;
ip_address.nxd_ip_address.v6[3]   = 1;

/* Create an entry in the neighbor cache table with the specified
   IPv6 address and hardware address. */
status = nxd_nd_cache_entry_set(&ip_0,
                                &ip_address.nxd_ip_address.v6[0],
                                PRIMARY_INTERFACE, mac);

/* If status == NX_SUCCESS, the entry was added to the neighbor
   cache table. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nxd_nd_cache_hardware_address_find"></a>nxd_nd_cache_hardware_address_find
IPv6 Adresi için Donanım Adresi Bulma

### <a name="prototype"></a>Prototype  

```c
UINT nxd_nd_cache_hardware_address_find(
    NX_IP *ip_ptr,
    NXD_ADDRESS *ip_address,
    ULONG *physical_msw,
    ULONG *physical_lsw
    UINT *interface_index);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan IPv6 adresiyle ilişkili IPv6 komşu bulma önbelleğinde bir fiziksel donanım adresi bulmaya çalışır. Komşuya ulaşılanın ağ arabirimi dizini, ağ arabiriminin *interface_index.* Eşdeğer NetX IPv4 hizmeti ***nx_arp_hardware_address_find.***

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine işaretçi
- **ip_address** Bulmak için IP adresi işaretçisi, konak byte sırası
- **physical_msw** Konak byte sırasına göre fiziksel adresin ilk 16 biti (47-32) işaretçisi 
- **physical_lsw** Konak byte sırasına göre fiziksel adresin alt 32 biti (31-0) işaretçisi
- **interface_index** IPv6 adresine erişilen ağ aygıtını belirten arabirim dizini için geçerli bellek konumunun işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) adresi başarıyla buldu
- **NX_ENTRY_NOT_FOUND** (0x16) eşleme, komşu önbelleğinde değil
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değil
- **NX_INVALID_PARAMETERS** (0x4D) sağlanan IP adresi 6. sürümde değil.
- **NX_PTR_ERROR** (0x07) geçersiz IP örneği veya depolama alanı
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* This example inputs an IP address on the primary network in order
   to obtain the hardware address it is mapped to in the neighbor
   cache able. */

NXD_ADDRESS  ip_address;
ULONG physical_msw, physical_lsw;
UINT  interface_index;

ip_address.nxd_ip_address_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]   = 0x20011234;
ip_address.nxd_ip_address.v6[1]   = 0x56780000;
ip_address.nxd_ip_address.v6[2]   = 0;
ip_address.nxd_ip_address.v6[3]   = 1;

/* Obtain the hardware address mapped to the supplied global IPv6
   address. */
status = nxd_nd_cache_hardware_address_find(&ip_0, &ip_address,
                                            &physical_msw,
                                            &physical_lsw
                                            &interface_index);

/* If status == NX_SUCCESS, a matching entry was found in the
   neighbor cache table and the hardware address returned in
   variables physical_msw and physical_lsw, the index of the network
   interface through which the neighbor can be reached is stored in
   interface_index. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nxd_nd_cache_invalidate"></a>nxd_nd_cache_invalidate
Komşu bulma önbelleğini geçersiz kılın

### <a name="prototype"></a>Prototype  

```c
UINT nxd_nd_cache_invalidate(NX_IP *ip_ptr);
```
### <a name="description"></a>Description

Bu hizmet IPv6 komşu bulma önbelleğinin tamamını geçersiz kılar. Bu hizmet, ICMPv6 etkinleştirildikten önce veya sonra çağrılabilir. Bu hizmet IPv4 bağlantısı için geçerli değildir, bu nedenle NetX eşdeğeri hizmet yoktur.

### <a name="parameters"></a>Parametreler

- **ip_ptr** IP örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) önbelleği başarıyla geçersiz kılındı
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değil
- **NX_PTR_ERROR** (0x07) geçersiz IP örneği
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* This example invalidates the host neighbor cache table. */

/* Invalidate the cache table bound to the IP instance. */
status = nxd_nd_cache_invalidate (&ip_0);

/* If status == NX_SUCCESS, all entries in the neighbor cache table
   are invalidated. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_ip_address_find

## <a name="nxd_nd_cache_ip_address_find"></a>nxd_nd_cache_ip_address_find
Fiziksel bir adres için IPv6 adresini al

### <a name="prototype"></a>Prototype  

```c
UINT nxd_nd_cache_ip_address_find(
    NX_IP *ip_ptr,
    NXD_ADDRESS *ip_address,
    ULONG physical_msw,
    ULONG physical_lsw,
    UINT *interface_index);
```
### <a name="description"></a>Description

Bu hizmet, sağlanan fiziksel adresle ilişkili IPv6 komşu bulma önbelleğinde bir IPv6 adresi bulmaya çalışır. Komşunuzun ulaşılbileceği ağ arabiriminin dizini de döndürülür. Eşdeğer NetX IPv4 hizmeti ***nx_arp_ip_address_find***.

### <a name="parameters"></a>Parametreler 

- **ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi
- **ip_address** Geçerli NXD_ADDRESS yapısına yönelik işaretçi
- **physical_msw** Bulunacak fiziksel adresin ilk 16 bit (47-32), ana bilgisayar bayt sıralaması
- **physical_lsw** Bulunacak fiziksel adresin düşük 32 bitleri (31-0), ana bilgisayar bayt sıralaması
- **interface_index** IPv6 adresine erişilebileceği ağ aygıtı dizinine yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) adresi başarıyla buldu
- **NX_ENTRY_NOT_FOUND** (0x16) fiziksel adres, komşu önbelleğinde bulunamadı
- **NX_NOT_SUPPORTED** (0x4b) IPv6 özelliği NETX Duo kitaplığında yerleşik değil
- **NX_PTR_ERROR** (0x07) geçersiz IP örneği veya depolama alanı
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı 
- **NX_INVALID_PARAMETERS** (0x4D) MAC adresi sıfırdır.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
/* This example inputs a hardware address to search on for the
   matching IPv6 global address in the neighbor cache table. */

NXD_ADDRESS ip_address;
ULONG physical_msw = 0xcf;
ULONG physical_lsw = 0x01020304;
UINT  interface_index;

/* Obtain the IPv6 address mapped to the supplied hardware
   Address on the primary device. */
status = nxd_nd_cache_ip_address_find(&ip_0, &ip_address,
                                      physical_msw, physical_lsw,
                                      &interface_index);

/* If status == NX_SUCCESS, a matching entry was found in the
   neighbor cache table and the global IPv6 address returned in
   variable ip_address. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate

## <a name="nxd_tcp_client_socket_connect"></a>nxd_tcp_client_socket_connect
TCP bağlantısı oluşturma

### <a name="prototype"></a>Prototype  

```c
UINT nxd_tcp_client_socket_connect(
    NX_TCP_SOCKET *socket_ptr
    NXD_ADDRESSS *server_ip,
    UINT server_port,
    ULONG wait_option);
```
### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir TCP istemci yuvasını belirtilen sunucunun bağlantı noktasına kullanarak TCP bağlantısı yapar. Bu hizmet, IPv4 veya IPv6 ağlarında çalışmaktadır. Geçerli TCP sunucusu bağlantı noktaları 0 ile 0xFFFF arasındadır. NetX Duo, sunucu IP adresine göre uygun fiziksel arabirimi belirler. NetX IPv4 eşdeğeri ***nx_tcp_client_socket_connect***.

Yuva bir yerel bağlantı noktası ile bağlantılı olmalıdır.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan TCP yuvasına yönelik işaretçi
- **server_ip** Ana bilgisayar bayt düzeninde IPv4 veya IPv6 hedef adresi işaretçisi
- **SERVER_PORT** Ana bilgisayar bayt düzeninde Bağlanılacak sunucu bağlantı noktası numarası (1 ila 0xFFFF)
- **wait_option** Bağlantı kurulurken bekle seçeneği. Bekleme seçenekleri aşağıdaki gibi tanımlanır:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xffffffff)
    - **ticks içinde zaman aşımı değeri** (0x00000001-0xfffffffe)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı yuva bağlantısı
- **NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi
- **NX_IP_ADDRESS_ERROR** (0x21) geçersiz sunucu IPv4 veya IPv6 adresi
- **NX_NOT_BOUND** (0x24) yuva bağlanmadı
- **NX_NOT_CLOSED** (0x35) yuva kapalı durumda değil
- **NX_IN_PROGRESS** (0x37) hiçbir bekleme belirtilmedi, bağlantı girişimi devam ediyor
- **NX_INVALID_INTERFACE** (0x4C) geçersiz arabirim dizini.
- **NX_NO_INTERFACE_ADDRESS** (0x50) ağ arabiriminin geçerli bir IPv6 adresi yok
- **NX_NOT_ENABLED** (0x14) TCP etkin değil
- **NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası
- **NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı
- **NX_NOT_CONNECTED** (0x38) bağlantı başarısız olur.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
NXD_ADDRESS peer_ip_address;
ULONG       peer_port;

/* Set Peer IPv6 address */
peer_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
peer_ip_address.nxd_ip_address.v6[0] = 0x20010000;
peer_ip_address.nxd_ip_address.v6[1] = 0;
peer_ip_address.nxd_ip_address.v6[2] = 0;
peer_ip_address.nxd_ip_address.v6[3] = 0x101;

/* Set peer port number */
peer_port = 2563;

/* Connect to the peer */
status = nxd_tcp_client_socket_connect(socket_ptr,
                                       &peer_ip_address,
                                       peer_port, NX_WAIT_FOREVER);
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_socket_peer_info_get

## <a name="nxd_tcp_socket_peer_info_get"></a>nxd_tcp_socket_peer_info_get
Eş TCP yuvası IP adresini ve bağlantı noktası numarasını alır

### <a name="prototype"></a>Prototype  

```c
UINT nxd_tcp_socket_peer_info_get
    (NX_TCP_SOCKET *socket_ptr,
    NXD_ADDRESS *peer_ip_address,
    ULONG *peer_port);
```
### <a name="description"></a>Description

Bu hizmet, bağlı TCP yuvasının eş IP adresini ve bağlantı noktası bilgilerini IPv4 veya IPv6 ağı üzerinden alır. Eşdeğer NetX IPv4 hizmeti ***nx_tcp_socket_peer_info_get***.

*Socket_ptr* , zaten bağlı durumda olan bir TCP yuvasına işaret etmelidir.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Eş konağa bağlı TCP yuvası işaretçisi
- **peer_ip_address** IPv4 veya IPv6 eş adresi işaretçisi. Döndürülen IP adresi ana bilgisayar bayt düzeninde.
- **peer_port** Eş bağlantı noktası numarası işaretçisi. Döndürülen bağlantı noktası numarası ana bilgisayar bayt düzeninde.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) yuva bilgileri başarıyla alındı
- **NX_NOT_CONNECTED** (0x38) yuva eşe bağlı değil
- **NX_NOT_ENABLED** (0x14) TCP etkin değil
- **NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi
- **NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önalım mümkün

No

### <a name="example"></a>Örnek

```c
NXD_ADDRESS  peer_ip_address;
ULONG        peer_port;

/* Get TCP socket information. */
status = nxd_tcp_socket_peer_info_get(socket_ptr, &peer_ip_address,
                                      &peer_port);

/* If status == NX_SUCCESS, the service returns valid peer info: */
if(peer_ip_address.nxd_ip_version == NX_IP_VERSION_V4)
    /* Peer IP address is stored in
       peer_ip_address.nxd_ip_address.v4 */

if(peer_ip_address.nxd_ip_version == NX_IP_VERSION_V6)
    /* Peer IP address is stored in
       peer_ip_address.nxd_ip_address.v6 */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect

## <a name="nxd_udp_packet_info_extract"></a>nxd_udp_packet_info_extract
UDP paketinden ağ parametrelerini ayıklama

### <a name="prototype"></a>Prototype  

```c
UINT nxd_udp_packet_info_extract(
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *ip_address,
    UINT *protocol,
    UINT *port,
    UINT *interface_index);
```
### <a name="description"></a>Description

Bu hizmet, IPv4 veya IPv6 UDP ağlarında alınan bir paketten ağ parametrelerini ayıklar. NetX eşdeğer hizmeti ***nx_udp_packet_info_extract.***

### <a name="parameters"></a>Parametreler

- **packet_ptr** Paket işaretçisi.
- **ip_address** Gönderen IP adresinin işaretçisi.
- **protokol** Döndürülen protokolün işaretçisi.
- **bağlantı noktası** Gönderenin bağlantı noktası numarasının işaretçisi.
- **interface_index** Bu paketin alınarak ağ arabirimi dizininin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri 

- **NX_SUCCESS** (0x00) Paket arabirimi verileri başarıyla ayıklandı.
- **NX_INVALID_PACKET** (0x12) Paketi ne IPv4 ne de IPv6'dır.
- **NX_PTR_ERROR** (0x07) Geçersiz işaretçi girişi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
/* Extract network data from UDP packet interface.*/
status = nxd_udp_packet_info_extract(packet_ptr, &ip_address,
                                    &protocol, &port,
                                    &interface_index);

/* If status is NX_SUCCESS packet data was successfully retrieved.*/
```
### <a name="see-also"></a>Ayrıca Bkz. 

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nxd_udp_socket_send"></a>nxd_udp_socket_send
UDP Veri Birimi gönderme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_udp_socket_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *ip_address,
    UINT port);
```
### <a name="description"></a>Description

Bu hizmet, IPv4 veya IPv6 ağları için önceden oluşturulmuş ve bağlı bir UDP yuvası üzerinden bir UDP veri birimi gönderir. NetX Duo, hedef IP adresine göre kaynak adres olarak uygun bir yerel IP adresi bulur. Uygulama, belirli bir arabirimi ve kaynak IP  adresini belirtmek için nxd_udp_socket_source_send kullanmalıdır.

UDP veri biriminin başarıyla gönderip gönderilmeden bağımsız olarak bu hizmetin hemen döndür olduğunu unutmayın. NetX (IPv4) eşdeğer hizmeti ***nx_udp_socket_send.***

Yuvanın yerel bir bağlantı noktasına bağlı olması gerekir.

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğinin işaretçisi
- **packet_ptr** UDP veri birimi paket işaretçisi
- **ip_address** Hedef IPv4 veya IPv6 adresinin işaretçisi
- **bağlantı noktası** Konak byte sırasına göre 1 ile 0xFFFF arasında geçerli hedef bağlantı noktası numarası

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı UDP yuva gönderme
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz sunucu IPv4 veya IPv6 adresi
- **NX_NOT_BOUND** (0x24) Yuva hiçbir bağlantı noktasına bağlı değil
- **NX_NO_INTERFACE_ADDRESS** (0x50) Uygun bir giden arabirim bulunamadı.
- **NX_UNDERFLOW** (0x02) Pakette UDP üst bilgisi için yeterli alan yok
- **NX_OVERFLOW** (0x03) Paket ekleme işaretçisi geçersiz
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi, adres işaretçisi veya paket işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz
- **NX_NOT_ENABLED** (0x14) UDP etkinleştirilmedi
- **NX_INVALID_PORT** (0x46) Bağlantı noktası numarası geçerli bir aralık içinde değil

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
NXD_ADDRESS ip_address, server_address;

/* Set the UDP Client IPv6 address. */
ip_address.nxd_ip_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0] = 0x20010000;
ip_address.nxd_ip_address.v6[1] = 0;
ip_address.nxd_ip_address.v6[2] = 0;
ip_address.nxd_ip_address.v6[3] = 1;

/* Set the UDP server IPv6 address to send to. */
server_address.nxd_ip_version = NX_IP_VERSION_V6;
server_address.nxd_ip_address.v6[0] = 0x20010000;
server_address.nxd_ip_address.v6[1] = 0;
server_address.nxd_ip_address.v6[2] = 0;
server_address.nxd_ip_address.v6[3] = 2;

/* Set the global address (indicated by the 64 bit prefix) using the
   IPv6 address just created on the primary device (index 0). We
   don’t need the index into the address table, so the last argument
   is set to null. */

interface_index = 0;
status = nxd_ipv6_address_set(&client_ip, interface_index,
                              &ip_address, 64, NX_NULL);

/* Create the UDP socket client_socket with the ip_address and
   allocate a packet pointed to by packet_ptr (not shown). */

/* Send a packet to the UDP server at server_address on port 12. */
status = nxd_udp_socket_send(&client_socket, packet_ptr,
                             &server_address, 12);

/* If status == NX_SUCCESS, the UDP host successfully transmitted
   the packet out the UDP socket to the server. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nxd_udp_socket_source_send"></a>nxd_udp_socket_source_send
UDP Veri Birimi gönderme

### <a name="prototype"></a>Prototype  

```c
UINT nxd_udp_socket_source_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *ip_address,
    UINT port, 
    UINT address_index);
```
### <a name="description"></a>Description

Bu hizmet, IPv4 veya IPv6 ağları için önceden oluşturulmuş ve bağlı bir UDP yuvası üzerinden bir UDP veri birimi gönderir. Parametre *address_index* giden paket için kullanmak üzere kaynak IP adresini belirtir. UDP veri biriminin başarıyla gönderip gönderilmeden bağımsız olarak işlevinin hemen döndür olduğunu unutmayın.

Yuvanın yerel bir bağlantı noktasına bağlı olması gerekir.

NetX (IPv4) eşdeğer hizmeti ***nx_udp_socket_source_send.***

### <a name="parameters"></a>Parametreler

- **socket_ptr** Daha önce oluşturulan UDP yuva örneğinin işaretçisi
- **packet_ptr** UDP veri birimi paket işaretçisi
- **ip_address** Ana bilgisayar sırasına göre hedef IPv4 veya IPv6 adres bağlantı noktası için işaretçi 1 ile 0xFFFF arasında geçerli hedef bağlantı noktası numarası)
- **address_index** Paket için kullanmak üzere kaynak adresi belirten dizin

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı UDP yuva gönderme
- **NX_IP_ADDRESS_ERROR** (0x21) Geçersiz sunucu IPv4 veya IPv6 adresi
- **NX_NOT_BOUND** (0x24) Yuva hiçbir bağlantı noktasına bağlı değil
- **NX_NO_INTERFACE_ADDRESS** (0x50) Uygun bir giden arabirim bulunamadı.
- **NX_NOT_FOUND** (0x4E) Uygun arabirim bulunamadı
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi, adresi veya paket işaretçisi.
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz
- **NX_NOT_ENABLED** (0x14) UDP etkinleştirilmedi
- **NX_INVALID_PORT** (0x46) Bağlantı noktası numarası geçerli aralık içinde değil.
- **NX_INVALID_INTERFACE** (0x4C) Belirtilen ağ arabirimi geçerli
- **NX_UNDERFLOW** (0x02) Pakette UDP üst bilgisi için yeterli alan yok
- **NX_OVERFLOW** (0x03) Paket ekleme işaretçisi geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
NXD_ADDRESS ip_address, server_address;
UINT address_index;

/* Set the UDP Client IPv6 address. */
ip_address.nxd_ip_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0] = 0x20010000;
ip_address.nxd_ip_address.v6[1] = 0;
ip_address.nxd_ip_address.v6[2] = 0;
ip_address.nxd_ip_address.v6[3] = 1;

/* Set the UDP server IPv6 address to send to. */
server_address.nxd_ip_version = NX_IP_VERSION_V6;
server_address.nxd_ip_address.v6[0] = 0x20010000;
server_address.nxd_ip_address.v6[1] = 0;
server_address.nxd_ip_address.v6[2] = 0;
server_address.nxd_ip_address.v6[3] = 2;

/* Set the global address (indicated by the 64 bit prefix) using the IPv6
   address just created on the primary device (index 0). The address index
   is needed for nxd_udp_socket_source_send. */

status = nxd_ipv6_address_set(&client_ip, 0,
                              &ip_address, 64, &address_index);

/* Create the UDP socket client_socket with the ip_address and
   allocate a packet pointed to by packet_ptr (not shown). */

/* Send a packet to the UDP server at server_address on port 12. */
status = nxd_udp_socket_source_send(&client_socket, packet_ptr,
                                    &server_address, 12, address_index);

/* If status == NX_SUCCESS, the UDP host successfully transmitted the
   packet out the UDP socket to the server. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_source_extract

## <a name="nxd_udp_source_extract"></a>nxd_udp_source_extract
UPD Paket Kaynağı Bilgilerini Alma

### <a name="prototype"></a>Prototype  

```c
UINT nxd_udp_source_extract(
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *ip_address, 
    UINT *port);
```
### <a name="description"></a>Description

Bu hizmet, konak UDP yuvası üzerinden alınan bir UDP paketinden kaynak IP adresini ve bağlantı noktası numarasını ayıklar. NetX (IPv4) eşdeğeri, ***nx_udp_source_extract.***

### <a name="parameters"></a>Parametreler

- **packet_ptr** Alınan UDP paketinin işaretçisi
- **ip_address** Paket NXD_ADDRESS IP adresini depolamak için uygulama yapısına işaretçi
- **bağlantı noktası** UDP yuva bağlantı noktası numarası işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı kaynak ayıklama
- **NX_INVALID_PACKET** (0x12) Paketi geçerli değil
- **NX_PTR_ERROR** (0x07) Geçersiz yuva işaretçisi
- **NX_CALLER_ERROR** (0x11) Bu hizmetin çağıranı geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="preemption-possible"></a>Önserme Olası

No

### <a name="example"></a>Örnek

```c
NXD_ADDRESS ip_address;
UINT         port;

/* Create the UDP socket client_socket and
   allocate the packet pointed to by packet_ptr (not shown). */

/* Extract the IP address and port of the packet received on the UDP
   socket specified in the packet interface. */
status = nxd_udp_source_extract(&packet_ptr, &ip_address, &port);

/* If status == NX_SUCCESS, the source IP address and port of the
   packet received on the UDP socket was successfully extracted. */
```
### <a name="see-also"></a>Ayrıca Bkz.

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send