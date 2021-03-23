---
title: Bölüm 3-Azure RTOS NetX Duo Telnet hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX Duo Telnet hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 991ec53aaba052b4f42da6e5a541151953121e76
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825714"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-telnet-services"></a><span data-ttu-id="172cc-103">Bölüm 3-Azure RTOS NetX Duo Telnet hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="172cc-103">Chapter 3 - Description of Azure RTOS NetX Duo Telnet services</span></span>

<span data-ttu-id="172cc-104">Bu bölüm, tüm Azure RTOS NetX Duo Telnet hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="172cc-104">This chapter contains a description of all Azure RTOS NetX Duo Telnet Services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="172cc-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="172cc-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="172cc-106">**nx_telnet_client_connect**: *bir Telnet istemcisini IPv4 adresiyle bağlama*</span><span class="sxs-lookup"><span data-stu-id="172cc-106">**nx_telnet_client_connect**: *Connect a Telnet Client with IPv4 address*</span></span>
- <span data-ttu-id="172cc-107">**nxd_telnet_client_connect**: IPv6 *bir IPv6 Telnet istemcisini IPv6 adresiyle bağlama*</span><span class="sxs-lookup"><span data-stu-id="172cc-107">**nxd_telnet_client_connect**: *Connect an IPv6 Telnet Client with IPv6 address*</span></span>
- <span data-ttu-id="172cc-108">**nx_telnet_client_create**: *bir Telnet istemcisi oluşturma*</span><span class="sxs-lookup"><span data-stu-id="172cc-108">**nx_telnet_client_create**: *Create a Telnet Client*</span></span>
- <span data-ttu-id="172cc-109">**nx_telnet_client_delete**: *bir Telnet istemcisini silme*</span><span class="sxs-lookup"><span data-stu-id="172cc-109">**nx_telnet_client_delete**: *Delete a Telnet Client*</span></span>
- <span data-ttu-id="172cc-110">**nx_telnet_client_disconnect**: *bir Telnet istemcisinin bağlantısını kesme*</span><span class="sxs-lookup"><span data-stu-id="172cc-110">**nx_telnet_client_disconnect**: *Disconnect a Telnet Client*</span></span>
- <span data-ttu-id="172cc-111">**nx_telnet_client_packet_receive**: *Telnet istemcisi aracılığıyla paket alma*</span><span class="sxs-lookup"><span data-stu-id="172cc-111">**nx_telnet_client_packet_receive**: *Receive packet via Telnet Client*</span></span>
- <span data-ttu-id="172cc-112">**nx_telnet_client_packet_send**: *Telnet istemcisi aracılığıyla paket gönder*</span><span class="sxs-lookup"><span data-stu-id="172cc-112">**nx_telnet_client_packet_send**: *Send packet via Telnet Client*</span></span>
- <span data-ttu-id="172cc-113">**nx_telnet_server_create**: *bir Telnet sunucusu oluşturma*</span><span class="sxs-lookup"><span data-stu-id="172cc-113">**nx_telnet_server_create**: *Create a Telnet Server*</span></span>
- <span data-ttu-id="172cc-114">**nx_telnet_server_delete**: *bir Telnet sunucusunu silme*</span><span class="sxs-lookup"><span data-stu-id="172cc-114">**nx_telnet_server_delete**: *Delete a Telnet Server*</span></span>
- <span data-ttu-id="172cc-115">**nx_telnet_server_disconnect**: *bir Telnet istemcisinin bağlantısını kesme*</span><span class="sxs-lookup"><span data-stu-id="172cc-115">**nx_telnet_server_disconnect**: *Disconnect a Telnet Client*</span></span>
- <span data-ttu-id="172cc-116">**nx_telnet_server_get_open_connection_count**: *açık bağlantı sayısını alma*</span><span class="sxs-lookup"><span data-stu-id="172cc-116">**nx_telnet_server_get_open_connection_count**: *Retrieve the number of open connections*</span></span>
- <span data-ttu-id="172cc-117">**nx_telnet_server_packet_send**: *istemci bağlantısı aracılığıyla paket gönder*</span><span class="sxs-lookup"><span data-stu-id="172cc-117">**nx_telnet_server_packet_send**: *Send packet through Client connection*</span></span>
- <span data-ttu-id="172cc-118">**nx_telnet_server_packet_pool_set**: *paket havuzunu Telnet sunucusu paket havuzu olarak ayarla*</span><span class="sxs-lookup"><span data-stu-id="172cc-118">**nx_telnet_server_packet_pool_set**: *Set packet pool as Telnet Server packet pool*</span></span>
- <span data-ttu-id="172cc-119">**nx_telnet_server_start**: *bir Telnet sunucusu başlatın*</span><span class="sxs-lookup"><span data-stu-id="172cc-119">**nx_telnet_server_start**: *Start a Telnet Server*</span></span>
- <span data-ttu-id="172cc-120">**nx_telnet_server_stop**: *bir Telnet sunucusunu durdur*</span><span class="sxs-lookup"><span data-stu-id="172cc-120">**nx_telnet_server_stop**: *Stop a Telnet Server*</span></span>

## <a name="nx_telnet_client_connect"></a><span data-ttu-id="172cc-121">nx_telnet_client_connect</span><span class="sxs-lookup"><span data-stu-id="172cc-121">nx_telnet_client_connect</span></span>

<span data-ttu-id="172cc-122">Bir Telnet Istemcisini IPv4 adresiyle bağlama</span><span class="sxs-lookup"><span data-stu-id="172cc-122">Connect a Telnet Client with IPv4 address</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-123">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-123">Prototype</span></span>

```c
UINT nx_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                              ULONG server_ip, UINT server_port, 
                              ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="172cc-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-124">Description</span></span>

<span data-ttu-id="172cc-125">Bu hizmet, daha önce oluşturulan Telnet Istemci örneğini, Telnet sunucusu için bir IPv4 adresi kullanarak belirtilen IP ve bağlantı noktasındaki sunucuya bağlamayı dener.</span><span class="sxs-lookup"><span data-stu-id="172cc-125">This service attempts to connect the previously created Telnet Client instance to the Server at the specified IP and port using an IPv4 address for the Telnet Server.</span></span> <span data-ttu-id="172cc-126">Bu hizmet, bir NXD_ADDRESS denetim bloğunda ULONG sunucu IP adresini ekler ve aşağıda açıklanan *nxd_telnet_client_connect* hizmeti ÇAĞRıLMADAN önce IP sürümünü 4 ' e ayarlar.</span><span class="sxs-lookup"><span data-stu-id="172cc-126">This service actually inserts the ULONG server IP address in an NXD_ADDRESS control block and sets the IP version to 4 before calling the *nxd_telnet_client_connect* service described below.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-127">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-127">Input Parameters</span></span>

- <span data-ttu-id="172cc-128">**client_ptr**: Telnet istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-128">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="172cc-129">**server_ip**: Telnet sunucusunun IPv4 adresi.</span><span class="sxs-lookup"><span data-stu-id="172cc-129">**server_ip**: IPv4 Address of the Telnet Server.</span></span>
- <span data-ttu-id="172cc-130">**SERVER_PORT**: sunucu TCP bağlantı noktası (Telnet sunucusu bağlantı noktası 23 ' dir).</span><span class="sxs-lookup"><span data-stu-id="172cc-130">**server_port**: TCP Port of Server (Telnet Server is port 23).</span></span>
- <span data-ttu-id="172cc-131">**wait_option**: hizmetin Telnet istemcisi bağlantısı için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="172cc-131">**wait_option**: Defines how long the service will wait for the Telnet Client connect.</span></span> <span data-ttu-id="172cc-132">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="172cc-132">The wait options are defined as follows:</span></span>

    - <span data-ttu-id="172cc-133">**zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="172cc-133">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="172cc-134">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="172cc-134">**TX_WAIT_FOREVER**: (0xFFFFFFFF)Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-135">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-135">Return Values</span></span>

- <span data-ttu-id="172cc-136">**NX_SUCCESS**: (0x00) Istemci bağlantısı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="172cc-136">**NX_SUCCESS**: (0x00) Successful Client connect.</span></span>
- <span data-ttu-id="172cc-137">**NX_TELNET_NOT_DISCONNECTED**: (0xf4) istemci zaten bağlı.</span><span class="sxs-lookup"><span data-stu-id="172cc-137">**NX_TELNET_NOT_DISCONNECTED**: (0xF4) Client already connected.</span></span>
- <span data-ttu-id="172cc-138">NX_PTR_ERROR: (0x07) geçersiz Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-138">NX_PTR_ERROR: (0x07) Invalid Client pointer.</span></span>
- <span data-ttu-id="172cc-139">NX_IP_ADDRESS_ERROR: (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="172cc-139">NX_IP_ADDRESS_ERROR: (0x21) Invalid IP address.</span></span>
- <span data-ttu-id="172cc-140">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="172cc-140">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-141">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-141">Allowed From</span></span>

<span data-ttu-id="172cc-142">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-142">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-143">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-143">Example</span></span>

```c
/* Connect the Telnet Client instance “my_client” to the Server at 
   IP address 1.2.3.4 and port 23.  */
status =  nx_telnet_client_connect(&my_client, IP_ADDRESS(1,2,3,4), 23, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   connected to the Telnet Server.  */
```

## <a name="nxd_telnet_client_connect"></a><span data-ttu-id="172cc-144">nxd_telnet_client_connect</span><span class="sxs-lookup"><span data-stu-id="172cc-144">nxd_telnet_client_connect</span></span>

<span data-ttu-id="172cc-145">Bir Telnet Istemcisini IPv6 veya IPv4 adresiyle bağlama</span><span class="sxs-lookup"><span data-stu-id="172cc-145">Connect a Telnet Client with IPv6 or IPv4 address</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-146">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-146">Prototype</span></span>

```c
UINT nxd_telnet_client_connect(NX_TELNET_CLIENT *client_ptr, 
                               NXD_ADDRESS *server_ip_address, 
                               UINT server_port, 
                               ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="172cc-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-147">Description</span></span>

<span data-ttu-id="172cc-148">Bu hizmet, daha önce oluşturulan Telnet Istemci örneğini, Telnet sunucusunun IPv6 adresini kullanarak belirtilen IP ve bağlantı noktasındaki sunucuya bağlamayı dener.</span><span class="sxs-lookup"><span data-stu-id="172cc-148">This service attempts to connect the previously created Telnet Client instance to the Server at the specified IP and port using the Telnet Server’s IPv6 address.</span></span> <span data-ttu-id="172cc-149">Bu hizmet bir IPv4 veya IPv6 adresi alabilir, ancak NXD_ADDRESS değişken *server_ip_address içermeli.*</span><span class="sxs-lookup"><span data-stu-id="172cc-149">This service can take an IPv4 or an IPv6 address but must be contained in the NXD_ADDRESS variable *server_ip_address.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-150">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-150">Input Parameters</span></span>

- <span data-ttu-id="172cc-151">**client_ptr**: Telnet istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-151">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="172cc-152">**server_ip_address**: sunucunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="172cc-152">**server_ip_address**: IP Address of Server.</span></span>
- <span data-ttu-id="172cc-153">**SERVER_PORT**: sunucu TCP bağlantı noktası (Telnet sunucusu bağlantı noktası 23 ' dir).</span><span class="sxs-lookup"><span data-stu-id="172cc-153">**server_port**: TCP Port of Server (Telnet Server is port 23).</span></span>
- <span data-ttu-id="172cc-154">**wait_option**: hizmetin Telnet istemcisi bağlantısı için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="172cc-154">**wait_option**: Defines how long the service will wait for the Telnet Client connect.</span></span> <span data-ttu-id="172cc-155">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="172cc-155">The wait options are defined as follows:</span></span>

    - <span data-ttu-id="172cc-156">**zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="172cc-156">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="172cc-157">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="172cc-157">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-158">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-158">Return Values</span></span>

- <span data-ttu-id="172cc-159">**NX_SUCCESS**: (0x00) Istemci bağlantısı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="172cc-159">**NX_SUCCESS**: (0x00) Successful Client connect.</span></span>
- <span data-ttu-id="172cc-160">**NX_TELNET_ERROR**: (0Xf0) istemci bağlantı hatası.</span><span class="sxs-lookup"><span data-stu-id="172cc-160">**NX_TELNET_ERROR**: (0xF0) Client connect error.</span></span>
- <span data-ttu-id="172cc-161">**NX_TELNET_NOT_DISCONNECTED**: (0xf4) istemci zaten bağlı.</span><span class="sxs-lookup"><span data-stu-id="172cc-161">**NX_TELNET_NOT_DISCONNECTED**: (0xF4) Client already connected.</span></span>
- <span data-ttu-id="172cc-162">NX_PTR_ERROR: (0x07) geçersiz Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-162">NX_PTR_ERROR: (0x07) Invalid Client pointer.</span></span>
- <span data-ttu-id="172cc-163">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="172cc-163">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="172cc-164">NX_TELNET_INVALID_PARAMETER: (0xF5) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="172cc-164">NX_TELNET_INVALID_PARAMETER: (0xF5) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-165">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-165">Allowed From</span></span>

<span data-ttu-id="172cc-166">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-166">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-167">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-167">Example</span></span>

```c
/* Connect the Telnet Client instance “my_client” to the Server at 
   IPv6 address 20010db1:0:f101::101 and port 23.  */
status =  nxd_telnet_client_connect(&my_client, &server_ip_address, 23, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   connected to the Telnet Server.  */
```

## <a name="nx_telnet_client_create"></a><span data-ttu-id="172cc-168">nx_telnet_client_create</span><span class="sxs-lookup"><span data-stu-id="172cc-168">nx_telnet_client_create</span></span>

<span data-ttu-id="172cc-169">Telnet Istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="172cc-169">Create a Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-170">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-170">Prototype</span></span>

```c
UINT nx_telnet_client_create(NX_TELNET_CLIENT *client_ptr, 
                             CHAR *client_name, NX_IP *ip_ptr, 
                             ULONG window_size);
```

### <a name="description"></a><span data-ttu-id="172cc-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-171">Description</span></span>

<span data-ttu-id="172cc-172">Bu hizmet bir Telnet Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="172cc-172">This service creates a Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-173">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-173">Input Parameters</span></span>

- <span data-ttu-id="172cc-174">**client_ptr**: Telnet istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-174">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="172cc-175">**client_name**: istemci örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="172cc-175">**client_name**: Name of Client instance.</span></span>
- <span data-ttu-id="172cc-176">**ip_ptr**: IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="172cc-176">**ip_ptr**: Pointer to IP instance.</span></span>
- <span data-ttu-id="172cc-177">**window_size**: Bu ISTEMCI için TCP alma penceresinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="172cc-177">**window_size**: Size of TCP receive window for this Client.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-178">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-178">Return Values</span></span>

- <span data-ttu-id="172cc-179">**NX_SUCCESS**: (0x00) Istemci oluşturma başarılı.</span><span class="sxs-lookup"><span data-stu-id="172cc-179">**NX_SUCCESS**: (0x00) Successful Client create.</span></span>
- <span data-ttu-id="172cc-180">**NX_TELNET_ERROR**: (0Xf0) yuva oluşturma hatası.</span><span class="sxs-lookup"><span data-stu-id="172cc-180">**NX_TELNET_ERROR**: (0xF0) Socket create error.</span></span>
- <span data-ttu-id="172cc-181">NX_PTR_ERROR: (0x07) geçersiz Istemci veya IP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-181">NX_PTR_ERROR: (0x07) Invalid Client or IP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-182">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-182">Allowed From</span></span>

<span data-ttu-id="172cc-183">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-183">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-184">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-184">Example</span></span>

```c
/* Create the Telnet Client instance “my_client” on the IP instance “ip_0”.  */
status =  nx_telnet_client_create(&my_client, “My Telnet Client”, &ip_0, 2048);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   created.  */
```
## <a name="nx_telnet_client_delete"></a><span data-ttu-id="172cc-185">nx_telnet_client_delete</span><span class="sxs-lookup"><span data-stu-id="172cc-185">nx_telnet_client_delete</span></span>

<span data-ttu-id="172cc-186">Bir Telnet Istemcisini silme</span><span class="sxs-lookup"><span data-stu-id="172cc-186">Delete a Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-187">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-187">Prototype</span></span>

```c
UINT nx_telnet_client_delete(NX_TELNET_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="172cc-188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-188">Description</span></span>

<span data-ttu-id="172cc-189">Bu hizmet, önceden oluşturulmuş bir Telnet Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="172cc-189">This service deletes a previously created Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-190">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-190">Input Parameters</span></span>

- <span data-ttu-id="172cc-191">**client_ptr**: Telnet istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-191">**client_ptr**: Pointer to Telnet Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-192">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-192">Return Values</span></span>

- <span data-ttu-id="172cc-193">**NX_SUCCESS**: (0x00) Istemci silme başarılı.</span><span class="sxs-lookup"><span data-stu-id="172cc-193">**NX_SUCCESS**: (0x00) Successful Client delete.</span></span>
- <span data-ttu-id="172cc-194">**NX_TELNET_NOT_DISCONNECTED**: (0xf4) istemci hala bağlı.</span><span class="sxs-lookup"><span data-stu-id="172cc-194">**NX_TELNET_NOT_DISCONNECTED**: (0xF4) Client still connected.</span></span>
- <span data-ttu-id="172cc-195">NX_PTR_ERROR: (0x07) geçersiz Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-195">NX_PTR_ERROR: (0x07) Invalid Client pointer.</span></span>
- <span data-ttu-id="172cc-196">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="172cc-196">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-197">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-197">Allowed From</span></span>

<span data-ttu-id="172cc-198">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-198">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-199">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-199">Example</span></span>

```c
/* Delete the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_delete(&my_client);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   deleted.  */
```

## <a name="nx_telnet_client_disconnect"></a><span data-ttu-id="172cc-200">nx_telnet_client_disconnect</span><span class="sxs-lookup"><span data-stu-id="172cc-200">nx_telnet_client_disconnect</span></span>

<span data-ttu-id="172cc-201">Telnet Istemcisinin bağlantısını kesme</span><span class="sxs-lookup"><span data-stu-id="172cc-201">Disconnect a Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-202">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-202">Prototype</span></span>

```c
UINT nx_telnet_client_disconnect(NX_TELNET_CLIENT *client_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="172cc-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-203">Description</span></span>

<span data-ttu-id="172cc-204">Bu hizmet, daha önce bağlı bir Telnet Istemci örneğinin bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="172cc-204">This service disconnects a previously connected Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-205">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-205">Input Parameters</span></span>

- <span data-ttu-id="172cc-206">**client_ptr**: Telnet istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-206">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="172cc-207">**wait_option**: hizmetin Telnet istemcisinin bağlantısını kesmek için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="172cc-207">**wait_option**: Defines how long the service will wait for the Telnet Client disconnect.</span></span> <span data-ttu-id="172cc-208">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="172cc-208">The wait options are defined as follows:</span></span>

    - <span data-ttu-id="172cc-209">**zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="172cc-209">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="172cc-210">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="172cc-210">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-211">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-211">Return Values</span></span>

- <span data-ttu-id="172cc-212">**NX_SUCCESS**: (0x00) Istemci bağlantısının başarıyla kesilmesi.</span><span class="sxs-lookup"><span data-stu-id="172cc-212">**NX_SUCCESS**: (0x00) Successful Client disconnect.</span></span>
- <span data-ttu-id="172cc-213">**NX_TELNET_NOT_CONNECTED**: (0Xf3) istemci bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="172cc-213">**NX_TELNET_NOT_CONNECTED**: (0xF3) Client not connected.</span></span>
- <span data-ttu-id="172cc-214">NX_PTR_ERROR: (0x07) geçersiz Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-214">NX_PTR_ERROR: (0x07) Invalid Client pointer.</span></span>
- <span data-ttu-id="172cc-215">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="172cc-215">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="172cc-216">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-216">Allowed From</span></span>

<span data-ttu-id="172cc-217">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-217">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-218">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-218">Example</span></span>

```c

/* Disconnect the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_disconnect(&my_client, 100);

/* If status is NX_SUCCESS the Telnet Client instance was successfully
   disconnected.  */
```

## <a name="nx_telnet_client_packet_receive"></a><span data-ttu-id="172cc-219">nx_telnet_client_packet_receive</span><span class="sxs-lookup"><span data-stu-id="172cc-219">nx_telnet_client_packet_receive</span></span>

<span data-ttu-id="172cc-220">Telnet Istemcisi aracılığıyla paket alma</span><span class="sxs-lookup"><span data-stu-id="172cc-220">Receive packet via Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-221">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-221">Prototype</span></span>

```c
UINT nx_telnet_client_packet_receive(NX_TELNET_CLIENT *client_ptr, 
                                     NX_PACKET **packet_ptr, 
                                     ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="172cc-222">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-222">Description</span></span>

<span data-ttu-id="172cc-223">Bu hizmet, daha önce bağlı olan Telnet Istemci örneğinden bir paket alır.</span><span class="sxs-lookup"><span data-stu-id="172cc-223">This service receives a packet from the previously connected Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-224">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-224">Input Parameters</span></span>

- <span data-ttu-id="172cc-225">**client_ptr**: Telnet istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-225">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="172cc-226">**packet_ptr**: alınan paket için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-226">**packet_ptr**: Pointer to the destination for the received packet.</span></span>
- <span data-ttu-id="172cc-227">**wait_option**: hizmetin Telnet istemci paketi alma süresini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="172cc-227">**wait_option**: Defines how long the service will wait for the Telnet Client packet receive.</span></span> <span data-ttu-id="172cc-228">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="172cc-228">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="172cc-229">**zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="172cc-229">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="172cc-230">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="172cc-230">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-231">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-231">Return Values</span></span>

- <span data-ttu-id="172cc-232">**NX_SUCCESS**: (0x00) istemci paketi alma başarılı.</span><span class="sxs-lookup"><span data-stu-id="172cc-232">**NX_SUCCESS**: (0x00) Successful Client packet receive.</span></span>
- <span data-ttu-id="172cc-233">NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="172cc-233">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="172cc-234">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="172cc-234">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-235">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-235">Allowed From</span></span>

<span data-ttu-id="172cc-236">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-236">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-237">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-237">Example</span></span>

```c

/* Receive a packet from the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_receive(&my_client, &my_packet, 100);

/* If status is NX_SUCCESS the “my_packet” pointer contains data received from
   the Telnet Client connection.  */
```
## <a name="nx_telnet_client_packet_send"></a><span data-ttu-id="172cc-238">nx_telnet_client_packet_send</span><span class="sxs-lookup"><span data-stu-id="172cc-238">nx_telnet_client_packet_send</span></span>

<span data-ttu-id="172cc-239">Telnet Istemcisi aracılığıyla paket gönder</span><span class="sxs-lookup"><span data-stu-id="172cc-239">Send packet via Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-240">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-240">Prototype</span></span>

```c
UINT nx_telnet_client_packet_send(NX_TELNET_CLIENT *client_ptr, 
                                  NX_PACKET *packet_ptr, 
                                  ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="172cc-241">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-241">Description</span></span>

<span data-ttu-id="172cc-242">Bu hizmet, daha önce bağlı olan Telnet Istemci örneği aracılığıyla bir paket gönderir.</span><span class="sxs-lookup"><span data-stu-id="172cc-242">This service sends a packet through the previously connected Telnet Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-243">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-243">Input Parameters</span></span>

- <span data-ttu-id="172cc-244">**client_ptr**: Telnet istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-244">**client_ptr**: Pointer to Telnet Client control block.</span></span>
- <span data-ttu-id="172cc-245">**packet_ptr**: gönderileceği pakete yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="172cc-245">**packet_ptr**: Pointer to the packet to send.</span></span>
- <span data-ttu-id="172cc-246">**wait_option**: hizmetin Telnet istemci paketinin gönderilmesi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="172cc-246">**wait_option**: Defines how long the service will wait for the Telnet Client packet send.</span></span> <span data-ttu-id="172cc-247">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="172cc-247">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="172cc-248">**zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="172cc-248">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="172cc-249">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="172cc-249">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-250">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-250">Return Values</span></span>

- <span data-ttu-id="172cc-251">**NX_SUCCESS**: (0x00) başarılı istemci paketi gönderme.</span><span class="sxs-lookup"><span data-stu-id="172cc-251">**NX_SUCCESS**: (0x00) Successful Client packet send.</span></span>
- <span data-ttu-id="172cc-252">**NX_TELNET_ERROR**: (0Xf0) paket gönderme başarısız oldu – çağıran, paketi serbest bırakmaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="172cc-252">**NX_TELNET_ERROR**: (0xF0) Send packet failed – caller is responsible for releasing the packet.</span></span>
- <span data-ttu-id="172cc-253">NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="172cc-253">NX_PTR_ERROR: (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="172cc-254">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="172cc-254">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-255">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-255">Allowed From</span></span>

<span data-ttu-id="172cc-256">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-256">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-257">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-257">Example</span></span>

```c
/* Send a packet via the Telnet Client instance “my_client”.  */
status =  nx_telnet_client_packet_send(&my_client, my_packet, 100);
/* If status is NX_SUCCESS the packet was successfully sent.  */

```

## <a name="nx_telnet_server_create"></a><span data-ttu-id="172cc-258">nx_telnet_server_create</span><span class="sxs-lookup"><span data-stu-id="172cc-258">nx_telnet_server_create</span></span>

<span data-ttu-id="172cc-259">Telnet sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="172cc-259">Create a Telnet Server</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-260">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-260">Prototype</span></span>

```c
UINT nx_telnet_server_create(NX_TELNET_SERVER *server_ptr, CHAR *server_name, NX_IP *ip_ptr, 
                             VOID *stack_ptr, ULONG stack_size, 
                             void (*new_connection)(struct NX_TELNET_SERVER_STRUCT*telnet_server_ptr, 
                                                    UINT logical_connection), 
                             void (*receive_data)(struct NX_TELNET_SERVER_STRUCT *telnet_server_ptr, 
                                                  UINT logical_connection, NX_PACKET *packet_ptr), 
                             void (*connection_end)(struct NX_TELNET_SERVER_STRUCT *telnet_server_ptr, 
                                                    UINT logical_connection));

```

### <a name="description"></a><span data-ttu-id="172cc-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-261">Description</span></span>

<span data-ttu-id="172cc-262">Bu hizmet, belirtilen IP örneğinde bir Telnet Server örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="172cc-262">This service creates a Telnet Server instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-263">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-263">Input Parameters</span></span>

- <span data-ttu-id="172cc-264">**server_ptr**: Telnet sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-264">**server_ptr**: Pointer to Telnet Server control block.</span></span>
- <span data-ttu-id="172cc-265">**SERVER_NAME**: Telnet sunucu örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="172cc-265">**server_name**: Name of Telnet Server instance.</span></span>
- <span data-ttu-id="172cc-266">**ip_ptr**: ilişkili IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="172cc-266">**ip_ptr**: Pointer to associated IP instance.</span></span>
- <span data-ttu-id="172cc-267">**stack_ptr**: iç sunucu iş parçacığı için yığın işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-267">**stack_ptr**: Pointer to stack for the internal Server thread.</span></span>
- <span data-ttu-id="172cc-268">**sack_size**: yığının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="172cc-268">**sack_size**: Size of the stack, in bytes.</span></span>
- <span data-ttu-id="172cc-269">**new_connection**: uygulama geri çağırma yordamı işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-269">**new_connection**: Application callback routine function pointer.</span></span> <span data-ttu-id="172cc-270">Bu yordam, sunucu tarafından her yeni bir Telnet Istemci bağlantı isteği algılandığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="172cc-270">This routine is called whenever a new Telnet Client connection request is detected by the Server.</span></span>
- <span data-ttu-id="172cc-271">**receive_data**: uygulama geri çağırma yordamı işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-271">**receive_data**: Application callback routine function pointer.</span></span> <span data-ttu-id="172cc-272">Bu yordam, bağlantıda her yeni bir Telnet Istemci verisi olduğunda çağrılır.</span><span class="sxs-lookup"><span data-stu-id="172cc-272">This routine is called whenever a new Telnet Client data is present on the connection.</span></span> <span data-ttu-id="172cc-273">Bu yordam, paketin serbest bırakılmasından sorumludur.</span><span class="sxs-lookup"><span data-stu-id="172cc-273">This routine is responsible for releasing the packet.</span></span>
- <span data-ttu-id="172cc-274">**end_connection**: uygulama geri çağırma yordamı işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-274">**end_connection**: Application callback routine function pointer.</span></span> <span data-ttu-id="172cc-275">Bu yordam, bir Telnet Istemci bağlantısının Istemci tarafından bağlantısı kesildiğinde veya Istemci bağlantısı zaman aşımına uğradığında ("etkinlik zaman aşımı" süresi dolduğunda) çağrılır.</span><span class="sxs-lookup"><span data-stu-id="172cc-275">This routine is called whenever a Telnet Client connection is disconnected by the Client or the Client connection times out (“activity timeout” expires).</span></span> <span data-ttu-id="172cc-276">Sunucu ayrıca aşağıda açıklanan *nx_telnet_server_disconnect* hizmeti aracılığıyla bağlantısını kesebilir.</span><span class="sxs-lookup"><span data-stu-id="172cc-276">The Server can also disconnect via the *nx_telnet_server_disconnect* service described below.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-277">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-277">Return Values</span></span>

- <span data-ttu-id="172cc-278">**NX_SUCCESS**: (0x00) sunucu oluşturma başarılı.</span><span class="sxs-lookup"><span data-stu-id="172cc-278">**NX_SUCCESS**: (0x00) Successful Server create.</span></span>
- <span data-ttu-id="172cc-279">NX_PTR_ERROR: (0x07) sunucu, IP, yığın veya uygulama geri çağırma işaretçileri geçersiz.</span><span class="sxs-lookup"><span data-stu-id="172cc-279">NX_PTR_ERROR: (0x07) Invalid Server, IP, stack, or application callback pointers.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-280">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-280">Allowed From</span></span>

<span data-ttu-id="172cc-281">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-281">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-282">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-282">Example</span></span>

```c
/* Create a Telnet Server instance “my_server”.  */
status =  nx_telnet_server_create(&my_server, "Telnet Server", &ip_0, 
                                   pointer, 2048, telnet_new_connection, 
                                   telnet_receive_data, telnet_connection_end);


/* If status is NX_SUCCESS the Telnet Server was successfully created.  */
```
## <a name="nx_telnet_server_delete"></a><span data-ttu-id="172cc-283">nx_telnet_server_delete</span><span class="sxs-lookup"><span data-stu-id="172cc-283">nx_telnet_server_delete</span></span>

<span data-ttu-id="172cc-284">Bir Telnet sunucusunu silme</span><span class="sxs-lookup"><span data-stu-id="172cc-284">Delete a Telnet Server</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-285">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-285">Prototype</span></span>

```c
UINT nx_telnet_server_delete(NX_TELNET_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="172cc-286">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-286">Description</span></span>

<span data-ttu-id="172cc-287">Bu hizmet, önceden oluşturulmuş bir Telnet sunucusu örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="172cc-287">This service deletes a previously created Telnet Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-288">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-288">Input Parameters</span></span>

- <span data-ttu-id="172cc-289">**server_ptr**: Telnet sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-289">**server_ptr**: Pointer to Telnet Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-290">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-290">Return Values</span></span>

- <span data-ttu-id="172cc-291">**NX_SUCCESS**: (0x00) sunucu başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="172cc-291">**NX_SUCCESS**: (0x00) Successful Server delete.</span></span>
- <span data-ttu-id="172cc-292">NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-292">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="172cc-293">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="172cc-293">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-294">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-294">Allowed From</span></span>

<span data-ttu-id="172cc-295">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-295">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-296">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-296">Example</span></span>

```c
/* Delete the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_delete(&my_server);

/* If status is NX_SUCCESS the Telnet Server was successfully deleted.  */
```

## <a name="nx_telnet_server_disconnect"></a><span data-ttu-id="172cc-297">nx_telnet_server_disconnect</span><span class="sxs-lookup"><span data-stu-id="172cc-297">nx_telnet_server_disconnect</span></span>

<span data-ttu-id="172cc-298">Telnet Istemcisinin bağlantısını kesme</span><span class="sxs-lookup"><span data-stu-id="172cc-298">Disconnect a Telnet Client</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-299">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-299">Prototype</span></span>

```c
UINT nx_telnet_server_disconnect(NX_TELNET_SERVER *server_ptr, UINT logical_connection);
```

### <a name="description"></a><span data-ttu-id="172cc-300">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-300">Description</span></span>

<span data-ttu-id="172cc-301">Bu hizmet, bu Telnet sunucu örneğindeki daha önce bağlı bir Istemcinin bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="172cc-301">This service disconnects a previously connected Client on this Telnet Server instance.</span></span> <span data-ttu-id="172cc-302">Bu yordam tipik olarak, alınan verilerde algılanan bir koşula yanıt olarak uygulamanın veri geri çağırma işlevinden çağrılır.</span><span class="sxs-lookup"><span data-stu-id="172cc-302">This routine is typically called from the application’s receive data callback function in response to a condition detected in the data received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-303">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-303">Input Parameters</span></span>

- <span data-ttu-id="172cc-304">**server_ptr**: Telnet sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-304">**server_ptr**: Pointer to Telnet Server control block.</span></span>
- <span data-ttu-id="172cc-305">**logical_connection**: Bu sunucudaki istemci bağlantısına karşılık gelen mantıksal bağlantı.</span><span class="sxs-lookup"><span data-stu-id="172cc-305">**logical_connection**: Logical connection corresponding the Client connection on this Server.</span></span> <span data-ttu-id="172cc-306">0 ile NX_TELENET_MAX_CLIENTS arasında geçerli değer aralığı.</span><span class="sxs-lookup"><span data-stu-id="172cc-306">Valid value range from 0 through NX_TELENET_MAX_CLIENTS.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-307">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-307">Return Values</span></span>

- <span data-ttu-id="172cc-308">**NX_SUCCESS**: (0x00) sunucu bağlantısı başarıyla kesilir.</span><span class="sxs-lookup"><span data-stu-id="172cc-308">**NX_SUCCESS**: (0x00) Successful Server disconnect.</span></span>
- <span data-ttu-id="172cc-309">**NX_TELNET_ERROR**: (0Xf0) sunucu bağlantısı kesilemedi.</span><span class="sxs-lookup"><span data-stu-id="172cc-309">**NX_TELNET_ERROR**: (0xF0) Server disconnect failed.</span></span>
- <span data-ttu-id="172cc-310">NX_OPTION_ERROR: (0x0A) geçersiz mantıksal bağlantı.</span><span class="sxs-lookup"><span data-stu-id="172cc-310">NX_OPTION_ERROR: (0x0A) Invalid logical connection.</span></span>
- <span data-ttu-id="172cc-311">NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-311">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="172cc-312">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="172cc-312">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-313">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-313">Allowed From</span></span>

<span data-ttu-id="172cc-314">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-314">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-315">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-315">Example</span></span>

```c

/* Disconnect the Telnet Client associated with logical connection 2 on 
   the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_disconnect(&my_server, 2);

/* If status is NX_SUCCESS the Client on logical connection 2 was 
   disconnected.  */
```

## <a name="nx_telnet_server_get_open_connection_count"></a><span data-ttu-id="172cc-316">nx_telnet_server_get_open_connection_count</span><span class="sxs-lookup"><span data-stu-id="172cc-316">nx_telnet_server_get_open_connection_count</span></span>

<span data-ttu-id="172cc-317">Açık durumdaki bağlantıların geri dönüş sayısı</span><span class="sxs-lookup"><span data-stu-id="172cc-317">Return number of currently open connections</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-318">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-318">Prototype</span></span>

```c
UINT nx_telnet_server_get_open_connection_count(NX_TELNET_SERVER *server_ptr, UINT *connection_count);
```

### <a name="description"></a><span data-ttu-id="172cc-319">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-319">Description</span></span>

<span data-ttu-id="172cc-320">Bu hizmet, şu anda bağlı olan Telnet Istemcilerinin sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="172cc-320">This service returns the number of currently connected Telnet Clients.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-321">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-321">Input Parameters</span></span>

- <span data-ttu-id="172cc-322">**server_ptr**: Telnet sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-322">**server_ptr**: Pointer to Telnet Server control block.</span></span>
- <span data-ttu-id="172cc-323">**Connection_count**: bağlantı sayısını depolamak için bellek işaretçisi</span><span class="sxs-lookup"><span data-stu-id="172cc-323">**Connection_count**: Pointer to memory to store connection count</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-324">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-324">Return Values</span></span>

- <span data-ttu-id="172cc-325">**NX_SUCCESS**: (0x00) başarılı tamamlama.</span><span class="sxs-lookup"><span data-stu-id="172cc-325">**NX_SUCCESS**: (0x00) Successful completion.</span></span>
- <span data-ttu-id="172cc-326">NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-326">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="172cc-327">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="172cc-327">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-328">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-328">Allowed From</span></span>

<span data-ttu-id="172cc-329">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-329">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-330">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-330">Example</span></span>

```c
/* Get the number of Telnet Clients connected to the Server. */

status =  nx_telnet_server_get_open_connection_count(&my_server, &conn_count);

/* If status is NX_SUCCESS the conn_count holds the number of open connections.  */

```

## <a name="nx_telnet_server_packet_send"></a><span data-ttu-id="172cc-331">nx_telnet_server_packet_send</span><span class="sxs-lookup"><span data-stu-id="172cc-331">nx_telnet_server_packet_send</span></span>

<span data-ttu-id="172cc-332">Istemci bağlantısı aracılığıyla paket gönder</span><span class="sxs-lookup"><span data-stu-id="172cc-332">Send packet through Client connection</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-333">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-333">Prototype</span></span>

```c
UINT nx_telnet_server_packet_send(NX_TELNET_SERVER *server_ptr, 
                                  UINT logical_connection, 
                                  NX_PACKET *packet_ptr, 
                                  ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="172cc-334">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-334">Description</span></span>

<span data-ttu-id="172cc-335">Bu hizmet, bu Telnet sunucu örneğindeki Istemci bağlantısına bir paket gönderir.</span><span class="sxs-lookup"><span data-stu-id="172cc-335">This service sends a packet to the Client connection on this Telnet Server instance.</span></span> <span data-ttu-id="172cc-336">Bu yordam tipik olarak, alınan verilerde algılanan bir koşula yanıt olarak uygulamanın veri geri çağırma işlevinden çağrılır.</span><span class="sxs-lookup"><span data-stu-id="172cc-336">This routine is typically called from the application’s receive data callback function in response to a condition detected in the data received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-337">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-337">Input Parameters</span></span>

- <span data-ttu-id="172cc-338">**server_ptr**: Telnet sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-338">**server_ptr**: Pointer to Telnet Server control block.</span></span>
- <span data-ttu-id="172cc-339">**logical_connection**: Bu sunucudaki istemci bağlantısına karşılık gelen mantıksal bağlantı.</span><span class="sxs-lookup"><span data-stu-id="172cc-339">**logical_connection**: Logical connection corresponding the Client connection on this Server.</span></span> <span data-ttu-id="172cc-340">0 ile NX_TELENET_MAX_CLIENTS arasında geçerli değer aralığı.</span><span class="sxs-lookup"><span data-stu-id="172cc-340">Valid value range from 0 through NX_TELENET_MAX_CLIENTS.</span></span>
- <span data-ttu-id="172cc-341">**packet_ptr**: alınan pakete yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="172cc-341">**packet_ptr**: Pointer to the received packet.</span></span>
- <span data-ttu-id="172cc-342">**wait_option**: hizmetin Telnet sunucusu paketini gönderme süresini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="172cc-342">**wait_option**: Defines how long the service will wait for the Telnet Server packet send.</span></span> <span data-ttu-id="172cc-343">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="172cc-343">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="172cc-344">**zaman aşımı değeri**: (0x00000001-0xfffffffe) sayısal değer (1-0XFFFFFFFE) seçildiğinde, Telnet sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="172cc-344">**timeout value**: (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the Telnet Server response.</span></span>
    - <span data-ttu-id="172cc-345">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi, çağıran iş parçacığının, Telnet sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="172cc-345">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the Telnet Server responds to the request.</span></span> 

### <a name="return-values"></a><span data-ttu-id="172cc-346">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-346">Return Values</span></span>

- <span data-ttu-id="172cc-347">**NX_SUCCESS**: (0x00) başarılı paket gönderme.</span><span class="sxs-lookup"><span data-stu-id="172cc-347">**NX_SUCCESS**: (0x00) Successful packet send.</span></span>
- <span data-ttu-id="172cc-348">**NX_TELNET_FAILED**: (0Xf2) TCP yuvası gönderme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="172cc-348">**NX_TELNET_FAILED**: (0xF2) TCP socket send failed.</span></span>
- <span data-ttu-id="172cc-349">NX_OPTION_ERROR: (0x0A) geçersiz mantıksal bağlantı.</span><span class="sxs-lookup"><span data-stu-id="172cc-349">NX_OPTION_ERROR: (0x0A) Invalid logical connection.</span></span>
- <span data-ttu-id="172cc-350">NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-350">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="172cc-351">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı.</span><span class="sxs-lookup"><span data-stu-id="172cc-351">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-352">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-352">Allowed From</span></span>

<span data-ttu-id="172cc-353">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-353">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-354">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-354">Example</span></span>

```c
/* Send a packet to the Telnet Client associated with logical connection 2 on 
   the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_packet_send(&my_server, 2, my_packet, 100);

/* If status is NX_SUCCESS the packet was sent to the Client on logical 
   connection 2.  */
```

## <a name="nx_telnet_server_packet_pool_set"></a><span data-ttu-id="172cc-355">nx_telnet_server_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="172cc-355">nx_telnet_server_packet_pool_set</span></span>

<span data-ttu-id="172cc-356">Daha önce oluşturulan paket havuzunu Telnet sunucu havuzu olarak ayarla</span><span class="sxs-lookup"><span data-stu-id="172cc-356">Set previously created packet pool as Telnet Server pool</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-357">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-357">Prototype</span></span>

```c
UINT nx_telnet_server_packet_pool_set(NX_TELNET_SERVER *server_ptr, NX_PACKET_POOL *packet_pool_ptr);

```

### <a name="description"></a><span data-ttu-id="172cc-358">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-358">Description</span></span>

<span data-ttu-id="172cc-359">Bu hizmet, NX_TELNET_SERVER_USER_CREATE_PACKET_POOL tanımlanmışsa, daha önce oluşturulmuş bir paket havuzunu Telnet sunucusu paket havuzu olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="172cc-359">This service sets a previously created packet pool as the Telnet Server packet pool if NX_TELNET_SERVER_USER_CREATE_PACKET_POOL is defined.</span></span> <span data-ttu-id="172cc-360">Ayrıca, Telnet sunucusunun Telnet istemcilerine Telnet seçeneklerini iletmek için bir paket havuzuna ihtiyacı olacak şekilde NX_TELNET_SERVER_OPTION_DISABLE tanımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="172cc-360">It also requires that NX_TELNET_SERVER_OPTION_DISABLE not be defined such that the Telnet Server needs a packet pool to transmit Telnet options to Telnet clients.</span></span>

<span data-ttu-id="172cc-361">Bu, uygulamaların paket havuzunu farklı bellekte oluşturmasına izin verir, örneğin, önbellek belleği, Telnet sunucu yığınından daha fazla.</span><span class="sxs-lookup"><span data-stu-id="172cc-361">This permits applications to create the packet pool in different memory e.g. no cache memory, than the Telnet Server stack.</span></span> <span data-ttu-id="172cc-362">Bu işlev, Telnet sunucusu paket havuzunun zaten ayarlanmış olup olmadığını denetlemez.</span><span class="sxs-lookup"><span data-stu-id="172cc-362">Note that if this function does not check if the Telnet Server packet pool is already set.</span></span> <span data-ttu-id="172cc-363">Null olmayan bir Telnet sunucusu paket havuzu işaretçisi üzerinde çağrılırsa, üzerine yazar ve giriş işaretçisi tarafından işaret edilen paket havuzu ile var olan paket havuzunu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="172cc-363">If it is called on a non null Telnet Server packet pool pointer, it will overwrite it and replace the existing packet pool with packet pool pointed to by the input pointer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-364">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-364">Input Parameters</span></span>

- <span data-ttu-id="172cc-365">**server_ptr**: Telnet sunucu denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="172cc-365">**server_ptr**: Pointer to Telnet Server control block</span></span>
- <span data-ttu-id="172cc-366">**packet_pool_ptr**: daha önce oluşturulmuş olan paket havuzuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="172cc-366">**packet_pool_ptr**: Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-367">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-367">Return Values</span></span>

- <span data-ttu-id="172cc-368">**NX_SUCCESS**: (0x00) havuz başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="172cc-368">**NX_SUCCESS**: (0x00) Successfully set pool.</span></span>
- <span data-ttu-id="172cc-369">NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-369">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-370">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-370">Allowed From</span></span>

<span data-ttu-id="172cc-371">Init, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-371">Init, Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-372">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-372">Example</span></span>

```c
status =  nx_packet_pool_create(&telnet_server_packet_pool, 
                                "Telnet Server Packet Pool", 
                                telnet_server_pool_area, 600*10);

/* Set the packet pool as the Telnet Server packet pool.   */
status =  nx_telnet_server_packet_pool_set(&my_server, &telnet_server_packet_pool);

/* If status is NX_SUCCESS the packet pool is set as Telnet Server pool.  */
```
## <a name="nx_telnet_server_start"></a><span data-ttu-id="172cc-373">nx_telnet_server_start</span><span class="sxs-lookup"><span data-stu-id="172cc-373">nx_telnet_server_start</span></span>

<span data-ttu-id="172cc-374">Telnet sunucusu başlatma</span><span class="sxs-lookup"><span data-stu-id="172cc-374">Start a Telnet Server</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-375">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-375">Prototype</span></span>

```c
UINT nx_telnet_server_start(NX_TELNET_SERVER *server_ptr);

```

### <a name="description"></a><span data-ttu-id="172cc-376">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-376">Description</span></span>

<span data-ttu-id="172cc-377">Bu hizmet önceden oluşturulmuş bir Telnet sunucu örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="172cc-377">This service starts a previously created Telnet Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-378">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-378">Input Parameters</span></span>

- <span data-ttu-id="172cc-379">**server_ptr**: Telnet sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-379">**server_ptr**: Pointer to Telnet Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-380">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-380">Return Values</span></span>

- <span data-ttu-id="172cc-381">**NX_SUCCESS**: (0x00) başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="172cc-381">**NX_SUCCESS**: (0x00) Successfully started.</span></span>
- <span data-ttu-id="172cc-382">**NX_TELNET_NO_PACKET_POOL**: (0Xf6) paket havuzu ayarlanmadı</span><span class="sxs-lookup"><span data-stu-id="172cc-382">**NX_TELNET_NO_PACKET_POOL**: (0xF6) No packet pool set</span></span>
- <span data-ttu-id="172cc-383">NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-383">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-384">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-384">Allowed From</span></span>

<span data-ttu-id="172cc-385">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-385">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-386">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-386">Example</span></span>

```c
/* Start the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_start(&my_server);

/* If status is NX_SUCCESS the Server was started.  */
```

## <a name="nx_telnet_server_stop"></a><span data-ttu-id="172cc-387">nx_telnet_server_stop</span><span class="sxs-lookup"><span data-stu-id="172cc-387">nx_telnet_server_stop</span></span>

<span data-ttu-id="172cc-388">Bir Telnet sunucusunu durdur</span><span class="sxs-lookup"><span data-stu-id="172cc-388">Stop a Telnet Server</span></span>

### <a name="prototype"></a><span data-ttu-id="172cc-389">Prototype</span><span class="sxs-lookup"><span data-stu-id="172cc-389">Prototype</span></span>

```c
UINT nx_telnet_server_stop(NX_TELNET_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="172cc-390">Açıklama</span><span class="sxs-lookup"><span data-stu-id="172cc-390">Description</span></span>

<span data-ttu-id="172cc-391">Bu hizmet önceden oluşturulmuş ve başlatılmış bir Telnet sunucu örneğini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="172cc-391">This service stops a previously created and started Telnet Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="172cc-392">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="172cc-392">Input Parameters</span></span>

- <span data-ttu-id="172cc-393">**server_ptr**: Telnet sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-393">**server_ptr**: Pointer to Telnet Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="172cc-394">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="172cc-394">Return Values</span></span>

- <span data-ttu-id="172cc-395">**NX_SUCCESS**: (0x00) başarıyla durduruldu</span><span class="sxs-lookup"><span data-stu-id="172cc-395">**NX_SUCCESS**: (0x00) Successfully stopped</span></span>
- <span data-ttu-id="172cc-396">NX_PTR_ERROR: (0x07) geçersiz sunucu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="172cc-396">NX_PTR_ERROR: (0x07) Invalid Server pointer.</span></span>
- <span data-ttu-id="172cc-397">NX_CALLER_ERROR: (0x11) geçersiz hizmet çağıranı</span><span class="sxs-lookup"><span data-stu-id="172cc-397">NX_CALLER_ERROR: (0x11) Invalid caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="172cc-398">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="172cc-398">Allowed From</span></span>

<span data-ttu-id="172cc-399">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="172cc-399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="172cc-400">Örnek</span><span class="sxs-lookup"><span data-stu-id="172cc-400">Example</span></span>

```c
/* Stop the Telnet Server instance “my_server”.  */
status =  nx_telnet_server_stop(&my_server);

/* If status is NX_SUCCESS the Server was stopped.  */
```