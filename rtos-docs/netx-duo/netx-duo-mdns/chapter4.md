---
title: Bölüm 4-mDNS hizmetlerinin açıklaması
description: Bu bölümde tüm NetX mDNS hizmetlerinin açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 89df0ab5f09be8ad50a27d23bae8b20d71caa0b4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825918"
---
# <a name="chapter-4---description-of-mdns-services"></a><span data-ttu-id="36d7e-103">Bölüm 4-mDNS hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="36d7e-103">Chapter 4 - Description of mDNS services</span></span>

<span data-ttu-id="36d7e-104">Bu bölüm tüm NetX mDNS hizmetlerinin (aşağıda listelenmiştir) bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-104">This chapter contains a description of all NetX mDNS services (listed below).</span></span>

> [!NOTE]
> <span data-ttu-id="36d7e-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_mdns_create"></a><span data-ttu-id="36d7e-106">nx_mdns_create</span><span class="sxs-lookup"><span data-stu-id="36d7e-106">nx_mdns_create</span></span>

<span data-ttu-id="36d7e-107">MDNS örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="36d7e-107">Create an mDNS instance</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-108">Prototype</span></span>

```C
UINT nx_mdns_create(NX_MDNS *mdns_ptr, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool,
    UINT priority, VOID *stack_ptr,
    UINT stack_size, UCHAR *host_name,
    VOID *local_service_cache,
    UINT local_service_cache_size,
    VOID *peer_service_cache,
    UINT peer_service_cache_size,
    VOID (*probing_notify)(NX_MDNS *mdns_ptr,
        UCHAR *name, UINT probing_state));
```

### <a name="description"></a><span data-ttu-id="36d7e-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-109">Description</span></span>

<span data-ttu-id="36d7e-110">Bu hizmet, belirli IP örneğinde ve ilişkili kaynaklarda bir mDNS örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="36d7e-110">This service creates an mDNS instance on the specific IP instance and associated resources.</span></span> <span data-ttu-id="36d7e-111">Ayrıca, gelen mDNS iletilerini işlemek, sorgulara yanıt vermek ve sorgu iletilerini düzenli olarak iletmek için bir iş parçacığı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="36d7e-111">A thread is also created to handle incoming mDNS messages, to respond to queries, and to periodically transmit query messages.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-112">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-112">Input Parameters</span></span>

- <span data-ttu-id="36d7e-113">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-113">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-114">**ip_ptr** İlişkili IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-114">**ip_ptr** Pointer to the associated IP instance.</span></span>
- <span data-ttu-id="36d7e-115">**packet_pool** Geçerli bir paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-115">**packet_pool** Pointer to a valid packet pool.</span></span>
- <span data-ttu-id="36d7e-116">**Öncelik** MDNS iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="36d7e-116">**priority** Priority of the mDNS thread.</span></span>
- <span data-ttu-id="36d7e-117">**stack_ptr** MDNS iş parçacığı için yığın alanı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="36d7e-117">**stack_ptr** Pointer to the stack area for the mDNS thread</span></span>
- <span data-ttu-id="36d7e-118">**stack_size** Yığın alanının boyutu.</span><span class="sxs-lookup"><span data-stu-id="36d7e-118">**stack_size** Size of the stack area.</span></span>
- <span data-ttu-id="36d7e-119">**host_name** Bu düğüme atanan konak adı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-119">**host_name** Host name assigned to this node.</span></span>
- <span data-ttu-id="36d7e-120">**local_service_cache** Yerel kayıtlı hizmetler için depolama alanı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-120">**local_service_cache** Storage space for local registered services.</span></span>
- <span data-ttu-id="36d7e-121">**local_service_cache_size** Yerel hizmet önbelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="36d7e-121">**local_service_cache_size** Size of the local service cache.</span></span>
- <span data-ttu-id="36d7e-122">**peer_service_cache** Alınan hizmet bilgileri için depolama alanı</span><span class="sxs-lookup"><span data-stu-id="36d7e-122">**peer_service_cache** Storage space for service information received</span></span>
- <span data-ttu-id="36d7e-123">**peer_service_cache_size** Eş hizmeti önbelleğinin boyutu</span><span class="sxs-lookup"><span data-stu-id="36d7e-123">**peer_service_cache_size** Size of the peer service cache</span></span>
- <span data-ttu-id="36d7e-124">**probing_notify** Araştırma işleminin sonunda çağrılan isteğe bağlı geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-124">**probing_notify** Optional callback function invoked at the end of the probing operation.</span></span> <span data-ttu-id="36d7e-125">Ana bilgisayar adı (yerel bir arabirimde mDNS etkinleştirildiğinde) veya hizmet adı (hizmet kaydedildikten sonra) benzersiz olup olmadığını uygulamaya bildirir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-125">It notifies the application whether or not the host name (when enabling mDNS on a local interface), or the service name (after registering a service) is unique.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-126">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-126">Return Values</span></span>

- <span data-ttu-id="36d7e-127">**NX_SUCCESS** (0x00) mdıdns örneğini başarıyla oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="36d7e-127">**NX_SUCCESS** (0x00) Successfully created mDNS instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-128">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-128">Allowed From</span></span>

<span data-ttu-id="36d7e-129">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-129">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-130">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-130">Example</span></span>

```C
UCHAR stack_ptr[2048];
UCHAR local_cache_ptr[2048];
UCHAR peer_cache_ptr[8192];

/* Create a mDNS instance. */
status = nx_mdns_create(&my_mdns, &ip_0, &pool_0,
    3, stack_ptr, 2048,
    “NETX-MDNS-HOST”,
    local_cache_ptr, 2048,
    peer_cache_ptr, 8192,
    probing_notify);

/* If status is NX_SUCCESS, mDNS instance was created. */
```

## <a name="nx_mdns_delete"></a><span data-ttu-id="36d7e-131">nx_mdns_delete</span><span class="sxs-lookup"><span data-stu-id="36d7e-131">nx_mdns_delete</span></span>

<span data-ttu-id="36d7e-132">MDNS örneğini silme</span><span class="sxs-lookup"><span data-stu-id="36d7e-132">Delete an mDNS instance</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-133">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-133">Prototype</span></span>

```C
UINT nx_mdns_delete(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="36d7e-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-134">Description</span></span>

<span data-ttu-id="36d7e-135">Bu hizmet, mDNS örneğini siler ve kaynaklarını serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-135">This service deletes the mDNS instance and frees its resources.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-136">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-136">Input Parameters</span></span>

- <span data-ttu-id="36d7e-137">**mdns_ptr** MDNS denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-137">**mdns_ptr** Pointer to the mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-138">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-138">Return Values</span></span>

- <span data-ttu-id="36d7e-139">**NX_SUCCESS** (0x00), MDNs örneğini başarıyla sildi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-139">**NX_SUCCESS** (0x00) Successfully deleted the mDNS instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-140">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-140">Allowed From</span></span>

<span data-ttu-id="36d7e-141">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-141">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-142">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-142">Example</span></span>

```C
/* Delete a previously created mDNS instance. */

status = nx_mdns_delete(&my_mdns);

/* If status is NX_SUCCESS, the mDNS instance has been deleted. */
```

## <a name="nx_mdns_enable"></a><span data-ttu-id="36d7e-143">nx_mdns_enable</span><span class="sxs-lookup"><span data-stu-id="36d7e-143">nx_mdns_enable</span></span>

<span data-ttu-id="36d7e-144">MDNS hizmetini başlatma</span><span class="sxs-lookup"><span data-stu-id="36d7e-144">Start the mDNS service</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-145">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-145">Prototype</span></span>

```C
UINT nx_mdns_enable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="36d7e-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-146">Description</span></span>

<span data-ttu-id="36d7e-147">Bu API, belirli fiziksel arabirimde mDNS hizmetini mümkün bir şekilde sunar.</span><span class="sxs-lookup"><span data-stu-id="36d7e-147">This API enables mDNS service on specific physical interface.</span></span> <span data-ttu-id="36d7e-148">Hizmet etkinleştirildikten sonra, mDNS modülü, arabirimde alınan sorgulara yanıt vermeden önce ağ üzerindeki tüm benzersiz hizmet adlarını yoklamaları.</span><span class="sxs-lookup"><span data-stu-id="36d7e-148">Once the service is enabled, the mDNS module first probes all its unique service names on the network before responding to queries received on the interface.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-149">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-149">Input Parameters</span></span>

- <span data-ttu-id="36d7e-150">**mdns_ptr** MDNS örnek denetimi bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-150">**mdns_ptr** Pointer to the mDNS instance control block.</span></span>
- <span data-ttu-id="36d7e-151">**interface_index** Hizmetin etkinleştirildiği arabirimin dizini</span><span class="sxs-lookup"><span data-stu-id="36d7e-151">**interface_index** Index to the interface where the service is to be enabled</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-152">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-152">Return Values</span></span>

- <span data-ttu-id="36d7e-153">**NX_SUCCESS** (0x00) hizmeti başarıyla etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-153">**NX_SUCCESS** (0x00) Successfully enabled the service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-154">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-154">Allowed From</span></span>

<span data-ttu-id="36d7e-155">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-155">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-156">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-156">Example</span></span>

```C
/* Enable mDNS service on specific interface. */

status = nx_mdns_enable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was enabled. */
```

## <a name="nx_mdns_disable"></a><span data-ttu-id="36d7e-157">nx_mdns_disable</span><span class="sxs-lookup"><span data-stu-id="36d7e-157">nx_mdns_disable</span></span>

<span data-ttu-id="36d7e-158">MDNS hizmetini devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="36d7e-158">Disable the mDNS service</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-159">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-159">Prototype</span></span>

```C
UINT nx_mdns_disable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="36d7e-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-160">Description</span></span>

<span data-ttu-id="36d7e-161">Bu API, belirli fiziksel arabirimde mDNS hizmetini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-161">This API disables mDNS service on the specific physical interface.</span></span> <span data-ttu-id="36d7e-162">Hizmet devre dışı bırakıldıktan sonra, mDNS her yerel hizmet için arabirime bağlı olan ağa "güle" iletileri gönderir, böylece komşu düğümler bilgilendirilir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-162">Once the service is disabled, the mDNS sends "goodbye" messages for every local service to the network that is attached to the interface, so the neighboring nodes are notified.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-163">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-163">Input Parameters</span></span>

- <span data-ttu-id="36d7e-164">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-164">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-165">**interface_index** Hizmetin devre dışı bırakıldığı arabirimin dizini</span><span class="sxs-lookup"><span data-stu-id="36d7e-165">**interface_index** Index to the interface where the service is to be disabled</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-166">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-166">Return Values</span></span>

- <span data-ttu-id="36d7e-167">**NX_SUCCESS** (0x00) hizmeti başarıyla devre dışı bıraktı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-167">**NX_SUCCESS** (0x00) Successfully disabled the service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-168">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-168">Allowed From</span></span>

<span data-ttu-id="36d7e-169">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-169">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-170">Example</span></span>

```C
/* Disable mDNS service on specific interface. */

status = nx_mdns_disable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was disabled. */
```

## <a name="nx_mdns_cache_notify_set"></a><span data-ttu-id="36d7e-171">nx_mdns_cache_notify_set</span><span class="sxs-lookup"><span data-stu-id="36d7e-171">nx_mdns_cache_notify_set</span></span>

<span data-ttu-id="36d7e-172">MDNS önbelleği tam bildirim işlevini yükleme</span><span class="sxs-lookup"><span data-stu-id="36d7e-172">Installs the mDNS cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-173">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-173">Prototype</span></span>

```c
UINT nx_mdns_cache_notify_set(NX_MDNS *mdns_ptr,
    VOID (*cache_full_notify_cb)(NX_MDNS *mdns_ptr,
        UINT state, UINT cache_type));
```

### <a name="description"></a><span data-ttu-id="36d7e-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-174">Description</span></span>

<span data-ttu-id="36d7e-175">Bu hizmet, yerel hizmet önbelleği veya eş hizmet Önbelleği dolduğunda çağrılan, Kullanıcı tarafından sağlanan bir geri çağırma işlevi yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="36d7e-175">This service installs a user-supplied callback function, which is invoked when either the local service cache or peer service cache becomes full.</span></span> <span data-ttu-id="36d7e-176">Hizmet Önbelleği dolduğunda, daha fazla mDNS kaynak kaydı eklenemez.</span><span class="sxs-lookup"><span data-stu-id="36d7e-176">When the service cache is full, no more mDNS Resource Record can be added.</span></span> <span data-ttu-id="36d7e-177">Farklı dize uzunluklarına sahip hizmetler eklendiğinde ve kaldırıldığında, hizmet önbelleğinin iç parçalanma sonucu olarak tam hale gelebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36d7e-177">Note that the service cache may become full as a result of internal fragmentation, when services with various string lengths are added and removed.</span></span> <span data-ttu-id="36d7e-178">Eş hizmeti önbelleğinde önbellek tam bildirimi alındığında, uygulama "*nx_mdns_service_cache_clear"* hizmetini kullanarak eş hizmeti önbelleğindeki tüm girdileri silebilir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-178">On receiving a cache full notification on peer service cache, the application may use the service "*nx_mdns_service_cache_clear"* to erase all entries in the peer service cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-179">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-179">Input Parameters</span></span>

- <span data-ttu-id="36d7e-180">**mdns_ptr** MDNS denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-180">**mdns_ptr** Pointer to the mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-181">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-181">Return Values</span></span>

- <span data-ttu-id="36d7e-182">**NX_SUCCESS** (0x00) MDNs önbellek bildirimi geri arama işlevini başarıyla yükledi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-182">**NX_SUCCESS** (0x00) Successfully installed the mDNS cache notify callback function.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-183">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-183">Allowed From</span></span>

<span data-ttu-id="36d7e-184">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-184">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-185">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-185">Example</span></span>

```C
/* Set mDNS cache notify callback. */

status = nx_mdns_cache_notify_set(&my_mdns, cache_full_nofiy_cb);

/* If status is NX_SUCCESS, mDNS cache notify callback was set. */
```

## <a name="nx_mdns_cache_notify_clear"></a><span data-ttu-id="36d7e-186">nx_mdns_cache_notify_clear</span><span class="sxs-lookup"><span data-stu-id="36d7e-186">nx_mdns_cache_notify_clear</span></span>

<span data-ttu-id="36d7e-187">MDNS hizmet önbelleği tam bildirim işlevini temizle</span><span class="sxs-lookup"><span data-stu-id="36d7e-187">Clear the mDNS service cache full notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-188">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-188">Prototype</span></span>

```C
UINT nx_mdns_cache_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="36d7e-189">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-189">Description</span></span>

<span data-ttu-id="36d7e-190">Bu hizmet, Kullanıcı tarafından sağlanan bir hizmet önbelleği bildirme geri arama işlevini temizler.</span><span class="sxs-lookup"><span data-stu-id="36d7e-190">This service clears a user-supplied service cache notify callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-191">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-191">Input Parameters</span></span>

- <span data-ttu-id="36d7e-192">**mdns_ptr** MDNS denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-192">**mdns_ptr** Pointer to the mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-193">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-193">Return Values</span></span>

- <span data-ttu-id="36d7e-194">**NX_SUCCESS** (0x00), MDNs hizmeti önbellek bildirimi geri arama işlevini başarıyla temizledi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-194">**NX_SUCCESS** (0x00) Successfully cleared the mDNS service cache notify callback function.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-195">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-195">Allowed From</span></span>

<span data-ttu-id="36d7e-196">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-196">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-197">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-197">Example</span></span>

```C
/* Clear mDNS cache notify callback. */

status = nx_mdns_cache_notify_clear(&my_mdns);

/* If status is NX_SUCCESS, mDNS cache notify callback clear. */
```

## <a name="nx_mdns_domain_name_set"></a><span data-ttu-id="36d7e-198">nx_mdns_domain_name_set</span><span class="sxs-lookup"><span data-stu-id="36d7e-198">nx_mdns_domain_name_set</span></span>

<span data-ttu-id="36d7e-199">Etki alanı adını ayarlar</span><span class="sxs-lookup"><span data-stu-id="36d7e-199">Sets the domain name</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-200">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-200">Prototype</span></span>

```C
UINT nx_mdns_domain_name_set(NX_MDNS *mdns_ptr, CHAR *domain_name);
```

### <a name="description"></a><span data-ttu-id="36d7e-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-201">Description</span></span>

<span data-ttu-id="36d7e-202">Bu hizmet varsayılan yerel etki alanı adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36d7e-202">This service sets up the default local domain name.</span></span> <span data-ttu-id="36d7e-203">MDNS örneği oluşturulduğunda, varsayılan yerel etki alanı adı ". Local" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-203">When the mDNS instance is created, the default local domain name is set to “.local”.</span></span> <span data-ttu-id="36d7e-204">Bu API, bir uygulamanın varsayılan yerel etki alanı adının üzerine yazılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-204">This API allows an application to overwrite the default local domain name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-205">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-205">Input Parameters</span></span>

- <span data-ttu-id="36d7e-206">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-206">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-207">**domain_name** Kullanılacak etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-207">**domain_name** The domain name to be used.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-208">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-208">Return Values</span></span>

- <span data-ttu-id="36d7e-209">**NX_SUCCESS** (0x00) yerel etki alanı başarıyla yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-209">**NX_SUCCESS** (0x00) Successfully configured local domain.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-210">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-210">Allowed From</span></span>

<span data-ttu-id="36d7e-211">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-211">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-212">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-212">Example</span></span>

```C
/* Set the domain name. */

status = nx_mdns_domain_name_set(&my_mdns, “home”);

/* If status is NX_SUCCESS, the “home” domain name was set. */
```

## <a name="nx_mdns_service_announcement_timing_set"></a><span data-ttu-id="36d7e-213">nx_mdns_service_announcement_timing_set</span><span class="sxs-lookup"><span data-stu-id="36d7e-213">nx_mdns_service_announcement_timing_set</span></span>

<span data-ttu-id="36d7e-214">Hizmet duyurusu iletileri için zamanlama parametrelerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="36d7e-214">Sets the timing parameters for service announcement messages</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-215">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-215">Prototype</span></span>

```C
UINT nx_mdns_service_announcement_timing_set(NX_MDNS *mdns_ptr,
    UINT t, UINT p, UINT k, UINT retrans_interval,
    UINT period_interval, UINT max_time);
```

### <a name="description"></a><span data-ttu-id="36d7e-216">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-216">Description</span></span>

<span data-ttu-id="36d7e-217">Bu hizmet, hizmet duyuruları gönderilirken mDNS tarafından çalıştırılan zamanlama parametrelerini yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-217">This service reconfigures the timing parameters employed by mDNS when sending the service announcements.</span></span> <span data-ttu-id="36d7e-218">Yayımlama dönemi *t* işaretleri ' nden başlar ve *k* faktörü 'nin gücünden 2 ile telescop'e göre genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-218">Publish period starts from *t* ticks and can be expanded telescopically with 2 to the power of *k* factor.</span></span> <span data-ttu-id="36d7e-219">Tanıtım başına gün sayısı *p*, yinelenen her reklam arasındaki Aralık *Aralık* işaretleri ve duyuru dönemi sayısı max_time.</span><span class="sxs-lookup"><span data-stu-id="36d7e-219">The number of repetitions per advertisement is *p*, the interval between each repeated advertisement is *interval* ticks, and the number of announcement period is max_time.</span></span> <span data-ttu-id="36d7e-220">Varsayılan olarak, başlangıç dönemi 1 saniye, k = 1 ile ayarlanır (her seferinde nokta iki katına çıkar), *p = 1* (yineleme yok), retrans_interval = 0 (zaman aralığı yok), Period_interval = 0xFFFFFFFF (en fazla süre aralığı) ve max_time = 3 (reklam sayısı).</span><span class="sxs-lookup"><span data-stu-id="36d7e-220">By default, the initial period is set to 1 second, with k = 1 (the period doubles each time), *p = 1* (no repetition), retrans_interval = 0(no time interval), period_interval = 0xFFFFFFFF(max period interval) and max_time = 3(number of advertisement).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-221">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-221">Input Parameters</span></span>

- <span data-ttu-id="36d7e-222">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-222">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-223">başlangıç dönemi için **t** onay işareti sayısı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-223">**t** Number of ticks for the initial period.</span></span> <span data-ttu-id="36d7e-224">1 saniye için varsayılan değer 100 ' dir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-224">Default is 100 ticks for 1 second.</span></span>
- <span data-ttu-id="36d7e-225">**p** Tekrarlamaların sayısı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-225">**p** Number of repetitions.</span></span> <span data-ttu-id="36d7e-226">Varsayılan değer 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-226">Default value is 1.</span></span>
- <span data-ttu-id="36d7e-227">**k** Telescopic faktörü.</span><span class="sxs-lookup"><span data-stu-id="36d7e-227">**k** Telescopic factor.</span></span> <span data-ttu-id="36d7e-228">Varsayılan değer 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-228">Default value is 1.</span></span>
- <span data-ttu-id="36d7e-229">**retrans_interval** Yinelenen duyuru iletileri gönderilmeden önce beklenecek onay işareti sayısı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-229">**retrans_interval** Number of ticks to wait before sending out repeated announcement messages.</span></span> <span data-ttu-id="36d7e-230">Varsayılan değer 0 ' dır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-230">Default value is 0.</span></span>
- <span data-ttu-id="36d7e-231">**period_interval** İki duyuru dönemi arasındaki onay işareti sayısı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-231">**period_interval** Number of ticks between two announcement period.</span></span> <span data-ttu-id="36d7e-232">Varsayılan değer 0xFFFFFFFF ' dir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-232">Default value is 0xFFFFFFFF.</span></span>
- <span data-ttu-id="36d7e-233">**max_time** Tanıtım için kullanılacak duyuru dönemi sayısı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-233">**max_time** Number of announcement period to use for the advertisement.</span></span> <span data-ttu-id="36d7e-234">*Max_time* duyuru dönemlerinde daha fazla duyuru iletisi gönderilmez.</span><span class="sxs-lookup"><span data-stu-id="36d7e-234">After the *max_time* announcement periods, no more announcement messages are sent.</span></span> <span data-ttu-id="36d7e-235">Varsayılan değer 3’tür.</span><span class="sxs-lookup"><span data-stu-id="36d7e-235">Default value is 3.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-236">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-236">Return Values</span></span>

- <span data-ttu-id="36d7e-237">**NX_SUCCESS** (0x00) zamanlama değerlerini başarıyla ayarlıyor.</span><span class="sxs-lookup"><span data-stu-id="36d7e-237">**NX_SUCCESS** (0x00) Successfully sets the timing values.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-238">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-238">Allowed From</span></span>

<span data-ttu-id="36d7e-239">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-239">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-240">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-240">Example</span></span>

```C
/* Set the service announcement timing. */

status = nx_mdns_service_announcement_timing_set(&my_mdns, 100,
    1, 1, 0, 0xFFFFFFFF, 3);

/* If status is NX_SUCCESS, the service announcement timing was set. */
```

## <a name="nx_mdns_service_add"></a><span data-ttu-id="36d7e-241">nx_mdns_service_add</span><span class="sxs-lookup"><span data-stu-id="36d7e-241">nx_mdns_service_add</span></span>

<span data-ttu-id="36d7e-242">Yerel hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="36d7e-242">Add a local service</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-243">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-243">Prototype</span></span>

```C
UINT nx_mdns_service_add(NX_MDNS *mdns_ptr, CHAR *instance,
    CHAR *service, CHAR *subtype, UINT ttl, USHORT priority,
    USHORT weight, USHORT port, UCHAR *text, UCHAR is_unique,
    UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="36d7e-244">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-244">Description</span></span>

<span data-ttu-id="36d7e-245">Bu API, uygulama tarafından sunulan bir hizmeti kaydeder.</span><span class="sxs-lookup"><span data-stu-id="36d7e-245">This API registers a service offered by the application.</span></span> <span data-ttu-id="36d7e-246">Bayrak *is_unique* ayarlandıysa, MDNs, ağdaki hizmeti duyurmadan önce yerel ağda benzersiz olduğundan emin olmak için hizmet adını yoklayın.</span><span class="sxs-lookup"><span data-stu-id="36d7e-246">If the flag *is_unique* is set, mDNS probes the service name to make sure it is unique on the local network before starting to announce the service on the network.</span></span> <span data-ttu-id="36d7e-247">*Örnek* , hizmet adının örnek bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="36d7e-247">*Instance* is the instance portion of the service name.</span></span> <span data-ttu-id="36d7e-248">Hizmet *,* hizmet adının hizmet bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="36d7e-248">The *service* is the service portion of the service name.</span></span> <span data-ttu-id="36d7e-249">Örneğin, "_HTTP. _tcp" bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-249">For example “_http._tcp” is a service.</span></span> <span data-ttu-id="36d7e-250">Alt türe sahip bir hizmeti anlatmak için çağıranın *Subtype* parametresini kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-250">To describe a service with subtype, caller must use the *subtype* parameter.</span></span> <span data-ttu-id="36d7e-251">Örneğin, istenen hizmet "_printer. _sub. _HTTP. _tcp" ise, hizmet alanı "_HTTP. _tcp:" ve alt tür alanı "_printer" olur.</span><span class="sxs-lookup"><span data-stu-id="36d7e-251">For example, if the desired service is “_printer._sub._http._tcp”, the service field is “_http._tcp:, and the subtype field is “_printer”.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-252">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-252">Input Parameters</span></span>

- <span data-ttu-id="36d7e-253">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-253">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-254">**örnek** Hizmetin örnek adına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-254">**instance** Pointer to the instance name of the service.</span></span>
- <span data-ttu-id="36d7e-255">**hizmet** Alt tür bilgileri hariç mDNS hizmet türüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-255">**service** Pointer to the mDNS service type, excluding subtype information.</span></span>
- <span data-ttu-id="36d7e-256">**alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-256">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>
- <span data-ttu-id="36d7e-257">**Öncelik** Hizmet önceliği</span><span class="sxs-lookup"><span data-stu-id="36d7e-257">**priority** Service priority</span></span>
- <span data-ttu-id="36d7e-258">**ağırlığı** Hizmet ağırlığı</span><span class="sxs-lookup"><span data-stu-id="36d7e-258">**weight** Service weight</span></span>
- <span data-ttu-id="36d7e-259">**bağlantı noktası** Hizmetin kullandığı TCP veya UDP bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="36d7e-259">**port** TCP or UDP port number the service uses</span></span>
- <span data-ttu-id="36d7e-260">**metin** Ek metin bilgileri</span><span class="sxs-lookup"><span data-stu-id="36d7e-260">**text** Additional text information</span></span>
- <span data-ttu-id="36d7e-261">**is_unique** Hizmetin paylaşılıp paylaşılmadığını veya benzersiz olduğunu belirten Boole bayrağı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-261">**is_unique** Boolean flag indicating whether the service is shared or unique.</span></span> <span data-ttu-id="36d7e-262">Benzersiz olarak kaydedilen hizmetler için mDNS, servisi sunmaya başlamadan önce ağdaki hizmeti araştırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-262">For services registered as unique, mDNS must probe the service on the network before starting offering it.</span></span>
- <span data-ttu-id="36d7e-263">**Interface_index** Hizmetin sunduğu fiziksel arabirim.</span><span class="sxs-lookup"><span data-stu-id="36d7e-263">**Interface_index** Physical interface the service is offered through.</span></span> <span data-ttu-id="36d7e-264">İliştirilmiş hizmetlerden herhangi biri üzerinden sunulan bir hizmet için *NX_MDNS_ALL_INTERFACES* değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-264">For a service that is offered through any of the attached services, the value *NX_MDNS_ALL_INTERFACES* is used.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-265">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-265">Return Values</span></span>

- <span data-ttu-id="36d7e-266">**NX_SUCCESS** (0x00) hizmet başarıyla kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-266">**NX_SUCCESS** (0x00) Successfully registered the service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-267">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-267">Allowed From</span></span>

<span data-ttu-id="36d7e-268">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-268">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-269">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-269">Example</span></span>

```C
/* Add local service. */

status = nx_mdns_service_add(&my_mdns, “NETX-SERVICE”,
    “_http._tcp”, NX_NULL,
    NX_NULL, 0, 0, 0, 80, NX_TRUE, 0);

/* If status is NX_SUCCESS, The service (NetX-SERVICE._http._tcp.local) was added. */
```

## <a name="nx_mdns_service_delete"></a><span data-ttu-id="36d7e-270">nx_mdns_service_delete</span><span class="sxs-lookup"><span data-stu-id="36d7e-270">nx_mdns_service_delete</span></span>

<span data-ttu-id="36d7e-271">Önceki kayıtlı bir hizmeti Kaldır</span><span class="sxs-lookup"><span data-stu-id="36d7e-271">Remove a previous registered service</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-272">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-272">Prototype</span></span>

```C
UINT nx_mdns_service_delete(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service,
    CHAR *subtype);
```

### <a name="description"></a><span data-ttu-id="36d7e-273">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-273">Description</span></span>

<span data-ttu-id="36d7e-274">Bu API, önceki kayıtlı bir hizmeti siler.</span><span class="sxs-lookup"><span data-stu-id="36d7e-274">This API deletes a previous registered service.</span></span> <span data-ttu-id="36d7e-275">Hizmet silindiğinden, komşu düğümlerin bildirilmesi için yerel ağa "güle" iletileri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-275">As the service is deleted, "goodbye" messages are sent to the local network so the neighboring nodes are notified.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-276">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-276">Input Parameters</span></span>

- <span data-ttu-id="36d7e-277">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-277">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-278">**örnek** Hizmetin örnek adına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-278">**instance** Pointer to the instance name of the service.</span></span>
- <span data-ttu-id="36d7e-279">**hizmet** Alt tür bilgileri hariç mDNS hizmet türüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-279">**service** Pointer to the mDNS service type, excluding subtype information.</span></span>
- <span data-ttu-id="36d7e-280">**alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-280">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-281">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-281">Return Values</span></span>

- <span data-ttu-id="36d7e-282">**NX_SUCCESS** (0x00) hizmeti başarıyla sildi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-282">**NX_SUCCESS** (0x00) Successfully deleted the service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-283">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-283">Allowed From</span></span>

<span data-ttu-id="36d7e-284">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-284">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-285">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-285">Example</span></span>

```C
/* Delete local service. */

status = nx_mdns_service_delete(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The service (NetX-SERVICE._http._tcp.local) was deleted. */
```

## <a name="nx_mdns_service_one_shot_query"></a><span data-ttu-id="36d7e-286">nx_mdns_service_one_shot_query</span><span class="sxs-lookup"><span data-stu-id="36d7e-286">nx_mdns_service_one_shot_query</span></span>

<span data-ttu-id="36d7e-287">Tek basamaklı hizmet bulma başlatın</span><span class="sxs-lookup"><span data-stu-id="36d7e-287">Initiate one-shot service discovery</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-288">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-288">Prototype</span></span>

```C
UINT nx_mdns_service_one_shot_query(NX_MDNS *mdns_ptr,
    UCHAR *instance,
    UCHAR *service,
    UCHAR *subtype,
    NX_MDNS_SERVICE *service_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36d7e-289">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-289">Description</span></span>

<span data-ttu-id="36d7e-290">Bu hizmet, tek seferlik bir mDNS sorgusu gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-290">This service performs a one-shot mDNS query.</span></span> <span data-ttu-id="36d7e-291">Belirtilen hizmet eş hizmeti önbelleğinde bulunursa, ilk örnek döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36d7e-291">If the specified service is found in the peer service cache, the first instance is returned.</span></span> <span data-ttu-id="36d7e-292">Yerel eş hizmeti önbelleğinde hiçbir hizmet bulunmazsa, mDNS modülü bir sorgu komutu yayınlar ve yanıt bekler.</span><span class="sxs-lookup"><span data-stu-id="36d7e-292">If no services are found in the local peer service cache, the mDNS module issues a query command and wait for response.</span></span> <span data-ttu-id="36d7e-293">İlk yanıt alınana veya sorgu zaman aşımına uğrayana kadar hizmet engellenir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-293">The service is blocked till either the first answer is received or the query times out.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-294">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-294">Input Parameters</span></span>

- <span data-ttu-id="36d7e-295">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-295">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-296">**örnek** Varsa hizmetin örnek adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-296">**instance** Pointer to the instance name of the service, if applicable.</span></span>
- <span data-ttu-id="36d7e-297">**hizmet** Alt tür bilgileri hariç mDNS hizmet türüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-297">**service** Pointer to the mDNS service type, excluding subtype information.</span></span> <span data-ttu-id="36d7e-298">uygulamanın hizmet türünü belirtmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-298">the application must specify the service type.</span></span>
- <span data-ttu-id="36d7e-299">**alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-299">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>
- <span data-ttu-id="36d7e-300">**service_ptr** Kullanıcı tarafından sorgu sonuçlarını depolayan NX_MDNS_SERVICE yapısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-300">**service_ptr** User provided pointer to NX_MDNS_SERVICE structure that stores the query results.</span></span>
- <span data-ttu-id="36d7e-301">**wait_option** Bir yanıt için beklemek için zaman işaretleri cinsinden süre miktarı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-301">**wait_option** The amount of time, in ticks, to wait for a response.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-302">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-302">Return Values</span></span>

- <span data-ttu-id="36d7e-303">**NX_SUCCESS** (0x00) hizmet bilgilerini başarıyla aldı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-303">**NX_SUCCESS** (0x00) Successfully obtained service information.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-304">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-304">Allowed From</span></span>

<span data-ttu-id="36d7e-305">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-305">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-306">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-306">Example</span></span>

```C
/* Start service one shot query. */

status = nx_mdns_service_one_shot_query(&my_mdns, “NETX-SERVICE”, “_http._tcp”,
    NX_NULL, service_ptr, 500);

/* If status is NX_SUCCESS, The query with
    name: NetX-SERVICE._http._tcp.local,
     type: ANY (SRV and TXT) was sent.
    And the answer was stored in service_ptr if success. */
```

## <a name="nx_mdns_service_continuous_query"></a><span data-ttu-id="36d7e-307">nx_mdns_service_continuous_query</span><span class="sxs-lookup"><span data-stu-id="36d7e-307">nx_mdns_service_continuous_query</span></span>

<span data-ttu-id="36d7e-308">Sürekli hizmet bulmayı Başlat</span><span class="sxs-lookup"><span data-stu-id="36d7e-308">Initiate continuous service discovery</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-309">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-309">Prototype</span></span>

```C
UINT nx_mdns_service_continous_query(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a><span data-ttu-id="36d7e-310">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-310">Description</span></span>

<span data-ttu-id="36d7e-311">Bu hizmet sürekli bir sorgu başlatır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-311">This service starts a continuous query.</span></span> <span data-ttu-id="36d7e-312">Hizmetin hemen geri döndüğünü unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36d7e-312">Note that the service returns immediately.</span></span> <span data-ttu-id="36d7e-313">Sürekli bir sorgu yayınladıktan sonra, uygulama API *nx_mdns_service_lookup* kullanarak hizmet kaydını alabilir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-313">After issuing a continuous query, the application may retrieve service record by using the API *nx_mdns_service_lookup*.</span></span> <span data-ttu-id="36d7e-314">Sürekli sorguyu durdurmak için, uygulama API 'YI kullanabilir *nx_mdns_service_query_stop*</span><span class="sxs-lookup"><span data-stu-id="36d7e-314">To stop the continuous query, the application may use the API *nx_mdns_service_query_stop*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-315">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-315">Input Parameters</span></span>

- <span data-ttu-id="36d7e-316">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-316">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-317">**örnek** Varsa hizmetin örnek adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-317">**instance** Pointer to the instance name of the service, if applicable.</span></span>
- <span data-ttu-id="36d7e-318">**hizmet** Varsa, alt tür bilgisi hariç olmak üzere mDNS hizmet türüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-318">**service** Pointer to the mDNS service type, excluding subtype information, if applicable.</span></span>
- <span data-ttu-id="36d7e-319">**alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-319">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-320">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-320">Return Values</span></span>

- <span data-ttu-id="36d7e-321">**NX_SUCCESS** (0x00) başarıyla başlatıldı sorgusu devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="36d7e-321">**NX_SUCCESS** (0x00) Successfully started continues query.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-322">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-322">Allowed From</span></span>

<span data-ttu-id="36d7e-323">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-323">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-324">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-324">Example</span></span>

```C
/* Start service continuous query. */

status = nx_mdns_service_continuous_query(&my_mdns,
    “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The continuous query with
    name: NetX-SERVICE._http._tcp.local,
    type: ANY (SRV and TXT) was added.
    And the query will be periodically sent. */
```

## <a name="nx_mdns_service_query_stop"></a><span data-ttu-id="36d7e-325">nx_mdns_service_query_stop</span><span class="sxs-lookup"><span data-stu-id="36d7e-325">nx_mdns_service_query_stop</span></span>

<span data-ttu-id="36d7e-326">Daha önce verilen bir sürekli hizmet bulmayı sona erdirin</span><span class="sxs-lookup"><span data-stu-id="36d7e-326">Cease a previously issued continuous service discovery</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-327">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-327">Prototype</span></span>

```C
UINT nx_mdns_service_query_stop(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a><span data-ttu-id="36d7e-328">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-328">Description</span></span>

<span data-ttu-id="36d7e-329">Bu API, önceki yayımlanmış bir sürekli hizmet bulmayı sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-329">This API terminates a previous issued continuous service discovery.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-330">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-330">Input Parameters</span></span>

- <span data-ttu-id="36d7e-331">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-331">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-332">**örnek** Hizmetin örnek adına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-332">**instance** Pointer to the instance name of the service.</span></span>
- <span data-ttu-id="36d7e-333">**hizmet** MDNS hizmet türü, alt tür bilgisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-333">**service** Pointer to the mDNS service type, subtype information.</span></span>
- <span data-ttu-id="36d7e-334">**alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-334">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-335">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-335">Return Values</span></span>

- <span data-ttu-id="36d7e-336">**NX_SUCCESS** (0x00) devam eden sorgu başarıyla durduruldu.</span><span class="sxs-lookup"><span data-stu-id="36d7e-336">**NX_SUCCESS** (0x00) Successfully stopped continues query.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-337">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-337">Allowed From</span></span>

<span data-ttu-id="36d7e-338">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-338">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-339">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-339">Example</span></span>

```C
/* Stop service continuous query. */

status = nx_mdns_service_query_stop(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The continuous query with
    name: NetX-SERVICE._http._tcp.local,
    type: ANY (SRV and TXT) was stopped. */
```

## <a name="nx_mdns_service_lookup"></a><span data-ttu-id="36d7e-340">nx_mdns_service_lookup</span><span class="sxs-lookup"><span data-stu-id="36d7e-340">nx_mdns_service_lookup</span></span>

<span data-ttu-id="36d7e-341">Hizmeti yerel eş hizmeti önbelleğinden alır</span><span class="sxs-lookup"><span data-stu-id="36d7e-341">Retrieves the service from the local peer service cache</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-342">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-342">Prototype</span></span>

```C
UINT nx_mdns_service_lookup(NXD_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service,
    CHAR *subtype, UINT instance_index,
    NXD_MDNS_SERVICE *service_ptr);
```

### <a name="description"></a><span data-ttu-id="36d7e-343">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-343">Description</span></span>

<span data-ttu-id="36d7e-344">Bu hizmet, örnek adıyla eşleşen Hizmetleri (sağlanmışsa) ve yerel eş hizmeti önbelleğindeki hizmet türünü arar.</span><span class="sxs-lookup"><span data-stu-id="36d7e-344">This service looks up services matching the instance name (if provided) and the type of service in the local peer service cache.</span></span> <span data-ttu-id="36d7e-345">Uygulama, açıklama ile eşleşen önbellekteki ilk hizmet için *instance_index* ayarlanmış olan hizmet aramasını başlatacak.</span><span class="sxs-lookup"><span data-stu-id="36d7e-345">Application shall start the service lookup with *instance_index* set to zero for the first service in the cache that matches the description.</span></span> <span data-ttu-id="36d7e-346">Uygulama, önbelleğin sonunu gösteren *NX_NO_MORE_ENTRIES* döndürdüğünden, bu hizmeti önbellekte bulunan ek hizmetler için artan *instance_index* değerle kullanmaya devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="36d7e-346">Application shall keep using this service with increasing *instance_index* value for additional services found in the cache, till the service returns *NX_NO_MORE_ENTRIES*, which indicates the end of the cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-347">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-347">Input Parameters</span></span>

- <span data-ttu-id="36d7e-348">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-348">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-349">**örnek** Varsa hizmetin örnek adının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-349">**instance** Pointer to the instance name of the service, if applicable.</span></span>
- <span data-ttu-id="36d7e-350">**hizmet** Varsa, alt tür bilgisi hariç olmak üzere mDNS hizmet türüne yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-350">**service** Pointer to the mDNS service type, excluding subtype information, if applicable.</span></span>
- <span data-ttu-id="36d7e-351">**alt tür** Varsa mDNS hizmetinin alt tür kısmına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-351">**subtype** Pointer to the subtype portion of the mDNS service, if applicable.</span></span>
- <span data-ttu-id="36d7e-352">**Instance_index** Döndürülecek örneğe Dizin numarası.</span><span class="sxs-lookup"><span data-stu-id="36d7e-352">**Instance_index** Index number to the instance to be returned.</span></span>
- <span data-ttu-id="36d7e-353">**service_ptr** Kullanıcı, arama sonuçlarını depolayan NX_MDNS_SERVICE yapısına işaret eden işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-353">**service_ptr** User provided pointer to NX_MDNS_SERVICE structure that stores the lookup results.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-354">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-354">Return Values</span></span>

- <span data-ttu-id="36d7e-355">**NX_SUCCESS** (0x00) hizmet başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="36d7e-355">**NX_SUCCESS** (0x00) Successfully retrieved the service</span></span>
- <span data-ttu-id="36d7e-356">**NX_NO_MORE_ENTRIES** (0x17) belirtilen dizin numarasında hizmet girdisi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-356">**NX_NO_MORE_ENTRIES** (0x17) No service entry is found at the specified index number.</span></span> <span data-ttu-id="36d7e-357">Bu hata kodu aramanın sonunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-357">This error code indicates the end of the search.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-358">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-358">Allowed From</span></span>

<span data-ttu-id="36d7e-359">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-359">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-360">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-360">Example</span></span>

```C
/* Lookup the service on specific index. */

status = nx_mdns_service_lookup(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL,
    0, service_ptr);

/* If status is NX_SUCCESS, The service with
    name: NetX-SERVICE._http._tcp.local, was retrieved. */
```

## <a name="nx_mdns_service_ignore_set"></a><span data-ttu-id="36d7e-361">nx_mdns_service_ignore_set</span><span class="sxs-lookup"><span data-stu-id="36d7e-361">nx_mdns_service_ignore_set</span></span>

<span data-ttu-id="36d7e-362">Bir hizmet yoksayma kümesini yapılandırır</span><span class="sxs-lookup"><span data-stu-id="36d7e-362">Configures a service ignore set</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-363">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-363">Prototype</span></span>

```C
UINT nx_mdns_service_ignore_set(NX_MDNS *mdns_ptr, ULONG service_mask);
```

### <a name="description"></a><span data-ttu-id="36d7e-364">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-364">Description</span></span>

<span data-ttu-id="36d7e-365">Bu API, *service_mask* bit maskesi tarafından belirtilen hizmetleri yoksayacak bir maske yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-365">This API configures a mask to ignore services specified by the *service_mask* bitmask.</span></span> <span data-ttu-id="36d7e-366">Kullanıcı isteğe bağlı olarak, önbelleğe alınmasını istemediğiniz hizmet türlerini seçmek için service_mask kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-366">User may optionally use the service_mask to select service types it does not wish to be cached.</span></span> <span data-ttu-id="36d7e-367">*Nxd_mdns. c* ' de *nx_mdns_service_types* tabloda tanımlanmış bir hizmet listesi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-367">A list of services is defined in the table *nx_mdns_service_types* in *nxd_mdns.c.*</span></span> <span data-ttu-id="36d7e-368">Nx_mdns_service_types [] içindeki ilk hizmet türünün karşılık gelen maskesi 0x00000001, ikinci hizmet türünün maskesi 0x00000002 ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="36d7e-368">The corresponding mask of the first service type in nx_mdns_service_types[] is 0x00000001, the mask of the second service type is 0x00000002, and so on.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-369">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-369">Input Parameters</span></span>

- <span data-ttu-id="36d7e-370">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-370">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-371">**service_mask** Yok sayılacak Kullanıcı tanımlı hizmet türleri.</span><span class="sxs-lookup"><span data-stu-id="36d7e-371">**service_mask** User-defined service types to ignore.</span></span> <span data-ttu-id="36d7e-372">Maske, 32 bitlik bir ULONG türüdür.</span><span class="sxs-lookup"><span data-stu-id="36d7e-372">The mask is a 32-bit ULONG type.</span></span> <span data-ttu-id="36d7e-373">Her bit, Kullanıcı tanımlı *nx_mdns_service_types* dizisindeki bir girişi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="36d7e-373">Each bit represents an entry in the user-defined *nx_mdns_service_types* array.</span></span> <span data-ttu-id="36d7e-374">Bir bit ayarlandıysa, *nx_mdns_service_type* dizisinde belirtilen karşılık gelen hizmet türü, eş hizmeti önbelleğinde depoolmaz.</span><span class="sxs-lookup"><span data-stu-id="36d7e-374">If a bit is set, the corresponding service type specified in the *nx_mdns_service_type* array will not store in the peer service cache.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-375">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-375">Return Values</span></span>

- <span data-ttu-id="36d7e-376">**NX_SUCCESS** (0x00) hizmeti yoksayma maskesini başarıyla ayarlıyor.</span><span class="sxs-lookup"><span data-stu-id="36d7e-376">**NX_SUCCESS** (0x00) Successfully sets the service ignore mask.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-377">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-377">Allowed From</span></span>

<span data-ttu-id="36d7e-378">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-378">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-379">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-379">Example</span></span>

```C
/* Set the service mask to ignore the specified service. */

status = nx_mdns_service_ignore_set(&my_mdns, 0x00000003);

/* If status is NX_SUCCESS, The service with
    type “_device-info” and “_http” will be ignored. */
```

## <a name="nx_mdns_service_notify_set"></a><span data-ttu-id="36d7e-380">nx_mdns_service_notify_set</span><span class="sxs-lookup"><span data-stu-id="36d7e-380">nx_mdns_service_notify_set</span></span>

<span data-ttu-id="36d7e-381">Bir hizmet değişikliği bildirme geri arama işlevini yapılandırır</span><span class="sxs-lookup"><span data-stu-id="36d7e-381">Configures a service change notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-382">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-382">Prototype</span></span>

```C
UINT nx_mdns_service_notify_set(NX_MDNS *mdns_ptr, ULONG service_mask,
    VOID (*service_change_notify)(NX_MDNS *mdns_ptr,
    NX_MDNS_SERVICE *service_ptr, UINT state));
```

### <a name="description"></a><span data-ttu-id="36d7e-383">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-383">Description</span></span>

<span data-ttu-id="36d7e-384">Bu API, bir hizmet değişikliği bildirme geri arama işlevini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-384">This API configures a service change notify callback function.</span></span> <span data-ttu-id="36d7e-385">Bu geri çağırma işlevi, ağdaki diğer düğümler tarafından sunulan bir hizmet eklendiğinde, değiştirildiğinde veya artık kullanılabilir olmadığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-385">This callback function is invoked when a service offered by other nodes on the network is added, changed or is no longer available.</span></span> <span data-ttu-id="36d7e-386">Kullanıcı, izlemek istediği hizmet türlerini seçmek için isteğe bağlı olarak service_mask kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-386">User may optionally use the service_mask to select service types it wishes to monitor.</span></span> <span data-ttu-id="36d7e-387">İzlenen hizmetlerin bir listesi, *nxd_mdns. c* içindeki *nx_mdns_service_types* tabloda sabit kodludur.</span><span class="sxs-lookup"><span data-stu-id="36d7e-387">A list of services being monitored are hard-coded in the table *nx_mdns_service_types* in *nxd_mdns.c.*</span></span>

<span data-ttu-id="36d7e-388">Nx_mdns_service_types [] içindeki ilk hizmet türünün karşılık gelen maskesi 0x00000001, ikinci hizmet türünün maskesi 0x00000002 ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="36d7e-388">The corresponding mask of the first service type in nx_mdns_service_types[] is 0x00000001, the mask of the second service type is 0x00000002, and so on.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-389">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-389">Input Parameters</span></span>

- <span data-ttu-id="36d7e-390">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-390">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-391">**service_mask** İzlenecek Kullanıcı tanımlı hizmet türleri.</span><span class="sxs-lookup"><span data-stu-id="36d7e-391">**service_mask** User-defined service types to monitor.</span></span> <span data-ttu-id="36d7e-392">Maske, 32 bitlik bir ULONG türüdür.</span><span class="sxs-lookup"><span data-stu-id="36d7e-392">The mask is a 32-bit ULONG type.</span></span> <span data-ttu-id="36d7e-393">Her bit *nx_mdns_service_types* dizideki bir girişi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="36d7e-393">Each bit represents an entry in the *nx_mdns_service_types* array.</span></span>
- <span data-ttu-id="36d7e-394">**service_change_notify** Belirtilen hizmet değiştirildiğinde çağrılacak geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-394">**service_change_notify** The callback function to be invoked when the specified service is changed.</span></span> <span data-ttu-id="36d7e-395">Ayrıntılı hizmet bilgileri service_ptr tarafından işaret edilen bellekte döndürülür *.*</span><span class="sxs-lookup"><span data-stu-id="36d7e-395">The detailed service information is returned in the memory pointed to by *service_ptr.*</span></span> <span data-ttu-id="36d7e-396">Geri aramayı bildir işlevinden döndükten sonra bellekteki içeriğin geçersiz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36d7e-396">Note that the content in the memory is invalid after returning from the notify callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-397">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-397">Return Values</span></span>

- <span data-ttu-id="36d7e-398">**NX_SUCCESS** (0x00) geri çağırma işlevi başarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-398">**NX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-399">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-399">Allowed From</span></span>

<span data-ttu-id="36d7e-400">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-400">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-401">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-401">Example</span></span>

```C
/* Set the service mask to notify the specified service. */

status = nx_mdns_service_notify_set(&my_mdns, 0x00000002, service_change_notify);

/* If status is NX_SUCCESS, the callback will be called
    if received the service with type “_http”. */
```

## <a name="nx_mdns_service_notify_clear"></a><span data-ttu-id="36d7e-402">nx_mdns_service_notify_clear</span><span class="sxs-lookup"><span data-stu-id="36d7e-402">nx_mdns_service_notify_clear</span></span>

<span data-ttu-id="36d7e-403">Hizmet değiştirme bildirimi geri arama işlevini temizle</span><span class="sxs-lookup"><span data-stu-id="36d7e-403">Clear the service change notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-404">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-404">Prototype</span></span>

```C
UINT nx_mdns_service_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="36d7e-405">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-405">Description</span></span>

<span data-ttu-id="36d7e-406">Bu API, hizmet değişikliği bildirme geri arama işlevini ve öğesini temizler.</span><span class="sxs-lookup"><span data-stu-id="36d7e-406">This API clears the service change notify callback function and the .</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-407">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-407">Input Parameters</span></span>

- <span data-ttu-id="36d7e-408">**mdns_ptr** MDNS denetim bloğu işaretçisi..</span><span class="sxs-lookup"><span data-stu-id="36d7e-408">**mdns_ptr** Pointer to mDNS control block..</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-409">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-409">Return Values</span></span>

- <span data-ttu-id="36d7e-410">**NX_SUCCESS** (0x00) geri çağırma işlevini başarıyla temizledi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-410">**NX_SUCCESS** (0x00) Successfully cleared the callback function.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-411">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-411">Allowed From</span></span>

<span data-ttu-id="36d7e-412">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-412">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-413">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-413">Example</span></span>

```C
/* Clear the service notify. */

status = nx_mdns_service_notify_clear(&my_mdns);

/* If status is NX_SUCCESS, the service notify function clear. */
```

## <a name="nx_mdns_host_address_get"></a><span data-ttu-id="36d7e-414">nx_mdns_host_address_get</span><span class="sxs-lookup"><span data-stu-id="36d7e-414">nx_mdns_host_address_get</span></span>

<span data-ttu-id="36d7e-415">Konak adresini al</span><span class="sxs-lookup"><span data-stu-id="36d7e-415">Get the host address</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-416">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-416">Prototype</span></span>

```C
UINT nx_mdns_host_address_get(NX_MDNS *mdns_ptr,
    UCHAR *host_name, ULONG *ipv4_address,
    ULONG *ipv6_address, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36d7e-417">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-417">Description</span></span>

<span data-ttu-id="36d7e-418">Bu hizmet, ana bilgisayar IPv4 ve IPv6 adresleri üzerinde bir mDNS sorgusu gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-418">This service performs a mDNS query on host IPv4 and IPv6 addresses.</span></span> <span data-ttu-id="36d7e-419">Belirtilen ana bilgisayar adının adresi eş hizmeti önbelleğinde bulunursa, adres döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36d7e-419">If the address of specified host name is found in peer service cache, the address is returned.</span></span> <span data-ttu-id="36d7e-420">Eş hizmeti önbelleğinde bir adres bulunmazsa, mDNS modülü A ve AAAA tür sorgularını yayınlar ve yanıt bekler.</span><span class="sxs-lookup"><span data-stu-id="36d7e-420">If no address is found in the peer service cache, the mDNS module issues A and AAAA type queries and wait for response.</span></span> <span data-ttu-id="36d7e-421">Bu API, bir yanıt alınana ya da sorgu zaman aşımına uğrayana kadar engeller.</span><span class="sxs-lookup"><span data-stu-id="36d7e-421">This API blocks until either an answer is received or the query times out.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-422">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-422">Input Parameters</span></span>

- <span data-ttu-id="36d7e-423">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-423">**mdns_ptr** Pointer to mDNS control block.</span></span>
- <span data-ttu-id="36d7e-424">**host_name** Ana bilgisayar adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-424">**host_name** Pointer to host name.</span></span>
- <span data-ttu-id="36d7e-425">**ipv4_address** IPv4 adresi depolama alanı için 4 baytlık hizalanmış bir adrese yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-425">**ipv4_address** Pointer to a 4-byte aligned address for IPv4 address storage space.</span></span> <span data-ttu-id="36d7e-426">Kullanıcı IPv4 adresi için 4 bayt alan ayırsın.</span><span class="sxs-lookup"><span data-stu-id="36d7e-426">User shall allocate 4 bytes of space for the IPv4 - address.</span></span> <span data-ttu-id="36d7e-427">Uygulamanın IPv4 adresini alması gerekmiyorsa NX_NULL adresi bu API 'ye geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-427">NX_NULL address can be passed into this API if application does not need to retrieve IPv4 address.</span></span>
- <span data-ttu-id="36d7e-428">**ipv6_address** IPv6 adresi depolama alanı için 4 baytlık hizalanmış adrese yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-428">**ipv6_address** Pointer to the 4-byte aligned address for IPv6 address storage space.</span></span> <span data-ttu-id="36d7e-429">Kullanıcı-IPv6 adresi için 16 bayt alan ayırır.</span><span class="sxs-lookup"><span data-stu-id="36d7e-429">User shall allocate 16 bytes of space for the - IPv6 address.</span></span> <span data-ttu-id="36d7e-430">Uygulamanın IPv6 adresini alması gerekmiyorsa, bu API 'ye NX_NULL adresi geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="36d7e-430">NX_NULL address can be passed into this API if application does not need to retrieve IPv6 address.</span></span>
- <span data-ttu-id="36d7e-431">**wait_option** Bir yanıt için beklemek için zaman işaretleri cinsinden süre miktarı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-431">**wait_option** The amount of time, in ticks, to wait for a response.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-432">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-432">Return Values</span></span>

- <span data-ttu-id="36d7e-433">**NX_SUCCESS** (0x00), ana bilgisayar adresini başarıyla aldı.</span><span class="sxs-lookup"><span data-stu-id="36d7e-433">**NX_SUCCESS** (0x00) Successfully obtained host address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-434">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-434">Allowed From</span></span>

<span data-ttu-id="36d7e-435">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-435">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-436">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-436">Example</span></span>

```C
ULONG ipv4_address;
ULONG ipv6_address[4];

/* Get the IP address of specified host. */
status = nx_mdns_host_address_get(&my_mdns, “MDNS-Host”, &ipv4_address, ipv6_address, 500);

/* If status is NX_SUCCESS, the IP address of specified host was retrieved. */
```

## <a name="nx_mdns_local_cache_clear"></a><span data-ttu-id="36d7e-437">nx_mdns_local_cache_clear</span><span class="sxs-lookup"><span data-stu-id="36d7e-437">nx_mdns_local_cache_clear</span></span>

<span data-ttu-id="36d7e-438">Tüm yerel Hizmetleri Sil</span><span class="sxs-lookup"><span data-stu-id="36d7e-438">Erase all local services</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-439">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-439">Prototype</span></span>

```C
UINT nx_mdns_local_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="36d7e-440">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-440">Description</span></span>

<span data-ttu-id="36d7e-441">Bu hizmet, güle iletisini gönderdikten sonra yerel hizmet önbelleğindeki tüm girişleri temizler.</span><span class="sxs-lookup"><span data-stu-id="36d7e-441">This service clears all entries in the local service cache after send the Goodbye message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-442">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-442">Input Parameters</span></span>

- <span data-ttu-id="36d7e-443">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-443">**mdns_ptr** Pointer to mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-444">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-444">Return Values</span></span>

- <span data-ttu-id="36d7e-445">**NX_SUCCESS** (0x00) önbellekteki tüm girdileri başarıyla sildiniz.</span><span class="sxs-lookup"><span data-stu-id="36d7e-445">**NX_SUCCESS** (0x00) Successfully erased all entries in the cache.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-446">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-446">Allowed From</span></span>

<span data-ttu-id="36d7e-447">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-447">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-448">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-448">Example</span></span>

```C
/* Clear the local cache, delete all local service. */

status = nx_mdns_local_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of local cache were deleted. */
```

## <a name="nx_mdns_peer_cache_clear"></a><span data-ttu-id="36d7e-449">nx_mdns_peer_cache_clear</span><span class="sxs-lookup"><span data-stu-id="36d7e-449">nx_mdns_peer_cache_clear</span></span>

<span data-ttu-id="36d7e-450">Bulunan tüm hizmetleri Sil</span><span class="sxs-lookup"><span data-stu-id="36d7e-450">Erase all the discovered services</span></span>

### <a name="prototype"></a><span data-ttu-id="36d7e-451">Prototype</span><span class="sxs-lookup"><span data-stu-id="36d7e-451">Prototype</span></span>

```C
UINT nx_mdns_peer_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a><span data-ttu-id="36d7e-452">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36d7e-452">Description</span></span>

<span data-ttu-id="36d7e-453">Bu hizmet, eş hizmeti önbelleğindeki tüm girdileri temizler.</span><span class="sxs-lookup"><span data-stu-id="36d7e-453">This service clears all entries in the peer service cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="36d7e-454">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-454">Input Parameters</span></span>

- <span data-ttu-id="36d7e-455">**mdns_ptr** MDNS denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36d7e-455">**mdns_ptr** Pointer to mDNS control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="36d7e-456">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36d7e-456">Return Values</span></span>

- <span data-ttu-id="36d7e-457">**NX_SUCCESS** (0x00) önbellekteki tüm girdileri başarıyla sildiniz.</span><span class="sxs-lookup"><span data-stu-id="36d7e-457">**NX_SUCCESS** (0x00) Successfully erased all entries in the cache.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36d7e-458">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36d7e-458">Allowed From</span></span>

<span data-ttu-id="36d7e-459">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36d7e-459">Threads</span></span>

### <a name="example"></a><span data-ttu-id="36d7e-460">Örnek</span><span class="sxs-lookup"><span data-stu-id="36d7e-460">Example</span></span>

```C
/* Clear the peer cache, delete all peer service. */

status = nx_mdns_peer_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of peer cache were deleted. */
```
