---
title: Bölüm 4-Azure RTOS NetX LWM2M Services açıklaması
description: Bu bölüm, tüm Azure RTOS NetX LWM2M hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d5a402790387c2720db304fe93d74252494d7638
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826674"
---
# <a name="chapter-4---description-of-azure-rtos-netx-lwm2m-services"></a><span data-ttu-id="1e11e-103">Bölüm 4-Azure RTOS NetX LWM2M Services açıklaması</span><span class="sxs-lookup"><span data-stu-id="1e11e-103">Chapter 4 - Description of Azure RTOS NetX LWM2M services</span></span>

<span data-ttu-id="1e11e-104">Bu bölüm, tüm Azure RTOS NetX LWM2M hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-104">This chapter contains a description of all Azure RTOS NetX LWM2M services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="1e11e-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

### <a name="lwm2m-client-management"></a><span data-ttu-id="1e11e-106">LWM2M Istemci yönetimi</span><span class="sxs-lookup"><span data-stu-id="1e11e-106">LWM2M Client Management</span></span>

- <span data-ttu-id="1e11e-107">**nx_lwm2m_client_create**: *lwm2m istemcisi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="1e11e-107">**nx_lwm2m_client_create**: *Create LWM2M Client*</span></span>
- <span data-ttu-id="1e11e-108">**nx_lwm2m_client_delete**: *lwm2m istemcisini Sil*</span><span class="sxs-lookup"><span data-stu-id="1e11e-108">**nx_lwm2m_client_delete**: *Delete LWM2M Client*</span></span>
- <span data-ttu-id="1e11e-109">**nx_lwm2m_client_lock**: *lwm2m istemcisini kilitle*</span><span class="sxs-lookup"><span data-stu-id="1e11e-109">**nx_lwm2m_client_lock**: *Lock LWM2M Client*</span></span>
- <span data-ttu-id="1e11e-110">**nx_lwm2m_client_object_add**: *lwm2m istemcisine nesne uygulamasını ekleme*</span><span class="sxs-lookup"><span data-stu-id="1e11e-110">**nx_lwm2m_client_object_add**: *Add Object implementation to the LWM2M Client*</span></span>
- <span data-ttu-id="1e11e-111">**nx_lwm2m_client_unlock**: *lwm2m istemcisinin kilidini aç*</span><span class="sxs-lookup"><span data-stu-id="1e11e-111">**nx_lwm2m_client_unlock**: *Unlock LWM2M Client*</span></span>

### <a name="lwm2m-client-session-management"></a><span data-ttu-id="1e11e-112">LWM2M Istemci oturumu yönetimi</span><span class="sxs-lookup"><span data-stu-id="1e11e-112">LWM2M Client Session Management</span></span>

- <span data-ttu-id="1e11e-113">**nx_lwm2m_client_session_bootstrap**: *bir önyükleme sunucusu ile oturum başlatma*</span><span class="sxs-lookup"><span data-stu-id="1e11e-113">**nx_lwm2m_client_session_bootstrap**: *Start a session with a Bootstrap Server*</span></span>
- <span data-ttu-id="1e11e-114">**nx_lwm2m_client_session_bootstrap_dtls**: *bir önyükleme sunucusu ile güvenli bir oturum başlatma*</span><span class="sxs-lookup"><span data-stu-id="1e11e-114">**nx_lwm2m_client_session_bootstrap_dtls**: *Start a secure session with a Bootstrap Server*</span></span>
- <span data-ttu-id="1e11e-115">**nx_lwm2m_client_session_create**: *lwm2m istemci oturumu oluştur*</span><span class="sxs-lookup"><span data-stu-id="1e11e-115">**nx_lwm2m_client_session_create**: *Create LWM2M Client Session*</span></span>
- <span data-ttu-id="1e11e-116">**nx_lwm2m_client_session_delete**: *lwm2m istemci oturumunu Sil*</span><span class="sxs-lookup"><span data-stu-id="1e11e-116">**nx_lwm2m_client_session_delete**: *Delete LWM2M Client Session*</span></span>
- <span data-ttu-id="1e11e-117">**nx_lwm2m_client_session_deregister**: BIR *oturumu lwm2m sunucusu ile sonlandırma*</span><span class="sxs-lookup"><span data-stu-id="1e11e-117">**nx_lwm2m_client_session_deregister**: *Terminate a session with a LWM2M Server*</span></span>
- <span data-ttu-id="1e11e-118">**nx_lwm2m_client_session_error_get**: *bir oturumun son hatasını al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-118">**nx_lwm2m_client_session_error_get**: *Get last error of a session*</span></span>
- <span data-ttu-id="1e11e-119">**nx_lwm2m_client_session_register**: *lwm2m sunucusu ile oturum başlatma*</span><span class="sxs-lookup"><span data-stu-id="1e11e-119">**nx_lwm2m_client_session_register**: *Start a session with a LWM2M Server*</span></span>
- <span data-ttu-id="1e11e-120">**nx_lwm2m_client_session_register_dtls**: *lwm2m sunucusu ile güvenli bir oturum başlatma*</span><span class="sxs-lookup"><span data-stu-id="1e11e-120">**nx_lwm2m_client_session_register_dtls**: *Start a secure session with a LWM2M Server*</span></span>
- <span data-ttu-id="1e11e-121">**nx_lwm2m_client_session_update**: *bir oturumu lwm2m sunucusuyla güncelleştirme*</span><span class="sxs-lookup"><span data-stu-id="1e11e-121">**nx_lwm2m_client_session_update**: *Update a session with a LWM2M Server*</span></span>

### <a name="security-object-implementation"></a><span data-ttu-id="1e11e-122">Güvenlik nesnesi uygulama</span><span class="sxs-lookup"><span data-stu-id="1e11e-122">Security Object Implementation</span></span>

- <span data-ttu-id="1e11e-123">**nx_lwm2m_client_security_key_callbacks_set**: *güvenlik anahtarı yönetimi geri çağırmaları ayarla*</span><span class="sxs-lookup"><span data-stu-id="1e11e-123">**nx_lwm2m_client_security_key_callbacks_set**: *Set security key management callbacks*</span></span>

### <a name="device-object-implementation"></a><span data-ttu-id="1e11e-124">Cihaz nesnesi uygulama</span><span class="sxs-lookup"><span data-stu-id="1e11e-124">Device Object Implementation</span></span>

- <span data-ttu-id="1e11e-125">**nx_lwm2m_client_device_callbacks_set**: *cihaz nesnesi uygulama geri çağırmaları ayarla*</span><span class="sxs-lookup"><span data-stu-id="1e11e-125">**nx_lwm2m_client_device_callbacks_set**: *Set Device Object application callbacks*</span></span>
- <span data-ttu-id="1e11e-126">**nx_lwm2m_client_device_error_push**: *cihaz nesnesine hata kodu ekleyin*</span><span class="sxs-lookup"><span data-stu-id="1e11e-126">**nx_lwm2m_client_device_error_push**: *Add error code to Device Object*</span></span>
- <span data-ttu-id="1e11e-127">**nx_lwm2m_client_device_error_reset**: *cihaz nesnesinin hata kodlarını sıfırlayın*</span><span class="sxs-lookup"><span data-stu-id="1e11e-127">**nx_lwm2m_client_device_error_reset**: *Reset error codes of Device Object*</span></span>
- <span data-ttu-id="1e11e-128">**nx_lwm2m_client_device_resource_changed**: *cihaz nesne kaynağının sinyal değişikliği*</span><span class="sxs-lookup"><span data-stu-id="1e11e-128">**nx_lwm2m_client_device_resource_changed**: *Signal change of Device Object resource*</span></span>

### <a name="custom-objects-implementation"></a><span data-ttu-id="1e11e-129">Özel nesne uygulamaları</span><span class="sxs-lookup"><span data-stu-id="1e11e-129">Custom Objects Implementation</span></span>

- <span data-ttu-id="1e11e-130">**nx_lwm2m_object_resource_changed**: bir *nesne örneğinin kaynak değeri için sinyal değişikliği*</span><span class="sxs-lookup"><span data-stu-id="1e11e-130">**nx_lwm2m_object_resource_changed**: *Signal change of a resource value of an Object Instance*</span></span>

### <a name="local-device-management"></a><span data-ttu-id="1e11e-131">Yerel cihaz yönetimi</span><span class="sxs-lookup"><span data-stu-id="1e11e-131">Local Device Management</span></span>

- <span data-ttu-id="1e11e-132">**nx_lwm2m_client_object_create**: *Yeni bir nesne örneği oluştur*</span><span class="sxs-lookup"><span data-stu-id="1e11e-132">**nx_lwm2m_client_object_create**: *Create a new Object Instance*</span></span>
- <span data-ttu-id="1e11e-133">**nx_lwm2m_client_object_delete**: *bir nesne örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="1e11e-133">**nx_lwm2m_client_object_delete**: *Delete an Object Instance*</span></span>
- <span data-ttu-id="1e11e-134">**nx_lwm2m_client_object_discover**: *bir nesne örneğinin kaynaklarını bulma*</span><span class="sxs-lookup"><span data-stu-id="1e11e-134">**nx_lwm2m_client_object_discover**: *Discover resources of an Object Instance*</span></span>
- <span data-ttu-id="1e11e-135">**nx_lwm2m_client_object_execute**: *bir nesne örneğinin kaynağını yürütün*</span><span class="sxs-lookup"><span data-stu-id="1e11e-135">**nx_lwm2m_client_object_execute**: *Execute resource of an Object Instance*</span></span>
- <span data-ttu-id="1e11e-136">**nx_lwm2m_client_object_get_next**: *lwm2m Istemcisi tarafından uygulanan nesne listesini al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-136">**nx_lwm2m_client_object_get_next**: *Get the list of Objects implemented by the LWM2M Client*</span></span>
- <span data-ttu-id="1e11e-137">**nx_lwm2m_client_object_instance_get_next**: *bir nesnenin örneklerinin listesini al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-137">**nx_lwm2m_client_object_instance_get_next**: *Get the list of Instances of an Object*</span></span>
- <span data-ttu-id="1e11e-138">**nx_lwm2m_client_object_read**: *bir nesne örneğinin kaynak değerlerini oku*</span><span class="sxs-lookup"><span data-stu-id="1e11e-138">**nx_lwm2m_client_object_read**: *Read resources values of an Object Instance*</span></span>
- <span data-ttu-id="1e11e-139">**nx_lwm2m_client_object_write**: *bir nesne örneğinin kaynak değerlerini değiştirme*</span><span class="sxs-lookup"><span data-stu-id="1e11e-139">**nx_lwm2m_client_object_write**: *Change resources values of an Object instance*</span></span>

### <a name="resources-values-decoding"></a><span data-ttu-id="1e11e-140">Kaynak değerlerinin kodunu çözme</span><span class="sxs-lookup"><span data-stu-id="1e11e-140">Resources Values Decoding</span></span>

- <span data-ttu-id="1e11e-141">**nx_lwm2m_resource_get_boolean**: *bir Boole kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-141">**nx_lwm2m_resource_get_boolean**: *Get the value of a Boolean Resource*</span></span>
- <span data-ttu-id="1e11e-142">**nx_lwm2m_resource_get_float32**: *32 bitlik kayan nokta kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-142">**nx_lwm2m_resource_get_float32**: *Get the value of a 32-bit Floating Point Resource*</span></span>
- <span data-ttu-id="1e11e-143">**nx_lwm2m_resource_get_float64**: *64 bitlik kayan nokta kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-143">**nx_lwm2m_resource_get_float64**: *Get the value of a 64-bit Floating Point Resource*</span></span>
- <span data-ttu-id="1e11e-144">**nx_lwm2m_resource_get_integer32**: *32 bitlik bir tamsayı kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-144">**nx_lwm2m_resource_get_integer32**: *Get the value of a 32-Bit Integer Resource*</span></span>
- <span data-ttu-id="1e11e-145">**nx_lwm2m_resource_get_integer64**: *64 bitlik bir tamsayı kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-145">**nx_lwm2m_resource_get_integer64**: *Get the value of a 64-Bit Integer Resource*</span></span>
- <span data-ttu-id="1e11e-146">**nx_lwm2m_resource_get_objlnk**: *nesne bağlantı kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-146">**nx_lwm2m_resource_get_objlnk**: *Get the value of an Object Link Resource*</span></span>
- <span data-ttu-id="1e11e-147">**nx_lwm2m_resource_get_opaque**: *donuk bir kaynağın değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-147">**nx_lwm2m_resource_get_opaque**: *Get the value of an Opaque Resource*</span></span>
- <span data-ttu-id="1e11e-148">**nx_lwm2m_resource_get_string**: *bir dize kaynağının değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-148">**nx_lwm2m_resource_get_string**: *Get the value of a String Resource*</span></span>
- <span data-ttu-id="1e11e-149">**nx_lwm2m_resource_multiple_get_boolean**: *bir Boole kaynağı birden çok kaynak örneği değeri alın*</span><span class="sxs-lookup"><span data-stu-id="1e11e-149">**nx_lwm2m_resource_multiple_get_boolean**: *Get the value of a Boolean Resource Multiple Resource Instance*</span></span>
- <span data-ttu-id="1e11e-150">**nx_lwm2m_resource_multiple_get_float32**: *32 bitlik kayan nokta çoklu kaynak örneği değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-150">**nx_lwm2m_resource_multiple_get_float32**: *Get the value of a 32-bit Floating Point Multiple Resource Instance*</span></span>
- <span data-ttu-id="1e11e-151">**nx_lwm2m_resource_multiple_get_float64**: *64 bitlik kayan nokta çoklu kaynak örneği değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-151">**nx_lwm2m_resource_multiple_get_float64**: *Get the value of a 64-bit Floating Point Multiple Resource Instance*</span></span>
- <span data-ttu-id="1e11e-152">**nx_lwm2m_resource_multiple_get_integer32**: *32 bitlik bir tamsayı birden çok kaynak örneğinin değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-152">**nx_lwm2m_resource_multiple_get_integer32**: *Get the value of a 32-Bit Integer Multiple Resource Instance*</span></span>
- <span data-ttu-id="1e11e-153">**nx_lwm2m_resource_multiple_get_integer64**: *64 bitlik bir tamsayı birden çok kaynak örneğinin değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-153">**nx_lwm2m_resource_multiple_get_integer64**: *Get the value of a 64-Bit Integer Multiple Resource Instance*</span></span>
- <span data-ttu-id="1e11e-154">**nx_lwm2m_resource_multiple_get_objlnk**: *birden çok kaynak örneği Için bir nesne bağlantısı değeri alın*</span><span class="sxs-lookup"><span data-stu-id="1e11e-154">**nx_lwm2m_resource_multiple_get_objlnk**: *Get the value of an Object Link Multiple Resource Instance*</span></span>
- <span data-ttu-id="1e11e-155">**nx_lwm2m_resource_multiple_get_opaque**: *donuk birden çok kaynak örneğinin değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-155">**nx_lwm2m_resource_multiple_get_opaque**: *Get the value of an Opaque Multiple Resource Instance*</span></span>
- <span data-ttu-id="1e11e-156">**nx_lwm2m_resource_multiple_get_string**: *dize çoklu kaynak örneği değerini Al*</span><span class="sxs-lookup"><span data-stu-id="1e11e-156">**nx_lwm2m_resource_multiple_get_string**: *Get the value of a String Multiple Resource Instance*</span></span>

### <a name="firmware-update-object"></a><span data-ttu-id="1e11e-157">Bellenim güncelleştirme nesnesi</span><span class="sxs-lookup"><span data-stu-id="1e11e-157">Firmware Update Object</span></span>

- <span data-ttu-id="1e11e-158">**nx_lwm2m_firmware_create**: *bellenim güncelleştirme nesnesi oluştur*</span><span class="sxs-lookup"><span data-stu-id="1e11e-158">**nx_lwm2m_firmware_create**: *Create Firmware Update Object*</span></span>
- <span data-ttu-id="1e11e-159">**nx_lwm2m_firmware_package_info_set**: *bellenim güncelleştirme paketi bilgilerini ayarla*</span><span class="sxs-lookup"><span data-stu-id="1e11e-159">**nx_lwm2m_firmware_package_info_set**: *Set Firmware Update Package Information*</span></span>
- <span data-ttu-id="1e11e-160">**nx_lwm2m_firmware_result_set**: *bellenim güncelleştirme sonucunu ayarla*</span><span class="sxs-lookup"><span data-stu-id="1e11e-160">**nx_lwm2m_firmware_result_set**: *Set Firmware Update Result*</span></span>
- <span data-ttu-id="1e11e-161">**nx_lwm2m_firmware_state_set**: *bellenim güncelleştirme durumunu ayarla*</span><span class="sxs-lookup"><span data-stu-id="1e11e-161">**nx_lwm2m_firmware_state_set**: *Set Firmware Update State*</span></span>

## <a name="nx_lwm2m_client_create"></a><span data-ttu-id="1e11e-162">nx_lwm2m_client_create</span><span class="sxs-lookup"><span data-stu-id="1e11e-162">nx_lwm2m_client_create</span></span>

<span data-ttu-id="1e11e-163">LWM2M Istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e11e-163">Create LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-164">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-164">Prototype</span></span>

```c
UINT nx_lwm2m_client_create(NX_LWM2M_CLIENT *client_ptr, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr, UINT local_port, const CHAR *name_ptr,
    const CHAR *msisdn_ptr, UCHAR binding_modes, VOID *stack_ptr, ULONG stack_size);
```

### <a name="description"></a><span data-ttu-id="1e11e-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-165">Description</span></span>

<span data-ttu-id="1e11e-166">Bu hizmet kendi ThreadX iş parçacığı bağlamında çalışan bir LWM2M Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1e11e-166">This service creates a LWM2M Client instance, which runs in the context of its own ThreadX thread.</span></span>

<span data-ttu-id="1e11e-167">LWM2M Istemcisi şu OMA LWM2M nesnelerini uygular: güvenlik (0), sunucu (1), Access Control (2) ve cihaz (3).</span><span class="sxs-lookup"><span data-stu-id="1e11e-167">The LWM2M Client implements the following OMA LWM2M Objects: Security (0), Server (1), Access Control (2) and Device (3).</span></span> <span data-ttu-id="1e11e-168">Diğer nesneler uygulamaları, uygulama tarafından eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-168">The other objects implementations must be added by the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-169">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-169">Parameters</span></span>

- <span data-ttu-id="1e11e-170">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-170">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-171">**ip_ptr**: daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-171">**ip_ptr**: Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="1e11e-172">**packet_pool_ptr**: Bu LWM2M istemcisi için varsayılan paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-172">**packet_pool_ptr**: Pointer to the default packet pool for this LWM2M Client.</span></span>
- <span data-ttu-id="1e11e-173">**local_port**: güvenli olmayan iletişim için kullanılan yerel UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="1e11e-173">**local_port**: The local UDP port used for non-secure communication.</span></span>
- <span data-ttu-id="1e11e-174">**name_ptr**: LWM2M istemci uç noktası adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-174">**name_ptr**: Pointer to LWM2M Client endpoint name.</span></span>
- <span data-ttu-id="1e11e-175">**msisdn_ptr**: LWM2M istemcisine SMS bağlaması ile kullanım için ULAŞıLABILDIĞI MSISDN IŞARETÇISINE, SMS bağlaması desteklenmiyorsa null olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-175">**msisdn_ptr**: Pointer to the MSISDN where the LWM2M Client can be reached for use with the SMS binding, can be NULL if SMS binding is not supported.</span></span>
- <span data-ttu-id="1e11e-176">**binding_modes**: LWM2M istemcisi tarafından desteklenen bağlama ve modlar NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S ve NX_LWM2M_BINDING_SQ bayraklarının bir birleşimi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-176">**binding_modes**: The binding and modes supported by the LWM2M Client, must be a combination of NX_LWM2M_BINDING_U, NX_LWM2M_BINDING_UQ, NX_LWM2M_BINDING_S and NX_LWM2M_BINDING_SQ flags.</span></span>
- <span data-ttu-id="1e11e-177">**stack_ptr**: Işaretçi LWM2M istemci iş parçacığı yığın alanı.</span><span class="sxs-lookup"><span data-stu-id="1e11e-177">**stack_ptr**: Pointer to LWM2M Client thread stack area.</span></span>
- <span data-ttu-id="1e11e-178">**stack_size**: LWM2M istemci iş parçacığı yığın boyutu.</span><span class="sxs-lookup"><span data-stu-id="1e11e-178">**stack_size**: The LWM2M Client thread stack size.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-179">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-179">Return Values</span></span>

- <span data-ttu-id="1e11e-180">**NX_SUCCESS**: LWM2M istemcisi başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="1e11e-180">**NX_SUCCESS**: The LWM2M Client has been successfully created.</span></span>
- <span data-ttu-id="1e11e-181">**NX_LWM2M_ERROR**: LWM2M istemcisi oluşturma hatası.</span><span class="sxs-lookup"><span data-stu-id="1e11e-181">**NX_LWM2M_ERROR**: LWM2M Client create error.</span></span>
- <span data-ttu-id="1e11e-182">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-182">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_delete"></a><span data-ttu-id="1e11e-183">nx_lwm2m_client_delete</span><span class="sxs-lookup"><span data-stu-id="1e11e-183">nx_lwm2m_client_delete</span></span>

<span data-ttu-id="1e11e-184">LWM2M Istemcisini Sil</span><span class="sxs-lookup"><span data-stu-id="1e11e-184">Delete LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-185">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-185">Prototype</span></span>

```c
UINT nx_lwm2m_client_delete(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-186">Description</span></span>

<span data-ttu-id="1e11e-187">Bu hizmet, daha önce oluşturulmuş bir LWM2M Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="1e11e-187">This service deletes a previously created LWM2M Client instance.</span></span>

<span data-ttu-id="1e11e-188">O anda istemcinin bağlı olduğu tüm oturumlar bu çağrı tarafından da silinir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-188">All sessions currently attached the client are also deleted by this call.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-189">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-189">Parameters</span></span>

- <span data-ttu-id="1e11e-190">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-190">**client_ptr**: Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-191">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-191">Return Values</span></span>

- <span data-ttu-id="1e11e-192">**NX_SUCCESS**: LWM2M istemcisi başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-192">**NX_SUCCESS**: The LWM2M Client has been successfully deleted.</span></span>
- <span data-ttu-id="1e11e-193">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-193">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_device_callbacks_set"></a><span data-ttu-id="1e11e-194">nx_lwm2m_client_device_callbacks_set</span><span class="sxs-lookup"><span data-stu-id="1e11e-194">nx_lwm2m_client_device_callbacks_set</span></span>

<span data-ttu-id="1e11e-195">Cihaz nesnesi uygulama geri çağırmaları ayarla</span><span class="sxs-lookup"><span data-stu-id="1e11e-195">Set Device Object application callbacks</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-196">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-196">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_CLIENT_DEVICE_READ_CALLBACK read_callback,
    NX_LWM2M_CLIENT_DEVICE_DISCOVER_CALLBACK discover_callback,
    NX_LWM2M_CLIENT_DEVICE_WRITE_CALLBACK write_callback,
    NX_LWM2M_CLIENT_DEVICE_EXECUTE_CALLBACK execute_callback);
```

### <a name="description"></a><span data-ttu-id="1e11e-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-197">Description</span></span>

<span data-ttu-id="1e11e-198">Bu hizmet, LWM2M Istemcisi tarafından işlenmeyen LWM2M cihaz nesnesi kaynaklarına işlem uygulamak için uygulama geri çağırmaları yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-198">This service installs the application callbacks for implementing operations on the LWM2M Device Object resources that are not handled by the LWM2M Client.</span></span>

<span data-ttu-id="1e11e-199">LWM2M Istemcisi şu kaynakları uygular: hata kodu (11), sıfırlama hata kodu (12) ve desteklenen bağlama ve modlar (16), diğer kaynaklara yönelik işlemler uygulamaya yeniden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-199">The LWM2M Client implements the following resources : Error Code (11), Reset Error Code (12) and Supported Binding and Modes (16), operations to the other resources are redirected to the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-200">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-200">Parameters</span></span>

- <span data-ttu-id="1e11e-201">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-201">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-202">**read_callback**: ' Read ' metodu geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="1e11e-202">**read_callback**: The 'Read' method callback.</span></span>
- <span data-ttu-id="1e11e-203">**discover_callback**: ' keşfet ' metodu geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="1e11e-203">**discover_callback**: The 'Discover' method callback.</span></span>
- <span data-ttu-id="1e11e-204">**write_callback**: ' Write ' metodu geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="1e11e-204">**write_callback**: The 'Write' method callback.</span></span>
- <span data-ttu-id="1e11e-205">**execute_callback**: ' Execute ' metodu geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="1e11e-205">**execute_callback**: The 'Execute' method callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-206">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-206">Return Values</span></span>

- <span data-ttu-id="1e11e-207">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-207">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-208">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-208">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_device_error_push"></a><span data-ttu-id="1e11e-209">nx_lwm2m_client_device_error_push</span><span class="sxs-lookup"><span data-stu-id="1e11e-209">nx_lwm2m_client_device_error_push</span></span>

<span data-ttu-id="1e11e-210">Cihaz nesnesine hata kodu ekle</span><span class="sxs-lookup"><span data-stu-id="1e11e-210">Add error code to Device Object</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-211">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-211">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_error_push(NX_LWM2M_CLIENT *client_ptr, UCHAR code);
```

### <a name="description"></a><span data-ttu-id="1e11e-212">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-212">Description</span></span>

<span data-ttu-id="1e11e-213">Bu hizmet, nesne cihazının hata kodu (11) kaynağına yeni bir örnek ekler.</span><span class="sxs-lookup"><span data-stu-id="1e11e-213">This service adds a new instance to the Error Code (11) resource of the Object Device.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-214">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-214">Parameters</span></span>

- <span data-ttu-id="1e11e-215">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-215">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-216">**kod**: yeni hata kodu.</span><span class="sxs-lookup"><span data-stu-id="1e11e-216">**code**: The new error code.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-217">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-217">Return Values</span></span>

- <span data-ttu-id="1e11e-218">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-218">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-219">**NX_LWM2M_BUFFER_TOO_SMALL**: en fazla depolanan hata kodu sayısına ulaşıldı.</span><span class="sxs-lookup"><span data-stu-id="1e11e-219">**NX_LWM2M_BUFFER_TOO_SMALL**: The maximum number of stored error codes has been reached.</span></span>
- <span data-ttu-id="1e11e-220">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-220">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_device_error_reset"></a><span data-ttu-id="1e11e-221">nx_lwm2m_client_device_error_reset</span><span class="sxs-lookup"><span data-stu-id="1e11e-221">nx_lwm2m_client_device_error_reset</span></span>

<span data-ttu-id="1e11e-222">Cihaz nesnesinin hata kodlarını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="1e11e-222">Reset error codes of Device Object</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-223">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-223">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_error_reset(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-224">Description</span></span>

<span data-ttu-id="1e11e-225">Bu hizmet, tüm hata kodu kaynak örneklerini cihaz nesnesinden siler.</span><span class="sxs-lookup"><span data-stu-id="1e11e-225">This service deletes all error code resource instances from the Device Object.</span></span> <span data-ttu-id="1e11e-226">Bu, kaynak sıfırlama hata kodunu (12) çalıştırmaya eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-226">This is equivalent to executing the resource Reset Error Code (12).</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-227">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-227">Parameters</span></span>

- <span data-ttu-id="1e11e-228">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-228">**client_ptr**: Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-229">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-229">Return Values</span></span>

- <span data-ttu-id="1e11e-230">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-230">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-231">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-231">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_device_resource_changed"></a><span data-ttu-id="1e11e-232">nx_lwm2m_client_device_resource_changed</span><span class="sxs-lookup"><span data-stu-id="1e11e-232">nx_lwm2m_client_device_resource_changed</span></span>

<span data-ttu-id="1e11e-233">Cihaz nesnesi kaynağının sinyal değişikliği</span><span class="sxs-lookup"><span data-stu-id="1e11e-233">Signal change of Device Object resource</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-234">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-234">Prototype</span></span>

```c
UINT nx_lwm2m_client_device_resource_changed(NX_LWM2M_CLIENT *client_ptr,
                                    const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a><span data-ttu-id="1e11e-235">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-235">Description</span></span>

<span data-ttu-id="1e11e-236">Hizmet, uygulama tarafından, nesne cihazının bir kaynağının değiştiği LWM2M Istemcisine işaret etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-236">The service is used by the application to signal to the LWM2M Client that a resource of the Object Device has changed.</span></span> <span data-ttu-id="1e11e-237">LWM2M Istemcisi, kaynak bir LWM2M sunucusu tarafından gözlemleniyorsa bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-237">The LWM2M Client will send a notification if the resource is observed by a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-238">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-238">Parameters</span></span>

- <span data-ttu-id="1e11e-239">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-239">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-240">**kaynak**: değiştirilen kaynağı açıklayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-240">**resource**: Pointer to the structure describing the resource that has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-241">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-241">Return Values</span></span>

- <span data-ttu-id="1e11e-242">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-242">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-243">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-243">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_lock"></a><span data-ttu-id="1e11e-244">nx_lwm2m_client_lock</span><span class="sxs-lookup"><span data-stu-id="1e11e-244">nx_lwm2m_client_lock</span></span>

<span data-ttu-id="1e11e-245">LWM2M Istemcisini kilitle</span><span class="sxs-lookup"><span data-stu-id="1e11e-245">Lock LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-246">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-246">Prototype</span></span>

```c
UINT nx_lwm2m_client_lock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-247">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-247">Description</span></span>

<span data-ttu-id="1e11e-248">Bu hizmet, LWM2M nesnelerine sunuculardan veya başka bir uygulama iş parçacığından sürekli erişimi engellemek için LWM2M Istemcisini kilitler.</span><span class="sxs-lookup"><span data-stu-id="1e11e-248">This service locks the LWM2M Client to prevent concurent access to the LWM2M objects from the servers or another application thread.</span></span>

<span data-ttu-id="1e11e-249">LWM2M Istemcisi Şu anda başka bir iş parçacığı tarafından kilitliyse, LWM2M Istemcisinin kilidi açana kadar işlev engellenir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-249">If the LWM2M Client is currently locked by another thread, the function will block until the LWM2M Client is unlocked.</span></span>

<span data-ttu-id="1e11e-250">Nx_lwm2m_client_lock ()/nx_lwm2m_client_unlock () çiftlerine yapılan çağrılar iç içe olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-250">Calls to nx_lwm2m_client_lock()/nx_lwm2m_client_unlock() pairs can be nested.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-251">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-251">Parameters</span></span>

- <span data-ttu-id="1e11e-252">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-252">**client_ptr**: Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-253">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-253">Return Values</span></span>

- <span data-ttu-id="1e11e-254">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-254">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-255">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-255">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_add"></a><span data-ttu-id="1e11e-256">nx_lwm2m_client_object_add</span><span class="sxs-lookup"><span data-stu-id="1e11e-256">nx_lwm2m_client_object_add</span></span>

<span data-ttu-id="1e11e-257">LWM2M Istemcisine nesne uygulamasını ekleme</span><span class="sxs-lookup"><span data-stu-id="1e11e-257">Add Object implementation to the LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-258">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-258">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_add(NX_LWM2M_CLIENT *client_ptr,
                                NX_LWM2M_OBJECT *object_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-259">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-259">Description</span></span>

<span data-ttu-id="1e11e-260">Bu hizmet, LWM2M Istemcisine yeni bir nesne uygulamasını ekler.</span><span class="sxs-lookup"><span data-stu-id="1e11e-260">This service adds a new Object implementation to the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-261">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-261">Parameters</span></span>

- <span data-ttu-id="1e11e-262">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-262">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-263">**object_ptr**: nesne uygulamasını tanımlayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-263">**object_ptr**: Pointer to the structure defining the Object implementation.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-264">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-264">Return Values</span></span>

- <span data-ttu-id="1e11e-265">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-265">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-266">**NX_LWM2M_ALREADY_EXIST**: nesne kimliği zaten var.</span><span class="sxs-lookup"><span data-stu-id="1e11e-266">**NX_LWM2M_ALREADY_EXIST**: The Object ID already exists.</span></span>
- <span data-ttu-id="1e11e-267">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-267">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_create"></a><span data-ttu-id="1e11e-268">nx_lwm2m_client_object_create</span><span class="sxs-lookup"><span data-stu-id="1e11e-268">nx_lwm2m_client_object_create</span></span>

<span data-ttu-id="1e11e-269">Yeni bir nesne örneği oluştur</span><span class="sxs-lookup"><span data-stu-id="1e11e-269">Create a new Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-270">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-270">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_create(NX_LWM2M_CLIENT *client_ptr,
            NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr,
            UINT num_values, const NX_LWM2M_RESOURCE *values_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-271">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-271">Description</span></span>

<span data-ttu-id="1e11e-272">Bu hizmet, yeni bir nesne örneği oluşturmak için LWM2M Istemcisinin bir nesnesi üzerinde bir ' Create ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-272">This service performs a 'Create' operation on an Object of the LWM2M Client to create a new Object Instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-273">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-273">Parameters</span></span>

- <span data-ttu-id="1e11e-274">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-274">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-275">**object_id**: nesne kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-275">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="1e11e-276">**instance_id_ptr**: LWM2M Istemcisinin BIR örnek kimliği ataması gerekiyorsa, yenı örneğin kimliğine YÖNELIK işaretçi null olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-276">**instance_id_ptr**: Pointer to the ID of the new instance, can be NULL if the LWM2M Client must assign an Instance ID.</span></span> <span data-ttu-id="1e11e-277">KIMLIK ayrılmış 65535 ise, LWM2M Istemcisi bir örnek KIMLIĞI atayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-277">If the ID is the reserved value 65535 the LWM2M Client will assign an Instance ID.</span></span> <span data-ttu-id="1e11e-278">NULL değilse, çağrının ardından atanan KIMLIK döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1e11e-278">If not NULL the assigned ID is returned after the call.</span></span>
- <span data-ttu-id="1e11e-279">**num_values**: ayarlanacak değer sayısı.</span><span class="sxs-lookup"><span data-stu-id="1e11e-279">**num_values**: The number of values to set.</span></span>
- <span data-ttu-id="1e11e-280">**values_ptr**: yeni nesne örneğini başlatmak için kaynak değerleri dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-280">**values_ptr**: Pointer to an array of resource values to initialize the new Object Instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-281">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-281">Return Values</span></span>

- <span data-ttu-id="1e11e-282">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-282">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-283">**NX_LWM2M_ALREADY_EXIST**: nesne örneği kimliği zaten var.</span><span class="sxs-lookup"><span data-stu-id="1e11e-283">**NX_LWM2M_ALREADY_EXIST**: The Object Instance ID already exists.</span></span>
- <span data-ttu-id="1e11e-284">**NX_LWM2M_METHOD_NOT_ALLOWED**: nesne, örnek oluşturmayı desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-284">**NX_LWM2M_METHOD_NOT_ALLOWED**: The Object doesn't support instance creation.</span></span>
- <span data-ttu-id="1e11e-285">**NX_LWM2M_NO_MEMORY**: yeni örneği depolamak için bellek ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-285">**NX_LWM2M_NO_MEMORY**: Cannot allocate memory to store the new instance.</span></span>
- <span data-ttu-id="1e11e-286">**NX_LWM2M_NOT_FOUND**: nesne kimliği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-286">**NX_LWM2M_NOT_FOUND**: The Object ID doesn't exist.</span></span>
- <span data-ttu-id="1e11e-287">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-287">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_delete"></a><span data-ttu-id="1e11e-288">nx_lwm2m_client_object_delete</span><span class="sxs-lookup"><span data-stu-id="1e11e-288">nx_lwm2m_client_object_delete</span></span>

<span data-ttu-id="1e11e-289">Bir nesne örneğini silme</span><span class="sxs-lookup"><span data-stu-id="1e11e-289">Delete an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-290">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-290">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_delete(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id);
```

### <a name="description"></a><span data-ttu-id="1e11e-291">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-291">Description</span></span>

<span data-ttu-id="1e11e-292">Bu hizmet, LWM2M Istemcisinin nesne örneği üzerinde bir ' DELETE ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-292">This service performs a 'Delete' operation on an Object Instance of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-293">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-293">Parameters</span></span>

- <span data-ttu-id="1e11e-294">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-294">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-295">**object_id**: nesne kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-295">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="1e11e-296">**instance_id**: nesne örneği kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-296">**instance_id**: The Object Instance ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-297">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-297">Return Values</span></span>

- <span data-ttu-id="1e11e-298">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-298">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-299">**NX_LWM2M_METHOD_NOT_ALLOWED**: nesne, örnek silmeyi desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-299">**NX_LWM2M_METHOD_NOT_ALLOWED**: The Object doesn't support instance deletion.</span></span>
- <span data-ttu-id="1e11e-300">**NX_LWM2M_NOT_FOUND**: nesne kimliği veya nesne örneği kimliği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-300">**NX_LWM2M_NOT_FOUND**: The Object ID or Object Instance ID doesn't exist.</span></span>
- <span data-ttu-id="1e11e-301">Geçersiz NX_PTR_ERROR işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-301">NX_PTR_ERROR Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_discover"></a><span data-ttu-id="1e11e-302">nx_lwm2m_client_object_discover</span><span class="sxs-lookup"><span data-stu-id="1e11e-302">nx_lwm2m_client_object_discover</span></span>

<span data-ttu-id="1e11e-303">Bir nesne örneğinin kaynaklarını bulma</span><span class="sxs-lookup"><span data-stu-id="1e11e-303">Discover resources of an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-304">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-304">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_discover(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT *num_resources_ptr, NX_LWM2M_RESOURCE_INFO *resources_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-305">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-305">Description</span></span>

<span data-ttu-id="1e11e-306">Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde bir ' bul ' işlemi gerçekleştirir, bu, nesne tarafından uygulanan kaynakların listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="1e11e-306">This service performs a 'Discover' operation on an Object Instance of the LWM2M Client, this returns the list of resources implemented by the Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-307">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-307">Parameters</span></span>

- <span data-ttu-id="1e11e-308">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-308">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-309">**object_id**: nesne kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-309">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="1e11e-310">**instance_id**: nesne örneği kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-310">**instance_id**: The Object Instance ID.</span></span>
- <span data-ttu-id="1e11e-311">**num_resources_ptr**: giriş, hedef arabelleğin boyutunun çıktıda, arabelleğe yazıldı.</span><span class="sxs-lookup"><span data-stu-id="1e11e-311">**num_resources_ptr**: On input the size of the destination buffer, on output the number of elements writen to the buffer.</span></span>
- <span data-ttu-id="1e11e-312">**resources_ptr**: hedef arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-312">**resources_ptr**: Pointer to the destination buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-313">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-313">Return Values</span></span>

- <span data-ttu-id="1e11e-314">**NX_SUCCESS**: başarılı işlem..</span><span class="sxs-lookup"><span data-stu-id="1e11e-314">**NX_SUCCESS**: Successful operation..</span></span>
- <span data-ttu-id="1e11e-315">**NX_LWM2M_BUFFER_TOO_SMALL**: kaynak arabelleği, kaynak listesini depolamak için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="1e11e-315">**NX_LWM2M_BUFFER_TOO_SMALL**: The resources buffer is too small to store the list of resources.</span></span>
- <span data-ttu-id="1e11e-316">**NX_LWM2M_NOT_FOUND**: nesne kimliği veya nesne örneği kimliği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-316">**NX_LWM2M_NOT_FOUND**: The Object ID or Object Instance ID doesn't exist.</span></span>
- <span data-ttu-id="1e11e-317">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-317">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_execute"></a><span data-ttu-id="1e11e-318">nx_lwm2m_client_object_execute</span><span class="sxs-lookup"><span data-stu-id="1e11e-318">nx_lwm2m_client_object_execute</span></span>

<span data-ttu-id="1e11e-319">Bir nesne örneğinin kaynağını yürütün</span><span class="sxs-lookup"><span data-stu-id="1e11e-319">Execute resource of an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-320">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-320">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_execute(NX_LWM2M_CLIENT *client_ptr,
    NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr, UINT arguments_length);
```

### <a name="description"></a><span data-ttu-id="1e11e-321">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-321">Description</span></span>

<span data-ttu-id="1e11e-322">Bu hizmet, LWM2M Istemcisinin nesne örneği kaynağında ' Execute ' işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-322">This service performs the 'Execute' operation on an Object Instance Resource of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-323">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-323">Parameters</span></span>

- <span data-ttu-id="1e11e-324">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-324">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-325">**object_id**: nesne kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-325">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="1e11e-326">**instance_id**: nesne örneği kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-326">**instance_id**: The Object Instance ID.</span></span>
- <span data-ttu-id="1e11e-327">**resource_id**: kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-327">**resource_id**: The Resource ID.</span></span>
- <span data-ttu-id="1e11e-328">**arguments_ptr**: yürütme işleminin bağımsız değişkenlerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-328">**arguments_ptr**: Pointer to the arguments of the execute operation.</span></span> <span data-ttu-id="1e11e-329">Arguments_length sıfırsa NULL olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-329">Can be NULL if arguments_length is zero.</span></span>
- <span data-ttu-id="1e11e-330">**arguments_length**: bağımsız değişkenlerin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="1e11e-330">**arguments_length**: The length of the arguments.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-331">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-331">Return Values</span></span>

- <span data-ttu-id="1e11e-332">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-332">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-333">**NX_LWM2M_METHOD_NOT_ALLOWED**: kaynak yürütme işlemini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-333">**NX_LWM2M_METHOD_NOT_ALLOWED**: The resource doesn't support the execute operation.</span></span>
- <span data-ttu-id="1e11e-334">**NX_LWM2M_NOT_FOUND**: nesne kimliği, nesne örneği kimliği veya kaynak kimliği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-334">**NX_LWM2M_NOT_FOUND**: The Object ID, Object Instance ID or the resource ID doesn't exist.</span></span>
- <span data-ttu-id="1e11e-335">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-335">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_get_next"></a><span data-ttu-id="1e11e-336">nx_lwm2m_client_object_get_next</span><span class="sxs-lookup"><span data-stu-id="1e11e-336">nx_lwm2m_client_object_get_next</span></span>

<span data-ttu-id="1e11e-337">LWM2M Istemcisi tarafından uygulanan nesne listesini al</span><span class="sxs-lookup"><span data-stu-id="1e11e-337">Get the list of Objects implemented by the LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-338">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-338">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_get_next(NX_LWM2M_CLIENT *client_ptr,
                                    NX_LWM2M_ID *object_id_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-339">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-339">Description</span></span>

<span data-ttu-id="1e11e-340">Bu hizmet, LWM2M Istemcisi tarafından uygulanan bir sonraki nesnenin KIMLIĞINI döndürür.</span><span class="sxs-lookup"><span data-stu-id="1e11e-340">This service returns the ID of the next Object implemented by the LWM2M Client.</span></span> <span data-ttu-id="1e11e-341">Geçerli nesne KIMLIĞI NX_LWM2M_RESERVED_ID olarak ayarlandıysa (65535) ilk nesne KIMLIĞI döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1e11e-341">If the current Object ID is set to NX_LWM2M_RESERVED_ID (65535) the first Object ID is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-342">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-342">Parameters</span></span>

- <span data-ttu-id="1e11e-343">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-343">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-344">**object_id_ptr**: GEÇERLI nesne kimliğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-344">**object_id_ptr**: Pointer to the current Object ID.</span></span> <span data-ttu-id="1e11e-345">Dönüşte, LWM2M Istemcisi tarafından uygulanan bir sonraki nesne KIMLIĞINI içerir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-345">On return contains the next Object ID implemented by the LWM2M Client.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-346">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-346">Return Values</span></span>

- <span data-ttu-id="1e11e-347">**NX_SUCCESS**: başarılı işlem..</span><span class="sxs-lookup"><span data-stu-id="1e11e-347">**NX_SUCCESS**: Successful operation..</span></span>
- <span data-ttu-id="1e11e-348">**NX_LWM2M_NOT_FOUND**: VERILEN nesne kimliği veritabanının son sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-348">**NX_LWM2M_NOT_FOUND**: The given Object ID is the last of the database.</span></span>
- <span data-ttu-id="1e11e-349">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-349">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_instance_get_next"></a><span data-ttu-id="1e11e-350">nx_lwm2m_client_object_instance_get_next</span><span class="sxs-lookup"><span data-stu-id="1e11e-350">nx_lwm2m_client_object_instance_get_next</span></span>

<span data-ttu-id="1e11e-351">Bir nesnenin örneklerinin listesini al</span><span class="sxs-lookup"><span data-stu-id="1e11e-351">Get the list of Instances of an Object</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-352">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-352">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_instance_get_next(NX_LWM2M_CLIENT *client_ptr,
                    NX_LWM2M_ID object_id, NX_LWM2M_ID *instance_id_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-353">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-353">Description</span></span>

<span data-ttu-id="1e11e-354">Bu hizmet, belirtilen nesnenin sonraki nesne örneğinin KIMLIĞINI döndürür.</span><span class="sxs-lookup"><span data-stu-id="1e11e-354">This service returns the ID of the next Object Instance of the given Object.</span></span> <span data-ttu-id="1e11e-355">Geçerli örnek KIMLIĞI NX_LWM2M_RESERVED_ID olarak ayarlandıysa (65535) ilk Örneğin KIMLIĞI döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1e11e-355">If the current Instance ID is set to NX_LWM2M_RESERVED_ID (65535) the ID of the first instance is returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-356">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-356">Parameters</span></span>

- <span data-ttu-id="1e11e-357">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-357">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-358">**object_id**: nesne kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-358">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="1e11e-359">**instance_id_ptr**: geçerli nesne örneği kimliğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-359">**instance_id_ptr**: Pointer to the current Object Instance ID.</span></span> <span data-ttu-id="1e11e-360">Dönüş sırasında nesnenin sonraki örnek KIMLIĞINI içerir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-360">On return contains the next Instance ID of the Object.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-361">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-361">Return Values</span></span>

- <span data-ttu-id="1e11e-362">**NX_SUCCESS**: başarılı işlem..</span><span class="sxs-lookup"><span data-stu-id="1e11e-362">**NX_SUCCESS**: Successful operation..</span></span>
- <span data-ttu-id="1e11e-363">**NX_LWM2M_NOT_FOUND**: VERILEN örnek kimliği nesnenin son, veya nesne kimliği uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="1e11e-363">**NX_LWM2M_NOT_FOUND**: The given Instance ID is the last of the object, or the Object ID is not implemented.</span></span>
- <span data-ttu-id="1e11e-364">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-364">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_read"></a><span data-ttu-id="1e11e-365">nx_lwm2m_client_object_read</span><span class="sxs-lookup"><span data-stu-id="1e11e-365">nx_lwm2m_client_object_read</span></span>

<span data-ttu-id="1e11e-366">Bir nesne örneğinin kaynak değerlerini oku</span><span class="sxs-lookup"><span data-stu-id="1e11e-366">Read resources values of an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-367">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-367">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_read(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id,
        UINT num_values, NX_LWM2M_RESOURCE *values);
```

### <a name="description"></a><span data-ttu-id="1e11e-368">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-368">Description</span></span>

<span data-ttu-id="1e11e-369">Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde ' Read ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-369">This service performs a 'Read' operation on an Object Instance of the LWM2M Client.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-370">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-370">Parameters</span></span>

- <span data-ttu-id="1e11e-371">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-371">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-372">**object_id**: nesne kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-372">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="1e11e-373">**instance_id**: nesne örneği kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-373">**instance_id**: The Object Instance ID.</span></span>
- <span data-ttu-id="1e11e-374">**num_values**: okunacak kaynak sayısı.</span><span class="sxs-lookup"><span data-stu-id="1e11e-374">**num_values**: The number of resources to read.</span></span>
- <span data-ttu-id="1e11e-375">**values_ptr**: okunacak kaynakların kimliklerini içeren bir NX_LWM2M_RESOURCE dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-375">**values_ptr**: Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources to read.</span></span> <span data-ttu-id="1e11e-376">Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="1e11e-376">On return the array is filled with the corresponding types and values.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-377">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-377">Return Values</span></span>

- <span data-ttu-id="1e11e-378">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-378">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-379">**NX_LWM2M_METHOD_NOT_ALLOWED**: bir kaynak okuma işlemini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-379">**NX_LWM2M_METHOD_NOT_ALLOWED**: A resource doesn't support the read operation.</span></span>
- <span data-ttu-id="1e11e-380">**NX_LWM2M_NOT_FOUND**: nesne kimliği, nesne örneği kimliği veya kaynak kimliği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-380">**NX_LWM2M_NOT_FOUND**: The Object ID, Object Instance ID or a resource ID doesn't exist.</span></span>
- <span data-ttu-id="1e11e-381">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-381">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_object_write"></a><span data-ttu-id="1e11e-382">nx_lwm2m_client_object_write</span><span class="sxs-lookup"><span data-stu-id="1e11e-382">nx_lwm2m_client_object_write</span></span>

<span data-ttu-id="1e11e-383">Bir nesne örneğinin kaynak değerlerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="1e11e-383">Change resources values of an Object instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-384">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-384">Prototype</span></span>

```c
UINT nx_lwm2m_client_object_write(NX_LWM2M_CLIENT *client_ptr,
        NX_LWM2M_ID object_id, NX_LWM2M_ID instance_id, UINT num_values,
        const NX_LWM2M_RESOURCE *values_ptr, UINT write_op);
```

### <a name="description"></a><span data-ttu-id="1e11e-385">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-385">Description</span></span>

<span data-ttu-id="1e11e-386">Bu hizmet, LWM2M Istemcisinin bir nesne örneğinde ' Write ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-386">This service performs a 'Write' operation on an Object Instance of the LWM2M Client.</span></span>

<span data-ttu-id="1e11e-387">*Write_op* parametresine aşağıdaki yazma işlemleri de belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="1e11e-387">The following write operations can be specified to the *write_op* parameter:</span></span>

- <span data-ttu-id="1e11e-388">**0** &mdash; Kısmi güncelleştirme: yeni değerde belirtilen kaynakları ekler veya güncelleştirir ve diğer mevcut kaynakları değiştirmeden bırakır,</span><span class="sxs-lookup"><span data-stu-id="1e11e-388">**0** &mdash; Partial Update: adds or updates Resources provided in the new value and leaves other existing Resources unchanged,</span></span>

- <span data-ttu-id="1e11e-389">**NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Örnek Değiştir: nesne örneğini, yeni sağlanmış kaynak değerleriyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-389">**NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Replace Instance: replaces the Object Instance with the new provided resource values.</span></span>

- <span data-ttu-id="1e11e-390">**NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Kaynağı değiştir: kaynakları, belirtilen yeni kaynak değerleriyle (birden çok kaynağı değiştirmek için kullanılır) değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-390">**NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Replace Resource: replaces the Resources with the new provided resource values (used to replace Multiple Resources).</span></span>

- <span data-ttu-id="1e11e-391">**NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Önyükleme yazma: bir önyükleme dizisinin çağrısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-391">**NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap Write: indicates a call from a Bootstrap sequence.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-392">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-392">Parameters</span></span>

- <span data-ttu-id="1e11e-393">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-393">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-394">**object_id**: nesne kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-394">**object_id**: The Object ID.</span></span>
- <span data-ttu-id="1e11e-395">**instance_id**: nesne örneği kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-395">**instance_id**: The Object Instance ID.</span></span>
- <span data-ttu-id="1e11e-396">**num_values**: yazılacak kaynak sayısı.</span><span class="sxs-lookup"><span data-stu-id="1e11e-396">**num_values**: The number of resources to write.</span></span>
- <span data-ttu-id="1e11e-397">**values_ptr**: kaynak kimliklerini, türleri ve yazılacak değerleri içeren bir NX_LWM2M_RESOURCE dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-397">**values_ptr**: Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources, the types and the values to write.</span></span>
- <span data-ttu-id="1e11e-398">**write_op**: yazma işlemi türü.</span><span class="sxs-lookup"><span data-stu-id="1e11e-398">**write_op**: The type of write operation.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-399">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-399">Return Values</span></span>

- <span data-ttu-id="1e11e-400">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-400">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-401">**NX_LWM2M_BAD_ENCODING**: kaynak türü geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-401">**NX_LWM2M_BAD_ENCODING**: The type of a resource is not valid.</span></span>
- <span data-ttu-id="1e11e-402">**NX_LWM2M_BUFFER_TOO_SMALL**: bir değerin uzunluğu, örnekte depolanamayacak kadar büyük.</span><span class="sxs-lookup"><span data-stu-id="1e11e-402">**NX_LWM2M_BUFFER_TOO_SMALL**: The length of a value is too big to be stored in the instance.</span></span>
- <span data-ttu-id="1e11e-403">**NX_LWM2M_METHOD_NOT_ALLOWED**: bir kaynak yazma işlemini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-403">**NX_LWM2M_METHOD_NOT_ALLOWED**: A resource doesn't support the write operation.</span></span>
- <span data-ttu-id="1e11e-404">**NX_LWM2M_NO_MEMORY**: bir kaynak değeri depolamak için bellek ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-404">**NX_LWM2M_NO_MEMORY**: Cannot allocate memory to store a resource value.</span></span>
- <span data-ttu-id="1e11e-405">**NX_LWM2M_NOT_ACCEPTABLE**: bir kaynağın değeri geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-405">**NX_LWM2M_NOT_ACCEPTABLE**: The value of a resource is not valid.</span></span>
- <span data-ttu-id="1e11e-406">**NX_LWM2M_NOT_FOUND**: nesne kimliği, nesne örneği kimliği veya kaynak kimliği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-406">**NX_LWM2M_NOT_FOUND**: The Object ID, Object Instance ID or a resource ID doesn't exist.</span></span>
- <span data-ttu-id="1e11e-407">NX_OPTION_ERROR: geçersiz yazma işlemi türü.</span><span class="sxs-lookup"><span data-stu-id="1e11e-407">NX_OPTION_ERROR: Invalid type of write operation.</span></span>
- <span data-ttu-id="1e11e-408">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-408">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_security_key_callbacks_set"></a><span data-ttu-id="1e11e-409">nx_lwm2m_client_security_key_callbacks_set</span><span class="sxs-lookup"><span data-stu-id="1e11e-409">nx_lwm2m_client_security_key_callbacks_set</span></span>

<span data-ttu-id="1e11e-410">Güvenlik nesnesi anahtar yönetimi geri çağırmaları ayarla</span><span class="sxs-lookup"><span data-stu-id="1e11e-410">Set Security Object key management callbacks</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-411">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-411">Prototype</span></span>

```c
UINT nx_lwm2m_client_security_key_callbacks_set(NX_LWM2M_CLIENT *client_ptr,
                NX_LWM2M_CLIENT_SECURITY_KEY_WRITE_CALLBACK write_callback,
                NX_LWM2M_CLIENT_SECURITY_KEY_DELETE_CALLBACK delete_callback);
```

### <a name="description"></a><span data-ttu-id="1e11e-412">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-412">Description</span></span>

<span data-ttu-id="1e11e-413">Bu hizmet, güvenlik anahtarlarıyla ilgili LWM2M güvenlik nesnesi kaynakları üzerinde işlem uygulamak için uygulama geri çağırmaları yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-413">This service installs the application callbacks for implementing operations on the LWM2M Security Object resources related to the security keys.</span></span>

<span data-ttu-id="1e11e-414">LWM2M Istemcisi, önyükleme oturumları sırasında güvenlik anahtarı yönetimini uygulamaya devreder, önyükleme sunucusu bir güvenlik nesnesi örneğinde aşağıdaki kaynakları yazdığında veya sildiği geri çağrılar çağrılır: ortak anahtar veya kimlik (3), sunucu ortak anahtar (4), gizli anahtar (5).</span><span class="sxs-lookup"><span data-stu-id="1e11e-414">The LWM2M Client delegates the security key management to the application during the Bootstrap sessions, the callbacks will be called when the Bootstrap Server writes or deletes the following resources on a Security Object Instance: Public Key or Identity (3), Server Public Key (4), Secret Key (5).</span></span>

<span data-ttu-id="1e11e-415">Uygulama, anahtar verilerinin depolanmasından ve LWM2M istemcisi tarafından kullanılan DTLS oturumlarını yapılandırmadan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="1e11e-415">The application is responsible for storing the keys data and for configuring the DTLS sessions used by the LWM2M client.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-416">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-416">Parameters</span></span>

- <span data-ttu-id="1e11e-417">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-417">**client_ptr**: Pointer to LWM2M Client control block.</span></span>
- <span data-ttu-id="1e11e-418">**write_callback**: ' Write ' anahtar yöntemi geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="1e11e-418">**write_callback**: The 'Write' key method callback.</span></span>
- <span data-ttu-id="1e11e-419">**delete_callback**: ' DELETE ' anahtar yöntemi geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="1e11e-419">**delete_callback**: The 'Delete' key method callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-420">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-420">Return Values</span></span>

- <span data-ttu-id="1e11e-421">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-421">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-422">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-422">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_bootstrap"></a><span data-ttu-id="1e11e-423">nx_lwm2m_client_session_bootstrap</span><span class="sxs-lookup"><span data-stu-id="1e11e-423">nx_lwm2m_client_session_bootstrap</span></span>

<span data-ttu-id="1e11e-424">Önyükleme sunucusu ile oturum başlatma</span><span class="sxs-lookup"><span data-stu-id="1e11e-424">Start a session with a Bootstrap Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-425">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-425">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_bootstrap(NX_LWM2M_CLIENT_SESSION
    *session_ptr, NX_LWM2M_ID security_id, ULONG ip_address, UINT port);
```

### <a name="description"></a><span data-ttu-id="1e11e-426">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-426">Description</span></span>

<span data-ttu-id="1e11e-427">Bu hizmet, bir önyükleme sunucusu ile oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-427">This service start a session with a Bootstrap Server.</span></span> <span data-ttu-id="1e11e-428">Sunucu, güvenlik nesnesinde karşılık gelen bir güvenlik örneğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-428">The server should have a corresponding security instance in the Security Object.</span></span>

<span data-ttu-id="1e11e-429">' Kapalı ' kaynağı bu sunucuyla ilişkili güvenlik örneğinde sıfırdan farklıysa, bu süre sonunda Istemci tarafından başlatılan bir önyükleme yoksa, oturum sunucu tarafından başlatılan bir önyükleme için bekler.</span><span class="sxs-lookup"><span data-stu-id="1e11e-429">If the 'Hold Off' resource is different than zero in the Security Instance associated with this server the session will wait for a Server Initiated Bootstrap, if no bootstrap is initiated by the server after this period of time a Client Initiated Boostrap will be performed.</span></span>

<span data-ttu-id="1e11e-430">Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni önyükleme sunucusu oturumuyla değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-430">Any current active session is aborted by this call and replaced by the new Bootstrap Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-431">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-431">Parameters</span></span>

- <span data-ttu-id="1e11e-432">**session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-432">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="1e11e-433">**security_id**: önyükleme sunucusunda tanımlı güvenlik örneği yoksa önyükleme sunucusunun GÜVENLIK örneği kimliği NX_LWM2M_RESERVED_ID (65535) olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-433">**security_id**: The Security Instance ID of the Bootstrap Server, must be set to NX_LWM2M_RESERVED_ID (65535) if the Bootstrap Server has no Security Instance defined.</span></span>
- <span data-ttu-id="1e11e-434">**ip_address**: sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-434">**ip_address**: The IP address of the server.</span></span>
- <span data-ttu-id="1e11e-435">**bağlantı noktası**: sunucunun UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="1e11e-435">**port**: The UDP port of the server.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-436">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-436">Return Values</span></span>

- <span data-ttu-id="1e11e-437">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-437">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-438">**NX_LWM2M_NOT_FOUND**: güvenlık örneği kimliğine karşılık gelen bir güvenlik nesnesi örneği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-438">**NX_LWM2M_NOT_FOUND**: There is No Security Object instance corresponding to the Security Instance ID.</span></span>
- <span data-ttu-id="1e11e-439">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-439">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_bootstrap_dtls"></a><span data-ttu-id="1e11e-440">nx_lwm2m_client_session_bootstrap_dtls</span><span class="sxs-lookup"><span data-stu-id="1e11e-440">nx_lwm2m_client_session_bootstrap_dtls</span></span>

<span data-ttu-id="1e11e-441">Önyükleme sunucusu ile güvenli bir oturum başlatma</span><span class="sxs-lookup"><span data-stu-id="1e11e-441">Start a secure session with a Bootstrap Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-442">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-442">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_bootstrap_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID security_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a><span data-ttu-id="1e11e-443">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-443">Description</span></span>

<span data-ttu-id="1e11e-444">Bu hizmet, güvenli bir DTLS bağlantısı kullanarak önyükleme sunucusuyla bir oturum başlatır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-444">This service start a session with a Bootstrap Server using a secure DTLS connection.</span></span> <span data-ttu-id="1e11e-445">Sunucu, güvenlik nesnesinde karşılık gelen bir güvenlik örneğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-445">The server should have a corresponding security instance in the Security Object.</span></span>

<span data-ttu-id="1e11e-446">DTLS oturumunun, bu işlev çağrılmadan önce uygun şifre paketleri ve anahtar malzemeyle yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-446">The DTLS session must have been configured with the proper cipher suites and key material before calling this function.</span></span> <span data-ttu-id="1e11e-447">NX_SECURE_ENABLE_DTLS tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-447">NX_SECURE_ENABLE_DTLS must be defined.</span></span>

<span data-ttu-id="1e11e-448">' Kapalı ' kaynağı bu sunucuyla ilişkili güvenlik örneğinde sıfırdan farklıysa, bu süre sonunda Istemci tarafından başlatılan bir önyükleme yoksa, oturum sunucu tarafından başlatılan bir önyükleme için bekler.</span><span class="sxs-lookup"><span data-stu-id="1e11e-448">If the 'Hold Off' resource is different than zero in the Security Instance associated with this server the session will wait for a Server Initiated Bootstrap, if no bootstrap is initiated by the server after this period of time a Client Initiated Boostrap will be performed.</span></span>

<span data-ttu-id="1e11e-449">Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni önyükleme sunucusu oturumuyla değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-449">Any current active session is aborted by this call and replaced by the new Bootstrap Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-450">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-450">Parameters</span></span>

- <span data-ttu-id="1e11e-451">**session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-451">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="1e11e-452">**security_id**: önyükleme sunucusunda tanımlı güvenlik örneği yoksa önyükleme sunucusunun GÜVENLIK örneği kimliği NX_LWM2M_RESERVED_ID (65535) olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-452">**security_id**: The Security Instance ID of the Bootstrap Server, must be set to NX_LWM2M_RESERVED_ID (65535) if the Bootstrap Server has no Security Instance defined.</span></span>
- <span data-ttu-id="1e11e-453">**ip_address**: sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-453">**ip_address**: The IP address of the server.</span></span>
- <span data-ttu-id="1e11e-454">**bağlantı noktası**: sunucunun UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="1e11e-454">**port**: The UDP port of the server.</span></span>
- <span data-ttu-id="1e11e-455">**dtls_session_ptr**: önyükleme oturumu için kullanılacak DTLS oturumu.</span><span class="sxs-lookup"><span data-stu-id="1e11e-455">**dtls_session_ptr**: The DTLS session to use for the Bootstrap session.</span></span>
- <span data-ttu-id="1e11e-456">**dtls_local_port**: DTLS oturumu için kullanılan yerel UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="1e11e-456">**dtls_local_port**: The local UDP port used for the DTLS session.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-457">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-457">Return Values</span></span>

- <span data-ttu-id="1e11e-458">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-458">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-459">**NX_LWM2M_NOT_FOUND**: güvenlık örneği kimliğine karşılık gelen bir güvenlik nesnesi örneği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-459">**NX_LWM2M_NOT_FOUND**: There is No Security Object instance corresponding to the Security Instance ID.</span></span>
- <span data-ttu-id="1e11e-460">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-460">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_create"></a><span data-ttu-id="1e11e-461">nx_lwm2m_client_session_create</span><span class="sxs-lookup"><span data-stu-id="1e11e-461">nx_lwm2m_client_session_create</span></span>

<span data-ttu-id="1e11e-462">LWM2M Istemci oturumu oluştur</span><span class="sxs-lookup"><span data-stu-id="1e11e-462">Create LWM2M Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-463">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-463">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_create(NX_LWM2M_CLIENT_SESSION *session_ptr,
         NX_LWM2M_CLIENT *client_ptr,
         NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK state_callback);
```

### <a name="description"></a><span data-ttu-id="1e11e-464">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-464">Description</span></span>

<span data-ttu-id="1e11e-465">Bu hizmet, var olan bir LWM2M Istemcisine bağlı yeni bir LWM2M Istemci oturumu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1e11e-465">This service creates a new LWM2M Client Session attached to an existing LWM2M Client.</span></span> <span data-ttu-id="1e11e-466">Oturum, bir önyükleme sunucusuyla veya bir LWM2M sunucusuyla iletişim kurmak için LWM2M Istemcisi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-466">The session is used by the LWM2M Client to communicate with a Bootstrap Server or a LWM2M Server.</span></span>

<span data-ttu-id="1e11e-467">Uygulama, oturumun durumu güncellendiği zaman çağrılacak bir geri çağırma işlevi sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-467">The application must provide a callback function that will be called when the state of the session is updated.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-468">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-468">Parameters</span></span>

- <span data-ttu-id="1e11e-469">**session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-469">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="1e11e-470">**client_ptr**: daha önce oluşturulan LWM2M istemcisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-470">**client_ptr**: Pointer to the previously created LWM2M Client.</span></span>
- <span data-ttu-id="1e11e-471">**state_callback**: oturumun durumu değiştiğinde çağrılan uygulama geri çağırması.</span><span class="sxs-lookup"><span data-stu-id="1e11e-471">**state_callback**: Application callback that is called when the state of the session has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-472">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-472">Return Values</span></span>

- <span data-ttu-id="1e11e-473">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-473">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-474">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-474">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_delete"></a><span data-ttu-id="1e11e-475">nx_lwm2m_client_session_delete</span><span class="sxs-lookup"><span data-stu-id="1e11e-475">nx_lwm2m_client_session_delete</span></span>

<span data-ttu-id="1e11e-476">LWM2M Istemci oturumunu Sil</span><span class="sxs-lookup"><span data-stu-id="1e11e-476">Delete LWM2M Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-477">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-477">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_delete(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-478">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-478">Description</span></span>

<span data-ttu-id="1e11e-479">Bu hizmet bir LWM2M Istemci oturumunu siler.</span><span class="sxs-lookup"><span data-stu-id="1e11e-479">This service deletes a LWM2M Client Session.</span></span>

<span data-ttu-id="1e11e-480">Nx_lwm2m_client_delete çağırarak bir LWM2M Istemcisi silindiğinde, istemciye bağlı tüm oturumlar da silinir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-480">When a LWM2M Client is deleted by calling nx_lwm2m_client_delete all sessions attached to the client are also deleted.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-481">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-481">Parameters</span></span>

- <span data-ttu-id="1e11e-482">**session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-482">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-483">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-483">Return Values</span></span>

- <span data-ttu-id="1e11e-484">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-484">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-485">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-485">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_deregister"></a><span data-ttu-id="1e11e-486">nx_lwm2m_client_session_deregister</span><span class="sxs-lookup"><span data-stu-id="1e11e-486">nx_lwm2m_client_session_deregister</span></span>

<span data-ttu-id="1e11e-487">LWM2M sunucusu ile bir oturumu sonlandırma</span><span class="sxs-lookup"><span data-stu-id="1e11e-487">Terminate a session with a LWM2M Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-488">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-488">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_deregister(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-489">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-489">Description</span></span>

<span data-ttu-id="1e11e-490">Bu hizmet bir LWM2M sunucusuna ' de Register ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-490">This service performs a 'De-Register' operation to a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-491">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-491">Parameters</span></span>

- <span data-ttu-id="1e11e-492">**session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-492">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-493">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-493">Return Values</span></span>

- <span data-ttu-id="1e11e-494">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-494">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-495">**NX_LWM2M_NOT_REGISTERED**: istemci sunucuya kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-495">**NX_LWM2M_NOT_REGISTERED**: The client is not registered to the server.</span></span>
- <span data-ttu-id="1e11e-496">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-496">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_error_get"></a><span data-ttu-id="1e11e-497">nx_lwm2m_client_session_error_get</span><span class="sxs-lookup"><span data-stu-id="1e11e-497">nx_lwm2m_client_session_error_get</span></span>

<span data-ttu-id="1e11e-498">Bir oturumun son hatasını al</span><span class="sxs-lookup"><span data-stu-id="1e11e-498">Get last error of a session</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-499">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-499">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_error_get(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-500">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-500">Description</span></span>

<span data-ttu-id="1e11e-501">Bu hizmet, oturum bir hata durumundayken oturumun hata kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="1e11e-501">This service returns the error code of the session when the session is in an error state.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-502">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-502">Parameters</span></span>

- <span data-ttu-id="1e11e-503">**session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-503">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-504">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-504">Return Values</span></span>

- <span data-ttu-id="1e11e-505">**NX_SUCCESS**: oturum hata durumunda değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-505">**NX_SUCCESS**: The session is not in error state.</span></span>
- <span data-ttu-id="1e11e-506">**NX_LWM2M_ADDRESS_ERROR**: geçersiz sunucu adresi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-506">**NX_LWM2M_ADDRESS_ERROR**: Invalid server address.</span></span>
- <span data-ttu-id="1e11e-507">**NX_LWM2M_BUFFER_TOO_SMALL**: istek yükü ağ arabelleğine uymuyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-507">**NX_LWM2M_BUFFER_TOO_SMALL**: Payload of request doesn't fit in network buffer.</span></span>
- <span data-ttu-id="1e11e-508">**NX_LWM2M_DTLS_ERROR**: sunucuyla güvenli bağlantı kurulamadı.</span><span class="sxs-lookup"><span data-stu-id="1e11e-508">**NX_LWM2M_DTLS_ERROR**: Failed to establish secured connection with server.</span></span>
- <span data-ttu-id="1e11e-509">**NX_LWM2M_ERROR**: belirtilmeyen hata.</span><span class="sxs-lookup"><span data-stu-id="1e11e-509">**NX_LWM2M_ERROR**: Unspecified error.</span></span>
- <span data-ttu-id="1e11e-510">**NX_LWM2M_FORBIDDEN**: kayıt sunucu tarafından reddedildi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-510">**NX_LWM2M_FORBIDDEN**: Registration refused by server.</span></span>
- <span data-ttu-id="1e11e-511">**NX_LWM2M_NOT_FOUND**: güncelleştirme/kaydını kaldırmak, istemci sunucu tarafından bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1e11e-511">**NX_LWM2M_NOT_FOUND**: Client not found by server when updating/deregistering.</span></span>
- <span data-ttu-id="1e11e-512">**NX_LWM2M_SERVER_INSTANCE_DELETED**: oturuma karşılık gelen sunucu nesnesi örneği silindi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-512">**NX_LWM2M_SERVER_INSTANCE_DELETED**: The Server Object Instance corresponding to the session has been deleted.</span></span>
- <span data-ttu-id="1e11e-513">**NX_LWM2M_TIMED_OUT**: sunucudan yanıt yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-513">**NX_LWM2M_TIMED_OUT**: No answer from server.</span></span>
- <span data-ttu-id="1e11e-514">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-514">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_register"></a><span data-ttu-id="1e11e-515">nx_lwm2m_client_session_register</span><span class="sxs-lookup"><span data-stu-id="1e11e-515">nx_lwm2m_client_session_register</span></span>

<span data-ttu-id="1e11e-516">LWM2M sunucusu ile oturum başlatma</span><span class="sxs-lookup"><span data-stu-id="1e11e-516">Start a session with a LWM2M Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-517">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-517">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register(NX_LWM2M_CLIENT_SESSION *session_ptr,
                    NX_LWM2M_ID server_id, ULONG ip_address, UINT port);
```

### <a name="description"></a><span data-ttu-id="1e11e-518">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-518">Description</span></span>

<span data-ttu-id="1e11e-519">Bu hizmet bir LWM2M sunucusuna ' Register ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-519">This service performs a 'Register' operation to a LWM2M Server.</span></span> <span data-ttu-id="1e11e-520">Sunucu, sunucu nesnesinde karşılık gelen bir sunucu örneğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-520">The server must have a corresponding server instance in the Server Object.</span></span>

<span data-ttu-id="1e11e-521">Kayıt başarılı olursa, LWM2M Istemcisi sunucudan daha fazla işlem gerçekleştirir ve istemci kayıtlı olana kadar düzenli olarak ' güncelleştirme ' iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-521">If the registration is successful the LWM2M Client will process further operations from the server and will periodically send 'Update' messages until the client is de-registered.</span></span>

<span data-ttu-id="1e11e-522">Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni LWM2M Server oturumu tarafından değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-522">Any current active session is aborted by this call and replaced by the new LWM2M Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-523">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-523">Parameters</span></span>

- <span data-ttu-id="1e11e-524">**session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-524">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="1e11e-525">**server_id**: LWM2M sunucusunun kısa sunucu kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-525">**server_id**: The Short Server ID of the LWM2M Server.</span></span>
- <span data-ttu-id="1e11e-526">**ip_address**: sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-526">**ip_address**: The IP address of the server.</span></span>
- <span data-ttu-id="1e11e-527">**bağlantı noktası**: sunucunun UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="1e11e-527">**port**: The UDP port of the server.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-528">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-528">Return Values</span></span>

- <span data-ttu-id="1e11e-529">**NX_SUCCESS**: başarılı işlem..</span><span class="sxs-lookup"><span data-stu-id="1e11e-529">**NX_SUCCESS**: Successful operation..</span></span>
- <span data-ttu-id="1e11e-530">**NX_LWM2M_NOT_FOUND**: kısa sunucu kimliğine karşılık gelen sunucu nesnesi örneği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-530">**NX_LWM2M_NOT_FOUND**: There is No Server Object instance corresponding to the Short Server ID.</span></span>
- <span data-ttu-id="1e11e-531">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-531">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_register_dtls"></a><span data-ttu-id="1e11e-532">nx_lwm2m_client_session_register_dtls</span><span class="sxs-lookup"><span data-stu-id="1e11e-532">nx_lwm2m_client_session_register_dtls</span></span>

<span data-ttu-id="1e11e-533">LWM2M sunucusu ile güvenli bir oturum başlatma</span><span class="sxs-lookup"><span data-stu-id="1e11e-533">Start a secure session with a LWM2M Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-534">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-534">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_register_dtls(NX_LWM2M_CLIENT_SESSION *session_ptr,
    NX_LWM2M_ID server_id, ULONG ip_address, UINT port, NX_SECURE_DTLS_SESSION
    *dtls_session_ptr, UINT dtls_local_port);
```

### <a name="description"></a><span data-ttu-id="1e11e-535">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-535">Description</span></span>

<span data-ttu-id="1e11e-536">Bu hizmet, güvenli bir DTLS bağlantısı kullanarak bir LWM2M sunucusuna ' Register ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-536">This service performs a 'Register' operation to a LWM2M Server using a secure DTLS connection.</span></span> <span data-ttu-id="1e11e-537">Sunucu, sunucu nesnesinde karşılık gelen bir sunucu örneğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-537">The server must have a corresponding server instance in the Server Object.</span></span>

<span data-ttu-id="1e11e-538">DTLS oturumunun, bu işlev çağrılmadan önce uygun şifre paketleri ve anahtar malzemeyle yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-538">The DTLS session must have been configured with the proper cipher suites and key material before calling this function.</span></span> <span data-ttu-id="1e11e-539">NX_SECURE_ENABLE_DTLS tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-539">NX_SECURE_ENABLE_DTLS must be defined.</span></span>

<span data-ttu-id="1e11e-540">Her DTLS oturumu, iletişim için kendi UDP yuvasını kullanır, bu nedenle uygulama birkaç güvenli oturum oluşturduğunda her oturum için yerel bağlantı noktası dtls_local_port farklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-540">Each DTLS session uses its own UDP socket for communication, so the local port dtls_local_port must be different for each session if the application creates several secure sessions.</span></span>

<span data-ttu-id="1e11e-541">Kayıt başarılı olursa, LWM2M Istemcisi sunucudan daha fazla işlem gerçekleştirir ve istemci kayıtlı olana kadar düzenli olarak ' güncelleştirme ' iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-541">If the registration is successful the LWM2M Client will process further operations from the server and will periodically send 'Update' messages until the client is de-registered.</span></span>

<span data-ttu-id="1e11e-542">Geçerli etkin bir oturum, bu çağrı tarafından iptal edilir ve yeni LWM2M Server oturumu tarafından değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-542">Any current active session is aborted by this call and replaced by the new LWM2M Server session.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-543">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-543">Parameters</span></span>

- <span data-ttu-id="1e11e-544">**session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-544">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>
- <span data-ttu-id="1e11e-545">**server_id**: LWM2M sunucusunun kısa sunucu kimliği.</span><span class="sxs-lookup"><span data-stu-id="1e11e-545">**server_id**: The Short Server ID of the LWM2M Server.</span></span>
- <span data-ttu-id="1e11e-546">**ip_address**: sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-546">**ip_address**: The IP address of the server.</span></span>
- <span data-ttu-id="1e11e-547">**bağlantı noktası**: sunucunun UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="1e11e-547">**port**: The UDP port of the server.</span></span>
- <span data-ttu-id="1e11e-548">**dtls_session_ptr**: LWM2M oturumu için kullanılacak DTLS oturumu.</span><span class="sxs-lookup"><span data-stu-id="1e11e-548">**dtls_session_ptr**: The DTLS session to use for the LWM2M session.</span></span>
- <span data-ttu-id="1e11e-549">**dtls_local_port**: DTLS oturumu için kullanılan yerel UDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="1e11e-549">**dtls_local_port**: The local UDP port used for the DTLS session.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-550">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-550">Return Values</span></span>

- <span data-ttu-id="1e11e-551">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-551">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-552">**NX_LWM2M_NOT_FOUND**: kısa sunucu kimliğine karşılık gelen sunucu nesnesi örneği yok.</span><span class="sxs-lookup"><span data-stu-id="1e11e-552">**NX_LWM2M_NOT_FOUND**: There is No Server Object instance corresponding to the Short Server ID.</span></span>
- <span data-ttu-id="1e11e-553">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-553">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_session_update"></a><span data-ttu-id="1e11e-554">nx_lwm2m_client_session_update</span><span class="sxs-lookup"><span data-stu-id="1e11e-554">nx_lwm2m_client_session_update</span></span>

<span data-ttu-id="1e11e-555">LWM2M sunucusu ile oturum güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1e11e-555">Update a session with a LWM2M Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-556">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-556">Prototype</span></span>

```c
UINT nx_lwm2m_client_session_update(NX_LWM2M_CLIENT_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-557">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-557">Description</span></span>

<span data-ttu-id="1e11e-558">Bu hizmet bir LWM2M sunucusuna ' Update ' işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-558">This service performs an 'Update' operation to a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-559">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-559">Parameters</span></span>

- <span data-ttu-id="1e11e-560">**session_ptr**: LWM2M istemci oturumu denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-560">**session_ptr**: Pointer to LWM2M Client Session control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-561">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-561">Return Values</span></span>

- <span data-ttu-id="1e11e-562">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-562">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-563">**NX_LWM2M_NOT_REGISTERED**: istemci sunucuya kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-563">**NX_LWM2M_NOT_REGISTERED**: The client is not registered to the server.</span></span>
- <span data-ttu-id="1e11e-564">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-564">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_client_unlock"></a><span data-ttu-id="1e11e-565">nx_lwm2m_client_unlock</span><span class="sxs-lookup"><span data-stu-id="1e11e-565">nx_lwm2m_client_unlock</span></span>

<span data-ttu-id="1e11e-566">LWM2M Istemcisinin kilidini aç</span><span class="sxs-lookup"><span data-stu-id="1e11e-566">Unlock LWM2M Client</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-567">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-567">Prototype</span></span>

```c
UINT nx_lwm2m_client_unlock(NX_LWM2M_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-568">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-568">Description</span></span>

<span data-ttu-id="1e11e-569">Bu hizmet, nx_lwm2m_client_unlock () çağrısıyla kilitlenmiş LWM2M Client previoulsy 'in kilidini açar.</span><span class="sxs-lookup"><span data-stu-id="1e11e-569">This service unlocks the LWM2M Client previoulsy locked by a call to nx_lwm2m_client_unlock().</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-570">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-570">Parameters</span></span>

- <span data-ttu-id="1e11e-571">**client_ptr**: LWM2M istemci denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-571">**client_ptr**: Pointer to LWM2M Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-572">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-572">Return Values</span></span>

- <span data-ttu-id="1e11e-573">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-573">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-574">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-574">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_firmware_create"></a><span data-ttu-id="1e11e-575">nx_lwm2m_firmware_create</span><span class="sxs-lookup"><span data-stu-id="1e11e-575">nx_lwm2m_firmware_create</span></span>

<span data-ttu-id="1e11e-576">Bellenim güncelleştirme nesnesi oluştur</span><span class="sxs-lookup"><span data-stu-id="1e11e-576">Create Firmware Update Object</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-577">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-577">Prototype</span></span>

```c
UINT nx_lwm2m_firmware_create(NX_LWM2M_FIRMWARE *firmware_ptr,
    NX_LWM2M_CLIENT *client_ptr, UINT protocols,
    NX_LWM2M_FIRMWARE_PACKAGE_CALLBACK package_callback,
    NX_LWM2M_FIRMWARE_PACKAGE_URI_CALLBACK package_uri_callback,
    NX_LWM2M_FIRMWARE_UPDATE_CALLBACK update_callback);
```

### <a name="description"></a><span data-ttu-id="1e11e-578">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-578">Description</span></span>

<span data-ttu-id="1e11e-579">Bu hizmet, bir bellenim güncelleştirme nesnesini başlatır ve nesneyi daha önce oluşturulmuş bir LWM2M Istemcisine ekler.</span><span class="sxs-lookup"><span data-stu-id="1e11e-579">This service initializes a Firmware Update Object and adds the Object to a previously created LWM2M Client.</span></span> <span data-ttu-id="1e11e-580">Üretici yazılımı güncelleştirme nesnesi, bir LWM2M sunucusuyla iletişim kurmak için kaynakları uygular, ancak uygulamanın üretici yazılımında gerçek işlemleri uygulamak için geri çağrılar sağlaması gerekir (söz konusu bellenimi yükleme, depolama ve güncelleştirme).</span><span class="sxs-lookup"><span data-stu-id="1e11e-580">The Firmware Update Object implements the resources for communicating with a LWM2M Server but the application must provide callbacks for implementing the actual operations on the firmware (dowloading, storing, and updating the firmware).</span></span>

<span data-ttu-id="1e11e-581">Protocols parametresi, ' paket URI 'SI ' kaynağıyla bellenimi almak için uygulama tarafından hangi protokollerin desteklendiğini belirtir, aşağıdaki bayraklar tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="1e11e-581">The protocols parameter indicates which protocols are supported by the application for retrieving the firmware with the 'Package URI' resource, the following flags are defined:</span></span>

<span data-ttu-id="1e11e-582">NX_LWM2M_FIRMWARE_PROTOCOL_COAP, NX_LWM2M_FIRMWARE_PROTOCOL_COAPS, NX_LWM2M_FIRMWARE_PROTOCOL_HTTP NX_LWM2M_FIRMWARE_PROTOCOL_HTPPS.</span><span class="sxs-lookup"><span data-stu-id="1e11e-582">NX_LWM2M_FIRMWARE_PROTOCOL_COAP, NX_LWM2M_FIRMWARE_PROTOCOL_COAPS, NX_LWM2M_FIRMWARE_PROTOCOL_HTTP, NX_LWM2M_FIRMWARE_PROTOCOL_HTPPS.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-583">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-583">Parameters</span></span>

- <span data-ttu-id="1e11e-584">**firmware_ptr**: bellenim nesne denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-584">**firmware_ptr**: Pointer to the Firmware Object control block.</span></span>
- <span data-ttu-id="1e11e-585">**client_ptr**: önceden oluşturulan LWM2M istemcisi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-585">**client_ptr**: Pointer to previsously created LWM2M Client.</span></span>
- <span data-ttu-id="1e11e-586">**protokoller**: paket URI 'si kaynağı tarafından hangi protokollerin desteklendiğini belirten bayraklar.</span><span class="sxs-lookup"><span data-stu-id="1e11e-586">**protocols**: Flags indicating which protocols are supported by the Package URI resource.</span></span>
- <span data-ttu-id="1e11e-587">**package_callback**: null [TBD] olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-587">**package_callback**: Must be NULL [TBD].</span></span>
- <span data-ttu-id="1e11e-588">**package_uri_callback**: paket URI kaynağını uygulamak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="1e11e-588">**package_uri_callback**: Callback used to implement the Package URI resource.</span></span>
- <span data-ttu-id="1e11e-589">**update_callback**: güncelleştirme kaynağını uygulamak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="1e11e-589">**update_callback**: Callback used to implement the Update resource.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-590">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-590">Return Values</span></span>

- <span data-ttu-id="1e11e-591">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-591">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-592">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-592">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_firmware_package_info_set"></a><span data-ttu-id="1e11e-593">nx_lwm2m_firmware_package_info_set</span><span class="sxs-lookup"><span data-stu-id="1e11e-593">nx_lwm2m_firmware_package_info_set</span></span>

<span data-ttu-id="1e11e-594">Bellenim güncelleştirme paketi bilgilerini ayarla</span><span class="sxs-lookup"><span data-stu-id="1e11e-594">Set Firmware Update Package Information</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-595">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-595">Prototype</span></span>

```c
UINT nx_lwm2m_firmware_package_info_set(NX_LWM2M_FIRMWARE *firmware_ptr,
                                const CHAR *name, const CHAR *version);
```

### <a name="description"></a><span data-ttu-id="1e11e-596">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-596">Description</span></span>

<span data-ttu-id="1e11e-597">Bu hizmet, bellenim güncelleştirme nesnesinin ' PkgName ' (6) ve ' PkgVersion ' (7) kaynaklarının değerlerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-597">This service changes the values of the 'PkgName' (6) and 'PkgVersion' (7) resources of the Firmware Update Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-598">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-598">Parameters</span></span>

- <span data-ttu-id="1e11e-599">**firmware_ptr**: bellenim güncelleştirme nesnesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-599">**firmware_ptr**: Pointer to the Firmware Update Object.</span></span>
- <span data-ttu-id="1e11e-600">**ad**: paket adının yeni değeri.</span><span class="sxs-lookup"><span data-stu-id="1e11e-600">**name**: The new value of the Package Name.</span></span>
- <span data-ttu-id="1e11e-601">**Sürüm**: paket sürümünün yeni değeri.</span><span class="sxs-lookup"><span data-stu-id="1e11e-601">**version**: The new value of the Package Version.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-602">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-602">Return Values</span></span>

- <span data-ttu-id="1e11e-603">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-603">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-604">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-604">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_firmware_result_set"></a><span data-ttu-id="1e11e-605">nx_lwm2m_firmware_result_set</span><span class="sxs-lookup"><span data-stu-id="1e11e-605">nx_lwm2m_firmware_result_set</span></span>

<span data-ttu-id="1e11e-606">Bellenim güncelleştirme sonucunu ayarla</span><span class="sxs-lookup"><span data-stu-id="1e11e-606">Set Firmware Update Result</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-607">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-607">Prototype</span></span>

```c
UINT nx_lwm2m_firmware_result_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR result);
```

### <a name="description"></a><span data-ttu-id="1e11e-608">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-608">Description</span></span>

<span data-ttu-id="1e11e-609">Bu hizmet, bellenim güncelleştirme nesnesinin ' güncelleştirme sonucu ' (5) kaynağının değerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-609">This service changes the value of the 'Update Result' (5) resource of the Firmware Update Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-610">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-610">Parameters</span></span>

- <span data-ttu-id="1e11e-611">**firmware_ptr**: bellenim güncelleştirme nesnesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-611">**firmware_ptr**: Pointer to the Firmware Update Object.</span></span>
- <span data-ttu-id="1e11e-612">**sonuç**: güncelleştirme sonucu kaynağının yeni değeri.</span><span class="sxs-lookup"><span data-stu-id="1e11e-612">**result**: The new value of the Update Result resource.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-613">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-613">Return Values</span></span>

- <span data-ttu-id="1e11e-614">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-614">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-615">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-615">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_firmware_state_set"></a><span data-ttu-id="1e11e-616">nx_lwm2m_firmware_state_set</span><span class="sxs-lookup"><span data-stu-id="1e11e-616">nx_lwm2m_firmware_state_set</span></span>

<span data-ttu-id="1e11e-617">Üretici yazılımı güncelleştirme durumunu ayarla</span><span class="sxs-lookup"><span data-stu-id="1e11e-617">Set Firmware Update State</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-618">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-618">Prototype</span></span>

```c
UINT nx_lwm2m_firmware_state_set(NX_LWM2M_FIRMWARE *firmware_ptr, UCHAR state);
```

### <a name="description"></a><span data-ttu-id="1e11e-619">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-619">Description</span></span>

<span data-ttu-id="1e11e-620">Bu hizmet, bellenim güncelleştirme nesnesinin ' durum ' (3) kaynağının değerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-620">This service changes the value of the 'State' (3) resource of the Firmware Update Object.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-621">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-621">Parameters</span></span>

- <span data-ttu-id="1e11e-622">**firmware_ptr**: bellenim güncelleştirme nesnesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-622">**firmware_ptr**: Pointer to the Firmware Update Object.</span></span>
- <span data-ttu-id="1e11e-623">**durum**: durum kaynağının yeni değeri.</span><span class="sxs-lookup"><span data-stu-id="1e11e-623">**state**: The new value of the State resource.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-624">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-624">Return Values</span></span>

- <span data-ttu-id="1e11e-625">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-625">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-626">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-626">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_object_resource_changed"></a><span data-ttu-id="1e11e-627">nx_lwm2m_object_resource_changed</span><span class="sxs-lookup"><span data-stu-id="1e11e-627">nx_lwm2m_object_resource_changed</span></span>

<span data-ttu-id="1e11e-628">Bir nesne örneğinin kaynak değeri için sinyal değişikliği</span><span class="sxs-lookup"><span data-stu-id="1e11e-628">Signal change of a resource value of an Object Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-629">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-629">Prototype</span></span>

```c
UINT nx_lwm2m_object_resource_changed(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, const NX_LWM2M_RESOURCE *resource);
```

### <a name="description"></a><span data-ttu-id="1e11e-630">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-630">Description</span></span>

<span data-ttu-id="1e11e-631">Bu hizmet bir nesne uygulama tarafından, kaynak değerinden birinin değiştiğini LWM2M Istemcisine işaret etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-631">This service is used by an Object implementation to signals the LWM2M Client that one of its resource value has changed.</span></span> <span data-ttu-id="1e11e-632">LWM2M Istemcisi, kaynak bir LWM2M sunucusu tarafından gözlemleniyorsa bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-632">The LWM2M Client will send a notification if the resource is observed by a LWM2M Server.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-633">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-633">Parameters</span></span>

- <span data-ttu-id="1e11e-634">**object_ptr**: nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-634">**object_ptr**: Pointer to the Object implementation.</span></span>
- <span data-ttu-id="1e11e-635">**instance_ptr**: nesne örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-635">**instance_ptr**: Pointer to the Object Instance.</span></span>
- <span data-ttu-id="1e11e-636">**kaynak**: değiştirilen kaynağı açıklayan yapıya yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-636">**resource**: Pointer to the structure describing the resource that has changed.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-637">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-637">Return Values</span></span>

- <span data-ttu-id="1e11e-638">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-638">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-639">NX_PTR_ERROR: geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-639">NX_PTR_ERROR: Invalid pointer.</span></span>

## <a name="nx_lwm2m_resource_get_boolean"></a><span data-ttu-id="1e11e-640">nx_lwm2m_resource_get_boolean</span><span class="sxs-lookup"><span data-stu-id="1e11e-640">nx_lwm2m_resource_get_boolean</span></span>

<span data-ttu-id="1e11e-641">Boole kaynağının değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-641">Get the value of a Boolean Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-642">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-642">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_boolean(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-643">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-643">Description</span></span>

<span data-ttu-id="1e11e-644">Hizmet bir Boole kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-644">The service retrieves the value of a Boolean Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-645">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-645">Parameters</span></span>

- <span data-ttu-id="1e11e-646">**değer**: kaynak değer açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-646">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="1e11e-647">**bool_ptr**: hedef Boolean değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-647">**bool_ptr**: Pointer to the destination Boolean value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-648">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-648">Return Values</span></span>

- <span data-ttu-id="1e11e-649">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-649">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-650">**NX_LWM2M_BAD_ENCODING**: kaynak değeri bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-650">**NX_LWM2M_BAD_ENCODING**: The resource value is not a Boolean value.</span></span>

## <a name="nx_lwm2m_resource_get_float32"></a><span data-ttu-id="1e11e-651">nx_lwm2m_resource_get_float32</span><span class="sxs-lookup"><span data-stu-id="1e11e-651">nx_lwm2m_resource_get_float32</span></span>

<span data-ttu-id="1e11e-652">32 bitlik kayan nokta kaynağının değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-652">Get the value of a 32-bit Floating Point Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-653">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-653">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_float32(const NX_LWM2M_RESOURCE *value,
                                NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-654">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-654">Description</span></span>

<span data-ttu-id="1e11e-655">Hizmet, 32 bitlik bir kayan nokta kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-655">The service retrieves the value of a 32-bit Floating Point Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-656">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-656">Parameters</span></span>

- <span data-ttu-id="1e11e-657">**değer**: kaynak değer açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-657">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="1e11e-658">**float32_ptr**: hedef 32 bit kayan nokta değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-658">**float32_ptr**: Pointer to the destination 32-Bit Floating Point value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-659">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-659">Return Values</span></span>

- <span data-ttu-id="1e11e-660">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-660">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-661">**NX_LWM2M_BAD_ENCODING**: kaynak değeri bir kayan nokta değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-661">**NX_LWM2M_BAD_ENCODING**: The resource value is not a Floating Point value.</span></span>

## <a name="nx_lwm2m_resource_get_float64"></a><span data-ttu-id="1e11e-662">nx_lwm2m_resource_get_float64</span><span class="sxs-lookup"><span data-stu-id="1e11e-662">nx_lwm2m_resource_get_float64</span></span>

<span data-ttu-id="1e11e-663">64 bitlik kayan nokta kaynağının değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-663">Get the value of a 64-bit Floating Point Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-664">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-664">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_float64(const NX_LWM2M_RESOURCE *value,
                                NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-665">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-665">Description</span></span>

<span data-ttu-id="1e11e-666">Hizmet, 64 bitlik bir kayan nokta kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-666">The service retrieves the value of a 64-bit Floating Point Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-667">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-667">Parameters</span></span>

- <span data-ttu-id="1e11e-668">**değer**: kaynak değer açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-668">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="1e11e-669">**float64_ptr**: hedef 64 bit kayan nokta değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-669">**float64_ptr**: Pointer to the destination 64-Bit Floating Point value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-670">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-670">Return Values</span></span>

- <span data-ttu-id="1e11e-671">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-671">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-672">**NX_LWM2M_BAD_ENCODING**: kaynak değeri bir kayan nokta değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-672">**NX_LWM2M_BAD_ENCODING**: The resource value is not a Floating Point value.</span></span>

## <a name="nx_lwm2m_resource_get_integer32"></a><span data-ttu-id="1e11e-673">nx_lwm2m_resource_get_integer32</span><span class="sxs-lookup"><span data-stu-id="1e11e-673">nx_lwm2m_resource_get_integer32</span></span>

<span data-ttu-id="1e11e-674">32 bitlik bir tamsayı kaynağının değerini alır</span><span class="sxs-lookup"><span data-stu-id="1e11e-674">Get the value of a 32-Bit Integer Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-675">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-675">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_integer32(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-676">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-676">Description</span></span>

<span data-ttu-id="1e11e-677">Hizmet, 32 bitlik bir tamsayı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-677">The service retrieves the value of a 32-Bit Integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-678">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-678">Parameters</span></span>

- <span data-ttu-id="1e11e-679">**değer**: kaynak değer açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-679">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="1e11e-680">**int32_ptr**: hedef 32-bit tamsayı değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-680">**int32_ptr**: Pointer to the destination 32-Bit Integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-681">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-681">Return Values</span></span>

- <span data-ttu-id="1e11e-682">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-682">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-683">**NX_LWM2M_BAD_ENCODING**: kaynak değeri bir tamsayı değer değil veya tamsayı değeri 32 bitlik bir numaraya uymuyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-683">**NX_LWM2M_BAD_ENCODING**: The resource value is not an Integer value, or the Integer value doesn't fit in a 32-Bit number.</span></span>

## <a name="nx_lwm2m_resource_get_integer64"></a><span data-ttu-id="1e11e-684">nx_lwm2m_resource_get_integer64</span><span class="sxs-lookup"><span data-stu-id="1e11e-684">nx_lwm2m_resource_get_integer64</span></span>

<span data-ttu-id="1e11e-685">64 bitlik bir tamsayı kaynağının değerini alır</span><span class="sxs-lookup"><span data-stu-id="1e11e-685">Get the value of a 64-Bit Integer Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-686">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-686">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_integer64(const NX_LWM2M_RESOURCE *value,
                                        NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-687">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-687">Description</span></span>

<span data-ttu-id="1e11e-688">Hizmet, 64 bitlik bir tamsayı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-688">The service retrieves the value of a 64-Bit Integer Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-689">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-689">Parameters</span></span>

- <span data-ttu-id="1e11e-690">**değer**: kaynak değer açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-690">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="1e11e-691">**int64_ptr**: hedef 64-bit tamsayı değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-691">**int64_ptr**: Pointer to the destination 64-Bit Integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-692">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-692">Return Values</span></span>

- <span data-ttu-id="1e11e-693">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-693">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-694">**NX_LWM2M_BAD_ENCODING**: kaynak değeri bir tamsayı değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-694">**NX_LWM2M_BAD_ENCODING**: The resource value is not an Integer value.</span></span>

## <a name="nx_lwm2m_resource_get_objlnk"></a><span data-ttu-id="1e11e-695">nx_lwm2m_resource_get_objlnk</span><span class="sxs-lookup"><span data-stu-id="1e11e-695">nx_lwm2m_resource_get_objlnk</span></span>

<span data-ttu-id="1e11e-696">Nesne bağlantı kaynağının değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-696">Get the value of an Object Link Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-697">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-697">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_objlnk(const NX_LWM2M_RESOURCE *value,
                                    NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-698">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-698">Description</span></span>

<span data-ttu-id="1e11e-699">Hizmet, bir nesne bağlantı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-699">The service retrieves the value of an Object Link Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-700">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-700">Parameters</span></span>

- <span data-ttu-id="1e11e-701">**değer**: kaynak değer açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-701">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="1e11e-702">**objlnk_ptr**: hedef nesne bağlantı değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-702">**objlnk_ptr**: Pointer to the destination Object Link value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-703">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-703">Return Values</span></span>

- <span data-ttu-id="1e11e-704">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-704">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-705">**NX_LWM2M_BAD_ENCODING**: kaynak değeri bir nesne bağlantı değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-705">**NX_LWM2M_BAD_ENCODING**: The resource value is not an Object Link value.</span></span>

## <a name="nx_lwm2m_resource_get_opaque"></a><span data-ttu-id="1e11e-706">nx_lwm2m_resource_get_opaque</span><span class="sxs-lookup"><span data-stu-id="1e11e-706">nx_lwm2m_resource_get_opaque</span></span>

<span data-ttu-id="1e11e-707">Donuk bir kaynağın değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-707">Get the value of an Opaque Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-708">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-708">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_opaque(const NX_LWM2M_RESOURCE *value,
            const VOID **opaque_ptr_ptr, UINT *opaque_length_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-709">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-709">Description</span></span>

<span data-ttu-id="1e11e-710">Hizmet, donuk bir kaynağın değerini alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-710">The service retrieves the value of an Opaque Resource.</span></span>

<span data-ttu-id="1e11e-711">Donuk bir kaynak değeri, arabelleğin ve uzunluğun bir işaretçisinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="1e11e-711">An opaque resource value consists of a pointer to a buffer and a length.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-712">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-712">Parameters</span></span>

- <span data-ttu-id="1e11e-713">**değer**: kaynak değer açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-713">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="1e11e-714">**opaque_ptr_ptr**: hedef donuk arabellek işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-714">**opaque_ptr_ptr**: Pointer to the destination opaque buffer pointer.</span></span>
- <span data-ttu-id="1e11e-715">**opaque_length_ptr**: hedef donuk arabellek uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-715">**opaque_length_ptr**: Pointer to the destination opaque buffer length.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-716">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-716">Return Values</span></span>

- <span data-ttu-id="1e11e-717">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-717">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-718">**NX_LWM2M_BAD_ENCODING**: kaynak değeri donuk bir değer değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-718">**NX_LWM2M_BAD_ENCODING**: The resource value is not an Opaque value.</span></span>

## <a name="nx_lwm2m_resource_get_string"></a><span data-ttu-id="1e11e-719">nx_lwm2m_resource_get_string</span><span class="sxs-lookup"><span data-stu-id="1e11e-719">nx_lwm2m_resource_get_string</span></span>

<span data-ttu-id="1e11e-720">Bir dize kaynağının değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-720">Get the value of a String Resource</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-721">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-721">Prototype</span></span>

```c
UINT nx_lwm2m_resource_get_string(const NX_LWM2M_RESOURCE *value,
            const CHAR **string_ptr_ptr, UINT *string_length_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-722">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-722">Description</span></span>

<span data-ttu-id="1e11e-723">Hizmet, bir dize kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-723">The service retrieves the value of a String Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-724">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-724">Parameters</span></span>

- <span data-ttu-id="1e11e-725">**değer**: kaynak değer açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-725">**value**: Pointer to Resource value description.</span></span>
- <span data-ttu-id="1e11e-726">**string_ptr_ptr**: hedef dize işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-726">**string_ptr_ptr**: Pointer to the destination string pointer.</span></span>
- <span data-ttu-id="1e11e-727">**string_length_ptr**: hedef dize uzunluğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-727">**string_length_ptr**: Pointer to the destination string length.</span></span> <span data-ttu-id="1e11e-728">Dize null sonlandırılırsa NULL olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-728">Can be NULL if the string is null-terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-729">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-729">Return Values</span></span>

- <span data-ttu-id="1e11e-730">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-730">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-731">**NX_LWM2M_BAD_ENCODING**: kaynak değeri bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-731">**NX_LWM2M_BAD_ENCODING**: The resource value is not a String value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_boolean"></a><span data-ttu-id="1e11e-732">nx_lwm2m_resource_multiple_get_boolean</span><span class="sxs-lookup"><span data-stu-id="1e11e-732">nx_lwm2m_resource_multiple_get_boolean</span></span>

<span data-ttu-id="1e11e-733">Bir Boole kaynağı için birden çok kaynak örneği değeri alın</span><span class="sxs-lookup"><span data-stu-id="1e11e-733">Get the value of a Boolean Resource Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-734">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-734">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_boolean(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_BOOL *bool_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-735">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-735">Description</span></span>

<span data-ttu-id="1e11e-736">Hizmet, bir Boolean kaynak örneğinin değerini birden çok kaynaktan alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-736">The service retrieves the value of a Boolean Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-737">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-737">Parameters</span></span>

- <span data-ttu-id="1e11e-738">**değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-738">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="1e11e-739">**Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.</span><span class="sxs-lookup"><span data-stu-id="1e11e-739">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="1e11e-740">**instance_id_ptr**: hedef örnek kimliği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-740">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="1e11e-741">**bool_ptr**: hedef Boolean değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-741">**bool_ptr**: Pointer to the destination Boolean value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-742">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-742">Return Values</span></span>

- <span data-ttu-id="1e11e-743">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-743">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-744">**NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="1e11e-744">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="1e11e-745">**NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-745">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not a Boolean value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_float32"></a><span data-ttu-id="1e11e-746">nx_lwm2m_resource_multiple_get_float32</span><span class="sxs-lookup"><span data-stu-id="1e11e-746">nx_lwm2m_resource_multiple_get_float32</span></span>

<span data-ttu-id="1e11e-747">32 bitlik kayan nokta çoklu kaynak örneği değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-747">Get the value of a 32-bit Floating Point Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-748">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-748">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_float32(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT32 *float32_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-749">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-749">Description</span></span>

<span data-ttu-id="1e11e-750">Hizmet, 32 bitlik bir kayan nokta kaynak örneğinin değerini birden çok kaynaktan alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-750">The service retrieves the value of a 32-bit Floating Point Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-751">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-751">Parameters</span></span>

- <span data-ttu-id="1e11e-752">**değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-752">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="1e11e-753">**Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.</span><span class="sxs-lookup"><span data-stu-id="1e11e-753">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="1e11e-754">**instance_id_ptr**: hedef örnek kimliği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-754">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="1e11e-755">**float32_ptr**: hedef 32 bit kayan nokta değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-755">**float32_ptr**: Pointer to the destination 32-Bit Floating Point value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-756">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-756">Return Values</span></span>

- <span data-ttu-id="1e11e-757">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-757">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-758">**NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="1e11e-758">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="1e11e-759">**NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir kayan nokta değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-759">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not a Floating Point value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_float64"></a><span data-ttu-id="1e11e-760">nx_lwm2m_resource_multiple_get_float64</span><span class="sxs-lookup"><span data-stu-id="1e11e-760">nx_lwm2m_resource_multiple_get_float64</span></span>

<span data-ttu-id="1e11e-761">64 bitlik kayan nokta çoklu kaynak örneği değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-761">Get the value of a 64-bit Floating Point Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-762">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-762">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_float64(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_FLOAT64 *float64_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-763">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-763">Description</span></span>

<span data-ttu-id="1e11e-764">Hizmet, 64 bitlik bir kayan nokta kaynak örneğinin değerini birden çok kaynaktan alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-764">The service retrieves the value of a 64-bit Floating Point Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-765">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-765">Parameters</span></span>

- <span data-ttu-id="1e11e-766">**değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-766">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="1e11e-767">**Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.</span><span class="sxs-lookup"><span data-stu-id="1e11e-767">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="1e11e-768">**instance_id_ptr**: hedef örnek kimliği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-768">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="1e11e-769">**float64_ptr**: hedef 64 bit kayan nokta değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-769">**float64_ptr**: Pointer to the destination 64-Bit Floating Point value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-770">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-770">Return Values</span></span>

- <span data-ttu-id="1e11e-771">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-771">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-772">**NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="1e11e-772">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="1e11e-773">**NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir kayan nokta değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-773">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not a Floating Point value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_integer32"></a><span data-ttu-id="1e11e-774">nx_lwm2m_resource_multiple_get_integer32</span><span class="sxs-lookup"><span data-stu-id="1e11e-774">nx_lwm2m_resource_multiple_get_integer32</span></span>

<span data-ttu-id="1e11e-775">32 bitlik bir tamsayı birden çok kaynak örneğinin değerini alır</span><span class="sxs-lookup"><span data-stu-id="1e11e-775">Get the value of a 32-Bit Integer Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-776">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-776">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_integer32(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT32 *int32_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-777">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-777">Description</span></span>

<span data-ttu-id="1e11e-778">Hizmet, 32 bitlik bir tamsayı kaynak örneğinin değerini birden çok kaynaktan alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-778">The service retrieves the value of a 32-Bit Integer Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-779">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-779">Parameters</span></span>

- <span data-ttu-id="1e11e-780">**değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-780">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="1e11e-781">**Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.</span><span class="sxs-lookup"><span data-stu-id="1e11e-781">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="1e11e-782">**instance_id_ptr**: hedef örnek kimliği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-782">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="1e11e-783">**int32_ptr**: hedef 32-bit tamsayı değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-783">**int32_ptr**: Pointer to the destination 32-Bit Integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-784">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-784">Return Values</span></span>

- <span data-ttu-id="1e11e-785">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-785">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-786">**NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="1e11e-786">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="1e11e-787">**NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir tamsayı değer değil veya tamsayı değeri 32 bitlik bir numaraya uymuyor.</span><span class="sxs-lookup"><span data-stu-id="1e11e-787">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not an Integer value, or the Integer value doesn't fit in a 32-Bit number.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_integer64"></a><span data-ttu-id="1e11e-788">nx_lwm2m_resource_multiple_get_integer64</span><span class="sxs-lookup"><span data-stu-id="1e11e-788">nx_lwm2m_resource_multiple_get_integer64</span></span>

<span data-ttu-id="1e11e-789">64 bitlik bir tamsayı birden çok kaynak örneğinin değerini alır</span><span class="sxs-lookup"><span data-stu-id="1e11e-789">Get the value of a 64-Bit Integer Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-790">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-790">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_integer64(const NX_LWM2M_RESOURCE *value,
        int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_INT64 *int64_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-791">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-791">Description</span></span>

<span data-ttu-id="1e11e-792">Hizmet, 64 bitlik bir tamsayı kaynak örneğinin değerini birden çok kaynaktan alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-792">The service retrieves the value of a 64-Bit Integer Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-793">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-793">Parameters</span></span>

- <span data-ttu-id="1e11e-794">**değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-794">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="1e11e-795">**Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.</span><span class="sxs-lookup"><span data-stu-id="1e11e-795">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="1e11e-796">**instance_id_ptr**: hedef örnek kimliği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-796">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="1e11e-797">**int64_ptr**: hedef 64-bit tamsayı değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-797">**int64_ptr**: Pointer to the destination 64-Bit Integer value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-798">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-798">Return Values</span></span>

- <span data-ttu-id="1e11e-799">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-799">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-800">**NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="1e11e-800">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="1e11e-801">**NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir tamsayı değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-801">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not an Integer value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_objlnk"></a><span data-ttu-id="1e11e-802">nx_lwm2m_resource_multiple_get_objlnk</span><span class="sxs-lookup"><span data-stu-id="1e11e-802">nx_lwm2m_resource_multiple_get_objlnk</span></span>

<span data-ttu-id="1e11e-803">Birden çok kaynak örneğinin bir nesne bağlantısının değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-803">Get the value of an Object Link Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-804">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-804">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_objlnk(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, NX_LWM2M_OBJLNK *objlnk_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-805">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-805">Description</span></span>

<span data-ttu-id="1e11e-806">Hizmet, bir nesne bağlantı kaynağı örneğinin değerini birden çok kaynaktan alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-806">The service retrieves the value of an Object Link Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-807">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-807">Parameters</span></span>

- <span data-ttu-id="1e11e-808">**değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-808">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="1e11e-809">**Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.</span><span class="sxs-lookup"><span data-stu-id="1e11e-809">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="1e11e-810">**instance_id_ptr**: hedef örnek kimliği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-810">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="1e11e-811">**objlnk_ptr**: hedef nesne bağlantı değerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-811">**objlnk_ptr**: Pointer to the destination Object Link value.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-812">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-812">Return Values</span></span>

- <span data-ttu-id="1e11e-813">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-813">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-814">**NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="1e11e-814">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="1e11e-815">**NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri bir nesne bağlantı değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-815">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not an Object Link value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_opaque"></a><span data-ttu-id="1e11e-816">nx_lwm2m_resource_multiple_get_opaque</span><span class="sxs-lookup"><span data-stu-id="1e11e-816">nx_lwm2m_resource_multiple_get_opaque</span></span>

<span data-ttu-id="1e11e-817">Donuk birden çok kaynak örneğinin değerini Al</span><span class="sxs-lookup"><span data-stu-id="1e11e-817">Get the value of an Opaque Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-818">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-818">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_opaque(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const VOID **opaque_ptr_ptr,
    UINT *opaque_length_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-819">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-819">Description</span></span>

<span data-ttu-id="1e11e-820">Hizmet, bir donuk kaynak örneğinin değerini birden çok kaynaktan alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-820">The service retrieves the value of an Opaque Resource Instance from a Multiple Resource.</span></span>

<span data-ttu-id="1e11e-821">Donuk bir kaynak değeri, arabelleğin ve uzunluğun bir işaretçisinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="1e11e-821">An opaque resource value consists of a pointer to a buffer and a length.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-822">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-822">Parameters</span></span>

- <span data-ttu-id="1e11e-823">**değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-823">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="1e11e-824">**Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.</span><span class="sxs-lookup"><span data-stu-id="1e11e-824">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="1e11e-825">**instance_id_ptr**: hedef örnek kimliği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-825">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="1e11e-826">**opaque_ptr_ptr**: hedef donuk arabellek işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-826">**opaque_ptr_ptr**: Pointer to the destination opaque buffer pointer.</span></span>
- <span data-ttu-id="1e11e-827">**opaque_length_ptr**: hedef donuk arabellek uzunluğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-827">**opaque_length_ptr**: Pointer to the destination opaque buffer length.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-828">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-828">Return Values</span></span>

- <span data-ttu-id="1e11e-829">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-829">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-830">**NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="1e11e-830">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="1e11e-831">**NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya kaynak değeri donuk bir değer değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-831">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the resource value is not an Opaque value.</span></span>

## <a name="nx_lwm2m_resource_multiple_get_string"></a><span data-ttu-id="1e11e-832">nx_lwm2m_resource_multiple_get_string</span><span class="sxs-lookup"><span data-stu-id="1e11e-832">nx_lwm2m_resource_multiple_get_string</span></span>

<span data-ttu-id="1e11e-833">Birden çok kaynak örneğinin bir dize değerini alır</span><span class="sxs-lookup"><span data-stu-id="1e11e-833">Get the value of a String Multiple Resource Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1e11e-834">Prototype</span><span class="sxs-lookup"><span data-stu-id="1e11e-834">Prototype</span></span>

```c
UINT nx_lwm2m_resource_multiple_get_string(const NX_LWM2M_RESOURCE *value,
    int index, NX_LWM2M_ID *instance_id_ptr, const CHAR **string_ptr_ptr,
    UINT *string_length_ptr);
```

### <a name="description"></a><span data-ttu-id="1e11e-835">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e11e-835">Description</span></span>

<span data-ttu-id="1e11e-836">Hizmet, bir dize kaynak örneğinin değerini birden çok kaynaktan alır.</span><span class="sxs-lookup"><span data-stu-id="1e11e-836">The service retrieves the value of a String Resource Instance from a Multiple Resource.</span></span>

### <a name="parameters"></a><span data-ttu-id="1e11e-837">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1e11e-837">Parameters</span></span>

- <span data-ttu-id="1e11e-838">**değer**: birden çok kaynak değeri açıklamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-838">**value**: Pointer to the Multiple Resource value description.</span></span>
- <span data-ttu-id="1e11e-839">**Dizin**: kaynak değer dizisinde alınacak Örneğin dizini.</span><span class="sxs-lookup"><span data-stu-id="1e11e-839">**index**: Index of the Instance to retrieve in the Resource value array.</span></span>
- <span data-ttu-id="1e11e-840">**instance_id_ptr**: hedef örnek kimliği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-840">**instance_id_ptr**: Pointer to the destination Instance ID.</span></span>
- <span data-ttu-id="1e11e-841">**string_ptr_ptr**: hedef dize işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-841">**string_ptr_ptr**: Pointer to the destination string pointer.</span></span>
- <span data-ttu-id="1e11e-842">**string_length_ptr**: hedef dize uzunluğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="1e11e-842">**string_length_ptr**: Pointer to the destination string length.</span></span> <span data-ttu-id="1e11e-843">Dize null sonlandırılırsa NULL olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e11e-843">Can be NULL if the string is null-terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="1e11e-844">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="1e11e-844">Return Values</span></span>

- <span data-ttu-id="1e11e-845">**NX_SUCCESS**: başarılı işlem.</span><span class="sxs-lookup"><span data-stu-id="1e11e-845">**NX_SUCCESS**: Successful operation.</span></span>
- <span data-ttu-id="1e11e-846">**NX_LWM2M_BAD_PARAMETER**: Dizin aralık dışında.</span><span class="sxs-lookup"><span data-stu-id="1e11e-846">**NX_LWM2M_BAD_PARAMETER**: The index is out of range.</span></span>
- <span data-ttu-id="1e11e-847">**NX_LWM2M_BAD_ENCODING**: kaynak birden fazla kaynak değil veya örnek değeri bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1e11e-847">**NX_LWM2M_BAD_ENCODING**: The resource is not a multiple resource, or the instance value is not a String value.</span></span>
