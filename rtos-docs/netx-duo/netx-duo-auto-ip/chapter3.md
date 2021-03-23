---
title: Bölüm 3-Azure RTOS NetX Duo Oto IP Hizmetleri açıklaması
description: Bu bölümde, tüm Azure RTOS NetX Duo Oto IP Hizmetleri (aşağıda listelenmiştir) alfabetik sırada bir açıklama bulunur.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 0935295ef9f7255c0851e1f64013884dce4c52f1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826165"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-autoip-services"></a><span data-ttu-id="fdddd-103">Bölüm 3-Azure RTOS NetX Duo Oto IP Hizmetleri açıklaması</span><span class="sxs-lookup"><span data-stu-id="fdddd-103">Chapter 3 - Description of Azure RTOS NetX Duo AutoIP services</span></span>

<span data-ttu-id="fdddd-104">Bu bölümde, tüm Azure RTOS NetX Duo Oto IP Hizmetleri (aşağıda listelenmiştir) alfabetik sırada bir açıklama bulunur.</span><span class="sxs-lookup"><span data-stu-id="fdddd-104">This chapter contains a description of all Azure RTOS NetX Duo AutoIP services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="fdddd-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="fdddd-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="fdddd-106">**nx_auto_ip_create**: *Oto IP örneği oluştur*</span><span class="sxs-lookup"><span data-stu-id="fdddd-106">**nx_auto_ip_create**: *Create AutoIP instance*</span></span>
- <span data-ttu-id="fdddd-107">**nx_auto_ip_delete**: *Oto IP örneğini Sil*</span><span class="sxs-lookup"><span data-stu-id="fdddd-107">**nx_auto_ip_delete**: *Delete AutoIP instance*</span></span>
- <span data-ttu-id="fdddd-108">**nx_auto_ip_get_address**: *geçerli Oto IP adresini al*</span><span class="sxs-lookup"><span data-stu-id="fdddd-108">**nx_auto_ip_get_address**: *Get current AutoIP address*</span></span>
- <span data-ttu-id="fdddd-109">**nx_auto_ip_set_interface**: *IP arabirimine bir Oto IP adresi ihtiyacı* olacak şekilde ayarla</span><span class="sxs-lookup"><span data-stu-id="fdddd-109">**nx_auto_ip_set_interface**: *Set IP interface needing an AutoIP address*</span></span>
- <span data-ttu-id="fdddd-110">**nx_auto_ip_start**: *Oto IP işlemesini Başlat*</span><span class="sxs-lookup"><span data-stu-id="fdddd-110">**nx_auto_ip_start**: *Start AutoIP processing*</span></span>
- <span data-ttu-id="fdddd-111">**nx_auto_ip_stop**: *Oto IP işlemesini durdur*</span><span class="sxs-lookup"><span data-stu-id="fdddd-111">**nx_auto_ip_stop**: *Stop AutoIP processing*</span></span>

## <a name="nx_auto_ip_create"></a><span data-ttu-id="fdddd-112">nx_auto_ip_create</span><span class="sxs-lookup"><span data-stu-id="fdddd-112">nx_auto_ip_create</span></span>

<span data-ttu-id="fdddd-113">Oto IP örneği oluştur</span><span class="sxs-lookup"><span data-stu-id="fdddd-113">Create AutoIP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="fdddd-114">Prototype</span><span class="sxs-lookup"><span data-stu-id="fdddd-114">Prototype</span></span>

```c
UINT nx_auto_ip_create(NX_AUTO_IP *auto_ip_ptr, CHAR *name,
                    NX_IP *ip_ptr, VOID *stack_ptr, ULONG stack_size,
                    UINT priority);
```

### <a name="description"></a><span data-ttu-id="fdddd-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdddd-115">Description</span></span>

<span data-ttu-id="fdddd-116">Bu hizmet, belirtilen IP örneğinde bir Oto IP örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fdddd-116">This service creates an AutoIP instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fdddd-117">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-117">Input Parameters</span></span>

- <span data-ttu-id="fdddd-118">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-118">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="fdddd-119">**ad**: Oto IP örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="fdddd-119">**name**: Name of AutoIP instance.</span></span>
- <span data-ttu-id="fdddd-120">**ip_ptr**: IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-120">**ip_ptr**: Pointer to IP instance.</span></span>
- <span data-ttu-id="fdddd-121">**stack_ptr**: Oto IP iş parçacığı yığın alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-121">**stack_ptr**: Pointer to AutoIP thread stack area.</span></span>
- <span data-ttu-id="fdddd-122">**stack_size**: Oto IP iş parçacığı yığını alanının boyutu.</span><span class="sxs-lookup"><span data-stu-id="fdddd-122">**stack_size**: Size of the AutoIP thread stack area.</span></span>
- <span data-ttu-id="fdddd-123">**Öncelik**: Oto IP iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="fdddd-123">**priority**: Priority of the AutoIP thread.</span></span>

> [!NOTE]
> <span data-ttu-id="fdddd-124">DHCP kullanılıyorsa, DHCP iş parçacığının IP örneği iş parçacığından ve Oto IP iş parçacığından daha yüksek bir önceliğe sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdddd-124">If DHCP is used, the DHCP thread must have a higher priority than the IP instance thread and the AutoIP thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="fdddd-125">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-125">Return Values</span></span>

- <span data-ttu-id="fdddd-126">**NX_SUCCESS**: (0x00) başarılı bir oto oluştur.</span><span class="sxs-lookup"><span data-stu-id="fdddd-126">**NX_SUCCESS**: (0x00) Successful AutoIP create.</span></span>
- <span data-ttu-id="fdddd-127">**NX_AUTO_IP_ERROR**: (0xa00) Oto IP oluşturma hatası.</span><span class="sxs-lookup"><span data-stu-id="fdddd-127">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP create error.</span></span>
- <span data-ttu-id="fdddd-128">NX_PTR_ERROR: (0x16) geçersiz Oto IP, ip_ptr veya yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-128">NX_PTR_ERROR: (0x16) Invalid AutoIP, ip_ptr, or stack pointer.</span></span>
- <span data-ttu-id="fdddd-129">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="fdddd-129">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fdddd-130">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fdddd-130">Allowed From</span></span>

<span data-ttu-id="fdddd-131">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="fdddd-131">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="fdddd-132">Örnek</span><span class="sxs-lookup"><span data-stu-id="fdddd-132">Example</span></span>

```c
/* Create the AutoIP instance "auto_ip_0" on "ip_0". */
status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);

/* If status is NX_SUCCESS an AutoIP instance was successfully created. */
```

### <a name="see-also"></a><span data-ttu-id="fdddd-133">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="fdddd-133">See Also</span></span>

<span data-ttu-id="fdddd-134">nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="fdddd-134">nx_auto_ip_delete, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_delete"></a><span data-ttu-id="fdddd-135">nx_auto_ip_delete</span><span class="sxs-lookup"><span data-stu-id="fdddd-135">nx_auto_ip_delete</span></span>

<span data-ttu-id="fdddd-136">Oto IP örneğini Sil</span><span class="sxs-lookup"><span data-stu-id="fdddd-136">Delete AutoIP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="fdddd-137">Prototype</span><span class="sxs-lookup"><span data-stu-id="fdddd-137">Prototype</span></span>

```c
UINT nx_auto_ip_delete(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a><span data-ttu-id="fdddd-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdddd-138">Description</span></span>

<span data-ttu-id="fdddd-139">Bu hizmet, belirtilen IP örneğinde daha önce oluşturulmuş bir Oto IP örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="fdddd-139">This service deletes a previously created AutoIP instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fdddd-140">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-140">Input Parameters</span></span>

- <span data-ttu-id="fdddd-141">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-141">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="fdddd-142">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-142">Return Values</span></span>

- <span data-ttu-id="fdddd-143">**NX_SUCCESS**: (0x00) başarılı Oto IP silme.</span><span class="sxs-lookup"><span data-stu-id="fdddd-143">**NX_SUCCESS**: (0x00) Successful AutoIP delete.</span></span>
- <span data-ttu-id="fdddd-144">**NX_AUTO_IP_ERROR**: (0xa00) Oto IP silme hatası.</span><span class="sxs-lookup"><span data-stu-id="fdddd-144">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP delete error.</span></span>
- <span data-ttu-id="fdddd-145">NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-145">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="fdddd-146">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="fdddd-146">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fdddd-147">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fdddd-147">Allowed From</span></span>

<span data-ttu-id="fdddd-148">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="fdddd-148">Threads</span></span>

### <a name="example"></a><span data-ttu-id="fdddd-149">Örnek</span><span class="sxs-lookup"><span data-stu-id="fdddd-149">Example</span></span>

```c
/* Delete the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_delete(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully deleted. */
```

### <a name="see-also"></a><span data-ttu-id="fdddd-150">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="fdddd-150">See Also</span></span>

<span data-ttu-id="fdddd-151">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="fdddd-151">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_get_address, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_get_address"></a><span data-ttu-id="fdddd-152">nx_auto_ip_get_address</span><span class="sxs-lookup"><span data-stu-id="fdddd-152">nx_auto_ip_get_address</span></span>

<span data-ttu-id="fdddd-153">Geçerli Oto IP adresini al</span><span class="sxs-lookup"><span data-stu-id="fdddd-153">Get current AutoIP address</span></span>

### <a name="prototype"></a><span data-ttu-id="fdddd-154">Prototype</span><span class="sxs-lookup"><span data-stu-id="fdddd-154">Prototype</span></span>

```c
UINT nx_auto_ip_get_address(NX_AUTO_IP *auto_ip_ptr,
                            ULONG *local_ip_address);
```

### <a name="description"></a><span data-ttu-id="fdddd-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdddd-155">Description</span></span>

<span data-ttu-id="fdddd-156">Bu hizmet şu anda kurulum diğer IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="fdddd-156">This service retrieves the currently setup AutoIP address.</span></span> <span data-ttu-id="fdddd-157">Bir tane yoksa, 0.0.0.0 IP adresi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="fdddd-157">If there isn't one, an IP address of 0.0.0.0 is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fdddd-158">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-158">Input Parameters</span></span>

- <span data-ttu-id="fdddd-159">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-159">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="fdddd-160">**local_ip_address**: dönüş IP adresi hedefi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-160">**local_ip_address**: Destination for return IP address.</span></span>

### <a name="return-values"></a><span data-ttu-id="fdddd-161">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-161">Return Values</span></span>

- <span data-ttu-id="fdddd-162">**NX_SUCCESS**: (0x00) başarılı bir Oto IP adresi al.</span><span class="sxs-lookup"><span data-stu-id="fdddd-162">**NX_SUCCESS**: (0x00) Successful AutoIP address get.</span></span>
- <span data-ttu-id="fdddd-163">**NX_AUTO_IP_NO_LOCAL**: (0xa01) geçerli bir Oto IP adresi yok.</span><span class="sxs-lookup"><span data-stu-id="fdddd-163">**NX_AUTO_IP_NO_LOCAL**: (0xA01) No valid AutoIP address.</span></span>
- <span data-ttu-id="fdddd-164">NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-164">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="fdddd-165">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="fdddd-165">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fdddd-166">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fdddd-166">Allowed From</span></span>

<span data-ttu-id="fdddd-167">Başlatma, zamanlayıcılar, Iş parçacıkları, ISRs</span><span class="sxs-lookup"><span data-stu-id="fdddd-167">Initialization, Timers, Threads, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="fdddd-168">Örnek</span><span class="sxs-lookup"><span data-stu-id="fdddd-168">Example</span></span>

```c
ULONG local_address;

/* Get the AutoIP address resolved by the instance "auto_ip_0." */
status = nx_auto_ip_get_address(&auto_ip_0, &local_address);

/* If status is NX_SUCCESS the local IP address is in "local_address." */
```

### <a name="see-also"></a><span data-ttu-id="fdddd-169">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="fdddd-169">See Also</span></span>

<span data-ttu-id="fdddd-170">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="fdddd-170">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_set_interface"></a><span data-ttu-id="fdddd-171">nx_auto_ip_set_interface</span><span class="sxs-lookup"><span data-stu-id="fdddd-171">nx_auto_ip_set_interface</span></span>

<span data-ttu-id="fdddd-172">Oto IP için ağ arabirimini ayarla</span><span class="sxs-lookup"><span data-stu-id="fdddd-172">Set network interface for AutoIP</span></span>

### <a name="prototype"></a><span data-ttu-id="fdddd-173">Prototype</span><span class="sxs-lookup"><span data-stu-id="fdddd-173">Prototype</span></span>

```c
UINT nx_auto_ip_set_interface(NX_AUTO_IP *auto_ip_ptr,
                            UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="fdddd-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdddd-174">Description</span></span>

<span data-ttu-id="fdddd-175">Bu hizmet, bir ağ IP adresi için ağ arabirimi Oto IP 'si araştırmasını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="fdddd-175">This service sets the index for the network interface AutoIP will probe for a network IP address.</span></span> <span data-ttu-id="fdddd-176">Varsayılan değer sıfırdır (birincil ağ arabirimi).</span><span class="sxs-lookup"><span data-stu-id="fdddd-176">The default is zero (the primary network interface).</span></span> <span data-ttu-id="fdddd-177">Yalnızca çok sayfalı cihazlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fdddd-177">Only applicable for multihomed devices.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fdddd-178">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-178">Input Parameters</span></span>

- <span data-ttu-id="fdddd-179">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-179">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="fdddd-180">**interface_index**: IÇIN araştırma IP adresi arabirimi</span><span class="sxs-lookup"><span data-stu-id="fdddd-180">**interface_index**: Interface to probe IP address for</span></span>

### <a name="return-values"></a><span data-ttu-id="fdddd-181">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-181">Return Values</span></span>

- <span data-ttu-id="fdddd-182">**NX_SUCCESS**: (0x00) başarılı bir oto arabirimi kümesi</span><span class="sxs-lookup"><span data-stu-id="fdddd-182">**NX_SUCCESS**: (0x00) Successful AutoIP interface set</span></span>
- <span data-ttu-id="fdddd-183">**NX_AUTO_IP_BAD_INTERFACE_INDEX**: (0Xa02) geçersiz ağ arabirimi NX_PTR_ERROR (0x16) geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-183">**NX_AUTO_IP_BAD_INTERFACE_INDEX**: (0xA02) Invalid network interface NX_PTR_ERROR (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="fdddd-184">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="fdddd-184">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fdddd-185">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fdddd-185">Allowed From</span></span>

<span data-ttu-id="fdddd-186">Başlatma, zamanlayıcılar, Iş parçacıkları, ISRs</span><span class="sxs-lookup"><span data-stu-id="fdddd-186">Initialization, Timers, Threads, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="fdddd-187">Örnek</span><span class="sxs-lookup"><span data-stu-id="fdddd-187">Example</span></span>

```c
ULONG interface_index;

/* Set the network interface on which AutoIP probes for host address. */
status = nx_auto_ip_set_interface(&auto_ip_0, interface_index);

/* If status is NX_SUCCESS the network interface is valid and set in the AutoIP control block *auto_ip_0*. */
```

### <a name="see-also"></a><span data-ttu-id="fdddd-188">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="fdddd-188">See Also</span></span>

<span data-ttu-id="fdddd-189">nx_auto_ip_create, nx_auto_ip_get_address, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="fdddd-189">nx_auto_ip_create, nx_auto_ip_get_address, nx_auto_ip_delete, nx_auto_ip_start, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_start"></a><span data-ttu-id="fdddd-190">nx_auto_ip_start</span><span class="sxs-lookup"><span data-stu-id="fdddd-190">nx_auto_ip_start</span></span>

<span data-ttu-id="fdddd-191">Oto IP işlemesini Başlat</span><span class="sxs-lookup"><span data-stu-id="fdddd-191">Start AutoIP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="fdddd-192">Prototype</span><span class="sxs-lookup"><span data-stu-id="fdddd-192">Prototype</span></span>

```c
UINT nx_auto_ip_start(NX_AUTO_IP *auto_ip_ptr,
                    ULONG starting_local_address);
```

### <a name="description"></a><span data-ttu-id="fdddd-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdddd-193">Description</span></span>

<span data-ttu-id="fdddd-194">Bu hizmet, daha önce oluşturulmuş bir Oto IP örneğinde, Oto IP protokolünü başlatır.</span><span class="sxs-lookup"><span data-stu-id="fdddd-194">This service starts the AutoIP protocol on a previously created AutoIP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fdddd-195">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-195">Input Parameters</span></span>

- <span data-ttu-id="fdddd-196">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-196">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>
- <span data-ttu-id="fdddd-197">**starting_local_address**: Isteğe bağlı otomatik IP başlangıç adresi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-197">**starting_local_address**: Optional AutoIP starting address.</span></span> <span data-ttu-id="fdddd-198">IP_ADDRESS değeri (0, 0, 0, 0) bir rastgele bir bir bir bir bir bir bir bir bir bir IP adresi elde edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="fdddd-198">A value of IP_ADDRESS(0,0,0,0) specifies that a random AutoIP address should be derived.</span></span> <span data-ttu-id="fdddd-199">Aksi takdirde, geçerli bir bir bir bir bir bir bir bir bir bir bir IP adresi belirtilmişse NetX, bu adresi atamayı dener.</span><span class="sxs-lookup"><span data-stu-id="fdddd-199">Otherwise, if a valid AutoIP address is specified, NetX AutoIP attempts to assign that address.</span></span>

### <a name="return-values"></a><span data-ttu-id="fdddd-200">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-200">Return Values</span></span>

- <span data-ttu-id="fdddd-201">**NX_SUCCESS**: (0x00) başarılı bir oto başlatması.</span><span class="sxs-lookup"><span data-stu-id="fdddd-201">**NX_SUCCESS**: (0x00) Successful AutoIP start.</span></span>
- <span data-ttu-id="fdddd-202">**NX_AUTO_IP_ERROR**: (0xa00) Oto IP başlatma hatası.</span><span class="sxs-lookup"><span data-stu-id="fdddd-202">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP start error.</span></span>
- <span data-ttu-id="fdddd-203">NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-203">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="fdddd-204">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="fdddd-204">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fdddd-205">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fdddd-205">Allowed From</span></span>

<span data-ttu-id="fdddd-206">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="fdddd-206">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="fdddd-207">Örnek</span><span class="sxs-lookup"><span data-stu-id="fdddd-207">Example</span></span>

```c
/* Start the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_start(&auto_ip_0, IP_ADDRESS(0,0,0,0));

/* If status is NX_SUCCESS an AutoIP instance was successfully started. */
```

### <a name="see-also"></a><span data-ttu-id="fdddd-208">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="fdddd-208">See Also</span></span>

<span data-ttu-id="fdddd-209">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="fdddd-209">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_stop</span></span>

## <a name="nx_auto_ip_stop"></a><span data-ttu-id="fdddd-210">nx_auto_ip_stop</span><span class="sxs-lookup"><span data-stu-id="fdddd-210">nx_auto_ip_stop</span></span>

<span data-ttu-id="fdddd-211">Oto IP işlemesini durdur</span><span class="sxs-lookup"><span data-stu-id="fdddd-211">Stop AutoIP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="fdddd-212">Prototype</span><span class="sxs-lookup"><span data-stu-id="fdddd-212">Prototype</span></span>

```c
UINT nx_auto_ip_stop(NX_AUTO_IP *auto_ip_ptr);
```

### <a name="description"></a><span data-ttu-id="fdddd-213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdddd-213">Description</span></span>

<span data-ttu-id="fdddd-214">Bu hizmet, daha önce oluşturulmuş ve başlatılan bir Oto IP örneğinde, Oto IP protokolünü sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="fdddd-214">This service stops the AutoIP protocol on a previously created and started AutoIP instance.</span></span> <span data-ttu-id="fdddd-215">Bu hizmet genellikle IP adresi DHCP aracılığıyla veya bir oto olmayan IP adresine el ile değiştirildiğinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fdddd-215">This service is typically used when the IP address is changed via DHCP or manually to a non-AutoIP address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fdddd-216">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-216">Input Parameters</span></span>

- <span data-ttu-id="fdddd-217">**auto_ip_ptr**: Oto IP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-217">**auto_ip_ptr**: Pointer to AutoIP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="fdddd-218">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fdddd-218">Return Values</span></span>

- <span data-ttu-id="fdddd-219">**NX_SUCCESS**: (0x00) başarılı bir oto durdur.</span><span class="sxs-lookup"><span data-stu-id="fdddd-219">**NX_SUCCESS**: (0x00) Successful AutoIP stop.</span></span>
- <span data-ttu-id="fdddd-220">**NX_AUTO_IP_ERROR**: (0xa00) Oto IP durağı hatası.</span><span class="sxs-lookup"><span data-stu-id="fdddd-220">**NX_AUTO_IP_ERROR**: (0xA00) AutoIP stop error.</span></span>
- <span data-ttu-id="fdddd-221">NX_PTR_ERROR: (0x16) geçersiz bir Oto IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="fdddd-221">NX_PTR_ERROR: (0x16) Invalid AutoIP pointer.</span></span>
- <span data-ttu-id="fdddd-222">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="fdddd-222">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fdddd-223">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fdddd-223">Allowed From</span></span>

<span data-ttu-id="fdddd-224">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="fdddd-224">Threads</span></span>

### <a name="example"></a><span data-ttu-id="fdddd-225">Örnek</span><span class="sxs-lookup"><span data-stu-id="fdddd-225">Example</span></span>

```c
/* Stop the AutoIP instance "auto_ip_0." */
status = nx_auto_ip_stop(&auto_ip_0);

/* If status is NX_SUCCESS an AutoIP instance was successfully stopped. */
```

### <a name="see-also"></a><span data-ttu-id="fdddd-226">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="fdddd-226">See Also</span></span>

<span data-ttu-id="fdddd-227">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_start</span><span class="sxs-lookup"><span data-stu-id="fdddd-227">nx_auto_ip_create, nx_auto_ip_set_interface, nx_auto_ip_delete, nx_auto_ip_get_address, nx_auto_ip_start</span></span>