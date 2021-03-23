---
title: Bölüm 3-Azure RTOS NetX Oto IP hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX Oto IP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 22cc06c32cc9f1857b32d1d2b44a506ea1652cfd
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826848"
---
# <a name="chapter-3---description-of-azure-rtos-netx-autoip-services"></a><span data-ttu-id="e4c6d-103">Bölüm 3-Azure RTOS NetX Oto IP hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="e4c6d-103">Chapter 3 - Description of Azure RTOS NetX AutoIP services</span></span>

<span data-ttu-id="e4c6d-104">Bu bölüm, tüm Azure RTOS NetX Oto IP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-104">This chapter contains a description of all Azure RTOS NetX AutoIP services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="e4c6d-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="e4c6d-106">**nx_auto_ip_create**: *Oto IP örneği oluştur*</span><span class="sxs-lookup"><span data-stu-id="e4c6d-106">**nx_auto_ip_create**: *Create AutoIP instance*</span></span>
- <span data-ttu-id="e4c6d-107">**nx_auto_ip_delete**: *Oto IP örneğini Sil*</span><span class="sxs-lookup"><span data-stu-id="e4c6d-107">**nx_auto_ip_delete**: *Delete AutoIP instance*</span></span>
- <span data-ttu-id="e4c6d-108">**nx_auto_ip_get_address**: *geçerli Oto IP adresini al*</span><span class="sxs-lookup"><span data-stu-id="e4c6d-108">**nx_auto_ip_get_address**: *Get current AutoIP address*</span></span>
- <span data-ttu-id="e4c6d-109">**nx_auto_ip_set_interface**: *IP arabirimine bir Oto IP adresi ihtiyacı* olacak şekilde ayarla</span><span class="sxs-lookup"><span data-stu-id="e4c6d-109">**nx_auto_ip_set_interface**: *Set IP interface needing an AutoIP address*</span></span>
- <span data-ttu-id="e4c6d-110">**nx_auto_ip_start**: *Oto IP işlemesini Başlat*</span><span class="sxs-lookup"><span data-stu-id="e4c6d-110">**nx_auto_ip_start**: *Start AutoIP processing*</span></span>
- <span data-ttu-id="e4c6d-111">**nx_auto_ip_stop**: *Oto IP işlemesini durdur*</span><span class="sxs-lookup"><span data-stu-id="e4c6d-111">**nx_auto_ip_stop**: *Stop AutoIP processing*</span></span>

## <a name="nx_auto_ip_create"></a><span data-ttu-id="e4c6d-112">nx_auto_ip_create</span><span class="sxs-lookup"><span data-stu-id="e4c6d-112">nx_auto_ip_create</span></span>

<span data-ttu-id="e4c6d-113">Oto IP örneği oluştur</span><span class="sxs-lookup"><span data-stu-id="e4c6d-113">Create AutoIP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="e4c6d-114">Prototype</span><span class="sxs-lookup"><span data-stu-id="e4c6d-114">Prototype</span></span>

```c
UINT nx_auto_ip_create(NX_AUTO_IP *auto_ip_ptr, CHAR *name,
            NX_IP *ip_ptr, VOID *stack_ptr, ULONG stack_size,
            UINT priority);
```

### <a name="description"></a><span data-ttu-id="e4c6d-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e4c6d-115">Description</span></span>

<span data-ttu-id="e4c6d-116">Bu hizmet, belirtilen IP örneğinde bir Oto IP örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-116">This service creates an AutoIP instance on the specified IP instance.</span></span>

- <span data-ttu-id="e4c6d-117">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-117">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="e4c6d-118">**ad**: Oto IP örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-118">**name**: Name of AutoIP instance.</span></span>
- <span data-ttu-id="e4c6d-119">**ip_ptr**: IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-119">**ip_ptr**: Pointer to IP instance.</span></span>
- <span data-ttu-id="e4c6d-120">**stack_ptr**: Oto IP iş parçacığı yığın alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-120">**stack_ptr**: Pointer to AutoIP thread stack area.</span></span>
- <span data-ttu-id="e4c6d-121">**stack_size**: Oto IP iş parçacığı yığını alanının boyutu.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-121">**stack_size**: Size of the AutoIP thread stack area.</span></span>
- <span data-ttu-id="e4c6d-122">**Öncelik**: Oto IP iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-122">**priority**: Priority of the AutoIP thread.</span></span>

> [!NOTE]
> <span data-ttu-id="e4c6d-123">DHCP kullanılıyorsa, DHCP iş parçacığının IP örneği iş parçacığından ve Oto IP iş parçacığından daha yüksek bir önceliğe sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-123">If DHCP is used, the DHCP thread must have a higher priority than the IP instance thread and the AutoIP thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="e4c6d-124">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-124">Return Values</span></span>

- <span data-ttu-id="e4c6d-125">**NX_SUCCESS**: (0x00) başarılı bir oto oluştur.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-125">**NX_SUCCESS**: (0x00) Successful AutoIP create.</span></span>
- <span data-ttu-id="e4c6d-126">**NX_AUTO_IP_ERROR**: (0xa00) Oto IP oluşturma hatası.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-126">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP create error.</span></span>
- <span data-ttu-id="e4c6d-127">NX_PTR_ERROR: (0x16) geçersiz Oto IP, ip_ptr veya yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-127">NX_PTR_ERROR: (0x16) Invalid AutoIP, ip_ptr, or stack pointer.</span></span>
- <span data-ttu-id="e4c6d-128">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-128">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e4c6d-129">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="e4c6d-129">Allowed From</span></span>

<span data-ttu-id="e4c6d-130">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="e4c6d-130">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="e4c6d-131">Örnek</span><span class="sxs-lookup"><span data-stu-id="e4c6d-131">Example</span></span>

```c
/* Create the AutoIP instance "auto_ip_0" on "ip_0". */
status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);

/* If status is NX_SUCCESS an AutoIP instance was successfully created. */
```

### <a name="see-also"></a><span data-ttu-id="e4c6d-132">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-132">See Also</span></span>

<span data-ttu-id="e4c6d-133">nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="e4c6d-133">nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_delete"></a><span data-ttu-id="e4c6d-134">nx_auto_ip_delete</span><span class="sxs-lookup"><span data-stu-id="e4c6d-134">nx_auto_ip_delete</span></span>

<span data-ttu-id="e4c6d-135">Oto IP örneğini Sil</span><span class="sxs-lookup"><span data-stu-id="e4c6d-135">Delete AutoIP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="e4c6d-136">Prototype</span><span class="sxs-lookup"><span data-stu-id="e4c6d-136">Prototype</span></span>

```c
UINT nx_auto_ip_delete(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a><span data-ttu-id="e4c6d-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e4c6d-137">Description</span></span>

<span data-ttu-id="e4c6d-138">Bu hizmet, belirtilen IP örneğinde daha önce oluşturulmuş bir Oto IP örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-138">This service deletes a previously created AutoIP instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e4c6d-139">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-139">Input Parameters</span></span>

- <span data-ttu-id="e4c6d-140">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-140">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="e4c6d-141">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-141">Return Values</span></span>

- <span data-ttu-id="e4c6d-142">**NX_SUCCESS**: (0x00) başarılı Oto IP silme.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-142">**NX_SUCCESS**: (0x00) Successful AutoIP delete.</span></span>
- <span data-ttu-id="e4c6d-143">**NX_AUTO_IP_ERROR**: (0xa00) Oto IP silme hatası.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-143">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP delete error.</span></span>
- <span data-ttu-id="e4c6d-144">NX_PTR_ERROR (0x16): geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-144">NX_PTR_ERROR (0x16): Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="e4c6d-145">NX_CALLER_ERROR (0x11): Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-145">NX_CALLER_ERROR (0x11): Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e4c6d-146">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="e4c6d-146">Allowed From</span></span>

<span data-ttu-id="e4c6d-147">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="e4c6d-147">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e4c6d-148">Örnek</span><span class="sxs-lookup"><span data-stu-id="e4c6d-148">Example</span></span>

```c
/* Delete the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_delete(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully deleted. */
```

### <a name="see-also"></a><span data-ttu-id="e4c6d-149">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-149">See Also</span></span>

<span data-ttu-id="e4c6d-150">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="e4c6d-150">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_get_address"></a><span data-ttu-id="e4c6d-151">nx_auto_ip_get_address</span><span class="sxs-lookup"><span data-stu-id="e4c6d-151">nx_auto_ip_get_address</span></span>

<span data-ttu-id="e4c6d-152">Geçerli Oto IP adresini al</span><span class="sxs-lookup"><span data-stu-id="e4c6d-152">Get current AutoIP address</span></span>

### <a name="prototype"></a><span data-ttu-id="e4c6d-153">Prototype</span><span class="sxs-lookup"><span data-stu-id="e4c6d-153">Prototype</span></span>

```c
UINT nx_auto_ip_get_address(NX_AUTO_IP *auto_ip_ptr,
                            ULONG *local_ip_address);
```

### <a name="description"></a><span data-ttu-id="e4c6d-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e4c6d-154">Description</span></span>

<span data-ttu-id="e4c6d-155">Bu hizmet şu anda kurulum diğer IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-155">This service retrieves the currently setup AutoIP address.</span></span> <span data-ttu-id="e4c6d-156">Bir tane yoksa, 0.0.0.0 IP adresi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-156">If there isn't one, an IP address of 0.0.0.0 is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e4c6d-157">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-157">Input Parameters</span></span>

- <span data-ttu-id="e4c6d-158">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-158">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="e4c6d-159">**local_ip_address**: dönüş IP adresi hedefi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-159">**local_ip_address**: Destination for return IP address.</span></span>

### <a name="return-values"></a><span data-ttu-id="e4c6d-160">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-160">Return Values</span></span>

- <span data-ttu-id="e4c6d-161">**NX_SUCCESS**: (0x00) başarılı bir Oto IP adresi al.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-161">**NX_SUCCESS**: (0x00) Successful AutoIP address get.</span></span>
- <span data-ttu-id="e4c6d-162">**NX_AUTO_IP_NO_LOCAL**: (0xa01) geçerli bir Oto IP adresi yok.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-162">**NX_AUTO_IP_NO_LOCAL**: (0xA01) No valid AutoIP address.</span></span>
- <span data-ttu-id="e4c6d-163">NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-163">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="e4c6d-164">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-164">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e4c6d-165">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="e4c6d-165">Allowed From</span></span>

<span data-ttu-id="e4c6d-166">Başlatma, zamanlayıcılar, Iş parçacıkları, ISRs</span><span class="sxs-lookup"><span data-stu-id="e4c6d-166">Initialization, Timers, Threads, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="e4c6d-167">Örnek</span><span class="sxs-lookup"><span data-stu-id="e4c6d-167">Example</span></span>

```c
ULONG local_address;

/* Get the AutoIP address resolved by the instance "auto_ip_0." */
status = nx_auto_ip_get_address(&auto_ip_0, &local_address);

/* If status is NX_SUCCESS the local IP address is in "local_address." */
```

### <a name="see-also"></a><span data-ttu-id="e4c6d-168">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-168">See Also</span></span>

<span data-ttu-id="e4c6d-169">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="e4c6d-169">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_set_interface"></a><span data-ttu-id="e4c6d-170">nx_auto_ip_set_interface</span><span class="sxs-lookup"><span data-stu-id="e4c6d-170">nx_auto_ip_set_interface</span></span>

<span data-ttu-id="e4c6d-171">Oto IP için ağ arabirimini ayarla</span><span class="sxs-lookup"><span data-stu-id="e4c6d-171">Set network interface for AutoIP</span></span>

### <a name="prototype"></a><span data-ttu-id="e4c6d-172">Prototype</span><span class="sxs-lookup"><span data-stu-id="e4c6d-172">Prototype</span></span>

```c
UINT nx_auto_ip_set_interface(NX_AUTO_IP *auto_ip_ptr,
                                UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="e4c6d-173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e4c6d-173">Description</span></span>

<span data-ttu-id="e4c6d-174">Bu hizmet, bir ağ IP adresi için ağ arabirimi Oto IP 'si araştırmasını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-174">This service sets the index for the network interface AutoIP will probe for a network IP address.</span></span> <span data-ttu-id="e4c6d-175">Varsayılan değer sıfırdır (birincil ağ arabirimi).</span><span class="sxs-lookup"><span data-stu-id="e4c6d-175">The default is zero (the primary network interface).</span></span> <span data-ttu-id="e4c6d-176">Yalnızca çok sayfalı cihazlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-176">Only applicable for multihomed devices.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e4c6d-177">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-177">Input Parameters</span></span>

- <span data-ttu-id="e4c6d-178">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-178">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="e4c6d-179">**interface_index**: IÇIN araştırma IP adresi arabirimi</span><span class="sxs-lookup"><span data-stu-id="e4c6d-179">**interface_index**: Interface to probe IP address for</span></span>

### <a name="return-values"></a><span data-ttu-id="e4c6d-180">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-180">Return Values</span></span>

- <span data-ttu-id="e4c6d-181">**NX_SUCCESS**: (0x00) başarılı bir oto arabirimi kümesi</span><span class="sxs-lookup"><span data-stu-id="e4c6d-181">**NX_SUCCESS**: (0x00) Successful AutoIP interface set</span></span>
- <span data-ttu-id="e4c6d-182">**NX_AUTO_IP_BAD_INTERFACE_INDEX**: (0Xa02) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="e4c6d-182">**NX_AUTO_IP_BAD_INTERFACE_INDEX**: (0xA02) Invalid network interface</span></span> 
- <span data-ttu-id="e4c6d-183">NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-183">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="e4c6d-184">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-184">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e4c6d-185">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="e4c6d-185">Allowed From</span></span>

<span data-ttu-id="e4c6d-186">Başlatma, zamanlayıcılar, Iş parçacıkları, ISRs</span><span class="sxs-lookup"><span data-stu-id="e4c6d-186">Initialization, Timers, Threads, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="e4c6d-187">Örnek</span><span class="sxs-lookup"><span data-stu-id="e4c6d-187">Example</span></span>

```c
ULONG interface_index;

/* Set the network interface on which AutoIP probes for host address. */
status = nx_auto_ip_set_interface(&auto_ip_0, interface_index);

/* If status is NX_SUCCESS the network interface is valid and set in the AutoIP control block auto_ip_0. */
```

### <a name="see-also"></a><span data-ttu-id="e4c6d-188">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-188">See Also</span></span>

<span data-ttu-id="e4c6d-189">nx_auto_ip_create, nx_auto_ip_get_address, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="e4c6d-189">nx_auto_ip_create, nx_auto_ip_get_address, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_start"></a><span data-ttu-id="e4c6d-190">nx_auto_ip_start</span><span class="sxs-lookup"><span data-stu-id="e4c6d-190">nx_auto_ip_start</span></span>

<span data-ttu-id="e4c6d-191">Oto IP işlemesini Başlat</span><span class="sxs-lookup"><span data-stu-id="e4c6d-191">Start AutoIP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="e4c6d-192">Prototype</span><span class="sxs-lookup"><span data-stu-id="e4c6d-192">Prototype</span></span>

```c
UINT nx_auto_ip_start(NX_AUTO_IP *auto_ip_ptr,
                    ULONG starting_local_address);
```

### <a name="description"></a><span data-ttu-id="e4c6d-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e4c6d-193">Description</span></span>

<span data-ttu-id="e4c6d-194">Bu hizmet, daha önce oluşturulmuş bir Oto IP örneğinde, Oto IP protokolünü başlatır.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-194">This service starts the AutoIP protocol on a previously created AutoIP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e4c6d-195">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-195">Input Parameters</span></span>

- <span data-ttu-id="e4c6d-196">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-196">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="e4c6d-197">**starting_local_address**: Isteğe bağlı otomatik IP başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-197">**starting_local_address**: Optional AutoIP starting address.</span></span> <span data-ttu-id="e4c6d-198">IP_ADDRESS değeri (0, 0, 0, 0) bir rastgele bir bir bir bir bir bir bir bir bir bir IP adresi elde edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-198">A value of IP_ADDRESS(0,0,0,0) specifies that a random AutoIP address should be derived.</span></span> <span data-ttu-id="e4c6d-199">Aksi takdirde, geçerli bir bir bir bir bir bir bir bir bir bir bir IP adresi belirtilmişse NetX, bu adresi atamayı dener.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-199">Otherwise, if a valid AutoIP address is specified, NetX AutoIP attempts to assign that address.</span></span>

### <a name="return-values"></a><span data-ttu-id="e4c6d-200">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-200">Return Values</span></span>

- <span data-ttu-id="e4c6d-201">**NX_SUCCESS**: (0x00) başarılı bir oto başlatması.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-201">**NX_SUCCESS**: (0x00) Successful AutoIP start.</span></span>
- <span data-ttu-id="e4c6d-202">**NX_AUTO_IP_ERROR**: (0xa00) Oto IP başlatma hatası.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-202">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP start error.</span></span>
- <span data-ttu-id="e4c6d-203">NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-203">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="e4c6d-204">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-204">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e4c6d-205">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="e4c6d-205">Allowed From</span></span>

<span data-ttu-id="e4c6d-206">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="e4c6d-206">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="e4c6d-207">Örnek</span><span class="sxs-lookup"><span data-stu-id="e4c6d-207">Example</span></span>

```c
/* Start the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_start(&auto_ip_0, IP_ADDRESS(0,0,0,0));

/* If status is NX_SUCCESS an AutoIP instance was successfully started. */
```

### <a name="see-also"></a><span data-ttu-id="e4c6d-208">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-208">See Also</span></span>

<span data-ttu-id="e4c6d-209">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="e4c6d-209">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_stop"></a><span data-ttu-id="e4c6d-210">nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="e4c6d-210">nx_auto_ip_stop</span></span>

<span data-ttu-id="e4c6d-211">Oto IP işlemesini durdur</span><span class="sxs-lookup"><span data-stu-id="e4c6d-211">Stop AutoIP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="e4c6d-212">Prototype</span><span class="sxs-lookup"><span data-stu-id="e4c6d-212">Prototype</span></span>

```c
UINT nx_auto_ip_stop(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a><span data-ttu-id="e4c6d-213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e4c6d-213">Description</span></span>

<span data-ttu-id="e4c6d-214">Bu hizmet, daha önce oluşturulmuş ve başlatılan bir Oto IP örneğinde, Oto IP protokolünü sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-214">This service stops the AutoIP protocol on a previously created and started AutoIP instance.</span></span> <span data-ttu-id="e4c6d-215">Bu hizmet genellikle IP adresi DHCP aracılığıyla veya bir oto olmayan IP adresine el ile değiştirildiğinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-215">This service is typically used when the IP address is changed via DHCP or manually to a non-AutoIP address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="e4c6d-216">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-216">Input Parameters</span></span>

- <span data-ttu-id="e4c6d-217">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-217">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="e4c6d-218">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="e4c6d-218">Return Values</span></span>

- <span data-ttu-id="e4c6d-219">**NX_SUCCESS**: (0x00) başarılı bir oto durdur.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-219">**NX_SUCCESS**: (0x00) Successful AutoIP stop.</span></span>
- <span data-ttu-id="e4c6d-220">**NX_AUTO_IP_ERROR**: (0xa00) Oto IP durağı hatası.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-220">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP stop error.</span></span>
- <span data-ttu-id="e4c6d-221">NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-221">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="e4c6d-222">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-222">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="e4c6d-223">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="e4c6d-223">Allowed From</span></span>

<span data-ttu-id="e4c6d-224">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="e4c6d-224">Threads</span></span>

### <a name="example"></a><span data-ttu-id="e4c6d-225">Örnek</span><span class="sxs-lookup"><span data-stu-id="e4c6d-225">Example</span></span>

```c
/* Stop the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_stop(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully stopped. */
```

### <a name="see-also"></a><span data-ttu-id="e4c6d-226">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e4c6d-226">See Also</span></span>

<span data-ttu-id="e4c6d-227">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_start</span><span class="sxs-lookup"><span data-stu-id="e4c6d-227">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_start</span></span>