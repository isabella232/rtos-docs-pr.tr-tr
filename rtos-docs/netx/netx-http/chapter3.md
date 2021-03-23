---
title: Bölüm 3-NetX HTTP hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX HTTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c58d0e3d7eca86816a9d656bf2b92a896ffb96fc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826711"
---
# <a name="chapter-3---description-of-netx-http-services"></a><span data-ttu-id="b2d24-103">Bölüm 3-NetX HTTP hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="b2d24-103">Chapter 3 - Description of NetX HTTP services</span></span>

<span data-ttu-id="b2d24-104">Bu bölüm, tüm NetX HTTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-104">This chapter contains a description of all NetX HTTP services (listed below) in alphabetical order.</span></span>

<span data-ttu-id="b2d24-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

<span data-ttu-id="b2d24-106">**HTTP Istemci Hizmetleri:**</span><span class="sxs-lookup"><span data-stu-id="b2d24-106">**HTTP Client services:**</span></span>

- <span data-ttu-id="b2d24-107">nx_http_client_create *http Istemci örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="b2d24-107">nx_http_client_create *Create an HTTP Client Instance*</span></span>
- <span data-ttu-id="b2d24-108">*http istemci örneğini silme* nx_http_client_delete</span><span class="sxs-lookup"><span data-stu-id="b2d24-108">nx_http_client_delete *Delete an HTTP Client instance*</span></span>
- <span data-ttu-id="b2d24-109">*http get Isteği başlatmak* nx_http_client_get_start</span><span class="sxs-lookup"><span data-stu-id="b2d24-109">nx_http_client_get_start *Start an HTTP GET request*</span></span>
- <span data-ttu-id="b2d24-110">*http get Isteği başlatmak* nx_http_client_get_start_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-110">nx_http_client_get_start_extended *Start an HTTP GET request*</span></span>
- <span data-ttu-id="b2d24-111">*sonraki kaynak veri paketini al* nx_http_client_get_packet</span><span class="sxs-lookup"><span data-stu-id="b2d24-111">nx_http_client_get_packet *Get next resource data packet*</span></span>
- <span data-ttu-id="b2d24-112">nx_http_client_put_start *BIR http put Isteği başlatın*</span><span class="sxs-lookup"><span data-stu-id="b2d24-112">nx_http_client_put_start *Start an HTTP PUT request*</span></span>
- <span data-ttu-id="b2d24-113">nx_http_client_put_start_extended *BIR http put Isteği başlatın*</span><span class="sxs-lookup"><span data-stu-id="b2d24-113">nx_http_client_put_start_extended *Start an HTTP PUT request*</span></span>
- <span data-ttu-id="b2d24-114">*sonraki kaynak veri paketini Nx_http_client_put_packet gönder*</span><span class="sxs-lookup"><span data-stu-id="b2d24-114">nx_http_client_put_packet *Send next resource data packet*</span></span>
- <span data-ttu-id="b2d24-115"> *http sunucusuna bağlanmak için bağlantı noktasını değiştirme* nx_http_client_set_connect_port</span><span class="sxs-lookup"><span data-stu-id="b2d24-115">*nx_http_client_set_connect_port* *Change the port to connect to the HTTP Server*</span></span>

<span data-ttu-id="b2d24-116">**HTTP sunucusu Hizmetleri:**</span><span class="sxs-lookup"><span data-stu-id="b2d24-116">**HTTP Server services:**</span></span>

- <span data-ttu-id="b2d24-117">*BELIRTILEN URL 'nin yaş ve son değiştirilme tarihini almak için geri çağırma* nx_http_server_cache_info_callback_set</span><span class="sxs-lookup"><span data-stu-id="b2d24-117">nx_http_server_cache_info_callback_set *Set callback to retrieve age and last modified date of specified URL*</span></span>
- <span data-ttu-id="b2d24-118">*geri çağırma IŞLEVINDEN http verileri gönderme* nx_http_server_callback_data_send</span><span class="sxs-lookup"><span data-stu-id="b2d24-118">nx_http_server_callback_data_send *Send HTTP data from callback function*</span></span>
- <span data-ttu-id="b2d24-119">*geri çağırma işlevlerinde yanıt üst bilgisi oluşturma* nx_http_server_callback_generate_response_header</span><span class="sxs-lookup"><span data-stu-id="b2d24-119">nx_http_server_callback_generate_response_header *Create response header in callback functions*</span></span>
- <span data-ttu-id="b2d24-120">*geri çağırma işlevlerinde yanıt üst bilgisi oluşturma* nx_http_server_callback_generate_response_header_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-120">nx_http_server_callback_generate_response_header_extended *Create response header in callback functions*</span></span>
- <span data-ttu-id="b2d24-121">*http geri ÇAĞRıSıNDAN http paketi gönderme* nx_http_server_callback_packet_send</span><span class="sxs-lookup"><span data-stu-id="b2d24-121">nx_http_server_callback_packet_send *Send an HTTP packet from an HTTP callback*</span></span>
- <span data-ttu-id="b2d24-122">*geri çağırma işlevinden yanıt gönder* nx_http_server_callback_response_send</span><span class="sxs-lookup"><span data-stu-id="b2d24-122">nx_http_server_callback_response_send *Send response from callback function*</span></span>
- <span data-ttu-id="b2d24-123">*geri çağırma işlevinden yanıt gönder* nx_http_server_callback_response_send_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-123">nx_http_server_callback_response_send_extended *Send response from callback function*</span></span>
- <span data-ttu-id="b2d24-124">*istekten Içerik al* nx_http_server_content_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-124">nx_http_server_content_get *Get content from the request*</span></span>
- <span data-ttu-id="b2d24-125">*istekten Içerik al nx_http_server_content_get_extended; boş (sıfır Içerik uzunluğu) isteklerini destekler*</span><span class="sxs-lookup"><span data-stu-id="b2d24-125">nx_http_server_content_get_extended *Get content from the request; supports empty (zero Content Length) requests*</span></span>
- <span data-ttu-id="b2d24-126">nx_http_server_content_length_get *istekteki içeriğin uzunluğunu al*</span><span class="sxs-lookup"><span data-stu-id="b2d24-126">nx_http_server_content_length_get *Get length of content in the request*</span></span>
- <span data-ttu-id="b2d24-127">*istekteki içeriğin uzunluğunu nx_http_server_content_length_get_extended; boş (sıfır Içerik uzunluğu) istekleri destekler*</span><span class="sxs-lookup"><span data-stu-id="b2d24-127">nx_http_server_content_length_get_extended *Get length of content in the request; supports empty (zero Content Length) requests*</span></span>
- <span data-ttu-id="b2d24-128">nx_http_server_create *http sunucu örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="b2d24-128">nx_http_server_create *Create an HTTP Server instance*</span></span>
- <span data-ttu-id="b2d24-129">*http sunucusu örneğini silme* nx_http_server_delete</span><span class="sxs-lookup"><span data-stu-id="b2d24-129">nx_http_server_delete *Delete an HTTP Server instance*</span></span>
- <span data-ttu-id="b2d24-130">nx_http_server_get_entity_content *, URL 'deki varlık içeriğinin boyutunu ve konumunu döndürür*</span><span class="sxs-lookup"><span data-stu-id="b2d24-130">nx_http_server_get_entity_content *Return size and location of entity content in URL*</span></span>
- <span data-ttu-id="b2d24-131">*URL varlık üst bilgisini belirtilen arabelleğe Nx_http_server_get_entity_header Ayıkla*</span><span class="sxs-lookup"><span data-stu-id="b2d24-131">nx_http_server_get_entity_header *Extract URL entity header into specified buffer*</span></span>
- <span data-ttu-id="b2d24-132">nx_http_server_gmt_callback_set *GMT Tarih ve saatini almak için geri çağırma ayarla*</span><span class="sxs-lookup"><span data-stu-id="b2d24-132">nx_http_server_gmt_callback_set *Set callback to retrieve GMT date and time*</span></span>
- <span data-ttu-id="b2d24-133">*istemci isteğinde geçersiz Kullanıcı adı ve parola alındığında geri çağırma* nx_http_server_invalid_userpassword_notify_set</span><span class="sxs-lookup"><span data-stu-id="b2d24-133">nx_http_server_invalid_userpassword_notify_set *Set callback for when invalid username and password is received in a Client request*</span></span>
- <span data-ttu-id="b2d24-134">*HTML için ek MIME haritaları tanımlama* nx_http_server_mime_maps_additional_set</span><span class="sxs-lookup"><span data-stu-id="b2d24-134">nx_http_server_mime_maps_additional_set *Define additional mime maps for HTML*</span></span>
- <span data-ttu-id="b2d24-135">*http üstbilgisindeki içerik uzunluğunu ayıklama nx_http_server_packet_content_find ve içerik verilerinin başlangıcına işaretçiyi ayarla*</span><span class="sxs-lookup"><span data-stu-id="b2d24-135">nx_http_server_packet_content_find *Extract content length in HTTP header and set pointer to start of content data*</span></span>
- <span data-ttu-id="b2d24-136">*istemci paketini doğrudan almak* nx_http_server_packet_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-136">nx_http_server_packet_get *Receive client packet directly*</span></span>
- <span data-ttu-id="b2d24-137">*istekten parametre al* nx_http_server_param_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-137">nx_http_server_param_get *Get parameter from the request*</span></span>
- <span data-ttu-id="b2d24-138">*istekten sorgu al* nx_http_server_query_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-138">nx_http_server_query_get *Get query from the request*</span></span>
- <span data-ttu-id="b2d24-139">*http sunucusunu Nx_http_server_start başlatın*</span><span class="sxs-lookup"><span data-stu-id="b2d24-139">nx_http_server_start *Start the HTTP Server*</span></span>
- <span data-ttu-id="b2d24-140">*http sunucusunu Nx_http_server_stop durdur*</span><span class="sxs-lookup"><span data-stu-id="b2d24-140">nx_http_server_stop *Stop the HTTP Server*</span></span>
- <span data-ttu-id="b2d24-141">*http türünü (örneğin, metin/düz üstbilgi) ayıkla* nx_http_server_type_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-141">nx_http_server_type_get *Extract HTTP type e.g. text/plain from header*</span></span>
- <span data-ttu-id="b2d24-142">*http türünü (örneğin, metin/düz üstbilgi) ayıkla* nx_http_server_type_get_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-142">nx_http_server_type_get_extended *Extract HTTP type e.g. text/plain from header*</span></span>
- <span data-ttu-id="b2d24-143">nx_http_server_digest_authenticate_notify_set *Özet kimlik doğrulaması geri arama Işlevini ayarla*</span><span class="sxs-lookup"><span data-stu-id="b2d24-143">nx_http_server_digest_authenticate_notify_set *Set digest authenticate callback function*</span></span>
- <span data-ttu-id="b2d24-144">nx_http_server_authentication_check_set *kimlik doğrulaması denetim geri arama Işlevini ayarla*</span><span class="sxs-lookup"><span data-stu-id="b2d24-144">nx_http_server_authentication_check_set *Set authentication checking callback function*</span></span>

## <a name="nx_http_client_create"></a><span data-ttu-id="b2d24-145">nx_http_client_create</span><span class="sxs-lookup"><span data-stu-id="b2d24-145">nx_http_client_create</span></span>

### <a name="create-an-http-client-instance"></a><span data-ttu-id="b2d24-146">HTTP Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2d24-146">Create an HTTP Client Instance</span></span>

<span data-ttu-id="b2d24-147">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-147">**Prototype**</span></span>

```c
UINT nx_http_client_create(NX_HTTP_CLIENT *client_ptr,
                          CHAR *client_name, NX_IP *ip_ptr, 
                          NX_PACKET_POOL *pool_ptr,
                          ULONG window_size);
```

<span data-ttu-id="b2d24-148">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-148">**Description**</span></span>

<span data-ttu-id="b2d24-149">Bu hizmet, belirtilen IP örneğinde bir HTTP Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-149">This service creates an HTTP Client instance on the specified IP instance.</span></span>

<span data-ttu-id="b2d24-150">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-150">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-151">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-151">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="b2d24-152">**client_name** HTTP Istemci örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-152">**client_name** Name of HTTP Client instance.</span></span>
- <span data-ttu-id="b2d24-153">**ip_ptr** IP örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-153">**ip_ptr** Pointer to IP instance.</span></span>
- <span data-ttu-id="b2d24-154">**pool_ptr** Varsayılan paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-154">**pool_ptr** Pointer to default packet pool.</span></span> <span data-ttu-id="b2d24-155">Bu havuzdaki paketlerin, tüm yanıt üst bilgisini işleyecek kadar büyük bir yükün olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-155">Note that the packets in this pool must have a payload large enough to handle the complete response header.</span></span> <span data-ttu-id="b2d24-156">Bu, *nx_http_client. h* içinde NX_HTTP_CLIENT_MIN_PACKET_SIZE tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-156">This is defined by NX_HTTP_CLIENT_MIN_PACKET_SIZE in *nx_http_client.h*.</span></span>
- <span data-ttu-id="b2d24-157">**window_size** Istemcinin TCP yuvası alma penceresinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-157">**window_size** Size of the Client’s TCP socket receive window.</span></span>

<span data-ttu-id="b2d24-158">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-158">**Return Values**</span></span>

- <span data-ttu-id="b2d24-159">**NX_SUCCESS** (0x00) başarılı http istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2d24-159">**NX_SUCCESS** (0x00) Successful HTTP Client create</span></span>
- <span data-ttu-id="b2d24-160">NX_PTR_ERROR (0x16) geçersiz HTTP, ip_ptr veya paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-160">NX_PTR_ERROR (0x16) Invalid HTTP, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="b2d24-161">NX_HTTP_POOL_ERROR (0xE9) paket havuzunda geçersiz yük boyutu</span><span class="sxs-lookup"><span data-stu-id="b2d24-161">NX_HTTP_POOL_ERROR(0xE9) Invalid payload size in packet pool</span></span>

<span data-ttu-id="b2d24-162">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-162">**Allowed From**</span></span>

<span data-ttu-id="b2d24-163">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-163">Initialization, Threads</span></span>

<span data-ttu-id="b2d24-164">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-164">**Example**</span></span>

```c
/* Create the HTTP Client instance “my_client” on “ip_0”. */
status = nx_http_client_create(&my_client, “my client”, &ip_0, &pool_0, 100);
  
/* If status is NX_SUCCESS an HTTP Client instance was successfully  created. */
```

## <a name="nx_http_client_delete"></a><span data-ttu-id="b2d24-165">nx_http_client_delete</span><span class="sxs-lookup"><span data-stu-id="b2d24-165">nx_http_client_delete</span></span>

### <a name="delete-an-http-client-instance"></a><span data-ttu-id="b2d24-166">HTTP Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="b2d24-166">Delete an HTTP Client Instance</span></span>

<span data-ttu-id="b2d24-167">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-167">**Prototype**</span></span>

```c
UINT nx_http_client_delete(NX_HTTP_CLIENT *client_ptr);
```

<span data-ttu-id="b2d24-168">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-168">**Description**</span></span>

<span data-ttu-id="b2d24-169">Bu hizmet, önceden oluşturulmuş bir HTTP Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="b2d24-169">This service deletes a previously created HTTP Client instance.</span></span>

<span data-ttu-id="b2d24-170">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-170">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-171">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-171">**client_ptr** Pointer to HTTP Client control block.</span></span>

<span data-ttu-id="b2d24-172">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-172">**Return Values**</span></span>

- <span data-ttu-id="b2d24-173">**NX_SUCCESS** (0x00) başarılı http istemcisi silme</span><span class="sxs-lookup"><span data-stu-id="b2d24-173">**NX_SUCCESS** (0x00) Successful HTTP Client delete</span></span>
- <span data-ttu-id="b2d24-174">NX_PTR_ERROR (0x16) geçersiz HTTP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-174">NX_PTR_ERROR (0x16) Invalid HTTP pointer</span></span>
- <span data-ttu-id="b2d24-175">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-175">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-176">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-176">**Allowed From**</span></span>

<span data-ttu-id="b2d24-177">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-177">Threads</span></span>

<span data-ttu-id="b2d24-178">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-178">**Example**</span></span>

```c
/* Delete the HTTP Client instance “my_client.” */
status = nx_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully  deleted. */
```

## <a name="nx_http_client_get_start"></a><span data-ttu-id="b2d24-179">nx_http_client_get_start</span><span class="sxs-lookup"><span data-stu-id="b2d24-179">nx_http_client_get_start</span></span>

### <a name="start-an-http-get-request"></a><span data-ttu-id="b2d24-180">HTTP GET isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="b2d24-180">Start an HTTP GET request</span></span>

<span data-ttu-id="b2d24-181">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-181">**Prototype**</span></span>

```c
UINT nx_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
                             ULONG ip_address, CHAR *resource, CHAR *input_ptr,
                             UINT input_size, CHAR *username, CHAR *password,
                             ULONG wait_option);
```

<span data-ttu-id="b2d24-182">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-182">**Description**</span></span>

<span data-ttu-id="b2d24-183">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-183">This service attempts to GET the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="b2d24-184">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-184">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="b2d24-185">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="b2d24-185">Note that the resource string can refer to a local file e.g. “/index.htm” or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="b2d24-186">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-186">This service is deprecated.</span></span> <span data-ttu-id="b2d24-187">Geliştiricilerin *nx_http_client_get_start_extended ()* uygulamasına geçirilmesi önerilir</span><span class="sxs-lookup"><span data-stu-id="b2d24-187">Developers are encouraged to migrate to *nx_http_client_get_start_extended()*</span></span>

<span data-ttu-id="b2d24-188">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-188">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-189">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-189">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="b2d24-190">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-190">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="b2d24-191">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-191">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="b2d24-192">**input_ptr** GET isteği için ek verilere yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-192">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="b2d24-193">Bu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-193">This is optional.</span></span> <span data-ttu-id="b2d24-194">Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-194">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
- <span data-ttu-id="b2d24-195">**input_size** İsteğe bağlı ek girişte input_ptr tarafından işaret edilen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-195">**input_size** Number of bytes in optional additional input pointed to by input_ptr.</span></span>
- <span data-ttu-id="b2d24-196">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-196">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="b2d24-197">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-197">**password** Pointer to optional password for authentication.</span></span><span data-ttu-id="b2d24-198">
-\*\*wait_option*\* Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-198">
-\*\*wait_option*\* Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="b2d24-199">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b2d24-199">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="b2d24-200">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="b2d24-200">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="b2d24-201">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="b2d24-201">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="b2d24-202">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-202">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="b2d24-203">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-203">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="b2d24-204">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-204">**Return Values**</span></span>

- <span data-ttu-id="b2d24-205">**NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="b2d24-205">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="b2d24-206">**NX_HTTP_ERROR** (0xE0) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="b2d24-206">**NX_HTTP_ERROR** (0xE0) Internal HTTP Client error</span></span>
- <span data-ttu-id="b2d24-207">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="b2d24-207">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="b2d24-208">**NX_HTTP_FAILED** (0xE2) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="b2d24-208">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="b2d24-209">**NX_HTTP_AUTHENTICATION_ERROR** (0xeb) adı ve/veya parolası geçersiz.</span><span class="sxs-lookup"><span data-stu-id="b2d24-209">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or password.</span></span>
- <span data-ttu-id="b2d24-210">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-210">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-211">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-211">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

<span data-ttu-id="b2d24-212">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-212">**Allowed From**</span></span>

<span data-ttu-id="b2d24-213">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-213">Threads</span></span>

<span data-ttu-id="b2d24-214">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-214">**Example**</span></span>

```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                  NX_NULL, 0, “myname”, “mypassword”, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
far successful. The client must now call *nx_http_client_get_packet* multiple
times to retrieve the content associated with TEST.HTM. */

#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                  POST_MESSAGE, sizeof(POST_MESSAGE),
                                  “myname”, “mypassword”, 1000);
 
/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST 
request for TEST.HTM and successfully sent. */
```


## <a name="nx_http_client_get_start_extended"></a><span data-ttu-id="b2d24-215">nx_http_client_get_start_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-215">nx_http_client_get_start_extended</span></span>

### <a name="start-an-http-get-request"></a><span data-ttu-id="b2d24-216">HTTP GET isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="b2d24-216">Start an HTTP GET request</span></span>

<span data-ttu-id="b2d24-217">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-217">**Prototype**</span></span>

```c
UINT nx_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
     ULONG ip_address, CHAR *resource, UINT resource_length,
     CHAR *input_ptr, UINT input_size, CHAR *username,
     UINT username_length, CHAR *password, UINT password_length,
     ULONG wait_option);
```

<span data-ttu-id="b2d24-218">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-218">**Description**</span></span>

<span data-ttu-id="b2d24-219">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-219">This service attempts to GET the resource specified by “resource” pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="b2d24-220">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_http_client_get_packet* için birden fazla çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-220">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_http_client_get_packet* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="b2d24-221">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="b2d24-221">Note that the resource string can refer to a local file e.g. “/index.htm” or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="b2d24-222">Bu hizmet *nx_http_client_get_start ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-222">This service replaces *nx_http_client_get_start()*.</span></span> <span data-ttu-id="b2d24-223">Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-223">It requires caller to specify the length of the resource, username and password.</span></span>

<span data-ttu-id="b2d24-224">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-224">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-225">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-225">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="b2d24-226">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-226">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="b2d24-227">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-227">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="b2d24-228">**resource_length** İstenen kaynak için URL dizesi uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-228">**resource_length** Length of URL string for requested resource.</span></span>
- <span data-ttu-id="b2d24-229">**input_ptr** GET isteği için ek verilere yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-229">**input_ptr** Pointer to additional data for the GET request.</span></span> <span data-ttu-id="b2d24-230">Bu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-230">This is optional.</span></span> <span data-ttu-id="b2d24-231">Geçerliyse, belirtilen giriş iletinin içerik alanına yerleştirilir ve GET işlemi yerine bir POST kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-231">If valid, the specified input is placed in the content area of the message and a POST is used instead of a GET operation.</span></span>
- <span data-ttu-id="b2d24-232">**input_size** İsteğe bağlı ek girişte input_ptr tarafından işaret edilen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-232">**input_size** Number of bytes in optional additional input pointed to by input_ptr.</span></span>
- <span data-ttu-id="b2d24-233">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-233">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="b2d24-234">**username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-234">**username_length** Length of optional user name for authentication.</span></span>
- <span data-ttu-id="b2d24-235">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-235">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="b2d24-236">**password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-236">**password_length** Length of optional password for authentication.</span></span>
- <span data-ttu-id="b2d24-237">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-237">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="b2d24-238">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b2d24-238">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="b2d24-239">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="b2d24-239">**time out value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="b2d24-240">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="b2d24-240">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="b2d24-241">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-241">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="b2d24-242">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-242">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="b2d24-243">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-243">**Return Values**</span></span>

- <span data-ttu-id="b2d24-244">**NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="b2d24-244">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="b2d24-245">**NX_HTTP_ERROR** (0xE0) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="b2d24-245">**NX_HTTP_ERROR** (0xE0) Internal HTTP Client error</span></span>
- <span data-ttu-id="b2d24-246">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="b2d24-246">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="b2d24-247">**NX_HTTP_FAILED** (0xE2) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="b2d24-247">**NX_HTTP_FAILED** (0xE2) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="b2d24-248">**NX_HTTP_AUTHENTICATION_ERROR** (0xeb) adı ve/veya parolası geçersiz.</span><span class="sxs-lookup"><span data-stu-id="b2d24-248">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or password.</span></span>
- <span data-ttu-id="b2d24-249">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-249">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-250">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-250">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

<span data-ttu-id="b2d24-251">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-251">**Allowed From**</span></span>

<span data-ttu-id="b2d24-252">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-252">Threads</span></span>

<span data-ttu-id="b2d24-253">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-253">**Example**</span></span>
            
```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5),
                                           “/TEST.HTM”,
                                           9, NX_NULL, 0, “myname”, 6,
                                           “mypassword”, 10, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
far successful. The client must now call *nx_http_client_get_packet* multiple
times to retrieve the content associated with TEST.HTM. */

#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5), 
                                           “/TEST.HTM”,
                                           9, POST_MESSAGE, sizeof(POST_MESSAGE),
                                           “myname”, 6, “mypassword”, 10, 1000);

/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST 
request for TEST.HTM and successfully sent. */
```

## <a name="nx_http_client_get_packet"></a><span data-ttu-id="b2d24-254">nx_http_client_get_packet</span><span class="sxs-lookup"><span data-stu-id="b2d24-254">nx_http_client_get_packet</span></span>

### <a name="get-next-resource-data-packet"></a><span data-ttu-id="b2d24-255">Sonraki kaynak veri paketini al</span><span class="sxs-lookup"><span data-stu-id="b2d24-255">Get next resource data packet</span></span>

<span data-ttu-id="b2d24-256">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-256">**Prototype**</span></span>

```c
UINT nx_http_client_get_packet(NX_HTTP_CLIENT *client_ptr,
                              NX_PACKET **packet_ptr,
                              ULONG wait_option);
```

<span data-ttu-id="b2d24-257">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-257">**Description**</span></span>

<span data-ttu-id="b2d24-258">Bu hizmet, önceki *nx_http_client_get_start* çağrısı tarafından istenen kaynağın sonraki içerik paketini alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-258">This service retrieves the next packet of content of the resource requested by the previous *nx_http_client_get_start* call.</span></span> <span data-ttu-id="b2d24-259">NX_HTTP_GET_DONE geri dönüş durumu alınana kadar bu yordama yönelik ardışık çağrılar yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-259">Successive calls to this routine should be made until the return status of NX_HTTP_GET_DONE is received.</span></span>

<span data-ttu-id="b2d24-260">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-260">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-261">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-261">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="b2d24-262">**packet_ptr** Kısmi kaynak içeriği içeren paket işaretçisi hedefi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-262">**packet_ptr** Destination for packet pointer containing partial resource content.</span></span>
- <span data-ttu-id="b2d24-263">**wait_option** Hizmetin HTTP Istemcisi alma paketi için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-263">**wait_option** Defines how long the service will wait for the HTTP Client get packet.</span></span> <span data-ttu-id="b2d24-264">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b2d24-264">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="b2d24-265">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="b2d24-265">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="b2d24-266">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="b2d24-266">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="b2d24-267">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-267">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="b2d24-268">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-268">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="b2d24-269">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-269">**Return Values**</span></span>

- <span data-ttu-id="b2d24-270">**NX_SUCCESS** (0x00) başarılı http istemcisi Get paketi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-270">**NX_SUCCESS** (0x00) Successful HTTP Client get packet.</span></span>
- <span data-ttu-id="b2d24-271">**NX_HTTP_GET_DONE** (0xEC) http istemcisi Get paketi bitti</span><span class="sxs-lookup"><span data-stu-id="b2d24-271">**NX_HTTP_GET_DONE** (0xEC) HTTP Client get packet is done</span></span>
- <span data-ttu-id="b2d24-272">**NX_HTTP_NOT_READY** (0xea) http istemcisi Get modunda değil.</span><span class="sxs-lookup"><span data-stu-id="b2d24-272">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not in get mode.</span></span>
- <span data-ttu-id="b2d24-273">**NX_HTTP_BAD_PACKET_LENGTH** (0faksla) geçersiz paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="b2d24-273">**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Invalid packet length</span></span>
- <span data-ttu-id="b2d24-274">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-274">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-275">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-275">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-276">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-276">**Allowed From**</span></span>

<span data-ttu-id="b2d24-277">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-277">Threads</span></span>

<span data-ttu-id="b2d24-278">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-278">**Example**</span></span>

```c
/* Get the next packet of resource content on the HTTP Client “my_client.”
Note that the nx_http_client_get_start routine must have been called
previously. */
status = nx_http_client_get_packet(&my_client, &next_packet, 1000);
 
/* If status is NX_SUCCESS, the next packet of content is pointed to by 
“next_packet”. */
```

## <a name="nx_http_client_put_start"></a><span data-ttu-id="b2d24-279">nx_http_client_put_start</span><span class="sxs-lookup"><span data-stu-id="b2d24-279">nx_http_client_put_start</span></span>

### <a name="start-an-http-put-request"></a><span data-ttu-id="b2d24-280">HTTP PUT isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="b2d24-280">Start an HTTP PUT request</span></span> 

<span data-ttu-id="b2d24-281">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-281">**Prototype**</span></span>

```c
UINT nx_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                             ULONG ip_address, CHAR *resource,
                             CHAR *username, CHAR *password,
                             ULONG total_bytes, ULONG wait_option);
```

<span data-ttu-id="b2d24-282">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-282">**Description**</span></span>

<span data-ttu-id="b2d24-283">Bu hizmet, belirtilen IP adresindeki HTTP sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-283">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address.</span></span> <span data-ttu-id="b2d24-284">Bu yordam başarılı olursa uygulama kodu, kaynak içeriğini HTTP sunucusuna gerçekten göndermek için *nx_http_client_put_packet* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-284">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet* routine to actually send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="b2d24-285">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="b2d24-285">Note that the resource string can refer to a local file e.g. “/index.htm” or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="b2d24-286">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-286">This service is deprecated.</span></span> <span data-ttu-id="b2d24-287">Geliştiricilerin *nx_http_client_put_start_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-287">Developers are encouraged to migrate to *nx_http_client_put_start_extended()*.</span></span>

<span data-ttu-id="b2d24-288">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-288">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-289">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-289">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="b2d24-290">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-290">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="b2d24-291">**kaynak** Sunucuya gönderilen kaynağın URL dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-291">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="b2d24-292">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-292">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="b2d24-293">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-293">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="b2d24-294">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-294">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="b2d24-295">*Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-295">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
- <span data-ttu-id="b2d24-296">**wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-296">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="b2d24-297">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b2d24-297">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="b2d24-298">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="b2d24-298">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="b2d24-299">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="b2d24-299">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="b2d24-300">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-300">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="b2d24-301">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-301">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="b2d24-302">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-302">**Return Values**</span></span>

- <span data-ttu-id="b2d24-303">**NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="b2d24-303">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="b2d24-304">**NX_HTTP_USERNAME_TOO_LONG**</span><span class="sxs-lookup"><span data-stu-id="b2d24-304">**NX_HTTP_USERNAME_TOO_LONG**</span></span>
- <span data-ttu-id="b2d24-305">**(0xF1) Kullanıcı adı arabellek için çok büyük**</span><span class="sxs-lookup"><span data-stu-id="b2d24-305">**(0xF1) Username too large for buffer**</span></span>
- <span data-ttu-id="b2d24-306">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="b2d24-306">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="b2d24-307">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-307">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-308">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="b2d24-308">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="b2d24-309">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-309">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-310">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-310">**Allowed From**</span></span>

<span data-ttu-id="b2d24-311">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-311">Threads</span></span>

<span data-ttu-id="b2d24-312">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-312">**Example**</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP 
Server at IP address 1.2.3.5. */
status = nx_http_client_put_start(&my_client, IP_ADDRESS(1, 2, 3, 5),
                                 “/TEST.HTM”, “myname”, “mypassword”, 20, 
                                 NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully 
been started. */
```

## <a name="nx_http_client_put_start_extended"></a><span data-ttu-id="b2d24-313">nx_http_client_put_start_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-313">nx_http_client_put_start_extended</span></span>

### <a name="start-an-http-put-request"></a><span data-ttu-id="b2d24-314">HTTP PUT isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="b2d24-314">Start an HTTP PUT request</span></span>

<span data-ttu-id="b2d24-315">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-315">**Prototype**</span></span>

```c
UINT nx_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
     ULONG ip_address, CHAR *resource, UINT resource_length,
     CHAR *username,UINT username_length, CHAR *password,
     UINT password_length, ULONG total_bytes, ULONG wait_option);
```

<span data-ttu-id="b2d24-316">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-316">**Description**</span></span>

<span data-ttu-id="b2d24-317">Bu hizmet, belirtilen IP adresindeki HTTP sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-317">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address.</span></span> <span data-ttu-id="b2d24-318">Bu yordam başarılı olursa uygulama kodu, kaynak içeriğini HTTP sunucusuna gerçekten göndermek için *nx_http_client_put_packet* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-318">If this routine is successful, the application code should make successive calls to the *nx_http_client_put_packet* routine to actually send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="b2d24-319">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="b2d24-319">Note that the resource string can refer to a local file e.g. “/index.htm” or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="b2d24-320">Bu hizmet *nx_http_client_put_start ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-320">This service replaces *nx_http_client_put_start()*.</span></span> <span data-ttu-id="b2d24-321">Çağıranın kaynak, Kullanıcı adı ve parola uzunluğunu belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-321">It requires caller to specify the length of the resource, username and password.</span></span>

<span data-ttu-id="b2d24-322">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-322">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-323">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-323">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="b2d24-324">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-324">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="b2d24-325">**kaynak** Sunucuya gönderilen kaynağın URL dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-325">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="b2d24-326">**resource_length** Sunucuya gönderilen kaynağın URL dizesi uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-326">**resource_length** Length of URL string for resource to send to Server.</span></span>
- <span data-ttu-id="b2d24-327">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-327">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="b2d24-328">**username_length** Kimlik doğrulaması için isteğe bağlı kullanıcı adının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-328">**username_length** Length of optional user name for authentication.</span></span>
- <span data-ttu-id="b2d24-329">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-329">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="b2d24-330">**password_length** Kimlik doğrulaması için isteğe bağlı parolanın uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-330">**password_length** Length of optional password for authentication.</span></span>
- <span data-ttu-id="b2d24-331">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-331">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="b2d24-332">*Nx_http_client_put_packet* sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-332">Note that the combined length of all packets sent via subsequent calls to *nx_http_client_put_packet* must equal this value.</span></span>
- <span data-ttu-id="b2d24-333">**wait_option** Hizmetin HTTP Istemcisi PUT başlatması için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-333">**wait_option** Defines how long the service will wait for the HTTP Client PUT start.</span></span> <span data-ttu-id="b2d24-334">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b2d24-334">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="b2d24-335">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="b2d24-335">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="b2d24-336">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="b2d24-336">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="b2d24-337">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-337">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /><span data-ttu-id="b2d24-338">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-338">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="b2d24-339">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-339">**Return Values**</span></span>

- <span data-ttu-id="b2d24-340">**NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="b2d24-340">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="b2d24-341">**NX_HTTP_USERNAME_TOO_LONG** (0xf1) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="b2d24-341">**NX_HTTP_USERNAME_TOO_LONG** (0xF1) Username too large for buffer</span></span>
- <span data-ttu-id="b2d24-342">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="b2d24-342">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="b2d24-343">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-343">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-344">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="b2d24-344">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="b2d24-345">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-345">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-346">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-346">**Allowed From**</span></span>

<span data-ttu-id="b2d24-347">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-347">Threads</span></span>

<span data-ttu-id="b2d24-348">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-348">**Example**</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP 
Server at IP address 1.2.3.5. */
status = nx_http_client_put_start_extended(&my_client, IP_ADDRESS(1, 2, 3, 5),
                                          “/TEST.HTM”, 9, “myname”, 6, 
                                          “mypassword”, 
                                          10, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully 
been started. */
```

## <a name="nx_http_client_put_packet"></a><span data-ttu-id="b2d24-349">nx_http_client_put_packet</span><span class="sxs-lookup"><span data-stu-id="b2d24-349">nx_http_client_put_packet</span></span>

### <a name="send-next-resource-data-packet"></a><span data-ttu-id="b2d24-350">Sonraki kaynak veri paketini gönder</span><span class="sxs-lookup"><span data-stu-id="b2d24-350">Send next resource data packet</span></span>

<span data-ttu-id="b2d24-351">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-351">**Prototype**</span></span>

```c
UINT nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                              NX_PACKET *packet_ptr,
                              ULONG wait_option);
```

<span data-ttu-id="b2d24-352">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-352">**Description**</span></span>

<span data-ttu-id="b2d24-353">Bu hizmet, kaynak içeriğinin bir sonraki paketini HTTP sunucusuna gönderilmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-353">This service attempts to send the next packet of resource content to the HTTP Server.</span></span> <span data-ttu-id="b2d24-354">Gönderilen paketlerin Birleşik uzunluğu önceki *nx_http_client_put_start ()* çağrısında belirtilen "total_bytes" değerine eşit olana kadar bu yordamın kaldı olarak çağrılması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-354">Note that this routine should be called repetitively until the combined length of the packets sent equals the “total_bytes” specified in the previous *nx_http_client_put_start()* call.</span></span>

<span data-ttu-id="b2d24-355">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-355">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-356">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-356">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="b2d24-357">**packet_ptr** HTTP sunucusuna gönderilen kaynağın bir sonraki içeriğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-357">**packet_ptr** Pointer to next content of the resource to being sent to the HTTP Server.</span></span>
- <span data-ttu-id="b2d24-358">**wait_option** Hizmetin, iç olarak HTTP Istemcisi PUT paketini işlemesini ne kadar bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-358">**wait_option** Defines how long the service will wait internally to process the HTTP Client PUT packet.</span></span> <span data-ttu-id="b2d24-359">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b2d24-359">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="b2d24-360">**zaman aşımı değeri** (0x00000001 üzerinden 0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="b2d24-360">**timeout value** (0x00000001 through 0xFFFFFFFE)</span></span>
  - <span data-ttu-id="b2d24-361">**TX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="b2d24-361">**TX_WAIT_FOREVER** (0xFFFFFFFF)</span></span><br /><span data-ttu-id="b2d24-362">TX_WAIT_FOREVER seçildiğinde çağıran iş parçacığının HTTP sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-362">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span><br /> <span data-ttu-id="b2d24-363">Sayısal bir değer (0x1-0xFFFFFFFE) seçildiğinde, HTTP sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-363">Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

<span data-ttu-id="b2d24-364">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-364">**Return Values**</span></span>

- <span data-ttu-id="b2d24-365">**NX_SUCCESS** (0x00) http Istemci paketini başarıyla gönderdi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-365">**NX_SUCCESS** (0x00) Successfully sent HTTP Client packet.</span></span>
- <span data-ttu-id="b2d24-366">**NX_HTTP_NOT_READY** (0xea) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="b2d24-366">**NX_HTTP_NOT_READY** (0xEA) HTTP Client not ready</span></span>
- <span data-ttu-id="b2d24-367">**NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0Xee) sunucu hatası kodu aldı \* *-\*\*NX_HTTP_BAD_PACKET_LENGTH*\* (0.) geçersiz paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="b2d24-367">**NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0xEE) Received Server error code\*\* -**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Invalid packet length</span></span>
- <span data-ttu-id="b2d24-368">**NX_HTTP_AUTHENTICATION_ERROR** (0xeb) geçersiz ad ve/veya parola</span><span class="sxs-lookup"><span data-stu-id="b2d24-368">**NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Invalid name and/or Password</span></span>
- <span data-ttu-id="b2d24-369">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) sunucu, put tamamlanmadan önce yanıt veriyor</span><span class="sxs-lookup"><span data-stu-id="b2d24-369">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Server responds before PUT Is complete</span></span>
- <span data-ttu-id="b2d24-370">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-370">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-371">NX_INVALID_PACKET (0x12) paketi TCP üst bilgisi için çok küçük</span><span class="sxs-lookup"><span data-stu-id="b2d24-371">NX_INVALID_PACKET (0x12) Packet too small for TCP header</span></span>
- <span data-ttu-id="b2d24-372">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-372">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-373">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-373">**Allowed From**</span></span>

<span data-ttu-id="b2d24-374">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-374">Threads</span></span>

<span data-ttu-id="b2d24-375">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-375">**Example**</span></span>

```c
/* Send a 20-byte packet representing the content of the resource
“/TEST.HTM” to the HTTP Server. */
status = nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                                  NX_PACKET *packet_ptr,
                                  ULONG wait_option);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM
has successfully been sent. */
```

## <a name="nx_http_client_set_connect_port"></a><span data-ttu-id="b2d24-376">nx_http_client_set_connect_port</span><span class="sxs-lookup"><span data-stu-id="b2d24-376">nx_http_client_set_connect_port</span></span>

### <a name="set-the-connection-port-to-the-server"></a><span data-ttu-id="b2d24-377">Bağlantı noktasını sunucuya ayarla</span><span class="sxs-lookup"><span data-stu-id="b2d24-377">Set the connection port to the Server</span></span>

<span data-ttu-id="b2d24-378">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-378">**Prototype**</span></span>

```c
UINT nx_http_client_set_connect_port(NX_HTTP_CLIENT *client_ptr,
                                    UINT port);
```

<span data-ttu-id="b2d24-379">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-379">**Description**</span></span>

<span data-ttu-id="b2d24-380">Bu hizmet, HTTP sunucusuna, çalışma zamanında belirtilen bağlantı noktasına bağlanırken bağlantı noktasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-380">This service changes the connect port when connecting to the HTTP Server to the specified port at runtime.</span></span> <span data-ttu-id="b2d24-381">Aksi takdirde, bağlantı noktası varsayılan olarak 80 ' dir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-381">Otherwise the connect port defaults to 80.</span></span> <span data-ttu-id="b2d24-382">Bunun *nx_http_client_get_start*() ve *nx_http_client_put_start*() öncesinde ÇAĞRıLMASı gerekir, örneğin http istemcisi sunucusuyla bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-382">This must be called before *nx_http_client_get_start*() and *nx_http_client_put_start*() e.g. when the HTTP Client connects with the Server.</span></span>

<span data-ttu-id="b2d24-383">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-383">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-384">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-384">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="b2d24-385">**bağlantı noktası** Sunucuya bağlanmak için bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="b2d24-385">**port** Port for connecting to the Server.</span></span>

<span data-ttu-id="b2d24-386">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-386">**Return Values**</span></span>

- <span data-ttu-id="b2d24-387">**NX_SUCCESS** (0x00) bağlantı noktasını başarıyla değiştirdi</span><span class="sxs-lookup"><span data-stu-id="b2d24-387">**NX_SUCCESS** (0x00) Successfully changed the connect port</span></span>
- <span data-ttu-id="b2d24-388">**NX_INVALID_PORT** (0X46) bağlantı noktası en büyük değeri (0xFFFF) aşıyor veya sıfır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-388">**NX_INVALID_PORT** (0x46) Port exceeds the maximum (0xFFFF) or is zero.</span></span>
- <span data-ttu-id="b2d24-389">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-389">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-390">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-390">**Allowed From**</span></span>

<span data-ttu-id="b2d24-391">İş parçacıkları, başlatma</span><span class="sxs-lookup"><span data-stu-id="b2d24-391">Threads, Initialization</span></span>

<span data-ttu-id="b2d24-392">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-392">**Example**</span></span>

```c
NX_HTTP_CLIENT *client_ptr;

/* Change the connect port to 114. */
status = nx_http_client_set_connect_port(client_ptr, 114);

/* If status is NX_SUCCESS, the connect port is successfully changed. */
```

## <a name="nx_http_server_cache_info_callback_set"></a><span data-ttu-id="b2d24-393">nx_http_server_cache_info_callback_set</span><span class="sxs-lookup"><span data-stu-id="b2d24-393">nx_http_server_cache_info_callback_set</span></span>

### <a name="set-the-callback-to-retrieve-url-max-age-and-date"></a><span data-ttu-id="b2d24-394">URL 'YI en yüksek yaş ve tarihi almak için geri aramayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b2d24-394">Set the callback to retrieve URL max age and date</span></span>

<span data-ttu-id="b2d24-395">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-395">**Prototype**</span></span>

```c
UINT nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                                           UINT (*cache_info_get)(CHAR *resource,
                                           UINT *max_age,
                                           NX_HTTP_SERVER_DATE *date));
```

<span data-ttu-id="b2d24-396">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-396">**Description**</span></span>

<span data-ttu-id="b2d24-397">Bu hizmet, belirtilen kaynağın yaş ve son değiştirilme tarihini elde etmek için çağrılan geri çağırma hizmetini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-397">This service sets the callback service invoked to obtain the maximum age and last modified date of the specified resource.</span></span>

<span data-ttu-id="b2d24-398">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-398">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-399">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-399">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="b2d24-400">**cache_info_get** Geri çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-400">**cache_info_get** Pointer to the callback</span></span>
- <span data-ttu-id="b2d24-401">**max_age** Bir kaynağın maksimum yaşı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-401">**max_age** Pointer to maximum age of a resource</span></span>
- <span data-ttu-id="b2d24-402">**veri** Son değiştirme tarihine yönelik işaretçi döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="b2d24-402">**data** Pointer to last modified date returned.</span></span>

<span data-ttu-id="b2d24-403">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-403">**Return Values**</span></span>

- <span data-ttu-id="b2d24-404">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="b2d24-404">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="b2d24-405">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-405">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-406">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-406">**Allowed From**</span></span>

<span data-ttu-id="b2d24-407">Başlatma</span><span class="sxs-lookup"><span data-stu-id="b2d24-407">Initialization</span></span>

<span data-ttu-id="b2d24-408">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-408">**Example**</span></span>

```c
NX_HTTP_SERVER my_server;
UINT cache_info_get(CHAR *resource, UINT *max_age,
                   NX_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_http_server_create and before the HTTP
server is set by nx_http_server_start(), set the cache info callback: */
status = nx_http_server_cache_info_callback_set(&my_server, cache_info_get);

/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_http_server_callback_data_send"></a><span data-ttu-id="b2d24-409">nx_http_server_callback_data_send</span><span class="sxs-lookup"><span data-stu-id="b2d24-409">nx_http_server_callback_data_send</span></span>

### <a name="send-data-from-callback-function"></a><span data-ttu-id="b2d24-410">Geri çağırma işlevinden veri Gönder</span><span class="sxs-lookup"><span data-stu-id="b2d24-410">Send data from callback function</span></span>

<span data-ttu-id="b2d24-411">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-411">**Prototype**</span></span>

```c
UINT nx_http_server_callback_data_send(NX_HTTP_SERVER *server_ptr,
                                      VOID *data_ptr,
                                      ULONG data_length);
```

<span data-ttu-id="b2d24-412">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-412">**Description**</span></span>

<span data-ttu-id="b2d24-413">Bu hizmet, sağlanan paketteki verileri uygulamanın geri arama yordamından gönderir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-413">This service sends the data in the supplied packet from the application’s callback routine.</span></span> <span data-ttu-id="b2d24-414">Bu, genellikle GET/POST istekleri ile ilişkili dinamik verileri göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-414">This is typically used to send dynamic data associated with GET/POST requests.</span></span> <span data-ttu-id="b2d24-415">Bu işlev kullanıldığında, tüm yanıtın doğru biçimde gönderilmesi için geri çağırma yordamının sorumlu olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-415">Note that if this function is used, the callback routine is responsible for sending the entire response in the proper format.</span></span> <span data-ttu-id="b2d24-416">Ayrıca, geri arama yordamı NX_HTTP_CALLBACK_COMPLETED durumunu döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-416">In addition, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="b2d24-417">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-417">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-418">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-418">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="b2d24-419">**data_ptr** Gönderilen verilerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-419">**data_ptr** Pointer to the data to send.</span></span>
- <span data-ttu-id="b2d24-420">**data_length** Gönderilen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-420">**data_length** Number of bytes to send.</span></span>

<span data-ttu-id="b2d24-421">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-421">**Return Values**</span></span>

- <span data-ttu-id="b2d24-422">**NX_SUCCESS** (0x00) sunucu verilerini başarıyla gönderdi</span><span class="sxs-lookup"><span data-stu-id="b2d24-422">**NX_SUCCESS** (0x00) Successfully sent Server data</span></span>
- <span data-ttu-id="b2d24-423">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-423">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-424">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-424">**Allowed From**</span></span>

<span data-ttu-id="b2d24-425">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-425">Threads</span></span>

<span data-ttu-id="b2d24-426">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-426">**Example**</span></span>

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
       (strcmp(resource, "/test.htm") == 0))
    {
        /* Found it, override the GET processing by sending the resource
        contents directly. */

        nx_http_server_callback_data_send(server_ptr,
                                         "HTTP/1.0 200 \r\nContent-Length:
                                         103\r\nContent-Type: text/html\r\n\r\n",
                                         63);
        nx_http_server_callback_data_send(server_ptr, "<HTML>> r\n<HEAD><TITLE>NetX
                                         HTTP Test </TITLE></HEAD>\r\n
                                         <BODY>\r\n<H1>NetX Test Page
                                         </H1>\r\n</BODY>> r\n</HTML>\r\n", 103);
        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }
    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_generate_response_header"></a><span data-ttu-id="b2d24-427">nx_http_server_callback_generate_response_header</span><span class="sxs-lookup"><span data-stu-id="b2d24-427">nx_http_server_callback_generate_response_header</span></span>

### <a name="create-a-response-header-in-a-callback-function"></a><span data-ttu-id="b2d24-428">Geri arama işlevinde yanıt üst bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2d24-428">Create a response header in a callback function</span></span>

<span data-ttu-id="b2d24-429">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-429">**Prototype**</span></span>

```c
UINT nx_http_server_callback_generate_response_header(NX_HTTP_SERVER *server_ptr,
     NX_PACKET **packet_pptr, CHAR *status_code, UINT content_length,
     CHAR *content_type, CHAR* additional_header);
```

<span data-ttu-id="b2d24-430">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-430">**Description**</span></span>

<span data-ttu-id="b2d24-431">HTTP sunucusu Istemci GET, put ve DELETE isteklerine yanıt verdiğinde, bu hizmet _ *nx_http_server_generate_response_header* iç işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-431">This service calls the internal function _ *nx_http_server_generate_response_header* when the HTTP server responds to Client get, put and delete requests.</span></span> <span data-ttu-id="b2d24-432">HTTP sunucusu uygulaması Istemciye yanıtını tasarlarken HTTP sunucusu geri çağırma işlevlerinde kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-432">It is intended for use in HTTP server callback functions when the HTTP server application is designing its response to the Client.</span></span>

<span data-ttu-id="b2d24-433">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-433">This service is deprecated.</span></span> <span data-ttu-id="b2d24-434">Geliştiricilerin *nxd_http_server_callback_generate_response_header_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-434">Developers are encouraged to migrate to *nxd_http_server_callback_generate_response_header_extended()*.</span></span>

<span data-ttu-id="b2d24-435">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-435">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-436">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-436">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="b2d24-437">**packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-437">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
- <span data-ttu-id="b2d24-438">**status_code** Kaynağın durumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="b2d24-438">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="b2d24-439">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="b2d24-439">Examples:</span></span>
- <span data-ttu-id="b2d24-440">**NX_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="b2d24-440">**NX_HTTP_STATUS_OK**</span></span>
- <span data-ttu-id="b2d24-441">**NX_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="b2d24-441">**NX_HTTP_STATUS_MODIFIED**</span></span>
- <span data-ttu-id="b2d24-442">**NX_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="b2d24-442">**NX_HTTP_STATUS_INTERNAL_ERROR**</span></span>
- <span data-ttu-id="b2d24-443">**CONTENT_LENGTH** İçerik boyutu (bayt)</span><span class="sxs-lookup"><span data-stu-id="b2d24-443">**content_length** Size of content in bytes</span></span>
- <span data-ttu-id="b2d24-444">**content_type** HTTP türü, örneğin "metin/düz"</span><span class="sxs-lookup"><span data-stu-id="b2d24-444">**content_type** Type of HTTP e.g. “text/plain”</span></span>
- <span data-ttu-id="b2d24-445">**additional_header** Ek üst bilgi metnine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-445">**additional_header** Pointer to additional header text</span></span>

<span data-ttu-id="b2d24-446">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-446">**Return Values**</span></span>

- <span data-ttu-id="b2d24-447">**NX_SUCCESS** (0x00) HTML üst bilgisi başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="b2d24-447">**NX_SUCCESS** (0x00) Successfully created HTML header</span></span>
- <span data-ttu-id="b2d24-448">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-448">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-449">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-449">**Allowed From**</span></span>

<span data-ttu-id="b2d24-450">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-450">Threads</span></span>

<span data-ttu-id="b2d24-451">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-451">**Example**</span></span>

```c
CHAR demotestbuffer[] = “<html>\r\n\r\n<head> r\n\r\n<title>Main                 \
                        Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n  \ 
                        </body>\r\n</html>\r\n";

/* my_request_notify is the application request notify callback registered with
the HTTP server in nx_http_server_create, creates a response to the received
Client request. */

UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET     *sresp_packet_ptr;
    ULONG         string_length;
    CHAR          temp_string[30];
    ULONG         length = 0;

        length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length = (ULONG) nx_http_server_type_get(server_ptr, server_ptr ->
                   nx_http_server_request_resource, temp_string);

/* Null terminate the string. */
   temp_string[temp] = 0;

/* Now build a response header with server status is OK and no additional header info. */
   status = nx_http_server_callback_generate_response_header(http_server_ptr,
            &resp_packet_ptr, NX_HTTP_STATUS_OK,
            length, temp_string, NX_NULL);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
            length, server_ptr >>
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

## <a name="nx_http_server_callback_generate_response_header_extended"></a><span data-ttu-id="b2d24-452">nx_http_server_callback_generate_response_header_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-452">nx_http_server_callback_generate_response_header_extended</span></span>

### <a name="create-a-response-header-in-a-callback-function"></a><span data-ttu-id="b2d24-453">Geri arama işlevinde yanıt üst bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2d24-453">Create a response header in a callback function</span></span>

<span data-ttu-id="b2d24-454">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-454">**Prototype**</span></span>

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

<span data-ttu-id="b2d24-455">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-455">**Description**</span></span>

<span data-ttu-id="b2d24-456">Bu hizmet, HTTP sunucusu Istemci GET, put ve DELETE isteklerine yanıt verdiğinde _ *nx_http_server_generate_response_header ()* iç işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-456">This service calls the internal function _ *nx_http_server_generate_response_header()* when the HTTP server responds to Client get, put and delete requests.</span></span> <span data-ttu-id="b2d24-457">HTTP sunucusu uygulaması Istemciye yanıtını tasarlarken HTTP sunucusu geri çağırma işlevlerinde kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-457">It is intended for use in HTTP server callback functions when the HTTP server application is designing its response to the Client.</span></span>

<span data-ttu-id="b2d24-458">Bu hizmet *nx_http_server_callback_generate_response_header ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-458">This service replaces *nx_http_server_callback_generate_response_header()*.</span></span> <span data-ttu-id="b2d24-459">Bu sürüm, geri çağırma işlevine ek uzunluk bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-459">This version supplies additional length information to the callback function.</span></span>

<span data-ttu-id="b2d24-460">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-460">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-461">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-461">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="b2d24-462">**packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-462">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
- <span data-ttu-id="b2d24-463">**status_code** Kaynağın durumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="b2d24-463">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="b2d24-464">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="b2d24-464">Examples:</span></span>
  - <span data-ttu-id="b2d24-465">**NX_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="b2d24-465">**NX_HTTP_STATUS_OK**</span></span>
  - <span data-ttu-id="b2d24-466">**NX_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="b2d24-466">**NX_HTTP_STATUS_MODIFIED**</span></span>
  - <span data-ttu-id="b2d24-467">**NX_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="b2d24-467">**NX_HTTP_STATUS_INTERNAL_ERROR**</span></span>
- <span data-ttu-id="b2d24-468">**status_code** Durum kodu uzunluğu</span><span class="sxs-lookup"><span data-stu-id="b2d24-468">**status_code** Length of status code</span></span>
- <span data-ttu-id="b2d24-469">**CONTENT_LENGTH** İçerik boyutu (bayt)</span><span class="sxs-lookup"><span data-stu-id="b2d24-469">**content_length** Size of content in bytes</span></span>
- <span data-ttu-id="b2d24-470">**content_type** HTTP türü, örneğin "metin/düz"</span><span class="sxs-lookup"><span data-stu-id="b2d24-470">**content_type** Type of HTTP e.g. “text/plain”</span></span>
- <span data-ttu-id="b2d24-471">**content_type_length** HTTP türünün uzunluğu</span><span class="sxs-lookup"><span data-stu-id="b2d24-471">**content_type_length** Length of HTTP type</span></span>
- <span data-ttu-id="b2d24-472">**additional_header** Ek üst bilgi metnine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-472">**additional_header** Pointer to additional header text</span></span>
- <span data-ttu-id="b2d24-473">**additional_header_length** Ek üst bilgi metninin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="b2d24-473">**additional_header_length** Length of additional header text</span></span>

<span data-ttu-id="b2d24-474">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-474">**Return Values**</span></span>

- <span data-ttu-id="b2d24-475">**NX_SUCCESS** (0x00) başarıyla oluşturuldu üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-475">**NX_SUCCESS** (0x00) Successfully created header</span></span>
- <span data-ttu-id="b2d24-476">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-476">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-477">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-477">**Allowed From**</span></span>

<span data-ttu-id="b2d24-478">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-478">Threads</span></span>

<span data-ttu-id="b2d24-479">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-479">**Example**</span></span>

```c
  CHAR demotestbuffer[] = “<html>\r\n\r\n<head>\r\n\r\n<title>Main                    \
                          Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n     \
                          </body>\r\n</html>\r\n";

/* my_request_notify is the application request notify callback registered with
   the HTTP server in nx_http_server_create, creates a response to the received
   Client request. */

   UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                         CHAR *resource, NX_PACKET *recv_packet_ptr)
   {
     NX_PACKET *sresp_packet_ptr;
     ULONG string_length;
     CHAR temp_string[30];
     ULONG length = 0;

     length = sizeof(demotestbuffer) - 1;

    /* Derive the client request type from the client request. */
       string_length = (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr >>
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
                length, server_ptr ->
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

## <a name="nx_http_server_callback_packet_send"></a><span data-ttu-id="b2d24-480">nx_http_server_callback_packet_send</span><span class="sxs-lookup"><span data-stu-id="b2d24-480">nx_http_server_callback_packet_send</span></span>

### <a name="send-an-http-packet-from-callback-function"></a><span data-ttu-id="b2d24-481">Geri çağırma işlevinden HTTP paketi gönder</span><span class="sxs-lookup"><span data-stu-id="b2d24-481">Send an HTTP packet from callback function</span></span>

<span data-ttu-id="b2d24-482">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-482">**Prototype**</span></span>

```c
UINT nx_http_server_callback_packet_send(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET *packet_ptr);
```

<span data-ttu-id="b2d24-483">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-483">**Description**</span></span>

<span data-ttu-id="b2d24-484">Bu hizmet, HTTP geri çağrısından gelen bir HTTP Sunucu yanıtı gönderir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-484">This service sends a complete HTTP server response from an HTTP callback.</span></span> <span data-ttu-id="b2d24-485">HTTP sunucusu, paketi NX_HTTP_SERVER _TIMEOUT_SEND gönderecek.</span><span class="sxs-lookup"><span data-stu-id="b2d24-485">HTTP server will send the packet with the NX_HTTP_SERVER _TIMEOUT_SEND.</span></span> <span data-ttu-id="b2d24-486">HTTP üst bilgisi ve verilerinin pakete eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-486">The HTTP header and data must be appended to the packet.</span></span> <span data-ttu-id="b2d24-487">Dönüş durumu bir hata gösteriyorsa, HTTP uygulaması paketi serbest bırakmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-487">If the return status indicates an error, the HTTP application must release the packet.</span></span>

<span data-ttu-id="b2d24-488">Geri çağırma NX_HTTP_CALLBACK_COMPLETED döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-488">The callback should return NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="b2d24-489">Daha ayrıntılı bir örnek için bkz. *nx_http_server_callback_generate_response_header ()* .</span><span class="sxs-lookup"><span data-stu-id="b2d24-489">See *nx_http_server_callback_generate_response_header()* for a more detailed example.</span></span>

<span data-ttu-id="b2d24-490">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-490">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-491">**server_ptr** HTTP sunucu denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-491">**server_ptr** Pointer to HTTP Server control block</span></span>
- <span data-ttu-id="b2d24-492">**packet_ptr** Gönderilmek üzere paket işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-492">**packet_ptr** Pointer to the packet to send</span></span>

<span data-ttu-id="b2d24-493">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-493">**Return Values**</span></span>

- <span data-ttu-id="b2d24-494">**NX_SUCCESS** (0x00) http sunucusu paketini başarıyla gönderdi</span><span class="sxs-lookup"><span data-stu-id="b2d24-494">**NX_SUCCESS** (0x00) Successfully sent HTTP Server packet</span></span>
- <span data-ttu-id="b2d24-495">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-495">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-496">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-496">**Allowed From**</span></span>

<span data-ttu-id="b2d24-497">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-497">Threads</span></span>

<span data-ttu-id="b2d24-498">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-498">**Example**</span></span>

```c
/* The packet is appended with HTTP header and data and is ready to send to the
Client directly. */

   status = nx_http_server_callback_response_send**(server_ptr, packet_ptr);
   
   if (status != NX_SUCCESS)
   {
        nx_packet_release(packet_ptr);
   }
    return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_callback_response_send"></a><span data-ttu-id="b2d24-499">nx_http_server_callback_response_send</span><span class="sxs-lookup"><span data-stu-id="b2d24-499">nx_http_server_callback_response_send</span></span>

### <a name="send-response-from-callback-function"></a><span data-ttu-id="b2d24-500">Geri çağırma işlevinden yanıt gönder</span><span class="sxs-lookup"><span data-stu-id="b2d24-500">Send response from callback function</span></span>

<span data-ttu-id="b2d24-501">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-501">**Prototype**</span></span>

```c
UINT nx_http_server_callback_response_send(NX_HTTP_SERVER *server_ptr,
     CHAR *header, CHAR *information, CHAR additional_info);
```

<span data-ttu-id="b2d24-502">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-502">**Description**</span></span>

<span data-ttu-id="b2d24-503">Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-503">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="b2d24-504">Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-504">This is typically used to send custom responses associated with GET/POST requests.</span></span> <span data-ttu-id="b2d24-505">Bu işlev kullanıldığında, geri çağırma yordamının NX_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-505">Note that if this function is used, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="b2d24-506">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-506">This service is deprecated.</span></span> <span data-ttu-id="b2d24-507">Geliştiricilerin *nx_http_server_callback_response_send_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-507">Developers are encouraged to migrate to *nx_http_server_callback_response_send_extended().*</span></span>

<span data-ttu-id="b2d24-508">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-508">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-509">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-509">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="b2d24-510">**üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-510">**header** Pointer to the response header string.</span></span>
- <span data-ttu-id="b2d24-511">**bilgi** Bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-511">**information** Pointer to the information string.</span></span>
- <span data-ttu-id="b2d24-512">**additional_info** Ek bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-512">**additional_info** Pointer to the additional information string.</span></span>

<span data-ttu-id="b2d24-513">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-513">**Return Values**</span></span>

- <span data-ttu-id="b2d24-514">**NX_SUCCESS** (0x00) http sunucusu yanıtı başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="b2d24-514">**NX_SUCCESS** (0x00) Successfully sent HTTP Server response</span></span>

<span data-ttu-id="b2d24-515">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-515">**Allowed From**</span></span>

<span data-ttu-id="b2d24-516">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-516">Threads</span></span>

<span data-ttu-id="b2d24-517">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-517">**Example**</span></span>

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
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

## <a name="nx_http_server_callback_response_send_extended"></a><span data-ttu-id="b2d24-518">nx_http_server_callback_response_send_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-518">nx_http_server_callback_response_send_extended</span></span>

### <a name="send-response-from-callback-function"></a><span data-ttu-id="b2d24-519">Geri çağırma işlevinden yanıt gönder</span><span class="sxs-lookup"><span data-stu-id="b2d24-519">Send response from callback function</span></span>

<span data-ttu-id="b2d24-520">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-520">**Prototype**</span></span>

```c
UINT nx_http_server_callback_response_send_extended(
     NX_HTTP_SERVER *server_ptr, CHAR *heade
     UINT header_length, CHAR *information,
     UINT information_length, CHAR *additional_info,
     UINT additional_info_length);
```

<span data-ttu-id="b2d24-521">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-521">**Description**</span></span>

<span data-ttu-id="b2d24-522">Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-522">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="b2d24-523">Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-523">This is typically used to send custom responses associated with GET/POST requests.</span></span> <span data-ttu-id="b2d24-524">Bu işlev kullanıldığında, geri çağırma yordamının NX_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-524">Note that if this function is used, the callback routine must return the status of NX_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="b2d24-525">Bu hizmet *nx_http_server_callback_response_send ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-525">This service replaces *nx_http_server_callback_response_send().*</span></span> <span data-ttu-id="b2d24-526">Bu sürüm, uzunluk bilgilerini giriş bağımsız değişkeni olarak alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-526">This version takes length information as input argument.</span></span>

<span data-ttu-id="b2d24-527">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-527">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-528">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-528">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="b2d24-529">**üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-529">**header** Pointer to the response header string.</span></span>
- <span data-ttu-id="b2d24-530">**header_length** Yanıt üst bilgisi dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-530">**header_length** Length of the response header string.</span></span>
- <span data-ttu-id="b2d24-531">**bilgi** Bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-531">**information** Pointer to the information string.</span></span>
- <span data-ttu-id="b2d24-532">**information_length** Bilgi dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-532">**information_length** Length of the information string.</span></span>
- <span data-ttu-id="b2d24-533">**additional_info** Ek bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-533">**additional_info** Pointer to the additional information string.</span></span>
- <span data-ttu-id="b2d24-534">**additional_info_length** Ek bilgi dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-534">**additional_info_length** Length of the additional information string.</span></span>

<span data-ttu-id="b2d24-535">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-535">**Return Values**</span></span>

- <span data-ttu-id="b2d24-536">**NX_SUCCESS** (0x00) sunucu yanıtı başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="b2d24-536">**NX_SUCCESS** (0x00) Successfully sent Server response</span></span>

<span data-ttu-id="b2d24-537">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-537">**Allowed From**</span></span>

<span data-ttu-id="b2d24-538">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-538">Threads</span></span>

<span data-ttu-id="b2d24-539">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-539">**Example**</span></span>

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
       if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
          (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
           a resource not found response. */
           nx_http_server_callback_response_send_extended(server_ptr,
                                                         "HTTP/1.0 404 ", 12,
                                                         "NetX HTTP Server unable to find
                                                         file: ", 38, resource, 9);
        /* Return completion status. */
           return(NX_HTTP_CALLBACK_COMPLETED);
    }
    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_content_get"></a><span data-ttu-id="b2d24-540">nx_http_server_content_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-540">nx_http_server_content_get</span></span>

### <a name="get-content-from-the-request"></a><span data-ttu-id="b2d24-541">İstekten içerik al</span><span class="sxs-lookup"><span data-stu-id="b2d24-541">Get content from the request</span></span>

<span data-ttu-id="b2d24-542">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-542">**Prototype**</span></span>

```c
UINT nx_http_server_content_get(NX_HTTP_SERVER *server_ptr,
                                NX_PACKET *packet_ptr,
                                ULONG byte_offset,
                                CHAR *destination_ptr,
                                UINT destination_size,
                                UINT *actual_size);
```

<span data-ttu-id="b2d24-543">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-543">**Description**</span></span>

<span data-ttu-id="b2d24-544">Bu hizmet, POST veya PUT HTTP Client isteğinden belirtilen miktarda içeriği almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-544">This service attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="b2d24-545">Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-545">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="b2d24-546">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-546">This service is deprecated.</span></span> <span data-ttu-id="b2d24-547">Geliştiricilerin nx_http_server_content_get_extended () uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-547">Developers are encouraged to migrate to nx_http_server_content_get_extended().</span></span>

<span data-ttu-id="b2d24-548">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-548">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-549">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-549">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="b2d24-550">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-550">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="b2d24-551">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-551">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="b2d24-552">**byte_offset** İçerik alanına kaydırılacağı bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-552">**byte_offset** Number of bytes to offset into the content area.</span></span>
- <span data-ttu-id="b2d24-553">**destination_ptr** İçerik için hedef alana yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-553">**destination_ptr** Pointer to the destination area for the content.</span></span>
- <span data-ttu-id="b2d24-554">**destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-554">**destination_size** Maximum number of bytes available in the destination area.</span></span>
- <span data-ttu-id="b2d24-555">**actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-555">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

<span data-ttu-id="b2d24-556">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-556">**Return Values**</span></span>

- <span data-ttu-id="b2d24-557">**NX_SUCCESS** (0x00) başarılı http sunucusu içerik al</span><span class="sxs-lookup"><span data-stu-id="b2d24-557">**NX_SUCCESS** (0x00) Successful HTTP Server content get</span></span>
- <span data-ttu-id="b2d24-558">**NX_HTTP_ERROR** (0xE0) http sunucusu iç hatası</span><span class="sxs-lookup"><span data-stu-id="b2d24-558">**NX_HTTP_ERROR** (0xE0) HTTP Server internal error</span></span>
- <span data-ttu-id="b2d24-559">**NX_HTTP_DATA_END** (0xE7) Istek içeriğinin sonu</span><span class="sxs-lookup"><span data-stu-id="b2d24-559">**NX_HTTP_DATA_END** (0xE7) End of request content</span></span>
- <span data-ttu-id="b2d24-560">**NX_HTTP_TIMEOUT** (0XE1) sonraki içerik paketini alma sırasında http sunucusu zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="b2d24-560">**NX_HTTP_TIMEOUT** (0xE1) HTTP Server timeout in getting next packet of content</span></span>
- <span data-ttu-id="b2d24-561">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-561">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-562">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-562">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-563">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-563">**Allowed From**</span></span>

<span data-ttu-id="b2d24-564">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-564">Threads</span></span>

<span data-ttu-id="b2d24-565">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-565">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, retrieve up to 100 bytes of content starting at offset 0. */
status = nx_http_server_content_get(&my_server, packet_ptr,
                                   0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
request content. */
```

## <a name="nx_http_server_content_get_extended"></a><span data-ttu-id="b2d24-566">nx_http_server_content_get_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-566">nx_http_server_content_get_extended</span></span>

### <a name="get-content-from-the-requestsupports-zero-length-content-length"></a><span data-ttu-id="b2d24-567">İstekten içerik al/sıfır uzunlukta Içerik uzunluğunu destekler</span><span class="sxs-lookup"><span data-stu-id="b2d24-567">Get content from the request/supports zero length Content Length</span></span>

<span data-ttu-id="b2d24-568">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-568">**Prototype**</span></span>

```c
UINT nx_http_server_content_get_extended(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET *packet_ptr,
                                        ULONG byte_offset,
                                        CHAR *destination_ptr,
                                        UINT destination_size,
                                        UINT *actual_size);
```

<span data-ttu-id="b2d24-569">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-569">**Description**</span></span>

<span data-ttu-id="b2d24-570">Bu hizmet *nx_http_server_content_get ()* ile neredeyse aynıdır; POST veya PUT HTTP Client isteğinden belirtilen miktarda içeriği almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-570">This service is almost identical to *nx_http_server_content_get()*; it attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="b2d24-571">Ancak, geçerli bir istek olarak sıfır değeri (' boş istek ') Içerik uzunluğundaki istekleri işler.</span><span class="sxs-lookup"><span data-stu-id="b2d24-571">However it handles requests with Content Length of zero value (‘empty request’) as a valid request.</span></span> <span data-ttu-id="b2d24-572">Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-572">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="b2d24-573">Bu hizmet *nx_http_server_content_get ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-573">This service replaces *nx_http_server_content_get().*</span></span> <span data-ttu-id="b2d24-574">Bu sürüm, çağıranın ek uzunluk bilgileri sağlaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-574">This version requires caller to supply additional length information.</span></span>

<span data-ttu-id="b2d24-575">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-575">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-576">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-576">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="b2d24-577">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-577">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="b2d24-578">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-578">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="b2d24-579">**byte_offset** İçerik alanına kaydırılacağı bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-579">**byte_offset** Number of bytes to offset into the content area.</span></span>
- <span data-ttu-id="b2d24-580">**destination_ptr** İçerik için hedef alana yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-580">**destination_ptr** Pointer to the destination area for the content.</span></span>
- <span data-ttu-id="b2d24-581">**destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="b2d24-581">**destination_size** Maximum number of bytes available in the destination area.</span></span>
- <span data-ttu-id="b2d24-582">**actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-582">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

<span data-ttu-id="b2d24-583">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-583">**Return Values**</span></span>

- <span data-ttu-id="b2d24-584">**NX_SUCCESS** (0x00) başarılı http içerik al</span><span class="sxs-lookup"><span data-stu-id="b2d24-584">**NX_SUCCESS** (0x00) Successful HTTP content get</span></span>
- <span data-ttu-id="b2d24-585">**NX_HTTP_ERROR** (0xE0) http sunucusu iç hatası</span><span class="sxs-lookup"><span data-stu-id="b2d24-585">**NX_HTTP_ERROR** (0xE0) HTTP Server internal error</span></span>
- <span data-ttu-id="b2d24-586">**NX_HTTP_DATA_END** (0xE7) Istek içeriğinin sonu</span><span class="sxs-lookup"><span data-stu-id="b2d24-586">**NX_HTTP_DATA_END** (0xE7) End of request content</span></span>
- <span data-ttu-id="b2d24-587">**NX_HTTP_TIMEOUT** (0XE1) sonraki paketi alma sırasında http sunucusu zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="b2d24-587">**NX_HTTP_TIMEOUT** (0xE1) HTTP Server timeout in getting next packet</span></span>
- <span data-ttu-id="b2d24-588">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-588">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-589">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-589">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-590">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-590">**Allowed From**</span></span>

<span data-ttu-id="b2d24-591">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-591">Threads</span></span>

<span data-ttu-id="b2d24-592">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-592">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, retrieve up to 100 bytes of content starting at offset 0. */
status = nx_http_server_content_get_extended(&my_server, packet_ptr,
                                            0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
request content. */
```

## <a name="nx_http_server_content_length_get"></a><span data-ttu-id="b2d24-593">nx_http_server_content_length_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-593">nx_http_server_content_length_get</span></span>

### <a name="get-length-of-content-in-the-request"></a><span data-ttu-id="b2d24-594">İstekteki içerik uzunluğunu al</span><span class="sxs-lookup"><span data-stu-id="b2d24-594">Get length of content in the request</span></span>

<span data-ttu-id="b2d24-595">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-595">**Prototype**</span></span>

```c
UINT nx_http_server_content_length_get(NX_PACKET *packet_ptr);
```
<span data-ttu-id="b2d24-596">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-596">**Description**</span></span>

<span data-ttu-id="b2d24-597">Bu hizmet, sağlanan paketteki HTTP içerik uzunluğunu almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-597">This service attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="b2d24-598">HTTP içeriği yoksa, bu yordam sıfır değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="b2d24-598">If there is no HTTP content, this routine returns a value of zero.</span></span> <span data-ttu-id="b2d24-599">Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-599">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="b2d24-600">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-600">This service is deprecated.</span></span> <span data-ttu-id="b2d24-601">Geliştiricilerin nx_http_server_content_length_get_extended () uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-601">Developers are encouraged to migrate to nx_http_server_content_length_get_extended().</span></span>

<span data-ttu-id="b2d24-602">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-602">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-603">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-603">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="b2d24-604">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-604">Note that this packet must not be released by the request notify callback.</span></span>

<span data-ttu-id="b2d24-605">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-605">**Return Values**</span></span>

- <span data-ttu-id="b2d24-606">**içerik uzunluğu** Hatada, sıfır değeri döndürülür</span><span class="sxs-lookup"><span data-stu-id="b2d24-606">**content length** On error, a value of zero is returned</span></span>

<span data-ttu-id="b2d24-607">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-607">**Allowed From**</span></span>

<span data-ttu-id="b2d24-608">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-608">Threads</span></span>

<span data-ttu-id="b2d24-609">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-609">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, get the content length of the HTTP Client request. */
length = nx_http_server_content_length_get(packet_ptr);

/* The “length” variable now contains the length of the HTTP Client
request content area. */
```

## <a name="nx_http_server_content_length_get_extended"></a><span data-ttu-id="b2d24-610">nx_http_server_content_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-610">nx_http_server_content_length_get_extended</span></span>

### <a name="get-length-of-content-in-the-requestsupports-content-length-of-zero-value"></a><span data-ttu-id="b2d24-611">İstekteki içerik uzunluğunu al/sıfır değerinin Içerik uzunluğunu destekler</span><span class="sxs-lookup"><span data-stu-id="b2d24-611">Get length of content in the request/supports Content Length of zero value</span></span>

<span data-ttu-id="b2d24-612">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-612">**Prototype**</span></span>

```c
UINT nx_http_server_content_length_get_extended(NX_PACKET *packet_ptr,
                                               UINT *content_length);
```

<span data-ttu-id="b2d24-613">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-613">**Description**</span></span>

<span data-ttu-id="b2d24-614">Bu hizmet *nx_http_server_content_length_get ()* ile benzerdir; sağlanan pakette HTTP içerik uzunluğunu almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-614">This service is similar to *nx_http_server_content_length_get()*; attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="b2d24-615">Ancak, dönüş değeri başarıyla tamamlanma durumunu gösterir ve content_length giriş İşaretçisinde gerçek uzunluk değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b2d24-615">However, the return value indicates successful completion status, and the actual length value is returned in the input pointer content_length.</span></span> <span data-ttu-id="b2d24-616">HTTP içeriği/Içerik uzunluğu = 0 yoksa, bu yordam yine de başarılı bir tamamlanma durumu döndürür ve content_length giriş işaretçisi geçerli bir uzunluğa (sıfır) işaret eder.</span><span class="sxs-lookup"><span data-stu-id="b2d24-616">If there is no HTTP content/Content Length = 0, this routine still returns a successful completion status and the content_length input pointer points to a valid length (zero).</span></span> <span data-ttu-id="b2d24-617">Bu, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-617">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="b2d24-618">Bu hizmet *nx_http_server_content_length_get*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-618">This service replaces *nx_http_server_content_length_get*().</span></span>

<span data-ttu-id="b2d24-619">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-619">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-620">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-620">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="b2d24-621">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-621">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="b2d24-622">**CONTENT_LENGTH** Içerik uzunluğu alanından alınan değer işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-622">**content_length** Pointer to value retrieved from Content Length field</span></span>

<span data-ttu-id="b2d24-623">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-623">**Return Values**</span></span>

- <span data-ttu-id="b2d24-624">**NX_SUCCESS** (0x00) başarılı http sunucusu içerik al</span><span class="sxs-lookup"><span data-stu-id="b2d24-624">**NX_SUCCESS** (0x00) Successful HTTP Server content get</span></span>
- <span data-ttu-id="b2d24-625">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) yanlış http üst bilgi biçimi</span><span class="sxs-lookup"><span data-stu-id="b2d24-625">**NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Improper HTTP header format</span></span>
- <span data-ttu-id="b2d24-626">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-626">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-627">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-627">**Allowed From**</span></span>

<span data-ttu-id="b2d24-628">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-628">Threads</span></span>

<span data-ttu-id="b2d24-629">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-629">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, get the content length of the HTTP Client request. */
ULONG content_length;

status = nx_http_server_content_length_get_extended(packet_ptr, &content_length);

/* If the “status” variable indicates successful completion, the“length” variable
contains the length of the HTTP Client request content area. */
```

## <a name="nx_http_server_create"></a><span data-ttu-id="b2d24-630">nx_http_server_create</span><span class="sxs-lookup"><span data-stu-id="b2d24-630">nx_http_server_create</span></span>

### <a name="create-an-http-server-instance"></a><span data-ttu-id="b2d24-631">HTTP sunucusu örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2d24-631">Create an HTTP Server instance</span></span>

<span data-ttu-id="b2d24-632">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-632">**Prototype**</span></span>

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

<span data-ttu-id="b2d24-633">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-633">**Description**</span></span>

<span data-ttu-id="b2d24-634">Bu hizmet kendi ThreadX iş parçacığı bağlamında çalışan bir HTTP sunucu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-634">This service creates an HTTP Server instance, which runs in the context of its own ThreadX thread.</span></span> <span data-ttu-id="b2d24-635">İsteğe bağlı *authentication_check* ve *request_notify* uygulama GERI çağırma yordamları, HTTP sunucusunun temel işlemleri üzerinde uygulama yazılım denetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-635">The optional *authentication_check* and *request_notify* application callback routines give the application software control over the basic operations of the HTTP Server.</span></span>

<span data-ttu-id="b2d24-636">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-636">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-637">**http_server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-637">**http_server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="b2d24-638">**http_server_name** HTTP sunucusu adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-638">**http_server_name** Pointer to HTTP Server’s name.</span></span>
- <span data-ttu-id="b2d24-639">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-639">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="b2d24-640">**media_ptr** Daha önce oluşturulan FileX medya örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-640">**media_ptr** Pointer to previously created FileX media instance.</span></span>
- <span data-ttu-id="b2d24-641">**stack_ptr** HTTP sunucusu iş parçacığı yığın alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-641">**stack_ptr** Pointer to HTTP Server thread stack area.</span></span>
- <span data-ttu-id="b2d24-642">**stack_size** HTTP sunucusu iş parçacığı yığın boyutu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-642">**stack_size** Pointer to HTTP Server thread stack size.</span></span>
- <span data-ttu-id="b2d24-643">**authentication_check** Uygulamanın kimlik doğrulama denetimi yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-643">**authentication_check** Function pointer to application’s authentication checking routine.</span></span> <span data-ttu-id="b2d24-644">Belirtilmişse, bu yordam her HTTP Istemci isteği için çağırılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-644">If specified, this routine is called for each HTTP Client request.</span></span> <span data-ttu-id="b2d24-645">Bu parametre NULL ise kimlik doğrulaması gerçekleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="b2d24-645">If this parameter is NULL no authentication will be performed.</span></span>
- <span data-ttu-id="b2d24-646">**request_notify** Uygulamanın istek bildirim yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-646">**request_notify** Function pointer to application’s request notify routine.</span></span> <span data-ttu-id="b2d24-647">Belirtilmişse, bu yordam isteğin HTTP sunucu işlemeden önce çağırılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-647">If specified, this routine is called prior to the HTTP server processing of the request.</span></span> <span data-ttu-id="b2d24-648">Bu, HTTP Istemci isteği tamamlanmadan önce kaynak adının yeniden yönlendirilmesine veya bir kaynak içindeki alanların güncelleştirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-648">This allows the resource name to be redirected or fields within a resource to be updated prior to completing the HTTP Client request.</span></span>

<span data-ttu-id="b2d24-649">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-649">**Return Values**</span></span>

- <span data-ttu-id="b2d24-650">**NX_SUCCESS** (0x00) başarılı http sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="b2d24-650">**NX_SUCCESS** (0x00) Successful HTTP Server create.</span></span>
- <span data-ttu-id="b2d24-651">NX_PTR_ERROR (0x07) geçersiz HTTP sunucusu, IP, medya, yığın veya paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-651">NX_PTR_ERROR (0x07) Invalid HTTP Server, IP, media, stack, or packet pool pointer.</span></span>
- <span data-ttu-id="b2d24-652">NX_HTTP_POOL_ERROR (0xE9) havuzun paket yükü, tüm HTTP isteklerini içerecek kadar büyük değil.</span><span class="sxs-lookup"><span data-stu-id="b2d24-652">NX_HTTP_POOL_ERROR (0xE9) Packet payload of pool is not large enough to contain complete HTTP request.</span></span>

<span data-ttu-id="b2d24-653">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-653">**Allowed From**</span></span>

<span data-ttu-id="b2d24-654">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-654">Initialization, Threads</span></span>

<span data-ttu-id="b2d24-655">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-655">**Example**</span></span>

```c
/* Create an HTTP Server instance called “my_server.” */
status = nx_http_server_create(&my_server, “my server”, &ip_0, &ram_disk,
                              stack_ptr, stack_size, &pool_0,
                              my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_http_server_delete"></a><span data-ttu-id="b2d24-656">nx_http_server_delete</span><span class="sxs-lookup"><span data-stu-id="b2d24-656">nx_http_server_delete</span></span>

### <a name="delete-an-http-server-instance"></a><span data-ttu-id="b2d24-657">HTTP sunucusu örneğini silme</span><span class="sxs-lookup"><span data-stu-id="b2d24-657">Delete an HTTP Server instance</span></span>

<span data-ttu-id="b2d24-658">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-658">**Prototype**</span></span>

```c
UINT nx_http_server_delete(NX_HTTP_SERVER *http_server_ptr);
```

<span data-ttu-id="b2d24-659">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-659">**Description**</span></span>

<span data-ttu-id="b2d24-660">Bu hizmet, önceden oluşturulmuş bir HTTP sunucusu örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="b2d24-660">This service deletes a previously created HTTP Server instance.</span></span>

<span data-ttu-id="b2d24-661">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-661">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-662">**http_server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-662">**http_server_ptr** Pointer to HTTP Server control block.</span></span>

<span data-ttu-id="b2d24-663">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-663">**Return Values**</span></span>

- <span data-ttu-id="b2d24-664">**NX_SUCCESS** (0x00) başarılı http sunucusu silme</span><span class="sxs-lookup"><span data-stu-id="b2d24-664">**NX_SUCCESS** (0x00) Successful HTTP Server delete</span></span>
- <span data-ttu-id="b2d24-665">NX_PTR_ERROR (0x07) geçersiz HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-665">NX_PTR_ERROR (0x07) Invalid HTTP Server pointer</span></span>
- <span data-ttu-id="b2d24-666">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-666">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-667">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-667">**Allowed From**</span></span>

<span data-ttu-id="b2d24-668">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-668">Threads</span></span>

<span data-ttu-id="b2d24-669">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-669">**Example**</span></span>

```c
/* Delete the HTTP Server instance called “my_server.” */
status = nx_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_http_server_get_entity_content"></a><span data-ttu-id="b2d24-670">nx_http_server_get_entity_content</span><span class="sxs-lookup"><span data-stu-id="b2d24-670">nx_http_server_get_entity_content</span></span>

### <a name="retrieve-the-location-and-length-of-entity-data"></a><span data-ttu-id="b2d24-671">Varlık verilerinin konumunu ve uzunluğunu alma</span><span class="sxs-lookup"><span data-stu-id="b2d24-671">Retrieve the location and length of entity data</span></span>

<span data-ttu-id="b2d24-672">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-672">**Prototype**</span></span>

```c
UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      ULONG *available_offset,
                                      ULONG *available_length);
```

<span data-ttu-id="b2d24-673">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-673">**Description**</span></span>

<span data-ttu-id="b2d24-674">Bu hizmet, alınan Istemci iletilerindeki geçerli çok parçalı varlıktaki verilerin başlangıç konumunu ve sınır dizesini dahil olmayan veri uzunluğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="b2d24-674">This service determines the location of the start of data within the current multipart entity in the received Client messages, and the length of data not including the boundary string.</span></span> <span data-ttu-id="b2d24-675">Dahili HTTP sunucusu, bu işlevin birden çok varlığa sahip iletiler için aynı Istemci veri biriminde yeniden çağrılabilmesi için kendi uzaklıklarını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-675">Internally HTTP server updates its own offsets so that this function can be called again on the same Client datagram for messages with multiple entities.</span></span> <span data-ttu-id="b2d24-676">Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-676">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

<span data-ttu-id="b2d24-677">Bu hizmeti kullanmak için NX_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-677">Note that NX_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span>

<span data-ttu-id="b2d24-678">Daha fazla bilgi için bkz. *nx_http_server_get_entity_header* .</span><span class="sxs-lookup"><span data-stu-id="b2d24-678">See *nx_http_server_get_entity_header* for more details.</span></span>

<span data-ttu-id="b2d24-679">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-679">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-680">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-680">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="b2d24-681">**packet_pptr** Paket işaretçisinin konumu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-681">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="b2d24-682">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-682">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="b2d24-683">**available_offset** Paket önüne işaretçisinden varlık verilerinin uzaklığa yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-683">**available_offset** Pointer to offset of entity data from the packet prepend pointer</span></span>
- <span data-ttu-id="b2d24-684">**available_length** Varlık verisi uzunluğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-684">**available_length** Pointer to length of entity data</span></span>

<span data-ttu-id="b2d24-685">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-685">**Return Values**</span></span>

- <span data-ttu-id="b2d24-686">**NX_SUCCESS** (0x00) varlık içeriğinin boyutunu ve konumunu başarıyla aldı</span><span class="sxs-lookup"><span data-stu-id="b2d24-686">**NX_SUCCESS** (0x00) Successfully retrieved size and location of entity content</span></span>
- <span data-ttu-id="b2d24-687">HTTP sunucusu iç çok parçalı işaretçiler için **NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xf4) içeriği zaten var</span><span class="sxs-lookup"><span data-stu-id="b2d24-687">**NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) Content for the HTTP server internal multipart markers is already found</span></span>
- <span data-ttu-id="b2d24-688">NX_HTTP_ERROR (0xE0) HTTP sunucusu iç hatası</span><span class="sxs-lookup"><span data-stu-id="b2d24-688">NX_HTTP_ERROR (0xE0) HTTP Server internal error</span></span>
- <span data-ttu-id="b2d24-689">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-689">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-690">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-690">**Allowed From**</span></span>

<span data-ttu-id="b2d24-691">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-691">Threads</span></span>

<span data-ttu-id="b2d24-692">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-692">**Example**</span></span>

```c
NX_HTTP_SERVER my_server;

UINT         offset, length;
NX_PACKET    *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
the entity header to determine details about the multipart data. If
successful, it then calls this service to get the location of entity data: */
status = nx_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
                                          &length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
entity data. */
```

## <a name="nx_http_server_get_entity_header"></a><span data-ttu-id="b2d24-693">nx_http_server_get_entity_header</span><span class="sxs-lookup"><span data-stu-id="b2d24-693">nx_http_server_get_entity_header</span></span>

### <a name="retrieve-the-contents-of-entity-header"></a><span data-ttu-id="b2d24-694">Varlık üstbilgisinin içeriğini alma</span><span class="sxs-lookup"><span data-stu-id="b2d24-694">Retrieve the contents of entity header</span></span>

<span data-ttu-id="b2d24-695">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-695">**Prototype**</span></span>

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                     NX_PACKET **packet_pptr,
                                     UCHAR *entity_header_buffer,
                                     ULONG buffer_size);
```

<span data-ttu-id="b2d24-696">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-696">**Description**</span></span>

<span data-ttu-id="b2d24-697">Bu hizmet varlık üstbilgisini belirtilen arabelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-697">This service retrieves the entity header into the specified buffer.</span></span> <span data-ttu-id="b2d24-698">Dahili HTTP sunucusu, birden çok varlık üst bilgilerine sahip bir Istemci veri biriminde bir sonraki çok parçalı varlığı bulmak için kendi işaretçilerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-698">Internally HTTP Server updates its own pointers to locate the next multipart entity in a Client datagram with multiple entity headers.</span></span> <span data-ttu-id="b2d24-699">Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-699">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

<span data-ttu-id="b2d24-700">Bu hizmeti kullanmak için NX_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-700">Note that NX_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span>

<span data-ttu-id="b2d24-701">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-701">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-702">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-702">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="b2d24-703">**packet_pptr** Paket işaretçisinin konumu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-703">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="b2d24-704">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-704">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="b2d24-705">**entity_header_buffer** Varlık üstbilgisinin depolanacak konuma işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-705">**entity_header_buffer** Pointer to location to store entity header</span></span>
- <span data-ttu-id="b2d24-706">**Buffer_size** Giriş arabelleğinin boyutu</span><span class="sxs-lookup"><span data-stu-id="b2d24-706">**buffer_size** Size of input buffer</span></span>

<span data-ttu-id="b2d24-707">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-707">**Return Values**</span></span>

- <span data-ttu-id="b2d24-708">**NX_SUCCESS** (0x00) varlık Heade başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="b2d24-708">**NX_SUCCESS** (0x00) Successfully retrieved entity heade</span></span>
- <span data-ttu-id="b2d24-709">**NX_HTTP_NOT_FOUND (0xE6)** Varlık üst bilgisi alanı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="b2d24-709">**NX_HTTP_NOT_FOUND (0xE6)** Entity header field not found</span></span>
- <span data-ttu-id="b2d24-710">**NX_HTTP_TIMEOUT (0xE1)** Çok paket istemci iletisi için sonraki paketin alınacağı sürenin süresi geçildi</span><span class="sxs-lookup"><span data-stu-id="b2d24-710">**NX_HTTP_TIMEOUT (0xE1)** Time expired to receive next packet for multipacket client message</span></span> 
- <span data-ttu-id="b2d24-711">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-711">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-712">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-712">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="b2d24-713">NX_HTTP_ERROR (0xE0) Iç HTTP hatası</span><span class="sxs-lookup"><span data-stu-id="b2d24-713">NX_HTTP_ERROR (0xE0) Internal HTTP error</span></span>

<span data-ttu-id="b2d24-714">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-714">**Allowed From**</span></span>

<span data-ttu-id="b2d24-715">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-715">Threads</span></span>

<span data-ttu-id="b2d24-716">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-716">**Example**</span></span>

```c
/* my_request_notify* is the application request notify callback registered with
the HTTP server in *nx_http_server_create,* creates a response to the received
Client request. */

UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

NX_PACKET     *sresp_packet_ptr;
UINT          offset, length;**
NX_PACKET     *response_pkt;
UCHAR         buffer[1440];

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
             "Server: NetX HTTP 5.3\r\n");

    if(status == NX_SUCCESS)
    {
        if(nx_http_server_callback_packet_send(server_ptr, response_pkt) !=
                                              NX_SUCCESS)
        {
            nx_packet_release(response_pkt);
        }
    }
}
Else
{

        /* Indicate we have not processed the response to client yet.*/        
        return(NX_SUCCESS);
}

/* Indicate the response to client is transmitted. */
return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_gmt_callback_set"></a><span data-ttu-id="b2d24-717">nx_http_server_gmt_callback_set</span><span class="sxs-lookup"><span data-stu-id="b2d24-717">nx_http_server_gmt_callback_set</span></span>

### <a name="set-the-callback-to-obtain-gmt-date-and-time"></a><span data-ttu-id="b2d24-718">GMT Tarih ve saati almak için geri aramayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b2d24-718">Set the callback to obtain GMT date and time</span></span>

<span data-ttu-id="b2d24-719">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-719">**Prototype**</span></span>

```c
UINT nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                                    VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

<span data-ttu-id="b2d24-720">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-720">**Description**</span></span>

<span data-ttu-id="b2d24-721">Bu hizmet, daha önce oluşturulmuş bir HTTP sunucusu ile GMT Tarih ve saati alacak şekilde geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-721">This service sets the callback to obtain GMT date and time with a previously created HTTP server.</span></span> <span data-ttu-id="b2d24-722">Bu hizmet HTTP sunucusu, Istemciye HTTP sunucu yanıtlarında bir üst bilgi oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="b2d24-722">This service is invoked with the HTTP server is creating a header in HTTP server responses to the Client.</span></span>

<span data-ttu-id="b2d24-723">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-723">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-724">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-724">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="b2d24-725">**gmt_get** GMT geri çağırması işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-725">**gmt_get** Pointer to GMT callback</span></span>
- <span data-ttu-id="b2d24-726">**Tarih** Alınan tarihin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-726">**date** Pointer to the date retrieved</span></span>

<span data-ttu-id="b2d24-727">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-727">**Return Values**</span></span>

- <span data-ttu-id="b2d24-728">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="b2d24-728">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="b2d24-729">NX_PTR_ERROR (0x07) geçersiz paket veya parametre işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-729">NX_PTR_ERROR (0x07) Invalid packet or parameter pointer.</span></span>

<span data-ttu-id="b2d24-730">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-730">**Allowed From**</span></span>

<span data-ttu-id="b2d24-731">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-731">Threads</span></span>

<span data-ttu-id="b2d24-732">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-732">**Example**</span></span>

```c
NX_HTTP_SERVER my_server;

VOID get_gmt(NX_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_http_server_create, and before
starting HTTP services when nx_http_server_start is called, set the GMT
retrieve callback: */

status = nx_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
response header date. */
```

## <a name="nx_http_server_invalid_userpassword_notify_set"></a><span data-ttu-id="b2d24-733">nx_http_server_invalid_userpassword_notify_set</span><span class="sxs-lookup"><span data-stu-id="b2d24-733">nx_http_server_invalid_userpassword_notify_set</span></span>

### <a name="set-the-callback-to-to-handle-invalid-userpassword"></a><span data-ttu-id="b2d24-734">Geri çağırma işlemini geçersiz kullanıcı/parola işleyecek şekilde ayarla</span><span class="sxs-lookup"><span data-stu-id="b2d24-734">Set the callback to to handle invalid user/password</span></span>

<span data-ttu-id="b2d24-735">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-735">**Prototype**</span></span>

```c
UINT nx_http_server_invalid_userpassword_notify_set(
     NX_HTTP_SERVER *http_server_ptr,
     UINT (*invalid_username_password_callback)
     (CHAR *resource,
     ULONG client_address,
     UINT request_type));
```

<span data-ttu-id="b2d24-736">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-736">**Description**</span></span>

<span data-ttu-id="b2d24-737">Bu hizmet, bir Istemci alma, yerleştirme veya silme isteğinde, Özet veya temel kimlik doğrulamasından göre geçersiz bir Kullanıcı adı ve parola alındığında çağrılan geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-737">This service sets the callback invoked when an invalid username and password is received in a Client get, put or delete request, either by digest or basic authentication.</span></span> <span data-ttu-id="b2d24-738">HTTP sunucusu daha önce oluşturulmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-738">The HTTP server must be previously created.</span></span>

<span data-ttu-id="b2d24-739">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-739">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-740">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-740">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="b2d24-741">**invalid_username_password_callback** Geçersiz Kullanıcı/geçiş geri çağırması işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-741">**invalid_username_password_callback** Pointer to invalid user/pass callback</span></span>
- <span data-ttu-id="b2d24-742">**kaynak** İstemci tarafından belirtilen kaynak işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-742">**resource** Pointer to the resource specified by the client</span></span>
- <span data-ttu-id="b2d24-743">**client_address** İstemci adresi</span><span class="sxs-lookup"><span data-stu-id="b2d24-743">**client_address** Client address</span></span>
- <span data-ttu-id="b2d24-744">**request_type** İstemci isteği türünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-744">**request_type** Indicates client request type.</span></span> <span data-ttu-id="b2d24-745">Belki:</span><span class="sxs-lookup"><span data-stu-id="b2d24-745">May be:</span></span>
  - <span data-ttu-id="b2d24-746">NX_HTTP_SERVER_GET_REQUEST</span><span class="sxs-lookup"><span data-stu-id="b2d24-746">NX_HTTP_SERVER_GET_REQUEST</span></span>
  - <span data-ttu-id="b2d24-747">NX_HTTP_SERVER_POST_REQUEST NX_HTTP_SERVER_HEAD_REQUEST</span><span class="sxs-lookup"><span data-stu-id="b2d24-747">NX_HTTP_SERVER_POST_REQUEST NX_HTTP_SERVER_HEAD_REQUEST</span></span>
  - <span data-ttu-id="b2d24-748">NX_HTTP_SERVER_PUT_REQUEST NX_HTTP_SERVER_DELETE_REQUEST</span><span class="sxs-lookup"><span data-stu-id="b2d24-748">NX_HTTP_SERVER_PUT_REQUEST NX_HTTP_SERVER_DELETE_REQUEST</span></span>

<span data-ttu-id="b2d24-749">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-749">**Return Values**</span></span>

- <span data-ttu-id="b2d24-750">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="b2d24-750">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="b2d24-751">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-751">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-752">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-752">**Allowed From**</span></span>

<span data-ttu-id="b2d24-753">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-753">Threads</span></span>

<span data-ttu-id="b2d24-754">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-754">**Example**</span></span>

```c
NX_HTTP_SERVER my_server;
VOID invalid_username_password_callback (NX_ CHAR *resource,
                                        ULONG client_address,
                                        UINT request_type);

/* After the HTTP server is created by calling nx_http_server_create, and before
starting HTTP services when nx_http_server_start is called, set the invalid
username password callback: */

status = nx_http_server_gmt_callback_set(&my_server,
                                        invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_http_server_mime_maps_additional_set"></a><span data-ttu-id="b2d24-755">nx_http_server_mime_maps_additional_set</span><span class="sxs-lookup"><span data-stu-id="b2d24-755">nx_http_server_mime_maps_additional_set</span></span>

### <a name="set-additional-mime-maps-for-html"></a><span data-ttu-id="b2d24-756">HTML için ek MIME haritaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="b2d24-756">Set additional MIME maps for HTML</span></span> 

<span data-ttu-id="b2d24-757">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-757">**Prototype**</span></span>

```c
UINT nx_http_server_mime_maps_additional_set(
     NX_HTTP_SERVER *server_ptr,
     NX_HTTP_SERVER_MIME_MAP *mime_maps,
     UINT mime_maps_num);
```

<span data-ttu-id="b2d24-758">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-758">**Description**</span></span>

<span data-ttu-id="b2d24-759">Bu hizmet, HTTP uygulama geliştiricisinin NetX HTTP sunucusu tarafından sağlanan varsayılan MIME türlerinden ek MIME türleri eklemesine izin verir (tanımlı türlerin listesi için bkz. *nx_http_server_get_type* ).</span><span class="sxs-lookup"><span data-stu-id="b2d24-759">This service allows the HTTP application developer to add additional MIME types from the default MIME types supplied by NetX HTTP Server (see *nx_http_server_get_type* for list of defined types).</span></span>

<span data-ttu-id="b2d24-760">Bir istemci isteği alındığında, örneğin, bir GET isteği, http üst bilgisinden istenen dosya türünü, tercihe bağlı olarak ek MIME eşleme kümesini kullanarak ayrıştırır ve bulunursa eşleşme yoksa, HTTP sunucusunun varsayılan MIME eşlemesinde bir eşleşme arar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-760">When a client request is received, e.g. a GET request, HTTP server parses the requested file type from the HTTP header using preferentially the additional MIME map set and if no match if found, it looks for a match in the default MIME map of the HTTP server.</span></span> <span data-ttu-id="b2d24-761">Eşleşme bulunmazsa, MIME türü varsayılan olarak "metin/düz" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-761">If no match is found, the MIME type defaults to “text/plain”.</span></span>

<span data-ttu-id="b2d24-762">İstek bildirimi işlevi HTTP sunucusuna kayıtlıysa, istek bildirimi geri araması dosya türünü ayrıştırmak için *nx_http_server_type_get* çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-762">If the request notify function is registered with the HTTP server, the request notify callback can call *nx_http_server_type_get* to parse the file type.</span></span>

<span data-ttu-id="b2d24-763">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-763">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-764">**server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-764">**server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="b2d24-765">**mime_maps** MIME eşleme dizisine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-765">**mime_maps** Pointer to a MIME map array</span></span>
- <span data-ttu-id="b2d24-766">**mime_map_num** Dizideki MIME haritaları sayısı</span><span class="sxs-lookup"><span data-stu-id="b2d24-766">**mime_map_num** Number of MIME maps in array</span></span>

<span data-ttu-id="b2d24-767">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-767">**Return Values**</span></span>

- <span data-ttu-id="b2d24-768">**NX_SUCCESS** (0x00) başarılı http sunucusu MIME eşleme kümesi</span><span class="sxs-lookup"><span data-stu-id="b2d24-768">**NX_SUCCESS** (0x00) Successful HTTP Server MIME map set</span></span>
- <span data-ttu-id="b2d24-769">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-769">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-770">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-770">**Allowed From**</span></span>

<span data-ttu-id="b2d24-771">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-771">Initialization, Threads</span></span>

<span data-ttu-id="b2d24-772">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-772">**Example**</span></span>

```c
/* my_server is an NX_HTTP_SERVER previously created. */

NX_HTTP_SERVER_MIME_MAP my_mime_maps [2];

static NX_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc", "yourtype/abc"},
    {"xyz", "mytype/xyz"},
};

status = nx_http_server_mime_maps_additional_set(&my_server,
                                                &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP
server MIME map set.” */
```

## <a name="nx_http_server_packet_content_find"></a><span data-ttu-id="b2d24-773">nx_http_server_packet_content_find</span><span class="sxs-lookup"><span data-stu-id="b2d24-773">nx_http_server_packet_content_find</span></span>

### <a name="extract-content-length-and-set-pointer-to-start-of-data"></a><span data-ttu-id="b2d24-774">İçerik uzunluğunu Ayıkla ve veri başına işaretçiyi ayarla</span><span class="sxs-lookup"><span data-stu-id="b2d24-774">Extract content length and set pointer to start of data</span></span>

<span data-ttu-id="b2d24-775">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-775">**Prototype**</span></span>

```c
UINT nx_http_server_packet_content_find(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_ptr,
                                       UINT *content_length);
```

<span data-ttu-id="b2d24-776">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-776">**Description**</span></span>

<span data-ttu-id="b2d24-777">Bu hizmet, HTTP üstbilgisinden içerik uzunluğunu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-777">This service extracts the content length from the HTTP header.</span></span> <span data-ttu-id="b2d24-778">Ayrıca, sağlanan paketi aşağıdaki gibi güncelleştirir: paket önüne işaretçisi (yazılacak paket arabelleğinin konumu), http içeriğine (veri) yalnızca http üst bilgisini geçirilmiş şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-778">It also updates the supplied packet as follows: the packet prepend pointer (start of location of packet buffer to write to) is set to the HTTP content (data) just passed the HTTP header.</span></span>

<span data-ttu-id="b2d24-779">İçeriğin başlangıcı geçerli pakette bulunmazsa, işlev, sonraki paketin NX_HTTP_SERVER_TIMEOUT_RECEIVE bekle seçeneği kullanılarak alınmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="b2d24-779">If the beginning of content is not found in the current packet, the function waits for the next packet to be received using the NX_HTTP_SERVER_TIMEOUT_RECEIVE wait option.</span></span>

<span data-ttu-id="b2d24-780">Bu, *nx_http_server_get_entity_header ()* çağrılmadan önce çağrılmamalıdır; çünkü varlık üstbilgisinin sonundaki önüne işaretçisini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-780">Note this should not be called before calling *nx_http_server_get_entity_header()* because it modifies the prepend pointer past the entity header.</span></span>

<span data-ttu-id="b2d24-781">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-781">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-782">**server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-782">**server_ptr** Pointer to HTTP server instance</span></span>
- <span data-ttu-id="b2d24-783">**packet_ptr** Güncelleştirilmiş önüne işaretçisine sahip paketi döndürmek için paket işaretçisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-783">**packet_ptr** Pointer to packet pointer for returning the packet with updated prepend pointer</span></span>
- <span data-ttu-id="b2d24-784">**CONTENT_LENGTH** Ayıklanan content_length işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-784">**content_length** Pointer to extracted content_length</span></span>

<span data-ttu-id="b2d24-785">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-785">**Return Values**</span></span>

- <span data-ttu-id="b2d24-786">**NX_SUCCESS** (0x00) http içerik uzunluğu bulundu ve paket başarıyla güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="b2d24-786">**NX_SUCCESS** (0x00) HTTP content length found and packet successfully updated</span></span>
- <span data-ttu-id="b2d24-787">**NX_HTTP_TIMEOUT** (0XE1) süre süresi dolduğunda sonraki pakette bekliyor</span><span class="sxs-lookup"><span data-stu-id="b2d24-787">**NX_HTTP_TIMEOUT** (0xE1) Time expired waiting on next packet</span></span>
- <span data-ttu-id="b2d24-788">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-788">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-789">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-789">**Allowed From**</span></span>

<span data-ttu-id="b2d24-790">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-790">Threads</span></span>

<span data-ttu-id="b2d24-791">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-791">**Example**</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
The server has received a Client request packet, recv_packet_ptr, and the packet
content find service is called from the request notify callback function 
registere with the HTTP server. */

UINT content_length;

status = nx_http_server_packet_content_find(server_ptr, recv_packet_ptr,
                                           &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_http_server_packet_get"></a><span data-ttu-id="b2d24-792">nx_http_server_packet_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-792">nx_http_server_packet_get</span></span>

### <a name="receive-the-next-http-packet"></a><span data-ttu-id="b2d24-793">Sonraki HTTP paketini al</span><span class="sxs-lookup"><span data-stu-id="b2d24-793">Receive the next HTTP packet</span></span>

<span data-ttu-id="b2d24-794">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-794">**Prototype**</span></span>

```c
UINT nx_http_server_packet_get(NX_HTTP_SERVER *server_ptr,
                              NX_PACKET **packet_ptr);
```

<span data-ttu-id="b2d24-795">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-795">**Description**</span></span>

<span data-ttu-id="b2d24-796">Bu hizmet, HTTP sunucusu yuvasında alınan bir sonraki paketi döndürür.</span><span class="sxs-lookup"><span data-stu-id="b2d24-796">This service returns the next packet received on the HTTP server socket.</span></span> <span data-ttu-id="b2d24-797">Bir paket almak için bekle seçeneği NX_HTTP_SERVER_TIMEOUT_RECEIVE.</span><span class="sxs-lookup"><span data-stu-id="b2d24-797">The wait option to receive a packet is NX_HTTP_SERVER_TIMEOUT_RECEIVE.</span></span>

<span data-ttu-id="b2d24-798">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-798">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-799">**server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-799">**server_ptr** Pointer to HTTP server instance</span></span>
- <span data-ttu-id="b2d24-800">**packet_ptr** Alınan paket işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-800">**packet_ptr** Pointer to received packet</span></span>

<span data-ttu-id="b2d24-801">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-801">**Return Values**</span></span>

- <span data-ttu-id="b2d24-802">**NX_SUCCESS** (0x00) sonraki http paketi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="b2d24-802">**NX_SUCCESS** (0x00) Successfully received next HTTP packet</span></span>
- <span data-ttu-id="b2d24-803">**NX_HTTP_TIMEOUT** (0XE1) süre süresi dolduğunda sonraki pakette bekliyor</span><span class="sxs-lookup"><span data-stu-id="b2d24-803">**NX_HTTP_TIMEOUT** (0xE1) Time expired waiting on next packet</span></span>
- <span data-ttu-id="b2d24-804">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-804">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-805">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-805">**Allowed From**</span></span>

<span data-ttu-id="b2d24-806">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-806">Threads</span></span>

<span data-ttu-id="b2d24-807">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-807">**Example**</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started. */

UINT content_length;
NX_PACKET *recv_packet_ptr;

status = nx_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_http_server_param_get"></a><span data-ttu-id="b2d24-808">nx_http_server_param_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-808">nx_http_server_param_get</span></span>

### <a name="get-parameter-from-the-request"></a><span data-ttu-id="b2d24-809">İstekten parametre al</span><span class="sxs-lookup"><span data-stu-id="b2d24-809">Get parameter from the request</span></span>

<span data-ttu-id="b2d24-810">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-810">**Prototype**</span></span>

```c
UINT nx_http_server_param_get(NX_PACKET *packet_ptr,
                             UINT param_number, CHAR *param_ptr,
                             UINT max_param_size);
```

<span data-ttu-id="b2d24-811">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-811">**Description**</span></span>

<span data-ttu-id="b2d24-812">Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL parametresini almaya çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="b2d24-812">This service attempts to retrieve the specified HTTP URL parameter in the supplied request packet.</span></span> <span data-ttu-id="b2d24-813">İstenen HTTP parametresi yoksa, bu yordam NX_HTTP_NOT_FOUND durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="b2d24-813">If the requested HTTP parameter is not present, this routine returns a status of NX_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="b2d24-814">Bu yordam, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-814">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="b2d24-815">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-815">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-816">**packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-816">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="b2d24-817">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-817">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="b2d24-818">**param_number** Parametre listesinde soldan sağa sıfırdan başlayan parametrenin mantıksal numarası.</span><span class="sxs-lookup"><span data-stu-id="b2d24-818">**param_number** Logical number of the parameter starting at zero, from left to right in the parameter list.</span></span>
- <span data-ttu-id="b2d24-819">**param_ptr** Parametreyi kopyalamak için hedef alan.</span><span class="sxs-lookup"><span data-stu-id="b2d24-819">**param_ptr** Destination area to copy the parameter.</span></span>
- <span data-ttu-id="b2d24-820">**max_param_size** Parametre hedefi alanının maksimum boyutu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-820">**max_param_size** Maximum size of the parameter destination area.</span></span>

<span data-ttu-id="b2d24-821">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-821">**Return Values**</span></span>

- <span data-ttu-id="b2d24-822">**NX_SUCCESS** (0x00) başarılı http sunucusu parametre al</span><span class="sxs-lookup"><span data-stu-id="b2d24-822">**NX_SUCCESS** (0x00) Successful HTTP Server parameter get</span></span>
- <span data-ttu-id="b2d24-823">**NX_HTTP_NOT_FOUND** (0xE6) belirtilen parametre bulunamadı</span><span class="sxs-lookup"><span data-stu-id="b2d24-823">**NX_HTTP_NOT_FOUND** (0xE6) Specified parameter not found</span></span>
- <span data-ttu-id="b2d24-824">**NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) istek parametresi düzgün sonlandırılmadı</span><span class="sxs-lookup"><span data-stu-id="b2d24-824">**NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) Request parameter not properly terminated</span></span>
- <span data-ttu-id="b2d24-825">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-825">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-826">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-826">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-827">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-827">**Allowed From**</span></span>

<span data-ttu-id="b2d24-828">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-828">Threads</span></span>

<span data-ttu-id="b2d24-829">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-829">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, get the first parameter of the HTTP Client request. */

status = nx_http_server_param_get(request_packet_ptr, 0, param_destination, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
in “param_destination.” */
```

## <a name="nx_http_server_query_get"></a><span data-ttu-id="b2d24-830">nx_http_server_query_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-830">nx_http_server_query_get</span></span>

### <a name="get-query-from-the-request"></a><span data-ttu-id="b2d24-831">İstekten sorgu al</span><span class="sxs-lookup"><span data-stu-id="b2d24-831">Get query from the request</span></span>

<span data-ttu-id="b2d24-832">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-832">**Prototype**</span></span>

```c
UINT nx_http_server_query_get(NX_PACKET *packet_ptr, UINT query_number,
                             CHAR *query_ptr, UINT max_query_size);
```

<span data-ttu-id="b2d24-833">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-833">**Description**</span></span>

<span data-ttu-id="b2d24-834">Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL sorgusunu almaya çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="b2d24-834">This service attempts to retrieve the specified HTTP URL query in the supplied request packet.</span></span> <span data-ttu-id="b2d24-835">İstenen HTTP sorgusu yoksa, bu yordam NX_HTTP_NOT_FOUND durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="b2d24-835">If the requested HTTP query is not present, this routine returns a status of NX_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="b2d24-836">Bu yordam, HTTP sunucusu oluşturma (*nx_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-836">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_http_server_create()*).</span></span>

<span data-ttu-id="b2d24-837">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-837">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-838">**packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-838">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="b2d24-839">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2d24-839">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="b2d24-840">**query_number** Sıfırdan başlayan parametrenin mantıksal numarası, sorgu listesinde soldan sağa.</span><span class="sxs-lookup"><span data-stu-id="b2d24-840">**query_number** Logical number of the parameter starting at zero, from left to right in the query list.</span></span>
- <span data-ttu-id="b2d24-841">**query_ptr** Sorguyu kopyalamak için hedef alan.</span><span class="sxs-lookup"><span data-stu-id="b2d24-841">**query_ptr** Destination area to copy the query.</span></span>
- <span data-ttu-id="b2d24-842">**max_query_size** Sorgu hedefi alanının maksimum boyutu.</span><span class="sxs-lookup"><span data-stu-id="b2d24-842">**max_query_size** Maximum size of the query destination area.</span></span>

<span data-ttu-id="b2d24-843">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-843">**Return Values**</span></span>

- <span data-ttu-id="b2d24-844">**NX_SUCCESS** (0x00) başarılı http sunucusu sorgusu al</span><span class="sxs-lookup"><span data-stu-id="b2d24-844">**NX_SUCCESS** (0x00) Successful HTTP Server query get</span></span>
- <span data-ttu-id="b2d24-845">**NX_HTTP_FAILED** (0xE2) sorgu boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="b2d24-845">**NX_HTTP_FAILED** (0xE2) Query size too small.</span></span>
- <span data-ttu-id="b2d24-846">**NX_HTTP_NOT_FOUND** (0xE6) belirtilen sorgu bulunamadı</span><span class="sxs-lookup"><span data-stu-id="b2d24-846">**NX_HTTP_NOT_FOUND** (0xE6) Specified query not found</span></span>
- <span data-ttu-id="b2d24-847">**NX_HTTP_NO_QUERY_PARSED** (0xF2) istemci Isteğinde sorgu yok</span><span class="sxs-lookup"><span data-stu-id="b2d24-847">**NX_HTTP_NO_QUERY_PARSED** (0xF2) No query in Client request</span></span>
- <span data-ttu-id="b2d24-848">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-848">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-849">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-849">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-850">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-850">**Allowed From**</span></span>

<span data-ttu-id="b2d24-851">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-851">Threads</span></span>

<span data-ttu-id="b2d24-852">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-852">**Example**</span></span>

```c
/* Assuming we are in the application’s request notify callback
routine, get the first query of the HTTP Client request. */
status = nx_http_server_query_get(request_packet_ptr, 0, query_destination, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
in “query_destination.” */
```

##   
<span data-ttu-id="b2d24-853">nx_http_server_start</span><span class="sxs-lookup"><span data-stu-id="b2d24-853">nx_http_server_start</span></span>

### <a name="start-the-http-server"></a><span data-ttu-id="b2d24-854">HTTP sunucusunu başlatma</span><span class="sxs-lookup"><span data-stu-id="b2d24-854">Start the HTTP Server</span></span>

<span data-ttu-id="b2d24-855">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-855">**Prototype**</span></span>

```c
UINT nx_http_server_start(NX_HTTP_SERVER *http_server_ptr);
```

<span data-ttu-id="b2d24-856">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-856">**Description**</span></span>

<span data-ttu-id="b2d24-857">Bu hizmet, önceden oluşturma HTTP sunucu örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-857">This service starts the previously create HTTP Server instance.</span></span>

<span data-ttu-id="b2d24-858">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-858">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-859">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-859">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

<span data-ttu-id="b2d24-860">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-860">**Return Values**</span></span>

- <span data-ttu-id="b2d24-861">**NX_SUCCESS** (0x00) başarılı http sunucusu başlatması</span><span class="sxs-lookup"><span data-stu-id="b2d24-861">**NX_SUCCESS** (0x00) Successful HTTP Server start</span></span>
- <span data-ttu-id="b2d24-862">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-862">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-863">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-863">**Allowed From**</span></span>

<span data-ttu-id="b2d24-864">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-864">Initialization, Threads</span></span>

<span data-ttu-id="b2d24-865">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-865">**Example**</span></span>

```c
/* Start the HTTP Server instance “my_server.” */
status = nx_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_http_server_stop"></a><span data-ttu-id="b2d24-866">nx_http_server_stop</span><span class="sxs-lookup"><span data-stu-id="b2d24-866">nx_http_server_stop</span></span>

### <a name="stop-the-http-server"></a><span data-ttu-id="b2d24-867">HTTP sunucusunu durdur</span><span class="sxs-lookup"><span data-stu-id="b2d24-867">Stop the HTTP Server</span></span>

<span data-ttu-id="b2d24-868">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-868">**Prototype**</span></span>

```c
UINT nx_http_server_stop(NX_HTTP_SERVER *http_server_ptr);
```

<span data-ttu-id="b2d24-869">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-869">**Description**</span></span>

<span data-ttu-id="b2d24-870">Bu hizmet, önceden oluşturma HTTP sunucu örneğini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="b2d24-870">This service stops the previously create HTTP Server instance.</span></span> <span data-ttu-id="b2d24-871">Bu yordam, bir HTTP sunucu örneği silinmeden önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-871">This routine should be called prior to deleting an HTTP Server instance.</span></span>

<span data-ttu-id="b2d24-872">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-872">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-873">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b2d24-873">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

<span data-ttu-id="b2d24-874">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-874">**Return Values**</span></span>

- <span data-ttu-id="b2d24-875">**NX_SUCCESS** (0x00) başarılı http sunucusu durdur</span><span class="sxs-lookup"><span data-stu-id="b2d24-875">**NX_SUCCESS** (0x00) Successful HTTP Server stop</span></span>
- <span data-ttu-id="b2d24-876">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-876">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-877">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="b2d24-877">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

<span data-ttu-id="b2d24-878">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-878">**Allowed From**</span></span>

<span data-ttu-id="b2d24-879">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b2d24-879">Threads</span></span>

<span data-ttu-id="b2d24-880">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-880">**Example**</span></span>

```c
/* Stop the HTTP Server instance “my_server.” */

status = nx_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_http_server_type_get"></a><span data-ttu-id="b2d24-881">nx_http_server_type_get</span><span class="sxs-lookup"><span data-stu-id="b2d24-881">nx_http_server_type_get</span></span>

### <a name="extract-file-type-from-client-http-request"></a><span data-ttu-id="b2d24-882">Istemci HTTP isteğinden dosya türünü Ayıkla</span><span class="sxs-lookup"><span data-stu-id="b2d24-882">Extract file type from Client HTTP request</span></span>

<span data-ttu-id="b2d24-883">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-883">**Prototype**</span></span>

```c
UINT nx_http_server_type_get(NX_HTTP_SERVER *http_server_ptr,
                            CHAR *name, CHAR *http_type_string);
```

<span data-ttu-id="b2d24-884">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-884">**Description**</span></span>

<span data-ttu-id="b2d24-885">Bu hizmet, arabellek *HTTP_TYPE_STRING* http istek türünü ve giriş arabelleği *ADıNDAN*(genellikle URL) gelen dönüş değerindeki uzunluğu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-885">This service extracts the HTTP request type in the buffer *http_type_string* and its length in the return value from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="b2d24-886">MIME eşlemesi bulunmazsa, varsayılan olarak "metin/düz" tür olur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-886">If no MIME map is found, it defaults to the “text/plain” type.</span></span> <span data-ttu-id="b2d24-887">Aksi takdirde, bir eşleşme için ayıklanan tür, HTTP sunucusu varsayılan MIME eşlemeleriyle karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-887">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="b2d24-888">NetX HTTP sunucusundaki varsayılan MIME haritaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b2d24-888">The default MIME maps in NetX HTTP Server are:</span></span>

- <span data-ttu-id="b2d24-889">HTML metni/HTML</span><span class="sxs-lookup"><span data-stu-id="b2d24-889">html text/html</span></span>
- <span data-ttu-id="b2d24-890">htm metin/html</span><span class="sxs-lookup"><span data-stu-id="b2d24-890">htm text/html</span></span>
- <span data-ttu-id="b2d24-891">txt metin/düz</span><span class="sxs-lookup"><span data-stu-id="b2d24-891">txt text/plain</span></span>
- <span data-ttu-id="b2d24-892">GIF resmi/GIF</span><span class="sxs-lookup"><span data-stu-id="b2d24-892">gif image/gif</span></span>
- <span data-ttu-id="b2d24-893">jpg resmi/JPEG</span><span class="sxs-lookup"><span data-stu-id="b2d24-893">jpg image/jpeg</span></span>
- <span data-ttu-id="b2d24-894">ICO resmi/x-simgesi</span><span class="sxs-lookup"><span data-stu-id="b2d24-894">ico image/x-icon</span></span>

<span data-ttu-id="b2d24-895">Sağlanırsa, Kullanıcı tanımlı ek MIME haritaları kümesi de arar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-895">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="b2d24-896">Kullanıcı tanımlı haritalar hakkında daha fazla bilgi için bkz. *nx_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="b2d24-896">See *nx_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="b2d24-897">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-897">This service is deprecated.</span></span> <span data-ttu-id="b2d24-898">Geliştiricilerin *nx_http_server_type_get_extended ()* uygulamasına geçirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="b2d24-898">Developers are encouraged to migrate to *nx_http_server_type_get_extended().*</span></span>

<span data-ttu-id="b2d24-899">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-899">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-900">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-900">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="b2d24-901">**ad** Aranacak arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-901">**name** Pointer to buffer to search</span></span>
- <span data-ttu-id="b2d24-902">**http_type_string** (ayıklanan HTML türüne yönelik işaretçi)</span><span class="sxs-lookup"><span data-stu-id="b2d24-902">**http_type_string** (Pointer to extracted HTML type)</span></span>

<span data-ttu-id="b2d24-903">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-903">**Return Values**</span></span>

- <span data-ttu-id="b2d24-904">**Bayt cinsinden dize uzunluğu** Sıfır olmayan değer başarılı</span><span class="sxs-lookup"><span data-stu-id="b2d24-904">**Length of string in bytes** Non zero value is success</span></span>
- <span data-ttu-id="b2d24-905">**Sıfır hatayı gösterir**</span><span class="sxs-lookup"><span data-stu-id="b2d24-905">**Zero indicates error**</span></span>

<span data-ttu-id="b2d24-906">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-906">**Allowed From**</span></span>

<span data-ttu-id="b2d24-907">Uygulama</span><span class="sxs-lookup"><span data-stu-id="b2d24-907">Application</span></span>

<span data-ttu-id="b2d24-908">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-908">**Example**</span></span>

```c
/* my_server is a previously created HTTP server, which starts accepting 
client requests when *nx_http_server_start* is called*/

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
string_length = nx_http_server_type_get(&my_server_ptr,
                my_server.nx_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
```

<span data-ttu-id="b2d24-909">Daha ayrıntılı bir örnek için bkz. için açıklama</span><span class="sxs-lookup"><span data-stu-id="b2d24-909">For a more detailed example, see the description for</span></span>

<span data-ttu-id="b2d24-910">*nx_http_server_callback_generate_response_header.*</span><span class="sxs-lookup"><span data-stu-id="b2d24-910">*nx_http_server_callback_generate_response_header.*</span></span>

## <a name="nx_http_server_type_get_extended"></a><span data-ttu-id="b2d24-911">nx_http_server_type_get_extended</span><span class="sxs-lookup"><span data-stu-id="b2d24-911">nx_http_server_type_get_extended</span></span>

### <a name="extract-file-type-from-client-http-request"></a><span data-ttu-id="b2d24-912">Istemci HTTP isteğinden dosya türünü Ayıkla</span><span class="sxs-lookup"><span data-stu-id="b2d24-912">Extract file type from Client HTTP request</span></span>

<span data-ttu-id="b2d24-913">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-913">**Prototype**</span></span>

```c
UINT nx_http_server_type_get_extended(
     NX_HTTP_SERVER *http_server_ptr,
     CHAR *name, CHAR *http_type_string,
     UINT http_type_string_max_size);
```

<span data-ttu-id="b2d24-914">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-914">**Description**</span></span>

<span data-ttu-id="b2d24-915">Bu hizmet, arabellek *HTTP_TYPE_STRING* http istek türünü ve giriş arabelleği *ADıNDAN*(genellikle URL) gelen dönüş değerindeki uzunluğu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-915">This service extracts the HTTP request type in the buffer *http_type_string* and its length in the return value from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="b2d24-916">MIME eşlemesi bulunmazsa, varsayılan olarak "metin/düz" tür olur.</span><span class="sxs-lookup"><span data-stu-id="b2d24-916">If no MIME map is found, it defaults to the “text/plain” type.</span></span> <span data-ttu-id="b2d24-917">Aksi takdirde, bir eşleşme için ayıklanan tür, HTTP sunucusu varsayılan MIME eşlemeleriyle karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-917">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="b2d24-918">NetX Duo HTTP sunucusundaki varsayılan MIME haritaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b2d24-918">The default MIME maps in NetX Duo HTTP Server are:</span></span>

- <span data-ttu-id="b2d24-919">HTML metni/HTML</span><span class="sxs-lookup"><span data-stu-id="b2d24-919">html text/html</span></span>
- <span data-ttu-id="b2d24-920">htm metin/html</span><span class="sxs-lookup"><span data-stu-id="b2d24-920">htm text/html</span></span>
- <span data-ttu-id="b2d24-921">txt metin/düz</span><span class="sxs-lookup"><span data-stu-id="b2d24-921">txt text/plain</span></span>
- <span data-ttu-id="b2d24-922">GIF resmi/GIF</span><span class="sxs-lookup"><span data-stu-id="b2d24-922">gif image/gif</span></span>
- <span data-ttu-id="b2d24-923">jpg resmi/JPEG</span><span class="sxs-lookup"><span data-stu-id="b2d24-923">jpg image/jpeg</span></span>
- <span data-ttu-id="b2d24-924">ICO resmi/x-simgesi</span><span class="sxs-lookup"><span data-stu-id="b2d24-924">ico image/x-icon</span></span>

<span data-ttu-id="b2d24-925">Sağlanırsa, Kullanıcı tanımlı ek MIME haritaları kümesi de arar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-925">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="b2d24-926">Kullanıcı tanımlı haritalar hakkında daha fazla bilgi için bkz. *nx_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="b2d24-926">See *nx_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="b2d24-927">Bu hizmet *nx_http_server_type_get ()* yerini alır.</span><span class="sxs-lookup"><span data-stu-id="b2d24-927">This service replaces *nx_http_server_type_get().*</span></span> <span data-ttu-id="b2d24-928">Bu sürüm, ek uzunluk bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-928">This version supplies additional length information.</span></span>

<span data-ttu-id="b2d24-929">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-929">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-930">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-930">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="b2d24-931">**ad** Aranacak arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-931">**name** Pointer to buffer to search</span></span>
- <span data-ttu-id="b2d24-932">**name_length** Aranacak arabelleğin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="b2d24-932">**name_length** Length of buffer to search</span></span>
- <span data-ttu-id="b2d24-933">**http_type_string** (ayıklanan HTML türüne yönelik işaretçi)</span><span class="sxs-lookup"><span data-stu-id="b2d24-933">**http_type_string** (Pointer to extracted HTML type)</span></span>
- <span data-ttu-id="b2d24-934">**http_type_string_max_size**</span><span class="sxs-lookup"><span data-stu-id="b2d24-934">**http_type_string_max_size**</span></span>

<span data-ttu-id="b2d24-935">*Http_type_string* arabelleğinin boyutu</span><span class="sxs-lookup"><span data-stu-id="b2d24-935">Size of the *http_type_string* buffer</span></span>

<span data-ttu-id="b2d24-936">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-936">**Return Values**</span></span>

- <span data-ttu-id="b2d24-937">**Bayt cinsinden dize uzunluğu** Sıfır olmayan değer başarılı</span><span class="sxs-lookup"><span data-stu-id="b2d24-937">**Length of string in bytes** Non zero value is success</span></span><br /><span data-ttu-id="b2d24-938">Sıfır hatayı gösterir</span><span class="sxs-lookup"><span data-stu-id="b2d24-938">Zero indicates error</span></span>

<span data-ttu-id="b2d24-939">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-939">**Allowed From**</span></span>

<span data-ttu-id="b2d24-940">Uygulama</span><span class="sxs-lookup"><span data-stu-id="b2d24-940">Application</span></span>

<span data-ttu-id="b2d24-941">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-941">**Example**</span></span>

```c
/* my_server is a previously created HTTP server, which starts accepting 
client requests when *nx_http_server_start* is called*/

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
string_length = nx_http_server_type_get_extended(&my_server,
                my_server.nx_http_server_request_resource, resource_length,
                temp_string, sizeof(temp_string));

/* If string_length is non zero, the HTTP string is extracted. */
```

<span data-ttu-id="b2d24-942">Daha ayrıntılı bir örnek için bkz. için açıklama</span><span class="sxs-lookup"><span data-stu-id="b2d24-942">For a more detailed example, see the description for</span></span>

<span data-ttu-id="b2d24-943">*nx_http_server_callback_generate_response_header.*</span><span class="sxs-lookup"><span data-stu-id="b2d24-943">*nx_http_server_callback_generate_response_header.*</span></span>

## <a name="nx_http_server_digest_authenticate_notify_set"></a><span data-ttu-id="b2d24-944">nx_http_server_digest_authenticate_notify_set</span><span class="sxs-lookup"><span data-stu-id="b2d24-944">nx_http_server_digest_authenticate_notify_set</span></span>

### <a name="set-digest-authenticate-callback-function"></a><span data-ttu-id="b2d24-945">Özet kimlik doğrulaması geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="b2d24-945">Set digest authenticate callback function</span></span>

<span data-ttu-id="b2d24-946">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-946">**Prototype**</span></span>

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

<span data-ttu-id="b2d24-947">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-947">**Description**</span></span>

<span data-ttu-id="b2d24-948">Bu hizmet Özet kimlik doğrulaması gerçekleştirildiğinde çağrılan geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-948">This service sets the callback invoked when digest authenticate is performed.</span></span>

<span data-ttu-id="b2d24-949">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-949">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-950">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-950">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="b2d24-951">**digest_authenticate_callback** Özet kimlik doğrulaması geri çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-951">**digest_authenticate_callback** Pointer to digest authenticate callback</span></span>

<span data-ttu-id="b2d24-952">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-952">**Return Values**</span></span>

- <span data-ttu-id="b2d24-953">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="b2d24-953">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="b2d24-954">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-954">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="b2d24-955">NX_NOT_SUPPORTED (0x4B) Özet kimlik doğrulaması etkin değil</span><span class="sxs-lookup"><span data-stu-id="b2d24-955">NX_NOT_SUPPORTED (0x4B) Digest authenticate not enabled</span></span>

<span data-ttu-id="b2d24-956">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-956">**Allowed From**</span></span>

<span data-ttu-id="b2d24-957">Uygulama</span><span class="sxs-lookup"><span data-stu-id="b2d24-957">Application</span></span>

<span data-ttu-id="b2d24-958">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-958">**Example**</span></span>

```c
UINT digest_authenticate_callback(NX_HTTP_SERVER *server_ptr, CHAR *name_ptr,
                                 CHAR *realm_ptr, CHAR *password_ptr,
                                 CHAR *method,CHAR *authorization_uri,
                                 CHAR *authorization_nc,
                                 CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and
before starting HTTP services when nx_http_server_start is called, set the
digest authenticate callback: */

status = nx_http_server_digest_authenticate_notify_set (&my_server,
                                                       digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_http_server_authentication_check_set"></a><span data-ttu-id="b2d24-959">nx_http_server_authentication_check_set</span><span class="sxs-lookup"><span data-stu-id="b2d24-959">nx_http_server_authentication_check_set</span></span>

### <a name="set-authentication-checking-callback-function"></a><span data-ttu-id="b2d24-960">Kimlik doğrulama denetimi geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="b2d24-960">Set authentication checking callback function</span></span>

<span data-ttu-id="b2d24-961">**Prototype**</span><span class="sxs-lookup"><span data-stu-id="b2d24-961">**Prototype**</span></span>

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

<span data-ttu-id="b2d24-962">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b2d24-962">**Description**</span></span>

<span data-ttu-id="b2d24-963">Bu hizmet, kimlik doğrulama denetiminin geri çağırma işlevini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b2d24-963">This service sets the callback function of authentication checking.</span></span>

<span data-ttu-id="b2d24-964">**Giriş parametreleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-964">**Input Parameters**</span></span>

- <span data-ttu-id="b2d24-965">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="b2d24-965">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="b2d24-966">**authentication_check_extended** Uygulamanın kimlik doğrulama denetimi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="b2d24-966">**authentication_check_extended** Pointer to application’s authentication checking</span></span>

<span data-ttu-id="b2d24-967">**Dönüş değerleri**</span><span class="sxs-lookup"><span data-stu-id="b2d24-967">**Return Values**</span></span>

- <span data-ttu-id="b2d24-968">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="b2d24-968">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="b2d24-969">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="b2d24-969">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

<span data-ttu-id="b2d24-970">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="b2d24-970">**Allowed From**</span></span>

<span data-ttu-id="b2d24-971">Uygulama</span><span class="sxs-lookup"><span data-stu-id="b2d24-971">Application</span></span>

<span data-ttu-id="b2d24-972">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="b2d24-972">**Example**</span></span>

```c
static UINT authentication_check_extended(NX_HTTP_SERVER *server_ptr,
                                         UINT request_type, CHAR *resource,
                                         CHAR **name, UINT *name_length,
                                         CHAR **password, 
                                         UINT *password_length,
                                         CHAR **realm, UINT *realm_length)
{

    /* Just use a simple name, password, and realm for all
    requests and resources. */

    *name = "name";
    *password = "password";
    *realm = "NetX Duo HTTP demo";
    *name_length = 4;
    *password_length = 8;
    *realm_length = 18;

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and
before starting HTTP services when nx_http_server_start is called, set 
the authentication checking callback: */

nx_http_server_authentication_check_set (&my_server,
                                        authentication_check_extended);
```