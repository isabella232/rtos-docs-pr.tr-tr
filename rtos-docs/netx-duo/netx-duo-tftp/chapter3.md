---
title: Bölüm 3-Azure RTOS NetX Duo TFTP hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo TFTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 56f0d8edb991fff6ae30b6411e375ace58c544f7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825708"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-tftp-services"></a><span data-ttu-id="295b6-103">Bölüm 3-Azure RTOS NetX Duo TFTP hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="295b6-103">Chapter 3 - Description of Azure RTOS NetX Duo TFTP services</span></span>

<span data-ttu-id="295b6-104">Bu bölüm, tüm NetX Duo TFTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="295b6-104">This chapter contains a description of all NetX Duo TFTP services (listed below) in alphabetic order.</span></span> <span data-ttu-id="295b6-105">Aksi belirtilmediği takdirde, tüm hizmetler IPv6 ve IPv4 iletişimini destekler.</span><span class="sxs-lookup"><span data-stu-id="295b6-105">Unless otherwise specified, all services support IPv6 and IPv4 communications.</span></span>

<span data-ttu-id="295b6-106">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="295b6-106">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="295b6-107">**nxd_tftp_client_file_open**: *Açık TFTP istemci dosyası*</span><span class="sxs-lookup"><span data-stu-id="295b6-107">**nxd_tftp_client_file_open**: *Open TFTP client file*</span></span>

- <span data-ttu-id="295b6-108">**nxd_tftp_client_create**: *TFTP istemci örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="295b6-108">**nxd_tftp_client_create**: *Create a TFTP client instance*</span></span>

- <span data-ttu-id="295b6-109">**nxd_tftp_client_delete**: *TFTP istemci örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="295b6-109">**nxd_tftp_client_delete**: *Delete a TFTP client instance*</span></span>

- <span data-ttu-id="295b6-110">**nxd_tftp_client_error_info_get**: *istemci hata bilgilerini al*</span><span class="sxs-lookup"><span data-stu-id="295b6-110">**nxd_tftp_client_error_info_get**: *Get client error information*</span></span>

- <span data-ttu-id="295b6-111">**nxd_tftp_client_file_close**: *istemci dosyasını kapat*</span><span class="sxs-lookup"><span data-stu-id="295b6-111">**nxd_tftp_client_file_close**: *Close client file*</span></span>

- <span data-ttu-id="295b6-112">**nxd_tftp_client_file_open**: *istemci dosyasını aç*</span><span class="sxs-lookup"><span data-stu-id="295b6-112">**nxd_tftp_client_file_open**: *Open client file*</span></span>

- <span data-ttu-id="295b6-113">**nxd_tftp_client_file_read**: *istemci dosyasından bir blok oku*</span><span class="sxs-lookup"><span data-stu-id="295b6-113">**nxd_tftp_client_file_read**: *Read a block from client file*</span></span>

- <span data-ttu-id="295b6-114">**nxd_tftp_client_file_write**: *istemci dosyasına blok yaz*</span><span class="sxs-lookup"><span data-stu-id="295b6-114">**nxd_tftp_client_file_write**: *Write block to client file*</span></span>

- <span data-ttu-id="295b6-115">**nxd_tftp_client_packet_allocate**: *istemci dosyası yazma için paket ayır*</span><span class="sxs-lookup"><span data-stu-id="295b6-115">**nxd_tftp_client_packet_allocate**: *Allocate packet for client file write*</span></span>

- <span data-ttu-id="295b6-116">**nxd_tftp_client_set_interface**: *TFTP istekleri için fiziksel arabirimi ayarla*</span><span class="sxs-lookup"><span data-stu-id="295b6-116">**nxd_tftp_client_set_interface**: *Set the physical interface for TFTP requests*</span></span>

- <span data-ttu-id="295b6-117">**nxd_tftp_server_create**: *TFTP sunucusu oluşturma*</span><span class="sxs-lookup"><span data-stu-id="295b6-117">**nxd_tftp_server_create**: *Create TFTP server*</span></span>

- <span data-ttu-id="295b6-118">**nxd_tftp_server_delete**: *TFTP sunucusunu Sil*</span><span class="sxs-lookup"><span data-stu-id="295b6-118">**nxd_tftp_server_delete**: *Delete TFTP server*</span></span>

- <span data-ttu-id="295b6-119">**nxd_tftp_server_start**: *TFTP sunucusunu Başlat*</span><span class="sxs-lookup"><span data-stu-id="295b6-119">**nxd_tftp_server_start**: *Start TFTP server*</span></span>

- <span data-ttu-id="295b6-120">**nxd_tftp_server_stop**: *TFTP sunucusunu durdur*</span><span class="sxs-lookup"><span data-stu-id="295b6-120">**nxd_tftp_server_stop**: *Stop TFTP server*</span></span>

> [!NOTE] 
> <span data-ttu-id="295b6-121">Yukarıda listelenen tüm hizmetlerin IPv4 eşdeğerleri NetX Duo TFTP Istemcisinde ve sunucu gibi *nx_tftp_server_create* ve *nx_tftp_client_file_open* kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="295b6-121">The IPv4 equivalents of all the services listed above are available in NetX Duo TFTP Client and Server e.g. *nx_tftp_server_create* and *nx_tftp_client_file_open*.</span></span> <span data-ttu-id="295b6-122">Aşağıdaki sayfalarda yalnızca ' Duo ' API açıklamaları, örneğin *nxd_* ile başlayan hizmetler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="295b6-122">Only the ‘Duo’ API descriptions, e.g. services beginning with *nxd_*, are provided in the following pages.</span></span> <span data-ttu-id="295b6-123">NXD_ADDRESS \* girişi belirtildiğinde, IPv4 EŞDEĞERI API, ulong girişi için çağırır.</span><span class="sxs-lookup"><span data-stu-id="295b6-123">Where an NXD_ADDRESS \* input is specified, the IPv4 equivalent API calls for ULONG input.</span></span> <span data-ttu-id="295b6-124">Aksi takdirde, API 'nin kullanılması fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="295b6-124">Otherwise there is no difference in using the API.</span></span>

## <a name="nxd_tftp_client_create"></a><span data-ttu-id="295b6-125">nxd_tftp_client_create</span><span class="sxs-lookup"><span data-stu-id="295b6-125">nxd_tftp_client_create</span></span>

<span data-ttu-id="295b6-126">TFTP Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="295b6-126">Create a TFTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-127">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-127">Prototype</span></span>

```C
UINT nxd_tftp_client_create(NX_TFTP_CLIENT *tftp_client_ptr,  
     CHAR *tftp_client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="295b6-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-128">Description</span></span>

<span data-ttu-id="295b6-129">Bu hizmet, daha önce oluşturulan IP örneği için bir TFTP Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="295b6-129">This service creates a TFTP Client instance for the previously created IP instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="295b6-130">Uygulama, sağlanan IP ve paket havuzunun daha önce oluşturulduğundan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="295b6-130">The application must make certain the supplied IP and packet pool are already created.</span></span> <span data-ttu-id="295b6-131">Buna ek olarak, bu hizmet çağrılmadan önce IP örneği için UDP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="295b6-131">In addition, UDP must be enabled for the IP instance prior to calling this service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-132">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-132">Input Parameters</span></span>

- <span data-ttu-id="295b6-133">**tftp_client_ptr** TFTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-133">**tftp_client_ptr** Pointer to TFTP Client control block.</span></span>

- <span data-ttu-id="295b6-134">**tftp_client_name** Bu TFTP Istemci örneğinin adı</span><span class="sxs-lookup"><span data-stu-id="295b6-134">**tftp_client_name** Name of this TFTP Client instance</span></span>

- <span data-ttu-id="295b6-135">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="295b6-135">**ip_ptr** Pointer to previously created IP instance.</span></span>

- <span data-ttu-id="295b6-136">**pool_ptr** Paket havuzu TFTP Istemci örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-136">**pool_ptr** Pointer to packet pool TFTP Client instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-137">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-137">Return Values</span></span>

- <span data-ttu-id="295b6-138">**NX_SUCCESS**(0x00) başarılı TFTP oluşturma.</span><span class="sxs-lookup"><span data-stu-id="295b6-138">**NX_SUCCESS**(0x00) Successful TFTP create.</span></span>

- <span data-ttu-id="295b6-139">**NX_TFTP_INVALID_IP_VERSION** (0x0C) geçersiz veya desteklenmeyen IP sürümü</span><span class="sxs-lookup"><span data-stu-id="295b6-139">**NX_TFTP_INVALID_IP_VERSION** (0x0C) Invalid or unsupported IP version</span></span>

- <span data-ttu-id="295b6-140">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) GEÇERSIZ sunucu IP adresi alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-140">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Invalid Server IP address received</span></span>

- <span data-ttu-id="295b6-141">**NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucu onayı alınmadı</span><span class="sxs-lookup"><span data-stu-id="295b6-141">**NX_TFTP_NO_ACK_RECEIVED** (0x09) Server ACK not received</span></span>

- <span data-ttu-id="295b6-142">NX_PTR_ERROR (0x16) geçersiz IP, havuz veya TFTP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-142">NX_PTR_ERROR (0x16) Invalid IP, pool, or TFTP pointer.</span></span>

- <span data-ttu-id="295b6-143">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="295b6-143">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

- <span data-ttu-id="295b6-144">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="295b6-144">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-145">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-145">Allowed From</span></span>

<span data-ttu-id="295b6-146">Başlatma ve Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-146">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-147">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-147">Example</span></span>

```C
/* Create a TFTP Client instance. */
status =  nxd_tftp_client_create(&my_tftp_client, “My TFTP Client”, 
                                                    &my_ip, &pool_ptr);

/* If status is NX_SUCCESS a TFTP Client instance was successfully
   created. */
```

## <a name="nxd_tftp_client_delete"></a><span data-ttu-id="295b6-148">nxd_tftp_client_delete</span><span class="sxs-lookup"><span data-stu-id="295b6-148">nxd_tftp_client_delete</span></span>

<span data-ttu-id="295b6-149">TFTP Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="295b6-149">Delete a TFTP Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-150">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-150">Prototype</span></span>

```C
UINT nxd_tftp_client_delete(NX_TFTP_CLIENT *tftp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="295b6-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-151">Description</span></span>

<span data-ttu-id="295b6-152">Bu hizmet, daha önce oluşturulmuş bir TFTP Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="295b6-152">This service deletes a previously created TFTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-153">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-153">Input Parameters</span></span>

- <span data-ttu-id="295b6-154">**tftp_client_ptr** Daha önce oluşturulan TFTP istemci örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="295b6-154">**tftp_client_ptr** Pointer to previously created TFTP client instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-155">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-155">Return Values</span></span>

- <span data-ttu-id="295b6-156">**NX_SUCCESS** (0x00) başarılı TFTP istemcisi silme.</span><span class="sxs-lookup"><span data-stu-id="295b6-156">**NX_SUCCESS** (0x00) Successful TFTP Client delete.</span></span>

- <span data-ttu-id="295b6-157">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-157">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-158">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="295b6-158">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-159">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-159">Allowed From</span></span>

<span data-ttu-id="295b6-160">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-160">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-161">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-161">Example</span></span>

```C
/* Delete a TFTP Client instance. */
status =  nxd_tftp_client_delete(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP Client instance was successfully
   deleted. */
```

## <a name="nxd_tftp_client_error_info_get"></a><span data-ttu-id="295b6-162">nxd_tftp_client_error_info_get</span><span class="sxs-lookup"><span data-stu-id="295b6-162">nxd_tftp_client_error_info_get</span></span>

<span data-ttu-id="295b6-163">İstemci hata bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="295b6-163">Get client error information</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-164">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-164">Prototype</span></span>

```C
UINT nxd_tftp_client_error_info_get(NX_TFTP_CLIENT *tftp_client_ptr,
                        UINT *error_code, CHAR **error_string);
```

### <a name="description"></a><span data-ttu-id="295b6-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-165">Description</span></span>

<span data-ttu-id="295b6-166">Bu hizmet, alınan son hata kodunu döndürür ve işaretçiyi istemcinin iç hata dizesine ayarlar.</span><span class="sxs-lookup"><span data-stu-id="295b6-166">This service returns the last error code received and sets the pointer to the client’s internal error string.</span></span> <span data-ttu-id="295b6-167">Hata koşullarında, Kullanıcı sunucu tarafından gönderilen son hatayı görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="295b6-167">In error conditions, the user can view the last error sent by the server.</span></span> <span data-ttu-id="295b6-168">Null hata dizesi bir hata olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="295b6-168">A null error string indicates no error is present.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-169">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-169">Input Parameters</span></span>

- <span data-ttu-id="295b6-170">**tftp_client_ptr** Daha önce oluşturulan TFTP Istemci örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="295b6-170">**tftp_client_ptr** Pointer to previously created TFTP Client instance.</span></span>

- <span data-ttu-id="295b6-171">**error_code** Hata kodu için hedef alan işaretçisi</span><span class="sxs-lookup"><span data-stu-id="295b6-171">**error_code** Pointer to destination area for error code</span></span>

- <span data-ttu-id="295b6-172">**error_string** Hata dizesi için hedef işaretçisi</span><span class="sxs-lookup"><span data-stu-id="295b6-172">**error_string** Pointer to destination for error string</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-173">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-173">Return Values</span></span>

- <span data-ttu-id="295b6-174">**NX_SUCCESS** (0x00) başarılı TFTP hata bilgileri al.</span><span class="sxs-lookup"><span data-stu-id="295b6-174">**NX_SUCCESS** (0x00) Successful TFTP error info get.</span></span>  

- <span data-ttu-id="295b6-175">NX_PTR_ERROR (0x16) geçersiz TFTP Istemci işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-175">NX_PTR_ERROR (0x16) Invalid TFTP Client pointer.</span></span>

- <span data-ttu-id="295b6-176">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="295b6-176">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-177">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-177">Allowed From</span></span>

<span data-ttu-id="295b6-178">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-178">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-179">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-179">Example</span></span>

```C
/* Get error information for client. */
status =  nxd_tftp_client_error_info_get(&my_tftp_client, &error_code,
                    &error_string_ptr);

/* If status is NX_SUCCESS the error code and error string are available. */
```

## <a name="nxd_tftp_client_file_close"></a><span data-ttu-id="295b6-180">nxd_tftp_client_file_close</span><span class="sxs-lookup"><span data-stu-id="295b6-180">nxd_tftp_client_file_close</span></span>

<span data-ttu-id="295b6-181">İstemci dosyasını kapat</span><span class="sxs-lookup"><span data-stu-id="295b6-181">Close client file</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-182">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-182">Prototype</span></span>

```C
UINT nxd_tftp_client_file_close(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="295b6-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-183">Description</span></span>

<span data-ttu-id="295b6-184">Bu hizmet, bu TFTP Istemci örneği tarafından daha önce açılmış dosyayı kapatır.</span><span class="sxs-lookup"><span data-stu-id="295b6-184">This service closes the previously opened file by this TFTP Client instance.</span></span> <span data-ttu-id="295b6-185">Bir TFTP Istemci örneğinin aynı anda yalnızca bir dosya açmasına izin verilir.</span><span class="sxs-lookup"><span data-stu-id="295b6-185">A TFTP Client instance is allowed to have only one file open at a time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-186">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-186">Input Parameters</span></span>

- <span data-ttu-id="295b6-187">**tftp_client_ptr** Daha önce oluşturulan TFTP Istemci örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="295b6-187">**tftp_client_ptr** Pointer to previously created TFTP Client instance.</span></span>

- <span data-ttu-id="295b6-188">**ip_type** Hangi IP protokolünün kullanılacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="295b6-188">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="295b6-189">Geçerli seçenekler IPv4 (4) veya IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="295b6-189">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-190">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-190">Return Values</span></span>

- <span data-ttu-id="295b6-191">**NX_SUCCESS** (0x00) başarılı TFTP dosyası kapatma.</span><span class="sxs-lookup"><span data-stu-id="295b6-191">**NX_SUCCESS** (0x00) Successful TFTP file close.</span></span>

- <span data-ttu-id="295b6-192">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-192">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-193">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="295b6-193">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="295b6-194">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-194">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-195">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-195">Allowed From</span></span>

<span data-ttu-id="295b6-196">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-196">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-197">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-197">Example</span></span>

```C
/* Close the previously opened file associated with “my_client”. */
status =  nxd_tftp_client_file_close(&my_tftp_client);

/* If status is NX_SUCCESS the TFTP file is closed. */
```

## <a name="nx_tftp_client_file_open"></a><span data-ttu-id="295b6-198">nx_tftp_client_file_open</span><span class="sxs-lookup"><span data-stu-id="295b6-198">nx_tftp_client_file_open</span></span>

<span data-ttu-id="295b6-199">TFTP istemci dosyasını aç</span><span class="sxs-lookup"><span data-stu-id="295b6-199">Open TFTP client file</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-200">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-200">Prototype</span></span>

```C
UINT nx_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr, 
            CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
            open_type, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="295b6-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-201">Description</span></span>

<span data-ttu-id="295b6-202">Bu hizmet belirtilen IP adresindeki TFTP sunucusunda belirtilen dosyayı açmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="295b6-202">This service attempts to open the specified file on the TFTP Server at the specified IP address.</span></span> <span data-ttu-id="295b6-203">Dosya okuma ya da yazma için açılacak.</span><span class="sxs-lookup"><span data-stu-id="295b6-203">The file will be opened for either reading or writing.</span></span> 

> [!NOTE] 
> <span data-ttu-id="295b6-204">Bu yalnızca IPv4 paketleriyle sınırlıdır ve NetX TFTP uygulamalarını desteklemeye yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="295b6-204">This is limited to IPv4 packets only, and is intended for supporting NetX TFTP applications.</span></span> <span data-ttu-id="295b6-205">Geliştiricilere, eşdeğer "Duo" hizmet nxd_tftp_client_file_open kullanmak için uygulamalarının bağlantı noktası kullanmaları önerilir *.*</span><span class="sxs-lookup"><span data-stu-id="295b6-205">Developers are encouraged to port their applications to using equivalent “duo” service *nxd_tftp_client_file_open.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-206">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-206">Input Parameters</span></span>

- <span data-ttu-id="295b6-207">**tftp_client_ptr** TFTP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-207">**tftp_client_ptr** Pointer to TFTP control block.</span></span>

- <span data-ttu-id="295b6-208">**file_name** ASCII dosya adı, NULL ile sonlandırılmış ve uygun yol bilgileri.</span><span class="sxs-lookup"><span data-stu-id="295b6-208">**file_name** ASCII file name, NULL-terminated and with appropriate path information.</span></span>

- <span data-ttu-id="295b6-209">**server_ip_address** Sunucu TFTP adresi.</span><span class="sxs-lookup"><span data-stu-id="295b6-209">**server_ip_address** Server TFTP address.</span></span>

- <span data-ttu-id="295b6-210">**open_type** Açık istek türü, aşağıdakilerden biri:</span><span class="sxs-lookup"><span data-stu-id="295b6-210">**open_type** Type of open request, either:</span></span>

  <span data-ttu-id="295b6-211">**NX_TFTP_OPEN_FOR_READ** (0x01)</span><span class="sxs-lookup"><span data-stu-id="295b6-211">**NX_TFTP_OPEN_FOR_READ** (0x01)</span></span>

  <span data-ttu-id="295b6-212">**NX_TFTP_OPEN_FOR_WRITE** (0x02)</span><span class="sxs-lookup"><span data-stu-id="295b6-212">**NX_TFTP_OPEN_FOR_WRITE** (0x02)</span></span>

- <span data-ttu-id="295b6-213">**wait_option** Hizmetin TFTP Istemci dosyasını açma süresini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="295b6-213">**wait_option** Defines how long the service will wait for the TFTP Client file open.</span></span> <span data-ttu-id="295b6-214">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="295b6-214">The wait options are defined as follows:</span></span>

  <span data-ttu-id="295b6-215">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="295b6-215">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="295b6-216">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="295b6-216">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span> 
  
  <span data-ttu-id="295b6-217">TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının bir TFTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="295b6-217">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a TFTP Server responds to the request.</span></span> 
  
  <span data-ttu-id="295b6-218">Sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, TFTP sunucu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="295b6-218">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the TFTP server response.</span></span>

- <span data-ttu-id="295b6-219">**ip_type** Hangi IP protokolünün kullanılacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="295b6-219">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="295b6-220">Geçerli seçenekler IPv4 (4) veya IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="295b6-220">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-221">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-221">Return Values</span></span>

- <span data-ttu-id="295b6-222">**NX_SUCCESS** (0x00) Istemci dosyası başarıyla açıldı</span><span class="sxs-lookup"><span data-stu-id="295b6-222">**NX_SUCCESS** (0x00) Successful Client file open</span></span>

- <span data-ttu-id="295b6-223">**NX_TFTP_NOT_CLOSED** (0xC3) istemcisinde zaten dosya açık</span><span class="sxs-lookup"><span data-stu-id="295b6-223">**NX_TFTP_NOT_CLOSED** (0xC3) Client already has file open</span></span>

- <span data-ttu-id="295b6-224">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-224">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="295b6-225">**NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucudan ACK alınmadı</span><span class="sxs-lookup"><span data-stu-id="295b6-225">**NX_TFTP_NO_ACK_RECEIVED** (0x09) No ACK received from server</span></span>

- <span data-ttu-id="295b6-226">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) geçersiz sunucu IP 'si alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-226">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Invalid Server IP received</span></span>

- <span data-ttu-id="295b6-227">**NX_TFTP_CODE_ERROR** (0x05) alınan hata kodu</span><span class="sxs-lookup"><span data-stu-id="295b6-227">**NX_TFTP_CODE_ERROR** (0x05) Received error code</span></span>

- <span data-ttu-id="295b6-228">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-228">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-229">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="295b6-229">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="295b6-230">NX_IP_ADDRESS_ERROR (0x21) geçersiz sunucu IP adresi</span><span class="sxs-lookup"><span data-stu-id="295b6-230">NX_IP_ADDRESS_ERROR (0x21) Invalid Server IP address</span></span>

- <span data-ttu-id="295b6-231">NX_OPTION_ERROR (0x0A) geçersiz açık tür</span><span class="sxs-lookup"><span data-stu-id="295b6-231">NX_OPTION_ERROR (0x0A) Invalid open type</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-232">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-232">Allowed From</span></span>

<span data-ttu-id="295b6-233">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-233">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-234">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-234">Example</span></span>

```C
/* Define the TFTP server address. */
NXD_ADDRESS server_ip_address;

server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server _ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server _ip_address.nxd_ip_address.v6[1] = 0xf101;
server _ip_address.nxd_ip_address.v6[2] = 0;
server _ip_address.nxd_ip_address.v6[3] = 0x101;

/* Open file “test.txt” for reading on the TFTP Server. */
status =  nxd_tftp_client_file_open(&my_tftp_client, “test.txt”,
        & server_ip_address, NX_TFTP_OPEN_FOR_READ, 200);

/* If status is NX_SUCCESS the “test.txt” file is now open for reading. */
```

## <a name="nxd_tftp_client_file_open"></a><span data-ttu-id="295b6-235">nxd_tftp_client_file_open</span><span class="sxs-lookup"><span data-stu-id="295b6-235">nxd_tftp_client_file_open</span></span>

<span data-ttu-id="295b6-236">TFTP istemci dosyasını aç</span><span class="sxs-lookup"><span data-stu-id="295b6-236">Open TFTP client file</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-237">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-237">Prototype</span></span>

```C
UINT nxd_tftp_client_file_open(NX_TFTP_CLIENT *tftp_client_ptr,
        CHAR *file_name, NXD_ADDRESS *server_ip_address, UINT 
        open_type, ULONG wait_option, UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="295b6-238">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-238">Description</span></span>

<span data-ttu-id="295b6-239">Bu hizmet, belirtilen bir IPv6 adresinde belirtilen dosyayı TFTP sunucusunda açmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="295b6-239">This service attempts to open the specified file on the TFTP Server at the specified IPv6 address.</span></span> <span data-ttu-id="295b6-240">Dosya okuma ya da yazma için açılacak.</span><span class="sxs-lookup"><span data-stu-id="295b6-240">The file will be opened for either reading or writing.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-241">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-241">Input Parameters</span></span>

- <span data-ttu-id="295b6-242">**tftp_client_ptr** TFTP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-242">**tftp_client_ptr** Pointer to TFTP control block.</span></span>

- <span data-ttu-id="295b6-243">**file_name** ASCII dosya adı, NULL ile sonlandırılmış ve uygun yol bilgileri.</span><span class="sxs-lookup"><span data-stu-id="295b6-243">**file_name** ASCII file name, NULL-terminated and with appropriate path information.</span></span>

- <span data-ttu-id="295b6-244">**server_ip_address** Sunucu TFTP adresi.</span><span class="sxs-lookup"><span data-stu-id="295b6-244">**server_ip_address** Server TFTP address.</span></span>

- <span data-ttu-id="295b6-245">**open_type** Açık istek türü, aşağıdakilerden biri:</span><span class="sxs-lookup"><span data-stu-id="295b6-245">**open_type** Type of open request, either:</span></span>

  <span data-ttu-id="295b6-246">**NX_TFTP_OPEN_FOR_READ** (0x01)</span><span class="sxs-lookup"><span data-stu-id="295b6-246">**NX_TFTP_OPEN_FOR_READ** (0x01)</span></span>

  <span data-ttu-id="295b6-247">**NX_TFTP_OPEN_FOR_WRITE** (0x02)</span><span class="sxs-lookup"><span data-stu-id="295b6-247">**NX_TFTP_OPEN_FOR_WRITE** (0x02)</span></span>

- <span data-ttu-id="295b6-248">**wait_option** Hizmetin TFTP Istemci dosyasını açma süresini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="295b6-248">**wait_option** Defines how long the service will wait for the TFTP Client file open.</span></span> <span data-ttu-id="295b6-249">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="295b6-249">The wait options are defined as follows:</span></span>

  <span data-ttu-id="295b6-250">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="295b6-250">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="295b6-251">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="295b6-251">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

  <span data-ttu-id="295b6-252">TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının bir TFTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="295b6-252">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a TFTP Server responds to the request.</span></span>

  <span data-ttu-id="295b6-253">Sayısal bir değer (1-0xFFFFFFFE) seçildiğinde, TFTP sunucu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="295b6-253">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the TFTP server response.</span></span>

- <span data-ttu-id="295b6-254">**ip_type** Hangi IP protokolünün kullanılacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="295b6-254">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="295b6-255">Geçerli seçenekler IPv4 (4) veya IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="295b6-255">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-256">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-256">Return Values</span></span>

- <span data-ttu-id="295b6-257">**NX_SUCCESS** (0x00) Istemci dosyası başarıyla açıldı</span><span class="sxs-lookup"><span data-stu-id="295b6-257">**NX_SUCCESS** (0x00) Successful Client file open</span></span>

- <span data-ttu-id="295b6-258">**NX_TFTP_NOT_CLOSED** (0xC3) istemcisinde zaten dosya açık</span><span class="sxs-lookup"><span data-stu-id="295b6-258">**NX_TFTP_NOT_CLOSED** (0xC3) Client already has file open</span></span>

- <span data-ttu-id="295b6-259">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-259">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="295b6-260">**NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucudan ACK alınmadı</span><span class="sxs-lookup"><span data-stu-id="295b6-260">**NX_TFTP_NO_ACK_RECEIVED** (0x09) No ACK received from server</span></span>

- <span data-ttu-id="295b6-261">**NX_TFTP_INVALID_IP_VERSION** (0x0C) geçersiz IP sürümü</span><span class="sxs-lookup"><span data-stu-id="295b6-261">**NX_TFTP_INVALID_IP_VERSION** (0x0C) Invalid IP version</span></span>

- <span data-ttu-id="295b6-262">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) geçersiz sunucu IP 'si alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-262">**NX_TFTP_INVALID_SERVER_ADDRESS** (0x08) Invalid Server IP received</span></span>

- <span data-ttu-id="295b6-263">**NX_TFTP_CODE_ERROR** (0x05) alınan hata kodu</span><span class="sxs-lookup"><span data-stu-id="295b6-263">**NX_TFTP_CODE_ERROR** (0x05) Received error code</span></span>

- <span data-ttu-id="295b6-264">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-264">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-265">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="295b6-265">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="295b6-266">NX_IP_ADDRESS_ERROR (0x21) geçersiz sunucu IP adresi</span><span class="sxs-lookup"><span data-stu-id="295b6-266">NX_IP_ADDRESS_ERROR (0x21) Invalid Server IP address</span></span>

- <span data-ttu-id="295b6-267">NX_OPTION_ERROR (0x0A) geçersiz açık tür</span><span class="sxs-lookup"><span data-stu-id="295b6-267">NX_OPTION_ERROR (0x0A) Invalid open type</span></span>

- <span data-ttu-id="295b6-268">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="295b6-268">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-269">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-269">Allowed From</span></span>

<span data-ttu-id="295b6-270">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-270">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-271">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-271">Example</span></span>

```C
/* Define the TFTP server address. */
NXD_ADDRESS server_ip_address;

server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server _ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server _ip_address.nxd_ip_address.v6[1] = 0xf101;
server _ip_address.nxd_ip_address.v6[2] = 0;
server _ip_address.nxd_ip_address.v6[3] = 0x101;

/* Open file “test.txt” for reading on the TFTP Server. */
status =  nxd_tftp_client_file_open(&my_tftp_client, “test.txt”,
                & server_ip_address, NX_TFTP_OPEN_FOR_READ, 200);

/* If status is NX_SUCCESS the “test.txt” file is now open for reading. */
```

## <a name="nxd_tftp_client_file_read"></a><span data-ttu-id="295b6-272">nxd_tftp_client_file_read</span><span class="sxs-lookup"><span data-stu-id="295b6-272">nxd_tftp_client_file_read</span></span>

<span data-ttu-id="295b6-273">İstemci dosyasından bir blok oku</span><span class="sxs-lookup"><span data-stu-id="295b6-273">Read a block from client file</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-274">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-274">Prototype</span></span>

```C
UINT nxd_tftp_client_file_read(NX_TFTP_CLIENT *tftp_client_ptr,
                        NX_PACKET **packet_ptr, ULONG wait_option,
                        UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="295b6-275">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-275">Description</span></span>

<span data-ttu-id="295b6-276">Bu hizmet, daha önce açılan TFTP Istemci dosyasından 512 baytlık bir blok okur.</span><span class="sxs-lookup"><span data-stu-id="295b6-276">This service reads a 512-byte block from the previously opened TFTP Client file.</span></span> <span data-ttu-id="295b6-277">512 bayttan az bir blok içeren bir blok, dosyanın sonuna işaret eder.</span><span class="sxs-lookup"><span data-stu-id="295b6-277">A block containing fewer than 512 bytes signals the end of the file.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-278">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-278">Input Parameters</span></span>

- <span data-ttu-id="295b6-279">**tftp_client_ptr** TFTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-279">**tftp_client_ptr** Pointer to TFTP Client control block.</span></span>

- <span data-ttu-id="295b6-280">**packet_ptr** Dosyadan okunan blok içeren paket hedefi.</span><span class="sxs-lookup"><span data-stu-id="295b6-280">**packet_ptr** Destination for packet containing the block read from the file.</span></span>

- <span data-ttu-id="295b6-281">**wait_option** Hizmetin okuma işleminin tamamlanmasını bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="295b6-281">**wait_option** Defines how long the service will wait for the read to complete.</span></span> <span data-ttu-id="295b6-282">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="295b6-282">The wait options are defined as follows:</span></span>

  <span data-ttu-id="295b6-283">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="295b6-283">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="295b6-284">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="295b6-284">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

  <span data-ttu-id="295b6-285">TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının, TFTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="295b6-285">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the TFTP Server responds to the request.</span></span>

  <span data-ttu-id="295b6-286">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, TFTP sunucusunun dosya bloğunu göndermesini beklerken askıya alınması için beklenecek en fazla Zamanlayıcı sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="295b6-286">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the TFTP server to send a block of the file.</span></span>

- <span data-ttu-id="295b6-287">**ip_type** Hangi IP protokolünün kullanılacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="295b6-287">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="295b6-288">Geçerli seçenekler IPv4 (4) veya IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="295b6-288">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-289">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-289">Return Values</span></span>

- <span data-ttu-id="295b6-290">**NX_SUCCESS** (0x00) başarılı istemci bloğu okuma</span><span class="sxs-lookup"><span data-stu-id="295b6-290">**NX_SUCCESS** (0x00) Successful Client block read</span></span>

- <span data-ttu-id="295b6-291">**NX_TFTP_NOT_OPEN** (0xC3) belirtilen istemci dosyası okuma için açık değil</span><span class="sxs-lookup"><span data-stu-id="295b6-291">**NX_TFTP_NOT_OPEN** (0xC3) Specified Client file is not open for reading</span></span>

- <span data-ttu-id="295b6-292">**NX_NO_PACKET** (0x01) sunucudan paket alınmadı.</span><span class="sxs-lookup"><span data-stu-id="295b6-292">**NX_NO_PACKET** (0x01) No Packet received from Server.</span></span>

- <span data-ttu-id="295b6-293">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-293">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="295b6-294">**NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucudan ACK alınmadı</span><span class="sxs-lookup"><span data-stu-id="295b6-294">**NX_TFTP_NO_ACK_RECEIVED** (0x09) No ACK received from Server</span></span>

- <span data-ttu-id="295b6-295">**NX_TFTP_END_OF_FILE** (0xC5) dosya sonu algılandı (hata değil).</span><span class="sxs-lookup"><span data-stu-id="295b6-295">**NX_TFTP_END_OF_FILE** (0xC5) End of file detected (not an error).</span></span>

- <span data-ttu-id="295b6-296">**NX_TFTP_INVALID_IP_VERSION** (0x0C) geçersiz IP sürümü</span><span class="sxs-lookup"><span data-stu-id="295b6-296">**NX_TFTP_INVALID_IP_VERSION** (0x0C) Invalid IP version</span></span>

- <span data-ttu-id="295b6-297">**NX_TFTP_CODE_ERROR** (0x05) alınan hata kodu</span><span class="sxs-lookup"><span data-stu-id="295b6-297">**NX_TFTP_CODE_ERROR** (0x05) Received error code</span></span>

- <span data-ttu-id="295b6-298">**NX_TFTP_FAILED** (0xC2) bilinmeyen TFTP kodu alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-298">**NX_TFTP_FAILED** (0xC2) Unknown TFTP code received</span></span>

- <span data-ttu-id="295b6-299">**NX_TFTP_INVALID_BLOCK_NUMBER** (0X0a) geçersiz blok numarası alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-299">**NX_TFTP_INVALID_BLOCK_NUMBER** (0x0A) Invalid block number received</span></span>

- <span data-ttu-id="295b6-300">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-300">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-301">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="295b6-301">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="295b6-302">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="295b6-302">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-303">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-303">Allowed From</span></span>

<span data-ttu-id="295b6-304">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-304">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-305">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-305">Example</span></span>

```C
/* Read a block from a previously opened file of “my_client”. */
status =  nxd_tftp_client_file_read(&my_tftp_client, &return_packet_ptr, 200);

/* If status is NX_SUCCESS a block of the TFTP file is in the payload of
   “return_packet_ptr”. */
```

## <a name="nxd_tftp_client_file_write"></a><span data-ttu-id="295b6-306">nxd_tftp_client_file_write</span><span class="sxs-lookup"><span data-stu-id="295b6-306">nxd_tftp_client_file_write</span></span>

<span data-ttu-id="295b6-307">Istemci dosyasına bir blok yaz</span><span class="sxs-lookup"><span data-stu-id="295b6-307">Write a block to Client file</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-308">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-308">Prototype</span></span>

```C
UINT nxd_tftp_client_file_write(NX_TFTP_CLIENT *tftp_client_ptr,
            NX_PACKET *packet_ptr, ULONG wait_option, UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="295b6-309">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-309">Description</span></span>

<span data-ttu-id="295b6-310">Bu hizmet, daha önce açılmış olan TFTP Istemci dosyasına 512 baytlık bir blok yazar.</span><span class="sxs-lookup"><span data-stu-id="295b6-310">This service writes a 512-byte block to the previously opened TFTP Client file.</span></span> <span data-ttu-id="295b6-311">512 bayttan daha az bir blok belirtmek dosyanın sonuna işaret eder.</span><span class="sxs-lookup"><span data-stu-id="295b6-311">Specifying a block containing fewer than 512 bytes signals the end of the file.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-312">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-312">Input Parameters</span></span>

- <span data-ttu-id="295b6-313">**tftp_client_ptr** TFTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-313">**tftp_client_ptr** Pointer to TFTP Client control block.</span></span>

- <span data-ttu-id="295b6-314">**packet_ptr** Dosyaya yazılacak bloğu içeren paket.</span><span class="sxs-lookup"><span data-stu-id="295b6-314">**packet_ptr** Packet containing the block to write to the file.</span></span>

- <span data-ttu-id="295b6-315">**wait_option** Hizmetin yazma işleminin tamamlanmasını bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="295b6-315">**wait_option** Defines how long the service will wait for the write to complete.</span></span> <span data-ttu-id="295b6-316">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="295b6-316">The wait options are defined as follows:</span></span>

  <span data-ttu-id="295b6-317">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="295b6-317">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="295b6-318">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="295b6-318">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

  <span data-ttu-id="295b6-319">TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının, TFTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="295b6-319">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the TFTP Server responds to the request.</span></span>
 
  <span data-ttu-id="295b6-320">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, TFTP sunucusunun yazma isteği için bir ACK göndermesini beklerken askıya alınması için beklenecek en fazla Zamanlayıcı sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="295b6-320">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the TFTP server to send an ACK for the write request.</span></span>

- <span data-ttu-id="295b6-321">**ip_type** Hangi IP protokolünün kullanılacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="295b6-321">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="295b6-322">Geçerli seçenekler IPv4 (4) veya IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="295b6-322">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-323">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-323">Return Values</span></span>

- <span data-ttu-id="295b6-324">**NX_SUCCESS** (0x00) başarılı istemci blok yazma</span><span class="sxs-lookup"><span data-stu-id="295b6-324">**NX_SUCCESS** (0x00) Successful Client block write</span></span>

- <span data-ttu-id="295b6-325">**NX_TFTP_NOT_OPEN** (0xC3) belirtilen istemci dosyası yazma için açık değil</span><span class="sxs-lookup"><span data-stu-id="295b6-325">**NX_TFTP_NOT_OPEN** (0xC3) Specified Client file is not open for writing</span></span>

- <span data-ttu-id="295b6-326">**NX_TFTP_TIMEOUT** (0xC1) sunucu onayı beklenirken zaman aşımı oluştu</span><span class="sxs-lookup"><span data-stu-id="295b6-326">**NX_TFTP_TIMEOUT** (0xC1) Timeout waiting for Server ACK</span></span>

- <span data-ttu-id="295b6-327">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-327">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="295b6-328">**NX_TFTP_NO_ACK_RECEIVED** (0x09) sunucudan ACK alınmadı</span><span class="sxs-lookup"><span data-stu-id="295b6-328">**NX_TFTP_NO_ACK_RECEIVED** (0x09) No ACK received from server</span></span>

- <span data-ttu-id="295b6-329">**NX_TFTP_INVALID_IP_VERSION** (0x0C) geçersiz IP sürümü</span><span class="sxs-lookup"><span data-stu-id="295b6-329">**NX_TFTP_INVALID_IP_VERSION** (0x0C) Invalid IP version</span></span>

- <span data-ttu-id="295b6-330">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) geçersiz sunucu adresi alındı</span><span class="sxs-lookup"><span data-stu-id="295b6-330">**NX_INVALID_TFTP_SERVER_ADDRESS** (0x08) Invalid server address received</span></span>

- <span data-ttu-id="295b6-331">**NX_TFTP_CODE_ERROR** (0x05) alınan hata kodu</span><span class="sxs-lookup"><span data-stu-id="295b6-331">**NX_TFTP_CODE_ERROR** (0x05) Received error code</span></span>

- <span data-ttu-id="295b6-332">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-332">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-333">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="295b6-333">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="295b6-334">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="295b6-334">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-335">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-335">Allowed From</span></span>

<span data-ttu-id="295b6-336">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-336">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-337">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-337">Example</span></span>

```C
/* Write a block to the previously opened file of “my_client”. */
status =  nxd_tftp_client_file_write(&my_tftp_client, packet_ptr, 200);

/* If status is NX_SUCCESS the block in the payload of “packet_ptr” was 
   written to the TFTP file opened by “my_client”. */
```

## <a name="nxd_tftp_client_packet_allocate"></a><span data-ttu-id="295b6-338">nxd_tftp_client_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="295b6-338">nxd_tftp_client_packet_allocate</span></span>

<span data-ttu-id="295b6-339">Istemci dosyası yazma için paket ayır</span><span class="sxs-lookup"><span data-stu-id="295b6-339">Allocate packet for Client file write</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-340">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-340">Prototype</span></span>

```C
UINT nxd_tftp_client_packet_allocate(NX_PACKET_POOL *pool_ptr,
                        NX_PACKET **packet_ptr, ULONG wait_option,
                        UINT ip_type);
```

### <a name="description"></a><span data-ttu-id="295b6-341">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-341">Description</span></span>

<span data-ttu-id="295b6-342">Bu hizmet, belirtilen paket havuzundan bir UDP paketi ayırır ve paket çağırana döndürülmeden önce 4 baytlık TFTP üst bilgisine yer açar.</span><span class="sxs-lookup"><span data-stu-id="295b6-342">This service allocates a UDP packet from the specified packet pool and makes room for the 4-byte TFTP header before the packet is returned to the caller.</span></span> <span data-ttu-id="295b6-343">Çağıran daha sonra bir istemci dosyasına yazmak için bir arabellek oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="295b6-343">The caller can then build a buffer for writing to a client file.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-344">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-344">Input Parameters</span></span>

- <span data-ttu-id="295b6-345">**pool_ptr** Paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-345">**pool_ptr** Pointer to packet pool.</span></span>

- <span data-ttu-id="295b6-346">**packet_ptr** Ayrılmış pakete işaretçinin hedefi.</span><span class="sxs-lookup"><span data-stu-id="295b6-346">**packet_ptr** Destination for pointer to allocated packet.</span></span>

- <span data-ttu-id="295b6-347">**wait_option** Hizmetin paket ayırma işleminin tamamlanmasını ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="295b6-347">**wait_option** Defines how long the service will wait for the packet allocate to complete.</span></span> <span data-ttu-id="295b6-348">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="295b6-348">The wait options are defined as follows:</span></span>

  <span data-ttu-id="295b6-349">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="295b6-349">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>

  <span data-ttu-id="295b6-350">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="295b6-350">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

  <span data-ttu-id="295b6-351">TX_WAIT_FOREVER seçilmesi çağıran iş parçacığının ayırma tamamlanana kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="295b6-351">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the allocation completes.</span></span>

  <span data-ttu-id="295b6-352">Sayısal bir değer (1-0xFFFFFFFE) seçilmesi, paket ayırmayı beklerken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="295b6-352">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the packet allocation.</span></span>

- <span data-ttu-id="295b6-353">**ip_type** Hangi IP protokolünün kullanılacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="295b6-353">**ip_type** Indicate which IP protocol to use.</span></span> <span data-ttu-id="295b6-354">Geçerli seçenekler IPv4 (4) veya IPv6 (6).</span><span class="sxs-lookup"><span data-stu-id="295b6-354">Valid options are IPv4 (4) or IPv6 (6).</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-355">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-355">Return Values</span></span>

- <span data-ttu-id="295b6-356">**NX_SUCCESS** (0x00) başarılı paket ayırma</span><span class="sxs-lookup"><span data-stu-id="295b6-356">**NX_SUCCESS** (0x00) Successful packet allocate</span></span>

- <span data-ttu-id="295b6-357">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-357">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-358">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="295b6-358">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="295b6-359">NX_INVALID_PARAMETERS (0x4D) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="295b6-359">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-360">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-360">Allowed From</span></span>

<span data-ttu-id="295b6-361">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-361">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-362">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-362">Example</span></span>

```C
/* Allocate a packet for TFTP file write. */
status =  nxd_tftp_client_packet_allocate(&my_pool, &packet_ptr, 200);

/* If status is NX_SUCCESS “packet_ptr” contains the new packet. */
```

## <a name="nxd_tftp_client_set_interface"></a><span data-ttu-id="295b6-363">nxd_tftp_client_set_interface</span><span class="sxs-lookup"><span data-stu-id="295b6-363">nxd_tftp_client_set_interface</span></span>

<span data-ttu-id="295b6-364">TFTP istekleri için fiziksel arabirimi ayarla</span><span class="sxs-lookup"><span data-stu-id="295b6-364">Set physical interface for TFTP requests</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-365">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-365">Prototype</span></span>

```C
UINT nxd_tftp_client_set_interface(NX_TFTP_CLIENT *tftp_client_ptr,
                                    UINT if_index);
```

### <a name="description"></a><span data-ttu-id="295b6-366">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-366">Description</span></span>

<span data-ttu-id="295b6-367">Bu hizmet, TFTP Istemcisine yönelik fiziksel arabirimi TFTP paketleri gönderecek ve alacak şekilde ayarlamak için giriş arabirimi dizinini kullanır.</span><span class="sxs-lookup"><span data-stu-id="295b6-367">This service uses the input interface index to set the physical interface for the TFTP Client to send and receive TFTP packets.</span></span> <span data-ttu-id="295b6-368">Birincil arabirim için varsayılan değer sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="295b6-368">The default value is zero, for the primary interface.</span></span>

> [!NOTE]
> <span data-ttu-id="295b6-369">NetX Duo bu hizmeti kullanmak için çok ana adresleme 'yi (v 5.6 veya üzeri) desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="295b6-369">NetX Duo must support multihome addressing (v5.6 or later) to use this service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-370">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-370">Input Parameters</span></span>

- <span data-ttu-id="295b6-371">**tftp_client_ptr** TFTP Istemci örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="295b6-371">**tftp_client_ptr** Pointer to TFTP Client instance</span></span>

- <span data-ttu-id="295b6-372">**if_index** Kullanılacak fiziksel arabirimin dizini</span><span class="sxs-lookup"><span data-stu-id="295b6-372">**if_index** Index of physical interface to use</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-373">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-373">Return Values</span></span>

- <span data-ttu-id="295b6-374">**NX_SUCCESS** (0x00) arabirimi başarıyla ayarlandı (0X0b) geçersiz arabirim girişi</span><span class="sxs-lookup"><span data-stu-id="295b6-374">**NX_SUCCESS** (0x00) Successfully set interface (0x0B) Invalid interface input</span></span>

- <span data-ttu-id="295b6-375">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-375">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-376">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="295b6-376">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="295b6-377">NX_TFTP_INVALID_INTERFACE (0x0B) geçersiz arabirim girişi</span><span class="sxs-lookup"><span data-stu-id="295b6-377">NX_TFTP_INVALID_INTERFACE (0x0B) Invalid interface input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-378">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-378">Allowed From</span></span>

<span data-ttu-id="295b6-379">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-379">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-380">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-380">Example</span></span>

```C
/* Specify the primary interface for TFTP requests. */
status =  nxd_tftp_client_set_interface(&client, 0);

/* If status is NX_SUCCESS the primary interface will be use for TFTP communications. */
```

## <a name="nxd_tftp_server_create"></a><span data-ttu-id="295b6-381">nxd_tftp_server_create</span><span class="sxs-lookup"><span data-stu-id="295b6-381">nxd_tftp_server_create</span></span>

<span data-ttu-id="295b6-382">TFTP sunucusu oluştur</span><span class="sxs-lookup"><span data-stu-id="295b6-382">Create TFTP server</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-383">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-383">Prototype</span></span>

```C
UINT nxd_tftp_server_create(NX_TFTP_SERVER *tftp_server_ptr,
            CHAR *tftp_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr, 
            VOID *stack_ptr, ULONG stack_size,
            NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="295b6-384">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-384">Description</span></span>

<span data-ttu-id="295b6-385">Bu hizmet, 69 numaralı bağlantı noktasında TFTP Istemci isteklerine yanıt veren bir TFTP sunucusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="295b6-385">This service creates a TFTP Server that responds to TFTP Client requests on port 69.</span></span> <span data-ttu-id="295b6-386">Sunucunun *nxd_tftp_server_start* sonraki bir çağrısıyla başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="295b6-386">The Server must be started by a subsequent call to *nxd_tftp_server_start*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="295b6-387">Uygulama, sağlanan IP örneğinin, paket havuzunun ve FileX Medya örneğinin zaten oluşturulduğundan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="295b6-387">The application must make certain the supplied IP instance, packet pool, and FileX media instance are already created.</span></span> <span data-ttu-id="295b6-388">Buna ek olarak, bu hizmet çağrılmadan önce IP örneği için UDP 'nin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="295b6-388">In addition, UDP must be enabled for the IP instance prior to calling this service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-389">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-389">Input Parameters</span></span>

- <span data-ttu-id="295b6-390">**tftp_server_ptr** TFTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-390">**tftp_server_ptr** Pointer to TFTP Server control block.</span></span>

- <span data-ttu-id="295b6-391">**tftp_server_name** Bu TFTP sunucu örneğinin adı</span><span class="sxs-lookup"><span data-stu-id="295b6-391">**tftp_server_name** Name of this TFTP Server instance</span></span>

- <span data-ttu-id="295b6-392">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="295b6-392">**ip_ptr** Pointer to previously created IP instance.</span></span>

- <span data-ttu-id="295b6-393">**media_ptr** FileX medya örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="295b6-393">**media_ptr** Pointer to FileX media instance.</span></span>

- <span data-ttu-id="295b6-394">**stack_ptr** TFTP sunucusu yığın alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-394">**stack_ptr** Pointer to TFTP Server stack area.</span></span>

- <span data-ttu-id="295b6-395">**stack_size** TFTP sunucu yığınındaki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="295b6-395">**stack_size** Number of bytes in the TFTP Server stack.</span></span>

- <span data-ttu-id="295b6-396">**pool_ptr** TFTP paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-396">**pool_ptr** Pointer to TFTP packet pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="295b6-397">Sağlanan havuzun paket yükleri en az 580 bayt boyutunda olmalıdır. <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="295b6-397">The supplied pool must have packet payloads at least 580 bytes in size.<sup>1</sup></span></span>

<span data-ttu-id="295b6-398"><sup>1</sup> bir paketin veri bölümü tam olarak 512 bayttır, ancak paket yükü boyutu en az 572 bayt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="295b6-398"><sup>1</sup> The data portion of a packet is exactly 512 bytes, but the packet payload size must be at least 572 bytes.</span></span> <span data-ttu-id="295b6-399">Kalan bayt sayısı, UDP, IPv6 ve Ethernet üstbilgileri ve hizalama için sürücü için gereken olası sondaki baytlar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="295b6-399">The remaining bytes are used for the UDP, IPv6, and Ethernet headers and potential trailing bytes required by the driver for alignment.</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-400">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-400">Return Values</span></span>

- <span data-ttu-id="295b6-401">**NX_SUCCESS** (0x00) başarılı sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="295b6-401">**NX_SUCCESS** (0x00) Successful Server create</span></span>

- <span data-ttu-id="295b6-402">**NX_TFTP_POOL_ERROR** (0xC6) paket havuzunda 560 bayttan daha az paket boyutu vardır</span><span class="sxs-lookup"><span data-stu-id="295b6-402">**NX_TFTP_POOL_ERROR** (0xC6) Packet pool has packet size of less than 560 bytes</span></span>

- <span data-ttu-id="295b6-403">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-403">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-404">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-404">Allowed From</span></span>

<span data-ttu-id="295b6-405">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-405">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-406">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-406">Example</span></span>

```C
/* Create a TFTP Server called “my_server”. */
status =  nxd_tftp_server_create(&my_server, “My TFTP Server”, &server_ip, 
                &ram_disk, stack_ptr, 2048, pool_ptr);

/* If status is NX_SUCCESS the TFTP Server is created. */
```

## <a name="nxd_tftp_server_delete"></a><span data-ttu-id="295b6-407">nxd_tftp_server_delete</span><span class="sxs-lookup"><span data-stu-id="295b6-407">nxd_tftp_server_delete</span></span>

<span data-ttu-id="295b6-408">TFTP sunucusunu Sil</span><span class="sxs-lookup"><span data-stu-id="295b6-408">Delete TFTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-409">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-409">Prototype</span></span>

```C
UINT nxd_tftp_server_delete(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="295b6-410">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-410">Description</span></span>

<span data-ttu-id="295b6-411">Bu hizmet, daha önce oluşturulmuş bir TFTP sunucusunu siler.</span><span class="sxs-lookup"><span data-stu-id="295b6-411">This service deletes a previously created TFTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-412">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-412">Input Parameters</span></span>

- <span data-ttu-id="295b6-413">**tftp_server_ptr** TFTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-413">**tftp_server_ptr** Pointer to TFTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-414">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-414">Return Values</span></span>

- <span data-ttu-id="295b6-415">**NX_SUCCESS** (0x00) başarılı sunucu silme</span><span class="sxs-lookup"><span data-stu-id="295b6-415">**NX_SUCCESS** (0x00) Successful Server delete</span></span>

- <span data-ttu-id="295b6-416">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-416">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-417">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="295b6-417">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-418">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-418">Allowed From</span></span>

<span data-ttu-id="295b6-419">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-419">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-420">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-420">Example</span></span>

```C
/* Delete the TFTP Server called “my_server”. */
status =  nxd_tftp_server_delete(&my_server);

/* If status is NX_SUCCESS the TFTP Server is deleted. */
```

## <a name="nxd_tftp_server_start"></a><span data-ttu-id="295b6-421">nxd_tftp_server_start</span><span class="sxs-lookup"><span data-stu-id="295b6-421">nxd_tftp_server_start</span></span>

<span data-ttu-id="295b6-422">TFTP sunucusunu Başlat</span><span class="sxs-lookup"><span data-stu-id="295b6-422">Start TFTP server</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-423">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-423">Prototype</span></span>

```C
UINT nxd_tftp_server_start(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="295b6-424">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-424">Description</span></span>

<span data-ttu-id="295b6-425">Bu hizmet, önceden oluşturulan TFTP sunucusunu başlatır.</span><span class="sxs-lookup"><span data-stu-id="295b6-425">This service starts the previously created TFTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-426">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-426">Input Parameters</span></span>

- <span data-ttu-id="295b6-427">**tftp_server_ptr** TFTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-427">**tftp_server_ptr** Pointer to TFTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-428">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-428">Return Values</span></span>

- <span data-ttu-id="295b6-429">**NX_SUCCESS** (0x00) başarılı sunucu başlatması</span><span class="sxs-lookup"><span data-stu-id="295b6-429">**NX_SUCCESS** (0x00) Successful Server start</span></span>

- <span data-ttu-id="295b6-430">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-430">NX_PTR_ERROR (0x16) Invalid pointer input .</span></span>
 
### <a name="allowed-from"></a><span data-ttu-id="295b6-431">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-431">Allowed From</span></span>

<span data-ttu-id="295b6-432">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-432">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-433">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-433">Example</span></span>

```C
/* Start the TFTP Server called “my_server”. */
status =  nxd_tftp_server_start(&my_server);

/* If status is NX_SUCCESS the TFTP Server is started. */
```

## <a name="nxd_tftp_server_stop"></a><span data-ttu-id="295b6-434">nxd_tftp_server_stop</span><span class="sxs-lookup"><span data-stu-id="295b6-434">nxd_tftp_server_stop</span></span>

<span data-ttu-id="295b6-435">TFTP sunucusunu durdur</span><span class="sxs-lookup"><span data-stu-id="295b6-435">Stop TFTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="295b6-436">Prototype</span><span class="sxs-lookup"><span data-stu-id="295b6-436">Prototype</span></span>

```C
UINT nxd_tftp_server_stop(NX_TFTP_SERVER *tftp_server_ptr);
```

### <a name="description"></a><span data-ttu-id="295b6-437">Açıklama</span><span class="sxs-lookup"><span data-stu-id="295b6-437">Description</span></span>

<span data-ttu-id="295b6-438">Bu hizmet, daha önce oluşturulan TFTP sunucusunu durduruyor.</span><span class="sxs-lookup"><span data-stu-id="295b6-438">This service stops the previously created TFTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="295b6-439">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="295b6-439">Input Parameters</span></span>

- <span data-ttu-id="295b6-440">**tftp_server_ptr** TFTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="295b6-440">**tftp_server_ptr** Pointer to TFTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="295b6-441">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="295b6-441">Return Values</span></span>

- <span data-ttu-id="295b6-442">**NX_SUCCESS** (0x00) başarılı sunucu durdu</span><span class="sxs-lookup"><span data-stu-id="295b6-442">**NX_SUCCESS** (0x00) Successful Server stop</span></span>

- <span data-ttu-id="295b6-443">NX_PTR_ERROR (0x16) geçersiz işaretçi girişi.</span><span class="sxs-lookup"><span data-stu-id="295b6-443">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

- <span data-ttu-id="295b6-444">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="295b6-444">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="295b6-445">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="295b6-445">Allowed From</span></span>

<span data-ttu-id="295b6-446">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="295b6-446">Threads</span></span>

### <a name="example"></a><span data-ttu-id="295b6-447">Örnek</span><span class="sxs-lookup"><span data-stu-id="295b6-447">Example</span></span>

```C
/* Stop the TFTP Server called “my_server”. */
status =  nxd_tftp_server_stop(&my_server);

/* If status is NX_SUCCESS the TFTP Server is stopped. */
```