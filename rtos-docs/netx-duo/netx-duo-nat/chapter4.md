---
title: Bölüm 4-NAT hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo NAT API hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8bdbdfcb2da6425fb99cadc7b2f6815dedc12953
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825852"
---
# <a name="chapter-4---description-of-nat-services"></a><span data-ttu-id="b4e1c-103">Bölüm 4-NAT hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="b4e1c-103">Chapter 4 - Description of NAT services</span></span>

<span data-ttu-id="b4e1c-104">Bu bölüm, tüm NetX Duo NAT API hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-104">This chapter contains a description of all NetX Duo NAT API services (listed below) in alphabetical order.</span></span>

> [!NOTE]
> <span data-ttu-id="b4e1c-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_nat_create"></a><span data-ttu-id="b4e1c-106">nx_nat_create</span><span class="sxs-lookup"><span data-stu-id="b4e1c-106">nx_nat_create</span></span>

<span data-ttu-id="b4e1c-107">NAT sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4e1c-107">Create a NAT Server</span></span>

### <a name="prototype"></a><span data-ttu-id="b4e1c-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="b4e1c-108">Prototype</span></span>

```C
UINT nx_nat_create(NX_NAT_DEVICE *nat_ptr, NX_IP *ip_ptr,
    UINT global_interface_index,
    VOID *dynamic_cache_memory,
    UINT dynamic_cache_size);
```

### <a name="description"></a><span data-ttu-id="b4e1c-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4e1c-109">Description</span></span>

<span data-ttu-id="b4e1c-110">Bu hizmet NAT sunucusunun bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-110">This service creates an instance of the NAT server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b4e1c-111">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-111">Input Parameters</span></span>

- <span data-ttu-id="b4e1c-112">**nat_ptr** Oluşturulacak NAT örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-112">**nat_ptr** Pointer to NAT instance to create</span></span>
- <span data-ttu-id="b4e1c-113">IP örneğine **Ip_ptr işaretçisi**</span><span class="sxs-lookup"><span data-stu-id="b4e1c-113">**ip_ptr Pointer** to IP instance</span></span>
- <span data-ttu-id="b4e1c-114">**global_interface_index** Genel ağ arabiriminin dizini</span><span class="sxs-lookup"><span data-stu-id="b4e1c-114">**global_interface_index** Index to the global network interface</span></span>
- <span data-ttu-id="b4e1c-115">**dynamic_cache_memory** İşaretçi bellek alanını NAT tablosuna</span><span class="sxs-lookup"><span data-stu-id="b4e1c-115">**dynamic_cache_memory** Pointer memory area to NAT table</span></span>
- <span data-ttu-id="b4e1c-116">**dynamic_cache_size** NAT tablosu için bellek alanı boyutu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-116">**dynamic_cache_size** Size of memory area for NAT table</span></span>

### <a name="return-values"></a><span data-ttu-id="b4e1c-117">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-117">Return Values</span></span>

- <span data-ttu-id="b4e1c-118">**NX_SUCCESS** (0x00) NAT sunucusu başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-118">**NX_SUCCESS** (0x00) NAT server successfully created</span></span>
- <span data-ttu-id="b4e1c-119">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-119">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="b4e1c-120">NX_NAT_PARAM_ERROR (0xD01) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-120">NX_NAT_PARAM_ERROR (0xD01) Invalid non pointer input</span></span>
- <span data-ttu-id="b4e1c-121">NX_NAT_CACHE_ERROR (0xD02) geçersiz önbellek işaretçisi girişi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-121">NX_NAT_CACHE_ERROR (0xD02) Invalid cache pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b4e1c-122">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b4e1c-122">Allowed From</span></span>

<span data-ttu-id="b4e1c-123">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-123">Application code</span></span>

### <a name="example"></a><span data-ttu-id="b4e1c-124">Örnek</span><span class="sxs-lookup"><span data-stu-id="b4e1c-124">Example</span></span>

```C
#define NX_NAT_ENTRY_CACHE_SIZE 20480

static UCHAR nat_cache[NX_NAT_ENTRY_CACHE_SIZE];
UINT global_interface_index = 0;

/* Create a NAT Server and cache with a global interface index. */
status = nx_nat_create(nat_ptr, ip_ptr, global_interface_index,
    nat_cache, NX_NAT_ENTRY_CACHE_SIZE);

/* If status = NX_SUCCESS, the NAT instance was successfully
    created. */
```

## <a name="nx_nat_delete"></a><span data-ttu-id="b4e1c-125">nx_nat_delete</span><span class="sxs-lookup"><span data-stu-id="b4e1c-125">nx_nat_delete</span></span>

<span data-ttu-id="b4e1c-126">Bir NAT sunucusunu silme</span><span class="sxs-lookup"><span data-stu-id="b4e1c-126">Delete a NAT Server</span></span>

### <a name="prototype"></a><span data-ttu-id="b4e1c-127">Prototype</span><span class="sxs-lookup"><span data-stu-id="b4e1c-127">Prototype</span></span>

```C
UINT nx_nat_delete(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a><span data-ttu-id="b4e1c-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4e1c-128">Description</span></span>

<span data-ttu-id="b4e1c-129">Bu hizmet, önceden oluşturulmuş bir NAT sunucusunu siler.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-129">This service deletes a previously created NAT Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b4e1c-130">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-130">Input Parameters</span></span>

- <span data-ttu-id="b4e1c-131">**nat_ptr** Silinecek NAT örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-131">**nat_ptr** Pointer to NAT instance to delete</span></span>

### <a name="return-values"></a><span data-ttu-id="b4e1c-132">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-132">Return Values</span></span>

- <span data-ttu-id="b4e1c-133">**NX_SUCCESS** (0x00) NAT başarıyla silindi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-133">**NX_SUCCESS** (0x00) NAT successfully deleted</span></span>
- <span data-ttu-id="b4e1c-134">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-134">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b4e1c-135">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b4e1c-135">Allowed From</span></span>

<span data-ttu-id="b4e1c-136">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-136">Application code</span></span>

### <a name="example"></a><span data-ttu-id="b4e1c-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="b4e1c-137">Example</span></span>

```C
/* Delete the NAT instance. */
status = nx_nat_delete (nat_ptr);

/* If the NAT instance was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_nat_enable"></a><span data-ttu-id="b4e1c-138">nx_nat_enable</span><span class="sxs-lookup"><span data-stu-id="b4e1c-138">nx_nat_enable</span></span>

<span data-ttu-id="b4e1c-139">NAT için IP örneğini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b4e1c-139">Enable the IP instance for NAT</span></span>

### <a name="prototype"></a><span data-ttu-id="b4e1c-140">Prototype</span><span class="sxs-lookup"><span data-stu-id="b4e1c-140">Prototype</span></span>

```C
UINT nx_nat_enable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a><span data-ttu-id="b4e1c-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4e1c-141">Description</span></span>

<span data-ttu-id="b4e1c-142">Bu hizmet NAT için IP örneğini (örn. alınan paketleri NAT sunucusuna ilet) sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-142">This service enables the IP instance for NAT (e.g. forward received packets to the NAT server).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b4e1c-143">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-143">Input Parameters</span></span>

- <span data-ttu-id="b4e1c-144">**nat_ptr** NAT örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-144">**nat_ptr** Pointer to NAT instance</span></span>

### <a name="return-values"></a><span data-ttu-id="b4e1c-145">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-145">Return Values</span></span>

- <span data-ttu-id="b4e1c-146">**NX_SUCCESS** (0x00) NAT başarıyla etkinleştirildi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-146">**NX_SUCCESS** (0x00) NAT successfully enabled</span></span>
- <span data-ttu-id="b4e1c-147">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-147">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b4e1c-148">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b4e1c-148">Allowed From</span></span>

<span data-ttu-id="b4e1c-149">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-149">Application code</span></span>

### <a name="example"></a><span data-ttu-id="b4e1c-150">Örnek</span><span class="sxs-lookup"><span data-stu-id="b4e1c-150">Example</span></span>

```C
/* Enable the NAT server. */
status = nx_nat_enable (nat_ptr);

/* If status = NX_SUCCESS, the IP instance was successfully enabled for NAT. */
```

## <a name="nx_nat_disable"></a><span data-ttu-id="b4e1c-151">nx_nat_disable</span><span class="sxs-lookup"><span data-stu-id="b4e1c-151">nx_nat_disable</span></span>

<span data-ttu-id="b4e1c-152">NAT için IP örneğini devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="b4e1c-152">Disable the IP instance for NAT</span></span>

### <a name="prototype"></a><span data-ttu-id="b4e1c-153">Prototype</span><span class="sxs-lookup"><span data-stu-id="b4e1c-153">Prototype</span></span>

```C
UINT nx_nat_disable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a><span data-ttu-id="b4e1c-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4e1c-154">Description</span></span>

<span data-ttu-id="b4e1c-155">Bu hizmet, IP örneğinde NAT 'yi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-155">This service disables NAT on the IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b4e1c-156">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-156">Input Parameters</span></span>

- <span data-ttu-id="b4e1c-157">**nat_ptr** NAT örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-157">**nat_ptr** Pointer to NAT instance</span></span>

### <a name="return-values"></a><span data-ttu-id="b4e1c-158">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-158">Return Values</span></span>

- <span data-ttu-id="b4e1c-159">**NX_SUCCESS** (0x00) NAT başarıyla devre dışı bırakıldı</span><span class="sxs-lookup"><span data-stu-id="b4e1c-159">**NX_SUCCESS** (0x00) NAT successfully disabled</span></span>
- <span data-ttu-id="b4e1c-160">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-160">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b4e1c-161">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b4e1c-161">Allowed From</span></span>

<span data-ttu-id="b4e1c-162">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-162">Application code</span></span>

### <a name="example"></a><span data-ttu-id="b4e1c-163">Örnek</span><span class="sxs-lookup"><span data-stu-id="b4e1c-163">Example</span></span>

```C
/* Disable the NAT server. */
status = nx_nat_disable (nat_ptr);

/* If status = NX_SUCCESS the NAT operation successfully disable. */
```

## <a name="nx_nat_cache_notify_set"></a><span data-ttu-id="b4e1c-164">nx_nat_cache_notify_set</span><span class="sxs-lookup"><span data-stu-id="b4e1c-164">nx_nat_cache_notify_set</span></span>

<span data-ttu-id="b4e1c-165">Önbellek tam bildirimi geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="b4e1c-165">Set a cache full notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="b4e1c-166">Prototype</span><span class="sxs-lookup"><span data-stu-id="b4e1c-166">Prototype</span></span>

```C
UINT nx_nat_cache_notify_set(NX_NAT_DEVICE *nat_ptr,
    VOID (*cache_full_notify_cb)
    (NX_NAT_DEVICE *nat_ptr)));
```

### <a name="description"></a><span data-ttu-id="b4e1c-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4e1c-167">Description</span></span>

<span data-ttu-id="b4e1c-168">Bu hizmet, Kullanıcı tanımlı önbellek tam bildirim işlevine işaret eden cache_full_notify_cb giriş işlevi işaretçisi ile önbellek tam geri çağırma işlemini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-168">This service registers the cache full callback with the input function pointer cache_full_notify_cb which points to a user defined cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b4e1c-169">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-169">Input Parameters</span></span>

- <span data-ttu-id="b4e1c-170">**nat_ptr** NAT örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-170">**nat_ptr** Pointer to NAT instance</span></span>
- <span data-ttu-id="b4e1c-171">**cache_full_notify_cb** Cache Full NOTIFY işlevi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-171">**cache_full_notify_cb** Pointer to cache full notify function</span></span>

### <a name="return-values"></a><span data-ttu-id="b4e1c-172">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-172">Return Values</span></span>

- <span data-ttu-id="b4e1c-173">**NX_SUCCESS** (0x00) önbellek tam bildirme işlevi başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="b4e1c-173">**NX_SUCCESS** (0x00) Cache full notify function successfully set</span></span>
- <span data-ttu-id="b4e1c-174">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-174">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="b4e1c-175">NX_NAT_PARAM_ERROR (0xD01) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-175">NX_NAT_PARAM_ERROR (0xD01) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b4e1c-176">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b4e1c-176">Allowed From</span></span>

<span data-ttu-id="b4e1c-177">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-177">Application code</span></span>

### <a name="example"></a><span data-ttu-id="b4e1c-178">Örnek</span><span class="sxs-lookup"><span data-stu-id="b4e1c-178">Example</span></span>

```C
/* Set the cache full notify callback function to the NAT instance. */
status = nx_nat_cache_notify_set(nat_ptr, cache_full_notify_cb);

/* If status = NX_SUCCESS the callback function was successfully set. */
```

## <a name="nx_nat_inbound_entry_create"></a><span data-ttu-id="b4e1c-179">nx_nat_inbound_entry_create</span><span class="sxs-lookup"><span data-stu-id="b4e1c-179">nx_nat_inbound_entry_create</span></span>

<span data-ttu-id="b4e1c-180">NAT çeviri tablosunda bir gelen giriş oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4e1c-180">Create an inbound entry in the NAT translation table</span></span>

### <a name="prototype"></a><span data-ttu-id="b4e1c-181">Prototype</span><span class="sxs-lookup"><span data-stu-id="b4e1c-181">Prototype</span></span>

```C
UINT nx_nat_inbound_entry_create(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *entry_ptr
    ULONG local_ip_address,
    USHORT external_port,
    USHORT local_port, UCHAR protocol);
```

### <a name="description"></a><span data-ttu-id="b4e1c-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4e1c-182">Description</span></span>

<span data-ttu-id="b4e1c-183">Bu hizmet, bir gelen girişi statik (kalıcı giriş, süresiz) olarak oluşturur ve NAT çeviri tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-183">This service creates an inbound entry as static (permanent entry, never expires) and adds it to the NAT translation table.</span></span> <span data-ttu-id="b4e1c-184">Bu girişler genellikle, dış ağdaki bir konaktan bir bağlantının başlatıldığı yerel ana bilgisayar sunucuları için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-184">These entries are usually created for local host servers where a connection is initiated from a host on the outside network.</span></span> <span data-ttu-id="b4e1c-185">NAT sunucusu, dış bağlantı noktasının çeviri tablosunda zaten kullanımda olmadığını veya aynı protokolün daha önce var olan bir NetX Duo yuvasına göre bağlandığını denetler.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-185">The NAT server checks that the external port is not already in use in the translation table or bound by a previously existing NetX Duo socket of the same protocol.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b4e1c-186">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-186">Input Parameters</span></span>

- <span data-ttu-id="b4e1c-187">**nat_ptr** NAT örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-187">**nat_ptr** Pointer to NAT instance</span></span>
- <span data-ttu-id="b4e1c-188">**entry_ptr** Çeviri girdisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-188">**entry_ptr** Pointer to translation entry</span></span>
- <span data-ttu-id="b4e1c-189">**local_ip_address** Yerel ana bilgisayar IP adresi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-189">**local_ip_address** Local host IP address</span></span>
- <span data-ttu-id="b4e1c-190">**external_port** Dış ağdaki hedef bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="b4e1c-190">**external_port** Destination port on the external network</span></span>
- <span data-ttu-id="b4e1c-191">**local_port** Kaynak (yerel ana bilgisayar) bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="b4e1c-191">**local_port** Source (local host) port</span></span>
- <span data-ttu-id="b4e1c-192">**protokol** Paket Protokolü (örn. TCP)</span><span class="sxs-lookup"><span data-stu-id="b4e1c-192">**protocol** Packet protocol (e.g TCP)</span></span>

### <a name="return-values"></a><span data-ttu-id="b4e1c-193">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-193">Return Values</span></span>

- <span data-ttu-id="b4e1c-194">**NX_SUCCESS** (0x00) girdisi başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-194">**NX_SUCCESS** (0x00) Entry successfully created</span></span>
- <span data-ttu-id="b4e1c-195">**NX_NAT_PORT_UNAVAILABLE** (0XD0D) geçersiz dış bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="b4e1c-195">**NX_NAT_PORT_UNAVAILABLE** (0xD0D) Invalid external port</span></span>
- <span data-ttu-id="b4e1c-196">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-196">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="b4e1c-197">NX_NAT_PARAM_ERROR (0xD01) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-197">NX_NAT_PARAM_ERROR (0xD01) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b4e1c-198">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b4e1c-198">Allowed From</span></span>

<span data-ttu-id="b4e1c-199">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-199">Application code</span></span>

### <a name="example"></a><span data-ttu-id="b4e1c-200">Örnek</span><span class="sxs-lookup"><span data-stu-id="b4e1c-200">Example</span></span>

```C
/* Create an entry for an inbound TCP packet. */
status = nx_nat_inbound_entry_create(nat_ptr, entry_ptr,
    IP_ADDRESS(192,168,2,2), 5001, 5001,
    NX_PROTOCOL_TCP);

/* If status = NX_SUCCESS the entry was successfully created. */
```

## <a name="nx_nat_inbound_entry_delete"></a><span data-ttu-id="b4e1c-201">nx_nat_inbound_entry_delete</span><span class="sxs-lookup"><span data-stu-id="b4e1c-201">nx_nat_inbound_entry_delete</span></span>

<span data-ttu-id="b4e1c-202">NAT çeviri tablosunda bir gelen girişi silme</span><span class="sxs-lookup"><span data-stu-id="b4e1c-202">Delete an inbound entry in the NAT translation table</span></span>

### <a name="prototype"></a><span data-ttu-id="b4e1c-203">Prototype</span><span class="sxs-lookup"><span data-stu-id="b4e1c-203">Prototype</span></span>

```C
UINT nx_nat_inbound_entry_delete(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *delete_entry_ptr)
```

### <a name="description"></a><span data-ttu-id="b4e1c-204">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4e1c-204">Description</span></span>

<span data-ttu-id="b4e1c-205">Bu hizmet, belirtilen gelen girdiyi çeviri tablosundan siler.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-205">This service deletes the specified inbound entry from the translation table.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b4e1c-206">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-206">Input Parameters</span></span>

- <span data-ttu-id="b4e1c-207">**nat_ptr** NAT örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-207">**nat_ptr** Pointer to NAT instance</span></span>
- <span data-ttu-id="b4e1c-208">**delete_entry_ptr** NAT çeviri girdisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-208">**delete_entry_ptr** Pointer to the NAT translation entry</span></span>

### <a name="return-values"></a><span data-ttu-id="b4e1c-209">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b4e1c-209">Return Values</span></span>

- <span data-ttu-id="b4e1c-210">**NX_SUCCESS** (0x00) girdisi başarıyla silindi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-210">**NX_SUCCESS** (0x00) Entry successfully deleted</span></span>
- <span data-ttu-id="b4e1c-211">**NX_NAT_ENTRY_NOT_FOUND** (0xd04) girişi bulunamadı</span><span class="sxs-lookup"><span data-stu-id="b4e1c-211">**NX_NAT_ENTRY_NOT_FOUND** (0xD04) Entry does not found</span></span>
- <span data-ttu-id="b4e1c-212">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="b4e1c-212">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="b4e1c-213">NX_NAT_ENTRY_TYPE_ERROR (0xD0C) geçersiz çeviri türü</span><span class="sxs-lookup"><span data-stu-id="b4e1c-213">NX_NAT_ENTRY_TYPE_ERROR (0xD0C) Invalid translation type</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b4e1c-214">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b4e1c-214">Allowed From</span></span>

<span data-ttu-id="b4e1c-215">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="b4e1c-215">Application code</span></span>

### <a name="example"></a><span data-ttu-id="b4e1c-216">Örnek</span><span class="sxs-lookup"><span data-stu-id="b4e1c-216">Example</span></span>

```C
/* Delete the specified static entry from the translation table. */
status = nx_nat_inbound_entry_delete(nat_ptr, delete_entry_ptr);

/* If status = NX_SUCCESS the entry was successfully deleted. */
```
