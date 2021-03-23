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
# <a name="chapter-4---module-apis"></a><span data-ttu-id="b0f04-103">Bölüm 4-modül API 'Leri</span><span class="sxs-lookup"><span data-stu-id="b0f04-103">Chapter 4 - Module APIs</span></span>

## <a name="summary-of-module-apis"></a><span data-ttu-id="b0f04-104">Modül API 'Lerinin Özeti</span><span class="sxs-lookup"><span data-stu-id="b0f04-104">Summary of Module APIs</span></span>

<span data-ttu-id="b0f04-105">Aşağıdaki gibi, bir modül için kullanılabilen birkaç ek API işlevi vardır:</span><span class="sxs-lookup"><span data-stu-id="b0f04-105">There are several additional API functions available to a module, as follows:</span></span>

- <span data-ttu-id="b0f04-106">\***txm_module_application_request** _-_Application-yerleşik koda özgü istek</span><span class="sxs-lookup"><span data-stu-id="b0f04-106">***txm_module_application_request** _ - _Application-specific request to resident code*</span></span>
- <span data-ttu-id="b0f04-107">*nesne \* için modül dışında _-_Allocate bellek **txm_module_object_allocate***</span><span class="sxs-lookup"><span data-stu-id="b0f04-107">***txm_module_object_allocate** _ - _Allocate memory outside of module for object*</span></span>
- <span data-ttu-id="b0f04-108">\***txm_module_object_deallocate** _-daha önce ayrılan nesne belleğini _Deallocate \*</span><span class="sxs-lookup"><span data-stu-id="b0f04-108">***txm_module_object_deallocate** _ - _Deallocate previously allocated object memory*</span></span>
- <span data-ttu-id="b0f04-109">\***txm_module_object_pointer_get** _-_Find sistem nesnesi ve nesne işaretçisini al \*</span><span class="sxs-lookup"><span data-stu-id="b0f04-109">***txm_module_object_pointer_get** _ - _Find system object and retrieve object pointer*</span></span>
- <span data-ttu-id="b0f04-110">\***txm_module_object_pointer_get_extended** _-sistem nesnesi _Find ve nesne işaretçisini alma, ad uzunluğu güvenliği \*</span><span class="sxs-lookup"><span data-stu-id="b0f04-110">***txm_module_object_pointer_get_extended** _ - _Find system object and retrieve object pointer, name length safety*</span></span>

## <a name="return-values"></a><span data-ttu-id="b0f04-111">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-111">Return values</span></span>

<span data-ttu-id="b0f04-112">Bazı Azure RTOS API 'Leri için ek hata kodları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b0f04-112">Additional error codes are returned for some Azure RTOS APIs.</span></span> <span data-ttu-id="b0f04-113">Bu ek hata kodları aşağıdaki şekilde tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="b0f04-113">These additional error codes are defined as follows:</span></span>

- <span data-ttu-id="b0f04-114">**TXM_MODULE_INVALID_PROPERTIES** (0xF3): modülün API çağrısı yapmak için doğru özelliklere sahip olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0f04-114">**TXM_MODULE_INVALID_PROPERTIES** (0xF3): Indicates the module does not have the correct properties to make an API call.</span></span> <span data-ttu-id="b0f04-115">Örneğin, izleme API 'Lerini Kullanıcı modunda çağırma.</span><span class="sxs-lookup"><span data-stu-id="b0f04-115">For example, calling trace APIs in user mode.</span></span>
- <span data-ttu-id="b0f04-116">**TXM_MODULE_INVALID_MEMORY** (0xf4): modül tarafından sağlanan belleğin geçersiz olduğunu veya geçersiz bir konumda olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0f04-116">**TXM_MODULE_INVALID_MEMORY** (0xF4): Indicates the memory supplied by the module is invalid or is in an invalid location.</span></span> <span data-ttu-id="b0f04-117">Örneğin, bellek korumalı modüller ' de, nesne denetim bloklarının modülün erişebileceği bellekte yer açmasına izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="b0f04-117">For example, in memory protected modules, object control blocks are not allowed to be located in memory the module can access.</span></span>
- <span data-ttu-id="b0f04-118">**TXM_MODULE_INVALID_CALLBACK** (0xf5): API 'de belirtilen geri çağırma, modülün kodunun aralığının dışında ve bu nedenle geçersiz.</span><span class="sxs-lookup"><span data-stu-id="b0f04-118">**TXM_MODULE_INVALID_CALLBACK** (0xF5): Callback specified in the API is outside the range of the module's code and is therefore invalid.</span></span>

---

## <a name="txm_module_application_request"></a><span data-ttu-id="b0f04-119">txm_module_application_request</span><span class="sxs-lookup"><span data-stu-id="b0f04-119">txm_module_application_request</span></span>

<span data-ttu-id="b0f04-120">Yerleşik koda uygulamaya özgü istek.</span><span class="sxs-lookup"><span data-stu-id="b0f04-120">Application-specific request to resident code.</span></span>

### <a name="prototype"></a><span data-ttu-id="b0f04-121">Prototype</span><span class="sxs-lookup"><span data-stu-id="b0f04-121">Prototype</span></span>

```c
UINT txm_module_application_request(
    ULONG request, 
    ULONG param_1,
    ULONG param_2,
    ULONG param_3);
```

### <a name="description"></a><span data-ttu-id="b0f04-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0f04-122">Description</span></span>

<span data-ttu-id="b0f04-123">Bu hizmet, belirtilen isteği uygulamanın yerleşik bölümüne yapar.</span><span class="sxs-lookup"><span data-stu-id="b0f04-123">This service makes the specified request to the resident portion of the application.</span></span> <span data-ttu-id="b0f04-124">İstek yapısının çağrıdan önce hazırlandığı varsayılır.</span><span class="sxs-lookup"><span data-stu-id="b0f04-124">It is assumed that the request structure is prepared prior to the call.</span></span> <span data-ttu-id="b0f04-125">İsteğin gerçek işleme, ***_txm_module_manager_application_request*** işlevindeki yerleşik kodda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="b0f04-125">The actual processing of the request takes place in the resident code in the function ***_txm_module_manager_application_request***.</span></span> <span data-ttu-id="b0f04-126">Varsayılan olarak, bu işlev boş bırakılır ve yerleşik uygulama geliştiricisinin değiştirmesi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0f04-126">By default, this function is left empty and is designed for the resident application developer to modify.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b0f04-127">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-127">Input parameters</span></span>

- <span data-ttu-id="b0f04-128">**istek** İstek KIMLIĞI (uygulama tanımlı)</span><span class="sxs-lookup"><span data-stu-id="b0f04-128">**request** Request ID (application defined)</span></span>
- <span data-ttu-id="b0f04-129">**param_1** İlk parametre</span><span class="sxs-lookup"><span data-stu-id="b0f04-129">**param_1** First parameter</span></span>
- <span data-ttu-id="b0f04-130">**param_2** İkinci parametre</span><span class="sxs-lookup"><span data-stu-id="b0f04-130">**param_2** Second parameter</span></span>
- <span data-ttu-id="b0f04-131">**param_3** Üçüncü parametre</span><span class="sxs-lookup"><span data-stu-id="b0f04-131">**param_3** Third parameter</span></span>

### <a name="return-values"></a><span data-ttu-id="b0f04-132">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-132">Return values</span></span>

- <span data-ttu-id="b0f04-133">**TX_SUCCESS** (0x00) başarılı istek.</span><span class="sxs-lookup"><span data-stu-id="b0f04-133">**TX_SUCCESS** (0x00) Successful request.</span></span>
- <span data-ttu-id="b0f04-134">**TX_NOT_AVAILABLE** (0x1d) isteği, yerleşik kod tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b0f04-134">**TX_NOT_AVAILABLE** (0x1D) Request not supported by resident code.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b0f04-135">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b0f04-135">Allowed from</span></span>

<span data-ttu-id="b0f04-136">Modül iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b0f04-136">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="b0f04-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="b0f04-137">Example</span></span>

```c
/* Call application resident code with ID=77 and the
   parameters set to 1, 2, 3. */
status = txm_module_application_request(77, 1, 2, 3);

/* If status is TX_SUCCESS the request was successful. */
```

---

## <a name="txm_module_object_allocate"></a><span data-ttu-id="b0f04-138">txm_module_object_allocate</span><span class="sxs-lookup"><span data-stu-id="b0f04-138">txm_module_object_allocate</span></span>

<span data-ttu-id="b0f04-139">Bir modül nesnesi denetim bloğu için nesne havuzunda (yerleşik uygulama tarafından oluşturulan) bellek ayırır.</span><span class="sxs-lookup"><span data-stu-id="b0f04-139">Allocate memory in the object pool (created by the resident application) for a module object control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="b0f04-140">Prototype</span><span class="sxs-lookup"><span data-stu-id="b0f04-140">Prototype</span></span>

```c
UINT txm_module_object_allocate(
   VOID **object_ptr, 
   ULONG object_size);
```

### <a name="description"></a><span data-ttu-id="b0f04-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0f04-141">Description</span></span>

<span data-ttu-id="b0f04-142">Bu hizmet, modülün dışında bir modül nesnesi için bellek ayırır, bu da modülün kodu tarafından nesne denetim bloğunun bozulmasını önlemeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b0f04-142">This service allocates memory for a module object from memory outside of the module, which helps prevent corruption of the object control block by the module's code.</span></span> <span data-ttu-id="b0f04-143">Bellek korumalı sistemlerde, tüm nesne denetim bloklarının oluşturulabilmesi için önce bu API ile ayrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0f04-143">In memory protected systems, all object control blocks must be allocated with this API before they can be created.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b0f04-144">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-144">Input parameters</span></span>

- <span data-ttu-id="b0f04-145">**object_ptr** Başarılı ayırma üzerine nesne işaretçisinin hedefi.</span><span class="sxs-lookup"><span data-stu-id="b0f04-145">**object_ptr** Destination of object pointer on successful allocation.</span></span>
- <span data-ttu-id="b0f04-146">**object_size** Ayrılacak nesnenin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="b0f04-146">**object_size** Size in bytes of the object to be allocated.</span></span>

### <a name="return-values"></a><span data-ttu-id="b0f04-147">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-147">Return values</span></span>

- <span data-ttu-id="b0f04-148">**TX_SUCCESS** (0x00) başarılı nesne ayırma.</span><span class="sxs-lookup"><span data-stu-id="b0f04-148">**TX_SUCCESS** (0x00) Successful object allocate.</span></span>
- <span data-ttu-id="b0f04-149">**TX_NO_MEMORY** (0x10) yeterli bellek yok.</span><span class="sxs-lookup"><span data-stu-id="b0f04-149">**TX_NO_MEMORY** (0x10) Not enough memory.</span></span>
- <span data-ttu-id="b0f04-150">**TX_NOT_AVAILABLE** (0x1d) Modül Yöneticisi, öğesinden ayrılacak bir nesne havuzu oluşturmadı</span><span class="sxs-lookup"><span data-stu-id="b0f04-150">**TX_NOT_AVAILABLE** (0x1D) Module manager has not created an object pool to allocate from</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b0f04-151">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b0f04-151">Allowed from</span></span>

<span data-ttu-id="b0f04-152">Modül iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b0f04-152">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="b0f04-153">Örnek</span><span class="sxs-lookup"><span data-stu-id="b0f04-153">Example</span></span>

```c
TX_QUEUE *queue_pointer;

/* Allocate a control block for a module message queue. */
status = txm_module_object_allocate(&queue_pointer, sizeof(TX_QUEUE));

/* If status is TX_SUCCESS the queue_pointer points to
   memory allocated outside of the module and can be supplied
   to tx_queue_create to create a queue for the module. */
```

### <a name="see-also"></a><span data-ttu-id="b0f04-154">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b0f04-154">See also</span></span>

- <span data-ttu-id="b0f04-155">txm_module_object_deallocate</span><span class="sxs-lookup"><span data-stu-id="b0f04-155">txm_module_object_deallocate</span></span>
- <span data-ttu-id="b0f04-156">txm_module_object_pointer_get</span><span class="sxs-lookup"><span data-stu-id="b0f04-156">txm_module_object_pointer_get</span></span>

---

## <a name="txm_module_object_deallocate"></a><span data-ttu-id="b0f04-157">txm_module_object_deallocate</span><span class="sxs-lookup"><span data-stu-id="b0f04-157">txm_module_object_deallocate</span></span>

<span data-ttu-id="b0f04-158">Önceden ayrılan nesne belleğini serbest bırak</span><span class="sxs-lookup"><span data-stu-id="b0f04-158">Deallocate previously allocated object memory</span></span>

### <a name="prototype"></a><span data-ttu-id="b0f04-159">Prototype</span><span class="sxs-lookup"><span data-stu-id="b0f04-159">Prototype</span></span>

```c
UINT txm_module_object_deallocate(VOID *object_ptr);
```

### <a name="description"></a><span data-ttu-id="b0f04-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0f04-160">Description</span></span>

<span data-ttu-id="b0f04-161">***Bu hizmet artık gerekli olmadığından kullanım dışı*** bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="b0f04-161">***This service has been deprecated because it is no longer needed***.</span></span>

<span data-ttu-id="b0f04-162">Daha önce txm_module_object_allocate \* _ aracılığıyla ayrılan bellek, \*\*\*_ _TX_ \_ _delete hizmetinde \*serbest bırakılır\*\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="b0f04-162">The memory that was previously allocated via ***txm_module_object_allocate\**_ is deallocated in the _*_tx_\__delete service***.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b0f04-163">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-163">Input parameters</span></span>

- <span data-ttu-id="b0f04-164">**object_ptr** Serbest bırakma için nesne işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b0f04-164">**object_ptr** Object pointer to deallocate.</span></span>

### <a name="return-values"></a><span data-ttu-id="b0f04-165">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-165">Return values</span></span>

- <span data-ttu-id="b0f04-166">**TX_SUCCESS** (0x00) başarılı nesne ayırma.</span><span class="sxs-lookup"><span data-stu-id="b0f04-166">**TX_SUCCESS** (0x00) Successful object allocate.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b0f04-167">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b0f04-167">Allowed from</span></span>

<span data-ttu-id="b0f04-168">Modül iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b0f04-168">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="b0f04-169">Örnek</span><span class="sxs-lookup"><span data-stu-id="b0f04-169">Example</span></span>

```c
TX_QUEUE *queue_pointer;

/* Deallocate control block for a module message queue. */
status = txm_module_object_deallocate(queue_pointer);

/* If status is TX_SUCCESS the object memory associated
   with queue_pointer is deallocated. */
```

### <a name="see-also"></a><span data-ttu-id="b0f04-170">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b0f04-170">See also</span></span>

- <span data-ttu-id="b0f04-171">txm_module_object_allocate</span><span class="sxs-lookup"><span data-stu-id="b0f04-171">txm_module_object_allocate</span></span>
- <span data-ttu-id="b0f04-172">txm_module_object_pointer_get</span><span class="sxs-lookup"><span data-stu-id="b0f04-172">txm_module_object_pointer_get</span></span>

---

## <a name="txm_module_object_pointer_get"></a><span data-ttu-id="b0f04-173">txm_module_object_pointer_get</span><span class="sxs-lookup"><span data-stu-id="b0f04-173">txm_module_object_pointer_get</span></span>

<span data-ttu-id="b0f04-174">Sistem nesnesi bul ve nesne işaretçisini al</span><span class="sxs-lookup"><span data-stu-id="b0f04-174">Find system object and retrieve object pointer</span></span>

### <a name="prototype"></a><span data-ttu-id="b0f04-175">Prototype</span><span class="sxs-lookup"><span data-stu-id="b0f04-175">Prototype</span></span>

```c
UINT txm_module_object_pointer_get(
   UINT object_type, CHAR *name, 
   VOID **object_ptr);
```

### <a name="description"></a><span data-ttu-id="b0f04-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0f04-176">Description</span></span>

<span data-ttu-id="b0f04-177">Bu hizmet belirli bir ada sahip belirli bir türün nesne işaretçisini alır.</span><span class="sxs-lookup"><span data-stu-id="b0f04-177">This service retrieves the object pointer of a particular type with a particular name.</span></span> <span data-ttu-id="b0f04-178">Nesne bulunamazsa bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b0f04-178">If the object is not found, an error is returned.</span></span> <span data-ttu-id="b0f04-179">Aksi takdirde, nesne bulunursa, bu nesnenin adresi "object_ptr" içine yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b0f04-179">Otherwise, if the object is found, the address of that object is placed in "object_ptr."</span></span> <span data-ttu-id="b0f04-180">Bu işaretçi daha sonra sistem hizmeti çağrıları yapmak, yerleşik kodla etkileşime geçmek ve/veya sistemdeki diğer yüklü modüller için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b0f04-180">This pointer can then be used to make system service calls, to interact with the resident code, and/or other loaded modules in the system.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b0f04-181">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-181">Input parameters</span></span>

- <span data-ttu-id="b0f04-182">**object_type** İstenen ThreadX nesnesi türü.</span><span class="sxs-lookup"><span data-stu-id="b0f04-182">**object_type** Type of ThreadX object requested.</span></span> <span data-ttu-id="b0f04-183">Geçerli türler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b0f04-183">Valid types are as follows:</span></span>
  - <span data-ttu-id="b0f04-184">TXM_BLOCK_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-184">TXM_BLOCK_POOL_OBJECT</span></span>
  - <span data-ttu-id="b0f04-185">TXM_BYTE_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-185">TXM_BYTE_POOL_OBJECT</span></span>
  - <span data-ttu-id="b0f04-186">TXM_EVENT_FLAGS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-186">TXM_EVENT_FLAGS_OBJECT</span></span>
  - <span data-ttu-id="b0f04-187">TXM_MUTEX_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-187">TXM_MUTEX_OBJECT</span></span>
  - <span data-ttu-id="b0f04-188">TXM_QUEUE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-188">TXM_QUEUE_OBJECT</span></span>
  - <span data-ttu-id="b0f04-189">TXM_SEMAPHORE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-189">TXM_SEMAPHORE_OBJECT</span></span>
  - <span data-ttu-id="b0f04-190">TXM_THREAD_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-190">TXM_THREAD_OBJECT</span></span>
  - <span data-ttu-id="b0f04-191">TXM_TIMER_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-191">TXM_TIMER_OBJECT</span></span>
  - <span data-ttu-id="b0f04-192">TXM_IP_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-192">TXM_IP_OBJECT</span></span>
  - <span data-ttu-id="b0f04-193">TXM_PACKET_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-193">TXM_PACKET_POOL_OBJECT</span></span>
  - <span data-ttu-id="b0f04-194">TXM_UDP_SOCKET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-194">TXM_UDP_SOCKET_OBJECT</span></span>
  - <span data-ttu-id="b0f04-195">TXM_TCP_SOCKET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-195">TXM_TCP_SOCKET_OBJECT</span></span>
- <span data-ttu-id="b0f04-196">**ad** Nesne oluşturulduğunda tanımlanan uygulamaya özgü nesne adı.</span><span class="sxs-lookup"><span data-stu-id="b0f04-196">**name** Application-specific object name as defined when the object was created.</span></span>
- <span data-ttu-id="b0f04-197">**object_ptr** Nesne işaretçisinin hedefi.</span><span class="sxs-lookup"><span data-stu-id="b0f04-197">**object_ptr** Destination for object pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="b0f04-198">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-198">Return values</span></span>

- <span data-ttu-id="b0f04-199">**TX_SUCCESS** (0x00) başarılı nesne Get.</span><span class="sxs-lookup"><span data-stu-id="b0f04-199">**TX_SUCCESS** (0x00) Successful object get.</span></span>
- <span data-ttu-id="b0f04-200">**TX_OPTION_ERROR** (0x08) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="b0f04-200">**TX_OPTION_ERROR** (0x08) Invalid object type.</span></span>
- <span data-ttu-id="b0f04-201">**TX_PTR_ERROR** (0x03) geçersiz hedef.</span><span class="sxs-lookup"><span data-stu-id="b0f04-201">**TX_PTR_ERROR** (0x03) Invalid destination.</span></span>
- <span data-ttu-id="b0f04-202">**TX_SIZE_ERROR** (0x05) geçersiz boyut.</span><span class="sxs-lookup"><span data-stu-id="b0f04-202">**TX_SIZE_ERROR** (0x05) Invalid size.</span></span>
- <span data-ttu-id="b0f04-203">**TX_NO_INSTANCE** (0x0D) nesne bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="b0f04-203">**TX_NO_INSTANCE** (0x0D) Object not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b0f04-204">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b0f04-204">Allowed from</span></span>

<span data-ttu-id="b0f04-205">Modül iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b0f04-205">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="b0f04-206">Örnek</span><span class="sxs-lookup"><span data-stu-id="b0f04-206">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="b0f04-207">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b0f04-207">See also</span></span>

- <span data-ttu-id="b0f04-208">txm_module_manager_object_pointer_get_extended</span><span class="sxs-lookup"><span data-stu-id="b0f04-208">txm_module_manager_object_pointer_get_extended</span></span>

---

## <a name="txm_module_object_pointer_get_extended"></a><span data-ttu-id="b0f04-209">txm_module_object_pointer_get_extended</span><span class="sxs-lookup"><span data-stu-id="b0f04-209">txm_module_object_pointer_get_extended</span></span>

<span data-ttu-id="b0f04-210">Sistem nesnesi bul ve nesne işaretçisini al</span><span class="sxs-lookup"><span data-stu-id="b0f04-210">Find system object and retrieve object pointer</span></span>

### <a name="prototype"></a><span data-ttu-id="b0f04-211">Prototype</span><span class="sxs-lookup"><span data-stu-id="b0f04-211">Prototype</span></span>

```c
UINT txm_module_object_pointer_get_extended(UINT object_type,
                                            CHAR *name,
                                            UINT name_length,
                                            VOID **object_ptr);
```

### <a name="description"></a><span data-ttu-id="b0f04-212">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0f04-212">Description</span></span>

<span data-ttu-id="b0f04-213">Bu hizmet belirli bir ada sahip belirli bir türün nesne işaretçisini alır.</span><span class="sxs-lookup"><span data-stu-id="b0f04-213">This service retrieves the object pointer of a particular type with a particular name.</span></span> <span data-ttu-id="b0f04-214">Nesne bulunamazsa bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b0f04-214">If the object is not found, an error is returned.</span></span> <span data-ttu-id="b0f04-215">Aksi takdirde, nesne bulunursa, bu nesnenin adresi "object_ptr" içine yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b0f04-215">Otherwise, if the object is found, the address of that object is placed in "object_ptr."</span></span> <span data-ttu-id="b0f04-216">Bu işaretçi daha sonra sistem hizmeti çağrıları yapmak, yerleşik kodla etkileşime geçmek ve/veya sistemdeki diğer yüklü modüller için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b0f04-216">This pointer can then be used to make system service calls, to interact with the resident code, and/or other loaded modules in the system.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b0f04-217">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-217">Input parameters</span></span>

- <span data-ttu-id="b0f04-218">**object_type** İstenen ThreadX nesnesi türü.</span><span class="sxs-lookup"><span data-stu-id="b0f04-218">**object_type** Type of ThreadX object requested.</span></span> <span data-ttu-id="b0f04-219">Geçerli türler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b0f04-219">Valid types are as follows:</span></span>
  - <span data-ttu-id="b0f04-220">TXM_BLOCK_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-220">TXM_BLOCK_POOL_OBJECT</span></span>
  - <span data-ttu-id="b0f04-221">TXM_BYTE_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-221">TXM_BYTE_POOL_OBJECT</span></span>
  - <span data-ttu-id="b0f04-222">TXM_EVENT_FLAGS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-222">TXM_EVENT_FLAGS_OBJECT</span></span>
  - <span data-ttu-id="b0f04-223">TXM_MUTEX_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-223">TXM_MUTEX_OBJECT</span></span>
  - <span data-ttu-id="b0f04-224">TXM_QUEUE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-224">TXM_QUEUE_OBJECT</span></span>
  - <span data-ttu-id="b0f04-225">TXM_SEMAPHORE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-225">TXM_SEMAPHORE_OBJECT</span></span>
  - <span data-ttu-id="b0f04-226">TXM_THREAD_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-226">TXM_THREAD_OBJECT</span></span>
  - <span data-ttu-id="b0f04-227">TXM_TIMER_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-227">TXM_TIMER_OBJECT</span></span>
  - <span data-ttu-id="b0f04-228">TXM_IP_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-228">TXM_IP_OBJECT</span></span>
  - <span data-ttu-id="b0f04-229">TXM_PACKET_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-229">TXM_PACKET_POOL_OBJECT</span></span>
  - <span data-ttu-id="b0f04-230">TXM_UDP_SOCKET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-230">TXM_UDP_SOCKET_OBJECT</span></span>
  - <span data-ttu-id="b0f04-231">TXM_TCP_SOCKET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b0f04-231">TXM_TCP_SOCKET_OBJECT</span></span>
- <span data-ttu-id="b0f04-232">**ad** Nesne oluşturulduğunda tanımlanan uygulamaya özgü nesne adı.</span><span class="sxs-lookup"><span data-stu-id="b0f04-232">**name** Application-specific object name as defined when the object was created.</span></span>
- <span data-ttu-id="b0f04-233">**name_length** Ad uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b0f04-233">**name_length** Length of name.</span></span>
- <span data-ttu-id="b0f04-234">**object_ptr** Nesne işaretçisinin hedefi.</span><span class="sxs-lookup"><span data-stu-id="b0f04-234">**object_ptr** Destination for object pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="b0f04-235">Dönüş değerleri</span><span class="sxs-lookup"><span data-stu-id="b0f04-235">Return values</span></span>

- <span data-ttu-id="b0f04-236">**TX_SUCCESS** (0x00) başarılı nesne Get.</span><span class="sxs-lookup"><span data-stu-id="b0f04-236">**TX_SUCCESS** (0x00) Successful object get.</span></span>
- <span data-ttu-id="b0f04-237">**TX_OPTION_ERROR** (0x08) geçersiz nesne türü.</span><span class="sxs-lookup"><span data-stu-id="b0f04-237">**TX_OPTION_ERROR** (0x08) Invalid object type.</span></span>
- <span data-ttu-id="b0f04-238">**TX_PTR_ERROR** (0x03) geçersiz hedef.</span><span class="sxs-lookup"><span data-stu-id="b0f04-238">**TX_PTR_ERROR** (0x03) Invalid destination.</span></span>
- <span data-ttu-id="b0f04-239">**TX_SIZE_ERROR** (0x05) geçersiz boyut.</span><span class="sxs-lookup"><span data-stu-id="b0f04-239">**TX_SIZE_ERROR** (0x05) Invalid size.</span></span>
- <span data-ttu-id="b0f04-240">**TX_NO_INSTANCE** (0x0D) nesne bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="b0f04-240">**TX_NO_INSTANCE** (0x0D) Object not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b0f04-241">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b0f04-241">Allowed from</span></span>

<span data-ttu-id="b0f04-242">Modül iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b0f04-242">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="b0f04-243">Örnek</span><span class="sxs-lookup"><span data-stu-id="b0f04-243">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="b0f04-244">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b0f04-244">See also</span></span>

- <span data-ttu-id="b0f04-245">txm_module_manager_object_pointer_get</span><span class="sxs-lookup"><span data-stu-id="b0f04-245">txm_module_manager_object_pointer_get</span></span>
