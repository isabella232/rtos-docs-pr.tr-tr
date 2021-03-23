---
title: Bölüm 3-Azure RTOS NetX Duo DHCP Server hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo DHCP sunucu hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 33eb0b4bd98f808124b9a6a1f01950639243d612
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826105"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dhcp-server-services"></a><span data-ttu-id="c67c2-103">Bölüm 3-Azure RTOS NetX Duo DHCP Server hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="c67c2-103">Chapter 3 - Description of Azure RTOS NetX Duo DHCP Server Services</span></span>

<span data-ttu-id="c67c2-104">Bu bölüm, tüm NetX Duo DHCP sunucu hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="c67c2-104">This chapter contains a description of all NetX Duo DHCP Server services (listed below) in alphabetic order.</span></span>

> [!NOTE]
> <span data-ttu-id="c67c2-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="c67c2-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_dhcp_server-create"></a><span data-ttu-id="c67c2-106">nx_dhcp_server oluştur</span><span class="sxs-lookup"><span data-stu-id="c67c2-106">nx_dhcp_server create</span></span>

<span data-ttu-id="c67c2-107">DHCP sunucu örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c67c2-107">Create a DHCP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c67c2-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="c67c2-108">Prototype</span></span>

```C
UINT nx_dhcp_server_create(NX_DHCP_SERVER *dhcp_ptr, NX_IP *ip_ptr,
    VOID *stack_ptr, ULONG stack_size,
    CHAR *input_address_list, CHAR *name_ptr, NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a><span data-ttu-id="c67c2-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c67c2-109">Description</span></span>

<span data-ttu-id="c67c2-110">Bu hizmet, daha önce oluşturulmuş bir IP örneğiyle bir DHCP sunucusu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c67c2-110">This service creates a DHCP Server instance with a previously created IP instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c67c2-111">Uygulama, IP oluşturma hizmeti için oluşturulan paket havuzunda UDP, IP ve Ethernet üst bilgilerini içermeyen en düşük 548 bayt yüküne sahip olduğundan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c67c2-111">The application must make sure the packet pool created for the IP create service has a minimum 548 byte payload, not including the UDP, IP and Ethernet headers.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c67c2-112">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-112">Input Parameters</span></span>

- <span data-ttu-id="c67c2-113">**dhcp_ptr** DHCP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-113">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>
- <span data-ttu-id="c67c2-114">**ip_ptr** DHCP sunucusu IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-114">**ip_ptr** Pointer to DHCP Server IP instance.</span></span>
- <span data-ttu-id="c67c2-115">**stack_ptr** İşaretçi DHCP sunucusu yığın konumu.</span><span class="sxs-lookup"><span data-stu-id="c67c2-115">**stack_ptr** Pointer DHCP Server stack location.</span></span>
- <span data-ttu-id="c67c2-116">Sunucunun IP adresleri listesine input_address_list **DHCP sunucusu yığınının Stack_size boyutu**</span><span class="sxs-lookup"><span data-stu-id="c67c2-116">**stack_size Size of DHCP Server stack** input_address_list Pointer to Server’s list of IP addresses</span></span>
- <span data-ttu-id="c67c2-117">DHCP sunucu adı packet_pool_ptr Işaretçiden DHCP sunucusu paket havuzuna **Name_ptr işaretçi**</span><span class="sxs-lookup"><span data-stu-id="c67c2-117">**name_ptr Pointer to DHCP Server name** packet_pool_ptr Pointer to DHCP Server packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="c67c2-118">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-118">Return Values</span></span>

- <span data-ttu-id="c67c2-119">**NX_SUCCESS** (0x00) başarılı DHCP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c67c2-119">**NX_SUCCESS** (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="c67c2-120">**NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD** (0xA9) paket yükü çok küçük hata</span><span class="sxs-lookup"><span data-stu-id="c67c2-120">**NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD** (0xA9) Packet payload too small error</span></span>
- <span data-ttu-id="c67c2-121">**NX_DHCP_NO_SERVER_OPTION_LIST** (0x96) sunucu seçenek listesi boş</span><span class="sxs-lookup"><span data-stu-id="c67c2-121">**NX_DHCP_NO_SERVER_OPTION_LIST** (0x96) Server option list is empty</span></span>
- <span data-ttu-id="c67c2-122">NX_DHCP_PARAMETER_ERROR (0x92) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c67c2-122">NX_DHCP_PARAMETER_ERROR (0x92) Invalid non pointer input</span></span>
- <span data-ttu-id="c67c2-123">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="c67c2-123">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="c67c2-124">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-124">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c67c2-125">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c67c2-125">Allowed From</span></span>

<span data-ttu-id="c67c2-126">Uygulama</span><span class="sxs-lookup"><span data-stu-id="c67c2-126">Application</span></span>

### <a name="example"></a><span data-ttu-id="c67c2-127">Örnek</span><span class="sxs-lookup"><span data-stu-id="c67c2-127">Example</span></span>

```C
/* Create a DHCP Server instance. */

status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
    DEMO_SERVER_STACK_SIZE, SERVER_IP_ADDRESS_LIST, "DHCP server", &server_pool);

/* If status is NX_SUCCESS a DHCP Server instance was successfully created. */
```

## <a name="nx_dhcp_create_server_ip_address_list"></a><span data-ttu-id="c67c2-128">nx_dhcp_create_server_ip_address_list</span><span class="sxs-lookup"><span data-stu-id="c67c2-128">nx_dhcp_create_server_ip_address_list</span></span>

<span data-ttu-id="c67c2-129">IP adresi havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c67c2-129">Create a IP address pool</span></span>

### <a name="prototype"></a><span data-ttu-id="c67c2-130">Prototype</span><span class="sxs-lookup"><span data-stu-id="c67c2-130">Prototype</span></span>

```C
UINT nx_dhcp_create_server_ip_address_list(NX_DHCP_SERVER *dhcp_ptr,
    UINT iface_index, ULONG start_ip_address,
    ULONG end_ip_address, UINT *addresses_added);
```

### <a name="description"></a><span data-ttu-id="c67c2-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c67c2-131">Description</span></span>

<span data-ttu-id="c67c2-132">Bu hizmet, belirtilen DHCP sunucusu için atanacak bir ağ arabirimine özel IP adresleri havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c67c2-132">This service creates a network interface specific pool of available IP addresses for the specified DHCP server to assign.</span></span> <span data-ttu-id="c67c2-133">Başlangıç ve bitiş IP adreslerinin belirtilen ağ arabirimiyle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c67c2-133">The start and end IP addresses must match the specified network interface.</span></span> <span data-ttu-id="c67c2-134">IP adresi listesi yeterince büyük değilse (Kullanıcı tarafından yapılandırılabilir *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parametresinde ayarlanır), eklenen IP adreslerinin gerçek sayısı toplam adresten daha az olabilir.</span><span class="sxs-lookup"><span data-stu-id="c67c2-134">The actual number of IP addresses added may be less than the total addresses if the IP address list is not large enough (which is set in the user configurable *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parameter).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c67c2-135">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-135">Input Parameters</span></span>

- <span data-ttu-id="c67c2-136">**dhcp_ptr** DHCP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-136">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>
- <span data-ttu-id="c67c2-137">**iface_index** Ağ arabirimine karşılık gelen dizin</span><span class="sxs-lookup"><span data-stu-id="c67c2-137">**iface_index** Index corresponding to network interface</span></span>
- <span data-ttu-id="c67c2-138">**start_ip_address** İlk kullanılabilir IP adresi</span><span class="sxs-lookup"><span data-stu-id="c67c2-138">**start_ip_address** First available IP address</span></span>
- <span data-ttu-id="c67c2-139">**end_ip_address** Kullanılabilir IP adresinin son sayısı</span><span class="sxs-lookup"><span data-stu-id="c67c2-139">**end_ip_address** Last of the available IP address</span></span>
- <span data-ttu-id="c67c2-140">**addresses_added** Listeye eklenen IP adresi sayısı</span><span class="sxs-lookup"><span data-stu-id="c67c2-140">**addresses_added** Number of IP addresses added to list</span></span>

### <a name="return-values"></a><span data-ttu-id="c67c2-141">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-141">Return Values</span></span>

- <span data-ttu-id="c67c2-142">**NX_SUCCESS** (0x00) başarılı DHCP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c67c2-142">**NX_SUCCESS** (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="c67c2-143">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) dizin adreslerle eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="c67c2-143">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) Index does not match addresses</span></span>
- <span data-ttu-id="c67c2-144">**NX_DHCP_INVALID_IP_ADDRESS_LIST** (0x99) geçersiz adres girişi</span><span class="sxs-lookup"><span data-stu-id="c67c2-144">**NX_DHCP_INVALID_IP_ADDRESS_LIST** (0x99) Invalid address input</span></span>
- <span data-ttu-id="c67c2-145">NX_DHCP_INVALID_IP_ADDRESS (0x9B) ıllogical başlangıç/bitiş adresleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-145">NX_DHCP_INVALID_IP_ADDRESS (0x9B) Illogical start/end addresses</span></span>
- <span data-ttu-id="c67c2-146">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-146">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c67c2-147">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c67c2-147">Allowed From</span></span>

<span data-ttu-id="c67c2-148">Uygulama</span><span class="sxs-lookup"><span data-stu-id="c67c2-148">Application</span></span>

### <a name="example"></a><span data-ttu-id="c67c2-149">Örnek</span><span class="sxs-lookup"><span data-stu-id="c67c2-149">Example</span></span>

```C
/* Create a pool of available IP addresses to assign. */

status = nx_dhcp_create_server_ip_list(&dhcp_server, iface_index,
    START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);

/* If status is NX_SUCCESS a IP address list was successfully created.
    addresses_added indicates how many IP addresses were actually added to the
    list. */
```

## <a name="nx_dhcp_clear_client_record"></a><span data-ttu-id="c67c2-150">nx_dhcp_clear_client_record</span><span class="sxs-lookup"><span data-stu-id="c67c2-150">nx_dhcp_clear_client_record</span></span>

<span data-ttu-id="c67c2-151">Istemci kaydını sunucu veritabanından kaldır</span><span class="sxs-lookup"><span data-stu-id="c67c2-151">Remove Client record from Server database</span></span>

### <a name="prototype"></a><span data-ttu-id="c67c2-152">Prototype</span><span class="sxs-lookup"><span data-stu-id="c67c2-152">Prototype</span></span>

```C
UINT nx_dhcp_clear_client_record(NX_DHCP_SERVER *dhcp_ptr,
    NX_DHCP_CLIENT *dhcp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="c67c2-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c67c2-153">Description</span></span>

<span data-ttu-id="c67c2-154">Bu hizmet, Istemci kaydını sunucu veritabanından temizler.</span><span class="sxs-lookup"><span data-stu-id="c67c2-154">This service clears the Client record from the Server database.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c67c2-155">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-155">Input Parameters</span></span>

- <span data-ttu-id="c67c2-156">**dhcp_ptr** DHCP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-156">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>
- <span data-ttu-id="c67c2-157">**kaldırılacak DHCP Istemcisine dhcp_client_ptr Işaretçisi**</span><span class="sxs-lookup"><span data-stu-id="c67c2-157">**dhcp_client_ptr Pointer to DHCP Client to remove**</span></span>

### <a name="return-values"></a><span data-ttu-id="c67c2-158">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-158">Return Values</span></span>

- <span data-ttu-id="c67c2-159">**NX_SUCCESS** (0x00) başarılı DHCP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c67c2-159">**NX_SUCCESS** (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="c67c2-160">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-160">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="c67c2-161">NX_CALLER_ERROR (0x11) hizmet iş parçacığı olmayan çağrı</span><span class="sxs-lookup"><span data-stu-id="c67c2-161">NX_CALLER_ERROR (0x11) Non thread caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c67c2-162">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c67c2-162">Allowed From</span></span>

<span data-ttu-id="c67c2-163">Uygulama</span><span class="sxs-lookup"><span data-stu-id="c67c2-163">Application</span></span>

### <a name="example"></a><span data-ttu-id="c67c2-164">Örnek</span><span class="sxs-lookup"><span data-stu-id="c67c2-164">Example</span></span>

```C
/* Remove Client record from the server database. */
status = nx_dhcp_clear_client_record(&dhcp_server, &dhcp_client_ptr);

/* If status is NX_SUCCESS the specified Client was removed from the database. */
```

## <a name="nx_dhcp_set_interface_network_parameters"></a><span data-ttu-id="c67c2-165">nx_dhcp_set_interface_network_parameters</span><span class="sxs-lookup"><span data-stu-id="c67c2-165">nx_dhcp_set_interface_network_parameters</span></span>

<span data-ttu-id="c67c2-166">DHCP seçenekleri için ağ parametrelerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="c67c2-166">Set network parameters for DHCP options</span></span>

### <a name="prototype"></a><span data-ttu-id="c67c2-167">Prototype</span><span class="sxs-lookup"><span data-stu-id="c67c2-167">Prototype</span></span>

```C
UINT nx_dhcp_set_interface_network_parameters(NX_DHCP_SERVER *dhcp_ptr,
    UINT iface_index, ULONG subnet_mask,
    ULONG default_gateway_address,
    ULONG dns_server_address);
```

### <a name="description"></a><span data-ttu-id="c67c2-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c67c2-168">Description</span></span>

<span data-ttu-id="c67c2-169">Bu hizmet, belirtilen arabirim için ağ kritik parametrelerinin varsayılan değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c67c2-169">This service sets default values for network critical parameters for the specified interface.</span></span> <span data-ttu-id="c67c2-170">DHCP sunucusu, bu seçenekleri sunmak ve DHCP Istemcisine onay yanıtlarını içerecektir.</span><span class="sxs-lookup"><span data-stu-id="c67c2-170">The DHCP server will include these options in its OFFER and ACK replies to the DHCP Client.</span></span> <span data-ttu-id="c67c2-171">Ana bilgisayar, bir DHCP sunucusunun çalıştığı arabirim parametreleri ayarlandıysa, parametreler varsayılan olarak aşağıdaki gibidir: yönlendirici, DHCP sunucusunun kendisi için birincil arabirim ağ geçidine, DHCP sunucusunun kendisi için de DNS sunucusu adresine ve DHCP sunucusu arabirimiyle aynı alt ağ maskesine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c67c2-171">If the host set interface parameters on which a DHCP server is running, the parameters will defaulted as follows: the router set to the primary interface gateway for the DHCP server itself, the DNS server address to the DHCP server itself, and the subnet mask to the same as the DHCP server interface is configured with.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c67c2-172">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-172">Input Parameters</span></span>

- <span data-ttu-id="c67c2-173">**dhcp_ptr** DHCP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-173">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>
- <span data-ttu-id="c67c2-174">**iface_index** Ağ arabirimine karşılık gelen dizin</span><span class="sxs-lookup"><span data-stu-id="c67c2-174">**iface_index** Index corresponding to network interface</span></span>
- <span data-ttu-id="c67c2-175">**subnet_mask** Istemci ağı için alt ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="c67c2-175">**subnet_mask** Subnet mask for Client network</span></span>
- <span data-ttu-id="c67c2-176">**default_gateway_address** İstemcinin yönlendirici IP adresi</span><span class="sxs-lookup"><span data-stu-id="c67c2-176">**default_gateway_address** Client’s router IP address</span></span>
- <span data-ttu-id="c67c2-177">**dns_server_address** Istemci ağı için DNS sunucusu</span><span class="sxs-lookup"><span data-stu-id="c67c2-177">**dns_server_address** DNS server for Client’s network</span></span>

### <a name="return-values"></a><span data-ttu-id="c67c2-178">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-178">Return Values</span></span>

- <span data-ttu-id="c67c2-179">**NX_SUCCESS** (0x00) başarılı DHCP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c67c2-179">**NX_SUCCESS** (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="c67c2-180">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) dizin adreslerle eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="c67c2-180">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) Index does not match addresses</span></span>
- <span data-ttu-id="c67c2-181">**NX_DHCP_INVALID_NETWORK_PARAMETERS** (0xA3) geçersiz ağ parametreleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-181">**NX_DHCP_INVALID_NETWORK_PARAMETERS** (0xA3) Invalid network parameters</span></span>
- <span data-ttu-id="c67c2-182">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-182">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c67c2-183">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c67c2-183">Allowed From</span></span>

<span data-ttu-id="c67c2-184">Uygulama</span><span class="sxs-lookup"><span data-stu-id="c67c2-184">Application</span></span>

### <a name="example"></a><span data-ttu-id="c67c2-185">Örnek</span><span class="sxs-lookup"><span data-stu-id="c67c2-185">Example</span></span>

```C
/* Set network parameters for a specific interface. */

status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
    NX_DHCP_SUBNET_MASK, NX_DHCP_DEFAULT_GATEWAY,
    NX_DHCP_DNS_SERVER);

/* If status is NX_SUCCESS network parameters were successfully set. */
```

## <a name="nx_dhcp_server_delete"></a><span data-ttu-id="c67c2-186">nx_dhcp_server_delete</span><span class="sxs-lookup"><span data-stu-id="c67c2-186">nx_dhcp_server_delete</span></span>

<span data-ttu-id="c67c2-187">DHCP sunucusu örneğini silme</span><span class="sxs-lookup"><span data-stu-id="c67c2-187">Delete a DHCP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c67c2-188">Prototype</span><span class="sxs-lookup"><span data-stu-id="c67c2-188">Prototype</span></span>

```C
UINT nx_dhcp_server_delete(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="c67c2-189">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c67c2-189">Description</span></span>

<span data-ttu-id="c67c2-190">Bu hizmet, önceden oluşturulmuş bir DHCP sunucusu örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="c67c2-190">This service deletes a previously created DHCP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c67c2-191">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-191">Input Parameters</span></span>

- <span data-ttu-id="c67c2-192">**dhcp_ptr** Bir DHCP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-192">**dhcp_ptr** Pointer to a DHCP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c67c2-193">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-193">Return Values</span></span>

- <span data-ttu-id="c67c2-194">**NX_SUCCESS** (0x00) başarılı DHCP sunucusu silme.</span><span class="sxs-lookup"><span data-stu-id="c67c2-194">**NX_SUCCESS** (0x00) Successful DHCP Server delete.</span></span>
- <span data-ttu-id="c67c2-195">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-195">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="c67c2-196">NX_DHCP_PARAMETER_ERROR (0x92) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c67c2-196">NX_DHCP_PARAMETER_ERROR (0x92) Invalid non pointer input</span></span>
- <span data-ttu-id="c67c2-197">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="c67c2-197">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c67c2-198">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c67c2-198">Allowed From</span></span>

<span data-ttu-id="c67c2-199">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c67c2-199">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c67c2-200">Örnek</span><span class="sxs-lookup"><span data-stu-id="c67c2-200">Example</span></span>

```C
/* Delete a DHCP Server instance. */

status = nx_dhcp_server_delete(&dhcp_server);

/* If status is NX_SUCCESS the DHCP Server instance was successfully deleted. */
```

## <a name="nx_dhcp_server_start"></a><span data-ttu-id="c67c2-201">nx_dhcp_server_start</span><span class="sxs-lookup"><span data-stu-id="c67c2-201">nx_dhcp_server_start</span></span>

<span data-ttu-id="c67c2-202">DHCP sunucusu işlemeyi Başlat</span><span class="sxs-lookup"><span data-stu-id="c67c2-202">Start DHCP Server processing</span></span>

### <a name="prototype"></a><span data-ttu-id="c67c2-203">Prototype</span><span class="sxs-lookup"><span data-stu-id="c67c2-203">Prototype</span></span>

```C
UINT nx_dhcp_server_start(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="c67c2-204">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c67c2-204">Description</span></span>

<span data-ttu-id="c67c2-205">Bu hizmet, bir sunucu UDP yuvası oluşturmayı, DHCP bağlantı noktasını bağlamayı ve Istemci DHCP isteklerini almayı beklemeyi içeren DHCP sunucusu işlemesini başlatır.</span><span class="sxs-lookup"><span data-stu-id="c67c2-205">This service starts DHCP Server processing, which includes creating a server UDP socket, binding the DHCP port and waiting to receive Client DHCP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c67c2-206">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-206">Input Parameters</span></span>

- <span data-ttu-id="c67c2-207">**dhcp_ptr** Daha önce oluşturulan DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-207">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c67c2-208">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-208">Return Values</span></span>

- <span data-ttu-id="c67c2-209">**NX_SUCCESS** (0x00) sunucu başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="c67c2-209">**NX_SUCCESS** (0x00) Successful Server start.</span></span>
- <span data-ttu-id="c67c2-210">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="c67c2-210">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP already started.</span></span>
- <span data-ttu-id="c67c2-211">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-211">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="c67c2-212">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="c67c2-212">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="c67c2-213">NX_DHCP_PARAMETER_ERROR (0x92) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c67c2-213">NX_DHCP_PARAMETER_ERROR (0x92) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c67c2-214">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c67c2-214">Allowed From</span></span>

<span data-ttu-id="c67c2-215">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c67c2-215">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c67c2-216">Örnek</span><span class="sxs-lookup"><span data-stu-id="c67c2-216">Example</span></span>

```C
/* Start the DHCP Server processing for this IP instance. */

status = nx_dhcp_server_start(&dhcp_server);

/* If status is NX_SUCCESS the DHCP Server was successfully started. */
```

## <a name="nx_dhcp_server_stop"></a><span data-ttu-id="c67c2-217">nx_dhcp_server_stop</span><span class="sxs-lookup"><span data-stu-id="c67c2-217">nx_dhcp_server_stop</span></span>

<span data-ttu-id="c67c2-218">DHCP sunucusu işlemesini durduruyor</span><span class="sxs-lookup"><span data-stu-id="c67c2-218">Stops DHCP Server processing</span></span>

### <a name="prototype"></a><span data-ttu-id="c67c2-219">Prototype</span><span class="sxs-lookup"><span data-stu-id="c67c2-219">Prototype</span></span>

```C
UINT nx_dhcp_server_stop(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="c67c2-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c67c2-220">Description</span></span>

<span data-ttu-id="c67c2-221">Bu hizmet, DHCP Istemci isteklerinin alınması dahil olmak üzere DHCP sunucusu işlemesini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="c67c2-221">This service stops DHCP Server processing, which includes of receiving DHCP Client requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c67c2-222">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-222">Input Parameters</span></span>

- <span data-ttu-id="c67c2-223">**dhcp_ptr** DHCP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-223">**dhcp_ptr** Pointer to DHCP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c67c2-224">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c67c2-224">Return Values</span></span>

- <span data-ttu-id="c67c2-225">**NX_SUCCESS** (0x00) başarılı DHCP durağı.</span><span class="sxs-lookup"><span data-stu-id="c67c2-225">**NX_SUCCESS** (0x00) Successful DHCP stop.</span></span>
- <span data-ttu-id="c67c2-226">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="c67c2-226">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP already started.</span></span>
- <span data-ttu-id="c67c2-227">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="c67c2-227">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="c67c2-228">NX_CALLER_ERROR (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="c67c2-228">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="c67c2-229">NX_DHCP_PARAMETER_ERROR (0x92) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c67c2-229">NX_DHCP_PARAMETER_ERROR (0x92) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c67c2-230">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c67c2-230">Allowed From</span></span>

<span data-ttu-id="c67c2-231">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c67c2-231">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c67c2-232">Örnek</span><span class="sxs-lookup"><span data-stu-id="c67c2-232">Example</span></span>

```C
/* Stop the DHCP Server processing for this IP instance. */

status = nx_dhcp_server_stop(&dhcp_server);

/* If status is NX_SUCCESS the DHCP Server was successfully stopped. */
```
