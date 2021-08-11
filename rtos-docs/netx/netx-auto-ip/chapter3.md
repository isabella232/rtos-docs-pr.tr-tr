---
title: Bölüm 3 - NetX AutoIP Azure RTOS açıklama
description: Bu bölümde, Tüm NetX AutoIP Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 15a70416f9d4d1324d930820b09366a7e7cd6f4525872472cd88edfbb25ee155
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796880"
---
# <a name="chapter-3---description-of-azure-rtos-netx-autoip-services"></a>Bölüm 3 - NetX AutoIP Azure RTOS açıklama

Bu bölümde, Tüm NetX AutoIP Azure RTOS (aşağıda listelenmiştir) alfabetik sırada bir açıklama yer almaktadır.

Aşağıdaki API açıklamalarında yer alan "Dönüş Değerleri" bölümünde, **KALıN**  olmayan değerler tamamen devre dışı bırakılırken, BOLD NX_DISABLE_ERROR_CHECKING API hata denetimlerini devre dışı bırakmak için kullanılan tanımdan etkilenmez.

- **nx_auto_ip_create:** *AutoIP örneği oluşturma*
- **nx_auto_ip_delete:** *AutoIP örneğini silme*
- **nx_auto_ip_get_address:** Geçerli *AutoIP adresini al*
- **nx_auto_ip_set_interface:** *AutoIP adresine ihtiyaç olan IP arabirimini ayarlama*
- **nx_auto_ip_start:** *AutoIP işlemeyi başlatma*
- **nx_auto_ip_stop:** *AutoIP işlemeyi durdurma*

## <a name="nx_auto_ip_create"></a>nx_auto_ip_create

AutoIP örneği oluşturma

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_create(NX_AUTO_IP *auto_ip_ptr, CHAR *name,
            NX_IP *ip_ptr, VOID *stack_ptr, ULONG stack_size,
            UINT priority);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneğinde bir AutoIP örneği oluşturur.

- **auto_ip_ptr:** AutoIP denetim bloğuna işaretçi.
- **name:** AutoIP örneğinin adı.
- **ip_ptr:** IP örneğine işaretçi.
- **stack_ptr:** AutoIP iş parçacığı yığın alanına işaretçi.
- **stack_size:** AutoIP iş parçacığı yığın alanı boyutu.
- **priority:** AutoIP iş parçacığının önceliği.

> [!NOTE]
> DHCP kullanılıyorsa, DHCP iş parçacığı IP örneği iş parçacığından ve AutoIP iş parçacığından daha yüksek önceliğe sahip olmalıdır.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı AutoIP oluşturma.
- **NX_AUTO_IP_ERROR:**(0xA00) AutoIP oluşturma hatası.
- NX_PTR_ERROR: (0x16) Geçersiz AutoIP, ip_ptr veya yığın işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, İş Parçacıkları

### <a name="example"></a>Örnek

```c
/* Create the AutoIP instance "auto_ip_0" on "ip_0". */
status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);

/* If status is NX_SUCCESS an AutoIP instance was successfully created. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_delete"></a>nx_auto_ip_delete

AutoIP örneğini silme

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_delete(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a>Description

Bu hizmet, belirtilen IP örneğinde önceden oluşturulmuş bir AutoIP örneğini siler.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr:** AutoIP denetim bloğuna işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) AutoIP silme başarılı.
- **NX_AUTO_IP_ERROR:**(0xA00) AutoIP silme hatası.
- NX_PTR_ERROR (0x16): Geçersiz AutoIP işaretçisi.
- NX_CALLER_ERROR (0x11): Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

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

Geçerli AutoIP adresini al

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_get_address(NX_AUTO_IP *auto_ip_ptr,
                            ULONG *local_ip_address);
```

### <a name="description"></a>Description

Bu hizmet, o anda kurulumu yapılan AutoIP adresini alır. Yoksa, 0.0.0.0 IP adresi döndürülür.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr:** AutoIP denetim bloğuna işaretçi.
- **local_ip_address:** Dönüş IP adresi hedefi.

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı AutoIP adresi get.
- **NX_AUTO_IP_NO_LOCAL:**(0xA01) Geçerli bir AutoIP adresi yok.
- NX_PTR_ERROR: (0x16) Geçersiz AutoIP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, Süreerler, İş Parçacıkları, ISR'ler

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

AutoIP için ağ arabirimi ayarlama

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_set_interface(NX_AUTO_IP *auto_ip_ptr,
                                UINT interface_index);
```

### <a name="description"></a>Description

Bu hizmet, AutoIP ağ arabiriminin bir ağ IP adresi için yoklama dizini ayarlar. Varsayılan değer sıfırdır (birincil ağ arabirimi). Yalnızca birden çok ana bilgisayara bağlı cihazlar için geçerlidir.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr:** AutoIP denetim bloğuna işaretçi.
- **interface_index:** IÇIN IP adresini yoklama arabirimi

### <a name="return-values"></a>Dönüş Değerleri

- **NX_SUCCESS:**(0x00) Başarılı AutoIP arabirim kümesi
- **NX_AUTO_IP_BAD_INTERFACE_INDEX:**(0xA02) Geçersiz ağ arabirimi 
- NX_PTR_ERROR: (0x16) Geçersiz AutoIP işaretçisi.
- NX_CALLER_ERROR: (0x11) Bu hizmetin çağıranı geçersiz.

### <a name="allowed-from"></a>İzin Verilen

Başlatma, Süreerler, İş Parçacıkları, ISR'ler

### <a name="example"></a>Örnek

```c
ULONG interface_index;

/* Set the network interface on which AutoIP probes for host address. */
status = nx_auto_ip_set_interface(&auto_ip_0, interface_index);

/* If status is NX_SUCCESS the network interface is valid and set in the AutoIP control block auto_ip_0. */
```

### <a name="see-also"></a>Ayrıca Bkz.

nx_auto_ip_create, nx_auto_ip_get_address, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop

## <a name="nx_auto_ip_start"></a>nx_auto_ip_start

AutoIP işlemeyi başlatma

### <a name="prototype"></a>Prototype

```c
UINT nx_auto_ip_start(NX_AUTO_IP *auto_ip_ptr,
                    ULONG starting_local_address);
```

### <a name="description"></a>Description

Bu hizmet, önceden oluşturulmuş bir AutoIP örneğinde AutoIP protokolünü başlatır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **auto_ip_ptr:** AutoIP denetim bloğuna işaretçi.
- **starting_local_address:** İsteğe bağlı AutoIP başlangıç adresi. IP_ADDRESS (0,0,0,0,0) değeri, rastgele bir AutoIP adresinin türetilen gerektiğini belirtir. Aksi takdirde, geçerli bir AutoIP adresi belirtilirse, NetX AutoIP bu adresi atamaya çalışır.

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

### <a name="description"></a>Description

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