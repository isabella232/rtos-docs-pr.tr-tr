---
title: Bölüm 4-Azure RTOS NetX Duo DHCPv6 Istemci Hizmetleri
description: Bu bölüm, tüm Azure RTOS NetX Duo DHCPv6 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 40fbfa7319ca95af65c92b12582d4bbb05005dc0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826074"
---
# <a name="chapter-4---azure-rtos-netx-duo-dhcpv6-client-services"></a>Bölüm 4-Azure RTOS NetX Duo DHCPv6 Istemci Hizmetleri

Bu bölüm, tüm Azure RTOS NetX Duo DHCPv6 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_dhcpv6_client_create:** *DHCPv6 istemci örneği oluşturma* 

- **nx_dhcpv6_client_delete:** *DHCPv6 istemci örneğini silme* 

- **nx_dhcpv6_create_ client_duid:** *bir DHCPv6 istemcisi DUID oluşturma* 

- **nx_dhcpv6 _add_client_ia:** *DHCPv6 istemci kimlik adresı ekleme (IA)* 

- **nx_dhcpv6 _create_client_ia:** (*eski bir DHCPv6 istemci KIMLIK adresi (IA) Ekle)* 

- **nx_dhcpv6_create_client_iana:** *geçici olmayan adresler (IANA) Için DHCPv6 istemci kimliği ilişkilendirmesi oluşturma* 

- **nx_dhcpv6_get_client_duid_time_id:** *DHCPv6 istemcisi DUID 'den saat kimliğini alın* 

- **nx_dhcpv6_client_set_interface:** *DHCPv6 sunucusuyla iletişim için istemci ağ arabirimini ayarlama* 

- **nx_dhcpv6_get_IP_address:** *DHCPv6 Istemcisine atanan genel IPv6 adresini al* 

- **nx_dhcpv6_get_lease_time_data:** *istemci genel IPv6 adresi Için T1, T2, geçerli ve tercih edilen yaşam süreleri alın*

- **nx_dhcpv6_get_valid_ip_address_lease_time:** *Adres dizinine göre DHCPv6 istemci IPv6 adresi Için T1, T2, geçerli ve tercih edilen yaşam süreleri alın* 

- **nx_dhcpv6_get_iana_lease_time:** *DHCPv6 Istemcisine kiralanmış kimlik ILIŞKILENDIRMESINDE (IANA) T1 ve T2 alın* 

- **nx_dhcpv6_get_other_option_data:** *belirtilen seçenek verilerini al, örn. etki alanı adı veya saat dilimi sunucusu* 

- **nx_dhcpv6_get_DNS_server_address:** *belirtilen dizindeki DNS sunucu ADRESINI DHCPv6 istemci DNS sunucusu listesine al* 

- **nx_dhcpv6_get_time_accrued:** *genel IPv6 adresi kiralamasının DHCPv6 istemcisine bağladığına yönelik zaman kazanın* 

- **nx_dhcpv6_get_time_server_address:** *belirtilen dizindeki saat sunucusu adresini DHCPv6 istemci zamanı sunucu listesine al*

- **nx_dhcpv6_get_valid_ip_address_count:** *DHCPv6 istemcisine atanan IPv6 adresi sayısını Al* 

- **nx_dhcpv6_reinitialize:** *DHCPv6 istemci durumu makinesini yeniden başlatmak için DHCPv6 'yi yeniden başlatın ve DHCPv6 protokolünü yeniden çalıştırarak* 

- **nx_dhcpv6_request_confirm:** *sunucuya bir onaylama isteği gönderin* 

- **nx_dhcpv6_request_inform_request:** S *BIR BILDIR istek Iletisini sunucuya Sonlandır* 

- **nx_dhcpv6_request_release:** *sunucuya bir yayın isteği gönderin* 

- **nx_dhcpv6_request_option_DNS_server:** *sunucu için Istek iletileri içindeki istemci SEÇENEĞI istek verilerine DNS sunucusu seçeneğini ekleyin* 

- **nx_dhcpv6_request_option_FQDN:** *sunucu için Istek iletileri içindeki istemci SEÇENEĞI istek verilerine FQDN seçeneğini ekleyin* 

- **nx_dhcpv6_request_option_domain_name:** *sunucu için Istek iletileri içindeki istemci seçeneği istek verilerine etki alanı adı seçeneğini ekleyin* 

- **nx_dhcpv6_request_option_time_server:** *sunucuya istek iletileri Istek iletileri için istemci seçeneğine saat sunucusu seçeneğini ekleyin* 

- **nx_dhcpv6_request_option_timezone:** *sunucuya Istek iletileri iste istemci seçeneği istek verilerine saat dilimi seçeneğini ekleyin* 

- **nx_dhcpv6_request_solicit:** *istemci ağındaki (yayın) herhangi BIR sunucuya DHCPv6 istem isteği gönderin* 

- **nx_dhcpv6_request_solicit_rapid:** *hızlı tamamlama seçenek kümesiyle istemci ağındaki (yayın) herhangi bir sunucuya bir DHCPv6 istek isteği gönderin* 

- **nx_dhcpv6_resume:** *DHCPv6 istemci işlemesini sürdürür* 

- **nx_dhcpv6_start:** *DHCPv6 istemci iş parçacığı görevini başlatın. Bu, DHCPv6 durum makinesinin başlatılmasına eşit değildir ve bir Istem isteği göndermez* 

- **nx_dhcpv6_stop:** *DHCPv6 istemci iş parçacığı görevini durdur* 

- **nx_dhcpv6_suspend:** *DHCPv6 istemci iş parçacığı görevini askıya al* 

- **nx_dhcpv6_set_time_accrued:** *Istemci kaydındaki genel istemci IPv6 adresi kirası üzerinde tahakkuk eden süreyi ayarlayın.*

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

### <a name="description"></a>Açıklama

Bu hizmet, geri çağırma işlevleri dahil olmak üzere bir DHCPv6 istemci örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 denetim bloğu işaretçisi  

- **ip_ptr** Istemci IP örneği işaretçisi  

- **name_ptr** DHCPv6 örneği için ad işaretçisi

- **packet_pool_ptr** Istemci paket havuzu işaretçisi

- **stack_ptr** Istemci yığını belleği işaretçisi

- **stack_size** Istemci yığını bellek boyutu

- **dhcpv6_state_change_notify** Istemci sunucuya yeni bir DHCPv6 isteği başlattığında çağrılan geri çağırma işlevi işaretçisi

- **dhcpv6_server_error_handler** Istemci sunucudan bir hata durumu aldığında çağrılan geri çağırma işlevi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı istemci oluşturma

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 Istemci örneğini silme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_client_delete(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir DHCPv6 istemci örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) başarılı DHCPv6 silme

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 için Istemcinin ağ arabirimini ayarlar

### <a name="prototype"></a>Prototype

```C
UINT    nx_dhcpv6_client_set_interface(NX_DHCPV6 *dhcpv6_ptr, 
                                       UINT *interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCPv6 sunucuları ile iletişim için Istemcinin ağ arabirimini belirtilen giriş arabirimi dizinine ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **interface_index** Ağ arabirimini belirten Dizin

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) arabirimi başarıyla ayarlandı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_INVALID_INTERFACE (0x4C) geçersiz arabirim dizin girişi

### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 iletisinin gönderileceği hedef adresi ayarlar

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_client_set_destination_address(NX_DHCPV6 *dhcpv6_ptr,
                                              NXD_ADDRESS *destination_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCPv6 iletisinin gönderileceği hedef adresi ayarlar. Varsayılan olarak ALL_DHCP_Relay_Agents_and_Servers (FF02:: 1:2).

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

Bu hizmet, Istemcinin IPv6 adresi kiralamasında tahakkuk eden süreyi alır. İşlevi, ilk geçerli adres için Istemciye atanan tüm IPv6 adreslerini denetler. Geçerli adres bulunmazsa, tahakkuk edilen zaman için sıfır değeri döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **time_accrued** IP kiralamasında tahakkuk eden zaman işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) tahakkuk edilen süre başarıyla alındı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

Saat sunucusu adresini alır 

### <a name="prototype"></a>Prototype

```C
UINT  nx_dhcpv6_get_time_server_address(NX_DHCPV6 *dhcpv6_ptr, UINT index, 
                                        NXD_ADDRESS *server_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, Istemci listesindeki belirtilen dizindeki saat sunucusu IPv6 adresi verilerini alır. Listede dizin üzerinde bir sunucu adresi yoksa bir hata döndürülür. Dizin, Kullanıcı tarafından yapılandırılabilir seçenek NX_DHCPV6_NUM_TIME_SERVERS tarafından belirtilen zaman sunucu listesinin boyutunu aşamaz.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **Dizin** Saat sunucusu listesinde Dizin

- **server_address** Sunucu adresi arabelleği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) adresi başarıyla alındı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

Istemci IP adresini IP tablosundan kaldır

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_reinitialize(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCPv6 durum makinesini yeniden başlatmak ve DHCPv6 protokolünü yeniden çalıştırmak için Istemciyi yeniden başlatır. Istemci daha önce DHPCv6 durum makinesini başlatmadıysanız veya herhangi bir IPv6 adresi atamamışsa bu gerekli değildir. DHCPv6 Istemcisine kaydedilen adresler ve IP örneğiyle kayıtlı olan adreslerin ikisi de temizlenir.

> [!NOTE]
> Uygulamanın yine de *nx_dhcpv6_start hizmetini* kullanarak DHCPv6 istemcisini başlatması ve *nx_dhcpv6_request_solicit* çağırarak IPv6 adres ataması isteğine başlaması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) adresi başarıyla kaldırıldı

- **NX_DHCPV6_ALREADY_STARTED** (0xe91) DHCPv6 istemcisi zaten çalışıyor

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

Istemcinin onaylama durumunu işleme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_confirm(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir onaylama isteği gönderir. Sunucudan bir yanıt alınmışsa, DHCPv6 Istemcisi kira parametrelerini alınan verilerle güncelleştirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) ileti başarıyla gönderildiğini ve işlendiğini onaylayın

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

Istemcinin BILGI ISTEğI durumunu işle

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_inform_request(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet bir BILGI ISTEğI iletisi gönderir. Bir yanıt alınmışsa, biri alındığında yanıt, geçerli olduğunu ve sunucunun isteği vermiş olduğunu tespit etmek üzere işlenir. Istemci örneği daha sonra gerektiği şekilde sunucu bilgileriyle güncellenir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) bildirme isteği iletisi başarıyla oluşturuldu ve işlendi

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 seçenek isteğine DNS sunucusu ekleme

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_DNS_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCPv6 seçenek isteğine DNS sunucusu bilgilerini isteme seçeneğini ekler. Sunucu yanıtı DNS sunucusu verilerini içeriyorsa, Istemci, bunu yapmak için bir oda varsa, DNS sunucusunu depolayacaktır. Istemcinin depolayabileceği DNS sunucusu sayısı, varsayılan değeri 2 olan yapılandırılabilir seçenek NX_DHCPV6_NUM_DNS_SERVERS belirlenir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) DNS sunucusu seçeneği dahildir

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

Seçenek istek listesine tam etki alanı adı seçeneği ekleyin

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_FQDN(NX_DHCPV6 *dhcpv6_ptr, UCHAR *domain_name, 
UINT op);
```

### <a name="description"></a>Açıklama

Bu hizmet, Istemci tam etki alanı adını DHCPv6 seçenek isteğine ekleme seçeneğini ekler. FQDN seçeneği için üç seçenek vardır:

- NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR 0, Istemci tarafından kullanılan FQDN ve adresler için FQDN-IPv6 adres eşlemeyi güncelleştirin.

- NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE 1 Istemci tarafından sunucu tarafından kullanılan FQDN ve adresler için FQDN-IPv6 adres eşlemeyi güncelleştirin.

- NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE 2 sunucunun Istemci adına DNS güncelleştirmesi gerçekleştirmesiz bir Istek.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **domain_name** Etki alanı adını tutan dize

- **op** Uygulanacak FQDN seçeneğinin türü (yukarıdaki listeye bakın)

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) FQDN seçeneği dahildir

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 seçenek isteğine etki alanı adı seçeneği ekleyin

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_domain_name(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, Istemci isteği iletilerindeki seçenek isteğine etki alanı adı seçeneğini ekler. Sunucu yanıtı etki alanı adı verileri içeriyorsa, etki alanı adının boyutu, etki alanı adının tutulması için arabellek boyutu içindeyse, Istemci etki alanı adı bilgilerini depolar. Bu arabellek boyutu, varsayılan değer olan 30 baytlık yapılandırılabilir bir seçenektir (NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE).

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) etki alanı adı seçenek kümesi

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

Saat sunucusu verilerini isteğe bağlı istek olarak ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_time_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, Istemci istek iletilerinin seçenek isteğine zaman sunucusu bilgilerini ekler. Sunucu yanıtı, Tim sunucu verilerini içeriyorsa, Istemci, bunu yapmak için yer aldığında zaman sunucusunu depolayacaktır. Istemcinin depolayabileceği zaman sunucularının sayısı, yapılandırılabilir seçenek tarafından belirlenir

Varsayılan değeri 1 olan _SERVERS NX_DHCPV6_NUM_TIME.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) saat sunucusu seçeneği eklendi

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

Saat dilimi verilerini isteğe bağlı istek olarak ayarla

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_option_timezone(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, Istemci seçenek isteğine saat dilimi bilgilerini isteme seçeneğini ekler. Sunucu yanıtı saat dilimi verilerini içeriyorsa, saat diliminin boyutu saat dilimini tutmak için arabellek boyutu içindeyse Istemci saat dilimi bilgilerini depolar. Bu arabellek boyutu, varsayılan 10 baytlık bir değere sahip yapılandırılabilir bir seçenektir (NX_DHCPV6_ TIME_ZONE _BUFFER_SIZE).

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) saat dilimi seçeneği eklendi

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 sürüm iletisi gönder

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_release(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, Istemci ağına bir sürüm iletisi gönderir. İleti başarıyla gönderilirse, başarılı bir durum döndürülür. Başarılı bir tamamlama, Istemcinin bir yanıt aldığını veya henüz bir IPv6 adresi verildiğini ifade etmez. DHCPv6 Istemci iş parçacığı görevi DHCPv6 sunucusundan yanıt bekler. Bir tane alınmışsa, yanıtın geçerli olduğunu denetler ve verileri Istemci kaydına depolar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) yayın iletisi başarıyla gönderildi

- **NX_DHCPV6_NOT_STARTED** (0xe92) DHCPv6 istemci görevi başlatılmadı

- **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xead) adresi istemciye bağlanmadı

- **NX_INVALID_INTERFACE** (0x4C) IP adresi tablosunda bulunamadı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

Istem iletisi gönder

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_solicit(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, ağda bir Istem iletisi gönderir. İleti başarıyla gönderilirse, başarılı bir durum döndürülür. Başarılı bir tamamlama, Istemcinin bir yanıt aldığını veya henüz bir IPv6 adresi verildiğini ifade etmez. DHCPv6 Istemci iş parçacığı görevi DHCPv6 sunucusundan bir yanıt (bir TANıTıM iletisi) bekler. Bir tane alınmışsa, yanıtın geçerli olduğunu denetler, verileri Istemci kaydına depolar ve Istemciyi Istek durumuna yükseltir.

> [!NOTE] 
> Hızlı tamamlama seçeneği ayarlandıysa, geçerli bir sunucu TANıTıM iletisi alırsa DHCPv6 Istemcisi doğrudan bağlantılı duruma geçer. Daha fazla bilgi için bkz. *nx_dhcpv6_request_solicit_rapid* için hizmet açıklaması.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istem iletisi başarıyla gönderildi

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```C
/* Send an SOLICIT message to the server. */
status = nx_dhcpv6_request_solicit(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the SOLICIT message. */
```

## <a name="nx_dhcpv6_request_solicit_rapid"></a>nx_dhcpv6_request_solicit_rapid

Hızlı tamamlama seçeneğiyle bir Istem iletisi gönderin

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_request_solicit_rapid(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, ağ üzerinde hızlı tamamlama seçeneği ayarlanmış bir Istem iletisi gönderir. İleti başarıyla gönderilirse, başarılı bir durum döndürülür. Başarılı bir tamamlama, Istemcinin bir yanıt aldığını veya henüz bir IPv6 adresi verildiğini ifade etmez. DHCPv6 Istemci iş parçacığı görevi DHCPv6 sunucusundan bir yanıt (bir TANıTıM iletisi) bekler. Bir tane alınmışsa, yanıtın geçerli olduğunu denetler, verileri Istemci kaydına depolar ve Istemciyi bağlantılı duruma yükseltir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istem iletisi başarıyla gönderildi

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 Istemci görevini sürdürür 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_resume(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCPv6 Istemci iş parçacığı görevini sürdürür. Geçerli DHCPv6 Istemci durumu işlenecek (örn. bağlanma, Istek)

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla sürdürüldü

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

Istemcinin IP adresi kirası üzerinde tahakkuk eden süreyi ayarlar

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_set_time_accrued(NX_DHCPV6 *dhcpv6_ptr,
                                ULONG time_accrued);
```

### <a name="description"></a>Açıklama

Bu hizmet, Istemcinin genel IP adresi sunucu tarafından atandıktan sonra tahakkuk eden süreyi ayarlar. Bu, yalnızca bir Istemci atanmış bir IPv6 adresine bağlıysa kullanılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

- **time_accrued** IP kiralamasında tahakkuk eden saat

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) tahakkuk eden zaman kümesi

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 Istemci görevini başlatın 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_start(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet DHCPv6 Istemci görevini başlatır ve Istemciyi DHCPv6 protokolünü çalıştırmaya hazırlar. Istemci örneğinin yeterli bilgilere sahip olduğunu doğrular (örneğin, bir Istemci DUıD), DHCPv6 iletilerini göndermek ve almak için UDP yuvasını oluşturup bağlar ve oturum süresini izlemek ve geçerli IPv6 kira süresinin dolması için zamanlayıcıları etkinleştirir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla başlatıldı

- **NX_DHCPV6_MISSING_REQUIRED_OPTIONS** (0xea9) istemcisinde gerekli seçenekler eksik

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 Istemci görevini durdur 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_stop(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCPv6 Istemci görevini sonlandırır ve yeniden aktarım sayısını, en fazla yeniden aktarım aralığını temizler, oturumu ve Kiralama süre sonu zamanlayıcıları devre dışı bırakır ve DHCPv6 Istemci yuva bağlantı noktasının bağlantısını kaldırır. Istemciyi yeniden başlatmak için, önce herhangi bir DHCPv6 sunucusu ile başka bir oturum başlatmadan önce Istemciyi durdurup isteğe bağlı olarak yeniden başlatmanız gerekir. Daha fazla bilgi için küçük örnek bölümüne bakın.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla durduruldu

- **NX_DHCPV6_NOT_STARTED** (0xe92) istemci iş parçacığı başlatılmadı

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır


### <a name="allowed-from"></a>İzin verilen

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

DHCPv6 Istemci görevini askıya alma 

### <a name="prototype"></a>Prototype

```C
UINT nx_dhcpv6_suspend(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, DHCPv6 istemci görevini ve işlemin ortasında olduğu tüm istekleri askıya alır. Zamanlayıcılar devre dışı bırakılır ve Istemci durumu çalışmıyor olarak ayarlanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS** (0x00) istemci başarıyla askıya alındı

- **NX_DHCPV6_NOT_STARTED** (0xe92) istemci çalışmıyor, askıya alınamıyor

- NX_PTR_ERROR (0x16) geçersiz işaretçi girişi

- NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır

### <a name="allowed-from"></a>İzin verilen

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
