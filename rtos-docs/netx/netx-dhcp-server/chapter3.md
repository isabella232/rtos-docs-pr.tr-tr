---
title: Bölüm 3 - NetX DHCP Azure RTOS hizmetlerinin açıklaması
description: Bu bölümde, Tüm NetX DHCP Azure RTOS hizmetlerinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 702499184b12484fa5862ba83ff3fadb8fccea31089b6bf8b71daf267e8c84a3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799532"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-server-services"></a>Bölüm 3 - NetX DHCP Azure RTOS hizmetlerinin açıklaması

Bu bölümde tüm NetX DHCP Sunucusu hizmetlerinin açıklaması yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_dhcp_server_create:** DHCP *Sunucusu örneği oluşturma*
- **nx_dhcp_set_interface_network_parameters:** Belirtilen *arabirim için kritik ağ parametreleri için DHCP Sunucusu seçeneklerini ayarlayın*
- **nx_dhcp_create_server_ip_address_list:** DHCP *İstemcileri arabirimine atamak için kullanılabilir IP adresleri havuzu oluşturma*
- **nx_dhcp_clear_client_record:** Sunucu *veritabanındaki İstemci kaydını kaldırma*
- **nx_dhcp_server_delete:** *DHCPServer örneğini silme*
- **nx_dhcp_server_start:** *DHCP Sunucusu işlemeyi başlatma veya sürdürme*
- **nx_dhcp_server_stop:** *DHCP sunucusu işlemeyi durdurma*

## <a name="nx_dhcp_server_create"></a>nx_dhcp_server_create

DHCP Sunucusu örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_server_create(NX_DHCP_SERVER *dhcp_ptr, NX_IP *ip_ptr,
                        VOID *stack_ptr, ULONG stack_size,
                        CHAR *input_address_list, CHAR *name_ptr,
                        NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir IP örneği ile bir DHCP Sunucusu örneği oluşturur.

> [!IMPORTANT]
> Uygulama, IP oluşturma hizmeti için oluşturulan paket havuzunun UDP, IP ve Ethernet üst bilgileri dahil olmak üzere en az 548 bayt yüküne sahip olduğundan emin olması gerekir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr:** DHCP Sunucusu denetim bloğuna işaretçi.  
- **ip_ptr:** DHCP Sunucusu IP örneğinin işaretçisi.
- **stack_ptr:** İşaretçi DHCP Sunucusu yığın konumu.
- **stack_size:** DHCP Sunucusu yığınının boyutu
- **input_address_list:** Sunucunun IP adresleri listesinin işaretçisi
- **name_ptr:** DHCP Sunucusu adı işaretçisi
- **packet_pool_ptr:** DHCP Sunucusu paket havuzunun işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı DHCP Sunucusu oluşturma.
- **NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD:**(0xA9) Paket yükü çok küçük hatası
- **NX_DHCP_NO_SERVER_OPTION_LIST:**(0x96) Sunucu seçeneği listesi boş
- NX_DHCP_PARAMETER_ERROR: (0x92) İşaretçi olmayan giriş geçersiz
- NX_CALLER_ERROR: (0x11) Geçersiz hizmet çağıranı.
- NX_PTR_ERROR: (0x16) Geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin Verilen

Uygulama

### <a name="example"></a>Örnek

```c
/* Create a DHCP Server instance. */
status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
                    DEMO_SERVER_STACK_SIZE, SERVER_IP_ADDRESS_LIST,
                    "DHCP server", &server_pool);

/* If status is NX_SUCCESS a DHCP Server instance was successfully created. */
```

## <a name="nx_dhcp_create_server_ip_address_list"></a>nx_dhcp_create_server_ip_address_list

IP adresi havuzu oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_create_server_ip_address_list(NX_DHCP_SERVER *dhcp_ptr,
                            UINT iface_index, ULONG start_ip_address,
                            ULONG end_ip_address, UINT *addresses_added);
```

### <a name="description"></a>Description

Bu hizmet, ataması belirtilen DHCP sunucusu için kullanılabilir IP adreslerinin ağ arabirime özgü bir havuzunu oluşturur. Başlangıç ve bitiş IP adresleri belirtilen ağ arabirimiyle eşleşmeli. IP adresi listesi yeterince büyük (kullanıcı tarafından yapılandırılabilir ip adresi parametresinde ayarlanır) yoksa, eklenen gerçek IP adresi sayısı toplam *adreslerden NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* olabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP Sunucusu denetim bloğu işaretçisi.  
- **iface_index:** Ağ arabirimine karşılık gelen dizin
- **start_ip_address:** İlk kullanılabilir IP adresi
- **end_ip_address:** Kullanılabilir IP adresinin son tarihi
- **addresses_added:** Listeye eklenen IP adresi sayısı

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı DHCP Sunucusu oluşturma.
- **NX_DHCP_SERVER_BAD_INTERFACE_INDEX:**(0xA1) Dizin adresle eşle değil
- **NX_DHCP_INVALID_IP_ADDRESS_LIST:**(0x99) Geçersiz adres girişi
- NX_DHCP_INVALID_IP_ADDRESS: (0x9B) İllogical başlangıç/bitiş adresleri
- NX_PTR_ERROR: (0x16) Geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin Verilen

Uygulama

### <a name="example"></a>Örnek

```c
/* Create a pool of available IP addresses to assign. */
status = nx_dhcp_create_server_ip_list (&dhcp_server, iface_index,
                START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);

/* If status is NX_SUCCESS aIP address list was successfully created. 
addresses_added indicates how many IP addresses were actually added to the list. */
```

## <a name="nx_dhcp_clear_client_record"></a>nx_dhcp_clear_client_record

Sunucu veritabanından İstemci kaydını kaldırma

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_clear_client_record (NX_DHCP_SERVER *dhcp_ptr,
                                NX_DHCP_CLIENT *dhcp_client_ptr);
```

### <a name="description"></a>Description

Bu hizmet, Sunucu veritabanından İstemci kaydını temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr:** DHCP Sunucusu denetim bloğuna işaretçi.  
- **dhcp_client_ptr:** Kaldırmak için DHCP İstemcisi işaretçisi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı DHCP Sunucusu oluşturma.
- NX_PTR_ERROR: (0x16) Geçersiz işaretçi girişi.
- NX_CALLER_ERROR: (0x11) Hizmetin iş parçacığı çağıranı değil

### <a name="allowed-from"></a>İzin Verilen

Uygulama

### <a name="example"></a>Örnek

```c
/* Remove Client record from the server database. */
status = nx_dhcp_clear_client_record (&dhcp_server, &dhcp_client_ptr);

/* If status is NX_SUCCESS the specified Client was removed from the database. */
```

## <a name="nx_dhcp_set_interface_network_parameters"></a>nx_dhcp_set_interface_network_parameters

DHCP seçenekleri için ağ parametrelerini ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_set_interface_network_parameters(NX_DHCP_SERVER *dhcp_ptr,
                                    UINT iface_index, ULONG subnet_mask,
                                    ULONG default_gateway_address,
                                    ULONG dns_server_address);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen arabirim için ağ kritik parametreleri için varsayılan değerleri ayarlar. DHCP sunucusu, TEKLIF'inde bu seçenekleri içerir ve ACK, DHCP İstemcisi'ne yanıtlar. Dhcp sunucusunun üzerinde çalıştırılan konak kümesi arabirim parametreleri, parametreler varsayılan olarak şu şekilde ayarlanır: yönlendirici DHCP sunucusunun kendisi için birincil arabirim ağ geçidine, DNS sunucusu adresi DHCP sunucusunun adresine ayarlanır ve alt ağ maskesi DHCP sunucu arabirimiyle aynı şekilde yapılandırılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr:** DHCP Sunucusu denetim bloğuna işaretçi.  
- **iface_index:** Ağ arabirimine karşılık gelen dizin
- **subnet_mask:** İstemci ağı için alt ağ maskesi
- **default_gateway_address:** İstemcinin yönlendirici IP adresi
- **dns_server_address:** İstemci ağı için DNS sunucusu

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı DHCP Sunucusu oluşturma.
- **NX_DHCP_SERVER_BAD_INTERFACE_INDEX:**(0xA1) Dizin adresle eşle değil
- **NX_DHCP_INVALID_NETWORK_PARAMETERS:**(0xA3) Geçersiz ağ parametreleri
- NX_PTR_ERROR: (0x16) Geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin Verilen

Uygulama

### <a name="example"></a>Örnek

```c
/* Set network parameters for a specific interface. */
status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
                                    NX_DHCP_SUBNET_MASK, IP_ADDRESS(10,0,0,1),
                                    IP_ADDRESS(10,0,0,1));

/* If status is NX_SUCCESS network parameters were successfully set. */
```

## <a name="nx_dhcp_server_delete"></a>nx_dhcp_server_delete

DHCP Sunucusu örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_server_delete(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, daha önce oluşturulmuş bir DHCP Sunucusu örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: bir DHCP sunucusu örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) DHCP sunucusu başarıyla silindi.
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.
- NX_DHCP_PARAMETER_ERROR: (0x92) geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete a DHCP Server instance. */
status = nx_dhcp_server_delete(&dhcp_server);  
  
/* If status is NX_SUCCESS the DHCP Server instance was successfully deleted. */
```

## <a name="nx_dhcp_server_start"></a>nx_dhcp_server_start

DHCP sunucusu işlemeyi Başlat

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_server_start(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, bir sunucu UDP yuvası oluşturmayı, DHCP bağlantı noktasını bağlamayı ve Istemci DHCP isteklerini almayı beklemeyi içeren DHCP sunucusu işlemesini başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) sunucu başarıyla başlatıldı.  
- **NX_DHCP_ALREADY_STARTED**: (0x93) DHCP zaten başlatılmış.
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.
- NX_DHCP_PARAMETER_ERROR: (0x92) geçersiz işaretçi girişi

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the DHCP Server processing for this IP instance. */
status = nx_dhcp_server_start(&dhcp_server);  

/* If status is NX_SUCCESS the DHCP Server was successfully started. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_dhcp_create, nx_dhcp_delete, nx_dhcp_release, nx_dhcp_state_change_notify, nx_dhcp_stop, nx_dhcp_user_option_retrieve, nx_dhcp_user_option_convert

## <a name="nx_dhcp_server_stop"></a>nx_dhcp_server_stop

DHCP sunucusu işlemesini durduruyor

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_server_stop(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Description

Bu hizmet, DHCP Istemci isteklerinin alınması dahil olmak üzere DHCP sunucusu işlemesini durduruyor.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP sunucusu örneğine yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP durağı.
- **NX_DHCP_ALREADY_STARTED**: (0x93) DHCP zaten başlatılmış.
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.
- NX_DHCP_PARAMETER_ERROR: (0x92) geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the DHCP Server processing for this IP instance. */
status = nx_dhcp_server_stop(&dhcp_server);  

/* If status is NX_SUCCESS the DHCP Server was successfully stopped. */
```
