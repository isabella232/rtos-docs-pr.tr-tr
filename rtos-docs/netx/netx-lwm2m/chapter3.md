---
title: Bölüm 3-Azure RTOS NetX LWM2M 'ın Işlevsel açıklaması
description: Bu bölümde, Azure RTOS NetX LWM2M 'in işlevsel bir açıklaması bulunmaktadır.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f49a4f5f4c899dfa461a9d57a8b56e4503d6acd4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826680"
---
# <a name="chapter-3---functional-description-of-azure-rtos-netx-lwm2m"></a><span data-ttu-id="d0ad1-103">Bölüm 3-Azure RTOS NetX LWM2M 'ın Işlevsel açıklaması</span><span class="sxs-lookup"><span data-stu-id="d0ad1-103">Chapter 3 - Functional description of Azure RTOS NetX LWM2M</span></span>

<span data-ttu-id="d0ad1-104">Bu bölümde, Azure RTOS NetX LWM2M 'in işlevsel bir açıklaması bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-104">This chapter contains a functional description of Azure RTOS NetX LWM2M.</span></span>

## <a name="lwm2m-client-initialization"></a><span data-ttu-id="d0ad1-105">LWM2M Istemci başlatması</span><span class="sxs-lookup"><span data-stu-id="d0ad1-105">LWM2M Client Initialization</span></span>

<span data-ttu-id="d0ad1-106">LWM2M Istemcisi ***nx_lwm2m_client_create*** hizmeti çağırarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-106">The LWM2M Client is initialized by calling ***nx_lwm2m_client_create*** service.</span></span> <span data-ttu-id="d0ad1-107">LWM2M Istemcisi kendi iş parçacığında çalışır ve geri çağırmalar kullanılarak veya uygulama tarafından uygulanan özel nesnelerin yöntemlerini çağırarak uygulamaya bazı olayları bildirebilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-107">The LWM2M Client runs in its own thread and can report some events to the application through the use of callbacks, or by calling methods of the custom objects implemented by the application.</span></span>

<span data-ttu-id="d0ad1-108">Ayrıca, bir veya daha fazla sunucuyla iletişimi etkinleştirmek için ***nx_lwm2m_client_session_create*** çağırarak LWM2M istemci oturumlarının oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-108">In addition, LWM2M Client Sessions must be created by calling ***nx_lwm2m_client_session_create*** for enabling communication with one or more servers.</span></span> <span data-ttu-id="d0ad1-109">Bir oturum iki farklı sunucu türüyle iletişim kurabilir: bir önyükleme sunucusu veya LWM2M sunucusu (cihaz yönetimi).</span><span class="sxs-lookup"><span data-stu-id="d0ad1-109">A session can communicate with two different types of servers: a Bootstrap Server or a LWM2M Server (Device Management).</span></span>

### <a name="bootstrap-server-session"></a><span data-ttu-id="d0ad1-110">Önyükleme sunucusu oturumu</span><span class="sxs-lookup"><span data-stu-id="d0ad1-110">Bootstrap Server Session</span></span>

<span data-ttu-id="d0ad1-111">LWM2M Istemcisinin, bir veya daha fazla LWM2M sunucusuyla "Register" işlemini gerçekleştirmesini sağlamak için, LWM2M Istemcisine bir iletişim oturumu, bir önyükleme sunucusu ile ilgili bilgi sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-111">A communication session with a Bootstrap Server is used to provision essential information into the LWM2M Client to enable the LWM2M Client to perform the operation "Register" with one or more LWM2M Servers.</span></span> <span data-ttu-id="d0ad1-112">Istemci tarafından başlatılan ve sunucu tarafından başlatılan önyükleme modlarında bu tür bir sunucu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-112">This type of server is used during the Client Initiated and Server Initiated Bootstrap modes.</span></span>

<span data-ttu-id="d0ad1-113">Uygulama, ***nx_lwm2m_client_session_bootstrap** _ veya _*_Nx_lwm2m_client_session_bootstrap_dtls_\*_ çağırarak bir önyükleme oturumu başlatabilir, sunucunun IP adresini ve bağlantı noktası numarasını ve Isteğe bağlı BIR güvenlik nesnesi örnek kimliğini sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-113">The application can start a Bootstrap session by calling ***nx_lwm2m_client_session_bootstrap** _ or _*_nx_lwm2m_client_session_bootstrap_dtls_\*_, it must provide the IP address and port number of the server, and an optional Security Object Instance ID.</span></span> <span data-ttu-id="d0ad1-114">_*_Nx_lwm2m_client_session_bootstrap_*_ işlevi güvenli olmayan iletişim kullanır, ancak _ *_nx_lwm2m_client_session_bootstrap_dtls_*\* sunucuyla güvenli bir DTLS bağlantısı kurar.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-114">The _*_nx_lwm2m_client_session_bootstrap_*_ function uses insecure communication, whereas _ *_nx_lwm2m_client_session_bootstrap_dtls_*\* establishes a secure DTLS connection with the server.</span></span>

<span data-ttu-id="d0ad1-115">Önyükleme işlemi başarılı olursa, önyükleme sunucusu, önyükleme ve LWM2M sunucuları için güvenlik nesne örnekleri ve LWM2M sunucuları için sunucu nesne örnekleri oluşturmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-115">If the Bootstrap operation is successful, the Bootstrap server should have created Security Object Instance(s) for the Bootstrap and LWM2M Servers, and Server Object Instance(s) for the LWM2M Servers.</span></span> <span data-ttu-id="d0ad1-116">Uygulamanın, LWM2M sunucuları ile oturum oluşturmak için bu bilgileri kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-116">The application must use this information for establishing a session with the LWM2M Server(s).</span></span>

<span data-ttu-id="d0ad1-117">Önyükleme verileri, cihazın bir sonraki yeniden başlatmada LWM2M Istemcisini yapılandırmak için uygulama tarafından geçici olmayan belleğe kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-117">The Bootstrap data should be saved to non-volatile memory by the application in order to configure the LWM2M Client at the next reboot of the device.</span></span>

### <a name="lwm2m-server-session"></a><span data-ttu-id="d0ad1-118">LWM2M sunucusu oturumu</span><span class="sxs-lookup"><span data-stu-id="d0ad1-118">LWM2M Server Session</span></span>

<span data-ttu-id="d0ad1-119">Kayıt, cihaz yönetimi ve hizmet etkinleştirme için bir LWM2M sunucusuyla iletişim oturumu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-119">A communication session with a LWM2M Server is used for Registration, Device Management and Service Enablement.</span></span>

<span data-ttu-id="d0ad1-120">Uygulama, LWM2M Istemcisini ***nx_lwm2m_client_session_register** _ veya _*_nx_lwm2m_client_session_register_dtls_\*_ çağırarak sunucuya kaydedebilir, sunucunun IP adresini ve bağlantı noktası numarasını ve var olan bir sunucu nesnesi örneğine KARŞıLıK gelen kısa sunucu kimliğini sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-120">The application can register the LWM2M Client to a server by calling ***nx_lwm2m_client_session_register** _ or _*_nx_lwm2m_client_session_register_dtls_\*_, it must provide the IP address and port number of the server, and the Short Server ID which corresponds to an existing Server Object Instance.</span></span> <span data-ttu-id="d0ad1-121">_*_Nx_lwm2m_client_session_register_*_ işlevi güvenli olmayan iletişim kullanır, ancak _ *_nx_lwm2m_client_session_register_dtls_*\* sunucuyla güvenli bir DTLS bağlantısı kurar.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-121">The _*_nx_lwm2m_client_session_register_*_ function uses insecure communication, whereas _ *_nx_lwm2m_client_session_register_dtls_*\* establishes a secure DTLS connection with the server.</span></span>

<span data-ttu-id="d0ad1-122">Uygulama, \***nx_lwm2m_client_session_deregister** _ ' i çağırarak LWM2M istemcisini kaydedebilir ve istemciden _ *_nx_lwm2m_client_session_update_* \* çağırarak bir ' güncelleştirme ' iletisi göndermesini ister.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-122">The application can de-register the LWM2M Client by calling ***nx_lwm2m_client_session_deregister** _, and ask the client to send an 'Update' message by calling _*_nx_lwm2m_client_session_update_\*\*.</span></span>

### <a name="session-state-callback"></a><span data-ttu-id="d0ad1-123">Oturum durumu geri çağırma</span><span class="sxs-lookup"><span data-stu-id="d0ad1-123">Session State Callback</span></span>

<span data-ttu-id="d0ad1-124">Uygulama, oturum durumu güncellendiğinde çağrılan bir oturum oluşturma sırasında bir geri çağırma kaydeder, geri çağırma işlevi NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK aşağıdaki prototiple sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-124">The application registers a callback at creation of a session which is called when the state of the session is updated, the callback function NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK has the following prototype:</span></span>

```c
typedef VOID (*NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK)
        (NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state);
```

<span data-ttu-id="d0ad1-125">Aşağıdaki durumlar tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-125">The following states are defined :</span></span>

- <span data-ttu-id="d0ad1-126">**NX_LWM2M_CLIENT_SESSION_INIT**: oturum oluşturulduktan sonra ilk durum.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-126">**NX_LWM2M_CLIENT_SESSION_INIT**: The initial state after session creation.</span></span>

- <span data-ttu-id="d0ad1-127">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING**: istemci, ' bekletme ' süreölçeri veya sunucu tarafından başlatılan önyükleme işleminin sona erme süresini bekliyor.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-127">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING**: The client is waiting for the expiration of the 'Hold Off' timer or Server Initiated Bootstrap.</span></span>

- <span data-ttu-id="d0ad1-128">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**: Istemci önyükleme sunucusuna bir ' istek ' iletisi gönderdi (Istemci tarafından başlatılan önyükleme).</span><span class="sxs-lookup"><span data-stu-id="d0ad1-128">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**: The client has sent a 'Request' message to the Bootstrap Server (Client Initiated Bootstrap).</span></span>

- <span data-ttu-id="d0ad1-129">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**: Istemci, önyükleme sunucusundan veri alıyor.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-129">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**: The client is receiving data from the Bootstrap Server.</span></span>

- <span data-ttu-id="d0ad1-130">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED**: önyükleme sunucusu ' FINISHED ' iletisi gönderdi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-130">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED**: The Bootstrap Server has sent a 'Finished' message.</span></span>

- <span data-ttu-id="d0ad1-131">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR**: önyükleme oturumu başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-131">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR**: The bootstrap session has failed.</span></span>

- <span data-ttu-id="d0ad1-132">**NX_LWM2M_CLIENT_SESSION_REGISTERING**: ISTEMCI, LWM2M sunucusuna bir ' Register ' iletisi gönderdi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-132">**NX_LWM2M_CLIENT_SESSION_REGISTERING**: The client has sent a 'Register' message to the LWM2M Server.</span></span>

- <span data-ttu-id="d0ad1-133">**NX_LWM2M_CLIENT_SESSION_REGISTERED**: Istemci LWM2M sunucusuna kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-133">**NX_LWM2M_CLIENT_SESSION_REGISTERED**: The client is registered to the LWM2M Server.</span></span>

- <span data-ttu-id="d0ad1-134">**NX_LWM2M_CLIENT_SESSION_UPDATING**: ISTEMCI, LWM2M sunucusuna bir ' Update ' iletisi gönderdi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-134">**NX_LWM2M_CLIENT_SESSION_UPDATING**: The client has sent an 'Update' message to the LWM2M Server.</span></span>

- <span data-ttu-id="d0ad1-135">**NX_LWM2M_CLIENT_SESSION_DEREGISTERING**: ISTEMCI, LWM2M sunucusuna ' de Register ' iletisi gönderdi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-135">**NX_LWM2M_CLIENT_SESSION_DEREGISTERING**: The client has sent an 'De-register' message to the LWM2M Server.</span></span>

- <span data-ttu-id="d0ad1-136">**NX_LWM2M_CLIENT_SESSION_DEREGISTERED**: ISTEMCI, LWM2M sunucusundan de kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-136">**NX_LWM2M_CLIENT_SESSION_DEREGISTERED**: The client is de-registered from the LWM2M Server.</span></span>

- <span data-ttu-id="d0ad1-137">**NX_LWM2M_CLIENT_SESSION_DISABLED**: LWM2M sunucusu devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-137">**NX_LWM2M_CLIENT_SESSION_DISABLED**: The LWM2M Server is disabled.</span></span> <span data-ttu-id="d0ad1-138">Devre dışı bırakma süreölçeri sona erdikten sonra bir ' Register ' gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-138">A 'Register' will be sent after the expiration of the disable timer.</span></span>

- <span data-ttu-id="d0ad1-139">**NX_LWM2M_CLIENT_SESSION_ERROR**: LWM2M sunucusuna kaydolma veya güncelleştirme işlemi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-139">**NX_LWM2M_CLIENT_SESSION_ERROR**: The registration or update operation to the LWM2M Server has failed.</span></span>

- <span data-ttu-id="d0ad1-140">**NX_LWM2M_CLIENT_SESSION_DELETED**: LWM2M sunucusuna karşılık gelen sunucu nesnesi örneği silindi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-140">**NX_LWM2M_CLIENT_SESSION_DELETED**: The Server Object Instance corresponding to the LWM2M Server has been deleted.</span></span> <span data-ttu-id="d0ad1-141">Hata durumunda uygulamanın, **_nx_lwm2m_client_session_error_get_** çağırarak hatanın nedenini elde edebilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-141">In case of error the application can retrieve the cause of the error by calling **_nx_lwm2m_client_session_error_get_**.</span></span>

## <a name="local-device-management"></a><span data-ttu-id="d0ad1-142">Yerel cihaz yönetimi</span><span class="sxs-lookup"><span data-stu-id="d0ad1-142">Local Device Management</span></span>

<span data-ttu-id="d0ad1-143">Uygulama, yerel cihaz yönetimi işlevlerini kullanarak LWM2M Istemcisinin nesnelerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-143">The application can access the Objects of the LWM2M Client by using the local device management functions.</span></span> <span data-ttu-id="d0ad1-144">Aşağıdaki işlevler verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-144">The following functions are provided:</span></span>

- <span data-ttu-id="d0ad1-145">***nx_lwm2m_client_object_read***: bir nesne örneğinden kaynakları okuyun.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-145">***nx_lwm2m_client_object_read***: Read resources from an Object Instance.</span></span>

- <span data-ttu-id="d0ad1-146">***nx_lwm2m_client_object_discover***: bir nesne örneğinin kaynak listesini alın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-146">***nx_lwm2m_client_object_discover***: Get the list of the resources of an Object Instance.</span></span>

- <span data-ttu-id="d0ad1-147">***nx_lwm2m_client_object_write***: kaynakları bir nesne örneğine yazma</span><span class="sxs-lookup"><span data-stu-id="d0ad1-147">***nx_lwm2m_client_object_write***: Write resources to an Object Instance</span></span>

- <span data-ttu-id="d0ad1-148">***nx_lwm2m_client_object_execute***: bir nesne örneğinin kaynağında yürütme işlemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-148">***nx_lwm2m_client_object_execute***: Perform the Execute operation on a resource of an Object Instance.</span></span>

- <span data-ttu-id="d0ad1-149">***nx_lwm2m_client_object_create***: yeni bir nesne örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-149">***nx_lwm2m_client_object_create***: Create a new Object Instance.</span></span>

- <span data-ttu-id="d0ad1-150">***nx_lwm2m_client_object_delete***: varolan bir nesne örneğini silin.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-150">***nx_lwm2m_client_object_delete***: Delete an existing Object Instance.</span></span>

- <span data-ttu-id="d0ad1-151">***nx_lwm2m_client_object_get_next***: lwm2m istemcisi tarafından uygulanan sonrakı nesne kimliğini alın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-151">***nx_lwm2m_client_object_get_next***: Get the next Object ID implemented by the LWM2M Client.</span></span>

- <span data-ttu-id="d0ad1-152">***nx_lwm2m_client_object_instance_get_next***: bir nesnenin sonraki örneğini al.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-152">***nx_lwm2m_client_object_instance_get_next***: Get the next Instance of an Object.</span></span>

## <a name="resource-information"></a><span data-ttu-id="d0ad1-153">Kaynak bilgileri</span><span class="sxs-lookup"><span data-stu-id="d0ad1-153">Resource Information</span></span>

<span data-ttu-id="d0ad1-154">Nesneleri okuma ve nesnelere yazma sırasında bir kaynak NX_LWM2M_RESOURCE yapısıyla temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-154">When reading from and writing to Objects a Resource is represented by the NX_LWM2M_RESOURCE structure.</span></span> <span data-ttu-id="d0ad1-155">Bu yapı, kaynak/örnek KIMLIĞINI ve değerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-155">This structure contains the ID of the Resource/Instance and its value.</span></span> <span data-ttu-id="d0ad1-156">Değerin kodlaması türüne ve kaynağına (uygulama veya ağ) bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-156">The encoding of the value depends on its type and its origin (application or network).</span></span>

<span data-ttu-id="d0ad1-157">NX_LWM2M_RESOURCE yapısı aşağıdaki tanıma sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-157">The NX_LWM2M_RESOURCE structure has the following definition:</span></span>

```c
typedef struct NX_LWM2M_RESOURCE_STRUCT
{
    NX_LWM2M_ID     nx_lwm2m_resource_id;
    UCHAR           nx_lwm2m_resource_type;
    union
    {
        struct
        {
            const VOID *     nx_lwm2m_resource_buffer_ptr;
            UINT             nx_lwm2m_resource_buffer_length;
        } nx_lwm2m_resource_bufferdata;
        const CHAR *         nx_lwm2m_resource_stringdata;
        NX_LWM2M_INT32       nx_lwm2m_resource_integer32data;
        NX_LWM2M_INT64       nx_lwm2m_resource_integer64data;
        NX_LWM2M_FLOAT32     nx_lwm2m_resource_float32data;
        NX_LWM2M_FLOAT64     nx_lwm2m_resource_float64data;
        NX_LWM2M_BOOL        nx_lwm2m_resource_booleandata;
        NX_LWM2M_OBJLNK      nx_lwm2m_resource_objlnkdata;
        
        struct
        {
            const VOID *     nx_lwm2m_resource_multiple_ptr;
            UINT             nx_lwm2m_resource_multiple_dim;
        } nx_lwm2m_resource_multipledata;
    } nx_lwm2m_resource_value;
} NX_LWM2M_RESOURCE;
```

- <span data-ttu-id="d0ad1-158">**nx_lwm2m_resource_id**: kaynağın veya örneğin kimliği.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-158">**nx_lwm2m_resource_id**: The ID of the Resource or the Instance.</span></span>
- <span data-ttu-id="d0ad1-159">**nx_lwm2m_resource_type**: değerin türü, aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-159">**nx_lwm2m_resource_type**: The type of the value, see below.</span></span>
- <span data-ttu-id="d0ad1-160">**nx_lwm2m_resource_value**: kaynağın değeri, değerin türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-160">**nx_lwm2m_resource_value**: The value of the Resource, depends on the type of the value.</span></span>

<span data-ttu-id="d0ad1-161">Aşağıdaki değer türleri tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-161">The following type of values are defined :</span></span>

- <span data-ttu-id="d0ad1-162">**NX_LWM2M_RESOURCE_NONE**: boş kaynak.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-162">**NX_LWM2M_RESOURCE_NONE**: Empty resource.</span></span>

- <span data-ttu-id="d0ad1-163">**NX_LWM2M_RESOURCE_STRING**: *nx_lwm2m_resource_stringdata* içinde depolanan, null ile sonlandırılmış bir UTF-8 dize değeri.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-163">**NX_LWM2M_RESOURCE_STRING**: A null-terminated UTF-8 string value stored in *nx_lwm2m_resource_stringdata*.</span></span>

- <span data-ttu-id="d0ad1-164">**NX_LWM2M_RESOURCE_INTEGER32**: *Nx_lwm2m_resource_integer32data* depolanan 32 bitlik bir tamsayı değeri.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-164">**NX_LWM2M_RESOURCE_INTEGER32**: A 32-Bit Integer value stored in *nx_lwm2m_resource_integer32data*.</span></span>

- <span data-ttu-id="d0ad1-165">**NX_LWM2M_RESOURCE_INTEGER64**: *Nx_lwm2m_resource_integer64data* depolanan 64 bitlik bir tamsayı değeri.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-165">**NX_LWM2M_RESOURCE_INTEGER64**: A 64-Bit Integer value stored in *nx_lwm2m_resource_integer64data*.</span></span>

- <span data-ttu-id="d0ad1-166">**NX_LWM2M_RESOURCE_FLOAT32**: *Nx_lwm2m_resource_float32data* depolanan 32 bitlik kayan nokta değeri.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-166">**NX_LWM2M_RESOURCE_FLOAT32**: A 32-Bit Floating Point value stored in *nx_lwm2m_resource_float32data*.</span></span>

- <span data-ttu-id="d0ad1-167">**NX_LWM2M_RESOURCE_FLOAT64**: *Nx_lwm2m_resource_float64data* depolanan 64 bitlik kayan nokta değeri.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-167">**NX_LWM2M_RESOURCE_FLOAT64**: A 64-Bit Floating Point value stored in *nx_lwm2m_resource_float64data*.</span></span>

- <span data-ttu-id="d0ad1-168">**NX_LWM2M_RESOURCE_BOOLEAN**: *Nx_lwm2m_resource_booleandata* depolanan bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-168">**NX_LWM2M_RESOURCE_BOOLEAN**: A Boolean value stored in *nx_lwm2m_resource_booleandata*.</span></span>

- <span data-ttu-id="d0ad1-169">**NX_LWM2M_RESOURCE_OPAQUE**: *Nx_lwm2m_resource_bufferdata* tarafından tanımlanan donuk bir değer.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-169">**NX_LWM2M_RESOURCE_OPAQUE**: An Opaque value defined by *nx_lwm2m_resource_bufferdata*.</span></span>

- <span data-ttu-id="d0ad1-170">**NX_LWM2M_RESOURCE_OBJLNK**: *Nx_lwm2m_resource_objlnkdata* depolanan bir nesne bağlantı değeri.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-170">**NX_LWM2M_RESOURCE_OBJLNK**: An Object Link value stored in *nx_lwm2m_resource_objlnkdata*.</span></span>

- <span data-ttu-id="d0ad1-171">**NX_LWM2M_RESOURCE_TLV**: *nx_lwm2m_resource_bufferdata* tarafından tanımlanan bir TLV şifreli değeri.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-171">**NX_LWM2M_RESOURCE_TLV**: A TLV encoded value defined by *nx_lwm2m_resource_bufferdata*.</span></span>

- <span data-ttu-id="d0ad1-172">**NX_LWM2M_RESOURCE_TEXT**: *nx_lwm2m_resource_bufferdata* tarafından tanımlanan Plain-Text kodlanmış bir değer.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-172">**NX_LWM2M_RESOURCE_TEXT**: A Plain-Text encoded value defined by *nx_lwm2m_resource_bufferdata*.</span></span>

- <span data-ttu-id="d0ad1-173">**NX_LWM2M_RESOURCE_MULTIPLE**: *Nx_lwm2m_resource_multipledata* tarafından tanımlanan birden çok kaynak.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-173">**NX_LWM2M_RESOURCE_MULTIPLE**: A Multiple Resource defined by *nx_lwm2m_resource_multipledata*.</span></span> <span data-ttu-id="d0ad1-174">*nx_lwm2m_resource_multiple_ptr* , her kaynak örneği hakkında bilgi içeren bir **NX_LWM2M_RESOURCE** yapıları dizisinin bir işaretçisidir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-174">*nx_lwm2m_resource_multiple_ptr* is a pointer to an array of **NX_LWM2M_RESOURCE** structures containing information about each Resource Instances.</span></span>

- <span data-ttu-id="d0ad1-175">**NX_LWM2M_RESOURCE_MULTIPLE_TLV**: *Nx_lwm2m_resource_multipledata* tarafından tanımlanan birden çok kaynak.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-175">**NX_LWM2M_RESOURCE_MULTIPLE_TLV**: A Multiple Resource defined by *nx_lwm2m_resource_multipledata*.</span></span> <span data-ttu-id="d0ad1-176">*nx_lwm2m_resource_multiple_ptr* , TLV kodlamalı arabelleğin bir işaretçisidir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-176">*nx_lwm2m_resource_multiple_ptr* is a pointer to a TLV encoded buffer.</span></span>

<span data-ttu-id="d0ad1-177">Değer almak ve türünü denetlemek için kullanışlı işlevler, NX_LWM2M_RESOURCE yapısından bir değer alırken uygulama asla *nx_lwm2m_resource_value* alana doğrudan erişmemelidir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-177">Convenience functions are provided for retrieving the value and checking its type, the application should never directly access the *nx_lwm2m_resource_value* field when getting a value from a NX_LWM2M_RESOURCE structure.</span></span> <span data-ttu-id="d0ad1-178">Aşağıdaki işlevler tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-178">The following functions are defined :</span></span>

- <span data-ttu-id="d0ad1-179">***nx_lwm2m_resource_get_***: verilen türe sahip bir değer alın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-179">***nx_lwm2m_resource_get_***: Get a value with the given type.</span></span>
- <span data-ttu-id="d0ad1-180">***nx_lwm2m_resource_multiple_get_***: birden fazla kaynaktan verilen türe sahip bir değer alın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-180">***nx_lwm2m_resource_multiple_get_***: Get a value with the given type from a Multiple Resource.</span></span>

<span data-ttu-id="d0ad1-181">Makro **NX_LWM2M_RESOURCE_IS_MULTIPLE**(tür), bir kaynak türünün birden çok kaynak olup olmadığını denetlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-181">The macro **NX_LWM2M_RESOURCE_IS_MULTIPLE**(type) can be used to check if a resource type is a Multiple Resource.</span></span>

## <a name="object-implementation"></a><span data-ttu-id="d0ad1-182">Nesne uygulama</span><span class="sxs-lookup"><span data-stu-id="d0ad1-182">Object Implementation</span></span>

<span data-ttu-id="d0ad1-183">LWM2M Istemcisi zorunlu OMA LWM2M nesnelerini uygular: güvenlik (0), sunucu (1), Access Control (2) ve cihaz (3).</span><span class="sxs-lookup"><span data-stu-id="d0ad1-183">The LWM2M Client implements the mandatory OMA LWM2M Objects: Security (0), Server (1), Access Control (2) and Device (3).</span></span> <span data-ttu-id="d0ad1-184">Diğer cihaza özgü nesnelerin uygulama tarafından uygulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-184">Other device specific objects must be implemented by the application.</span></span>

<span data-ttu-id="d0ad1-185">Bir nesneyi tanımlamak için iki veri yapısı kullanılır: NX_LWM2M_OBJECT yapısı, nesne KIMLIĞI ve nesne yöntemleri de dahil olmak üzere nesne uygulamasını tanımlar ve NX_LWM2M_OBJECT_INSTANCE yapısı bir nesne örneğinin verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-185">Two data structures are used to define an Object: the NX_LWM2M_OBJECT structure defines the Object implementation, including the Object ID and the object methods, and the NX_LWM2M_OBJECT_INSTANCE structure contains the data of an Object Instance.</span></span>

<span data-ttu-id="d0ad1-186">NX_LWM2M_OBJECT yapısı aşağıdaki tanıma sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-186">The NX_LWM2M_OBJECT structure has the following definition:</span></span>

```c
typedef struct NX_LWM2M_OBJECT_STRUCT
{
    NX_LWM2M_OBJECT * nx_lwm2m_object_next;
    NX_LWM2M_ID nx_lwm2m_object_id;
    UINT (*nx_lwm2m_object_read)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
        NX_LWM2M_RESOURCE *values);
    UINT (*nx_lwm2m_object_discover)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT *num_resources,
        NX_LWM2M_RESOURCE_INFO *resources);
    UINT (*nx_lwm2m_object_write)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values, const
        NX_LWM2M_RESOURCE *values, UINT write_op);
    UINT (*nx_lwm2m_object_execute)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
        const CHAR *args_ptr, UINT args_length);
    UINT (*nx_lwm2m_object_create)(NX_LWM2M_OBJECT * object_ptr,
        NX_LWM2M_ID instance_id, UINT num_values, const NX_LWM2M_RESOURCE
        *values, NX_LWM2M_OBJECT_INSTANCE **instance_ptr);
    UINT (*nx_lwm2m_object_delete)(NX_LWM2M_OBJECT *object_ptr,
        NX_LWM2M_OBJECT_INSTANCE *instance_ptr);
    NX_LWM2M_OBJECT_INSTANCE * nx_lwm2m_object_instances;
} NX_LWM2M_OBJECT;
```

- <span data-ttu-id="d0ad1-187">**nx_lwm2m_object_next**: listedeki bir sonraki nesne.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-187">**nx_lwm2m_object_next**: The next object in the list.</span></span>
- <span data-ttu-id="d0ad1-188">**nx_lwm2m_object_id**: nesne kimliği.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-188">**nx_lwm2m_object_id**: The Object ID.</span></span>
- <span data-ttu-id="d0ad1-189">**nx_lwm2m_object_read**: ' Read ' yöntemi, aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-189">**nx_lwm2m_object_read**: The 'Read' method, see below.</span></span>
- <span data-ttu-id="d0ad1-190">**nx_lwm2m_object_discover**: ' bul ' yöntemi aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-190">**nx_lwm2m_object_discover**: The 'Discover' method, see below.</span></span>
- <span data-ttu-id="d0ad1-191">**nx_lwm2m_object_write**: ' Write ' yöntemi, aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-191">**nx_lwm2m_object_write**: The 'Write' method, see below.</span></span>
- <span data-ttu-id="d0ad1-192">**nx_lwm2m_object_execute**: ' Execute ' yöntemi, aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-192">**nx_lwm2m_object_execute**: The 'Execute' method, see below.</span></span>
- <span data-ttu-id="d0ad1-193">**nx_lwm2m_object_create**: ' Create ' yöntemi, aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-193">**nx_lwm2m_object_create**: The 'Create' method, see below.</span></span>
- <span data-ttu-id="d0ad1-194">**nx_lwm2m_object_delete**: ' DELETE ' yöntemi, aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-194">**nx_lwm2m_object_delete**: The 'Delete' method, see below.</span></span>
- <span data-ttu-id="d0ad1-195">**nx_lwm2m_object_instances**: nesne örneklerinin null ile sonlandırılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-195">**nx_lwm2m_object_instances**: The NULL-terminated list of object instances.</span></span>

<span data-ttu-id="d0ad1-196">NX_LWM2M_OBJECT_INSTANCE yapısı aşağıdaki tanıma sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-196">The NX_LWM2M_OBJECT_INSTANCE structure has the following definition:</span></span>

```c
typedef struct NX_LWM2M_OBJECT_INSTANCE_STRUCT
{
    NX_LWM2M_OBJECT_INSTANCE * nx_lwm2m_object_instance_next;
    NX_LWM2M_ID nx_lwm2m_object_instance_id;
} NX_LWM2M_OBJECT_INSTANCE;
```

- <span data-ttu-id="d0ad1-197">**nx_lwm2m_object_instance_next**: listedeki bir sonraki örnek.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-197">**nx_lwm2m_object_instance_next**: The next instance in the list.</span></span>
- <span data-ttu-id="d0ad1-198">**nx_lwm2m_object_instance_id**: nesne örneği kimliği.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-198">**nx_lwm2m_object_instance_id**: The Object Instance ID.</span></span>

<span data-ttu-id="d0ad1-199">Nesne, LWM2M cihaz yönetimi arabirimi tarafından tanımlanan işlemlere karşılık gelen yöntemleri uygulamalıdır: ' Read ', ' Discover ', ' Write ', ' Execute ', ' Create ' ve ' DELETE '.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-199">The Object must implement the methods corresponding to the operations defined by the LWM2M Device Management Interface: 'Read', 'Discover', 'Write', 'Execute', 'Create' and 'Delete'.</span></span> <span data-ttu-id="d0ad1-200">' Create ' ve ' DELETE ' yöntemleri, nesne örneklerin dinamik olarak oluşturulmasını desteklemiyorsa NULL olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-200">The 'Create' and 'Delete' methods can be set to NULL if the object doesn't support dynamic creation of instances.</span></span>

### <a name="the-read-method"></a><span data-ttu-id="d0ad1-201">' Read ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="d0ad1-201">The 'Read' Method</span></span>

<span data-ttu-id="d0ad1-202">' Read ' yöntemi, bir nesne örneğinden kaynak değerlerini okumak için kullanılır, işlev aşağıdaki tanıma sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-202">The 'Read' method is used to read Resource values from an Object Instance, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_read(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    NX_LWM2M_RESOURCE *values_ptr);
```

<span data-ttu-id="d0ad1-203">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-203">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="d0ad1-204">**object_ptr**: nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-204">**object_ptr**: Pointer to the Object implementation.</span></span>

- <span data-ttu-id="d0ad1-205">**instance_ptr**: nesne örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-205">**instance_ptr**: Pointer to the Object Instance.</span></span>

- <span data-ttu-id="d0ad1-206">**num_values**: okunacak kaynak sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-206">**num_values**: The number of resources to read.</span></span>

- <span data-ttu-id="d0ad1-207">**values_ptr**: okunacak kaynakların kimliklerini içeren bir NX_LWM2M_RESOURCE dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-207">**values_ptr**: Pointer to an array of NX_LWM2M_RESOURCE containing the IDs of the resources to read.</span></span> <span data-ttu-id="d0ad1-208">Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-208">On return the array is filled with the corresponding types and values.</span></span>

### <a name="the-discover-method"></a><span data-ttu-id="d0ad1-209">' Keşfet ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="d0ad1-209">The 'Discover' Method</span></span>

<span data-ttu-id="d0ad1-210">' Keşfet ' yöntemi, bir nesne tarafından uygulanan tüm kaynakların listesini almak için kullanılır, işlev aşağıdaki tanıma sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-210">The 'Discover' method is used to retrieve the list of all Resources implemented by an Object, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_discover(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT *num_resources_ptr,
    NX_LWM2M_RESOURCE_INFO *resources_ptr);
```

<span data-ttu-id="d0ad1-211">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-211">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="d0ad1-212">**object_ptr**: nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-212">**object_ptr**: Pointer to the Object implementation.</span></span>

- <span data-ttu-id="d0ad1-213">**instance_ptr**: nesne örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-213">**instance_ptr**: Pointer to the Object Instance.</span></span>

- <span data-ttu-id="d0ad1-214">**num_resources_ptr**: giriş, hedef arabelleğin boyutunun çıktıda, arabelleğe yazıldı.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-214">**num_resources_ptr**: On input the size of the destination buffer, on output the number of elements writen to the buffer.</span></span>

- <span data-ttu-id="d0ad1-215">**resources_ptr**: hedef arabelleğin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-215">**resources_ptr**: Pointer to the destination buffer.</span></span>

<span data-ttu-id="d0ad1-216">Kaynak bilgileri aşağıdaki şekilde tanımlanan bir NX_LWM2M_RESOURCE_INFO yapısında döndürülür:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-216">The resource information is returned in a NX_LWM2M_RESOURCE_INFO structure defined as follows:</span></span>

```c
typedef struct NX_LWM2M_RESOURCE_INFO_STRUCT
{
    NX_LWM2M_ID     nx_lwm2m_resource_info_id;
    USHORT          nx_lwm2m_resource_info_flags;
    UINT            nx_lwm2m_resource_info_dim;
} NX_LWM2M_RESOURCE_INFO;
```

- <span data-ttu-id="d0ad1-217">**nx_lwm2m_resource_info_id**: kaynağın kimliği.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-217">**nx_lwm2m_resource_info_id**: The ID of the Resource.</span></span>

- <span data-ttu-id="d0ad1-218">**nx_lwm2m_resource_info_flags**: aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-218">**nx_lwm2m_resource_info_flags**: See below.</span></span>

- <span data-ttu-id="d0ad1-219">**nx_lwm2m_resource_info_dim**: bayrak NX_LWM2M_RESOURCE_INFO_MULTIPLE ayarlandıysa birden çok kaynağın boyutu.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-219">**nx_lwm2m_resource_info_dim**: The dimension of Multiple Resource if the flag NX_LWM2M_RESOURCE_INFO_MULTIPLE is set.</span></span>

<span data-ttu-id="d0ad1-220">*Nx_lwm2m_resource_flags* alan aşağıdaki değerlere sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-220">The field *nx_lwm2m_resource_flags* can have to the following values:</span></span>

- <span data-ttu-id="d0ad1-221">0: tek okunabilir kaynak.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-221">0: Single readable resource.</span></span>

- <span data-ttu-id="d0ad1-222">**NX_LWM2M_RESOURCE_INFO_MULTIPLE**: birden çok kaynak, *nx_lwm2m_resource_info_dim* tanımlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-222">**NX_LWM2M_RESOURCE_INFO_MULTIPLE**: Multiple Resource, *nx_lwm2m_resource_info_dim* must be defined.</span></span>

- <span data-ttu-id="d0ad1-223">**NX_LWM2M_RESOURCE_INFO_EXECUTABLE**: çalıştırılabilir veya okunabilir olmayan kaynak.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-223">**NX_LWM2M_RESOURCE_INFO_EXECUTABLE**: Executable or Non-Readable Resource.</span></span>

### <a name="the-write-method"></a><span data-ttu-id="d0ad1-224">' Write ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="d0ad1-224">The 'Write' Method</span></span>

<span data-ttu-id="d0ad1-225">' Write ' yöntemi bir nesne örneğinin kaynaklarını güncelleştirmek ya da değiştirmek için kullanılır, işlevin aşağıdaki tanımı vardır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-225">The 'Write' method is used to update or replace resources of an Object Instance, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_write(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    const NX_LWM2M_RESOURCE *values_ptr, UINT write_op);
```

<span data-ttu-id="d0ad1-226">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-226">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="d0ad1-227">**object_ptr**: nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-227">**object_ptr**: Pointer to the Object implementation.</span></span>
- <span data-ttu-id="d0ad1-228">**instance_ptr**: nesne örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-228">**instance_ptr**: Pointer to the Object Instance.</span></span>
- <span data-ttu-id="d0ad1-229">**num_values**: yazılacak kaynak sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-229">**num_values**: The number of resources to write.</span></span>
- <span data-ttu-id="d0ad1-230">**values_ptr**: kaynak değerlerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-230">**values_ptr**: Pointer to the resources values.</span></span>
- <span data-ttu-id="d0ad1-231">**write_op**: yazma işlemlerinin türü.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-231">**write_op**: The type of write operations.</span></span>

<span data-ttu-id="d0ad1-232">*Write_op* parametresine aşağıdaki yazma işlemleri de belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-232">The following write operations can be specified to the *write_op* parameter :</span></span>

- <span data-ttu-id="d0ad1-233">0 &mdash; Kısmi güncelleştirme: yeni değerde belirtilen kaynakları ekler veya güncelleştirir ve diğer mevcut kaynakları değiştirmeden bırakır,</span><span class="sxs-lookup"><span data-stu-id="d0ad1-233">0 &mdash; Partial Update: adds or updates Resources provided in the new value and leaves other existing Resources unchanged,</span></span>

- <span data-ttu-id="d0ad1-234">**NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Örnek Değiştir: nesne örneğini, yeni sağlanmış kaynak değerleriyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-234">**NX_LWM2M_OBJECT_WRITE_REPLACE_INSTANCE** &mdash; Replace Instance: replaces the Object Instance with the new provided resource values.</span></span>

- <span data-ttu-id="d0ad1-235">**NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Kaynağı değiştir: kaynakları, belirtilen yeni kaynak değerleriyle (birden çok kaynağı değiştirmek için kullanılır) değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-235">**NX_LWM2M_OBJECT_WRITE_REPLACE_RESOURCE** &mdash; Replace Resource: replaces the Resources with the new provided resource values (used to replace Multiple Resources).</span></span>

- <span data-ttu-id="d0ad1-236">**NX_LWM2M_OBJECT_WRITE_CREATE** &mdash; Örnek oluştur: yeni oluşturulan nesne örneğini, belirtilen kaynak değerleriyle ( *nx_lwm2m_object_create* yönteminden çağırılır) başlatır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-236">**NX_LWM2M_OBJECT_WRITE_CREATE** &mdash; Create Instance: initializes the newly created Object Instance with the provided resource values (called from the *nx_lwm2m_object_create* method).</span></span>

- <span data-ttu-id="d0ad1-237">**NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap yazma: önyükleme sırası sırasında çağırılır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-237">**NX_LWM2M_OBJECT_WRITE_BOOTSTRAP** &mdash; Bootstrap Write: called during Bootstrap sequence.</span></span>

### <a name="the-execute-method"></a><span data-ttu-id="d0ad1-238">' Execute ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="d0ad1-238">The 'Execute' Method</span></span>

<span data-ttu-id="d0ad1-239">' Execute ' yöntemi bir nesne kaynağının yürütülmesini uygular, işlev aşağıdaki tanıma sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-239">The 'Execute' method implements the execution of an Object Resource, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_execute(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
    const CHAR *arguments_ptr);
```

<span data-ttu-id="d0ad1-240">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-240">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="d0ad1-241">**object_ptr**: nesne uygulamasına yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="d0ad1-241">**object_ptr**: Pointer to the Object implementation</span></span>
- <span data-ttu-id="d0ad1-242">**instance_ptr**: nesne örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-242">**instance_ptr**: Pointer to the Object Instance.</span></span>
- <span data-ttu-id="d0ad1-243">**resource_id**: kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-243">**resource_id**: The Resource ID.</span></span>
- <span data-ttu-id="d0ad1-244">**arguments_ptr**: yürütme işleminin bağımsız değişkenlerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-244">**arguments_ptr**: Pointer to the arguments of the execute operation.</span></span> <span data-ttu-id="d0ad1-245">*Arguments_length* sıfırsa null olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-245">Can be NULL if *arguments_length* is zero.</span></span>
- <span data-ttu-id="d0ad1-246">**arguments_length**: bağımsız değişkenlerin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-246">**arguments_length**: The length of the arguments.</span></span>

<span data-ttu-id="d0ad1-247">Kaynak KIMLIĞI yoksa işlevin NX_LWM2M_NOT_FOUND döndürmesi veya yürütmeyi desteklememesi durumunda NX_LWM2M_METHOD_NOT_ALLOWED gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-247">The function must return NX_LWM2M_NOT_FOUND if the Resource ID doesn't exist, or NX_LWM2M_METHOD_NOT_ALLOWED if it doesn't support execution.</span></span>

### <a name="the-create-method"></a><span data-ttu-id="d0ad1-248">' Create ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="d0ad1-248">The 'Create' Method</span></span>

<span data-ttu-id="d0ad1-249">' Create ' yöntemi, yeni bir nesne örneği oluşturulmasını uygular, işlev aşağıdaki tanıma sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-249">The 'Create' method implements the creation of a new Object Instance, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_create(NX_LWM2M_OBJECT * object_ptr,
    NX_LWM2M_ID instance_id, UINT num_values, const NX_LWM2M_RESOURCE *values_ptr,
    NX_LWM2M_OBJECT_INSTANCE **instance_ptr, NX_LWM2M_BOOL bootstrap);
```

<span data-ttu-id="d0ad1-250">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-250">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="d0ad1-251">**object_ptr**: nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-251">**object_ptr**: Pointer to the Object implementation.</span></span>
- <span data-ttu-id="d0ad1-252">**instance_id**: yenı örneğin kimliği.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-252">**instance_id**: The ID of the new Instance.</span></span>
- <span data-ttu-id="d0ad1-253">**num_values**: başlatılacak kaynak sayısı.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-253">**num_values**: The number of resources to initialize.</span></span>
- <span data-ttu-id="d0ad1-254">**values_ptr**: kaynak değerlerine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-254">**values_ptr**: Pointer to the resources values.</span></span>
- <span data-ttu-id="d0ad1-255">**instance_ptr**: oluşturulan örneğin hedef işaretçisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-255">**instance_ptr**: Pointer to the destination pointer of the created instance.</span></span>
- <span data-ttu-id="d0ad1-256">**bootstrap**: önyükleme sırasından çağrılırsa true.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-256">**bootstrap**: True if called from bootstrap sequence.</span></span>

<span data-ttu-id="d0ad1-257">Nesne, belirtilen kaynak değerleri listesini kullanarak yeni bir nesne örneği ayırmalıdır ve bu örneğe yeniden başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-257">The Object must allocate and initialiaze a new Object instance, using the provided list of resource values.</span></span>

### <a name="the-delete-method"></a><span data-ttu-id="d0ad1-258">' DELETE ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="d0ad1-258">The 'Delete' Method</span></span>

<span data-ttu-id="d0ad1-259">' DELETE ' yöntemi bir nesne örneğinin silinmesini uygular, işlev aşağıdaki tanıma sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-259">The 'Delete' method implements the deletion of an object instance, the function has the following definition:</span></span>

```c
UINT nx_lwm2m_object_delete(NX_LWM2M_OBJECT *object_ptr,
                NX_LWM2M_OBJECT_INSTANCE *instance_ptr);
```

<span data-ttu-id="d0ad1-260">Giriş parametreleri aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0ad1-260">The input parameters are defined as follows:</span></span>

- <span data-ttu-id="d0ad1-261">**object_ptr**: nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-261">**object_ptr**: Pointer to the Object implementation.</span></span>
- <span data-ttu-id="d0ad1-262">**instance_ptr**: nesne örneğine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-262">**instance_ptr**: Pointer to the Object Instance.</span></span>

<span data-ttu-id="d0ad1-263">Başarılı olduğunda, nesne örnek verilerini ve örnek tarafından ayrılan diğer kaynakları serbest bırakmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-263">On success the Object must release the Object Instance data and any other resource allocated by the instance.</span></span>

### <a name="adding-object-implementations-and-instances-to-the-lwm2m-client"></a><span data-ttu-id="d0ad1-264">LWM2M Istemcisine nesne uygulamaları ve örnekler ekleme</span><span class="sxs-lookup"><span data-stu-id="d0ad1-264">Adding Object Implementations and Instances to the LWM2M Client</span></span>

<span data-ttu-id="d0ad1-265">Uygulama, ***nx_lwm2m_client_object_add*** HIZMETINI çağırarak LWM2M istemcisine yeni nesne uygulaması ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-265">The application can add new object implementation to the LWM2M Client by calling the ***nx_lwm2m_client_object_add*** service.</span></span>

<span data-ttu-id="d0ad1-266">Nesnesi dinamik örnek oluşturmayı desteklemiyorsa örneğin yalnızca tek örnekli bir nesne ise, nesne yapısının *nx_lwm2m_object_instances* alanı statik örnekler yapıları listesine işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-266">If the Object doesn't support dynamic creation of Instances, for example if it's a single instance only Object, the *nx_lwm2m_object_instances* field of the object structure should point to the list of the static instances structures.</span></span>

<span data-ttu-id="d0ad1-267">Nesne dinamik örnek oluşturmayı destekliyorsa, *NX_LWM2M_OBJECT_INSTANCES* null olarak ayarlanmalıdır ve nesnenin ' Create ' metodunu çağırmak için bunun yerine ***nx_lwm2m_client_object_create*** hizmeti kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-267">If the Object supports dynamic instance creation, *nx_lwm2m_object_instances* should be set to NULL and the ***nx_lwm2m_client_object_create*** service should be used instead in order to call the 'Create' method of the object.</span></span>

## <a name="example-of-lwm2m-client-application"></a><span data-ttu-id="d0ad1-268">LWM2M Istemci uygulaması örneği</span><span class="sxs-lookup"><span data-stu-id="d0ad1-268">Example of LWM2M Client Application</span></span>

<span data-ttu-id="d0ad1-269">Aşağıdaki kod, bir sıcaklık sensörden ve hafif anahtardan oluşan özel bir cihaz uygulayan basit bir LWM2M Istemci uygulamasına bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-269">The following code is an example of a simple LWM2M Client Application which implements a custom device consisting of a temperature sensor and a light switch.</span></span>

<span data-ttu-id="d0ad1-270">Cihaz, bir sunucunun ısı algılayıcısı değerini ve ışık anahtarının Boole durumunu okumasına izin verir ve ışığı açık/kapalı olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d0ad1-270">The device allows a server to read the value of the temperature sensor and the boolean state of the light switch, and to set the light switch to on/off.</span></span>

```c
#include "nx_lwm2m_client.h"

/* Custom Object implementation */
/* Define the Custom Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_OBJECT_INSTANCE     lwm2m;

    /* Resources Data */
    NX_LWM2M_FLOAT32             temperature;
    NX_LWM2M_BOOL                light;
} MYOBJECT_INSTANCE;

/* Define the Resources IDs */
#define MYOBJECT_RES_TEMPERATURE     0 /* temperature sensor */
#define MYOBJECT_RES_LIGHT           1 /* light switch */

/* Define the 'Read' Method */
UINT myobject_read(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr,
    UINT num_values, NX_LWM2M_RESOURCE *values)
{
    UINT i;
    for (i=0; i<num_values; i++)
    {
        switch (values[i].nx_lwm2m_resource_id)
        {
        case MYOBJECT_RES_TEMPERATURE:

            /* return the temperature value */
            values[i].nx_lwm2m_resource_type = NX_LWM2M_RESOURCE_FLOAT32;
            values[i].nx_lwm2m_resource_value.nx_lwm2m_resource_float32data =
                ((MYOBJECT_INSTANCE *) instance_ptr)->temperature;
            break;
        case MYOBJECT_RES_LIGHT:

            /* return the state of the light switch */
            values[i].nx_lwm2m_resource_type = NX_LWM2M_RESOURCE_BOOLEAN;
            values[i].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata =
                ((MYOBJECT_INSTANCE *) instance_ptr)->light;
            break;

        default:

            /* unknown resource ID */
            return NX_LWM2M_NOT_FOUND;
        }
    }
    return NX_SUCCESS;
}

/* Define the 'Discover' method */
UINT myobject_discover(NX_LWM2M_OBJECT *object_ptr, NX_LWM2M_OBJECT_INSTANCE *instance_ptr,
                                    UINT *num_resources, NX_LWM2M_RESOURCE_INFO *resources)
{
    if (*num_resources < 2)
    {
        return NX_LWM2M_BUFFER_TOO_SMALL;
    }

    /* return the list of supported resources IDs */
    *num_resources = 2;
    resources[0].nx_lwm2m_resource_info_id        = MYOBJECT_RES_TEMPERATURE;
    resources[0].nx_lwm2m_resource_info_flags     = 0;
    resources[1].nx_lwm2m_resource_info_id        = MYOBJECT_RES_LIGHT;
    resources[1].nx_lwm2m_resource_info_flags     = 0;
    return NX_SUCCESS;
}

/* Define the 'Write' method */
UINT myobject_write(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, UINT num_values,
    const NX_LWM2M_RESOURCE *values, UINT flags)
{
    UINT i;
    for (i=0; i<num_values; i++)
    {
        UINT ret;
        switch (values[i].nx_lwm2m_resource_id)
        {

        case MYOBJECT_RES_TEMPERATURE:

            /* read-only resource */
            return NX_LWM2M_METHOD_NOT_ALLOWED;

        case MYOBJECT_RES_LIGHT:

            /* assign boolean value */

            ret = nx_lwm2m_resource_get_boolean(&values[i],
                &((MYOBJECT_INSTANCE *) instance_ptr)->light);

            if (ret != NX_SUCCESS)
            {

                /* invalid value type */
                return ret;
            }
            break;

        default:

            /* unknown resource ID */
            return NX_LWM2M_NOT_FOUND;
        }
    }
    return NX_SUCCESS;
}

/* Define the 'Execute' method */
UINT myobject_execute(NX_LWM2M_OBJECT *object_ptr,
    NX_LWM2M_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_ID resource_id,
    const CHAR *args_ptr, UINT args_length)
{
    switch (resource_id)
    {

    case MYOBJECT_RES_TEMPERATURE:
    case MYOBJECT_RES_LIGHT:

        /* read-only resource */
        return NX_LWM2M_METHOD_NOT_ALLOWED;

    default:

        /* unknown resource ID */
        return NX_LWM2M_NOT_FOUND;

    }
}

/* NetX data */
NX_IP                       ip;
NX_PACKET_POOL              packet_pool;

/* LWM2M Client data */
NX_LWM2M_CLIENT             client;
ULONG                       client_stack[4096 / sizeof(ULONG)];
NX_LWM2M_CLIENT_SESSION     session;

/* Custom Object Data */
NX_LWM2M_OBJECT             myobject;
MYOBJECT_INSTANCE           myinstance;

/* Define the session state callback */
void session_callback(NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state)
{
    switch (state)
    {

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:

        /* Bootstrap session done, we can register to the LWM2M Server */
        {
            NX_LWM2M_ID security_id;

            /* find the Security Object Instance of the LWM2M Server */
            security_id = NX_LWM2M_RESERVED_ID;
            while (nx_lwm2m_client_object_instance_get_next(&client,
                NX_LWM2M_SECURITY_OBJECT_ID, &security_id) == NX_SUCCESS)
            {
                NX_LWM2M_RESOURCE res[3];

                /* retrieve instance data: */
                /* Bootstrap server flag */
                res[0].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_BOOTSTRAP_ID;

                /* URI of server */
                res[1].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_URI_ID;

                /* Short Server ID */
                res[2].nx_lwm2m_resource_id = NX_LWM2M_SECURITY_SHORT_SERVER_ID;

                /* Read Object Instance: */
                nx_lwm2m_client_object_read(&client,
                    NX_LWM2M_SECURITY_OBJECT_ID, security_id, 3, res);

                /* Not a bootstrap server? */
                if (!res[0].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata)
                {
                    ULONG ip_addr;
                    UINT udp_port;

                    /* get IP address and UDP port from server URI */
                    parse_uri(res[1].nx_lwm2m_resource_value.nx_lwm2m_resource_stringdata, &ip_addr, &udp_port);

                    /* Start registration to the LWM2M server */
                    nx_lwm2m_client_session_register(&session,
                        (NX_LWM2M_ID) res[2].nx_lwm2m_resource_value.
                        nx_lwm2m_resource_integer32data,
                        ip_addr, udp_port);
                    break;
                }
            }
        }
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:

        /* Failed to Bootstrap the LWM2M Client. */
        break;

    case NX_LWM2M_CLIENT_SESSION_REGISTERED:

        /* Registration to the LWM2M Client done. */
        break;

    case NX_LWM2M_CLIENT_SESSION_ERROR:

        /* Failed to register to the LWM2M Client. */
        break;
    }
}

/* Application main thread */
void application_thread(ULONG info)
{
    NX_LWM2M_RESOURCE res[4];
    NX_LWM2M_ID security_id;

    /* Create the LWM2M client */
    nx_lwm2m_client_create(&client, &ip, &packet_pool, NX_LWM2M_COAP_PORT,
        "mylwm2mclient", NULL, NX_LWM2M_BINDING_U,
        client_stack, sizeof(client_stack));

    /* Define our custom object */
    myobject.nx_lwm2m_object_id           = 1024;
    myobject.nx_lwm2m_object_read         = myobject_read;
    myobject.nx_lwm2m_object_discover     = myobject_discover;
    myobject.nx_lwm2m_object_write        = myobject_write;
    myobject.nx_lwm2m_object_execute      = myobject_execute;
    myobject.nx_lwm2m_object_create       = NULL;
    myobject.nx_lwm2m_object_delete       = NULL;

    /* Define a single instance */
    myobject.nx_lwm2m_object_instances             = (NX_LWM2M_OBJECT_INSTANCE *) &myinstance;
    myinstance.lwm2m.nx_lwm2m_object_instance_id   = 0;
    myinstance.lwm2m.nx_lwm2m_object_instance_next = NULL;
    myinstance.temperature                         = 22.5f;
    myinstance.light                               = NX_FALSE;

    /* Add the object to the LWM2M Client */
    nx_lwm2m_client_object_add(&client, &myobject);

    /* Create a security entry for the bootstrap server */
    security_id = 0;

    /* set the URI of the server */
    res[0].nx_lwm2m_resource_id                                 = NX_LWM2M_SECURITY_URI_ID;
    res[0].nx_lwm2m_resource_type                               = NX_LWM2M_RESOURCE_STRING;
    res[0].nx_lwm2m_resource_value.nx_lwm2m_resource_stringdata = "coap://1.2.3.4";

    /* set the Bootstrap flag */
    res[1].nx_lwm2m_resource_id                                  = NX_LWM2M_SECURITY_BOOTSTRAP_ID;
    res[1].nx_lwm2m_resource_type                                = NX_LWM2M_RESOURCE_BOOLEAN;
    res[1].nx_lwm2m_resource_value.nx_lwm2m_resource_booleandata = NX_TRUE;

    /* set the security mode */
    res[2].nx_lwm2m_resource_id                                    = NX_LWM2M_SECURITY_MODE_ID;
    res[2].nx_lwm2m_resource_type                                  = NX_LWM2M_RESOURCE_INTEGER32;
    res[2].nx_lwm2m_resource_value.nx_lwm2m_resource_integer32data =
    NX_LWM2M_SECURITY_MODE_NOSEC;

    /* set the Hold Off timer */
    res[3].nx_lwm2m_resource_id                                    = NX_LWM2M_SECURITY_HOLD_OFF_ID;
    res[3].nx_lwm2m_resource_type                                  = NX_LWM2M_RESOURCE_INTEGER32;
    res[3].nx_lwm2m_resource_value.nx_lwm2m_resource_integer32data = 10;
    nx_lwm2m_client_object_create(&client, NX_LWM2M_SECURITY_OBJECT_ID,
        &security_id, 4, res);

    /* Create a session */
    nx_lwm2m_client_session_create(&session, &client, session_callback);

    /* start bootstrap session */
    nx_lwm2m_client_session_bootstrap(&session, security_id,
                            IP_ADDRESS(1, 2, 3, 4), 5683);

    /* Application main loop */
    while (1)
    {
        /* ...application code... */
    }

    /* Terminate the LWM2M Client */
    nx_lwm2m_client_delete(&client);
}
```
