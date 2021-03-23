---
title: Bölüm 3-Azure RTOS NetX FTP hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX FTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b05d03c45607c45acf32474cf8e40861532c5fae
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826722"
---
# <a name="chapter-3---description-of-azure-rtos-netx-ftp-services"></a><span data-ttu-id="be5af-103">Bölüm 3-Azure RTOS NetX FTP hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="be5af-103">Chapter 3 - Description of Azure RTOS NetX FTP services</span></span>

<span data-ttu-id="be5af-104">Bu bölüm, tüm Azure RTOS NetX FTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="be5af-104">This chapter contains a description of all Azure RTOS NetX FTP services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="be5af-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="be5af-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="be5af-106">**nx_ftp_client_connect**: *FTP sunucusuna bağlan*</span><span class="sxs-lookup"><span data-stu-id="be5af-106">**nx_ftp_client_connect**: *Connect to FTP Server*</span></span>
- <span data-ttu-id="be5af-107">**nx_ftp_client_create**: *FTP istemci örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="be5af-107">**nx_ftp_client_create**: *Create an FTP Client instance*</span></span>
- <span data-ttu-id="be5af-108">**nx_ftp_client_delete**: *FTP istemci örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="be5af-108">**nx_ftp_client_delete**: *Delete an FTP Client instance*</span></span>
- <span data-ttu-id="be5af-109">**nx_ftp_client_directory_create**: *sunucuda bir dizin oluşturma*</span><span class="sxs-lookup"><span data-stu-id="be5af-109">**nx_ftp_client_directory_create**: *Create a directory on Server*</span></span>
- <span data-ttu-id="be5af-110">**nx_ftp_client_directory_default_set**: *sunucuda varsayılan dizini ayarla*</span><span class="sxs-lookup"><span data-stu-id="be5af-110">**nx_ftp_client_directory_default_set**: *Set default directory on Server*</span></span>
- <span data-ttu-id="be5af-111">**nx_ftp_client_directory_delete**: *sunucuda bir dizini silme*</span><span class="sxs-lookup"><span data-stu-id="be5af-111">**nx_ftp_client_directory_delete**: *Delete a directory on Server*</span></span>
- <span data-ttu-id="be5af-112">**nx_ftp_client_directory_listing_get**: *sunucudan dizin listesini al*</span><span class="sxs-lookup"><span data-stu-id="be5af-112">**nx_ftp_client_directory_listing_get**: *Get directory listing from Server*</span></span>
- <span data-ttu-id="be5af-113">**nx_ftp_client_directory_listing_continue**: *sunucudan dizin listesine devam et*</span><span class="sxs-lookup"><span data-stu-id="be5af-113">**nx_ftp_client_directory_listing_continue**: *Continue directory listing from Server*</span></span>
- <span data-ttu-id="be5af-114">**nx_ftp_client_disconnect**: *FTP sunucusu bağlantısını kes*</span><span class="sxs-lookup"><span data-stu-id="be5af-114">**nx_ftp_client_disconnect**: *Disconnect from FTP Server*</span></span>
- <span data-ttu-id="be5af-115">**nx_ftp_client_file_close**: *istemci dosyasını kapat*</span><span class="sxs-lookup"><span data-stu-id="be5af-115">**nx_ftp_client_file_close**: *Close Client file*</span></span>
- <span data-ttu-id="be5af-116">**nx_ftp_client_file_delete**: *sunucudaki dosyayı Sil*</span><span class="sxs-lookup"><span data-stu-id="be5af-116">**nx_ftp_client_file_delete**: *Delete file on Server*</span></span>
- <span data-ttu-id="be5af-117">**nx_ftp_client_file_open**: *istemci dosyasını aç*</span><span class="sxs-lookup"><span data-stu-id="be5af-117">**nx_ftp_client_file_open**: *Open Client file*</span></span>
- <span data-ttu-id="be5af-118">**nx_ftp_client_file_read**: dosyadan *Oku*</span><span class="sxs-lookup"><span data-stu-id="be5af-118">**nx_ftp_client_file_read**: *Read from file*</span></span>
- <span data-ttu-id="be5af-119">**nx_ftp_client_file_rename**: *sunucudaki dosyayı yeniden adlandır*</span><span class="sxs-lookup"><span data-stu-id="be5af-119">**nx_ftp_client_file_rename**: *Rename file on Server*</span></span>
- <span data-ttu-id="be5af-120">**nx_ftp_client_file_write**: *dosyaya yaz*</span><span class="sxs-lookup"><span data-stu-id="be5af-120">**nx_ftp_client_file_write**: *Write to file*</span></span>
- <span data-ttu-id="be5af-121">**nx_ftp_server_create**: *FTP sunucusu oluştur*</span><span class="sxs-lookup"><span data-stu-id="be5af-121">**nx_ftp_server_create**: *Create FTP Server*</span></span>
- <span data-ttu-id="be5af-122">**nx_ftp_server_delete**: *FTP sunucusunu Sil*</span><span class="sxs-lookup"><span data-stu-id="be5af-122">**nx_ftp_server_delete**: *Delete FTP Server*</span></span>
- <span data-ttu-id="be5af-123">**nx_ftp_server_start**: *FTP sunucusunu Başlat*</span><span class="sxs-lookup"><span data-stu-id="be5af-123">**nx_ftp_server_start**: *Start FTP Server*</span></span>
- <span data-ttu-id="be5af-124">**nx_ftp_server_stop**: *FTP sunucusunu durdur*</span><span class="sxs-lookup"><span data-stu-id="be5af-124">**nx_ftp_server_stop**: *Stop FTP Server*</span></span>

## <a name="nx_ftp_client_connect"></a><span data-ttu-id="be5af-125">nx_ftp_client_connect</span><span class="sxs-lookup"><span data-stu-id="be5af-125">nx_ftp_client_connect</span></span>

<span data-ttu-id="be5af-126">FTP sunucusuna bağlanma</span><span class="sxs-lookup"><span data-stu-id="be5af-126">Connect to an FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-127">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-127">Prototype</span></span>

```c
UINT nx_ftp_client_connect(NX_FTP_CLIENT *ftp_client_ptr,
        ULONG server_ip, CHAR *username, CHAR *password,
        ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-128">Description</span></span>

<span data-ttu-id="be5af-129">Bu hizmet, önceden oluşturulan FTP Istemci örneğini sağlanan IP adresindeki FTP sunucusuna bağlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-129">This service connects the previously created FTP Client instance to the FTP Server at the supplied IP address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-130">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-130">Input Parameters</span></span>

- <span data-ttu-id="be5af-131">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-131">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-132">**server_ip**: FTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="be5af-132">**server_ip**: IP address of FTP Server.</span></span>
- <span data-ttu-id="be5af-133">**Kullanıcı adı**: kimlik doğrulaması için istemci Kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-133">**username**: Client username for authentication.</span></span>
- <span data-ttu-id="be5af-134">**parola**: kimlik doğrulaması için istemci parolası.</span><span class="sxs-lookup"><span data-stu-id="be5af-134">**password**: Client password for authentication.</span></span>
- <span data-ttu-id="be5af-135">**wait_option**: hizmetin FTP istemci bağlantısı için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-135">**wait_option**: Defines how long the service will wait for the FTP Client connection.</span></span> <span data-ttu-id="be5af-136">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-136">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-137">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-137">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-138">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-138">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-139">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-139">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-140">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-140">Return Values</span></span>

- <span data-ttu-id="be5af-141">**NX_SUCCESS**: (0x00) FTP bağlantısı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="be5af-141">**NX_SUCCESS**: (0x00) Successful FTP connection.</span></span>
- <span data-ttu-id="be5af-142">**NX_TFTP_EXPECTED_22X_CODE**: (0xDB), 22x (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-142">**NX_TFTP_EXPECTED_22X_CODE**: (0xDB) Did not get a 22X (ok) response</span></span>
- <span data-ttu-id="be5af-143">**NX_FTP_EXPECTED_23X_CODE**: (0xDC), 23x (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-143">**NX_FTP_EXPECTED_23X_CODE**: (0xDC) Did not get a 23X (ok) response</span></span>
- <span data-ttu-id="be5af-144">**NX_FTP_EXPECTED_33X_CODE**: (0xDE), bir 33x (Tamam) yanıtı almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-144">**NX_FTP_EXPECTED_33X_CODE**: (0xDE) Did not get a 33X (ok) response</span></span>
- <span data-ttu-id="be5af-145">**NX_FTP_NOT_DISCONNECTED**: (0xd4) istemci zaten bağlı.</span><span class="sxs-lookup"><span data-stu-id="be5af-145">**NX_FTP_NOT_DISCONNECTED**: (0xD4) Client is already connected.</span></span>
- <span data-ttu-id="be5af-146">NX_PTR_ERROR: (0x07) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="be5af-146">NX_PTR_ERROR: (0x07) Invalid pointer inout.</span></span>
- <span data-ttu-id="be5af-147">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-147">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="be5af-148">NX_IP_ADDRESS_ERROR: (0x21) geçersiz IP adresi.</span><span class="sxs-lookup"><span data-stu-id="be5af-148">NX_IP_ADDRESS_ERROR: (0x21) Invalid IP address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-149">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-149">Allowed From</span></span>

<span data-ttu-id="be5af-150">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-150">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-151">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-151">Example</span></span>

```c
/* Connect the FTP Client instance "my_client" to the FTP Server at
    IP address 1.2.3.4. */
status = nx_ftp_client_connect(&my_client, IP_ADDRESS(1,2,3,4), NULL, NULL, 100);

/* If status is NX_SUCCESS an FTP Client instance was successfully  
connected to the FTP Server. */
```

## <a name="nx_ftp_client_create"></a><span data-ttu-id="be5af-152">nx_ftp_client_create</span><span class="sxs-lookup"><span data-stu-id="be5af-152">nx_ftp_client_create</span></span>

<span data-ttu-id="be5af-153">FTP Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="be5af-153">Create an FTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-154">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-154">Prototype</span></span>

```c
UINT nx_ftp_client_create(NX_FTP_CLIENT *ftp_client_ptr,
    CHAR *ftp_client_name, NX_IP *ip_ptr, ULONG window_size,
    NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="be5af-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-155">Description</span></span>

<span data-ttu-id="be5af-156">Bu hizmet bir FTP Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be5af-156">This service creates an FTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-157">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-157">Input Parameters</span></span>

- <span data-ttu-id="be5af-158">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-158">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-159">**ftp_client_name**: FTP istemcisinin adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-159">**ftp_client_name**: Name of FTP Client.</span></span>
- <span data-ttu-id="be5af-160">**ip_ptr**: daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="be5af-160">**ip_ptr**: Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="be5af-161">**window_size**: Bu FTP istemcisinin TCP yuvası için tanıtılan pencere boyutu.</span><span class="sxs-lookup"><span data-stu-id="be5af-161">**window_size**: Advertised window size for TCP socket of this FTP Client.</span></span>
- <span data-ttu-id="be5af-162">**pool_ptr**: Bu FTP istemcisi için varsayılan paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="be5af-162">**pool_ptr**: Pointer to the default packet pool for this FTP Client.</span></span> <span data-ttu-id="be5af-163">En düşük paket yükünün, tüm yolu ve dosya ya da dizin adını tutabilecek kadar büyük olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="be5af-163">Note that the minimum packet payload must be large enough to hold complete path and the file or directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-164">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-164">Return Values</span></span>

- <span data-ttu-id="be5af-165">**NX_SUCCESS**: (0x00) başarılı FTP istemcisi oluştur.</span><span class="sxs-lookup"><span data-stu-id="be5af-165">**NX_SUCCESS**: (0x00) Successful FTP Client create.</span></span>
- <span data-ttu-id="be5af-166">NX_PTR_ERROR: (0x16) geçersiz FTP, IP işaretçisi veya paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-166">NX_PTR_ERROR: (0x16) Invalid FTP, IP pointer, or packet pool pointer.</span></span> <span data-ttu-id="be5af-167">parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-167">password pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-168">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-168">Allowed From</span></span>

<span data-ttu-id="be5af-169">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-169">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-170">Example</span></span>

```c
/* Create the FTP Client instance "my_client." */
status = nx_ftp_client_create(&my_client, "My Client", &client_ip,
                                2000, &client_pool);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
created. */
```

## <a name="nx_ftp_client_delete"></a><span data-ttu-id="be5af-171">nx_ftp_client_delete</span><span class="sxs-lookup"><span data-stu-id="be5af-171">nx_ftp_client_delete</span></span>

<span data-ttu-id="be5af-172">FTP Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="be5af-172">Delete an FTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-173">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-173">Prototype</span></span>

```c
UINT nx_ftp_client_delete(NX_FTP_CLIENT *ftp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="be5af-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-174">Description</span></span>

<span data-ttu-id="be5af-175">Bu hizmet bir FTP Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="be5af-175">This service deletes an FTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-176">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-176">Input Parameters</span></span>

- <span data-ttu-id="be5af-177">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-177">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-178">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-178">Return Values</span></span>

- <span data-ttu-id="be5af-179">**NX_SUCCESS**: (0x00) başarılı FTP istemcisi silme.</span><span class="sxs-lookup"><span data-stu-id="be5af-179">**NX_SUCCESS**: (0x00) Successful FTP Client delete.</span></span>
- <span data-ttu-id="be5af-180">**NX_FTP_NOT_DISCONNECTED**: (0xd4) FTP istemcisi silme hatası.</span><span class="sxs-lookup"><span data-stu-id="be5af-180">**NX_FTP_NOT_DISCONNECTED**: (0xD4) FTP Client delete error.</span></span>
- <span data-ttu-id="be5af-181">NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-181">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-182">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-182">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-183">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-183">Allowed From</span></span>

<span data-ttu-id="be5af-184">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-184">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-185">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-185">Example</span></span>

```c
/* Delete the FTP Client instance "my_client." */
status = nx_ftp_client_delete(&my_client);

/* If status is NX_SUCCESS the FTP Client instance was successfully  
    deleted. */
```

## <a name="nx_ftp_client_directory_create"></a><span data-ttu-id="be5af-186">nx_ftp_client_directory_create</span><span class="sxs-lookup"><span data-stu-id="be5af-186">nx_ftp_client_directory_create</span></span>

<span data-ttu-id="be5af-187">FTP sunucusunda bir dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="be5af-187">Create a directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-188">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-188">Prototype</span></span>

```c
UINT nx_ftp_client_directory_create(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-189">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-189">Description</span></span>

<span data-ttu-id="be5af-190">Bu hizmet, belirtilen FTP sunucusuna bağlı FTP sunucusunda belirtilen dizini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be5af-190">This service creates the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-191">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-191">Input Parameters</span></span>

- <span data-ttu-id="be5af-192">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-192">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-193">**directory_name**: Oluşturulacak dizinin adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-193">**directory_name**: Name of directory to create.</span></span>
- <span data-ttu-id="be5af-194">**wait_option**: hizmetin FTP dizin oluşturma için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-194">**wait_option**: Defines how long the service will wait for the FTP directory create.</span></span> <span data-ttu-id="be5af-195">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-195">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-196">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-196">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-197">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-197">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-198">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-198">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-199">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-199">Return Values</span></span>

- <span data-ttu-id="be5af-200">**NX_SUCCESS**: (0x00) başarılı FTP dizin oluşturma.</span><span class="sxs-lookup"><span data-stu-id="be5af-200">**NX_SUCCESS**: (0x00) Successful FTP directory create.</span></span>
- <span data-ttu-id="be5af-201">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-201">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-202">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-202">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span> 
- <span data-ttu-id="be5af-203">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-203">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span> 
- <span data-ttu-id="be5af-204">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-204">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-205">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-205">Allowed From</span></span>

<span data-ttu-id="be5af-206">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-206">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-207">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-207">Example</span></span>

```c
/* Create the directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_create(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" was successfully  
    created. */
```

## <a name="nx_ftp_client_directory_default_set"></a><span data-ttu-id="be5af-208">nx_ftp_client_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="be5af-208">nx_ftp_client_directory_default_set</span></span>

<span data-ttu-id="be5af-209">FTP sunucusunda varsayılan dizini ayarla</span><span class="sxs-lookup"><span data-stu-id="be5af-209">Set default directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-210">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-210">Prototype</span></span>

```c
UINT nx_ftp_client_directory_default_set(NX_FTP_CLIENT *ftp_client_ptr,
                                CHAR *directory_path, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-211">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-211">Description</span></span>

<span data-ttu-id="be5af-212">Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda varsayılan dizini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-212">This service sets the default directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="be5af-213">Bu varsayılan dizin yalnızca bu istemcinin bağlantısı için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="be5af-213">This default directory applies only to this client's connection.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-214">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-214">Input Parameters</span></span>

- <span data-ttu-id="be5af-215">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-215">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-216">**directory_path**: ayarlanacak dizin yolunun adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-216">**directory_path**: Name of directory path to set.</span></span>
- <span data-ttu-id="be5af-217">**wait_option**: hizmetin FTP varsayılan dizin kümesi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-217">**wait_option**: Defines how long the service will wait for the FTP default directory set.</span></span> <span data-ttu-id="be5af-218">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-218">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-219">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-219">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-220">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-220">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-221">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-221">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-222">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-222">Return Values</span></span>

- <span data-ttu-id="be5af-223">**NX_SUCCESS**: (0x00) başarılı FTP varsayılan kümesi.</span><span class="sxs-lookup"><span data-stu-id="be5af-223">**NX_SUCCESS**: (0x00) Successful FTP default set.</span></span>
- <span data-ttu-id="be5af-224">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-224">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-225">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-225">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span> 
- <span data-ttu-id="be5af-226">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-226">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span> 
- <span data-ttu-id="be5af-227">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-227">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-228">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-228">Allowed From</span></span>

<span data-ttu-id="be5af-229">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-229">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-230">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-230">Example</span></span>

```c
/* Set the default directory to "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_default_set(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is the default directory. */
```

## <a name="nx_ftp_client_directory_delete"></a><span data-ttu-id="be5af-231">nx_ftp_client_directory_delete</span><span class="sxs-lookup"><span data-stu-id="be5af-231">nx_ftp_client_directory_delete</span></span>

<span data-ttu-id="be5af-232">FTP sunucusundaki dizini Sil</span><span class="sxs-lookup"><span data-stu-id="be5af-232">Delete directory on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-233">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-233">Prototype</span></span>

```c
UINT nx_ftp_client_directory_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *directory_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-234">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-234">Description</span></span>

<span data-ttu-id="be5af-235">Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda belirtilen dizini siler.</span><span class="sxs-lookup"><span data-stu-id="be5af-235">This service deletes the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-236">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-236">Input Parameters</span></span>

- <span data-ttu-id="be5af-237">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-237">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-238">**directory_name**: silinecek dizinin adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-238">**directory_name**: Name of directory to delete.</span></span>
- <span data-ttu-id="be5af-239">**wait_option**: hizmetin FTP dizin silme işleminin ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-239">**wait_option**: Defines how long the service will wait for the FTP directory delete.</span></span> <span data-ttu-id="be5af-240">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-240">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-241">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-241">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-242">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-242">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-243">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-243">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-244">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-244">Return Values</span></span>

- <span data-ttu-id="be5af-245">**NX_SUCCESS**: (0x00) başarılı FTP dizin silme.</span><span class="sxs-lookup"><span data-stu-id="be5af-245">**NX_SUCCESS**: (0x00) Successful FTP directory delete.</span></span>
- <span data-ttu-id="be5af-246">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-246">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-247">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-247">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span> 
- <span data-ttu-id="be5af-248">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-248">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span> 
- <span data-ttu-id="be5af-249">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-249">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-250">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-250">Allowed From</span></span>

<span data-ttu-id="be5af-251">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-251">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-252">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-252">Example</span></span>

```c
/* Delete directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_delete(&my_client, "my_dir", 200);

/* If status is NX_SUCCESS the directory "my_dir" is deleted. */
```

## <a name="nx_ftp_client_directory_listing_get"></a><span data-ttu-id="be5af-253">nx_ftp_client_directory_listing_get</span><span class="sxs-lookup"><span data-stu-id="be5af-253">nx_ftp_client_directory_listing_get</span></span>

<span data-ttu-id="be5af-254">FTP sunucusundan dizin listesini al</span><span class="sxs-lookup"><span data-stu-id="be5af-254">Get directory listing from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-255">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-255">Prototype</span></span>

```c
UINT nx_ftp_client_directory_listing_get(NX_FTP_CLIENT *ftp_client_ptr,
                            CHAR *directory_name, NX_PACKET **packet_ptr,
                            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-256">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-256">Description</span></span>

<span data-ttu-id="be5af-257">Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda belirtilen dizinin içeriğini alır.</span><span class="sxs-lookup"><span data-stu-id="be5af-257">This service gets the contents of the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="be5af-258">Sağlanan paket işaretçisi bir veya daha fazla dizin girişi içerecektir.</span><span class="sxs-lookup"><span data-stu-id="be5af-258">The supplied packet pointer will contain one or more directory entries.</span></span> <span data-ttu-id="be5af-259">Her giriş bir &lt; CR/LF \ birleşimi ile ayrılır.</span><span class="sxs-lookup"><span data-stu-id="be5af-259">Each entry is separated by a &lt;cr/lf\combination.</span></span> <span data-ttu-id="be5af-260">***Nx_ftp_client_directory_listing_continue***: Dizin Al işlemini tamamlayacak şekilde çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be5af-260">The ***nx_ftp_client_directory_listing_continue***: should be called to complete the directory get operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-261">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-261">Input Parameters</span></span>

- <span data-ttu-id="be5af-262">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-262">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-263">**directory_name**: içeriğinin alınacağı dizinin adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-263">**directory_name**: Name of directory to get contents of.</span></span>
- <span data-ttu-id="be5af-264">**packet_ptr**: hedef paket işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="be5af-264">**packet_ptr**: Pointer to destination packet pointer.</span></span> <span data-ttu-id="be5af-265">Başarılı olursa, paket yükü bir veya daha fazla dizin girişi içerir.</span><span class="sxs-lookup"><span data-stu-id="be5af-265">If successful, the packet payload will contain one or more directory entries.</span></span>
- <span data-ttu-id="be5af-266">**wait_option**: hizmetin FTP dizin listesi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-266">**wait_option**: Defines how long the service will wait for the FTP directory listing.</span></span> <span data-ttu-id="be5af-267">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-267">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-268">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-268">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-269">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-269">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-270">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-270">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-271">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-271">Return Values</span></span>

- <span data-ttu-id="be5af-272">**NX_SUCCESS**: (0x00) FTP Dizin listeleme başarılı.</span><span class="sxs-lookup"><span data-stu-id="be5af-272">**NX_SUCCESS**: (0x00) Successful FTP directory listing.</span></span>
- <span data-ttu-id="be5af-273">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-273">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-274">**NX_NOT_ENABLED**: (0X14) hizmet (IPv6) etkin değil</span><span class="sxs-lookup"><span data-stu-id="be5af-274">**NX_NOT_ENABLED**: (0x14) Service (IPv6) not enabled</span></span>
- <span data-ttu-id="be5af-275">**NX_FTP_EXPECTED_1XX_CODE**: (0xD9), 1xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-275">**NX_FTP_EXPECTED_1XX_CODE**: (0xD9) Did not get a 1XX (ok) response</span></span>
- <span data-ttu-id="be5af-276">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-276">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="be5af-277">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-277">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-278">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-278">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-279">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-279">Allowed From</span></span>

<span data-ttu-id="be5af-280">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-280">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-281">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-281">Example</span></span>

```c
/* Get the contents of directory "my_dir" on the FTP Server connected to
    the FTP Client instance "my_client." */
status = nx_ftp_client_directory_listing_get(&my_client, "my_dir", &my_packet,
                                            200);

/* If status is NX_SUCCESS, one or more entries of the directory "my_dir"
    can be found in "my_packet". */
```

## <a name="nx_ftp_client_directory_listing_continue"></a><span data-ttu-id="be5af-282">nx_ftp_client_directory_listing_continue</span><span class="sxs-lookup"><span data-stu-id="be5af-282">nx_ftp_client_directory_listing_continue</span></span>

<span data-ttu-id="be5af-283">FTP sunucusundan dizin listesine devam et</span><span class="sxs-lookup"><span data-stu-id="be5af-283">Continue directory listing from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-284">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-284">Prototype</span></span>

```c
UINT nx_ftp_client_directory_listing_continue(NX_FTP_CLIENT
                    *ftp_client_ptr, NX_PACKET **packet_ptr,
                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-285">Description</span></span>

<span data-ttu-id="be5af-286">Bu hizmet, belirtilen FTP Istemcisine bağlı FTP sunucusunda belirtilen dizinin içeriğini almaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="be5af-286">This service continues getting the contents of the specified directory on the FTP Server that is connected to the specified FTP Client.</span></span> <span data-ttu-id="be5af-287">***Nx_ftp_client_directory_listing_get*** çağrısı hemen öncesinde gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="be5af-287">It should have been immediately preceded by a call to ***nx_ftp_client_directory_listing_get***.</span></span> <span data-ttu-id="be5af-288">Başarılı olursa, sağlanan paket işaretçisi bir veya daha fazla dizin girişi içerir.</span><span class="sxs-lookup"><span data-stu-id="be5af-288">If successful, the supplied packet pointer will contain one or more directory entries.</span></span> <span data-ttu-id="be5af-289">Bu yordam, bir NX_FTP_END_OF_LISTING durumu alınana kadar çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be5af-289">This routine should be called until an NX_FTP_END_OF_LISTING status is received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-290">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-290">Input Parameters</span></span>

- <span data-ttu-id="be5af-291">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-291">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-292">**packet_ptr**: hedef paket işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="be5af-292">**packet_ptr**: Pointer to destination packet pointer.</span></span> <span data-ttu-id="be5af-293">İşlem başarılı olursa, paket yükü bir CR/LF ile ayrılmış bir veya daha fazla dizin girişi içerecektir &lt; &gt; .</span><span class="sxs-lookup"><span data-stu-id="be5af-293">If successful, the packet payload will contain one or more directory entries, separated by a &lt;cr/lf&gt;.</span></span>
- <span data-ttu-id="be5af-294">**wait_option**: hizmetin FTP dizin listesi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-294">**wait_option**: Defines how long the service will wait for the FTP directory listing.</span></span> <span data-ttu-id="be5af-295">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-295">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-296">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-296">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-297">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-297">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-298">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-298">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-299">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-299">Return Values</span></span>

- <span data-ttu-id="be5af-300">**NX_SUCCESS**: (0x00) FTP Dizin listeleme başarılı.</span><span class="sxs-lookup"><span data-stu-id="be5af-300">**NX_SUCCESS**: (0x00) Successful FTP directory listing.</span></span>
- <span data-ttu-id="be5af-301">**NX_FTP_END_OF_LISTING**: (0xd8) bu dizinde daha fazla girdi yok.</span><span class="sxs-lookup"><span data-stu-id="be5af-301">**NX_FTP_END_OF_LISTING**: (0xD8) No more entries in this directory.</span></span>
- <span data-ttu-id="be5af-302">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-302">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-303">**NX_FTP_EXPECTED_2XX_CODE** (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-303">**NX_FTP_EXPECTED_2XX_CODE** (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="be5af-304">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-304">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-305">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-305">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-306">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-306">Allowed From</span></span>

<span data-ttu-id="be5af-307">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-307">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-308">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-308">Example</span></span>

```c
/* Continue getting the contents of directory "my_dir" on the FTP Server
    connected to the FTP Client instance "my_client." */
status = nx_ftp_client_directory_listing_continue(&my_client, &my_packet,
                                                200);

/* If status is NX_SUCCESS, one or more entries of the directory "my_dir"
    can be found in "my_packet". */
```

## <a name="nx_ftp_client_disconnect"></a><span data-ttu-id="be5af-309">nx_ftp_client_disconnect</span><span class="sxs-lookup"><span data-stu-id="be5af-309">nx_ftp_client_disconnect</span></span>

<span data-ttu-id="be5af-310">FTP sunucusu bağlantısını kes</span><span class="sxs-lookup"><span data-stu-id="be5af-310">Disconnect from FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-311">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-311">Prototype</span></span>

```c
UINT nx_ftp_client_disconnect(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-312">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-312">Description</span></span>

<span data-ttu-id="be5af-313">Bu hizmet, belirtilen FTP Istemcisiyle önceden oluşturulmuş bir FTP sunucusu bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="be5af-313">This service disconnects a previously established FTP Server connection with the specified FTP Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-314">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-314">Input Parameters</span></span>

- <span data-ttu-id="be5af-315">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-315">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-316">**wait_option**: hizmetin FTP istemcisinin bağlantısını kesmek için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-316">**wait_option**: Defines how long the service will wait for the FTP Client disconnect.</span></span> <span data-ttu-id="be5af-317">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-317">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-318">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-318">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-319">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-319">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-320">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-320">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-321">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-321">Return Values</span></span>

- <span data-ttu-id="be5af-322">**NX_SUCCESS**: (0x00) FTP bağlantısı başarıyla açıldı.</span><span class="sxs-lookup"><span data-stu-id="be5af-322">**NX_SUCCESS**: (0x00) Successful FTP disconnect.</span></span>
- <span data-ttu-id="be5af-323">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-323">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-324">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-324">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="be5af-325">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-325">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-326">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-326">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-327">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-327">Allowed From</span></span>

<span data-ttu-id="be5af-328">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-328">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-329">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-329">Example</span></span>

```c
/* Disconnect "my_client" from the FTP Server. */
status = nx_ftp_client_disconnect(&my_client, 200);

/* If status is NX_SUCCESS, "my_client" has been disconnected. */
```

## <a name="nx_ftp_client_file_close"></a><span data-ttu-id="be5af-330">nx_ftp_client_file_close</span><span class="sxs-lookup"><span data-stu-id="be5af-330">nx_ftp_client_file_close</span></span>

<span data-ttu-id="be5af-331">Istemci dosyasını kapat</span><span class="sxs-lookup"><span data-stu-id="be5af-331">Close Client file</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-332">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-332">Prototype</span></span>

```c
UINT nx_ftp_client_file_close(NX_FTP_CLIENT *ftp_client_ptr,
                            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-333">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-333">Description</span></span>

<span data-ttu-id="be5af-334">Bu hizmet, FTP sunucusunda daha önce açılmış bir dosyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="be5af-334">This service closes a previously opened file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-335">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-335">Input Parameters</span></span>

- <span data-ttu-id="be5af-336">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-336">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-337">**wait_option**: hizmetin FTP istemci dosyası kapanması için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-337">**wait_option**: Defines how long the service will wait for the FTP Client file close.</span></span> <span data-ttu-id="be5af-338">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-338">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-339">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-339">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-340">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-340">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-341">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-341">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-342">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-342">Return Values</span></span>

- <span data-ttu-id="be5af-343">**NX_SUCCESS**: (0x00) başarılı FTP dosyası kapatma.</span><span class="sxs-lookup"><span data-stu-id="be5af-343">**NX_SUCCESS**: (0x00) Successful FTP file close.</span></span>
- <span data-ttu-id="be5af-344">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-344">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-345">**NX_FTP_NOT_OPEN (0xD5)**: dosya açık değil; kapatılamıyor</span><span class="sxs-lookup"><span data-stu-id="be5af-345">**NX_FTP_NOT_OPEN (0xD5)**: File not open; cannot close it</span></span>
- <span data-ttu-id="be5af-346">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-346">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="be5af-347">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-347">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-348">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-348">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-349">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-349">Allowed From</span></span>

<span data-ttu-id="be5af-350">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-350">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-351">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-351">Example</span></span>

```c
/* Close previously opened file of client "my_client" on the FTP Server. */
status = nx_ftp_client_file_close(&my_client, 200);

/* If status is NX_SUCCESS, the file opened previously in the "my_client" FTP
    connection has been closed. */
```

## <a name="nx_ftp_client_file_delete"></a><span data-ttu-id="be5af-352">nx_ftp_client_file_delete</span><span class="sxs-lookup"><span data-stu-id="be5af-352">nx_ftp_client_file_delete</span></span>

<span data-ttu-id="be5af-353">FTP sunucusundaki dosyayı Sil</span><span class="sxs-lookup"><span data-stu-id="be5af-353">Delete file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-354">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-354">Prototype</span></span>

```c
UINT nx_ftp_client_file_delete(NX_FTP_CLIENT *ftp_client_ptr,
                        CHAR *file_name, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-355">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-355">Description</span></span>

<span data-ttu-id="be5af-356">Bu hizmet, FTP sunucusunda belirtilen dosyayı siler.</span><span class="sxs-lookup"><span data-stu-id="be5af-356">This service deletes the specified file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-357">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-357">Input Parameters</span></span>

- <span data-ttu-id="be5af-358">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-358">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-359">**file_name**: Silinecek dosyanın adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-359">**file_name**: Name of file to delete.</span></span>
- <span data-ttu-id="be5af-360">**wait_option**: hizmetin FTP istemci dosyası silme işleminin ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-360">**wait_option**: Defines how long the service will wait for the FTP Client file delete.</span></span> <span data-ttu-id="be5af-361">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-361">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-362">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-362">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-363">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-363">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-364">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-364">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-365">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-365">Return Values</span></span>

- <span data-ttu-id="be5af-366">**NX_SUCCESS**: (0x00) FTP dosyası başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="be5af-366">**NX_SUCCESS**: (0x00) Successful FTP file delete.</span></span>
- <span data-ttu-id="be5af-367">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-367">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-368">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-368">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="be5af-369">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-369">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-370">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-370">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-371">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-371">Allowed From</span></span>

<span data-ttu-id="be5af-372">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-372">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-373">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-373">Example</span></span>

```c
/* Delete the file "my_file.txt" on the FTP Server using the previously
    connected client "my_client." */
status = nx_ftp_client_file_delete(&my_client, "my_file.txt", 200);

/* If status is NX_SUCCESS, the file "my_file.txt" on the FTP Server is
    deleted. */
```

## <a name="nx_ftp_client_file_open"></a><span data-ttu-id="be5af-374">nx_ftp_client_file_open</span><span class="sxs-lookup"><span data-stu-id="be5af-374">nx_ftp_client_file_open</span></span>

<span data-ttu-id="be5af-375">Dosyayı FTP sunucusunda açar</span><span class="sxs-lookup"><span data-stu-id="be5af-375">Opens file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-376">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-376">Prototype</span></span>

```c
UINT nx_ftp_client_file_open(NX_FTP_CLIENT *ftp_client_ptr,
        CHAR *file_name, UINT open_type, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-377">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-377">Description</span></span>

<span data-ttu-id="be5af-378">Bu hizmet, belirtilen Istemci örneğine daha önce bağlı FTP sunucusunda belirtilen dosyayı (okuma veya yazma için) açar.</span><span class="sxs-lookup"><span data-stu-id="be5af-378">This service opens the specified file – for reading or writing – on the FTP Server previously connected to the specified Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-379">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-379">Input Parameters</span></span>

- <span data-ttu-id="be5af-380">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-380">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-381">**file_name**: açılacak dosyanın adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-381">**file_name**: Name of file to open.</span></span>
- <span data-ttu-id="be5af-382">**open_type**: **NX_FTP_OPEN_FOR_READ** veya **NX_FTP_OPEN_FOR_WRITE**.</span><span class="sxs-lookup"><span data-stu-id="be5af-382">**open_type**: Either **NX_FTP_OPEN_FOR_READ** or **NX_FTP_OPEN_FOR_WRITE**.</span></span>
- <span data-ttu-id="be5af-383">**wait_option**: hizmetin FTP istemci dosyası açılmasını ne kadar süreyle bekleyecektir tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-383">**wait_option**: Defines how long the service will wait for the FTP Client file open.</span></span> <span data-ttu-id="be5af-384">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-384">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-385">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-385">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-386">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-386">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-387">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-387">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-388">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-388">Return Values</span></span>

- <span data-ttu-id="be5af-389">**NX_SUCCESS**: (0x00) FTP dosyası başarıyla açıldı.</span><span class="sxs-lookup"><span data-stu-id="be5af-389">**NX_SUCCESS**: (0x00) Successful FTP file open.</span></span>
- <span data-ttu-id="be5af-390">**NX_OPTION_ERROR**: (0X0a) geçersiz açık tür.</span><span class="sxs-lookup"><span data-stu-id="be5af-390">**NX_OPTION_ERROR**: (0x0A) Invalid open type.</span></span>
- <span data-ttu-id="be5af-391">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-391">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-392">**NX_FTP_NOT_CLOSED**: (0xd6) FTP istemcisi zaten açık.</span><span class="sxs-lookup"><span data-stu-id="be5af-392">**NX_FTP_NOT_CLOSED**: (0xD6) FTP Client is already opened.</span></span>
- <span data-ttu-id="be5af-393">**NX_NO_FREE_PORTS**: (0x45) atanacak TCP bağlantı noktası yok</span><span class="sxs-lookup"><span data-stu-id="be5af-393">**NX_NO_FREE_PORTS**: (0x45) No TCP ports available to assign</span></span>
- <span data-ttu-id="be5af-394">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-394">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-395">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-395">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-396">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-396">Allowed From</span></span>

<span data-ttu-id="be5af-397">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-397">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-398">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-398">Example</span></span>

```c
/* Open the file "my_file.txt" for reading on the FTP Server using the previously
    connected client "my_client." */
status = nx_ftp_client_file_open(&my_client, "my_file.txt", NX_FTP_OPEN_FOR_READ,
                                200);

/* If status is NX_SUCCESS, the file "my_file.txt" on the FTP Server is
    open for reading. */
```

## <a name="nx_ftp_client_file_read"></a><span data-ttu-id="be5af-399">nx_ftp_client_file_read</span><span class="sxs-lookup"><span data-stu-id="be5af-399">nx_ftp_client_file_read</span></span>

<span data-ttu-id="be5af-400">Dosyadan oku</span><span class="sxs-lookup"><span data-stu-id="be5af-400">Read from file</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-401">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-401">Prototype</span></span>

```c
UINT nx_ftp_client_file_read(NX_FTP_CLIENT *ftp_client_ptr,
                NX_PACKET **packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-402">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-402">Description</span></span>

<span data-ttu-id="be5af-403">Bu hizmet, daha önce açılmış bir dosyanın paketini okur.</span><span class="sxs-lookup"><span data-stu-id="be5af-403">This service reads a packet from a previously opened file.</span></span> <span data-ttu-id="be5af-404">NX_FTP_END_OF_FILE bir durum alınana kadar kaldı çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be5af-404">It should be called repetitively until a status of NX_FTP_END_OF_FILE is received.</span></span>

<span data-ttu-id="be5af-405">Çağıranın bu hizmet için bir paket ayırmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="be5af-405">Note that the caller does not allocate a packet for this service.</span></span>  <span data-ttu-id="be5af-406">Yalnızca bir paket işaretçisine işaretçi sağlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="be5af-406">It need only supply a pointer to a packet pointer.</span></span> <span data-ttu-id="be5af-407">Bu hizmet, bu paket işaretçisini yuva alma sırasından alınan bir pakete işaret edecek şekilde güncelleştirecek.</span><span class="sxs-lookup"><span data-stu-id="be5af-407">This service will update that packet pointer to point to a packet retrieved from the socket receive queue.</span></span>  <span data-ttu-id="be5af-408">Başarılı bir durum döndürülürse, bu, kullanılabilir bir paket olduğu anlamına gelir ve bu, paketin yaptığı sırada paketi serbest bırakma sorumluluğudur.</span><span class="sxs-lookup"><span data-stu-id="be5af-408">If a successful status is returned, that means there was a packet available, and it is the caller's responsibility to release the packet when it is done with it.</span></span>

<span data-ttu-id="be5af-409">Sıfır olmayan bir durum (bir hata durumu veya NX_FTP_END_OF_FILE) döndürülürse, çağıran paketi serbest bırakmaz.</span><span class="sxs-lookup"><span data-stu-id="be5af-409">If a non-zero status (either an error status or NX_FTP_END_OF_FILE) is returned, the caller does not release the packet.</span></span> <span data-ttu-id="be5af-410">Aksi takdirde, paket işaretçisi NULL olduğunda bir hata oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="be5af-410">Otherwise, an error is generated when if the packet pointer is NULL.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-411">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-411">Input Parameters</span></span>

- <span data-ttu-id="be5af-412">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-412">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-413">**packet_ptr**: kuyruktan alınan veri paketi işaretçisi için hedef işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-413">**packet_ptr**: Pointer to destination for the data packet pointer retrieved from the queue.</span></span> <span data-ttu-id="be5af-414">Başarılı olursa, paket verileri dosyanın bir kısmını veya tamamını içerir.</span><span class="sxs-lookup"><span data-stu-id="be5af-414">If successful, the packet data contains some or all of the file.</span></span>
- <span data-ttu-id="be5af-415">**wait_option**: hizmetin FTP istemci dosyası okuması için ne kadar süre bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-415">**wait_option**: Defines how long the service will wait for the FTP Client file read.</span></span> <span data-ttu-id="be5af-416">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-416">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-417">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-417">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-418">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-418">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-419">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-419">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-420">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-420">Return Values</span></span>

- <span data-ttu-id="be5af-421">**NX_SUCCESS**: (0x00) FTP dosyası başarıyla okundu.</span><span class="sxs-lookup"><span data-stu-id="be5af-421">**NX_SUCCESS**: (0x00) Successful FTP file read.</span></span>
- <span data-ttu-id="be5af-422">**NX_FTP_NOT_OPEN**: (0xd5) FTP istemcisi açık değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-422">**NX_FTP_NOT_OPEN**: (0xD5) FTP Client is not opened.</span></span>
- <span data-ttu-id="be5af-423">**NX_FTP_END_OF_FILE**: (0xd7) dosya koşulunun sonu.</span><span class="sxs-lookup"><span data-stu-id="be5af-423">**NX_FTP_END_OF_FILE**: (0xD7) End of file condition.</span></span>
- <span data-ttu-id="be5af-424">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-424">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-425">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-425">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-426">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-426">Allowed From</span></span>

<span data-ttu-id="be5af-427">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-427">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-428">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-428">Example</span></span>

```c
       NX_PACKET   *my_packet;

/* Read a packet of data from the file "my_file.txt" that was previously opened
    from the client "my_client." */

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

/* If status is NX_SUCCESS, the packet pointer, "my_packet" points to the packet
that contains the next bytes from the file. If the file is completely
downloaded, an NX_FTP_END_OF_FILE status is returned (no packet retrieved). */
```

## <a name="nx_ftp_client_file_rename"></a><span data-ttu-id="be5af-429">nx_ftp_client_file_rename</span><span class="sxs-lookup"><span data-stu-id="be5af-429">nx_ftp_client_file_rename</span></span>

<span data-ttu-id="be5af-430">FTP sunucusundaki dosyayı yeniden adlandır</span><span class="sxs-lookup"><span data-stu-id="be5af-430">Rename file on FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-431">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-431">Prototype</span></span>

```c
UINT nx_ftp_client_file_rename(NX_FTP_CLIENT *ftp_ptr, CHAR *filename,
                                CHAR *new_filename, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-432">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-432">Description</span></span>

<span data-ttu-id="be5af-433">Bu hizmet, FTP sunucusundaki bir dosyayı yeniden adlandırır.</span><span class="sxs-lookup"><span data-stu-id="be5af-433">This service renames a file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-434">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-434">Input Parameters</span></span>

- <span data-ttu-id="be5af-435">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-435">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-436">**dosya adı**: dosyanın geçerli adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-436">**filename**: Current name of file.</span></span>
- <span data-ttu-id="be5af-437">**new_filename**: dosyanın yeni adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-437">**new_filename**: New name for file.</span></span>
- <span data-ttu-id="be5af-438">**wait_option**: hizmetin FTP istemci dosyası yeniden adlandırma için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-438">**wait_option**: Defines how long the service will wait for the FTP Client file rename.</span></span> <span data-ttu-id="be5af-439">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-439">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-440">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-440">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-441">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-441">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-442">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-442">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-443">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-443">Return Values</span></span>

- <span data-ttu-id="be5af-444">**NX_SUCCESS**: (0x00) başarılı FTP dosyası yeniden adlandırma.</span><span class="sxs-lookup"><span data-stu-id="be5af-444">**NX_SUCCESS**: (0x00) Successful FTP file rename.</span></span>
- <span data-ttu-id="be5af-445">**NX_FTP_NOT_CONNECTED**: (0xd3) FTP istemcisi bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-445">**NX_FTP_NOT_CONNECTED**: (0xD3) FTP Client is not connected.</span></span>
- <span data-ttu-id="be5af-446">**NX_FTP_EXPECTED_3XX_CODE**: (0xDD), 3xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-446">**NX_FTP_EXPECTED_3XX_CODE**: (0XDD) Did not receive 3XX (ok) response</span></span>
- <span data-ttu-id="be5af-447">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA), 2xx (Tamam) yanıtını almadı</span><span class="sxs-lookup"><span data-stu-id="be5af-447">**NX_FTP_EXPECTED_2XX_CODE**: (0xDA) Did not get a 2XX (ok) response</span></span>
- <span data-ttu-id="be5af-448">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-448">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-449">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-449">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-450">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-450">Allowed From</span></span>

<span data-ttu-id="be5af-451">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-451">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-452">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-452">Example</span></span>

```c
/* Rename file "my_file.txt" to "new_file.txt" on the previously connected
    Client instance "my_client." */

status = nx_ftp_client_file_rename(&my_client, "my_file.txt", "new_file.txt",
                                    200);

/* If status is NX_SUCCESS, the file has been renamed. */
```

## <a name="nx_ftp_client_file_write"></a><span data-ttu-id="be5af-453">nx_ftp_client_file_write</span><span class="sxs-lookup"><span data-stu-id="be5af-453">nx_ftp_client_file_write</span></span>

<span data-ttu-id="be5af-454">Dosyaya yaz</span><span class="sxs-lookup"><span data-stu-id="be5af-454">Write to file</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-455">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-455">Prototype</span></span>

```c
UINT nx_ftp_client_file_write(NX_FTP_CLIENT *ftp_client_ptr,
                    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="be5af-456">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-456">Description</span></span>

<span data-ttu-id="be5af-457">Bu hizmet, FTP sunucusundaki daha önce açılan dosyaya bir veri paketi yazar.</span><span class="sxs-lookup"><span data-stu-id="be5af-457">This service writes a packet of data to the previously opened file on the FTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-458">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-458">Input Parameters</span></span>

- <span data-ttu-id="be5af-459">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-459">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-460">**packet_ptr**: yazılacak verileri içeren paket işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-460">**packet_ptr**: Packet pointer containing data to write.</span></span>
- <span data-ttu-id="be5af-461">**wait_option**: hizmetin FTP istemci dosyası yazma süresini ne kadar bekleyecektir tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-461">**wait_option**: Defines how long the service will wait for the FTP Client file write.</span></span> <span data-ttu-id="be5af-462">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="be5af-462">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="be5af-463">**zaman aşımı değeri**: (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="be5af-463">**timeout value**: (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="be5af-464">**TX_WAIT_FOREVER**: (0xffffffff) TX_WAIT_FOREVER seçilmesi çağıran iş PARÇACıĞıNıN bir FTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="be5af-464">**TX_WAIT_FOREVER**: (0xFFFFFFFF) Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a FTP Server responds to the request.</span></span> <span data-ttu-id="be5af-465">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, FTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="be5af-465">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the FTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-466">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-466">Return Values</span></span>

- <span data-ttu-id="be5af-467">**NX_SUCCESS**: (0x00) başarılı FTP dosyası yazma.</span><span class="sxs-lookup"><span data-stu-id="be5af-467">**NX_SUCCESS**: (0x00) Successful FTP file write.</span></span>
- <span data-ttu-id="be5af-468">**NX_FTP_NOT_OPEN**: (0xd5) FTP istemcisi açık değil.</span><span class="sxs-lookup"><span data-stu-id="be5af-468">**NX_FTP_NOT_OPEN**: (0xD5) FTP Client is not opened.</span></span>
- <span data-ttu-id="be5af-469">NX_PTR_ERROR: (0x07) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-469">NX_PTR_ERROR: (0x07) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-470">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-470">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-471">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-471">Allowed From</span></span>

<span data-ttu-id="be5af-472">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-472">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-473">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-473">Example</span></span>

```c
/* Write the data contained in "my_packet" to the previously opened file
    "my_file.txt". */

status = nx_ftp_client_file_write(&my_client, my_packet, 200);

/* If status is NX_SUCCESS, the file has been written to. */
```

## <a name="nx_ftp_client_passive_mode_set"></a><span data-ttu-id="be5af-474">nx_ftp_client_passive_mode_set</span><span class="sxs-lookup"><span data-stu-id="be5af-474">nx_ftp_client_passive_mode_set</span></span>

<span data-ttu-id="be5af-475">Pasif aktarım modunu etkinleştirme veya devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="be5af-475">Enable or disable passive transfer mode</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-476">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-476">Prototype</span></span>

```c
UINT nx_ftp_client_passive_mode_set(NX_FTP_CLIENT *ftp_client_ptr,
                                    UINT passive_mode_enabled);
```

### <a name="description"></a><span data-ttu-id="be5af-477">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-477">Description</span></span>

<span data-ttu-id="be5af-478">Bu hizmet, passive_mode_enabled girişi daha önceden oluşturulmuş bir FTP Istemci örneğinde NX_TRUE olarak ayarlandıysa (RETR, STOR) veya bir dizin listesini indirme (NLST), Aktarım modunda yapıldıktan sonra, pasif aktarım modunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="be5af-478">This service enables passive transfer mode if the passive_mode_enabled input is set to NX_TRUE on a previously created FTP Client instance such that subsequent calls to read or write files (RETR, STOR) or download a directory listing (NLST) are done in transfer mode.</span></span> <span data-ttu-id="be5af-479">Pasif mod aktarımını devre dışı bırakmak ve etkin aktarım modunun varsayılan davranışına geri dönmek için, bu işlevi passive_mode_enabled girişi NX_FALSE kümesiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="be5af-479">To disable passive mode transfer and return to the default behavior of active transfer mode, call this function with the passive_mode_enabled input set to NX_FALSE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-480">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-480">Input Parameters</span></span>

- <span data-ttu-id="be5af-481">**ftp_client_ptr**: FTP istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-481">**ftp_client_ptr**: Pointer to FTP Client control block.</span></span>
- <span data-ttu-id="be5af-482">**passive_mode_enabled**:</span><span class="sxs-lookup"><span data-stu-id="be5af-482">**passive_mode_enabled**:</span></span>
  - <span data-ttu-id="be5af-483">NX_TRUE olarak ayarlanırsa, Pasif mod etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="be5af-483">If set to NX_TRUE, passive mode is enabled.</span></span>
  - <span data-ttu-id="be5af-484">NX_FALSE olarak ayarlanırsa, Pasif mod devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="be5af-484">If set to NX_FALSE, passive mode is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-485">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-485">Return Values</span></span>

- <span data-ttu-id="be5af-486">**NX_SUCCESS**: (0x00) başarılı Pasif mod kümesi.</span><span class="sxs-lookup"><span data-stu-id="be5af-486">**NX_SUCCESS**: (0x00) Successful passive mode set.</span></span>
- <span data-ttu-id="be5af-487">NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-487">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-488">NX_INVALID_PARAMETERS: (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="be5af-488">NX_INVALID_PARAMETERS: (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-489">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-489">Allowed From</span></span>

<span data-ttu-id="be5af-490">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-490">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-491">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-491">Example</span></span>

```c
/* Enable the FTP Client to exchange data with the FTP server in passive mode. */

status = nx_ftp_client_passive_mode_set(&my_client, NX_TRUE);

/* If status is NX_SUCCESS, the FTP client is in passive transfer mode. */
```

## <a name="nx_ftp_server_create"></a><span data-ttu-id="be5af-492">nx_ftp_server_create</span><span class="sxs-lookup"><span data-stu-id="be5af-492">nx_ftp_server_create</span></span>

<span data-ttu-id="be5af-493">FTP sunucusu oluştur</span><span class="sxs-lookup"><span data-stu-id="be5af-493">Create FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-494">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-494">Prototype</span></span>

```c
UINT nx_ftp_server_create(NX_FTP_SERVER *ftp_server_ptr,
        CHAR *ftp_server_name, NX_IP *ip_ptr,
        FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
        NX_PACKET_POOL *pool_ptr,
        UINT (*ftp_login)(struct NX_FTP_SERVER_STRUCT
                *ftp_server_ptr, ULONG client_ip_address,
                UINT client_port, CHAR *name, CHAR *password,
                CHAR *extra_info),
        UINT (*ftp_logout)(struct NX_FTP_SERVER_STRUCT
                *ftp_server_ptr, ULONG client_ip_address,
                UINT client_port, CHAR *name, CHAR *password,
                CHAR *extra_info));
```

### <a name="description"></a><span data-ttu-id="be5af-495">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-495">Description</span></span>

<span data-ttu-id="be5af-496">Bu hizmet, belirtilen ve daha önce oluşturulmuş NetX IP örneğinde bir FTP sunucu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="be5af-496">This service creates an FTP Server instance on the specified and previously created NetX IP instance.</span></span> <span data-ttu-id="be5af-497">FTP sunucusunun, işleme başlaması için bir ***nx_ftp_server_start*** çağrısıyla başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be5af-497">Note the FTP Server needs to be started with a call to ***nx_ftp_server_start*** for it to begin operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-498">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-498">Input Parameters</span></span>

- <span data-ttu-id="be5af-499">**ftp_server_ptr**: FTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-499">**ftp_server_ptr**: Pointer to FTP Server control block.</span></span>
- <span data-ttu-id="be5af-500">**ftp_server_name**: FTP sunucusunun adı.</span><span class="sxs-lookup"><span data-stu-id="be5af-500">**ftp_server_name**: Name of FTP Server.</span></span>
- <span data-ttu-id="be5af-501">**ip_ptr**: Ilişkili NETX IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="be5af-501">**ip_ptr**: Pointer to associated NetX IP instance.</span></span> <span data-ttu-id="be5af-502">Bir IP örneği için yalnızca bir FTP sunucusu olabileceğini göz önünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be5af-502">Note there can only be one FTP Server for an IP instance.</span></span>
- <span data-ttu-id="be5af-503">**media_ptr**: Ilişkili FileX medya örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="be5af-503">**media_ptr**: Pointer to associated FileX media instance.</span></span>
- <span data-ttu-id="be5af-504">**stack_ptr**: Iç FTP sunucusu iş parçacığının yığın alanı için bellek işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-504">**stack_ptr**: Pointer to memory for the internal FTP Server thread's stack area.</span></span>
- <span data-ttu-id="be5af-505">**stack_size**: *stack_ptr* tarafından belirtilen yığın alanının boyutu.</span><span class="sxs-lookup"><span data-stu-id="be5af-505">**stack_size**: Size of stack area specified by *stack_ptr*.</span></span>
- <span data-ttu-id="be5af-506">**pool_ptr**: varsayılan NETX paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="be5af-506">**pool_ptr**: Pointer to default NetX packet pool.</span></span> <span data-ttu-id="be5af-507">Notdaki paketlerin yük boyutu, en büyük dosya adına/yola uyum sağlayacak kadar büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be5af-507">Note the payload size of packets in the pool must be large enough to accommodate the largest filename/path.</span></span>
- <span data-ttu-id="be5af-508">**ftp_login**: uygulamanın oturum açma işlevine yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-508">**ftp_login**: Function pointer to application's login function.</span></span> <span data-ttu-id="be5af-509">Bu işleve bir bağlantı isteyen Istemciden Kullanıcı adı ve parola verilir.</span><span class="sxs-lookup"><span data-stu-id="be5af-509">This function is supplied the username and password from the Client requesting a connection.</span></span> <span data-ttu-id="be5af-510">Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="be5af-510">If this is valid, the application's login function should return NX_SUCCESS.</span></span>
- <span data-ttu-id="be5af-511">**ftp_logout**: uygulamanın oturum kapatma işlevine yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-511">**ftp_logout**: Function pointer to application's logout function.</span></span> <span data-ttu-id="be5af-512">Bu işleve, bir bağlantı kesilmesi isteyen Istemciden Kullanıcı adı ve parola verilir.</span><span class="sxs-lookup"><span data-stu-id="be5af-512">This function is supplied the username and password from the Client requesting a disconnection.</span></span> <span data-ttu-id="be5af-513">Bu geçerliyse, uygulamanın oturum açma işlevi NX_SUCCESS döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="be5af-513">If this is valid, the application's login function should return NX_SUCCESS.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-514">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-514">Return Values</span></span>

- <span data-ttu-id="be5af-515">**NX_SUCCESS**: (0x00) başarılı FTP sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="be5af-515">**NX_SUCCESS**: (0x00) Successful FTP Server create.</span></span>
- <span data-ttu-id="be5af-516">NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-516">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-517">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-517">Allowed From</span></span>

<span data-ttu-id="be5af-518">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-518">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-519">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-519">Example</span></span>

```c
/* Create the FTP Server "my_server" on the IP instance "ip_0" using the
    "ram_disk" media. */

status = nx_ftp_server_create(&my_server, "My Server Name", &ip_0, &ram_disk,
                                stack_ptr, stack_size, &pool_0,
                                my_login, my_logout);

/* If status is NX_SUCCESS, the FTP Server has been created. */
```

## <a name="nx_ftp_server_delete"></a><span data-ttu-id="be5af-520">nx_ftp_server_delete</span><span class="sxs-lookup"><span data-stu-id="be5af-520">nx_ftp_server_delete</span></span>

<span data-ttu-id="be5af-521">FTP sunucusunu Sil</span><span class="sxs-lookup"><span data-stu-id="be5af-521">Delete FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-522">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-522">Prototype</span></span>

```c
UINT nx_ftp_server_delete(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="be5af-523">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-523">Description</span></span>

<span data-ttu-id="be5af-524">Bu hizmet, daha önce oluşturulmuş bir FTP sunucusu örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="be5af-524">This service deletes a previously created FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-525">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-525">Input Parameters</span></span>

- <span data-ttu-id="be5af-526">**ftp_server_ptr**: FTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-526">**ftp_server_ptr**: Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-527">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-527">Return Values</span></span>

- <span data-ttu-id="be5af-528">**NX_SUCCESS**: (0x00) FTP sunucusu başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="be5af-528">**NX_SUCCESS**: (0x00) Successful FTP Server delete.</span></span>
- <span data-ttu-id="be5af-529">NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-529">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-530">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-530">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-531">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-531">Allowed From</span></span>

<span data-ttu-id="be5af-532">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-532">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-533">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-533">Example</span></span>

```c
/* Delete the FTP Server "my_server". */

status = nx_ftp_server_delete(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been deleted. */
```

## <a name="nx_ftp_server_start"></a><span data-ttu-id="be5af-534">nx_ftp_server_start</span><span class="sxs-lookup"><span data-stu-id="be5af-534">nx_ftp_server_start</span></span>

<span data-ttu-id="be5af-535">FTP sunucusunu Başlat</span><span class="sxs-lookup"><span data-stu-id="be5af-535">Start FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-536">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-536">Prototype</span></span>

```c
UINT nx_ftp_server_start(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="be5af-537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-537">Description</span></span>

<span data-ttu-id="be5af-538">Bu hizmet daha önce oluşturulmuş bir FTP sunucusu örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="be5af-538">This service starts a previously created FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-539">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-539">Input Parameters</span></span>

- <span data-ttu-id="be5af-540">**ftp_server_ptr**: FTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-540">**ftp_server_ptr**: Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-541">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-541">Return Values</span></span>

- <span data-ttu-id="be5af-542">**NX_SUCCESS**: (0x00) FTP sunucusu başarıyla başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="be5af-542">**NX_SUCCESS**: (0x00) Successful FTP Server start.</span></span>
- <span data-ttu-id="be5af-543">NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-543">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-544">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-544">Allowed From</span></span>

<span data-ttu-id="be5af-545">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-545">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-546">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-546">Example</span></span>

```c
/* Start the FTP Server "my_server". */

status = nx_ftp_server_start(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been started. */
```

## <a name="nx_ftp_server_stop"></a><span data-ttu-id="be5af-547">nx_ftp_server_stop</span><span class="sxs-lookup"><span data-stu-id="be5af-547">nx_ftp_server_stop</span></span>

<span data-ttu-id="be5af-548">FTP sunucusunu durdur</span><span class="sxs-lookup"><span data-stu-id="be5af-548">Stop FTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="be5af-549">Prototype</span><span class="sxs-lookup"><span data-stu-id="be5af-549">Prototype</span></span>

```c
UINT nx_ftp_server_stop(NX_FTP_SERVER *ftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="be5af-550">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be5af-550">Description</span></span>

<span data-ttu-id="be5af-551">Bu hizmet daha önce oluşturulmuş ve başlatılmış bir FTP sunucu örneğini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="be5af-551">This service stops a previously created and started FTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="be5af-552">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="be5af-552">Input Parameters</span></span>

- <span data-ttu-id="be5af-553">**ftp_server_ptr**: FTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-553">**ftp_server_ptr**: Pointer to FTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="be5af-554">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="be5af-554">Return Values</span></span>

- <span data-ttu-id="be5af-555">**NX_SUCCESS**: (0x00) FTP sunucusu başarıyla durdu.</span><span class="sxs-lookup"><span data-stu-id="be5af-555">**NX_SUCCESS**: (0x00) Successful FTP Server stop.</span></span>
- <span data-ttu-id="be5af-556">NX_PTR_ERROR: (0x16) geçersiz FTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="be5af-556">NX_PTR_ERROR: (0x16) Invalid FTP pointer.</span></span>
- <span data-ttu-id="be5af-557">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="be5af-557">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="be5af-558">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="be5af-558">Allowed From</span></span>

<span data-ttu-id="be5af-559">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="be5af-559">Threads</span></span>

### <a name="example"></a><span data-ttu-id="be5af-560">Örnek</span><span class="sxs-lookup"><span data-stu-id="be5af-560">Example</span></span>

```c
/* Stop the FTP Server "my_server". */

status = nx_ftp_server_stop(&my_server);

/* If status is NX_SUCCESS, the FTP Server has been stopped. */
```
