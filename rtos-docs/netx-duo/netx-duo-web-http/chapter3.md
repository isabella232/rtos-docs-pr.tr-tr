---
title: Bölüm 3-HTTP hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Web HTTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 30168ad5a564b0f4c0a8c999046c5103385f4f90
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826986"
---
# <a name="chapter-3---description-of-http-services"></a><span data-ttu-id="c8f61-103">Bölüm 3-HTTP hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="c8f61-103">Chapter 3 - Description of HTTP services</span></span>

<span data-ttu-id="c8f61-104">Bu bölüm, tüm NetX Web HTTP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-104">This chapter contains a description of all NetX Web HTTP services (listed below) in alphabetical order.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="http-and-https-client-api"></a><span data-ttu-id="c8f61-106">HTTP ve HTTPS Istemci API 'SI</span><span class="sxs-lookup"><span data-stu-id="c8f61-106">HTTP and HTTPS Client API</span></span>

## <a name="nx_web_http_client_connect"></a><span data-ttu-id="c8f61-107">nx_web_http_client_connect</span><span class="sxs-lookup"><span data-stu-id="c8f61-107">nx_web_http_client_connect</span></span>

<span data-ttu-id="c8f61-108">Özel istekler için bir HTTP sunucusuna düz metin yuvası açma</span><span class="sxs-lookup"><span data-stu-id="c8f61-108">Open a plaintext socket to an HTTP server for custom requests</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-109">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-109">Prototype</span></span>

```C
UINT nx_web_http_client_connect(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip,
    UINT server_port, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-110">Description</span></span>

<span data-ttu-id="c8f61-111">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-111">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-112">Bu hizmet bir HTTP sunucusuna düz metin TCP yuvası açar, ancak hiçbir istek göndermez.</span><span class="sxs-lookup"><span data-stu-id="c8f61-112">This service opens a plaintext TCP socket to an HTTP server but does not send any requests.</span></span> <span data-ttu-id="c8f61-113">İstekler n *x_web_http_client_request_initialize ()* ile oluşturulur ve *nx_web_http_client_request_send ()* kullanılarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-113">Requests are created with n *x_web_http_client_request_initialize()* and sent using *nx_web_http_client_request_send()*.</span></span> <span data-ttu-id="c8f61-114">*Nx_web_http_client_request_header_add ()* kullanılarak Isteğe özel http üstbilgileri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-114">Custom HTTP headers may be added to the request using *nx_web_http_client_request_header_add()*.</span></span>

<span data-ttu-id="c8f61-115">Bu hizmetin kullanılması, bir uygulamanın isteğe herhangi sayıda özel üst bilgi eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-115">Use of this service enables an application to add any number of custom headers to the request.</span></span> <span data-ttu-id="c8f61-116">**Bu, belirli uygulamalar için tasarlanan özelleştirilmiş HTTP isteklerine izin verir.**</span><span class="sxs-lookup"><span data-stu-id="c8f61-116">**This allows for customized HTTP requests intended for specific applications.**</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-117">Nx_web_http_client_ \* _start yöntemleri kolaylık sağlaması için sunulmaktadır (örn. *nx_web_http_client_get_start*()) ve istek oluşturma ve yuva bağlantısını işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-117">The nx_web_http_client_\*_start methods are provided for convenience (e.g. *nx_web_http_client_get_start*()) and handle the request generation and socket connection.</span></span> <span data-ttu-id="c8f61-118">İsteklerinize özel HTTP üstbilgileri gerekmiyorsa, *nx_web_http_client_connect ()* yerine bu hizmetleri ve ilgili yordamları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-118">You can use those services instead of *nx_web_http_client_connect()* and the related routines if you do not need custom HTTP headers in your requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-119">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-119">Input Parameters</span></span>

- <span data-ttu-id="c8f61-120">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-120">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-121">**server_ip** Uzak HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-121">**server_ip** IP address of remote HTTP server.</span></span>
- <span data-ttu-id="c8f61-122">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası (örneğin, HTTP için 80).</span><span class="sxs-lookup"><span data-stu-id="c8f61-122">**server_port** Port on remote HTTP server (e.g. 80 for HTTP).</span></span>
- <span data-ttu-id="c8f61-123">**wait_option** Hizmetin temel alınan ağ işlemleri için ne kadar süre bekleyeceğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-123">**wait_option** Defines how long the service will wait for underlying network operations.</span></span> <span data-ttu-id="c8f61-124">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-124">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-125">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-125">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-126">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-126">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-127">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-127">Return Values</span></span>

- <span data-ttu-id="c8f61-128">**NX_SUCCESS** (0x00) TCP yuvasının başarılı bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-128">**NX_SUCCESS** (0x00) Successful connection of TCP socket.</span></span>
- <span data-ttu-id="c8f61-129">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-129">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-130">NX_WEB_HTTP_NOT_READY (0x3000A) başka bir istek zaten devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="c8f61-130">NX_WEB_HTTP_NOT_READY (0x3000A) Another request is already in progress.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-131">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-131">Allowed From</span></span>

<span data-ttu-id="c8f61-132">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-132">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-133">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-133">Example</span></span>

```C
NXD_ADDRESS server_ip_addr;

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

nx_web_http_client_connect(&my_client, &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get* until the entire response is retrieved. *./

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);
    /* Process response packets… */
}
```

## <a name="nx_web_http_client_create"></a><span data-ttu-id="c8f61-134">nx_web_http_client_create</span><span class="sxs-lookup"><span data-stu-id="c8f61-134">nx_web_http_client_create</span></span>

<span data-ttu-id="c8f61-135">HTTP Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8f61-135">Create an HTTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-136">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-136">Prototype</span></span>

```C
UINT nx_web_http_client_create(NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *client_name, NX_IP *ip_ptr, NX_PACKET_POOL *pool_ptr,
    ULONG window_size);
```

### <a name="description"></a><span data-ttu-id="c8f61-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-137">Description</span></span>

<span data-ttu-id="c8f61-138">Bu hizmet, belirtilen IP örneğinde bir HTTP Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-138">This service creates an HTTP Client instance on the specified IP instance.</span></span> <span data-ttu-id="c8f61-139">Istemci örneği, HTTP ya da HTTPS için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-139">The Client instance can be used for either HTTP or HTTPS.</span></span> <span data-ttu-id="c8f61-140">HTTP veya HTTPS örneği başlatma hakkında daha fazla bilgi için bkz. *nx_web_http_client_connect ()* ve *nx_web_http_client_secure_connect ()* .</span><span class="sxs-lookup"><span data-stu-id="c8f61-140">See the services *nx_web_http_client_connect()* and *nx_web_http_client_secure_connect()* for more information on starting an HTTP or HTTPS instance.</span></span> <span data-ttu-id="c8f61-141">Ayrıca, GET, PUT ve POST yöntemlerinin basit etkinleştirmeleri için nx_web_http_client_post_ nx_web_http_client_get_ \* \*, \*nx_web_http_client_put_ \* \*\* için API 'ye de bakın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-141">Also refer to the API for \*nx_web_http_client_get_\*\*, *nx_web_http_client_put_\*\*, *nx_web_http_client_post_** for simple invocations of GET, PUT, and POST methods.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-142">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-142">Input Parameters</span></span>

- <span data-ttu-id="c8f61-143">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-143">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-144">**client_name** HTTP Istemci örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-144">**client_name** Name of HTTP Client instance.</span></span>
- <span data-ttu-id="c8f61-145">**ip_ptr** IP örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-145">**ip_ptr** Pointer to IP instance.</span></span>
- <span data-ttu-id="c8f61-146">**pool_ptr** Varsayılan paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-146">**pool_ptr** Pointer to default packet pool.</span></span> <span data-ttu-id="c8f61-147">Bu havuzdaki paketlerin, tüm yanıt üst bilgisini işleyecek kadar büyük bir yükün olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-147">Note that the packets in this pool must have a payload large enough to handle the complete response header.</span></span> <span data-ttu-id="c8f61-148">Bu, *nx_web_http_client. h* içinde *NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE* tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-148">This is defined by *NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE* in *nx_web_http_client.h*.</span></span>
- <span data-ttu-id="c8f61-149">**window_size** Istemcinin TCP yuvası alma penceresinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-149">**window_size** Size of the Client’s TCP socket receive window.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-150">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-150">Return Values</span></span>

- <span data-ttu-id="c8f61-151">**NX_SUCCESS** (0x00) başarılı http istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8f61-151">**NX_SUCCESS** (0x00) Successful HTTP Client create</span></span>
- <span data-ttu-id="c8f61-152">NX_PTR_ERROR (0x16) geçersiz HTTP, ip_ptr veya paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-152">NX_PTR_ERROR (0x16) Invalid HTTP, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="c8f61-153">NX_WEB_HTTP_POOL_ERROR (0x30009) paket havuzunda geçersiz yük boyutu</span><span class="sxs-lookup"><span data-stu-id="c8f61-153">NX_WEB_HTTP_POOL_ERROR (0x30009) Invalid payload size in packet pool</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-154">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-154">Allowed From</span></span>

<span data-ttu-id="c8f61-155">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-155">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-156">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-156">Example</span></span>

```C
/* Create the HTTP Client instance "my_client" on "ip_0". */
status = nx_web_http_client_create(&my_client, "my client", &ip_0, &pool_0, 8192);

/* If status is NX_SUCCESS an HTTP Client instance was successfully
    created. */
```

## <a name="nx_web_http_client_delete"></a><span data-ttu-id="c8f61-157">nx_web_http_client_delete</span><span class="sxs-lookup"><span data-stu-id="c8f61-157">nx_web_http_client_delete</span></span>

<span data-ttu-id="c8f61-158">HTTP Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="c8f61-158">Delete an HTTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-159">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-159">Prototype</span></span>

```C
UINT nx_web_http_client_delete(NX_WEB_HTTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="c8f61-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-160">Description</span></span>

<span data-ttu-id="c8f61-161">Bu hizmet, önceden oluşturulmuş bir HTTP Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-161">This service deletes a previously created HTTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-162">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-162">Input Parameters</span></span>

- <span data-ttu-id="c8f61-163">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-163">**client_ptr** Pointer to HTTP Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-164">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-164">Return Values</span></span>

- <span data-ttu-id="c8f61-165">**NX_SUCCESS** (0x00) başarılı http istemcisi silme</span><span class="sxs-lookup"><span data-stu-id="c8f61-165">**NX_SUCCESS** (0x00) Successful HTTP Client delete</span></span>
- <span data-ttu-id="c8f61-166">NX_PTR_ERROR (0x16) geçersiz HTTP işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-166">NX_PTR_ERROR (0x16) Invalid HTTP pointer</span></span>
- <span data-ttu-id="c8f61-167">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-167">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-168">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-168">Allowed From</span></span>

<span data-ttu-id="c8f61-169">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-169">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-170">Example</span></span>

```C
/* Delete the HTTP Client instance "my_client." */
status = nx_web_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully
    deleted. */
```

## <a name="nx_web_http_client_delete_start"></a><span data-ttu-id="c8f61-171">nx_web_http_client_delete_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-171">nx_web_http_client_delete_start</span></span>

<span data-ttu-id="c8f61-172">Düz metin HTTP SILME isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-172">Start a plaintext HTTP DELETE request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-173">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-173">Prototype</span></span>

```C
UINT nx_web_http_client_delete_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-174">Description</span></span>

<span data-ttu-id="c8f61-175">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-175">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-176">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynak için SILME isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-176">This service attempts to send a DELETE request for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-177">Bu yordam NX_SUCCESS döndürürse, uygulama daha sonra sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilirler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-177">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response.</span></span>

<span data-ttu-id="c8f61-178">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-178">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-179">Bu API kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-179">This API is deprecated.</span></span> <span data-ttu-id="c8f61-180">Geliştiricilerin *nx_web_http_client_delete_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-180">Developers are encouraged to use *nx_web_http_client_delete_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-181">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-181">Input Parameters</span></span>

- <span data-ttu-id="c8f61-182">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-182">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-183">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-183">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-184">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-184">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-185">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-185">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-186">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-186">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-187">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-187">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-188">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-188">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-189">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-189">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-190">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-190">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-191">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-191">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-192">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-192">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-193">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-193">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-194">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-194">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-195">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-195">Return Values</span></span>

- <span data-ttu-id="c8f61-196">**NX_SUCCESS** (0x00) http istemcisi silme Isteği iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-196">**NX_SUCCESS** (0x00) Successfully sent HTTP Client DELETE request message</span></span>
- <span data-ttu-id="c8f61-197">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-197">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-198">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-198">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-199">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-199">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-200">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-200">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-201">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-201">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-202">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-202">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-203">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-203">Allowed From</span></span>

<span data-ttu-id="c8f61-204">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-204">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-205">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-205">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_start(&my_client, &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_delete_start_extended"></a><span data-ttu-id="c8f61-206">nx_web_http_client_delete_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-206">nx_web_http_client_delete_start_extended</span></span>

<span data-ttu-id="c8f61-207">Düz metin HTTP SILME isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-207">Start a plaintext HTTP DELETE request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-208">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-208">Prototype</span></span>

```C
UINT nx_web_http_client_delete_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-209">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-209">Description</span></span>

<span data-ttu-id="c8f61-210">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-210">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-211">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynak için SILME isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-211">This service attempts to send a DELETE request for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-212">Bu yordam NX_SUCCESS döndürürse, uygulama daha sonra sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilirler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-212">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response.</span></span>

<span data-ttu-id="c8f61-213">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-213">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-214">Kaynak, konak, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-214">The strings of resource, host, username and password must be NULL-terminated, and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-215">Bu hizmet *nx_web_http_client_delete_start* () yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-215">This service replaces *nx_web_http_client_delete_start* ().</span></span> <span data-ttu-id="c8f61-216">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-216">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-217">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-217">Input Parameters</span></span>

- <span data-ttu-id="c8f61-218">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-218">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-219">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-219">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-220">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-220">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-221">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-221">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-222">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-222">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-223">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-223">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-224">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-224">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-225">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-225">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-226">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-226">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-227">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-227">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-228">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-228">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-229">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-229">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-230">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-230">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-231">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-231">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-232">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-232">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-233">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-233">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-234">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-234">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-235">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-235">Return Values</span></span>

- <span data-ttu-id="c8f61-236">**NX_SUCCESS** (0x00) http istemcisi silme Isteği iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-236">**NX_SUCCESS** (0x00) Successfully sent HTTP Client DELETE request message</span></span>
- <span data-ttu-id="c8f61-237">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-237">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-238">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-238">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-239">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-239">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-240">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-240">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-241">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-241">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-242">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-242">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-243">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-243">Allowed From</span></span>

<span data-ttu-id="c8f61-244">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-244">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-245">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-245">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_start_extended(&my_client,
    &server_ip_address,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_delete_secure_start"></a><span data-ttu-id="c8f61-246">nx_web_http_client_delete_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-246">nx_web_http_client_delete_secure_start</span></span>

<span data-ttu-id="c8f61-247">Şifrelenmiş bir HTTPS SILME isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-247">Start an encrypted HTTPS DELETE request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-248">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-248">Prototype</span></span>

```C
UINT nx_web_http_client_delete_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-249">Description</span></span>

<span data-ttu-id="c8f61-250">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-250">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-251">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynak için SILME isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-251">This service attempts to send a DELETE request for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-252">Bu yordam NX_SUCCESS döndürürse, uygulama daha sonra sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilirler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-252">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response.</span></span>

<span data-ttu-id="c8f61-253">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-253">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-254">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-254">This service is deprecated.</span></span> <span data-ttu-id="c8f61-255">Geliştiricilerin *nx_web_http_client_delete_secure_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-255">Developers are encouraged to use *nx_web_http_client_delete_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-256">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-256">Input Parameters</span></span>

- <span data-ttu-id="c8f61-257">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-257">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-258">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-258">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-259">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-259">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-260">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-260">**resource** Pointer to URL string for requested resource.</span></span> <span data-ttu-id="c8f61-261">Kaynak, NULL ile sonlandırılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-261">resource must be NULL-terminated.</span></span>
- <span data-ttu-id="c8f61-262">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-262">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-263">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-263">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-264">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-264">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-265">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-265">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-266">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-266">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-267">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-267">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-268">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-268">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-269">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-269">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-270">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-270">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-271">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-271">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-272">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-272">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-273">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-273">Return Values</span></span>

- <span data-ttu-id="c8f61-274">**NX_SUCCESS** (0x00) http istemcisi silme Isteği iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-274">**NX_SUCCESS** (0x00) Successfully sent HTTP Client DELETE request message</span></span>
- <span data-ttu-id="c8f61-275">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-275">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-276">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-276">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-277">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-277">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-278">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-278">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-279">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-279">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-280">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-280">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-281">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-281">Allowed From</span></span>

<span data-ttu-id="c8f61-282">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-282">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-283">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-283">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_delete_secure_start_extended"></a><span data-ttu-id="c8f61-284">nx_web_http_client_delete_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-284">nx_web_http_client_delete_secure_start_extended</span></span>

<span data-ttu-id="c8f61-285">Şifrelenmiş bir HTTPS SILME isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-285">Start an encrypted HTTPS DELETE request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-286">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-286">Prototype</span></span>

```C
UINT nx_web_http_client_delete_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-287">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-287">Description</span></span>

<span data-ttu-id="c8f61-288">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-288">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-289">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynak için SILME isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-289">This service attempts to send a DELETE request for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-290">Bu yordam NX_SUCCESS döndürürse, uygulama daha sonra sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilirler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-290">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response.</span></span>

<span data-ttu-id="c8f61-291">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-291">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-292">Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-292">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-293">Bu hizmet *nx_web_http_client_delete_secure_start*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-293">This service replaces *nx_web_http_client_delete_secure_start*().</span></span> <span data-ttu-id="c8f61-294">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-294">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-295">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-295">Input Parameters</span></span>

- <span data-ttu-id="c8f61-296">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-296">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-297">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-297">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-298">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-298">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-299">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-299">**resource** Pointer to URL string for requested resource.</span></span> <span data-ttu-id="c8f61-300">Kaynak, NULL ile sonlandırılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-300">resource must be NULL-terminated.</span></span>
- <span data-ttu-id="c8f61-301">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-301">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-302">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-302">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-303">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-303">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-304">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-304">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-305">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-305">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-306">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-306">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-307">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-307">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-308">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-308">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-309">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-309">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-310">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-310">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-311">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-311">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-312">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-312">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-313">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-313">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-314">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-314">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-315">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-315">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-316">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-316">Return Values</span></span>

- <span data-ttu-id="c8f61-317">**NX_SUCCESS** (0x00) http istemcisi silme Isteği iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-317">**NX_SUCCESS** (0x00) Successfully sent HTTP Client DELETE request message</span></span>
- <span data-ttu-id="c8f61-318">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-318">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-319">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-319">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-320">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-320">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-321">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-321">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-322">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-322">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-323">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-323">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="c8f61-324">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-324">Allowed From</span></span>

<span data-ttu-id="c8f61-325">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-325">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-326">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-326">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the DELETE operation on the HTTP Client "my_client." */
status = nx_web_http_client_delete_secure_start_extended(&my_client,
    &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the DELETE request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_get_start"></a><span data-ttu-id="c8f61-327">nx_web_http_client_get_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-327">nx_web_http_client_get_start</span></span>

<span data-ttu-id="c8f61-328">Düz metin HTTP GET isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-328">Start a plaintext HTTP GET request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-329">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-329">Prototype</span></span>

```C
UINT nx_web_http_client_get_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-330">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-330">Description</span></span>

<span data-ttu-id="c8f61-331">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-331">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-332">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-332">This service attempts to GET the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-333">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_web_http_client_response_body_get ()* öğesine birden çok çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-333">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_web_http_client_response_body_get()* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8f61-334">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-334">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-335">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-335">This service is deprecated.</span></span> <span data-ttu-id="c8f61-336">Geliştiricilerin *nx_web_http_client_get_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-336">Developers are encouraged to use *nx_web_http_client_get_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-337">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-337">Input Parameters</span></span>

- <span data-ttu-id="c8f61-338">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-338">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-339">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-339">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-340">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-340">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-341">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-341">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-342">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-342">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-343">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-343">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-344">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-344">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-345">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-345">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-346">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-346">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-347">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-347">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-348">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-348">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-349">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-349">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-350">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-350">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-351">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-351">Return Values</span></span>

- <span data-ttu-id="c8f61-352">**NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-352">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="c8f61-353">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-353">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-354">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-354">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-355">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-355">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-356">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-356">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-357">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-357">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-358">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-358">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-359">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-359">Allowed From</span></span>

<span data-ttu-id="c8f61-360">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-360">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-361">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-361">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    multiple times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_start_extended"></a><span data-ttu-id="c8f61-362">nx_web_http_client_get_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-362">nx_web_http_client_get_start_extended</span></span>

<span data-ttu-id="c8f61-363">Düz metin HTTP GET isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-363">Start a plaintext HTTP GET request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-364">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-364">Prototype</span></span>

```C
UINT nx_web_http_client_get_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-365">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-365">Description</span></span>

<span data-ttu-id="c8f61-366">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-366">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-367">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-367">This service attempts to GET the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-368">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_web_http_client_response_body_get ()* öğesine birden çok çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-368">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_web_http_client_response_body_get()* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8f61-369">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-369">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-370">Kaynak, konak, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-370">The strings of resource, host, username and password must be NULL-terminated, and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-371">Bu hizmet *nx_web_http_client_get_start*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-371">This service replaces *nx_web_http_client_get_start*().</span></span> <span data-ttu-id="c8f61-372">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-372">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-373">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-373">Input Parameters</span></span>

- <span data-ttu-id="c8f61-374">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-374">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-375">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-375">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-376">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-376">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-377">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-377">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-378">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-378">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-379">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-379">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-380">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-380">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-381">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-381">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-382">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-382">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-383">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-383">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-384">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-384">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-385">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-385">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-386">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-386">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-387">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-387">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-388">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-388">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-389">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-389">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-390">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-390">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-391">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-391">Return Values</span></span>

- <span data-ttu-id="c8f61-392">**NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-392">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="c8f61-393">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-393">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-394">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-394">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-395">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-395">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-396">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-396">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-397">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-397">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-398">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-398">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-399">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-399">Allowed From</span></span>

<span data-ttu-id="c8f61-400">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-400">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-401">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-401">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_start_extended(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    multiple times to retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_secure_start"></a><span data-ttu-id="c8f61-402">nx_web_http_client_get_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-402">nx_web_http_client_get_secure_start</span></span>

<span data-ttu-id="c8f61-403">Şifrelenmiş bir HTTPS GET isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-403">Start an encrypted HTTPS GET request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-404">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-404">Prototype</span></span>

```C
UINT nx_web_http_client_get_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
        NX_SECURE_TLS_SESSION *tls_session),
        ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-405">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-405">Description</span></span>

<span data-ttu-id="c8f61-406">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-406">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-407">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-407">This service attempts to GET the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-408">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_web_http_client_response_body_get ()* öğesine birden çok çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-408">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_web_http_client_response_body_get()* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8f61-409">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-409">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-410">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-410">This service is deprecated.</span></span> <span data-ttu-id="c8f61-411">Geliştiricilerin *nx_web_http_client_get_secure_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-411">Developers are encouraged to use *nx_web_http_client_get_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-412">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-412">Input Parameters</span></span>

- <span data-ttu-id="c8f61-413">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-413">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-414">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-414">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-415">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-415">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-416">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-416">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-417">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-417">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-418">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-418">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-419">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-419">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-420">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-420">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-421">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-421">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-422">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-422">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-423">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-423">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-424">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-424">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-425">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-425">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-426">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-426">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-427">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-427">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-428">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-428">Return Values</span></span>

- <span data-ttu-id="c8f61-429">**NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-429">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="c8f61-430">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-430">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-431">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-431">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-432">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-432">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-433">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-433">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-434">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-434">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-435">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-435">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-436">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-436">Allowed From</span></span>

<span data-ttu-id="c8f61-437">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-437">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-438">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-438">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started
    and is so far successful. The client must now call
    *nx_web_http_client_response_body_get()* multiple times to
    retrieve the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_get_secure_start_extended"></a><span data-ttu-id="c8f61-439">nx_web_http_client_get_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-439">nx_web_http_client_get_secure_start_extended</span></span>

<span data-ttu-id="c8f61-440">Şifrelenmiş bir HTTPS GET isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-440">Start an encrypted HTTPS GET request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-441">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-441">Prototype</span></span>

```C
UINT nx_web_http_client_get_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-442">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-442">Description</span></span>

<span data-ttu-id="c8f61-443">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-443">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-444">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağı almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-444">This service attempts to GET the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-445">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen veri paketlerini almak için *nx_web_http_client_response_body_get ()* öğesine birden çok çağrı yapabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-445">If this routine returns NX_SUCCESS, the application can then make multiple calls to *nx_web_http_client_response_body_get()* to retrieve packets of data corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8f61-446">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-446">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-447">Kaynak, konak, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-447">The strings of resource, host, username and password must be NULL-terminated, and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-448">Bu hizmet *nx_web_http_client_secure_start*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-448">This service replaces *nx_web_http_client_secure_start*().</span></span> <span data-ttu-id="c8f61-449">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-449">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-450">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-450">Input Parameters</span></span>

- <span data-ttu-id="c8f61-451">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-451">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-452">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-452">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-453">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-453">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-454">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-454">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-455">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-455">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-456">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-456">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-457">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-457">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-458">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-458">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-459">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-459">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-460">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-460">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-461">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-461">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-462">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-462">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-463">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-463">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-464">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-464">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-465">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-465">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-466">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-466">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-467">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-467">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-468">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-468">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-469">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-469">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-470">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-470">Return Values</span></span>

- <span data-ttu-id="c8f61-471">**NX_SUCCESS** (0x00) http istemcisi al Başlangıç iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-471">**NX_SUCCESS** (0x00) Successfully sent HTTP Client GET start message</span></span>
- <span data-ttu-id="c8f61-472">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-472">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-473">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-473">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-474">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-474">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-475">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-475">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-476">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-476">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-477">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-477">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-478">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-478">Allowed From</span></span>

<span data-ttu-id="c8f61-479">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-479">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-480">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-480">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the GET operation on the HTTP Client "my_client." */
status = nx_web_http_client_get_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM
    is started and is so far successful. The client must now call
    *nx_web_http_client_response_body_get()* multiple times to retrieve
    the content associated with TEST.HTM. */
```

## <a name="nx_web_http_client_head_start"></a><span data-ttu-id="c8f61-481">nx_web_http_client_head_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-481">nx_web_http_client_head_start</span></span>

<span data-ttu-id="c8f61-482">Düz metin HTTP HEAD isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-482">Start a plaintext HTTP HEAD request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-483">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-483">Prototype</span></span>

```C
UINT nx_web_http_client_head_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-484">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-484">Description</span></span>

<span data-ttu-id="c8f61-485">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-485">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-486">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağın baş meta verilerini almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-486">This service attempts to retrieve the HEAD metadata for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-487">Bu yordam NX_SUCCESS döndürürse, uygulama yanıt almak için *nx_web_http_client_response_body_get ()* çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-487">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the response.</span></span>

<span data-ttu-id="c8f61-488">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-488">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-489">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-489">This service is deprecated.</span></span> <span data-ttu-id="c8f61-490">Geliştiricilerin *nx_web_http_client_head_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-490">Developers are encouraged to use *nx_web_http_client_head_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-491">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-491">Input Parameters</span></span>

- <span data-ttu-id="c8f61-492">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-492">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-493">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-493">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-494">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-494">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-495">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-495">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-496">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-496">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-497">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-497">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-498">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-498">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-499">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-499">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-500">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-500">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-501">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-501">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-502">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-502">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-503">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-503">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-504">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-504">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-505">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-505">Return Values</span></span>

- <span data-ttu-id="c8f61-506">**NX_SUCCESS** (0x00) http istemci Head Isteği iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-506">**NX_SUCCESS** (0x00) Successfully sent HTTP Client HEAD request message</span></span>
- <span data-ttu-id="c8f61-507">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-507">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-508">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-508">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-509">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-509">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-510">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-510">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-511">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-511">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-512">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-512">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-513">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-513">Allowed From</span></span>

<span data-ttu-id="c8f61-514">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-514">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-515">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-515">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_head_start_extended"></a><span data-ttu-id="c8f61-516">nx_web_http_client_head_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-516">nx_web_http_client_head_start_extended</span></span>

<span data-ttu-id="c8f61-517">Düz metin HTTP HEAD isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-517">Start a plaintext HTTP HEAD request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-518">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-518">Prototype</span></span>

```C
UINT nx_web_http_client_head_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-519">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-519">Description</span></span>

<span data-ttu-id="c8f61-520">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-520">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-521">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağın baş meta verilerini almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-521">This service attempts to retrieve the HEAD metadata for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-522">Bu yordam NX_SUCCESS döndürürse, uygulama yanıt almak için *nx_web_http_client_response_body_get ()* çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-522">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the response.</span></span>

<span data-ttu-id="c8f61-523">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-523">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-524">Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-524">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-525">Bu hizmet *nx_web_http_client_head_start*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-525">This service replaces *nx_web_http_client_head_start*().</span></span> <span data-ttu-id="c8f61-526">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-526">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-527">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-527">Input Parameters</span></span>

- <span data-ttu-id="c8f61-528">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-528">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-529">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-529">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-530">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-530">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-531">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-531">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-532">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-532">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-533">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-533">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-534">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-534">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-535">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-535">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-536">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-536">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-537">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-537">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-538">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-538">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-539">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-539">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-540">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-540">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-541">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-541">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-542">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-542">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-543">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-543">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-544">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-544">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-545">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-545">Return Values</span></span>

- <span data-ttu-id="c8f61-546">**NX_SUCCESS** (0x00) http istemci Head Isteği iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-546">**NX_SUCCESS** (0x00) Successfully sent HTTP Client HEAD request message</span></span>
- <span data-ttu-id="c8f61-547">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-547">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-548">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-548">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-549">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-549">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-550">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-550">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-551">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-551">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-552">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-552">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-553">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-553">Allowed From</span></span>

<span data-ttu-id="c8f61-554">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-554">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-555">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-555">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the response from the server. */
```

## <a name="nx_web_http_client_head_secure_start"></a><span data-ttu-id="c8f61-556">nx_web_http_client_head_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-556">nx_web_http_client_head_secure_start</span></span>

<span data-ttu-id="c8f61-557">Şifrelenmiş bir HTTPS HEAD isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-557">Start an encrypted HTTPS HEAD request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-558">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-558">Prototype</span></span>

```C
UINT nx_web_http_client_head_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port, CHAR *resource,
    CHAR *host, CHAR *username, CHAR *password,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-559">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-559">Description</span></span>

<span data-ttu-id="c8f61-560">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-560">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-561">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağın baş meta verilerini almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-561">This service attempts to retrieve the HEAD metadata for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-562">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-562">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8f61-563">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-563">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-564">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-564">This service is deprecated.</span></span> <span data-ttu-id="c8f61-565">Geliştiricilerin *nx_web_http_client_head_secure_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-565">Developers are encouraged to use *nx_web_http_client_head_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-566">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-566">Input Parameters</span></span>

- <span data-ttu-id="c8f61-567">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-567">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-568">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-568">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-569">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-569">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-570">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-570">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-571">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-571">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-572">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-572">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-573">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-573">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-574">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-574">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-575">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-575">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-576">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-576">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-577">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-577">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-578">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-578">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-579">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-579">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-580">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-580">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-581">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-581">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-582">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-582">Return Values</span></span>

- <span data-ttu-id="c8f61-583">**NX_SUCCESS** (0x00) http istemci Head Isteği iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-583">**NX_SUCCESS** (0x00) Successfully sent HTTP Client HEAD request message</span></span>
- <span data-ttu-id="c8f61-584">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-584">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-585">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-585">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-586">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-586">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-587">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-587">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-588">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-588">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-589">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-589">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-590">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-590">Allowed From</span></span>

<span data-ttu-id="c8f61-591">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-591">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-592">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-592">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword",
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_head_secure_start_extended"></a><span data-ttu-id="c8f61-593">nx_web_http_client_head_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-593">nx_web_http_client_head_secure_start_extended</span></span>

<span data-ttu-id="c8f61-594">Şifrelenmiş bir HTTPS HEAD isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-594">Start an encrypted HTTPS HEAD request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-595">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-595">Prototype</span></span>

```C
UINT nx_web_http_client_head_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-596">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-596">Description</span></span>

<span data-ttu-id="c8f61-597">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-597">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-598">Bu hizmet, önceden oluşturulan HTTP Istemci örneğinde "kaynak" işaretçisi tarafından belirtilen kaynağın baş meta verilerini almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-598">This service attempts to retrieve the HEAD metadata for the resource specified by "resource" pointer on the previously created HTTP Client instance.</span></span> <span data-ttu-id="c8f61-599">Bu yordam NX_SUCCESS döndürürse, uygulama, istenen kaynak içeriğine karşılık gelen sunucunun yanıtını almak için *nx_web_http_client_response_body_get ()* çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-599">If this routine returns NX_SUCCESS, the application can then call *nx_web_http_client_response_body_get()* to retrieve the server’s response corresponding to the requested resource content.</span></span>

<span data-ttu-id="c8f61-600">Kaynak dizesinin, "/index.htm" gibi bir yerel dosyaya başvuramayacağını veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` http sunucusu, başvuran Get isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-600">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring GET requests.</span></span>

<span data-ttu-id="c8f61-601">Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-601">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-602">Bu hizmet *nx_web_http_client_head_secure_start*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-602">This service replaces *nx_web_http_client_head_secure_start*().</span></span> <span data-ttu-id="c8f61-603">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-603">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-604">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-604">Input Parameters</span></span>

- <span data-ttu-id="c8f61-605">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-605">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-606">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-606">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-607">**SERVER_PORT** Uzak HTTP sunucusundaki bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-607">**server_port** Port on remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-608">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-608">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-609">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-609">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-610">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-610">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-611">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-611">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-612">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-612">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-613">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-613">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-614">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-614">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-615">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-615">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-616">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-616">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-617">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-617">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-618">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-618">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-619">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-619">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-620">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-620">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-621">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-621">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-622">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-622">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-623">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-623">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-624">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-624">Return Values</span></span>

- <span data-ttu-id="c8f61-625">**NX_SUCCESS** (0x00) http istemci Head Isteği iletisi başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-625">**NX_SUCCESS** (0x00) Successfully sent HTTP Client HEAD request message</span></span>
- <span data-ttu-id="c8f61-626">**NX_WEB_HTTP_ERROR** (0x30000) Iç http istemcisi hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-626">**NX_WEB_HTTP_ERROR** (0x30000) Internal HTTP Client error</span></span>
- <span data-ttu-id="c8f61-627">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-627">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-628">**NX_WEB_HTTP_FAILED** (0x30002) http sunucusuyla ILETIŞIM kurarken http istemci hatası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-628">**NX_WEB_HTTP_FAILED** (0x30002) HTTP Client error communicating with the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-629">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-629">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or password.</span></span>
- <span data-ttu-id="c8f61-630">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-630">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-631">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-631">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-632">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-632">Allowed From</span></span>

<span data-ttu-id="c8f61-633">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-633">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-634">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-634">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start the HEAD operation on the HTTP Client "my_client." */
status = nx_web_http_client_head_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1,
    my_tls_setup_function, 1000);

/* If status is NX_SUCCESS, the HEAD request for TEST.HTM is started and is so
    far successful. The client must now call *nx_web_http_client_response_body_get*
    to retrieve the server’s response. */
```

## <a name="nx_web_http_client_request_packet_allocate"></a><span data-ttu-id="c8f61-635">nx_web_http_client_request_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="c8f61-635">nx_web_http_client_request_packet_allocate</span></span>

<span data-ttu-id="c8f61-636">HTTP (S) paketi ayır</span><span class="sxs-lookup"><span data-stu-id="c8f61-636">Allocate a HTTP(S) packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-637">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-637">Prototype</span></span>

```C
UINT nx_web_http_client_request_packet_allocate(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-638">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-638">Description</span></span>

<span data-ttu-id="c8f61-639">Bu hizmet, Istemci HTTP 'Leri için bir paket ayırır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-639">This service attempts to allocates a packet for Client HTTP(S).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-640">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-640">Input Parameters</span></span>

- <span data-ttu-id="c8f61-641">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-641">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-642">**packet_ptr** Ayrılan pakete yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-642">**packet_ptr** Pointer to allocated packet.</span></span>
- <span data-ttu-id="c8f61-643">**wait_option** Paket havuzunda kullanılabilir bir paket yoksa, zaman işaretleri cinsinden bekleme süresini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-643">**wait_option** Defines the wait time in ticks if there are no packets available in the packet pool.</span></span> <span data-ttu-id="c8f61-644">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-644">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-645">**NX_NO_WAIT** (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="c8f61-645">**NX_NO_WAIT** (0x00000000)</span></span>
  - <span data-ttu-id="c8f61-646">**NX_WAIT_FOREVER** (0xffffffff)</span><span class="sxs-lookup"><span data-stu-id="c8f61-646">**NX_WAIT_FOREVER** (0xFFFFFFFF)</span></span>
  - <span data-ttu-id="c8f61-647">**ticks içinde zaman aşımı** (0x00000001-0xfffffffe)</span><span class="sxs-lookup"><span data-stu-id="c8f61-647">**timeout in ticks** (0x00000001 through 0xFFFFFFFE)</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-648">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-648">Return Values</span></span>

- <span data-ttu-id="c8f61-649">**NX_SUCCESS** (0x00) başarılı paket ayırma</span><span class="sxs-lookup"><span data-stu-id="c8f61-649">**NX_SUCCESS** (0x00) Successful packet allocate</span></span>
- <span data-ttu-id="c8f61-650">**NX_NO_PACKET** (0x01) kullanılabilir paket yok</span><span class="sxs-lookup"><span data-stu-id="c8f61-650">**NX_NO_PACKET** (0x01) No packet available</span></span>
- <span data-ttu-id="c8f61-651">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği *tx_thread_wait_abort* bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-651">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="c8f61-652">**NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.</span><span class="sxs-lookup"><span data-stu-id="c8f61-652">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="c8f61-653">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-653">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-654">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-654">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-655">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-655">Allowed From</span></span>

<span data-ttu-id="c8f61-656">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-656">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-657">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-657">Example</span></span>

```C
/* Allocate a packet for HTTP(S) Client and suspend for a maximum of 5 timer
    ticks if the pool is empty. */
status = nx_web_http_client_request_packet_allocate(&my_client, &packet_ptr, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
    variable packet_ptr. */
```

## <a name="nx_web_http_client_post_start"></a><span data-ttu-id="c8f61-658">nx_web_http_client_post_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-658">nx_web_http_client_post_start</span></span>

<span data-ttu-id="c8f61-659">HTTP POST isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-659">Start an HTTP POST request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-660">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-660">Prototype</span></span>

```C
UINT nx_web_http_client_post_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host,
    CHAR *username, CHAR *password,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-661">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-661">Description</span></span>

<span data-ttu-id="c8f61-662">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-662">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-663">Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTP sunucusuna belirtilen kaynağa sahip bir POST isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-663">This service attempts to send a POST request with the specified resource to the HTTP Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8f61-664">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-664">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8f61-665">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-665">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8f61-666">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-666">This service is deprecated.</span></span> <span data-ttu-id="c8f61-667">Geliştiricilerin *nx_web_http_client_post_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-667">Developers are encouraged to use *nx_web_http_client_post_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-668">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-668">Input Parameters</span></span>

- <span data-ttu-id="c8f61-669">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-669">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-670">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-670">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-671">**SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-671">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-672">**kaynak** Sunucuya gönderilen kaynağın URL dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-672">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="c8f61-673">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-673">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-674">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-674">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-675">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-675">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-676">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-676">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-677">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-677">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-678">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-678">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8f61-679">*Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-679">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8f61-680">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-680">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-681">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-681">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-682">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-682">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-683">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-683">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-684">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-684">Return Values</span></span>

- <span data-ttu-id="c8f61-685">**NX_SUCCESS** (0x00) post isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-685">**NX_SUCCESS** (0x00) Successfully sent POST request</span></span>
- <span data-ttu-id="c8f61-686">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-686">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8f61-687">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-687">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-688">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-688">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-689">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="c8f61-689">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8f61-690">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-690">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-691">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-691">Allowed From</span></span>

<span data-ttu-id="c8f61-692">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-692">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-693">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-693">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start an HTTP POST to post the 20-byte resource "/TEST.HTM" to the HTTP Server
    at IP address 1.2.3.5. */
status = nx_web_http_client_post_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_start_extended"></a><span data-ttu-id="c8f61-694">nx_web_http_client_post_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-694">nx_web_http_client_post_start_extended</span></span>

<span data-ttu-id="c8f61-695">HTTP POST isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-695">Start an HTTP POST request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-696">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-696">Prototype</span></span>

```C
UINT nx_web_http_client_post_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-697">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-697">Description</span></span>

<span data-ttu-id="c8f61-698">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-698">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-699">Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTP sunucusuna belirtilen kaynağa sahip bir POST isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-699">This service attempts to send a POST request with the specified resource to the HTTP Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8f61-700">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-700">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8f61-701">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-701">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8f61-702">Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-702">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-703">Bu hizmet *nx_web_http_client_post_start* () yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-703">This service replaces *nx_web_http_client_post_start* ().</span></span> <span data-ttu-id="c8f61-704">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-704">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-705">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-705">Input Parameters</span></span>

- <span data-ttu-id="c8f61-706">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-706">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-707">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-707">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-708">**SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-708">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-709">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-709">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-710">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-710">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-711">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-711">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-712">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-712">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-713">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-713">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-714">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-714">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-715">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-715">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-716">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-716">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-717">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-717">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-718">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-718">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-719">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-719">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8f61-720">*Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-720">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8f61-721">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-721">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-722">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-722">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-723">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-723">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-724">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-724">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-725">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-725">Return Values</span></span>

- <span data-ttu-id="c8f61-726">**NX_SUCCESS** (0x00) post isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-726">**NX_SUCCESS** (0x00) Successfully sent POST request</span></span>
- <span data-ttu-id="c8f61-727">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-727">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8f61-728">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-728">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-729">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-729">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-730">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="c8f61-730">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8f61-731">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-731">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-732">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-732">Allowed From</span></span>

<span data-ttu-id="c8f61-733">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-733">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-734">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-734">Example</span></span>

```C
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

/* Start an HTTP POST to post the 20-byte resource "/TEST.HTM" to the HTTP Server
    at IP address 1.2.3.5. */
status = nx_web_http_client_post_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_secure_start"></a><span data-ttu-id="c8f61-735">nx_web_http_client_post_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-735">nx_web_http_client_post_secure_start</span></span>

<span data-ttu-id="c8f61-736">Şifrelenmiş bir HTTPS POST isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-736">Start an encrypted HTTPS POST request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-737">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-737">Prototype</span></span>

```C
UINT nx_web_http_client_post_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-738">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-738">Description</span></span>

<span data-ttu-id="c8f61-739">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-739">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-740">Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTPS sunucusuna belirtilen kaynağa sahip bir POST isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-740">This service attempts to send a POST request with the specified resource to the HTTPS Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8f61-741">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-741">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8f61-742">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-742">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8f61-743">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-743">This service is deprecated.</span></span> <span data-ttu-id="c8f61-744">Geliştiricilerin *nx_web_http_client_post_secure_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-744">Developers are encouraged to use *nx_web_http_client_post_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-745">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-745">Input Parameters</span></span>

- <span data-ttu-id="c8f61-746">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-746">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-747">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-747">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-748">**SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-748">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-749">**kaynak** Sunucuya gönderilen kaynağın URL dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-749">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="c8f61-750">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-750">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-751">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-751">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-752">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-752">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-753">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-753">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-754">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-754">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-755">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-755">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8f61-756">*Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-756">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8f61-757">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-757">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-758">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-758">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-759">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-759">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-760">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-760">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-761">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-761">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-762">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-762">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-763">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-763">Return Values</span></span>

- <span data-ttu-id="c8f61-764">**NX_SUCCESS** (0x00) post isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-764">**NX_SUCCESS** (0x00) Successfully sent POST request</span></span>
- <span data-ttu-id="c8f61-765">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-765">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8f61-766">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-766">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-767">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-767">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-768">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="c8f61-768">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8f61-769">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-769">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-770">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-770">Allowed From</span></span>

<span data-ttu-id="c8f61-771">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-771">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-772">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-772">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_post_secure_start_extended"></a><span data-ttu-id="c8f61-773">nx_web_http_client_post_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-773">nx_web_http_client_post_secure_start_extended</span></span>

<span data-ttu-id="c8f61-774">Şifrelenmiş bir HTTPS POST isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-774">Start an encrypted HTTPS POST request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-775">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-775">Prototype</span></span>

```C
UINT nx_web_http_client_post_secure_start_extended(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-776">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-776">Description</span></span>

<span data-ttu-id="c8f61-777">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-777">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-778">Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTPS sunucusuna belirtilen kaynağa sahip bir POST isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-778">This service attempts to send a POST request with the specified resource to the HTTPS Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8f61-779">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-779">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8f61-780">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-780">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8f61-781">Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-781">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-782">Bu hizmet *nx_web_http_client_post_secure_start* () yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-782">This service replaces *nx_web_http_client_post_secure_start* ().</span></span> <span data-ttu-id="c8f61-783">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-783">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-784">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-784">Input Parameters</span></span>

- <span data-ttu-id="c8f61-785">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-785">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-786">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-786">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-787">**SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-787">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-788">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-788">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-789">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-789">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-790">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-790">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-791">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-791">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-792">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-792">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-793">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-793">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-794">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-794">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-795">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-795">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-796">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-796">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-797">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-797">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-798">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-798">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8f61-799">*Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-799">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8f61-800">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-800">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-801">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-801">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-802">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-802">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-803">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-803">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-804">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-804">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-805">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-805">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-806">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-806">Return Values</span></span>

- <span data-ttu-id="c8f61-807">**NX_SUCCESS** (0x00) post isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-807">**NX_SUCCESS** (0x00) Successfully sent POST request</span></span>
- <span data-ttu-id="c8f61-808">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-808">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8f61-809">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-809">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-810">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-810">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-811">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="c8f61-811">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8f61-812">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-812">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-813">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-813">Allowed From</span></span>

<span data-ttu-id="c8f61-814">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-814">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-815">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-815">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the POST operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_start"></a><span data-ttu-id="c8f61-816">nx_web_http_client_put_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-816">nx_web_http_client_put_start</span></span>

<span data-ttu-id="c8f61-817">HTTP PUT isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-817">Start an HTTP PUT request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-818">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-818">Prototype</span></span>

```C
UINT nx_web_http_client_put_start(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-819">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-819">Description</span></span>

<span data-ttu-id="c8f61-820">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-820">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-821">Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTP sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-821">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8f61-822">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-822">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8f61-823">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-823">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8f61-824">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-824">This service is deprecated.</span></span> <span data-ttu-id="c8f61-825">Geliştiricilerin *nx_web_http_client_put_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-825">Developers are encouraged to use *nx_web_http_client_put_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-826">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-826">Input Parameters</span></span>

- <span data-ttu-id="c8f61-827">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-827">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-828">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-828">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-829">**SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-829">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-830">**kaynak** Sunucuya gönderilen kaynağın URL dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-830">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="c8f61-831">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-831">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-832">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-832">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-833">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-833">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-834">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-834">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-835">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-835">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-836">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-836">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8f61-837">*Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-837">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8f61-838">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-838">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-839">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-839">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-840">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-840">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-841">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-841">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-842">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-842">Return Values</span></span>

- <span data-ttu-id="c8f61-843">**NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-843">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="c8f61-844">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-844">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8f61-845">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-845">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-846">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-846">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-847">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="c8f61-847">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8f61-848">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-848">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-849">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-849">Allowed From</span></span>

<span data-ttu-id="c8f61-850">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-850">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-851">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-851">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTP Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_start(&my_client, &server_ip_addr,
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_start_extended"></a><span data-ttu-id="c8f61-852">nx_web_http_client_put_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-852">nx_web_http_client_put_start_extended</span></span>

<span data-ttu-id="c8f61-853">HTTP PUT isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-853">Start an HTTP PUT request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-854">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-854">Prototype</span></span>

```C
UINT nx_web_http_client_put_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length,
    ULONG total_bytes, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-855">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-855">Description</span></span>

<span data-ttu-id="c8f61-856">Bu yöntem **düz metin** http içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-856">This method is for **plaintext** HTTP.</span></span>

<span data-ttu-id="c8f61-857">Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTP sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-857">This service attempts to send a PUT request with the specified resource to the HTTP Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8f61-858">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-858">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8f61-859">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-859">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8f61-860">Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-860">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-861">Bu hizmet *nx_web_http_client_put_start* () yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-861">This service replaces *nx_web_http_client_put_start* ().</span></span> <span data-ttu-id="c8f61-862">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-862">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-863">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-863">Input Parameters</span></span>

- <span data-ttu-id="c8f61-864">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-864">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-865">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-865">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-866">**SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-866">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-867">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-867">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-868">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-868">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-869">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-869">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-870">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-870">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-871">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-871">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-872">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-872">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-873">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-873">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-874">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-874">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-875">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-875">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-876">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-876">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-877">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-877">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8f61-878">*Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-878">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8f61-879">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-879">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-880">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-880">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-881">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-881">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-882">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-882">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-883">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-883">Return Values</span></span>

- <span data-ttu-id="c8f61-884">**NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-884">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="c8f61-885">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-885">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8f61-886">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-886">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-887">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-887">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-888">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="c8f61-888">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8f61-889">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-889">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-890">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-890">Allowed From</span></span>

<span data-ttu-id="c8f61-891">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-891">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-892">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-892">Example</span></span>

```c
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTP Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_secure_start"></a><span data-ttu-id="c8f61-893">nx_web_http_client_put_secure_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-893">nx_web_http_client_put_secure_start</span></span>

<span data-ttu-id="c8f61-894">Şifrelenmiş bir HTTPS PUT isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-894">Start an encrypted HTTPS PUT request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-895">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-895">Prototype</span></span>

```C
UINT nx_web_http_client_put_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS ip_address, UINT server_port,
    CHAR *resource, CHAR *host, CHAR *username,
    CHAR *password, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-896">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-896">Description</span></span>

<span data-ttu-id="c8f61-897">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-897">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-898">Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTPS sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-898">This service attempts to send a PUT request with the specified resource to the HTTPS Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8f61-899">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-899">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8f61-900">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-900">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8f61-901">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-901">This service is deprecated.</span></span> <span data-ttu-id="c8f61-902">Geliştiricilerin *nx_web_http_client_put_secure_start_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-902">Developers are encouraged to use *nx_web_http_client_put_secure_start_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-903">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-903">Input Parameters</span></span>

- <span data-ttu-id="c8f61-904">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-904">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-905">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-905">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-906">**SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-906">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-907">**kaynak** Sunucuya gönderilen kaynağın URL dizesi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-907">**resource** Pointer to URL string for resource to send to Server.</span></span>
- <span data-ttu-id="c8f61-908">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-908">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-909">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-909">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-910">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-910">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-911">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-911">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-912">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-912">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-913">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-913">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8f61-914">*Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-914">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8f61-915">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-915">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-916">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-916">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-917">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-917">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-918">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-918">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-919">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-919">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-920">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-920">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-921">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-921">Return Values</span></span>

- <span data-ttu-id="c8f61-922">**NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-922">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="c8f61-923">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-923">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8f61-924">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-924">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-925">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-925">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-926">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="c8f61-926">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8f61-927">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-927">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-928">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-928">Allowed From</span></span>

<span data-ttu-id="c8f61-929">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-929">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-930">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-930">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, "/TEST.HTM",
    "host.com", "myname", "mypassword", 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_secure_start_extended"></a><span data-ttu-id="c8f61-931">nx_web_http_client_put_secure_start_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-931">nx_web_http_client_put_secure_start_extended</span></span>

<span data-ttu-id="c8f61-932">Şifrelenmiş bir HTTPS PUT isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-932">Start an encrypted HTTPS PUT request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-933">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-933">Prototype</span></span>

```C
UINT nx_web_http_client_put_secure_start(
    NX_WEB_HTTP_CLIENT *client_ptr, NXD_ADDRESS ip_address,
    UINT server_port, CHAR *resource, UINT resource_length,
    CHAR *host, UINT host_length, CHAR *username,
    UINT username_length, CHAR *password, UINT password_length, ULONG total_bytes,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls_session),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-934">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-934">Description</span></span>

<span data-ttu-id="c8f61-935">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-935">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-936">Bu hizmet, belirtilen IP adresi ve bağlantı noktasındaki HTTPS sunucusuna belirtilen kaynağa sahip bir PUT isteği gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-936">This service attempts to send a PUT request with the specified resource to the HTTPS Server at the supplied IP address and port.</span></span> <span data-ttu-id="c8f61-937">Bu yordam başarılı olursa, uygulama kodu kaynak içeriğini HTTP sunucusuna göndermek için *nx_web_http_client_put_packet ()* yordamına art arda çağrılar yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-937">If this routine is successful, the application code should make successive calls to the *nx_web_http_client_put_packet()* routine to send the resource contents to the HTTP Server.</span></span>

<span data-ttu-id="c8f61-938">Kaynak dizesinin yerel bir dosyaya (örneğin, "/index.htm") başvurabilir veya başka bir URL 'ye başvuramayacağını unutmayın, örneğin `http://abc.website.com/index.htm` , http sunucusu başvuran put isteklerini desteklediğini gösteriyorsa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-938">Note that the resource string can refer to a local file e.g. "/index.htm" or it can refer to another URL e.g. `http://abc.website.com/index.htm` if the HTTP Server indicates it supports referring PUT requests.</span></span>

<span data-ttu-id="c8f61-939">Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-939">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-940">Bu hizmet *nx_web_http_client_put_secure_start*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-940">This service replaces *nx_web_http_client_put_secure_start*().</span></span> <span data-ttu-id="c8f61-941">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-941">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-942">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-942">Input Parameters</span></span>

- <span data-ttu-id="c8f61-943">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-943">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-944">**ip_address** HTTP sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-944">**ip_address** IP address of the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-945">**SERVER_PORT** Uzak HTTP sunucusundaki TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-945">**server_port** TCP port on the remote HTTP Server.</span></span>
- <span data-ttu-id="c8f61-946">**kaynak** İstenen kaynak için URL dizesine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-946">**resource** Pointer to URL string for requested resource.</span></span>
- <span data-ttu-id="c8f61-947">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-947">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-948">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-948">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-949">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-949">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-950">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-950">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-951">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-951">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-952">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-952">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-953">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-953">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-954">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-954">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-955">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-955">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-956">**total_bytes** Gönderilen toplam kaynak bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-956">**total_bytes** Total bytes of resource being sent.</span></span> <span data-ttu-id="c8f61-957">*Nx_web_http_client_put_packet ()* için sonraki çağrılar aracılığıyla gönderilen tüm paketlerin toplam uzunluğunun bu değere eşit olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-957">Note that the combined length of all packets sent via subsequent calls to *nx_web_http_client_put_packet()* must equal this value.</span></span>
- <span data-ttu-id="c8f61-958">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-958">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-959">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-959">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-960">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-960">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-961">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-961">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-962">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-962">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-963">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-963">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-964">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-964">Return Values</span></span>

- <span data-ttu-id="c8f61-965">**NX_SUCCESS** (0x00) PUT isteği başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-965">**NX_SUCCESS** (0x00) Successfully sent PUT request</span></span>
- <span data-ttu-id="c8f61-966">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Kullanıcı adı arabellek için çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-966">**NX_WEB_HTTP_USERNAME_TOO_LONG** (0x30012) Username too large for buffer</span></span>
- <span data-ttu-id="c8f61-967">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-967">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-968">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-968">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-969">NX_SIZE_ERROR (0x09) Toplam kaynak boyutu geçersiz</span><span class="sxs-lookup"><span data-stu-id="c8f61-969">NX_SIZE_ERROR (0x09) Invalid total size of resource</span></span>
- <span data-ttu-id="c8f61-970">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-970">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-971">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-971">Allowed From</span></span>

<span data-ttu-id="c8f61-972">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-972">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-973">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-973">Example</span></span>

```C
/* Start an HTTP PUT to place the 20-byte resource "/TEST.HTM" on the HTTPS Server
    at IP address 1.2.3.5. */

/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

status = nx_web_http_client_put_secure_start_extended(&my_client,
    &server_ip_addr, NX_WEB_HTTPS_SERVER_PORT,
    "/TEST.HTM", sizeof("/TEST.HTM") – 1,
    "host.com", sizeof("host.com") – 1,
    "myname", sizeof("myname") – 1,
    "mypassword", sizeof("mypassword") – 1, 20,
    tls_setup, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully been
    started. */
```

## <a name="nx_web_http_client_put_packet"></a><span data-ttu-id="c8f61-974">nx_web_http_client_put_packet</span><span class="sxs-lookup"><span data-stu-id="c8f61-974">nx_web_http_client_put_packet</span></span>

<span data-ttu-id="c8f61-975">Sonraki kaynak veri paketini gönder</span><span class="sxs-lookup"><span data-stu-id="c8f61-975">Send next resource data packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-976">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-976">Prototype</span></span>

```C
UINT nx_web_http_client_put_packet(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET *packet_ptr, ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-977">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-977">Description</span></span>

<span data-ttu-id="c8f61-978">Bu hizmet, kaynak içeriğinin bir sonraki paketini hem PUT hem de POST işlemleri için HTTP sunucusuna gönderme girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-978">This service attempts to send the next packet of resource content to the HTTP Server for both PUT and POST operations.</span></span> <span data-ttu-id="c8f61-979">Gönderilen paketlerin Birleşik uzunluğu önceki *nx_web_http_client_put_start ()* veya *nx_web_http_client_post_start ()* çağrısında (veya bunlara karşılık gelen güvenli sürümlerde) belirtilen "total_bytes" değerine eşit olana kadar bu yordamın kaldı olarak çağrılması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-979">Note that this routine should be called repetitively until the combined length of the packets sent equals the "total_bytes" specified in the previous *nx_web_http_client_put_start()* or *nx_web_http_client_post_start()* call (or their corresponding secure versions).</span></span>

<span data-ttu-id="c8f61-980">Bu hizmet, HTTP (veya HTTPS) bağlantısı kurulurken bir sorun olması durumunda sunucudan bir yanıt olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-980">This service also checks for a response from the server in case there was a problem establishing the HTTP (or HTTPS) connection.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-981">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-981">Input Parameters</span></span>

- <span data-ttu-id="c8f61-982">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-982">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-983">**packet_ptr** HTTP sunucusuna gönderilen kaynağın bir sonraki içeriğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-983">**packet_ptr** Pointer to next content of the resource to being sent to the HTTP Server.</span></span>
- <span data-ttu-id="c8f61-984">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-984">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-985">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-985">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-986">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-986">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-987">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-987">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-988">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-988">Return Values</span></span>

- <span data-ttu-id="c8f61-989">**NX_SUCCESS** (0x00) http Istemci paketini başarıyla gönderdi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-989">**NX_SUCCESS** (0x00) Successfully sent HTTP Client packet.</span></span>
- <span data-ttu-id="c8f61-990">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-990">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not ready</span></span>
- <span data-ttu-id="c8f61-991">**NX_WEB_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0x3000e) alınan sunucu hata kodu \* \*</span><span class="sxs-lookup"><span data-stu-id="c8f61-991">**NX_WEB_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0x3000E) Received Server error code\*\*</span></span>
- <span data-ttu-id="c8f61-992">**NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000d) geçersiz paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="c8f61-992">**NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000D) Invalid packet length</span></span>
- <span data-ttu-id="c8f61-993">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000b) geçersiz ad ve/veya parola</span><span class="sxs-lookup"><span data-stu-id="c8f61-993">**NX_WEB_HTTP_AUTHENTICATION_ERROR** (0x3000B) Invalid name and/or Password</span></span>
- <span data-ttu-id="c8f61-994">**NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000f) sunucu, put tamamlanmadan önce yanıt veriyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-994">**NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000F) Server responds before PUT is complete</span></span>
- <span data-ttu-id="c8f61-995">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-995">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-996">NX_INVALID_PACKET (0x12) paketi TCP üst bilgisi için çok küçük</span><span class="sxs-lookup"><span data-stu-id="c8f61-996">NX_INVALID_PACKET (0x12) Packet too small for TCP header</span></span>
- <span data-ttu-id="c8f61-997">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-997">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-998">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-998">Allowed From</span></span>

<span data-ttu-id="c8f61-999">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-999">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1000">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1000">Example</span></span>

```C
/* Send a 20-byte packet representing the content of the resource
    "/TEST.HTM" to the HTTP Server. */

status = nx_web_http_client_put_packet(&client_ptr, packet_ptr, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM has
    successfully been sent. */
```

## <a name="nx_web_http_client_request_chunked_set"></a><span data-ttu-id="c8f61-1001">nx_web_http_client_request_chunked_set</span><span class="sxs-lookup"><span data-stu-id="c8f61-1001">nx_web_http_client_request_chunked_set</span></span>

<span data-ttu-id="c8f61-1002">HTTP (S) isteği için öbekli aktarım ayarla</span><span class="sxs-lookup"><span data-stu-id="c8f61-1002">Set chunked transfer for HTTP(S) request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1003">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1003">Prototype</span></span>

```C
UINT nx_web_http_client_request_chunked_set(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT chunk_size, NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="c8f61-1004">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1004">Description</span></span>

<span data-ttu-id="c8f61-1005">Bu hizmet, daha önce uzak ana bilgisayara soket bağlantısı oluşturmuş olan *nx_web_http_client_connect ()* veya *nx_web_http_client_secure_connect ()* çağrısında BELIRTILEN sunucuya özel bir http (S) isteği göndermek için öbekli aktarım kodlamasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1005">This service uses chunked transfer coding to send a custom HTTP(S) request to the server specified in the *nx_web_http_client_connect()* or *nx_web_http_client_secure_connect()* call which has previously established the socket connection to the remote host.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-1006">Uygulama, istek veri paketi göndermek için öbekli aktarım kodlaması kullanıyorsa, *nx_web_http_client_request_packet_allocate*() çağrıldıktan sonra ve *nx_web_http_client_reqeust_packet_send* () çağrısından önce bu hizmeti çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1006">If the application uses chunked transfer coding to send a request data packet, it must call this service after calling *nx_web_http_client_request_packet_allocate*(), and before call *nx_web_http_client_reqeust_packet_send* ().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1007">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1007">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1008">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1008">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-1009">**chunk_size** Öbek verilerinin sekizli cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1009">**chunk_size** Size of the chunk-data in octets.</span></span>
- <span data-ttu-id="c8f61-1010">**packet_ptr** HTTP (S) istek veri paketi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1010">**packet_ptr** HTTP(S) request data packet pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1011">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1011">Return Values</span></span>

- <span data-ttu-id="c8f61-1012">**NX_SUCCESS** (0x00) yığını başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1012">**NX_SUCCESS** (0x00) Successfully set chunked.</span></span>
- <span data-ttu-id="c8f61-1013">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1013">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1014">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1014">Allowed From</span></span>

<span data-ttu-id="c8f61-1015">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1015">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1016">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1016">Example</span></span>

```C
/* Connect to a remote HTTPS server. */

nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a PUT request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_PUT, "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_TRUE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the PUT operation. */
nx_web_http_client_request_send(&my_client, 1000);

/* Create a new data packet request on the HTTP(S) client instance. */
nx_web_http_client_request_packet_allocate(&my_client,
    &my_packet,
    NX_WAIT_FOREVER);

/* Set the chunked transfer. */
status = nx_web_http_client_request_chunked_set(&my_client, 128, my_packet);

/* At this point, user can fill the data into my_packet. *./
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet request to server. */
nx_web_http_client_request_packet_send(&my_client, my_packet,
    0, NX_WAIT_FOREVER);
```

## <a name="nx_web_http_client_request_header_add"></a><span data-ttu-id="c8f61-1017">nx_web_http_client_request_header_add</span><span class="sxs-lookup"><span data-stu-id="c8f61-1017">nx_web_http_client_request_header_add</span></span>

<span data-ttu-id="c8f61-1018">Özel bir HTTP isteğine özel üst bilgi ekleme</span><span class="sxs-lookup"><span data-stu-id="c8f61-1018">Add a custom header to a custom HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1019">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1019">Prototype</span></span>

```C
UINT nx_web_http_client_request_header_add(
    NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *field_name, UINT name_length,
    CHAR *field_value, UINT value_length,
    UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-1020">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1020">Description</span></span>

<span data-ttu-id="c8f61-1021">Bu hizmet, n *x_web_http_client_request_initialize ()* ile oluşturulan özel bir HTTP isteğine özel bir üst bilgi (alan adı ve değeri biçiminde) ekler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1021">This service adds a custom header (in the form of a field name and value) to a custom HTTP request created with n *x_web_http_client_request_initialize()*.</span></span>

<span data-ttu-id="c8f61-1022">Bu hizmetin kullanılması, bir uygulamanın isteğe herhangi sayıda özel üst bilgi eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1022">Use of this service enables an application to add any number of custom headers to the request.</span></span> <span data-ttu-id="c8f61-1023">**Bu, belirli uygulamalar için tasarlanan özelleştirilmiş HTTP isteklerine izin verir.**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1023">**This allows for customized HTTP requests intended for specific applications.**</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-1024">Nx_web_http_client_ \* _start yöntemleri kolaylık sağlaması için verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1024">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8f61-1025">Bu işlevlerin tümü bu yordamı, HTTP istekleri oluşturmak ve göndermek için dahili olarak ( *nx_web_http_client_request_initialize ()* ile birlikte kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1025">These functions all use this routine internally (along with *nx_web_http_client_request_initialize())* to create and send HTTP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1026">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1026">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1027">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1027">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-1028">**field_name** Alan adı dizesi (örn. "Content-Type").</span><span class="sxs-lookup"><span data-stu-id="c8f61-1028">**field_name** Field name string (e.g. "Content-Type").</span></span>
- <span data-ttu-id="c8f61-1029">**name_length** Alan adı dizesinin bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1029">**name_length** Length of field name string in bytes.</span></span>
- <span data-ttu-id="c8f61-1030">**field_value** Alan değeri dizesi (ör. "Application/sekizli-Stream").</span><span class="sxs-lookup"><span data-stu-id="c8f61-1030">**field_value** Field value string (e.g. "application/octet-stream").</span></span>
- <span data-ttu-id="c8f61-1031">**value_length** Bayt cinsinden değer dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1031">**value_length** Length of value string in bytes.</span></span>
- <span data-ttu-id="c8f61-1032">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1032">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-1033">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1033">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1034">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1034">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-1035">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1035">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1036">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1036">Return Values</span></span>

- <span data-ttu-id="c8f61-1037">**NX_SUCCESS** (0x00) isteğin üst bilgisinin başarıyla eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1037">**NX_SUCCESS** (0x00) Successful addition of header to request.</span></span>
- <span data-ttu-id="c8f61-1038">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1038">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1039">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1039">Allowed From</span></span>

<span data-ttu-id="c8f61-1040">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1040">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1041">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1041">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */

nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server
    by repeatedly calling *nx_web_http_client_response_body_get()*
    until the entire response is retrieved. *./

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_initialize"></a><span data-ttu-id="c8f61-1042">nx_web_http_client_request_initialize</span><span class="sxs-lookup"><span data-stu-id="c8f61-1042">nx_web_http_client_request_initialize</span></span>

<span data-ttu-id="c8f61-1043">Özel bir HTTP isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1043">Initialize a custom HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1044">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1044">Prototype</span></span>

```C
UINT nx_web_http_client_request_initialize(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT method, CHAR *resource, CHAR *host,
    UINT input_size, UINT transfer_encoding_trunked,
    CHAR *username, CHAR *password, UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-1045">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1045">Description</span></span>

<span data-ttu-id="c8f61-1046">Bu hizmet özel bir HTTP isteği oluşturur ve bunu HTTP Istemci örneğiyle ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1046">This service creates a custom HTTP request and associates it with the HTTP Client instance.</span></span> <span data-ttu-id="c8f61-1047">Daha basit *nx_web_http_client_get_start ()* aksine (Bu API 'nin put, post ve ilişkili güvenli sürümlerinin yanı sıra), *nx_web_http_client_request_send ()* hizmeti çağrılana kadar özel istek gönderilmez.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1047">Unlike the simpler *nx_web_http_client_get_start()* (along with the methods for PUT, POST, and the associated secure versions of those API), the custom request is not sent until the *nx_web_http_client_request_send()* service is called.</span></span>

<span data-ttu-id="c8f61-1048">Bu hizmetin kullanılması, bir uygulamanın ***nx_web_http_client_request_header_add ()*** hizmetini kullanarak isteğe herhangi bir sayıda özel üst bilgi eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1048">Use of this service enables an application to add any number of custom headers to the request using the ***nx_web_http_client_request_header_add()*** service.</span></span> <span data-ttu-id="c8f61-1049">Bu, belirli uygulamalar için tasarlanan özelleştirilmiş HTTP isteklerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1049">This allows for customized HTTP requests intended for specific applications.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-1050">Nx_web_http_client_ \* _start yöntemleri kolaylık sağlaması için verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1050">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8f61-1051">Bu işlevlerin tümü bu yordamı, HTTP istekleri oluşturmak ve göndermek için dahili olarak ( *nx_web_http_client_request_send ()* ile birlikte kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1051">These functions all use this routine internally (along with *nx_web_http_client_request_send())* to create and send HTTP requests.</span></span>

<span data-ttu-id="c8f61-1052">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1052">This service is deprecated.</span></span> <span data-ttu-id="c8f61-1053">Geliştiricilerin *nx_web_http_client_request_initialize_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1053">Developers are encouraged to use *nx_web_http_client_request_initialize_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1054">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1054">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1055">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1055">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-1056">**yöntemi** Kullanılacak HTTP istek yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1056">**method** The HTTP request method to use.</span></span> <span data-ttu-id="c8f61-1057">Seçenekler aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1057">The options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1058">**NX_WEB_HTTP_METHOD_NONE (0x0)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1058">**NX_WEB_HTTP_METHOD_NONE (0x0)**</span></span>
  - <span data-ttu-id="c8f61-1059">**NX_WEB_HTTP_METHOD_GET (0x1)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1059">**NX_WEB_HTTP_METHOD_GET (0x1)**</span></span>
  - <span data-ttu-id="c8f61-1060">**NX_WEB_HTTP_METHOD_PUT (0x2)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1060">**NX_WEB_HTTP_METHOD_PUT (0x2)**</span></span>
  - <span data-ttu-id="c8f61-1061">**NX_WEB_HTTP_METHOD_POST (0x3)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1061">**NX_WEB_HTTP_METHOD_POST (0x3)**</span></span>
  - <span data-ttu-id="c8f61-1062">**NX_WEB_HTTP_METHOD_DELETE (0x4)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1062">**NX_WEB_HTTP_METHOD_DELETE (0x4)**</span></span>
  - <span data-ttu-id="c8f61-1063">**NX_WEB_HTTP_METHOD_HEAD (0x5)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1063">**NX_WEB_HTTP_METHOD_HEAD (0x5)**</span></span>
- <span data-ttu-id="c8f61-1064">**kaynak** Aktarılmakta olan kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1064">**resource** Name of resource being transferred.</span></span>
- <span data-ttu-id="c8f61-1065">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1065">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-1066">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1066">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-1067">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1067">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-1068">**input_size** PUT ve POST için giriş verilerinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1068">**input_size** Size of input data for PUT and POST.</span></span> <span data-ttu-id="c8f61-1069">Diğer işlemler için 0 geçirin.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1069">Pass 0 for other operations.</span></span>
- <span data-ttu-id="c8f61-1070">**transfer_encoding_trunked** Gelecekteki santrale Aktarım desteği için ayrılmış parametre.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1070">**transfer_encoding_trunked** Reserved parameter for future trunked transfer support.</span></span>
- <span data-ttu-id="c8f61-1071">**Kullanıcı adı** Korunan kaynaklar için Kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1071">**username** Username for protected resources.</span></span>
- <span data-ttu-id="c8f61-1072">**parola** Korumalı kaynaklar için parola.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1072">**password** Password for protected resources.</span></span>
- <span data-ttu-id="c8f61-1073">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1073">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-1074">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1074">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1075">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1075">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-1076">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1076">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1077">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1077">Return Values</span></span>

- <span data-ttu-id="c8f61-1078">**NX_SUCCESS** (0x00) isteğin başarıyla başlatılması.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1078">**NX_SUCCESS** (0x00) Successful initialization of request.</span></span>
- <span data-ttu-id="c8f61-1079">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1079">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1080">NX_WEB_HTTP_METHOD_ERROR (0x30014) bazı gerekli bilgiler eksikti (ör. PUT veya POST için input_size).</span><span class="sxs-lookup"><span data-stu-id="c8f61-1080">NX_WEB_HTTP_METHOD_ERROR (0x30014) Some required information was missing (e.g. input_size for PUT or POST).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1081">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1081">Allowed From</span></span>

<span data-ttu-id="c8f61-1082">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1082">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1083">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1083">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "test.txt ", "host.com",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */

status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get()* until the entire response is retrieved. *./
get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_initialize_extended"></a><span data-ttu-id="c8f61-1084">nx_web_http_client_request_initialize_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-1084">nx_web_http_client_request_initialize_extended</span></span>

<span data-ttu-id="c8f61-1085">Özel bir HTTP isteği başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1085">Initialize a custom HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1086">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1086">Prototype</span></span>

```C
UINT nx_web_http_client_request_initialize(
    NX_WEB_HTTP_CLIENT *client_ptr,
    UINT method, CHAR *resource, CHAR *host,
    UINT input_size, UINT transfer_encoding_trunked,
    CHAR *username, CHAR *password, UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-1087">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1087">Description</span></span>

<span data-ttu-id="c8f61-1088">Bu hizmet özel bir HTTP isteği oluşturur ve bunu HTTP Istemci örneğiyle ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1088">This service creates a custom HTTP request and associates it with the HTTP Client instance.</span></span> <span data-ttu-id="c8f61-1089">Daha basit *nx_web_http_client_get_start ()* aksine (Bu API 'nin put, post ve ilişkili güvenli sürümlerinin yanı sıra), *nx_web_http_client_request_send ()* hizmeti çağrılana kadar özel istek gönderilmez.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1089">Unlike the simpler *nx_web_http_client_get_start()* (along with the methods for PUT, POST, and the associated secure versions of those API), the custom request is not sent until the *nx_web_http_client_request_send()* service is called.</span></span>

<span data-ttu-id="c8f61-1090">Bu hizmetin kullanılması, bir uygulamanın ***nx_web_http_client_request_header_add ()*** hizmetini kullanarak isteğe herhangi bir sayıda özel üst bilgi eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1090">Use of this service enables an application to add any number of custom headers to the request using the ***nx_web_http_client_request_header_add()*** service.</span></span> <span data-ttu-id="c8f61-1091">Bu, belirli uygulamalar için tasarlanan özelleştirilmiş HTTP isteklerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1091">This allows for customized HTTP requests intended for specific applications.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-1092">Nx_web_http_client_ \* _start yöntemleri kolaylık sağlaması için verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1092">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8f61-1093">Bu işlevlerin tümü bu yordamı, HTTP istekleri oluşturmak ve göndermek için dahili olarak ( *nx_web_http_client_request_send ()* ile birlikte kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1093">These functions all use this routine internally (along with *nx_web_http_client_request_send())* to create and send HTTP requests.</span></span>

<span data-ttu-id="c8f61-1094">Kaynak, ana bilgisayar, Kullanıcı adı ve parola dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1094">The strings of resource, host, username and password must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-1095">Bu hizmet *nx_web_http_client_request_initialize*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1095">This service replaces *nx_web_http_client_request_initialize*().</span></span> <span data-ttu-id="c8f61-1096">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1096">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1097">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1097">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1098">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1098">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-1099">**yöntemi** Kullanılacak HTTP istek yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1099">**method** The HTTP request method to use.</span></span> <span data-ttu-id="c8f61-1100">Seçenekler aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1100">The options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1101">**NX_WEB_HTTP_METHOD_NONE (0x0)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1101">**NX_WEB_HTTP_METHOD_NONE (0x0)**</span></span>
  - <span data-ttu-id="c8f61-1102">**NX_WEB_HTTP_METHOD_GET (0x1)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1102">**NX_WEB_HTTP_METHOD_GET (0x1)**</span></span>
  - <span data-ttu-id="c8f61-1103">**NX_WEB_HTTP_METHOD_PUT (0x2)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1103">**NX_WEB_HTTP_METHOD_PUT (0x2)**</span></span>
  - <span data-ttu-id="c8f61-1104">**NX_WEB_HTTP_METHOD_POST (0x3)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1104">**NX_WEB_HTTP_METHOD_POST (0x3)**</span></span>
  - <span data-ttu-id="c8f61-1105">**NX_WEB_HTTP_METHOD_DELETE (0x4)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1105">**NX_WEB_HTTP_METHOD_DELETE (0x4)**</span></span>
  - <span data-ttu-id="c8f61-1106">**NX_WEB_HTTP_METHOD_HEAD (0x5)**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1106">**NX_WEB_HTTP_METHOD_HEAD (0x5)**</span></span>
- <span data-ttu-id="c8f61-1107">**kaynak** Aktarılmakta olan kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1107">**resource** Name of resource being transferred.</span></span>
- <span data-ttu-id="c8f61-1108">**resource_length** İstenen kaynağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1108">**resource_length** String length of requested resource.</span></span>
- <span data-ttu-id="c8f61-1109">**ana bilgisayar** Sunucunun etki alanı adının null ile sonlandırılmış dizesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1109">**host** Null-terminated string of the server’s domain name.</span></span> <span data-ttu-id="c8f61-1110">Bu dize HTTP ana bilgisayar üst bilgisi alanında iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1110">This string is transmitted in the HTTP Host header field.</span></span> <span data-ttu-id="c8f61-1111">Ana bilgisayar dizesi NULL olamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1111">The host string cannot be NULL.</span></span>
- <span data-ttu-id="c8f61-1112">**host_length** Konağın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1112">**host_length** String length of host.</span></span>
- <span data-ttu-id="c8f61-1113">**input_size** PUT ve POST için giriş verilerinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1113">**input_size** Size of input data for PUT and POST.</span></span> <span data-ttu-id="c8f61-1114">Diğer işlemler için 0 geçirin.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1114">Pass 0 for other operations.</span></span>
- <span data-ttu-id="c8f61-1115">**transfer_encoding_trunked** Gelecekteki santrale Aktarım desteği için ayrılmış parametre.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1115">**transfer_encoding_trunked** Reserved parameter for future trunked transfer support.</span></span>
- <span data-ttu-id="c8f61-1116">**Kullanıcı adı** Kimlik doğrulaması için isteğe bağlı kullanıcı adına işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1116">**username** Pointer to optional user name for authentication.</span></span>
- <span data-ttu-id="c8f61-1117">**username_length** Kimlik doğrulaması için Kullanıcı adının dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1117">**username_length** String length of user name for authentication.</span></span>
- <span data-ttu-id="c8f61-1118">**parola** Kimlik doğrulaması için isteğe bağlı parola işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1118">**password** Pointer to optional password for authentication.</span></span>
- <span data-ttu-id="c8f61-1119">**password_length** Kimlik doğrulaması için parolanın dize uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1119">**password_length** String length of password for authentication.</span></span>
- <span data-ttu-id="c8f61-1120">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1120">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-1121">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1121">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1122">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1122">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-1123">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1123">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1124">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1124">Return Values</span></span>

- <span data-ttu-id="c8f61-1125">**NX_SUCCESS** (0x00) isteğin başarıyla başlatılması.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1125">**NX_SUCCESS** (0x00) Successful initialization of request.</span></span>
- <span data-ttu-id="c8f61-1126">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1126">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1127">NX_WEB_HTTP_METHOD_ERROR (0x30014) bazı gerekli bilgiler eksikti (ör. PUT veya POST için input_size).</span><span class="sxs-lookup"><span data-stu-id="c8f61-1127">NX_WEB_HTTP_METHOD_ERROR (0x30014) Some required information was missing (e.g. input_size for PUT or POST).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1128">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1128">Allowed From</span></span>

<span data-ttu-id="c8f61-1129">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1129">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1130">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1130">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize_extended(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "test.txt ", sizeof("test.txt ") – 1,
    "host.com", sizeof("host.com") – 1,
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    0,
    NX_NULL, /* password */
    0,
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);


/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get()* until the entire response is retrieved. *./
get_status = NX_SUCCESS;
while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_request_packet_send"></a><span data-ttu-id="c8f61-1131">nx_web_http_client_request_packet_send</span><span class="sxs-lookup"><span data-stu-id="c8f61-1131">nx_web_http_client_request_packet_send</span></span>

<span data-ttu-id="c8f61-1132">HTTP (S) istek veri paketini uzak sunucuya gönder</span><span class="sxs-lookup"><span data-stu-id="c8f61-1132">Send HTTP(S) request data packet to remote server</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1133">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1133">Prototype</span></span>

```C
UINT nx_web_http_client_request_packet_send(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET *packet_ptr, UINT more_date,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-1134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1134">Description</span></span>

<span data-ttu-id="c8f61-1135">Bu hizmet, daha önce uzak ana bilgisayara soket bağlantısı oluşturmuş olan *nx_web_http_client_connect ()* veya *nx_web_http_client_secure_connect (*) çağrısında belirtilen sunucuya *nx_web_http_client_request_packet_allocate* () Ile oluşturulan özel bir http (S) istek veri paketi gönderir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1135">This service sends a custom HTTP(S) request data packet created with *nx_web_http_client_request_packet_allocate* () to the server specified in the *nx_web_http_client_connect()* or *nx_web_http_client_secure_connect(*) call which has previously established the socket connection to the remote host.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1136">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1136">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1137">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1137">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-1138">**packet_ptr** HTTP (S) istek veri paketi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1138">**packet_ptr** HTTP(S) request data packet pointer.</span></span>
- <span data-ttu-id="c8f61-1139">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1139">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-1140">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1140">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1141">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1141">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-1142">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1142">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1143">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1143">Return Values</span></span>

- <span data-ttu-id="c8f61-1144">**NX_SUCCESS** (0x00) istek veri paketinin başarıyla gönderilmesi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1144">**NX_SUCCESS** (0x00) Successful send of request data packet.</span></span>
- <span data-ttu-id="c8f61-1145">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1145">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1146">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1146">Allowed From</span></span>

<span data-ttu-id="c8f61-1147">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1147">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1148">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1148">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a PUT request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_PUT,
    "https://192.168.1.150/test.txt ",
    128, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the PUT operation. */
nx_web_http_client_request_send(&my_client, 1000);

/* Create a new data packet request on the HTTP(S) client instance. */
nx_web_http_client_request_packet_allocate(&my_client,
    &my_packet,
    NX_WAIT_FOREVER);

/* At this point, user can fill the data into my_packet. *./
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet request to server. */
status = nx_web_http_client_request_packet_send(&my_client,
    my_packet,
    0,
    NX_WAIT_FOREVER);
```

## <a name="nx_web_http_client_request_send"></a><span data-ttu-id="c8f61-1149">nx_web_http_client_request_send</span><span class="sxs-lookup"><span data-stu-id="c8f61-1149">nx_web_http_client_request_send</span></span>

<span data-ttu-id="c8f61-1150">Özel bir HTTP isteği gönder</span><span class="sxs-lookup"><span data-stu-id="c8f61-1150">Send a custom HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1151">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1151">Prototype</span></span>

```C
UINT nx_web_http_client_request_send(NX_WEB_HTTP_CLIENT *client_ptr,
    UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-1152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1152">Description</span></span>

<span data-ttu-id="c8f61-1153">Bu hizmet, *nx_web_http_client_connect (* ) veya *nx_web_http_client_secure_connect ()* içinde belirtilen sunucuya *nx_web_http_client_request_initialize (* ) ile oluşturulan özel bir http isteğini, her ikisi de daha önce uzak ana bilgisayara soket bağlantısını kurdu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1153">This service sends a custom HTTP request created with *nx_web_http_client_request_initialize()* to the server specified in the *nx_web_http_client_connect()* or *nx_web_http_client_secure_connect()* both of which have previously established the socket connection to the remote host.</span></span>

<span data-ttu-id="c8f61-1154">Bu hizmetin kullanılması, bir uygulamanın ***nx_web_http_client_request_header_add ()*** hizmetini kullanarak isteğe herhangi bir sayıda özel üst bilgi eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1154">Use of this service enables an application to add any number of custom headers to the request using the ***nx_web_http_client_request_header_add()*** service.</span></span> <span data-ttu-id="c8f61-1155">Bu, belirli uygulamalar için tasarlanan özelleştirilmiş HTTP isteklerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1155">This allows for customized HTTP requests intended for specific applications.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-1156">Nx_web_http_client_ \* _start yöntemleri kolaylık sağlaması için verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1156">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8f61-1157">Bu işlevlerin tümü bu yordamı, HTTP istekleri oluşturmak ve göndermek için dahili olarak ( *nx_web_http_client_request_initialize ()* ile birlikte kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1157">These functions all use this routine internally (along with *nx_web_http_client_request_initialize())* to create and send HTTP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1158">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1158">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1159">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1159">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-1160">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1160">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-1161">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1161">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1162">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1162">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-1163">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1163">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1164">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1164">Return Values</span></span>

- <span data-ttu-id="c8f61-1165">**NX_SUCCESS** (0x00) başarılı istek gönderme.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1165">**NX_SUCCESS** (0x00) Successful send of request.</span></span>
- <span data-ttu-id="c8f61-1166">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1166">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1167">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1167">Allowed From</span></span>

<span data-ttu-id="c8f61-1168">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1168">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1169">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1169">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
nx_web_http_client_secure_connect(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by
    repeatedly calling *nx_web_http_client_response_body_get* until
    the entire response is retrieved. *./

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);

    /* Process response packets… */
}
```

## <a name="nx_web_http_client_response_body_get"></a><span data-ttu-id="c8f61-1170">nx_web_http_client_response_body_get</span><span class="sxs-lookup"><span data-stu-id="c8f61-1170">nx_web_http_client_response_body_get</span></span>

<span data-ttu-id="c8f61-1171">Sonraki kaynak veri paketini al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1171">Get next resource data packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1172">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1172">Prototype</span></span>

```C
UINT nx_web_http_client_response_body_get(
    NX_WEB_HTTP_CLIENT *client_ptr,
    NX_PACKET **packet_ptr, ULONG
    wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-1173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1173">Description</span></span>

<span data-ttu-id="c8f61-1174">Bu hizmet, önceki *nx_web_http_client_get_start ()* veya *nx_web_http_client_get_secure_start ()* çağrısı tarafından istenen kaynağın sonraki içerik paketini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1174">This service retrieves the next packet of content of the resource requested by the previous *nx_web_http_client_get_start()* or *nx_web_http_client_get_secure_start()* call.</span></span> <span data-ttu-id="c8f61-1175">NX_WEB_HTTP_GET_DONE geri dönüş durumu alınana kadar bu yordama yönelik ardışık çağrılar yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1175">Successive calls to this routine should be made until the return status of NX_WEB_HTTP_GET_DONE is received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1176">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1176">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1177">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1177">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-1178">**packet_ptr** Kısmi kaynak içeriği içeren paket işaretçisi hedefi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1178">**packet_ptr** Destination for packet pointer containing partial resource content.</span></span>
- <span data-ttu-id="c8f61-1179">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1179">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-1180">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1180">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1181">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1181">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-1182">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1182">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1183">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1183">Return Values</span></span>

- <span data-ttu-id="c8f61-1184">**NX_SUCCESS** (0x00) http Istemci paketinin başarılı bir şekilde alınacağı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1184">**NX_SUCCESS** (0x00) Successful get of HTTP Client packet.</span></span>
- <span data-ttu-id="c8f61-1185">**NX_WEB_HTTP_GET_DONE** (0x3000c) http istemcisi Get paketi bitti</span><span class="sxs-lookup"><span data-stu-id="c8f61-1185">**NX_WEB_HTTP_GET_DONE** (0x3000C) HTTP Client get packet is done</span></span>
- <span data-ttu-id="c8f61-1186">**NX_WEB_HTTP_NOT_READY** (0x3000a) http istemcisi Get modunda değil.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1186">**NX_WEB_HTTP_NOT_READY** (0x3000A) HTTP Client not in get mode.</span></span>
- <span data-ttu-id="c8f61-1187">**NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000d) geçersiz paket uzunluğu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1187">**NX_WEB_HTTP_BAD_PACKET_LENGTH** (0x3000D) Invalid packet length</span></span>
- <span data-ttu-id="c8f61-1188">**NX_WEB_HTTP_STATUS_CODE_CONTINUE** (0x3001a) http durum kodu 100 devam</span><span class="sxs-lookup"><span data-stu-id="c8f61-1188">**NX_WEB_HTTP_STATUS_CODE_CONTINUE** (0x3001A) HTTP status code 100 Continue</span></span>
- <span data-ttu-id="c8f61-1189">**NX_WEB_HTTP_STATUS_CODE_SWITCHING_PROTOCOLS** (0x3001b) http durum kodu 101 anahtarlama protokolleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1189">**NX_WEB_HTTP_STATUS_CODE_SWITCHING_PROTOCOLS** (0x3001B) HTTP status code 101 Switching Protocols</span></span>
- <span data-ttu-id="c8f61-1190">**NX_WEB_HTTP_STATUS_CODE_CREATED** (0x3001c) http durum kodu 201 oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1190">**NX_WEB_HTTP_STATUS_CODE_CREATED** (0x3001C) HTTP status code 201 Created</span></span>
- <span data-ttu-id="c8f61-1191">**NX_WEB_HTTP_STATUS_CODE_ACCEPTED** (0x3001d) http durum kodu 202 kabul edildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1191">**NX_WEB_HTTP_STATUS_CODE_ACCEPTED** (0x3001D) HTTP status code 202 Accepted</span></span>
- <span data-ttu-id="c8f61-1192">**NX_WEB_HTTP_STATUS_CODE_NON_AUTH_INFO** (0x3001e) http durum kodu 203 yetkili olmayan bilgiler</span><span class="sxs-lookup"><span data-stu-id="c8f61-1192">**NX_WEB_HTTP_STATUS_CODE_NON_AUTH_INFO** (0x3001E) HTTP status code 203 Non-Authoritative Information</span></span>
- <span data-ttu-id="c8f61-1193">**NX_WEB_HTTP_STATUS_CODE_NO_CONTENT** (0x3001f) http durum kodu 204 içerik yok</span><span class="sxs-lookup"><span data-stu-id="c8f61-1193">**NX_WEB_HTTP_STATUS_CODE_NO_CONTENT** (0x3001F) HTTP status code 204 No Content</span></span>
- <span data-ttu-id="c8f61-1194">**NX_WEB_HTTP_STATUS_CODE_RESET_CONTENT** (0x30020) http durum kodu 205 sıfırlama içeriği</span><span class="sxs-lookup"><span data-stu-id="c8f61-1194">**NX_WEB_HTTP_STATUS_CODE_RESET_CONTENT** (0x30020) HTTP status code 205 Reset Content</span></span>
- <span data-ttu-id="c8f61-1195">**NX_WEB_HTTP_STATUS_CODE_PARTIAL_CONTENT** (0x30021) http durum kodu 206 kısmi içerik</span><span class="sxs-lookup"><span data-stu-id="c8f61-1195">**NX_WEB_HTTP_STATUS_CODE_PARTIAL_CONTENT** (0x30021) HTTP status code 206 Partial Content</span></span>
- <span data-ttu-id="c8f61-1196">**NX_WEB_HTTP_STATUS_CODE_MULTIPLE_CHOICES** (0x30022) http durum kodu 300 birden çok seçenek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1196">**NX_WEB_HTTP_STATUS_CODE_MULTIPLE_CHOICES** (0x30022) HTTP status code 300 Multiple Choices</span></span>
- <span data-ttu-id="c8f61-1197">**NX_WEB_HTTP_STATUS_CODE_MOVED_PERMANETLY** (0x30023) http durum kodu 301 kalıcı olarak taşındı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1197">**NX_WEB_HTTP_STATUS_CODE_MOVED_PERMANETLY** (0x30023) HTTP status code 301 Moved Permanently</span></span>
- <span data-ttu-id="c8f61-1198">**NX_WEB_HTTP_STATUS_CODE_FOUND** (0x30024) http durum kodu 302 bulundu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1198">**NX_WEB_HTTP_STATUS_CODE_FOUND** (0x30024) HTTP status code 302 Found</span></span>
- <span data-ttu-id="c8f61-1199">**NX_WEB_HTTP_STATUS_CODE_SEE_OTHER** (0x30025) http durum kodu 303 bkz. diğer</span><span class="sxs-lookup"><span data-stu-id="c8f61-1199">**NX_WEB_HTTP_STATUS_CODE_SEE_OTHER** (0x30025) HTTP status code 303 See Other</span></span>
- <span data-ttu-id="c8f61-1200">**NX_WEB_HTTP_STATUS_CODE_NOT_MODIFIED** (0x30026) http durum kodu 304 değiştirilmedi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1200">**NX_WEB_HTTP_STATUS_CODE_NOT_MODIFIED** (0x30026) HTTP status code 304 Not Modified</span></span>
- <span data-ttu-id="c8f61-1201">**NX_WEB_HTTP_STATUS_CODE_USE_PROXY** (0x30027) http durum kodu 305 proxy kullan</span><span class="sxs-lookup"><span data-stu-id="c8f61-1201">**NX_WEB_HTTP_STATUS_CODE_USE_PROXY** (0x30027) HTTP status code 305 Use Proxy</span></span>
- <span data-ttu-id="c8f61-1202">**NX_WEB_HTTP_STATUS_CODE_TEMPORARY_REDIRECT** (0x30028) http durum kodu 307 geçici yeniden yönlendirme</span><span class="sxs-lookup"><span data-stu-id="c8f61-1202">**NX_WEB_HTTP_STATUS_CODE_TEMPORARY_REDIRECT** (0x30028) HTTP status code 307 Temporary Redirect</span></span>
- <span data-ttu-id="c8f61-1203">**NX_WEB_HTTP_STATUS_CODE_BAD_REQUEST** (0x30029) http durum kodu 400 hatalı istek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1203">**NX_WEB_HTTP_STATUS_CODE_BAD_REQUEST** (0x30029) HTTP status code 400 Bad Request</span></span>
- <span data-ttu-id="c8f61-1204">**NX_WEB_HTTP_STATUS_CODE_UNAUTHORIZED** (0x3002a) http durum kodu 401 Yetkisiz</span><span class="sxs-lookup"><span data-stu-id="c8f61-1204">**NX_WEB_HTTP_STATUS_CODE_UNAUTHORIZED** (0x3002A) HTTP status code 401 Unauthorized</span></span>
- <span data-ttu-id="c8f61-1205">**NX_WEB_HTTP_STATUS_CODE_PAYMENT_REQUIRED** (0x3002b) http durum kodu 402 ödeme gerekiyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-1205">**NX_WEB_HTTP_STATUS_CODE_PAYMENT_REQUIRED** (0x3002B) HTTP status code 402 Payment Required</span></span>
- <span data-ttu-id="c8f61-1206">**NX_WEB_HTTP_STATUS_CODE_FORBIDDEN** (0x3002c) http durum kodu 403 Yasak</span><span class="sxs-lookup"><span data-stu-id="c8f61-1206">**NX_WEB_HTTP_STATUS_CODE_FORBIDDEN** (0x3002C) HTTP status code 403 Forbidden</span></span>
- <span data-ttu-id="c8f61-1207">**NX_WEB_HTTP_STATUS_CODE_NOT_FOUND** (0x3002d) http durum kodu 404 bulunamadı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1207">**NX_WEB_HTTP_STATUS_CODE_NOT_FOUND** (0x3002D) HTTP status code 404 Not Found</span></span>
- <span data-ttu-id="c8f61-1208">**NX_WEB_HTTP_STATUS_CODE_METHOD_NOT_ALLOWED** (0x3002e) http durum kodu 405 yöntemine izin verilmiyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-1208">**NX_WEB_HTTP_STATUS_CODE_METHOD_NOT_ALLOWED** (0x3002E) HTTP status code 405 Method Not Allowed</span></span>
- <span data-ttu-id="c8f61-1209">**NX_WEB_HTTP_STATUS_CODE_NOT_ACCEPTABLE** (0x3002f) http durum kodu 406 kabul edilemez</span><span class="sxs-lookup"><span data-stu-id="c8f61-1209">**NX_WEB_HTTP_STATUS_CODE_NOT_ACCEPTABLE** (0x3002F) HTTP status code 406 Not Acceptable</span></span>
- <span data-ttu-id="c8f61-1210">**NX_WEB_HTTP_STATUS_CODE_PROXY_AUTH_REQUIRED** (0x30030) http durum kodu 407 Proxy kimlik doğrulaması gerekiyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-1210">**NX_WEB_HTTP_STATUS_CODE_PROXY_AUTH_REQUIRED** (0x30030) HTTP status code 407 Proxy Authentication Required</span></span>
- <span data-ttu-id="c8f61-1211">**NX_WEB_HTTP_STATUS_CODE_REQUEST_TIMEOUT** (0x30031) http durum kodu 408 istek zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1211">**NX_WEB_HTTP_STATUS_CODE_REQUEST_TIMEOUT** (0x30031) HTTP status code 408 Request Time-out</span></span>
- <span data-ttu-id="c8f61-1212">**NX_WEB_HTTP_STATUS_CODE_CONFLICT** (0x30032) http durum kodu 409 çakışması</span><span class="sxs-lookup"><span data-stu-id="c8f61-1212">**NX_WEB_HTTP_STATUS_CODE_CONFLICT** (0x30032) HTTP status code 409 Conflict</span></span>
- <span data-ttu-id="c8f61-1213">**NX_WEB_HTTP_STATUS_CODE_GONE** (0x30033) http durum kodu 410 gitti</span><span class="sxs-lookup"><span data-stu-id="c8f61-1213">**NX_WEB_HTTP_STATUS_CODE_GONE** (0x30033) HTTP status code 410 Gone</span></span>
- <span data-ttu-id="c8f61-1214">**NX_WEB_HTTP_STATUS_CODE_LENGTH_REQUIRED** (0x30034) http durum kodu 411 uzunluğu gereklidir</span><span class="sxs-lookup"><span data-stu-id="c8f61-1214">**NX_WEB_HTTP_STATUS_CODE_LENGTH_REQUIRED** (0x30034) HTTP status code 411 Length Required</span></span>
- <span data-ttu-id="c8f61-1215">**NX_WEB_HTTP_STATUS_CODE_PRECONDITION_FAILED** (0x30035) http durum kodu 412 önkoşulu başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1215">**NX_WEB_HTTP_STATUS_CODE_PRECONDITION_FAILED** (0x30035) HTTP status code 412 Precondition Failed</span></span>
- <span data-ttu-id="c8f61-1216">**NX_WEB_HTTP_STATUS_CODE_ENTITY_TOO_LARGE** (0x30036) http durum kodu 413 Istek varlığı çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-1216">**NX_WEB_HTTP_STATUS_CODE_ENTITY_TOO_LARGE** (0x30036) HTTP status code 413 Request Entity Too Large</span></span>
- <span data-ttu-id="c8f61-1217">**NX_WEB_HTTP_STATUS_CODE_URL_TOO_LARGE** (0x30037) http durum kodu 414 istek URL 'Si çok büyük</span><span class="sxs-lookup"><span data-stu-id="c8f61-1217">**NX_WEB_HTTP_STATUS_CODE_URL_TOO_LARGE** (0x30037) HTTP status code 414 Request URL Too Large</span></span>
- <span data-ttu-id="c8f61-1218">**NX_WEB_HTTP_STATUS_CODE_UNSUPPORTED_MEDIA** (0x30038) http durum kodu 415 desteklenmeyen medya türü</span><span class="sxs-lookup"><span data-stu-id="c8f61-1218">**NX_WEB_HTTP_STATUS_CODE_UNSUPPORTED_MEDIA** (0x30038) HTTP status code 415 Unsupported Media Type</span></span>
- <span data-ttu-id="c8f61-1219">**NX_WEB_HTTP_STATUS_CODE_RANGE_NOT_SATISFY** (0x30039) http durum kodu 416 İstenen Aralık satisfiable değil</span><span class="sxs-lookup"><span data-stu-id="c8f61-1219">**NX_WEB_HTTP_STATUS_CODE_RANGE_NOT_SATISFY** (0x30039) HTTP status code 416 Requested range not satisfiable</span></span>
- <span data-ttu-id="c8f61-1220">**NX_WEB_HTTP_STATUS_CODE_EXPECTATION_FAILED** (0x3003a) http durum kodu 417 beklenti başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1220">**NX_WEB_HTTP_STATUS_CODE_EXPECTATION_FAILED** (0x3003A) HTTP status code 417 Expectation Failed</span></span>
- <span data-ttu-id="c8f61-1221">**NX_WEB_HTTP_STATUS_CODE_INTERNAL_ERROR** (0x3003b) http durum kodu 500 Iç sunucu hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-1221">**NX_WEB_HTTP_STATUS_CODE_INTERNAL_ERROR** (0x3003B) HTTP status code 500 Internal Server Error</span></span>
- <span data-ttu-id="c8f61-1222">**NX_WEB_HTTP_STATUS_CODE_NOT_IMPLEMENTED** (0x3003c) http durum kodu 501 uygulanmadı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1222">**NX_WEB_HTTP_STATUS_CODE_NOT_IMPLEMENTED** (0x3003C) HTTP status code 501 Not Implemented</span></span>
- <span data-ttu-id="c8f61-1223">**NX_WEB_HTTP_STATUS_CODE_BAD_GATEWAY** (0x3003d) http durum kodu 502 hatalı ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1223">**NX_WEB_HTTP_STATUS_CODE_BAD_GATEWAY** (0x3003D) HTTP status code 502 Bad Gateway</span></span>
- <span data-ttu-id="c8f61-1224">**NX_WEB_HTTP_STATUS_CODE_SERVICE_UNAVAILABLE** (0x3003e) http durum kodu 503 hizmeti kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-1224">**NX_WEB_HTTP_STATUS_CODE_SERVICE_UNAVAILABLE** (0x3003E) HTTP status code 503 Service Unavailable</span></span>
- <span data-ttu-id="c8f61-1225">**NX_WEB_HTTP_STATUS_CODE_GATEWAY_TIMEOUT** (0x3003f) http durum kodu 504 ağ geçidi zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1225">**NX_WEB_HTTP_STATUS_CODE_GATEWAY_TIMEOUT** (0x3003F) HTTP status code 504 Gateway Time-out</span></span>
- <span data-ttu-id="c8f61-1226">**NX_WEB_HTTP_STATUS_CODE_VERSION_ERROR** (0x30040) http durum kodu 505 http sürümü desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="c8f61-1226">**NX_WEB_HTTP_STATUS_CODE_VERSION_ERROR** (0x30040) HTTP status code 505 HTTP Version not supported</span></span>
- <span data-ttu-id="c8f61-1227">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1227">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1228">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1228">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1229">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1229">Allowed From</span></span>

<span data-ttu-id="c8f61-1230">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1230">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1231">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1231">Example</span></span>

```C
/* Get the next packet of resource content on the HTTP Client "my_client."
    Note that the nx_web_http_client_get_start() routine must have been called
    previously. */
status = nx_web_http_client_response_body_get(&my_client, &next_packet, 1000);

/* If status is NX_SUCCESS, the next packet of content is pointed to
    by "next_packet". */
```

## <a name="nx_web_http_client_response_header_callback_set"></a><span data-ttu-id="c8f61-1232">nx_web_http_client_response_header_callback_set</span><span class="sxs-lookup"><span data-stu-id="c8f61-1232">nx_web_http_client_response_header_callback_set</span></span>

<span data-ttu-id="c8f61-1233">HTTP üstbilgilerini işlerken çağırmak için geri çağırma ayarla</span><span class="sxs-lookup"><span data-stu-id="c8f61-1233">Set callback to invoke when processing HTTP headers</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1234">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1234">Prototype</span></span>

```C
UINT nx_web_http_client_response_header_callback_set(
    NX_WEB_HTTP_CLIENT *client_ptr,
    VOID (*callback_function)(NX_WEB_HTTP_CLIENT *client_ptr,
    CHAR *field_name, UINT field_name_length,
    CHAR *field_value, UINT field_value_length));
```

### <a name="description"></a><span data-ttu-id="c8f61-1235">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1235">Description</span></span>

<span data-ttu-id="c8f61-1236">Bu hizmet, NetX Web HTTP Istemcisi, uzak bir HTTP sunucusundan gelen bir yanıtta bir HTTP üst bilgisini işlediğinde çağrılacak bir geri çağırma işlemi atar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1236">This service assigns a callback that will be invoked whenever NetX Web HTTP Client processes an HTTP header in an incoming response from a remote HTTP server.</span></span> <span data-ttu-id="c8f61-1237">Geri çağırma, yanıttaki her üstbilgi için bir kez çağrılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1237">The callback is invoked once for each header in the response as it is processed.</span></span> <span data-ttu-id="c8f61-1238">Geri arama, bir HTTP Istemci uygulamasının, NetX Web HTTP Istemcisinin işlediği temel işlemenin ötesinde istenen eylemleri gerçekleştirmek için HTTP sunucusu yanıtında her bir üst bilgiye erişmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1238">The callback allows an HTTP Client application to access each of the headers in the HTTP server response to take any desired actions beyond the basic processing that NetX Web HTTP Client does.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1239">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1239">Input Parameters</span></span>

<span data-ttu-id="c8f61-1240">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1240">**client_ptr** Pointer to HTTP Client control block.</span></span>

<span data-ttu-id="c8f61-1241">**callback_function** Yanıt üst bilgisi işleme sırasında geri çağırma çağrıldı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1241">**callback_function** Callback invoked during response header processing.</span></span> <span data-ttu-id="c8f61-1242">Geri çağırma, alan adı ve değeri dizeler (ve uzunlukları) ile çağrılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1242">The callback is invoked with the field name and value as strings (and their lengths).</span></span> <span data-ttu-id="c8f61-1243">Örneğin, "Content-Length: 100" üstbilgisi, işlevin *field_name* Için "Content-Length" ve *field_value*"100" dizesi ile çağrılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1243">For example, the header "Content-Length: 100" would cause the function to be invoked with "Content-Length" for *field_name* and the string "100" for *field_value*.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1244">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1244">Return Values</span></span>

- <span data-ttu-id="c8f61-1245">**NX_SUCCESS** (0x00) geri aramanın başarıyla atanması.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1245">**NX_SUCCESS** (0x00) Successful assignment of callback.</span></span>
- <span data-ttu-id="c8f61-1246">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1246">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1247">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1247">Allowed From</span></span>

<span data-ttu-id="c8f61-1248">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1248">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1249">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1249">Example</span></span>

```C
/* Setup a callback to print out header information as it is processed. */
VOID http_response_callback(NX_WEB_HTTP_CLIENT *client_ptr, CHAR *field_name,
    UINT field_name_length, CHAR *field_value,
    UINT field_value_length)
{
    CHAR name[100];
    CHAR value[100];
    memset(name, 0, sizeof(name));

    memset(value, 0, sizeof(value));

    strncpy(name, field_name, field_name_length);
    strncpy(value, field_value, field_value_length);

    printf("Received header: \n");
    printf("\tField name: %s (%d bytes)\n", name, field_name_length);
    printf("\tValue: %s (%d bytes)\n\n", value, field_value_length);
}

/* Assign the callback to the HTTP client instance. */
nx_web_http_client_response_header_callback_set(&my_client,
    http_response_callback);

/* Start a GET operation to get a response from the HTTP server. */
status = nx_web_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5),
    NX_WEB_HTTP_SERVER_PORT, "/TEST.HTM",
    "myname", "mypassword", 1000);

/* When the HTTP server returns a response to the GET request, NetX Web HTTP
    Client will invoke the http_response_callback function for each header
    processed in the HTTP response. */
```

## <a name="nx_web_http_client_secure_connect"></a><span data-ttu-id="c8f61-1250">nx_web_http_client_secure_connect</span><span class="sxs-lookup"><span data-stu-id="c8f61-1250">nx_web_http_client_secure_connect</span></span>

<span data-ttu-id="c8f61-1251">Özel istekler için bir HTTPS sunucusunda TLS oturumu açma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1251">Open a TLS session to an HTTPS server for custom requests</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1252">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1252">Prototype</span></span>

```C
UINT nx_web_http_client_secure_connect(NX_WEB_HTTP_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT (*tls_setup)(NX_WEB_HTTP_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *tls),
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-1253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1253">Description</span></span>

<span data-ttu-id="c8f61-1254">Bu yöntem **TLS ile güvenli** https içindir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1254">This method is for **TLS-secured** HTTPS.</span></span>

<span data-ttu-id="c8f61-1255">Bu hizmet bir HTTPS sunucusunda güvenli bir TLS oturumu açar, ancak hiçbir istek göndermez.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1255">This service opens a secured TLS session to an HTTPS server but does not send any requests.</span></span> <span data-ttu-id="c8f61-1256">İstekler n *x_web_http_client_request_initialize ()* ile oluşturulur ve *nx_web_http_client_request_send ()* kullanılarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1256">Requests are created with n *x_web_http_client_request_initialize()* and sent using *nx_web_http_client_request_send()*.</span></span> <span data-ttu-id="c8f61-1257">*Nx_web_http_client_request_header_add ()* kullanılarak Isteğe özel http üstbilgileri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1257">Custom HTTP headers may be added to the request using *nx_web_http_client_request_header_add()*.</span></span>

<span data-ttu-id="c8f61-1258">Bu hizmetin kullanılması, bir uygulamanın isteğe herhangi sayıda özel üst bilgi eklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1258">Use of this service enables an application to add any number of custom headers to the request.</span></span> <span data-ttu-id="c8f61-1259">**Bu, belirli uygulamalar için tasarlanan özelleştirilmiş HTTP isteklerine izin verir.**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1259">**This allows for customized HTTP requests intended for specific applications.**</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-1260">Nx_web_http_client_ \* _start yöntemleri kolaylık sağlaması için verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1260">The nx_web_http_client_\*_start methods are provided for convenience.</span></span> <span data-ttu-id="c8f61-1261">Bu işlevlerin tümü bu yordamı, HTTP istekleri oluşturmak ve göndermek için dahili olarak ( *nx_web_http_client_request_initialize ()* ile birlikte kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1261">These functions all use this routine internally (along with *nx_web_http_client_request_initialize())* to create and send HTTP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1262">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1262">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1263">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1263">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-1264">**server_ip** Uzak HTTPS sunucusunun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1264">**server_ip** IP address of remote HTTPS server.</span></span>
- <span data-ttu-id="c8f61-1265">**SERVER_PORT** Uzak HTTPS sunucusundaki bağlantı noktası (örneğin, HTTPS için 443).</span><span class="sxs-lookup"><span data-stu-id="c8f61-1265">**server_port** Port on remote HTTPS server (e.g. 443 for HTTPS).</span></span>
- <span data-ttu-id="c8f61-1266">**tls_setup** TLS yapılandırmasını kurmak için kullanılan geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1266">**tls_setup** Callback used to setup TLS configuration.</span></span> <span data-ttu-id="c8f61-1267">Uygulama, TLS şifrelemesini ve kimlik bilgilerini (örn. Sertifikalar) başlatmak için bu geri aramayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1267">The application defines this callback to initialize TLS cryptography and credentials (e.g. certificates).</span></span>
- <span data-ttu-id="c8f61-1268">**wait_option** Hizmetin HTTP Istemcisi alma başlangıç isteği için bekleyeceği süreyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1268">**wait_option** Defines how long the service will wait for the HTTP Client get start request.</span></span> <span data-ttu-id="c8f61-1269">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1269">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1270">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1270">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>
  - <span data-ttu-id="c8f61-1271">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1271">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1272">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1272">Return Values</span></span>

- <span data-ttu-id="c8f61-1273">**NX_SUCCESS** (0x00) TLS oturumunun başarıyla bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1273">**NX_SUCCESS** (0x00) Successful connection of TLS session.</span></span>
- <span data-ttu-id="c8f61-1274">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1274">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1275">NX_WEB_HTTP_NOT_READY (0x3000A) başka bir istek zaten devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1275">NX_WEB_HTTP_NOT_READY (0x3000A) Another request is already in progress.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1276">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1276">Allowed From</span></span>

<span data-ttu-id="c8f61-1277">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1277">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1278">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1278">Example</span></span>

```C
/* Connect to a remote HTTPS server. */
/* Connect to a remote HTTP server. */
server_ip_addr.nxd_ip_version = NX_IP_VERSION_V4;
server_ip_addr.nxd_ip_address.v4 = IP_ADDRESS(1,2,3,5);

nx_web_http_client_secure_connect(&my_client, &server_ip_addr,
    NX_WEB_HTTPS_SERVER_PORT, tls_setup_callback,
    NX_WAIT_FOREVER);

/* Create a new GET request on the HTTP client instance. */
nx_web_http_client_request_initialize(&my_client,
    NX_WEB_HTTP_METHOD_GET,
    "https://192.168.1.150/test.txt ",
    0, /* Used by PUT and POST only */
    NX_FALSE,
    NX_NULL, /* username */
    NX_NULL, /* password */
    NX_WAIT_FOREVER);

/* Add a custom header to the GET request we just created. */
status = nx_web_http_client_request_header_add(&my_client, "Server", 6,
    "NetX Web HTTPS Server", 21, NX_WAIT_FOREVER);

/* Start the GET operation to get a response from the HTTPS server. */
status = nx_web_http_client_request_send(&my_client, 1000);

/* At this point, we need to handle the response from the server by repeatedly
    calling *nx_web_http_client_response_body_get* until the entire response is retrieved. *./

get_status = NX_SUCCESS;

while(get_status != NX_WEB_HTTP_GET_DONE)
{
    get_status = nx_web_http_client_response_body_get(&my_client, &receive_packet,
        NX_WAIT_FOREVER);
    /* Process response packets… */
}
```

## <a name="http-and-https-server-api"></a><span data-ttu-id="c8f61-1279">HTTP ve HTTPS sunucu API 'SI</span><span class="sxs-lookup"><span data-stu-id="c8f61-1279">HTTP and HTTPS Server API</span></span>

## <a name="nx_web_http_server_cache_info_callback_set"></a><span data-ttu-id="c8f61-1280">nx_web_http_server_cache_info_callback_set</span><span class="sxs-lookup"><span data-stu-id="c8f61-1280">nx_web_http_server_cache_info_callback_set</span></span>

<span data-ttu-id="c8f61-1281">URL 'YI en yüksek yaş ve tarihi almak için geri aramayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c8f61-1281">Set the callback to retrieve URL max age and date</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1282">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1282">Prototype</span></span>

```C
UINT nx_web_http_server_cache_info_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT (*cache_info_get)(CHAR *resource,
    UINT *max_age,
    NX_WEB_HTTP_SERVER_DATE *date));
```

### <a name="description"></a><span data-ttu-id="c8f61-1283">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1283">Description</span></span>

<span data-ttu-id="c8f61-1284">Bu hizmet, belirtilen kaynağın yaş ve son değiştirilme tarihini elde etmek için çağrılan geri çağırma hizmetini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1284">This service sets the callback service invoked to obtain the maximum age and last modified date of the specified resource.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1285">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1285">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1286">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1286">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1287">**cache_info_get** Geri çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1287">**cache_info_get** Pointer to the callback</span></span>
- <span data-ttu-id="c8f61-1288">**max_age** Bir kaynağın maksimum yaşı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1288">**max_age** Pointer to maximum age of a resource</span></span>
- <span data-ttu-id="c8f61-1289">**veri** Son değiştirme tarihine yönelik işaretçi döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1289">**data** Pointer to last modified date returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1290">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1290">Return Values</span></span>

- <span data-ttu-id="c8f61-1291">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1291">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8f61-1292">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1292">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1293">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1293">Allowed From</span></span>

<span data-ttu-id="c8f61-1294">Başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1294">Initialization</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1295">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1295">Example</span></span>

```C
NX_WEB_HTTP_SERVER my_server;

UINT cache_info_get(CHAR *resource, UINT *max_age,
    NX_WEB_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_web_http_server_create and before the HTTP
    server is set by nx_web_http_server_start(), set the cache info callback: */
status = nx_web_http_server_cache_info_callback_set(&my_server, cache_info_get);

/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_web_http_server_callback_data_send"></a><span data-ttu-id="c8f61-1296">nx_web_http_server_callback_data_send</span><span class="sxs-lookup"><span data-stu-id="c8f61-1296">nx_web_http_server_callback_data_send</span></span>

<span data-ttu-id="c8f61-1297">Geri çağırma işlevinden veri Gönder</span><span class="sxs-lookup"><span data-stu-id="c8f61-1297">Send data from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1298">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1298">Prototype</span></span>

```C
UINT nx_web_http_server_callback_data_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID *data_ptr, ULONG data_length);
```

### <a name="description"></a><span data-ttu-id="c8f61-1299">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1299">Description</span></span>

<span data-ttu-id="c8f61-1300">Bu hizmet, sağlanan paketteki verileri uygulamanın geri arama yordamından gönderir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1300">This service sends the data in the supplied packet from the application’s callback routine.</span></span> <span data-ttu-id="c8f61-1301">Bu, genellikle GET/POST istekleri ile ilişkili dinamik verileri göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1301">This is typically used to send dynamic data associated with GET/POST requests.</span></span> <span data-ttu-id="c8f61-1302">Bu işlev kullanıldığında, tüm yanıtın doğru biçimde gönderilmesi için geri çağırma yordamının sorumlu olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1302">Note that if this function is used, the callback routine is responsible for sending the entire response in the proper format.</span></span> <span data-ttu-id="c8f61-1303">Ayrıca, geri arama yordamı NX_WEB_HTTP_CALLBACK_COMPLETED durumunu döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1303">In addition, the callback routine must return the status of NX_WEB_HTTP_CALLBACK_COMPLETED.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1304">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1304">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1305">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1305">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1306">**data_ptr** Gönderilen verilerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1306">**data_ptr** Pointer to the data to send.</span></span>
- <span data-ttu-id="c8f61-1307">**data_length** Gönderilen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1307">**data_length** Number of bytes to send.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1308">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1308">Return Values</span></span>

- <span data-ttu-id="c8f61-1309">**NX_SUCCESS** (0x00) sunucu verilerini başarıyla gönderdi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1309">**NX_SUCCESS** (0x00) Successfully sent Server data</span></span>
- <span data-ttu-id="c8f61-1310">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1310">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1311">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1311">Allowed From</span></span>

<span data-ttu-id="c8f61-1312">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1312">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1313">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1313">Example</span></span>

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* Found it, override the GET processing by sending the resource
            contents directly. */
        nx_web_http_server_callback_data_send(server_ptr,
            "HTTP/1.0 200 \r\nContent-Length:" "103\r\nContent-Type: text/html\r\n\r\n",
            63);

        nx_web_http_server_callback_data_send(server_ptr, "<HTML>\r\n<HEAD><TITLE>NetX"
            "HTTP Test </TITLE></HEAD>\r\n"
            :<BODY>\r\n<H1>NetX Test Page"
            "</H1>\r\n</BODY>\r\n</HTML>\r\n", 103);

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_callback_generate_response_header"></a><span data-ttu-id="c8f61-1314">nx_web_http_server_callback_generate_response_header</span><span class="sxs-lookup"><span data-stu-id="c8f61-1314">nx_web_http_server_callback_generate_response_header</span></span>

<span data-ttu-id="c8f61-1315">Geri arama işlevinde yanıt üst bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1315">Create a response header in a callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1316">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1316">Prototype</span></span>

```C
UINT nx_web_http_server_callback_generate_response_header(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    CHAR *status_code, UINT content_length,
    CHAR *content_type, CHAR* additional_header);
```

### <a name="description"></a><span data-ttu-id="c8f61-1317">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1317">Description</span></span>

<span data-ttu-id="c8f61-1318">Bu hizmet http (S) sunucusu geri çağırma yordamında (uygulama tarafından tanımlanır) bir HTTP yanıt üst bilgisi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1318">This service is used in the HTTP(S) server callback routine (defined by the application) to generate an HTTP response header.</span></span> <span data-ttu-id="c8f61-1319">Http sunucusu, HTTP yanıtı gerektiren Istemci al, koy ve SIL isteklerini yanıtladığı zaman sunucu geri çağırma yordamı çağrılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1319">The server callback routine is invoked when the HTTP server responds to Client GET, PUT and DELETE requests which require an HTTP response.</span></span> <span data-ttu-id="c8f61-1320">Bu işlev, uygulamadan gelen yanıt bilgilerini alır ve uygun yanıt üst bilgisini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1320">This function takes the response information from the application and generates the appropriate response header.</span></span> <span data-ttu-id="c8f61-1321">Sunucu isteği geri arama yordamı hakkında daha fazla bilgi için *nx_web_http_server_create ()* hizmetine bakın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1321">See the service *nx_web_http_server_create()* for more information on the server request callback routine.</span></span>

<span data-ttu-id="c8f61-1322">Bu API kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1322">This API is deprecated.</span></span> <span data-ttu-id="c8f61-1323">Geliştiricilerin *nx_web_http_server_callback_generate_response_header_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1323">Developers are encouraged to use *nx_web_http_server_callback_generate_response_header_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1324">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1324">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1325">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1325">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1326">**packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1326">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
- <span data-ttu-id="c8f61-1327">**status_code** Kaynağın durumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1327">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="c8f61-1328">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1328">Examples:</span></span>
  - <span data-ttu-id="c8f61-1329">**NX_WEB_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1329">**NX_WEB_HTTP_STATUS_OK**</span></span>
  - <span data-ttu-id="c8f61-1330">**NX_WEB_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1330">**NX_WEB_HTTP_STATUS_MODIFIED**</span></span>
  - <span data-ttu-id="c8f61-1331">**NX_WEB_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1331">**NX_WEB_HTTP_STATUS_INTERNAL_ERROR**</span></span>
- <span data-ttu-id="c8f61-1332">**CONTENT_LENGTH** İçerik boyutu (bayt)</span><span class="sxs-lookup"><span data-stu-id="c8f61-1332">**content_length** Size of content in bytes</span></span>
- <span data-ttu-id="c8f61-1333">**content_type** HTTP türü, örneğin "metin/düz"</span><span class="sxs-lookup"><span data-stu-id="c8f61-1333">**content_type** Type of HTTP e.g. "text/plain"</span></span>
- <span data-ttu-id="c8f61-1334">**additional_header** Ek üst bilgi metnine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1334">**additional_header** Pointer to additional header text</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1335">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1335">Return Values</span></span>

- <span data-ttu-id="c8f61-1336">**NX_SUCCESS** (0x00) HTML üst bilgisi başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1336">**NX_SUCCESS** (0x00) Successfully created HTML header</span></span>
- <span data-ttu-id="c8f61-1337">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1337">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1338">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1338">Allowed From</span></span>

<span data-ttu-id="c8f61-1339">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1339">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1340">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1340">Example</span></span>

```C
CHAR demotestbuffer[] = "<html>> r\n\r\n<head>> r\n\r\n<title>Main \
    Window</title>> r\n</head>> r\n\r\n<body>Test message\r\n \ </body>> r\n</html>> r\n";

/* my_request_notify* is the application request notify callback registered
    with the HTTP server in *nx_web_http_server_create*,
    creates a response to the received Client request. */

UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET *resp_packet_ptr;
    ULONG string_length;
    CHAR temp_string[30];
    ULONG length = 0;
    length = strlen(&demotestbuffer[0]);

    /* Derive the client request type from the client request. */
    nx_web_http_server_type_extract(server_ptr,
        server_ptr -> nx_web_http_server_request_resource,
        temp_string, sizeof(temp_string), &string_length);

    /* Null terminate the string. */
    temp_string[string_length] = 0;

    /* Now build a response header with server status is OK and no additional header info. */
    status = nx_web_http_server_callback_generate_response_header(http_server_ptr,
        &resp_packet_ptr, NX_WEB_HTTP_STATUS_OK,
        length, temp_string, NX_NULL);

    /* If status is NX_SUCCESS, the header was successfully appended. */

    /* Now add data to the packet. */
    status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
        strlen(&demotestbuffer[0]), server_ptr >>
        nx_web_http_server_packet_pool_ptr, NX_WAIT_FOREVER);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Now send the packet! */
    status = nx_web_http_server_callback_packet_send(
        &(server_ptr -> nx_web_http_server_socket),
        resp_packet_ptr);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Let HTTP server know the response has been sent. */
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);
}
```

## <a name="nx_web_http_server_callback_generate_response_header_extended"></a><span data-ttu-id="c8f61-1341">nx_web_http_server_callback_generate_response_header_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-1341">nx_web_http_server_callback_generate_response_header_extended</span></span>

<span data-ttu-id="c8f61-1342">Geri arama işlevinde yanıt üst bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1342">Create a response header in a callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1343">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1343">Prototype</span></span>

```C
UINT nx_web_http_server_callback_generate_response_header_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    CHAR *status_code, UINT status_code_length,
    UINT content_length, CHAR *content_type,
    UINT content_type_length,
    CHAR* additional_header,
    UINT additional_header_length);
```

### <a name="description"></a><span data-ttu-id="c8f61-1344">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1344">Description</span></span>

<span data-ttu-id="c8f61-1345">Bu hizmet http (S) sunucusu geri çağırma yordamında (uygulama tarafından tanımlanır) bir HTTP yanıt üst bilgisi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1345">This service is used in the HTTP(S) server callback routine (defined by the application) to generate an HTTP response header.</span></span> <span data-ttu-id="c8f61-1346">Http sunucusu, HTTP yanıtı gerektiren Istemci al, koy ve SIL isteklerini yanıtladığı zaman sunucu geri çağırma yordamı çağrılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1346">The server callback routine is invoked when the HTTP server responds to Client GET, PUT and DELETE requests which require an HTTP response.</span></span> <span data-ttu-id="c8f61-1347">Bu işlev, uygulamadan gelen yanıt bilgilerini alır ve uygun yanıt üst bilgisini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1347">This function takes the response information from the application and generates the appropriate response header.</span></span> <span data-ttu-id="c8f61-1348">Sunucu isteği geri arama yordamı hakkında daha fazla bilgi için *nx_web_http_server_create ()* hizmetine bakın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1348">See the service *nx_web_http_server_create()* for more information on the server request callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1349">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1349">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1350">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1350">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1351">**packet_pptr** İleti için ayrılmış bir paket işaretçisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1351">**packet_pptr** Pointer a packet pointer allocated for message</span></span>
- <span data-ttu-id="c8f61-1352">**status_code** Kaynağın durumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1352">**status_code** Indicate status of resource.</span></span> <span data-ttu-id="c8f61-1353">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1353">Examples:</span></span>
  - <span data-ttu-id="c8f61-1354">**NX_WEB_HTTP_STATUS_OK**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1354">**NX_WEB_HTTP_STATUS_OK**</span></span>
  - <span data-ttu-id="c8f61-1355">**NX_WEB_HTTP_STATUS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1355">**NX_WEB_HTTP_STATUS_MODIFIED**</span></span>
  - <span data-ttu-id="c8f61-1356">**NX_WEB_HTTP_STATUS_INTERNAL_ERROR**</span><span class="sxs-lookup"><span data-stu-id="c8f61-1356">**NX_WEB_HTTP_STATUS_INTERNAL_ERROR**</span></span>
- <span data-ttu-id="c8f61-1357">**status_code_length** Durum kodunun dize uzunluğu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1357">**status_code_length** String length of status code</span></span>
- <span data-ttu-id="c8f61-1358">**CONTENT_LENGTH** İçerik boyutu (bayt)</span><span class="sxs-lookup"><span data-stu-id="c8f61-1358">**content_length** Size of content in bytes</span></span>
- <span data-ttu-id="c8f61-1359">**content_type** HTTP türü, örneğin "metin/düz"</span><span class="sxs-lookup"><span data-stu-id="c8f61-1359">**content_type** Type of HTTP e.g. "text/plain"</span></span>
- <span data-ttu-id="c8f61-1360">**content_type_length** İçerik türünün dize uzunluğu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1360">**content_type_length** String length of content type</span></span>
- <span data-ttu-id="c8f61-1361">**additional_header** Ek üst bilgi metnine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1361">**additional_header** Pointer to additional header text</span></span>
- <span data-ttu-id="c8f61-1362">**additional_header_length** Ek üst bilgi metninin uzunluğu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1362">**additional_header_length** Length of additional header text</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1363">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1363">Return Values</span></span>

- <span data-ttu-id="c8f61-1364">**NX_SUCCESS** (0x00) HTML üst bilgisi başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1364">**NX_SUCCESS** (0x00) Successfully created HTML header</span></span>
- <span data-ttu-id="c8f61-1365">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1365">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1366">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1366">Allowed From</span></span>

<span data-ttu-id="c8f61-1367">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1367">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1368">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1368">Example</span></span>

```C
CHAR demotestbuffer[] = "<html>> r\n\r\n<head>> r\n\r\n<title>Main \
    Window</title>> r\n</head>> r\n\r\n<body>Test message\r\n \ </body>> r\n</html>> r\n";

/* my_request_notify* is the application request notify callback
    registered with the HTTP server in *nx_web_http_server_create*,
    creates a response to the received Client request. */

UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET *resp_packet_ptr;
    ULONG string_length;
    CHAR temp_string[30];
    ULONG length = 0;
    length = strlen(&demotestbuffer[0]);

    /* Derive the client request type from the client request. */
    nx_web_http_server_type_extract(server_ptr,
        server_ptr -> nx_web_http_server_request_resource,
        temp_string, sizeof(temp_string), &string_length);

    /* Null terminate the string. */
    temp_string[string_length] = 0;

    /* Now build a response header with server status is OK and no additional header info. */
    status = nx_web_http_server_callback_generate_response_header_extended(http_server_ptr,
        &resp_packet_ptr, NX_WEB_HTTP_STATUS_OK,
        sizeof(NX_WEB_HTTP_STATUS_OK) – 1,
        length, temp_string, string_length NX_NULL, 0);

    /* If status is NX_SUCCESS, the header was successfully appended. */

    /* Now add data to the packet. */
    status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
        strlen(&demotestbuffer[0]), server_ptr >>
        nx_web_http_server_packet_pool_ptr, NX_WAIT_FOREVER);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Now send the packet! */
    status = nx_web_http_server_callback_packet_send(
        &(server_ptr -> nx_web_http_server_socket),
        resp_packet_ptr);

    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Let HTTP server know the response has been sent. */
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);

}
```

## <a name="nx_web_http_server_callback_packet_send"></a><span data-ttu-id="c8f61-1369">nx_web_http_server_callback_packet_send</span><span class="sxs-lookup"><span data-stu-id="c8f61-1369">nx_web_http_server_callback_packet_send</span></span>

<span data-ttu-id="c8f61-1370">Geri çağırma işlevinden HTTP paketi gönder</span><span class="sxs-lookup"><span data-stu-id="c8f61-1370">Send an HTTP packet from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1371">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1371">Prototype</span></span>

```C
UINT nx_web_http_server_callback_packet_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="c8f61-1372">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1372">Description</span></span>

<span data-ttu-id="c8f61-1373">Bu hizmet, HTTP geri çağrısından gelen bir HTTP Sunucu yanıtı gönderir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1373">This service sends a complete HTTP server response from an HTTP callback.</span></span> <span data-ttu-id="c8f61-1374">HTTP sunucusu, paketi NX_WEB_HTTP_SERVER _TIMEOUT_SEND gönderecek.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1374">HTTP server will send the packet with the NX_WEB_HTTP_SERVER _TIMEOUT_SEND.</span></span> <span data-ttu-id="c8f61-1375">HTTP üst bilgisi ve verilerinin pakete eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1375">The HTTP header and data must be appended to the packet.</span></span> <span data-ttu-id="c8f61-1376">Dönüş durumu bir hata gösteriyorsa, HTTP uygulaması paketi serbest bırakmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1376">If the return status indicates an error, the HTTP application must release the packet.</span></span>

<span data-ttu-id="c8f61-1377">Geri çağırma NX_WEB_HTTP_CALLBACK_COMPLETED döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1377">The callback should return NX_WEB_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="c8f61-1378">Daha ayrıntılı bir örnek için bkz. *nx_web_http_server_callback_generate_response_header ()* .</span><span class="sxs-lookup"><span data-stu-id="c8f61-1378">See *nx_web_http_server_callback_generate_response_header()* for a more detailed example.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1379">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1379">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1380">**server_ptr** HTTP sunucu denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1380">**server_ptr** Pointer to HTTP Server control block</span></span>
- <span data-ttu-id="c8f61-1381">**packet_ptr** Gönderilmek üzere paket işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1381">**packet_ptr** Pointer to the packet to send</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1382">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1382">Return Values</span></span>

- <span data-ttu-id="c8f61-1383">**NX_SUCCESS** (0x00) http sunucusu paketini başarıyla gönderdi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1383">**NX_SUCCESS** (0x00) Successfully sent HTTP Server packet</span></span>
- <span data-ttu-id="c8f61-1384">**NX_PTR_ERROR** (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1384">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1385">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1385">Allowed From</span></span>

<span data-ttu-id="c8f61-1386">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1386">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1387">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1387">Example</span></span>

```C
/* The packet is appended with HTTP header and data
    and is ready to send to the Client directly. */
status = nx_web_http_server_callback_packet_send(server_ptr, packet_ptr);

if (status != NX_SUCCESS)
{
    nx_packet_release(packet_ptr);
}

return(NX_WEB_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_web_http_server_callback_response_send"></a><span data-ttu-id="c8f61-1388">nx_web_http_server_callback_response_send</span><span class="sxs-lookup"><span data-stu-id="c8f61-1388">nx_web_http_server_callback_response_send</span></span>

<span data-ttu-id="c8f61-1389">Geri çağırma işlevinden yanıt gönder</span><span class="sxs-lookup"><span data-stu-id="c8f61-1389">Send response from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1390">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1390">Prototype</span></span>

```C
UINT nx_web_http_server_callback_response_send(
    NX_WEB_HTTP_SERVER *server_ptr,
    CHAR *header,
    CHAR *information,
    CHAR additional_info);
```

### <a name="description"></a><span data-ttu-id="c8f61-1391">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1391">Description</span></span>

<span data-ttu-id="c8f61-1392">Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1392">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="c8f61-1393">Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1393">This is typically used to send custom responses associated with GET/POST requests.</span></span> <span data-ttu-id="c8f61-1394">Bu işlev kullanıldığında, geri çağırma yordamının NX_WEB_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1394">Note that if this function is used, the callback routine must return the status of NX_WEB_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="c8f61-1395">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1395">This service is deprecated.</span></span> <span data-ttu-id="c8f61-1396">Geliştiricilerin *nx_web_http_server_callback_response_send_extended ()* kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1396">Developers are encouraged to use *nx_web_http_server_callback_response_send_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1397">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1397">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1398">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1398">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1399">**üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1399">**header** Pointer to the response header string.</span></span>
- <span data-ttu-id="c8f61-1400">**bilgi** Bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1400">**information** Pointer to the information string.</span></span>
- <span data-ttu-id="c8f61-1401">**additional_info** Ek bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1401">**additional_info** Pointer to the additional information string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1402">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1402">Return Values</span></span>

- <span data-ttu-id="c8f61-1403">**NX_SUCCESS** (0x00) http sunucusu yanıtı başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1403">**NX_SUCCESS** (0x00) Successfully sent HTTP Server response</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1404">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1404">Allowed From</span></span>

<span data-ttu-id="c8f61-1405">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1405">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1406">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1406">Example</span></span>

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
            a resource not found response. */
        nx_web_http_server_callback_response_send(server_ptr,
            "HTTP/1.0 404 ",
            "NetX HTTP Server unable to find file: ",
            resource);

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_callback_response_send_extended"></a><span data-ttu-id="c8f61-1407">nx_web_http_server_callback_response_send_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-1407">nx_web_http_server_callback_response_send_extended</span></span>

<span data-ttu-id="c8f61-1408">Geri çağırma işlevinden yanıt gönder</span><span class="sxs-lookup"><span data-stu-id="c8f61-1408">Send response from callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1409">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1409">Prototype</span></span>

```C
UINT nx_web_http_server_callback_response_send_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    CHAR *header, UINT header_length,
    CHAR *information,
    UINT information_length,
    CHAR additional_info,
    UINT additional_info_length);
```

### <a name="description"></a><span data-ttu-id="c8f61-1410">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1410">Description</span></span>

<span data-ttu-id="c8f61-1411">Bu hizmet, sağlanan yanıt bilgilerini uygulamanın geri arama yordamından gönderir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1411">This service sends the supplied response information from the application’s callback routine.</span></span> <span data-ttu-id="c8f61-1412">Bu, genellikle GET/POST istekleri ile ilişkili özel yanıtları göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1412">This is typically used to send custom responses associated with GET/POST requests.</span></span> <span data-ttu-id="c8f61-1413">Bu işlev kullanıldığında, geri çağırma yordamının NX_WEB_HTTP_CALLBACK_COMPLETED durumunu döndürmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1413">Note that if this function is used, the callback routine must return the status of NX_WEB_HTTP_CALLBACK_COMPLETED.</span></span>

<span data-ttu-id="c8f61-1414">Üstbilgi, bilgi ve additional_info dizeleri NULL sonlandırılmış olmalıdır ve her bir dizenin uzunluğu bağımsız değişken listesinde belirtilen uzunlukla eşleşir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1414">The strings of header, information and additional_info must be NULL-terminated and length of each string matches the length specified in the argument list.</span></span>

<span data-ttu-id="c8f61-1415">Bu hizmet *nx_web_http_server_callback_response_send*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1415">This service replaces *nx_web_http_server_callback_response_send*().</span></span> <span data-ttu-id="c8f61-1416">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1416">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1417">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1417">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1418">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1418">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1419">**üst bilgi** Yanıt üst bilgisi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1419">**header** Pointer to the response header string.</span></span>
- <span data-ttu-id="c8f61-1420">**header_length** Yanıt üst bilgisi dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1420">**header_length** Length of the response header string.</span></span>
- <span data-ttu-id="c8f61-1421">**bilgi** Bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1421">**information** Pointer to the information string.</span></span>
- <span data-ttu-id="c8f61-1422">**Information_length** Bilgi dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1422">**Information_length** Length of the information string.</span></span>
- <span data-ttu-id="c8f61-1423">**additional_info** Ek bilgi dizesinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1423">**additional_info** Pointer to the additional information string.</span></span>
- <span data-ttu-id="c8f61-1424">**additional_info_length** Ek bilgi dizesinin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1424">**additional_info_length** Length of the additional information string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1425">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1425">Return Values</span></span>

- <span data-ttu-id="c8f61-1426">**NX_SUCCESS** (0x00) http sunucusu yanıtı başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1426">**NX_SUCCESS** (0x00) Successfully sent HTTP Server response</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1427">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1427">Allowed From</span></span>

<span data-ttu-id="c8f61-1428">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1428">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1429">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1429">Example</span></span>

```C
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    /* Look for the test resource! */
    if ((request_type == NX_WEB_HTTP_SERVER_GET_REQUEST) &&
        (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
            a resource not found response. */
        nx_web_http_server_callback_response_send_extended(server_ptr,
            "HTTP/1.0 404 ",
            sizeof("HTTP/1.0 404 ") – 1,
            "NetX HTTP Server unable to find file: ",
            sizeof("NetX HTTP Server unable to find file: ") – 1,
            resource, strlen(resource));

        /* Return completion status. */
        return(NX_WEB_HTTP_CALLBACK_COMPLETED);
    }

    return(NX_SUCCESS);
}
```

## <a name="nx_web_http_server_content_get"></a><span data-ttu-id="c8f61-1430">nx_web_http_server_content_get</span><span class="sxs-lookup"><span data-stu-id="c8f61-1430">nx_web_http_server_content_get</span></span>

<span data-ttu-id="c8f61-1431">İstekten içerik al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1431">Get content from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1432">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1432">Prototype</span></span>

```C
UINT nx_web_http_server_content_get(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr,
    ULONG byte_offset,
    CHAR *destination_ptr,
    UINT destination_size,
    UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="c8f61-1433">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1433">Description</span></span>

<span data-ttu-id="c8f61-1434">Bu hizmet, POST veya PUT HTTP Client isteğinden belirtilen miktarda içeriği almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1434">This service attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="c8f61-1435">Bu, HTTP sunucusu oluşturma (*nx_web_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1435">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1436">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1436">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1437">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1437">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1438">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1438">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="c8f61-1439">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1439">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="c8f61-1440">**byte_offset** İçerik alanına kaydırılacağı bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1440">**byte_offset** Number of bytes to offset into the content area.</span></span>
- <span data-ttu-id="c8f61-1441">**destination_ptr** İçerik için hedef alana yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1441">**destination_ptr** Pointer to the destination area for the content.</span></span>
- <span data-ttu-id="c8f61-1442">**destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1442">**destination_size** Maximum number of bytes available in the destination area.</span></span>
- <span data-ttu-id="c8f61-1443">**actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1443">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1444">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1444">Return Values</span></span>

- <span data-ttu-id="c8f61-1445">**NX_SUCCESS** (0x00) başarılı http sunucusu içerik al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1445">**NX_SUCCESS** (0x00) Successful HTTP Server content Get</span></span>
- <span data-ttu-id="c8f61-1446">**NX_WEB_HTTP_ERROR** (0x30000) http sunucusu iç hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-1446">**NX_WEB_HTTP_ERROR** (0x30000) HTTP Server internal error</span></span>
- <span data-ttu-id="c8f61-1447">**NX_WEB_HTTP_DATA_END** (0x30007) Istek içeriğinin sonu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1447">**NX_WEB_HTTP_DATA_END** (0x30007) End of request content</span></span>
- <span data-ttu-id="c8f61-1448">**NX_WEB_HTTP_TIMEOUT** (0x30001) sonraki içerik paketini alma sırasında http sunucusu zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1448">**NX_WEB_HTTP_TIMEOUT** (0x30001) HTTP Server timeout in getting next packet of content</span></span>
- <span data-ttu-id="c8f61-1449">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1449">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1450">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1450">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1451">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1451">Allowed From</span></span>

<span data-ttu-id="c8f61-1452">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1452">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1453">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1453">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, retrieve up to 100 bytes of content starting at offset
    0. */
status = nx_web_http_server_content_get(&my_server, packet_ptr,
    0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, "my_buffer" contains "actual_size" bytes of
    request content. */
```

## <a name="nx_web_http_server_content_get_extended"></a><span data-ttu-id="c8f61-1454">nx_web_http_server_content_get_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-1454">nx_web_http_server_content_get_extended</span></span>

<span data-ttu-id="c8f61-1455">İstekten içerik al/sıfır uzunlukta Içerik uzunluğunu destekler</span><span class="sxs-lookup"><span data-stu-id="c8f61-1455">Get content from the request/supports zero length Content Length</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1456">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1456">Prototype</span></span>

```C
UINT nx_web_http_server_content_get_extended(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET *packet_ptr,
    ULONG byte_offset,
    CHAR *destination_ptr,
    UINT destination_size,
    UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="c8f61-1457">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1457">Description</span></span>

<span data-ttu-id="c8f61-1458">Bu hizmet *nx_web_http_server_content_get ()* ile neredeyse aynıdır; POST veya PUT HTTP Client isteğinden belirtilen miktarda içeriği almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1458">This service is almost identical to *nx_web_http_server_content_get()*; it attempts to retrieve the specified amount of content from the POST or PUT HTTP Client request.</span></span> <span data-ttu-id="c8f61-1459">Ancak, geçerli bir istek olarak sıfır değeri (' boş istek ') Içerik uzunluğundaki istekleri işler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1459">However it handles requests with Content Length of zero value (‘empty request’) as a valid request.</span></span> <span data-ttu-id="c8f61-1460">Bu, HTTP sunucusu oluşturma (*nx_web_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1460">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

<span data-ttu-id="c8f61-1461">Bu hizmet *nx_web_http_server_content_get*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1461">This service replaces *nx_web_http_server_content_get*().</span></span> <span data-ttu-id="c8f61-1462">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1462">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1463">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1463">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1464">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1464">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1465">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1465">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="c8f61-1466">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1466">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="c8f61-1467">**byte_offset** İçerik alanına kaydırılacağı bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1467">**byte_offset** Number of bytes to offset into the content area.</span></span>
- <span data-ttu-id="c8f61-1468">**destination_ptr** İçerik için hedef alana yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1468">**destination_ptr** Pointer to the destination area for the content.</span></span>
- <span data-ttu-id="c8f61-1469">**destination_size** Hedef alanda kullanılabilir en fazla bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1469">**destination_size** Maximum number of bytes available in the destination area.</span></span>
- <span data-ttu-id="c8f61-1470">**actual_size** Kopyalanmış içeriğin gerçek boyutuna ayarlanacak hedef değişkene yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1470">**actual_size** Pointer to the destination variable that will be set to the actual size of the content copied.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1471">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1471">Return Values</span></span>

- <span data-ttu-id="c8f61-1472">**NX_SUCCESS** (0x00) başarılı http içerik al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1472">**NX_SUCCESS** (0x00) Successful HTTP content get</span></span>
- <span data-ttu-id="c8f61-1473">**NX_WEB_HTTP_ERROR** (0x30000) http sunucusu iç hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-1473">**NX_WEB_HTTP_ERROR** (0x30000) HTTP Server internal error</span></span>
- <span data-ttu-id="c8f61-1474">**NX_WEB_HTTP_DATA_END** (0x30007) Istek içeriğinin sonu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1474">**NX_WEB_HTTP_DATA_END** (0x30007) End of request content</span></span>
- <span data-ttu-id="c8f61-1475">**NX_WEB_HTTP_TIMEOUT** (0x30001) sonraki paketi alma sırasında http sunucusu zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1475">**NX_WEB_HTTP_TIMEOUT** (0x30001) HTTP Server timeout in getting next packet</span></span>
- <span data-ttu-id="c8f61-1476">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1476">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1477">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1477">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1478">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1478">Allowed From</span></span>

<span data-ttu-id="c8f61-1479">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1479">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1480">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1480">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, retrieve up to 100 bytes of content starting at offset
    0. */
status = nx_web_http_server_content_get_extended(&my_server, packet_ptr,
    0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, "my_buffer" contains "actual_size" bytes of
    request content. */
```

## <a name="nx_web_http_server_content_length_get"></a><span data-ttu-id="c8f61-1481">nx_web_http_server_content_length_get</span><span class="sxs-lookup"><span data-stu-id="c8f61-1481">nx_web_http_server_content_length_get</span></span>

<span data-ttu-id="c8f61-1482">İstekteki içerik uzunluğunu al/sıfır değerinin Içerik uzunluğunu destekler</span><span class="sxs-lookup"><span data-stu-id="c8f61-1482">Get length of content in the request/supports Content Length of zero value</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1483">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1483">Prototype</span></span>

```C
UINT nx_web_http_server_content_length_get(
    NX_PACKET *packet_ptr,
    UINT *content_length);
```

### <a name="description"></a><span data-ttu-id="c8f61-1484">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1484">Description</span></span>

<span data-ttu-id="c8f61-1485">Bu hizmet, sağlanan paketteki HTTP içerik uzunluğunu almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1485">This service attempts to retrieve the HTTP content length in the supplied packet.</span></span> <span data-ttu-id="c8f61-1486">Dönüş değeri başarıyla tamamlanma durumunu gösterir ve content_length giriş İşaretçisinde gerçek uzunluk değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1486">The return value indicates successful completion status and the actual length value is returned in the input pointer content_length.</span></span> <span data-ttu-id="c8f61-1487">HTTP içeriği/Içerik uzunluğu = 0 yoksa, bu yordam yine de başarılı bir tamamlanma durumu döndürür ve content_length giriş işaretçisi geçerli bir uzunluğa (sıfır) işaret eder.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1487">If there is no HTTP content/Content Length = 0, this routine still returns a successful completion status and the content_length input pointer points to a valid length (zero).</span></span> <span data-ttu-id="c8f61-1488">Bu, HTTP sunucusu oluşturma (*nx_web_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1488">It should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1489">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1489">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1490">**packet_ptr** HTTP Istemcisi istek paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1490">**packet_ptr** Pointer to the HTTP Client request packet.</span></span> <span data-ttu-id="c8f61-1491">Bu paketin istek bildirimi geri araması tarafından yayımlanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1491">Note that this packet must not be released by the request notify callback.</span></span>
- <span data-ttu-id="c8f61-1492">**CONTENT_LENGTH** Içerik uzunluğu alanından alınan değer işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1492">**content_length** Pointer to value retrieved from Content Length field</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1493">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1493">Return Values</span></span>

- <span data-ttu-id="c8f61-1494">**NX_SUCCESS** (0x00) başarılı http sunucusu Içerik uzunluğu al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1494">**NX_SUCCESS** (0x00) Successful HTTP Server Content Length Get</span></span>
- <span data-ttu-id="c8f61-1495">**NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000f) yanlış http üst bilgi biçimi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1495">**NX_WEB_HTTP_INCOMPLETE_PUT_ERROR** (0x3000F) Improper HTTP header format</span></span>
- <span data-ttu-id="c8f61-1496">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1496">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1497">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1497">Allowed From</span></span>

<span data-ttu-id="c8f61-1498">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1498">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1499">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1499">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, get the content length of the HTTP Client request. */

ULONG content_length;
status = nx_web_http_server_content_length_get(packet_ptr, &content_length);

/* If the "status" variable indicates successful completion, the "length"
    Variable contains the length of the HTTP Client request content area. */
```

## <a name="nx_web_http_server_create"></a><span data-ttu-id="c8f61-1500">nx_web_http_server_create</span><span class="sxs-lookup"><span data-stu-id="c8f61-1500">nx_web_http_server_create</span></span>

<span data-ttu-id="c8f61-1501">HTTP sunucusu örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1501">Create an HTTP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1502">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1502">Prototype</span></span>

```C
UINT nx_web_http_server_create(NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *http_server_name, NX_IP *ip_ptr, UINT server_port,
    FX_MEDIA *media_ptr, VOID *stack_ptr, ULONG stack_size,
    NX_PACKET_POOL *pool_ptr,
    UINT (*authentication_check)(NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type, CHAR *resource, CHAR **name,
        CHAR **password, CHAR **realm),
    UINT (*request_notify)(NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type, CHAR *resource, NX_PACKET *packet_ptr));
```

### <a name="description"></a><span data-ttu-id="c8f61-1503">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1503">Description</span></span>

<span data-ttu-id="c8f61-1504">Bu hizmet kendi ThreadX iş parçacığı bağlamında çalışan bir HTTP sunucu örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1504">This service creates an HTTP Server instance, which runs in the context of its own ThreadX thread.</span></span> <span data-ttu-id="c8f61-1505">İsteğe bağlı *authentication_check* ve *request_notify* uygulama GERI çağırma yordamları, HTTP sunucusunun temel işlemleri üzerinde uygulama yazılım denetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1505">The optional *authentication_check* and *request_notify* application callback routines give the application software control over the basic operations of the HTTP Server.</span></span>

<span data-ttu-id="c8f61-1506">Bu hizmet, hem düz metin HTTP sunucuları hem de TLS ile güvenli HTTPS sunucuları oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1506">This service is used to create both plaintext HTTP servers and TLS-secured HTTPS servers.</span></span> <span data-ttu-id="c8f61-1507">TLS kullanarak HTTPS 'yi etkinleştirmek için *nx_web_http_server_secure_configure ()* hizmetine bakın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1507">To enable HTTPS using TLS, see the service *nx_web_http_server_secure_configure()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1508">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1508">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1509">**http_server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1509">**http_server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1510">**http_server_name** HTTP sunucusu adı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1510">**http_server_name** Pointer to HTTP Server’s name.</span></span>
- <span data-ttu-id="c8f61-1511">**ip_ptr** Daha önce oluşturulan IP örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1511">**ip_ptr** Pointer to previously created IP instance.</span></span>
- <span data-ttu-id="c8f61-1512">**SERVER_PORT** Sunucu örneği için TCP dinleme bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1512">**server_port** TCP listening port for server instance.</span></span>
- <span data-ttu-id="c8f61-1513">**media_ptr** Daha önce oluşturulan FileX medya örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1513">**media_ptr** Pointer to previously created FileX media instance.</span></span>
- <span data-ttu-id="c8f61-1514">**stack_ptr** HTTP sunucusu iş parçacığı yığın alanı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1514">**stack_ptr** Pointer to HTTP Server thread stack area.</span></span>
- <span data-ttu-id="c8f61-1515">**stack_size** HTTP sunucusu iş parçacığı yığın boyutu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1515">**stack_size** Pointer to HTTP Server thread stack size.</span></span>
- <span data-ttu-id="c8f61-1516">**authentication_check** Uygulamanın kimlik doğrulama denetimi yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1516">**authentication_check** Function pointer to application’s authentication checking routine.</span></span> <span data-ttu-id="c8f61-1517">Belirtilmişse, bu yordam her HTTP Istemci isteği için çağırılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1517">If specified, this routine is called for each HTTP Client request.</span></span> <span data-ttu-id="c8f61-1518">Bu parametre NULL ise, kimlik doğrulaması gerçekleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1518">If this parameter is NULL, no authentication will be performed.</span></span> <span data-ttu-id="c8f61-1519">Bu parametre kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1519">This parameter is deprecated.</span></span> <span data-ttu-id="c8f61-1520">Bunun yerine *nx_web_http_server_authenticate_check_set*() çağırın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1520">Call *nx_web_http_server_authenticate_check_set*() instead.</span></span>
- <span data-ttu-id="c8f61-1521">**request_notify** Uygulamanın istek bildirim yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1521">**request_notify** Function pointer to application’s request notify routine.</span></span> <span data-ttu-id="c8f61-1522">Belirtilmişse, bu yordam isteğin HTTP sunucu işlemeden önce çağırılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1522">If specified, this routine is called prior to the HTTP server processing of the request.</span></span> <span data-ttu-id="c8f61-1523">Bu, HTTP Istemci isteği tamamlanmadan önce kaynak adının yeniden yönlendirilmesine veya bir kaynak içindeki alanların güncelleştirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1523">This allows the resource name to be redirected or fields within a resource to be updated prior to completing the HTTP Client request.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1524">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1524">Return Values</span></span>

- <span data-ttu-id="c8f61-1525">**NX_SUCCESS** (0x00) başarılı http sunucusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1525">**NX_SUCCESS** (0x00) Successful HTTP Server create.</span></span>
- <span data-ttu-id="c8f61-1526">NX_PTR_ERROR (0x07) geçersiz HTTP sunucusu, IP, medya, yığın veya paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1526">NX_PTR_ERROR (0x07) Invalid HTTP Server, IP, media, stack, or packet pool pointer.</span></span>
- <span data-ttu-id="c8f61-1527">NX_WEB_HTTP_POOL_ERROR (0x30009) havuzun paket yükü, tüm HTTP isteklerini içerecek kadar büyük değil.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1527">NX_WEB_HTTP_POOL_ERROR (0x30009) Packet payload of pool is not large enough to contain complete HTTP request.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1528">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1528">Allowed From</span></span>

<span data-ttu-id="c8f61-1529">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1529">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1530">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1530">Example</span></span>

```C
/* Create an HTTP Server instance called "my_server." */
status = nx_web_http_server_create(&my_server, "my server", &ip_0,
    NX_WEB_HTTPS_SERVER_PORT, &ram_disk,
    stack_ptr, stack_size, &pool_0,
    my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_web_http_server_delete"></a><span data-ttu-id="c8f61-1531">nx_web_http_server_delete</span><span class="sxs-lookup"><span data-stu-id="c8f61-1531">nx_web_http_server_delete</span></span>

<span data-ttu-id="c8f61-1532">HTTP sunucusu örneğini silme</span><span class="sxs-lookup"><span data-stu-id="c8f61-1532">Delete an HTTP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1533">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1533">Prototype</span></span>

```C
UINT nx_web_http_server_delete(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="c8f61-1534">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1534">Description</span></span>

<span data-ttu-id="c8f61-1535">Bu hizmet, önceden oluşturulmuş bir HTTP sunucusu örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1535">This service deletes a previously created HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1536">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1536">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1537">**http_server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1537">**http_server_ptr** Pointer to HTTP Server control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1538">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1538">Return Values</span></span>

- <span data-ttu-id="c8f61-1539">**NX_SUCCESS** (0x00) başarılı http sunucusu silme</span><span class="sxs-lookup"><span data-stu-id="c8f61-1539">**NX_SUCCESS** (0x00) Successful HTTP Server delete</span></span>
- <span data-ttu-id="c8f61-1540">NX_PTR_ERROR (0x07) geçersiz HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1540">NX_PTR_ERROR (0x07) Invalid HTTP Server pointer</span></span>
- <span data-ttu-id="c8f61-1541">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1541">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1542">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1542">Allowed From</span></span>

<span data-ttu-id="c8f61-1543">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1543">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1544">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1544">Example</span></span>

```C
/* Delete the HTTP Server instance called "my_server." */
status = nx_web_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_web_http_server_get_entity_content"></a><span data-ttu-id="c8f61-1545">nx_web_http_server_get_entity_content</span><span class="sxs-lookup"><span data-stu-id="c8f61-1545">nx_web_http_server_get_entity_content</span></span>

<span data-ttu-id="c8f61-1546">Varlık verilerinin konumunu ve uzunluğunu alma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1546">Retrieve the location and length of entity data</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1547">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1547">Prototype</span></span>

```C
UINT nx_web_http_server_get_entity_content(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    ULONG *available_offset,
    ULONG *available_length);
```

### <a name="description"></a><span data-ttu-id="c8f61-1548">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1548">Description</span></span>

<span data-ttu-id="c8f61-1549">Bu hizmet, alınan Istemci iletilerindeki geçerli çok parçalı varlıktaki verilerin başlangıç konumunu ve sınır dizesini dahil olmayan veri uzunluğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1549">This service determines the location of the start of data within the current multipart entity in the received Client messages, and the length of data not including the boundary string.</span></span> <span data-ttu-id="c8f61-1550">Dahili olarak, HTTP sunucusu, bu işlevin birden çok varlık içeren iletiler için aynı Istemci veri biriminde tekrar çağrılabilmesi için kendi uzaklıklarını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1550">Internally, the HTTP server updates its own offsets so that this function can be called again on the same Client datagram for messages with multiple entities.</span></span> <span data-ttu-id="c8f61-1551">Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1551">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

<span data-ttu-id="c8f61-1552">Bu hizmeti kullanmak için NX_WEB_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1552">Note that NX_WEB_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span> <span data-ttu-id="c8f61-1553">Ayrıca, uygulamanın packet_pptr tarafından işaret edilen paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1553">Also note that the application should not release the packet pointed to by packet_pptr.</span></span> <span data-ttu-id="c8f61-1554">Bu, HTTP sunucusu tarafından dahili olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1554">This is done internally by the HTTP server.</span></span>

<span data-ttu-id="c8f61-1555">Daha fazla ayrıntı için bkz. *nx_web_http_server_get_entity_header ()* .</span><span class="sxs-lookup"><span data-stu-id="c8f61-1555">See *nx_web_http_server_get_entity_header()* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1556">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1556">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1557">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1557">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="c8f61-1558">**packet_pptr** Paket işaretçisinin konumu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1558">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="c8f61-1559">Uygulamanın bu paketi serbest bırakmadığını unutmayın</span><span class="sxs-lookup"><span data-stu-id="c8f61-1559">Note that the application should not release this packet</span></span>
- <span data-ttu-id="c8f61-1560">**available_offset** Paket önüne işaretçisinden varlık verilerinin uzaklığa yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1560">**available_offset** Pointer to offset of entity data from the packet prepend pointer</span></span>
- <span data-ttu-id="c8f61-1561">**available_length** Varlık verisi uzunluğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1561">**available_length** Pointer to length of entity data</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1562">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1562">Return Values</span></span>

- <span data-ttu-id="c8f61-1563">**NX_SUCCESS** (0x00) varlık içeriğinin boyutunu ve konumunu başarıyla aldı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1563">**NX_SUCCESS** (0x00) Successfully retrieved size and location of entity content</span></span>
- <span data-ttu-id="c8f61-1564">HTTP sunucusu iç parçalı işaretçiler için **NX_WEB_HTTP_BOUNDARY_ALREADY_FOUND** (0x30016) içeriği zaten var</span><span class="sxs-lookup"><span data-stu-id="c8f61-1564">**NX_WEB_HTTP_BOUNDARY_ALREADY_FOUND** (0x30016) Content for the HTTP server internal multipart markers is already found</span></span>
- <span data-ttu-id="c8f61-1565">NX_WEB_HTTP_ERROR (0x30000) HTTP sunucusu iç hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-1565">NX_WEB_HTTP_ERROR (0x30000) HTTP Server internal error</span></span>
- <span data-ttu-id="c8f61-1566">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1566">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1567">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1567">Allowed From</span></span>

<span data-ttu-id="c8f61-1568">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1568">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1569">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1569">Example</span></span>

```C
NX_WEB_HTTP_SERVER my_server;
UINT offset, length;
NX_PACKET *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
    the entity header to determine details about the multipart data. If
    successful, it then calls this service to get the location of entity data: */
status = nx_web_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
    &length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
    entity data. */
```

## <a name="nx_web_http_server_get_entity_header"></a><span data-ttu-id="c8f61-1570">nx_web_http_server_get_entity_header</span><span class="sxs-lookup"><span data-stu-id="c8f61-1570">nx_web_http_server_get_entity_header</span></span>

<span data-ttu-id="c8f61-1571">Varlık üstbilgisinin içeriğini alma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1571">Retrieve the contents of entity header</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1572">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1572">Prototype</span></span>

```C
UINT nx_web_http_server_get_entity_header(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_pptr,
    UCHAR *entity_header_buffer,
    ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="c8f61-1573">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1573">Description</span></span>

<span data-ttu-id="c8f61-1574">Bu hizmet varlık üstbilgisini belirtilen arabelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1574">This service retrieves the entity header into the specified buffer.</span></span> <span data-ttu-id="c8f61-1575">Dahili HTTP sunucusu, birden çok varlık üst bilgilerine sahip bir Istemci veri biriminde bir sonraki çok parçalı varlığı bulmak için kendi işaretçilerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1575">Internally HTTP Server updates its own pointers to locate the next multipart entity in a Client datagram with multiple entity headers.</span></span> <span data-ttu-id="c8f61-1576">Paket işaretçisi, Istemci iletisinin çoklu paket veri birimi olduğu bir sonraki pakete güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1576">The packet pointer is updated to the next packet where the Client message is a multi-packet datagram.</span></span>

<span data-ttu-id="c8f61-1577">Bu hizmeti kullanmak için NX_WEB_HTTP_MULTIPART_ENABLE etkinleştirilmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1577">Note that NX_WEB_HTTP_MULTIPART_ENABLE must be enabled to use this service.</span></span> <span data-ttu-id="c8f61-1578">Ayrıca, uygulamanın packet_pptr tarafından işaret edilen paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1578">Note also that the application should not release the packet pointed to by packet_pptr.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1579">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1579">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1580">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1580">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="c8f61-1581">**packet_pptr** Paket işaretçisinin konumu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1581">**packet_pptr** Pointer to location of packet pointer.</span></span> <span data-ttu-id="c8f61-1582">Uygulamanın bu paketi serbest bırakmadığını unutmayın</span><span class="sxs-lookup"><span data-stu-id="c8f61-1582">Note that the application should not release this packet</span></span>
- <span data-ttu-id="c8f61-1583">**entity_header_buffer** Varlık üstbilgisinin depolanacak konuma işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1583">**entity_header_buffer** Pointer to location to store entity header</span></span>
- <span data-ttu-id="c8f61-1584">**Buffer_size** Giriş arabelleğinin boyutu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1584">**buffer_size** Size of input buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1585">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1585">Return Values</span></span>

- <span data-ttu-id="c8f61-1586">**NX_SUCCESS** (0x00) varlık üstbilgisi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1586">**NX_SUCCESS** (0x00) Successfully retrieved entity Header</span></span>
- <span data-ttu-id="c8f61-1587">**NX_WEB_HTTP_NOT_FOUND** (0x30006) varlık üst bilgisi alanı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1587">**NX_WEB_HTTP_NOT_FOUND** (0x30006) Entity header field not found</span></span>
- <span data-ttu-id="c8f61-1588">**NX_WEB_HTTP_TIMEOUT** (0x30001) çok paket istemci iletisi için sonraki paketi almak üzere zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1588">**NX_WEB_HTTP_TIMEOUT** (0x30001) Time expired to receive next packet for multipacket client message</span></span>
- <span data-ttu-id="c8f61-1589">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1589">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1590">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1590">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="c8f61-1591">NX_WEB_HTTP_ERROR (0x30000) Iç HTTP hatası</span><span class="sxs-lookup"><span data-stu-id="c8f61-1591">NX_WEB_HTTP_ERROR (0x30000) Internal HTTP error</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1592">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1592">Allowed From</span></span>

<span data-ttu-id="c8f61-1593">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1593">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1594">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1594">Example</span></span>

```C
/* Buffer to hold data we are extracting from the request. */
UCHAR buffer[1440];

/* *my_request_notify()* is the application request notify callback
    registered with the HTTP server in *nx_web_http_server_create()*,
    creates a response to the received Client request. */
UINT my_request_notify(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
    CHAR *resource, NX_PACKET *packet_ptr)
{
    UINT offset, length;
    NX_PACKET *response_pkt;

    /* Process multipart data. */
    if(request_type == NX_WEB_HTTP_SERVER_POST_REQUEST)
    {
        /* Get the content header. */
        while(nx_web_http_server_get_entity_header(server_ptr, &packet_ptr, buffer,
            sizeof(buffer)) == NX_SUCCESS)
        {
            /* Header obtained successfully. Get the content data location. */
            while(nx_web_http_server_get_entity_content(server_ptr,
                &packet_ptr, &offset, &length) == NX_SUCCESS)
            {
                /* Write content data to buffer. */
                nx_packet_data_extract_offset(packet_ptr, offset, buffer, length,
                    &length);
                buffer[length] = 0;
            }
        }

        /* Generate HTTP header. */
        status = nx_web_http_server_callback_generate_response_header(server_ptr,
            &response_pkt, NX_WEB_HTTP_STATUS_OK, 800, "text/html",
            "Server: NetX WEB HTTP 5.10\r\n");

        if(status == NX_SUCCESS)
        {
            if(nx_web_http_server_callback_packet_send(server_ptr, response_pkt) !=
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
    return(NX_WEB_HTTP_CALLBACK_COMPLETED);
}

```

## <a name="nx_web_http_server_gmt_callback_set"></a><span data-ttu-id="c8f61-1595">nx_web_http_server_gmt_callback_set</span><span class="sxs-lookup"><span data-stu-id="c8f61-1595">nx_web_http_server_gmt_callback_set</span></span>

<span data-ttu-id="c8f61-1596">GMT Tarih ve saati almak için geri aramayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c8f61-1596">Set the callback to obtain GMT date and time</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1597">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1597">Prototype</span></span>

```C
UINT nx_web_http_server_gmt_callback_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    VOID (*gmt_get)(NX_WEB_HTTP_SERVER_DATE *date);
```

### <a name="description"></a><span data-ttu-id="c8f61-1598">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1598">Description</span></span>

<span data-ttu-id="c8f61-1599">Bu hizmet, daha önce oluşturulmuş bir HTTP sunucusu ile GMT Tarih ve saati alacak şekilde geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1599">This service sets the callback to obtain GMT date and time with a previously created HTTP server.</span></span> <span data-ttu-id="c8f61-1600">Bu hizmet HTTP sunucusu, Istemciye HTTP sunucu yanıtlarında bir üst bilgi oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1600">This service is invoked with the HTTP server is creating a header in HTTP server responses to the Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1601">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1601">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1602">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1602">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="c8f61-1603">**gmt_get** GMT geri çağırması işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1603">**gmt_get** Pointer to GMT callback</span></span>
- <span data-ttu-id="c8f61-1604">**Tarih** Alınan tarihin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1604">**date** Pointer to the date retrieved</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1605">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1605">Return Values</span></span>

- <span data-ttu-id="c8f61-1606">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1606">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8f61-1607">NX_PTR_ERROR (0x07) geçersiz paket veya parametre işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1607">NX_PTR_ERROR (0x07) Invalid packet or parameter pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1608">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1608">Allowed From</span></span>

<span data-ttu-id="c8f61-1609">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1609">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1610">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1610">Example</span></span>

```C
NX_WEB_HTTP_SERVER my_server;

VOID get_gmt(NX_WEB_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_web_http_server_create(),
    and before starting HTTP services when nx_web_http_server_start() is called,
    set the GMT retrieve callback: */
status = nx_web_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
    response header date. */
```

## <a name="nx_web_http_server_invalid_userpassword_notify_set"></a><span data-ttu-id="c8f61-1611">nx_web_http_server_invalid_userpassword_notify_set</span><span class="sxs-lookup"><span data-stu-id="c8f61-1611">nx_web_http_server_invalid_userpassword_notify_set</span></span>

<span data-ttu-id="c8f61-1612">Geçersiz Kullanıcı/parola işlemek için geri çağırma ayarla</span><span class="sxs-lookup"><span data-stu-id="c8f61-1612">Set the callback to handle invalid user/password</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1613">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1613">Prototype</span></span>

```C
UINT nx_web_http_server_invalid_userpassword_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*invalid_username_password_callback)
        (CHAR *resource,
        ULONG client_address,
        UINT request_type));
```

### <a name="description"></a><span data-ttu-id="c8f61-1614">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1614">Description</span></span>

<span data-ttu-id="c8f61-1615">Bu hizmet, bir Istemci alma, yerleştirme veya silme isteğinde, Özet veya temel kimlik doğrulamasından göre geçersiz bir Kullanıcı adı ve parola alındığında çağrılan geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1615">This service sets the callback invoked when an invalid username and password is received in a Client get, put or delete request, either by digest or basic authentication.</span></span> <span data-ttu-id="c8f61-1616">HTTP sunucusu daha önce oluşturulmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1616">The HTTP server must be previously created.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1617">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1617">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1618">**server_ptr** HTTP sunucusu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1618">**server_ptr** Pointer to HTTP Server</span></span>
- <span data-ttu-id="c8f61-1619">**invalid_username_password_callback** Geçersiz Kullanıcı/geçiş geri çağırması işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1619">**invalid_username_password_callback** Pointer to invalid user/pass callback</span></span>
- <span data-ttu-id="c8f61-1620">**kaynak** İstemci tarafından belirtilen kaynak işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1620">**resource** Pointer to the resource specified by the client</span></span>
- <span data-ttu-id="c8f61-1621">**client_address** İstemci adresi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1621">**client_address** Client address</span></span>
- <span data-ttu-id="c8f61-1622">**request_type** İstemci isteği türünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1622">**request_type** Indicates client request type.</span></span> <span data-ttu-id="c8f61-1623">Belki:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1623">May be:</span></span>
  - <span data-ttu-id="c8f61-1624">*NX_WEB_HTTP_SERVER_GET_REQUEST*</span><span class="sxs-lookup"><span data-stu-id="c8f61-1624">*NX_WEB_HTTP_SERVER_GET_REQUEST*</span></span>
  - <span data-ttu-id="c8f61-1625">*NX_WEB_HTTP_SERVER_POST_REQUEST NX_WEB_HTTP_SERVER_HEAD_REQUEST*</span><span class="sxs-lookup"><span data-stu-id="c8f61-1625">*NX_WEB_HTTP_SERVER_POST_REQUEST NX_WEB_HTTP_SERVER_HEAD_REQUEST*</span></span>
  - <span data-ttu-id="c8f61-1626">*NX_WEB_HTTP_SERVER_PUT_REQUEST NX_WEB_HTTP_SERVER_DELETE_REQUEST*</span><span class="sxs-lookup"><span data-stu-id="c8f61-1626">*NX_WEB_HTTP_SERVER_PUT_REQUEST NX_WEB_HTTP_SERVER_DELETE_REQUEST*</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1627">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1627">Return Values</span></span>

- <span data-ttu-id="c8f61-1628">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1628">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8f61-1629">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1629">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1630">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1630">Allowed From</span></span>

<span data-ttu-id="c8f61-1631">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1631">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1632">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1632">Example</span></span>

```C
NX_WEB_HTTP_SERVER my_server;

VOID invalid_username_password_callback(NX_CHAR *resource,
    ULONG client_address,
    UINT request_type);

/* After the HTTP server is created by calling nx_web_http_server_create,
    and before starting HTTP services when nx_web_http_server_start() is called,
    set the invalid username password callback: */

status = nx_web_http_server_invalid_userpassword_notify_set( (&my_server,
    invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
    will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_web_http_server_mime_maps_additional_set"></a><span data-ttu-id="c8f61-1633">nx_web_http_server_mime_maps_additional_set</span><span class="sxs-lookup"><span data-stu-id="c8f61-1633">nx_web_http_server_mime_maps_additional_set</span></span>

<span data-ttu-id="c8f61-1634">HTML için ek MIME haritaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1634">Set additional MIME maps for HTML</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1635">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1635">Prototype</span></span>

```C
UINT nx_web_http_server_mime_maps_additional_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_WEB_HTTP_SERVER_MIME_MAP *mime_maps,
    UINT mime_maps_num);
```

### <a name="description"></a><span data-ttu-id="c8f61-1636">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1636">Description</span></span>

<span data-ttu-id="c8f61-1637">Bu hizmet, HTTP uygulama geliştiricisinin NetX Web HTTP sunucusu tarafından sağlanan varsayılan MIME türlerinden ek MIME türleri eklemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1637">This service allows the HTTP application developer to add additional MIME types from the default MIME types supplied by the NetX Web HTTP Server.</span></span> <span data-ttu-id="c8f61-1638">Tanımlı türlerin listesi için bkz. *nx_web_http_server_get_type ()* .</span><span class="sxs-lookup"><span data-stu-id="c8f61-1638">See *nx_web_http_server_get_type()* for list of defined types.</span></span>

<span data-ttu-id="c8f61-1639">Bir istemci isteği alındığında, örneğin, bir GET isteği, http üst bilgisinden istenen dosya türünü, tercihe bağlı olarak ek MIME eşleme kümesini kullanarak ayrıştırır ve bulunursa eşleşme yoksa, HTTP sunucusunun varsayılan MIME eşlemesinde bir eşleşme arar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1639">When a client request is received, e.g. a GET request, HTTP server parses the requested file type from the HTTP header using preferentially the additional MIME map set and if no match if found, it looks for a match in the default MIME map of the HTTP server.</span></span> <span data-ttu-id="c8f61-1640">Eşleşme bulunmazsa, MIME türü varsayılan olarak "metin/düz" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1640">If no match is found, the MIME type defaults to "text/plain".</span></span>

<span data-ttu-id="c8f61-1641">İstek bildirimi işlevi HTTP sunucusuna kayıtlıysa, istek bildirimi geri araması dosya türünü ayrıştırmak için *nx_web_http_server_type_get_extended ()* çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1641">If the request notify function is registered with the HTTP server, the request notify callback can call *nx_web_http_server_type_get_extended()* to parse the file type.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1642">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1642">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1643">**server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1643">**server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8f61-1644">**mime_maps** MIME eşleme dizisine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1644">**mime_maps** Pointer to a MIME map array</span></span>
- <span data-ttu-id="c8f61-1645">**mime_map_num** Dizideki MIME haritaları sayısı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1645">**mime_map_num** Number of MIME maps in array</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1646">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1646">Return Values</span></span>

- <span data-ttu-id="c8f61-1647">**NX_SUCCESS** (0x00) başarılı http sunucusu MIME eşleme kümesi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1647">**NX_SUCCESS** (0x00) Successful HTTP Server MIME map set</span></span>
- <span data-ttu-id="c8f61-1648">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1648">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1649">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1649">Allowed From</span></span>

<span data-ttu-id="c8f61-1650">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1650">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1651">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1651">Example</span></span>

```C
/* my_server is an NX_WEB_HTTP_SERVER previously created. */
static NX_WEB_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc", "yourtype/abc"},
    {"xyz", "mytype/xyz"},
};

status = nx_web_http_server_mime_maps_additional_set(&my_server,
    &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP
    server MIME map set." */
```

## <a name="nx_web_http_server_response_packet_allocate"></a><span data-ttu-id="c8f61-1652">nx_web_http_server_response_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="c8f61-1652">nx_web_http_server_response_packet_allocate</span></span>

<span data-ttu-id="c8f61-1653">HTTP (S) paketi ayır</span><span class="sxs-lookup"><span data-stu-id="c8f61-1653">Allocate an HTTP(S) packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1654">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1654">Prototype</span></span>

```C
UINT nx_web_http_server_response_packet_allocate(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c8f61-1655">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1655">Description</span></span>

<span data-ttu-id="c8f61-1656">Bu hizmet, HTTP (S) sunucusu için bir paket ayırır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1656">This service attempts to allocates a packet for the HTTP(S) server.</span></span>

<span data-ttu-id="c8f61-1657">Sonraki bir NetX veya bu paketi giriş olarak kullanan bir HTTP sunucu API 'SI nx_packet_data_append veya \* \* nx_web_http_server_callback_packet_send gibi **başarısız olursa**, uygulamanın paketi serbest bırakmasından sorumlu olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1657">Note that if a subsequent NetX or HTTP Server API using this packet as input **fails**, such as nx_packet_data_append or \*\*nx_web_http_server_callback_packet_send, the application is responsible for releasing the packet.</span></span> **

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1658">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1658">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1659">**server_ptr** HTTP sunucu denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1659">**server_ptr** Pointer to HTTP Server control block.</span></span>
- <span data-ttu-id="c8f61-1660">**packet_ptr** Ayrılan pakete yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1660">**packet_ptr** Pointer to allocated packet.</span></span>
- <span data-ttu-id="c8f61-1661">**wait_option** Paket havuzunda kullanılabilir bir paket yoksa, zaman işaretleri cinsinden bekleme süresini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1661">**wait_option** Defines the wait time in ticks if there are no packets available in the packet pool.</span></span> <span data-ttu-id="c8f61-1662">Bekleme seçenekleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1662">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="c8f61-1663">**NX_NO_WAIT** (0x00000000) NX_NO_WAIT seçilmesi çağıran iş parçacığının istek karşılanmıyorsa hemen dönmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1663">**NX_NO_WAIT** (0x00000000) Selecting NX_NO_WAIT causes the calling thread to return immediately if the request cannot be fulfilled.</span></span>
  - <span data-ttu-id="c8f61-1664">**NX_WAIT_FOREVER** (0xffffffff) NX_WAIT_FOREVER seçilmesi çağıran Iş parçacığının http sunucusu isteğe yanıt verene kadar süresiz olarak askıda kalmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1664">**NX_WAIT_FOREVER** (0xFFFFFFFF) Selecting NX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the HTTP Server responds to the request.</span></span>
  - <span data-ttu-id="c8f61-1665">**zaman aşımı değeri** (0x00000001 aracılığıyla 0xfffffffe) sayısal değer seçme (0x1-0xfffffffe), http sunucusu yanıtı beklenirken askıya alınması için en fazla Zamanlayıcı onay işareti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1665">**timeout value** (0x00000001 through 0xFFFFFFFE) Selecting a numeric value (0x1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the HTTP Server response.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1666">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1666">Return Values</span></span>

- <span data-ttu-id="c8f61-1667">**NX_SUCCESS** (0x00) başarılı paket ayırma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1667">**NX_SUCCESS** (0x00) Successful packet allocate</span></span>
- <span data-ttu-id="c8f61-1668">**NX_NO_PACKET** (0x01) kullanılabilir paket yok</span><span class="sxs-lookup"><span data-stu-id="c8f61-1668">**NX_NO_PACKET** (0x01) No packet available</span></span>
- <span data-ttu-id="c8f61-1669">**NX_WAIT_ABORTED** (0x1A) askıya alma isteği *tx_thread_wait_abort* bir çağrı tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1669">**NX_WAIT_ABORTED** (0x1A) Requested suspension was aborted by a call to *tx_thread_wait_abort*.</span></span>
- <span data-ttu-id="c8f61-1670">**NX_INVALID_PARAMETERS** (0x4D) paket boyutu Protokolü desteklenemez.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1670">**NX_INVALID_PARAMETERS** (0x4D) Packet size cannot support protocol.</span></span>
- <span data-ttu-id="c8f61-1671">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1671">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1672">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1672">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1673">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1673">Allowed From</span></span>

<span data-ttu-id="c8f61-1674">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1674">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1675">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1675">Example</span></span>

```C
/* Allocate a packet for HTTP(S) Server and suspend for a maximum of 5 timer
    ticks if the pool is empty. */
status = nx_web_http_server_response_packet_allocate(&my_client, &packet_ptr, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
    variable packet_ptr. */
```

## <a name="nx_web_http_server_packet_content_find"></a><span data-ttu-id="c8f61-1676">nx_web_http_server_packet_content_find</span><span class="sxs-lookup"><span data-stu-id="c8f61-1676">nx_web_http_server_packet_content_find</span></span>

<span data-ttu-id="c8f61-1677">İçerik uzunluğunu Ayıkla ve veri başına işaretçiyi ayarla</span><span class="sxs-lookup"><span data-stu-id="c8f61-1677">Extract content length and set pointer to start of data</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1678">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1678">Prototype</span></span>

```C
UINT nx_web_http_server_packet_content_find(
    NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr,
    UINT *content_length);
```

### <a name="description"></a><span data-ttu-id="c8f61-1679">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1679">Description</span></span>

<span data-ttu-id="c8f61-1680">Bu hizmet, HTTP üstbilgisinden içerik uzunluğunu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1680">This service extracts the content length from the HTTP header.</span></span> <span data-ttu-id="c8f61-1681">Ayrıca, sağlanan paketi aşağıdaki gibi güncelleştirir: paket önüne işaretçisi (yazılacak paket arabelleğinin konumu), http içeriğine (veri) yalnızca http üst bilgisini geçirilmiş şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1681">It also updates the supplied packet as follows: the packet prepend pointer (start of location of packet buffer to write to) is set to the HTTP content (data) just passed the HTTP header.</span></span>

<span data-ttu-id="c8f61-1682">İçeriğin başlangıcı geçerli pakette bulunmazsa, işlev, sonraki paketin NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE bekle seçeneği kullanılarak alınmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1682">If the beginning of content is not found in the current packet, the function waits for the next packet to be received using the NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE wait option.</span></span>

<span data-ttu-id="c8f61-1683">Bu, *nx_web_http_server_get_entity_header ()* çağrılmadan önce çağrılmamalıdır; çünkü bu, varlık üstbilgisinin ötesinde paket önüne işaretçisini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1683">Note this should not be called before calling *nx_web_http_server_get_entity_header()* because it modifies the packet prepend pointer past the entity header.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1684">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1684">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1685">**server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1685">**server_ptr** Pointer to HTTP server instance</span></span>
- <span data-ttu-id="c8f61-1686">**packet_ptr** Güncelleştirilmiş önüne işaretçisine sahip paketi döndürmek için paket işaretçisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1686">**packet_ptr** Pointer to packet pointer for returning the packet with updated prepend pointer</span></span>
- <span data-ttu-id="c8f61-1687">**CONTENT_LENGTH** Ayıklanan content_length işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1687">**content_length** Pointer to extracted content_length</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1688">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1688">Return Values</span></span>

- <span data-ttu-id="c8f61-1689">**NX_SUCCESS** (0x00) http içerik uzunluğu bulundu ve paket başarıyla güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1689">**NX_SUCCESS** (0x00) HTTP content length found and packet successfully updated</span></span>
- <span data-ttu-id="c8f61-1690">**NX_WEB_HTTP_TIMEOUT** (0x30001) sonraki pakette bekleme süresi geçildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1690">**NX_WEB_HTTP_TIMEOUT** (0x30001) Time expired waiting on next Packet</span></span>
- <span data-ttu-id="c8f61-1691">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1691">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1692">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1692">Allowed From</span></span>

<span data-ttu-id="c8f61-1693">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1693">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1694">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1694">Example</span></span>

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
    The server has received a Client request packet, recv_packet_ptr,
    and the packet content find service is called from the request notify callback
    function registered with the HTTP server. */

UINT content_length;

status = nx_web_http_server_packet_content_find(server_ptr, recv_packet_ptr,
    &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
    and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_web_http_server_packet_get"></a><span data-ttu-id="c8f61-1695">nx_web_http_server_packet_get</span><span class="sxs-lookup"><span data-stu-id="c8f61-1695">nx_web_http_server_packet_get</span></span>

<span data-ttu-id="c8f61-1696">Sonraki HTTP paketini al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1696">Receive the next HTTP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1697">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1697">Prototype</span></span>

```C
UINT nx_web_http_server_packet_get(NX_WEB_HTTP_SERVER *server_ptr,
    NX_PACKET **packet_ptr);
```

### <a name="description"></a><span data-ttu-id="c8f61-1698">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1698">Description</span></span>

<span data-ttu-id="c8f61-1699">Bu hizmet, HTTP sunucusu yuvasında alınan bir sonraki paketi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1699">This service returns the next packet received on the HTTP server socket.</span></span> <span data-ttu-id="c8f61-1700">Bir paket almak için bekle seçeneği NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1700">The wait option to receive a packet is NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE.</span></span>

<span data-ttu-id="c8f61-1701">Uygulamanın paketin serbest bırakılmasından sorumlu olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1701">Note that if successful the application is responsible for releasing the packet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1702">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1702">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1703">**server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1703">**server_ptr** Pointer to HTTP server instance</span></span>
- <span data-ttu-id="c8f61-1704">**packet_ptr** Alınan paket işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1704">**packet_ptr** Pointer to received packet</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1705">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1705">Return Values</span></span>

- <span data-ttu-id="c8f61-1706">**NX_SUCCESS** (0x00) sonraki http paketi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1706">**NX_SUCCESS** (0x00) Successfully received next HTTP packet</span></span>
- <span data-ttu-id="c8f61-1707">**NX_WEB_HTTP_TIMEOUT** (0x30001) sonraki pakette bekleme süresi geçildi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1707">**NX_WEB_HTTP_TIMEOUT** (0x30001) Time expired waiting on next Packet</span></span>
- <span data-ttu-id="c8f61-1708">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1708">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1709">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1709">Allowed From</span></span>

<span data-ttu-id="c8f61-1710">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1710">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1711">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1711">Example</span></span>

```C
/* The HTTP server pointed to by server_ptr is previously created and started. */
UINT content_length;
NX_PACKET *recv_packet_ptr;

status = nx_web_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_web_http_server_param_get"></a><span data-ttu-id="c8f61-1712">nx_web_http_server_param_get</span><span class="sxs-lookup"><span data-stu-id="c8f61-1712">nx_web_http_server_param_get</span></span>

<span data-ttu-id="c8f61-1713">İstekten parametre al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1713">Get parameter from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1714">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1714">Prototype</span></span>

```C
UINT nx_web_http_server_param_get(NX_PACKET *packet_ptr,
    UINT param_number, CHAR *param_ptr,
    UINT *param_size, UINT max_param_size);
```

### <a name="description"></a><span data-ttu-id="c8f61-1715">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1715">Description</span></span>

<span data-ttu-id="c8f61-1716">Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL parametresini almaya çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1716">This service attempts to retrieve the specified HTTP URL parameter in the supplied request packet.</span></span> <span data-ttu-id="c8f61-1717">İstenen HTTP parametresi yoksa, bu yordam NX_WEB_HTTP_NOT_FOUND durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1717">If the requested HTTP parameter is not present, this routine returns a status of NX_WEB_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="c8f61-1718">Bu yordam, HTTP sunucusu oluşturma (*nx_web_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1718">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1719">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1719">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1720">**packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1720">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="c8f61-1721">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1721">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="c8f61-1722">**param_number** Parametre listesinde soldan sağa sıfırdan başlayan parametrenin mantıksal numarası.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1722">**param_number** Logical number of the parameter starting at zero, from left to right in the parameter list.</span></span>
- <span data-ttu-id="c8f61-1723">**param_ptr** Parametreyi kopyalamak için hedef alan.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1723">**param_ptr** Destination area to copy the parameter.</span></span>
- <span data-ttu-id="c8f61-1724">**param_size** Toplam parametre veri uzunluğunu (bayt olarak) döndürür.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1724">**param_size** Return the total parameter data length (in bytes).</span></span>
- <span data-ttu-id="c8f61-1725">**max_param_size** Parametre hedefi alanının maksimum boyutu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1725">**max_param_size** Maximum size of the parameter destination area.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1726">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1726">Return Values</span></span>

- <span data-ttu-id="c8f61-1727">**NX_SUCCESS** (0x00) başarılı http sunucusu parametre al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1727">**NX_SUCCESS** (0x00) Successful HTTP Server parameter get</span></span>
- <span data-ttu-id="c8f61-1728">**NX_WEB_HTTP_NOT_FOUND** (0x30006) belirtilen parametre bulunamadı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1728">**NX_WEB_HTTP_NOT_FOUND** (0x30006) Specified parameter not found</span></span>
- <span data-ttu-id="c8f61-1729">**NX_WEB_HTTP_IMPROPERLY_TERMINATED_PARAM** (0x30015) istek parametresi düzgün sonlandırılmadı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1729">**NX_WEB_HTTP_IMPROPERLY_TERMINATED_PARAM** (0x30015) Request parameter not properly terminated</span></span>
- <span data-ttu-id="c8f61-1730">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1730">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1731">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1731">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1732">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1732">Allowed From</span></span>

<span data-ttu-id="c8f61-1733">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1733">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1734">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1734">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, get the first parameter of the HTTP Client request. */

status = nx_web_http_server_param_get(request_packet_ptr, 0, param_destination,
    &param_size, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
    in "param_destination" and the size of that string can be found
    in the variable "param_size." */
```

## <a name="nx_web_http_server_query_get"></a><span data-ttu-id="c8f61-1735">nx_web_http_server_query_get</span><span class="sxs-lookup"><span data-stu-id="c8f61-1735">nx_web_http_server_query_get</span></span>

<span data-ttu-id="c8f61-1736">İstekten sorgu al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1736">Get query from the request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1737">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1737">Prototype</span></span>

```C
UINT nx_web_http_server_query_get(NX_PACKET *packet_ptr,
    UINT query_number,
    CHAR *query_ptr,
    CHAR *query_size,
    UINT max_query_size);
```

### <a name="description"></a><span data-ttu-id="c8f61-1738">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1738">Description</span></span>

<span data-ttu-id="c8f61-1739">Bu hizmet, sağlanan istek paketinde belirtilen HTTP URL sorgusunu almaya çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1739">This service attempts to retrieve the specified HTTP URL query in the supplied request packet.</span></span> <span data-ttu-id="c8f61-1740">İstenen HTTP sorgusu yoksa, bu yordam NX_WEB_HTTP_NOT_FOUND durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1740">If the requested HTTP query is not present, this routine returns a status of NX_WEB_HTTP_NOT_FOUND.</span></span> <span data-ttu-id="c8f61-1741">Bu yordam, HTTP sunucusu oluşturma (*nx_web_http_server_create ()*) sırasında uygulamanın istek bildirimi geri çağrısından çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1741">This routine should be called from the application’s request notify callback specified during HTTP Server creation (*nx_web_http_server_create()*).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1742">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1742">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1743">**packet_ptr** HTTP Istemci isteği paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1743">**packet_ptr** Pointer to HTTP Client request packet.</span></span> <span data-ttu-id="c8f61-1744">Uygulamanın bu paketi serbest bırakmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1744">Note that the application should not release this packet.</span></span>
- <span data-ttu-id="c8f61-1745">**query_number** Sıfırdan başlayan parametrenin mantıksal numarası, sorgu listesinde soldan sağa.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1745">**query_number** Logical number of the parameter starting at zero, from left to right in the query list.</span></span>
- <span data-ttu-id="c8f61-1746">**query_ptr** Sorguyu kopyalamak için hedef alan.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1746">**query_ptr** Destination area to copy the query.</span></span>
- <span data-ttu-id="c8f61-1747">**query_size** Sorgu veri boyutunu (bayt cinsinden) döndürün.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1747">**query_size** Return query data size (in bytes).</span></span>
- <span data-ttu-id="c8f61-1748">**max_query_size** Sorgu hedefinin en büyük boyutu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1748">**max_query_size** Maximum size of the query destination</span></span>

<span data-ttu-id="c8f61-1749">alandır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1749">area.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1750">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1750">Return Values</span></span>

- <span data-ttu-id="c8f61-1751">**NX_SUCCESS** (0x00) başarılı http sunucusu sorgusu al</span><span class="sxs-lookup"><span data-stu-id="c8f61-1751">**NX_SUCCESS** (0x00) Successful HTTP Server query get</span></span>
- <span data-ttu-id="c8f61-1752">**NX_WEB_HTTP_FAILED** (0x30002) sorgu boyutu çok küçük.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1752">**NX_WEB_HTTP_FAILED** (0x30002) Query size too small.</span></span>
- <span data-ttu-id="c8f61-1753">**NX_WEB_HTTP_NOT_FOUND** (0x30006) belirtilen sorgu bulunamadı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1753">**NX_WEB_HTTP_NOT_FOUND** (0x30006) Specified query not found</span></span>
- <span data-ttu-id="c8f61-1754">**NX_WEB_HTTP_NO_QUERY_PARSED** (0x30013) istemci Isteğinde sorgu yok</span><span class="sxs-lookup"><span data-stu-id="c8f61-1754">**NX_WEB_HTTP_NO_QUERY_PARSED** (0x30013) No query in Client request</span></span>
- <span data-ttu-id="c8f61-1755">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1755">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1756">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1756">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1757">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1757">Allowed From</span></span>

<span data-ttu-id="c8f61-1758">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1758">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1759">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1759">Example</span></span>

```C
/* Assuming we are in the application’s request notify callback
    routine, get the first query of the HTTP Client request. */

status = nx_web_http_server_query_get(request_packet_ptr, 0,
    query_destination, &query_size, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
    in "query_destination" and the length of that string can be found in the
    variable "query_size". */
```

## <a name="nx_web_http_server_response_chunked_set"></a><span data-ttu-id="c8f61-1760">nx_web_http_server_response_chunked_set</span><span class="sxs-lookup"><span data-stu-id="c8f61-1760">nx_web_http_server_response_chunked_set</span></span>

<span data-ttu-id="c8f61-1761">HTTP (S) yanıtı için öbekli aktarım ayarla</span><span class="sxs-lookup"><span data-stu-id="c8f61-1761">Set chunked transfer for HTTP(S) response</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1762">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1762">Prototype</span></span>

```C
UINT nx_web_http_server_response_chunked_set(
    NX_WEB_HTTP_SERVER *server_ptr,
    UINT chunk_size, NX_PACKET *packet_ptr);
```

### <a name="description"></a><span data-ttu-id="c8f61-1763">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1763">Description</span></span>

<span data-ttu-id="c8f61-1764">Bu hizmet, istemciye *nx_web_http_server_response_packet_allocate*() ile oluşturulmuş özel bir http (S) yanıt veri paketi göndermek için öbekli aktarım kodlamasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1764">This service uses chunked transfer coding to send a custom HTTP(S) response data packet created with *nx_web_http_server_response_packet_allocate*() to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-1765">Uygulama bir yanıt veri paketi göndermek için öbekli aktarım kodlaması kullanıyorsa, *nx_web_http_server_response_packet_allocate*() çağrıldıktan sonra ve *nx_web_http_server_callback_packet_send*() çağrısından önce bu hizmeti çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1765">If the application uses chunked transfer coding to send a response data packet, it must call this service after calling *nx_web_http_server_response_packet_allocate*(), and before calling *nx_web_http_server_callback_packet_send*().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1766">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1766">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1767">**client_ptr** HTTP Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1767">**client_ptr** Pointer to HTTP Client control block.</span></span>
- <span data-ttu-id="c8f61-1768">**chunk_size** Öbek verilerinin sekizli cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1768">**chunk_size** Size of the chunk-data in octets.</span></span>
- <span data-ttu-id="c8f61-1769">**packet_ptr** HTTP (S) istek veri paketi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1769">**packet_ptr** HTTP(S) request data packet pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1770">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1770">Return Values</span></span>

- <span data-ttu-id="c8f61-1771">**NX_SUCCESS** (0x00) başarılı kümesi yığını.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1771">**NX_SUCCESS** (0x00) Successful set chunked.</span></span>
- <span data-ttu-id="c8f61-1772">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1772">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1773">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1773">Allowed From</span></span>

<span data-ttu-id="c8f61-1774">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1774">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1775">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1775">Example</span></span>

```C
/* Generate HTTP header. */
nx_web_http_server_callback_generate_response_header(server_ptr,
    &response_pkt, NX_WEB_HTTP_STATUS_OK, 0, "text/html",
    "Transfer-Encoding: chunked\r\n");

/* Create a new data packet response on the HTTP(S) Server instance. */
nx_web_http_server_response_packet_allocate(&my_server, &my_packet, NX_WAIT_FOREVER);

/* Set the chunked transfer. */
status = nx_web_http_server_response_chunked_set(&my_server, 128, my_packet)

/* At this point, user can fill the data into my_packet. *./
nx_packet_data_append(my_packet, data_ptr, data_size,
    packet_pool, NX_WAIT_FOREVER);

/* Send data packet response to client. */
nx_web_http_server_callback_packet_send(&my_server, my_packet);
```

## <a name="nx_web_http_server_secure_configure"></a><span data-ttu-id="c8f61-1776">nx_web_http_server_secure_configure</span><span class="sxs-lookup"><span data-stu-id="c8f61-1776">nx_web_http_server_secure_configure</span></span>

<span data-ttu-id="c8f61-1777">Güvenli HTTPS için TLS kullanmak üzere bir HTTP sunucusu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1777">Configure an HTTP Server to use TLS for secure HTTPS</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1778">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1778">Prototype</span></span>

```C
UINT nx_web_http_server_secure_configure(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    const NX_SECURE_TLS_CRYPTO *crypto_table,
    VOID *metadata_buffer, ULONG metadata_size,
    UCHAR* packet_buffer, UINT packet_buffer_size,
    NX_SECURE_X509_CERT *identity_certificate,
    NX_SECURE_X509_CERT *trusted_certificates[],
    UINT trusted_certs_num,
    NX_SECURE_X509_CERT *remote_certificates[],
    UINT remote_certs_num,
    UCHAR *remote_certificate_buffer,
    UINT remote_cert_buffer_size);
```

### <a name="description"></a><span data-ttu-id="c8f61-1779">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1779">Description</span></span>

<span data-ttu-id="c8f61-1780">Bu hizmet, güvenli HTTPS iletişimleri için TLS kullanmak üzere önceden oluşturulmuş bir NetX Web HTTP sunucusu örneğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1780">This service configures a previously created NetX Web HTTP server instance to use TLS for secure HTTPS communications.</span></span> <span data-ttu-id="c8f61-1781">Parametreler, her gelen HTTPS Istemcisinin tutarlı davranışlar ile karşılaşabilmesi için aynı durum ile tüm olası TLS oturumlarını yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1781">The parameters are used to configure all the possible TLS sessions with identical state so that each incoming HTTPS Client experiences consistent behavior.</span></span> <span data-ttu-id="c8f61-1782">TLS oturumlarının sayısı NX_WEB_HTTP_SESSION_MAX makro kullanılarak denetlenir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1782">The number of TLS sessions is controlled using the macro NX_WEB_HTTP_SESSION_MAX.</span></span>

<span data-ttu-id="c8f61-1783">Şifreleme rutin tablosu (ciphersuite tablosu) yalnızca işlev işaretçileri içerdiği için tüm TLS oturumları arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1783">The cryptographic routine table (ciphersuite table) is shared between all TLS sessions as it just contains function pointers.</span></span>

<span data-ttu-id="c8f61-1784">Meta veri ve paket yeniden birleştirme arabelleklerinin hepsi tüm TLS oturumları arasında eşit olarak bölünür.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1784">The metadata and packet reassembly buffers are each divided equally between all TLS sessions.</span></span> <span data-ttu-id="c8f61-1785">Arabellek boyutu, oturum sayısına eşit olarak bölünemez ve geri kalan kullanım dışı kalır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1785">If the buffer size is not evenly divisible by the number of sessions the remainder will be unused.</span></span>

<span data-ttu-id="c8f61-1786">Geçilen kimlik sertifikası tüm oturumlar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1786">The passed-in identity certificate is used by all sessions.</span></span> <span data-ttu-id="c8f61-1787">TLS işlemi sırasında sunucu kimliği sertifikası, her oturum için kopyaların her biri için gerekli olmadığı şekilde salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1787">During TLS operation the server identity certificate is only read from so copies are not needed for each session.</span></span>

<span data-ttu-id="c8f61-1788">Güvenilen Sertifikalar, HTTPS sunucusundaki her bir TLS oturumuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1788">The trusted certificates are added to each TLS session in the HTTPS Server.</span></span> <span data-ttu-id="c8f61-1789">Bunlar, uzak sertifika alanı sağlandığında otomatik olarak etkinleştirilen Istemci sertifikası kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1789">These are used for Client certificate authentication which is automatically enabled when remote certificate space is provided.</span></span>

<span data-ttu-id="c8f61-1790">Uzak sertifika dizisi ve arabelleği, tüm TLS oturumları arasında varsayılan olarak paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1790">The remote certificate array and buffer is shared by default between all TLS sessions.</span></span> <span data-ttu-id="c8f61-1791">Uzak sertifikalar, uzak sertifika sayısı sıfır olmadığında otomatik olarak etkinleştirilen Istemci sertifikası kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1791">The remote certificates are used for Client certificate authentication which is automatically enabled when the remote certificate count is nonzero.</span></span> <span data-ttu-id="c8f61-1792">Paylaşılan arabellek nedeniyle, bazı oturumlar sertifika doğrulaması sırasında engelleyebilen bir durum olabilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1792">Due to the buffer being shared some sessions may block during certificate validation.</span></span>

<span data-ttu-id="c8f61-1793">İstemci sertifikası kimlik doğrulamasını devre dışı bırakmak için, remote_certificates parametresi için NX_NULL geçirin ve remote_certs_num parametresi için 0 değeri.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1793">To disable client certificate authentication, pass NX_NULL for the remote_certificates parameter and a value of 0 for the remote_certs_num parameter.</span></span>

<span data-ttu-id="c8f61-1794">Dönüş değerleri, TLS oturumlarının yapılandırmasındaki sorunlardan kaynaklanan herhangi bir TLS hata kodu içerecektir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1794">Return values will include any TLS error codes resulting from issues in the configuration of the TLS sessions.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1795">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1795">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1796">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1796">**http_server_ptr** Pointer to HTTP Server instance.</span></span>
- <span data-ttu-id="c8f61-1797">**crypto_table** TLS ciphersuite tablosuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1797">**crypto_table** Pointer to TLS ciphersuite table.</span></span>
- <span data-ttu-id="c8f61-1798">**metadata_buffer** Şifreleme meta veri arabelleği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1798">**metadata_buffer** Pointer to cryptographic metadata buffer.</span></span>
- <span data-ttu-id="c8f61-1799">**metadata_size** Şifreleme meta veri arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1799">**metadata_size** Size of cryptographic metadata buffer.</span></span>
- <span data-ttu-id="c8f61-1800">**packet_buffer** TLS paketi yeniden birleştirme arabelleği.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1800">**packet_buffer** TLS packet reassembly buffer.</span></span>
- <span data-ttu-id="c8f61-1801">**packet_buffer** TLS paket arabelleğinin boyutu – şuna eşit olmalıdır: istenen TLS arabelleği boyutu \* NX_WEB_HTTP_SESSION_MAX <.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1801">**packet_buffer** Size of TLS packet buffer – should be equal to (<desired TLS buffer size\* NX_WEB_HTTP_SESSION_MAX).</span></span>
- <span data-ttu-id="c8f61-1802">**identity_certificate** TLS sunucu kimlik sertifikası – tüm HTTPS sunucu oturumları için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1802">**identity_certificate** TLS server identity certificate – will be used for all HTTPS server sessions.</span></span>
- <span data-ttu-id="c8f61-1803">**trusted_certificates** İstemci sertifikası kimlik doğrulaması etkinse, *remote_certs_num* parametresi için sıfır olmayan bir değer geçirerek, gelen istemci sertifikalarını doğrulamak için kullanılan NX_SECURE_X509_CERT nesneleri dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1803">**trusted_certificates** Pointer to array of NX_SECURE_X509_CERT objects, used to validate incoming client certificates if client certificate authentication is enabled by passing a non-zero value for the *remote_certs_num* parameter.</span></span>
- <span data-ttu-id="c8f61-1804">**trusted_certs_num** *Trusted_certificates* dizisindeki güvenilir sertifika sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1804">**trusted_certs_num** Number of trusted certificates in the *trusted_certificates* array.</span></span>
- <span data-ttu-id="c8f61-1805">**remote_certificates** Gelen istemci sertifikaları için kullanılan NX_SECURE_X509_CERT nesneleri dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1805">**remote_certificates** Pointer to array of NX_SECURE_X509_CERT objects, used for incoming client certificates.</span></span>
- <span data-ttu-id="c8f61-1806">**remote_certs_num** Uzak sertifika sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1806">**remote_certs_num** Number of remote certificates.</span></span> <span data-ttu-id="c8f61-1807">İstemcilerden beklenen sertifika sayısının üst sınırı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1807">Should be the maximum number of expected certificates from clients.</span></span> <span data-ttu-id="c8f61-1808">Bu sıfır dışında olduğunda istemci sertifikası kimlik doğrulaması otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1808">Client certificate authentication is enabled automatically when this is non-zero.</span></span>
- <span data-ttu-id="c8f61-1809">**remote_certificate_buffer** İstemci sertifikası kimlik doğrulaması etkinse istemcilerden gelen uzak sertifikaları içeren arabellek.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1809">**remote_certificate_buffer** Buffer to contain incoming remote certificates from clients if client certificate authentication is enabled.</span></span> <span data-ttu-id="c8f61-1810">uzak sertifika arabelleğinin remote_cert_buffer_size boyutu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1810">remote_cert_buffer_size Size of remote certificates buffer.</span></span> <span data-ttu-id="c8f61-1811">Şuna eşit olmalıdır (<en fazla beklenen sertifika boyutu \* remote_certs_num).</span><span class="sxs-lookup"><span data-stu-id="c8f61-1811">Should be equal to (<maximum expected certificate size \* remote_certs_num).</span></span>


### <a name="return-values"></a><span data-ttu-id="c8f61-1812">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1812">Return Values</span></span>

- <span data-ttu-id="c8f61-1813">TLS oturumunun başarıyla başlatılmasından **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="c8f61-1813">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c8f61-1814">**NX_NOT_CONNECTED** (0x38) temel alınan TCP yuvası artık bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1814">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="c8f61-1815">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) ALıNAN bir TLS ileti türü yanlış.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1815">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) A received TLS message type is incorrect.</span></span>
- <span data-ttu-id="c8f61-1816">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) uzak ana bilgisayar tarafından sağlanmış bir şifre desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1816">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A cipher provided by the remote host is not supported.</span></span>
- <span data-ttu-id="c8f61-1817">TLS el sıkışması sırasında **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) ileti işleme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1817">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Message processing during the TLS handshake has failed.</span></span>
- <span data-ttu-id="c8f61-1818">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) gelen bir ILETI karma Mac denetiminde başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1818">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) An incoming message failed a  hash MAC check.</span></span>
- <span data-ttu-id="c8f61-1819">**NX_SECURE_TLS_TCP_SEND_FAILE** (0x109) temel alınan TCP yuvası gönderme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1819">**NX_SECURE_TLS_TCP_SEND_FAILE** (0x109) An underlying TCP socket send failed.</span></span>
- <span data-ttu-id="c8f61-1820">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10a) gelen iletide geçersiz uzunluk alanı vardı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1820">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) An incoming message had an invalid length field.</span></span>
- <span data-ttu-id="c8f61-1821">**NX_SECURE_TLS_BAD_CIPHERSPE** (0x10b) gelen bir Changecyaspec iletisi hatalı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1821">**NX_SECURE_TLS_BAD_CIPHERSPE** (0x10B) An incoming ChangeCipherSpec message was incorrect.</span></span>
- <span data-ttu-id="c8f61-1822">**NX_SECURE_TLS_INVALID_SERVER_CER** (0x10c) uzak TLS sunucusunu tanımlamak Için gelen bir TLS sertifikası kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1822">**NX_SECURE_TLS_INVALID_SERVER_CER** (0x10C) An incoming TLS certificate is unusable for identifying the remote TLS server.</span></span>
- <span data-ttu-id="c8f61-1823">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10d) uzak ana bilgisayar tarafından sunulan ortak anahtar şifresi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1823">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) The public-key cipher provided by the remote host is unsupported.</span></span>
- <span data-ttu-id="c8f61-1824">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10e) uzak ana bilgisayar, NETX güvenli TLS yığını tarafından desteklenen ciphersuites belirtti.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1824">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) The remote host has indicated no ciphersuites that are supported by the NetX Secure TLS stack.</span></span>
- <span data-ttu-id="c8f61-1825">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) ALıNAN bir TLS iletisinde üst bilgisinde BILINMEYEN bir TLS sürümü vardı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1825">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received TLS message had an unknown TLS version in its header.</span></span>
- <span data-ttu-id="c8f61-1826">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) ALıNAN bir TLS iletisinde, üstbilgisinde bilinen ancak desteklenmeyen bir TLS sürümü vardı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1826">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) A received TLS message had a known but unsupported TLS version in its header.</span></span>
- <span data-ttu-id="c8f61-1827">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) BIR iç TLS paket ayırması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1827">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) An internal TLS packet allocation failed.</span></span>
- <span data-ttu-id="c8f61-1828">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) uzak ana bilgisayar geçersiz bir sertifika sağladı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1828">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) The remote host provided an invalid certificate.</span></span>
- <span data-ttu-id="c8f61-1829">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) uzak ana bilgisayar bir hatayı BELIRTEN ve TLS oturumunu sonlandıran bir uyarı gönderdi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1829">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) The remote host sent an alert indicating an error and ending the TLS session.</span></span>
- <span data-ttu-id="c8f61-1830">**NX_PTR_ERROR** (0x07) geçersiz bir Işaretçi kullanmaya çalıştı.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1830">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1831">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1831">Allowed From</span></span>

<span data-ttu-id="c8f61-1832">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1832">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1833">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1833">Example</span></span>

```C
/* Create the HTTPS Server. */

status = nx_web_http_server_create(&my_server, "My HTTP Server",
    &ip_0, &ram_disk, &server_stack, sizeof(server_stack),
    &pool_0, authentication_check, server_request_callback);

/* Initialize device certificate (used for all sessions in HTTPS server). */
nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
    device_cert_der_len, NX_NULL, 0,
    device_cert_key_der, device_cert_key_der_len,
    NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

/* Setup TLS session for the HTTPS server.
    Note that since the remote_certs_num parameter is 0,
    no trusted certificates are needed, and Client certificate authentication is disabled. */
status = nx_web_http_server_secure_configure(&my_server, &nx_crypto_tls_ciphers,
    crypto_metadata,
    sizeof(crypto_metadata),
    tls_packet_buffer, sizeof(tls_packet_buffer),
    &certificate, NX_NULL, 0, NX_NULL, 0, NX_NULL, 0);

/* Start an HTTPS Server with TLS. */
status = nx_web_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_web_http_server_start"></a><span data-ttu-id="c8f61-1834">nx_web_http_server_start</span><span class="sxs-lookup"><span data-stu-id="c8f61-1834">nx_web_http_server_start</span></span>

<span data-ttu-id="c8f61-1835">HTTP sunucusunu başlatma</span><span class="sxs-lookup"><span data-stu-id="c8f61-1835">Start the HTTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1836">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1836">Prototype</span></span>

```C
UINT nx_web_http_server_start(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="c8f61-1837">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1837">Description</span></span>

<span data-ttu-id="c8f61-1838">Bu hizmet önceden oluşturulmuş bir HTTP veya HTTPS sunucu örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1838">This service starts a previously created HTTP or HTTPS Server instance.</span></span>

<span data-ttu-id="c8f61-1839">HTTPS sunucuları aynı API 'YI HTTP ile paylaşır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1839">HTTPS servers share the same API as HTTP.</span></span> <span data-ttu-id="c8f61-1840">HTTP sunucusunda TLS kullanarak HTTPS 'yi etkinleştirmek için *nx_web_http_server_secure_configure ()* hizmetine bakın.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1840">To enable HTTPS using TLS on an HTTP server, see the service *nx_web_http_server_secure_configure().*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1841">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1841">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1842">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1842">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1843">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1843">Return Values</span></span>

- <span data-ttu-id="c8f61-1844">**NX_SUCCESS** (0x00) başarılı http sunucusu başlatması</span><span class="sxs-lookup"><span data-stu-id="c8f61-1844">**NX_SUCCESS** (0x00) Successful HTTP Server Start</span></span>
- <span data-ttu-id="c8f61-1845">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1845">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1846">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1846">Allowed From</span></span>

<span data-ttu-id="c8f61-1847">Başlatma, Iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1847">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1848">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1848">Example</span></span>

```C
/* Start the HTTP Server instance "my_server." */
status = nx_web_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_web_http_server_stop"></a><span data-ttu-id="c8f61-1849">nx_web_http_server_stop</span><span class="sxs-lookup"><span data-stu-id="c8f61-1849">nx_web_http_server_stop</span></span>

<span data-ttu-id="c8f61-1850">HTTP sunucusunu durdur</span><span class="sxs-lookup"><span data-stu-id="c8f61-1850">Stop the HTTP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1851">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1851">Prototype</span></span>

```C
UINT nx_web_http_server_stop(NX_WEB_HTTP_SERVER *http_server_ptr);
```

### <a name="description"></a><span data-ttu-id="c8f61-1852">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1852">Description</span></span>

<span data-ttu-id="c8f61-1853">Bu hizmet, önceden oluşturma HTTP sunucu örneğini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1853">This service stops the previously create HTTP Server instance.</span></span> <span data-ttu-id="c8f61-1854">Bu yordam, bir HTTP sunucu örneği silinmeden önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1854">This routine should be called prior to deleting an HTTP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1855">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1855">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1856">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1856">**http_server_ptr** Pointer to HTTP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1857">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1857">Return Values</span></span>

- <span data-ttu-id="c8f61-1858">**NX_SUCCESS** (0x00) başarılı http sunucusu durdur</span><span class="sxs-lookup"><span data-stu-id="c8f61-1858">**NX_SUCCESS** (0x00) Successful HTTP Server Stop</span></span>
- <span data-ttu-id="c8f61-1859">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1859">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1860">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1860">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1861">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1861">Allowed From</span></span>

<span data-ttu-id="c8f61-1862">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="c8f61-1862">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1863">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1863">Example</span></span>

```C
/* Stop the HTTP Server instance "my_server." */
status = nx_web_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_web_http_server_type_get"></a><span data-ttu-id="c8f61-1864">nx_web_http_server_type_get</span><span class="sxs-lookup"><span data-stu-id="c8f61-1864">nx_web_http_server_type_get</span></span>

<span data-ttu-id="c8f61-1865">Istemci HTTP isteğinden dosya türünü Ayıkla</span><span class="sxs-lookup"><span data-stu-id="c8f61-1865">Extract file type from Client HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1866">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1866">Prototype</span></span>

```C
UINT nx_web_http_server_type_get(NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *name, CHAR *http_type_string,
    UINT *string_size);
```

### <a name="description"></a><span data-ttu-id="c8f61-1867">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1867">Description</span></span>

> [!NOTE]
> <span data-ttu-id="c8f61-1868">Bu hizmet kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1868">This service is deprecated.</span></span> <span data-ttu-id="c8f61-1869">Kullanıcıların *nx_web_http_server_type_get_extended ()* hizmetini kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1869">Users are encouraged to use the service *nx_web_http_server_type_get_extended()*.</span></span>

<span data-ttu-id="c8f61-1870">Bu hizmet, arabellek *HTTP_TYPE_STRING* http istek türünü ve (genellikle URL) giriş arabelleği *adından* *string_size* uzunluğunu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1870">This service extracts the HTTP request type in the buffer *http_type_string* and its length in *string_size* from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="c8f61-1871">MIME eşlemesi bulunmazsa, varsayılan olarak "metin/düz" tür olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1871">If no MIME map is found, it defaults to the "text/plain" type.</span></span> <span data-ttu-id="c8f61-1872">Aksi takdirde, bir eşleşme için ayıklanan tür, HTTP sunucusu varsayılan MIME eşlemeleriyle karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1872">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="c8f61-1873">NetX Web HTTP sunucusundaki varsayılan MIME haritaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1873">The default MIME maps in NetX Web HTTP Server are:</span></span>

- <span data-ttu-id="c8f61-1874">HTML metni/HTML</span><span class="sxs-lookup"><span data-stu-id="c8f61-1874">html text/html</span></span>
- <span data-ttu-id="c8f61-1875">htm metin/html</span><span class="sxs-lookup"><span data-stu-id="c8f61-1875">htm text/html</span></span>
- <span data-ttu-id="c8f61-1876">txt metin/düz</span><span class="sxs-lookup"><span data-stu-id="c8f61-1876">txt text/plain</span></span>
- <span data-ttu-id="c8f61-1877">GIF resmi/GIF</span><span class="sxs-lookup"><span data-stu-id="c8f61-1877">gif image/gif</span></span>
- <span data-ttu-id="c8f61-1878">jpg resmi/JPEG</span><span class="sxs-lookup"><span data-stu-id="c8f61-1878">jpg image/jpeg</span></span>
- <span data-ttu-id="c8f61-1879">ICO resmi/x-simgesi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1879">ico image/x-icon</span></span>

<span data-ttu-id="c8f61-1880">Sağlanırsa, Kullanıcı tanımlı ek MIME haritaları kümesi de arar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1880">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="c8f61-1881">Kullanıcı tanımlı haritalar hakkında daha fazla bilgi için bkz. *nx_web_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="c8f61-1881">See *nx_web_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1882">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1882">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1883">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1883">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8f61-1884">**ad** Aranacak arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1884">**name** Pointer to buffer to search</span></span>
- <span data-ttu-id="c8f61-1885">**http_type_string** Ayıklanan HTML türü dizesi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1885">**http_type_string** Pointer to extracted HTML type string</span></span>
- <span data-ttu-id="c8f61-1886">**string_size** Ayıklanan HTML türü dize uzunluğunu döndürme işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1886">**string_size** Pointer to return extracted HTML type string length.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1887">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1887">Return Values</span></span>

- <span data-ttu-id="c8f61-1888">**NX_SUCCESS** (0x00) tür başarıyla ayıklanamadı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1888">**NX_SUCCESS** (0x00) Successful extraction of type</span></span>
- <span data-ttu-id="c8f61-1889">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1889">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1890">**NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) varsayılan "metin/düz" döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1890">**NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) Default "text/plain" returned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1891">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1891">Allowed From</span></span>

<span data-ttu-id="c8f61-1892">Uygulama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1892">Application</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1893">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1893">Example</span></span>

```C
/* my_server is a previously created HTTP server, which starts accepting client
    requests when *nx_web_http_server_start* is called */

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
string_length = nx_web_http_server_type_get(&my_server_ptr,
    my_server.nx_web_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
    For a more detailed example, see the description for
    *nx_web_http_server_callback_generate_response_header().*
```

## <a name="nx_web_http_server_type_get_extended"></a><span data-ttu-id="c8f61-1894">nx_web_http_server_type_get_extended</span><span class="sxs-lookup"><span data-stu-id="c8f61-1894">nx_web_http_server_type_get_extended</span></span>

<span data-ttu-id="c8f61-1895">Istemci HTTP isteğinden dosya türünü Ayıkla</span><span class="sxs-lookup"><span data-stu-id="c8f61-1895">Extract file type from Client HTTP request</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1896">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1896">Prototype</span></span>

```C
UINT nx_web_http_server_type_get_extended(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    CHAR *name, UINT name_length,
    CHAR *http_type_string,
    UINT http_type_string_max_size,
    UINT *string_size);
```

### <a name="description"></a><span data-ttu-id="c8f61-1897">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1897">Description</span></span>

<span data-ttu-id="c8f61-1898">Bu hizmet, arabellek *HTTP_TYPE_STRING* http istek türünü ve (genellikle URL) giriş arabelleği *adından* *string_size* uzunluğunu ayıklar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1898">This service extracts the HTTP request type in the buffer *http_type_string* and its length in *string_size* from the input buffer *name*, usually the URL.</span></span> <span data-ttu-id="c8f61-1899">MIME eşlemesi bulunmazsa, varsayılan olarak "metin/düz" tür olur.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1899">If no MIME map is found, it defaults to the "text/plain" type.</span></span> <span data-ttu-id="c8f61-1900">Aksi takdirde, bir eşleşme için ayıklanan tür, HTTP sunucusu varsayılan MIME eşlemeleriyle karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1900">Otherwise it compares the extracted type against the HTTP Server default MIME maps for a match.</span></span> <span data-ttu-id="c8f61-1901">NetX Web HTTP sunucusundaki varsayılan MIME haritaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c8f61-1901">The default MIME maps in NetX Web HTTP Server are:</span></span>

- <span data-ttu-id="c8f61-1902">HTML metni/HTML</span><span class="sxs-lookup"><span data-stu-id="c8f61-1902">html text/html</span></span>
- <span data-ttu-id="c8f61-1903">htm metin/html</span><span class="sxs-lookup"><span data-stu-id="c8f61-1903">htm text/html</span></span>
- <span data-ttu-id="c8f61-1904">txt metin/düz</span><span class="sxs-lookup"><span data-stu-id="c8f61-1904">txt text/plain</span></span>
- <span data-ttu-id="c8f61-1905">GIF resmi/GIF</span><span class="sxs-lookup"><span data-stu-id="c8f61-1905">gif image/gif</span></span>
- <span data-ttu-id="c8f61-1906">jpg resmi/JPEG</span><span class="sxs-lookup"><span data-stu-id="c8f61-1906">jpg image/jpeg</span></span>
- <span data-ttu-id="c8f61-1907">ICO resmi/x-simgesi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1907">ico image/x-icon</span></span>

<span data-ttu-id="c8f61-1908">Sağlanırsa, Kullanıcı tanımlı ek MIME haritaları kümesi de arar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1908">If supplied, it will also search a user defined set of additional MIME maps.</span></span> <span data-ttu-id="c8f61-1909">Kullanıcı tanımlı haritalar hakkında daha fazla bilgi için bkz. *nx_web_http_server_mime_maps_addtional_set ()* .</span><span class="sxs-lookup"><span data-stu-id="c8f61-1909">See *nx_web_http_server_mime_maps_addtional_set()* for more details on user defined maps.</span></span>

<span data-ttu-id="c8f61-1910">Bu hizmet *nx_web_http_server_type_get*() yerini alır.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1910">This service replaces *nx_web_http_server_type_get*().</span></span> <span data-ttu-id="c8f61-1911">Bu sürüm, çağrı yapanların işleve uzunluk bilgilerini vermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1911">This version requires callers to supply length information to the function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1912">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1912">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1913">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1913">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8f61-1914">**ad** Aranacak arabelleğin işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1914">**name** Pointer to buffer to search</span></span>
- <span data-ttu-id="c8f61-1915">**name_length** Ad uzunluğu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1915">**name_length** Length of name</span></span>
- <span data-ttu-id="c8f61-1916">**http_type_string** Ayıklanan HTML türü dizesi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1916">**http_type_string** Pointer to extracted HTML type string</span></span>
- <span data-ttu-id="c8f61-1917">**http_type_string_max_size** Http_type_string arabellek boyutunun boyutu</span><span class="sxs-lookup"><span data-stu-id="c8f61-1917">**http_type_string_max_size** Size of the http_type_string buffer size</span></span>
- <span data-ttu-id="c8f61-1918">**string_size** Ayıklanan HTML türü dizesini döndürme işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1918">**string_size** Pointer to return extracted HTML type string</span></span>

<span data-ttu-id="c8f61-1919">uzunluklu.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1919">length.</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1920">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1920">Return Values</span></span>

- <span data-ttu-id="c8f61-1921">**NX_SUCCESS** (0x00) tür başarıyla ayıklanamadı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1921">**NX_SUCCESS** (0x00) Successful extraction of type</span></span>
- <span data-ttu-id="c8f61-1922">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1922">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1923">**NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) varsayılan "metin/düz" döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1923">**NX_WEB_HTTP_EXTENSION_MIME_DEFAULT** (0x30019) Default "text/plain" returned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1924">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1924">Allowed From</span></span>

<span data-ttu-id="c8f61-1925">Uygulama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1925">Application</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1926">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1926">Example</span></span>

```C
/* my_server is a previously created HTTP server, which starts accepting client
    requests when *nx_web_http_server_start* is called */

CHAR temp_string[20];
UINT string_length;
UINT ret;

/* Extract the HTTP type. */
ret = nx_web_http_server_type_get_extended(&my_server_ptr,
    my_server.nx_web_http_server_request_resource,
    strlen(my_server.nx_web_http_server_request_resource),
    temp_string,sizeof(temp_string), &string_length);

/* If string_length is non zero, the HTTP string is extracted. */
    For a more detailed example, see the description for
    *nx_web_http_server_callback_generate_response_header().*
```

## <a name="nx_web_http_server_digest_authenticate_notify_set"></a><span data-ttu-id="c8f61-1927">nx_web_http_server_digest_authenticate_notify_set</span><span class="sxs-lookup"><span data-stu-id="c8f61-1927">nx_web_http_server_digest_authenticate_notify_set</span></span>

<span data-ttu-id="c8f61-1928">Özet kimlik doğrulaması geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="c8f61-1928">Set digest authenticate callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1929">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1929">Prototype</span></span>

```C
UINT nx_web_http_server_digest_authenticate_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*digest_authenticate_callback)(NX_WEB_HTTP_SERVER *server_ptr,
        CHAR *name_ptr,
        CHAR *realm_ptr,
        CHAR *password_ptr,
        CHAR *method,
        CHAR *authorization_uri,
        CHAR *authorization_nc,
        CHAR *authorization_cnonce));
```

### <a name="description"></a><span data-ttu-id="c8f61-1930">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1930">Description</span></span>

<span data-ttu-id="c8f61-1931">Bu hizmet Özet kimlik doğrulaması gerçekleştirildiğinde çağrılan geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1931">This service sets the callback invoked when digest authenticate is performed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1932">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1932">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1933">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1933">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8f61-1934">**digest_authenticate_callback** Özet kimlik doğrulaması geri çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1934">**digest_authenticate_callback** Pointer to digest authenticate callback</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1935">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1935">Return Values</span></span>

- <span data-ttu-id="c8f61-1936">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1936">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8f61-1937">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1937">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>
- <span data-ttu-id="c8f61-1938">NX_NOT_SUPPORTED (0x4B) Özet kimlik doğrulaması etkin değil</span><span class="sxs-lookup"><span data-stu-id="c8f61-1938">NX_NOT_SUPPORTED (0x4B) Digest authenticate not enabled</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1939">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1939">Allowed From</span></span>

<span data-ttu-id="c8f61-1940">Uygulama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1940">Application</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1941">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1941">Example</span></span>

```C
UINT digest_authenticate_callback(NX_WEB_HTTP_SERVER *server_ptr, CHAR *name_ptr,
    CHAR *realm_ptr, CHAR *password_ptr, CHAR *method,
    CHAR *authorization_uri, CHAR *authorization_nc,
    CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_WEB_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_web_http_server_create, and
    before starting HTTP services when nx_web_http_server_start is called, set the digest authenticate callback: */
status = nx_web_http_server_digest_authenticate_notify_set(&my_server,
    digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
    will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_web_http_server_authenticate_check_set"></a><span data-ttu-id="c8f61-1942">nx_web_http_server_authenticate_check_set</span><span class="sxs-lookup"><span data-stu-id="c8f61-1942">nx_web_http_server_authenticate_check_set</span></span>

<span data-ttu-id="c8f61-1943">Özet kimlik doğrulaması geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="c8f61-1943">Set digest authenticate callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="c8f61-1944">Prototype</span><span class="sxs-lookup"><span data-stu-id="c8f61-1944">Prototype</span></span>

```C
UINT nx_web_http_server_digest_authenticate_notify_set(
    NX_WEB_HTTP_SERVER *http_server_ptr,
    UINT (*authentication_check_extended)(
        NX_WEB_HTTP_SERVER *server_ptr,
        UINT request_type,
        CHAR *resource,
        CHAR **name,
        UINT *name_length,
        CHAR **password,
        UINT password_length,
        CHAR **realm,
        UINT *realm_length));
```

### <a name="description"></a><span data-ttu-id="c8f61-1945">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1945">Description</span></span>

<span data-ttu-id="c8f61-1946">Bu hizmet, kimlik doğrulama denetimi gerçekleştirildiğinde çağrılan geri aramayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c8f61-1946">This service sets the callback invoked when authenticate check is performed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="c8f61-1947">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1947">Input Parameters</span></span>

- <span data-ttu-id="c8f61-1948">**http_server_ptr** HTTP sunucusu örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1948">**http_server_ptr** Pointer to HTTP Server instance</span></span>
- <span data-ttu-id="c8f61-1949">**authenticate_check_externded** Kimlik doğrulama denetimi geri çağırma işaretçisi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1949">**authenticate_check_externded** Pointer to authenticate check callback</span></span>

### <a name="return-values"></a><span data-ttu-id="c8f61-1950">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="c8f61-1950">Return Values</span></span>

- <span data-ttu-id="c8f61-1951">**NX_SUCCESS** (0x00) geri çağırma başarıyla ayarlandı</span><span class="sxs-lookup"><span data-stu-id="c8f61-1951">**NX_SUCCESS** (0x00) Successfully set the callback</span></span>
- <span data-ttu-id="c8f61-1952">NX_PTR_ERROR (0x07) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="c8f61-1952">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c8f61-1953">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="c8f61-1953">Allowed From</span></span>

<span data-ttu-id="c8f61-1954">Uygulama</span><span class="sxs-lookup"><span data-stu-id="c8f61-1954">Application</span></span>

### <a name="example"></a><span data-ttu-id="c8f61-1955">Örnek</span><span class="sxs-lookup"><span data-stu-id="c8f61-1955">Example</span></span>

```C
UINT authenticate_check_callback(NX_WEB_HTTP_SERVER *server_ptr,
    UINT request_type,
    CHAR *name_ptr, UCHAR *resource, UCHAR **name,
    UINT *name_length, UCHAR **password,
    UINT *password_length, UCHAR **realm,
    UINT *realm_length)
{
    *name = "name";
    *name_length = 4;
    *password = "password";
    *password_length = 8;
    *realm = "realm";
    *realm_length = 5;
    return(NX_SUCCESS);
}

NX_WEB_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_web_http_server_create, and
    before starting HTTP services when nx_web_http_server_start is called, set the authenticate check callback: */

status = nx_web_http_digest_authenticate_check_set (&my_server,
    authenticate_check_callback);

/* If status equals NX_SUCCESS, the authenticate_check_callback function
    will be called when the HTTP server performs authenticate check. */
```
