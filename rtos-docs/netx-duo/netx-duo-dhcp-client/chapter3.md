---
title: Bölüm 3-Azure RTOS NetX Duo DHCP Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX Duo DHCP Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f143a443221ae08848316a458a630a0790108198
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826117"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dhcp-client-services"></a><span data-ttu-id="50d63-103">Bölüm 3-Azure RTOS NetX Duo DHCP Istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="50d63-103">Chapter 3 - Description of Azure RTOS NetX Duo DHCP Client services</span></span>

<span data-ttu-id="50d63-104">Bu bölüm, tüm Azure RTOS NetX Duo DHCP Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="50d63-104">This chapter contains a description of all Azure RTOS NetX Duo DHCP Client services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="50d63-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="50d63-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="50d63-106">**nx_dhcp_create**: *DHCP örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="50d63-106">**nx_dhcp_create**: *Create a DHCP instance*</span></span>
- <span data-ttu-id="50d63-107">**nx_dhcp_clear_broadcast_flag**: *istemci iletilerinde yayın bayrağını temizle*</span><span class="sxs-lookup"><span data-stu-id="50d63-107">**nx_dhcp_clear_broadcast_flag**: *Clear broadcast flag on Client messages*</span></span>
- <span data-ttu-id="50d63-108">**nx_dhcp_delete**: *bir DHCP örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="50d63-108">**nx_dhcp_delete**: *Delete a DHCP instance*</span></span>
- <span data-ttu-id="50d63-109">**nx_dhcp_force_renew**: *zorla yenileme iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="50d63-109">**nx_dhcp_force_renew**: *Send a force renew message*</span></span>
- <span data-ttu-id="50d63-110">**nx_dhcp_packet_pool_set**: *DHCP istemci paket havuzunu ayarlama*</span><span class="sxs-lookup"><span data-stu-id="50d63-110">**nx_dhcp_packet_pool_set**: *Set the DHCP Client packet pool*</span></span>
- <span data-ttu-id="50d63-111">**nx_dhcp_decline**: *sunucuya reddetme iletisi* gönder</span><span class="sxs-lookup"><span data-stu-id="50d63-111">**nx_dhcp_decline**: Send *Decline message to server*</span></span>
- <span data-ttu-id="50d63-112">**nx_dhcp_release**: *sunucuya sürüm iletisi* gönder</span><span class="sxs-lookup"><span data-stu-id="50d63-112">**nx_dhcp_release**: Send *Release message to server*</span></span>
- <span data-ttu-id="50d63-113">**nx_dhcp_reinitialize**: *DHCP istemci ağı parametrelerini temizle*</span><span class="sxs-lookup"><span data-stu-id="50d63-113">**nx_dhcp_reinitialize**: *Clear DHCP client network parameters*</span></span>
- <span data-ttu-id="50d63-114">**nx_dhcp_request_client_ip**: *belirli bir IP adresi belirtin*</span><span class="sxs-lookup"><span data-stu-id="50d63-114">**nx_dhcp_request_client_ip**: *Specify a specific IP address*</span></span>
- <span data-ttu-id="50d63-115">**nx_dhcp_send_request**: *sunucuya DHCP iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="50d63-115">**nx_dhcp_send_request**: *Send DHCP message to server*</span></span>
- <span data-ttu-id="50d63-116">**nx_dhcp_start**: *DHCP istemci işlemesini Başlat*</span><span class="sxs-lookup"><span data-stu-id="50d63-116">**nx_dhcp_start**: *Start the DHCP Client processing*</span></span>
- <span data-ttu-id="50d63-117">**nx_dhcp_stop**: *DHCP istemci işlemesini durdur*</span><span class="sxs-lookup"><span data-stu-id="50d63-117">**nx_dhcp_stop**: *Stop the DHCP Client processing*</span></span>
- <span data-ttu-id="50d63-118">**nx_dhcp_set_interface_index**: *arabirimi DHCP istemcisini çalıştıracak şekilde ayarlama*</span><span class="sxs-lookup"><span data-stu-id="50d63-118">**nx_dhcp_set_interface_index**: *Set the interface to run DHCP Client*</span></span>
- <span data-ttu-id="50d63-119">**nx_dhcp_server_address_get**: *DHCP sunucusu IP adresini al*</span><span class="sxs-lookup"><span data-stu-id="50d63-119">**nx_dhcp_server_address_get**: *Get the DHCP server IP address*</span></span>
- <span data-ttu-id="50d63-120">**nx_dhcp_state_change_notify**: *DHCP durumu değiştiğinde geri çağırma işlevini ayarla*</span><span class="sxs-lookup"><span data-stu-id="50d63-120">**nx_dhcp_state_change_notify**: *Set the callback function when DHCP state changes*</span></span>
- <span data-ttu-id="50d63-121">**nx_dhcp_user_option_retrieve**: *belirtilen DHCP seçeneğini Al*</span><span class="sxs-lookup"><span data-stu-id="50d63-121">**nx_dhcp_user_option_retrieve**: *Retrieve the specified DHCP option*</span></span>
- <span data-ttu-id="50d63-122">**nx_dhcp_user_option_convert**: *dört baytı ulong 'a Dönüştür*</span><span class="sxs-lookup"><span data-stu-id="50d63-122">**nx_dhcp_user_option_convert**: *Convert four bytes to ULONG*</span></span>

<span data-ttu-id="50d63-123">Arabirime özgü DHCP Istemci Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="50d63-123">Interface specific DHCP Client services:</span></span>
 
- <span data-ttu-id="50d63-124">**nx_dhcp_interface_clear_broadcast_flag**: *belirtilen arabirimdeki istemci iletilerinde yayın bayrağını temizle*</span><span class="sxs-lookup"><span data-stu-id="50d63-124">**nx_dhcp_interface_clear_broadcast_flag**: *Clear broadcast flag on Client messages on specified interface*</span></span>
- <span data-ttu-id="50d63-125">**nx_dhcp_interface_enable**: *belirtilen arabirimde DHCP çalıştırmak için arabirimi etkinleştir*</span><span class="sxs-lookup"><span data-stu-id="50d63-125">**nx_dhcp_interface_enable**: *Enable interface to run DHCP on the specified interface*</span></span>
- <span data-ttu-id="50d63-126">**nx_dhcp_interface_disable**: *belirtilen arabirimde DHCP çalıştırmak için arabirimi devre dışı bırak*</span><span class="sxs-lookup"><span data-stu-id="50d63-126">**nx_dhcp_interface_disable**: *Disable interface to run DHCP on the specified interface*</span></span>
- <span data-ttu-id="50d63-127">**nx_dhcp_interface_decline**: *belirtilen arabirimdeki sunucuya reddetme iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="50d63-127">**nx_dhcp_interface_decline**: *Send Decline message to server on the specified interface*</span></span>
- <span data-ttu-id="50d63-128">**nx_dhcp_interface_force_renew**: *belirtilen arabirimde zorla yenileme iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="50d63-128">**nx_dhcp_interface_force_renew**: *Send a force renew message on the specified interface*</span></span>
- <span data-ttu-id="50d63-129">**nx_dhcp_interface_reinitialize**: *belirtilen arabirimdeki DHCP istemci ağ parametrelerini temizle*</span><span class="sxs-lookup"><span data-stu-id="50d63-129">**nx_dhcp_interface_reinitialize**: *Clear DHCP client network parameters on the specified interface*</span></span>
- <span data-ttu-id="50d63-130">**nx_dhcp_interface_release**: *belirtilen arabirimdeki sunucuya sürüm iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="50d63-130">**nx_dhcp_interface_release**: *Send Release message to server on the specified interface*</span></span>
- <span data-ttu-id="50d63-131">**nx_dhcp_interface_request_client_ip**: *belirtilen ARABIRIMDE belirli bir IP adresi belirtin*</span><span class="sxs-lookup"><span data-stu-id="50d63-131">**nx_dhcp_interface_request_client_ip**: *Specify a specific IP address on the specified interface*</span></span>
- <span data-ttu-id="50d63-132">**nx_dhcp_interface_send_request**: *belirtilen arabirimdeki DHCP iletisini sunucuya gönderin*</span><span class="sxs-lookup"><span data-stu-id="50d63-132">**nx_dhcp_interface_send_request**: *Send DHCP message to server on the specified interface*</span></span>
- <span data-ttu-id="50d63-133">**nx_dhcp_interface_server_address_get**: *belirtilen ARABIRIMDEKI DHCP sunucusu IP adresini al*</span><span class="sxs-lookup"><span data-stu-id="50d63-133">**nx_dhcp_interface_server_address_get**: *Get the DHCP server IP address on the specified interface*</span></span>
- <span data-ttu-id="50d63-134">**nx_dhcp_interface_start**: *belirtilen arabirimde DHCP istemci işlemesini Başlat*</span><span class="sxs-lookup"><span data-stu-id="50d63-134">**nx_dhcp_interface_start**: *Start the DHCP Client processing on the specified interface*</span></span>
- <span data-ttu-id="50d63-135">**nx_dhcp_interface_stop**: *belirtilen arabirimdeki DHCP istemci işlemesini durdur*</span><span class="sxs-lookup"><span data-stu-id="50d63-135">**nx_dhcp_interface_stop**: *Stop the DHCP Client processing on the specified interface*</span></span>
- <span data-ttu-id="50d63-136">**nx_dhcp_interface_state_change_notify**: *belirtilen arabirimdeki DHCP durumu değiştiğinde geri çağırma işlevini ayarla*</span><span class="sxs-lookup"><span data-stu-id="50d63-136">**nx_dhcp_interface_state_change_notify**: *Set the callback function when DHCP state changes on the specified interface*</span></span>
- <span data-ttu-id="50d63-137">**nx_dhcp_interface_user_option_retrieve**: belirtilen *arabirimde belirtilen DHCP seçeneğini Al*</span><span class="sxs-lookup"><span data-stu-id="50d63-137">**nx_dhcp_interface_user_option_retrieve**: *Retrieve the specified DHCP option on the specified interface*</span></span>

<span data-ttu-id="50d63-138">NX_DHCP_CLIENT_RESORE_STATE tanımlanmışsa DHCP Istemci Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="50d63-138">DHCP Client Services if NX_DHCP_CLIENT_RESORE_STATE is defined:</span></span>

- <span data-ttu-id="50d63-139">**nx_dhcp_resume**: *önceden oluşturulmuş DHCP istemci durumunu sürdürür*</span><span class="sxs-lookup"><span data-stu-id="50d63-139">**nx_dhcp_resume**: *Resume previously established DHCP Client state*</span></span>
- <span data-ttu-id="50d63-140">**nx_dhcp_suspend**: *DHCP istemci durumunu işlemeyi askıya al*</span><span class="sxs-lookup"><span data-stu-id="50d63-140">**nx_dhcp_suspend**: *Suspend processing the DHCP Client state*</span></span>
- <span data-ttu-id="50d63-141">**nx_dhcp_client_get_record**: *DHCP istemci durumunun kaydını oluşturma*</span><span class="sxs-lookup"><span data-stu-id="50d63-141">**nx_dhcp_client_get_record**: *Create a record of the DHCP Client state*</span></span>
- <span data-ttu-id="50d63-142">**nx_dhcp_client_restore_record**: *daha önce KAYDEDILMIŞ bir kaydı DHCP istemcisine geri yükleme*</span><span class="sxs-lookup"><span data-stu-id="50d63-142">**nx_dhcp_client_restore_record**: *Restore a previously saved record to the DHCP Client*</span></span>
- <span data-ttu-id="50d63-143">**nx_dhcp_client_update_time_remaining**: *geçerli DHCP durumunda kalan süreyi Güncelleştir*</span><span class="sxs-lookup"><span data-stu-id="50d63-143">**nx_dhcp_client_update_time_remaining**: *Update the time remaining in the current DHCP state*</span></span>

<span data-ttu-id="50d63-144">NX_DHCP_CLIENT_RESORE_STATE tanımlanmışsa arabirime özgü DHCP Istemci Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="50d63-144">Interface Specific DHCP Client Services if NX_DHCP_CLIENT_RESORE_STATE is defined:</span></span>

- <span data-ttu-id="50d63-145">**nx_dhcp_client_interface_get_record**: *belirtilen arabirimde DHCP istemci durumunun bir kaydını oluşturun*</span><span class="sxs-lookup"><span data-stu-id="50d63-145">**nx_dhcp_client_interface_get_record**: *Create a record of the DHCP Client state on the specified interface*</span></span>
- <span data-ttu-id="50d63-146">**nx_dhcp_client_interface_restore_record**: *önceden kaydedilmiş bir kaydı belirtilen arabirimdeki DHCP istemcisine geri yükleme*</span><span class="sxs-lookup"><span data-stu-id="50d63-146">**nx_dhcp_client_interface_restore_record**: *Restore a previously saved record to the DHCP Client on the specified interface*</span></span>
- <span data-ttu-id="50d63-147">**nx_dhcp_client_interface_update_time_remaining**: *BELIRTILEN arabirimdeki geçerli DHCP durumunda kalan süreyi Güncelleştir*</span><span class="sxs-lookup"><span data-stu-id="50d63-147">**nx_dhcp_client_interface_update_time_remaining**: *Update the time remaining in the current DHCP state on the specified interface*</span></span>

## <a name="nx_dhcp_create"></a><span data-ttu-id="50d63-148">nx_dhcp_create</span><span class="sxs-lookup"><span data-stu-id="50d63-148">nx_dhcp_create</span></span>

<span data-ttu-id="50d63-149">DHCP örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="50d63-149">Create a DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-150">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-150">Prototype</span></span>

```c
UINT nx_dhcp_create(NX_DHCP *dhcp_ptr, NX_IP *ip_ptr, CHAR *name_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-151">Description</span></span>

<span data-ttu-id="50d63-152">Bu hizmet, önceden oluşturulan IP örneği için bir DHCP örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="50d63-152">This service creates a DHCP instance for the previously created IP instance.</span></span> <span data-ttu-id="50d63-153">Varsayılan olarak, birincil arabirim DHCP çalıştırmak için etkinleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="50d63-153">By default the primary interface is enabled for running DHCP.</span></span> <span data-ttu-id="50d63-154">DHCP Istemcisinin NetX Duo uygulamasında kullanılmayan ad girişi, ana bilgisayar adları için RFC 1035 ölçütlerine uymalıdır.</span><span class="sxs-lookup"><span data-stu-id="50d63-154">The name input, while not used in the NetX Duo implementation of DHCP Client, must follow RFC 1035 criteria for host names.</span></span> <span data-ttu-id="50d63-155">Toplam uzunluk 255 karakteri aşmamalıdır, noktalarla ayrılmış etiketlerin bir harfle başlaması ve bir harf ya da sayıyla bitmesi gerekir ve kısa çizgi içeremez, ancak alfasayısal olmayan başka karakterler içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="50d63-155">The total length must not exceed 255 characters, the labels separate by dots must begin with a letter, and end with a letter or number, and may contain hyphens but no other non-alphanumeric character.</span></span>

<span data-ttu-id="50d63-156">Uygulama, DHCP 'nin IP örneğiyle kaydedilmiş başka bir arabirimi çalıştırmak istiyorsanız ( *nx_ip_interface_attach* kullanarak), uygulama, DHCP 'yi yalnızca o arabirim üzerinde çalıştırmak için *nx_dhcp_set_interface_index* ÇAĞıRABILIR veya bu arabirimde DHCP çalıştırmak için *nx_dhcp_interface_enable* .</span><span class="sxs-lookup"><span data-stu-id="50d63-156">If the application would like to run DHCP another interface registered with the IP instance, (using *nx_ip_interface_attach*), the application can call *nx_dhcp_set_interface_index* to run DHCP on just that interface, or *nx_dhcp_interface_enable* to run DHCP on that interface as well.</span></span> <span data-ttu-id="50d63-157">Daha fazla ayrıntı için bu hizmetlerin açıklamasına bakın.</span><span class="sxs-lookup"><span data-stu-id="50d63-157">See description of these services for more details.</span></span>

>[!NOTE]
> <span data-ttu-id="50d63-158">Uygulamanın, DHCP Istemci paket havuzu yükünün, RFC 2131 Bölüm 2 tarafından belirtilen en düşük DHCP ileti boyutunu (548 bayt DHCP ileti verilerinin yanı sıra UDP, IP ve fiziksel ağ çerçeve üstbilgileri) destekleyebileceğine emin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50d63-158">The application must make sure the DHCP Client packet pool payload can support the minimum DHCP message size specified by the RFC 2131 Section 2 (548 bytes of DHCP message data plus UDP, IP and physical network frame headers).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-159">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-159">Input Parameters</span></span>

- <span data-ttu-id="50d63-160">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-160">**dhcp_ptr**: Pointer to DHCP control block.</span></span> 
- <span data-ttu-id="50d63-161">**ip_ptr**: daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-161">**ip_ptr**: Pointer to previously created IP instance.</span></span>  
- <span data-ttu-id="50d63-162">**name_ptr**: DHCP örneği için ana bilgisayar adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-162">**name_ptr**: Pointer to host name for DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-163">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-163">Return Values</span></span>

- <span data-ttu-id="50d63-164">**NX_SUCCESS**: (0x00) başarılı DHCP oluşturma</span><span class="sxs-lookup"><span data-stu-id="50d63-164">**NX_SUCCESS**: (0x00) Successful DHCP create</span></span>
- <span data-ttu-id="50d63-165">**NX_DHCP_INVALID_NAME**: (0Xa8) geçersiz konak adı</span><span class="sxs-lookup"><span data-stu-id="50d63-165">**NX_DHCP_INVALID_NAME**: (0xA8) Invalid host name</span></span>
- <span data-ttu-id="50d63-166">**NX_DHCP_INVALID_PAYLOAD**: (0x9C) yük DHCP iletisi için çok küçük</span><span class="sxs-lookup"><span data-stu-id="50d63-166">**NX_DHCP_INVALID_PAYLOAD**: (0x9C) Payload too small for DHCP message</span></span>
- <span data-ttu-id="50d63-167">NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-167">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-168">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-168">Allowed From</span></span>

<span data-ttu-id="50d63-169">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="50d63-169">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="50d63-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-170">Example</span></span>

```c
/* Create a DHCP instance.  */
status =  nx_dhcp_create(&my_dhcp, &my_ip, "My-DHCP");

/* If status is NX_SUCCESS a DHCP instance was successfully created.  */
```

## <a name="nx_dhcp_interface_enable"></a><span data-ttu-id="50d63-171">nx_dhcp_interface_enable</span><span class="sxs-lookup"><span data-stu-id="50d63-171">nx_dhcp_interface_enable</span></span>

<span data-ttu-id="50d63-172">Belirtilen arabirimi DHCP çalıştırmak için etkinleştir</span><span class="sxs-lookup"><span data-stu-id="50d63-172">Enable the specified interface to run DHCP</span></span> 

### <a name="prototype"></a><span data-ttu-id="50d63-173">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-173">Prototype</span></span>

```c
UINT nx_dhcp_interface_enable(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="50d63-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-174">Description</span></span>

<span data-ttu-id="50d63-175">Bu hizmet, DHCP çalıştırmak için belirtilen arabirimi sunar.</span><span class="sxs-lookup"><span data-stu-id="50d63-175">This service enables the specified interface for running DHCP.</span></span> <span data-ttu-id="50d63-176">Varsayılan olarak, birincil arabirim DHCP Istemcisi için etkinleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="50d63-176">By default the primary interface is enabled for DHCP Client.</span></span> <span data-ttu-id="50d63-177">Bu noktada, DHCP, *nx_dhcp_interface_start* çağırarak veya tüm ETKINLEŞTIRILMIŞ arabirimlerde DHCP 'yi başlatmak için bu arabirim üzerinde başlatılabilir *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="50d63-177">At this point, DHCP can be started on this interface either by calling *nx_dhcp_interface_start* or to start DHCP on all enabled interfaces *nx_dhcp_start*.</span></span>

>[!NOTE] 
> <span data-ttu-id="50d63-178">Uygulamanın, nx_ip_interface_attach kullanarak bu arabirimi IP örneğiyle kaydetmesi gerekir *.*</span><span class="sxs-lookup"><span data-stu-id="50d63-178">The application must first register this interface with the IP instance, using *nx_ip_interface_attach.*</span></span>

<span data-ttu-id="50d63-179">Ayrıca, bu arabirimi etkin arabirimler listesine eklemek için kullanılabilir bir DHCP Istemci arabirimi ' Record ' olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="50d63-179">Further, there must be an available DHCP Client interface ‘record’ to add this interface to the list of enabled interfaces.</span></span> <span data-ttu-id="50d63-180">Varsayılan olarak NX_DHCP_CLIENT_MAX_RECORDS 1 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="50d63-180">By default NX_DHCP_CLIENT_MAX_RECORDS is defined to 1.</span></span> <span data-ttu-id="50d63-181">DHCP Istemcisini aynı anda çalıştırmak için beklenen en fazla arabirim sayısına bu seçeneği ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="50d63-181">Set this option to the maximum number of interfaces expected to run DHCP Client simultaneously.</span></span> <span data-ttu-id="50d63-182">Genellikle NX_DHCP_CLIENT_MAX_RECORDS, NX_MAX_PHYSICAL_INTERFACES eşit olur; Ancak, bir cihazda DHCP Istemcisi çalıştırmak beklediğinden daha fazla fiziksel arabirim varsa, bu sayıdan daha az NX_DHCP_CLIENT_MAX_RECORDS ayarlayarak bellek tasarrufu sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="50d63-182">Typically NX_DHCP_CLIENT_MAX_RECORDS will equal NX_MAX_PHYSICAL_INTERFACES; however, if a device has more physical interfaces than it expects to run DHCP Client, it can save memory by setting NX_DHCP_CLIENT_MAX_RECORDS to less than that number.</span></span> <span data-ttu-id="50d63-183">DHCP Istemci arabirimi kayıtlarıyla bir fiziksel arabirimlerin eşleştirmesi bir tane değildir.</span><span class="sxs-lookup"><span data-stu-id="50d63-183">There is not a one to one mapping of physical interfaces with DHCP Client interface records.</span></span>

<span data-ttu-id="50d63-184">Bu hizmet ve *nx_dhcp_set_interface_index* arasındaki fark, ikinci olarak yalnızca tek BIR arabirim DHCP 'yi çalıştıracak şekilde ayarlıyor. bu hizmet, BELIRTILEN arabirimi DHCP Için etkinleştirilen istemci arabirimleri listesine ekler.</span><span class="sxs-lookup"><span data-stu-id="50d63-184">The difference between this service and *nx_dhcp_set_interface_index* is the latter sets only a single interface to run DHCP whereas this service simply adds the specified interface to the list of Client interfaces enabled for DHCP.</span></span>

<span data-ttu-id="50d63-185">DHCP arabirimini devre dışı bırakmak için uygulama</span><span class="sxs-lookup"><span data-stu-id="50d63-185">To disable an interface for DHCP, the application can call the</span></span>

<span data-ttu-id="50d63-186">*nx_dhcp_interface_disable* hizmet.</span><span class="sxs-lookup"><span data-stu-id="50d63-186">*nx_dhcp_interface_disable* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-187">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-187">Input Parameters</span></span>

- <span data-ttu-id="50d63-188">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-188">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="50d63-189">**interface_index**: üzerinde DHCP 'yi etkinleştirmek için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-189">**interface_index**: Index of interface to enable DHCP on</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-190">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-190">Return Values</span></span>

- <span data-ttu-id="50d63-191">**NX_SUCCESS**: (0x00) başarılı DHCP etkin</span><span class="sxs-lookup"><span data-stu-id="50d63-191">**NX_SUCCESS**: (0x00) Successful DHCP enable</span></span>
- <span data-ttu-id="50d63-192">**NX_DHCP_NO_RECORDS_AVAILABLE**: (0xa7) başka BIR arabirimin DHCP için etkinleştirilmesi için kullanılabilir kayıt yok</span><span class="sxs-lookup"><span data-stu-id="50d63-192">**NX_DHCP_NO_RECORDS_AVAILABLE**: (0xA7) No record available for another Interface to be enabled for DHCP</span></span>
- <span data-ttu-id="50d63-193">**NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) arabirim DHCP için etkinleştirildi</span><span class="sxs-lookup"><span data-stu-id="50d63-193">**NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) Interface enabled for DHCP</span></span>
- <span data-ttu-id="50d63-194">NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-194">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="50d63-195">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-195">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-196">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-196">Allowed From</span></span>

<span data-ttu-id="50d63-197">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="50d63-197">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="50d63-198">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-198">Example</span></span>

```c
/* Enable DHCP on a secondary interface. It is already enabled on the primary 
   interface.  NX_DHCP_CLIENT_MAX_RECORDS is set to 2. */

status =  nx_dhcp_interface_enable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface was successfully enabled.  */


status = nx_dhcp_start(&my_dhcp);
/* If status is NX_SUCCESS DHCP is running on interface 0 and 1.  */
```

## <a name="nx_dhcp_interface_disable"></a><span data-ttu-id="50d63-199">nx_dhcp_interface_disable</span><span class="sxs-lookup"><span data-stu-id="50d63-199">nx_dhcp_interface_disable</span></span>

<span data-ttu-id="50d63-200">DHCP çalıştırmak için belirtilen arabirimi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="50d63-200">Disable the specified interface to run DHCP</span></span> 

### <a name="prototype"></a><span data-ttu-id="50d63-201">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-201">Prototype</span></span>

```c

UINT nx_dhcp_interface_disable(NX_DHCP *dhcp_ptr, 
                               UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="50d63-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-202">Description</span></span>

<span data-ttu-id="50d63-203">Bu hizmet, DHCP çalıştırmak için belirtilen arabirimi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="50d63-203">This service disables the specified interface for running DHCP.</span></span> <span data-ttu-id="50d63-204">Bu arabirimdeki DHCP Istemcisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="50d63-204">It reinitializes the DHCP Client on this interface.</span></span>

<span data-ttu-id="50d63-205">DHCP Istemcisini yeniden başlatmak için, uygulamanın *nx_dhcp_interface_enable* kullanarak arabirimi yeniden etkinleştirmeleri ve *nx_dhcp_interface_start* çağırarak DHCP 'yi yeniden başlatması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50d63-205">To restart the DHCP Client the application must re-enable the interface using *nx_dhcp_interface_enable* and restart DHCP by calling *nx_dhcp_interface_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-206">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-206">Input Parameters</span></span>

- <span data-ttu-id="50d63-207">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-207">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="50d63-208">**interface_index**: DHCP 'yi devre dışı bırakmak için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-208">**interface_index**: Index of interface to disable DHCP on</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-209">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-209">Return Values</span></span>

- <span data-ttu-id="50d63-210">**NX_SUCCESS**: (0x00) başarılı DHCP oluşturma</span><span class="sxs-lookup"><span data-stu-id="50d63-210">**NX_SUCCESS**: (0x00) Successful DHCP create</span></span>
- <span data-ttu-id="50d63-211">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="50d63-211">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="50d63-212">NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-212">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="50d63-213">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="50d63-213">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="50d63-214">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-214">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-215">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-215">Allowed From</span></span>

<span data-ttu-id="50d63-216">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-216">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-217">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-217">Example</span></span>

```c
/* Disable DHCP on a secondary interface. */

status =  nx_dhcp_interface_disable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface is successfully disabled.  */
```
## <a name="nx_dhcp_clear_broadcast_flag"></a><span data-ttu-id="50d63-218">nx_dhcp_clear_broadcast_flag</span><span class="sxs-lookup"><span data-stu-id="50d63-218">nx_dhcp_clear_broadcast_flag</span></span>

<span data-ttu-id="50d63-219">DHCP yayın bayrağını ayarlama</span><span class="sxs-lookup"><span data-stu-id="50d63-219">Set the DHCP broadcast flag</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-220">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-220">Prototype</span></span>

```c
UINT nx_dhcp_clear_broadcast_flag(NX_DHCP *dhcp_ptr, UINT clear_flag);
```

### <a name="description"></a><span data-ttu-id="50d63-221">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-221">Description</span></span>

<span data-ttu-id="50d63-222">Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerin DHCP ileti üst bilgisini ayarlar veya temizler.</span><span class="sxs-lookup"><span data-stu-id="50d63-222">This service sets or clears the broadcast flag the DHCP message header for all interfaces enabled for DHCP.</span></span> <span data-ttu-id="50d63-223">Istemci bir IP adresine sahip olmadığından, bazı DHCP iletileri (örneğin, bul) yayın bayrağı Broadcast olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="50d63-223">For some DHCP messages (e.g. DISCOVER) the broadcast flag is set to broadcast because the Client does not have an IP address.</span></span>

<span data-ttu-id="50d63-224">clear_flag değerleri:</span><span class="sxs-lookup"><span data-stu-id="50d63-224">clear_flag values:</span></span> 

- <span data-ttu-id="50d63-225">**NX_TRUE**: yayın bayrağı temizlendi (tek noktaya yayın yanıtı iste)</span><span class="sxs-lookup"><span data-stu-id="50d63-225">**NX_TRUE**: broadcast flag is cleared (request unicast response)</span></span>
- <span data-ttu-id="50d63-226">**NX_FALSE**: yayın bayrağı ayarlandı (Yayın yanıtı iste)</span><span class="sxs-lookup"><span data-stu-id="50d63-226">**NX_FALSE**: broadcast flag is set (request broadcast response)</span></span>

<span data-ttu-id="50d63-227">Bu hizmet, yönlendiricinin, iletme yayını iletilerini reddettiği DHCP sunucusuna ulaşmak için bir yönlendiriciden geçmesi gereken DHCP Istemcilerine yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="50d63-227">This service is intended for DHCP Clients that must go through a router to get to the DHCP Server, where the router rejects forwarding broadcast messages.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-228">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-228">Input Parameters</span></span>

- <span data-ttu-id="50d63-229">**dhcp_ptr**: DHCP denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-229">**dhcp_ptr**: Pointer to DHCP control block</span></span>  
- <span data-ttu-id="50d63-230">**clear_flag**: yayın bayrağını ayarlanacak değer</span><span class="sxs-lookup"><span data-stu-id="50d63-230">**clear_flag**: Value to set the broadcast flag to</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-231">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-231">Return Values</span></span>

- <span data-ttu-id="50d63-232">**NX_SUCCESS**: (0x00) bayrağı başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="50d63-232">**NX_SUCCESS**: (0x00) Successfully set flag</span></span>
- <span data-ttu-id="50d63-233">NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-233">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-234">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-234">Allowed From</span></span>

<span data-ttu-id="50d63-235">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="50d63-235">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="50d63-236">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-236">Example</span></span>

```c
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a  
    unicast response).  */
status =  nx_dhcp_clear_broadcast_flag(&my_dhcp, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated.  */
```

## <a name="nx_dhcp_interface_clear_broadcast_flag"></a><span data-ttu-id="50d63-237">nx_dhcp_interface_clear_broadcast_flag</span><span class="sxs-lookup"><span data-stu-id="50d63-237">nx_dhcp_interface_clear_broadcast_flag</span></span>

<span data-ttu-id="50d63-238">Belirtilen arabirimdeki yayın bayrağını ayarla veya temizle</span><span class="sxs-lookup"><span data-stu-id="50d63-238">Set or clear the broadcast flag on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-239">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-239">Prototype</span></span>

```c
UINT nx_dhcp_interface_clear_broadcast_flag(NX_DHCP *dhcp_ptr, 
                                            UINT interface_index, 
                                            UINT clear_flag);
```

### <a name="description"></a><span data-ttu-id="50d63-240">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-240">Description</span></span>

<span data-ttu-id="50d63-241">Bu hizmet, DHCP Istemci ana bilgisayar uygulamasının, DHCP Istemci iletilerindeki yayın bayrağını belirtilen arabirimdeki DHCP sunucusuna ayarlamasını veya temizlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="50d63-241">This service enables the DHCP Client host application to set or clear the broadcast flag in DHCP Client messages to the DHCP Server on the specified interface.</span></span> <span data-ttu-id="50d63-242">Daha fazla bilgi için bkz. **nx_dhcp_clear_broadcast_flag**.</span><span class="sxs-lookup"><span data-stu-id="50d63-242">For more details see **nx_dhcp_clear_broadcast_flag**.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-243">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-243">Input Parameters</span></span>

- <span data-ttu-id="50d63-244">**dhcp_ptr**: DHCP denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-244">**dhcp_ptr**: Pointer to DHCP control block</span></span>
- <span data-ttu-id="50d63-245">**interface_index**: yayın bayrağını ayarlamak için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-245">**interface_index**: Index of interface to set the broadcast flag</span></span>
- <span data-ttu-id="50d63-246">**clear_flag**: yayın bayrağını ayarlanacak değer</span><span class="sxs-lookup"><span data-stu-id="50d63-246">**clear_flag**: Value to set the broadcast flag to</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-247">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-247">Return Values</span></span>

- <span data-ttu-id="50d63-248">**NX_SUCCESS**: (0x00) bayrağı başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="50d63-248">**NX_SUCCESS**: (0x00) Successfully set flag</span></span>
- <span data-ttu-id="50d63-249">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="50d63-249">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="50d63-250">NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-250">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="50d63-251">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-251">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-252">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-252">Allowed From</span></span>

<span data-ttu-id="50d63-253">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="50d63-253">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="50d63-254">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-254">Example</span></span>

```c
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a 
   unicast response) on a previously attached secondary interface.  */

iface_index = 1;

status =  nx_dhcp_interface_clear_broadcast_flag(&my_dhcp, iface_index, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated.  */
```

## <a name="nx_dhcp_delete"></a><span data-ttu-id="50d63-255">nx_dhcp_delete</span><span class="sxs-lookup"><span data-stu-id="50d63-255">nx_dhcp_delete</span></span>

<span data-ttu-id="50d63-256">DHCP örneğini silme</span><span class="sxs-lookup"><span data-stu-id="50d63-256">Delete a DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-257">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-257">Prototype</span></span>

```c
UINT nx_dhcp_delete(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-258">Description</span></span>

<span data-ttu-id="50d63-259">Bu hizmet önceden oluşturulmuş bir DHCP örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="50d63-259">This service deletes a previously created DHCP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-260">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-260">Input Parameters</span></span>

- <span data-ttu-id="50d63-261">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-261">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-262">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-262">Return Values</span></span>

- <span data-ttu-id="50d63-263">**NX_SUCCESS**: (0x00) başarılı DHCP silme.</span><span class="sxs-lookup"><span data-stu-id="50d63-263">**NX_SUCCESS**: (0x00) Successful DHCP delete.</span></span>
- <span data-ttu-id="50d63-264">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-264">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="50d63-265">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-265">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-266">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-266">Allowed From</span></span>

<span data-ttu-id="50d63-267">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-267">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-268">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-268">Example</span></span>

```c
/* Delete a DHCP instance.  */
status =  nx_dhcp_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCP instance was successfully deleted.  */
```

## <a name="nx_dhcp_-force_renew"></a><span data-ttu-id="50d63-269">nx_dhcp_ force_renew</span><span class="sxs-lookup"><span data-stu-id="50d63-269">nx_dhcp_ force_renew</span></span>

<span data-ttu-id="50d63-270">Zorla yenileme iletisi gönder</span><span class="sxs-lookup"><span data-stu-id="50d63-270">Send a force renew message</span></span> 

### <a name="prototype"></a><span data-ttu-id="50d63-271">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-271">Prototype</span></span>

```c
UINT nx_dhcp force_renew(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-272">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-272">Description</span></span>

<span data-ttu-id="50d63-273">Bu hizmet, ana bilgisayar uygulamasının DHCP için etkinleştirilen tüm arabirimlerde zorla yenileme iletisi göndermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="50d63-273">This service enables the host application to send a force renew message on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="50d63-274">DHCP Istemcisi, bir bağlantılı durumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="50d63-274">The DHCP Client must be in a BOUND state.</span></span> <span data-ttu-id="50d63-275">Bu işlev, DHCP Istemcisinin T1 zaman aşımı dolmadan önce yenilemeyi deneyecek şekilde, durumu yenıleme olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="50d63-275">This function sets the state to RENEW such that the DHCP Client will try to renew before the T1 timeout expires.</span></span>

<span data-ttu-id="50d63-276">Birden çok arabirim DHCP etkinken belirli bir arabirim üzerinde zorla yenileme göndermek için *nx_dhcp_interface_force_renew* kullanın.</span><span class="sxs-lookup"><span data-stu-id="50d63-276">To send a force renew on a specific interface when multiple interfaces are DHCP-enabled, use *nx_dhcp_interface_force_renew*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-277">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-277">Input Parameters</span></span>

- <span data-ttu-id="50d63-278">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-278">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-279">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-279">Return Values</span></span>

- <span data-ttu-id="50d63-280">**NX_SUCCESS**: (0x00) zorla yenilemeyi başarıyla gönderdi.</span><span class="sxs-lookup"><span data-stu-id="50d63-280">**NX_SUCCESS**: (0x00) Successfully sent force renew.</span></span>
- <span data-ttu-id="50d63-281">**NX_DHCP_NOT_BOUND**: (0x94) istemci IP adresi bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="50d63-281">**NX_DHCP_NOT_BOUND**: (0x94) Client IP address not bound.</span></span>  
- <span data-ttu-id="50d63-282">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-282">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="50d63-283">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-283">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-284">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-284">Allowed From</span></span>

<span data-ttu-id="50d63-285">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-285">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-286">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-286">Example</span></span>

```c
/* Send a force renew message from the Client.  */
status =  nx_dhcp_force_renew(&my_dhcp);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired.  */
```

## <a name="nx_dhcp_interface_force_renew"></a><span data-ttu-id="50d63-287">nx_dhcp_interface_force_renew</span><span class="sxs-lookup"><span data-stu-id="50d63-287">nx_dhcp_interface_force_renew</span></span>

<span data-ttu-id="50d63-288">Belirtilen arabirimde zorla yenileme iletisi gönder</span><span class="sxs-lookup"><span data-stu-id="50d63-288">Send a force renew message on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-289">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-289">Prototype</span></span>

```c
UINT nx_dhcp_interface_force_renew(NX_DHCP *dhcp_ptr, 
                                   UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="50d63-290">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-290">Description</span></span>

<span data-ttu-id="50d63-291">Bu hizmet, arabirim DHCP için etkinleştirilmiş olduğu sürece, ana bilgisayar uygulamasının giriş arabiriminde zorla yenileme iletisi göndermesini sağlar (bkz. *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="50d63-291">This service enables the host application to send a force renew message on the input interface as long as that interface has been enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="50d63-292">Belirtilen arabirimdeki DHCP Istemcisinin bağlı durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50d63-292">The DHCP Client on the specified interface must be in a BOUND state.</span></span> <span data-ttu-id="50d63-293">Bu işlev, DHCP Istemcisinin T1 zaman aşımı dolmadan önce yenilemeyi deneyecek şekilde, durumu yenıleme olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="50d63-293">This function sets the state to RENEW such that the DHCP Client will try to renew before the T1 timeout expires.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-294">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-294">Input Parameters</span></span>

- <span data-ttu-id="50d63-295">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-295">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-296">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-296">Return Values</span></span>

- <span data-ttu-id="50d63-297">**NX_SUCCESS**: (0x00) zorla yenilemeyi başarıyla gönderdi.</span><span class="sxs-lookup"><span data-stu-id="50d63-297">**NX_SUCCESS**: (0x00) Successfully sent force renew.</span></span>  
- <span data-ttu-id="50d63-298">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="50d63-298">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="50d63-299">NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-299">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="50d63-300">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-300">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-301">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-301">Allowed From</span></span>

<span data-ttu-id="50d63-302">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-302">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-303">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-303">Example</span></span>

```c
/* Send a force renew message to the server on interface 1.  */
status =  nx_dhcp_interface_force_renew(&my_dhcp, 1);


/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired.  */
```

## <a name="nx_dhcp_packet_pool_set"></a><span data-ttu-id="50d63-304">nx_dhcp_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="50d63-304">nx_dhcp_packet_pool_set</span></span>

<span data-ttu-id="50d63-305">DHCP Istemci paket havuzunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="50d63-305">Set the DHCP Client packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-306">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-306">Prototype</span></span>

```c
UINT nx_dhcp_packet_pool_set(NX_DHCP *dhcp_ptr, NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-307">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-307">Description</span></span>

<span data-ttu-id="50d63-308">Bu hizmet, uygulamanın bu hizmet çağrısında daha önce oluşturulmuş bir paket havuzuna bir işaretçi geçirerek DHCP Istemci paket havuzunu oluşturmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="50d63-308">This service allows the application to create the DHCP Client packet pool by passing in a pointer to a previously created packet pool in this service call.</span></span> <span data-ttu-id="50d63-309">Bu özelliği kullanmak için, ana bilgisayar uygulamasının NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="50d63-309">To use this feature, the host application must define NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL.</span></span> <span data-ttu-id="50d63-310">Tanımlandığında, *nx_dhcp_create* hizmet istemcinin paket havuzunu oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="50d63-310">When defined, the *nx_dhcp_create* service will not create the Client’s packet pool.</span></span> 

>[!NOTE] 
> <span data-ttu-id="50d63-311">Uygulamanın, paket havuzu oluştururken *nxd_dhcp_client. h* içinde NX_DHCP_PACKET_PAYLOAD olarak tanımlanan DHCP istemci paket havuzu yükünün varsayılan değerlerini kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="50d63-311">The application is recommended to use the default values for the DHCP client packet pool payload, defined as NX_DHCP_PACKET_PAYLOAD in *nxd_dhcp_client.h* when creating the packet pool.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-312">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-312">Input Parameters</span></span>

- <span data-ttu-id="50d63-313">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-313">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="50d63-314">**packet_pool_ptr**: daha önce oluşturulmuş olan paket havuzuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="50d63-314">**packet_pool_ptr**: Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-315">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-315">Return Values</span></span>

- <span data-ttu-id="50d63-316">**NX_SUCCESS**: (0x00) DHCP istemci paket havuzu ayarlandı</span><span class="sxs-lookup"><span data-stu-id="50d63-316">**NX_SUCCESS**: (0x00) DHCP Client packet pool is set</span></span>
- <span data-ttu-id="50d63-317">**NX_NOT_ENABLED**: (0x14) hizmeti etkin değil</span><span class="sxs-lookup"><span data-stu-id="50d63-317">**NX_NOT_ENABLED**: (0x14) Service is not enabled</span></span>
- <span data-ttu-id="50d63-318">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-318">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="50d63-319">NX_DHCP_INVALID_PAYLOAD: (0x9C) yük çok küçük</span><span class="sxs-lookup"><span data-stu-id="50d63-319">NX_DHCP_INVALID_PAYLOAD: (0x9C) Payload is too small</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-320">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-320">Allowed From</span></span>

<span data-ttu-id="50d63-321">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="50d63-321">Application code</span></span>

### <a name="example"></a><span data-ttu-id="50d63-322">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-322">Example</span></span>

```c
/* Create the packet pool. */
status =  nx_packet_pool_create(&dhcp_pool, "DHCP Client Packet Pool", 
                                 NX_DHCP_PACKET_PAYLOAD, pointer, 
                                 (15 * NX_DHCP_PACKET_PAYLOAD));

/* Create the DHCP Client. */
status =  nx_dhcp_create(&dhcp_0, &ip_0, "janetsdhcp1");

/* Set the DHCP Client packet pool.  */
status =  nx_dhcp_packet_pool_set(&my_dhcp, packet_pool_ptr);
/* If status is NX_SUCCESS packet pool was successfully set.  */

```

## <a name="nx_dhcp_request_client_ip"></a><span data-ttu-id="50d63-323">nx_dhcp_request_client_ip</span><span class="sxs-lookup"><span data-stu-id="50d63-323">nx_dhcp_request_client_ip</span></span>

<span data-ttu-id="50d63-324">DHCP örneği için istenen IP adresini ayarlama</span><span class="sxs-lookup"><span data-stu-id="50d63-324">Set requested IP address for DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-325">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-325">Prototype</span></span>

```c
UINT nx_dhcp_request_client_ip(NX_DHCP *dhcp_ptr, 
                               ULONG client_ip_address, 
                               UINT skip_discover_message);
```

### <a name="description"></a><span data-ttu-id="50d63-326">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-326">Description</span></span>

<span data-ttu-id="50d63-327">Bu hizmet, DHCP Istemcisinin DHCP istemci kaydında DHCP için etkinleştirilen ilk arabirimdeki DHCP sunucusundan istemesi için IP adresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="50d63-327">This service sets the IP address for the DHCP Client to request from the DHCP Server on the first interface enabled for DHCP in the DHCP Client record.</span></span> <span data-ttu-id="50d63-328">*Skip_discover_message* bayrağı AYARLANDıYSA, DHCP istemcisi bulma iletisini atlar ve bir istek iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="50d63-328">If the *skip_discover_message* flag is set, the DHCP Client skips the Discover message and sends a Request message.</span></span>

<span data-ttu-id="50d63-329">Belirli bir arabirimdeki DHCP iletileri için belirli bir IP isteği ayarlamak üzere *nx_dhcp_interface_request_client_ip* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="50d63-329">To set the request for a specific IP for DHCP messages on a specific interface, use the *nx_dhcp_interface_request_client_ip* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-330">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-330">Input Parameters</span></span>

- <span data-ttu-id="50d63-331">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-331">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="50d63-332">**client_ip_address**: DHCP sunucusundan isteğin IP adresi</span><span class="sxs-lookup"><span data-stu-id="50d63-332">**client_ip_address**: IP address to request from DHCP server</span></span>
- <span data-ttu-id="50d63-333">**skip_discover_message**:</span><span class="sxs-lookup"><span data-stu-id="50d63-333">**skip_discover_message**:</span></span> 
    - <span data-ttu-id="50d63-334">Doğru ise, DHCP Istemcisi Istek iletisi gönderir</span><span class="sxs-lookup"><span data-stu-id="50d63-334">If true, DHCP Client sends Request message</span></span>
    - <span data-ttu-id="50d63-335">Yanlışsa, bulma iletisini gönderir.</span><span class="sxs-lookup"><span data-stu-id="50d63-335">If false, it sends the Discover message.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-336">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-336">Return Values</span></span>

- <span data-ttu-id="50d63-337">**NX_SUCCESS**: (0x00) istenen IP adresi ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="50d63-337">**NX_SUCCESS**: (0x00) Requested IP address is set.</span></span>
- <span data-ttu-id="50d63-338">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-338">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="50d63-339">NX_DHCP_INVALID_IP_REQUEST: (0x9D) NULL IP adresi istendi</span><span class="sxs-lookup"><span data-stu-id="50d63-339">NX_DHCP_INVALID_IP_REQUEST: (0x9D) NULL IP address requested</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-340">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-340">Allowed From</span></span>

<span data-ttu-id="50d63-341">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-341">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-342">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-342">Example</span></span>

```c
/* Set the DHCP Client requested IP address and skip the discover message.  */

status =  nx_dhcp_request_client_ip(&my_dhcp, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set.  */

```

## <a name="nx_dhcp_interface_request_client_ip"></a><span data-ttu-id="50d63-343">nx_dhcp_interface_request_client_ip</span><span class="sxs-lookup"><span data-stu-id="50d63-343">nx_dhcp_interface_request_client_ip</span></span>

<span data-ttu-id="50d63-344">Belirtilen arabirimdeki DHCP örneği için istenen IP adresini ayarla</span><span class="sxs-lookup"><span data-stu-id="50d63-344">Set requested IP address for DHCP instance on specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-345">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-345">Prototype</span></span>

```c
UINT nx_dhcp_interface_request_client_ip(NX_DHCP *dhcp_ptr, UINT  interface_index, 
                                         ULONG client_ip_address, UINT skip_discover_message);
```

### <a name="description"></a><span data-ttu-id="50d63-346">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-346">Description</span></span>

<span data-ttu-id="50d63-347">Bu hizmet, DHCP Istemcisinin, belirtilen arabirimdeki DHCP sunucusundan istemesi için IP adresini ayarlar, bu arabirim DHCP için etkinleştirilmişse (bkz. *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="50d63-347">This service sets the IP address for the DHCP Client to request from the DHCP Server on the specified interface, if that interface is enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="50d63-348">*Skip_discover_message* bayrağı AYARLANDıYSA, DHCP istemcisi bulma iletisini atlar ve bir istek iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="50d63-348">If the *skip_discover_message* flag is set, the DHCP Client skips the Discover message and sends a Request message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-349">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-349">Input Parameters</span></span>

- <span data-ttu-id="50d63-350">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-350">**dhcp_ptr**: Pointer to DHCP control block.</span></span>
- <span data-ttu-id="50d63-351">**Interface_index**: IP adresi istemek için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-351">**Interface_index**: Index of interface to request IP address on</span></span>
- <span data-ttu-id="50d63-352">**client_ip_address**: DHCP sunucusundan isteğin IP adresi</span><span class="sxs-lookup"><span data-stu-id="50d63-352">**client_ip_address**: IP address to request from DHCP server</span></span>
- <span data-ttu-id="50d63-353">**skip_discover_message**: true Ise, DHCP istemcisi istek iletisi gönderir; diğer bir deyişle, bulma iletisini gönderir.</span><span class="sxs-lookup"><span data-stu-id="50d63-353">**skip_discover_message**: If true, DHCP Client sends Request message; else it sends the Discover message.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-354">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-354">Return Values</span></span>

- <span data-ttu-id="50d63-355">**NX_SUCCESS**: (0x00) istenen IP adresi ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="50d63-355">**NX_SUCCESS**: (0x00) Requested IP address is set.</span></span>
- <span data-ttu-id="50d63-356">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="50d63-356">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="50d63-357">NX_PTR_ERROR: (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-357">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="50d63-358">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-358">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-359">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-359">Allowed From</span></span>

<span data-ttu-id="50d63-360">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-360">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-361">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-361">Example</span></span>

```c
/* Set the DHCP Client requested IP address and skip the discover message on  
   interface 0.  */
status =  nx_dhcp_interface_request_client_ip(&my_dhcp, 0, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set.  */
```

## <a name="nx_dhcp_reinitialize"></a><span data-ttu-id="50d63-362">nx_dhcp_reinitialize</span><span class="sxs-lookup"><span data-stu-id="50d63-362">nx_dhcp_reinitialize</span></span>

<span data-ttu-id="50d63-363">DHCP istemci ağı parametrelerini Temizleme</span><span class="sxs-lookup"><span data-stu-id="50d63-363">Clear the DHCP client network parameters</span></span> 

### <a name="prototype"></a><span data-ttu-id="50d63-364">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-364">Prototype</span></span>

```c
UINT nx_dhcp_reinitialize(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-365">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-365">Description</span></span>

<span data-ttu-id="50d63-366">Bu hizmet, ana bilgisayar uygulama ağ parametrelerini (IP adresi, ağ adresi ve ağ maskesi) temizler ve DHCP için etkinleştirilen tüm arabirimlerde DHCP Istemci durumunu temizler.</span><span class="sxs-lookup"><span data-stu-id="50d63-366">This service clears the host application network parameters (IP address, network address and network mask), and clears the DHCP Client state on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="50d63-367">*Nx_dhcp_stop* ile birlikte KULLANıLıR ve DHCP durum makinesine ' yeniden Başlat ' için *nx_dhcp_start* :</span><span class="sxs-lookup"><span data-stu-id="50d63-367">It is used in combination with *nx_dhcp_stop* and *nx_dhcp_start* to ‘restart’ the DHCP state machine:</span></span>

```c
nx_dhcp_stop(&my_dhcp);
nx_dhcp_reinitialize(&my_dhcp);
nx_dhcp_start(&my_dhcp);
```

<span data-ttu-id="50d63-368">DHCP için birden fazla arabirim etkinleştirildiğinde belirli bir arabirimdeki DHCP Istemcisini yeniden başlatmak için *nx_dhcp_interface_reinitialize* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="50d63-368">To reinitialize the DHCP Client on a specific interface when multiple interfaces are enabled for DHCP, use the *nx_dhcp_interface_reinitialize* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-369">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-369">Input Parameters</span></span>

- <span data-ttu-id="50d63-370">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-370">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-371">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-371">Return Values</span></span>

- <span data-ttu-id="50d63-372">**NX_SUCCESS**: (0x00) DHCP başarıyla yeniden başlatıldı</span><span class="sxs-lookup"><span data-stu-id="50d63-372">**NX_SUCCESS**: (0x00) DHCP successfully reinitialized</span></span> 
- <span data-ttu-id="50d63-373">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-373">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-374">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-374">Allowed From</span></span>

<span data-ttu-id="50d63-375">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-375">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-376">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-376">Example</span></span>

```c
/* Reinitialize the previously started DHCP client.  */
status =  nx_dhcp_reinitialize(&my_dhcp);

/* If status is NX_SUCCESS the host application successfully reinitialized its network parameters and DHCP client state. */
```

## <a name="nx_dhcp_interface_reinitialize"></a><span data-ttu-id="50d63-377">nx_dhcp_interface_reinitialize</span><span class="sxs-lookup"><span data-stu-id="50d63-377">nx_dhcp_interface_reinitialize</span></span>

<span data-ttu-id="50d63-378">Belirtilen arabirimdeki DHCP istemci ağ parametrelerini temizle</span><span class="sxs-lookup"><span data-stu-id="50d63-378">Clear the DHCP client network parameters on the specified interface</span></span> 

### <a name="prototype"></a><span data-ttu-id="50d63-379">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-379">Prototype</span></span>

```c
UINT nx_dhcp_interface_reinitialize(NX_DHCP *dhcp_ptr, 
                                     UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="50d63-380">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-380">Description</span></span>

<span data-ttu-id="50d63-381">Bu hizmet, bu arabirim DHCP için etkinleştirilmişse belirtilen arabirimdeki ağ parametrelerini (IP adresi, ağ adresi ve ağ maskesi) temizler (bkz. *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="50d63-381">This service clears the network parameters (IP address, network address and network mask) on the specified interface if that interface is enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="50d63-382">Daha fazla bilgi için bkz. *nx_dhcp_reinitialize* .</span><span class="sxs-lookup"><span data-stu-id="50d63-382">See *nx_dhcp_reinitialize* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-383">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-383">Input Parameters</span></span>

- <span data-ttu-id="50d63-384">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="50d63-384">**dhcp_ptr**: Pointer to previously created DHCP instance</span></span>
- <span data-ttu-id="50d63-385">**interface_index**: yeniden başlatmak için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-385">**interface_index**: Index of interface to reinitialize</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-386">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-386">Return Values</span></span>

- <span data-ttu-id="50d63-387">**NX_SUCCESS**: (0x00) arabirimi başarıyla yeniden başlatıldı</span><span class="sxs-lookup"><span data-stu-id="50d63-387">**NX_SUCCESS**: (0x00) Interface successfully reinitialized</span></span>
- <span data-ttu-id="50d63-388">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="50d63-388">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="50d63-389">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-389">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="50d63-390">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-390">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="50d63-391">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-391">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-392">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-392">Allowed From</span></span>

<span data-ttu-id="50d63-393">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-393">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-394">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-394">Example</span></span>

```c
/* Reinitialize the previously started DHCP client on interface 1.  */
status =  nx_dhcp_interface_reinitialize(&my_dhcp, 1);

/* If status is NX_SUCCESS the host application successfully reinitialized its network parameters and DHCP client state. */
```

## <a name="nx_dhcp_release"></a><span data-ttu-id="50d63-395">nx_dhcp_release</span><span class="sxs-lookup"><span data-stu-id="50d63-395">nx_dhcp_release</span></span>

<span data-ttu-id="50d63-396">Yayın kiralanan IP adresi</span><span class="sxs-lookup"><span data-stu-id="50d63-396">Release Leased IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-397">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-397">Prototype</span></span>

```c
UINT nx_dhcp_release(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-398">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-398">Description</span></span>

<span data-ttu-id="50d63-399">Bu hizmet, bir DHCP sunucusundan alınan IP adresini, yayın iletisini bu sunucuya göndererek yayınlar.</span><span class="sxs-lookup"><span data-stu-id="50d63-399">This service releases the IP address obtained from a DHCP server by sending the RELEASE message to that server.</span></span> <span data-ttu-id="50d63-400">Daha sonra DHCP Istemcisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="50d63-400">It then reinitializes the DHCP Client.</span></span> <span data-ttu-id="50d63-401">Bu hizmet, DHCP için etkinleştirilen tüm arabirimlere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="50d63-401">This service is applied to all interfaces enabled for DHCP.</span></span>

<span data-ttu-id="50d63-402">Uygulama, *nx_dhcp_start* çağırarak DHCP istemcisini yeniden başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="50d63-402">The application can restart the DHCP Client by calling *nx_dhcp_start*.</span></span>

<span data-ttu-id="50d63-403">Bir adresi belirli bir arabirimdeki DHCP sunucusuna geri yüklemek için *nx_dhcp_interface_release* hizmetini kullanın</span><span class="sxs-lookup"><span data-stu-id="50d63-403">To release an address back to the DHCP server on a specific interface, use the *nx_dhcp_interface_release* service</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-404">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-404">Input Parameters</span></span>

- <span data-ttu-id="50d63-405">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-405">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-406">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-406">Return Values</span></span>

- <span data-ttu-id="50d63-407">**NX_SUCCESS**: (0x00) başarılı DHCP sürümü.</span><span class="sxs-lookup"><span data-stu-id="50d63-407">**NX_SUCCESS**: (0x00) Successful DHCP release.</span></span>  
- <span data-ttu-id="50d63-408">**NX_DHCP_NOT_BOUND**: (0x94) IP adresi kiralamadı, bu nedenle serbest bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="50d63-408">**NX_DHCP_NOT_BOUND**: (0x94) The IP address has not been leased so it can’t be released.</span></span>
- <span data-ttu-id="50d63-409">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-409">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="50d63-410">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-410">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-411">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-411">Allowed From</span></span>

<span data-ttu-id="50d63-412">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-412">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-413">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-413">Example</span></span>

```c
/* Release the previously leased IP address.  */
status =  nx_dhcp_release(&my_dhcp);

/* If status is NX_SUCCESS the previous IP lease was successfully released.  */
```

## <a name="nx_dhcp_interface_release"></a><span data-ttu-id="50d63-414">nx_dhcp_interface_release</span><span class="sxs-lookup"><span data-stu-id="50d63-414">nx_dhcp_interface_release</span></span>

<span data-ttu-id="50d63-415">Belirtilen arabirimdeki IP adresini serbest bırak</span><span class="sxs-lookup"><span data-stu-id="50d63-415">Release IP address on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-416">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-416">Prototype</span></span>

```c
UINT nx_dhcp_interface_release(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="50d63-417">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-417">Description</span></span>

<span data-ttu-id="50d63-418">Bu hizmet, belirtilen arabirimdeki bir DHCP sunucusundan alınan IP adresini serbest bırakır ve DHCP Istemcisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="50d63-418">This service releases the IP address obtained from a DHCP server on the specified interface and reinitializes the DHCP Client.</span></span> <span data-ttu-id="50d63-419">DHCP Istemcisi, *nx_dhcp_start* çağırarak yeniden başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="50d63-419">The DHCP Client can be restarted by calling *nx_dhcp_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-420">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-420">Input Parameters</span></span>

- <span data-ttu-id="50d63-421">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-421">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-422">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-422">Return Values</span></span>

- <span data-ttu-id="50d63-423">**NX_SUCCESS**: (0x00) başarılı DHCP sürümü.</span><span class="sxs-lookup"><span data-stu-id="50d63-423">**NX_SUCCESS**: (0x00) Successful DHCP release.</span></span>
- <span data-ttu-id="50d63-424">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="50d63-424">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="50d63-425">**NX_DHCP_NOT_BOUND**: (0x94) IP adresi kiralamadı, bu nedenle serbest bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="50d63-425">**NX_DHCP_NOT_BOUND**: (0x94) The IP address has not been leased so it can’t be released.</span></span>
- <span data-ttu-id="50d63-426">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-426">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="50d63-427">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-427">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="50d63-428">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-428">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-429">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-429">Allowed From</span></span>

<span data-ttu-id="50d63-430">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-430">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-431">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-431">Example</span></span>

```c
/* Release the previously leased IP address on interface 1.  */
status =  nx_dhcp_interface_release(&my_dhcp, 1);

/* If status is NX_SUCCESS the previous IP lease was successfully released.  */
```

## <a name="nx_dhcp_decline"></a><span data-ttu-id="50d63-432">nx_dhcp_decline</span><span class="sxs-lookup"><span data-stu-id="50d63-432">nx_dhcp_decline</span></span>

<span data-ttu-id="50d63-433">DHCP sunucusundan IP adresini Reddet</span><span class="sxs-lookup"><span data-stu-id="50d63-433">Decline IP address from DHCP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-434">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-434">Prototype</span></span>

```c
UINT nx_dhcp_decline(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-435">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-435">Description</span></span>

<span data-ttu-id="50d63-436">Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerde DHCP sunucusundan kiralanmış bir IP adresini reddeder.</span><span class="sxs-lookup"><span data-stu-id="50d63-436">This service declines an IP address leased from the DHCP server on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="50d63-437">NX_DHCP_CLIENT_ SEND_ ARP_PROBE tanımlanmışsa, DHCP Istemcisi IP adresinin zaten kullanımda olduğunu algılarsa bir reddetme iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="50d63-437">If NX_DHCP_CLIENT_ SEND_ ARP_PROBE is defined, the DHCP Client will send a DECLINE message if it detects that the IP address is already in use.</span></span> <span data-ttu-id="50d63-438">NetX Duo DHCP Istemcisinde ARP araştırma yapılandırması hakkında daha fazla bilgi için bkz. bölüm içinde **ARP araştırmaları** .</span><span class="sxs-lookup"><span data-stu-id="50d63-438">See **ARP Probes** in Chapter One for more information on ARP probe configuration in the NetX Duo DHCP Client.</span></span>

<span data-ttu-id="50d63-439">Uygulama, adresin başka yollarla kullanımda olduğunu tespit etmezse IP adresini reddetmek için bu hizmeti kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="50d63-439">The application can use this service to decline its IP address if it discovers the address is in use by other means.</span></span>

<span data-ttu-id="50d63-440">Bu hizmet, DHCP Istemcisini *nx_dhcp_start* çağırarak yeniden başlatılacak şekilde yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="50d63-440">This service reinitializes the DHCP Client to that it can be restarted by calling *nx_dhcp_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-441">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-441">Input Parameters</span></span>

- <span data-ttu-id="50d63-442">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-442">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-443">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-443">Return Values</span></span>

- <span data-ttu-id="50d63-444">**NX_SUCCESS**: (0x00) reddetme başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="50d63-444">**NX_SUCCESS**: (0x00) Decline successfully sent</span></span>  
- <span data-ttu-id="50d63-445">**NX_DHCP_NOT_BOUND**: (0x94) DHCP istemcisi bağlanmadı</span><span class="sxs-lookup"><span data-stu-id="50d63-445">**NX_DHCP_NOT_BOUND**: (0x94) DHCP Client not bound</span></span>
- <span data-ttu-id="50d63-446">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-446">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="50d63-447">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="50d63-447">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-448">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-448">Allowed From</span></span>

<span data-ttu-id="50d63-449">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-449">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-450">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-450">Example</span></span>

```c

/* Decline the IP address offered by the DHCP server.  */
status =  nx_dhcp_decline(&my_dhcp);

/* If status is NX_SUCCESS the previous IP address decline message was successfully trasnmitted.  */
```

## <a name="nx_dhcp_interface_decline"></a><span data-ttu-id="50d63-451">nx_dhcp_interface_decline</span><span class="sxs-lookup"><span data-stu-id="50d63-451">nx_dhcp_interface_decline</span></span>

<span data-ttu-id="50d63-452">Belirtilen arabirimdeki DHCP sunucusundan IP adresini Reddet</span><span class="sxs-lookup"><span data-stu-id="50d63-452">Decline IP address from DHCP Server on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-453">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-453">Prototype</span></span>

```c
UINT nx_dhcp_interface_decline(NX_DHCP *dhcp_ptr, 
                               UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="50d63-454">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-454">Description</span></span>

<span data-ttu-id="50d63-455">Bu hizmet, DHCP sunucusu tarafından atanan bir IP adresini reddetmek için reddetme iletisini sunucuya gönderir.</span><span class="sxs-lookup"><span data-stu-id="50d63-455">This service sends the DECLINE message to the server to decline an IP address assigned by the DHCP server.</span></span> <span data-ttu-id="50d63-456">Ayrıca, DHCP Istemcisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="50d63-456">It also reinitializes the DHCP Client.</span></span> <span data-ttu-id="50d63-457">Daha fazla bilgi için bkz. *nx_dhcp_decline* .</span><span class="sxs-lookup"><span data-stu-id="50d63-457">See *nx_dhcp_decline* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-458">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-458">Input Parameters</span></span>

- <span data-ttu-id="50d63-459">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-459">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="50d63-460">**Interface_index**: IP adresini reddetme arabiriminin dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-460">**Interface_index**: Index of interface to decline IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-461">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-461">Return Values</span></span>

- <span data-ttu-id="50d63-462">**NX_SUCCESS**: (0x00) DHCP reddetme iletisi gönderildi</span><span class="sxs-lookup"><span data-stu-id="50d63-462">**NX_SUCCESS**: (0x00) DHCP decline message sent</span></span>  
- <span data-ttu-id="50d63-463">**NX_DHCP_NOT_BOUND**: (0x94) DHCP istemcisi bağlanmadı</span><span class="sxs-lookup"><span data-stu-id="50d63-463">**NX_DHCP_NOT_BOUND**: (0x94) DHCP Client not bound</span></span>
- <span data-ttu-id="50d63-464">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="50d63-464">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="50d63-465">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-465">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="50d63-466">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-466">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="50d63-467">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-467">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-468">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-468">Allowed From</span></span>

<span data-ttu-id="50d63-469">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-469">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-470">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-470">Example</span></span>

```c
/* Decline the IP address offered by the DHCP server on interface 2.  */
status =  nx_dhcp_interface_decline(&my_dhcp, 2);

/* If status is NX_SUCCESS the previous IP address decline message was successfully trasnmitted.  */
```
## <a name="nx_dhcp_send_request"></a><span data-ttu-id="50d63-471">nx_dhcp_send_request</span><span class="sxs-lookup"><span data-stu-id="50d63-471">nx_dhcp_send_request</span></span>

<span data-ttu-id="50d63-472">DHCP iletisini sunucuya gönder</span><span class="sxs-lookup"><span data-stu-id="50d63-472">Send DHCP message to Server</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-473">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-473">Prototype</span></span>

```c
UINT nx_dhcp_send_request(NX_DHCP *dhcp_ptr, UINT dhcp_message_type);

```

### <a name="description"></a><span data-ttu-id="50d63-474">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-474">Description</span></span>

<span data-ttu-id="50d63-475">Bu hizmet, belirtilen DHCP iletisini DHCP Istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="50d63-475">This service sends the specified DHCP message to the DHCP server on the first interface enabled for DHCP found in the DHCP Client record.</span></span> <span data-ttu-id="50d63-476">Bir yayın veya reddetme iletisi göndermek için, uygulamanın sırasıyla *nx_dhcp [_interface] _Release*() veya *nx_dhcp_interface_decline ()* hizmetlerini kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50d63-476">To send a RELEASE or DECLINE message, the application must use the *nx_dhcp[_interface]_release*() or *nx_dhcp_interface_decline()* services respectively.</span></span>

<span data-ttu-id="50d63-477">Bu hizmeti kullanmak için, DHCP Istemcisinin INFORM_REQUEST ileti türünü gönderme haricinde başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50d63-477">The DHCP Client must be started to use this service except for sending the INFORM_REQUEST message type.</span></span>

>[!NOTE]
> <span data-ttu-id="50d63-478">Bu hizmet, ana bilgisayar uygulamasının DHCP Istemci durumu makinesine ' Drive ' için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="50d63-478">This service is not intended for the host application to ‘drive’ the DHCP Client state machine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-479">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-479">Input Parameters</span></span>

- <span data-ttu-id="50d63-480">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-480">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="50d63-481">**dhcp_message_type**: ileti isteği ( *nxd_dhcp_client. h* içinde tanımlı)</span><span class="sxs-lookup"><span data-stu-id="50d63-481">**dhcp_message_type**: Message request (defined in *nxd_dhcp_client.h*)</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-482">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-482">Return Values</span></span>

- <span data-ttu-id="50d63-483">**NX_SUCCESS**: (0x00) DHCP iletisi gönderildi</span><span class="sxs-lookup"><span data-stu-id="50d63-483">**NX_SUCCESS**: (0x00) DHCP message sent</span></span>  
- <span data-ttu-id="50d63-484">**NX_DHCP_NOT_STARTED**: (0x96) geçersiz arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-484">**NX_DHCP_NOT_STARTED**: (0x96) Invalid interface index</span></span>
- <span data-ttu-id="50d63-485">**NX_DHCP_INVALID_MESSAGE**: (0x9b) göndermek için geçersiz ileti türü</span><span class="sxs-lookup"><span data-stu-id="50d63-485">**NX_DHCP_INVALID_MESSAGE**: (0x9B) Invalid message type to send</span></span>
- <span data-ttu-id="50d63-486">NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="50d63-486">NX_PTR_ERROR: (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-487">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-487">Allowed From</span></span>

<span data-ttu-id="50d63-488">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-488">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-489">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-489">Example</span></span>

```c
/* Send the DHCP INFORM REQUEST message to the server.  */

status =  nx_dhcp_send_request(&my_dhcp, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent.  */
```

## <a name="nx_dhcp_interface_send_request"></a><span data-ttu-id="50d63-490">nx_dhcp_interface_send_request</span><span class="sxs-lookup"><span data-stu-id="50d63-490">nx_dhcp_interface_send_request</span></span>

<span data-ttu-id="50d63-491">Belirli bir arabirimdeki DHCP iletisini sunucuya gönder</span><span class="sxs-lookup"><span data-stu-id="50d63-491">Send DHCP message to Server on a specific interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-492">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-492">Prototype</span></span>

```c
UINT nx_dhcp_interface_send_request(NX_DHCP *dhcp_ptr, 
                                    UINT interface_index, 
                                    UINT dhcp_message_type);
```

### <a name="description"></a><span data-ttu-id="50d63-493">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-493">Description</span></span>

<span data-ttu-id="50d63-494">Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirimdeki DHCP sunucusuna bir ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="50d63-494">This service sends a message to the DHCP server on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="50d63-495">Bir yayın veya reddetme iletisi göndermek için, uygulamanın sırasıyla *nx_dhcp [_interface] _Release*() veya *nx_dhcp_interface_decline ()* hizmetlerini kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50d63-495">To send a RELEASE or DECLINE message, the application must use the *nx_dhcp[_interface]_release*() or *nx_dhcp_interface_decline()* services respectively.</span></span>

<span data-ttu-id="50d63-496">DHCP Istemcisi, DHCP BILDIR Istek iletisi türünü göndermek dışında bu hizmeti kullanacak şekilde başlatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="50d63-496">The DHCP Client must be started to use this service except for sending the DHCP INFORM REQUEST message type.</span></span>

<span data-ttu-id="50d63-497">Bu hizmet, ana bilgisayar uygulamasının DHCP Istemci durumu makinesine ' Drive ' için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="50d63-497">This service is not intended for the host application to ‘drive’ the DHCP Client state machine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-498">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-498">Input Parameters</span></span>

- <span data-ttu-id="50d63-499">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-499">**dhcp_ptr**: Pointer to DHCP control block.</span></span>
- <span data-ttu-id="50d63-500">**Interface_index**: iletinin gönderileceği arabirimin dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-500">**Interface_index**: Index of interface to send message on</span></span>
- <span data-ttu-id="50d63-501">**dhcp_message_type**: ileti isteği (nxd_dhcp_client. h içinde tanımlı)</span><span class="sxs-lookup"><span data-stu-id="50d63-501">**dhcp_message_type**: Message request (defined in nxd_dhcp_client.h)</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-502">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-502">Return Values</span></span>

- <span data-ttu-id="50d63-503">**NX_SUCCESS**: (0x00) DHCP iletisi gönderildi</span><span class="sxs-lookup"><span data-stu-id="50d63-503">**NX_SUCCESS**: (0x00) DHCP message sent</span></span>  
- <span data-ttu-id="50d63-504">**NX_DHCP_NOT_STARTED**: (0x96) geçersiz arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-504">**NX_DHCP_NOT_STARTED**: (0x96) Invalid interface index</span></span>
- <span data-ttu-id="50d63-505">**NX_DHCP_INVALID_MESSAGE**: (0x9b) göndermek için geçersiz ileti türü</span><span class="sxs-lookup"><span data-stu-id="50d63-505">**NX_DHCP_INVALID_MESSAGE**: (0x9B) Invalid message type to send</span></span>
- <span data-ttu-id="50d63-506">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="50d63-506">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="50d63-507">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-507">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="50d63-508">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-508">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="50d63-509">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-509">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-510">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-510">Allowed From</span></span>

<span data-ttu-id="50d63-511">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-511">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-512">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-512">Example</span></span>

```c
/* Send the INFORM REQUEST message to the server on the primary interface.  */

status =  nx_dhcp_interface_send_request(&my_dhcp, 0, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent.  */
```

## <a name="nx_dhcp_server_address_get"></a><span data-ttu-id="50d63-513">nx_dhcp_server_address_get</span><span class="sxs-lookup"><span data-stu-id="50d63-513">nx_dhcp_server_address_get</span></span>

<span data-ttu-id="50d63-514">DHCP Istemcisinin DHCP sunucusu IP adresini al</span><span class="sxs-lookup"><span data-stu-id="50d63-514">Get the DHCP Client’s DHCP server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-515">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-515">Prototype</span></span>

```c
UINT nx_dhcp_server_address_get(NX_DHCP *dhcp_ptr, 
                                ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="50d63-516">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-516">Description</span></span>

<span data-ttu-id="50d63-517">Bu hizmet DHCP istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP Istemci DHCP sunucusu IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="50d63-517">This service retrieves the DHCP Client DHCP server IP address on the first interface enabled for DHCP found in the DHCP Client record.</span></span> <span data-ttu-id="50d63-518">Çağıran bu hizmeti yalnızca DHCP Istemcisi DHCP sunucusu tarafından atanan bir IP adresine bağlandıktan sonra kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="50d63-518">The caller can only use this service after the DHCP Client is bound to an IP address assigned by the DHCP Server.</span></span> <span data-ttu-id="50d63-519">Konak uygulama, IP adresinin ayarlandığını doğrulamak için *nx_ip_status_check* hizmetini kullanabilir veya NX *_DHCP_STATE_CHANGE_NOTIFY* kullanabilir ve DHCP istemci durumunun NX_DHCP_STATE_BOUND olduğunu sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="50d63-519">The host application can use the *nx_ip_status_check* service to verify IP address is set, or it can use the nx *_dhcp_state_change_notify* and query the DHCP Client state is NX_DHCP_STATE_BOUND.</span></span> <span data-ttu-id="50d63-520">Durum değişikliği geri arama işlevini ayarlama hakkında daha fazla ayrıntı için bkz. *nx_dhcp_state_change_notify* .</span><span class="sxs-lookup"><span data-stu-id="50d63-520">See *nx_dhcp_state_change_notify* for more details about setting the state change callback function.</span></span>

<span data-ttu-id="50d63-521">DHCP Istemcisi için birden çok arabirim etkinleştirildiğinde, belirli bir arabirimdeki DHCP sunucusunu bulmak için *nx_dhcp_interface_server_address_get* hizmetini kullanın</span><span class="sxs-lookup"><span data-stu-id="50d63-521">To find the DHCP server on a specific interface when multiple interfaces are enabled for DHCP Client, use the *nx_dhcp_interface_server_address_get* service</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-522">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-522">Input Parameters</span></span>

- <span data-ttu-id="50d63-523">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-523">**dhcp_ptr**: Pointer to DHCP control block.</span></span>
- <span data-ttu-id="50d63-524">**server_address**: sunucu IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-524">**server_address**: Pointer to server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-525">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-525">Return Values</span></span>

- <span data-ttu-id="50d63-526">**NX_SUCCESS**: (0x00) DHCP sunucusu adresi döndürüldü</span><span class="sxs-lookup"><span data-stu-id="50d63-526">**NX_SUCCESS**: (0x00) DHCP server address returned</span></span>
- <span data-ttu-id="50d63-527">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xa5) DHCP için etkinleştirilen arabirim yok</span><span class="sxs-lookup"><span data-stu-id="50d63-527">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) No interfaces enabled for DHCP</span></span>
- <span data-ttu-id="50d63-528">NX_PTR_ERROR: (0x16) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-528">NX_PTR_ERROR: (0x16) Invalid input pointer</span></span>
- <span data-ttu-id="50d63-529">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-529">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-530">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-530">Allowed From</span></span>

<span data-ttu-id="50d63-531">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-531">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-532">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-532">Example</span></span>

```c
/* Use the state change notify service to determine the Client transition to the bound state and get its DHCP server IP address.*/

void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{
ULONG server_address;
UINT  status;

/* Increment state changes counter.  */
state_changes++;

if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
        {
            status = nx_dhcp_server_address_get(&dhcp_0, &server_address);
        }

}
```

## <a name="nx_dhcp_interface_server_address_get"></a><span data-ttu-id="50d63-533">nx_dhcp_interface_server_address_get</span><span class="sxs-lookup"><span data-stu-id="50d63-533">nx_dhcp_interface_server_address_get</span></span>

<span data-ttu-id="50d63-534">Belirtilen arabirimdeki DHCP Istemcisinin DHCP sunucusu IP adresini al</span><span class="sxs-lookup"><span data-stu-id="50d63-534">Get the DHCP Client’s DHCP server IP address on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-535">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-535">Prototype</span></span>

```c
UINT nx_dhcp_interface_server_address_get(NX_DHCP *dhcp_ptr, 
                                          UINT interface_index,
                                          ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="50d63-536">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-536">Description</span></span>

<span data-ttu-id="50d63-537">Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirimdeki DHCP Istemci DHCP sunucusu IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="50d63-537">This service retrieves the DHCP Client DHCP server IP address on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="50d63-538">DHCP Istemcisi, bağlantılı durumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="50d63-538">The DHCP Client must be in the Bound state.</span></span> <span data-ttu-id="50d63-539">Bu arabirimdeki DHCP Istemcisini başlattıktan sonra konak uygulama, IP adresinin ayarlandığını doğrulamak için *nx_ip_status_check* hizmetini kullanabilir ya da DHCP istemci durumu değişikliği geri aramasını KULLANABILIR ve DHCP istemci durumunun NX_DHCP_STATE_BOUND.</span><span class="sxs-lookup"><span data-stu-id="50d63-539">After starting the DHCP Client on that interface, the host application can either use the *nx_ip_status_check* service to verify the IP address is set, or it can use the DHCP Client state change callback and query the DHCP Client state is NX_DHCP_STATE_BOUND.</span></span> <span data-ttu-id="50d63-540">Durum değişikliği geri arama işlevini ayarlama hakkında daha fazla ayrıntı için bkz. *nx_dhcp_state_change_notify* .</span><span class="sxs-lookup"><span data-stu-id="50d63-540">See *nx_dhcp_state_change_notify* for more details about setting the state change callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-541">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-541">Input Parameters</span></span>

- <span data-ttu-id="50d63-542">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-542">**dhcp_ptr**: Pointer to DHCP control block.</span></span>
- <span data-ttu-id="50d63-543">**Interface_index**: IP adresi almak için arabirimin dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-543">**Interface_index**: Index of interface to obtain IP address</span></span>
- <span data-ttu-id="50d63-544">**server_address**: sunucu IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-544">**server_address**: Pointer to server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-545">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-545">Return Values</span></span>

- <span data-ttu-id="50d63-546">**NX_SUCCESS**: (0x00) DHCP sunucusu adresi döndürüldü</span><span class="sxs-lookup"><span data-stu-id="50d63-546">**NX_SUCCESS**: (0x00) DHCP server address returned</span></span>
- <span data-ttu-id="50d63-547">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xa5) DHCP için etkinleştirilen arabirim yok</span><span class="sxs-lookup"><span data-stu-id="50d63-547">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) No interfaces enabled for DHCP</span></span>
- <span data-ttu-id="50d63-548">**NX_DHCP_NOT_BOUND**: (0x94) DHCP istemcisi bağlanmadı</span><span class="sxs-lookup"><span data-stu-id="50d63-548">**NX_DHCP_NOT_BOUND**: (0x94) DHCP Client not bound</span></span>
- <span data-ttu-id="50d63-549">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-549">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="50d63-550">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-550">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="50d63-551">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-551">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-552">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-552">Allowed From</span></span>

<span data-ttu-id="50d63-553">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-553">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-554">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-554">Example</span></span>

```c
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. */

void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter.  */
state_changes++;

/* Get the DHCP server IP address on interface 1 */
if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
        {
         status = nx_dhcp_interface_server_address_get(&dhcp_0, 1, 
                                                       &server_address);
        }
}
```

## <a name="nx_dhcp_set_interface_index"></a><span data-ttu-id="50d63-555">nx_dhcp_set_interface_index</span><span class="sxs-lookup"><span data-stu-id="50d63-555">nx_dhcp_set_interface_index</span></span>

<span data-ttu-id="50d63-556">DHCP örneği için ağ arabirimini ayarla</span><span class="sxs-lookup"><span data-stu-id="50d63-556">Set network interface for DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-557">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-557">Prototype</span></span>

```c
UINT nx_dhcp_set_interface_index(NX_DHCP *dhcp_ptr, UINT index);
```

### <a name="description"></a><span data-ttu-id="50d63-558">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-558">Description</span></span>

<span data-ttu-id="50d63-559">Bu hizmet, DHCP örneği için ağ arabirimini, tek bir ağ arabirimi için yapılandırılmış DHCP Istemcisini çalıştırırken üzerinde DHCP sunucusuna bağlanacak şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="50d63-559">This service sets the network interface for the DHCP instance to connect to the DHCP Server on when running DHCP Client configured for a single network interface.</span></span>

<span data-ttu-id="50d63-560">Varsayılan olarak, DHCP Istemcisi birincil arabirimde çalışır.</span><span class="sxs-lookup"><span data-stu-id="50d63-560">By default the DHCP Client runs on the primary interface.</span></span> <span data-ttu-id="50d63-561">İkincil bir hizmette DHCP çalıştırmak için bu hizmeti kullanarak ikincil arabirimi DHCP Istemci arabirimi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="50d63-561">To run DHCP on a secondary service, use this service to set the secondary interface as the DHCP Client interface.</span></span> <span data-ttu-id="50d63-562">Uygulamanın, *nx_ip_interface_attach* hizmetini kullanarak BELIRTILEN arabirimi IP örneğine daha önce kaydetmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="50d63-562">The application must previously register the specified interface to the IP instance using the *nx_ip_interface_attach* service.</span></span>

>[!NOTE]
> <span data-ttu-id="50d63-563">Bu hizmet, DHCP Istemcisini yalnızca bir arabirimde çalıştırmayı hedefleyen uygulamalara yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="50d63-563">This service is intended for applications that intend to run the DHCP Client on only one interface.</span></span> <span data-ttu-id="50d63-564">Birden çok arabirimde DHCP çalıştırmak için daha fazla ayrıntı için *nx_dhcp_interface_enable* bakın.</span><span class="sxs-lookup"><span data-stu-id="50d63-564">To run DHCP on multiple interfaces see *nx_dhcp_interface_enable* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-565">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-565">Input Parameters</span></span>

- <span data-ttu-id="50d63-566">**dhcp_ptr**: DHCP denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-566">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="50d63-567">**Dizin**: cihaz ağ arabiriminin dizini</span><span class="sxs-lookup"><span data-stu-id="50d63-567">**index**: Index of device network interface</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-568">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-568">Return Values</span></span>

- <span data-ttu-id="50d63-569">**NX_SUCCESS**: (0x00) arabirimi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="50d63-569">**NX_SUCCESS**: (0x00) Interface is successfully set.</span></span>
- <span data-ttu-id="50d63-570">**NX_INVALID_INTERFACE**: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-570">**NX_INVALID_INTERFACE**: (0x4C) Invalid network interface</span></span>
- <span data-ttu-id="50d63-571">**NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) arabirim DHCP için etkinleştirildi</span><span class="sxs-lookup"><span data-stu-id="50d63-571">**NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) Interface enabled for DHCP</span></span>
- <span data-ttu-id="50d63-572">**NX_DHCP_NO_RECORDS_AVAILABLE**: (0xa7) başka bir kayıt yok</span><span class="sxs-lookup"><span data-stu-id="50d63-572">**NX_DHCP_NO_RECORDS_AVAILABLE**: (0xA7) No record available for another</span></span> 
- <span data-ttu-id="50d63-573">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-573">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-574">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-574">Allowed From</span></span>

<span data-ttu-id="50d63-575">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-575">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-576">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-576">Example</span></span>

```c
/* Set the DHCP Client interface to the secondary interface (index 1).  */
status =  nx_dhcp_set_interface_index(&my_dhcp, 1);
/* If status is NX_SUCCESS a DHCP interface was successfully set.  */
```

## <a name="nx_dhcp_start"></a><span data-ttu-id="50d63-577">nx_dhcp_start</span><span class="sxs-lookup"><span data-stu-id="50d63-577">nx_dhcp_start</span></span>

<span data-ttu-id="50d63-578">DHCP işlemesini Başlat</span><span class="sxs-lookup"><span data-stu-id="50d63-578">Start DHCP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-579">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-579">Prototype</span></span>

```c
UINT nx_dhcp_start(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-580">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-580">Description</span></span>

<span data-ttu-id="50d63-581">Bu hizmet DHCP için etkinleştirilen tüm arabirimlerde DHCP işlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="50d63-581">This service starts DHCP processing on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="50d63-582">Varsayılan olarak, uygulama nx_dhcp_create çağırdığında, birincil arabirim DHCP için etkinleştirilir *.*</span><span class="sxs-lookup"><span data-stu-id="50d63-582">By default the primary interface is enabled for DHCP when the application calls *nx_dhcp_create.*</span></span>

<span data-ttu-id="50d63-583">IP örneğinin DHCP Istemci arabirimindeki bir IP adresine bağlı olduğunu doğrulamak için *nx_ip_status_check* kullanarak IP adresinin geçerli olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="50d63-583">To verify when the IP instance is bound to an IP address on the DHCP Client interface, use *nx_ip_status_check* to see confirm the IP address is valid.</span></span>

<span data-ttu-id="50d63-584">Zaten DHCP çalıştıran başka arabirimler varsa, bu hizmet bu hizmet tarafından etkilenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="50d63-584">If there are other interfaces already running DHCP, this service will not affect them.</span></span>

<span data-ttu-id="50d63-585">Birden çok arabirim etkinleştirildiğinde, belirli bir arabirimde DHCP 'yi başlatmak için *nx_dhcp_interface_start* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="50d63-585">To start DHCP on a specific interface when multiple interfaces are enabled, use the *nx_dhcp_interface_start* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-586">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-586">Input Parameters</span></span>

- <span data-ttu-id="50d63-587">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-587">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-588">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-588">Return Values</span></span>

- <span data-ttu-id="50d63-589">**NX_SUCCESS**: (0x00) başarılı DHCP başlatması.</span><span class="sxs-lookup"><span data-stu-id="50d63-589">**NX_SUCCESS**: (0x00) Successful DHCP start.</span></span>  
- <span data-ttu-id="50d63-590">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="50d63-590">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP already started.</span></span>
- <span data-ttu-id="50d63-591">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-591">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="50d63-592">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="50d63-592">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-593">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-593">Allowed From</span></span>

<span data-ttu-id="50d63-594">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-594">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-595">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-595">Example</span></span>

```c
/* Start the DHCP processing for this IP instance.  */
status =  nx_dhcp_start(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully started.  */
```

## <a name="nx_dhcp_interface_start"></a><span data-ttu-id="50d63-596">nx_dhcp_interface_start</span><span class="sxs-lookup"><span data-stu-id="50d63-596">nx_dhcp_interface_start</span></span>

<span data-ttu-id="50d63-597">Belirtilen arabirimde DHCP işlemeyi Başlat</span><span class="sxs-lookup"><span data-stu-id="50d63-597">Start DHCP processing on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-598">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-598">Prototype</span></span>

```c
UINT nx_dhcp_interface_start(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="50d63-599">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-599">Description</span></span>

<span data-ttu-id="50d63-600">Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirim üzerinde DHCP işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="50d63-600">This service starts DHCP processing on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="50d63-601">DHCP için bir arabirim etkinleştirme hakkında daha fazla ayrıntı için bkz. *nx_dhcp_interface_enable*().</span><span class="sxs-lookup"><span data-stu-id="50d63-601">See *nx_dhcp_interface_enable*() for more details about enabling an interface for DHCP.</span></span> <span data-ttu-id="50d63-602">Varsayılan olarak, uygulama nx_dhcp_create çağırdığında, birincil arabirim DHCP için etkinleştirilir *.*</span><span class="sxs-lookup"><span data-stu-id="50d63-602">By default the primary interface is enabled for DHCP when the application calls *nx_dhcp_create.*</span></span>

<span data-ttu-id="50d63-603">DHCP Istemcisi çalıştıran başka arabirim yoksa, bu hizmet DHCP istemci iş parçacığını başlatır/sürdürür ve (yeniden) DHCP Istemci zamanlayıcısını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="50d63-603">If there are no other interfaces running DHCP Client this service will start/resume the DHCP Client thread and (re)activate the DHCP Client timer.</span></span>  
  
<span data-ttu-id="50d63-604">Uygulamanın bir IP adresinin elde olup olmadığını doğrulamak için *nx_ip_status_check* kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50d63-604">The application should use *nx_ip_status_check* to verify if an IP address is obtained.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-605">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-605">Input Parameters</span></span>

- <span data-ttu-id="50d63-606">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-606">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="50d63-607">**Interface_index**: DHCP istemcisinin başlatılacağı Dizin</span><span class="sxs-lookup"><span data-stu-id="50d63-607">**Interface_index**: Index on which to start the DHCP Client</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-608">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-608">Return Values</span></span>

- <span data-ttu-id="50d63-609">**NX_SUCCESS**: (0x00) başarılı DHCP başlatması.</span><span class="sxs-lookup"><span data-stu-id="50d63-609">**NX_SUCCESS**: (0x00) Successful DHCP start.</span></span> 
- <span data-ttu-id="50d63-610">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="50d63-610">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP already started.</span></span>
- <span data-ttu-id="50d63-611">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-611">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="50d63-612">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="50d63-612">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="50d63-613">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-613">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-614">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-614">Allowed From</span></span>

<span data-ttu-id="50d63-615">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-615">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-616">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-616">Example</span></span>

```c
/* Start the DHCP processing for this IP instance on interface 1.  */
status =  nx_dhcp_interface_start(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully started.  */
```

## <a name="nx_dhcp_state_change_notify"></a><span data-ttu-id="50d63-617">nx_dhcp_state_change_notify</span><span class="sxs-lookup"><span data-stu-id="50d63-617">nx_dhcp_state_change_notify</span></span>

<span data-ttu-id="50d63-618">DHCP durum değiştirme geri çağırma işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="50d63-618">Set DHCP state change callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-619">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-619">Prototype</span></span>

```c
UINT nx_dhcp_state_change_notify(NX_DHCP *dhcp_ptr, 
                                 VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, UCHAR new_state));
```

### <a name="description"></a><span data-ttu-id="50d63-620">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-620">Description</span></span>

<span data-ttu-id="50d63-621">Bu hizmet, DHCP durum değişikliklerinin bir uygulamasına bildirimde bulunmak için dhcp_state_change_notify belirtilen geri çağırma işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="50d63-621">This service registers the specified callback function dhcp_state_change_notify for notifying an application of DHCP state changes.</span></span> <span data-ttu-id="50d63-622">Geri arama işlevi, DHCP Istemcisinin geçiş durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="50d63-622">The callback function supplies the state the DHCP Client has transitioned into.</span></span>

<span data-ttu-id="50d63-623">Aşağıdakiler, çeşitli DHCP durumlarıyla ilişkili değerlerdir:</span><span class="sxs-lookup"><span data-stu-id="50d63-623">Following are values associated with the various DHCP states:</span></span>

- <span data-ttu-id="50d63-624">NX_DHCP_STATE_BOOT: 1</span><span class="sxs-lookup"><span data-stu-id="50d63-624">NX_DHCP_STATE_BOOT: 1</span></span>
- <span data-ttu-id="50d63-625">NX_DHCP_STATE_INIT: 2</span><span class="sxs-lookup"><span data-stu-id="50d63-625">NX_DHCP_STATE_INIT: 2</span></span>
- <span data-ttu-id="50d63-626">NX_DHCP_STATE_SELECTING: 3</span><span class="sxs-lookup"><span data-stu-id="50d63-626">NX_DHCP_STATE_SELECTING: 3</span></span>
- <span data-ttu-id="50d63-627">NX_DHCP_STATE_REQUESTING: 4</span><span class="sxs-lookup"><span data-stu-id="50d63-627">NX_DHCP_STATE_REQUESTING: 4</span></span>
- <span data-ttu-id="50d63-628">NX_DHCP_STATE_BOUND: 5</span><span class="sxs-lookup"><span data-stu-id="50d63-628">NX_DHCP_STATE_BOUND: 5</span></span>
- <span data-ttu-id="50d63-629">NX_DHCP_STATE_RENEWING: 6</span><span class="sxs-lookup"><span data-stu-id="50d63-629">NX_DHCP_STATE_RENEWING: 6</span></span>
- <span data-ttu-id="50d63-630">NX_DHCP_STATE_REBINDING: 7</span><span class="sxs-lookup"><span data-stu-id="50d63-630">NX_DHCP_STATE_REBINDING: 7</span></span>
- <span data-ttu-id="50d63-631">NX_DHCP_STATE_FORCERENEW: 8</span><span class="sxs-lookup"><span data-stu-id="50d63-631">NX_DHCP_STATE_FORCERENEW: 8</span></span>
- <span data-ttu-id="50d63-632">NX_DHCP_STATE_ADDRESS_PROBING: 9</span><span class="sxs-lookup"><span data-stu-id="50d63-632">NX_DHCP_STATE_ADDRESS_PROBING: 9</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-633">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-633">Input Parameters</span></span>

- <span data-ttu-id="50d63-634">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-634">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="50d63-635">**dhcp_state_change_notify**: durum değiştirme geri çağırma işlev işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-635">**dhcp_state_change_notify**: State change callback function pointer</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-636">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-636">Return Values</span></span>

- <span data-ttu-id="50d63-637">**NX_SUCCESS**: (0x00) başarılı geri arama kümesi.</span><span class="sxs-lookup"><span data-stu-id="50d63-637">**NX_SUCCESS**: (0x00) Successful callback set.</span></span>  
- <span data-ttu-id="50d63-638">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-638">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="50d63-639">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="50d63-639">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-640">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-640">Allowed From</span></span>

<span data-ttu-id="50d63-641">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="50d63-641">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="50d63-642">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-642">Example</span></span>

```c
/* Register the “my_state_change” function to be called on any DHCP state change, assuming DHCP has alreadybeen created.  */
status =  nx_dhcp_state_change_notify(&my_dhcp, my_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered.  */
```

## <a name="nx_dhcp_interface_state_change_notify"></a><span data-ttu-id="50d63-643">nx_dhcp_interface_state_change_notify</span><span class="sxs-lookup"><span data-stu-id="50d63-643">nx_dhcp_interface_state_change_notify</span></span>

<span data-ttu-id="50d63-644">Belirtilen arabirimdeki DHCP durum değiştirme geri çağırma işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="50d63-644">Set DHCP state change callback function on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-645">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-645">Prototype</span></span>

```c
UINT nx_dhcp_interface_state_change_notify(NX_DHCP *dhcp_ptr, UINT interface_index,
                                           VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                                                            UINT interface_index,
                                                                            UCHAR new_state));
```

### <a name="description"></a><span data-ttu-id="50d63-646">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-646">Description</span></span>

<span data-ttu-id="50d63-647">Bu hizmet, DHCP durum değişikliklerinin bir uygulamasına bildirimde bulunmak için belirtilen geri çağırma işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="50d63-647">This service registers the specified callback function for notifying an application of DHCP state changes.</span></span> <span data-ttu-id="50d63-648">Geri çağırma, funcıton giriş bağımsız değişkenleri, arabirim dizinidir ve DHCP Istemcisinin bu arabirimde geçiş olduğu durumdur.</span><span class="sxs-lookup"><span data-stu-id="50d63-648">The callback funciton input arguments are the interface index and the state the DHCP Client has transitioned to on that interface.</span></span>

<span data-ttu-id="50d63-649">Durum değişikliği işlevleri hakkında daha fazla bilgi için bkz. *nx_dhcp_state_change_notify*().</span><span class="sxs-lookup"><span data-stu-id="50d63-649">For more information about state change functions, see *nx_dhcp_state_change_notify*().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-650">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-650">Input Parameters</span></span>

- <span data-ttu-id="50d63-651">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-651">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="50d63-652">**dhcp_interface_state_change_notify**: uygulama geri çağırma işlev işaretçisi</span><span class="sxs-lookup"><span data-stu-id="50d63-652">**dhcp_interface_state_change_notify**: Application callback function pointer</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-653">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-653">Return Values</span></span>

- <span data-ttu-id="50d63-654">**NX_SUCCESS**: (0x00) başarılı geri arama kümesi.</span><span class="sxs-lookup"><span data-stu-id="50d63-654">**NX_SUCCESS**: (0x00) Successful callback set.</span></span>  
- <span data-ttu-id="50d63-655">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-655">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-656">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-656">Allowed From</span></span>

<span data-ttu-id="50d63-657">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="50d63-657">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="50d63-658">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-658">Example</span></span>

```c
/* Register the “my_state_change” function to be called on any DHCP state change,   
   assuming DHCP has alreadybeen created.  */

void dhcp_interstate_state_change(NX_DHCP *dhcp_ptr, UINT iface_index, 
                                  UCHAR new_state);


status =  nx_dhcp_interstate_state_change_notify(&my_dhcp,  
                                                 dhcp_interstate_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered.  */
```

## <a name="nx_dhcp_stop"></a><span data-ttu-id="50d63-659">nx_dhcp_stop</span><span class="sxs-lookup"><span data-stu-id="50d63-659">nx_dhcp_stop</span></span>

<span data-ttu-id="50d63-660">DHCP işlemesini durduruyor</span><span class="sxs-lookup"><span data-stu-id="50d63-660">Stops DHCP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-661">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-661">Prototype</span></span>

```c
UINT nx_dhcp_stop(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-662">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-662">Description</span></span>

<span data-ttu-id="50d63-663">Bu hizmet, DHCP işlemesini Başlatan tüm arabirimlerde DHCP işlemeyi durduruyor.</span><span class="sxs-lookup"><span data-stu-id="50d63-663">This service stops DHCP processing on all interfaces that have started DHCP processing.</span></span> <span data-ttu-id="50d63-664">DHCP 'yi işleyen bir arabirim yoksa, bu hizmet DHCP Istemci iş parçacığını askıya alacak ve DHCP Istemci zamanlayıcısını devre dışı kalacak.</span><span class="sxs-lookup"><span data-stu-id="50d63-664">If there are no interfaces processing DHCP, this service will suspend the DHCP Client thread, and inactivate the DHCP Client timer.</span></span>

<span data-ttu-id="50d63-665">DHCP için birden çok arabirim etkinleştirilmişse, belirli bir arabirimdeki DHCP 'yi durdurmak için *nx_dhcp_interface_stop* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="50d63-665">To stop DHCP on a specific interface if multiple interfaces are enabled for DHCP, use the *nx_dhcp_interface_stop* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-666">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-666">Input Parameters</span></span>

- <span data-ttu-id="50d63-667">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-667">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-668">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-668">Return Values</span></span>

- <span data-ttu-id="50d63-669">**NX_SUCCESS**: (0x00) başarılı DHCP durağı</span><span class="sxs-lookup"><span data-stu-id="50d63-669">**NX_SUCCESS**: (0x00) Successful DHCP stop</span></span>
- <span data-ttu-id="50d63-670">**NX_DHCP_NOT_STARTED**: (0x96) DHCP örneği başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="50d63-670">**NX_DHCP_NOT_STARTED**: (0x96) The DHCP instance not started.</span></span>
- <span data-ttu-id="50d63-671">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-671">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="50d63-672">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="50d63-672">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-673">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-673">Allowed From</span></span>

<span data-ttu-id="50d63-674">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-674">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-675">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-675">Example</span></span>

```c
/* Stop the DHCP processing for this IP instance.  */
status =  nx_dhcp_stop(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully stopped.  */
```

## <a name="nx_dhcp_interface_stop"></a><span data-ttu-id="50d63-676">nx_dhcp_interface_stop</span><span class="sxs-lookup"><span data-stu-id="50d63-676">nx_dhcp_interface_stop</span></span>

<span data-ttu-id="50d63-677">Belirtilen arabirimdeki DHCP işlemesini durdur</span><span class="sxs-lookup"><span data-stu-id="50d63-677">Stop DHCP processing on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-678">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-678">Prototype</span></span>

```c
UINT nx_dhcp_interface_stop(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="50d63-679">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-679">Description</span></span>

<span data-ttu-id="50d63-680">Bu hizmet, DHCP zaten başlatılmışsa belirtilen arabirimdeki DHCP işlemesini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="50d63-680">This service stops DHCP processing on the specified interface if DHCP is already started.</span></span> <span data-ttu-id="50d63-681">DHCP çalıştıran başka arabirimler yoksa, DHCP iş parçacığı ve Zamanlayıcı askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="50d63-681">If there are no other interfaces running DHCP, the DHCP thread and timer are suspended.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-682">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-682">Input Parameters</span></span>

- <span data-ttu-id="50d63-683">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-683">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="50d63-684">**Interface_index**: DHCP işleminin durdurulacağı arabirim</span><span class="sxs-lookup"><span data-stu-id="50d63-684">**Interface_index**: Interface on which to stop DHCP processing</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-685">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-685">Return Values</span></span>

- <span data-ttu-id="50d63-686">**NX_SUCCESS**: (0x00) başarılı DHCP durağı</span><span class="sxs-lookup"><span data-stu-id="50d63-686">**NX_SUCCESS**: (0x00) Successful DHCP stop</span></span>
- <span data-ttu-id="50d63-687">**NX_DHCP_NOT_STARTED**: (0x96) DHCP başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="50d63-687">**NX_DHCP_NOT_STARTED**: (0x96) DHCP not started.</span></span>
- <span data-ttu-id="50d63-688">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-688">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="50d63-689">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="50d63-689">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="50d63-690">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-690">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-691">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-691">Allowed From</span></span>

<span data-ttu-id="50d63-692">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-692">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-693">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-693">Example</span></span>

```c
/* Stop DHCP processing for this IP instance on interface 1.  */
status =  nx_dhcp_interface_stop(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully stopped.  */
```

## <a name="nx_dhcp_user_option_retrieve"></a><span data-ttu-id="50d63-694">nx_dhcp_user_option_retrieve</span><span class="sxs-lookup"><span data-stu-id="50d63-694">nx_dhcp_user_option_retrieve</span></span>

<span data-ttu-id="50d63-695">Son sunucu yanıtından bir DHCP seçeneği alın</span><span class="sxs-lookup"><span data-stu-id="50d63-695">Retrieve a DHCP option from last server response</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-696">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-696">Prototype</span></span>

```c
UINT nx_dhcp_user_option_retrieve(NX_DHCP *dhcp_ptr, UINT request_option, 
                                  UCHAR *destination_ptr, UINT *destination_size);
```

### <a name="description"></a><span data-ttu-id="50d63-697">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-697">Description</span></span>

<span data-ttu-id="50d63-698">Bu hizmet, DHCP Istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP seçenekleri arabelleğinden belirtilen DHCP seçeneğini alır.</span><span class="sxs-lookup"><span data-stu-id="50d63-698">This service retrieves the specified DHCP option from the DHCP options buffer on the first interface enabled for DHCP found on the DHCP Client record.</span></span> <span data-ttu-id="50d63-699">Başarılı olursa, seçenek verileri belirtilen arabelleğe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="50d63-699">If successful, the option data is copied into the specified buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-700">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-700">Input Parameters</span></span>

- <span data-ttu-id="50d63-701">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-701">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>  
- <span data-ttu-id="50d63-702">**request_option**: DHCP seçeneği, RFC 'ler tarafından belirtilen şekilde.</span><span class="sxs-lookup"><span data-stu-id="50d63-702">**request_option**: DHCP option, as specified by the RFCs.</span></span> <span data-ttu-id="50d63-703">*Nxd_dhcp_client. h* içindeki NX_DHCP_OPTION seçeneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="50d63-703">See the NX_DHCP_OPTION option in *nxd_dhcp_client.h*.</span></span>
- <span data-ttu-id="50d63-704">**destination_ptr**: Yanıt dizesi için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-704">**destination_ptr**: Pointer to the destination for the response string.</span></span>  
- <span data-ttu-id="50d63-705">**destination_size**: hedefin boyutuna ve dönüşe ilişkin işaretçi, döndürülen bayt sayısını yerleştirmek için hedef.</span><span class="sxs-lookup"><span data-stu-id="50d63-705">**destination_size**: Pointer to the size of the destination and on return, the destination to place the number of bytes returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-706">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-706">Return Values</span></span>

- <span data-ttu-id="50d63-707">**NX_SUCCESS**: (0x00) başarılı seçenek alma.</span><span class="sxs-lookup"><span data-stu-id="50d63-707">**NX_SUCCESS**: (0x00) Successful option retrieval.</span></span>  
- <span data-ttu-id="50d63-708">**NX_DHCP_NOT_BOUND**: (0x94) DHCP istemcisi bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="50d63-708">**NX_DHCP_NOT_BOUND**: (0x94) DHCP Client not bound.</span></span>
- <span data-ttu-id="50d63-709">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xa5) DHCP için etkinleştirilen arabirim yok</span><span class="sxs-lookup"><span data-stu-id="50d63-709">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) No interfaces enabled for DHCP</span></span>
- <span data-ttu-id="50d63-710">**NX_DHCP_DEST_TO_SMALL**: (0x95) hedef, yanıtı tutmak için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="50d63-710">**NX_DHCP_DEST_TO_SMALL**: (0x95) Destination is too small to hold response.</span></span>
- <span data-ttu-id="50d63-711">**NX_DHCP_PARSE_ERROR**: (0x97) seçeneği sunucu yanıtında bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="50d63-711">**NX_DHCP_PARSE_ERROR**: (0x97) Option not found in Server response.</span></span>
- <span data-ttu-id="50d63-712">NX_PTR_ERROR: (0x16) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-712">NX_PTR_ERROR: (0x16) Invalid input pointer.</span></span>
- <span data-ttu-id="50d63-713">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="50d63-713">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-714">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-714">Allowed From</span></span>

<span data-ttu-id="50d63-715">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-715">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-716">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-716">Example</span></span>

```c
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server.  */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_user_option_retrieve(&my_dhcp, NX_DHCP_OPTION_DNS_SVR,
                                        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string.  */
```

## <a name="nx_dhcp_interface_user_option_retrieve"></a><span data-ttu-id="50d63-717">nx_dhcp_interface_user_option_retrieve</span><span class="sxs-lookup"><span data-stu-id="50d63-717">nx_dhcp_interface_user_option_retrieve</span></span>

<span data-ttu-id="50d63-718">Belirtilen arabirimdeki son sunucu yanıtından bir DHCP seçeneği alın</span><span class="sxs-lookup"><span data-stu-id="50d63-718">Retrieve a DHCP option from last server response on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-719">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-719">Prototype</span></span>

```c
UINT nx_dhcp_interface_user_option_retrieve(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            UINT request_option, UCHAR *destination_ptr,
                                            UINT *destination_size);
```

### <a name="description"></a><span data-ttu-id="50d63-720">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-720">Description</span></span>

<span data-ttu-id="50d63-721">Bu hizmet, belirtilen arabirim DHCP için etkinleştirilirse belirtilen arabirimdeki DHCP seçenekleri arabelleğinden belirtilen DHCP seçeneğini alır.</span><span class="sxs-lookup"><span data-stu-id="50d63-721">This service retrieves the specified DHCP option from the DHCP options buffer on the specified interface, if that interface is enabled for DHCP.</span></span> <span data-ttu-id="50d63-722">Başarılı olursa, seçenek verileri belirtilen arabelleğe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="50d63-722">If successful, the option data is copied into the specified buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-723">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-723">Input Parameters</span></span>

- <span data-ttu-id="50d63-724">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-724">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="50d63-725">**Interface_index**: belirtilen seçeneğin alınacağı dizin</span><span class="sxs-lookup"><span data-stu-id="50d63-725">**Interface_index**: Index on which to retrieve the specified option</span></span>
- <span data-ttu-id="50d63-726">**request_option**: DHCP seçeneği, RFC 'ler tarafından belirtilen şekilde.</span><span class="sxs-lookup"><span data-stu-id="50d63-726">**request_option**: DHCP option, as specified by the RFCs.</span></span> <span data-ttu-id="50d63-727">NX_DHCP_OPTION seçeneğine bakın: *nxd_dhcp_client. h*.</span><span class="sxs-lookup"><span data-stu-id="50d63-727">See the NX_DHCP_OPTION option: in *nxd_dhcp_client.h*.</span></span>  
- <span data-ttu-id="50d63-728">**destination_ptr**: Yanıt dizesi için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-728">**destination_ptr**: Pointer to the destination for the response string.</span></span>  
- <span data-ttu-id="50d63-729">**destination_size**: hedefin boyutuna ve dönüşe ilişkin işaretçi, döndürülen bayt sayısını yerleştirmek için hedef.</span><span class="sxs-lookup"><span data-stu-id="50d63-729">**destination_size**: Pointer to the size of the destination and on return, the destination to place the number of bytes returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-730">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-730">Return Values</span></span>

- <span data-ttu-id="50d63-731">**NX_SUCCESS**: (0x00) başarılı seçenek alma.</span><span class="sxs-lookup"><span data-stu-id="50d63-731">**NX_SUCCESS**: (0x00) Successful option retrieval.</span></span>  
- <span data-ttu-id="50d63-732">**NX_DHCP_NOT_BOUND**: (0x94) IP adresi atanmadı</span><span class="sxs-lookup"><span data-stu-id="50d63-732">**NX_DHCP_NOT_BOUND**: (0x94) IP address not assigned</span></span>
- <span data-ttu-id="50d63-733">**NX_DHCP_DEST_TO_SMALL**: (0x95) arabellek çok küçük</span><span class="sxs-lookup"><span data-stu-id="50d63-733">**NX_DHCP_DEST_TO_SMALL**: (0x95) Buffer is too small</span></span>
- <span data-ttu-id="50d63-734">**NX_DHCP_PARSE_ERROR**: (0x97) DHCP seçeneği sunucu yanıtında bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="50d63-734">**NX_DHCP_PARSE_ERROR**: (0x97) DHCP Option not found in Server response.</span></span>
- <span data-ttu-id="50d63-735">NX_PTR_ERROR: (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-735">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="50d63-736">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="50d63-736">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="50d63-737">NX_INVALID_INTERFACE: (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="50d63-737">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-738">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-738">Allowed From</span></span>

<span data-ttu-id="50d63-739">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-739">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-740">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-740">Example</span></span>

```c
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server on the prmary interface.  */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_interface_user_option_retrieve(&my_dhcp, 0, NX_DHCP_OPTION_DNS_SVR,
                                                  dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string.  */
```

## <a name="nx_dhcp_user_option_convert"></a><span data-ttu-id="50d63-741">nx_dhcp_user_option_convert</span><span class="sxs-lookup"><span data-stu-id="50d63-741">nx_dhcp_user_option_convert</span></span>

<span data-ttu-id="50d63-742">Dört baytı ULONG 'a Dönüştür</span><span class="sxs-lookup"><span data-stu-id="50d63-742">Convert four bytes to ULONG</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-743">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-743">Prototype</span></span>

```c
ULONG nx_dhcp_user_option_convert(UCHAR *option_string_ptr);
```

### <a name="description"></a><span data-ttu-id="50d63-744">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-744">Description</span></span>

<span data-ttu-id="50d63-745">Bu hizmet, "option_string_ptr" ile işaret edilen dört karakteri işaretsiz bir Long değere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="50d63-745">This service converts the four characters pointed to by “option_string_ptr” into an unsigned long value.</span></span> <span data-ttu-id="50d63-746">Bu, özellikle IP adresleri olduğunda yararlıdır</span><span class="sxs-lookup"><span data-stu-id="50d63-746">It is especially useful when IP addresses are</span></span>  
<span data-ttu-id="50d63-747">görüntülemeyen.</span><span class="sxs-lookup"><span data-stu-id="50d63-747">present.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-748">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-748">Input Parameters</span></span>

- <span data-ttu-id="50d63-749">**option_string_ptr**: daha önce alınan seçenek dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-749">**option_string_ptr**: Pointer to previously retrieved option string.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-750">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-750">Return Values</span></span>

- <span data-ttu-id="50d63-751">**Değer**: ilk dört baytın değeri.</span><span class="sxs-lookup"><span data-stu-id="50d63-751">**Value**: Value of first four bytes.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-752">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-752">Allowed From</span></span>

<span data-ttu-id="50d63-753">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-753">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-754">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-754">Example</span></span>

```c
UCHAR  dns_ip_string[4];
ULONG  dns_ip;

/* Convert the first four bytes of “dns_ip_string” to an actual IP
address in “dns_ip.”  */
dns_ip=  nx_dhcp_user_option_convert(dns_ip_string);

/* If status is NX_SUCCESS the DNS IP address is in “dns_ip.”  */
```

## <a name="nx_dhcp_user_option_add_callback_set"></a><span data-ttu-id="50d63-755">nx_dhcp_user_option_add_callback_set</span><span class="sxs-lookup"><span data-stu-id="50d63-755">nx_dhcp_user_option_add_callback_set</span></span>

<span data-ttu-id="50d63-756">Kullanıcı tarafından sağlanan seçenekleri eklemek için geri çağırma işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="50d63-756">Set callback function for adding user supplied options</span></span>

### <a name="prototype"></a><span data-ttu-id="50d63-757">Prototype</span><span class="sxs-lookup"><span data-stu-id="50d63-757">Prototype</span></span>

```c
ULONG nx_dhcp_user_option_add_callbcak_set(NX_DHCP *dhcp_ptr, 
                                           UINT (*dhcp_user_option_add)(NX_DHCP *dhcp_ptr, 
                                                                        UINT iface_index, 
                                                                        UINT message_type, 
                                                                        UCHAR *user_option_ptr, 
                                                                        UINT *user_option_length));
```

### <a name="description"></a><span data-ttu-id="50d63-758">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50d63-758">Description</span></span>

<span data-ttu-id="50d63-759">Bu hizmet, Kullanıcı tarafından sağlanan seçenekleri eklemek için belirtilen geri çağırma işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="50d63-759">This service registers the specified callback function for adding user supplied options.</span></span>

<span data-ttu-id="50d63-760">Geri çağırma işlevi belirtilmişse, uygulamalar iface_index ve message_type tarafından pakete Kullanıcı tarafından sağlanan seçenekleri ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="50d63-760">If the callback function specified, the applications can add user supplied options into the packet by iface_index and message_type.</span></span>

>[!NOTE] 
> <span data-ttu-id="50d63-761">Kullanıcı yordamında.</span><span class="sxs-lookup"><span data-stu-id="50d63-761">In user’s routine.</span></span> <span data-ttu-id="50d63-762">Kullanıcı tarafından sağlanan seçenekler eklerken uygulamaların DHCP seçenekleri biçimi gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="50d63-762">Applications must follow the DHCP options format when add user supplied options.</span></span> <span data-ttu-id="50d63-763">Kullanıcı seçeneklerinin toplam boyutu user_option_length küçük veya eşit olmalı ve user_option_length gerçek seçenek uzunluğu olarak güncellenebilir.</span><span class="sxs-lookup"><span data-stu-id="50d63-763">The total size of user options must be less or equal to user_option_length, and update the user_option_length as real options length.</span></span> <span data-ttu-id="50d63-764">Seçenek başarıyla Ekle ' NX_TRUE döndürün, aksi NX_FALSE döndürün.</span><span class="sxs-lookup"><span data-stu-id="50d63-764">Return NX_TRUE if add options successfully, else return NX_FALSE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="50d63-765">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="50d63-765">Input Parameters</span></span>

- <span data-ttu-id="50d63-766">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-766">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="50d63-767">**dhcp_user_option_add**: Kullanıcı seçeneği ekleme işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="50d63-767">**dhcp_user_option_add**: Pointer to user option add function.</span></span>

### <a name="return-values"></a><span data-ttu-id="50d63-768">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="50d63-768">Return Values</span></span>

- <span data-ttu-id="50d63-769">**NX_SUCCESS**: (0x00) başarılı geri arama kümesi.</span><span class="sxs-lookup"><span data-stu-id="50d63-769">**NX_SUCCESS**: (0x00) Successful callback set.</span></span>
- <span data-ttu-id="50d63-770">NX_PTR_ERROR: (0x16) geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="50d63-770">NX_PTR_ERROR: (0x16) Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="50d63-771">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="50d63-771">Allowed From</span></span>

<span data-ttu-id="50d63-772">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="50d63-772">Threads</span></span>

### <a name="example"></a><span data-ttu-id="50d63-773">Örnek</span><span class="sxs-lookup"><span data-stu-id="50d63-773">Example</span></span>

```c
/* Register the “my_dhcp_user_option_add” function to be called when add DHCP
options, assuming DHCP has already been created.  */

status =  nx_dhcp_user_option_add_callback_set(&my_dhcp, my_dhcp_user_option_add);

/* If status is NX_SUCCESS the callback function was successfully registered.  */

```

