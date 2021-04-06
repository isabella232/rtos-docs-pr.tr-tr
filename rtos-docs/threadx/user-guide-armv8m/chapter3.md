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
# <a name="chapter-3--threadx-apis-for-armv8-m"></a><span data-ttu-id="bd5db-103">ARMv8-d için Bölüm 3 ThreadX API 'Leri</span><span class="sxs-lookup"><span data-stu-id="bd5db-103">Chapter 3  ThreadX APIs for ARMv8-M</span></span>

<span data-ttu-id="bd5db-104">Bu bölüm, ARMv8-l 'e özgü ThreadX hizmetlerinin alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="bd5db-104">This chapter contains a description of the ARMv8-M-specific ThreadX services in alphabetic order.</span></span> <span data-ttu-id="bd5db-105">Adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bd5db-105">Their names are designed so all similar services are grouped together.</span></span> <span data-ttu-id="bd5db-106">Aşağıdaki açıklamaların "dönüş değerleri" bölümünde, **kalın yazı** DEĞERLERI, API hata denetimini devre dışı bırakmak için kullanılan tanımlama **TX_DISABLE_ERROR_CHECKING** etkilenmez; kalın olmayan ' de gösterilen değerler tamamen devre dışı kalır.</span><span class="sxs-lookup"><span data-stu-id="bd5db-106">In the "Return Values" section in the following descriptions, values in **BOLD** are not affected by the **TX_DISABLE_ERROR_CHECKING** define used to disable API error checking; while values shown in non-bold are completely disabled.</span></span>

- <span data-ttu-id="bd5db-107">[tx_thread_secure_stack_allocate](#tx_thread_secure_stack_allocate) Güvenli bellekte bir iş parçacığı yığını ayırın.</span><span class="sxs-lookup"><span data-stu-id="bd5db-107">[tx_thread_secure_stack_allocate](#tx_thread_secure_stack_allocate) Allocate a thread stack in secure memory.</span></span>
- <span data-ttu-id="bd5db-108">[tx_thread_secure_stack_free](#tx_thread_secure_stack_free) Güvenli bellekte ücretsiz iş parçacığı yığını</span><span class="sxs-lookup"><span data-stu-id="bd5db-108">[tx_thread_secure_stack_free](#tx_thread_secure_stack_free) Free thread stack in secure memory</span></span>

## <a name="tx_thread_secure_stack_allocate"></a><span data-ttu-id="bd5db-109">tx_thread_secure_stack_allocate</span><span class="sxs-lookup"><span data-stu-id="bd5db-109">tx_thread_secure_stack_allocate</span></span>

<span data-ttu-id="bd5db-110">Güvenli bellekte bir iş parçacığı yığını ayırın.</span><span class="sxs-lookup"><span data-stu-id="bd5db-110">Allocate a thread stack in secure memory.</span></span>

### <a name="prototype"></a><span data-ttu-id="bd5db-111">Prototype</span><span class="sxs-lookup"><span data-stu-id="bd5db-111">Prototype</span></span>

```c
UINT tx_thread_secure_stack_allocate(
    TX_THREAD *thread_ptr, 
    ULONG stack_size);
```

### <a name="description"></a><span data-ttu-id="bd5db-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd5db-112">Description</span></span>

<span data-ttu-id="bd5db-113">Bu hizmet, güvenli bellekte stack_size bayt boyutunda bir yığın ayırır.</span><span class="sxs-lookup"><span data-stu-id="bd5db-113">This service allocates a stack of size stack_size bytes in secure memory.</span></span> <span data-ttu-id="bd5db-114">Bu işlev, güvenli işlevleri çağıran her iş parçacığı için çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bd5db-114">This function should be called for every thread that calls secure functions.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bd5db-115">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bd5db-115">Input Parameters</span></span>

- <span data-ttu-id="bd5db-116">**thread_ptr** Daha önce oluşturulmuş iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="bd5db-116">**thread_ptr** Pointer to previously created thread.</span></span>

- <span data-ttu-id="bd5db-117">**stack_size** Güvenli yığının boyutu.</span><span class="sxs-lookup"><span data-stu-id="bd5db-117">**stack_size** Size of secure stack.</span></span>

### <a name="return-values"></a><span data-ttu-id="bd5db-118">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bd5db-118">Return Values</span></span>

- <span data-ttu-id="bd5db-119">**TX_SUCCESS** (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bd5db-119">**TX_SUCCESS** (0x00) Successful request.</span></span>

- <span data-ttu-id="bd5db-120">**TX_SIZE_ERROR** (0x05) yığın boyutu Aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="bd5db-120">**TX_SIZE_ERROR** (0x05) Stack size out of range.</span></span>

- <span data-ttu-id="bd5db-121">**TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bd5db-121">**TX_THREAD_ERROR** (0x0E) Invalid thread pointer.</span></span>

- <span data-ttu-id="bd5db-122">**TX_NO_MEMORY** (0x10) bellek ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="bd5db-122">**TX_NO_MEMORY** (0x10) Unable to allocate memory.</span></span>

- <span data-ttu-id="bd5db-123">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="bd5db-123">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

- <span data-ttu-id="bd5db-124">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem güvenli modda çalışacak şekilde derlendi.</span><span class="sxs-lookup"><span data-stu-id="bd5db-124">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled to run in secure mode.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bd5db-125">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bd5db-125">Allowed From</span></span>

<span data-ttu-id="bd5db-126">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bd5db-126">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="bd5db-127">Örnek</span><span class="sxs-lookup"><span data-stu-id="bd5db-127">Example</span></span>

```c
/* Create thread.  */
tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0, pointer, DEMO_STACK_SIZE, 1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);

/* Allocate secure stack so this thread can call secure functions.  */
status = tx_thread_secure_stack_allocate(&thread_0, 256);

/* If status is TX_SUCCESS the request was successful.  */
```

### <a name="see-also"></a><span data-ttu-id="bd5db-128">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bd5db-128">See Also</span></span>

<span data-ttu-id="bd5db-129">tx_thread_secure_stack_free</span><span class="sxs-lookup"><span data-stu-id="bd5db-129">tx_thread_secure_stack_free</span></span>

##  <a name="tx_thread_secure_stack_free"></a><span data-ttu-id="bd5db-130">tx_thread_secure_stack_free</span><span class="sxs-lookup"><span data-stu-id="bd5db-130">tx_thread_secure_stack_free</span></span>

<span data-ttu-id="bd5db-131">Güvenli bellekte bir iş parçacığı yığınını boşaltın.</span><span class="sxs-lookup"><span data-stu-id="bd5db-131">Free a thread stack in secure memory.</span></span> 

### <a name="prototype"></a><span data-ttu-id="bd5db-132">Prototype</span><span class="sxs-lookup"><span data-stu-id="bd5db-132">Prototype</span></span>

```c
UINT tx_thread_secure_stack_free(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="bd5db-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd5db-133">Description</span></span>

<span data-ttu-id="bd5db-134">Bu hizmet, bir iş parçacığının güvenli yığınını güvenli bellekte boşaltır.</span><span class="sxs-lookup"><span data-stu-id="bd5db-134">This service frees a thread's secure stack in secure memory.</span></span> <span data-ttu-id="bd5db-135">Bir iş parçacığının güvenli bir yığını varsa ve iş parçacığının artık güvenli işlevleri çağırması gerekmiyorsa veya iş parçacığı silinirse bu işlev çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bd5db-135">This function should be called if a thread has a secure stack and when the thread no longer needs to call secure functions or the thread is deleted.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="bd5db-136">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="bd5db-136">Input Parameters</span></span>

- <span data-ttu-id="bd5db-137">**thread_ptr** Daha önce oluşturulmuş iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="bd5db-137">**thread_ptr** Pointer to previously created thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="bd5db-138">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="bd5db-138">Return Values</span></span>

- <span data-ttu-id="bd5db-139">**TX_SUCCESS** (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="bd5db-139">**TX_SUCCESS** (0x00) Successful request.</span></span>

- <span data-ttu-id="bd5db-140">**TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="bd5db-140">**TX_THREAD_ERROR** (0x0E) Invalid thread pointer.</span></span>

- <span data-ttu-id="bd5db-141">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="bd5db-141">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

- <span data-ttu-id="bd5db-142">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem güvenli modda çalışacak şekilde derlendi.</span><span class="sxs-lookup"><span data-stu-id="bd5db-142">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled to run in secure mode.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="bd5db-143">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="bd5db-143">Allowed From</span></span>

<span data-ttu-id="bd5db-144">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="bd5db-144">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="bd5db-145">Örnek</span><span class="sxs-lookup"><span data-stu-id="bd5db-145">Example</span></span>

```c
/* Free thread’s secure stack.  */
status = tx_thread_secure_stack_free(&thread_0);

/* If status is TX_SUCCESS the request was successful.  */

/* Delete thread.  */
tx_thread_delete(&thread_0);
```

## <a name="see-also"></a><span data-ttu-id="bd5db-146">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bd5db-146">See Also</span></span>

<span data-ttu-id="bd5db-147">tx_thread_secure_stack_allocate</span><span class="sxs-lookup"><span data-stu-id="bd5db-147">tx_thread_secure_stack_allocate</span></span>
