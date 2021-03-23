---
title: Bölüm 4-LWM2M ISTEMCI hizmetlerinin açıklaması
description: Bu bölüm, tüm LWM2M Istemci hizmetlerinin alfabetik sırada bir açıklamasını içerir.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 825a215ba756b39b6d76e6cc773c288e8b8aab01
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825930"
---
# <a name="chapter-4--description-of-lwm2m-client-services"></a><span data-ttu-id="10326-103">Bölüm 4 LWM2M ISTEMCI hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="10326-103">Chapter 4  Description of LWM2M CLIENT Services</span></span>

<span data-ttu-id="10326-104">Bu bölüm, aşağıda listelenen tüm LWM2M Istemci hizmetlerinin alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="10326-104">This chapter contains a description of all LWM2M Client services listed below in alphabetic order.</span></span>

<span data-ttu-id="10326-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan  **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="10326-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the  **NX_DISABLE_ERROR_CHECKING** define that is used to disable API  error checking, while non-bold values are completely disabled.</span></span>

<span data-ttu-id="10326-106">**LWM2M Istemci yönetimi:**</span><span class="sxs-lookup"><span data-stu-id="10326-106">**LWM2M Client Management:**</span></span>

- <span data-ttu-id="10326-107">nx_lwm2m_client_create: *Lwm2m Istemcisi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="10326-107">nx_lwm2m_client_create: *Create LWM2M Client*</span></span>

- <span data-ttu-id="10326-108">nx_lwm2m_client_delete: *Lwm2m Istemcisini Sil*</span><span class="sxs-lookup"><span data-stu-id="10326-108">nx_lwm2m_client_delete: *Delete LWM2M Client*</span></span>

- <span data-ttu-id="10326-109">nx_lwm2m_client_lock: *Lwm2m Istemcisini kilitle*</span><span class="sxs-lookup"><span data-stu-id="10326-109">nx_lwm2m_client_lock: *Lock LWM2M Client*</span></span>

- <span data-ttu-id="10326-110">nx_lwm2m_client_unlock: *Lwm2m Istemcisinin kilidini aç*</span><span class="sxs-lookup"><span data-stu-id="10326-110">nx_lwm2m_client_unlock: *Unlock LWM2M Client*</span></span>

<span data-ttu-id="10326-111">**LWM2M Istemci oturumu yönetimi:**</span><span class="sxs-lookup"><span data-stu-id="10326-111">**LWM2M Client Session Management:**</span></span>

- <span data-ttu-id="10326-112">nx_lwm2m_client_session_create: *Lwm2m Istemci oturumu oluştur*</span><span class="sxs-lookup"><span data-stu-id="10326-112">nx_lwm2m_client_session_create: *Create LWM2M Client Session*</span></span>

- <span data-ttu-id="10326-113">nx_lwm2m_client_session_delete: *Lwm2m Istemci oturumunu Sil*</span><span class="sxs-lookup"><span data-stu-id="10326-113">nx_lwm2m_client_session_delete: *Delete LWM2M Client Session*</span></span>

- <span data-ttu-id="10326-114">nx_lwm2m_client_session_bootstrap: *bir önyükleme sunucusu ile oturum başlatma*</span><span class="sxs-lookup"><span data-stu-id="10326-114">nx_lwm2m_client_session_bootstrap: *Start a session with a Bootstrap Server*</span></span>

- <span data-ttu-id="10326-115">nx_lwm2m_client_session_bootstrap_dtls: *bir önyükleme sunucusu ile güvenli bir oturum başlatma*</span><span class="sxs-lookup"><span data-stu-id="10326-115">nx_lwm2m_client_session_bootstrap_dtls: *Start a secure session with a Bootstrap Server*</span></span>

- <span data-ttu-id="10326-116">nx_lwm2m_client_session_register_info_get: *Lwm2m Server kayıt bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="10326-116">nx_lwm2m_client_session_register_info_get: *Get LWM2M Server register info*</span></span>

- <span data-ttu-id="10326-117">nx_lwm2m_client_session_register: *Lwm2m sunucusu ile oturum başlatma*</span><span class="sxs-lookup"><span data-stu-id="10326-117">nx_lwm2m_client_session_register: *Start a session with a LWM2M Server*</span></span>

- <span data-ttu-id="10326-118">nx_lwm2m_client_session_register_dtls: *Lwm2m sunucusu ile güvenli bir oturum başlatma*</span><span class="sxs-lookup"><span data-stu-id="10326-118">nx_lwm2m_client_session_register_dtls: *Start a secure session with a LWM2M Server*</span></span>

- <span data-ttu-id="10326-119">nx_lwm2m_client_session_update: *bir oturumu Lwm2m sunucusuyla güncelleştirme*</span><span class="sxs-lookup"><span data-stu-id="10326-119">nx_lwm2m_client_session_update: *Update a session with a LWM2M Server*</span></span>

- <span data-ttu-id="10326-120">nx_lwm2m_client_session_deregister: bir *oturumu Lwm2m sunucusu Ile sonlandırma*</span><span class="sxs-lookup"><span data-stu-id="10326-120">nx_lwm2m_client_session_deregister: *Terminate a session with a LWM2M Server*</span></span>

- <span data-ttu-id="10326-121">nx_lwm2m_client_session_error_get: *bir oturumun son hatasını al*</span><span class="sxs-lookup"><span data-stu-id="10326-121">nx_lwm2m_client_session_error_get: *Get last error of a session*</span></span>

<span data-ttu-id="10326-122">**Cihaz nesnesi uygulama:**</span><span class="sxs-lookup"><span data-stu-id="10326-122">**Device Object Implementation:**</span></span>

- <span data-ttu-id="10326-123">nx_lwm2m_client_device_callbacks_set: *cihaz nesnesi uygulama geri çağırmaları ayarla*</span><span class="sxs-lookup"><span data-stu-id="10326-123">nx_lwm2m_client_device_callbacks_set: *Set Device Object application callbacks*</span></span>

- <span data-ttu-id="10326-124">nx_lwm2m_client_device_error_push: *cihaz nesnesine hata kodu ekleyin*</span><span class="sxs-lookup"><span data-stu-id="10326-124">nx_lwm2m_client_device_error_push: *Add error code to Device Object*</span></span>

- <span data-ttu-id="10326-125">nx_lwm2m_client_device_error_reset: *cihaz nesnesinin hata kodlarını sıfırlayın*</span><span class="sxs-lookup"><span data-stu-id="10326-125">nx_lwm2m_client_device_error_reset: *Reset error codes of Device Object*</span></span>

- <span data-ttu-id="10326-126">nx_lwm2m_client_device_resource_changed: *cihaz nesne kaynağının sinyal değişikliği*</span><span class="sxs-lookup"><span data-stu-id="10326-126">nx_lwm2m_client_device_resource_changed: *Signal change of Device Object resource*</span></span>

<span data-ttu-id="10326-127">**Üretici yazılımı güncelleştirme nesne uygulama:**</span><span class="sxs-lookup"><span data-stu-id="10326-127">**Firmware Update Object Implementation:**</span></span>

- <span data-ttu-id="10326-128">nx_lwm2m_firmware_create: *bellenim güncelleştirme nesnesi oluştur*</span><span class="sxs-lookup"><span data-stu-id="10326-128">nx_lwm2m_firmware_create: *Create Firmware Update Object*</span></span>

- <span data-ttu-id="10326-129">nx_lwm2m_firmware_package_info_set: *bellenim güncelleştirme paketi bilgilerini ayarla*</span><span class="sxs-lookup"><span data-stu-id="10326-129">nx_lwm2m_firmware_package_info_set: *Set Firmware Update Package Information*</span></span>

- <span data-ttu-id="10326-130">nx_lwm2m_firmware_result_set: *bellenim güncelleştirme sonucunu ayarla*</span><span class="sxs-lookup"><span data-stu-id="10326-130">nx_lwm2m_firmware_result_set: *Set Firmware Update Result*</span></span>

- <span data-ttu-id="10326-131">nx_lwm2m_firmware_state_set: *bellenim güncelleştirme durumunu ayarla*</span><span class="sxs-lookup"><span data-stu-id="10326-131">nx_lwm2m_firmware_state_set: *Set Firmware Update State*</span></span>

<span data-ttu-id="10326-132">**Özel nesne uygulamaları:**</span><span class="sxs-lookup"><span data-stu-id="10326-132">**Custom Objects Implementation:**</span></span>

- <span data-ttu-id="10326-133">nx_lwm2m_client_object_add: *Lwm2m Istemcisine nesne uygulamasını ekleme*</span><span class="sxs-lookup"><span data-stu-id="10326-133">nx_lwm2m_client_object_add: *Add Object implementation to LWM2M Client*</span></span>

- <span data-ttu-id="10326-134">nx_lwm2m_client_object_remove: *Lwm2m Istemcisinden nesne uygulamasını kaldırma*</span><span class="sxs-lookup"><span data-stu-id="10326-134">nx_lwm2m_client_object_remove: *Remove Object implementation from LWM2M Client*</span></span>

- <span data-ttu-id="10326-135">nx_lwm2m_client_object_instance_add: *Lwm2m Istemcisine nesne örneği ekleme*</span><span class="sxs-lookup"><span data-stu-id="10326-135">nx_lwm2m_client_object_instance_add: *Add Object Instance to LWM2M Client*</span></span>

- <span data-ttu-id="10326-136">nx_lwm2m_client_object_instance_remove: *nesne ÖRNEĞINI Lwm2m Istemcisinden kaldır*</span><span class="sxs-lookup"><span data-stu-id="10326-136">nx_lwm2m_client_object_instance_remove: *Remove Object Instance from LWM2M Client*</span></span>

- <span data-ttu-id="10326-137">nx_lwm2m_object_resource_changed: bir *nesne örneğinin kaynak değeri Için sinyal değişikliği*</span><span class="sxs-lookup"><span data-stu-id="10326-137">nx_lwm2m_object_resource_changed: *Signal change of a resource value of an Object Instance*</span></span>

<span data-ttu-id="10326-138">**Yerel cihaz yönetimi**</span><span class="sxs-lookup"><span data-stu-id="10326-138">**Local Device Management**</span></span>

- <span data-ttu-id="10326-139">nx_lwm2m_client_object_create: *Yeni bir nesne örneği oluştur*</span><span class="sxs-lookup"><span data-stu-id="10326-139">nx_lwm2m_client_object_create: *Create a new Object Instance*</span></span>

- <span data-ttu-id="10326-140">nx_lwm2m_client_object_delete: *bir nesne örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="10326-140">nx_lwm2m_client_object_delete: *Delete an Object Instance*</span></span>

- <span data-ttu-id="10326-141">nx_lwm2m_client_object_discover: *bir nesne örneğinin kaynaklarını bulma*</span><span class="sxs-lookup"><span data-stu-id="10326-141">nx_lwm2m_client_object_discover: *Discover resources of an Object Instance*</span></span>

- <span data-ttu-id="10326-142">nx_lwm2m_client_object_execute: *bir nesne örneğinin kaynağını yürütün*</span><span class="sxs-lookup"><span data-stu-id="10326-142">nx_lwm2m_client_object_execute: *Execute resource of an Object Instance*</span></span>

- <span data-ttu-id="10326-143">nx_lwm2m_client_object_next_get: *Lwm2m istemcisi tarafından uygulanan nesne listesini al*</span><span class="sxs-lookup"><span data-stu-id="10326-143">nx_lwm2m_client_object_next_get: *Get the list of Objects implemented by the LWM2M Client*</span></span>

- <span data-ttu-id="10326-144">nx_lwm2m_client_object_instance_next_get: *bir nesnenin örneklerinin listesini al*</span><span class="sxs-lookup"><span data-stu-id="10326-144">nx_lwm2m_client_object_instance_next_get: *Get the list of Instances of an Object*</span></span>

- <span data-ttu-id="10326-145">nx_lwm2m_client_object_read: *bir nesne örneğinin kaynak değerlerini oku*</span><span class="sxs-lookup"><span data-stu-id="10326-145">nx_lwm2m_client_object_read: *Read resources values of an Object Instance*</span></span>

- <span data-ttu-id="10326-146">nx_lwm2m_client_object_write: *bir nesne örneğinin kaynak değerlerini değiştirme*</span><span class="sxs-lookup"><span data-stu-id="10326-146">nx_lwm2m_client_object_write: *Change resources values of an Object instance*</span></span>

<span data-ttu-id="10326-147">**Kaynak bilgileri ve değerler ayarı:**</span><span class="sxs-lookup"><span data-stu-id="10326-147">**Resources Info and Values Setting:**</span></span>

- <span data-ttu-id="10326-148">nx_lwm2m_client_resource_info_set: *kaynak bilgilerini ayarlama*</span><span class="sxs-lookup"><span data-stu-id="10326-148">nx_lwm2m_client_resource_info_set: *Set the resource info*</span></span>

- <span data-ttu-id="10326-149">nx_lwm2m_client_resource_string_set: *kaynak değerini dize olarak ayarla*</span><span class="sxs-lookup"><span data-stu-id="10326-149">nx_lwm2m_client_resource_string_set: *Set the resource value as string*</span></span>

- <span data-ttu-id="10326-150">nx_lwm2m_client_resource_integer32_set: *kaynak değerini 32-bit tamsayı olarak ayarlayın*</span><span class="sxs-lookup"><span data-stu-id="10326-150">nx_lwm2m_client_resource_integer32_set: *Set the resource value as 32-Bit integer*</span></span>

- <span data-ttu-id="10326-151">nx_lwm2m_client_resource_integer64_set: *kaynak değerini 64-bit tamsayı olarak ayarlayın*</span><span class="sxs-lookup"><span data-stu-id="10326-151">nx_lwm2m_client_resource_integer64_set: *Set the resource value as 64-Bit integer*</span></span>

- <span data-ttu-id="10326-152">nx_lwm2m_client_resource_float32_set: *kaynak değerini 32-bit float olarak ayarlayın*</span><span class="sxs-lookup"><span data-stu-id="10326-152">nx_lwm2m_client_resource_float32_set: *Set the resource value as 32-Bit float*</span></span>

- <span data-ttu-id="10326-153">nx_lwm2m_client_resource_float64_set: *kaynak değerini 64-bit float olarak ayarlayın*</span><span class="sxs-lookup"><span data-stu-id="10326-153">nx_lwm2m_client_resource_float64_set: *Set the resource value as 64-Bit float*</span></span>

- <span data-ttu-id="10326-154">nx_lwm2m_client_resource_boolean_set: *kaynak değerini Boole olarak ayarlayın*</span><span class="sxs-lookup"><span data-stu-id="10326-154">nx_lwm2m_client_resource_boolean_set: *Set the resource value as boolean*</span></span>

- <span data-ttu-id="10326-155">nx_lwm2m_client_resource_objlnk_set: *kaynak değerini nesne bağlantısı olarak ayarla*</span><span class="sxs-lookup"><span data-stu-id="10326-155">nx_lwm2m_client_resource_objlnk_set: *Set the resource value as object link*</span></span>

- <span data-ttu-id="10326-156">nx_lwm2m_client_resource_opaque_set: *kaynak değerini donuk olarak ayarlayın*</span><span class="sxs-lookup"><span data-stu-id="10326-156">nx_lwm2m_client_resource_opaque_set: *Set the resource value as opaque*</span></span>

- <span data-ttu-id="10326-157">nx_lwm2m_client_resource_instance_set: *birden çok kaynak için kaynak değerini örnek olarak ayarla*</span><span class="sxs-lookup"><span data-stu-id="10326-157">nx_lwm2m_client_resource_instance_set: *Set the resource value as instance for multiple resource*</span></span>
-
- <span data-ttu-id="10326-158">nx_lwm2m_client_resource_dim_set: *birden çok kaynak için kaynak boyutunu ayarlayın.*</span><span class="sxs-lookup"><span data-stu-id="10326-158">nx_lwm2m_client_resource_dim_set: *Set the resource dimension for multiple resource.*</span></span>

<span data-ttu-id="10326-159">**Kaynak bilgileri ve değerleri alma:**</span><span class="sxs-lookup"><span data-stu-id="10326-159">**Resources Info and Values Getting:**</span></span>

- <span data-ttu-id="10326-160">nx_lwm2m_client_resource_info_get: *kaynak bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="10326-160">nx_lwm2m_client_resource_info_get: *Get the resource info*</span></span>

- <span data-ttu-id="10326-161">nx_lwm2m_client_resource_string_get: *bir dize kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="10326-161">nx_lwm2m_client_resource_string_get: *Get the value of a string resource*</span></span>

- <span data-ttu-id="10326-162">nx_lwm2m_client_resource_integer32_get: *32 bitlik bir tamsayı kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="10326-162">nx_lwm2m_client_resource_integer32_get: *Get the value of a 32-Bit integer resource*</span></span>

- <span data-ttu-id="10326-163">nx_lwm2m_client_resource_integer64_get: *64 bitlik bir tamsayı kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="10326-163">nx_lwm2m_client_resource_integer64_get: *Get the value of a 64-Bit integer resource*</span></span>

- <span data-ttu-id="10326-164">nx_lwm2m_client_resource_float32_get: *32 bitlik bir kayan kaynağın değerini alın*</span><span class="sxs-lookup"><span data-stu-id="10326-164">nx_lwm2m_client_resource_float32_get: *Get the value of a 32-Bit float resource*</span></span>

- <span data-ttu-id="10326-165">nx_lwm2m_client_resource_float64_get: *64 bitlik bir kayan kaynağın değerini alın*</span><span class="sxs-lookup"><span data-stu-id="10326-165">nx_lwm2m_client_resource_float64_get: *Get the value of a 64-Bit float resource*</span></span>

- <span data-ttu-id="10326-166">nx_lwm2m_client_resource_boolean_get: *bir Boole kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="10326-166">nx_lwm2m_client_resource_boolean_get: *Get the value of a boolean resource*</span></span>

- <span data-ttu-id="10326-167">nx_lwm2m_client_resource_objlnk_get: *nesne bağlantı kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="10326-167">nx_lwm2m_client_resource_objlnk_get: *Get the value of an object link resource*</span></span>

- <span data-ttu-id="10326-168">nx_lwm2m_client_resource_opaque_get: *donuk bir kaynağın değerini Al*</span><span class="sxs-lookup"><span data-stu-id="10326-168">nx_lwm2m_client_resource_opaque_get: *Get the value of an opaque resource*</span></span>

- <span data-ttu-id="10326-169">nx_lwm2m_client_resource_instance_get: *birden çok kaynak için kaynak örneğini al*</span><span class="sxs-lookup"><span data-stu-id="10326-169">nx_lwm2m_client_resource_instance_get: *Get the resource instance for multiple resource*</span></span>

- <span data-ttu-id="10326-170">nx_lwm2m_client_resource_dim_get: *birden çok kaynak için kaynak boyutunu alın.*</span><span class="sxs-lookup"><span data-stu-id="10326-170">nx_lwm2m_client_resource_dim_get: *Get the resource dimension for multiple resource.*</span></span>

## <a name="nx_lwm2m_client_create"></a><span data-ttu-id="10326-171">nx_lwm2m_client_create</span><span class="sxs-lookup"><span data-stu-id="10326-171">nx_lwm2m_client_create</span></span>

<span data-ttu-id="10326-172">Bir LWM2M istemcisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="10326-172">Creates a LWM2M client.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-173">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-173">Prototype</span></span>

```C
UINT nx_lwm2m_client_create(
    NX_LWM2M_CLIENT client_ptr,
    NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    const CHAR *name_ptr,
    UINT name_length,
    const CHAR *msisdn_ptr,
    UINT msisdn_length,
    UCHAR binding_modes,
    VOID *stack_ptr,
    ULONG stack_size,
    UINT priority);
```

### <a name="description"></a><span data-ttu-id="10326-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-174">Description</span></span>

<span data-ttu-id="10326-175">Bu hizmet kendi ThreadX iş parçacığı bağlamında çalışan bir LWM2M Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="10326-175">This service creates a LWM2M Client instance, which runs in the context of its own ThreadX thread.</span></span>

<span data-ttu-id="10326-176">LWM2M Istemcisi şu OMA LWM2M nesnelerini uygular: güvenlik (0), sunucu (1), Access Control (2) ve cihaz (3).</span><span class="sxs-lookup"><span data-stu-id="10326-176">The LWM2M Client implements the following OMA LWM2M Objects: Security (0), Server (1), Access Control (2) and Device (3).</span></span> <span data-ttu-id="10326-177">Diğer nesneler uygulamaları, uygulama tarafından eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="10326-177">The other objects implementations must be added by the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-178">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-178">Parameters</span></span>

- <span data-ttu-id="10326-179">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-179">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-180">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-180">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="10326-181">**packet_pool_ptr** Bu LWM2M Istemcisi için varsayılan paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-181">**packet_pool_ptr** Pointer to the default packet pool for this LWM2M Client.</span></span>
- <span data-ttu-id="10326-182">**name_ptr** LWM2M Istemci uç noktası adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-182">**name_ptr** Pointer to LWM2M Client endpoint name.</span></span>
- <span data-ttu-id="10326-183">**name_length** LWM2M Istemci uç noktası adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="10326-183">**name_length** Length of LWM2M Client endpoint name.</span></span>
- <span data-ttu-id="10326-184">**msisdn_ptr** SMS bağlaması ile kullanım için LWM2M Istemcisine ulaşılabileceği MSıSDN işaretçisine, SMS bağlama desteklenmiyorsa NULL olabilir.</span><span class="sxs-lookup"><span data-stu-id="10326-184">**msisdn_ptr** Pointer to the MSISDN where the LWM2M Client can be reached for use with the SMS binding, can be NULL if SMS binding is not supported.</span></span>
- <span data-ttu-id="10326-185">**msisdn_length** MSıSDN numarası uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="10326-185">**msisdn_length** Length of MSISDN number.</span></span>
- <span data-ttu-id="10326-186">**binding_modes** LWM2M Istemcisi tarafından desteklenen bağlama ve modlar, NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S ve NX_LWM2M_BINDING_SQ bayraklarının bir birleşimi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-186">**binding_modes** The binding and modes supported by the LWM2M Client, must be a combination of NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S and NX_LWM2M_BINDING_SQ flags.</span></span>
- <span data-ttu-id="10326-187">**stack_ptr** LWM2M Istemci iş parçacığı yığın alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-187">**stack_ptr** Pointer to LWM2M Client thread stack area.</span></span>
- <span data-ttu-id="10326-188">**stack_size** LWM2M Istemci iş parçacığı yığın boyutu.</span><span class="sxs-lookup"><span data-stu-id="10326-188">**stack_size** The LWM2M Client thread stack size.</span></span>
- <span data-ttu-id="10326-189">**Öncelik** LWM2M Istemcisinin önceliği.</span><span class="sxs-lookup"><span data-stu-id="10326-189">**priority** Priority of LWM2M Client.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-190">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-190">Return Values</span></span>

- <span data-ttu-id="10326-191">**NX_SUCCESS** LWM2M Istemcisi başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="10326-191">**NX_SUCCESS** The LWM2M Client has been successfully created.</span></span>
- <span data-ttu-id="10326-192">**NX_LWM2M_CLIENT_ERROR** LWM2M Istemcisi oluşturma hatası.</span><span class="sxs-lookup"><span data-stu-id="10326-192">**NX_LWM2M_CLIENT_ERROR** LWM2M Client create error.</span></span>
- <span data-ttu-id="10326-193">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="10326-193">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="10326-194">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-194">**NX_PTR_ERROR** Invalid pointer.</span></span>
- <span data-ttu-id="10326-195">**NX_SIZE_ERROR** Geçersiz yığın boyutu.</span><span class="sxs-lookup"><span data-stu-id="10326-195">**NX_SIZE_ERROR** Invalid stack size.</span></span>
- <span data-ttu-id="10326-196">**NX_OPTION_ERROR** Geçersiz öncelik.</span><span class="sxs-lookup"><span data-stu-id="10326-196">**NX_OPTION_ERROR** Invalid priority.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-197">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-197">Allowed From</span></span>

<span data-ttu-id="10326-198">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-198">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-199">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-199">Example</span></span>

```C
/* Create LWM2M Client instance.  */
status = nx_lwm2m_client_create(&lwm2m_client, &ip_0, &pool_0, 
  "netxlwm2mclient", sizeof("netxlwm2mclient") - 1,           
                                NX_NULL, 0, NX_LWM2M_CLIENT_BINDING_U, 
                                stack_ptr, stack_size, priority);

/* If status is NX_SUCCESS a LWM2M Client instance was successfully created.  */
```

## <a name="nx_lwm2m_client_delete"></a><span data-ttu-id="10326-200">nx_lwm2m_client_delete</span><span class="sxs-lookup"><span data-stu-id="10326-200">nx_lwm2m_client_delete</span></span>

<span data-ttu-id="10326-201">Bir LWM2M Istemcisini siler.</span><span class="sxs-lookup"><span data-stu-id="10326-201">Deletes a LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-202">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-202">Prototype</span></span>

```C
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-203">Description</span></span>

<span data-ttu-id="10326-204">Bu hizmet, daha önce oluşturulmuş bir LWM2M Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="10326-204">This service deletes a previously created LWM2M Client instance.</span></span>

<span data-ttu-id="10326-205">O anda istemcinin bağlı olduğu tüm oturumlar bu çağrı tarafından da silinir.</span><span class="sxs-lookup"><span data-stu-id="10326-205">All sessions currently attached the client are also deleted by this call.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-206">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-206">Parameters</span></span>

- <span data-ttu-id="10326-207">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-207">**client_ptr** Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-208">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-208">Return Values</span></span>

- <span data-ttu-id="10326-209">**NX_SUCCESS** LWM2M Istemcisi başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="10326-209">**NX_SUCCESS** The LWM2M Client has been successfully deleted.</span></span>
- <span data-ttu-id="10326-210">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-210">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-211">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-211">Allowed From</span></span>

<span data-ttu-id="10326-212">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-212">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-213">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-213">Example</span></span>

```c
/* Delete the LWM2M Client instance.  */
status = nx_lwm2m_client_create(&lwm2m_client);

/* If status is NX_SUCCESS a LWM2M Client instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_device_callback_set"></a><span data-ttu-id="10326-214">nx_lwm2m_client_device_callback_set</span><span class="sxs-lookup"><span data-stu-id="10326-214">nx_lwm2m_client_device_callback_set</span></span>

<span data-ttu-id="10326-215">Bir cihaz nesnesinin uygulama geri aramasını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-215">Sets a device object's application callback.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-216">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-216">Prototype</span></span>

```C
UINT **nx_lwm2m_client_device_callback_set**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_OPERATION_CALLBACK operation_callback);
```

### <a name="description"></a><span data-ttu-id="10326-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-217">Description</span></span>

<span data-ttu-id="10326-218">Bu hizmet, LWM2M Istemcisi tarafından işlenmeyen LWM2M cihaz nesnesi kaynaklarına işlem uygulamak için uygulama geri aramasını kurar.</span><span class="sxs-lookup"><span data-stu-id="10326-218">This service installs the application callback for implementing operations on the LWM2M Device Object resources that are not handled by the LWM2M Client.</span></span>

<span data-ttu-id="10326-219">LWM2M Istemcisi şu kaynakları uygular: hata kodu (11), sıfırlama hata kodu (12) ve desteklenen bağlama ve modlar (16), diğer kaynaklara yönelik işlemler uygulamaya yeniden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="10326-219">The LWM2M Client implements the following resources: Error Code (11), Reset Error Code (12) and Supported Binding and Modes (16), operations to the other resources are redirected to the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-220">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-220">Parameters</span></span>

- <span data-ttu-id="10326-221">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-221">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-222">**operation_callback** "Oku", "Keşfet", "Write" ve "Execute" için işlem geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="10326-222">**operation_callback** The operation callback for “Read”, “Discover”, “Write” and “Execute”.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-223">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-223">Return Values</span></span>

- <span data-ttu-id="10326-224">**NX_SUCCESS** İşlem geri çağırması başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="10326-224">**NX_SUCCESS** The operation callback has been successfully set.</span></span>
- <span data-ttu-id="10326-225">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-225">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-226">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-226">Allowed From</span></span>

<span data-ttu-id="10326-227">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-227">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-228">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-228">Example</span></span>

```c
/* Set device callback.  */
status = nx_lwm2m_client_device_callback_set(&lwm2m_client, device_operation);

/* If status is NX_SUCCESS a device callback was successfully set.  */
```

## <a name="nx_lwm2m_client_device_error_push"></a><span data-ttu-id="10326-229">nx_lwm2m_client_device_error_push</span><span class="sxs-lookup"><span data-stu-id="10326-229">nx_lwm2m_client_device_error_push</span></span>
<span data-ttu-id="10326-230">Bir cihaz nesnesine bir hata kodu ekler.</span><span class="sxs-lookup"><span data-stu-id="10326-230">Adds an error code to a device object.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-231">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-231">Prototype</span></span>

```C
UINT **nx_lwm2m_client_device_error_push**(
    NX_LWM2M_CLIENT *client_ptr,
    UCHAR code);
```

### <a name="description"></a><span data-ttu-id="10326-232">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-232">Description</span></span>

<span data-ttu-id="10326-233">Bu hizmet, nesne cihazının hata kodu (11) kaynağına yeni bir örnek ekler.</span><span class="sxs-lookup"><span data-stu-id="10326-233">This service adds a new instance to the Error Code (11) resource of the Object Device.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-234">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-234">Parameters</span></span>

- <span data-ttu-id="10326-235">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-235">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-236">**kod** Yeni hata kodu.</span><span class="sxs-lookup"><span data-stu-id="10326-236">**code** The new error code.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-237">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-237">Return Values</span></span>

- <span data-ttu-id="10326-238">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-238">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-239">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL**</span><span class="sxs-lookup"><span data-stu-id="10326-239">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL**</span></span>

<span data-ttu-id="10326-240">En fazla depolanan hata kodu sayısı</span><span class="sxs-lookup"><span data-stu-id="10326-240">The maximum number of stored error codes has</span></span>

<span data-ttu-id="10326-241">ulaşıldı.</span><span class="sxs-lookup"><span data-stu-id="10326-241">been reached.</span></span>

<span data-ttu-id="10326-242">Geçersiz NX_PTR_ERROR işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-242">NX_PTR_ERROR Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-243">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-243">Allowed From</span></span>

<span data-ttu-id="10326-244">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-244">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-245">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-245">Example</span></span>

```C
/* Push device error 1 (Low battery power) to server.  */
status = nx_lwm2m_client_device_error_push(&lwm2m_client, 1);

/* If status is NX_SUCCESS a device error was successfully pushed.  */
```

## <a name="nx_lwm2m_client_device_error_reset"></a><span data-ttu-id="10326-246">nx_lwm2m_client_device_error_reset</span><span class="sxs-lookup"><span data-stu-id="10326-246">nx_lwm2m_client_device_error_reset</span></span>

<span data-ttu-id="10326-247">Cihaz nesnesinin hata kodlarını sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="10326-247">Resets the error codes of Device Object.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-248">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-248">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-249">Description</span></span>

<span data-ttu-id="10326-250">Bu hizmet, tüm hata kodu kaynak örneklerini cihaz nesnesinden siler.</span><span class="sxs-lookup"><span data-stu-id="10326-250">This service deletes all error code resource instances from the Device Object.</span></span> <span data-ttu-id="10326-251">Bu, kaynak sıfırlama hata kodunu (12) çalıştırmaya eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="10326-251">This is equivalent to executing the resource Reset Error Code (12).</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-252">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-252">Parameters</span></span>

- <span data-ttu-id="10326-253">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-253">**client_ptr** Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-254">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-254">Return Values</span></span>

- <span data-ttu-id="10326-255">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-255">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-256">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-256">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-257">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-257">Allowed From</span></span>

<span data-ttu-id="10326-258">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-258">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-259">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-259">Example</span></span>

```c
/* Delete all device error code.  */
status = nx_lwm2m_client_device_error_reset(&lwm2m_client);

/* If status is NX_SUCCESS, reset device error successfully.  */
```

## <a name="nx_lwm2m_client_device_resource_changed"></a><span data-ttu-id="10326-260">nx_lwm2m_client_device_resource_changed</span><span class="sxs-lookup"><span data-stu-id="10326-260">nx_lwm2m_client_device_resource_changed</span></span>

<span data-ttu-id="10326-261">Bir cihaz nesne kaynağında değişikliğe işaret eder.</span><span class="sxs-lookup"><span data-stu-id="10326-261">Signals a change to a Device Object resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-262">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-262">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_resource_changed(
    NX_LWM2M_CLIENT *client_ptr, 
    const NX_LWM2M_RESOURCE *resource);

```

### <a name="description"></a><span data-ttu-id="10326-263">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-263">Description</span></span>

<span data-ttu-id="10326-264">Hizmet, uygulama tarafından, nesne cihazının bir kaynağının değiştiği LWM2M Istemcisine işaret etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10326-264">The service is used by the application to signal to the LWM2M Client that a resource of the Object Device has changed.</span></span> <span data-ttu-id="10326-265">LWM2M Istemcisi, kaynak bir LWM2M sunucusu tarafından gözlemleniyorsa bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="10326-265">The LWM2M Client will send a notification if the resource is observed by a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-266">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-266">Parameters</span></span>

- <span data-ttu-id="10326-267">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-267">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-268">**kaynak** Değiştirilen kaynağı açıklayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-268">**resource** Pointer to the structure describing the resource that has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-269">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-269">Return Values</span></span>

- <span data-ttu-id="10326-270">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-270">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-271">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-271">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-272">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-272">Allowed From</span></span>

<span data-ttu-id="10326-273">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-273">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-274">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-274">Example</span></span>

```c
/* Change device resource.  */
status = nx_lwm2m_client_device_resource_changed(&lwm2m_client, &resource);

/* If status is NX_SUCCESS, a device resource was successfully changed.  */
```

##  <a name="nx_lwm2m_client_firmware_create"></a><span data-ttu-id="10326-275">nx_lwm2m_client_firmware_create</span><span class="sxs-lookup"><span data-stu-id="10326-275">nx_lwm2m_client_firmware_create</span></span>

<span data-ttu-id="10326-276">LWM2M Istemci üretici yazılımı nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="10326-276">Create a LWM2M Client Firmware Object.</span></span> 

### <a name="prototype"></a><span data-ttu-id="10326-277">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-277">Prototype</span></span>

```c
UINT nx_lwm2m_client_firmware_create(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    NX_LWM2M_CLIENT *client_ptr, 
    UINT protocols,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_CLIENT_FIRMWARE_PACKAGE_URI_CALLBACK update_callback);
```

### <a name="description"></a><span data-ttu-id="10326-278">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-278">Description</span></span>

<span data-ttu-id="10326-279">Hizmet, uygulama tarafından bellenim nesnesi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10326-279">The service is used by the application to create firmware object.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-280">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-280">Parameters</span></span>

- <span data-ttu-id="10326-281">**firmware_ptr** LWM2M Istemci üretici yazılımı nesnesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-281">**firmware_ptr** Pointer to LWM2M Client Firmware object.</span></span>
- <span data-ttu-id="10326-282">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-282">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-283">**protokoller** Desteklenen protokoller.</span><span class="sxs-lookup"><span data-stu-id="10326-283">**protocols** The supported protocols.</span></span>
- <span data-ttu-id="10326-284">**package_callback** Paket geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="10326-284">**package_callback** The package callback.</span></span>
- <span data-ttu-id="10326-285">**package_uri_callback** Paket URI geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="10326-285">**package_uri_callback** The package URI callback.</span></span>
- <span data-ttu-id="10326-286">**update_callback** Güncelleştirme geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="10326-286">**update_callback** The update callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-287">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-287">Return Values</span></span>

<span data-ttu-id="10326-288">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-288">**NX_SUCCESS** Successful operation.</span></span>
<span data-ttu-id="10326-289">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-289">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-290">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-290">Allowed From</span></span>

<span data-ttu-id="10326-291">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-291">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-292">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-292">Example</span></span>

```c
/* Create firmware object.  */
status = nx_lwm2m_client_firmware_create(&firmware, &lwm2m_client,     
                                         NX_LWM2M_CLIENT_FIRMWARE_PROTOCOL_HTTP, 
                                         NX_NULL, firmware_packet_uri,
                                         firmware_update);

/* If status is NX_SUCCESS, firmware object was successfully created.  */
```

##  <a name="nx_lwm2m_client_firmware_package_info_set"></a><span data-ttu-id="10326-293">nx_lwm2m_client_firmware_package_info_set</span><span class="sxs-lookup"><span data-stu-id="10326-293">nx_lwm2m_client_firmware_package_info_set</span></span>

<span data-ttu-id="10326-294">LWM2M Istemci üretici yazılımı paket bilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-294">Sets the LWM2M Client Firmware package information.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-295">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-295">Prototype</span></span>

```c
UINT nx_lwm2m_client_firmware_package_info_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    const CHAR *name, 
    UINT name_length, 
    const CHAR *version, 
    UINT version_length);
```

### <a name="description"></a><span data-ttu-id="10326-296">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-296">Description</span></span>

<span data-ttu-id="10326-297">Hizmet, uygulama tarafından bellenim güncelleştirme nesnesinin paket bilgi kaynaklarını ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10326-297">The service is used by the application to set the package information resources of the firmware update object.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-298">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-298">Parameters</span></span>

- <span data-ttu-id="10326-299">**firmware_ptr** LWM2M Istemci üretici yazılımı nesnesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-299">**firmware_ptr** Pointer to LWM2M Client Firmware object.</span></span>
- <span data-ttu-id="10326-300">**ad** Üretici yazılımı paketinin adı.</span><span class="sxs-lookup"><span data-stu-id="10326-300">**name** The name of firmware package.</span></span>
- <span data-ttu-id="10326-301">**name_length** Ad uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="10326-301">**name_length** The length of name.</span></span>
- <span data-ttu-id="10326-302">**sürümü** Üretici yazılımı paketinin sürümü.</span><span class="sxs-lookup"><span data-stu-id="10326-302">**version** The version of firmware package.</span></span>
- <span data-ttu-id="10326-303">**version_length** Sürüm uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="10326-303">**version_length** The length of version.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-304">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-304">Return Values</span></span>

- <span data-ttu-id="10326-305">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-305">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-306">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-306">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-307">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-307">Allowed From</span></span>

<span data-ttu-id="10326-308">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-308">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-309">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-309">Example</span></span>

```c
/* Set the package information resources of the firmware object.  */
status = nx_lwm2m_client_firmware_package_info_set(&firmware, 2m_client,     
                                    “LWM2M Firmware”, sizeof(“LWM2M Firmware”) -1,
                                    “1.0.0.0”, sizeof(“1.0.0.0”) - 1);

/* If status is NX_SUCCESS, package information resources was successfully set. */
```

##  <a name="nx_lwm2m_client_firmware_result_set"></a><span data-ttu-id="10326-310">nx_lwm2m_client_firmware_result_set</span><span class="sxs-lookup"><span data-stu-id="10326-310">nx_lwm2m_client_firmware_result_set</span></span>

<span data-ttu-id="10326-311">Bellenim güncelleştirme nesnesinin güncelleştirme sonucu kaynağını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-311">Sets the update result resource of the firmware update object.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-312">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-312">Prototype</span></span>

```c
UINT nx_lwm2m_client_firmware_result_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a><span data-ttu-id="10326-313">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-313">Description</span></span>

<span data-ttu-id="10326-314">Hizmet, uygulama tarafından bellenim güncelleştirme nesnesinin güncelleştirme sonucu kaynağını ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10326-314">The service is used by the application to set the update result resource of the firmware update object.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-315">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-315">Parameters</span></span>

- <span data-ttu-id="10326-316">**firmware_ptr** LWM2M Istemci üretici yazılımı nesnesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-316">**firmware_ptr** Pointer to LWM2M Client Firmware object.</span></span>
- <span data-ttu-id="10326-317">**sonuç** Güncelleştirme sonucu.</span><span class="sxs-lookup"><span data-stu-id="10326-317">**result** The update result.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-318">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-318">Return Values</span></span>

- <span data-ttu-id="10326-319">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-319">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-320">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-320">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-321">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-321">Allowed From</span></span>

<span data-ttu-id="10326-322">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-322">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-323">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-323">Example</span></span>

```c
/* Set the update result resource of the firmware object.  */
status = nx_lwm2m_client_firmware_result_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_RESULT_SUCCESS);

/* If status is NX_SUCCESS, the update result resource was successfully set.  */
```

##  <a name="nx_lwm2m_client_firmware_state_set"></a><span data-ttu-id="10326-324">nx_lwm2m_client_firmware_state_set</span><span class="sxs-lookup"><span data-stu-id="10326-324">nx_lwm2m_client_firmware_state_set</span></span>

<span data-ttu-id="10326-325">Bellenim güncelleştirme nesnesinin güncelleştirme sonucu kaynağını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-325">Sets the update result resource of the firmware update object.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-326">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-326">Prototype</span></span>

```c
UINT nx_lwm2m_client_firmware_state_set(
    NX_LWM2M_CLIENT_FIRMWARE *firmware_ptr, 
    UCHAR result);
```

### <a name="description"></a><span data-ttu-id="10326-327">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-327">Description</span></span>

<span data-ttu-id="10326-328">Hizmet, uygulama tarafından bellenim güncelleştirme nesnesinin durumunu ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10326-328">The service is used by the application to set the state of the firmware update object.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-329">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-329">Parameters</span></span>

- <span data-ttu-id="10326-330">**firmware_ptr** LWM2M Istemci üretici yazılımı nesnesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-330">**firmware_ptr** Pointer to LWM2M Client Firmware object.</span></span>
- <span data-ttu-id="10326-331">**durum** Bellenim nesnesinin durumu.</span><span class="sxs-lookup"><span data-stu-id="10326-331">**state** The state of the firmware object.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-332">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-332">Return Values</span></span>

- <span data-ttu-id="10326-333">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-333">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-334">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-334">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-335">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-335">Allowed From</span></span>

<span data-ttu-id="10326-336">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-336">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-337">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-337">Example</span></span>

```c
/* Set the state of the firmware object.  */
status = nx_lwm2m_client_firmware_state_set(&firmware, 
                                         NX_LWM2M_CLIENT_FIRMWARE_STATE_IDLE);

/* If status is NX_SUCCESS, the state was successfully set.  */
```

## <a name="nx_lwm2m_client_lock"></a><span data-ttu-id="10326-338">nx_lwm2m_client_lock</span><span class="sxs-lookup"><span data-stu-id="10326-338">nx_lwm2m_client_lock</span></span>

<span data-ttu-id="10326-339">LWM2M Istemcisini kilitler.</span><span class="sxs-lookup"><span data-stu-id="10326-339">Locks the LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-340">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-340">Prototype</span></span>

```c
UINT **nx_lwm2m_client_lock**(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-341">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-341">Description</span></span>

<span data-ttu-id="10326-342">Bu hizmet, LWM2M nesnelerine sunuculardan veya başka bir uygulama iş parçacığından eş zamanlı erişimi engellemek için LWM2M Istemcisini kilitler.</span><span class="sxs-lookup"><span data-stu-id="10326-342">This service locks the LWM2M Client to prevent concurrent access to the LWM2M objects from the servers or another application thread.</span></span>

<span data-ttu-id="10326-343">LWM2M Istemcisi Şu anda başka bir iş parçacığı tarafından kilitliyse, LWM2M Istemcisinin kilidi açana kadar işlev engellenir.</span><span class="sxs-lookup"><span data-stu-id="10326-343">If the LWM2M Client is currently locked by another thread, the function will block until the LWM2M Client is unlocked.</span></span>

<span data-ttu-id="10326-344">***Nx_lwm2m_client_lock** _/_ *_nx_lwm2m_client_unlock_** çiftlerine yapılan çağrılar iç içe olabilir.</span><span class="sxs-lookup"><span data-stu-id="10326-344">Calls to \***nx_lwm2m_client_lock**_/_*_nx_lwm2m_client_unlock_*\* pairs can be nested.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-345">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-345">Parameters</span></span>

- <span data-ttu-id="10326-346">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-346">**client_ptr** Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-347">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-347">Return Values</span></span>

- <span data-ttu-id="10326-348">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-348">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-349">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-349">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-350">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-350">Allowed From</span></span>

<span data-ttu-id="10326-351">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-351">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-352">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-352">Example</span></span>

```c
/* Lock the LWM2M client.  */
status = nx_lwm2m_client_lock(&lwm2m_client);

/* If status is NX_SUCCESS, lwm2m client was successfully locked.  */
```

## <a name="nx_lwm2m_client_object_add"></a><span data-ttu-id="10326-353">nx_lwm2m_client_object_add</span><span class="sxs-lookup"><span data-stu-id="10326-353">nx_lwm2m_client_object_add</span></span>

<span data-ttu-id="10326-354">LWM2M Istemcisine bir nesne uygulamasını ekler.</span><span class="sxs-lookup"><span data-stu-id="10326-354">Adds an Object implementation to the LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-355">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-355">Prototype</span></span>

```c
UINT **nx_lwm2m_client_object_add**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_CLIENT_OBJECT_OPERATION_CALLBACK object_operation);
```

### <a name="description"></a><span data-ttu-id="10326-356">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-356">Description</span></span>

<span data-ttu-id="10326-357">Bu hizmet, LWM2M Istemcisine yeni bir nesne uygulamasını ekler.</span><span class="sxs-lookup"><span data-stu-id="10326-357">This service adds a new Object implementation to the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-358">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-358">Parameters</span></span>

- <span data-ttu-id="10326-359">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-359">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-360">**object_ptr** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-360">**object_ptr** Pointer to the structure defining the Object implementation.</span></span>
- <span data-ttu-id="10326-361">**object_id** Nesne kimliği.</span><span class="sxs-lookup"><span data-stu-id="10326-361">**object_id** The object id.</span></span>
- <span data-ttu-id="10326-362">**object_operation** Nesne işlemi geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="10326-362">**object_operation** The object operation callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-363">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-363">Return Values</span></span>

- <span data-ttu-id="10326-364">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-364">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-365">**NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne KIMLIĞI zaten var.</span><span class="sxs-lookup"><span data-stu-id="10326-365">**NX_LWM2M_CLIENT_ALREADY_EXIST** The Object ID already exists.</span></span>
- <span data-ttu-id="10326-366">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-366">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-367">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-367">Allowed From</span></span>

<span data-ttu-id="10326-368">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-368">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-369">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-369">Example</span></span>

```c
/* Add new object to the lwm2m client.  */
status = nx_lwm2m_client_object_add(&lwm2m_client, &object, 
                                    3303, object_operation);

/* If status is NX_SUCCESS, the new object was successfully added.  */
```

## <a name="nx_lwm2m_client_object_create"></a><span data-ttu-id="10326-370">nx_lwm2m_client_object_create</span><span class="sxs-lookup"><span data-stu-id="10326-370">nx_lwm2m_client_object_create</span></span>

<span data-ttu-id="10326-371">Yeni bir nesne örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="10326-371">Creates a new Object Instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-372">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-372">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_create(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID *instance_id_ptr,
    UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-373">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-373">Description</span></span>

<span data-ttu-id="10326-374">Bu hizmet, yeni bir nesne örneği oluşturmak için LWM2M Istemcisinin bir nesnesi üzerinde bir ' Create ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-374">This service performs a ‘Create’ operation on an Object of the LWM2M Client to create a new Object Instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-375">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-375">Parameters</span></span>

- <span data-ttu-id="10326-376">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-376">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-377">**object_id** Nesne KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-377">**object_id** The Object ID.</span></span>
- <span data-ttu-id="10326-378">**instance_id_ptr** LWM2M Istemcisinin bir örnek KIMLIĞI ataması gerekiyorsa, yeni örneğin KIMLIĞINE yönelik işaretçi **null** olabilir.</span><span class="sxs-lookup"><span data-stu-id="10326-378">**instance_id_ptr** Pointer to the ID of the new instance, can be **NULL** if the LWM2M Client must assign an Instance ID.</span></span> <span data-ttu-id="10326-379">KIMLIK ayrılmış 65535 ise, LWM2M Istemcisi bir örnek KIMLIĞI atayacaktır.</span><span class="sxs-lookup"><span data-stu-id="10326-379">If the ID is the reserved value 65535 the LWM2M Client will assign an Instance ID.</span></span> <span data-ttu-id="10326-380">NULL değilse, çağrının ardından atanan KIMLIK döndürülür.</span><span class="sxs-lookup"><span data-stu-id="10326-380">If not NULL the assigned ID is returned after the call.</span></span>
- <span data-ttu-id="10326-381">**num_values** Ayarlanacak değer sayısı.</span><span class="sxs-lookup"><span data-stu-id="10326-381">**num_values** The number of values to set.</span></span>
- <span data-ttu-id="10326-382">**values_ptr** Yeni nesne örneğini başlatmak için kaynak değerleri dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-382">**values_ptr** Pointer to an array of resource values to initialize the new Object Instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-383">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-383">Return Values</span></span>

- <span data-ttu-id="10326-384">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-384">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-385">**NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne örneği KIMLIĞI zaten var.</span><span class="sxs-lookup"><span data-stu-id="10326-385">**NX_LWM2M_CLIENT_ALREADY_EXIST** The Object Instance ID already exists.</span></span>
- <span data-ttu-id="10326-386">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Nesne, örnek oluşturmayı desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="10326-386">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** The Object doesn’t support instance creation.</span></span>
- <span data-ttu-id="10326-387">**NX_LWM2M_CLIENT_NO_MEMORY** Yeni örneği depolamak için bellek ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="10326-387">**NX_LWM2M_CLIENT_NO_MEMORY** Cannot allocate memory to store the new instance.</span></span>
- <span data-ttu-id="10326-388">**NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI yok.</span><span class="sxs-lookup"><span data-stu-id="10326-388">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID doesn’t exist.</span></span>
- <span data-ttu-id="10326-389">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-389">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-390">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-390">Allowed From</span></span>

<span data-ttu-id="10326-391">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-391">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-392">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-392">Example</span></span>

```c
/* Create new object instance.  */
status = nx_lwm2m_client_object_create(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, a new object instance was successfully created.  */
```

## <a name="nx_lwm2m_client_object_delete"></a><span data-ttu-id="10326-393">nx_lwm2m_client_object_delete</span><span class="sxs-lookup"><span data-stu-id="10326-393">nx_lwm2m_client_object_delete</span></span>

<span data-ttu-id="10326-394">Bir nesne örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="10326-394">Deletes an Object Instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-395">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-395">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_delete(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id);
```

### <a name="description"></a><span data-ttu-id="10326-396">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-396">Description</span></span>

<span data-ttu-id="10326-397">Bu hizmet, LWM2M Istemcisinin nesne örneği üzerinde bir ' DELETE ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-397">This service performs a ‘Delete’ operation on an Object Instance of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-398">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-398">Parameters</span></span>

- <span data-ttu-id="10326-399">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-399">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-400">**object_id** Nesne KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-400">**object_id** The Object ID.</span></span>
- <span data-ttu-id="10326-401">**instance_id** Nesne örneği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-401">**instance_id** The Object Instance ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-402">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-402">Return Values</span></span>

- <span data-ttu-id="10326-403">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-403">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-404">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Nesne, örnek silmeyi desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="10326-404">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** The Object doesn’t support instance deletion.</span></span>
- <span data-ttu-id="10326-405">**NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI veya nesne örneği KIMLIĞI yok.</span><span class="sxs-lookup"><span data-stu-id="10326-405">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID or Object Instance ID doesn’t exist.</span></span>
- <span data-ttu-id="10326-406">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-406">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-407">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-407">Allowed From</span></span>

<span data-ttu-id="10326-408">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-408">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-409">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-409">Example</span></span>

```c
/* Delete an object instance.  */
status = nx_lwm2m_client_object_delete(&lwm2m_client, 3303, 0);

/* If status is NX_SUCCESS, an object instance was successfully deleted.  */
```

## <a name="nx_lwm2m_client_object_discover"></a><span data-ttu-id="10326-410">nx_lwm2m_client_object_discover</span><span class="sxs-lookup"><span data-stu-id="10326-410">nx_lwm2m_client_object_discover</span></span>

<span data-ttu-id="10326-411">Bir nesne örneğinin kaynaklarını bulur.</span><span class="sxs-lookup"><span data-stu-id="10326-411">Discovers resources of an Object Instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-412">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-412">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_discover(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT *num_resources,
    NX_LWM2M_CLIENT_RESOURCE *resources);

```

### <a name="description"></a><span data-ttu-id="10326-413">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-413">Description</span></span>

<span data-ttu-id="10326-414">Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde bir ' bul ' işlemi gerçekleştirir, bu, nesne tarafından uygulanan kaynakların listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="10326-414">This service performs a ‘Discover’ operation on an Object Instance of the LWM2M Client, this returns the list of resources implemented by the Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-415">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-415">Parameters</span></span>

- <span data-ttu-id="10326-416">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-416">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-417">**object_id** Nesne KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-417">**object_id** The Object ID.</span></span>
- <span data-ttu-id="10326-418">**instance_id** Nesne örneği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-418">**instance_id** The Object Instance ID.</span></span>
- <span data-ttu-id="10326-419">**num_resources** Hedef arabelleğin boyutunu girişte, arabelleğe yazılan öğelerin sayısı çıktı olarak.</span><span class="sxs-lookup"><span data-stu-id="10326-419">**num_resources** On input the size of the destination buffer, on output the number of elements written to the buffer.</span></span>
- <span data-ttu-id="10326-420">**kaynaklar** Hedef arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-420">**resources** Pointer to the destination buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-421">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-421">Return Values</span></span>

- <span data-ttu-id="10326-422">Başarılı bir işlem *NX_SUCCESS*.</span><span class="sxs-lookup"><span data-stu-id="10326-422">*NX_SUCCESS*\* Successful operation.</span></span>
- <span data-ttu-id="10326-423">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Kaynak ara belleği, kaynak listesini depolamak için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="10326-423">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** The resources buffer is too small to store the list of resources.</span></span>
- <span data-ttu-id="10326-424">**NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI veya nesne örneği KIMLIĞI yok.</span><span class="sxs-lookup"><span data-stu-id="10326-424">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID or Object Instance ID doesn’t exist.</span></span>
- <span data-ttu-id="10326-425">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-425">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-426">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-426">Allowed From</span></span>

<span data-ttu-id="10326-427">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-427">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-428">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-428">Example</span></span>

```c
NX_LWM2M_CLIENT_RESOURCE resources[10]
UINT num_resources = 10;

/* Discover object resources.  */
status = nx_lwm2m_client_object_discover(&lwm2m_client, 3303, 0, 
                                         &num_resources, resource);

/* If status is NX_SUCCESS, discover object resources successfully.  */
```

## <a name="nx_lwm2m_client_object_execute"></a><span data-ttu-id="10326-429">nx_lwm2m_client_object_execute</span><span class="sxs-lookup"><span data-stu-id="10326-429">nx_lwm2m_client_object_execute</span></span>

<span data-ttu-id="10326-430">Bir nesne örneğinin kaynağında ' Execute ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-430">Performs an 'Execute' operation on a resource of an Object Instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-431">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-431">Prototype</span></span>

```C
UINT **nx_lwm2m_client_object_execute**(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr,
    UINT arguments_length);
```

### <a name="description"></a><span data-ttu-id="10326-432">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-432">Description</span></span>

<span data-ttu-id="10326-433">Bu hizmet, LWM2M Istemcisinin nesne örneği kaynağında ' Execute ' işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-433">This service performs the ‘Execute’ operation on an Object Instance Resource of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-434">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-434">Parameters</span></span>

- <span data-ttu-id="10326-435">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-435">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-436">**object_id** Nesne KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-436">**object_id** The Object ID.</span></span>
- <span data-ttu-id="10326-437">**instance_id** Nesne örneği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-437">**instance_id** The Object Instance ID.</span></span>
- <span data-ttu-id="10326-438">**resource_id** Kaynak KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-438">**resource_id** The Resource ID.</span></span>
- <span data-ttu-id="10326-439">**arguments_ptr** Yürütme işleminin bağımsız değişkenlerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-439">**arguments_ptr** Pointer to the arguments of the execute operation.</span></span> <span data-ttu-id="10326-440">Arguments_length sıfırsa NULL olabilir.</span><span class="sxs-lookup"><span data-stu-id="10326-440">Can be NULL if arguments_length is zero.</span></span>
- <span data-ttu-id="10326-441">**arguments_length** Bağımsız değişkenlerin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="10326-441">**arguments_length** The length of the arguments.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-442">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-442">Return Values</span></span>

- <span data-ttu-id="10326-443">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-443">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-444">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Kaynak ara belleği, kaynak listesini depolamak için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="10326-444">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** The resources buffer is too small to store the list of resources.</span></span>
- <span data-ttu-id="10326-445">**NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI veya nesne örneği KIMLIĞI yok.</span><span class="sxs-lookup"><span data-stu-id="10326-445">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID or Object Instance ID doesn’t exist.</span></span>
- <span data-ttu-id="10326-446">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-446">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-447">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-447">Allowed From</span></span>

<span data-ttu-id="10326-448">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-448">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-449">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-449">Example</span></span>

```c
/* Execute object resource.  */
status = nx_lwm2m_client_object_execute (&lwm2m_client, 3303, 0, 0,  
                                         “5”, 1);

/* If status is NX_SUCCESS, an object resource was successfully executed.  */
```

## <a name="nx_lwm2m_client_object_instance_add"></a><span data-ttu-id="10326-450">nx_lwm2m_client_object_instance_add</span><span class="sxs-lookup"><span data-stu-id="10326-450">nx_lwm2m_client_object_instance_add</span></span>

<span data-ttu-id="10326-451">Nesnesine bir nesne örneği uygulama ekler.</span><span class="sxs-lookup"><span data-stu-id="10326-451">Adds an Object instance implementation to an object.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-452">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-452">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_instance_add(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-453">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-453">Description</span></span>

<span data-ttu-id="10326-454">Bu hizmet, LWM2M Istemcisine yeni bir nesne örneği uygulamasını ekler.</span><span class="sxs-lookup"><span data-stu-id="10326-454">This service adds a new Object instance implementation to the LWM2M Client.</span></span> <span data-ttu-id="10326-455">İnstance_id_ptr değeri **NX_LWM2M_CLIENT_RESERVED_ID**, LWM2M Client kullanılmamış bir örnek kimliğini otomatik olarak atayacaktır, aksi takdırde, LWM2M istemcisi uygulama kümesi değer kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="10326-455">If the value of instance_id_ptr is **NX_LWM2M_CLIENT_RESERVED_ID**, LWM2M Client will automatically assign an unused instance id, otherwise, LWM2M Client will use the value application set.</span></span> <span data-ttu-id="10326-456">Yeni örnek başarıyla eklendikten sonra, instance_id uygulamaya geri dönmek için instance_id_ptr doldurulur.</span><span class="sxs-lookup"><span data-stu-id="10326-456">Once new instance was added successfully, the instance_id will be filled in instance_id_ptr to return to application.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-457">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-457">Parameters</span></span>

- <span data-ttu-id="10326-458">**object_ptr** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-458">**object_ptr** Pointer to the structure defining the Object implementation.</span></span>
- <span data-ttu-id="10326-459">**instance_ptr** Nesne örneği uygulamasını tanımlayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-459">**instance_ptr** Pointer to the structure defining the Object instance implementation.</span></span>
- <span data-ttu-id="10326-460">**instance_id_ptr** Nesne örneği kimliğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-460">**instance_id_ptr** Pointer to the object instance id.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-461">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-461">Return Values</span></span>

- <span data-ttu-id="10326-462">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-462">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-463">**NX_CLIENT_LWM2M_ALREADY_EXIST** Nesne KIMLIĞI zaten var.</span><span class="sxs-lookup"><span data-stu-id="10326-463">**NX_CLIENT_LWM2M_ALREADY_EXIST** The Object ID already exists.</span></span>
- <span data-ttu-id="10326-464">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-464">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-465">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-465">Allowed From</span></span>

<span data-ttu-id="10326-466">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-466">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-467">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-467">Example</span></span>

```c
/* Add new object instance to the object.  */
status = nx_lwm2m_client_object_instance_add(&object, &object_instance,
                                             &instance_id);

/* If status is NX_SUCCESS, the new object instance was successfully added.  */
```

## <a name="nx_lwm2m_client_object_instance_next_get"></a><span data-ttu-id="10326-468">nx_lwm2m_client_object_instance_next_get</span><span class="sxs-lookup"><span data-stu-id="10326-468">nx_lwm2m_client_object_instance_next_get</span></span>

<span data-ttu-id="10326-469">Bir nesnenin sonraki örneğini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-469">Gets the next instance of an Object.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-470">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-470">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_instance_next_get(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-471">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-471">Description</span></span>

<span data-ttu-id="10326-472">Bu hizmet, belirtilen nesnenin sonraki nesne örneğinin KIMLIĞINI döndürür.</span><span class="sxs-lookup"><span data-stu-id="10326-472">This service returns the ID of the next Object Instance of the given Object.</span></span> <span data-ttu-id="10326-473">Geçerli örnek KIMLIĞI NX_LWM2M_RESERVED_ID olarak ayarlandıysa (65535) ilk Örneğin KIMLIĞI döndürülür.</span><span class="sxs-lookup"><span data-stu-id="10326-473">If the current Instance ID is set to NX_LWM2M_RESERVED_ID (65535) the ID of the first instance is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-474">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-474">Parameters</span></span>

- <span data-ttu-id="10326-475">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-475">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-476">**object_id** Nesne KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-476">**object_id** The Object ID.</span></span>
- <span data-ttu-id="10326-477">**instance_id_ptr** Geçerli nesne örneği KIMLIĞINE yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-477">**instance_id_ptr** Pointer to the current Object Instance ID.</span></span> <span data-ttu-id="10326-478">Dönüş sırasında nesnenin sonraki örnek KIMLIĞINI içerir.</span><span class="sxs-lookup"><span data-stu-id="10326-478">On return contains the next Instance ID of the Object.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-479">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-479">Return Values</span></span>

- <span data-ttu-id="10326-480">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-480">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-481">**NX_CLIENT_LWM2M_NOT_FOUND** Verilen örnek KIMLIĞI nesnenin son, veya nesne KIMLIĞI uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="10326-481">**NX_CLIENT_LWM2M_NOT_FOUND** The given Instance ID is the last of the object, or the Object ID is not implemented.</span></span>
- <span data-ttu-id="10326-482">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-482">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-483">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-483">Allowed From</span></span>

<span data-ttu-id="10326-484">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-484">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-485">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-485">Example</span></span>

```c
/* Get the next instance of an object.  */
status = nx_lwm2m_client_object_instance_next_get(&lwm2m_client, 3303, 
                                                  &instance_id);

/* If status is NX_SUCCESS, get the next instance successfully.  */
```

## <a name="nx_lwm2m_client_object_instance_remove"></a><span data-ttu-id="10326-486">nx_lwm2m_client_object_instance_remove</span><span class="sxs-lookup"><span data-stu-id="10326-486">nx_lwm2m_client_object_instance_remove</span></span>

<span data-ttu-id="10326-487">Nesne örneği uygulamasını nesnesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="10326-487">Removes an  Object instance implementation from an object.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-488">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-488">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_instance_remove(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-489">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-489">Description</span></span>

<span data-ttu-id="10326-490">Bu hizmet bir nesneden nesne örneğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="10326-490">This service removes an Object instance from an object.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-491">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-491">Parameters</span></span>

- <span data-ttu-id="10326-492">***object_ptr*** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-492">***object_ptr*** Pointer to the structure defining the Object implementation.</span></span>
- <span data-ttu-id="10326-493">**instance_ptr** Nesne örneği uygulamasını tanımlayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-493">**instance_ptr** Pointer to the structure defining the Object instance implementation.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-494">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-494">Return Values</span></span>

- <span data-ttu-id="10326-495">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-495">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-496">**NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne KIMLIĞI zaten var.</span><span class="sxs-lookup"><span data-stu-id="10326-496">**NX_LWM2M_CLIENT_ALREADY_EXIST** The Object ID already exists.</span></span>
- <span data-ttu-id="10326-497">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-497">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-498">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-498">Allowed From</span></span>

<span data-ttu-id="10326-499">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-499">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-500">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-500">Example</span></span>

```c
/* Remove object instance from an object.  */
status = nx_lwm2m_client_object_instance_remove(&object, &object_instance);

/* If status is NX_SUCCESS, the object instance was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_next_get"></a><span data-ttu-id="10326-501">nx_lwm2m_client_object_next_get</span><span class="sxs-lookup"><span data-stu-id="10326-501">nx_lwm2m_client_object_next_get</span></span>

<span data-ttu-id="10326-502">LWM2M Istemcisinin bir sonraki nesnesini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-502">Gets the next object of the LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-503">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-503">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_next_get(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID \*object_id_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-504">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-504">Description</span></span>

<span data-ttu-id="10326-505">Bu hizmet, LWM2M Istemcisi tarafından uygulanan bir sonraki nesnenin KIMLIĞINI döndürür.</span><span class="sxs-lookup"><span data-stu-id="10326-505">This service returns the ID of the next Object implemented by the LWM2M Client.</span></span> <span data-ttu-id="10326-506">Geçerli nesne KIMLIĞI NX_LWM2M_RESERVED_ID olarak ayarlandıysa (65535) ilk nesne KIMLIĞI döndürülür.</span><span class="sxs-lookup"><span data-stu-id="10326-506">If the current Object ID is set to NX_LWM2M_RESERVED_ID (65535) the first Object ID is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-507">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-507">Parameters</span></span>

- <span data-ttu-id="10326-508">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-508">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-509">**object_id_ptr** Geçerli nesne KIMLIĞINE yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-509">**object_id_ptr** Pointer to the current Object ID.</span></span> <span data-ttu-id="10326-510">Dönüşte, LWM2M Istemcisi tarafından uygulanan bir sonraki nesne KIMLIĞINI içerir.</span><span class="sxs-lookup"><span data-stu-id="10326-510">On return contains the next Object ID implemented by the LWM2M Client.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-511">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-511">Return Values</span></span>

- <span data-ttu-id="10326-512">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-512">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-513">**NX_LWM2M_CLIENT_NOT_FOUND** Verilen nesne KIMLIĞI, veritabanının son nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="10326-513">**NX_LWM2M_CLIENT_NOT_FOUND** The given Object ID is the last of the database.</span></span>
<span data-ttu-id="10326-514">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-514">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-515">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-515">Allowed From</span></span>

<span data-ttu-id="10326-516">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-516">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-517">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-517">Example</span></span>

```c
/* Get the next object of lwm2m client.  */
status = nx_lwm2m_client_object_next_get(&lwm2m_client, &object_id);

/* If status is NX_SUCCESS, get the next object successfully.  */
```

## <a name="nx_lwm2m_client_object_read"></a><span data-ttu-id="10326-518">nx_lwm2m_client_object_read</span><span class="sxs-lookup"><span data-stu-id="10326-518">nx_lwm2m_client_object_read</span></span>

<span data-ttu-id="10326-519">Bir nesne örneğinin resourcevalues değerlerini okur.</span><span class="sxs-lookup"><span data-stu-id="10326-519">Reads an Object Instance's resource's values.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-520">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-520">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_read(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT num_values,
    NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a><span data-ttu-id="10326-521">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-521">Description</span></span>

<span data-ttu-id="10326-522">Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde ' Read ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-522">This service performs a ‘Read’ operation on an Object Instance of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-523">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-523">Parameters</span></span>

- <span data-ttu-id="10326-524">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-524">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-525">**object_id** Nesne KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-525">**object_id** The Object ID.</span></span>
- <span data-ttu-id="10326-526">**instance_id** Nesne örneği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-526">**instance_id** The Object Instance ID.</span></span>
- <span data-ttu-id="10326-527">**num_values** Okunacak kaynak sayısı.</span><span class="sxs-lookup"><span data-stu-id="10326-527">**num_values** The number of resources to read.</span></span>
- <span data-ttu-id="10326-528">**values_ptr** Okunacak kaynakların kimliklerini içeren NX_LWM2M_RESOURCE dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-528">**values_ptr** Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources to read.</span></span> <span data-ttu-id="10326-529">Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="10326-529">On return the array is filled with the corresponding types and values.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-530">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-530">Return Values</span></span>

- <span data-ttu-id="10326-531">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-531">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-532">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Bir kaynak okuma işlemini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="10326-532">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** A resource doesn’t support the read operation.</span></span>
- <span data-ttu-id="10326-533">**NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI, nesne örneği KIMLIĞI veya kaynak KIMLIĞI yok.</span><span class="sxs-lookup"><span data-stu-id="10326-533">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID, Object Instance ID or a resource ID doesn’t exist.</span></span>
- <span data-ttu-id="10326-534">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-534">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-535">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-535">Allowed From</span></span>

<span data-ttu-id="10326-536">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-536">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-537">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-537">Example</span></span>

```c
/* Read the object resources.  */
status = nx_lwm2m_client_object_read(&lwm2m_client, 3303, 0, 2, &resource);

/* If status is NX_SUCCESS, the resources were successfully read.  */
```

## <a name="nx_lwm2m_client_object_remove"></a><span data-ttu-id="10326-538">nx_lwm2m_client_object_remove</span><span class="sxs-lookup"><span data-stu-id="10326-538">nx_lwm2m_client_object_remove</span></span>

<span data-ttu-id="10326-539">Nesne örneği uygulamasını nesnesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="10326-539">Removes an Object instance implementation from an object.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-540">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-540">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_remove(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_OBJECT *object_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-541">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-541">Description</span></span>

<span data-ttu-id="10326-542">Bu hizmet, bir nesneyi LWM2M Istemcisinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="10326-542">This service removes an Object from the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-543">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-543">Parameters</span></span>

- <span data-ttu-id="10326-544">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-544">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-545">**object_ptr** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-545">**object_ptr** Pointer to the structure defining the Object implementation.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-546">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-546">Return Values</span></span>

- <span data-ttu-id="10326-547">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-547">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-548">**NX_LWM2M_CLIENT_ALREADY_EXIST** Nesne KIMLIĞI zaten var.</span><span class="sxs-lookup"><span data-stu-id="10326-548">**NX_LWM2M_CLIENT_ALREADY_EXIST** The Object ID already exists.</span></span>
- <span data-ttu-id="10326-549">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-549">**NX_PTR_ERROR** Invalid pointer.</span></span>
- <span data-ttu-id="10326-550">**NX_LWM2M_CLIENT_FORBIDDEN** İç nesne kaldırılmaya izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="10326-550">**NX_LWM2M_CLIENT_FORBIDDEN** Removing internal object is forbidden.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-551">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-551">Allowed From</span></span>

<span data-ttu-id="10326-552">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-552">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-553">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-553">Example</span></span>

```c
/* Remove object from lwm2m client.  */
status = nx_lwm2m_client_object_remove(&lwm2m_client, &object);

/* If status is NX_SUCCESS, the object was successfully removed.  */
```

## <a name="nx_lwm2m_client_object_resource_changed"></a><span data-ttu-id="10326-554">nx_lwm2m_client_object_resource_changed</span><span class="sxs-lookup"><span data-stu-id="10326-554">nx_lwm2m_client_object_resource_changed</span></span>

<span data-ttu-id="10326-555">Bir nesne kaynağının değişikliğine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="10326-555">Signals a change of an Object resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-556">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-556">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_resource_changed(
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr,
    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a><span data-ttu-id="10326-557">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-557">Description</span></span>

<span data-ttu-id="10326-558">Hizmet, uygulama tarafından nesne kaynağının değiştiği LWM2M Istemcisine işaret etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10326-558">The service is used by the application to signal to the LWM2M Client that a resource of the Object has changed.</span></span> <span data-ttu-id="10326-559">LWM2M Istemcisi, kaynak bir LWM2M sunucusu tarafından gözlemleniyorsa bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="10326-559">The LWM2M Client will send a notification if the resource is observed by a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-560">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-560">Parameters</span></span>

- <span data-ttu-id="10326-561">**object_ptr** Nesne uygulamasını tanımlayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-561">**object_ptr** Pointer to the structure defining the Object implementation.</span></span>
- <span data-ttu-id="10326-562">***instance_ptr*** Nesne örneği uygulamasını tanımlayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-562">***instance_ptr*** Pointer to the structure defining the Object instance implementation.</span></span>
- <span data-ttu-id="10326-563">**kaynak** Değiştirilen kaynağı açıklayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-563">**resource** Pointer to the structure describing the resource that has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-564">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-564">Return Values</span></span>

- <span data-ttu-id="10326-565">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-565">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-566">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-566">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-567">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-567">Allowed From</span></span>

<span data-ttu-id="10326-568">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-568">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-569">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-569">Example</span></span>

```c
/* Change object resource.  */
status = nx_lwm2m_client_object_resource_changed(&object, &instance, &resource);

/* If status is NX_SUCCESS, a resource was successfully changed.  */
```

## <a name="nx_lwm2m_client_object_write"></a><span data-ttu-id="10326-570">nx_lwm2m_client_object_write</span><span class="sxs-lookup"><span data-stu-id="10326-570">nx_lwm2m_client_object_write</span></span>

<span data-ttu-id="10326-571">Kaynak bir nesne örneğinin değerlerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-571">Changes resource's values of an Object instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-572">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-572">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_write(
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id,
    NX_LWM2M_ID instance_id,
    UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr,
    UINT write_op);
```

### <a name="description"></a><span data-ttu-id="10326-573">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-573">Description</span></span>

<span data-ttu-id="10326-574">Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde ' Write ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-574">This service performs a ‘Write’ operation on an Object Instance of the LWM2M Client.</span></span>

<span data-ttu-id="10326-575">*Write_op* parametresine aşağıdaki yazma işlemleri de belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="10326-575">The following write operations can be specified to the *write_op* parameter.</span></span>

| <span data-ttu-id="10326-576">Değer</span><span class="sxs-lookup"><span data-stu-id="10326-576">Value</span></span> | <span data-ttu-id="10326-577">Yazma &nbsp; işlemi</span><span class="sxs-lookup"><span data-stu-id="10326-577">Write&nbsp;Operation</span></span> | <span data-ttu-id="10326-578">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-578">Description</span></span> |
| --- | ---| --- |
| <span data-ttu-id="10326-579">0</span><span class="sxs-lookup"><span data-stu-id="10326-579">0</span></span> | <span data-ttu-id="10326-580">Kısmi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="10326-580">Partial Update</span></span> | <span data-ttu-id="10326-581">Yeni değerde belirtilen kaynakları ekler veya güncelleştirir ve diğer mevcut kaynakları değişmeden bırakır.</span><span class="sxs-lookup"><span data-stu-id="10326-581">Adds or updates Resources provided in the new value and leaves other existing Resources unchanged.</span></span> |
| <span data-ttu-id="10326-582">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE**</span><span class="sxs-lookup"><span data-stu-id="10326-582">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE**</span></span> | <span data-ttu-id="10326-583">Örneği Değiştir</span><span class="sxs-lookup"><span data-stu-id="10326-583">Replace Instance</span></span> | <span data-ttu-id="10326-584">Nesne örneğini, belirtilen yeni kaynak değerleriyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-584">Replaces the Object Instance with the new provided resource values.</span></span> |
| <span data-ttu-id="10326-585">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE**</span><span class="sxs-lookup"><span data-stu-id="10326-585">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE**</span></span> | <span data-ttu-id="10326-586">Kaynağı değiştir</span><span class="sxs-lookup"><span data-stu-id="10326-586">Replace Resource</span></span> | <span data-ttu-id="10326-587">Kaynakları, belirtilen yeni kaynak değerleriyle (birden çok kaynağı değiştirmek için kullanılır) değiştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-587">Replaces the Resources with the new provided resource values (used to replace Multiple Resources).</span></span> |
| <span data-ttu-id="10326-588">**NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP**</span><span class="sxs-lookup"><span data-stu-id="10326-588">**NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP**</span></span> | <span data-ttu-id="10326-589">Önyükleme yazma</span><span class="sxs-lookup"><span data-stu-id="10326-589">Bootstrap Write</span></span> | <span data-ttu-id="10326-590">Bir önyükleme dizisinin çağrısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="10326-590">Indicates a call from a Bootstrap sequence.</span></span> |

### <a name="parameters"></a><span data-ttu-id="10326-591">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-591">Parameters</span></span>

- <span data-ttu-id="10326-592">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-592">**client_ptr** Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="10326-593">**object_id** Nesne KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-593">**object_id** The Object ID.</span></span>
- <span data-ttu-id="10326-594">**instance_id** Nesne örneği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-594">**instance_id** The Object Instance ID.</span></span>
- <span data-ttu-id="10326-595">**num_values** Yazılacak kaynak sayısı.</span><span class="sxs-lookup"><span data-stu-id="10326-595">**num_values** The number of resources to write.</span></span>
- <span data-ttu-id="10326-596">**values_ptr** Kaynak kimliklerini, türleri ve yazılacak değerleri içeren bir NX_LWM2M_RESOURCE dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-596">**values_ptr** Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources, the types and the values to write.</span></span>
- <span data-ttu-id="10326-597">**write_op** Yazma işlemi türü.</span><span class="sxs-lookup"><span data-stu-id="10326-597">**write_op** The type of write operation.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-598">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-598">Return Values</span></span>

- <span data-ttu-id="10326-599">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-599">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-600">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak türü geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="10326-600">**NX_LWM2M_CLIENT_BAD_ENCODING** The type of a resource is not valid.</span></span>
- <span data-ttu-id="10326-601">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** Değerin uzunluğu, örnekte depolanamayacak kadar büyük.</span><span class="sxs-lookup"><span data-stu-id="10326-601">**NX_LWM2M_CLIENT_BUFFER_TOO_SMALL** The length of a value is too big to be stored in the instance.</span></span>
- <span data-ttu-id="10326-602">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** Kaynak, yazma işlemini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="10326-602">**NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** A resource doesn’t support the write operation.</span></span>
- <span data-ttu-id="10326-603">**NX_LWM2M_CLIENT_NO_MEMORY** Kaynak değeri depolamak için bellek ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="10326-603">**NX_LWM2M_CLIENT_NO_MEMORY** Cannot allocate memory to store a resource value.</span></span>
- <span data-ttu-id="10326-604">**NX_LWM2M_CLIENT_NOT_ACCEPTABLE** Kaynağın değeri geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="10326-604">**NX_LWM2M_CLIENT_NOT_ACCEPTABLE** The value of a resource is not valid.</span></span>
- <span data-ttu-id="10326-605">**NX_LWM2M_CLIENT_NOT_FOUND** Nesne KIMLIĞI, nesne örneği KIMLIĞI veya kaynak KIMLIĞI yok.</span><span class="sxs-lookup"><span data-stu-id="10326-605">**NX_LWM2M_CLIENT_NOT_FOUND** The Object ID, Object Instance ID or a resource ID doesn’t exist.</span></span>
- <span data-ttu-id="10326-606">**NX_OPTION_ERROR** Geçersiz yazma işlemi türü.</span><span class="sxs-lookup"><span data-stu-id="10326-606">**NX_OPTION_ERROR** Invalid type of write operation.</span></span> 
- <span data-ttu-id="10326-607">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-607">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-608">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-608">Allowed From</span></span>

<span data-ttu-id="10326-609">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-609">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-610">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-610">Example</span></span>

```c
/* Write object resources.  */
status = nx_lwm2m_client_object_write(&lwm2m_client, 3303, 0, 2, &resource,
                                      NX_LWM2M_CLIENT_OBJECT_WRITE_UPDATE);

/* If status is NX_SUCCESS, write object resources successfully.  */
```

## <a name="nx_lwm2m_client_resource_boolean_get"></a><span data-ttu-id="10326-611">nx_lwm2m_client_resource_boolean_get</span><span class="sxs-lookup"><span data-stu-id="10326-611">nx_lwm2m_client_resource_boolean_get</span></span>

<span data-ttu-id="10326-612">Boole kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-612">Gets the value of a Boolean Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-613">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-613">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_boolean_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-614">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-614">Description</span></span>

<span data-ttu-id="10326-615">Hizmet bir Boole kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-615">The service retrieves the value of a Boolean Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-616">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-616">Parameters</span></span>

- <span data-ttu-id="10326-617">**kaynak** Kaynak değeri açıklaması işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-617">**resource** Pointer to Resource value description.</span></span>
- <span data-ttu-id="10326-618">**bool_ptr** Hedef Boolean değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-618">**bool_ptr** Pointer to the destination Boolean value.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-619">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-619">Return Values</span></span>

- <span data-ttu-id="10326-620">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-620">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-621">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="10326-621">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a Boolean value.</span></span>
- <span data-ttu-id="10326-622">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-622">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-623">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-623">Allowed From</span></span>

<span data-ttu-id="10326-624">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-624">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-625">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-625">Example</span></span>

```c
/* Get the value of a Boolean resource.  */
status = nx_lwm2m_client_resource_boolean_get(&resource, &bool);

/* If status is NX_SUCCESS, the value of Boolean resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_boolean_set"></a><span data-ttu-id="10326-626">nx_lwm2m_client_resource_boolean_set</span><span class="sxs-lookup"><span data-stu-id="10326-626">nx_lwm2m_client_resource_boolean_set</span></span>

<span data-ttu-id="10326-627">Boole kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-627">Sets the value of a Boolean Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-628">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-628">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_boolean_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_BOOL bool_data);
```

### <a name="description"></a><span data-ttu-id="10326-629">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-629">Description</span></span>

<span data-ttu-id="10326-630">Hizmet bir Boole kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-630">The service sets the value of a Boolean Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-631">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-631">Parameters</span></span>

- <span data-ttu-id="10326-632">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-632">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-633">**bool_data** Boole verileri.</span><span class="sxs-lookup"><span data-stu-id="10326-633">**bool_data** Boolean data.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-634">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-634">Return Values</span></span>

- <span data-ttu-id="10326-635">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-635">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-636">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-636">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-637">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-637">Allowed From</span></span>

<span data-ttu-id="10326-638">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-638">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-639">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-639">Example</span></span>

```c
/* Set the value of a Boolean resource.  */
status = nx_lwm2m_client_resource_boolean_set(&resource, NX_TRUE);

/* If status is NX_SUCCESS, the value of Boolean resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_dim_get"></a><span data-ttu-id="10326-640">nx_lwm2m_client_resource_dim_get</span><span class="sxs-lookup"><span data-stu-id="10326-640">nx_lwm2m_client_resource_dim_get</span></span>

<span data-ttu-id="10326-641">Birden çok kaynak için kaynak boyutunu alır</span><span class="sxs-lookup"><span data-stu-id="10326-641">Gets the resource dimension for multiple Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-642">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-642">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_dim_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    UCHAR *dim);
```

### <a name="description"></a><span data-ttu-id="10326-643">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-643">Description</span></span>

<span data-ttu-id="10326-644">Hizmet, birden fazla kaynak için kaynak boyutunu alır.</span><span class="sxs-lookup"><span data-stu-id="10326-644">The service retrieves the resource dimension for multiple resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-645">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-645">Parameters</span></span>

- <span data-ttu-id="10326-646">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-646">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-647">hedef boyutun **karartma** işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-647">**dim** Pointer to the destination dimension.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-648">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-648">Return Values</span></span>

- <span data-ttu-id="10326-649">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-649">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-650">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="10326-650">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a Boolean value.</span></span>
- <span data-ttu-id="10326-651">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-651">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-652">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-652">Allowed From</span></span>

<span data-ttu-id="10326-653">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-653">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-654">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-654">Example</span></span>

```c
/* Get the resource dimension for multiple resource.  */
status = nx_lwm2m_client_resource_dim_get(&resource, &dim);

/* If status is NX_SUCCESS, the resource dimension was successfully get. */
```

## <a name="nx_lwm2m_client_resource_dim_set"></a><span data-ttu-id="10326-655">nx_lwm2m_client_resource_dim_set</span><span class="sxs-lookup"><span data-stu-id="10326-655">nx_lwm2m_client_resource_dim_set</span></span>

<span data-ttu-id="10326-656">Birden çok kaynak için kaynak boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-656">Sets the resource dimension for multiple resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-657">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-657">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_dim_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    CHAR dim);
```

### <a name="description"></a><span data-ttu-id="10326-658">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-658">Description</span></span>

<span data-ttu-id="10326-659">Hizmet, birden fazla kaynak için kaynak boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-659">The service sets the resource dimension for multiple resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-660">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-660">Parameters</span></span>

- <span data-ttu-id="10326-661">**değer** Kaynak değeri açıklaması işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-661">**value** Pointer to Resource value description.</span></span>
- <span data-ttu-id="10326-662">**Dim** boyut değeri.</span><span class="sxs-lookup"><span data-stu-id="10326-662">**dim** Dimension value.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-663">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-663">Return Values</span></span>

- <span data-ttu-id="10326-664">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-664">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-665">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-665">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-666">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-666">Allowed From</span></span>

<span data-ttu-id="10326-667">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-667">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-668">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-668">Example</span></span>

```c
/* Set the resource dimension.  */
status = nx_lwm2m_client_resource_dim_set(&resource, 3);

/* If status is NX_SUCCESS, the resource dimension was successfully set. */
```

## <a name="nx_lwm2m_client_resource_float32_get"></a><span data-ttu-id="10326-669">nx_lwm2m_client_resource_float32_get</span><span class="sxs-lookup"><span data-stu-id="10326-669">nx_lwm2m_client_resource_float32_get</span></span>

<span data-ttu-id="10326-670">32 bitlik bir **float** kaynağının değerini alır</span><span class="sxs-lookup"><span data-stu-id="10326-670">Gets the value of a 32-Bit **float** Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-671">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-671">Prototype</span></span>

```C
UINT nx_lwm2m_client_resource_float32_get(
    NX_LWM2M_CLIENT_RESOURCE *resource,
    NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-672">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-672">Description</span></span>

<span data-ttu-id="10326-673">Hizmet, 32 bitlik bir **float** kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-673">The service retrieves the value of a 32-Bit **float** Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-674">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-674">Parameters</span></span>

- <span data-ttu-id="10326-675">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-675">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-676">**float32_ptr** Hedef 32-bit **kayan** değer işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-676">**float32_ptr** Pointer to the destination 32-Bit **float** value.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-677">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-677">Return Values</span></span>

- <span data-ttu-id="10326-678">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-678">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-679">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="10326-679">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a Boolean value.</span></span>
- <span data-ttu-id="10326-680">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-680">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-681">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-681">Allowed From</span></span>

<span data-ttu-id="10326-682">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-682">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-683">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-683">Example</span></span>

```C
/* Get the value of a 32-Bit float resource.  */
status = nx_lwm2m_client_resource_float32_get(&resource, &float32);

/* If status is NX_SUCCESS, the value of 32-Bit float resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_float32_set"></a><span data-ttu-id="10326-684">nx_lwm2m_client_resource_float32_set</span><span class="sxs-lookup"><span data-stu-id="10326-684">nx_lwm2m_client_resource_float32_set</span></span>

<span data-ttu-id="10326-685">32 bitlik bir **float** kaynağının değerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="10326-685">Sets the value of a 32-Bit **float** Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-686">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-686">Prototype</span></span>

```C
UINT nx_lwm2m_client_resource_float32_set(
    NX_LWM2M_CLIENT_RESOURCE *resource,
    NX_LWM2M_FLOAT32 float32_data);
```

### <a name="description"></a><span data-ttu-id="10326-687">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-687">Description</span></span>

<span data-ttu-id="10326-688">Hizmet, 32 bitlik bir **float** kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-688">The service sets the value of a 32-Bit **float** Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-689">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-689">Parameters</span></span>

- <span data-ttu-id="10326-690">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-690">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-691">**float32_data** 32 bit **kayan** verileri.</span><span class="sxs-lookup"><span data-stu-id="10326-691">**float32_data** 32-Bit **float** data.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-692">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-692">Return Values</span></span>

- <span data-ttu-id="10326-693">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-693">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-694">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-694">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-695">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-695">Allowed From</span></span>

<span data-ttu-id="10326-696">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-696">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-697">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-697">Example</span></span>

```c
/* Set the value of a 32-Bit float resource.  */
status = nx_lwm2m_client_resource_float32_set(&resource, 1.24);

/* If status is NX_SUCCESS, the value of 32-Bit float resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_float64_get"></a><span data-ttu-id="10326-698">nx_lwm2m_client_resource_float64_get</span><span class="sxs-lookup"><span data-stu-id="10326-698">nx_lwm2m_client_resource_float64_get</span></span>

<span data-ttu-id="10326-699">64 bitlik bir float kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-699">Gets the value of a 64-Bit float Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-700">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-700">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_float64_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-701">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-701">Description</span></span>

<span data-ttu-id="10326-702">Hizmet, 64 bitlik bir **float** kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-702">The service retrieves the value of a 64-Bit **float** Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-703">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-703">Parameters</span></span>

- <span data-ttu-id="10326-704">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-704">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-705">**float64_ptr** Hedef 64-bit **kayan** değer işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-705">**float64_ptr** Pointer to the destination 64-Bit **float** value.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-706">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-706">Return Values</span></span>

- <span data-ttu-id="10326-707">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-707">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-708">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir float değeri değil.</span><span class="sxs-lookup"><span data-stu-id="10326-708">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a float value.</span></span>
- <span data-ttu-id="10326-709">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-709">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-710">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-710">Allowed From</span></span>

<span data-ttu-id="10326-711">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-711">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-712">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-712">Example</span></span>

```c
/* Get the value of a 64-Bit float resource.  */
status = nx_lwm2m_client_resource_float64_get(&resource, &float64);

/* If status is NX_SUCCESS, the value of 64-Bit float resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_float64_set"></a><span data-ttu-id="10326-713">nx_lwm2m_client_resource_float64_set</span><span class="sxs-lookup"><span data-stu-id="10326-713">nx_lwm2m_client_resource_float64_set</span></span>

<span data-ttu-id="10326-714">64 bitlik bir **float** kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-714">Sets the value of a 64-Bit **float** Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-715">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-715">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_float64_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_FLOAT64 float64_data);
```

### <a name="description"></a><span data-ttu-id="10326-716">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-716">Description</span></span>

<span data-ttu-id="10326-717">Hizmet, 64 bitlik bir **float** kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-717">The service sets the value of a 64-Bit **float** Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-718">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-718">Parameters</span></span>

- <span data-ttu-id="10326-719">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-719">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-720">**float64_data** 64 bit **kayan** verileri.</span><span class="sxs-lookup"><span data-stu-id="10326-720">**float64_data** 64-bit **float** data.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-721">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-721">Return Values</span></span>

- <span data-ttu-id="10326-722">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-722">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-723">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-723">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-724">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-724">Allowed From</span></span>

<span data-ttu-id="10326-725">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-725">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-726">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-726">Example</span></span>

```c
/* Set the value of a 64-Bit float resource.  */
status = nx_lwm2m_client_resource_float64_set(&resource, 1.24);

/* If status is NX_SUCCESS, the value of 64-Bit float resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_info_get"></a><span data-ttu-id="10326-727">nx_lwm2m_client_resource_info_get</span><span class="sxs-lookup"><span data-stu-id="10326-727">nx_lwm2m_client_resource_info_get</span></span>

<span data-ttu-id="10326-728">Kaynak bilgisini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-728">Gets the resource info.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-729">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-729">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_info_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_ID *resource_id, 
    ULONG *operation);
```

### <a name="description"></a><span data-ttu-id="10326-730">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-730">Description</span></span>

<span data-ttu-id="10326-731">Hizmet, kaynağın kaynak bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-731">The service retrieves the resource information of Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-732">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-732">Parameters</span></span>

- <span data-ttu-id="10326-733">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-733">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-734">**resource_id** Hedef kaynak KIMLIĞI işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-734">**resource_id** Pointer to the destination resource ID.</span></span>
- <span data-ttu-id="10326-735">**işlem** Hedef kaynak işlemine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-735">**operation** Pointer to the destination resource operation.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-736">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-736">Return Values</span></span>

- <span data-ttu-id="10326-737">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-737">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-738">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-738">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-739">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-739">Allowed From</span></span>

<span data-ttu-id="10326-740">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-740">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-741">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-741">Example</span></span>

```c
/* Get the resource information.  */
status = nx_lwm2m_client_resource_info_get(&resource, &resource_id, &operation);

/* If status is NX_SUCCESS, the resource information was successfully get. */
```

## <a name="nx_lwm2m_client_resource_info_set"></a><span data-ttu-id="10326-742">nx_lwm2m_client_resource_info_set</span><span class="sxs-lookup"><span data-stu-id="10326-742">nx_lwm2m_client_resource_info_set</span></span>

<span data-ttu-id="10326-743">Kaynak bilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-743">Sets the resource information.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-744">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-744">Prototype</span></span>

```C
UINT nx_lwm2m_client_resource_info_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    NX_LWM2M_FLOAT64 float64_data);
```

### <a name="description"></a><span data-ttu-id="10326-745">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-745">Description</span></span>

<span data-ttu-id="10326-746">Hizmet, kaynak bilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-746">The service sets the resource information.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-747">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-747">Parameters</span></span>

- <span data-ttu-id="10326-748">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-748">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-749">**resource_id** Kaynağın KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-749">**resource_id** ID of the resource.</span></span>
- <span data-ttu-id="10326-750">**işlem** Kaynağın işlemi.</span><span class="sxs-lookup"><span data-stu-id="10326-750">**operation** Operation of the resource.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-751">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-751">Return Values</span></span>

- <span data-ttu-id="10326-752">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-752">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-753">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-753">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-754">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-754">Allowed From</span></span>

<span data-ttu-id="10326-755">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-755">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-756">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-756">Example</span></span>

```c
/* Set the resource information.  */
status = nx_lwm2m_client_resource_info_set(&resource, 0, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);

/* If status is NX_SUCCESS, the resource information was successfully set. */
```

## <a name="nx_lwm2m_client_resource_instances_get"></a><span data-ttu-id="10326-757">nx_lwm2m_client_resource_instances_get</span><span class="sxs-lookup"><span data-stu-id="10326-757">nx_lwm2m_client_resource_instances_get</span></span>

<span data-ttu-id="10326-758">Birden çok kaynağın örneğini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-758">Gets the instance of multiple resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-759">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-759">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_instances_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_CLIENT_RESOURCE *resource_instances, 
    UINT *count);
```

### <a name="description"></a><span data-ttu-id="10326-760">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-760">Description</span></span>

<span data-ttu-id="10326-761">Hizmet, kaynağın kaynak bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-761">The service retrieves the resource information of Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-762">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-762">Parameters</span></span>

- <span data-ttu-id="10326-763">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-763">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-764">**resource_instances** Hedef kaynak KIMLIĞI işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-764">**resource_instances** Pointer to the destination resource ID.</span></span>
- <span data-ttu-id="10326-765">**sayı** Sayı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-765">**count** Pointer to the count.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-766">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-766">Return Values</span></span>

- <span data-ttu-id="10326-767">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-767">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-768">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="10326-768">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a Boolean value.</span></span>
- <span data-ttu-id="10326-769">**NX_LWM2M_CLIENT_NO_MEMORY** Örnekleri doldurulacak bellek yok.</span><span class="sxs-lookup"><span data-stu-id="10326-769">**NX_LWM2M_CLIENT_NO_MEMORY** No memory to fill out instances.</span></span>
- <span data-ttu-id="10326-770">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-770">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-771">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-771">Allowed From</span></span>

<span data-ttu-id="10326-772">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-772">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-773">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-773">Example</span></span>

```c
/* Get the resource information.  */
status = nx_lwm2m_client_resource_instances_get(&resource, &resource_instances,
                                                &count);

/* If status is NX_SUCCESS, the instances of multiple resource information were successfully get. */
```

## <a name="nx_lwm2m_client_resource_instances_set"></a><span data-ttu-id="10326-774">nx_lwm2m_client_resource_instances_set</span><span class="sxs-lookup"><span data-stu-id="10326-774">nx_lwm2m_client_resource_instances_set</span></span>

<span data-ttu-id="10326-775">Kaynak örneklerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-775">Sets the resource instances.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-776">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-776">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_instances_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_CLIENT_RESOURCE *resource_instances, 
    UINT count);
```
### <a name="description"></a><span data-ttu-id="10326-777">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-777">Description</span></span>

<span data-ttu-id="10326-778">Hizmet, birden fazla kaynağın kaynak örneklerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-778">The service sets the resource instances for multiple resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-779">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-779">Parameters</span></span>

- <span data-ttu-id="10326-780">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-780">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-781">**resource_instance** Kaynak örnekleri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-781">**resource_instance** Pointer to resource instances.</span></span>
- <span data-ttu-id="10326-782">**sayı** Kaynak örneklerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="10326-782">**count** Count of resource instances.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-783">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-783">Return Values</span></span>

- <span data-ttu-id="10326-784">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-784">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-785">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-785">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-786">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-786">Allowed From</span></span>

<span data-ttu-id="10326-787">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-787">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-788">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-788">Example</span></span>

```c
/* Set the resource information.  */
status = nx_lwm2m_client_resource_instances_set(&resource, &resource_instance, 2);

/* If status is NX_SUCCESS, the resource instances were successfully set. */
```

## <a name="nx_lwm2m_client_resource_integer32_get"></a><span data-ttu-id="10326-789">nx_lwm2m_client_resource_integer32_get</span><span class="sxs-lookup"><span data-stu-id="10326-789">nx_lwm2m_client_resource_integer32_get</span></span>

<span data-ttu-id="10326-790">32 bitlik bir tamsayı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-790">Gets the value of a 32-Bit integer Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-791">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-791">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_integer32_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER32 *integer32_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-792">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-792">Description</span></span>

<span data-ttu-id="10326-793">Hizmet, 32 bitlik bir tamsayı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-793">The service retrieves the value of a 32-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-794">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-794">Parameters</span></span>

- <span data-ttu-id="10326-795">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-795">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-796">**integer32_ptr** 32 bitlik tamsayı değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-796">**integer32_ptr** Pointer to the 32-Bit integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-797">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-797">Return Values</span></span>

- <span data-ttu-id="10326-798">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-798">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-799">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri tamsayı değeri değil.</span><span class="sxs-lookup"><span data-stu-id="10326-799">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not integer value.</span></span>
- <span data-ttu-id="10326-800">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-800">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-801">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-801">Allowed From</span></span>

<span data-ttu-id="10326-802">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-802">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-803">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-803">Example</span></span>

```c
/* Get the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_get(&resource, &integer32);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer32_set"></a><span data-ttu-id="10326-804">nx_lwm2m_client_resource_integer32_set</span><span class="sxs-lookup"><span data-stu-id="10326-804">nx_lwm2m_client_resource_integer32_set</span></span>

<span data-ttu-id="10326-805">32 bitlik bir tamsayı kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-805">Sets the value of a 32-Bit integer Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-806">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-806">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_integer32_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER32 integer32_data);
```

### <a name="description"></a><span data-ttu-id="10326-807">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-807">Description</span></span>

<span data-ttu-id="10326-808">Hizmet, 32 bitlik bir tamsayı kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-808">The service sets the value of a 32-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-809">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-809">Parameters</span></span>

- <span data-ttu-id="10326-810">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-810">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-811">**integer32_data** 32 bit tamsayı verileri.</span><span class="sxs-lookup"><span data-stu-id="10326-811">**integer32_data** 32-Bit integer data.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-812">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-812">Return Values</span></span>

- <span data-ttu-id="10326-813">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-813">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-814">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-814">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-815">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-815">Allowed From</span></span>

<span data-ttu-id="10326-816">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-816">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-817">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-817">Example</span></span>

```c
/* Set the value of a 32-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer32_set(&resource, 8);

/* If status is NX_SUCCESS, the value of 32-Bit integer resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_integer64_get"></a><span data-ttu-id="10326-818">nx_lwm2m_client_resource_integer64_get</span><span class="sxs-lookup"><span data-stu-id="10326-818">nx_lwm2m_client_resource_integer64_get</span></span>

<span data-ttu-id="10326-819">64 bitlik bir tamsayı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-819">Gets the value of a 64-Bit integer Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-820">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-820">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_integer64_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 *integer64_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-821">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-821">Description</span></span>

<span data-ttu-id="10326-822">Hizmet, 64 bitlik bir tamsayı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-822">The service retrieves the value of a 64-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-823">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-823">Parameters</span></span>

- <span data-ttu-id="10326-824">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-824">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-825">**integer64_ptr** 64 bitlik tamsayı değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-825">**integer64_ptr** Pointer to the 64-Bit integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-826">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-826">Return Values</span></span>

- <span data-ttu-id="10326-827">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-827">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-828">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri 64 bitlik bir tamsayı değeri değil.</span><span class="sxs-lookup"><span data-stu-id="10326-828">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not 64-Bit integer value.</span></span>
- <span data-ttu-id="10326-829">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-829">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-830">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-830">Allowed From</span></span>

<span data-ttu-id="10326-831">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-831">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-832">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-832">Example</span></span>

```c
/* Get the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_get(&resource, &integer64);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_integer64_set"></a><span data-ttu-id="10326-833">nx_lwm2m_client_resource_integer64_set</span><span class="sxs-lookup"><span data-stu-id="10326-833">nx_lwm2m_client_resource_integer64_set</span></span>

## <a name="set-the-value-of-a-64-bit-integer-resource"></a><span data-ttu-id="10326-834">64 bitlik bir tamsayı kaynağının değerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="10326-834">Set the value of a 64-Bit integer Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-835">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-835">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_integer64_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_INTEGER64 integer64_data);
```

### <a name="description"></a><span data-ttu-id="10326-836">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-836">Description</span></span>

<span data-ttu-id="10326-837">Hizmet, 64 bitlik bir tamsayı kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-837">The service sets the value of a 64-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-838">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-838">Parameters</span></span>

- <span data-ttu-id="10326-839">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-839">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-840">**integer64_data** 64 bit tamsayı.</span><span class="sxs-lookup"><span data-stu-id="10326-840">**integer64_data** 64-bit integer.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-841">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-841">Return Values</span></span>

- <span data-ttu-id="10326-842">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-842">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-843">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-843">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-844">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-844">Allowed From</span></span>

<span data-ttu-id="10326-845">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-845">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-846">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-846">Example</span></span>

```c
/* Set the value of a 64-Bit integer resource.  */
status = nx_lwm2m_client_resource_integer64_set(&resource, 32323);

/* If status is NX_SUCCESS, the value of 64-Bit integer resource was successfully set. */
```

##  <a name="nx_lwm2m_client_resource_objlnk_get"></a><span data-ttu-id="10326-847">nx_lwm2m_client_resource_objlnk_get</span><span class="sxs-lookup"><span data-stu-id="10326-847">nx_lwm2m_client_resource_objlnk_get</span></span>

<span data-ttu-id="10326-848">Bir nesne bağlantı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-848">Gets the value of an object link resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-849">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-849">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_objlnk_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    NX_LWM2M_ID *object_id, 
    NX_LWM2M_ID *instance_id);
```

### <a name="description"></a><span data-ttu-id="10326-850">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-850">Description</span></span>

<span data-ttu-id="10326-851">Hizmet, nesne bağlantısının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-851">The service retrieves the value of object link.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-852">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-852">Parameters</span></span>

- <span data-ttu-id="10326-853">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-853">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-854">**object_id** Nesne KIMLIĞINE yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-854">**object_id** Pointer to the object ID.</span></span>
- <span data-ttu-id="10326-855">**instance_id** Nesne örneği KIMLIĞINE yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-855">**instance_id** Pointer to the object instance ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-856">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-856">Return Values</span></span>

- <span data-ttu-id="10326-857">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-857">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-858">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir nesne bağlantı değeri değil.</span><span class="sxs-lookup"><span data-stu-id="10326-858">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not an object link value.</span></span>
- <span data-ttu-id="10326-859">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-859">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-860">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-860">Allowed From</span></span>

<span data-ttu-id="10326-861">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-861">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-862">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-862">Example</span></span>

```c
/* Get the value of the object link resource.  */
status = nx_lwm2m_client_resource_objlnk_get(&resource, &object_id, &instance_id);

/* If status is NX_SUCCESS, the object link value was successfully get. */
```

## <a name="nx_lwm2m_client_resource_objlnk_set"></a><span data-ttu-id="10326-863">nx_lwm2m_client_resource_objlnk_set</span><span class="sxs-lookup"><span data-stu-id="10326-863">nx_lwm2m_client_resource_objlnk_set</span></span>

<span data-ttu-id="10326-864">Kaynak örneklerini ayarlar</span><span class="sxs-lookup"><span data-stu-id="10326-864">Sets the resource instances</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-865">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-865">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_objlnk_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    NX_LWM2M_ID object_id, 
    NX_LWM2M_ID instance_id);
```

### <a name="description"></a><span data-ttu-id="10326-866">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-866">Description</span></span>

<span data-ttu-id="10326-867">Hizmet, nesne bağlantısı kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-867">The service sets the value of the object link resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-868">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-868">Parameters</span></span>

- <span data-ttu-id="10326-869">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-869">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-870">**object_id** Nesne KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-870">**object_id** Object ID.</span></span>
- <span data-ttu-id="10326-871">**instance_id** Nesne örneği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-871">**instance_id** Object instance ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-872">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-872">Return Values</span></span>

- <span data-ttu-id="10326-873">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-873">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-874">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-874">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-875">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-875">Allowed From</span></span>

<span data-ttu-id="10326-876">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-876">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-877">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-877">Example</span></span>

```c
/* Set the value of object link resource.  */
status = nx_lwm2m_client_resource_objlnk_set(&resource, 3303, 2);

/* If status is NX_SUCCESS, the value of object link resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_opaque_get"></a><span data-ttu-id="10326-878">nx_lwm2m_client_resource_opaque_get</span><span class="sxs-lookup"><span data-stu-id="10326-878">nx_lwm2m_client_resource_opaque_get</span></span>

<span data-ttu-id="10326-879">Donuk bir kaynağın değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-879">Gets the value of an opaque Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-880">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-880">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_opaque_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    const VOID **opaque_ptr, 
    UINT \*opaque_length);
```


### <a name="description"></a><span data-ttu-id="10326-881">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-881">Description</span></span>

<span data-ttu-id="10326-882">Hizmet, donuk bir kaynağın değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-882">The service retrieves the value of an opaque Resource.</span></span> <span data-ttu-id="10326-883">Donuk bir kaynak değeri, arabelleğin ve uzunluğun bir işaretçisinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="10326-883">An opaque resource value consists of a pointer to a buffer and a length.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-884">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-884">Parameters</span></span>

- <span data-ttu-id="10326-885">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-885">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-886">**opaque_ptr** Donuk verilerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-886">**opaque_ptr** Pointer to the opaque data.</span></span>
- <span data-ttu-id="10326-887">**opaque_length** Donuk veri uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-887">**opaque_length** Pointer to the opaque data length.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-888">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-888">Return Values</span></span>

- <span data-ttu-id="10326-889">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-889">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-890">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri donuk bir kaynak değil.</span><span class="sxs-lookup"><span data-stu-id="10326-890">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not an opaque resource.</span></span>
- <span data-ttu-id="10326-891">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-891">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-892">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-892">Allowed From</span></span>

<span data-ttu-id="10326-893">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-893">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-894">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-894">Example</span></span>

```c
/* Get the value of an opaque resource.  */
status = nx_lwm2m_client_resource_opaque_get(&resource, &opaque_ptr, &opaque_length);

/* If status is NX_SUCCESS, the value of opaque resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_opaque_set"></a><span data-ttu-id="10326-895">nx_lwm2m_client_resource_opaque_set</span><span class="sxs-lookup"><span data-stu-id="10326-895">nx_lwm2m_client_resource_opaque_set</span></span>

<span data-ttu-id="10326-896">Donuk bir kaynağın değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-896">Sets the value of an opaque Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-897">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-897">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_opaque_set(
    NX_LWM2M_CLIENT_RESOURCE *value, 
    VOID *opaque_ptr, 
    UINT opaque_length);
```

### <a name="description"></a><span data-ttu-id="10326-898">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-898">Description</span></span>

<span data-ttu-id="10326-899">Hizmet, donuk bir kaynağın değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-899">The service sets the value of an opaque Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-900">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-900">Parameters</span></span>

- <span data-ttu-id="10326-901">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-901">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-902">**opaque_ptr** Donuk verilerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-902">**opaque_ptr** Pointer to the opaque data.</span></span>
- <span data-ttu-id="10326-903">**opaque_length** Donuk verilerin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="10326-903">**opaque_length** Length of the opaque data.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-904">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-904">Return Values</span></span>

- <span data-ttu-id="10326-905">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-905">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-906">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-906">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-907">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-907">Allowed From</span></span>

<span data-ttu-id="10326-908">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-908">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-909">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-909">Example</span></span>

```c
/* Set the value of an opaque resource.  */
status = nx_lwm2m_client_resource_opaque_set(&resource, “AQIDBAU=”, 8);

/* If status is NX_SUCCESS, the value of opaque resource was successfully set. */
```

## <a name="nx_lwm2m_client_resource_string_get"></a><span data-ttu-id="10326-910">nx_lwm2m_client_resource_string_get</span><span class="sxs-lookup"><span data-stu-id="10326-910">nx_lwm2m_client_resource_string_get</span></span>

<span data-ttu-id="10326-911">Bir dize kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-911">Gets the value of a string Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-912">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-912">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_string_get(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    const CHAR **string_ptr, 
    UINT *string_length);
```

### <a name="description"></a><span data-ttu-id="10326-913">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-913">Description</span></span>

<span data-ttu-id="10326-914">Hizmet, bir dize kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="10326-914">The service retrieves the value of a string Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-915">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-915">Parameters</span></span>

- <span data-ttu-id="10326-916">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-916">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-917">**string_ptr** Hedef dize işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-917">**string_ptr** Pointer to the destination string pointer.</span></span>
- <span data-ttu-id="10326-918">**string_length** Hedef dize uzunluğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-918">**string_length** Pointer to the destination string length.</span></span> <span data-ttu-id="10326-919">Dize null sonlandırılırsa **null** olabilir.</span><span class="sxs-lookup"><span data-stu-id="10326-919">Can be **NULL** if the string is null-terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-920">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-920">Return Values</span></span>

- <span data-ttu-id="10326-921">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-921">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-922">**NX_LWM2M_CLIENT_BAD_ENCODING** Kaynak değeri bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="10326-922">**NX_LWM2M_CLIENT_BAD_ENCODING** The resource value is not a string value.</span></span>
- <span data-ttu-id="10326-923">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-923">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-924">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-924">Allowed From</span></span>

<span data-ttu-id="10326-925">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-925">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-926">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-926">Example</span></span>

```c
/* Get the value of a string resource.  */
status = nx_lwm2m_client_resource_string_get(&resource, &string_ptr, &string_length);

/* If status is NX_SUCCESS, the value of string resource was successfully get. */
```

## <a name="nx_lwm2m_client_resource_string_set"></a><span data-ttu-id="10326-927">nx_lwm2m_client_resource_string_set</span><span class="sxs-lookup"><span data-stu-id="10326-927">nx_lwm2m_client_resource_string_set</span></span>

<span data-ttu-id="10326-928">Bir dize kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-928">Sets the value of a string Resource.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-929">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-929">Prototype</span></span>

```c
UINT nx_lwm2m_client_resource_string_set(
    NX_LWM2M_CLIENT_RESOURCE *resource, 
    CHAR *string_ptr, 
    UINT string_length);
```

### <a name="description"></a><span data-ttu-id="10326-930">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-930">Description</span></span>

<span data-ttu-id="10326-931">Hizmet, 64 bitlik bir tamsayı kaynağının değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="10326-931">The service sets the value of a 64-Bit integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-932">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-932">Parameters</span></span>

- <span data-ttu-id="10326-933">**kaynak** Kaynak işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-933">**resource** Pointer to Resource.</span></span>
- <span data-ttu-id="10326-934">**string_ptr** Dize işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-934">**string_ptr** Pointer to the string.</span></span>
- <span data-ttu-id="10326-935">**string_length** Dizenin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="10326-935">**string_length** Length of the string.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-936">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-936">Return Values</span></span>

- <span data-ttu-id="10326-937">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-937">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-938">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-938">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-939">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-939">Allowed From</span></span>

<span data-ttu-id="10326-940">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-940">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-941">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-941">Example</span></span>

```c
/* Set the value of a string resource.  */
status = nx_lwm2m_client_resource_string_set(&resource, “test”, sizeof(“test”) - 1);

/* If status is NX_SUCCESS, the value of string resource was successfully set. */
```

## <a name="nx_lwm2m_client_session_bootstrap"></a><span data-ttu-id="10326-942">nx_lwm2m_client_session_bootstrap</span><span class="sxs-lookup"><span data-stu-id="10326-942">nx_lwm2m_client_session_bootstrap</span></span>

<span data-ttu-id="10326-943">Bir önyükleme sunucusu ile oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="10326-943">Starts a session with a Bootstrap Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-944">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-944">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_bootstrap(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID security_id, 
    ULONG ip_address, 
    UINT port);
```

### <a name="description"></a><span data-ttu-id="10326-945">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-945">Description</span></span>

<span data-ttu-id="10326-946">Bu hizmet, bir önyükleme sunucusu ile oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="10326-946">This service starts a session with a Bootstrap Server.</span></span> <span data-ttu-id="10326-947">Sunucu, güvenlik nesnesinde karşılık gelen bir güvenlik örneğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-947">The server should have a corresponding security instance in the Security Object.</span></span>

<span data-ttu-id="10326-948">' Kapalı ' kaynağı bu sunucuyla ilişkili güvenlik örneğinde sıfırdan farklıysa, bu süre sonunda Istemci tarafından başlatılan bir önyükleme yoksa, oturum sunucu tarafından başlatılan bir önyükleme için bekler.</span><span class="sxs-lookup"><span data-stu-id="10326-948">If the ‘Hold Off’ resource is different than zero in the Security Instance associated with this server the session will wait for a Server Initiated Bootstrap, If no bootstrap is initiated by the server after this period of time a Client Initiated Boostrap will be performed.</span></span>

<span data-ttu-id="10326-949">Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni önyükleme sunucusu oturumuyla değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="10326-949">Any current active session is aborted by this call and replaced by the new Bootstrap Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-950">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-950">Parameters</span></span>

- <span data-ttu-id="10326-951">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-951">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="10326-952">**security_id** Önyükleme sunucusunda tanımlı güvenlik örneği yoksa, önyükleme sunucusunun güvenlik örneği KIMLIĞI NX_LWM2M_RESERVED_ID (65535) olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-952">**security_id** The Security Instance ID of the Bootstrap Server, must be set to NX_LWM2M_RESERVED_ID (65535) if the Bootstrap Server has no Security Instance defined.</span></span>
- <span data-ttu-id="10326-953">**ip_address** Sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="10326-953">**ip_address** The IP address of the server.</span></span>
- <span data-ttu-id="10326-954">**bağlantı noktası** Sunucunun UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="10326-954">**port** The UDP port of the server.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-955">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-955">Return Values</span></span>

- <span data-ttu-id="10326-956">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-956">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-957">**NX_LWM2M_CLIENT_ERROR** Önyükleme hatası.</span><span class="sxs-lookup"><span data-stu-id="10326-957">**NX_LWM2M_CLIENT_ERROR** Bootstrap error.</span></span>
- <span data-ttu-id="10326-958">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="10326-958">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="10326-959">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-959">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-960">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-960">Allowed From</span></span>

<span data-ttu-id="10326-961">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-961">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-962">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-962">Example</span></span>

```c
/* Start bootstrap.  */
status = nx_lwm2m_client_session_bootstrap(&lwm2m_client, 0, &ip_address, 5783);

/* If status is NX_SUCCESS, start bootstrap successfully.  */
```

## <a name="nx_lwm2m_client_session_bootstrap_dtls"></a><span data-ttu-id="10326-963">nx_lwm2m_client_session_bootstrap_dtls</span><span class="sxs-lookup"><span data-stu-id="10326-963">nx_lwm2m_client_session_bootstrap_dtls</span></span>

<span data-ttu-id="10326-964">Bir önyükleme sunucusu ile güvenli bir oturum başlatır</span><span class="sxs-lookup"><span data-stu-id="10326-964">Starts a secure session with a Bootstrap Server</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-965">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-965">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_bootstrap_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID security_id, 
    ULONG ip_address, 
    UINT port, 
    NX_SECURE_DTLS_SESSION *dtls_session_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-966">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-966">Description</span></span>

<span data-ttu-id="10326-967">Bu hizmet, güvenli bir DTLS bağlantısı kullanarak önyükleme sunucusuyla bir oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="10326-967">This service start a session with a Bootstrap Server using a secure DTLS connection.</span></span> <span data-ttu-id="10326-968">Sunucu, güvenlik nesnesinde karşılık gelen bir güvenlik örneğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-968">The server should have a corresponding security instance in the Security Object.</span></span>

<span data-ttu-id="10326-969">DTLS oturumunun, bu işlev çağrılmadan önce uygun şifre paketleri ve anahtar malzemeyle yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="10326-969">The DTLS session must have been configured with the proper cipher suites and key material before calling this function.</span></span> <span data-ttu-id="10326-970">**NX_SECURE_ENABLE_DTLS** tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-970">**NX_SECURE_ENABLE_DTLS** must be defined.</span></span>

<span data-ttu-id="10326-971">' Kapalı ' kaynağı bu sunucuyla ilişkili güvenlik örneğinde sıfırdan farklıysa, bu süre sonunda Istemci tarafından başlatılan bir önyükleme yoksa, oturum sunucu tarafından başlatılan bir önyükleme için bekler.</span><span class="sxs-lookup"><span data-stu-id="10326-971">If the ‘Hold Off’ resource is different than zero in the Security Instance associated with this server the session will wait for a Server Initiated Bootstrap, if no bootstrap is initiated by the server after this period of time a Client Initiated Boostrap will be performed.</span></span> 

<span data-ttu-id="10326-972">Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni önyükleme sunucusu oturumuyla değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="10326-972">Any current active session is aborted by this call and replaced by the new Bootstrap Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-973">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-973">Parameters</span></span>

- <span data-ttu-id="10326-974">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-974">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="10326-975">**security_id** Önyükleme sunucusunda tanımlı güvenlik örneği yoksa, önyükleme sunucusunun güvenlik örneği KIMLIĞI **NX_LWM2M_RESERVED_ID** (65535) olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-975">**security_id** The Security Instance ID of the Bootstrap Server, must be set to **NX_LWM2M_RESERVED_ID** (65535) if the Bootstrap Server has no Security Instance defined.</span></span>
- <span data-ttu-id="10326-976">**ip_address** Sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="10326-976">**ip_address** The IP address of the server.</span></span>
- <span data-ttu-id="10326-977">**bağlantı noktası** Sunucunun UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="10326-977">**port** The UDP port of the server.</span></span>
- <span data-ttu-id="10326-978">**dtls_session_ptr** Önyükleme oturumu için kullanılacak DTLS oturumu.</span><span class="sxs-lookup"><span data-stu-id="10326-978">**dtls_session_ptr** The DTLS session to use for the Bootstrap session.</span></span>
- <span data-ttu-id="10326-979">**dtls_local_port** DTLS oturumu için kullanılan yerel UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="10326-979">**dtls_local_port** The local UDP port used for the DTLS session.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-980">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-980">Return Values</span></span>

- <span data-ttu-id="10326-981">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-981">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-982">**NX_LWM2M_CLIENT_ERROR** Önyükleme hatası.</span><span class="sxs-lookup"><span data-stu-id="10326-982">**NX_LWM2M_CLIENT_ERROR** Bootstrap error.</span></span>
- <span data-ttu-id="10326-983">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="10326-983">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="10326-984">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-984">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-985">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-985">Allowed From</span></span>

<span data-ttu-id="10326-986">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-986">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-987">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-987">Example</span></span>

```c
/* Start bootstrap with DTLS.  */
status = nx_lwm2m_client_session_bootstrap_dtls(&lwm2m_client, 0, &ip_address, 5784, &dtls_session);

/* If status is NX_SUCCESS, start bootstrap successfully.  */
```

## <a name="nx_lwm2m_client_session_create"></a><span data-ttu-id="10326-988">nx_lwm2m_client_session_create</span><span class="sxs-lookup"><span data-stu-id="10326-988">nx_lwm2m_client_session_create</span></span>

<span data-ttu-id="10326-989">Bir LWM2M Istemci oturumu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="10326-989">Creates a LWM2M Client Session.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-990">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-990">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_create(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK state_callback);
```

### <a name="description"></a><span data-ttu-id="10326-991">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-991">Description</span></span>

<span data-ttu-id="10326-992">Bu hizmet, var olan bir LWM2M Istemcisine bağlı yeni bir LWM2M Istemci oturumu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="10326-992">This service creates a new LWM2M Client Session attached to an existing LWM2M Client.</span></span> <span data-ttu-id="10326-993">Oturum, bir önyükleme sunucusuyla veya bir LWM2M sunucusuyla iletişim kurmak için LWM2M Istemcisi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10326-993">The session is used by the LWM2M Client to communicate with a Bootstrap Server or a LWM2M Server.</span></span> 

<span data-ttu-id="10326-994">Uygulama, oturumun durumu güncellendiği zaman çağrılacak bir geri çağırma işlevi sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-994">The application must provide a callback function that will be called when the state of the session is updated.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-995">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-995">Parameters</span></span>

- <span data-ttu-id="10326-996">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-996">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="10326-997">**client_ptr** Daha önce oluşturulan LWM2M Istemcisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-997">**client_ptr** Pointer to the previously created LWM2M Client.</span></span>
- <span data-ttu-id="10326-998">**state_callback** Oturumun durumu değiştiğinde çağrılan uygulama geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="10326-998">**state_callback** Application callback that is called when the state of the session has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-999">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-999">Return Values</span></span>

- <span data-ttu-id="10326-1000">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-1000">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-1001">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-1001">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-1002">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-1002">Allowed From</span></span>

<span data-ttu-id="10326-1003">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-1003">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-1004">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-1004">Example</span></span>

```c
/* Create session.  */
status = nx_lwm2m_client_session_create(&session, &lwm2m_client, session_callback);

/* If status is NX_SUCCESS, a session was successfully created.  */
```

## <a name="nx_lwm2m_client_session_delete"></a><span data-ttu-id="10326-1005">nx_lwm2m_client_session_delete</span><span class="sxs-lookup"><span data-stu-id="10326-1005">nx_lwm2m_client_session_delete</span></span>

<span data-ttu-id="10326-1006">Bir LWM2M Istemci oturumunu siler.</span><span class="sxs-lookup"><span data-stu-id="10326-1006">Deletes a LWM2M Client Session.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-1007">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-1007">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_delete(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-1008">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-1008">Description</span></span>

<span data-ttu-id="10326-1009">Bu hizmet bir LWM2M Istemci oturumunu siler.</span><span class="sxs-lookup"><span data-stu-id="10326-1009">This service deletes a LWM2M Client Session.</span></span>

<span data-ttu-id="10326-1010">Nx_lwm2m_client_delete çağırarak bir LWM2M Istemcisi silindiğinde, istemciye bağlı tüm oturumlar da silinir.</span><span class="sxs-lookup"><span data-stu-id="10326-1010">When a LWM2M Client is deleted by calling nx_lwm2m_client_delete all sessions attached to the client are also deleted.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-1011">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-1011">Parameters</span></span>

- <span data-ttu-id="10326-1012">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1012">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-1013">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-1013">Return Values</span></span>

- <span data-ttu-id="10326-1014">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-1014">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-1015">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-1015">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-1016">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-1016">Allowed From</span></span>

<span data-ttu-id="10326-1017">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-1017">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-1018">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-1018">Example</span></span>

```c
/* Delete session.  */
status = nx_lwm2m_client_session_delete(&session);

/* If status is NX_SUCCESS, a session was successfully deleted.  */
```

## <a name="nx_lwm2m_client_session_deregister"></a><span data-ttu-id="10326-1019">nx_lwm2m_client_session_deregister</span><span class="sxs-lookup"><span data-stu-id="10326-1019">nx_lwm2m_client_session_deregister</span></span>

<span data-ttu-id="10326-1020">Bir LWM2M sunucusuyla oturumu sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="10326-1020">Terminates a session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-1021">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-1021">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_deregister(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-1022">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-1022">Description</span></span>

<span data-ttu-id="10326-1023">Bu hizmet bir LWM2M sunucusuna ' de Register ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-1023">This service performs a ‘De-Register’ operation to a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-1024">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-1024">Parameters</span></span>

- <span data-ttu-id="10326-1025">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1025">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-1026">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-1026">Return Values</span></span>

- <span data-ttu-id="10326-1027">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-1027">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-1028">**NX_LWM2M_CLIENT_NOT_REGISTERED** İstemci sunucuya kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="10326-1028">**NX_LWM2M_CLIENT_NOT_REGISTERED** The client is not registered to the server.</span></span>
- <span data-ttu-id="10326-1029">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-1029">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-1030">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-1030">Allowed From</span></span>

<span data-ttu-id="10326-1031">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-1031">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-1032">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-1032">Example</span></span>

```c
/* De-register session.  */
status = nx_lwm2m_client_session_deregister(&session);

/* If status is NX_SUCCESS, session was successfully de-registered.  */
```

## <a name="nx_lwm2m_client_session_error_get"></a><span data-ttu-id="10326-1033">nx_lwm2m_client_session_error_get</span><span class="sxs-lookup"><span data-stu-id="10326-1033">nx_lwm2m_client_session_error_get</span></span>

<span data-ttu-id="10326-1034">Bir oturumun son hatasını alır.</span><span class="sxs-lookup"><span data-stu-id="10326-1034">Gets the last error of a session.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-1035">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-1035">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_error_get(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-1036">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-1036">Description</span></span>

<span data-ttu-id="10326-1037">Bu hizmet, oturum bir hata durumundayken oturumun hata kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="10326-1037">This service returns the error code of the session when the session is in an error state.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-1038">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-1038">Parameters</span></span>

- <span data-ttu-id="10326-1039">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1039">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-1040">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-1040">Return Values</span></span>

- <span data-ttu-id="10326-1041">**NX_SUCCESS** Oturum hata durumunda değil.</span><span class="sxs-lookup"><span data-stu-id="10326-1041">**NX_SUCCESS** The session is not in error state.</span></span>
- <span data-ttu-id="10326-1042">**NX_LWM2M_CLIENT_ADDRESS_ERROR** Geçersiz sunucu adresi.</span><span class="sxs-lookup"><span data-stu-id="10326-1042">**NX_LWM2M_CLIENT_ADDRESS_ERROR** Invalid server address.</span></span>
- <span data-ttu-id="10326-1043">**NX_LWM2M_ CLIENT_BUFFER_TOO_SMALL** İsteğin yükü ağ arabelleğine uymuyor.</span><span class="sxs-lookup"><span data-stu-id="10326-1043">**NX_LWM2M_ CLIENT_BUFFER_TOO_SMALL** Payload of request doesn’t fit in network buffer.</span></span>
- <span data-ttu-id="10326-1044">**NX_LWM2M_ CLIENT_DTLS_ERROR** Sunucuyla güvenli bağlantı kurulamadı.</span><span class="sxs-lookup"><span data-stu-id="10326-1044">**NX_LWM2M_ CLIENT_DTLS_ERROR** Failed to establish secured connection with server.</span></span>
- <span data-ttu-id="10326-1045">**NX_LWM2M_ CLIENT_ERROR** Belirtilmeyen hata.</span><span class="sxs-lookup"><span data-stu-id="10326-1045">**NX_LWM2M_ CLIENT_ERROR** Unspecified error.</span></span>
- <span data-ttu-id="10326-1046">**NX_LWM2M_ CLIENT_FORBIDDEN** Kayıt sunucu tarafından reddedildi.</span><span class="sxs-lookup"><span data-stu-id="10326-1046">**NX_LWM2M_ CLIENT_FORBIDDEN** Registration refused by server.</span></span>
- <span data-ttu-id="10326-1047">**NX_LWM2M_ CLIENT_NOT_FOUND** Güncelleştirme/kaydını kaldırmak, istemci sunucu tarafından bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="10326-1047">**NX_LWM2M_ CLIENT_NOT_FOUND** Client not found by server when updating/deregistering.</span></span>
- <span data-ttu-id="10326-1048">**NX_LWM2M_ CLIENT_SERVER_INSTANCE_DELETED** Oturuma karşılık gelen sunucu nesnesi örneği silindi.</span><span class="sxs-lookup"><span data-stu-id="10326-1048">**NX_LWM2M_ CLIENT_SERVER_INSTANCE_DELETED** The Server Object Instance corresponding to the session has been deleted.</span></span>
- <span data-ttu-id="10326-1049">**NX_LWM2M_ CLIENT_TIMED_OUT** Sunucudan yanıt yok.</span><span class="sxs-lookup"><span data-stu-id="10326-1049">**NX_LWM2M_ CLIENT_TIMED_OUT** No answer from server.</span></span>
- <span data-ttu-id="10326-1050">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-1050">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-1051">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-1051">Allowed From</span></span>

<span data-ttu-id="10326-1052">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-1052">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-1053">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-1053">Example</span></span>

```c
/* Get the error.  */
status = nx_lwm2m_client_session_error_get(&session);
```
## <a name="nx_lwm2m_client_session_register"></a><span data-ttu-id="10326-1054">nx_lwm2m_client_session_register</span><span class="sxs-lookup"><span data-stu-id="10326-1054">nx_lwm2m_client_session_register</span></span>

<span data-ttu-id="10326-1055">Bir LWM2M sunucusuyla oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="10326-1055">Starts a session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-1056">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-1056">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID server_id, 
    ULONG ip_address, 
    UINT port);
```


### <a name="description"></a><span data-ttu-id="10326-1057">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-1057">Description</span></span>

<span data-ttu-id="10326-1058">Bu hizmet bir LWM2M sunucusuna ' Register ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-1058">This service performs a ‘Register’ operation to a LWM2M Server.</span></span> <span data-ttu-id="10326-1059">Sunucu, sunucu nesnesinde karşılık gelen bir sunucu örneğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-1059">The server must have a corresponding server instance in the Server Object.</span></span>

<span data-ttu-id="10326-1060">Kayıt başarılı bir şekilde LWM2M Istemcisi, sunucudan daha fazla işlem gerçekleştirir ve istemci kayıtlı olana kadar düzenli olarak ' güncelleştirme ' iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="10326-1060">If the registration is successfully the LWM2M Client will process further operations from the server and will periodically send ‘Update’ messages until the client is de-registered.</span></span>

<span data-ttu-id="10326-1061">Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni LWM2M Server oturumu tarafından değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="10326-1061">Any current active session is aborted by this call and replaced by the new LWM2M Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-1062">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-1062">Parameters</span></span>

- <span data-ttu-id="10326-1063">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1063">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="10326-1064">**server_id** LWM2M sunucusunun kısa sunucu KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-1064">**server_id** The Short Server ID of the LWM2M Server.</span></span>
- <span data-ttu-id="10326-1065">**ip_address** Sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="10326-1065">**ip_address** The IP address of the server.</span></span>
- <span data-ttu-id="10326-1066">**bağlantı noktası** Sunucunun UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="10326-1066">**port** The UDP port of the server.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-1067">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-1067">Return Values</span></span>

- <span data-ttu-id="10326-1068">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-1068">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-1069">**NX_LWM2M_CLIENT_ERROR** Önyükleme hatası.</span><span class="sxs-lookup"><span data-stu-id="10326-1069">**NX_LWM2M_CLIENT_ERROR** Bootstrap error.</span></span>
- <span data-ttu-id="10326-1070">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="10326-1070">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="10326-1071">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-1071">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-1072">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-1072">Allowed From</span></span>

<span data-ttu-id="10326-1073">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-1073">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-1074">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-1074">Example</span></span>

```c
/* Start register.  */
status = nx_lwm2m_client_session_register (&lwm2m_client, 123, &ip_address, 5683);

/* If status is NX_SUCCESS, start register successfully.  */
```

## <a name="nx_lwm2m_client_session_register_dtls"></a><span data-ttu-id="10326-1075">nx_lwm2m_client_session_register_dtls</span><span class="sxs-lookup"><span data-stu-id="10326-1075">nx_lwm2m_client_session_register_dtls</span></span>

<span data-ttu-id="10326-1076">LWM2M sunucusu ile güvenli bir oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="10326-1076">Starts a secure session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-1077">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-1077">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    NX_LWM2M_ID server_id, 
    ULONG ip_address, 
    UINT port,
    NX_SECURE_DTLS_SESSION *dtls_session_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-1078">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-1078">Description</span></span>

<span data-ttu-id="10326-1079">Bu hizmet, güvenli bir DTLS bağlantısı kullanarak bir LWM2M sunucusuna ' Register ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-1079">This service performs a ‘Register’ operation to a LWM2M Server using a secure DTLS connection.</span></span> <span data-ttu-id="10326-1080">Sunucu, sunucu nesnesinde karşılık gelen bir sunucu örneğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-1080">The server must have a corresponding server instance in the Server Object.</span></span>

<span data-ttu-id="10326-1081">DTLS oturumunun, bu işlev çağrılmadan önce uygun şifre paketleri ve anahtar malzemeyle yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="10326-1081">The DTLS session must have been configured with the proper cipher suites and key material before calling this function.</span></span> <span data-ttu-id="10326-1082">**NX_SECURE_ENABLE_DTLS** tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10326-1082">**NX_SECURE_ENABLE_DTLS** must be defined.</span></span>

<span data-ttu-id="10326-1083">Kayıt başarılı bir şekilde LWM2M Istemcisi, sunucudan daha fazla işlem gerçekleştirir ve istemci kayıtlı olana kadar düzenli olarak ' güncelleştirme ' iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="10326-1083">If the registration is successfully the LWM2M Client will process further operations from the server and will periodically send ‘Update’ messages until the client is de-registered.</span></span>

<span data-ttu-id="10326-1084">Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni LWM2M Server oturumu tarafından değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="10326-1084">Any current active session is aborted by this call and replaced by the new LWM2M Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-1085">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-1085">Parameters</span></span>

- <span data-ttu-id="10326-1086">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1086">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="10326-1087">**server_id** LWM2M sunucusunun kısa sunucu KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-1087">**server_id** The Short Server ID of the LWM2M Server.</span></span>
- <span data-ttu-id="10326-1088">**ip_address** Sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="10326-1088">**ip_address** The IP address of the server.</span></span>
- <span data-ttu-id="10326-1089">**bağlantı noktası** Sunucunun UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="10326-1089">**port** The UDP port of the server.</span></span>
- <span data-ttu-id="10326-1090">**dtls_session_ptr** LWM2M oturumu için kullanılacak DTLS oturumu.</span><span class="sxs-lookup"><span data-stu-id="10326-1090">**dtls_session_ptr** The DTLS session to use for the LWM2M session.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-1091">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-1091">Return Values</span></span>

- <span data-ttu-id="10326-1092">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-1092">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-1093">**NX_LWM2M_CLIENT_ERROR** Önyükleme hatası.</span><span class="sxs-lookup"><span data-stu-id="10326-1093">**NX_LWM2M_CLIENT_ERROR** Bootstrap error.</span></span>
- <span data-ttu-id="10326-1094">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Bağlantı noktası kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="10326-1094">**NX_LWM2M_CLIENT_PORT_UNAVAILABLE** Port is unavailable.</span></span>
- <span data-ttu-id="10326-1095">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-1095">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-1096">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-1096">Allowed From</span></span>

<span data-ttu-id="10326-1097">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-1097">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-1098">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-1098">Example</span></span>

```c
/* Start register with DTLS.  */
status = nx_lwm2m_client_session_register_dtls(&lwm2m_client, 123, &ip_address, 5683, &dtls_session);

/* If status is NX_SUCCESS, start register with DTLS successfully.  */
```

## <a name="nx_lwm2m_client_session_register_info_get"></a><span data-ttu-id="10326-1099">nx_lwm2m_client_session_register_info_get</span><span class="sxs-lookup"><span data-stu-id="10326-1099">nx_lwm2m_client_session_register_info_get</span></span>

<span data-ttu-id="10326-1100">LWM2M sunucusu ile güvenli bir oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="10326-1100">Starts a secure session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-1101">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-1101">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register_dtls(
    NX_LWM2M_CLIENT_SESSION *session_ptr, 
    UINT security_instance_id, 
    NX_LWM2M_ID *server_id,
    CHAR **server_uri, 
    UINT *server_uri_length, 
    UCHAR *security_mode, 
    UCHAR **pub_key_or_id, 
    UINT *pub_key_or_id_len, 
    UCHAR **server_pub_key, 
    UINT *server_pub_key_len, 
    UCHAR **secret_key, 
    UINT *secret_key_len);
```

### <a name="description"></a><span data-ttu-id="10326-1102">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-1102">Description</span></span>

<span data-ttu-id="10326-1103">Bir önyükleme sunucusuyla iletişim oturumu kurulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="10326-1103">Once a communication session with a Bootstrap server was established.</span></span> <span data-ttu-id="10326-1104">Uygulama, sonraki kayıt adımı için sunucu ve güvenlik bilgilerini almak üzere bu API 'yi çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="10326-1104">Application can call this api to get the server and security information for the next registration step.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-1105">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-1105">Parameters</span></span>

- <span data-ttu-id="10326-1106">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1106">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="10326-1107">**security_instance_id** Güvenlik örneği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="10326-1107">**security_instance_id** Security instance ID.</span></span>
- <span data-ttu-id="10326-1108">**server_id** Hedef sunucu KIMLIĞI işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1108">**server_id** Pointer to destination server ID.</span></span>
- <span data-ttu-id="10326-1109">**server_uri** Hedef sunucu URI 'si işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1109">**server_uri** Pointer to destination server uri.</span></span>
- <span data-ttu-id="10326-1110">**server_uri_len** Hedef sunucu URI uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1110">**server_uri_len** Pointer to destination server uri length.</span></span>
- <span data-ttu-id="10326-1111">**security_mode** Hedef güvenlik modu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1111">**security_mode** Pointer to destination security mode.</span></span>
- <span data-ttu-id="10326-1112">**pub_key_or_id** Hedef ortak anahtar veya kimlik işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1112">**pub_key_or_id** Pointer to destination public key or identity.</span></span>
- <span data-ttu-id="10326-1113">**pub_key_or_id_len** Hedef ortak anahtar veya kimlik uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1113">**pub_key_or_id_len** Pointer to destination public key or identity length.</span></span>
- <span data-ttu-id="10326-1114">**server_pub_key** Hedef sunucu ortak anahtarı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1114">**server_pub_key** Pointer to destination server public key.</span></span>
- <span data-ttu-id="10326-1115">**server_pub_key_len** Hedef sunucu ortak anahtar uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1115">**server_pub_key_len** Pointer to destination server public key length.</span></span>
- <span data-ttu-id="10326-1116">**secret_key** Hedef gizli anahtar işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1116">**secret_key** Pointer to destination secret key.</span></span>
- <span data-ttu-id="10326-1117">**secret_key_len** Hedef gizli anahtar uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1117">**secret_key_len** Pointer to destination secret key length.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-1118">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-1118">Return Values</span></span>

- <span data-ttu-id="10326-1119">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-1119">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-1120">**NX_LWM2M_CLIENT_NOT_FOUND** Güvenlik nesnesi örneği yok.</span><span class="sxs-lookup"><span data-stu-id="10326-1120">**NX_LWM2M_CLIENT_NOT_FOUND** There is no security Object instance.</span></span>
- <span data-ttu-id="10326-1121">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-1121">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-1122">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-1122">Allowed From</span></span>

<span data-ttu-id="10326-1123">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-1123">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-1124">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-1124">Example</span></span>

```c
/* Get the register information.  */
status = nx_lwm2m_client_session_register_info_get(&session, NX_LWM2M_CLIENT_RESERVED_ID, &server_id, &server_uri, &server_uri_length, &security_mode, &pub_key_or_id, &pub_key_or_id_len, NX_NULL, NX_NULL, &secret_key, &secret_key_len);

/* If status is NX_SUCCESS, the register information was successfully gotten.  */
```

## <a name="nx_lwm2m_client_session_update"></a><span data-ttu-id="10326-1125">nx_lwm2m_client_session_update</span><span class="sxs-lookup"><span data-stu-id="10326-1125">nx_lwm2m_client_session_update</span></span>

<span data-ttu-id="10326-1126">Bir oturumu LWM2M sunucusu ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-1126">Updates a session with a LWM2M Server.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-1127">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-1127">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-1128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-1128">Description</span></span>

<span data-ttu-id="10326-1129">Bu hizmet bir LWM2M sunucusuna ' Update ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="10326-1129">This service performs an ‘Update’ operation to a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-1130">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-1130">Parameters</span></span>

- <span data-ttu-id="10326-1131">**session_ptr** LWM2M Istemci oturumu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1131">**session_ptr** Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-1132">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-1132">Return Values</span></span>

- <span data-ttu-id="10326-1133">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-1133">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-1134">**NX_LWM2M_CLIENT_NOT_REGISTERED** İstemci sunucuya kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="10326-1134">**NX_LWM2M_CLIENT_NOT_REGISTERED** The client is not registered to the server.</span></span>
- <span data-ttu-id="10326-1135">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-1135">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-1136">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-1136">Allowed From</span></span>

<span data-ttu-id="10326-1137">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-1137">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-1138">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-1138">Example</span></span>

```c
/* Update a session.  */
status = nx_lwm2m_client_session_update(&session);

/* If status is NX_SUCCESS, a session was successfully updated.  */
```

## <a name="nx_lwm2m_client_unlock"></a><span data-ttu-id="10326-1139">nx_lwm2m_client_unlock</span><span class="sxs-lookup"><span data-stu-id="10326-1139">nx_lwm2m_client_unlock</span></span>

<span data-ttu-id="10326-1140">Bir LWM2M Istemcisinin kilidini açar.</span><span class="sxs-lookup"><span data-stu-id="10326-1140">Unlocks a LWM2M Client.</span></span>

### <a name="prototype"></a><span data-ttu-id="10326-1141">Prototype</span><span class="sxs-lookup"><span data-stu-id="10326-1141">Prototype</span></span>

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="10326-1142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10326-1142">Description</span></span>

<span data-ttu-id="10326-1143">Bu hizmet, daha önce bir ***nx_lwm2m_client_unlock*** ÇAĞRıSıYLA kilitlenen LWM2M istemcisinin kilidini açar.</span><span class="sxs-lookup"><span data-stu-id="10326-1143">This service unlocks the LWM2M Client previously locked by a call to ***nx_lwm2m_client_unlock***.</span></span>

### <a name="parameters"></a><span data-ttu-id="10326-1144">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10326-1144">Parameters</span></span>

- <span data-ttu-id="10326-1145">**client_ptr** LWM2M Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="10326-1145">**client_ptr** Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="10326-1146">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="10326-1146">Return Values</span></span>

- <span data-ttu-id="10326-1147">**NX_SUCCESS** İşlem başarılı.</span><span class="sxs-lookup"><span data-stu-id="10326-1147">**NX_SUCCESS** Successful operation.</span></span>
- <span data-ttu-id="10326-1148">**NX_PTR_ERROR** Geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="10326-1148">**NX_PTR_ERROR** Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="10326-1149">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="10326-1149">Allowed From</span></span>

<span data-ttu-id="10326-1150">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="10326-1150">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="10326-1151">Örnek</span><span class="sxs-lookup"><span data-stu-id="10326-1151">Example</span></span>

```c
/* Unlock lwm2m client.  */
status = nx_lwm2m_client_unlock(&lwm2m_client);

/* If status is NX_SUCCESS, unlock lwm2m client successfully.  */
```