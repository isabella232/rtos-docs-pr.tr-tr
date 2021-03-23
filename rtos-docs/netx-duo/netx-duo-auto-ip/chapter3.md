---
title: Bölüm 3-Azure RTOS NetX Duo Oto IP Hizmetleri açıklaması
description: Bu bölümde, tüm Azure RTOS NetX Duo Oto IP Hizmetleri (aşağıda listelenmiştir) alfabetik sırada bir açıklama bulunur.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 0935295ef9f7255c0851e1f64013884dce4c52f1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826165"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-autoip-services"></a>Bölüm 3-Azure RTOS NetX Duo Oto IP Hizmetleri açıklaması

Bu bölümde, tüm Azure RTOS NetX Duo Oto IP Hizmetleri (aşağıda listelenmiştir) alfabetik sırada bir açıklama bulunur.

Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.

- **nx_auto_ip_create**: *Oto IP örneği oluştur*
- **nx_auto_ip_delete**: *Oto IP örneğini Sil*
- **nx_auto_ip_get_address**: *geçerli Oto IP adresini al*
- **nx_auto_ip_set_interface**: *IP arabirimine bir Oto IP adresi ihtiyacı* olacak şekilde ayarla
- **nx_auto_ip_start**: *Oto IP işlemesini Başlat*
- **nx_auto_ip_stop**: *Oto IP işlemesini durdur*

## <a name="nx_auto_ip_create"></a>nx_auto_ip_create

Oto IP örneği oluştur

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_create(NX_AUTO_IP *auto_ip_ptr, CHAR *name,
                    NX_IP *ip_ptr, VOID *stack_ptr, ULONG stack_size,
                    UINT priority);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneğinde bir Oto IP örneği oluşturur.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.
- **ad**: Oto IP örneğinin adı.
- **ip_ptr**: IP örneğine yönelik işaretçi.
- **stack_ptr**: Oto IP iş parçacığı yığın alanı işaretçisi.
- **stack_size**: Oto IP iş parçacığı yığını alanının boyutu.
- **Öncelik**: Oto IP iş parçacığının önceliği.

> [!NOTE]
> DHCP kullanılıyorsa, DHCP iş parçacığının IP örneği iş parçacığından ve Oto IP iş parçacığından daha yüksek bir önceliğe sahip olması gerekir.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı bir oto oluştur.
- **NX_AUTO_IP_ERROR**: (0xa00) Oto IP oluşturma hatası.
- NX_PTR_ERROR: (0x16) geçersiz Oto IP, ip_ptr veya yığın işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create the AutoIP instance "auto_ip_0" on "ip_0". */
status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);

/* If status is NX_SUCCESS an AutoIP instance was successfully created. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_delete"></a>nx_auto_ip_delete

Oto IP örneğini Sil

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_delete(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen IP örneğinde daha önce oluşturulmuş bir Oto IP örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı Oto IP silme.
- **NX_AUTO_IP_ERROR**: (0xa00) Oto IP silme hatası.
- NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Delete the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_delete(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully deleted. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_get_address"></a>nx_auto_ip_get_address

Geçerli Oto IP adresini al

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_get_address(NX_AUTO_IP *auto_ip_ptr,
                            ULONG *local_ip_address);
```

### <a name="description"></a>Açıklama

Bu hizmet şu anda kurulum diğer IP adresini alır. Bir tane yoksa, 0.0.0.0 IP adresi döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.
- **local_ip_address**: dönüş IP adresi hedefi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı bir Oto IP adresi al.
- **NX_AUTO_IP_NO_LOCAL**: (0xa01) geçerli bir Oto IP adresi yok.
- NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, zamanlayıcılar, Iş parçacıkları, ISRs

### <a name="example"></a>Örnek

```c
ULONG local_address;

/* Get the AutoIP address resolved by the instance "auto_ip_0." */
status = nx_auto_ip_get_address(&auto_ip_0, &local_address);

/* If status is NX_SUCCESS the local IP address is in "local_address." */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_set_interface"></a>nx_auto_ip_set_interface

Oto IP için ağ arabirimini ayarla

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_set_interface(NX_AUTO_IP *auto_ip_ptr,
                            UINT interface_index);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir ağ IP adresi için ağ arabirimi Oto IP 'si araştırmasını ayarlar. Varsayılan değer sıfırdır (birincil ağ arabirimi). Yalnızca çok sayfalı cihazlar için geçerlidir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.
- **interface_index**: IÇIN araştırma IP adresi arabirimi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı bir oto arabirimi kümesi
- **NX_AUTO_IP_BAD_INTERFACE_INDEX**: (0Xa02) geçersiz ağ arabirimi NX_PTR_ERROR (0x16) geçersiz bir Oto IP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, zamanlayıcılar, Iş parçacıkları, ISRs

### <a name="example"></a>Örnek

```c
ULONG interface_index;

/* Set the network interface on which AutoIP probes for host address. */
status = nx_auto_ip_set_interface(&auto_ip_0, interface_index);

/* If status is NX_SUCCESS the network interface is valid and set in the AutoIP control block *auto_ip_0*. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_auto_ip_create, nx_auto_ip_get_address, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_start"></a>nx_auto_ip_start

Oto IP işlemesini Başlat

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_start(NX_AUTO_IP *auto_ip_ptr,
                    ULONG starting_local_address);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş bir Oto IP örneğinde, Oto IP protokolünü başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.
- **starting_local_address**: Isteğe bağlı otomatik IP başlangıç adresi. IP_ADDRESS değeri (0, 0, 0, 0) bir rastgele bir bir bir bir bir bir bir bir bir bir IP adresi elde edilmelidir. Aksi takdirde, geçerli bir bir bir bir bir bir bir bir bir bir bir IP adresi belirtilmişse NetX, bu adresi atamayı dener.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı bir oto başlatması.
- **NX_AUTO_IP_ERROR**: (0xa00) Oto IP başlatma hatası.
- NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

Başlatma, Iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Start the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_start(&auto_ip_0, IP_ADDRESS(0,0,0,0));

/* If status is NX_SUCCESS an AutoIP instance was successfully started. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_stop

## <a name="nx_auto_ip_stop"></a>nx_auto_ip_stop

Oto IP işlemesini durdur

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_stop(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, daha önce oluşturulmuş ve başlatılan bir Oto IP örneğinde, Oto IP protokolünü sonlandırır. Bu hizmet genellikle IP adresi DHCP aracılığıyla veya bir oto olmayan IP adresine el ile değiştirildiğinde kullanılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS**: (0x00) başarılı bir oto durdur.
- **NX_AUTO_IP_ERROR**: (0xa00) Oto IP durağı hatası.
- NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.

### <a name="allowed-from"></a>İzin verilen

İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Stop the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_stop(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully stopped. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_start