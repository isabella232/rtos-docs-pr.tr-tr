---
title: Bölüm 4-Azure RTOS NetX hizmetlerinin açıklaması
description: Bu bölümde, tüm Azure RTOS NetX Hizmetleri alfabetik sırada bir açıklama bulunur.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 720e573b53070a754618830134f63a8421b9fd29
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825642"
---
# <a name="chapter-4---description-of-azure-rtos-netx-services"></a><span data-ttu-id="36624-103">Bölüm 4-Azure RTOS NetX hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="36624-103">Chapter 4 - Description of Azure RTOS NetX Services</span></span>

<span data-ttu-id="36624-104">Bu bölümde, tüm Azure RTOS NetX Hizmetleri alfabetik sırada bir açıklama bulunur.</span><span class="sxs-lookup"><span data-stu-id="36624-104">This chapter contains a description of all Azure RTOS NetX services in alphabetic order.</span></span> <span data-ttu-id="36624-105">Hizmet adları, benzer tüm hizmetlerin birlikte gruplanabilmesi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="36624-105">Service names are designed so all similar services are grouped together.</span></span> <span data-ttu-id="36624-106">Örneğin, bu bölümün başlangıcında tüm ARP hizmetleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="36624-106">For example, all ARP services are found at the beginning of this chapter.</span></span>

> [!NOTE]
> <span data-ttu-id="36624-107">*Yüksek performanslı NetX API 'den tam olarak yararlanmayan eski uygulama kodu için BSD-Compatible yuva API 'SI kullanılabilir olduğunu unutmayın. BSD-Compatible yuva API 'SI hakkında daha fazla bilgi için ek D 'ye bakın.*</span><span class="sxs-lookup"><span data-stu-id="36624-107">*Note that a BSD-Compatible Socket API is available for legacy application code that cannot take full advantage of the high-performance NetX API. Refer to Appendix D for more information on the BSD-Compatible Socket API.*</span></span>

<span data-ttu-id="36624-108">Her açıklamanın "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan NX_DISABLE_ERROR_CHECKING seçeneğinden etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-108">In the "Return Values" section of each description, values in **BOLD** are not affected by the NX_DISABLE_ERROR_CHECKING option used to disable the API error checking, while values in non-bold are completely disabled.</span></span> <span data-ttu-id="36624-109">"Izin verilen" bölümler, her bir NetX hizmetinin çağrılabilecek olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="36624-109">The "Allowed From" sections indicate from which each NetX service can be called.</span></span>

## <a name="nx_arp_dynamic_entries_invalidate"></a><span data-ttu-id="36624-110">nx_arp_dynamic_entries_invalidate</span><span class="sxs-lookup"><span data-stu-id="36624-110">nx_arp_dynamic_entries_invalidate</span></span>

<span data-ttu-id="36624-111">ARP önbelleğindeki tüm dinamik girdileri geçersiz kıl</span><span class="sxs-lookup"><span data-stu-id="36624-111">Invalidate all dynamic entries in the ARP cache</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-112">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-112">Prototype</span></span>

```C
UINT nx_arp_dynamic_entries_invalidate(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-113">Description</span></span>

<span data-ttu-id="36624-114">Bu hizmet, şu anda ARP önbelleğindeki tüm dinamik ARP girdilerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="36624-114">This service invalidates all dynamic ARP entries currently in the ARP cache.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-115">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-115">Parameters</span></span>

- <span data-ttu-id="36624-116">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-116">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-117">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-117">Return Values</span></span>

- <span data-ttu-id="36624-118">**NX_SUCCESS** (0x00) başarılı ARP önbelleği geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="36624-118">**NX_SUCCESS** (0x00) Successful ARP cache invalidate.</span></span>
- <span data-ttu-id="36624-119">**NX_NOT_ENABLED** (0x14) ARP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-119">**NX_NOT_ENABLED** (0x14) ARP is not enabled.</span></span>
- <span data-ttu-id="36624-120">**NX_PTR_ERROR** (0x07) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-120">**NX_PTR_ERROR** (0x07) Invalid IP address.</span></span>
- <span data-ttu-id="36624-121">**NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="36624-121">**NX_CALLER_ERROR** (0x11) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-122">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-122">Allowed From</span></span>

<span data-ttu-id="36624-123">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-123">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-124">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-124">Preemption Possible</span></span>

<span data-ttu-id="36624-125">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-125">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-126">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-126">Example</span></span>

```c
/* Invalidate all dynamic entries in the ARP cache. */
status = nx_arp_dynamic_entries_invalidate(&ip_0);
/* If status is NX_SUCCESS the dynamic ARP entries were successfully invalidated. */
```

### <a name="see-also"></a><span data-ttu-id="36624-127">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-127">See Also</span></span>

- <span data-ttu-id="36624-128">nx_arp_dynamic_entry_set, nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="36624-128">nx_arp_dynamic_entry_set, nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="36624-129">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-129">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="36624-130">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-130">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="36624-131">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-131">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_dynamic_entry_set"></a><span data-ttu-id="36624-132">nx_arp_dynamic_entry_set</span><span class="sxs-lookup"><span data-stu-id="36624-132">nx_arp_dynamic_entry_set</span></span>

<span data-ttu-id="36624-133">Dinamik ARP girdisi ayarla</span><span class="sxs-lookup"><span data-stu-id="36624-133">Set dynamic ARP entry</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-134">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-134">Prototype</span></span>

```C
UINT nx_arp_dynamic_entry_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a><span data-ttu-id="36624-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-135">Description</span></span>

<span data-ttu-id="36624-136">Bu hizmet ARP önbelleğinden dinamik bir giriş ayırır ve belirtilen IP 'yi fiziksel adres eşlemesi olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36624-136">This service allocates a dynamic entry from the ARP cache and sets up the specified IP to physical address mapping.</span></span> <span data-ttu-id="36624-137">Sıfır fiziksel adresi belirtilmişse, fiziksel adresin çözülebilmesi için ağa gerçek bir ARP isteği gönderilir.</span><span class="sxs-lookup"><span data-stu-id="36624-137">If a zero physical address is specified, an actual ARP request is sent to the network in order to have the physical address resolved.</span></span> <span data-ttu-id="36624-138">Ayrıca, ARP eskime etkin olduğunda veya ARP önbelleği tükenirse ve en son kullanılan ARP girişi ise bu girişin kaldırılacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-138">Also note that this entry will be removed if ARP aging is active or if the ARP cache is exhausted and this is the least recently used ARP entry.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-139">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-139">Parameters</span></span>

- <span data-ttu-id="36624-140">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-140">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-141">**ip_address** Eşlenecek IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-141">**ip_address** IP address to map.</span></span>
- <span data-ttu-id="36624-142">**physical_msw** Fiziksel adresin ilk 16 bit (47-32).</span><span class="sxs-lookup"><span data-stu-id="36624-142">**physical_msw** Top 16 bits (47-32) of the physical address.</span></span>
- <span data-ttu-id="36624-143">**physical_lsw** Fiziksel adresin düşük 32 bitleri (31-0).</span><span class="sxs-lookup"><span data-stu-id="36624-143">**physical_lsw** Lower 32 bits (31-0) of the physical address.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-144">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-144">Return Values</span></span>

- <span data-ttu-id="36624-145">**NX_SUCCESS** (0x00) başarılı ARP dinamik giriş kümesi.</span><span class="sxs-lookup"><span data-stu-id="36624-145">**NX_SUCCESS** (0x00) Successful ARP dynamic entry set.</span></span>
- <span data-ttu-id="36624-146">**NX_NO_MORE_ENTRIES** (0x17) ARP önbelleğinde daha fazla ARP girişi bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="36624-146">**NX_NO_MORE_ENTRIES** (0x17) No more ARP entries are available in the ARP cache.</span></span>
- <span data-ttu-id="36624-147">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-147">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="36624-148">**NX_PTR_ERROR** (0x07) geçersiz IP örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-148">**NX_PTR_ERROR** (0x07) Invalid IP instance pointer.</span></span>
- <span data-ttu-id="36624-149">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-149">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-150">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-150">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-151">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-151">Allowed From</span></span>

<span data-ttu-id="36624-152">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-152">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-153">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-153">Preemption Possible</span></span>

<span data-ttu-id="36624-154">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-154">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-155">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-155">Example</span></span>

```C
/* Setup a dynamic ARP entry on the previously created IP Instance 0. */
status = nx_arp_dynamic_entry_set(&ip_0, IP_ADDRESS(1,2,3,4),
    0x1022, 0x1234);
/* If status is NX_SUCCESS, there is now a dynamic mapping between
    the IP address of 1.2.3.4 and the physical hardware address of
    10:22:00:00:12:34. */
```

### <a name="see-also"></a><span data-ttu-id="36624-156">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-156">See Also</span></span>

- <span data-ttu-id="36624-157">nx_arp_dynamic_entries_invalidate, nx_arp_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-157">nx_arp_dynamic_entries_invalidate, nx_arp_enable,</span></span>
- <span data-ttu-id="36624-158">nx_arp_gratuitous_send, nx_arp_hardware_address_find,</span><span class="sxs-lookup"><span data-stu-id="36624-158">nx_arp_gratuitous_send, nx_arp_hardware_address_find,</span></span>
- <span data-ttu-id="36624-159">nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-159">nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="36624-160">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-160">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_enable"></a><span data-ttu-id="36624-161">nx_arp_enable</span><span class="sxs-lookup"><span data-stu-id="36624-161">nx_arp_enable</span></span>

<span data-ttu-id="36624-162">Adres Çözümleme Protokolü (ARP) etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="36624-162">Enables Address Resolution Protocol (ARP).</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-163">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-163">Prototype</span></span>

```C
UINT nx_arp_enable(
    NX_IP *ip_ptr, 
    VOID *arp_cache_memory, 
    ULONG arp_cache_size);
```

### <a name="description"></a><span data-ttu-id="36624-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-164">Description</span></span>

<span data-ttu-id="36624-165">Bu hizmet, belirli IP örneği için NetX ARP bileşenini başlatır.</span><span class="sxs-lookup"><span data-stu-id="36624-165">This service initializes the ARP component of NetX for the specific IP instance.</span></span> <span data-ttu-id="36624-166">ARP başlatma, ARP iletilerinin gönderilmesi ve alınması için gereken ARP önbelleğini ve çeşitli ARP işleme yordamlarını ayarlamayı içerir.</span><span class="sxs-lookup"><span data-stu-id="36624-166">ARP initialization includes setting up the ARP cache and various ARP processing routines necessary for sending and receiving ARP messages.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-167">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-167">Parameters</span></span>

- <span data-ttu-id="36624-168">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-168">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-169">**arp_cache_memory** ARP önbelleğinin yerleştirileceği bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-169">**arp_cache_memory** Pointer to memory area to place ARP cache.</span></span>
- <span data-ttu-id="36624-170">**arp_cache_size** Her ARP girişi 52 bayttır, ARP girişlerinin toplam sayısı, bu nedenle boyut 52 ' ye bölünür.</span><span class="sxs-lookup"><span data-stu-id="36624-170">**arp_cache_size** Each ARP entry is 52 bytes, the total number of ARP entries is, therefore, the size divided by 52.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-171">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-171">Return Values</span></span>

- <span data-ttu-id="36624-172">**NX_SUCCESS** (0x00) başarılı ARP etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-172">**NX_SUCCESS** (0x00) Successful ARP enable.</span></span>
- <span data-ttu-id="36624-173">**NX_PTR_ERROR** (0x07) geçersiz IP veya önbellek bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-173">**NX_PTR_ERROR** (0x07) Invalid IP or cache memory pointer.</span></span>
- <span data-ttu-id="36624-174">**NX_SIZE_ERROR** (0x09) Kullanıcı tarafından sağlanan ARP önbelleği belleği çok küçük.</span><span class="sxs-lookup"><span data-stu-id="36624-174">**NX_SIZE_ERROR** (0x09) User supplied ARP cache memory is too small.</span></span>
- <span data-ttu-id="36624-175">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-175">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-176">**NX_ALREADY_ENABLED** (0x15) Bu bileşen zaten etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="36624-176">**NX_ALREADY_ENABLED** (0x15) This component has already been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-177">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-177">Allowed From</span></span>

<span data-ttu-id="36624-178">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-178">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-179">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-179">Preemption Possible</span></span>

<span data-ttu-id="36624-180">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-180">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-181">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-181">Example</span></span>

```C
/* Enable ARP and supply 1024 bytes of ARP cache memory for
    previously created IP Instance ip_0. */
status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
/* If status is NX_SUCCESS, ARP was successfully enabled for this IP instance.*/
```

### <a name="see-also"></a><span data-ttu-id="36624-182">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-182">See Also</span></span>

- <span data-ttu-id="36624-183">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="36624-183">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="36624-184">nx_arp_gratuitous_send, nx_arp_hardware_address_find,</span><span class="sxs-lookup"><span data-stu-id="36624-184">nx_arp_gratuitous_send, nx_arp_hardware_address_find,</span></span>
- <span data-ttu-id="36624-185">nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-185">nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="36624-186">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-186">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_gratuitous_send"></a><span data-ttu-id="36624-187">nx_arp_gratuitous_send</span><span class="sxs-lookup"><span data-stu-id="36624-187">nx_arp_gratuitous_send</span></span>

<span data-ttu-id="36624-188">Gereksiz ARP isteği gönder</span><span class="sxs-lookup"><span data-stu-id="36624-188">Send gratuitous ARP request</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-189">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-189">Prototype</span></span>

```C
UINT nx_arp_gratuitous_send(
    NX_IP *ip_ptr,
    VOID (*response_handler) (NX_IP *ip_ptr, NX_PACKET *packet_ptr));
```

### <a name="description"></a><span data-ttu-id="36624-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-190">Description</span></span>

<span data-ttu-id="36624-191">Bu hizmet, arabirim IP adresi geçerli olduğu sürece gereksiz ARP isteklerini iletmek için tüm fiziksel arabirimlerin üzerinden geçer.</span><span class="sxs-lookup"><span data-stu-id="36624-191">This service goes through all the physical interfaces to transmit gratuitous ARP requests as long as the interface IP address is valid.</span></span> <span data-ttu-id="36624-192">Bir ARP yanıtı alındıktan sonra, sağlanan yanıt işleyicisi, gereksiz ARP için yanıtı işlemek üzere çağırılır.</span><span class="sxs-lookup"><span data-stu-id="36624-192">If an ARP response is subsequently received, the supplied response handler is called to process the response to the gratuitous ARP.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-193">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-193">Parameters</span></span>

- <span data-ttu-id="36624-194">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-194">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-195">**response_handler** Yanıt işleme işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-195">**response_handler** Pointer to response handling function.</span></span> <span data-ttu-id="36624-196">NX_NULL sağlanırsa, yanıtlar yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="36624-196">If NX_NULL is supplied, responses are ignored.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-197">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-197">Return Values</span></span>

- <span data-ttu-id="36624-198">**NX_SUCCESS** (0x00) başarılı gereksiz ARP gönderme.</span><span class="sxs-lookup"><span data-stu-id="36624-198">**NX_SUCCESS** (0x00) Successful gratuitous ARP send.</span></span>
- <span data-ttu-id="36624-199">**NX_NO_PACKET** (0x01) kullanılabilir paket yok.</span><span class="sxs-lookup"><span data-stu-id="36624-199">**NX_NO_PACKET** (0x01) No packet available.</span></span>
- <span data-ttu-id="36624-200">**NX_NOT_ENABLED** (0x14) ARP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-200">**NX_NOT_ENABLED** (0x14) ARP is not enabled.</span></span>
- <span data-ttu-id="36624-201">**NX_IP_ADDRESS_ERROR** (0x21) geçerli IP adresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-201">**NX_IP_ADDRESS_ERROR** (0x21) Current IP address is invalid.</span></span>
- <span data-ttu-id="36624-202">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-202">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-203">**NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı değil.</span><span class="sxs-lookup"><span data-stu-id="36624-203">**NX_CALLER_ERROR** (0x11) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-204">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-204">Allowed From</span></span>

<span data-ttu-id="36624-205">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-205">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-206">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-206">Preemption Possible</span></span>

<span data-ttu-id="36624-207">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-207">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-208">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-208">Example</span></span>

```C
/* Send gratuitous ARP without any response handler. */
status = nx_arp_gratuitous_send(&ip_0, NX_NULL);

/* If status is NX_SUCCESS the gratuitous ARP was successfully sent. */
```

### <a name="see-also"></a><span data-ttu-id="36624-209">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-209">See Also</span></span>

- <span data-ttu-id="36624-210">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="36624-210">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="36624-211">nx_arp_enable, nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-211">nx_arp_enable, nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="36624-212">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-212">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="36624-213">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-213">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_hardware_address_find"></a><span data-ttu-id="36624-214">nx_arp_hardware_address_find</span><span class="sxs-lookup"><span data-stu-id="36624-214">nx_arp_hardware_address_find</span></span>

<span data-ttu-id="36624-215">Bir IP adresi verilen fiziksel donanım adresini bulma</span><span class="sxs-lookup"><span data-stu-id="36624-215">Locate physical hardware address given an IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-216">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-216">Prototype</span></span>

```C
UINT nx_arp_hardware_address_find(
    NX_IP *ip_ptr,
    ULONG ip_address, 
    ULONG *physical_msw, 
    ULONG *physical_lsw);
```

### <a name="description"></a><span data-ttu-id="36624-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-217">Description</span></span>

<span data-ttu-id="36624-218">Bu hizmet, belirtilen IP adresiyle ilişkili ARP önbelleğinde fiziksel bir donanım adresi bulmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="36624-218">This service attempts to find a physical hardware address in the ARP cache that is associated with the supplied IP address.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-219">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-219">Parameters</span></span>

- <span data-ttu-id="36624-220">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-220">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-221">**ip_address** Aranacak IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-221">**ip_address** IP address to search for.</span></span>
- <span data-ttu-id="36624-222">**physical_msw** Fiziksel adresin ilk 16 bitini (47-32) döndürmek için değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-222">**physical_msw** Pointer to the variable for returning the top 16 bits (47-32) of the physical address.</span></span>
- <span data-ttu-id="36624-223">**physical_lsw** Fiziksel adresin alt 32 bitlerini (31-0) döndürmek için değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-223">**physical_lsw** Pointer to the variable for returning the lower 32 bits (31-0) of the physical address.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-224">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-224">Return Values</span></span>

- <span data-ttu-id="36624-225">**NX_SUCCESS** (0x00) başarılı ARP donanım adresi bul.</span><span class="sxs-lookup"><span data-stu-id="36624-225">**NX_SUCCESS** (0x00) Successful ARP hardware address find.</span></span>
- <span data-ttu-id="36624-226">**NX_ENTRY_NOT_FOUND** (0x16) eşleme ARP önbelleğinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="36624-226">**NX_ENTRY_NOT_FOUND** (0x16) Mapping was not found in the ARP cache.</span></span>
- <span data-ttu-id="36624-227">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-227">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="36624-228">**NX_PTR_ERROR** (0x07) geçersiz IP veya bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-228">**NX_PTR_ERROR** (0x07) Invalid IP or memory pointer.</span></span>
- <span data-ttu-id="36624-229">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-229">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-230">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-230">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-231">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-231">Allowed From</span></span>

<span data-ttu-id="36624-232">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-232">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-233">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-233">Preemption Possible</span></span>

<span data-ttu-id="36624-234">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-234">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-235">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-235">Example</span></span>

```C
/* Search for the hardware address associated with the IP address of
    1.2.3.4 in the ARP cache of the previously created IP
    Instance 0. */
status = nx_arp_hardware_address_find(
    &ip_0, 
    IP_ADDRESS(1,2,3,4),
    &physical_msw, 
    &physical_lsw);

/* If status is NX_SUCCESS, the variables physical_msw and
    physical_lsw contain the hardware address.*/
```

### <a name="see-also"></a><span data-ttu-id="36624-236">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-236">See Also</span></span>

- <span data-ttu-id="36624-237">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="36624-237">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="36624-238">nx_arp_enable, nx_arp_gratuitous_send, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-238">nx_arp_enable, nx_arp_gratuitous_send, nx_arp_info_get,</span></span>
- <span data-ttu-id="36624-239">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-239">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="36624-240">nx_arp_static_entry_create, nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-240">nx_arp_static_entry_create, nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_info_get"></a><span data-ttu-id="36624-241">nx_arp_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-241">nx_arp_info_get</span></span>

<span data-ttu-id="36624-242">ARP etkinlikleri hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="36624-242">Retrieve information about ARP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-243">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-243">Prototype</span></span>

```C
UINT nx_arp_info_get(
    NX_IP *ip_ptr,
    ULONG *arp_requests_sent,
    ULONG *arp_requests_received,
    ULONG *arp_responses_sent,
    ULONG *arp_responses_received,
    ULONG *arp_dynamic_entries,
    ULONG *arp_static_entries,
    ULONG *arp_aged_entries,
    ULONG *arp_invalid_messages);
```

### <a name="description"></a><span data-ttu-id="36624-244">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-244">Description</span></span>

<span data-ttu-id="36624-245">Bu hizmet, ilişkili IP örneği için ARP etkinlikleri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-245">This service retrieves information about ARP activities for the associated IP instance.</span></span>

<span data-ttu-id="36624-246">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-246">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-247">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-247">Parameters</span></span>

- <span data-ttu-id="36624-248">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-248">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-249">**arp_requests_sent** Bu IP örneğinden gönderilen toplam ARP isteği için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-249">**arp_requests_sent** Pointer to destination for the total ARP requests sent from this IP instance.</span></span>
- <span data-ttu-id="36624-250">**arp_requests_received** Ağdan alınan toplam ARP istekleri için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-250">**arp_requests_received** Pointer to destination for the total ARP requests received from the network.</span></span>
- <span data-ttu-id="36624-251">**arp_responses_sent** Bu IP örneğinden gönderilen toplam ARP yanıtlarının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-251">**arp_responses_sent** Pointer to destination for the total ARP responses sent from this IP instance.</span></span>
- <span data-ttu-id="36624-252">**arp_responses_received** Ağdan alınan toplam ARP yanıtlarının hedefe yönelik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-252">**arp_responses_received** Pointer to the destination for the total ARP responses received from the network.</span></span>
- <span data-ttu-id="36624-253">**arp_dynamic_entries** Geçerli dinamik ARP girişi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-253">**arp_dynamic_entries** Pointer to the destination for the current number of dynamic ARP entries.</span></span>
- <span data-ttu-id="36624-254">**arp_static_entries** Geçerli statik ARP girişi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-254">**arp_static_entries** Pointer to the destination for the current number of static ARP entries.</span></span>
- <span data-ttu-id="36624-255">**arp_aged_entries** Eski olan ve geçersiz duruma gelen toplam ARP girişi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-255">**arp_aged_entries** Pointer to the destination of the total number of ARP entries that have aged and became invalid.</span></span>
- <span data-ttu-id="36624-256">**arp_invalid_messages** Alınan toplam geçersiz ARP iletisi hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-256">**arp_invalid_messages** Pointer to the destination of the total invalid ARP messages received.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-257">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-257">Return Values</span></span>

- <span data-ttu-id="36624-258">**NX_SUCCESS** (0x00) başarılı ARP bilgisi alma.</span><span class="sxs-lookup"><span data-stu-id="36624-258">**NX_SUCCESS** (0x00) Successful ARP information retrieval.</span></span>
- <span data-ttu-id="36624-259">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-259">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-260">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-260">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-261">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-261">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-262">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-262">Allowed From</span></span>

<span data-ttu-id="36624-263">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-263">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-264">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-264">Preemption Possible</span></span>

<span data-ttu-id="36624-265">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-265">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-266">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-266">Example</span></span>

```C
/* Pickup ARP information for ip_0. */
status = nx_arp_info_get(
    &ip_0, 
    &arp_requests_sent,
    &arp_requests_received,
    &arp_responses_sent,
    &arp_responses_received,
    &arp_dynamic_entries,
    &arp_static_entries,
    &arp_aged_entries,
    &arp_invalid_messages);
/* If status is NX_SUCCESS, the ARP information has been stored in
    the supplied variables. */
```

### <a name="see-also"></a><span data-ttu-id="36624-267">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-267">See Also</span></span>

- <span data-ttu-id="36624-268">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="36624-268">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="36624-269">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="36624-269">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="36624-270">nx_arp_hardware_address_find, nx_arp_ip_address_find,</span><span class="sxs-lookup"><span data-stu-id="36624-270">nx_arp_hardware_address_find, nx_arp_ip_address_find,</span></span>
- <span data-ttu-id="36624-271">nx_arp_static_entries_delete, nx_arp_static_entry_create,</span><span class="sxs-lookup"><span data-stu-id="36624-271">nx_arp_static_entries_delete, nx_arp_static_entry_create,</span></span>
- <span data-ttu-id="36624-272">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-272">nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_ip_address_find"></a><span data-ttu-id="36624-273">nx_arp_ip_address_find</span><span class="sxs-lookup"><span data-stu-id="36624-273">nx_arp_ip_address_find</span></span>

<span data-ttu-id="36624-274">Fiziksel bir adres verilen IP adresini bulma</span><span class="sxs-lookup"><span data-stu-id="36624-274">Locate IP address given a physical address</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-275">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-275">Prototype</span></span>

```C
UINT nx_arp_ip_address_find(
    NX_IP *ip_ptr, 
    ULONG *ip_address,
    ULONG physical_msw, 
    ULONG physical_lsw);
```

### <a name="description"></a><span data-ttu-id="36624-276">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-276">Description</span></span>

<span data-ttu-id="36624-277">Bu hizmet, ARP önbelleğinde sağlanan fiziksel adresle ilişkili bir IP adresi bulmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="36624-277">This service attempts to find an IP address in the ARP cache that is associated with the supplied physical address.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-278">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-278">Parameters</span></span>

- <span data-ttu-id="36624-279">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-279">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-280">**ip_address** Eşlenen IP adresi işaretçisi, eşlenmiş bir değer bulundu.</span><span class="sxs-lookup"><span data-stu-id="36624-280">**ip_address** Pointer to return IP address, if one is found that has been mapped.</span></span>
- <span data-ttu-id="36624-281">**physical_msw** Aranacak fiziksel adresin ilk 16 bit (47-32).</span><span class="sxs-lookup"><span data-stu-id="36624-281">**physical_msw** Top 16 bits (47-32) of the physical address to search for.</span></span>
- <span data-ttu-id="36624-282">**physical_lsw** Aranacak fiziksel adresin düşük 32 bitleri (31-0).</span><span class="sxs-lookup"><span data-stu-id="36624-282">**physical_lsw** Lower 32 bits (31-0) of the physical address to search for.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-283">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-283">Return Values</span></span>

- <span data-ttu-id="36624-284">**NX_SUCCESS** (0x00) başarılı ARP IP adresi bulma</span><span class="sxs-lookup"><span data-stu-id="36624-284">**NX_SUCCESS** (0x00) Successful ARP IP address find</span></span>
- <span data-ttu-id="36624-285">**NX_ENTRY_NOT_FOUND** (0x16) eşleme ARP önbelleğinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="36624-285">**NX_ENTRY_NOT_FOUND** (0x16) Mapping was not found in the ARP cache.</span></span>
- <span data-ttu-id="36624-286">**NX_PTR_ERROR** (0x07) geçersiz IP veya bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-286">**NX_PTR_ERROR** (0x07) Invalid IP or memory pointer.</span></span>
- <span data-ttu-id="36624-287">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-287">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-288">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-288">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-289">**NX_INVALID_PARAMETERS** (0x4D) Physical_msw ve physical_lsw ikisi de 0 ' dır.</span><span class="sxs-lookup"><span data-stu-id="36624-289">**NX_INVALID_PARAMETERS** (0x4D) Physical_msw and physical_lsw are both 0.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-290">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-290">Allowed From</span></span>

<span data-ttu-id="36624-291">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-291">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-292">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-292">Preemption Possible</span></span>

<span data-ttu-id="36624-293">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-293">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-294">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-294">Example</span></span>

```C
/* Search for the IP address associated with the hardware address of
    0x0:0x01234 in the ARP cache of the previously created IP
    Instance ip_0. */
status = nx_arp_ip_address_find(&ip_0, &ip_address, 0x0, 0x1234);

/* If status is NX_SUCCESS, the variables ip_address contains the
    associated IP address.*/
```

### <a name="see-also"></a><span data-ttu-id="36624-295">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-295">See Also</span></span>

- <span data-ttu-id="36624-296">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="36624-296">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="36624-297">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="36624-297">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="36624-298">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-298">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="36624-299">nx_arp_static_entries_delete, nx_arp_static_entry_create,</span><span class="sxs-lookup"><span data-stu-id="36624-299">nx_arp_static_entries_delete,nx_arp_static_entry_create,</span></span>
- <span data-ttu-id="36624-300">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-300">nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_static_entries_delete"></a><span data-ttu-id="36624-301">nx_arp_static_entries_delete</span><span class="sxs-lookup"><span data-stu-id="36624-301">nx_arp_static_entries_delete</span></span>

<span data-ttu-id="36624-302">Tüm statik ARP girdilerini Sil</span><span class="sxs-lookup"><span data-stu-id="36624-302">Delete all static ARP entries</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-303">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-303">Prototype</span></span>

```C
UINT nx_arp_static_entries_delete(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-304">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-304">Description</span></span>

<span data-ttu-id="36624-305">Bu hizmet ARP önbelleğindeki tüm statik girişleri siler.</span><span class="sxs-lookup"><span data-stu-id="36624-305">This service deletes all static entries in the ARP cache.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-306">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-306">Parameters</span></span>

- <span data-ttu-id="36624-307">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-307">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-308">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-308">Return Values</span></span>

- <span data-ttu-id="36624-309">**NX_SUCCESS** (0x00) statik girdileri silinir.</span><span class="sxs-lookup"><span data-stu-id="36624-309">**NX_SUCCESS** (0x00) Static entries are deleted.</span></span>
- <span data-ttu-id="36624-310">**NX_PTR_ERROR** (0x07) geçersiz ip_ptr işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-310">**NX_PTR_ERROR** (0x07) Invalid ip_ptr pointer.</span></span>
- <span data-ttu-id="36624-311">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-311">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-312">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-312">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-313">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-313">Allowed From</span></span>

<span data-ttu-id="36624-314">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-314">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-315">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-315">Preemption Possible</span></span>

<span data-ttu-id="36624-316">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-316">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-317">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-317">Example</span></span>

```C
/* Delete all the static ARP entries for IP Instance 0, assuming
    "ip_0" is the NX_IP structure for IP Instance 0. */

status = nx_arp_static_entries_delete(&ip_0);

/* If status is NX_SUCCESS all static ARP entries in the ARP cache
have been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="36624-318">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-318">See Also</span></span>

- <span data-ttu-id="36624-319">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="36624-319">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="36624-320">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="36624-320">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="36624-321">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-321">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="36624-322">nx_arp_ip_address_find, nx_arp_static_entry_create,</span><span class="sxs-lookup"><span data-stu-id="36624-322">nx_arp_ip_address_find, nx_arp_static_entry_create,</span></span>
- <span data-ttu-id="36624-323">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-323">nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_static_entry_create"></a><span data-ttu-id="36624-324">nx_arp_static_entry_create</span><span class="sxs-lookup"><span data-stu-id="36624-324">nx_arp_static_entry_create</span></span>

<span data-ttu-id="36624-325">ARP önbelleğinde donanım eşlemeye statik IP oluşturma</span><span class="sxs-lookup"><span data-stu-id="36624-325">Create static IP to hardware mapping in ARP cache</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-326">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-326">Prototype</span></span>

```C
UINT nx_arp_static_entry_create(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a><span data-ttu-id="36624-327">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-327">Description</span></span>

<span data-ttu-id="36624-328">Bu hizmet, belirtilen IP örneği için ARP önbelleğinde statik bir IP-fiziksel adres eşlemesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="36624-328">This service creates a static IP-to-physical address mapping in the ARP cache for the specified IP instance.</span></span> <span data-ttu-id="36624-329">Statik ARP girdileri ARP düzenli güncelleştirmelerine tabi değildir.</span><span class="sxs-lookup"><span data-stu-id="36624-329">Static ARP entries are not subject to ARP periodic updates.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-330">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-330">Parameters</span></span>

- <span data-ttu-id="36624-331">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-331">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-332">**ip_address** Eşlenecek IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-332">**ip_address** IP address to map.</span></span>
- <span data-ttu-id="36624-333">**physical_msw** Eşlenecek fiziksel adresin ilk 16 bit (47-32).</span><span class="sxs-lookup"><span data-stu-id="36624-333">**physical_msw** Top 16 bits (47-32) of the physical address to map.</span></span>
- <span data-ttu-id="36624-334">**physical_lsw** Eşlenecek fiziksel adresin düşük 32 bitleri (31-0).</span><span class="sxs-lookup"><span data-stu-id="36624-334">**physical_lsw** Lower 32 bits (31-0) of the physical address to map.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-335">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-335">Return Values</span></span>

- <span data-ttu-id="36624-336">**NX_SUCCESS** (0x00) başarılı ARP statik girdisi oluştur.</span><span class="sxs-lookup"><span data-stu-id="36624-336">**NX_SUCCESS** (0x00) Successful ARP static entry create.</span></span>
- <span data-ttu-id="36624-337">**NX_NO_MORE_ENTRIES** (0x17) ARP önbelleğinde daha fazla ARP girişi bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="36624-337">**NX_NO_MORE_ENTRIES** (0x17) No more ARP entries are available in the ARP cache.</span></span>
- <span data-ttu-id="36624-338">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-338">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="36624-339">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-339">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-340">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-340">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-341">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-341">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-342">**NX_INVALID_PARAMETERS** (0x4D) Physical_msw ve physical_lsw ikisi de 0 ' dır.</span><span class="sxs-lookup"><span data-stu-id="36624-342">**NX_INVALID_PARAMETERS** (0x4D) Physical_msw and physical_lsw are both 0.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-343">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-343">Allowed From</span></span>

<span data-ttu-id="36624-344">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-344">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-345">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-345">Preemption Possible</span></span>

<span data-ttu-id="36624-346">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-346">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-347">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-347">Example</span></span>

```C
/* Create a static ARP entry on the previously created IP
    Instance 0. */

status = nx_arp_static_entry_create(&ip_0, IP_ADDRESS(1,2,3,4),
    0x0, 0x1234);

/* If status is NX_SUCCESS, there is now a static mapping between
    the IP address of 1.2.3.4 and the physical hardware address of
    00:00:00:00:12:34. */
```

### <a name="see-also"></a><span data-ttu-id="36624-348">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-348">See Also</span></span>

- <span data-ttu-id="36624-349">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="36624-349">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="36624-350">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="36624-350">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="36624-351">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-351">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="36624-352">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-352">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="36624-353">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-353">nx_arp_static_entry_delete</span></span>

## <a name="nx_arp_static_entry_delete"></a><span data-ttu-id="36624-354">nx_arp_static_entry_delete</span><span class="sxs-lookup"><span data-stu-id="36624-354">nx_arp_static_entry_delete</span></span>

<span data-ttu-id="36624-355">ARP önbelleğindeki statik IP 'yi donanım eşleştirmeye silme</span><span class="sxs-lookup"><span data-stu-id="36624-355">Delete static IP to hardware mapping in ARP cache</span></span>


### <a name="prototype"></a><span data-ttu-id="36624-356">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-356">Prototype</span></span>

```C
UINT nx_arp_static_entry_delete(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a><span data-ttu-id="36624-357">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-357">Description</span></span>

<span data-ttu-id="36624-358">Bu hizmet, belirtilen IP örneği için ARP önbelleğinde önceden oluşturulmuş bir statik IP-fiziksel adres eşlemeyi bulur ve siler.</span><span class="sxs-lookup"><span data-stu-id="36624-358">This service finds and deletes a previously created static IP-to-physical address mapping in the ARP cache for the specified IP instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-359">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-359">Parameters</span></span>

- <span data-ttu-id="36624-360">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-360">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-361">**ip_address** Statik olarak eşlenmiş IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-361">**ip_address** IP address that was mapped statically.</span></span>
- <span data-ttu-id="36624-362">**physical_msw** Statik olarak eşlenmiş fiziksel adresin ilk 16 bit (47-32).</span><span class="sxs-lookup"><span data-stu-id="36624-362">**physical_msw** Top 16 bits (47 - 32) of the physical address that was mapped statically.</span></span>
- <span data-ttu-id="36624-363">**physical_lsw** Statik olarak eşlenmiş fiziksel adresin düşük 32 bitleri (31-0).</span><span class="sxs-lookup"><span data-stu-id="36624-363">**physical_lsw** Lower 32 bits (31 - 0) of the physical address that was mapped statically.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-364">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-364">Return Values</span></span>

- <span data-ttu-id="36624-365">**NX_SUCCESS** (0x00) başarılı ARP statik girdisi silme.</span><span class="sxs-lookup"><span data-stu-id="36624-365">**NX_SUCCESS** (0x00) Successful ARP static entry delete.</span></span>
- <span data-ttu-id="36624-366">**NX_ENTRY_NOT_FOUND** (0x16) ARP ÖNBELLEĞINDE statik ARP girdisi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="36624-366">**NX_ENTRY_NOT_FOUND** (0x16) Static ARP entry was not found in the ARP cache.</span></span>
- <span data-ttu-id="36624-367">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-367">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-368">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-368">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-369">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-369">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-370">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-370">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="36624-371">**NX_INVALID_PARAMETERS** (0x4D) Physical_msw ve physical_lsw ikisi de 0 ' dır.</span><span class="sxs-lookup"><span data-stu-id="36624-371">**NX_INVALID_PARAMETERS** (0x4D) Physical_msw and physical_lsw are both 0.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-372">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-372">Allowed From</span></span>

<span data-ttu-id="36624-373">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-373">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-374">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-374">Preemption Possible</span></span>

<span data-ttu-id="36624-375">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-375">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-376">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-376">Example</span></span>

```C
/* Delete a static ARP entry on the previously created IP
    instance ip_0. */
status = nx_arp_static_entry_delete(&ip_0, IP_ADDRESS(1,2,3,4),
    0x0, 0x1234);
/* If status is NX_SUCCESS, the previously created static ARP entry
    was successfully deleted. */
```

### <a name="see-also"></a><span data-ttu-id="36624-377">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-377">See Also</span></span>

- <span data-ttu-id="36624-378">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span><span class="sxs-lookup"><span data-stu-id="36624-378">nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,</span></span>
- <span data-ttu-id="36624-379">nx_arp_enable, nx_arp_gratuitous_send,</span><span class="sxs-lookup"><span data-stu-id="36624-379">nx_arp_enable, nx_arp_gratuitous_send,</span></span>
- <span data-ttu-id="36624-380">nx_arp_hardware_address_find, nx_arp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-380">nx_arp_hardware_address_find, nx_arp_info_get,</span></span>
- <span data-ttu-id="36624-381">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-381">nx_arp_ip_address_find, nx_arp_static_entries_delete,</span></span>
- <span data-ttu-id="36624-382">nx_arp_static_entry_create</span><span class="sxs-lookup"><span data-stu-id="36624-382">nx_arp_static_entry_create</span></span>

## <a name="nx_icmp_enable"></a><span data-ttu-id="36624-383">nx_icmp_enable</span><span class="sxs-lookup"><span data-stu-id="36624-383">nx_icmp_enable</span></span>

<span data-ttu-id="36624-384">Internet Denetim Iletisi Protokolü 'Nü (ıCMP) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-384">Enable Internet Control Message Protocol (ICMP)</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-385">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-385">Prototype</span></span>

```C
UINT nx_icmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-386">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-386">Description</span></span>

<span data-ttu-id="36624-387">Bu hizmet, belirtilen IP örneği için ıCMP bileşenini sunar.</span><span class="sxs-lookup"><span data-stu-id="36624-387">This service enables the ICMP component for the specified IP instance.</span></span>
<span data-ttu-id="36624-388">ICMP bileşeni, Internet hata iletilerini ve ping isteklerini ve yanıtlarını işlemekten sorumludur.</span><span class="sxs-lookup"><span data-stu-id="36624-388">The ICMP component is responsible for handling Internet error messages and ping requests and replies.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-389">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-389">Parameters</span></span>

- <span data-ttu-id="36624-390">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-390">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-391">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-391">Return Values</span></span>

- <span data-ttu-id="36624-392">**NX_SUCCESS** (0x00) başarılı ICMP etkinleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="36624-392">**NX_SUCCESS** (0x00) Successful ICMP enable.</span></span>
- <span data-ttu-id="36624-393">**NX_ALREADY_ENABLED** (0x15) ICMP zaten etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-393">**NX_ALREADY_ENABLED** (0x15) ICMP is already enabled.</span></span>
- <span data-ttu-id="36624-394">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-394">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-395">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-395">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-396">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-396">Allowed From</span></span>

<span data-ttu-id="36624-397">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-397">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-398">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-398">Preemption Possible</span></span>

<span data-ttu-id="36624-399">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-399">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-400">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-400">Example</span></span>

```C
/* Enable ICMP on the previously created IP Instance ip_0. */
status = nx_icmp_enable(&ip_0);

/* If status is NX_SUCCESS, ICMP is enabled. */
```

### <a name="see-also"></a><span data-ttu-id="36624-401">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-401">See Also</span></span>

- <span data-ttu-id="36624-402">nx_icmp_info_get, nx_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="36624-402">nx_icmp_info_get, nx_icmp_ping</span></span>

## <a name="nx_icmp_info_get"></a><span data-ttu-id="36624-403">nx_icmp_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-403">nx_icmp_info_get</span></span>

<span data-ttu-id="36624-404">ICMP etkinlikleri hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="36624-404">Retrieve information about ICMP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-405">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-405">Prototype</span></span>

```C
UINT nx_icmp_info_get(
    NX_IP *ip_ptr,
    ULONG *pings_sent,
    ULONG *ping_timeouts,
    ULONG *ping_threads_suspended,
    ULONG *ping_responses_received,
    ULONG *icmp_checksum_errors,
    ULONG *icmp_unhandled_messages);
```

### <a name="description"></a><span data-ttu-id="36624-406">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-406">Description</span></span>

<span data-ttu-id="36624-407">Bu hizmet, belirtilen IP örneği için ıCMP etkinlikleri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-407">This service retrieves information about ICMP activities for the specified IP instance.</span></span>

<span data-ttu-id="36624-408">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-408">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-409">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-409">Parameters</span></span>

- <span data-ttu-id="36624-410">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-410">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-411">**pings_sent** Gönderilen toplam ping sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-411">**pings_sent** Pointer to destination for the total number of pings sent.</span></span>
- <span data-ttu-id="36624-412">**ping_timeouts** Toplam ping zaman aşımı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-412">**ping_timeouts** Pointer to destination for the total number of ping timeouts.</span></span>
- <span data-ttu-id="36624-413">**ping_threads_suspended** Ping isteklerinde askıya alınan toplam iş parçacığı sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-413">**ping_threads_suspended** Pointer to destination of the total number of threads suspended on ping requests.</span></span>
- <span data-ttu-id="36624-414">**ping_responses_received** Alınan toplam ping yanıtı sayısının hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-414">**ping_responses_received** Pointer to estination of the total number of ping responses received.</span></span>
- <span data-ttu-id="36624-415">**icmp_checksum_errors** Toplam ıCMP sağlama toplamı hatası sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-415">**icmp_checksum_errors** Pointer to destination of the total number of ICMP checksum errors.</span></span>
- <span data-ttu-id="36624-416">**icmp_unhandled_messages** İşlenmemiş ıCMP iletilerinin toplam sayısının hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-416">**icmp_unhandled_messages** Pointer to estination of the total number of un-handled ICMP messages.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-417">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-417">Return Values</span></span>

- <span data-ttu-id="36624-418">**NX_SUCCESS** (0x00) başarılı ICMP bilgisi alma.</span><span class="sxs-lookup"><span data-stu-id="36624-418">**NX_SUCCESS** (0x00) Successful ICMP information retrieval.</span></span>
- <span data-ttu-id="36624-419">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-419">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-420">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-420">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-421">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-421">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-422">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-422">Allowed From</span></span>

<span data-ttu-id="36624-423">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-423">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-424">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-424">Preemption Possible</span></span>

<span data-ttu-id="36624-425">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-425">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-426">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-426">Example</span></span>

```C
/* Retrieve ICMP information from previously created IP
    instance ip_0. */
status = nx_icmp_info_get(
    &ip_0, 
    &pings_sent, 
    &ping_timeouts,
    &ping_threads_suspended,
    &ping_responses_received,
    &icmp_checksum_errors,
    &icmp_unhandled_messages);

/* If status is NX_SUCCESS, ICMP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-427">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-427">See Also</span></span>

- <span data-ttu-id="36624-428">nx_icmp_enable, nx_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="36624-428">nx_icmp_enable, nx_icmp_ping</span></span>

## <a name="nx_icmp_ping"></a><span data-ttu-id="36624-429">nx_icmp_ping</span><span class="sxs-lookup"><span data-stu-id="36624-429">nx_icmp_ping</span></span>

<span data-ttu-id="36624-430">Belirtilen IP adresine ping isteği gönder</span><span class="sxs-lookup"><span data-stu-id="36624-430">Send ping request to specified IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-431">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-431">Prototype</span></span>

```C
UINT nx_icmp_ping(
    NX_IP *ip_ptr,
    ULONG ip_address,
    CHAR *data, ULONG data_size,
    NX_PACKET **response_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-432">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-432">Description</span></span>

<span data-ttu-id="36624-433">Bu hizmet, belirtilen IP adresine bir ping isteği gönderir ve bir ping yanıtı iletisi için belirtilen süre için bekler.</span><span class="sxs-lookup"><span data-stu-id="36624-433">This service sends a ping request to the specified IP address and waits for the specified amount of time for a ping response message.</span></span> <span data-ttu-id="36624-434">Yanıt alınmadığında bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-434">If no response is received, an error is returned.</span></span> <span data-ttu-id="36624-435">Aksi takdirde, tüm yanıt iletisi response_ptr tarafından işaret edilen değişkende döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-435">Otherwise, the entire response message is returned in the variable pointed to by response_ptr.</span></span>

<span data-ttu-id="36624-436">*NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur.*</span><span class="sxs-lookup"><span data-stu-id="36624-436">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet after it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-437">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-437">Parameters</span></span>

- <span data-ttu-id="36624-438">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-438">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-439">**ip_address** Ping yapılacak ana bilgisayar bayt sırasındaki IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-439">**ip_address** IP address, in host byte order, to ping.</span></span> <span data-ttu-id="36624-440">ping iletisi için veri alanına veri Işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-440">data Pointer to data area for ping message.</span></span>
- <span data-ttu-id="36624-441">**data_size** Ping verilerinde bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="36624-441">**data_size** Number of bytes in the ping data</span></span>
- <span data-ttu-id="36624-442">**response_ptr** İçindeki ping yanıt iletisini döndürecek paket işaretçisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-442">**response_ptr** Pointer to packet pointer to return the ping response message in.</span></span>
- <span data-ttu-id="36624-443">**wait_option** Bir ping yanıtı için ne kadar bekleneceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-443">**wait_option** Defines how long to wait for a ping response.</span></span> <span data-ttu-id="36624-444">bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-444">wait options are defined as follows:</span></span>

  - <span data-ttu-id="36624-445">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-445">NX_NO_WAIT (0x00000000)</span></span>
  - <span data-ttu-id="36624-446">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-446">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
  - <span data-ttu-id="36624-447">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-447">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-448">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-448">Return Values</span></span>

- <span data-ttu-id="36624-449">**NX_SUCCESS** (0x00) başarılı ping.</span><span class="sxs-lookup"><span data-stu-id="36624-449">**NX_SUCCESS** (0x00) Successful ping.</span></span> <span data-ttu-id="36624-450">Yanıt iletisi işaretçisi, response_ptr tarafından işaret edilen değişkene yerleştirildi.</span><span class="sxs-lookup"><span data-stu-id="36624-450">Response message pointer was placed in the variable pointed to by response_ptr.</span></span>
- <span data-ttu-id="36624-451">**NX_NO_PACKET** (0x01) bir ping isteği paketi ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="36624-451">**NX_NO_PACKET** (0x01) Unable to allocate a ping request packet.</span></span>
- <span data-ttu-id="36624-452">**NX_OVERFLOW** (0x03) belirtilen veri alanı, bu IP örneği için varsayılan paket boyutunu aşıyor.</span><span class="sxs-lookup"><span data-stu-id="36624-452">**NX_OVERFLOW** (0x03) Specified data area exceeds the default packet size for this IP instance.</span></span>
- <span data-ttu-id="36624-453">**NX_NO_RESPONSE** (0x29) istenen IP yanıt vermedi.</span><span class="sxs-lookup"><span data-stu-id="36624-453">**NX_NO_RESPONSE** (0x29) Requested IP did not respond.</span></span>
- <span data-ttu-id="36624-454">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-454">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-455">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-455">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="36624-456">**NX_PTR_ERROR** (0x07) geçersiz IP veya Yanıt işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-456">**NX_PTR_ERROR** (0x07) Invalid IP or response pointer.</span></span>
- <span data-ttu-id="36624-457">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-457">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-458">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-458">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-459">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-459">Allowed From</span></span>

<span data-ttu-id="36624-460">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-460">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-461">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-461">Preemption Possible</span></span>

<span data-ttu-id="36624-462">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-462">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-463">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-463">Example</span></span>

```C
/* Issue a ping to IP address 1.2.3.5 from the previously created IP
    Instance ip_0. */
status = nx_icmp_ping(&ip_0, IP_ADDRESS(1,2,3,5), "abcd", 4,
    &response_ptr, 10);

/* If status is NX_SUCCESS, a ping response was received from IP
    address 1.2.3.5 and the response packet is contained in the
    packet pointed to by response_ptr. It should have the same "abcd"
    four bytes of data. */
```

### <a name="see-also"></a><span data-ttu-id="36624-464">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-464">See Also</span></span>

- <span data-ttu-id="36624-465">nx_icmp_enable, nx_icmp_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-465">nx_icmp_enable, nx_icmp_info_get</span></span>

## <a name="nx_igmp_enable"></a><span data-ttu-id="36624-466">nx_igmp_enable</span><span class="sxs-lookup"><span data-stu-id="36624-466">nx_igmp_enable</span></span>

<span data-ttu-id="36624-467">Internet Grubu Yönetim Protokolü 'Nü (ıGMP) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-467">Enable Internet Group Management Protocol (IGMP)</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-468">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-468">Prototype</span></span>

```C
UINT nx_igmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-469">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-469">Description</span></span>

<span data-ttu-id="36624-470">Bu hizmet, belirtilen IP örneğindeki ıGMP bileşenini sunar.</span><span class="sxs-lookup"><span data-stu-id="36624-470">This service enables the IGMP component on the specified IP instance.</span></span>
<span data-ttu-id="36624-471">IGMP bileşeni, IP çok noktaya yayın grup yönetimi işlemlerine yönelik destek sağlamaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="36624-471">The IGMP component is responsible for providing support for IP multicast group management operations.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-472">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-472">Parameters</span></span>

- <span data-ttu-id="36624-473">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-473">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-474">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-474">Return Values</span></span>

- <span data-ttu-id="36624-475">**NX_SUCCESS** (0x00) başarıyla IGMP etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-475">**NX_SUCCESS** (0x00) Successful IGMP enable.</span></span>
- <span data-ttu-id="36624-476">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-476">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-477">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-477">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-478">**NX_ALREADY_ENABLED** (0x15) Bu bileşen zaten etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="36624-478">**NX_ALREADY_ENABLED** (0x15) This component has already been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-479">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-479">Allowed From</span></span>

<span data-ttu-id="36624-480">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-480">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-481">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-481">Preemption Possible</span></span>

<span data-ttu-id="36624-482">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-482">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-483">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-483">Example</span></span>

```C
/* Enable IGMP on the previously created IP Instance ip_0. */
status = nx_igmp_enable(&ip_0);

/* If status is NX_SUCCESS, IGMP is enabled. */
```

### <a name="see-also"></a><span data-ttu-id="36624-484">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-484">See Also</span></span>

- <span data-ttu-id="36624-485">nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-485">nx_igmp_info_get,nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="36624-486">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span><span class="sxs-lookup"><span data-stu-id="36624-486">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span></span>
- <span data-ttu-id="36624-487">nx_igmp_multicast_join, nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="36624-487">nx_igmp_multicast_join, nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_info_get"></a><span data-ttu-id="36624-488">nx_igmp_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-488">nx_igmp_info_get</span></span>

<span data-ttu-id="36624-489">IGMP etkinlikleri hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="36624-489">Retrieve information about IGMP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-490">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-490">Prototype</span></span>

```C
UINT nx_igmp_info_get(
    NX_IP *ip_ptr,
    ULONG *igmp_reports_sent,
    ULONG *igmp_queries_received,
    ULONG *igmp_checksum_errors,
    ULONG *current_groups_joined);
```

### <a name="description"></a><span data-ttu-id="36624-491">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-491">Description</span></span>

<span data-ttu-id="36624-492">Bu hizmet, belirtilen IP örneği için ıGMP etkinlikleri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-492">This service retrieves information about IGMP activities for the specified IP instance.</span></span>

<span data-ttu-id="36624-493">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-493">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-494">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-494">Parameters</span></span>

- <span data-ttu-id="36624-495">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-495">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-496">**igmp_reports_sent** Gönderilen toplam ıCMP raporu sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-496">**igmp_reports_sent** Pointer to destination for the total number of ICMP reports sent.</span></span>
- <span data-ttu-id="36624-497">**igmp_queries_received** Çok noktaya yayın yönlendiricisi tarafından alınan toplam sorgu sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-497">**igmp_queries_received** Pointer to destination for the total number of queries received by multicast router.</span></span>
- <span data-ttu-id="36624-498">**igmp_checksum_errors** Alma paketlerindeki toplam ıGMP sağlama toplamı hatalarının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-498">**igmp_checksum_errors** Pointer to destination of the total number of IGMP checksum errors on receive packets.</span></span>
- <span data-ttu-id="36624-499">**current_groups_joined** Bu IP örneğine katılmış geçerli grup sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-499">**current_groups_joined** Pointer to destination of the current number of groups joined through this IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-500">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-500">Return Values</span></span>

- <span data-ttu-id="36624-501">**NX_SUCCESS** (0x00) başarıyla IGMP bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="36624-501">**NX_SUCCESS** (0x00) Successful IGMP information retrieval.</span></span>
- <span data-ttu-id="36624-502">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-502">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-503">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-503">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-504">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-504">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-505">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-505">Allowed From</span></span>

<span data-ttu-id="36624-506">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-506">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-507">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-507">Preemption Possible</span></span>

<span data-ttu-id="36624-508">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-508">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-509">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-509">Example</span></span>

```C
/* Retrieve IGMP information
    from previously created IP Instance ip_0. */
status = nx_igmp_info_get(
    &ip_0, 
    &igmp_reports_sent,
    &igmp_queries_received,
    &igmp_checksum_errors,
    &current_groups_joined);
/* If status is NX_SUCCESS, IGMP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-510">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-510">See Also</span></span>

- <span data-ttu-id="36624-511">nx_igmp_enable, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-511">nx_igmp_enable, nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="36624-512">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span><span class="sxs-lookup"><span data-stu-id="36624-512">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span></span>
- <span data-ttu-id="36624-513">nx_igmp_multicast_join, nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="36624-513">nx_igmp_multicast_join, nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_loopback_disable"></a><span data-ttu-id="36624-514">nx_igmp_loopback_disable</span><span class="sxs-lookup"><span data-stu-id="36624-514">nx_igmp_loopback_disable</span></span>

<span data-ttu-id="36624-515">IGMP geri döngüsünü devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="36624-515">Disable IGMP loopback</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-516">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-516">Prototype</span></span>

```C
UINT nx_igmp_loopback_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-517">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-517">Description</span></span>

<span data-ttu-id="36624-518">Bu hizmet, sonraki tüm çok noktaya yayın gruplarına katılmış ıGMP geri döngüsünü devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="36624-518">This service disables IGMP loopback for all subsequent multicast groups joined.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-519">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-519">Parameters</span></span>

- <span data-ttu-id="36624-520">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-520">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-521">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-521">Return Values</span></span>
- <span data-ttu-id="36624-522">**NX_SUCCESS** (0x00) başarıyla IGMP geri döngü devre dışı.</span><span class="sxs-lookup"><span data-stu-id="36624-522">**NX_SUCCESS** (0x00) Successful IGMP loopback disable.</span></span>
- <span data-ttu-id="36624-523">**NX_NOT_ENABLED** (0x14) IGMP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-523">**NX_NOT_ENABLED** (0x14) IGMP is not enabled.</span></span>
- <span data-ttu-id="36624-524">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-524">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-525">**NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.</span><span class="sxs-lookup"><span data-stu-id="36624-525">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-526">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-526">Allowed From</span></span>

<span data-ttu-id="36624-527">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-527">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-528">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-528">Preemption Possible</span></span>

<span data-ttu-id="36624-529">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-529">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-530">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-530">Example</span></span>

```C
/* Disable IGMP loopback for all subsequent multicast groups joined. */
status = nx_igmp_loopback_disable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is disabled. */
```

### <a name="see-also"></a><span data-ttu-id="36624-531">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-531">See Also</span></span>

- <span data-ttu-id="36624-532">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-532">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_enable,</span></span>
- <span data-ttu-id="36624-533">nx_igmp_multicast_interface_join, nx_igmp_multicast_join,</span><span class="sxs-lookup"><span data-stu-id="36624-533">nx_igmp_multicast_interface_join, nx_igmp_multicast_join,</span></span>
- <span data-ttu-id="36624-534">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="36624-534">nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_loopback_enable"></a><span data-ttu-id="36624-535">nx_igmp_loopback_enable</span><span class="sxs-lookup"><span data-stu-id="36624-535">nx_igmp_loopback_enable</span></span>

<span data-ttu-id="36624-536">IGMP geri döngüsünü etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-536">Enable IGMP loopback</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-537">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-537">Prototype</span></span>

```C
UINT nx_igmp_loopback_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-538">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-538">Description</span></span>

<span data-ttu-id="36624-539">Bu hizmet, sonraki tüm çok noktaya yayın gruplarına katılmış ıGMP geri döngüsüne izin vermez.</span><span class="sxs-lookup"><span data-stu-id="36624-539">This service enables IGMP loopback for all subsequent multicast groups joined.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-540">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-540">Parameters</span></span>

- <span data-ttu-id="36624-541">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-541">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-542">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-542">Return Values</span></span>
- <span data-ttu-id="36624-543">**NX_SUCCESS** (0x00) başarıyla IGMP geri döngü devre dışı.</span><span class="sxs-lookup"><span data-stu-id="36624-543">**NX_SUCCESS** (0x00) Successful IGMP loopback disable.</span></span>
- <span data-ttu-id="36624-544">**NX_NOT_ENABLED** (0x14) IGMP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-544">**NX_NOT_ENABLED** (0x14) IGMP is not enabled.</span></span>
- <span data-ttu-id="36624-545">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-545">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-546">**NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.</span><span class="sxs-lookup"><span data-stu-id="36624-546">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-547">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-547">Allowed From</span></span>

<span data-ttu-id="36624-548">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-548">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-549">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-549">Preemption Possible</span></span>

<span data-ttu-id="36624-550">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-550">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-551">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-551">Example</span></span>

```C
/* Enable IGMP loopback for all subsequent multicast groups joined. */
status = nx_igmp_loopback_enable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is enabled. */
```

### <a name="see-also"></a><span data-ttu-id="36624-552">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-552">See Also</span></span>

- <span data-ttu-id="36624-553">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-553">nx_igmp_enable, nx_igmp_info_get,nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="36624-554">nx_igmp_multicast_interface_join, nx_igmp_multicast_join,</span><span class="sxs-lookup"><span data-stu-id="36624-554">nx_igmp_multicast_interface_join, nx_igmp_multicast_join,</span></span>
- <span data-ttu-id="36624-555">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="36624-555">nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_multicast_interface_join"></a><span data-ttu-id="36624-556">nx_igmp_multicast_interface_join</span><span class="sxs-lookup"><span data-stu-id="36624-556">nx_igmp_multicast_interface_join</span></span>

<span data-ttu-id="36624-557">IP örneğini bir arabirim aracılığıyla belirtilen çok noktaya yayın grubuna ekleyin</span><span class="sxs-lookup"><span data-stu-id="36624-557">Join IP instance to specified multicast group via an interface</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-558">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-558">Prototype</span></span>

```C
UINT nx_igmp_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="36624-559">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-559">Description</span></span>

<span data-ttu-id="36624-560">Bu hizmet, belirtilen ağ arabirimi aracılığıyla bir IP örneğini belirtilen çok noktaya yayın grubuna birleştirir.</span><span class="sxs-lookup"><span data-stu-id="36624-560">This service joins an IP instance to the specified multicast group via a specified network interface.</span></span> <span data-ttu-id="36624-561">Aynı grubun kaç kez katıldığını izlemek için bir iç sayaç tutulur.</span><span class="sxs-lookup"><span data-stu-id="36624-561">An internal counter is maintained to keep track of the number of times the same group has been joined.</span></span> <span data-ttu-id="36624-562">Çok noktaya yayın grubuna katıldıktan sonra, ıGMP bileşeni, belirtilen ağ arabirimi aracılığıyla bu grup adresiyle IP paketlerinin alımına ve ayrıca bu IP 'nin bu çok noktaya yayın grubunun bir üyesi olduğu yönlendiricilere rapor vermeyecektir.</span><span class="sxs-lookup"><span data-stu-id="36624-562">After joining the multicast group, the IGMP component will allow reception of IP packets with this group address via the specified network interface and also report to routers that this IP is a member of this multicast group.</span></span> <span data-ttu-id="36624-563">IGMP üyelik birleşimi, rapor ve çıkış iletileri belirtilen ağ arabirimi aracılığıyla da gönderilir.</span><span class="sxs-lookup"><span data-stu-id="36624-563">The IGMP membership join, report, and leave messages are also sent via the specified network interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-564">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-564">Parameters</span></span>

- <span data-ttu-id="36624-565">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-565">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-566">**group_address** Ana bilgisayar bayt düzeninde katılacak sınıf D IP çok noktaya yayın grubu adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-566">**group_address** Class D IP multicast group address to join in host byte order.</span></span>
- <span data-ttu-id="36624-567">**interface_index** NetX örneğine iliştirilmiş arabirimin dizini.</span><span class="sxs-lookup"><span data-stu-id="36624-567">**interface_index** Index of the Interface attached to the NetX instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-568">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-568">Return Values</span></span>

- <span data-ttu-id="36624-569">**NX_SUCCESS** (0x00) başarılı çok noktaya yayın grubu katılımı.</span><span class="sxs-lookup"><span data-stu-id="36624-569">**NX_SUCCESS** (0x00) Successful multicast group join.</span></span>
- <span data-ttu-id="36624-570">**NX_NO_MORE_ENTRIES** (0x17) daha fazla çok noktaya yayın grubu birleştirilemez, en fazla sınır aşıldı.</span><span class="sxs-lookup"><span data-stu-id="36624-570">**NX_NO_MORE_ENTRIES** (0x17) No more multicast groups can be joined, maximum exceeded.</span></span>
- <span data-ttu-id="36624-571">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-571">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-572">**NX_INVALID_INTERFACE** (0x4C) cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.</span><span class="sxs-lookup"><span data-stu-id="36624-572">**NX_INVALID_INTERFACE** (0x4C) Device index points to an invalid network interface.</span></span>
- <span data-ttu-id="36624-573">**NX_IP_ADDRESS_ERROR** (0x21) belirtilen çok noktaya yayın grubu adresi geçerli bir sınıf D adresi değil.</span><span class="sxs-lookup"><span data-stu-id="36624-573">**NX_IP_ADDRESS_ERROR** (0x21) Multicast group address provided is not a valid class D address.</span></span>
- <span data-ttu-id="36624-574">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-574">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-575">**NX_NOT_ENABLED** (0x14) IP çok noktaya yayın desteği etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-575">**NX_NOT_ENABLED** (0x14) IP multicast support is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-576">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-576">Allowed From</span></span>

<span data-ttu-id="36624-577">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-577">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-578">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-578">Preemption Possible</span></span>

<span data-ttu-id="36624-579">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-579">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-580">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-580">Example</span></span>

```C
/* Previously created IP Instance joins the multicast group
    244.0.0.200, via the interface at index 1 in the IP interface list. */
#define INTERFACE_INDEX 1
status = nx_igmp_multicast_interface_join
    (&ip, IP_ADDRESS(244,0,0,200),
    INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully joined
    the multicast group. */
```

### <a name="see-also"></a><span data-ttu-id="36624-581">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-581">See Also</span></span>

- <span data-ttu-id="36624-582">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-582">nx_igmp_enable, nx_igmp_info_get,nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="36624-583">nx_igmp_loopback_enable, nx_igmp_multicast_join,</span><span class="sxs-lookup"><span data-stu-id="36624-583">nx_igmp_loopback_enable, nx_igmp_multicast_join,</span></span>
- <span data-ttu-id="36624-584">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="36624-584">nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_multicast_join"></a><span data-ttu-id="36624-585">nx_igmp_multicast_join</span><span class="sxs-lookup"><span data-stu-id="36624-585">nx_igmp_multicast_join</span></span>

<span data-ttu-id="36624-586">IP örneğini belirtilen çok noktaya yayın grubuna ekleyin</span><span class="sxs-lookup"><span data-stu-id="36624-586">Join IP instance to specified multicast group</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-587">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-587">Prototype</span></span>

```C
UINT nx_igmp_multicast_join(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a><span data-ttu-id="36624-588">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-588">Description</span></span>

<span data-ttu-id="36624-589">Bu hizmet, bir IP örneğini belirtilen çok noktaya yayın grubuna birleştirir.</span><span class="sxs-lookup"><span data-stu-id="36624-589">This service joins an IP instance to the specified multicast group.</span></span> <span data-ttu-id="36624-590">Aynı grubun kaç kez katıldığını izlemek için bir iç sayaç tutulur.</span><span class="sxs-lookup"><span data-stu-id="36624-590">An internal counter is maintained to keep track of the number of times the same group has been joined.</span></span> <span data-ttu-id="36624-591">Bu, konağın gruba katılması için bir ağ üzerinde ilk JOIN isteği olduğunu belirten bir ıGMP raporu göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36624-591">The driver is commanded to send an IGMP report if this is the first join request out on the network indicating the host's intention to join the group.</span></span> <span data-ttu-id="36624-592">Birleştirme sonrasında, ıGMP bileşeni, bu IP 'nin bu çok noktaya yayın grubunun üyesi olduğu yönlendiricilerle bu grup adresi ve raporla IP paketleri alımına izin verir.</span><span class="sxs-lookup"><span data-stu-id="36624-592">After joining, the IGMP component will allow reception of IP packets with this group address and report to routers that this IP is a member of this multicast group.</span></span>

> [!NOTE]
> <span data-ttu-id="36624-593">*Birincil olmayan bir cihazdaki çok noktaya yayın grubuna katmak için, hizmet **nx_igmp_multicast_interface_join kullanın.***</span><span class="sxs-lookup"><span data-stu-id="36624-593">*To join a multicast group on a non-primary device, use the service **nx_igmp_multicast_interface_join.***</span></span>

- <span data-ttu-id="36624-594">**Parametreler**</span><span class="sxs-lookup"><span data-stu-id="36624-594">**Parameters**</span></span>

- <span data-ttu-id="36624-595">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-595">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-596">**group_address** Katılacak sınıf D IP çok noktaya yayın grubu adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-596">**group_address** Class D IP multicast group address to join.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-597">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-597">Return Values</span></span>

- <span data-ttu-id="36624-598">**NX_SUCCESS** (0x00) başarılı çok noktaya yayın grubu katılımı.</span><span class="sxs-lookup"><span data-stu-id="36624-598">**NX_SUCCESS** (0x00) Successful multicast group join.</span></span>
- <span data-ttu-id="36624-599">**NX_NO_MORE_ENTRIES** (0x17) daha fazla çok noktaya yayın grubu birleştirilemez, en fazla sınır aşıldı.</span><span class="sxs-lookup"><span data-stu-id="36624-599">**NX_NO_MORE_ENTRIES** (0x17) No more multicast groups can be joined, maximum exceeded.</span></span>
- <span data-ttu-id="36624-600">**NX_INVALID_INTERFACE** (0x4C) cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.</span><span class="sxs-lookup"><span data-stu-id="36624-600">**NX_INVALID_INTERFACE** (0x4C) Device index points to an invalid network interface.</span></span>
- <span data-ttu-id="36624-601">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP grubu adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-601">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP group address.</span></span>
- <span data-ttu-id="36624-602">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-602">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-603">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-603">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-604">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-604">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-605">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-605">Allowed From</span></span>

<span data-ttu-id="36624-606">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-606">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-607">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-607">Preemption Possible</span></span>

<span data-ttu-id="36624-608">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-608">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-609">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-609">Example</span></span>

```C
/* Previously created IP Instance ip_0 joins the multicast group
    224.0.0.200. */
status = nx_igmp_multicast_join(&ip_0, IP_ADDRESS(224,0,0,200));

/* If status is NX_SUCCESS, this IP instance has successfully
    joined the multicast group 224.0.0.200. */
```

### <a name="see-also"></a><span data-ttu-id="36624-610">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-610">See Also</span></span>

- <span data-ttu-id="36624-611">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-611">nx_igmp_enable, nx_igmp_info_get,nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="36624-612">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span><span class="sxs-lookup"><span data-stu-id="36624-612">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span></span>
- <span data-ttu-id="36624-613">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="36624-613">nx_igmp_multicast_leave</span></span>

## <a name="nx_igmp_multicast_leave"></a><span data-ttu-id="36624-614">nx_igmp_multicast_leave</span><span class="sxs-lookup"><span data-stu-id="36624-614">nx_igmp_multicast_leave</span></span>

<span data-ttu-id="36624-615">IP örneğinin belirtilen çok noktaya yayın grubuna ayrılma nedeni</span><span class="sxs-lookup"><span data-stu-id="36624-615">Cause IP instance to leave specified multicast group</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-616">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-616">Prototype</span></span>

```C
UINT nx_igmp_multicast_leave(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a><span data-ttu-id="36624-617">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-617">Description</span></span>

<span data-ttu-id="36624-618">Bu hizmet, çıkış isteklerinin sayısı, JOIN isteklerinin sayısı ile eşleşiyorsa bir IP örneğinin belirtilen çok noktaya yayın grubunu bırakmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="36624-618">This service causes an IP instance to leave the specified multicast group, if the number of leave requests matches the number of join requests.</span></span> <span data-ttu-id="36624-619">Aksi takdirde, iç ekleme sayısı yalnızca azaltılır.</span><span class="sxs-lookup"><span data-stu-id="36624-619">Otherwise, the internal join count is simply decremented.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-620">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-620">Parameters</span></span>

- <span data-ttu-id="36624-621">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-621">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-622">**group_address** Bırakılacak çok noktaya yayın grubu.</span><span class="sxs-lookup"><span data-stu-id="36624-622">**group_address** Multicast group to leave.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-623">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-623">Return Values</span></span>

- <span data-ttu-id="36624-624">**NX_SUCCESS** (0x00) başarılı çok noktaya yayın grubu katılımı.</span><span class="sxs-lookup"><span data-stu-id="36624-624">**NX_SUCCESS** (0x00) Successful multicast group join.</span></span>
- <span data-ttu-id="36624-625">**NX_ENTRY_NOT_FOUND** (0x16) önceki JOIN isteği bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="36624-625">**NX_ENTRY_NOT_FOUND** (0x16) Previous join request was not found.</span></span>
- <span data-ttu-id="36624-626">**NX_INVALID_INTERFACE** (0x4C) cihaz dizini geçersiz bir ağ arabirimine işaret ediyor.</span><span class="sxs-lookup"><span data-stu-id="36624-626">**NX_INVALID_INTERFACE** (0x4C) Device index points to an invalid network interface.</span></span>
- <span data-ttu-id="36624-627">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP grubu adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-627">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP group address.</span></span>
- <span data-ttu-id="36624-628">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-628">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-629">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-629">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-630">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-630">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-631">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-631">Allowed From</span></span>

<span data-ttu-id="36624-632">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-632">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-633">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-633">Preemption Possible</span></span>

<span data-ttu-id="36624-634">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-634">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-635">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-635">Example</span></span>

```C
/* Cause IP instance to leave the multicast group 224.0.0.200. */
status = nx_igmp_multicast_leave(&ip_0, IP_ADDRESS(224,0,0,200);

/* If status is NX_SUCCESS, this IP instance has successfully left
    the multicast group 224.0.0.200. */
```
### <a name="see-also"></a><span data-ttu-id="36624-636">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-636">See Also</span></span>

- <span data-ttu-id="36624-637">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-637">nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,</span></span>
- <span data-ttu-id="36624-638">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span><span class="sxs-lookup"><span data-stu-id="36624-638">nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,</span></span>
- <span data-ttu-id="36624-639">nx_igmp_multicast_join</span><span class="sxs-lookup"><span data-stu-id="36624-639">nx_igmp_multicast_join</span></span>

## <a name="nx_ip_address_change_notifiy"></a><span data-ttu-id="36624-640">nx_ip_address_change_notifiy</span><span class="sxs-lookup"><span data-stu-id="36624-640">nx_ip_address_change_notifiy</span></span>

<span data-ttu-id="36624-641">IP adresi değişirse uygulamayı bilgilendir</span><span class="sxs-lookup"><span data-stu-id="36624-641">Notify application if IP address changes</span></span>


### <a name="prototype"></a><span data-ttu-id="36624-642">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-642">Prototype</span></span>

```C
UINT nx_ip_address_change_notify(
    NX_IP *ip_ptr,
    VOID(*change_notify)(NX_IP *,VOID *),
    VOID *additional_info);
```

### <a name="description"></a><span data-ttu-id="36624-643">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-643">Description</span></span>

<span data-ttu-id="36624-644">Bu hizmet, IP adresi her değiştirildiğinde çağrılan bir uygulama bildirim işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="36624-644">This service registers an application notification function that is called whenever the IP address is changed.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-645">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-645">Parameters</span></span>

- <span data-ttu-id="36624-646">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-646">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-647">**change_notify** IP değişikliği bildirim işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-647">**change_notify** Pointer to IP change notification function.</span></span> <span data-ttu-id="36624-648">Bu parametre NX_NULL, IP adresi değişiklik bildirimi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-648">If this parameter is NX_NULL, IP address change notification is disabled.</span></span>
- <span data-ttu-id="36624-649">**additional_info** IP adresi değiştirildiğinde bildirim işlevine de sağlanan isteğe bağlı ek bilgilere yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-649">**additional_info** Pointer to optional additional information that is also supplied to the notification function when the IP address is changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-650">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-650">Return Values</span></span>

- <span data-ttu-id="36624-651">**NX_SUCCESS** (0x00) başarılı IP adresi değişikliği bildirimi.</span><span class="sxs-lookup"><span data-stu-id="36624-651">**NX_SUCCESS** (0x00) Successful IP address change notification.</span></span>
- <span data-ttu-id="36624-652">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-652">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-653">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-653">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-654">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-654">Allowed From</span></span>

<span data-ttu-id="36624-655">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-655">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-656">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-656">Preemption Possible</span></span>

<span data-ttu-id="36624-657">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-657">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-658">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-658">Example</span></span>

```C
/* Register the function "my_ip_changed" to be called whenever
the IP address is changed. */
status = nx_ip_address_change_notify(&ip_0, my_ip_changed, NX_NULL);

/* If status is NX_SUCCESS, the "my_ip_changed" function will be
    called whenever the IP address changes. */
```

### <a name="see-also"></a><span data-ttu-id="36624-659">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-659">See Also</span></span>

- <span data-ttu-id="36624-660">nx_ip_address_get, nx_ip_address_set, nx_ip_create, nx_ip_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-660">nx_ip_address_get, nx_ip_address_set, nx_ip_create, nx_ip_delete,</span></span>
- <span data-ttu-id="36624-661">nx_ip_driver_direct_command, nx_ip_driver_interface_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-661">nx_ip_driver_direct_command, nx_ip_driver_interface_direct_command,</span></span>
- <span data-ttu-id="36624-662">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-662">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span></span>
- <span data-ttu-id="36624-663">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-663">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="36624-664">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-664">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_address_get"></a><span data-ttu-id="36624-665">nx_ip_address_get</span><span class="sxs-lookup"><span data-stu-id="36624-665">nx_ip_address_get</span></span>

<span data-ttu-id="36624-666">IP adresi ve ağ maskesini al</span><span class="sxs-lookup"><span data-stu-id="36624-666">Retrieve IP address and network mask</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-667">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-667">Prototype</span></span>

```C
UINT nx_ip_address_get(
    NX_IP *ip_ptr,
    ULONG *ip_address,
    ULONG *network_mask);
```

### <a name="description"></a><span data-ttu-id="36624-668">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-668">Description</span></span>

<span data-ttu-id="36624-669">Bu hizmet, birincil ağ arabiriminin IP adresini ve alt ağ maskesini alır.</span><span class="sxs-lookup"><span data-stu-id="36624-669">This service retrieves IP address and its subnet mask of the primary network interface.</span></span>

<span data-ttu-id="36624-670">\* İkincil cihaz hakkında bilgi edinmek için hizmetini kullanın</span><span class="sxs-lookup"><span data-stu-id="36624-670">\*To obtain information of the secondary device, use the service</span></span>
- <span data-ttu-id="36624-671">**nx_ip_interface_address_get**. \*</span><span class="sxs-lookup"><span data-stu-id="36624-671">**nx_ip_interface_address_get**.\*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-672">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-672">Parameters</span></span>

- <span data-ttu-id="36624-673">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-673">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-674">**ip_address** IP adresi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-674">**ip_address** Pointer to destination for IP address.</span></span>
- <span data-ttu-id="36624-675">**network_mask** Ağ maskesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-675">**network_mask** Pointer to destination for network mask.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-676">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-676">Return Values</span></span>

- <span data-ttu-id="36624-677">**NX_SUCCESS** (0x00) başarılı IP adresi al.</span><span class="sxs-lookup"><span data-stu-id="36624-677">**NX_SUCCESS** (0x00) Successful IP address get.</span></span>
- <span data-ttu-id="36624-678">**NX_PTR_ERROR** (0x07) geçersiz IP veya dönüş değişkeni işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-678">**NX_PTR_ERROR** (0x07) Invalid IP or return variable pointer.</span></span>
- <span data-ttu-id="36624-679">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-679">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-680">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-680">Allowed From</span></span>

<span data-ttu-id="36624-681">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-681">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-682">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-682">Preemption Possible</span></span>

<span data-ttu-id="36624-683">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-683">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-684">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-684">Example</span></span>

```C
/* Get the IP address and network mask from the previously created
    IP Instance ip_0. */
status = nx_ip_address_get(&ip_0,
    &ip_address, &network_mask);

/* If status is NX_SUCCESS, the variables ip_address and
    network_mask contain the IP and network mask respectively. */
```

### <a name="see-also"></a><span data-ttu-id="36624-685">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-685">See Also</span></span>

- <span data-ttu-id="36624-686">nx_ip_address_change_notify, nx_ip_address_set, nx_ip_create,</span><span class="sxs-lookup"><span data-stu-id="36624-686">nx_ip_address_change_notify, nx_ip_address_set, nx_ip_create,</span></span>
- <span data-ttu-id="36624-687">nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-687">nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-688">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-688">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-689">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-689">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="36624-690">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span><span class="sxs-lookup"><span data-stu-id="36624-690">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span></span>
- <span data-ttu-id="36624-691">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-691">nx_system_initialize</span></span>

## <a name="nx_ip_address_set"></a><span data-ttu-id="36624-692">nx_ip_address_set</span><span class="sxs-lookup"><span data-stu-id="36624-692">nx_ip_address_set</span></span>

<span data-ttu-id="36624-693">IP adresi ve ağ maskesini ayarla</span><span class="sxs-lookup"><span data-stu-id="36624-693">Set IP address and network mask</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-694">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-694">Prototype</span></span>

```C
UINT nx_ip_address_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a><span data-ttu-id="36624-695">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-695">Description</span></span>

<span data-ttu-id="36624-696">Bu hizmet, birincil ağ arabirimi için IP adresi ve ağ maskesini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36624-696">This service sets IP address and network mask for the primary network interface.</span></span>

<span data-ttu-id="36624-697">*İkincil cihaz için IP adresi ve ağ maskesini ayarlamak için, hizmet **nx_ip_interface_address_set** kullanın.*</span><span class="sxs-lookup"><span data-stu-id="36624-697">*To set IP address and network mask for the secondary device, use the service **nx_ip_interface_address_set**.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-698">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-698">Parameters</span></span>

- <span data-ttu-id="36624-699">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-699">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-700">**ip_address** Yeni IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-700">**ip_address** New IP address.</span></span>
- <span data-ttu-id="36624-701">**network_mask** Yeni ağ maskesi.</span><span class="sxs-lookup"><span data-stu-id="36624-701">**network_mask** New network mask.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-702">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-702">Return Values</span></span>

- <span data-ttu-id="36624-703">**NX_SUCCESS** (0x00) başarılı IP adresi kümesi.</span><span class="sxs-lookup"><span data-stu-id="36624-703">**NX_SUCCESS** (0x00) Successful IP address set.</span></span>
- <span data-ttu-id="36624-704">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-704">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="36624-705">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-705">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-706">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-706">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-707">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-707">Allowed From</span></span>

<span data-ttu-id="36624-708">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-708">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-709">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-709">Preemption Possible</span></span>

<span data-ttu-id="36624-710">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-710">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-711">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-711">Example</span></span>

```C
/* Set the IP address and network mask to 1.2.3.4 and 0xFFFFFF00
    for the previously created IP Instance ip_0. */
status = nx_ip_address_set(&ip_0, IP_ADDRESS(1,2,3,4), 0xFFFFFF00UL);

/* If status is NX_SUCCESS, the IP instance now has an IP address
    of 1.2.3.4 and a network mask of 0xFFFFFF00. */
```

### <a name="see-also"></a><span data-ttu-id="36624-712">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-712">See Also</span></span>

- <span data-ttu-id="36624-713">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_create,</span><span class="sxs-lookup"><span data-stu-id="36624-713">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_create,</span></span>
- <span data-ttu-id="36624-714">nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-714">nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-715">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-715">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-716">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-716">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="36624-717">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span><span class="sxs-lookup"><span data-stu-id="36624-717">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span></span>
- <span data-ttu-id="36624-718">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-718">nx_system_initialize</span></span>

## <a name="nx_ip_create"></a><span data-ttu-id="36624-719">nx_ip_create</span><span class="sxs-lookup"><span data-stu-id="36624-719">nx_ip_create</span></span>

<span data-ttu-id="36624-720">IP örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="36624-720">Create an IP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-721">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-721">Prototype</span></span>

```C
UINT nx_ip_create(
    NX_IP *ip_ptr, 
    CHAR *name, 
    ULONG ip_address,
    ULONG network_mask, 
    NX_PACKET_POOL *default_pool,
    VOID (*ip_network_driver)(NX_IP_DRIVER *),
    VOID *memory_ptr, 
    ULONG memory_size,
    UINT priority);
```

### <a name="description"></a><span data-ttu-id="36624-722">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-722">Description</span></span>

<span data-ttu-id="36624-723">Bu hizmet, Kullanıcı tarafından sağlanan IP adresi ve ağ sürücüsüne sahip bir IP örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="36624-723">This service creates an IP instance with the user supplied IP address and network driver.</span></span> <span data-ttu-id="36624-724">Ayrıca, uygulamanın, iç paket ayırması için kullanacağı IP örneği için önceden oluşturulmuş bir paket havuzu sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36624-724">In addition, the application must supply a previously created packet pool for the IP instance to use for internal packet allocation.</span></span> <span data-ttu-id="36624-725">Sağlanan uygulama ağ sürücüsünün bu IP iş parçacığı yürütülene kadar çağrılmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-725">Note that the supplied application network driver is not called until this IP's thread executes.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-726">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-726">Parameters</span></span>

- <span data-ttu-id="36624-727">**ip_ptr** Yeni bir IP örneği oluşturmak için denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-727">**ip_ptr** Pointer to control block to create a new IP instance.</span></span>
- <span data-ttu-id="36624-728">**ad** Bu yeni IP örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="36624-728">**name** Name of this new IP instance.</span></span>
- <span data-ttu-id="36624-729">**ip_address** Bu yeni IP örneğinin IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-729">**ip_address** IP address for this new IP instance.</span></span>
- <span data-ttu-id="36624-730">**network_mask** Alt ağ ve süper netme kullanımları için IP adresinin ağ bölümünü maskelemek için maske.</span><span class="sxs-lookup"><span data-stu-id="36624-730">**network_mask** Mask to delineate the network portion of the IP address for sub-netting and super-netting uses.</span></span>
- <span data-ttu-id="36624-731">**default_pool** Daha önce oluşturulmuş NetX paket havuzunun denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-731">**default_pool** Pointer to control block of previously created NetX packet pool.</span></span>
- <span data-ttu-id="36624-732">**ip_network_driver** IP paketleri göndermek ve almak için kullanılan Kullanıcı tarafından sağlanan ağ sürücüsü.</span><span class="sxs-lookup"><span data-stu-id="36624-732">**ip_network_driver** User-supplied network driver used to send and receive IP packets.</span></span>
- <span data-ttu-id="36624-733">**memory_ptr** IP Yardımcısı iş parçacığının yığın alanı için bellek alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-733">**memory_ptr** Pointer to memory area for the IP helper thread’s stack area.</span></span>
- <span data-ttu-id="36624-734">**memory_size** IP Yardımcısı iş parçacığı yığınının bellek alanındaki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="36624-734">**memory_size** Number of bytes in the memory area for the IP helper thread’s stack.</span></span>
- <span data-ttu-id="36624-735">**Öncelik** IP Yardımcısı iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="36624-735">**priority** Priority of IP helper thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-736">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-736">Return Values</span></span>
- <span data-ttu-id="36624-737">**NX_SUCCESS** (0x00) başarılı IP örneği oluşturma.</span><span class="sxs-lookup"><span data-stu-id="36624-737">**NX_SUCCESS** (0x00) Successful IP instance creation.</span></span>
- <span data-ttu-id="36624-738">**NX_NOT_IMPLEMENTED** (0x4A) NETX kitaplığı yanlış yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="36624-738">**NX_NOT_IMPLEMENTED** (0x4A) NetX library is configured incorrectly.</span></span>
- <span data-ttu-id="36624-739">**NX_PTR_ERROR** (0x07) geçersiz IP, ağ sürücüsü işlev işaretçisi, paket havuzu veya bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-739">**NX_PTR_ERROR** (0x07) Invalid IP, network driver function pointer, packet pool, or memory pointer.</span></span>
- <span data-ttu-id="36624-740">**NX_SIZE_ERROR** (0x09) sağlanan yığın boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="36624-740">**NX_SIZE_ERROR** (0x09) The supplied stack size is too small.</span></span>
- <span data-ttu-id="36624-741">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-741">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-742">**NX_IP_ADDRESS_ERROR** (0x21) sağlanan IP adresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-742">**NX_IP_ADDRESS_ERROR** (0x21) The supplied IP address is invalid.</span></span>
- <span data-ttu-id="36624-743">**NX_OPTION_ERROR** (0x21) sağlanan IP iş parçacığı önceliği geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-743">**NX_OPTION_ERROR** (0x21) The supplied IP thread priority is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-744">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-744">Allowed From</span></span>

<span data-ttu-id="36624-745">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-745">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-746">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-746">Preemption Possible</span></span>

<span data-ttu-id="36624-747">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-747">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-748">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-748">Example</span></span>

```C
/* Create an IP instance with an IP address of 1.2.3.4 and a network
    mask of 0xFFFFFF00UL. The "ethernet_driver" specifies the entry
    point of the application specific network driver and the
    "stack_memory_ptr" specifies the start of a 1024 byte memory
    area that is used for this IP instance’s helper thread.  */
status = nx_ip_create(
    &ip_0, 
    "NetX IP Instance ip_0",
    IP_ADDRESS(1, 2, 3, 4),
    0xFFFFFF00UL, &pool_0, 
    ethernet_driver,
    stack_memory_ptr, 
    1024, 
    1);

/* If status is NX_SUCCESS, the IP instance has been created. */
```

### <a name="see-also"></a><span data-ttu-id="36624-749">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-749">See Also</span></span>

- <span data-ttu-id="36624-750">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-750">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-751">nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-751">nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-752">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-752">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-753">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-753">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="36624-754">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span><span class="sxs-lookup"><span data-stu-id="36624-754">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span></span>
- <span data-ttu-id="36624-755">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-755">nx_system_initialize</span></span>

## <a name="nx_ip_delete"></a><span data-ttu-id="36624-756">nx_ip_delete</span><span class="sxs-lookup"><span data-stu-id="36624-756">nx_ip_delete</span></span>

<span data-ttu-id="36624-757">Önceden oluşturulan IP örneğini Sil</span><span class="sxs-lookup"><span data-stu-id="36624-757">Delete previously created IP instance</span></span>


### <a name="prototype"></a><span data-ttu-id="36624-758">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-758">Prototype</span></span>

```C
UINT nx_ip_delete(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-759">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-759">Description</span></span>

<span data-ttu-id="36624-760">Bu hizmet, önceden oluşturulmuş bir IP örneğini siler ve IP örneğinin sahip olduğu tüm sistem kaynaklarını serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="36624-760">This service deletes a previously created IP instance and releases all of the system resources owned by the IP instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-761">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-761">Parameters</span></span>
- <span data-ttu-id="36624-762">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-762">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-763">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-763">Return Values</span></span>

- <span data-ttu-id="36624-764">**NX_SUCCESS** (0x00) başarılı IP silme işlemi.</span><span class="sxs-lookup"><span data-stu-id="36624-764">**NX_SUCCESS** (0x00) Successful IP deletion.</span></span>
- <span data-ttu-id="36624-765">**NX_SOCKETS_BOUND** (0x28) bu IP örneğine, bağımlı UDP veya TCP yuvaları hala sahip.</span><span class="sxs-lookup"><span data-stu-id="36624-765">**NX_SOCKETS_BOUND** (0x28) This IP instance still has UDP or TCP sockets bound to it.</span></span> <span data-ttu-id="36624-766">IP örneği silinmeden önce tüm yuvaların bağlantısı kesildi ve silinmemelidir.</span><span class="sxs-lookup"><span data-stu-id="36624-766">All sockets must be unbound and deleted prior to deleting the IP instance.</span></span>
- <span data-ttu-id="36624-767">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-767">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-768">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-768">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-769">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-769">Allowed From</span></span>

<span data-ttu-id="36624-770">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-770">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-771">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-771">Preemption Possible</span></span>

<span data-ttu-id="36624-772">Yes</span><span class="sxs-lookup"><span data-stu-id="36624-772">Yes</span></span>

### <a name="example"></a><span data-ttu-id="36624-773">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-773">Example</span></span>

```C
/* Delete a previously created IP instance. */
status = nx_ip_delete(&ip_0);

/* If status is NX_SUCCESS, the IP instance has been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="36624-774">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-774">See Also</span></span>

- <span data-ttu-id="36624-775">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-775">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-776">nx_ip_create, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-776">nx_ip_create, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-777">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-777">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-778">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-778">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="36624-779">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span><span class="sxs-lookup"><span data-stu-id="36624-779">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,</span></span>
- <span data-ttu-id="36624-780">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-780">nx_system_initialize</span></span>

## <a name="nx_ip_driver_direct_command"></a><span data-ttu-id="36624-781">nx_ip_driver_direct_command</span><span class="sxs-lookup"><span data-stu-id="36624-781">nx_ip_driver_direct_command</span></span>

<span data-ttu-id="36624-782">Ağ sürücüsüne komut verme</span><span class="sxs-lookup"><span data-stu-id="36624-782">Issue command to network driver</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-783">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-783">Prototype</span></span>

```C
UINT nx_ip_driver_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    ULONG *return_value_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-784">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-784">Description</span></span>

<span data-ttu-id="36624-785">Bu hizmet, uygulamanın ***nx_ip_create*** çağrısı sırasında belirtilen birincil ağ arabirimi sürücüsüne doğrudan bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="36624-785">This service provides a direct interface to the application's primary network interface driver specified during the ***nx_ip_create*** call.</span></span>

<span data-ttu-id="36624-786">Uygulamaya özgü komutlar, sayısal değerleri NX_LINK_USER_COMMAND daha büyük veya eşit bir değere göre kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-786">Application-specific commands can be used providing their numeric value is greater than or equal to NX_LINK_USER_COMMAND.</span></span>

<span data-ttu-id="36624-787">*İkincil cihaz için komut vermek üzere **nx_ip_driver_interface_direct_command** hizmetini kullanın.*</span><span class="sxs-lookup"><span data-stu-id="36624-787">*To issue command for the secondary device, use the **nx_ip_driver_interface_direct_command** service.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-788">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-788">Parameters</span></span>

- <span data-ttu-id="36624-789">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-789">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-790">**komut** Sayısal komut kodu.</span><span class="sxs-lookup"><span data-stu-id="36624-790">**command** Numeric command code.</span></span> <span data-ttu-id="36624-791">Standart komutlar aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-791">Standard commands are defined as follows:</span></span>

- <span data-ttu-id="36624-792">NX_LINK_GET_STATUS (10)</span><span class="sxs-lookup"><span data-stu-id="36624-792">NX_LINK_GET_STATUS (10)</span></span>
- <span data-ttu-id="36624-793">NX_LINK_GET_SPEED (11)</span><span class="sxs-lookup"><span data-stu-id="36624-793">NX_LINK_GET_SPEED (11)</span></span>
- <span data-ttu-id="36624-794">NX_LINK_GET_DUPLEX_TYPE (12)</span><span class="sxs-lookup"><span data-stu-id="36624-794">NX_LINK_GET_DUPLEX_TYPE (12)</span></span>
- <span data-ttu-id="36624-795">NX_LINK_GET_ERROR_COUNT (13)</span><span class="sxs-lookup"><span data-stu-id="36624-795">NX_LINK_GET_ERROR_COUNT (13)</span></span>
- <span data-ttu-id="36624-796">NX_LINK_GET_RX_COUNT (14)</span><span class="sxs-lookup"><span data-stu-id="36624-796">NX_LINK_GET_RX_COUNT (14)</span></span>
- <span data-ttu-id="36624-797">NX_LINK_GET_TX_COUNT (15)</span><span class="sxs-lookup"><span data-stu-id="36624-797">NX_LINK_GET_TX_COUNT (15)</span></span>
- <span data-ttu-id="36624-798">NX_LINK_GET_ALLOC_ERRORS (16)</span><span class="sxs-lookup"><span data-stu-id="36624-798">NX_LINK_GET_ALLOC_ERRORS (16)</span></span>
- <span data-ttu-id="36624-799">NX_LINK_USER_COMMAND (50)</span><span class="sxs-lookup"><span data-stu-id="36624-799">NX_LINK_USER_COMMAND (50)</span></span>

- <span data-ttu-id="36624-800">**return_value_ptr** Çağıran değişkenin dönüş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-800">**return_value_ptr** Pointer to return variable in the caller.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-801">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-801">Return Values</span></span>

- <span data-ttu-id="36624-802">**NX_SUCCESS** (0x00) ağ sürücüsü doğrudan komutu başarıyla açıldı.</span><span class="sxs-lookup"><span data-stu-id="36624-802">**NX_SUCCESS** (0x00) Successful network driver direct command.</span></span>
- <span data-ttu-id="36624-803">**NX_UNHANDLED_COMMAND** (0x44) işlenmemiş veya uygulanmayan ağ sürücüsü komutu.</span><span class="sxs-lookup"><span data-stu-id="36624-803">**NX_UNHANDLED_COMMAND** (0x44) Unhandled or unimplemented network driver command.</span></span>
- <span data-ttu-id="36624-804">**NX_PTR_ERROR** (0x07) geçersiz IP veya dönüş değeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-804">**NX_PTR_ERROR** (0x07) Invalid IP or return value pointer.</span></span>
- <span data-ttu-id="36624-805">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-805">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-806">**NX_INVALID_INTERFACE** (0x4C) geçersiz arabirim dizini.</span><span class="sxs-lookup"><span data-stu-id="36624-806">**NX_INVALID_INTERFACE** (0x4C) Invalid interface index.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-807">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-807">Allowed From</span></span>

<span data-ttu-id="36624-808">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-808">Threads</span></span>

- <span data-ttu-id="36624-809">**Önalım mümkün**</span><span class="sxs-lookup"><span data-stu-id="36624-809">**Preemption Possible**</span></span>

<span data-ttu-id="36624-810">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-810">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-811">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-811">Example</span></span>

```C
/* Make a direct call to the application-specific network driver
    for the previously created IP instance. For this example, the
    network driver is interrogated for the link status. */
status = nx_ip_driver_direct_command(
    &ip_0, NX_LINK_GET_STATUS,
    &link_status);

/* If status is NX_SUCCESS, the link_status variable contains a
    NX_TRUE or NX_FALSE value representing the status of the
    physical link. */
```

### <a name="see-also"></a><span data-ttu-id="36624-812">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-812">See Also</span></span>

- <span data-ttu-id="36624-813">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-813">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-814">nx_ip_create, nx_ip_delete, nx_ip_driver_interface_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-814">nx_ip_create, nx_ip_delete, nx_ip_driver_interface_direct_command,</span></span>
- <span data-ttu-id="36624-815">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-815">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span></span>
- <span data-ttu-id="36624-816">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-816">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="36624-817">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-817">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_driver_interface_direct_command"></a><span data-ttu-id="36624-818">nx_ip_driver_interface_direct_command</span><span class="sxs-lookup"><span data-stu-id="36624-818">nx_ip_driver_interface_direct_command</span></span>

<span data-ttu-id="36624-819">Ağ sürücüsüne komut verme</span><span class="sxs-lookup"><span data-stu-id="36624-819">Issue command to network driver</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-820">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-820">Prototype</span></span>

```C
UINT nx_ip_driver_interface_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    UINT interface_index,
    ULONG *return_value_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-821">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-821">Description</span></span>

<span data-ttu-id="36624-822">Bu hizmet, IP örneğindeki uygulamanın ağ aygıtı sürücüsüne doğrudan bir komut sağlar.</span><span class="sxs-lookup"><span data-stu-id="36624-822">This service provides a direct command to the application's network device driver in the IP instance.</span></span> <span data-ttu-id="36624-823">Uygulamaya özgü komutlar, sayısal değerleri *NX_LINK_USER_COMMAND* daha büyük veya eşit bir değere göre kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-823">Application-specific commands can be used providing their numeric value is greater than or equal to *NX_LINK_USER_COMMAND*.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-824">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-824">Parameters</span></span>

- <span data-ttu-id="36624-825">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-825">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-826">**komut** Sayısal komut kodu.</span><span class="sxs-lookup"><span data-stu-id="36624-826">**command** Numeric command code.</span></span> <span data-ttu-id="36624-827">Standart komutlar aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-827">Standard commands are defined as follows:</span></span>
- <span data-ttu-id="36624-828">NX_LINK_GET_STATUS (10)</span><span class="sxs-lookup"><span data-stu-id="36624-828">NX_LINK_GET_STATUS (10)</span></span>
- <span data-ttu-id="36624-829">NX_LINK_GET_SPEED (11)</span><span class="sxs-lookup"><span data-stu-id="36624-829">NX_LINK_GET_SPEED (11)</span></span>
- <span data-ttu-id="36624-830">NX_LINK_GET_DUPLEX_TYPE (12)</span><span class="sxs-lookup"><span data-stu-id="36624-830">NX_LINK_GET_DUPLEX_TYPE (12)</span></span>
- <span data-ttu-id="36624-831">NX_LINK_GET_ERROR_COUNT (13)</span><span class="sxs-lookup"><span data-stu-id="36624-831">NX_LINK_GET_ERROR_COUNT (13)</span></span>
- <span data-ttu-id="36624-832">NX_LINK_GET_RX_COUNT (14)</span><span class="sxs-lookup"><span data-stu-id="36624-832">NX_LINK_GET_RX_COUNT (14)</span></span>
- <span data-ttu-id="36624-833">NX_LINK_GET_TX_COUNT (15)</span><span class="sxs-lookup"><span data-stu-id="36624-833">NX_LINK_GET_TX_COUNT (15)</span></span>
- <span data-ttu-id="36624-834">NX_LINK_GET_ALLOC_ERRORS (16)</span><span class="sxs-lookup"><span data-stu-id="36624-834">NX_LINK_GET_ALLOC_ERRORS (16)</span></span>
- <span data-ttu-id="36624-835">NX_LINK_USER_COMMAND (50)</span><span class="sxs-lookup"><span data-stu-id="36624-835">NX_LINK_USER_COMMAND (50)</span></span>
- <span data-ttu-id="36624-836">**interface_index** Komutun gönderilmesi gereken ağ arabiriminin dizini.</span><span class="sxs-lookup"><span data-stu-id="36624-836">**interface_index** Index of the network interface the command should be sent to.</span></span>
- <span data-ttu-id="36624-837">**return_value_ptr** Çağıran değişkenin dönüş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-837">**return_value_ptr** Pointer to return variable in the caller.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-838">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-838">Return Values</span></span>
- <span data-ttu-id="36624-839">**NX_SUCCESS** (0x00) ağ sürücüsü doğrudan komutu başarıyla açıldı.</span><span class="sxs-lookup"><span data-stu-id="36624-839">**NX_SUCCESS** (0x00) Successful network driver direct command.</span></span>
- <span data-ttu-id="36624-840">**NX_UNHANDLED_COMMAND** (0x44) işlenmemiş veya uygulanmayan ağ sürücüsü komutu.</span><span class="sxs-lookup"><span data-stu-id="36624-840">**NX_UNHANDLED_COMMAND** (0x44) Unhandled or unimplemented network driver command.</span></span>
- <span data-ttu-id="36624-841">**NX_INVALID_INTERFACE** (0x4C) geçersiz arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="36624-841">**NX_INVALID_INTERFACE** (0x4C) Invalid interface index</span></span>
- <span data-ttu-id="36624-842">**NX_PTR_ERROR** (0x07) geçersiz IP veya dönüş değeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-842">**NX_PTR_ERROR** (0x07) Invalid IP or return value pointer.</span></span>
- <span data-ttu-id="36624-843">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-843">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-844">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-844">Allowed From</span></span>

<span data-ttu-id="36624-845">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-845">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-846">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-846">Preemption Possible</span></span>

<span data-ttu-id="36624-847">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-847">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-848">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-848">Example</span></span>

```C
/* Make a direct call to the application-specific network driver
    for the previously created IP instance. For this example, the
    network driver is interrogated for the link status. */

/* Set the interface index to the primary device. */
UINT interface_index = 0;
    status = nx_ip_driver_interface_direct_command(&ip_0,
    NX_LINK_GET_STATUS,
    interface_index,
    &link_status);
/* If status is NX_SUCCESS, the link_status variable contains a
    NX_TRUE or NX_FALSE value representing the status of the
    physical link. */
```

### <a name="see-also"></a><span data-ttu-id="36624-849">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-849">See Also</span></span>

- <span data-ttu-id="36624-850">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-850">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-851">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-851">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-852">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-852">nx_ip_forwarding_disable, nx_ip_forwarding_enable,</span></span>
- <span data-ttu-id="36624-853">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-853">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="36624-854">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-854">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_forwarding_disable"></a><span data-ttu-id="36624-855">nx_ip_forwarding_disable</span><span class="sxs-lookup"><span data-stu-id="36624-855">nx_ip_forwarding_disable</span></span>

<span data-ttu-id="36624-856">IP paket iletmeyi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="36624-856">Disable IP packet forwarding</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-857">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-857">Prototype</span></span>

```C
UINT nx_ip_forwarding_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-858">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-858">Description</span></span>

<span data-ttu-id="36624-859">Bu hizmet, IP paketlerinin NetX IP bileşeni içinde iletilmesini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="36624-859">This service disables forwarding IP packets inside the NetX IP component.</span></span> <span data-ttu-id="36624-860">Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-860">On creation of the IP task, this service is automatically disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-861">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-861">Parameters</span></span>

- <span data-ttu-id="36624-862">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-862">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-863">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-863">Return Values</span></span>

- <span data-ttu-id="36624-864">**NX_SUCCESS** (0x00) başarılı IP iletimi devre dışı.</span><span class="sxs-lookup"><span data-stu-id="36624-864">**NX_SUCCESS** (0x00) Successful IP forwarding disable.</span></span>
- <span data-ttu-id="36624-865">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-865">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-866">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-866">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-867">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-867">Allowed From</span></span>

<span data-ttu-id="36624-868">Başlatma, iş parçacıkları, zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="36624-868">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-869">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-869">Preemption Possible</span></span>

<span data-ttu-id="36624-870">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-870">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-871">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-871">Example</span></span>

```C
/* Disable IP forwarding on this IP instance. */
status = nx_ip_forwarding_disable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been disabled on the
    previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-872">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-872">See Also</span></span>

- <span data-ttu-id="36624-873">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-873">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-874">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-874">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-875">nx_ip_driver_interface_direct_command, nx_ip_forwarding_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-875">nx_ip_driver_interface_direct_command, nx_ip_forwarding_enable,</span></span>
- <span data-ttu-id="36624-876">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-876">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="36624-877">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-877">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_forwarding_enable"></a><span data-ttu-id="36624-878">nx_ip_forwarding_enable</span><span class="sxs-lookup"><span data-stu-id="36624-878">nx_ip_forwarding_enable</span></span>

<span data-ttu-id="36624-879">IP paket iletmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-879">Enable IP packet forwarding</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-880">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-880">Prototype</span></span>

```C
UINT nx_ip_forwarding_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-881">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-881">Description</span></span>

<span data-ttu-id="36624-882">Bu hizmet, IP paketlerinin NetX IP bileşeni içinde iletilmesine izin vermez.</span><span class="sxs-lookup"><span data-stu-id="36624-882">This service enables forwarding IP packets inside the NetX IP component.</span></span> <span data-ttu-id="36624-883">Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-883">On creation of the IP task, this service is automatically disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-884">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-884">Parameters</span></span>

- <span data-ttu-id="36624-885">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-885">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-886">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-886">Return Values</span></span>
- <span data-ttu-id="36624-887">**NX_SUCCESS** (0x00) başarılı IP iletimi etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-887">**NX_SUCCESS** (0x00) Successful IP forwarding enable.</span></span>
- <span data-ttu-id="36624-888">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-888">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-889">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-889">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-890">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-890">Allowed From</span></span>

<span data-ttu-id="36624-891">Başlatma, iş parçacıkları, zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="36624-891">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-892">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-892">Preemption Possible</span></span>

<span data-ttu-id="36624-893">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-893">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-894">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-894">Example</span></span>

```C
/* Enable IP forwarding on this IP instance. */
status = nx_ip_forwarding_enable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been enabled on the
    previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-895">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-895">See Also</span></span>

- <span data-ttu-id="36624-896">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-896">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-897">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-897">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-898">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-898">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-899">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-899">nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="36624-900">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-900">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_fragment_disable"></a><span data-ttu-id="36624-901">nx_ip_fragment_disable</span><span class="sxs-lookup"><span data-stu-id="36624-901">nx_ip_fragment_disable</span></span>

<span data-ttu-id="36624-902">IP paketi fragmenting devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="36624-902">Disable IP packet fragmenting</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-903">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-903">Prototype</span></span>

```C
UINT nx_ip_fragment_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-904">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-904">Description</span></span>

<span data-ttu-id="36624-905">Bu hizmet, IP paketi fragmenting devre dışı bırakır ve işlevselliği yeniden birleştirir.</span><span class="sxs-lookup"><span data-stu-id="36624-905">This service disables IP packet fragmenting and reassembling functionality.</span></span> <span data-ttu-id="36624-906">Yeniden birleştirilme bekleyen paketler için, bu hizmet bu paketleri yayınlar.</span><span class="sxs-lookup"><span data-stu-id="36624-906">For packets waiting to be reassembled, this service releases these packets.</span></span> <span data-ttu-id="36624-907">Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-907">On creation of the IP task, this service is automatically disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-908">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-908">Parameters</span></span>

- <span data-ttu-id="36624-909">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-909">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-910">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-910">Return Values</span></span>
- <span data-ttu-id="36624-911">**NX_SUCCESS** (0x00) başarılı IP parçası devre dışı.</span><span class="sxs-lookup"><span data-stu-id="36624-911">**NX_SUCCESS** (0x00) Successful IP fragment disable.</span></span>
- <span data-ttu-id="36624-912">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-912">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-913">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-913">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-914">**NX_NOT_ENABLED** (0x14) IP örneğinde IP parçalanması etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-914">**NX_NOT_ENABLED** (0x14) IP Fragmentation is not enabled on the IP instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-915">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-915">Allowed From</span></span>

<span data-ttu-id="36624-916">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-916">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-917">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-917">Preemption Possible</span></span>

<span data-ttu-id="36624-918">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-918">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-919">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-919">Example</span></span>

```C
/* Disable IP fragmenting on this IP instance. */
status = nx_ip_fragment_disable(&ip_0);

/* If status is NX_SUCCESS, disables IP fragmenting on the
    previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-920">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-920">See Also</span></span>

- <span data-ttu-id="36624-921">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-921">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-922">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-922">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-923">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-923">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-924">nx_ip_forwarding_enable, nx_ip_fragment_enable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-924">nx_ip_forwarding_enable, nx_ip_fragment_enable, nx_ip_info_get,</span></span>
- <span data-ttu-id="36624-925">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-925">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_fragment_enable"></a><span data-ttu-id="36624-926">nx_ip_fragment_enable</span><span class="sxs-lookup"><span data-stu-id="36624-926">nx_ip_fragment_enable</span></span>

<span data-ttu-id="36624-927">IP paketi fragmenting etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-927">Enable IP packet fragmenting</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-928">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-928">Prototype</span></span>

```C
UINT nx_ip_fragment_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-929">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-929">Description</span></span>

<span data-ttu-id="36624-930">Bu hizmet, IP paketi fragmenting ve yeniden birleştirilen işlevselliği sunar.</span><span class="sxs-lookup"><span data-stu-id="36624-930">This service enables IP packet fragmenting and reassembling functionality.</span></span> <span data-ttu-id="36624-931">Bu hizmet, IP görevini oluştururken otomatik olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-931">On creation of the IP task, this service is automatically disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-932">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-932">Parameters</span></span>

- <span data-ttu-id="36624-933">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-933">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-934">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-934">Return Values</span></span>

- <span data-ttu-id="36624-935">**NX_SUCCESS** (0x00) başarılı IP parçası etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="36624-935">**NX_SUCCESS** (0x00) Successful IP fragment enable.</span></span>
- <span data-ttu-id="36624-936">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-936">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-937">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-937">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-938">**NX_NOT_ENABLED** (0x14) IP parçalanma özellikleri NETX olarak derlenmedi.</span><span class="sxs-lookup"><span data-stu-id="36624-938">**NX_NOT_ENABLED** (0x14) IP Fragmentation features is not compiled into NetX.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-939">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-939">Allowed From</span></span>

<span data-ttu-id="36624-940">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-940">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-941">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-941">Preemption Possible</span></span>

<span data-ttu-id="36624-942">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-942">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-943">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-943">Example</span></span>

```C
/* Enable IP fragmenting on this IP instance. */
status = nx_ip_fragment_enable(&ip_0);

/* If status is NX_SUCCESS, IP fragmenting has been enabled on the
    previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-944">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-944">See Also</span></span>

- <span data-ttu-id="36624-945">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-945">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-946">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-946">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-947">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-947">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-948">nx_ip_forwarding_enable, nx_ip_fragment_disable, nx_ip_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-948">nx_ip_forwarding_enable, nx_ip_fragment_disable, nx_ip_info_get,</span></span>
- <span data-ttu-id="36624-949">nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-949">nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_gateway_address_set"></a><span data-ttu-id="36624-950">nx_ip_gateway_address_set</span><span class="sxs-lookup"><span data-stu-id="36624-950">nx_ip_gateway_address_set</span></span>

<span data-ttu-id="36624-951">Ağ geçidi IP adresi ayarla</span><span class="sxs-lookup"><span data-stu-id="36624-951">Set Gateway IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-952">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-952">Prototype</span></span>

```C
UINT nx_ip_gateway_address_set(
    NX_IP *ip_ptr, 
    ULONG ip_address);
```

### <a name="description"></a><span data-ttu-id="36624-953">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-953">Description</span></span>

<span data-ttu-id="36624-954">Bu hizmet, IP ağ geçidi IP adresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36624-954">This service sets the IP gateway IP address.</span></span> <span data-ttu-id="36624-955">Tüm ağ dışı trafik, iletim için bu ağ geçidine yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="36624-955">All out-of-network traffic are routed to this gateway for transmission.</span></span> <span data-ttu-id="36624-956">Ağ geçidine ağ arabirimlerinden biri aracılığıyla doğrudan erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36624-956">The gateway must be directly accessible through one of the network interfaces.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-957">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-957">Parameters</span></span>

- <span data-ttu-id="36624-958">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-958">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-959">**ip_address** Ağ geçidinin IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-959">**ip_address** IP address of the gateway.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-960">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-960">Return Values</span></span>

- <span data-ttu-id="36624-961">**NX_SUCCESS** (0x00) başarılı ağ geçidi IP adresi kümesi.</span><span class="sxs-lookup"><span data-stu-id="36624-961">**NX_SUCCESS** (0x00) Successful Gateway IP address set.</span></span>
- <span data-ttu-id="36624-962">**NX_PTR_ERROR** (0x07) geçersiz IP örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-962">**NX_PTR_ERROR** (0x07) Invalid IP instance pointer.</span></span>
- <span data-ttu-id="36624-963">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-963">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="36624-964">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-964">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-965">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-965">Allowed From</span></span>

<span data-ttu-id="36624-966">Başlatma, iş parçacığı</span><span class="sxs-lookup"><span data-stu-id="36624-966">Initialization, thread</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-967">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-967">Preemption Possible</span></span>

<span data-ttu-id="36624-968">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-968">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-969">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-969">Example</span></span>

```C
/* Setup the Gateway address for previously created IP
    Instance ip_0. */
status = nx_ip_gateway_address_set(&ip_0, IP_ADDRESS(1,2,3,99));

/* If status is NX_SUCCESS, all out-of-network send requests are
    routed to 1.2.3.99. */
```
### <a name="see-also"></a><span data-ttu-id="36624-970">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-970">See Also</span></span>

- <span data-ttu-id="36624-971">nx_ip_info_get, nx_ip_static_route_add, nx_ip_static_route_delete</span><span class="sxs-lookup"><span data-stu-id="36624-971">nx_ip_info_get, nx_ip_static_route_add, nx_ip_static_route_delete</span></span>

## <a name="nx_ip_info_get"></a><span data-ttu-id="36624-972">nx_ip_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-972">nx_ip_info_get</span></span>

<span data-ttu-id="36624-973">IP etkinlikleri hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="36624-973">Retrieve information about IP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-974">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-974">Prototype</span></span>

```C
UINT nx_ip_info_get(
    NX_IP *ip_ptr,
    ULONG *ip_total_packets_sent,
    ULONG *ip_total_bytes_sent,
    ULONG *ip_total_packets_received,
    ULONG *ip_total_bytes_received,
    ULONG *ip_invalid_packets,
    ULONG *ip_receive_packets_dropped,
    ULONG *ip_receive_checksum_errors,
    ULONG *ip_send_packets_dropped,
    ULONG *ip_total_fragments_sent,
    ULONG *ip_total_fragments_received);
```

### <a name="description"></a><span data-ttu-id="36624-975">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-975">Description</span></span>

<span data-ttu-id="36624-976">Bu hizmet, belirtilen IP örneği için IP etkinlikleri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-976">This service retrieves information about IP activities for the specified IP instance.</span></span>

<span data-ttu-id="36624-977">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-977">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-978">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-978">Parameters</span></span>

- <span data-ttu-id="36624-979">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-979">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-980">**ip_total_packets_sent** Gönderilen IP paketlerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-980">**ip_total_packets_sent** Pointer to destination for the total number of IP packets sent.</span></span>
- <span data-ttu-id="36624-981">**ip_total_bytes_sent** Gönderilen toplam bayt sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-981">**ip_total_bytes_sent** Pointer to destination for the total number of bytes sent.</span></span>
- <span data-ttu-id="36624-982">**ip_total_packets_received** IP alma paketlerinin toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-982">**ip_total_packets_received** Pointer to destination of the total number of IP receive packets.</span></span>
- <span data-ttu-id="36624-983">**ip_total_bytes_received** Alınan IP baytlarının toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-983">**ip_total_bytes_received** Pointer to destination of the total number of IP bytes received.</span></span>
- <span data-ttu-id="36624-984">**ip_invalid_packets** Toplam geçersiz IP paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-984">**ip_invalid_packets** Pointer to destination of the total number of invalid IP packets.</span></span>
- <span data-ttu-id="36624-985">**ip_receive_packets_dropped** Bırakılan toplam alım paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-985">**ip_receive_packets_dropped** Pointer to destination of the total number of receive packets dropped.</span></span>
- <span data-ttu-id="36624-986">**ip_receive_checksum_errors** Alma paketlerindeki toplam sağlama toplamı hatalarının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-986">**ip_receive_checksum_errors** Pointer to destination of the total number of checksum errors in receive packets.</span></span>
- <span data-ttu-id="36624-987">**ip_send_packets_dropped** Bırakılan Toplam gönderme paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-987">**ip_send_packets_dropped** Pointer to destination of the total number of send packets dropped.</span></span>
- <span data-ttu-id="36624-988">**ip_total_fragments_sent** Gönderilen toplam parçacık sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-988">**ip_total_fragments_sent** Pointer to destination of the total number of fragments sent.</span></span>
- <span data-ttu-id="36624-989">**ip_total_fragments_received** Toplam alınan parçacık sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-989">**ip_total_fragments_received** Pointer to destination of the total number of fragments received.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-990">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-990">Return Values</span></span>

- <span data-ttu-id="36624-991">**NX_SUCCESS** (0x00) başarılı IP bilgisi alma.</span><span class="sxs-lookup"><span data-stu-id="36624-991">**NX_SUCCESS** (0x00) Successful IP information retrieval.</span></span>
- <span data-ttu-id="36624-992">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-992">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-993">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-993">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-994">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-994">Allowed From</span></span>

<span data-ttu-id="36624-995">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-995">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-996">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-996">Preemption Possible</span></span>

<span data-ttu-id="36624-997">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-997">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-998">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-998">Example</span></span>

```C
/* Retrieve IP information from previously created IP
Instance 0. */
status = nx_ip_info_get(&ip_0,
    &ip_total_packets_sent,
    &ip_total_bytes_sent,
    &ip_total_packets_received,
    &ip_total_bytes_received,
    &ip_invalid_packets,
    &ip_receive_packets_dropped,
    &ip_receive_checksum_errors,
    &ip_send_packets_dropped,
    &ip_total_fragments_sent,
    &ip_total_fragments_received);

/* If status is NX_SUCCESS, IP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-999">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-999">See Also</span></span>

- <span data-ttu-id="36624-1000">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-1000">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-1001">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-1001">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-1002">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-1002">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-1003">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-1003">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="36624-1004">nx_ip_fragment_enable, nx_ip_status_check, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-1004">nx_ip_fragment_enable, nx_ip_status_check, nx_system_initialize</span></span>

## <a name="nx_ip_interface_address_get"></a><span data-ttu-id="36624-1005">nx_ip_interface_address_get</span><span class="sxs-lookup"><span data-stu-id="36624-1005">nx_ip_interface_address_get</span></span>

<span data-ttu-id="36624-1006">Arabirim IP adresini al</span><span class="sxs-lookup"><span data-stu-id="36624-1006">Retrieve interface IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1007">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1007">Prototype</span></span>

```C
UINT nx_ip_interface_address_get (
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *ip_address,
    ULONG *network_mask);
```

### <a name="description"></a><span data-ttu-id="36624-1008">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1008">Description</span></span>

<span data-ttu-id="36624-1009">Bu hizmet, belirtilen ağ arabiriminin IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="36624-1009">This service retrieves the IP address of a specified network interface.</span></span>

<span data-ttu-id="36624-1010">*Birincil cihaz değilse belirtilen cihaz, daha önce IP örneğine eklenmiş olmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="36624-1010">*The specified device, if not the primary device, must be previously attached to the IP instance.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1011">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1011">Parameters</span></span>

- <span data-ttu-id="36624-1012">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1012">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1013">**interface_index** Arabirim dizini, IP örneğine iliştirilmiş ağ arabiriminin diziniyle aynı değer.</span><span class="sxs-lookup"><span data-stu-id="36624-1013">**interface_index** Interface index, the same value as the index to the network interface attached to the IP instance.</span></span>
- <span data-ttu-id="36624-1014">**ip_address** Cihaz arabirimi IP adresi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1014">**ip_address** Pointer to destination for the device interface IP address.</span></span>
- <span data-ttu-id="36624-1015">**network_mask** Cihaz arabirimi ağ maskesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1015">**network_mask** Pointer to destination for the device interface network mask.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1016">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1016">Return Values</span></span>

- <span data-ttu-id="36624-1017">**NX_SUCCESS** (0x00) başarılı IP adresi al.</span><span class="sxs-lookup"><span data-stu-id="36624-1017">**NX_SUCCESS** (0x00) Successful IP address get.</span></span>
- <span data-ttu-id="36624-1018">**NX_INVALID_INTERFACE** (0x4C) belirtilen ağ arabirimi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-1018">**NX_INVALID_INTERFACE** (0x4C) Specified network interface is invalid.</span></span>
- <span data-ttu-id="36624-1019">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1019">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1020">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1020">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1021">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1021">Allowed From</span></span>

<span data-ttu-id="36624-1022">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1022">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1023">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1023">Preemption Possible</span></span>

<span data-ttu-id="36624-1024">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1024">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1025">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1025">Example</span></span>

```C
#define INTERFACE_INDEX 1
/* Get device IP address and network mask for the specified
    interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_get(ip_ptr,INTERFACE_INDEX,
    &ip_address, &network_mask);

/* If status is NX_SUCCESS the interface address was successfully
    retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1026">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1026">See Also</span></span>

- <span data-ttu-id="36624-1027">nx_ip_interface_address_set, nx_ip_interface_attach,</span><span class="sxs-lookup"><span data-stu-id="36624-1027">nx_ip_interface_address_set, nx_ip_interface_attach,</span></span>
- <span data-ttu-id="36624-1028">nx_ip_interface_info_get, nx_ip_interface_status_check,</span><span class="sxs-lookup"><span data-stu-id="36624-1028">nx_ip_interface_info_get, nx_ip_interface_status_check,</span></span>
- <span data-ttu-id="36624-1029">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-1029">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_interface_address_set"></a><span data-ttu-id="36624-1030">nx_ip_interface_address_set</span><span class="sxs-lookup"><span data-stu-id="36624-1030">nx_ip_interface_address_set</span></span>

<span data-ttu-id="36624-1031">Arabirim IP adresi ve ağ maskesini ayarla</span><span class="sxs-lookup"><span data-stu-id="36624-1031">Set interface IP address and network mask</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1032">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1032">Prototype</span></span>

```C
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a><span data-ttu-id="36624-1033">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1033">Description</span></span>

<span data-ttu-id="36624-1034">Bu hizmet, belirtilen IP arabirimi için IP adresini ve ağ maskesini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1034">This service sets the IP address and network mask for the specified IP interface.</span></span>

<span data-ttu-id="36624-1035">*Belirtilen arabirim daha önce IP örneğine eklenmiş olmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="36624-1035">*The specified interface must be previously attached to the IP instance.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1036">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1036">Parameters</span></span>

- <span data-ttu-id="36624-1037">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1037">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1038">**interface_index** NetX örneğine iliştirilmiş arabirimin dizini.</span><span class="sxs-lookup"><span data-stu-id="36624-1038">**interface_index** Index of the interface attached to the NetX instance.</span></span>
- <span data-ttu-id="36624-1039">**ip_address** Yeni ağ arabirimi IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-1039">**ip_address** New network interface IP address.</span></span>
- <span data-ttu-id="36624-1040">**network_mask** Yeni Arabirim ağ maskesi.</span><span class="sxs-lookup"><span data-stu-id="36624-1040">**network_mask** New interface network mask.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1041">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1041">Return Values</span></span>

- <span data-ttu-id="36624-1042">**NX_SUCCESS** (0x00) başarılı IP adresi kümesi.</span><span class="sxs-lookup"><span data-stu-id="36624-1042">**NX_SUCCESS** (0x00) Successful IP address set.</span></span>
- <span data-ttu-id="36624-1043">**NX_INVALID_INTERFACE** (0x4C) belirtilen ağ arabirimi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-1043">**NX_INVALID_INTERFACE** (0x4C) Specified network interface is invalid.</span></span>
- <span data-ttu-id="36624-1044">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1044">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1045">**NX_PTR_ERROR** (0x07) geçersiz işaretçiler.</span><span class="sxs-lookup"><span data-stu-id="36624-1045">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="36624-1046">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi</span><span class="sxs-lookup"><span data-stu-id="36624-1046">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1047">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1047">Allowed From</span></span>

<span data-ttu-id="36624-1048">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1048">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1049">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1049">Preemption Possible</span></span>

<span data-ttu-id="36624-1050">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1050">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1051">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1051">Example</span></span>

```C
#define INTERFACE_INDEX 1
/* Set device IP address and network mask for the specified
    interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_set(ip_ptr, INTERFACE_INDEX,
    ip_address, network_mask);

/* If status is NX_SUCCESS the interface IP address and mask was
successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1052">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1052">See Also</span></span>

- <span data-ttu-id="36624-1053">nx_ip_interface_address_get, nx_ip_interface_attach,</span><span class="sxs-lookup"><span data-stu-id="36624-1053">nx_ip_interface_address_get, nx_ip_interface_attach,</span></span>
- <span data-ttu-id="36624-1054">nx_ip_interface_info_get, nx_ip_interface_status_check,</span><span class="sxs-lookup"><span data-stu-id="36624-1054">nx_ip_interface_info_get, nx_ip_interface_status_check,</span></span>
- <span data-ttu-id="36624-1055">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-1055">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_interface_attach"></a><span data-ttu-id="36624-1056">nx_ip_interface_attach</span><span class="sxs-lookup"><span data-stu-id="36624-1056">nx_ip_interface_attach</span></span>

<span data-ttu-id="36624-1057">Ağ arabirimini IP örneğine Ekle</span><span class="sxs-lookup"><span data-stu-id="36624-1057">Attach network interface to IP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1058">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1058">Prototype</span></span>

```C
UINT nx_ip_interface_attach(
    NX_IP *ip_ptr, 
    CHAR *interface_name,
    ULONG ip_address,
    ULONG network_mask,
    VOID(*ip_link_driver)
    (struct NX_IP_DRIVER_STRUCT *));
```

### <a name="description"></a><span data-ttu-id="36624-1059">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1059">Description</span></span>

<span data-ttu-id="36624-1060">Bu hizmet, IP arabirimine bir fiziksel ağ arabirimi ekler.</span><span class="sxs-lookup"><span data-stu-id="36624-1060">This service adds a physical network interface to the IP interface.</span></span> <span data-ttu-id="36624-1061">Bu durumda, her ek arabirimin birincil arabirime ikincil olması için, IP örneğinin birincil arabirimle oluşturulduğunu aklınızda bulunur.</span><span class="sxs-lookup"><span data-stu-id="36624-1061">Note the IP instance is created with the primary interface so each additional interface is secondary to the primary interface.</span></span> <span data-ttu-id="36624-1062">IP örneğine (birincil arabirim dahil) bağlı olan ağ arabirimlerinin toplam sayısı **NX_MAX_PHYSICAL_INTERFACES** aşamaz.</span><span class="sxs-lookup"><span data-stu-id="36624-1062">The total number of network interfaces attached to the IP instance (including the primary interface) cannot exceed **NX_MAX_PHYSICAL_INTERFACES**.</span></span>

<span data-ttu-id="36624-1063">IP iş parçacığı henüz çalışmıyorsa, ikincil arabirimler tüm fiziksel arabirimleri Başlatan IP iş parçacığı başlatma sürecinin bir parçası olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="36624-1063">If the IP thread has not been running yet, the secondary interfaces will be initialized as part of the IP thread startup process that initializes all physical interfaces.</span></span>

<span data-ttu-id="36624-1064">IP iş parçacığı henüz çalışmıyorsa, ikincil arabirim ***nx_ip_interface_attach*** hizmetin bir parçası olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="36624-1064">If the IP thread is not running yet, the secondary interface is initialized as part of the ***nx_ip_interface_attach*** service.</span></span>

<span data-ttu-id="36624-1065">*ip_ptr geçerli bir NetX IP yapısına işaret etmelidir.*</span><span class="sxs-lookup"><span data-stu-id="36624-1065">*ip_ptr must point to a valid NetX IP structure.*</span></span>

- <span data-ttu-id="36624-1066">*IP örneği için ağ arabirimlerinin sayısı için **NX_MAX_PHYSICAL_INTERFACES** yapılandırılması gerekir. Varsayılan değer bir değeridir.*</span><span class="sxs-lookup"><span data-stu-id="36624-1066">***NX_MAX_PHYSICAL_INTERFACES** must be configured for the number of network interfaces for the IP instance. The default value is one.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1067">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1067">Parameters</span></span>

- <span data-ttu-id="36624-1068">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1068">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1069">**interface_name** Arabirim adı dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1069">**interface_name** Pointer to interface name string.</span></span>
- <span data-ttu-id="36624-1070">**ip_address** Konak bayt düzeninde cihaz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-1070">**ip_address** Device IP address in host byte order.</span></span>
- <span data-ttu-id="36624-1071">**network_mask** Konak bayt düzeninde cihaz ağ maskesi.</span><span class="sxs-lookup"><span data-stu-id="36624-1071">**network_mask** Device network mask in host byte order.</span></span>
- <span data-ttu-id="36624-1072">**ip_link_driver** Arabirim için Ethernet sürücüsü.</span><span class="sxs-lookup"><span data-stu-id="36624-1072">**ip_link_driver** Ethernet driver for the interface.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1073">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1073">Return Values</span></span>

- <span data-ttu-id="36624-1074">**NX_SUCCESS** (0x00) girişi statik yönlendirme tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="36624-1074">**NX_SUCCESS** (0x00) Entry is added to static routing table.</span></span>
- <span data-ttu-id="36624-1075">**NX_NO_MORE_ENTRIES** (0x17) en fazla arabirim sayısı.</span><span class="sxs-lookup"><span data-stu-id="36624-1075">**NX_NO_MORE_ENTRIES** (0x17) Max number of interfaces.</span></span>
- <span data-ttu-id="36624-1076">**NX_MAX_PHYSICAL_INTERFACES** aşıldı.</span><span class="sxs-lookup"><span data-stu-id="36624-1076">**NX_MAX_PHYSICAL_INTERFACES** is exceeded.</span></span>
- <span data-ttu-id="36624-1077">**NX_DUPLICATED_ENTRY** (0x52) sağlanan IP adresı bu IP örneğinde zaten kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="36624-1077">**NX_DUPLICATED_ENTRY** (0x52) The supplied IP address is already used on this IP instance.</span></span>
- <span data-ttu-id="36624-1078">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1078">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1079">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="36624-1079">**NX_PTR_ERROR** (0x07) Invalid pointer input.</span></span>
- <span data-ttu-id="36624-1080">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi girişi.</span><span class="sxs-lookup"><span data-stu-id="36624-1080">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1081">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1081">Allowed From</span></span>

<span data-ttu-id="36624-1082">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1082">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1083">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1083">Preemption Possible</span></span>

<span data-ttu-id="36624-1084">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1084">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1085">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1085">Example</span></span>

```C
/* Attach secondary device for device IP address 192.168.1.68 with
    the specified Ethernet driver. */
status = nx_ip_interface_attach(ip_ptr, “secondary_port”,
    IP_ADDRESS(192,168,1,68),
    0xFFFFFF00UL,
    nx_etherDriver);
/* If status is NX_SUCCESS the interface was successfully added to
    the IP instance interface table. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1086">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1086">See Also</span></span>

- <span data-ttu-id="36624-1087">nx_ip_interface_address_get, nx_ip_interface_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-1087">nx_ip_interface_address_get, nx_ip_interface_address_set,</span></span>
- <span data-ttu-id="36624-1088">nx_ip_interface_info_get, nx_ip_interface_status_check,</span><span class="sxs-lookup"><span data-stu-id="36624-1088">nx_ip_interface_info_get, nx_ip_interface_status_check,</span></span>
- <span data-ttu-id="36624-1089">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-1089">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_interface_info_get"></a><span data-ttu-id="36624-1090">nx_ip_interface_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-1090">nx_ip_interface_info_get</span></span>

<span data-ttu-id="36624-1091">Ağ arabirimi parametrelerini al</span><span class="sxs-lookup"><span data-stu-id="36624-1091">Retrieve network interface parameters</span></span>


### <a name="prototype"></a><span data-ttu-id="36624-1092">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1092">Prototype</span></span>

```C
UINT nx_ip_interface_info_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    CHAR **interface_name,
    ULONG *ip_address,
    ULONG *network_mask,
    ULONG *mtu_size,
    ULONG *physical_address_msw,
    ULONG *physical_address_lsw);
```

### <a name="description"></a><span data-ttu-id="36624-1093">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1093">Description</span></span>

<span data-ttu-id="36624-1094">Bu hizmet, belirtilen ağ arabirimi için ağ parametreleriyle ilgili bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="36624-1094">This service retrieves information on network parameters for the specified network interface.</span></span> <span data-ttu-id="36624-1095">Tüm veriler ana bilgisayar bayt düzeninde alınır.</span><span class="sxs-lookup"><span data-stu-id="36624-1095">All data are retrieved in host byte order.</span></span>

<span data-ttu-id="36624-1096">*ip_ptr geçerli bir NetX IP yapısına işaret etmelidir. Belirtilen arabirim, birincil arabirim değilse, daha önce IP örneğine eklenmelidir.*</span><span class="sxs-lookup"><span data-stu-id="36624-1096">*ip_ptr must point to a valid NetX IP structure. The specified interface, if not the primary interface, must be previously attached to the IP instance.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1097">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1097">Parameters</span></span>

- <span data-ttu-id="36624-1098">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1098">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1099">**interface_index** Ağ arabirimini belirten Dizin.</span><span class="sxs-lookup"><span data-stu-id="36624-1099">**interface_index** Index specifying network interface.</span></span>
- <span data-ttu-id="36624-1100">**interface_name** Ağ arabiriminin adını tutan arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1100">**interface_name** Pointer to the buffer that holds the name of the network interface.</span></span>
- <span data-ttu-id="36624-1101">**ip_address** Arabirimin IP adresi için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1101">**ip_address** Pointer to the destination for the IP address of the interface.</span></span>
- <span data-ttu-id="36624-1102">**network_mask** Ağ maskesi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1102">**network_mask** Pointer to destination for network mask.</span></span>
- <span data-ttu-id="36624-1103">**mtu_size** Bu arabirim için en fazla aktarım birimi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1103">**mtu_size** Pointer to destination for maximum transfer unit for this interface.</span></span>
- <span data-ttu-id="36624-1104">**physical_address_msw** Cihaz MAC adresi için en iyi 16 bit için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1104">**physical_address_msw** Pointer to destination for top 16 bits of the device MAC address.</span></span>
- <span data-ttu-id="36624-1105">**physical_address_lsw** Cihaz MAC adresinin daha düşük 32 bitleri için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1105">**physical_address_lsw** Pointer to destination for lower 32 bits of the device MAC address.</span></span>


### <a name="return-values"></a><span data-ttu-id="36624-1106">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1106">Return Values</span></span>
- <span data-ttu-id="36624-1107">**NX_SUCCESS** (0x00) arabirim bilgisi alındı.</span><span class="sxs-lookup"><span data-stu-id="36624-1107">**NX_SUCCESS** (0x00) Interface information has been obtained.</span></span>
- <span data-ttu-id="36624-1108">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="36624-1108">**NX_PTR_ERROR** (0x07) Invalid pointer input.</span></span>
- <span data-ttu-id="36624-1109">**NX_INVALID_INTERFACE** (0x4C) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1109">**NX_INVALID_INTERFACE** (0x4C) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-1110">**NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.</span><span class="sxs-lookup"><span data-stu-id="36624-1110">**NX_CALLER_ERROR** (0x11) Service is not called from system initialization or thread context.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1111">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1111">Allowed From</span></span>

<span data-ttu-id="36624-1112">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1112">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1113">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1113">Preemption Possible</span></span>

<span data-ttu-id="36624-1114">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1114">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1115">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1115">Example</span></span>

```C
/* Retrieve interface parameters for the specified interface (index
    1 in IP instance list of interfaces). */
#define INTERFACE_INDEX 1

status = nx_ip_interface_info_get(ip_ptr, INTERFACE_INDEX,
    &name_ptr, &ip_address,
    &network_mask,
    &mtu_size,
    &physical_address_msw,
    &physical_address_lsw);

/* If status is NX_SUCCESS the interface information is
    successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1116">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1116">See Also</span></span>

- <span data-ttu-id="36624-1117">nx_ip_interface_address_get, nx_ip_interface_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-1117">nx_ip_interface_address_get, nx_ip_interface_address_set,</span></span>
- <span data-ttu-id="36624-1118">nx_ip_interface_attach, nx_ip_interface_status_check,</span><span class="sxs-lookup"><span data-stu-id="36624-1118">nx_ip_interface_attach, nx_ip_interface_status_check,</span></span>
- <span data-ttu-id="36624-1119">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-1119">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_interface_status_check"></a><span data-ttu-id="36624-1120">nx_ip_interface_status_check</span><span class="sxs-lookup"><span data-stu-id="36624-1120">nx_ip_interface_status_check</span></span>

<span data-ttu-id="36624-1121">Bir IP örneğinin durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="36624-1121">Check status of an IP instance</span></span>


### <a name="prototype"></a><span data-ttu-id="36624-1122">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1122">Prototype</span></span>

```C
UINT nx_ip_interface_status_check(
    NX_IP *ip_ptr,
    UINT interface_index
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-1123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1123">Description</span></span>

<span data-ttu-id="36624-1124">Bu hizmet, daha önce oluşturulmuş bir IP örneğinin ağ arabiriminin belirtilen durumunu denetler ve isteğe bağlı olarak bekler.</span><span class="sxs-lookup"><span data-stu-id="36624-1124">This service checks and optionally waits for the specified status of the network interface of a previously created IP instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1125">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1125">Parameters</span></span>

- <span data-ttu-id="36624-1126">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1126">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1127">**interface_index** Arabirim dizin numarası</span><span class="sxs-lookup"><span data-stu-id="36624-1127">**interface_index** Interface index number</span></span>
- <span data-ttu-id="36624-1128">**needed_status** Aşağıdaki gibi bit eşleme biçiminde tanımlanan IP durumu istendi:</span><span class="sxs-lookup"><span data-stu-id="36624-1128">**needed_status** IP status requested, defined in bit-map form as follows:</span></span>
    - <span data-ttu-id="36624-1129">NX_IP_INITIALIZE_DONE (0x0001)</span><span class="sxs-lookup"><span data-stu-id="36624-1129">NX_IP_INITIALIZE_DONE (0x0001)</span></span>
    - <span data-ttu-id="36624-1130">NX_IP_ADDRESS_RESOLVED (0x0002)</span><span class="sxs-lookup"><span data-stu-id="36624-1130">NX_IP_ADDRESS_RESOLVED (0x0002)</span></span>
    - <span data-ttu-id="36624-1131">NX_IP_LINK_ENABLED (0x0004)</span><span class="sxs-lookup"><span data-stu-id="36624-1131">NX_IP_LINK_ENABLED (0x0004)</span></span>
    - <span data-ttu-id="36624-1132">NX_IP_ARP_ENABLED (0x0008)</span><span class="sxs-lookup"><span data-stu-id="36624-1132">NX_IP_ARP_ENABLED (0x0008)</span></span>
    - <span data-ttu-id="36624-1133">NX_IP_UDP_ENABLED (0x0010)</span><span class="sxs-lookup"><span data-stu-id="36624-1133">NX_IP_UDP_ENABLED (0x0010)</span></span>
    - <span data-ttu-id="36624-1134">NX_IP_TCP_ENABLED (0x0020)</span><span class="sxs-lookup"><span data-stu-id="36624-1134">NX_IP_TCP_ENABLED (0x0020)</span></span>
    - <span data-ttu-id="36624-1135">NX_IP_IGMP_ENABLED (0x0040)</span><span class="sxs-lookup"><span data-stu-id="36624-1135">NX_IP_IGMP_ENABLED (0x0040)</span></span>
    - <span data-ttu-id="36624-1136">NX_IP_RARP_COMPLETE (0x0080)</span><span class="sxs-lookup"><span data-stu-id="36624-1136">NX_IP_RARP_COMPLETE (0x0080)</span></span>
    - <span data-ttu-id="36624-1137">NX_IP_INTERFACE_LINK_ENABLED (0x0100)</span><span class="sxs-lookup"><span data-stu-id="36624-1137">NX_IP_INTERFACE_LINK_ENABLED (0x0100)</span></span>
- <span data-ttu-id="36624-1138">**actual_status** Gerçek bitler kümesinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1138">**actual_status** Pointer to destination of actual bits set.</span></span>
- <span data-ttu-id="36624-1139">**wait_option** İstenen durum bitleri yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1139">**wait_option** Defines how the service behaves if the requested status bits are not available.</span></span> <span data-ttu-id="36624-1140">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-1140">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="36624-1141">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-1141">NX_NO_WAIT (0x00000000)</span></span>
    - <span data-ttu-id="36624-1142">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-1142">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="36624-1143">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-1143">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1144">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1144">Return Values</span></span>

- <span data-ttu-id="36624-1145">**NX_SUCCESS** (0x00) başarılı IP durum denetimi.</span><span class="sxs-lookup"><span data-stu-id="36624-1145">**NX_SUCCESS** (0x00) Successful IP status check.</span></span>
- <span data-ttu-id="36624-1146">**NX_NOT_SUCCESSFUL** (0x43) durum isteği belirtilen zaman aşımı süresi içinde karşılanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-1146">**NX_NOT_SUCCESSFUL** (0x43) Status request was not satisfied within the timeout specified.</span></span>
- <span data-ttu-id="36624-1147">**NX_PTR_ERROR** (0x07) IP işaretçisi veya geçersiz hale geldi ya da gerçek durum işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-1147">**NX_PTR_ERROR** (0x07) IP pointer is or has become invalid, or actual status pointer is invalid.</span></span>
- <span data-ttu-id="36624-1148">**NX_OPTION_ERROR** (0X0a) geçersiz gerekli durum seçeneği.</span><span class="sxs-lookup"><span data-stu-id="36624-1148">**NX_OPTION_ERROR** (0x0a) Invalid needed status option.</span></span>
- <span data-ttu-id="36624-1149">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1149">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1150">**NX_INVALID_INTERFACE** (0x4C) Interface_index Aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="36624-1150">**NX_INVALID_INTERFACE** (0x4C) Interface_index is out of range.</span></span> <span data-ttu-id="36624-1151">ya da arabirim geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="36624-1151">or the interface is not valid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1152">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1152">Allowed From</span></span>

<span data-ttu-id="36624-1153">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1153">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1154">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1154">Preemption Possible</span></span>

<span data-ttu-id="36624-1155">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1155">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1156">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1156">Example</span></span>

```C
/* Wait 10 ticks for the link up status on the previously created IP
    instance. */
status = nx_ip_interface_status_check(&ip_0, 1, NX_IP_LINK_ENABLED,
    &actual_status, 10);

/* If status is NX_SUCCESS, the secondary link for the specified IP
    instance is up. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1157">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1157">See Also</span></span>

- <span data-ttu-id="36624-1158">nx_ip_interface_address_get, nx_ip_interface_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-1158">nx_ip_interface_address_get, nx_ip_interface_address_set,</span></span>
- <span data-ttu-id="36624-1159">nx_ip_interface_attach, nx_ip_interface_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-1159">nx_ip_interface_attach, nx_ip_interface_info_get,</span></span>
- <span data-ttu-id="36624-1160">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-1160">nx_ip_link_status_change_notify_set</span></span>

## <a name="nx_ip_link_status_change_notify_set"></a><span data-ttu-id="36624-1161">nx_ip_link_status_change_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-1161">nx_ip_link_status_change_notify_set</span></span>

<span data-ttu-id="36624-1162">Bağlantı durumu değiştirme bildirimi geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="36624-1162">Set the link status change notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1163">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1163">Prototype</span></span>

```C
UINT nx_ip_link_status_change_notify_set(
    NX_IP *ip_ptr,
    VOID (*link_status_change_notify)(NX_IP *ip_ptr, UINT interface_index, UINT link_up));
```

### <a name="description"></a><span data-ttu-id="36624-1164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1164">Description</span></span>

<span data-ttu-id="36624-1165">Bu hizmet bağlantı durumu değişikliği bildirim geri arama işlevini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="36624-1165">This service configures the link status change notify callback function.</span></span> <span data-ttu-id="36624-1166">Kullanıcı tarafından sağlanan *link_status_change_notify* yordamı, birincil veya ikincil arabirim durumu DEĞIŞTIRILDIĞINDE (IP adresi değiştirildiğinde) çağrılır. *LINK_STATUS_CHANGE_NOTIFY* null ise, bağlantı durumu değiştirme bildirimi geri arama özelliği devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-1166">The user-supplied *link_status_change_notify* routine is invoked when either the primary or secondary interface status is changed (such as IP address is changed.) If *link_status_change_notify* is NULL, the link status change notify callback feature is disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1167">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1167">Parameters</span></span>

- <span data-ttu-id="36624-1168">**ip_ptr** IP denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="36624-1168">**ip_ptr** IP control block pointer</span></span>
- <span data-ttu-id="36624-1169">**link_status_change_notify** Fiziksel arabirimde bir değişiklikten sonra çağrılacak Kullanıcı tarafından sağlanan geri arama işlevi.</span><span class="sxs-lookup"><span data-stu-id="36624-1169">**link_status_change_notify** User-supplied callback function to be called upon a change to the physical interface.</span></span>


### <a name="return-values"></a><span data-ttu-id="36624-1170">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1170">Return Values</span></span>

- <span data-ttu-id="36624-1171">**NX_SUCCESS** (0x00) başarılı küme</span><span class="sxs-lookup"><span data-stu-id="36624-1171">**NX_SUCCESS** (0x00) Successful set</span></span>
- <span data-ttu-id="36624-1172">**NX_PTR_ERROR** (0x07) geçersiz IP denetim bloğu işaretçisi veya yeni fiziksel adres işaretçisi</span><span class="sxs-lookup"><span data-stu-id="36624-1172">**NX_PTR_ERROR** (0x07) Invalid IP control block pointer or new physical address pointer</span></span>
- <span data-ttu-id="36624-1173">**NX_CALLER_ERROR** (0x11) hizmeti sistem başlatma veya iş parçacığı bağlamından çağrılmıyor.</span><span class="sxs-lookup"><span data-stu-id="36624-1173">**NX_CALLER_ERROR** (0x11) Service is not called from system initialization or thread context.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="36624-1174">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1174">Allowed From</span></span>

<span data-ttu-id="36624-1175">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1175">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1176">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1176">Preemption Possible</span></span>

<span data-ttu-id="36624-1177">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1177">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1178">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1178">Example</span></span>

```C
/* Configure a callback function to be used when the physical
    interface status is changed. */
status = nx_ip_link_status_change_notify_set(&ip_0, my_change_cb);

/* If status == NX_SUCCESS, the link status change notify function
    is set. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1179">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1179">See Also</span></span>

- <span data-ttu-id="36624-1180">nx_ip_interface_address_get, nx_ip_interface_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-1180">nx_ip_interface_address_get, nx_ip_interface_address_set,</span></span>
- <span data-ttu-id="36624-1181">nx_ip_interface_attach, nx_ip_interface_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-1181">nx_ip_interface_attach, nx_ip_interface_info_get,</span></span>
- <span data-ttu-id="36624-1182">nx_ip_interface_status_check</span><span class="sxs-lookup"><span data-stu-id="36624-1182">nx_ip_interface_status_check</span></span>

## <a name="nx_ip_raw_packet_disable"></a><span data-ttu-id="36624-1183">nx_ip_raw_packet_disable</span><span class="sxs-lookup"><span data-stu-id="36624-1183">nx_ip_raw_packet_disable</span></span>

<span data-ttu-id="36624-1184">Ham paket göndermeyi/almayı devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="36624-1184">Disable raw packet sending/receiving</span></span>


### <a name="prototype"></a><span data-ttu-id="36624-1185">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1185">Prototype</span></span>

```C
UINT nx_ip_raw_packet_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1186">Description</span></span>

<span data-ttu-id="36624-1187">Bu hizmet, bu IP örneği için ham IP paketlerinin aktarımını ve alımını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="36624-1187">This service disables transmission and reception of raw IP packets for this IP instance.</span></span> <span data-ttu-id="36624-1188">Ham paket hizmeti önceden etkinleştirildiyse ve alma kuyruğunda ham paketler varsa, bu hizmet alınan tüm ham paketleri serbest bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-1188">If the raw packet service was previously enabled, and there are raw packets in the receive queue, this service will release any received raw packets.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1189">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1189">Parameters</span></span>

- <span data-ttu-id="36624-1190">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1190">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1191">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1191">Return Values</span></span>

- <span data-ttu-id="36624-1192">**NX_SUCCESS** (0x00) başarılı IP ham paket devre dışı.</span><span class="sxs-lookup"><span data-stu-id="36624-1192">**NX_SUCCESS** (0x00) Successful IP raw packet disable.</span></span>
- <span data-ttu-id="36624-1193">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1193">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-1194">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1194">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1195">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1195">Allowed From</span></span>

<span data-ttu-id="36624-1196">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1196">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1197">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1197">Preemption Possible</span></span>

<span data-ttu-id="36624-1198">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1198">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1199">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1199">Example</span></span>

```C
/* Disable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_disable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
    been disabled for the previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1200">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1200">See Also</span></span>

- <span data-ttu-id="36624-1201">nx_ip_raw_packet_enable, nx_ip_raw_packet_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-1201">nx_ip_raw_packet_enable, nx_ip_raw_packet_receive,</span></span>
- <span data-ttu-id="36624-1202">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="36624-1202">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span></span>

## <a name="nx_ip_raw_packet_enable"></a><span data-ttu-id="36624-1203">nx_ip_raw_packet_enable</span><span class="sxs-lookup"><span data-stu-id="36624-1203">nx_ip_raw_packet_enable</span></span>

<span data-ttu-id="36624-1204">Ham paket işlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-1204">Enable raw packet processing</span></span>


### <a name="prototype"></a><span data-ttu-id="36624-1205">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1205">Prototype</span></span>

```C
UINT nx_ip_raw_packet_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1206">Description</span></span>

<span data-ttu-id="36624-1207">Bu hizmet, bu IP örneği için ham IP paketleri aktarımına ve alımına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="36624-1207">This service enables transmission and reception of raw IP packets for this IP instance.</span></span> <span data-ttu-id="36624-1208">Gelen TCP, UDP, ıCMP ve ıGMP paketleri hala NetX tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="36624-1208">Incoming TCP, UDP, ICMP, and IGMP packets are still processed by NetX.</span></span> <span data-ttu-id="36624-1209">Bilinmeyen üst katman protokol türlerine sahip paketler, ham paket alma yordamına göre işlenir.</span><span class="sxs-lookup"><span data-stu-id="36624-1209">Packets with unknown upper layer protocol types are processed by raw packet reception routine.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1210">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1210">Parameters</span></span>

- <span data-ttu-id="36624-1211">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1211">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1212">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1212">Return Values</span></span>

- <span data-ttu-id="36624-1213">**NX_SUCCESS** (0x00) başarılı IP ham paket etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-1213">**NX_SUCCESS** (0x00) Successful IP raw packet enable.</span></span>
- <span data-ttu-id="36624-1214">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1214">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-1215">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1215">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1216">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1216">Allowed From</span></span>

<span data-ttu-id="36624-1217">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1217">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1218">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1218">Preemption Possible</span></span>

<span data-ttu-id="36624-1219">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1219">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1220">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1220">Example</span></span>

```C
/* Enable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_enable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
    been enabled for the previously created IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1221">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1221">See Also</span></span>

- <span data-ttu-id="36624-1222">nx_ip_raw_packet_disable, nx_ip_raw_packet_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-1222">nx_ip_raw_packet_disable, nx_ip_raw_packet_receive,</span></span>
- <span data-ttu-id="36624-1223">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="36624-1223">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span></span>

## <a name="nx_ip_raw_packet_interface_send"></a><span data-ttu-id="36624-1224">nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="36624-1224">nx_ip_raw_packet_interface_send</span></span>

<span data-ttu-id="36624-1225">Belirtilen ağ arabirimi aracılığıyla ham IP paketi gönder</span><span class="sxs-lookup"><span data-stu-id="36624-1225">Send raw IP packet through specified network interface</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1226">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1226">Prototype</span></span>

```C
UINT nx_ip_raw_packet_interface_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    UINT address_index,
    ULONG type_of_service);
```

### <a name="description"></a><span data-ttu-id="36624-1227">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1227">Description</span></span>

<span data-ttu-id="36624-1228">Bu hizmet, kaynak adres olarak belirtilen yerel IP adresini ve ilişkili ağ arabirimini kullanarak hedef IP adresine bir ham IP paketi gönderir.</span><span class="sxs-lookup"><span data-stu-id="36624-1228">This service sends a raw IP packet to the destination IP address using the specified local IP address as the source address, and through the associated network interface.</span></span> <span data-ttu-id="36624-1229">Bu yordamın hemen geri döndüğüne ve bu nedenle, IP paketinin gerçekten gönderildiyse bilinmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-1229">Note that this routine returns immediately, and it is, therefore, not known if the IP packet has actually been sent.</span></span> <span data-ttu-id="36624-1230">Ağ sürücüsü, iletim tamamlandığında paketin serbest bırakılmasından sorumlu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="36624-1230">The network driver will be responsible for releasing the packet when the transmission is complete.</span></span> <span data-ttu-id="36624-1231">Bu hizmet, paketin gerçekten gönderilip gönderilmediğini bilmenin bir yolu olmadığından diğer hizmetlerden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-1231">This service differs from other services in that there is no way of knowing if the packet was actually sent.</span></span> <span data-ttu-id="36624-1232">Internet 'te kaybolabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-1232">It could get lost on the Internet.</span></span>

<span data-ttu-id="36624-1233">*Ham IP işlemenin etkin olması gerektiğini unutmayın.*</span><span class="sxs-lookup"><span data-stu-id="36624-1233">*Note that raw IP processing must be enabled.*</span></span>

<span data-ttu-id="36624-1234">*Bu hizmet **nx_ip_raw_packet_send** benzerdir, ancak bu hizmet, bir uygulamanın belirtilen fiziksel ARABIRIMLERDEN ham IP paketi göndermesini sağlar.*</span><span class="sxs-lookup"><span data-stu-id="36624-1234">*This service is similar to **nx_ip_raw_packet_send**, except that this service allows an application to send raw IP packet from a specified physical interfaces.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1235">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1235">Parameters</span></span>

- <span data-ttu-id="36624-1236">**ip_ptr** Daha önce oluşturulan IP görevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1236">**ip_ptr** Pointer to previously created IP task.</span></span>
- <span data-ttu-id="36624-1237">**packet_ptr** İletilecek paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1237">**packet_ptr** Pointer to packet to transmit.</span></span>
- <span data-ttu-id="36624-1238">**destination_ip** Paketin gönderileceği IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-1238">**destination_ip** IP address to send packet.</span></span>
- <span data-ttu-id="36624-1239">**address_index** Paketin dışına gönderilmesi için arabirim adresinin dizini.</span><span class="sxs-lookup"><span data-stu-id="36624-1239">**address_index** Index of the address of the interface to send packet out on.</span></span>
- <span data-ttu-id="36624-1240">**Type_of_service** Paket için hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="36624-1240">**type_of_service** Type of service for packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1241">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1241">Return Values</span></span>

- <span data-ttu-id="36624-1242">**NX_SUCCESS** (0x00) paketi başarıyla iletildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1242">**NX_SUCCESS** (0x00) Packet successfully transmitted.</span></span>
- <span data-ttu-id="36624-1243">**NX_IP_ADDRESS_ERROR** (0x21) uygun bir giden arabirim yok.</span><span class="sxs-lookup"><span data-stu-id="36624-1243">**NX_IP_ADDRESS_ERROR** (0x21) No suitable outgoing interface available.</span></span>
- <span data-ttu-id="36624-1244">**NX_NOT_ENABLED** (0x14) ham IP paket işleme etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-1244">**NX_NOT_ENABLED** (0x14) Raw IP packet processing not enabled.</span></span>
- <span data-ttu-id="36624-1245">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1245">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1246">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="36624-1246">**NX_PTR_ERROR** (0x07) Invalid pointer input.</span></span>
- <span data-ttu-id="36624-1247">**NX_OPTION_ERROR** (0X0a) geçersiz hizmet türü belirtildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1247">**NX_OPTION_ERROR** (0x0A) Invalid type of service specified.</span></span>
- <span data-ttu-id="36624-1248">**NX_OVERFLOW** (0x03) geçersiz paket önüne işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1248">**NX_OVERFLOW** (0x03) Invalid packet prepend pointer.</span></span>
- <span data-ttu-id="36624-1249">**NX_UNDERFLOW** (0x02) geçersiz paket önüne işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1249">**NX_UNDERFLOW** (0x02) Invalid packet prepend pointer.</span></span>
- <span data-ttu-id="36624-1250">**NX_INVALID_INTERFACE** (0x4C) geçersiz arabirim dizini belirtildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1250">**NX_INVALID_INTERFACE** (0x4C) Invalid interface index specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1251">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1251">Allowed From</span></span>

<span data-ttu-id="36624-1252">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1252">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1253">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1253">Preemption Possible</span></span>

<span data-ttu-id="36624-1254">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1254">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1255">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1255">Example</span></span>

```C
#define ADDRESS_IDNEX 1
/* Send packet out on interface 1 with normal type of service. */
status = nx_ip_raw_packet_interface_send(ip_ptr, packet_ptr,
    destination_ip,
    ADDRESS_INDEX,
    NX_IP_NORMAL);
/* If status is NX_SUCCESS the packet was successfully transmitted. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1256">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1256">See Also</span></span>

- <span data-ttu-id="36624-1257">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-1257">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span></span>
- <span data-ttu-id="36624-1258">nx_ip_raw_packet_receive, nx_ip_raw_packet_send</span><span class="sxs-lookup"><span data-stu-id="36624-1258">nx_ip_raw_packet_receive, nx_ip_raw_packet_send</span></span>

## <a name="nx_ip_raw_packet_receive"></a><span data-ttu-id="36624-1259">nx_ip_raw_packet_receive</span><span class="sxs-lookup"><span data-stu-id="36624-1259">nx_ip_raw_packet_receive</span></span>

<span data-ttu-id="36624-1260">Ham IP paketi al</span><span class="sxs-lookup"><span data-stu-id="36624-1260">Receive raw IP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1261">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1261">Prototype</span></span>

```C
UINT nx_ip_raw_packet_receive(
    NX_IP *ip_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-1262">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1262">Description</span></span>

<span data-ttu-id="36624-1263">Bu hizmet, belirtilen IP örneğinden bir ham IP paketi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-1263">This service receives a raw IP packet from the specified IP instance.</span></span> <span data-ttu-id="36624-1264">Ham paket alma kuyruğunda IP paketleri varsa, arayana ilk (en eski) paket döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-1264">If there are IP packets on the raw packet receive queue, the first (oldest) packet is returned to the caller.</span></span> <span data-ttu-id="36624-1265">Aksi takdirde, kullanılabilir bir paket yoksa, çağıran bekleme seçeneğinde belirtilen şekilde askıya alabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-1265">Otherwise, if no packets are available, the caller may suspend as specified by the wait option.</span></span>

<span data-ttu-id="36624-1266">*NX_SUCCESS, döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur.*</span><span class="sxs-lookup"><span data-stu-id="36624-1266">*If NX_SUCCESS, is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1267">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1267">Parameters</span></span>

- <span data-ttu-id="36624-1268">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1268">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1269">**packet_ptr** Alınan ham IP paketinin yerleştirileceği işaretçiye işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1269">**packet_ptr** Pointer to pointer to place the received raw IP packet in.</span></span>
- <span data-ttu-id="36624-1270">**wait_option** Kullanılabilir ham IP paketleri yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1270">**wait_option** Defines how the service behaves if there are no raw IP packets available.</span></span> <span data-ttu-id="36624-1271">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-1271">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-1272">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-1272">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-1273">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-1273">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-1274">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-1274">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1275">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1275">Return Values</span></span>

- <span data-ttu-id="36624-1276">**NX_SUCCESS** (0x00) başarılı IP ham paket alma.</span><span class="sxs-lookup"><span data-stu-id="36624-1276">**NX_SUCCESS** (0x00) Successful IP raw packet receive.</span></span>
- <span data-ttu-id="36624-1277">**NX_NO_PACKET** (0x01) kullanılabilir paket yok.</span><span class="sxs-lookup"><span data-stu-id="36624-1277">**NX_NO_PACKET** (0x01) No packet was available.</span></span>
- <span data-ttu-id="36624-1278">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1278">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-1279">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-1279">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-1280">**NX_PTR_ERROR** (0x07) geçersiz IP veya dönüş paketi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1280">**NX_PTR_ERROR** (0x07) Invalid IP or return packet pointer.</span></span>
- <span data-ttu-id="36624-1281">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="36624-1281">**NX_CALLER_ERROR** (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1282">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1282">Allowed From</span></span>

<span data-ttu-id="36624-1283">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1283">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1284">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1284">Preemption Possible</span></span>

<span data-ttu-id="36624-1285">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1285">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1286">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1286">Example</span></span>

```C
/* Receive a raw IP packet for this IP instance, wait for a maximum
    of 4 timer ticks. */
status = nx_ip_raw_packet_receive(&ip_0, &packet_ptr, 4);

/* If status is NX_SUCCESS, the raw IP packet pointer is in the
    variable packet_ptr. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1287">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1287">See Also</span></span>

- <span data-ttu-id="36624-1288">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-1288">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span></span>
- <span data-ttu-id="36624-1289">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="36624-1289">nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send</span></span>

## <a name="nx_ip_raw_packet_send"></a><span data-ttu-id="36624-1290">nx_ip_raw_packet_send</span><span class="sxs-lookup"><span data-stu-id="36624-1290">nx_ip_raw_packet_send</span></span>

<span data-ttu-id="36624-1291">Ham IP paketi gönder</span><span class="sxs-lookup"><span data-stu-id="36624-1291">Send raw IP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1292">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1292">Prototype</span></span>

```C
UINT nx_ip_raw_packet_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    ULONG type_of_service);
```

### <a name="description"></a><span data-ttu-id="36624-1293">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1293">Description</span></span>

<span data-ttu-id="36624-1294">Bu hizmet hedef IP adresine bir ham IP paketi gönderir.</span><span class="sxs-lookup"><span data-stu-id="36624-1294">This service sends a raw IP packet to the destination IP address.</span></span> <span data-ttu-id="36624-1295">Bu yordamın hemen geri döndüğüne ve bu nedenle IP paketinin gerçekten gönderilip gönderilmediğini bilinmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-1295">Note that this routine returns immediately, and it is therefore not known whether the IP packet has actually been sent.</span></span> <span data-ttu-id="36624-1296">Ağ sürücüsü, iletim tamamlandığında paketin serbest bırakılmasından sorumlu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="36624-1296">The network driver will be responsible for releasing the packet when the transmission is complete.</span></span>

<span data-ttu-id="36624-1297">NetX, çok ana bir sistem için hedef IP adresini kullanarak uygun bir ağ arabirimi bulur ve arabirimin IP adresini kaynak adres olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="36624-1297">For a multihome system, NetX uses the destination IP address to find an appropriate network interface and uses the IP address of the interface as the source address.</span></span> <span data-ttu-id="36624-1298">Hedef IP adresi yayın veya çok noktaya yayın ise, ilk geçerli arabirim kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36624-1298">If the destination IP address is broadcast or multicast, the first valid interface is used.</span></span> <span data-ttu-id="36624-1299">Uygulamalar bu durumda ***nx_ip_raw_packet_interface_send*** kullanır.</span><span class="sxs-lookup"><span data-stu-id="36624-1299">Applications use the ***nx_ip_raw_packet_interface_send*** in this case.</span></span>

<span data-ttu-id="36624-1300">*Bir hata döndürülmediği takdirde, uygulama bu çağrıdan sonra paketi serbest bırakmamalıdır. Bunu yapmak öngörülemeyen sonuçlara neden olur çünkü ağ sürücüsü iletim sonrasında paketi serbest bırakacaktır.*</span><span class="sxs-lookup"><span data-stu-id="36624-1300">*Unless an error is returned, the application should not release the packet after this call. Doing so will cause unpredictable results because the network driver will release the packet after transmission.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1301">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1301">Parameters</span></span>

- <span data-ttu-id="36624-1302">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1302">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1303">**packet_ptr** Gönderilen ham IP paketinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1303">**packet_ptr** Pointer to the raw IP packet to send.</span></span>
- <span data-ttu-id="36624-1304">**destination_ip** Hedef IP adresi, belirli bir ana bilgisayar IP adresi, bir ağ yayını, iç geri döngü veya çok noktaya yayın adresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-1304">**destination_ip** Destination IP address, which can be a specific host IP address, a network broadcast, an internal loop-back, or a multicast address.</span></span>
- <span data-ttu-id="36624-1305">**Type_of_service** İletim için hizmet türünü tanımlar, yasal değerler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="36624-1305">**type_of_service** Defines the type of service for the transmission, legal values are as follows:</span></span>
- <span data-ttu-id="36624-1306">NX_IP_NORMAL (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-1306">NX_IP_NORMAL (0x00000000)</span></span>
- <span data-ttu-id="36624-1307">NX_IP_MIN_DELAY (0x00100000)</span><span class="sxs-lookup"><span data-stu-id="36624-1307">NX_IP_MIN_DELAY (0x00100000)</span></span>
- <span data-ttu-id="36624-1308">NX_IP_MAX_DATA (0x00080000)</span><span class="sxs-lookup"><span data-stu-id="36624-1308">NX_IP_MAX_DATA (0x00080000)</span></span>
- <span data-ttu-id="36624-1309">NX_IP_MAX_RELIABLE (0x00040000)</span><span class="sxs-lookup"><span data-stu-id="36624-1309">NX_IP_MAX_RELIABLE (0x00040000)</span></span>
- <span data-ttu-id="36624-1310">NX_IP_MIN_COST (0x00020000)</span><span class="sxs-lookup"><span data-stu-id="36624-1310">NX_IP_MIN_COST (0x00020000)</span></span>


### <a name="return-values"></a><span data-ttu-id="36624-1311">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1311">Return Values</span></span>

- <span data-ttu-id="36624-1312">**NX_SUCCESS** (0x00) başarılı IP ham paket gönderimi başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="36624-1312">**NX_SUCCESS** (0x00) Successful IP raw packet send initiated.</span></span>
- <span data-ttu-id="36624-1313">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-1313">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="36624-1314">**NX_NOT_ENABLED** (0x14) ham IP özelliği etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-1314">**NX_NOT_ENABLED** (0x14) Raw IP feature is not enabled.</span></span>
- <span data-ttu-id="36624-1315">**NX_OPTION_ERROR** (0X0a) geçersiz hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="36624-1315">**NX_OPTION_ERROR** (0x0A) Invalid type of service.</span></span>
- <span data-ttu-id="36624-1316">**NX_UNDERFLOW** (0x02) pakette bir IP üst bilgisini eklemek için yeterli yer yok.</span><span class="sxs-lookup"><span data-stu-id="36624-1316">**NX_UNDERFLOW** (0x02) Not enough room to prepend an IP header on the packet.</span></span>
- <span data-ttu-id="36624-1317">**NX_OVERFLOW** (0x03) paket ekleme işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-1317">**NX_OVERFLOW** (0x03) Packet append pointer is invalid.</span></span>
- <span data-ttu-id="36624-1318">**NX_PTR_ERROR** (0x07) geçersiz IP veya paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1318">**NX_PTR_ERROR** (0x07) Invalid IP or packet pointer.</span></span>
- <span data-ttu-id="36624-1319">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1319">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1320">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1320">Allowed From</span></span>

<span data-ttu-id="36624-1321">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1321">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1322">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1322">Preemption Possible</span></span>

<span data-ttu-id="36624-1323">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1323">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1324">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1324">Example</span></span>

```C
/* Send a raw IP packet to IP address 1.2.3.5. */
status = nx_ip_raw_packet_send(&ip_0, packet_ptr,
    IP_ADDRESS(1,2,3,5),
    NX_IP_NORMAL);

/* If status is NX_SUCCESS, the raw IP packet pointed to by
    packet_ptr has been sent. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1325">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1325">See Also</span></span>

- <span data-ttu-id="36624-1326">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-1326">nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,</span></span>
- <span data-ttu-id="36624-1327">nx_ip_raw_packet_receive, nx_ip_raw_packet_send,</span><span class="sxs-lookup"><span data-stu-id="36624-1327">nx_ip_raw_packet_receive, nx_ip_raw_packet_send,</span></span>
- <span data-ttu-id="36624-1328">nx_ip_raw_packet_interface_send</span><span class="sxs-lookup"><span data-stu-id="36624-1328">nx_ip_raw_packet_interface_send</span></span>

## <a name="nx_ip_static_route_add"></a><span data-ttu-id="36624-1329">nx_ip_static_route_add</span><span class="sxs-lookup"><span data-stu-id="36624-1329">nx_ip_static_route_add</span></span>

<span data-ttu-id="36624-1330">Yönlendirme tablosuna statik yol ekleme</span><span class="sxs-lookup"><span data-stu-id="36624-1330">Add static route to the routing table</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1331">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1331">Prototype</span></span>

```C
UINT nx_ip_static_route_add(
    NX_IP *ip_ptr,
    ULONG network_address,
    ULONG net_mask,
    ULONG next_hop);
```

### <a name="description"></a><span data-ttu-id="36624-1332">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1332">Description</span></span>

<span data-ttu-id="36624-1333">Bu hizmet, statik yönlendirme tablosuna bir giriş ekler.</span><span class="sxs-lookup"><span data-stu-id="36624-1333">This service adds an entry to the static routing table.</span></span> <span data-ttu-id="36624-1334">*Next_hop* adresine yerel ağ aygıtlarından birinden doğrudan erişilebilir olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-1334">Note that the *next_hop* address must be directly accessible from one of the local network devices.</span></span>

<span data-ttu-id="36624-1335">*İp_ptr geçerli bir NetX IP yapısına işaret etmelidir ve NetX kitaplığı bu hizmeti kullanmak için tanımlanan NX_ENABLE_IP_STATIC_ROUTING oluşturulmuş olmalıdır. Varsayılan olarak NetX, NX_ENABLE_IP_STATIC_ROUTING tanımlı olmadan oluşturulur.*</span><span class="sxs-lookup"><span data-stu-id="36624-1335">*Note that ip_ptr must point to a valid NetX IP structure and the NetX library must be built with NX_ENABLE_IP_STATIC_ROUTING defined to use this service. By default NetX is built without NX_ENABLE_IP_STATIC_ROUTING defined.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1336">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1336">Parameters</span></span>

- <span data-ttu-id="36624-1337">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1337">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1338">**network_address** Konak bayt düzeninde hedef ağ adresi</span><span class="sxs-lookup"><span data-stu-id="36624-1338">**network_address** Target network address, in host byte order</span></span>
- <span data-ttu-id="36624-1339">**net_mask** Konak bayt düzeninde hedef ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="36624-1339">**net_mask** Target network mask, in host byte order</span></span>
- <span data-ttu-id="36624-1340">**next_hop** Hedef ağ için, ana bilgisayar bayt düzeninde sonraki atlama adresi</span><span class="sxs-lookup"><span data-stu-id="36624-1340">**next_hop** Next hop address for the target network, in host byte order</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1341">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1341">Return Values</span></span>

- <span data-ttu-id="36624-1342">**NX_SUCCESS** (0x00) girişi statik yönlendirme tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="36624-1342">**NX_SUCCESS** (0x00) Entry is added to the static routing table.</span></span>
- <span data-ttu-id="36624-1343">**NX_OVERFLOW** (0x03) statik yönlendirme tablosu dolu.</span><span class="sxs-lookup"><span data-stu-id="36624-1343">**NX_OVERFLOW** (0x03) Static routing table is full.</span></span>
- <span data-ttu-id="36624-1344">**NX_NOT_SUPPORTED** (0x4b) Bu özellik ' de derlenmiyor.</span><span class="sxs-lookup"><span data-stu-id="36624-1344">**NX_NOT_SUPPORTED** (0x4B) This feature is not compiled in.</span></span>
- <span data-ttu-id="36624-1345">**NX_IP_ADDRESS_ERROR** (0x21) sonraki atlama, yerel arabirimler aracılığıyla doğrudan erişilemez.</span><span class="sxs-lookup"><span data-stu-id="36624-1345">**NX_IP_ADDRESS_ERROR** (0x21) Next hop is not directly accessible via local interfaces.</span></span>
- <span data-ttu-id="36624-1346">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1346">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1347">**NX_PTR_ERROR** (0x07) geçersiz ip_ptr işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1347">**NX_PTR_ERROR** (0x07) Invalid ip_ptr pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1348">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1348">Allowed From</span></span>

<span data-ttu-id="36624-1349">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1349">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1350">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1350">Preemption Possible</span></span>

<span data-ttu-id="36624-1351">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1351">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1352">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1352">Example</span></span>

```C
/* Specify the next hop for the 192.168.10.0 through the gateway
    192.168.1.1. */
status = nx_ip_static_route_add(ip_ptr, IP_ADDRESS(192,168,10,0),
    0xFFFFFF00UL,
    IP_ADDRESS(192,168,1,1));

/* If status is NX_SUCCESS the route was successfully added to the
    static routing table. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1353">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1353">See Also</span></span>

- <span data-ttu-id="36624-1354">nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_delete</span><span class="sxs-lookup"><span data-stu-id="36624-1354">nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_delete</span></span>

## <a name="nx_ip_static_route_delete"></a><span data-ttu-id="36624-1355">nx_ip_static_route_delete</span><span class="sxs-lookup"><span data-stu-id="36624-1355">nx_ip_static_route_delete</span></span>

<span data-ttu-id="36624-1356">Yönlendirme tablosundan statik yolu Sil</span><span class="sxs-lookup"><span data-stu-id="36624-1356">Delete static route from routing table</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1357">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1357">Prototype</span></span>

```C
UINT nx_ip_static_route_delete(
    NX_IP *ip_ptr,
    ULONG network_address, 
    ULONG net_mask);
```

### <a name="description"></a><span data-ttu-id="36624-1358">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1358">Description</span></span>

<span data-ttu-id="36624-1359">Bu hizmet, statik yönlendirme tablosundan bir girişi siler.</span><span class="sxs-lookup"><span data-stu-id="36624-1359">This service deletes an entry from the static routing table.</span></span>

<span data-ttu-id="36624-1360">*İp_ptr geçerli bir NetX IP yapısına işaret etmelidir ve NetX kitaplığı bu hizmeti kullanmak için tanımlanan NX_ENABLE_IP_STATIC_ROUTING oluşturulmuş olmalıdır. Varsayılan olarak NetX, NX_ENABLE_IP_STATIC_ROUTING tanımlı olmadan oluşturulur.*</span><span class="sxs-lookup"><span data-stu-id="36624-1360">*Note that ip_ptr must point to a valid NetX IP structure and the NetX library must be built with NX_ENABLE_IP_STATIC_ROUTING defined to use this service. By default NetX is built without NX_ENABLE_IP_STATIC_ROUTING defined.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1361">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1361">Parameters</span></span>

- <span data-ttu-id="36624-1362">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1362">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1363">**network_address** Konak bayt düzeninde hedef ağ adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-1363">**network_address** Target network address, in host byte order.</span></span>
- <span data-ttu-id="36624-1364">**net_mask** Konak bayt düzeninde hedef ağ maskesi.</span><span class="sxs-lookup"><span data-stu-id="36624-1364">**net_mask** Target network mask, in host byte order.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1365">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1365">Allowed From</span></span>

<span data-ttu-id="36624-1366">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1366">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1367">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1367">Preemption Possible</span></span>

<span data-ttu-id="36624-1368">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1368">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1369">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1369">Example</span></span>

```C
/* Remove the static route for 192.168.10.0 from the routing table.*/
status = nx_ip_static_route_delete(ip_ptr,
    IP_ADDRESS(192,168,10,0), 0xFFFFFF00UL,);

/* If status is NX_SUCCESS the route was successfully removed from
    the static routing table. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1370">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1370">See Also</span></span>

- <span data-ttu-id="36624-1371">nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_add</span><span class="sxs-lookup"><span data-stu-id="36624-1371">nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_add</span></span>

## <a name="nx_ip_status_check"></a><span data-ttu-id="36624-1372">nx_ip_status_check</span><span class="sxs-lookup"><span data-stu-id="36624-1372">nx_ip_status_check</span></span>

<span data-ttu-id="36624-1373">Bir IP örneğinin durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="36624-1373">Check status of an IP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1374">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1374">Prototype</span></span>

```C
UINT nx_ip_status_check(
    NX_IP *ip_ptr,
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-1375">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1375">Description</span></span>

<span data-ttu-id="36624-1376">Bu hizmet, daha önce oluşturulmuş bir IP örneğinin birincil ağ arabiriminin belirtilen durumunu denetler ve isteğe bağlı olarak bekler.</span><span class="sxs-lookup"><span data-stu-id="36624-1376">This service checks and optionally waits for the specified status of the primary network interface of a previously created IP instance.</span></span> <span data-ttu-id="36624-1377">İkincil arabirimlerde durum almak için, uygulamalar hizmeti ***nx_ip_interface_status_check kullanacaktır.***</span><span class="sxs-lookup"><span data-stu-id="36624-1377">To obtain status on secondary interfaces, applications shall use the service ***nx_ip_interface_status_check.***</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1378">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1378">Parameters</span></span>

- <span data-ttu-id="36624-1379">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1379">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1380">**needed_status** Aşağıdaki gibi bit eşleme biçiminde tanımlanan IP durumu istendi:</span><span class="sxs-lookup"><span data-stu-id="36624-1380">**needed_status** IP status requested, defined in bit-map form as follows:</span></span>
- <span data-ttu-id="36624-1381">NX_IP_INITIALIZE_DONE (0x0001)</span><span class="sxs-lookup"><span data-stu-id="36624-1381">NX_IP_INITIALIZE_DONE (0x0001)</span></span>
- <span data-ttu-id="36624-1382">NX_IP_ADDRESS_RESOLVED (0x0002)</span><span class="sxs-lookup"><span data-stu-id="36624-1382">NX_IP_ADDRESS_RESOLVED (0x0002)</span></span>
- <span data-ttu-id="36624-1383">NX_IP_LINK_ENABLED (0x0004)</span><span class="sxs-lookup"><span data-stu-id="36624-1383">NX_IP_LINK_ENABLED (0x0004)</span></span>
- <span data-ttu-id="36624-1384">NX_IP_ARP_ENABLED (0x0008)</span><span class="sxs-lookup"><span data-stu-id="36624-1384">NX_IP_ARP_ENABLED (0x0008)</span></span>
- <span data-ttu-id="36624-1385">NX_IP_UDP_ENABLED (0x0010)</span><span class="sxs-lookup"><span data-stu-id="36624-1385">NX_IP_UDP_ENABLED (0x0010)</span></span>
- <span data-ttu-id="36624-1386">NX_IP_TCP_ENABLED (0x0020)</span><span class="sxs-lookup"><span data-stu-id="36624-1386">NX_IP_TCP_ENABLED (0x0020)</span></span>
- <span data-ttu-id="36624-1387">NX_IP_IGMP_ENABLED (0x0040)</span><span class="sxs-lookup"><span data-stu-id="36624-1387">NX_IP_IGMP_ENABLED (0x0040)</span></span>
- <span data-ttu-id="36624-1388">NX_IP_RARP_COMPLETE (0x0080)</span><span class="sxs-lookup"><span data-stu-id="36624-1388">NX_IP_RARP_COMPLETE (0x0080)</span></span>
- <span data-ttu-id="36624-1389">NX_IP_INTERFACE_LINK_ENABLED (0x0100)</span><span class="sxs-lookup"><span data-stu-id="36624-1389">NX_IP_INTERFACE_LINK_ENABLED (0x0100)</span></span>
- <span data-ttu-id="36624-1390">**actual_status** Gerçek bitler kümesinin hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1390">**actual_status** Pointer to destination of actual bits set.</span></span>
- <span data-ttu-id="36624-1391">**wait_option** İstenen durum bitleri yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1391">**wait_option** Defines how the service behaves if the requested status bits are not available.</span></span> <span data-ttu-id="36624-1392">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-1392">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-1393">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-1393">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-1394">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-1394">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-1395">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-1395">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1396">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1396">Return Values</span></span>

- <span data-ttu-id="36624-1397">**NX_SUCCESS** (0x00) başarılı IP durum denetimi.</span><span class="sxs-lookup"><span data-stu-id="36624-1397">**NX_SUCCESS** (0x00) Successful IP status check.</span></span>
- <span data-ttu-id="36624-1398">**NX_NOT_SUCCESSFUL** (0x43) durum isteği belirtilen zaman aşımı süresi içinde karşılanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-1398">**NX_NOT_SUCCESSFUL** (0x43) Status request was not satisfied within the timeout specified.</span></span>
- <span data-ttu-id="36624-1399">**NX_PTR_ERROR** (0x07) IP işaretçisi veya geçersiz hale geldi ya da gerçek durum işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-1399">**NX_PTR_ERROR** (0x07) IP pointer is or has become invalid, or actual status pointer is invalid.</span></span>
- <span data-ttu-id="36624-1400">**NX_OPTION_ERROR** (0X0a) geçersiz gerekli durum seçeneği.</span><span class="sxs-lookup"><span data-stu-id="36624-1400">**NX_OPTION_ERROR** (0x0a) Invalid needed status option.</span></span>
- <span data-ttu-id="36624-1401">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1401">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1402">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1402">Allowed From</span></span>

<span data-ttu-id="36624-1403">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1403">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1404">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1404">Preemption Possible</span></span>

<span data-ttu-id="36624-1405">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1405">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1406">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1406">Example</span></span>

```C
/* Wait 10 ticks for the link up status on the previously created IP
    instance. */
status = nx_ip_status_check(&ip_0, NX_IP_LINK_ENABLED,
    &actual_status, 10);

/* If status is NX_SUCCESS, the link for the specified IP instance
    is up. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1407">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1407">See Also</span></span>

- <span data-ttu-id="36624-1408">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-1408">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-1409">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-1409">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-1410">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-1410">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-1411">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-1411">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="36624-1412">nx_ip_fragment_enable, nx_ip_info_get, nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-1412">nx_ip_fragment_enable, nx_ip_info_get, nx_system_initialize</span></span>

## <a name="nx_packet_allocate"></a><span data-ttu-id="36624-1413">nx_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="36624-1413">nx_packet_allocate</span></span>

<span data-ttu-id="36624-1414">Belirtilen havuzdan paket ayır</span><span class="sxs-lookup"><span data-stu-id="36624-1414">Allocate packet from specified pool</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1415">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1415">Prototype</span></span>

```C
UINT nx_packet_allocate(
    NX_PACKET_POOL *pool_ptr,
    NX_PACKET **packet_ptr,
    ULONG packet_type,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-1416">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1416">Description</span></span>

<span data-ttu-id="36624-1417">Bu hizmet belirtilen havuzdan bir paket ayırır ve belirtilen paket türüne göre paketteki preppointer 'ı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1417">This service allocates a packet from the specified pool and adjusts the prepend pointer in the packet according to the type of packet specified.</span></span> <span data-ttu-id="36624-1418">Kullanılabilir bir paket yoksa hizmet, sağlanan bekleme seçeneğine göre askıya alır.</span><span class="sxs-lookup"><span data-stu-id="36624-1418">If no packet is available, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1419">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1419">Parameters</span></span>

- <span data-ttu-id="36624-1420">**pool_ptr** Daha önce oluşturulan paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1420">**pool_ptr** Pointer to previously created packet pool.</span></span>
- <span data-ttu-id="36624-1421">**packet_ptr** Ayrılan paket işaretçisinin işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1421">**packet_ptr** Pointer to the pointer of the allocated packet pointer.</span></span>
- <span data-ttu-id="36624-1422">**packet_type** İstenen paket türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1422">**packet_type** Defines the type of packet requested.</span></span> <span data-ttu-id="36624-1423">Desteklenen paket türlerinin listesi için, Bölüm 3 ' teki "Paket havuzları 49" bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="36624-1423">See “Packet Pools” on page 49 in Chapter 3 for a list of supported packet types.</span></span>
- <span data-ttu-id="36624-1424">**wait_option** Paket havuzunda kullanılabilir bir paket yoksa, zaman işaretleri cinsinden bekleme süresini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1424">**wait_option** Defines the wait time in ticks if there are no packets available in the packet pool.</span></span> <span data-ttu-id="36624-1425">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-1425">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-1426">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-1426">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-1427">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-1427">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-1428">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-1428">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1429">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1429">Return Values</span></span>

- <span data-ttu-id="36624-1430">**NX_SUCCESS** (0x00) başarılı paket ayırması.</span><span class="sxs-lookup"><span data-stu-id="36624-1430">**NX_SUCCESS** (0x00) Successful packet allocate.</span></span>
- <span data-ttu-id="36624-1431">**NX_NO_PACKET** (0x01) kullanılabilir paket yok.</span><span class="sxs-lookup"><span data-stu-id="36624-1431">**NX_NO_PACKET** (0x01) No packet available.</span></span>
- <span data-ttu-id="36624-1432">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1432">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-1433">**NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.</span><span class="sxs-lookup"><span data-stu-id="36624-1433">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="36624-1434">**NX_OPTION_ERROR** (0X0a) geçersiz paket türü.</span><span class="sxs-lookup"><span data-stu-id="36624-1434">**NX_OPTION_ERROR** (0x0A) Invalid packet type.</span></span>
- <span data-ttu-id="36624-1435">**NX_PTR_ERROR** (0x07) geçersiz havuz veya paket döndürme işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1435">**NX_PTR_ERROR** (0x07) Invalid pool or packet return pointer.</span></span>
- <span data-ttu-id="36624-1436">**NX_CALLER_ERROR** (0x11) Iş parçacığından geçersiz bekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="36624-1436">**NX_CALLER_ERROR** (0x11) Invalid wait option from nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1437">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1437">Allowed From</span></span>

<span data-ttu-id="36624-1438">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs (uygulama ağ sürücüleri).</span><span class="sxs-lookup"><span data-stu-id="36624-1438">Initialization, threads, timers, and ISRs (application network drivers).</span></span> <span data-ttu-id="36624-1439">Wait seçeneği, ıSR 'de veya zamanlayıcı bağlamında kullanıldığında NX_NO_WAIT olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-1439">Wait option must be NX_NO_WAIT when used in ISR or in timer context.</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1440">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1440">Preemption Possible</span></span>

<span data-ttu-id="36624-1441">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1441">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1442">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1442">Example</span></span>

```C
/* Allocate a new UDP packet from the previously created packet pool
    and suspend for a maximum of 5 timer ticks if the pool is
    empty. */
status = nx_packet_allocate(&pool_0, &packet_ptr, NX_UDP_PACKET, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is
    found in the variable packet_ptr. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1443">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1443">See Also</span></span>

- <span data-ttu-id="36624-1444">nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1444">nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1445">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="36624-1445">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="36624-1446">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-1446">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="36624-1447">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="36624-1447">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="36624-1448">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1448">nx_packet_transmit_release</span></span>

## <a name="nx_packet_copy"></a><span data-ttu-id="36624-1449">nx_packet_copy</span><span class="sxs-lookup"><span data-stu-id="36624-1449">nx_packet_copy</span></span>

<span data-ttu-id="36624-1450">Paketi Kopyala</span><span class="sxs-lookup"><span data-stu-id="36624-1450">Copy packet</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1451">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1451">Prototype</span></span>

```C
UINT nx_packet_copy(
    NX_PACKET *packet_ptr,
    NX_PACKET **new_packet_ptr,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-1452">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1452">Description</span></span>

<span data-ttu-id="36624-1453">Bu hizmet, sağlanan paketteki bilgileri sağlanan paket havuzundan ayrılan bir veya daha fazla yeni pakete kopyalar.</span><span class="sxs-lookup"><span data-stu-id="36624-1453">This service copies the information in the supplied packet to one or more new packets that are allocated from the supplied packet pool.</span></span> <span data-ttu-id="36624-1454">Başarılı olursa, yeni pakete yönelik işaretçi **new_packet_ptr** tarafından işaret edilen hedefte döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-1454">If successful, the pointer to the new packet is returned in destination pointed to by **new_packet_ptr**.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1455">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1455">Parameters</span></span>

- <span data-ttu-id="36624-1456">**packet_ptr** Kaynak paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1456">**packet_ptr** Pointer to the source packet.</span></span>
- <span data-ttu-id="36624-1457">**new_packet_ptr** Paketin yeni kopyasına işaretçinin nereye dönebileceği hedefe yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1457">**new_packet_ptr** Pointer to the destination of where to return the pointer to the new copy of the packet.</span></span>
- <span data-ttu-id="36624-1458">**pool_ptr** Kopya için bir veya daha fazla paket ayırmak için kullanılan önceden oluşturulmuş paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1458">**pool_ptr** Pointer to the previously created packet pool that is used to allocate one or more packets for the copy.</span></span>
- <span data-ttu-id="36624-1459">**wait_option** Kullanılabilir bir paket yoksa hizmetin nasıl bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1459">**wait_option** Defines how the service waits if there are no packets available.</span></span> <span data-ttu-id="36624-1460">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-1460">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-1461">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-1461">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-1462">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-1462">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-1463">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-1463">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1464">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1464">Return Values</span></span>
- <span data-ttu-id="36624-1465">**NX_SUCCESS** (0x00) başarılı paket kopyası.</span><span class="sxs-lookup"><span data-stu-id="36624-1465">**NX_SUCCESS** (0x00) Successful packet copy.</span></span>
- <span data-ttu-id="36624-1466">**NX_NO_PACKET** (0x01) paketi kopyalama için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="36624-1466">**NX_NO_PACKET** (0x01) Packet not available for copy.</span></span>
- <span data-ttu-id="36624-1467">**NX_INVALID_PACKET** (0x12) boş kaynak paketi veya kopyalama başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="36624-1467">**NX_INVALID_PACKET** (0x12) Empty source packet or copy failed.</span></span>
- <span data-ttu-id="36624-1468">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1468">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-1469">**NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.</span><span class="sxs-lookup"><span data-stu-id="36624-1469">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="36624-1470">**NX_PTR_ERROR** (0x07) geçersiz havuz, paket veya hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1470">**NX_PTR_ERROR** (0x07) Invalid pool, packet, or destination pointer.</span></span>
- <span data-ttu-id="36624-1471">**NX_UNDERFLOW** (0x02) geçersiz paket önüne işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1471">**NX_UNDERFLOW** (0x02) Invalid packet prepend pointer.</span></span>
- <span data-ttu-id="36624-1472">**NX_OVERFLOW** (0x03) geçersiz paket ekleme işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1472">**NX_OVERFLOW** (0x03) Invalid packet append pointer.</span></span>
- <span data-ttu-id="36624-1473">**NX_CALLER_ERROR** (0x11) başlatma veya ISR içinde bir bekleme seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1473">**NX_CALLER_ERROR** (0x11) A wait option was specified in initialization or in an ISR.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1474">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1474">Allowed From</span></span>

<span data-ttu-id="36624-1475">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="36624-1475">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1476">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1476">Preemption Possible</span></span>

<span data-ttu-id="36624-1477">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1477">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1478">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1478">Example</span></span>

```C
NX_PACKET *new_copy_ptr;

/* Copy packet pointed to by "old_packet_ptr" using packets from
    previously created packet pool_0. */
status = nx_packet_copy(old_packet, &new_copy_ptr, &pool_0, 20);

/* If status is NX_SUCCESS, new_copy_ptr points to the packet copy. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1479">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1479">See Also</span></span>

- <span data-ttu-id="36624-1480">nx_packet_allocate, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1480">nx_packet_allocate, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1481">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="36624-1481">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="36624-1482">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-1482">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="36624-1483">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="36624-1483">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="36624-1484">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1484">nx_packet_transmit_release</span></span>

## <a name="nx_packet_data_append"></a><span data-ttu-id="36624-1485">nx_packet_data_append</span><span class="sxs-lookup"><span data-stu-id="36624-1485">nx_packet_data_append</span></span>

<span data-ttu-id="36624-1486">Paketi sonuna veri Ekle</span><span class="sxs-lookup"><span data-stu-id="36624-1486">Append data to end of packet</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1487">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1487">Prototype</span></span>

```C
UINT nx_packet_data_append(
    NX_PACKET *packet_ptr,
    VOID *data_start, 
    ULONG data_size,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-1488">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1488">Description</span></span>

<span data-ttu-id="36624-1489">Bu hizmet, verileri belirtilen paketin sonuna ekler.</span><span class="sxs-lookup"><span data-stu-id="36624-1489">This service appends data to the end of the specified packet.</span></span> <span data-ttu-id="36624-1490">Sağlanan veri alanı pakete kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="36624-1490">The supplied data area is copied into the packet.</span></span> <span data-ttu-id="36624-1491">Yeterli kullanılabilir bellek yoksa ve zincirleme paket özelliği etkinse, isteği karşılamak için bir veya daha fazla paket ayrılır.</span><span class="sxs-lookup"><span data-stu-id="36624-1491">If there is not enough memory available, and the chained packet feature is enabled, one or more packets will be allocated to satisfy the request.</span></span> <span data-ttu-id="36624-1492">Zincirleme paket özelliği etkinleştirilmemişse, *NX_SIZE_ERROR* döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-1492">If the chained packet feature is not enabled, *NX_SIZE_ERROR* is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1493">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1493">Parameters</span></span>

- <span data-ttu-id="36624-1494">**packet_ptr** Paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1494">**packet_ptr** Packet pointer.</span></span>
- <span data-ttu-id="36624-1495">**data_start** Pakete eklenecek kullanıcının veri alanının başlangıcına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1495">**data_start** Pointer to the start of the user’s data area to append to the packet.</span></span>
- <span data-ttu-id="36624-1496">**data_size** Kullanıcının veri alanının boyutu.</span><span class="sxs-lookup"><span data-stu-id="36624-1496">**data_size** Size of user’s data area.</span></span>
- <span data-ttu-id="36624-1497">**pool_ptr** Geçerli pakette yeterli alan yoksa başka bir paketin ayırabileceği paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1497">**pool_ptr** Pointer to packet pool from which to allocate another packet if there is not enough room in the current packet.</span></span>
- <span data-ttu-id="36624-1498">**wait_option** Kullanılabilir bir paket yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1498">**wait_option** Defines how the service behaves if there are no packets available.</span></span> <span data-ttu-id="36624-1499">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-1499">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-1500">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-1500">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-1501">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-1501">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-1502">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-1502">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1503">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1503">Return Values</span></span>

- <span data-ttu-id="36624-1504">**NX_SUCCESS** (0x00) başarılı paket ekleme.</span><span class="sxs-lookup"><span data-stu-id="36624-1504">**NX_SUCCESS** (0x00) Successful packet append.</span></span>
- <span data-ttu-id="36624-1505">**NX_NO_PACKET** (0x01) kullanılabilir paket yok.</span><span class="sxs-lookup"><span data-stu-id="36624-1505">**NX_NO_PACKET** (0x01) No packet available.</span></span>
- <span data-ttu-id="36624-1506">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği *tx_thread_wait_abort* bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1506">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="36624-1507">**NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.</span><span class="sxs-lookup"><span data-stu-id="36624-1507">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="36624-1508">**NX_UNDERFLOW** (0x02) Prepend işaretçisi yük başlangıcından daha küçüktür.</span><span class="sxs-lookup"><span data-stu-id="36624-1508">**NX_UNDERFLOW** (0x02) Prepend pointer is less than payload start.</span></span>
- <span data-ttu-id="36624-1509">**NX_OVERFLOW** (0x03) ekleme işaretçisi yük ucundan daha büyük.</span><span class="sxs-lookup"><span data-stu-id="36624-1509">**NX_OVERFLOW** (0x03) Append pointer is greater than payload end.</span></span>
- <span data-ttu-id="36624-1510">**NX_PTR_ERROR** (0x07) geçersiz havuz, paket veya veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1510">**NX_PTR_ERROR** (0x07) Invalid pool, packet, or data Pointer.</span></span>
- <span data-ttu-id="36624-1511">**NX_SIZE_ERROR** (0x09) geçersiz veri boyutu.</span><span class="sxs-lookup"><span data-stu-id="36624-1511">**NX_SIZE_ERROR** (0x09) Invalid data size.</span></span>
- <span data-ttu-id="36624-1512">**NX_CALLER_ERROR** (0x11) Iş parçacığından geçersiz bekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="36624-1512">**NX_CALLER_ERROR** (0x11) Invalid wait option from nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1513">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1513">Allowed From</span></span>

<span data-ttu-id="36624-1514">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs (uygulama ağ sürücüleri)</span><span class="sxs-lookup"><span data-stu-id="36624-1514">Initialization, threads, timers, and ISRs (application network drivers)</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1515">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1515">Preemption Possible</span></span>

<span data-ttu-id="36624-1516">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1516">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1517">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1517">Example</span></span>

```C
/* Append "abcd" to the specified packet. */
status = nx_packet_data_append(packet_ptr, "abcd", 4, &pool_0, 5);

/* If status is NX_SUCCESS, the additional four bytes "abcd" have
    been appended to the packet. */
```


### <a name="see-also"></a><span data-ttu-id="36624-1518">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1518">See Also</span></span>

- <span data-ttu-id="36624-1519">nx_packet_allocate, nx_packet_copy, nx_packet_data_extract_offset,</span><span class="sxs-lookup"><span data-stu-id="36624-1519">nx_packet_allocate, nx_packet_copy, nx_packet_data_extract_offset,</span></span>
- <span data-ttu-id="36624-1520">nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,</span><span class="sxs-lookup"><span data-stu-id="36624-1520">nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,</span></span>
- <span data-ttu-id="36624-1521">nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="36624-1521">nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="36624-1522">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1522">nx_packet_transmit_release</span></span>

## <a name="nx_packet_data_extract_offset"></a><span data-ttu-id="36624-1523">nx_packet_data_extract_offset</span><span class="sxs-lookup"><span data-stu-id="36624-1523">nx_packet_data_extract_offset</span></span>

<span data-ttu-id="36624-1524">Bir sapmayı kullanarak paketten veri ayıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1524">Extract data from packet via an offset</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1525">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1525">Prototype</span></span>

```C
UINT nx_packet_data_extract_offset(
    NX_PACKET *packet_ptr,
    ULONG offset,
    VOID *buffer_start,
    ULONG buffer_length,
    ULONG *bytes_copied);
```

### <a name="description"></a><span data-ttu-id="36624-1526">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1526">Description</span></span>

<span data-ttu-id="36624-1527">Bu hizmet bir NetX paketinden (veya paket zincirinden), belirtilen boyutun bayt cinsinden belirtilen baytından başlayarak belirtilen bir arabellekteki verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="36624-1527">This service copies data from a NetX packet (or packet chain) starting at the specified offset from the packet prepend pointer of the specified size in bytes into the specified buffer.</span></span> <span data-ttu-id="36624-1528">Gerçekten kopyalanmış olan bayt sayısı *bytes_copied döndürülür.*</span><span class="sxs-lookup"><span data-stu-id="36624-1528">The number of bytes actually copied is returned in *bytes_copied.*</span></span> <span data-ttu-id="36624-1529">Bu hizmet, paketten verileri kaldırmaz veya önüne işaretçisini veya diğer iç durum bilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1529">This service does not remove data from the packet, nor does it adjust the prepend pointer or other internal state information.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1530">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1530">Parameters</span></span>

- <span data-ttu-id="36624-1531">**packet_ptr** Ayıklanacak paket işaretçisi</span><span class="sxs-lookup"><span data-stu-id="36624-1531">**packet_ptr** Pointer to packet to extract</span></span>
- <span data-ttu-id="36624-1532">**konum** Geçerli önüne işaretçisinden gelen fark.</span><span class="sxs-lookup"><span data-stu-id="36624-1532">**offset** Offset from the current prepend pointer.</span></span>
- <span data-ttu-id="36624-1533">**buffer_start** Kaydetme arabelleğinin başlangıcı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="36624-1533">**buffer_start** Pointer to start of save buffer</span></span>
- <span data-ttu-id="36624-1534">**BUFFER_LENGTH** Kopyalanacak bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="36624-1534">**buffer_length** Number of bytes to copy</span></span>
- <span data-ttu-id="36624-1535">**bytes_copied** Gerçekten kopyalandığı bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="36624-1535">**bytes_copied** Number of bytes actually copied</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1536">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1536">Return Values</span></span>

- <span data-ttu-id="36624-1537">**NX_SUCCESS** (0x00) başarılı paket kopyası</span><span class="sxs-lookup"><span data-stu-id="36624-1537">**NX_SUCCESS** (0x00) Successful packet copy</span></span>
- <span data-ttu-id="36624-1538">**NX_PACKET_OFFSET_ERROR** (0x53) geçersiz fark değeri sağlandı</span><span class="sxs-lookup"><span data-stu-id="36624-1538">**NX_PACKET_OFFSET_ERROR** (0x53) Invalid offset value was supplied</span></span>
- <span data-ttu-id="36624-1539">**NX_PTR_ERROR** (0x07) geçersiz paket işaretçisi veya arabellek işaretçisi</span><span class="sxs-lookup"><span data-stu-id="36624-1539">**NX_PTR_ERROR** (0x07) Invalid packet pointer or buffer pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1540">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1540">Allowed From</span></span>

<span data-ttu-id="36624-1541">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="36624-1541">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1542">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1542">Preemption Possible</span></span>

<span data-ttu-id="36624-1543">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1543">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1544">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1544">Example</span></span>

```C
/* Extract 10 bytes from the start of the received packet buffer
    into the specified memory area. */
status = nx_packet_data_extract_offset(my_packet, 0, &data[0], 10,
    &bytes_copied);

/* If status is NX_SUCCESS, 10 bytes were successfully copied into
    the data buffer. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1545">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1545">See Also</span></span>

- <span data-ttu-id="36624-1546">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1546">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1547">nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,</span><span class="sxs-lookup"><span data-stu-id="36624-1547">nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,</span></span>
- <span data-ttu-id="36624-1548">nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="36624-1548">nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="36624-1549">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1549">nx_packet_transmit_release</span></span>

## <a name="nx_packet_data_retrieve"></a><span data-ttu-id="36624-1550">nx_packet_data_retrieve</span><span class="sxs-lookup"><span data-stu-id="36624-1550">nx_packet_data_retrieve</span></span>

<span data-ttu-id="36624-1551">Paketten veri al</span><span class="sxs-lookup"><span data-stu-id="36624-1551">Retrieve data from packet</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1552">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1552">Prototype</span></span>

```C
UINT nx_packet_data_retrieve(
    NX_PACKET *packet_ptr,
    VOID *buffer_start, 
    ULONG *bytes_copied);
```

### <a name="description"></a><span data-ttu-id="36624-1553">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1553">Description</span></span>

<span data-ttu-id="36624-1554">Bu hizmet, sağlanan paketten verileri sağlanan arabelleğe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="36624-1554">This service copies data from the supplied packet into the supplied buffer.</span></span> <span data-ttu-id="36624-1555">Hedef, **bytes_copied** tarafından işaret edilen hedefte döndürülen gerçek bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="36624-1555">The actual number of bytes copied is returned in the destination pointed to by **bytes_copied**.</span></span>

<span data-ttu-id="36624-1556">Bu hizmetin paketin iç durumunu değiştirmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-1556">Note that this service does not change internal state of the packet.</span></span> <span data-ttu-id="36624-1557">Alınmakta olan veriler pakette hala kullanılabilir durumda.</span><span class="sxs-lookup"><span data-stu-id="36624-1557">The data being retrieved is still available in the packet.</span></span>

<span data-ttu-id="36624-1558">*Hedef arabelleğinin paketin içeriğini tutabilecek kadar büyük olması gerekir. Aksi takdirde, bellek bozulması öngörülemeyen sonuçlara neden olur.*</span><span class="sxs-lookup"><span data-stu-id="36624-1558">*The destination buffer must be large enough to hold the packet's contents. If not, memory will be corrupted causing unpredictable results.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1559">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1559">Parameters</span></span>

- <span data-ttu-id="36624-1560">**packet_ptr** Kaynak paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1560">**packet_ptr** Pointer to the source packet.</span></span>
- <span data-ttu-id="36624-1561">**buffer_start** Arabellek alanının başlangıcına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1561">**buffer_start** Pointer to the start of the buffer area.</span></span>
- <span data-ttu-id="36624-1562">**bytes_copied** Kopyalanmış bayt sayısı için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1562">**bytes_copied** Pointer to the destination for the number of bytes copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1563">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1563">Return Values</span></span>

- <span data-ttu-id="36624-1564">**NX_SUCCESS** (0x00) başarılı paket verileri alma.</span><span class="sxs-lookup"><span data-stu-id="36624-1564">**NX_SUCCESS** (0x00) Successful packet data retrieve.</span></span>
- <span data-ttu-id="36624-1565">**NX_INVALID_PACKET** (0x12) geçersiz paket.</span><span class="sxs-lookup"><span data-stu-id="36624-1565">**NX_INVALID_PACKET** (0x12) Invalid packet.</span></span>
- <span data-ttu-id="36624-1566">**NX_PTR_ERROR** (0x07) geçersiz paket, arabellek başlangıcı veya bayt kopyalanmış işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1566">**NX_PTR_ERROR** (0x07) Invalid packet, buffer start, or bytes copied pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1567">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1567">Allowed From</span></span>

<span data-ttu-id="36624-1568">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="36624-1568">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1569">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1569">Preemption Possible</span></span>

<span data-ttu-id="36624-1570">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1570">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1571">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1571">Example</span></span>

```C
UCHAR buffer[512];
ULONG bytes_copied;

/* Retrieve data from packet pointed to by "packet_ptr". */
status = nx_packet_data_retrieve(packet_ptr, buffer, &bytes_copied);

/* If status is NX_SUCCESS, buffer contains the contents of the
    packet, the size of which is contained in "bytes_copied." */
```

### <a name="see-also"></a><span data-ttu-id="36624-1572">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1572">See Also</span></span>

- <span data-ttu-id="36624-1573">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1573">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1574">nx_packet_data_extract_offset, nx_packet_length_get,</span><span class="sxs-lookup"><span data-stu-id="36624-1574">nx_packet_data_extract_offset, nx_packet_length_get,</span></span>
- <span data-ttu-id="36624-1575">nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-1575">nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="36624-1576">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="36624-1576">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="36624-1577">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1577">nx_packet_transmit_release</span></span>

## <a name="nx_packet_length_get"></a><span data-ttu-id="36624-1578">nx_packet_length_get</span><span class="sxs-lookup"><span data-stu-id="36624-1578">nx_packet_length_get</span></span>

<span data-ttu-id="36624-1579">Paket verilerinin uzunluğunu al</span><span class="sxs-lookup"><span data-stu-id="36624-1579">Get length of packet data</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1580">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1580">Prototype</span></span>

```C
UINT nx_packet_length_get(
    NX_PACKET *packet_ptr, 
    ULONG *length);
```

### <a name="description"></a><span data-ttu-id="36624-1581">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1581">Description</span></span>

<span data-ttu-id="36624-1582">Bu hizmet, belirtilen paketteki verilerin uzunluğunu alır.</span><span class="sxs-lookup"><span data-stu-id="36624-1582">This service gets the length of the data in the specified packet.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1583">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1583">Parameters</span></span>

- <span data-ttu-id="36624-1584">**packet_ptr** Pakete yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1584">**packet_ptr** Pointer to the packet.</span></span>
- <span data-ttu-id="36624-1585">**uzunluk** Paket uzunluğu için hedef.</span><span class="sxs-lookup"><span data-stu-id="36624-1585">**length** Destination for the packet length.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1586">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1586">Allowed From</span></span>

<span data-ttu-id="36624-1587">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="36624-1587">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1588">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1588">Preemption Possible</span></span>

<span data-ttu-id="36624-1589">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1589">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1590">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1590">Example</span></span>

```C
/* Get the length of the data in "my_packet." */
status = nx_packet_length_get(my_packet, &my_length);

/* If status is NX_SUCCESS, data length is in "my_length". */
```

### <a name="see-also"></a><span data-ttu-id="36624-1591">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1591">See Also</span></span>

- <span data-ttu-id="36624-1592">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1592">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1593">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="36624-1593">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="36624-1594">nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-1594">nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="36624-1595">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="36624-1595">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="36624-1596">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1596">nx_packet_transmit_release</span></span>

## <a name="nx_packet_pool_create"></a><span data-ttu-id="36624-1597">nx_packet_pool_create</span><span class="sxs-lookup"><span data-stu-id="36624-1597">nx_packet_pool_create</span></span>

<span data-ttu-id="36624-1598">Belirtilen bellek alanında paket havuzu oluştur</span><span class="sxs-lookup"><span data-stu-id="36624-1598">Create packet pool in specified memory area</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1599">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1599">Prototype</span></span>

```C
UINT nx_packet_pool_create(
    NX_PACKET_POOL *pool_ptr,
    CHAR *name,
    ULONG payload_size,
    VOID *memory_ptr,
    ULONG memory_size);
```

### <a name="description"></a><span data-ttu-id="36624-1600">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1600">Description</span></span>

<span data-ttu-id="36624-1601">Bu hizmet, Kullanıcı tarafından sağlanan bellek alanında belirtilen paket boyutunun bir paket havuzunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="36624-1601">This service creates a packet pool of the specified packet size in the memory area supplied by the user.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1602">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1602">Parameters</span></span>

- <span data-ttu-id="36624-1603">**pool_ptr** Paket havuzu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1603">**pool_ptr** Pointer to packet pool control block.</span></span>
- <span data-ttu-id="36624-1604">**ad** Paket havuzu için uygulama adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1604">**name** Pointer to application’s name for the packet pool.</span></span>
- <span data-ttu-id="36624-1605">**payload_size** Havuzdaki her paketteki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="36624-1605">**payload_size** Number of bytes in each packet in the pool.</span></span> <span data-ttu-id="36624-1606">Bu değer en az 40 bayt olmalıdır ve ayrıca 4 ile eşit olarak bölünebilmelidir.</span><span class="sxs-lookup"><span data-stu-id="36624-1606">This value must be at least 40 bytes and must also be evenly divisible by 4.</span></span>
- <span data-ttu-id="36624-1607">**memory_ptr** Paket havuzunun yerleştirileceği bellek alanına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1607">**memory_ptr** Pointer to the memory area to place the packet pool in.</span></span> <span data-ttu-id="36624-1608">İşaretçi bir ULONG sınırında hizalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-1608">The pointer should be aligned on an ULONG boundary.</span></span>
- <span data-ttu-id="36624-1609">**memory_size** Havuz belleği alanının boyutu.</span><span class="sxs-lookup"><span data-stu-id="36624-1609">**memory_size** Size of the pool memory area.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1610">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1610">Return Values</span></span>

- <span data-ttu-id="36624-1611">**NX_SUCCESS** (0x00) başarılı paket havuzu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="36624-1611">**NX_SUCCESS** (0x00) Successful packet pool create.</span></span>
- <span data-ttu-id="36624-1612">**NX_PTR_ERROR** (0x07) geçersiz havuz veya bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1612">**NX_PTR_ERROR** (0x07) Invalid pool or memory pointer.</span></span>
- <span data-ttu-id="36624-1613">**NX_SIZE_ERROR** (0x09) geçersiz blok veya bellek boyutu.</span><span class="sxs-lookup"><span data-stu-id="36624-1613">**NX_SIZE_ERROR** (0x09) Invalid block or memory size.</span></span>
- <span data-ttu-id="36624-1614">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1614">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1615">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1615">Allowed From</span></span>

<span data-ttu-id="36624-1616">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1616">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1617">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1617">Preemption Possible</span></span>

<span data-ttu-id="36624-1618">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1618">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1619">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1619">Example</span></span>

```C
/* Create a packet pool of 32000 bytes starting at physical
    address 0x10000000. */
status = nx_packet_pool_create(&pool_0, "Default Pool", 128,
    (void *) 0x10000000, 32000);

/* If status is NX_SUCCESS, the packet pool has been successfully
    created. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1620">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1620">See Also</span></span>

- <span data-ttu-id="36624-1621">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1621">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1622">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="36624-1622">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="36624-1623">nx_packet_length_get, nx_packet_pool_delete, nx_packet_pool_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-1623">nx_packet_length_get, nx_packet_pool_delete, nx_packet_pool_info_get,</span></span>
- <span data-ttu-id="36624-1624">nx_packet_release, nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1624">nx_packet_release, nx_packet_transmit_release</span></span>

## <a name="nx_packet_pool_delete"></a><span data-ttu-id="36624-1625">nx_packet_pool_delete</span><span class="sxs-lookup"><span data-stu-id="36624-1625">nx_packet_pool_delete</span></span>

<span data-ttu-id="36624-1626">Önceden oluşturulmuş paket havuzunu Sil</span><span class="sxs-lookup"><span data-stu-id="36624-1626">Delete previously created packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1627">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1627">Prototype</span></span>

```C
UINT nx_packet_pool_delete(NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1628">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1628">Description</span></span>

<span data-ttu-id="36624-1629">Bu hizmet, önceden oluşturulmuş bir paket havuzunu siler.</span><span class="sxs-lookup"><span data-stu-id="36624-1629">This service deletes a previously-created packet pool.</span></span> <span data-ttu-id="36624-1630">NetX, paket havuzundaki paketlerde Şu anda askıya alınmış olan her iş parçacığını denetler ve askıya alınma 'yi temizler.</span><span class="sxs-lookup"><span data-stu-id="36624-1630">NetX checks for any threads currently suspended on packets in the packet pool and clears the suspension.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1631">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1631">Parameters</span></span>

- <span data-ttu-id="36624-1632">**pool_ptr** Paket havuzu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1632">**pool_ptr** Packet pool control block pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1633">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1633">Return Values</span></span>

- <span data-ttu-id="36624-1634">**NX_SUCCESS** (0x00) başarılı paket havuzu silme.</span><span class="sxs-lookup"><span data-stu-id="36624-1634">**NX_SUCCESS** (0x00) Successful packet pool delete.</span></span>
- <span data-ttu-id="36624-1635">**NX_PTR_ERROR** (0x07) geçersiz havuz işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1635">**NX_PTR_ERROR** (0x07) Invalid pool pointer.</span></span>
- <span data-ttu-id="36624-1636">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1636">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1637">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1637">Allowed From</span></span>

<span data-ttu-id="36624-1638">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1638">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1639">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1639">Preemption Possible</span></span>

<span data-ttu-id="36624-1640">Yes</span><span class="sxs-lookup"><span data-stu-id="36624-1640">Yes</span></span>

### <a name="example"></a><span data-ttu-id="36624-1641">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1641">Example</span></span>

```C
/* Delete a previously created packet pool. */
status = nx_packet_pool_delete(&pool_0);

/* If status is NX_SUCCESS, the packet pool has been successfully
    deleted. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1642">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1642">See Also</span></span>

- <span data-ttu-id="36624-1643">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1643">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1644">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="36624-1644">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="36624-1645">nx_packet_length_get, nx_packet_pool_create,</span><span class="sxs-lookup"><span data-stu-id="36624-1645">nx_packet_length_get, nx_packet_pool_create,</span></span>
- <span data-ttu-id="36624-1646">nx_packet_pool_info_get, nx_packet_release,</span><span class="sxs-lookup"><span data-stu-id="36624-1646">nx_packet_pool_info_get, nx_packet_release,</span></span>
- <span data-ttu-id="36624-1647">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1647">nx_packet_transmit_release</span></span>

## <a name="nx_packet_pool_info_get"></a><span data-ttu-id="36624-1648">nx_packet_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-1648">nx_packet_pool_info_get</span></span>

<span data-ttu-id="36624-1649">Bir paket havuzu hakkında bilgi alma</span><span class="sxs-lookup"><span data-stu-id="36624-1649">Retrieve information about a packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1650">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1650">Prototype</span></span>

```C
UINT nx_packet_pool_info_get(
    NX_PACKET_POOL *pool_ptr,
    ULONG *total_packets,
    ULONG *free_packets,
    ULONG *empty_pool_requests,
    ULONG *empty_pool_suspensions,
    ULONG *invalid_packet_releases);
```

### <a name="description"></a><span data-ttu-id="36624-1651">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1651">Description</span></span>

<span data-ttu-id="36624-1652">Bu hizmet, belirtilen paket havuzu hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-1652">This service retrieves information about the specified packet pool.</span></span>

<span data-ttu-id="36624-1653">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-1653">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1654">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1654">Parameters</span></span>

- <span data-ttu-id="36624-1655">**pool_ptr** Daha önce oluşturulan paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1655">**pool_ptr** Pointer to previously created packet pool.</span></span>
- <span data-ttu-id="36624-1656">**total_packets** Havuzdaki toplam paket sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1656">**total_packets** Pointer to destination for the total number of packets in the pool.</span></span>
- <span data-ttu-id="36624-1657">**free_packets** Şu anda boş olan paketlerin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1657">**free_packets** Pointer to destination for the total number of currently free packets.</span></span>
- <span data-ttu-id="36624-1658">**empty_pool_requests** Havuz boş olduğunda toplam ayırma isteği sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1658">**empty_pool_requests** Pointer to destination of the total number of allocation requests when the pool was empty.</span></span>
- <span data-ttu-id="36624-1659">**empty_pool_suspensions** Boş havuz getirilmesi toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1659">**empty_pool_suspensions** Pointer to destination of the total number of empty pool suspensions.</span></span>
- <span data-ttu-id="36624-1660">**invalid_packet_releases** Toplam geçersiz paket sürümü sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1660">**invalid_packet_releases** Pointer to destination of the total number of invalid packet releases.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1661">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1661">Return Values</span></span>

- <span data-ttu-id="36624-1662">**NX_SUCCESS** (0x00) başarılı paket havuzu bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="36624-1662">**NX_SUCCESS** (0x00) Successful packet pool information retrieval.</span></span>
- <span data-ttu-id="36624-1663">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1663">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-1664">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1664">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1665">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1665">Allowed From</span></span>

<span data-ttu-id="36624-1666">Başlatma, iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="36624-1666">Initialization, threads, and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1667">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1667">Preemption Possible</span></span>

<span data-ttu-id="36624-1668">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1668">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1669">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1669">Example</span></span>

```C
/* Retrieve packet pool information. */
status = nx_packet_pool_info_get(&pool_0,
    &total_packets,
    &free_packets,
    &empty_pool_requests,
    &empty_pool_suspensions,
    &invalid_packet_releases);

/* If status is NX_SUCCESS, packet pool information was
    retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1670">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1670">See Also</span></span>

- <span data-ttu-id="36624-1671">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1671">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1672">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="36624-1672">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="36624-1673">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete</span><span class="sxs-lookup"><span data-stu-id="36624-1673">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete</span></span>
- <span data-ttu-id="36624-1674">nx_packet_release, nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1674">nx_packet_release, nx_packet_transmit_release</span></span>

## <a name="nx_packet_release"></a><span data-ttu-id="36624-1675">nx_packet_release</span><span class="sxs-lookup"><span data-stu-id="36624-1675">nx_packet_release</span></span>

<span data-ttu-id="36624-1676">Önceden ayrılmış paketi serbest bırak</span><span class="sxs-lookup"><span data-stu-id="36624-1676">Release previously allocated packet</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1677">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1677">Prototype</span></span>

```C
UINT nx_packet_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1678">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1678">Description</span></span>

<span data-ttu-id="36624-1679">Bu hizmet, belirtilen pakete zincirleme ek paketler de dahil olmak üzere bir paket yayınlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1679">This service releases a packet, including any additional packets chained to the specified packet.</span></span> <span data-ttu-id="36624-1680">Paket ayırma üzerinde başka bir iş parçacığı engellenirse, paket verilir ve sürdürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-1680">If another thread is blocked on packet allocation, it is given the packet and resumed.</span></span>

<span data-ttu-id="36624-1681">*Uygulamanın, bir paketin birden çok kez serbest bırakılmasını önlemesi gerekir, çünkü bunu yapmak öngörülemeyen sonuçlara neden olur.*</span><span class="sxs-lookup"><span data-stu-id="36624-1681">*The application must prevent releasing a packet more than once, because doing so will cause unpredictable results.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1682">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1682">Parameters</span></span>

- <span data-ttu-id="36624-1683">**packet_ptr** Paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1683">**packet_ptr** Packet pointer.</span></span>


### <a name="return-values"></a><span data-ttu-id="36624-1684">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1684">Return Values</span></span>
- <span data-ttu-id="36624-1685">**NX_SUCCESS** (0x00) başarılı paket sürümü.</span><span class="sxs-lookup"><span data-stu-id="36624-1685">**NX_SUCCESS** (0x00) Successful packet release.</span></span>
- <span data-ttu-id="36624-1686">**NX_PTR_ERROR** (0x07) geçersiz paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1686">**NX_PTR_ERROR** (0x07) Invalid packet pointer.</span></span>
- <span data-ttu-id="36624-1687">**NX_UNDERFLOW** (0x02) Prepend işaretçisi yük başlangıcından daha küçüktür.</span><span class="sxs-lookup"><span data-stu-id="36624-1687">**NX_UNDERFLOW** (0x02) Prepend pointer is less than payload start.</span></span>
- <span data-ttu-id="36624-1688">**NX_OVERFLOW** (0x03) ekleme işaretçisi yük ucundan daha büyük.</span><span class="sxs-lookup"><span data-stu-id="36624-1688">**NX_OVERFLOW** (0x03) Append pointer is greater than payload end.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1689">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1689">Allowed From</span></span>

<span data-ttu-id="36624-1690">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs (uygulama ağ sürücüleri)</span><span class="sxs-lookup"><span data-stu-id="36624-1690">Initialization, threads, timers, and ISRs (application network drivers)</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1691">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1691">Preemption Possible</span></span>

<span data-ttu-id="36624-1692">Yes</span><span class="sxs-lookup"><span data-stu-id="36624-1692">Yes</span></span>

### <a name="example"></a><span data-ttu-id="36624-1693">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1693">Example</span></span>

```C
/* Release a previously allocated packet. */
status = nx_packet_release(packet_ptr);

/* If status is NX_SUCCESS, the packet has been returned to the
    packet pool it was allocated from. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1694">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1694">See Also</span></span>

- <span data-ttu-id="36624-1695">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1695">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1696">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="36624-1696">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="36624-1697">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-1697">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="36624-1698">nx_packet_pool_info_get, nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1698">nx_packet_pool_info_get, nx_packet_transmit_release</span></span>

## <a name="nx_packet_transmit_release"></a><span data-ttu-id="36624-1699">nx_packet_transmit_release</span><span class="sxs-lookup"><span data-stu-id="36624-1699">nx_packet_transmit_release</span></span>

<span data-ttu-id="36624-1700">İletilen bir paketi serbest bırakma</span><span class="sxs-lookup"><span data-stu-id="36624-1700">Release a transmitted packet</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1701">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1701">Prototype</span></span>

```C
UINT nx_packet_transmit_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1702">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1702">Description</span></span>

<span data-ttu-id="36624-1703">Bu hizmet, TCP olmayan paketler için, belirtilen pakete zincirleme ek paketler de dahil olmak üzere, iletilen bir paket yayınlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1703">For non-TCP packets, this service releases a transmitted packet, including any additional packets chained to the specified packet.</span></span> <span data-ttu-id="36624-1704">Paket ayırma üzerinde başka bir iş parçacığı engellenirse, paket verilir ve sürdürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-1704">If another thread is blocked on packet allocation, it is given the packet and resumed.</span></span> <span data-ttu-id="36624-1705">İletilen bir TCP paketi için paket aktarılmakta olarak işaretlenir ancak paket onaylanana kadar serbest bırakılmaz.</span><span class="sxs-lookup"><span data-stu-id="36624-1705">For a transmitted TCP packet, the packet is marked as being transmitted but not released till the packet is acknowledged.</span></span> <span data-ttu-id="36624-1706">Bu hizmet genellikle bir paket iletildikten sonra uygulamanın ağ sürücüsünden çağrılır.</span><span class="sxs-lookup"><span data-stu-id="36624-1706">This service is typically called from the application's network driver after a packet is transmitted.</span></span>

<span data-ttu-id="36624-1707">*Ağ sürücüsünün fiziksel medya üstbilgisini kaldırması ve bu hizmeti çağırmadan önce paketin uzunluğunu ayarlaması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="36624-1707">*The network driver should remove the physical media header and adjust the length of the packet before calling this service.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1708">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1708">Parameters</span></span>

- <span data-ttu-id="36624-1709">**packet_ptr** Paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1709">**packet_ptr** Packet pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1710">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1710">Return Values</span></span>

- <span data-ttu-id="36624-1711">**NX_SUCCESS** (0x00) başarılı iletme paketi sürümü.</span><span class="sxs-lookup"><span data-stu-id="36624-1711">**NX_SUCCESS** (0x00) Successful transmit packet release.</span></span>
- <span data-ttu-id="36624-1712">**NX_PTR_ERROR** (0x07) geçersiz paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1712">**NX_PTR_ERROR** (0x07) Invalid packet pointer.</span></span>
- <span data-ttu-id="36624-1713">**NX_UNDERFLOW** (0x02) Prepend işaretçisi yük başlangıcından daha küçüktür.</span><span class="sxs-lookup"><span data-stu-id="36624-1713">**NX_UNDERFLOW** (0x02) Prepend pointer is less than payload start.</span></span>
- <span data-ttu-id="36624-1714">**NX_OVERFLOW** (0x03) ekleme işaretçisi yük ucundan daha büyük.</span><span class="sxs-lookup"><span data-stu-id="36624-1714">**NX_OVERFLOW** (0x03) Append pointer is greater than payload end.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1715">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1715">Allowed From</span></span>

<span data-ttu-id="36624-1716">Başlatma, iş parçacıkları, zamanlayıcılar, uygulama ağ sürücüleri (ISRS dahil)</span><span class="sxs-lookup"><span data-stu-id="36624-1716">Initialization, threads, timers, Application network drivers (including ISRs)</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1717">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1717">Preemption Possible</span></span>

<span data-ttu-id="36624-1718">Yes</span><span class="sxs-lookup"><span data-stu-id="36624-1718">Yes</span></span>

### <a name="example"></a><span data-ttu-id="36624-1719">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1719">Example</span></span>

```C
/* Release a previously allocated packet that was just transmitted
    from the application network driver. */
status = nx_packet_transmit_release(packet_ptr);

/* If status is NX_SUCCESS, the transmitted packet has been
    returned to the packet pool it was allocated from. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1720">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1720">See Also</span></span>

- <span data-ttu-id="36624-1721">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span><span class="sxs-lookup"><span data-stu-id="36624-1721">nx_packet_allocate, nx_packet_copy, nx_packet_data_append,</span></span>
- <span data-ttu-id="36624-1722">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span><span class="sxs-lookup"><span data-stu-id="36624-1722">nx_packet_data_extract_offset, nx_packet_data_retrieve,</span></span>
- <span data-ttu-id="36624-1723">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-1723">nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,</span></span>
- <span data-ttu-id="36624-1724">nx_packet_pool_info_get, nx_packet_release</span><span class="sxs-lookup"><span data-stu-id="36624-1724">nx_packet_pool_info_get, nx_packet_release</span></span>

## <a name="nx_rarp_disable"></a><span data-ttu-id="36624-1725">nx_rarp_disable</span><span class="sxs-lookup"><span data-stu-id="36624-1725">nx_rarp_disable</span></span>

<span data-ttu-id="36624-1726">Ters adres çözümleme protokolünü devre dışı bırak (RARP)</span><span class="sxs-lookup"><span data-stu-id="36624-1726">Disable Reverse Address Resolution Protocol (RARP)</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1727">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1727">Prototype</span></span>

```C
UINT nx_rarp_disable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1728">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1728">Description</span></span>

<span data-ttu-id="36624-1729">Bu hizmet, belirli IP örneği için NetX 'in RARP bileşenini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="36624-1729">This service disables the RARP component of NetX for the specific IP instance.</span></span> <span data-ttu-id="36624-1730">Bu hizmet, çok ana bir sistem için tüm arabirimlerde RARP 'yi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="36624-1730">For a multihome system, this service disables RARP on all interfaces.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1731">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1731">Parameters</span></span>

- <span data-ttu-id="36624-1732">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1732">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1733">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1733">Return Values</span></span>

- <span data-ttu-id="36624-1734">**NX_SUCCESS** (0x00) başarılı RARP devre dışı.</span><span class="sxs-lookup"><span data-stu-id="36624-1734">**NX_SUCCESS** (0x00) Successful RARP disable.</span></span>
- <span data-ttu-id="36624-1735">**NX_NOT_ENABLED** (0x14) RARP etkin değildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1735">**NX_NOT_ENABLED** (0x14) RARP was not enabled.</span></span>
- <span data-ttu-id="36624-1736">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1736">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-1737">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1737">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1738">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1738">Allowed From</span></span>

<span data-ttu-id="36624-1739">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1739">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1740">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1740">Preemption Possible</span></span>

<span data-ttu-id="36624-1741">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1741">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1742">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1742">Example</span></span>

```C
/* Disable RARP on the previously created IP instance. */
status = nx_rarp_disable(&ip_0);

/* If status is NX_SUCCESS, RARP is disabled. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1743">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1743">See Also</span></span>

- <span data-ttu-id="36624-1744">nx_rarp_enable, nx_rarp_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-1744">nx_rarp_enable, nx_rarp_info_get</span></span>

## <a name="nx_rarp_enable"></a><span data-ttu-id="36624-1745">nx_rarp_enable</span><span class="sxs-lookup"><span data-stu-id="36624-1745">nx_rarp_enable</span></span>

<span data-ttu-id="36624-1746">Ters adres çözümleme protokolünü etkinleştir (RARP)</span><span class="sxs-lookup"><span data-stu-id="36624-1746">Enable Reverse Address Resolution Protocol (RARP)</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1747">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1747">Prototype</span></span>

```C
UINT nx_rarp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1748">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1748">Description</span></span>

<span data-ttu-id="36624-1749">Bu hizmet, belirli IP örneği için NetX 'in RARP bileşenini sunar.</span><span class="sxs-lookup"><span data-stu-id="36624-1749">This service enables the RARP component of NetX for the specific IP instance.</span></span> <span data-ttu-id="36624-1750">RARP bileşenleri, sıfır IP adresi için tüm bağlı ağ arabirimlerini arar.</span><span class="sxs-lookup"><span data-stu-id="36624-1750">The RARP components searches through all attached network interfaces for zero IP address.</span></span> <span data-ttu-id="36624-1751">Sıfır IP adresi, arabirimin henüz IP adresi ataması olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="36624-1751">A zero IP address indicates the interface does not have IP address assignment yet.</span></span> <span data-ttu-id="36624-1752">RARP, bu arabirimde RARP işlemini etkinleştirerek IP adresini çözümlemeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="36624-1752">RARP attempts to resolve the IP address by enabling RARP process on that interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1753">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1753">Parameters</span></span>

- <span data-ttu-id="36624-1754">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1754">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1755">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1755">Return Values</span></span>

- <span data-ttu-id="36624-1756">**NX_SUCCESS** (0x00) başarılı RARP etkinleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="36624-1756">**NX_SUCCESS** (0x00) Successful RARP enable.</span></span>
- <span data-ttu-id="36624-1757">**NX_IP_ADDRESS_ERROR** (0x21) IP adresi zaten geçerli.</span><span class="sxs-lookup"><span data-stu-id="36624-1757">**NX_IP_ADDRESS_ERROR** (0x21) IP address is already valid.</span></span>
- <span data-ttu-id="36624-1758">**NX_ALREADY_ENABLED** (0x15) RARP zaten etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-1758">**NX_ALREADY_ENABLED** (0x15) RARP was already enabled.</span></span>
- <span data-ttu-id="36624-1759">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1759">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-1760">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1760">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1761">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1761">Allowed From</span></span>

<span data-ttu-id="36624-1762">Başlatma, iş parçacıkları, zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="36624-1762">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1763">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1763">Preemption Possible</span></span>

<span data-ttu-id="36624-1764">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1764">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1765">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1765">Example</span></span>

```C
/* Enable RARP on the previously created IP instance. */
status = nx_rarp_enable(&ip_0);

/* If status is NX_SUCCESS, RARP is enabled and is attempting to
    resolve this IP instance’s address by querying the network. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1766">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1766">See Also</span></span>

- <span data-ttu-id="36624-1767">nx_rarp_disable, nx_rarp_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-1767">nx_rarp_disable, nx_rarp_info_get</span></span>

## <a name="nx_rarp_info_get"></a><span data-ttu-id="36624-1768">nx_rarp_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-1768">nx_rarp_info_get</span></span>

<span data-ttu-id="36624-1769">RARP etkinlikleri hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="36624-1769">Retrieve information about RARP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1770">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1770">Prototype</span></span>

```C
UINT nx_rarp_info_get(
    NX_IP *ip_ptr,
    ULONG *rarp_requests_sent,
    ULONG *rarp_responses_received,
    ULONG *rarp_invalid_messages);
```

### <a name="description"></a><span data-ttu-id="36624-1771">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1771">Description</span></span>

<span data-ttu-id="36624-1772">Bu hizmet, belirtilen IP örneği için RARP etkinlikleriyle ilgili bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="36624-1772">This service retrieves information about RARP activities for the specified IP instance.</span></span>

<span data-ttu-id="36624-1773">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-1773">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1774">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1774">Parameters</span></span>

- <span data-ttu-id="36624-1775">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1775">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1776">**rarp_requests_sent** Gönderilen toplam RARP isteği sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1776">**rarp_requests_sent** Pointer to destination for the total number of RARP requests sent.</span></span>
- <span data-ttu-id="36624-1777">**rarp_responses_received** Alınan toplam RARP yanıtı sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1777">**rarp_responses_received** Pointer to destination for the total number of RARP responses received.</span></span>
- <span data-ttu-id="36624-1778">**rarp_invalid_messages** Toplam geçersiz ileti sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1778">**rarp_invalid_messages** Pointer to destination of the total number of invalid messages.</span></span>


### <a name="return-values"></a><span data-ttu-id="36624-1779">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1779">Return Values</span></span>
- <span data-ttu-id="36624-1780">**NX_SUCCESS** (0x00) başarılı bir RARP bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="36624-1780">**NX_SUCCESS** (0x00) Successful RARP information retrieval.</span></span>
- <span data-ttu-id="36624-1781">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1781">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-1782">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-1782">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-1783">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1783">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1784">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1784">Allowed From</span></span>

<span data-ttu-id="36624-1785">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1785">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1786">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1786">Preemption Possible</span></span>

<span data-ttu-id="36624-1787">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1787">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1788">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1788">Example</span></span>

```C
/* Retrieve RARP information from previously created IP
    Instance 0. */
status = nx_rarp_info_get(&ip_0,
    &rarp_requests_sent,
    &rarp_responses_received,
    &rarp_invalid_messages);

/* If status is NX_SUCCESS, RARP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1789">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1789">See Also</span></span>

- <span data-ttu-id="36624-1790">nx_rarp_disable, nx_rarp_enable</span><span class="sxs-lookup"><span data-stu-id="36624-1790">nx_rarp_disable, nx_rarp_enable</span></span>

## <a name="nx_system_initialize"></a><span data-ttu-id="36624-1791">nx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="36624-1791">nx_system_initialize</span></span>

<span data-ttu-id="36624-1792">NetX sistemini Başlat</span><span class="sxs-lookup"><span data-stu-id="36624-1792">Initialize NetX System</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1793">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1793">Prototype</span></span>

```C
VOID nx_system_initialize(VOID);
```

### <a name="description"></a><span data-ttu-id="36624-1794">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1794">Description</span></span>

<span data-ttu-id="36624-1795">Bu hizmet, kullanıma hazırlık aşamasında temel NetX sistem kaynaklarını başlatır.</span><span class="sxs-lookup"><span data-stu-id="36624-1795">This service initializes the basic NetX system resources in preparation for use.</span></span> <span data-ttu-id="36624-1796">Başlatma sırasında ve diğer bir NetX çağrısının yapılabilmesi için uygulama tarafından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-1796">It should be called by the application during initialization and before any other NetX call are made.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1797">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1797">Parameters</span></span>

<span data-ttu-id="36624-1798">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="36624-1798">None</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1799">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1799">Return Values</span></span>

<span data-ttu-id="36624-1800">Yok</span><span class="sxs-lookup"><span data-stu-id="36624-1800">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1801">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1801">Allowed From</span></span>

<span data-ttu-id="36624-1802">Başlatma, iş parçacıkları, zamanlayıcılar, ISRs</span><span class="sxs-lookup"><span data-stu-id="36624-1802">Initialization, threads, timers, ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1803">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1803">Preemption Possible</span></span>

<span data-ttu-id="36624-1804">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1804">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1805">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1805">Example</span></span>

```C
/* Initialize NetX for operation. */
nx_system_initialize();

/* At this point, NetX is ready for IP creation and all subsequent
    network operations. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1806">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1806">See Also</span></span>

- <span data-ttu-id="36624-1807">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span><span class="sxs-lookup"><span data-stu-id="36624-1807">nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,</span></span>
- <span data-ttu-id="36624-1808">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span><span class="sxs-lookup"><span data-stu-id="36624-1808">nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,</span></span>
- <span data-ttu-id="36624-1809">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-1809">nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,</span></span>
- <span data-ttu-id="36624-1810">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-1810">nx_ip_forwarding_enable, nx_ip_fragment_disable,</span></span>
- <span data-ttu-id="36624-1811">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check</span><span class="sxs-lookup"><span data-stu-id="36624-1811">nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check</span></span>

## <a name="nx_tcp_client_socket_bind"></a><span data-ttu-id="36624-1812">nx_tcp_client_socket_bind</span><span class="sxs-lookup"><span data-stu-id="36624-1812">nx_tcp_client_socket_bind</span></span>

<span data-ttu-id="36624-1813">İstemci TCP yuvasını TCP bağlantı noktasına bağlama</span><span class="sxs-lookup"><span data-stu-id="36624-1813">Bind client TCP socket to TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1814">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1814">Prototype</span></span>

```C
UINT nx_tcp_client_socket_bind(
    NX_TCP_SOCKET *socket_ptr,
    UINT port, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-1815">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1815">Description</span></span>

<span data-ttu-id="36624-1816">Bu hizmet, önceden oluşturulan TCP istemci yuvasını belirtilen TCP bağlantı noktasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1816">This service binds the previously created TCP client socket to the specified TCP port.</span></span> <span data-ttu-id="36624-1817">Geçerli TCP Yuvaları 0 ile 0xFFFF arasındadır.</span><span class="sxs-lookup"><span data-stu-id="36624-1817">Valid TCP sockets range from 0 through 0xFFFF.</span></span> <span data-ttu-id="36624-1818">Belirtilen TCP bağlantı noktası kullanılamıyorsa, hizmet sağlanan bekleme seçeneğine göre askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="36624-1818">If the specified TCP port is unavailable, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1819">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1819">Parameters</span></span>

- <span data-ttu-id="36624-1820">**socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1820">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="36624-1821">**bağlantı noktası** Bağlanacak bağlantı noktası numarası (1 ile 0xFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="36624-1821">**port** Port number to bind (1 through 0xFFFF).</span></span> <span data-ttu-id="36624-1822">Bağlantı noktası numarası NX_ANY_PORT (0x0000) ise, IP örneği bir sonraki boş bağlantı noktasını arar ve bu bağlantıyı bağlama için kullanır.</span><span class="sxs-lookup"><span data-stu-id="36624-1822">If port number is NX_ANY_PORT (0x0000), the IP instance will search for the next free port and use that for the binding.</span></span>
- <span data-ttu-id="36624-1823">**wait_option** Bağlantı noktası zaten başka bir yuvaya bağlanmışsa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1823">**wait_option** Defines how the service behaves if the port is already bound to another socket.</span></span> <span data-ttu-id="36624-1824">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-1824">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-1825">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-1825">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-1826">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-1826">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-1827">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-1827">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1828">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1828">Return Values</span></span>

- <span data-ttu-id="36624-1829">**NX_SUCCESS** (0x00) başarılı yuva bağlaması.</span><span class="sxs-lookup"><span data-stu-id="36624-1829">**NX_SUCCESS** (0x00) Successful socket bind.</span></span>
- <span data-ttu-id="36624-1830">**NX_ALREADY_BOUND** (0x22) bu yuva zaten başka bir TCP bağlantı noktasına bağlıydı.</span><span class="sxs-lookup"><span data-stu-id="36624-1830">**NX_ALREADY_BOUND** (0x22) This socket is already bound to another TCP port.</span></span>
- <span data-ttu-id="36624-1831">**NX_PORT_UNAVAILABLE** (0x23) bağlantı noktası zaten farklı bir yuvaya bağlıydı.</span><span class="sxs-lookup"><span data-stu-id="36624-1831">**NX_PORT_UNAVAILABLE** (0x23) Port is already bound to a different socket.</span></span>
- <span data-ttu-id="36624-1832">**NX_NO_FREE_PORTS** (0x45) boş bağlantı noktası yok.</span><span class="sxs-lookup"><span data-stu-id="36624-1832">**NX_NO_FREE_PORTS** (0x45) No free port.</span></span>
- <span data-ttu-id="36624-1833">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği *tx_thread_wait_abort* bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1833">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="36624-1834">**NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="36624-1834">**NX_INVALID_PORT** (0x46) Invalid port.</span></span>
- <span data-ttu-id="36624-1835">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1835">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-1836">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1836">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1837">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-1837">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1838">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1838">Allowed From</span></span>

<span data-ttu-id="36624-1839">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1839">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1840">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1840">Preemption Possible</span></span>

<span data-ttu-id="36624-1841">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1841">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1842">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1842">Example</span></span>

```C
/* Bind a previously created client socket to port 12 and wait for 7
    timer ticks for the bind to complete. */
status = nx_tcp_client_socket_bind(&client_socket, 12, 7);

/* If status is NX_SUCCESS, the previously created client_socket is
    bound to port 12 on the associated IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1843">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1843">See Also</span></span>

- <span data-ttu-id="36624-1844">nx_tcp_client_socket_connect, nx_tcp_client_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="36624-1844">nx_tcp_client_socket_connect, nx_tcp_client_socket_port_get,</span></span>
- <span data-ttu-id="36624-1845">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span><span class="sxs-lookup"><span data-stu-id="36624-1845">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span></span>
- <span data-ttu-id="36624-1846">nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="36624-1846">nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="36624-1847">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1847">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-1848">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1848">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-1849">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-1849">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-1850">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-1850">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-1851">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-1851">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-1852">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-1852">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-1853">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-1853">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_client_socket_connect"></a><span data-ttu-id="36624-1854">nx_tcp_client_socket_connect</span><span class="sxs-lookup"><span data-stu-id="36624-1854">nx_tcp_client_socket_connect</span></span>

<span data-ttu-id="36624-1855">İstemci TCP yuvasını bağlama</span><span class="sxs-lookup"><span data-stu-id="36624-1855">Connect client TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1856">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1856">Prototype</span></span>

```C
UINT nx_tcp_client_socket_connect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG server_ip,
    UINT server_port,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-1857">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1857">Description</span></span>

<span data-ttu-id="36624-1858">Bu hizmet, önceden oluşturulmuş ve bağlı TCP istemci yuvasını belirtilen sunucunun bağlantı noktasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1858">This service connects the previously-created and bound TCP client socket to the specified server's port.</span></span> <span data-ttu-id="36624-1859">Geçerli TCP sunucusu bağlantı noktaları 0 ile 0xFFFF arasındadır.</span><span class="sxs-lookup"><span data-stu-id="36624-1859">Valid TCP server ports range from 0 through 0xFFFF.</span></span> <span data-ttu-id="36624-1860">Bağlantı hemen tamamlanmazsa, hizmet sağlanan bekleme seçeneğine göre askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="36624-1860">If the connection does not complete immediately, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1861">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1861">Parameters</span></span>

- <span data-ttu-id="36624-1862">**socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1862">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="36624-1863">**server_ip** Sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-1863">**server_ip** Server’s IP address.</span></span>
- <span data-ttu-id="36624-1864">**SERVER_PORT** Bağlanılacak sunucu bağlantı noktası numarası (1 ile 0xFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="36624-1864">**server_port** Server port number to connect to (1 through 0xFFFF).</span></span>
- <span data-ttu-id="36624-1865">**wait_option** Bağlantı kurulurken hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1865">**wait_option** Defines how the service behaves while the connection is being established.</span></span> <span data-ttu-id="36624-1866">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-1866">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-1867">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-1867">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-1868">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-1868">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-1869">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-1869">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1870">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1870">Return Values</span></span>

- <span data-ttu-id="36624-1871">**NX_SUCCESS** (0x00) başarılı yuva bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="36624-1871">**NX_SUCCESS** (0x00) Successful socket connect.</span></span>
- <span data-ttu-id="36624-1872">**NX_NOT_BOUND** (0x24) yuva bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-1872">**NX_NOT_BOUND** (0x24) Socket is not bound.</span></span>
- <span data-ttu-id="36624-1873">**NX_NOT_CLOSED** (0x35) yuva kapalı durumda değil.</span><span class="sxs-lookup"><span data-stu-id="36624-1873">**NX_NOT_CLOSED** (0x35) Socket is not in a closed state.</span></span>
- <span data-ttu-id="36624-1874">**NX_IN_PROGRESS** (0x37) bekleme belirtilmedi, bağlantı girişimi devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="36624-1874">**NX_IN_PROGRESS** (0x37) No wait was specified, the connection attempt is in progress.</span></span>
- <span data-ttu-id="36624-1875">**NX_INVALID_INTERFACE** (0x4C) geçersiz arabirim sağlandı.</span><span class="sxs-lookup"><span data-stu-id="36624-1875">**NX_INVALID_INTERFACE** (0x4C) Invalid interface supplied.</span></span>
- <span data-ttu-id="36624-1876">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-1876">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-1877">**NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ sunucu IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-1877">**NX_IP_ADDRESS_ERROR** (0x21) Invalid server IP address.</span></span>
- <span data-ttu-id="36624-1878">**NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="36624-1878">**NX_INVALID_PORT** (0x46) Invalid port.</span></span>
- <span data-ttu-id="36624-1879">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1879">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-1880">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1880">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1881">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-1881">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1882">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1882">Allowed From</span></span>

<span data-ttu-id="36624-1883">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1883">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1884">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1884">Preemption Possible</span></span>

<span data-ttu-id="36624-1885">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1885">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1886">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1886">Example</span></span>

```C
/* Initiate a TCP connection from a previously created and bound
    client socket. The connection requested in this example is to
    port 12 on the server with the IP address of 1.2.3.5. This
    service will wait 300 timer ticks for the connection to take
    place before giving up. */
status = nx_tcp_client_socket_connect(&client_socket,
    IP_ADDRESS(1,2,3,5), 12, 300);

/* If status is NX_SUCCESS, the previously created and bound
    client_socket is connected to port 12 on IP 1.2.3.5. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1887">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1887">See Also</span></span>

- <span data-ttu-id="36624-1888">nx_tcp_client_socket_bind, nx_tcp_client_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="36624-1888">nx_tcp_client_socket_bind, nx_tcp_client_socket_port_get,</span></span>
- <span data-ttu-id="36624-1889">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span><span class="sxs-lookup"><span data-stu-id="36624-1889">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span></span>
- <span data-ttu-id="36624-1890">nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="36624-1890">nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="36624-1891">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1891">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-1892">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1892">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-1893">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-1893">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-1894">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-1894">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-1895">nx_tcp_socket_info_get, nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="36624-1895">nx_tcp_socket_info_get, nx_tcp_socket_receive</span></span>
- <span data-ttu-id="36624-1896">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-1896">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-1897">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-1897">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_client_socket_port_get"></a><span data-ttu-id="36624-1898">nx_tcp_client_socket_port_get</span><span class="sxs-lookup"><span data-stu-id="36624-1898">nx_tcp_client_socket_port_get</span></span>

<span data-ttu-id="36624-1899">İstemci TCP yuvasına bağlantı noktası numarasını al</span><span class="sxs-lookup"><span data-stu-id="36624-1899">Get port number bound to client TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1900">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1900">Prototype</span></span>

```C
UINT nx_tcp_client_socket_port_get(
    NX_TCP_SOCKET *socket_ptr,
    UINT *port_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1901">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1901">Description</span></span>

<span data-ttu-id="36624-1902">Bu hizmet, yuvanın bağlandığı zamanda NX_ANY_PORT belirtildiği durumlarda NetX tarafından ayrılan bağlantı noktasını bulmak için yararlı olan yuva ile ilişkili bağlantı noktası numarasını alır.</span><span class="sxs-lookup"><span data-stu-id="36624-1902">This service retrieves the port number associated with the socket, which is useful to find the port allocated by NetX in situations where the NX_ANY_PORT was specified at the time the socket was bound.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1903">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1903">Parameters</span></span>

- <span data-ttu-id="36624-1904">**socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1904">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="36624-1905">**port_ptr** Dönüş bağlantı noktası numarası için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1905">**port_ptr** Pointer to destination for the return port number.</span></span> <span data-ttu-id="36624-1906">Geçerli bağlantı noktası numaraları (1 ile 0xFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="36624-1906">Valid port numbers are (1 through 0xFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1907">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1907">Return Values</span></span>

- <span data-ttu-id="36624-1908">**NX_SUCCESS** (0x00) başarılı yuva bağlaması.</span><span class="sxs-lookup"><span data-stu-id="36624-1908">**NX_SUCCESS** (0x00) Successful socket bind.</span></span>
- <span data-ttu-id="36624-1909">**NX_NOT_BOUND** (0x24) bu yuva bir bağlantı noktasına bağlanmamış.</span><span class="sxs-lookup"><span data-stu-id="36624-1909">**NX_NOT_BOUND** (0x24) This socket is not bound to a port.</span></span>
- <span data-ttu-id="36624-1910">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi veya bağlantı noktası döndürme işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1910">**NX_PTR_ERROR** (0x07) Invalid socket pointer or port return pointer.</span></span>
- <span data-ttu-id="36624-1911">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1911">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1912">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-1912">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1913">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1913">Allowed From</span></span>

<span data-ttu-id="36624-1914">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1914">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1915">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1915">Preemption Possible</span></span>

<span data-ttu-id="36624-1916">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1916">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1917">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1917">Example</span></span>

```C
/* Get the port number of previously created and bound client
    socket. */
status = nx_tcp_client_socket_port_get(&client_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
    socket is bound to. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1918">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1918">See Also</span></span>

- <span data-ttu-id="36624-1919">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-1919">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-1920">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span><span class="sxs-lookup"><span data-stu-id="36624-1920">nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,</span></span>
- <span data-ttu-id="36624-1921">nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="36624-1921">nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="36624-1922">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1922">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-1923">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1923">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-1924">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-1924">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-1925">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-1925">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-1926">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-1926">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-1927">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-1927">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-1928">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-1928">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_client_socket_unbind"></a><span data-ttu-id="36624-1929">nx_tcp_client_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="36624-1929">nx_tcp_client_socket_unbind</span></span>

<span data-ttu-id="36624-1930">TCP bağlantı noktasından TCP istemci yuvasının bağlantısını kaldır</span><span class="sxs-lookup"><span data-stu-id="36624-1930">Unbind TCP client socket from TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1931">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1931">Prototype</span></span>

```C
UINT nx_tcp_client_socket_unbind(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1932">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1932">Description</span></span>

<span data-ttu-id="36624-1933">Bu hizmet TCP istemci yuvası ile bir TCP bağlantı noktası arasındaki bağlamayı yayınlar.</span><span class="sxs-lookup"><span data-stu-id="36624-1933">This service releases the binding between the TCP client socket and a TCP port.</span></span> <span data-ttu-id="36624-1934">Başka bir yuvayı aynı bağlantı noktası numarasına bağlamayı bekleyen başka iş parçacıkları varsa, ilk askıya alınan iş parçacığı bu bağlantı noktasına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="36624-1934">If there are other threads waiting to bind another socket to the same port number, the first suspended thread is then bound to this port.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1935">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1935">Parameters</span></span>

- <span data-ttu-id="36624-1936">**socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1936">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1937">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1937">Return Values</span></span>

- <span data-ttu-id="36624-1938">**NX_SUCCESS** (0x00) başarılı yuva bağlantısı kesiliyor.</span><span class="sxs-lookup"><span data-stu-id="36624-1938">**NX_SUCCESS** (0x00) Successful socket unbind.</span></span>
- <span data-ttu-id="36624-1939">**NX_NOT_BOUND** (0x24) yuva herhangi bir bağlantı noktasına bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-1939">**NX_NOT_BOUND** (0x24) Socket was not bound to any port.</span></span>
- <span data-ttu-id="36624-1940">**NX_NOT_CLOSED** (0x35) yuvasının bağlantısı kesilmedi.</span><span class="sxs-lookup"><span data-stu-id="36624-1940">**NX_NOT_CLOSED** (0x35) Socket has not been disconnected.</span></span>
- <span data-ttu-id="36624-1941">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1941">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-1942">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1942">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-1943">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-1943">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1944">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1944">Allowed From</span></span>

<span data-ttu-id="36624-1945">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-1945">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1946">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1946">Preemption Possible</span></span>

<span data-ttu-id="36624-1947">Yes</span><span class="sxs-lookup"><span data-stu-id="36624-1947">Yes</span></span>

### <a name="example"></a><span data-ttu-id="36624-1948">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1948">Example</span></span>

```C
/* Unbind a previously created and bound client TCP socket. */
status = nx_tcp_client_socket_unbind(&client_socket);

/* If status is NX_SUCCESS, the client socket is no longer
    bound. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1949">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1949">See Also</span></span>

- <span data-ttu-id="36624-1950">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-1950">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-1951">nx_tcp_client_socket_port_get, nx_tcp_enable, nx_tcp_free_port_find,</span><span class="sxs-lookup"><span data-stu-id="36624-1951">nx_tcp_client_socket_port_get, nx_tcp_enable, nx_tcp_free_port_find,</span></span>
- <span data-ttu-id="36624-1952">nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="36624-1952">nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="36624-1953">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1953">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-1954">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1954">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-1955">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-1955">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-1956">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-1956">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-1957">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-1957">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-1958">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-1958">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-1959">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-1959">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_enable"></a><span data-ttu-id="36624-1960">nx_tcp_enable</span><span class="sxs-lookup"><span data-stu-id="36624-1960">nx_tcp_enable</span></span>

<span data-ttu-id="36624-1961">NetX TCP bileşenini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-1961">Enable TCP component of NetX</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1962">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1962">Prototype</span></span>

```C
UINT nx_tcp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1963">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1963">Description</span></span>

<span data-ttu-id="36624-1964">Bu hizmet, NetX 'in Iletim Denetim Protokolü (TCP) bileşenini sunar.</span><span class="sxs-lookup"><span data-stu-id="36624-1964">This service enables the Transmission Control Protocol (TCP) component of NetX.</span></span> <span data-ttu-id="36624-1965">Etkinleştirildikten sonra, uygulama tarafından TCP bağlantıları kurulabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-1965">After enabled, TCP connections may be established by the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1966">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1966">Parameters</span></span>

- <span data-ttu-id="36624-1967">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1967">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-1968">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-1968">Return Values</span></span>

- <span data-ttu-id="36624-1969">**NX_SUCCESS** (0x00) başarılı TCP etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-1969">**NX_SUCCESS** (0x00) Successful TCP enable.</span></span>
- <span data-ttu-id="36624-1970">**NX_ALREADY_ENABLED** (0x15) TCP zaten etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-1970">**NX_ALREADY_ENABLED** (0x15) TCP is already enabled.</span></span>
- <span data-ttu-id="36624-1971">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-1971">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-1972">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-1972">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-1973">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-1973">Allowed From</span></span>

<span data-ttu-id="36624-1974">Başlatma, iş parçacıkları, zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="36624-1974">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-1975">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-1975">Preemption Possible</span></span>

<span data-ttu-id="36624-1976">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-1976">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-1977">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-1977">Example</span></span>

```C
/* Enable TCP on a previously created IP instance ip_0. */
status = nx_tcp_enable(&ip_0);

/* If status is NX_SUCCESS, TCP is enabled on the IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-1978">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-1978">See Also</span></span>

- <span data-ttu-id="36624-1979">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-1979">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-1980">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-1980">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-1981">nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="36624-1981">nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="36624-1982">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1982">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-1983">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-1983">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-1984">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-1984">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-1985">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-1985">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-1986">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-1986">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-1987">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-1987">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-1988">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-1988">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_free_port_find"></a><span data-ttu-id="36624-1989">nx_tcp_free_port_find</span><span class="sxs-lookup"><span data-stu-id="36624-1989">nx_tcp_free_port_find</span></span>

<span data-ttu-id="36624-1990">Sonraki kullanılabilir TCP bağlantı noktasını bul</span><span class="sxs-lookup"><span data-stu-id="36624-1990">Find next available TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-1991">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-1991">Prototype</span></span>

```C
UINT nx_tcp_free_port_find(
    NX_IP *ip_ptr,
    UINT port, UINT *free_port_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-1992">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-1992">Description</span></span>

<span data-ttu-id="36624-1993">Bu hizmet, uygulama tarafından sağlanan bağlantı noktasından başlayarak ücretsiz bir TCP bağlantı noktasını (ilişkisiz) bulmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="36624-1993">This service attempts to locate a free TCP port (unbound) starting from the application supplied port.</span></span> <span data-ttu-id="36624-1994">Arama mantığı, en fazla 0xFFFF bağlantı noktası değerine ulaşmak için arama gerçekleşeceği gibi kaydırılır.</span><span class="sxs-lookup"><span data-stu-id="36624-1994">The search logic will wrap around if the search happens to reach the maximum port value of 0xFFFF.</span></span> <span data-ttu-id="36624-1995">Arama başarılı olursa, *free_port_ptr* tarafından işaret edilen değişkende boş bağlantı noktası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-1995">If the search is successful, the free port is returned in the variable pointed to by *free_port_ptr*.</span></span>

<span data-ttu-id="36624-1996">*Bu hizmet başka bir iş parçacığından çağrılabilir ve aynı bağlantı noktasına sahip olabilir. Bu yarış durumunu engellemek için, uygulama bu hizmeti ve gerçek istemci yuvasını bir mutex 'in koruması altına yerleştirmek isteyebilir.*</span><span class="sxs-lookup"><span data-stu-id="36624-1996">*This service can be called from another thread and have the same port returned. To prevent this race condition, the application may wish to place this service and the actual client socket bind under the protection of a mutex.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-1997">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-1997">Parameters</span></span>

- <span data-ttu-id="36624-1998">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-1998">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-1999">**bağlantı noktası** Aramaya başlamak için bağlantı noktası numarası (1 ile 0xFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="36624-1999">**port** Port number to start search at (1 through 0xFFFF).</span></span>
- <span data-ttu-id="36624-2000">**free_port_ptr** Hedef boş bağlantı noktası dönüş değeri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2000">**free_port_ptr** Pointer to the destination free port return value.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2001">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2001">Return Values</span></span>

- <span data-ttu-id="36624-2002">**NX_SUCCESS** (0x00) başarılı boş bağlantı noktası bul.</span><span class="sxs-lookup"><span data-stu-id="36624-2002">**NX_SUCCESS** (0x00) Successful free port find.</span></span>
- <span data-ttu-id="36624-2003">**NX_NO_FREE_PORTS** (0x45) boş bağlantı noktası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="36624-2003">**NX_NO_FREE_PORTS** (0x45) No free ports found.</span></span>
- <span data-ttu-id="36624-2004">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2004">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-2005">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2005">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2006">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2006">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-2007">**NX_INVALID_PORT** (0x46) belirtilen bağlantı noktası numarası geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-2007">**NX_INVALID_PORT** (0x46) The specified port number is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2008">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2008">Allowed From</span></span>

<span data-ttu-id="36624-2009">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2009">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2010">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2010">Preemption Possible</span></span>

<span data-ttu-id="36624-2011">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2011">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2012">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2012">Example</span></span>

```C
/* Locate a free TCP port, starting at port 12, on a previously
    created IP instance. */
status = nx_tcp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS, "free_port" contains the next free port
    on the IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2013">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2013">See Also</span></span>

- <span data-ttu-id="36624-2014">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2014">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2015">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2015">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2016">nx_tcp_enable, nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="36624-2016">nx_tcp_enable, nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="36624-2017">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2017">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-2018">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2018">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-2019">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2019">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2020">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2020">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2021">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2021">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2022">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2022">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2023">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2023">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_info_get"></a><span data-ttu-id="36624-2024">nx_tcp_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-2024">nx_tcp_info_get</span></span>

<span data-ttu-id="36624-2025">TCP etkinlikleri hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="36624-2025">Retrieve information about TCP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2026">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2026">Prototype</span></span>

```C
UINT nx_tcp_info_get(
    NX_IP *ip_ptr,
    ULONG *tcp_packets_sent,
    ULONG *tcp_bytes_sent,
    ULONG *tcp_packets_received,
    ULONG *tcp_bytes_received,
    ULONG *tcp_invalid_packets,
    ULONG *tcp_receive_packets_dropped,
    ULONG *tcp_checksum_errors,
    ULONG *tcp_connections,
    ULONG *tcp_disconnections,
    ULONG *tcp_connections_dropped,
    ULONG *tcp_retransmit_packets);
```

### <a name="description"></a><span data-ttu-id="36624-2027">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2027">Description</span></span>

<span data-ttu-id="36624-2028">Bu hizmet, belirtilen IP örneği için TCP etkinlikleri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2028">This service retrieves information about TCP activities for the specified IP instance.</span></span>

<span data-ttu-id="36624-2029">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-2029">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2030">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2030">Parameters</span></span>

- <span data-ttu-id="36624-2031">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2031">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-2032">**tcp_packets_sent** Gönderilen toplam TCP paketi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2032">**tcp_packets_sent** Pointer to destination for the total number of TCP packets sent.</span></span>
- <span data-ttu-id="36624-2033">**tcp_bytes_sent** Gönderilen TCP baytlarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2033">**tcp_bytes_sent** Pointer to destination for the total number of TCP bytes sent.</span></span>
- <span data-ttu-id="36624-2034">**tcp_packets_received** Alınan toplam TCP paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2034">**tcp_packets_received** Pointer to destination of the total number of TCP packets received.</span></span>
- <span data-ttu-id="36624-2035">**tcp_bytes_received** Alınan TCP baytlarının toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2035">**tcp_bytes_received** Pointer to destination of the total number of TCP bytes received.</span></span>
- <span data-ttu-id="36624-2036">**tcp_invalid_packets** Geçersiz TCP paketlerinin toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2036">**tcp_invalid_packets** Pointer to destination of the total number of invalid TCP packets.</span></span>
- <span data-ttu-id="36624-2037">**tcp_receive_packets_dropped** Bırakılan TCP alma paketlerinin toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2037">**tcp_receive_packets_dropped** Pointer to destination of the total number of TCP receive packets dropped.</span></span>
- <span data-ttu-id="36624-2038">**tcp_checksum_errors** Toplam TCP paketi sayısının sağlama toplamı hataları olan hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2038">**tcp_checksum_errors** Pointer to destination of the total number of TCP packets with checksum errors.</span></span>
- <span data-ttu-id="36624-2039">**tcp_connections** Toplam TCP bağlantısı sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2039">**tcp_connections** Pointer to destination of the total number of TCP connections.</span></span>
- <span data-ttu-id="36624-2040">**tcp_disconnections** Toplam TCP bağlantısı sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2040">**tcp_disconnections** Pointer to destination of the total number of TCP disconnections.</span></span>
- <span data-ttu-id="36624-2041">**tcp_connections_dropped** Bırakılan toplam TCP bağlantısı sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2041">**tcp_connections_dropped** Pointer to destination of the total number of TCP connections dropped.</span></span>
- <span data-ttu-id="36624-2042">**tcp_retransmit_packets** Yeniden iletilen TCP paketlerinin toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2042">**tcp_retransmit_packets** Pointer to destination of the total number of TCP packets retransmitted.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2043">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2043">Return Values</span></span>

- <span data-ttu-id="36624-2044">**NX_SUCCESS** (0x00) TCP bilgilerinin başarıyla alımı.</span><span class="sxs-lookup"><span data-stu-id="36624-2044">**NX_SUCCESS** (0x00) Successful TCP information retrieval.</span></span>
- <span data-ttu-id="36624-2045">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2045">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-2046">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2046">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2047">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2047">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2048">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2048">Allowed From</span></span>

<span data-ttu-id="36624-2049">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2049">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2050">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2050">Preemption Possible</span></span>

<span data-ttu-id="36624-2051">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2051">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2052">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2052">Example</span></span>

```C
/* Retrieve TCP information from previously created IP Instance ip_0. */
status = nx_tcp_info_get(&ip_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_invalid_packets,
    &tcp_receive_packets_dropped,
    &tcp_checksum_errors,
    &tcp_connections,
    &tcp_disconnections
    &tcp_connections_dropped,
    &tcp_retransmit_packets);

/* If status is NX_SUCCESS, TCP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2053">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2053">See Also</span></span>

- <span data-ttu-id="36624-2054">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2054">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2055">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2055">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2056">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="36624-2056">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="36624-2057">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2057">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-2058">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2058">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-2059">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2059">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2060">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2060">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2061">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2061">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2062">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2062">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2063">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2063">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_accept"></a><span data-ttu-id="36624-2064">nx_tcp_server_socket_accept</span><span class="sxs-lookup"><span data-stu-id="36624-2064">nx_tcp_server_socket_accept</span></span>

<span data-ttu-id="36624-2065">TCP bağlantısını kabul et</span><span class="sxs-lookup"><span data-stu-id="36624-2065">Accept TCP connection</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2066">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2066">Prototype</span></span>

```C
UINT nx_tcp_server_socket_accept(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-2067">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2067">Description</span></span>

<span data-ttu-id="36624-2068">Bu hizmet, daha önce dinlemek üzere ayarlanmış bir bağlantı noktası için TCP istemci yuvası bağlantı isteğini kabul eder (veya kabul edilmeye hazırlanır).</span><span class="sxs-lookup"><span data-stu-id="36624-2068">This service accepts (or prepares to accept) a TCP client socket connection request for a port that was previously set up for listening.</span></span> <span data-ttu-id="36624-2069">Bu hizmet, uygulama dinlemesi veya yeniden dinleme hizmetini çağırırsa ya da istemci bağlantısı gerçekten mevcut olduğunda dinleme geri çağırma yordamından çağrıldıktan sonra çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-2069">This service may be called immediately after the application calls the listen or re-listen service, or after the listen callback routine is called when the client connection is actually present.</span></span> <span data-ttu-id="36624-2070">Bağlantı hemen kurulamazsa, hizmet sağlanan bekleme seçeneğine göre askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="36624-2070">If a connection cannot not be established right away, the service suspends according to the supplied wait option.</span></span>

<span data-ttu-id="36624-2071">*Sunucu yuvasının sunucu bağlantı noktasına bağlamasını kaldırmak için bağlantı artık gerekmiyorsa, uygulamanın **nx_tcp_server_socket_unaccept** çağrısı gerekir.*</span><span class="sxs-lookup"><span data-stu-id="36624-2071">*The application must call **nx_tcp_server_socket_unaccept** after the connection is no longer needed to remove the server socket's binding to the server port.*</span></span>

<span data-ttu-id="36624-2072">*Uygulama geri çağırma yordamları, IP 'nin yardımcı iş parçacığı içinden çağrılır.*</span><span class="sxs-lookup"><span data-stu-id="36624-2072">*Application callback routines are called from within the IP's helper thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2073">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2073">Parameters</span></span>

- <span data-ttu-id="36624-2074">**socket_ptr** TCP sunucusu yuva denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2074">**socket_ptr** Pointer to the TCP server socket control block.</span></span>
- <span data-ttu-id="36624-2075">**wait_option** Bağlantı kurulurken hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-2075">**wait_option** Defines how the service behaves while the connection is being established.</span></span> <span data-ttu-id="36624-2076">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-2076">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-2077">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-2077">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-2078">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-2078">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-2079">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-2079">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>


### <a name="return-values"></a><span data-ttu-id="36624-2080">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2080">Return Values</span></span>
- <span data-ttu-id="36624-2081">**NX_SUCCESS** (0x00) başarılı TCP sunucusu yuvası kabulü (pasif bağlantı).</span><span class="sxs-lookup"><span data-stu-id="36624-2081">**NX_SUCCESS** (0x00) Successful TCP server socket accept (passive connect).</span></span>
- <span data-ttu-id="36624-2082">**NX_NOT_LISTEN_STATE** (0x36) sağlanan sunucu yuvası bir dinleme durumunda değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2082">**NX_NOT_LISTEN_STATE** (0x36) The server socket supplied is not in a listen state.</span></span>
- <span data-ttu-id="36624-2083">**NX_IN_PROGRESS** (0x37) bekleme belirtilmedi, bağlantı girişimi devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="36624-2083">**NX_IN_PROGRESS** (0x37) No wait was specified, the connection attempt is in progress.</span></span>
- <span data-ttu-id="36624-2084">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği *tx_thread_wait_abort* bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-2084">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="36624-2085">**NX_PTR_ERROR** (0x07) yuva işaretçisi hatası.</span><span class="sxs-lookup"><span data-stu-id="36624-2085">**NX_PTR_ERROR** (0x07) Socket pointer error.</span></span>
- <span data-ttu-id="36624-2086">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2086">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2087">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2087">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2088">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2088">Allowed From</span></span>

<span data-ttu-id="36624-2089">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2089">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2090">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2090">Preemption Possible</span></span>

<span data-ttu-id="36624-2091">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2091">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2092">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2092">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;
void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This
    example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;
    /* Assuming that:
        "port_12_semaphore" has already been created with an
        initial count of 0 "my_ip" has already been created and the
        link is enabled "my_pool" packet pool has already been
        created */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to each client and then disconnecting.*/
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
            request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
            complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye"
                message */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is called
            even if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket
            again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }

    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a><span data-ttu-id="36624-2093">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2093">See Also</span></span>

- <span data-ttu-id="36624-2094">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2094">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2095">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2095">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2096">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2096">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2097">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2097">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-2098">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2098">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-2099">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2099">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2100">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2100">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2101">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2101">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2102">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2102">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2103">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2103">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_listen"></a><span data-ttu-id="36624-2104">nx_tcp_server_socket_listen</span><span class="sxs-lookup"><span data-stu-id="36624-2104">nx_tcp_server_socket_listen</span></span>

<span data-ttu-id="36624-2105">TCP bağlantı noktasında istemci bağlantısı dinlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-2105">Enable listening for client connection on TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2106">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2106">Prototype</span></span>

```C
UINT nx_tcp_server_socket_listen(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr,
    UINT listen_queue_size,
    VOID (*listen_callback)(NX_TCP_SOCKET *socket_ptr, UINT port));
```

### <a name="description"></a><span data-ttu-id="36624-2107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2107">Description</span></span>

<span data-ttu-id="36624-2108">Bu hizmet, belirtilen TCP bağlantı noktasında istemci bağlantı isteği dinlemeyi mümkün.</span><span class="sxs-lookup"><span data-stu-id="36624-2108">This service enables listening for a client connection request on the specified TCP port.</span></span> <span data-ttu-id="36624-2109">İstemci bağlantı isteği alındığında, sağlanan sunucu yuvası belirtilen bağlantı noktasına bağlanır ve sağlanan dinleme geri çağırma işlevi çağırılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2109">When a client connection request is received, the supplied server socket is bound to the specified port and the supplied listen callback function is called.</span></span>

<span data-ttu-id="36624-2110">Dinleme geri çağırma yordamının işlenmesi tamamen uygulamaya göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2110">The listen callback routine's processing is completely up to the application.</span></span> <span data-ttu-id="36624-2111">Daha sonra kabul etme işlemini gerçekleştiren bir uygulama iş parçacığını uyandırma mantığını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="36624-2111">It may contain logic to wake up an application thread that subsequently performs an accept operation.</span></span> <span data-ttu-id="36624-2112">Uygulamanın bu yuva için kabul etme sırasında askıya alınmış bir iş parçacığı zaten varsa, dinleme geri çağırma yordamına gerek duyulmayabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-2112">If the application already has a thread suspended on accept processing for this socket, the listen callback routine may not be needed.</span></span>

<span data-ttu-id="36624-2113">Uygulama aynı bağlantı noktasında ek istemci bağlantılarını ele istiyorsa, bir sonraki bağlantı için ***nx_tcp_server_socket_relisten*** kullanılabilir bir yuva (kapalı durumda olan bir yuva) ile çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-2113">If the application wishes to handle additional client connections on the same port, the ***nx_tcp_server_socket_relisten*** must be called with an available socket (a socket in the CLOSED state) for the next connection.</span></span> <span data-ttu-id="36624-2114">Yeniden dinleme hizmeti çağrılana kadar, ek istemci bağlantıları sıraya alınır.</span><span class="sxs-lookup"><span data-stu-id="36624-2114">Until the re-listen service is called, additional client connections are queued.</span></span> <span data-ttu-id="36624-2115">Maksimum sıra derinliği aşıldığında, en eski bağlantı isteği yeni bağlantı isteğini sıraya alma lehine bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2115">When the maximum queue depth is exceeded, the oldest connection request is dropped in favor of queuing the new connection request.</span></span> <span data-ttu-id="36624-2116">En yüksek sıra derinliği bu hizmet tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="36624-2116">The maximum queue depth is specified by this service.</span></span>

<span data-ttu-id="36624-2117">*Uygulama geri çağırma yordamları iç IP Yardımcısı iş parçacığından çağırılır.*</span><span class="sxs-lookup"><span data-stu-id="36624-2117">*Application callback routines are called from the internal IP helper thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2118">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2118">Parameters</span></span>

- <span data-ttu-id="36624-2119">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2119">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-2120">**bağlantı noktası** Dinlenecek bağlantı noktası numarası (1 ile 0xFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="36624-2120">**port** Port number to listen on (1 through 0xFFFF).</span></span>
- <span data-ttu-id="36624-2121">**socket_ptr** Bağlantı için kullanılacak yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2121">**socket_ptr** Pointer to socket to use for the connection.</span></span>
- <span data-ttu-id="36624-2122">**listen_queue_size** Sıraya alınabilen istemci bağlantı isteği sayısı.</span><span class="sxs-lookup"><span data-stu-id="36624-2122">**listen_queue_size** Number of client connection requests that can be queued.</span></span>
- <span data-ttu-id="36624-2123">**listen_callback** Bağlantı alındığında çağrılacak uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="36624-2123">**listen_callback** Application function to call when the connection is received.</span></span> <span data-ttu-id="36624-2124">NULL belirtilirse, geri arama dinlemesi özelliği devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-2124">If a NULL is specified, the listen callback feature is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2125">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2125">Return Values</span></span>

- <span data-ttu-id="36624-2126">**NX_SUCCESS** (0x00) başarılı TCP bağlantı noktası dinleme etkinleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="36624-2126">**NX_SUCCESS** (0x00) Successful TCP port listen enable.</span></span>
- <span data-ttu-id="36624-2127">**NX_MAX_LISTEN** (0x33) daha fazla dinleme isteği yapısı yok.</span><span class="sxs-lookup"><span data-stu-id="36624-2127">**NX_MAX_LISTEN** (0x33) No more listen request structures are available.</span></span> <span data-ttu-id="36624-2128">Nx_api. h içindeki sabit NX_MAX_LISTEN_REQUESTS, kaç tane etkin dinleme isteğinin mümkün olduğunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-2128">The constant NX_MAX_LISTEN_REQUESTS in nx_api.h defines how many active listen requests are possible.</span></span>
- <span data-ttu-id="36624-2129">**NX_NOT_CLOSED** (0x35) sağlanan sunucu yuvası kapalı durumda değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2129">**NX_NOT_CLOSED** (0x35) The supplied server socket is not in a closed state.</span></span>
- <span data-ttu-id="36624-2130">**NX_ALREADY_BOUND** (0x22) sağlanan sunucu yuvası bir bağlantı noktasına zaten bağlıydı.</span><span class="sxs-lookup"><span data-stu-id="36624-2130">**NX_ALREADY_BOUND** (0x22) The supplied server socket is already bound to a port.</span></span>
- <span data-ttu-id="36624-2131">**NX_DUPLICATE_LISTEN** (0x34) Bu bağlantı noktası için zaten etkin bir dinleme isteği var.</span><span class="sxs-lookup"><span data-stu-id="36624-2131">**NX_DUPLICATE_LISTEN** (0x34) There is already an active listen request for this port.</span></span>
- <span data-ttu-id="36624-2132">**NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası belirtildi.</span><span class="sxs-lookup"><span data-stu-id="36624-2132">**NX_INVALID_PORT** (0x46) Invalid port specified.</span></span>
- <span data-ttu-id="36624-2133">**NX_PTR_ERROR** (0x07) geçersiz IP veya yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2133">**NX_PTR_ERROR** (0x07) Invalid IP or socket pointer.</span></span>
- <span data-ttu-id="36624-2134">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2134">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2135">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2135">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2136">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2136">Allowed From</span></span>

<span data-ttu-id="36624-2137">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2137">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2138">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2138">Preemption Possible</span></span>

<span data-ttu-id="36624-2139">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2139">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2140">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2140">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread.*/
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket.
        This example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an
        initial count of 0 "my_ip" has already been created
        and the link is enabled "my_pool" packet pool has already
        been created.
    */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server
        Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to
        each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
            request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

    /* Wait for 200 ticks for the client socket connection
        to complete. */
    status = nx_tcp_server_socket_accept(&server_socket, 200);

    /* Check for a successful connection. */
    if (status == NX_SUCCESS)
    {
        /* Allocate a packet for the "Hello_and_Goodbye"
            message. */
        nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
            NX_WAIT_FOREVER);

        /* Place "Hello_and_Goodbye" in the packet. */
        nx_packet_data_append(my_packet, "Hello_and_Goodbye",
            sizeof("Hello_and_Goodbye"),
            &my_pool,
            NX_WAIT_FOREVER);

        /* Send "Hello_and_Goodbye" to client. */
        nx_tcp_socket_send(&server_socket, my_packet, 200);

        /* Check for an error. */
        if (status)
        {
            /* Error, release the packet. */
            nx_packet_release(my_packet);
        }
        /* Now disconnect the server socket from the client. */
        nx_tcp_socket_disconnect(&server_socket, 200);
    }

    /* Unaccept the server socket. Note that unaccept is called
        even if disconnect or accept fails. */
    nx_tcp_server_socket_unaccept(&server_socket);

    /* Setup server socket for listening with this socket
    again. */
    nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
}

/* We are now done so unlisten on server port 12. */
nx_tcp_server_socket_unlisten(&my_ip, 12);

/* Delete the server socket. */
nx_tcp_socket_delete(&server_socket);
```

### <a name="see-also"></a><span data-ttu-id="36624-2141">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2141">See Also</span></span>

- <span data-ttu-id="36624-2142">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2142">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2143">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2143">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2144">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2144">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2145">nx_tcp_server_socket_accept, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2145">nx_tcp_server_socket_accept, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-2146">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2146">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-2147">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2147">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2148">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2148">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2149">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2149">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2150">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2150">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2151">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2151">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_relisten"></a><span data-ttu-id="36624-2152">nx_tcp_server_socket_relisten</span><span class="sxs-lookup"><span data-stu-id="36624-2152">nx_tcp_server_socket_relisten</span></span>

<span data-ttu-id="36624-2153">TCP bağlantı noktasındaki istemci bağlantısını yeniden dinle</span><span class="sxs-lookup"><span data-stu-id="36624-2153">Re-listen for client connection on TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2154">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2154">Prototype</span></span>

```C
UINT nx_tcp_server_socket_relisten(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-2155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2155">Description</span></span>

<span data-ttu-id="36624-2156">Bu hizmet, daha önce dinlemek üzere ayarlanan bir bağlantı noktasında bir bağlantı alındıktan sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2156">This service is called after a connection has been received on a port that was setup previously for listening.</span></span> <span data-ttu-id="36624-2157">Bu hizmetin ana amacı, sonraki istemci bağlantısı için yeni bir sunucu yuvası sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="36624-2157">The main purpose of this service is to provide a new server socket for the next client connection.</span></span> <span data-ttu-id="36624-2158">Bir bağlantı isteği sıraya alınmışsa, bu hizmet çağrısı sırasında bağlantı hemen işlenir.</span><span class="sxs-lookup"><span data-stu-id="36624-2158">If a connection request is queued, the connection will be processed immediately during this service call.</span></span>

<span data-ttu-id="36624-2159">*Özgün dinleme isteği tarafından belirtilen geri arama yordamı, bu yeni sunucu yuvası için bir bağlantı olduğunda da çağırılır.*</span><span class="sxs-lookup"><span data-stu-id="36624-2159">*The same callback routine specified by the original listen request is also called when a connection is present for this new server socket.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2160">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2160">Parameters</span></span>

- <span data-ttu-id="36624-2161">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2161">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-2162">**bağlantı noktası** Yeniden dinlemek için bağlantı noktası numarası (1 ile 0xFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="36624-2162">**port** Port number to re-listen on (1 through 0xFFFF).</span></span>
- <span data-ttu-id="36624-2163">**socket_ptr** Sonraki istemci bağlantısı için kullanılacak yuva.</span><span class="sxs-lookup"><span data-stu-id="36624-2163">**socket_ptr** Socket to use for the next client connection.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2164">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2164">Return Values</span></span>
- <span data-ttu-id="36624-2165">**NX_SUCCESS** (0x00) başarılı TCP bağlantı noktası yeniden dinleme.</span><span class="sxs-lookup"><span data-stu-id="36624-2165">**NX_SUCCESS** (0x00) Successful TCP port re-listen.</span></span>
- <span data-ttu-id="36624-2166">**NX_NOT_CLOSED** (0x35) sağlanan sunucu yuvası kapalı durumda değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2166">**NX_NOT_CLOSED** (0x35) The supplied server socket is not in a closed state.</span></span>
- <span data-ttu-id="36624-2167">**NX_ALREADY_BOUND** (0x22) sağlanan sunucu yuvası bir bağlantı noktasına zaten bağlıydı.</span><span class="sxs-lookup"><span data-stu-id="36624-2167">**NX_ALREADY_BOUND** (0x22) The supplied server socket is already bound to a port.</span></span>
- <span data-ttu-id="36624-2168">**NX_INVALID_RELISTEN** (0x47) Bu bağlantı noktası için zaten geçerli bir yuva işaretçisi var veya belirtilen bağlantı noktasında bir dinleme isteği etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2168">**NX_INVALID_RELISTEN** (0x47) There is already a valid socket pointer for this port or the port specified does not have a listen request active.</span></span>
- <span data-ttu-id="36624-2169">Sıraya alınmış bir bağlantı isteği olduğundan ve bu çağrı sırasında işlendiği için, NX_SUCCESS ile aynı **NX_CONNECTION_PENDING** (0x48).</span><span class="sxs-lookup"><span data-stu-id="36624-2169">**NX_CONNECTION_PENDING** (0x48) Same as NX_SUCCESS, except there was a queued connection request and it was processed during this call.</span></span>
- <span data-ttu-id="36624-2170">**NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası belirtildi.</span><span class="sxs-lookup"><span data-stu-id="36624-2170">**NX_INVALID_PORT** (0x46) Invalid port specified.</span></span>
- <span data-ttu-id="36624-2171">**NX_PTR_ERROR** (0x07) geçersiz IP veya dinleme geri çağırma işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2171">**NX_PTR_ERROR** (0x07) Invalid IP or listen callback pointer.</span></span>
- <span data-ttu-id="36624-2172">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2172">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2173">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2173">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2174">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2174">Allowed From</span></span>

<span data-ttu-id="36624-2175">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2175">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2176">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2176">Preemption Possible</span></span>

<span data-ttu-id="36624-2177">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2177">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2178">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2178">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread.*/
    tx_semaphore_put(&port_12_semaphore);
    }

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This
    example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
    "port_12_semaphore" has already been created with an initial
        count of 0.
        "my_ip" has already been created and the link is enabled.
        "my_pool" packet pool has already been created. */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL,
        port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);
    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to each client then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
        request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
        complete. */
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye"
            message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is
        called even if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket
        again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a><span data-ttu-id="36624-2179">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2179">See Also</span></span>

- <span data-ttu-id="36624-2180">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2180">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2181">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2181">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2182">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2182">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2183">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2183">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2184">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2184">nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,</span></span>
- <span data-ttu-id="36624-2185">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2185">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2186">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2186">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2187">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2187">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2188">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2188">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2189">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2189">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_unaccept"></a><span data-ttu-id="36624-2190">nx_tcp_server_socket_unaccept</span><span class="sxs-lookup"><span data-stu-id="36624-2190">nx_tcp_server_socket_unaccept</span></span>

<span data-ttu-id="36624-2191">Yuva ilişkilendirmesini dinleme bağlantı noktasıyla kaldır</span><span class="sxs-lookup"><span data-stu-id="36624-2191">Remove socket association with listening port</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2192">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2192">Prototype</span></span>

```C
UINT nx_tcp_server_socket_unaccept(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-2193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2193">Description</span></span>

<span data-ttu-id="36624-2194">Bu hizmet, bu sunucu yuvası ile belirtilen sunucu bağlantı noktası arasındaki ilişkiyi kaldırır.</span><span class="sxs-lookup"><span data-stu-id="36624-2194">This service removes the association between this server socket and the specified server port.</span></span> <span data-ttu-id="36624-2195">Uygulamanın, bir bağlantının kesilmesi veya bir başarısız kabul çağrısından sonra bu hizmeti çağırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36624-2195">The application must call this service after a disconnection or after an unsuccessful accept call.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2196">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2196">Parameters</span></span>

- <span data-ttu-id="36624-2197">**socket_ptr** Daha önce kurulum sunucusu yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2197">**socket_ptr** Pointer to previously setup server socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2198">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2198">Return Values</span></span>

- <span data-ttu-id="36624-2199">**NX_SUCCESS** (0x00) başarılı sunucu yuvası kabul iptali.</span><span class="sxs-lookup"><span data-stu-id="36624-2199">**NX_SUCCESS** (0x00) Successful server socket unaccept.</span></span>
- <span data-ttu-id="36624-2200">**NX_NOT_LISTEN_STATE** (0x36) sunucu yuvası yanlış bir durumda ve muhtemelen kesilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="36624-2200">**NX_NOT_LISTEN_STATE** (0x36) Server socket is in an improper state, and is probably not disconnected.</span></span>
- <span data-ttu-id="36624-2201">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2201">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2202">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2202">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2203">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2203">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2204">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2204">Allowed From</span></span>

<span data-ttu-id="36624-2205">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2205">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2206">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2206">Preemption Possible</span></span>

<span data-ttu-id="36624-2207">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2207">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2208">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2208">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This example
    doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an initial count
        of 0 "my_ip" has already been created and the link is enabled
        "my_pool" packet pool has already been created
        */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,NX_NULL,
        port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye"
        to each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection request
            is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
            complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye" message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet,
                "Hello_and_Goodbye",sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is called even
            if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a><span data-ttu-id="36624-2209">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2209">See Also</span></span>

- <span data-ttu-id="36624-2210">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2210">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2211">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind, nx_tcp_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-2211">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind, nx_tcp_enable,</span></span>
- <span data-ttu-id="36624-2212">nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,</span><span class="sxs-lookup"><span data-stu-id="36624-2212">nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,</span></span>
- <span data-ttu-id="36624-2213">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span><span class="sxs-lookup"><span data-stu-id="36624-2213">nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,</span></span>
- <span data-ttu-id="36624-2214">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2214">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2215">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2215">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2216">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2216">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2217">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2217">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2218">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2218">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_server_socket_unlisten"></a><span data-ttu-id="36624-2219">nx_tcp_server_socket_unlisten</span><span class="sxs-lookup"><span data-stu-id="36624-2219">nx_tcp_server_socket_unlisten</span></span>

<span data-ttu-id="36624-2220">TCP bağlantı noktasındaki istemci bağlantısını dinlemeyi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="36624-2220">Disable listening for client connection on TCP port</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2221">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2221">Prototype</span></span>

```C
UINT nx_tcp_server_socket_unlisten(NX_IP *ip_ptr, UINT port);
```

### <a name="description"></a><span data-ttu-id="36624-2222">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2222">Description</span></span>

<span data-ttu-id="36624-2223">Bu hizmet, belirtilen TCP bağlantı noktasındaki istemci bağlantı isteğini dinlemeyi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="36624-2223">This service disables listening for a client connection request on the specified TCP port.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2224">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2224">Parameters</span></span>

- <span data-ttu-id="36624-2225">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2225">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-2226">**bağlantı noktası** Dinlemeyi devre dışı bırakılacak bağlantı noktası sayısı (0 ile 0xFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="36624-2226">**port** Number of port to disable listening (0 through 0xFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2227">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2227">Return Values</span></span>

- <span data-ttu-id="36624-2228">**NX_SUCCESS** (0x00) başarılı TCP dinlemesi devre dışı.</span><span class="sxs-lookup"><span data-stu-id="36624-2228">**NX_SUCCESS** (0x00) Successful TCP listen disable.</span></span>
- <span data-ttu-id="36624-2229">**NX_ENTRY_NOT_FOUND** (0x16) dinleme, belirtilen bağlantı noktası için etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2229">**NX_ENTRY_NOT_FOUND** (0x16) Listening was not enabled for the specified port.</span></span>
- <span data-ttu-id="36624-2230">**NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası belirtildi.</span><span class="sxs-lookup"><span data-stu-id="36624-2230">**NX_INVALID_PORT** (0x46) Invalid port specified.</span></span>
- <span data-ttu-id="36624-2231">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2231">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-2232">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2232">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2233">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2233">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2234">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2234">Allowed From</span></span>

<span data-ttu-id="36624-2235">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2235">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2236">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2236">Preemption Possible</span></span>

<span data-ttu-id="36624-2237">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2237">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2238">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2238">Example</span></span>

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This example
    doesn't use this callback.*/
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an initial count
        of 0 "my_ip" has already been created and the link is enabled
        "my_pool" packet pool has already been created
    */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye" to
        each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection request is
            present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye" message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"), &my_pool,
                NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }
            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }
        /* Unaccept the server socket. Note that unaccept is called even if
        disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a><span data-ttu-id="36624-2239">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2239">See Also</span></span>

- <span data-ttu-id="36624-2240">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2240">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2241">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2241">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2242">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2242">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2243">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2243">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2244">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="36624-2244">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="36624-2245">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2245">nx_tcp_socket_bytes_available, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2246">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2246">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2247">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2247">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2248">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2248">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2249">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2249">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_bytes_available"></a><span data-ttu-id="36624-2250">nx_tcp_socket_bytes_available</span><span class="sxs-lookup"><span data-stu-id="36624-2250">nx_tcp_socket_bytes_available</span></span>

<span data-ttu-id="36624-2251">Alma için kullanılabilir bayt sayısını alır</span><span class="sxs-lookup"><span data-stu-id="36624-2251">Retrieves number of bytes available for retrieval</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2252">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2252">Prototype</span></span>

```C
UINT nx_tcp_socket_bytes_available(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```

### <a name="description"></a><span data-ttu-id="36624-2253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2253">Description</span></span>

<span data-ttu-id="36624-2254">Bu hizmet, belirtilen TCP yuvasında alınabilmeleri için kullanılabilen bayt sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2254">This service obtains the number of bytes available for retrieval in the specified TCP socket.</span></span> <span data-ttu-id="36624-2255">TCP yuvasının zaten bağlı olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-2255">Note that the TCP socket must already be connected.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2256">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2256">Parameters</span></span>

- <span data-ttu-id="36624-2257">**socket_ptr** Önceden oluşturulmuş ve bağlı TCP yuvasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2257">**socket_ptr** Pointer to previously created and connected TCP socket.</span></span>
- <span data-ttu-id="36624-2258">**bytes_available** Kullanılabilir baytlar için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2258">**bytes_available** Pointer to destination for bytes available.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2259">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2259">Return Values</span></span>

- <span data-ttu-id="36624-2260">**NX_SUCCESS** (0x00) hizmeti başarıyla çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2260">**NX_SUCCESS** (0x00) Service executes successfully.</span></span> <span data-ttu-id="36624-2261">Okuma için kullanılabilir bayt sayısı çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-2261">Number of bytes available for read is returned to the caller.</span></span>
- <span data-ttu-id="36624-2262">**NX_NOT_CONNECTED** (0x38) yuva bağlı durumda değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2262">**NX_NOT_CONNECTED** (0x38) Socket is not in a connected state.</span></span>
- <span data-ttu-id="36624-2263">**NX_PTR_ERROR** (0x07) geçersiz işaretçiler.</span><span class="sxs-lookup"><span data-stu-id="36624-2263">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="36624-2264">**NX_NOT_ENABLED** (0x14) TCP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2264">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="36624-2265">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2265">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2266">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2266">Allowed From</span></span>

<span data-ttu-id="36624-2267">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2267">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2268">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2268">Preemption Possible</span></span>

<span data-ttu-id="36624-2269">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2269">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2270">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2270">Example</span></span>

```C
/* Get the bytes available for retrieval on the specified socket. */
status = nx_tcp_socket_bytes_available(&my_socket,
    &bytes_available);

/* Is status = NX_SUCCESS, the available bytes is returned in
    bytes_available. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2271">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2271">See Also</span></span>

- <span data-ttu-id="36624-2272">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2272">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2273">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2273">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2274">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2274">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2275">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2275">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2276">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="36624-2276">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="36624-2277">nx_tcp_server_socket_unlisten, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2277">nx_tcp_server_socket_unlisten, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2278">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2278">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2279">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2279">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2280">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2280">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2281">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2281">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_create"></a><span data-ttu-id="36624-2282">nx_tcp_socket_create</span><span class="sxs-lookup"><span data-stu-id="36624-2282">nx_tcp_socket_create</span></span>

<span data-ttu-id="36624-2283">TCP istemcisi veya sunucu yuvası oluşturma</span><span class="sxs-lookup"><span data-stu-id="36624-2283">Create TCP client or server socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2284">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2284">Prototype</span></span>

```C
UINT nx_tcp_socket_create(
    NX_IP *ip_ptr, 
    NX_TCP_SOCKET *socket_ptr,
    CHAR *name, ULONG type_of_service, 
    ULONG fragment,
    UINT time_to_live, 
    ULONG window_size,
    VOID (*urgent_data_callback)(NX_TCP_SOCKET *socket_ptr),
    VOID (*disconnect_callback)(NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="36624-2285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2285">Description</span></span>

<span data-ttu-id="36624-2286">Bu hizmet, belirtilen IP örneği için bir TCP istemcisi veya sunucu yuvası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="36624-2286">This service creates a TCP client or server socket for the specified IP instance.</span></span>

<span data-ttu-id="36624-2287">*Uygulama geri çağırma yordamları, bu IP örneğiyle ilişkili iş parçacığından çağırılır.*</span><span class="sxs-lookup"><span data-stu-id="36624-2287">*Application callback routines are called from the thread associated with this IP instance.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2288">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2288">Parameters</span></span>

- <span data-ttu-id="36624-2289">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2289">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-2290">**socket_ptr** Yeni TCP yuvası denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2290">**socket_ptr** Pointer to new TCP socket control block.</span></span>
- <span data-ttu-id="36624-2291">**ad** Bu TCP yuvasının uygulama adı.</span><span class="sxs-lookup"><span data-stu-id="36624-2291">**name** Application name for this TCP socket.</span></span>
- <span data-ttu-id="36624-2292">**Type_of_service** İletim için hizmet türünü tanımlar, yasal değerler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="36624-2292">**type_of_service** Defines the type of service for the transmission, legal values are as follows:</span></span>

- <span data-ttu-id="36624-2293">NX_IP_NORMAL (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-2293">NX_IP_NORMAL (0x00000000)</span></span>
- <span data-ttu-id="36624-2294">NX_IP_MIN_DELAY (0x00100000)</span><span class="sxs-lookup"><span data-stu-id="36624-2294">NX_IP_MIN_DELAY (0x00100000)</span></span>
- <span data-ttu-id="36624-2295">NX_IP_MAX_DATA (0x00080000)</span><span class="sxs-lookup"><span data-stu-id="36624-2295">NX_IP_MAX_DATA (0x00080000)</span></span>
- <span data-ttu-id="36624-2296">NX_IP_MAX_RELIABLE (0x00040000)</span><span class="sxs-lookup"><span data-stu-id="36624-2296">NX_IP_MAX_RELIABLE (0x00040000)</span></span>
- <span data-ttu-id="36624-2297">NX_IP_MIN_COST (0x00020000)</span><span class="sxs-lookup"><span data-stu-id="36624-2297">NX_IP_MIN_COST (0x00020000)</span></span>

- <span data-ttu-id="36624-2298">**parça**  IP fragmenting izin verilip verilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="36624-2298">**fragment**  Specifies whether or not IP fragmenting is allowed.</span></span> <span data-ttu-id="36624-2299">NX_FRAGMENT_OKAY (0x0) belirtilmişse, IP fragmenting izin verilir.</span><span class="sxs-lookup"><span data-stu-id="36624-2299">If NX_FRAGMENT_OKAY (0x0) is specified, IP fragmenting is allowed.</span></span> <span data-ttu-id="36624-2300">NX_DONT_FRAGMENT (0x4000) belirtilirse, IP fragmenting devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2300">If  NX_DONT_FRAGMENT (0x4000) is specified, IP fragmenting is disabled.</span></span>
- <span data-ttu-id="36624-2301">**Time_to_live** Bu paketin oluşturulmadan önce kaç yönlendirici geçebileceğini tanımlayan 8 bitlik değeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="36624-2301">**time_to_live** Specifies the 8-bit value that defines how many routers this packet can pass before being thrown away.</span></span> <span data-ttu-id="36624-2302">Varsayılan değer NX_IP_TIME_TO_LIVE tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="36624-2302">The default value is specified by NX_IP_TIME_TO_LIVE.</span></span>
- <span data-ttu-id="36624-2303">**window_size** Bu yuva için alma sırasında izin verilen en fazla bayt sayısını tanımlar</span><span class="sxs-lookup"><span data-stu-id="36624-2303">**window_size** Defines the maximum number of bytes allowed in the receive queue for this socket</span></span>
- <span data-ttu-id="36624-2304">**urgent_data_callback** Alma akışında acil verilerin her ne zaman algılandığına çağrılan uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="36624-2304">**urgent_data_callback** Application function that is called whenever urgent data is detected in the receive stream.</span></span> <span data-ttu-id="36624-2305">Bu değer NX_NULL, acil veriler yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2305">If this value is NX_NULL, urgent data is ignored.</span></span>
- <span data-ttu-id="36624-2306">**disconnect_callback** Bağlantının diğer ucundaki yuva tarafından her bir bağlantı kesilmesi verildiğinde çağrılan uygulama işlevi.</span><span class="sxs-lookup"><span data-stu-id="36624-2306">**disconnect_callback** Application function that is called whenever a disconnect is issued by the socket at the other end of the connection.</span></span> <span data-ttu-id="36624-2307">Bu değer NX_NULL ise, bağlantıyı kes geri çağırma işlevi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2307">If this value is NX_NULL, the disconnect callback function is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2308">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2308">Return Values</span></span>
- <span data-ttu-id="36624-2309">**NX_SUCCESS** (0x00) başarılı TCP istemci yuvası oluşturma.</span><span class="sxs-lookup"><span data-stu-id="36624-2309">**NX_SUCCESS** (0x00) Successful TCP client socket create.</span></span>
- <span data-ttu-id="36624-2310">**NX_OPTION_ERROR** (0X0a) geçersiz hizmet türü, parça, geçersiz pencere boyutu veya zaman tolive seçeneği.</span><span class="sxs-lookup"><span data-stu-id="36624-2310">**NX_OPTION_ERROR** (0x0A) Invalid type-of-service, fragment, invalid window size, or time-tolive option.</span></span>
- <span data-ttu-id="36624-2311">**NX_PTR_ERROR** (0x07) geçersiz IP veya yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2311">**NX_PTR_ERROR** (0x07) Invalid IP or socket pointer.</span></span>
- <span data-ttu-id="36624-2312">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2312">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2313">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2313">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2314">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2314">Allowed From</span></span>

<span data-ttu-id="36624-2315">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2315">Initialization and Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2316">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2316">Preemption Possible</span></span>

<span data-ttu-id="36624-2317">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2317">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2318">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2318">Example</span></span>

```C
/* Create a TCP client socket on the previously created IP instance,
    with normal delivery, IP fragmentation enabled, 0x80 time to
    live, a 200-byte receive window, no urgent callback routine, and
    the "client_disconnect" routine to handle disconnection initiated
    from the other end of the connection. */
status = nx_tcp_socket_create(&ip_0, &client_socket,
    "Client Socket",
    NX_IP_NORMAL, NX_FRAGMENT_OKAY,
    0x80, 200, NX_NULL
    client_disconnect);

/* If status is NX_SUCCESS, the client socket is created and ready
    to be bound. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2319">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2319">See Also</span></span>

- <span data-ttu-id="36624-2320">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2320">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2321">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2321">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2322">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2322">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2323">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2323">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2324">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="36624-2324">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="36624-2325">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2325">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2326">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2326">nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2327">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2327">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2328">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2328">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2329">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2329">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_delete"></a><span data-ttu-id="36624-2330">nx_tcp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="36624-2330">nx_tcp_socket_delete</span></span>

<span data-ttu-id="36624-2331">TCP yuvasını Sil</span><span class="sxs-lookup"><span data-stu-id="36624-2331">Delete TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2332">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2332">Prototype</span></span>

```C
UINT nx_tcp_socket_delete(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-2333">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2333">Description</span></span>

<span data-ttu-id="36624-2334">Bu hizmet, önceden oluşturulmuş bir TCP yuvasını siler.</span><span class="sxs-lookup"><span data-stu-id="36624-2334">This service deletes a previously created TCP socket.</span></span> <span data-ttu-id="36624-2335">Yuva hala bağlı veya bağlı ise, hizmet bir hata kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="36624-2335">If the socket is still bound or connected, the service returns an error code.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2336">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2336">Parameters</span></span>

- <span data-ttu-id="36624-2337">**socket_ptr** Önceden oluşturulmuş TCP yuvası</span><span class="sxs-lookup"><span data-stu-id="36624-2337">**socket_ptr** Previously created TCP socket</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2338">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2338">Return Values</span></span>

- <span data-ttu-id="36624-2339">**NX_SUCCESS** (0x00) başarılı yuva silme.</span><span class="sxs-lookup"><span data-stu-id="36624-2339">**NX_SUCCESS** (0x00) Successful socket delete.</span></span>
- <span data-ttu-id="36624-2340">**NX_NOT_CREATED** (0x27) yuva oluşturulmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-2340">**NX_NOT_CREATED** (0x27) Socket was not created.</span></span>
- <span data-ttu-id="36624-2341">**NX_STILL_BOUND** (0x42) yuva hala bağımlı.</span><span class="sxs-lookup"><span data-stu-id="36624-2341">**NX_STILL_BOUND** (0x42) Socket is still bound.</span></span>
- <span data-ttu-id="36624-2342">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2342">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2343">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2343">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2344">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2344">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2345">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2345">Allowed From</span></span>

<span data-ttu-id="36624-2346">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2346">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2347">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2347">Preemption Possible</span></span>

<span data-ttu-id="36624-2348">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2348">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2349">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2349">Example</span></span>

```C
/* Delete a previously created TCP client socket. */
status = nx_tcp_socket_delete(&client_socket);

/* If status is NX_SUCCESS, the client socket is deleted. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2350">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2350">See Also</span></span>

- <span data-ttu-id="36624-2351">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2351">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2352">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2352">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2353">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2353">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2354">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2354">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2355">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="36624-2355">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="36624-2356">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2356">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2357">nx_tcp_socket_create, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2357">nx_tcp_socket_create, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2358">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2358">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2359">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2359">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,</span></span>
- <span data-ttu-id="36624-2360">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2360">nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_disconnect"></a><span data-ttu-id="36624-2361">nx_tcp_socket_disconnect</span><span class="sxs-lookup"><span data-stu-id="36624-2361">nx_tcp_socket_disconnect</span></span>

<span data-ttu-id="36624-2362">İstemci ve sunucu yuvası bağlantılarının bağlantısını kes</span><span class="sxs-lookup"><span data-stu-id="36624-2362">Disconnect client and server socket connections</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2363">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2363">Prototype</span></span>

```C
UINT nx_tcp_socket_disconnect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-2364">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2364">Description</span></span>

<span data-ttu-id="36624-2365">Bu hizmet, kurulan bir istemci veya sunucu yuvası bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="36624-2365">This service disconnects an established client or server socket connection.</span></span> <span data-ttu-id="36624-2366">Sunucu yuvasının bağlantısının kesilmesi, geri kabul edilmemiş bir istek gelmelidir, ancak bağlantısı kesilen bir istemci yuvası, başka bir bağlantı isteği için bir durumda bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2366">A disconnect of a server socket should be followed by an unaccept request, while a client socket that is disconnected is left in a state ready for another connection request.</span></span> <span data-ttu-id="36624-2367">Bağlantıyı kesme işlemi hemen tamamlanmazsa, hizmet sağlanan bekleme seçeneğine göre askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="36624-2367">If the disconnect process cannot finish immediately, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2368">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2368">Parameters</span></span>

- <span data-ttu-id="36624-2369">**socket_ptr** Daha önce bağlı olan istemci veya sunucu yuvası örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2369">**socket_ptr** Pointer to previously connected client or server socket instance.</span></span>
- <span data-ttu-id="36624-2370">**wait_option** Bağlantının kesilmesi devam ederken hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-2370">**wait_option** Defines how the service behaves while the disconnection is in progress.</span></span> <span data-ttu-id="36624-2371">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-2371">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-2372">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-2372">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-2373">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-2373">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-2374">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-2374">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2375">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2375">Return Values</span></span>

- <span data-ttu-id="36624-2376">**NX_SUCCESS** (0x00) başarılı yuva bağlantısı kesilemedi.</span><span class="sxs-lookup"><span data-stu-id="36624-2376">**NX_SUCCESS** (0x00) Successful socket disconnect.</span></span>
- <span data-ttu-id="36624-2377">**NX_NOT_CONNECTED** (0x38) belirtilen yuva bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2377">**NX_NOT_CONNECTED** (0x38) Specified socket is not connected.</span></span>
- <span data-ttu-id="36624-2378">**NX_IN_PROGRESS** (0x37) bağlantı kesilmesi devam ediyor, hiçbir bekleme belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="36624-2378">**NX_IN_PROGRESS** (0x37) Disconnect is in progress, no wait was specified.</span></span>
- <span data-ttu-id="36624-2379">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-2379">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-2380">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2380">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2381">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2381">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2382">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2382">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2383">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2383">Allowed From</span></span>

<span data-ttu-id="36624-2384">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2384">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2385">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2385">Preemption Possible</span></span>

<span data-ttu-id="36624-2386">Yes</span><span class="sxs-lookup"><span data-stu-id="36624-2386">Yes</span></span>

### <a name="example"></a><span data-ttu-id="36624-2387">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2387">Example</span></span>

```C
/* Disconnect from a previously established connection and wait a
    maximum of 400 timer ticks. */
status = nx_tcp_socket_disconnect(&client_socket, 400);

/* If status is NX_SUCCESS, the previously connected socket (either
    as a result of the client socket connect or the server accept) is
    disconnected. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2388">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2388">See Also</span></span>

- <span data-ttu-id="36624-2389">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2389">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2390">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2390">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2391">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2391">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2392">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2392">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2393">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="36624-2393">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="36624-2394">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2394">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2395">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2395">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_info_get,</span></span>
- <span data-ttu-id="36624-2396">nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,</span><span class="sxs-lookup"><span data-stu-id="36624-2396">nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,</span></span>
- <span data-ttu-id="36624-2397">nx_tcp_socket_send, nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2397">nx_tcp_socket_send, nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_disconnect_complete_notify"></a><span data-ttu-id="36624-2398">nx_tcp_socket_disconnect_complete_notify</span><span class="sxs-lookup"><span data-stu-id="36624-2398">nx_tcp_socket_disconnect_complete_notify</span></span>

<span data-ttu-id="36624-2399">TCP bağlantı kesmeyi yüklemeyi bildirme geri çağırma işlevi</span><span class="sxs-lookup"><span data-stu-id="36624-2399">Install TCP disconnect complete notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2400">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2400">Prototype</span></span>

```C
UINT nx_tcp_socket_disconnect_complete_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_disconnect_complete_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="36624-2401">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2401">Description</span></span>

<span data-ttu-id="36624-2402">Bu hizmet, bir yuva bağlantı kesme işlemi tamamlandıktan sonra çağrılan bir geri arama işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="36624-2402">This service registers a callback function which is invoked after a socket disconnect operation is completed.</span></span> <span data-ttu-id="36624-2403">NetX seçeneği ile derlenip, TCP yuvası bağlantı kesme tamam geri çağırma işlevi kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="36624-2403">The TCP socket disconnect complete callback function is available if NetX is built with the option</span></span>

- <span data-ttu-id="36624-2404">***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="36624-2404">***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** defined.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2405">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2405">Parameters</span></span>

- <span data-ttu-id="36624-2406">**socket_ptr** Daha önce bağlı olan istemci veya sunucu yuvası örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2406">**socket_ptr** Pointer to previously connected client or server socket instance.</span></span>
- <span data-ttu-id="36624-2407">**tcp_disconnect_complete_notify** Yüklenecek geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="36624-2407">**tcp_disconnect_complete_notify** The callback function to be installed.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2408">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2408">Return Values</span></span>
- <span data-ttu-id="36624-2409">**NX_SUCCESS** (0x00) geri çağırma işlevi başarıyla kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="36624-2409">**NX_SUCCESS** (0x00) Successfully registered the callback function.</span></span>
- <span data-ttu-id="36624-2410">**NX_NOT_SUPPORTED** (0x4b) genişletilmiş bildirim özelliği NETX kitaplığında yerleşik değildir</span><span class="sxs-lookup"><span data-stu-id="36624-2410">**NX_NOT_SUPPORTED** (0x4B) The extended notify feature is not built into the NetX library</span></span>
- <span data-ttu-id="36624-2411">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2411">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2412">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2412">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2413">**NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2413">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2414">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2414">Allowed From</span></span>

<span data-ttu-id="36624-2415">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2415">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2416">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2416">Preemption Possible</span></span>

<span data-ttu-id="36624-2417">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2417">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2418">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2418">Example</span></span>

```C
/* Install the disconnect complete notify callback function. */
status = nx_tcp_socket_disconnect_complete_notify(&client_socket,
    callback);
```

### <a name="see-also"></a><span data-ttu-id="36624-2419">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2419">See Also</span></span>

- <span data-ttu-id="36624-2420">nx_tcp_enable, nx_tcp_socket_create, nx_tcp_socket_establish_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2420">nx_tcp_enable, nx_tcp_socket_create, nx_tcp_socket_establish_notify,</span></span>
- <span data-ttu-id="36624-2421">nx_tcp_socket_mss_get, nx_tcp_socket_mss_peer_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2421">nx_tcp_socket_mss_get, nx_tcp_socket_mss_peer_get,</span></span>
- <span data-ttu-id="36624-2422">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2422">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span></span>
- <span data-ttu-id="36624-2423">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="36624-2423">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="36624-2424">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="36624-2424">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="36624-2425">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2425">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_establish_notify"></a><span data-ttu-id="36624-2426">nx_tcp_socket_establish_notify</span><span class="sxs-lookup"><span data-stu-id="36624-2426">nx_tcp_socket_establish_notify</span></span>

<span data-ttu-id="36624-2427">TCP kurma bildirimi geri aramasını ayarla işlevi</span><span class="sxs-lookup"><span data-stu-id="36624-2427">Set TCP establish notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2428">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2428">Prototype</span></span>

```C
UINT nx_tcp_socket_establish_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_establish_notify)(NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="36624-2429">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2429">Description</span></span>

<span data-ttu-id="36624-2430">Bu hizmet, bir TCP yuvası bağlantı yaptığında çağrılan bir geri arama işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="36624-2430">This service registers a callback function, which is called after a TCP socket makes a connection.</span></span> <span data-ttu-id="36624-2431">NetX, ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** tanımlı seçeneği ile DERLENIP, TCP yuvası oluşturma geri çağırma işlevi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-2431">The TCP socket establish callback function is available if NetX is built with the option ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** defined.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2432">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2432">Parameters</span></span>

- <span data-ttu-id="36624-2433">**socket_ptr** Daha önce bağlı olan istemci veya sunucu yuvası örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2433">**socket_ptr** Pointer to previously connected client or server socket instance.</span></span>
- <span data-ttu-id="36624-2434">**tcp_establish_notify** Bir TCP bağlantısı kurulduktan sonra geri çağırma işlevi başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="36624-2434">**tcp_establish_notify** Callback function invoked after a TCP connection is established.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2435">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2435">Return Values</span></span>

- <span data-ttu-id="36624-2436">**NX_SUCCESS** (0x00), bildirim işlevini başarıyla ayarlıyor.</span><span class="sxs-lookup"><span data-stu-id="36624-2436">**NX_SUCCESS** (0x00) Successfully sets the notify function.</span></span>
- <span data-ttu-id="36624-2437">**NX_NOT_SUPPORTED** (0x4b) genişletilmiş bildirim özelliği NETX kitaplığında yerleşik değildir</span><span class="sxs-lookup"><span data-stu-id="36624-2437">**NX_NOT_SUPPORTED** (0x4B) The extended notify feature is not built into the NetX library</span></span>
- <span data-ttu-id="36624-2438">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2438">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2439">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2439">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2440">**NX_NOT_ENABLED** (0x14) TCP, uygulama tarafından etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2440">**NX_NOT_ENABLED** (0x14) TCP has not been enabled by the application.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2441">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2441">Allowed From</span></span>

<span data-ttu-id="36624-2442">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2442">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2443">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2443">Preemption Possible</span></span>

<span data-ttu-id="36624-2444">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2444">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2445">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2445">Example</span></span>

```C
/* Set the function pointer "callback" as the notify function NetX
will call when the connection is in the established state. */
status = nx_tcp_socket_establish_notify(&client_socket, callback);
```

### <a name="see-also"></a><span data-ttu-id="36624-2446">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2446">See Also</span></span>

- <span data-ttu-id="36624-2447">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2447">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2448">nx_tcp_socket_disconnect_complete_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2448">nx_tcp_socket_disconnect_complete_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="36624-2449">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="36624-2449">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="36624-2450">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2450">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span></span>
- <span data-ttu-id="36624-2451">nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="36624-2451">nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="36624-2452">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2452">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_info_get"></a><span data-ttu-id="36624-2453">nx_tcp_socket_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-2453">nx_tcp_socket_info_get</span></span>

<span data-ttu-id="36624-2454">TCP yuva etkinlikleri hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="36624-2454">Retrieve information about TCP socket activities</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2455">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2455">Prototype</span></span>

```C
UINT nx_tcp_socket_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *tcp_packets_sent,
    ULONG *tcp_bytes_sent,
    ULONG *tcp_packets_received,
    ULONG *tcp_bytes_received,
    ULONG *tcp_retransmit_packets,
    ULONG *tcp_packets_queued,
    ULONG *tcp_checksum_errors,
    ULONG *tcp_socket_state,
    ULONG *tcp_transmit_queue_depth,
    ULONG *tcp_transmit_window,
    ULONG *tcp_receive_window);
```

### <a name="description"></a><span data-ttu-id="36624-2456">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2456">Description</span></span>

<span data-ttu-id="36624-2457">Bu hizmet, belirtilen TCP yuvası örneği için TCP yuva etkinlikleri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2457">This service retrieves information about TCP socket activities for the specified TCP socket instance.</span></span>

<span data-ttu-id="36624-2458">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-2458">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2459">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2459">Parameters</span></span>

- <span data-ttu-id="36624-2460">**socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2460">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="36624-2461">**tcp_packets_sent** Yuvada Gönderilen TCP paketlerinin toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2461">**tcp_packets_sent** Pointer to destination for the total number of TCP packets sent on socket.</span></span>
- <span data-ttu-id="36624-2462">**tcp_bytes_sent** Yuvada Gönderilen TCP baytlarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2462">**tcp_bytes_sent** Pointer to destination for the total number of TCP bytes sent on socket.</span></span>
- <span data-ttu-id="36624-2463">**tcp_packets_received** Yuvada alınan toplam TCP paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2463">**tcp_packets_received** Pointer to destination of the total number of TCP packets received on socket.</span></span>
- <span data-ttu-id="36624-2464">**tcp_bytes_received** Yuvada alınan TCP baytlarının toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2464">**tcp_bytes_received** Pointer to destination of the total number of TCP bytes received on socket.</span></span>
- <span data-ttu-id="36624-2465">**tcp_retransmit_packets** Toplam TCP paketi yeniden aktarımlar sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2465">**tcp_retransmit_packets** Pointer to destination of the total number of TCP packet retransmissions.</span></span>
- <span data-ttu-id="36624-2466">**tcp_packets_queued** Yuvada sıraya alınan TCP paketlerinin toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2466">**tcp_packets_queued** Pointer to destination of the total number of queued TCP packets on socket.</span></span>
- <span data-ttu-id="36624-2467">**tcp_checksum_errors** Yuvada sağlama toplamı hataları olan toplam TCP paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2467">**tcp_checksum_errors** Pointer to destination of the total number of TCP packets with checksum errors on socket.</span></span>
- <span data-ttu-id="36624-2468">**tcp_socket_state** Yuvanın geçerli durumunun hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2468">**tcp_socket_state** Pointer to destination of the socket’s current state.</span></span>
- <span data-ttu-id="36624-2469">**tcp_transmit_queue_depth** Toplam iletim paketi sayısının hedefe yönelik işaretçisi, hala ACK için bekleyen sıraya alındı.</span><span class="sxs-lookup"><span data-stu-id="36624-2469">**tcp_transmit_queue_depth** Pointer to destination of the total number of transmit packets still queued waiting for ACK.</span></span>
- <span data-ttu-id="36624-2470">**tcp_transmit_window** Geçerli iletme penceresi boyutunun hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2470">**tcp_transmit_window** Pointer to destination of the current transmit window size.</span></span>
- <span data-ttu-id="36624-2471">**tcp_receive_window** Geçerli alma penceresi boyutunun hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2471">**tcp_receive_window** Pointer to destination of the current receive window size.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2472">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2472">Return Values</span></span>

- <span data-ttu-id="36624-2473">**NX_SUCCESS** (0x00) TCP yuvası bilgilerinin alımı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="36624-2473">**NX_SUCCESS** (0x00) Successful TCP socket information retrieval.</span></span>
- <span data-ttu-id="36624-2474">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2474">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2475">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2475">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2476">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2476">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2477">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2477">Return Values</span></span>

```C
/* Retrieve TCP socket information from previously created socket_0.*/
status = nx_tcp_socket_info_get(&socket_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_retransmit_packets,
    &tcp_packets_queued,
    &tcp_checksum_errors,
    &tcp_socket_state,
    &tcp_transmit_queue_depth,
    &tcp_transmit_window,
    &tcp_receive_window);

/* If status is NX_SUCCESS, TCP socket information was retrieved. */
```

### <a name="allowed-from"></a><span data-ttu-id="36624-2478">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2478">Allowed From</span></span>

<span data-ttu-id="36624-2479">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2479">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2480">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2480">Preemption Possible</span></span>

<span data-ttu-id="36624-2481">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2481">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2482">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2482">Example</span></span>

```C
/* Retrieve TCP socket information from previously created socket_0.*/
status = nx_tcp_socket_info_get(&socket_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_retransmit_packets,
    &tcp_packets_queued,
    &tcp_checksum_errors,
    &tcp_socket_state,
    &tcp_transmit_queue_depth,
    &tcp_transmit_window,
    &tcp_receive_window);

/* If status is NX_SUCCESS, TCP socket information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2483">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2483">See Also</span></span>

- <span data-ttu-id="36624-2484">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2484">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2485">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2485">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2486">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2486">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2487">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2487">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2488">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="36624-2488">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="36624-2489">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2489">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2490">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2490">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2491">nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,</span><span class="sxs-lookup"><span data-stu-id="36624-2491">nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,</span></span>
- <span data-ttu-id="36624-2492">nx_tcp_socket_send, nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2492">nx_tcp_socket_send, nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_mss_get"></a><span data-ttu-id="36624-2493">nx_tcp_socket_mss_get</span><span class="sxs-lookup"><span data-stu-id="36624-2493">nx_tcp_socket_mss_get</span></span>

<span data-ttu-id="36624-2494">Yuvanın düzeyini al</span><span class="sxs-lookup"><span data-stu-id="36624-2494">Get MSS of socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2495">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2495">Prototype</span></span>

```C
UINT nx_tcp_socket_mss_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a><span data-ttu-id="36624-2496">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2496">Description</span></span>

<span data-ttu-id="36624-2497">Bu hizmet, belirtilen yuvanın yerel en büyük kesim boyutunu (Bu) alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2497">This service retrieves the specified socket's local Maximum Segment Size (MSS).</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2498">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2498">Parameters</span></span>

- <span data-ttu-id="36624-2499">**socket_ptr** Daha önce oluşturulmuş yuvanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2499">**socket_ptr** Pointer to previously created socket.</span></span>
- <span data-ttu-id="36624-2500"> , ' İ döndürmek için hedef.</span><span class="sxs-lookup"><span data-stu-id="36624-2500">**mss** Destination for returning MSS.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2501">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2501">Return Values</span></span>

- <span data-ttu-id="36624-2502">**NX_SUCCESS** (0x00) başarılı bir wget al.</span><span class="sxs-lookup"><span data-stu-id="36624-2502">**NX_SUCCESS** (0x00) Successful MSS get.</span></span>
- <span data-ttu-id="36624-2503">**NX_PTR_ERROR** (0x07) geçersiz yuva veya kaynak hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2503">**NX_PTR_ERROR** (0x07) Invalid socket or MSS destination pointer.</span></span>
- <span data-ttu-id="36624-2504">**NX_NOT_ENABLED** (0x14) TCP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2504">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="36624-2505">**NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2505">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2506">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2506">Allowed From</span></span>

<span data-ttu-id="36624-2507">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2507">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2508">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2508">Preemption Possible</span></span>

<span data-ttu-id="36624-2509">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2509">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2510">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2510">Example</span></span>

```C
/* Get the MSS for the socket "my_socket". */
status = nx_tcp_socket_mss_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
    socket's current MSS value. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2511">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2511">See Also</span></span>

- <span data-ttu-id="36624-2512">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2512">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2513">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2513">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="36624-2514">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_peer_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2514">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_peer_get,</span></span>
- <span data-ttu-id="36624-2515">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2515">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span></span>
- <span data-ttu-id="36624-2516">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="36624-2516">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="36624-2517">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="36624-2517">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="36624-2518">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2518">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_mss_peer_get"></a><span data-ttu-id="36624-2519">nx_tcp_socket_mss_peer_get</span><span class="sxs-lookup"><span data-stu-id="36624-2519">nx_tcp_socket_mss_peer_get</span></span>

<span data-ttu-id="36624-2520">Eş TCP yuvasının düzeyini alın</span><span class="sxs-lookup"><span data-stu-id="36624-2520">Get MSS of the peer TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2521">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2521">Prototype</span></span>

```C
UINT nx_tcp_socket_mss_peer_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a><span data-ttu-id="36624-2522">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2522">Description</span></span>

<span data-ttu-id="36624-2523">Bu hizmet, Eş yuva tarafından tanıtılan en büyük kesim boyutunu (,) alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2523">This service retrieves the Maximum Segment Size (MSS) advertised by the peer socket.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2524">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2524">Parameters</span></span>

- <span data-ttu-id="36624-2525">**socket_ptr** Daha önce oluşturulmuş ve bağlı yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2525">**socket_ptr** Pointer to previously created and connected socket.</span></span>
- <span data-ttu-id="36624-2526"> , ' İ döndürmek için hedef.</span><span class="sxs-lookup"><span data-stu-id="36624-2526">**mss** Destination for returning the MSS.</span></span>


### <a name="return-values"></a><span data-ttu-id="36624-2527">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2527">Return Values</span></span>

- <span data-ttu-id="36624-2528">**NX_SUCCESS** (0x00) başarılı eş ve Get.</span><span class="sxs-lookup"><span data-stu-id="36624-2528">**NX_SUCCESS** (0x00) Successful peer MSS get.</span></span>
- <span data-ttu-id="36624-2529">**NX_PTR_ERROR** (0x07) geçersiz yuva veya kaynak hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2529">**NX_PTR_ERROR** (0x07) Invalid socket or MSS destination pointer.</span></span>
- <span data-ttu-id="36624-2530">**NX_NOT_ENABLED** (0x14) TCP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2530">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="36624-2531">**NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2531">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2532">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2532">Allowed From</span></span>

<span data-ttu-id="36624-2533">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2533">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2534">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2534">Preemption Possible</span></span>

<span data-ttu-id="36624-2535">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2535">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2536">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2536">Example</span></span>

```C
/* Get the MSS of the connected peer to the socket "my_socket". */
status = nx_tcp_socket_mss_peer_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
    socket peer’s advertised MSS value. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2537">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2537">See Also</span></span>

- <span data-ttu-id="36624-2538">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2538">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2539">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2539">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="36624-2540">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2540">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="36624-2541">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2541">nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,</span></span>
- <span data-ttu-id="36624-2542">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="36624-2542">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="36624-2543">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="36624-2543">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="36624-2544">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2544">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_mss_set"></a><span data-ttu-id="36624-2545">nx_tcp_socket_mss_set</span><span class="sxs-lookup"><span data-stu-id="36624-2545">nx_tcp_socket_mss_set</span></span>

<span data-ttu-id="36624-2546">Yuvanın düzeyini ayarla</span><span class="sxs-lookup"><span data-stu-id="36624-2546">Set MSS of socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2547">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2547">Prototype</span></span>

```C
UINT nx_tcp_socket_mss_set(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG mss);
```

### <a name="description"></a><span data-ttu-id="36624-2548">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2548">Description</span></span>

<span data-ttu-id="36624-2549">Bu hizmet, belirtilen yuvanın en büyük kesim boyutunu (Bu) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36624-2549">This service sets the specified socket's Maximum Segment Size (MSS).</span></span> <span data-ttu-id="36624-2550">Bu değer, IP ve TCP üstbilgileri için odaya izin veren ağ arabirimi IP MTU 'SU içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-2550">Note the MSS value must be within the network interface IP MTU, allowing room for IP and TCP headers.</span></span>

<span data-ttu-id="36624-2551">Bu hizmet, TCP yuvası bağlantı işlemini başlatılmadan önce kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-2551">This service should be used before a TCP socket starts the connection process.</span></span> <span data-ttu-id="36624-2552">Hizmet bir TCP bağlantısı kurulduktan sonra kullanılıyorsa, yeni değerin bağlantı üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="36624-2552">If the service is used after a TCP connection is established, the new value has no effect on the connection.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2553">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2553">Parameters</span></span>

- <span data-ttu-id="36624-2554">**socket_ptr** Daha önce oluşturulmuş yuvanın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2554">**socket_ptr** Pointer to previously created socket.</span></span>
- <span data-ttu-id="36624-2555"> , Ayarlanacak bir sahip değeri.</span><span class="sxs-lookup"><span data-stu-id="36624-2555">**mss** Value of MSS to set.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2556">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2556">Return Values</span></span>

- <span data-ttu-id="36624-2557">**NX_SUCCESS** (0x00) başarılı bir Wonu kümesi.</span><span class="sxs-lookup"><span data-stu-id="36624-2557">**NX_SUCCESS** (0x00) Successful MSS set.</span></span>
- <span data-ttu-id="36624-2558">**NX_SIZE_ERROR** (0x09) belirtilen '% ' değeri çok büyük.</span><span class="sxs-lookup"><span data-stu-id="36624-2558">**NX_SIZE_ERROR** (0x09) Specified MSS value is too large.</span></span>
- <span data-ttu-id="36624-2559">**NX_NOT_CONNECTED** (0x38) TCP bağlantısı kurulmadı</span><span class="sxs-lookup"><span data-stu-id="36624-2559">**NX_NOT_CONNECTED** (0x38) TCP connection has not been established</span></span>
- <span data-ttu-id="36624-2560">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2560">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2561">**NX_NOT_ENABLED** (0x14) TCP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2561">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="36624-2562">**NX_CALLER_ERROR** (0x11) çağıran bir iş parçacığı veya başlatma değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2562">**NX_CALLER_ERROR** (0x11) Caller is not a thread or initialization.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2563">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2563">Allowed From</span></span>

<span data-ttu-id="36624-2564">Başlatma ve iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2564">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2565">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2565">Preemption Possible</span></span>

<span data-ttu-id="36624-2566">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2566">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2567">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2567">Example</span></span>

```C
/* Set the MSS of the socket "my_socket" to 1000 bytes. */
status = nx_tcp_socket_mss_set(&my_socket, 1000);

/* If status is NX_SUCCESS, the MSS of "my_socket" is 1000 bytes. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2568">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2568">See Also</span></span>

- <span data-ttu-id="36624-2569">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2569">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2570">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2570">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="36624-2571">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2571">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="36624-2572">nx_tcp_socket_mss_peer_get, nx_tcp_socket_peer_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2572">nx_tcp_socket_mss_peer_get, nx_tcp_socket_peer_info_get,</span></span>
- <span data-ttu-id="36624-2573">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="36624-2573">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="36624-2574">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="36624-2574">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="36624-2575">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2575">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_peer_info_get"></a><span data-ttu-id="36624-2576">nx_tcp_socket_peer_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-2576">nx_tcp_socket_peer_info_get</span></span>

<span data-ttu-id="36624-2577">Eş TCP soketi hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="36624-2577">Retrieve information about peer TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2578">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2578">Prototype</span></span>

```C
UINT nx_tcp_socket_peer_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *peer_ip_address, 
    ULONG *peer_port);
```

### <a name="description"></a><span data-ttu-id="36624-2579">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2579">Description</span></span>

<span data-ttu-id="36624-2580">Bu hizmet, bağlı TCP yuvasının IP ağı üzerinden eş IP adresini ve bağlantı noktası bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2580">This service retrieves peer IP address and port information for the connected TCP socket over IP network.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2581">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2581">Parameters</span></span>

- <span data-ttu-id="36624-2582">**socket_ptr** Daha önce oluşturulan TCP yuvasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2582">**socket_ptr** Pointer to previously created TCP socket.</span></span>
- <span data-ttu-id="36624-2583">**peer_ip_address** Konak bayt düzeninde eş IP adresi hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2583">**peer_ip_address** Pointer to destination for peer IP address, in host byte order.</span></span>
- <span data-ttu-id="36624-2584">**peer_port** Ana bilgisayar bayt düzeninde eş bağlantı noktası numarası için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2584">**peer_port** Pointer to destination for peer port number, in host byte order.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2585">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2585">Return Values</span></span>

- <span data-ttu-id="36624-2586">**NX_SUCCESS** (0x00) hizmeti başarıyla çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2586">**NX_SUCCESS** (0x00) Service executes successfully.</span></span> <span data-ttu-id="36624-2587">Eş IP adresi ve bağlantı noktası numarası çağırana döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-2587">Peer IP address and port number are returned to the caller.</span></span>
- <span data-ttu-id="36624-2588">**NX_NOT_CONNECTED** (0x38) yuva bağlı durumda değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2588">**NX_NOT_CONNECTED** (0x38) Socket is not in a connected state.</span></span>
- <span data-ttu-id="36624-2589">**NX_PTR_ERROR** (0x07) geçersiz işaretçiler.</span><span class="sxs-lookup"><span data-stu-id="36624-2589">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="36624-2590">**NX_NOT_ENABLED** (0x14) TCP etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2590">**NX_NOT_ENABLED** (0x14) TCP is not enabled.</span></span>
- <span data-ttu-id="36624-2591">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2591">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2592">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2592">Allowed From</span></span>

<span data-ttu-id="36624-2593">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2593">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2594">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2594">Preemption Possible</span></span>

<span data-ttu-id="36624-2595">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2595">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2596">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2596">Example</span></span>

```C
/* Obtain peer IP address and port on the specified TCP socket. */
status = nx_tcp_socket_peer_info_get(&my_socket, &peer_ip_address,
    &peer_port);

/* If status = NX_SUCCESS, the data was successfully obtained. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2597">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2597">See Also</span></span>

- <span data-ttu-id="36624-2598">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2598">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2599">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2599">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="36624-2600">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2600">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="36624-2601">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="36624-2601">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="36624-2602">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="36624-2602">nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="36624-2603">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="36624-2603">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="36624-2604">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2604">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_receive"></a><span data-ttu-id="36624-2605">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="36624-2605">nx_tcp_socket_receive</span></span>

<span data-ttu-id="36624-2606">TCP yuvasından veri al</span><span class="sxs-lookup"><span data-stu-id="36624-2606">Receive data from TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2607">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2607">Prototype</span></span>

```C
UINT nx_tcp_socket_receive(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-2608">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2608">Description</span></span>

<span data-ttu-id="36624-2609">Bu hizmet, belirtilen yuvadan TCP verileri alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2609">This service receives TCP data from the specified socket.</span></span> <span data-ttu-id="36624-2610">Belirtilen yuvada hiçbir veri sıraya alınmaz, çağıran, sağlanan bekleme seçeneğine göre askıya alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2610">If no data are queued on the specified socket, the caller suspends based on the supplied wait option.</span></span>

<span data-ttu-id="36624-2611">*NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur.*</span><span class="sxs-lookup"><span data-stu-id="36624-2611">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2612">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2612">Parameters</span></span>

- <span data-ttu-id="36624-2613">**socket_ptr** Daha önce oluşturulan TCP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2613">**socket_ptr** Pointer to previously created TCP socket instance.</span></span>
- <span data-ttu-id="36624-2614">**packet_ptr** TCP paket işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2614">**packet_ptr** Pointer to TCP packet pointer.</span></span>
- <span data-ttu-id="36624-2615">**wait_option** Şu anda bu yuvada sıraya alınmış veri yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-2615">**wait_option** Defines how the service behaves if no data are currently queued on this socket.</span></span> <span data-ttu-id="36624-2616">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-2616">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-2617">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-2617">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-2618">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-2618">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-2619">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-2619">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2620">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2620">Return Values</span></span>
- <span data-ttu-id="36624-2621">**NX_SUCCESS** (0x00) başarılı yuva verileri alma.</span><span class="sxs-lookup"><span data-stu-id="36624-2621">**NX_SUCCESS** (0x00) Successful socket data receive.</span></span>
- <span data-ttu-id="36624-2622">**NX_NOT_BOUND** (0x24) yuva henüz bağlanmamış.</span><span class="sxs-lookup"><span data-stu-id="36624-2622">**NX_NOT_BOUND** (0x24) Socket is not bound yet.</span></span>
- <span data-ttu-id="36624-2623">**NX_NO_PACKET** (0x01) veri alınmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-2623">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="36624-2624">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-2624">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-2625">**NX_NOT_CONNECTED** (0x38) yuva artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2625">**NX_NOT_CONNECTED** (0x38) The socket is no longer connected.</span></span>
- <span data-ttu-id="36624-2626">**NX_PTR_ERROR** (0x07) geçersiz yuva veya dönüş paketi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2626">**NX_PTR_ERROR** (0x07) Invalid socket or return packet pointer.</span></span>
- <span data-ttu-id="36624-2627">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2627">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2628">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2628">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2629">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2629">Allowed From</span></span>

<span data-ttu-id="36624-2630">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2630">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2631">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2631">Preemption Possible</span></span>

<span data-ttu-id="36624-2632">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2632">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2633">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2633">Example</span></span>

<span data-ttu-id="36624-2634">/\* Önceden oluşturulmuş ve bağlı TCP istemci yuvasından bir paket alın.</span><span class="sxs-lookup"><span data-stu-id="36624-2634">/\* Receive a packet from the previously created and connected TCP client socket.</span></span> <span data-ttu-id="36624-2635">Kullanılabilir bir paket yoksa, vermeden önce 200 Zamanlayıcı onay işareti bekleyin.</span><span class="sxs-lookup"><span data-stu-id="36624-2635">If no packet is available, wait for 200 timer ticks before giving up.</span></span> <span data-ttu-id="36624-2636">\*/Status = nx_tcp_socket_receive (&client_socket, &packet_ptr, 200);</span><span class="sxs-lookup"><span data-stu-id="36624-2636">\*/ status = nx_tcp_socket_receive(&client_socket, &packet_ptr, 200);</span></span>

<span data-ttu-id="36624-2637">/\* Durum NX_SUCCESS ise, alınan paket "packet_ptr" tarafından işaret edilir.</span><span class="sxs-lookup"><span data-stu-id="36624-2637">/\* If status is NX_SUCCESS, the received packet is pointed to by "packet_ptr".</span></span> */

### <a name="see-also"></a><span data-ttu-id="36624-2638">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2638">See Also</span></span>

- <span data-ttu-id="36624-2639">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2639">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2640">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2640">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2641">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2641">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2642">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2642">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2643">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="36624-2643">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="36624-2644">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2644">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2645">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2645">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2646">nx_tcp_socket_info_get, nx_tcp_socket_receive_queue_max_set,</span><span class="sxs-lookup"><span data-stu-id="36624-2646">nx_tcp_socket_info_get, nx_tcp_socket_receive_queue_max_set,</span></span>
- <span data-ttu-id="36624-2647">nx_tcp_socket_send, nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2647">nx_tcp_socket_send, nx_tcp_socket_state_wait</span></span>

## <a name="nx_tcp_socket_receive_notify"></a><span data-ttu-id="36624-2648">nx_tcp_socket_receive_notify</span><span class="sxs-lookup"><span data-stu-id="36624-2648">nx_tcp_socket_receive_notify</span></span>

<span data-ttu-id="36624-2649">Alınan paketlerin uygulamasına bildirme</span><span class="sxs-lookup"><span data-stu-id="36624-2649">Notify application of received packets</span></span>


### <a name="prototype"></a><span data-ttu-id="36624-2650">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2650">Prototype</span></span>

```C
UINT nx_tcp_socket_receive_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_receive_notify) (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="36624-2651">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2651">Description</span></span>

<span data-ttu-id="36624-2652">Bu hizmet, bildirim al işlev işaretçisini uygulama tarafından belirtilen geri çağırma işleviyle yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="36624-2652">This service configures the receive notify function pointer with the callback function specified by the application.</span></span> <span data-ttu-id="36624-2653">Bu geri çağırma işlevi, daha sonra yuvada bir veya daha fazla paket alındığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2653">This callback function is then called whenever one or more packets are received on the socket.</span></span> <span data-ttu-id="36624-2654">NX_NULL bir işaretçi sağlanırsa, bildir işlevi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2654">If a NX_NULL pointer is supplied, the notify function is disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2655">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2655">Parameters</span></span>

- <span data-ttu-id="36624-2656">**socket_ptr** TCP yuvasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2656">**socket_ptr** Pointer to the TCP socket.</span></span>
- <span data-ttu-id="36624-2657">**tcp_receive_notify** Yuvada bir veya daha fazla paket alındığında çağrılan uygulama geri çağırma işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2657">**tcp_receive_notify** Application callback function pointer that is called when one or more packets are received on the socket.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2658">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2658">Return Values</span></span>

- <span data-ttu-id="36624-2659">**NX_SUCCESS** (0x00) başarılı yuva alma bildirimi.</span><span class="sxs-lookup"><span data-stu-id="36624-2659">**NX_SUCCESS** (0x00) Successful socket receive notify.</span></span>
- <span data-ttu-id="36624-2660">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2660">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2661">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2661">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2662">**NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2662">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2663">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2663">Allowed From</span></span>

<span data-ttu-id="36624-2664">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2664">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2665">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2665">Preemption Possible</span></span>

<span data-ttu-id="36624-2666">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2666">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2667">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2667">Example</span></span>

```C
/* Setup a receive packet callback function for the "client_socket"
socket. */
status = nx_tcp_socket_receive_notify(&client_socket,
    my_receive_notify);

/* If status is NX_SUCCESS, NetX will call the function named
    "my_receive_notify" whenever one or more packets are received for
    "client_socket". */
```

### <a name="see-also"></a><span data-ttu-id="36624-2668">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2668">See Also</span></span>

- <span data-ttu-id="36624-2669">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2669">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2670">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2670">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="36624-2671">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2671">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="36624-2672">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="36624-2672">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="36624-2673">nx_tcp_socket_peer_info_get, nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="36624-2673">nx_tcp_socket_peer_info_get, nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="36624-2674">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="36624-2674">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="36624-2675">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2675">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_send"></a><span data-ttu-id="36624-2676">nx_tcp_socket_send</span><span class="sxs-lookup"><span data-stu-id="36624-2676">nx_tcp_socket_send</span></span>

<span data-ttu-id="36624-2677">TCP yuvası üzerinden veri gönderme</span><span class="sxs-lookup"><span data-stu-id="36624-2677">Send data through a TCP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2678">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2678">Prototype</span></span>

```C
UINT nx_tcp_socket_send(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-2679">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2679">Description</span></span>

<span data-ttu-id="36624-2680">Bu hizmet, TCP verilerini daha önce bağlı bir TCP yuvası üzerinden gönderir.</span><span class="sxs-lookup"><span data-stu-id="36624-2680">This service sends TCP data through a previously connected TCP socket.</span></span> <span data-ttu-id="36624-2681">Alıcının en son tanıtılan pencere boyutu bu istekten azsa, hizmet isteğe bağlı olarak, belirtilen bekleme seçeneğine göre askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="36624-2681">If the receiver's last advertised window size is less than this request, the service optionally suspends based on the wait option specified.</span></span> <span data-ttu-id="36624-2682">Bu hizmet, IP katmanına, \ ' dan daha büyük bir paket verisi gönderilmesini güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2682">This service guarantees that no packet data larger than MSS is sent to the IP layer.</span></span>

<span data-ttu-id="36624-2683">*Bir hata döndürülmediği takdirde, uygulama bu çağrıdan sonra paketi serbest bırakmamalıdır. Bunu yapmak öngörülemeyen sonuçlara neden olur çünkü ağ sürücüsü iletim sonrasında paketi serbest bırakmaya da çalışacaktır.*</span><span class="sxs-lookup"><span data-stu-id="36624-2683">*Unless an error is returned, the application should not release the packet after this call. Doing so will cause unpredictable results because the network driver will also try to release the packet after transmission.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2684">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2684">Parameters</span></span>

- <span data-ttu-id="36624-2685">**socket_ptr** Daha önce bağlı TCP yuvası örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2685">**socket_ptr** Pointer to previously connected TCP socket instance.</span></span>
- <span data-ttu-id="36624-2686">**packet_ptr** TCP veri paketi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2686">**packet_ptr** TCP data packet pointer.</span></span>
- <span data-ttu-id="36624-2687">**wait_option** İstek alıcının pencere boyutundan fazlaysa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-2687">**wait_option** Defines how the service behaves if the request is greater than the window size of the receiver.</span></span> <span data-ttu-id="36624-2688">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-2688">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-2689">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-2689">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-2690">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-2690">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-2691">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-2691">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2692">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2692">Return Values</span></span>

- <span data-ttu-id="36624-2693">**NX_SUCCESS** (0x00) başarılı yuva gönderme.</span><span class="sxs-lookup"><span data-stu-id="36624-2693">**NX_SUCCESS** (0x00) Successful socket send.</span></span>
- <span data-ttu-id="36624-2694">**NX_NOT_BOUND** (0x24) yuva herhangi bir bağlantı noktasına bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-2694">**NX_NOT_BOUND** (0x24) Socket was not bound to any port.</span></span>
- <span data-ttu-id="36624-2695">**NX_NO_INTERFACE_ADDRESS** (0x50) uygun giden arabirim bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="36624-2695">**NX_NO_INTERFACE_ADDRESS** (0x50) No suitable outgoing interface found.</span></span>
- <span data-ttu-id="36624-2696">**NX_NOT_CONNECTED** (0x38) yuva artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2696">**NX_NOT_CONNECTED** (0x38) Socket is no longer connected.</span></span>
- <span data-ttu-id="36624-2697">**NX_WINDOW_OVERFLOW** (0x39) isteği, alıcının tanıtılan pencere boyutundan bayt cinsinden daha büyük.</span><span class="sxs-lookup"><span data-stu-id="36624-2697">**NX_WINDOW_OVERFLOW** (0x39) Request is greater than receiver’s advertised window size in bytes.</span></span>
- <span data-ttu-id="36624-2698">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-2698">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-2699">**NX_INVALID_PACKET** (0x12) paketi ayrılmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-2699">**NX_INVALID_PACKET** (0x12) Packet is not allocated.</span></span>
- <span data-ttu-id="36624-2700">**NX_TX_QUEUE_DEPTH** (0x49) en yüksek iletim sırası derinliğine ulaşıldı.</span><span class="sxs-lookup"><span data-stu-id="36624-2700">**NX_TX_QUEUE_DEPTH** (0x49) Maximum transmit queue depth has been reached.</span></span>
- <span data-ttu-id="36624-2701">**NX_OVERFLOW** (0x03) paket ekleme işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-2701">**NX_OVERFLOW** (0x03) Packet append pointer is invalid.</span></span>
- <span data-ttu-id="36624-2702">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2702">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2703">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2703">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2704">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2704">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-2705">**NX_UNDERFLOW** (0x02) paket önüne işaretçisi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-2705">**NX_UNDERFLOW** (0x02) Packet prepend pointer is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2706">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2706">Allowed From</span></span>

<span data-ttu-id="36624-2707">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2707">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2708">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2708">Preemption Possible</span></span>

<span data-ttu-id="36624-2709">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2709">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2710">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2710">Example</span></span>

```C
/* Send a packet out on the previously created and connected TCP
    socket. If the receive window on the other side of the connection
    is less than the packet size, wait 200 timer ticks before giving up. */
status = nx_tcp_socket_send(&client_socket, packet_ptr, 200);

/* If status is NX_SUCCESS, the packet has been sent! */
```

### <a name="see-also"></a><span data-ttu-id="36624-2711">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2711">See Also</span></span>

- <span data-ttu-id="36624-2712">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2712">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2713">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2713">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2714">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2714">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2715">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2715">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2716">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="36624-2716">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="36624-2717">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2717">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2718">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2718">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2719">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2719">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2720">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2720">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_state_wait</span></span>

### <a name="nx_tcp_socket_state_wait"></a><span data-ttu-id="36624-2721">nx_tcp_socket_state_wait</span><span class="sxs-lookup"><span data-stu-id="36624-2721">nx_tcp_socket_state_wait</span></span>

<span data-ttu-id="36624-2722">TCP yuvasının belirli bir durumu girmesini bekleyin</span><span class="sxs-lookup"><span data-stu-id="36624-2722">Wait for TCP socket to enter specific state</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2723">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2723">Prototype</span></span>

```C
UINT nx_tcp_socket_state_wait(
    NX_TCP_SOCKET *socket_ptr,
    UINT desired_state, 
    ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="36624-2724">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2724">Description</span></span>

<span data-ttu-id="36624-2725">Bu hizmet, yuvanın istenen durumu girmesini bekler.</span><span class="sxs-lookup"><span data-stu-id="36624-2725">This service waits for the socket to enter the desired state.</span></span> <span data-ttu-id="36624-2726">Yuva istenen durumda değilse, hizmet sağlanan bekleme seçeneğine göre askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="36624-2726">If the socket is not in the desired state, the service suspends according to the supplied wait option.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2727">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2727">Parameters</span></span>

- <span data-ttu-id="36624-2728">**socket_ptr** Daha önce bağlı TCP yuvası örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2728">**socket_ptr** Pointer to previously connected TCP socket instance.</span></span>
- <span data-ttu-id="36624-2729">**desired_state** İstenen TCP durumu.</span><span class="sxs-lookup"><span data-stu-id="36624-2729">**desired_state** Desired TCP state.</span></span> <span data-ttu-id="36624-2730">Geçerli TCP yuvası durumları şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-2730">Valid TCP socket states are defined as follows:</span></span>
- <span data-ttu-id="36624-2731">NX_TCP_CLOSED (0x01)</span><span class="sxs-lookup"><span data-stu-id="36624-2731">NX_TCP_CLOSED (0x01)</span></span>
- <span data-ttu-id="36624-2732">NX_TCP_LISTEN_STATE (0x02)</span><span class="sxs-lookup"><span data-stu-id="36624-2732">NX_TCP_LISTEN_STATE (0x02)</span></span>
- <span data-ttu-id="36624-2733">NX_TCP_SYN_SENT (0x03)</span><span class="sxs-lookup"><span data-stu-id="36624-2733">NX_TCP_SYN_SENT (0x03)</span></span>
- <span data-ttu-id="36624-2734">NX_TCP_SYN_RECEIVED (0x04)</span><span class="sxs-lookup"><span data-stu-id="36624-2734">NX_TCP_SYN_RECEIVED (0x04)</span></span>
- <span data-ttu-id="36624-2735">NX_TCP_ESTABLISHED (0x05)</span><span class="sxs-lookup"><span data-stu-id="36624-2735">NX_TCP_ESTABLISHED (0x05)</span></span>
- <span data-ttu-id="36624-2736">NX_TCP_CLOSE_WAIT (0x06)</span><span class="sxs-lookup"><span data-stu-id="36624-2736">NX_TCP_CLOSE_WAIT (0x06)</span></span>
- <span data-ttu-id="36624-2737">NX_TCP_FIN_WAIT_1 (0x07)</span><span class="sxs-lookup"><span data-stu-id="36624-2737">NX_TCP_FIN_WAIT_1 (0x07)</span></span>
- <span data-ttu-id="36624-2738">NX_TCP_FIN_WAIT_2 (0x08)</span><span class="sxs-lookup"><span data-stu-id="36624-2738">NX_TCP_FIN_WAIT_2 (0x08)</span></span>
- <span data-ttu-id="36624-2739">NX_TCP_CLOSING (0x09)</span><span class="sxs-lookup"><span data-stu-id="36624-2739">NX_TCP_CLOSING (0x09)</span></span>
- <span data-ttu-id="36624-2740">NX_TCP_TIMED_WAIT (0x0A)</span><span class="sxs-lookup"><span data-stu-id="36624-2740">NX_TCP_TIMED_WAIT (0x0A)</span></span>
- <span data-ttu-id="36624-2741">NX_TCP_LAST_ACK (0x0B)</span><span class="sxs-lookup"><span data-stu-id="36624-2741">NX_TCP_LAST_ACK (0x0B)</span></span>
- <span data-ttu-id="36624-2742">**wait_option** İstenen durum yoksa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-2742">**wait_option** Defines how the service behaves if the requested state is not present.</span></span> <span data-ttu-id="36624-2743">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-2743">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-2744">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-2744">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-2745">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-2745">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-2746">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-2746">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2747">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2747">Return Values</span></span>
- <span data-ttu-id="36624-2748">**NX_SUCCESS** (0x00) başarılı durum bekleme.</span><span class="sxs-lookup"><span data-stu-id="36624-2748">**NX_SUCCESS** (0x00) Successful state wait.</span></span>
- <span data-ttu-id="36624-2749">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2749">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2750">**NX_NOT_SUCCESSFUL** (0x43) belirtilen bekleme süresi içinde mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2750">**NX_NOT_SUCCESSFUL** (0x43) State not present within the specified wait time.</span></span>
- <span data-ttu-id="36624-2751">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-2751">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-2752">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2752">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2753">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2753">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-2754">**NX_OPTION_ERROR** (0x0A) istenen yuva durumu geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-2754">**NX_OPTION_ERROR** (0x0A) The desired socket state is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2755">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2755">Allowed From</span></span>

<span data-ttu-id="36624-2756">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2756">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2757">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2757">Preemption Possible</span></span>

<span data-ttu-id="36624-2758">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2758">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2759">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2759">Example</span></span>

```C
/* Wait 300 timer ticks for the previously created socket to enter
    the established state in the TCP state machine. */
status = nx_tcp_socket_state_wait(&client_socket,
    NX_TCP_ESTABLISHED, 300);

/* If status is NX_SUCCESS, the socket is now in the established
    state! */
```

### <a name="see-also"></a><span data-ttu-id="36624-2760">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2760">See Also</span></span>

- <span data-ttu-id="36624-2761">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span><span class="sxs-lookup"><span data-stu-id="36624-2761">nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,</span></span>
- <span data-ttu-id="36624-2762">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2762">nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,</span></span>
- <span data-ttu-id="36624-2763">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2763">nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,</span></span>
- <span data-ttu-id="36624-2764">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span><span class="sxs-lookup"><span data-stu-id="36624-2764">nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,</span></span>
- <span data-ttu-id="36624-2765">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span><span class="sxs-lookup"><span data-stu-id="36624-2765">nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,</span></span>
- <span data-ttu-id="36624-2766">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2766">nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2767">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span><span class="sxs-lookup"><span data-stu-id="36624-2767">nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,</span></span>
- <span data-ttu-id="36624-2768">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2768">nx_tcp_socket_info_get, nx_tcp_socket_receive,</span></span>
- <span data-ttu-id="36624-2769">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send</span><span class="sxs-lookup"><span data-stu-id="36624-2769">nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send</span></span>

## <a name="nx_tcp_socket_timed_wait_callback"></a><span data-ttu-id="36624-2770">nx_tcp_socket_timed_wait_callback</span><span class="sxs-lookup"><span data-stu-id="36624-2770">nx_tcp_socket_timed_wait_callback</span></span>

<span data-ttu-id="36624-2771">Zamanlanmış bekleme durumu için geri çağırma 'yi yükler</span><span class="sxs-lookup"><span data-stu-id="36624-2771">Install callback for timed wait state</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2772">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2772">Prototype</span></span>

```C
UINT nx_tcp_socket_timed_wait_callback(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_timed_wait_callback) (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="36624-2773">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2773">Description</span></span>

<span data-ttu-id="36624-2774">Bu hizmet, TCP yuvası zamanlanmış bekleme durumunda olduğunda çağrılan bir geri arama işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="36624-2774">This service registers a callback function which is invoked when the TCP socket is in timed wait state.</span></span> <span data-ttu-id="36624-2775">Bu hizmeti kullanmak için, NetX kitaplığı tanımlı ***NX_ENABLE_EXTENDED_NOTIFY*** seçeneği ile oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-2775">To use this service, the NetX library must be built with the option ***NX_ENABLE_EXTENDED_NOTIFY*** defined.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2776">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2776">Parameters</span></span>

- <span data-ttu-id="36624-2777">**socket_ptr** Daha önce bağlı olan istemci veya sunucu yuvası örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2777">**socket_ptr** Pointer to previously connected client or server socket instance.</span></span>
- <span data-ttu-id="36624-2778">**tcp_timed_wait_callback** Zamanlanmış geri çağırma işlevi</span><span class="sxs-lookup"><span data-stu-id="36624-2778">**tcp_timed_wait_callback** The timed wait callback function</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2779">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2779">Return Values</span></span>

- <span data-ttu-id="36624-2780">**NX_SUCCESS** (0x00) geri çağırma Işlevi yuvasını başarıyla kaydeder</span><span class="sxs-lookup"><span data-stu-id="36624-2780">**NX_SUCCESS** (0x00) Successfully registers the callback function socket</span></span>
- <span data-ttu-id="36624-2781">**NX_NOT_SUPPORTED** (0x4b) NETX kitaplığı, genişletilmiş bildirim özelliği etkin olmadan oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="36624-2781">**NX_NOT_SUPPORTED** (0x4B) NetX library is built without the extended notify feature enabled.</span></span>
- <span data-ttu-id="36624-2782">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2782">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2783">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2783">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2784">**NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2784">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2785">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2785">Allowed From</span></span>

<span data-ttu-id="36624-2786">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2786">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2787">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2787">Preemption Possible</span></span>

<span data-ttu-id="36624-2788">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2788">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2789">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2789">Example</span></span>

```C
/* Install the timed wait callback function */
nx_tcp_socket_timed_wait_callback(&client_socket, callback);
```

### <a name="see-also"></a><span data-ttu-id="36624-2790">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2790">See Also</span></span>

- <span data-ttu-id="36624-2791">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2791">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2792">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2792">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="36624-2793">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2793">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="36624-2794">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="36624-2794">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="36624-2795">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2795">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span></span>
- <span data-ttu-id="36624-2796">nx_tcp_socket_transmit_configure,</span><span class="sxs-lookup"><span data-stu-id="36624-2796">nx_tcp_socket_transmit_configure,</span></span>
- <span data-ttu-id="36624-2797">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2797">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_transmit_configure"></a><span data-ttu-id="36624-2798">nx_tcp_socket_transmit_configure</span><span class="sxs-lookup"><span data-stu-id="36624-2798">nx_tcp_socket_transmit_configure</span></span>

<span data-ttu-id="36624-2799">Yuvanın iletim parametrelerini Yapılandır</span><span class="sxs-lookup"><span data-stu-id="36624-2799">Configure socket's transmit parameters</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2800">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2800">Prototype</span></span>

```C
UINT nx_tcp_socket_transmit_configure(
    NX_TCP_SOCKET *socket_ptr,
    ULONG max_queue_depth,
    ULONG timeout,
    ULONG max_retries,
    ULONG timeout_shift);
```

### <a name="description"></a><span data-ttu-id="36624-2801">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2801">Description</span></span>

<span data-ttu-id="36624-2802">Bu hizmet, belirtilen TCP yuvasının çeşitli iletim parametrelerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="36624-2802">This service configures various transmit parameters of the specified TCP socket.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2803">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2803">Parameters</span></span>

- <span data-ttu-id="36624-2804">**socket_ptr** TCP yuvasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2804">**socket_ptr** Pointer to the TCP socket.</span></span>
- <span data-ttu-id="36624-2805">**max_queue_depth** İletim için sıraya izin verilen en fazla paket sayısı.</span><span class="sxs-lookup"><span data-stu-id="36624-2805">**max_queue_depth** Maximum number of packets allowed to be queued for transmission.</span></span>
- <span data-ttu-id="36624-2806">**zaman aşımı** Paket yeniden gönderilmeden önce bir ACK değeri için ThreadX Zamanlayıcı onay işareti sayısı bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="36624-2806">**timeout** Number of ThreadX timer ticks an ACK is waited for before the packet is sent again.</span></span>
- <span data-ttu-id="36624-2807">**max_retries** İzin verilen en fazla yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="36624-2807">**max_retries** Maximum number of retries allowed.</span></span>
- <span data-ttu-id="36624-2808">**timeout_shift** Sonraki yeniden denemelerde zaman aşımını kaydırmak için değer.</span><span class="sxs-lookup"><span data-stu-id="36624-2808">**timeout_shift** Value to shift the timeout for each subsequent retry.</span></span> <span data-ttu-id="36624-2809">0 değeri, sonraki yeniden denemeler arasındaki aynı zaman aşımı ile sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="36624-2809">A value of 0, results in the same timeout between successive retries.</span></span> <span data-ttu-id="36624-2810">1 değeri, yeniden denemeler arasındaki zaman aşımını iki katına çıkarır.</span><span class="sxs-lookup"><span data-stu-id="36624-2810">A value of 1, doubles the timeout between retries.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2811">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2811">Return Values</span></span>
- <span data-ttu-id="36624-2812">**NX_SUCCESS** (0x00) başarılı iletme yuvası yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="36624-2812">**NX_SUCCESS** (0x00) Successful transmit socket configure.</span></span>
- <span data-ttu-id="36624-2813">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2813">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-2814">**NX_OPTION_ERROR** (0x0A) sıra derinliği seçeneği geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-2814">**NX_OPTION_ERROR** (0x0a) Invalid queue depth option.</span></span>
- <span data-ttu-id="36624-2815">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2815">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2816">**NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2816">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2817">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2817">Allowed From</span></span>

<span data-ttu-id="36624-2818">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2818">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2819">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2819">Preemption Possible</span></span>

<span data-ttu-id="36624-2820">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2820">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2821">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2821">Example</span></span>

```C
/* Configure the "client_socket" for a maximum transmit queue depth
    of 12, 100 tick timeouts, a maximum of 20 retries, and a timeout
    double on each successive retry. */
status = nx_tcp_socket_transmit_configure(&client_socket,
    12,100,20, 1);

/* If status is NX_SUCCESS, the socket’s transmit retry has been
    configured. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2822">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2822">See Also</span></span>

- <span data-ttu-id="36624-2823">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2823">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2824">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2824">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="36624-2825">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2825">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="36624-2826">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="36624-2826">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="36624-2827">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2827">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span></span>
- <span data-ttu-id="36624-2828">nx_tcp_socket_timed_wait_callback,</span><span class="sxs-lookup"><span data-stu-id="36624-2828">nx_tcp_socket_timed_wait_callback,</span></span>
- <span data-ttu-id="36624-2829">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2829">nx_tcp_socket_window_update_notify_set</span></span>

## <a name="nx_tcp_socket_window_update_notify_set"></a><span data-ttu-id="36624-2830">nx_tcp_socket_window_update_notify_set</span><span class="sxs-lookup"><span data-stu-id="36624-2830">nx_tcp_socket_window_update_notify_set</span></span>

<span data-ttu-id="36624-2831">Pencere boyutu güncelleştirmelerinin uygulamasını bilgilendir</span><span class="sxs-lookup"><span data-stu-id="36624-2831">Notify application of window size updates</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2832">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2832">Prototype</span></span>

```C
UINT nx_tcp_socket_window_update_notify_set(
    NX_TCP_SOCKET
    *socket_ptr,
    VOID (*tcp_window_update_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="36624-2833">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2833">Description</span></span>

<span data-ttu-id="36624-2834">Bu hizmet, bir yuva penceresi güncelleştirme geri arama yordamını yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="36624-2834">This service installs a socket window update callback routine.</span></span> <span data-ttu-id="36624-2835">Bu yordam, belirtilen yuva uzak konağın pencere boyutunda bir artışı gösteren bir paket aldığında otomatik olarak çağrılır.</span><span class="sxs-lookup"><span data-stu-id="36624-2835">This routine is called automatically whenever the specified socket receives a packet indicating an increase in the window size of the remote host.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2836">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2836">Parameters</span></span>

- <span data-ttu-id="36624-2837">**socket_ptr** Daha önce oluşturulan TCP yuvasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2837">**socket_ptr** Pointer to previously created TCP socket.</span></span>
- <span data-ttu-id="36624-2838">**tcp_window_update_notify** Pencere boyutu değiştiğinde çağrılacak geri arama yordamı.</span><span class="sxs-lookup"><span data-stu-id="36624-2838">**tcp_window_update_notify** Callback routine to be called when the window size changes.</span></span> <span data-ttu-id="36624-2839">NULL değeri, pencere değişikliğini güncelleştirmeyi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="36624-2839">A value of NULL disables the window change update.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2840">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2840">Return Values</span></span>
- <span data-ttu-id="36624-2841">**NX_SUCCESS** (0x00) geri çağırma yordamı yuvaya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="36624-2841">**NX_SUCCESS** (0x00) Callback routine is installed on the socket.</span></span>
- <span data-ttu-id="36624-2842">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2842">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2843">**NX_PTR_ERROR** (0x07) geçersiz işaretçiler.</span><span class="sxs-lookup"><span data-stu-id="36624-2843">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="36624-2844">**NX_NOT_ENABLED** (0x14) TCP özelliği etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-2844">**NX_NOT_ENABLED** (0x14) TCP feature is not enabled.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="36624-2845">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2845">Allowed From</span></span>

<span data-ttu-id="36624-2846">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2846">Initialization, threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2847">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2847">Preemption Possible</span></span>

<span data-ttu-id="36624-2848">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2848">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2849">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2849">Example</span></span>

```C
/* Set the function pointer to the windows update callback after creating the
socket. */
status = nx_tcp_socket_window_update_notify_set(&data_socket,
    my_windows_update_callback);

/* Define the window callback function in the host application. */
void my_windows_update_callback(NX_TCP_SCOCKET *data_socket)
{
    /* Process update on increase TCP transmit socket window size. */
    return;
}
```

### <a name="see-also"></a><span data-ttu-id="36624-2850">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2850">See Also</span></span>

- <span data-ttu-id="36624-2851">nx_tcp_enable, nx_tcp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-2851">nx_tcp_enable, nx_tcp_socket_create,</span></span>
- <span data-ttu-id="36624-2852">nx_tcp_socket_disconnect_complete_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2852">nx_tcp_socket_disconnect_complete_notify,</span></span>
- <span data-ttu-id="36624-2853">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2853">nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,</span></span>
- <span data-ttu-id="36624-2854">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span><span class="sxs-lookup"><span data-stu-id="36624-2854">nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,</span></span>
- <span data-ttu-id="36624-2855">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-2855">nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,</span></span>
- <span data-ttu-id="36624-2856">nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure</span><span class="sxs-lookup"><span data-stu-id="36624-2856">nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure</span></span>

## <a name="nx_udp_enable"></a><span data-ttu-id="36624-2857">nx_udp_enable</span><span class="sxs-lookup"><span data-stu-id="36624-2857">nx_udp_enable</span></span>

<span data-ttu-id="36624-2858">NetX 'in UDP bileşenini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-2858">Enable UDP component of NetX</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2859">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2859">Prototype</span></span>

```C
UINT nx_udp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-2860">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2860">Description</span></span>

<span data-ttu-id="36624-2861">Bu hizmet, NetX 'in Kullanıcı Datagram Protokolü (UDP) bileşenini sunar.</span><span class="sxs-lookup"><span data-stu-id="36624-2861">This service enables the User Datagram Protocol (UDP) component of NetX.</span></span> <span data-ttu-id="36624-2862">Etkinleştirildikten sonra, uygulama tarafından UDP veri birimleri gönderilebilir ve alınabilir.</span><span class="sxs-lookup"><span data-stu-id="36624-2862">After enabled, UDP datagrams may be sent and received by the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2863">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2863">Parameters</span></span>

- <span data-ttu-id="36624-2864">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2864">**ip_ptr** Pointer to previously created IP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2865">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2865">Return Values</span></span>

- <span data-ttu-id="36624-2866">**NX_SUCCESS** (0x00) başarıyla UDP etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-2866">**NX_SUCCESS** (0x00) Successful UDP enable.</span></span>
- <span data-ttu-id="36624-2867">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2867">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-2868">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2868">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2869">**NX_ALREADY_ENABLED** (0x15) Bu bileşen zaten etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2869">**NX_ALREADY_ENABLED** (0x15) This component has already been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2870">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2870">Allowed From</span></span>

<span data-ttu-id="36624-2871">Başlatma, iş parçacıkları, zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="36624-2871">Initialization, threads, timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2872">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2872">Preemption Possible</span></span>

<span data-ttu-id="36624-2873">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2873">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2874">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2874">Example</span></span>

```C
/* Enable UDP on the previously created IP instance. */
status = nx_udp_enable(&ip_0);

/* If status is NX_SUCCESS, UDP is now enabled on the specified IP
    instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2875">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2875">See Also</span></span>

- <span data-ttu-id="36624-2876">nx_udp_free_port_find, nx_udp_info_get, nx_udp_packet_info_extract,</span><span class="sxs-lookup"><span data-stu-id="36624-2876">nx_udp_free_port_find, nx_udp_info_get, nx_udp_packet_info_extract,</span></span>
- <span data-ttu-id="36624-2877">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2877">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2878">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-2878">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="36624-2879">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2879">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-2880">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2880">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-2881">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2881">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-2882">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2882">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="36624-2883">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-2883">nx_udp_source_extract</span></span>

## <a name="nx_udp_free_port_find"></a><span data-ttu-id="36624-2884">nx_udp_free_port_find</span><span class="sxs-lookup"><span data-stu-id="36624-2884">nx_udp_free_port_find</span></span>

<span data-ttu-id="36624-2885">Sonraki kullanılabilir UDP bağlantı noktasını bul</span><span class="sxs-lookup"><span data-stu-id="36624-2885">Find next available UDP port</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2886">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2886">Prototype</span></span>

```C
UINT nx_udp_free_port_find(
    NX_IP *ip_ptr, 
    UINT port,
    UINT *free_port_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-2887">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2887">Description</span></span>

<span data-ttu-id="36624-2888">Bu hizmet, uygulama tarafından sağlanan bağlantı noktası numarasından başlayarak ücretsiz bir UDP bağlantı noktası (ilişkisiz) arar.</span><span class="sxs-lookup"><span data-stu-id="36624-2888">This service looks for a free UDP port (unbound) starting from the application supplied port number.</span></span> <span data-ttu-id="36624-2889">Arama mantığı, en fazla 0xFFFF bağlantı noktası değerine ulaşırsa, arama mantığı sarmalacaktır.</span><span class="sxs-lookup"><span data-stu-id="36624-2889">The search logic will wrap around if the search reaches the maximum port value of 0xFFFF.</span></span> <span data-ttu-id="36624-2890">Arama başarılı olursa, *free_port_ptr* tarafından işaret edilen değişkende boş bağlantı noktası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="36624-2890">If the search is successful, the free port is returned in the variable pointed to by *free_port_ptr*.</span></span>

<span data-ttu-id="36624-2891">*Bu hizmet başka bir iş parçacığından çağrılabilir ve aynı bağlantı noktasına geri dönüş yapılabilir. Bu yarış durumunu engellemek için, uygulama bu hizmeti ve gerçek yuva bağlamasını bir mutex 'in altına yerleştirmek isteyebilir.*</span><span class="sxs-lookup"><span data-stu-id="36624-2891">*This service can be called from another thread and can have the same port returned. To prevent this race condition, the application may wish to place this service and the actual socket bind under the protection of a mutex.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2892">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2892">Parameters</span></span>

- <span data-ttu-id="36624-2893">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2893">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-2894">**bağlantı noktası** Aramaya başlamak için bağlantı noktası numarası (1 ile 0xFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="36624-2894">**port** Port number to start search (1 through 0xFFFF).</span></span>
- <span data-ttu-id="36624-2895">**free_port_ptr** Hedef boş bağlantı noktası dönüş değişkenine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2895">**free_port_ptr** Pointer to the destination free port return variable.</span></span>


### <a name="return-values"></a><span data-ttu-id="36624-2896">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2896">Return Values</span></span>

- <span data-ttu-id="36624-2897">**NX_SUCCESS** (0x00) başarılı boş bağlantı noktası bul.</span><span class="sxs-lookup"><span data-stu-id="36624-2897">**NX_SUCCESS** (0x00) Successful free port find.</span></span>
- <span data-ttu-id="36624-2898">**NX_NO_FREE_PORTS** (0x45) boş bağlantı noktası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="36624-2898">**NX_NO_FREE_PORTS** (0x45) No free ports found.</span></span>
- <span data-ttu-id="36624-2899">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2899">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-2900">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2900">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2901">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2901">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>
- <span data-ttu-id="36624-2902">**NX_INVALID_PORT** (0x46) belirtilen bağlantı noktası numarası geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-2902">**NX_INVALID_PORT** (0x46) Specified port number is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2903">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2903">Allowed From</span></span>

<span data-ttu-id="36624-2904">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2904">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2905">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2905">Preemption Possible</span></span>

<span data-ttu-id="36624-2906">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2906">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2907">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2907">Example</span></span>

```C
/* Locate a free UDP port, starting at port 12, on a previously
    created IP instance. */
status = nx_udp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS pointer, "free_port" identifies the next
    free UDP port on the IP instance. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2908">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2908">See Also</span></span>

- <span data-ttu-id="36624-2909">nx_udp_enable, nx_udp_info_get, nx_udp_packet_info_extract,</span><span class="sxs-lookup"><span data-stu-id="36624-2909">nx_udp_enable, nx_udp_info_get, nx_udp_packet_info_extract,</span></span>
- <span data-ttu-id="36624-2910">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2910">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2911">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-2911">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="36624-2912">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2912">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-2913">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2913">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-2914">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2914">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-2915">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2915">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="36624-2916">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-2916">nx_udp_source_extract</span></span>

## <a name="nx_udp_info_get"></a><span data-ttu-id="36624-2917">nx_udp_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-2917">nx_udp_info_get</span></span>

<span data-ttu-id="36624-2918">UDP etkinlikleri hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="36624-2918">Retrieve information about UDP activities</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2919">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2919">Prototype</span></span>

```C
UINT nx_udp_info_get(
    NX_IP *ip_ptr,
    ULONG *udp_packets_sent,
    ULONG *udp_bytes_sent,
    ULONG *udp_packets_received,
    ULONG *udp_bytes_received,
    ULONG *udp_invalid_packets,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
```

### <a name="description"></a><span data-ttu-id="36624-2920">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2920">Description</span></span>

<span data-ttu-id="36624-2921">Bu hizmet, belirtilen IP örneği için UDP etkinlikleriyle ilgili bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="36624-2921">This service retrieves information about UDP activities for the specified IP instance.</span></span>

<span data-ttu-id="36624-2922">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-2922">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2923">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2923">Parameters</span></span>

- <span data-ttu-id="36624-2924">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2924">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-2925">**udp_packets_sent** Gönderilen toplam UDP paketi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2925">**udp_packets_sent** Pointer to destination for the total number of UDP packets sent.</span></span>
- <span data-ttu-id="36624-2926">**udp_bytes_sent** Gönderilen toplam UDP bayt sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2926">**udp_bytes_sent** Pointer to destination for the total number of UDP bytes sent.</span></span>
- <span data-ttu-id="36624-2927">**udp_packets_received** Alınan toplam UDP paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2927">**udp_packets_received** Pointer to destination of the total number of UDP packets received.</span></span>
- <span data-ttu-id="36624-2928">**udp_bytes_received** Alınan UDP baytlarının toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2928">**udp_bytes_received** Pointer to destination of the total number of UDP bytes received.</span></span>
- <span data-ttu-id="36624-2929">**udp_invalid_packets** Toplam geçersiz UDP paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2929">**udp_invalid_packets** Pointer to destination of the total number of invalid UDP packets.</span></span>
- <span data-ttu-id="36624-2930">**udp_receive_packets_dropped** Bırakılan UDP alma paketlerinin toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2930">**udp_receive_packets_dropped** Pointer to destination of the total number of UDP receive packets dropped.</span></span>
- <span data-ttu-id="36624-2931">**udp_checksum_errors** Toplam UDP paketi sayısının sağlama toplamı hataları olan hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2931">**udp_checksum_errors** Pointer to destination of the total number of UDP packets with checksum errors.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2932">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2932">Return Values</span></span>

- <span data-ttu-id="36624-2933">**NX_SUCCESS** (0x00) başarılı UDP bilgisi alma.</span><span class="sxs-lookup"><span data-stu-id="36624-2933">**NX_SUCCESS** (0x00) Successful UDP information retrieval.</span></span>
- <span data-ttu-id="36624-2934">**NX_PTR_ERROR** (0x07) geçersiz IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2934">**NX_PTR_ERROR** (0x07) Invalid IP pointer.</span></span>
- <span data-ttu-id="36624-2935">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2935">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-2936">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-2936">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="36624-2937">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2937">Allowed From</span></span>

<span data-ttu-id="36624-2938">Başlatma, iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="36624-2938">Initialization, threads, and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2939">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2939">Preemption Possible</span></span>

<span data-ttu-id="36624-2940">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2940">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2941">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2941">Example</span></span>

```C
/* Retrieve UDP information from previously created IP Instance ip_0. */
status = nx_udp_info_get(&ip_0, &udp_packets_sent,
    &udp_bytes_sent,
    &udp_packets_received,
    &udp_bytes_received,
    &udp_invalid_packets,
    &udp_receive_packets_dropped,
    &udp_checksum_errors);

/* If status is NX_SUCCESS, UDP information was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2942">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2942">See Also</span></span>

- <span data-ttu-id="36624-2943">nx_udp_enable, nx_udp_free_port_find, nx_udp_packet_info_extract,</span><span class="sxs-lookup"><span data-stu-id="36624-2943">nx_udp_enable, nx_udp_free_port_find, nx_udp_packet_info_extract,</span></span>
- <span data-ttu-id="36624-2944">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2944">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2945">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-2945">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="36624-2946">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2946">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-2947">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2947">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-2948">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2948">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-2949">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2949">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="36624-2950">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-2950">nx_udp_source_extract</span></span>

## <a name="nx_udp_packet_info_extract"></a><span data-ttu-id="36624-2951">nx_udp_packet_info_extract</span><span class="sxs-lookup"><span data-stu-id="36624-2951">nx_udp_packet_info_extract</span></span>

<span data-ttu-id="36624-2952">UDP paketindeki ağ parametrelerini Ayıkla</span><span class="sxs-lookup"><span data-stu-id="36624-2952">Extract network parameters from UDP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2953">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2953">Prototype</span></span>

```C
UINT nx_udp_packet_info_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address,
    UINT *protocol,
    UINT *port,
    UINT *interface_index);
```

### <a name="description"></a><span data-ttu-id="36624-2954">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2954">Description</span></span>

<span data-ttu-id="36624-2955">Bu hizmet, IP adresi, eş bağlantı noktası numarası, protokol türü (Bu hizmet her zaman UDP türünü döndürür) gibi ağ parametrelerini, gelen bir arabirimde alınan bir paketten ayıklar.</span><span class="sxs-lookup"><span data-stu-id="36624-2955">This service extracts network parameters, such as IP address, peer port number, protocol type (this service always returns UDP type) from a packet received on an incoming interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2956">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2956">Parameters</span></span>

- <span data-ttu-id="36624-2957">**packet_ptr** Paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2957">**packet_ptr** Pointer to packet.</span></span>
- <span data-ttu-id="36624-2958">**ip_address** Gönderenin IP adresi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2958">**ip_address** Pointer to sender IP address.</span></span>
- <span data-ttu-id="36624-2959">**protokol** Protokol işaretçisi (UDP).</span><span class="sxs-lookup"><span data-stu-id="36624-2959">**protocol** Pointer to protocol (UDP).</span></span>
- <span data-ttu-id="36624-2960">**bağlantı noktası** Gönderenin bağlantı noktası numarası işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2960">**port** Pointer to sender’s port number.</span></span>
- <span data-ttu-id="36624-2961">**interface_index** Arabirim dizini alma işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-2961">**interface_index** Pointer to receiving interface index.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2962">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2962">Return Values</span></span>

- <span data-ttu-id="36624-2963">**NX_SUCCESS** (0x00) paket arabirimi verileri başarıyla ayıklandı.</span><span class="sxs-lookup"><span data-stu-id="36624-2963">**NX_SUCCESS** (0x00) Packet interface data successfully extracted.</span></span>
- <span data-ttu-id="36624-2964">**NX_INVALID_PACKET** (0x12) PAKETI, IP çerçevesi içermiyor.</span><span class="sxs-lookup"><span data-stu-id="36624-2964">**NX_INVALID_PACKET** (0x12) Packet does not contain IP frame.</span></span>
- <span data-ttu-id="36624-2965">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="36624-2965">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="36624-2966">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-2966">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-2967">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-2967">Allowed From</span></span>

<span data-ttu-id="36624-2968">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-2968">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-2969">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-2969">Preemption Possible</span></span>

<span data-ttu-id="36624-2970">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-2970">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-2971">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-2971">Example</span></span>

```C
/* Extract network data from UDP packet interface.*/
status = nx_udp_packet_info_extract( packet_ptr, &ip_address,
    &protocol, &port,
    &interface_index);

/* If status is NX_SUCCESS packet data was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="36624-2972">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-2972">See Also</span></span>

- <span data-ttu-id="36624-2973">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2973">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-2974">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-2974">nx_udp_socket_bind, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-2975">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-2975">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="36624-2976">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-2976">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-2977">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-2977">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-2978">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-2978">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-2979">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-2979">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="36624-2980">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-2980">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_bind"></a><span data-ttu-id="36624-2981">nx_udp_socket_bind</span><span class="sxs-lookup"><span data-stu-id="36624-2981">nx_udp_socket_bind</span></span>

<span data-ttu-id="36624-2982">UDP yuvasını UDP bağlantı noktasına bağla</span><span class="sxs-lookup"><span data-stu-id="36624-2982">Bind UDP socket to UDP port</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-2983">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-2983">Prototype</span></span>

```C
UINT nx_udp_socket_bind(
    NX_UDP_SOCKET *socket_ptr, 
    UINT port,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-2984">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-2984">Description</span></span>

<span data-ttu-id="36624-2985">Bu hizmet, önceden oluşturulan UDP yuvasını belirtilen UDP bağlantı noktasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="36624-2985">This service binds the previously created UDP socket to the specified UDP port.</span></span> <span data-ttu-id="36624-2986">Geçerli UDP yuvaları 0 ile 0xFFFF arasındadır.</span><span class="sxs-lookup"><span data-stu-id="36624-2986">Valid UDP sockets range from 0 through 0xFFFF.</span></span> <span data-ttu-id="36624-2987">İstenen bağlantı noktası numarası başka bir yuvaya bağlıysa, bu hizmet, yuvanın bağlantı noktası numarasından bağlantısını kesmek için belirtilen süre boyunca bekler.</span><span class="sxs-lookup"><span data-stu-id="36624-2987">If the requested port number is bound to another socket, this service waits for specified period of time for the socket to unbind from the port number.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-2988">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-2988">Parameters</span></span>

- <span data-ttu-id="36624-2989">**socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-2989">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>
- <span data-ttu-id="36624-2990">**bağlantı noktası** Bağlanacak bağlantı noktası numarası (1 ile 0xFFFF arasında).</span><span class="sxs-lookup"><span data-stu-id="36624-2990">**port** Port number to bind to (1 through 0xFFFF).</span></span> <span data-ttu-id="36624-2991">Bağlantı noktası numarası NX_ANY_PORT (0x0000) ise, IP örneği bir sonraki boş bağlantı noktasını arar ve bu bağlantıyı bağlama için kullanır.</span><span class="sxs-lookup"><span data-stu-id="36624-2991">If port number is NX_ANY_PORT (0x0000), the IP instance will search for the next free port and use that for the binding.</span></span>
- <span data-ttu-id="36624-2992">**wait_option** Bağlantı noktası zaten başka bir yuvaya bağlanmışsa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-2992">**wait_option** Defines how the service behaves if the port is already bound to another socket.</span></span> <span data-ttu-id="36624-2993">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-2993">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-2994">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-2994">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-2995">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-2995">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-2996">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-2996">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-2997">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-2997">Return Values</span></span>

- <span data-ttu-id="36624-2998">**NX_SUCCESS** (0x00) başarılı yuva bağlaması.</span><span class="sxs-lookup"><span data-stu-id="36624-2998">**NX_SUCCESS** (0x00) Successful socket bind.</span></span>
- <span data-ttu-id="36624-2999">**NX_ALREADY_BOUND** (0x22) bu yuva zaten başka bir bağlantı noktasına bağlıydı.</span><span class="sxs-lookup"><span data-stu-id="36624-2999">**NX_ALREADY_BOUND** (0x22) This socket is already bound to another port.</span></span>
- <span data-ttu-id="36624-3000">**NX_PORT_UNAVAILABLE** (0x23) bağlantı noktası zaten farklı bir yuvaya bağlıydı.</span><span class="sxs-lookup"><span data-stu-id="36624-3000">**NX_PORT_UNAVAILABLE** (0x23) Port is already bound to a different socket.</span></span>
- <span data-ttu-id="36624-3001">**NX_NO_FREE_PORTS** (0x45) boş bağlantı noktası yok.</span><span class="sxs-lookup"><span data-stu-id="36624-3001">**NX_NO_FREE_PORTS** (0x45) No free port.</span></span>
- <span data-ttu-id="36624-3002">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği tx_thread_wait_abort bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="36624-3002">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to tx_thread_wait_abort.</span></span>
- <span data-ttu-id="36624-3003">**NX_INVALID_PORT** (0x46) geçersiz bağlantı noktası belirtildi.</span><span class="sxs-lookup"><span data-stu-id="36624-3003">**NX_INVALID_PORT** (0x46) Invalid port specified.</span></span>
- <span data-ttu-id="36624-3004">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3004">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-3005">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3005">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-3006">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-3006">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3007">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3007">Allowed From</span></span>

<span data-ttu-id="36624-3008">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-3008">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3009">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3009">Preemption Possible</span></span>

<span data-ttu-id="36624-3010">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3010">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3011">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3011">Example</span></span>

```C
/* Bind the previously created UDP socket to port 12 on the
    previously created IP instance. If the port is already bound,
    wait for 300 timer ticks before giving up. */
status = nx_udp_socket_bind(&udp_socket, 12, 300);

/* If status is NX_SUCCESS, the UDP socket is now bound to
    port 12.*/
```

### <a name="see-also"></a><span data-ttu-id="36624-3012">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3012">See Also</span></span>

- <span data-ttu-id="36624-3013">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3013">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3014">nx_udp_packet_info_extract, nx_udp_socket_bytes_available,</span><span class="sxs-lookup"><span data-stu-id="36624-3014">nx_udp_packet_info_extract, nx_udp_socket_bytes_available,</span></span>
- <span data-ttu-id="36624-3015">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-3015">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="36624-3016">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3016">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3017">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-3017">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-3018">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3018">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-3019">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-3019">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="36624-3020">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3020">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_bytes_available"></a><span data-ttu-id="36624-3021">nx_udp_socket_bytes_available</span><span class="sxs-lookup"><span data-stu-id="36624-3021">nx_udp_socket_bytes_available</span></span>

<span data-ttu-id="36624-3022">Alma için kullanılabilir bayt sayısını alır</span><span class="sxs-lookup"><span data-stu-id="36624-3022">Retrieves number of bytes available for retrieval</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3023">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3023">Prototype</span></span>

```C
UINT nx_udp_socket_bytes_available(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```

### <a name="description"></a><span data-ttu-id="36624-3024">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3024">Description</span></span>

<span data-ttu-id="36624-3025">Bu hizmet, belirtilen UDP yuvasında alım için kullanılabilen bayt sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="36624-3025">This service retrieves number of bytes available for reception in the specified UDP socket.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3026">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3026">Parameters</span></span>

- <span data-ttu-id="36624-3027">**socket_ptr** Daha önce oluşturulan UDP yuvasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3027">**socket_ptr** Pointer to previously created UDP socket.</span></span>
- <span data-ttu-id="36624-3028">**bytes_available** Kullanılabilir baytlar için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3028">**bytes_available** Pointer to destination for bytes available.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3029">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3029">Return Values</span></span>

- <span data-ttu-id="36624-3030">**NX_SUCCESS** (0x00) başarılı bayt kullanılabilir alma.</span><span class="sxs-lookup"><span data-stu-id="36624-3030">**NX_SUCCESS** (0x00) Successful bytes available retrieval.</span></span>
- <span data-ttu-id="36624-3031">**NX_NOT_SUCCESSFUL** (0x43) yuva bir bağlantı noktasına bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-3031">**NX_NOT_SUCCESSFUL** (0x43) Socket not bound to a port.</span></span>
- <span data-ttu-id="36624-3032">**NX_PTR_ERROR** (0x07) geçersiz işaretçiler.</span><span class="sxs-lookup"><span data-stu-id="36624-3032">**NX_PTR_ERROR** (0x07) Invalid pointers.</span></span>
- <span data-ttu-id="36624-3033">**NX_NOT_ENABLED** (0x14) UDP özelliği etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-3033">**NX_NOT_ENABLED** (0x14) UDP feature is not enabled.</span></span>
- <span data-ttu-id="36624-3034">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3034">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3035">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3035">Allowed From</span></span>

<span data-ttu-id="36624-3036">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-3036">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3037">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3037">Preemption Possible</span></span>

<span data-ttu-id="36624-3038">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3038">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3039">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3039">Example</span></span>

```C
/* Get the bytes available for retrieval from the UDP socket. */
status = nx_udp_socket_bytes_available(&my_socket, &bytes_available);

/* If status == NX_SUCCESS, the number of bytes was successfully
    retrieved.*/
```

### <a name="see-also"></a><span data-ttu-id="36624-3040">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3040">See Also</span></span>

- <span data-ttu-id="36624-3041">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3041">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3042">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3042">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3043">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span><span class="sxs-lookup"><span data-stu-id="36624-3043">nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,</span></span>
- <span data-ttu-id="36624-3044">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3044">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3045">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-3045">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-3046">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3046">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-3047">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-3047">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="36624-3048">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3048">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_checksum_disable"></a><span data-ttu-id="36624-3049">nx_udp_socket_checksum_disable</span><span class="sxs-lookup"><span data-stu-id="36624-3049">nx_udp_socket_checksum_disable</span></span>

<span data-ttu-id="36624-3050">UDP yuvası için sağlama toplamını devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="36624-3050">Disable checksum for UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3051">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3051">Prototype</span></span>

```C
UINT nx_udp_socket_checksum_disable(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-3052">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3052">Description</span></span>

<span data-ttu-id="36624-3053">Bu hizmet, belirtilen UDP yuvasında paketleri göndermek ve almak için sağlama toplamı mantığını devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="36624-3053">This service disables the checksum logic for sending and receiving packets on the specified UDP socket.</span></span> <span data-ttu-id="36624-3054">Sağlama toplamı mantığı devre dışı bırakıldığında, bu yuva aracılığıyla gönderilen tüm paketler için UDP üstbilgisinin sağlama toplamı alanına sıfır değeri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="36624-3054">When the checksum logic is disabled, a value of zero is loaded into the UDP header's checksum field for all packets sent through this socket.</span></span> <span data-ttu-id="36624-3055">UDP üst bilgisindeki sıfır değerli sağlama toplamı değeri, bu paket için sağlama toplamı hesaplanmayan alıcıyı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="36624-3055">A zero-value checksum value in the UDP header signals the receiver that checksum is not computed for this packet.</span></span>

<span data-ttu-id="36624-3056">Ayrıca, sırasıyla UDP paketlerini alırken ve gönderirken, bu, ***NX_DISABLE_UDP_RX_CHECKSUM** _ ve _ *_NX_DISABLE_UDP_TX_CHECKSUM_** tanımlı bir etkiye sahip olmadığına de unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-3056">Also note that this has no effect if ***NX_DISABLE_UDP_RX_CHECKSUM** _ and _ *_NX_DISABLE_UDP_TX_CHECKSUM_** are defined when receiving and sending UDP packets respectively.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3057">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3057">Parameters</span></span>

- <span data-ttu-id="36624-3058">**socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3058">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3059">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3059">Return Values</span></span>

- <span data-ttu-id="36624-3060">**NX_SUCCESS** (0x00) başarılı yuva sağlama toplamı devre dışı.</span><span class="sxs-lookup"><span data-stu-id="36624-3060">**NX_SUCCESS** (0x00) Successful socket checksum disable.</span></span>
- <span data-ttu-id="36624-3061">**NX_NOT_BOUND** (0x24) yuva bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-3061">**NX_NOT_BOUND** (0x24) Socket is not bound.</span></span>
- <span data-ttu-id="36624-3062">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3062">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-3063">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3063">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-3064">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-3064">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3065">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3065">Allowed From</span></span>

<span data-ttu-id="36624-3066">Başlatma, iş parçacıkları, süreölçer</span><span class="sxs-lookup"><span data-stu-id="36624-3066">Initialization, threads, timer</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3067">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3067">Preemption Possible</span></span>

<span data-ttu-id="36624-3068">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3068">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3069">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3069">Example</span></span>

```C
/* Disable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_disable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will not have a checksum
    calculated. */
```

### <a name="see-also"></a><span data-ttu-id="36624-3070">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3070">See Also</span></span>

- <span data-ttu-id="36624-3071">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3071">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3072">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3072">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3073">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3073">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3074">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3074">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3075">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-3075">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-3076">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3076">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-3077">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-3077">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="36624-3078">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3078">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_checksum_enable"></a><span data-ttu-id="36624-3079">nx_udp_socket_checksum_enable</span><span class="sxs-lookup"><span data-stu-id="36624-3079">nx_udp_socket_checksum_enable</span></span>

<span data-ttu-id="36624-3080">UDP yuvası için sağlama toplamını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36624-3080">Enable checksum for UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3081">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3081">Prototype</span></span>

```C
UINT nx_udp_socket_checksum_enable(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-3082">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3082">Description</span></span>

<span data-ttu-id="36624-3083">Bu hizmet, belirtilen UDP yuvasında paket göndermek ve almak için sağlama toplamı mantığını sunar.</span><span class="sxs-lookup"><span data-stu-id="36624-3083">This service enables the checksum logic for sending and receiving packets on the specified UDP socket.</span></span> <span data-ttu-id="36624-3084">Sağlama toplamı, tüm UDP veri alanının yanı sıra sözde IP üst bilgisini de içerir.</span><span class="sxs-lookup"><span data-stu-id="36624-3084">The checksum covers the entire UDP data area as well as a pseudo IP header.</span></span>

<span data-ttu-id="36624-3085">Ayrıca, **NX_DISABLE_UDP_RX_CHECKSUM** ve **NX_DISABLE_UDP_TX_CHECKSUM** , sırasıyla UDP paketlerini alırken ve gönderirken tanımlanmış bir etkiye sahip olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-3085">Also note that this has no effect if **NX_DISABLE_UDP_RX_CHECKSUM** and **NX_DISABLE_UDP_TX_CHECKSUM** are defined when receiving and sending UDP packets respectively.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3086">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3086">Parameters</span></span>

- <span data-ttu-id="36624-3087">**socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3087">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3088">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3088">Return Values</span></span>

- <span data-ttu-id="36624-3089">**NX_SUCCESS** (0x00) başarılı yuva sağlama toplamı etkin.</span><span class="sxs-lookup"><span data-stu-id="36624-3089">**NX_SUCCESS** (0x00) Successful socket checksum enable.</span></span>
- <span data-ttu-id="36624-3090">**NX_NOT_BOUND** (0x24) yuva bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-3090">**NX_NOT_BOUND** (0x24) Socket is not bound.</span></span>
- <span data-ttu-id="36624-3091">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3091">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-3092">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3092">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-3093">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-3093">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3094">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3094">Allowed From</span></span>

<span data-ttu-id="36624-3095">Başlatma, iş parçacıkları, süreölçer</span><span class="sxs-lookup"><span data-stu-id="36624-3095">Initialization, threads, timer</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3096">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3096">Preemption Possible</span></span>

<span data-ttu-id="36624-3097">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3097">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3098">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3098">Example</span></span>

```C
/* Enable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_enable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will have a checksum
    calculated. */
```

### <a name="see-also"></a><span data-ttu-id="36624-3099">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3099">See Also</span></span>

- <span data-ttu-id="36624-3100">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3100">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3101">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3101">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3102">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3102">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3103">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3103">nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3104">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-3104">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-3105">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3105">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-3106">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-3106">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="36624-3107">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3107">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_create"></a><span data-ttu-id="36624-3108">nx_udp_socket_create</span><span class="sxs-lookup"><span data-stu-id="36624-3108">nx_udp_socket_create</span></span>

<span data-ttu-id="36624-3109">UDP yuvası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="36624-3109">Create UDP socket.</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3110">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3110">Prototype</span></span>

```C
UINT nx_udp_socket_create(
    NX_IP *ip_ptr,
    NX_UDP_SOCKET *socket_ptr, CHAR *name,
    ULONG type_of_service, ULONG fragment,
    UINT time_to_live, ULONG queue_maximum);
```

### <a name="description"></a><span data-ttu-id="36624-3111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3111">Description</span></span>

<span data-ttu-id="36624-3112">Bu hizmet, belirtilen IP örneği için bir UDP yuvası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="36624-3112">This service creates a UDP socket for the specified IP instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3113">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3113">Parameters</span></span>

- <span data-ttu-id="36624-3114">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3114">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="36624-3115">**socket_ptr** Yeni UDP yuva denetimi Bloc işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3115">**socket_ptr** Pointer to new UDP socket control bloc.</span></span>
- <span data-ttu-id="36624-3116">**ad** Bu UDP yuvasının uygulama adı.</span><span class="sxs-lookup"><span data-stu-id="36624-3116">**name** Application name for this UDP socket.</span></span>
- <span data-ttu-id="36624-3117">**Type_of_service** İletim için hizmet türünü tanımlar, yasal değerler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="36624-3117">**type_of_service** Defines the type of service for the transmission, legal values are as follows:</span></span>
    - <span data-ttu-id="36624-3118">NX_IP_NORMAL (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-3118">NX_IP_NORMAL (0x00000000)</span></span>
    - <span data-ttu-id="36624-3119">NX_IP_MIN_DELAY (0x00100000)</span><span class="sxs-lookup"><span data-stu-id="36624-3119">NX_IP_MIN_DELAY (0x00100000)</span></span>
    - <span data-ttu-id="36624-3120">NX_IP_MAX_DATA (0x00080000)</span><span class="sxs-lookup"><span data-stu-id="36624-3120">NX_IP_MAX_DATA (0x00080000)</span></span>
    - <span data-ttu-id="36624-3121">NX_IP_MAX_RELIABLE (0x00040000)</span><span class="sxs-lookup"><span data-stu-id="36624-3121">NX_IP_MAX_RELIABLE (0x00040000)</span></span>
    - <span data-ttu-id="36624-3122">NX_IP_MIN_COST (0x00020000)</span><span class="sxs-lookup"><span data-stu-id="36624-3122">NX_IP_MIN_COST (0x00020000)</span></span>
- <span data-ttu-id="36624-3123">**parça** IP fragmenting izin verilip verilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="36624-3123">**fragment** Specifies whether or not IP fragmenting is allowed.</span></span> <span data-ttu-id="36624-3124">NX_FRAGMENT_OKAY (0x0) belirtilmişse, IP fragmenting izin verilir.</span><span class="sxs-lookup"><span data-stu-id="36624-3124">If NX_FRAGMENT_OKAY (0x0) is specified, IP fragmenting is allowed.</span></span> <span data-ttu-id="36624-3125">NX_DONT_FRAGMENT (0x4000) belirtilirse, IP fragmenting devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-3125">If NX_DONT_FRAGMENT (0x4000) is specified, IP fragmenting is disabled.</span></span>
- <span data-ttu-id="36624-3126">**Time_to_live** Bu paketin oluşturulmadan önce kaç yönlendirici geçebileceğini tanımlayan 8 bitlik değeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="36624-3126">**time_to_live** Specifies the 8-bit value that defines how many routers this packet can pass before being thrown away.</span></span> <span data-ttu-id="36624-3127">Varsayılan değer NX_IP_TIME_TO_LIVE tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="36624-3127">The default value is specified by NX_IP_TIME_TO_LIVE.</span></span>
- <span data-ttu-id="36624-3128">**queue_maximum** Bu yuva için sıraya alınabilen en fazla UDP veri birimi sayısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-3128">**queue_maximum** Defines the maximum number of UDP datagrams that can be queued for this socket.</span></span> <span data-ttu-id="36624-3129">Kuyruk sınırına ulaşıldığında, alınan her yeni paket için en eski UDP paketi yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="36624-3129">After the queue limit is reached, for every new packet received the oldest UDP packet is released.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3130">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3130">Return Values</span></span>

- <span data-ttu-id="36624-3131">**NX_SUCCESS** (0x00) başarılı UDP yuvası oluşturma.</span><span class="sxs-lookup"><span data-stu-id="36624-3131">**NX_SUCCESS** (0x00) Successful UDP socket create.</span></span>
- <span data-ttu-id="36624-3132">**NX_OPTION_ERROR** (0X0a) geçersiz hizmet türü, parça veya yaşam süresi seçeneği.</span><span class="sxs-lookup"><span data-stu-id="36624-3132">**NX_OPTION_ERROR** (0x0A) Invalid type-of-service, fragment, or time-to-live option.</span></span>
- <span data-ttu-id="36624-3133">**NX_PTR_ERROR** (0x07) geçersiz IP veya yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3133">**NX_PTR_ERROR** (0x07) Invalid IP or socket pointer.</span></span>
- <span data-ttu-id="36624-3134">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3134">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-3135">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-3135">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3136">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3136">Allowed From</span></span>

<span data-ttu-id="36624-3137">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-3137">Initialization and Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3138">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3138">Preemption Possible</span></span>

<span data-ttu-id="36624-3139">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3139">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3140">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3140">Example</span></span>

```C
/* Create a UDP socket with a maximum receive queue of 30 packets.*/
status = nx_udp_socket_create(&ip_0, &udp_socket, "Sample UDP Socket",
    NX_IP_NORMAL, NX_FRAGMENT_OKAY, 0x80, 30);

/* If status is NX_SUCCESS, the new UDP socket has been created and
    is ready for binding. */
```

### <a name="see-also"></a><span data-ttu-id="36624-3141">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3141">See Also</span></span>

- <span data-ttu-id="36624-3142">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3142">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3143">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3143">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3144">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3144">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3145">nx_udp_socket_checksum_enable, nx_udp_socket_delete,</span><span class="sxs-lookup"><span data-stu-id="36624-3145">nx_udp_socket_checksum_enable, nx_udp_socket_delete,</span></span>
- <span data-ttu-id="36624-3146">nx_udp_socket_info_get, nx_udp_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3146">nx_udp_socket_info_get, nx_udp_socket_port_get,</span></span>
- <span data-ttu-id="36624-3147">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-3147">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="36624-3148">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3148">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="36624-3149">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3149">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_delete"></a><span data-ttu-id="36624-3150">nx_udp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="36624-3150">nx_udp_socket_delete</span></span>

<span data-ttu-id="36624-3151">UDP yuvasını Sil</span><span class="sxs-lookup"><span data-stu-id="36624-3151">Delete UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3152">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3152">Prototype</span></span>

```C
UINT nx_udp_socket_delete(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-3153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3153">Description</span></span>

<span data-ttu-id="36624-3154">Bu hizmet, önceden oluşturulmuş bir UDP yuvasını siler.</span><span class="sxs-lookup"><span data-stu-id="36624-3154">This service deletes a previously created UDP socket.</span></span> <span data-ttu-id="36624-3155">Yuva bir bağlantı noktasına bağlıysa, önce yuvanın bağlantısı kaldırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-3155">If the socket was bound to a port, the socket must be unbound first.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3156">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3156">Parameters</span></span>

- <span data-ttu-id="36624-3157">**socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3157">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3158">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3158">Return Values</span></span>

- <span data-ttu-id="36624-3159">**NX_SUCCESS** (0x00) başarılı yuva silme.</span><span class="sxs-lookup"><span data-stu-id="36624-3159">**NX_SUCCESS** (0x00) Successful socket delete.</span></span>
- <span data-ttu-id="36624-3160">**NX_STILL_BOUND** (0x42) yuva hala bağımlı.</span><span class="sxs-lookup"><span data-stu-id="36624-3160">**NX_STILL_BOUND** (0x42) Socket is still bound.</span></span>
- <span data-ttu-id="36624-3161">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3161">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-3162">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3162">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-3163">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-3163">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3164">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3164">Allowed From</span></span>

<span data-ttu-id="36624-3165">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-3165">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3166">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3166">Preemption Possible</span></span>

<span data-ttu-id="36624-3167">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3167">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3168">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3168">Example</span></span>

```C
/* Delete a previously created UDP socket. */
status = nx_udp_socket_delete(&udp_socket);

/* If status is NX_SUCCESS, the previously created UDP socket has
    been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="36624-3169">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3169">See Also</span></span>

- <span data-ttu-id="36624-3170">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3170">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3171">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3171">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3172">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3172">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3173">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-3173">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="36624-3174">nx_udp_socket_info_get, nx_udp_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3174">nx_udp_socket_info_get, nx_udp_socket_port_get,</span></span>
- <span data-ttu-id="36624-3175">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-3175">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="36624-3176">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3176">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="36624-3177">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3177">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_info_get"></a><span data-ttu-id="36624-3178">nx_udp_socket_info_get</span><span class="sxs-lookup"><span data-stu-id="36624-3178">nx_udp_socket_info_get</span></span>

<span data-ttu-id="36624-3179">UDP yuva etkinlikleri hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="36624-3179">Retrieve information about UDP socket activities</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3180">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3180">Prototype</span></span>

```C
UINT nx_udp_socket_info_get(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *udp_packets_sent,
    ULONG *udp_bytes_sent,
    ULONG *udp_packets_received,
    ULONG *udp_bytes_received,
    ULONG *udp_packets_queued,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
```

### <a name="description"></a><span data-ttu-id="36624-3181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3181">Description</span></span>

<span data-ttu-id="36624-3182">Bu hizmet, belirtilen UDP yuva örneği için UDP yuva etkinlikleri hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-3182">This service retrieves information about UDP socket activities for the specified UDP socket instance.</span></span>

<span data-ttu-id="36624-3183">*Hedef işaretçi NX_NULL, bu belirli bilgiler çağırana döndürülmez.*</span><span class="sxs-lookup"><span data-stu-id="36624-3183">*If a destination pointer is NX_NULL, that particular information is not returned to the caller.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3184">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3184">Parameters</span></span>

- <span data-ttu-id="36624-3185">**socket_ptr** Önceden oluşturulmuş UDP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3185">**socket_ptr** Pointer to previously-created UDP socket instance.</span></span>
- <span data-ttu-id="36624-3186">**udp_packets_sent** Yuvada gönderilen toplam UDP paketi sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3186">**udp_packets_sent** Pointer to destination for the total number of UDP packets sent on socket.</span></span>
- <span data-ttu-id="36624-3187">**udp_bytes_sent** Yuvada gönderilen UDP baytlarının toplam sayısı için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3187">**udp_bytes_sent** Pointer to destination for the total number of UDP bytes sent on socket.</span></span>
- <span data-ttu-id="36624-3188">**udp_packets_received** Yuvada alınan UDP paketlerinin toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3188">**udp_packets_received** Pointer to destination of the total number of UDP packets received on socket.</span></span>
- <span data-ttu-id="36624-3189">**udp_bytes_received** Yuvada alınan UDP baytlarının toplam sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3189">**udp_bytes_received** Pointer to destination of the total number of UDP bytes received on socket.</span></span>
- <span data-ttu-id="36624-3190">**udp_packets_queued** Yuva üzerindeki toplam sıraya alınmış UDP paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3190">**udp_packets_queued** Pointer to destination of the total number of queued UDP packets on socket.</span></span>
- <span data-ttu-id="36624-3191">**udp_receive_packets_dropped** Sıra boyutunun aşılması nedeniyle yuva için bırakılan toplam UDP alma paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3191">**udp_receive_packets_dropped** Pointer to destination of the total number of UDP receive packets dropped for socket due to queue size being exceeded.</span></span>
- <span data-ttu-id="36624-3192">**udp_checksum_errors** Yuvada sağlama toplamı hataları olan toplam UDP paketi sayısının hedefi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3192">**udp_checksum_errors** Pointer to destination of the total number of UDP packets with checksum errors on socket.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3193">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3193">Return Values</span></span>

- <span data-ttu-id="36624-3194">**NX_SUCCESS** (0x00) başarılı UDP yuvası bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="36624-3194">**NX_SUCCESS** (0x00) Successful UDP socket information retrieval.</span></span>
- <span data-ttu-id="36624-3195">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3195">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-3196">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3196">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-3197">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-3197">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3198">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3198">Allowed From</span></span>

<span data-ttu-id="36624-3199">Başlatma, iş parçacıkları ve zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="36624-3199">Initialization, threads, and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3200">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3200">Preemption Possible</span></span>

<span data-ttu-id="36624-3201">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3201">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3202">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3202">Example</span></span>

```C
/* Retrieve UDP socket information from socket 0.*/
status = nx_udp_socket_info_get(&socket_0,
    &udp_packets_sent,
    &udp_bytes_sent,
    &udp_packets_received,
    &udp_bytes_received,
    &udp_queued_packets,
    &udp_receive_packets_dropped,
    &udp_checksum_errors);

/* If status is NX_SUCCESS, UDP socket information was retrieved.*/
```

### <a name="see-also"></a><span data-ttu-id="36624-3203">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3203">See Also</span></span>

- <span data-ttu-id="36624-3204">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3204">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3205">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3205">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3206">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3206">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3207">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-3207">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="36624-3208">nx_udp_socket_delete, nx_udp_socket_port_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3208">nx_udp_socket_delete, nx_udp_socket_port_get,</span></span>
- <span data-ttu-id="36624-3209">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-3209">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="36624-3210">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3210">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="36624-3211">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3211">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_port_get"></a><span data-ttu-id="36624-3212">nx_udp_socket_port_get</span><span class="sxs-lookup"><span data-stu-id="36624-3212">nx_udp_socket_port_get</span></span>

<span data-ttu-id="36624-3213">UDP yuvasına göre bağlantı noktası numarasını seçin</span><span class="sxs-lookup"><span data-stu-id="36624-3213">Pick up port number bound to UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3214">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3214">Prototype</span></span>

```C
UINT nx_udp_socket_port_get(NX_UDP_SOCKET *socket_ptr, UINT *port_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-3215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3215">Description</span></span>

<span data-ttu-id="36624-3216">Bu hizmet, yuvanın bağlandığı zamanda NX_ANY_PORT belirtildiği durumlarda NetX tarafından ayrılan bağlantı noktasını bulmak için yararlı olan yuva ile ilişkili bağlantı noktası numarasını alır.</span><span class="sxs-lookup"><span data-stu-id="36624-3216">This service retrieves the port number associated with the socket, which is useful to find the port allocated by NetX in situations where the NX_ANY_PORT was specified at the time the socket was bound.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3217">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3217">Parameters</span></span>

- <span data-ttu-id="36624-3218">**socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3218">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>
- <span data-ttu-id="36624-3219">**port_ptr** Dönüş bağlantı noktası numarası için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3219">**port_ptr** Pointer to destination for the return port number.</span></span> <span data-ttu-id="36624-3220">Geçerli bağlantı noktası numaraları (1-0xFFFF).</span><span class="sxs-lookup"><span data-stu-id="36624-3220">Valid port numbers are (1- 0xFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3221">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3221">Return Values</span></span>

- <span data-ttu-id="36624-3222">**NX_SUCCESS** (0x00) başarılı yuva bağlaması.</span><span class="sxs-lookup"><span data-stu-id="36624-3222">**NX_SUCCESS** (0x00) Successful socket bind.</span></span>
- <span data-ttu-id="36624-3223">**NX_NOT_BOUND** (0x24) bu yuva bir bağlantı noktasına bağlanmamış.</span><span class="sxs-lookup"><span data-stu-id="36624-3223">**NX_NOT_BOUND** (0x24) This socket is not bound to a port.</span></span>
- <span data-ttu-id="36624-3224">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi veya bağlantı noktası döndürme işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3224">**NX_PTR_ERROR** (0x07) Invalid socket pointer or port return pointer.</span></span>
- <span data-ttu-id="36624-3225">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3225">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-3226">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-3226">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3227">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3227">Allowed From</span></span>

<span data-ttu-id="36624-3228">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-3228">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3229">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3229">Preemption Possible</span></span>

<span data-ttu-id="36624-3230">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3230">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3231">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3231">Example</span></span>

```C
/* Get the port number of created and bound UDP socket. */
status = nx_udp_socket_port_get(&udp_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
    socket is bound to. */
```

### <a name="see-also"></a><span data-ttu-id="36624-3232">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3232">See Also</span></span>

- <span data-ttu-id="36624-3233">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3233">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3234">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3234">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3235">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3235">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3236">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-3236">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="36624-3237">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3237">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3238">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-3238">nx_udp_socket_receive, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="36624-3239">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3239">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="36624-3240">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3240">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_receive"></a><span data-ttu-id="36624-3241">nx_udp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="36624-3241">nx_udp_socket_receive</span></span>

<span data-ttu-id="36624-3242">UDP yuvasından veri birimi al</span><span class="sxs-lookup"><span data-stu-id="36624-3242">Receive datagram from UDP socket</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3243">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3243">Prototype</span></span>

```C
UINT nx_udp_socket_receive(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="36624-3244">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3244">Description</span></span>

<span data-ttu-id="36624-3245">Bu hizmet, belirtilen yuvadan bir UDP veri birimi alır.</span><span class="sxs-lookup"><span data-stu-id="36624-3245">This service receives an UDP datagram from the specified socket.</span></span> <span data-ttu-id="36624-3246">Belirtilen yuvada hiçbir veri birimi sıraya alınmaz, çağıran, sağlanan bekleme seçeneğine göre askıya alır.</span><span class="sxs-lookup"><span data-stu-id="36624-3246">If no datagram is queued on the specified socket, the caller suspends based on the supplied wait option.</span></span>

<span data-ttu-id="36624-3247">*NX_SUCCESS döndürülürse, uygulama artık gerekli olmadığında alınan paketi serbest bırakmaktan sorumludur.*</span><span class="sxs-lookup"><span data-stu-id="36624-3247">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3248">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3248">Parameters</span></span>

- <span data-ttu-id="36624-3249">**socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3249">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>
- <span data-ttu-id="36624-3250">**packet_ptr** UDP veri birimi paket işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3250">**packet_ptr** Pointer to UDP datagram packet pointer.</span></span>
- <span data-ttu-id="36624-3251">**wait_option** Bir veri birimi şu anda bu yuvada sıraya alınmışsa hizmetin nasıl davranacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="36624-3251">**wait_option** Defines how the service behaves if a datagram is not currently queued on this socket.</span></span> <span data-ttu-id="36624-3252">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="36624-3252">The wait options are defined as follows:</span></span>
- <span data-ttu-id="36624-3253">NX_NO_WAIT (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="36624-3253">NX_NO_WAIT (0x00000000)</span></span>
- <span data-ttu-id="36624-3254">NX_WAIT_FOREVER (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="36624-3254">NX_WAIT_FOREVER (0xFFFFFFFF)</span></span>
- <span data-ttu-id="36624-3255">ticks içinde zaman aşımı değeri (0x00000001-0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="36624-3255">timeout value in ticks (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3256">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3256">Allowed From</span></span>

<span data-ttu-id="36624-3257">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-3257">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3258">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3258">Preemption Possible</span></span>

<span data-ttu-id="36624-3259">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3259">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3260">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3260">Example</span></span>

```C
/* Receive a packet from a previously created and bound UDP socket.
    If no packets are currently available, wait for 500 timer ticks
    before giving up. */
status = nx_udp_socket_receive(&udp_socket, &packet_ptr, 500);

/* If status is NX_SUCCESS, the received UDP packet is pointed to by
    packet_ptr. */
```

### <a name="see-also"></a><span data-ttu-id="36624-3261">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3261">See Also</span></span>

- <span data-ttu-id="36624-3262">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3262">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3263">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3263">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3264">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3264">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3265">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-3265">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="36624-3266">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3266">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3267">nx_udp_socket_port_get, nx_udp_socket_receive_notify,</span><span class="sxs-lookup"><span data-stu-id="36624-3267">nx_udp_socket_port_get, nx_udp_socket_receive_notify,</span></span>
- <span data-ttu-id="36624-3268">nx_udp_socket_send, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3268">nx_udp_socket_send, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="36624-3269">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3269">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_receive_notify"></a><span data-ttu-id="36624-3270">nx_udp_socket_receive_notify</span><span class="sxs-lookup"><span data-stu-id="36624-3270">nx_udp_socket_receive_notify</span></span>

<span data-ttu-id="36624-3271">Alınan her paketin uygulamasını bilgilendir</span><span class="sxs-lookup"><span data-stu-id="36624-3271">Notify application of each received packet</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3272">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3272">Prototype</span></span>

```C
UINT nx_udp_socket_receive_notify(
    NX_UDP_SOCKET *socket_ptr,
    VOID (*udp_receive_notify)
    (NX_UDP_SOCKET *socket_ptr));
```

### <a name="description"></a><span data-ttu-id="36624-3273">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3273">Description</span></span>

<span data-ttu-id="36624-3274">Bu hizmet, bildirim al işlev işaretçisini uygulama tarafından belirtilen geri çağırma işlevine ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36624-3274">This service sets the receive notify function pointer to the callback function specified by the application.</span></span> <span data-ttu-id="36624-3275">Bu geri çağırma işlevi, yuva üzerinde her paket alındığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="36624-3275">This callback function is then called whenever a packet is received on the socket.</span></span> <span data-ttu-id="36624-3276">NX_NULL bir işaretçi sağlanırsa, alma bildirme işlevi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-3276">If a NX_NULL pointer is supplied, the receive notify function is disabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3277">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3277">Parameters</span></span>

- <span data-ttu-id="36624-3278">**socket_ptr** UDP yuvasının işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3278">**socket_ptr** Pointer to the UDP socket.</span></span>
- <span data-ttu-id="36624-3279">**udp_receive_notify** Yuvada bir paket alındığında çağrılan uygulama geri çağırma işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3279">**udp_receive_notify** Application callback function pointer that is called when a packet is received on the socket.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3280">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3280">Allowed From</span></span>

<span data-ttu-id="36624-3281">Başlatma, iş parçacıkları, zamanlayıcılar ve ISRs</span><span class="sxs-lookup"><span data-stu-id="36624-3281">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3282">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3282">Preemption Possible</span></span>

<span data-ttu-id="36624-3283">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3283">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3284">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3284">Example</span></span>

```C
/* Setup a receive packet callback function for the "udp_socket"
socket. */
status = nx_udp_socket_receive_notify(&udp_socket,
    my_receive_notify);

/* If status is NX_SUCCESS, NetX will call the function named
    "my_receive_notify" whenever a packet is received for
    "udp_socket". */
```

### <a name="see-also"></a><span data-ttu-id="36624-3285">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3285">See Also</span></span>

- <span data-ttu-id="36624-3286">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3286">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3287">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3287">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3288">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3288">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3289">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-3289">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="36624-3290">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3290">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3291">nx_udp_socket_port_get, nx_udp_socket_receive, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3291">nx_udp_socket_port_get, nx_udp_socket_receive, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-3292">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span><span class="sxs-lookup"><span data-stu-id="36624-3292">nx_udp_socket_interface_send, nx_udp_socket_unbind,</span></span>
- <span data-ttu-id="36624-3293">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3293">nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_send"></a><span data-ttu-id="36624-3294">nx_udp_socket_send</span><span class="sxs-lookup"><span data-stu-id="36624-3294">nx_udp_socket_send</span></span>

<span data-ttu-id="36624-3295">UDP veri birimi gönder</span><span class="sxs-lookup"><span data-stu-id="36624-3295">Send a UDP Datagram</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3296">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3296">Prototype</span></span>

```C
UINT nx_udp_socket_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port);
```

### <a name="description"></a><span data-ttu-id="36624-3297">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3297">Description</span></span>

<span data-ttu-id="36624-3298">Bu hizmet, daha önce oluşturulmuş ve bağlantılı bir UDP yuvası aracılığıyla bir UDP datagramı gönderir.</span><span class="sxs-lookup"><span data-stu-id="36624-3298">This service sends a UDP datagram through a previously created and bound UDP socket.</span></span> <span data-ttu-id="36624-3299">NetX, hedef IP adresini temel alarak kaynak adresi olarak uygun bir yerel IP adresi bulur.</span><span class="sxs-lookup"><span data-stu-id="36624-3299">NetX finds a suitable local IP address as source address based on the destination IP address.</span></span> <span data-ttu-id="36624-3300">Belirli bir arabirim ve kaynak IP adresi belirtmek için, uygulamanın **nx_udp_socket_interface_send** hizmetini kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36624-3300">To specify a specific interface and source IP address, the application should use the **nx_udp_socket_interface_send** service.</span></span>

<span data-ttu-id="36624-3301">Bu hizmetin UDP veri biriminin başarıyla gönderilip gönderilmediğini ne olursa olsun, hemen geri dönmediğine unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-3301">Note that this service returns immediately regardless of whether the UDP datagram was successfully sent.</span></span>

<span data-ttu-id="36624-3302">Yuva yerel bir bağlantı noktasına bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36624-3302">The socket must be bound to a local port.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3303">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3303">Parameters</span></span>

- <span data-ttu-id="36624-3304">**socket_ptr** Önceden oluşturulan UDP yuva örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="36624-3304">**socket_ptr** Pointer to previously created UDP socket instance</span></span>
- <span data-ttu-id="36624-3305">**packet_ptr** UDP veri birimi paket işaretçisi</span><span class="sxs-lookup"><span data-stu-id="36624-3305">**packet_ptr** UDP datagram packet pointer</span></span>
- <span data-ttu-id="36624-3306">**ip_address** Hedef IP adresi</span><span class="sxs-lookup"><span data-stu-id="36624-3306">**ip_address** Destination IP address</span></span>
- <span data-ttu-id="36624-3307">**bağlantı noktası** Ana bilgisayar bayt düzeninde geçerli hedef bağlantı noktası numarası 1 ile 0xFFFF arasında)</span><span class="sxs-lookup"><span data-stu-id="36624-3307">**port** Valid destination port number between 1 and 0xFFFF), in host byte order</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3308">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3308">Return Values</span></span>

- <span data-ttu-id="36624-3309">**NX_SUCCESS** (0x00) başarılı UDP yuvası gönderme</span><span class="sxs-lookup"><span data-stu-id="36624-3309">**NX_SUCCESS** (0x00) Successful UDP socket send</span></span>
- <span data-ttu-id="36624-3310">**NX_NOT_BOUND** (0x24) yuva herhangi bir bağlantı noktasına bağlanmadı</span><span class="sxs-lookup"><span data-stu-id="36624-3310">**NX_NOT_BOUND** (0x24) Socket not bound to any port</span></span>
- <span data-ttu-id="36624-3311">**NX_NO_INTERFACE_ADDRESS** (0x50) uygun bir giden arabirim bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="36624-3311">**NX_NO_INTERFACE_ADDRESS** (0x50) No suitable outgoing interface can be found.</span></span>
- <span data-ttu-id="36624-3312">**NX_IP_ADDRESS_ERROR** (0x21) GEÇERSIZ sunucu IP adresi</span><span class="sxs-lookup"><span data-stu-id="36624-3312">**NX_IP_ADDRESS_ERROR** (0x21) Invalid server IP address</span></span>
- <span data-ttu-id="36624-3313">**NX_UNDERFLOW** (0x02) paketteki UDP üst bilgisi için yeterli yer yok</span><span class="sxs-lookup"><span data-stu-id="36624-3313">**NX_UNDERFLOW** (0x02) Not enough room for UDP header in the packet</span></span>
- <span data-ttu-id="36624-3314">**NX_OVERFLOW** (0x03) paket ekleme işaretçisi geçersiz</span><span class="sxs-lookup"><span data-stu-id="36624-3314">**NX_OVERFLOW** (0x03) Packet append pointer is invalid</span></span>
- <span data-ttu-id="36624-3315">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi</span><span class="sxs-lookup"><span data-stu-id="36624-3315">**NX_PTR_ERROR** (0x07) Invalid socket pointer</span></span>
- <span data-ttu-id="36624-3316">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="36624-3316">**NX_CALLER_ERROR** (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="36624-3317">**NX_NOT_ENABLED** (0x14) UDP etkin değil</span><span class="sxs-lookup"><span data-stu-id="36624-3317">**NX_NOT_ENABLED** (0x14) UDP has not been enabled</span></span>
- <span data-ttu-id="36624-3318">**NX_INVALID_PORT** (0x46) bağlantı noktası numarası geçerli bir Aralık içinde değil</span><span class="sxs-lookup"><span data-stu-id="36624-3318">**NX_INVALID_PORT** (0x46) Port number is not within a valid range</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3319">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3319">Allowed From</span></span>

<span data-ttu-id="36624-3320">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-3320">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3321">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3321">Preemption Possible</span></span>

<span data-ttu-id="36624-3322">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3322">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3323">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3323">Example</span></span>

```C
ULONG server_address;

/* Set the UDP Client IP address. */
server_address = IP_ADDRESS(1,2,3,5);

/* Send a packet to the UDP server at server_address on port 12. */
status = nx_udp_socket_send(&client_socket, packet_ptr,
    server_address, 12);

/* If status == NX_SUCCESS, the application successfully transmitted
    the packet out the UDP socket to its peer. */
```

### <a name="see-also"></a><span data-ttu-id="36624-3324">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3324">See Also</span></span>

- <span data-ttu-id="36624-3325">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3325">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3326">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3326">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3327">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3327">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3328">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-3328">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="36624-3329">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3329">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3330">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-3330">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-3331">nx_udp_socket_receive_notify, nx_udp_socket_interface_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3331">nx_udp_socket_receive_notify, nx_udp_socket_interface_send,</span></span>
- <span data-ttu-id="36624-3332">nx_udp_socket_unbind, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3332">nx_udp_socket_unbind, nx_udp_source_extract</span></span>

## <a name="nx_udp_socket_interface_send"></a><span data-ttu-id="36624-3333">nx_udp_socket_interface_send</span><span class="sxs-lookup"><span data-stu-id="36624-3333">nx_udp_socket_interface_send</span></span>

<span data-ttu-id="36624-3334">UDP yuvası üzerinden veri birimi gönderin.</span><span class="sxs-lookup"><span data-stu-id="36624-3334">Send datagram through UDP socket.</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3335">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3335">Prototype</span></span>

```C
UINT nx_udp_socket_interface_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port,
    UINT address_index);
```

### <a name="description"></a><span data-ttu-id="36624-3336">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3336">Description</span></span>

<span data-ttu-id="36624-3337">Bu hizmet, kaynak adresi olarak belirtilen IP adresine sahip ağ arabirimi aracılığıyla daha önce oluşturulmuş ve bağlantılı bir UDP yuvası aracılığıyla bir UDP datagramı gönderir.</span><span class="sxs-lookup"><span data-stu-id="36624-3337">This service sends a UDP datagram through a previously created and bound UDP socket through the network interface with the specified IP address as the source address.</span></span> <span data-ttu-id="36624-3338">UDP veri biriminin başarıyla gönderilip gönderilmediğini ne olursa olsun hizmetin hemen geri döndüğünü unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36624-3338">Note that service returns immediately, regardless of whether or not the UDP datagram was successfully sent.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3339">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3339">Parameters</span></span>

- <span data-ttu-id="36624-3340">**socket_ptr** Paketin üzerine iletilmesi için yuva.</span><span class="sxs-lookup"><span data-stu-id="36624-3340">**socket_ptr** Socket to transmit the packet out on.</span></span>
- <span data-ttu-id="36624-3341">**packet_ptr** İletilecek paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3341">**packet_ptr** Pointer to packet to transmit.</span></span>
- <span data-ttu-id="36624-3342">**ip_address** Paketin gönderileceği hedef IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-3342">**ip_address** Destination IP address to send packet.</span></span>
- <span data-ttu-id="36624-3343">**bağlantı noktası** Hedef bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="36624-3343">**port** Destination port.</span></span>
- <span data-ttu-id="36624-3344">**address_index** Paketin gönderileceği arabirimle ilişkili adresin dizini.</span><span class="sxs-lookup"><span data-stu-id="36624-3344">**address_index** Index of the address associated with the interface to send packet on.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3345">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3345">Return Values</span></span>

- <span data-ttu-id="36624-3346">**NX_SUCCESS** (0x00) paketi başarıyla gönderildi.</span><span class="sxs-lookup"><span data-stu-id="36624-3346">**NX_SUCCESS** (0x00) Packet successfully sent.</span></span>
- <span data-ttu-id="36624-3347">**NX_NOT_BOUND** (0x24) yuva bir bağlantı noktasına bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-3347">**NX_NOT_BOUND** (0x24) Socket not bound to a port.</span></span>
- <span data-ttu-id="36624-3348">**NX_IP_ADDRESS_ERROR** (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="36624-3348">**NX_IP_ADDRESS_ERROR** (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="36624-3349">**NX_NOT_ENABLED** (0x14) UDP işleme etkin değil.</span><span class="sxs-lookup"><span data-stu-id="36624-3349">**NX_NOT_ENABLED** (0x14) UDP processing not enabled.</span></span>
- <span data-ttu-id="36624-3350">**NX_PTR_ERROR** (0x07) geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3350">**NX_PTR_ERROR** (0x07) Invalid pointer.</span></span>
- <span data-ttu-id="36624-3351">**NX_OVERFLOW** (0x03) geçersiz paket ekleme işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3351">**NX_OVERFLOW** (0x03) Invalid packet append pointer.</span></span>
- <span data-ttu-id="36624-3352">**NX_UNDERFLOW** (0x02) geçersiz paket önüne işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3352">**NX_UNDERFLOW** (0x02) Invalid packet prepend pointer.</span></span>
- <span data-ttu-id="36624-3353">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3353">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-3354">**NX_INVALID_INTERFACE** (0x4C) geçersiz adres dizini.</span><span class="sxs-lookup"><span data-stu-id="36624-3354">**NX_INVALID_INTERFACE** (0x4C) Invalid address index.</span></span>
- <span data-ttu-id="36624-3355">**NX_INVALID_PORT** (0x46) bağlantı noktası numarası en fazla bağlantı noktası numarasını aşıyor.</span><span class="sxs-lookup"><span data-stu-id="36624-3355">**NX_INVALID_PORT** (0x46) Port number exceeds maximum port number.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3356">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3356">Allowed From</span></span>

<span data-ttu-id="36624-3357">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-3357">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3358">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3358">Preemption Possible</span></span>

<span data-ttu-id="36624-3359">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3359">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3360">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3360">Example</span></span>

```C
#define ADDRESS_INDEX 1

/* Send packet out on port 80 to the specified destination IP on the
interface at index 1 in the IP task interface list. */
status = nx_udp_packet_interface_send(socket_ptr, packet_ptr,
    destination_ip, 80,
    ADDRESS_INDEX);

/* If status is NX_SUCCESS packet was successfully transmitted. */
```

### <a name="see-also"></a><span data-ttu-id="36624-3361">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3361">See Also</span></span>

- <span data-ttu-id="36624-3362">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3362">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3363">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3363">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3364">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3364">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3365">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-3365">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="36624-3366">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3366">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3367">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-3367">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-3368">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3368">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-3369">nx_udp_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="36624-3369">nx_udp_socket_unbind</span></span>

## <a name="nx_udp_socket_unbind"></a><span data-ttu-id="36624-3370">nx_udp_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="36624-3370">nx_udp_socket_unbind</span></span>

<span data-ttu-id="36624-3371">UDP bağlantı noktasından UDP yuvasının bağlantısını kaldır.</span><span class="sxs-lookup"><span data-stu-id="36624-3371">Unbind UDP socket from UDP port.</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3372">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3372">Prototype</span></span>

```C
UINT nx_udp_socket_unbind(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a><span data-ttu-id="36624-3373">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3373">Description</span></span>

<span data-ttu-id="36624-3374">Bu hizmet, UDP yuvası ile UDP bağlantı noktası arasındaki bağlamayı yayınlar.</span><span class="sxs-lookup"><span data-stu-id="36624-3374">This service releases the binding between the UDP socket and a UDP port.</span></span> <span data-ttu-id="36624-3375">Alma sırasında depolanan tüm alınan paketler, ciltten çıkarma işleminin bir parçası olarak serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="36624-3375">Any received packets stored in the receive queue are released as part of the unbind operation.</span></span>

<span data-ttu-id="36624-3376">İlişkisiz bağlantı noktasına başka bir yuva bağlamayı bekleyen başka iş parçacıkları varsa, ilk askıya alınan iş parçacığı daha sonra yeni ilişkisiz bağlantı noktasına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="36624-3376">If there are other threads waiting to bind another socket to the unbound port, the first suspended thread is then bound to the newly unbound port.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3377">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3377">Parameters</span></span>

- <span data-ttu-id="36624-3378">**socket_ptr** Daha önce oluşturulan UDP yuva örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3378">**socket_ptr** Pointer to previously created UDP socket instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3379">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3379">Return Values</span></span>

- <span data-ttu-id="36624-3380">**NX_SUCCESS** (0x00) başarılı yuva bağlantısı kesiliyor.</span><span class="sxs-lookup"><span data-stu-id="36624-3380">**NX_SUCCESS** (0x00) Successful socket unbind.</span></span>
- <span data-ttu-id="36624-3381">**NX_NOT_BOUND** (0x24) yuva herhangi bir bağlantı noktasına bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="36624-3381">**NX_NOT_BOUND** (0x24) Socket was not bound to any port.</span></span>
- <span data-ttu-id="36624-3382">**NX_PTR_ERROR** (0x07) geçersiz yuva işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3382">**NX_PTR_ERROR** (0x07) Invalid socket pointer.</span></span>
- <span data-ttu-id="36624-3383">**NX_CALLER_ERROR** (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="36624-3383">**NX_CALLER_ERROR** (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="36624-3384">**NX_NOT_ENABLED** (0x14) Bu bileşen etkinleştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="36624-3384">**NX_NOT_ENABLED** (0x14) This component has not been enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3385">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3385">Allowed From</span></span>

<span data-ttu-id="36624-3386">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="36624-3386">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3387">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3387">Preemption Possible</span></span>

<span data-ttu-id="36624-3388">Yes</span><span class="sxs-lookup"><span data-stu-id="36624-3388">Yes</span></span>

### <a name="example"></a><span data-ttu-id="36624-3389">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3389">Example</span></span>

```C
/* Unbind the previously bound UDP socket. */
status = nx_udp_socket_unbind(&udp_socket);

/* If status is NX_SUCCESS, the previously bound socket is now
    unbound. */
```

### <a name="see-also"></a><span data-ttu-id="36624-3390">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3390">See Also</span></span>

- <span data-ttu-id="36624-3391">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3391">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3392">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3392">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3393">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3393">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3394">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-3394">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="36624-3395">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3395">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3396">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-3396">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-3397">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3397">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-3398">nx_udp_socket_interface_send, nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3398">nx_udp_socket_interface_send, nx_udp_source_extract</span></span>

## <a name="nx_udp_source_extract"></a><span data-ttu-id="36624-3399">nx_udp_source_extract</span><span class="sxs-lookup"><span data-stu-id="36624-3399">nx_udp_source_extract</span></span>

<span data-ttu-id="36624-3400">UDP veri kaynağından IP ve gönderme bağlantı noktasını Ayıkla</span><span class="sxs-lookup"><span data-stu-id="36624-3400">Extract IP and sending port from UDP datagram</span></span>

### <a name="prototype"></a><span data-ttu-id="36624-3401">Prototype</span><span class="sxs-lookup"><span data-stu-id="36624-3401">Prototype</span></span>

```C
UINT nx_udp_source_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address, UINT *port);
```

### <a name="description"></a><span data-ttu-id="36624-3402">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36624-3402">Description</span></span>

<span data-ttu-id="36624-3403">Bu hizmet, gönderenin IP ve bağlantı noktası numarasını, sağlanan UDP veri biriminin IP ve UDP üst bilgilerinden ayıklar.</span><span class="sxs-lookup"><span data-stu-id="36624-3403">This service extracts the sender's IP and port number from the IP and UDP headers of the supplied UDP datagram.</span></span>

### <a name="parameters"></a><span data-ttu-id="36624-3404">Parametreler</span><span class="sxs-lookup"><span data-stu-id="36624-3404">Parameters</span></span>

- <span data-ttu-id="36624-3405">**packet_ptr** UDP veri birimi paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="36624-3405">**packet_ptr** UDP datagram packet pointer.</span></span>
- <span data-ttu-id="36624-3406">**ip_address** Dönüş IP adresi değişkenine yönelik geçerli işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3406">**ip_address** Valid pointer to the return IP address variable.</span></span>
- <span data-ttu-id="36624-3407">**bağlantı noktası** Dönüş bağlantı noktası değişkenine geçerli işaretçi.</span><span class="sxs-lookup"><span data-stu-id="36624-3407">**port** Valid pointer to the return port variable.</span></span>

### <a name="return-values"></a><span data-ttu-id="36624-3408">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="36624-3408">Return Values</span></span>

- <span data-ttu-id="36624-3409">**NX_SUCCESS** (0x00) başarılı kaynak IP/bağlantı noktası ayıklama.</span><span class="sxs-lookup"><span data-stu-id="36624-3409">**NX_SUCCESS** (0x00) Successful source IP/port extraction.</span></span>
- <span data-ttu-id="36624-3410">**NX_INVALID_PACKET** (0x12) sağlanan paket geçersiz.</span><span class="sxs-lookup"><span data-stu-id="36624-3410">**NX_INVALID_PACKET** (0x12) The supplied packet is invalid.</span></span>
- <span data-ttu-id="36624-3411">**NX_PTR_ERROR** (0x07) geçersiz paket veya IP veya bağlantı noktası hedefi.</span><span class="sxs-lookup"><span data-stu-id="36624-3411">**NX_PTR_ERROR** (0x07) Invalid packet or IP or port destination.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="36624-3412">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="36624-3412">Allowed From</span></span>

<span data-ttu-id="36624-3413">Başlatma, iş parçacıkları, zamanlayıcılar, ıSR</span><span class="sxs-lookup"><span data-stu-id="36624-3413">Initialization, threads, timers, ISR</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="36624-3414">Önalım mümkün</span><span class="sxs-lookup"><span data-stu-id="36624-3414">Preemption Possible</span></span>

<span data-ttu-id="36624-3415">Hayır</span><span class="sxs-lookup"><span data-stu-id="36624-3415">No</span></span>

### <a name="example"></a><span data-ttu-id="36624-3416">Örnek</span><span class="sxs-lookup"><span data-stu-id="36624-3416">Example</span></span>

```C
/* Extract the IP and port information from the sender of the UPD
    packet. */
status = nx_udp_source_extract(packet_ptr, &sender_ip_address,
    &sender_port);

/* If status is NX_SUCCESS, the sender IP and port information has
    been stored in sender_ip_address and sender_port respectively.*/
```

### <a name="see-also"></a><span data-ttu-id="36624-3417">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="36624-3417">See Also</span></span>

- <span data-ttu-id="36624-3418">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3418">nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,</span></span>
- <span data-ttu-id="36624-3419">nx_udp_packet_info_extract, nx_udp_socket_bind,</span><span class="sxs-lookup"><span data-stu-id="36624-3419">nx_udp_packet_info_extract, nx_udp_socket_bind,</span></span>
- <span data-ttu-id="36624-3420">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span><span class="sxs-lookup"><span data-stu-id="36624-3420">nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,</span></span>
- <span data-ttu-id="36624-3421">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span><span class="sxs-lookup"><span data-stu-id="36624-3421">nx_udp_socket_checksum_enable, nx_udp_socket_create,</span></span>
- <span data-ttu-id="36624-3422">nx_udp_socket_delete, nx_udp_socket_info_get,</span><span class="sxs-lookup"><span data-stu-id="36624-3422">nx_udp_socket_delete, nx_udp_socket_info_get,</span></span>
- <span data-ttu-id="36624-3423">nx_udp_socket_port_get, nx_udp_socket_receive,</span><span class="sxs-lookup"><span data-stu-id="36624-3423">nx_udp_socket_port_get, nx_udp_socket_receive,</span></span>
- <span data-ttu-id="36624-3424">nx_udp_socket_receive_notify, nx_udp_socket_send,</span><span class="sxs-lookup"><span data-stu-id="36624-3424">nx_udp_socket_receive_notify, nx_udp_socket_send,</span></span>
- <span data-ttu-id="36624-3425">nx_udp_socket_interface_send, nx_udp_socket_unbind</span><span class="sxs-lookup"><span data-stu-id="36624-3425">nx_udp_socket_interface_send, nx_udp_socket_unbind</span></span>