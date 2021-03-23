---
title: Bölüm 2-Azure RTOS NetX Duo DHCPv6 Istemcisini yükleme ve kullanma
description: Bu bölümde, Azure RTOS NetX Duo DHCPv6 Istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a154dbeb91b46a2c8bd5f4585e168a6b62d042ff
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826093"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-dhcpv6-client"></a><span data-ttu-id="1ce47-103">Bölüm 2-Azure RTOS NetX Duo DHCPv6 Istemcisini yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="1ce47-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo DHCPv6 Client</span></span>

<span data-ttu-id="1ce47-104">Bu bölümde, Azure RTOS NetX Duo DHCPv6 Istemci bileşeni yükleme, kurulum ve kullanımı ile ilgili çeşitli sorunların bir açıklaması yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo DHCPv6 Client component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="1ce47-105">Ürün dağıtımı</span><span class="sxs-lookup"><span data-stu-id="1ce47-105">Product Distribution</span></span>

<span data-ttu-id="1ce47-106">NetX Duo DHCPv6 Istemcisi adresinde bulunabilir [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="1ce47-106">NetX Duo DHCPv6 Client is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="1ce47-107">Paket, aşağıdaki gibi, bu belgeyi içeren iki kaynak dosya ve bir PDF dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="1ce47-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="1ce47-108">**nxd_dhcpv6_client. h** NetX DuoDHCPv6 Istemcisi için üst bilgi dosyası</span><span class="sxs-lookup"><span data-stu-id="1ce47-108">**nxd_dhcpv6_client.h** Header file for NetX DuoDHCPv6 Client</span></span>

- <span data-ttu-id="1ce47-109">**nxd_dhcpv6_client. c** NetX Duo DHCPv6 Istemcisi için kaynak kodu dosyası</span><span class="sxs-lookup"><span data-stu-id="1ce47-109">**nxd_dhcpv6_client.c** Source code file for NetX Duo DHCPv6 Client</span></span>

- <span data-ttu-id="1ce47-110">**demo_netxduo_dhcpv6_client. c** NetX Duo DHCPv6 Istemcisinin kurulumunu gösteren örnek program</span><span class="sxs-lookup"><span data-stu-id="1ce47-110">**demo_netxduo_dhcpv6_client.c** Sample program demonstrating the setup of the NetX Duo DHCPv6 Client</span></span>

- <span data-ttu-id="1ce47-111">**nxd_dhcpv6_client.pdf** NetX Duo DHCPv6 Istemcisinin PDF açıklaması</span><span class="sxs-lookup"><span data-stu-id="1ce47-111">**nxd_dhcpv6_client.pdf** PDF description of NetX Duo DHCPv6 Client</span></span>

## <a name="netx-duo-dhcpv6-client-installation"></a><span data-ttu-id="1ce47-112">NetX Duo DHCPv6 Istemci yüklemesi</span><span class="sxs-lookup"><span data-stu-id="1ce47-112">NetX Duo DHCPv6 Client Installation</span></span>

<span data-ttu-id="1ce47-113">NetX Duo DHCPv6 Istemci API 'sini kullanmak için, yukarıda belirtilen tüm dağıtım, NetX Duo 'un yüklü olduğu dizine kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-113">To use NetX Duo DHCPv6 Client API, the entire distribution mentioned above can be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="1ce47-114">Örneğin, "*\threadx\arm7\green*" dizininde NETX Duo yüklüyse, *nxd_dhcpv6_client. h* ve *nxd_dhpcv6_client. c* dosyaları bu dizine kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-114">For example, if NetX Duo is installed in the directory “*\threadx\arm7\green*” then the *nxd_dhcpv6_client.h* and *nxd_dhpcv6_client.c* files can be copied into this directory.</span></span>

## <a name="using-the-netx-duo-dhcpv6-client"></a><span data-ttu-id="1ce47-115">NetX Duo DHCPv6 Istemcisini kullanma</span><span class="sxs-lookup"><span data-stu-id="1ce47-115">Using the NetX Duo DHCPv6 Client</span></span>

<span data-ttu-id="1ce47-116">Uygulama kodu, sırasıyla *nxd_dhcpv6_client.* h ve bir *nx_api.* h içermelidir, *tx_api* Bu da DHCPv6 Istemcisi, threadx ve NETX Duo hizmetlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-116">The application code must include *nxd_dhcpv6_client.h* after it includes *tx_api.h* and *nx_api.h*, to use DHCPv6 Client, ThreadX and NetX Duo services, respectively.</span></span> <span data-ttu-id="1ce47-117">*nxd_dhcpv6_client. c* , diğer uygulama dosyalarıyla aynı şekilde projede derlenmesi gerekir ve nesne formu, uygulamanın dosyalarıyla birlikte bağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-117">*nxd_dhcpv6_client.c* must be compiled in the project in the same manner as other application files and its object form must be linked along with the files of the application.</span></span>

### <a name="span-classunderlineclient-dhcp-unique-identifier-duidspan"></a><span data-ttu-id="1ce47-118"><span class="underline">İstemci DHCP benzersiz tanımlayıcısı (DUıD)</span></span><span class="sxs-lookup"><span data-stu-id="1ce47-118"><span class="underline">Client DHCP Unique Identifier (DUID)</span></span></span>

<span data-ttu-id="1ce47-119">Istemci DUıD her Istemciyi bir ağ üzerinde benzersiz şekilde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1ce47-119">The Client DUID uniquely defines each Client on a network.</span></span> <span data-ttu-id="1ce47-120">Bir uygulamanın bir sunucudan IPv6 adresi istenmeden önce Istemci DUıD oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-120">An application must create a Client DUID prior to requesting an IPv6 address from a Server.</span></span> <span data-ttu-id="1ce47-121">Istemci DUıD 'si sunucuya tüm iletilere otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-121">The Client DUID is automatically included in all messages to the Server.</span></span> <span data-ttu-id="1ce47-122">Bir DUıD oluşturmak için, uygulama hizmeti *nx_dhcpv6_create_client_duid çağırır:*</span><span class="sxs-lookup"><span data-stu-id="1ce47-122">To create a DUID, the application calls the service *nx_dhcpv6_create_client_duid:*</span></span>
```C
UINT nx_dhcpv6_create_client_duid(NX_DHCPV6 *dhcpv6_ptr, 
                                  UINT duid_type, 
                                  UINT hardware_type, ULONG time);
```

<span data-ttu-id="1ce47-123">Uygulama bu hizmeti çağırır ve DUıD türünü belirtir (yalnızca bağlantı katmanı veya bağlantı katmanı ve saati).</span><span class="sxs-lookup"><span data-stu-id="1ce47-123">The application calls this service and specifies the type of DUID (link layer only, or link layer plus time.</span></span> <span data-ttu-id="1ce47-124">Bağlantı katmanı ve zaman Duıds için, bu hizmet zaman girişi belirtilmemişse saat alanı sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-124">For link layer plus time DUIDs, this service will provide the time field if the time input is not specified.</span></span>

<span data-ttu-id="1ce47-125">Önceden atanmış bir IPv6 adresi kiralamasını yeniden başlatma ve kullanma desteği olan cihazlar için, uygulamanın, IPv6 adresi atandığında kullananın Istemci DUıD 'sini oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-125">For devices rebooting and wishing to use a previously assigned IPv6 address lease, the application must create the Client DUID as the one it used when assigned the IPv6 address.</span></span> <span data-ttu-id="1ce47-126">Bağlantı katmanı adresinin hepsi bir bağlantı katmanı Istemci DUıD 'si oluşturmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-126">The link layer address is all that is needed to create a link layer Client DUID.</span></span> <span data-ttu-id="1ce47-127">Cihazın bağlantı katmanı adresine erişimi varsa, bu önceki geçici bellek depolama alanı gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1ce47-127">This does not require previous non volatile memory storage if the device has access to the link layer address.</span></span> <span data-ttu-id="1ce47-128">Zaman türündeki Duıds 'ler için, uygulamanın önceki DUıD oluşturmada kullanılan aynı saat verilerine erişimi olmalıdır ve bu, geçici olmayan bellek gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-128">For DUIDs of type time, the application must have access to the same time data used in the previous DUID creation and this does require non volatile memory.</span></span> <span data-ttu-id="1ce47-129">Kararlı depolama alanı olmayan istemciler, zaman türünde Duıds içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-129">Clients that do not have any stable storage must not use DUIDs of type time.</span></span>

### <a name="span-classunderlineclient-identity-association-for-non-temporary-addresses-ianaspan"></a><span data-ttu-id="1ce47-130"><span class="underline">Geçici olmayan adresler için istemci kimliği Ilişkilendirmesi (ıANA)</span></span><span class="sxs-lookup"><span data-stu-id="1ce47-130"><span class="underline">Client Identity Association for Non Temporary Addresses (IANA)</span></span></span>

<span data-ttu-id="1ce47-131">Uygulamanın bir IPv6 adresi istenmeden önce bir ıANA ve isteğe bağlı olarak bir veya daha fazla IA adresi oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-131">The application must create an IANA and optionally one or more IA addresses before requesting an IPv6 address.</span></span> <span data-ttu-id="1ce47-132">Bunu yapmak için uygulama *nx_dhcpv6_create_client_iana* hizmetini çağırır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-132">To do so, the application calls the *nx_dhcpv6_create_client_iana* service.</span></span> <span data-ttu-id="1ce47-133">Bir IA Adres seçeneği oluşturmak için uygulama, istenen bir IPv6 adresi ve yaşam süresi değerleriyle *nx_dhcpv6_add_client_ia* hizmetini sunucuya bir ipucu olarak çağırır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-133">To create an IA address option, the application calls the *nx_dhcpv6_add_client_ia* service with a requested IPv6 address and lifetime values as a hint to the Server.</span></span>

<span data-ttu-id="1ce47-134">IANA ve IAS, Istemci IPv6 adresi atama parametrelerini üst üste tanımlar:</span><span class="sxs-lookup"><span data-stu-id="1ce47-134">The IANA and its IAs cumulatively define the Client IPv6 address assignment parameters:</span></span>

<span data-ttu-id="1ce47-135">DHCPv6 istemcisini başlatmadan önce, DHCPv6 Istemci uygulaması *nx_dhcpv6_create_client_iana* hizmetini kullanarak bir IANA oluşturur:</span><span class="sxs-lookup"><span data-stu-id="1ce47-135">Before starting the DHCPv6 Client, the DHCPv6 Client application creates an IANA using the *nx_dhcpv6_create_client_iana* service:</span></span>

```C
UINT    nx_dhcpv6_create_client_iana(NX_DHCPV6 *dhcpv6_ptr, 
                                     UINT IA_ident, ULONG T1, ULONG T2);
```

<span data-ttu-id="1ce47-136">Ayrıca, DHCPv6 Istemcisini başlatmadan önce *nx_dhcpv6_create_client_ia* hizmetini ve istenen IPv6 adreslerini kullanarak bir veya daha fazla IAS oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-136">It must also create one or more IAs using the *nx_dhcpv6_create_client_ia* service and requested IPv6 addresses before starting the DHCPv6 Client.</span></span>

```C
UINT    nx_dhcpv6_add_client_ia(NX_DHCPV6 *dhcpv6_ptr, 
                                NXD_ADDRESS *ipv6_address, 
                                ULONG preferred_lifetime, 
                                ULONG valid_lifetime);
```

> [!NOTE]
> <span data-ttu-id="1ce47-137">Uygulama tarafından oluşturulan IA adresi sayısı, varsayılan değeri 1 olan NX_DHCPV6_MAX_IA_ADDRESS parametresini aşamaz.</span><span class="sxs-lookup"><span data-stu-id="1ce47-137">The number of IA addresses the application creates cannot exceed the NX_DHCPV6_MAX_IA_ADDRESS parameter whose default value is 1.</span></span>

<span data-ttu-id="1ce47-138">NetX Duo DHCPv6 Istemcisi, eski DHCPv6 Istemci uygulamaları için *nx_dhcpv6_create_client_ia* destekler ve *nx_dhcpv6_add_client_ia* , ancak geliştiricilerin *nx_dhcpv6_add_client_ia* hizmetini kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-138">The NetX Duo DHCPv6 Client supports *nx_dhcpv6_create_client_ia* for legacy DHCPv6 Client applications and which is identical to *nx_dhcpv6_add_client_ia* but developers are encouraged to use the *nx_dhcpv6_add_client_ia* service.</span></span>

<span data-ttu-id="1ce47-139">Bu hizmetler, bu bölümün başka bir yerinde "küçük örnek sistem" bölümünde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-139">These services are demonstrated in the “Small Example System” elsewhere in this chapter.</span></span>

### <a name="span-classunderlinenon-volatile-memory-considerations-to-reuse-ianas-and-iasspan"></a><span data-ttu-id="1ce47-140"><span class="underline">Ianas ve IAS 'Yi yeniden kullanmak Için geçici olmayan bellek konuları</span></span><span class="sxs-lookup"><span data-stu-id="1ce47-140"><span class="underline">Non Volatile Memory Considerations To Reuse IANAs and IAs</span></span></span>

<span data-ttu-id="1ce47-141">Uygulamanın yeniden başlatma sırasında aynı adresleri kullanmasını istiyorsa, uygulamanın ıANA parametrelerini T1, T2 ve ıANA tanımlayıcısını geçici olmayan belleğe kaydetmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-141">The application must save IANA parameters T1, T2, and the IANA identifier to non volatile memory if it wishes to use the same address(es) on rebooting.</span></span> <span data-ttu-id="1ce47-142">Uygulamanın, IPv6 adresini geçici olmayan belleğe dahil eden IA de kaydetmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-142">The application must also save its IA which includes its IPv6 address to non volatile memory.</span></span>

<span data-ttu-id="1ce47-143">Ayrıca uygulama, kapanması durumunda geçici olmayan belleğe atanmış IPv6 adresi kiralamasına bağlanan süreyi de depolamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-143">The application must also store the time elapsed that it has been bound to its assigned IPv6 address lease(s) to non volatile memory if shutting down.</span></span> <span data-ttu-id="1ce47-144">Bunu, DHCPv6 Istemcisini durdurmadan önce *nx_dhcpv6_get_time_accrued* hizmetini çağırarak yapar.</span><span class="sxs-lookup"><span data-stu-id="1ce47-144">It does this by calling the *nx_dhcpv6_get_time_accrued* service before it stops the DHCPv6 Client.</span></span>

```C
UINT nx_dhcpv6_get_time_accrued(NX_DHCPV6 *dhcpv6_ptr, 
                                ULONG *time_accrued);
```

<span data-ttu-id="1ce47-145">Uygulamanın, bir yeniden başlatmadan sonra DHCPv6 Istemcisini durdurduğu ve yeniden başlatmasının zaman aralığını izlemek için bağımsız bir saatinin olduğu varsayıldığında, bu geçen süreye, durdurulmadan önce IPv6 kiralamasında tahakkuk eden zamana ekler.</span><span class="sxs-lookup"><span data-stu-id="1ce47-145">Assuming the application has an independent clock to track the time interval from when it stopped and restarted the DHCPv6 Client after a reboot, it adds to that elapsed time to the time accrued on the IPv6 lease before stopping.</span></span> <span data-ttu-id="1ce47-146">Artık, aşağıdaki nv_time giriş olarak IPv6 kirasına göre geçen toplam süre ile Istemci iş parçacığı görevini başlatır:</span><span class="sxs-lookup"><span data-stu-id="1ce47-146">It now starts the Client thread task with the total elapsed time bound to the IPv6 lease as the nv_time input below:</span></span>

```C
UINT nx_dhcpv6_start(NX_DHCPV6 *dhcpv6_ptr, ULONG nv_time);
```

<span data-ttu-id="1ce47-147">Bu noktadan sonra, DHCPv6 Istemci iş parçacığı görevi, kiralamanın ne zaman yenileneceğini, IPv6 kirası üzerinde tahakkuk eden süreyi izlemeyi alır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-147">From this point, the DHCPv6 Client thread task will take over monitoring the time accrued on the IPv6 lease for when to renew the lease.</span></span>

### <a name="span-classunderlinesetting-dhcpv6-option-dataspan"></a><span data-ttu-id="1ce47-148"><span class="underline">DHCPv6 seçenek verilerini ayarlama</span></span><span class="sxs-lookup"><span data-stu-id="1ce47-148"><span class="underline">Setting DHCPv6 Option Data</span></span></span>

<span data-ttu-id="1ce47-149">Bir IPv6 kirası istenmeden önce, uygulama DNS sunucusu ve saat sunucusu gibi diğer ağ parametresi verileri isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-149">Before requesting an IPv6 lease, the application can request other network parameter data such as DNS server and time server.</span></span> <span data-ttu-id="1ce47-150">Bu parametrelerden bazılarının belirli hizmetleri vardır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-150">Some of these parameters have specific services.</span></span> <span data-ttu-id="1ce47-151">Aşağıda aşağıda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1ce47-151">A few are shown below:</span></span>

```C
UINT  nx_dhcpv6_request_option_DNS_server(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT enable)

UINT  nx_dhcpv6_request_option_time_server(NX_DHCPV6 *dhcpv6_ptr, 
                                           UINT enable);
```

### <a name="span-classunderlineinitiating-the-ipv6-address-requestspan"></a><span data-ttu-id="1ce47-152"><span class="underline">IPv6 adresi Isteği başlatılıyor</span></span><span class="sxs-lookup"><span data-stu-id="1ce47-152"><span class="underline">Initiating the IPv6 address Request</span></span></span>

<span data-ttu-id="1ce47-153">Uygulama, *nx_dhcpv6_start* hizmetini sıfır zaman girişi Ile çağırarak DHCPv6 istemci iş parçacığını başlatır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-153">The application starts the DHCPv6 Client thread by calling the *nx_dhcpv6_start* service with a zero time input.</span></span> <span data-ttu-id="1ce47-154">Bir IPv6 adresi istemek üzere DHCPv6 protokolünü başlatmak için, uygulama *nx_dhcpv6_request_solicit çağırır.*</span><span class="sxs-lookup"><span data-stu-id="1ce47-154">To initiate the DHCPv6 protocol to request an IPv6 address, the application calls *nx_dhcpv6_request_solicit.*</span></span>

<span data-ttu-id="1ce47-155">Uygulama daha önce atanmış bir IPv6 kirası kullanmayı istiyorsa, sıfır olmayan bir zaman girişi ile *nx_dhcpv6_start* çağırır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-155">If the application wishes to use a previously assigned IPv6 lease assigned, it calls *nx_dhcpv6_start* with a non zero time input.</span></span> <span data-ttu-id="1ce47-156">*Nx_dhcpv6_request_solicit* çağırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-156">It should not call *nx_dhcpv6_request_solicit*.</span></span>

<span data-ttu-id="1ce47-157">Bundan sonra uygulama için başka bir şey yapmanız gerekmez ve bir IPv6 adresini yenileme veya yeniden bağlama sırasında DHCPv6 Istemcisi otomatik olarak izlenir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-157">Thereafter the application need do nothing more and the DHCPv6 Client will automatically monitor when it is time to renew or rebind an IPv6 address.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="1ce47-158">Küçük örnek sistem</span><span class="sxs-lookup"><span data-stu-id="1ce47-158">Small Example System</span></span>

<span data-ttu-id="1ce47-159">NetX Duo DHCPv6 Istemcisini kullanmanın ne kadar kolay olduğunu bir örnek, DHCPv6 Istemcisi ve sanal "RAM" sürücüsü kullanarak aşağıdaki küçük örnekte açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-159">An example of how easy it is to use the NetX Duo DHCPv6 Client is described in the small example below using a DHCPv6 Client and a virtual “RAM” driver.</span></span> <span data-ttu-id="1ce47-160">Bu demo, bir cihazı yalnızca tek bir fiziksel ağ arabirimine sahip olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="1ce47-160">This demo assumes a device with only a single physical network interface.</span></span>

<span data-ttu-id="1ce47-161">*tx_application_define* , DHCPv6 istemcisinin DHCPv6 iletilerini gönderebilmesi için paket havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ce47-161">*tx_application_define* creates packet pool for the DHCPv6 Client to send DHCPv6 messages.</span></span> <span data-ttu-id="1ce47-162">Ayrıca bir uygulama iş parçacığı ve IP örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ce47-162">It also creates an application thread and IP instance.</span></span> <span data-ttu-id="1ce47-163">Daha sonra 130-148 satırlarında IP 'de UDP ve ıCMP 'yi sunar.</span><span class="sxs-lookup"><span data-stu-id="1ce47-163">It then enables UDP and ICMP on IP in lines 130-148.</span></span> <span data-ttu-id="1ce47-164">Ardından, line151 içinde durum değişikliği (*dhcpv6_state_change_notify* ) ve sunucu hatası (*dhcpv6_server_error_handler*) geri çağırma işlevleriyle DHCPv6 istemcisi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1ce47-164">Then the DHCPv6 Client is created with state change (*dhcpv6_state_change_notify* ) and server error (*dhcpv6_server_error_handler*) callback functions in line151.</span></span>

<span data-ttu-id="1ce47-165">Istemci iş parçacığı girişi işlevinde *thread_client_entry*, istemci IP 'si bir bağlantı yerel adresi ile ayarlanır ve 202-217 numaralı satırlarda IPv6 ve ICMPv6 Hizmetleri için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-165">In the Client thread entry function, *thread_client_entry*, the Client IP is set up with a link local address and enabled for IPv6 and ICMPv6 services on lines 202-217.</span></span> <span data-ttu-id="1ce47-166">Uygulama, DHCPv6 Istemcisini başlatmadan önce lines219-303 üzerinde bir Istemci DUıD, bir ıANA seçeneği ve bir IA Address seçeneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ce47-166">Before starting the DHCPv6 Client, the application creates a Client DUID, an IANA option and an IA address option on lines219-303.</span></span> <span data-ttu-id="1ce47-167">Istemci, sunucudan bir IPv6 adresi ve geçerli ve tercih edilen yaşam süreleri istemek isterse, IA adresi seçeneği isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-167">The IA address option is optional if the Client wishes to request an IPv6 address and valid and preferred lifetimes from the Server.</span></span> <span data-ttu-id="1ce47-168">Sunucu istenen IPv6 adresini veya kira sürelerini verebilir veya vermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-168">The Server may or may not grant the requested IPv6 address or lease times.</span></span> <span data-ttu-id="1ce47-169">Uygulama birden fazla genel adres atamak için daha fazla IA seçeneği (NX_DHCPV6_MAX_IA_ADDRESS kadar) ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-169">The application may add more IA options (up to NX_DHCPV6_MAX_IA_ADDRESS) to be assigned multiple global addresses.</span></span>

<span data-ttu-id="1ce47-170">Son olarak, uygulama, iletilerinde DHCPv6 sunucusuna ağ parametreleri istemek için çeşitli seçenekler ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1ce47-170">Lastly, the application sets various options to request network parameters in its messages to the DHCPv6 Server.</span></span> <span data-ttu-id="1ce47-171">DHCPv6 Istemci görevi, line306 ' deki *nx_dhcpv6_start* çağırarak başlatılır ve gerçek DHCPv6 protokolü, 317. satırdaki *NX_DHCPV6_REQUEST_SOLICIT* çağrısıyla birlikte istem durumunda başlatılır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-171">The DHCPv6 Client task is started by calling *nx_dhcpv6_start* in line306, and the actual DHCPv6 protocol is started in the SOLICIT state with the call to *nx_dhcpv6_request_solicit* in line 317.</span></span> <span data-ttu-id="1ce47-172">DHCPv6 Istemcisi daha sonra, bir adrese bağlanana kadar veya bir hata oluştuğunda, Istemci durumunun, DHCPv6 protokolü aracılığıyla otomatik olarak yükseltilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ce47-172">The DHCPv6 Client then automatically handles the promotion of the Client state through the DHCPv6 protocol until it is bound to an address or an error occurs.</span></span> <span data-ttu-id="1ce47-173">Bu süre boyunca, uygulamanın protokolün tamamlanmasını bekler ve IP örneği BABACıĞıM (varsayılan yapılandırma) için yapılandırılmışsa yinelenen adres algılama (BABACıĞıM) işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-173">During this time, the application waits for the protocol to complete, as well as the Duplicate Address Detection (DAD) to complete if the IP instance is configured for DAD (which is the default configuration).</span></span>

<span data-ttu-id="1ce47-174">Tx_thread_sleep çağrısından sonra, uygulama bir IPv6 kirası atamak için her iki DHCPv6 Istemci görevinin başarısını ve bu durumda benzersizlik denetimi başarılı olup olmadığını denetlemek için durum değişikliği geri aramasında ayarlanan genel parametreleri denetler.</span><span class="sxs-lookup"><span data-stu-id="1ce47-174">After the tx_thread_sleep call, the application checks on the global parameters set in the state change callback to determine the success of both the DHCPv6 Client task to get assigned an IPv6 lease and if so, that the DAD check for uniqueness succeeded.</span></span> <span data-ttu-id="1ce47-175">Bu, durum değişikliği ve sunucu hatası geri arama işlevlerinde ayarlanan sayaçlar kullanılarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-175">This is done using the counters set up in the state change and server error callback functions.</span></span> <span data-ttu-id="1ce47-176">Uygulama, başarısız adres ataması için sıfır olmayan address_not_assigned, address_expired ve server_errors için yoklar.</span><span class="sxs-lookup"><span data-stu-id="1ce47-176">The application polls for non zero counts of address_not_assigned, address_expired and server_errors for failed address assignment.</span></span> <span data-ttu-id="1ce47-177">Bound_addresses sayısı sıfır değilse (en az bir adres başarıyla atandı), başarısız bir baba denetimi için sıfır olmayan bir address_failed_dad denetler.</span><span class="sxs-lookup"><span data-stu-id="1ce47-177">If the count of bound_addresses is non zero (at least one address successfully assigned), it checks for a non zero address_failed_dad for a failed DAD check.</span></span> <span data-ttu-id="1ce47-178">Durum değişikliği ve sunucu hatası geri çağırmaları hakkında bir açıklama aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1ce47-178">An explanation of the state change and server error callbacks follows:</span></span>

<span data-ttu-id="1ce47-179">Durum değişikliği geri araması, *dhcpv6_state_change_notify*, önceki ve geçerli DHCPv6 istemci durumu, Istemcinin geçerli sunucu yanıtları aldığından belirlenir:</span><span class="sxs-lookup"><span data-stu-id="1ce47-179">The state change callback, *dhcpv6_state_change_notify*, the previous and current DHCPv6 Client state to determine if the Client received any valid Server responses:</span></span>

  - <span data-ttu-id="1ce47-180">*dhcpv6_state_change_notify* , GEÇIŞLERI doğrudan Init 'e ve sunucudan yanıt alma DHCPv6 istemcisi için bir sayacı arttırır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-180">*dhcpv6_state_change_notify* checks for transitions directly from SOLICIT to INIT and if so it increments a counter for the DHCPv6 Client receiving no responses from the Server.</span></span>

<span data-ttu-id="1ce47-181">Sonraki *dhcpv6_state_change_notify* , istemcinin bir veya daha fazla IPv6 adresine atanıp atanmadığını (bağlanmadığını) denetler:</span><span class="sxs-lookup"><span data-stu-id="1ce47-181">Next *dhcpv6_state_change_notify* checks if the Client was assigned (bound) to one or more IPv6 addresses:</span></span>

  - <span data-ttu-id="1ce47-182">Yeni durum BAĞLıYSA, Istemciye dayalı bir adres sayacını artırır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-182">If the new state is BOUND, it increments a counter of addresses bound to the Client.</span></span>
    
<span data-ttu-id="1ce47-183">*Dhcpv6_state_change_notify* , başarısız bir babacığım denetimi de denetler:</span><span class="sxs-lookup"><span data-stu-id="1ce47-183">The *dhcpv6_state_change_notify* also checks for a failed DAD check:</span></span>

  - <span data-ttu-id="1ce47-184">Durum geçişi 'den ıNIT 'e geçiş yapmak için, DHCPv6 Istemcisi atanan adreslerinden birini denetleyemedi ve başarısız adres atamalarının sayısını artırır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-184">If the state transitions from DECLINE to INIT, the DHCPv6 Client has failed DAD check on one of its assigned addresses and increments the count of failed address assignments.</span></span>
    
<span data-ttu-id="1ce47-185">Bu örnekteki *dhcpv6_state_change_notify* tarafından yapılan son denetim, sorunsuz bir şekilde atanmış bir adres olup olmadığını denetlemek veya yeniden bağlamak için babacığım:</span><span class="sxs-lookup"><span data-stu-id="1ce47-185">The last check by *dhcpv6_state_change_notify* in this example is for a successfully assigned address that passed the DAD check to fail to be renewed or rebind:</span></span>

  - <span data-ttu-id="1ce47-186">Durum yeniden bağlama 'den ıNIT 'e değişirse, Istemci yenıleme veya yeniden bağlama istekleri için herhangi bir yanıt almadı ve *dhcpv6_state_change_notify* , zaman aşımına uğradı adres sayısını artırır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-186">If the state changes from REBIND to INIT, the Client did not get any responses to either its RENEW or REBIND requests and *dhcpv6_state_change_notify* increments its count of expired addresses.</span></span>

<span data-ttu-id="1ce47-187">Sunucudan alınan bir hata durumunun DHCPv6 Istemci görevi tarafından bildirilmişse, sunucu hatalarının sayısını artırır *dhcpv6_server_error_handler* .</span><span class="sxs-lookup"><span data-stu-id="1ce47-187">The *dhcpv6_server_error_handler* if notified by the DHCPv6 Client task of an error status received from the Server increments the count of server errors.</span></span>

<span data-ttu-id="1ce47-188">Her şey iyi kabul edilse de, uygulama, kira süreleri dahil olmak üzere adres verileri için DHCPv6 Istemcisini sorgular.</span><span class="sxs-lookup"><span data-stu-id="1ce47-188">Assuming all goes well, the application queries the DHCPv6 Client for address data including lease times.</span></span> <span data-ttu-id="1ce47-189">372-392 satırlarına *nx_dhcpv6_get_iana_lease_time* çağırarak IANA 'da (atanan tüm IA adresleri için geçerlidir) *nx_dhcpv6_get_valid_ip_address_count* hizmetini çağırarak geçerli (başarıyla atanan) adreslerin sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-189">It gets a count of valid (successfully assigned) addresses by calling the *nx_dhcpv6_get_valid_ip_address_count* service and time to renew in the IANA (applies to all IA addresses assigned) by calling *nx_dhcpv6_get_iana_lease_time* on lines 372-392.</span></span> <span data-ttu-id="1ce47-190">Daha sonra, IPv6 adresi ve kira süreleri için her bir IA seçeneğinin her biri için DHCPv6 Istemcisini adres dizinine göre sorgular.</span><span class="sxs-lookup"><span data-stu-id="1ce47-190">It then queries the DHCPv6 Client for each of its IA options for IPv6 address and lease times by address index.</span></span>

<span data-ttu-id="1ce47-191">Bazı DHCPv6 Istemci Hizmetleri (*nx_dhcpv6_get_lease_time_data, nx_dhcpv6_get_IP_address*), giriş olarak bir adres dizini gerektirmez ve birincil istemci genel adresi için DHCPv6 parametrelerini döndürmez.</span><span class="sxs-lookup"><span data-stu-id="1ce47-191">Some DHCPv6 Client services (*nx_dhcpv6_get_lease_time_data, nx_dhcpv6_get_IP_address*) do not require an address index as an input, and return DHCPv6 parameters for the primary Client global address.</span></span> <span data-ttu-id="1ce47-192">Bu, satır 384 ' de *nx_dhcpv6_get_valid_ip_address_lease_time* çağırdığında tek bir genel IPv6 adresine sahip istemciler için uygundur.</span><span class="sxs-lookup"><span data-stu-id="1ce47-192">This is suitable for Clients with a single global IPv6 address when it calls *nx_dhcpv6_get_valid_ip_address_lease_time* in line 384.</span></span>

<span data-ttu-id="1ce47-193">NX_DHCPV6_CLIENT_RESTORE_STATE, t DHCPv6 Istemci yapılandırması, sistemin önceden oluşturulmuş bir DHCPv6 Istemcisini sistem yeniden başlatmalar arasında bağlantılı durumda geri yüklemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-193">The DHCPv6 Client configuration, NX_DHCPV6_CLIENT_RESTORE_STATE, t allows a system to restore a previously created DHCPv6 Client in Bound state between system reboots.</span></span> <span data-ttu-id="1ce47-194">434 satırı üzerinde sistem yeniden başlatmalar arasında DHCPv6 Istemci kaydını almak için *nx_dhcpv6_client_get_record* çağırarak, 525. satırdaki sistem gücünden sonra DHCPv6 istemci kaydını depolamak için *nx_dhcpv6_client_restore_record* çağırır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-194">Calling the *nx_dhcpv6_client_get_record* to get the DHCPv6 Client record between system reboots on line 434, calling the *nx_dhcpv6_client_restore_record* to store the DHCPv6 Client record after system power up on line 525.</span></span>

<span data-ttu-id="1ce47-195">Daha sonra uygulama, 552 satırındaki *nx_dhcpv6_request_release* hizmetini kullanarak atanan adresleri serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-195">The application then releases the assigned addresses using the *nx_dhcpv6_request_release* service in line 552.</span></span> <span data-ttu-id="1ce47-196">Uygulamayı yeniden başlatmak için, 567. satırdaki DHCPv6 Istemcisini *nx_dhcpv6_client_stop* hizmeti ile sonlandırır ve DHCPv6 istemcisi tarafından yapılandırılan IP örneğiyle kaydedilen tüm IPv6 adreslerini temizler.</span><span class="sxs-lookup"><span data-stu-id="1ce47-196">To restart the application stops the DHCPv6 Client with the *nx_dhcpv6_client_stop* service in line 567 and clears all IPv6 addresses registered with the IP instance that were configured throughthe DHCPv6 Client.</span></span> <span data-ttu-id="1ce47-197">Bunu, satır 578 ' de *nx_dhcpv6_reinitialize* çağırarak yapar.</span><span class="sxs-lookup"><span data-stu-id="1ce47-197">It does this by calling *nx_dhcpv6_reinitialize* in line 578.</span></span> <span data-ttu-id="1ce47-198">Ardından, daha önce olduğu gibi *nx_dhcpv6_start* ve *Nx_dhcpv6_request_solicit* hizmetleriyle DHCPv6 istemci görevini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="1ce47-198">Then it restarts the DHCPv6 Client task with *nx_dhcpv6_start* and *nx_dhcpv6_request_solicit* services as before.</span></span>

<span data-ttu-id="1ce47-199">DHCPv6 Istemcisi, line626 içinde *nx_dhcpv6_delete* çağrısıyla silinir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-199">The DHCPv6 Client is deleted with the call to *nx_dhcpv6_delete* in line626.</span></span> <span data-ttu-id="1ce47-200">Bu paket havuzu IP örneği tarafından da kullanıldığından, DHCPv6 Istemcisi için oluşturduğu *bir paket havuzunu* silmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ce47-200">Note that it does not delete th *e* packet pool it created for the DHCPv6 Client because this packet pool is also used by the IP instance.</span></span> <span data-ttu-id="1ce47-201">Aksi halde, NetX Duo *nx_packet_pool_delete* hizmeti kullanılarak bu hizmet için başka bir kullanım yoksa, paket havuzunu silmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ce47-201">Otherwise it should delete the packet pool if it has no further use for it using the NetX Duo *nx_packet_pool_delete* service.</span></span>

```C
/* This is a small demo of the NetX Duo DHCPv6 Client for the high-performance NetX Duo stack. */

#include    <stdio.h>
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nxd_dhcpv6_client.h"

#ifdef FEATURE_NX_IPV6
#define     DEMO_STACK_SIZE         2048

/* Set the client address, and request these address from DHCPv6 Server. */
/*
#define     NX_DHCPV6_REQUEST_IA_ADDRESS
*/

/* Set the list of DHCPv6 option data (timezone, DNS server, timer server, domain name)to get from the DHCPv6 server. */

#define     NX_DHCPV6_REQUEST_OPTION


/* Add the fully qualified domain name to request whether the DHCPv6 server SHOULD or SHOULD NOT perform the AAAA RR or DNS updates. */

#define     NX_DHCPV6_REQUEST_FQDN_OPTION


/* Define the ThreadX and NetX object control blocks... */

NX_PACKET_POOL          pool_0;
TX_THREAD               thread_client;
NX_IP                   client_ip;

/* Define the Client and Server instances. */

NX_DHCPV6               dhcp_client;

/* Define the error counter used in the demo application... */
ULONG                   error_counter;
CHAR                    *pointer;

/* Define thread prototypes. */
void    thread_client_entry(ULONG thread_input);

/***** Substitute your ethernet driver entry function here *********/
extern VOID    _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

/* Declare DHCPv6 Client callbacks */
VOID dhcpv6_state_change_notify(NX_DHCPV6 *dhcpv6_ptr, UINT old_state, UINT new_state);
VOID dhcpv6_server_error_handler(NX_DHCPV6 *dhcpv6_ptr, UINT op_code, UINT status_code, UINT message_type);

/* Set up globals for tracking changes to DHCPv6 Client from callback services. */
UINT state_changes = 0;
UINT address_expired = 0;
UINT address_failed_dad = 0;
UINT bound_addresses = 0;
UINT address_not_assigned = 0;
UINT server_errors = 0;

/* Define some DHCPv6 parameters. */

#define DHCPV6_IANA_ID      0xC0DEDBAD
#define DHCPV6_T1           NX_DHCPV6_INFINITE_LEASE
#define DHCPV6_T2           NX_DHCPV6_INFINITE_LEASE
#define DHCPV6_RENEW_TIME   NX_DHCPV6_INFINITE_LEASE
#define DHCPV6_REBIND_TIME  NX_DHCPV6_INFINITE_LEASE
#define PACKET_PAYLOAD      500
#define PACKET_POOL_SIZE    (5*PACKET_PAYLOAD)

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}


/* Define what the initial system looks like. */

void    tx_application_define(void *first_unused_memory)
{

UINT    status;

    /* Setup the working pointer. */
    pointer =  (CHAR *) first_unused_memory;

    /* Create the Client thread. */
    status = tx_thread_create(&thread_client, "Client thread", thread_client_entry, 0,
                              pointer, DEMO_STACK_SIZE, 8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Check for IP create errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status =  nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 1024,  pointer, PACKET_POOL_SIZE);

    pointer = pointer + PACKET_POOL_SIZE;

    /* Check for pool creation error. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Create a Client IP instance. */
    status = nx_ip_create(&client_ip, "Client IP", IP_ADDRESS(0, 0, 0, 0),
                          0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                          pointer, 2048, 1);

    pointer =  pointer + 2048;

    /* Check for IP create errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Enable UDP traffic for sending DHCPv6 messages. */
    status =  nx_udp_enable(&client_ip);

    /* Check for UDP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Enable ICMP. */
    status =  nx_icmp_enable(&client_ip);

    /* Check for ICMP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Create the DHCPv6 Client. */
    status =  nx_dhcpv6_client_create(&dhcp_client, &client_ip, "DHCPv6 Client",
                                      &pool_0, pointer, 2048, dhcpv6_state_change_notify,
                                      dhcpv6_server_error_handler);

    /* Check for errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Update the stack pointer because we need it again. */
    pointer = pointer + 2048;

    /* Yield control to DHCPv6 threads and ThreadX. */
    return;
}


/* Define the Client host application thread. */

void    thread_client_entry(ULONG thread_input)
{

UINT        status;
ULONG       T1, T2;
UINT        address_count;
UINT        address_index = 0;
NXD_ADDRESS valid_ipv6_address;
ULONG       preferred_lifetime;
ULONG       valid_lifetime;
UINT        ia_count = 1;

#ifdef NX_DHCPV6_REQUEST_IA_ADDRESS
NXD_ADDRESS ipv6_address;
#endif

#ifdef NX_DHCPV6_REQUEST_OPTION
UCHAR       buffer[200];
NXD_ADDRESS dns_server;
#endif

#ifdef NX_DHCPV6_CLIENT_RESTORE_STATE
ULONG       current_time;
ULONG       elapsed_time;
NX_DHCPV6_CLIENT_RECORD dhcpv6_client_record;
#endif


    state_changes = 0;

    /* Establish the link local address for the host. The RAM driver creates
       a virtual MAC address of 0x1122334456. */
    status = nxd_ipv6_address_set(&client_ip, 0, NX_NULL, 10, NULL);

    if (status)
    {
        error_counter++;
        return;
    }

    /* Let NetX Duo get initialized. */
    tx_thread_sleep(50);

    /* Enable the Client IP for IPv6 and ICMPv6 services. */
    nxd_ipv6_enable(&client_ip);
    nxd_icmp_enable(&client_ip);

    /* Create a Link Layer Plus Time DUID for the DHCPv6 Client. Set time ID field
       to NULL; the DHCPv6 Client API will supply one. */
    status = nx_dhcpv6_create_client_duid(&dhcp_client, NX_DHCPV6_DUID_TYPE_LINK_TIME,
                                          NX_DHCPV6_HW_TYPE_IEEE_802, 0);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Create the DHCPv6 client's Identity Association (IA-NA) now.

       Note that if this host had already been assigned in IPv6 lease, it
       would have to use the assigned T1 and T2 values in loading the DHCPv6
       client with an IANA block.
    */
    status = nx_dhcpv6_create_client_iana(&dhcp_client, DHCPV6_IANA_ID, DHCPV6_T1,  DHCPV6_T2);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

#ifdef NX_DHCPV6_REQUEST_IA_ADDRESS
    memset(&ipv6_address,0x0, sizeof(NXD_ADDRESS));
    ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
    ipv6_address.nxd_ip_address.v6[0] = 0x3ffe0501;
    ipv6_address.nxd_ip_address.v6[1] = 0xffff0100;
    ipv6_address.nxd_ip_address.v6[2] = 0x00000000;
    ipv6_address.nxd_ip_address.v6[3] = 0x0000abcd;

    /* Create an IA address option.
        Note that if this host had already been assigned in IPv6 lease, it
        would have to use the assigned IPv6 address, preferred and valid lifetime
        values in loading the DHCPv6 Client with an IA block.
    */
    status = nx_dhcpv6_add_client_ia(&dhcp_client, &ipv6_address,DHCPV6_RENEW_TIME, DHCPV6_REBIND_TIME);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* If the DHCPv6 Client is configured for a maximum number of IA addresses
       greater than 1, we can add another IA address if the device requires
       multiple global IPv6 addresses. */
    if(NX_DHCPV6_MAX_IA_ADDRESS >= 2)
    {
        memset(&ipv6_address,0x0, sizeof(NXD_ADDRESS));
        ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
        ipv6_address.nxd_ip_address.v6[0] = 0x3ffe0501;
        ipv6_address.nxd_ip_address.v6[1] = 0xffff0100;
        ipv6_address.nxd_ip_address.v6[2] = 0x00000000;
        ipv6_address.nxd_ip_address.v6[3] = 0x00001234;

        /* Add another  IA address option. */
        status = nx_dhcpv6_add_client_ia(&dhcp_client, &ipv6_address, DHCPV6_RENEW_TIME, DHCPV6_REBIND_TIME);

        if (status != NX_SUCCESS)
        {
            error_counter++;
            return;
        }
    }
#endif /* NX_DHCPV6_REQUEST_IA_ADDRESS  */

#ifdef NX_DHCPV6_REQUEST_OPTION
    /* Set the list of DHCPv6 option data to get from the DHCPv6 server if needed. */
    nx_dhcpv6_request_option_timezone(&dhcp_client, NX_TRUE);
    nx_dhcpv6_request_option_DNS_server(&dhcp_client, NX_TRUE);
    nx_dhcpv6_request_option_time_server(&dhcp_client, NX_TRUE);
    nx_dhcpv6_request_option_domain_name(&dhcp_client, NX_TRUE);
#endif /* NX_DHCPV6_REQUEST_OPTION */


#ifdef NX_DHCPV6_REQUEST_FQDN_OPTION
    /* Set the DHCPv6 Client FQDN option.
       operation: NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR         DHCPv6 Client choose to updating the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the client.
                  NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE   DHCPv6 Client choose to updating the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the client to the server.
                  NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE   DHCPv6 Client choose to request that the server perform no DNS updatest on its behalf. */
    nx_dhcpv6_request_option_FQDN(&dhcp_client, "DHCPv6-Client", NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR);
#endif /* NX_DHCPV6_REQUEST_FQDN_OPTION */

    /* Start up the NetX DHCPv6 Client thread task. */
    status =  nx_dhcpv6_start(&dhcp_client);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Start the DHCPv6 by sending a Solicit message out on the network. */
    status = nx_dhcpv6_request_solicit(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Is the DHCPv6 Client request for address assignment successfully started? */
    if (status == NX_SUCCESS)
    {

        /* If Duplicate Address Detection (DAD) is enabled in NetX Duo, e.g. #NXDUO_DISABLE_DAD
           not defined, allow time for NetX Duo to verify the address is unique on our network.
         */
        tx_thread_sleep(500);

        /* Check the bound address. */
        if (bound_addresses != ia_count)
        {

            /* Attempt to find out why DHCPv6 failed, where...*/

            if (server_errors > 0)
            {
                /* Actually you would compare server_error count with number of IA's added
                   to determine if any addresses were assigned. */
                printf("Server error, not all address assigned\n");
            }

            if (address_not_assigned > 0)
            {
                /* Actually you would compare address not assigned count with number of IA's added
                   to determine if any addresses were assigned. */

                printf("No servers responded to some or all of our IAs\n");
            }

        }

        /* Regardless if the DHCPv6 Client achieved a bound state, check for DAD
           failures. */
        if (address_failed_dad > 0)
        {
            /* Actually you would compare failed dad count with number of IA's added
               to determine if any addresses were assigned. */

            printf("Some or all of our IAs failed DAD\n");

        }

        /* Successfully assigned IPv6 addresses! */

        /* Get the count of valid IPv6 address obtained by DHCPv6. */
        status = nx_dhcpv6_get_valid_ip_address_count(&dhcp_client, &address_count);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Get the IPv6 address and related lifetimes by address index. This index is the
           index into the DHCPv6 Client address table. Not to be confused with the IP
           instance address table! */
        status = nx_dhcpv6_get_valid_ip_address_lease_time(&dhcp_client, address_index,
                                                           &valid_ipv6_address, 
                                                               &preferred_lifetime,
                                                           &valid_lifetime);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Get the IANA options for when to start renew/rebind requests. These time
           parameters are the same for all IPv6 addresses assigned in the Client
           e.g. IANA returned from Server. */
        status = nx_dhcpv6_get_iana_lease_time(&dhcp_client, &T1, &T2);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /*****************************************************************************/
        /* These are 'legacy' DHCPv6 services and are for the most part identical to the services
           above except they default to the primary global IPv6 address regardless if the
           Client was assigned more than one global IPv6 address. */

        /* Now check the assigned lease times. */
        status = nx_dhcpv6_get_lease_time_data(&dhcp_client, &T1, &T2,
                                               &preferred_lifetime, &valid_lifetime);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Get the IP address. */
        status = nx_dhcpv6_get_IP_address(&dhcp_client, &valid_ipv6_address);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Bound state. */

#ifdef NX_DHCPV6_CLIENT_RESTORE_STATE

        /* Get the DHCPv6 Client record. */
        nx_dhcpv6_client_get_record(&dhcp_client, &dhcpv6_client_record);

        /* Delete DHCPv6 instance. */
        nx_dhcpv6_client_delete(&dhcp_client);

        /* Delete IP instance. */
        status = nx_ip_delete(&client_ip);

        /* Check for error. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Create a Client IP instance. */
        status = nx_ip_create(&client_ip, "Client IP", IP_ADDRESS(0, 0, 0, 0),
                              0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                              pointer, 2048, 1);

        pointer =  pointer + 2048;

        /* Check for IP create errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Enable UDP traffic for sending DHCPv6 messages. */
        status =  nx_udp_enable(&client_ip);

        /* Check for UDP enable errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Enable ICMP. */
        status =  nx_icmp_enable(&client_ip);

        /* Check for ICMP enable errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Enable the Client IP for IPv6 and ICMPv6 services. */
        status = nxd_ipv6_enable(&client_ip);
        status += nxd_icmp_enable(&client_ip);

        /* Check for IPv6 and ICMPv6 enable errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Establish the link local address for the host. The RAM driver creates
           a virtual MAC address of 0x1122334456. */
        status = nxd_ipv6_address_set(&client_ip, 0, NX_NULL, 10, NULL);

        if (status)
        {
            error_counter++;
            return;
        }

        /* If Duplicate Address Detection (DAD) is enabled in NetX Duo, e.g. #NXDUO_DISABLE_DAD
           not defined, allow time for NetX Duo to verify the address is unique on our network.
         */
        tx_thread_sleep(500);

        /* Create the DHCPv6 Client. */
        status =  nx_dhcpv6_client_create(&dhcp_client, &client_ip, "DHCPv6 Client",
                                          &pool_0, pointer, 2048, dhcpv6_state_change_notify,
                                          dhcpv6_server_error_handler);

        /* Check for errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Update the stack pointer because we need it again. */
        pointer = pointer + 2048;

        /* Restore the DHCPv6 record. */
        nx_dhcpv6_client_restore_record(&dhcp_client, &dhcpv6_client_record, 5);

        /* Resume the DHCPv6 service. */
        nx_dhcpv6_resume(&dhcp_client);
#endif


#ifdef NX_DHCPV6_REQUEST_OPTION

        /* Get the DNS Server address. */
        nx_dhcpv6_get_DNS_server_address(&dhcp_client, 0, &dns_server);

        /* Get the domain name. */
        memset(buffer, 0, sizeof(buffer));

        nx_dhcpv6_get_other_option_data(&dhcp_client, NX_DHCPV6_DOMAIN_NAME_OPTION, buffer, 200); // Try to get DNS info got from DHCPv6 Server

        /* Get the domain name. */
        memset(buffer, 0, sizeof(buffer));

        /* Get the time zone. */
        nx_dhcpv6_get_other_option_data(&dhcp_client, NX_DHCPV6_NEW_POSIX_TIMEZONE_OPTION, buffer, 200); // Try to get DNS info got from DHCPv6 Server
#endif

        /* At some point, we may wish to release the IPv6 address lease e.g. the device
           is leaving the network or powering down. In that case we inform the
           DHCPv6 Server that we are releasing the address lease. */
        status = nx_dhcpv6_request_release(&dhcp_client);

        /* Check status. */
        if (status != NX_SUCCESS)
        {

            error_counter++;
            return;
        }

        /* Send the release message. */
        tx_thread_sleep(100);
    }

    /* Stopping the Client task. */
    status = nx_dhcpv6_stop(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Clear the previously assigned IPv6 addresses from the Client and IP address table. */
    status = nx_dhcpv6_reinitialize(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Start up the Client task again. */
    status = nx_dhcpv6_start(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Begin the request process by sending a Solicit message with the IA created above
       with our preferred IPv6 address. */
    status = nx_dhcpv6_request_solicit(&dhcp_client);
    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Wait a bit before releasing the IP address and terminating the client. */
    tx_thread_sleep(500);

    /* Ok, lets stop the application. Again we DO NOT plan
       to keep the IPv6 address we were assigned and need to release it
       back to the DHCPv6 server. */
    status = nx_dhcpv6_request_release(&dhcp_client);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    /* Now delete the DHCPv6 client and release ThreadX and
       NetX Duo resources back to the system. */
    nx_dhcpv6_client_delete(&dhcp_client);


    return;

}


/* This is the notification from the DHCPv6 Client task that it has changed
   state in the DHCPv6 protocol, for example getting assigned an IPv6 lease and
   achieving the bound state or an IPv6 lease expires and being reset to
   the init state.
*/
VOID dhcpv6_state_change_notify(NX_DHCPV6 *dhcpv6_ptr, UINT old_state, UINT new_state)
{


    /* Increment state change counter. */
    state_changes++;

    /* Check if the Client attempted to request an IPv6 lease but no servers
       responded. */
    if ((old_state == NX_DHCPV6_STATE_SENDING_SOLICIT) && (new_state == NX_DHCPV6_STATE_INIT))
    {

        /* Indication that either DAD failed or IP lease expired. */
        address_not_assigned++;
    }

    /* Check if the Client has been assigned an IPv6 lease. */
    if (new_state == NX_DHCPV6_STATE_BOUND_TO_ADDRESS)
    {
        bound_addresses++;
    }

   /* Check if the Client was bound, but failed the uniqueness check
       (Duplicate Address Detection) and was reset to the INIT state. */
    if ((old_state == NX_DHCPV6_STATE_SENDING_DECLINE) && (new_state == NX_DHCPV6_STATE_INIT))
    {

        /* Indication that DAD failed on Client IA. */
        address_failed_dad++;
    }

    /* Check if the Client was bound, attempted renew the lease but the
       IPv6 address renewal/rebinding failed. */
    if ((old_state == NX_DHCPV6_STATE_SENDING_REBIND) && (new_state == NX_DHCPV6_STATE_INIT))
    {

        /* Indication that the IP lease expired. */
        address_expired++;
    }



    /* Other checks are possible. */

}

/* This is the notification from the DHCPv6 Client task that it received an error
   from the server (status code) in response to the Client's last DHCPv6 message.
*/

VOID dhcpv6_server_error_handler(NX_DHCPV6 *dhcpv6_ptr, UINT op_code, UINT status_code, UINT message_type)
{

    /* Increment the server error count. */
    server_errors++;

    /* This should distinguish between receiving a server error and no server
       available to assign the Client an IPv6 address if the Client fails
       to get assigned an address. */
}

#endif /* FEATURE_NX_IPV6 */
```
