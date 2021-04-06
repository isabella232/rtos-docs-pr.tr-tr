---
title: Bölüm 2-yürütme profili seti API başvuruları
description: Bu bölüm EPK tarafından sunulan API işlevlerini belgeler.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a198e48bdacbc141fb3de4670cc7ea5ba079612d
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377632"
---
#  <a name="chapter-2--execution-profile-kit-api-references"></a>Bölüm 2 yürütme profili seti API başvuruları

ThreadX EPK, yürütme profili bilgilerini aşağıdaki şekilde almak için erişim işlevleri sağlar.

| İşlev &nbsp; adı | Açıklama |
| --- | --- |
| _tx_execution_thread_time_reset | Bir iş parçacığının birikmiş süresini sıfırlayın. |
| _tx_execution_thread_total_time_reset | Birikmiş toplam iş parçacığı süresini sıfırlayın. |
| _tx_execution_isr_time_reset | Birikmiş ıSR süresini sıfırlayın. |
| _tx_execution_idle_time_reset | Birikmiş boşta kalma süresini sıfırlayın. |
| bir iş parçacığının birikmiş süresini almak _tx_execution_thread_time_get. |
| _tx_execution_thread_total_time_get | Birikmiş toplam iş parçacığı süresini alır. |
| _tx_execution_isr_time_get | Birikmiş ıSR süresini alır. |
| _tx_execution_idle_time_get | Birikmiş boşta kalma süresini alır. |

##  <a name="_tx_execution_thread_time_reset"></a>_tx_execution_thread_time_reset

Bir iş parçacığının birikmiş süresini sıfırlayın.

### <a name="prototype"></a>Prototype

```C
UINT _tx_execution_thread_time_reset(TX_THREAD *thread_ptr);
```

### <a name="description"></a>Açıklama

Bu hizmet, birikmiş iş parçacığı yürütme süresini yeniden sıfıra ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

- **thread_ptr** İş parçacığı işaretçisi.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı epk sıfırlaması.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
/* Reset the execution time for thread_0.  */
status =  tx_execution_thread_time_reset(&thread_0);

/* If status is TX_SUCCESS thread_0's execution time is now 0.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_thread_total_time_reset"></a>_tx_execution_thread_total_time_reset

Toplam birikmiş iş parçacığı süresini sıfırlayın.

### <a name="prototype"></a>Prototype
```c
UINT _tx_execution_thread_total_time_reset(void);
```

### <a name="description"></a>Açıklama

Bu hizmet, birikmiş toplam iş parçacığı yürütme süresini sıfıra doğru ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

Yok.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı epk sıfırlaması.

### <a name="allowed-from"></a>İzin verilen

- İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
/* Reset the total execution time for all threads.  */
status =  tx_execution_thread_total_time_reset();

/* If status is TX_SUCCESS the total thread execution time is now 0.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- _tx_execution_thread_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_isr_time_reset"></a>_tx_execution_isr_time_reset

Birikmiş ıSR süresini sıfırlayın.

### <a name="prototype"></a>Prototype

```c
UINT _tx_execution_isr_time_reset(void);
```

### <a name="description"></a>Açıklama

Bu hizmet, birikmiş toplam ıSR yürütme süresini sıfıra doğru ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

Yok.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı epk sıfırlaması.

**İzin verilen**

- İş parçacıkları, zamanlayıcılar ve ISRs

**Örnek**

```c
/* Reset the total ISR execution time.  */
status =  tx_execution_isr_time_reset();

/* If status is TX_SUCCESS the total ISR execution time is now 0.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_idle_time_reset"></a>_tx_execution_idle_time_reset

Birikmiş boşta kalma süresini sıfırlayın.

### <a name="prototype"></a>Prototype

```c
UINT _tx_execution_idle_time_reset(void);
```

### <a name="description"></a>Açıklama

Bu hizmet, birikmiş toplam boşta çalışma süresini sıfıra doğru ayarlar.

### <a name="input-parameters"></a>Giriş Parametreleri

Yok.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı epk sıfırlaması.

### <a name="allowed-from"></a>İzin verilen

- İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
/* Reset the total idle execution time.  */
status =  tx_execution_idle_time_reset();

/* If status is TX_SUCCESS the total idle execution time is now 0.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_thread_time_get"></a>_tx_execution_thread_time_get

Bir iş parçacığının birikmiş süresini alır.

### <a name="prototype"></a>Prototype

```c
UINT _tx_execution_thread_time_get(
    TX_THREAD *thread_ptr,
    EXECUTION_TIME *total_time);
```

### <a name="description"></a>Açıklama

Bu hizmet, bir iş parçacığının birikmiş yürütme süresini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **thread_ptr** İş parçacığı işaretçisi.

- **total_time** İş parçacığı \' yürütme süresi için hedef.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı epk zamanı Get.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c

/* Get the total thread execution time for thread_0.  */
status =  tx_execution_thread_time_get(&thread_0, &execution_time);

/* If status is TX_SUCCESS, execution_time contains the thread's
   execution time.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_thread_total_time_get"></a>_tx_execution_thread_total_time_get

Toplam süreyi birikmiş iş parçacığına alın.

### <a name="prototype"></a>Prototype

```c
UINT _tx_execution_thread_total_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a>Açıklama

Bu hizmet birikmiş toplam iş parçacığı yürütme süresini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **total_time** Toplam iş parçacığı yürütme süresi için hedef.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı epk zamanı Get.

### <a name="allowed-from"></a>İzin verilen

- İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
EXECUTION_TIME *execution_time;

/* Get the total thread execution time.  */
status =  tx_execution_thread_total_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the thread
   execution time.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_isr_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_isr_time_get"></a>_tx_execution_isr_time_get

Birikmiş ıSR süresini alır.

### <a name="prototype"></a>Prototype

```c
UINT _tx_execution_isr_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a>Açıklama

Bu hizmet birikmiş ıSR yürütme süresini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **total_time** Toplam ıSR yürütme süresi için hedef.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı epk zamanı Get.

### <a name="allowed-from"></a>İzin verilen

İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
EXECUTION_TIME  *execution_time;

/* Get the total ISR execution time.  */
status =  tx_execution_isr_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the ISR
   execution time.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_idle_time_get

## <a name="_tx_execution_idle_time_get"></a>_tx_execution_idle_time_get

### <a name="get-the-accumulated-idle-time"></a>Birikmiş boşta kalma süresini al

### <a name="prototype"></a>Prototype

```c
UINT _tx_execution_idle_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a>Açıklama

Bu hizmet, birikmiş boşta yürütme süresini alır.

### <a name="input-parameters"></a>Giriş Parametreleri

- **total_time** Toplam boş yürütme süresi için hedef.

### <a name="return-values"></a>Dönüş Değerleri

- **TX_SUCCESS** (0x00) başarılı epk zamanı Get.

### <a name="allowed-from"></a>İzin verilen

- İş parçacıkları, zamanlayıcılar ve ISRs

### <a name="example"></a>Örnek

```c
EXECUTION_TIME  *execution_time;

/* Get the total idle execution time.  */
status =  tx_execution_idle_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the idle
   execution time.  */
```

### <a name="see-also"></a>Ayrıca Bkz.

- _tx_execution_thread_time_reset
- _tx_execution_thread_total_time_reset
- _tx_execution_isr_time_reset
- _tx_execution_idle_time_reset
- _tx_execution_thread_time_get
- _tx_execution_thread_total_time_get
- _tx_execution_isr_time_get
