---
title: Bölüm 3-Azure RTOS NetX PPPoE Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX PPPoE Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 246115fc97d7597246f7fd5b4fb88cb615baab33
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825589"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pppoe-client-services"></a><span data-ttu-id="3127f-103">Bölüm 3-Azure RTOS NetX PPPoE Istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="3127f-103">Chapter 3 - Description of Azure RTOS NetX PPPoE Client Services</span></span>

<span data-ttu-id="3127f-104">Bu bölüm, tüm Azure RTOS NetX PPPoE Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="3127f-104">This chapter contains a description of all Azure RTOS NetX PPPoE Client services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="3127f-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="3127f-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="3127f-106">**nx_pppoe_client_create** *bir PPPoE istemci örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="3127f-106">**nx_pppoe_client_create** *Create a PPPoE Client instance*</span></span>
- <span data-ttu-id="3127f-107">**Nx_pppoe_client_delete** *PPPoE istemci örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="3127f-107">**nx_pppoe_client_delete** *Delete a PPPoE Client instance*</span></span>
- <span data-ttu-id="3127f-108">**Nx_pppoe_client_host_uniq_set** *PPPoE istemcisi için benzersiz konak kümesi*</span><span class="sxs-lookup"><span data-stu-id="3127f-108">**nx_pppoe_client_host_uniq_set** *Set the host unique for PPPoE Client*</span></span>
- <span data-ttu-id="3127f-109">**Nx_pppoe_client_host_uniq_set_extended** *PPPoE istemcisi için benzersiz konak kümesi*</span><span class="sxs-lookup"><span data-stu-id="3127f-109">**nx_pppoe_client_host_uniq_set_extended** *Set the host unique for PPPoE Client*</span></span>
- <span data-ttu-id="3127f-110">**Nx_pppoe_client_service_name_set** *PPPoE istemcisinin hizmet adını ayarlama*</span><span class="sxs-lookup"><span data-stu-id="3127f-110">**nx_pppoe_client_service_name_set** *Set the service name for PPPoE Client*</span></span>
- <span data-ttu-id="3127f-111">**Nx_pppoe_client_service_name_set_extended** *PPPoE istemcisinin hizmet adını ayarlama*</span><span class="sxs-lookup"><span data-stu-id="3127f-111">**nx_pppoe_client_service_name_set_extended** *Set the service name for PPPoE Client*</span></span>
- <span data-ttu-id="3127f-112">**Nx_pppoe_client_session_connect** *PPPoE Istemci oturumunu PPPoE sunucusuna bağlama*</span><span class="sxs-lookup"><span data-stu-id="3127f-112">**nx_pppoe_client_session_connect** *Connect PPPoE Client session to PPPoE Server*</span></span>
- <span data-ttu-id="3127f-113">**Nx_pppoe_client_session_packet_send** *PPPoE oturum paketi gönder*</span><span class="sxs-lookup"><span data-stu-id="3127f-113">**nx_pppoe_client_session_packet_send** *Send PPPoE session packet*</span></span>
- <span data-ttu-id="3127f-114">**Nx_pppoe_client_session_terminate** *PPPoE oturumunu Sonlandır*</span><span class="sxs-lookup"><span data-stu-id="3127f-114">**nx_pppoe_client_session_terminate** *Terminate the PPPoE session*</span></span>
- <span data-ttu-id="3127f-115">**nx_pppoe_client_session_get** *belirtilen PPPoE oturum inf dosyasını Al*</span><span class="sxs-lookup"><span data-stu-id="3127f-115">**nx_pppoe_client_session_get** *Get the specified PPPoE session inf*</span></span>

## <a name="nx_pppoe_client_create"></a><span data-ttu-id="3127f-116">nx_pppoe_client_create</span><span class="sxs-lookup"><span data-stu-id="3127f-116">nx_pppoe_client_create</span></span>

<span data-ttu-id="3127f-117">Bir PPPoE Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="3127f-117">Create a PPPoE Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-118">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-118">Prototype</span></span>

```c
UINT  nx_pppoe_client_create(NX_PPPOE_CLIENT *pppoe_client_ptr,
                            CHAR *name, NX_IP *ip_ptr,
                            UINT interface_index,
                            NX_PACKET_POOL *pool_ptr,
                            VOID *stack_ptr, ULONG stack_size,
                            UINT priority,
                            VOID (*pppoe_link_driver)
                            (struct NX_IP_DRIVER_STRUCT *)
                            VOID (*pppoe_packet_receive)
                            (NX_PACKET *packet_ptr));
```

### <a name="description"></a><span data-ttu-id="3127f-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-119">Description</span></span>

<span data-ttu-id="3127f-120">Bu hizmet, belirtilen NetX IP örneği için Kullanıcı tarafından sağlanan bağlantı sürücüsüyle bir PPPoE Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3127f-120">This service creates a PPPoE Client instance with the user supplied link driver for the specified NetX IP instance.</span></span> <span data-ttu-id="3127f-121">Bağlantı sürücüsü başlatılmamış ve etkin değilse, PPPoE Istemci yazılımı bağlantı sürücüsünü başlatmaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="3127f-121">If link driver has not been initialized, and enabled, PPPoE Client software is responsible initializing the link driver.</span></span>

<span data-ttu-id="3127f-122">Ayrıca, uygulamanın, iç paket ayırma için kullanması için, PPPoE Istemci örneği için önceden oluşturulmuş bir paket havuzu sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3127f-122">In addition, the application must supply a previously created packet pool for the PPPoE Client instance to use for internal packet allocation.</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-123">Genellikle NetX IP iş parçacığını, PPPoE Istemci iş parçacığı önceliğinden daha yüksek bir önceliğe göre oluşturmanız iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="3127f-123">Generally a good idea to create the NetX IP thread at a higher priority than the PPPoE Client thread priority.</span></span> <span data-ttu-id="3127f-124">IP iş parçacığı önceliğini belirtme hakkında daha fazla bilgi için lütfen *nx_ip_create* hizmetine bakın.</span><span class="sxs-lookup"><span data-stu-id="3127f-124">Please refer to the *nx_ip_create* service for more information on specifying the IP thread priority.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-125">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-125">Input Parameters</span></span>

 - <span data-ttu-id="3127f-126">**pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-126">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="3127f-127">**ad** Bu PPPoE Istemci örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="3127f-127">**name** Name of this PPPoE Client instance.</span></span>
 - <span data-ttu-id="3127f-128">**ip_ptr** IP örneği için denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="3127f-128">**ip_ptr** Pointer to control block for IP instance.</span></span>
 - <span data-ttu-id="3127f-129">**interface_index** Arabirim dizini.</span><span class="sxs-lookup"><span data-stu-id="3127f-129">**interface_index** Interface index.</span></span>
 - <span data-ttu-id="3127f-130">**pool_ptr** Paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-130">**pool_ptr** Pointer to packet pool.</span></span>
 - <span data-ttu-id="3127f-131">**stack_ptr** PPPoE Istemci iş parçacığının yığın alanının başlangıcı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-131">**stack_ptr** Pointer to start of PPPoE Client thread’s stack area.</span></span>
 - <span data-ttu-id="3127f-132">**stack_size** İş parçacığının yığınında bayt cinsinden boyut.</span><span class="sxs-lookup"><span data-stu-id="3127f-132">**stack_size** Size in bytes in the thread’s stack.</span></span>
 - <span data-ttu-id="3127f-133">**Öncelik** İç PPPoE Istemci iş parçacıklarının önceliği (1-31).</span><span class="sxs-lookup"><span data-stu-id="3127f-133">**priority** Priority of internal PPPoE Client threads (1-31).</span></span>
 - <span data-ttu-id="3127f-134">**pppoe_link_driver** Kullanıcı tarafından sağlanan bağlantı sürücüsü.</span><span class="sxs-lookup"><span data-stu-id="3127f-134">**pppoe_link_driver** User supplied link driver.</span></span>
 - <span data-ttu-id="3127f-135">**pppoe_packet_receive** Kullanıcı tarafından sağlanan paket alma işlevi.</span><span class="sxs-lookup"><span data-stu-id="3127f-135">**pppoe_packet_receive** User supplied packet receive function.</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-136">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-136">Return Values</span></span>

 - <span data-ttu-id="3127f-137">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemcisi oluştur.</span><span class="sxs-lookup"><span data-stu-id="3127f-137">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client create.</span></span>
 - <span data-ttu-id="3127f-138">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemcisi, IP, paket havuzu veya yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-138">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client, IP, packet pool, or stack pointer.</span></span>
 - <span data-ttu-id="3127f-139">NX_PPPOE_CLIENT_INVALID_INTERFACE (0xD2) geçersiz arabirim.</span><span class="sxs-lookup"><span data-stu-id="3127f-139">NX_PPPOE_CLIENT_INVALID_INTERFACE (0xD2) Invalid interface.</span></span>
 - <span data-ttu-id="3127f-140">NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) paket havuzunun yük boyutu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="3127f-140">NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) Invalid payload size of packet pool.</span></span>
 - <span data-ttu-id="3127f-141">NX_PPPOE_CLIENT_MEMORY_SIZE_ERROR (0xD4) geçersiz bellek boyutu.</span><span class="sxs-lookup"><span data-stu-id="3127f-141">NX_PPPOE_CLIENT_MEMORY_SIZE_ERROR (0xD4) Invalid memory size.</span></span>
 - <span data-ttu-id="3127f-142">NX_PPPOE_CLIENT_PRIORITY_ERROR (0xD5) PPPoE Istemci iş parçacığının geçersiz önceliği.</span><span class="sxs-lookup"><span data-stu-id="3127f-142">NX_PPPOE_CLIENT_PRIORITY_ERROR (0xD5) Invalid priority of PPPoE Client thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-143">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-143">Allowed From</span></span>

<span data-ttu-id="3127f-144">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-144">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-145">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-145">Example</span></span>

```c
/* Create “my_pppoe_client” for IP instance “my_ip”. */
status =  nx_pppoe_client_create(&my_pppoe_client, “my PPPoE Client”, &my_ip,
0, &my_pool, stack_start, 1024, 2,
link_driver, packet_receive);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” was successfully created. */
```

## <a name="nx_pppoe_client_delete"></a><span data-ttu-id="3127f-146">nx_pppoe_client_delete</span><span class="sxs-lookup"><span data-stu-id="3127f-146">nx_pppoe_client_delete</span></span>

<span data-ttu-id="3127f-147">Bir PPPoE Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="3127f-147">Delete a PPPoE Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-148">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-148">Prototype</span></span>

```c
UINT nx_pppoe_client_delete(NX_PPPOE_CLIENT *pppoe_client_ptr);
```

### <a name="description"></a><span data-ttu-id="3127f-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-149">Description</span></span>

<span data-ttu-id="3127f-150">Bu hizmet, önceden oluşturulmuş olan PPPoE Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="3127f-150">This service deletes the previously created PPPoE Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-151">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-151">Input Parameters</span></span>

 - <span data-ttu-id="3127f-152">**pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="3127f-152">**pppoe_client_ptr** Pointer to PPPoE Client control block</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-153">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-153">Return Values</span></span>

 - <span data-ttu-id="3127f-154">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemcisi silme.</span><span class="sxs-lookup"><span data-stu-id="3127f-154">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client delete.</span></span>
 - <span data-ttu-id="3127f-155">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-155">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-156">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-156">Allowed From</span></span>

<span data-ttu-id="3127f-157">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-157">Threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-158">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-158">Example</span></span>

```c
/* Delete PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_delete(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” was successfully deleted. */
```

## <a name="nx_pppoe_client_host_uniq_set"></a><span data-ttu-id="3127f-159">nx_pppoe_client_host_uniq_set</span><span class="sxs-lookup"><span data-stu-id="3127f-159">nx_pppoe_client_host_uniq_set</span></span>

<span data-ttu-id="3127f-160">PPPoE Istemci konağını benzersiz ayarla</span><span class="sxs-lookup"><span data-stu-id="3127f-160">Set PPPoE Client host unique</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-161">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-161">Prototype</span></span>

```c
UINT nx_pppoe_client_host_uniq_set(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq);
```

### <a name="description"></a><span data-ttu-id="3127f-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-162">Description</span></span>

<span data-ttu-id="3127f-163">Bu hizmet, PPPoE Istemci konağını benzersiz olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3127f-163">This service sets PPPoE Client host unique.</span></span> <span data-ttu-id="3127f-164">Host-Uniq, bir ana bilgisayar tarafından bir erişim yoğunlaştırıcıyı belirli bir ana bilgisayar isteğiyle benzersiz bir şekilde ilişkilendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3127f-164">Host-Uniq is used by a host to uniquely associate an Access Concentrator to a particular Host request.</span></span>
<span data-ttu-id="3127f-165">Bu, konağın seçtiği herhangi bir değerin ve uzunluğun ikili verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3127f-165">It can be binary data of any value and length that the Host chooses.</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-166">benzersiz konak, null ile sonlandırılmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3127f-166">host unique must be Null-terminated string.</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-167">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="3127f-167">This service is deprecated.</span></span> <span data-ttu-id="3127f-168">Geliştiricilerin *nx_pppoe_client_host_uniq_set_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="3127f-168">Developers are encouraged to migrate to *nx_pppoe_client_host_uniq_set_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-169">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-169">Input Parameters</span></span>

 - <span data-ttu-id="3127f-170">**pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-170">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="3127f-171">**host_uniq** Benzersiz bir ana bilgisayar işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-171">**host_uniq** Pointer to an host unique.</span></span> <span data-ttu-id="3127f-172">Benzersiz konak, null ile sonlandırılmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3127f-172">Host unique must be Null-terminated string.</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-173">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-173">Return Values</span></span>

 - <span data-ttu-id="3127f-174">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci ana bilgisayar benzersiz kümesi.</span><span class="sxs-lookup"><span data-stu-id="3127f-174">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client host unique set.</span></span>
 - <span data-ttu-id="3127f-175">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-175">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-176">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-176">Allowed From</span></span>

<span data-ttu-id="3127f-177">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-177">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-178">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-178">Example</span></span>

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_host_uniq_set(&my_pppoe_client,
“220000000000000041000000”);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” host unique has set. */
```

## <a name="nx_pppoe_client_host_uniq_set_extended"></a><span data-ttu-id="3127f-179">nx_pppoe_client_host_uniq_set_extended</span><span class="sxs-lookup"><span data-stu-id="3127f-179">nx_pppoe_client_host_uniq_set_extended</span></span>

<span data-ttu-id="3127f-180">PPPoE Istemci konağını benzersiz ayarla</span><span class="sxs-lookup"><span data-stu-id="3127f-180">Set PPPoE Client host unique</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-181">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-181">Prototype</span></span>

```c
UINT nx_pppoe_client_host_uniq_set_extended(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *host_uniq,UINT host_uniq_length);
```

### <a name="description"></a><span data-ttu-id="3127f-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-182">Description</span></span>

<span data-ttu-id="3127f-183">Bu hizmet, PPPoE Istemci konağını benzersiz olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3127f-183">This service sets PPPoE Client host unique.</span></span> <span data-ttu-id="3127f-184">Host-Uniq, bir ana bilgisayar tarafından bir erişim yoğunlaştırıcıyı belirli bir ana bilgisayar isteğiyle benzersiz bir şekilde ilişkilendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3127f-184">Host-Uniq is used by a host to uniquely associate an Access Concentrator to a particular Host request.</span></span>
<span data-ttu-id="3127f-185">Bu, konağın seçtiği herhangi bir değerin ve uzunluğun ikili verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3127f-185">It can be binary data of any value and length that the Host chooses.</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-186">benzersiz konak, null ile sonlandırılmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3127f-186">host unique must be Null-terminated string.</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-187">Bu hizmet *nx_pppoe_client_host_uniq_set ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="3127f-187">This service replaces *nx_pppoe_client_host_uniq_set()*.</span></span> <span data-ttu-id="3127f-188">Bu sürüm, hizmete ek uzunluk bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="3127f-188">This version supplies additional length information to the service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-189">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-189">Input Parameters</span></span>

 - <span data-ttu-id="3127f-190">**pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-190">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="3127f-191">**host_uniq** Benzersiz bir ana bilgisayar işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-191">**host_uniq** Pointer to an host unique.</span></span> <span data-ttu-id="3127f-192">Benzersiz konak, null ile sonlandırılmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3127f-192">Host unique must be Null-terminated string.</span></span>
 - <span data-ttu-id="3127f-193">**host_uniq_length** Host_uniq uzunluğu</span><span class="sxs-lookup"><span data-stu-id="3127f-193">**host_uniq_length** Length of host_uniq</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-194">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-194">Return Values</span></span>

 - <span data-ttu-id="3127f-195">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci ana bilgisayar benzersiz kümesi.</span><span class="sxs-lookup"><span data-stu-id="3127f-195">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client host unique set.</span></span>
 - <span data-ttu-id="3127f-196">**NX_PPPOE_CLIENT_PTR_ERROR** (0Xd1) geçersiz PPPoE istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-196">**NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Invalid PPPoE Client pointer.</span></span>
 - <span data-ttu-id="3127f-197">**NX_SIZE_ERROR** (0x09) denetim host_uniq_length başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="3127f-197">**NX_SIZE_ERROR** (0x09) Check host_uniq_length fail</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-198">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-198">Allowed From</span></span>

<span data-ttu-id="3127f-199">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-199">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-200">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-200">Example</span></span>

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_host_uniq_set_extended(&my_pppoe_client,
“220000000000000041000000”,24);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” host unique has set. */
```

## <a name="nx_pppoe_client_service_name_set"></a><span data-ttu-id="3127f-201">nx_pppoe_client_service_name_set</span><span class="sxs-lookup"><span data-stu-id="3127f-201">nx_pppoe_client_service_name_set</span></span>

<span data-ttu-id="3127f-202">PPPoE Istemci hizmeti adını ayarla</span><span class="sxs-lookup"><span data-stu-id="3127f-202">Set PPPoE Client service name</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-203">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-203">Prototype</span></span>

```c
UINT nx_pppoe_client_service_name_set(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *service_name);
```

### <a name="description"></a><span data-ttu-id="3127f-204">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-204">Description</span></span>

<span data-ttu-id="3127f-205">Bu hizmet, PPPoE Istemci hizmeti adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3127f-205">This service sets PPPoE Client service name.</span></span> <span data-ttu-id="3127f-206">Konağın istediği hizmeti belirten Service-Name.</span><span class="sxs-lookup"><span data-stu-id="3127f-206">The Service-Name indicating the service the Host is requesting.</span></span> <span data-ttu-id="3127f-207">Service-Name ayarlanmamışsa konağın herhangi bir sayıda hizmeti kabul edeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3127f-207">If Service-Name is not set, indicating Host will accept any number of services.</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-208">hizmet adı null ile sonlandırılmış bir dize olmalıdır</span><span class="sxs-lookup"><span data-stu-id="3127f-208">service name must be Null-terminated string</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-209">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="3127f-209">This service is deprecated.</span></span> <span data-ttu-id="3127f-210">Geliştiricilerin *nx_pppoe_client_service_name_set_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="3127f-210">Developers are encouraged to migrate to *nx_pppoe_client_service_name_set_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-211">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-211">Input Parameters</span></span>

 - <span data-ttu-id="3127f-212">**pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-212">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="3127f-213">**service_name** Hizmet adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-213">**service_name** Pointer to an service name.</span></span> <span data-ttu-id="3127f-214">Hizmet adı null ile sonlandırılmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3127f-214">Service name must be Null-terminated string.</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-215">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-215">Return Values</span></span>

 - <span data-ttu-id="3127f-216">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci hizmeti adı kümesi.</span><span class="sxs-lookup"><span data-stu-id="3127f-216">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client service name set.</span></span>
 - <span data-ttu-id="3127f-217">**NX_PPPOE_CLIENT_PTR_ERROR** (0Xd1) geçersiz PPPoE istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-217">**NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-218">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-218">Allowed From</span></span>

<span data-ttu-id="3127f-219">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-219">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-220">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-220">Example</span></span>

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_service_name_set(&my_pppoe_client,
“BRAS”);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” service name has set. */
```

## <a name="nx_pppoe_client_service_name_set_extended"></a><span data-ttu-id="3127f-221">nx_pppoe_client_service_name_set_extended</span><span class="sxs-lookup"><span data-stu-id="3127f-221">nx_pppoe_client_service_name_set_extended</span></span>

<span data-ttu-id="3127f-222">PPPoE Istemci hizmeti adını ayarla</span><span class="sxs-lookup"><span data-stu-id="3127f-222">Set PPPoE Client service name</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-223">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-223">Prototype</span></span>

```c
UINT nx_pppoe_client_service_name_set_extended(
                        NX_PPPOE_CLIENT *pppoe_client_ptr,
                        UCHAR *service_name,UINT service_name_length);
```

### <a name="description"></a><span data-ttu-id="3127f-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-224">Description</span></span>

<span data-ttu-id="3127f-225">Bu hizmet, PPPoE Istemci hizmeti adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3127f-225">This service sets PPPoE Client service name.</span></span> <span data-ttu-id="3127f-226">Konağın istediği hizmeti belirten Service-Name.</span><span class="sxs-lookup"><span data-stu-id="3127f-226">The Service-Name indicating the service the Host is requesting.</span></span> <span data-ttu-id="3127f-227">Service-Name ayarlanmamışsa konağın herhangi bir sayıda hizmeti kabul edeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3127f-227">If Service-Name is not set, indicating Host will accept any number of services.</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-228">hizmet adı null ile sonlandırılmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3127f-228">service name must be Null-terminated string.</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-229">Bu hizmet *nx_pppoe_client_service_name_set ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="3127f-229">This service replaces *nx_pppoe_client_service_name_set()*.</span></span> <span data-ttu-id="3127f-230">Bu sürüm, işleve ek hizmet adı uzunluk bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="3127f-230">This version supplies additional service name length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-231">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-231">Input Parameters</span></span>

 - <span data-ttu-id="3127f-232">**pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-232">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="3127f-233">**service_name** Hizmet adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-233">**service_name** Pointer to an service name.</span></span> <span data-ttu-id="3127f-234">Hizmet adı null ile sonlandırılmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3127f-234">Service name must be Null-terminated string.</span></span>
 - <span data-ttu-id="3127f-235">**service_name_length** Service_name uzunluğu</span><span class="sxs-lookup"><span data-stu-id="3127f-235">**service_name_length** Length of service_name</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-236">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-236">Return Values</span></span>

 - <span data-ttu-id="3127f-237">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci hizmeti adı kümesi.</span><span class="sxs-lookup"><span data-stu-id="3127f-237">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client service name set.</span></span>
 - <span data-ttu-id="3127f-238">**NX_PPPOE_CLIENT_PTR_ERROR** (0Xd1) geçersiz PPPoE istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-238">**NX_PPPOE_CLIENT_PTR_ERROR** (0xD1) Invalid PPPoE Client pointer.</span></span>
 - <span data-ttu-id="3127f-239">**NX_SIZE_ERROR** (0x09) denetim service_name_length başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="3127f-239">**NX_SIZE_ERROR** (0x09) Check service_name_length fail</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-240">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-240">Allowed From</span></span>

<span data-ttu-id="3127f-241">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-241">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-242">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-242">Example</span></span>

```c
/* Set service name for PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_service_name_set_extended(&my_pppoe_client,
“BRAS”,4);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” service name has set. */
```

## <a name="nx_pppoe_client_session_connect"></a><span data-ttu-id="3127f-243">nx_pppoe_client_session_connect</span><span class="sxs-lookup"><span data-stu-id="3127f-243">nx_pppoe_client_session_connect</span></span>

<span data-ttu-id="3127f-244">PPPoE Istemci oturumunu bağlama</span><span class="sxs-lookup"><span data-stu-id="3127f-244">Connect PPPoE Client session</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-245">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-245">Prototype</span></span>

```c
UINT nx_pppoe_client_session_connect(NX_PPPOE_CLIENT *pppoe_client_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="3127f-246">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-246">Description</span></span>

<span data-ttu-id="3127f-247">Bu hizmet, daha önce oluşturulmuş bir PPPoE Istemcisini belirtilen PPPoE sunucusuna kullanarak PPPoE oturum bağlantısı yapar.</span><span class="sxs-lookup"><span data-stu-id="3127f-247">This service makes PPPoE session connection using a previously created PPPoE Client to the specified PPPoE Server.</span></span>

> [!NOTE]
> <span data-ttu-id="3127f-248">Bu işlev, *nx_pppoe_client_create*, *nx_pppoe_client_host_uniq_set* ve *nx_pppoe_client_service_name_set* sonra çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3127f-248">This function must be called after *nx_pppoe_client_create*, *nx_pppoe_client_host_uniq_set* and *nx_pppoe_client_service_name_set*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-249">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-249">Input Parameters</span></span>

 - <span data-ttu-id="3127f-250">**pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-250">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="3127f-251">**wait_option** Bağlantı kurulurken bekle seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3127f-251">**wait_option** Wait option while the connection is being established.</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-252">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-252">Return Values</span></span>

 - <span data-ttu-id="3127f-253">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci oturumu bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="3127f-253">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client session connect.</span></span>
 - <span data-ttu-id="3127f-254">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-254">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-255">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-255">Allowed From</span></span>

<span data-ttu-id="3127f-256">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-256">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-257">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-257">Example</span></span>

```c
/* Enable PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_connect(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” session connection has connected. */
```

## <a name="nx_pppoe_client_session_packet_send"></a><span data-ttu-id="3127f-258">nx_pppoe_client_session_packet_send</span><span class="sxs-lookup"><span data-stu-id="3127f-258">nx_pppoe_client_session_packet_send</span></span>

<span data-ttu-id="3127f-259">PPPoE Istemci paketini belirtilen oturuma gönder</span><span class="sxs-lookup"><span data-stu-id="3127f-259">Send PPPoE Client packet to specified session</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-260">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-260">Prototype</span></span>

```c
UINT nx_pppoe_client_session_packet_send(
                                    NX_PPPOE_CLIENT *pppoe_client_ptr,
                                    NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="3127f-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-261">Description</span></span>

<span data-ttu-id="3127f-262">Bu hizmet, belirtilen oturum KIMLIĞINI kullanarak PPPoE paketi gönderir.</span><span class="sxs-lookup"><span data-stu-id="3127f-262">This service sends PPPoE packet using specified session ID.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-263">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-263">Input Parameters</span></span>

 - <span data-ttu-id="3127f-264">**pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-264">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="3127f-265">**packet_ptr** PPPoE paketi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-265">**packet_ptr** Pointer to PPPoE packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-266">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-266">Return Values</span></span>

 - <span data-ttu-id="3127f-267">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci paketi gönderme.</span><span class="sxs-lookup"><span data-stu-id="3127f-267">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client packet send.</span></span>
 - <span data-ttu-id="3127f-268">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-268">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>
 - <span data-ttu-id="3127f-269">NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) geçersiz PPPoE Istemci paketi.</span><span class="sxs-lookup"><span data-stu-id="3127f-269">NX_PPPOE_CLIENT_PACKET_PAYLOAD_ERROR (0xD3) Invalid PPPoE Client packet.</span></span>
 - <span data-ttu-id="3127f-270">NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) PPPoE oturumu kurulmadı.</span><span class="sxs-lookup"><span data-stu-id="3127f-270">NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-271">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-271">Allowed From</span></span>

<span data-ttu-id="3127f-272">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-272">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-273">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-273">Example</span></span>

```c
/* Send PPPoE client packet to specified session, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_packet_send(&my_pppoe_client, packet_ptr);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the “my_pppoe_client” packet has sent. */
```

## <a name="nx_pppoe_client_session_terminate"></a><span data-ttu-id="3127f-274">nx_pppoe_client_session_terminate</span><span class="sxs-lookup"><span data-stu-id="3127f-274">nx_pppoe_client_session_terminate</span></span>

<span data-ttu-id="3127f-275">PPPoE Istemci oturumunu Sonlandır</span><span class="sxs-lookup"><span data-stu-id="3127f-275">Terminate PPPoE Client session</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-276">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-276">Prototype</span></span>

```c
UINT nx_pppoe_client_session_terminate(
                                    NX_PPPOE_CLIENT *pppoe_client_ptr);
```

### <a name="description"></a><span data-ttu-id="3127f-277">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-277">Description</span></span>

<span data-ttu-id="3127f-278">Bu hizmet, belirtilen PPPoE oturumunu sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="3127f-278">This service terminates the specified PPPoE session.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-279">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-279">Input Parameters</span></span>

 - <span data-ttu-id="3127f-280">**pppoe_client_ptr** PPPoE Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-280">**pppoe_client_ptr** Pointer to PPPoE Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-281">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-281">Return Values</span></span>

 - <span data-ttu-id="3127f-282">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci oturumu sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="3127f-282">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client session terminate.</span></span>
 - <span data-ttu-id="3127f-283">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-283">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-284">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-284">Allowed From</span></span>

<span data-ttu-id="3127f-285">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-285">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-286">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-286">Example</span></span>

```c
/* Terminates the specified PPPoE session, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_terminate(&my_pppoe_client);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the session has terminated. */
```

## <a name="nx_pppoe_client_session_get"></a><span data-ttu-id="3127f-287">nx_pppoe_client_session_get</span><span class="sxs-lookup"><span data-stu-id="3127f-287">nx_pppoe_client_session_get</span></span>

<span data-ttu-id="3127f-288">Belirtilen PPPoE oturum bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="3127f-288">Get the specified PPPoE session information</span></span>

### <a name="prototype"></a><span data-ttu-id="3127f-289">Prototype</span><span class="sxs-lookup"><span data-stu-id="3127f-289">Prototype</span></span>

```c
UINT nx_pppoe_client_session_get(NX_PPPOE_CLIENT *pppoe_client_ptr,
                                ULONG *server_mac_msw,
                                ULONG *server_mac_lsw,
                                ULONG *session_id);
```

### <a name="description"></a><span data-ttu-id="3127f-290">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3127f-290">Description</span></span>

<span data-ttu-id="3127f-291">Bu hizmet, belirtilen PPPoE oturum bilgilerini, sunucu fiziksel adresini ve oturum kimliğini alır.</span><span class="sxs-lookup"><span data-stu-id="3127f-291">This service gets the specified PPPoE session information, server physical address and session id.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3127f-292">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="3127f-292">Input Parameters</span></span>

 - <span data-ttu-id="3127f-293">**pppoe_server_ptr** PPPoE Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-293">**pppoe_server_ptr** Pointer to PPPoE Client control block.</span></span>
 - <span data-ttu-id="3127f-294">**server_mac_msw** Sunucu fiziksel adresi MSW işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-294">**server_mac_msw** Server Physical address MSW pointer.</span></span>
 - <span data-ttu-id="3127f-295">**server_mac_lsw** Sunucu fiziksel adresi MSW işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-295">**server_mac_lsw** Server Physical address MSW pointer.</span></span>
 - <span data-ttu-id="3127f-296">**session_id** Oturum KIMLIĞI işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-296">**session_id** Session ID pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="3127f-297">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="3127f-297">Return Values</span></span>

 - <span data-ttu-id="3127f-298">**NX_PPPOE_CLIENT_SUCCESS** (0x00) başarılı PPPoE istemci oturumu al.</span><span class="sxs-lookup"><span data-stu-id="3127f-298">**NX_PPPOE_CLIENT_SUCCESS** (0x00) Successful PPPoE Client session get.</span></span>
 - <span data-ttu-id="3127f-299">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) geçersiz PPPoE Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="3127f-299">NX_PPPOE_CLIENT_PTR_ERROR (0xD1) Invalid PPPoE Client pointer.</span></span>
 - <span data-ttu-id="3127f-300">NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) PPPoE oturumu kurulmadı.</span><span class="sxs-lookup"><span data-stu-id="3127f-300">NX_PPPOE_CLIENT_SESSION_NOT_ESTABLISHED (0xD8) PPPoE session is not established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="3127f-301">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="3127f-301">Allowed From</span></span>

<span data-ttu-id="3127f-302">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="3127f-302">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="3127f-303">Örnek</span><span class="sxs-lookup"><span data-stu-id="3127f-303">Example</span></span>

```c
/* Gets the specified PPPoE session information, PPPoE Client instance “my_pppoe_client”. */
status =  nx_pppoe_client_session_get (&my_pppoe_client, &server_mac_msw, &server_mac_lsw, &session_id);

/* If status is NX_PPPOE_CLIENT_SUCCESS, the server physical address and session id
   of the session has got. */
```
