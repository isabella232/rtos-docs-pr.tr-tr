---
title: Bölüm 3-Azure RTOS NetX DHCP sunucu hizmetlerinin açıklaması
description: Bu bölümde tüm Azure RTOS NetX DHCP sunucu hizmetlerinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d24c69cf6b8c2bb84b7155e49a54e8296ee662f0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826783"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-server-services"></a>Bölüm 3-Azure RTOS NetX DHCP sunucu hizmetlerinin açıklaması

Bu bölüm, tüm NetX DHCP sunucusu hizmetlerinin bir açıklamasını içerir.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_dhcp_server_create**: *DHCP sunucusu örneği oluşturma*
- **nx_dhcp_set_interface_network_parameters**: *belirtilen arabirim için kritik ağ parametreleri için DHCP sunucusu seçeneklerini ayarla*
- **nx_dhcp_create_server_ip_address_list**: *DHCP istemcileri ARABIRIMINE atanacak kullanılabilir IP adresleri havuzu oluştur*
- **nx_dhcp_clear_client_record**: *sunucu veritabanındaki istemci kaydını kaldırma*
- **nx_dhcp_server_delete**: *bir dhcpserver örneğini silme*
- **nx_dhcp_server_start**: *DHCP sunucusu işlemeyi Başlat veya sürüyor*
- **nx_dhcp_server_stop**: *DHCP sunucusu işlemesini durdur*

## <a name="nx_dhcp_server_create"></a>nx_dhcp_server_create

DHCP sunucu örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_server_create(NX_DHCP_SERVER *dhcp_ptr, NX_IP *ip_ptr,
                        VOID *stack_ptr, ULONG stack_size,
                        CHAR *input_address_list, CHAR *name_ptr,
                        NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş bir IP örneğiyle bir DHCP sunucusu örneği oluşturur.

> [!IMPORTANT]
> Uygulama, IP oluşturma hizmeti için oluşturulan paket havuzunun UDP, IP ve Ethernet üst bilgilerini içermeyen bir minimum548 Byte yüküne sahip olduğundan emin olmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP sunucusu denetim bloğu işaretçisi.  
- **ip_ptr**: DHCP sunucusu IP örneğine yönelik işaretçi.
- **stack_ptr**: Işaretçi DHCP sunucusu yığın konumu.
- **stack_size**: DHCP sunucusu yığınının boyutu
- **input_address_list**: sunucunun IP adresleri listesine yönelik işaretçi
- **name_ptr**: DHCP sunucu adı işaretçisi
- **packet_pool_ptr**: DHCP sunucusu paket havuzuna yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP sunucusu oluşturma.
- **NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD**: (0xA9) paket yükü çok küçük hata
- **NX_DHCP_NO_SERVER_OPTION_LIST**: (0x96) sunucu seçenek listesi boş
- NX_DHCP_PARAMETER_ERROR: (0x92) geçersiz işaretçi girişi
- NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin verilen

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

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen DHCP sunucusuna atanacak bir NetworkInterface 'e özgü IP adresleri havuzu oluşturur. Başlangıç ve bitiş IP adreslerinin belirtilen ağ arabirimiyle eşleşmesi gerekir. IP adresi listesi yeterince büyük değilse (Kullanıcı tarafından yapılandırılabilir *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parametresinde ayarlanır), eklenen IP adreslerinin gerçek sayısı toplam adresten daha az olabilir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr** DHCP sunucu denetim bloğu işaretçisi.  
- **iface_index**: ağ arabirimine karşılık gelen dizin
- **start_ip_address**: Ilk kullanılabilir IP adresi
- **end_ip_address**: en son kullanılabilir IP adresi
- **addresses_added**: LISTEYE eklenen IP adresi sayısı

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP sunucusu oluşturma.
- **NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: (0xA1) dizin adreslerle eşleşmiyor
- **NX_DHCP_INVALID_IP_ADDRESS_LIST**: (0x99) geçersiz adres girişi
- NX_DHCP_INVALID_IP_ADDRESS: (0x9B) ıllogical başlangıç/bitiş adresleri
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin verilen

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

Istemci kaydını sunucu veritabanından kaldır

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_clear_client_record (NX_DHCP_SERVER *dhcp_ptr,
                                NX_DHCP_CLIENT *dhcp_client_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, Istemci kaydını sunucu veritabanından temizler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP sunucusu denetim bloğu işaretçisi.  
- **dhcp_client_ptr**: kaldırılacak DHCP istemcisine yönelik işaretçi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP sunucusu oluşturma.
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.
- NX_CALLER_ERROR: (0x11) hizmet iş parçacığı olmayan çağrı

### <a name="allowed-from"></a>İzin verilen

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

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen arabirim için ağ kritik parametrelerinin varsayılan değerlerini ayarlar. DHCP sunucusu, bu seçenekleri sunmak ve DHCP Istemcisine onay yanıtlarını içerecektir. Ana bilgisayar, bir DHCP sunucusunun çalıştığı arabirim parametreleri ayarlandıysa, parametreler varsayılan olarak aşağıdaki gibidir: yönlendirici, DHCP sunucusunun kendisi için birincil arabirim ağ geçidine, DHCP sunucusunun kendisi için de DNS sunucusu adresine ve DHCP sunucusu arabirimiyle aynı alt ağ maskesine ayarlanır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **dhcp_ptr**: DHCP sunucusu denetim bloğu işaretçisi.  
- **iface_index**: ağ arabirimine karşılık gelen dizin
- **subnet_mask**: istemci ağı için alt ağ maskesi
- **default_gateway_address**: ISTEMCININ yönlendirici IP adresi
- **dns_server_address**: istemci ağı için DNS sunucusu

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı DHCP sunucusu oluşturma.
- **NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: (0xA1) dizin adreslerle eşleşmiyor
- **NX_DHCP_INVALID_NETWORK_PARAMETERS**: (0xA3) geçersiz ağ parametreleri
- NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.

### <a name="allowed-from"></a>İzin verilen

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

DHCP sunucusu örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_dhcp_server_delete(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, önceden oluşturulmuş bir DHCP sunucusu örneğini siler.

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

### <a name="description"></a>Açıklama

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

### <a name="description"></a>Açıklama

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
