---
title: Bölüm 3-Azure RTOS NetX Duo HTTP hizmetlerinin açıklaması
description: Bu bölümde, aynı hizmetin ' NetX ' (yalnızca IPv4) eşdeğeri olarak eşleştirilmiş olması dışında tüm Azure RTOS NetX Duo HTTP Hizmetleri (aşağıda listelenmiştir) alfabetik sırada bir açıklama bulunur.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 703071cd5a1d0677a3e995fccfe35d8b1dbbd9f3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825967"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-http-services"></a><span data-ttu-id="86682-103">Bölüm 3-Azure RTOS NetX Duo HTTP hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="86682-103">Chapter 3 - Description of Azure RTOS NetX Duo HTTP Services</span></span>

<span data-ttu-id="86682-104">Bu bölümde, aynı hizmetin ' NetX ' (yalnızca IPv4) eşdeğeri olarak eşleştirilmiş olması dışında tüm Azure RTOS NetX Duo HTTP Hizmetleri (aşağıda listelenmiştir) alfabetik sırada bir açıklama bulunur.</span><span class="sxs-lookup"><span data-stu-id="86682-104">This chapter contains a description of all Azure RTOS NetX Duo HTTP services (listed below) in alphabetical order except for the ‘NetX’ (IPv4 only) equivalent of the same service are paired together).</span></span>

<span data-ttu-id="86682-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, KALıN olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="86682-105">In the “Return Values” section in the following API descriptions, values in BOLD are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

<span data-ttu-id="86682-106">**HTTP Istemci Hizmetleri:**</span><span class="sxs-lookup"><span data-stu-id="86682-106">**HTTP Client services:**</span></span>

- <span data-ttu-id="86682-107">**NX_HTTP_CLIENT_CREATE** *http istemci örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="86682-107">**nx_http_client_create** *Create an HTTP Client Instance*</span></span>
- <span data-ttu-id="86682-108"> *http istemci örneğini silme* nx_http_client_delete</span><span class="sxs-lookup"><span data-stu-id="86682-108">**nx_http_client_delete** *Delete an HTTP Client instance*</span></span>
- <span data-ttu-id="86682-109"> *http get isteği başlatmak Nx_http_client_get_start (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="86682-109">**nx_http_client_get_start** *Start an HTTP GET request (IPv4 only)*</span></span>
- <span data-ttu-id="86682-110"> *http get isteği başlatmak Nx_http_client_get_start_extended (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="86682-110">**nx_http_client_get_start_extended** *Start an HTTP GET request (IPv4 only)*</span></span>
- <span data-ttu-id="86682-111"> *http get isteği başlatma nxd_http_client_get_start (IPv4 veya IPv6)*</span><span class="sxs-lookup"><span data-stu-id="86682-111">**nxd_http_client_get_start** *Start an HTTP GET request (IPv4 or IPv6)*</span></span>
- <span data-ttu-id="86682-112"> *http get isteği başlatma nxd_http_client_get_start_extended (IPv4 veya IPv6)*</span><span class="sxs-lookup"><span data-stu-id="86682-112">**nxd_http_client_get_start_extended** *Start an HTTP GET request (IPv4 or IPv6)*</span></span>
- <span data-ttu-id="86682-113"> *sonraki kaynak veri paketini al* nx_http_client_get_packet</span><span class="sxs-lookup"><span data-stu-id="86682-113">**nx_http_client_get_packet** *Get next resource data packet*</span></span>
- <span data-ttu-id="86682-114"> *http put isteği başlatmak Nx_http_client_put_start (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="86682-114">**nx_http_client_put_start** *Start an HTTP PUT request (IPv4 only)*</span></span>
- <span data-ttu-id="86682-115"> *http put isteği başlatmak Nx_http_client_put_start_extended (yalnızca IPv4)*</span><span class="sxs-lookup"><span data-stu-id="86682-115">**nx_http_client_put_start_extended** *Start an HTTP PUT request (IPv4 only)*</span></span>
- <span data-ttu-id="86682-116"> *http put isteği başlatma nxd_http_client_put_start (IPv4 veya IPv6)*</span><span class="sxs-lookup"><span data-stu-id="86682-116">**nxd_http_client_put_start** *Start an HTTP PUT request (IPv4 or IPv6)*</span></span>
- <span data-ttu-id="86682-117"> *http put isteği başlatma nxd_http_client_put_start_extended (IPv4 veya IPv6)*</span><span class="sxs-lookup"><span data-stu-id="86682-117">**nxd_http_client_put_start_extended** *Start an HTTP PUT request (IPv4 or IPv6)*</span></span>
- <span data-ttu-id="86682-118"> *sonraki kaynak veri paketini nx_http_client_put_packet gönder*</span><span class="sxs-lookup"><span data-stu-id="86682-118">**nx_http_client_put_packet** *Send next resource data packet*</span></span>
- <span data-ttu-id="86682-119"> *http sunucusuna bağlanmak için bağlantı noktasını değiştirme* nx_http_client_set_connect_port</span><span class="sxs-lookup"><span data-stu-id="86682-119">**nx_http_client_set_connect_port** *Change the port to connect to the HTTP Server*</span></span>

<span data-ttu-id="86682-120">**HTTP sunucusu Hizmetleri:**</span><span class="sxs-lookup"><span data-stu-id="86682-120">**HTTP server services:**</span></span>

- <span data-ttu-id="86682-121"> *belirtilen URL 'nin yaş ve son değiştirilme tarihini almak için geri çağırma* nx_http_server_cache_info_callback_set</span><span class="sxs-lookup"><span data-stu-id="86682-121">**nx_http_server_cache_info_callback_set** *Set callback to retrieve age and last modified date of specified URL*</span></span>
- <span data-ttu-id="86682-122"> *GERI çağırma işlevinden http verileri gönderme* nx_http_server_callback_data_send</span><span class="sxs-lookup"><span data-stu-id="86682-122">**nx_http_server_callback_data_send** *Send HTTP data from callback function*</span></span>
- <span data-ttu-id="86682-123"> *geri çağırma işlevlerinde yanıt üst bilgisi oluşturma* nx_http_server_callback_generate_response_header</span><span class="sxs-lookup"><span data-stu-id="86682-123">**nx_http_server_callback_generate_response_header** *Create response header in callback functions*</span></span>
- <span data-ttu-id="86682-124"> *geri çağırma işlevlerinde yanıt üst bilgisi oluşturma* nx_http_server_callback_generate_response_header_extended</span><span class="sxs-lookup"><span data-stu-id="86682-124">**nx_http_server_callback_generate_response_header_extended** *Create response header in callback functions*</span></span>
- <span data-ttu-id="86682-125"> *HTTP geri çağrısından http paketi gönderme* nx_http_server_callback_packet_send</span><span class="sxs-lookup"><span data-stu-id="86682-125">**nx_http_server_callback_packet_send** *Send an HTTP packet from an HTTP callback*</span></span>
- <span data-ttu-id="86682-126"> *geri çağırma işlevinden yanıt gönder* nx_http_server_callback_response_send</span><span class="sxs-lookup"><span data-stu-id="86682-126">**nx_http_server_callback_response_send** *Send response from callback function*</span></span>
- <span data-ttu-id="86682-127"> *geri çağırma işlevinden yanıt gönder* nx_http_server_callback_response_send_extended</span><span class="sxs-lookup"><span data-stu-id="86682-127">**nx_http_server_callback_response_send_extended** *Send response from callback function*</span></span>
- <span data-ttu-id="86682-128"> *istekten içerik al* nx_http_server_content_get</span><span class="sxs-lookup"><span data-stu-id="86682-128">**nx_http_server_content_get** *Get content from the request*</span></span>
- <span data-ttu-id="86682-129"> *istekten içerik al nx_http_server_content_get_extended; boş (sıfır içerik uzunluğu) isteklerini destekler*</span><span class="sxs-lookup"><span data-stu-id="86682-129">**nx_http_server_content_get_extended** *Get content from the request; supports empty (zero Content Length) requests*</span></span>
- <span data-ttu-id="86682-130">**nx_http_server_content_length_get** *istekteki içeriğin uzunluğunu al*</span><span class="sxs-lookup"><span data-stu-id="86682-130">**nx_http_server_content_length_get** *Get length of content in the request*</span></span>
- <span data-ttu-id="86682-131"> *istekteki içeriğin uzunluğunu nx_http_server_content_length_get_extended; boş (sıfır içerik uzunluğu) istekleri destekler*</span><span class="sxs-lookup"><span data-stu-id="86682-131">**nx_http_server_content_length_get_extended** *Get length of content in the request; supports empty (zero Content Length) requests*</span></span>
- <span data-ttu-id="86682-132">**NX_HTTP_SERVER_CREATE** *http sunucu örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="86682-132">**nx_http_server_create** *Create an HTTP Server instance*</span></span>
- <span data-ttu-id="86682-133">**nx_http_server_delete** \* bir http sunucu örneğini silme \*</span><span class="sxs-lookup"><span data-stu-id="86682-133">**nx_http_server_delete** \* Delete an HTTP Server instance\*</span></span>
- <span data-ttu-id="86682-134">**nx_http_server_get_entity_content** *, URL 'deki varlık içeriğinin boyutunu ve konumunu döndürür*</span><span class="sxs-lookup"><span data-stu-id="86682-134">**nx_http_server_get_entity_content** *Return size and location of entity content in URL*</span></span>
- <span data-ttu-id="86682-135"> *URL varlık üst bilgisini belirtilen arabelleğe nx_http_server_get_entity_header Ayıkla*</span><span class="sxs-lookup"><span data-stu-id="86682-135">**nx_http_server_get_entity_header** *Extract URL entity header into specified buffer*</span></span>
- <span data-ttu-id="86682-136">**NX_HTTP_SERVER_GMT_CALLBACK_SET** *GMT Tarih ve saatini almak için geri çağırma ayarla*</span><span class="sxs-lookup"><span data-stu-id="86682-136">**nx_http_server_gmt_callback_set** *Set callback to retrieve GMT date and time*</span></span>
- <span data-ttu-id="86682-137"> *istemci isteğinde geçersiz Kullanıcı adı ve parola alındığında geri çağırma* nx_http_server_invalid_userpassword_notify_set</span><span class="sxs-lookup"><span data-stu-id="86682-137">**nx_http_server_invalid_userpassword_notify_set** *Set callback for when invalid username and password is received in a Client request*</span></span>
- <span data-ttu-id="86682-138"> *HTML için ek mıme haritaları tanımlama* nx_http_server_mime_maps_additional_set</span><span class="sxs-lookup"><span data-stu-id="86682-138">**nx_http_server_mime_maps_additional_set** *Define additional mime maps for HTML*</span></span>
- <span data-ttu-id="86682-139"> *http üstbilgisindeki içerik uzunluğunu ayıklama nx_http_server_packet_content_find ve içerik verilerinin başlangıcına işaretçiyi ayarla*</span><span class="sxs-lookup"><span data-stu-id="86682-139">**nx_http_server_packet_content_find** *Extract content length in HTTP header and set pointer to start of content data*</span></span>
- <span data-ttu-id="86682-140"> *istemci paketini doğrudan almak* nx_http_server_packet_get</span><span class="sxs-lookup"><span data-stu-id="86682-140">**nx_http_server_packet_get** *Receive client packet directly*</span></span>
- <span data-ttu-id="86682-141"> *istekten parametre al* nx_http_server_param_get</span><span class="sxs-lookup"><span data-stu-id="86682-141">**nx_http_server_param_get** *Get parameter from the request*</span></span>
- <span data-ttu-id="86682-142"> *istekten sorgu al* nx_http_server_query_get</span><span class="sxs-lookup"><span data-stu-id="86682-142">**nx_http_server_query_get** *Get query from the request*</span></span>
- <span data-ttu-id="86682-143"> *http sunucusunu nx_http_server_start başlatın*</span><span class="sxs-lookup"><span data-stu-id="86682-143">**nx_http_server_start** *Start the HTTP Server*</span></span>
- <span data-ttu-id="86682-144"> *http sunucusunu nx_http_server_stop durdur*</span><span class="sxs-lookup"><span data-stu-id="86682-144">**nx_http_server_stop** *Stop the HTTP Server*</span></span>
- <span data-ttu-id="86682-145">**nx_http_server_type_get (kullanım dışı)** *http türünü (örneğin, metin/düz üstbilgi) Ayıkla*</span><span class="sxs-lookup"><span data-stu-id="86682-145">**nx_http_server_type_get (deprecated)** *Extract HTTP type e.g. text/plain from header*</span></span>
- <span data-ttu-id="86682-146"> *http türünü (örneğin, metin/düz üstbilgi) Ayıkla* nx_http_server_type_get_extended</span><span class="sxs-lookup"><span data-stu-id="86682-146">**nx_http_server_type_get_extended** *Extract HTTP type e.g. text/plain from header*</span></span>
- <span data-ttu-id="86682-147">**nx_http_server_digest_authenticate_notify_set** *Özet kimlik doğrulaması geri arama işlevini ayarla*</span><span class="sxs-lookup"><span data-stu-id="86682-147">**nx_http_server_digest_authenticate_notify_set** *Set digest authenticate callback function*</span></span>
- <span data-ttu-id="86682-148">**nx_http_server_authentication_check_set** *kimlik doğrulaması denetim geri arama işlevini ayarla*</span><span class="sxs-lookup"><span data-stu-id="86682-148">**nx_http_server_authentication_check_set** *Set authentication checking callback function*</span></span>

## <a name="nx_http_client_create"></a><span data-ttu-id="86682-149">nx_http_client_create</span><span class="sxs-lookup"><span data-stu-id="86682-149">nx_http_client_create</span></span>

<span data-ttu-id="86682-150">Bir PPPoE Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="86682-150">Create a PPPoE Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-151">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-151">Prototype</span></span>

```c
UINT nx_http_client_create(NX_HTTP_CLIENT *client_ptr,
            CHAR *client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr,
            ULONG window_size);
```

### <a name="description"></a><span data-ttu-id="86682-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-152">Description</span></span>

<span data-ttu-id="86682-153">Bu hizmet, belirtilen IP örneğinde bir HTTP Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86682-153">This service creates an HTTP Client instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-154">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-154">Input Parameters</span></span>

 - <span data-ttu-id="86682-155">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-155">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-156">**client_name** HTTP Istemci örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="86682-156">**client_name** Name of HTTP Client instance.</span></span>
 - <span data-ttu-id="86682-157">**ip_ptr** IP örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-157">**ip_ptr** Pointer to IP instance.</span></span>
 - <span data-ttu-id="86682-158">**pool_ptr** Varsayılan paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-158">**pool_ptr** Pointer to default packet pool.</span></span> <span data-ttu-id="86682-159">Bu havuzdaki paketlerin, tüm yanıt üst bilgisini işleyecek kadar büyük bir yükün olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86682-159">Note that the packets in this pool must have a payload large enough to handle the complete response header.</span></span> <span data-ttu-id="86682-160">Bu, *nx_http. h* içinde NX_HTTP_CLIENT_MIN_PACKET_SIZE tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="86682-160">This is defined by NX_HTTP_CLIENT_MIN_PACKET_SIZE in *nx_http.h*.</span></span>
 - <span data-ttu-id="86682-161">**window_size** Istemcinin TCP yuvası alma penceresinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="86682-161">**window_size** Size of the Client’s TCP socket receive window.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-162">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-162">Return Values</span></span>

 - <span data-ttu-id="86682-163">**NX_SUCCESS** (0x00) başarılı http istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="86682-163">**NX_SUCCESS** (0x00) Successful HTTP Client create</span></span>
 - <span data-ttu-id="86682-164">NX_PTR_ERROR (0x07) geçersiz HTTP, ip_ptr veya paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-164">NX_PTR_ERROR (0x07) Invalid HTTP, ip_ptr, or packet pool pointer</span></span>
 - <span data-ttu-id="86682-165">NX_HTTP_POOL_ERROR (0xE9) paket havuzunda geçersiz yük boyutu</span><span class="sxs-lookup"><span data-stu-id="86682-165">NX_HTTP_POOL_ERROR (0xE9) Invalid payload size in packet pool</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-166">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-166">Allowed From</span></span>

<span data-ttu-id="86682-167">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-167">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-168">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-168">Example</span></span>

```c
/* Create the HTTP Client instance “my_client” on “ip_0”. */
status =  nx_http_client_create(&my_client, “my client”, &ip_0, &pool_0, 100);

/* If status is NX_SUCCESS an HTTP Client instance was successfully created. */
```

## <a name="nx_http_client_delete"></a><span data-ttu-id="86682-169">nx_http_client_delete</span><span class="sxs-lookup"><span data-stu-id="86682-169">nx_http_client_delete</span></span>

<span data-ttu-id="86682-170">HTTP Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="86682-170">Delete an HTTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-171">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-171">Prototype</span></span>

```c
UINT nx_http_client_delete(NX_HTTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="86682-172">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-172">Description</span></span>

<span data-ttu-id="86682-173">Bu hizmet, önceden oluşturulmuş bir HTTP Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="86682-173">This service deletes a previously created HTTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-174">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-174">Input Parameters</span></span>

 - <span data-ttu-id="86682-175">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-175">**client_ptr** Pointer to HTTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-176">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-176">Return Values</span></span>

 - <span data-ttu-id="86682-177">**NX_SUCCESS** (0x00) başarılı http istemcisi silme</span><span class="sxs-lookup"><span data-stu-id="86682-177">**NX_SUCCESS** (0x00) Successful HTTP Client delete</span></span>
 - <span data-ttu-id="86682-178">NX_PTR_ERROR (0x07) geçersiz HTTP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-178">NX_PTR_ERROR (0x07) Invalid HTTP pointer</span></span>
 - <span data-ttu-id="86682-179">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-179">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-180">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-180">Allowed From</span></span>

<span data-ttu-id="86682-181">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-181">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-182">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-182">Example</span></span>

```c
/* Delete the HTTP Client instance “my_client.”  */
status =  nx_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully deleted. */
```

## <a name="nx_http_client_get_start"></a><span data-ttu-id="86682-183">nx_http_client_get_start</span><span class="sxs-lookup"><span data-stu-id="86682-183">nx_http_client_get_start</span></span>

<span data-ttu-id="86682-184">IPv4 üzerinden HTTP GET isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="86682-184">Start an HTTP GET request over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-185">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-185">Prototype</span></span>

```c
UINT nx_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, CHAR *input_ptr,
            UINT input_size, CHAR *username, CHAR *password,
            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-186">Description</span></span>

<span data-ttu-id="86682-187">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynakla bir GET isteği oluşturmaya ve gönderilmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-187">This service attempts to create and send a GET request with the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="86682-188">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="86682-188">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-189">Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, ÖRNEĞIN ```http://abc.website.com/index.htm``` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="86682-189">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="86682-190">Bu hizmet yalnızca IPv4 ağı üzerinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86682-190">This service works only over IPv4 network.</span></span> <span data-ttu-id="86682-191">IPv6 ağına bağlanması gereken uygulamalar için *nxd_http_client_get_start_extended ()* kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-191">For applications that need to connect to IPv6 network, *nxd_http_client_get_start_extended()* should be used.</span></span>

<span data-ttu-id="86682-192">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-192">This service is deprecated.</span></span> <span data-ttu-id="86682-193">Geliştiricilerin *nx_http_client_get_start_extended ()* veya *nxd_http_client_get_start_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-193">Developers are encouraged to migrate to *nx_http_client_get_start_extended()* or *nxd_http_client_get_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-194">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-194">Input Parameters</span></span>

 - <span data-ttu-id="86682-195">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-195">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-196">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="86682-196">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="86682-197">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-197">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="86682-198">**input_ptr** GET isteği için ek verilere yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-198">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="86682-199">Bu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-199">This is optional.</span></span> <span data-ttu-id="86682-200">Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86682-200">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
 - <span data-ttu-id="86682-201">**input_size** İsteğe bağlı ek girişte tarafından işaret edilen bayt sayısı ```input_ptr``` .</span><span class="sxs-lookup"><span data-stu-id="86682-201">**input_size** Number of bytes in optional additional input pointed to by ```input_ptr```.</span></span>
 - <span data-ttu-id="86682-202">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-202">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-203">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-203">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="86682-204">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-204">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="86682-205">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-205">The wait options are defined as follows:</span></span>

    - <span data-ttu-id="86682-206">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-206">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-207">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-207">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-208">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-208">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-209">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86682-209">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-210">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-210">Return Values</span></span>

 - <span data-ttu-id="86682-211">**NX_SUCCESS** (0x00) http istemcisi başarıyla gönderildi.</span><span class="sxs-lookup"><span data-stu-id="86682-211">**NX_SUCCESS** (0x00) Successfully sent HTTP Client.</span></span> <span data-ttu-id="86682-212">Başlangıç iletisi al.</span><span class="sxs-lookup"><span data-stu-id="86682-212">GET start message.</span></span>
 - <span data-ttu-id="86682-213">**NX_HTTP_ERROR** (0xE0) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="86682-213">**NX_HTTP_ERROR** (0xE0) Internal HTTP Client error</span></span>
 - <span data-ttu-id="86682-214">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="86682-214">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="86682-215">**NX_HTTP_FAILED** (0xE2) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="86682-215">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server.</span></span>
 - <span data-ttu-id="86682-216">**NX_HTTP_AUTHENTICATION_ERROR** (0xeb) adı ve/veya parolası geçersiz.</span><span class="sxs-lookup"><span data-stu-id="86682-216">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or password.</span></span>
 - <span data-ttu-id="86682-217">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-217">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-218">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="86682-218">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-219">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-219">Allowed From</span></span>

<span data-ttu-id="86682-220">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-220">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-221">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-221">Example</span></span>

```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                           NX_NULL, 0, “myname”, “mypassword”, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */


#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                            POST_MESSAGE, sizeof(POST_MESSAGE),
                            “myname”, “mypassword”, 1000);


/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST request
   for TEST.HTM and successfully sent. */
```

## <a name="nx_http_client_get_start_extended"></a><span data-ttu-id="86682-222">nx_http_client_get_start_extended</span><span class="sxs-lookup"><span data-stu-id="86682-222">nx_http_client_get_start_extended</span></span>

<span data-ttu-id="86682-223">IPv4 üzerinden HTTP GET isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="86682-223">Start an HTTP GET request over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-224">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-224">Prototype</span></span>

```c
UINT nx_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
            ULONG ip_address, CHAR *resource, UINT resource_length,
            CHAR *input_ptr, UINT input_size, CHAR *username,
            UINT username_length, CHAR *password, UINT password_length,
            ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-225">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-225">Description</span></span>

<span data-ttu-id="86682-226">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynakla bir GET isteği oluşturmaya ve gönderilmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-226">This service attempts to create and send a GET request with the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="86682-227">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="86682-227">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-228">Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, ÖRNEĞIN ```http://abc.website.com/index.htm``` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="86682-228">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="86682-229">Bu hizmet yalnızca IPv4 ağı üzerinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86682-229">This service works only over IPv4 network.</span></span> <span data-ttu-id="86682-230">IPv6 ağına bağlanması gereken uygulamalar için *nxd_http_client_get_start_extended ()* kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-230">For applications that need to connect to IPv6 network, *nxd_http_client_get_start_extended()* should be used.</span></span>

<span data-ttu-id="86682-231">Bu hizmet *nx_http_client_get_start ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-231">This service replaces *nx_http_client_get_start()*.</span></span> <span data-ttu-id="86682-232">Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="86682-232">It requires caller to specify the length of the resource, username and password.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-233">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-233">Input Parameters</span></span>

 - <span data-ttu-id="86682-234">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-234">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-235">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="86682-235">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="86682-236">istenen kaynağın URL dizesine yönelik **kaynak işaretçisi** .</span><span class="sxs-lookup"><span data-stu-id="86682-236">**resource Pointer** to URL string for requested resource.</span></span>
 - <span data-ttu-id="86682-237">**resource_length** İstenen kaynak için URL dizesi uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-237">**resource_length** Length of URL string for requested resource.</span></span>
 - <span data-ttu-id="86682-238">**input_ptr** GET isteği için ek verilere yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-238">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="86682-239">Bu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-239">This is optional.</span></span> <span data-ttu-id="86682-240">Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86682-240">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
 - <span data-ttu-id="86682-241">**input_size** İsteğe bağlı ek girişte tarafından işaret edilen bayt sayısı ```input_ptr``` .</span><span class="sxs-lookup"><span data-stu-id="86682-241">**input_size** Number of bytes in optional additional input pointed to by ```input_ptr```.</span></span>
 - <span data-ttu-id="86682-242">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-242">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-243">**username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-243">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-244">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-244">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="86682-245">**password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-245">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="86682-246">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-246">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="86682-247">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-247">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="86682-248">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-248">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-249">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-249">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-250">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-250">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-251">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86682-251">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-252">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-252">Return Values</span></span>

 - <span data-ttu-id="86682-253">**NX_SUCCESS** (0x00) http istemcisi başarıyla gönderildi.</span><span class="sxs-lookup"><span data-stu-id="86682-253">**NX_SUCCESS** (0x00) Successfully sent HTTP Client.</span></span> <span data-ttu-id="86682-254">Başlangıç iletisi al</span><span class="sxs-lookup"><span data-stu-id="86682-254">GET start message</span></span>
 - <span data-ttu-id="86682-255">**NX_HTTP_ERROR** (0xE0) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="86682-255">**NX_HTTP_ERROR** (0xE0) Internal HTTP Client error</span></span>
 - <span data-ttu-id="86682-256">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="86682-256">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="86682-257">**NX_HTTP_FAILED** (0xE2) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="86682-257">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server.</span></span>
 - <span data-ttu-id="86682-258">**NX_HTTP_AUTHENTICATION_ERROR** (0xeb) adı ve/veya parolası geçersiz.</span><span class="sxs-lookup"><span data-stu-id="86682-258">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or password.</span></span>
 - <span data-ttu-id="86682-259">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-259">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-260">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="86682-260">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-261">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-261">Allowed From</span></span>

<span data-ttu-id="86682-262">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-262">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-263">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-263">Example</span></span>

```c
/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */


#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                     9, POST_MESSAGE, sizeof(POST_MESSAGE),
                                     “myname”, 6, “mypassword”, 10, 1000);


/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST request
   for TEST.HTM and successfully sent. */
```

## <a name="nxd_http_client_get_start"></a><span data-ttu-id="86682-264">nxd_http_client_get_start</span><span class="sxs-lookup"><span data-stu-id="86682-264">nxd_http_client_get_start</span></span>

<span data-ttu-id="86682-265">HTTP GET isteği gönderme (IPv4 veya IPv6)</span><span class="sxs-lookup"><span data-stu-id="86682-265">Send an HTTP GET request (IPv4 or IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-266">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-266">Prototype</span></span>

```c
UINT nxd_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
                NXD_ADDRESS *server_ip, CHAR *resource,
                CHAR *input_ptr, UINT input_size, CHAR *username, CHAR *password, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-267">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-267">Description</span></span>

<span data-ttu-id="86682-268">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynakla bir GET isteği oluşturmaya ve gönderilmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-268">This service attempts to create and send a GET request with the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="86682-269">Bu, IPv4 veya IPv6 ağına bağlanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86682-269">It can be used to connect to IPv4 or IPv6 network.</span></span> <span data-ttu-id="86682-270">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="86682-270">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

> [!NOTE]
><span data-ttu-id="86682-271">Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, ÖRNEĞIN ```http://abc.website.com/index.htm``` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="86682-271">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="86682-272">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-272">This service is deprecated.</span></span> <span data-ttu-id="86682-273">Geliştiricilerin *nxd_http_client_get_start_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-273">Developers are encouraged to migrate to *nxd_http_client_get_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-274">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-274">Input Parameters</span></span>

 - <span data-ttu-id="86682-275">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-275">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-276">**Server_ip** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="86682-276">**Server_ip** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="86682-277">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-277">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="86682-278">**input_ptr** GET isteği için ek verilere yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-278">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="86682-279">Bu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-279">This is optional.</span></span> <span data-ttu-id="86682-280">Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86682-280">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
 - <span data-ttu-id="86682-281">**input_size** İsteğe bağlı ek girişte tarafından işaret edilen bayt sayısı ```input_ptr``` .</span><span class="sxs-lookup"><span data-stu-id="86682-281">**input_size** Number of bytes in optional additional input pointed to by ```input_ptr```.</span></span>
 - <span data-ttu-id="86682-282">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-282">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-283">**username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-283">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-284">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-284">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="86682-285">**password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-285">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="86682-286">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-286">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="86682-287">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-287">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="86682-288">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-288">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-289">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-289">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-290">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-290">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-291">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86682-291">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-292">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-292">Return Values</span></span>

 - <span data-ttu-id="86682-293">**NX_SUCCESS** (0x00) GET isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="86682-293">**NX_SUCCESS** (0x00) Successfully sent GET request</span></span>
 - <span data-ttu-id="86682-294">**NX_HTTP_PASSWORD_TOO_LONG** (0xf0) parolası arabellek boyutunu aşıyor</span><span class="sxs-lookup"><span data-stu-id="86682-294">**NX_HTTP_PASSWORD_TOO_LONG** (0xF0) Password exceeds buffer size</span></span>
 - <span data-ttu-id="86682-295">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="86682-295">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="86682-296">**NX_HTTP_FAILED** (0xE2) geçersiz paket parametreleri.</span><span class="sxs-lookup"><span data-stu-id="86682-296">**NX_HTTP_FAILED** (0xE2) Invalid packet parameters.</span></span>
 - <span data-ttu-id="86682-297">**NX_HTTP_AUTHENTICATION_ERROR** (0xeb) geçersiz ad veya parola</span><span class="sxs-lookup"><span data-stu-id="86682-297">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name or password</span></span>
 - <span data-ttu-id="86682-298">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-298">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-299">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-299">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-300">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-300">Allowed From</span></span>

<span data-ttu-id="86682-301">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-301">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-302">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-302">Example</span></span>

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;


/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nxd_http_client_get_start(&my_client, server_ip_address, “/TEST.HTM”,
NX_NULL, 0, “myname”, “mypassword”, 1000);


/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */
```

## <a name="nxd_http_client_get_start_extended"></a><span data-ttu-id="86682-303">nxd_http_client_get_start_extended</span><span class="sxs-lookup"><span data-stu-id="86682-303">nxd_http_client_get_start_extended</span></span>

<span data-ttu-id="86682-304">HTTP GET isteği gönderme (IPv4 veya IPv6)</span><span class="sxs-lookup"><span data-stu-id="86682-304">Send an HTTP GET request (IPv4 or IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-305">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-305">Prototype</span></span>

```c
UINT nxd_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
                NXD_ADDRESS *server_ip, CHAR *resource,
                UINT resource_length, CHAR *input_ptr,
                UINT input_size, CHAR *username, UINT
                username_length, CHAR *password, UINT
                password_length, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-306">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-306">Description</span></span>

<span data-ttu-id="86682-307">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynakla bir GET isteği oluşturmaya ve gönderilmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-307">This service attempts to create and send a GET request with the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="86682-308">Bu, IPv4 veya IPv6 ağına bağlanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86682-308">It can be used to connect to IPv4 or IPv6 network.</span></span> <span data-ttu-id="86682-309">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="86682-309">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-310">Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, ÖRNEĞIN ```http://abc.website.com/index.htm``` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="86682-310">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="86682-311">Bu hizmet *nxd_http_client_get_start ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-311">This service replaces *nxd_http_client_get_start()*.</span></span> <span data-ttu-id="86682-312">Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="86682-312">It requires caller to specify the length of the resource, username and password.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-313">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-313">Input Parameters</span></span>

 - <span data-ttu-id="86682-314">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-314">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-315">**Server_ip** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="86682-315">**Server_ip** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="86682-316">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-316">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="86682-317">**resource_length** İstenen kaynak için URL dizesi uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-317">**resource_length** Length of URL string for requested resource.</span></span>
 - <span data-ttu-id="86682-318">**input_ptr** GET isteği için ek verilere yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-318">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="86682-319">Bu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-319">This is optional.</span></span> <span data-ttu-id="86682-320">Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86682-320">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
 - <span data-ttu-id="86682-321">**input_size** İsteğe bağlı ek girişte tarafından işaret edilen bayt sayısı ```input_ptr``` .</span><span class="sxs-lookup"><span data-stu-id="86682-321">**input_size** Number of bytes in optional additional input pointed to by ```input_ptr```.</span></span>
 - <span data-ttu-id="86682-322">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-322">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-323">**username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-323">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-324">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-324">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="86682-325">**password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-325">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="86682-326">**wait_option** Hizmetin HTTP Istemcisi alma başlangıcını işlemek için dahili olarak bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-326">**wait_option** Defines how long the service will wait internally to process the HTTP Client get start.</span></span> <span data-ttu-id="86682-327">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-327">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="86682-328">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-328">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-329">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-329">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-330">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-330">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-331">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86682-331">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-332">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-332">Return Values</span></span>

 - <span data-ttu-id="86682-333">**NX_SUCCESS** (0x00) GET isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="86682-333">**NX_SUCCESS** (0x00) Successfully sent GET request</span></span>
 - <span data-ttu-id="86682-334">**NX_HTTP_PASSWORD_TOO_LONG** (0xf0) parolası arabellek boyutunu aşıyor</span><span class="sxs-lookup"><span data-stu-id="86682-334">**NX_HTTP_PASSWORD_TOO_LONG** (0xF0) Password exceeds buffer size</span></span>
 - <span data-ttu-id="86682-335">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="86682-335">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="86682-336">**NX_HTTP_FAILED** (0xE2) geçersiz paket parametreleri.</span><span class="sxs-lookup"><span data-stu-id="86682-336">**NX_HTTP_FAILED** (0xE2) Invalid packet parameters.</span></span>
 - <span data-ttu-id="86682-337">**NX_HTTP_AUTHENTICATION_ERROR** (0xeb) geçersiz ad veya parola</span><span class="sxs-lookup"><span data-stu-id="86682-337">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name or password</span></span>
 - <span data-ttu-id="86682-338">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-338">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-339">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-339">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-340">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-340">Allowed From</span></span>

<span data-ttu-id="86682-341">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-341">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-342">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-342">Example</span></span>

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;


/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nxd_http_client_get_start_extended(&my_client, server_ip_address,
                                             “/TEST.HTM”, 9, NX_NULL, 0, “myname”,
        6, “mypassword”, 10, 1000);


/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
   far successful. The client must now call nx_http_client_get_packet multiple
   times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_http_client_get_packet"></a><span data-ttu-id="86682-343">nx_http_client_get_packet</span><span class="sxs-lookup"><span data-stu-id="86682-343">nx_http_client_get_packet</span></span>

<span data-ttu-id="86682-344">Sonraki kaynak veri paketini al</span><span class="sxs-lookup"><span data-stu-id="86682-344">Get next resource data packet</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-345">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-345">Prototype</span></span>

```c
UINT nx_http_client_get_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET **packet_ptr, ULONG
                               wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-346">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-346">Description</span></span>

<span data-ttu-id="86682-347">Bu hizmet, önceki *nx_http_client_get_start* çağrısı tarafından istenen kaynağın sonraki içerik paketini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-347">This service retrieves the next packet of content of the resource requested by the previous *nx_http_client_get_start* call.</span></span> <span data-ttu-id="86682-348">NX_HTTP_GET_DONE geri dönüş durumu alınana kadar bu yordama yönelik ardışık çağrılar yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-348">Successive calls to this routine should be made until the return status of NX_HTTP_GET_DONE is received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-349">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-349">Input Parameters</span></span>

 - <span data-ttu-id="86682-350">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-350">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-351">**packet_ptr** Kısmi kaynak içeriği içeren paket işaretçisi hedefi.</span><span class="sxs-lookup"><span data-stu-id="86682-351">**packet_ptr** Destination for packet pointer containing partial resource content.</span></span>
 - <span data-ttu-id="86682-352">**wait_option** Hizmetin HTTP Istemcisi alma paketi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-352">**wait_option** Defines how long the service will wait for the HTTP Client get packet.</span></span> <span data-ttu-id="86682-353">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-353">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="86682-354">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-354">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-355">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-355">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-356">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-356">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-357">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86682-357">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-358">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-358">Return Values</span></span>

 - <span data-ttu-id="86682-359">**NX_SUCCESS** (0x00) başarılı http istemcisi Get paketi.</span><span class="sxs-lookup"><span data-stu-id="86682-359">**NX_SUCCESS** (0x00) Successful HTTP Client get packet.</span></span>
 - <span data-ttu-id="86682-360">**NX_HTTP_GET_DONE** (0xEC) http istemcisi Get paketi bitti</span><span class="sxs-lookup"><span data-stu-id="86682-360">**NX_HTTP_GET_DONE** (0xEC) HTTP Client get packet is done</span></span>
 - <span data-ttu-id="86682-361">**NX_HTTP_NOT_READY** (0xea) http istemcisi Get modunda değil.</span><span class="sxs-lookup"><span data-stu-id="86682-361">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not in get mode.</span></span>
 - <span data-ttu-id="86682-362">**NX_HTTP_BAD_PACKET_LENGTH** (0faksla) geçersiz paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="86682-362">**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Invalid packet length</span></span>
 - <span data-ttu-id="86682-363">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-363">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-364">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-364">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-365">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-365">Allowed From</span></span>

<span data-ttu-id="86682-366">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-366">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-367">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-367">Example</span></span>

```c
/* Get the next packet of resource content on the HTTP Client “my_client.”
   Note that the nx_http_client_get_start routine must have been called
   previously. */
status =  nx_http_client_get_packet(&my_client, &next_packet, 1000);


/* If status is NX_SUCCESS, the next packet of content is pointed to
   by “next_packet”. */
```

## <a name="nx_http_client_put_start"></a><span data-ttu-id="86682-368">nx_http_client_put_start</span><span class="sxs-lookup"><span data-stu-id="86682-368">nx_http_client_put_start</span></span>

<span data-ttu-id="86682-369">IPv4 üzerinden HTTP PUT isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="86682-369">Start an HTTP PUT request over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-370">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-370">Prototype</span></span>

```c
UINT nx_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                               ULONG ip_address, CHAR *resource,
                               CHAR *username, CHAR *password,
                               ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-371">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-371">Description</span></span>

<span data-ttu-id="86682-372">Bu hizmet, belirtilen IP adresindeki HTTP sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="86682-372">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address.</span></span> <span data-ttu-id="86682-373">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-373">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet()* routine to actually send the resource contents to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-374">Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, örneğin ```http://abc.website.com/index.htm``` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="86682-374">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="86682-375">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-375">This service is deprecated.</span></span> <span data-ttu-id="86682-376">Geliştiricilerin *nxd_http_client_put_start_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-376">Developers are encouraged to migrate to *nxd_http_client_put_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-377">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-377">Input Parameters</span></span>

 - <span data-ttu-id="86682-378">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-378">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-379">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="86682-379">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="86682-380">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-380">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="86682-381">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-381">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-382">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-382">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="86682-383">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="86682-383">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="86682-384">*Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86682-384">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
 - <span data-ttu-id="86682-385">**wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-385">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="86682-386">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-386">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="86682-387">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-387">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-388">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-388">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-389">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-389">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-390">Sayısal bir değer seçilmesi (0x1-0xFFFFFFFE), HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı sayısını belirtir</span><span class="sxs-lookup"><span data-stu-id="86682-390">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-391">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-391">Return Values</span></span>

 - <span data-ttu-id="86682-392">**NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="86682-392">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
 - <span data-ttu-id="86682-393">**NX_HTTP_USERNAME_TOO_LONG** (0xf1) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="86682-393">**NX_HTTP_USERNAME_TOO_LONG** (0xF1) Username too large for buffer</span></span>
 - <span data-ttu-id="86682-394">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="86682-394">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="86682-395">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-395">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-396">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="86682-396">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
 - <span data-ttu-id="86682-397">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-397">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-398">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-398">Allowed From</span></span>

<span data-ttu-id="86682-399">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-400">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-400">Example</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP Server
   at IP address 1.2.3.5. */
status =  nx_http_client_put_start(&my_client, IP_ADDRESS(1, 2, 3, 5),
“/TEST.HTM”, “myname”, “mypassword”, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
   started. */
```

## <a name="nx_http_client_put_start_extended"></a><span data-ttu-id="86682-401">nx_http_client_put_start_extended</span><span class="sxs-lookup"><span data-stu-id="86682-401">nx_http_client_put_start_extended</span></span>

<span data-ttu-id="86682-402">IPv4 üzerinden HTTP PUT isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="86682-402">Start an HTTP PUT request over IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-403">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-403">Prototype</span></span>

```c
UINT nx_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
           ULONG ip_address, CHAR *resource, UINT resource_length,
           CHAR *username,UINT username_length, CHAR *password,
           UINT password_length, ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-404">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-404">Description</span></span>

<span data-ttu-id="86682-405">Bu hizmet, belirtilen IP adresindeki HTTP sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="86682-405">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address.</span></span> <span data-ttu-id="86682-406">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-406">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet()* routine to actually send the resource contents to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-407">Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, örneğin ```http://abc.website.com/index.htm``` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="86682-407">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="86682-408">Bu hizmet *nx_http_client_put_start ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-408">This service replaces *nx_http_client_put_start()*.</span></span> <span data-ttu-id="86682-409">Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="86682-409">It requires caller to specify the length of the resource, username and password.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-410">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-410">Input Parameters</span></span>

 - <span data-ttu-id="86682-411">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-411">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-412">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="86682-412">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="86682-413">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-413">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="86682-414">**resource_length** Sunucuya gönderilen kaynağın URL dizesi uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-414">**resource_length** Length of URL string for resource to send to Server.</span></span>
 - <span data-ttu-id="86682-415">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-415">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-416">**username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-416">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-417">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-417">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="86682-418">**password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-418">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="86682-419">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="86682-419">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="86682-420">*Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86682-420">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
 - <span data-ttu-id="86682-421">**wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-421">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="86682-422">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-422">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="86682-423">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-423">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-424">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-424">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-425">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-425">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-426">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86682-426">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-427">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-427">Return Values</span></span>

 - <span data-ttu-id="86682-428">**NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="86682-428">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
 - <span data-ttu-id="86682-429">**NX_HTTP_USERNAME_TOO_LONG** (0xf1) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="86682-429">**NX_HTTP_USERNAME_TOO_LONG** (0xF1) Username too large for buffer</span></span>
 - <span data-ttu-id="86682-430">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="86682-430">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="86682-431">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-431">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-432">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="86682-432">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
 - <span data-ttu-id="86682-433">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-433">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-434">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-434">Allowed From</span></span>

<span data-ttu-id="86682-435">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-435">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-436">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-436">Example</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP Server
   at IP address 1.2.3.5. */
status =  nx_http_client_put_start_extended(&my_client, IP_ADDRESS(1, 2, 3, 5),
“/TEST.HTM”, 9, “myname”, 6, “mypassword”, 10, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
   started. */
```

## <a name="nxd_http_client_put_start"></a><span data-ttu-id="86682-437">nxd_http_client_put_start</span><span class="sxs-lookup"><span data-stu-id="86682-437">nxd_http_client_put_start</span></span>

<span data-ttu-id="86682-438">HTTP PUT isteği (IPv4 veya IPv6) başlatma</span><span class="sxs-lookup"><span data-stu-id="86682-438">Start an HTTP PUT request (IPv4 or IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-439">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-439">Prototype</span></span>

```c
UINT nxd_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                               NXD_ADDRESS *server_ip, CHAR *resource,
                               CHAR *username, CHAR *password,
                               ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-440">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-440">Description</span></span>

<span data-ttu-id="86682-441">Bu hizmet, belirtilen kaynağı HTTP sunucusunda IPv6 üzerinden sağlanan IP adresine (gönderme) (Gönderen) yüklemeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-441">This service attempts to PUT (send) the specified resource on the HTTP Server at the supplied IP address over IPv6.</span></span> <span data-ttu-id="86682-442">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-442">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet()* routine to actually send the resource contents to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-443">Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, örneğin ```http://abc.website.com/index.htm``` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="86682-443">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="86682-444">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-444">This service is deprecated.</span></span> <span data-ttu-id="86682-445">Geliştiricilerin *nxd_http_client_put_start_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-445">Developers are encouraged to migrate to *nxd_http_client_put_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-446">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-446">Input Parameters</span></span>

 - <span data-ttu-id="86682-447">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-447">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-448">**server_ip** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="86682-448">**server_ip** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="86682-449">**kaynak** Sunucuya gönderilen kaynağın URL dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-449">**resource** Pointer to URL string for resource to send to Server.</span></span>
 - <span data-ttu-id="86682-450">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-450">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-451">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-451">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="86682-452">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="86682-452">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="86682-453">*Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86682-453">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
 - <span data-ttu-id="86682-454">**wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-454">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="86682-455">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-455">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="86682-456">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-456">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-457">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-457">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-458">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-458">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-459">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86682-459">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-460">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-460">Return Values</span></span>

 - <span data-ttu-id="86682-461">**NX_SUCCESS** (0x00) http istemcisi PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="86682-461">**NX_SUCCESS** (0x00) Successfully sent HTTP Client PUT request</span></span>
 - <span data-ttu-id="86682-462">**NX_HTTP_ERROR** (0xE0) http istemcisi iç hatası</span><span class="sxs-lookup"><span data-stu-id="86682-462">**NX_HTTP_ERROR** (0xE0) HTTP Client internal error</span></span>
 - <span data-ttu-id="86682-463">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="86682-463">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="86682-464">**NX_HTTP_FAILED** (0xE2) http sunucusuyla ILETIŞIM kurarken http istemci hatası</span><span class="sxs-lookup"><span data-stu-id="86682-464">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server</span></span>
 - <span data-ttu-id="86682-465">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-465">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-466">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="86682-466">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
 - <span data-ttu-id="86682-467">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-467">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-468">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-468">Allowed From</span></span>

<span data-ttu-id="86682-469">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-469">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-470">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-470">Example</span></span>

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;

/* Start an HTTP PUT to place the 20-byte resource Client_test.HTM” on the HTTPv6  
   Server. */
status =  nxd_http_client_put_start(&my_client, &server_ip_address,
                                    "/client_test.htm", "name", "password", 103, 50);

/* If status is NX_SUCCESS, the PUT operation for Client_test.HTM has successfully
   been started. */
```

## <a name="nxd_http_client_put_start_extended"></a><span data-ttu-id="86682-471">nxd_http_client_put_start_extended</span><span class="sxs-lookup"><span data-stu-id="86682-471">nxd_http_client_put_start_extended</span></span>

<span data-ttu-id="86682-472">HTTP PUT isteği (IPv4 veya IPv6) başlatma</span><span class="sxs-lookup"><span data-stu-id="86682-472">Start an HTTP PUT request (IPv4 or IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-473">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-473">Prototype</span></span>

```c
UINT nxd_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
          NXD_ADDRESS *server_ip, CHAR *resource, UINT resource_length,
          CHAR *username, UINT username_length, CHAR *password,
          UINT password_length, ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-474">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-474">Description</span></span>

<span data-ttu-id="86682-475">Bu hizmet, belirtilen kaynağı HTTP sunucusunda IPv6 üzerinden sağlanan IP adresine (gönderme) (Gönderen) yüklemeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-475">This service attempts to PUT (send) the specified resource on the HTTP Server at the supplied IP address over IPv6.</span></span> <span data-ttu-id="86682-476">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-476">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet()* routine to actually send the resource contents to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-477">Kaynak dizesi yerel bir dosyaya başvurabilir, örneğin ``` “/index.htm” ``` başka BIR URL 'ye başvurabilir, örneğin ```http://abc.website.com/index.htm``` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="86682-477">The resource string can refer to a local file e.g. ``` “/index.htm” ``` or it can refer to another URL e.g. ```http://abc.website.com/index.htm``` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="86682-478">Bu hizmet *nxd_http_client_put_start ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-478">This service replaces *nxd_http_client_put_start()*.</span></span> <span data-ttu-id="86682-479">Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="86682-479">It requires caller to specify the length of the resource, username and password.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-480">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-480">Input Parameters</span></span>

 - <span data-ttu-id="86682-481">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-481">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-482">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="86682-482">**ip_address** IP address of the HTTP Server.</span></span>
 - <span data-ttu-id="86682-483">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-483">**resource** Pointer to URL string for requested resource.</span></span>
 - <span data-ttu-id="86682-484">**resource_length** Sunucuya gönderilen kaynağın URL dizesi uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-484">**resource_length** Length of URL string for resource to send to Server.</span></span>
 - <span data-ttu-id="86682-485">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-485">**username** Pointer to optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-486">**username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-486">**username_length** Length of optional user name for authentication.</span></span>
 - <span data-ttu-id="86682-487">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-487">**password** Pointer to optional password for authentication.</span></span>
 - <span data-ttu-id="86682-488">**password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-488">**password_length** Length of optional password for authentication.</span></span>
 - <span data-ttu-id="86682-489">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="86682-489">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="86682-490">*Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86682-490">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
 - <span data-ttu-id="86682-491">**wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-491">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="86682-492">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-492">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="86682-493">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-493">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-494">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-494">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-495">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-495">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-496">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86682-496">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-497">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-497">Return Values</span></span>

 - <span data-ttu-id="86682-498">**NX_SUCCESS** (0x00) http istemcisi PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="86682-498">**NX_SUCCESS** (0x00) Successfully sent HTTP Client PUT request</span></span>
 - <span data-ttu-id="86682-499">**NX_HTTP_ERROR** (0xE0) http istemcisi iç hatası</span><span class="sxs-lookup"><span data-stu-id="86682-499">**NX_HTTP_ERROR** (0xE0) HTTP Client internal error</span></span>
 - <span data-ttu-id="86682-500">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="86682-500">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="86682-501">NX_HTTP_FAILED (0xE2) http sunucusuyla iletişim kurarken HTTP Istemci hatası</span><span class="sxs-lookup"><span data-stu-id="86682-501">NX_HTTP_FAILED (0xE2) HTTP Client error communicating with the HTTP Server</span></span>
 - <span data-ttu-id="86682-502">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-502">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-503">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="86682-503">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
 - <span data-ttu-id="86682-504">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-504">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-505">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-505">Allowed From</span></span>

<span data-ttu-id="86682-506">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-506">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-507">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-507">Example</span></span>

```c
NXD_ADDRESS server_ip_address;

/* for an IPv4 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_address.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,4);

/* for an IPv6 address, define as follows: */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0x0;
server_ip_address.nxd_ip_address.v6[2] = 0xf101;
server_ip_address.nxd_ip_address.v6[3] = 0x106;

/* Start an HTTP PUT to place the 20-byte resource Client_test.HTM” on the HTTPv6  
   Server. */
status =  nxd_http_client_put_start_extended(&my_client, &server_ip_address,
                                            "/client_test.htm", 16, "name", 4, "password", 8, 103, 50);

/* If status is NX_SUCCESS, the PUT operation for Client_test.HTM has successfully
   been started. */
```

## <a name="nx_http_client_put_packet"></a><span data-ttu-id="86682-508">nx_http_client_put_packet</span><span class="sxs-lookup"><span data-stu-id="86682-508">nx_http_client_put_packet</span></span>

<span data-ttu-id="86682-509">Sonraki kaynak veri paketini gönder</span><span class="sxs-lookup"><span data-stu-id="86682-509">Send next resource data packet</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-510">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-510">Prototype</span></span>

```c
UINT nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                               NX_PACKET *packet_ptr,
                               ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="86682-511">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-511">Description</span></span>

<span data-ttu-id="86682-512">Bu hizmet, kaynak içeriğinin bir sonraki paketini HTTP sunucusuna gönderilmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-512">This service attempts to send the next packet of resource content to the HTTP Server.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-513">Bu yordam, gönderilen paketlerin Birleşik uzunluğu önceki *nx_http_client_put_start* çağrısında belirtilen "total_bytes" değerine eşit olana kadar kaldı çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-513">This routine should be called repetitively until the combined length of the packets sent equals the “total_bytes” specified in the previous *nx_http_client_put_start* call.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-514">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-514">Input Parameters</span></span>

 - <span data-ttu-id="86682-515">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-515">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-516">**packet_ptr** HTTP sunucusuna gönderilen kaynağın bir sonraki içeriğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-516">**packet_ptr** Pointer to next content of the resource to being sent to the HTTP Server.</span></span>
 - <span data-ttu-id="86682-517">**wait_option** Hizmetin, iç olarak HTTP Istemcisi PUT paketini işlemesini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86682-517">**wait_option** Defines how long the service will wait internally to process the HTTP Client PUT packet.</span></span> <span data-ttu-id="86682-518">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="86682-518">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="86682-519">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="86682-519">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
    - <span data-ttu-id="86682-520">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="86682-520">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>

    <span data-ttu-id="86682-521">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86682-521">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

    <span data-ttu-id="86682-522">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86682-522">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-523">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-523">Return Values</span></span>

 - <span data-ttu-id="86682-524">**NX_SUCCESS** (0x00) http Istemci paketini başarıyla gönderdi.</span><span class="sxs-lookup"><span data-stu-id="86682-524">**NX_SUCCESS** (0x00) Successfully sent HTTP Client packet.</span></span>
 - <span data-ttu-id="86682-525">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="86682-525">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
 - <span data-ttu-id="86682-526">**NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0xEE) sunucu hata kodu aldı</span><span class="sxs-lookup"><span data-stu-id="86682-526">**NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0xEE) Received Server error code</span></span>
 - <span data-ttu-id="86682-527">**NX_HTTP_BAD_PACKET_LENGTH** (0faksla) geçersiz paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="86682-527">**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Invalid packet length</span></span>
 - <span data-ttu-id="86682-528">**NX_HTTP_AUTHENTICATION_ERROR** (0xeb) geçersiz ad ve/veya parola</span><span class="sxs-lookup"><span data-stu-id="86682-528">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or Password</span></span>
 - <span data-ttu-id="86682-529">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) sunucu, put tamamlanmadan önce yanıt veriyor</span><span class="sxs-lookup"><span data-stu-id="86682-529">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Server responds before PUT Is complete</span></span>
 - <span data-ttu-id="86682-530">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-530">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-531">NX_INVALID_PACKET (0x12) paketi TCP üst bilgisi için çok küçük</span><span class="sxs-lookup"><span data-stu-id="86682-531">NX_INVALID_PACKET (0x12) Packet too small for TCP header</span></span>
 - <span data-ttu-id="86682-532">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-532">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-533">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-533">Allowed From</span></span>

<span data-ttu-id="86682-534">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-534">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-535">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-535">Example</span></span>

```c
/* Send a 20-byte packet representing the content of the resource
   “/TEST.HTM” to the HTTP Server. */
status =  nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr, NX_PACKET *packet_ptr, ULONG wait_option);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM has
   successfully been sent. */
```

## <a name="nx_http_client_set_connect_port"></a><span data-ttu-id="86682-536">nx_http_client_set_connect_port</span><span class="sxs-lookup"><span data-stu-id="86682-536">nx_http_client_set_connect_port</span></span>

<span data-ttu-id="86682-537">Bağlantı noktasını sunucuya ayarla</span><span class="sxs-lookup"><span data-stu-id="86682-537">Set the connection port to the Server</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-538">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-538">Prototype</span></span>

```c
UINT nx_http_client_set_connect_port(NX_HTTP_CLIENT *client_ptr,
                                      UINT port);
```

### <a name="description"></a><span data-ttu-id="86682-539">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-539">Description</span></span>

<span data-ttu-id="86682-540">Bu hizmet, HTTP sunucusuna, çalışma zamanında belirtilen bağlantı noktasına bağlanırken bağlantı noktasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="86682-540">This service changes the connect port when connecting to the HTTP Server to the specified port at runtime.</span></span> <span data-ttu-id="86682-541">Aksi takdirde, bağlantı noktası varsayılan olarak 80 ' dir.</span><span class="sxs-lookup"><span data-stu-id="86682-541">Otherwise the connect port defaults to 80.</span></span> <span data-ttu-id="86682-542">Bunun *nx_http_client_get_start ()* ve *nx_http_client_put_start ()* öncesinde ÇAĞRıLMASı gerekir, örneğin http istemcisi sunucusuyla bağlanır.</span><span class="sxs-lookup"><span data-stu-id="86682-542">This must be called before *nx_http_client_get_start()* and *nx_http_client_put_start()* e.g. when the HTTP Client connects with the Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-543">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-543">Input Parameters</span></span>

 - <span data-ttu-id="86682-544">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-544">**client_ptr** Pointer to HTTP Client control block.</span></span>
 - <span data-ttu-id="86682-545">**bağlantı noktası** Sunucuya bağlanmak için bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="86682-545">**port** Port for connecting to the Server.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-546">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-546">Return Values</span></span>

 - <span data-ttu-id="86682-547">**NX_SUCCESS** (0x00) bağlantı noktası başarıyla değiştirilir</span><span class="sxs-lookup"><span data-stu-id="86682-547">**NX_SUCCESS** (0x00) Successfully change port</span></span>
 - <span data-ttu-id="86682-548">NX_INVALID_PORT (0x46) bağlantı noktası en büyük değeri (0xFFFF) aşıyor veya sıfır</span><span class="sxs-lookup"><span data-stu-id="86682-548">NX_INVALID_PORT (0x46) Port exceeds the maximum (0xFFFF) or is zero</span></span>
 - <span data-ttu-id="86682-549">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-549">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-550">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-550">Allowed From</span></span>

<span data-ttu-id="86682-551">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="86682-551">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="86682-552">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-552">Example</span></span>

```c
NX_HTTP_CLIENT *client_ptr;

/* Change the connect port to 114. */
status =  nx_http_client_set_connect_port(client_ptr, 114);

/* If status is NX_SUCCESS, the connect port is successfully changed. */
```

## <a name="nx_http_server_cache_info_callback_set"></a><span data-ttu-id="86682-553">nx_http_server_cache_info_callback_set</span><span class="sxs-lookup"><span data-stu-id="86682-553">nx_http_server_cache_info_callback_set</span></span>

<span data-ttu-id="86682-554">URL 'YI en yüksek yaş ve tarihi almak için geri aramayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="86682-554">Set the callback to retrieve URL max age and date</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-555">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-555">Prototype</span></span>

```c
UINT nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                         UINT (*cache_info_get)(CHAR *resource,
                                                 UINT *max_age,
                                                 NX_HTTP_SERVER_DATE
                                                      *date));
```

### <a name="description"></a><span data-ttu-id="86682-556">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-556">Description</span></span>

<span data-ttu-id="86682-557">Bu hizmet, belirtilen kaynağın yaş ve son değiştirilme tarihini elde etmek için çağrılan geri çağırma hizmetini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="86682-557">This service sets the callback service invoked to obtain the maximum age and last modified date of the specified resource.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-558">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-558">Input Parameters</span></span>

 - <span data-ttu-id="86682-559">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-559">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-560">**cache_info_get** Geri çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-560">**cache_info_get** Pointer to the callback</span></span>
 - <span data-ttu-id="86682-561">**max_age** Bir kaynağın maksimum yaşı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-561">**max_age** Pointer to maximum age of a resource</span></span>
 - <span data-ttu-id="86682-562">**veri** Son değiştirme tarihine yönelik işaretçi döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="86682-562">**data** Pointer to last modified date returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-563">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-563">Return Values</span></span>

 - <span data-ttu-id="86682-564">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="86682-564">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="86682-565">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-565">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-566">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-566">Allowed From</span></span>

<span data-ttu-id="86682-567">Başlatma</span><span class="sxs-lookup"><span data-stu-id="86682-567">Initialization</span></span>

### <a name="example"></a><span data-ttu-id="86682-568">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-568">Example</span></span>

```c
NX_HTTP_SERVER my_server;

UINT cache_info_get(CHAR *resource, UINT *max_age,
                           NX_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_http_server_create and before the HTTP  
   server is set by nx_http_server_start(), set the cache info callback: */

status = nx_http_server_cache_info_callback_set(&my_server, cache_info_get);


/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_http_server_callback_data_send"></a><span data-ttu-id="86682-569">nx_http_server_callback_data_send</span><span class="sxs-lookup"><span data-stu-id="86682-569">nx_http_server_callback_data_send</span></span>

<span data-ttu-id="86682-570">Geri çağırma işlevinden veri Gönder</span><span class="sxs-lookup"><span data-stu-id="86682-570">Send data from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-571">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-571">Prototype</span></span>

```c
UINT nx_http_server_callback_data_send(NX_HTTP_SERVER *server_ptr,
                                       VOID *data_ptr,
                                       ULONG data_length);
```

### <a name="description"></a><span data-ttu-id="86682-572">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-572">Description</span></span>

<span data-ttu-id="86682-573">Bu hizmet, sağlanan paketteki verileri uygulamanın geri arama yordamından gönderir.</span><span class="sxs-lookup"><span data-stu-id="86682-573">This service sends the data in the supplied packet from the application’s callback routine.</span></span> <span data-ttu-id="86682-574">Bu, genellikle GET/POST istekleri ile ilişkili dinamik verileri göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86682-574">This is typically used to send dynamic data associated with GET/POST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-575">Bu işlev kullanılıyorsa, tüm yanıtın doğru biçimde gönderilmesi için geri çağırma yordamı sorumludur.</span><span class="sxs-lookup"><span data-stu-id="86682-575">If this function is used, the callback routine is responsible for sending the entire response in the proper format.</span></span> <span data-ttu-id="86682-576">Ayrıca, geri arama yordamı NX_HTTP_CALLBACK_COMPLETED durumunu döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="86682-576">In addition, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-577">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-577">Input Parameters</span></span>

 - <span data-ttu-id="86682-578">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-578">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-579">**data_ptr** Gönderilen verilerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-579">**data_ptr** Pointer to the data to send.</span></span>
 - <span data-ttu-id="86682-580">**data_length**  Gönderilen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="86682-580">**data_length**  Number of bytes to send.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-581">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-581">Return Values</span></span>

 - <span data-ttu-id="86682-582">**NX_SUCCESS** (0x00) sunucu verilerini başarıyla gönderdi</span><span class="sxs-lookup"><span data-stu-id="86682-582">**NX_SUCCESS** (0x00) Successfully sent Server data</span></span>
 - <span data-ttu-id="86682-583">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-583">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-584">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-584">Allowed From</span></span>

<span data-ttu-id="86682-585">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-585">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-586">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-586">Example</span></span>

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
  CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
                (strcmp(resource, "/test.htm") == 0))
    {

        /* Found it, override the GET processing by sending the resource
    contents directly. */

        nx_http_server_callback_data_send(server_ptr,
    "HTTP/1.0 200 \r\nContent-Length:
    103\r\nContent-Type: text/html\r\n\r\n",
    63);

        nx_http_server_callback_data_send(server_ptr, "<HTML>\r\n<HEAD><TITLE>NetX
    HTTP Test </TITLE></HEAD>\r\n
    <BODY>\r\n<H1>NetX Test Page
    </H1>\r\n</BODY>\r\n</HTML>\r\n", 103);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_generate_response_header"></a><span data-ttu-id="86682-587">nx_http_server_callback_generate_response_header</span><span class="sxs-lookup"><span data-stu-id="86682-587">nx_http_server_callback_generate_response_header</span></span>

<span data-ttu-id="86682-588">Geri arama işlevinde yanıt üst bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="86682-588">Create a response header in a callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-589">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-589">Prototype</span></span>

```c
UINT nx_http_server_callback_generate_response_header(
                        NX_HTTP_SERVER *server_ptr,
                        NX_PACKET **packet_pptr,
                        CHAR *status_code, UINT content_length,
                        CHAR *content_type, CHAR* additional_header);
```

### <a name="description"></a><span data-ttu-id="86682-590">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-590">Description</span></span>

<span data-ttu-id="86682-591">Bu hizmet, HTTP sunucusu Istemci GET, put ve DELETE isteklerine yanıt verdiğinde iç işlevi *_nx_http_server_generate_response_header* çağırır.</span><span class="sxs-lookup"><span data-stu-id="86682-591">This service calls the internal function *_nx_http_server_generate_response_header* when the HTTP server responds to Client get, put and delete requests.</span></span> <span data-ttu-id="86682-592">HTTP sunucusu uygulaması Istemciye yanıtını tasarlarken HTTP sunucusu geri çağırma işlevlerinde kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-592">It is intended for use in HTTP server callback functions when the HTTP server application is designing its response to the Client.</span></span>

<span data-ttu-id="86682-593">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-593">This service is deprecated.</span></span> <span data-ttu-id="86682-594">Geliştiricilerin *nxd_http_server_callback_generate_response_header_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-594">Developers are encouraged to migrate to *nxd_http_server_callback_generate_response_header_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-595">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-595">Input Parameters</span></span>

 - <span data-ttu-id="86682-596">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-596">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-597">**packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-597">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
 - <span data-ttu-id="86682-598">**status_code** Kaynağın durumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="86682-598">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="86682-599">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="86682-599">Examples:</span></span>
    - <span data-ttu-id="86682-600">**NX_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="86682-600">**NX_HTTP_STATUS_OK**</span></span>
    - <span data-ttu-id="86682-601">**NX_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="86682-601">**NX_HTTP_STATUS_MODIFIED**</span></span>
    - <span data-ttu-id="86682-602">**NX_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="86682-602">**NX_HTTP_STATUS_INTERNAL_ERROR**</span></span>
 - <span data-ttu-id="86682-603">**CONTENT_LENGTH** İçerik boyutu (bayt)</span><span class="sxs-lookup"><span data-stu-id="86682-603">**content_length** Size of content in bytes</span></span>
 - <span data-ttu-id="86682-604">**content_type** HTTP türü, örneğin "metin/düz"</span><span class="sxs-lookup"><span data-stu-id="86682-604">**content_type** Type of HTTP e.g. “text/plain”</span></span>
 - <span data-ttu-id="86682-605">**additional_header** Ek üst bilgi metnine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-605">**additional_header** Pointer to additional header text</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-606">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-606">Return Values</span></span>

 - <span data-ttu-id="86682-607">**NX_SUCCESS** (0x00) başarıyla oluşturuldu üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="86682-607">**NX_SUCCESS** (0x00) Successfully created header</span></span>
 - <span data-ttu-id="86682-608">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-608">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-609">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-609">Allowed From</span></span>

<span data-ttu-id="86682-610">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-610">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-611">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-611">Example</span></span>

```c
CHAR demotestbuffer[] = "<html>\r\n\r\n<head>\r\n\r\n<title>Main   \
            Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n   \  </body>\r\n</html>\r\n";

     /* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
 CHAR *resource, NX_PACKET *recv_packet_ptr)
      {

NX_PACKET   *sresp_packet_ptr;
ULONG       string_length;
CHAR        temp_string[30];
ULONG       length = 0;


   length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length =  (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr ->
nx_http_server_request_resource, temp_string,
sizeof(temp_string));

       /* Null terminate the string. */
   temp_string[temp] = 0;

       /* Now build a response header with server status is OK and no additional header  
          info. */
   status = nx_http_server_callback_generate_response_header(http_server_ptr,
                  &resp_packet_ptr, NX_HTTP_STATUS_OK,
                  length, temp_string, NX_NULL);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
                 length,  server_ptr ->
                 nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
   if (status != NX_SUCCESS)
   {
       nx_packet_release(resp_packet_ptr);
       return status;
   }



/* Now send the packet! */
           status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
                                      resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);

   if (status != NX_SUCCESS)
   {
      nx_packet_release(resp_packet_ptr);

      return status;
   }

/* Let HTTP server know the response has been sent. */
  return NX_HTTP_CALLBACK_COMPLETED;

     }
```

## <a name="nx_http_server_callback_generate_response_header_extended"></a><span data-ttu-id="86682-612">nx_http_server_callback_generate_response_header_extended</span><span class="sxs-lookup"><span data-stu-id="86682-612">nx_http_server_callback_generate_response_header_extended</span></span>

<span data-ttu-id="86682-613">Geri arama işlevinde yanıt üst bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="86682-613">Create a response header in a callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-614">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-614">Prototype</span></span>

```c
UINT nx_http_server_callback_generate_response_header_extended(
                        NX_HTTP_SERVER *server_ptr,
                        NX_PACKET **packet_pptr,
                        CHAR *status_code, UINT status_code_length,
                        UINT content_length,
                        CHAR *content_type, UINT content_type_length,
                        CHAR *additional_header,
                        UINT additional_header_length);
```

### <a name="description"></a><span data-ttu-id="86682-615">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-615">Description</span></span>

<span data-ttu-id="86682-616">Bu hizmet, HTTP sunucusu Istemci GET, put ve DELETE isteklerine yanıt verdiğinde *_nx_http_server_generate_response_header ()* iç işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="86682-616">This service calls the internal function *_nx_http_server_generate_response_header()* when the HTTP server responds to Client get, put and delete requests.</span></span> <span data-ttu-id="86682-617">HTTP sunucusu uygulaması Istemciye yanıtını tasarlarken HTTP sunucusu geri çağırma işlevlerinde kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-617">It is intended for use in HTTP server callback functions when the HTTP server application is designing its response to the Client.</span></span>

<span data-ttu-id="86682-618">Bu hizmet *nx_http_server_callback_generate_response_header ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-618">This service replaces *nx_http_server_callback_generate_response_header()*.</span></span> <span data-ttu-id="86682-619">Bu sürüm, geri çağırma işlevine ek uzunluk bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="86682-619">This version supplies additional length information to the callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-620">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-620">Input Parameters</span></span>

 - <span data-ttu-id="86682-621">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-621">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-622">**packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-622">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
 - <span data-ttu-id="86682-623">**status_code** Kaynağın durumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="86682-623">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="86682-624">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="86682-624">Examples:</span></span>
    - <span data-ttu-id="86682-625">**NX_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="86682-625">**NX_HTTP_STATUS_OK**</span></span>
    - <span data-ttu-id="86682-626">**NX_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="86682-626">**NX_HTTP_STATUS_MODIFIED**</span></span>
    - <span data-ttu-id="86682-627">**NX_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="86682-627">**NX_HTTP_STATUS_INTERNAL_ERROR**</span></span>
 - <span data-ttu-id="86682-628">**status_code** Durum kodu uzunluğu</span><span class="sxs-lookup"><span data-stu-id="86682-628">**status_code** Length of status code</span></span>
 - <span data-ttu-id="86682-629">**CONTENT_LENGTH** İçerik boyutu (bayt)</span><span class="sxs-lookup"><span data-stu-id="86682-629">**content_length** Size of content in bytes</span></span>
 - <span data-ttu-id="86682-630">**content_type** HTTP türü, örneğin "metin/düz"</span><span class="sxs-lookup"><span data-stu-id="86682-630">**content_type** Type of HTTP e.g. “text/plain”</span></span>
 - <span data-ttu-id="86682-631">**content_type_length** HTTP türünün uzunluğu</span><span class="sxs-lookup"><span data-stu-id="86682-631">**content_type_length** Length of HTTP type</span></span>
 - <span data-ttu-id="86682-632">**additional_header** Ek üst bilgi metnine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-632">**additional_header** Pointer to additional header text</span></span>
 - <span data-ttu-id="86682-633">**additional_header_length** Ek üst bilgi metninin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="86682-633">**additional_header_length** Length of additional header text</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-634">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-634">Return Values</span></span>

 - <span data-ttu-id="86682-635">**NX_SUCCESS** (0x00) başarıyla oluşturuldu üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="86682-635">**NX_SUCCESS** (0x00) Successfully created header</span></span>
 - <span data-ttu-id="86682-636">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-636">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-637">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-637">Allowed From</span></span>

<span data-ttu-id="86682-638">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-638">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-639">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-639">Example</span></span>

```c
CHAR demotestbuffer[] = "<html>\r\n\r\n<head>\r\n\r\n<title>Main   \
     Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n   \  </body>\r\n</html>\r\n";

     /* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
 CHAR *resource, NX_PACKET *recv_packet_ptr)
      {

NX_PACKET   *sresp_packet_ptr;
ULONG       string_length;
CHAR        temp_string[30];
ULONG       length = 0;


   length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length =  (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr ->
nx_http_server_request_resource, temp_string,
sizeof(temp_string));

       /* Null terminate the string. */
   temp_string[temp] = 0;

       /* Now build a response header with server status is OK and no additional header  
          info. */
   status = nx_http_server_callback_generate_response_header_extended(
                             http_server_ptr, &resp_packet_ptr, NX_HTTP_STATUS_OK,
              sizeof(NX_HTTP_STATUS_OK) - 1, length,
              temp_string, string_length, NX_NULL, 0);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
                 length,  server_ptr ->
                 nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
   if (status != NX_SUCCESS)
   {
       nx_packet_release(resp_packet_ptr);
       return status;
   }



/* Now send the packet! */
           status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
                                      resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);

   if (status != NX_SUCCESS)
   {
      nx_packet_release(resp_packet_ptr);

      return status;
   }

/* Let HTTP server know the response has been sent. */
  return NX_HTTP_CALLBACK_COMPLETED;

     }
```

## <a name="nx_http_server_callback_packet_send"></a><span data-ttu-id="86682-640">nx_http_server_callback_packet_send</span><span class="sxs-lookup"><span data-stu-id="86682-640">nx_http_server_callback_packet_send</span></span>

<span data-ttu-id="86682-641">Geri çağırma işlevinden HTTP paketi gönder</span><span class="sxs-lookup"><span data-stu-id="86682-641">Send an HTTP packet from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-642">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-642">Prototype</span></span>

```c
UINT nx_http_server_callback_packet_send(NX_HTTP_SERVER *server_ptr,
                                         NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="86682-643">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-643">Description</span></span>

<span data-ttu-id="86682-644">Bu hizmet, HTTP geri çağrısından gelen bir HTTP Sunucu yanıtı gönderir.</span><span class="sxs-lookup"><span data-stu-id="86682-644">This service sends a complete HTTP server response from an HTTP callback.</span></span> <span data-ttu-id="86682-645">HTTP sunucusu, paketi NX_HTTP_SERVER _TIMEOUT_SEND gönderecek.</span><span class="sxs-lookup"><span data-stu-id="86682-645">HTTP server will send the packet with the NX_HTTP_SERVER _TIMEOUT_SEND.</span></span> <span data-ttu-id="86682-646">HTTP üst bilgisi ve verilerinin pakete eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="86682-646">The HTTP header and data must be appended to the packet.</span></span> <span data-ttu-id="86682-647">Dönüş durumu bir hata gösteriyorsa, HTTP uygulaması paketi serbest bırakmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-647">If the return status indicates an error, the HTTP application must release the packet.</span></span>

<span data-ttu-id="86682-648">Geri çağırma NX_HTTP_CALLBACK_COMPLETED döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="86682-648">The callback should return NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="86682-649">Daha ayrıntılı bir örnek için bkz. *nx_http_server_callback_generate_response_header ()* .</span><span class="sxs-lookup"><span data-stu-id="86682-649">See *nx_http_server_callback_generate_response_header()* for a more detailed example.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-650">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-650">Input Parameters</span></span>

 - <span data-ttu-id="86682-651">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-651">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-652">**packet_ptr** Gönderilmek üzere paket işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-652">**packet_ptr** Pointer to the packet to send</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-653">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-653">Return Values</span></span>

 - <span data-ttu-id="86682-654">**NX_SUCCESS** (0x00) sunucu paketi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="86682-654">**NX_SUCCESS** (0x00) Successfully sent Server packet</span></span>
 - <span data-ttu-id="86682-655">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-655">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-656">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-656">Allowed From</span></span>

<span data-ttu-id="86682-657">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-657">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-658">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-658">Example</span></span>

```c
/* The packet is appended with HTTP header and data and is ready to send to the
   Client directly. */

   status = nx_http_server_callback_response_send(server_ptr, packet_ptr);

   if (status != NX_SUCCESS)
   {

    nx_packet_release(packet_ptr);
   }

    return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_callback_response_send"></a><span data-ttu-id="86682-659">nx_http_server_callback_response_send</span><span class="sxs-lookup"><span data-stu-id="86682-659">nx_http_server_callback_response_send</span></span>

<span data-ttu-id="86682-660">Geri çağırma işlevinden yanıt gönder</span><span class="sxs-lookup"><span data-stu-id="86682-660">Send response from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-661">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-661">Prototype</span></span>

```c
UINT nx_http_server_callback_response_send(NX_HTTP_SERVER *server_ptr,
                                           CHAR *header,
                                           CHAR *information,
                                           CHAR additional_info);
```

### <a name="description"></a><span data-ttu-id="86682-662">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-662">Description</span></span>

<span data-ttu-id="86682-663">Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir.</span><span class="sxs-lookup"><span data-stu-id="86682-663">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="86682-664">Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86682-664">This is typically used to send custom responses associated with GET/POST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-665">Bu işlev kullanılırsa, geri çağırma yordamının NX_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="86682-665">If this function is used, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="86682-666">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-666">This service is deprecated.</span></span> <span data-ttu-id="86682-667">Geliştiricilerin *nxd_http_server_callback_response_send_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-667">Developers are encouraged to migrate to *nxd_http_server_callback_response_send_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-668">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-668">Input Parameters</span></span>

 - <span data-ttu-id="86682-669">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-669">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-670">**üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-670">**header** Pointer to the response header string.</span></span>
 - <span data-ttu-id="86682-671">**bilgi** Bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-671">**information** Pointer to the information string.</span></span>
 - <span data-ttu-id="86682-672">**additional_info** Ek bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-672">**additional_info** Pointer to the additional information string.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-673">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-673">Return Values</span></span>

 - <span data-ttu-id="86682-674">**NX_SUCCESS** (0x00) sunucu yanıtı başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="86682-674">**NX_SUCCESS** (0x00) Successfully sent Server response</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-675">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-675">Allowed From</span></span>

<span data-ttu-id="86682-676">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-676">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-677">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-677">Example</span></span>

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                        CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
               (strcmp(resource, "/test.htm") == 0))
    {

        /* In this example, we will complete the GET processing with
           a resource not found response. */
     nx_http_server_callback_response_send(server_ptr,
                      "HTTP/1.0 404 ",
                      "NetX HTTP Server unable to find  
                       file: ", resource);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_response_send_extended"></a><span data-ttu-id="86682-678">nx_http_server_callback_response_send_extended</span><span class="sxs-lookup"><span data-stu-id="86682-678">nx_http_server_callback_response_send_extended</span></span>

<span data-ttu-id="86682-679">Geri çağırma işlevinden yanıt gönder</span><span class="sxs-lookup"><span data-stu-id="86682-679">Send response from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-680">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-680">Prototype</span></span>

```c
UINT nx_http_server_callback_response_send_extended(
                                          NX_HTTP_SERVER *server_ptr,
                                          CHAR *header,
                                          UINT header_length,
                                          CHAR *information,
                                          UINT information_length,
                                          CHAR *additional_info,
                                          UINT additional_info_length);
```

### <a name="description"></a><span data-ttu-id="86682-681">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-681">Description</span></span>

<span data-ttu-id="86682-682">Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir.</span><span class="sxs-lookup"><span data-stu-id="86682-682">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="86682-683">Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86682-683">This is typically used to send custom responses associated with GET/POST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-684">Bu işlev kullanılırsa, geri çağırma yordamının NX_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="86682-684">If this function is used, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="86682-685">Bu hizmet *nx_http_server_callback_response_send ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-685">This service replaces *nx_http_server_callback_response_send()*.</span></span> <span data-ttu-id="86682-686">Bu sürüm, ek uzunluk bilgilerini bağımsız değişken olarak alır.</span><span class="sxs-lookup"><span data-stu-id="86682-686">This version takes additional length information as arguments.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-687">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-687">Input Parameters</span></span>

 - <span data-ttu-id="86682-688">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-688">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-689">**üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-689">**header** Pointer to the response header string.</span></span>
 - <span data-ttu-id="86682-690">**header_length** Yanıt üst bilgisi dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-690">**header_length** Length of the response header string.</span></span>
 - <span data-ttu-id="86682-691">**bilgi** Bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-691">**information** Pointer to the information string.</span></span>
 - <span data-ttu-id="86682-692">**information_length** Bilgi dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-692">**information_length** Length of the information string.</span></span>
 - <span data-ttu-id="86682-693">**additional_info** Ek bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-693">**additional_info** Pointer to the additional information string.</span></span>
 - <span data-ttu-id="86682-694">**additional_info_length** Ek bilgi dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="86682-694">**additional_info_length** Length of the additional information string.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-695">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-695">Return Values</span></span>

 - <span data-ttu-id="86682-696">**NX_SUCCESS** (0x00) sunucu yanıtı başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="86682-696">**NX_SUCCESS** (0x00) Successfully sent Server response</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-697">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-697">Allowed From</span></span>

<span data-ttu-id="86682-698">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-698">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-699">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-699">Example</span></span>

```c
UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                        CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource!  */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
               (strcmp(resource, "/test.htm") == 0))
    {

        /* In this example, we will complete the GET processing with
           a resource not found response. */
     nx_http_server_callback_response_send_extended(
                                             server_ptr,
                      "HTTP/1.0 404 ", 12,
                      "NetX HTTP Server unable to find  
                       file: ", 38, resource, 9);

        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_content_get"></a><span data-ttu-id="86682-700">nx_http_server_content_get</span><span class="sxs-lookup"><span data-stu-id="86682-700">nx_http_server_content_get</span></span>

<span data-ttu-id="86682-701">İstekten içerik al</span><span class="sxs-lookup"><span data-stu-id="86682-701">Get content from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-702">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-702">Prototype</span></span>

```c
UINT nx_http_server_content_get(NX_HTTP_SERVER *server_ptr,
                                NX_PACKET *packet_ptr,
                                ULONG byte_offset,
                                CHAR *destination_ptr,
                                UINT destination_size,
                                UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="86682-703">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-703">Description</span></span>

<span data-ttu-id="86682-704">Bu hizmet, POST veya PUT HTTP Client isteğinden belirtilen miktarda içeriği almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-704">This service attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="86682-705">HTTP sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağrısından (*nx_http_server_create*) çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-705">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create*).</span></span>

<span data-ttu-id="86682-706">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-706">This service is deprecated.</span></span> <span data-ttu-id="86682-707">Geliştiricilerin *nx_http_server_content_get_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-707">Developers are encouraged to migrate to *nx_http_server_content_get_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-708">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-708">Input Parameters</span></span>

 - <span data-ttu-id="86682-709">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-709">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-710">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-710">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="86682-711">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-711">Note that this packet must not be released by the request notify callback.</span></span>
 - <span data-ttu-id="86682-712">**byte_offset** İçerik alanına kaydırılacağı bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="86682-712">**byte_offset** Number of bytes to offset into the content area.</span></span>
 - <span data-ttu-id="86682-713">**destination_ptr** İçerik için hedef alana yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-713">**destination_ptr** Pointer to the destination area for the content.</span></span>
 - <span data-ttu-id="86682-714">**destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="86682-714">**destination_size** Maximum number of bytes available in the destination area.</span></span>
 - <span data-ttu-id="86682-715">**actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-715">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-716">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-716">Return Values</span></span>

 - <span data-ttu-id="86682-717">**NX_SUCCESS** (0x00) başarılı http sunucusu içerik al</span><span class="sxs-lookup"><span data-stu-id="86682-717">**NX_SUCCESS** (0x00) Successful HTTP Server content get</span></span>
 - <span data-ttu-id="86682-718">**NX_HTTP_ERROR** (0xE0) http sunucusu iç hatası</span><span class="sxs-lookup"><span data-stu-id="86682-718">**NX_HTTP_ERROR** (0xE0) HTTP Server internal error</span></span>
 - <span data-ttu-id="86682-719">**NX_HTTP_DATA_END** (0xE7) Istek içeriğinin sonu</span><span class="sxs-lookup"><span data-stu-id="86682-719">**NX_HTTP_DATA_END** (0xE7) End of request content</span></span>
 - <span data-ttu-id="86682-720">**NX_HTTP_TIMEOUT** (0XE1) sonraki içerik paketini alma sırasında http sunucusu zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="86682-720">**NX_HTTP_TIMEOUT** (0xE1) HTTP Server timeout in getting next packet of content</span></span>
 - <span data-ttu-id="86682-721">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-721">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-722">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-722">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-723">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-723">Allowed From</span></span>

<span data-ttu-id="86682-724">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-724">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-725">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-725">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, retrieve up to 100 bytes of content starting at offset
   0. */
status =  nx_http_server_content_get(&my_server, packet_ptr,
                      0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
   request content. */
```

## <a name="nx_http_server_content_get_extended"></a><span data-ttu-id="86682-726">nx_http_server_content_get_extended</span><span class="sxs-lookup"><span data-stu-id="86682-726">nx_http_server_content_get_extended</span></span>

<span data-ttu-id="86682-727">İstekten içerik al/sıfır uzunlukta Içerik uzunluğunu destekler</span><span class="sxs-lookup"><span data-stu-id="86682-727">Get content from the request/supports zero length Content Length</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-728">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-728">Prototype</span></span>

```c
UINT nx_http_server_content_get_extended(NX_HTTP_SERVER *server_ptr,
                                         NX_PACKET *packet_ptr,
                                         ULONG byte_offset,
                                         CHAR *destination_ptr,
                                         UINT destination_size,
                                         UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="86682-729">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-729">Description</span></span>

<span data-ttu-id="86682-730">Bu hizmet neredeyse *nx_http_server_content_get ()* ile AYNıDıR; Post veya put http Client isteğinden belirtilen miktarda içeriği almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-730">This service is almost identical to *nx_http_server_content_get();* it attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="86682-731">Ancak, geçerli bir istek olarak sıfır değeri (' boş istek ') Içerik uzunluğundaki istekleri işler.</span><span class="sxs-lookup"><span data-stu-id="86682-731">However it handles requests with Content Length of zero value (‘empty request’) as a valid request.</span></span> <span data-ttu-id="86682-732">Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-732">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="86682-733">Bu hizmet *nx_http_server_content_get ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-733">This service replaces *nx_http_server_content_get()*.</span></span> <span data-ttu-id="86682-734">Bu sürüm, çağıranın ek uzunluk bilgileri sağlaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86682-734">This version requires caller to supply additional length information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-735">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-735">Input Parameters</span></span>

 - <span data-ttu-id="86682-736">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-736">**server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-737">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-737">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="86682-738">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-738">Note that this packet must not be released by the request notify callback.</span></span>
 - <span data-ttu-id="86682-739">**byte_offset** İçerik alanına kaydırılacağı bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="86682-739">**byte_offset** Number of bytes to offset into the content area.</span></span>
 - <span data-ttu-id="86682-740">**destination_ptr** İçerik için hedef alana yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-740">**destination_ptr** Pointer to the destination area for the content.</span></span>
 - <span data-ttu-id="86682-741">**destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="86682-741">**destination_size** Maximum number of bytes available in the destination area.</span></span>
 - <span data-ttu-id="86682-742">**actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-742">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-743">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-743">Return Values</span></span>

 - <span data-ttu-id="86682-744">**NX_SUCCESS** (0x00) başarılı http içerik al</span><span class="sxs-lookup"><span data-stu-id="86682-744">**NX_SUCCESS** (0x00) Successful HTTP content get</span></span>
 - <span data-ttu-id="86682-745">**NX_HTTP_ERROR** (0xE0) http sunucusu iç hatası</span><span class="sxs-lookup"><span data-stu-id="86682-745">**NX_HTTP_ERROR** (0xE0) HTTP Server internal error</span></span>
 - <span data-ttu-id="86682-746">**NX_HTTP_DATA_END** (0xE7) Istek içeriğinin sonu</span><span class="sxs-lookup"><span data-stu-id="86682-746">**NX_HTTP_DATA_END** (0xE7) End of request content</span></span>
 - <span data-ttu-id="86682-747">**NX_HTTP_TIMEOUT** (0XE1) sonraki paketi alma sırasında http sunucusu zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="86682-747">**NX_HTTP_TIMEOUT** (0xE1) HTTP Server timeout in getting next packet</span></span>
 - <span data-ttu-id="86682-748">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-748">NX_PTR_ERROR (0x07) Invalid  pointer input</span></span>
 - <span data-ttu-id="86682-749">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-749">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-750">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-750">Allowed From</span></span>

<span data-ttu-id="86682-751">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-751">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-752">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-752">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, retrieve up to 100 bytes of content starting at offset
   0. */
status =  nx_http_server_content_get_extended(&my_server, packet_ptr,
                               0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
   request content. */
```

## <a name="nx_http_server_content_length_get"></a><span data-ttu-id="86682-753">nx_http_server_content_length_get</span><span class="sxs-lookup"><span data-stu-id="86682-753">nx_http_server_content_length_get</span></span>

<span data-ttu-id="86682-754">İstekteki içerik uzunluğunu al</span><span class="sxs-lookup"><span data-stu-id="86682-754">Get length of content in the request</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-755">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-755">Prototype</span></span>

```c
UINT nx_http_server_content_length_get(NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="86682-756">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-756">Description</span></span>

<span data-ttu-id="86682-757">Bu hizmet, sağlanan paketteki HTTP içerik uzunluğunu almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="86682-757">This service attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="86682-758">HTTP içeriği yoksa, bu yordam sıfır değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="86682-758">If there is no HTTP content, this routine returns a value of zero.</span></span> <span data-ttu-id="86682-759">Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-759">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="86682-760">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-760">This service is deprecated.</span></span> <span data-ttu-id="86682-761">Geliştiricilerin *nx_http_server_content_length_get_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-761">Developers are encouraged to migrate to *nx_http_server_content_length_get_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-762">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-762">Input Parameters</span></span>

 - <span data-ttu-id="86682-763">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-763">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="86682-764">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-764">Note that this packet must not be released by the request notify callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-765">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-765">Return Values</span></span>

 - <span data-ttu-id="86682-766">**içerik uzunluğu** Hatada, sıfır değeri döndürülür</span><span class="sxs-lookup"><span data-stu-id="86682-766">**content length** On error, a value of zero is returned</span></span>  

### <a name="allowed-from"></a><span data-ttu-id="86682-767">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-767">Allowed From</span></span>

<span data-ttu-id="86682-768">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-768">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-769">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-769">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, get the content length of the HTTP Client request. */
length =  nx_http_server_content_length_get(packet_ptr);

/* The “length” variable now contains the length of the HTTP Client
   request content area. */
```

## <a name="nx_http_server_content_length_get_extended"></a><span data-ttu-id="86682-770">nx_http_server_content_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="86682-770">nx_http_server_content_length_get_extended</span></span>

<span data-ttu-id="86682-771">İstekteki içerik uzunluğunu al/sıfır değerinin Içerik uzunluğunu destekler</span><span class="sxs-lookup"><span data-stu-id="86682-771">Get length of content in the request/supports Content Length of zero value</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-772">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-772">Prototype</span></span>

```c
UINT nx_http_server_content_length_get_extended(NX_PACKET *packet_ptr,
                                                UINT *content_length);
```

### <a name="description"></a><span data-ttu-id="86682-773">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-773">Description</span></span>

<span data-ttu-id="86682-774">Bu hizmet *nx_http_server_content_length_get benzerdir;* sağlanan paketteki http içerik uzunluğunu alma girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="86682-774">This service is similar to *nx_http_server_content_length_get;* attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="86682-775">Ancak, dönüş değeri başarıyla tamamlanma durumunu gösterir ve giriş İşaretçisinde gerçek uzunluk değeri döndürülür ```content_length``` .</span><span class="sxs-lookup"><span data-stu-id="86682-775">However, the return value indicates successful completion status, and the actual length value is returned in the input pointer ```content_length```.</span></span> <span data-ttu-id="86682-776">HTTP içeriği/Içerik uzunluğu = 0 yoksa, bu yordam yine de başarılı bir tamamlanma durumu döndürür ve content_length giriş işaretçisi geçerli bir uzunluğa (sıfır) işaret eder.</span><span class="sxs-lookup"><span data-stu-id="86682-776">If there is no HTTP content/Content Length = 0, this routine still returns a successful completion status and the content_length input pointer points to a valid length (zero).</span></span> <span data-ttu-id="86682-777">HTTP sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağrısından (*nx_http_server_create*) çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-777">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create*).</span></span>

<span data-ttu-id="86682-778">Bu hizmet *nx_http_server_content_length_get ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-778">This service replaces *nx_http_server_content_length_get()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-779">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-779">Input Parameters</span></span>

 - <span data-ttu-id="86682-780">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-780">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="86682-781">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-781">Note that this packet must not be released by the request notify callback.</span></span>
 - <span data-ttu-id="86682-782">**CONTENT_LENGTH** Içerik uzunluğu alanından alınan değer işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-782">**content_length** Pointer to value retrieved from Content Length field</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-783">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-783">Return Values</span></span>

 - <span data-ttu-id="86682-784">**NX_SUCCESS** (0x00) başarılı sunucu içeriği al</span><span class="sxs-lookup"><span data-stu-id="86682-784">**NX_SUCCESS** (0x00) Successful Server content get</span></span>
 - <span data-ttu-id="86682-785">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) yanlış http üst bilgi biçimi</span><span class="sxs-lookup"><span data-stu-id="86682-785">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Improper HTTP header format</span></span>
 - <span data-ttu-id="86682-786">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-786">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-787">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-787">Allowed From</span></span>

<span data-ttu-id="86682-788">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-788">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-789">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-789">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, get the content length of the HTTP Client request. */
ULONG content_length;

status =  nx_http_server_content_length_get_extended(packet_ptr, &content_length);

/* If the “status” variable indicates successful completion, the“length” variable
   contains the length of the HTTP Client request content area. */
```

## <a name="nx_http_server_create"></a><span data-ttu-id="86682-790">nx_http_server_create</span><span class="sxs-lookup"><span data-stu-id="86682-790">nx_http_server_create</span></span>

<span data-ttu-id="86682-791">HTTP sunucusu örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="86682-791">Create an HTTP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-792">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-792">Prototype</span></span>

```c
UINT nx_http_server_create(NX_HTTP_SERVER *http_server_ptr,
      CHAR *http_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr,
      VOID *stack_ptr, ULONG stack_size, NX_PACKET_POOL *pool_ptr,
      UINT (*authentication_check)(NX_HTTP_SERVER *server_ptr,
            UINT request_type, CHAR *resource, CHAR **name,
            CHAR **password, CHAR **realm),
      UINT (*request_notify)(NX_HTTP_SERVER *server_ptr,
            UINT request_type, CHAR *resource, NX_PACKET *packet_ptr));
```

### <a name="description"></a><span data-ttu-id="86682-793">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-793">Description</span></span>

<span data-ttu-id="86682-794">Bu hizmet kendi ThreadX iş parçacığı bağlamında çalışan bir HTTP sunucu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86682-794">This service creates an HTTP Server instance, which runs in the context of its own ThreadX thread.</span></span> <span data-ttu-id="86682-795">İsteğe bağlı *authentication_check* ve request_notify uygulama geri çağırma yordamları, HTTP sunucusunun temel işlemleri üzerinde uygulama yazılım denetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="86682-795">The optional *authentication_check* and request_notify application callback routines give the application software control over the basic operations of the HTTP Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-796">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-796">Input Parameters</span></span>

 - <span data-ttu-id="86682-797">**http_server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-797">**http_server_ptr** Pointer to HTTP Server control block.</span></span>
 - <span data-ttu-id="86682-798">**http_server_name** HTTP sunucusu adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-798">**http_server_name** Pointer to HTTP Server’s name.</span></span>
 - <span data-ttu-id="86682-799">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-799">**ip_ptr** Pointer to previously created IP instance.</span></span>
 - <span data-ttu-id="86682-800">**media_ptr** Daha önce oluşturulan FileX medya örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-800">**media_ptr** Pointer to previously created FileX media instance.</span></span>
 - <span data-ttu-id="86682-801">**stack_ptr** HTTP sunucusu iş parçacığı yığın alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-801">**stack_ptr** Pointer to HTTP Server thread stack area.</span></span>
 - <span data-ttu-id="86682-802">**stack_size** HTTP sunucusu iş parçacığı yığın boyutu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-802">**stack_size** Pointer to HTTP Server thread stack size.</span></span>
 - <span data-ttu-id="86682-803">**authentication_check** Uygulamanın kimlik doğrulama denetimi yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-803">**authentication_check** Function pointer to application’s authentication checking routine.</span></span> <span data-ttu-id="86682-804">Belirtilmişse, bu yordam her HTTP Istemci isteği için çağırılır.</span><span class="sxs-lookup"><span data-stu-id="86682-804">If specified, this routine is called for each HTTP Client request.</span></span> <span data-ttu-id="86682-805">Bu parametre NULL ise, kimlik doğrulaması gerçekleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="86682-805">If this parameter is NULL, no authentication will be performed.</span></span>
 - <span data-ttu-id="86682-806">**request_notify** Uygulamanın istek bildirim yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-806">**request_notify** Function pointer to application’s request notify routine.</span></span> <span data-ttu-id="86682-807">Belirtilmişse, bu yordam isteğin HTTP sunucu işlemeden önce çağırılır.</span><span class="sxs-lookup"><span data-stu-id="86682-807">If specified, this routine is called prior to the HTTP server processing of the request.</span></span> <span data-ttu-id="86682-808">Bu, HTTP Istemci isteği tamamlanmadan önce kaynak adının yeniden yönlendirilmesine veya bir kaynak içindeki alanların güncelleştirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="86682-808">This allows the resource name to be redirected or fields within a resource to be updated prior to completing the HTTP Client request.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-809">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-809">Return Values</span></span>

 - <span data-ttu-id="86682-810">**NX_SUCCESS** (0x00) başarılı http sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="86682-810">**NX_SUCCESS** (0x00) Successful HTTP Server create.</span></span>
 - <span data-ttu-id="86682-811">NX_PTR_ERROR (0x07) geçersiz HTTP sunucusu, IP, medya, yığın veya paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-811">NX_PTR_ERROR (0x07) Invalid HTTP Server, IP, media, stack, or packet pool pointer.</span></span>
 - <span data-ttu-id="86682-812">NX_HTTP_POOL_ERROR (0xE9) havuzun paket yükü, tüm HTTP isteklerini içerecek kadar büyük değil.</span><span class="sxs-lookup"><span data-stu-id="86682-812">NX_HTTP_POOL_ERROR (0xE9) Packet payload of pool is not large enough to contain complete HTTP request.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-813">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-813">Allowed From</span></span>

<span data-ttu-id="86682-814">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-814">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-815">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-815">Example</span></span>

```c
/* Create an HTTP Server instance called “my_server.”  */
status =  nx_http_server_create(&my_server, “my server”, &ip_0, &ram_disk,
              stack_ptr, stack_size, &pool_0,
              my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_http_server_delete"></a><span data-ttu-id="86682-816">nx_http_server_delete</span><span class="sxs-lookup"><span data-stu-id="86682-816">nx_http_server_delete</span></span>

<span data-ttu-id="86682-817">HTTP sunucusu örneğini silme</span><span class="sxs-lookup"><span data-stu-id="86682-817">Delete an HTTP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-818">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-818">Prototype</span></span>

```c
UINT nx_http_server_delete(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="86682-819">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-819">Description</span></span>

<span data-ttu-id="86682-820">Bu hizmet, önceden oluşturulmuş bir HTTP sunucusu örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="86682-820">This service deletes a previously created HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-821">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-821">Input Parameters</span></span>

 - <span data-ttu-id="86682-822">**http_server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-822">**http_server_ptr** Pointer to HTTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-823">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-823">Return Values</span></span>

 - <span data-ttu-id="86682-824">**NX_SUCCESS** (0x00) başarılı http sunucusu silme</span><span class="sxs-lookup"><span data-stu-id="86682-824">**NX_SUCCESS** (0x00) Successful HTTP Server delete</span></span>
 - <span data-ttu-id="86682-825">NX_PTR_ERROR (0x07) geçersiz HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-825">NX_PTR_ERROR (0x07) Invalid HTTP Server pointer</span></span>
 - <span data-ttu-id="86682-826">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-826">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-827">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-827">Allowed From</span></span>

<span data-ttu-id="86682-828">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-828">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-829">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-829">Example</span></span>

```c
/* Delete the HTTP Server instance called “my_server.”  */
status =  nx_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_http_server_get_entity_content"></a><span data-ttu-id="86682-830">nx_http_server_get_entity_content</span><span class="sxs-lookup"><span data-stu-id="86682-830">nx_http_server_get_entity_content</span></span>

<span data-ttu-id="86682-831">Varlık verilerinin konumunu ve uzunluğunu alma</span><span class="sxs-lookup"><span data-stu-id="86682-831">Retrieve the location and length of entity data</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-832">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-832">Prototype</span></span>

```c
UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_pptr,
                                       ULONG *available_offset,
                                       ULONG *available_length);
```

### <a name="description"></a><span data-ttu-id="86682-833">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-833">Description</span></span>

<span data-ttu-id="86682-834">Bu hizmet, alınan Istemci iletilerindeki geçerli çok parçalı varlıktaki verilerin başlangıç konumunu ve sınır dizesini dahil olmayan veri uzunluğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="86682-834">This service determines the location of the start of data within the current multipart entity in the received Client messages, and the length of data not including the boundary string.</span></span> <span data-ttu-id="86682-835">Dahili HTTP sunucusu, bu işlevin birden çok varlığa sahip iletiler için aynı Istemci veri biriminde yeniden çağrılabilmesi için kendi uzaklıklarını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="86682-835">Internally HTTP server updates its own offsets so that this function can be called again on the same Client datagram for messages with multiple entities.</span></span> <span data-ttu-id="86682-836">Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="86682-836">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-837">Bu hizmeti kullanmak için NX_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="86682-837">NX_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span>

<span data-ttu-id="86682-838">Daha fazla bilgi için bkz. [*nx_http_server_get_entity_header*](#nx_http_server_get_entity_header) .</span><span class="sxs-lookup"><span data-stu-id="86682-838">See [*nx_http_server_get_entity_header*](#nx_http_server_get_entity_header) for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-839">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-839">Input Parameters</span></span>

 - <span data-ttu-id="86682-840">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-840">**server_ptr** Pointer to HTTP Server</span></span>
 - <span data-ttu-id="86682-841">**packet_pptr** Paket işaretçisinin konumu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-841">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="86682-842">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86682-842">Note that the application should not release this packet.</span></span>
 - <span data-ttu-id="86682-843">**available_offset** Paket önüne işaretçisinden varlık verilerinin uzaklığa yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-843">**available_offset** Pointer to offset of entity data from the packet prepend pointer</span></span>
 - <span data-ttu-id="86682-844">**available_length** Varlık verisi uzunluğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-844">**available_length** Pointer to length of entity data</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-845">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-845">Return Values</span></span>

 - <span data-ttu-id="86682-846">**NX_SUCCESS** (0x00) varlık içeriğinin boyutunu ve konumunu başarıyla aldı</span><span class="sxs-lookup"><span data-stu-id="86682-846">**NX_SUCCESS** (0x00) Successfully retrieved size and location of entity content</span></span>
 - <span data-ttu-id="86682-847">HTTP sunucusu iç çok parçalı işaretçiler için **NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xf4) içeriği zaten var</span><span class="sxs-lookup"><span data-stu-id="86682-847">**NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) Content for the HTTP server  internal multipart markers is already found</span></span>
 - <span data-ttu-id="86682-848">NX_HTTP_ERROR (0xE0) Iç HTTP hatası</span><span class="sxs-lookup"><span data-stu-id="86682-848">NX_HTTP_ERROR (0xE0) Internal HTTP error</span></span>
 - <span data-ttu-id="86682-849">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-849">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-850">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-850">Allowed From</span></span>

<span data-ttu-id="86682-851">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-851">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-852">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-852">Example</span></span>

```c
NX_HTTP_SERVER my_server;

UINT        offset, length;
NX_PACKET  *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
   the entity header to determine details about the multipart data. If
   successful, it then calls this service to get the location of entity data: */

status =  nx_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
&length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
   entity data. */
```

## <a name="nx_http_server_get_entity_header"></a><span data-ttu-id="86682-853">nx_http_server_get_entity_header</span><span class="sxs-lookup"><span data-stu-id="86682-853">nx_http_server_get_entity_header</span></span>

<span data-ttu-id="86682-854">Varlık üstbilgisinin içeriğini alma</span><span class="sxs-lookup"><span data-stu-id="86682-854">Retrieve the contents of entity header</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-855">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-855">Prototype</span></span>

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      UCHAR *entity_header_buffer,
                                      ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="86682-856">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-856">Description</span></span>

<span data-ttu-id="86682-857">Bu hizmet varlık üstbilgisini belirtilen arabelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="86682-857">This service retrieves the entity header into the specified buffer.</span></span> <span data-ttu-id="86682-858">Dahili HTTP sunucusu, birden çok varlık üst bilgilerine sahip bir Istemci veri biriminde bir sonraki çok parçalı varlığı bulmak için kendi işaretçilerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="86682-858">Internally HTTP Server updates its own pointers to locate the next multipart entity in a Client datagram with multiple entity headers.</span></span> <span data-ttu-id="86682-859">Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="86682-859">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-860">Bu hizmeti kullanmak için NX_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="86682-860">NX_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-861">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-861">Input Parameters</span></span>

 - <span data-ttu-id="86682-862">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-862">**server_ptr** Pointer to HTTP Server</span></span>
 - <span data-ttu-id="86682-863">**packet_pptr** Paket işaretçisinin konumu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-863">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="86682-864">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86682-864">Note that the application should not release this packet.</span></span>
 - <span data-ttu-id="86682-865">**entity_header_buffer** Varlık üstbilgisinin depolanacak konuma işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-865">**entity_header_buffer** Pointer to location to store entity header</span></span>
 - <span data-ttu-id="86682-866">**Buffer_size** Giriş arabelleğinin boyutu</span><span class="sxs-lookup"><span data-stu-id="86682-866">**buffer_size** Size of input buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-867">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-867">Return Values</span></span>

 - <span data-ttu-id="86682-868">**NX_SUCCESS** (0x00) varlık Heade başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="86682-868">**NX_SUCCESS** (0x00) Successfully retrieved entity heade</span></span>
 - <span data-ttu-id="86682-869">**NX_HTTP_NOT_FOUND** **(0xE6)** varlık üst bilgisi alanı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="86682-869">**NX_HTTP_NOT_FOUND** **(0xE6)** Entity header field not found</span></span>
 - <span data-ttu-id="86682-870">Çok müşterili istemci ileti için sonraki paketi almak üzere **NX_HTTP_TIMEOUT** **(0XE1)** süresi geçildi</span><span class="sxs-lookup"><span data-stu-id="86682-870">**NX_HTTP_TIMEOUT** **(0xE1)** Time expired to receive next packet for multipacket client message</span></span>
 - <span data-ttu-id="86682-871">NX_HTTP_ERROR (0xE0) Iç HTTP hatası</span><span class="sxs-lookup"><span data-stu-id="86682-871">NX_HTTP_ERROR (0xE0) Internal HTTP error</span></span>
 - <span data-ttu-id="86682-872">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-872">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-873">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-873">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-874">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-874">Allowed From</span></span>

<span data-ttu-id="86682-875">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-875">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-876">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-876">Example</span></span>

```c
/* my_request_notify is the application request notify callback registered with
      the HTTP server in nx_http_server_create, creates a response to the received  
      Client request. */

      UINT  my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                              CHAR *resource, NX_PACKET *packet_ptr)
      {

        NX_PACKET   *sresp_packet_ptr;
        UINT        offset, length;
        NX_PACKET   *response_pkt;
        UCHAR       buffer[1440];

        /* Process multipart data. */
        if(request_type == NX_HTTP_SERVER_POST_REQUEST)
        {

       /* Get the content header. */
       while(nx_http_server_get_entity_header(server_ptr, &packet_ptr, buffer,
                                         sizeof(buffer)) == NX_SUCCESS)
   {

      /* Header obtained successfully. Get the content data location. */
      while(nx_http_server_get_entity_content(server_ptr, &packet_ptr, &offset,
                                              &length) == NX_SUCCESS)
      {
           /* Write content data to buffer. */
           nx_packet_data_extract_offset(packet_ptr, offset, buffer, length,
                                         &length);
           buffer[length] = 0;
      }

    }

    /* Generate HTTP header. */
    status = nx_http_server_callback_generate_response_header(server_ptr,
                         &response_pkt, NX_HTTP_STATUS_OK, 800, "text/html",
                         "Server: NetXDuo HTTP 5.3\r\n");

    if(status == NX_SUCCESS)
    {
        if(nx_http_server_callback_packet_send(server_ptr, response_pkt) !=
  NX_SUCCESS)
 {
                nx_packet_release(response_pkt);
     }
    }


}
else
{
    /* Indicate we have not processed the response to client yet.*/
    return(NX_SUCCESS);
}

/* Indicate the response to client is transmitted. */
return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_gmt_callback_set"></a><span data-ttu-id="86682-877">nx_http_server_gmt_callback_set</span><span class="sxs-lookup"><span data-stu-id="86682-877">nx_http_server_gmt_callback_set</span></span>

<span data-ttu-id="86682-878">GMT Tarih ve saati almak için geri aramayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="86682-878">Set the callback to obtain GMT date and time</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-879">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-879">Prototype</span></span>

```c
UINT nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                     VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

### <a name="description"></a><span data-ttu-id="86682-880">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-880">Description</span></span>

<span data-ttu-id="86682-881">Bu hizmet, daha önce oluşturulmuş bir HTTP sunucusu ile GMT Tarih ve saati alacak şekilde geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="86682-881">This service sets the callback to obtain GMT date and time with a previously created HTTP server.</span></span> <span data-ttu-id="86682-882">Bu hizmet HTTP sunucusu, Istemciye HTTP sunucu yanıtlarında bir üst bilgi oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="86682-882">This service is invoked with the HTTP server is creating a header in HTTP server responses to the Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-883">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-883">Input Parameters</span></span>

 - <span data-ttu-id="86682-884">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-884">**server_ptr** Pointer to HTTP Server</span></span>
 - <span data-ttu-id="86682-885">**gmt_getv** GMT geri çağırması işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-885">**gmt_getv** Pointer to GMT callback</span></span>
 - <span data-ttu-id="86682-886">**Tarih v** Alınan tarihin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-886">**datev** Pointer to the date retrieved</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-887">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-887">Return Values</span></span>

 - <span data-ttu-id="86682-888">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="86682-888">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="86682-889">NX_PTR_ERROR (0x07) geçersiz paket veya parametre işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-889">NX_PTR_ERROR (0x07)  Invalid packet or parameter pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-890">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-890">Allowed From</span></span>

<span data-ttu-id="86682-891">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-891">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-892">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-892">Example</span></span>

```c
NX_HTTP_SERVER my_server;

VOID get_gmt(NX_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the GMT
   retrieve callback: */

status =  nx_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
   response header date. */
```

## <a name="nx_http_server_invalid_userpassword_notify_set"></a><span data-ttu-id="86682-893">nx_http_server_invalid_userpassword_notify_set</span><span class="sxs-lookup"><span data-stu-id="86682-893">nx_http_server_invalid_userpassword_notify_set</span></span>

<span data-ttu-id="86682-894">Geri çağırma işlemini geçersiz kullanıcı/parola işleyecek şekilde ayarla</span><span class="sxs-lookup"><span data-stu-id="86682-894">Set the callback to to handle invalid user/password</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-895">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-895">Prototype</span></span>

```c
UINT nx_http_server_invalid_userpassword_notify_set(
            NX_HTTP_SERVER *http_server_ptr,
            UINT (*invalid_username_password_callback)
                        (CHAR *resource,
                        NXD_ADDRESS *client_address,
                        UINT request_type));
```

### <a name="description"></a><span data-ttu-id="86682-896">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-896">Description</span></span>

<span data-ttu-id="86682-897">Bu hizmet, bir Istemci alma, yerleştirme veya silme isteğinde, Özet veya temel kimlik doğrulamasından göre geçersiz bir Kullanıcı adı ve parola alındığında çağrılan geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="86682-897">This service sets the callback invoked when an invalid username and password is received in a Client get, put or delete request, either by digest or basic authentication.</span></span> <span data-ttu-id="86682-898">HTTP sunucusu daha önce oluşturulmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-898">The HTTP server must be previously created.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-899">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-899">Input Parameters</span></span>

 - <span data-ttu-id="86682-900">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-900">**server_ptr** Pointer to HTTP Server</span></span>
 - <span data-ttu-id="86682-901">**invalid_username_password_callback** Geçersiz Kullanıcı/geçiş geri çağırması işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-901">**invalid_username_password_callback** Pointer to invalid user/pass callback</span></span>
 - <span data-ttu-id="86682-902">**kaynak** İstemci tarafından belirtilen kaynak işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-902">**resource** Pointer to the resource specified by the client</span></span>
 - <span data-ttu-id="86682-903">**client_address** İstemci adresi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="86682-903">**client_address** Pointer to client address.</span></span> <span data-ttu-id="86682-904">IPv4 veya IPv6 olabilir</span><span class="sxs-lookup"><span data-stu-id="86682-904">Can be IPv4 or IPv6</span></span>
 - <span data-ttu-id="86682-905">**request_type** İstemci isteği türünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="86682-905">**request_type** Indicates client request type.</span></span> <span data-ttu-id="86682-906">Belki:</span><span class="sxs-lookup"><span data-stu-id="86682-906">May be:</span></span>
    - <span data-ttu-id="86682-907">NX_HTTP_SERVER_GET_REQUEST</span><span class="sxs-lookup"><span data-stu-id="86682-907">NX_HTTP_SERVER_GET_REQUEST</span></span>
    - <span data-ttu-id="86682-908">NX_HTTP_SERVER_POST_REQUEST</span><span class="sxs-lookup"><span data-stu-id="86682-908">NX_HTTP_SERVER_POST_REQUEST</span></span>
    - <span data-ttu-id="86682-909">NX_HTTP_SERVER_HEAD_REQUEST</span><span class="sxs-lookup"><span data-stu-id="86682-909">NX_HTTP_SERVER_HEAD_REQUEST</span></span>
    - <span data-ttu-id="86682-910">NX_HTTP_SERVER_PUT_REQUEST</span><span class="sxs-lookup"><span data-stu-id="86682-910">NX_HTTP_SERVER_PUT_REQUEST</span></span>
    - <span data-ttu-id="86682-911">NX_HTTP_SERVER_DELETE_REQUEST</span><span class="sxs-lookup"><span data-stu-id="86682-911">NX_HTTP_SERVER_DELETE_REQUEST</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-912">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-912">Return Values</span></span>

 - <span data-ttu-id="86682-913">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="86682-913">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="86682-914">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-914">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-915">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-915">Allowed From</span></span>

<span data-ttu-id="86682-916">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-916">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-917">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-917">Example</span></span>

```c
NX_HTTP_SERVER my_server;
VOID invalid_username_password_callback (NX_ CHAR *resource,
                                         NXD_ADDRESS *client_address,
                                         UINT   request_type);

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the invalid
   username password callback: */

status =  nx_http_server_gmt_callback_set(&my_server,
                                          invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
   will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_http_server_mime_maps_additional_set"></a><span data-ttu-id="86682-918">nx_http_server_mime_maps_additional_set</span><span class="sxs-lookup"><span data-stu-id="86682-918">nx_http_server_mime_maps_additional_set</span></span>

<span data-ttu-id="86682-919">HTML için ek MIME haritaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="86682-919">Set additional MIME maps for HTML</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-920">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-920">Prototype</span></span>

```c
UINT nx_http_server_mime_maps_additional_set(
                        NX_HTTP_SERVER *server_ptr,
                        NX_HTTP_SERVER_MIME_MAP *mime_maps,
                        UINT mime_maps_num);
```

### <a name="description"></a><span data-ttu-id="86682-921">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-921">Description</span></span>

<span data-ttu-id="86682-922">Bu hizmet, HTTP uygulama geliştiricisinin NetX Duo HTTP sunucusu tarafından sağlanan varsayılan MIME türlerinden ek MIME türleri eklemesine izin verir (tanımlı türlerin listesi için bkz. *nx_http_server_get_type* ).</span><span class="sxs-lookup"><span data-stu-id="86682-922">This service allows the HTTP application developer to add additional MIME types from the default MIME types supplied by NetX Duo HTTP Server (see *nx_http_server_get_type* for list of defined types).</span></span>

<span data-ttu-id="86682-923">Bir istemci isteği alındığında, örneğin, bir GET isteği, http üst bilgisinden istenen dosya türünü, tercihe bağlı olarak ek MIME eşleme kümesini kullanarak ayrıştırır ve bulunursa eşleşme yoksa, HTTP sunucusunun varsayılan MIME eşlemesinde bir eşleşme arar.</span><span class="sxs-lookup"><span data-stu-id="86682-923">When a client request is received, e.g. a GET request, HTTP server parses the requested file type from the HTTP header using preferentially the additional MIME map set and if no match if found, it looks for a match in the default MIME map of the HTTP server.</span></span> <span data-ttu-id="86682-924">Eşleşme bulunmazsa, MIME türü varsayılan olarak "metin/düz" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="86682-924">If no match is found, the MIME type defaults to “text/plain”.</span></span>

<span data-ttu-id="86682-925">İstek bildirimi işlevi HTTP sunucusuna kayıtlıysa, istek bildirimi geri araması dosya türünü ayrıştırmak için *nx_http_server_type_retrieve ()* çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="86682-925">If the request notify function is registered with the HTTP server, the request notify callback can call *nx_http_server_type_retrieve()* to parse the file type.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-926">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-926">Input Parameters</span></span>

 - <span data-ttu-id="86682-927">**server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-927">**server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="86682-928">**mime_maps** MIME eşleme dizisine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-928">**mime_maps** Pointer to a MIME map array</span></span>
 - <span data-ttu-id="86682-929">**mime_map_num** Dizideki MIME haritaları sayısı</span><span class="sxs-lookup"><span data-stu-id="86682-929">**mime_map_num** Number of MIME maps in array</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-930">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-930">Return Values</span></span>

 - <span data-ttu-id="86682-931">**NX_SUCCESS** (0x00) başarılı http sunucusu MIME eşleme kümesi</span><span class="sxs-lookup"><span data-stu-id="86682-931">**NX_SUCCESS** (0x00) Successful HTTP Server MIME map set</span></span>
 - <span data-ttu-id="86682-932">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-932">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-933">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-933">Allowed From</span></span>

<span data-ttu-id="86682-934">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-934">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-935">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-935">Example</span></span>

```c
/* my_server is an NX_HTTP_SERVER previously created. */

NX_HTTP_SERVER_MIME_MAP my_mime_maps [2];

static NX_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc",      "yourtype/abc"},
    {"xyz",      "mytype/xyz"},
};

status =  nx_http_server_mime_maps_additional_set(&my_server,
                                                  &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP  
  server MIME map set.” */
```

## <a name="nx_http_server_packet_content_find"></a><span data-ttu-id="86682-936">nx_http_server_packet_content_find</span><span class="sxs-lookup"><span data-stu-id="86682-936">nx_http_server_packet_content_find</span></span>

<span data-ttu-id="86682-937">İçerik uzunluğunu Ayıkla ve veri başına işaretçiyi ayarla</span><span class="sxs-lookup"><span data-stu-id="86682-937">Extract content length and set pointer to start of data</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-938">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-938">Prototype</span></span>

```c
UINT nx_http_server_packet_content_find(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET **packet_ptr,
                                        UINT *content_length);
```

### <a name="description"></a><span data-ttu-id="86682-939">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-939">Description</span></span>

<span data-ttu-id="86682-940">Bu hizmet, HTTP üstbilgisinden içerik uzunluğunu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="86682-940">This service extracts the content length from the HTTP header.</span></span> <span data-ttu-id="86682-941">Ayrıca, sağlanan paketi aşağıdaki gibi güncelleştirir: paket önüne işaretçisi (yazılacak paket arabelleğinin konumu), http içeriğine (veri) yalnızca http üst bilgisini geçirilmiş şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="86682-941">It also  updates the supplied packet as follows: the packet prepend pointer (start of location of packet buffer to write to) is set to the HTTP content (data) just passed the HTTP header.</span></span>

<span data-ttu-id="86682-942">İçeriğin başlangıcı geçerli pakette bulunmazsa, işlev, sonraki paketin NX_HTTP_SERVER_TIMEOUT_RECEIVE bekle seçeneği kullanılarak alınmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="86682-942">If the beginning of content is not found in the current packet, the function waits for the next packet to be received using the NX_HTTP_SERVER_TIMEOUT_RECEIVE wait option.</span></span>

> [!NOTE]
> <span data-ttu-id="86682-943">Bu, *nx_http_server_get_entity_header* çağrılmadan önce çağrılmamalıdır çünkü varlık üstbilgisinin sonundaki önüne işaretçisini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="86682-943">This should not be called before calling *nx_http_server_get_entity_header* because it modifies the prepend pointer past the entity header.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-944">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-944">Input Parameters</span></span>

 - <span data-ttu-id="86682-945">**server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-945">**server_ptr** Pointer to HTTP server instance</span></span>
 - <span data-ttu-id="86682-946">**packet_ptr** Güncelleştirilmiş önüne işaretçisine sahip paketi döndürmek için paket işaretçisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-946">**packet_ptr** Pointer to packet pointer for returning the packet with updated prepend pointer</span></span>
 - <span data-ttu-id="86682-947">**CONTENT_LENGTH** Ayıklanan işaretçi ```content_length```</span><span class="sxs-lookup"><span data-stu-id="86682-947">**content_length** Pointer to extracted ```content_length```</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-948">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-948">Return Values</span></span>

 - <span data-ttu-id="86682-949">**NX_SUCCESS** (0x00) http içerik uzunluğu bulundu ve paket başarıyla güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="86682-949">**NX_SUCCESS** (0x00) HTTP content length found and packet successfully updated</span></span>
 - <span data-ttu-id="86682-950">**NX_HTTP_TIMEOUT** (0XE1) süre süresi dolduğunda sonraki pakette bekliyor</span><span class="sxs-lookup"><span data-stu-id="86682-950">**NX_HTTP_TIMEOUT** (0xE1) Time expired waiting on next packet</span></span>
 - <span data-ttu-id="86682-951">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-951">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-952">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-952">Allowed From</span></span>

<span data-ttu-id="86682-953">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-953">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-954">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-954">Example</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
The server has received a Client request packet, recv_packet_ptr, and the packet
content find service is called from the request notify callback function
registered with the HTTP server. */

UINT content_length;

status =  nx_http_server_packet_content_find(server_ptr, recv_packet_ptr,
                                             &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
   and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_http_server_packet_get"></a><span data-ttu-id="86682-955">nx_http_server_packet_get</span><span class="sxs-lookup"><span data-stu-id="86682-955">nx_http_server_packet_get</span></span>

<span data-ttu-id="86682-956">Sonraki HTTP paketini al</span><span class="sxs-lookup"><span data-stu-id="86682-956">Receive the next HTTP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-957">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-957">Prototype</span></span>

```c
UINT nx_http_server_packet_get(NX_HTTP_SERVER *server_ptr,
                              NX_PACKET **packet_ptr);
```

### <a name="description"></a><span data-ttu-id="86682-958">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-958">Description</span></span>

<span data-ttu-id="86682-959">Bu hizmet, HTTP sunucusu yuvasında alınan bir sonraki paketi döndürür.</span><span class="sxs-lookup"><span data-stu-id="86682-959">This service returns the next packet received on the HTTP server socket.</span></span> <span data-ttu-id="86682-960">Bir paket almak için bekle seçeneği NX_HTTP_SERVER_TIMEOUT_RECEIVE.</span><span class="sxs-lookup"><span data-stu-id="86682-960">The wait option to receive a packet is NX_HTTP_SERVER_TIMEOUT_RECEIVE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-961">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-961">Input Parameters</span></span>

 - <span data-ttu-id="86682-962">**server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-962">**server_ptr** Pointer to HTTP server instance</span></span>
 - <span data-ttu-id="86682-963">**packet_ptr** Alınan paket işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-963">**packet_ptr** Pointer to received packet</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-964">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-964">Return Values</span></span>

 - <span data-ttu-id="86682-965">**NX_SUCCESS** (0x00) sonraki paket başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="86682-965">**NX_SUCCESS** (0x00) Successfully received next packet</span></span>
 - <span data-ttu-id="86682-966">**NX_HTTP_TIMEOUT** (0XE1) süre süresi dolduğunda sonraki pakette bekliyor</span><span class="sxs-lookup"><span data-stu-id="86682-966">**NX_HTTP_TIMEOUT** (0xE1) Time expired waiting on next packet</span></span>
 - <span data-ttu-id="86682-967">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-967">NX_PTR_ERROR (0x07)  Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-968">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-968">Allowed From</span></span>

<span data-ttu-id="86682-969">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-969">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-970">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-970">Example</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started. */

UINT content_length;
NX_PACKET *recv_packet_ptr;

status =  nx_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_http_server_param_get"></a><span data-ttu-id="86682-971">nx_http_server_param_get</span><span class="sxs-lookup"><span data-stu-id="86682-971">nx_http_server_param_get</span></span>

<span data-ttu-id="86682-972">İstekten parametre al</span><span class="sxs-lookup"><span data-stu-id="86682-972">Get parameter from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-973">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-973">Prototype</span></span>

```c
UINT nx_http_server_param_get(NX_PACKET *packet_ptr,
                              UINT param_number, CHAR *param_ptr,
                              UINT max_param_size);
```

### <a name="description"></a><span data-ttu-id="86682-974">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-974">Description</span></span>

<span data-ttu-id="86682-975">Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL parametresini almaya çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="86682-975">This service attempts to retrieve the specified HTTP URL parameter in the supplied request packet.</span></span> <span data-ttu-id="86682-976">İstenen HTTP parametresi yoksa, bu yordam NX_HTTP_NOT_FOUND durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="86682-976">If the requested HTTP parameter is not present,  this routine returns a status of NX_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="86682-977">Bu yordam, HTTP sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağrısından çağrılmalıdır (*nx_http_server_create*).</span><span class="sxs-lookup"><span data-stu-id="86682-977">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-978">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-978">Input Parameters</span></span>

 - <span data-ttu-id="86682-979">**packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-979">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="86682-980">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86682-980">Note that the application should not release this packet.</span></span>
 - <span data-ttu-id="86682-981">**param_number** Parametre listesinde soldan sağa sıfırdan başlayan parametrenin mantıksal numarası.</span><span class="sxs-lookup"><span data-stu-id="86682-981">**param_number** Logical number of the parameter starting at zero, from left to right in the parameter list.</span></span>
 - <span data-ttu-id="86682-982">**param_ptr** Parametreyi kopyalamak için hedef alan.</span><span class="sxs-lookup"><span data-stu-id="86682-982">**param_ptr** Destination area to copy the parameter.</span></span>
 - <span data-ttu-id="86682-983">**max_param_size** Parametre hedefi alanının maksimum boyutu.</span><span class="sxs-lookup"><span data-stu-id="86682-983">**max_param_size** Maximum size of the parameter destination area.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-984">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-984">Return Values</span></span>

 - <span data-ttu-id="86682-985">**NX_SUCCESS** (0x00) başarılı http sunucusu parametre al</span><span class="sxs-lookup"><span data-stu-id="86682-985">**NX_SUCCESS** (0x00) Successful HTTP Server parameter get</span></span>
 - <span data-ttu-id="86682-986">**NX_HTTP_NOT_FOUND** (0xE6) belirtilen parametre bulunamadı</span><span class="sxs-lookup"><span data-stu-id="86682-986">**NX_HTTP_NOT_FOUND** (0xE6) Specified parameter not found</span></span>
 - <span data-ttu-id="86682-987">**NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) istek parametresi düzgün sonlandırılmadı</span><span class="sxs-lookup"><span data-stu-id="86682-987">**NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) Request parameter not properly terminated</span></span>
 - <span data-ttu-id="86682-988">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-988">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-989">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-989">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-990">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-990">Allowed From</span></span>

<span data-ttu-id="86682-991">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-991">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-992">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-992">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, get the first parameter of the HTTP Client request. */

status =  nx_http_server_param_get(request_packet_ptr, 0, param_destination,
               30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
   in “param_destination.” */
```

## <a name="nx_http_server_query_get"></a><span data-ttu-id="86682-993">nx_http_server_query_get</span><span class="sxs-lookup"><span data-stu-id="86682-993">nx_http_server_query_get</span></span>

<span data-ttu-id="86682-994">İstekten sorgu al</span><span class="sxs-lookup"><span data-stu-id="86682-994">Get query from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-995">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-995">Prototype</span></span>

```c
UINT nx_http_server_query_get(NX_PACKET *packet_ptr, UINT query_number,
                   CHAR *query_ptr, UINT max_query_size);
```

### <a name="description"></a><span data-ttu-id="86682-996">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-996">Description</span></span>

<span data-ttu-id="86682-997">Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL sorgusunu almaya çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="86682-997">This service attempts to retrieve the specified HTTP URL query in the supplied request packet.</span></span> <span data-ttu-id="86682-998">İstenen HTTP sorgusu yoksa, bu yordam NX_HTTP_NOT_FOUND durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="86682-998">If the requested HTTP query is not present,  this routine returns a status of NX_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="86682-999">Bu yordam, HTTP sunucusu oluşturma sırasında belirtilen uygulamanın istek bildirimi geri çağrısından çağrılmalıdır (*nx_http_server_create*).</span><span class="sxs-lookup"><span data-stu-id="86682-999">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-1000">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-1000">Input Parameters</span></span>

 - <span data-ttu-id="86682-1001">**packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-1001">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="86682-1002">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86682-1002">Note that the application should not release this packet.</span></span>
 - <span data-ttu-id="86682-1003">**query_number** Sıfırdan başlayan parametrenin mantıksal numarası, sorgu listesinde soldan sağa.</span><span class="sxs-lookup"><span data-stu-id="86682-1003">**query_number** Logical number of the parameter starting at zero, from left to right in the query list.</span></span>
 - <span data-ttu-id="86682-1004">**query_ptr** Sorguyu kopyalamak için hedef alan.</span><span class="sxs-lookup"><span data-stu-id="86682-1004">**query_ptr** Destination area to copy the query.</span></span>
 - <span data-ttu-id="86682-1005">**max_query_size** Sorgu hedefi alanının maksimum boyutu.</span><span class="sxs-lookup"><span data-stu-id="86682-1005">**max_query_size** Maximum size of the query destination area.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-1006">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-1006">Return Values</span></span>

 - <span data-ttu-id="86682-1007">**NX_SUCCESS** (0x00) başarılı http sunucusu sorgusu al</span><span class="sxs-lookup"><span data-stu-id="86682-1007">**NX_SUCCESS** (0x00) Successful HTTP Server query get</span></span>
 - <span data-ttu-id="86682-1008">**NX_HTTP_FAILED** (0xE2) sorgu boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="86682-1008">**NX_HTTP_FAILED** (0xE2) Query size too small.</span></span>
 - <span data-ttu-id="86682-1009">**NX_HTTP_NOT_FOUND** (0xE6) belirtilen sorgu bulunamadı</span><span class="sxs-lookup"><span data-stu-id="86682-1009">**NX_HTTP_NOT_FOUND** (0xE6) Specified query not found</span></span>
 - <span data-ttu-id="86682-1010">**NX_HTTP_NO_QUERY_PARSED** (0xF2) istemci Isteğinde sorgu yok</span><span class="sxs-lookup"><span data-stu-id="86682-1010">**NX_HTTP_NO_QUERY_PARSED** (0xF2) No query in Client request</span></span>
 - <span data-ttu-id="86682-1011">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-1011">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-1012">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-1012">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-1013">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-1013">Allowed From</span></span>

<span data-ttu-id="86682-1014">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-1014">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-1015">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-1015">Example</span></span>

```c
/* Assuming we are in the application’s request notify callback
   routine, get the first query of the HTTP Client request. */
status =  nx_http_server_query_get(request_packet_ptr, 0, query_destination,
                30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
   in “query_destination.” */
```

## <a name="nx_http_server_start"></a><span data-ttu-id="86682-1016">nx_http_server_start</span><span class="sxs-lookup"><span data-stu-id="86682-1016">nx_http_server_start</span></span>

<span data-ttu-id="86682-1017">HTTP sunucusunu başlatma</span><span class="sxs-lookup"><span data-stu-id="86682-1017">Start the HTTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-1018">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-1018">Prototype</span></span>

```c
UINT nx_http_server_start(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="86682-1019">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-1019">Description</span></span>

<span data-ttu-id="86682-1020">Bu hizmet, önceden oluşturma HTTP sunucu örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="86682-1020">This service starts the previously create HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-1021">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-1021">Input Parameters</span></span>

 - <span data-ttu-id="86682-1022">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-1022">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-1023">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-1023">Return Values</span></span>

 - <span data-ttu-id="86682-1024">**NX_SUCCESS** (0x00) başarılı sunucu başlatması</span><span class="sxs-lookup"><span data-stu-id="86682-1024">**NX_SUCCESS** (0x00) Successful Server start</span></span>
 - <span data-ttu-id="86682-1025">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-1025">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-1026">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-1026">Allowed From</span></span>

<span data-ttu-id="86682-1027">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-1027">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-1028">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-1028">Example</span></span>

```c
/* Start the HTTP Server instance “my_server.”  */
status =  nx_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_http_server_stop"></a><span data-ttu-id="86682-1029">nx_http_server_stop</span><span class="sxs-lookup"><span data-stu-id="86682-1029">nx_http_server_stop</span></span>

<span data-ttu-id="86682-1030">HTTP sunucusunu durdur</span><span class="sxs-lookup"><span data-stu-id="86682-1030">Stop the HTTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-1031">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-1031">Prototype</span></span>

```c
UINT nx_http_server_stop(NX_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="86682-1032">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-1032">Description</span></span>

<span data-ttu-id="86682-1033">Bu hizmet, önceden oluşturma HTTP sunucu örneğini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="86682-1033">This service stops the previously create HTTP Server instance.</span></span> <span data-ttu-id="86682-1034">Bu yordam, bir HTTP sunucu örneği silinmeden önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86682-1034">This routine should be called prior to deleting an HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-1035">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-1035">Input Parameters</span></span>

 - <span data-ttu-id="86682-1036">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="86682-1036">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-1037">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-1037">Return Values</span></span>

 - <span data-ttu-id="86682-1038">**NX_SUCCESS** (0x00) başarılı sunucu durdu</span><span class="sxs-lookup"><span data-stu-id="86682-1038">**NX_SUCCESS** (0x00) Successful Server stop</span></span>
 - <span data-ttu-id="86682-1039">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-1039">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-1040">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="86682-1040">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-1041">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-1041">Allowed From</span></span>

<span data-ttu-id="86682-1042">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="86682-1042">Threads</span></span>

### <a name="example"></a><span data-ttu-id="86682-1043">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-1043">Example</span></span>

```c
/* Stop the HTTP Server instance “my_server.”  */
status =  nx_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_http_server_type_get"></a><span data-ttu-id="86682-1044">nx_http_server_type_get</span><span class="sxs-lookup"><span data-stu-id="86682-1044">nx_http_server_type_get</span></span>

<span data-ttu-id="86682-1045">Istemci HTTP isteğinden dosya türünü Ayıkla</span><span class="sxs-lookup"><span data-stu-id="86682-1045">Extract file type from Client HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-1046">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-1046">Prototype</span></span>

```c
UINT nx_http_server_type_get(NX_HTTP_SERVER *http_server_ptr,
                             CHAR *name, CHAR *http_type_string);
```

### <a name="description"></a><span data-ttu-id="86682-1047">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-1047">Description</span></span>

> [!NOTE]
> <span data-ttu-id="86682-1048">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-1048">This service is deprecated.</span></span> <span data-ttu-id="86682-1049">Kullanıcıların *nx_http_server_type_retrieve ()* hizmetini kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-1049">Users are encouraged to use the service *nx_http_server_type_retrieve()*.</span></span>

<span data-ttu-id="86682-1050">Bu hizmet, arabellek http_type_string HTTP istek türünü ve giriş arabelleği adından (genellikle URL) gelen dönüş değerindeki uzunluğu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="86682-1050">This service extracts the HTTP request type in the buffer http_type_string and its length in the return value from the input buffer name, usually the URL.</span></span> <span data-ttu-id="86682-1051">MIME eşlemesi bulunmazsa, varsayılan olarak "metin/düz" tür olur.</span><span class="sxs-lookup"><span data-stu-id="86682-1051">If no MIME map is found, it defaults to the “text/plain” type.</span></span> <span data-ttu-id="86682-1052">Aksi takdirde, bir eşleşme için ayıklanan tür, HTTP sunucusu varsayılan MIME eşlemeleriyle karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="86682-1052">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="86682-1053">NetX Duo HTTP sunucusundaki varsayılan MIME haritaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="86682-1053">The default MIME maps in NetX Duo HTTP Server are:</span></span>

 - <span data-ttu-id="86682-1054">**HTML** metni/HTML</span><span class="sxs-lookup"><span data-stu-id="86682-1054">**html** text/html</span></span>
 - <span data-ttu-id="86682-1055">**htm** metin/html</span><span class="sxs-lookup"><span data-stu-id="86682-1055">**htm** text/html</span></span>
 - <span data-ttu-id="86682-1056">**txt** metin/düz</span><span class="sxs-lookup"><span data-stu-id="86682-1056">**txt** text/plain</span></span>
 - <span data-ttu-id="86682-1057">**GIF** resmi/GIF</span><span class="sxs-lookup"><span data-stu-id="86682-1057">**gif** image/gif</span></span>
 - <span data-ttu-id="86682-1058">**jpg** resmi/JPEG</span><span class="sxs-lookup"><span data-stu-id="86682-1058">**jpg** image/jpeg</span></span>
 - <span data-ttu-id="86682-1059">**ICO** resmi/x-simgesi</span><span class="sxs-lookup"><span data-stu-id="86682-1059">**ico** image/x-icon</span></span>

<span data-ttu-id="86682-1060">Sağlanırsa, Kullanıcı tanımlı ek MIME haritaları kümesi de arar.</span><span class="sxs-lookup"><span data-stu-id="86682-1060">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="86682-1061">Kullanıcı tanımlı haritalar hakkında daha fazla bilgi için bkz. *nx_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="86682-1061">See *nx_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="86682-1062">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="86682-1062">This service is deprecated.</span></span> <span data-ttu-id="86682-1063">Geliştiricilerin *nx_http_server_type_get_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="86682-1063">Developers are encouraged to migrate to *nx_http_server_type_get_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-1064">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-1064">Input Parameters</span></span>

 - <span data-ttu-id="86682-1065">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-1065">**http_server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="86682-1066">Aranacak arabelleğe yönelik **işaretçiyi adlandırın**</span><span class="sxs-lookup"><span data-stu-id="86682-1066">**name Pointer** to buffer to search</span></span>
 - <span data-ttu-id="86682-1067">**http_type_string** (ayıklanan HTML türüne yönelik işaretçi)</span><span class="sxs-lookup"><span data-stu-id="86682-1067">**http_type_string** (Pointer to extracted HTML type)</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-1068">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-1068">Return Values</span></span>

 - <span data-ttu-id="86682-1069">**Bayt cinsinden dize uzunluğu** Sıfır olmayan değer başarılı.</span><span class="sxs-lookup"><span data-stu-id="86682-1069">**Length of string in bytes** Non zero value is success.</span></span> <span data-ttu-id="86682-1070">Sıfır hatayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="86682-1070">Zero indicates error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-1071">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-1071">Allowed From</span></span>

<span data-ttu-id="86682-1072">Uygulama</span><span class="sxs-lookup"><span data-stu-id="86682-1072">Application</span></span>

### <a name="example"></a><span data-ttu-id="86682-1073">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-1073">Example</span></span>

```c
/* my_server is a previously created HTTP server, which starts accepting client
   requests when nx_http_server_start is called*/

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
    string_length =  nx_http_server_type_get(&my_server_ptr,
                my_server.nx_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
```

## <a name="nx_http_server_type_get_extended"></a><span data-ttu-id="86682-1074">nx_http_server_type_get_extended</span><span class="sxs-lookup"><span data-stu-id="86682-1074">nx_http_server_type_get_extended</span></span>

<span data-ttu-id="86682-1075">Istemci HTTP isteğinden dosya türünü Ayıkla</span><span class="sxs-lookup"><span data-stu-id="86682-1075">Extract file type from Client HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-1076">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-1076">Prototype</span></span>

```c
UINT nx_http_server_type_get_extended(
                                    NX_HTTP_SERVER *http_server_ptr,
                                    CHAR *name, CHAR *http_type_string,
                                    UINT http_type_string_max_size);
```

### <a name="description"></a><span data-ttu-id="86682-1077">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-1077">Description</span></span>

<span data-ttu-id="86682-1078">Bu hizmet, arabellek *HTTP_TYPE_STRING* http istek türünü ve giriş arabelleği *ADıNDAN*(genellikle URL) gelen dönüş değerindeki uzunluğu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="86682-1078">This service extracts the HTTP request type in the buffer *http_type_string* and its length in the return value from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="86682-1079">MIME eşlemesi bulunmazsa, varsayılan olarak "metin/düz" tür olur.</span><span class="sxs-lookup"><span data-stu-id="86682-1079">If no MIME map is found, it defaults to the “text/plain” type.</span></span> <span data-ttu-id="86682-1080">Aksi takdirde, bir eşleşme için ayıklanan tür, HTTP sunucusu varsayılan MIME eşlemeleriyle karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="86682-1080">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="86682-1081">NetX Duo HTTP sunucusundaki varsayılan MIME haritaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="86682-1081">The default MIME maps in NetX Duo HTTP Server are:</span></span>

 - <span data-ttu-id="86682-1082">**HTML** metni/HTML</span><span class="sxs-lookup"><span data-stu-id="86682-1082">**html** text/html</span></span>
 - <span data-ttu-id="86682-1083">**htm** metin/html</span><span class="sxs-lookup"><span data-stu-id="86682-1083">**htm** text/html</span></span>
 - <span data-ttu-id="86682-1084">**txt** metin/düz</span><span class="sxs-lookup"><span data-stu-id="86682-1084">**txt** text/plain</span></span>
 - <span data-ttu-id="86682-1085">**GIF** resmi/GIF</span><span class="sxs-lookup"><span data-stu-id="86682-1085">**gif** image/gif</span></span>
 - <span data-ttu-id="86682-1086">**jpg** resmi/JPEG</span><span class="sxs-lookup"><span data-stu-id="86682-1086">**jpg** image/jpeg</span></span>
 - <span data-ttu-id="86682-1087">**ICO** resmi/x-simgesi</span><span class="sxs-lookup"><span data-stu-id="86682-1087">**ico** image/x-icon</span></span>

<span data-ttu-id="86682-1088">Sağlanırsa, Kullanıcı tanımlı ek MIME haritaları kümesi de arar.</span><span class="sxs-lookup"><span data-stu-id="86682-1088">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="86682-1089">Kullanıcı tanımlı haritalar hakkında daha fazla bilgi için bkz. *nx_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="86682-1089">See *nx_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="86682-1090">Bu hizmet *nx_http_server_type_get ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86682-1090">This service replaces *nx_http_server_type_get()*.</span></span> <span data-ttu-id="86682-1091">Bu sürüm, ek uzunluk bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="86682-1091">This version supplies additional length information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-1092">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-1092">Input Parameters</span></span>

 - <span data-ttu-id="86682-1093">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-1093">**http_server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="86682-1094">**ad** Aranacak arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-1094">**name** Pointer to buffer to search</span></span>
 - <span data-ttu-id="86682-1095">**name_length** Aranacak arabelleğin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="86682-1095">**name_length** Length of buffer to search</span></span>
 - <span data-ttu-id="86682-1096">**http_type_string** (ayıklanan HTML türüne yönelik işaretçi)</span><span class="sxs-lookup"><span data-stu-id="86682-1096">**http_type_string** (Pointer to extracted HTML type)</span></span>
 - <span data-ttu-id="86682-1097">**http_type_string_max_size** Http_type_string arabelleğinin boyutu</span><span class="sxs-lookup"><span data-stu-id="86682-1097">**http_type_string_max_size** Size of the http_type_string buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-1098">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-1098">Return Values</span></span>

 - <span data-ttu-id="86682-1099">**Bayt cinsinden dize uzunluğu** Sıfır olmayan değer başarılı.</span><span class="sxs-lookup"><span data-stu-id="86682-1099">**Length of string in bytes** Non zero value is success.</span></span> <span data-ttu-id="86682-1100">Sıfır hatayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="86682-1100">Zero indicates error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-1101">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-1101">Allowed From</span></span>

<span data-ttu-id="86682-1102">Uygulama</span><span class="sxs-lookup"><span data-stu-id="86682-1102">Application</span></span>

### <a name="example"></a><span data-ttu-id="86682-1103">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-1103">Example</span></span>

```c
/* my_server is a previously created HTTP server, which starts accepting client
   requests when nx_http_server_start is called*/

CHAR temp_string[20];
UINT string_length;

/* Get the length of request resource. */
    if (_nx_utility_string_length_check(
                    my_server.nx_http_server_request_resource, &resource_length,
                    sizeof(my_server.nx_http_server_request_resource) - 1))
           {
               return;
           }

/* Extract the HTTP type. */
    string_length =  nx_http_server_type_get_extended(&my_server,
               my_server.nx_http_server_request_resource, resource_length,
               temp_string, sizeof(temp_string));

/* If string_length is non zero, the HTTP string is extracted. */
```

<span data-ttu-id="86682-1104">Daha ayrıntılı bir örnek için [*nx_http_server_callback_generate_response_header*](#nx_http_server_callback_generate_response_header)açıklamasına bakın.</span><span class="sxs-lookup"><span data-stu-id="86682-1104">For a more detailed example, see the description for [*nx_http_server_callback_generate_response_header*](#nx_http_server_callback_generate_response_header).</span></span>

## <a name="nx_http_server_digest_authenticate_notify_set"></a><span data-ttu-id="86682-1105">nx_http_server_digest_authenticate_notify_set</span><span class="sxs-lookup"><span data-stu-id="86682-1105">nx_http_server_digest_authenticate_notify_set</span></span>

<span data-ttu-id="86682-1106">Özet kimlik doğrulaması geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="86682-1106">Set digest authenticate callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-1107">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-1107">Prototype</span></span>

```c
UINT nx_http_server_digest_authenticate_notify_set(
       NX_HTTP_SERVER *http_server_ptr,
       UINT (*digest_authenticate_callback)(NX_HTTP_SERVER *server_ptr,
                                            CHAR *name_ptr,
                                            CHAR *realm_ptr,
                                            CHAR *password_ptr,
                                            CHAR *method,
                                            CHAR *authorization_uri,
                                            CHAR *authorization_nc,
                                            CHAR *authorization_cnonce
                                           ));
```

### <a name="description"></a><span data-ttu-id="86682-1108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-1108">Description</span></span>

<span data-ttu-id="86682-1109">Bu hizmet Özet kimlik doğrulaması gerçekleştirildiğinde çağrılan geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="86682-1109">This service sets the callback invoked when digest authenticate is performed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-1110">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-1110">Input Parameters</span></span>

 - <span data-ttu-id="86682-1111">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-1111">**http_server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="86682-1112">**digest_authenticate_callback** Özet kimlik doğrulaması geri çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-1112">**digest_authenticate_callback** Pointer to digest authenticate callback</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-1113">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-1113">Return Values</span></span>

 - <span data-ttu-id="86682-1114">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="86682-1114">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="86682-1115">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-1115">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
 - <span data-ttu-id="86682-1116">NX_NOT_SUPPORTED (0x4B) Özet kimlik doğrulaması etkin değil</span><span class="sxs-lookup"><span data-stu-id="86682-1116">NX_NOT_SUPPORTED (0x4B) Digest authenticate not enabled</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-1117">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-1117">Allowed From</span></span>

<span data-ttu-id="86682-1118">Uygulama</span><span class="sxs-lookup"><span data-stu-id="86682-1118">Application</span></span>

### <a name="example"></a><span data-ttu-id="86682-1119">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-1119">Example</span></span>

```c
UINT digest_authenticate_callback(NX_HTTP_SERVER *server_ptr, CHAR *name_ptr,
                                  CHAR *realm_ptr, CHAR *password_ptr, CHAR *method,
                                  CHAR *authorization_uri, CHAR *authorization_nc,
                                  CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the digest authenticate callback: */

status =  nx_http_server_digest_authenticate_notify_set (&my_server,
    digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
   will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_http_server_authentication_check_set"></a><span data-ttu-id="86682-1120">nx_http_server_authentication_check_set</span><span class="sxs-lookup"><span data-stu-id="86682-1120">nx_http_server_authentication_check_set</span></span>

<span data-ttu-id="86682-1121">Kimlik doğrulama denetimi geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="86682-1121">Set authentication checking callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="86682-1122">Prototype</span><span class="sxs-lookup"><span data-stu-id="86682-1122">Prototype</span></span>

```c
UINT nx_http_server_authentication_check_set(
       NX_HTTP_SERVER *http_server_ptr,
       UINT (*authentication_check_extended)(
                                            NX_HTTP_SERVER *server_ptr,
                                            UINT request_type,
                                            CHAR *resource,
                                            CHAR **name,
                                            UINT *name_length,
                                            CHAR **password,
                                            UINT *password_length,
                                            CHAR **realm,
                                            UINT *realm_length
                                            ));
```

### <a name="description"></a><span data-ttu-id="86682-1123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86682-1123">Description</span></span>

<span data-ttu-id="86682-1124">Bu hizmet, kimlik doğrulama denetiminin geri çağırma işlevini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="86682-1124">This service sets the callback function of authentication checking.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="86682-1125">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="86682-1125">Input Parameters</span></span>

 - <span data-ttu-id="86682-1126">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="86682-1126">**http_server_ptr** Pointer to HTTP Server instance</span></span>
 - <span data-ttu-id="86682-1127">**authentication_check_extended** Uygulamanın kimlik doğrulama denetimi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="86682-1127">**authentication_check_extended** Pointer to application’s authentication checking</span></span>

### <a name="return-values"></a><span data-ttu-id="86682-1128">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="86682-1128">Return Values</span></span>

 - <span data-ttu-id="86682-1129">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="86682-1129">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
 - <span data-ttu-id="86682-1130">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="86682-1130">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="86682-1131">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="86682-1131">Allowed From</span></span>

<span data-ttu-id="86682-1132">Uygulama</span><span class="sxs-lookup"><span data-stu-id="86682-1132">Application</span></span>

### <a name="example"></a><span data-ttu-id="86682-1133">Örnek</span><span class="sxs-lookup"><span data-stu-id="86682-1133">Example</span></span>

```c
static UINT  authentication_check_extended(NX_HTTP_SERVER *server_ptr,
                                           UINT request_type, CHAR *resource,
                                           CHAR **name, UINT *name_length,
                                           CHAR **password, UINT *password_length,
                                           CHAR **realm, UINT *realm_length)
{

    /* Just use a simple name, password, and realm for all
       requests and resources. */
    *name =     "name";
    *password = "password";
    *realm =    "NetX Duo HTTP demo";
    *name_length = 4;
    *password_length = 8;
    *realm_length = 18;

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and before
   starting HTTP services when nx_http_server_start is called, set the
   authentication checking callback: */

nx_http_server_authentication_check_set (&my_server,
                                         authentication_check_extended);
```
