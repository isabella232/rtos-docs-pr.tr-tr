---
title: Bölüm 4-modül API 'Leri
author: philmea
ms.author: philmea
description: Bu makale, bir modülün kullanabileceği ek API 'lerin bir özetidir.
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b5804e2dbb8d08a272abc85a583576f43b7204c1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825487"
---
# <a name="chapter-4---module-apis"></a>Bölüm 4-modül API 'Leri

## <a name="summary-of-module-apis"></a>Modül API 'Lerinin Özeti

Aşağıdaki gibi, bir modül için kullanılabilen birkaç ek API işlevi vardır:

- ***txm_module_application_request** _-_Application-yerleşik koda özgü istek
- *nesne * için modül dışında _-_Allocate bellek **txm_module_object_allocate***
- ***txm_module_object_deallocate** _-daha önce ayrılan nesne belleğini _Deallocate *
- ***txm_module_object_pointer_get** _-_Find sistem nesnesi ve nesne işaretçisini al *
- ***txm_module_object_pointer_get_extended** _-sistem nesnesi _Find ve nesne işaretçisini alma, ad uzunluğu güvenliği *

## <a name="return-values"></a>Dönüş değerleri

Bazı Azure RTOS API 'Leri için ek hata kodları döndürülür. Bu ek hata kodları aşağıdaki şekilde tanımlanmıştır:

- **TXM_MODULE_INVALID_PROPERTIES** (0xF3): modülün API çağrısı yapmak için doğru özelliklere sahip olmadığını gösterir. Örneğin, izleme API 'Lerini Kullanıcı modunda çağırma.
- **TXM_MODULE_INVALID_MEMORY** (0xf4): modül tarafından sağlanan belleğin geçersiz olduğunu veya geçersiz bir konumda olduğunu gösterir. Örneğin, bellek korumalı modüller ' de, nesne denetim bloklarının modülün erişebileceği bellekte yer açmasına izin verilmez.
- **TXM_MODULE_INVALID_CALLBACK** (0xf5): API 'de belirtilen geri çağırma, modülün kodunun aralığının dışında ve bu nedenle geçersiz.

---

## <a name="txm_module_application_request"></a>txm_module_application_request

Yerleşik koda uygulamaya özgü istek.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_application_request(
    ULONG request, 
    ULONG param_1,
    ULONG param_2,
    ULONG param_3);
```

### <a name="description"></a>Açıklama

Bu hizmet, belirtilen isteği uygulamanın yerleşik bölümüne yapar. İstek yapısının çağrıdan önce hazırlandığı varsayılır. İsteğin gerçek işleme, ***_txm_module_manager_application_request*** işlevindeki yerleşik kodda gerçekleşir. Varsayılan olarak, bu işlev boş bırakılır ve yerleşik uygulama geliştiricisinin değiştirmesi için tasarlanmıştır.

### <a name="input-parameters"></a>Giriş parametreleri

- **istek** İstek KIMLIĞI (uygulama tanımlı)
- **param_1** İlk parametre
- **param_2** İkinci parametre
- **param_3** Üçüncü parametre

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı istek.
- **TX_NOT_AVAILABLE** (0x1d) isteği, yerleşik kod tarafından desteklenmiyor.

### <a name="allowed-from"></a>İzin verilen

Modül iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Call application resident code with ID=77 and the
   parameters set to 1, 2, 3. */
status = txm_module_application_request(77, 1, 2, 3);

/* If status is TX_SUCCESS the request was successful. */
```

---

## <a name="txm_module_object_allocate"></a>txm_module_object_allocate

Bir modül nesnesi denetim bloğu için nesne havuzunda (yerleşik uygulama tarafından oluşturulan) bellek ayırır.

### <a name="prototype"></a>Prototype

```c
UINT txm_module_object_allocate(
   VOID **object_ptr, 
   ULONG object_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, modülün dışında bir modül nesnesi için bellek ayırır, bu da modülün kodu tarafından nesne denetim bloğunun bozulmasını önlemeye yardımcı olur. Bellek korumalı sistemlerde, tüm nesne denetim bloklarının oluşturulabilmesi için önce bu API ile ayrılması gerekir.

### <a name="input-parameters"></a>Giriş parametreleri

- **object_ptr** Başarılı ayırma üzerine nesne işaretçisinin hedefi.
- **object_size** Ayrılacak nesnenin bayt cinsinden boyutu.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı nesne ayırma.
- **TX_NO_MEMORY** (0x10) yeterli bellek yok.
- **TX_NOT_AVAILABLE** (0x1d) Modül Yöneticisi, öğesinden ayrılacak bir nesne havuzu oluşturmadı

### <a name="allowed-from"></a>İzin verilen

Modül iş parçacıkları

### <a name="example"></a>Örnek

```c
TX_QUEUE *queue_pointer;

/* Allocate a control block for a module message queue. */
status = txm_module_object_allocate(&queue_pointer, sizeof(TX_QUEUE));

/* If status is TX_SUCCESS the queue_pointer points to
   memory allocated outside of the module and can be supplied
   to tx_queue_create to create a queue for the module. */
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_object_deallocate
- txm_module_object_pointer_get

---

## <a name="txm_module_object_deallocate"></a>txm_module_object_deallocate

Önceden ayrılan nesne belleğini serbest bırak

### <a name="prototype"></a>Prototype

```c
UINT txm_module_object_deallocate(VOID *object_ptr);
```

### <a name="description"></a>Açıklama

***Bu hizmet artık gerekli olmadığından kullanım dışı*** bırakıldı.

Daha önce txm_module_object_allocate * _ aracılığıyla ayrılan bellek, ***_ _TX_ \_ _delete hizmetinde *serbest bırakılır****.

### <a name="input-parameters"></a>Giriş parametreleri

- **object_ptr** Serbest bırakma için nesne işaretçisi.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı nesne ayırma.

### <a name="allowed-from"></a>İzin verilen

Modül iş parçacıkları

### <a name="example"></a>Örnek

```c
TX_QUEUE *queue_pointer;

/* Deallocate control block for a module message queue. */
status = txm_module_object_deallocate(queue_pointer);

/* If status is TX_SUCCESS the object memory associated
   with queue_pointer is deallocated. */
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_object_allocate
- txm_module_object_pointer_get

---

## <a name="txm_module_object_pointer_get"></a>txm_module_object_pointer_get

Sistem nesnesi bul ve nesne işaretçisini al

### <a name="prototype"></a>Prototype

```c
UINT txm_module_object_pointer_get(
   UINT object_type, CHAR *name, 
   VOID **object_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet belirli bir ada sahip belirli bir türün nesne işaretçisini alır. Nesne bulunamazsa bir hata döndürülür. Aksi takdirde, nesne bulunursa, bu nesnenin adresi "object_ptr" içine yerleştirilir. Bu işaretçi daha sonra sistem hizmeti çağrıları yapmak, yerleşik kodla etkileşime geçmek ve/veya sistemdeki diğer yüklü modüller için kullanılabilir.

### <a name="input-parameters"></a>Giriş parametreleri

- **object_type** İstenen ThreadX nesnesi türü. Geçerli türler şunlardır:
  - TXM_BLOCK_POOL_OBJECT
  - TXM_BYTE_POOL_OBJECT
  - TXM_EVENT_FLAGS_OBJECT
  - TXM_MUTEX_OBJECT
  - TXM_QUEUE_OBJECT
  - TXM_SEMAPHORE_OBJECT
  - TXM_THREAD_OBJECT
  - TXM_TIMER_OBJECT
  - TXM_IP_OBJECT
  - TXM_PACKET_POOL_OBJECT
  - TXM_UDP_SOCKET_OBJECT
  - TXM_TCP_SOCKET_OBJECT
- **ad** Nesne oluşturulduğunda tanımlanan uygulamaya özgü nesne adı.
- **object_ptr** Nesne işaretçisinin hedefi.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı nesne Get.
- **TX_OPTION_ERROR** (0x08) geçersiz nesne türü.
- **TX_PTR_ERROR** (0x03) geçersiz hedef.
- **TX_SIZE_ERROR** (0x05) geçersiz boyut.
- **TX_NO_INSTANCE** (0x0D) nesne bulunamadı.

### <a name="allowed-from"></a>İzin verilen

Modül iş parçacıkları

### <a name="example"></a>Örnek

```c
TX_QUEUE *queue_pointer;

/* Find the pointer for "fft_queue" in the resident part
   of the application. */
status = txm_module_object_pointer_get(TXM_QUEUE_OBJECT,
         "fft_queue", &queue_pointer);

/* If status is TX_SUCCESS the found queue pointer is in
   "queue_pointer". This queue pointer can then be used to
   send messages to the "fft_queue." */
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_object_pointer_get_extended

---

## <a name="txm_module_object_pointer_get_extended"></a>txm_module_object_pointer_get_extended

Sistem nesnesi bul ve nesne işaretçisini al

### <a name="prototype"></a>Prototype

```c
UINT txm_module_object_pointer_get_extended(UINT object_type,
                                            CHAR *name,
                                            UINT name_length,
                                            VOID **object_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet belirli bir ada sahip belirli bir türün nesne işaretçisini alır. Nesne bulunamazsa bir hata döndürülür. Aksi takdirde, nesne bulunursa, bu nesnenin adresi "object_ptr" içine yerleştirilir. Bu işaretçi daha sonra sistem hizmeti çağrıları yapmak, yerleşik kodla etkileşime geçmek ve/veya sistemdeki diğer yüklü modüller için kullanılabilir.

### <a name="input-parameters"></a>Giriş parametreleri

- **object_type** İstenen ThreadX nesnesi türü. Geçerli türler şunlardır:
  - TXM_BLOCK_POOL_OBJECT
  - TXM_BYTE_POOL_OBJECT
  - TXM_EVENT_FLAGS_OBJECT
  - TXM_MUTEX_OBJECT
  - TXM_QUEUE_OBJECT
  - TXM_SEMAPHORE_OBJECT
  - TXM_THREAD_OBJECT
  - TXM_TIMER_OBJECT
  - TXM_IP_OBJECT
  - TXM_PACKET_POOL_OBJECT
  - TXM_UDP_SOCKET_OBJECT
  - TXM_TCP_SOCKET_OBJECT
- **ad** Nesne oluşturulduğunda tanımlanan uygulamaya özgü nesne adı.
- **name_length** Ad uzunluğu.
- **object_ptr** Nesne işaretçisinin hedefi.

### <a name="return-values"></a>Dönüş değerleri

- **TX_SUCCESS** (0x00) başarılı nesne Get.
- **TX_OPTION_ERROR** (0x08) geçersiz nesne türü.
- **TX_PTR_ERROR** (0x03) geçersiz hedef.
- **TX_SIZE_ERROR** (0x05) geçersiz boyut.
- **TX_NO_INSTANCE** (0x0D) nesne bulunamadı.

### <a name="allowed-from"></a>İzin verilen

Modül iş parçacıkları

### <a name="example"></a>Örnek

```c
TX_QUEUE *queue_pointer;

/* Find the pointer for "fft_queue" in the resident part
   of the application. */
   status = txm_module_object_pointer_get_extended(TXM_QUEUE_OBJECT,
            "fft_queue", 9, &queue_pointer);

/* If status is TX_SUCCESS the found queue pointer is in
   "queue_pointer". This queue pointer can then be used to
   send messages to the "fft_queue." */
```

### <a name="see-also"></a>Ayrıca bkz.

- txm_module_manager_object_pointer_get
