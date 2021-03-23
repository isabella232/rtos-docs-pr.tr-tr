---
title: Bölüm 3-Azure RTOS NetX DHCP Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX DHCP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8a614d22eca4fe693209751d72958b7d975c64c2
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826795"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-client-services"></a><span data-ttu-id="78432-103">Bölüm 3-Azure RTOS NetX DHCP Istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="78432-103">Chapter 3 - Description of Azure RTOS NetX DHCP Client services</span></span>

<span data-ttu-id="78432-104">Bu bölüm, tüm Azure RTOS NetX DHCP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="78432-104">This chapter contains a description of all Azure RTOS NetX DHCP services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="78432-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="78432-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="78432-106">**nx_dhcp_create**: *DHCP örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="78432-106">**nx_dhcp_create**: *Create a DHCP instance*</span></span>

- <span data-ttu-id="78432-107">**nx_dhcp_clear_broadcast_flag**: istemci iletilerinde yayın bayrağını temizle</span><span class="sxs-lookup"><span data-stu-id="78432-107">**nx_dhcp_clear_broadcast_flag**: Clear broadcast flag on Client messages</span></span>

- <span data-ttu-id="78432-108">**nx_dhcp_delete**: *bir DHCP örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="78432-108">**nx_dhcp_delete**: *Delete a DHCP instance*</span></span>

- <span data-ttu-id="78432-109">**nx_dhcp_decline**: *sunucuya reddetme iletisi* gönder</span><span class="sxs-lookup"><span data-stu-id="78432-109">**nx_dhcp_decline**: Send *Decline message to server*</span></span>

- <span data-ttu-id="78432-110">**nx_dhcp_force_renew**: *zorla yenileme iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="78432-110">**nx_dhcp_force_renew**: *Send force renew message*</span></span>

- <span data-ttu-id="78432-111">**nx_dhcp_packet_pool_set**: *DHCP istemci paket havuzunu ayarlama*</span><span class="sxs-lookup"><span data-stu-id="78432-111">**nx_dhcp_packet_pool_set**: *Set the DHCP Client packet pool*</span></span>

- <span data-ttu-id="78432-112">**nx_dhcp_release**: *sunucuya sürüm iletisi* gönder</span><span class="sxs-lookup"><span data-stu-id="78432-112">**nx_dhcp_release**: Send *Release message to server*</span></span>

- <span data-ttu-id="78432-113">**nx_dhcp_reinitialize**: *DHCP istemci ağı parametrelerini temizle*</span><span class="sxs-lookup"><span data-stu-id="78432-113">**nx_dhcp_reinitialize**: *Clear DHCP client network parameters*</span></span>

- <span data-ttu-id="78432-114">**nx_dhcp_request_client_ip**: *belirli bir IP adresi belirtin*</span><span class="sxs-lookup"><span data-stu-id="78432-114">**nx_dhcp_request_client_ip**: *Specify a specific IP address*</span></span>

- <span data-ttu-id="78432-115">**nx_dhcp_send_request**: *sunucuya DHCP iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="78432-115">**nx_dhcp_send_request**: *Send DHCP message to server*</span></span>

- <span data-ttu-id="78432-116">**nx_dhcp_server_address_get**: *DHCP istemcisinin DHCP sunucu adresini al*</span><span class="sxs-lookup"><span data-stu-id="78432-116">**nx_dhcp_server_address_get**: *Retrieve DHCP Client’s DHCP server address*</span></span>

- <span data-ttu-id="78432-117">**nx_dhcp_set_interface_index**: *istemci ağ arabirimini belirtin*</span><span class="sxs-lookup"><span data-stu-id="78432-117">**nx_dhcp_set_interface_index**: *Specify the Client network interface*</span></span>

- <span data-ttu-id="78432-118">**nx_dhcp_start**: *DHCP işlemeyi Başlat*</span><span class="sxs-lookup"><span data-stu-id="78432-118">**nx_dhcp_start**: *Start DHCP processing*</span></span>

- <span data-ttu-id="78432-119">**nx_dhcp_state_change_notify**: *DHCP durum değişikliğinin uygulamasına bildirme*</span><span class="sxs-lookup"><span data-stu-id="78432-119">**nx_dhcp_state_change_notify**: *Notify application of DHCP state change*</span></span>

- <span data-ttu-id="78432-120">**nx_dhcp_stop**: *DHCP işlemesini durdur*</span><span class="sxs-lookup"><span data-stu-id="78432-120">**nx_dhcp_stop**: *Stop DHCP processing*</span></span>

- <span data-ttu-id="78432-121">**nx_dhcp_user_option_retrieve**: *DHCP seçeneğini Al*</span><span class="sxs-lookup"><span data-stu-id="78432-121">**nx_dhcp_user_option_retrieve**: *Retrieve DHCP option*</span></span>

- <span data-ttu-id="78432-122">**nx_dhcp_user_option_convert**: *dört baytı ulong 'a Dönüştür*</span><span class="sxs-lookup"><span data-stu-id="78432-122">**nx_dhcp_user_option_convert**: *Convert four bytes to ULONG*</span></span>

<span data-ttu-id="78432-123">Arabirime özgü DHCP Istemci Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="78432-123">Interface specific DHCP Client services:</span></span>

- <span data-ttu-id="78432-124">**nx_dhcp_interface_clear_broadcast_flag**: *belirtilen arabirimdeki istemci iletilerinde yayın bayrağını temizle*</span><span class="sxs-lookup"><span data-stu-id="78432-124">**nx_dhcp_interface_clear_broadcast_flag**: *Clear broadcast flag on Client messages on specified interface*</span></span>

- <span data-ttu-id="78432-125">**nx_dhcp_interface_enable**: *belirtilen arabirimde DHCP çalıştırmak için arabirimi etkinleştir*</span><span class="sxs-lookup"><span data-stu-id="78432-125">**nx_dhcp_interface_enable**: *Enable interface to run DHCP on the specified interface*</span></span>

- <span data-ttu-id="78432-126">**nx_dhcp_interface_disable**: *belirtilen arabirimde DHCP çalıştırmak için arabirimi devre dışı bırak*</span><span class="sxs-lookup"><span data-stu-id="78432-126">**nx_dhcp_interface_disable**: *Disable interface to run DHCP on the specified interface*</span></span>

- <span data-ttu-id="78432-127">**nx_dhcp_interface_decline**: *belirtilen arabirimdeki sunucuya reddetme iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="78432-127">**nx_dhcp_interface_decline**: *Send Decline message to server on the specified interface*</span></span>

- <span data-ttu-id="78432-128">**nx_dhcp_interface_force_renew**: *belirtilen arabirimde zorla yenileme iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="78432-128">**nx_dhcp_interface_force_renew**: *Send a force renew message on the specified interface*</span></span>

- <span data-ttu-id="78432-129">**nx_dhcp_interface_reinitialize**: *belirtilen arabirimdeki DHCP istemci ağ parametrelerini temizle*</span><span class="sxs-lookup"><span data-stu-id="78432-129">**nx_dhcp_interface_reinitialize**: *Clear DHCP client network parameters on the specified interface*</span></span>

- <span data-ttu-id="78432-130">**nx_dhcp_interface_release**: *belirtilen arabirimdeki sunucuya sürüm iletisi gönder*</span><span class="sxs-lookup"><span data-stu-id="78432-130">**nx_dhcp_interface_release**: *Send Release message to server  on the specified interface*</span></span>

- <span data-ttu-id="78432-131">**nx_dhcp_interface_request_client_ip**: *belirtilen ARABIRIMDE belirli bir IP adresi belirtin*</span><span class="sxs-lookup"><span data-stu-id="78432-131">**nx_dhcp_interface_request_client_ip**: *Specify a specific IP address on the specified interface*</span></span>

- <span data-ttu-id="78432-132">**nx_dhcp_interface_send_request**: *belirtilen arabirimdeki DHCP iletisini sunucuya gönderin*</span><span class="sxs-lookup"><span data-stu-id="78432-132">**nx_dhcp_interface_send_request**: *Send DHCP message to server on the specified interface*</span></span>

- <span data-ttu-id="78432-133">**nx_dhcp_interface_server_address_get**: *belirtilen ARABIRIMDEKI DHCP sunucusu IP adresini al*</span><span class="sxs-lookup"><span data-stu-id="78432-133">**nx_dhcp_interface_server_address_get**: *Get the DHCP server IP address on the specified interface*</span></span>

- <span data-ttu-id="78432-134">**nx_dhcp_interface_start**: *belirtilen arabirimde DHCP istemci işlemesini Başlat*</span><span class="sxs-lookup"><span data-stu-id="78432-134">**nx_dhcp_interface_start**: *Start the DHCP Client processing on the specified interface*</span></span>

- <span data-ttu-id="78432-135">**nx_dhcp_interface_stop**: *belirtilen arabirimdeki DHCP istemci işlemesini durdur*</span><span class="sxs-lookup"><span data-stu-id="78432-135">**nx_dhcp_interface_stop**: *Stop the DHCP Client processing on the specified interface*</span></span>

- <span data-ttu-id="78432-136">**nx_dhcp_interface_state_change_notify**: *belirtilen arabirimdeki DHCP durumu değiştiğinde geri çağırma işlevini ayarla*</span><span class="sxs-lookup"><span data-stu-id="78432-136">**nx_dhcp_interface_state_change_notify**: *Set the callback function when DHCP state changes on the specified interface*</span></span>

- <span data-ttu-id="78432-137">**nx_dhcp_interface_user_option_retrieve**: belirtilen *arabirimde belirtilen DHCP seçeneğini Al*</span><span class="sxs-lookup"><span data-stu-id="78432-137">**nx_dhcp_interface_user_option_retrieve**: *Retrieve the specified DHCP option on the specified interface*</span></span>

<span data-ttu-id="78432-138">NX_DHCP_CLIENT_RESORE_STATE tanımlanmışsa DHCP Istemci Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="78432-138">DHCP Client Services if NX_DHCP_CLIENT_RESORE_STATE is defined:</span></span>

- <span data-ttu-id="78432-139">**nx_dhcp_resume**: *önceden oluşturulmuş DHCP istemci durumunu sürdürür*</span><span class="sxs-lookup"><span data-stu-id="78432-139">**nx_dhcp_resume**: *Resume previously established DHCP Client state*</span></span>

- <span data-ttu-id="78432-140">**nx_dhcp_suspend**: *DHCP istemci durumunu işlemeyi askıya al*</span><span class="sxs-lookup"><span data-stu-id="78432-140">**nx_dhcp_suspend**: *Suspend processing the DHCP Client state*</span></span>

- <span data-ttu-id="78432-141">**nx_dhcp_client_get_record**: *DHCP istemci durumunun kaydını oluşturma*</span><span class="sxs-lookup"><span data-stu-id="78432-141">**nx_dhcp_client_get_record**: *Create a record of the DHCP Client state*</span></span>

- <span data-ttu-id="78432-142">**nx_dhcp_client_restore_record**: *daha önce KAYDEDILMIŞ bir kaydı DHCP istemcisine geri yükleme*</span><span class="sxs-lookup"><span data-stu-id="78432-142">**nx_dhcp_client_restore_record**: *Restore a previously saved record to the DHCP Client*</span></span>

- <span data-ttu-id="78432-143">**nx_dhcp_client_update_time_remaining**: *geçerli DHCP durumunda kalan süreyi Güncelleştir*</span><span class="sxs-lookup"><span data-stu-id="78432-143">**nx_dhcp_client_update_time_remaining**: *Update the time remaining in the current DHCP state*</span></span>

<span data-ttu-id="78432-144">NX_DHCP_CLIENT_RESORE_STATE tanımlanmışsa arabirime özgü DHCP Istemci Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="78432-144">Interface Specific DHCP Client Services if NX_DHCP_CLIENT_RESORE_STATE is defined:</span></span>

- <span data-ttu-id="78432-145">**nx_dhcp_client_interface_get_record**: *belirtilen arabirimde DHCP istemci durumunun bir kaydını oluşturun*</span><span class="sxs-lookup"><span data-stu-id="78432-145">**nx_dhcp_client_interface_get_record**: *Create a record of the DHCP Client state on the specified interface*</span></span>

- <span data-ttu-id="78432-146">**nx_dhcp_client_interface_restore_record**: *önceden kaydedilmiş bir kaydı belirtilen arabirimdeki DHCP istemcisine geri yükleme*</span><span class="sxs-lookup"><span data-stu-id="78432-146">**nx_dhcp_client_interface_restore_record**: *Restore a previously saved record to the DHCP Client on the specified interface*</span></span>

- <span data-ttu-id="78432-147">**nx_dhcp_client_interface_update_time_remaining**: *BELIRTILEN arabirimdeki geçerli DHCP durumunda kalan süreyi Güncelleştir*</span><span class="sxs-lookup"><span data-stu-id="78432-147">**nx_dhcp_client_interface_update_time_remaining**: *Update the time remaining in the current DHCP state on the specified interface*</span></span>

## <a name="nx_dhcp_create"></a><span data-ttu-id="78432-148">nx_dhcp_create</span><span class="sxs-lookup"><span data-stu-id="78432-148">nx_dhcp_create</span></span>

<span data-ttu-id="78432-149">DHCP örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="78432-149">Create a DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-150">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-150">Prototype</span></span>

```C
UINT nx_dhcp_create(NX_DHCP *dhcp_ptr, NX_IP *ip_ptr, CHAR *name_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-151">Description</span></span>

<span data-ttu-id="78432-152">Bu hizmet, önceden oluşturulan IP örneği için bir DHCP örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="78432-152">This service creates a DHCP instance for the previously created IP instance.</span></span> <span data-ttu-id="78432-153">Varsayılan olarak, birincil arabirim DHCP çalıştırmak için etkinleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="78432-153">By default the primary interface is enabled for running DHCP.</span></span> <span data-ttu-id="78432-154">Ad girişi, DHCP Istemcisinin NetX uygulamasında kullanılmadığından, ana bilgisayar adları için RFC 1035 ölçütlerine uymalıdır.</span><span class="sxs-lookup"><span data-stu-id="78432-154">The name input, while not used in the NetX implementation of DHCP Client, must follow RFC 1035 criteria for host names.</span></span> <span data-ttu-id="78432-155">Toplam uzunluk 255 karakteri aşmamalıdır, noktalarla ayrılmış etiketlerin bir harfle başlaması ve bir harf ya da sayıyla bitmesi gerekir ve kısa çizgi içeremez, ancak alfasayısal olmayan başka karakterler içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="78432-155">The total length must not exceed 255 characters, the labels separate by dots must begin with a letter, and end with a letter or number, and may contain hyphens but no other non-alphanumeric character.</span></span>

<span data-ttu-id="78432-156">Uygulama, DHCP 'nin IP örneğiyle kaydedilmiş başka bir arabirimi çalıştırmak istiyorsanız ( *nx_ip_interface_attach* kullanarak), uygulama, DHCP 'yi yalnızca o arabirim üzerinde çalıştırmak için *nx_dhcp_set_interface_index* ÇAĞıRABILIR veya bu arabirimde DHCP çalıştırmak için *nx_dhcp_interface_enable* .</span><span class="sxs-lookup"><span data-stu-id="78432-156">If the application would like to run DHCP another interface registered with the IP instance, (using *nx_ip_interface_attach*), the application can call *nx_dhcp_set_interface_index* to run DHCP on just that interface, or *nx_dhcp_interface_enable* to run DHCP on that interface as well.</span></span> <span data-ttu-id="78432-157">Daha fazla ayrıntı için bu hizmetlerin açıklamasına bakın.</span><span class="sxs-lookup"><span data-stu-id="78432-157">See description of these services for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="78432-158">Uygulamanın, DHCP Istemci paket havuzu yükünün, RFC 2131 Bölüm 2 tarafından belirtilen en düşük DHCP ileti boyutunu (548 bayt DHCP ileti verilerinin yanı sıra UDP, IP ve fiziksel ağ çerçeve üstbilgileri) destekleyebileceğine emin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78432-158">The application must make sure the DHCP Client packet pool payload can support the minimum DHCP message size specified by the RFC 2131 Section 2 (548 bytes of DHCP message data plus UDP, IP and physical network frame headers).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-159">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-159">Input Parameters</span></span>

- <span data-ttu-id="78432-160">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-160">**dhcp_ptr** Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="78432-161">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-161">**ip_ptr** Pointer to previously created IP instance.</span></span>  
- <span data-ttu-id="78432-162">**name_ptr** DHCP örneği için ana bilgisayar adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-162">**name_ptr** Pointer to host name for DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-163">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-163">Return Values</span></span>

- <span data-ttu-id="78432-164">**NX_SUCCESS** (0x00) başarılı DHCP oluştur</span><span class="sxs-lookup"><span data-stu-id="78432-164">**NX_SUCCESS** (0x00) Successful DHCP create</span></span>

- <span data-ttu-id="78432-165">**NX_DHCP_INVALID_NAME** (0Xa8) geçersiz ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="78432-165">**NX_DHCP_INVALID_NAME** (0xA8) Invalid host name</span></span>

- <span data-ttu-id="78432-166">**NX_DHCP_INVALID_PAYLOAD** (0x9C) yükü DHCP iletisi için çok küçük</span><span class="sxs-lookup"><span data-stu-id="78432-166">**NX_DHCP_INVALID_PAYLOAD** (0x9C) Payload too small for DHCP message</span></span>

- <span data-ttu-id="78432-167">NX_PTR_ERROR (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-167">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-168">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-168">Allowed From</span></span>

<span data-ttu-id="78432-169">**Iş parçacıkları,** Başlatılmasında</span><span class="sxs-lookup"><span data-stu-id="78432-169">**Threads,** Initialization</span></span>

### <a name="example"></a><span data-ttu-id="78432-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-170">Example</span></span>

```C
/* Create a DHCP instance. */
status =  nx_dhcp_create(&my_dhcp, &my_ip, "My-DHCP");

/* If status is NX_SUCCESS a DHCP instance was successfully created. */
```

## <a name="nx_dhcp_interface_enable"></a><span data-ttu-id="78432-171">nx_dhcp_interface_enable</span><span class="sxs-lookup"><span data-stu-id="78432-171">nx_dhcp_interface_enable</span></span>

<span data-ttu-id="78432-172">Belirtilen arabirimi DHCP çalıştırmak için etkinleştir</span><span class="sxs-lookup"><span data-stu-id="78432-172">Enable the specified interface to run DHCP</span></span> 

### <a name="prototype"></a><span data-ttu-id="78432-173">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-173">Prototype</span></span>

```C
UINT nx_dhcp_interface_enable(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="78432-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-174">Description</span></span>

<span data-ttu-id="78432-175">Bu hizmet, DHCP çalıştırmak için belirtilen arabirimi sunar.</span><span class="sxs-lookup"><span data-stu-id="78432-175">This service enables the specified interface for running DHCP.</span></span> <span data-ttu-id="78432-176">Varsayılan olarak, birincil arabirim DHCP Istemcisi için etkinleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="78432-176">By default the primary interface is enabled for DHCP Client.</span></span> <span data-ttu-id="78432-177">Bu noktada, DHCP, *nx_dhcp_interface_start* çağırarak veya tüm ETKINLEŞTIRILMIŞ arabirimlerde DHCP 'yi başlatmak için bu arabirim üzerinde başlatılabilir *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="78432-177">At this point, DHCP can be started on this interface either by calling *nx_dhcp_interface_start* or to start DHCP on all enabled interfaces *nx_dhcp_start*.</span></span>

<span data-ttu-id="78432-178">Uygulamanın öncelikle nx_ip_interface_attach kullanarak bu arabirimi IP örneğiyle kaydetmesi gerektiğini aklınızda *.*</span><span class="sxs-lookup"><span data-stu-id="78432-178">Note the application must first register this interface with the IP instance, using *nx_ip_interface_attach.*</span></span>

<span data-ttu-id="78432-179">Ayrıca, bu arabirimi etkin arabirimler listesine eklemek için kullanılabilir bir DHCP Istemci arabirimi ' Record ' olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="78432-179">Further, there must be an available DHCP Client interface ‘record’ to add this interface to the list of enabled interfaces.</span></span> <span data-ttu-id="78432-180">Varsayılan olarak NX_DHCP_CLIENT_MAX_RECORDS 1 olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="78432-180">By default NX_DHCP_CLIENT_MAX_RECORDS is defined to 1.</span></span> <span data-ttu-id="78432-181">DHCP Istemcisini aynı anda çalıştırmak için beklenen en fazla arabirim sayısına bu seçeneği ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78432-181">Set this option to the maximum number of interfaces expected to run DHCP Client simultaneously.</span></span> <span data-ttu-id="78432-182">Genellikle NX_DHCP_CLIENT_MAX_RECORDS, NX_MAX_PHYSICAL_INTERFACES eşit olur; Ancak, bir cihazda DHCP Istemcisi çalıştırmak beklediğinden daha fazla fiziksel arabirim varsa, bu sayıdan daha az NX_DHCP_CLIENT_MAX_RECORDS ayarlayarak bellek tasarrufu sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="78432-182">Typically NX_DHCP_CLIENT_MAX_RECORDS will equal NX_MAX_PHYSICAL_INTERFACES; however, if a device has more physical interfaces than it expects to run DHCP Client, it can save memory by setting NX_DHCP_CLIENT_MAX_RECORDS to less than that number.</span></span> <span data-ttu-id="78432-183">DHCP Istemci arabirimi kayıtlarıyla bir fiziksel arabirimlerin eşleştirmesi bir tane değildir.</span><span class="sxs-lookup"><span data-stu-id="78432-183">There is not a one to one mapping of physical interfaces with DHCP Client interface records.</span></span>

<span data-ttu-id="78432-184">Bu hizmet ve *nx_dhcp_set_interface_index* arasındaki fark, ikinci olarak yalnızca tek BIR arabirim DHCP 'yi çalıştıracak şekilde ayarlıyor. bu hizmet, BELIRTILEN arabirimi DHCP Için etkinleştirilen istemci arabirimleri listesine ekler.</span><span class="sxs-lookup"><span data-stu-id="78432-184">The difference between this service and *nx_dhcp_set_interface_index* is the latter sets only a single interface to run DHCP whereas this service simply adds the specified interface to the list of Client interfaces enabled for DHCP.</span></span>

<span data-ttu-id="78432-185">Bir arabirimi DHCP için devre dışı bırakmak için uygulama *nx_dhcp_interface_disable* hizmetini çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="78432-185">To disable an interface for DHCP, the application can call the *nx_dhcp_interface_disable* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-186">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-186">Input Parameters</span></span>

- <span data-ttu-id="78432-187">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-187">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="78432-188">**interface_index** Üzerinde DHCP 'yi etkinleştirmek için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="78432-188">**interface_index** Index of interface to enable DHCP on</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-189">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-189">Return Values</span></span>

- <span data-ttu-id="78432-190">**NX_SUCCESS** (0x00) başarılı DHCP etkin</span><span class="sxs-lookup"><span data-stu-id="78432-190">**NX_SUCCESS** (0x00) Successful DHCP enable</span></span>

- <span data-ttu-id="78432-191">**NX_DHCP_NO_RECORDS_AVAILABLE** (0xa7) DHCP için başka bir arabirimin etkinleştirilebilmesi için kullanılabilir kayıt yok</span><span class="sxs-lookup"><span data-stu-id="78432-191">**NX_DHCP_NO_RECORDS_AVAILABLE** (0xA7) No record available for another Interface to be enabled for DHCP</span></span>

- <span data-ttu-id="78432-192">DHCP için **NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) arabirimi etkinleştirildi</span><span class="sxs-lookup"><span data-stu-id="78432-192">**NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) Interface enabled for DHCP</span></span>

- <span data-ttu-id="78432-193">NX_PTR_ERROR (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-193">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="78432-194">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-194">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-195">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-195">Allowed From</span></span>

<span data-ttu-id="78432-196">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="78432-196">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="78432-197">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-197">Example</span></span>

```C
/* Enable DHCP on a secondary interface. It is already enabled on the primary 
   interface. NX_DHCP_CLIENT_MAX_RECORDS is set to 2. */

status =  nx_dhcp_interface_enable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface was successfully enabled. */


status = nx_dhcp_start(&my_dhcp);
/* If status is NX_SUCCESS DHCP is running on interface 0 and 1. */
```

## <a name="nx_dhcp_interface_disable"></a><span data-ttu-id="78432-198">nx_dhcp_interface_disable</span><span class="sxs-lookup"><span data-stu-id="78432-198">nx_dhcp_interface_disable</span></span>

<span data-ttu-id="78432-199">DHCP çalıştırmak için belirtilen arabirimi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="78432-199">Disable the specified interface to run DHCP</span></span> 

### <a name="prototype"></a><span data-ttu-id="78432-200">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-200">Prototype</span></span>

```C
UINT nx_dhcp_interface_disable(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="78432-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-201">Description</span></span>

<span data-ttu-id="78432-202">Bu hizmet, DHCP çalıştırmak için belirtilen arabirimi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="78432-202">This service disables the specified interface for running DHCP.</span></span> <span data-ttu-id="78432-203">Bu arabirimdeki DHCP Istemcisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="78432-203">It reinitializes the DHCP Client on this interface.</span></span>

<span data-ttu-id="78432-204">DHCP Istemcisini yeniden başlatmak için, uygulamanın *nx_dhcp_interface_enable* kullanarak arabirimi yeniden etkinleştirmeleri ve *nx_dhcp_interface_start* çağırarak DHCP 'yi yeniden başlatması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78432-204">To restart the DHCP Client the application must re-enable the interface using *nx_dhcp_interface_enable* and restart DHCP by calling *nx_dhcp_interface_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-205">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-205">Input Parameters</span></span>

- <span data-ttu-id="78432-206">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-206">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="78432-207">**interface_index** DHCP 'yi devre dışı bırakmak için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="78432-207">**interface_index** Index of interface to disable DHCP on</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-208">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-208">Return Values</span></span>

- <span data-ttu-id="78432-209">**NX_SUCCESS** (0x00) başarılı DHCP oluştur</span><span class="sxs-lookup"><span data-stu-id="78432-209">**NX_SUCCESS** (0x00) Successful DHCP create</span></span>

- <span data-ttu-id="78432-210">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-210">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="78432-211">NX_PTR_ERROR (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-211">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="78432-212">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="78432-212">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="78432-213">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-213">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-214">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-214">Allowed From</span></span>

<span data-ttu-id="78432-215">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-215">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-216">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-216">Example</span></span>

```C
/* Disable DHCP on a secondary interface.
. */

status = nx_dhcp_interface_disable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface is successfully disabled. */
```

## <a name="nx_dhcp_clear_broadcast_flag"></a><span data-ttu-id="78432-217">nx_dhcp_clear_broadcast_flag</span><span class="sxs-lookup"><span data-stu-id="78432-217">nx_dhcp_clear_broadcast_flag</span></span>

<span data-ttu-id="78432-218">DHCP yayın bayrağını ayarlama</span><span class="sxs-lookup"><span data-stu-id="78432-218">Set the DHCP broadcast flag</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-219">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-219">Prototype</span></span>

```C
UINT nx_dhcp_clear_broadcast_flag(NX_DHCP *dhcp_ptr, UINT clear_flag);
```

### <a name="description"></a><span data-ttu-id="78432-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-220">Description</span></span>

<span data-ttu-id="78432-221">Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerin DHCP ileti üst bilgisini ayarlar veya temizler.</span><span class="sxs-lookup"><span data-stu-id="78432-221">This service sets or clears the broadcast flag the DHCP message header for all interfaces enabled for DHCP.</span></span> <span data-ttu-id="78432-222">Istemci bir IP adresine sahip olmadığından, bazı DHCP iletileri (örneğin, bul) yayın bayrağı Broadcast olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="78432-222">For some DHCP messages (e.g. DISCOVER) the broadcast flag is set to broadcast because the Client does not have an IP address.</span></span>

<span data-ttu-id="78432-223">__clear_flag__</span><span class="sxs-lookup"><span data-stu-id="78432-223">__clear_flag__</span></span>


- <span data-ttu-id="78432-224">**NX_TRUE** yayın bayrağı temizlendi (tek noktaya yayın yanıtı iste)</span><span class="sxs-lookup"><span data-stu-id="78432-224">**NX_TRUE** broadcast flag is cleared (request unicast response)</span></span>

- <span data-ttu-id="78432-225">**NX_FALSE** yayın bayrağı ayarlandı (Yayın yanıtı iste)</span><span class="sxs-lookup"><span data-stu-id="78432-225">**NX_FALSE** broadcast flag is set (request broadcast response)</span></span>

<span data-ttu-id="78432-226">Bu hizmet, yönlendiricinin, iletme yayını iletilerini reddettiği DHCP sunucusuna ulaşmak için bir yönlendiriciden geçmesi gereken DHCP Istemcilerine yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="78432-226">This service is intended for DHCP Clients that must go through a router to get to the DHCP Server, where the router rejects forwarding broadcast messages.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-227">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-227">Input Parameters</span></span>

- <span data-ttu-id="78432-228">**dhcp_ptr** DHCP denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-228">**dhcp_ptr** Pointer to DHCP control block</span></span>  

- <span data-ttu-id="78432-229">**clear_flag** Yayın bayrağını ayarlanacak değer</span><span class="sxs-lookup"><span data-stu-id="78432-229">**clear_flag** Value to set the broadcast flag to</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-230">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-230">Return Values</span></span>

- <span data-ttu-id="78432-231">**NX_SUCCESS** (0x00) yayın bayrağını başarıyla güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="78432-231">**NX_SUCCESS** (0x00) Successfully updated the broadcast flag</span></span>

- <span data-ttu-id="78432-232">NX_PTR_ERROR (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-232">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="78432-233">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="78432-233">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-234">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-234">Allowed From</span></span>

<span data-ttu-id="78432-235">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="78432-235">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="78432-236">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-236">Example</span></span>

```C
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a  
    unicast response). */
status =  nx_dhcp_clear_broadcast_flag(&my_dhcp, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated. */
```

## <a name="nx_dhcp_interface_clear_broadcast_flag"></a><span data-ttu-id="78432-237">nx_dhcp_interface_clear_broadcast_flag</span><span class="sxs-lookup"><span data-stu-id="78432-237">nx_dhcp_interface_clear_broadcast_flag</span></span>

<span data-ttu-id="78432-238">Belirtilen arabirimdeki yayın bayrağını ayarla veya temizle</span><span class="sxs-lookup"><span data-stu-id="78432-238">Set or clear the broadcast flag on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-239">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-239">Prototype</span></span>

```C
UINT nx_dhcp_interface_clear_broadcast_flag(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            UINT clear_flag);
```

### <a name="description"></a><span data-ttu-id="78432-240">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-240">Description</span></span>

<span data-ttu-id="78432-241">Bu hizmet, DHCP Istemci ana bilgisayar uygulamasının, DHCP Istemci iletilerindeki yayın bayrağını belirtilen arabirimdeki DHCP sunucusuna ayarlamasını veya temizlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="78432-241">This service enables the DHCP Client host application to set or clear the broadcast flag in DHCP Client messages to the DHCP Server on the specified interface.</span></span> <span data-ttu-id="78432-242">Daha fazla bilgi için bkz. **nx_dhcp_clear_broadcast_flag**</span><span class="sxs-lookup"><span data-stu-id="78432-242">For more details see **nx_dhcp_clear_broadcast_flag**</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-243">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-243">Input Parameters</span></span>

- <span data-ttu-id="78432-244">**dhcp_ptr** DHCP denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-244">**dhcp_ptr** Pointer to DHCP control block</span></span>

- <span data-ttu-id="78432-245">**interface_index** Yayın bayrağını ayarlamak için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="78432-245">**interface_index** Index of interface to set the broadcast flag</span></span>  

- <span data-ttu-id="78432-246">**clear_flag** Yayın bayrağını ayarlanacak değer</span><span class="sxs-lookup"><span data-stu-id="78432-246">**clear_flag** Value to set the broadcast flag to</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-247">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-247">Return Values</span></span>

- <span data-ttu-id="78432-248">**NX_SUCCESS** (0x00) yayın bayrağını başarıyla güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="78432-248">**NX_SUCCESS** (0x00) Successfully updated the broadcast flag</span></span>

- <span data-ttu-id="78432-249">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-249">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="78432-250">NX_PTR_ERROR (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-250">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="78432-251">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-251">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-252">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-252">Allowed From</span></span>

<span data-ttu-id="78432-253">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="78432-253">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="78432-254">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-254">Example</span></span>

```C
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a 
   unicast response) on a previously attached secondary interface. */

iface_index = 1;

status =  nx_dhcp_interface_clear_broadcast_flag(&my_dhcp, iface_index, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated. */
```

## <a name="nx_dhcp_delete"></a><span data-ttu-id="78432-255">nx_dhcp_delete</span><span class="sxs-lookup"><span data-stu-id="78432-255">nx_dhcp_delete</span></span>

<span data-ttu-id="78432-256">DHCP örneğini silme</span><span class="sxs-lookup"><span data-stu-id="78432-256">Delete a DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-257">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-257">Prototype</span></span>

```C
UINT nx_dhcp_delete(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-258">Description</span></span>

<span data-ttu-id="78432-259">Bu hizmet önceden oluşturulmuş bir DHCP örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="78432-259">This service deletes a previously created DHCP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-260">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-260">Input Parameters</span></span>

- <span data-ttu-id="78432-261">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-261">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-262">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-262">Return Values</span></span>

- <span data-ttu-id="78432-263">**NX_SUCCESS** (0x00) başarılı DHCP silme.</span><span class="sxs-lookup"><span data-stu-id="78432-263">**NX_SUCCESS** (0x00) Successful DHCP delete.</span></span>

- <span data-ttu-id="78432-264">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-264">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="78432-265">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-265">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-266">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-266">Allowed From</span></span>

<span data-ttu-id="78432-267">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-267">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-268">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-268">Example</span></span>

```C
/* Delete a DHCP instance. */
status =  nx_dhcp_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCP instance was successfully deleted. */
```

## <a name="nx_dhcp_-force_renew"></a><span data-ttu-id="78432-269">nx_dhcp_ force_renew</span><span class="sxs-lookup"><span data-stu-id="78432-269">nx_dhcp_ force_renew</span></span>

<span data-ttu-id="78432-270">Zorla yenileme iletisi gönder</span><span class="sxs-lookup"><span data-stu-id="78432-270">Send a force renew message</span></span> 

### <a name="prototype"></a><span data-ttu-id="78432-271">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-271">Prototype</span></span>

```C
UINT nx_dhcp force_renew(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-272">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-272">Description</span></span>

<span data-ttu-id="78432-273">Bu hizmet, ana bilgisayar uygulamasının DHCP için etkinleştirilen tüm arabirimlerde zorla yenileme iletisi göndermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="78432-273">This service enables the host application to send a force renew message on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="78432-274">DHCP Istemcisi, bir bağlantılı durumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="78432-274">The DHCP Client must be in a BOUND state.</span></span> <span data-ttu-id="78432-275">Bu işlev, DHCP Istemcisinin T1 zaman aşımı dolmadan önce yenilemeyi deneyecek şekilde, durumu yenıleme olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="78432-275">This function sets the state to RENEW such that the DHCP Client will try to renew before the T1 timeout expires.</span></span>

<span data-ttu-id="78432-276">Birden çok arabirim DHCP etkinken belirli bir arabirim üzerinde zorla yenileme göndermek için *nx_dhcp_interface_force_renew* kullanın.</span><span class="sxs-lookup"><span data-stu-id="78432-276">To send a force renew on a specific interface when multiple interfaces are DHCP-enabled, use *nx_dhcp_interface_force_renew*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-277">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-277">Input Parameters</span></span>

- <span data-ttu-id="78432-278">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-278">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-279">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-279">Return Values</span></span>

- <span data-ttu-id="78432-280">**NX_SUCCESS** (0x00) zorla yenilemeyi başarıyla gönderdi.</span><span class="sxs-lookup"><span data-stu-id="78432-280">**NX_SUCCESS** (0x00) Successfully sent force renew.</span></span>  

- <span data-ttu-id="78432-281">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-281">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="78432-282">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-282">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-283">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-283">Allowed From</span></span>

<span data-ttu-id="78432-284">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-284">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-285">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-285">Example</span></span>

```C
/* Send a force renew message from the Client. */
status =  nx_dhcp_force_renew(&my_dhcp);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired. */
```

## <a name="nx_dhcp_interface_force_renew"></a><span data-ttu-id="78432-286">nx_dhcp_interface_force_renew</span><span class="sxs-lookup"><span data-stu-id="78432-286">nx_dhcp_interface_force_renew</span></span>

<span data-ttu-id="78432-287">Belirtilen arabirimde zorla yenileme iletisi gönder</span><span class="sxs-lookup"><span data-stu-id="78432-287">Send a force renew message on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-288">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-288">Prototype</span></span>

```C
UINT nx_dhcp_interface_force_renew(NX_DHCP *dhcp_ptr,
                                    UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="78432-289">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-289">Description</span></span>

<span data-ttu-id="78432-290">Bu hizmet, arabirim DHCP için etkinleştirilmiş olduğu sürece, ana bilgisayar uygulamasının giriş arabiriminde zorla yenileme iletisi göndermesini sağlar (bkz. *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="78432-290">This service enables the host application to send a force renew message on the input interface as long as that interface has been enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="78432-291">Belirtilen arabirimdeki DHCP Istemcisinin bağlı durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78432-291">The DHCP Client on the specified interface must be in a BOUND state.</span></span> <span data-ttu-id="78432-292">Bu işlev, DHCP Istemcisinin T1 zaman aşımı dolmadan önce yenilemeyi deneyecek şekilde, durumu yenıleme olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="78432-292">This function sets the state to RENEW such that the DHCP Client will try to renew before the T1 timeout expires.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-293">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-293">Input Parameters</span></span>

- <span data-ttu-id="78432-294">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-294">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-295">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-295">Return Values</span></span>

- <span data-ttu-id="78432-296">**NX_SUCCESS** (0x00) zorla yenilemeyi başarıyla gönderdi.</span><span class="sxs-lookup"><span data-stu-id="78432-296">**NX_SUCCESS** (0x00) Successfully sent force renew.</span></span>  

- <span data-ttu-id="78432-297">**NX_DHCP_INTERFACE_NOT_ENABLED**  (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-297">**NX_DHCP_INTERFACE_NOT_ENABLED**  (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="78432-298">NX_PTR_ERROR (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-298">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="78432-299">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-299">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-300">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-300">Allowed From</span></span>

<span data-ttu-id="78432-301">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-301">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-302">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-302">Example</span></span>

```C
/* Send a force renew message to the server on interface 1. */
status =  nx_dhcp_interface_force_renew(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired. */
```

## <a name="nx_dhcp_packet_pool_set"></a><span data-ttu-id="78432-303">nx_dhcp_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="78432-303">nx_dhcp_packet_pool_set</span></span>

<span data-ttu-id="78432-304">DHCP Istemci paket havuzunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="78432-304">Set the DHCP Client packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-305">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-305">Prototype</span></span>

```C
UINT nx_dhcp_packet_pool_set(NX_DHCP *dhcp_ptr,
                            NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-306">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-306">Description</span></span>

<span data-ttu-id="78432-307">Bu hizmet, uygulamanın bu hizmet çağrısında daha önce oluşturulmuş bir paket havuzuna bir işaretçi geçirerek DHCP Istemci paket havuzunu oluşturmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="78432-307">This service allows the application to create the DHCP Client packet pool by passing in a pointer to a previously created packet pool in this service call.</span></span> <span data-ttu-id="78432-308">Bu özelliği kullanmak için, ana bilgisayar uygulamasının NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="78432-308">To use this feature, the host application must define NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL.</span></span> <span data-ttu-id="78432-309">Tanımlandığında, *nx_dhcp_create* hizmet istemcinin paket havuzunu oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="78432-309">When defined, the *nx_dhcp_create* service will not create the Client’s packet pool.</span></span> <span data-ttu-id="78432-310">Uygulamanın, paket havuzu oluştururken *nx_dhcp. h* içinde NX_DHCP_PACKET_PAYLOAD olarak tanımlanan DHCP istemci paket havuzu yükünün varsayılan değerlerini kullanması önerildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78432-310">Note that the application is recommended to use the default values for the DHCP client packet pool payload, defined as NX_DHCP_PACKET_PAYLOAD in *nx_dhcp.h* when creating the packet pool.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-311">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-311">Input Parameters</span></span>

- <span data-ttu-id="78432-312">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-312">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="78432-313">**packet_pool_ptr** Önceden oluşturulmuş paket havuzuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="78432-313">**packet_pool_ptr** Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-314">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-314">Return Values</span></span>

- <span data-ttu-id="78432-315">**NX_SUCCESS** (0x00) DHCP istemci paket havuzu ayarlandı</span><span class="sxs-lookup"><span data-stu-id="78432-315">**NX_SUCCESS** (0x00) DHCP Client packet pool is set</span></span>

- <span data-ttu-id="78432-316">**NX_NOT_ENABLED** (0x14) hizmeti etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-316">**NX_NOT_ENABLED** (0x14) Service is not enabled</span></span>

- <span data-ttu-id="78432-317">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-317">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="78432-318">NX_DHCP_INVALID_PAYLOAD (0x9C) yükü çok küçük</span><span class="sxs-lookup"><span data-stu-id="78432-318">NX_DHCP_INVALID_PAYLOAD (0x9C) Payload is too small</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-319">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-319">Allowed From</span></span>

<span data-ttu-id="78432-320">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="78432-320">Application code</span></span>

### <a name="example"></a><span data-ttu-id="78432-321">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-321">Example</span></span>

```C
/* Create the packet pool. */
status =  nx_packet_pool_create(&dhcp_pool, "DHCP Client Packet Pool", 
        NX_DHCP_PACKET_PAYLOAD, pointer, (15 * NX_DHCP_PACKET_PAYLOAD));

/* Create the DHCP Client. */
status =  nx_dhcp_create(&dhcp_0, &ip_0, "janetsdhcp1");

/* Set the DHCP Client packet pool. */
status =  nx_dhcp_packet_pool_set(&my_dhcp, packet_pool_ptr);
/* If status is NX_SUCCESS packet pool was successfully set. */
```

## <a name="nx_dhcp_request_client_ip"></a><span data-ttu-id="78432-322">nx_dhcp_request_client_ip</span><span class="sxs-lookup"><span data-stu-id="78432-322">nx_dhcp_request_client_ip</span></span>

<span data-ttu-id="78432-323">DHCP örneği için istenen IP adresini ayarlama</span><span class="sxs-lookup"><span data-stu-id="78432-323">Set requested IP address for DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-324">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-324">Prototype</span></span>

```C
UINT nx_dhcp_request_client_ip(NX_DHCP *dhcp_ptr,
                                ULONG client_ip_address,
                                UINT skip_discover_message);
```

### <a name="description"></a><span data-ttu-id="78432-325">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-325">Description</span></span>

<span data-ttu-id="78432-326">Bu hizmet, DHCP Istemcisinin DHCP istemci kaydında DHCP için etkinleştirilen ilk arabirimdeki DHCP sunucusundan istemesi için IP adresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="78432-326">This service sets the IP address for the DHCP Client to request from the DHCP Server on the first interface enabled for DHCP in the DHCP Client record.</span></span> <span data-ttu-id="78432-327">*Skip_discover_message* bayrağı AYARLANDıYSA, DHCP istemcisi bulma iletisini atlar ve bir istek iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="78432-327">If the *skip_discover_message* flag is set, the DHCP Client skips the Discover message and sends a Request message.</span></span>

<span data-ttu-id="78432-328">Belirli bir arabirimdeki DHCP iletileri için belirli bir IP isteği ayarlamak üzere *nx_dhcp_interface_request_client_ip* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="78432-328">To set the request for a specific IP for DHCP messages on a specific interface, use the *nx_dhcp_interface_request_client_ip* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-329">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-329">Input Parameters</span></span>

- <span data-ttu-id="78432-330">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-330">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="78432-331">**client_ip_address** DHCP sunucusundan istek yapılacak IP adresi</span><span class="sxs-lookup"><span data-stu-id="78432-331">**client_ip_address** IP address to request from DHCP server</span></span>

- <span data-ttu-id="78432-332">**skip_discover_message** Doğru ise, DHCP Istemcisi Istek iletisi gönderir</span><span class="sxs-lookup"><span data-stu-id="78432-332">**skip_discover_message** If true, DHCP Client sends Request message</span></span>  
<span data-ttu-id="78432-333">Yanlışsa, bulma iletisini gönderir.</span><span class="sxs-lookup"><span data-stu-id="78432-333">If false, it sends the Discover message.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-334">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-334">Return Values</span></span>

- <span data-ttu-id="78432-335">**NX_SUCCESS** (0x00) istenen IP adresi ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="78432-335">**NX_SUCCESS** (0x00) Requested IP address is set.</span></span>

- <span data-ttu-id="78432-336">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-336">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="78432-337">NX_PTR_ERROR (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-337">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="78432-338">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-338">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>
 
### <a name="allowed-from"></a><span data-ttu-id="78432-339">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-339">Allowed From</span></span>

<span data-ttu-id="78432-340">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-340">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-341">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-341">Example</span></span>

```C
/* Set the DHCP Client requested IP address and skip the discover message. */

status =  nx_dhcp_request_client_ip(&my_dhcp, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set. */
```

## <a name="nx_dhcp_interface_request_client_ip"></a><span data-ttu-id="78432-342">nx_dhcp_interface_request_client_ip</span><span class="sxs-lookup"><span data-stu-id="78432-342">nx_dhcp_interface_request_client_ip</span></span>

<span data-ttu-id="78432-343">Belirtilen arabirimdeki DHCP örneği için istenen IP adresini ayarla</span><span class="sxs-lookup"><span data-stu-id="78432-343">Set requested IP address for DHCP instance on specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-344">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-344">Prototype</span></span>

```C
UINT nx_dhcp_interface_request_client_ip(NX_DHCP *dhcp_ptr,
                                        UINT interface_index,
                                        ULONG client_ip_address,
                                        UINT skip_discover_message);
```

### <a name="description"></a><span data-ttu-id="78432-345">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-345">Description</span></span>

<span data-ttu-id="78432-346">Bu hizmet, DHCP Istemcisinin, belirtilen arabirimdeki DHCP sunucusundan istemesi için IP adresini ayarlar, bu arabirim DHCP için etkinleştirilmişse (bkz. *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="78432-346">This service sets the IP address for the DHCP Client to request from the DHCP Server on the specified interface, if that interface is enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="78432-347">*Skip_discover_message* bayrağı AYARLANDıYSA, DHCP istemcisi bulma iletisini atlar ve bir istek iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="78432-347">If the *skip_discover_message* flag is set, the DHCP Client skips the Discover message and sends a Request message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-348">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-348">Input Parameters</span></span>

- <span data-ttu-id="78432-349">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-349">**dhcp_ptr** Pointer to DHCP control block.</span></span>

- <span data-ttu-id="78432-350">**Interface_index** IP adresi isteği için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="78432-350">**Interface_index** Index of interface to request IP address on</span></span>

- <span data-ttu-id="78432-351">**client_ip_address** DHCP sunucusundan istek yapılacak IP adresi</span><span class="sxs-lookup"><span data-stu-id="78432-351">**client_ip_address** IP address to request from DHCP server</span></span>

- <span data-ttu-id="78432-352">**skip_discover_message** Doğru ise, DHCP Istemcisi Istek iletisi gönderir; diğer bir deyişle, bulma iletisini gönderir.</span><span class="sxs-lookup"><span data-stu-id="78432-352">**skip_discover_message** If true, DHCP Client sends Request message; else it sends the Discover message.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-353">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-353">Return Values</span></span>

- <span data-ttu-id="78432-354">**NX_SUCCESS** (0x00) istenen IP adresi ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="78432-354">**NX_SUCCESS** (0x00) Requested IP address is set.</span></span>

- <span data-ttu-id="78432-355">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-355">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="78432-356">NX_PTR_ERROR (0x16) geçersiz IP veya DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-356">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="78432-357">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-357">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>


### <a name="allowed-from"></a><span data-ttu-id="78432-358">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-358">Allowed From</span></span>

<span data-ttu-id="78432-359">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-359">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-360">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-360">Example</span></span>

```C
/* Set the DHCP Client requested IP address and skip the discover message on  
   interface 0. */
status =  nx_dhcp_interface_request_client_ip(&my_dhcp, 0, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set. */
```

## <a name="nx_dhcp_reinitialize"></a><span data-ttu-id="78432-361">nx_dhcp_reinitialize</span><span class="sxs-lookup"><span data-stu-id="78432-361">nx_dhcp_reinitialize</span></span>

<span data-ttu-id="78432-362">DHCP istemci ağı parametrelerini Temizleme</span><span class="sxs-lookup"><span data-stu-id="78432-362">Clear the DHCP client network parameters</span></span> 

### <a name="prototype"></a><span data-ttu-id="78432-363">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-363">Prototype</span></span>

```C
UINT nx_dhcp_reinitialize(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-364">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-364">Description</span></span>

<span data-ttu-id="78432-365">Bu hizmet, ana bilgisayar uygulama ağ parametrelerini (IP adresi, ağ adresi ve ağ maskesi) temizler ve DHCP için etkinleştirilen tüm arabirimlerde DHCP Istemci durumunu temizler.</span><span class="sxs-lookup"><span data-stu-id="78432-365">This service clears the host application network parameters (IP address, network address and network mask), and clears the DHCP Client state on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="78432-366">*Nx_dhcp_stop* ile birlikte KULLANıLıR ve DHCP durum makinesine ' yeniden Başlat ' için *nx_dhcp_start* :</span><span class="sxs-lookup"><span data-stu-id="78432-366">It is used in combination with *nx_dhcp_stop* and *nx_dhcp_start* to ‘restart’ the DHCP state machine:</span></span> 

<span data-ttu-id="78432-367">nx_dhcp_stop (&my_dhcp);</span><span class="sxs-lookup"><span data-stu-id="78432-367">nx_dhcp_stop(&my_dhcp);</span></span>  
<span data-ttu-id="78432-368">nx_dhcp_reinitialize (&my_dhcp);</span><span class="sxs-lookup"><span data-stu-id="78432-368">nx_dhcp_reinitialize(&my_dhcp);</span></span>  
<span data-ttu-id="78432-369">nx_dhcp_start (&my_dhcp);</span><span class="sxs-lookup"><span data-stu-id="78432-369">nx_dhcp_start(&my_dhcp);</span></span>


<span data-ttu-id="78432-370">DHCP için birden fazla arabirim etkinleştirildiğinde belirli bir arabirimdeki DHCP Istemcisini yeniden başlatmak için *nx_dhcp_interface_reinitialize* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="78432-370">To reinitialize the DHCP Client on a specific interface when multiple interfaces are enabled for DHCP, use the *nx_dhcp_interface_reinitialize* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-371">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-371">Input Parameters</span></span>

- <span data-ttu-id="78432-372">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-372">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-373">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-373">Return Values</span></span>

- <span data-ttu-id="78432-374">**NX_SUCCESS** (0x00) DHCP başarıyla yeniden başlatıldı</span><span class="sxs-lookup"><span data-stu-id="78432-374">**NX_SUCCESS** (0x00) DHCP successfully reinitialized</span></span> 

- <span data-ttu-id="78432-375">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-375">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-376">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-376">Allowed From</span></span>

<span data-ttu-id="78432-377">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-377">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-378">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-378">Example</span></span>

```C
/* Reinitialize the previously started DHCP client. */
status =  nx_dhcp_reinitialize(&my_dhcp);

/* If status is NX_SUCCESS the host application successfully reinitialized its 
network parameters and DHCP client state. */
```

## <a name="nx_dhcp_interface_reinitialize"></a><span data-ttu-id="78432-379">nx_dhcp_interface_reinitialize</span><span class="sxs-lookup"><span data-stu-id="78432-379">nx_dhcp_interface_reinitialize</span></span>

<span data-ttu-id="78432-380">Belirtilen arabirimdeki DHCP istemci ağ parametrelerini temizle</span><span class="sxs-lookup"><span data-stu-id="78432-380">Clear the DHCP client network parameters on the specified interface</span></span> 

### <a name="prototype"></a><span data-ttu-id="78432-381">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-381">Prototype</span></span>

```C
UINT nx_dhcp_interface_reinitialize(NX_DHCP *dhcp_ptr,
                                    UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="78432-382">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-382">Description</span></span>

<span data-ttu-id="78432-383">Bu hizmet, bu arabirim DHCP için etkinleştirilmişse belirtilen arabirimdeki ağ parametrelerini (IP adresi, ağ adresi ve ağ maskesi) temizler (bkz. *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="78432-383">This service clears the network parameters (IP address, network address and network mask) on the specified interface if that interface is enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="78432-384">Daha fazla bilgi için bkz. *nx_dhcp_reinitialize* .</span><span class="sxs-lookup"><span data-stu-id="78432-384">See *nx_dhcp_reinitialize* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-385">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-385">Input Parameters</span></span>

- <span data-ttu-id="78432-386">**dhcp_ptr** Önceden oluşturulmuş DHCP örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="78432-386">**dhcp_ptr** Pointer to previously created DHCP instance</span></span>

- <span data-ttu-id="78432-387">**interface_index** Yeniden başlatmak için arabirim dizini.</span><span class="sxs-lookup"><span data-stu-id="78432-387">**interface_index** Index of interface to reinitialize.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-388">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-388">Return Values</span></span>

- <span data-ttu-id="78432-389">**NX_SUCCESS** (0x00) arabirimi başarıyla yeniden başlatıldı</span><span class="sxs-lookup"><span data-stu-id="78432-389">**NX_SUCCESS** (0x00) Interface successfully reinitialized</span></span>

- <span data-ttu-id="78432-390">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-390">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="78432-391">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-391">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="78432-392">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-392">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="78432-393">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-393">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-394">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-394">Allowed From</span></span>

<span data-ttu-id="78432-395">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-395">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-396">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-396">Example</span></span>

```C
/* Reinitialize the previously started DHCP client on interface 1. */
status =  nx_dhcp_interface_reinitialize(&my_dhcp, 1);

/* If status is NX_SUCCESS the host application successfully reinitialized its 
network parameters and DHCP client state. */
```

## <a name="nx_dhcp_release"></a><span data-ttu-id="78432-397">nx_dhcp_release</span><span class="sxs-lookup"><span data-stu-id="78432-397">nx_dhcp_release</span></span>

<span data-ttu-id="78432-398">Yayın kiralanan IP adresi</span><span class="sxs-lookup"><span data-stu-id="78432-398">Release Leased IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-399">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-399">Prototype</span></span>

```C
UINT nx_dhcp_release(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-400">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-400">Description</span></span>

<span data-ttu-id="78432-401">Bu hizmet, bir DHCP sunucusundan alınan IP adresini, yayın iletisini bu sunucuya göndererek yayınlar.</span><span class="sxs-lookup"><span data-stu-id="78432-401">This service releases the IP address obtained from a DHCP server by sending the RELEASE message to that server.</span></span> <span data-ttu-id="78432-402">Daha sonra DHCP Istemcisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="78432-402">It then reinitializes the DHCP Client.</span></span> <span data-ttu-id="78432-403">Bu hizmet, DHCP için etkinleştirilen tüm arabirimlere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="78432-403">This service is applied to all interfaces enabled for DHCP.</span></span>

<span data-ttu-id="78432-404">Uygulama, *nx_dhcp_start* çağırarak DHCP istemcisini yeniden başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="78432-404">The application can restart the DHCP Client by calling *nx_dhcp_start*.</span></span>

<span data-ttu-id="78432-405">Bir adresi belirli bir arabirimdeki DHCP sunucusuna geri yüklemek için *nx_dhcp_interface_release* hizmetini kullanın</span><span class="sxs-lookup"><span data-stu-id="78432-405">To release an address back to the DHCP server on a specific interface, use the *nx_dhcp_interface_release* service</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-406">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-406">Input Parameters</span></span>

- <span data-ttu-id="78432-407">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-407">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-408">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-408">Return Values</span></span>

- <span data-ttu-id="78432-409">**NX_SUCCESS** (0x00) başarılı bir DHCP sürümü.</span><span class="sxs-lookup"><span data-stu-id="78432-409">**NX_SUCCESS** (0x00) Successful DHCP release.</span></span>  

- <span data-ttu-id="78432-410">**NX_DHCP_NOT_BOUND** (0x94) IP adresi kiralamadı, bu nedenle serbest bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="78432-410">**NX_DHCP_NOT_BOUND** (0x94) The IP address has not been leased so it can’t be released.</span></span>

- <span data-ttu-id="78432-411">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-411">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="78432-412">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-412">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-413">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-413">Allowed From</span></span>

<span data-ttu-id="78432-414">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-414">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-415">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-415">Example</span></span>

```C
/* Release the previously leased IP address. */
status =  nx_dhcp_release(&my_dhcp);

/* If status is NX_SUCCESS the previous IP lease was successfully released. */
```

## <a name="nx_dhcp_interface_release"></a><span data-ttu-id="78432-416">nx_dhcp_interface_release</span><span class="sxs-lookup"><span data-stu-id="78432-416">nx_dhcp_interface_release</span></span>

<span data-ttu-id="78432-417">Belirtilen arabirimdeki IP adresini serbest bırak</span><span class="sxs-lookup"><span data-stu-id="78432-417">Release IP address on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-418">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-418">Prototype</span></span>

```C
UINT nx_dhcp_interface_release(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="78432-419">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-419">Description</span></span>

<span data-ttu-id="78432-420">Bu hizmet, belirtilen arabirimdeki bir DHCP sunucusundan alınan IP adresini serbest bırakır ve DHCP Istemcisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="78432-420">This service releases the IP address obtained from a DHCP server on the specified interface and reinitializes the DHCP Client.</span></span> <span data-ttu-id="78432-421">DHCP Istemcisi, *nx_dhcp_start* çağırarak yeniden başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="78432-421">The DHCP Client can be restarted by calling *nx_dhcp_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-422">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-422">Input Parameters</span></span>

- <span data-ttu-id="78432-423">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-423">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-424">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-424">Return Values</span></span>

- <span data-ttu-id="78432-425">**NX_SUCCESS** (0x00) başarılı bir DHCP sürümü.</span><span class="sxs-lookup"><span data-stu-id="78432-425">**NX_SUCCESS** (0x00) Successful DHCP release.</span></span>

- <span data-ttu-id="78432-426">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-426">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="78432-427">**NX_DHCP_NOT_BOUND** (0x94) IP adresi kiralamadı, bu nedenle serbest bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="78432-427">**NX_DHCP_NOT_BOUND** (0x94) The IP address has not been leased so it can’t be released.</span></span>

- <span data-ttu-id="78432-428">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-428">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="78432-429">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-429">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="78432-430">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-430">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-431">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-431">Allowed From</span></span>

<span data-ttu-id="78432-432">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-432">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-433">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-433">Example</span></span>

```C
/* Release the previously leased IP address on interface 1. */
status =  nx_dhcp_interface_release(&my_dhcp, 1);

/* If status is NX_SUCCESS the previous IP lease was successfully released. */
```

## <a name="nx_dhcp_decline"></a><span data-ttu-id="78432-434">nx_dhcp_decline</span><span class="sxs-lookup"><span data-stu-id="78432-434">nx_dhcp_decline</span></span>

<span data-ttu-id="78432-435">DHCP sunucusundan IP adresini Reddet</span><span class="sxs-lookup"><span data-stu-id="78432-435">Decline IP address from DHCP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-436">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-436">Prototype</span></span>

```C
UINT nx_dhcp_decline(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-437">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-437">Description</span></span>

<span data-ttu-id="78432-438">Bu hizmet, DHCP için etkinleştirilen tüm arabirimlerde DHCP sunucusundan kiralanmış bir IP adresini reddeder.</span><span class="sxs-lookup"><span data-stu-id="78432-438">This service declines an IP address leased from the DHCP server on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="78432-439">NX_DHCP_CLIENT_ SEND_ ARP_PROBE tanımlanmışsa, DHCP Istemcisi IP adresinin zaten kullanımda olduğunu algılarsa bir reddetme iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="78432-439">If NX_DHCP_CLIENT_ SEND_ ARP_PROBE is defined, the DHCP Client will send a DECLINE message if it detects that the IP address is already in use.</span></span> <span data-ttu-id="78432-440">NetX DHCP Istemcisinde ARP araştırma yapılandırması hakkında daha fazla bilgi için bkz. bölüm içinde **ARP araştırmaları** .</span><span class="sxs-lookup"><span data-stu-id="78432-440">See **ARP Probes** in Chapter One for more information on ARP probe configuration in the NetX DHCP Client.</span></span>

<span data-ttu-id="78432-441">Uygulama, adresin başka yollarla kullanımda olduğunu tespit etmezse IP adresini reddetmek için bu hizmeti kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="78432-441">The application can use this service to decline its IP address if it discovers the address is in use by other means.</span></span>

<span data-ttu-id="78432-442">Bu hizmet, DHCP Istemcisini *nx_dhcp_start* çağırarak yeniden başlatılacak şekilde yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="78432-442">This service reinitializes the DHCP Client to that it can be restarted by calling *nx_dhcp_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-443">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-443">Input Parameters</span></span>

- <span data-ttu-id="78432-444">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-444">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-445">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-445">Return Values</span></span>

- <span data-ttu-id="78432-446">**NX_SUCCESS** (0x00) reddetme başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="78432-446">**NX_SUCCESS** (0x00) Decline successfully sent</span></span>  

- <span data-ttu-id="78432-447">**NX_DHCP_NOT_STARTED** (0x96) DHCP örneği başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="78432-447">**NX_DHCP_NOT_STARTED** (0x96) The DHCP instance not started</span></span>

- <span data-ttu-id="78432-448">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-448">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="78432-449">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="78432-449">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-450">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-450">Allowed From</span></span>

<span data-ttu-id="78432-451">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-451">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-452">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-452">Example</span></span>

```C
/* Decline the IP address offered by the DHCP server. */
status =  nx_dhcp_decline(&my_dhcp);

/* If status is NX_SUCCESS the previous IP address decline message was 
   successfully trasnmitted. */
```

## <a name="nx_dhcp_interface_decline"></a><span data-ttu-id="78432-453">nx_dhcp_interface_decline</span><span class="sxs-lookup"><span data-stu-id="78432-453">nx_dhcp_interface_decline</span></span>

<span data-ttu-id="78432-454">Belirtilen arabirimdeki DHCP sunucusundan IP adresini Reddet</span><span class="sxs-lookup"><span data-stu-id="78432-454">Decline IP address from DHCP Server on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-455">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-455">Prototype</span></span>

```C
UINT nx_dhcp_interface_decline(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="78432-456">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-456">Description</span></span>

<span data-ttu-id="78432-457">Bu hizmet, DHCP sunucusu tarafından atanan bir IP adresini reddetmek için reddetme iletisini sunucuya gönderir.</span><span class="sxs-lookup"><span data-stu-id="78432-457">This service sends the DECLINE message to the server to decline an IP address assigned by the DHCP server.</span></span> <span data-ttu-id="78432-458">Ayrıca, DHCP Istemcisini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="78432-458">It also reinitializes the DHCP Client.</span></span> <span data-ttu-id="78432-459">Daha fazla bilgi için bkz. *nx_dhcp_decline* .</span><span class="sxs-lookup"><span data-stu-id="78432-459">See *nx_dhcp_decline* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-460">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-460">Input Parameters</span></span>

- <span data-ttu-id="78432-461">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-461">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="78432-462">**Interface_index** IP adresini reddetme arabiriminin dizini</span><span class="sxs-lookup"><span data-stu-id="78432-462">**Interface_index** Index of interface to decline IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-463">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-463">Return Values</span></span>

- <span data-ttu-id="78432-464">**NX_SUCCESS** (0x00) DHCP reddetme iletisi gönderildi</span><span class="sxs-lookup"><span data-stu-id="78432-464">**NX_SUCCESS** (0x00) DHCP decline message sent</span></span>  

- <span data-ttu-id="78432-465">**NX_DHCP_NOT_BOUND** (0x94) DHCP istemcisi bağlanmadı</span><span class="sxs-lookup"><span data-stu-id="78432-465">**NX_DHCP_NOT_BOUND** (0x94) DHCP Client not bound</span></span>

- <span data-ttu-id="78432-466">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-466">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="78432-467">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-467">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="78432-468">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-468">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="78432-469">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-469">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-470">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-470">Allowed From</span></span>

<span data-ttu-id="78432-471">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-471">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-472">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-472">Example</span></span>
```C
/* Decline the IP address offered by the DHCP server on interface 2. */
status =  nx_dhcp_interface_decline(&my_dhcp, 2);

/* If status is NX_SUCCESS the previous IP address decline message was
   successfully trasnmitted. */
```

## <a name="nx_dhcp_send_request"></a><span data-ttu-id="78432-473">nx_dhcp_send_request</span><span class="sxs-lookup"><span data-stu-id="78432-473">nx_dhcp_send_request</span></span>

<span data-ttu-id="78432-474">DHCP iletisini sunucuya gönder</span><span class="sxs-lookup"><span data-stu-id="78432-474">Send DHCP message to Server</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-475">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-475">Prototype</span></span>

```C
UINT nx_dhcp_send_request(NX_DHCP *dhcp_ptr, UINT dhcp_message_type);
```

### <a name="description"></a><span data-ttu-id="78432-476">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-476">Description</span></span>

<span data-ttu-id="78432-477">Bu hizmet, belirtilen DHCP iletisini DHCP Istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="78432-477">This service sends the specified DHCP message to the DHCP server on the first interface enabled for DHCP found in the DHCP Client record.</span></span> <span data-ttu-id="78432-478">Bir yayın veya reddetme iletisi göndermek için, uygulamanın sırasıyla *nx_dhcp [_interface] _Release*() veya *nx_dhcp_interface_decline ()* hizmetlerini kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78432-478">To send a RELEASE or DECLINE message, the application must use the *nx_dhcp[_interface]_release*() or *nx_dhcp_interface_decline()* services respectively.</span></span>

<span data-ttu-id="78432-479">Bu hizmeti kullanmak için, DHCP Istemcisinin INFORM_REQUEST ileti türünü gönderme haricinde başlatılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78432-479">The DHCP Client must be started to use this service except for sending the INFORM_REQUEST message type.</span></span>

> [!NOTE] 
> <span data-ttu-id="78432-480">Bu hizmet, ana bilgisayar uygulamasının DHCP Istemci durumu makinesine ' Drive ' için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="78432-480">This service is not intended for the host application to ‘drive’ the DHCP Client state machine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-481">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-481">Input Parameters</span></span>

- <span data-ttu-id="78432-482">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-482">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="78432-483">**dhcp_message_type** İleti isteği ( *nx_dhcp. h* içinde tanımlanmıştır)</span><span class="sxs-lookup"><span data-stu-id="78432-483">**dhcp_message_type** Message request (defined in *nx_dhcp.h*)</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-484">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-484">Return Values</span></span>

- <span data-ttu-id="78432-485">**NX_SUCCESS** (0x00) DHCP iletisi gönderildi</span><span class="sxs-lookup"><span data-stu-id="78432-485">**NX_SUCCESS** (0x00) DHCP message sent</span></span>  

- <span data-ttu-id="78432-486">**NX_DHCP_NOT_STARTED** (0x96) geçersiz arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="78432-486">**NX_DHCP_NOT_STARTED** (0x96) Invalid interface index</span></span>

- <span data-ttu-id="78432-487">**NX_DHCP_INVALID_MESSAGE** (0x9b) göndermek için geçersiz ileti türü</span><span class="sxs-lookup"><span data-stu-id="78432-487">**NX_DHCP_INVALID_MESSAGE** (0x9B) Invalid message type to send</span></span>

- <span data-ttu-id="78432-488">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="78432-488">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-489">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-489">Allowed From</span></span>

<span data-ttu-id="78432-490">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-490">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-491">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-491">Example</span></span>

```C
/* Send the DHCP INFORM REQUEST message to the server. */

status =  nx_dhcp_send_request(&my_dhcp, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent. */
```

## <a name="nx_dhcp_interface_send_request"></a><span data-ttu-id="78432-492">nx_dhcp_interface_send_request</span><span class="sxs-lookup"><span data-stu-id="78432-492">nx_dhcp_interface_send_request</span></span>

<span data-ttu-id="78432-493">Belirli bir arabirimdeki DHCP iletisini sunucuya gönder</span><span class="sxs-lookup"><span data-stu-id="78432-493">Send DHCP message to Server on a specific interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-494">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-494">Prototype</span></span>

```C
UINT nx_dhcp_interface_send_request(NX_DHCP *dhcp_ptr,
                                    UINT interface_index,
                                    UINT dhcp_message_type);
```

### <a name="description"></a><span data-ttu-id="78432-495">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-495">Description</span></span>

<span data-ttu-id="78432-496">Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirimdeki DHCP sunucusuna bir ileti gönderir.</span><span class="sxs-lookup"><span data-stu-id="78432-496">This service sends a message to the DHCP server on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="78432-497">Bir yayın veya reddetme iletisi göndermek için, uygulamanın sırasıyla *nx_dhcp [_interface] _Release*() veya *nx_dhcp_interface_decline ()* hizmetlerini kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78432-497">To send a RELEASE or DECLINE message, the application must use the *nx_dhcp[_interface]_release*() or *nx_dhcp_interface_decline()* services respectively.</span></span>

<span data-ttu-id="78432-498">DHCP Istemcisi, DHCP BILDIR Istek iletisi türünü göndermek dışında bu hizmeti kullanacak şekilde başlatılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="78432-498">The DHCP Client must be started to use this service except for sending the DHCP INFORM REQUEST message type.</span></span>

<span data-ttu-id="78432-499">Bu hizmet, ana bilgisayar uygulamasının DHCP Istemci durumu makinesine ' Drive ' için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="78432-499">This service is not intended for the host application to ‘drive’ the DHCP Client state machine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-500">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-500">Input Parameters</span></span>

- <span data-ttu-id="78432-501">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-501">**dhcp_ptr** Pointer to DHCP control block.</span></span>

- <span data-ttu-id="78432-502">**Interface_index** İletinin gönderileceği arabirimin dizini</span><span class="sxs-lookup"><span data-stu-id="78432-502">**Interface_index** Index of interface to send message on</span></span>  

- <span data-ttu-id="78432-503">**dhcp_message_type** İleti isteği ( *nx_dhcp. h* içinde tanımlanmıştır)</span><span class="sxs-lookup"><span data-stu-id="78432-503">**dhcp_message_type** Message request (defined in *nx_dhcp.h*)</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-504">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-504">Return Values</span></span>

- <span data-ttu-id="78432-505">**NX_SUCCESS** (0x00) DHCP iletisi gönderildi</span><span class="sxs-lookup"><span data-stu-id="78432-505">**NX_SUCCESS** (0x00) DHCP message sent</span></span>  

- <span data-ttu-id="78432-506">**NX_DHCP_NOT_STARTED** (0x96) geçersiz arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="78432-506">**NX_DHCP_NOT_STARTED** (0x96) Invalid interface index</span></span>

- <span data-ttu-id="78432-507">**NX_DHCP_INVALID_MESSAGE** (0x9b) göndermek için geçersiz ileti türü</span><span class="sxs-lookup"><span data-stu-id="78432-507">**NX_DHCP_INVALID_MESSAGE** (0x9B) Invalid message type to send</span></span>

- <span data-ttu-id="78432-508">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) arabirimi DHCP için etkin değil</span><span class="sxs-lookup"><span data-stu-id="78432-508">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="78432-509">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-509">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="78432-510">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-510">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="78432-511">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-511">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-512">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-512">Allowed From</span></span>

<span data-ttu-id="78432-513">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-513">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-514">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-514">Example</span></span>

```C
/* Send the INFORM REQUEST message to the server on the primary interface. */

status =  nx_dhcp_interface_send_request(&my_dhcp, 0, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent. */
```

## <a name="nx_dhcp_server_address_get"></a><span data-ttu-id="78432-515">nx_dhcp_server_address_get</span><span class="sxs-lookup"><span data-stu-id="78432-515">nx_dhcp_server_address_get</span></span>

<span data-ttu-id="78432-516">DHCP Istemcisinin DHCP sunucusu IP adresini al</span><span class="sxs-lookup"><span data-stu-id="78432-516">Get the DHCP Client’s DHCP server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-517">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-517">Prototype</span></span>

```C
UINT nx_dhcp_server_address_get(NX_DHCP *dhcp_ptr,
                                ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="78432-518">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-518">Description</span></span>

<span data-ttu-id="78432-519">Bu hizmet DHCP istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP Istemci DHCP sunucusu IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="78432-519">This service retrieves the DHCP Client DHCP server IP address on the first interface enabled for DHCP found in the DHCP Client record.</span></span> <span data-ttu-id="78432-520">Çağıran bu hizmeti yalnızca DHCP Istemcisi DHCP sunucusu tarafından atanan bir IP adresine bağlandıktan sonra kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="78432-520">The caller can only use this service after the DHCP Client is bound to an IP address assigned by the DHCP Server.</span></span> <span data-ttu-id="78432-521">Ana bilgisayar uygulaması, IP adresinin ayarlandığını doğrulamak için *nx_ip_status_check* hizmetini kullanabilir veya *NX_DHCP_STATE_CHANGE_NOTIFY* kullanabilir ve DHCP istemci durumunun NX_DHCP_STATE_BOUND olduğunu sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="78432-521">The host application can use the *nx_ip_status_check* service to verify IP address is set, or it can use the *nx_dhcp_state_change_notify* and query the DHCP Client state is NX_DHCP_STATE_BOUND.</span></span> <span data-ttu-id="78432-522">Durum değişikliği geri arama işlevini ayarlama hakkında daha fazla ayrıntı için bkz. *nx_dhcp_state_change_notify* .</span><span class="sxs-lookup"><span data-stu-id="78432-522">See *nx_dhcp_state_change_notify* for more details about setting the state change callback function.</span></span>

<span data-ttu-id="78432-523">DHCP Istemcisi için birden çok arabirim etkinleştirildiğinde, belirli bir arabirimdeki DHCP sunucusunu bulmak için *nx_dhcp_interface_server_address_get* hizmetini kullanın</span><span class="sxs-lookup"><span data-stu-id="78432-523">To find the DHCP server on a specific interface when multiple interfaces are enabled for DHCP Client, use the *nx_dhcp_interface_server_address_get* service</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-524">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-524">Input Parameters</span></span>

- <span data-ttu-id="78432-525">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-525">**dhcp_ptr** Pointer to DHCP control block.</span></span>

- <span data-ttu-id="78432-526">**server_address** Sunucu IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-526">**server_address** Pointer to server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-527">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-527">Return Values</span></span>

- <span data-ttu-id="78432-528">**NX_SUCCESS** (0x00) DHCP sunucusu adresi döndürüldü</span><span class="sxs-lookup"><span data-stu-id="78432-528">**NX_SUCCESS** (0x00) DHCP server address returned</span></span>

- <span data-ttu-id="78432-529">NX_PTR_ERROR (0x16) geçersiz giriş işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-529">NX_PTR_ERROR (0x16) Invalid input pointer</span></span>

- <span data-ttu-id="78432-530">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-530">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-531">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-531">Allowed From</span></span>

<span data-ttu-id="78432-532">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-532">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-533">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-533">Example</span></span>

```C
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. 
/* void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter. */
    state_changes++;

    if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
    {
            status = nx_dhcp_server_address_get(&dhcp_0, &server_address);
    }
```

## <a name="nx_dhcp_interface_server_address_get"></a><span data-ttu-id="78432-534">nx_dhcp_interface_server_address_get</span><span class="sxs-lookup"><span data-stu-id="78432-534">nx_dhcp_interface_server_address_get</span></span>

<span data-ttu-id="78432-535">Belirtilen arabirimdeki DHCP Istemcisinin DHCP sunucusu IP adresini al</span><span class="sxs-lookup"><span data-stu-id="78432-535">Get the DHCP Client’s DHCP server IP address on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-536">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-536">Prototype</span></span>

```C
UINT nx_dhcp_interface_server_address_get(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="78432-537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-537">Description</span></span>

<span data-ttu-id="78432-538">Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirimdeki DHCP Istemci DHCP sunucusu IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="78432-538">This service retrieves the DHCP Client DHCP server IP address on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="78432-539">DHCP Istemcisi, bağlantılı durumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="78432-539">The DHCP Client must be in the Bound state.</span></span> <span data-ttu-id="78432-540">Bu arabirimdeki DHCP Istemcisini başlattıktan sonra konak uygulama, IP adresinin ayarlandığını doğrulamak için *nx_ip_status_check* hizmetini kullanabilir ya da DHCP istemci durumu değişikliği geri aramasını KULLANABILIR ve DHCP istemci durumunun NX_DHCP_STATE_BOUND.</span><span class="sxs-lookup"><span data-stu-id="78432-540">After starting the DHCP Client on that interface, the host application can either use the *nx_ip_status_check* service to verify the IP address is set, or it can use the DHCP Client state change callback and query the DHCP Client state is NX_DHCP_STATE_BOUND.</span></span> <span data-ttu-id="78432-541">Durum değişikliği geri arama işlevini ayarlama hakkında daha fazla ayrıntı için bkz. *nx_dhcp_state_change_notify* .</span><span class="sxs-lookup"><span data-stu-id="78432-541">See *nx_dhcp_state_change_notify* for more details about setting the state change callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-542">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-542">Input Parameters</span></span>

- <span data-ttu-id="78432-543">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-543">**dhcp_ptr** Pointer to DHCP control block.</span></span>

- <span data-ttu-id="78432-544">**Interface_index** IP adresi almak için arabirim dizini</span><span class="sxs-lookup"><span data-stu-id="78432-544">**Interface_index** Index of interface to obtain IP address</span></span>  

- <span data-ttu-id="78432-545">**server_address** Sunucu IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-545">**server_address** Pointer to server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-546">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-546">Return Values</span></span>

- <span data-ttu-id="78432-547">**NX_SUCCESS** (0x00) DHCP sunucusu adresi döndürüldü</span><span class="sxs-lookup"><span data-stu-id="78432-547">**NX_SUCCESS** (0x00) DHCP server address returned</span></span>

- <span data-ttu-id="78432-548">**NX_DHCP_NO_INTERFACES_ENABLED** (0xa5) DHCP için etkinleştirilen arabirim yok</span><span class="sxs-lookup"><span data-stu-id="78432-548">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces enabled for DHCP</span></span>

- <span data-ttu-id="78432-549">**NX_DHCP_NOT_BOUND** (0x94) DHCP istemcisi bağlanmadı</span><span class="sxs-lookup"><span data-stu-id="78432-549">**NX_DHCP_NOT_BOUND** (0x94) DHCP Client not bound</span></span>

- <span data-ttu-id="78432-550">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-550">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="78432-551">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-551">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="78432-552">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-552">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-553">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-553">Allowed From</span></span>

<span data-ttu-id="78432-554">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-554">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-555">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-555">Example</span></span>

```C
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. 
/* void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter. */
    state_changes++;

    /* Get the DHCP server IP address on interface 1 */
    if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
    {
            status = nx_dhcp_interface_server_address_get(&dhcp_0, 1, 
                                                    &server_address);
    }
```

## <a name="nx_dhcp_set_interface_index"></a><span data-ttu-id="78432-556">nx_dhcp_set_interface_index</span><span class="sxs-lookup"><span data-stu-id="78432-556">nx_dhcp_set_interface_index</span></span>

<span data-ttu-id="78432-557">DHCP örneği için ağ arabirimini ayarla</span><span class="sxs-lookup"><span data-stu-id="78432-557">Set network interface for DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-558">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-558">Prototype</span></span>

```C
UINT nx_dhcp_set_interface_index(NX_DHCP *dhcp_ptr, UINT index);
```

### <a name="description"></a><span data-ttu-id="78432-559">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-559">Description</span></span>

<span data-ttu-id="78432-560">Bu hizmet, DHCP örneği için ağ arabirimini, tek bir ağ arabirimi için yapılandırılmış DHCP Istemcisini çalıştırırken üzerinde DHCP sunucusuna bağlanacak şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="78432-560">This service sets the network interface for the DHCP instance to connect to the DHCP Server on when running DHCP Client configured for a single network interface.</span></span>

<span data-ttu-id="78432-561">Varsayılan olarak, DHCP Istemcisi birincil arabirimde çalışır.</span><span class="sxs-lookup"><span data-stu-id="78432-561">By default the DHCP Client runs on the primary interface.</span></span> <span data-ttu-id="78432-562">İkincil bir hizmette DHCP çalıştırmak için bu hizmeti kullanarak ikincil arabirimi DHCP Istemci arabirimi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78432-562">To run DHCP on a secondary service, use this service to set the secondary interface as the DHCP Client interface.</span></span> <span data-ttu-id="78432-563">Uygulamanın, *nx_ip_interface_attach* hizmetini kullanarak BELIRTILEN arabirimi IP örneğine daha önce kaydetmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="78432-563">The application must previously register the specified interface to the IP instance using the *nx_ip_interface_attach* service.</span></span>

<span data-ttu-id="78432-564">Bu hizmetin DHCP Istemcisini yalnızca bir arabirimde çalıştırmayı sağlayan uygulamalar için tasarlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78432-564">Note that this service is intended for applications that intend to run the DHCP Client on only one interface.</span></span> <span data-ttu-id="78432-565">Birden çok arabirimde DHCP çalıştırmak için daha fazla ayrıntı için *nx_dhcp_interface_enable* bakın.</span><span class="sxs-lookup"><span data-stu-id="78432-565">To run DHCP on multiple interfaces see *nx_dhcp_interface_enable* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-566">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-566">Input Parameters</span></span>

- <span data-ttu-id="78432-567">**dhcp_ptr** DHCP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-567">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="78432-568">**Dizin** Cihaz ağ arabiriminin dizini</span><span class="sxs-lookup"><span data-stu-id="78432-568">**index** Index of device network interface</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-569">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-569">Return Values</span></span>

- <span data-ttu-id="78432-570">**NX_SUCCESS** (0x00) arabirimi başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="78432-570">**NX_SUCCESS** (0x00) Interface is successfully set.</span></span>

- <span data-ttu-id="78432-571">**NX_INVALID_INTERFACE** (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-571">**NX_INVALID_INTERFACE** (0x4C) Invalid network interface</span></span>

- <span data-ttu-id="78432-572">DHCP için **NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) arabirimi etkinleştirildi</span><span class="sxs-lookup"><span data-stu-id="78432-572">**NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) Interface enabled for DHCP</span></span>

- <span data-ttu-id="78432-573">**NX_DHCP_NO_RECORDS_AVAILABLE** (0xa7) başka bir kayıt yok</span><span class="sxs-lookup"><span data-stu-id="78432-573">**NX_DHCP_NO_RECORDS_AVAILABLE** (0xA7) No record available for another</span></span>

- <span data-ttu-id="78432-574">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-574">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-575">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-575">Allowed From</span></span>

<span data-ttu-id="78432-576">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-576">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-577">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-577">Example</span></span>

```C
/* Set the DHCP Client interface to the secondary interface (index 1). */
status =  nx_dhcp_set_interface_index(&my_dhcp, 1);
/* If status is NX_SUCCESS a DHCP interface was successfully set. */
```

## <a name="nx_dhcp_start"></a><span data-ttu-id="78432-578">nx_dhcp_start</span><span class="sxs-lookup"><span data-stu-id="78432-578">nx_dhcp_start</span></span>

<span data-ttu-id="78432-579">DHCP işlemesini Başlat</span><span class="sxs-lookup"><span data-stu-id="78432-579">Start DHCP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-580">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-580">Prototype</span></span>

```C
UINT nx_dhcp_start(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-581">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-581">Description</span></span>

<span data-ttu-id="78432-582">Bu hizmet DHCP için etkinleştirilen tüm arabirimlerde DHCP işlemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="78432-582">This service starts DHCP processing on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="78432-583">Varsayılan olarak, uygulama nx_dhcp_create çağırdığında, birincil arabirim DHCP için etkinleştirilir *.*</span><span class="sxs-lookup"><span data-stu-id="78432-583">By default the primary interface is enabled for DHCP when the application calls *nx_dhcp_create.*</span></span>

<span data-ttu-id="78432-584">IP örneğinin DHCP Istemci arabirimindeki bir IP adresine bağlı olduğunu doğrulamak için *nx_ip_status_check* kullanarak IP adresinin geçerli olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="78432-584">To verify when the IP instance is bound to an IP address on the DHCP Client interface, use *nx_ip_status_check* to see confirm the IP address is valid.</span></span>

<span data-ttu-id="78432-585">Zaten DHCP çalıştıran başka arabirimler varsa, bu hizmet bu hizmet tarafından etkilenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="78432-585">If there are other interfaces already running DHCP, this service will not affect them.</span></span>

<span data-ttu-id="78432-586">Birden çok arabirim etkinleştirildiğinde, belirli bir arabirimde DHCP 'yi başlatmak için *nx_dhcp_interface_start* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="78432-586">To start DHCP on a specific interface when multiple interfaces are enabled, use the *nx_dhcp_interface_start* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-587">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-587">Input Parameters</span></span>

- <span data-ttu-id="78432-588">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-588">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-589">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-589">Return Values</span></span>

- <span data-ttu-id="78432-590">**NX_SUCCESS** (0x00) başarılı DHCP başlatması.</span><span class="sxs-lookup"><span data-stu-id="78432-590">**NX_SUCCESS** (0x00) Successful DHCP start.</span></span>  

- <span data-ttu-id="78432-591">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="78432-591">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP already started.</span></span>

- <span data-ttu-id="78432-592">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-592">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="78432-593">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="78432-593">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-594">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-594">Allowed From</span></span>

<span data-ttu-id="78432-595">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-595">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-596">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-596">Example</span></span>

```C
/* Start the DHCP processing for this IP instance. */
status =  nx_dhcp_start(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully started. */
```

## <a name="nx_dhcp_interface_start"></a><span data-ttu-id="78432-597">nx_dhcp_interface_start</span><span class="sxs-lookup"><span data-stu-id="78432-597">nx_dhcp_interface_start</span></span>

<span data-ttu-id="78432-598">Belirtilen arabirimde DHCP işlemeyi Başlat</span><span class="sxs-lookup"><span data-stu-id="78432-598">Start DHCP processing on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-599">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-599">Prototype</span></span>

```C
UINT nx_dhcp_interface_start(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="78432-600">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-600">Description</span></span>

<span data-ttu-id="78432-601">Bu hizmet, bu arabirim DHCP için etkinleştirilmişse, belirtilen arabirim üzerinde DHCP işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="78432-601">This service starts DHCP processing on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="78432-602">DHCP için bir arabirim etkinleştirme hakkında daha fazla ayrıntı için bkz. *nx_dhcp_interface_enable*().</span><span class="sxs-lookup"><span data-stu-id="78432-602">See *nx_dhcp_interface_enable*() for more details about enabling an interface for DHCP.</span></span> <span data-ttu-id="78432-603">Varsayılan olarak, uygulama nx_dhcp_create çağırdığında, birincil arabirim DHCP için etkinleştirilir *.*</span><span class="sxs-lookup"><span data-stu-id="78432-603">By default the primary interface is enabled for DHCP when the application calls *nx_dhcp_create.*</span></span>

<span data-ttu-id="78432-604">DHCP Istemcisi çalıştıran başka arabirim yoksa, bu hizmet DHCP istemci iş parçacığını başlatır/sürdürür ve (yeniden) DHCP Istemci zamanlayıcısını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="78432-604">If there are no other interfaces running DHCP Client this service will start/resume the DHCP Client thread and (re)activate the DHCP Client timer.</span></span>  
  
<span data-ttu-id="78432-605">Uygulamanın bir IP adresinin elde olup olmadığını doğrulamak için *nx_ip_status_check* kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78432-605">The application should use *nx_ip_status_check* to verify if an IP address is obtained.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-606">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-606">Input Parameters</span></span>

- <span data-ttu-id="78432-607">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-607">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="78432-608">**Interface_index** DHCP Istemcisinin başlatılacağı Dizin</span><span class="sxs-lookup"><span data-stu-id="78432-608">**Interface_index** Index on which to start the DHCP Client</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-609">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-609">Return Values</span></span>

- <span data-ttu-id="78432-610">**NX_SUCCESS** (0x00) başarılı DHCP başlatması.</span><span class="sxs-lookup"><span data-stu-id="78432-610">**NX_SUCCESS** (0x00) Successful DHCP start.</span></span>  

- <span data-ttu-id="78432-611">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP örneği zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="78432-611">**NX_DHCP_ALREADY_STARTED** (0x93) The DHCP instance has already been started.</span></span>

- <span data-ttu-id="78432-612">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-612">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="78432-613">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="78432-613">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

- <span data-ttu-id="78432-614">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-614">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-615">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-615">Allowed From</span></span>

<span data-ttu-id="78432-616">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-616">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-617">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-617">Example</span></span>

```C
/* Start the DHCP processing for this IP instance on interface 1. */
status =  nx_dhcp_interface_start(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully started. */
```

## <a name="nx_dhcp_state_change_notify"></a><span data-ttu-id="78432-618">nx_dhcp_state_change_notify</span><span class="sxs-lookup"><span data-stu-id="78432-618">nx_dhcp_state_change_notify</span></span>

<span data-ttu-id="78432-619">DHCP durum değiştirme geri çağırma işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="78432-619">Set DHCP state change callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-620">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-620">Prototype</span></span>

```C
UINT nx_dhcp_state_change_notify(
          NX_DHCP *dhcp_ptr, 
          VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                           UCHAR new_state));
```

### <a name="description"></a><span data-ttu-id="78432-621">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-621">Description</span></span>

<span data-ttu-id="78432-622">Bu hizmet, DHCP durum değişikliklerinin bir uygulamasına bildirimde bulunmak için dhcp_state_change_notify belirtilen geri çağırma işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="78432-622">This service registers the specified callback function dhcp_state_change_notify for notifying an application of DHCP state changes.</span></span> <span data-ttu-id="78432-623">Geri arama işlevi, DHCP Istemcisinin geçiş durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="78432-623">The callback function supplies the state the DHCP Client has transitioned into.</span></span>

<span data-ttu-id="78432-624">Aşağıdakiler, çeşitli DHCP durumlarıyla ilişkili değerlerdir:</span><span class="sxs-lookup"><span data-stu-id="78432-624">Following are values associated with the various DHCP states:</span></span>

| <span data-ttu-id="78432-625">Durum</span><span class="sxs-lookup"><span data-stu-id="78432-625">State</span></span>                             | <span data-ttu-id="78432-626">Değer</span><span class="sxs-lookup"><span data-stu-id="78432-626">Value</span></span> |
|-----------------------------------|-------|
| <span data-ttu-id="78432-627">NX \_ DHCP \_ durumu \_ önyüklemesi</span><span class="sxs-lookup"><span data-stu-id="78432-627">NX\_DHCP\_STATE\_BOOT</span></span>             | <span data-ttu-id="78432-628">1</span><span class="sxs-lookup"><span data-stu-id="78432-628">1</span></span>     |
| <span data-ttu-id="78432-629">NX \_ DHCP \_ durumu \_ INIT</span><span class="sxs-lookup"><span data-stu-id="78432-629">NX\_DHCP\_STATE\_INIT</span></span>             | <span data-ttu-id="78432-630">2</span><span class="sxs-lookup"><span data-stu-id="78432-630">2</span></span>     |
| <span data-ttu-id="78432-631">NX \_ DHCP \_ durumu \_ seçme</span><span class="sxs-lookup"><span data-stu-id="78432-631">NX\_DHCP\_STATE\_SELECTING</span></span>        | <span data-ttu-id="78432-632">3</span><span class="sxs-lookup"><span data-stu-id="78432-632">3</span></span>     |
| <span data-ttu-id="78432-633">NX \_ DHCP \_ durumu \_ isteniyor</span><span class="sxs-lookup"><span data-stu-id="78432-633">NX\_DHCP\_STATE\_REQUESTING</span></span>       | <span data-ttu-id="78432-634">4</span><span class="sxs-lookup"><span data-stu-id="78432-634">4</span></span>     |
| <span data-ttu-id="78432-635">NX \_ DHCP \_ durum \_ sınırı</span><span class="sxs-lookup"><span data-stu-id="78432-635">NX\_DHCP\_STATE\_BOUND</span></span>            | <span data-ttu-id="78432-636">5</span><span class="sxs-lookup"><span data-stu-id="78432-636">5</span></span>     |
| <span data-ttu-id="78432-637">NX \_ DHCP \_ durumu \_ yenileniyor</span><span class="sxs-lookup"><span data-stu-id="78432-637">NX\_DHCP\_STATE\_RENEWING</span></span>         | <span data-ttu-id="78432-638">6</span><span class="sxs-lookup"><span data-stu-id="78432-638">6</span></span>     |
| <span data-ttu-id="78432-639">NX \_ DHCP \_ durumu yeniden \_ bağlama</span><span class="sxs-lookup"><span data-stu-id="78432-639">NX\_DHCP\_STATE\_REBINDING</span></span>        | <span data-ttu-id="78432-640">7</span><span class="sxs-lookup"><span data-stu-id="78432-640">7</span></span>     |
| <span data-ttu-id="78432-641">NX_DHCP_STATE_FORCERENEW</span><span class="sxs-lookup"><span data-stu-id="78432-641">NX_DHCP_STATE_FORCERENEW</span></span>          | <span data-ttu-id="78432-642">8</span><span class="sxs-lookup"><span data-stu-id="78432-642">8</span></span>     |
| <span data-ttu-id="78432-643">NX \_ DHCP \_ durum \_ adresi \_ yoklama</span><span class="sxs-lookup"><span data-stu-id="78432-643">NX\_DHCP\_STATE\_ADDRESS\_PROBING</span></span> | <span data-ttu-id="78432-644">9</span><span class="sxs-lookup"><span data-stu-id="78432-644">9</span></span>     |


### <a name="input-parameters"></a><span data-ttu-id="78432-645">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-645">Input Parameters</span></span>

- <span data-ttu-id="78432-646">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-646">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="78432-647">**dhcp_state_change_notify** Durum değişikliği geri çağırma işlev işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-647">**dhcp_state_change_notify** State change callback function pointer</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-648">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-648">Return Values</span></span>

- <span data-ttu-id="78432-649">**NX_SUCCESS** (0x00) başarılı geri çağırma kümesi.</span><span class="sxs-lookup"><span data-stu-id="78432-649">**NX_SUCCESS** (0x00) Successful callback set.</span></span>  

- <span data-ttu-id="78432-650">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-650">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="78432-651">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="78432-651">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-652">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-652">Allowed From</span></span>

<span data-ttu-id="78432-653">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="78432-653">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="78432-654">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-654">Example</span></span>

```C
/* Register the “my_state_change” function to be called on any DHCP state change, 
   assuming DHCP has alreadybeen created. */
status =  nx_dhcp_state_change_notify(&my_dhcp, my_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered. */
```

## <a name="nx_dhcp_interface_state_change_notify"></a><span data-ttu-id="78432-655">nx_dhcp_interface_state_change_notify</span><span class="sxs-lookup"><span data-stu-id="78432-655">nx_dhcp_interface_state_change_notify</span></span>

<span data-ttu-id="78432-656">Belirtilen arabirimdeki DHCP durum değiştirme geri çağırma işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="78432-656">Set DHCP state change callback function on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-657">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-657">Prototype</span></span>

```C
UINT nx_dhcp_interface_state_change_notify(
              NX_DHCP *dhcp_ptr, 
              UINT interface_index,
              VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                               UINT interface_index,
                                               UCHAR new_state));
```

### <a name="description"></a><span data-ttu-id="78432-658">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-658">Description</span></span>

<span data-ttu-id="78432-659">Bu hizmet, DHCP durum değişikliklerinin bir uygulamasına bildirimde bulunmak için belirtilen geri çağırma işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="78432-659">This service registers the specified callback function for notifying an application of DHCP state changes.</span></span> <span data-ttu-id="78432-660">Geri çağırma, funcıton giriş bağımsız değişkenleri, arabirim dizinidir ve DHCP Istemcisinin bu arabirimde geçiş olduğu durumdur.</span><span class="sxs-lookup"><span data-stu-id="78432-660">The callback funciton input arguments are the interface index and the state the DHCP Client has transitioned to on that interface.</span></span>

<span data-ttu-id="78432-661">Durum değişikliği işlevleri hakkında daha fazla bilgi için bkz. *nx_dhcp_state_change_notify*().</span><span class="sxs-lookup"><span data-stu-id="78432-661">For more information about state change functions, see *nx_dhcp_state_change_notify*().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-662">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-662">Input Parameters</span></span>

- <span data-ttu-id="78432-663">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-663">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="78432-664">**dhcp_interface_state_change_notify** Uygulama geri çağırma işlev işaretçisi</span><span class="sxs-lookup"><span data-stu-id="78432-664">**dhcp_interface_state_change_notify** Application callback function pointer</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-665">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-665">Return Values</span></span>

- <span data-ttu-id="78432-666">**NX_SUCCESS** (0x00) başarılı geri çağırma kümesi.</span><span class="sxs-lookup"><span data-stu-id="78432-666">**NX_SUCCESS** (0x00) Successful callback set.</span></span>  

- <span data-ttu-id="78432-667">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-667">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-668">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-668">Allowed From</span></span>

<span data-ttu-id="78432-669">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="78432-669">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="78432-670">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-670">Example</span></span>

```C
/* Register the “my_state_change” function to be called on any DHCP state 
   change, assuming DHCP has alreadybeen created. */

void dhcp_interstate_state_change(NX_DHCP *dhcp_ptr, UINT iface_index, 
                                 UCHAR new_state);


status =  nx_dhcp_interstate_state_change_notify(&my_dhcp,  
                                                 dhcp_interstate_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered. */
```

## <a name="nx_dhcp_stop"></a><span data-ttu-id="78432-671">nx_dhcp_stop</span><span class="sxs-lookup"><span data-stu-id="78432-671">nx_dhcp_stop</span></span>

<span data-ttu-id="78432-672">DHCP işlemesini durduruyor</span><span class="sxs-lookup"><span data-stu-id="78432-672">Stops DHCP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-673">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-673">Prototype</span></span>

```C
UINT nx_dhcp_stop(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-674">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-674">Description</span></span>

<span data-ttu-id="78432-675">Bu hizmet, DHCP işlemesini Başlatan tüm arabirimlerde DHCP işlemeyi durduruyor.</span><span class="sxs-lookup"><span data-stu-id="78432-675">This service stops DHCP processing on all interfaces that have started DHCP processing.</span></span> <span data-ttu-id="78432-676">DHCP 'yi işleyen bir arabirim yoksa, bu hizmet DHCP Istemci iş parçacığını askıya alacak ve DHCP Istemci zamanlayıcısını devre dışı kalacak.</span><span class="sxs-lookup"><span data-stu-id="78432-676">If there are no interfaces processing DHCP, this service will suspend the DHCP Client thread, and inactivate the DHCP Client timer.</span></span>

<span data-ttu-id="78432-677">DHCP için birden çok arabirim etkinleştirilmişse, belirli bir arabirimdeki DHCP 'yi durdurmak için *nx_dhcp_interface_stop* hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="78432-677">To stop DHCP on a specific interface if multiple interfaces are enabled for DHCP, use the *nx_dhcp_interface_stop* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-678">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-678">Input Parameters</span></span>

- <span data-ttu-id="78432-679">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-679">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-680">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-680">Return Values</span></span>

- <span data-ttu-id="78432-681">**NX_SUCCESS** (0x00) başarılı DHCP durağı</span><span class="sxs-lookup"><span data-stu-id="78432-681">**NX_SUCCESS** (0x00) Successful DHCP stop</span></span>

- <span data-ttu-id="78432-682">**NX_DHCP_NOT_STARTED** (0x96) DHCP örneği başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="78432-682">**NX_DHCP_NOT_STARTED** (0x96) The DHCP instance not started.</span></span>

- <span data-ttu-id="78432-683">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-683">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="78432-684">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="78432-684">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-685">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-685">Allowed From</span></span>

<span data-ttu-id="78432-686">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-686">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-687">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-687">Example</span></span>

```C
/* Stop the DHCP processing for this IP instance. */
status =  nx_dhcp_stop(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully stopped. */
```

## <a name="nx_dhcp_interface_stop"></a><span data-ttu-id="78432-688">nx_dhcp_interface_stop</span><span class="sxs-lookup"><span data-stu-id="78432-688">nx_dhcp_interface_stop</span></span>

<span data-ttu-id="78432-689">Belirtilen arabirimdeki DHCP işlemesini durdur</span><span class="sxs-lookup"><span data-stu-id="78432-689">Stop DHCP processing on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-690">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-690">Prototype</span></span>

```C
UINT nx_dhcp_interface_stop(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="78432-691">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-691">Description</span></span>

<span data-ttu-id="78432-692">Bu hizmet, DHCP zaten başlatılmışsa belirtilen arabirimdeki DHCP işlemesini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="78432-692">This service stops DHCP processing on the specified interface if DHCP is already started.</span></span> <span data-ttu-id="78432-693">DHCP çalıştıran başka arabirimler yoksa, DHCP iş parçacığı ve Zamanlayıcı askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="78432-693">If there are no other interfaces running DHCP, the DHCP thread and timer are suspended.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-694">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-694">Input Parameters</span></span>

- <span data-ttu-id="78432-695">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-695">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="78432-696">**Interface_index** DHCP işlemenin durdurulacağı arabirim</span><span class="sxs-lookup"><span data-stu-id="78432-696">**Interface_index** Interface on which to stop DHCP processing</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-697">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-697">Return Values</span></span>

- <span data-ttu-id="78432-698">**NX_SUCCESS** (0x00) başarılı DHCP durağı</span><span class="sxs-lookup"><span data-stu-id="78432-698">**NX_SUCCESS** (0x00) Successful DHCP stop</span></span>

- <span data-ttu-id="78432-699">**NX_DHCP_NOT_STARTED** (0x96) DHCP başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="78432-699">**NX_DHCP_NOT_STARTED** (0x96) DHCP not started.</span></span>

- <span data-ttu-id="78432-700">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-700">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="78432-701">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="78432-701">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

- <span data-ttu-id="78432-702">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-702">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-703">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-703">Allowed From</span></span>

<span data-ttu-id="78432-704">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-704">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-705">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-705">Example</span></span>

```C
/* Stop DHCP processing for this IP instance on interface 1. */
status =  nx_dhcp_interface_stop(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully stopped. */
```

## <a name="nx_dhcp_user_option_retrieve"></a><span data-ttu-id="78432-706">nx_dhcp_user_option_retrieve</span><span class="sxs-lookup"><span data-stu-id="78432-706">nx_dhcp_user_option_retrieve</span></span>

<span data-ttu-id="78432-707">Son sunucu yanıtından bir DHCP seçeneği alın</span><span class="sxs-lookup"><span data-stu-id="78432-707">Retrieve a DHCP option from last server response</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-708">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-708">Prototype</span></span>

```C
UINT nx_dhcp_user_option_retrieve(NX_DHCP *dhcp_ptr, 
            UINT request_option, UCHAR *destination_ptr, 
            UINT *destination_size);
```

### <a name="description"></a><span data-ttu-id="78432-709">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-709">Description</span></span>

<span data-ttu-id="78432-710">Bu hizmet, DHCP Istemci kaydında bulunan DHCP için etkinleştirilen ilk arabirimdeki DHCP seçenekleri arabelleğinden belirtilen DHCP seçeneğini alır.</span><span class="sxs-lookup"><span data-stu-id="78432-710">This service retrieves the specified DHCP option from the DHCP options buffer on the first interface enabled for DHCP found on the DHCP Client record.</span></span> <span data-ttu-id="78432-711">Başarılı olursa, seçenek verileri belirtilen arabelleğe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="78432-711">If successful, the option data is copied into the specified buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-712">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-712">Input Parameters</span></span>

- <span data-ttu-id="78432-713">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-713">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>  

- <span data-ttu-id="78432-714">**request_option** RFC tarafından belirtilen şekilde DHCP seçeneği.</span><span class="sxs-lookup"><span data-stu-id="78432-714">**request_option** DHCP option, as specified by the RFCs.</span></span> <span data-ttu-id="78432-715">*Nx_dhcp. h* içindeki NX_DHCP_OPTION seçeneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="78432-715">See the NX_DHCP_OPTION option in *nx_dhcp.h*.</span></span>

- <span data-ttu-id="78432-716">**destination_ptr** Yanıt dizesi için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-716">**destination_ptr** Pointer to the destination for the response string.</span></span>  

- <span data-ttu-id="78432-717">**destination_size** Hedefin boyutuna ve dönüşe ilişkin işaretçi, döndürülen bayt sayısını yerleştirmek için hedef.</span><span class="sxs-lookup"><span data-stu-id="78432-717">**destination_size** Pointer to the size of the destination and on return, the destination to place the number of bytes returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-718">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-718">Return Values</span></span>

- <span data-ttu-id="78432-719">**NX_SUCCESS** (0x00) başarılı seçenek alma.</span><span class="sxs-lookup"><span data-stu-id="78432-719">**NX_SUCCESS** (0x00) Successful option retrieval.</span></span>  

- <span data-ttu-id="78432-720">**NX_DHCP_NOT_BOUND** (0x94) DHCP istemcisi bağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="78432-720">**NX_DHCP_NOT_BOUND** (0x94) DHCP Client not bound.</span></span>

- <span data-ttu-id="78432-721">**NX_DHCP_NO_INTERFACES_ENABLED** (0xa5) DHCP için etkinleştirilen arabirim yok</span><span class="sxs-lookup"><span data-stu-id="78432-721">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces enabled for DHCP</span></span>

- <span data-ttu-id="78432-722">**NX_DHCP_DEST_TO_SMALL** (0x95) hedefi, yanıtı tutmak için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="78432-722">**NX_DHCP_DEST_TO_SMALL** (0x95) Destination is too small to hold response.</span></span>

- <span data-ttu-id="78432-723">Sunucu yanıtında **NX_DHCP_PARSE_ERROR** (0x97) DHCP seçeneği bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="78432-723">**NX_DHCP_PARSE_ERROR** (0x97) DHCP Option not found in Server response.</span></span>

- <span data-ttu-id="78432-724">NX_PTR_ERROR (0x16) geçersiz giriş işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-724">NX_PTR_ERROR (0x16) Invalid input pointer.</span></span>

- <span data-ttu-id="78432-725">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="78432-725">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-726">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-726">Allowed From</span></span>

<span data-ttu-id="78432-727">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-727">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-728">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-728">Example</span></span>

```C
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server. */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_user_option_retrieve(&my_dhcp, NX_DHCP_OPTION_DNS_SVR,
        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string. */
```

## <a name="nx_dhcp_interface_user_option_retrieve"></a><span data-ttu-id="78432-729">nx_dhcp_interface_user_option_retrieve</span><span class="sxs-lookup"><span data-stu-id="78432-729">nx_dhcp_interface_user_option_retrieve</span></span>

<span data-ttu-id="78432-730">Belirtilen arabirimdeki son sunucu yanıtından bir DHCP seçeneği alın</span><span class="sxs-lookup"><span data-stu-id="78432-730">Retrieve a DHCP option from last server response on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-731">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-731">Prototype</span></span>

```C
UINT nx_dhcp_interface_user_option_retrieve(NX_DHCP *dhcp_ptr,
                  UINT interface_index, 
            UINT request_option, UCHAR *destination_ptr, 
            UINT *destination_size);
```

### <a name="description"></a><span data-ttu-id="78432-732">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-732">Description</span></span>

<span data-ttu-id="78432-733">Bu hizmet, belirtilen arabirim DHCP için etkinleştirilirse belirtilen arabirimdeki DHCP seçenekleri arabelleğinden belirtilen DHCP seçeneğini alır.</span><span class="sxs-lookup"><span data-stu-id="78432-733">This service retrieves the specified DHCP option from the DHCP options buffer on the specified interface, if that interface is enabled for DHCP.</span></span> <span data-ttu-id="78432-734">Başarılı olursa, seçenek verileri belirtilen arabelleğe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="78432-734">If successful, the option data is copied into the specified buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-735">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-735">Input Parameters</span></span>

- <span data-ttu-id="78432-736">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-736">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="78432-737">**Interface_index** Belirtilen seçeneğin alınacağı dizin</span><span class="sxs-lookup"><span data-stu-id="78432-737">**Interface_index** Index on which to retrieve the specified option</span></span>  

- <span data-ttu-id="78432-738">**request_option** RFC tarafından belirtilen şekilde DHCP seçeneği.</span><span class="sxs-lookup"><span data-stu-id="78432-738">**request_option** DHCP option, as specified by the RFCs.</span></span> <span data-ttu-id="78432-739">*Nx_dhcp. h* içindeki NX_DHCP_OPTION seçeneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="78432-739">See the NX_DHCP_OPTION option in *nx_dhcp.h*.</span></span>  

- <span data-ttu-id="78432-740">**destination_ptr** Yanıt dizesi için hedefin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-740">**destination_ptr** Pointer to the destination for the response string.</span></span>  

- <span data-ttu-id="78432-741">**destination_size** Hedefin boyutuna ve dönüşe ilişkin işaretçi, döndürülen bayt sayısını yerleştirmek için hedef.</span><span class="sxs-lookup"><span data-stu-id="78432-741">**destination_size** Pointer to the size of the destination and on return, the destination to place the number of bytes returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-742">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-742">Return Values</span></span>

- <span data-ttu-id="78432-743">**NX_SUCCESS** (0x00) başarılı seçenek alma.</span><span class="sxs-lookup"><span data-stu-id="78432-743">**NX_SUCCESS** (0x00) Successful option retrieval.</span></span>  

- <span data-ttu-id="78432-744">**NX_DHCP_NOT_BOUND** (0x94) IP adresi atanmadı</span><span class="sxs-lookup"><span data-stu-id="78432-744">**NX_DHCP_NOT_BOUND** (0x94) IP address not assigned</span></span>

- <span data-ttu-id="78432-745">**NX_DHCP_DEST_TO_SMALL** (0x95) arabelleği çok küçük</span><span class="sxs-lookup"><span data-stu-id="78432-745">**NX_DHCP_DEST_TO_SMALL** (0x95) Buffer is too small</span></span>

- <span data-ttu-id="78432-746">Sunucu yanıtında **NX_DHCP_PARSE_ERROR** (0x97) DHCP seçeneği bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="78432-746">**NX_DHCP_PARSE_ERROR** (0x97) DHCP Option not found in Server response.</span></span>

- <span data-ttu-id="78432-747">NX_PTR_ERROR (0x16) geçersiz DHCP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-747">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="78432-748">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="78432-748">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

- <span data-ttu-id="78432-749">NX_INVALID_INTERFACE (0x4C) geçersiz ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="78432-749">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-750">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-750">Allowed From</span></span>

<span data-ttu-id="78432-751">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-751">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-752">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-752">Example</span></span>

```C
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server on the prmary interface. */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_interface_user_option_retrieve(&my_dhcp, 0, NX_DHCP_OPTION_DNS_SVR,
        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string. */
```

## <a name="nx_dhcp_user_option_convert"></a><span data-ttu-id="78432-753">nx_dhcp_user_option_convert</span><span class="sxs-lookup"><span data-stu-id="78432-753">nx_dhcp_user_option_convert</span></span>

<span data-ttu-id="78432-754">Dört baytı ULONG 'a Dönüştür</span><span class="sxs-lookup"><span data-stu-id="78432-754">Convert four bytes to ULONG</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-755">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-755">Prototype</span></span>

```C
ULONG nx_dhcp_user_option_convert(UCHAR *option_string_ptr);
```

### <a name="description"></a><span data-ttu-id="78432-756">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-756">Description</span></span>

<span data-ttu-id="78432-757">Bu hizmet, "option_string_ptr" ile işaret edilen dört karakteri işaretsiz bir Long değere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="78432-757">This service converts the four characters pointed to by “option_string_ptr” into an unsigned long value.</span></span> <span data-ttu-id="78432-758">Bu, özellikle IP adresleri mevcut olduğunda faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="78432-758">It is especially useful when IP addresses are present.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-759">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-759">Input Parameters</span></span>

- <span data-ttu-id="78432-760">**option_string_ptr** Daha önce alınan seçenek dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-760">**option_string_ptr** Pointer to previously retrieved option string.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-761">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-761">Return Values</span></span>

- <span data-ttu-id="78432-762">**Değer** İlk dört baytın değeri.</span><span class="sxs-lookup"><span data-stu-id="78432-762">**Value** Value of first four bytes.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-763">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-763">Allowed From</span></span>

<span data-ttu-id="78432-764">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-764">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-765">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-765">Example</span></span>

```C
UCHAR  dns_ip_string[4];
ULONG  dns_ip;

/* Convert the first four bytes of “dns_ip_string” to an actual IP
address in “dns_ip.”  */
dns_ip=  nx_dhcp_user_option_convert(dns_ip_string);

/* If status is NX_SUCCESS the DNS IP address is in “dns_ip.”  */
```

## <a name="nx_dhcp_user_option_add_callback_set"></a><span data-ttu-id="78432-766">nx_dhcp_user_option_add_callback_set</span><span class="sxs-lookup"><span data-stu-id="78432-766">nx_dhcp_user_option_add_callback_set</span></span>

<span data-ttu-id="78432-767">Kullanıcı tarafından sağlanan seçenekleri eklemek için geri çağırma işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="78432-767">Set callback function for adding user supplied options</span></span>

### <a name="prototype"></a><span data-ttu-id="78432-768">Prototype</span><span class="sxs-lookup"><span data-stu-id="78432-768">Prototype</span></span>

```C
ULONG nx_dhcp_user_option_add_callbcak_set(NX_DHCP *dhcp_ptr, 
    UINT (*dhcp_user_option_add)(NX_DHCP *dhcp_ptr, 
                                 UINT iface_index, 
                                 UINT message_type, 
                                 UCHAR *user_option_ptr, 
                                 UINT *user_option_length));
```

### <a name="description"></a><span data-ttu-id="78432-769">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78432-769">Description</span></span>

<span data-ttu-id="78432-770">Bu hizmet, Kullanıcı tarafından sağlanan seçenekleri eklemek için belirtilen geri çağırma işlevini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="78432-770">This service registers the specified callback function for adding user supplied options.</span></span>

<span data-ttu-id="78432-771">Geri çağırma işlevi belirtilmişse, uygulamalar iface_index ve message_type tarafından pakete Kullanıcı tarafından sağlanan seçenekleri ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="78432-771">If the callback function specified, the applications can add user supplied options into the packet by iface_index and message_type.</span></span>

> [!NOTE]
> <span data-ttu-id="78432-772">Kullanıcı yordamında.</span><span class="sxs-lookup"><span data-stu-id="78432-772">In user’s routine.</span></span> <span data-ttu-id="78432-773">Kullanıcı tarafından sağlanan seçenekler eklerken uygulamaların DHCP seçenekleri biçimi gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="78432-773">Applications must follow the DHCP options format when add user supplied options.</span></span> <span data-ttu-id="78432-774">Kullanıcı seçeneklerinin toplam boyutu user_option_length küçük veya eşit olmalı ve user_option_length gerçek seçenek uzunluğu olarak güncellenebilir.</span><span class="sxs-lookup"><span data-stu-id="78432-774">The total size of user options must be less or equal to user_option_length, and update the user_option_length as real options length.</span></span> <span data-ttu-id="78432-775">Seçenek başarıyla Ekle ' NX_TRUE döndürün, aksi NX_FALSE döndürün.</span><span class="sxs-lookup"><span data-stu-id="78432-775">Return NX_TRUE if add options successfully, else return NX_FALSE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="78432-776">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="78432-776">Input Parameters</span></span>

- <span data-ttu-id="78432-777">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-777">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="78432-778">**dhcp_user_option_add** Kullanıcı seçeneği ekleme işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="78432-778">**dhcp_user_option_add** Pointer to user option add function.</span></span>

### <a name="return-values"></a><span data-ttu-id="78432-779">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="78432-779">Return Values</span></span>

- <span data-ttu-id="78432-780">**NX_SUCCESS** (0x00) başarılı geri çağırma kümesi.</span><span class="sxs-lookup"><span data-stu-id="78432-780">**NX_SUCCESS** (0x00) Successful callback set.</span></span>

- <span data-ttu-id="78432-781">NX_PTR_ERROR (0x16) geçersiz işaretçi.</span><span class="sxs-lookup"><span data-stu-id="78432-781">NX_PTR_ERROR (0x16) Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="78432-782">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="78432-782">Allowed From</span></span>

<span data-ttu-id="78432-783">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="78432-783">Threads</span></span>

### <a name="example"></a><span data-ttu-id="78432-784">Örnek</span><span class="sxs-lookup"><span data-stu-id="78432-784">Example</span></span>

```C
/* Register the “my_dhcp_user_option_add” function to be called when add DHCP
options, assuming DHCP has already been created. */

status =  nx_dhcp_user_option_add_callback_set(&my_dhcp, my_dhcp_user_option_add);

/* If status is NX_SUCCESS the callback function was successfully registered. */
```
