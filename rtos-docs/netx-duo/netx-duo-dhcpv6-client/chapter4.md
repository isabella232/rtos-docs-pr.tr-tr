---
title: Bölüm 4 - Azure RTOS NetX Duo DHCPv6 İstemci hizmetleri
description: Bu bölümde tüm NetX Duo DHCPv6 Azure RTOS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6caf943f990f8fe5cbd2cd6139a1253fcaf47dc207141963e31a9e31864ef839
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791746"
---
# <a name="chapter-4---azure-rtos-netx-duo-dhcpv6-client-services"></a>Bölüm 4 - Azure RTOS NetX Duo DHCPv6 İstemci hizmetleri

Bu bölümde tüm NetX Duo DHCPv6 Azure RTOS hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklaması yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_dhcpv6_client_create:** *DHCPv6 İstemci örneği oluşturma* 

- **nx_dhcpv6_client_delete:** *DHCPv6 İstemci örneğini silme* 

- **nx_dhcpv6_create_ client_duid:** *DHCPv6 İstemciSI DUID oluşturma* 

- **nx_dhcpv6 _add_client_ia:** *DHCPv6 İstemci Kimliği Adresi (IA) ekleme* 

- **nx_dhcpv6 _create_client_ia:** (*Eski Bir DHCPv6 İstemci Kimliği Adresi (IA) Ekleme)* 

- **nx_dhcpv6_create_client_iana:** *Geçici Olmayan Adresler (IANA) için DHCPv6* İstemci Kimliği İlişkisi Oluşturma 

- **nx_dhcpv6_get_client_duid_time_id:** *DHCPv6 İstemciSI DUID'den saat kimliğini al* 

- **nx_dhcpv6_client_set_interface:** *DHCPv6 Sunucusu ile iletişim için İstemci ağ arabirimini ayarlama* 

- **nx_dhcpv6_get_IP_address:** *DHCPv6 istemcisine atanan genel IPv6 adresini al* 

- **nx_dhcpv6_get_lease_time_data:** İstemci genel IPv6 adresi için *T1, T2, geçerli* ve tercih edilen yaşam sürelerini al

- **nx_dhcpv6_get_valid_ip_address_lease_time:** Adres dizinine göre DHCPv6 İstemci IPv6 adresi için *T1, T2,* geçerli ve tercih edilen yaşam sürelerini al 

- **nx_dhcpv6_get_iana_lease_time:** *Kimlik İlişkisi'nde (IANA) DHCPv6* İstemcisi'ne kiralanan T1 ve T2'leri al 

- **nx_dhcpv6_get_other_option_data:** Etki alanı adı veya saat dilimi *sunucusu gibi belirtilen seçenek verilerini alma* 

- **nx_dhcpv6_get_DNS_server_address:** *Belirtilen dizinde DNS Sunucusu adresini DHCPv6 İstemciSI DNS sunucusu listesine alın* 

- **nx_dhcpv6_get_time_accrued:** Genel IPv6 adresi kirası tahakkuk eden *zaman DHCPv6* İstemcisi'ne bağlandı 

- **nx_dhcpv6_get_time_server_address:** Belirtilen dizinde Saat *Sunucusu adresini DHCPv6 İstemci Zamanı sunucu listesine alın*

- **nx_dhcpv6_get_valid_ip_address_count:** *DHCPv6 İstemcisi'ne atanan IPv6 adreslerinin sayısını al* 

- **nx_dhcpv6_reinitialize:** DHCPv6 İstemci durumu makinesini yeniden başlatmak ve DHCPv6 protokolünü yeniden çalıştırmak için *DHCPv6'yı yeniden başlatın* 

- **nx_dhcpv6_request_confirm:** *Sunucuya CONFIRM isteği gönderme* 

- **nx_dhcpv6_request_inform_request:** S *sunucuya bir INFORM REQUEST iletisi sona erer* 

- **nx_dhcpv6_request_release:** *Sunucuya YAYıN isteği gönderme* 

- **nx_dhcpv6_request_option_DNS_server:** *İstek iletisinde İstemci seçeneği istek verilerine DNS sunucusu seçeneğini Sunucuya ekleme* 

- **nx_dhcpv6_request_option_FQDN:** *sunucuya gönderilen istek iletisinde İstemci seçeneği istek verilerine FQDN seçeneğini ekleyin* 

- **nx_dhcpv6_request_option_domain_name:** *sunucuya gönderilen istek iletisinde İstemci seçeneği istek verilerine etki alanı adı seçeneğini ekleyin* 

- **nx_dhcpv6_request_option_time_server:** *İstek iletisinde İstemci seçeneği istek verilerine sunucuya saat sunucusu seçeneğini ekleyin* 

- **nx_dhcpv6_request_option_timezone:** *İstek iletisinde İstemci seçeneği istek verilerine sunucuya saat dilimi seçeneğini ekleyin* 

- **nx_dhcpv6_request_solicit:** İstemci ağı (yayın) üzerinde herhangi bir *Sunucuya DHCPv6 SOLICIT isteği gönderme* 

- **nx_dhcpv6_request_solicit_rapid:** Hızlı Yürütme seçeneği ayarlanmış şekilde İstemci ağı (yayın) üzerinde herhangi bir Sunucuya *DHCPv6 SOLICIT isteği gönderme* 

- **nx_dhcpv6_resume:** *DHCPv6 İstemcisini İşlemeyi Sürdürme* 

- **nx_dhcpv6_start:** *DHCPv6 İstemci iş parçacığı görevini başlatma. Bunun DHCPv6 durum makinesini başlatmaya eşdeğer* olmadığını ve bir SOLICIT isteği göndermez 

- **nx_dhcpv6_stop:** *DHCPv6 İstemci iş parçacığı görevini durdurun* 

- **nx_dhcpv6_suspend:** *DHCPv6 İstemci iş parçacığı görevini askıya alma* 

- **nx_dhcpv6_set_time_accrued:** İstemci kaydında genel İstemci *IPv6 adresi kirası için tahakkuk eden zamanı ayarlayın.*

## <a name="nx_dhcpv6_client_create"></a>nx_dhcpv6_client_create

DHCPv6 istemci örneği oluşturma

### <a name="prototype"></a>Prototype

```C
UINT  nx_dhcpv6_client_create(NX_DHCPV6 *dhcpv6_ptr, 
                        NX_IP *ip_ptr, CHAR *name_ptr, 
                        NX_PACKET_POOL *packet_pool_ptr, 
                        VOID *stack_ptr, ULONG stack_size,
                        VOID (*dhcpv6_state_change_notify)
                                 (struct NX_DHCPV6_STRUCT *dhcpv6_ptr, 
                                  UINT old_state, UINT new_state), 
                        VOID (*dhcpv6_server_error_handler)
                                 (struct NX_DHCPV6_STRUCT *dhcpv6_ptr, 
                                 UINT op_code, UINT status_code, 
                                 UINT message_type));
```

### <a name="description"></a>Description

Bu hizmet, geri çağırma işlevlerini içeren bir DHCPv6 istemci örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 denetim bloğu işaretçisi  

- **ip_ptr** İstemci IP örneğine işaretçi  

- **name_ptr** DHCPv6 örneği için ad işaretçisi

- **packet_pool_ptr** İstemci paket havuzu işaretçisi

- **stack_ptr** İstemci yığını belleği işaretçisi

- **stack_size** İstemci yığın belleğinin boyutu

- **dhcpv6_state_change_notify** İstemci sunucuya yeni bir DHCPv6 isteği başlattığında çağrılan geri çağırma işlevinin işaretçisi

- **dhcpv6_server_error_handler** İstemci sunucudan hata durumu aldığında çağrılan geri çağırma işlevinin işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı İstemci oluşturma

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_DHCPV6_PARAM_ERROR (0xE93) İşaretçi olmayan giriş geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Create a DHCPv6 client instance without specifying link local or preferred
   global IP address.  */
status =  nx_dhcpv6_client_create(&dhcp_0, &ip_0, "DHCPv6 Client", &pool_0,
                                  NULL, NULL, pointer, 2048,        
                                  dhcpv6_state_change_notify, 
                                  dhcpv6_server_error_handler);

/* If status is NX_SUCCESS a DHCPv6 client instance was successfully
   created.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_client_delete

## <a name="nx_dhcpv6_client_delete"></a>nx_dhcpv6_client_delete

DHCPv6 İstemci örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_client_delete(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir DHCPv6 istemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 istemci örneğine işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Başarılı DHCPv6 silme

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_DHCPV6_PARAM_ERROR (0xE93) İşaretçi olmayan giriş geçersiz

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Delete a DHCPv6 client instance.  */
status =  nx_dhcpv6_client_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCPv6 client instance was successfully
   deleted.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_client_create

## <a name="nx_dhcpv6_client_set_interface"></a>nx_dhcpv6_client_set_interface

DHCPv6 için İstemcinin Ağ Arabirimini Ayarlar

### <a name="prototype"></a>Prototype

```C
UINT    nx_dhcpv6_client_set_interface(NX_DHCPV6 *dhcpv6_ptr, 
                                       UINT *interface_index);
```

### <a name="description"></a>Description

Bu hizmet, İstemcinin ağ arabirimini DHCPv6 Sunucularla belirtilen giriş arabirimi dizinine iletişim kurmak için ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

- **interface_index** Ağ arabirimini gösteren dizin

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Arabirimi başarıyla ayarlanmış

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_INVALID_INTERFACE (0x4C) Geçersiz arabirim dizini girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the client interface for DHCPv6 communication with the Server to 
   the secondary interface (1). */

UINT index = 1;
status = nx_dhcpv6_client_set_interface(&dhcp_0, index);

/* If status is NX_SUCCESS, the Client successfully set 
   the DHCPv6 network interface.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_client _create
- nx_dhcpv6_start

## <a name="nx_dhcpv6_client_set_destination_address"></a>nx_dhcpv6_client_set_destination_address

DHCPv6 iletisi gönderilecek hedef adresi ayarlar

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_client_set_destination_address(NX_DHCPV6 *dhcpv6_ptr,
                                              NXD_ADDRESS *destination_address);
```

### <a name="description"></a>Description

Bu hizmet, DHCPv6 iletisi gönderilecek hedef adresi ayarlar. Varsayılan olarak ALL_DHCP_Relay_Agents_and_Servers (FF02:: 1:2).

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **destination_address** Hedef adres

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) arabirimi başarıyla ayarlandı

- NX_PTR_ERROR (0x07) geçersiz işaretçi girişi

- NX_DHCPV6_PARAM_ERROR (0xE93) parametre hatası

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the destination address where DHCPv6 message should be sent to. */

NXD_ADDRESS dest_address; /* Set the destination address.  */

status = nx_dhcpv6_client_set_destination_address(&dhcp_0, &dest_address);

/* If status is NX_SUCCESS, the Client successfully set the destination address. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_client _create
- nx_dhcpv6_start

## <a name="nx_dhcpv6_create_client_duid"></a>nx_dhcpv6_create_client_duid

Istemci DUıD nesnesi oluştur

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_create_client_duid(NX_DHCPV6 *dhcpv6_ptr,
                                  UINT duid_type, UINT hardware_type,
                                  ULONG time);
```

### <a name="description"></a>Description

Bu hizmet, giriş parametreleriyle Istemci DUıD 'sini oluşturur. Zaman girişi sağlanmazsa ve DUID türü bağlantı katmanını zamana göre gösteriyorsa, bu işlev benzersizlik için rastgele bir faktör içeren bir zaman sağlar. Satıcı atanmış (Kurumsal) DUID türleri desteklenmez.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **duid_type** DUıD türü (donanım, kuruluş vb.)

- **hardware_type** Ağ donanımı ör. IEEE 802

- **zaman** Benzersiz tanımlayıcı oluşturmak için kullanılan değer

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı istemci DUID 'si oluşturuldu

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi

- NX_DHCPV6_UNSUPPORTED_DUID_TYPE (0xE98) DUıD türü bilinmiyor veya desteklenmiyor 

- NX_DHCPV6_UNSUPPORTED_DUID_HW_TYPE (0xE99) DUıD donanım türü bilinmiyor veya desteklenmiyor

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Create the Client DUID from the supplied input.
   The time field is left NULL so the DHCPv6 client will provide one.  */
status = nx_dhcpv6_create_client_duid(&dhcp_0, NX_DHCPV6_DUID_TYPE_LINK_TIME,
                                      NX_DHCPV6_HW_TYPE_IEEE_802, 0)

/* If status is NX_SUCCESS the client DUID was successfully created.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_create_client_ia
- nx_dhcpv6_create_client_iana
- nx_dhcpv6_create_server_duid

## <a name="nx_dhcpv6_create_client_ia"></a>nx_dhcpv6_create_client_ia

Istemciye bir kimlik Ilişkilendirmesi ekleme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_create_client_ia(NX_DHCPV6 *dhcpv6_ptr,
                                NXD_ADDRESS *ipv6_address,
                                ULONG preferred_lifetime,
                                ULONG valid_lifetime);
```

### <a name="description"></a>Description

Bu hizmet *nx_dhcpv6_add_client_ia* hizmetiyle aynıdır. Istemci kaydını sağlanan parametrelerle doldurarak bir Istemci kimliği Ilişkilendirmesi ekler. En fazla tercih edilen ve geçerli yaşam sürelerini istemek için, bu parametreleri sonsuz olarak ayarlayın. Bir DHCPv6 Istemcisine birden fazla IA eklemek için NX_DHCPV6_MAX_IA_ADDRESS varsayılan değer olan 1 ' den daha yüksek bir değere ayarlayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **ipv6_address** NetX Duo IP adres bloğunun işaretçisi

- **preferred_lifetime** IP adresi kullanım dışı olmadan önce geçen sürenin uzunluğu

- **valid_lifetime** IP adresinin süresi dolmadan önce geçen süre

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı istemci IA eklendi

- **NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xeaf) yinelenen IA adresi 

- **NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0xeae) IA, en fazla IAS istemcisinin depolayabileceği sınırı aşıyor

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) IA 'da geçersiz (örn. null) IA adresi

- NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi


### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Add an Client IA using the supplied input.   */
status = nx_dhcpv6_create_client_ia(&dhcp_0, &ipv6_address, 
NX_DHCPV6_PREFERRED_LIFETIME, NX_DHCPV6_VALID_LIFETIME);

/* If status is NX_SUCCESS the client IA was successfully added.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_add_client_duid
- nx_dhcpv6_create_server_duid
- nx_dhcpv6_create_client_iana

## <a name="nx_dhcpv6_create_client_iana"></a>nx_dhcpv6_create_client_iana

Istemci için bir kimlik Ilişkisi (geçici olmayan) oluşturma

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_create_client_iana(NX_DHCPV6 *dhcpv6_ptr, 
                                  UINT IA_ident, ULONG T1, ULONG T2);
```

### <a name="description"></a>Description

Bu hizmet, sağlanan parametrelerden geçici olmayan bir Istemci kimlik Ilişkisi (ıANA) oluşturur. T1 ve T2 sürelerini DHCPv6 Istemci isteklerinde maksimum (Infinity) olarak ayarlamak için, bu parametreleri NX_DHCPV6_INFINITE_LEASE olarak ayarlayın. 

> [!NOTE]
> Bir Istemcide yalnızca bir ıANA vardır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **IA_ident** Kimlik Ilişkilendirmesi benzersiz tanımlayıcısı

- **T1** Istemci, IPv6 adresi yenilemeyi başlatması gereken zaman

- **T2** Istemci theIPv6 adresi yeniden bağlama başlatması gereken zaman

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IANA başarıyla oluşturuldu

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Create the Client IANA from the supplied input.  */
status = nx_dhcpv6_create_client_iana(&dhcp_0, DHCPV6_IA_ID, DHCPV6_T1,   
                                      DHCPV6_T2);

/* If status is NX_SUCCESS the client IANA was successfully created.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_create_client_duid
- nx_dhcpv6_create_server_duid
- nx_dhcpv6_add_client_ia

## <a name="nx_dhcpv6_add_client_ia"></a>nx_dhcpv6_add_client_ia 

Istemciye bir kimlik Ilişkilendirmesi ekleme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_add_client_ia(NX_DHCPV6 *dhcpv6_ptr, 
                             NXD_ADDRESS *ipv6_address, 
                             ULONG preferred_lifetime, 
                             ULONG valid_lifetime);
```

### <a name="description"></a>Description

Bu hizmet, Istemci kaydını sağlanan parametrelerle doldurarak bir Istemci kimliği Ilişkilendirmesi ekler. En fazla tercih edilen ve geçerli yaşam sürelerini istemek için, bu parametreleri sonsuz olarak ayarlayın. Bir DHCPv6 Istemcisine birden fazla IA eklemek için NX_DHCPV6_MAX_IA_ADDRESS varsayılan değer olan 1 ' den daha yüksek bir değere ayarlayın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **ipv6_address** NetX Duo IP adres bloğunun işaretçisi

- **preferred_lifetime** IP adresi kullanım dışı olmadan önce geçen sürenin uzunluğu

- **valid_lifetime** IP adresinin süresi dolmadan önce geçen süre 

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı istemci IA eklendi

- **NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xeaf) yinelenen IA adresi 

- **NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0xeae) IA, en fazla IAS istemcisinin depolayabileceği sınırı aşıyor

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) IA 'da geçersiz (örn. null) IA adresi

- NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi

 
### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Add an Client IA using the supplied input.   */
status = nx_dhcpv6_add_client_ia(&dhcp_0, &ipv6_address, 
                                 NX_DHCPV6_PREFERRED_LIFETIME,
                                 NX_DHCPV6_VALID_LIFETIME);

/* If status is NX_SUCCESS the client IA was successfully added.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_create_client_duid
- nx_dhcpv6_create_server_duid
- nx_dhcpv6_create_client_iana

## <a name="nx_dhcpv6_get_client_duid_time_id"></a>nx_dhcpv6_get_client_duid_time_id

Istemci DUıD 'sinden saat KIMLIĞINI alır

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_get_client_duid_time_id(NX_DHCPV6 *dhcpv6_ptr, ULONG *time_id);
```

### <a name="description"></a>Description

Bu hizmet, Istemci DUıD 'sinden saat KIMLIĞI alanını alır. Uygulamanın, DHCPv6 Istemci örneğindeki Istemci DUıD 'sini doldurması için *nx_dhcpv6_create_client_duid* çağrısı olması veya bu alan için null değere sahip olması gerekir. Amaç, uygulamanın bu verileri kaydetmesi ve zaman alanı da dahil olmak üzere sunucuya aynı Istemci DUıD 'sini sunmaktır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **time_id** Istemci DUıD saat alanı işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IP Kiralama verileri başarıyla alındı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Retrieve the time ID from the Client DUID.  */
status = nx_dhcpv6_get_client_duid_time_id(&dhcp_0, &time_ID);

/* If status is NX_SUCCESS the time ID was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_time_lease_data
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_get_ip_address"></a>nx_dhcpv6_get_IP_address

Istemcinin genel IPv6 adresini alır

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_get_IP_address(NX_DHCPV6 *dhcpv6_ptr, 
                              NXD_ADDRESS *ip_address);
```

### <a name="description"></a>Description

Bu hizmet, Istemcinin genel IPv6 adresini alır. Istemcinin geçerli bir adresi yoksa bir hata durumu döndürülür. Bir Istemcide birden fazla genel IPv6 adresi varsa, birincil IPv6 adresi döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **ip_address** IPv6 adresi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IPv6 adresi başarıyla atandı

- **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xead) IPv6 adresi geçerli değil

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
UINT address_status;
UINT address_index;

/* Retrieve the client’s assigned IP address.  */
status = nx_dhcpv6_get_IP_address(&dhcp_0, &ipv6_address);

/* If status is NX_SUCCESS the client IP address was assigned.
   Now register it with NetX Duo on the primary interface (index zero). 
   The address index is returned in the address_index field*/
status = nxd_ipv6_address_set(&ip_0, 0, &ipv6_address, 64, &address_index);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_client_duid_time_id
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_get_lease_time_data"></a>nx_dhcpv6_get_lease_time_data

Istemcinin IA adresi kiralama süresi verilerini alır

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_get_lease_time_data(NX_DHCPV6 *dhcpv6_ptr, ULONG *T1, 
                                   ULONG *T2, ULONG *preferred_lifetime, 
                                   ULONG *valid_lifetime);
```

### <a name="description"></a>Description

Bu hizmet, Istemcinin genel IA adres saat verilerini alır. Istemci IA adresi durumu geçersizse, zaman verileri sıfır olarak ayarlanır ve başarılı bir tamamlanma durumu döndürülür. Bir Istemcide birden fazla genel IPv6 adresi varsa, birincil IA adres verileri döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **T1** IA adres yenileme zamanı işaretçisi

- **T2** IA adresi yeniden bağlama saati işaretçisi

- **preferred_lifetime** IA adresinin kullanım dışı olduğu zaman işaretçisi

- **valid_lifetime** IA adresinin süresi dolduğunda zaman işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IA kira verileri başarıyla alındı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Retrieve the client’s assigned IA lease data.  */
status = nx_dhcpv6_get_lease_time_data(&dhcp_0, &T1, &T2, &preferred_lifetime, 
                                       &valid_lifetime);

/* If status is NX_SUCCESS the client IA address lease data was retrieved.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_client_duid_time_id
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_time_accrued
- nx_dhcpv6_get_iana_lease_time

## <a name="nx_dhcpv6_get_iana-lease_time"></a>nx_dhcpv6_get_iana lease_time

Istemcinin ıANA kira süresi verilerini alma

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_get_iana_lease_time(NX_DHCPV6 *dhcpv6_ptr, ULONG *T1, 
                                    ULONG *T2);
```

### <a name="description"></a>Description

Bu hizmet, Istemcinin Global IA-NA kira süresi verilerini (T1 ve T2) alır. Hiçbir Istemci IA-yok adresinin geçerli bir adres durumu yoksa, zaman verileri sıfır olarak ayarlanır ve başarılı bir tamamlanma durumu döndürülür. Bir Istemcide birden fazla genel IPv6 adresi varsa, birincil IA adres verileri döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **T1** Kira yenilemesi başlatmak için zaman işaretçisi

- **T2** Kira yeniden bağlamasının başlaması için zaman işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IANA kira verileri başarıyla alındı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Retrieve the client’s assigned IANA lease data.  */
status = nx_dhcpv6_get_iana_lease_time(&dhcp_0, &T1, &T2);

/* If status is NX_SUCCESS the client IA address lease data was retrieved.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_client_duid_time_id
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_time_accrued
- nx_dhcpv6_get_lease_time_data

## <a name="nx_dhcpv6_get_valid_ip_address_count"></a>nx_dhcpv6_get_valid_ip_address_count

Istemcinin geçerli IA adresleri sayısını alma

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_get_valid_ip_address_count(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT *address_count);
```

### <a name="description"></a>Description

Bu hizmet, Istemcinin geçerli IPv6 adreslerinin sayısını alır. Istemciye geçerli bir IPv6 adresi (atandı) bağlanır ve IP örneğiyle kaydedilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **address_count** Döndürülecek adres sayısı işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IANA kira verileri başarıyla alındı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
UINT address_count; 

/* Retrieve the count of valid IA-NA addresses.  */
status = nx_dhcpv6_get_valid_ip_address_count(&dhcp_0, &address_count);

/* If status is NX_SUCCESS the client IA address count was retrieved.  */
```

## <a name="nx_dhcpv6_get_valid_ip_address_lease_time"></a>nx_dhcpv6_get_valid_ip_address_lease_time

Istemci IA verilerini adres dizinine göre al

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_get_valid_ip_address_lease_time(NX_DHCPV6 *dhcpv6_ptr, 
                                               UINT address_index,
                                               NXD_ADDRESS *ip_address,
                                               ULONG *preferred_lifetime,
                                               ULONG *valid_lifetime);
```

### <a name="description"></a>Description

Bu hizmet, Istemcinin IA adresini ve kira verilerini adres dizinine göre alır. Geçersiz bir dizin sağlanırsa veya bu dizindeki IPv6 adresi geçerli değilse, hizmet NX_DHCPV6_IA_ADDRESS_NOT_VALID bir hata durumu döndürür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **address_index** DHCPv6 IA tablosuna Dizin

- **ip_address** Alınacak IPv6 adresine yönelik işaretçi

- **preferred_lifetime** IA adresinin kullanım dışı olduğu zaman işaretçisi

- **valid_lifetime** IA adresinin süresi dolduğunda zaman işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) IANA verileri başarıyla alındı

- Belirtilen dizinde geçersiz bir dizin veya geçerli bir IPv6 adresi **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xead) 

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
UINT address_index = 1; 
NXD_ADDRESS *ip_address;

/* Retrieve the IPv6 address, and valid and preferred lifetime for the IA record
   Saved at index 1 in the DHCPv6 table.  */
status = nx_dhcpv6_get_valid_ip_address_lease_time(&dhcp_0, address_index, 
                                                   &ip_address, 
                                                   &preferred_lifetime,  
                                                   &valid_lifetime);

/* If status is NX_SUCCESS the client IA address and lease data were retrieved.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_iana_lease_time
- nx_dhcpv6_get_lease_time_data

## <a name="nx_dhcpv6_get_dns_server_address"></a>nx_dhcpv6_get_DNS_server_address

DNS sunucusu adresini alır 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_get_DNS_server_address(NX_DHCPV6 *dhcpv6_ptr, UINT index,
                                      NXD_ADDRESS *server_address);
```

### <a name="description"></a>Description

Bu hizmet, Istemci listesinde belirtilen dizindeki DNS sunucusu IPv6 adresi verilerini alır. Listede dizin üzerinde bir sunucu adresi yoksa bir hata döndürülür. Dizin, DNS sunucusu listesinin boyutunu aşmayabilir NX_DHCPV6_NUM_DNS_SERVERS Kullanıcı tarafından yapılandırılabilir seçeneği ile belirtilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **Dizin** DNS sunucusu listesinde Dizin

- **server_address** Sunucu adresi arabelleği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) adresi başarıyla alındı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Retrieve the DNS server at the specified index in the list. */

UINT index = 0;
NXD_ADDRESS server_address;


        status = nx_dhcpv6_get_DNS_server_address(&dhcp_0, index, &server_address);

/* If status == NX_SUCCESS, the DNS server IP address successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_get_other_option_data"></a>nx_dhcpv6_get_other_option_data

DHCPv6 seçenek verilerini alır 

### <a name="prototype"></a>Prototype

```C
UINT  nx_dhcpv6_get_other_option_data(NX_DHCPV6 *dhcpv6_ptr, 
                                      UINT option_code, UCHAR *buffer);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen seçenek kodu için DHCPv6 iletisinden DHCPv6 seçenek verilerini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- alınacak veriler için **seçenek** kodu seçenek kodu

- **arabellek** Verilerin kopyalanacağı arabelleğin işaretçisi 

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) seçenek verileri başarıyla alındı

- **NX_DHCPV6_UNKNOWN_OPTION** (0xeab) bilinmeyen/desteklenmeyen seçenek kodu

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Retrieve the option data specified by the input option code. */
status = nx_dhcpv6_get_other_option_data(&dhcp_0, option_code, buffer);

/* If status is NX_SUCCESS the option data was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_get_time_accrued"></a>nx_dhcpv6_get_time_accrued

Istemcinin IP adresi kiralamasında tahakkuk eden süreyi alır

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_get_time_accrued(NX_DHCPV6 *dhcpv6_ptr, ULONG *time_accrued);
```

### <a name="description"></a>Description

Bu hizmet, Istemcinin IPv6 adresi kiralamasında tahakkuk eden süreyi alır. İşlevi, ilk geçerli adres için Istemciye atanan tüm IPv6 adreslerini denetler. Geçerli adres bulunamasa, tahakkuk eden zaman için sıfır değeri döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

- **time_accrued** IP kiralamada tahakkuk eden zaman işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Tahakkuk eden süre başarıyla alındı

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Retrieve time accrued time on the Client address lease. */
status = nx_dhcpv6_get_time_accrued(&dhcp_0, &time_accrued);

/* If status is NX_SUCCESS the time accrued on the client IP address 
   lease was retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_set_time_accrued

## <a name="nx_dhcpv6_get_time_server_address"></a>nx_dhcpv6_get_time_server_address

Zaman Sunucusu adresini alma 

### <a name="prototype"></a>Prototype

```C
UINT  nx_dhcpv6_get_time_server_address(NX_DHCPV6 *dhcpv6_ptr, UINT index, 
                                        NXD_ADDRESS *server_address);
```

### <a name="description"></a>Description

Bu hizmet, İstemci listesinde belirtilen dizinde Saat sunucusu IPv6 adresi verilerini verir. Listede dizinde bir sunucu adresi yoksa bir hata döndürülür. Dizin, Zaman Sunucusu listesinin kullanıcı tarafından yapılandırılabilir seçenek tarafından belirtilen boyutunu aşabilir NX_DHCPV6_NUM_TIME_SERVERS.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

- **dizin** Zaman Sunucusu listesinde dizin oluşturma

- **server_address** Sunucu adresi arabelleği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Adresi başarıyla alındı

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Retrieve the Time server at the specified index in the list. */

UINT index = 0;
NXD_ADDRESS server_address;


      status = nx_dhcpv6_get_time_server_address(&dhcp_0, index, &server_address);

/* If status == NX_SUCCESS, the Time server IP address successfully retrieved. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_time_accrued
- nx_dhcpv6_get_DNS_server_address

## <a name="nx_dhcpv6_reinitialize"></a>nx_dhcpv6_reinitialize

IP tablosundan İstemci IP adresini kaldırma

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_reinitialize(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet, DHCPv6 durum makinesini yeniden başlatmak ve DHCPv6 protokolünü yeniden çalıştırarak İstemciyi yeniden başlatıyor. İstemci daha önce DHPCv6 durum makinesini başlatmamışsa veya herhangi bir IPv6 adresi atanmışsa bu gerekli değildir. DHCPv6 İstemcisi'ne kaydedilen ve IP örneğiyle kaydedilen adreslerin her ikisi de temizlendi.

> [!NOTE]
> Uygulamanın yine de nx_dhcpv6_start hizmetini kullanarak  DHCPv6 İstemcisini başlatması ve nx_dhcpv6_request_solicit çağırarak IPv6 adresi *ataması isteğini başlatması gerekir.*

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Adresi başarıyla kaldırıldı

- **NX_DHCPV6_ALREADY_STARTED** (0xE91) DHCPv6 İstemcisi zaten çalışıyor

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Clear the assigned IP address(es) from the Client and the IP instance */
status = nx_dhcpv6_reinitialize(&dhcp_0);

/* If status is NX_SUCCESS the Client IP address was successfully removed. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_stop
- nx_dhcpv6_start

## <a name="nx_dhcpv6_request_confirm"></a>nx_dhcpv6_request_confirm

İstemcinin CONFIRM durumunu işleme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_confirm(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir CONFIRM isteği gönderir. Sunucudan bir yanıt alınıyorsa, DHCPv6 İstemcisi kira parametrelerini alınan verilerle günceller.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) CONFIRM iletisi başarıyla gönderildi ve işlendi

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send a CONFIRM message to the Server. */
status = nx_dhcpv6_request_confirm(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the CONFIRM message. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_request_inform_request
- nx_dhcpv6_request_release
- nx_dhcpv6_request_solicit


## <a name="nx_dhcpv6_request_inform_request"></a>nx_dhcpv6_request_inform_request

İstemcinin INFORM REQUEST durumunu işleme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_inform_request(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet bir INFORM REQUEST iletisi gönderir. Yanıt alınırsa, Bir yanıt alınırsa, yanıt geçerli olduğunu belirlemek için işlenir ve sunucu isteği verdi. İstemci örneği daha sonra gerektiğinde sunucu bilgileriyle güncelleştirilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) INFORM REQUEST iletisi başarıyla oluşturuldu ve işlendi

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send an INFORM REQUEST message to the server. */
status = nx_dhcpv6_request_inform_request(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the INFORM REQUEST 
   message and processed the reply. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_request_confirm

## <a name="nx_dhcpv6_request_option_dns_server"></a>nx_dhcpv6_request_option_DNS_server

DHCPv6 Seçenek isteğine DNS Sunucusu ekleme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_DNS_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet, DHCPv6 seçenek isteğine DNS sunucusu bilgileri isteği için seçeneğini ekler. Sunucu yanıtı DNS sunucusu verilerini içerirse, İstemci DNS sunucusunu depolar ve dns sunucusunu depolar. İstemcinin depolay olduğu DNS sunucusu sayısı, varsayılan değeri 2 olan NX_DHCPV6_NUM_DNS_SERVERS yapılandırılabilir seçenek tarafından belirlenir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DNS sunucusu seçeneği dahil edildi

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the DNS server option in Client requests. */
nx_dhcpv6_request_option_DNS_server(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_request_option_domain_name
- nx_dhcpv6_request_option_time_server
- nx_dhcpv6_request_option_timezone

## <a name="nx_dhcpv6_request_option_fqdn"></a>nx_dhcpv6_request_option_FQDN

Seçenek isteği listesine Tam Etki Alanı Adı ekle seçeneği

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_FQDN(NX_DHCPV6 *dhcpv6_ptr, UCHAR *domain_name, 
UINT op);
```

### <a name="description"></a>Description

Bu hizmet, DHCPv6 seçenek isteğine İstemci Tam Etki Alanı Adı ekleme seçeneğini ekler. FQDN seçeneği için üç seçenek vardır:

- NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR 0 İstemci tarafından kullanılan FQDN ve adresler için FQDN'den IPv6'ya adres eşlemesini güncelleştirin.

- NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE 1 İstemci tarafından sunucuya kullanılan FQDN ve adresler için FQDN'den IPv6'ya adres eşlemesini güncelleştirin.

- NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE 2 Sunucunun İstemci adına DNS güncelleştirmesi gerçekleştirmesini talep edin.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

- **domain_name** Etki alanı adını tutan dize

- **op (op)** Uygulanacak FQDN seçeneğinin türü (yukarıdaki listeye bakın)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FQDN seçeneği dahil edildi

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the FQDN option in Client DHCPv6 request. */
nx_dhcpv6_request_option_FQDN(&dhcp_0, “DHCPv6_Client”, 
                              NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_request_option_domain_name
- nx_dhcpv6_request_option_time_server
- nx_dhcpv6_request_option_timezone

## <a name="nx_dhcpv6_request_option_domain_name"></a>nx_dhcpv6_request_option_domain_name

DHCPv6 seçenek isteğine etki alanı adı seçeneği ekleme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_domain_name(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet, İstemci isteği iletisinde seçenek isteğine etki alanı adı seçeneğini ekler. Sunucu yanıtı etki alanı adı verileri içerirse, etki alanı adının boyutu etki alanı adını tutmak için arabellek boyutu içinde ise İstemci etki alanı adı bilgilerini depolar. Bu arabellek boyutu, varsayılan değeri 30 NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE yapılandırılabilir bir seçenektir (NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE).

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Etki alanı adı seçenek kümesi

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the domain name option in Client requests. */
nx_dhcpv6_request_option_domain_name(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_request_option_DNS_server
- nx_dhcpv6_request_option_time_server
- nx_dhcpv6_request_option_timezone

## <a name="nx_dhcpv6_request_option_time_server"></a>nx_dhcpv6_request_option_time_server

Saat sunucusu verilerini isteğe bağlı istek olarak ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_time_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet, İstemci isteği iletilerinin seçenek isteğine saat sunucusu bilgileri için seçeneğini ekler. Sunucu yanıtı tim sunucusu verilerini içerirse, istemci zaman sunucusunu depolar ve buna yer vardır. İstemcinin depolanabilir sunucu sayısı yapılandırılabilir seçenek tarafından belirlenir

NX_DHCPV6_NUM_TIME _SERVERS değeri 1 olan bir dosyadır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Sunucu seçeneği eklendi

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set the time server option in Client request messages. */
nx_dhcpv6_request_option_time_server(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_request_option_DNS_server
- nx_dhcpv6_request_option_domain_name
- nx_dhcpv6_request_option_timezone

## <a name="nx_dhcpv6_request_option_timezone"></a>nx_dhcpv6_request_option_timezone

Saat dilimi verilerini isteğe bağlı olarak ayarlama

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_timezone(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet, İstemci seçeneği isteğine saat dilimi bilgileri isteği için seçeneğini ekler. Sunucu yanıtı saat dilimi verilerini içerirse, saat diliminin boyutu saat dilimini tutmak için arabellek boyutu içinde ise İstemci saat dilimi bilgilerini depolar. Bu arabellek boyutu, varsayılan değeri 10 NX_DHCPV6_ TIME_ZONE _BUFFER_SIZE yapılandırılabilir bir seçenektir (NX_DHCPV6_ TIME_ZONE _BUFFER_SIZE).

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Saat dilimi seçeneği eklendi

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set time zone option in Client request messages. */
nx_dhcpv6_request_option_timezone(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_request_option_DNS_server
- nx_dhcpv6_request_option_domain_name
- nx_dhcpv6_request_option_time_server

## <a name="nx_dhcpv6_request_release"></a>nx_dhcpv6_request_release

DHCPv6 RELEASE iletisi gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_release(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet, İstemci ağına bir YAYıN iletisi gönderir. İleti başarıyla gönderilirse başarılı bir durum döndürülür. Başarılı bir tamamlama, İstemcinin yanıt aldığı veya henüz bir IPv6 adresi verilmiş olduğu anlamına değildir. DHCPv6 İstemcisi iş parçacığı görevi, bir DHCPv6 Sunucusundan yanıt bekler. Alınan yanıt geçerli olup olmadığını denetler ve verileri İstemci kaydında depolar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) YAYıN iletisi başarıyla gönderildi

- **NX_DHCPV6_NOT_STARTED** (0xE92) DHCPv6 İstemci görevi başlamadı

- **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) adresi İstemciye bağlı değil

- **NX_INVALID_INTERFACE** (0x4C) IP adresi tablosunda bulunamadı

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send an RELEASE message to the Server. */
status = nx_dhcpv6_request_release(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the RELEASE message. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_request_confirm
- nx_dhcpv6_request_inform_request
- nx_dhcpv6_request_solicit

## <a name="nx_dhcpv6_request_solicit"></a>nx_dhcpv6_request_solicit

SOLICIT iletisi gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_solicit(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet ağ üzerinde bir SOLICIT iletisi gönderir. İleti başarıyla gönderilirse başarılı bir durum döndürülür. Başarılı bir tamamlama, İstemcinin yanıt aldığı veya henüz bir IPv6 adresi verilmiş olduğu anlamına değildir. DHCPv6 İstemci iş parçacığı görevi, bir DHCPv6 Sunucusundan bir yanıt (BIR ADVERTISE iletisi) bekler. Yanıt alındı ise yanıtın geçerli olup olmadığını denetler, verileri İstemci kaydına depolar ve İstemciyi REQUEST durumuna yükselter.

> [!NOTE] 
> Hızlı Yürütme seçeneği ayarlanırsa, DHCPv6 İstemcisi geçerli bir Sunucu ADVERTISE iletisi alırsa doğrudan Bağlı durumuna gider. Diğer ayrıntılar için *bkz. nx_dhcpv6_request_solicit_rapid* hizmet açıklaması.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) SOLICIT iletisi başarıyla gönderildi

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send an SOLICIT message to the server. */
status = nx_dhcpv6_request_solicit(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the SOLICIT message. */
```

## <a name="nx_dhcpv6_request_solicit_rapid"></a>nx_dhcpv6_request_solicit_rapid

Hızlı Yürütme seçeneğiyle bir SOLICIT iletisi gönderme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_solicit_rapid(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet, Ağ üzerinde Hızlı Yürütme seçeneği ayarlanmış bir SOLICIT iletisi gönderir. İleti başarıyla gönderilirse başarılı bir durum döndürülür. Başarılı bir tamamlama, İstemcinin yanıt aldığı veya henüz bir IPv6 adresi verilmiş olduğu anlamına değildir. DHCPv6 İstemci iş parçacığı görevi, bir DHCPv6 Sunucusundan bir yanıt (BIR ADVERTISE iletisi) bekler. Alınan yanıt geçerli olup olmadığını denetler, verileri İstemci kaydına depolar ve İstemciyi BOUND durumuna yükselter.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) SOLICIT iletisi başarıyla gönderildi

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send an SOLICIT message to the server. */
status = nx_dhcpv6_request_solicit_rapid(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the SOLICIT message. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_request_solicit
- nx_dhcpv6_request_confirm
- nx_dhcpv6_request_inform_request
- nx_dhcpv6_request_release

## <a name="nx_dhcpv6_resume"></a>nx_dhcpv6_resume

DHCPv6 İstemci görevini sürdürme 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_resume(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet DHCPv6 İstemci iş parçacığı görevini sürdürür. Geçerli DHCPv6 İstemci durumu işlenir (örneğin, Bound, Solicit)

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstemcisi başarıyla sürdürıldı

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Resume the DHCPv6 Client task. */
status = nx_dhcpv6_resume(&dhcp_0);

/* If status is NX_SUCCESS the Client thread task successfully resumed. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_start
- nx_dhcpv6_stop
- nx_dhcpv6_suspend

## <a name="nx_dhcpv6_set_-time_accrued"></a>nx_dhcpv6_set_ time_accrued

İstemcinin IP adresi kirası için tahakkuk eden zamanı ayarlar

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_set_time_accrued(NX_DHCPV6 *dhcpv6_ptr,
                                ULONG time_accrued);
```

### <a name="description"></a>Description

Bu hizmet, sunucu tarafından atandığı için İstemcinin genel IP adresine tahakkuk eden saati ayarlar. Bu yalnızca bir İstemci şu anda atanmış bir IPv6 adresine bağlı ise kullanılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

- **time_accrued** IP kiralamada tahakkuk eden süre

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) Tahakkuk eden süre başarıyla ayarlanmış

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Set time accrued since client’s assigned IP address was assigned. */
status = nx_dhcpv6_set_time_accrued(&dhcp_0, time_accrued);

/* If status is NX_SUCCESS the time accrued on the client IP address lease was 
   successfully set. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_get_IP_address
- nx_dhcpv6_get_other_option_data
- nx_dhcpv6_get_lease_time_data
- nx_dhcpv6_get_time_accrued

## <a name="nx_dhcpv6_start"></a>nx_dhcpv6_start

DHCPv6 İstemcisi görevini başlatma 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_start(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet DHCPv6 İstemcisi görevini başlatır ve İstemciyi DHCPv6 protokolünü çalıştırmaya hazırlar. İstemci örneğinin yeterli bilgiye sahip olduğunu doğrular (örneğin, İstemci DUID'si), DHCPv6 iletilerini göndermek ve almak için UDP yuvasını oluşturur ve bağlar ve oturum süresini ve geçerli IPv6 kira süresinin ne zaman sona erer olduğunu izlemek için süreerleri etkinleştirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstemcisi başarıyla başlatıldı

- **NX_DHCPV6_MISSING_REQUIRED_OPTIONS** (0xEA9) İstemcide gerekli seçenekler eksik

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Start the DHCPv6 Client task. */
status = nx_dhcpv6_start(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully started. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_resume
- nx_dhcpv6_suspend
- nx_dhcpv6_stop
- nx_dhcpv6_reinitialize

## <a name="nx_dhcpv6_stop"></a>nx_dhcpv6_stop

DHCPv6 İstemcisi görevini durdurma 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_stop(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet DHCPv6 İstemcisi görevini durdurur, yeniden iletim sayılarını, en fazla yeniden iletim aralıklarını temizler, oturumu ve kira süre sonu sürelerini devre dışı bırakarak DHCPv6 İstemci yuva bağlantı noktasının bağlantı noktasını devre dışı tutar. İstemciyi yeniden başlatmak için, herhangi bir DHCPv6 sunucusuyla başka bir oturum başlatmadan önce istemcinin durdurması ve isteğe bağlı olarak yeniden başlatılması gerekir. Diğer ayrıntılar için Küçük Örnek bölümüne bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstemcisi başarıyla durduruldu

- **NX_DHCPV6_NOT_STARTED** (0xE92) İstemci iş parçacığı başlamadı

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı


### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Stop the DHCPv6 Client task. */
status = nx_dhcpv6_start(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully stopped. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_resume
- nx_dhcpv6_suspend
- nx_dhcpv6_reinitialize
- nx_dhcpv6_start

## <a name="nx_dhcpv6_suspend"></a>nx_dhcpv6_suspend

DHCPv6 İstemci görevini askıya alma 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_suspend(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Description

Bu hizmet DHCPv6 istemci görevini ve işlemenin ortasındaki tüm istekleri askıya alır. Süreerler devre dışı bırakılır ve İstemci durumu çalışmıyor olarak ayarlanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 İstemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) İstemcisi başarıyla askıya alındı

- **NX_DHCPV6_NOT_STARTED** (0XE92) İstemcisi çalışmıyor, bu nedenle askıya alınamaz

- NX_PTR_ERROR (0x16) Geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) İş parçacığından çağrılmalı

### <a name="allowed-from"></a>İzin Verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Suspend the DHCPv6 Client task. */
status = nx_dhcpv6_suspend(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully suspended. */
```

### <a name="see-also"></a>Ayrıca Bkz.

- nx_dhcpv6_resume
- nx_dhcpv6_start
- nx_dhcpv6_reinitialize
- nx_dhcpv6_stop
