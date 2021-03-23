---
title: Bölüm 3-Azure RTOS NetX DHCP sunucu hizmetlerinin açıklaması
description: Bu bölümde tüm Azure RTOS NetX DHCP sunucu hizmetlerinin açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d24c69cf6b8c2bb84b7155e49a54e8296ee662f0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826783"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-server-services"></a><span data-ttu-id="7bb3d-103">Bölüm 3-Azure RTOS NetX DHCP sunucu hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="7bb3d-103">Chapter 3 - Description of Azure RTOS NetX DHCP Server services</span></span>

<span data-ttu-id="7bb3d-104">Bu bölüm, tüm NetX DHCP sunucusu hizmetlerinin bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-104">This chapter contains a description of all NetX DHCP Server services.</span></span>

<span data-ttu-id="7bb3d-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="7bb3d-106">**nx_dhcp_server_create**: *DHCP sunucusu örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7bb3d-106">**nx_dhcp_server_create**: *Create a DHCP Server instance*</span></span>
- <span data-ttu-id="7bb3d-107">**nx_dhcp_set_interface_network_parameters**: *belirtilen arabirim için kritik ağ parametreleri için DHCP sunucusu seçeneklerini ayarla*</span><span class="sxs-lookup"><span data-stu-id="7bb3d-107">**nx_dhcp_set_interface_network_parameters**: *Set DHCP Server options for critical network parameters for specified interface*</span></span>
- <span data-ttu-id="7bb3d-108">**nx_dhcp_create_server_ip_address_list**: *DHCP istemcileri ARABIRIMINE atanacak kullanılabilir IP adresleri havuzu oluştur*</span><span class="sxs-lookup"><span data-stu-id="7bb3d-108">**nx_dhcp_create_server_ip_address_list**: *Create pool of available IP addresses to assign to DHCP Clients interface*</span></span>
- <span data-ttu-id="7bb3d-109">**nx_dhcp_clear_client_record**: *sunucu veritabanındaki istemci kaydını kaldırma*</span><span class="sxs-lookup"><span data-stu-id="7bb3d-109">**nx_dhcp_clear_client_record**: *Remove Client record in the Server database*</span></span>
- <span data-ttu-id="7bb3d-110">**nx_dhcp_server_delete**: *bir dhcpserver örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="7bb3d-110">**nx_dhcp_server_delete**: *Delete a DHCPServer instance*</span></span>
- <span data-ttu-id="7bb3d-111">**nx_dhcp_server_start**: *DHCP sunucusu işlemeyi Başlat veya sürüyor*</span><span class="sxs-lookup"><span data-stu-id="7bb3d-111">**nx_dhcp_server_start**: *Start or resume DHCP Server processing*</span></span>
- <span data-ttu-id="7bb3d-112">**nx_dhcp_server_stop**: *DHCP sunucusu işlemesini durdur*</span><span class="sxs-lookup"><span data-stu-id="7bb3d-112">**nx_dhcp_server_stop**: *Stop DHCP server processing*</span></span>

## <a name="nx_dhcp_server_create"></a><span data-ttu-id="7bb3d-113">nx_dhcp_server_create</span><span class="sxs-lookup"><span data-stu-id="7bb3d-113">nx_dhcp_server_create</span></span>

<span data-ttu-id="7bb3d-114">DHCP sunucu örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="7bb3d-114">Create a DHCP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="7bb3d-115">Prototype</span><span class="sxs-lookup"><span data-stu-id="7bb3d-115">Prototype</span></span>

```c
UINT nx_dhcp_server_create(NX_DHCP_SERVER *dhcp_ptr, NX_IP *ip_ptr,
                        VOID *stack_ptr, ULONG stack_size,
                        CHAR *input_address_list, CHAR *name_ptr,
                        NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a><span data-ttu-id="7bb3d-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-116">Description</span></span>

<span data-ttu-id="7bb3d-117">Bu hizmet, daha önce oluşturulmuş bir IP örneğiyle bir DHCP sunucusu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-117">This service creates a DHCP Server instance with a previously created IP instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7bb3d-118">Uygulama, IP oluşturma hizmeti için oluşturulan paket havuzunun UDP, IP ve Ethernet üst bilgilerini içermeyen bir minimum548 Byte yüküne sahip olduğundan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-118">The application must make sure the packet pool created for the IP create service has a minimum548 byte payload, not including the UDP, IP and Ethernet headers.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="7bb3d-119">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-119">Input Parameters</span></span>

- <span data-ttu-id="7bb3d-120">**dhcp_ptr**: DHCP sunucusu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-120">**dhcp_ptr**: Pointer to DHCP Server control block.</span></span>  
- <span data-ttu-id="7bb3d-121">**ip_ptr**: DHCP sunucusu IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-121">**ip_ptr**: Pointer to DHCP Server IP instance.</span></span>
- <span data-ttu-id="7bb3d-122">**stack_ptr**: Işaretçi DHCP sunucusu yığın konumu.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-122">**stack_ptr**: Pointer DHCP Server stack location.</span></span>
- <span data-ttu-id="7bb3d-123">**stack_size**: DHCP sunucusu yığınının boyutu</span><span class="sxs-lookup"><span data-stu-id="7bb3d-123">**stack_size**: Size of DHCP Server stack</span></span>
- <span data-ttu-id="7bb3d-124">**input_address_list**: sunucunun IP adresleri listesine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-124">**input_address_list**: Pointer to Server's list of IP addresses</span></span>
- <span data-ttu-id="7bb3d-125">**name_ptr**: DHCP sunucu adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-125">**name_ptr**: Pointer to DHCP Server name</span></span>
- <span data-ttu-id="7bb3d-126">**packet_pool_ptr**: DHCP sunucusu paket havuzuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-126">**packet_pool_ptr**: Pointer to DHCP Server packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="7bb3d-127">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-127">Return Values</span></span>

- <span data-ttu-id="7bb3d-128">**NX_SUCCESS**: (0x00) başarılı DHCP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-128">**NX_SUCCESS**: (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="7bb3d-129">**NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD**: (0xA9) paket yükü çok küçük hata</span><span class="sxs-lookup"><span data-stu-id="7bb3d-129">**NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD**: (0xA9) Packet payload too small error</span></span>
- <span data-ttu-id="7bb3d-130">**NX_DHCP_NO_SERVER_OPTION_LIST**: (0x96) sunucu seçenek listesi boş</span><span class="sxs-lookup"><span data-stu-id="7bb3d-130">**NX_DHCP_NO_SERVER_OPTION_LIST**: (0x96) Server option list is empty</span></span>
- <span data-ttu-id="7bb3d-131">NX_DHCP_PARAMETER_ERROR: (0x92) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-131">NX_DHCP_PARAMETER_ERROR: (0x92) Invalid non pointer input</span></span>
- <span data-ttu-id="7bb3d-132">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-132">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="7bb3d-133">NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-133">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7bb3d-134">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7bb3d-134">Allowed From</span></span>

<span data-ttu-id="7bb3d-135">Uygulama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-135">Application</span></span>

### <a name="example"></a><span data-ttu-id="7bb3d-136">Örnek</span><span class="sxs-lookup"><span data-stu-id="7bb3d-136">Example</span></span>

```c
/* Create a DHCP Server instance. */
status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
                    DEMO_SERVER_STACK_SIZE, SERVER_IP_ADDRESS_LIST,
                    "DHCP server", &server_pool);

/* If status is NX_SUCCESS a DHCP Server instance was successfully created. */
```

## <a name="nx_dhcp_create_server_ip_address_list"></a><span data-ttu-id="7bb3d-137">nx_dhcp_create_server_ip_address_list</span><span class="sxs-lookup"><span data-stu-id="7bb3d-137">nx_dhcp_create_server_ip_address_list</span></span>

<span data-ttu-id="7bb3d-138">IP adresi havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7bb3d-138">Create a IP address pool</span></span>

### <a name="prototype"></a><span data-ttu-id="7bb3d-139">Prototype</span><span class="sxs-lookup"><span data-stu-id="7bb3d-139">Prototype</span></span>

```c
UINT nx_dhcp_create_server_ip_address_list(NX_DHCP_SERVER *dhcp_ptr,
                            UINT iface_index, ULONG start_ip_address,
                            ULONG end_ip_address, UINT *addresses_added);
```

### <a name="description"></a><span data-ttu-id="7bb3d-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-140">Description</span></span>

<span data-ttu-id="7bb3d-141">Bu hizmet, belirtilen DHCP sunucusuna atanacak bir NetworkInterface 'e özgü IP adresleri havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-141">This service creates a networkinterface specific pool of available IP addresses for the specified DHCP server to assign.</span></span> <span data-ttu-id="7bb3d-142">Başlangıç ve bitiş IP adreslerinin belirtilen ağ arabirimiyle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-142">The start and end IP addresses must match the specified network interface.</span></span> <span data-ttu-id="7bb3d-143">IP adresi listesi yeterince büyük değilse (Kullanıcı tarafından yapılandırılabilir *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parametresinde ayarlanır), eklenen IP adreslerinin gerçek sayısı toplam adresten daha az olabilir.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-143">The actual number of IP addresses added may be less than the total addresses if the IP address list is not large enough (which is set in the user configurable *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parameter).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="7bb3d-144">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-144">Input Parameters</span></span>

- <span data-ttu-id="7bb3d-145">**dhcp_ptr** DHCP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-145">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>  
- <span data-ttu-id="7bb3d-146">**iface_index**: ağ arabirimine karşılık gelen dizin</span><span class="sxs-lookup"><span data-stu-id="7bb3d-146">**iface_index**: Index corresponding to network interface</span></span>
- <span data-ttu-id="7bb3d-147">**start_ip_address**: Ilk kullanılabilir IP adresi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-147">**start_ip_address**: First available IP address</span></span>
- <span data-ttu-id="7bb3d-148">**end_ip_address**: en son kullanılabilir IP adresi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-148">**end_ip_address**: Last of the available IP address</span></span>
- <span data-ttu-id="7bb3d-149">**addresses_added**: LISTEYE eklenen IP adresi sayısı</span><span class="sxs-lookup"><span data-stu-id="7bb3d-149">**addresses_added**: Number of IP addresses added to list</span></span>

### <a name="return-values"></a><span data-ttu-id="7bb3d-150">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-150">Return Values</span></span>

- <span data-ttu-id="7bb3d-151">**NX_SUCCESS**: (0x00) başarılı DHCP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-151">**NX_SUCCESS**: (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="7bb3d-152">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: (0xA1) dizin adreslerle eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="7bb3d-152">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: (0xA1) Index does not match addresses</span></span>
- <span data-ttu-id="7bb3d-153">**NX_DHCP_INVALID_IP_ADDRESS_LIST**: (0x99) geçersiz adres girişi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-153">**NX_DHCP_INVALID_IP_ADDRESS_LIST**: (0x99) Invalid address input</span></span>
- <span data-ttu-id="7bb3d-154">NX_DHCP_INVALID_IP_ADDRESS: (0x9B) ıllogical başlangıç/bitiş adresleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-154">NX_DHCP_INVALID_IP_ADDRESS: (0x9B) Illogical start/end addresses</span></span>
- <span data-ttu-id="7bb3d-155">NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-155">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7bb3d-156">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7bb3d-156">Allowed From</span></span>

<span data-ttu-id="7bb3d-157">Uygulama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-157">Application</span></span>

### <a name="example"></a><span data-ttu-id="7bb3d-158">Örnek</span><span class="sxs-lookup"><span data-stu-id="7bb3d-158">Example</span></span>

```c
/* Create a pool of available IP addresses to assign. */
status = nx_dhcp_create_server_ip_list (&dhcp_server, iface_index,
                START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);

/* If status is NX_SUCCESS aIP address list was successfully created. 
addresses_added indicates how many IP addresses were actually added to the list. */
```

## <a name="nx_dhcp_clear_client_record"></a><span data-ttu-id="7bb3d-159">nx_dhcp_clear_client_record</span><span class="sxs-lookup"><span data-stu-id="7bb3d-159">nx_dhcp_clear_client_record</span></span>

<span data-ttu-id="7bb3d-160">Istemci kaydını sunucu veritabanından kaldır</span><span class="sxs-lookup"><span data-stu-id="7bb3d-160">Remove Client record from Server database</span></span>

### <a name="prototype"></a><span data-ttu-id="7bb3d-161">Prototype</span><span class="sxs-lookup"><span data-stu-id="7bb3d-161">Prototype</span></span>

```c
UINT nx_dhcp_clear_client_record (NX_DHCP_SERVER *dhcp_ptr,
                                NX_DHCP_CLIENT *dhcp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="7bb3d-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-162">Description</span></span>

<span data-ttu-id="7bb3d-163">Bu hizmet, Istemci kaydını sunucu veritabanından temizler.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-163">This service clears the Client record from the Server database.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="7bb3d-164">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-164">Input Parameters</span></span>

- <span data-ttu-id="7bb3d-165">**dhcp_ptr**: DHCP sunucusu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-165">**dhcp_ptr**: Pointer to DHCP Server control block.</span></span>  
- <span data-ttu-id="7bb3d-166">**dhcp_client_ptr**: kaldırılacak DHCP istemcisine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-166">**dhcp_client_ptr**: Pointer to DHCP Client to remove</span></span>

### <a name="return-values"></a><span data-ttu-id="7bb3d-167">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-167">Return Values</span></span>

- <span data-ttu-id="7bb3d-168">**NX_SUCCESS**: (0x00) başarılı DHCP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-168">**NX_SUCCESS**: (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="7bb3d-169">NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-169">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="7bb3d-170">NX_CALLER_ERROR: (0x11) hizmet iş parçacığı olmayan çağrı</span><span class="sxs-lookup"><span data-stu-id="7bb3d-170">NX_CALLER_ERROR: (0x11) Non thread caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7bb3d-171">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7bb3d-171">Allowed From</span></span>

<span data-ttu-id="7bb3d-172">Uygulama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-172">Application</span></span>

### <a name="example"></a><span data-ttu-id="7bb3d-173">Örnek</span><span class="sxs-lookup"><span data-stu-id="7bb3d-173">Example</span></span>

```c
/* Remove Client record from the server database. */
status = nx_dhcp_clear_client_record (&dhcp_server, &dhcp_client_ptr);

/* If status is NX_SUCCESS the specified Client was removed from the database. */
```

## <a name="nx_dhcp_set_interface_network_parameters"></a><span data-ttu-id="7bb3d-174">nx_dhcp_set_interface_network_parameters</span><span class="sxs-lookup"><span data-stu-id="7bb3d-174">nx_dhcp_set_interface_network_parameters</span></span>

<span data-ttu-id="7bb3d-175">DHCP seçenekleri için ağ parametrelerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-175">Set network parameters for DHCP options</span></span>

### <a name="prototype"></a><span data-ttu-id="7bb3d-176">Prototype</span><span class="sxs-lookup"><span data-stu-id="7bb3d-176">Prototype</span></span>

```c
UINT nx_dhcp_set_interface_network_parameters(NX_DHCP_SERVER *dhcp_ptr,
                                    UINT iface_index, ULONG subnet_mask,
                                    ULONG default_gateway_address,
                                    ULONG dns_server_address);
```

### <a name="description"></a><span data-ttu-id="7bb3d-177">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-177">Description</span></span>

<span data-ttu-id="7bb3d-178">Bu hizmet, belirtilen arabirim için ağ kritik parametrelerinin varsayılan değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-178">This service sets default values for network critical parameters for the specified interface.</span></span> <span data-ttu-id="7bb3d-179">DHCP sunucusu, bu seçenekleri sunmak ve DHCP Istemcisine onay yanıtlarını içerecektir.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-179">The DHCP server will include these options in its OFFER and ACK replies to the DHCP Client.</span></span> <span data-ttu-id="7bb3d-180">Ana bilgisayar, bir DHCP sunucusunun çalıştığı arabirim parametreleri ayarlandıysa, parametreler varsayılan olarak aşağıdaki gibidir: yönlendirici, DHCP sunucusunun kendisi için birincil arabirim ağ geçidine, DHCP sunucusunun kendisi için de DNS sunucusu adresine ve DHCP sunucusu arabirimiyle aynı alt ağ maskesine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-180">If the host set interface parameters on which a DHCP server is running, the parameters will defaulted as follows: the router set to the primary interface gateway for the DHCP server itself, the DNS server address to the DHCP server itself, and the subnet mask to the same as the DHCP server interface is configured with.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="7bb3d-181">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-181">Input Parameters</span></span>

- <span data-ttu-id="7bb3d-182">**dhcp_ptr**: DHCP sunucusu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-182">**dhcp_ptr**: Pointer to DHCP Server control block.</span></span>  
- <span data-ttu-id="7bb3d-183">**iface_index**: ağ arabirimine karşılık gelen dizin</span><span class="sxs-lookup"><span data-stu-id="7bb3d-183">**iface_index**: Index corresponding to network interface</span></span>
- <span data-ttu-id="7bb3d-184">**subnet_mask**: istemci ağı için alt ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-184">**subnet_mask**: Subnet mask for Client network</span></span>
- <span data-ttu-id="7bb3d-185">**default_gateway_address**: ISTEMCININ yönlendirici IP adresi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-185">**default_gateway_address**: Client's router IP address</span></span>
- <span data-ttu-id="7bb3d-186">**dns_server_address**: istemci ağı için DNS sunucusu</span><span class="sxs-lookup"><span data-stu-id="7bb3d-186">**dns_server_address**: DNS server for Client's network</span></span>

### <a name="return-values"></a><span data-ttu-id="7bb3d-187">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-187">Return Values</span></span>

- <span data-ttu-id="7bb3d-188">**NX_SUCCESS**: (0x00) başarılı DHCP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-188">**NX_SUCCESS**: (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="7bb3d-189">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: (0xA1) dizin adreslerle eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="7bb3d-189">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: (0xA1) Index does not match addresses</span></span>
- <span data-ttu-id="7bb3d-190">**NX_DHCP_INVALID_NETWORK_PARAMETERS**: (0xA3) geçersiz ağ parametreleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-190">**NX_DHCP_INVALID_NETWORK_PARAMETERS**: (0xA3) Invalid network parameters</span></span>
- <span data-ttu-id="7bb3d-191">NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-191">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7bb3d-192">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7bb3d-192">Allowed From</span></span>

<span data-ttu-id="7bb3d-193">Uygulama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-193">Application</span></span>

### <a name="example"></a><span data-ttu-id="7bb3d-194">Örnek</span><span class="sxs-lookup"><span data-stu-id="7bb3d-194">Example</span></span>

```c
/* Set network parameters for a specific interface. */
status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
                                    NX_DHCP_SUBNET_MASK, IP_ADDRESS(10,0,0,1),
                                    IP_ADDRESS(10,0,0,1));

/* If status is NX_SUCCESS network parameters were successfully set. */
```

## <a name="nx_dhcp_server_delete"></a><span data-ttu-id="7bb3d-195">nx_dhcp_server_delete</span><span class="sxs-lookup"><span data-stu-id="7bb3d-195">nx_dhcp_server_delete</span></span>

<span data-ttu-id="7bb3d-196">DHCP sunucusu örneğini silme</span><span class="sxs-lookup"><span data-stu-id="7bb3d-196">Delete a DHCP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="7bb3d-197">Prototype</span><span class="sxs-lookup"><span data-stu-id="7bb3d-197">Prototype</span></span>

```c
UINT nx_dhcp_server_delete(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="7bb3d-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-198">Description</span></span>

<span data-ttu-id="7bb3d-199">Bu hizmet, önceden oluşturulmuş bir DHCP sunucusu örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-199">This service deletes a previously created DHCP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="7bb3d-200">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-200">Input Parameters</span></span>

- <span data-ttu-id="7bb3d-201">**dhcp_ptr**: bir DHCP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-201">**dhcp_ptr**: Pointer to a DHCP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="7bb3d-202">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-202">Return Values</span></span>

- <span data-ttu-id="7bb3d-203">**NX_SUCCESS**: (0x00) DHCP sunucusu başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-203">**NX_SUCCESS**: (0x00) Successful DHCP Server delete.</span></span>
- <span data-ttu-id="7bb3d-204">NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-204">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="7bb3d-205">NX_DHCP_PARAMETER_ERROR: (0x92) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-205">NX_DHCP_PARAMETER_ERROR: (0x92) Invalid non pointer input</span></span>
- <span data-ttu-id="7bb3d-206">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-206">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7bb3d-207">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7bb3d-207">Allowed From</span></span>

<span data-ttu-id="7bb3d-208">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7bb3d-208">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7bb3d-209">Örnek</span><span class="sxs-lookup"><span data-stu-id="7bb3d-209">Example</span></span>

```c
/* Delete a DHCP Server instance. */
status = nx_dhcp_server_delete(&dhcp_server);  
  
/* If status is NX_SUCCESS the DHCP Server instance was successfully deleted. */
```

## <a name="nx_dhcp_server_start"></a><span data-ttu-id="7bb3d-210">nx_dhcp_server_start</span><span class="sxs-lookup"><span data-stu-id="7bb3d-210">nx_dhcp_server_start</span></span>

<span data-ttu-id="7bb3d-211">DHCP sunucusu işlemeyi Başlat</span><span class="sxs-lookup"><span data-stu-id="7bb3d-211">Start DHCP Server processing</span></span>

### <a name="prototype"></a><span data-ttu-id="7bb3d-212">Prototype</span><span class="sxs-lookup"><span data-stu-id="7bb3d-212">Prototype</span></span>

```c
UINT nx_dhcp_server_start(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="7bb3d-213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-213">Description</span></span>

<span data-ttu-id="7bb3d-214">Bu hizmet, bir sunucu UDP yuvası oluşturmayı, DHCP bağlantı noktasını bağlamayı ve Istemci DHCP isteklerini almayı beklemeyi içeren DHCP sunucusu işlemesini başlatır.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-214">This service starts DHCP Server processing, which includes creating a server UDP socket, binding the DHCP port and waiting to receive Client DHCP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="7bb3d-215">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-215">Input Parameters</span></span>

- <span data-ttu-id="7bb3d-216">**dhcp_ptr**: daha önce oluşturulmuş DHCP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-216">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="7bb3d-217">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-217">Return Values</span></span>

- <span data-ttu-id="7bb3d-218">**NX_SUCCESS**: (0x00) sunucu başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-218">**NX_SUCCESS**: (0x00) Successful Server start.</span></span>  
- <span data-ttu-id="7bb3d-219">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-219">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP already started.</span></span>
- <span data-ttu-id="7bb3d-220">NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-220">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="7bb3d-221">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-221">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="7bb3d-222">NX_DHCP_PARAMETER_ERROR: (0x92) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="7bb3d-222">NX_DHCP_PARAMETER_ERROR: (0x92) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7bb3d-223">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7bb3d-223">Allowed From</span></span>

<span data-ttu-id="7bb3d-224">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7bb3d-224">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7bb3d-225">Örnek</span><span class="sxs-lookup"><span data-stu-id="7bb3d-225">Example</span></span>

```c
/* Start the DHCP Server processing for this IP instance. */
status = nx_dhcp_server_start(&dhcp_server);  

/* If status is NX_SUCCESS the DHCP Server was successfully started. */
```

### <a name="see-also"></a><span data-ttu-id="7bb3d-226">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-226">See Also</span></span>

<span data-ttu-id="7bb3d-227">nx_dhcp_create, nx_dhcp_delete, nx_dhcp_release, nx_dhcp_state_change_notify, nx_dhcp_stop, nx_dhcp_user_option_retrieve, nx_dhcp_user_option_convert</span><span class="sxs-lookup"><span data-stu-id="7bb3d-227">nx_dhcp_create, nx_dhcp_delete, nx_dhcp_release, nx_dhcp_state_change_notify, nx_dhcp_stop, nx_dhcp_user_option_retrieve, nx_dhcp_user_option_convert</span></span>

## <a name="nx_dhcp_server_stop"></a><span data-ttu-id="7bb3d-228">nx_dhcp_server_stop</span><span class="sxs-lookup"><span data-stu-id="7bb3d-228">nx_dhcp_server_stop</span></span>

<span data-ttu-id="7bb3d-229">DHCP sunucusu işlemesini durduruyor</span><span class="sxs-lookup"><span data-stu-id="7bb3d-229">Stops DHCP Server processing</span></span>

### <a name="prototype"></a><span data-ttu-id="7bb3d-230">Prototype</span><span class="sxs-lookup"><span data-stu-id="7bb3d-230">Prototype</span></span>

```c
UINT nx_dhcp_server_stop(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="7bb3d-231">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7bb3d-231">Description</span></span>

<span data-ttu-id="7bb3d-232">Bu hizmet, DHCP Istemci isteklerinin alınması dahil olmak üzere DHCP sunucusu işlemesini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-232">This service stops DHCP Server processing, which includes of receiving DHCP Client requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="7bb3d-233">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-233">Input Parameters</span></span>

- <span data-ttu-id="7bb3d-234">**dhcp_ptr**: DHCP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-234">**dhcp_ptr**: Pointer to DHCP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="7bb3d-235">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="7bb3d-235">Return Values</span></span>

- <span data-ttu-id="7bb3d-236">**NX_SUCCESS**: (0x00) başarılı DHCP durağı.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-236">**NX_SUCCESS**: (0x00) Successful DHCP stop.</span></span>
- <span data-ttu-id="7bb3d-237">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-237">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP already started.</span></span>
- <span data-ttu-id="7bb3d-238">NX_PTR_ERROR: (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-238">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="7bb3d-239">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-239">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="7bb3d-240">NX_DHCP_PARAMETER_ERROR: (0x92) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="7bb3d-240">NX_DHCP_PARAMETER_ERROR: (0x92) Invalid non pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="7bb3d-241">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="7bb3d-241">Allowed From</span></span>

<span data-ttu-id="7bb3d-242">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="7bb3d-242">Threads</span></span>

### <a name="example"></a><span data-ttu-id="7bb3d-243">Örnek</span><span class="sxs-lookup"><span data-stu-id="7bb3d-243">Example</span></span>

```c
/* Stop the DHCP Server processing for this IP instance. */
status = nx_dhcp_server_stop(&dhcp_server);  

/* If status is NX_SUCCESS the DHCP Server was successfully stopped. */
```
