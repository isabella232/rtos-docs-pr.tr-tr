---
title: Bölüm 4-Azure RTOS NetX Duo DHCPv6 sunucu hizmetleri
description: Bu bölümde tüm NetX Duo DHCPv6Server hizmetlerinin açıklaması yer almaktadır
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1d45139031b5a687baacf86c7a2e0a53c90533be
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826027"
---
# <a name="chapter-4---azure-rtos-netx-duo-dhcpv6-server-services"></a><span data-ttu-id="2303f-103">Bölüm 4-Azure RTOS NetX Duo DHCPv6 sunucu hizmetleri</span><span class="sxs-lookup"><span data-stu-id="2303f-103">Chapter 4 - Azure RTOS NetX Duo DHCPv6 server services</span></span>

<span data-ttu-id="2303f-104">Bu bölüm tüm NetX Duo DHCPv6Server hizmetlerinin (aşağıda listelenmiştir) bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="2303f-104">This chapter contains a description of all NetX Duo DHCPv6Server services (listed below).</span></span>

<span data-ttu-id="2303f-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="2303f-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="2303f-106">nx_dhcpv6_server_create *DHCPv6 ServerInstance oluşturma*</span><span class="sxs-lookup"><span data-stu-id="2303f-106">nx_dhcpv6_server_create *Create a DHCPv6 serverinstance*</span></span>
- <span data-ttu-id="2303f-107">nx_dhcpv6_server_delete *DHCPv6 ServerInstance silme*</span><span class="sxs-lookup"><span data-stu-id="2303f-107">nx_dhcpv6_server_delete *Delete a DHCPv6 serverinstance*</span></span>
- <span data-ttu-id="2303f-108">nx_dhcpv6_server_start *DHCPv6 sunucusu görevini başlatın*</span><span class="sxs-lookup"><span data-stu-id="2303f-108">nx_dhcpv6_server_start *Start the DHCPv6 server task*</span></span>
- <span data-ttu-id="2303f-109">nx_dhcpv6_server_suspend *DHCPv6 sunucusu görevini askıya al*</span><span class="sxs-lookup"><span data-stu-id="2303f-109">nx_dhcpv6_server_suspend *Suspend the DHCPv6 server task*</span></span>
- <span data-ttu-id="2303f-110">nx_dhcpv6_server_resume *DHCPv6 istemci Işlemesini sürdürür*</span><span class="sxs-lookup"><span data-stu-id="2303f-110">nx_dhcpv6_server_resume *Resume DHCPv6 client processing*</span></span>
- <span data-ttu-id="2303f-111">nx_dhcpv6_server_suspend *DHCPv6 istemci Işlemesini askıya al*</span><span class="sxs-lookup"><span data-stu-id="2303f-111">nx_dhcpv6_server_suspend *Suspend DHCPv6 client processing*</span></span>
- <span data-ttu-id="2303f-112">*seçenek istekleri IÇIN DNS sunucusunu Nx_dhcpv6_create_dns_address ayarlama*</span><span class="sxs-lookup"><span data-stu-id="2303f-112">nx_dhcpv6_create_dns_address *Set the DNS server for option requests*</span></span>
- <span data-ttu-id="2303f-113">nx_dhcpv6_create_ip_address_range *kiralamak IÇIN IP adresi aralığı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="2303f-113">nx_dhcpv6_create_ip_address_range *Create the range of IP addresses to lease*</span></span>
- <span data-ttu-id="2303f-114">*sunucu LISTESINDEKI IP adreslerinin ayrılmış aralığını* nx_dhcpv6_reserve_ip_address_range</span><span class="sxs-lookup"><span data-stu-id="2303f-114">nx_dhcpv6_reserve_ip_address_range *Reserve range of IP addresses in server list*</span></span>
- <span data-ttu-id="2303f-115">nx_dhcpv6_set_server_duid *DHCPv6 paketleri Için sunucu DUID 'Sini ayarlama*</span><span class="sxs-lookup"><span data-stu-id="2303f-115">nx_dhcpv6_set_server_duid *Set the Server DUID for DHCPv6 packets*</span></span>
- <span data-ttu-id="2303f-116">*DHCPv6 sunucu tablosuna bir kira kaydı eklemek* nx_dhcpv6_add_ip_address_lease</span><span class="sxs-lookup"><span data-stu-id="2303f-116">nx_dhcpv6_add_ip_address_lease *Add a lease record to the DHCPv6 server table*</span></span>
- <span data-ttu-id="2303f-117">*Sunucu tablosundan BIR IP Kiralama kaydı almak* Nx_dhcpv6_retrieve_ip_address_lease</span><span class="sxs-lookup"><span data-stu-id="2303f-117">Nx_dhcpv6_retrieve_ip_address_lease *Retrieve an IP lease record from the Server table*</span></span>
- <span data-ttu-id="2303f-118">*sunucu tablosuna bir DHCPv6 istemci kaydı eklemek* nx_dhcpv6_add_client_record</span><span class="sxs-lookup"><span data-stu-id="2303f-118">nx_dhcpv6_add_client_record *Add a DHCPv6 Client record to the Server table*</span></span>
- <span data-ttu-id="2303f-119">*sunucu tablosundan bir istemci kaydı almak* nx_dhcpv6_retrieve_client_record</span><span class="sxs-lookup"><span data-stu-id="2303f-119">nx_dhcpv6_retrieve_client_record *Retrieve a client record from the Server table*</span></span>
- <span data-ttu-id="2303f-120">*sunucu DHCPv6 Hizmetleri için arabirim dizinini Nx_dhcpv6_server_interface_set ayarlama*</span><span class="sxs-lookup"><span data-stu-id="2303f-120">nx_dhcpv6_server_interface_set *Set the interface index for Server DHCPv6 services*</span></span>
- <span data-ttu-id="2303f-121">*seçenek isteği işleyicisini Nx_dhcpv6_server_option_request_handler_set ayarla*</span><span class="sxs-lookup"><span data-stu-id="2303f-121">nx_dhcpv6_server_option_request_handler_set *Set the option request handler*</span></span>

## <a name="nx_dhcpv6_create_dns_address"></a><span data-ttu-id="2303f-122">nx_dhcpv6_create_dns_address</span><span class="sxs-lookup"><span data-stu-id="2303f-122">nx_dhcpv6_create_dns_address</span></span>

### <a name="set-the-network-dns-server"></a><span data-ttu-id="2303f-123">Ağ DNS sunucusunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="2303f-123">Set the network DNS server</span></span>

<span data-ttu-id="2303f-124">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-124">**Prototype**</span></span>

```
UINT nx_dhcpv6_create_dns_address(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *dns_ipv6_address);
```

<span data-ttu-id="2303f-125">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-125">**Description**</span></span>

<span data-ttu-id="2303f-126">Bu hizmet, DHCPv6 sunucusunu sunucu DHCPv6 ağ arabirimi için DNS sunucu adresiyle yükler.</span><span class="sxs-lookup"><span data-stu-id="2303f-126">This service loads the DHCPv6 Server with the DNS server address for the Server DHCPv6 network interface.</span></span>

<span data-ttu-id="2303f-127">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-127">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-128">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-128">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-129">**dns_ipv6_address** DNS sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-129">**dns_ipv6_address** Pointer to the DNS server</span></span>

<span data-ttu-id="2303f-130">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-130">**Return Values**</span></span>

- <span data-ttu-id="2303f-131">**NX_SUCCESS** (0x00) DNS sunucusu, DHCPv6 sunucu örneğine kaydedildi</span><span class="sxs-lookup"><span data-stu-id="2303f-131">**NX_SUCCESS** (0x00) DNS Serversaved to DHCPv6 Server instance</span></span>
- <span data-ttu-id="2303f-132">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xe95) geçersiz bir adres sağlandı</span><span class="sxs-lookup"><span data-stu-id="2303f-132">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) An invalid address is supplied</span></span>
- <span data-ttu-id="2303f-133">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-133">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-134">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-134">**Allowed From**</span></span>

<span data-ttu-id="2303f-135">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-135">Application Code</span></span>

<span data-ttu-id="2303f-136">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-136">**Example**</span></span>

```
/* Set the network DNS server with the input address for the Server DHCPv6interface. */
status = nx_dhcpv6_create__dns_address(&dhcp_server_0, &dns_ipv6_address);
/* If this service returns NX_SUCCESS the DNS server data was accepted. */
```

## <a name="nx_dhcpv6_create_ip_address_range"></a><span data-ttu-id="2303f-137">nx_dhcpv6_create_ip_address_range</span><span class="sxs-lookup"><span data-stu-id="2303f-137">nx_dhcpv6_create_ip_address_range</span></span>

### <a name="create-the-server-ip-address-list"></a><span data-ttu-id="2303f-138">Sunucu IP adresi listesini oluşturma</span><span class="sxs-lookup"><span data-stu-id="2303f-138">Create the Server IP address list</span></span>

<span data-ttu-id="2303f-139">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-139">**Prototype**</span></span>

```
UINT _nx_dhcpv6_create_ip_address_range(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *start_ipv6_address, NXD_ADDRESS *end_ipv6_address, 
     UINT *addresses_added)
```

<span data-ttu-id="2303f-140">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-140">**Description**</span></span>

<span data-ttu-id="2303f-141">Bu hizmet, sunucunun atanabilir adres aralığının başlangıç ve bitiş adresleriyle belirtilen IP adresi listesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2303f-141">This service creates the IP address list specified by the start and end addresses of the Server’s assignable address range.</span></span> <span data-ttu-id="2303f-142">Başlangıç ve bitiş adresleri sunucu arabirimi adres önekiyle eşleşmelidir (sunucu DHCPv6 arabirimiyle aynı bağlantıda olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="2303f-142">The start and end addresses must match the Server interface address prefix (must be on the same link as the Server DHCPv6 interface).</span></span> <span data-ttu-id="2303f-143">Gerçekte eklenen adreslerin sayısı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="2303f-143">The number of addresses actually added is returned.</span></span>

<span data-ttu-id="2303f-144">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-144">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-145">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-145">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-146">**start_ipv6_address** Eklenecek adreslerin başlangıcı</span><span class="sxs-lookup"><span data-stu-id="2303f-146">**start_ipv6_address** Start of addresses to add</span></span>
- <span data-ttu-id="2303f-147">**end_ipv6_address** Eklenecek adreslerin sonu</span><span class="sxs-lookup"><span data-stu-id="2303f-147">**end_ipv6_address** End of addresses to add</span></span>
- <span data-ttu-id="2303f-148">\***addresses_added** Eklenen adreslerin çıkışı</span><span class="sxs-lookup"><span data-stu-id="2303f-148">\***addresses_added** Output of addresses added</span></span>

<span data-ttu-id="2303f-149">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-149">**Return Values**</span></span>

- <span data-ttu-id="2303f-150">**NX_SUCCESS** (0x00) IP adresi listesi başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="2303f-150">**NX_SUCCESS** (0x00) IP address list successfully created</span></span>
- <span data-ttu-id="2303f-151">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xe95) geçersiz bir adres sağlandı</span><span class="sxs-lookup"><span data-stu-id="2303f-151">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) An invalid address is supplied</span></span>
- <span data-ttu-id="2303f-152">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-152">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-153">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-153">**Allowed From**</span></span>

<span data-ttu-id="2303f-154">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-154">Application Code</span></span>

<span data-ttu-id="2303f-155">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-155">**Example**</span></span>

```
/* Create the Server IP address list for the server DHCPv6 interface. */
status = nx_dhcpv6_create_ip_address_range(&dhcp_server_0,
         &start_ipv6_address, &end_ipv6_address, &addresses_reserved);
/* If status is NX_SUCCESS one or more addresses were successfully added. */
```

## <a name="nx_dhcpv6_reserve_ip_address_range"></a><span data-ttu-id="2303f-156">nx_dhcpv6_reserve_ip_address_range</span><span class="sxs-lookup"><span data-stu-id="2303f-156">nx_dhcpv6_reserve_ip_address_range</span></span>

### <a name="reserve-specified-range-of-ip-addresses"></a><span data-ttu-id="2303f-157">Belirtilen IP adresi aralığını ayır</span><span class="sxs-lookup"><span data-stu-id="2303f-157">Reserve specified range of IP addresses</span></span>

<span data-ttu-id="2303f-158">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-158">**Prototype**</span></span>

```
UINT _nx_dhcpv6_reserve_ip_address_range(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *start_ipv6_address, NXD_ADDRESS *end_ipv6_address, 
     UINT *addresses_reserved)
```

<span data-ttu-id="2303f-159">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-159">**Description**</span></span>

<span data-ttu-id="2303f-160">Bu hizmet başlangıç ve bitiş adresleriyle belirtilen IP adresi aralığını ayırır.</span><span class="sxs-lookup"><span data-stu-id="2303f-160">This service reserves the IP address range specified by the start and end addresses.</span></span> <span data-ttu-id="2303f-161">Bu adresler, önceden oluşturulmuş sunucu IP adresi aralığında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2303f-161">These addresses must be within in the previously created server IP address range.</span></span> <span data-ttu-id="2303f-162">Bu adresler, DHCPv6 sunucusu tarafından herhangi bir Istemciye atanmaz.</span><span class="sxs-lookup"><span data-stu-id="2303f-162">These addresses will not be assigned to any Clients by the DHCPv6 Server.</span></span> <span data-ttu-id="2303f-163">Başlangıç ve bitiş adresleri sunucu arabirimi adres önekiyle eşleşmelidir (sunucu DHCPv6 ağ arabirimiyle aynı bağlantıda olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="2303f-163">The start and end addresses must match the Server interface address prefix (must be on the same link as the Server DHCPv6 network interface).</span></span> <span data-ttu-id="2303f-164">Gerçekte ayrılan adreslerin sayısı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="2303f-164">The number of addresses actually reserved is returned.</span></span>

<span data-ttu-id="2303f-165">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-165">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-166">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-166">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-167">**start_ipv6_address** Ayrılacak adreslerin başlangıcı</span><span class="sxs-lookup"><span data-stu-id="2303f-167">**start_ipv6_address** Start of addresses to reserve</span></span>
- <span data-ttu-id="2303f-168">**end_ipv6_address** Ayrılacak adreslerin sonu</span><span class="sxs-lookup"><span data-stu-id="2303f-168">**end_ipv6_address** End of addresses to reserve</span></span>
- <span data-ttu-id="2303f-169">\***addresses_reserved** Ayrılan adres sayısı</span><span class="sxs-lookup"><span data-stu-id="2303f-169">\***addresses_reserved** Number of addresses reserved</span></span>

<span data-ttu-id="2303f-170">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-170">**Return Values**</span></span>

- <span data-ttu-id="2303f-171">**NX_SUCCESS** (0x00) yayın iletisi başarıyla oluşturuldu ve işlendi</span><span class="sxs-lookup"><span data-stu-id="2303f-171">**NX_SUCCESS** (0x00) RELEASE message successfully created and processed</span></span>
- <span data-ttu-id="2303f-172">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xe95) geçersiz bir adres sağlandı</span><span class="sxs-lookup"><span data-stu-id="2303f-172">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) An invalid address is supplied</span></span>
- <span data-ttu-id="2303f-173">Sunucu adres listesinde **NX_DHCPV6_INVALID_IP_ADDRESS** (0xed1) başlangıç adresi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="2303f-173">**NX_DHCPV6_INVALID_IP_ADDRESS** (0xED1) Starting address not found in Server address list.</span></span>
- <span data-ttu-id="2303f-174">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-174">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-175">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-175">**Allowed From**</span></span>

<span data-ttu-id="2303f-176">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-176">Application Code</span></span>

<span data-ttu-id="2303f-177">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-177">**Example**</span></span>

```
/* Reserve a range of ip addresses in the Server address table for the server DHCPv6 
network interface. */

status = nx_dhcpv6_reserve_ip_address_range(&dhcp_server_0,
         &start_ipv6_address, &end_ipv6_address, &addresses_reserved);

/* If status is NX_SUCCESS one or more addresses were successfully reserved. */
```

## <a name="nx_dhcpv6_server_create"></a><span data-ttu-id="2303f-178">nx_dhcpv6_server_create</span><span class="sxs-lookup"><span data-stu-id="2303f-178">nx_dhcpv6_server_create</span></span>

### <a name="create-the-dhcpv6-server-instance"></a><span data-ttu-id="2303f-179">DHCPv6 sunucusu örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="2303f-179">Create the DHCPv6 Server instance</span></span> 

<span data-ttu-id="2303f-180">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-180">**Prototype**</span></span>

```
UINT nx_dhcpv6_server_create(NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
        NX_IP *ip_ptr, CHAR *name_ptr, 
        NX_PACKET_POOL *packet_pool_ptr, 
        VOID *stack_ptr,ULONG stack_size,
    VOID (*dhcpv6_address_declined_handler)(struct 
        NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
        NX_DHCPV6_CLIENT *dhcpv6_client_ptr, 
        UINT message),
    VOID (*dhcpv6_option_request_handler)(
        struct NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
        UINT option_request, UCHAR *buffer_ptr, UINT *index));
```

<span data-ttu-id="2303f-181">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-181">**Description**</span></span>

<span data-ttu-id="2303f-182">Bu hizmet, belirtilen girişe sahip DHCPv6 sunucusu görevini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2303f-182">This service creates the DHCPv6 Server task with the specified input.</span></span> <span data-ttu-id="2303f-183">Geri çağırma işleyicileri isteğe bağlı giriştir.</span><span class="sxs-lookup"><span data-stu-id="2303f-183">The callback handlers are optional input.</span></span> <span data-ttu-id="2303f-184">Yığın işaretçisi, IP örneği ve paket havuzu girişi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="2303f-184">The stack pointer, IP instance and packet pool input are required.</span></span> <span data-ttu-id="2303f-185">IP örneği ve paket havuzu zaten oluşturulmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2303f-185">The IP instance and packet pool must already be created.</span></span>

<span data-ttu-id="2303f-186">Kullanıcının, seçenek isteği işleyicisini ayarlamak için nx_dhcpv6_server_option_request_handler_set çağırması önerilir.</span><span class="sxs-lookup"><span data-stu-id="2303f-186">User is encouraged to call nx_dhcpv6_server_option_request_handler_set to set the option request handler.</span></span>

<span data-ttu-id="2303f-187">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-187">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-188">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-188">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-189">**ip_ptr** IP örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="2303f-189">**ip_ptr** Pointer to the IP instance</span></span>
- <span data-ttu-id="2303f-190">**name_str** Sunucu adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-190">**name_str** Pointer to Server name</span></span>
- <span data-ttu-id="2303f-191">**packet_pool_ptr** Sunucu paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-191">**packet_pool_ptr** Pointer to Server packet pool</span></span>
- <span data-ttu-id="2303f-192">**stack_ptr** Sunucu yığını belleği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-192">**stack_ptr** Pointer to Server stack memory</span></span>
- <span data-ttu-id="2303f-193">**stack_size** Sunucu yığını belleğinin boyutu</span><span class="sxs-lookup"><span data-stu-id="2303f-193">**stack_size** Size of Server stack memory</span></span>
- <span data-ttu-id="2303f-194">**dhcpv6_address_declined_handler** Istemci reddetme veya yayın iletisi işleyicisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-194">**dhcpv6_address_declined_handler** Pointer to Client Decline or Release message handler</span></span>
- <span data-ttu-id="2303f-195">**dhcpv6_option_request_handler** Seçenekler isteği seçenek işleyicisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-195">**dhcpv6_option_request_handler** Pointer to options request option handler</span></span>

<span data-ttu-id="2303f-196">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-196">**Return Values**</span></span>

- <span data-ttu-id="2303f-197">**NX_SUCCESS** (0x00) sunucu başarıyla sürdürüldü</span><span class="sxs-lookup"><span data-stu-id="2303f-197">**NX_SUCCESS** (0x00) Server successfully resumed</span></span>
- <span data-ttu-id="2303f-198">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-198">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>
- <span data-ttu-id="2303f-199">NX_DHCPV6_PARAM_ERROR işaretçi olmayan giriş geçersiz</span><span class="sxs-lookup"><span data-stu-id="2303f-199">NX_DHCPV6_PARAM_ERROR Invalid non pointer input</span></span>

<span data-ttu-id="2303f-200">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-200">**Allowed From**</span></span>

<span data-ttu-id="2303f-201">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-201">Application Code</span></span>

<span data-ttu-id="2303f-202">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-202">**Example**</span></span>

```
/* Create the DHCPv6 Server. */
status = nx_dhcpv6_server_create(&dhcp_server_0, &ip_0, "DHCPv6 Server",
         &pool_0, stack_pointer,2048, dhcpv6_decline_handler,
         dhcpv6_get_time_handler);
/* If status is NX_SUCCESS the Server successfully created. */
```

## <a name="nx_dhcpv6_server_delete"></a><span data-ttu-id="2303f-203">nx_dhcpv6_server_delete</span><span class="sxs-lookup"><span data-stu-id="2303f-203">nx_dhcpv6_server_delete</span></span>

### <a name="delete-the-dhcpv6-server"></a><span data-ttu-id="2303f-204">DHCPv6 sunucusunu silme</span><span class="sxs-lookup"><span data-stu-id="2303f-204">Delete the DHCPv6 Server</span></span>

<span data-ttu-id="2303f-205">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-205">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_delee(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

<span data-ttu-id="2303f-206">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-206">**Description**</span></span>

<span data-ttu-id="2303f-207">Bu hizmet, DHCPv6 sunucusu görevini ve sunucunun işlediği tüm istekleri siler.</span><span class="sxs-lookup"><span data-stu-id="2303f-207">This service deletes the DHCPv6 Server task and any request that the Server was processing.</span></span>

<span data-ttu-id="2303f-208">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-208">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-209">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-209">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="2303f-210">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-210">**Return Values**</span></span>

- <span data-ttu-id="2303f-211">**NX_SUCCESS** (0x00) sunucu başarıyla silindi</span><span class="sxs-lookup"><span data-stu-id="2303f-211">**NX_SUCCESS** (0x00) Server successfully deleted</span></span>
- <span data-ttu-id="2303f-212">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-212">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-213">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-213">**Allowed From**</span></span>

<span data-ttu-id="2303f-214">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="2303f-214">Threads</span></span>

<span data-ttu-id="2303f-215">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-215">**Example**</span></span>

```
/* Delete the DHCPv6 Serve. */
status = nx_dhcpv6_server_delete(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully deleted. */
```

## <a name="nx_dhcpv6_server_resume"></a><span data-ttu-id="2303f-216">nx_dhcpv6_server_resume</span><span class="sxs-lookup"><span data-stu-id="2303f-216">nx_dhcpv6_server_resume</span></span>

### <a name="resume-dhcpv6-server-task"></a><span data-ttu-id="2303f-217">DHCPv6 sunucusu görevini sürdürür</span><span class="sxs-lookup"><span data-stu-id="2303f-217">Resume DHCPv6 Server task</span></span> 

<span data-ttu-id="2303f-218">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-218">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_resume(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

<span data-ttu-id="2303f-219">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-219">**Description**</span></span>

<span data-ttu-id="2303f-220">Bu hizmet, DHCPv6 sunucusu görevini ve sunucunun işlediği tüm istekleri sürdürür.</span><span class="sxs-lookup"><span data-stu-id="2303f-220">This service resumes the DHCPv6 Server task and any request that the Server was processing.</span></span>

<span data-ttu-id="2303f-221">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-221">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-222">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-222">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="2303f-223">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-223">**Return Values**</span></span>

- <span data-ttu-id="2303f-224">**NX_SUCCESS** (0x00) sunucu başarıyla sürdürüldü</span><span class="sxs-lookup"><span data-stu-id="2303f-224">**NX_SUCCESS** (0x00) Server successfully resumed</span></span>
- <span data-ttu-id="2303f-225">**NX_DHCPV6_ALREADY_STARTED** (0xe91) sunucu zaten çalışıyor</span><span class="sxs-lookup"><span data-stu-id="2303f-225">**NX_DHCPV6_ALREADY_STARTED** (0xE91) Server is running already</span></span>
- <span data-ttu-id="2303f-226">**durum** (değişken) threadx ve NETX Duo hata durumu</span><span class="sxs-lookup"><span data-stu-id="2303f-226">**status** (variable) ThreadX and NetX Duo error status</span></span>
- <span data-ttu-id="2303f-227">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-227">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-228">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-228">**Allowed From**</span></span>

<span data-ttu-id="2303f-229">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="2303f-229">Threads</span></span>

<span data-ttu-id="2303f-230">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-230">**Example**</span></span>

```
/* Resume the DHCPv6 Server task. */
status = nx_dhcpv6_server_resume(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully resumed. */
```

## <a name="nx_dhcpv6_server_suspend"></a><span data-ttu-id="2303f-231">nx_dhcpv6_server_suspend</span><span class="sxs-lookup"><span data-stu-id="2303f-231">nx_dhcpv6_server_suspend</span></span>

### <a name="suspend-dhcpv6-server-task"></a><span data-ttu-id="2303f-232">DHCPv6 sunucusunu askıya al görevi</span><span class="sxs-lookup"><span data-stu-id="2303f-232">Suspend DHCPv6 Server task</span></span> 

<span data-ttu-id="2303f-233">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-233">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_suspend(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

<span data-ttu-id="2303f-234">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-234">**Description**</span></span>

<span data-ttu-id="2303f-235">Bu hizmet, DHCPv6 sunucusu görevini ve sunucunun işlediği tüm istekleri askıya alır.</span><span class="sxs-lookup"><span data-stu-id="2303f-235">This service suspends the DHCPv6 Server task and any request that the Server was processing.</span></span>

<span data-ttu-id="2303f-236">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-236">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-237">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-237">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="2303f-238">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-238">**Return Values**</span></span>

- <span data-ttu-id="2303f-239">**NX_SUCCESS** (0x00) sunucu başarıyla sürdürüldü</span><span class="sxs-lookup"><span data-stu-id="2303f-239">**NX_SUCCESS** (0x00) Server successfully resumed</span></span>
- <span data-ttu-id="2303f-240">**NX_DHCPV6_NOT_STARTED** (0xe92) sunucusu başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="2303f-240">**NX_DHCPV6_NOT_STARTED** (0xE92) Server is not started</span></span> 
- <span data-ttu-id="2303f-241">**Durum** (değişken) threadx ve NETX Duo hata durumu</span><span class="sxs-lookup"><span data-stu-id="2303f-241">**Status** (variable) ThreadX and NetX Duo error status</span></span>
- <span data-ttu-id="2303f-242">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-242">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-243">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-243">**Allowed From**</span></span>

<span data-ttu-id="2303f-244">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="2303f-244">Threads</span></span>

<span data-ttu-id="2303f-245">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-245">**Example**</span></span>

```
/* Suspend the DHCPv6 Server task. */
status = nx_dhcpv6_server_suspend(&dhcp_server_0);

/* If status is NX_SUCCESS the Server successfully suspended. */
```

## <a name="nx_dhcpv6_server_start"></a><span data-ttu-id="2303f-246">nx_dhcpv6_server_start</span><span class="sxs-lookup"><span data-stu-id="2303f-246">nx_dhcpv6_server_start</span></span>

### <a name="start-the-dhcpv6-server-task"></a><span data-ttu-id="2303f-247">DHCPv6 sunucusu görevini başlatın</span><span class="sxs-lookup"><span data-stu-id="2303f-247">Start the DHCPv6 Server task</span></span> 

<span data-ttu-id="2303f-248">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-248">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_start(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

<span data-ttu-id="2303f-249">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-249">**Description**</span></span>

<span data-ttu-id="2303f-250">Bu hizmet DHCPv6 sunucusu görevini başlatır ve DHCPv6 Istemci iletilerini almak için uygulama isteklerini işlemek üzere sunucuyu yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="2303f-250">This service starts the DHCPv6 Server task and readies the Server to process application requests for receiving DHCPv6 Client messages.</span></span> <span data-ttu-id="2303f-251">Sunucu örneğinin yeterli bilgilere sahip olduğunu doğrular (sunucu DUıD), DHCPv6 iletilerini göndermek ve almak için UDP yuvasını oluşturup bağlar ve oturum süresini ve IP Kiralama süre sonunu izlemek için zamanlayıcıları etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="2303f-251">It verifies the Server instance has sufficient information (Server DUID), creates and binds the UDP socket for sending and receiving DHCPv6 messages, and activates timers for keeping track of session time and IP lease expiration.</span></span>

>[!NOTE] 
> <span data-ttu-id="2303f-252">DHCPv6 sunucusunun çalıştırılabilmesi için, ana bilgisayar uygulaması, sunucunun IP adreslerini atayabileceği IP adresi aralığını oluşturmaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="2303f-252">Before the DHCPv6 Server can run, the host application is responsible for creating the IP address range from which the Server can assign IP addresses.</span></span> <span data-ttu-id="2303f-253">Ayrıca, sunucu DUıD ve DHCPv6 arabirimini ayarlamaktan de sorumludur (sırasıyla *nx_dhcpv6_server_duid_set* ve *nx_dhcpv6_server_interface_set* .</span><span class="sxs-lookup"><span data-stu-id="2303f-253">It is also responsible for setting the Server DUID and DHCPv6 interface (see *nx_dhcpv6_server_duid_set* and *nx_dhcpv6_server_interface_set* respectively.</span></span>

<span data-ttu-id="2303f-254">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-254">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-255">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-255">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="2303f-256">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-256">**Return Values**</span></span>

- <span data-ttu-id="2303f-257">**NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="2303f-257">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="2303f-258">**NX_DHCPV6_ALREADY_STARTED** (0xe91) sunucu zaten çalışıyor</span><span class="sxs-lookup"><span data-stu-id="2303f-258">**NX_DHCPV6_ALREADY_STARTED** (0xE91) Server is running already</span></span>
- <span data-ttu-id="2303f-259">**NX_DHCPV6_NO_ASSIGNABLE_ADDRESSES** (0xea7) sunucusunda kiralamaya atanabilen bir adres yok</span><span class="sxs-lookup"><span data-stu-id="2303f-259">**NX_DHCPV6_NO_ASSIGNABLE_ADDRESSES** (0xEA7) Server has no assignable addresses to lease</span></span>
- <span data-ttu-id="2303f-260">**NX_DHCPV6_INVALID_GLOBAL_INDEX** (0xe97) genel adres dizini ayarlanmadı</span><span class="sxs-lookup"><span data-stu-id="2303f-260">**NX_DHCPV6_INVALID_GLOBAL_INDEX** (0xE97) Global address index not set</span></span>
- <span data-ttu-id="2303f-261">**NX_DHCPV6_NO_SERVER_DUID** (0xe92) sunucu DUID oluşturulmadı</span><span class="sxs-lookup"><span data-stu-id="2303f-261">**NX_DHCPV6_NO_SERVER_DUID** (0xE92) No Server DUID created</span></span> 
- <span data-ttu-id="2303f-262">**durum** (değişken) threadx ve NETX Duo hata durumu</span><span class="sxs-lookup"><span data-stu-id="2303f-262">**status** (variable) ThreadX and NetX Duo error status</span></span>
- <span data-ttu-id="2303f-263">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-263">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-264">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-264">**Allowed From**</span></span>

<span data-ttu-id="2303f-265">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="2303f-265">Threads</span></span>

<span data-ttu-id="2303f-266">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-266">**Example**</span></span>

```
/* Start the DHCPv6 Server task. */
status = nx_dhcpv6_server_start(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully started. */
```

## <a name="nx_dhcpv6_retrieve_ip_address_lease"></a><span data-ttu-id="2303f-267">nx_dhcpv6_retrieve_ip_address_lease</span><span class="sxs-lookup"><span data-stu-id="2303f-267">nx_dhcpv6_retrieve_ip_address_lease</span></span>

### <a name="get-an-ip-address-lease-from-the-server-table"></a><span data-ttu-id="2303f-268">Sunucu tablosundan bir IP adresi kirası al</span><span class="sxs-lookup"><span data-stu-id="2303f-268">Get an IP address lease from the Server table</span></span>

<span data-ttu-id="2303f-269">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-269">**Prototype**</span></span>

```
UINT _nx_dhcpv6_retrieve_ip_address_lease(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, UINT table_index, 
     NXD_ADDRESS *lease_IP_address, ULONG *T1, ULONG *T2, 
     ULONG *valid_lifetime, ULONG *preferred_lifetime)
```

<span data-ttu-id="2303f-270">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-270">**Description**</span></span>

<span data-ttu-id="2303f-271">Bu hizmet, belirtilen tablo dizini konumundaki sunucu tablosundan bir IP adresi kiralama kaydı alır.</span><span class="sxs-lookup"><span data-stu-id="2303f-271">This service retrieves an IP address lease record from the Server table at the specified table index location.</span></span> <span data-ttu-id="2303f-272">Bu işlem, Istemci kaydı verilerinin alınmadan önce veya sonra yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="2303f-272">This can be done before or after retrieving Client record data.</span></span>

<span data-ttu-id="2303f-273">DHCPv6 sunucusu ile geçici olmayan bellek arasında veri depolama ve alma özelliği, DHCPv6 protokolünün bir gereksinimidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-273">The capability of storing and retrieving data between the DHCPv6 Server and non volatile memory is a requirement of the DHCPv6 protocol.</span></span> <span data-ttu-id="2303f-274">IP Kiralama verilerinin ve Istemci kayıt verilerinin kalıcı olmayan belleğe kaydedildiği sırada farklılık yapmaz.</span><span class="sxs-lookup"><span data-stu-id="2303f-274">It makes no difference in what order IP lease data and Client record data is saved to nonvolatile memory.</span></span>

>[!NOTE] 
> <span data-ttu-id="2303f-275">Önce DHCPv6 sunucusunu durdurmadan veya askıya almadan sunucu tablolarına veya sunucudan veri kopyalanması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="2303f-275">It is not recommended to copy data to or from Server tables without stopping or suspending the DHCPv6 Server first.</span></span>

<span data-ttu-id="2303f-276">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-276">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-277">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-277">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-278">**table_index** Kira depolanacak tablo dizini</span><span class="sxs-lookup"><span data-stu-id="2303f-278">**table_index** Table index to store lease at</span></span>
- <span data-ttu-id="2303f-279">**lease_IP_address** Istemciye kiralanan IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-279">**lease_IP_address** Pointer to IP address leased to the Client</span></span>
- <span data-ttu-id="2303f-280">**T1** İstemci yenileme süresi istedi</span><span class="sxs-lookup"><span data-stu-id="2303f-280">**T1** Client requested renew time</span></span>
- <span data-ttu-id="2303f-281">**T2** İstemci yeniden bağlama süresi istedi</span><span class="sxs-lookup"><span data-stu-id="2303f-281">**T2** Client requested rebind time</span></span>
- <span data-ttu-id="2303f-282">**valid_lifetime** İstemci kirası kullanım dışı duruma geliyor</span><span class="sxs-lookup"><span data-stu-id="2303f-282">**valid_lifetime** Client lease becomes deprecated</span></span>
- <span data-ttu-id="2303f-283">**preferred_lifetime** İstemci kirası geçersiz hale geliyor</span><span class="sxs-lookup"><span data-stu-id="2303f-283">**preferred_lifetime** Client lease becomes invalid</span></span>

<span data-ttu-id="2303f-284">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-284">**Return Values**</span></span>

- <span data-ttu-id="2303f-285">**NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="2303f-285">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="2303f-286">**NX_DHCPV6_PARAMETER_ERROR** (0xe93) geçersiz IP Kiralama verileri girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-286">**NX_DHCPV6_PARAMETER_ERROR** (0xE93) Invalid IP lease data input</span></span>
- <span data-ttu-id="2303f-287">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-287">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-288">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-288">**Allowed From**</span></span>

<span data-ttu-id="2303f-289">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-289">Application code</span></span>

<span data-ttu-id="2303f-290">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-290">**Example**</span></span>

```
/* Retrieve the DHCPv6 Server lease data. */
For (I = 0; I < NX_DHCPV6_MAX_LEASES; i++)
{
    /* Get the next lease record. */
    status = nx_dhcpv6_server_startdhcpv6_server_ptr, i, &next_ipv6_address, &T1,
             &T2, &preferred_lifetime, &valid_lifetime);
    /* The host application then saves this record to memory.
}
/* If status is NX_SUCCESS the Server data is successfully downloaded. */
```

## <a name="nx_dhcpv6_add_ip_address_lease"></a><span data-ttu-id="2303f-291">nx_dhcpv6_add_ip_address_lease</span><span class="sxs-lookup"><span data-stu-id="2303f-291">nx_dhcpv6_add_ip_address_lease</span></span>

### <a name="add-an-ip-address-lease-to-the-server-table"></a><span data-ttu-id="2303f-292">Sunucu tablosuna bir IP adresi kirası ekleyin</span><span class="sxs-lookup"><span data-stu-id="2303f-292">Add an IP address lease to the Server table</span></span>

<span data-ttu-id="2303f-293">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-293">**Prototype**</span></span>

```
UINT _nx_dhcpv6_add_ip_address_lease(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, UINT table_index, NXD_ADDRESS *lease_IP_address, ULONG T1, ULONG T2, 
     ULONG valid_lifetime, ULONG preferred_lifetime)
```

<span data-ttu-id="2303f-294">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-294">**Description**</span></span>

<span data-ttu-id="2303f-295">Bu hizmet, önceki bir DHCPv6 sunucu oturumundan gelen IP Kiralama verilerini geçici olmayan bellekten sunucu kiralama tablosuna yükler.</span><span class="sxs-lookup"><span data-stu-id="2303f-295">This service loads IP lease data from a previous DHCPv6 Server session from non volatile memory to the Server lease table.</span></span> <span data-ttu-id="2303f-296">Sunucu ilk kez çalışıyorsa ve önceki kira verisi yoksa, bu gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2303f-296">This is not necessary if the Server is running for the first time and has no previous lease data.</span></span> <span data-ttu-id="2303f-297">Bu durum, ana bilgisayar uygulamasının IP adreslerini atamak için *nx_dhcpv6_create_ip_address_range* hizmetini kullanarak bir IP adresi aralığı oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2303f-297">If this is the case the host application must create an IP address range for assigning IP addresses, using the *nx_dhcpv6_create_ip_address_range* service.</span></span> <span data-ttu-id="2303f-298">Veriler, bir DHCPv6 Kiralama kaydını yeniden oluşturmak için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-298">The data is sufficient to reconstruct a DHCPv6 lease record.</span></span> <span data-ttu-id="2303f-299">Tablo dizini belirtilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-299">The table index need not be specified.</span></span> <span data-ttu-id="2303f-300">0xFFFFFFFF (Infinity) olarak ayarlandıysa, DHCPv6 sunucusu, verileri kopyalamak için kullanılabilecek bir sonraki yuvayı bulur.</span><span class="sxs-lookup"><span data-stu-id="2303f-300">If set to 0xFFFFFFFF (infinity) the DHCPv6 Server will find the next available slot to copy the data to.</span></span>

>[!NOTE] 
> <span data-ttu-id="2303f-301">Istemci kayıtları karşıya yüklenmeden önce IP kira verilerinin yüklenmesi yapılmalıdır; yalnızca DHCPv6 sunucusu başlatılmadan önce (yeniden) yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2303f-301">Uploading IP lease data MUST be done before uploading Client records; both MUST be done before (re)starting the DHCPv6 Server.</span></span>

<span data-ttu-id="2303f-302">DHCPv6 sunucusu ile geçici olmayan bellek arasında veri depolama ve alma özelliği, DHCPv6 protokolünün bir gereksinimidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-302">The capability of storing and retrieving data between the DHCPv6 Server and non volatile memory is a requirement of the DHCPv6 protocol.</span></span>

<span data-ttu-id="2303f-303">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-303">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-304">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-304">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-305">**table_index** Kira depolanacak tablo dizini</span><span class="sxs-lookup"><span data-stu-id="2303f-305">**table_index** Table index to store lease at</span></span>
- <span data-ttu-id="2303f-306">**lease_IP_address** Istemciye kiralanan IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-306">**lease_IP_address** Pointer to IP address leased to the Client</span></span>
- <span data-ttu-id="2303f-307">**T1** İstemci yenileme süresi istedi</span><span class="sxs-lookup"><span data-stu-id="2303f-307">**T1** Client requested renew time</span></span>
- <span data-ttu-id="2303f-308">**T2** İstemci yeniden bağlama süresi istedi</span><span class="sxs-lookup"><span data-stu-id="2303f-308">**T2** Client requested rebind time</span></span>
- <span data-ttu-id="2303f-309">**valid_lifetime** İstemci kirası kullanım dışı duruma geliyor</span><span class="sxs-lookup"><span data-stu-id="2303f-309">**valid_lifetime** Client lease becomes deprecated</span></span>
- <span data-ttu-id="2303f-310">**preferred_lifetime** İstemci kirası geçersiz hale geliyor</span><span class="sxs-lookup"><span data-stu-id="2303f-310">**preferred_lifetime** Client lease becomes invalid</span></span>

<span data-ttu-id="2303f-311">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-311">**Return Values**</span></span>

- <span data-ttu-id="2303f-312">**NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="2303f-312">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="2303f-313">**NX_DHCPV6_TABLE_FULL** (0xec4) daha fazla kira verisi Için boşluk yok \* \*</span><span class="sxs-lookup"><span data-stu-id="2303f-313">**NX_DHCPV6_TABLE_FULL** (0xEC4) No room for more lease data\*\*</span></span>
- <span data-ttu-id="2303f-314">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xe95) kira verisi sunucu DHCPv6 arabirimiyle bağlantılı olarak görünmüyor</span><span class="sxs-lookup"><span data-stu-id="2303f-314">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) Lease data does not appear to be on link with Server DHCPv6 interface</span></span>
- <span data-ttu-id="2303f-315">**NX_DHCPV6_PARAM_ERROR** (0xe93) geçersiz IP Kiralama verileri girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-315">**NX_DHCPV6_PARAM_ERROR** (0xE93) Invalid IP lease data input</span></span>
- <span data-ttu-id="2303f-316">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-316">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-317">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-317">**Allowed From**</span></span>

<span data-ttu-id="2303f-318">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-318">Application code</span></span>

<span data-ttu-id="2303f-319">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-319">**Example**</span></span>

```
/* Copy the IP lease data to the Server address table. Note that the table index
is defaulted to 0xFFFFFFFF meaning the DHCPv6 Server will find an empty slot 
for each lease. */

    For(I = 0; I < NX_DHCPV6_MAX_LEASES; i++)
    {
        status = nx_dhcpv6_add_ip_address_lease(dhcpv6_server_ptr, 0xFFFFFFFF,
                 &next_ipv6_address, &T1, &T2, &preferred_lifetime, &valid_lifetime);
        /* Get the next lease address from memory… */
    }
    
    /* If status is NX_SUCCESS the lease data was successfully uploaded. It is opk
    to add the Client records to the Server table now. */
```

## <a name="nx_dhcpv6_add_client_record"></a><span data-ttu-id="2303f-320">nx_dhcpv6_add_client_record</span><span class="sxs-lookup"><span data-stu-id="2303f-320">nx_dhcpv6_add_client_record</span></span>

### <a name="add-a-client-record-to-the-server-table"></a><span data-ttu-id="2303f-321">Sunucu tablosuna bir Istemci kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="2303f-321">Add a Client record to the Server table</span></span>

<span data-ttu-id="2303f-322">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-322">**Prototype**</span></span>

```
UINT _nx_dhcpv6_add_client_record(NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT table_index, ULONG message_xid, 
     NXD_ADDRESS *client_address, UINT client_state, 
     ULONG IP_lease_time_accrued, ULONG valid_lifetime, UINT duid_type, UINTduid_hardware, 
     ULONG physical_address_msw, ULONG physical_address_lsw, ULONG duid_time, 
     ULONG duid_vendor_number, UCHAR *duid_vendor_private, UINT duid_private_length)
```

<span data-ttu-id="2303f-323">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-323">**Description**</span></span>

<span data-ttu-id="2303f-324">Bu hizmet, Istemci verilerini geçici olmayan bellekten sunucu tablosuna tek seferde kopyalar.</span><span class="sxs-lookup"><span data-stu-id="2303f-324">This service copies Client data from non volatile memory to the Server table one record at a time.</span></span> <span data-ttu-id="2303f-325">Bu, yalnızca sunucu yeniden başlatılırsa ve bellekten geri yüklemek için önceki bir oturumdan Istemci verilerinin bulunduğu durumlarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-325">This is only necessary if the Server is being rebooted and has Client data from a previous session to restore from memory.</span></span> <span data-ttu-id="2303f-326">Bir sunucuda önceki veriler yoksa, DHCPv6 sunucusu istemci kayıtları eklemek için Istemci tablosunu başlatır.</span><span class="sxs-lookup"><span data-stu-id="2303f-326">If a Server has no previous data, the DHCPv6 Server will initialize the Client table to be able for adding Client records.</span></span>

<span data-ttu-id="2303f-327">Tablo dizinini belirtmek gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2303f-327">It is not necessary to specify the table index.</span></span> <span data-ttu-id="2303f-328">0xFFFFFFFF (Infinity) olarak ayarlandıysa, DHCPv6 sunucusu bir sonraki kullanılabilir yuvayı bulur.</span><span class="sxs-lookup"><span data-stu-id="2303f-328">If set to 0xFFFFFFFF (infinity) the DHCPv6 Server will locate the next available slot.</span></span> <span data-ttu-id="2303f-329">DHCPv6 sunucusu, bu verilerden bir Istemci kaydını yeniden oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="2303f-329">The DHCPv6 Server can reconstruct a Client record from this data.</span></span>

>[!NOTE] 
> <span data-ttu-id="2303f-330">Ana bilgisayar uygulamasının, Istemci kaydından önce IP Kiralama verilerini yüklemesi gerekır.</span><span class="sxs-lookup"><span data-stu-id="2303f-330">The host application MUST upload the IP lease data BEFORE the Client record data.</span></span> <span data-ttu-id="2303f-331">Bu sayede, her bir Istemci kaydının ilgili tablolarında karşılık gelen IP Kiralama kaydıyla birleştirilebilecek şekilde, DHCPv6 sunucusunun tabloları çapraz bir şekilde bağlantısı sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2303f-331">This is so that internally the DHCPv6 Server can cross link the tables so that each Client record is joined with its corresponding IP lease record in their respective tables.</span></span> <span data-ttu-id="2303f-332">Bellekten IP Kiralama verilerini karşıya yükleme hakkında ayrıntılı bilgi için bkz. *nx_dhcpv6_add_ip_address_lease* .</span><span class="sxs-lookup"><span data-stu-id="2303f-332">See *nx_dhcpv6_add_ip_address_lease* for details on uploading IP lease data from memory.</span></span>

>[!NOTE] 
> <span data-ttu-id="2303f-333">DUıD türüne bağlı olarak, tüm verilerin sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2303f-333">Depending on DUID type, not all data must be supplied.</span></span> <span data-ttu-id="2303f-334">Örneğin, bir Istemcide bir satıcı atanmış DUıD türü varsa, bu, DUıD bağlantı katmanı parametreleri (MAC adresi, donanım türü, DUıD saati) için sıfır olarak gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="2303f-334">For example if a Client has a vendor assigned DUID type, it can send in zero for DUID Link Layer parameters (MAC address, hardware type, DUID time).</span></span>

<span data-ttu-id="2303f-335">DHCPv6 sunucusu ile geçici olmayan bellek arasında veri depolama ve alma özelliği, DHCPv6 protokolünün bir gereksinimidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-335">The capability of storing and retrieving data between the DHCPv6 Server and non volatile memory is a requirement of the DHCPv6 protocol.</span></span>

<span data-ttu-id="2303f-336">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-336">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-337">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-337">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="2303f-338">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-338">**Return Values**</span></span>

- <span data-ttu-id="2303f-339">**NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="2303f-339">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="2303f-340">**NX_ INVALID_PARAMETERS** (0x4D) geçersiz işaretçi girişi \* \*</span><span class="sxs-lookup"><span data-stu-id="2303f-340">**NX_ INVALID_PARAMETERS** (0x4D) Invalid non pointer input\*\*</span></span>
- <span data-ttu-id="2303f-341">**NX_DHCPV6_TABLE_FULL** (0xec4) başka bir istemci kaydı eklemek için boş yuva kalmadı</span><span class="sxs-lookup"><span data-stu-id="2303f-341">**NX_DHCPV6_TABLE_FULL** (0xEC4) No empty slots left for adding another Client record</span></span>
- <span data-ttu-id="2303f-342">**NX_DHCPV6_ADDRESS_NOT_FOUND** (0xea8) istemci tarafından atanan adres sunucu kira tablosunda bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="2303f-342">**NX_DHCPV6_ADDRESS_NOT_FOUND** (0xEA8) Client assigned address not found in Server lease table.</span></span>
- <span data-ttu-id="2303f-343">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-343">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-344">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-344">**Allowed From**</span></span>

<span data-ttu-id="2303f-345">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-345">Application code</span></span>

<span data-ttu-id="2303f-346">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-346">**Example**</span></span>

```
/*Add the IP lease data and Client records back to the server before starting
theServer. */
    /* Copy the 'lease data' to the server table FIRST. */
for (i = 0; i< NX_DHCPV6_MAX_LEASES; i++)
    {

        /* Add the next lease record. Let the server find the next
        available slot. */
        status = nx_dhcpv6_add_ip_address_lease(dhcpv6_server_ptr,
                 0xFFFFFFFF,,&next_ipv6_address, NX_DHCPV6_DEFAULT_T1_TIME, 
                 NX_DHCPV6_DEFAULT_T2_TIME, NX_DHCPV6_DEFAULT_PREFERRED_TIME, 
                 NX_DHCPV6_DEFAULT_VALID_TIME);
if (status != NX_SUCCESS)
return status;
        /* Get the next IP lease record from memory. */
        …
    }
    /* Copy the client records to the Server table NEXT.
    for (i = 0; i< NX_DHCPV6_MAX_LEASES; i++)
    {
        /* Add the next client record. Let the server find the next
        available slot. */
        status = nx_dhcpv6_add_client_record(dhcpv6_server_ptr, 0xFFFFFFFF,
                 message_xid, &client_ipv6_address, NX_DHCPV6_STATE_BOUND,
                 IP_lifetime_time_accrued, valid_lifetime, duid_type, 
                 duid_hardware, physical_address_msw, physical_address_lsw, 
                 duid_time, 0, NX_NULL, 0);
if (status != NX_SUCCESS)
return status;
        /* Get the next Client record from memory. */
        …
    }

/* If status is NX_SUCCESS the Server data was successfully restored and 
it is ok to start the DHCPv6 server now. */
```

## <a name="nx_dhcpv6_retrieve_client_record"></a><span data-ttu-id="2303f-347">nx_dhcpv6_retrieve_client_record</span><span class="sxs-lookup"><span data-stu-id="2303f-347">nx_dhcpv6_retrieve_client_record</span></span>

### <a name="retrieve-a-client-record-from-the-server-table"></a><span data-ttu-id="2303f-348">Sunucu tablosundan bir Istemci kaydı alma</span><span class="sxs-lookup"><span data-stu-id="2303f-348">Retrieve a Client record from the Server table</span></span>

<span data-ttu-id="2303f-349">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-349">**Prototype**</span></span>

```
UINT _nx_dhcpv6_retrieve_client_record(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT table_index, ULONG *message_xid, 
     NXD_ADDRESS *client_address, UINT *client_state, 
     ULONG IP_lease_time_accrued, 
     ULONG *valid_lifetime, UINT *duid_type, 
     UINT *duid_hardware, ULONG *physical_address_msw, 
     ULONG *physical_address_lsw, ULONG *duid_time, 
     ULONG *duid_vendor_number, 
     UCHAR *duid_vendor_private, 
     UINT *duid_private_length)
```

<span data-ttu-id="2303f-350">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-350">**Description**</span></span>

<span data-ttu-id="2303f-351">Bu hizmet, gerekli verileri depolama için sunucunun Istemci kayıt tablosundan geçici olmayan belleğe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="2303f-351">This service copies the essential data from the Server’s Client record table for storage to non-volatile memory.</span></span> <span data-ttu-id="2303f-352">Sunucu, ters işlemdeki (sunucu tablosuna verileri karşıya yükleme) bu tür verilerden yeterli bir Istemci kaydını yeniden oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="2303f-352">The Server can reconstruct an adequate Client record from such data in the reverse process (uploading data to the Server table).</span></span> <span data-ttu-id="2303f-353">DUıD türünden bağımsız olarak işaretçilerin hiçbiri NULL işaretçiler olamaz; veriler tüm parametreler için sıfır olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="2303f-353">Regardless of the DUID type, none of the pointers can be NULL pointers; data is initialized to zero for all parameters.</span></span> <span data-ttu-id="2303f-354">Örneğin, Istemci DUıD türü bağlantı katmanı ve zaman ise, satıcı numarası sıfır olarak döndürülür ve özel KIMLIK boş bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="2303f-354">For example, if the Client DUID type is Link Layer Plus Time, the vendor number is returned as zero and the private ID is an empty string.</span></span>

<span data-ttu-id="2303f-355">DHCPv6 sunucusu ile geçici olmayan bellek arasında veri depolama ve alma özelliği, DHCPv6 protokolünün bir gereksinimidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-355">The capability of storing and retrieving data between the DHCPv6 Server and non volatile memory is a requirement of the DHCPv6 protocol.</span></span> <span data-ttu-id="2303f-356">IP Kiralama verilerinin ve Istemci kayıt verilerinin kalıcı olmayan belleğe kaydedildiği sırada farklılık yapmaz.</span><span class="sxs-lookup"><span data-stu-id="2303f-356">It makes no difference in what order IP lease data and Client record data is saved to nonvolatile memory.</span></span>

>[!NOTE] 
> <span data-ttu-id="2303f-357">Önce DHCPv6 sunucusunu durdurmadan veya askıya almadan sunucu tablolarına veya sunucudan veri kopyalanması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="2303f-357">It is not recommended to copy data to or from Server tables without stopping or suspending the DHCPv6 Server first.</span></span>

<span data-ttu-id="2303f-358">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-358">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-359">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-359">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-360">**table_index** Sunucunun istemci tablosuna Dizin</span><span class="sxs-lookup"><span data-stu-id="2303f-360">**table_index** Index into Server’s client table</span></span>
- <span data-ttu-id="2303f-361">**message_xid** İstemci sunucusu Işlem KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="2303f-361">**message_xid** Client Server Transaction ID</span></span>
- <span data-ttu-id="2303f-362">**client_address** Istemciye kiralanan IPv6 adresi</span><span class="sxs-lookup"><span data-stu-id="2303f-362">**client_address** IPv6 address leased to Client</span></span>
- <span data-ttu-id="2303f-363">**client_state** İstemci DHCPv6 durumu (örn. bağlantılı)</span><span class="sxs-lookup"><span data-stu-id="2303f-363">**client_state** Client DHCPv6 state (e.g. bound)</span></span>
- <span data-ttu-id="2303f-364">**IP_lease_time_accrued** DHCPv6 sunucusuna yönelik işaretçinin zaten **dhcpv6_server_ptr** kira süresi geçildi</span><span class="sxs-lookup"><span data-stu-id="2303f-364">**IP_lease_time_accrued** Time expired on lease already **dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-365">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-365">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="2303f-366">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-366">**Return Values**</span></span>

- <span data-ttu-id="2303f-367">**NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="2303f-367">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="2303f-368">**NX_DHCPV6_INVALID_DUID** (0xecc) geçersiz veya tutarsız DUID verileri</span><span class="sxs-lookup"><span data-stu-id="2303f-368">**NX_DHCPV6_INVALID_DUID** (0xECC) Invalid or inconsistent DUID data</span></span>
- <span data-ttu-id="2303f-369">**NX_PTR_ERROR** (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-369">**NX_PTR_ERROR** (0x16) Invalid pointer input</span></span>
- <span data-ttu-id="2303f-370">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-370">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

<span data-ttu-id="2303f-371">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-371">**Allowed From**</span></span>

<span data-ttu-id="2303f-372">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-372">Application code</span></span>

<span data-ttu-id="2303f-373">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-373">**Example**</span></span>

```
/* Retrieve the Client records from the DHCPv6 Server table. */
For (i = 0; i< NX_MAX_DHCPV6_CLIENTS; i++)
{
    status = nx_dhcpv6_retrieve_client_recorddhcpv6_server_ptr, i, &message_xid,
             &client_ipv6_address, &client_state, &IP_lifetime_time_accrued, 
             valid_lifetime, &duid_type, &duid_hardware, &physical_address_msw,
             &physical_address_lsw, &duid_time, &duid_vendor_number, &private_id[0], 
             &length);
    /* The host application can save this data to memory now.
}
/* If status is NX_SUCCESS the Server successfully started. */
```

## <a name="nx_dhcpv6_server_interface_set"></a><span data-ttu-id="2303f-374">nx_dhcpv6_server_interface_set</span><span class="sxs-lookup"><span data-stu-id="2303f-374">nx_dhcpv6_server_interface_set</span></span>

### <a name="setthe-interface-index-for-server-dhcpv6-interface"></a><span data-ttu-id="2303f-375">Sunucu DHCPv6 arabirimi için arabirim dizinini ayarla</span><span class="sxs-lookup"><span data-stu-id="2303f-375">Setthe interface index for Server DHCPv6 interface</span></span>

<span data-ttu-id="2303f-376">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-376">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_interface_set(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT iface_index, UINT ga_address_index)
```

<span data-ttu-id="2303f-377">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-377">**Description**</span></span>

<span data-ttu-id="2303f-378">Bu hizmet, DHCPv6 sunucusunun DHCPv6 Istemci isteklerini işlediği ağ arabirimini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2303f-378">This service sets the network interface on which the DHCPv6 Server handles DHCPv6 Client requests.</span></span> <span data-ttu-id="2303f-379">Birden çok giriş desteği olmayan NetX Duo sürümleri için, arabirim değeri varsayılan olarak sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="2303f-379">Not that for versions of NetX Duo that do not support multihome, the interface value is defaulted to zero.</span></span> <span data-ttu-id="2303f-380">Genel Adres dizini, DHCPv6 arabiriminde sunucu genel adresini elde etmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-380">The global address index is necessary to obtain the Server global address on its DHCPv6 interface.</span></span> <span data-ttu-id="2303f-381">Bu, kira adreslerinin ve diğer DHCPv6 verilerinin DHCPv6 sunucusuyla bağlantılı olduğundan emin olmak için DHCPv6 mantığı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2303f-381">This is used by the DHCPv6 logic to ensure that lease addresses and other DHCPv6 data is on link with the DHCPv6 Server.</span></span>

<span data-ttu-id="2303f-382">Bu, tek bağlantılı cihazlardaki uygulamalar veya çok giriş desteği olmadan, DHCPv6 sunucusu başlatılmadan önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2303f-382">This must be called before the DHCPv6 server is started, even for applications on single homed devices or without multihome support.</span></span>

<span data-ttu-id="2303f-383">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-383">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-384">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-384">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-385">**iface_index** Sunucu DHCPv6 sunucu arabirimi</span><span class="sxs-lookup"><span data-stu-id="2303f-385">**iface_index** Server DHCPv6 Server interface</span></span>
- <span data-ttu-id="2303f-386">**ga_address_index** Sunucu IP örnek adresi tablosundaki sunucu genel adresinin dizini</span><span class="sxs-lookup"><span data-stu-id="2303f-386">**ga_address_index** Index of Server global address in the Server IP instance address table</span></span>

<span data-ttu-id="2303f-387">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-387">**Return Values**</span></span>

- <span data-ttu-id="2303f-388">**NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı</span><span class="sxs-lookup"><span data-stu-id="2303f-388">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="2303f-389">**NX_INVALID_INTERFACE** (0x4C) arabirimi yok</span><span class="sxs-lookup"><span data-stu-id="2303f-389">**NX_INVALID_INTERFACE** (0x4C) Interface does not exist</span></span>
- <span data-ttu-id="2303f-390">NX_NO_INTERFACE_ADDRESS (0x50) Genel dizin, IP örneği en fazla IPv6 adresini aşıyor (NX_MAX_IPV6_ADDRESSES)</span><span class="sxs-lookup"><span data-stu-id="2303f-390">NX_NO_INTERFACE_ADDRESS (0x50) Global index exceeds the IP instance maximum IPv6 addresses (NX_MAX_IPV6_ADDRESSES)</span></span>
- <span data-ttu-id="2303f-391">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-391">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-392">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-392">**Allowed From**</span></span>

<span data-ttu-id="2303f-393">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-393">Application code</span></span>

<span data-ttu-id="2303f-394">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-394">**Example**</span></span>

```
/* Set the Server DHCPv6 interface to the primary interface. The global IP 
address is at the index 1 in the IP address table. */
status = nx_dhcpv6_server_interface_set(&dhcp_server_0, 0, 1);

/* If status is NX_SUCCESS the Server interface is successfully set. */
```
## <a name="nx_dhcpv6_set_server_duid"></a><span data-ttu-id="2303f-395">nx_dhcpv6_set_server_duid</span><span class="sxs-lookup"><span data-stu-id="2303f-395">nx_dhcpv6_set_server_duid</span></span>

### <a name="set-the-server-duid-for-dhcpv6-packets"></a><span data-ttu-id="2303f-396">DHCPv6 paketleri için sunucu DUıD 'sini ayarlama</span><span class="sxs-lookup"><span data-stu-id="2303f-396">Set the Server DUID for DHCPv6 packets</span></span>

<span data-ttu-id="2303f-397">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-397">**Prototype**</span></span>

```
UINT _nx_dhcpv6_set_server_duid(NX_DHCPV6_SERVER *dhcpv6_server_ptr,
     UINT duid_type, UINT hardware_type, 
     ULONG mac_address_msw, ULONG mac_address_lsw, 
     ULONG time)
```

<span data-ttu-id="2303f-398">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-398">**Description**</span></span>

<span data-ttu-id="2303f-399">Bu hizmet, sunucu DUıD 'yi ayarlar ve konak uygulama sunucuyu başlamadan önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2303f-399">This service sets the Server DUID and must be called before the host application starts the Server.</span></span> <span data-ttu-id="2303f-400">Bağlantı katmanı ve bağlantı katmanı zaman DUıD türleri için, ana bilgisayar uygulamasının donanım türü ve MAC adresi verilerini sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2303f-400">For link layer and link layer time DUID types, the host application must supply the hardware type and MAC address data.</span></span> <span data-ttu-id="2303f-401">Bağlantı katmanı zaman DUID 'Leri için zaman işaretçisi geçerli bir saate işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-401">For link layer time DUIDs, the time pointer must point to a valid time.</span></span> <span data-ttu-id="2303f-402">1 Ocak 2000 ' den beri geçen saniye sayısı tipik bir çekirdek değerdir.</span><span class="sxs-lookup"><span data-stu-id="2303f-402">The number of seconds since Jan 1, 2000 is a typical seed value.</span></span> <span data-ttu-id="2303f-403">Sunucu DUıD türü kurumsal, satıcıya atanmış tür ise, DUıD Kullanıcı yapılandırılabilir seçenekleri NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID ve NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID oluşturulur ve zaman ve MAC adresi değerleri NULL olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2303f-403">If the Server DUID type is the enterprise, vendor assigned type, the DUID will be created from the user configurable options NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID and NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID, and the time and MAC address values can be set to NULL.</span></span>

>[!NOTE] 
> <span data-ttu-id="2303f-404">Sunucu DUıD parametrelerini, yeniden başlatmalar arasındaki Istemcilere yönelik iletilerde aynı DUıD 'yi kullanacak şekilde kalıcı belleğe kaydetmek, ana bilgisayar uygulamasının sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="2303f-404">It is the host application’s responsibility to save the Server DUID parameters to nonvolatile memory such that it uses the same DUID in messages to Clients between reboots.</span></span> <span data-ttu-id="2303f-405">Bu, DHCPv6 protokolünün (RFC 3315) bir gereksinimidir.</span><span class="sxs-lookup"><span data-stu-id="2303f-405">This is a requirement of the DHCPv6 protocol (RFC 3315).</span></span>

<span data-ttu-id="2303f-406">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-406">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-407">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-407">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-408">**duid_type** DHCPv6 sunucusu DUıD türü</span><span class="sxs-lookup"><span data-stu-id="2303f-408">**duid_type** DHCPv6 Server DUID type</span></span>
- <span data-ttu-id="2303f-409">**hardware_type** Donanım türü (örneğin, Ethernet)</span><span class="sxs-lookup"><span data-stu-id="2303f-409">**hardware_type** Hardware type (e.g. Ethernet)</span></span>
- <span data-ttu-id="2303f-410">**mac_address_msw** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-410">**mac_address_msw** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-411">**mac_address_lsw** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-411">**mac_address_lsw** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-412">**zaman** DUıD için saat değeri</span><span class="sxs-lookup"><span data-stu-id="2303f-412">**time** Time value for DUID</span></span>

<span data-ttu-id="2303f-413">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-413">**Return Values**</span></span>

- <span data-ttu-id="2303f-414">**NX_SUCCESS** (0x00) sunucu başarıyla askıya alındı</span><span class="sxs-lookup"><span data-stu-id="2303f-414">**NX_SUCCESS** (0x00) Server successfully suspended</span></span>
- <span data-ttu-id="2303f-415">**NX_DHCPV6_INVALID_SERVER_DUID** (0xe98) bilinmeyen veya desteklenmeyen DUID türü</span><span class="sxs-lookup"><span data-stu-id="2303f-415">**NX_DHCPV6_INVALID_SERVER_DUID** (0XE98) Unknown or unsupported DUID type</span></span>
- <span data-ttu-id="2303f-416">**NX_INVALID_PARAMETERS** (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-416">**NX_INVALID_PARAMETERS** (0x4D) Invalid non pointer input</span></span>
- <span data-ttu-id="2303f-417">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-417">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-418">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-418">**Allowed From**</span></span>

<span data-ttu-id="2303f-419">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-419">Application code</span></span>

<span data-ttu-id="2303f-420">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-420">**Example**</span></span>

```
/* Set the DHCPv6 ServerDUID as Link layer plus time, over Ethernet hardware. */
duid_time = SECONDS_SINCE_JAN_1_2000_MOD_32 + rand();

status = nx_dhcpv6_set_server_duid(&dhcp_server_0,1, 0x6,
         physical_address_msw,physical_address_lsw,duid_time);

/* If status is NX_SUCCESS the ServerDUID is successfully set. */
```

## <a name="nx_dhcpv6_server_option_request_handler_set"></a><span data-ttu-id="2303f-421">nx_dhcpv6_server_option_request_handler_set</span><span class="sxs-lookup"><span data-stu-id="2303f-421">nx_dhcpv6_server_option_request_handler_set</span></span>

### <a name="set-the-option-request-handler-for-dhcpv6-server-instance"></a><span data-ttu-id="2303f-422">DHCPv6 sunucu örneği için seçenek isteği işleyicisini ayarla</span><span class="sxs-lookup"><span data-stu-id="2303f-422">Set the option request handler for DHCPv6 Server instance</span></span> 

<span data-ttu-id="2303f-423">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="2303f-423">**Prototype**</span></span>

```
UINT nx_dhcpv6_server_option_request_handler_set(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     VOID (*dhcpv6_option_request_handler_extended)(
          struct NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
          UINT option_request, UCHAR *buffer_ptr, 
          UINT *index, UINT available_payload));
```

<span data-ttu-id="2303f-424">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2303f-424">**Description**</span></span>

<span data-ttu-id="2303f-425">Bu hizmet, DHCPv6 sunucusu genişletilmiş seçenek isteği işleyicisini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2303f-425">This service sets the DHCPv6 Server extended option request handler.</span></span>

<span data-ttu-id="2303f-426">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-426">**Input Parameters**</span></span>

- <span data-ttu-id="2303f-427">**dhcpv6_server_ptr** DHCPv6 sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-427">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="2303f-428">**dhcpv6_option_request_handler_extended** Genişletilmiş Seçenekler istek işleyicisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="2303f-428">**dhcpv6_option_request_handler_extended** Pointer to extended options request handler</span></span>

<span data-ttu-id="2303f-429">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="2303f-429">**Return Values**</span></span>

- <span data-ttu-id="2303f-430">**NX_SUCCESS** (0x00) sunucu başarıyla sürdürüldü</span><span class="sxs-lookup"><span data-stu-id="2303f-430">**NX_SUCCESS** (0x00) Server successfully resumed</span></span>
- <span data-ttu-id="2303f-431">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="2303f-431">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="2303f-432">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="2303f-432">**Allowed From**</span></span>

<span data-ttu-id="2303f-433">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="2303f-433">Application Code</span></span>

<span data-ttu-id="2303f-434">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="2303f-434">**Example**</span></span>

```
/* Set the option request handler for DHCPv6 Server. */
status = nx_dhcpv6_server_option_request_handler_set(&dhcp_server_0,
         dhcpv6_option_request_handler_extended);

/* If status is NX_SUCCESS the extended handler successfully set. */
```