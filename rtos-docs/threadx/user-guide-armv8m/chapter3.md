---
title: Bölüm 3-ARMv8-d için ThreadX API 'Leri
description: Bu bölümde ARMv8-l-specific ThreadX hizmetlerinin açıklaması.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 14bdfab3d56476d52ba91f859cec4af4ab7f4bef
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377631"
---
# <a name="chapter-3--threadx-apis-for-armv8-m"></a>ARMv8-d için Bölüm 3 ThreadX API 'Leri

Bu bölüm, ARMv8-l 'e özgü ThreadX hizmetlerinin alfabetik sırada bir açıklamasını içerir. Adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır. Aşağıdaki açıklamaların "dönüş değerleri" bölümünde, **kalın yazı** DEĞERLERI, API hata denetimini devre dışı bırakmak için kullanılan tanımlama **TX_DISABLE_ERROR_CHECKING** etkilenmez; kalın olmayan ' de gösterilen değerler tamamen devre dışı kalır.

- [tx_thread_secure_stack_allocate](#tx_thread_secure_stack_allocate) Güvenli bellekte bir iş parçacığı yığını ayırın.
- [tx_thread_secure_stack_free](#tx_thread_secure_stack_free) Güvenli bellekte ücretsiz iş parçacığı yığını

## <a name="tx_thread_secure_stack_allocate"></a>tx_thread_secure_stack_allocate

Güvenli bellekte bir iş parçacığı yığını ayırın.

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_secure_stack_allocate(
    TX_THREAD *thread_ptr, 
    ULONG stack_size);
```

### <a name="description"></a>Açıklama

Bu hizmet, güvenli bellekte stack_size bayt boyutunda bir yığın ayırır. Bu işlev, güvenli işlevleri çağıran her iş parçacığı için çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **thread_ptr** Daha önce oluşturulmuş iş parçacığına yönelik işaretçi.

- **stack_size** Güvenli yığının boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı istek.

- **TX_SIZE_ERROR** (0x05) yığın boyutu Aralık dışında.

- **TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı işaretçisi.

- **TX_NO_MEMORY** (0x10) bellek ayrılamıyor.

- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem güvenli modda çalışacak şekilde derlendi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Create thread.  */
tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0, pointer, DEMO_STACK_SIZE, 1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);

/* Allocate secure stack so this thread can call secure functions.  */
status = tx_thread_secure_stack_allocate(&thread_0, 256);

/* If status is TX_SUCCESS the request was successful.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

tx_thread_secure_stack_free

##  <a name="tx_thread_secure_stack_free"></a>tx_thread_secure_stack_free

Güvenli bellekte bir iş parçacığı yığınını boşaltın. 

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_secure_stack_free(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir iş parçacığının güvenli yığınını güvenli bellekte boşaltır. Bir iş parçacığının güvenli bir yığını varsa ve iş parçacığının artık güvenli işlevleri çağırması gerekmiyorsa veya iş parçacığı silinirse bu işlev çağrılmalıdır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **thread_ptr** Daha önce oluşturulmuş iş parçacığına yönelik işaretçi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı istek.

- **TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı işaretçisi.

- **TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.

- **TX_FEATURE_NOT_ENABLED** (0xFF) sistem güvenli modda çalışacak şekilde derlendi.

### <a name="allowed-from"></a>İzin verilen

Başlatma, iş parçacıkları

### <a name="example"></a>Örnek

```c
/* Free thread’s secure stack.  */
status = tx_thread_secure_stack_free(&thread_0);

/* If status is TX_SUCCESS the request was successful.  */

/* Delete thread.  */
tx_thread_delete(&thread_0);
```

## <a name="see-also"></a>Ayrıca Bkz.

tx_thread_secure_stack_allocate
