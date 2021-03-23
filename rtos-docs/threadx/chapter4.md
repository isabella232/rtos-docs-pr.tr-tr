---
title: Bölüm 4-Azure RTOS ThreadX hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS ThreadX hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 60ecc96df07b1f77b9b448814c4420133f3e2afc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825457"
---
# <a name="chapter-4---description-of-azure-rtos-threadx-services"></a><span data-ttu-id="9fec9-103">Bölüm 4-Azure RTOS ThreadX hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="9fec9-103">Chapter 4 - Description of Azure RTOS ThreadX Services</span></span>

<span data-ttu-id="9fec9-104">Bu bölüm, tüm Azure RTOS ThreadX hizmetlerinin alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-104">This chapter contains a description of all Azure RTOS ThreadX services in alphabetic order.</span></span> <span data-ttu-id="9fec9-105">Adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-105">Their names are designed so all similar services are grouped together.</span></span> <span data-ttu-id="9fec9-106">Aşağıdaki açıklamaların "dönüş değerleri" bölümünde, **kalın yazı** DEĞERLERI, API hata denetimini devre dışı bırakmak için kullanılan tanımlama **TX_DISABLE_ERROR_CHECKING** etkilenmez; kalın olmayan içinde gösterilen değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-106">In the "Return Values" section in the following descriptions, values in **BOLD** are not affected by the **TX_DISABLE_ERROR_CHECKING** define used to disable API error checking; while values shown in nonbold are completely disabled.</span></span> <span data-ttu-id="9fec9-107">Buna ek olarak, "**önalım olası**" başlığı altında listelenen bir "**Evet**" seçeneği, hizmeti çağırmanın daha yüksek öncelikli bir iş parçacığını sürdürüleceği ve bu nedenle çağıran iş parçacığını öncelik verme gösterir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-107">In addition, a "**Yes**" listed under the "**Preemption Possible**" heading indicates that calling the service may resume a higher-priority thread, thus preempting the calling thread.</span></span>

## <a name="tx_block_allocate"></a><span data-ttu-id="9fec9-108">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-108">tx_block_allocate</span></span>

<span data-ttu-id="9fec9-109">Sabit boyutlu bellek bloğunu ayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-109">Allocate fixed-size block of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-110">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-110">Prototype</span></span>

```c
UINT tx_block_allocate(
    TX_BLOCK_POOL *pool_ptr, 
    VOID **block_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="9fec9-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-111">Description</span></span>

<span data-ttu-id="9fec9-112">Bu hizmet, belirtilen bellek havuzundan sabit boyutlu bir bellek bloğu ayırır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-112">This service allocates a fixed-size memory block from the specified memory pool.</span></span> <span data-ttu-id="9fec9-113">Bellek bloğunun gerçek boyutu bellek havuzu oluşturma sırasında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-113">The actual size of the memory block is determined during memory pool creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-114">*Uygulama kodunun ayrılan bellek bloğunun dışına yazmadığından emin olmak önemlidir. Bu durumda, bir komşu (genellikle sonraki) bellek bloğunda bozulma oluşur. Sonuçlar tahmin edilemez ve genellikle önemli olur!*</span><span class="sxs-lookup"><span data-stu-id="9fec9-114">*It is important to ensure application code does not write outside the allocated memory block. If this happens, corruption occurs in an adjacent (usually subsequent) memory block. The results are unpredictable and often fatal!*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-115">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-115">Parameters</span></span>

- <span data-ttu-id="9fec9-116">**pool_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-116">**pool_ptr**</span></span> <br><span data-ttu-id="9fec9-117">Önceden oluşturulmuş bir bellek blok havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-117">Pointer to a previously created memory block pool.</span></span>
- <span data-ttu-id="9fec9-118">**block_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-118">**block_ptr**</span></span> <br><span data-ttu-id="9fec9-119">Hedef blok işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-119">Pointer to a destination block pointer.</span></span> <span data-ttu-id="9fec9-120">Başarılı bir ayırma sırasında, ayrılan bellek bloğunun adresi bu parametrenin gösterdiği yere yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-120">On successful allocation, the address of the allocated memory block is placed where this parameter points.</span></span>
- <span data-ttu-id="9fec9-121">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-121">**wait_option**</span></span> <br><span data-ttu-id="9fec9-122">Kullanılabilir bellek bloğu yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-122">Defines how the service behaves if there are no memory blocks available.</span></span> <span data-ttu-id="9fec9-123">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="9fec9-123">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9fec9-124">**TX_NO_WAIT** (0x00000000)- **TX_NO_WAIT** seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında dönüşte sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-124">**TX_NO_WAIT** (0x00000000) - Selecting **TX_NO_WAIT** results in an immediate return from this service regardless if it was successful or not.</span></span> <span data-ttu-id="9fec9-125">*Bu, hizmet iş parçacığından çağrıldığında geçerli olan tek seçenektir; Örneğin, başlatma, süreölçer veya ISR*.</span><span class="sxs-lookup"><span data-stu-id="9fec9-125">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR*.</span></span>
  - <span data-ttu-id="9fec9-126">**TX_WAIT_FOREVER** (0xFFFFFFF)- **TX_WAIT_FOREVER** seçme, bir bellek bloğu kullanılabilir olana kadar çağıran iş parçacığının süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-126">**TX_WAIT_FOREVER** (0xFFFFFFF) - Selecting **TX_WAIT_FOREVER** causes the calling thread to suspend indefinitely until a memory block is available.</span></span>
  - <span data-ttu-id="9fec9-127">*zaman aşımı değeri* (0x00000001-0xfffffffe)-sayısal bir değer (1-0XFFFFFFFE) seçildiğinde, bellek bloğu beklenirken askıya alınması için en fazla Zamanlayıcı sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-127">*timeout value* (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a memory block.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-128">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-128">Return Values</span></span>

- <span data-ttu-id="9fec9-129">**TX_SUCCESS**    (0x00) başarılı bellek bloğu ayırması.</span><span class="sxs-lookup"><span data-stu-id="9fec9-129">**TX_SUCCESS**    (0x00)  Successful memory block allocation.</span></span>
- <span data-ttu-id="9fec9-130">**TX_DELETED**    (0x01) bellek bloğu havuzu, iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-130">**TX_DELETED**    (0x01)  Memory block pool was deleted while thread was suspended.</span></span>
- <span data-ttu-id="9fec9-131">**TX_NO_MEMORY**  (0x10) hizmeti, belirli bir süre içinde beklenecek bir bellek bloğunu ayıramadı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-131">**TX_NO_MEMORY**  (0x10)  Service was unable to allocate a block of memory within the specified time to wait.</span></span>
- <span data-ttu-id="9fec9-132">**TX_WAIT_ABORTED**   (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-132">**TX_WAIT_ABORTED**   (0x1A)  Suspension was aborted by another thread, timer or ISR.</span></span>
- <span data-ttu-id="9fec9-133">**TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-133">**TX_POOL_ERROR** (0x02)  Invalid memory block pool pointer.</span></span>
- <span data-ttu-id="9fec9-134">**TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-134">**TX_WAIT_ERROR** (0x04)  A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="9fec9-135">**TX_PTR_ERROR**  (0x03) hedef işaretçisine geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-135">**TX_PTR_ERROR**  (0x03)  Invalid pointer to destination pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-136">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-136">Allowed From</span></span>

<span data-ttu-id="9fec9-137">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-137">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-138">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-138">Preemption Possible</span></span>

<span data-ttu-id="9fec9-139">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-139">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-140">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-140">Example</span></span>

```c
TX_BLOCK_POOL my_pool;
unsigned char *memory_ptr;

UINT status;

/* Allocate a memory block from my_pool. Assume that the pool has
already been created with a call to tx_block_pool_create. */

status = tx_block_allocate(&my_pool, (VOID **) &memory_ptr,
  TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the address of
the allocated block of memory. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-141">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-141">See Also</span></span>

- <span data-ttu-id="9fec9-142">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-142">tx_block_pool_create</span></span>
- <span data-ttu-id="9fec9-143">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-143">tx_block_pool_delete</span></span>
- <span data-ttu-id="9fec9-144">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-144">tx_block_pool_info_get</span></span>
- <span data-ttu-id="9fec9-145">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-145">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-146">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-146">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-147">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-147">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="9fec9-148">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-148">tx_block_release</span></span>

## <a name="tx_block_pool_create"></a><span data-ttu-id="9fec9-149">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-149">tx_block_pool_create</span></span>

<span data-ttu-id="9fec9-150">Sabit boyutlu bellek blokları Havuzu Oluştur</span><span class="sxs-lookup"><span data-stu-id="9fec9-150">Create pool of fixed-size memory blocks</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-151">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-151">Prototype</span></span>

```c
UINT tx_block_pool_create(
    TX_BLOCK_POOL pool_ptr,
    CHAR name_ptr, 
    ULONG block_size,
    VOID pool_start, 
    ULONG pool_size);
```

### <a name="description"></a><span data-ttu-id="9fec9-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-152">Description</span></span>

<span data-ttu-id="9fec9-153">Bu hizmet sabit boyutlu bellek blokları havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-153">This service creates a pool of fixed-size memory blocks.</span></span> <span data-ttu-id="9fec9-154">Belirtilen bellek alanı, formülü kullanılarak olabildiğince çok sabit boyutlu bellek bloklarına ayrılmıştır:</span><span class="sxs-lookup"><span data-stu-id="9fec9-154">The memory area specified is divided into as many fixed-size memory blocks as possible using the formula:</span></span>

<span data-ttu-id="9fec9-155">**Toplam blok** = (**toplam bayt**)/(**blok boyutu** + sizeof (void \*))</span><span class="sxs-lookup"><span data-stu-id="9fec9-155">**total blocks** = (**total bytes**) / (**block size** + sizeof(void \*))</span></span>

> [!NOTE]
><span data-ttu-id="9fec9-156">\* Her bellek bloğunda, kullanıcıya görünmeyen bir ek yük işaretçisi bulunur ve önceki formülde "sizeof (void *)"* ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-156">\*Each memory block contains one pointer of overhead that is invisible to the user and is represented by the "sizeof(void *)" in the preceding formula.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-157">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-157">Parameters</span></span>

- <span data-ttu-id="9fec9-158">**pool_ptr**  Bellek blok havuzu denetim bloğunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-158">**pool_ptr**  Pointer to a memory block pool control block.</span></span>
- <span data-ttu-id="9fec9-159">**name_ptr**  Bellek bloğu havuzunun adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-159">**name_ptr**  Pointer to the name of the memory block pool.</span></span>
- <span data-ttu-id="9fec9-160">**block_size**    Her bir bellek bloğundaki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-160">**block_size**    Number of bytes in each memory block.</span></span>
- <span data-ttu-id="9fec9-161">**pool_start**    Bellek bloğu havuzunun başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-161">**pool_start**    Starting address of the memory block pool.</span></span> <span data-ttu-id="9fec9-162">Başlangıç adresi ULONG veri türünün boyutuna hizalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-162">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="9fec9-163">**pool_size** Bellek blok havuzu için kullanılabilen toplam bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-163">**pool_size** Total number of bytes available for the memory block pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-164">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-164">Return Values</span></span>

- <span data-ttu-id="9fec9-165">**TX_SUCCESS**    (0x00) başarılı bellek bloğu havuzu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-165">**TX_SUCCESS**    (0x00)  Successful memory block pool creation.</span></span>
- <span data-ttu-id="9fec9-166">**TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-166">**TX_POOL_ERROR** (0x02)  Invalid memory block pool pointer.</span></span> <span data-ttu-id="9fec9-167">İşaretçi NULL ya da havuz zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9fec9-167">Either the pointer is NULL or the pool is already created.</span></span>
- <span data-ttu-id="9fec9-168">**TX_PTR_ERROR**  (0x03) havuzun başlangıç adresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-168">**TX_PTR_ERROR**  (0x03)  Invalid starting address of the pool.</span></span>
- <span data-ttu-id="9fec9-169">**TX_CALLER_ERROR**   (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-169">**TX_CALLER_ERROR**   (0x13)  Invalid caller of this service.</span></span>
- <span data-ttu-id="9fec9-170">**TX_SIZE_ERROR** (0x05) havuzun boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-170">**TX_SIZE_ERROR** (0x05)  Size of pool is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-171">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-171">Allowed From</span></span>

<span data-ttu-id="9fec9-172">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-172">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-173">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-173">Preemption Possible</span></span>

<span data-ttu-id="9fec9-174">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-174">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-175">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-175">Example</span></span>

```c
TX_BLOCK_POOL my_pool;

UINT status;

/* Create a memory pool whose total size is 1000 bytes starting at
address 0x100000. Each block in this pool is defined to be 50 bytes
long. */
status = tx_block_pool_create(&my_pool, "my_pool_name",
  50, (VOID *) 0x100000, 1000);

/* If status equals TX_SUCCESS, my_pool contains 18 memory blocks
of 50 bytes each. The reason there are not 20 blocks in the pool is
because of the one overhead pointer associated with each block. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-176">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-176">See Also</span></span>

- <span data-ttu-id="9fec9-177">tx_block_allocate, tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-177">tx_block_allocate, tx_block_pool_delete</span></span>
- <span data-ttu-id="9fec9-178">tx_block_pool_info_get, tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-178">tx_block_pool_info_get, tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-179">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-179">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-180">tx_block_pool_prioritize, tx_block_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-180">tx_block_pool_prioritize, tx_block_release</span></span>

## <a name="tx_block_pool_delete"></a><span data-ttu-id="9fec9-181">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-181">tx_block_pool_delete</span></span>

<span data-ttu-id="9fec9-182">Bellek blok havuzunu Sil</span><span class="sxs-lookup"><span data-stu-id="9fec9-182">Delete memory block pool</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-183">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-183">Prototype</span></span>

```c
UINT tx_block_pool_delete(TX_BLOCK_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-184">Description</span></span>

<span data-ttu-id="9fec9-185">Bu hizmet, belirtilen blok bellek havuzunu siler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-185">This service deletes the specified block-memory pool.</span></span> <span data-ttu-id="9fec9-186">Bu havuzdan bir bellek bloğunun beklediği tüm iş parçacıkları sürdürülür ve **TX_DELETED** bir dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-186">All threads suspended waiting for a memory block from this pool are resumed and given a **TX_DELETED** return status.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-187">*Bu hizmet tamamlandıktan sonra kullanılabilir olan havuz ile ilişkili bellek alanını yönetmek uygulamanın sorumluluğundadır. Ayrıca, uygulamanın silinen bir havuzun veya eski bellek bloklarının kullanımını engellemesi gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-187">*It is the application's responsibility to manage the memory area associated with the pool, which is available after this service completes. In addition, the application must prevent use of a deleted pool or its former memory blocks.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-188">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-188">Parameters</span></span>

- <span data-ttu-id="9fec9-189">**pool_ptr** Önceden oluşturulmuş bir bellek blok havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-189">**pool_ptr** Pointer to a previously created memory block pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-190">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-190">Return Values</span></span>

- <span data-ttu-id="9fec9-191">**TX_SUCCESS** (0x00) başarılı bellek blok havuzu silme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-191">**TX_SUCCESS** (0x00) Successful memory block pool deletion.</span></span>
- <span data-ttu-id="9fec9-192">**TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-192">**TX_POOL_ERROR** (0x02) Invalid memory block pool pointer.</span></span>
- <span data-ttu-id="9fec9-193">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-193">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-194">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-194">Allowed From</span></span>

<span data-ttu-id="9fec9-195">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-195">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-196">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-196">Preemption Possible</span></span>

<span data-ttu-id="9fec9-197">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-197">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-198">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-198">Example</span></span>

```c
TX_BLOCK_POOL my_pool;

UINT           status;

/* Delete entire memory block
pool. Assume that the pool has already been created with a call to
tx_block_pool_create. */
status = tx_block_pool_delete(&my_pool);

/* If status equals TX_SUCCESS, the memory block pool is deleted.*/
```

### <a name="see-also"></a><span data-ttu-id="9fec9-199">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-199">See Also</span></span>

- <span data-ttu-id="9fec9-200">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-200">tx_block_allocate</span></span>
- <span data-ttu-id="9fec9-201">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-201">tx_block_pool_create</span></span>
- <span data-ttu-id="9fec9-202">tx_block_pool_info_get, tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-202">tx_block_pool_info_get, tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-203">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-203">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-204">tx_block_pool_prioritize, tx_block_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-204">tx_block_pool_prioritize, tx_block_release</span></span>

## <a name="tx_block_pool_info_get"></a><span data-ttu-id="9fec9-205">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-205">tx_block_pool_info_get</span></span>

<span data-ttu-id="9fec9-206">Blok havuzu hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="9fec9-206">Retrieve information about block pool</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-207">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-207">Prototype</span></span>

```c
UINT tx_block_pool_info_get(
    TX_BLOCK_POOL *pool_ptr, 
    CHAR **name,
    ULONG *available, 
    ULONG *total_blocks,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_BLOCK_POOL **next_pool);
```

### <a name="description"></a><span data-ttu-id="9fec9-208">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-208">Description</span></span>

<span data-ttu-id="9fec9-209">Bu hizmet, belirtilen blok bellek havuzu hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-209">This service retrieves information about the specified block memory pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-210">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-210">Parameters</span></span>

- <span data-ttu-id="9fec9-211">**pool_ptr**  Daha önce oluşturulan bellek bloğu havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-211">**pool_ptr**  Pointer to previously created memory block pool.</span></span>
- <span data-ttu-id="9fec9-212">**ad**  Blok havuzunun adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-212">**name**  Pointer to destination for the pointer to the block pool's name.</span></span>
- <span data-ttu-id="9fec9-213">**kullanılabilir** Blok havuzundaki kullanılabilir blok sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-213">**available** Pointer to destination for the number of available blocks in the block pool.</span></span>
- <span data-ttu-id="9fec9-214">**total_blocks**  Blok havuzundaki toplam blok sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-214">**total_blocks**  Pointer to destination for the total number of blocks in the block pool.</span></span>
- <span data-ttu-id="9fec9-215">**first_suspended**   Bu blok havuzunun askıya alma listesindeki ilk iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-215">**first_suspended**   Pointer to destination for the pointer to the thread that is first on the suspension list of this block pool.</span></span>
- <span data-ttu-id="9fec9-216">**suspended_count**   Bu blok havuzunda Şu anda askıya alınmış iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-216">**suspended_count**   Pointer to destination for the number of threads currently suspended on this block pool.</span></span>
- <span data-ttu-id="9fec9-217">**next_pool** Sonraki oluşturulan blok havuzunun işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-217">**next_pool** Pointer to destination for the pointer of the next created block pool.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-218">*Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-218">*Supplying a TX_NULL for any parameter indicates the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-219">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-219">Return Values</span></span>

- <span data-ttu-id="9fec9-220">**TX_SUCCESS** (0x00) başarılı blok havuzu bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-220">**TX_SUCCESS** (0x00) Successful block pool information retrieve.</span></span>
- <span data-ttu-id="9fec9-221">**TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-221">**TX_POOL_ERROR** (0x02) Invalid memory block pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-222">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-222">Allowed From</span></span>

<span data-ttu-id="9fec9-223">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-223">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-224">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-224">Example</span></span>

```c
TX_BLOCK_POOL my_pool;
CHAR *name;
ULONG available;
ULONG total_blocks;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_BLOCK_POOL *next_pool;
UINT status;

/* Retrieve information about the previously created
block pool "my_pool." */
status = tx_block_pool_info_get(&my_pool, &name,
  &available,&total_blocks,
  &first_suspended, &suspended_count,
  &next_pool);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-225">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-225">See Also</span></span>

- <span data-ttu-id="9fec9-226">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-226">tx_block_allocate</span></span>
- <span data-ttu-id="9fec9-227">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-227">tx_block_pool_create</span></span>
- <span data-ttu-id="9fec9-228">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-228">tx_block_pool_delete</span></span>
- <span data-ttu-id="9fec9-229">tx_block_pool_info_get, tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-229">tx_block_pool_info_get, tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-230">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-230">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-231">tx_block_pool_prioritize, tx_block_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-231">tx_block_pool_prioritize, tx_block_release</span></span>

## <a name="tx_block_pool_performance_info_get"></a><span data-ttu-id="9fec9-232">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-232">tx_block_pool_performance_info_get</span></span>

<span data-ttu-id="9fec9-233">Blok havuzu performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-233">Get block pool performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-234">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-234">Prototype</span></span>

```c
UINT tx_block_pool_performance_info_get(
    TX_BLOCK_POOL *pool_ptr,
    ULONG *allocates, 
    ULONG *releases,
    ULONG *suspensions, 
    ULONG *timeouts));
```

### <a name="description"></a><span data-ttu-id="9fec9-235">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-235">Description</span></span>

<span data-ttu-id="9fec9-236">Bu hizmet, belirtilen bellek bloğu havuzuyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-236">This service retrieves performance information about the specified memory block pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-237">*ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-237">*The ThreadX library and application must be built with* **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-238">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-238">Parameters</span></span>

- <span data-ttu-id="9fec9-239">**pool_ptr**  Daha önce oluşturulan bellek bloğu havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-239">**pool_ptr**  Pointer to previously created memory block pool.</span></span>
- <span data-ttu-id="9fec9-240">**ayırır** Bu havuzda gerçekleştirilen ayırma isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-240">**allocates** Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="9fec9-241">**yayınlar**  Bu havuzda gerçekleştirilen yayın isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-241">**releases**  Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="9fec9-242">**getirilmesi**   Bu havuzdaki iş parçacığı ayırma getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-242">**suspensions**   Pointer to destination for the number of thread allocation suspensions on this pool.</span></span>
- <span data-ttu-id="9fec9-243">**zaman aşımları**  Bu havuzdaki askıya alma zaman aşımı sayısını ayır için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-243">**timeouts**  Pointer to destination for the number of allocate suspension timeouts on this pool.</span></span>

>[!NOTE]
> <span data-ttu-id="9fec9-244">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-244">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-245">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-245">Return Values</span></span>

- <span data-ttu-id="9fec9-246">**TX_SUCCESS**    (0x00) başarılı blok havuz performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-246">**TX_SUCCESS**    (0x00)  Successful block pool performance get.</span></span>
- <span data-ttu-id="9fec9-247">**TX_PTR_ERROR**  (0x03) geçersiz blok havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-247">**TX_PTR_ERROR**  (0x03)  Invalid block pool pointer.</span></span>
- <span data-ttu-id="9fec9-248">**TX_FEATURE_NOT_ENABLED**    (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-248">**TX_FEATURE_NOT_ENABLED**    (0xFF)  The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-249">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-249">Allowed From</span></span>

<span data-ttu-id="9fec9-250">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-250">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-251">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-251">Example</span></span>

```c
TX_BLOCK_POOL my_pool;
ULONG allocates;
ULONG releases;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created block
pool. */
status = tx_block_pool_performance_info_get(&my_pool, &allocates,
  &releases,
  &suspensions,
  &timeouts);

/* If status is TX_SUCCESS the performance information was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-252">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-252">See Also</span></span>

- <span data-ttu-id="9fec9-253">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-253">tx_block_allocate</span></span>
- <span data-ttu-id="9fec9-254">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-254">tx_block_pool_create</span></span>
- <span data-ttu-id="9fec9-255">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-255">tx_block_pool_delete</span></span>
- <span data-ttu-id="9fec9-256">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-256">tx_block_pool_info_get</span></span>
- <span data-ttu-id="9fec9-257">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-257">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-258">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-258">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-259">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-259">tx_block_release</span></span>

## <a name="tx_block_pool_performance_system_info_get"></a><span data-ttu-id="9fec9-260">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-260">tx_block_pool_performance_system_info_get</span></span>

<span data-ttu-id="9fec9-261">Blok havuzu sistem performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-261">Get block pool system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-262">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-262">Prototype</span></span>

```c
UINT tx_block_pool_performance_system_info_get(
    ULONG *allocates,
    ULONG *releases, 
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="9fec9-263">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-263">Description</span></span>

<span data-ttu-id="9fec9-264">Bu hizmet, uygulamadaki tüm bellek blok havuzlarıyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-264">This service retrieves performance information about all memory block pools in the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-265">*ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-265">*The ThreadX library and application must be built with* **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-266">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-266">Parameters</span></span>

- <span data-ttu-id="9fec9-267">**ayırır** Tüm blok havuzlarında gerçekleştirilen toplam ayırma isteği sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-267">**allocates** Pointer to destination for the total number of allocate requests performed on all block pools.</span></span>
- <span data-ttu-id="9fec9-268">**yayınlar**  Tüm blok havuzlarında gerçekleştirilen yayın isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-268">**releases**  Pointer to destination for the total number of release requests performed on all block pools.</span></span>
- <span data-ttu-id="9fec9-269">**getirilmesi**   Tüm blok havuzlarındaki iş parçacığı ayırma getirilmesi toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-269">**suspensions**   Pointer to destination for the total number of thread allocation suspensions on all block pools.</span></span>
- <span data-ttu-id="9fec9-270">**zaman aşımları**  Tüm blok havuzlarında askıya alınma zaman aşımlarının toplam sayısını ayırmak için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-270">**timeouts**  Pointer to destination for the total number of allocate suspension timeouts on all block pools.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-271">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-271">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-272">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-272">Return Values</span></span>

- <span data-ttu-id="9fec9-273">**TX_SUCCESS** (0x00) başarılı blok havuzu sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-273">**TX_SUCCESS** (0x00) Successful block pool system performance get.</span></span>
- <span data-ttu-id="9fec9-274">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-274">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-275">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-275">Allowed From</span></span>

<span data-ttu-id="9fec9-276">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-276">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-277">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-277">Example</span></span>

```c
ULONG       allocates;
ULONG       releases;
ULONG       suspensions;
ULONG       timeouts;

/* Retrieve performance information on all the block pools in
the system. */
status = tx_block_pool_performance_system_info_get(&allocates,
    &releases,&suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-278">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-278">See Also</span></span>

- <span data-ttu-id="9fec9-279">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-279">tx_block_allocate</span></span>
- <span data-ttu-id="9fec9-280">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-280">tx_block_pool_create</span></span>
- <span data-ttu-id="9fec9-281">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-281">tx_block_pool_delete</span></span>
- <span data-ttu-id="9fec9-282">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-282">tx_block_pool_info_get</span></span>
- <span data-ttu-id="9fec9-283">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-283">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-284">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-284">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="9fec9-285">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-285">tx_block_release</span></span>

## <a name="tx_block_pool_prioritize"></a><span data-ttu-id="9fec9-286">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-286">tx_block_pool_prioritize</span></span>

<span data-ttu-id="9fec9-287">Blok havuzunu askıya alma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="9fec9-287">Prioritize block pool suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-288">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-288">Prototype</span></span>

```c
UINT tx_block_pool_prioritize(TX_BLOCK_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-289">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-289">Description</span></span>

<span data-ttu-id="9fec9-290">Bu hizmet, askıya alma listesinin önünde bu havuzdaki bellek bloğu için en yüksek öncelikli iş parçacığını askıya aldı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-290">This service places the highest priority thread suspended for a block of memory on this pool at the front of the suspension list.</span></span> <span data-ttu-id="9fec9-291">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-291">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-292">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-292">Parameters</span></span>

- <span data-ttu-id="9fec9-293">**pool_ptr** Bellek blok havuzu denetim bloğunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-293">**pool_ptr** Pointer to a memory block pool control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-294">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-294">Return Values</span></span>

- <span data-ttu-id="9fec9-295">**TX_SUCCESS** (0x00) başarılı blok havuzu önceliği.</span><span class="sxs-lookup"><span data-stu-id="9fec9-295">**TX_SUCCESS** (0x00) Successful block pool prioritize.</span></span>
- <span data-ttu-id="9fec9-296">**TX_POOL_ERROR** (0x02) geçersiz bellek bloğu havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-296">**TX_POOL_ERROR** (0x02) Invalid memory block pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-297">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-297">Allowed From</span></span>

<span data-ttu-id="9fec9-298">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-298">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-299">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-299">Preemption Possible</span></span>

<span data-ttu-id="9fec9-300">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-300">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-301">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-301">Example</span></span>
```c
TX_BLOCK_POOL my_pool;
UINT status;

/* Ensure that the highest priority thread will receive
the next free block in this pool. */
status = tx_block_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_block_release call will wake up this thread. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-302">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-302">See Also</span></span>

- <span data-ttu-id="9fec9-303">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-303">tx_block_allocate</span></span>
- <span data-ttu-id="9fec9-304">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-304">tx_block_pool_create</span></span>
- <span data-ttu-id="9fec9-305">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-305">tx_block_pool_delete</span></span>
- <span data-ttu-id="9fec9-306">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-306">tx_block_pool_info_get</span></span>
- <span data-ttu-id="9fec9-307">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-307">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-308">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-308">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-309">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-309">tx_block_release</span></span>

## <a name="tx_block_release"></a><span data-ttu-id="9fec9-310">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-310">tx_block_release</span></span>

<span data-ttu-id="9fec9-311">Sabit boyutlu bellek bloğunu serbest bırakma</span><span class="sxs-lookup"><span data-stu-id="9fec9-311">Release fixed-size block of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-312">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-312">Prototype</span></span>

```c
UINT tx_block_release(VOID *block_ptr);
``````

### <a name="description"></a><span data-ttu-id="9fec9-313">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-313">Description</span></span>

<span data-ttu-id="9fec9-314">Bu hizmet önceden ayrılmış bir bloğu, ilişkili bellek havuzuna geri yayınlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-314">This service releases a previously allocated block back to its associated memory pool.</span></span> <span data-ttu-id="9fec9-315">Bu havuzdan bellek blokları bekleyen bir veya daha fazla iş parçacığı varsa, askıya alınan ilk iş parçacığına bu bellek bloğu verilir ve devam edilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-315">If there are one or more threads suspended waiting for memory blocks from this pool, the first thread suspended is given this memory block and resumed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="9fec9-316">*Uygulamanın, havuza geri sunulduktan sonra bir bellek bloğu alanını kullanmasını engellemesi gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-316">*The application must prevent using a memory block area after it has been released back to the pool.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-317">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-317">Parameters</span></span>

- <span data-ttu-id="9fec9-318">**block_ptr** Önceden ayrılmış bellek bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-318">**block_ptr** Pointer to the previously allocated memory block.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-319">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-319">Return Values</span></span>

- <span data-ttu-id="9fec9-320">**TX_SUCCESS** (0x00) başarılı bellek bloğu sürümü.</span><span class="sxs-lookup"><span data-stu-id="9fec9-320">**TX_SUCCESS** (0x00) Successful memory block release.</span></span>
- <span data-ttu-id="9fec9-321">**TX_PTR_ERROR** (0x03) bellek bloğunun işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-321">**TX_PTR_ERROR** (0x03) Invalid pointer to memory block.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-322">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-322">Allowed From</span></span>

<span data-ttu-id="9fec9-323">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-323">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-324">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-324">Preemption Possible</span></span>

<span data-ttu-id="9fec9-325">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-325">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-326">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-326">Example</span></span>

```c
TX_BLOCK_POOL my_pool;
unsigned char *memory_ptr;
UINT status;

/* Release a memory block back to my_pool. Assume that the
pool has been created and the memory block has been
allocated. */
status = tx_block_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the block of memory pointed
to by memory_ptr has been returned to the pool. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-327">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-327">See Also</span></span>

- <span data-ttu-id="9fec9-328">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-328">tx_block_allocate</span></span>
- <span data-ttu-id="9fec9-329">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-329">tx_block_pool_create</span></span>
- <span data-ttu-id="9fec9-330">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-330">tx_block_pool_delete</span></span>
- <span data-ttu-id="9fec9-331">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-331">tx_block_pool_info_get</span></span>
- <span data-ttu-id="9fec9-332">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-332">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-333">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-333">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-334">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-334">tx_block_pool_prioritize</span></span>

## <a name="tx_byte_allocate"></a><span data-ttu-id="9fec9-335">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-335">tx_byte_allocate</span></span>

<span data-ttu-id="9fec9-336">Bellek baytları ayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-336">Allocate bytes of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-337">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-337">Prototype</span></span>

```c
UINT tx_byte_allocate(
    TX_BYTE_POOL *pool_ptr,
    VOID **memory_ptr, 
    ULONG memory_size,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="9fec9-338">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-338">Description</span></span>

<span data-ttu-id="9fec9-339">Bu hizmet, belirtilen bellek bayt havuzundan belirtilen sayıda bayt ayırır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-339">This service allocates the specified number of bytes from the specified memory byte pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-340">*Uygulama kodunun ayrılan bellek bloğunun dışına yazmadığından emin olmak önemlidir. Bu durumda, bir komşu (genellikle sonraki) bellek bloğunda bozulma oluşur. Sonuçlar tahmin edilemez ve genellikle önemli olur!*</span><span class="sxs-lookup"><span data-stu-id="9fec9-340">*It is important to ensure application code does not write outside the allocated memory block. If this happens, corruption occurs in an adjacent (usually subsequent) memory block. The results are unpredictable and often fatal!*</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-341">*Bu hizmetin performansı, blok boyutunun ve havuzdaki parçalanma miktarının bir işlevidir. Bu nedenle, bu hizmet yürütmenin zaman kritik iş parçacıkları sırasında kullanılmamalıdır.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-341">*The performance of this service is a function of the block size and the amount of fragmentation in the pool. Hence, this service should not be used during time-critical threads of execution.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-342">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-342">Parameters</span></span>

- <span data-ttu-id="9fec9-343">**pool_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-343">**pool_ptr**</span></span> <br><span data-ttu-id="9fec9-344">Önceden oluşturulmuş bir bellek blok havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-344">Pointer to a previously created memory block pool.</span></span>
- <span data-ttu-id="9fec9-345">**memory_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-345">**memory_ptr**</span></span> <br><span data-ttu-id="9fec9-346">Hedef bellek işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-346">Pointer to a destination memory pointer.</span></span> <span data-ttu-id="9fec9-347">Başarılı bir ayırma sırasında, ayrılan bellek alanının adresi bu parametrenin işaret ettiği yere yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-347">On successful allocation, the address of the allocated memory area is placed where this parameter points to.</span></span>
- <span data-ttu-id="9fec9-348">**memory_size**</span><span class="sxs-lookup"><span data-stu-id="9fec9-348">**memory_size**</span></span> <br><span data-ttu-id="9fec9-349">İstenen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-349">Number of bytes requested.</span></span>
- <span data-ttu-id="9fec9-350">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-350">**wait_option**</span></span> <br><span data-ttu-id="9fec9-351">Yeterli kullanılabilir bellek yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-351">Defines how the service behaves if there is not enough memory available.</span></span> <span data-ttu-id="9fec9-352">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="9fec9-352">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9fec9-353">**TX_NO_WAIT** (0x00000000)- **TX_NO_WAIT** seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-353">**TX_NO_WAIT** (0x00000000) - Selecting **TX_NO_WAIT** results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="9fec9-354">*Bu, hizmet başlatma işleminden çağrıldığında geçerli tek seçenektir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-354">*This is the only valid option if the service is called from initialization.*</span></span>
  - <span data-ttu-id="9fec9-355">**TX_WAIT_FOREVER** 0xFFFFFFFF)- **TX_WAIT_FOREVER** seçilmesi, çağıran iş parçacığının yeterli bellek kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-355">**TX_WAIT_FOREVER** 0xFFFFFFFF) - Selecting **TX_WAIT_FOREVER** causes the calling thread to suspend indefinitely until enough memory is available.</span></span>
  - <span data-ttu-id="9fec9-356">*zaman aşımı değeri* (0x00000001-0xfffffffe)-sayısal bir değer (1-0XFFFFFFFE) seçildiğinde, bellek beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-356">*timeout value* (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the memory.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-357">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-357">Return Values</span></span>

- <span data-ttu-id="9fec9-358">**TX_SUCCESS** (0x00) başarılı bellek ayırması.</span><span class="sxs-lookup"><span data-stu-id="9fec9-358">**TX_SUCCESS** (0x00) Successful memory allocation.</span></span>
- <span data-ttu-id="9fec9-359">**TX_DELETED** (0x01) bellek havuzu, iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-359">**TX_DELETED** (0x01) Memory pool was deleted while thread was suspended.</span></span>
- <span data-ttu-id="9fec9-360">**TX_NO_MEMORY** (0x10) hizmeti, belleği, belirtilen süre içinde beklemek için ayıramadı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-360">**TX_NO_MEMORY** (0x10) Service was unable to allocate the memory within the specified time to wait.</span></span>
- <span data-ttu-id="9fec9-361">**TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-361">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="9fec9-362">**TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-362">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span>
- <span data-ttu-id="9fec9-363">**TX_PTR_ERROR** (0x03) hedef işaretçisine geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-363">**TX_PTR_ERROR** (0x03) Invalid pointer to destination pointer.</span></span>
- <span data-ttu-id="9fec9-364">**TX_SIZE_ERROR** (0x05) istenen boyut sıfır veya havuzdan büyük.</span><span class="sxs-lookup"><span data-stu-id="9fec9-364">**TX_SIZE_ERROR** (0X05) Requested size is zero or larger than the pool.</span></span>
- <span data-ttu-id="9fec9-365">**TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-365">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="9fec9-366">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-366">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-367">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-367">Allowed From</span></span>

<span data-ttu-id="9fec9-368">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-368">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-369">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-369">Preemption Possible</span></span>

<span data-ttu-id="9fec9-370">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-370">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-371">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-371">Example</span></span>
```c
TX_BYTE_POOL my_pool;
unsigned char*memory_ptr;
UINT status;
/* Allocate a 112 byte memory area from my_pool. Assume
that the pool has already been created with a call to
tx_byte_pool_create. */
status = tx_byte_allocate(&my_pool, (VOID **) &memory_ptr,
    112, TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the
address of the allocated memory area. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-372">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-372">See Also</span></span>

- <span data-ttu-id="9fec9-373">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-373">tx_byte_pool_create</span></span>
- <span data-ttu-id="9fec9-374">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-374">tx_byte_pool_delete</span></span>
- <span data-ttu-id="9fec9-375">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-375">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="9fec9-376">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-376">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-377">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-377">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-378">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-378">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="9fec9-379">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-379">tx_byte_release</span></span>

## <a name="tx_byte_pool_create"></a><span data-ttu-id="9fec9-380">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-380">tx_byte_pool_create</span></span>

<span data-ttu-id="9fec9-381">Bayt bellek havuzu oluştur</span><span class="sxs-lookup"><span data-stu-id="9fec9-381">Create memory pool of bytes</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-382">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-382">Prototype</span></span>

```c
UINT tx_byte_pool_create(
    TX_BYTE_POOL *pool_ptr,
    CHAR *name_ptr, 
    VOID *pool_start,
    ULONG pool_size);
```

### <a name="description"></a><span data-ttu-id="9fec9-383">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-383">Description</span></span>

<span data-ttu-id="9fec9-384">Bu hizmet, belirtilen alanda bir bellek bayt havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-384">This service creates a memory byte pool in the area specified.</span></span> <span data-ttu-id="9fec9-385">İlk olarak havuz, temel olarak bir çok büyük ücretsiz bloğundan oluşur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-385">Initially the pool consists of basically one very large free block.</span></span> <span data-ttu-id="9fec9-386">Ancak, ayırmalar yapıldığından havuz daha küçük bloklar halinde bozulur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-386">However, the pool is broken into smaller blocks as allocations are made.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-387">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-387">Parameters</span></span>

- <span data-ttu-id="9fec9-388">**pool_ptr** Bellek havuzu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-388">**pool_ptr** Pointer to a memory pool control block.</span></span>
- <span data-ttu-id="9fec9-389">**name_ptr** Bellek havuzunun adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-389">**name_ptr** Pointer to the name of the memory pool.</span></span>
- <span data-ttu-id="9fec9-390">**pool_start** Bellek havuzunun başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-390">**pool_start** Starting address of the memory pool.</span></span> <span data-ttu-id="9fec9-391">Başlangıç adresi ULONG veri türünün boyutuna hizalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-391">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="9fec9-392">**pool_size** Bellek havuzu için kullanılabilen toplam bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-392">**pool_size** Total number of bytes available for the memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-393">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-393">Return Values</span></span>

- <span data-ttu-id="9fec9-394">**TX_SUCCESS** (0x00) başarılı bellek havuzu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-394">**TX_SUCCESS** (0x00) Successful memory pool creation.</span></span>
- <span data-ttu-id="9fec9-395">**TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-395">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span> <span data-ttu-id="9fec9-396">İşaretçi NULL ya da havuz zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9fec9-396">Either the pointer is NULL or the pool is already created.</span></span>
- <span data-ttu-id="9fec9-397">**TX_PTR_ERROR** (0x03) havuzun başlangıç adresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-397">**TX_PTR_ERROR** (0x03) Invalid starting address of the pool.</span></span>
- <span data-ttu-id="9fec9-398">**TX_SIZE_ERROR** (0x05) havuzun boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-398">**TX_SIZE_ERROR** (0x05) Size of pool is invalid.</span></span>
- <span data-ttu-id="9fec9-399">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-399">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-400">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-400">Allowed From</span></span>

<span data-ttu-id="9fec9-401">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-401">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-402">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-402">Preemption Possible</span></span>

<span data-ttu-id="9fec9-403">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-403">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-404">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-404">Example</span></span>

```c
TX_BYTE_POOL my_pool;
UINT status;
/* Create a memory pool whose total size is 2000 bytes
starting at address 0x500000. */
status = tx_byte_pool_create(&my_pool, "my_pool_name",
    (VOID *) 0x500000, 2000);

/* If status equals TX_SUCCESS, my_pool is available for
allocating memory. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-405">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-405">See Also</span></span>

- <span data-ttu-id="9fec9-406">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-406">tx_byte_allocate</span></span>
- <span data-ttu-id="9fec9-407">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-407">tx_byte_pool_delete</span></span>
- <span data-ttu-id="9fec9-408">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-408">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="9fec9-409">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-409">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-410">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-410">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-411">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-411">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="9fec9-412">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-412">tx_byte_release</span></span>

## <a name="tx_byte_pool_delete"></a><span data-ttu-id="9fec9-413">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-413">tx_byte_pool_delete</span></span>

<span data-ttu-id="9fec9-414">Bellek bayt havuzunu Sil</span><span class="sxs-lookup"><span data-stu-id="9fec9-414">Delete memory byte pool</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-415">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-415">Prototype</span></span>

```c
UINT tx_byte_pool_delete(TX_BYTE_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-416">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-416">Description</span></span>

<span data-ttu-id="9fec9-417">Bu hizmet, belirtilen bellek bayt havuzunu siler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-417">This service deletes the specified memory byte pool.</span></span> <span data-ttu-id="9fec9-418">Bu havuzdan bellek beklemeyi askıya alınmış tüm iş parçacıkları sürdürülür ve **TX_DELETED** bir dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-418">All threads suspended waiting for memory from this pool are resumed and given a **TX_DELETED** return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-419">*Bu hizmet tamamlandıktan sonra kullanılabilir olan havuz ile ilişkili bellek alanını yönetmek uygulamanın sorumluluğundadır. Ayrıca, uygulamanın silinen bir havuzun veya daha önce ayrılmış belleğin kullanımını önlemesi gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-419">*It is the application's responsibility to manage the memory area associated with the pool, which is available after this service completes. In addition, the application must prevent use of a deleted pool or memory previously allocated from it.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-420">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-420">Parameters</span></span>

- <span data-ttu-id="9fec9-421">**pool_ptr** Daha önce oluşturulmuş bir bellek havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-421">**pool_ptr** Pointer to a previously created memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-422">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-422">Return Values</span></span>

- <span data-ttu-id="9fec9-423">**TX_SUCCESS** (0x00) başarılı bellek havuzu silme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-423">**TX_SUCCESS** (0x00) Successful memory pool deletion.</span></span>
- <span data-ttu-id="9fec9-424">**TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-424">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span>
- <span data-ttu-id="9fec9-425">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-425">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-426">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-426">Allowed From</span></span>

<span data-ttu-id="9fec9-427">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-427">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-428">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-428">Preemption Possible</span></span>

<span data-ttu-id="9fec9-429">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-429">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-430">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-430">Example</span></span>

```c
TX_BYTE_POOL my_pool;
UINT status;
/* Delete entire memory pool. Assume that the pool has already
been created with a call to tx_byte_pool_create. */
status = tx_byte_pool_delete(&my_pool);

/* If status equals TX_SUCCESS, memory pool is deleted. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-431">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-431">See Also</span></span>

- <span data-ttu-id="9fec9-432">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-432">tx_byte_allocate</span></span>
- <span data-ttu-id="9fec9-433">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-433">tx_byte_pool_create</span></span>
- <span data-ttu-id="9fec9-434">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-434">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="9fec9-435">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-435">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-436">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-436">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-437">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-437">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="9fec9-438">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-438">tx_byte_release</span></span>

## <a name="tx_byte_pool_info_get"></a><span data-ttu-id="9fec9-439">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-439">tx_byte_pool_info_get</span></span>

<span data-ttu-id="9fec9-440">Bayt havuzu hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="9fec9-440">Retrieve information about byte pool</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-441">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-441">Prototype</span></span>

```c
UINT tx_byte_pool_info_get(
    TX_BYTE_POOL *pool_ptr, 
    CHAR **name,
    ULONG *available, 
    ULONG *fragments,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_BYTE_POOL **next_pool);
```

### <a name="description"></a><span data-ttu-id="9fec9-442">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-442">Description</span></span>

<span data-ttu-id="9fec9-443">Bu hizmet, belirtilen bellek bayt havuzu hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-443">This service retrieves information about the specified memory byte pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-444">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-444">Parameters</span></span>

- <span data-ttu-id="9fec9-445">**pool_ptr** Daha önce oluşturulmuş bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-445">**pool_ptr** Pointer to previously created memory pool.</span></span>
- <span data-ttu-id="9fec9-446">**ad** Bayt havuzunun adı işaretçisinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-446">**name** Pointer to destination for the pointer to the byte pool's name.</span></span>
- <span data-ttu-id="9fec9-447">**kullanılabilir** Havuzdaki kullanılabilir bayt sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-447">**available** Pointer to destination for the number of available bytes in the pool.</span></span>
- <span data-ttu-id="9fec9-448">**parçalar** Bayt havuzundaki toplam bellek parçası sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-448">**fragments** Pointer to destination for the total number of memory fragments in the byte pool.</span></span>
- <span data-ttu-id="9fec9-449">**first_suspended** Bu bayt havuzunun askıya alma listesindeki iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-449">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this byte pool.</span></span>
- <span data-ttu-id="9fec9-450">**suspended_count** Bu bayt havuzunda Şu anda askıya alınan iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-450">**suspended_count** Pointer to destination for the number of threads currently suspended on this byte pool.</span></span>
- <span data-ttu-id="9fec9-451">**next_pool** Sonraki oluşturulan bayt havuzunun işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-451">**next_pool** Pointer to destination for the pointer of the next created byte pool.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-452">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-452">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-453">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-453">Return Values</span></span>

- <span data-ttu-id="9fec9-454">**TX_SUCCESS** (0x00) başarılı havuz bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-454">**TX_SUCCESS** (0x00) Successful pool information retrieve.</span></span>
- <span data-ttu-id="9fec9-455">**TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-455">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-456">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-456">Allowed From</span></span>

<span data-ttu-id="9fec9-457">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-457">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-458">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-458">Preemption Possible</span></span>

<span data-ttu-id="9fec9-459">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-459">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-460">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-460">Example</span></span>

```c
TX_BYTE_POOL my_pool;
CHAR *name;
ULONG available;
ULONG fragments;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_BYTE_POOL *next_pool;
UINT status;

/* Retrieve information about the previously created
block pool "my_pool." */
status = tx_byte_pool_info_get(&my_pool, &name,
  &available, &fragments,
  &first_suspended, &suspended_count,
  &next_pool);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-461">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-461">See Also</span></span>

- <span data-ttu-id="9fec9-462">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-462">tx_byte_allocate</span></span>
- <span data-ttu-id="9fec9-463">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-463">tx_byte_pool_create</span></span>
- <span data-ttu-id="9fec9-464">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-464">tx_byte_pool_delete</span></span>
- <span data-ttu-id="9fec9-465">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-465">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-466">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-466">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-467">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-467">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="9fec9-468">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-468">tx_byte_release</span></span>

## <a name="tx_byte_pool_performance_info_get"></a><span data-ttu-id="9fec9-469">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-469">tx_byte_pool_performance_info_get</span></span>

<span data-ttu-id="9fec9-470">Bayt havuzu performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-470">Get byte pool performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-471">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-471">Prototype</span></span>

```c
UINT tx_byte_pool_performance_info_get(
    TX_BYTE_POOL *pool_ptr,
    ULONG *allocates, 
    ULONG *releases,
    ULONG *fragments_searched, 
    ULONG *merges, 
    ULONG *splits,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="9fec9-472">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-472">Description</span></span>

<span data-ttu-id="9fec9-473">Bu hizmet, belirtilen bellek bayt havuzuyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-473">This service retrieves performance information about the specified memory byte pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-474">*ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-474">*The ThreadX library and application must be built with* **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-475">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-475">Parameters</span></span>

- <span data-ttu-id="9fec9-476">**pool_ptr** Daha önce oluşturulan bellek bayt havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-476">**pool_ptr** Pointer to previously created memory byte pool.</span></span>
- <span data-ttu-id="9fec9-477">**ayırır** Bu havuzda gerçekleştirilen ayırma isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-477">**allocates** Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="9fec9-478">**yayınlar** Bu havuzda gerçekleştirilen yayın isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-478">**releases** Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="9fec9-479">**fragments_searched** Bu havuzdaki ayırma istekleri sırasında aranan iç bellek parçacıklarının sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-479">**fragments_searched** Pointer to destination for the number of internal memory fragments searched during allocation requests on this pool.</span></span>
- <span data-ttu-id="9fec9-480">**birleştirmeler** Bu havuzdaki ayırma istekleri sırasında birleştirilmiş iç bellek blokları sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-480">**merges** Pointer to destination for the number of internal memory blocks merged during allocation requests on this pool.</span></span>
- <span data-ttu-id="9fec9-481">**böler** Bu havuzdaki ayırma istekleri sırasında oluşturulan iç bellek blokları sayısı (parçalar) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-481">**splits** Pointer to destination for the number of internal memory blocks split (fragments) created during allocation requests on this pool.</span></span>
- <span data-ttu-id="9fec9-482">**getirilmesi** Bu havuzdaki iş parçacığı ayırma getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-482">**suspensions** Pointer to destination for the number of thread allocation suspensions on this pool.</span></span>
- <span data-ttu-id="9fec9-483">**zaman aşımları** Bu havuzdaki askıya alma zaman aşımı sayısını ayır için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-483">**timeouts** Pointer to destination for the number of allocate suspension timeouts on this pool.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-484">*Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-484">*Supplying a TX_NULL for any parameter indicates the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-485">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-485">Return Values</span></span>

- <span data-ttu-id="9fec9-486">**TX_SUCCESS** (0x00) başarılı bayt havuzu performans Get.</span><span class="sxs-lookup"><span data-stu-id="9fec9-486">**TX_SUCCESS** (0x00) Successful byte pool performance get.</span></span>
- <span data-ttu-id="9fec9-487">**TX_PTR_ERROR** (0x03) geçersiz bayt havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-487">**TX_PTR_ERROR** (0x03) Invalid byte pool pointer.</span></span>
- <span data-ttu-id="9fec9-488">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-488">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-489">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-489">Allowed From</span></span>

<span data-ttu-id="9fec9-490">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-490">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-491">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-491">Example</span></span>

```c
TX_BYTE_POOL my_pool;
ULONG fragments_searched;
ULONG merges;
ULONG splits;
ULONG allocates;
ULONG releases;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created byte
pool. */
status = tx_byte_pool_performance_info_get(&my_pool,
  &fragments_searched,
  &merges, &splits,
  &allocates, &releases,
  &suspensions,&timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="9fec9-492">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-492">See Also</span></span>

- <span data-ttu-id="9fec9-493">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-493">tx_byte_allocate</span></span>
- <span data-ttu-id="9fec9-494">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-494">tx_byte_pool_create</span></span>
- <span data-ttu-id="9fec9-495">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-495">tx_byte_pool_delete</span></span>
- <span data-ttu-id="9fec9-496">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-496">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="9fec9-497">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-497">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-498">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-498">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="9fec9-499">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-499">tx_byte_release</span></span>

## <a name="tx_byte_pool_performance_system_info_get"></a><span data-ttu-id="9fec9-500">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-500">tx_byte_pool_performance_system_info_get</span></span>

<span data-ttu-id="9fec9-501">Bayt havuzu sistem performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-501">Get byte pool system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-502">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-502">Prototype</span></span>

```c
UINT tx_byte_pool_performance_system_info_get(
    ULONG *allocates,
    ULONG *releases, 
    ULONG *fragments_searched, 
    ULONG *merges,
    ULONG *splits, 
    ULONG *suspensions, 
    ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="9fec9-503">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-503">Description</span></span>

<span data-ttu-id="9fec9-504">Bu hizmet sistemdeki tüm bellek bayt havuzlarıyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-504">This service retrieves performance information about all memory byte pools in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-505">*ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-505">*The ThreadX library and application must be built with* **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-506">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-506">Parameters</span></span>

- <span data-ttu-id="9fec9-507">**ayırır** Bu havuzda gerçekleştirilen ayırma isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-507">**allocates** Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="9fec9-508">**yayınlar** Bu havuzda gerçekleştirilen yayın isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-508">**releases** Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="9fec9-509">**fragments_searched** Tüm bayt havuzlarındaki ayırma istekleri sırasında aranan iç bellek parçacıklarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-509">**fragments_searched** Pointer to destination for the total number of internal memory fragments searched during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="9fec9-510">**birleştirmeler** Tüm bayt havuzlarındaki ayırma istekleri sırasında birleştirilmiş iç bellek bloklarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-510">**merges** Pointer to destination for the total number of internal memory blocks merged during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="9fec9-511">**böler** Tüm bayt havuzlarındaki ayırma istekleri sırasında oluşturulan toplam iç bellek bloğu sayısı (parça) için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-511">**splits** Pointer to destination for the total number of internal memory blocks split (fragments) created during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="9fec9-512">**getirilmesi** Tüm bayt havuzlarındaki iş parçacığı ayırma getirilmesi toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-512">**suspensions** Pointer to destination for the total number of thread allocation suspensions on all byte pools.</span></span>
- <span data-ttu-id="9fec9-513">**zaman aşımları** Tüm bayt havuzlarında askıya alınma zaman aşımlarının toplam sayısını ayırmak için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-513">**timeouts** Pointer to destination for the total number of allocate suspension timeouts on all byte pools.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-514">*Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-514">*Supplying a TX_NULL for any parameter indicates the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-515">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-515">Return Values</span></span>

- <span data-ttu-id="9fec9-516">**TX_SUCCESS** (0x00) başarılı bayt havuzu performans Get.</span><span class="sxs-lookup"><span data-stu-id="9fec9-516">**TX_SUCCESS** (0x00) Successful byte pool performance get.</span></span>
- <span data-ttu-id="9fec9-517">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-517">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-518">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-518">Allowed From</span></span>

 <span data-ttu-id="9fec9-519">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-519">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-520">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-520">Example</span></span>

```c
ULONG fragments_searched;
ULONG merges;
ULONG splits;
ULONG allocates;
ULONG releases;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on all byte pools in the
system. */
status =
tx_byte_pool_performance_system_info_get(&fragments_searched,
  &merges, &splits, &allocates, &releases,
  &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-521">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-521">See Also</span></span>

- <span data-ttu-id="9fec9-522">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-522">tx_byte_allocate</span></span>
- <span data-ttu-id="9fec9-523">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-523">tx_byte_pool_create</span></span>
- <span data-ttu-id="9fec9-524">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-524">tx_byte_pool_delete</span></span>
- <span data-ttu-id="9fec9-525">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-525">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="9fec9-526">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-526">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-527">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-527">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="9fec9-528">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-528">tx_byte_release</span></span>

## <a name="tx_byte_pool_prioritize"></a><span data-ttu-id="9fec9-529">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-529">tx_byte_pool_prioritize</span></span>

<span data-ttu-id="9fec9-530">Bayt havuzunun askıya alınma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="9fec9-530">Prioritize byte pool suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-531">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-531">Prototype</span></span>

```c
UINT tx_byte_pool_prioritize(TX_BYTE_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="9fec9-532">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-532">Description</span></span>

<span data-ttu-id="9fec9-533">Bu hizmet, bu havuzdaki bellek için askıya alınan en yüksek öncelikli iş parçacığını askıya alma listesinin önüne koyar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-533">This service places the highest priority thread suspended for memory on this pool at the front of the suspension list.</span></span> <span data-ttu-id="9fec9-534">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-534">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-535">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-535">Parameters</span></span>

- <span data-ttu-id="9fec9-536">**pool_ptr** Bellek havuzu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-536">**pool_ptr** Pointer to a memory pool control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-537">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-537">Return Values</span></span>

- <span data-ttu-id="9fec9-538">**TX_SUCCESS** (0x00) başarılı bellek havuzu önceliği belirleme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-538">**TX_SUCCESS** (0x00) Successful memory pool prioritize.</span></span>
- <span data-ttu-id="9fec9-539">**TX_POOL_ERROR** (0x02) geçersiz bellek havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-539">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-540">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-540">Allowed From</span></span>

<span data-ttu-id="9fec9-541">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-541">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-542">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-542">Preemption Possible</span></span>

<span data-ttu-id="9fec9-543">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-543">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-544">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-544">Example</span></span>

```c
TX_BYTE_POOL my_pool;
UINT status;

/* Ensure that the highest priority thread will receive
the next free memory from this pool. */
status = tx_byte_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_byte_release call will wake up this thread,
if there is enough memory to satisfy its request. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-545">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-545">See Also</span></span>

- <span data-ttu-id="9fec9-546">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-546">tx_byte_allocate</span></span>
- <span data-ttu-id="9fec9-547">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-547">tx_byte_pool_create</span></span>
- <span data-ttu-id="9fec9-548">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-548">tx_byte_pool_delete</span></span>
- <span data-ttu-id="9fec9-549">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-549">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="9fec9-550">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-550">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-551">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-551">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-552">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-552">tx_byte_release</span></span>

## <a name="tx_byte_release"></a><span data-ttu-id="9fec9-553">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="9fec9-553">tx_byte_release</span></span>

<span data-ttu-id="9fec9-554">Baytları bellek havuzuna geri bırakma</span><span class="sxs-lookup"><span data-stu-id="9fec9-554">Release bytes back to memory pool</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-555">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-555">Prototype</span></span>

```c
UINT tx_byte_release(VOID *memory_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-556">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-556">Description</span></span>

<span data-ttu-id="9fec9-557">Bu hizmet önceden ayrılmış bir bellek alanını ilişkili havuzuna geri yayınlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-557">This service releases a previously allocated memory area back to its associated pool.</span></span> <span data-ttu-id="9fec9-558">Bu havuzdan bellek beklemeyi askıya alınmış bir veya daha fazla iş parçacığı varsa, askıya alınan her iş parçacığına bellek verilir ve bellek tükenene veya daha fazla askıya alınmış iş parçacığı kalmayana kadar devam sürdürülür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-558">If there are one or more threads suspended waiting for memory from this pool, each suspended thread is given memory and resumed until the memory is exhausted or until there are no more suspended threads.</span></span> <span data-ttu-id="9fec9-559">Askıya alınan iş parçacıkları için bellek ayırma işlemi, her zaman askıya alınan ilk iş parçacığı ile başlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-559">This process of allocating memory to suspended threads always begins with the first thread suspended.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-560">*Uygulamanın, serbest bırakıldıktan sonra bellek alanını kullanmasını önleyecek olması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-560">*The application must prevent using the memory area after it is released.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-561">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-561">Parameters</span></span>

- <span data-ttu-id="9fec9-562">**memory_ptr** Önceden ayrılmış bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-562">**memory_ptr** Pointer to the previously allocated memory area.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-563">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-563">Return Values</span></span>

- <span data-ttu-id="9fec9-564">**TX_SUCCESS** (0x00) başarılı bellek sürümü.</span><span class="sxs-lookup"><span data-stu-id="9fec9-564">**TX_SUCCESS** (0x00) Successful memory release.</span></span>
- <span data-ttu-id="9fec9-565">**TX_PTR_ERROR** (0x03) geçersiz bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-565">**TX_PTR_ERROR** (0x03) Invalid memory area pointer.</span></span>
- <span data-ttu-id="9fec9-566">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-566">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-567">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-567">Allowed From</span></span>

<span data-ttu-id="9fec9-568">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-568">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-569">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-569">Preemption Possible</span></span>

<span data-ttu-id="9fec9-570">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-570">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-571">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-571">Example</span></span>

```c
unsigned char *memory_ptr;
UINT status;

/* Release a memory back to my_pool. Assume that the memory
area was previously allocated from my_pool. */
status = tx_byte_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the memory pointed to by
memory_ptr has been returned to the pool. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-572">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-572">See Also</span></span>

- <span data-ttu-id="9fec9-573">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="9fec9-573">tx_byte_allocate</span></span>
- <span data-ttu-id="9fec9-574">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-574">tx_byte_pool_create</span></span>
- <span data-ttu-id="9fec9-575">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-575">tx_byte_pool_delete</span></span>
- <span data-ttu-id="9fec9-576">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-576">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="9fec9-577">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-577">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="9fec9-578">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-578">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-579">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-579">tx_byte_pool_prioritize</span></span>

## <a name="tx_event_flags_create"></a><span data-ttu-id="9fec9-580">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-580">tx_event_flags_create</span></span>

<span data-ttu-id="9fec9-581">Olay bayrakları grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="9fec9-581">Create event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-582">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-582">Prototype</span></span>

```c
UINT tx_event_flags_create(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    CHAR *name_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-583">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-583">Description</span></span>

<span data-ttu-id="9fec9-584">Bu hizmet bir 32 olay bayrağı grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-584">This service creates a group of 32 event flags.</span></span> <span data-ttu-id="9fec9-585">Gruptaki tüm 32 olay bayrakları sıfır olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-585">All 32 event flags in the group are initialized to zero.</span></span> <span data-ttu-id="9fec9-586">Her olay bayrağı tek bir bit ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-586">Each event flag is represented by a single bit.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-587">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-587">Parameters</span></span>

- <span data-ttu-id="9fec9-588">**group_ptr** Olay bayrakları Grup denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-588">**group_ptr** Pointer to an event flags group control block.</span></span>
- <span data-ttu-id="9fec9-589">**name_ptr** Olay bayrakları grubunun adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-589">**name_ptr** Pointer to the name of the event flags group.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-590">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-590">Return Values</span></span>

- <span data-ttu-id="9fec9-591">**TX_SUCCESS** (0x00) başarılı olay grubu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-591">**TX_SUCCESS** (0x00) Successful event group creation.</span></span>
- <span data-ttu-id="9fec9-592">**TX_GROUP_ERROR** (0x06) geçersiz olay grubu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-592">**TX_GROUP_ERROR** (0x06) Invalid event group pointer.</span></span> <span data-ttu-id="9fec9-593">İşaretçi **null** ya da olay grubu zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9fec9-593">Either the pointer is **NULL** or the event group is already created.</span></span>
- <span data-ttu-id="9fec9-594">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-594">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-595">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-595">Allowed From</span></span>

<span data-ttu-id="9fec9-596">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-596">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-597">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-597">Preemption Possible</span></span>

<span data-ttu-id="9fec9-598">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-598">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-599">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-599">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_group;
UINT status;

/* Create an event flags group. */
status = tx_event_flags_create(&my_event_group,
  "my_event_group_name");

/* If status equals TX_SUCCESS, my_event_group is ready
for get and set services. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-600">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-600">See Also</span></span>

- <span data-ttu-id="9fec9-601">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-601">tx_event_flags_delete</span></span>
- <span data-ttu-id="9fec9-602">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-602">tx_event_flags_get</span></span>
- <span data-ttu-id="9fec9-603">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-603">tx_event_flags_info_get</span></span>
- <span data-ttu-id="9fec9-604">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-604">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="9fec9-605">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-605">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-606">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-606">tx_event_flags_set</span></span>
- <span data-ttu-id="9fec9-607">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-607">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_delete"></a><span data-ttu-id="9fec9-608">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-608">tx_event_flags_delete</span></span>

<span data-ttu-id="9fec9-609">Olay bayrakları grubunu sil</span><span class="sxs-lookup"><span data-stu-id="9fec9-609">Delete event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-610">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-610">Prototype</span></span>

```c
UINT tx_event_flags_delete(TX_EVENT_FLAGS_GROUP *group_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-611">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-611">Description</span></span>

<span data-ttu-id="9fec9-612">Bu hizmet, belirtilen olay bayrakları grubunu siler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-612">This service deletes the specified event flags group.</span></span> <span data-ttu-id="9fec9-613">Bu gruptan gelen olayların beklediği tüm iş parçacıkları sürdürülür ve TX_DELETED bir dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-613">All threads suspended waiting for events from this group are resumed and given a TX_DELETED return status.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="9fec9-614">*Uygulama, olay bayrakları grubu silinmeden önce bu olay bayrakları grubu için bir küme bildirme geri çağrısının tamamlandığını (veya devre dışı) içerdiğinden emin olmalıdır. Ayrıca, uygulamanın, silinen bir olay bayrakları grubunun gelecekteki tüm kullanımını önlemesi gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-614">*The application must ensure that a set notify callback for this event flags group is completed (or disabled) before deleting the event flags group. In addition, the application must prevent all future use of a deleted event flags group.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-615">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-615">Parameters</span></span>

- <span data-ttu-id="9fec9-616">**group_ptr** Daha önce oluşturulmuş bir olay bayrakları grubuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-616">**group_ptr** Pointer to a previously created event flags group.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-617">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-617">Return Values</span></span>

- <span data-ttu-id="9fec9-618">**TX_SUCCESS** (0x00) başarılı olay bayrakları grubu silme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-618">**TX_SUCCESS** (0x00) Successful event flags group deletion.</span></span>
- <span data-ttu-id="9fec9-619">**TX_GROUP_ERROR** (0x06) geçersiz olay bayrakları grup işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-619">**TX_GROUP_ERROR** (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="9fec9-620">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-620">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-621">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-621">Allowed From</span></span>

<span data-ttu-id="9fec9-622">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-622">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-623">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-623">Preemption Possible</span></span>

<span data-ttu-id="9fec9-624">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-624">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-625">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-625">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_flags_group;
UINT status;

/* Delete event flags group. Assume that the group has
already been created with a call to
tx_event_flags_create. */
status = tx_event_flags_delete(&my_event_flags_group);

/* If status equals TX_SUCCESS, the event flags group is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-626">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-626">See Also</span></span>

- <span data-ttu-id="9fec9-627">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-627">tx_event_flags_create</span></span>
- <span data-ttu-id="9fec9-628">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-628">tx_event_flags_get</span></span>
- <span data-ttu-id="9fec9-629">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-629">tx_event_flags_info_get</span></span>
- <span data-ttu-id="9fec9-630">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-630">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="9fec9-631">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-631">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-632">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-632">tx_event_flags_set</span></span>
- <span data-ttu-id="9fec9-633">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-633">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_get"></a><span data-ttu-id="9fec9-634">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-634">tx_event_flags_get</span></span>

<span data-ttu-id="9fec9-635">Olay bayrakları grubundan olay bayraklarını al</span><span class="sxs-lookup"><span data-stu-id="9fec9-635">Get event flags from event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-636">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-636">Prototype</span></span>

```c
UINT tx_event_flags_get(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    ULONG requested_flags, 
    UINT get_option,
    ULONG *actual_flags_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="9fec9-637">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-637">Description</span></span>

<span data-ttu-id="9fec9-638">Bu hizmet, belirtilen olay bayrakları grubundan olay bayraklarını alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-638">This service retrieves event flags from the specified event flags group.</span></span> <span data-ttu-id="9fec9-639">Her olay bayrakları grubu 32 olay bayrağını içerir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-639">Each event flags group contains 32 event flags.</span></span> <span data-ttu-id="9fec9-640">Her bayrak tek bir bit ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-640">Each flag is represented by a single bit.</span></span> <span data-ttu-id="9fec9-641">Bu hizmet, giriş parametreleri tarafından seçilen çeşitli olay bayrağı kombinasyonlarını alabilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-641">This service can retrieve a variety of event flag combinations, as selected by the input parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-642">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-642">Parameters</span></span>

- <span data-ttu-id="9fec9-643">**group_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-643">**group_ptr**</span></span> <br><span data-ttu-id="9fec9-644">Daha önce oluşturulmuş bir olay bayrakları grubuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-644">Pointer to a previously created event flags group.</span></span>
- <span data-ttu-id="9fec9-645">**requested_flags**</span><span class="sxs-lookup"><span data-stu-id="9fec9-645">**requested_flags**</span></span> <br><span data-ttu-id="9fec9-646">İstenen olay bayraklarını temsil eden 32 bitlik işaretsiz değişken.</span><span class="sxs-lookup"><span data-stu-id="9fec9-646">32-bit unsigned variable that represents the requested event flags.</span></span>
- <span data-ttu-id="9fec9-647">**get_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-647">**get_option**</span></span> <br><span data-ttu-id="9fec9-648">İstenen olay bayraklarının tümünün veya herhangi birinin gerekli olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-648">Specifies whether all or any of the requested event flags are required.</span></span> <span data-ttu-id="9fec9-649">Aşağıdakiler geçerli seçimlerdir:</span><span class="sxs-lookup"><span data-stu-id="9fec9-649">The following are valid selections:</span></span>

  - <span data-ttu-id="9fec9-650">**TX_AND** (0x02)</span><span class="sxs-lookup"><span data-stu-id="9fec9-650">**TX_AND** (0x02)</span></span>
  - <span data-ttu-id="9fec9-651">**TX_AND_CLEAR** (0x03)</span><span class="sxs-lookup"><span data-stu-id="9fec9-651">**TX_AND_CLEAR** (0x03)</span></span>
  - <span data-ttu-id="9fec9-652">**TX_OR** (0x00)</span><span class="sxs-lookup"><span data-stu-id="9fec9-652">**TX_OR** (0x00)</span></span>
  - <span data-ttu-id="9fec9-653">**TX_OR_CLEAR** (0x01)</span><span class="sxs-lookup"><span data-stu-id="9fec9-653">**TX_OR_CLEAR** (0x01)</span></span>

    <span data-ttu-id="9fec9-654">TX_AND veya TX_AND_CLEAR seçilmesi, tüm olay bayraklarının grupta mevcut olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-654">Selecting TX_AND or TX_AND_CLEAR specifies that all event flags must be present in the group.</span></span> <span data-ttu-id="9fec9-655">TX_OR veya TX_OR_CLEAR seçilmesi herhangi bir olay bayrağının tatmin edici olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-655">Selecting TX_OR or TX_OR_CLEAR     specifies that any event flag is satisfactory.</span></span> <span data-ttu-id="9fec9-656">TX_AND_CLEAR veya TX_OR_CLEAR belirtilirse, isteği karşılayan olay bayrakları temizlenir (sıfır olarak ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="9fec9-656">Event flags that satisfy the request are cleared (set to zero) if TX_AND_CLEAR or TX_OR_CLEAR are specified.</span></span>

- <span data-ttu-id="9fec9-657">**actual_flags_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-657">**actual_flags_ptr**</span></span> <br><span data-ttu-id="9fec9-658">Alınan olay bayraklarının yerleştirildiği hedefin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-658">Pointer to destination of where the retrieved event flags are placed.</span></span> <span data-ttu-id="9fec9-659">Alınan gerçek bayrakların istenmedi bayrakları içerebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9fec9-659">Note that the actual flags obtained may contain flags that were not requested.</span></span>
- <span data-ttu-id="9fec9-660">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-660">**wait_option**</span></span>  <br><span data-ttu-id="9fec9-661">Seçilen olay bayrakları ayarlanmamışsa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-661">Defines how the service behaves if the selected event flags are not set.</span></span> <span data-ttu-id="9fec9-662">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="9fec9-662">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9fec9-663">**TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-663">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="9fec9-664">Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.</span><span class="sxs-lookup"><span data-stu-id="9fec9-664">This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.</span></span>
  - <span data-ttu-id="9fec9-665">**TX_WAIT_FOREVER** zaman aşımı değeri (0xffffffff)-TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının olay bayrakları kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-665">**TX_WAIT_FOREVER** timeout value  (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the event flags are available.</span></span>
  - <span data-ttu-id="9fec9-666">zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, olay bayrakları beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-666">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the event flags.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-667">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-667">Return Values</span></span>

- <span data-ttu-id="9fec9-668">**TX_SUCCESS** (0x00) başarılı olay bayrakları al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-668">**TX_SUCCESS** (0x00) Successful event flags get.</span></span>
- <span data-ttu-id="9fec9-669">İş parçacığı askıya alınırken **TX_DELETED** (0x01) olay bayrakları grubu silindi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-669">**TX_DELETED** (0x01) Event flags group was deleted while thread was suspended.</span></span>
- <span data-ttu-id="9fec9-670">**TX_NO_EVENTS** (0x07) hizmeti, belirtilen olayları beklemek için belirtilen süre içinde alamadı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-670">**TX_NO_EVENTS** (0x07) Service was unable to get the specified events within the specified time to wait.</span></span>
- <span data-ttu-id="9fec9-671">**TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-671">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="9fec9-672">**TX_GROUP_ERROR** (0x06) geçersiz olay bayrakları grup işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-672">**TX_GROUP_ERROR** (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="9fec9-673">**TX_PTR_ERROR** (0x03) gerçek olay bayrakları için geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-673">**TX_PTR_ERROR** (0x03) Invalid pointer for actual event flags.</span></span>
- <span data-ttu-id="9fec9-674">**TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-674">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="9fec9-675">**TX_OPTION_ERROR** (0x08) geçersiz Get-OPTION belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-675">**TX_OPTION_ERROR** (0x08) Invalid get-option was specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-676">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-676">Allowed From</span></span>

<span data-ttu-id="9fec9-677">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-677">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-678">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-678">Preemption Possible</span></span>

<span data-ttu-id="9fec9-679">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-679">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-680">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-680">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_flags_group;
ULONG actual_events;
UINT status;

/* Request that event flags 0, 4, and 8 are all set. Also,
if they are set they should be cleared. If the event
flags are not set, this service suspends for a maximum of
20 timer-ticks. */
status = tx_event_flags_get(&my_event_flags_group, 0x111,
    TX_AND_CLEAR, &actual_events, 20);

/* If status equals TX_SUCCESS, actual_events contains the
actual events obtained. */
```

<span data-ttu-id="9fec9-681">**Ayrıca bkz.**</span><span class="sxs-lookup"><span data-stu-id="9fec9-681">**See Also**</span></span>

- <span data-ttu-id="9fec9-682">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-682">tx_event_flags_create</span></span>
- <span data-ttu-id="9fec9-683">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-683">tx_event_flags_delete</span></span>
- <span data-ttu-id="9fec9-684">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-684">tx_event_flags_info_get</span></span>
- <span data-ttu-id="9fec9-685">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-685">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="9fec9-686">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-686">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-687">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-687">tx_event_flags_set</span></span>
- <span data-ttu-id="9fec9-688">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-688">tx_event_flags_set_notify</span></span>

### <a name="tx_event_flags_info_get"></a><span data-ttu-id="9fec9-689">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-689">tx_event_flags_info_get</span></span>

<span data-ttu-id="9fec9-690">Olay bayrakları grubu hakkında bilgi al</span><span class="sxs-lookup"><span data-stu-id="9fec9-690">Retrieve information about event flags group</span></span>

<span data-ttu-id="9fec9-691">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="9fec9-691">**Prototype**</span></span>

```c
UINT tx_event_flags_info_get(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    CHAR **name, ULONG *current_flags,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_EVENT_FLAGS_GROUP **next_group);
```

<span data-ttu-id="9fec9-692">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="9fec9-692">**Description**</span></span>

<span data-ttu-id="9fec9-693">Bu hizmet, belirtilen olay bayrakları grubu hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-693">This service retrieves information about the specified event flags group.</span></span>

<span data-ttu-id="9fec9-694">**Parametreler**</span><span class="sxs-lookup"><span data-stu-id="9fec9-694">**Parameters**</span></span>

- <span data-ttu-id="9fec9-695">**group_ptr** Olay bayrakları Grup denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-695">**group_ptr** Pointer to an event flags group control block.</span></span>
- <span data-ttu-id="9fec9-696">**ad** Olay bayrakları grubunun adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-696">**name** Pointer to destination for the pointer to the event flags group's name.</span></span>
- <span data-ttu-id="9fec9-697">**current_flags** Olay bayrakları grubundaki geçerli küme bayrakları için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-697">**current_flags** Pointer to destination for the current set flags in the event flags group.</span></span>
- <span data-ttu-id="9fec9-698">**first_suspended** Bu olay bayrakları grubunun askıya alma listesindeki ilk iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-698">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this event flags group.</span></span>
- <span data-ttu-id="9fec9-699">**suspended_count** Bu olay bayrakları grubunda askıya alınmış olan iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-699">**suspended_count** Pointer to destination for the number of threads currently suspended on this event flags group.</span></span>
- <span data-ttu-id="9fec9-700">**next_group** Sonraki oluşturulan olay bayrakları grubunun işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-700">**next_group** Pointer to destination for the pointer of the next created event flags group.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-701">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-701">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-702">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-702">Return Values</span></span>

- <span data-ttu-id="9fec9-703">**TX_SUCCESS** (0x00) başarılı olay grubu bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-703">**TX_SUCCESS** (0x00) Successful event group information retrieval.</span></span>
- <span data-ttu-id="9fec9-704">**TX_GROUP_ERROR** (0x06) geçersiz olay grubu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-704">**TX_GROUP_ERROR** (0x06) Invalid event group pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-705">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-705">Allowed From</span></span>

<span data-ttu-id="9fec9-706">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-706">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-707">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-707">Preemption Possible</span></span>

<span data-ttu-id="9fec9-708">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-708">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-709">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-709">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_group;
CHAR *name;
ULONG current_flags;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_EVENT_FLAGS_GROUP *next_group;
UINT status;

/* Retrieve information about the previously created
event flags group "my_event_group." */
status = tx_event_flags_info_get(&my_event_group, &name,
    &current_flags,
    &first_suspended, &suspended_count,
    &next_group);
/* If status equals TX_SUCCESS, the information requested is
valid. */
```
<span data-ttu-id="9fec9-710">**Ayrıca bkz.**</span><span class="sxs-lookup"><span data-stu-id="9fec9-710">**See Also**</span></span>

- <span data-ttu-id="9fec9-711">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-711">tx_event_flags_create</span></span>
- <span data-ttu-id="9fec9-712">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-712">tx_event_flags_delete</span></span>
- <span data-ttu-id="9fec9-713">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-713">tx_event_flags_get</span></span>
- <span data-ttu-id="9fec9-714">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-714">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="9fec9-715">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-715">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-716">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-716">tx_event_flags_set</span></span>
- <span data-ttu-id="9fec9-717">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-717">tx_event_flags_set_notify</span></span>

### <a name="tx_event_flags_performance_info_get"></a><span data-ttu-id="9fec9-718">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-718">tx_event_flags_performance_info_get</span></span>

<span data-ttu-id="9fec9-719">Olay bayrakları grubu performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-719">Get event flags group performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-720">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-720">Prototype</span></span>

```c
UINT tx_event_flags_performance_info_get(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    ULONG *sets, ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="9fec9-721">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-721">Description</span></span>

<span data-ttu-id="9fec9-722">Bu hizmet, belirtilen olay bayrakları grubuyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-722">This service retrieves performance information about the specified event flags group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-723">*Threadx kitaplığı ve uygulaması* , *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-723">*ThreadX library and application must be built with* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-724">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-724">Parameters</span></span>

- <span data-ttu-id="9fec9-725">**group_ptr** Daha önce oluşturulan olay bayrakları grubuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-725">**group_ptr** Pointer to previously created event flags group.</span></span>
- <span data-ttu-id="9fec9-726">**Ayarlar** Bu grupta gerçekleştirilen olay bayrak kümesi isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-726">**sets** Pointer to destination for the number of event flags set requests performed on this group.</span></span>
- <span data-ttu-id="9fec9-727">**alır** Bu grupta gerçekleştirilen olay bayrakları Al istekleri için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-727">**gets** Pointer to destination for the number of event flags get requests performed on this group.</span></span>
- <span data-ttu-id="9fec9-728">**getirilmesi** Bu gruptaki iş parçacığı olay bayraklarının sayısı için hedef işaretçisi getirilmesi al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-728">**suspensions** Pointer to destination for the number of thread event flags get suspensions on this group.</span></span>
- <span data-ttu-id="9fec9-729">**zaman aşımları** Olay bayraklarının sayısı için hedefin işaretçisi bu gruptaki askıya alma zaman aşımlarını al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-729">**timeouts** Pointer to destination for the number of event flags get suspension timeouts on this group.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-730">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-730">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-731">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-731">Return Values</span></span>

- <span data-ttu-id="9fec9-732">**TX_SUCCESS** (0x00) başarılı olay bayrakları grup performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-732">**TX_SUCCESS** (0x00) Successful event flags group performance get.</span></span>
- <span data-ttu-id="9fec9-733">**TX_PTR_ERROR** (0x03) geçersiz olay bayrakları grup işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-733">**TX_PTR_ERROR** (0x03) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="9fec9-734">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-734">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-735">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-735">Allowed From</span></span>

<span data-ttu-id="9fec9-736">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-736">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-737">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-737">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_flag_group;
ULONG sets;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created event
flag group. */
status = tx_event_flags_performance_info_get(&my_event_flag_group,
    &sets, &gets, &suspensions,
    &timeouts);

/* If status is TX_SUCCESS the performance information was successfully
retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-738">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-738">See Also</span></span>

- <span data-ttu-id="9fec9-739">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-739">tx_event_flags_create</span></span>
- <span data-ttu-id="9fec9-740">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-740">tx_event_flags_delete</span></span>
- <span data-ttu-id="9fec9-741">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-741">tx_event_flags_get</span></span>
- <span data-ttu-id="9fec9-742">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-742">tx_event_flags_info_get</span></span>
- <span data-ttu-id="9fec9-743">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-743">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-744">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-744">tx_event_flags_set</span></span>
- <span data-ttu-id="9fec9-745">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-745">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_performance_system_info_get"></a><span data-ttu-id="9fec9-746">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-746">tx_event_flags_performance_system_info_get</span></span>

<span data-ttu-id="9fec9-747">Performans sistemi bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-747">Retrieve performance system information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-748">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-748">Prototype</span></span>

```c
UINT tx_event_flags_performance_system_info_get(
    ULONG *sets,
    ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="9fec9-749">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-749">Description</span></span>

<span data-ttu-id="9fec9-750">Bu hizmet sistemdeki tüm olay bayrakları gruplarıyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-750">This service retrieves performance information about all event flags groups in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-751">*Threadx kitaplığı ve uygulaması* , *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-751">*ThreadX library and application must be built with* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-752">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-752">Parameters</span></span>

- <span data-ttu-id="9fec9-753">**Ayarlar** Tüm gruplarda gerçekleştirilen olay bayrakları kümesi isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-753">**sets** Pointer to destination for the total number of event flags set requests performed on all groups.</span></span>
- <span data-ttu-id="9fec9-754">**alır** Tüm gruplarda gerçekleştirilen olay bayraklarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-754">**gets** Pointer to destination for the total number of event flags get requests performed on all groups.</span></span>
- <span data-ttu-id="9fec9-755">**getirilmesi** İş parçacığı olay bayraklarının toplam sayısı için hedef işaretçisi tüm gruplar üzerinde getirilmesi alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-755">**suspensions** Pointer to destination for the total number of thread event flags get suspensions on all groups.</span></span>
- <span data-ttu-id="9fec9-756">**zaman aşımları** Toplam olay bayrakları sayısı için hedefin işaretçisi tüm gruplardaki askıya alınma zaman aşımlarını alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-756">**timeouts** Pointer to destination for the total number of event flags get suspension timeouts on all groups.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-757">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-757">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-758">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-758">Return Values</span></span>

- <span data-ttu-id="9fec9-759">**TX_SUCCESS** (0x00) başarılı olay bayrakları sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-759">**TX_SUCCESS** (0x00) Successful event flags system performance get.</span></span>
- <span data-ttu-id="9fec9-760">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-760">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-761">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-761">Example</span></span>

```c
ULONG sets;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on all previously created event
flag groups. */
status = tx_event_flags_performance_system_info_get(&sets, &gets,
    &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-762">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-762">See Also</span></span>

- <span data-ttu-id="9fec9-763">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-763">tx_event_flags_create</span></span>
- <span data-ttu-id="9fec9-764">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-764">tx_event_flags_delete</span></span>
- <span data-ttu-id="9fec9-765">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-765">tx_event_flags_get</span></span>
- <span data-ttu-id="9fec9-766">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-766">tx_event_flags_info_get</span></span>
- <span data-ttu-id="9fec9-767">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-767">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="9fec9-768">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-768">tx_event_flags_set</span></span>
- <span data-ttu-id="9fec9-769">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-769">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_set"></a><span data-ttu-id="9fec9-770">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-770">tx_event_flags_set</span></span>

<span data-ttu-id="9fec9-771">Olay bayrakları grubundaki olay bayraklarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="9fec9-771">Set event flags in an event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-772">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-772">Prototype</span></span>

```c
UINT tx_event_flags_set(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    ULONG flags_to_set,
    UINT set_option);
```

### <a name="description"></a><span data-ttu-id="9fec9-773">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-773">Description</span></span>

<span data-ttu-id="9fec9-774">Bu hizmet, belirtilen set-Option öğesine bağlı olarak bir olay bayrakları grubundaki olay bayraklarını ayarlar veya temizler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-774">This service sets or clears event flags in an event flags group, depending upon the specified set-option.</span></span> <span data-ttu-id="9fec9-775">Olay bayrakları isteği artık karşılanan tüm askıya alınmış iş parçacıkları devam ettirildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-775">All suspended threads whose event flags request is now satisfied are resumed.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-776">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-776">Parameters</span></span>

- <span data-ttu-id="9fec9-777">**group_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-777">**group_ptr**</span></span> <br><span data-ttu-id="9fec9-778">Önceden oluşturulan olay bayrakları Grup denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-778">Pointer to the previously created event flags group control block.</span></span>
- <span data-ttu-id="9fec9-779">**flags_to_set**</span><span class="sxs-lookup"><span data-stu-id="9fec9-779">**flags_to_set**</span></span> <br><span data-ttu-id="9fec9-780">Belirlenen küme seçeneğinin üzerine ayarlanacak veya temizlenecek olay bayraklarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-780">Specifies the event flags to set or clear based upon the set option selected.</span></span>
- <span data-ttu-id="9fec9-781">**set_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-781">**set_option**</span></span> <br><span data-ttu-id="9fec9-782">Belirtilen olay bayraklarının, grubun geçerli olay bayraklarına mi yoksa ORed mi olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-782">Specifies whether the event flags specified are ANDed or ORed into the current event flags of the group.</span></span> <span data-ttu-id="9fec9-783">Aşağıdakiler geçerli seçimlerdir:</span><span class="sxs-lookup"><span data-stu-id="9fec9-783">The following are valid selections:</span></span>
  - <span data-ttu-id="9fec9-784">**TX_AND** (0x02)</span><span class="sxs-lookup"><span data-stu-id="9fec9-784">**TX_AND** (0x02)</span></span>
  - <span data-ttu-id="9fec9-785">**TX_OR** (0x00)</span><span class="sxs-lookup"><span data-stu-id="9fec9-785">**TX_OR** (0x00)</span></span>

  <span data-ttu-id="9fec9-786">TX_AND seçilirse, belirtilen olay bayraklarının gruptaki geçerli olay bayraklarına ait olduğunu **ve** bulunduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-786">Selecting TX_AND specifies that the specified event flags are **AND** ed into the current event flags in the group.</span></span> <span data-ttu-id="9fec9-787">Bu seçenek, genellikle bir gruptaki olay bayraklarını temizlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-787">This option is often used to clear event flags in a group.</span></span> <span data-ttu-id="9fec9-788">Aksi takdirde, TX_OR belirtilirse, belirtilen olay bayrakları gruptaki geçerli olayla **birlikte olur.**</span><span class="sxs-lookup"><span data-stu-id="9fec9-788">Otherwise, if TX_OR is specified, the specified event flags are **OR** ed with the current event in the group.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-789">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-789">Return Values</span></span>
- <span data-ttu-id="9fec9-790">**TX_SUCCESS** (0x00) başarılı olay bayrakları kümesi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-790">**TX_SUCCESS** (0x00) Successful event flags set.</span></span>
- <span data-ttu-id="9fec9-791">**TX_GROUP_ERROR** (0x06) olay bayrakları grubuna yönelik geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-791">**TX_GROUP_ERROR** (0x06) Invalid pointer to event flags group.</span></span>
- <span data-ttu-id="9fec9-792">**TX_OPTION_ERROR** (0x08) geçersiz set-OPTION belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-792">**TX_OPTION_ERROR** (0x08) Invalid set-option specified.</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-793">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-793">Preemption Possible</span></span>

<span data-ttu-id="9fec9-794">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-794">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-795">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-795">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_flags_group;
UINT status;

/* Set event flags 0, 4, and 8. */
status = tx_event_flags_set(&my_event_flags_group,
    0x111, TX_OR);

/* If status equals TX_SUCCESS, the event flags have been
set and any suspended thread whose request was satisfied
has been resumed. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-796">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-796">See Also</span></span>

- <span data-ttu-id="9fec9-797">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-797">tx_event_flags_create</span></span>
- <span data-ttu-id="9fec9-798">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-798">tx_event_flags_delete</span></span>
- <span data-ttu-id="9fec9-799">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-799">tx_event_flags_get</span></span>
- <span data-ttu-id="9fec9-800">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-800">tx_event_flags_info_get</span></span>
- <span data-ttu-id="9fec9-801">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-801">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="9fec9-802">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-802">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-803">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-803">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_set_notify"></a><span data-ttu-id="9fec9-804">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-804">tx_event_flags_set_notify</span></span>

<span data-ttu-id="9fec9-805">Olay bayrakları ayarlandığında uygulamaya bildir</span><span class="sxs-lookup"><span data-stu-id="9fec9-805">Notify application when event flags are set</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-806">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-806">Prototype</span></span>

```c
UINT tx_event_flags_set_notify(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    VOID (*events_set_notify)(TX_EVENT_FLAGS_GROUP *));
```

### <a name="description"></a><span data-ttu-id="9fec9-807">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-807">Description</span></span>

<span data-ttu-id="9fec9-808">Bu hizmet, belirtilen olay bayrakları grubunda bir veya daha fazla olay bayrağı ayarlandığında çağrılan bir bildirim geri arama işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9fec9-808">This service registers a notification callback function that is called whenever one or more event flags are set in the specified event flags group.</span></span> <span data-ttu-id="9fec9-809">Bildirim geri çağrısının işlenmesi,</span><span class="sxs-lookup"><span data-stu-id="9fec9-809">The processing of the notification callback is defined by the</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-810">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-810">Parameters</span></span>
- <span data-ttu-id="9fec9-811">**group_ptr** Daha önce oluşturulan olay bayrakları grubuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-811">**group_ptr** Pointer to previously created event flags group.</span></span>
- <span data-ttu-id="9fec9-812">**events_set_notify** Uygulamanın olay bayrakları kümesi bildirim işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-812">**events_set_notify** Pointer to application's event flags set notification function.</span></span> <span data-ttu-id="9fec9-813">Bu değer TX_NULL, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-813">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-814">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-814">Return Values</span></span>

- <span data-ttu-id="9fec9-815">**TX_SUCCESS** (0x00) olay bayrakları ayarlama bildiriminin başarılı kaydı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-815">**TX_SUCCESS** (0x00) Successful registration of event flags set notification.</span></span>
- <span data-ttu-id="9fec9-816">**TX_GROUP_ERROR** (0x06) geçersiz olay bayrakları grup işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-816">**TX_GROUP_ERROR** (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="9fec9-817">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem bildirim özellikleri devre dışı olarak derlendi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-817">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-818">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-818">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_group;

/* Register the "my_event_flags_set_notify" function for monitoring
event flags set in the event flags group "my_group." */
status = tx_event_flags_set_notify(&my_group, my_event_flags_set_notify);

/* If status is TX_SUCCESS the event flags set notification function
was successfully registered. */
void my_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr)

/* One or more event flags was set in this group! */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-819">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-819">See Also</span></span>

- <span data-ttu-id="9fec9-820">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-820">tx_event_flags_create</span></span>
- <span data-ttu-id="9fec9-821">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-821">tx_event_flags_delete</span></span>
- <span data-ttu-id="9fec9-822">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-822">tx_event_flags_get</span></span>
- <span data-ttu-id="9fec9-823">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-823">tx_event_flags_info_get</span></span>
- <span data-ttu-id="9fec9-824">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-824">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="9fec9-825">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-825">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-826">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-826">tx_event_flags_set</span></span>

## <a name="tx_interrupt_control"></a><span data-ttu-id="9fec9-827">tx_interrupt_control</span><span class="sxs-lookup"><span data-stu-id="9fec9-827">tx_interrupt_control</span></span>

<span data-ttu-id="9fec9-828">Kesmeleri etkinleştirme ve devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="9fec9-828">Enable and disable interrupts</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-829">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-829">Prototype</span></span>

```c
UINT tx_interrupt_control(UINT new_posture);
```

### <a name="description"></a><span data-ttu-id="9fec9-830">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-830">Description</span></span>

<span data-ttu-id="9fec9-831">Bu hizmet, *new_posture* giriş parametresi tarafından belirtilen kesintileri etkinleştirilir veya devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-831">This service enables or disables interrupts as specified by the input parameter *new_posture*.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-832">*Bu hizmet bir uygulama iş parçacığından çağrılırsa, kesme sonrası bu iş parçacığı bağlamının bir parçası olarak kalır. Örneğin, iş parçacığı kesintileri devre dışı bırakmak ve sonra askıya almak için bu yordamı çağırırsa, kesintiler yeniden devre dışı bırakılır.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-832">*If this service is called from an application thread, the interrupt posture remains part of that thread's context. For example, if the thread calls this routine to disable interrupts and then suspends, when it is resumed, interrupts are disabled again.*</span></span>

> [!WARNING]
> <span data-ttu-id="9fec9-833">*Bu hizmet, başlatma sırasında kesmeleri etkinleştirmek için kullanılmamalıdır! Bunun yapılması öngörülemeyen sonuçlara neden olabilir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-833">*This service should not be used to enable interrupts during initialization! Doing so could cause unpredictable results.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-834">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-834">Parameters</span></span>

- <span data-ttu-id="9fec9-835">**new_posture** Bu parametre, kesmelerin devre dışı veya etkin olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-835">**new_posture** This parameter specifies whether interrupts are disabled or enabled.</span></span> <span data-ttu-id="9fec9-836">Yasal değerler **TX_INT_DISABLE** ve **TX_INT_ENABLE** içerir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-836">Legal values include **TX_INT_DISABLE** and **TX_INT_ENABLE**.</span></span> <span data-ttu-id="9fec9-837">Bu parametrelerin gerçek değerleri bağlantı noktasına özeldir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-837">The actual values for these parameters are port specific.</span></span> <span data-ttu-id="9fec9-838">Bunlara ek olarak, bazı işleme mimarileri ek kesme devre dışı bırakmayı destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-838">In addition, some processing architectures might support additional interrupt disable postures.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-839">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-839">Return Values</span></span>
- <span data-ttu-id="9fec9-840">**önceki duruşunu** Bu hizmet, çağırana bir önceki kesme sonrası döndürür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-840">**previous posture** This service returns the previous interrupt posture to the caller.</span></span> <span data-ttu-id="9fec9-841">Bu, hizmet kullanıcılarının kesintiler devre dışı bırakıldıktan sonra önceki duruşunu geri yüklemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-841">This allows users of the service to restore the previous posture after interrupts are disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-842">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-842">Allowed From</span></span>

<span data-ttu-id="9fec9-843">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-843">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-844">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-844">Preemption Possible</span></span>

<span data-ttu-id="9fec9-845">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-845">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-846">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-846">Example</span></span>

```c
UINT my_old_posture;

/* Lockout interrupts */
my_old_posture = tx_interrupt_control(TX_INT_DISABLE);

/* Perform critical operations that need interrupts
locked-out.... */

/* Restore previous interrupt lockout posture. */
tx_interrupt_control(my_old_posture);
```

### <a name="see-also"></a><span data-ttu-id="9fec9-847">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-847">See Also</span></span>

<span data-ttu-id="9fec9-848">Yok</span><span class="sxs-lookup"><span data-stu-id="9fec9-848">None</span></span>

## <a name="tx_mutex_create"></a><span data-ttu-id="9fec9-849">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-849">tx_mutex_create</span></span>

<span data-ttu-id="9fec9-850">Karşılıklı dışlama mutex oluştur</span><span class="sxs-lookup"><span data-stu-id="9fec9-850">Create mutual exclusion mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-851">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-851">Prototype</span></span>

```c
UINT tx_mutex_create(
    TX_MUTEX *mutex_ptr,
    CHAR *name_ptr, 
    UINT priority_inherit);
```

### <a name="description"></a><span data-ttu-id="9fec9-852">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-852">Description</span></span>

<span data-ttu-id="9fec9-853">Bu hizmet, kaynak koruması için iş parçacıkları arası karşılıklı dışlama için bir mutex oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-853">This service creates a mutex for inter-thread mutual exclusion for resource protection.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-854">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-854">Parameters</span></span>

- <span data-ttu-id="9fec9-855">**mutex_ptr** Mutex denetim bloğunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-855">**mutex_ptr** Pointer to a mutex control block.</span></span>
- <span data-ttu-id="9fec9-856">**name_ptr** Mutex adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-856">**name_ptr** Pointer to the name of the mutex.</span></span>
- <span data-ttu-id="9fec9-857">**priority_inherit** Bu mutex 'in öncelik devralmayı destekleyip desteklemediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-857">**priority_inherit** Specifies whether or not this mutex supports priority inheritance.</span></span> <span data-ttu-id="9fec9-858">Bu değer TX_INHERIT, öncelikli devralma desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-858">If this value is TX_INHERIT, then priority inheritance is supported.</span></span> <span data-ttu-id="9fec9-859">Ancak TX_NO_INHERIT belirtilirse, bu mutex tarafından öncelik devralımı desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="9fec9-859">However, if TX_NO_INHERIT is specified, priority inheritance is not supported by this mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-860">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-860">Return Values</span></span>

- <span data-ttu-id="9fec9-861">**TX_SUCCESS** (0x00) başarılı mutex oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-861">**TX_SUCCESS** (0x00) Successful mutex creation.</span></span>
- <span data-ttu-id="9fec9-862">**TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-862">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span> <span data-ttu-id="9fec9-863">İşaretçi NULL ya da mutex zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9fec9-863">Either the pointer is NULL or the mutex is already created.</span></span>
- <span data-ttu-id="9fec9-864">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-864">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>
- <span data-ttu-id="9fec9-865">**TX_INHERIT_ERROR** (0x1F) geçersiz öncelik devralma parametresi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-865">**TX_INHERIT_ERROR** (0x1F) Invalid priority inherit parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-866">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-866">Allowed From</span></span>

<span data-ttu-id="9fec9-867">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-867">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-868">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-868">Preemption Possible</span></span>

<span data-ttu-id="9fec9-869">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-869">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-870">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-870">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Create a mutex to provide protection over a
common resource. */
status = tx_mutex_create(&my_mutex,"my_mutex_name",
    TX_NO_INHERIT);

/* If status equals TX_SUCCESS, my_mutex is ready for
use. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-871">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-871">See Also</span></span>

- <span data-ttu-id="9fec9-872">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-872">tx_mutex_delete</span></span>
- <span data-ttu-id="9fec9-873">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-873">tx_mutex_get</span></span>
- <span data-ttu-id="9fec9-874">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-874">tx_mutex_info_get</span></span>
- <span data-ttu-id="9fec9-875">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-875">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="9fec9-876">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-876">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-877">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-877">tx_mutex_prioritize</span></span>
- <span data-ttu-id="9fec9-878">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-878">tx_mutex_put</span></span>

## <a name="tx_mutex_delete"></a><span data-ttu-id="9fec9-879">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-879">tx_mutex_delete</span></span>

<span data-ttu-id="9fec9-880">Karşılıklı dışlama mutex 'i Sil</span><span class="sxs-lookup"><span data-stu-id="9fec9-880">Delete mutual exclusion mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-881">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-881">Prototype</span></span>

```c
UINT tx_mutex_delete(TX_MUTEX *mutex_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-882">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-882">Description</span></span>

<span data-ttu-id="9fec9-883">Bu hizmet, belirtilen mutex 'i siler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-883">This service deletes the specified mutex.</span></span> <span data-ttu-id="9fec9-884">Mutex bekleniyor olan tüm iş parçacıkları sürdürülür ve **TX_DELETED** dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-884">All threads suspended waiting for the mutex are resumed and given a **TX_DELETED** return status.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-885">*Silinen bir mutex 'in kullanımını önleyen uygulamanın sorumluluğundadır.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-885">*It is the application's responsibility to prevent use of a deleted mutex.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-886">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-886">Parameters</span></span>

- <span data-ttu-id="9fec9-887">**mutex_ptr** Daha önce oluşturulmuş bir mutex işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-887">**mutex_ptr** Pointer to a previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-888">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-888">Return Values</span></span>

- <span data-ttu-id="9fec9-889">**TX_SUCCESS** (0x00) başarılı mutex silme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-889">**TX_SUCCESS** (0x00) Successful mutex deletion.</span></span>
- <span data-ttu-id="9fec9-890">**TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-890">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span>
- <span data-ttu-id="9fec9-891">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-891">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-892">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-892">Allowed From</span></span>

<span data-ttu-id="9fec9-893">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-893">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-894">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-894">Preemption Possible</span></span>

<span data-ttu-id="9fec9-895">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-895">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-896">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-896">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Delete a mutex. Assume that the mutex
has already been created. */
status = tx_mutex_delete(&my_mutex);

/* If status equals TX_SUCCESS, the mutex is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-897">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-897">See Also</span></span>

- <span data-ttu-id="9fec9-898">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-898">tx_mutex_create</span></span>
- <span data-ttu-id="9fec9-899">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-899">tx_mutex_get</span></span>
- <span data-ttu-id="9fec9-900">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-900">tx_mutex_info_get</span></span>
- <span data-ttu-id="9fec9-901">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-901">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="9fec9-902">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-902">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-903">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-903">tx_mutex_prioritize</span></span>
- <span data-ttu-id="9fec9-904">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-904">tx_mutex_put</span></span>

## <a name="tx_mutex_get"></a><span data-ttu-id="9fec9-905">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-905">tx_mutex_get</span></span>

<span data-ttu-id="9fec9-906">Mutex sahipliğini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-906">Obtain ownership of mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-907">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-907">Prototype</span></span>

```c
UINT tx_mutex_get(
    TX_MUTEX *mutex_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="9fec9-908">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-908">Description</span></span>

<span data-ttu-id="9fec9-909">Bu hizmet, belirtilen mutex 'in özel sahipliğini almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-909">This service attempts to obtain exclusive ownership of the specified mutex.</span></span> <span data-ttu-id="9fec9-910">Çağıran iş parçacığı zaten mutex 'e sahipse, bir iç sayaç artırılır ve başarılı bir durum döndürülür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-910">If the calling thread already owns the mutex, an internal counter is incremented and a successful status is returned.</span></span>

<span data-ttu-id="9fec9-911">Mutex, başka bir iş parçacığına aitse ve bu iş parçacığı daha yüksek önceliktir ve öncelikli devralma, karşılıklı dışlama oluşturma sırasında belirtilmişse, daha düşük öncelikli iş parçacığının önceliği geçici olarak çağıran iş parçacığından çıkarılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-911">If the mutex is owned by another thread and this thread is higher priority and priority inheritance was specified at mutex create, the lower priority thread's priority will be temporarily raised to that of the calling thread.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-912">*Prioritykalýtým ile bir mutex sahibi olan düşük öncelikli iş parçacığının önceliği, zaman uyumu sahipliği sırasında asla bir dış iş parçacığı tarafından değiştirilmemelidir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-912">*The priority of the lower priority thread owning a mutex with priorityinheritance should never be modified by an external thread during mutex ownership.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-913">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-913">Parameters</span></span>

- <span data-ttu-id="9fec9-914">**mutex_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-914">**mutex_ptr**</span></span>   <br><span data-ttu-id="9fec9-915">Daha önce oluşturulmuş bir mutex işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-915">Pointer to a previously created mutex.</span></span>
- <span data-ttu-id="9fec9-916">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-916">**wait_option**</span></span> <br><span data-ttu-id="9fec9-917">Mutex 'in zaten başka bir iş parçacığı tarafından sahiplendiyse hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-917">Defines how the service behaves if the mutex is already owned by another thread.</span></span> <span data-ttu-id="9fec9-918">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="9fec9-918">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9fec9-919">**TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-919">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="9fec9-920">*Bu, hizmet başlatma işleminden çağrıldığında geçerli tek seçenektir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-920">*This is the only valid option if the service is called from Initialization.*</span></span>
  - <span data-ttu-id="9fec9-921">**TX_WAIT_FOREVER** zaman aşımı değeri (0xffffffff)- **TX_WAIT_FOREVER** seçilmesi, çağıran iş parçacığının mutex kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-921">**TX_WAIT_FOREVER** timeout value (0xFFFFFFFF) - Selecting **TX_WAIT_FOREVER** causes the calling thread to suspend indefinitely until the mutex is available.</span></span>
  - <span data-ttu-id="9fec9-922">zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçilirse, mutex beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-922">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-923">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-923">Return Values</span></span>

- <span data-ttu-id="9fec9-924">**TX_SUCCESS** (0x00) başarılı mutex al işlemi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-924">**TX_SUCCESS** (0x00) Successful mutex get operation.</span></span>
- <span data-ttu-id="9fec9-925">**TX_DELETED** (0x01) mutex 'i iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-925">**TX_DELETED** (0x01) Mutex was deleted while thread was suspended.</span></span>
- <span data-ttu-id="9fec9-926">**TX_NOT_AVAILABLE** (0x1d) hizmeti, mutex 'in sahipliğini, belirtilen süre içinde beklemek için alamadı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-926">**TX_NOT_AVAILABLE** (0x1D) Service was unable to get ownership of the mutex within the specified time to wait.</span></span>
- <span data-ttu-id="9fec9-927">**TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-927">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="9fec9-928">**TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-928">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span>
- <span data-ttu-id="9fec9-929">**TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-929">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>
- <span data-ttu-id="9fec9-930">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-930">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-931">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-931">Allowed From</span></span>

<span data-ttu-id="9fec9-932">Başlatma ve iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="9fec9-932">Initialization and threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-933">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-933">Preemption Possible</span></span>

<span data-ttu-id="9fec9-934">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-934">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-935">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-935">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Obtain exclusive ownership of the mutex "my_mutex".
If the mutex "my_mutex" is not available, suspend until it
becomes available. */
status = tx_mutex_get(&my_mutex, TX_WAIT_FOREVER);
```

### <a name="see-also"></a><span data-ttu-id="9fec9-936">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-936">See Also</span></span>

- <span data-ttu-id="9fec9-937">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-937">tx_mutex_create</span></span>
- <span data-ttu-id="9fec9-938">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-938">tx_mutex_delete</span></span>
- <span data-ttu-id="9fec9-939">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-939">tx_mutex_info_get</span></span>
- <span data-ttu-id="9fec9-940">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-940">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="9fec9-941">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-941">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-942">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-942">tx_mutex_prioritize</span></span>
- <span data-ttu-id="9fec9-943">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-943">tx_mutex_put</span></span>

## <a name="tx_mutex_info_get"></a><span data-ttu-id="9fec9-944">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-944">tx_mutex_info_get</span></span>

<span data-ttu-id="9fec9-945">Mutex hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="9fec9-945">Retrieve information about mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-946">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-946">Prototype</span></span>

```c
UINT tx_mutex_info_get(
    TX_MUTEX *mutex_ptr, 
    CHAR **name,
    ULONG *count, 
    TX_THREAD **owner,
    TX_THREAD **first_suspended,
    ULONG *suspended_count, 
    TX_MUTEX **next_mutex);
```

### <a name="description"></a><span data-ttu-id="9fec9-947">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-947">Description</span></span>

<span data-ttu-id="9fec9-948">Bu hizmet, belirtilen mutex 'ten bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-948">This service retrieves information from the specified mutex.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-949">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-949">Parameters</span></span>

- <span data-ttu-id="9fec9-950">**mutex_ptr** Mutex denetim bloğunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-950">**mutex_ptr** Pointer to mutex control block.</span></span>
- <span data-ttu-id="9fec9-951">**ad** Mutex 'in adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-951">**name** Pointer to destination for the pointer to the mutex's name.</span></span>
- <span data-ttu-id="9fec9-952">**sayı** Mutex 'in sahiplik sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-952">**count** Pointer to destination for the ownership count of the mutex.</span></span>
- <span data-ttu-id="9fec9-953">**sahip** Sahibi olan iş parçacığının işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-953">**owner** Pointer to destination for the owning thread's pointer.</span></span>
- <span data-ttu-id="9fec9-954">**first_suspended** Bu mutex 'in askıya alma listesindeki ilk iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-954">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this mutex.</span></span>
- <span data-ttu-id="9fec9-955">**suspended_count** Bu mutex üzerinde şu anda askıya alınan iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-955">**suspended_count** Pointer to destination for the number of threads currently suspended on this mutex.</span></span>
- <span data-ttu-id="9fec9-956">**next_mutex** Sonraki oluşturulan mutex işaretçisinin işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-956">**next_mutex** Pointer to destination for the pointer of the next created mutex.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-957">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-957">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-958">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-958">Return Values</span></span>

- <span data-ttu-id="9fec9-959">**TX_SUCCESS** (0x00) başarılı mutex bilgisi alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-959">**TX_SUCCESS** (0x00) Successful mutex information retrieval.</span></span>
- <span data-ttu-id="9fec9-960">**TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-960">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-961">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-961">Allowed From</span></span>

<span data-ttu-id="9fec9-962">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-962">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-963">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-963">Preemption Possible</span></span>

<span data-ttu-id="9fec9-964">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-964">No</span></span>

<span data-ttu-id="9fec9-965">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="9fec9-965">**Example**</span></span>

```c
TX_MUTEX my_mutex;
CHAR *name;
ULONG count;
TX_THREAD *owner;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_MUTEX *next_mutex;
UINT status;

/* Retrieve information about the previously created
mutex "my_mutex." */
status = tx_mutex_info_get(&my_mutex, &name,
    &count, &owner,
    &first_suspended, &suspended_count,
    &next_mutex);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-966">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-966">See Also</span></span>

- <span data-ttu-id="9fec9-967">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-967">tx_mutex_create</span></span>
- <span data-ttu-id="9fec9-968">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-968">tx_mutex_delete</span></span>
- <span data-ttu-id="9fec9-969">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-969">tx_mutex_get</span></span>
- <span data-ttu-id="9fec9-970">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-970">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="9fec9-971">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-971">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-972">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-972">tx_mutex_prioritize</span></span>
- <span data-ttu-id="9fec9-973">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-973">tx_mutex_put</span></span>

## <a name="tx_mutex_performance_info_get"></a><span data-ttu-id="9fec9-974">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-974">tx_mutex_performance_info_get</span></span>

<span data-ttu-id="9fec9-975">Mutex performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-975">Get mutex performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-976">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-976">Prototype</span></span>

```c
UINT tx_mutex_performance_info_get(
    TX_MUTEX *mutex_ptr, 
    ULONG *puts,
    ULONG *gets, 
    ULONG *suspensions, 
    ULONG *timeouts,
    ULONG *inversions, 
    ULONG *inheritances);
```

### <a name="description"></a><span data-ttu-id="9fec9-977">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-977">Description</span></span>

<span data-ttu-id="9fec9-978">Bu hizmet, belirtilen mutex hakkında performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-978">This service retrieves performance information about the specified mutex.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-979">*Işparçacığıx kitaplığı ve uygulaması ile*  \* oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_MUTEX_ENABLE_PERFORMANCE_INFO** _ _defined. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-979">*The ThreadX library and application must be built with* ***TX_MUTEX_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-980">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-980">Parameters</span></span>

- <span data-ttu-id="9fec9-981">**mutex_ptr** Önceden oluşturulmuş mutex için işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-981">**mutex_ptr** Pointer to previously created mutex.</span></span>
- <span data-ttu-id="9fec9-982">**koyar** Bu mutex üzerinde gerçekleştirilen PUT isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-982">**puts** Pointer to destination for the number of put requests performed on this mutex.</span></span>
- <span data-ttu-id="9fec9-983">**alır** Bu mutex üzerinde gerçekleştirilen GET isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-983">**gets** Pointer to destination for the number of get requests performed on this mutex.</span></span>
- <span data-ttu-id="9fec9-984">**getirilmesi** Bu mutex üzerinde getirilmesi al iş parçacığı mutex 'in sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-984">**suspensions** Pointer to destination for the number of thread mutex get suspensions on this mutex.</span></span>
- <span data-ttu-id="9fec9-985">**zaman aşımları** Bu mutex üzerinde askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-985">**timeouts** Pointer to destination for the number of mutex get suspension timeouts on this mutex.</span></span>
- <span data-ttu-id="9fec9-986">**Inversions** Bu mutex 'teki iş parçacığı önceliği ınsürümlerin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-986">**inversions** Pointer to destination for the number of thread priority inversions on this mutex.</span></span>
- <span data-ttu-id="9fec9-987">**Inheritances** Bu mutex 'teki iş parçacığı önceliği devralma işlemlerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-987">**inheritances** Pointer to destination for the number of thread priority inheritance operations on this mutex.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-988">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-988">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-989">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-989">Return Values</span></span>

- <span data-ttu-id="9fec9-990">**TX_SUCCESS** (0x00) başarılı mutex performansı Get.</span><span class="sxs-lookup"><span data-stu-id="9fec9-990">**TX_SUCCESS** (0x00) Successful mutex performance get.</span></span>
- <span data-ttu-id="9fec9-991">**TX_PTR_ERROR** (0x03) geçersiz mutex işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-991">**TX_PTR_ERROR** (0x03) Invalid mutex pointer.</span></span>
- <span data-ttu-id="9fec9-992">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-992">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-993">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-993">Allowed From</span></span>

<span data-ttu-id="9fec9-994">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-994">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-995">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-995">Example</span></span>

```c
TX_MUTEX my_mutex;
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;
ULONG inversions;
ULONG inheritances;

/* Retrieve performance information on the previously created
mutex. */
status = tx_mutex_performance_info_get(&my_mutex_ptr, &puts, &gets,
    &suspensions, &timeouts, &inversions, &inheritances);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-996">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-996">See Also</span></span>

- <span data-ttu-id="9fec9-997">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-997">tx_mutex_create</span></span>
- <span data-ttu-id="9fec9-998">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-998">tx_mutex_delete</span></span>
- <span data-ttu-id="9fec9-999">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-999">tx_mutex_get</span></span>
- <span data-ttu-id="9fec9-1000">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1000">tx_mutex_info_get</span></span>
- <span data-ttu-id="9fec9-1001">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1001">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1002">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1002">tx_mutex_prioritize</span></span>
- <span data-ttu-id="9fec9-1003">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1003">tx_mutex_put</span></span>

## <a name="tx_mutex_performance_system_info_get"></a><span data-ttu-id="9fec9-1004">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1004">tx_mutex_performance_system_info_get</span></span>

<span data-ttu-id="9fec9-1005">Mutex sistem performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-1005">Get mutex system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1006">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1006">Prototype</span></span>

```c
UINT tx_mutex_performance_system_info_get(
    ULONG *puts, 
    ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts,
    ULONG *inversions, 
    ULONG *inheritances);
```

### <a name="description"></a><span data-ttu-id="9fec9-1007">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1007">Description</span></span>

<span data-ttu-id="9fec9-1008">Bu hizmet, sistemdeki tüm zaman uyumu sağlayıcılar hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1008">This service retrieves performance information about all the mutexes in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-1009">*ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_MUTEX_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1009">*The ThreadX library and application must be built with* **TX_MUTEX_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1010">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1010">Parameters</span></span>

- <span data-ttu-id="9fec9-1011">**koyar** Tüm zaman uyumu sağlayıcılar üzerinde gerçekleştirilen put isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1011">**puts** Pointer to destination for the total number of put requests performed on all mutexes.</span></span>
- <span data-ttu-id="9fec9-1012">**alır** Tüm zaman uyumu sağlayıcılar üzerinde gerçekleştirilen GET isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1012">**gets** Pointer to destination for the total number of get requests performed on all mutexes.</span></span>
- <span data-ttu-id="9fec9-1013">**getirilmesi** Tüm zaman uyumu sağlayıcılar üzerinde getirilmesi al toplam iş parçacığı mutex için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1013">**suspensions** Pointer to destination for the total number of thread mutex get suspensions on all mutexes.</span></span>
- <span data-ttu-id="9fec9-1014">**zaman aşımları** Tüm zaman uyumu sağlayıcılar üzerinde askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1014">**timeouts** Pointer to destination for the total number of mutex get suspension timeouts on all mutexes.</span></span>
- <span data-ttu-id="9fec9-1015">**Inversions** Tüm zaman uyumu sağlayıcılar üzerinde iş parçacığı önceliği Inversions 'lerin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1015">**inversions** Pointer to destination for the total number of thread priority inversions on all mutexes.</span></span>
- <span data-ttu-id="9fec9-1016">**Inheritances** Tüm zaman uyumu sağlayıcılar üzerinde iş parçacığı önceliği devralma işlemlerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1016">**inheritances** Pointer to destination for the total number of thread priority inheritance operations on all mutexes.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1017">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1017">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1018">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1018">Return Values</span></span>

- <span data-ttu-id="9fec9-1019">**TX_SUCCESS** (0x00) başarılı mutex sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1019">**TX_SUCCESS** (0x00) Successful mutex system performance get.</span></span>
- <span data-ttu-id="9fec9-1020">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1020">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1021">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1021">Allowed From</span></span>

<span data-ttu-id="9fec9-1022">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1022">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1023">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1023">Example</span></span>

```c
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;
ULONG inversions;
ULONG inheritances;

/* Retrieve performance information on all previously created
mutexes. */
status = tx_mutex_performance_system_info_get(&puts, &gets,
    &suspensions, &timeouts,
    &inversions, &inheritances);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1024">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1024">See Also</span></span>

- <span data-ttu-id="9fec9-1025">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1025">tx_mutex_create</span></span>
- <span data-ttu-id="9fec9-1026">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1026">tx_mutex_delete</span></span>
- <span data-ttu-id="9fec9-1027">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1027">tx_mutex_get</span></span>
- <span data-ttu-id="9fec9-1028">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1028">tx_mutex_info_get</span></span>
- <span data-ttu-id="9fec9-1029">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1029">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1030">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1030">tx_mutex_prioritize</span></span>
- <span data-ttu-id="9fec9-1031">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1031">tx_mutex_put</span></span>

## <a name="tx_mutex_prioritize"></a><span data-ttu-id="9fec9-1032">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1032">tx_mutex_prioritize</span></span>

<span data-ttu-id="9fec9-1033">Mutex askıya alma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="9fec9-1033">Prioritize mutex suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1034">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1034">Prototype</span></span>

```c
UINT tx_mutex_prioritize(TX_MUTEX *mutex_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-1035">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1035">Description</span></span>

<span data-ttu-id="9fec9-1036">Bu hizmet, askıya alma listesinin önünde mutex 'in sahipliği için askıya alınan en yüksek öncelik iş parçacığını koyar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1036">This service places the highest priority thread suspended for ownership of the mutex at the front of the suspension list.</span></span> <span data-ttu-id="9fec9-1037">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1037">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1038">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1038">Parameters</span></span>

- <span data-ttu-id="9fec9-1039">**mutex_ptr** Daha önce oluşturulmuş mutex işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1039">**mutex_ptr** Pointer to the previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1040">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1040">Return Values</span></span>

- <span data-ttu-id="9fec9-1041">**TX_SUCCESS** (0x00) başarılı karşılıklı dışlama önceliği.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1041">**TX_SUCCESS** (0x00) Successful mutex prioritize.</span></span>
- <span data-ttu-id="9fec9-1042">**TX_MUTEX_ERROR** (0x1C) geçersiz MUTEX işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1042">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1043">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1043">Allowed From</span></span>

<span data-ttu-id="9fec9-1044">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1044">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1045">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1045">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1046">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1046">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1047">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1047">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Ensure that the highest priority thread will receive
ownership of the mutex when it becomes available. */
status = tx_mutex_prioritize(&my_mutex);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_mutex_put call that releases ownership of the
mutex will give ownership to this thread and wake it
up. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1048">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1048">See Also</span></span>

- <span data-ttu-id="9fec9-1049">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1049">tx_mutex_create</span></span>
- <span data-ttu-id="9fec9-1050">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1050">tx_mutex_delete</span></span>
- <span data-ttu-id="9fec9-1051">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1051">tx_mutex_get</span></span>
- <span data-ttu-id="9fec9-1052">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1052">tx_mutex_info_get</span></span>
- <span data-ttu-id="9fec9-1053">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1053">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1054">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1054">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1055">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1055">tx_mutex_put</span></span>

## <a name="tx_mutex_put"></a><span data-ttu-id="9fec9-1056">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1056">tx_mutex_put</span></span>

<span data-ttu-id="9fec9-1057">Mutex 'in sahipliğini serbest bırakma</span><span class="sxs-lookup"><span data-stu-id="9fec9-1057">Release ownership of mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1058">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1058">Prototype</span></span>

```c
UINT tx_mutex_put(TX_MUTEX *mutex_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-1059">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1059">Description</span></span>

<span data-ttu-id="9fec9-1060">Bu hizmet, belirtilen mutex 'in sahiplik sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1060">This service decrements the ownership count of the specified mutex.</span></span> <span data-ttu-id="9fec9-1061">Sahiplik sayısı sıfırsa, mutex kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1061">If the ownership count is zero, the mutex is made available.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1062">*Karşılıklı dışlama oluşturma sırasında öncelik devralma seçilmişse, serbest bırakma iş parçacığının önceliği, başlangıçta mutex 'in sahipliğini aldığında sahip olduğu önceliğe geri yüklenecektir. Mutex 'in sahipliği sırasında, serbest bırakma iş parçacığında yapılan diğer tüm öncelik değişiklikleri geri alınabilir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1062">*If priority inheritance was selected during mutex creation, the priority of the releasing thread will be restored to the priority it had when it originally obtained ownership of the mutex. Any other priority changes made to the releasing thread during ownership of the mutex may be undone.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1063">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1063">Parameters</span></span>
- <span data-ttu-id="9fec9-1064">daha önce oluşturulmuş olan mutex Işaretçisine mutex_ptr.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1064">mutex_ptr Pointer to the previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1065">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1065">Return Values</span></span>
- <span data-ttu-id="9fec9-1066">**TX_SUCCESS** (0x00) başarılı mutex sürümü.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1066">**TX_SUCCESS** (0x00) Successful mutex release.</span></span>
- <span data-ttu-id="9fec9-1067">**TX_NOT_OWNED** (0x1E) mutex 'i arayana ait değil.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1067">**TX_NOT_OWNED** (0x1E) Mutex is not owned by caller.</span></span>
- <span data-ttu-id="9fec9-1068">**TX_MUTEX_ERROR** (0x1C) MUTEX için geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1068">**TX_MUTEX_ERROR** (0x1C) Invalid pointer to mutex.</span></span>
- <span data-ttu-id="9fec9-1069">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1069">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1070">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1070">Allowed From</span></span>

<span data-ttu-id="9fec9-1071">Başlatma ve iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="9fec9-1071">Initialization and threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1072">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1072">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1073">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1073">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1074">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1074">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Release ownership of "my_mutex." */
status = tx_mutex_put(&my_mutex);

/* If status equals TX_SUCCESS, the mutex ownership
count has been decremented and if zero, released. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1075">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1075">See Also</span></span>

- <span data-ttu-id="9fec9-1076">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1076">tx_mutex_create</span></span>
- <span data-ttu-id="9fec9-1077">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1077">tx_mutex_delete</span></span>
- <span data-ttu-id="9fec9-1078">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1078">tx_mutex_get</span></span>
- <span data-ttu-id="9fec9-1079">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1079">tx_mutex_info_get</span></span>
- <span data-ttu-id="9fec9-1080">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1080">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1081">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1081">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1082">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1082">tx_mutex_prioritize</span></span>

## <a name="tx_queue_create"></a><span data-ttu-id="9fec9-1083">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1083">tx_queue_create</span></span>

<span data-ttu-id="9fec9-1084">İleti kuyruğu oluştur</span><span class="sxs-lookup"><span data-stu-id="9fec9-1084">Create message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1085">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1085">Prototype</span></span>

```c
UINT tx_queue_create(
    TX_QUEUE *queue_ptr, 
    CHAR *name_ptr,
    UINT message_size,
    VOID *queue_start, 
    ULONG queue_size);
```

### <a name="description"></a><span data-ttu-id="9fec9-1086">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1086">Description</span></span>

<span data-ttu-id="9fec9-1087">Bu hizmet, genellikle karşılıklı iş parçacığı iletişimi için kullanılan bir ileti kuyruğu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1087">This service creates a message queue that is typically used for interthread communication.</span></span> <span data-ttu-id="9fec9-1088">Toplam ileti sayısı, belirtilen ileti boyutundan ve sıradaki toplam bayt sayısından hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1088">The total number of messages is calculated from the specified message size and the total number of bytes in the queue.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1089">*Kuyruğun bellek alanında belirtilen toplam bayt sayısı, belirtilen ileti boyutuyla eşit olarak bölünemiyor ise, bellek alanındaki kalan baytlar kullanılmaz.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1089">*If the total number of bytes specified in the queue's memory area is not evenly divisible by the specified message size, the remaining bytes in the memory area are not used.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1090">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1090">Parameters</span></span>

- <span data-ttu-id="9fec9-1091">**queue_ptr** İleti kuyruğu denetim bloğunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1091">**queue_ptr** Pointer to a message queue control block.</span></span>
- <span data-ttu-id="9fec9-1092">**name_ptr** İleti sırasının adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1092">**name_ptr** Pointer to the name of the message queue.</span></span>
- <span data-ttu-id="9fec9-1093">**message_size** Kuyruktaki her iletinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1093">**message_size** Specifies the size of each message in the queue.</span></span> <span data-ttu-id="9fec9-1094">İleti boyutları 1 32 bitlik sözcükten 16 32 bit sözcüklere kadar değişir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1094">Message sizes range from 1 32-bit word to 16 32-bit words.</span></span> <span data-ttu-id="9fec9-1095">Geçerli ileti boyutu seçenekleri, 1 ile 16 arasında (dahil) sayısal değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1095">Valid message size options are numerical values from 1 through 16, inclusive.</span></span>
- <span data-ttu-id="9fec9-1096">**queue_start** İleti sırasının başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1096">**queue_start** Starting address of the message queue.</span></span> <span data-ttu-id="9fec9-1097">Başlangıç adresi ULONG veri türünün boyutuna hizalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1097">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="9fec9-1098">**queue_size** İleti kuyruğu için kullanılabilen toplam bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1098">**queue_size** Total number of bytes available for the message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1099">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1099">Return Values</span></span>

- <span data-ttu-id="9fec9-1100">**TX_SUCCESS** (0x00) başarılı ileti kuyruğu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1100">**TX_SUCCESS** (0x00) Successful message queue creation.</span></span>
- <span data-ttu-id="9fec9-1101">**TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1101">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span> <span data-ttu-id="9fec9-1102">İşaretçi NULL ya da sıra zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1102">Either the pointer is NULL or the queue is already created.</span></span>
- <span data-ttu-id="9fec9-1103">**TX_PTR_ERROR** (0x03) ileti sırasının başlangıç adresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1103">**TX_PTR_ERROR** (0x03) Invalid starting address of the message queue.</span></span>
- <span data-ttu-id="9fec9-1104">**TX_SIZE_ERROR** (0x05) Ileti sırasının boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1104">**TX_SIZE_ERROR** (0x05) Size of message queue is invalid.</span></span>
- <span data-ttu-id="9fec9-1105">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1105">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1106">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1106">Allowed From</span></span>

<span data-ttu-id="9fec9-1107">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-1107">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1108">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1108">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1109">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1109">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1110">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1110">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;

/* Create a message queue whose total size is 2000 bytes
starting at address 0x300000. Each message in this
queue is defined to be 4 32-bit words long. */
status = tx_queue_create(&my_queue, "my_queue_name",
    4, (VOID *) 0x300000, 2000);

/* If status equals TX_SUCCESS, my_queue contains room
for storing 125 messages (2000 bytes/ 16 bytes per
message). */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1111">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1111">See Also</span></span>

- <span data-ttu-id="9fec9-1112">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1112">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1113">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1113">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1114">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1114">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1115">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1115">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1116">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1116">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1117">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1117">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1118">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1118">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1119">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1119">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1120">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1120">tx_queue_send</span></span>
- <span data-ttu-id="9fec9-1121">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1121">tx_queue_send_notify</span></span>

## <a name="tx_queue_delete"></a><span data-ttu-id="9fec9-1122">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1122">tx_queue_delete</span></span>

<span data-ttu-id="9fec9-1123">İleti kuyruğunu sil</span><span class="sxs-lookup"><span data-stu-id="9fec9-1123">Delete message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1124">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1124">Prototype</span></span>

```c
UINT tx_queue_delete(TX_QUEUE *queue_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-1125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1125">Description</span></span>

<span data-ttu-id="9fec9-1126">Bu hizmet, belirtilen ileti sırasını siler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1126">This service deletes the specified message queue.</span></span> <span data-ttu-id="9fec9-1127">Bu kuyruktan bir ileti beklemeden askıya alınmış tüm iş parçacıkları sürdürülür ve TX_DELETED dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1127">All threads suspended waiting for a message from this queue are resumed and given a TX_DELETED return status.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="9fec9-1128">*Uygulama, kuyruk silinmeden önce bu sıra için gönderilen bildirim geri çağrısının tamamlandı (veya devre dışı) olduğundan emin olmalıdır. Ayrıca, uygulamanın, silinen bir kuyruğun gelecekteki kullanımını önlemesi gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1128">*The application must ensure that any send notify callback for this queue is completed (or disabled) before deleting the queue. In addition, the application must prevent any future use of a deleted queue.*</span></span> <br><br><span data-ttu-id="9fec9-1129">*Ayrıca, bu hizmet tamamlandıktan sonra kullanılabilir olan Kuyrukla ilişkili bellek alanını yönetmek için uygulamanın sorumluluğundadır.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1129">*It is also the application's responsibility to manage the memory area associated with the queue, which is available after this service completes.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1130">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1130">Parameters</span></span>

- <span data-ttu-id="9fec9-1131">**queue_ptr** Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1131">**queue_ptr** Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1132">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1132">Return Values</span></span>

- <span data-ttu-id="9fec9-1133">**TX_SUCCESS** (0x00) başarılı ileti sırası silme işlemi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1133">**TX_SUCCESS** (0x00) Successful message queue deletion.</span></span>
- <span data-ttu-id="9fec9-1134">**TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1134">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="9fec9-1135">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1135">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1136">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1136">Allowed From</span></span>

<span data-ttu-id="9fec9-1137">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-1137">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1138">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1138">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1139">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1139">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1140">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1140">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;

/* Delete entire message queue. Assume that the queue
has already been created with a call to
tx_queue_create. */
status = tx_queue_delete(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1141">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1141">See Also</span></span>

- <span data-ttu-id="9fec9-1142">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1142">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1143">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1143">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1144">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1144">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1145">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1145">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1146">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1146">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1147">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1147">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1148">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1148">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1149">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1149">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1150">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1150">tx_queue_send</span></span>
- <span data-ttu-id="9fec9-1151">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1151">tx_queue_send_notify</span></span>

## <a name="tx_queue_flush"></a><span data-ttu-id="9fec9-1152">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1152">tx_queue_flush</span></span>

<span data-ttu-id="9fec9-1153">İleti sırasındaki boş iletiler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1153">Empty messages in message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1154">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1154">Prototype</span></span>

```c
UINT tx_queue_flush(TX_QUEUE *queue_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-1155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1155">Description</span></span>

<span data-ttu-id="9fec9-1156">Bu hizmet, belirtilen ileti kuyruğunda depolanan tüm iletileri siler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1156">This service deletes all messages stored in the specified message queue.</span></span>

<span data-ttu-id="9fec9-1157">Sıra doluysa, askıya alınmış tüm iş parçacıklarının iletileri atılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1157">If the queue is full, messages of all suspended threads are discarded.</span></span> <span data-ttu-id="9fec9-1158">Askıya alınan her iş parçacığı daha sonra ileti gönderme işleminin başarılı olduğunu belirten bir dönüş durumuyla sürdürülür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1158">Each suspended thread is then resumed with a return status that indicates the message send was successful.</span></span> <span data-ttu-id="9fec9-1159">Sıra boşsa, bu hizmet hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1159">If the queue is empty, this service does nothing.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1160">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1160">Parameters</span></span>

- <span data-ttu-id="9fec9-1161">**queue_ptr** Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1161">**queue_ptr** Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1162">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1162">Return Values</span></span>

- <span data-ttu-id="9fec9-1163">**TX_SUCCESS** (0x00) başarılı ileti kuyruğu Temizleme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1163">**TX_SUCCESS** (0x00) Successful message queue flush.</span></span>
- <span data-ttu-id="9fec9-1164">**TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1164">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1165">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1165">Allowed From</span></span>

<span data-ttu-id="9fec9-1166">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1166">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1167">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1167">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1168">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1168">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1169">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1169">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;

/* Flush out all pending messages in the specified message
queue. Assume that the queue has already been created
with a call to tx_queue_create. */
status = tx_queue_flush(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
empty. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1170">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1170">See Also</span></span>

- <span data-ttu-id="9fec9-1171">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1171">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1172">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1172">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1173">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1173">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1174">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1174">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1175">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1175">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1176">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1176">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1177">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1177">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1178">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1178">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1179">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1179">tx_queue_send</span></span>
- <span data-ttu-id="9fec9-1180">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1180">tx_queue_send_notify</span></span>

## <a name="tx_queue_front_send"></a><span data-ttu-id="9fec9-1181">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1181">tx_queue_front_send</span></span>

<span data-ttu-id="9fec9-1182">Kuyruğun önüne ileti gönder</span><span class="sxs-lookup"><span data-stu-id="9fec9-1182">Send message to the front of queue</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1183">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1183">Prototype</span></span>

```c
UINT tx_queue_front_send(
    TX_QUEUE *queue_ptr,
    VOID *source_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="9fec9-1184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1184">Description</span></span>

<span data-ttu-id="9fec9-1185">Bu hizmet, belirtilen ileti sırasının ön konumuna bir ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1185">This service sends a message to the front location of the specified message queue.</span></span> <span data-ttu-id="9fec9-1186">İleti, kaynak işaretçi tarafından belirtilen bellek alanından kuyruğun önüne **kopyalanır** .</span><span class="sxs-lookup"><span data-stu-id="9fec9-1186">The message is **copied** to the front of the queue from the memory area specified by the source pointer.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1187">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1187">Parameters</span></span>

- <span data-ttu-id="9fec9-1188">**queue_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1188">**queue_ptr**</span></span> <br><span data-ttu-id="9fec9-1189">İleti kuyruğu denetim bloğunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1189">Pointer to a message queue control block.</span></span>
- <span data-ttu-id="9fec9-1190">**source_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1190">**source_ptr**</span></span> <br><span data-ttu-id="9fec9-1191">İleti işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1191">Pointer to the message.</span></span>
- <span data-ttu-id="9fec9-1192">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1192">**wait_option**</span></span>  <br><span data-ttu-id="9fec9-1193">İleti kuyruğu doluysa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1193">Defines how the service behaves if the message queue is full.</span></span> <span data-ttu-id="9fec9-1194">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="9fec9-1194">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9fec9-1195">**TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1195">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="9fec9-1196">*Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1196">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.*</span></span>
  - <span data-ttu-id="9fec9-1197">**TX_WAIT_FOREVER** (0xffffffff)-TX_WAIT_FOREVER seçilmesi, sıraya alan alana kadar çağıran iş parçacığının sonsuza kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1197">**TX_WAIT_FOREVER** (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until there is room in the queue.</span></span>
  - <span data-ttu-id="9fec9-1198">zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçilirse, kuyrukta Oda beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1198">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for room in the queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1199">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1199">Return Values</span></span>

- <span data-ttu-id="9fec9-1200">**TX_SUCCESS** (0x00) Ileti gönderme başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1200">**TX_SUCCESS** (0x00) Successful sending of message.</span></span>
- <span data-ttu-id="9fec9-1201">**TX_DELETED** (0x01) ileti kuyruğu, iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1201">**TX_DELETED** (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="9fec9-1202">**TX_QUEUE_FULL** (0x0B) hizmeti, belirtilen süre boyunca sıra dolu olduğundan ileti gönderemedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1202">**TX_QUEUE_FULL** (0x0B) Service was unable to send message because the queue was full for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="9fec9-1203">**TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1203">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="9fec9-1204">**TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1204">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="9fec9-1205">**TX_PTR_ERROR** (0x03) Ileti için geçersiz kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1205">**TX_PTR_ERROR** (0x03) Invalid source pointer for message.</span></span>
- <span data-ttu-id="9fec9-1206">**TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1206">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1207">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1207">Allowed From</span></span>

<span data-ttu-id="9fec9-1208">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1208">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1209">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1209">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1210">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1210">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1211">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1211">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Send a message to the front of "my_queue." Return
immediately, regardless of success. This wait
option is used for calls from initialization, timers,
and ISRs. */
status = tx_queue_front_send(&my_queue, my_message,
    TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is at the front
of the specified queue. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1212">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1212">See Also</span></span>

- <span data-ttu-id="9fec9-1213">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1213">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1214">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1214">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1215">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1215">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1216">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1216">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1217">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1217">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1218">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1218">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1219">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1219">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1220">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1220">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1221">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1221">tx_queue_send</span></span>
- <span data-ttu-id="9fec9-1222">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1222">tx_queue_send_notify</span></span>

## <a name="tx_queue_info_get"></a><span data-ttu-id="9fec9-1223">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1223">tx_queue_info_get</span></span>

<span data-ttu-id="9fec9-1224">Kuyruk hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="9fec9-1224">Retrieve information about queue</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1225">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1225">Prototype</span></span>

```c
UINT tx_queue_info_get(
    TX_QUEUE *queue_ptr, 
    CHAR **name,
    ULONG *enqueued, 
    ULONG *available_storage
    TX_THREAD **first_suspended, 
    ULONG *suspended_count,
    TX_QUEUE **next_queue);
```

### <a name="description"></a><span data-ttu-id="9fec9-1226">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1226">Description</span></span>

<span data-ttu-id="9fec9-1227">Bu hizmet, belirtilen ileti kuyruğu hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1227">This service retrieves information about the specified message queue.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1228">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1228">Parameters</span></span>

- <span data-ttu-id="9fec9-1229">**queue_ptr** Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1229">**queue_ptr** Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="9fec9-1230">**ad** Kuyruğun adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1230">**name** Pointer to destination for the pointer to the queue's name.</span></span>
- <span data-ttu-id="9fec9-1231">**sıraya alındı** Şu anda kuyruktaki ileti sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1231">**enqueued** Pointer to destination for the number of messages currently in the queue.</span></span>
- <span data-ttu-id="9fec9-1232">**available_storage** Kuyruğun Şu anda alanı bulunan ileti sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1232">**available_storage** Pointer to destination for the number of messages the queue currently has space for.</span></span>
- <span data-ttu-id="9fec9-1233">**first_suspended** Bu sıranın askıya alma listesindeki iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1233">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this queue.</span></span>
- <span data-ttu-id="9fec9-1234">**suspended_count** Bu sırada askıya alınmış olan iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1234">**suspended_count** Pointer to destination for the number of threads currently suspended on this queue.</span></span>
- <span data-ttu-id="9fec9-1235">**next_queue** Sonraki oluşturulan sıranın işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1235">**next_queue** Pointer to destination for the pointer of the next created queue.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1236">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1236">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1237">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1237">Return Values</span></span>

- <span data-ttu-id="9fec9-1238">**TX_SUCCESS** (0x00) başarılı kuyruk bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1238">**TX_SUCCESS** (0x00) Successful queue information get.</span></span>
- <span data-ttu-id="9fec9-1239">**TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1239">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1240">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1240">Allowed From</span></span>

<span data-ttu-id="9fec9-1241">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1241">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1242">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1242">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1243">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1243">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1244">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1244">Example</span></span>

```c
TX_QUEUE my_queue;
CHAR *name;
ULONG enqueued;
ULONG available_storage;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_QUEUE *next_queue;
UINT status;

/* Retrieve information about the previously created
message queue "my_queue." */
status = tx_queue_info_get(&my_queue, &name,
    &enqueued, &available_storage,
    &first_suspended, &suspended_count,
    &next_queue);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1245">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1245">See Also</span></span>

- <span data-ttu-id="9fec9-1246">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1246">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1247">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1247">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1248">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1248">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1249">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1249">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1250">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1250">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1251">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1251">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1252">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1252">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1253">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1253">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1254">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1254">tx_queue_send</span></span>
- <span data-ttu-id="9fec9-1255">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1255">tx_queue_send_notify</span></span>

## <a name="tx_queue_performance_info_get"></a><span data-ttu-id="9fec9-1256">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1256">tx_queue_performance_info_get</span></span>

<span data-ttu-id="9fec9-1257">Sıra performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-1257">Get queue performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1258">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1258">Prototype</span></span>

```c
UINT tx_queue_performance_info_get(
    TX_QUEUE *queue_ptr,
    ULONG *messages_sent, 
    ULONG *messages_received,
    ULONG *empty_suspensions, 
    ULONG *full_suspensions,
    ULONG *full_errors, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="9fec9-1259">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1259">Description</span></span>

<span data-ttu-id="9fec9-1260">Bu hizmet, belirtilen sıra hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1260">This service retrieves performance information about the specified queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-1261">*Işparçacığıx kitaplığı ve uygulaması ile*  \* oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1261">*The ThreadX library and application must be built with* ***TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1262">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1262">Parameters</span></span>

- <span data-ttu-id="9fec9-1263">**queue_ptr** Önceden oluşturulmuş sıranın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1263">**queue_ptr** Pointer to previously created queue.</span></span>
- <span data-ttu-id="9fec9-1264">**messages_sent** Bu kuyrukta gerçekleştirilen gönderme isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1264">**messages_sent** Pointer to destination for the number of send requests performed on this queue.</span></span>
- <span data-ttu-id="9fec9-1265">**messages_received** Bu kuyrukta gerçekleştirilen alma isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1265">**messages_received** Pointer to destination for the number of receive requests performed on this queue.</span></span>
- <span data-ttu-id="9fec9-1266">**empty_suspensions** Bu kuyruktaki kuyruk boş getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1266">**empty_suspensions** Pointer to destination for the number of queue empty suspensions on this queue.</span></span>
- <span data-ttu-id="9fec9-1267">**full_suspensions** Bu kuyruktaki sıra Full getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1267">**full_suspensions** Pointer to destination for the number of queue full suspensions on this queue.</span></span>
- <span data-ttu-id="9fec9-1268">**full_errors** Bu kuyruktaki sıranın tam hatalarının sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1268">**full_errors** Pointer to destination for the number of queue full errors on this queue.</span></span>
- <span data-ttu-id="9fec9-1269">**zaman aşımları** Bu kuyruktaki iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1269">**timeouts** Pointer to destination for the number of thread suspension timeouts on this queue.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1270">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1270">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1271">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1271">Return Values</span></span>

- <span data-ttu-id="9fec9-1272">**TX_SUCCESS** (0x00) başarılı kuyruk performansı alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1272">**TX_SUCCESS** (0x00) Successful queue performance get.</span></span>
- <span data-ttu-id="9fec9-1273">**TX_PTR_ERROR** (0x03) geçersiz kuyruk işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1273">**TX_PTR_ERROR** (0x03) Invalid queue pointer.</span></span>
- <span data-ttu-id="9fec9-1274">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1274">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1275">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1275">Allowed From</span></span>

<span data-ttu-id="9fec9-1276">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1276">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1277">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1277">Example</span></span>

```c
TX_QUEUE my_queue;
ULONG messages_sent;
ULONG messages_received;
ULONG empty_suspensions;
ULONG full_suspensions;
ULONG full_errors;
ULONG timeouts;

/* Retrieve performance information on the previously created
queue. */
status = tx_queue_performance_info_get(&my_queue, &messages_sent,
    &messages_received, &empty_suspensions,
    &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1278">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1278">See Also</span></span>

- <span data-ttu-id="9fec9-1279">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1279">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1280">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1280">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1281">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1281">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1282">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1282">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1283">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1283">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1284">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1284">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1285">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1285">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1286">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1286">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1287">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1287">tx_queue_send</span></span>
- <span data-ttu-id="9fec9-1288">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1288">tx_queue_send_notify</span></span>

## <a name="tx_queue_performance_system_info_get"></a><span data-ttu-id="9fec9-1289">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1289">tx_queue_performance_system_info_get</span></span>

<span data-ttu-id="9fec9-1290">Sıra sistemi performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-1290">Get queue system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1291">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1291">Prototype</span></span>

```c
UINT tx_queue_performance_system_info_get(
    ULONG *messages_sent,
    ULONG *messages_received, 
    ULONG *empty_suspensions,
    ULONG *full_suspensions, 
    ULONG *full_errors,
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="9fec9-1292">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1292">Description</span></span>

<span data-ttu-id="9fec9-1293">Bu hizmet sistemdeki tüm kuyruklarla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1293">This service retrieves performance information about all the queues in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-1294">*Işparçacığıx kitaplığı ve uygulaması ile*  \* oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1294">*The ThreadX library and application must be built with* ***TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1295">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1295">Parameters</span></span>

- <span data-ttu-id="9fec9-1296">**messages_sent** Tüm kuyruklarda gerçekleştirilen gönderme isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1296">**messages_sent** Pointer to destination for the total number of send requests performed on all queues.</span></span>
- <span data-ttu-id="9fec9-1297">**messages_received** Tüm kuyruklarda gerçekleştirilen Alım isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1297">**messages_received** Pointer to destination for the total number of receive requests performed on all queues.</span></span>
- <span data-ttu-id="9fec9-1298">**empty_suspensions** Tüm kuyruklarda boş sıranın toplam sayısı için hedef işaretçisi. getirilmesi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1298">**empty_suspensions** Pointer to destination for the total number of queue empty suspensions on all queues.</span></span>
- <span data-ttu-id="9fec9-1299">**full_suspensions** Tüm kuyruklarda toplam Queue Full getirilmesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1299">**full_suspensions** Pointer to destination for the total number of queue full suspensions on all queues.</span></span>
- <span data-ttu-id="9fec9-1300">**full_errors** Tüm sıralarda toplam sıra tam hatalarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1300">**full_errors** Pointer to destination for the total number of queue full errors on all queues.</span></span>
- <span data-ttu-id="9fec9-1301">**zaman aşımları** Tüm sıralarda toplam iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1301">**timeouts** Pointer to destination for the total number of thread suspension timeouts on all queues.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1302">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1302">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

<span data-ttu-id="9fec9-1303">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1303">**Return Values**</span></span>

- <span data-ttu-id="9fec9-1304">**TX_SUCCESS** (0x00) başarılı kuyruk sistem performansı alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1304">**TX_SUCCESS** (0x00) Successful queue system performance get.</span></span>
- <span data-ttu-id="9fec9-1305">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1305">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1306">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1306">Allowed From</span></span>

<span data-ttu-id="9fec9-1307">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1307">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1308">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1308">Example</span></span>

```c
ULONG messages_sent;
ULONG messages_received;
ULONG empty_suspensions;
ULONG full_suspensions;
ULONG full_errors;
ULONG timeouts;

/* Retrieve performance information on all previously created
queues. */
status = tx_queue_performance_system_info_get(&messages_sent,
    &messages_received, &empty_suspensions,
    &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1309">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1309">See Also</span></span>

- <span data-ttu-id="9fec9-1310">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1310">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1311">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1311">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1312">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1312">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1313">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1313">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1314">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1314">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1315">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1315">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1316">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1316">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1317">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1317">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1318">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1318">tx_queue_send</span></span>
- <span data-ttu-id="9fec9-1319">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1319">tx_queue_send_notify</span></span>

## <a name="tx_queue_prioritize"></a><span data-ttu-id="9fec9-1320">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1320">tx_queue_prioritize</span></span>

<span data-ttu-id="9fec9-1321">Sıra askıya alma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="9fec9-1321">Prioritize queue suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1322">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1322">Prototype</span></span>

```c
UINT tx_queue_prioritize(TX_QUEUE *queue_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-1323">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1323">Description</span></span>

<span data-ttu-id="9fec9-1324">Bu hizmet, askıya alma listesinin önünde bu kuyruğa bir ileti (veya bir ileti yerleştirmek için) için askıya alınan en yüksek öncelik iş parçacığını yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1324">This service places the highest priority thread suspended for a message (or to place a message) on this queue at the front of the suspension list.</span></span>

<span data-ttu-id="9fec9-1325">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1325">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1326">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1326">Parameters</span></span>

- <span data-ttu-id="9fec9-1327">**queue_ptr** Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1327">**queue_ptr** Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1328">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1328">Return Values</span></span>

- <span data-ttu-id="9fec9-1329">**TX_SUCCESS** (0x00) başarılı kuyruk önceliği belirleme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1329">**TX_SUCCESS** (0x00) Successful queue prioritize.</span></span>
- <span data-ttu-id="9fec9-1330">**TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1330">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1331">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1331">Allowed From</span></span>

<span data-ttu-id="9fec9-1332">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1332">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1333">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1333">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1334">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1334">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1335">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1335">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;

/* Ensure that the highest priority thread will receive
the next message placed on this queue. */
status = tx_queue_prioritize(&my_queue);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_queue_send or tx_queue_front_send call made
to this queue will wake up this thread. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1336">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1336">See Also</span></span>

- <span data-ttu-id="9fec9-1337">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1337">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1338">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1338">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1339">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1339">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1340">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1340">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1341">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1341">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1342">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1342">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1343">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1343">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1344">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1344">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1345">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1345">tx_queue_send</span></span>
- <span data-ttu-id="9fec9-1346">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1346">tx_queue_send_notify</span></span>

## <a name="tx_queue_receive"></a><span data-ttu-id="9fec9-1347">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1347">tx_queue_receive</span></span>

<span data-ttu-id="9fec9-1348">İleti kuyruğundan ileti al</span><span class="sxs-lookup"><span data-stu-id="9fec9-1348">Get message from message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1349">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1349">Prototype</span></span>

```c
UINT tx_queue_receive(
    TX_QUEUE *queue_ptr,
    VOID *destination_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="9fec9-1350">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1350">Description</span></span>

<span data-ttu-id="9fec9-1351">Bu hizmet, belirtilen ileti sırasından bir ileti alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1351">This service retrieves a message from the specified message queue.</span></span> <span data-ttu-id="9fec9-1352">Alınan ileti, kuyruktan hedef işaretçi tarafından belirtilen bellek alanına **kopyalanır** .</span><span class="sxs-lookup"><span data-stu-id="9fec9-1352">The retrieved message is **copied** from the queue into the memory area specified by the destination pointer.</span></span> <span data-ttu-id="9fec9-1353">Bu ileti daha sonra kuyruktan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1353">That message is then removed from the queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-1354">*Belirtilen hedef bellek alanı iletiyi tutabilecek kadar büyük olmalıdır; yani, ileti hedefi tarafından*  \* işaret edilen **destination_ptr** _ _must en azından bu sıranın ileti boyutu kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1354">*The specified destination memory area must be large enough to hold the message; i.e., the message destination pointed to by* \***destination_ptr** _ _must be at least as large as the message size for this queue.</span></span> <span data-ttu-id="9fec9-1355">Aksi takdirde, hedef yeterince büyük değilse, aşağıdaki bellek alanında bellek bozulması oluşur. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1355">Otherwise, if the destination is not large enough, memory corruption occurs in the following memory area.\*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1356">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1356">Parameters</span></span>

- <span data-ttu-id="9fec9-1357">**queue_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1357">**queue_ptr**</span></span> <br><span data-ttu-id="9fec9-1358">Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1358">Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="9fec9-1359">**destination_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1359">**destination_ptr**</span></span> <br><span data-ttu-id="9fec9-1360">İletinin kopyalanacağı konum.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1360">Location of where to copy the message.</span></span>
- <span data-ttu-id="9fec9-1361">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1361">**wait_option**</span></span> <br><span data-ttu-id="9fec9-1362">İleti sırası boş ise hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1362">Defines how the service behaves if the message queue is empty.</span></span> <span data-ttu-id="9fec9-1363">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="9fec9-1363">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9fec9-1364">**TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1364">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="9fec9-1365">Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1365">This is the only valid option if the service is called from a non-thread; e.g.,  Initialization, timer, or ISR.</span></span>
  - <span data-ttu-id="9fec9-1366">**TX_WAIT_FOREVER** (0xffffffff)-TX_WAIT_FOREVER seçme, çağıran iş parçacığının bir ileti kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1366">**TX_WAIT_FOREVER** (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a message is available.</span></span>
  - <span data-ttu-id="9fec9-1367">zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, ileti beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1367">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a message.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1368">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1368">Return Values</span></span>

- <span data-ttu-id="9fec9-1369">İleti başarıyla alımı **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="9fec9-1369">**TX_SUCCESS** (0x00) Successful retrieval of message.</span></span>
- <span data-ttu-id="9fec9-1370">**TX_DELETED** (0x01) ileti kuyruğu, iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1370">**TX_DELETED** (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="9fec9-1371">**TX_QUEUE_EMPTY** (0X0a) hizmeti, belirtilen sürenin süresi boyunca sıra boş olduğundan bir iletiyi alamadı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1371">**TX_QUEUE_EMPTY** (0x0A) Service was unable to retrieve a message because the queue was empty for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="9fec9-1372">**TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1372">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="9fec9-1373">**TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1373">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="9fec9-1374">**TX_PTR_ERROR** (0x03) Ileti için geçersiz hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1374">**TX_PTR_ERROR** (0x03) Invalid destination pointer for message.</span></span>
- <span data-ttu-id="9fec9-1375">**TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1375">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1376">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1376">Allowed From</span></span>

<span data-ttu-id="9fec9-1377">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1377">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1378">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1378">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1379">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1379">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1380">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1380">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Retrieve a message from "my_queue." If the queue is
empty, suspend until a message is present. Note that
this suspension is only possible from application
threads. */
status = tx_queue_receive(&my_queue, my_message,
    TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the message is in
"my_message." */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1381">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1381">See Also</span></span>

- <span data-ttu-id="9fec9-1382">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1382">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1383">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1383">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1384">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1384">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1385">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1385">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1386">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1386">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1387">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1387">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1388">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1388">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1389">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1389">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1390">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1390">tx_queue_send</span></span>
- <span data-ttu-id="9fec9-1391">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1391">tx_queue_send_notify</span></span>

## <a name="tx_queue_send"></a><span data-ttu-id="9fec9-1392">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1392">tx_queue_send</span></span>

<span data-ttu-id="9fec9-1393">İletiyi ileti kuyruğuna gönder</span><span class="sxs-lookup"><span data-stu-id="9fec9-1393">Send message to message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1394">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1394">Prototype</span></span>

```c
UINT tx_queue_send(
    TX_QUEUE *queue_ptr,
    VOID *source_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="9fec9-1395">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1395">Description</span></span>

<span data-ttu-id="9fec9-1396">Bu hizmet, belirtilen ileti kuyruğuna bir ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1396">This service sends a message to the specified message queue.</span></span> <span data-ttu-id="9fec9-1397">Gönderilen ileti, kaynak işaretçi tarafından belirtilen bellek alanından kuyruğa **kopyalanır** .</span><span class="sxs-lookup"><span data-stu-id="9fec9-1397">The sent message is **copied** to the queue from the memory area specified by the source pointer.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1398">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1398">Parameters</span></span>
- <span data-ttu-id="9fec9-1399">**queue_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1399">**queue_ptr**</span></span> <br><span data-ttu-id="9fec9-1400">Önceden oluşturulmuş bir ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1400">Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="9fec9-1401">**source_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1401">**source_ptr**</span></span> <br><span data-ttu-id="9fec9-1402">İleti işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1402">Pointer to the message.</span></span>
- <span data-ttu-id="9fec9-1403">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1403">**wait_option**</span></span> <br><span data-ttu-id="9fec9-1404">İleti kuyruğu doluysa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1404">Defines how the service behaves if the message queue is full.</span></span> <span data-ttu-id="9fec9-1405">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="9fec9-1405">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9fec9-1406">**TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1406">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="9fec9-1407">*Bu, hizmet iş parçacığından çağrıldığında geçerli olan tek seçenektir; Örneğin, başlatma, süreölçer veya ISR*.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1407">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR*.</span></span>
  - <span data-ttu-id="9fec9-1408">**TX_WAIT_FOREVER** (0xffffffff)-TX_WAIT_FOREVER seçilmesi, sıraya alan alana kadar çağıran iş parçacığının sonsuza kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1408">**TX_WAIT_FOREVER** (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until there is room in the queue.</span></span>
  - <span data-ttu-id="9fec9-1409">zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçilirse, kuyrukta Oda beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1409">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for room in the queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1410">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1410">Return Values</span></span>

- <span data-ttu-id="9fec9-1411">**TX_SUCCESS** (0x00) Ileti gönderme başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1411">**TX_SUCCESS** (0x00) Successful sending of message.</span></span>
- <span data-ttu-id="9fec9-1412">**TX_DELETED** (0x01) ileti kuyruğu, iş parçacığı askıya alınırken silindi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1412">**TX_DELETED** (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="9fec9-1413">**TX_QUEUE_FULL** (0x0B) hizmeti, belirtilen süre boyunca sıra dolu olduğundan ileti gönderemedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1413">**TX_QUEUE_FULL** (0x0B) Service was unable to send message because the queue was full for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="9fec9-1414">**TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1414">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="9fec9-1415">**TX_QUEUE_ERROR** (0x09) geçersiz ileti kuyruğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1415">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="9fec9-1416">**TX_PTR_ERROR** (0x03) Ileti için geçersiz kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1416">**TX_PTR_ERROR** (0x03) Invalid source pointer for message.</span></span>
- <span data-ttu-id="9fec9-1417">**TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1417">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1418">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1418">Allowed From</span></span>

<span data-ttu-id="9fec9-1419">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1419">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1420">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1420">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1421">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1421">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1422">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1422">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Send a message to "my_queue." Return immediately,
regardless of success. This wait option is used for
calls from initialization, timers, and ISRs. */
status = tx_queue_send(&my_queue, my_message, TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is in the
queue. */
```

<span data-ttu-id="9fec9-1423">**Ayrıca bkz.**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1423">**See Also**</span></span>

- <span data-ttu-id="9fec9-1424">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1424">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1425">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1425">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1426">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1426">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1427">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1427">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1428">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1428">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1429">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1429">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1430">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1430">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1431">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1431">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1432">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1432">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1433">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1433">tx_queue_send_notify</span></span>

## <a name="tx_queue_send_notify"></a><span data-ttu-id="9fec9-1434">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1434">tx_queue_send_notify</span></span>

<span data-ttu-id="9fec9-1435">İleti kuyruğa gönderildiğinde uygulamayı bilgilendir</span><span class="sxs-lookup"><span data-stu-id="9fec9-1435">Notify application when message is sent to queue</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1436">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1436">Prototype</span></span>

```c
UINT tx_queue_send_notify(
    TX_QUEUE *queue_ptr,
    VOID (*queue_send_notify)(TX_QUEUE *));
```

### <a name="description"></a><span data-ttu-id="9fec9-1437">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1437">Description</span></span>

<span data-ttu-id="9fec9-1438">Bu hizmet, belirtilen sıraya bir ileti gönderildiğinde çağrılan bir bildirim geri arama işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1438">This service registers a notification callback function that is called whenever a message is sent to the specified queue.</span></span> <span data-ttu-id="9fec9-1439">Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1439">The processing of the notification callback is defined by the application.</span></span>

>[!NOTE]
> <span data-ttu-id="9fec9-1440">*Uygulamanın kuyruk gönderme bildirimi geri çağırması, askıya alma seçeneğiyle herhangi bir ThreadX API çağrısı yapılmasına izin verilmez.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1440">*The application's queue send notification callback is not allowed to call any ThreadX API with a suspension option.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1441">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1441">Parameters</span></span>

- <span data-ttu-id="9fec9-1442">**queue_ptr** Önceden oluşturulmuş sıranın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1442">**queue_ptr** Pointer to previously created queue.</span></span>
- <span data-ttu-id="9fec9-1443">**queue_send_notify** Uygulamanın kuyruk gönderme bildirimi işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1443">**queue_send_notify** Pointer to application's queue send notification function.</span></span> <span data-ttu-id="9fec9-1444">Bu değer TX_NULL, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1444">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1445">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1445">Return Values</span></span>

- <span data-ttu-id="9fec9-1446">**TX_SUCCESS** (0x00) kuyruk gönderme bildiriminin başarıyla kaydı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1446">**TX_SUCCESS** (0x00) Successful registration of queue send notification.</span></span>
- <span data-ttu-id="9fec9-1447">**TX_QUEUE_ERROR** (0x09) geçersiz kuyruk işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1447">**TX_QUEUE_ERROR** (0x09) Invalid queue pointer.</span></span>
- <span data-ttu-id="9fec9-1448">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem bildirim özellikleri devre dışı olarak derlendi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1448">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1449">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1449">Allowed From</span></span>

<span data-ttu-id="9fec9-1450">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1450">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1451">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1451">Example</span></span>

```c
TX_QUEUE my_queue;
/* Register the "my_queue_send_notify" function for monitoring
messages sent to the queue "my_queue." */
status = tx_queue_send_notify(&my_queue, my_queue_send_notify);

/* If status is TX_SUCCESS the queue send notification function was
successfully registered. */
void my_queue_send_notify(TX_QUEUE *queue_ptr)
{
    /* A message was just sent to this queue! */
}
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1452">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1452">See Also</span></span>

- <span data-ttu-id="9fec9-1453">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1453">tx_queue_create</span></span>
- <span data-ttu-id="9fec9-1454">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1454">tx_queue_delete</span></span>
- <span data-ttu-id="9fec9-1455">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="9fec9-1455">tx_queue_flush</span></span>
- <span data-ttu-id="9fec9-1456">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1456">tx_queue_front_send</span></span>
- <span data-ttu-id="9fec9-1457">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1457">tx_queue_info_get</span></span>
- <span data-ttu-id="9fec9-1458">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1458">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1459">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1459">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1460">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1460">tx_queue_prioritize</span></span>
- <span data-ttu-id="9fec9-1461">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="9fec9-1461">tx_queue_receive</span></span>
- <span data-ttu-id="9fec9-1462">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="9fec9-1462">tx_queue_send</span></span>

## <a name="tx_semaphore_ceiling_put"></a><span data-ttu-id="9fec9-1463">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1463">tx_semaphore_ceiling_put</span></span>

<span data-ttu-id="9fec9-1464">Tavan ile sayım semafora bir örnek yerleştirme</span><span class="sxs-lookup"><span data-stu-id="9fec9-1464">Place an instance in counting semaphore with ceiling</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1465">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1465">Prototype</span></span>

```c
UINT tx_semaphore_ceiling_put(
    TX_SEMAPHORE *semaphore_ptr,
    ULONG ceiling);
```

### <a name="description"></a><span data-ttu-id="9fec9-1466">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1466">Description</span></span>

<span data-ttu-id="9fec9-1467">Bu hizmet, gerçekte belirtilen sayım semafora bir örnek koyar ve bu da gerçekteki sayım semaforu bir tane artırır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1467">This service puts an instance into the specified counting semaphore, which in reality increments the counting semaphore by one.</span></span> <span data-ttu-id="9fec9-1468">Sayım semaforun geçerli değeri belirtilen tavan değerinden büyük veya bu değere eşitse, örnek yerleştirmeyecektir ve bir TX_CEILING_EXCEEDED hatası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1468">If the counting semaphore's current value is greater than or equal to the specified ceiling, the instance will not be put and a TX_CEILING_EXCEEDED error will be returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1469">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1469">Parameters</span></span>

- <span data-ttu-id="9fec9-1470">**semaphore_ptr** Daha önce oluşturulan semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1470">**semaphore_ptr** Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="9fec9-1471">**tavan** Semafor için izin verilen üst sınır (geçerli değer aralığı 1 ile 0xFFFFFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="9fec9-1471">**ceiling** Maximum limit allowed for the semaphore (valid values range from 1 through 0xFFFFFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1472">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1472">Return Values</span></span>

- <span data-ttu-id="9fec9-1473">**TX_SUCCESS (0x00)** Başarılı semafor tavan koyma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1473">**TX_SUCCESS (0x00)** Successful semaphore ceiling put.</span></span>
- <span data-ttu-id="9fec9-1474">**TX_CEILING_EXCEEDED** (0x21) PUT isteği tavan aşıyor.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1474">**TX_CEILING_EXCEEDED** (0x21) Put request exceeds ceiling.</span></span>
- <span data-ttu-id="9fec9-1475">**TX_INVALID_CEILING** (0x22) tavan için geçersiz sıfır değeri sağlandı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1475">**TX_INVALID_CEILING** (0x22) An invalid value of zero was supplied for ceiling.</span></span>
- <span data-ttu-id="9fec9-1476">**TX_SEMAPHORE_ERROR** (0x0C) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1476">**TX_SEMAPHORE_ERROR** (0x0C) Invalid semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1477">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1477">Allowed From</span></span>

<span data-ttu-id="9fec9-1478">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1478">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1479">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1479">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;

/* Increment the counting semaphore "my_semaphore" but make sure
that it never exceeds 7 as specified in the call. */
status = tx_semaphore_ceiling_put(&my_semaphore, 7);

/* If status is TX_SUCCESS the semaphore count has been
incremented. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1480">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1480">See Also</span></span>

- <span data-ttu-id="9fec9-1481">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1481">tx_semaphore_create</span></span>
- <span data-ttu-id="9fec9-1482">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1482">tx_semaphore_delete</span></span>
- <span data-ttu-id="9fec9-1483">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1483">tx_semaphore_get</span></span>
- <span data-ttu-id="9fec9-1484">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1484">tx_semaphore_info_get</span></span>
- <span data-ttu-id="9fec9-1485">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1485">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1486">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1486">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1487">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1487">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="9fec9-1488">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1488">tx_semaphore_put</span></span>
- <span data-ttu-id="9fec9-1489">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1489">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_create"></a><span data-ttu-id="9fec9-1490">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1490">tx_semaphore_create</span></span>

<span data-ttu-id="9fec9-1491">Sayım semaforu oluştur</span><span class="sxs-lookup"><span data-stu-id="9fec9-1491">Create counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1492">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1492">Prototype</span></span>

```c
UINT tx_semaphore_create(
    TX_SEMAPHORE *semaphore_ptr,
    CHAR *name_ptr, 
    ULONG initial_count);
```

### <a name="description"></a><span data-ttu-id="9fec9-1493">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1493">Description</span></span>

<span data-ttu-id="9fec9-1494">Bu hizmet, iş parçacıkları arası eşitleme için bir sayım semaforu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1494">This service creates a counting semaphore for inter-thread synchronization.</span></span> <span data-ttu-id="9fec9-1495">İlk semafor sayısı bir giriş parametresi olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1495">The initial semaphore count is specified as an input parameter.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1496">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1496">Parameters</span></span>

- <span data-ttu-id="9fec9-1497">**semaphore_ptr** Semafor denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1497">**semaphore_ptr** Pointer to a semaphore control block.</span></span>
- <span data-ttu-id="9fec9-1498">**name_ptr** Semafor adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1498">**name_ptr** Pointer to the name of the semaphore.</span></span>
- <span data-ttu-id="9fec9-1499">**initial_count** Bu semafor için başlangıç sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1499">**initial_count** Specifies the initial count for this semaphore.</span></span> <span data-ttu-id="9fec9-1500">Yasal değerler 0x00000000 ile 0xFFFFFFFF arasında değişir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1500">Legal values range from 0x00000000 through 0xFFFFFFFF.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1501">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1501">Return Values</span></span>

- <span data-ttu-id="9fec9-1502">**TX_SUCCESS** (0x00) başarılı semafor oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1502">**TX_SUCCESS** (0x00) Successful semaphore creation.</span></span>
- <span data-ttu-id="9fec9-1503">**TX_SEMAPHORE_ERROR** (0x0C) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1503">**TX_SEMAPHORE_ERROR** (0x0C) Invalid semaphore pointer.</span></span> <span data-ttu-id="9fec9-1504">İşaretçi NULL ya da semafor zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1504">Either the pointer is NULL or the semaphore is already created.</span></span>
- <span data-ttu-id="9fec9-1505">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1505">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1506">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1506">Allowed From</span></span>

<span data-ttu-id="9fec9-1507">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-1507">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1508">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1508">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1509">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1509">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1510">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1510">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Create a counting semaphore whose initial value is 1.
This is typically the technique used to make a binary
semaphore. Binary semaphores are used to provide
protection over a common resource. */
status = tx_semaphore_create(&my_semaphore,
    "my_semaphore_name", 1);

/* If status equals TX_SUCCESS, my_semaphore is ready for
use. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1511">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1511">See Also</span></span>

- <span data-ttu-id="9fec9-1512">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1512">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="9fec9-1513">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1513">tx_semaphore_delete</span></span>
- <span data-ttu-id="9fec9-1514">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1514">tx_semaphore_get</span></span>
- <span data-ttu-id="9fec9-1515">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1515">tx_semaphore_info_get</span></span>
- <span data-ttu-id="9fec9-1516">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1516">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1517">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1517">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1518">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1518">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="9fec9-1519">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1519">tx_semaphore_put</span></span>
- <span data-ttu-id="9fec9-1520">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1520">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_delete"></a><span data-ttu-id="9fec9-1521">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1521">tx_semaphore_delete</span></span>

<span data-ttu-id="9fec9-1522">Sayım semaforu Sil</span><span class="sxs-lookup"><span data-stu-id="9fec9-1522">Delete counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1523">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1523">Prototype</span></span>
```c
UINT tx_semaphore_delete(TX_SEMAPHORE *semaphore_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-1524">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1524">Description</span></span>

<span data-ttu-id="9fec9-1525">Bu hizmet, belirtilen sayım semaforu siler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1525">This service deletes the specified counting semaphore.</span></span> <span data-ttu-id="9fec9-1526">Bir semafor örneği için bekleyen askıya alınan tüm iş parçacıkları sürdürülür ve TX_DELETED dönüş durumu verilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1526">All threads suspended waiting for a semaphore instance are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-1527">*Uygulama, semafor silinmeden önce Bu semafor için bir put bildirimi geri çağrısının tamamlandığından (veya devre dışı bırakıldığından) emin olmalıdır. Ayrıca, uygulamanın, silinen semaforun gelecekteki tüm kullanımını önlemesi gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1527">*The application must ensure that a put notify callback for this semaphore is completed (or disabled) before deleting the semaphore. In addition, the application must prevent all future use of a deleted semaphore.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1528">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1528">Parameters</span></span>

- <span data-ttu-id="9fec9-1529">**semaphore_ptr** Daha önce oluşturulmuş bir semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1529">**semaphore_ptr** Pointer to a previously created semaphore.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1530">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1530">Return Values</span></span>

- <span data-ttu-id="9fec9-1531">**TX_SUCCESS** (0x00) semafor silme işlemi başarılı sayılıyor.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1531">**TX_SUCCESS** (0x00) Successful counting semaphore deletion.</span></span>
- <span data-ttu-id="9fec9-1532">**TX_SEMAPHORE_ERROR** (0x0C) geçersiz sayma semaforu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1532">**TX_SEMAPHORE_ERROR** (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="9fec9-1533">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1533">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1534">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1534">Allowed From</span></span>

<span data-ttu-id="9fec9-1535">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-1535">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1536">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1536">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1537">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1537">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1538">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1538">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Delete counting semaphore. Assume that the counting
semaphore has already been created. */
status = tx_semaphore_delete(&my_semaphore);

/* If status equals TX_SUCCESS, the counting semaphore is
deleted. */
```

<span data-ttu-id="9fec9-1539">**Ayrıca bkz.**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1539">**See Also**</span></span>

- <span data-ttu-id="9fec9-1540">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1540">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="9fec9-1541">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1541">tx_semaphore_create</span></span>
- <span data-ttu-id="9fec9-1542">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1542">tx_semaphore_get</span></span>
- <span data-ttu-id="9fec9-1543">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1543">tx_semaphore_info_get</span></span>
- <span data-ttu-id="9fec9-1544">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1544">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1545">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1545">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1546">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1546">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="9fec9-1547">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1547">tx_semaphore_put</span></span>
- <span data-ttu-id="9fec9-1548">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1548">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_get"></a><span data-ttu-id="9fec9-1549">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1549">tx_semaphore_get</span></span>

<span data-ttu-id="9fec9-1550">Sayım semafordan örnek al</span><span class="sxs-lookup"><span data-stu-id="9fec9-1550">Get instance from counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1551">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1551">Prototype</span></span>

```c
UINT tx_semaphore_get(
    TX_SEMAPHORE *semaphore_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="9fec9-1552">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1552">Description</span></span>

<span data-ttu-id="9fec9-1553">Bu hizmet, belirtilen sayım semafordan bir örnek (tek bir sayı) alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1553">This service retrieves an instance (a single count) from the specified counting semaphore.</span></span> <span data-ttu-id="9fec9-1554">Sonuç olarak, belirtilen Semaforun sayısı bir ile azaltılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1554">As a result, the specified semaphore's count is decreased by one.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1555">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1555">Parameters</span></span>

- <span data-ttu-id="9fec9-1556">**semaphore_ptr**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1556">**semaphore_ptr**</span></span> <br><span data-ttu-id="9fec9-1557">Önceden oluşturulmuş bir sayım semaforu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1557">Pointer to a previously created counting semaphore.</span></span>
- <span data-ttu-id="9fec9-1558">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1558">**wait_option**</span></span> <br><span data-ttu-id="9fec9-1559">Semaforun kullanılabilir bir örneği yoksa hizmetin nasıl davranacağını tanımlar; Yani, semafor sayısı sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1559">Defines how the service behaves if there are no instances of the semaphore available; i.e., the semaphore count is zero.</span></span> <span data-ttu-id="9fec9-1560">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="9fec9-1560">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="9fec9-1561">**TX_NO_WAIT** (0x00000000)-TX_NO_WAIT seçilmesi, başarılı olup olmamasına bakılmaksızın bu hizmetten anında geri dönüş sonucunu verir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1561">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="9fec9-1562">*Bu, hizmet iş parçacığından çağrıldığında tek geçerli seçenektir; Örneğin, başlatma, süreölçer veya ıSR.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1562">*This is the only valid option if the service is called from a non-thread; e.g., initialization, timer, or ISR.*</span></span>
  - <span data-ttu-id="9fec9-1563">**TX_WAIT_FOREVER** (0xffffffff)-TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının bir semafor örneği kullanılabilir olana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1563">**TX_WAIT_FOREVER** (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a semaphore instance is available.</span></span>
  - <span data-ttu-id="9fec9-1564">zaman aşımı değeri (0x00000001-0xFFFFFFFE)-sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, bir semafor örneği beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1564">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a semaphore instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1565">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1565">Return Values</span></span>

- <span data-ttu-id="9fec9-1566">**TX_SUCCESS** (0x00) bir semafor örneğinin başarıyla alımı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1566">**TX_SUCCESS** (0x00) Successful retrieval of a semaphore instance.</span></span>
- <span data-ttu-id="9fec9-1567">İş parçacığı askıya alınırken **TX_DELETED** (0x01) sayım semaforu silindi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1567">**TX_DELETED** (0x01) Counting semaphore was deleted while thread was suspended.</span></span>
- <span data-ttu-id="9fec9-1568">**TX_NO_INSTANCE** (0x0D) hizmeti, sayım semaforun bir örneğini alamadı (semafor sayısı, belirtilen süre içinde beklenecek şekilde sıfır).</span><span class="sxs-lookup"><span data-stu-id="9fec9-1568">**TX_NO_INSTANCE** (0x0D) Service was unable to retrieve an instance of the counting semaphore (semaphore count is zero within the specified time to wait).</span></span>
- <span data-ttu-id="9fec9-1569">**TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1569">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="9fec9-1570">**TX_SEMAPHORE_ERROR** (0x0C) geçersiz sayma semaforu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1570">**TX_SEMAPHORE_ERROR** (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="9fec9-1571">**TX_WAIT_ERROR** (0x04) TX_NO_WAIT dışında bir bekleme seçeneği, iş parçacığından oluşan bir çağrıda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1571">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1572">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1572">Allowed From</span></span>

<span data-ttu-id="9fec9-1573">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1573">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1574">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1574">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1575">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1575">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1576">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1576">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Get a semaphore instance from the semaphore
"my_semaphore." If the semaphore count is zero,
suspend until an instance becomes available.
Note that this suspension is only possible from
application threads. */
status = tx_semaphore_get(&my_semaphore, TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the thread has obtained
an instance of the semaphore. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1577">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1577">See Also</span></span>

- <span data-ttu-id="9fec9-1578">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1578">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="9fec9-1579">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1579">tx_semaphore_create</span></span>
- <span data-ttu-id="9fec9-1580">tx_semahore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1580">tx_semahore_delete</span></span>
- <span data-ttu-id="9fec9-1581">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1581">tx_semaphore_info_get</span></span>
- <span data-ttu-id="9fec9-1582">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1582">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1583">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1583">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="9fec9-1584">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1584">tx_semaphore_put</span></span>
- <span data-ttu-id="9fec9-1585">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1585">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_info_get"></a><span data-ttu-id="9fec9-1586">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1586">tx_semaphore_info_get</span></span>

<span data-ttu-id="9fec9-1587">Semafor hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="9fec9-1587">Retrieve information about semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1588">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1588">Prototype</span></span>

```c
UINT tx_semaphore_info_get(
    TX_SEMAPHORE *semaphore_ptr,
    CHAR **name, ULONG *current_value,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_SEMAPHORE **next_semaphore);
```

### <a name="description"></a><span data-ttu-id="9fec9-1589">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1589">Description</span></span>

<span data-ttu-id="9fec9-1590">Bu hizmet belirtilen semafor hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1590">This service retrieves information about the specified semaphore.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1591">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1591">Parameters</span></span>

- <span data-ttu-id="9fec9-1592">**semaphore_ptr** Semafor denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1592">**semaphore_ptr** Pointer to semaphore control block.</span></span>
- <span data-ttu-id="9fec9-1593">**ad** Semafor adı işaretçisinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1593">**name** Pointer to destination for the pointer to the semaphore's name.</span></span>
- <span data-ttu-id="9fec9-1594">**Current_value** Geçerli semafor sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1594">**current_value** Pointer to destination for the current semaphore's count.</span></span>
- <span data-ttu-id="9fec9-1595">**first_suspended** Bu semaforun askıya alma listesindeki iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1595">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this semaphore.</span></span>
- <span data-ttu-id="9fec9-1596">**suspended_count** Bu semaforda Şu anda askıya alınan iş parçacığı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1596">**suspended_count** Pointer to destination for the number of threads currently suspended on this semaphore.</span></span>
- <span data-ttu-id="9fec9-1597">**next_semaphore** Sonraki oluşturulan semaforun işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1597">**next_semaphore** Pointer to destination for the pointer of the next created semaphore.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1598">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1598">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1599">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1599">Return Values</span></span>

- <span data-ttu-id="9fec9-1600">**TX_SUCCESS** (0x00) bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1600">**TX_SUCCESS** (0x00) information retrieval.</span></span>

- <span data-ttu-id="9fec9-1601">**TX_SEMAPHORE_ERROR** (0x0C) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1601">**TX_SEMAPHORE_ERROR** (0x0C) Invalid semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1602">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1602">Allowed From</span></span>

<span data-ttu-id="9fec9-1603">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1603">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1604">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1604">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1605">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1605">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1606">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1606">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
CHAR *name;
ULONG current_value;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_SEMAPHORE *next_semaphore;
UINT status;

/* Retrieve information about the previously created
semaphore "my_semaphore." */
status = tx_semaphore_info_get(&my_semaphore, &name,
    &current_value,
    &first_suspended, &suspended_count,
    &next_semaphore);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1607">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1607">See Also</span></span>

- <span data-ttu-id="9fec9-1608">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1608">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="9fec9-1609">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1609">tx_semaphore_create</span></span>
- <span data-ttu-id="9fec9-1610">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1610">tx_semaphore_delete</span></span>
- <span data-ttu-id="9fec9-1611">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1611">tx_semaphore_get</span></span>
- <span data-ttu-id="9fec9-1612">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1612">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1613">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1613">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1614">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1614">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="9fec9-1615">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1615">tx_semaphore_put</span></span>
- <span data-ttu-id="9fec9-1616">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1616">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_performance_info_get"></a><span data-ttu-id="9fec9-1617">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1617">tx_semaphore_performance_info_get</span></span>

<span data-ttu-id="9fec9-1618">Semafor performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-1618">Get semaphore performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1619">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1619">Prototype</span></span>

```c
UINT tx_semaphore_performance_info_get(
    TX_SEMAPHORE *semaphore_ptr,
    ULONG *puts, 
    ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="9fec9-1620">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1620">Description</span></span>

<span data-ttu-id="9fec9-1621">Bu hizmet, belirtilen semafor hakkında performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1621">This service retrieves performance information about the specified semaphore.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-1622">*Işparçacığıx kitaplığı ve uygulaması ile*  \* oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1622">*The ThreadX library and application must be built with* ***TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

<span data-ttu-id="9fec9-1623">**Parametreler**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1623">**Parameters**</span></span>

-  <span data-ttu-id="9fec9-1624">**semaphore_ptr** Daha önce oluşturulan semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1624">**semaphore_ptr** Pointer to previously created semaphore.</span></span>
-  <span data-ttu-id="9fec9-1625">**koyar** Bu semafor üzerinde gerçekleştirilen PUT isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1625">**puts** Pointer to destination for the number of put requests performed on this semaphore.</span></span>
-  <span data-ttu-id="9fec9-1626">**alır** Bu semafor üzerinde gerçekleştirilen GET isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1626">**gets** Pointer to destination for the number of get requests performed on this semaphore.</span></span>
-  <span data-ttu-id="9fec9-1627">**getirilmesi** Bu semaforda iş parçacığı getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1627">**suspensions** Pointer to destination for the number of thread suspensions on this semaphore.</span></span>
-  <span data-ttu-id="9fec9-1628">**zaman aşımları** Bu semaforda iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1628">**timeouts** Pointer to destination for the number of thread suspension timeouts on this semaphore.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1629">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1629">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1630">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1630">Return Values</span></span>

- <span data-ttu-id="9fec9-1631">**TX_SUCCESS** (0x00) başarılı semafor performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1631">**TX_SUCCESS** (0x00) Successful semaphore performance get.</span></span>
- <span data-ttu-id="9fec9-1632">**TX_PTR_ERROR** (0x03) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1632">**TX_PTR_ERROR** (0x03) Invalid semaphore pointer.</span></span>
- <span data-ttu-id="9fec9-1633">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1633">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1634">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1634">Allowed From</span></span>

<span data-ttu-id="9fec9-1635">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1635">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1636">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1636">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created
semaphore. */
status = tx_semaphore_performance_info_get(&my_semaphore, &puts,
    &gets, &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1637">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1637">See Also</span></span>

- <span data-ttu-id="9fec9-1638">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1638">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="9fec9-1639">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1639">tx_semaphore_create</span></span>
- <span data-ttu-id="9fec9-1640">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1640">tx_semaphore_delete</span></span>
- <span data-ttu-id="9fec9-1641">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1641">tx_semaphore_get</span></span>
- <span data-ttu-id="9fec9-1642">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1642">tx_semaphore_info_get</span></span>
- <span data-ttu-id="9fec9-1643">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1643">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1644">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1644">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="9fec9-1645">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1645">tx_semaphore_put</span></span>
- <span data-ttu-id="9fec9-1646">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1646">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_performance_system_info_get"></a><span data-ttu-id="9fec9-1647">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1647">tx_semaphore_performance_system_info_get</span></span>

<span data-ttu-id="9fec9-1648">Semafor sistem performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-1648">Get semaphore system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1649">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1649">Prototype</span></span>

```c
UINT tx_semaphore_performance_system_info_get(
    ULONG *puts,
    ULONG *gets, 
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="9fec9-1650">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1650">Description</span></span>

<span data-ttu-id="9fec9-1651">Bu hizmet sistemdeki tüm Semaforlar hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1651">This service retrieves performance information about all the semaphores in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-1652">*Işparçacığıx kitaplığı ve uygulaması ile*  \* oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1652">*The ThreadX library and application must be built with* ***TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1653">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1653">Parameters</span></span>

- <span data-ttu-id="9fec9-1654">**koyar** Tüm Semaforlarda gerçekleştirilen put isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1654">**puts** Pointer to destination for the total number of put requests performed on all semaphores.</span></span>
- <span data-ttu-id="9fec9-1655">**alır** Tüm Semaforlarda gerçekleştirilen GET isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1655">**gets** Pointer to destination for the total number of get requests performed on all semaphores.</span></span>
- <span data-ttu-id="9fec9-1656">**getirilmesi** Tüm Semaforlarda toplam iş parçacığı getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1656">**suspensions** Pointer to destination for the total number of thread suspensions on all semaphores.</span></span>
- <span data-ttu-id="9fec9-1657">**zaman aşımları** Tüm Semaforlarda toplam iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1657">**timeouts** Pointer to destination for the total number of thread suspension timeouts on all semaphores.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1658">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1658">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1659">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1659">Return Values</span></span>

- <span data-ttu-id="9fec9-1660">**TX_SUCCESS** (0x00) sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1660">**TX_SUCCESS** (0x00) system performance get.</span></span>
- <span data-ttu-id="9fec9-1661">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1661">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1662">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1662">Allowed From</span></span>

<span data-ttu-id="9fec9-1663">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1663">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1664">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1664">Example</span></span>

```c
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on all previously created
semaphores. */
status = tx_semaphore_performance_system_info_get(&puts, &gets,
    &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1665">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1665">See Also</span></span>

- <span data-ttu-id="9fec9-1666">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1666">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="9fec9-1667">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1667">tx_semaphore_create</span></span>
- <span data-ttu-id="9fec9-1668">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1668">tx_semaphore_delete</span></span>
- <span data-ttu-id="9fec9-1669">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1669">tx_semaphore_get</span></span>
- <span data-ttu-id="9fec9-1670">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1670">tx_semaphore_info_get</span></span>
- <span data-ttu-id="9fec9-1671">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1671">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1672">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1672">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="9fec9-1673">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1673">tx_semaphore_put</span></span>
- <span data-ttu-id="9fec9-1674">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1674">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_prioritize"></a><span data-ttu-id="9fec9-1675">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1675">tx_semaphore_prioritize</span></span>

<span data-ttu-id="9fec9-1676">Semafor askıya alma listesini önceliklendir</span><span class="sxs-lookup"><span data-stu-id="9fec9-1676">Prioritize semaphore suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1677">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1677">Prototype</span></span>

```c
UINT tx_semaphore_prioritize(TX_SEMAPHORE *semaphore_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-1678">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1678">Description</span></span>

<span data-ttu-id="9fec9-1679">Bu hizmet, askıya alma listesinin önündeki semafor örneği için askıya alınan en yüksek öncelik iş parçacığını koyar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1679">This service places the highest priority thread suspended for an instance of the semaphore at the front of the suspension list.</span></span> <span data-ttu-id="9fec9-1680">Diğer tüm iş parçacıkları ' de askıya alındığı FıFO sırasında kalır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1680">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1681">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1681">Parameters</span></span>

- <span data-ttu-id="9fec9-1682">**semaphore_ptr** Daha önce oluşturulmuş bir semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1682">**semaphore_ptr** Pointer to a previously created semaphore.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1683">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1683">Return Values</span></span>

- <span data-ttu-id="9fec9-1684">**TX_SUCCESS** (0x00) başarılı semafor önceliği belirleme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1684">**TX_SUCCESS** (0x00) Successful semaphore prioritize.</span></span>
- <span data-ttu-id="9fec9-1685">**TX_SEMAPHORE_ERROR** (0x0C) geçersiz sayma semaforu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1685">**TX_SEMAPHORE_ERROR** (0x0C) Invalid counting semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1686">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1686">Allowed From</span></span>

<span data-ttu-id="9fec9-1687">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1687">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1688">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1688">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1689">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1689">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1690">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1690">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Ensure that the highest priority thread will receive
the next instance of this semaphore. */
status = tx_semaphore_prioritize(&my_semaphore);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_semaphore_put call made to this semaphore will
wake up this thread. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1691">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1691">See Also</span></span>

- <span data-ttu-id="9fec9-1692">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1692">tx_semaphore_create</span></span>
- <span data-ttu-id="9fec9-1693">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1693">tx_semaphore_delete</span></span>
- <span data-ttu-id="9fec9-1694">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1694">tx_semaphore_get</span></span>
- <span data-ttu-id="9fec9-1695">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1695">tx_semaphore_info_get</span></span>
- <span data-ttu-id="9fec9-1696">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1696">tx_semaphore_put</span></span>

## <a name="tx_semaphore_put"></a><span data-ttu-id="9fec9-1697">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1697">tx_semaphore_put</span></span>

<span data-ttu-id="9fec9-1698">Sayım semafora bir örnek yerleştirme</span><span class="sxs-lookup"><span data-stu-id="9fec9-1698">Place an instance in counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1699">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1699">Prototype</span></span>

```c
UINT tx_semaphore_put(TX_SEMAPHORE *semaphore_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-1700">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1700">Description</span></span>

<span data-ttu-id="9fec9-1701">Bu hizmet, gerçekte belirtilen sayım semafora bir örnek koyar ve bu da gerçekteki sayım semaforu bir tane artırır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1701">This service puts an instance into the specified counting semaphore, which in reality increments the counting semaphore by one.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1702">*Semaforun hepsi (OxFFFFFFFF) olduğunda bu hizmet çağrılırsa, yeni PUT işlemi semaforun sıfıra sıfırlanmasına neden olur.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1702">*If this service is called when the semaphore is all ones (OxFFFFFFFF), the new put operation will cause the semaphore to be reset to zero.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1703">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1703">Parameters</span></span>

- <span data-ttu-id="9fec9-1704">**semaphore_ptr** Önceden oluşturulan sayım semaforu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1704">**semaphore_ptr** Pointer to the previously created counting semaphore control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1705">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1705">Return Values</span></span>

- <span data-ttu-id="9fec9-1706">**TX_SUCCESS** (0x00) başarılı semafor put.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1706">**TX_SUCCESS** (0x00) Successful semaphore put.</span></span>
- <span data-ttu-id="9fec9-1707">**TX_SEMAPHORE_ERROR** (0x0C) semaforu saymak için geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1707">**TX_SEMAPHORE_ERROR** (0x0C) Invalid pointer to counting semaphore.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1708">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1708">Allowed From</span></span>

<span data-ttu-id="9fec9-1709">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1709">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1710">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1710">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1711">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1711">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1712">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1712">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Increment the counting semaphore "my_semaphore." */
status = tx_semaphore_put(&my_semaphore);

/* If status equals TX_SUCCESS, the semaphore count has
been incremented. Of course, if a thread was waiting,
it was given the semaphore instance and resumed. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1713">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1713">See Also</span></span>

- <span data-ttu-id="9fec9-1714">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1714">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="9fec9-1715">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1715">tx_semaphore_create</span></span>
- <span data-ttu-id="9fec9-1716">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1716">tx_semaphore_delete</span></span>
- <span data-ttu-id="9fec9-1717">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1717">tx_semaphore_info_get</span></span>
- <span data-ttu-id="9fec9-1718">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1718">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1719">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1719">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1720">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1720">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="9fec9-1721">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1721">tx_semaphore_get</span></span>
- <span data-ttu-id="9fec9-1722">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1722">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_put_notify"></a><span data-ttu-id="9fec9-1723">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1723">tx_semaphore_put_notify</span></span>

<span data-ttu-id="9fec9-1724">Semafor yerleştirayarlandığında uygulamaya bildir</span><span class="sxs-lookup"><span data-stu-id="9fec9-1724">Notify application when semaphore is put</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1725">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1725">Prototype</span></span>

```c
UINT tx_semaphore_put_notify(
    TX_SEMAPHORE *semaphore_ptr,
    VOID (*semaphore_put_notify)(TX_SEMAPHORE *));
```

### <a name="description"></a><span data-ttu-id="9fec9-1726">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1726">Description</span></span>

<span data-ttu-id="9fec9-1727">Bu hizmet, belirtilen semafor her gerçekleştiğinde çağrılan bir bildirim geri çağırma işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1727">This service registers a notification callback function that is called whenever the specified semaphore is put.</span></span> <span data-ttu-id="9fec9-1728">Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1728">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1729">*Uygulamanın semafor bildirimi geri çağrısının askıya alma seçeneği ile herhangi bir ThreadX API çağrısı yapılmasına izin verilmez.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1729">*The application's semaphore notification callback is not allowed to call any ThreadX API with a suspension option.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1730">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1730">Parameters</span></span>

- <span data-ttu-id="9fec9-1731">**semaphore_ptr** Daha önce oluşturulan semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1731">**semaphore_ptr** Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="9fec9-1732">**semaphore_put_notify** Uygulamanın semafor put bildirimi işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1732">**semaphore_put_notify** Pointer to application's semaphore put notification function.</span></span> <span data-ttu-id="9fec9-1733">Bu değer TX_NULL, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1733">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1734">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1734">Return Values</span></span>

- <span data-ttu-id="9fec9-1735">**TX_SUCCESS** (0x00) semafor put bildiriminin başarıyla kaydı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1735">**TX_SUCCESS** (0x00) Successful registration of semaphore put notification.</span></span>
- <span data-ttu-id="9fec9-1736">**TX_SEMAPHORE_ERROR** (0x0C) geçersiz semafor işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1736">**TX_SEMAPHORE_ERROR** (0x0C) Invalid semaphore pointer.</span></span>
- <span data-ttu-id="9fec9-1737">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem bildirim özellikleri devre dışı olarak derlendi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1737">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1738">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1738">Allowed From</span></span>

<span data-ttu-id="9fec9-1739">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1739">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1740">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1740">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;

/* Register the "my_semaphore_put_notify" function for monitoring
the put operations on the semaphore "my_semaphore." */
status = tx_semaphore_put_notify(&my_semaphore, my_semaphore_put_notify);

/* If status is TX_SUCCESS the semaphore put notification function
was successfully registered. */
void my_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr)
{
    /* The semaphore was just put! */
}
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1741">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1741">See Also</span></span>

- <span data-ttu-id="9fec9-1742">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1742">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="9fec9-1743">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1743">tx_semaphore_create</span></span>
- <span data-ttu-id="9fec9-1744">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1744">tx_semaphore_delete</span></span>
- <span data-ttu-id="9fec9-1745">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1745">tx_semaphore_get</span></span>
- <span data-ttu-id="9fec9-1746">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1746">tx_semaphore_info_get</span></span>
- <span data-ttu-id="9fec9-1747">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1747">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1748">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1748">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1749">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="9fec9-1749">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="9fec9-1750">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="9fec9-1750">tx_semaphore_put</span></span>

## <a name="tx_thread_create"></a><span data-ttu-id="9fec9-1751">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1751">tx_thread_create</span></span>

<span data-ttu-id="9fec9-1752">Uygulama iş parçacığı oluştur</span><span class="sxs-lookup"><span data-stu-id="9fec9-1752">Create application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1753">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1753">Prototype</span></span>

```c
UINT tx_thread_create(
    TX_THREAD *thread_ptr,
    CHAR *name_ptr, 
    VOID (*entry_function)(ULONG),
    ULONG entry_input, 
    VOID *stack_start,
    ULONG stack_size, 
    UINT priority,
    UINT preempt_threshold, 
    ULONG time_slice,
    UINT auto_start);
```

### <a name="description"></a><span data-ttu-id="9fec9-1754">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1754">Description</span></span>

<span data-ttu-id="9fec9-1755">Bu hizmet, belirtilen görev girişi işlevinde yürütmeyi Başlatan bir uygulama iş parçacığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1755">This service creates an application thread that starts execution at the specified task entry function.</span></span> <span data-ttu-id="9fec9-1756">Yığın, öncelik, önalım-Threshold ve zaman dilimi, giriş parametreleri tarafından belirtilen özniteliklerin arasındadır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1756">The stack, priority, preemption-threshold, and time-slice are among the attributes specified by the input parameters.</span></span> <span data-ttu-id="9fec9-1757">Ayrıca, iş parçacığının ilk yürütme durumu da belirtilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1757">In addition, the initial execution state of the thread is also specified.</span></span>

<span data-ttu-id="9fec9-1758">**Parametreler**</span><span class="sxs-lookup"><span data-stu-id="9fec9-1758">**Parameters**</span></span>

- <span data-ttu-id="9fec9-1759">**thread_ptr** İş parçacığı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1759">**thread_ptr** Pointer to a thread control block.</span></span>
- <span data-ttu-id="9fec9-1760">**name_ptr** İş parçacığının adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1760">**name_ptr** Pointer to the name of the thread.</span></span>
- <span data-ttu-id="9fec9-1761">**entry_function** İş parçacığı yürütmesi için ilk C işlevini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1761">**entry_function** Specifies the initial C function for thread execution.</span></span> <span data-ttu-id="9fec9-1762">Bir iş parçacığı bu giriş işlevinden döndüğünde, *tamamlanmış* bir duruma konur ve süresiz olarak askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1762">When a thread returns from this entry function, it is placed in a *completed* state and suspended indefinitely.</span></span>
- <span data-ttu-id="9fec9-1763">**entry_input** İlk yürütüldüğünde iş parçacığının giriş işlevine geçirilen 32 bitlik bir değer.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1763">**entry_input** A 32-bit value that is passed to the thread's entry function when it first executes.</span></span> <span data-ttu-id="9fec9-1764">Bu giriş için kullanım, uygulama tarafından özel olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1764">The use for this input is determined exclusively by the application.</span></span>
- <span data-ttu-id="9fec9-1765">**stack_start** Yığının bellek alanının başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1765">**stack_start** Starting address of the stack's memory area.</span></span>
- <span data-ttu-id="9fec9-1766">**stack_size** Yığın bellek alanındaki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1766">**stack_size** Number bytes in the stack memory area.</span></span> <span data-ttu-id="9fec9-1767">İş parçacığının yığın alanı, en kötü durum işlevi çağrı iç içe ve yerel değişken kullanımını işleyecek kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1767">The thread's stack area must be large enough to handle its worst-case function call nesting and local variable usage.</span></span>
- <span data-ttu-id="9fec9-1768">**Öncelik** İş parçacığının sayısal önceliği.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1768">**priority** Numerical priority of thread.</span></span> <span data-ttu-id="9fec9-1769">Geçerli değerler 0 ile (TX_MAX_PRIORITES-1) arasındadır; burada 0 değeri, en yüksek önceliği temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1769">Legal values range from 0 through (TX_MAX_PRIORITES-1), where a value of 0 represents the highest priority.</span></span>
- <span data-ttu-id="9fec9-1770">**preempt_threshold** Devre dışı önalım en yüksek öncelik düzeyi (0 ila (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="9fec9-1770">**preempt_threshold** Highest priority level (0 through (TX_MAX_PRIORITIES-1)) of disabled preemption.</span></span> <span data-ttu-id="9fec9-1771">Bu iş parçacığını yalnızca bu düzeyden daha yüksek öncelikler için izin verilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1771">Only priorities higher than this level are allowed to preempt this thread.</span></span> <span data-ttu-id="9fec9-1772">Bu değer, belirtilen önceliğe eşit veya ondan küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1772">This value must be less than or equal to the specified priority.</span></span> <span data-ttu-id="9fec9-1773">İş parçacığı önceliğine eşit bir değer önalım eşiğini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1773">A value equal to the thread priority disables preemption-threshold.</span></span>
- <span data-ttu-id="9fec9-1774">**time_slice** Aynı önceliğe sahip diğer hazırlık iş parçacıklarıyla çalışma şansı verilmeye başlamadan önce bu iş parçacığının çalışmasına izin verilen zamanlayıcı sayısı-işaretleri.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1774">**time_slice** Number of timer-ticks this thread is allowed to run before other ready threads of the same priority are given a chance to run.</span></span> <span data-ttu-id="9fec9-1775">Önalım-Threshold kullanmanın zaman dilimini devre dışı bıraktığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1775">Note that using preemption-threshold disables time-slicing.</span></span> <span data-ttu-id="9fec9-1776">Yasal zaman dilimi değerleri 1 ile 0xFFFFFFFF (dahil) arasındadır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1776">Legal time-slice values range from 1 to 0xFFFFFFFF (inclusive).</span></span> <span data-ttu-id="9fec9-1777">**TX_NO_TIME_SLICE** değeri (0 değeri), bu iş parçacığının zaman dilimzamanını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1777">A value of **TX_NO_TIME_SLICE** (a value of 0) disables time-slicing of this thread.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9fec9-1778">*Zaman dilimletmek, daha hafif bir sistem yükü miktarına neden olur.   Zaman dilimi yalnızca birden çok iş parçacığının aynı önceliğe sahip olduğu durumlarda faydalıdır, benzersiz önceliğe sahip iş parçacıkları zaman dilimi atanmamalıdır.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1778">*Using time-slicing results in a slight amount of system overhead.   Since time-slicing is only useful in cases where multiple threads   share the same priority, threads having a unique priority should not   be assigned a time-slice.*</span></span>

- <span data-ttu-id="9fec9-1779">**auto_start** İş parçacığının hemen başlatılıp başlatılmayacağını veya askıya alınma durumuna yerleştirilip yerleştirilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1779">**auto_start** Specifies whether the thread starts immediately or is placed in a suspended state.</span></span> <span data-ttu-id="9fec9-1780">Yasal seçenekler **TX_AUTO_START** (0x01) ve **TX_DONT_START** (0x00).</span><span class="sxs-lookup"><span data-stu-id="9fec9-1780">Legal options are **TX_AUTO_START** (0x01) and **TX_DONT_START** (0x00).</span></span> <span data-ttu-id="9fec9-1781">TX_DONT_START belirtilirse, uygulamanın iş parçacığının çalışması için daha sonra tx_thread_resume çağırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1781">If TX_DONT_START is specified, the application must later call tx_thread_resume in order for the thread to run.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1782">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1782">Return Values</span></span>

- <span data-ttu-id="9fec9-1783">**TX_SUCCESS** (0x00) başarılı iş parçacığı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1783">**TX_SUCCESS** (0x00) Successful thread creation.</span></span>
- <span data-ttu-id="9fec9-1784">**TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı denetim işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1784">**TX_THREAD_ERROR** (0x0E) Invalid thread control pointer.</span></span> <span data-ttu-id="9fec9-1785">İşaretçi NULL ya da iş parçacığı zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1785">Either the pointer is NULL or the thread is already created.</span></span>
- <span data-ttu-id="9fec9-1786">**TX_PTR_ERROR** (0x03) giriş noktasının başlangıç adresi geçersiz veya yığın alanı geçersiz, genellikle null.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1786">**TX_PTR_ERROR** (0x03) Invalid starting address of the entry point or the stack area is invalid, usually NULL.</span></span>
- <span data-ttu-id="9fec9-1787">**TX_SIZE_ERROR** (0x05) yığın alanının boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1787">**TX_SIZE_ERROR** (0x05) Size of stack area is invalid.</span></span> <span data-ttu-id="9fec9-1788">İş parçacıklarının yürütülmesi için en az **TX_MINIMUM_STACK** bayt olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1788">Threads must have at least **TX_MINIMUM_STACK** bytes to execute.</span></span>
- <span data-ttu-id="9fec9-1789">**TX_PRIORITY_ERROR** (0X0f) geçersiz iş parçacığı önceliği (0-(TX_MAX_PRIORITIES-1) aralığı dışında bir değer.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1789">**TX_PRIORITY_ERROR** (0x0F) Invalid thread priority, which is a value outside the range of (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="9fec9-1790">**TX_THRESH_ERROR** (0x18) geçersiz preemptionthreshold belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1790">**TX_THRESH_ERROR** (0x18) Invalid preemptionthreshold specified.</span></span> <span data-ttu-id="9fec9-1791">Bu değer, iş parçacığının ilk önceliğine eşit veya ondan küçük geçerli bir öncelik olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1791">This value must be a valid priority less than or equal to the initial priority of the thread.</span></span>
- <span data-ttu-id="9fec9-1792">**TX_START_ERROR** (0x10) geçersiz otomatik başlatma seçimi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1792">**TX_START_ERROR** (0x10) Invalid auto-start selection.</span></span>
- <span data-ttu-id="9fec9-1793">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1793">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1794">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1794">Allowed From</span></span>

<span data-ttu-id="9fec9-1795">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-1795">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1796">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1796">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1797">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-1797">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1798">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1798">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Create a thread of priority 15 whose entry point is
"my_thread_entry". This thread’s stack area is 1000
bytes in size, starting at address 0x400000. The
preemption-threshold is setup to allow preemption of threads
with priorities ranging from 0 through 14. Time-slicing is
disabled. This thread is automatically put into a ready
condition. */
status = tx_thread_create(&my_thread, "my_thread_name",
    my_thread_entry, 0x1234,
    (VOID *) 0x400000, 1000,
    15, 15, TX_NO_TIME_SLICE,
    TX_AUTO_START);

/* If status equals TX_SUCCESS, my_thread is ready
for execution! */

...

/* Thread’s entry function. When "my_thread" actually
begins execution, control is transferred to this
function. */

VOID my_thread_entry (ULONG initial_input)
{
    /* When we get here, the value of initial_input is
    0x1234. See how this was specified during
    creation. */
    /* The real work of the thread, including calls to
    other function should be called from here! */
    /* When this function returns, the corresponding
    thread is placed into a "completed" state. */
}
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1799">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1799">See Also</span></span>

- <span data-ttu-id="9fec9-1800">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1800">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-1801">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1801">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-1802">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1802">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-1803">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1803">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-1804">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1804">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1805">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1805">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1806">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1806">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-1807">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1807">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-1808">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-1808">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-1809">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-1809">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-1810">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-1810">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-1811">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-1811">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-1812">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1812">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-1813">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-1813">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-1814">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-1814">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-1815">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1815">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-1816">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-1816">tx_thread_wait_abort</span></span>

## <a name="tx_thread_delete"></a><span data-ttu-id="9fec9-1817">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1817">tx_thread_delete</span></span>

<span data-ttu-id="9fec9-1818">Uygulama iş parçacığını Sil</span><span class="sxs-lookup"><span data-stu-id="9fec9-1818">Delete application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1819">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1819">Prototype</span></span>

```c
UINT tx_thread_delete(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-1820">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1820">Description</span></span>

<span data-ttu-id="9fec9-1821">Bu hizmet, belirtilen uygulama iş parçacığını siler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1821">This service deletes the specified application thread.</span></span> <span data-ttu-id="9fec9-1822">Belirtilen iş parçacığının sonlandırılmış veya tamamlanmış durumda olması gerektiğinden, bu hizmet kendisini silmeye çalışan bir iş parçacığından çağrılamaz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1822">Since the specified thread must be in a terminated or completed state, this service cannot be called from a thread attempting to delete itself.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1823">*Bu hizmet tamamlandıktan sonra kullanılabilir olan iş parçacığının yığınında ilişkili bellek alanını yönetmek uygulamanın sorumluluğundadır. Ayrıca, uygulamanın silinen bir iş parçacığının kullanımını önlemesi gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1823">*It is the application's responsibility to manage the memory area associated with the thread's stack, which is available after this service completes. In addition, the application must prevent use of a deleted thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1824">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1824">Parameters</span></span>

- <span data-ttu-id="9fec9-1825">**thread_ptr** Daha önce oluşturulmuş bir uygulama iş parçacığına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1825">**thread_ptr** Pointer to a previously created application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1826">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1826">Return Values</span></span>

- <span data-ttu-id="9fec9-1827">**TX_SUCCESS** (0x00) başarılı iş parçacığı silme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1827">**TX_SUCCESS** (0x00) Successful thread deletion.</span></span>
- <span data-ttu-id="9fec9-1828">**TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1828">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="9fec9-1829">**TX_DELETE_ERROR** (0x11) belirtilen iş parçacığı sonlandırılmış veya tamamlanmış durumda değil.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1829">**TX_DELETE_ERROR** (0x11) Specified thread is not in a terminated or completed state.</span></span>
- <span data-ttu-id="9fec9-1830">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1830">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1831">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1831">Allowed From</span></span>

<span data-ttu-id="9fec9-1832">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="9fec9-1832">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1833">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1833">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1834">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1834">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1835">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1835">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Delete an application thread whose control block is
"my_thread". Assume that the thread has already been
created with a call to tx_thread_create. */
status = tx_thread_delete(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1836">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1836">See Also</span></span>

- <span data-ttu-id="9fec9-1837">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1837">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-1838">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1838">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-1839">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1839">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-1840">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1840">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-1841">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1841">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1842">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1842">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1843">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1843">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-1844">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1844">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-1845">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-1845">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-1846">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-1846">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-1847">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-1847">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-1848">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-1848">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-1849">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1849">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-1850">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-1850">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-1851">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-1851">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-1852">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1852">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-1853">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-1853">tx_thread_wait_abort</span></span>

## <a name="tx_thread_entry_exit_notify"></a><span data-ttu-id="9fec9-1854">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1854">tx_thread_entry_exit_notify</span></span>

<span data-ttu-id="9fec9-1855">İş parçacığı girdisi ve çıkış sonrasında uygulamayı bilgilendir</span><span class="sxs-lookup"><span data-stu-id="9fec9-1855">Notify application upon thread entry and exit</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1856">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1856">Prototype</span></span>

```c
UINT tx_thread_entry_exit_notify(
    TX_THREAD *thread_ptr,
    VOID (*entry_exit_notify)(TX_THREAD *, UINT));
```

### <a name="description"></a><span data-ttu-id="9fec9-1857">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1857">Description</span></span>

<span data-ttu-id="9fec9-1858">Bu hizmet, belirtilen iş parçacığı girildiğinde veya çıktığında çağrılan bir bildirim geri arama işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1858">This service registers a notification callback function that is called whenever the specified thread is entered or exits.</span></span> <span data-ttu-id="9fec9-1859">Bildirim geri çağrısının işlenmesi uygulama tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1859">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1860">Uygulamanın iş parçacığı giriş/çıkış bildirimi geri çağrısının askıya alma seçeneği ile herhangi bir ThreadX API çağrısı yapılmasına izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1860">The application's thread entry/exit notification callback is not allowed to call any ThreadX API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1861">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1861">Parameters</span></span>

- <span data-ttu-id="9fec9-1862">**thread_ptr** Daha önce oluşturulmuş iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1862">**thread_ptr** Pointer to previously created thread.</span></span>
- <span data-ttu-id="9fec9-1863">**entry_exit_notify** Uygulamanın iş parçacığı giriş/çıkış bildirimi işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1863">**entry_exit_notify** Pointer to application's thread entry/exit notification function.</span></span> <span data-ttu-id="9fec9-1864">Giriş/çıkış bildirimi işlevinin ikinci parametresi, bir giriş veya çıkış varsa belirler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1864">The second parameter to the entry/exit notification function designates if an entry or exit is present.</span></span> <span data-ttu-id="9fec9-1865">**TX_THREAD_ENTRY** (0x00) değeri, iş parçacığının girildiğini belirtir, ancak değer **TX_THREAD_EXIT** (0x01), iş parçacığının çıkış olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1865">The value **TX_THREAD_ENTRY** (0x00) indicates the thread was entered, while the value **TX_THREAD_EXIT** (0x01) indicates the thread was exited.</span></span> <span data-ttu-id="9fec9-1866">Bu değer **TX_NULL**, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1866">If this value is **TX_NULL**, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1867">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1867">Return Values</span></span>

- <span data-ttu-id="9fec9-1868">**TX_SUCCESS** (0x00) iş parçacığı giriş/çıkış bildirimi işlevinin başarıyla kaydı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1868">**TX_SUCCESS** (0x00) Successful registration of the thread entry/exit notification function.</span></span>
- <span data-ttu-id="9fec9-1869">**TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1869">**TX_THREAD_ERROR** (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="9fec9-1870">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem bildirim özellikleri devre dışı olarak derlendi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1870">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1871">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1871">Allowed From</span></span>

<span data-ttu-id="9fec9-1872">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1872">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1873">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1873">Example</span></span>

```c
TX_THREAD my_thread;
/* Register the "my_entry_exit_notify" function for monitoring
the entry/exit of the thread "my_thread." */
status = tx_thread_entry_exit_notify(&my_thread,
    my_entry_exit_notify);

/* If status is TX_SUCCESS the entry/exit notification function was
successfully registered. */
void my_entry_exit_notify(TX_THREAD *thread_ptr, UINT condition)
{
    /* Determine if the thread was entered or exited. */
    if (condition == TX_THREAD_ENTRY)
        /* Thread entry! */
    else if (condition == TX_THREAD_EXIT)
        /* Thread exit! */
}
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1874">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1874">See Also</span></span>

- <span data-ttu-id="9fec9-1875">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1875">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-1876">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1876">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-1877">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1877">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-1878">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1878">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-1879">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1879">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-1880">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1880">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1881">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1881">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1882">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1882">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-1883">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1883">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-1884">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-1884">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-1885">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-1885">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-1886">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-1886">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-1887">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-1887">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-1888">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1888">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-1889">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-1889">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-1890">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-1890">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-1891">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1891">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-1892">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-1892">tx_thread_wait_abort</span></span>

## <a name="tx_thread_identify"></a><span data-ttu-id="9fec9-1893">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1893">tx_thread_identify</span></span>

<span data-ttu-id="9fec9-1894">Şu anda yürütülmekte olan iş parçacığına olan işaretçiyi alır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1894">Retrieves pointer to currently executing thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1895">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1895">Prototype</span></span>

```c
TX_THREAD* tx_thread_identify(VOID);
```
### <a name="description"></a><span data-ttu-id="9fec9-1896">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1896">Description</span></span>

<span data-ttu-id="9fec9-1897">Bu hizmet şu anda yürütülmekte olan iş parçacığına bir işaretçi döndürür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1897">This service returns a pointer to the currently executing thread.</span></span> <span data-ttu-id="9fec9-1898">İş parçacığı yürütülerek, bu hizmet null bir işaretçi döndürür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1898">If no thread is executing, this service returns a null pointer.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1899">*Bu hizmet bir ıSR 'den çağrılırsa, dönüş değeri yürütülen kesme işleyicisinden önce çalışan iş parçacığını temsil eder.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1899">*If this service is called from an ISR, the return value represents the thread running prior to the executing interrupt handler.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1900">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1900">Parameters</span></span>

<span data-ttu-id="9fec9-1901">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1901">None</span></span>

### <a name="retuen-values"></a><span data-ttu-id="9fec9-1902">Retuen değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1902">Retuen Values</span></span>

- <span data-ttu-id="9fec9-1903">**iş parçacığı işaretçisi** Şu anda yürütülmekte olan iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1903">**thread pointer** Pointer to the currently executing thread.</span></span> <span data-ttu-id="9fec9-1904">İş parçacığı yürütülerek, dönüş değeri **TX_NULL**.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1904">If no thread is executing, the return value is **TX_NULL**.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1905">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1905">Allowed From</span></span>

<span data-ttu-id="9fec9-1906">İş parçacıkları ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1906">Threads and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1907">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1907">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1908">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1908">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1909">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1909">Example</span></span>

<span data-ttu-id="9fec9-1910">TX_THREAD \* my_thread_ptr;</span><span class="sxs-lookup"><span data-stu-id="9fec9-1910">TX_THREAD \*my_thread_ptr;</span></span>

```c
TX_THREAD *my_thread_ptr;

/* Find out who we are! */
my_thread_ptr = tx_thread_identify();

/* If my_thread_ptr is non-null, we are currently executing
from that thread or an ISR that interrupted that thread.
Otherwise, this service was called
from an ISR when no thread was running when the
interrupt occurred. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1911">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1911">See Also</span></span>

- <span data-ttu-id="9fec9-1912">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1912">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-1913">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1913">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-1914">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1914">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-1915">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1915">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-1916">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1916">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1917">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1917">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1918">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1918">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-1919">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1919">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-1920">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-1920">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-1921">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-1921">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-1922">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-1922">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-1923">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-1923">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-1924">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1924">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-1925">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-1925">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-1926">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-1926">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-1927">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1927">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-1928">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-1928">tx_thread_wait_abort</span></span>

## <a name="tx_thread_info_get"></a><span data-ttu-id="9fec9-1929">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1929">tx_thread_info_get</span></span>

<span data-ttu-id="9fec9-1930">İş parçacığı hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="9fec9-1930">Retrieve information about thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1931">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1931">Prototype</span></span>

```c
UINT tx_thread_info_get(
    TX_THREAD *thread_ptr, 
    CHAR **name,
    UINT *state, 
    ULONG *run_count,
    UINT *priority,
    UINT *preemption_threshold,
    ULONG *time_slice,
    TX_THREAD **next_thread,
    TX_THREAD **suspended_thread);
```

### <a name="description"></a><span data-ttu-id="9fec9-1932">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1932">Description</span></span>

<span data-ttu-id="9fec9-1933">Bu hizmet, belirtilen iş parçacığı hakkındaki bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1933">This service retrieves information about the specified thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1934">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1934">Parameters</span></span>
- <span data-ttu-id="9fec9-1935">**thread_ptr** İş parçacığı denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1935">**thread_ptr** Pointer to thread control block.</span></span>
- <span data-ttu-id="9fec9-1936">**ad** İş parçacığının adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1936">**name** Pointer to destination for the pointer to the thread's name.</span></span>
- <span data-ttu-id="9fec9-1937">**durum** İş parçacığının geçerli yürütme durumu için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1937">**state** Pointer to destination for the thread's current execution state.</span></span> <span data-ttu-id="9fec9-1938">Olası değerler aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1938">Possible values are as follows.</span></span>
    - <span data-ttu-id="9fec9-1939">**TX_READY** (0x00)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1939">**TX_READY** (0x00)</span></span>
    - <span data-ttu-id="9fec9-1940">**TX_COMPLETED** (0x01)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1940">**TX_COMPLETED** (0x01)</span></span>
    - <span data-ttu-id="9fec9-1941">**TX_TERMINATED** (0x02)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1941">**TX_TERMINATED** (0x02)</span></span>
    - <span data-ttu-id="9fec9-1942">**TX_SUSPENDED** (0x03)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1942">**TX_SUSPENDED** (0x03)</span></span>
    - <span data-ttu-id="9fec9-1943">**TX_SLEEP** (0x04)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1943">**TX_SLEEP** (0x04)</span></span>
    - <span data-ttu-id="9fec9-1944">**TX_QUEUE_SUSP** (0x05)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1944">**TX_QUEUE_SUSP** (0x05)</span></span>
    - <span data-ttu-id="9fec9-1945">**TX_SEMAPHORE_SUSP** (0x06)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1945">**TX_SEMAPHORE_SUSP** (0x06)</span></span>
    - <span data-ttu-id="9fec9-1946">**TX_EVENT_FLAG** (0x07)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1946">**TX_EVENT_FLAG** (0x07)</span></span>
    - <span data-ttu-id="9fec9-1947">**TX_BLOCK_MEMORY** (0x08)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1947">**TX_BLOCK_MEMORY** (0x08)</span></span>
    - <span data-ttu-id="9fec9-1948">**TX_BYTE_MEMORY** (0x09)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1948">**TX_BYTE_MEMORY** (0x09)</span></span>
    - <span data-ttu-id="9fec9-1949">**TX_MUTEX_SUSP** (0x0D)</span><span class="sxs-lookup"><span data-stu-id="9fec9-1949">**TX_MUTEX_SUSP** (0x0D)</span></span>  

- <span data-ttu-id="9fec9-1950">**run_count** İş parçacığının çalışma sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1950">**run_count** Pointer to destination for the thread's run count.</span></span>
- <span data-ttu-id="9fec9-1951">**Öncelik** İş parçacığının önceliği için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1951">**priority** Pointer to destination for the thread's priority.</span></span>
- <span data-ttu-id="9fec9-1952">**preemption_threshold** İş parçacığının önalım-Threshold hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1952">**preemption_threshold** Pointer to destination for the thread's preemption-threshold.</span></span>
<span data-ttu-id="9fec9-1953">**time_slice** İş parçacığının zaman dilimi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1953">**time_slice** Pointer to destination for the thread's time-slice.</span></span>
<span data-ttu-id="9fec9-1954">**next_thread** Sonraki oluşturulan iş parçacığı işaretçisinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1954">**next_thread** Pointer to destination for next created thread pointer.</span></span>

<span data-ttu-id="9fec9-1955">**suspended_thread** Askıya alma listesindeki bir sonraki iş parçacığına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1955">**suspended_thread** Pointer to destination for pointer to next thread in suspension list.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-1956">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1956">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-1957">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-1957">Return Values</span></span>

- <span data-ttu-id="9fec9-1958">**TX_SUCCESS** (0x00) başarılı iş parçacığı bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1958">**TX_SUCCESS** (0x00) Successful thread information retrieval.</span></span>
- <span data-ttu-id="9fec9-1959">**TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı denetim işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1959">**TX_THREAD_ERROR** (0x0E) Invalid thread control pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-1960">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-1960">Allowed From</span></span>

<span data-ttu-id="9fec9-1961">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-1961">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-1962">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-1962">Preemption Possible</span></span>

<span data-ttu-id="9fec9-1963">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-1963">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-1964">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-1964">Example</span></span>

```c
TX_THREAD my_thread;
CHAR *name;
UINT state;
ULONG run_count;
UINT priority;
UINT preemption_threshold;
UINT time_slice;
TX_THREAD *next_thread;
TX_THREAD *suspended_thread;
UINT status;

/* Retrieve information about the previously created
thread "my_thread." */

status = tx_thread_info_get(&my_thread, &name,
    &state, &run_count,
    &priority, &preemption_threshold,
    &time_slice, &next_thread,&suspended_thread);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-1965">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1965">See Also</span></span>

- <span data-ttu-id="9fec9-1966">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-1966">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-1967">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-1967">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-1968">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1968">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-1969">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1969">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-1970">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1970">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-1971">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1971">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-1972">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1972">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-1973">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1973">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-1974">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-1974">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-1975">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-1975">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-1976">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-1976">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-1977">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-1977">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-1978">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-1978">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-1979">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-1979">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-1980">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-1980">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-1981">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-1981">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-1982">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-1982">tx_thread_wait_abort</span></span>

## <a name="tx_thread_performance_info_get"></a><span data-ttu-id="9fec9-1983">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-1983">tx_thread_performance_info_get</span></span>

<span data-ttu-id="9fec9-1984">İş parçacığı performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-1984">Get thread performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-1985">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-1985">Prototype</span></span>

```c
UINT tx_thread_performance_info_get(
    TX_THREAD *thread_ptr,
    LONG *resumptions, 
    ULONG *suspensions,
    ULONG *solicited_preemptions, 
    ULONG *interrupt_preemptions,
    ULONG *priority_inversions, 
    ULONG *time_slices,
    ULONG *relinquishes, 
    ULONG *timeouts, 
    ULONG *wait_aborts,
    TX_THREAD **last_preempted_by);
```

### <a name="description"></a><span data-ttu-id="9fec9-1986">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-1986">Description</span></span>

<span data-ttu-id="9fec9-1987">Bu hizmet, belirtilen iş parçacığıyla ilgili performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1987">This service retrieves performance information about the specified thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-1988">*Işparçacığıx kitaplığı ve uygulaması ile*  \* oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için _ _defined **TX_THREAD_ENABLE_PERFORMANCE_INFO**. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-1988">*The ThreadX library and application must be built with* ***TX_THREAD_ENABLE_PERFORMANCE_INFO** _ _defined in order for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-1989">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-1989">Parameters</span></span>
- <span data-ttu-id="9fec9-1990">**thread_ptr** Daha önce oluşturulmuş iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1990">**thread_ptr** Pointer to previously created thread.</span></span>
- <span data-ttu-id="9fec9-1991">**bağlantının sürdürülmesi** Bu iş parçacığının bağlantının sürdürülmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1991">**resumptions** Pointer to destination for the number of resumptions of this thread.</span></span>
- <span data-ttu-id="9fec9-1992">**getirilmesi** Bu iş parçacığının getirilmesi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1992">**suspensions** Pointer to destination for the number of suspensions of this thread.</span></span>
- <span data-ttu-id="9fec9-1993">**solicited_preemptions** Bu iş parçacığı tarafından yapılan bir ThreadX API hizmeti çağrısının sonucu olarak, preemptions sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1993">**solicited_preemptions** Pointer to destination for the number of preemptions as a result of a ThreadX API service call made by this thread.</span></span>
- <span data-ttu-id="9fec9-1994">**interrupt_preemptions** Bu iş parçacığının preemptions sayısı için hedef işaretçisi, kesme işlemenin sonucu olarak.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1994">**interrupt_preemptions** Pointer to destination for the number of preemptions of this thread as a result of interrupt processing.</span></span>
- <span data-ttu-id="9fec9-1995">**priority_inversions** Bu iş parçacığının öncelik Inin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1995">**priority_inversions** Pointer to destination for the number of priority inversions of this thread.</span></span>
- <span data-ttu-id="9fec9-1996">**time_slices** Bu iş parçacığının zaman dilimlerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1996">**time_slices** Pointer to destination for the number of time-slices of this thread.</span></span>
- <span data-ttu-id="9fec9-1997">**relinquishes** Bu iş parçacığı tarafından gerçekleştirilen iş parçacığı relini sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1997">**relinquishes** Pointer to destination for the number of thread relinquishes performed by this thread.</span></span>
- <span data-ttu-id="9fec9-1998">**zaman aşımları** Bu iş parçacığında askıya alınma zaman aşımları sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1998">**timeouts** Pointer to destination for the number of suspension timeouts on this thread.</span></span>
- <span data-ttu-id="9fec9-1999">**wait_aborts** Bu iş parçacığında gerçekleştirilen bekleme iptal sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-1999">**wait_aborts** Pointer to destination for the number of wait aborts performed on this thread.</span></span>
- <span data-ttu-id="9fec9-2000">**last_preempted_by** Bu iş parçacığını en son alan iş parçacığı işaretçisinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2000">**last_preempted_by** Pointer to destination for the thread pointer that last preempted this thread.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2001">*Herhangi bir parametre için TX_NULL sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2001">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2002">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2002">Return Values</span></span>

- <span data-ttu-id="9fec9-2003">**TX_SUCCESS** (0x00) başarılı iş parçacığı performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2003">**TX_SUCCESS** (0x00) Successful thread performance get.</span></span>
- <span data-ttu-id="9fec9-2004">**TX_PTR_ERROR** (0x03) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2004">**TX_PTR_ERROR** (0x03) Invalid thread pointer.</span></span>
- <span data-ttu-id="9fec9-2005">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2005">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2006">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2006">Allowed From</span></span>

<span data-ttu-id="9fec9-2007">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2007">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2008">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2008">Example</span></span>

```c
TX_THREAD my_thread;
ULONG resumptions;
ULONG suspensions;
ULONG solicited_preemptions;
ULONG interrupt_preemptions;
ULONG priority_inversions;
ULONG time_slices;
ULONG relinquishes;
ULONG timeouts;
ULONG wait_aborts;
TX_THREAD *last_preempted_by;

/* Retrieve performance information on the previously created
thread. */

status = tx_thread_performance_info_get(&my_thread, &resumptions,
    &suspensions,
    &solicited_preemptions, &interrupt_preemptions,
    &priority_inversions, &time_slices,
    &relinquishes, &timeouts,
    &wait_aborts, &last_preempted_by);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2009">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2009">See Also</span></span>

- <span data-ttu-id="9fec9-2010">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2010">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2011">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2011">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2012">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2012">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2013">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2013">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2014">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2014">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2015">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2015">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2016">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2016">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2017">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2017">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2018">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2018">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2019">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2019">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2020">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2020">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2021">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2021">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2022">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2022">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2023">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2023">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2024">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2024">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2025">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2025">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2026">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2026">tx_thread_wait_abort</span></span>

## <a name="tx_thread_performance_system_info_get"></a><span data-ttu-id="9fec9-2027">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2027">tx_thread_performance_system_info_get</span></span>

<span data-ttu-id="9fec9-2028">İş parçacığı sistemi performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-2028">Get thread system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2029">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2029">Prototype</span></span>

```c
UINT tx_thread_performance_system_info_get(
    ULONG *resumptions,
    ULONG *suspensions, 
    ULONG *solicited_preemptions,
    ULONG *interrupt_preemptions, 
    ULONG *priority_inversions,
    ULONG *time_slices, 
    ULONG *relinquishes, 
    ULONG *timeouts,
    ULONG *wait_aborts, 
    ULONG *non_idle_returns,
    ULONG *idle_returns);
```

### <a name="description"></a><span data-ttu-id="9fec9-2030">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2030">Description</span></span>

<span data-ttu-id="9fec9-2031">Bu hizmet, sistemdeki tüm iş parçacıkları hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2031">This service retrieves performance information about all the threads in the system.</span></span>

<span data-ttu-id="9fec9-2032">*Işparçacığıx kitaplığı ve uygulaması ile oluşturulmalıdır*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2032">*The ThreadX library and application must be built with*</span></span>

<span data-ttu-id="9fec9-2033">\*Bu hizmetin performans bilgilerini döndürmesi için _ _defined **TX_THREAD_ENABLE_PERFORMANCE_INFO**. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2033">***TX_THREAD_ENABLE_PERFORMANCE_INFO** _ _defined in order for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2034">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2034">Parameters</span></span>

- <span data-ttu-id="9fec9-2035">**bağlantının sürdürülmesi** Toplam iş parçacığı sayısı için hedef işaretçisi bağlantının sürdürülmesi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2035">**resumptions** Pointer to destination for the total number of thread resumptions.</span></span>
- <span data-ttu-id="9fec9-2036">**getirilmesi** Toplam iş parçacığı sayısı için hedef işaretçisi getirilmesi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2036">**suspensions** Pointer to destination for the total number of thread suspensions.</span></span>
- <span data-ttu-id="9fec9-2037">**solicited_preemptions** Bir ThreadX API hizmetini çağıran iş parçacığının bir sonucu olarak preemptions iş parçacığı toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2037">**solicited_preemptions** Pointer to destination for the total number of thread preemptions as a result of a thread calling a ThreadX API service.</span></span>
- <span data-ttu-id="9fec9-2038">**interrupt_preemptions** Kesme işlemenin sonucu olarak preemptions iş parçacığı toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2038">**interrupt_preemptions** Pointer to destination for the total number of thread preemptions as a result of interrupt processing.</span></span>
- <span data-ttu-id="9fec9-2039">**priority_inversions** Toplam iş parçacığı önceliği ınsürümlerin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2039">**priority_inversions** Pointer to destination for the total number of thread priority inversions.</span></span>
- <span data-ttu-id="9fec9-2040">**time_slices** İş parçacığı zaman dilimlerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2040">**time_slices** Pointer to destination for the total number of thread time-slices.</span></span>
- <span data-ttu-id="9fec9-2041">**relinquishes** Toplam iş parçacığı yeniden sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2041">**relinquishes** Pointer to destination for the total number of thread relinquishes.</span></span>
- <span data-ttu-id="9fec9-2042">**zaman aşımları** Toplam iş parçacığı askıya alma zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2042">**timeouts** Pointer to destination for the total number of thread suspension timeouts.</span></span>
- <span data-ttu-id="9fec9-2043">**wait_aborts** Toplam iş parçacığı bekleme sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2043">**wait_aborts** Pointer to destination for the total number of thread wait aborts.</span></span>
- <span data-ttu-id="9fec9-2044">**non_idle_returns** Başka bir iş parçacığı yürütülmeye hazırlandığınızda, bir iş parçacığının sisteme kaç kez geri döndüğünü gösteren hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2044">**non_idle_returns** Pointer to destination for the number of times a thread returns to the system when another thread is ready to execute.</span></span>
- <span data-ttu-id="9fec9-2045">**idle_returns** Başka bir iş parçacığı yürütülmeye hazırlanana olmadığında, bir iş parçacığının sisteme döndürdüğü süre için hedef işaretçisi (boş sistem).</span><span class="sxs-lookup"><span data-stu-id="9fec9-2045">**idle_returns** Pointer to destination for the number of times a thread returns to the system when no other thread is ready to execute (idle system).</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2046">*Herhangi bir parametre için **TX_NULL** sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2046">*Supplying a **TX_NULL** for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2047">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2047">Return Values</span></span>

- <span data-ttu-id="9fec9-2048">**TX_SUCCESS** (0x00) başarılı iş parçacığı sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2048">**TX_SUCCESS** (0x00) Successful thread system performance get.</span></span>
- <span data-ttu-id="9fec9-2049">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2049">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2050">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2050">Allowed From</span></span>

<span data-ttu-id="9fec9-2051">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2051">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2052">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2052">Example</span></span>

```c
ULONG resumptions;
ULONG suspensions;
ULONG solicited_preemptions;
ULONG interrupt_preemptions;
ULONG priority_inversions;
ULONG time_slices;
ULONG relinquishes;
ULONG timeouts;
ULONG wait_aborts;
ULONG non_idle_returns;
ULONG idle_returns;

/* Retrieve performance information on all previously created
thread. */

status = tx_thread_performance_system_info_get(&resumptions,
    &suspensions,
    &solicited_preemptions, &interrupt_preemptions,
    &priority_inversions, &time_slices, &relinquishes,
    &timeouts, &wait_aborts, &non_idle_returns,
    &idle_returns);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2053">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2053">See Also</span></span>

- <span data-ttu-id="9fec9-2054">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2054">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2055">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2055">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2056">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2056">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2057">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2057">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2058">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2058">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2059">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2059">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2060">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2060">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2061">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2061">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2062">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2062">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2063">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2063">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2064">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2064">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2065">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2065">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2066">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2066">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2067">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2067">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2068">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2068">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2069">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2069">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2070">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2070">tx_thread_wait_abort</span></span>

## <a name="tx_thread_preemption_change"></a><span data-ttu-id="9fec9-2071">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2071">tx_thread_preemption_change</span></span>

<span data-ttu-id="9fec9-2072">Önalım-uygulama iş parçacığının eşiğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="9fec9-2072">Change preemption-threshold of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2073">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2073">Prototype</span></span>

```c
UINT tx_thread_preemption_change(
    TX_THREAD *thread_ptr,
    UINT new_threshold, 
    UINT *old_threshold);
```

### <a name="description"></a><span data-ttu-id="9fec9-2074">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2074">Description</span></span>

<span data-ttu-id="9fec9-2075">Bu hizmet, belirtilen iş parçacığının önalım eşiğini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2075">This service changes the preemption-threshold of the specified thread.</span></span> <span data-ttu-id="9fec9-2076">Önalım-Threshold, önalım-Threshold değerine eşit veya daha küçük olan iş parçacıkları tarafından belirtilen iş parçacığının önalım ' i engelliyor.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2076">The preemption-threshold prevents preemption of the specified thread by threads equal to or less than the preemption-threshold value.</span></span>

>[!NOTE]
> <span data-ttu-id="9fec9-2077">*Önalım-Threshold kullanılması, belirtilen iş parçacığı için zaman dilimini devre dışı bırakır.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2077">*Using preemption-threshold disables time-slicing for the specified thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2078">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2078">Parameters</span></span>
- <span data-ttu-id="9fec9-2079">**thread_ptr** Daha önce oluşturulmuş bir uygulama iş parçacığına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2079">**thread_ptr** Pointer to a previously created application thread.</span></span>
- <span data-ttu-id="9fec9-2080">**new_threshold** Yeni önalım-Threshold öncelik düzeyi (0 ila (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="9fec9-2080">**new_threshold** New preemption-threshold priority level (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="9fec9-2081">**old_threshold** Önceki önalım-Threshold döndürecek bir konum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2081">**old_threshold** Pointer to a location to return the previous preemption-threshold.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2082">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2082">Return Values</span></span>

- <span data-ttu-id="9fec9-2083">**TX_SUCCESS** (0x00) başarılı önalım-eşik değişikliği.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2083">**TX_SUCCESS** (0x00) Successful preemption-threshold change.</span></span>
- <span data-ttu-id="9fec9-2084">**TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2084">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="9fec9-2085">**TX_THRESH_ERROR** (0x18) belirtilen yeni önalım-Threshold geçerli iş parçacığı önceliğine göre geçerli bir iş parçacığı önceliği ((0 ila (**TX_MAX_PRIORITIES**-1) veya daha büyük (düşük öncelik) değil.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2085">**TX_THRESH_ERROR** (0x18) Specified new preemption-threshold is not a valid thread priority (a value other than (0 through (**TX_MAX_PRIORITIES**-1)) or is greater than (lower priority) than the current thread priority.</span></span>
- <span data-ttu-id="9fec9-2086">**TX_PTR_ERROR** (0x03) önceki preemptionthreshold depolama konumuna yönelik geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2086">**TX_PTR_ERROR** (0x03) Invalid pointer to previous preemptionthreshold storage location.</span></span>
- <span data-ttu-id="9fec9-2087">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2087">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2088">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2088">Allowed From</span></span>

<span data-ttu-id="9fec9-2089">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="9fec9-2089">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2090">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2090">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2091">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-2091">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2092">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2092">Example</span></span>

```c
TX_THREAD my_thread;
UINT my_old_threshold;
UINT status;

/* Disable all preemption of the specified thread. The
current preemption-threshold is returned in
"my_old_threshold". Assume that "my_thread" has
already been created. */

status = tx_thread_preemption_change(&my_thread,
    0, &my_old_threshold);

/* If status equals TX_SUCCESS, the application thread is
non-preemptable by another thread. Note that ISRs are
not prevented by preemption disabling. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2093">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2093">See Also</span></span>

- <span data-ttu-id="9fec9-2094">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2094">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2095">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2095">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2096">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2096">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2097">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2097">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2098">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2098">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2099">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2099">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2100">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2100">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2101">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2101">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2102">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2102">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2103">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2103">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2104">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2104">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2105">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2105">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2106">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2106">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2107">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2107">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2108">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2108">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2109">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2109">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2110">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2110">tx_thread_wait_abort</span></span>

## <a name="tx_thread_priority_change"></a><span data-ttu-id="9fec9-2111">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2111">tx_thread_priority_change</span></span>

<span data-ttu-id="9fec9-2112">Uygulama iş parçacığının önceliğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="9fec9-2112">Change priority of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2113">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2113">Prototype</span></span>

```c
UINT tx_thread_priority_change(
    TX_THREAD *thread_ptr,
    UINT new_priority, 
    UINT *old_priority);
```

### <a name="description"></a><span data-ttu-id="9fec9-2114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2114">Description</span></span>

<span data-ttu-id="9fec9-2115">Bu hizmet, belirtilen iş parçacığının önceliğini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2115">This service changes the priority of the specified thread.</span></span> <span data-ttu-id="9fec9-2116">Geçerli öncelikler 0 ile (TX_MAX_PRIORITES-1) arasındadır; burada 0 en yüksek öncelik düzeyini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2116">Valid priorities range from 0 through (TX_MAX_PRIORITES-1), where 0 represents the highest priority level.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-2117">\* Belirtilen iş parçacığının önalım-Threshold değeri otomatik olarak yeni önceliğe ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2117">\*The preemption-threshold of the specified thread is automatically set to the new priority.</span></span> <span data-ttu-id="9fec9-2118">Yeni bir eşik isteniyorsa, bu call._ sonra \***tx_thread_preemption_change** _ hizmetinin kullanılması gerekir</span><span class="sxs-lookup"><span data-stu-id="9fec9-2118">If a new threshold is desired, the \***tx_thread_preemption_change** _ service must be used after this call._</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2119">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2119">Parameters</span></span>

- <span data-ttu-id="9fec9-2120">**thread_ptr** Daha önce oluşturulmuş bir uygulama iş parçacığına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2120">**thread_ptr** Pointer to a previously created application thread.</span></span>
- <span data-ttu-id="9fec9-2121">**new_priority** Yeni iş parçacığı öncelik düzeyi (0 ila (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="9fec9-2121">**new_priority** New thread priority level (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="9fec9-2122">**old_priority** İş parçacığının önceki önceliğini döndürmek için bir konum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2122">**old_priority** Pointer to a location to return the thread's previous priority.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2123">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2123">Return Values</span></span>

- <span data-ttu-id="9fec9-2124">**TX_SUCCESS** (0x00) başarılı öncelik değişikliği.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2124">**TX_SUCCESS** (0x00) Successful priority change.</span></span>
- <span data-ttu-id="9fec9-2125">**TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2125">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="9fec9-2126">**TX_PRIORITY_ERROR** (0x0F) belirtilen yeni öncelik geçerli değil ((0-(TX_MAX_PRIORITIES-1) dışında bir değer).</span><span class="sxs-lookup"><span data-stu-id="9fec9-2126">**TX_PRIORITY_ERROR** (0x0F) Specified new priority is not valid (a value other than (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="9fec9-2127">**TX_PTR_ERROR** (0x03) önceki öncelikli depolama konumuna yönelik geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2127">**TX_PTR_ERROR** (0x03) Invalid pointer to previous priority storage location.</span></span>
- <span data-ttu-id="9fec9-2128">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2128">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2129">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2129">Allowed From</span></span>

<span data-ttu-id="9fec9-2130">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="9fec9-2130">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2131">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2131">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2132">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-2132">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2133">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2133">Example</span></span>

```c
TX_THREAD my_thread;
UINT my_old_priority;
UINT status;

/* Change the thread represented by "my_thread" to priority
0. */

status = tx_thread_priority_change(&my_thread,
    0, &my_old_priority);

/* If status equals TX_SUCCESS, the application thread is
now at the highest priority level in the system. */
```
### <a name="see-also"></a><span data-ttu-id="9fec9-2134">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2134">See Also</span></span>

- <span data-ttu-id="9fec9-2135">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2135">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2136">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2136">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2137">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2137">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2138">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2138">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2139">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2139">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2140">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2140">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2141">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2141">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2142">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2142">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2143">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2143">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2144">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2144">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2145">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2145">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2146">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2146">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2147">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2147">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2148">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2148">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2149">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2149">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2150">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2150">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2151">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2151">tx_thread_wait_abort</span></span>

## <a name="tx_thread_relinquish"></a><span data-ttu-id="9fec9-2152">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2152">tx_thread_relinquish</span></span>

<span data-ttu-id="9fec9-2153">Diğer uygulama iş parçacıklarıyla denetimi yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fec9-2153">Relinquish control to other application threads</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2154">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2154">Prototype</span></span>

```c
VOID tx_thread_relinquish(VOID);
```

### <a name="description"></a><span data-ttu-id="9fec9-2155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2155">Description</span></span>

<span data-ttu-id="9fec9-2156">Bu hizmet, aynı veya daha yüksek önceliğe sahip başka bir hazırlık iş parçacığına işlemci denetimini yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2156">This service relinquishes processor control to other ready-to-run threads at the same or higher priority.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2157">*Aynı önceliğe sahip iş parçacıklarıyla, bu hizmetin aynı önceliğe sahip iş parçacıklarından de daha fazla denetim, geçerli iş parçacığının önalım-Threshold ayarı nedeniyle yürütmenin en yüksek öncelikli iş parçacığına karşı çalışmasını engelledi.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2157">*In addition to relinquishing control to threads of the same priority, this service also relinquishes control to the highest-priority thread prevented from execution because of the current thread's preemption-threshold setting.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2158">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2158">Parameters</span></span>

<span data-ttu-id="9fec9-2159">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2159">None</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2160">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2160">Return Values</span></span>

<span data-ttu-id="9fec9-2161">Yok</span><span class="sxs-lookup"><span data-stu-id="9fec9-2161">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2162">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2162">Allowed From</span></span>

<span data-ttu-id="9fec9-2163">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-2163">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2164">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2164">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2165">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-2165">Yes</span></span>

### <a name="examples"></a><span data-ttu-id="9fec9-2166">Örnekler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2166">Examples</span></span>

```c
ULONG run_counter_1 = 0;
ULONG run_counter_2 = 0;

/* Example of two threads relinquishing control to
each other in an infinite loop. Assume that
both of these threads are ready and have the same
priority. The run counters will always stay within one
of each other. */

VOID my_first_thread(ULONG thread_input)
{
    /* Endless loop of relinquish. */
    while(1)
    {
        /* Increment the run counter. */
        run_counter_1++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}

VOID my_second_thread(ULONG thread_input)
{

    /* Endless loop of relinquish. */
    while(1)
    {
        /* Increment the run counter. */
        run_counter_2++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2167">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2167">See Also</span></span>

- <span data-ttu-id="9fec9-2168">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2168">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2169">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2169">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2170">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2170">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2171">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2171">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2172">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2172">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2173">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2173">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2174">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2174">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2175">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2175">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2176">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2176">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2177">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2177">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2178">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2178">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2179">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2179">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2180">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2180">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2181">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2181">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2182">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2182">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2183">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2183">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2184">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2184">tx_thread_wait_abort</span></span>

## <a name="tx_thread_reset"></a><span data-ttu-id="9fec9-2185">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2185">tx_thread_reset</span></span>

<span data-ttu-id="9fec9-2186">İş parçacığını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="9fec9-2186">Reset thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2187">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2187">Prototype</span></span>

```c
UINT tx_thread_reset(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-2188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2188">Description</span></span>

<span data-ttu-id="9fec9-2189">Bu hizmet, belirtilen iş parçacığını iş parçacığı oluşturma sırasında tanımlanan giriş noktasında yürütülecek şekilde sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2189">This service resets the specified thread to execute at the entry point defined at thread creation.</span></span> <span data-ttu-id="9fec9-2190">İş parçacığı sıfırlanmak için bir **TX_COMPLETED** veya **TX_TERMINATED** durumunda olmalıdır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2190">The thread must be in either a **TX_COMPLETED** or **TX_TERMINATED** state for it to be reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-2191">*Yeniden yürütülmesi için iş parçacığının sürdürülmeye devam etmelidir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2191">*The thread must be resumed for it to execute again.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2192">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2192">Parameters</span></span>

- <span data-ttu-id="9fec9-2193">**thread_ptr** Daha önce oluşturulmuş bir iş parçacığına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2193">**thread_ptr** Pointer to a previously created thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2194">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2194">Return Values</span></span>

- <span data-ttu-id="9fec9-2195">**TX_SUCCESS** (0x00) başarılı iş parçacığı sıfırlaması.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2195">**TX_SUCCESS** (0x00) Successful thread reset.</span></span>
- <span data-ttu-id="9fec9-2196">**TX_NOT_DONE** (0x20) belirtilen iş parçacığı **TX_COMPLETED** veya **TX_TERMINATED** durumunda değil.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2196">**TX_NOT_DONE** (0x20) Specified thread is not in a **TX_COMPLETED** or **TX_TERMINATED** state.</span></span>
- <span data-ttu-id="9fec9-2197">**TX_THREAD_ERROR** (0x0E) geçersiz iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2197">**TX_THREAD_ERROR** (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="9fec9-2198">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2198">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2199">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2199">Allowed From</span></span>

<span data-ttu-id="9fec9-2200">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-2200">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2201">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2201">Example</span></span>

<span data-ttu-id="9fec9-2202">TX_THREAD my_thread;</span><span class="sxs-lookup"><span data-stu-id="9fec9-2202">TX_THREAD my_thread;</span></span>

```c
TX_THREAD my_thread;

/* Reset the previously created thread "my_thread." */

status = tx_thread_reset(&my_thread);

/* If status is TX_SUCCESS the thread is reset. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2203">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2203">See Also</span></span>

- <span data-ttu-id="9fec9-2204">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2204">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2205">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2205">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2206">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2206">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2207">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2207">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2208">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2208">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2209">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2209">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2210">tx_thread_preformance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2210">tx_thread_preformance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2211">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2211">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2212">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2212">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2213">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2213">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2214">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2214">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2215">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2215">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2216">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2216">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2217">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2217">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2218">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2218">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2219">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2219">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2220">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2220">tx_thread_wait_abort</span></span>

## <a name="tx_thread_resume"></a><span data-ttu-id="9fec9-2221">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2221">tx_thread_resume</span></span>

<span data-ttu-id="9fec9-2222">Askıya alınmış uygulama iş parçacığını sürdürür</span><span class="sxs-lookup"><span data-stu-id="9fec9-2222">Resume suspended application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2223">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2223">Prototype</span></span>

```c
UINT tx_thread_resume(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-2224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2224">Description</span></span>

<span data-ttu-id="9fec9-2225">Bu hizmet, daha önce bir ***tx_thread_suspend*** çağrısıyla askıya alınmış bir iş parçacığını yürütmeye devam eder veya hazırlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2225">This service resumes or prepares for execution a thread that was previously suspended by a ***tx_thread_suspend*** call.</span></span> <span data-ttu-id="9fec9-2226">Ayrıca, bu hizmet otomatik başlatma olmadan oluşturulan iş parçacıklarını sürdürür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2226">In addition, this service resumes threads that were created without an automatic start.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2227">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2227">Parameters</span></span>

- <span data-ttu-id="9fec9-2228">**thread_ptr** Askıya alınmış bir uygulama iş parçacığına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2228">**thread_ptr** Pointer to a suspended application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2229">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2229">Return Values</span></span>

- <span data-ttu-id="9fec9-2230">**TX_SUCCESS** (0x00) başarılı iş parçacığı özgeçmişi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2230">**TX_SUCCESS** (0x00) Successful thread resume.</span></span>
- <span data-ttu-id="9fec9-2231">**TX_SUSPEND_LIFTED** (0x19) daha önce Gecikmeli askıya alma yükseltilmemiş idi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2231">**TX_SUSPEND_LIFTED** (0x19) Previously set delayed suspension was lifted.</span></span>
- <span data-ttu-id="9fec9-2232">**TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2232">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="9fec9-2233">**TX_RESUME_ERROR** (0x12) belirtilen iş parçacığı askıya alınmaz veya daha önce **_tx_thread_suspend_** dışında bir hizmet tarafından askıya alındı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2233">**TX_RESUME_ERROR** (0x12) Specified thread is not suspended or was previously suspended by a service other than **_tx_thread_suspend_**.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2234">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2234">Allowed From</span></span>

<span data-ttu-id="9fec9-2235">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2235">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2236">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2236">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2237">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-2237">Yes</span></span>

<span data-ttu-id="9fec9-2238">TX_THREAD my_thread;</span><span class="sxs-lookup"><span data-stu-id="9fec9-2238">TX_THREAD my_thread;</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2239">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2239">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Resume the thread represented by "my_thread". */
status = tx_thread_resume(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
now ready to execute. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2240">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2240">See Also</span></span>

- <span data-ttu-id="9fec9-2241">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2241">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2242">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2242">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2243">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2243">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2244">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2244">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2245">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2245">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2246">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2246">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2247">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2247">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2248">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2248">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2249">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2249">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2250">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2250">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2251">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2251">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2252">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2252">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2253">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2253">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2254">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2254">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2255">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2255">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2256">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2256">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2257">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2257">tx_thread_wait_abort</span></span>

## <a name="tx_thread_sleep"></a><span data-ttu-id="9fec9-2258">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2258">tx_thread_sleep</span></span>

<span data-ttu-id="9fec9-2259">Belirtilen süre boyunca geçerli iş parçacığını askıya al</span><span class="sxs-lookup"><span data-stu-id="9fec9-2259">Suspend current thread for specified time</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2260">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2260">Prototype</span></span>

```c
UINT tx_thread_sleep(ULONG timer_ticks);
```

### <a name="description"></a><span data-ttu-id="9fec9-2261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2261">Description</span></span>

<span data-ttu-id="9fec9-2262">Bu hizmet, çağıran iş parçacığının belirtilen sayıda süreölçer onay işareti için askıda olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2262">This service causes the calling thread to suspend for the specified number of timer ticks.</span></span> <span data-ttu-id="9fec9-2263">Süreölçer Tick ile ilişkili fiziksel sürenin miktarı uygulamaya özgüdür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2263">The amount of physical time associated with a timer tick is application specific.</span></span> <span data-ttu-id="9fec9-2264">Bu hizmet, yalnızca bir uygulama iş parçacığından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2264">This service can be called only from an application thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2265">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2265">Parameters</span></span>

- <span data-ttu-id="9fec9-2266">**timer_ticks** Çağıran uygulama iş parçacığını askıya almak için 0 ile 0xFFFFFFFF arasında değişen Zamanlayıcı onay işaretleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2266">**timer_ticks** The number of timer ticks to suspend the calling application thread, ranging from 0 through 0xFFFFFFFF.</span></span> <span data-ttu-id="9fec9-2267">0 belirtilirse, hizmet hemen döndürür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2267">If 0 is specified, the service returns immediately.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2268">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2268">Return Values</span></span>

- <span data-ttu-id="9fec9-2269">**TX_SUCCESS** (0x00) başarılı iş parçacığı uykusu.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2269">**TX_SUCCESS** (0x00) Successful thread sleep.</span></span>
- <span data-ttu-id="9fec9-2270">**TX_WAIT_ABORTED** (0x1A) askıya alma başka bir iş parçacığı, ZAMANLAYıCı veya ISR tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2270">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="9fec9-2271">**TX_CALLER_ERROR** (0x13) hizmet iş parçacığından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2271">**TX_CALLER_ERROR** (0x13) Service called from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2272">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2272">Allowed From</span></span>

<span data-ttu-id="9fec9-2273">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-2273">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2274">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2274">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2275">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-2275">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2276">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2276">Example</span></span>

```c
UINT status;

/* Make the calling thread sleep for 100
timer-ticks. */
status = tx_thread_sleep(100);

/* If status equals TX_SUCCESS, the currently running
application thread slept for the specified number of
timer-ticks. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2277">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2277">See Also</span></span>

- <span data-ttu-id="9fec9-2278">tx_thread_create, tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2278">tx_thread_create, tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2279">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2279">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2280">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2280">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2281">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2281">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2282">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2282">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2283">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2283">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2284">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2284">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2285">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2285">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2286">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2286">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2287">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2287">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2288">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2288">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2289">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2289">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2290">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2290">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2291">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2291">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2292">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2292">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2293">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2293">tx_thread_wait_abort</span></span>

## <a name="tx_thread_stack_error_notify"></a><span data-ttu-id="9fec9-2294">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2294">tx_thread_stack_error_notify</span></span>

<span data-ttu-id="9fec9-2295">İş parçacığı yığınını kaydet hata bildirimi geri araması</span><span class="sxs-lookup"><span data-stu-id="9fec9-2295">Register thread stack error notification callback</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2296">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2296">Prototype</span></span>

```c
UINT tx_thread_stack_error_notify(VOID (*error_handler)(TX_THREAD *));
```

### <a name="description"></a><span data-ttu-id="9fec9-2297">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2297">Description</span></span>

<span data-ttu-id="9fec9-2298">Bu hizmet, iş parçacığı yığın hatalarını işlemek için bir bildirim geri çağırma işlevi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2298">This service registers a notification callback function for handling thread stack errors.</span></span> <span data-ttu-id="9fec9-2299">ThreadX, yürütme sırasında bir iş parçacığı yığını hatası algıladığında, hatayı işlemek için bu bildirim işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2299">When ThreadX detects a thread stack error during execution, it will call this notification function to process the error.</span></span> <span data-ttu-id="9fec9-2300">Hatanın işlenmesi uygulama tarafından tamamen tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2300">Processing of the error is completely defined by the application.</span></span> <span data-ttu-id="9fec9-2301">Sistemin tamamını sıfırlamak için ihlal iş parçacığını askıya almadan herhangi bir şey yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2301">Anything from suspending the violating thread to resetting the entire system may be done.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-2302">*Bu hizmetin performans bilgilerini döndürmesi* Için *threadx kitaplığı,* **TX_ENABLE_STACK_CHECKING** tanımlanmış olarak oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2302">*The ThreadX library must be built with* **TX_ENABLE_STACK_CHECKING** *defined in order for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2303">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2303">Parameters</span></span>
- <span data-ttu-id="9fec9-2304">**error_handler** Uygulamanın yığın hata işleme işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2304">**error_handler** Pointer to application's stack error handling function.</span></span> <span data-ttu-id="9fec9-2305">Bu değer TX_NULL, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2305">If this value is TX_NULL, the notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2306">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2306">Return Values</span></span>

- <span data-ttu-id="9fec9-2307">**TX_SUCCESS** (0x00) başarılı iş parçacığı sıfırlaması.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2307">**TX_SUCCESS** (0x00) Successful thread reset.</span></span>
- <span data-ttu-id="9fec9-2308">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2308">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2309">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2309">Allowed From</span></span>

<span data-ttu-id="9fec9-2310">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2310">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2311">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2311">Example</span></span>

```c
void my_stack_error_handler(TX_THREAD *thread_ptr);

/* Register the "my_stack_error_handler" function with ThreadX
so that thread stack errors can be handled by the application. */
status = tx_thread_stack_error_notify(my_stack_error_handler);

/* If status is TX_SUCCESS the stack error handler is registered.*/
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2312">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2312">See Also</span></span>

- <span data-ttu-id="9fec9-2313">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2313">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2314">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2314">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2315">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2315">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2316">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2316">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2317">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2317">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2318">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2318">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2319">tx_thread_preformance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2319">tx_thread_preformance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2320">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2320">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2321">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2321">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2322">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2322">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2323">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2323">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2324">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2324">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2325">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2325">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2326">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2326">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2327">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2327">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2328">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2328">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2329">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2329">tx_thread_wait_abort</span></span>

## <a name="tx_thread_suspend"></a><span data-ttu-id="9fec9-2330">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2330">tx_thread_suspend</span></span>

<span data-ttu-id="9fec9-2331">Uygulama iş parçacığını askıya al</span><span class="sxs-lookup"><span data-stu-id="9fec9-2331">Suspend application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2332">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2332">Prototype</span></span>

```c
UINT tx_thread_suspend(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-2333">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2333">Description</span></span>

<span data-ttu-id="9fec9-2334">Bu hizmet belirtilen uygulama iş parçacığını askıya alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2334">This service suspends the specified application thread.</span></span> <span data-ttu-id="9fec9-2335">Bir iş parçacığı, kendisini askıya almak için bu hizmeti çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2335">A thread may call this service to suspend itself.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2336">*Belirtilen iş parçacığı başka bir nedenle zaten askıya alınmışsa, önceki askıya alma yükseltilmemiş olana kadar bu askıya alma işlemi dahili olarak tutulur. Bu gerçekleştiğinde, belirtilen iş parçacığının koşulsuz olarak askıya alınması gerçekleştirilir. Daha fazla koşulsuz askıya alma isteği etkisizdir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2336">*If the specified thread is already suspended for another reason, this suspension is held internally until the prior suspension is lifted. When that happens, this unconditional suspension of the specified thread is performed. Further unconditional suspension requests have no effect.*</span></span>

<span data-ttu-id="9fec9-2337">Askıya alındıktan sonra, yeniden yürütmek için iş parçacığının ***tx_thread_resume*** tarafından sürdürülmeye devam etmelidir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2337">After being suspended, the thread must be resumed by ***tx_thread_resume*** to execute again.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2338">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2338">Parameters</span></span>

- <span data-ttu-id="9fec9-2339">**thread_ptr** Uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2339">**thread_ptr** Pointer to an application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2340">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2340">Return Values</span></span>

- <span data-ttu-id="9fec9-2341">**TX_SUCCESS** (0x00) başarılı iş parçacığı askıya alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2341">**TX_SUCCESS** (0x00) Successful thread suspend.</span></span>
- <span data-ttu-id="9fec9-2342">**TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2342">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="9fec9-2343">**TX_SUSPEND_ERROR** (0x14) belirtilen iş parçacığı sonlandırılmış veya tamamlanmış durumda.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2343">**TX_SUSPEND_ERROR** (0x14) Specified thread is in a terminated or completed state.</span></span>
- <span data-ttu-id="9fec9-2344">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2344">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2345">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2345">Allowed From</span></span>

<span data-ttu-id="9fec9-2346">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2346">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2347">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2347">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2348">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-2348">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2349">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2349">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Suspend the thread represented by "my_thread". */
status = tx_thread_suspend(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
unconditionally suspended. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2350">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2350">See Also</span></span>

- <span data-ttu-id="9fec9-2351">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2351">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2352">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2352">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2353">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2353">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2354">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2354">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2355">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2355">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2356">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2356">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2357">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2357">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2358">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2358">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2359">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2359">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2360">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2360">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2361">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2361">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2362">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2362">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2363">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2363">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2364">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2364">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2365">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2365">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2366">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2366">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2367">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2367">tx_thread_wait_abort</span></span>

## <a name="tx_thread_terminate"></a><span data-ttu-id="9fec9-2368">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2368">tx_thread_terminate</span></span>

<span data-ttu-id="9fec9-2369">Uygulama iş parçacığını sonlandırır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2369">Terminates application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2370">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2370">Prototype</span></span>

```c
UINT tx_thread_terminate(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="9fec9-2371">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2371">Description</span></span>

<span data-ttu-id="9fec9-2372">Bu hizmet, iş parçacığının askıya alınmadığına bakılmaksızın belirtilen uygulama iş parçacığını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2372">This service terminates the specified application thread regardless of whether the thread is suspended or not.</span></span> <span data-ttu-id="9fec9-2373">Bir iş parçacığı, kendisini sonlandırmak için bu hizmeti çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2373">A thread may call this service to terminate itself.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2374">*İş parçacığının sonlandırma için uygun bir durumda olduğundan emin olmak uygulamanın sorumluluğundadır. Örneğin, bir iş parçacığı kritik uygulama işlemleri sırasında veya bu tür işlemleri bilinmeyen bir durumda bırakabileceği diğer ara yazılım bileşenleri içinde sonlandırmamalıdır.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2374">*It is the application's responsibility to ensure that the thread is in a state suitable for termination. For example, a thread should not be terminated during critical application processing or inside of other middleware components where it could leave such processing in an unknown state.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-2375">*Sonlandırıldıktan sonra, yeniden yürütülmesi için iş parçacığının sıfırlanması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2375">*After being terminated, the thread must be reset for it to execute again.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2376">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2376">Parameters</span></span>

- <span data-ttu-id="9fec9-2377">**thread_ptr** Uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2377">**thread_ptr** Pointer to application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2378">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2378">Return Values</span></span>
- <span data-ttu-id="9fec9-2379">**TX_SUCCESS** (0x00) başarılı iş parçacığı sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2379">**TX_SUCCESS** (0x00) Successful thread terminate.</span></span>
- <span data-ttu-id="9fec9-2380">**TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2380">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="9fec9-2381">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2381">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2382">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2382">Allowed From</span></span>

<span data-ttu-id="9fec9-2383">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="9fec9-2383">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2384">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2384">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2385">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-2385">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2386">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2386">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Terminate the thread represented by "my_thread". */
status = tx_thread_terminate(&my_thread);

/* If status equals TX_SUCCESS, the thread is terminated
and cannot execute again until it is reset. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2387">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2387">See Also</span></span>

- <span data-ttu-id="9fec9-2388">tx_thread_create tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2388">tx_thread_create tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2389">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2389">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2390">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2390">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2391">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2391">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2392">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2392">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2393">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2393">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2394">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2394">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2395">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2395">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2396">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2396">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2397">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2397">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2398">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2398">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2399">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2399">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2400">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2400">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2401">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2401">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2402">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2402">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="9fec9-2403">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2403">tx_thread_wait_abort</span></span>

## <a name="tx_thread_time_slice_change"></a><span data-ttu-id="9fec9-2404">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2404">tx_thread_time_slice_change</span></span>

<span data-ttu-id="9fec9-2405">Değişiklik saati-uygulama iş parçacığının dilimi</span><span class="sxs-lookup"><span data-stu-id="9fec9-2405">Changes time-slice of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2406">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2406">Prototype</span></span>

```c
UINT tx_thread_time_slice_change(
    TX_THREAD *thread_ptr,
    ULONG new_time_slice, 
    ULONG *old_time_slice);
```

### <a name="description"></a><span data-ttu-id="9fec9-2407">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2407">Description</span></span>

<span data-ttu-id="9fec9-2408">Bu hizmet, belirtilen uygulama iş parçacığının zaman dilimini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2408">This service changes the time-slice of the specified application thread.</span></span> <span data-ttu-id="9fec9-2409">Bir iş parçacığı için zaman dilimi seçme, aynı veya daha yüksek önceliklerin diğer iş parçacıklarının yürütme şansı olması için belirtilen sayıda süreölçer işareti yürütümeyeceğini yöntem.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2409">Selecting a time-slice for a thread insures that it won't execute more than the specified number of timer ticks before other threads of the same or higher priorities have a chance to execute.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2410">*Önalım-Threshold kullanılması, belirtilen iş parçacığı için zaman dilimini devre dışı bırakır.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2410">*Using preemption-threshold disables time-slicing for the specified thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2411">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2411">Parameters</span></span>

- <span data-ttu-id="9fec9-2412">**thread_ptr** Uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2412">**thread_ptr** Pointer to application thread.</span></span>
- <span data-ttu-id="9fec9-2413">**new_time_slice** Yeni zaman dilimi değeri.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2413">**new_time_slice** New time slice value.</span></span> <span data-ttu-id="9fec9-2414">Yasal değerler 1 ile 0xFFFFFFFF arasında TX_NO_TIME_SLICE ve sayısal değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2414">Legal values include TX_NO_TIME_SLICE and numeric values from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="9fec9-2415">**old_time_slice** Belirtilen iş parçacığının önceki timeslice değerini depolamak için konum işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2415">**old_time_slice** Pointer to location for storing the previous timeslice value of the specified thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2416">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2416">Return Values</span></span>

- <span data-ttu-id="9fec9-2417">**TX_SUCCESS** (0x00) başarılı zaman dilimi şansı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2417">**TX_SUCCESS** (0x00) Successful time-slice chance.</span></span>
- <span data-ttu-id="9fec9-2418">**TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2418">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="9fec9-2419">**TX_PTR_ERROR** (0x03) önceki zaman dilimi depolama konumuna yönelik geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2419">**TX_PTR_ERROR** (0x03) Invalid pointer to previous time-slice storage location.</span></span>
- <span data-ttu-id="9fec9-2420">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2420">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2421">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2421">Allowed From</span></span>

<span data-ttu-id="9fec9-2422">İş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="9fec9-2422">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2423">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2423">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2424">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2424">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2425">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2425">Example</span></span>

```c
TX_THREAD my_thread;
ULONG my_old_time_slice;
UINT status;

/* Change the time-slice of the thread associated with
"my_thread" to 20. This will mean that "my_thread"
can only run for 20 timer-ticks consecutively before
other threads of equal or higher priority get a chance
to run. */
status = tx_thread_time_slice_change(&my_thread, 20,
    &my_old_time_slice);

/* If status equals TX_SUCCESS, the thread’s time-slice
has been changed to 20 and the previous time-slice is
in "my_old_time_slice." */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2426">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2426">See Also</span></span>

- <span data-ttu-id="9fec9-2427">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2427">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2428">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2428">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2429">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2429">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2430">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2430">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2431">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2431">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2432">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2432">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2433">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2433">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2434">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2434">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2435">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2435">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2436">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2436">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2437">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2437">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2438">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2438">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2439">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2439">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2440">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2440">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2441">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2441">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2442">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2442">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2443">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2443">tx_thread_wait_abort</span></span>

## <a name="tx_thread_wait_abort"></a><span data-ttu-id="9fec9-2444">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="9fec9-2444">tx_thread_wait_abort</span></span>

<span data-ttu-id="9fec9-2445">Belirtilen iş parçacığını askıya alma işlemini durdur</span><span class="sxs-lookup"><span data-stu-id="9fec9-2445">Abort suspension of specified thread</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2446">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2446">Prototype</span></span>

```c
UINT tx_thread_wait_abort(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-2447">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2447">Description</span></span>

<span data-ttu-id="9fec9-2448">Bu hizmet, belirtilen iş parçacığının uyku veya diğer nesne askıya alınma işlemini iptal eder.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2448">This service aborts sleep or any other object suspension of the specified thread.</span></span> <span data-ttu-id="9fec9-2449">Bekleme iptal edildiğinde, iş parçacığının beklediği hizmetten bir **TX_WAIT_ABORTED** değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2449">If the wait is aborted, a **TX_WAIT_ABORTED** value is returned from the service that the thread was waiting on.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2450">*Bu hizmet, tx_thread_suspend hizmeti tarafından yapılan açık askıya alma sürümü oluşturmaz.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2450">*This service does not release explicit suspension that is made by the tx_thread_suspend service.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2451">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2451">Parameters</span></span>

- <span data-ttu-id="9fec9-2452">**thread_ptr** Daha önce oluşturulmuş bir uygulama iş parçacığına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2452">**thread_ptr** Pointer to a previously created application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2453">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2453">Return Values</span></span>

- <span data-ttu-id="9fec9-2454">**TX_SUCCESS** (0x00) başarılı iş parçacığı bekleme iptali.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2454">**TX_SUCCESS** (0x00) Successful thread wait abort.</span></span>
- <span data-ttu-id="9fec9-2455">**TX_THREAD_ERROR** (0x0E) geçersiz uygulama iş parçacığı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2455">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="9fec9-2456">**TX_WAIT_ABORT_ERROR** (0x1B) belirtilen iş parçacığı bekleme durumunda değil.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2456">**TX_WAIT_ABORT_ERROR** (0x1B) Specified thread is not in a waiting state.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2457">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2457">Allowed From</span></span>

<span data-ttu-id="9fec9-2458">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2458">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2459">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2459">Preemption Possible</span></span>
<span data-ttu-id="9fec9-2460">Yes</span><span class="sxs-lookup"><span data-stu-id="9fec9-2460">Yes</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2461">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2461">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Abort the suspension condition of "my_thread." */
status = tx_thread_wait_abort(&my_thread);

/* If status equals TX_SUCCESS, the thread is now ready
again, with a return value showing its suspension
was aborted (TX_WAIT_ABORTED). */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2462">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2462">See Also</span></span>

- <span data-ttu-id="9fec9-2463">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2463">tx_thread_create</span></span>
- <span data-ttu-id="9fec9-2464">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2464">tx_thread_delete</span></span>
- <span data-ttu-id="9fec9-2465">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2465">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="9fec9-2466">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2466">tx_thread_identify</span></span>
- <span data-ttu-id="9fec9-2467">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2467">tx_thread_info_get</span></span>
- <span data-ttu-id="9fec9-2468">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2468">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2469">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2469">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="9fec9-2470">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2470">tx_thread_preemption_change</span></span>
- <span data-ttu-id="9fec9-2471">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2471">tx_thread_priority_change</span></span>
- <span data-ttu-id="9fec9-2472">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="9fec9-2472">tx_thread_relinquish</span></span>
- <span data-ttu-id="9fec9-2473">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="9fec9-2473">tx_thread_reset</span></span>
- <span data-ttu-id="9fec9-2474">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="9fec9-2474">tx_thread_resume</span></span>
- <span data-ttu-id="9fec9-2475">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="9fec9-2475">tx_thread_sleep</span></span>
- <span data-ttu-id="9fec9-2476">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="9fec9-2476">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="9fec9-2477">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="9fec9-2477">tx_thread_suspend</span></span>
- <span data-ttu-id="9fec9-2478">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2478">tx_thread_terminate</span></span>
- <span data-ttu-id="9fec9-2479">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2479">tx_thread_time_slice_change</span></span>

## <a name="tx_time_get"></a><span data-ttu-id="9fec9-2480">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2480">tx_time_get</span></span>

<span data-ttu-id="9fec9-2481">Geçerli saati alır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2481">Retrieves the current time</span></span>

<span data-ttu-id="9fec9-2482">Uygulama zamanlayıcıları</span><span class="sxs-lookup"><span data-stu-id="9fec9-2482">Application Timers</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2483">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2483">Prototype</span></span>

```c
ULONG tx_time_get(VOID);
```

### <a name="description"></a><span data-ttu-id="9fec9-2484">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2484">Description</span></span>

<span data-ttu-id="9fec9-2485">Bu hizmet, iç sistem saatinin içeriğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2485">This service returns the contents of the internal system clock.</span></span> <span data-ttu-id="9fec9-2486">Her timertick, iç sistem saatini bir artırır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2486">Each timertick increases the internal system clock by one.</span></span> <span data-ttu-id="9fec9-2487">Sistem saati, başlatma sırasında sıfır olarak ayarlanır ve hizmet ***tx_time_set*** belirli bir değere değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2487">The system clock is set to zero during initialization and can be changed to a specific value by the service ***tx_time_set***.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2488">*Her Zamanlayıcı-onay her temsil eden gerçek zaman uygulamaya özgüdür.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2488">*The actual time each timer-tick represents is application specific.*</span></span>

<span data-ttu-id="9fec9-2489">**Parametreler**</span><span class="sxs-lookup"><span data-stu-id="9fec9-2489">**Parameters**</span></span>

<span data-ttu-id="9fec9-2490">Yok</span><span class="sxs-lookup"><span data-stu-id="9fec9-2490">None</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2491">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2491">Return Values</span></span>

- <span data-ttu-id="9fec9-2492">**sistem saat işaretleri** İç, ücretsiz çalışan, sistem saatinin değeri.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2492">**system clock ticks** Value of the internal, free running, system clock.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2493">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2493">Allowed From</span></span>

<span data-ttu-id="9fec9-2494">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2494">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2495">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2495">Preemption Possible</span></span>
<span data-ttu-id="9fec9-2496">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2496">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2497">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2497">Example</span></span>

```c
ULONG current_time;

/* Pickup the current system time, in timer-ticks. */
current_time = tx_time_get();

/* Current time now contains a copy of the internal system
clock. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2498">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2498">See Also</span></span>

- <span data-ttu-id="9fec9-2499">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-2499">tx_time_set</span></span>

## <a name="tx_time_set"></a><span data-ttu-id="9fec9-2500">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="9fec9-2500">tx_time_set</span></span>

<span data-ttu-id="9fec9-2501">Geçerli saati ayarlar</span><span class="sxs-lookup"><span data-stu-id="9fec9-2501">Sets the current time</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2502">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2502">Prototype</span></span>

```c
VOID tx_time_set(ULONG new_time);
```

### <a name="description"></a><span data-ttu-id="9fec9-2503">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2503">Description</span></span>

<span data-ttu-id="9fec9-2504">Bu hizmet, iç sistem saatini belirtilen değere ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2504">This service sets the internal system clock to the specified value.</span></span> <span data-ttu-id="9fec9-2505">Her Zamanlayıcı-onay, iç sistem saatini bir artırır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2505">Each timer-tick increases the internal system clock by one.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2506">*Her Zamanlayıcı-onay her temsil eden gerçek zaman uygulamaya özgüdür.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2506">*The actual time each timer-tick represents is application specific.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2507">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2507">Parameters</span></span>

- <span data-ttu-id="9fec9-2508">**new_time** Yeni saat, sistem saatine koymak için geçerli değerler 0 ile 0xFFFFFFFF arasındadır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2508">**new_time** New time to put in the system clock, legal values range from 0 through 0xFFFFFFFF.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2509">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2509">Return Values</span></span>

<span data-ttu-id="9fec9-2510">Yok</span><span class="sxs-lookup"><span data-stu-id="9fec9-2510">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2511">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2511">Allowed From</span></span>

<span data-ttu-id="9fec9-2512">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2512">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2513">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2513">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2514">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2514">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2515">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2515">Example</span></span>

```c
/* Set the internal system time to 0x1234. */
tx_time_set(0x1234);

/* Current time now contains 0x1234 until the next timer
interrupt. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2516">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2516">See Also</span></span>

- <span data-ttu-id="9fec9-2517">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2517">tx_time_get</span></span>

## <a name="tx_timer_activate"></a><span data-ttu-id="9fec9-2518">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2518">tx_timer_activate</span></span>

<span data-ttu-id="9fec9-2519">Uygulama zamanlayıcısını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="9fec9-2519">Activate application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2520">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2520">Prototype</span></span>

```c
UINT tx_timer_activate(TX_TIMER *timer_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-2521">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2521">Description</span></span>

<span data-ttu-id="9fec9-2522">Bu hizmet, belirtilen uygulama zamanlayıcısını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2522">This service activates the specified application timer.</span></span> <span data-ttu-id="9fec9-2523">Aynı anda süresi dolan zamanlayıcılar için geçen süre sonu yordamları, etkinleştirildikleri sırada yürütülür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2523">The expiration routines of timers that expire at the same time are executed in the order they were activated.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2524">*Süre sonu bir tek kararlı Zamanlayıcı, ile*  \* sıfırlanması gerekir **tx_timer_change** _ _before yeniden etkinleştirilebilir. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2524">*An expired one-shot timer must be reset via* ***tx_timer_change** _ _before it can be activated again.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2525">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2525">Parameters</span></span>

- <span data-ttu-id="9fec9-2526">**timer_ptr** Daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2526">**timer_ptr** Pointer to a previously created application timer.</span></span>

<span data-ttu-id="9fec9-2527">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="9fec9-2527">**Return Values**</span></span>

- <span data-ttu-id="9fec9-2528">**TX_SUCCESS** (0x00) başarılı uygulama süreölçeri etkinleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2528">**TX_SUCCESS** (0x00) Successful application timer activation.</span></span>
- <span data-ttu-id="9fec9-2529">**TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2529">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="9fec9-2530">**TX_ACTIVATE_ERROR** (0x17) Zamanlayıcı zaten etkin veya zaten süresi geçmiş tek bir görüntü süreölçeri.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2530">**TX_ACTIVATE_ERROR** (0x17) Timer was already active or is a one-shot timer that has already expired.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2531">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2531">Allowed From</span></span>

<span data-ttu-id="9fec9-2532">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2532">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2533">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2533">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2534">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2534">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2535">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2535">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Activate an application timer. Assume that the
application timer has already been created. */
status = tx_timer_activate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
now active. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2536">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2536">See Also</span></span>

- <span data-ttu-id="9fec9-2537">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2537">tx_timer_change</span></span>
- <span data-ttu-id="9fec9-2538">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2538">tx_timer_create</span></span>
- <span data-ttu-id="9fec9-2539">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2539">tx_timer_deactivate</span></span>
- <span data-ttu-id="9fec9-2540">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2540">tx_timer_delete</span></span>
- <span data-ttu-id="9fec9-2541">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2541">tx_timer_info_get</span></span>
- <span data-ttu-id="9fec9-2542">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2542">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2543">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2543">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_change"></a><span data-ttu-id="9fec9-2544">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2544">tx_timer_change</span></span>

<span data-ttu-id="9fec9-2545">Uygulama zamanlayıcısını değiştirme</span><span class="sxs-lookup"><span data-stu-id="9fec9-2545">Change application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2546">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2546">Prototype</span></span>

```c
UINT tx_timer_change(
    TX_TIMER *timer_ptr,
    ULONG initial_ticks, 
    ULONG reschedule_ticks);
```

### <a name="description"></a><span data-ttu-id="9fec9-2547">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2547">Description</span></span>

<span data-ttu-id="9fec9-2548">Bu hizmet, belirtilen uygulama süreölçerinin süre sonu özelliklerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2548">This service changes the expiration characteristics of the specified application timer.</span></span> <span data-ttu-id="9fec9-2549">Bu hizmet çağrılmadan önce zamanlayıcı devre dışı bırakılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2549">The timer must be deactivated prior to calling this service.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2550">*Öğesine*  \* bir çağrı Zamanlayıcıyı yeniden başlatmak için bu hizmetten sonra **tx_timer_activate** _ _Service gereklidir. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2550">*A call to the* ***tx_timer_activate** _ _service is required after this service in order to start the timer again.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2551">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2551">Parameters</span></span>

- <span data-ttu-id="9fec9-2552">**timer_ptr** Zamanlayıcı denetim bloğunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2552">**timer_ptr** Pointer to a timer control block.</span></span>
- <span data-ttu-id="9fec9-2553">**initial_ticks** Zamanlayıcı süre sonu için başlangıç onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2553">**initial_ticks** Specifies the initial number of ticks for timer expiration.</span></span> <span data-ttu-id="9fec9-2554">Yasal değerler 1 ile 0xFFFFFFFF arasındadır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2554">Legal values range from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="9fec9-2555">**reschedule_ticks** İlk süre sonra tüm süreölçer süre sonları için onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2555">**reschedule_ticks** Specifies the number of ticks for all timer expirations after the first.</span></span> <span data-ttu-id="9fec9-2556">Bu parametre için bir sıfır, zamanlayıcının *tek bir görüntü* süreölçeri olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2556">A zero for this parameter makes the timer a *one-shot* timer.</span></span> <span data-ttu-id="9fec9-2557">Aksi takdirde, düzenli zamanlayıcılar için 1 ile 0xFFFFFFFF arasında geçerli değerler değişir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2557">Otherwise, for periodic timers, legal values range from 1 through 0xFFFFFFFF.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2558">*Süre sonu bir tek kararlı Zamanlayıcı, ile* 
\* sıfırlanması gerekir **tx_timer_change** _ _before yeniden etkinleştirilebilir. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2558">*An expired one-shot timer must be reset via*
***tx_timer_change** _ _before it can be activated again.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2559">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2559">Return Values</span></span>

- <span data-ttu-id="9fec9-2560">**TX_SUCCESS** (0x00) başarılı uygulama süreölçeri değişikliği.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2560">**TX_SUCCESS** (0x00) Successful application timer change.</span></span>
- <span data-ttu-id="9fec9-2561">**TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2561">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="9fec9-2562">**TX_TICK_ERROR** (0x16) ilk Ticks için geçersiz değer (sıfır) sağlandı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2562">**TX_TICK_ERROR** (0x16) Invalid value (a zero) supplied for initial ticks.</span></span>
- <span data-ttu-id="9fec9-2563">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2563">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2564">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2564">Allowed From</span></span>

<span data-ttu-id="9fec9-2565">İş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2565">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2566">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2566">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2567">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2567">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2568">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2568">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Change a previously created and now deactivated timer
to expire every 50 timer ticks, including the initial
expiration. */
status = tx_timer_change(&my_timer,50, 50);

/* If status equals TX_SUCCESS, the specified timer is
changed to expire every 50 ticks. */

/* Activate the specified timer to get it started again. */
status = tx_timer_activate(&my_timer);
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2569">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2569">See Also</span></span>

- <span data-ttu-id="9fec9-2570">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2570">tx_timer_activate</span></span>
- <span data-ttu-id="9fec9-2571">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2571">tx_timer_create</span></span>
- <span data-ttu-id="9fec9-2572">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2572">tx_timer_deactivate</span></span>
- <span data-ttu-id="9fec9-2573">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2573">tx_timer_delete</span></span>
- <span data-ttu-id="9fec9-2574">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2574">tx_timer_info_get</span></span>
- <span data-ttu-id="9fec9-2575">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2575">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2576">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2576">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_create"></a><span data-ttu-id="9fec9-2577">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2577">tx_timer_create</span></span>

<span data-ttu-id="9fec9-2578">Uygulama süreölçeri oluştur</span><span class="sxs-lookup"><span data-stu-id="9fec9-2578">Create application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2579">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2579">Prototype</span></span>

```c
UINT tx_timer_create(
    TX_TIMER *timer_ptr, 
    CHAR *name_ptr,
    VOID (*expiration_function)(ULONG),
    ULONG expiration_input, 
    ULONG initial_ticks,
    ULONG reschedule_ticks, 
    UINT auto_activate);
```

### <a name="description"></a><span data-ttu-id="9fec9-2580">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2580">Description</span></span>

<span data-ttu-id="9fec9-2581">Bu hizmet, belirtilen süre sonu işleviyle ve periyodik olarak bir uygulama süreölçeri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2581">This service creates an application timer with the specified expiration function and periodic.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2582">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2582">Parameters</span></span>

- <span data-ttu-id="9fec9-2583">**timer_ptr** Zamanlayıcı denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="9fec9-2583">**timer_ptr** Pointer to a timer control block</span></span>
- <span data-ttu-id="9fec9-2584">**name_ptr** Süreölçerin adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2584">**name_ptr** Pointer to the name of the timer.</span></span>
- <span data-ttu-id="9fec9-2585">**expiration_function** Süreölçerin süresi dolduğunda çağrılacak uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2585">**expiration_function** Application function to call when the timer expires.</span></span>
- <span data-ttu-id="9fec9-2586">**expiration_input** Zamanlayıcı süresi dolduğunda sona erme işlevine geçirilecek giriş.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2586">**expiration_input** Input to pass to expiration function when timer expires.</span></span>
- <span data-ttu-id="9fec9-2587">**initial_ticks** Zamanlayıcı süre sonu için başlangıç onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2587">**initial_ticks** Specifies the initial number of ticks for timer expiration.</span></span> <span data-ttu-id="9fec9-2588">Yasal değerler 1 ile 0xFFFFFFFF arasındadır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2588">Legal values range from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="9fec9-2589">**reschedule_ticks** İlk süre sonra tüm süreölçer süre sonları için onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2589">**reschedule_ticks** Specifies the number of ticks for all timer expirations after the first.</span></span> <span data-ttu-id="9fec9-2590">Bu parametre için bir sıfır, zamanlayıcının *tek bir görüntü* süreölçeri olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2590">A zero for this parameter makes the timer a *one-shot* timer.</span></span> <span data-ttu-id="9fec9-2591">Aksi takdirde, düzenli zamanlayıcılar için 1 ile 0xFFFFFFFF arasında geçerli değerler değişir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2591">Otherwise, for periodic timers, legal values range from 1 through 0xFFFFFFFF.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9fec9-2592">*Tek bir anlık zamanlayıcı süresi dolduktan sonra, yeniden etkinleştirilmeden önce tx_timer_change aracılığıyla sıfırlanması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2592">*After a one-shot timer expires, it must be reset via   tx_timer_change before it can be activated again.*</span></span>

- <span data-ttu-id="9fec9-2593">**Auto_Activate** Süreölçerin oluşturma sırasında otomatik olarak etkinleştirildiğini belirler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2593">**auto_activate** Determines if the timer is automatically activated during creation.</span></span> <span data-ttu-id="9fec9-2594">Bu değer **TX_AUTO_ACTIVATE** (0x01), süreölçer etkin hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2594">If this value is **TX_AUTO_ACTIVATE** (0x01) the timer is made active.</span></span> <span data-ttu-id="9fec9-2595">Aksi takdirde, **TX_NO_ACTIVATE** (0x00) değeri seçilirse, süreölçer etkin olmayan bir durumda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2595">Otherwise, if the value **TX_NO_ACTIVATE** (0x00) is selected, the timer is created in a non-active state.</span></span> <span data-ttu-id="9fec9-2596">Bu durumda, süreölçer 'in gerçekten başlatılmış olması için sonraki bir **_tx_timer_activate_** hizmet çağrısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2596">In this case, a subsequent **_tx_timer_activate_** service call is necessary to get the timer actually started.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2597">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2597">Return Values</span></span>

- <span data-ttu-id="9fec9-2598">**TX_SUCCESS** (0x00) başarılı uygulama süreölçeri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2598">**TX_SUCCESS** (0x00) Successful application timer creation.</span></span>
- <span data-ttu-id="9fec9-2599">**TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2599">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span> <span data-ttu-id="9fec9-2600">İşaretçi NULL ya da süreölçer zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2600">Either the pointer is NULL or the timer is already created.</span></span>
- <span data-ttu-id="9fec9-2601">**TX_TICK_ERROR** (0x16) ilk Ticks için geçersiz değer (sıfır) sağlandı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2601">**TX_TICK_ERROR** (0x16) Invalid value (a zero) supplied for initial ticks.</span></span>
- <span data-ttu-id="9fec9-2602">**TX_ACTIVATE_ERROR** (0x17) geçersiz etkinleştirme seçildi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2602">**TX_ACTIVATE_ERROR** (0x17) Invalid activation selected.</span></span>
- <span data-ttu-id="9fec9-2603">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2603">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2604">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2604">Allowed From</span></span>

<span data-ttu-id="9fec9-2605">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-2605">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2606">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2606">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2607">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2607">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2608">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2608">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Create an application timer that executes
"my_timer_function" after 100 ticks initially and then
after every 25 ticks. This timer is specified to start
immediately! */
status = tx_timer_create(&my_timer,"my_timer_name",
    my_timer_function, 0x1234, 100, 25,
    TX_AUTO_ACTIVATE);

/* If status equals TX_SUCCESS, my_timer_function will
be called 100 timer ticks later and then called every
25 timer ticks. Note that the value 0x1234 is passed to
my_timer_function every time it is called. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2609">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2609">See Also</span></span>

- <span data-ttu-id="9fec9-2610">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2610">tx_timer_activate</span></span>
- <span data-ttu-id="9fec9-2611">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2611">tx_timer_change</span></span>
- <span data-ttu-id="9fec9-2612">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2612">tx_timer_deactivate</span></span>
- <span data-ttu-id="9fec9-2613">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2613">tx_timer_delete</span></span>
- <span data-ttu-id="9fec9-2614">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2614">tx_timer_info_get</span></span>
- <span data-ttu-id="9fec9-2615">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2615">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2616">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2616">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_deactivate"></a><span data-ttu-id="9fec9-2617">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2617">tx_timer_deactivate</span></span>

<span data-ttu-id="9fec9-2618">Uygulama zamanlayıcısını devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="9fec9-2618">Deactivate application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2619">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2619">Prototype</span></span>

```c
UINT tx_timer_deactivate(TX_TIMER *timer_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-2620">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2620">Description</span></span>

<span data-ttu-id="9fec9-2621">Bu hizmet, belirtilen uygulama zamanlayıcısını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2621">This service deactivates the specified application timer.</span></span> <span data-ttu-id="9fec9-2622">Süreölçer zaten devre dışı bırakılmışsa, bu hizmetin bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2622">If the timer is already deactivated, this service has no effect.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2623">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2623">Parameters</span></span>

- <span data-ttu-id="9fec9-2624">**timer_ptr** Daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2624">**timer_ptr** Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2625">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2625">Return Values</span></span>

- <span data-ttu-id="9fec9-2626">**TX_SUCCESS** (0x00) başarılı uygulama süreölçeri devre dışı bırakma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2626">**TX_SUCCESS** (0x00) Successful application timer deactivation.</span></span>
- <span data-ttu-id="9fec9-2627">**TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2627">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2628">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2628">Allowed From</span></span>

<span data-ttu-id="9fec9-2629">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2629">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2630">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2630">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2631">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2631">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2632">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2632">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Deactivate an application timer. Assume that the
application timer has already been created. */
status = tx_timer_deactivate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
now deactivated. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2633">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2633">See Also</span></span>

- <span data-ttu-id="9fec9-2634">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2634">tx_timer_activate</span></span>
- <span data-ttu-id="9fec9-2635">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2635">tx_timer_change</span></span>
- <span data-ttu-id="9fec9-2636">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2636">tx_timer_create</span></span>
- <span data-ttu-id="9fec9-2637">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2637">tx_timer_delete</span></span>
- <span data-ttu-id="9fec9-2638">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2638">tx_timer_info_get</span></span>
- <span data-ttu-id="9fec9-2639">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2639">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2640">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2640">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_delete"></a><span data-ttu-id="9fec9-2641">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2641">tx_timer_delete</span></span>

<span data-ttu-id="9fec9-2642">Uygulama zamanlayıcısını Sil</span><span class="sxs-lookup"><span data-stu-id="9fec9-2642">Delete application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2643">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2643">Prototype</span></span>

```c
UINT tx_timer_delete(TX_TIMER *timer_ptr);
```

### <a name="description"></a><span data-ttu-id="9fec9-2644">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2644">Description</span></span>

<span data-ttu-id="9fec9-2645">Bu hizmet, belirtilen uygulama zamanlayıcısını siler.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2645">This service deletes the specified application timer.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2646">*Silinen bir zamanlayıcının kullanımını önleyen uygulamanın sorumluluğundadır.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2646">*It is the application's responsibility to prevent use of a deleted timer.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2647">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2647">Parameters</span></span>

- <span data-ttu-id="9fec9-2648">**timer_ptr** Daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2648">**timer_ptr** Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2649">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2649">Return Values</span></span>

- <span data-ttu-id="9fec9-2650">**TX_SUCCESS** (0x00) başarılı uygulama süreölçeri silme.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2650">**TX_SUCCESS** (0x00) Successful application timer deletion.</span></span>
- <span data-ttu-id="9fec9-2651">**TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2651">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="9fec9-2652">**TX_CALLER_ERROR** (0x13) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2652">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2653">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2653">Allowed From</span></span>

<span data-ttu-id="9fec9-2654">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="9fec9-2654">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2655">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2655">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2656">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2656">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2657">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2657">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Delete application timer. Assume that the application
timer has already been created. */
status = tx_timer_delete(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2658">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2658">See Also</span></span>

- <span data-ttu-id="9fec9-2659">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2659">tx_timer_activate</span></span>
- <span data-ttu-id="9fec9-2660">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2660">tx_timer_change</span></span>
- <span data-ttu-id="9fec9-2661">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2661">tx_timer_create</span></span>
- <span data-ttu-id="9fec9-2662">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2662">tx_timer_deactivate</span></span>
- <span data-ttu-id="9fec9-2663">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2663">tx_timer_info_get</span></span>
- <span data-ttu-id="9fec9-2664">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2664">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2665">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2665">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_info_get"></a><span data-ttu-id="9fec9-2666">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2666">tx_timer_info_get</span></span>

<span data-ttu-id="9fec9-2667">Uygulama süreölçeri hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="9fec9-2667">Retrieve information about an application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2668">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2668">Prototype</span></span>

```c
UINT tx_timer_info_get(
    TX_TIMER *timer_ptr, 
    CHAR **name,
    UINT *active,
    ULONG *remaining_ticks,
    ULONG *reschedule_ticks,
    TX_TIMER **next_timer);
```

### <a name="description"></a><span data-ttu-id="9fec9-2669">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2669">Description</span></span>

<span data-ttu-id="9fec9-2670">Bu hizmet, belirtilen uygulama süreölçeri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2670">This service retrieves information about the specified application timer.</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2671">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2671">Parameters</span></span>

- <span data-ttu-id="9fec9-2672">**timer_ptr** Daha önce oluşturulmuş bir uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2672">**timer_ptr** Pointer to a previously created application timer.</span></span>
- <span data-ttu-id="9fec9-2673">**ad** Süreölçerin adına işaretçi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2673">**name** Pointer to destination for the pointer to the timer's name.</span></span>
- <span data-ttu-id="9fec9-2674">**etkin** Süreölçer etkin göstergesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2674">**active** Pointer to destination for the timer active indication.</span></span> <span data-ttu-id="9fec9-2675">Süreölçer devre dışı bırakılırsa veya bu hizmet zamanlayıcının kendisinden çağrılırsa bir **TX_FALSE** değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2675">If the timer is inactive or this service is called from the timer itself, a **TX_FALSE** value is returned.</span></span> <span data-ttu-id="9fec9-2676">Aksi takdirde, süreölçer etkin ise bir **TX_TRUE** değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2676">Otherwise, if the timer is active, a **TX_TRUE** value is returned.</span></span>
- <span data-ttu-id="9fec9-2677">**remaining_ticks** Süreölçer süresi dolmadan önce bırakılan Zamanlayıcı onay işareti sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2677">**remaining_ticks** Pointer to destination for the number of timer ticks left before the timer expires.</span></span>
- <span data-ttu-id="9fec9-2678">**reschedule_ticks** Bu süreölçeri otomatik olarak yeniden çizelgelemek için kullanılacak süreölçer onay işareti sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2678">**reschedule_ticks** Pointer to destination for the number of timer ticks that will be used to automatically reschedule this timer.</span></span> <span data-ttu-id="9fec9-2679">Değer sıfırsa, süreölçer tek bir çekmeydir ve yeniden planlanmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2679">If the value is zero, then the timer is a one-shot and won't be rescheduled.</span></span>
- <span data-ttu-id="9fec9-2680">**next_timer** Sonraki oluşturulan uygulama süreölçerinin işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2680">**next_timer** Pointer to destination for the pointer of the next created application timer.</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2681">*Herhangi bir parametre için **TX_NULL** sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2681">*Supplying a **TX_NULL** for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2682">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2682">Return Values</span></span>

- <span data-ttu-id="9fec9-2683">**TX_SUCCESS** (0x00) başarılı Zamanlayıcı bilgisi alma.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2683">**TX_SUCCESS** (0x00) Successful timer information retrieval.</span></span>
- <span data-ttu-id="9fec9-2684">**TX_TIMER_ERROR** (0x15) geçersiz uygulama süreölçeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2684">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2685">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2685">Allowed From</span></span>

<span data-ttu-id="9fec9-2686">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2686">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="9fec9-2687">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="9fec9-2687">Preemption Possible</span></span>

<span data-ttu-id="9fec9-2688">Hayır</span><span class="sxs-lookup"><span data-stu-id="9fec9-2688">No</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2689">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2689">Example</span></span>

```c
TX_TIMER my_timer;
CHAR *name;
UINT active;
ULONG remaining_ticks;
ULONG reschedule_ticks;
TX_TIMER *next_timer;
UINT status;

/* Retrieve information about the previously created
application timer "my_timer." */
status = tx_timer_info_get(&my_timer, &name,
    &active,&remaining_ticks,
    &reschedule_ticks,
    &next_timer);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2690">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2690">See Also</span></span>

- <span data-ttu-id="9fec9-2691">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2691">tx_timer_activate</span></span>
- <span data-ttu-id="9fec9-2692">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2692">tx_timer_change</span></span>
- <span data-ttu-id="9fec9-2693">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2693">tx_timer_create</span></span>
- <span data-ttu-id="9fec9-2694">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2694">tx_timer_deactivate</span></span>
- <span data-ttu-id="9fec9-2695">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2695">tx_timer_delete</span></span>
- <span data-ttu-id="9fec9-2696">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2696">tx_timer_info_get</span></span>
- <span data-ttu-id="9fec9-2697">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2697">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="9fec9-2698">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2698">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_performance_info_get"></a><span data-ttu-id="9fec9-2699">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2699">tx_timer_performance_info_get</span></span>

<span data-ttu-id="9fec9-2700">Zamanlayıcı performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-2700">Get timer performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2701">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2701">Prototype</span></span>

```c
UINT tx_timer_performance_info_get(
    TX_TIMER *timer_ptr,
    ULONG *activates, 
    ULONG *reactivates,
    ULONG *deactivates, 
    ULONG *expirations,
    ULONG *expiration_adjusts);
```

### <a name="description"></a><span data-ttu-id="9fec9-2702">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2702">Description</span></span>

<span data-ttu-id="9fec9-2703">Bu hizmet, belirtilen uygulama süreölçeri hakkında performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2703">This service retrieves performance information about the specified application timer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-2704">*Işparçacığıx kitaplığı ve uygulaması ile*  \* oluşturulmalıdır Bu hizmetin performans bilgilerini döndürmesi için **TX_TIMER_ENABLE_PERFORMANCE_INFO** _ _defined. \*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2704">*The ThreadX library and application must be built with* ***TX_TIMER_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="9fec9-2705">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9fec9-2705">Parameters</span></span>
- <span data-ttu-id="9fec9-2706">**timer_ptr** Daha önce oluşturulan Zamanlayıcı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2706">**timer_ptr** Pointer to previously created timer.</span></span>
- <span data-ttu-id="9fec9-2707">**etkinleştirir** Bu zamanlayıcıda gerçekleştirilen etkinleştirme isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2707">**activates** Pointer to destination for the number of activation requests performed on this timer.</span></span>
- <span data-ttu-id="9fec9-2708">yeniden **etkinleştirir** Bu dönemsel süreölçer üzerinde gerçekleştirilen otomatik yeniden etkinleştirme sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2708">**reactivates** Pointer to destination for the number of automatic reactivations performed on this periodic timer.</span></span>
- <span data-ttu-id="9fec9-2709">**devre dışı bırakır** Bu zamanlayıcıda gerçekleştirilen devre dışı bırakma isteklerinin sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2709">**deactivates** Pointer to destination for the number of deactivation requests performed on this timer.</span></span>
- <span data-ttu-id="9fec9-2710">**süre sonları** Bu zamanlayıcının süre sonu sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2710">**expirations** Pointer to destination for the number of expirations of this timer.</span></span>
- <span data-ttu-id="9fec9-2711">**expiration_adjusts** Bu zamanlayıcıda gerçekleştirilen iç süre sonu ayarlamaları sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2711">**expiration_adjusts** Pointer to destination for the number of internal expiration adjustments performed on this timer.</span></span> <span data-ttu-id="9fec9-2712">Bu ayarlamalar, varsayılan Zamanlayıcı listesi boyutundan daha büyük olan zamanlayıcılar için süreölçer kesme işlemi sırasında yapılır (varsayılan süre sonu 32 ' den büyük olan zamanlayıcılar).</span><span class="sxs-lookup"><span data-stu-id="9fec9-2712">These adjustments are done in the timer interrupt processing for timers that are larger than the default timer list size (by default timers with expirations greater than 32 ticks).</span></span>

> <span data-ttu-id="9fec9-2713">NOTUN *Herhangi bir parametre için TX_NULL sağlamak, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2713">[NOTE] *Supplying a TX_NULL for any parameter indicates the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2714">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2714">Return Values</span></span>

- <span data-ttu-id="9fec9-2715">**TX_SUCCESS** (0x00) başarılı Zamanlayıcı performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2715">**TX_SUCCESS** (0x00) Successful timer performance get.</span></span>
- <span data-ttu-id="9fec9-2716">**TX_PTR_ERROR** (0x03) geçersiz süreölçer işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2716">**TX_PTR_ERROR** (0x03) Invalid timer pointer.</span></span>
- <span data-ttu-id="9fec9-2717">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2717">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2718">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2718">Allowed From</span></span>

<span data-ttu-id="9fec9-2719">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2719">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2720">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2720">Example</span></span>

```c
TX_TIMER my_timer;
ULONG activates;
ULONG reactivates;
ULONG deactivates;
ULONG expirations;
ULONG expiration_adjusts;

/* Retrieve performance information on the previously created
timer. */
status = tx_timer_performance_info_get(&my_timer, &activates,
    &reactivates,&deactivates, &expirations,
    &expiration_adjusts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2721">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2721">See Also</span></span>

- <span data-ttu-id="9fec9-2722">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2722">tx_timer_activate</span></span>
- <span data-ttu-id="9fec9-2723">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2723">tx_timer_change</span></span>
- <span data-ttu-id="9fec9-2724">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2724">tx_timer_create</span></span>
- <span data-ttu-id="9fec9-2725">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2725">tx_timer_deactivate</span></span>
- <span data-ttu-id="9fec9-2726">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2726">tx_timer_delete</span></span>
- <span data-ttu-id="9fec9-2727">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2727">tx_timer_info_get</span></span>
- <span data-ttu-id="9fec9-2728">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2728">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_performance_system_info_get"></a><span data-ttu-id="9fec9-2729">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2729">tx_timer_performance_system_info_get</span></span>

<span data-ttu-id="9fec9-2730">Zamanlayıcı sistemi performans bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="9fec9-2730">Get timer system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="9fec9-2731">Prototype</span><span class="sxs-lookup"><span data-stu-id="9fec9-2731">Prototype</span></span>

```c
UINT tx_timer_performance_system_info_get(
    ULONG *activates,
    ULONG *reactivates, 
    ULONG *deactivates,
    ULONG *expirations, 
    ULONG *expiration_adjusts);
```

### <a name="description"></a><span data-ttu-id="9fec9-2732">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fec9-2732">Description</span></span>

<span data-ttu-id="9fec9-2733">Bu hizmet, sistemdeki tüm uygulama zamanlayıcıları hakkındaki performans bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2733">This service retrieves performance information about all the application timers in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fec9-2734">*ThreadX kitaplığı ve uygulaması,*  *performans bilgilerini döndürmek için bu hizmetin tanımlanmış* TX_TIMER_ENABLE_PERFORMANCE_INFO oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2734">*The ThreadX library and application must be built with* **TX_TIMER_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

<span data-ttu-id="9fec9-2735">**Parametreler**</span><span class="sxs-lookup"><span data-stu-id="9fec9-2735">**Parameters**</span></span>

- <span data-ttu-id="9fec9-2736">**etkinleştirir** Tüm zamanlayıcılar üzerinde gerçekleştirilen etkinleştirme isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2736">**activates** Pointer to destination for the total number of activation requests performed on all timers.</span></span>
- <span data-ttu-id="9fec9-2737">yeniden **etkinleştirir** Tüm düzenli zamanlayıcıların toplam otomatik yeniden etkinleştirme sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2737">**reactivates** Pointer to destination for the total number of automatic reactivation performed on all periodic timers.</span></span>
- <span data-ttu-id="9fec9-2738">**devre dışı bırakır** Tüm zamanlayıcılar üzerinde gerçekleştirilen devre dışı bırakma isteklerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2738">**deactivates** Pointer to destination for the total number of deactivation requests performed on all timers.</span></span>
- <span data-ttu-id="9fec9-2739">**süre sonları** Tüm zamanlayıcılar üzerindeki toplam süre sonu sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2739">**expirations** Pointer to destination for the total number of expirations on all timers.</span></span>
- <span data-ttu-id="9fec9-2740">**expiration_adjusts** Tüm zamanlayıcılar üzerinde gerçekleştirilen toplam iç sona erme ayarlamaları sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2740">**expiration_adjusts** Pointer to destination for the total number of internal expiration adjustments performed on all timers.</span></span> <span data-ttu-id="9fec9-2741">Bu ayarlamalar, varsayılan Zamanlayıcı listesi boyutundan daha büyük olan zamanlayıcılar için süreölçer kesme işlemi sırasında yapılır (varsayılan süre sonu 32 ' den büyük olan zamanlayıcılar).</span><span class="sxs-lookup"><span data-stu-id="9fec9-2741">These adjustments are done in the timer interrupt processing for timers that are larger than the default timer list size (by default timers with expirations greater than 32 ticks).</span></span>

> [!NOTE]
> <span data-ttu-id="9fec9-2742">*Herhangi bir parametre için **TX_NULL** sağlama, parametrenin gerekli olmadığını gösterir.*</span><span class="sxs-lookup"><span data-stu-id="9fec9-2742">*Supplying a **TX_NULL** for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="9fec9-2743">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="9fec9-2743">Return Values</span></span>

- <span data-ttu-id="9fec9-2744">**TX_SUCCESS** (0x00) başarılı Zamanlayıcı sistem performansı al.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2744">**TX_SUCCESS** (0x00) Successful timer system performance get.</span></span>
- <span data-ttu-id="9fec9-2745">**TX_FEATURE_NOT_ENABLED** (0xFF) sistem, etkin performans bilgileri ile derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2745">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9fec9-2746">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="9fec9-2746">Allowed From</span></span>

<span data-ttu-id="9fec9-2747">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="9fec9-2747">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="9fec9-2748">Örnek</span><span class="sxs-lookup"><span data-stu-id="9fec9-2748">Example</span></span>

```c
ULONG activates;
ULONG reactivates;
ULONG deactivates;
ULONG expirations;
ULONG expiration_adjusts;

/* Retrieve performance information on all previously created
timers. */
status = tx_timer_performance_system_info_get(&activates,
    &reactivates, &deactivates, &expirations,
    &expiration_adjusts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9fec9-2749">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9fec9-2749">See Also</span></span>

- <span data-ttu-id="9fec9-2750">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2750">tx_timer_activate</span></span>
- <span data-ttu-id="9fec9-2751">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="9fec9-2751">tx_timer_change</span></span>
- <span data-ttu-id="9fec9-2752">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="9fec9-2752">tx_timer_create</span></span>
- <span data-ttu-id="9fec9-2753">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="9fec9-2753">tx_timer_deactivate</span></span>
- <span data-ttu-id="9fec9-2754">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="9fec9-2754">tx_timer_delete</span></span>
- <span data-ttu-id="9fec9-2755">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2755">tx_timer_info_get</span></span>
- <span data-ttu-id="9fec9-2756">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="9fec9-2756">tx_timer_performance_info_get</span></span>
