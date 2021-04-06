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
#  <a name="chapter-2--execution-profile-kit-api-references"></a><span data-ttu-id="ab11b-103">Bölüm 2 yürütme profili seti API başvuruları</span><span class="sxs-lookup"><span data-stu-id="ab11b-103">Chapter 2  Execution Profile Kit API References</span></span>

<span data-ttu-id="ab11b-104">ThreadX EPK, yürütme profili bilgilerini aşağıdaki şekilde almak için erişim işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab11b-104">The ThreadX EPK provides access functions to get the execution profile information, as follows.</span></span>

| <span data-ttu-id="ab11b-105">İşlev &nbsp; adı</span><span class="sxs-lookup"><span data-stu-id="ab11b-105">Function&nbsp;Name</span></span> | <span data-ttu-id="ab11b-106">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab11b-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab11b-107">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-107">_tx_execution_thread_time_reset</span></span> | <span data-ttu-id="ab11b-108">Bir iş parçacığının birikmiş süresini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="ab11b-108">Reset the accumulated time for a thread.</span></span> |
| <span data-ttu-id="ab11b-109">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-109">_tx_execution_thread_total_time_reset</span></span> | <span data-ttu-id="ab11b-110">Birikmiş toplam iş parçacığı süresini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="ab11b-110">Reset the accumulated total thread time.</span></span> |
| <span data-ttu-id="ab11b-111">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-111">_tx_execution_isr_time_reset</span></span> | <span data-ttu-id="ab11b-112">Birikmiş ıSR süresini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="ab11b-112">Reset the accumulated ISR time.</span></span> |
| <span data-ttu-id="ab11b-113">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-113">_tx_execution_idle_time_reset</span></span> | <span data-ttu-id="ab11b-114">Birikmiş boşta kalma süresini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="ab11b-114">Reset the accumulated idle time.</span></span> |
| <span data-ttu-id="ab11b-115">bir iş parçacığının birikmiş süresini almak _tx_execution_thread_time_get.</span><span class="sxs-lookup"><span data-stu-id="ab11b-115">_tx_execution_thread_time_get Get the accumulated time for a thread.</span></span> |
| <span data-ttu-id="ab11b-116">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-116">_tx_execution_thread_total_time_get</span></span> | <span data-ttu-id="ab11b-117">Birikmiş toplam iş parçacığı süresini alır.</span><span class="sxs-lookup"><span data-stu-id="ab11b-117">Get the accumulated total thread time.</span></span> |
| <span data-ttu-id="ab11b-118">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-118">_tx_execution_isr_time_get</span></span> | <span data-ttu-id="ab11b-119">Birikmiş ıSR süresini alır.</span><span class="sxs-lookup"><span data-stu-id="ab11b-119">Get the accumulated ISR time.</span></span> |
| <span data-ttu-id="ab11b-120">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-120">_tx_execution_idle_time_get</span></span> | <span data-ttu-id="ab11b-121">Birikmiş boşta kalma süresini alır.</span><span class="sxs-lookup"><span data-stu-id="ab11b-121">Get the accumulated idle time.</span></span> |

##  <a name="_tx_execution_thread_time_reset"></a><span data-ttu-id="ab11b-122">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-122">_tx_execution_thread_time_reset</span></span>

<span data-ttu-id="ab11b-123">Bir iş parçacığının birikmiş süresini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="ab11b-123">Reset the accumulated time for a thread.</span></span>

### <a name="prototype"></a><span data-ttu-id="ab11b-124">Prototype</span><span class="sxs-lookup"><span data-stu-id="ab11b-124">Prototype</span></span>

```C
UINT _tx_execution_thread_time_reset(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="ab11b-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab11b-125">Description</span></span>

<span data-ttu-id="ab11b-126">Bu hizmet, birikmiş iş parçacığı yürütme süresini yeniden sıfıra ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ab11b-126">This service sets the accumulated thread execution time back to zero.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab11b-127">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-127">Input Parameters</span></span>

- <span data-ttu-id="ab11b-128">**thread_ptr** İş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ab11b-128">**thread_ptr** Pointer to thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="ab11b-129">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-129">Return Values</span></span>

- <span data-ttu-id="ab11b-130">**TX_SUCCESS** (0x00) başarılı epk sıfırlaması.</span><span class="sxs-lookup"><span data-stu-id="ab11b-130">**TX_SUCCESS** (0x00) Successful EPK reset.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab11b-131">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ab11b-131">Allowed From</span></span>

<span data-ttu-id="ab11b-132">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ab11b-132">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ab11b-133">Örnek</span><span class="sxs-lookup"><span data-stu-id="ab11b-133">Example</span></span>

```c
/* Reset the execution time for thread_0.  */
status =  tx_execution_thread_time_reset(&thread_0);

/* If status is TX_SUCCESS thread_0's execution time is now 0.  */
```

### <a name="see-also"></a><span data-ttu-id="ab11b-134">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ab11b-134">See Also</span></span>

- <span data-ttu-id="ab11b-135">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-135">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="ab11b-136">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-136">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="ab11b-137">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-137">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="ab11b-138">tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-138">tx_execution_thread_time_get</span></span>
- <span data-ttu-id="ab11b-139">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-139">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="ab11b-140">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-140">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="ab11b-141">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-141">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_thread_total_time_reset"></a><span data-ttu-id="ab11b-142">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-142">_tx_execution_thread_total_time_reset</span></span>

<span data-ttu-id="ab11b-143">Toplam birikmiş iş parçacığı süresini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="ab11b-143">Reset the total accumulated thread time.</span></span>

### <a name="prototype"></a><span data-ttu-id="ab11b-144">Prototype</span><span class="sxs-lookup"><span data-stu-id="ab11b-144">Prototype</span></span>
```c
UINT _tx_execution_thread_total_time_reset(void);
```

### <a name="description"></a><span data-ttu-id="ab11b-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab11b-145">Description</span></span>

<span data-ttu-id="ab11b-146">Bu hizmet, birikmiş toplam iş parçacığı yürütme süresini sıfıra doğru ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ab11b-146">This service sets the accumulated total thread execution time back to zero.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab11b-147">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-147">Input Parameters</span></span>

<span data-ttu-id="ab11b-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="ab11b-148">None.</span></span>

### <a name="return-values"></a><span data-ttu-id="ab11b-149">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-149">Return Values</span></span>

- <span data-ttu-id="ab11b-150">**TX_SUCCESS** (0x00) başarılı epk sıfırlaması.</span><span class="sxs-lookup"><span data-stu-id="ab11b-150">**TX_SUCCESS** (0x00) Successful EPK reset.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab11b-151">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ab11b-151">Allowed From</span></span>

- <span data-ttu-id="ab11b-152">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ab11b-152">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ab11b-153">Örnek</span><span class="sxs-lookup"><span data-stu-id="ab11b-153">Example</span></span>

```c
/* Reset the total execution time for all threads.  */
status =  tx_execution_thread_total_time_reset();

/* If status is TX_SUCCESS the total thread execution time is now 0.  */
```

### <a name="see-also"></a><span data-ttu-id="ab11b-154">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ab11b-154">See Also</span></span>

- <span data-ttu-id="ab11b-155">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-155">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="ab11b-156">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-156">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="ab11b-157">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-157">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="ab11b-158">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-158">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="ab11b-159">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-159">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="ab11b-160">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-160">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="ab11b-161">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-161">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_isr_time_reset"></a><span data-ttu-id="ab11b-162">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-162">_tx_execution_isr_time_reset</span></span>

<span data-ttu-id="ab11b-163">Birikmiş ıSR süresini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="ab11b-163">Reset the accumulated ISR time.</span></span>

### <a name="prototype"></a><span data-ttu-id="ab11b-164">Prototype</span><span class="sxs-lookup"><span data-stu-id="ab11b-164">Prototype</span></span>

```c
UINT _tx_execution_isr_time_reset(void);
```

### <a name="description"></a><span data-ttu-id="ab11b-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab11b-165">Description</span></span>

<span data-ttu-id="ab11b-166">Bu hizmet, birikmiş toplam ıSR yürütme süresini sıfıra doğru ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ab11b-166">This service sets the accumulated total ISR execution time back to zero.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab11b-167">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-167">Input Parameters</span></span>

<span data-ttu-id="ab11b-168">Yok.</span><span class="sxs-lookup"><span data-stu-id="ab11b-168">None.</span></span>

### <a name="return-values"></a><span data-ttu-id="ab11b-169">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-169">Return Values</span></span>

- <span data-ttu-id="ab11b-170">**TX_SUCCESS** (0x00) başarılı epk sıfırlaması.</span><span class="sxs-lookup"><span data-stu-id="ab11b-170">**TX_SUCCESS** (0x00) Successful EPK reset.</span></span>

<span data-ttu-id="ab11b-171">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="ab11b-171">**Allowed From**</span></span>

- <span data-ttu-id="ab11b-172">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ab11b-172">Threads, timers, and ISRs</span></span>

<span data-ttu-id="ab11b-173">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="ab11b-173">**Example**</span></span>

```c
/* Reset the total ISR execution time.  */
status =  tx_execution_isr_time_reset();

/* If status is TX_SUCCESS the total ISR execution time is now 0.  */
```

### <a name="see-also"></a><span data-ttu-id="ab11b-174">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ab11b-174">See Also</span></span>

- <span data-ttu-id="ab11b-175">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-175">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="ab11b-176">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-176">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="ab11b-177">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-177">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="ab11b-178">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-178">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="ab11b-179">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-179">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="ab11b-180">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-180">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="ab11b-181">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-181">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_idle_time_reset"></a><span data-ttu-id="ab11b-182">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-182">_tx_execution_idle_time_reset</span></span>

<span data-ttu-id="ab11b-183">Birikmiş boşta kalma süresini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="ab11b-183">Reset the accumulated idle time.</span></span>

### <a name="prototype"></a><span data-ttu-id="ab11b-184">Prototype</span><span class="sxs-lookup"><span data-stu-id="ab11b-184">Prototype</span></span>

```c
UINT _tx_execution_idle_time_reset(void);
```

### <a name="description"></a><span data-ttu-id="ab11b-185">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab11b-185">Description</span></span>

<span data-ttu-id="ab11b-186">Bu hizmet, birikmiş toplam boşta çalışma süresini sıfıra doğru ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ab11b-186">This service sets the accumulated total idle execution time back to zero.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab11b-187">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-187">Input Parameters</span></span>

<span data-ttu-id="ab11b-188">Yok.</span><span class="sxs-lookup"><span data-stu-id="ab11b-188">None.</span></span>

### <a name="return-values"></a><span data-ttu-id="ab11b-189">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-189">Return Values</span></span>

- <span data-ttu-id="ab11b-190">**TX_SUCCESS** (0x00) başarılı epk sıfırlaması.</span><span class="sxs-lookup"><span data-stu-id="ab11b-190">**TX_SUCCESS** (0x00) Successful EPK reset.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab11b-191">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ab11b-191">Allowed From</span></span>

- <span data-ttu-id="ab11b-192">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ab11b-192">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ab11b-193">Örnek</span><span class="sxs-lookup"><span data-stu-id="ab11b-193">Example</span></span>

```c
/* Reset the total idle execution time.  */
status =  tx_execution_idle_time_reset();

/* If status is TX_SUCCESS the total idle execution time is now 0.  */
```

### <a name="see-also"></a><span data-ttu-id="ab11b-194">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ab11b-194">See Also</span></span>

- <span data-ttu-id="ab11b-195">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-195">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="ab11b-196">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-196">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="ab11b-197">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-197">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="ab11b-198">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-198">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="ab11b-199">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-199">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="ab11b-200">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-200">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="ab11b-201">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-201">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_thread_time_get"></a><span data-ttu-id="ab11b-202">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-202">_tx_execution_thread_time_get</span></span>

<span data-ttu-id="ab11b-203">Bir iş parçacığının birikmiş süresini alır.</span><span class="sxs-lookup"><span data-stu-id="ab11b-203">Get the accumulated time for a thread.</span></span>

### <a name="prototype"></a><span data-ttu-id="ab11b-204">Prototype</span><span class="sxs-lookup"><span data-stu-id="ab11b-204">Prototype</span></span>

```c
UINT _tx_execution_thread_time_get(
    TX_THREAD *thread_ptr,
    EXECUTION_TIME *total_time);
```

### <a name="description"></a><span data-ttu-id="ab11b-205">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab11b-205">Description</span></span>

<span data-ttu-id="ab11b-206">Bu hizmet, bir iş parçacığının birikmiş yürütme süresini alır.</span><span class="sxs-lookup"><span data-stu-id="ab11b-206">This service gets the accumulated execution time for a thread.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab11b-207">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-207">Input Parameters</span></span>

- <span data-ttu-id="ab11b-208">**thread_ptr** İş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="ab11b-208">**thread_ptr** Pointer to thread.</span></span>

- <span data-ttu-id="ab11b-209">**total_time** İş parçacığı \' yürütme süresi için hedef.</span><span class="sxs-lookup"><span data-stu-id="ab11b-209">**total_time** Destination for thread\'s execution time.</span></span>

### <a name="return-values"></a><span data-ttu-id="ab11b-210">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-210">Return Values</span></span>

- <span data-ttu-id="ab11b-211">**TX_SUCCESS** (0x00) başarılı epk zamanı Get.</span><span class="sxs-lookup"><span data-stu-id="ab11b-211">**TX_SUCCESS** (0x00) Successful EPK time get.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab11b-212">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ab11b-212">Allowed From</span></span>

<span data-ttu-id="ab11b-213">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ab11b-213">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ab11b-214">Örnek</span><span class="sxs-lookup"><span data-stu-id="ab11b-214">Example</span></span>

```c

/* Get the total thread execution time for thread_0.  */
status =  tx_execution_thread_time_get(&thread_0, &execution_time);

/* If status is TX_SUCCESS, execution_time contains the thread's
   execution time.  */
```

### <a name="see-also"></a><span data-ttu-id="ab11b-215">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ab11b-215">See Also</span></span>

- <span data-ttu-id="ab11b-216">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-216">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="ab11b-217">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-217">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="ab11b-218">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-218">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="ab11b-219">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-219">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="ab11b-220">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-220">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="ab11b-221">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-221">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="ab11b-222">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-222">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_thread_total_time_get"></a><span data-ttu-id="ab11b-223">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-223">_tx_execution_thread_total_time_get</span></span>

<span data-ttu-id="ab11b-224">Toplam süreyi birikmiş iş parçacığına alın.</span><span class="sxs-lookup"><span data-stu-id="ab11b-224">Get the accumulated thread total time.</span></span>

### <a name="prototype"></a><span data-ttu-id="ab11b-225">Prototype</span><span class="sxs-lookup"><span data-stu-id="ab11b-225">Prototype</span></span>

```c
UINT _tx_execution_thread_total_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a><span data-ttu-id="ab11b-226">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab11b-226">Description</span></span>

<span data-ttu-id="ab11b-227">Bu hizmet birikmiş toplam iş parçacığı yürütme süresini alır.</span><span class="sxs-lookup"><span data-stu-id="ab11b-227">This service gets the accumulated total thread execution time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab11b-228">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-228">Input Parameters</span></span>

- <span data-ttu-id="ab11b-229">**total_time** Toplam iş parçacığı yürütme süresi için hedef.</span><span class="sxs-lookup"><span data-stu-id="ab11b-229">**total_time** Destination for total thread execution time.</span></span>

### <a name="return-values"></a><span data-ttu-id="ab11b-230">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-230">Return Values</span></span>

- <span data-ttu-id="ab11b-231">**TX_SUCCESS** (0x00) başarılı epk zamanı Get.</span><span class="sxs-lookup"><span data-stu-id="ab11b-231">**TX_SUCCESS** (0x00) Successful EPK time get.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab11b-232">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ab11b-232">Allowed From</span></span>

- <span data-ttu-id="ab11b-233">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ab11b-233">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ab11b-234">Örnek</span><span class="sxs-lookup"><span data-stu-id="ab11b-234">Example</span></span>

```c
EXECUTION_TIME *execution_time;

/* Get the total thread execution time.  */
status =  tx_execution_thread_total_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the thread
   execution time.  */
```

### <a name="see-also"></a><span data-ttu-id="ab11b-235">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ab11b-235">See Also</span></span>

- <span data-ttu-id="ab11b-236">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-236">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="ab11b-237">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-237">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="ab11b-238">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-238">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="ab11b-239">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-239">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="ab11b-240">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-240">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="ab11b-241">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-241">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="ab11b-242">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-242">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_isr_time_get"></a><span data-ttu-id="ab11b-243">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-243">_tx_execution_isr_time_get</span></span>

<span data-ttu-id="ab11b-244">Birikmiş ıSR süresini alır.</span><span class="sxs-lookup"><span data-stu-id="ab11b-244">Get the accumulated ISR time.</span></span>

### <a name="prototype"></a><span data-ttu-id="ab11b-245">Prototype</span><span class="sxs-lookup"><span data-stu-id="ab11b-245">Prototype</span></span>

```c
UINT _tx_execution_isr_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a><span data-ttu-id="ab11b-246">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab11b-246">Description</span></span>

<span data-ttu-id="ab11b-247">Bu hizmet birikmiş ıSR yürütme süresini alır.</span><span class="sxs-lookup"><span data-stu-id="ab11b-247">This service gets the accumulated ISR execution time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab11b-248">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-248">Input Parameters</span></span>

- <span data-ttu-id="ab11b-249">**total_time** Toplam ıSR yürütme süresi için hedef.</span><span class="sxs-lookup"><span data-stu-id="ab11b-249">**total_time** Destination for total ISR execution time.</span></span>

### <a name="return-values"></a><span data-ttu-id="ab11b-250">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-250">Return Values</span></span>

- <span data-ttu-id="ab11b-251">**TX_SUCCESS** (0x00) başarılı epk zamanı Get.</span><span class="sxs-lookup"><span data-stu-id="ab11b-251">**TX_SUCCESS** (0x00) Successful EPK time get.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab11b-252">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ab11b-252">Allowed From</span></span>

<span data-ttu-id="ab11b-253">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ab11b-253">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ab11b-254">Örnek</span><span class="sxs-lookup"><span data-stu-id="ab11b-254">Example</span></span>

```c
EXECUTION_TIME  *execution_time;

/* Get the total ISR execution time.  */
status =  tx_execution_isr_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the ISR
   execution time.  */
```

### <a name="see-also"></a><span data-ttu-id="ab11b-255">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ab11b-255">See Also</span></span>

- <span data-ttu-id="ab11b-256">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-256">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="ab11b-257">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-257">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="ab11b-258">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-258">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="ab11b-259">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-259">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="ab11b-260">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-260">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="ab11b-261">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-261">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="ab11b-262">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-262">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_idle_time_get"></a><span data-ttu-id="ab11b-263">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-263">_tx_execution_idle_time_get</span></span>

### <a name="get-the-accumulated-idle-time"></a><span data-ttu-id="ab11b-264">Birikmiş boşta kalma süresini al</span><span class="sxs-lookup"><span data-stu-id="ab11b-264">Get the accumulated idle time</span></span>

### <a name="prototype"></a><span data-ttu-id="ab11b-265">Prototype</span><span class="sxs-lookup"><span data-stu-id="ab11b-265">Prototype</span></span>

```c
UINT _tx_execution_idle_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a><span data-ttu-id="ab11b-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab11b-266">Description</span></span>

<span data-ttu-id="ab11b-267">Bu hizmet, birikmiş boşta yürütme süresini alır.</span><span class="sxs-lookup"><span data-stu-id="ab11b-267">This service gets the accumulated idle execution time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab11b-268">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-268">Input Parameters</span></span>

- <span data-ttu-id="ab11b-269">**total_time** Toplam boş yürütme süresi için hedef.</span><span class="sxs-lookup"><span data-stu-id="ab11b-269">**total_time** Destination for total idle execution time.</span></span>

### <a name="return-values"></a><span data-ttu-id="ab11b-270">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="ab11b-270">Return Values</span></span>

- <span data-ttu-id="ab11b-271">**TX_SUCCESS** (0x00) başarılı epk zamanı Get.</span><span class="sxs-lookup"><span data-stu-id="ab11b-271">**TX_SUCCESS** (0x00) Successful EPK time get.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ab11b-272">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="ab11b-272">Allowed From</span></span>

- <span data-ttu-id="ab11b-273">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="ab11b-273">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="ab11b-274">Örnek</span><span class="sxs-lookup"><span data-stu-id="ab11b-274">Example</span></span>

```c
EXECUTION_TIME  *execution_time;

/* Get the total idle execution time.  */
status =  tx_execution_idle_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the idle
   execution time.  */
```

### <a name="see-also"></a><span data-ttu-id="ab11b-275">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ab11b-275">See Also</span></span>

- <span data-ttu-id="ab11b-276">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-276">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="ab11b-277">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-277">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="ab11b-278">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-278">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="ab11b-279">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="ab11b-279">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="ab11b-280">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-280">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="ab11b-281">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-281">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="ab11b-282">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="ab11b-282">_tx_execution_isr_time_get</span></span>
