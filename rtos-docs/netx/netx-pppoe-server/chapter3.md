---
title: Bölüm 3-Azure RTOS NetX PPPoE sunucu hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX PPPoE sunucu hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d1137fae4dfea428d50e2defed94de6a838b01c6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826602"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-server-services"></a><span data-ttu-id="3bb3d-103">Bölüm 3-Azure RTOS NetX PPPoE sunucu hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="3bb3d-103">Chapter 3 - Description of Azure RTOS NetX PPPoE Server Services</span></span>

<span data-ttu-id="3bb3d-104">Bu bölüm, tüm Azure RTOS NetX PPPoE sunucu hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-104">This chapter contains a description of all Azure RTOS NetX PPPoE Server services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="3bb3d-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="3bb3d-106">**nx_pppoe_server_create**: *bir PPPoE sunucu örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-106">**nx_pppoe_server_create**: *Create a PPPoE Server instance*</span></span>

- <span data-ttu-id="3bb3d-107">**nx_pppoe_server_ac_name_set**: *erişim yoğunlaştırıcı adını ayarla*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-107">**nx_pppoe_server_ac_name_set**: *Set Access Concentrator name*</span></span>

- <span data-ttu-id="3bb3d-108">**nx_pppoe_server_delete**: *bir PPPoE sunucu örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-108">**nx_pppoe_server_delete**: *Delete a PPPoE Server instance*</span></span>

- <span data-ttu-id="3bb3d-109">**nx_pppoe_server_enable**: *PPPoE sunucu hizmetlerini etkinleştirme*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-109">**nx_pppoe_server_enable**: *Enable PPPoE Server services*</span></span>

- <span data-ttu-id="3bb3d-110">**nx_pppoe_server_disable**: *PPPoE sunucu hizmetlerini devre dışı bırak*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-110">**nx_pppoe_server_disable**: *Disable PPPoE Server services*</span></span>

- <span data-ttu-id="3bb3d-111">**nx_pppoe_server_callback_notify_set**: *PPPoE sunucusu geri çağırma bildirim işlevlerini ayarla*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-111">**nx_pppoe_server_callback_notify_set**: *Set PPPoE Server callback notify functions*</span></span>

- <span data-ttu-id="3bb3d-112">**nx_pppoe_server_service_name_set**: *PPPoE sunucu hizmeti adını ayarla*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-112">**nx_pppoe_server_service_name_set**: *Set PPPoE Server service name*</span></span>

- <span data-ttu-id="3bb3d-113">**nx_pppoe_server_session_send**: *PPPoE sunucu verilerini belirtilen oturuma gönder*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-113">**nx_pppoe_server_session_send**: *Send PPPoE Server data to specified session*</span></span>

- <span data-ttu-id="3bb3d-114">**nx_pppoe_server_session_packet_send**: *PPPoE sunucu paketini belirtilen oturuma gönder*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-114">**nx_pppoe_server_session_packet_send**: *Send PPPoE Server packet to specified session*</span></span>

- <span data-ttu-id="3bb3d-115">**nx_pppoe_server_session_terminate**: *belirtilen PPPoE oturumunu Sonlandır*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-115">**nx_pppoe_server_session_terminate**: *Terminate the specified PPPoE session*</span></span>

- <span data-ttu-id="3bb3d-116">**nx_pppoe_server_session_get**: *belirtilen oturum bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="3bb3d-116">**nx_pppoe_server_session_get**: *Get the specified session information*</span></span>

## <a name="nx_pppoe_server_create"></a><span data-ttu-id="3bb3d-117">nx_pppoe_server_create</span><span class="sxs-lookup"><span data-stu-id="3bb3d-117">nx_pppoe_server_create</span></span>

<span data-ttu-id="3bb3d-118">Bir PPPoE sunucu örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="3bb3d-118">Create a PPPoE Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-119">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-119">Prototype</span></span>

```c
UINT nx_pppoe_server_create(NX_PPPOE_SERVER *pppoe_server_ptr,
                            CHAR *name, NX_IP *ip_ptr,
                            UINT interface_index,
                            VOID (*pppoe_link_driver)
                            (struct NX_IP_DRIVER_STRUCT *)
                            NX_PACKET_POOL *pool_ptr,
                            VOID *stack_ptr, ULONG stack_size,
                            UINT priority);
```

### <a name="description"></a><span data-ttu-id="3bb3d-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-120">Description</span></span>

<span data-ttu-id="3bb3d-121">Bu hizmet, belirtilen NetX IP örneği için Kullanıcı tarafından sağlanan bağlantı sürücüsüyle bir PPPoE sunucu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-121">This service creates a PPPoE Server instance with the user supplied link driver for the specified NetX IP instance.</span></span> <span data-ttu-id="3bb3d-122">Bağlantı sürücüsü başlatılmamış ve etkin değilse, PPPoE sunucu yazılımı bağlantı sürücüsünü başlatmaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-122">If link driver has not been initialized, and enabled, PPPoE sever software is responsible initializing the link driver.</span></span>

<span data-ttu-id="3bb3d-123">Ayrıca, uygulamanın, iç paket ayırma için kullanması için, PPPoE sunucu örneği için önceden oluşturulmuş bir paket havuzu sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-123">In addition, the application must supply a previously created packet pool for the PPPoE Server instance to use for internal packet allocation.</span></span>

<span data-ttu-id="3bb3d-124">Genellikle NetX IP iş parçacığını, PPPoE sunucu iş parçacığı önceliğinden daha yüksek bir önceliğe göre oluşturmak iyi bir fikir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-124">Note that it is generally a good idea to create the NetX IP thread at a higher priority than the PPPoE Server thread priority.</span></span> <span data-ttu-id="3bb3d-125">IP iş parçacığı önceliğini belirtme hakkında daha fazla bilgi için lütfen *nx_ip_create* hizmetine bakın.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-125">Please refer to the *nx_ip_create* service for more information on specifying the IP thread priority.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-126">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-126">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-127">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-127">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="3bb3d-128">**ad**: Bu PPPoE sunucu örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-128">**name**: Name of this PPPoE Server instance.</span></span>
- <span data-ttu-id="3bb3d-129">**ip_ptr**: IP örneği için denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-129">**ip_ptr**: Pointer to control block for IP instance.</span></span>
- <span data-ttu-id="3bb3d-130">**interface_index**: arabirim dizini.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-130">**interface_index**: Interface index.</span></span>
- <span data-ttu-id="3bb3d-131">**pppoe_link_driver**: Kullanıcı tarafından sağlanan bağlantı sürücüsü.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-131">**pppoe_link_driver**: User supplied link driver.</span></span>
- <span data-ttu-id="3bb3d-132">**pool_ptr**: paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-132">**pool_ptr**: Pointer to packet pool.</span></span>
- <span data-ttu-id="3bb3d-133">**stack_ptr**: PPPoE sunucu iş parçacığının yığın alanının başlangıcı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-133">**stack_ptr**: Pointer to start of PPPoE Server thread's stack area.</span></span>
- <span data-ttu-id="3bb3d-134">**stack_size**: iş parçacığının yığınında bayt cinsinden boyut.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-134">**stack_size**: Size in bytes in the thread's stack.</span></span>
- <span data-ttu-id="3bb3d-135">**Öncelik**: Iç PPPoE sunucu iş parçacıklarının önceliği (1-31).</span><span class="sxs-lookup"><span data-stu-id="3bb3d-135">**priority**: Priority of internal PPPoE Server threads (1-31).</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-136">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-136">Return Values</span></span>

- <span data-ttu-id="3bb3d-137">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı bir PPPoE sunucu oluştur.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-137">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server create.</span></span>
- <span data-ttu-id="3bb3d-138">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucusu, IP, paket havuzu veya yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-138">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server, IP, packet pool, or stack pointer.</span></span>
- <span data-ttu-id="3bb3d-139">NX_PPPOE_SERVER_INVALID_INTERFACE: (0xC2) geçersiz arabirim.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-139">NX_PPPOE_SERVER_INVALID_INTERFACE: (0xC2) Invalid interface.</span></span>
- <span data-ttu-id="3bb3d-140">NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) paket havuzunun yük boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-140">NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) Invalid payload size of packet pool.</span></span>
- <span data-ttu-id="3bb3d-141">NX_PPPOE_SERVER_MEMORY_SIZE_ERROR: (0xC4) geçersiz bellek boyutu.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-141">NX_PPPOE_SERVER_MEMORY_SIZE_ERROR: (0xC4) Invalid memory size.</span></span>
- <span data-ttu-id="3bb3d-142">NX_PPPOE_SERVER_PRIORITY_ERROR: (0xC5) PPPoE sunucu iş parçacığının geçersiz önceliği.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-142">NX_PPPOE_SERVER_PRIORITY_ERROR: (0xC5) Invalid priority of PPPoE Server thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-143">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-143">Allowed From</span></span>

<span data-ttu-id="3bb3d-144">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-144">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-145">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-145">Example</span></span>

```c
/* Create "my_pppoe_server" for IP instance "my_ip". */
status = nx_pppoe_server_create(&my_pppoe_server, "my PPPoE Server", &my_ip,
                                &my_pool, stack_start, 1024, 2);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully created. */
```

## <a name="nx_pppoe_server_delete"></a><span data-ttu-id="3bb3d-146">nx_pppoe_server_delete</span><span class="sxs-lookup"><span data-stu-id="3bb3d-146">nx_pppoe_server_delete</span></span>

<span data-ttu-id="3bb3d-147">Bir PPPoE sunucu örneğini silme</span><span class="sxs-lookup"><span data-stu-id="3bb3d-147">Delete a PPPoE Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-148">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-148">Prototype</span></span>

```c
UINT nx_pppoe_server_delete(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a><span data-ttu-id="3bb3d-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-149">Description</span></span>

<span data-ttu-id="3bb3d-150">Bu hizmet, önceden oluşturulmuş olan PPPoE sunucu örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-150">This service deletes the previously created PPPoE Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-151">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-151">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-152">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-152">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-153">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-153">Return Values</span></span>

- <span data-ttu-id="3bb3d-154">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-154">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="3bb3d-155">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-155">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-156">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-156">Allowed From</span></span>

<span data-ttu-id="3bb3d-157">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-157">Threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-158">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-158">Example</span></span>

```c
/* Delete PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_delete(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" was successfully deleted. */
```

## <a name="nx_pppoe_server_enable"></a><span data-ttu-id="3bb3d-159">nx_pppoe_server_enable</span><span class="sxs-lookup"><span data-stu-id="3bb3d-159">nx_pppoe_server_enable</span></span>

<span data-ttu-id="3bb3d-160">PPPoE sunucu hizmetini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3bb3d-160">Enable PPPoE Server service</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-161">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-161">Prototype</span></span>

```c
UINT nx_pppoe_server_enable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a><span data-ttu-id="3bb3d-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-162">Description</span></span>

<span data-ttu-id="3bb3d-163">Bu hizmet, PPPoE sunucu hizmetlerini sunar.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-163">This service enables the PPPoE Server services.</span></span>

> [!NOTE]
> <span data-ttu-id="3bb3d-164">Bu işlev, *nx_pppoe_server_create* ve *nx_pppoe_server_callback_notify_set* sonra çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-164">This function must be called after *nx_pppoe_server_create* and *nx_pppoe_server_callback_notify_set*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-165">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-165">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-166">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-166">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-167">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-167">Return Values</span></span>

- <span data-ttu-id="3bb3d-168">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-168">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="3bb3d-169">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-169">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-170">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-170">Allowed From</span></span>

<span data-ttu-id="3bb3d-171">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-171">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-172">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-172">Example</span></span>

```c
/* Enable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_enable(&my_pppoe_server);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has enabled. */
```

## <a name="nx_pppoe_server_disable"></a><span data-ttu-id="3bb3d-173">nx_pppoe_server_disable</span><span class="sxs-lookup"><span data-stu-id="3bb3d-173">nx_pppoe_server_disable</span></span>

<span data-ttu-id="3bb3d-174">PPPoE sunucu hizmetini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="3bb3d-174">Disable PPPoE Server service</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-175">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-175">Prototype</span></span>

```c
UINT nx_pppoe_server_disable(NX_PPPOE_SERVER *pppoe_server_ptr);
```

### <a name="description"></a><span data-ttu-id="3bb3d-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-176">Description</span></span>

<span data-ttu-id="3bb3d-177">Bu hizmet, PPPoE sunucu hizmetlerini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-177">This service disables the PPPoE Server services.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-178">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-178">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-179">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-179">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-180">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-180">Return Values</span></span>

- <span data-ttu-id="3bb3d-181">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-181">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="3bb3d-182">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-182">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-183">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-183">Allowed From</span></span>

<span data-ttu-id="3bb3d-184">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-184">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-185">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-185">Example</span></span>

```c
/* Disable PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_disable(&my_pppoe_server);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service has disabled. */
```

## <a name="nx_pppoe_server_callback_notify_set"></a><span data-ttu-id="3bb3d-186">nx_pppoe_server_callback_notify_set</span><span class="sxs-lookup"><span data-stu-id="3bb3d-186">nx_pppoe_server_callback_notify_set</span></span>

<span data-ttu-id="3bb3d-187">PPPoE sunucusu geri çağırma bildirim işlevlerini ayarla</span><span class="sxs-lookup"><span data-stu-id="3bb3d-187">Set PPPoE Server callback notify functions</span></span> 

### <a name="prototype"></a><span data-ttu-id="3bb3d-188">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-188">Prototype</span></span>

```c
UINT nx_pppoe_server_callback_notify_set(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        VOID (* pppoe_discover_initiation_notify)(UINT session_index,
                ULONG length, UCHAR *data),
        VOID (* pppoe_discover_request_notify)(UINT session_index),
        VOID (* pppoe_discover_terminate_notify)(UINT session_index),
        VOID (* pppoe_discover_terminate_confirm)(UINT session_index),
        VOID (* pppoe_data_receive_notify)(UINT session_index,
                ULONG length, UCHAR *data, UINT packet_id),
        VOID (* pppoe_discover_notify)(UINT session_index, UCHAR *data))
```

### <a name="description"></a><span data-ttu-id="3bb3d-189">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-189">Description</span></span>

<span data-ttu-id="3bb3d-190">Bu hizmet, PPPoE sunucu geri çağırma bildirim işlevlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-190">This service sets PPPoE Server callback notify functions.</span></span>

> [!NOTE]
> <span data-ttu-id="3bb3d-191">Bu işlev nx_pppoe_server_enabl önce çağrılmalıdır *ve* pppoe_data_receive_notify işlev işaretçisinin ayarlanması gerekir, aksi takdirde *nx_pppoe_server_enable* hata olur.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-191">This function must be called before *nx_pppoe_server_enabl, and* the pppoe_data_receive_notify function pointer must be set, if not, *nx_pppoe_server_enable* will be failure.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-192">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-192">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-193">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-193">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="3bb3d-194">**pppoe_discover_initiation_notify**: her PPPoE bulma başlatma iletisi alındığında çağrılan uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-194">**pppoe_discover_initiation_notify**: Application function that is called whenever PPPoE discover initiation message is received.</span></span> <span data-ttu-id="3bb3d-195">Bu değer NULL ise, başlatma geri çağırma işlevini bul seçeneği devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-195">If this value is NULL, discover initiation callback function is disabled.</span></span>
- <span data-ttu-id="3bb3d-196">**pppoe_discover_request_notify**: PPPoE bulma isteği iletisi alındığında çağrılan uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-196">**pppoe_discover_request_notify**: Application function that is called whenever PPPoE discover request message is received.</span></span> <span data-ttu-id="3bb3d-197">Bu değer NULL ise, bulma isteği geri çağırma işlevi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-197">If this value is NULL, discover request callback function is disabled.</span></span>
- <span data-ttu-id="3bb3d-198">**pppoe_discover_terminate_notify**: PPPoE bulma sonlandırma iletisi alındığında çağrılan uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-198">**pppoe_discover_terminate_notify**: Application function that is called whenever PPPoE discover terminate message is received.</span></span> <span data-ttu-id="3bb3d-199">Bu değer NULL ise, bulma Sonlandır geri aramayı bul işlevi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-199">If this value is NULL, discover terminate callback function is disabled.</span></span>
- <span data-ttu-id="3bb3d-200">**pppoe_discover_terminate_confirm**: PPPoE her sonlandırma iletisi gönderildiğinde çağrılan uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-200">**pppoe_discover_terminate_confirm**: Application function that is called whenever PPPoE discover terminate message is sent.</span></span> <span data-ttu-id="3bb3d-201">Bu değer NULL ise, bulma Sonlandır geri aramayı bul işlevi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-201">If this value is NULL, discover terminate callback function is disabled.</span></span>
- <span data-ttu-id="3bb3d-202">**pppoe_data_receive_notify**: PPPoE veri iletisi alındığında çağrılan uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-202">**pppoe_data_receive_notify**: Application function that is called whenever PPPoE data message is received.</span></span> <span data-ttu-id="3bb3d-203">Bu değer sıfır olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-203">This value must not be zero.</span></span>
- <span data-ttu-id="3bb3d-204">**pppoe_data_send_notify**: PPPoE veri iletisi gönderildiğinde çağrılan uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-204">**pppoe_data_send_notify**: Application function that is called whenever PPPoE data message is sent.</span></span> <span data-ttu-id="3bb3d-205">Bu değer NULL ise, veri geri arama gönder işlevi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-205">If this value is NULL, data send callback function is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-206">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-206">Return Values</span></span>

- <span data-ttu-id="3bb3d-207">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-207">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="3bb3d-208">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi veya işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-208">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer or function pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-209">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-209">Allowed From</span></span>

<span data-ttu-id="3bb3d-210">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-210">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-211">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-211">Example</span></span>

```c
/* Set PPPoE Server callback notify functions, PPPoE Server instance "my_pppoe_server". */

status = nx_pppoe_server_disable(&my_pppoe_server,
                pppoe_discovery_initiation_notify,
                pppoe_discovery_request_notify,
                pppoe_discovery_terminate_notify,
                pppoe_discovery_terminate_confirm,
                pppoe_data_receive_notify,
                pppoe_data_send_notify);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the callback notify functions for "my_pppoe_server" service has set. */
```

## <a name="nx_pppoe_server_ac_name_set"></a><span data-ttu-id="3bb3d-212">nx_pppoe_server_ac_name_set</span><span class="sxs-lookup"><span data-stu-id="3bb3d-212">nx_pppoe_server_ac_name_set</span></span>

<span data-ttu-id="3bb3d-213">Erişim yoğunlaştırıcı adını ayarla</span><span class="sxs-lookup"><span data-stu-id="3bb3d-213">Set Access Concentrator name</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-214">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-214">Prototype</span></span>

```c
UINT nx_pppoe_server_ac_name_set(
    NX_PPPOE_SERVER *pppoe_server_ptr,
    CHAR *ac_name, UINT ac_name_length,
);
```

### <a name="description"></a><span data-ttu-id="3bb3d-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-215">Description</span></span>

<span data-ttu-id="3bb3d-216">Bu işlev, erişim yoğunlaştırıcı adı işlev çağrısını ayarladı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-216">This function set Access Concentrator name function call.</span></span>

> [!NOTE]
> <span data-ttu-id="3bb3d-217">Ac_name dizesi NULL sonlandırılmış olmalı ve ac_name uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşiyor.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-217">The string of ac_name must be NULL-terminated and length of ac_name matches the length specified in the argument list.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-218">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-218">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-219">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-219">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="3bb3d-220">**ac_name**: erişim yoğunlaştırıcı adı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-220">**ac_name**: Access Concentrator name.</span></span>
- <span data-ttu-id="3bb3d-221">**ac_name_length**: ac_ame uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-221">**ac_name_length**: Length of ac_ame.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-222">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-222">Return Values</span></span>

- <span data-ttu-id="3bb3d-223">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı bir PPPoE sunucu kümesi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-223">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server set.</span></span>
- <span data-ttu-id="3bb3d-224">**NX_PPPOE_SERVER_PTR_ERROR**: (0xC1) geçersiz PPPoE sunucusu, IP, paket havuzu veya yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-224">**NX_PPPOE_SERVER_PTR_ERROR**: (0xC1) Invalid PPPoE Server, IP, packet pool, or stack pointer.</span></span>
- <span data-ttu-id="3bb3d-225">**NX_SIZE_ERROR**: (0x09) denetim name_length başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-225">**NX_SIZE_ERROR**: (0x09) Check name_length fail.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-226">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-226">Allowed From</span></span>

<span data-ttu-id="3bb3d-227">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-227">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-228">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-228">Example</span></span>

```c
/* Set "my PPPoE ac name" for Server instance "my_pppoe_server". */
status = nx_pppoe_server_ac_name_set(&my_pppoe_server, "my PPPoE ac name",16);

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my PPPoE ac name" was successfully set. */
```

## <a name="nx_pppoe_server_service_name_set"></a><span data-ttu-id="3bb3d-229">nx_pppoe_server_service_name_set</span><span class="sxs-lookup"><span data-stu-id="3bb3d-229">nx_pppoe_server_service_name_set</span></span>

<span data-ttu-id="3bb3d-230">PPPoE sunucu hizmeti adını ayarla</span><span class="sxs-lookup"><span data-stu-id="3bb3d-230">Set PPPoE Server service name</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-231">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-231">Prototype</span></span>

```c
UINT nx_pppoe_server_service_name_set(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UCHAR **service_name, UINT service_name_count);
```

### <a name="description"></a><span data-ttu-id="3bb3d-232">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-232">Description</span></span>

<span data-ttu-id="3bb3d-233">Bu hizmet, PPPoE sunucu hizmeti adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-233">This service sets PPPoE Server service name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-234">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-234">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-235">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-235">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-236">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-236">Return Values</span></span>

- <span data-ttu-id="3bb3d-237">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-237">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="3bb3d-238">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-238">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-239">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-239">Allowed From</span></span>

<span data-ttu-id="3bb3d-240">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-240">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-241">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-241">Example</span></span>

```c
CHAR *nx_pppoe_service_name[] =
{
    "XBB",
    "PRINTER",
    NX_NULL
};

/* Set service name for PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_service_namet_set(&my_pppoe_server,
                                    nx_pppoe_service_name, 2);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" service name has set. */
```

## <a name="nx_pppoe_server_session_send"></a><span data-ttu-id="3bb3d-242">nx_pppoe_server_session_send</span><span class="sxs-lookup"><span data-stu-id="3bb3d-242">nx_pppoe_server_session_send</span></span>

<span data-ttu-id="3bb3d-243">PPPoE sunucu verilerini belirtilen oturuma gönder</span><span class="sxs-lookup"><span data-stu-id="3bb3d-243">Send PPPoE Server data to specified session</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-244">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-244">Prototype</span></span>

```c
UINT nx_pppoe_server_session_send (NX_PPPOE_SERVER *pppoe_server_ptr,
                UINT session_index, UCHAR *data_ptr, UINT data_length);
```

### <a name="description"></a><span data-ttu-id="3bb3d-245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-245">Description</span></span>

<span data-ttu-id="3bb3d-246">Bu hizmet, belirtilen oturum KIMLIĞINI kullanarak PPPoE çerçevesini gönderir.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-246">This service sends PPPoE frame using specified session ID.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-247">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-247">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-248">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-248">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="3bb3d-249">**session_index**: oturumun dizini.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-249">**session_index**: The index of session.</span></span>
- <span data-ttu-id="3bb3d-250">**data_ptr**: PPPoE sunucu veri çerçevesinin başlangıcı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-250">**data_ptr**: Pointer to start of PPPoE Server data frame.</span></span>
- <span data-ttu-id="3bb3d-251">**data_length**: PPPoE sunucu veri çerçevesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-251">**data_length**: Length of PPPoE Server data frame.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-252">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-252">Return Values</span></span>

- <span data-ttu-id="3bb3d-253">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-253">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="3bb3d-254">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-254">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>
- <span data-ttu-id="3bb3d-255">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE sunucu hizmeti etkin değil.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-255">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE Server service is not enabled.</span></span>
- <span data-ttu-id="3bb3d-256">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) geçersiz PPPoE oturum dizini.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-256">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Invalid PPPoE session index.</span></span>
- <span data-ttu-id="3bb3d-257">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE oturumu kurulmadı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-257">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-258">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-258">Allowed From</span></span>

<span data-ttu-id="3bb3d-259">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-259">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-260">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-260">Example</span></span>

```c
/* Send PPPoE Server data to specified session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_send(&my_pppoe_server, 0, my_data_ptr, 1400);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" data has sent. */
```

## <a name="nx_pppoe_server_session_packet_send"></a><span data-ttu-id="3bb3d-261">nx_pppoe_server_session_packet_send</span><span class="sxs-lookup"><span data-stu-id="3bb3d-261">nx_pppoe_server_session_packet_send</span></span>

<span data-ttu-id="3bb3d-262">PPPoE sunucu paketini belirtilen oturuma gönder</span><span class="sxs-lookup"><span data-stu-id="3bb3d-262">Send PPPoE Server packet to specified session</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-263">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-263">Prototype</span></span>

```c
UINT nx_pppoe_server_session_packet_send (
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UINT session_index, NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="3bb3d-264">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-264">Description</span></span>

<span data-ttu-id="3bb3d-265">Bu hizmet, belirtilen oturum KIMLIĞINI kullanarak PPPoE paketi gönderir.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-265">This service sends PPPoE packet using specified session ID.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-266">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-266">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-267">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-267">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="3bb3d-268">**session_index**: oturumun dizini.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-268">**session_index**: The index of session.</span></span>
- <span data-ttu-id="3bb3d-269">**packet_ptr**: PPPoE paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-269">**packet_ptr**: Pointer to PPPoE packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-270">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-270">Return Values</span></span>

- <span data-ttu-id="3bb3d-271">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-271">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="3bb3d-272">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-272">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>
- <span data-ttu-id="3bb3d-273">NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) geçersiz PPPoE sunucu paketi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-273">NX_PPPOE_SERVER_PACKET_PAYLOAD_ERROR: (0xC3) Invalid PPPoE Server packet.</span></span>
- <span data-ttu-id="3bb3d-274">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE sunucu hizmeti etkin değil.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-274">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE Server service is not enabled.</span></span>
- <span data-ttu-id="3bb3d-275">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) geçersiz PPPoE oturum dizini.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-275">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Invalid PPPoE session index.</span></span>
- <span data-ttu-id="3bb3d-276">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE oturumu kurulmadı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-276">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-277">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-277">Allowed From</span></span>

<span data-ttu-id="3bb3d-278">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-278">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-279">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-279">Example</span></span>

```c
/* Send PPPoE Server data to specified session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_packet_send(&my_pppoe_server, 0, packet_ptr);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the "my_pppoe_server" packet has sent. */
```

## <a name="nx_pppoe_server_session_terminate"></a><span data-ttu-id="3bb3d-280">nx_pppoe_server_session_terminate</span><span class="sxs-lookup"><span data-stu-id="3bb3d-280">nx_pppoe_server_session_terminate</span></span>

<span data-ttu-id="3bb3d-281">Belirtilen PPPoE oturumunu Sonlandır</span><span class="sxs-lookup"><span data-stu-id="3bb3d-281">Terminate the specified PPPoE session</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-282">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-282">Prototype</span></span>

```c
UINT nx_pppoe_server_session_terminate(
        NX_PPPOE_SERVER *pppoe_server_ptr,
        UINT session_index);
```

### <a name="description"></a><span data-ttu-id="3bb3d-283">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-283">Description</span></span>

<span data-ttu-id="3bb3d-284">Bu hizmet, belirtilen PPPoE oturumunu sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-284">This service terminates the specified PPPoE session.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-285">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-285">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-286">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-286">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="3bb3d-287">**session_index**: oturumun dizini.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-287">**session_index**: The index of session.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-288">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-288">Return Values</span></span>

- <span data-ttu-id="3bb3d-289">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-289">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="3bb3d-290">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-290">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>
- <span data-ttu-id="3bb3d-291">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE sunucu hizmeti etkin değil.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-291">NX_PPPOE_SERVER_NOT_ENABLED: (0xC6) PPPoE Server service is not enabled.</span></span>
- <span data-ttu-id="3bb3d-292">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) geçersiz PPPoE oturum dizini.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-292">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Invalid PPPoE session index.</span></span>
- <span data-ttu-id="3bb3d-293">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE oturumu kurulmadı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-293">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-294">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-294">Allowed From</span></span>

<span data-ttu-id="3bb3d-295">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-295">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-296">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-296">Example</span></span>

```c
/* Terminates the specified PPPoE session, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_send(&my_pppoe_server, 0);  

/* If status is NX_PPPOE_SERVER_SUCCESS, the session indexed with 0 has terminated. */
```

## <a name="nx_pppoe_server_session_get"></a><span data-ttu-id="3bb3d-297">nx_pppoe_server_session_get</span><span class="sxs-lookup"><span data-stu-id="3bb3d-297">nx_pppoe_server_session_get</span></span>

<span data-ttu-id="3bb3d-298">Belirtilen PPPoE oturum bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="3bb3d-298">Get the specified PPPoE session information</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-299">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-299">Prototype</span></span>

```c
UINT nx_pppoe_server_session_get(NX_PPPOE_SERVER *pppoe_server_ptr,
                                UINT session_index
                                ULONG *client_mac_msw,
                                ULONG *client_mac_lsw,
                                ULONG *session_id);
```

### <a name="description"></a><span data-ttu-id="3bb3d-300">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-300">Description</span></span>

<span data-ttu-id="3bb3d-301">Bu hizmet, belirtilen PPPoE oturum bilgilerini, istemci fiziksel adresini ve oturum kimliğini alır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-301">This service gets the specified PPPoE session information, client physical address and session id.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-302">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-302">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-303">**pppoe_server_ptr**: PPPoE sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-303">**pppoe_server_ptr**: Pointer to PPPoE Server control block.</span></span>
- <span data-ttu-id="3bb3d-304">**session_index**: oturumun dizini.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-304">**session_index**: The index of session.</span></span>
- <span data-ttu-id="3bb3d-305">**client_mac_msw**: istemci fiziksel adresi MSW işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-305">**client_mac_msw**: Client Physical address MSW pointer.</span></span>
- <span data-ttu-id="3bb3d-306">**client_mac_lsw**: istemci fiziksel adresi MSW işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-306">**client_mac_lsw**: Client Physical address MSW pointer.</span></span>
- <span data-ttu-id="3bb3d-307">**session_id**: oturum kimliği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-307">**session_id**: Session ID pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-308">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-308">Return Values</span></span>

- <span data-ttu-id="3bb3d-309">**NX_PPPOE_SERVER_SUCCESS**: (0x00) başarılı PPPoE sunucu silme.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-309">**NX_PPPOE_SERVER_SUCCESS**: (0x00) Successful PPPoE Server delete.</span></span>
- <span data-ttu-id="3bb3d-310">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) geçersiz PPPoE sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-310">NX_PPPOE_SERVER_PTR_ERROR: (0xC1) Invalid PPPoE Server pointer.</span></span>
- <span data-ttu-id="3bb3d-311">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) geçersiz PPPoE oturum dizini.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-311">NX_PPPOE_SERVER_INVALID_SESSION: (0xC7) Invalid PPPoE session index.</span></span>
- <span data-ttu-id="3bb3d-312">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE oturumu kurulmadı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-312">NX_PPPOE_SERVER_SESSION_NOT_ESTABLISHED: (0xC8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-313">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-313">Allowed From</span></span>

<span data-ttu-id="3bb3d-314">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-314">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-315">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-315">Example</span></span>

```c
/* Gets the specified PPPoE session information, PPPoE Server instance "my_pppoe_server". */
status = nx_pppoe_server_session_get (&my_pppoe_server, 0, &client_mac_msw, &client_mac_lsw, &session_id);

/* If status is NX_PPPOE_SERVER_SUCCESS, the client physical address and session id of the session indexed with 0 has got. */
```

## <a name="pppinitind"></a><span data-ttu-id="3bb3d-316">PppInitInd</span><span class="sxs-lookup"><span data-stu-id="3bb3d-316">PppInitInd</span></span>

<span data-ttu-id="3bb3d-317">Varsayılan hizmet adını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3bb3d-317">Configure the default Service Name</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-318">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-318">Prototype</span></span>

```c
VOID PppInitnd(UINT length, UCHAR *aData);
```

### <a name="description"></a><span data-ttu-id="3bb3d-319">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-319">Description</span></span>

<span data-ttu-id="3bb3d-320">Bu işlevin, TTP 'nin, PPPoE 'nin gelen PADI isteklerini filtrelemek için kullanması gereken ' varsayılan hizmet adı ' öğesini yapılandırmasına izin vermek için bu işlevi kullanıma sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-320">The PPPoE software will expose this function to allow TTP's software to configure the 'default Service Name' that the PPPoE should use to filter incoming PADI requests.</span></span> <span data-ttu-id="3bb3d-321">PPPoE yazılımı bu bilgileri unutmalıdır ve eşleşen bir hizmet adı içeren bir PADI paketi alınmışsa PppDiscoverReq öğesini çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-321">The PPPoE software should remember this information, and if a PADI packet is received containing a service name that matches then it should call PppDiscoverReq.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-322">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-322">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-323">**uzunluk**: varsayılan hizmet adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-323">**length**: Length of default service name.</span></span>
- <span data-ttu-id="3bb3d-324">**ADATA**: varsayılan hizmet adı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-324">**aData**: Default service name.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-325">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-325">Return Values</span></span>

<span data-ttu-id="3bb3d-326">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="3bb3d-326">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-327">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-327">Allowed From</span></span>

<span data-ttu-id="3bb3d-328">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-328">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-329">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-329">Example</span></span>

```c
/* Configure the default Service Name. */
PppInitInd (3, "XBB");
```

## <a name="pppdiscovercnf"></a><span data-ttu-id="3bb3d-330">PppDiscoverCnf</span><span class="sxs-lookup"><span data-stu-id="3bb3d-330">PppDiscoverCnf</span></span>

<span data-ttu-id="3bb3d-331">PADO paketinin hizmet adı alanını tanımlayın</span><span class="sxs-lookup"><span data-stu-id="3bb3d-331">Define the Service Name field of the PADO packet</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-332">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-332">Prototype</span></span>

```c
VOID PppDiscoverCnf (UINT length, UCHAR *aData, UINT interfaceHandle);
```

### <a name="description"></a><span data-ttu-id="3bb3d-333">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-333">Description</span></span>

<span data-ttu-id="3bb3d-334">PPPoE yazılımı, TTP yazılımının PADO paketinin hizmet adı alanını tanımlamasına izin vermek için bu işlevi kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-334">The PPPoE software will expose this function to allow TTP's software to define the Service Name field of the PADO packet.</span></span> <span data-ttu-id="3bb3d-335">PppDiscoverCnf çağrıldığında, PPPoE yazılımı PADO 'yi göndermemelidir.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-335">The PPPoE software should not send the PADO until the PppDiscoverCnf is called.</span></span>

<span data-ttu-id="3bb3d-336">PADO paketi, PPPoE yazılımının başlatılabilir bölümünde tanımlanan bir erişim yoğunlaştırıcısı adı (RFC2516 ' de tanımlanan # 2 etiket kimliği kullanılarak) içerir.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-336">The PADO packet shall contain an access concentrator name (using the tag id 0x0102 as defined in RFC2516), defined on initialisation of the PPPoE software.</span></span>

<span data-ttu-id="3bb3d-337">Her ad null olarak sonlandırıldığından, aData içinde birden çok hizmet adı geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-337">Multiple service names can be passed in aData, with each name to be null terminated.</span></span>

<span data-ttu-id="3bb3d-338">Diğer komutların hizmet adının bir parçası olarak geçirilmesi gereken durumlarda, en yüksek esnekliği sağlamak için null karakter kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-338">Null character is used as a separator to provide maximum flexibility in case other commands need to be passed in as part of the service name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-339">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-339">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-340">**uzunluk**: varsayılan hizmet adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-340">**length**: Length of default service name.</span></span>
- <span data-ttu-id="3bb3d-341">**ADATA**: varsayılan hizmet adı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-341">**aData**: Default service name.</span></span>
- <span data-ttu-id="3bb3d-342">**ınterfacehandle**: arabirim tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-342">**interfaceHandle**: Interface handle.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-343">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-343">Return Values</span></span>

<span data-ttu-id="3bb3d-344">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="3bb3d-344">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-345">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-345">Allowed From</span></span>

<span data-ttu-id="3bb3d-346">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-346">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-347">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-347">Example</span></span>

```c
/* Define the Service Name field of the PADO packet. */
PppDiscoverCnf (3, "XBB", 0);
```

## <a name="pppopencnf"></a><span data-ttu-id="3bb3d-348">PppOpenCnf</span><span class="sxs-lookup"><span data-stu-id="3bb3d-348">PppOpenCnf</span></span>

<span data-ttu-id="3bb3d-349">PPPoE oturumunu kabul etme veya reddetme</span><span class="sxs-lookup"><span data-stu-id="3bb3d-349">Accept or reject the PPPoE session</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-350">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-350">Prototype</span></span>

```c
VOID PppOpenCnf (UCHAR accept, UINT interfaceHandle);
```

### <a name="description"></a><span data-ttu-id="3bb3d-351">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-351">Description</span></span>

<span data-ttu-id="3bb3d-352">PPPoE yazılımı, TTP 'nin yazılım PPPoE oturumunu kabul etmesine veya reddetmesine izin vermek için bu işlevi kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-352">The PPPoE software will expose this function to allow TTP's software to accept or reject the PPPoE session.</span></span>  <span data-ttu-id="3bb3d-353">Buna yanıt olarak, PPPoE yığını bağlantıyı kabul etmeli ve ınterfacehandle ile ilişkili benzersiz bir PPPoE Session_ID numarası atamalıdır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-353">In response to this the PPPoE stack should accept the connection and assign a unique PPPoE Session_ID number associated with the interfaceHandle.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-354">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-354">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-355">**kabul et**: bağlantının kabul edileceği NX_TRUE.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-355">**accept**: NX_TRUE if the connection is to be accepted.</span></span>
- <span data-ttu-id="3bb3d-356">**ınterfacehandle**: arabirim tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-356">**interfaceHandle**: Interface handle.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-357">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-357">Return Values</span></span>

<span data-ttu-id="3bb3d-358">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="3bb3d-358">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-359">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-359">Allowed From</span></span>

<span data-ttu-id="3bb3d-360">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-360">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-361">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-361">Example</span></span>

```c
/* Accept the connection. */
PppOpenCnf(NX_TRUE, 0);
```

## <a name="pppcloseind"></a><span data-ttu-id="3bb3d-362">PppCloseInd</span><span class="sxs-lookup"><span data-stu-id="3bb3d-362">PppCloseInd</span></span>

<span data-ttu-id="3bb3d-363">Bir PPPoE oturumunu kapatma</span><span class="sxs-lookup"><span data-stu-id="3bb3d-363">Close a PPPoE session</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-364">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-364">Prototype</span></span>

```c
VOID PppCloseInd (UINT interfaceHandle, UCHAR *causeCode);
```

### <a name="description"></a><span data-ttu-id="3bb3d-365">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-365">Description</span></span>

<span data-ttu-id="3bb3d-366">Bu işlev, TTP 'nin yazılımının bir PPPoE oturumunu kapatmasını sağlamak için bu işlevi açığa çıkarır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-366">The PPPoE software will expose this function to allow TTP's software to close a PPPoE session.</span></span>

<span data-ttu-id="3bb3d-367">PPPoE yazılımı, TıT iletisindeki Generic-Error etiketinde neden kod dizesinin (0x0203) olduğunu gösterir</span><span class="sxs-lookup"><span data-stu-id="3bb3d-367">The PPPoE software will indicate the cause code string in the Generic-Error tag (0x0203) in the PADT message</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-368">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-368">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-369">**ınterfacehandle**: arabirim tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-369">**interfaceHandle**: Interface handle.</span></span>
- <span data-ttu-id="3bb3d-370">**Causecode**: PPPoE sunucusundan bağlantı kapatma nedeni hakkında bilgi göndermek için null sonlandırılmış dize.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-370">**causeCode**: Null terminated string for sending information about the reason for closing the connection from the PPPoE Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-371">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-371">Return Values</span></span>

<span data-ttu-id="3bb3d-372">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="3bb3d-372">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-373">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-373">Allowed From</span></span>

<span data-ttu-id="3bb3d-374">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-374">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-375">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-375">Example</span></span>

```c
/* Close a PPPoE session. */
PppCloseInd(0, NX_NULL);
```

## <a name="pppclosecnf"></a><span data-ttu-id="3bb3d-376">PppCloseCnf</span><span class="sxs-lookup"><span data-stu-id="3bb3d-376">PppCloseCnf</span></span>

<span data-ttu-id="3bb3d-377">Tanıtıcının serbest bırakılmış olduğunu onaylayın</span><span class="sxs-lookup"><span data-stu-id="3bb3d-377">Confirm that the handle has been freed</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-378">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-378">Prototype</span></span>

```c
VOID PppCloseCnf (UINT interfaceHandle);
```

### <a name="description"></a><span data-ttu-id="3bb3d-379">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-379">Description</span></span>

<span data-ttu-id="3bb3d-380">PPPoE yazılımı, bu işlevi, TTP 'nin yazılımın, tanıtıcının serbest bırakılmış olduğunu onaylamasını sağlamak için kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-380">The PPPoE software will expose this function to allow TTP's software to confirm that the handle has been freed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-381">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-381">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-382">**ınterfacehandle**: arabirim tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-382">**interfaceHandle**: Interface handle.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-383">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-383">Return Values</span></span>

<span data-ttu-id="3bb3d-384">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="3bb3d-384">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-385">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-385">Allowed From</span></span>

<span data-ttu-id="3bb3d-386">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-386">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-387">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-387">Example</span></span>

```c
/* Confirm that the handle has been freed. */
PppCloseCnf(0);
```

## <a name="ppptransmitdatacnf"></a><span data-ttu-id="3bb3d-388">PppTransmitDataCnf</span><span class="sxs-lookup"><span data-stu-id="3bb3d-388">PppTransmitDataCnf</span></span>

<span data-ttu-id="3bb3d-389">Önceki PPP verilerinin onaylaneklenmesine izin ver</span><span class="sxs-lookup"><span data-stu-id="3bb3d-389">Allow a preceding PPP data to be acknowledged</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-390">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-390">Prototype</span></span>

```c
VOID PppTransmitDataCnf (UINT interfaceHandle, UCHAR *aData,
                        UINT packet_id);
```

### <a name="description"></a><span data-ttu-id="3bb3d-391">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-391">Description</span></span>

<span data-ttu-id="3bb3d-392">PPPoE yazılımı, önceki bir PppTransmitDataReq 'ın onaylanmasına izin vermek için bu işlevi kullanıma sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-392">The PPPoE software will expose this function to allow a preceding PppTransmitDataReq to be acknowledged.</span></span>  <span data-ttu-id="3bb3d-393">Bu, TTP 'nin, PPPoE 'den yeni bir PPP çerçevesi için hazırlandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-393">It implies that TTP's software is ready for a new PPP frame from PPPoE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-394">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-394">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-395">**ınterfacehandle**: arabirim tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-395">**interfaceHandle**: Interface handle.</span></span>
- <span data-ttu-id="3bb3d-396">**ADATA**: işaretçi kabul edilen PPP veri arabelleğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-396">**aData**: Pointer the PPP data buffer that has been accepted.</span></span>
- <span data-ttu-id="3bb3d-397">**Packet_id**: paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-397">**Packet_id**: Packet identifier.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-398">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-398">Return Values</span></span>

<span data-ttu-id="3bb3d-399">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="3bb3d-399">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-400">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-400">Allowed From</span></span>

<span data-ttu-id="3bb3d-401">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-401">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-402">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-402">Example</span></span>

```c
UINT packet_id = 0x20015429

/* Allow a preceding PPP data to be acknowledged, let PPPoE Server release the packet with same packet identifier. */
PppTransmitDataCnf(0, NX_NULL, packet_id);
```

## <a name="pppreceivedataind"></a><span data-ttu-id="3bb3d-403">PppReceiveDataInd</span><span class="sxs-lookup"><span data-stu-id="3bb3d-403">PppReceiveDataInd</span></span>

<span data-ttu-id="3bb3d-404">Ethernet üzerinden aktarımdan veri al</span><span class="sxs-lookup"><span data-stu-id="3bb3d-404">Receive data from transmission over Ethernet</span></span>

### <a name="prototype"></a><span data-ttu-id="3bb3d-405">Prototype</span><span class="sxs-lookup"><span data-stu-id="3bb3d-405">Prototype</span></span>

```c
VOID PppReceiveDataInd(UINT interfaceHandle, UINT length, UCHAR *aData);
```

### <a name="description"></a><span data-ttu-id="3bb3d-406">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3bb3d-406">Description</span></span>

<span data-ttu-id="3bb3d-407">PPPoE yazılımı, Ethernet üzerinden iletilmek üzere veri almak için bu işlevi kullanıma sunacaktır</span><span class="sxs-lookup"><span data-stu-id="3bb3d-407">The PPPoE software will expose this function to receive data for transmission over Ethernet</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3bb3d-408">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-408">Input Parameters</span></span>

- <span data-ttu-id="3bb3d-409">**ınterfacehandle**: arabirim tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-409">**interfaceHandle**: Interface handle.</span></span>
- <span data-ttu-id="3bb3d-410">**uzunluk**: ADATA 'daki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-410">**length**: The number of bytes in aData.</span></span>
- <span data-ttu-id="3bb3d-411">**ADATA**: PPP verilerinin çerçevesini içeren veri arabelleği.</span><span class="sxs-lookup"><span data-stu-id="3bb3d-411">**aData**: Data buffer containing the frame of PPP data.</span></span>

### <a name="return-values"></a><span data-ttu-id="3bb3d-412">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3bb3d-412">Return Values</span></span>

<span data-ttu-id="3bb3d-413">**Hiçbiri**</span><span class="sxs-lookup"><span data-stu-id="3bb3d-413">**None**</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3bb3d-414">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3bb3d-414">Allowed From</span></span>

<span data-ttu-id="3bb3d-415">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3bb3d-415">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3bb3d-416">Örnek</span><span class="sxs-lookup"><span data-stu-id="3bb3d-416">Example</span></span>

```c
/* Receive data from transmission over Ethernet, data start pointer is aData.
The number of bytes in aData is 1480. */
PppReceiveDataInd (0, 1480, aData);
```