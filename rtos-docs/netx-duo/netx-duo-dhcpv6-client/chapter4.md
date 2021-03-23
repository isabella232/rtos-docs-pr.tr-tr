---
title: Bölüm 4-Azure RTOS NetX Duo DHCPv6 Istemci Hizmetleri
description: Bu bölüm, tüm Azure RTOS NetX Duo DHCPv6 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 40fbfa7319ca95af65c92b12582d4bbb05005dc0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826074"
---
# <a name="chapter-4---azure-rtos-netx-duo-dhcpv6-client-services"></a><span data-ttu-id="f7734-103">Bölüm 4-Azure RTOS NetX Duo DHCPv6 Istemci Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="f7734-103">Chapter 4 - Azure RTOS NetX Duo DHCPv6 Client services</span></span>

<span data-ttu-id="f7734-104">Bu bölüm, tüm Azure RTOS NetX Duo DHCPv6 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="f7734-104">This chapter contains a description of all Azure RTOS NetX Duo DHCPv6 Client services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="f7734-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="f7734-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="f7734-106">**nx_dhcpv6_client_create:** *DHCPv6 istemci örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="f7734-106">**nx_dhcpv6_client_create:** *Create a DHCPv6 Client instance*</span></span> 

- <span data-ttu-id="f7734-107">**nx_dhcpv6_client_delete:** *DHCPv6 istemci örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="f7734-107">**nx_dhcpv6_client_delete:** *Delete a DHCPv6 Client instance*</span></span> 

- <span data-ttu-id="f7734-108">**nx_dhcpv6_create_ client_duid:** *bir DHCPv6 istemcisi DUID oluşturma*</span><span class="sxs-lookup"><span data-stu-id="f7734-108">**nx_dhcpv6_create_ client_duid:** *Create a DHCPv6 Client DUID*</span></span> 

- <span data-ttu-id="f7734-109">**nx_dhcpv6 _add_client_ia:** *DHCPv6 istemci kimlik adresı ekleme (IA)*</span><span class="sxs-lookup"><span data-stu-id="f7734-109">**nx_dhcpv6 _add_client_ia:** *Add a DHCPv6 Client Identity Address (IA)*</span></span> 

- <span data-ttu-id="f7734-110">**nx_dhcpv6 _create_client_ia:** (*eski bir DHCPv6 istemci KIMLIK adresi (IA) Ekle)*</span><span class="sxs-lookup"><span data-stu-id="f7734-110">**nx_dhcpv6 _create_client_ia:** (*Legacy Add a DHCPv6 Client Identity Address (IA))*</span></span> 

- <span data-ttu-id="f7734-111">**nx_dhcpv6_create_client_iana:** *geçici olmayan adresler (IANA) Için DHCPv6 istemci kimliği ilişkilendirmesi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="f7734-111">**nx_dhcpv6_create_client_iana:** *Create a DHCPv6 Client Identity Association for Non Temporary Addresses (IANA)*</span></span> 

- <span data-ttu-id="f7734-112">**nx_dhcpv6_get_client_duid_time_id:** *DHCPv6 istemcisi DUID 'den saat kimliğini alın*</span><span class="sxs-lookup"><span data-stu-id="f7734-112">**nx_dhcpv6_get_client_duid_time_id:** *Get the time ID from DHCPv6 Client DUID*</span></span> 

- <span data-ttu-id="f7734-113">**nx_dhcpv6_client_set_interface:** *DHCPv6 sunucusuyla iletişim için istemci ağ arabirimini ayarlama*</span><span class="sxs-lookup"><span data-stu-id="f7734-113">**nx_dhcpv6_client_set_interface:** *Set the Client network interface for communications with the DHCPv6 Server*</span></span> 

- <span data-ttu-id="f7734-114">**nx_dhcpv6_get_IP_address:** *DHCPv6 Istemcisine atanan genel IPv6 adresini al*</span><span class="sxs-lookup"><span data-stu-id="f7734-114">**nx_dhcpv6_get_IP_address:** *Get the global IPv6 address assigned to the DHCPv6 client*</span></span> 

- <span data-ttu-id="f7734-115">**nx_dhcpv6_get_lease_time_data:** *istemci genel IPv6 adresi Için T1, T2, geçerli ve tercih edilen yaşam süreleri alın*</span><span class="sxs-lookup"><span data-stu-id="f7734-115">**nx_dhcpv6_get_lease_time_data:** *Get T1, T2, valid and preferred lifetimes for the Client global IPv6 address*</span></span>

- <span data-ttu-id="f7734-116">**nx_dhcpv6_get_valid_ip_address_lease_time:** *Adres dizinine göre DHCPv6 istemci IPv6 adresi Için T1, T2, geçerli ve tercih edilen yaşam süreleri alın*</span><span class="sxs-lookup"><span data-stu-id="f7734-116">**nx_dhcpv6_get_valid_ip_address_lease_time:** *Get T1, T2, valid and preferred lifetimes for the DHCPv6 Client IPv6 address by address index*</span></span> 

- <span data-ttu-id="f7734-117">**nx_dhcpv6_get_iana_lease_time:** *DHCPv6 Istemcisine kiralanmış kimlik ILIŞKILENDIRMESINDE (IANA) T1 ve T2 alın*</span><span class="sxs-lookup"><span data-stu-id="f7734-117">**nx_dhcpv6_get_iana_lease_time:** *Get T1 and T2 in the Identity Association (IANA) leased to the DHCPv6 Client*</span></span> 

- <span data-ttu-id="f7734-118">**nx_dhcpv6_get_other_option_data:** *belirtilen seçenek verilerini al, örn. etki alanı adı veya saat dilimi sunucusu*</span><span class="sxs-lookup"><span data-stu-id="f7734-118">**nx_dhcpv6_get_other_option_data:** *Get the specified option data e.g. domain name or time zone server*</span></span> 

- <span data-ttu-id="f7734-119">**nx_dhcpv6_get_DNS_server_address:** *belirtilen dizindeki DNS sunucu ADRESINI DHCPv6 istemci DNS sunucusu listesine al*</span><span class="sxs-lookup"><span data-stu-id="f7734-119">**nx_dhcpv6_get_DNS_server_address:** *Get DNS Server address at the specified index into the DHCPv6 Client DNS server list*</span></span> 

- <span data-ttu-id="f7734-120">**nx_dhcpv6_get_time_accrued:** *genel IPv6 adresi kiralamasının DHCPv6 istemcisine bağladığına yönelik zaman kazanın*</span><span class="sxs-lookup"><span data-stu-id="f7734-120">**nx_dhcpv6_get_time_accrued:** *Get the time accrued the global IPv6 address lease has been bound to the DHCPv6 Client*</span></span> 

- <span data-ttu-id="f7734-121">**nx_dhcpv6_get_time_server_address:** *belirtilen dizindeki saat sunucusu adresini DHCPv6 istemci zamanı sunucu listesine al*</span><span class="sxs-lookup"><span data-stu-id="f7734-121">**nx_dhcpv6_get_time_server_address:** *Get Time Server address at the specified index into the DHCPv6 Client Time server list*</span></span>

- <span data-ttu-id="f7734-122">**nx_dhcpv6_get_valid_ip_address_count:** *DHCPv6 istemcisine atanan IPv6 adresi sayısını Al*</span><span class="sxs-lookup"><span data-stu-id="f7734-122">**nx_dhcpv6_get_valid_ip_address_count:** *Get the number of IPv6 addresses assigned to the DHCPv6 Client*</span></span> 

- <span data-ttu-id="f7734-123">**nx_dhcpv6_reinitialize:** *DHCPv6 istemci durumu makinesini yeniden başlatmak için DHCPv6 'yi yeniden başlatın ve DHCPv6 protokolünü yeniden çalıştırarak*</span><span class="sxs-lookup"><span data-stu-id="f7734-123">**nx_dhcpv6_reinitialize:** *Reinitialize the DHCPv6 for restarting the DHCPv6 Client state machine and rerunning the DHCPv6 protocol*</span></span> 

- <span data-ttu-id="f7734-124">**nx_dhcpv6_request_confirm:** *sunucuya bir onaylama isteği gönderin*</span><span class="sxs-lookup"><span data-stu-id="f7734-124">**nx_dhcpv6_request_confirm:** *Send a CONFIRM request to the Server*</span></span> 

- <span data-ttu-id="f7734-125">**nx_dhcpv6_request_inform_request:** S *BIR BILDIR istek Iletisini sunucuya Sonlandır*</span><span class="sxs-lookup"><span data-stu-id="f7734-125">**nx_dhcpv6_request_inform_request:** S *end an INFORM REQUEST message to the Server*</span></span> 

- <span data-ttu-id="f7734-126">**nx_dhcpv6_request_release:** *sunucuya bir yayın isteği gönderin*</span><span class="sxs-lookup"><span data-stu-id="f7734-126">**nx_dhcpv6_request_release:** *Send a RELEASE request to the Server*</span></span> 

- <span data-ttu-id="f7734-127">**nx_dhcpv6_request_option_DNS_server:** *sunucu için Istek iletileri içindeki istemci SEÇENEĞI istek verilerine DNS sunucusu seçeneğini ekleyin*</span><span class="sxs-lookup"><span data-stu-id="f7734-127">**nx_dhcpv6_request_option_DNS_server:** *Add the DNS server option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="f7734-128">**nx_dhcpv6_request_option_FQDN:** *sunucu için Istek iletileri içindeki istemci SEÇENEĞI istek verilerine FQDN seçeneğini ekleyin*</span><span class="sxs-lookup"><span data-stu-id="f7734-128">**nx_dhcpv6_request_option_FQDN:** *Add the FQDN option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="f7734-129">**nx_dhcpv6_request_option_domain_name:** *sunucu için Istek iletileri içindeki istemci seçeneği istek verilerine etki alanı adı seçeneğini ekleyin*</span><span class="sxs-lookup"><span data-stu-id="f7734-129">**nx_dhcpv6_request_option_domain_name:** *Add the domain name option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="f7734-130">**nx_dhcpv6_request_option_time_server:** *sunucuya istek iletileri Istek iletileri için istemci seçeneğine saat sunucusu seçeneğini ekleyin*</span><span class="sxs-lookup"><span data-stu-id="f7734-130">**nx_dhcpv6_request_option_time_server:** *Add the time server option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="f7734-131">**nx_dhcpv6_request_option_timezone:** *sunucuya Istek iletileri iste istemci seçeneği istek verilerine saat dilimi seçeneğini ekleyin*</span><span class="sxs-lookup"><span data-stu-id="f7734-131">**nx_dhcpv6_request_option_timezone:** *Add the time zone option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="f7734-132">**nx_dhcpv6_request_solicit:** *istemci ağındaki (yayın) herhangi BIR sunucuya DHCPv6 istem isteği gönderin*</span><span class="sxs-lookup"><span data-stu-id="f7734-132">**nx_dhcpv6_request_solicit:** *Send a DHCPv6 SOLICIT request to any Server on the Client network (broadcast)*</span></span> 

- <span data-ttu-id="f7734-133">**nx_dhcpv6_request_solicit_rapid:** *hızlı tamamlama seçenek kümesiyle istemci ağındaki (yayın) herhangi bir sunucuya bir DHCPv6 istek isteği gönderin*</span><span class="sxs-lookup"><span data-stu-id="f7734-133">**nx_dhcpv6_request_solicit_rapid:** *Send a DHCPv6 SOLICIT request to any Server on the Client network (broadcast) with the Rapid Commit option set*</span></span> 

- <span data-ttu-id="f7734-134">**nx_dhcpv6_resume:** *DHCPv6 istemci işlemesini sürdürür*</span><span class="sxs-lookup"><span data-stu-id="f7734-134">**nx_dhcpv6_resume:** *Resume DHCPv6 Client processing*</span></span> 

- <span data-ttu-id="f7734-135">**nx_dhcpv6_start:** *DHCPv6 istemci iş parçacığı görevini başlatın. Bu, DHCPv6 durum makinesinin başlatılmasına eşit değildir ve bir Istem isteği göndermez*</span><span class="sxs-lookup"><span data-stu-id="f7734-135">**nx_dhcpv6_start:** *Start the DHCPv6 Client thread task. Note this is not equivalent to starting the DHCPv6 state machine and does not send a SOLICIT request*</span></span> 

- <span data-ttu-id="f7734-136">**nx_dhcpv6_stop:** *DHCPv6 istemci iş parçacığı görevini durdur*</span><span class="sxs-lookup"><span data-stu-id="f7734-136">**nx_dhcpv6_stop:** *Stop the DHCPv6 Client thread task*</span></span> 

- <span data-ttu-id="f7734-137">**nx_dhcpv6_suspend:** *DHCPv6 istemci iş parçacığı görevini askıya al*</span><span class="sxs-lookup"><span data-stu-id="f7734-137">**nx_dhcpv6_suspend:** *Suspend the DHCPv6 Client thread task*</span></span> 

- <span data-ttu-id="f7734-138">**nx_dhcpv6_set_time_accrued:** *Istemci kaydındaki genel istemci IPv6 adresi kirası üzerinde tahakkuk eden süreyi ayarlayın.*</span><span class="sxs-lookup"><span data-stu-id="f7734-138">**nx_dhcpv6_set_time_accrued:** *Set the time accrued on the global Client IPv6 address lease in the Client record.*</span></span>

## <a name="nx_dhcpv6_client_create"></a><span data-ttu-id="f7734-139">nx_dhcpv6_client_create</span><span class="sxs-lookup"><span data-stu-id="f7734-139">nx_dhcpv6_client_create</span></span>

<span data-ttu-id="f7734-140">DHCPv6 istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7734-140">Create a DHCPv6 client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-141">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-141">Prototype</span></span>

```C
UINT  nx_dhcpv6_client_create(NX_DHCPV6 *dhcpv6_ptr, 
                        NX_IP *ip_ptr, CHAR *name_ptr, 
                        NX_PACKET_POOL *packet_pool_ptr, 
                        VOID *stack_ptr, ULONG stack_size,
                        VOID (*dhcpv6_state_change_notify)
                                 (struct NX_DHCPV6_STRUCT *dhcpv6_ptr, 
                                  UINT old_state, UINT new_state), 
                        VOID (*dhcpv6_server_error_handler)
                                 (struct NX_DHCPV6_STRUCT *dhcpv6_ptr, 
                                 UINT op_code, UINT status_code, 
                                 UINT message_type));
```

### <a name="description"></a><span data-ttu-id="f7734-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-142">Description</span></span>

<span data-ttu-id="f7734-143">Bu hizmet, geri çağırma işlevleri dahil olmak üzere bir DHCPv6 istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f7734-143">This service creates a DHCPv6 client instance including callback functions.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-144">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-144">Input Parameters</span></span>

- <span data-ttu-id="f7734-145">**dhcpv6_ptr** DHCPv6 denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-145">**dhcpv6_ptr** Pointer to DHCPv6 control block</span></span>  

- <span data-ttu-id="f7734-146">**ip_ptr** Istemci IP örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-146">**ip_ptr** Pointer to Client IP instance</span></span>  

- <span data-ttu-id="f7734-147">**name_ptr** DHCPv6 örneği için ad işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-147">**name_ptr** Pointer to name for DHCPv6 instance</span></span>

- <span data-ttu-id="f7734-148">**packet_pool_ptr** Istemci paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-148">**packet_pool_ptr** Pointer to Client packet pool</span></span>

- <span data-ttu-id="f7734-149">**stack_ptr** Istemci yığını belleği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-149">**stack_ptr** Pointer to Client stack memory</span></span>

- <span data-ttu-id="f7734-150">**stack_size** Istemci yığını bellek boyutu</span><span class="sxs-lookup"><span data-stu-id="f7734-150">**stack_size** Size of Client stack memory</span></span>

- <span data-ttu-id="f7734-151">**dhcpv6_state_change_notify** Istemci sunucuya yeni bir DHCPv6 isteği başlattığında çağrılan geri çağırma işlevi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-151">**dhcpv6_state_change_notify** Pointer to callback function invoked when the Client initiates a new DHCPv6 request to the server</span></span>

- <span data-ttu-id="f7734-152">**dhcpv6_server_error_handler** Istemci sunucudan bir hata durumu aldığında çağrılan geri çağırma işlevi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-152">**dhcpv6_server_error_handler** Pointer to callback function invoked when the Client receives an error status from the server</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-153">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-153">Return Values</span></span>

- <span data-ttu-id="f7734-154">**NX_SUCCESS** (0x00) başarılı istemci oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7734-154">**NX_SUCCESS** (0x00) Successful Client create</span></span>

- <span data-ttu-id="f7734-155">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-155">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-156">NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-156">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-157">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-157">Allowed From</span></span>

<span data-ttu-id="f7734-158">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-158">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-159">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-159">Example</span></span>

```C
/* Create a DHCPv6 client instance without specifying link local or preferred
   global IP address.  */
status =  nx_dhcpv6_client_create(&dhcp_0, &ip_0, "DHCPv6 Client", &pool_0,
                                  NULL, NULL, pointer, 2048,        
                                  dhcpv6_state_change_notify, 
                                  dhcpv6_server_error_handler);

/* If status is NX_SUCCESS a DHCPv6 client instance was successfully
   created.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-160">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-160">See Also</span></span>

- <span data-ttu-id="f7734-161">nx_dhcpv6_client_delete</span><span class="sxs-lookup"><span data-stu-id="f7734-161">nx_dhcpv6_client_delete</span></span>

## <a name="nx_dhcpv6_client_delete"></a><span data-ttu-id="f7734-162">nx_dhcpv6_client_delete</span><span class="sxs-lookup"><span data-stu-id="f7734-162">nx_dhcpv6_client_delete</span></span>

<span data-ttu-id="f7734-163">DHCPv6 Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="f7734-163">Delete a DHCPv6 Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-164">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-164">Prototype</span></span>

```C
UINT nx_dhcpv6_client_delete(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-165">Description</span></span>

<span data-ttu-id="f7734-166">Bu hizmet, önceden oluşturulmuş bir DHCPv6 istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="f7734-166">This service deletes a previously created DHCPv6 client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-167">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-167">Input Parameters</span></span>

- <span data-ttu-id="f7734-168">**dhcpv6_ptr** DHCPv6 istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-168">**dhcpv6_ptr** Pointer to DHCPv6 client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-169">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-169">Return Values</span></span>

- <span data-ttu-id="f7734-170">**NX_SUCCESS** (0x00) başarılı DHCPv6 silme</span><span class="sxs-lookup"><span data-stu-id="f7734-170">**NX_SUCCESS** (0x00) Successful DHCPv6 deletion</span></span>

- <span data-ttu-id="f7734-171">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-171">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-172">NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-172">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-173">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-173">Allowed From</span></span>

<span data-ttu-id="f7734-174">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-174">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-175">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-175">Example</span></span>

```C
/* Delete a DHCPv6 client instance.  */
status =  nx_dhcpv6_client_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCPv6 client instance was successfully
   deleted.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-176">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-176">See Also</span></span>

- <span data-ttu-id="f7734-177">nx_dhcpv6_client_create</span><span class="sxs-lookup"><span data-stu-id="f7734-177">nx_dhcpv6_client_create</span></span>

## <a name="nx_dhcpv6_client_set_interface"></a><span data-ttu-id="f7734-178">nx_dhcpv6_client_set_interface</span><span class="sxs-lookup"><span data-stu-id="f7734-178">nx_dhcpv6_client_set_interface</span></span>

<span data-ttu-id="f7734-179">DHCPv6 için Istemcinin ağ arabirimini ayarlar</span><span class="sxs-lookup"><span data-stu-id="f7734-179">Sets Client’s Network Interface for DHCPv6</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-180">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-180">Prototype</span></span>

```C
UINT    nx_dhcpv6_client_set_interface(NX_DHCPV6 *dhcpv6_ptr, 
                                       UINT *interface_index);
```

### <a name="description"></a><span data-ttu-id="f7734-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-181">Description</span></span>

<span data-ttu-id="f7734-182">Bu hizmet, DHCPv6 sunucuları ile iletişim için Istemcinin ağ arabirimini belirtilen giriş arabirimi dizinine ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f7734-182">This service sets the Client’s network interface for communicating with the DHCPv6 Server(s) to the specified input interface index.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-183">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-183">Input Parameters</span></span>

- <span data-ttu-id="f7734-184">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-184">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-185">**interface_index** Ağ arabirimini belirten Dizin</span><span class="sxs-lookup"><span data-stu-id="f7734-185">**interface_index** Index indicating network interface</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-186">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-186">Return Values</span></span>

- <span data-ttu-id="f7734-187">**NX_SUCCESS** (0x00) arabirimi başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="f7734-187">**NX_SUCCESS** (0x00) Interface successfully set</span></span>

- <span data-ttu-id="f7734-188">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-188">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-189">NX_INVALID_INTERFACE (0x4C) geçersiz arabirim dizin girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-189">NX_INVALID_INTERFACE (0x4C) Invalid interface index input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-190">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-190">Allowed From</span></span>

<span data-ttu-id="f7734-191">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-192">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-192">Example</span></span>

```C
/* Set the client interface for DHCPv6 communication with the Server to 
   the secondary interface (1). */

UINT index = 1;
status = nx_dhcpv6_client_set_interface(&dhcp_0, index);

/* If status is NX_SUCCESS, the Client successfully set 
   the DHCPv6 network interface.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-193">See Also</span></span>

- <span data-ttu-id="f7734-194">nx_dhcpv6_client _create</span><span class="sxs-lookup"><span data-stu-id="f7734-194">nx_dhcpv6_client _create</span></span>
- <span data-ttu-id="f7734-195">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="f7734-195">nx_dhcpv6_start</span></span>

## <a name="nx_dhcpv6_client_set_destination_address"></a><span data-ttu-id="f7734-196">nx_dhcpv6_client_set_destination_address</span><span class="sxs-lookup"><span data-stu-id="f7734-196">nx_dhcpv6_client_set_destination_address</span></span>

<span data-ttu-id="f7734-197">DHCPv6 iletisinin gönderileceği hedef adresi ayarlar</span><span class="sxs-lookup"><span data-stu-id="f7734-197">Sets the destination address where DHCPv6 message should be sent to</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-198">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-198">Prototype</span></span>

```C
UINT nx_dhcpv6_client_set_destination_address(NX_DHCPV6 *dhcpv6_ptr,
                                              NXD_ADDRESS *destination_address);
```

### <a name="description"></a><span data-ttu-id="f7734-199">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-199">Description</span></span>

<span data-ttu-id="f7734-200">Bu hizmet, DHCPv6 iletisinin gönderileceği hedef adresi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f7734-200">This service sets the destination address where DHCPv6 message should be sent to.</span></span> <span data-ttu-id="f7734-201">Varsayılan olarak ALL_DHCP_Relay_Agents_and_Servers (FF02:: 1:2).</span><span class="sxs-lookup"><span data-stu-id="f7734-201">By default is ALL_DHCP_Relay_Agents_and_Servers(FF02::1:2).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-202">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-202">Input Parameters</span></span>

- <span data-ttu-id="f7734-203">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-203">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-204">**destination_address** Hedef adres</span><span class="sxs-lookup"><span data-stu-id="f7734-204">**destination_address** Destination address</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-205">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-205">Return Values</span></span>

- <span data-ttu-id="f7734-206">**NX_SUCCESS** (0x00) arabirimi başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="f7734-206">**NX_SUCCESS** (0x00) Interface successfully set</span></span>

- <span data-ttu-id="f7734-207">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-207">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-208">NX_DHCPV6_PARAM_ERROR (0xE93) parametre hatası</span><span class="sxs-lookup"><span data-stu-id="f7734-208">NX_DHCPV6_PARAM_ERROR (0xE93) Parament error</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-209">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-209">Allowed From</span></span>

<span data-ttu-id="f7734-210">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-210">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-211">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-211">Example</span></span>

```C
/* Set the destination address where DHCPv6 message should be sent to. */

NXD_ADDRESS dest_address; /* Set the destination address.  */

status = nx_dhcpv6_client_set_destination_address(&dhcp_0, &dest_address);

/* If status is NX_SUCCESS, the Client successfully set the destination address. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-212">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-212">See Also</span></span>

- <span data-ttu-id="f7734-213">nx_dhcpv6_client _create</span><span class="sxs-lookup"><span data-stu-id="f7734-213">nx_dhcpv6_client _create</span></span>
- <span data-ttu-id="f7734-214">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="f7734-214">nx_dhcpv6_start</span></span>

## <a name="nx_dhcpv6_create_client_duid"></a><span data-ttu-id="f7734-215">nx_dhcpv6_create_client_duid</span><span class="sxs-lookup"><span data-stu-id="f7734-215">nx_dhcpv6_create_client_duid</span></span>

<span data-ttu-id="f7734-216">Istemci DUıD nesnesi oluştur</span><span class="sxs-lookup"><span data-stu-id="f7734-216">Create Client DUID object</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-217">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-217">Prototype</span></span>

```C
UINT nx_dhcpv6_create_client_duid(NX_DHCPV6 *dhcpv6_ptr,
                                  UINT duid_type, UINT hardware_type,
                                  ULONG time);
```

### <a name="description"></a><span data-ttu-id="f7734-218">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-218">Description</span></span>

<span data-ttu-id="f7734-219">Bu hizmet, giriş parametreleriyle Istemci DUıD 'sini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f7734-219">This service creates the Client DUID with the input parameters.</span></span> <span data-ttu-id="f7734-220">Zaman girişi sağlanmazsa ve DUID türü bağlantı katmanını zamana göre gösteriyorsa, bu işlev benzersizlik için rastgele bir faktör içeren bir zaman sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7734-220">If the time input is not supplied and the duid type indicates link layer with time, this function will supply a time which includes a randomizing factor for uniqueness.</span></span> <span data-ttu-id="f7734-221">Satıcı atanmış (Kurumsal) DUID türleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f7734-221">Vendor assigned (enterprise) duid types are not supported.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-222">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-222">Input Parameters</span></span>

- <span data-ttu-id="f7734-223">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-223">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-224">**duid_type** DUıD türü (donanım, kuruluş vb.)</span><span class="sxs-lookup"><span data-stu-id="f7734-224">**duid_type** Type of DUID (hardware, enterprise etc)</span></span>

- <span data-ttu-id="f7734-225">**hardware_type** Ağ donanımı ör. IEEE 802</span><span class="sxs-lookup"><span data-stu-id="f7734-225">**hardware_type** Network hardware e.g. IEEE 802</span></span>

- <span data-ttu-id="f7734-226">**zaman** Benzersiz tanımlayıcı oluşturmak için kullanılan değer</span><span class="sxs-lookup"><span data-stu-id="f7734-226">**time** Value used in creating unique identifier</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-227">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-227">Return Values</span></span>

- <span data-ttu-id="f7734-228">**NX_SUCCESS** (0x00) başarılı istemci DUID 'si oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="f7734-228">**NX_SUCCESS** (0x00) Successful Client DUID created</span></span>

- <span data-ttu-id="f7734-229">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-229">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-230">NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-230">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

- <span data-ttu-id="f7734-231">NX_DHCPV6_UNSUPPORTED_DUID_TYPE (0xE98) DUıD türü bilinmiyor veya desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="f7734-231">NX_DHCPV6_UNSUPPORTED_DUID_TYPE (0xE98) DUID type unknown or not supported</span></span> 

- <span data-ttu-id="f7734-232">NX_DHCPV6_UNSUPPORTED_DUID_HW_TYPE (0xE99) DUıD donanım türü bilinmiyor veya desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="f7734-232">NX_DHCPV6_UNSUPPORTED_DUID_HW_TYPE (0xE99) DUID hardware type unknown or not supported</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-233">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-233">Allowed From</span></span>

<span data-ttu-id="f7734-234">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-234">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-235">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-235">Example</span></span>

```C
/* Create the Client DUID from the supplied input.
   The time field is left NULL so the DHCPv6 client will provide one.  */
status = nx_dhcpv6_create_client_duid(&dhcp_0, NX_DHCPV6_DUID_TYPE_LINK_TIME,
                                      NX_DHCPV6_HW_TYPE_IEEE_802, 0)

/* If status is NX_SUCCESS the client DUID was successfully created.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-236">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-236">See Also</span></span>

- <span data-ttu-id="f7734-237">nx_dhcpv6_create_client_ia</span><span class="sxs-lookup"><span data-stu-id="f7734-237">nx_dhcpv6_create_client_ia</span></span>
- <span data-ttu-id="f7734-238">nx_dhcpv6_create_client_iana</span><span class="sxs-lookup"><span data-stu-id="f7734-238">nx_dhcpv6_create_client_iana</span></span>
- <span data-ttu-id="f7734-239">nx_dhcpv6_create_server_duid</span><span class="sxs-lookup"><span data-stu-id="f7734-239">nx_dhcpv6_create_server_duid</span></span>

## <a name="nx_dhcpv6_create_client_ia"></a><span data-ttu-id="f7734-240">nx_dhcpv6_create_client_ia</span><span class="sxs-lookup"><span data-stu-id="f7734-240">nx_dhcpv6_create_client_ia</span></span>

<span data-ttu-id="f7734-241">Istemciye bir kimlik Ilişkilendirmesi ekleme</span><span class="sxs-lookup"><span data-stu-id="f7734-241">Add an Identity Association to the Client</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-242">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-242">Prototype</span></span>

```C
UINT nx_dhcpv6_create_client_ia(NX_DHCPV6 *dhcpv6_ptr,
                                NXD_ADDRESS *ipv6_address,
                                ULONG preferred_lifetime,
                                ULONG valid_lifetime);
```

### <a name="description"></a><span data-ttu-id="f7734-243">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-243">Description</span></span>

<span data-ttu-id="f7734-244">Bu hizmet *nx_dhcpv6_add_client_ia* hizmetiyle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="f7734-244">This service is identical to the *nx_dhcpv6_add_client_ia* service.</span></span> <span data-ttu-id="f7734-245">Istemci kaydını sağlanan parametrelerle doldurarak bir Istemci kimliği Ilişkilendirmesi ekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-245">It adds a Client Identity Association by filling in the Client record with the supplied parameters.</span></span> <span data-ttu-id="f7734-246">En fazla tercih edilen ve geçerli yaşam sürelerini istemek için, bu parametreleri sonsuz olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f7734-246">To request the maximum preferred and valid lifetimes, set these parameters to infinity.</span></span> <span data-ttu-id="f7734-247">Bir DHCPv6 Istemcisine birden fazla IA eklemek için NX_DHCPV6_MAX_IA_ADDRESS varsayılan değer olan 1 ' den daha yüksek bir değere ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f7734-247">To add more than one IA to a DHCPv6 Client, set the NX_DHCPV6_MAX_IA_ADDRESS to a value higher than the default value of 1.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-248">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-248">Input Parameters</span></span>

- <span data-ttu-id="f7734-249">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-249">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-250">**ipv6_address** NetX Duo IP adres bloğunun işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-250">**ipv6_address** Pointer to NetX Duo IP address block</span></span>

- <span data-ttu-id="f7734-251">**preferred_lifetime** IP adresi kullanım dışı olmadan önce geçen sürenin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="f7734-251">**preferred_lifetime** Length of time before IP address is deprecated</span></span>

- <span data-ttu-id="f7734-252">**valid_lifetime** IP adresinin süresi dolmadan önce geçen süre</span><span class="sxs-lookup"><span data-stu-id="f7734-252">**valid_lifetime** Length of time before IP address is expired</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-253">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-253">Return Values</span></span>

- <span data-ttu-id="f7734-254">**NX_SUCCESS** (0x00) başarılı istemci IA eklendi</span><span class="sxs-lookup"><span data-stu-id="f7734-254">**NX_SUCCESS** (0x00) Successful Client IA added</span></span>

- <span data-ttu-id="f7734-255">**NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xeaf) yinelenen IA adresi</span><span class="sxs-lookup"><span data-stu-id="f7734-255">**NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xEAF) Duplicate IA address</span></span> 

- <span data-ttu-id="f7734-256">**NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0xeae) IA, en fazla IAS istemcisinin depolayabileceği sınırı aşıyor</span><span class="sxs-lookup"><span data-stu-id="f7734-256">**NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0xEAE) IA exceeds the max IAs Client can store</span></span>

- <span data-ttu-id="f7734-257">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-257">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-258">NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) IA 'da geçersiz (örn. null) IA adresi</span><span class="sxs-lookup"><span data-stu-id="f7734-258">NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) Invalid (e.g. null) IA address in IA</span></span>

- <span data-ttu-id="f7734-259">NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-259">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>


### <a name="allowed-from"></a><span data-ttu-id="f7734-260">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-260">Allowed From</span></span>

<span data-ttu-id="f7734-261">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-261">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-262">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-262">Example</span></span>

```C
/* Add an Client IA using the supplied input.   */
status = nx_dhcpv6_create_client_ia(&dhcp_0, &ipv6_address, 
NX_DHCPV6_PREFERRED_LIFETIME, NX_DHCPV6_VALID_LIFETIME);

/* If status is NX_SUCCESS the client IA was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-263">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-263">See Also</span></span>

- <span data-ttu-id="f7734-264">nx_dhcpv6_add_client_duid</span><span class="sxs-lookup"><span data-stu-id="f7734-264">nx_dhcpv6_add_client_duid</span></span>
- <span data-ttu-id="f7734-265">nx_dhcpv6_create_server_duid</span><span class="sxs-lookup"><span data-stu-id="f7734-265">nx_dhcpv6_create_server_duid</span></span>
- <span data-ttu-id="f7734-266">nx_dhcpv6_create_client_iana</span><span class="sxs-lookup"><span data-stu-id="f7734-266">nx_dhcpv6_create_client_iana</span></span>

## <a name="nx_dhcpv6_create_client_iana"></a><span data-ttu-id="f7734-267">nx_dhcpv6_create_client_iana</span><span class="sxs-lookup"><span data-stu-id="f7734-267">nx_dhcpv6_create_client_iana</span></span>

<span data-ttu-id="f7734-268">Istemci için bir kimlik Ilişkisi (geçici olmayan) oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7734-268">Create an Identity Association (Non Temporary) for the Client</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-269">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-269">Prototype</span></span>

```C
UINT nx_dhcpv6_create_client_iana(NX_DHCPV6 *dhcpv6_ptr, 
                                  UINT IA_ident, ULONG T1, ULONG T2);
```

### <a name="description"></a><span data-ttu-id="f7734-270">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-270">Description</span></span>

<span data-ttu-id="f7734-271">Bu hizmet, sağlanan parametrelerden geçici olmayan bir Istemci kimlik Ilişkisi (ıANA) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f7734-271">This service creates a Client Non Temporary Identity Association (IANA) from the supplied parameters.</span></span> <span data-ttu-id="f7734-272">T1 ve T2 sürelerini DHCPv6 Istemci isteklerinde maksimum (Infinity) olarak ayarlamak için, bu parametreleri NX_DHCPV6_INFINITE_LEASE olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f7734-272">To set the T1 and T2 times to maximum (infinity) in the DHCPv6 Client requests, set these parameters to NX_DHCPV6_INFINITE_LEASE.</span></span> 

> [!NOTE]
> <span data-ttu-id="f7734-273">Bir Istemcide yalnızca bir ıANA vardır.</span><span class="sxs-lookup"><span data-stu-id="f7734-273">A Client has only one IANA.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-274">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-274">Input Parameters</span></span>

- <span data-ttu-id="f7734-275">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-275">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-276">**IA_ident** Kimlik Ilişkilendirmesi benzersiz tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="f7734-276">**IA_ident** Identity Association unique identifier</span></span>

- <span data-ttu-id="f7734-277">**T1** Istemci, IPv6 adresi yenilemeyi başlatması gereken zaman</span><span class="sxs-lookup"><span data-stu-id="f7734-277">**T1** When the Client must start the IPv6 address renewal</span></span>

- <span data-ttu-id="f7734-278">**T2** Istemci theIPv6 adresi yeniden bağlama başlatması gereken zaman</span><span class="sxs-lookup"><span data-stu-id="f7734-278">**T2** When the Client must start theIPv6 address rebinding</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-279">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-279">Return Values</span></span>

- <span data-ttu-id="f7734-280">**NX_SUCCESS** (0x00) IANA başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="f7734-280">**NX_SUCCESS** (0x00) Successfully created the IANA</span></span>

- <span data-ttu-id="f7734-281">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-281">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-282">NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-282">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-283">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-283">Allowed From</span></span>

<span data-ttu-id="f7734-284">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-284">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-285">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-285">Example</span></span>

```C
/* Create the Client IANA from the supplied input.  */
status = nx_dhcpv6_create_client_iana(&dhcp_0, DHCPV6_IA_ID, DHCPV6_T1,   
                                      DHCPV6_T2);

/* If status is NX_SUCCESS the client IANA was successfully created.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-286">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-286">See Also</span></span>

- <span data-ttu-id="f7734-287">nx_dhcpv6_create_client_duid</span><span class="sxs-lookup"><span data-stu-id="f7734-287">nx_dhcpv6_create_client_duid</span></span>
- <span data-ttu-id="f7734-288">nx_dhcpv6_create_server_duid</span><span class="sxs-lookup"><span data-stu-id="f7734-288">nx_dhcpv6_create_server_duid</span></span>
- <span data-ttu-id="f7734-289">nx_dhcpv6_add_client_ia</span><span class="sxs-lookup"><span data-stu-id="f7734-289">nx_dhcpv6_add_client_ia</span></span>

## <a name="nx_dhcpv6_add_client_ia"></a><span data-ttu-id="f7734-290">nx_dhcpv6_add_client_ia</span><span class="sxs-lookup"><span data-stu-id="f7734-290">nx_dhcpv6_add_client_ia</span></span> 

<span data-ttu-id="f7734-291">Istemciye bir kimlik Ilişkilendirmesi ekleme</span><span class="sxs-lookup"><span data-stu-id="f7734-291">Add an Identity Association to the Client</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-292">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-292">Prototype</span></span>

```C
UINT nx_dhcpv6_add_client_ia(NX_DHCPV6 *dhcpv6_ptr, 
                             NXD_ADDRESS *ipv6_address, 
                             ULONG preferred_lifetime, 
                             ULONG valid_lifetime);
```

### <a name="description"></a><span data-ttu-id="f7734-293">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-293">Description</span></span>

<span data-ttu-id="f7734-294">Bu hizmet, Istemci kaydını sağlanan parametrelerle doldurarak bir Istemci kimliği Ilişkilendirmesi ekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-294">This service adds a Client Identity Association by filling in the Client record with the supplied parameters.</span></span> <span data-ttu-id="f7734-295">En fazla tercih edilen ve geçerli yaşam sürelerini istemek için, bu parametreleri sonsuz olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f7734-295">To request the maximum preferred and valid lifetimes, set these parameters to infinity.</span></span> <span data-ttu-id="f7734-296">Bir DHCPv6 Istemcisine birden fazla IA eklemek için NX_DHCPV6_MAX_IA_ADDRESS varsayılan değer olan 1 ' den daha yüksek bir değere ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f7734-296">To add more than one IA to a DHCPv6 Client, set the NX_DHCPV6_MAX_IA_ADDRESS to a value higher than the default value of 1.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-297">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-297">Input Parameters</span></span>

- <span data-ttu-id="f7734-298">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-298">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-299">**ipv6_address** NetX Duo IP adres bloğunun işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-299">**ipv6_address** Pointer to NetX Duo IP address block</span></span>

- <span data-ttu-id="f7734-300">**preferred_lifetime** IP adresi kullanım dışı olmadan önce geçen sürenin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="f7734-300">**preferred_lifetime** Length of time before IP address is deprecated</span></span>

- <span data-ttu-id="f7734-301">**valid_lifetime** IP adresinin süresi dolmadan önce geçen süre</span><span class="sxs-lookup"><span data-stu-id="f7734-301">**valid_lifetime** Length of time before IP address is expired</span></span> 

### <a name="return-values"></a><span data-ttu-id="f7734-302">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-302">Return Values</span></span>

- <span data-ttu-id="f7734-303">**NX_SUCCESS** (0x00) başarılı istemci IA eklendi</span><span class="sxs-lookup"><span data-stu-id="f7734-303">**NX_SUCCESS** (0x00) Successful Client IA added</span></span>

- <span data-ttu-id="f7734-304">**NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xeaf) yinelenen IA adresi</span><span class="sxs-lookup"><span data-stu-id="f7734-304">**NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xEAF) Duplicate IA address</span></span> 

- <span data-ttu-id="f7734-305">**NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0xeae) IA, en fazla IAS istemcisinin depolayabileceği sınırı aşıyor</span><span class="sxs-lookup"><span data-stu-id="f7734-305">**NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0xEAE) IA exceeds the max IAs Client can store</span></span>

- <span data-ttu-id="f7734-306">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-306">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-307">NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) IA 'da geçersiz (örn. null) IA adresi</span><span class="sxs-lookup"><span data-stu-id="f7734-307">NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) Invalid (e.g. null) IA address in IA</span></span>

- <span data-ttu-id="f7734-308">NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-308">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

 
### <a name="allowed-from"></a><span data-ttu-id="f7734-309">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-309">Allowed From</span></span>

<span data-ttu-id="f7734-310">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-310">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-311">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-311">Example</span></span>

```C
/* Add an Client IA using the supplied input.   */
status = nx_dhcpv6_add_client_ia(&dhcp_0, &ipv6_address, 
                                 NX_DHCPV6_PREFERRED_LIFETIME,
                                 NX_DHCPV6_VALID_LIFETIME);

/* If status is NX_SUCCESS the client IA was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-312">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-312">See Also</span></span>

- <span data-ttu-id="f7734-313">nx_dhcpv6_create_client_duid</span><span class="sxs-lookup"><span data-stu-id="f7734-313">nx_dhcpv6_create_client_duid</span></span>
- <span data-ttu-id="f7734-314">nx_dhcpv6_create_server_duid</span><span class="sxs-lookup"><span data-stu-id="f7734-314">nx_dhcpv6_create_server_duid</span></span>
- <span data-ttu-id="f7734-315">nx_dhcpv6_create_client_iana</span><span class="sxs-lookup"><span data-stu-id="f7734-315">nx_dhcpv6_create_client_iana</span></span>

## <a name="nx_dhcpv6_get_client_duid_time_id"></a><span data-ttu-id="f7734-316">nx_dhcpv6_get_client_duid_time_id</span><span class="sxs-lookup"><span data-stu-id="f7734-316">nx_dhcpv6_get_client_duid_time_id</span></span>

<span data-ttu-id="f7734-317">Istemci DUıD 'sinden saat KIMLIĞINI alır</span><span class="sxs-lookup"><span data-stu-id="f7734-317">Retrieves time ID from Client DUID</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-318">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-318">Prototype</span></span>

```C
UINT nx_dhcpv6_get_client_duid_time_id(NX_DHCPV6 *dhcpv6_ptr, ULONG *time_id);
```

### <a name="description"></a><span data-ttu-id="f7734-319">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-319">Description</span></span>

<span data-ttu-id="f7734-320">Bu hizmet, Istemci DUıD 'sinden saat KIMLIĞI alanını alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-320">This service retrieves the time ID field from the Client DUID.</span></span> <span data-ttu-id="f7734-321">Uygulamanın, DHCPv6 Istemci örneğindeki Istemci DUıD 'sini doldurması için *nx_dhcpv6_create_client_duid* çağrısı olması veya bu alan için null değere sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7734-321">If the application must first call *nx_dhcpv6_create_client_duid*, to fill in the Client DUID in the DHCPv6 Client instance or it will have a null value for this field.</span></span> <span data-ttu-id="f7734-322">Amaç, uygulamanın bu verileri kaydetmesi ve zaman alanı da dahil olmak üzere sunucuya aynı Istemci DUıD 'sini sunmaktır.</span><span class="sxs-lookup"><span data-stu-id="f7734-322">The intent is for the application to save this data and present the same Client DUID to the server, including the time field, across reboots.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-323">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-323">Input Parameters</span></span>

- <span data-ttu-id="f7734-324">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-324">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-325">**time_id** Istemci DUıD saat alanı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-325">**time_id** Pointer to Client DUID time field</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-326">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-326">Return Values</span></span>

- <span data-ttu-id="f7734-327">**NX_SUCCESS** (0x00) IP Kiralama verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-327">**NX_SUCCESS** (0x00) IP lease data successfully retrieved</span></span>

- <span data-ttu-id="f7734-328">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-328">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-329">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-329">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-330">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-330">Allowed From</span></span>

<span data-ttu-id="f7734-331">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-331">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-332">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-332">Example</span></span>

```C
/* Retrieve the time ID from the Client DUID.  */
status = nx_dhcpv6_get_client_duid_time_id(&dhcp_0, &time_ID);

/* If status is NX_SUCCESS the time ID was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-333">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-333">See Also</span></span>

- <span data-ttu-id="f7734-334">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-334">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="f7734-335">nx_dhcpv6_get_time_lease_data</span><span class="sxs-lookup"><span data-stu-id="f7734-335">nx_dhcpv6_get_time_lease_data</span></span>
- <span data-ttu-id="f7734-336">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="f7734-336">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="f7734-337">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-337">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_get_ip_address"></a><span data-ttu-id="f7734-338">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-338">nx_dhcpv6_get_IP_address</span></span>

<span data-ttu-id="f7734-339">Istemcinin genel IPv6 adresini alır</span><span class="sxs-lookup"><span data-stu-id="f7734-339">Retrieves Client’s global IPv6 address</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-340">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-340">Prototype</span></span>

```C
UINT nx_dhcpv6_get_IP_address(NX_DHCPV6 *dhcpv6_ptr, 
                              NXD_ADDRESS *ip_address);
```

### <a name="description"></a><span data-ttu-id="f7734-341">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-341">Description</span></span>

<span data-ttu-id="f7734-342">Bu hizmet, Istemcinin genel IPv6 adresini alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-342">This service retrieves the Client’s global IPv6 address.</span></span> <span data-ttu-id="f7734-343">Istemcinin geçerli bir adresi yoksa bir hata durumu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-343">If the Client does not have a valid address, an error status is returned.</span></span> <span data-ttu-id="f7734-344">Bir Istemcide birden fazla genel IPv6 adresi varsa, birincil IPv6 adresi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-344">If a Client has more than one global IPv6 address, the primary IPv6 address is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-345">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-345">Input Parameters</span></span>

- <span data-ttu-id="f7734-346">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-346">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-347">**ip_address** IPv6 adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-347">**ip_address** Pointer to IPv6 address</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-348">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-348">Return Values</span></span>

- <span data-ttu-id="f7734-349">**NX_SUCCESS** (0x00) IPv6 adresi başarıyla atandı</span><span class="sxs-lookup"><span data-stu-id="f7734-349">**NX_SUCCESS** (0x00) IPv6 address successfully assigned</span></span>

- <span data-ttu-id="f7734-350">**NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xead) IPv6 adresi geçerli değil</span><span class="sxs-lookup"><span data-stu-id="f7734-350">**NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) IPv6 address is not valid</span></span>

- <span data-ttu-id="f7734-351">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-351">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-352">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-352">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-353">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-353">Allowed From</span></span>

<span data-ttu-id="f7734-354">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-354">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-355">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-355">Example</span></span>

```C
UINT address_status;
UINT address_index;

/* Retrieve the client’s assigned IP address.  */
status = nx_dhcpv6_get_IP_address(&dhcp_0, &ipv6_address);

/* If status is NX_SUCCESS the client IP address was assigned.
   Now register it with NetX Duo on the primary interface (index zero). 
   The address index is returned in the address_index field*/
status = nxd_ipv6_address_set(&ip_0, 0, &ipv6_address, 64, &address_index);
```

### <a name="see-also"></a><span data-ttu-id="f7734-356">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-356">See Also</span></span>

- <span data-ttu-id="f7734-357">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="f7734-357">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="f7734-358">nx_dhcpv6_get_client_duid_time_id</span><span class="sxs-lookup"><span data-stu-id="f7734-358">nx_dhcpv6_get_client_duid_time_id</span></span>
- <span data-ttu-id="f7734-359">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="f7734-359">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="f7734-360">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-360">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_get_lease_time_data"></a><span data-ttu-id="f7734-361">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="f7734-361">nx_dhcpv6_get_lease_time_data</span></span>

<span data-ttu-id="f7734-362">Istemcinin IA adresi kiralama süresi verilerini alır</span><span class="sxs-lookup"><span data-stu-id="f7734-362">Retrieves Client’s IA address lease time data</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-363">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-363">Prototype</span></span>

```C
UINT nx_dhcpv6_get_lease_time_data(NX_DHCPV6 *dhcpv6_ptr, ULONG *T1, 
                                   ULONG *T2, ULONG *preferred_lifetime, 
                                   ULONG *valid_lifetime);
```

### <a name="description"></a><span data-ttu-id="f7734-364">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-364">Description</span></span>

<span data-ttu-id="f7734-365">Bu hizmet, Istemcinin genel IA adres saat verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-365">This service retrieves the Client’s global IA address time data.</span></span> <span data-ttu-id="f7734-366">Istemci IA adresi durumu geçersizse, zaman verileri sıfır olarak ayarlanır ve başarılı bir tamamlanma durumu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-366">If the Client IA address status is invalid, time data is set to zero and a successful completion status is returned.</span></span> <span data-ttu-id="f7734-367">Bir Istemcide birden fazla genel IPv6 adresi varsa, birincil IA adres verileri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-367">If a Client has more than one global IPv6 address, the primary IA address data is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-368">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-368">Input Parameters</span></span>

- <span data-ttu-id="f7734-369">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-369">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-370">**T1** IA adres yenileme zamanı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-370">**T1** Pointer to IA address renew time</span></span>

- <span data-ttu-id="f7734-371">**T2** IA adresi yeniden bağlama saati işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-371">**T2** Pointer to IA address rebind time</span></span>

- <span data-ttu-id="f7734-372">**preferred_lifetime** IA adresinin kullanım dışı olduğu zaman işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-372">**preferred_lifetime** Pointer to time when IA address is deprecated</span></span>

- <span data-ttu-id="f7734-373">**valid_lifetime** IA adresinin süresi dolduğunda zaman işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-373">**valid_lifetime** Pointer to time when IA address is expired</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-374">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-374">Return Values</span></span>

- <span data-ttu-id="f7734-375">**NX_SUCCESS** (0x00) IA kira verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-375">**NX_SUCCESS** (0x00) IA lease data successfully retrieved</span></span>

- <span data-ttu-id="f7734-376">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-376">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-377">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-377">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-378">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-378">Allowed From</span></span>

<span data-ttu-id="f7734-379">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-379">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-380">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-380">Example</span></span>

```C
/* Retrieve the client’s assigned IA lease data.  */
status = nx_dhcpv6_get_lease_time_data(&dhcp_0, &T1, &T2, &preferred_lifetime, 
                                       &valid_lifetime);

/* If status is NX_SUCCESS the client IA address lease data was retrieved.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-381">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-381">See Also</span></span>

- <span data-ttu-id="f7734-382">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-382">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="f7734-383">nx_dhcpv6_get_client_duid_time_id</span><span class="sxs-lookup"><span data-stu-id="f7734-383">nx_dhcpv6_get_client_duid_time_id</span></span>
- <span data-ttu-id="f7734-384">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="f7734-384">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="f7734-385">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-385">nx_dhcpv6_get_time_accrued</span></span>
- <span data-ttu-id="f7734-386">nx_dhcpv6_get_iana_lease_time</span><span class="sxs-lookup"><span data-stu-id="f7734-386">nx_dhcpv6_get_iana_lease_time</span></span>

## <a name="nx_dhcpv6_get_iana-lease_time"></a><span data-ttu-id="f7734-387">nx_dhcpv6_get_iana lease_time</span><span class="sxs-lookup"><span data-stu-id="f7734-387">nx_dhcpv6_get_iana lease_time</span></span>

<span data-ttu-id="f7734-388">Istemcinin ıANA kira süresi verilerini alma</span><span class="sxs-lookup"><span data-stu-id="f7734-388">Retrieve the Client’s IANA lease time data</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-389">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-389">Prototype</span></span>

```C
UINT nx_dhcpv6_get_iana_lease_time(NX_DHCPV6 *dhcpv6_ptr, ULONG *T1, 
                                    ULONG *T2);
```

### <a name="description"></a><span data-ttu-id="f7734-390">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-390">Description</span></span>

<span data-ttu-id="f7734-391">Bu hizmet, Istemcinin Global IA-NA kira süresi verilerini (T1 ve T2) alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-391">This service retrieves the Client’s global IA-NA lease time data (T1 and T2).</span></span> <span data-ttu-id="f7734-392">Hiçbir Istemci IA-yok adresinin geçerli bir adres durumu yoksa, zaman verileri sıfır olarak ayarlanır ve başarılı bir tamamlanma durumu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-392">If none of the Client IA-NA addresses have a valid address status, time data is set to zero and a successful completion status is returned.</span></span> <span data-ttu-id="f7734-393">Bir Istemcide birden fazla genel IPv6 adresi varsa, birincil IA adres verileri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-393">If a Client has more than one global IPv6 address, the primary IA address data is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-394">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-394">Input Parameters</span></span>

- <span data-ttu-id="f7734-395">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-395">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-396">**T1** Kira yenilemesi başlatmak için zaman işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-396">**T1** Pointer to time for starting lease renewal</span></span>

- <span data-ttu-id="f7734-397">**T2** Kira yeniden bağlamasının başlaması için zaman işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-397">**T2** Pointer to time for starting lease rebinding</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-398">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-398">Return Values</span></span>

- <span data-ttu-id="f7734-399">**NX_SUCCESS** (0x00) IANA kira verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-399">**NX_SUCCESS** (0x00) IANA lease data successfully retrieved</span></span>

- <span data-ttu-id="f7734-400">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-400">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-401">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-401">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-402">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-402">Allowed From</span></span>

<span data-ttu-id="f7734-403">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-403">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-404">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-404">Example</span></span>

```C
/* Retrieve the client’s assigned IANA lease data.  */
status = nx_dhcpv6_get_iana_lease_time(&dhcp_0, &T1, &T2);

/* If status is NX_SUCCESS the client IA address lease data was retrieved.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-405">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-405">See Also</span></span>

- <span data-ttu-id="f7734-406">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-406">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="f7734-407">nx_dhcpv6_get_client_duid_time_id</span><span class="sxs-lookup"><span data-stu-id="f7734-407">nx_dhcpv6_get_client_duid_time_id</span></span>
- <span data-ttu-id="f7734-408">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="f7734-408">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="f7734-409">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-409">nx_dhcpv6_get_time_accrued</span></span>
- <span data-ttu-id="f7734-410">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="f7734-410">nx_dhcpv6_get_lease_time_data</span></span>

## <a name="nx_dhcpv6_get_valid_ip_address_count"></a><span data-ttu-id="f7734-411">nx_dhcpv6_get_valid_ip_address_count</span><span class="sxs-lookup"><span data-stu-id="f7734-411">nx_dhcpv6_get_valid_ip_address_count</span></span>

<span data-ttu-id="f7734-412">Istemcinin geçerli IA adresleri sayısını alma</span><span class="sxs-lookup"><span data-stu-id="f7734-412">Retrieve a count of Client’s valid IA addresses</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-413">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-413">Prototype</span></span>

```C
UINT nx_dhcpv6_get_valid_ip_address_count(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT *address_count);
```

### <a name="description"></a><span data-ttu-id="f7734-414">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-414">Description</span></span>

<span data-ttu-id="f7734-415">Bu hizmet, Istemcinin geçerli IPv6 adreslerinin sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-415">This service retrieves the count of the Client’s valid IPv6 addresses.</span></span> <span data-ttu-id="f7734-416">Istemciye geçerli bir IPv6 adresi (atandı) bağlanır ve IP örneğiyle kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f7734-416">A valid IPv6 address is bound (assigned) to the Client and registered with the IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-417">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-417">Input Parameters</span></span>

- <span data-ttu-id="f7734-418">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-418">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-419">**address_count** Döndürülecek adres sayısı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-419">**address_count** Pointer to address count to return</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-420">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-420">Return Values</span></span>

- <span data-ttu-id="f7734-421">**NX_SUCCESS** (0x00) IANA kira verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-421">**NX_SUCCESS** (0x00) IANA lease data successfully retrieved</span></span>

- <span data-ttu-id="f7734-422">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-422">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-423">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-423">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-424">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-424">Allowed From</span></span>

<span data-ttu-id="f7734-425">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-425">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-426">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-426">Example</span></span>

```C
UINT address_count; 

/* Retrieve the count of valid IA-NA addresses.  */
status = nx_dhcpv6_get_valid_ip_address_count(&dhcp_0, &address_count);

/* If status is NX_SUCCESS the client IA address count was retrieved.  */
```

## <a name="nx_dhcpv6_get_valid_ip_address_lease_time"></a><span data-ttu-id="f7734-427">nx_dhcpv6_get_valid_ip_address_lease_time</span><span class="sxs-lookup"><span data-stu-id="f7734-427">nx_dhcpv6_get_valid_ip_address_lease_time</span></span>

<span data-ttu-id="f7734-428">Istemci IA verilerini adres dizinine göre al</span><span class="sxs-lookup"><span data-stu-id="f7734-428">Retrieve the Client IA data by address index</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-429">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-429">Prototype</span></span>

```C
UINT nx_dhcpv6_get_valid_ip_address_lease_time(NX_DHCPV6 *dhcpv6_ptr, 
                                               UINT address_index,
                                               NXD_ADDRESS *ip_address,
                                               ULONG *preferred_lifetime,
                                               ULONG *valid_lifetime);
```

### <a name="description"></a><span data-ttu-id="f7734-430">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-430">Description</span></span>

<span data-ttu-id="f7734-431">Bu hizmet, Istemcinin IA adresini ve kira verilerini adres dizinine göre alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-431">This service retrieves the Client’s IA address and lease data by address index.</span></span> <span data-ttu-id="f7734-432">Geçersiz bir dizin sağlanırsa veya bu dizindeki IPv6 adresi geçerli değilse, hizmet NX_DHCPV6_IA_ADDRESS_NOT_VALID bir hata durumu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f7734-432">If an invalid index is supplied, or the IPv6 address at that index is not valid, the service returns an NX_DHCPV6_IA_ADDRESS_NOT_VALID error status.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-433">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-433">Input Parameters</span></span>

- <span data-ttu-id="f7734-434">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-434">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-435">**address_index** DHCPv6 IA tablosuna Dizin</span><span class="sxs-lookup"><span data-stu-id="f7734-435">**address_index** Index into DHCPv6 IA table</span></span>

- <span data-ttu-id="f7734-436">**ip_address** Alınacak IPv6 adresine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="f7734-436">**ip_address** Pointer to IPv6 address to retrieve</span></span>

- <span data-ttu-id="f7734-437">**preferred_lifetime** IA adresinin kullanım dışı olduğu zaman işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-437">**preferred_lifetime** Pointer to time when IA address is deprecated</span></span>

- <span data-ttu-id="f7734-438">**valid_lifetime** IA adresinin süresi dolduğunda zaman işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-438">**valid_lifetime** Pointer to time when IA address is expired</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-439">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-439">Return Values</span></span>

- <span data-ttu-id="f7734-440">**NX_SUCCESS** (0x00) IANA verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-440">**NX_SUCCESS** (0x00) IANA data successfully retrieved</span></span>

- <span data-ttu-id="f7734-441">Belirtilen dizinde geçersiz bir dizin veya geçerli bir IPv6 adresi **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xead)</span><span class="sxs-lookup"><span data-stu-id="f7734-441">**NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) An invalid index or no valid IPv6 address at the supplied index</span></span> 

- <span data-ttu-id="f7734-442">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-442">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-443">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-443">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-444">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-444">Allowed From</span></span>

<span data-ttu-id="f7734-445">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-445">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-446">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-446">Example</span></span>

```C
UINT address_index = 1; 
NXD_ADDRESS *ip_address;

/* Retrieve the IPv6 address, and valid and preferred lifetime for the IA record
   Saved at index 1 in the DHCPv6 table.  */
status = nx_dhcpv6_get_valid_ip_address_lease_time(&dhcp_0, address_index, 
                                                   &ip_address, 
                                                   &preferred_lifetime,  
                                                   &valid_lifetime);

/* If status is NX_SUCCESS the client IA address and lease data were retrieved.  */
```

### <a name="see-also"></a><span data-ttu-id="f7734-447">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-447">See Also</span></span>

- <span data-ttu-id="f7734-448">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-448">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="f7734-449">nx_dhcpv6_get_iana_lease_time</span><span class="sxs-lookup"><span data-stu-id="f7734-449">nx_dhcpv6_get_iana_lease_time</span></span>
- <span data-ttu-id="f7734-450">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="f7734-450">nx_dhcpv6_get_lease_time_data</span></span>

## <a name="nx_dhcpv6_get_dns_server_address"></a><span data-ttu-id="f7734-451">nx_dhcpv6_get_DNS_server_address</span><span class="sxs-lookup"><span data-stu-id="f7734-451">nx_dhcpv6_get_DNS_server_address</span></span>

<span data-ttu-id="f7734-452">DNS sunucusu adresini alır</span><span class="sxs-lookup"><span data-stu-id="f7734-452">Retrieves DNS Server address</span></span> 

### <a name="prototype"></a><span data-ttu-id="f7734-453">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-453">Prototype</span></span>

```C
UINT nx_dhcpv6_get_DNS_server_address(NX_DHCPV6 *dhcpv6_ptr, UINT index,
                                      NXD_ADDRESS *server_address);
```

### <a name="description"></a><span data-ttu-id="f7734-454">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-454">Description</span></span>

<span data-ttu-id="f7734-455">Bu hizmet, Istemci listesinde belirtilen dizindeki DNS sunucusu IPv6 adresi verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-455">This service retrieves the DNS server IPv6 address data at the specified index in the Client list.</span></span> <span data-ttu-id="f7734-456">Listede dizin üzerinde bir sunucu adresi yoksa bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-456">If the list does not contain a server address at the index, an error is returned.</span></span> <span data-ttu-id="f7734-457">Dizin, DNS sunucusu listesinin boyutunu aşmayabilir NX_DHCPV6_NUM_DNS_SERVERS Kullanıcı tarafından yapılandırılabilir seçeneği ile belirtilir.</span><span class="sxs-lookup"><span data-stu-id="f7734-457">The index may not exceed the size of the DNS Server list is specified by the user configurable option NX_DHCPV6_NUM_DNS_SERVERS.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-458">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-458">Input Parameters</span></span>

- <span data-ttu-id="f7734-459">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-459">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-460">**Dizin** DNS sunucusu listesinde Dizin</span><span class="sxs-lookup"><span data-stu-id="f7734-460">**index** Index into the DNS Server list</span></span>

- <span data-ttu-id="f7734-461">**server_address** Sunucu adresi arabelleği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-461">**server_address** Pointer to Server address buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-462">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-462">Return Values</span></span>

- <span data-ttu-id="f7734-463">**NX_SUCCESS** (0x00) adresi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-463">**NX_SUCCESS** (0x00) Address successfully retrieved</span></span>

- <span data-ttu-id="f7734-464">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-464">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-465">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-465">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-466">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-466">Allowed From</span></span>

<span data-ttu-id="f7734-467">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-467">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-468">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-468">Example</span></span>

```C
/* Retrieve the DNS server at the specified index in the list. */

UINT index = 0;
NXD_ADDRESS server_address;


        status = nx_dhcpv6_get_DNS_server_address(&dhcp_0, index, &server_address);

/* If status == NX_SUCCESS, the DNS server IP address successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-469">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-469">See Also</span></span>

- <span data-ttu-id="f7734-470">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-470">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="f7734-471">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="f7734-471">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="f7734-472">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-472">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_get_other_option_data"></a><span data-ttu-id="f7734-473">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="f7734-473">nx_dhcpv6_get_other_option_data</span></span>

<span data-ttu-id="f7734-474">DHCPv6 seçenek verilerini alır</span><span class="sxs-lookup"><span data-stu-id="f7734-474">Retrieves DHCPv6 option data</span></span> 

### <a name="prototype"></a><span data-ttu-id="f7734-475">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-475">Prototype</span></span>

```C
UINT  nx_dhcpv6_get_other_option_data(NX_DHCPV6 *dhcpv6_ptr, 
                                      UINT option_code, UCHAR *buffer);
```

### <a name="description"></a><span data-ttu-id="f7734-476">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-476">Description</span></span>

<span data-ttu-id="f7734-477">Bu hizmet, belirtilen seçenek kodu için DHCPv6 iletisinden DHCPv6 seçenek verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-477">This service retrieves DHCPv6 option data from a DHCPv6 message for the specified option code.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-478">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-478">Input Parameters</span></span>

- <span data-ttu-id="f7734-479">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-479">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-480">alınacak veriler için **seçenek** kodu seçenek kodu</span><span class="sxs-lookup"><span data-stu-id="f7734-480">**option** code Option code for which data to retrieve</span></span>

- <span data-ttu-id="f7734-481">**arabellek** Verilerin kopyalanacağı arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-481">**buffer** Pointer to buffer to copy data to</span></span> 

### <a name="return-values"></a><span data-ttu-id="f7734-482">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-482">Return Values</span></span>

- <span data-ttu-id="f7734-483">**NX_SUCCESS** (0x00) seçenek verileri başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-483">**NX_SUCCESS** (0x00) Option data successfully retrieved</span></span>

- <span data-ttu-id="f7734-484">**NX_DHCPV6_UNKNOWN_OPTION** (0xeab) bilinmeyen/desteklenmeyen seçenek kodu</span><span class="sxs-lookup"><span data-stu-id="f7734-484">**NX_DHCPV6_UNKNOWN_OPTION** (0xEAB) Unknown/unsupported option code</span></span>

- <span data-ttu-id="f7734-485">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-485">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-486">NX_DHCPV6_PARAM_ERROR (0xE93) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-486">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

- <span data-ttu-id="f7734-487">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-487">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-488">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-488">Allowed From</span></span>

<span data-ttu-id="f7734-489">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-489">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-490">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-490">Example</span></span>

```C
/* Retrieve the option data specified by the input option code. */
status = nx_dhcpv6_get_other_option_data(&dhcp_0, option_code, buffer);

/* If status is NX_SUCCESS the option data was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-491">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-491">See Also</span></span>

- <span data-ttu-id="f7734-492">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-492">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="f7734-493">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="f7734-493">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="f7734-494">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-494">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_get_time_accrued"></a><span data-ttu-id="f7734-495">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-495">nx_dhcpv6_get_time_accrued</span></span>

<span data-ttu-id="f7734-496">Istemcinin IP adresi kiralamasında tahakkuk eden süreyi alır</span><span class="sxs-lookup"><span data-stu-id="f7734-496">Retrieves time accrued on Client’s IP address lease</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-497">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-497">Prototype</span></span>

```C
UINT nx_dhcpv6_get_time_accrued(NX_DHCPV6 *dhcpv6_ptr, ULONG *time_accrued);
```

### <a name="description"></a><span data-ttu-id="f7734-498">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-498">Description</span></span>

<span data-ttu-id="f7734-499">Bu hizmet, Istemcinin IPv6 adresi kiralamasında tahakkuk eden süreyi alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-499">This service retrieves the time accrued on the Client’s IPv6 address lease.</span></span> <span data-ttu-id="f7734-500">İşlevi, ilk geçerli adres için Istemciye atanan tüm IPv6 adreslerini denetler.</span><span class="sxs-lookup"><span data-stu-id="f7734-500">The function checks all the IPv6 addresses assigned to the Client for the first valid address.</span></span> <span data-ttu-id="f7734-501">Geçerli adres bulunmazsa, tahakkuk edilen zaman için sıfır değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-501">If no valid addresses are found, a zero value for time accrued is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-502">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-502">Input Parameters</span></span>

- <span data-ttu-id="f7734-503">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-503">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-504">**time_accrued** IP kiralamasında tahakkuk eden zaman işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-504">**time_accrued** Pointer to time accrued in IP lease</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-505">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-505">Return Values</span></span>

- <span data-ttu-id="f7734-506">**NX_SUCCESS** (0x00) tahakkuk edilen süre başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-506">**NX_SUCCESS** (0x00) Accrued time successfully retrieved</span></span>

- <span data-ttu-id="f7734-507">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-507">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-508">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-508">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-509">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-509">Allowed From</span></span>

<span data-ttu-id="f7734-510">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-510">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-511">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-511">Example</span></span>

```C
/* Retrieve time accrued time on the Client address lease. */
status = nx_dhcpv6_get_time_accrued(&dhcp_0, &time_accrued);

/* If status is NX_SUCCESS the time accrued on the client IP address 
   lease was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-512">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-512">See Also</span></span>

- <span data-ttu-id="f7734-513">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-513">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="f7734-514">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="f7734-514">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="f7734-515">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="f7734-515">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="f7734-516">nx_dhcpv6_set_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-516">nx_dhcpv6_set_time_accrued</span></span>

## <a name="nx_dhcpv6_get_time_server_address"></a><span data-ttu-id="f7734-517">nx_dhcpv6_get_time_server_address</span><span class="sxs-lookup"><span data-stu-id="f7734-517">nx_dhcpv6_get_time_server_address</span></span>

<span data-ttu-id="f7734-518">Saat sunucusu adresini alır</span><span class="sxs-lookup"><span data-stu-id="f7734-518">Retrieves Time Server address</span></span> 

### <a name="prototype"></a><span data-ttu-id="f7734-519">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-519">Prototype</span></span>

```C
UINT  nx_dhcpv6_get_time_server_address(NX_DHCPV6 *dhcpv6_ptr, UINT index, 
                                        NXD_ADDRESS *server_address);
```

### <a name="description"></a><span data-ttu-id="f7734-520">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-520">Description</span></span>

<span data-ttu-id="f7734-521">Bu hizmet, Istemci listesindeki belirtilen dizindeki saat sunucusu IPv6 adresi verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-521">This service retrieves the Time server IPv6 address data at the specified index in the Client list.</span></span> <span data-ttu-id="f7734-522">Listede dizin üzerinde bir sunucu adresi yoksa bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-522">If the list does not contain a server address at the index, an error is returned.</span></span> <span data-ttu-id="f7734-523">Dizin, Kullanıcı tarafından yapılandırılabilir seçenek NX_DHCPV6_NUM_TIME_SERVERS tarafından belirtilen zaman sunucu listesinin boyutunu aşamaz.</span><span class="sxs-lookup"><span data-stu-id="f7734-523">The index may not exceed the size of the Time Server list is specified by the user configurable option NX_DHCPV6_NUM_TIME_SERVERS.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-524">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-524">Input Parameters</span></span>

- <span data-ttu-id="f7734-525">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-525">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-526">**Dizin** Saat sunucusu listesinde Dizin</span><span class="sxs-lookup"><span data-stu-id="f7734-526">**index** Index into the Time Server list</span></span>

- <span data-ttu-id="f7734-527">**server_address** Sunucu adresi arabelleği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-527">**server_address** Pointer to Server address buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-528">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-528">Return Values</span></span>

- <span data-ttu-id="f7734-529">**NX_SUCCESS** (0x00) adresi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-529">**NX_SUCCESS** (0x00) Address successfully retrieved</span></span>

- <span data-ttu-id="f7734-530">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-530">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-531">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-531">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-532">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-532">Allowed From</span></span>

<span data-ttu-id="f7734-533">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-533">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-534">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-534">Example</span></span>

```C
/* Retrieve the Time server at the specified index in the list. */

UINT index = 0;
NXD_ADDRESS server_address;


      status = nx_dhcpv6_get_time_server_address(&dhcp_0, index, &server_address);

/* If status == NX_SUCCESS, the Time server IP address successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-535">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-535">See Also</span></span>

- <span data-ttu-id="f7734-536">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-536">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="f7734-537">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="f7734-537">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="f7734-538">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-538">nx_dhcpv6_get_time_accrued</span></span>
- <span data-ttu-id="f7734-539">nx_dhcpv6_get_DNS_server_address</span><span class="sxs-lookup"><span data-stu-id="f7734-539">nx_dhcpv6_get_DNS_server_address</span></span>

## <a name="nx_dhcpv6_reinitialize"></a><span data-ttu-id="f7734-540">nx_dhcpv6_reinitialize</span><span class="sxs-lookup"><span data-stu-id="f7734-540">nx_dhcpv6_reinitialize</span></span>

<span data-ttu-id="f7734-541">Istemci IP adresini IP tablosundan kaldır</span><span class="sxs-lookup"><span data-stu-id="f7734-541">Remove the Client IP address from the IP table</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-542">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-542">Prototype</span></span>

```C
UINT nx_dhcpv6_reinitialize(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-543">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-543">Description</span></span>

<span data-ttu-id="f7734-544">Bu hizmet, DHCPv6 durum makinesini yeniden başlatmak ve DHCPv6 protokolünü yeniden çalıştırmak için Istemciyi yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="f7734-544">This service reinitializes the Client for restarting the DHCPv6 state machine and re-running the DHCPv6 protocol.</span></span> <span data-ttu-id="f7734-545">Istemci daha önce DHPCv6 durum makinesini başlatmadıysanız veya herhangi bir IPv6 adresi atamamışsa bu gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="f7734-545">This is not necessary if the Client has not previously started the DHPCv6 state machine or been assigned any IPv6 addresses.</span></span> <span data-ttu-id="f7734-546">DHCPv6 Istemcisine kaydedilen adresler ve IP örneğiyle kayıtlı olan adreslerin ikisi de temizlenir.</span><span class="sxs-lookup"><span data-stu-id="f7734-546">The addresses saved to the DHCPv6 Client as well as registered with the IP instance are both cleared.</span></span>

> [!NOTE]
> <span data-ttu-id="f7734-547">Uygulamanın yine de *nx_dhcpv6_start hizmetini* kullanarak DHCPv6 istemcisini başlatması ve *nx_dhcpv6_request_solicit* çağırarak IPv6 adres ataması isteğine başlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7734-547">The application must still start the DHCPv6 Client using the *nx_dhcpv6_start service* and begin the request for IPv6 address assignment by calling *nx_dhcpv6_request_solicit*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-548">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-548">Input Parameters</span></span>

- <span data-ttu-id="f7734-549">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-549">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-550">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-550">Return Values</span></span>

- <span data-ttu-id="f7734-551">**NX_SUCCESS** (0x00) adresi başarıyla kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="f7734-551">**NX_SUCCESS** (0x00) Address successfully removed</span></span>

- <span data-ttu-id="f7734-552">**NX_DHCPV6_ALREADY_STARTED** (0xe91) DHCPv6 istemcisi zaten çalışıyor</span><span class="sxs-lookup"><span data-stu-id="f7734-552">**NX_DHCPV6_ALREADY_STARTED** (0xE91) DHCPv6 Client is already running</span></span>

- <span data-ttu-id="f7734-553">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-553">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-554">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-554">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-555">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-555">Allowed From</span></span>

<span data-ttu-id="f7734-556">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-556">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-557">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-557">Example</span></span>

```C
/* Clear the assigned IP address(es) from the Client and the IP instance */
status = nx_dhcpv6_reinitialize(&dhcp_0);

/* If status is NX_SUCCESS the Client IP address was successfully removed. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-558">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-558">See Also</span></span>

- <span data-ttu-id="f7734-559">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="f7734-559">nx_dhcpv6_stop</span></span>
- <span data-ttu-id="f7734-560">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="f7734-560">nx_dhcpv6_start</span></span>

## <a name="nx_dhcpv6_request_confirm"></a><span data-ttu-id="f7734-561">nx_dhcpv6_request_confirm</span><span class="sxs-lookup"><span data-stu-id="f7734-561">nx_dhcpv6_request_confirm</span></span>

<span data-ttu-id="f7734-562">Istemcinin onaylama durumunu işleme</span><span class="sxs-lookup"><span data-stu-id="f7734-562">Process the Client’s CONFIRM state</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-563">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-563">Prototype</span></span>

```C
UINT nx_dhcpv6_request_confirm(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-564">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-564">Description</span></span>

<span data-ttu-id="f7734-565">Bu hizmet bir onaylama isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="f7734-565">This service sends a CONFIRM request.</span></span> <span data-ttu-id="f7734-566">Sunucudan bir yanıt alınmışsa, DHCPv6 Istemcisi kira parametrelerini alınan verilerle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f7734-566">If a reply is received from the Server, the DHCPv6 Client updates its lease parameters with the received data.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-567">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-567">Input Parameters</span></span>

- <span data-ttu-id="f7734-568">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-568">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-569">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-569">Return Values</span></span>

- <span data-ttu-id="f7734-570">**NX_SUCCESS** (0x00) ileti başarıyla gönderildiğini ve işlendiğini onaylayın</span><span class="sxs-lookup"><span data-stu-id="f7734-570">**NX_SUCCESS** (0x00) CONFIRM message successfully sent and processed</span></span>

- <span data-ttu-id="f7734-571">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-571">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-572">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-572">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-573">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-573">Allowed From</span></span>

<span data-ttu-id="f7734-574">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-574">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-575">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-575">Example</span></span>

```C
/* Send a CONFIRM message to the Server. */
status = nx_dhcpv6_request_confirm(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the CONFIRM message. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-576">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-576">See Also</span></span>

- <span data-ttu-id="f7734-577">nx_dhcpv6_request_inform_request</span><span class="sxs-lookup"><span data-stu-id="f7734-577">nx_dhcpv6_request_inform_request</span></span>
- <span data-ttu-id="f7734-578">nx_dhcpv6_request_release</span><span class="sxs-lookup"><span data-stu-id="f7734-578">nx_dhcpv6_request_release</span></span>
- <span data-ttu-id="f7734-579">nx_dhcpv6_request_solicit</span><span class="sxs-lookup"><span data-stu-id="f7734-579">nx_dhcpv6_request_solicit</span></span>


## <a name="nx_dhcpv6_request_inform_request"></a><span data-ttu-id="f7734-580">nx_dhcpv6_request_inform_request</span><span class="sxs-lookup"><span data-stu-id="f7734-580">nx_dhcpv6_request_inform_request</span></span>

<span data-ttu-id="f7734-581">Istemcinin BILGI ISTEğI durumunu işle</span><span class="sxs-lookup"><span data-stu-id="f7734-581">Process the Client’s INFORM REQUEST state</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-582">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-582">Prototype</span></span>

```C
UINT nx_dhcpv6_request_inform_request(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-583">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-583">Description</span></span>

<span data-ttu-id="f7734-584">Bu hizmet bir BILGI ISTEğI iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f7734-584">This service sends an INFORM REQUEST message.</span></span> <span data-ttu-id="f7734-585">Bir yanıt alınmışsa, biri alındığında yanıt, geçerli olduğunu ve sunucunun isteği vermiş olduğunu tespit etmek üzere işlenir.</span><span class="sxs-lookup"><span data-stu-id="f7734-585">If a reply is received, When one is received, the reply is processed to determine it is valid and the server granted the request.</span></span> <span data-ttu-id="f7734-586">Istemci örneği daha sonra gerektiği şekilde sunucu bilgileriyle güncellenir.</span><span class="sxs-lookup"><span data-stu-id="f7734-586">The Client instance is then updated with the server information as needed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-587">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-587">Input Parameters</span></span>

- <span data-ttu-id="f7734-588">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-588">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-589">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-589">Return Values</span></span>

- <span data-ttu-id="f7734-590">**NX_SUCCESS** (0x00) bildirme isteği iletisi başarıyla oluşturuldu ve işlendi</span><span class="sxs-lookup"><span data-stu-id="f7734-590">**NX_SUCCESS** (0x00) INFORM REQUEST message successfully created and processed</span></span>

- <span data-ttu-id="f7734-591">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-591">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-592">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-592">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-593">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-593">Allowed From</span></span>

<span data-ttu-id="f7734-594">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-594">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-595">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-595">Example</span></span>

```C
/* Send an INFORM REQUEST message to the server. */
status = nx_dhcpv6_request_inform_request(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the INFORM REQUEST 
   message and processed the reply. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-596">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-596">See Also</span></span>

- <span data-ttu-id="f7734-597">nx_dhcpv6_request_confirm</span><span class="sxs-lookup"><span data-stu-id="f7734-597">nx_dhcpv6_request_confirm</span></span>

## <a name="nx_dhcpv6_request_option_dns_server"></a><span data-ttu-id="f7734-598">nx_dhcpv6_request_option_DNS_server</span><span class="sxs-lookup"><span data-stu-id="f7734-598">nx_dhcpv6_request_option_DNS_server</span></span>

<span data-ttu-id="f7734-599">DHCPv6 seçenek isteğine DNS sunucusu ekleme</span><span class="sxs-lookup"><span data-stu-id="f7734-599">Add DNS Server to DHCPv6 Option request</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-600">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-600">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_DNS_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-601">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-601">Description</span></span>

<span data-ttu-id="f7734-602">Bu hizmet, DHCPv6 seçenek isteğine DNS sunucusu bilgilerini isteme seçeneğini ekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-602">This service adds the option for requesting DNS server information to the DHCPv6 option request.</span></span> <span data-ttu-id="f7734-603">Sunucu yanıtı DNS sunucusu verilerini içeriyorsa, Istemci, bunu yapmak için bir oda varsa, DNS sunucusunu depolayacaktır.</span><span class="sxs-lookup"><span data-stu-id="f7734-603">If the Server reply includes DNS server data, the Client will store the DNS server if it has room to do so.</span></span> <span data-ttu-id="f7734-604">Istemcinin depolayabileceği DNS sunucusu sayısı, varsayılan değeri 2 olan yapılandırılabilir seçenek NX_DHCPV6_NUM_DNS_SERVERS belirlenir.</span><span class="sxs-lookup"><span data-stu-id="f7734-604">The number of DNS servers the Client can store is determined by the configurable option NX_DHCPV6_NUM_DNS_SERVERS whose default value is 2.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-605">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-605">Input Parameters</span></span>

- <span data-ttu-id="f7734-606">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-606">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-607">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-607">Return Values</span></span>

- <span data-ttu-id="f7734-608">**NX_SUCCESS** (0x00) DNS sunucusu seçeneği dahildir</span><span class="sxs-lookup"><span data-stu-id="f7734-608">**NX_SUCCESS** (0x00) DNS server option is included</span></span>

- <span data-ttu-id="f7734-609">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-609">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-610">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-610">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-611">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-611">Allowed From</span></span>

<span data-ttu-id="f7734-612">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-612">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-613">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-613">Example</span></span>

```C
/* Set the DNS server option in Client requests. */
nx_dhcpv6_request_option_DNS_server(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a><span data-ttu-id="f7734-614">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-614">See Also</span></span>

- <span data-ttu-id="f7734-615">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="f7734-615">nx_dhcpv6_request_option_domain_name</span></span>
- <span data-ttu-id="f7734-616">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="f7734-616">nx_dhcpv6_request_option_time_server</span></span>
- <span data-ttu-id="f7734-617">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="f7734-617">nx_dhcpv6_request_option_timezone</span></span>

## <a name="nx_dhcpv6_request_option_fqdn"></a><span data-ttu-id="f7734-618">nx_dhcpv6_request_option_FQDN</span><span class="sxs-lookup"><span data-stu-id="f7734-618">nx_dhcpv6_request_option_FQDN</span></span>

<span data-ttu-id="f7734-619">Seçenek istek listesine tam etki alanı adı seçeneği ekleyin</span><span class="sxs-lookup"><span data-stu-id="f7734-619">Add Fully Qualified Domain Name option to Option request list</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-620">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-620">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_FQDN(NX_DHCPV6 *dhcpv6_ptr, UCHAR *domain_name, 
UINT op);
```

### <a name="description"></a><span data-ttu-id="f7734-621">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-621">Description</span></span>

<span data-ttu-id="f7734-622">Bu hizmet, Istemci tam etki alanı adını DHCPv6 seçenek isteğine ekleme seçeneğini ekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-622">This service adds the option for adding the Client Fully Qualified Domain Name to the DHCPv6 option request.</span></span> <span data-ttu-id="f7734-623">FQDN seçeneği için üç seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="f7734-623">There are three options for the FQDN option:</span></span>

- <span data-ttu-id="f7734-624">NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR 0, Istemci tarafından kullanılan FQDN ve adresler için FQDN-IPv6 adres eşlemeyi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f7734-624">NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR 0 Update the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the Client.</span></span>

- <span data-ttu-id="f7734-625">NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE 1 Istemci tarafından sunucu tarafından kullanılan FQDN ve adresler için FQDN-IPv6 adres eşlemeyi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f7734-625">NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE 1 Update the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the Client to the server.</span></span>

- <span data-ttu-id="f7734-626">NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE 2 sunucunun Istemci adına DNS güncelleştirmesi gerçekleştirmesiz bir Istek.</span><span class="sxs-lookup"><span data-stu-id="f7734-626">NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE 2 Request the server perform no DNS updates on the Client’s behalf.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-627">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-627">Input Parameters</span></span>

- <span data-ttu-id="f7734-628">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-628">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-629">**domain_name** Etki alanı adını tutan dize</span><span class="sxs-lookup"><span data-stu-id="f7734-629">**domain_name** String holding the domain name</span></span>

- <span data-ttu-id="f7734-630">**op** Uygulanacak FQDN seçeneğinin türü (yukarıdaki listeye bakın)</span><span class="sxs-lookup"><span data-stu-id="f7734-630">**op** Type of FQDN option to apply (see list above)</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-631">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-631">Return Values</span></span>

- <span data-ttu-id="f7734-632">**NX_SUCCESS** (0x00) FQDN seçeneği dahildir</span><span class="sxs-lookup"><span data-stu-id="f7734-632">**NX_SUCCESS** (0x00) FQDN option is included</span></span>

- <span data-ttu-id="f7734-633">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-633">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-634">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-634">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-635">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-635">Allowed From</span></span>

<span data-ttu-id="f7734-636">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-636">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-637">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-637">Example</span></span>

```C
/* Set the FQDN option in Client DHCPv6 request. */
nx_dhcpv6_request_option_FQDN(&dhcp_0, “DHCPv6_Client”, 
                              NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE);
```

### <a name="see-also"></a><span data-ttu-id="f7734-638">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-638">See Also</span></span>

- <span data-ttu-id="f7734-639">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="f7734-639">nx_dhcpv6_request_option_domain_name</span></span>
- <span data-ttu-id="f7734-640">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="f7734-640">nx_dhcpv6_request_option_time_server</span></span>
- <span data-ttu-id="f7734-641">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="f7734-641">nx_dhcpv6_request_option_timezone</span></span>

## <a name="nx_dhcpv6_request_option_domain_name"></a><span data-ttu-id="f7734-642">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="f7734-642">nx_dhcpv6_request_option_domain_name</span></span>

<span data-ttu-id="f7734-643">DHCPv6 seçenek isteğine etki alanı adı seçeneği ekleyin</span><span class="sxs-lookup"><span data-stu-id="f7734-643">Add domain name option to DHCPv6 option request</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-644">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-644">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_domain_name(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-645">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-645">Description</span></span>

<span data-ttu-id="f7734-646">Bu hizmet, Istemci isteği iletilerindeki seçenek isteğine etki alanı adı seçeneğini ekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-646">This service adds the domain name option to the option request in Client request messages.</span></span> <span data-ttu-id="f7734-647">Sunucu yanıtı etki alanı adı verileri içeriyorsa, etki alanı adının boyutu, etki alanı adının tutulması için arabellek boyutu içindeyse, Istemci etki alanı adı bilgilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="f7734-647">If the Server reply includes domain name data, the Client will store the domain name information if the size of the domain name is within the buffer size for holding the domain name.</span></span> <span data-ttu-id="f7734-648">Bu arabellek boyutu, varsayılan değer olan 30 baytlık yapılandırılabilir bir seçenektir (NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE).</span><span class="sxs-lookup"><span data-stu-id="f7734-648">This buffer size is a configurable option (NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE) with a default value of 30 bytes.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-649">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-649">Input Parameters</span></span>

- <span data-ttu-id="f7734-650">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-650">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-651">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-651">Return Values</span></span>

- <span data-ttu-id="f7734-652">**NX_SUCCESS** (0x00) etki alanı adı seçenek kümesi</span><span class="sxs-lookup"><span data-stu-id="f7734-652">**NX_SUCCESS** (0x00) Domain name option set</span></span>

- <span data-ttu-id="f7734-653">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-653">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-654">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-654">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-655">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-655">Allowed From</span></span>

<span data-ttu-id="f7734-656">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-656">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-657">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-657">Example</span></span>

```C
/* Set the domain name option in Client requests. */
nx_dhcpv6_request_option_domain_name(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a><span data-ttu-id="f7734-658">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-658">See Also</span></span>

- <span data-ttu-id="f7734-659">nx_dhcpv6_request_option_DNS_server</span><span class="sxs-lookup"><span data-stu-id="f7734-659">nx_dhcpv6_request_option_DNS_server</span></span>
- <span data-ttu-id="f7734-660">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="f7734-660">nx_dhcpv6_request_option_time_server</span></span>
- <span data-ttu-id="f7734-661">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="f7734-661">nx_dhcpv6_request_option_timezone</span></span>

## <a name="nx_dhcpv6_request_option_time_server"></a><span data-ttu-id="f7734-662">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="f7734-662">nx_dhcpv6_request_option_time_server</span></span>

<span data-ttu-id="f7734-663">Saat sunucusu verilerini isteğe bağlı istek olarak ayarla</span><span class="sxs-lookup"><span data-stu-id="f7734-663">Set time server data as optional request</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-664">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-664">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_time_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-665">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-665">Description</span></span>

<span data-ttu-id="f7734-666">Bu hizmet, Istemci istek iletilerinin seçenek isteğine zaman sunucusu bilgilerini ekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-666">This service adds the option for time server information to the option request of Client request messages.</span></span> <span data-ttu-id="f7734-667">Sunucu yanıtı, Tim sunucu verilerini içeriyorsa, Istemci, bunu yapmak için yer aldığında zaman sunucusunu depolayacaktır.</span><span class="sxs-lookup"><span data-stu-id="f7734-667">If the Server reply includes tim server data, the Client will store the time server if it has room to do so.</span></span> <span data-ttu-id="f7734-668">Istemcinin depolayabileceği zaman sunucularının sayısı, yapılandırılabilir seçenek tarafından belirlenir</span><span class="sxs-lookup"><span data-stu-id="f7734-668">The number of time servers the Client can store is determined by the configurable option</span></span>

<span data-ttu-id="f7734-669">Varsayılan değeri 1 olan _SERVERS NX_DHCPV6_NUM_TIME.</span><span class="sxs-lookup"><span data-stu-id="f7734-669">NX_DHCPV6_NUM_TIME _SERVERS whose default value is 1.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-670">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-670">Input Parameters</span></span>

- <span data-ttu-id="f7734-671">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-671">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-672">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-672">Return Values</span></span>

- <span data-ttu-id="f7734-673">**NX_SUCCESS** (0x00) saat sunucusu seçeneği eklendi</span><span class="sxs-lookup"><span data-stu-id="f7734-673">**NX_SUCCESS** (0x00) Time server option added</span></span>

- <span data-ttu-id="f7734-674">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-674">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-675">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-675">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-676">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-676">Allowed From</span></span>

<span data-ttu-id="f7734-677">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-677">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-678">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-678">Example</span></span>

```C
/* Set the time server option in Client request messages. */
nx_dhcpv6_request_option_time_server(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a><span data-ttu-id="f7734-679">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-679">See Also</span></span>

- <span data-ttu-id="f7734-680">nx_dhcpv6_request_option_DNS_server</span><span class="sxs-lookup"><span data-stu-id="f7734-680">nx_dhcpv6_request_option_DNS_server</span></span>
- <span data-ttu-id="f7734-681">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="f7734-681">nx_dhcpv6_request_option_domain_name</span></span>
- <span data-ttu-id="f7734-682">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="f7734-682">nx_dhcpv6_request_option_timezone</span></span>

## <a name="nx_dhcpv6_request_option_timezone"></a><span data-ttu-id="f7734-683">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="f7734-683">nx_dhcpv6_request_option_timezone</span></span>

<span data-ttu-id="f7734-684">Saat dilimi verilerini isteğe bağlı istek olarak ayarla</span><span class="sxs-lookup"><span data-stu-id="f7734-684">Set time zone data as optional request</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-685">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-685">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_timezone(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-686">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-686">Description</span></span>

<span data-ttu-id="f7734-687">Bu hizmet, Istemci seçenek isteğine saat dilimi bilgilerini isteme seçeneğini ekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-687">This service adds the option for requesting time zone information to the Client option request.</span></span> <span data-ttu-id="f7734-688">Sunucu yanıtı saat dilimi verilerini içeriyorsa, saat diliminin boyutu saat dilimini tutmak için arabellek boyutu içindeyse Istemci saat dilimi bilgilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="f7734-688">If the Server reply includes time zone data, the Client will store the time zone information if the size of the time zone is within the buffer size for holding the time zone.</span></span> <span data-ttu-id="f7734-689">Bu arabellek boyutu, varsayılan 10 baytlık bir değere sahip yapılandırılabilir bir seçenektir (NX_DHCPV6_ TIME_ZONE _BUFFER_SIZE).</span><span class="sxs-lookup"><span data-stu-id="f7734-689">This buffer size is a configurable option (NX_DHCPV6_ TIME_ZONE _BUFFER_SIZE) with a default value of 10 bytes.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-690">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-690">Input Parameters</span></span>

- <span data-ttu-id="f7734-691">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-691">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-692">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-692">Return Values</span></span>

- <span data-ttu-id="f7734-693">**NX_SUCCESS** (0x00) saat dilimi seçeneği eklendi</span><span class="sxs-lookup"><span data-stu-id="f7734-693">**NX_SUCCESS** (0x00) Time zone option added</span></span>

- <span data-ttu-id="f7734-694">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-694">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-695">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-695">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-696">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-696">Allowed From</span></span>

<span data-ttu-id="f7734-697">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-697">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-698">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-698">Example</span></span>

```C
/* Set time zone option in Client request messages. */
nx_dhcpv6_request_option_timezone(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a><span data-ttu-id="f7734-699">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-699">See Also</span></span>

- <span data-ttu-id="f7734-700">nx_dhcpv6_request_option_DNS_server</span><span class="sxs-lookup"><span data-stu-id="f7734-700">nx_dhcpv6_request_option_DNS_server</span></span>
- <span data-ttu-id="f7734-701">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="f7734-701">nx_dhcpv6_request_option_domain_name</span></span>
- <span data-ttu-id="f7734-702">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="f7734-702">nx_dhcpv6_request_option_time_server</span></span>

## <a name="nx_dhcpv6_request_release"></a><span data-ttu-id="f7734-703">nx_dhcpv6_request_release</span><span class="sxs-lookup"><span data-stu-id="f7734-703">nx_dhcpv6_request_release</span></span>

<span data-ttu-id="f7734-704">DHCPv6 sürüm iletisi gönder</span><span class="sxs-lookup"><span data-stu-id="f7734-704">Send a DHCPv6 RELEASE message</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-705">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-705">Prototype</span></span>

```C
UINT nx_dhcpv6_request_release(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-706">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-706">Description</span></span>

<span data-ttu-id="f7734-707">Bu hizmet, Istemci ağına bir sürüm iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f7734-707">This service sends a RELEASE message on the Client network.</span></span> <span data-ttu-id="f7734-708">İleti başarıyla gönderilirse, başarılı bir durum döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-708">If the message is successfully sent, a successful status is returned.</span></span> <span data-ttu-id="f7734-709">Başarılı bir tamamlama, Istemcinin bir yanıt aldığını veya henüz bir IPv6 adresi verildiğini ifade etmez.</span><span class="sxs-lookup"><span data-stu-id="f7734-709">A successful completion does not mean the Client received a response or has been granted an IPv6 address yet.</span></span> <span data-ttu-id="f7734-710">DHCPv6 Istemci iş parçacığı görevi DHCPv6 sunucusundan yanıt bekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-710">The DHCPv6 Client thread task waits for a reply from a DHCPv6 Server.</span></span> <span data-ttu-id="f7734-711">Bir tane alınmışsa, yanıtın geçerli olduğunu denetler ve verileri Istemci kaydına depolar.</span><span class="sxs-lookup"><span data-stu-id="f7734-711">If one is received, it checks the reply is valid and stores the data to the Client record.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-712">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-712">Input Parameters</span></span>

- <span data-ttu-id="f7734-713">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-713">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-714">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-714">Return Values</span></span>

- <span data-ttu-id="f7734-715">**NX_SUCCESS** (0x00) yayın iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="f7734-715">**NX_SUCCESS** (0x00) RELEASE message successfully sent</span></span>

- <span data-ttu-id="f7734-716">**NX_DHCPV6_NOT_STARTED** (0xe92) DHCPv6 istemci görevi başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="f7734-716">**NX_DHCPV6_NOT_STARTED** (0xE92) DHCPv6 Client task not started</span></span>

- <span data-ttu-id="f7734-717">**NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xead) adresi istemciye bağlanmadı</span><span class="sxs-lookup"><span data-stu-id="f7734-717">**NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) Address not bound to Client</span></span>

- <span data-ttu-id="f7734-718">**NX_INVALID_INTERFACE** (0x4C) IP adresi tablosunda bulunamadı</span><span class="sxs-lookup"><span data-stu-id="f7734-718">**NX_INVALID_INTERFACE** (0x4C) Not found in IP address table</span></span>

- <span data-ttu-id="f7734-719">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-719">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-720">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-720">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-721">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-721">Allowed From</span></span>

<span data-ttu-id="f7734-722">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-722">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-723">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-723">Example</span></span>

```C
/* Send an RELEASE message to the Server. */
status = nx_dhcpv6_request_release(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the RELEASE message. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-724">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-724">See Also</span></span>

- <span data-ttu-id="f7734-725">nx_dhcpv6_request_confirm</span><span class="sxs-lookup"><span data-stu-id="f7734-725">nx_dhcpv6_request_confirm</span></span>
- <span data-ttu-id="f7734-726">nx_dhcpv6_request_inform_request</span><span class="sxs-lookup"><span data-stu-id="f7734-726">nx_dhcpv6_request_inform_request</span></span>
- <span data-ttu-id="f7734-727">nx_dhcpv6_request_solicit</span><span class="sxs-lookup"><span data-stu-id="f7734-727">nx_dhcpv6_request_solicit</span></span>

## <a name="nx_dhcpv6_request_solicit"></a><span data-ttu-id="f7734-728">nx_dhcpv6_request_solicit</span><span class="sxs-lookup"><span data-stu-id="f7734-728">nx_dhcpv6_request_solicit</span></span>

<span data-ttu-id="f7734-729">Istem iletisi gönder</span><span class="sxs-lookup"><span data-stu-id="f7734-729">Send a SOLICIT message</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-730">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-730">Prototype</span></span>

```C
UINT nx_dhcpv6_request_solicit(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-731">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-731">Description</span></span>

<span data-ttu-id="f7734-732">Bu hizmet, ağda bir Istem iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f7734-732">This service sends a SOLICIT message out on the network.</span></span> <span data-ttu-id="f7734-733">İleti başarıyla gönderilirse, başarılı bir durum döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-733">If the message is successfully sent, a successful status is returned.</span></span> <span data-ttu-id="f7734-734">Başarılı bir tamamlama, Istemcinin bir yanıt aldığını veya henüz bir IPv6 adresi verildiğini ifade etmez.</span><span class="sxs-lookup"><span data-stu-id="f7734-734">A successful completion does not mean the Client received a response or has been granted an IPv6 address yet.</span></span> <span data-ttu-id="f7734-735">DHCPv6 Istemci iş parçacığı görevi DHCPv6 sunucusundan bir yanıt (bir TANıTıM iletisi) bekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-735">The DHCPv6 Client thread task waits for a reply (an ADVERTISE message) from a DHCPv6 Server.</span></span> <span data-ttu-id="f7734-736">Bir tane alınmışsa, yanıtın geçerli olduğunu denetler, verileri Istemci kaydına depolar ve Istemciyi Istek durumuna yükseltir.</span><span class="sxs-lookup"><span data-stu-id="f7734-736">If one is received, it checks the reply is valid, stores the data to the Client record and promotes the Client to the REQUEST state.</span></span>

> [!NOTE] 
> <span data-ttu-id="f7734-737">Hızlı tamamlama seçeneği ayarlandıysa, geçerli bir sunucu TANıTıM iletisi alırsa DHCPv6 Istemcisi doğrudan bağlantılı duruma geçer.</span><span class="sxs-lookup"><span data-stu-id="f7734-737">If the Rapid Commit option is set, the DHCPv6 Client will go directly to the Bound state if it receives a valid Server ADVERTISE message.</span></span> <span data-ttu-id="f7734-738">Daha fazla bilgi için bkz. *nx_dhcpv6_request_solicit_rapid* için hizmet açıklaması.</span><span class="sxs-lookup"><span data-stu-id="f7734-738">See the service description for *nx_dhcpv6_request_solicit_rapid* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-739">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-739">Input Parameters</span></span>

- <span data-ttu-id="f7734-740">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-740">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-741">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-741">Return Values</span></span>

- <span data-ttu-id="f7734-742">**NX_SUCCESS** (0x00) istem iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="f7734-742">**NX_SUCCESS** (0x00) SOLICIT message successfully sent</span></span>

- <span data-ttu-id="f7734-743">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-743">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-744">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-744">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-745">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-745">Allowed From</span></span>

<span data-ttu-id="f7734-746">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-746">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-747">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-747">Example</span></span>

```C
/* Send an SOLICIT message to the server. */
status = nx_dhcpv6_request_solicit(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the SOLICIT message. */
```

## <a name="nx_dhcpv6_request_solicit_rapid"></a><span data-ttu-id="f7734-748">nx_dhcpv6_request_solicit_rapid</span><span class="sxs-lookup"><span data-stu-id="f7734-748">nx_dhcpv6_request_solicit_rapid</span></span>

<span data-ttu-id="f7734-749">Hızlı tamamlama seçeneğiyle bir Istem iletisi gönderin</span><span class="sxs-lookup"><span data-stu-id="f7734-749">Send a SOLICIT message with the Rapid Commit option</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-750">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-750">Prototype</span></span>

```C
UINT nx_dhcpv6_request_solicit_rapid(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-751">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-751">Description</span></span>

<span data-ttu-id="f7734-752">Bu hizmet, ağ üzerinde hızlı tamamlama seçeneği ayarlanmış bir Istem iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f7734-752">This service sends a SOLICIT message out on the network with the Rapid Commit option set.</span></span> <span data-ttu-id="f7734-753">İleti başarıyla gönderilirse, başarılı bir durum döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f7734-753">If the message is successfully sent, a successful status is returned.</span></span> <span data-ttu-id="f7734-754">Başarılı bir tamamlama, Istemcinin bir yanıt aldığını veya henüz bir IPv6 adresi verildiğini ifade etmez.</span><span class="sxs-lookup"><span data-stu-id="f7734-754">A successful completion does not mean the Client received a response or has been granted an IPv6 address yet.</span></span> <span data-ttu-id="f7734-755">DHCPv6 Istemci iş parçacığı görevi DHCPv6 sunucusundan bir yanıt (bir TANıTıM iletisi) bekler.</span><span class="sxs-lookup"><span data-stu-id="f7734-755">The DHCPv6 Client thread task waits for a reply (an ADVERTISE message) from a DHCPv6 Server.</span></span> <span data-ttu-id="f7734-756">Bir tane alınmışsa, yanıtın geçerli olduğunu denetler, verileri Istemci kaydına depolar ve Istemciyi bağlantılı duruma yükseltir.</span><span class="sxs-lookup"><span data-stu-id="f7734-756">If one is received, it checks the reply is valid, stores the data to the Client record and promotes the Client to the BOUND state.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-757">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-757">Input Parameters</span></span>

- <span data-ttu-id="f7734-758">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-758">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-759">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-759">Return Values</span></span>

- <span data-ttu-id="f7734-760">**NX_SUCCESS** (0x00) istem iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="f7734-760">**NX_SUCCESS** (0x00) SOLICIT message successfully sent</span></span>

- <span data-ttu-id="f7734-761">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-761">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-762">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-762">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-763">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-763">Allowed From</span></span>

<span data-ttu-id="f7734-764">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-764">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-765">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-765">Example</span></span>

```C
/* Send an SOLICIT message to the server. */
status = nx_dhcpv6_request_solicit_rapid(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the SOLICIT message. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-766">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-766">See Also</span></span>

- <span data-ttu-id="f7734-767">nx_dhcpv6_request_solicit</span><span class="sxs-lookup"><span data-stu-id="f7734-767">nx_dhcpv6_request_solicit</span></span>
- <span data-ttu-id="f7734-768">nx_dhcpv6_request_confirm</span><span class="sxs-lookup"><span data-stu-id="f7734-768">nx_dhcpv6_request_confirm</span></span>
- <span data-ttu-id="f7734-769">nx_dhcpv6_request_inform_request</span><span class="sxs-lookup"><span data-stu-id="f7734-769">nx_dhcpv6_request_inform_request</span></span>
- <span data-ttu-id="f7734-770">nx_dhcpv6_request_release</span><span class="sxs-lookup"><span data-stu-id="f7734-770">nx_dhcpv6_request_release</span></span>

## <a name="nx_dhcpv6_resume"></a><span data-ttu-id="f7734-771">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="f7734-771">nx_dhcpv6_resume</span></span>

<span data-ttu-id="f7734-772">DHCPv6 Istemci görevini sürdürür</span><span class="sxs-lookup"><span data-stu-id="f7734-772">Resume DHCPv6 Client task</span></span> 

### <a name="prototype"></a><span data-ttu-id="f7734-773">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-773">Prototype</span></span>

```C
UINT nx_dhcpv6_resume(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-774">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-774">Description</span></span>

<span data-ttu-id="f7734-775">Bu hizmet, DHCPv6 Istemci iş parçacığı görevini sürdürür.</span><span class="sxs-lookup"><span data-stu-id="f7734-775">This service resumes the DHCPv6 Client thread task.</span></span> <span data-ttu-id="f7734-776">Geçerli DHCPv6 Istemci durumu işlenecek (örn. bağlanma, Istek)</span><span class="sxs-lookup"><span data-stu-id="f7734-776">The current DHCPv6 Client state will be processed (e.g. Bound, Solicit)</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-777">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-777">Input Parameters</span></span>

- <span data-ttu-id="f7734-778">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-778">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-779">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-779">Return Values</span></span>

- <span data-ttu-id="f7734-780">**NX_SUCCESS** (0x00) istemci başarıyla sürdürüldü</span><span class="sxs-lookup"><span data-stu-id="f7734-780">**NX_SUCCESS** (0x00) Client successfully resumed</span></span>

- <span data-ttu-id="f7734-781">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-781">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-782">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-782">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-783">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-783">Allowed From</span></span>

<span data-ttu-id="f7734-784">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-784">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-785">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-785">Example</span></span>

```C
/* Resume the DHCPv6 Client task. */
status = nx_dhcpv6_resume(&dhcp_0);

/* If status is NX_SUCCESS the Client thread task successfully resumed. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-786">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-786">See Also</span></span>

- <span data-ttu-id="f7734-787">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="f7734-787">nx_dhcpv6_start</span></span>
- <span data-ttu-id="f7734-788">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="f7734-788">nx_dhcpv6_stop</span></span>
- <span data-ttu-id="f7734-789">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="f7734-789">nx_dhcpv6_suspend</span></span>

## <a name="nx_dhcpv6_set_-time_accrued"></a><span data-ttu-id="f7734-790">nx_dhcpv6_set_ time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-790">nx_dhcpv6_set_ time_accrued</span></span>

<span data-ttu-id="f7734-791">Istemcinin IP adresi kirası üzerinde tahakkuk eden süreyi ayarlar</span><span class="sxs-lookup"><span data-stu-id="f7734-791">Sets time accrued on Client’s IP address lease</span></span>

### <a name="prototype"></a><span data-ttu-id="f7734-792">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-792">Prototype</span></span>

```C
UINT nx_dhcpv6_set_time_accrued(NX_DHCPV6 *dhcpv6_ptr,
                                ULONG time_accrued);
```

### <a name="description"></a><span data-ttu-id="f7734-793">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-793">Description</span></span>

<span data-ttu-id="f7734-794">Bu hizmet, Istemcinin genel IP adresi sunucu tarafından atandıktan sonra tahakkuk eden süreyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f7734-794">This service sets the time accrued on the Client’s global IP address since it was assigned by the server.</span></span> <span data-ttu-id="f7734-795">Bu, yalnızca bir Istemci atanmış bir IPv6 adresine bağlıysa kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f7734-795">This should only be used if a Client is currently bound to an assigned IPv6 address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-796">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-796">Input Parameters</span></span>

- <span data-ttu-id="f7734-797">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-797">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="f7734-798">**time_accrued** IP kiralamasında tahakkuk eden saat</span><span class="sxs-lookup"><span data-stu-id="f7734-798">**time_accrued** Time accrued in IP lease</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-799">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-799">Return Values</span></span>

- <span data-ttu-id="f7734-800">**NX_SUCCESS** (0x00) tahakkuk eden zaman kümesi</span><span class="sxs-lookup"><span data-stu-id="f7734-800">**NX_SUCCESS** (0x00) Time accrued successfully set</span></span>

- <span data-ttu-id="f7734-801">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-801">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-802">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-802">Allowed From</span></span>

<span data-ttu-id="f7734-803">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-803">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-804">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-804">Example</span></span>

```C
/* Set time accrued since client’s assigned IP address was assigned. */
status = nx_dhcpv6_set_time_accrued(&dhcp_0, time_accrued);

/* If status is NX_SUCCESS the time accrued on the client IP address lease was 
   successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-805">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-805">See Also</span></span>

- <span data-ttu-id="f7734-806">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="f7734-806">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="f7734-807">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="f7734-807">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="f7734-808">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="f7734-808">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="f7734-809">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="f7734-809">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_start"></a><span data-ttu-id="f7734-810">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="f7734-810">nx_dhcpv6_start</span></span>

<span data-ttu-id="f7734-811">DHCPv6 Istemci görevini başlatın</span><span class="sxs-lookup"><span data-stu-id="f7734-811">Start the DHCPv6 Client task</span></span> 

### <a name="prototype"></a><span data-ttu-id="f7734-812">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-812">Prototype</span></span>

```C
UINT nx_dhcpv6_start(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-813">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-813">Description</span></span>

<span data-ttu-id="f7734-814">Bu hizmet DHCPv6 Istemci görevini başlatır ve Istemciyi DHCPv6 protokolünü çalıştırmaya hazırlar.</span><span class="sxs-lookup"><span data-stu-id="f7734-814">This service starts the DHCPv6 Client task and prepares the Client for running the DHCPv6 protocol.</span></span> <span data-ttu-id="f7734-815">Istemci örneğinin yeterli bilgilere sahip olduğunu doğrular (örneğin, bir Istemci DUıD), DHCPv6 iletilerini göndermek ve almak için UDP yuvasını oluşturup bağlar ve oturum süresini izlemek ve geçerli IPv6 kira süresinin dolması için zamanlayıcıları etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="f7734-815">It verifies the Client instance has sufficient information (such as a Client DUID), creates and binds the UDP socket for sending and receiving DHCPv6 messages and activates timers for keeping track of session time and when the current IPv6 lease expires.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-816">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-816">Input Parameters</span></span>

- <span data-ttu-id="f7734-817">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-817">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-818">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-818">Return Values</span></span>

- <span data-ttu-id="f7734-819">**NX_SUCCESS** (0x00) istemci başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="f7734-819">**NX_SUCCESS** (0x00) Client successfully started</span></span>

- <span data-ttu-id="f7734-820">**NX_DHCPV6_MISSING_REQUIRED_OPTIONS** (0xea9) istemcisinde gerekli seçenekler eksik</span><span class="sxs-lookup"><span data-stu-id="f7734-820">**NX_DHCPV6_MISSING_REQUIRED_OPTIONS** (0xEA9) Client missing required options</span></span>

- <span data-ttu-id="f7734-821">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-821">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-822">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-822">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-823">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-823">Allowed From</span></span>

<span data-ttu-id="f7734-824">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-824">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-825">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-825">Example</span></span>

```C
/* Start the DHCPv6 Client task. */
status = nx_dhcpv6_start(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully started. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-826">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-826">See Also</span></span>

- <span data-ttu-id="f7734-827">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="f7734-827">nx_dhcpv6_resume</span></span>
- <span data-ttu-id="f7734-828">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="f7734-828">nx_dhcpv6_suspend</span></span>
- <span data-ttu-id="f7734-829">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="f7734-829">nx_dhcpv6_stop</span></span>
- <span data-ttu-id="f7734-830">nx_dhcpv6_reinitialize</span><span class="sxs-lookup"><span data-stu-id="f7734-830">nx_dhcpv6_reinitialize</span></span>

## <a name="nx_dhcpv6_stop"></a><span data-ttu-id="f7734-831">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="f7734-831">nx_dhcpv6_stop</span></span>

<span data-ttu-id="f7734-832">DHCPv6 Istemci görevini durdur</span><span class="sxs-lookup"><span data-stu-id="f7734-832">Stop the DHCPv6 Client task</span></span> 

### <a name="prototype"></a><span data-ttu-id="f7734-833">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-833">Prototype</span></span>

```C
UINT nx_dhcpv6_stop(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-834">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-834">Description</span></span>

<span data-ttu-id="f7734-835">Bu hizmet, DHCPv6 Istemci görevini sonlandırır ve yeniden aktarım sayısını, en fazla yeniden aktarım aralığını temizler, oturumu ve Kiralama süre sonu zamanlayıcıları devre dışı bırakır ve DHCPv6 Istemci yuva bağlantı noktasının bağlantısını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f7734-835">This service stops the DHCPv6 Client task, and clears retransmission counts, maximum retransmission intervals, deactivates the session and lease expiration timers, and unbinds the DHCPv6 Client socket port.</span></span> <span data-ttu-id="f7734-836">Istemciyi yeniden başlatmak için, önce herhangi bir DHCPv6 sunucusu ile başka bir oturum başlatmadan önce Istemciyi durdurup isteğe bağlı olarak yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7734-836">To restart the Client, one must first stop and optionally reinitialize the Client before starting another session with any DHCPv6 server.</span></span> <span data-ttu-id="f7734-837">Daha fazla bilgi için küçük örnek bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f7734-837">See the Small Example section for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-838">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-838">Input Parameters</span></span>

- <span data-ttu-id="f7734-839">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-839">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-840">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-840">Return Values</span></span>

- <span data-ttu-id="f7734-841">**NX_SUCCESS** (0x00) istemci başarıyla durduruldu</span><span class="sxs-lookup"><span data-stu-id="f7734-841">**NX_SUCCESS** (0x00) Client successfully stopped</span></span>

- <span data-ttu-id="f7734-842">**NX_DHCPV6_NOT_STARTED** (0xe92) istemci iş parçacığı başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="f7734-842">**NX_DHCPV6_NOT_STARTED** (0xE92) Client thread not started</span></span>

- <span data-ttu-id="f7734-843">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-843">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-844">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-844">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>


### <a name="allowed-from"></a><span data-ttu-id="f7734-845">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-845">Allowed From</span></span>

<span data-ttu-id="f7734-846">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-846">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-847">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-847">Example</span></span>

```C
/* Stop the DHCPv6 Client task. */
status = nx_dhcpv6_start(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully stopped. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-848">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-848">See Also</span></span>

- <span data-ttu-id="f7734-849">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="f7734-849">nx_dhcpv6_resume</span></span>
- <span data-ttu-id="f7734-850">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="f7734-850">nx_dhcpv6_suspend</span></span>
- <span data-ttu-id="f7734-851">nx_dhcpv6_reinitialize</span><span class="sxs-lookup"><span data-stu-id="f7734-851">nx_dhcpv6_reinitialize</span></span>
- <span data-ttu-id="f7734-852">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="f7734-852">nx_dhcpv6_start</span></span>

## <a name="nx_dhcpv6_suspend"></a><span data-ttu-id="f7734-853">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="f7734-853">nx_dhcpv6_suspend</span></span>

<span data-ttu-id="f7734-854">DHCPv6 Istemci görevini askıya alma</span><span class="sxs-lookup"><span data-stu-id="f7734-854">Suspend the DHCPv6 Client task</span></span> 

### <a name="prototype"></a><span data-ttu-id="f7734-855">Prototype</span><span class="sxs-lookup"><span data-stu-id="f7734-855">Prototype</span></span>

```C
UINT nx_dhcpv6_suspend(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="f7734-856">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f7734-856">Description</span></span>

<span data-ttu-id="f7734-857">Bu hizmet, DHCPv6 istemci görevini ve işlemin ortasında olduğu tüm istekleri askıya alır.</span><span class="sxs-lookup"><span data-stu-id="f7734-857">This service suspends the DHCPv6 client task and any request it was in the middle of processing.</span></span> <span data-ttu-id="f7734-858">Zamanlayıcılar devre dışı bırakılır ve Istemci durumu çalışmıyor olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f7734-858">Timers are deactivated and the Client state is set to non-running.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f7734-859">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="f7734-859">Input Parameters</span></span>

- <span data-ttu-id="f7734-860">**dhcpv6_ptr** DHCPv6 Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="f7734-860">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="f7734-861">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="f7734-861">Return Values</span></span>

- <span data-ttu-id="f7734-862">**NX_SUCCESS** (0x00) istemci başarıyla askıya alındı</span><span class="sxs-lookup"><span data-stu-id="f7734-862">**NX_SUCCESS** (0x00) Client successfully suspended</span></span>

- <span data-ttu-id="f7734-863">**NX_DHCPV6_NOT_STARTED** (0xe92) istemci çalışmıyor, askıya alınamıyor</span><span class="sxs-lookup"><span data-stu-id="f7734-863">**NX_DHCPV6_NOT_STARTED** (0XE92) Client not running so cannot be suspended</span></span>

- <span data-ttu-id="f7734-864">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="f7734-864">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="f7734-865">NX_CALLER_ERROR (0x11) iş parçacığından çağrılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f7734-865">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7734-866">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="f7734-866">Allowed From</span></span>

<span data-ttu-id="f7734-867">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="f7734-867">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7734-868">Örnek</span><span class="sxs-lookup"><span data-stu-id="f7734-868">Example</span></span>

```C
/* Suspend the DHCPv6 Client task. */
status = nx_dhcpv6_suspend(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully suspended. */
```

### <a name="see-also"></a><span data-ttu-id="f7734-869">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f7734-869">See Also</span></span>

- <span data-ttu-id="f7734-870">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="f7734-870">nx_dhcpv6_resume</span></span>
- <span data-ttu-id="f7734-871">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="f7734-871">nx_dhcpv6_start</span></span>
- <span data-ttu-id="f7734-872">nx_dhcpv6_reinitialize</span><span class="sxs-lookup"><span data-stu-id="f7734-872">nx_dhcpv6_reinitialize</span></span>
- <span data-ttu-id="f7734-873">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="f7734-873">nx_dhcpv6_stop</span></span>
