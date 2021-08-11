---
title: Bölüm 3 - ARMv8-M için ThreadX API'leri
description: Bu bölümde ARMv8-M'ye özgü ThreadX hizmetlerinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 99633db55a5d93eb32ce4fb5429f3fe2f9ab5137cffc30b27982f702cece1ca5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791508"
---
# <a name="chapter-3--threadx-apis-for-armv8-m"></a>ARMv8-M için Bölüm 3 ThreadX API'leri

Bu bölümde ARMv8 M'ye özgü ThreadX hizmetlerinin alfabetik sırada bir açıklaması yer almaktadır. Adları, benzer hizmetlerin hepsi birlikte grup olacak şekilde tasarlanmıştır. Aşağıdaki açıklamalarda yer alan "Dönüş Değerleri" **bölümünde,** BOLD'daki  değerler API hata TX_DISABLE_ERROR_CHECKING için kullanılan tanımdan etkilenmez; ise kalın olmayan değerler tamamen devre dışı bırakılır.

- [tx_thread_secure_stack_allocate](#tx_thread_secure_stack_allocate) Güvenli bellekte iş parçacığı yığını ayırma.
- [tx_thread_secure_stack_free](#tx_thread_secure_stack_free) Güvenli bellekte boş iş parçacığı yığını

## <a name="tx_thread_secure_stack_allocate"></a>tx_thread_secure_stack_allocate

Güvenli bellekte iş parçacığı yığını ayırma.

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_secure_stack_allocate(
    TX_THREAD *thread_ptr, 
    ULONG stack_size);
```

### <a name="description"></a>Description

Bu hizmet, güvenli bellekte bayt stack_size yığın ayırır. Bu işlev, güvenli işlevleri çağıran her iş parçacığı için çağrılmalı.

### <a name="input-parameters"></a>Giriş Parametreleri

- **thread_ptr** Daha önce oluşturulan iş parçacığının işaretçisi.

- **stack_size** Güvenli yığının boyutu.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) Başarılı istek.

- **TX_SIZE_ERROR** (0x05) Yığın boyutu aralık dışında.

- **TX_THREAD_ERROR** (0x0E) Geçersiz iş parçacığı işaretçisi.

- **TX_NO_MEMORY** (0x10) Bellek ayrılamadı.

- **TX_CALLER_ERROR** (0x13) Bu hizmetin çağıranı geçersiz.

- **TX_FEATURE_NOT_ENABLED** (0xFF) Sistem güvenli modda çalıştıracak şekilde derlenmiş.

### <a name="allowed-from"></a>İzin Verilen

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

Güvenli bellekte bir iş parçacığı yığınını serbest bırak. 

### <a name="prototype"></a>Prototype

```c
UINT tx_thread_secure_stack_free(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Description

Bu hizmet, bir iş parçacığının güvenli yığınını güvenli bellekte serbest bıraktır. Bir iş parçacığı güvenli bir yığına sahipse ve iş parçacığı artık güvenli işlevleri çağırmayacaksa veya iş parçacığı silindiğinde bu işlev çağrılır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **thread_ptr** Daha önce oluşturulan iş parçacığının işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) Başarılı istek.

- **TX_THREAD_ERROR** (0x0E) Geçersiz iş parçacığı işaretçisi.

- **TX_CALLER_ERROR** (0x13) Bu hizmetin çağıranı geçersiz.

- **TX_FEATURE_NOT_ENABLED** (0xFF) Sistem güvenli modda çalıştıracak şekilde derlenmiş.

### <a name="allowed-from"></a>İzin Verilen

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
