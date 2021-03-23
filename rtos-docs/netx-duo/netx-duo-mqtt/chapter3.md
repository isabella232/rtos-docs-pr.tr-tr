---
title: Bölüm 3-Azure RTOS NetX Duo MQTT Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo MQTT Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9cbb65946c45bfbc476091f7c604346e839a42fc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825895"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-mqtt-client-services"></a><span data-ttu-id="344c7-103">Bölüm 3-Azure RTOS NetX Duo MQTT istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="344c7-103">Chapter 3 - Description of Azure RTOS NetX Duo MQTT client services</span></span>

<span data-ttu-id="344c7-104">Bu bölüm, tüm Azure RTOS NetX Duo MQTT istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="344c7-104">This chapter contains a description of all Azure RTOS NetX Duo MQTT client services (listed below) in alphabetical order.</span></span>

<span data-ttu-id="344c7-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="344c7-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="344c7-106"> *MQTT istemci örneği nxd_mqtt_client_create oluştur*</span><span class="sxs-lookup"><span data-stu-id="344c7-106">**nxd_mqtt_client_create** *Create MQTT client instance*</span></span>
- <span data-ttu-id="344c7-107">**nxd_mqtt_client_will_message_set** *iletiyi ayarla*</span><span class="sxs-lookup"><span data-stu-id="344c7-107">**nxd_mqtt_client_will_message_set** *Set the will message*</span></span>
- <span data-ttu-id="344c7-108">**nxd_mqtt_client_client_login_set** *MQTT istemci oturum açma Kullanıcı adı ve parolasını ayarlama*</span><span class="sxs-lookup"><span data-stu-id="344c7-108">**nxd_mqtt_client_client_login_set** *Set MQTT client login username and password*</span></span>
- <span data-ttu-id="344c7-109"> *MQTT istemcisini aracıya bağlama* nxd_mqtt_client_connect</span><span class="sxs-lookup"><span data-stu-id="344c7-109">**nxd_mqtt_client_connect** *Connect MQTT Client to the broker*</span></span>
- <span data-ttu-id="344c7-110">**nxd_mqtt_client_secure_connect** *MQTT istemcisini, TLS güvenliği ile aracıya bağlama*</span><span class="sxs-lookup"><span data-stu-id="344c7-110">**nxd_mqtt_client_secure_connect** *Connect MQTT client to the broker with TLS security*</span></span>
- <span data-ttu-id="344c7-111">**nxd_mqtt_client_publish** *aracı aracılığıyla bir ileti yayımlayın.*</span><span class="sxs-lookup"><span data-stu-id="344c7-111">**nxd_mqtt_client_publish** *Publish a message through the broker.*</span></span>
- <span data-ttu-id="344c7-112">**nxd_mqtt_client_subscribe** *bir konuya abone olma*</span><span class="sxs-lookup"><span data-stu-id="344c7-112">**nxd_mqtt_client_subscribe** *Subscribe to a topic*</span></span>
- <span data-ttu-id="344c7-113">**nxd_mqtt_client_unsubscribe** *bir konuyla aboneliğinizi kaldırma*</span><span class="sxs-lookup"><span data-stu-id="344c7-113">**nxd_mqtt_client_unsubscribe** *Unsubscribe from a topic*</span></span>
- <span data-ttu-id="344c7-114"> *MQTT ileti alma geri arama işlevini nxd_mqtt_client_receive_notify_set ayarlama*</span><span class="sxs-lookup"><span data-stu-id="344c7-114">**nxd_mqtt_client_receive_notify_set** *Set MQTT message receive notify callback function*</span></span>
- <span data-ttu-id="344c7-115">**nxd_mqtt_client_message_get** *aracıdan ileti alma*</span><span class="sxs-lookup"><span data-stu-id="344c7-115">**nxd_mqtt_client_message_get** *Retrieve a message from the broker*</span></span>
- <span data-ttu-id="344c7-116"> *MQTT iletisi bağlantısını kesme geri arama işlevini nxd_mqtt_client_disconnect_notify_set ayarla*</span><span class="sxs-lookup"><span data-stu-id="344c7-116">**nxd_mqtt_client_disconnect_notify_set** *Set MQTT message disconnect notify callback function*</span></span>
- <span data-ttu-id="344c7-117">**nxd_mqtt_client_disconnect** *, aracıdan MQTT istemcisinin bağlantısını keser*</span><span class="sxs-lookup"><span data-stu-id="344c7-117">**nxd_mqtt_client_disconnect** *Disconnect MQTT client from the broker*</span></span>
- <span data-ttu-id="344c7-118"> *MQTT istemci örneğini silmek* nxd_mqtt_client_delete</span><span class="sxs-lookup"><span data-stu-id="344c7-118">**nxd_mqtt_client_delete** *Delete the MQTT client instance*</span></span>

## <a name="nxd_mqtt_client_create"></a><span data-ttu-id="344c7-119">nxd_mqtt_client_create</span><span class="sxs-lookup"><span data-stu-id="344c7-119">nxd_mqtt_client_create</span></span>

<span data-ttu-id="344c7-120">MQTT Istemci örneği oluştur</span><span class="sxs-lookup"><span data-stu-id="344c7-120">Create MQTT Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-121">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-121">Prototype</span></span>

```c
UINT nxd_mqtt_client_create(NXD_MQTT_CLIENT *client_ptr,
    CHAR *client_name, CHAR *client_id,
    UINT client_id_length, NX_IP *ip_ptr, NX_PACKET_POOL
    *pool_ptr, VOID *stack_ptr, ULONG stack_size, UINT
    mqtt_thread_priority,
    VOID *memory_ptr, ULONG memory_size);
```

### <a name="description"></a><span data-ttu-id="344c7-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-122">Description</span></span>

<span data-ttu-id="344c7-123">Bu hizmet, belirtilen IP örneğinde bir MQTT Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="344c7-123">This service creates an MQTT Client instance on the specified IP instance.</span></span> <span data-ttu-id="344c7-124">*Client_id* dize, *Istemci tanımlayıcısı (ClientID)* olarak MQTT bağlantı aşamasında sunucuya geçirilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-124">The *client_id* string is passed to the server during MQTT connection phase as the *Client Identifier (ClientId)*.</span></span> <span data-ttu-id="344c7-125">Ayrıca, gerekli ThreadX kaynaklarını (MQTT Istemci görevi iş parçacığı, mutex, olay bayrağı grubu ve TCP yuvası) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="344c7-125">It also creates the necessary ThreadX resources (MQTT Client task thread, mutex, event flag group, and TCP socket).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-126">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-126">Input Parameters</span></span>

- <span data-ttu-id="344c7-127">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-127">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-128">**client_name** İstemci adı dizesi.</span><span class="sxs-lookup"><span data-stu-id="344c7-128">**client_name** Client name string.</span></span>
- <span data-ttu-id="344c7-129">**client_id** Bağlantı aşamasında kullanılan istemci KIMLIĞI dizesi.</span><span class="sxs-lookup"><span data-stu-id="344c7-129">**client_id** Client ID string used during connection phase.</span></span> <span data-ttu-id="344c7-130">MQTT Aracısı, bir istemciyi benzersiz şekilde tanımlamak için bu client_id kullanır.</span><span class="sxs-lookup"><span data-stu-id="344c7-130">MQTT broker uses this client_id to uniquely identify a client.</span></span>
- <span data-ttu-id="344c7-131">**client_id_length** İstemci KIMLIĞI dizesinin bayt cinsinden uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="344c7-131">**client_id_length** Length of the client ID string, in bytes.</span></span>
- <span data-ttu-id="344c7-132">**ip_ptr** IP örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-132">**ip_ptr** Pointer to IP instance.</span></span>
- <span data-ttu-id="344c7-133">**pool_ptr** MQTT istemcisinin işlem için kullandığı paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-133">**pool_ptr** Pointer to a packet pool MQTT client uses for its operation.</span></span>
- <span data-ttu-id="344c7-134">**stack_ptr** MQTT Istemci iş parçacığı için yığın alanı.</span><span class="sxs-lookup"><span data-stu-id="344c7-134">**stack_ptr** Stack area for the MQTT Client thread.</span></span>
- <span data-ttu-id="344c7-135">**stack_size** Yığın alanının bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="344c7-135">**stack_size** Size of the stack area, in bytes.</span></span>
- <span data-ttu-id="344c7-136">**mqtt_thread_priority** MQTT Iş parçacığının önceliği.</span><span class="sxs-lookup"><span data-stu-id="344c7-136">**mqtt_thread_priority** The priority of the MQTT Thread.</span></span>
- <span data-ttu-id="344c7-137">**memory_ptr** Kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="344c7-137">**memory_ptr** Deprecated.</span></span> <span data-ttu-id="344c7-138">Artık kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-138">Not used anymore.</span></span>
- <span data-ttu-id="344c7-139">**memory_size** Kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="344c7-139">**memory_size** Deprecated.</span></span> <span data-ttu-id="344c7-140">Artık kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-140">Not used anymore.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-141">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-141">Return Values</span></span>

- <span data-ttu-id="344c7-142">**NXD_MQTT_SUCCESS** (0x00) MQTT istemcisini başarıyla oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="344c7-142">**NXD_MQTT_SUCCESS** (0x00) Successfully created MQTT client.</span></span>
- <span data-ttu-id="344c7-143">**NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası</span><span class="sxs-lookup"><span data-stu-id="344c7-143">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="344c7-144">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-144">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer.</span></span>
- <span data-ttu-id="344c7-145">NXD_MQTT_INVALID_PARAMETER (0x10009), konu başlığı dizesi, will_retrain_flag veya will_QoS değeri geçersiz.</span><span class="sxs-lookup"><span data-stu-id="344c7-145">NXD_MQTT_INVALID_PARAMETER (0x10009) Invalid will topic string, will_retrain_flag, or will_QoS value.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-146">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-146">Allowed From</span></span>

<span data-ttu-id="344c7-147">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-147">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-148">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-148">Example</span></span>

```c
#define CLIENT_ID_STRING "My Test Client"

#define MQTT_THREAD_PRIORITY 2

NXD_MQTT_CLIENT my_client;
NX_IP ip_0; /* Assume ip_0 is created prior to MQTT client creation. */
NX_PACKET_POOL pool_0;/* Assume pool_0 is created prior to MQTT client creation. */
UCHAR mqtt_thread_stack[STACK_SIZE];

/* Create the MQTT Client instance on "ip_0". */
status = **nxd_mqtt_client_create**(&my_client, "my client",
    CLIENT_ID_STRING, stlren(CLIENT_ID_STRING),
    &ip_0, &pool_0, (VOID*)mqtt_thread_stack, STACK_SIZE,
    MQTT_THREAD_PRIORITY, NX_NULL, 0);

/* If status is NXD_MQTT_SUCCESS an MQTT Client instance was successfully created. */
```

## <a name="nxd_mqtt_client_will_message_set"></a><span data-ttu-id="344c7-149">nxd_mqtt_client_will_message_set</span><span class="sxs-lookup"><span data-stu-id="344c7-149">nxd_mqtt_client_will_message_set</span></span>

<span data-ttu-id="344c7-150">Yapılacak iletileri ayarlar</span><span class="sxs-lookup"><span data-stu-id="344c7-150">Sets the Will message</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-151">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-151">Prototype</span></span>

```c
UINT nxd_mqtt_client_will_message_set(NXD_MQTT_CLIENT
    *client_ptr,
    Const UCHAR *will_topic,
    UINT will_topic_length
    Const UCHAR *will_message,
    UINT will_message_length,
    UINT will_retain_flag,
    UINT will_QoS);
```

### <a name="description"></a><span data-ttu-id="344c7-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-152">Description</span></span>

<span data-ttu-id="344c7-153">Bu hizmet, istemci sunucuya bağlanmadan önce isteğe bağlı olarak yapılacak konuyu ve iletiyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="344c7-153">This service sets the optional will topic and will message before the client connects to the server.</span></span> <span data-ttu-id="344c7-154">Bu konu başlığı UTF-8 kodlu dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="344c7-154">Will topic must be UTF-8 encoded string.</span></span>

<span data-ttu-id="344c7-155">, Ayarlandıysa, CONNECT iletisinin bir parçası olarak aracısına iletilir iletisi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-155">The will message, if set, is transmitted to the broker as part of the CONNECT message.</span></span> <span data-ttu-id="344c7-156">Bu nedenle, kullanmak isteyen uygulamanın MQTT bağlantısı yapmadan önce bu hizmeti kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="344c7-156">Therefore application wishing to use will message must use this service before the MQTT connection is make.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-157">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-157">Input Parameters</span></span>

- <span data-ttu-id="344c7-158">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-158">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-159">**will_topic** UTF-8 kodlu, konu dizesi.</span><span class="sxs-lookup"><span data-stu-id="344c7-159">**will_topic** UTF-8 encoded will topic string.</span></span> <span data-ttu-id="344c7-160">Konunun mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="344c7-160">Will topic must be present.</span></span> <span data-ttu-id="344c7-161">Çağıran, *nx_mqtt_client_connect* çağrısının yapılana kadar will_topic dizenin geçerli kalması gerekir.</span><span class="sxs-lookup"><span data-stu-id="344c7-161">Caller must keep the will_topic string valid till the *nx_mqtt_client_connect* call is made.</span></span>
- <span data-ttu-id="344c7-162">**will_topic_length** Bu konu başlığı dizesindeki bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="344c7-162">**will_topic_length** Number of bytes in the will topic string</span></span>
- <span data-ttu-id="344c7-163">**will_message** Uygulama tanımlı olacaktır iletisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-163">**will_message** Application defined will message.</span></span> <span data-ttu-id="344c7-164">İleti gerekli değilse, uygulama bu alanı NX_NULL olarak ayarlayabilir *.*</span><span class="sxs-lookup"><span data-stu-id="344c7-164">If will message is not required, application can set this field to *NX_NULL.*</span></span>
- <span data-ttu-id="344c7-165">**will_message_length** İleti dizesindeki bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="344c7-165">**will_message_length** Number of bytes in the will message string.</span></span> <span data-ttu-id="344c7-166">Will_message NULL olarak ayarlandıysa, will_message_length 0 olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="344c7-166">If will_message is set to NULL, will_message_length must be set to 0.</span></span>
- <span data-ttu-id="344c7-167">**will_retain_flag** Sunucunun, iletileri bir tutulan ileti olarak yayınlayıp yayımlamayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="344c7-167">**will_retain_flag** Whether the server publishes the will message as a retained message.</span></span> <span data-ttu-id="344c7-168">Geçerli değerler *NX_TRUE* veya *NX_FALSE.*</span><span class="sxs-lookup"><span data-stu-id="344c7-168">Valid values are *NX_TRUE* or *NX_FALSE.*</span></span>
- <span data-ttu-id="344c7-169">**will_QoS** İleti gönderilirken sunucu tarafından kullanılan QoS değeri.</span><span class="sxs-lookup"><span data-stu-id="344c7-169">**will_QoS** QoS value used by the server when sending will message.</span></span> <span data-ttu-id="344c7-170">Geçerli değerler 0 veya 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="344c7-170">Valid values are 0 or 1.</span></span>  

### <a name="return-values"></a><span data-ttu-id="344c7-171">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-171">Return Values</span></span>

- <span data-ttu-id="344c7-172">**NXD_MQTT_SUCCESS** (0x00), iletileri başarıyla ayarlıyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-172">**NXD_MQTT_SUCCESS** (0x00) Successfully sets the will message.</span></span>
- <span data-ttu-id="344c7-173">**NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000c) QoS düzey 2 iletileri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="344c7-173">**NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) QoS level 2 messages are not supported.</span></span>
- <span data-ttu-id="344c7-174">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu.</span><span class="sxs-lookup"><span data-stu-id="344c7-174">NX_PTR_ERROR (0x07) Invalid MQTT control block.</span></span>
- <span data-ttu-id="344c7-175">NXD_MQTT_INVALID_PARAMETER (0x10009), konu başlığı dizesi, will_retrain_flag veya will_QoS değeri geçersiz.</span><span class="sxs-lookup"><span data-stu-id="344c7-175">NXD_MQTT_INVALID_PARAMETER (0x10009) Invalid will topic string, will_retrain_flag, or will_QoS value.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-176">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-176">Allowed From</span></span>

<span data-ttu-id="344c7-177">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-177">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-178">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-178">Example</span></span>

```c
#define WILL_TOPIC "my_will_topic"

#define WILL_MESSAGE "my will message"

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_will_message_set(&my_client,
    WILL_TOPIC, STRLEN(WILL_TOPIC),
    WILL_MESSAGE, STRLEN(WILL_MESSAGE),
    NX_TRUE, 0);

/* If status is NXD_MQTT_SUCCESS the will message is properly
configured for the session. It will be transmitted to the server
during MQTT connection. */
```

## <a name="nxd_mqtt_client_login_set"></a><span data-ttu-id="344c7-179">nxd_mqtt_client_login_set</span><span class="sxs-lookup"><span data-stu-id="344c7-179">nxd_mqtt_client_login_set</span></span>

<span data-ttu-id="344c7-180">MQTT istemci oturum açma Kullanıcı adı ve parolasını ayarlar</span><span class="sxs-lookup"><span data-stu-id="344c7-180">Sets MQTT client login username and password</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-181">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-181">Prototype</span></span>

```c
UINT nxd_mqtt_client_login_set(NXD_MQTT_CLIENT *client_ptr,
    Const UCHAR *username,
    UINT username_length
    Const UCHAR *password,
    UINT password_length);
```

### <a name="description"></a><span data-ttu-id="344c7-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-182">Description</span></span>

<span data-ttu-id="344c7-183">Bu hizmet, kimlik doğrulama amacıyla MQTT bağlantı aşamasında kullanılan Kullanıcı adını ve parolayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="344c7-183">This service sets the username and password, which is used during MQTT connection phase for log in authentication purpose.</span></span>

<span data-ttu-id="344c7-184">Kullanıcı adı ve parolayla MQTT istemci oturumu açma isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="344c7-184">The MQTT client login with username and password is optional.</span></span> <span data-ttu-id="344c7-185">Sunucunun Kullanıcı adı ve parola gerektirdiği durumlarda, bağlantı oluşturulmadan önce Kullanıcı adı ve parolanın ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="344c7-185">In situations where the server requires a user name and password, the user name and password must be set before the connection is established.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-186">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-186">Input Parameters</span></span>

- <span data-ttu-id="344c7-187">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-187">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-188">**Kullanıcı adı** UTF-8 kodlu Kullanıcı adı dizesi.</span><span class="sxs-lookup"><span data-stu-id="344c7-188">**username** UTF-8 encoded user name string.</span></span> <span data-ttu-id="344c7-189">Çağıran, *nx_mqtt_client_connect* çağrısı yapıldığından Kullanıcı adı dizesinin geçerli kalmasını sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="344c7-189">Caller must keep the username string valid till the *nx_mqtt_client_connect* call is made.</span></span>
- <span data-ttu-id="344c7-190">**username_length** Kullanıcı adı dizesindeki bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="344c7-190">**username_length** Number of bytes in the username string</span></span>
- <span data-ttu-id="344c7-191">**parola** Parola dizesi.</span><span class="sxs-lookup"><span data-stu-id="344c7-191">**password** Password string.</span></span> <span data-ttu-id="344c7-192">Parola gerekmiyorsa, bu alan NX_NULL olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-192">If password is not required, this field may be set to NX_NULL.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-193">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-193">Return Values</span></span>

- <span data-ttu-id="344c7-194">**NXD_MQTT_SUCCESS** (0x00), iletileri başarıyla ayarlıyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-194">**NXD_MQTT_SUCCESS** (0x00) Successfully sets the will message.</span></span>
- <span data-ttu-id="344c7-195">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu.</span><span class="sxs-lookup"><span data-stu-id="344c7-195">NX_PTR_ERROR (0x07) Invalid MQTT control block.</span></span>
- <span data-ttu-id="344c7-196">NXD_MQTT_INVALID_PARAMETER (0x10009) geçersiz Kullanıcı adı dizesi veya parola dizesi.</span><span class="sxs-lookup"><span data-stu-id="344c7-196">NXD_MQTT_INVALID_PARAMETER (0x10009) Invalid username string or the password string.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-197">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-197">Allowed From</span></span>

<span data-ttu-id="344c7-198">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-198">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-199">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-199">Example</span></span>

```c
#define USERNAME "MY_NAME"

#define PASSWORD "MY_LOGIN_SECRET"

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_login_set(&my_client,
    USERNAME, STRLEN(USERNAME),
    PASSWORD, STRLEN(PASSWORD));

/* If status is NXD_MQTT_SUCCESS the username and the password 
are set for the session. This information will be 
transmitted to the server during MQTT connection. */
```

## <a name="nxd_mqtt_client_connect"></a><span data-ttu-id="344c7-200">nxd_mqtt_client_connect</span><span class="sxs-lookup"><span data-stu-id="344c7-200">nxd_mqtt_client_connect</span></span>

<span data-ttu-id="344c7-201">MQTT Istemcisini aracıya bağlama</span><span class="sxs-lookup"><span data-stu-id="344c7-201">Connect MQTT Client to the broker</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-202">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-202">Prototype</span></span>

```c
UINT nxd_mqtt_client_connect(NXD_MQTT_CLIENT *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT keepalive, UINT clean_session, ULONG wait_option));
```

### <a name="description"></a><span data-ttu-id="344c7-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-203">Description</span></span>

<span data-ttu-id="344c7-204">Bu hizmet, aracıya bir bağlantı başlatır.</span><span class="sxs-lookup"><span data-stu-id="344c7-204">This service initiates a connection to the broker.</span></span> <span data-ttu-id="344c7-205">İlk olarak bir TCP yuvasını bağlar ve bir TCP bağlantısı yapar.</span><span class="sxs-lookup"><span data-stu-id="344c7-205">First it binds a TCP socket, then makes a TCP connection.</span></span> <span data-ttu-id="344c7-206">Başarılı olduğunu varsayarsak, MQTT canlı tut özelliği etkinse bir zamanlayıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="344c7-206">Assuming that succeeds, it creates a timer if the MQTT keep alive feature is enabled.</span></span> <span data-ttu-id="344c7-207">Ardından MQTT sunucusu (Broker) ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="344c7-207">Then it connects with the MQTT server (broker).</span></span>

<span data-ttu-id="344c7-208">Bu hizmetin TLS koruması olmayan bir MQTT bağlantısı oluşturduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="344c7-208">Note that this service creates an MQTT connection with no TLS protection.</span></span> <span data-ttu-id="344c7-209">Güvenli bir MQTT bağlantısı oluşturmak için, uygulama ***nxd_mqtt_client_secure_connect ()*** hizmetini kullanır.</span><span class="sxs-lookup"><span data-stu-id="344c7-209">To create a secure MQTT connection, the application shall use the service ***nxd_mqtt_client_secure_connect().***</span></span>

<span data-ttu-id="344c7-210">Bağlantı kurulduğunda, istemci *clean_session* NX_FALSE olarak ayarlarsa, istemci henüz kabul edilmemiş olan tüm iletileri yeniden gönderilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-210">Upon the connection, if the client sets the *clean_session* to NX_FALSE, the client will retransmit any messages stored that have not been acknowledged yet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-211">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-211">Input Parameters</span></span>

- <span data-ttu-id="344c7-212">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-212">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-213">**server_ip** Aracı IP adresi.</span><span class="sxs-lookup"><span data-stu-id="344c7-213">**server_ip** Broker IP address.</span></span>
- <span data-ttu-id="344c7-214">**SERVER_PORT** Aracı bağlantı noktası numarası.</span><span class="sxs-lookup"><span data-stu-id="344c7-214">**server_port** Broker port number.</span></span> <span data-ttu-id="344c7-215">MQTT için varsayılan bağlantı noktası **_NXD_MQTT_PORT_** (1883) olarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="344c7-215">The default port for MQTT is defined as **_NXD_MQTT_PORT_** (1883).</span></span>
- <span data-ttu-id="344c7-216">**keep_alive** Oturum sırasında kullanılmak üzere etkin tut değeri (saniye cinsinden).</span><span class="sxs-lookup"><span data-stu-id="344c7-216">**keep_alive** The keep alive value, in seconds, to be used during the session.</span></span> <span data-ttu-id="344c7-217">Değer, aracı bu istemcinin zaman aşımına uğramadan önce aracıya gönderilen iki MQTT denetim iletisi arasındaki en uzun süreyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="344c7-217">The value indicates the maximum time between two MQTT control messages being sent to the broker before the broker times out this client.</span></span> <span data-ttu-id="344c7-218">0 değeri, etkin tut özelliğini kapatır.</span><span class="sxs-lookup"><span data-stu-id="344c7-218">The value 0 turns off the keep-alive feature.</span></span>
- <span data-ttu-id="344c7-219">**clean_session** Sunucunun bu oturumu Temizleme işleminin başlatılıp başlatılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="344c7-219">**clean_session** Whether the server shall start this session clean.</span></span> <span data-ttu-id="344c7-220">Geçerli seçenekler şunlardır **_NX_TRUE_*_ veya _*_NX_FALSE._**</span><span class="sxs-lookup"><span data-stu-id="344c7-220">Valid options are **_NX_TRUE_*_ or _*_NX_FALSE._**</span></span>
- <span data-ttu-id="344c7-221">**wait_option** Bağlantı bekleme süresi.</span><span class="sxs-lookup"><span data-stu-id="344c7-221">**wait_option** Connection wait time.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-222">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-222">Return Values</span></span>

- <span data-ttu-id="344c7-223">**NXD_MQTT_SUCCESS** (0x00) başarılı MQTT bağlantısı</span><span class="sxs-lookup"><span data-stu-id="344c7-223">**NXD_MQTT_SUCCESS** (0x00) Successful MQTT connection</span></span>
- <span data-ttu-id="344c7-224">**NXD_MQTT_ALREADY_CONNECTED** (0x10001) istemci, aracıya zaten bağlı.</span><span class="sxs-lookup"><span data-stu-id="344c7-224">**NXD_MQTT_ALREADY_CONNECTED** (0x10001) The client is already connected to the broker.</span></span>
- <span data-ttu-id="344c7-225">**NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX elde edilemedi</span><span class="sxs-lookup"><span data-stu-id="344c7-225">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex</span></span> 
- <span data-ttu-id="344c7-226">**NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası</span><span class="sxs-lookup"><span data-stu-id="344c7-226">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="344c7-227">**NXD_MQTT_CONNECT_FAILURE** (0x10005) aracıya bağlanılamadı.</span><span class="sxs-lookup"><span data-stu-id="344c7-227">**NXD_MQTT_CONNECT_FAILURE** (0x10005) Failed to connect to the broker.</span></span>
- <span data-ttu-id="344c7-228">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) aracıya ileti gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-228">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Unable to send messages to the broker.</span></span>
- <span data-ttu-id="344c7-229">**NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) sunucu hatayla yanıtladı</span><span class="sxs-lookup"><span data-stu-id="344c7-229">**NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) Server responded with error</span></span>
- <span data-ttu-id="344c7-230">**NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-230">**NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081) Server response code</span></span>
- <span data-ttu-id="344c7-231">**NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-231">**NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082) Server response code</span></span>
- <span data-ttu-id="344c7-232">**NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-232">**NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083) Server response code</span></span>
- <span data-ttu-id="344c7-233">**NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-233">**NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084) Server response code</span></span>
- <span data-ttu-id="344c7-234">**NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-234">**NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085) Server response code</span></span>
- <span data-ttu-id="344c7-235">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="344c7-235">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-236">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-236">Allowed From</span></span>

<span data-ttu-id="344c7-237">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-237">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-238">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-238">Example</span></span>

```c
NXD_ADDRESS broker_address;

/* Set up broker IP address */
broker_address.nxd_ip_version = 4;
broker_address.nxd_ip_address.v4 = MQTT_BROKER_ADDRESS;

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_connect(&my_client, &broker_address,
    NXD_MQTT_PORT,
    0, /* Turn off keepalive */
    NX_TRUE, /* Clean session flag set */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS a connection to the broker is successfully established. */
```

## <a name="nxd_mqtt_client_secure_connect"></a><span data-ttu-id="344c7-239">nxd_mqtt_client_secure_connect</span><span class="sxs-lookup"><span data-stu-id="344c7-239">nxd_mqtt_client_secure_connect</span></span>

<span data-ttu-id="344c7-240">MQTT istemcisini TLS güvenliği ile aracıya bağlama</span><span class="sxs-lookup"><span data-stu-id="344c7-240">Connect MQTT client to the broker with TLS security</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-241">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-241">Prototype</span></span>

```c
UINT nxd_mqtt_client_secure_connect(NXD_MQTT_CLIENT
    *client_ptr,
    NXD_ADDRESS *server_ip, UINT server_port,
    UINT (*tls_setup)(NXD_MQTT_CLIENT *,
        NX_SECURE_TLS_SESISON *,
        NX_SECURE_TLS_CERTIFICATE *,
        NX_SECURE_TLS_CERTIFICATE *),
    UINT keepalive, UINT connection_flag,
    UINT clean_session, ULONG wait_option));
```

### <a name="description"></a><span data-ttu-id="344c7-242">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-242">Description</span></span>

<span data-ttu-id="344c7-243">Bu hizmet, bağlantı TCP yerine TLS katmanından geçilerek ***nxd_mqtt_client_connect*** aynıdır.</span><span class="sxs-lookup"><span data-stu-id="344c7-243">This service is identical to ***nxd_mqtt_client_connect*** except that the connection goes through TLS layer instead of TCP.</span></span> <span data-ttu-id="344c7-244">Bu nedenle, istemci ile aracı arasındaki iletişim güvenli hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-244">Therefore, communication between the client and the broker is secured.</span></span>

<span data-ttu-id="344c7-245">Kullanıcı tanımlı *tls_setup* , MQTT istemcisinin MQTT istemci bağlantısı yapmadan önce kullandığı bir geri çağırma işlevidir.</span><span class="sxs-lookup"><span data-stu-id="344c7-245">The user-defined *tls_setup* is a callback function that the MQTT client uses prior to making a MQTT client connection.</span></span> <span data-ttu-id="344c7-246">Uygulama NetX güvenli TLS 'yi başlatır, güvenlik parametrelerini yapılandırır ve TLS el sıkışması sırasında kullanılacak ilgili sertifikaları yükler.</span><span class="sxs-lookup"><span data-stu-id="344c7-246">The application shall initialize NetX Secure TLS, configure security parameters, and load relevant certificates to be used during TLS handshake.</span></span> <span data-ttu-id="344c7-247">Asıl TLS el sıkışması, aracının MQTT TLS bağlantı noktasında bir TCP bağlantısı kurulduktan sonra olur (varsayılan TCP bağlantı noktası 8883).</span><span class="sxs-lookup"><span data-stu-id="344c7-247">The actual TLS handshake happens after a TCP connection is established on the broker's MQTT TLS port (default TCP port 8883).</span></span> <span data-ttu-id="344c7-248">TLS el sıkışması başarılı olduktan sonra MQTT CONNECT denetim paketi TLS aracılığıyla gönderilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-248">Once the TLS handshake is successful, the MQTT CONNECT control packet is sent via TLS.</span></span>

<span data-ttu-id="344c7-249">Güvenli bağlantılar oluşturmak için, NetX güvenli TLS kitaplığı kullanılabilir olmalıdır ve NetX Duo MQTT istemcisinin tanımlanmış ***NX_SECURE_ENABLE*** oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="344c7-249">To make secure connections, the NetX Secure TLS library must be available, and the NetX Duo MQTT client must be built with ***NX_SECURE_ENABLE*** defined.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-250">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-250">Input Parameters</span></span>

- <span data-ttu-id="344c7-251">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-251">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-252">**server_ip** Aracı IP adresi.</span><span class="sxs-lookup"><span data-stu-id="344c7-252">**server_ip** Broker IP address.</span></span>
- <span data-ttu-id="344c7-253">**SERVER_PORT** Aracı bağlantı noktası numarası.</span><span class="sxs-lookup"><span data-stu-id="344c7-253">**server_port** Broker port number.</span></span> <span data-ttu-id="344c7-254">MQTT için varsayılan bağlantı noktası **_NXD_MQTT_TLS_PORT_** olarak tanımlanır (8883).</span><span class="sxs-lookup"><span data-stu-id="344c7-254">The default port for MQTT isdefined as **_NXD_MQTT_TLS_PORT_** (8883).</span></span>
- <span data-ttu-id="344c7-255">**tls_setup** Kullanıcı tarafından sunulan TLS kurulum geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="344c7-255">**tls_setup** User-provided TLS Setup callback function.</span></span> <span data-ttu-id="344c7-256">Bu geri çağırma işlevi, TLS istemci bağlantı parametrelerini ayarlamak için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="344c7-256">This callback function is invoked to set up TLS client connection parameters.</span></span>
- <span data-ttu-id="344c7-257">**keep_alive** Oturum sırasında kullanılacak etkin tut değeri.</span><span class="sxs-lookup"><span data-stu-id="344c7-257">**keep_alive** The keep-alive value to be used during the session.</span></span> <span data-ttu-id="344c7-258">0 değeri, etkin tut özelliğini kapatır.</span><span class="sxs-lookup"><span data-stu-id="344c7-258">The value 0 turns off the keep-alive feature.</span></span>
- <span data-ttu-id="344c7-259">**clean_session** Sunucunun bu oturumu Temizleme işleminin başlatılıp başlatılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="344c7-259">**clean_session** Whether or not the server shall start this session clean.</span></span> <span data-ttu-id="344c7-260">Geçerli seçenekler şunlardır **_NX_TRUE_*_ veya _*_NX_FALSE._**</span><span class="sxs-lookup"><span data-stu-id="344c7-260">Valid options are **_NX_TRUE_*_ or _*_NX_FALSE._**</span></span>
- <span data-ttu-id="344c7-261">**wait_option** Bağlantı bekleme süresi.</span><span class="sxs-lookup"><span data-stu-id="344c7-261">**wait_option** Connection wait time.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-262">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-262">Return Values</span></span>

- <span data-ttu-id="344c7-263">**NXD_MQTT_SUCCESS** (0x00) TLS aracılığıyla kurulan başarılı MQTT istemci bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="344c7-263">**NXD_MQTT_SUCCESS** (0x00) Successful MQTT client connection established via TLS.</span></span>
- <span data-ttu-id="344c7-264">**NXD_MQTT_ALREADY_CONNECTED** (0x10001) istemci, aracıya zaten bağlı.</span><span class="sxs-lookup"><span data-stu-id="344c7-264">**NXD_MQTT_ALREADY_CONNECTED** (0x10001) The client is already connected to the broker.</span></span>
- <span data-ttu-id="344c7-265">**NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX elde edilemedi</span><span class="sxs-lookup"><span data-stu-id="344c7-265">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex</span></span> 
- <span data-ttu-id="344c7-266">**NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası</span><span class="sxs-lookup"><span data-stu-id="344c7-266">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="344c7-267">**NXD_MQTT_CONNECT_FAILURE** (0x10005) aracıya bağlanılamadı.</span><span class="sxs-lookup"><span data-stu-id="344c7-267">**NXD_MQTT_CONNECT_FAILURE** (0x10005) Failed to connect to the broker.</span></span>
- <span data-ttu-id="344c7-268">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) aracıya ileti gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-268">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Unable to send messages to the broker.</span></span>
- <span data-ttu-id="344c7-269">**NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) sunucusu hata iletisiyle yanıtladı.</span><span class="sxs-lookup"><span data-stu-id="344c7-269">**NXD_MQTT_SERVER_MESSAGE_FAILURE** (0x10008) Server responded with error message.</span></span>
- <span data-ttu-id="344c7-270">**NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-270">**NXD_MQTT_ERROR_UNACCEPTABLE_PROTOCOL** (0x10081) Server response code</span></span>
- <span data-ttu-id="344c7-271">**NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-271">**NXD_MQTT_ERROR_IDENTIFYIER_REJECTED** (0x10082) Server response code</span></span>
- <span data-ttu-id="344c7-272">**NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-272">**NXD_MQTT_ERROR_SERVER_UNAVAILABLE** (0x10083) Server response code</span></span>
- <span data-ttu-id="344c7-273">**NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-273">**NXD_MQTT_ERROR_BAD_USERNAME_PASSWORD** (0x10084) Server response code</span></span>
- <span data-ttu-id="344c7-274">**NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085) sunucu yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="344c7-274">**NXD_MQTT_ERROR_NOT_AUTHORIZED** (0x10085) Server response code</span></span>
- <span data-ttu-id="344c7-275">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu veya sunucu adresi yapısı.</span><span class="sxs-lookup"><span data-stu-id="344c7-275">NX_PTR_ERROR (0x07) Invalid MQTT control block or sever address structure.</span></span>
- <span data-ttu-id="344c7-276">NX_INVALID_PORT (0x46) sunucu bağlantı noktası 0 olamaz.</span><span class="sxs-lookup"><span data-stu-id="344c7-276">NX_INVALID_PORT (0x46) Server port cannot be 0.</span></span>
- <span data-ttu-id="344c7-277">NXD_MQTT_INVALID_PARAMETER (0x10009) giriş parametresi hatası</span><span class="sxs-lookup"><span data-stu-id="344c7-277">NXD_MQTT_INVALID_PARAMETER (0x10009) Input parameter error</span></span>
- <span data-ttu-id="344c7-278">NXD_MQTT_CLIENT_NOT_RUNNING (0x1000E) MQTT Iş parçacığı henüz çalışmaya başlamadı.</span><span class="sxs-lookup"><span data-stu-id="344c7-278">NXD_MQTT_CLIENT_NOT_RUNNING (0x1000E) MQTT Thread has not started running yet.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-279">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-279">Allowed From</span></span>

<span data-ttu-id="344c7-280">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-280">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-281">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-281">Example</span></span>

```c
/* TLS setup routine. This function is responsible for setting up TLS parameters.*/
UINT tls_setup_callback(NXD_MQTT_CLIENT *client_ptr,
    NX_SECURE_TLS_SESSION *session_ptr,
    NX_SECURE_TLS_CERTIFICATE *certificate_ptr,
    NX_SECURE_TLS_CERTIFICATE *trusted_certificate,
    UINT timeout)
{
/* Note this routine is simplified to highlight the
necessary steps to setup a TLS session. Each
application may employ different procedures suitable for
its TLS settings, such as cipher suite, certificates. */

/* Create a TLS session for the MQTT connection, and pass
in various crypto methods this session can use for the
initial TLS handshake. */

/* Load appropriate certificates, or set up session key for Pre-share key operation. */

/* Start the TLS session */

/* Return NX_SUCCESS if the TLS session is established. */
    return(NX_SUCCESS);
}

NXD_ADDRESS broker_address;

/* Set up broker IP address */
broker_address.nxd_ip_version = 4;
broker_address.nxd_ip_address.v4 = MQTT_BROKER_ADDRESS;

/* Create the MQTT Client instance "my_client" on "ip_0". */
status = nxd_mqtt_client_secure_connect(&my_client,
    &server_address, NXD_MQTT_TLS_PORT, tls_setup_callback,
    0, /* Turn off keepalive */
    NX_TRUE, /* Clean session set */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS the MQTT Client was successfully connected to the broker via TLS. */
```

## <a name="nxd_mqtt_client_publish"></a><span data-ttu-id="344c7-282">nxd_mqtt_client_publish</span><span class="sxs-lookup"><span data-stu-id="344c7-282">nxd_mqtt_client_publish</span></span>

<span data-ttu-id="344c7-283">Aracı aracılığıyla bir ileti yayımlayın</span><span class="sxs-lookup"><span data-stu-id="344c7-283">Publish a message through the broker</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-284">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-284">Prototype</span></span>

```c
UINT nxd_mqtt_client_publish(NXD_MQTT_CLIENT *client_ptr,
    CHAR *topic_name, UINT topic_name_length, CHAR *message, UINT
    message_length,
    UINT retain, UINT QoS, ULONG timeout);
```

### <a name="description"></a><span data-ttu-id="344c7-285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-285">Description</span></span>

<span data-ttu-id="344c7-286">Bu hizmet, aracı aracılığıyla bir ileti yayımlar.</span><span class="sxs-lookup"><span data-stu-id="344c7-286">This service publishes a message through the broker.</span></span> <span data-ttu-id="344c7-287">QoS düzey 2 iletilerinin yayımlanması henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-287">Publishing QoS level 2 messages is not supported yet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-288">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-288">Input Parameters</span></span>

- <span data-ttu-id="344c7-289">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-289">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-290">**topic_name** ' De yayımlanacak konu.</span><span class="sxs-lookup"><span data-stu-id="344c7-290">**topic_name** Topic to publish to.</span></span>
- <span data-ttu-id="344c7-291">**topic_name_length** Konunun uzunluğu (bayt).</span><span class="sxs-lookup"><span data-stu-id="344c7-291">**topic_name_length** Length of the topic, in bytes.</span></span>
- <span data-ttu-id="344c7-292">**ileti** İleti arabelleğinin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-292">**message** Pointer to the message buffer.</span></span>
- <span data-ttu-id="344c7-293">**message_length** İletinin bayt cinsinden boyutu</span><span class="sxs-lookup"><span data-stu-id="344c7-293">**message_length** Size of the message, in bytes</span></span>
- <span data-ttu-id="344c7-294">**sakla** Aracının iletiyi tutyacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="344c7-294">**retain** Determines if the broker shall retain the message.</span></span>
- <span data-ttu-id="344c7-295">**QoS** İstenen QoS değeri: 0 veya 1.</span><span class="sxs-lookup"><span data-stu-id="344c7-295">**QoS** The desired QoS value: 0 or 1.</span></span>
- <span data-ttu-id="344c7-296">**zaman aşımı** Zaman aşımı değeri</span><span class="sxs-lookup"><span data-stu-id="344c7-296">**timeout** Timeout value</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-297">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-297">Return Values</span></span>

- <span data-ttu-id="344c7-298">**NXD_MQTT_SUCCESS** (0x00) başarılı MQTT istemci oluşturma</span><span class="sxs-lookup"><span data-stu-id="344c7-298">**NXD_MQTT_SUCCESS** (0x00) Successful MQTT Client create</span></span>
- <span data-ttu-id="344c7-299">**NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası.</span><span class="sxs-lookup"><span data-stu-id="344c7-299">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error.</span></span>
- <span data-ttu-id="344c7-300">**NXD_MQTT_PACKET_POOL_FAILURE** (0x10006) paket havuzundan paket alamadı.</span><span class="sxs-lookup"><span data-stu-id="344c7-300">**NXD_MQTT_PACKET_POOL_FAILURE** (0x10006) Failed to obtain packet from the packet pool.</span></span>
- <span data-ttu-id="344c7-301">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007), aracıyla iletişim kuramadı.</span><span class="sxs-lookup"><span data-stu-id="344c7-301">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Failed to communication with the broker.</span></span>
- <span data-ttu-id="344c7-302">**NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000c) QoS düzey 2 iletileri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="344c7-302">**NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) QoS level 2 messages are not supported.</span></span>
- <span data-ttu-id="344c7-303">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="344c7-303">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="344c7-304">NXD_MQTT_INVALID_PARAMETER (0x10009) giriş parametresi hatası</span><span class="sxs-lookup"><span data-stu-id="344c7-304">NXD_MQTT_INVALID_PARAMETER (0x10009) Input parameter error</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-305">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-305">Allowed From</span></span>

<span data-ttu-id="344c7-306">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-306">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-307">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-307">Example</span></span>

```c
CHAR *topic = "temperature";
CHAR *message = "100";

/* Publish the temperature value. */
status = nxd_mqtt_client_publish(&my_client,
    topic, STRLEN(topic),
    message, STRLEN(message),
    NX_TRUE, /* Server retains message. */);
    0, /* QOS */
    NX_WAIT_FOREVER);

/* If status is NXD_MQTT_SUCCESS the message has been 
successfully sent to the broker. */
```

## <a name="nxd_mqtt_client_subscribe"></a><span data-ttu-id="344c7-308">nxd_mqtt_client_subscribe</span><span class="sxs-lookup"><span data-stu-id="344c7-308">nxd_mqtt_client_subscribe</span></span>

<span data-ttu-id="344c7-309">Bir konuya abone olma</span><span class="sxs-lookup"><span data-stu-id="344c7-309">Subscribe to a topic</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-310">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-310">Prototype</span></span>

```c
UINT nxd_mqtt_client_subscribe(NXD_MQTT_CLIENT
    *mqtt_client_ptr, CHAR *topic_name,
    UINT topic_name_length, UINT QoS);
```

### <a name="description"></a><span data-ttu-id="344c7-311">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-311">Description</span></span>

<span data-ttu-id="344c7-312">Bu hizmet belirli bir konuya abone olur.</span><span class="sxs-lookup"><span data-stu-id="344c7-312">This service subscribes to a specific topic.</span></span> <span data-ttu-id="344c7-313">QoS düzey 2 iletilerine abone olma henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-313">Subscribing to QoS level 2 messages is not supported yet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-314">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-314">Input Parameters</span></span>

- <span data-ttu-id="344c7-315">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-315">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-316">**topic_name** ' De yayımlanacak konu.</span><span class="sxs-lookup"><span data-stu-id="344c7-316">**topic_name** Topic to publish to.</span></span>
- <span data-ttu-id="344c7-317">**topic_name_length** Konunun uzunluğu (bayt).</span><span class="sxs-lookup"><span data-stu-id="344c7-317">**topic_name_length** Length of the topic, in bytes.</span></span>
- <span data-ttu-id="344c7-318">**QoS Istenen QoS düzeyi:** 0 veya 1.</span><span class="sxs-lookup"><span data-stu-id="344c7-318">**QoS The desired QoS level:** 0 or 1.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-319">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-319">Return Values</span></span>

- <span data-ttu-id="344c7-320">**NXD_MQTT_SUCCESS** (0x00) konuya başarıyla abone oldu.</span><span class="sxs-lookup"><span data-stu-id="344c7-320">**NXD_MQTT_SUCCESS** (0x00) Successfully subscribed to the topic.</span></span>
- <span data-ttu-id="344c7-321">**NXD_MQTT_NOT_CONNECTED** (0x10002) istemci, aracıya bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="344c7-321">**NXD_MQTT_NOT_CONNECTED** (0x10002) The client is not connected to the broker.</span></span>
- <span data-ttu-id="344c7-322">**NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX elde edilemedi</span><span class="sxs-lookup"><span data-stu-id="344c7-322">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex</span></span>
- <span data-ttu-id="344c7-323">**NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası</span><span class="sxs-lookup"><span data-stu-id="344c7-323">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="344c7-324">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) aracıya ileti gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-324">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Unable to send messages to the broker.</span></span>
- <span data-ttu-id="344c7-325">**NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000c) QoS düzey 2 iletileri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="344c7-325">**NXD_MQTT_QOS2_NOT_SUPPORTED** (0x1000C) QoS level 2messages are not supported.</span></span>
- <span data-ttu-id="344c7-326">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="344c7-326">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="344c7-327">NXD_MQTT_INVALID_PARAMETER (0x10009) topic_name ayarlı değil veya topic_name_length sıfır ya da QoS değeri geçersiz.</span><span class="sxs-lookup"><span data-stu-id="344c7-327">NXD_MQTT_INVALID_PARAMETER (0x10009) topic_name is not set, or topic_name_length is zero, or QoS is value is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-328">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-328">Allowed From</span></span>

<span data-ttu-id="344c7-329">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-329">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-330">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-330">Example</span></span>

```c
/* Subscribe to the topic "temperature" with QoS level 0 */
CHAR *topic = "temperature";

status = nxd_mqtt_client_subscribe(&my_client, topic,
    STRLEN(topic), 0);

/* If status is NXD_MQTT_SUCCESS, the client successfully
subscribes to the topic "temperate". At this point the client
is ready for receiving messages from the broker. */
```

## <a name="nxd_mqtt_client_unsubscribe"></a><span data-ttu-id="344c7-331">nxd_mqtt_client_unsubscribe</span><span class="sxs-lookup"><span data-stu-id="344c7-331">nxd_mqtt_client_unsubscribe</span></span>

<span data-ttu-id="344c7-332">Bir konuyla abonelik kaldırma</span><span class="sxs-lookup"><span data-stu-id="344c7-332">Unsubscribe from a topic</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-333">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-333">Prototype</span></span>

```c
UINT nxd_mqtt_client_unsubscribe(NXD_MQTT_CLIENT
    *mqtt_client_pr,
    CHAR *topic_name,
    UINT topic_name_length);
```

### <a name="description"></a><span data-ttu-id="344c7-334">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-334">Description</span></span>

<span data-ttu-id="344c7-335">Bu hizmet, bir konudan aboneliği kaldırır.</span><span class="sxs-lookup"><span data-stu-id="344c7-335">This service unsubscribes from a topic.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-336">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-336">Input Parameters</span></span>

- <span data-ttu-id="344c7-337">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-337">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-338">**topic_name** Aboneliği kaldırma konusu.</span><span class="sxs-lookup"><span data-stu-id="344c7-338">**topic_name** Topic to unsubscribe from.</span></span>
- <span data-ttu-id="344c7-339">**topic_name_length** Konunun uzunluğu (bayt).</span><span class="sxs-lookup"><span data-stu-id="344c7-339">**topic_name_length** Length of the topic, in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-340">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-340">Return Values</span></span>

- <span data-ttu-id="344c7-341">**NXD_MQTT_SUCCESS** (0x00), konunun aboneliği başarıyla kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="344c7-341">**NXD_MQTT_SUCCESS** (0x00) Successfully unsubscribed from the topic.</span></span>
- <span data-ttu-id="344c7-342">**NXD_MQTT_NOT_CONNECTED** (0x10002) istemci, aracıya bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="344c7-342">**NXD_MQTT_NOT_CONNECTED** (0x10002) The client is not connected to the broker.</span></span>
- <span data-ttu-id="344c7-343">**NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX 'i alamadı.</span><span class="sxs-lookup"><span data-stu-id="344c7-343">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex.</span></span>
- <span data-ttu-id="344c7-344">**NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası</span><span class="sxs-lookup"><span data-stu-id="344c7-344">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="344c7-345">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) aracıya ileti gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="344c7-345">**NXD_MQTT_COMMUNICATION_FAILURE** (0x10007) Unable to send messages to the broker.</span></span>
- <span data-ttu-id="344c7-346">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="344c7-346">NX_PTR_ERROR (0x07) Invalid MQTT control block pointer</span></span>
- <span data-ttu-id="344c7-347">NXD_MQTT_INVALID_PARAMETER (0x10009) topic_name ayarlı değil veya topic_name_length sıfır.</span><span class="sxs-lookup"><span data-stu-id="344c7-347">NXD_MQTT_INVALID_PARAMETER (0x10009) topic_name is not set, or topic_name_length is zero.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-348">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-348">Allowed From</span></span>

<span data-ttu-id="344c7-349">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-349">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-350">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-350">Example</span></span>

```c
/* Subscribe to the topic "temperature" with QoS level 0 */
CHAR *topic = "temperature";

status = nxd_mqtt_client_unsubscribe(&my_client, topic,
    STRLEN(topic));

/* If status is NXD_MQTT_SUCCESS, the client successfully
unsubscribes the topic "temperate". */
```

## <a name="nxd_mqtt_client_receive_notify_set"></a><span data-ttu-id="344c7-351">nxd_mqtt_client_receive_notify_set</span><span class="sxs-lookup"><span data-stu-id="344c7-351">nxd_mqtt_client_receive_notify_set</span></span>

<span data-ttu-id="344c7-352">MQTT ileti alma geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="344c7-352">Set MQTT message receive notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-353">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-353">Prototype</span></span>

```c
UINT nxd_mqtt_client_receive_notify_set(NXD_MQTT_CLIENT
    *client_ptr,
    VOID(*receive_notify)(NXD_MQTT_CLIENT* client_ptr,
    UINT message_count));
```

### <a name="description"></a><span data-ttu-id="344c7-354">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-354">Description</span></span>

<span data-ttu-id="344c7-355">Bu hizmet MQTT istemcisiyle bir geri çağırma işlevi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="344c7-355">This service registers a callback function with the MQTT client.</span></span> <span data-ttu-id="344c7-356">Aracı tarafından yayınlanan bir ileti alındıktan sonra MQTT istemcisi iletiyi alma kuyruğunda depolar.</span><span class="sxs-lookup"><span data-stu-id="344c7-356">Upon receiving a message published by the broker, MQTT client stores the message in the receive queue.</span></span> <span data-ttu-id="344c7-357">Geri çağırma işlevi ayarlandıysa, uygulamaya bir iletinin alınmaya hazırlandığını bildirmek için geri çağırma işlevi çağırılır.</span><span class="sxs-lookup"><span data-stu-id="344c7-357">If the callback function is set, the callback function is invoked to notify the application that a message is ready to be retrieved.</span></span> <span data-ttu-id="344c7-358">Alma bildirme işlevi MQTT istemci denetim bloğuna bir işaretçi alır ve alma sırasındaki ileti sayısını belirten bir *message_count* .</span><span class="sxs-lookup"><span data-stu-id="344c7-358">The receive notify function takes a pointer to the MQTT client control block, and a *message_count* indicating the number of messages available in the receive queue.</span></span> <span data-ttu-id="344c7-359">Bu sayı, zaman aralığında ulaşan yeni iletiler geldiği için alma bildirimi ve uygulamanın bu iletileri aldığı zaman arasında değişebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="344c7-359">Note that the number may change between the receive notification and when the application retrieves these messages, as new messages may have arrived in the interval.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-360">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-360">Input Parameters</span></span>

- <span data-ttu-id="344c7-361">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-361">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-362">**receive_notify** Kullanıcının bir ileti alındığında çağrılması için geri arama işlevi sağlandı.</span><span class="sxs-lookup"><span data-stu-id="344c7-362">**receive_notify** User supplied callback function to be invoked on receiving a message.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-363">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-363">Return Values</span></span>

- <span data-ttu-id="344c7-364">**NXD_MQTT_SUCCESS** (0x00) alma bildirim işlevini başarıyla ayarladı.</span><span class="sxs-lookup"><span data-stu-id="344c7-364">**NXD_MQTT_SUCCESS** (0x00) Successfully set the receive notify function.</span></span>
- <span data-ttu-id="344c7-365">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu.</span><span class="sxs-lookup"><span data-stu-id="344c7-365">NX_PTR_ERROR (0x07) Invalid MQTT control block.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-366">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-366">Allowed From</span></span>

<span data-ttu-id="344c7-367">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-367">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-368">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-368">Example</span></span>

```c
/* Sample MQTT receive notify function. */

VOID my_notify_func(NXD_MQTT_CLIENT* client_ptr,
    UINT message_count)
{

/* On receiving a message, set an event flag to wake up the
application thread. The message will be received and
processed in the application thread. */
tx_event_flags_set(&mqtt_app_flag,
    MESSAGE_RECEIVED_EVENT, TX_OR);

/* All done. Return to the caller. */
    return;
}

/* Set the receive callback function. */
status = **nxd_mqtt_client_receive_notify_set**(&my_client,
    my_notify_func);

/* If status is NXD_MQTT_SUCCESS the notify function is properly set. */
```

## <a name="nxd_mqtt_client_message_get"></a><span data-ttu-id="344c7-369">nxd_mqtt_client_message_get</span><span class="sxs-lookup"><span data-stu-id="344c7-369">nxd_mqtt_client_message_get</span></span>

<span data-ttu-id="344c7-370">Aracıdan bir ileti alma</span><span class="sxs-lookup"><span data-stu-id="344c7-370">Retrieve a message from the broker</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-371">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-371">Prototype</span></span>

```c
UINT nxd_mqtt_client_message_get(NXD_MQTT_CLIENT
    *client_ptr,
    UCHAR *topic_buffer, UINT topic_buffer_size,
    UINT *actual_topic_length, UCHAR *message_buffer,
    UINT message_buffer_size, UINT *actual_message_length);
```

### <a name="description"></a><span data-ttu-id="344c7-372">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-372">Description</span></span>

<span data-ttu-id="344c7-373">Bu hizmet, aracı tarafından yayınlanan bir iletiyi alır.</span><span class="sxs-lookup"><span data-stu-id="344c7-373">This service retrieves a message published by the broker.</span></span> <span data-ttu-id="344c7-374">Gelen tüm iletiler alma sırasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="344c7-374">All incoming messages are stored in the receive queue.</span></span> <span data-ttu-id="344c7-375">Uygulama bu hizmeti bu iletileri almak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="344c7-375">The application uses this service to retrieve these messages.</span></span> <span data-ttu-id="344c7-376">Bu çağrı engellenmemiş.</span><span class="sxs-lookup"><span data-stu-id="344c7-376">This call is non-blocking.</span></span> <span data-ttu-id="344c7-377">Alma sırası boşsa, bu hizmet \***NXD_MQTT_NO_MESSAGE** _ döndürür.</span><span class="sxs-lookup"><span data-stu-id="344c7-377">If the receive queue is empty, this service returns \***NXD_MQTT_NO_MESSAGE** _.</span></span> <span data-ttu-id="344c7-378">Gelen ileti hakkında bildirim almak isteyen bir uygulama, alma geri araması işlevini kaydetmek için _ *_nxd_mqtt_client_receive_notify_set_*\* hizmetini çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-378">An application wishing to be notified of incoming message can call the service _ *_nxd_mqtt_client_receive_notify_set_*\* to register a receive callback function.</span></span>

<span data-ttu-id="344c7-379">Çağıranın, konu dizesi ve ileti gövdesi için bellek alanı sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="344c7-379">The caller needs to provide memory space for the topic string and the message body.</span></span> <span data-ttu-id="344c7-380">Bu iki arabelleğe ait boyutlar *topic_buffer_size* ve *message_buffer_size* kullanılarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-380">The sizes of these two buffers are passed in using *topic_buffer_size* and *message_buffer_size*.</span></span> <span data-ttu-id="344c7-381">Konu dizesindeki gerçek bayt sayısı ve ileti gövdesi *actual_topic_length* ve *actual_message_length* döndürülür.</span><span class="sxs-lookup"><span data-stu-id="344c7-381">The actual number of bytes in the topic string and the message body are returned in *actual_topic_length* and *actual_message_length*.</span></span> <span data-ttu-id="344c7-382">Konu uzunluğu veya maszu uzunluğu, girilen arabellek alanından büyükse, bu hizmet *NXD_MQTT_INSUFFICIENT_BUFFER_SIZE* hata kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="344c7-382">If topic length or massage length is greater than the buffer space provided, this service returns error code *NXD_MQTT_INSUFFICIENT_BUFFER_SIZE*.</span></span>

<span data-ttu-id="344c7-383">Uygulama daha büyük bir arabellek ayırır ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="344c7-383">The application shall allocate a bigger buffer and try again.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-384">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-384">Input Parameters</span></span>

- <span data-ttu-id="344c7-385">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-385">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-386">**topic_buffer** Konu dizesinin kopyalandığı bellek konumunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-386">**topic_buffer** Pointer to the memory location where the topic string is copied into.</span></span>
- <span data-ttu-id="344c7-387">**topic_buffer_size** Konu arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="344c7-387">**topic_buffer_size** Size of the topic buffer.</span></span>
- <span data-ttu-id="344c7-388">**actual_topic_length** Gerçek konu uzunluğunun döndürüldüğü bellek konumunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-388">**actual_topic_length** Pointer to the memory location where the actual topic length is returned.</span></span>
- <span data-ttu-id="344c7-389">**message_buffer** İleti dizesinin kopyalandığı bellek konumunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-389">**message_buffer** Pointer to the memory location where the message string is copied into.</span></span>
- <span data-ttu-id="344c7-390">**message_buffer_size** İleti arabelleğinin boyutu.</span><span class="sxs-lookup"><span data-stu-id="344c7-390">**message_buffer_size** Size of the message buffer.</span></span>
- <span data-ttu-id="344c7-391">**actual_message_length** İleti uzunluğunun döndürüldüğü bellek konumunun işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-391">**actual_message_length** Pointer to the memory location where the message length is returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-392">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-392">Return Values</span></span>

- <span data-ttu-id="344c7-393">**NXD_MQTT_SUCCESS** (0x00) ileti başarıyla alındı.</span><span class="sxs-lookup"><span data-stu-id="344c7-393">**NXD_MQTT_SUCCESS** (0x00) Successfully retrieved message.</span></span>
- <span data-ttu-id="344c7-394">**NXD_MQTT_INTERNAL_ERROR** (0x10004) iç mantık hatası</span><span class="sxs-lookup"><span data-stu-id="344c7-394">**NXD_MQTT_INTERNAL_ERROR** (0x10004) Internal logic error</span></span>
- <span data-ttu-id="344c7-395">**NXD_MQTT_NO_MESSAGE** (0x1000a) alma kuyruğu boştur.</span><span class="sxs-lookup"><span data-stu-id="344c7-395">**NXD_MQTT_NO_MESSAGE** (0x1000A) The receive queue is empty.</span></span>
- <span data-ttu-id="344c7-396">**NXD_MQTT_INSUFFICIENT_BUFFER_SIZE** (0x1000d) konu arabelleği veya ileti arabelleği konu başlığı veya ileti için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="344c7-396">**NXD_MQTT_INSUFFICIENT_BUFFER_SIZE** (0x1000D) Topic buffer or message buffer is too small for the topic or the message.</span></span>
- <span data-ttu-id="344c7-397">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu, ip_ptr veya paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="344c7-397">NX_PTR_ERROR (0x07) Invalid MQTT control block, ip_ptr, or packet pool pointer</span></span>
- <span data-ttu-id="344c7-398">NXD_MQTT_INVALID_PARAMETER (0x10009) message_buffer veya topic_buffer işaretçi NULL</span><span class="sxs-lookup"><span data-stu-id="344c7-398">NXD_MQTT_INVALID_PARAMETER (0x10009) message_buffer or topic_buffer pointer is NULL</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-399">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-399">Allowed From</span></span>

<span data-ttu-id="344c7-400">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-400">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-401">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-401">Example</span></span>

```c
UCHAR topic[MAX_TOPIC_SIZE];
UCHAR message[MAX_TOPIC_SIZE];
UINT topic_length;
UINT message_length;

/* Retrieve a message from MQTT client receive queue. */
status = nxd_mqtt_client_message_get(&my_client, topic,
    sizeof(topic), &topic_length, message, sizeof(message),
    &message_length);

/* Check the return value. */
if(status == NXD_MQTT_SUCCESS)
{
/* A message is received. All done. */
}
else if (status == NXD_MQTT_NO_MESSAGE)
{
/* No more messages in the receive queue. All done. */
}
else
{
/* Receive error. */
}
```

## <a name="nxd_mqtt_client_disconnect_notify_set"></a><span data-ttu-id="344c7-402">nxd_mqtt_client_disconnect_notify_set</span><span class="sxs-lookup"><span data-stu-id="344c7-402">nxd_mqtt_client_disconnect_notify_set</span></span>

<span data-ttu-id="344c7-403">MQTT iletisi bağlantısını kes bildirimi geri arama işlevini ayarla</span><span class="sxs-lookup"><span data-stu-id="344c7-403">Set MQTT message disconnect notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-404">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-404">Prototype</span></span>

```c
UINT nxd_mqtt_client_disconnect_notify_set(
    NXD_MQTT_CLIENT *client_ptr,
    VOID(*disconnect_notify)(NXD_MQTT_CLIENT* client_ptr));
```

### <a name="description"></a><span data-ttu-id="344c7-405">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-405">Description</span></span>

<span data-ttu-id="344c7-406">Bu hizmet MQTT istemcisiyle bir geri çağırma işlevi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="344c7-406">This service registers a callback function with the MQTT client.</span></span> <span data-ttu-id="344c7-407">MQTT, aracı bağlantısını algıladığında, uygulamayı uyarmak için bu bildirim işlevini çağırır.</span><span class="sxs-lookup"><span data-stu-id="344c7-407">When MQTT detects the connection to the broker is lost, it calls this notify function to alert the application.</span></span> <span data-ttu-id="344c7-408">Bu nedenle uygulama, kayıp bir bağlantıyı algılamak ve aracıya yeniden bağlantı kurmak için bu geri çağırma işlevini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-408">Therefore, the application can use this callback function to detect a lost connection, and to be able to re-establish connection to the broker.</span></span>

```c
VOID callback_func(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="input-parameters"></a><span data-ttu-id="344c7-409">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-409">Input Parameters</span></span>

- <span data-ttu-id="344c7-410">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-410">**client_ptr** Pointer to MQTT Client control block.</span></span>
- <span data-ttu-id="344c7-411">**disconnect_notify** MQTT, aracı bağlantısını algıladığında, çağrılacak Kullanıcı tarafından sağlanan geri arama işlevi kaybolur.</span><span class="sxs-lookup"><span data-stu-id="344c7-411">**disconnect_notify** User supplied callback function to be invoked when MQTT detects the connection to the broker is lost.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-412">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-412">Return Values</span></span>

- <span data-ttu-id="344c7-413">**NXD_MQTT_SUCCESS** (0x00), bağlantı kesme bildirimi işlevini başarıyla ayarladı.</span><span class="sxs-lookup"><span data-stu-id="344c7-413">**NXD_MQTT_SUCCESS** (0x00) Successfully set the disconnect notify function.</span></span>
- <span data-ttu-id="344c7-414">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu.</span><span class="sxs-lookup"><span data-stu-id="344c7-414">NX_PTR_ERROR (0x07) Invalid MQTT control block.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-415">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-415">Allowed From</span></span>

<span data-ttu-id="344c7-416">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-416">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-417">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-417">Example</span></span>

```c
VOID disconnect_notify(NXD_MQTT_CLIENT *client_ptr)
{
/* MQTT client is disconnected from the broker. Notify the application so it can re-connect to the broker. */
}

status = nxd_mqtt_client_disconnect_notify_set(client_ptr,
    disconnect_notify);
```

## <a name="nxd_mqtt_client_disconnect"></a><span data-ttu-id="344c7-418">nxd_mqtt_client_disconnect</span><span class="sxs-lookup"><span data-stu-id="344c7-418">nxd_mqtt_client_disconnect</span></span>

<span data-ttu-id="344c7-419">MQTT istemcisinin aracıdan bağlantısını kesme</span><span class="sxs-lookup"><span data-stu-id="344c7-419">Disconnect MQTT client from the broker</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-420">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-420">Prototype</span></span>

```c
UINT nxd_mqtt_client_disconnect(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="344c7-421">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-421">Description</span></span>

<span data-ttu-id="344c7-422">Bu hizmet, istemcinin aracısından bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="344c7-422">This service disconnects the client from the broker.</span></span> <span data-ttu-id="344c7-423">Alma sırasındaki iletilerin serbest bırakıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="344c7-423">Note that messages on the receive queue are released.</span></span> <span data-ttu-id="344c7-424">İletme sırasındaki QoS 1 olan iletiler serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="344c7-424">Messages with QoS 1 in the transmit queue are not released.</span></span> <span data-ttu-id="344c7-425">İstemci sunucuya yeniden bağlandıktan sonra, istemci sunucuya yeniden bağlanmadığı müddetçe, *clean_session* bayrağı ***NX_TRUE*** olarak ayarlanan QoS 1 iletileri işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="344c7-425">After the client reconnects to the server, QoS 1 messages can be processed, unless the client reconnects to the server with *clean_session* flag set to ***NX_TRUE***.</span></span>

<span data-ttu-id="344c7-426">Bağlantı TLS güvenlik koruması ile yapılmışsa, bu hizmet TCP bağlantısının bağlantısını kesmeden önce TLS oturumunu kapatır.</span><span class="sxs-lookup"><span data-stu-id="344c7-426">If the connection was made with TLS security protection, this service will close the TLS session before disconnecting the TCP connection.</span></span>

<span data-ttu-id="344c7-427">Gerçek TCP yuvası bağlantı kesilmesi çağrısının NXD_MQTT_SOCKET_TIMEOUT (süreölçer işaretleri) tarafından tanımlanan bir bekleme seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="344c7-427">The actual TCP socket disconnect call has a wait option defined by NXD_MQTT_SOCKET_TIMEOUT (timer ticks).</span></span> <span data-ttu-id="344c7-428">Varsayılan değer NX_WAIT_FOREVER.</span><span class="sxs-lookup"><span data-stu-id="344c7-428">The default value is NX_WAIT_FOREVER.</span></span> <span data-ttu-id="344c7-429">Ağ bağlantısının kaybolması veya sunucunun yanıt vermemesi durumunda sınırsız askıya alma önlemek için bu seçeneği sınırlı bir değere ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="344c7-429">To avoid indefinite suspension in the event that the network connection is lost or the server is not responding, set this option to a finite value.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-430">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-430">Input Parameters</span></span>

- <span data-ttu-id="344c7-431">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-431">**client_ptr** Pointer to MQTT Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-432">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-432">Return Values</span></span>

- <span data-ttu-id="344c7-433">**NXD_MQTT_SUCCESS** (0x00) aracısının bağlantısı başarıyla kesildi</span><span class="sxs-lookup"><span data-stu-id="344c7-433">**NXD_MQTT_SUCCESS** (0x00) Successfully disconnected from broker</span></span>
- <span data-ttu-id="344c7-434">**NXD_MQTT_MUTEX_FAILURE** (0x10003) MQTT MUTEX 'i alamadı.</span><span class="sxs-lookup"><span data-stu-id="344c7-434">**NXD_MQTT_MUTEX_FAILURE** (0x10003) Failed to obtain MQTT mutex.</span></span>
- <span data-ttu-id="344c7-435">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu</span><span class="sxs-lookup"><span data-stu-id="344c7-435">NX_PTR_ERROR (0x07) Invalid MQTT control block</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-436">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-436">Allowed From</span></span>

<span data-ttu-id="344c7-437">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-437">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-438">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-438">Example</span></span>

```c
/* Disconnect from the broker. */
status = nxd_mqtt_client_disconnect(&my_client);

/* If status is NXD_MQTT_SUCCESS the client is successfully
disconnected from the broker. */
```

## <a name="nxd_mqtt_client_delete"></a><span data-ttu-id="344c7-439">nxd_mqtt_client_delete</span><span class="sxs-lookup"><span data-stu-id="344c7-439">nxd_mqtt_client_delete</span></span>

<span data-ttu-id="344c7-440">MQTT istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="344c7-440">Delete the MQTT client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="344c7-441">Prototype</span><span class="sxs-lookup"><span data-stu-id="344c7-441">Prototype</span></span>

```c
UINT nxd_mqtt_client_delete(NXD_MQTT_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="344c7-442">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c7-442">Description</span></span>

<span data-ttu-id="344c7-443">Bu hizmet MQTT istemci örneğini siler ve iç kaynakları yayınlar.</span><span class="sxs-lookup"><span data-stu-id="344c7-443">This service deletes the MQTT client instance and releases internal resources.</span></span> <span data-ttu-id="344c7-444">Bu hizmet hala bağlıysa, istemcinin aracısının bağlantısını otomatik olarak keser.</span><span class="sxs-lookup"><span data-stu-id="344c7-444">This service automatically disconnects the client from the broker if it is still connected.</span></span> <span data-ttu-id="344c7-445">Henüz iletilmemiş veya onaylanmamış iletiler serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="344c7-445">Messages not yet transmitted or not been acknowledged are released.</span></span> <span data-ttu-id="344c7-446">Alınan ancak uygulama tarafından alınmayan iletiler de serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="344c7-446">Messages received but not retrieved by the application are also released.</span></span>

<span data-ttu-id="344c7-447">Bağlantı TLS güvenlik koruması ile yapılmışsa, bu hizmet TCP bağlantısının bağlantısını kesmeden önce TLS oturumunu kapatır.</span><span class="sxs-lookup"><span data-stu-id="344c7-447">If the connection was made with TLS security protection, this service closes the TLS session before disconnecting the TCP connection.</span></span>

<span data-ttu-id="344c7-448">İstemci silindikten sonra MQTT hizmetini kullanmak isteyen bir uygulamanın yeni bir örnek oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="344c7-448">After the client is deleted, an application wishing to use MQTT service needs to create a new instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="344c7-449">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c7-449">Input Parameters</span></span>

- <span data-ttu-id="344c7-450">**client_ptr** MQTT Istemci denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="344c7-450">**client_ptr** Pointer to MQTT Client control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="344c7-451">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="344c7-451">Return Values</span></span>

- <span data-ttu-id="344c7-452">**NXD_MQTT_SUCCESS** (0x00) MQTT istemcisini başarıyla sildi.</span><span class="sxs-lookup"><span data-stu-id="344c7-452">**NXD_MQTT_SUCCESS** (0x00) Successfully deleted MQTT client.</span></span>
- <span data-ttu-id="344c7-453">NX_PTR_ERROR (0x07) geçersiz MQTT denetim bloğu</span><span class="sxs-lookup"><span data-stu-id="344c7-453">NX_PTR_ERROR (0x07) Invalid MQTT control block</span></span>

### <a name="allowed-from"></a><span data-ttu-id="344c7-454">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="344c7-454">Allowed From</span></span>

<span data-ttu-id="344c7-455">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="344c7-455">Threads</span></span>

### <a name="example"></a><span data-ttu-id="344c7-456">Örnek</span><span class="sxs-lookup"><span data-stu-id="344c7-456">Example</span></span>

```c
/* Delete the MQTT client instance. */
status = nxd_mqtt_client_delete(&my_client);

/* If status is NXD_MQTT_SUCCESS the client is successfully
deleted from the system. */
```
