---
title: Bölüm 3-FTP hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX FTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d721d8bd3e08d8cccdc13011807b4c5017c84173
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825979"
---
# <a name="chapter-3---description-of-ftp-services"></a><span data-ttu-id="87ba2-103">Bölüm 3-FTP hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="87ba2-103">Chapter 3 - Description of FTP services</span></span>

<span data-ttu-id="87ba2-104">Bu bölüm, tüm NetX FTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada (burada listelenen IPv4 ve IPv6 eşdeğerlerinin birlikte eşleştirilmiş olması dışında) açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-104">This chapter contains a description of all NetX FTP services (listed below) in alphabetic order (except where IPv4 and IPv6 equivalents of the same service are paired together).</span></span>

> [!NOTE]
> <span data-ttu-id="87ba2-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_ftp_client_connect"></a><span data-ttu-id="87ba2-106">nx_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="87ba2-106">nx_ftp_client_connect</span></span>

<span data-ttu-id="87ba2-107">IPv4 üzerinden FTP sunucusuna bağlanma</span><span class="sxs-lookup"><span data-stu-id="87ba2-107">Connect to an FTP Server over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-108">Prototype</span></span>

```C
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG server_ip, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-109">Description</span></span>

<span data-ttu-id="87ba2-110">Bu hizmet, önceden oluşturulan NetX FTP Istemci örneğini sağlanan IP adresindeki FTP sunucusuna bağlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-110">This service connects the previously created NetX FTP Client instance to the FTP Server at the supplied IP address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-111">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-111">Input Parameters</span></span>

- <span data-ttu-id="87ba2-112">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-112">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-113">**server_ip** FTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-113">**server_ip** IP address of FTP Server.</span></span>
- <span data-ttu-id="87ba2-114">**Kullanıcı adı** Kimlik doğrulaması için istemci Kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-114">**username** Client username for authentication.</span></span>
- <span data-ttu-id="87ba2-115">**parola** Kimlik doğrulaması için istemci parolası.</span><span class="sxs-lookup"><span data-stu-id="87ba2-115">**password** Client password for authentication.</span></span>
- <span data-ttu-id="87ba2-116">**wait_option** Hizmetin FTP Istemci bağlantısı için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-116">**wait_option** Defines how long the service will wait for the FTP Client connection.</span></span> <span data-ttu-id="87ba2-117">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-117">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-118">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-118">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-119">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-119">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-120">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-120">Return Values</span></span>

- <span data-ttu-id="87ba2-121">**NX_SUCCESS** (0x00) FTP bağlantısı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-121">**NX_SUCCESS** (0x00) Successful FTP connection.</span></span>
- <span data-ttu-id="87ba2-122">**NX_TFTP_EXPECTED_22X_CODE** (0xDB), 22x (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-122">**NX_TFTP_EXPECTED_22X_CODE** (0xDB) Did not get a 22X (ok) response</span></span>
- <span data-ttu-id="87ba2-123">**NX_FTP_EXPECTED_23X_CODE** (0xDC), 23x (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-123">**NX_FTP_EXPECTED_23X_CODE** (0xDC) Did not get a 23X (ok) response</span></span>
- <span data-ttu-id="87ba2-124">**NX_FTP_EXPECTED_33X_CODE** (0xDE), bir 33x (Tamam) yanıtı almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-124">**NX_FTP_EXPECTED_33X_CODE** (0xDE) Did not get a 33X (ok) response</span></span>
- <span data-ttu-id="87ba2-125">**NX_FTP_NOT_DISCONNECTED** (0xd4) istemci zaten bağlı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-125">**NX_FTP_NOT_DISCONNECTED** (0xD4) Client is already connected.</span></span>
- <span data-ttu-id="87ba2-126">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-126">NX_PTR_ERROR (0x07) Invalid pointer input.</span></span>
- <span data-ttu-id="87ba2-127">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-127">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="87ba2-128">NX_IP_ADDRESS_ERROR (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-128">NX_IP_ADDRESS_ERROR (0x21) Invalid IP address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-129">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-129">Allowed From</span></span>

<span data-ttu-id="87ba2-130">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-130">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-131">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-131">Example</span></span>

```C
/* Connect the FTP Client instance “my_client” to the FTP Server at

IP address 1.2.3.4. */

status = nx_ftp_client_connect(&my_client, IP_ADDRESS(1,2,3,4), NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
    connected to the FTP Server. */
```

### <a name="see-also"></a><span data-ttu-id="87ba2-132">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="87ba2-132">See Also</span></span>

<span data-ttu-id="87ba2-133">nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nxd_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="87ba2-133">nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nxd_ftp_client_connect</span></span>

## <a name="nxd_ftp_client_connect"></a><span data-ttu-id="87ba2-134">nxd_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="87ba2-134">nxd_ftp_client_connect</span></span>

<span data-ttu-id="87ba2-135">IPv6 desteğiyle FTP sunucusuna bağlanma</span><span class="sxs-lookup"><span data-stu-id="87ba2-135">Connect to an FTP Server with IPv6 support</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-136">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-136">Prototype</span></span>

```C
UINT nxd_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
    NXD_ADDRESS *server_ipduo, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-137">Description</span></span>

<span data-ttu-id="87ba2-138">Bu hizmet, önceden oluşturulmuş NetX Duo FTP Istemci örneğini sağlanan IP adresindeki FTP sunucusuna bağlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-138">This service connects the previously created NetX Duo FTP Client instance to the FTP Server at the supplied IP address.</span></span> <span data-ttu-id="87ba2-139">Hem IPv4 hem de IPv6 ağları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-139">Both IPv4 and IPv6 networks are supported.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-140">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-140">Input Parameters</span></span>

- <span data-ttu-id="87ba2-141">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-141">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-142">**server_ipduo** FTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-142">**server_ipduo** IP address of the FTP Server.</span></span>
- <span data-ttu-id="87ba2-143">**Kullanıcı adı** Kimlik doğrulaması için istemci Kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-143">**username** Client username for authentication.</span></span>
- <span data-ttu-id="87ba2-144">**parola** Kimlik doğrulaması için istemci parolası.</span><span class="sxs-lookup"><span data-stu-id="87ba2-144">**password** Client password for authentication.</span></span>
- <span data-ttu-id="87ba2-145">**wait_option** Hizmetin FTP Istemci bağlantısı için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-145">**wait_option** Defines how long the service will wait for the FTP Client connection.</span></span> <span data-ttu-id="87ba2-146">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-146">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-147">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-147">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-148">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-148">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-149">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-149">Return Values</span></span>

- <span data-ttu-id="87ba2-150">**NX_SUCCESS** (0x00) FTP bağlantısı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-150">**NX_SUCCESS** (0x00) Successful FTP connection.</span></span>
- <span data-ttu-id="87ba2-151">**NX_TFTP_EXPECTED_22X_CODE** (0xDB), 22x (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-151">**NX_TFTP_EXPECTED_22X_CODE** (0xDB) Did not get a 22X (ok) response</span></span>
- <span data-ttu-id="87ba2-152">**NX_FTP_EXPECTED_23X_CODE** (0xDC), 23x (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-152">**NX_FTP_EXPECTED_23X_CODE** (0xDC) Did not get a 23X (ok) response</span></span>
- <span data-ttu-id="87ba2-153">**NX_FTP_EXPECTED_33X_CODE** (0xDE), bir 33x (Tamam) yanıtı almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-153">**NX_FTP_EXPECTED_33X_CODE** (0xDE) Did not get a 33X (ok) response</span></span>
- <span data-ttu-id="87ba2-154">**NX_FTP_NOT_DISCONNECTED** (0xd4) istemci zaten bağlı</span><span class="sxs-lookup"><span data-stu-id="87ba2-154">**NX_FTP_NOT_DISCONNECTED** (0xD4) Client is already connected</span></span>
- <span data-ttu-id="87ba2-155">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-155">NX_PTR_ERROR (0x07) Invalid pointer inout.</span></span>
- <span data-ttu-id="87ba2-156">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-156">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="87ba2-157">NX_IP_ADDRESS_ERROR (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-157">NX_IP_ADDRESS_ERROR (0x21) Invalid IP address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-158">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-158">Allowed From</span></span>

<span data-ttu-id="87ba2-159">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-159">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-160">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-160">Example</span></span>

```C
/* Connect an FTP Client instance to the FTP Server. */

/* Set up an IPv6 address for the server here.
    Note this could also be an IPv4 address as well*/

server_ip_addr.nxd_ip_address.v6[3] = 0x106;
server_ip_addr.nxd_ip_address.v6[2] = 0x0;
server_ip_addr.nxd_ip_address.v6[1] = 0x0000f101;
server_ip_addr.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V6;

status = nxd_ftp_client_connect(&my_client, server_ip_addr, NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
    connected to the FTP Server. */
```

### <a name="see-also"></a><span data-ttu-id="87ba2-161">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="87ba2-161">See Also</span></span>

<span data-ttu-id="87ba2-162">nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nx_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="87ba2-162">nx_ftp_client_create, nx_ftp_client_delete, nx_ftp_client_directory_create, nx_ftp_client_disconnect, nx_ftp_client_connect</span></span>

## <a name="nx_ftp_client_create"></a><span data-ttu-id="87ba2-163">nx_ftp_client_create</span><span class="sxs-lookup"><span data-stu-id="87ba2-163">nx_ftp_client_create</span></span>

<span data-ttu-id="87ba2-164">FTP Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="87ba2-164">Create an FTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-165">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-165">Prototype</span></span>

```C
UINT nx_ftp_client_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *ftp_client_name, NX_IP *ip_ptr, ULONG window_size,
    NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="87ba2-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-166">Description</span></span>

<span data-ttu-id="87ba2-167">Bu hizmet bir FTP Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-167">This service creates an FTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-168">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-168">Input Parameters</span></span>

- <span data-ttu-id="87ba2-169">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-169">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-170">**ftp_client_name** FTP Istemcisinin adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-170">**ftp_client_name** Name of FTP Client.</span></span>
- <span data-ttu-id="87ba2-171">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-171">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="87ba2-172">**window_size** Bu FTP Istemcisinin TCP yuvaları için tanıtılan pencere boyutu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-172">**window_size** Advertised window size for TCP sockets of this FTP Client.</span></span>
- <span data-ttu-id="87ba2-173">**pool_ptr** Bu FTP Istemcisi için varsayılan paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-173">**pool_ptr** Pointer to the default packet pool for this FTP Client.</span></span> <span data-ttu-id="87ba2-174">En düşük paket yükünün, tüm yolu ve dosya ya da dizin adını tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="87ba2-174">Note that the minimum packet payload must be large enough to hold  complete path and the file or directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-175">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-175">Return Values</span></span>

- <span data-ttu-id="87ba2-176">**NX_SUCCESS** (0x00) başarılı FTP istemcisi oluştur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-176">**NX_SUCCESS** (0x00) Successful FTP Client create.</span></span>
- <span data-ttu-id="87ba2-177">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-177">NX_PTR_ERROR (0x07) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-178">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-178">Allowed From</span></span>

<span data-ttu-id="87ba2-179">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-179">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-180">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-180">Example</span></span>

```C
/* Create the FTP Client instance “my_client.” */
status = nx_ftp_client_create(&my_client, "My Client", &client_ip,
    2000, &client_pool);
/* If status is NX_SUCCESS the FTP Client instance was successfully created. */
```

## <a name="nx_ftp_client_delete"></a><span data-ttu-id="87ba2-181">nx_ftp_client_delete</span><span class="sxs-lookup"><span data-stu-id="87ba2-181">nx_ftp_client_delete</span></span>

<span data-ttu-id="87ba2-182">FTP Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="87ba2-182">Delete an FTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-183">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-183">Prototype</span></span>

```C
UINT nx_ftp_client_delete(NX_FTP_CLIENT *ftp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="87ba2-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-184">Description</span></span>

<span data-ttu-id="87ba2-185">Bu hizmet bir FTP Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="87ba2-185">This service deletes an FTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-186">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-186">Input Parameters</span></span>

- <span data-ttu-id="87ba2-187">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-187">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-188">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-188">Return Values</span></span>

- <span data-ttu-id="87ba2-189">**NX_SUCCESS** (0x00) başarılı FTP istemcisi silme.</span><span class="sxs-lookup"><span data-stu-id="87ba2-189">**NX_SUCCESS** (0x00) Successful FTP Client delete.</span></span>
- <span data-ttu-id="87ba2-190">**NX_FTP_NOT_DISCONNECTED** (0xd4) FTP istemcisinin bağlantısı kesildi</span><span class="sxs-lookup"><span data-stu-id="87ba2-190">**NX_FTP_NOT_DISCONNECTED** (0xD4) FTP client not disconnected</span></span>
- <span data-ttu-id="87ba2-191">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-191">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-192">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-192">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-193">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-193">Allowed From</span></span>

<span data-ttu-id="87ba2-194">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-194">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-195">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-195">Example</span></span>

```C
/* Delete the FTP Client instance “my_client.” */

status = nx_ftp_client_delete(&my_client);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
    deleted. */
```

## <a name="nx_ftp_client_directory_create"></a><span data-ttu-id="87ba2-196">nx_ftp_client_directory_create</span><span class="sxs-lookup"><span data-stu-id="87ba2-196">nx_ftp_client_directory_create</span></span>

<span data-ttu-id="87ba2-197">FTP sunucusunda bir dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="87ba2-197">Create a directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-198">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-198">Prototype</span></span>

```C
UINT nx_ftp_client_directory_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-199">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-199">Description</span></span>

<span data-ttu-id="87ba2-200">Bu hizmet, belirtilen FTP sunucusuna bağlı FTP sunucusunda belirtilen dizini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-200">This service creates the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-201">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-201">Input Parameters</span></span>

- <span data-ttu-id="87ba2-202">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-202">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-203">**directory_name** Oluşturulacak dizinin adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-203">**directory_name** Name of directory to create.</span></span>
- <span data-ttu-id="87ba2-204">**wait_option** Hizmetin FTP dizin oluşturma için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-204">**wait_option** Defines how long the service will wait for the FTP directory create.</span></span> <span data-ttu-id="87ba2-205">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-205">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-206">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-206">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-207">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-207">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-208">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-208">Return Values</span></span>

- <span data-ttu-id="87ba2-209">**NX_SUCCESS** (0x00) başarılı FTP dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="87ba2-209">**NX_SUCCESS** (0x00) Successful FTP directory create.</span></span>
- <span data-ttu-id="87ba2-210">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-210">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-211">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-211">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="87ba2-212">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-212">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-213">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-213">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-214">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-214">Allowed From</span></span>

<span data-ttu-id="87ba2-215">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-215">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-216">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-216">Example</span></span>

```C
/* Create the directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_create(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” was successfully created. */
```

## <a name="nx_ftp_client_directory_default_set"></a><span data-ttu-id="87ba2-217">nx_ftp_client_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="87ba2-217">nx_ftp_client_directory_default_set</span></span>

<span data-ttu-id="87ba2-218">FTP sunucusunda varsayılan dizini ayarla</span><span class="sxs-lookup"><span data-stu-id="87ba2-218">Set default directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-219">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-219">Prototype</span></span>

```C
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-220">Description</span></span>

<span data-ttu-id="87ba2-221">Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda varsayılan dizini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-221">This service sets the default directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="87ba2-222">Bu varsayılan dizin yalnızca bu istemcinin bağlantısı için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-222">This default directory applies only to this client’s connection.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-223">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-223">Input Parameters</span></span>

- <span data-ttu-id="87ba2-224">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-224">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-225">**directory_path** Ayarlanacak dizin yolunun adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-225">**directory_path** Name of directory path to set.</span></span>
- <span data-ttu-id="87ba2-226">**wait_option** Hizmetin FTP varsayılan dizin kümesi için ne kadar süre bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-226">**wait_option** Defines how long the service will wait for the FTP default directory set.</span></span> <span data-ttu-id="87ba2-227">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-227">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-228">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-228">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-229">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-229">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-230">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-230">Return Values</span></span>

- <span data-ttu-id="87ba2-231">**NX_SUCCESS** (0x00) başarılı FTP varsayılan kümesi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-231">**NX_SUCCESS** (0x00) Successful FTP default set.</span></span>
- <span data-ttu-id="87ba2-232">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-232">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-233">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-233">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="87ba2-234">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-234">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-235">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-235">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-236">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-236">Allowed From</span></span>

<span data-ttu-id="87ba2-237">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-237">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-238">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-238">Example</span></span>

```C
/* Set the default directory to “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_default_set(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” is the default directory. */
```

## <a name="nx_ftp_client_directory_delete"></a><span data-ttu-id="87ba2-239">nx_ftp_client_directory_delete</span><span class="sxs-lookup"><span data-stu-id="87ba2-239">nx_ftp_client_directory_delete</span></span>

<span data-ttu-id="87ba2-240">FTP sunucusundaki dizini Sil</span><span class="sxs-lookup"><span data-stu-id="87ba2-240">Delete directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-241">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-241">Prototype</span></span>

```C
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-242">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-242">Description</span></span>

<span data-ttu-id="87ba2-243">Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda belirtilen dizini siler.</span><span class="sxs-lookup"><span data-stu-id="87ba2-243">This service deletes the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-244">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-244">Input Parameters</span></span>

- <span data-ttu-id="87ba2-245">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-245">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-246">**directory_name** Silinecek dizinin adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-246">**directory_name** Name of directory to delete.</span></span>
- <span data-ttu-id="87ba2-247">**wait_option** Hizmetin FTP dizin silme işleminin ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-247">**wait_option** Defines how long the service will wait for the FTP directory delete.</span></span> <span data-ttu-id="87ba2-248">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-248">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-249">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-249">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-250">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-250">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-251">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-251">Return Values</span></span>

- <span data-ttu-id="87ba2-252">**NX_SUCCESS** (0x00) başarılı FTP dizin silme.</span><span class="sxs-lookup"><span data-stu-id="87ba2-252">**NX_SUCCESS** (0x00) Successful FTP directory delete.</span></span>
- <span data-ttu-id="87ba2-253">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-253">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-254">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-254">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="87ba2-255">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-255">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-256">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-256">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-257">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-257">Allowed From</span></span>

<span data-ttu-id="87ba2-258">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-258">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-259">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-259">Example</span></span>

```C
/* Delete directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_delete(&my_client, “my_dir”, 200);

/* If status is NX_SUCCESS the directory “my_dir” is deleted. */
```

## <a name="nx_ftp_client_directory_listing_get"></a><span data-ttu-id="87ba2-260">nx_ftp_client_directory_listing_get</span><span class="sxs-lookup"><span data-stu-id="87ba2-260">nx_ftp_client_directory_listing_get</span></span>

<span data-ttu-id="87ba2-261">FTP sunucusundan dizin listesini al</span><span class="sxs-lookup"><span data-stu-id="87ba2-261">Get directory listing from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-262">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-262">Prototype</span></span>

```C
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *directory_name, NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-263">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-263">Description</span></span>

<span data-ttu-id="87ba2-264">Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda belirtilen dizinin içeriğini alır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-264">This service gets the contents of the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="87ba2-265">Sağlanan paket işaretçisi bir veya daha fazla dizin girişi içerecektir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-265">The supplied packet pointer will contain one or more directory entries.</span></span> <span data-ttu-id="87ba2-266">Her giriş bir bileşim ile ayrılır \<cr/lf\> .</span><span class="sxs-lookup"><span data-stu-id="87ba2-266">Each entry is separated by a \<cr/lf\> combination.</span></span> <span data-ttu-id="87ba2-267">***Nx_ftp_client_directory_listing_continue*** , Dizin Al işlemini tamamlayacak şekilde çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-267">The ***nx_ftp_client_directory_listing_continue*** should be called to complete the directory get operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-268">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-268">Input Parameters</span></span>

- <span data-ttu-id="87ba2-269">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-269">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-270">**directory_name** İçeriğin alınacağı dizinin adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-270">**directory_name** Name of directory to get contents of.</span></span>
- <span data-ttu-id="87ba2-271">**packet_ptr** Hedef paket işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-271">**packet_ptr** Pointer to destination packet pointer.</span></span> <span data-ttu-id="87ba2-272">Başarılı olursa, paket yükü bir veya daha fazla dizin girişi içerir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-272">If successful, the packet payload will contain one or more directory entries.</span></span>
- <span data-ttu-id="87ba2-273">**wait_option** Hizmetin FTP dizin listesi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-273">**wait_option** Defines how long the service will wait for the FTP directory listing.</span></span> <span data-ttu-id="87ba2-274">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-274">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-275">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-275">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-276">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-276">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-277">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-277">Return Values</span></span>

- <span data-ttu-id="87ba2-278">**NX_SUCCESS** (0x00) FTP Dizin listeleme başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-278">**NX_SUCCESS** (0x00) Successful FTP directory listing.</span></span>
- <span data-ttu-id="87ba2-279">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-279">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-280">**NX_NOT_ENABLED** (0X14) hizmeti (IPv6) etkin değil</span><span class="sxs-lookup"><span data-stu-id="87ba2-280">**NX_NOT_ENABLED** (0x14) Service (IPv6) not enabled</span></span>
- <span data-ttu-id="87ba2-281">**NX_FTP_EXPECTED_1XX_CODE** (0xD9), 1xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-281">**NX_FTP_EXPECTED_1XX_CODE** (0xD9) Did not get a 1XX (ok) response</span></span>
- <span data-ttu-id="87ba2-282">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-282">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="87ba2-283">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-283">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-284">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-284">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-285">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-285">Allowed From</span></span>

<span data-ttu-id="87ba2-286">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-286">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-287">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-287">Example</span></span>

```C
/* Get the contents of directory “my_dir” on the FTP Server connected to
    the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_listing_get(&my_client, “my_dir”, &my_packet,
    200);

/* If status is NX_SUCCESS, one or more entries of the directory “my_dir”
    can be found in “my_packet”. */
```

## <a name="nx_ftp_client_directory_listing_continue"></a><span data-ttu-id="87ba2-288">nx_ftp_client_directory_listing_continue</span><span class="sxs-lookup"><span data-stu-id="87ba2-288">nx_ftp_client_directory_listing_continue</span></span>

<span data-ttu-id="87ba2-289">FTP sunucusundan dizin listesine devam et</span><span class="sxs-lookup"><span data-stu-id="87ba2-289">Continue directory listing from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-290">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-290">Prototype</span></span>

```C
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-291">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-291">Description</span></span>

<span data-ttu-id="87ba2-292">Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda belirtilen dizinin içeriğini almaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="87ba2-292">This service continues getting the contents of the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="87ba2-293">***Nx_ftp_client_directory_listing_get*** çağrısı hemen öncesinde gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-293">It should have been immediately preceded by a call to ***nx_ftp_client_directory_listing_get***.</span></span> <span data-ttu-id="87ba2-294">Başarılı olursa, sağlanan paket işaretçisi bir veya daha fazla dizin girişi içerir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-294">If successful, the supplied packet pointer will contain one or more directory entries.</span></span> <span data-ttu-id="87ba2-295">Bu yordam, bir NX_FTP_END_OF_LISTING durumu alınana kadar çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-295">This routine should be called until an NX_FTP_END_OF_LISTING status is received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-296">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-296">Input Parameters</span></span>

- <span data-ttu-id="87ba2-297">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-297">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-298">**packet_ptr** Hedef paket işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-298">**packet_ptr** Pointer to destination packet pointer.</span></span> <span data-ttu-id="87ba2-299">Başarılı olursa, paket yükü bir <CR/LF> ile ayrılmış bir veya daha fazla dizin girişi içerecektir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-299">If successful, the packet payload will contain one or more directory entries, separated by a <cr/lf>.</span></span>
- <span data-ttu-id="87ba2-300">**wait_option** Hizmetin FTP dizin listesi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-300">**wait_option** Defines how long the service will wait for the FTP directory listing.</span></span> <span data-ttu-id="87ba2-301">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-301">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-302">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-302">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-303">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-303">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-304">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-304">Return Values</span></span>

- <span data-ttu-id="87ba2-305">**NX_SUCCESS** (0x00) FTP Dizin listeleme başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-305">**NX_SUCCESS** (0x00) Successful FTP directory listing.</span></span>
- <span data-ttu-id="87ba2-306">**NX_FTP_END_OF_LISTING** (0xd8) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="87ba2-306">**NX_FTP_END_OF_LISTING** (0xD8) No more entries in this directory.</span></span>
- <span data-ttu-id="87ba2-307">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-307">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-308">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-308">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="87ba2-309">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-309">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-310">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-310">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-311">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-311">Allowed From</span></span>

<span data-ttu-id="87ba2-312">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-312">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-313">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-313">Example</span></span>

```C
/* Continue getting the contents of directory “my_dir” on the FTP Server
    connected to the FTP Client instance “my_client.” */

status = nx_ftp_client_directory_listing_continue(&my_client, &my_packet,
    200);

/* If status is NX_SUCCESS, one or more entries of the directory “my_dir”
    can be found in “my_packet”. */
```

## <a name="nx_ftp_client_disconnect"></a><span data-ttu-id="87ba2-314">nx_ftp_client_disconnect</span><span class="sxs-lookup"><span data-stu-id="87ba2-314">nx_ftp_client_disconnect</span></span>

<span data-ttu-id="87ba2-315">FTP sunucusu bağlantısını kes</span><span class="sxs-lookup"><span data-stu-id="87ba2-315">Disconnect from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-316">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-316">Prototype</span></span>

```C
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-317">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-317">Description</span></span>

<span data-ttu-id="87ba2-318">Bu hizmet, belirtilen FTP Istemcisiyle önceden oluşturulmuş bir FTP sunucusu bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="87ba2-318">This service disconnects a previously established FTP Server connection with the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-319">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-319">Input Parameters</span></span>

- <span data-ttu-id="87ba2-320">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-320">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-321">**wait_option** Hizmetin FTP Istemcisinin bağlantısını kesmeyi bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-321">**wait_option** Defines how long the service will wait for the FTP Client disconnect.</span></span> <span data-ttu-id="87ba2-322">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-322">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-323">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-323">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-324">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-324">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-325">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-325">Return Values</span></span>

- <span data-ttu-id="87ba2-326">**NX_SUCCESS** (0x00) FTP bağlantısı başarıyla açıldı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-326">**NX_SUCCESS** (0x00) Successful FTP disconnect.</span></span>
- <span data-ttu-id="87ba2-327">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-327">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-328">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-328">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="87ba2-329">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-329">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-330">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-330">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-331">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-331">Allowed From</span></span>

<span data-ttu-id="87ba2-332">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-332">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-333">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-333">Example</span></span>

```C
/* Disconnect “my_client” from the FTP Server. */

status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, “my_client” has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a><span data-ttu-id="87ba2-334">nx_ftp_client_file_close</span><span class="sxs-lookup"><span data-stu-id="87ba2-334">nx_ftp_client_file_close</span></span>

<span data-ttu-id="87ba2-335">Istemci dosyasını kapat</span><span class="sxs-lookup"><span data-stu-id="87ba2-335">Close Client file</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-336">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-336">Prototype</span></span>

```C
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-337">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-337">Description</span></span>

<span data-ttu-id="87ba2-338">Bu hizmet, FTP sunucusunda daha önce açılmış bir dosyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-338">This service closes a previously opened file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-339">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-339">Input Parameters</span></span>

- <span data-ttu-id="87ba2-340">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-340">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-341">**wait_option** Hizmetin FTP Istemci dosyası kapanması için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-341">**wait_option** Defines how long the service will wait for the FTP Client file close.</span></span> <span data-ttu-id="87ba2-342">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-342">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-343">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-343">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-344">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-344">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-345">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-345">Return Values</span></span>

- <span data-ttu-id="87ba2-346">**NX_SUCCESS** (0x00) başarılı FTP dosyası kapatma.</span><span class="sxs-lookup"><span data-stu-id="87ba2-346">**NX_SUCCESS** (0x00) Successful FTP file close.</span></span>
- <span data-ttu-id="87ba2-347">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-347">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-348">**NX_FTP_NOT_OPEN (0xD5)** Dosya açık değil; kapatılamıyor</span><span class="sxs-lookup"><span data-stu-id="87ba2-348">**NX_FTP_NOT_OPEN (0xD5)** File not open; cannot close it</span></span>
- <span data-ttu-id="87ba2-349">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-349">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="87ba2-350">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-350">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-351">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-351">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-352">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-352">Allowed From</span></span>

<span data-ttu-id="87ba2-353">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-353">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-354">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-354">Example</span></span>

```C
/* Close previously opened file of client “my_client” on the FTP Server. */

status = nx_ftp_client_file_close(&my_client, 200);

/* If status is NX_SUCCESS, the file opened previously in the “my_client” FTP
    connection has been closed. */
```

## <a name="nx_ftp_client_file_delete"></a><span data-ttu-id="87ba2-355">nx_ftp_client_file_delete</span><span class="sxs-lookup"><span data-stu-id="87ba2-355">nx_ftp_client_file_delete</span></span>

<span data-ttu-id="87ba2-356">FTP sunucusundaki dosyayı Sil</span><span class="sxs-lookup"><span data-stu-id="87ba2-356">Delete file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-357">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-357">Prototype</span></span>

```C
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-358">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-358">Description</span></span>

<span data-ttu-id="87ba2-359">Bu hizmet, FTP sunucusunda belirtilen dosyayı siler.</span><span class="sxs-lookup"><span data-stu-id="87ba2-359">This service deletes the specified file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-360">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-360">Input Parameters</span></span>

- <span data-ttu-id="87ba2-361">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-361">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-362">**file_name** Silinecek dosyanın adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-362">**file_name** Name of file to delete.</span></span>
- <span data-ttu-id="87ba2-363">**wait_option** Hizmetin FTP Istemci dosyası silme işleminin ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-363">**wait_option** Defines how long the service will wait for the FTP Client file delete.</span></span> <span data-ttu-id="87ba2-364">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-364">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-365">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-365">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-366">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-366">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-367">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-367">Return Values</span></span>

- <span data-ttu-id="87ba2-368">**NX_SUCCESS** (0x00) FTP dosyası başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-368">**NX_SUCCESS** (0x00) Successful FTP file delete.</span></span>
- <span data-ttu-id="87ba2-369">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-369">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-370">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-370">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="87ba2-371">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-371">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-372">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-372">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-373">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-373">Allowed From</span></span>

<span data-ttu-id="87ba2-374">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-374">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-375">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-375">Example</span></span>

```C
/* Delete the file “my_file.txt” on the FTP Server using the previously
    connected client “my_client.” */

status = nx_ftp_client_file_delete(&my_client, “my_file.txt”, 200);

/* If status is NX_SUCCESS, the file “my_file.txt” on the FTP Server is
    deleted. */
```

## <a name="nx_ftp_client_file_open"></a><span data-ttu-id="87ba2-376">nx_ftp_client_file_open</span><span class="sxs-lookup"><span data-stu-id="87ba2-376">nx_ftp_client_file_open</span></span>

<span data-ttu-id="87ba2-377">Dosyayı FTP sunucusunda açar</span><span class="sxs-lookup"><span data-stu-id="87ba2-377">Opens file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-378">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-378">Prototype</span></span>

```C
UINT nx_ftp_client_file_open(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *file_name, UINT open_type, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-379">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-379">Description</span></span>

<span data-ttu-id="87ba2-380">Bu hizmet, belirtilen Istemci örneğine daha önce bağlı FTP sunucusunda belirtilen dosyayı (okuma veya yazma için) açar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-380">This service opens the specified file – for reading or writing – on the FTP Server previously connected to the specified Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-381">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-381">Input Parameters</span></span>

- <span data-ttu-id="87ba2-382">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-382">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-383">**file_name** Açılacak dosyanın adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-383">**file_name** Name of file to open.</span></span>
- <span data-ttu-id="87ba2-384">**open_type** Ya **NX_FTP_OPEN_FOR_READ** ya da **NX_FTP_OPEN_FOR_WRITE**.</span><span class="sxs-lookup"><span data-stu-id="87ba2-384">**open_type** Either **NX_FTP_OPEN_FOR_READ** or **NX_FTP_OPEN_FOR_WRITE**.</span></span>
- <span data-ttu-id="87ba2-385">**wait_option** Hizmetin FTP Istemci dosyası açma süresini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-385">**wait_option** Defines how long the service will wait for the FTP Client file open.</span></span> <span data-ttu-id="87ba2-386">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-386">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-387">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-387">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-388">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-388">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-389">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-389">Return Values</span></span>

- <span data-ttu-id="87ba2-390">**NX_SUCCESS** (0x00) FTP dosyası başarıyla açıldı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-390">**NX_SUCCESS** (0x00) Successful FTP file open.</span></span>
- <span data-ttu-id="87ba2-391">**NX_OPTION_ERROR** (0X0a) geçersiz açık tür.</span><span class="sxs-lookup"><span data-stu-id="87ba2-391">**NX_OPTION_ERROR** (0x0A) Invalid open type.</span></span>
- <span data-ttu-id="87ba2-392">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-392">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-393">**NX_FTP_NOT_CLOSED** (0xd6) FTP istemcisi zaten açık.</span><span class="sxs-lookup"><span data-stu-id="87ba2-393">**NX_FTP_NOT_CLOSED** (0xD6) FTP Client is already opened.</span></span>
- <span data-ttu-id="87ba2-394">**NX_NO_FREE_PORTS** (0x45) atamak IÇIN kullanılabilir TCP bağlantı noktası yok</span><span class="sxs-lookup"><span data-stu-id="87ba2-394">**NX_NO_FREE_PORTS** (0x45) No TCP ports available to assign</span></span>
- <span data-ttu-id="87ba2-395">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-395">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-396">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-396">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-397">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-397">Allowed From</span></span>

<span data-ttu-id="87ba2-398">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-398">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-399">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-399">Example</span></span>

```C
/* Open the file “my_file.txt” for reading on the FTP Server using the previously
    connected client “my_client.” */

status = nx_ftp_client_file_open(&my_client, “my_file.txt”, NX_FTP_OPEN_FOR_READ,
    200);

/* If status is NX_SUCCESS, the file “my_file.txt” on the FTP Server is
    open for reading. */
```

## <a name="nx_ftp_client_file_read"></a><span data-ttu-id="87ba2-400">nx_ftp_client_file_read</span><span class="sxs-lookup"><span data-stu-id="87ba2-400">nx_ftp_client_file_read</span></span>

<span data-ttu-id="87ba2-401">Dosyadan oku</span><span class="sxs-lookup"><span data-stu-id="87ba2-401">Read from file</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-402">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-402">Prototype</span></span>

```C
UINT nx_ftp_client_file_read(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-403">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-403">Description</span></span>

<span data-ttu-id="87ba2-404">Bu hizmet, daha önce açılmış bir dosyanın paketini okur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-404">This service reads a packet from a previously opened file.</span></span> <span data-ttu-id="87ba2-405">NX_FTP_END_OF_FILE bir durum alınana kadar kaldı çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-405">It should be called repetitively until a status of NX_FTP_END_OF_FILE is received.</span></span>

<span data-ttu-id="87ba2-406">Çağıranın bu hizmet için bir paket ayırmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="87ba2-406">Note that the caller does not allocate a packet for this service.</span></span>  <span data-ttu-id="87ba2-407">Yalnızca bir paket işaretçisine işaretçi sağlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-407">It need only supply a pointer to a packet pointer.</span></span> <span data-ttu-id="87ba2-408">Bu hizmet, bu paket işaretçisini yuva alma sırasından alınan bir pakete işaret edecek şekilde güncelleştirecek.</span><span class="sxs-lookup"><span data-stu-id="87ba2-408">This service will update that packet pointer to point to a packet retrieved from the socket receive queue.</span></span>  <span data-ttu-id="87ba2-409">Başarılı bir durum döndürülürse, bu, kullanılabilir bir paket olduğu anlamına gelir ve bu, paketin yaptığı sırada paketi serbest bırakma sorumluluğudur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-409">If a successful status is returned, that means there was a packet available, and it is the caller’s responsibility to release the packet when it is done with it.</span></span>

<span data-ttu-id="87ba2-410">Sıfır olmayan bir durum (bir hata durumu veya NX_FTP_END_OF_FILE) döndürülürse, çağıran paketi serbest bırakmaz.</span><span class="sxs-lookup"><span data-stu-id="87ba2-410">If a non-zero status (either an error status or NX_FTP_END_OF_FILE) is returned, the caller does not release the packet.</span></span> <span data-ttu-id="87ba2-411">Aksi takdirde, paket işaretçisi NULL olduğunda bir hata oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-411">Otherwise, an error is generated when if the packet pointer is NULL.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-412">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-412">Input Parameters</span></span>

- <span data-ttu-id="87ba2-413">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-413">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-414">**packet_ptr** Veri paketi işaretçisinin depolanacağı hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-414">**packet_ptr** Pointer to destination for the data packet pointer to be stored.</span></span> <span data-ttu-id="87ba2-415">Başarılı olursa, paketin bir kısmı veya hepsi dosyanın içerir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-415">If successful, the packet some or all the contains of the file.</span></span>
- <span data-ttu-id="87ba2-416">**wait_option** Hizmetin FTP Istemci dosyası okuması için ne kadar süre bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-416">**wait_option** Defines how long the service will wait for the FTP Client file read.</span></span> <span data-ttu-id="87ba2-417">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-417">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-418">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-418">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-419">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-419">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-420">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-420">Return Values</span></span>

- <span data-ttu-id="87ba2-421">**NX_SUCCESS** (0x00) başarılı FTP dosyası okundu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-421">**NX_SUCCESS** (0x00) Successful FTP file read.</span></span>
- <span data-ttu-id="87ba2-422">**NX_FTP_NOT_OPEN** (0xd5) FTP istemcisi açık değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-422">**NX_FTP_NOT_OPEN** (0xD5) FTP Client is not opened.</span></span>
- <span data-ttu-id="87ba2-423">**NX_FTP_END_OF_FILE** (0xd7) dosya koşulunun sonu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-423">**NX_FTP_END_OF_FILE** (0xD7) End of file condition.</span></span>
- <span data-ttu-id="87ba2-424">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-424">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-425">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-425">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-426">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-426">Allowed From</span></span>

<span data-ttu-id="87ba2-427">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-427">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-428">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-428">Example</span></span>

```C
NX_PACKET   *my_packet;

/* Read a packet of data from the file “my_file.txt” that was previously opened
    from the client “my_client.” */

status = nx_ftp_client_file_read(&my_client, &my_packet, 200);

/* Check status.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else
{
    /* Release packet when done with it. */
    nx_packet_release(my_packet);
}

/* If status is NX_SUCCESS, the packet pointer, “my_packet” points to the packet
    that contains the next bytes from the file. If the file is completely
    downloaded, an NX_FTP_END_OF_FILE status is returned (no packet retrieved). */
```

## <a name="nx_ftp_client_file_rename"></a><span data-ttu-id="87ba2-429">nx_ftp_client_file_rename</span><span class="sxs-lookup"><span data-stu-id="87ba2-429">nx_ftp_client_file_rename</span></span>

<span data-ttu-id="87ba2-430">FTP sunucusundaki dosyayı yeniden adlandır</span><span class="sxs-lookup"><span data-stu-id="87ba2-430">Rename file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-431">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-431">Prototype</span></span>

```C
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
    CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-432">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-432">Description</span></span>

<span data-ttu-id="87ba2-433">Bu hizmet, FTP sunucusundaki bir dosyayı yeniden adlandırır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-433">This service renames a file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-434">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-434">Input Parameters</span></span>

- <span data-ttu-id="87ba2-435">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-435">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-436">**dosya adı** Dosyanın geçerli adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-436">**filename** Current name of file.</span></span>
- <span data-ttu-id="87ba2-437">**new_filename** Dosya için yeni ad.</span><span class="sxs-lookup"><span data-stu-id="87ba2-437">**new_filename** New name for file.</span></span>
- <span data-ttu-id="87ba2-438">**wait_option** Hizmetin FTP Istemci dosyası yeniden adlandırma için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-438">**wait_option** Defines how long the service will wait for the FTP Client file rename.</span></span> <span data-ttu-id="87ba2-439">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-439">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-440">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-440">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-441">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-441">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-442">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-442">Return Values</span></span>

- <span data-ttu-id="87ba2-443">**NX_SUCCESS** (0x00) başarılı FTP dosyası yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="87ba2-443">**NX_SUCCESS** (0x00) Successful FTP file rename.</span></span>
- <span data-ttu-id="87ba2-444">**NX_FTP_NOT_CONNECTED** (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-444">**NX_FTP_NOT_CONNECTED** (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="87ba2-445">**NX_FTP_EXPECTED_3XX_CODE** (0xDD), 3xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-445">**NX_FTP_EXPECTED_3XX_CODE** (0XDD) Did not receive 3XX (ok) response</span></span>
- <span data-ttu-id="87ba2-446">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="87ba2-446">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="87ba2-447">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-447">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-448">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-448">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-449">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-449">Allowed From</span></span>

<span data-ttu-id="87ba2-450">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-450">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-451">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-451">Example</span></span>

```C
/* Rename file “my_file.txt” to “new_file.txt” on the previously connected
    Client instance “my_client.” */

status = nx_ftp_client_file_rename(&my_client, “my_file.txt”, “new_file.txt”,
    200);

/* If status is NX_SUCCESS, the file has been renamed. */
```

## <a name="nx_ftp_client_file_write"></a><span data-ttu-id="87ba2-452">nx_ftp_client_file_write</span><span class="sxs-lookup"><span data-stu-id="87ba2-452">nx_ftp_client_file_write</span></span>

<span data-ttu-id="87ba2-453">Dosyaya yaz</span><span class="sxs-lookup"><span data-stu-id="87ba2-453">Write to file</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-454">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-454">Prototype</span></span>

```C
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="87ba2-455">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-455">Description</span></span>

<span data-ttu-id="87ba2-456">Bu hizmet, FTP sunucusundaki daha önce açılan dosyaya bir veri paketi yazar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-456">This service writes a packet of data to the previously opened file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-457">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-457">Input Parameters</span></span>

- <span data-ttu-id="87ba2-458">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-458">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-459">**packet_ptr** Yazılacak verileri içeren paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-459">**packet_ptr** Packet pointer containing data to write.</span></span>
- <span data-ttu-id="87ba2-460">**wait_option** Hizmetin FTP Istemci dosyası yazma süresini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-460">**wait_option** Defines how long the service will wait for the FTP Client file write.</span></span> <span data-ttu-id="87ba2-461">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="87ba2-461">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="87ba2-462">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal bir değer (1-0XFFFFFFFE) SEÇILIRSE, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-462">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>
  - <span data-ttu-id="87ba2-463">**TX_WAIT_FOREVER** (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-463">**TX_WAIT_FOREVER** (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-464">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-464">Return Values</span></span>

- <span data-ttu-id="87ba2-465">**NX_SUCCESS** (0x00) başarılı FTP dosyası yazma.</span><span class="sxs-lookup"><span data-stu-id="87ba2-465">**NX_SUCCESS** (0x00) Successful FTP file write.</span></span>
- <span data-ttu-id="87ba2-466">**NX_FTP_NOT_OPEN** (0xd5) FTP istemcisi açık değil.</span><span class="sxs-lookup"><span data-stu-id="87ba2-466">**NX_FTP_NOT_OPEN** (0xD5) FTP Client is not opened.</span></span>
- <span data-ttu-id="87ba2-467">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-467">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-468">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-468">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-469">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-469">Allowed From</span></span>

<span data-ttu-id="87ba2-470">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-470">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-471">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-471">Example</span></span>

```C
/* Write the data contained in “my_packet” to the previously opened file
    “my_file.txt”. */

status = nx_ftp_client_file_write(&my_client, my_packet, 200);

/* If status is NX_SUCCESS, the file has been written to. */
```

## <a name="nx_ftp_client_passive_mode_set"></a><span data-ttu-id="87ba2-472">nx_ftp_client_passive_mode_set</span><span class="sxs-lookup"><span data-stu-id="87ba2-472">nx_ftp_client_passive_mode_set</span></span>

<span data-ttu-id="87ba2-473">Pasif aktarım modunu etkinleştirme veya devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="87ba2-473">Enable or disable passive transfer mode</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-474">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-474">Prototype</span></span>

```C
UINT nx_ftp_client_passive_mode_set(NX_FTP_CLIENT *ftp_client_ptr,
    UINT passive_mode_enabled);
```

### <a name="description"></a><span data-ttu-id="87ba2-475">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-475">Description</span></span>

<span data-ttu-id="87ba2-476">Bu hizmet, passive_mode_enabled girişi daha önceden oluşturulmuş bir FTP Istemci örneğinde NX_TRUE olarak ayarlandıysa (RETR, STOR) veya bir dizin listesini indirme (NLST), Aktarım modunda yapıldıktan sonra, pasif aktarım modunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="87ba2-476">This service enables passive transfer mode if the passive_mode_enabled input is set to NX_TRUE on a previously created FTP Client instance such that subsequent calls to read or write files (RETR, STOR) or download a directory listing (NLST) are done in transfer mode.</span></span> <span data-ttu-id="87ba2-477">Pasif mod aktarımını devre dışı bırakmak ve etkin aktarım modunun varsayılan davranışına geri dönmek için, bu işlevi passive_mode_enabled girişi NX_FALSE kümesiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="87ba2-477">To disable passive mode transfer and return to the default behavior of active transfer mode, call this function with the passive_mode_enabled input set to NX_FALSE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-478">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-478">Input Parameters</span></span>

- <span data-ttu-id="87ba2-479">**ftp_client_ptr** FTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-479">**ftp_client_ptr** Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="87ba2-480">**passive_mode_enabled** NX_TRUE olarak ayarlanırsa, Pasif mod etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-480">**passive_mode_enabled** If set to NX_TRUE, passive mode is enabled.</span></span><br /><span data-ttu-id="87ba2-481">NX_FALSE olarak ayarlanırsa, Pasif mod devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-481">If set to NX_FALSE, passive mode is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-482">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-482">Return Values</span></span>

- <span data-ttu-id="87ba2-483">**NX_SUCCESS** (0x00) başarılı Pasif mod kümesi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-483">**NX_SUCCESS** (0x00) Successful passive mode set.</span></span>
- <span data-ttu-id="87ba2-484">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-484">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-485">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="87ba2-485">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-486">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-486">Allowed From</span></span>

<span data-ttu-id="87ba2-487">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-487">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-488">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-488">Example</span></span>

```C
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a><span data-ttu-id="87ba2-489">nx_ftp_server_create</span><span class="sxs-lookup"><span data-stu-id="87ba2-489">nx_ftp_server_create</span></span>

<span data-ttu-id="87ba2-490">FTP sunucusu oluştur</span><span class="sxs-lookup"><span data-stu-id="87ba2-490">Create FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-491">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-491">Prototype</span></span>

```C
UINT nx_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
    CHAR *ftp_server_name, NX_IP *ip_ptr,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*ftp_login)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        ULONG client_ip_address,
        UINT client_port, CHAR *name, CHAR *password,
        CHAR *extra_info),
    UINT (*ftp_logout)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        ULONG client_ip_address, UINT client_port,
         CHAR *name, CHAR *password, CHAR *extra_info));
```

### <a name="description"></a><span data-ttu-id="87ba2-492">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-492">Description</span></span>

<span data-ttu-id="87ba2-493">Bu hizmet, belirtilen ve daha önce oluşturulmuş NetX IP örneğinde bir FTP sunucu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-493">This service creates an FTP Server instance on the specified and previously created NetX IP instance.</span></span> <span data-ttu-id="87ba2-494">FTP sunucusunun, işleme başlaması için bir ***nx_ftp_server_start*** çağrısıyla başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-494">Note the FTP Server needs to be started with a call to ***nx_ftp_server_start*** for it to begin operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-495">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-495">Input Parameters</span></span>

- <span data-ttu-id="87ba2-496">**ftp_server_ptr** FTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-496">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>
- <span data-ttu-id="87ba2-497">**ftp_server_name** FTP sunucusunun adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-497">**ftp_server_name** Name of FTP Server.</span></span>
- <span data-ttu-id="87ba2-498">**ip_ptr** İlişkili NetX IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-498">**ip_ptr** Pointer to associated NetX IP instance.</span></span> <span data-ttu-id="87ba2-499">Bir IP örneği için yalnızca bir FTP sunucusu olabileceğini göz önünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87ba2-499">Note there can only be one FTP Server for an IP instance.</span></span>
- <span data-ttu-id="87ba2-500">**media_ptr** İlişkili FileX medya örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-500">**media_ptr** Pointer to associated FileX media instance.</span></span>
- <span data-ttu-id="87ba2-501">**stack_ptr** İç FTP sunucusu iş parçacığının yığın alanı için bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-501">**stack_ptr** Pointer to memory for the internal FTP Server thread’s stack area.</span></span>
- <span data-ttu-id="87ba2-502">**stack_size** *Stack_ptr* tarafından belirtilen yığın alanının boyutu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-502">**stack_size** Size of stack area specified by *stack_ptr*.</span></span>
- <span data-ttu-id="87ba2-503">**pool_ptr** Varsayılan NetX paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-503">**pool_ptr** Pointer to default NetX packet pool.</span></span> <span data-ttu-id="87ba2-504">Notdaki paketlerin yük boyutu, en büyük dosya adına/yola uyum sağlayacak kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-504">Note the payload size of packets in the pool must be large enough to accommodate the largest filename/path.</span></span>
- <span data-ttu-id="87ba2-505">**ftp_login** Uygulamanın oturum açma işlevine yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-505">**ftp_login** Function pointer to application’s login function.</span></span> <span data-ttu-id="87ba2-506">Bu işleve, bir bağlantı isteyen Istemciden Kullanıcı adı ve parola ve ULONG veri türündeki Istemci adresi verilir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-506">This function is supplied the username and password from the Client requesting a connection, and the Client address in the ULONG data type.</span></span> <span data-ttu-id="87ba2-507">Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-507">If this is valid, the application’s login function should return NX_SUCCESS.</span></span>
- <span data-ttu-id="87ba2-508">**ftp_logout** Uygulamanın oturum kapatma işlevine yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-508">**ftp_logout** Function pointer to application’s logout function.</span></span> <span data-ttu-id="87ba2-509">Bu işleve, bir bağlantı kesilmesi isteyen Istemciden Kullanıcı adı ve parola ve ULONG veri türündeki Istemci adresi verilir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-509">This function is supplied the username and password from the Client requesting a disconnection, and the Client address in the ULONG data type.</span></span> <span data-ttu-id="87ba2-510">Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-510">If this is valid, the application’s login function should return NX_SUCCESS.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-511">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-511">Return Values</span></span>

- <span data-ttu-id="87ba2-512">**NX_SUCCESS** (0x00) başarılı FTP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="87ba2-512">**NX_SUCCESS** (0x00) Successful FTP Server create.</span></span>
- <span data-ttu-id="87ba2-513">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-513">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-514">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-514">Allowed From</span></span>

<span data-ttu-id="87ba2-515">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-515">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-516">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-516">Example</span></span>

```C
/* Create the FTP Server “my_server” on the IP instance “ip_0” using the
    “ram_disk” media. */

status = nx_ftp_server_create(&my_server, “My Server Name”, &ip_0, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_login, my_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nxd_ftp_server_create"></a><span data-ttu-id="87ba2-517">nxd_ftp_server_create</span><span class="sxs-lookup"><span data-stu-id="87ba2-517">nxd_ftp_server_create</span></span>

<span data-ttu-id="87ba2-518">IPv4 ve IPv6 desteğiyle FTP sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="87ba2-518">Create FTP Server with IPv4 and IPv6 support</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-519">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-519">Prototype</span></span>

```C
UINT nxd_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
    CHAR *ftp_server_name, NX_IP *ip_ptr,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*ftp_login_duo)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        NXD_ADDRESS *client_ip_address, UINT client_port, CHAR *name,
        CHAR *password, CHAR *extra_info),
    UINT (*ftp_logout_duo)(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
        NXD_ADDRESS *client_ip_address, UINT client_port, CHAR *name,
        CHAR *password, CHAR *extra_info));
```

### <a name="description"></a><span data-ttu-id="87ba2-520">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-520">Description</span></span>

<span data-ttu-id="87ba2-521">Bu hizmet, belirtilen ve daha önce oluşturulmuş NetX IP örneğinde bir FTP sunucu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87ba2-521">This service creates an FTP Server instance on the specified and previously created NetX IP instance.</span></span> <span data-ttu-id="87ba2-522">Sunucu oluşturulduktan sonra işlemin başlaması için FTP sunucusunun hala ***nx_ftp_server_start*** çağrısıyla başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-522">Note the FTP Server still needs to be started with a call to ***nx_ftp_server_start*** for it to begin operation after the Server is created.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-523">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-523">Input Parameters</span></span>

- <span data-ttu-id="87ba2-524">**ftp_server_ptr** FTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-524">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>
- <span data-ttu-id="87ba2-525">**ftp_server_name** FTP sunucusunun adı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-525">**ftp_server_name** Name of FTP Server.</span></span>
- <span data-ttu-id="87ba2-526">**ip_ptr** İlişkili NetX IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-526">**ip_ptr** Pointer to associated NetX IP instance.</span></span> <span data-ttu-id="87ba2-527">Bir IP örneği için yalnızca bir FTP sunucusu olabileceğini göz önünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87ba2-527">Note there can only be one FTP Server for an IP instance.</span></span>
- <span data-ttu-id="87ba2-528">**media_ptr** İlişkili FileX medya örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-528">**media_ptr** Pointer to associated FileX media instance.</span></span>
- <span data-ttu-id="87ba2-529">**stack_ptr** İç FTP sunucusu iş parçacığının yığın alanı için bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-529">**stack_ptr** Pointer to memory for the internal FTP Server thread’s stack area.</span></span>
- <span data-ttu-id="87ba2-530">**stack_size** *Stack_ptr* tarafından belirtilen yığın alanının boyutu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-530">**stack_size** Size of stack area specified by *stack_ptr*.</span></span>
- <span data-ttu-id="87ba2-531">**pool_ptr** Varsayılan NetX paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-531">**pool_ptr** Pointer to default NetX packet pool.</span></span> <span data-ttu-id="87ba2-532">Notdaki paketlerin yük boyutu, en büyük dosya adına/yola uyum sağlayacak kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-532">Note the payload size of packets in the pool must be large enough to accommodate the largest filename/path.</span></span>
- <span data-ttu-id="87ba2-533">**ftp_login_duo** Uygulamanın oturum açma işlevine yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-533">**ftp_login_duo** Function pointer to application’s login function.</span></span> <span data-ttu-id="87ba2-534">Bu işleve, bir bağlantı isteyen Istemciden Kullanıcı adı ve parola ve NXD_ADDRESS veri türünde Istemci adresine yönelik bir işaretçi verilir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-534">This function is supplied the username and password from the Client requesting a connection, and a pointer to the Client address in the NXD_ADDRESS data type.</span></span> <span data-ttu-id="87ba2-535">Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-535">If this is valid, the application’s login function should return NX_SUCCESS.</span></span>
- <span data-ttu-id="87ba2-536">**ftp_logout_duo** Uygulamanın oturum kapatma işlevine yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-536">**ftp_logout_duo** Function pointer to application’s logout function.</span></span> <span data-ttu-id="87ba2-537">Bu işleve, bir bağlantı kesilmesi isteyen Istemciden Kullanıcı adı ve parola ve NXD_ADDRESS veri türünde Istemci adresine yönelik bir işaretçi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-537">This function is supplied the username and password from the Client requesting a disconnection, and a pointer to the Client address in the NXD_ADDRESS data type.</span></span> <span data-ttu-id="87ba2-538">Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="87ba2-538">If this is valid, the application’s login function should return NX_SUCCESS.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-539">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-539">Return Values</span></span>

- <span data-ttu-id="87ba2-540">**NX_SUCCESS** (0x00) başarılı FTP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="87ba2-540">**NX_SUCCESS** (0x00) Successful FTP Server create.</span></span>
- <span data-ttu-id="87ba2-541">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-541">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-542">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-542">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-543">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-543">Allowed From</span></span>

<span data-ttu-id="87ba2-544">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-544">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-545">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-545">Example</span></span>

```C
/* Create the FTP Server “my_server” on the IP instance “ip_0” using the
    “ram_disk” media. */

status = nxd_ftp_server_create(&my_server, “My Server Name”, &ip_0, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_duo_login, my_duo_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nx_ftp_server_delete"></a><span data-ttu-id="87ba2-546">nx_ftp_server_delete</span><span class="sxs-lookup"><span data-stu-id="87ba2-546">nx_ftp_server_delete</span></span>

<span data-ttu-id="87ba2-547">FTP sunucusunu Sil</span><span class="sxs-lookup"><span data-stu-id="87ba2-547">Delete FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-548">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-548">Prototype</span></span>

```C
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="87ba2-549">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-549">Description</span></span>

<span data-ttu-id="87ba2-550">Bu hizmet, daha önce oluşturulmuş bir FTP sunucusu örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="87ba2-550">This service deletes a previously created FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-551">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-551">Input Parameters</span></span>

- <span data-ttu-id="87ba2-552">**ftp_server_ptr** FTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-552">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-553">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-553">Return Values</span></span>

- <span data-ttu-id="87ba2-554">**NX_SUCCESS** (0x00) FTP sunucusu başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-554">**NX_SUCCESS** (0x00) Successful FTP Server delete.</span></span>
- <span data-ttu-id="87ba2-555">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-555">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-556">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-556">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-557">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-557">Allowed From</span></span>

<span data-ttu-id="87ba2-558">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-558">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-559">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-559">Example</span></span>

```C
/* Delete the FTP Server “my_server”. */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a><span data-ttu-id="87ba2-560">nx_ftp_server_start</span><span class="sxs-lookup"><span data-stu-id="87ba2-560">nx_ftp_server_start</span></span>

<span data-ttu-id="87ba2-561">FTP sunucusunu Başlat</span><span class="sxs-lookup"><span data-stu-id="87ba2-561">Start FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-562">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-562">Prototype</span></span>

```C
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="87ba2-563">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-563">Description</span></span>

<span data-ttu-id="87ba2-564">Bu hizmet daha önce oluşturulmuş bir FTP sunucusu örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="87ba2-564">This service starts a previously created FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-565">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-565">Input Parameters</span></span>

- <span data-ttu-id="87ba2-566">**ftp_server_ptr** FTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-566">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-567">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-567">Return Values</span></span>

- <span data-ttu-id="87ba2-568">**NX_SUCCESS** (0x00) FTP sunucusu başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-568">**NX_SUCCESS** (0x00) Successful FTP Server start.</span></span>
- <span data-ttu-id="87ba2-569">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-569">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-570">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-570">Allowed From</span></span>

<span data-ttu-id="87ba2-571">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-571">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-572">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-572">Example</span></span>

```C
/* Start the FTP Server “my_server”. */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a><span data-ttu-id="87ba2-573">nx_ftp_server_stop</span><span class="sxs-lookup"><span data-stu-id="87ba2-573">nx_ftp_server_stop</span></span>

<span data-ttu-id="87ba2-574">FTP sunucusunu durdur</span><span class="sxs-lookup"><span data-stu-id="87ba2-574">Stop FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="87ba2-575">Prototype</span><span class="sxs-lookup"><span data-stu-id="87ba2-575">Prototype</span></span>

```C
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="87ba2-576">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ba2-576">Description</span></span>

<span data-ttu-id="87ba2-577">Bu hizmet daha önce oluşturulmuş ve başlatılmış bir FTP sunucu örneğini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="87ba2-577">This service stops a previously created and started FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="87ba2-578">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-578">Input Parameters</span></span>

- <span data-ttu-id="87ba2-579">**ftp_server_ptr** FTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-579">**ftp_server_ptr** Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="87ba2-580">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="87ba2-580">Return Values</span></span>

- <span data-ttu-id="87ba2-581">**NX_SUCCESS** (0x00) başarılı FTP sunucusu durdu.</span><span class="sxs-lookup"><span data-stu-id="87ba2-581">**NX_SUCCESS** (0x00) Successful FTP Server stop.</span></span>
- <span data-ttu-id="87ba2-582">NX_PTR_ERROR (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="87ba2-582">NX_PTR_ERROR (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="87ba2-583">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="87ba2-583">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="87ba2-584">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="87ba2-584">Allowed From</span></span>

<span data-ttu-id="87ba2-585">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="87ba2-585">Threads</span></span>

### <a name="example"></a><span data-ttu-id="87ba2-586">Örnek</span><span class="sxs-lookup"><span data-stu-id="87ba2-586">Example</span></span>

```C
/* Stop the FTP Server “my_server”. */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
