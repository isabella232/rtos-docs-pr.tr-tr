---
title: Bölüm 3-LWM2M Istemcisinin Işlevsel açıklaması
description: Bu bölüm, LWM2M Istemcisinin işlevsel bir açıklamasını içerir.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 24b7ff66fb4d060075eb6bc81bed45b3479e18dc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825937"
---
# <a name="chapter-3--functional-description-of-lwm2m-client"></a><span data-ttu-id="66119-103">Bölüm 3 LWM2M Istemcisinin Işlevsel açıklaması</span><span class="sxs-lookup"><span data-stu-id="66119-103">Chapter 3  Functional Description of LWM2M Client</span></span>

> <span data-ttu-id="66119-104">Bu bölüm, LWM2M Istemcisinin işlevsel bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="66119-104">This chapter contains a functional description of LWM2M Client.</span></span>

## <a name="lwm2m-client-initialization"></a><span data-ttu-id="66119-105">LWM2M Istemci başlatması</span><span class="sxs-lookup"><span data-stu-id="66119-105">LWM2M Client Initialization</span></span>

<span data-ttu-id="66119-106">LWM2M Istemcisi ***nx_lwm2m_client_create*** hizmeti çağırarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="66119-106">The LWM2M Client is initialized by calling ***nx_lwm2m_client_create*** service.</span></span> <span data-ttu-id="66119-107">LWM2M Istemcisi kendi iş parçacığında çalışır ve geri çağırmalar kullanılarak veya uygulama tarafından uygulanan özel nesnelerin yöntemlerini çağırarak uygulamaya bazı olayları bildirebilir.</span><span class="sxs-lookup"><span data-stu-id="66119-107">The LWM2M Client runs in its own thread and can report some events to the application through the use of callbacks, or by calling methods of the custom objects implemented by the application.</span></span>

<span data-ttu-id="66119-108">Ayrıca, bir veya daha fazla sunucuyla iletişimi etkinleştirmek için ***nx_lwm2m_client_session_create*** çağırarak LWM2M istemci oturumlarının oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="66119-108">In addition, LWM2M Client Sessions must be created by calling ***nx_lwm2m_client_session_create*** for enabling communication with one or more servers.</span></span> <span data-ttu-id="66119-109">Bir oturum iki farklı sunucu türüyle iletişim kurabilir: bir önyükleme sunucusu veya LWM2M sunucusu (cihaz yönetimi).</span><span class="sxs-lookup"><span data-stu-id="66119-109">A session can communicate with two different types of servers: a Bootstrap Server or a LWM2M Server (Device Management).</span></span>

### <a name="bootstrap-server-session"></a><span data-ttu-id="66119-110">Önyükleme sunucusu oturumu</span><span class="sxs-lookup"><span data-stu-id="66119-110">Bootstrap Server Session</span></span>

<span data-ttu-id="66119-111">LWM2M Istemcisinin, bir veya daha fazla LWM2M sunucusuyla "Register" işlemini gerçekleştirmesini sağlamak için, LWM2M Istemcisine bir iletişim oturumu, bir önyükleme sunucusu ile ilgili bilgi sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66119-111">A communication session with a Bootstrap Server is used to provision essential information into the LWM2M Client to enable the LWM2M Client to perform the operation “Register” with one or more LWM2M Servers.</span></span> <span data-ttu-id="66119-112">Istemci tarafından başlatılan ve sunucu tarafından başlatılan önyükleme modlarında bu tür bir sunucu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66119-112">This type of server is used during the Client Initiated and Server Initiated Bootstrap modes.</span></span>

<span data-ttu-id="66119-113">Uygulama, ***nx_lwm2m_client_session_bootstrap** _ veya _*_Nx_lwm2m_client_session_bootstrap_dtls_\*_ çağırarak bir önyükleme oturumu başlatabilir, sunucunun IP adresini ve bağlantı noktası numarasını ve Isteğe bağlı BIR güvenlik nesnesi örnek kimliğini sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="66119-113">The application can start a Bootstrap session by calling ***nx_lwm2m_client_session_bootstrap** _ or _*_nx_lwm2m_client_session_bootstrap_dtls_\*_, it must provide the IP address and port number of the server, and an optional Security Object Instance ID.</span></span> <span data-ttu-id="66119-114">_*_Nx_lwm2m_client_session_bootstrap_*_ işlevi güvenli olmayan iletişim kullanır, ancak _ *_nx_lwm2m_client_session_bootstrap_dtls_*\* sunucuyla güvenli bir DTLS bağlantısı kurar.</span><span class="sxs-lookup"><span data-stu-id="66119-114">The _*_nx_lwm2m_client_session_bootstrap_*_ function uses insecure communication, whereas _ *_nx_lwm2m_client_session_bootstrap_dtls_*\* establishes a secure DTLS connection with the server.</span></span>

<span data-ttu-id="66119-115">Önyükleme işlemi başarılı olursa, önyükleme sunucusu, önyükleme ve LWM2M sunucuları için güvenlik nesne örnekleri ve LWM2M sunucuları için sunucu nesne örnekleri oluşturmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="66119-115">If the Bootstrap operation is successful, the Bootstrap server should have created Security Object Instance(s) for the Bootstrap and LWM2M Servers, and Server Object Instance(s) for the LWM2M Servers.</span></span> <span data-ttu-id="66119-116">Uygulama, LWM2M sunucusu bilgilerini almak için ***nx_lwm2m_client_session_register_info_get*** çağırabilir ve bu bilgileri lwm2m sunucuları ile oturum oluşturmak için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="66119-116">The application can call ***nx_lwm2m_client_session_register_info_get*** to get LWM2M Server(s) information and use this information for establishing a session with the LWM2M Server(s).</span></span>

<span data-ttu-id="66119-117">Önyükleme verileri, cihazın bir sonraki yeniden başlatmada LWM2M Istemcisini yapılandırmak için uygulama tarafından geçici olmayan belleğe kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="66119-117">The Bootstrap data should be saved to non-volatile memory by the application to configure the LWM2M Client at the next reboot of the device.</span></span>

### <a name="lwm2m-server-session"></a><span data-ttu-id="66119-118">LWM2M sunucusu oturumu</span><span class="sxs-lookup"><span data-stu-id="66119-118">LWM2M Server Session</span></span>

<span data-ttu-id="66119-119">Kayıt, cihaz yönetimi ve hizmet etkinleştirme için bir LWM2M sunucusuyla iletişim oturumu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66119-119">A communication session with a LWM2M Server is used for Registration, Device Management and Service Enablement.</span></span>

<span data-ttu-id="66119-120">Uygulama, LWM2M Istemcisini ***nx_lwm2m_client_session_register** _ veya _*_nx_lwm2m_client_session_register_dtls_\*_ çağırarak sunucuya kaydedebilir, sunucunun IP adresini ve bağlantı noktası numarasını ve var olan bir sunucu nesnesi örneğine KARŞıLıK gelen kısa sunucu kimliğini sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="66119-120">The application can register the LWM2M Client to a server by calling ***nx_lwm2m_client_session_register** _ or _*_nx_lwm2m_client_session_register_dtls_\*_, it must provide the IP address and port number of the server, and the Short Server ID which corresponds to an existing Server Object Instance.</span></span> <span data-ttu-id="66119-121">_*_Nx_lwm2m_client_session_register_*_ işlevi güvenli olmayan iletişim kullanır, ancak _ *_nx_lwm2m_client_session_register_dtls_*\* sunucuyla güvenli bir DTLS bağlantısı kurar.</span><span class="sxs-lookup"><span data-stu-id="66119-121">The _*_nx_lwm2m_client_session_register_*_ function uses insecure communication, whereas  _ *_nx_lwm2m_client_session_register_dtls_*\* establishes a secure DTLS connection with the server.</span></span>

<span data-ttu-id="66119-122">Uygulama, \***nx_lwm2m_client_session_deregister** _ ' i çağırarak LWM2M istemcisini kaydedebilir ve istemciden _ *_nx_lwm2m_client_session_update_* \* çağırarak bir ' güncelleştirme ' iletisi göndermesini ister.</span><span class="sxs-lookup"><span data-stu-id="66119-122">The application can de-register the LWM2M Client by calling ***nx_lwm2m_client_session_deregister** _, and ask the client to send an ‘Update’ message by calling _*_nx_lwm2m_client_session_update_\*\*.</span></span>

### <a name="session-state-callback"></a><span data-ttu-id="66119-123">Oturum durumu geri çağırma</span><span class="sxs-lookup"><span data-stu-id="66119-123">Session State Callback</span></span>

<span data-ttu-id="66119-124">Uygulama, oturum durumu güncellendiğinde çağrılan bir oturum oluşturma sırasında bir geri çağırma kaydeder, geri çağırma işlevi **NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK** aşağıdaki prototiple sahiptir.</span><span class="sxs-lookup"><span data-stu-id="66119-124">The application registers a callback at creation of a session which is called when the state of the session is updated, the callback function **NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK** has the following prototype.</span></span>

<span data-ttu-id="66119-125">TypeDef VOID ( \* NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK) (NX_LWM2M_CLIENT_SESSION \* SESSION_PTR, UINT durumu);</span><span class="sxs-lookup"><span data-stu-id="66119-125">typedef VOID (\*NX_LWM2M_CLIENT_SESSION_STATE_CALLBACK)(NX_LWM2M_CLIENT_SESSION \*session_ptr,UINT state);</span></span>

<span data-ttu-id="66119-126">Aşağıdaki durumlar tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="66119-126">The following states are defined.</span></span>

| <span data-ttu-id="66119-127">Oturum &nbsp; durumu</span><span class="sxs-lookup"><span data-stu-id="66119-127">Session&nbsp;State</span></span> | <span data-ttu-id="66119-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-129">**NX_LWM2M_CLIENT_SESSION_INIT**</span><span class="sxs-lookup"><span data-stu-id="66119-129">**NX_LWM2M_CLIENT_SESSION_INIT**</span></span> | <span data-ttu-id="66119-130">Oturum oluşturulduktan sonra ilk durum.</span><span class="sxs-lookup"><span data-stu-id="66119-130">The initial state after session creation.</span></span> |
| <span data-ttu-id="66119-131">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING**</span><span class="sxs-lookup"><span data-stu-id="66119-131">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_WAITING**</span></span> | <span data-ttu-id="66119-132">İstemci, ' bekletme ' süreölçeri veya sunucu tarafından başlatılan önyükleme işleminin sona erme süresini bekliyor.</span><span class="sxs-lookup"><span data-stu-id="66119-132">The client is waiting for the expiration of the ‘Hold Off’ timer or Server Initiated Bootstrap.</span></span> |
| <span data-ttu-id="66119-133">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**</span><span class="sxs-lookup"><span data-stu-id="66119-133">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING**</span></span> | <span data-ttu-id="66119-134">İstemci, önyükleme sunucusuna bir ' Istek ' iletisi gönderdi (Istemci tarafından başlatılan önyükleme).</span><span class="sxs-lookup"><span data-stu-id="66119-134">The client has sent a ‘Request’ message to the Bootstrap Server (Client Initiated Bootstrap).</span></span> |
| <span data-ttu-id="66119-135">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**</span><span class="sxs-lookup"><span data-stu-id="66119-135">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED**</span></span> | <span data-ttu-id="66119-136">İstemci, önyükleme sunucusundan veri alıyor.</span><span class="sxs-lookup"><span data-stu-id="66119-136">The client is receiving data from the Bootstrap Server.</span></span> |
| <span data-ttu-id="66119-137">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED**</span><span class="sxs-lookup"><span data-stu-id="66119-137">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED**</span></span> | <span data-ttu-id="66119-138">Önyükleme sunucusu ' finished ' iletisi gönderdi.</span><span class="sxs-lookup"><span data-stu-id="66119-138">The Bootstrap Server has sent a ‘Finished’ message.</span></span> |
| <span data-ttu-id="66119-139">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR**</span><span class="sxs-lookup"><span data-stu-id="66119-139">**NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR**</span></span> | <span data-ttu-id="66119-140">Önyükleme oturumu başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="66119-140">The bootstrap session has failed.</span></span> |
| <span data-ttu-id="66119-141">**NX_LWM2M_CLIENT_SESSION_REGISTERING**</span><span class="sxs-lookup"><span data-stu-id="66119-141">**NX_LWM2M_CLIENT_SESSION_REGISTERING**</span></span> | <span data-ttu-id="66119-142">İstemci, LWM2M sunucusuna bir ' Register ' iletisi gönderdi.</span><span class="sxs-lookup"><span data-stu-id="66119-142">The client has sent a ‘Register’ message to the LWM2M Server.</span></span> |
| <span data-ttu-id="66119-143">**NX_LWM2M_CLIENT_SESSION_REGISTERED**</span><span class="sxs-lookup"><span data-stu-id="66119-143">**NX_LWM2M_CLIENT_SESSION_REGISTERED**</span></span> | <span data-ttu-id="66119-144">İstemci LWM2M sunucusuna kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="66119-144">The client is registered to the LWM2M Server.</span></span> |
| <span data-ttu-id="66119-145">**NX_LWM2M_CLIENT_SESSION_UPDATING**</span><span class="sxs-lookup"><span data-stu-id="66119-145">**NX_LWM2M_CLIENT_SESSION_UPDATING**</span></span> | <span data-ttu-id="66119-146">İstemci, LWM2M sunucusuna bir ' Update ' iletisi gönderdi.</span><span class="sxs-lookup"><span data-stu-id="66119-146">The client has sent an ‘Update’ message to the LWM2M Server.</span></span> |
| <span data-ttu-id="66119-147">**NX_LWM2M_CLIENT_SESSION_DEREGISTERING**</span><span class="sxs-lookup"><span data-stu-id="66119-147">**NX_LWM2M_CLIENT_SESSION_DEREGISTERING**</span></span> | <span data-ttu-id="66119-148">İstemci, LWM2M sunucusuna ' de Register ' iletisi gönderdi.</span><span class="sxs-lookup"><span data-stu-id="66119-148">The client has sent an ‘De-register’ message to the LWM2M Server.</span></span> |
| <span data-ttu-id="66119-149">**NX_LWM2M_CLIENT_SESSION_DEREGISTERED**</span><span class="sxs-lookup"><span data-stu-id="66119-149">**NX_LWM2M_CLIENT_SESSION_DEREGISTERED**</span></span> | <span data-ttu-id="66119-150">İstemci, LWM2M sunucusundan de kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="66119-150">The client is de-registered from the LWM2M Server.</span></span> |
| <span data-ttu-id="66119-151">**NX_LWM2M_CLIENT_SESSION_DISABLED**</span><span class="sxs-lookup"><span data-stu-id="66119-151">**NX_LWM2M_CLIENT_SESSION_DISABLED**</span></span> | <span data-ttu-id="66119-152">LWM2M sunucusu devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="66119-152">The LWM2M Server is disabled.</span></span> <span data-ttu-id="66119-153">Devre dışı bırakma süreölçeri sona erdikten sonra bir ' Register ' gönderilir.</span><span class="sxs-lookup"><span data-stu-id="66119-153">A ‘Register’ will be sent after the expiration of the disable timer.</span></span> |
| <span data-ttu-id="66119-154">**NX_LWM2M_CLIENT_SESSION_ERROR**</span><span class="sxs-lookup"><span data-stu-id="66119-154">**NX_LWM2M_CLIENT_SESSION_ERROR**</span></span> | <span data-ttu-id="66119-155">LWM2M sunucusuna kaydolma veya güncelleştirme işlemi başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="66119-155">The registration or update operation to the LWM2M Server has failed.</span></span> |
| <span data-ttu-id="66119-156">**NX_LWM2M_CLIENT_SESSION_DELETED**</span><span class="sxs-lookup"><span data-stu-id="66119-156">**NX_LWM2M_CLIENT_SESSION_DELETED**</span></span> | <span data-ttu-id="66119-157">LWM2M sunucusuna karşılık gelen sunucu nesnesi örneği silindi.</span><span class="sxs-lookup"><span data-stu-id="66119-157">The Server Object Instance corresponding to the LWM2M Server has been deleted.</span></span> |

<span data-ttu-id="66119-158">Hata durumunda uygulamanın, ***nx_lwm2m_client_session_error_get*** çağırarak hatanın nedenini elde edebilir.</span><span class="sxs-lookup"><span data-stu-id="66119-158">In case of error the application can retrieve the cause of the error by calling ***nx_lwm2m_client_session_error_get***.</span></span>

## <a name="local-device-management"></a><span data-ttu-id="66119-159">Yerel cihaz yönetimi</span><span class="sxs-lookup"><span data-stu-id="66119-159">Local Device Management</span></span>

<span data-ttu-id="66119-160">Uygulama, yerel cihaz yönetimi işlevlerini kullanarak LWM2M Istemcisinin nesnelerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="66119-160">The application can access the Objects of the LWM2M Client by using the local device management functions.</span></span> <span data-ttu-id="66119-161">Aşağıdaki işlevler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66119-161">The following functions are provided.</span></span>

| <span data-ttu-id="66119-162">İşlev &nbsp; adı</span><span class="sxs-lookup"><span data-stu-id="66119-162">Function&nbsp;Name</span></span> | <span data-ttu-id="66119-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-163">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-164">***nx_lwm2m_client_object_read***</span><span class="sxs-lookup"><span data-stu-id="66119-164">***nx_lwm2m_client_object_read***</span></span> | <span data-ttu-id="66119-165">Bir nesne örneğinden kaynakları okuyun.</span><span class="sxs-lookup"><span data-stu-id="66119-165">Read resources from an Object Instance.</span></span> |
| <span data-ttu-id="66119-166">***nx_lwm2m_client_object_discover***</span><span class="sxs-lookup"><span data-stu-id="66119-166">***nx_lwm2m_client_object_discover***</span></span> | <span data-ttu-id="66119-167">Bir nesne örneğinin kaynak listesini alın.</span><span class="sxs-lookup"><span data-stu-id="66119-167">Get the list of the resources of an Object Instance.</span></span>
| <span data-ttu-id="66119-168">***nx_lwm2m_client_object_write***</span><span class="sxs-lookup"><span data-stu-id="66119-168">***nx_lwm2m_client_object_write***</span></span> | <span data-ttu-id="66119-169">Kaynakları bir nesne örneğine yazın.</span><span class="sxs-lookup"><span data-stu-id="66119-169">Write resources to an Object Instance.</span></span> |
| <span data-ttu-id="66119-170">***nx_lwm2m_client_object_execute***</span><span class="sxs-lookup"><span data-stu-id="66119-170">***nx_lwm2m_client_object_execute***</span></span> | <span data-ttu-id="66119-171">Bir nesne örneğinin kaynağında yürütme işlemini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="66119-171">Perform the Execute operation on a resource of an Object Instance.</span></span> |
| <span data-ttu-id="66119-172">***nx_lwm2m_client_object_create***</span><span class="sxs-lookup"><span data-stu-id="66119-172">***nx_lwm2m_client_object_create***</span></span> | <span data-ttu-id="66119-173">Yeni bir nesne örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="66119-173">Create a new Object Instance.</span></span> |
| <span data-ttu-id="66119-174">***nx_lwm2m_client_object_delete***</span><span class="sxs-lookup"><span data-stu-id="66119-174">***nx_lwm2m_client_object_delete***</span></span> | <span data-ttu-id="66119-175">Varolan bir nesne örneğini silin.</span><span class="sxs-lookup"><span data-stu-id="66119-175">Delete an existing Object Instance.</span></span> |
| <span data-ttu-id="66119-176">***nx_lwm2m_client_object_next_get***</span><span class="sxs-lookup"><span data-stu-id="66119-176">***nx_lwm2m_client_object_next_get***</span></span> | <span data-ttu-id="66119-177">LWM2M Istemcisinin sonraki nesne KIMLIĞINI alın.</span><span class="sxs-lookup"><span data-stu-id="66119-177">Get the next Object ID by the LWM2M Client.</span></span> |
| <span data-ttu-id="66119-178">***nx_lwm2m_client_object_instance_next_get***</span><span class="sxs-lookup"><span data-stu-id="66119-178">***nx_lwm2m_client_object_instance_next_get***</span></span> | <span data-ttu-id="66119-179">Bir nesnenin sonraki örneğini alır.</span><span class="sxs-lookup"><span data-stu-id="66119-179">Get the next Instance of an Object.</span></span> |

## <a name="resource-information"></a><span data-ttu-id="66119-180">Kaynak bilgileri</span><span class="sxs-lookup"><span data-stu-id="66119-180">Resource Information</span></span>

<span data-ttu-id="66119-181">Nesneleri okuma ve nesnelere yazma sırasında bir kaynak NX_LWM2M_CLIENT_RESOURCE yapısıyla temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="66119-181">When reading from and writing to Objects a Resource is represented by the NX_LWM2M_CLIENT_RESOURCE structure.</span></span> <span data-ttu-id="66119-182">Bu yapı, kaynak/örnek KIMLIĞINI ve değerini içerir.</span><span class="sxs-lookup"><span data-stu-id="66119-182">This structure contains the ID of the Resource/Instance and its value.</span></span>

<span data-ttu-id="66119-183">Kaynak bilgileri ve değeri ayarlamak için aşağıdaki işlevler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66119-183">The following functions are provided for setting resource info and value.</span></span>

| <span data-ttu-id="66119-184">İşlev &nbsp; adı</span><span class="sxs-lookup"><span data-stu-id="66119-184">Function&nbsp;Name</span></span> | <span data-ttu-id="66119-185">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-185">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-186">***nx_lwm2m_client_resource_info_set***</span><span class="sxs-lookup"><span data-stu-id="66119-186">***nx_lwm2m_client_resource_info_set***</span></span> | <span data-ttu-id="66119-187">Kaynak bilgilerini ayarlama: kaynak kimliği ve işlemi: okuma, yazma, ÇALıŞTıRıLABILIR.</span><span class="sxs-lookup"><span data-stu-id="66119-187">Set resource info: resource id and operation: READ, WRITE, EXECUTABLE.</span></span> |
| <span data-ttu-id="66119-188">***nx_lwm2m_client_resource_string_set***</span><span class="sxs-lookup"><span data-stu-id="66119-188">***nx_lwm2m_client_resource_string_set***</span></span> | <span data-ttu-id="66119-189">Kaynak değerini dize olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-189">Set the resource value as string.</span></span> |
| <span data-ttu-id="66119-190">***nx_lwm2m_client_resource_integer32_set***</span><span class="sxs-lookup"><span data-stu-id="66119-190">***nx_lwm2m_client_resource_integer32_set***</span></span> | <span data-ttu-id="66119-191">Kaynak değerini 32 bitlik bir tamsayı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-191">Set the resource value as 32-Bit integer.</span></span> |
| <span data-ttu-id="66119-192">***nx_lwm2m_client_resource_integer64_set***</span><span class="sxs-lookup"><span data-stu-id="66119-192">***nx_lwm2m_client_resource_integer64_set***</span></span> | <span data-ttu-id="66119-193">Kaynak değerini 64 bitlik bir tamsayı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-193">Set the resource value as 64-Bit integer.</span></span> |
| <span data-ttu-id="66119-194">***nx_lwm2m_client_resource_float32_set***</span><span class="sxs-lookup"><span data-stu-id="66119-194">***nx_lwm2m_client_resource_float32_set***</span></span> | <span data-ttu-id="66119-195">Kaynak değerini 32-bit float olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-195">Set the resource value as 32-Bit float.</span></span> |
| <span data-ttu-id="66119-196">***nx_lwm2m_client_resource_float64_set***</span><span class="sxs-lookup"><span data-stu-id="66119-196">***nx_lwm2m_client_resource_float64_set***</span></span> | <span data-ttu-id="66119-197">Kaynak değerini 64-bit float olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-197">Set the resource value as 64-Bit float.</span></span> |
| <span data-ttu-id="66119-198">***nx_lwm2m_client_resource_boolean_set***</span><span class="sxs-lookup"><span data-stu-id="66119-198">***nx_lwm2m_client_resource_boolean_set***</span></span> | <span data-ttu-id="66119-199">Kaynak değerini Boole olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-199">Set the resource value as boolean.</span></span> |
| <span data-ttu-id="66119-200">***nx_lwm2m_client_resource_objlnk_set***</span><span class="sxs-lookup"><span data-stu-id="66119-200">***nx_lwm2m_client_resource_objlnk_set***</span></span> | <span data-ttu-id="66119-201">Kaynak değerini nesne bağlantısı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-201">Set the resource value as object link.</span></span> |
| <span data-ttu-id="66119-202">***nx_lwm2m_client_resource_opaque_set***</span><span class="sxs-lookup"><span data-stu-id="66119-202">***nx_lwm2m_client_resource_opaque_set***</span></span> | <span data-ttu-id="66119-203">Kaynak değerini donuk olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-203">Set the resource value as opaque.</span></span> |
| <span data-ttu-id="66119-204">***nx_lwm2m_client_resource_instance_set***</span><span class="sxs-lookup"><span data-stu-id="66119-204">***nx_lwm2m_client_resource_instance_set***</span></span> | <span data-ttu-id="66119-205">Birden çok kaynak için kaynak değerini örnek olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-205">Set the resource value as instance for multiple resource.</span></span> |
| <span data-ttu-id="66119-206">***nx_lwm2m_client_resource_dim_set***</span><span class="sxs-lookup"><span data-stu-id="66119-206">***nx_lwm2m_client_resource_dim_set***</span></span> | <span data-ttu-id="66119-207">Bulma için birden çok kaynak için kaynak boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66119-207">Set the resource dimension for multiple resource for discover.</span></span> |

<span data-ttu-id="66119-208">Kaynak bilgilerini ve değerini almak için aşağıdaki işlevler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66119-208">The following functions are provided for getting resource info and value.</span></span>

| <span data-ttu-id="66119-209">İşlev &nbsp; adı</span><span class="sxs-lookup"><span data-stu-id="66119-209">Function&nbsp;Name</span></span> | <span data-ttu-id="66119-210">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-210">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-211">***nx_lwm2m_client_resource_info_get***</span><span class="sxs-lookup"><span data-stu-id="66119-211">***nx_lwm2m_client_resource_info_get***</span></span> | <span data-ttu-id="66119-212">Kaynak bilgilerini al: kaynak kimliği ve işlemi: okuma, yazma, ÇALıŞTıRıLABILIR.</span><span class="sxs-lookup"><span data-stu-id="66119-212">Get resource info: resource id and operation: READ, WRITE, EXECUTABLE.</span></span> |
| <span data-ttu-id="66119-213">***nx_lwm2m_client_resource_string_get***</span><span class="sxs-lookup"><span data-stu-id="66119-213">***nx_lwm2m_client_resource_string_get***</span></span> | <span data-ttu-id="66119-214">Bir dize kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="66119-214">Get the value of a string resource.</span></span> |
| <span data-ttu-id="66119-215">***nx_lwm2m_client_resource_integer32_get***</span><span class="sxs-lookup"><span data-stu-id="66119-215">***nx_lwm2m_client_resource_integer32_get***</span></span> | <span data-ttu-id="66119-216">32 bitlik bir tamsayı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="66119-216">Get the value of a 32-Bit integer resource.</span></span> |
| <span data-ttu-id="66119-217">***nx_lwm2m_client_resource_integer64_get***</span><span class="sxs-lookup"><span data-stu-id="66119-217">***nx_lwm2m_client_resource_integer64_get***</span></span> | <span data-ttu-id="66119-218">B4 bitlik bir tamsayı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="66119-218">Get the value of a b4-Bit integer resource.</span></span> |
| <span data-ttu-id="66119-219">***nx_lwm2m_client_resource_float32_get***</span><span class="sxs-lookup"><span data-stu-id="66119-219">***nx_lwm2m_client_resource_float32_get***</span></span> | <span data-ttu-id="66119-220">32 bitlik bir float kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="66119-220">Get the value of a 32-Bit float resource.</span></span> |
| <span data-ttu-id="66119-221">***nx_lwm2m_client_resource_float64_get***</span><span class="sxs-lookup"><span data-stu-id="66119-221">***nx_lwm2m_client_resource_float64_get***</span></span> | <span data-ttu-id="66119-222">64 bitlik bir float kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="66119-222">Get the value of a 64-Bit float resource.</span></span> |
| <span data-ttu-id="66119-223">***nx_lwm2m_client_resource_boolean_get***</span><span class="sxs-lookup"><span data-stu-id="66119-223">***nx_lwm2m_client_resource_boolean_get***</span></span> | <span data-ttu-id="66119-224">Boole kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="66119-224">Get the value of a Boolean resource.</span></span> |
| <span data-ttu-id="66119-225">***nx_lwm2m_client_resource_objlnk_get***</span><span class="sxs-lookup"><span data-stu-id="66119-225">***nx_lwm2m_client_resource_objlnk_get***</span></span> | <span data-ttu-id="66119-226">Bir nesne bağlantı kaynağının değerini alır.</span><span class="sxs-lookup"><span data-stu-id="66119-226">Get the value of an object link resource.</span></span> |
| <span data-ttu-id="66119-227">***nx_lwm2m_client_resource_opaque_get***</span><span class="sxs-lookup"><span data-stu-id="66119-227">***nx_lwm2m_client_resource_opaque_get***</span></span> | <span data-ttu-id="66119-228">Donuk bir kaynağın değerini alın.</span><span class="sxs-lookup"><span data-stu-id="66119-228">Get the value of an opaque resource.</span></span> |
| <span data-ttu-id="66119-229">***nx_lwm2m_client_resource_instance_get***</span><span class="sxs-lookup"><span data-stu-id="66119-229">***nx_lwm2m_client_resource_instance_get***</span></span> | <span data-ttu-id="66119-230">Birden çok kaynak için kaynak örneğini alın.</span><span class="sxs-lookup"><span data-stu-id="66119-230">Get the resource instance for multiple resource.</span></span> |
| <span data-ttu-id="66119-231">***nx_lwm2m_client_resource_dim_get***</span><span class="sxs-lookup"><span data-stu-id="66119-231">***nx_lwm2m_client_resource_dim_get***</span></span> | <span data-ttu-id="66119-232">Birden çok kaynak için kaynak boyutunu alın.</span><span class="sxs-lookup"><span data-stu-id="66119-232">Get the resource dimension for multiple resource.</span></span> |

## <a name="object-implementation"></a><span data-ttu-id="66119-233">Nesne uygulama</span><span class="sxs-lookup"><span data-stu-id="66119-233">Object Implementation</span></span>

<span data-ttu-id="66119-234">LWM2M Istemcisi zorunlu OMA LWM2M nesnelerini uygular: güvenlik (0), sunucu (1), Access Control (2) ve cihaz (3).</span><span class="sxs-lookup"><span data-stu-id="66119-234">The LWM2M Client implements the mandatory OMA LWM2M Objects: Security (0), Server (1), Access Control (2) and Device (3).</span></span> <span data-ttu-id="66119-235">Diğer cihaza özgü nesnelerin uygulama tarafından uygulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="66119-235">Other device specific objects must be implemented by the application.</span></span>

<span data-ttu-id="66119-236">Bir nesneyi tanımlamak için iki veri yapısı kullanılır: NX_LWM2M_CLIENT_OBJECT yapısı, nesne KIMLIĞI ve nesne yöntemleri de dahil olmak üzere nesne uygulamasını tanımlar ve NX_LWM2M_CLIENT_OBJECT_INSTANCE yapısı bir nesne örneğinin verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="66119-236">Two data structures are used to define an Object: the NX_LWM2M_CLIENT_OBJECT structure defines the Object implementation, including the Object ID and the object methods, and the NX_LWM2M_CLIENT_OBJECT_INSTANCE structure contains the data of an Object Instance.</span></span>

<span data-ttu-id="66119-237">Aşağıdaki işlevler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66119-237">The following functions are provided.</span></span>

| <span data-ttu-id="66119-238">İşlev &nbsp; adı</span><span class="sxs-lookup"><span data-stu-id="66119-238">Function&nbsp;Name</span></span> | <span data-ttu-id="66119-239">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-240">***nx_lwm2m_client_object_add***</span><span class="sxs-lookup"><span data-stu-id="66119-240">***nx_lwm2m_client_object_add***</span></span> | <span data-ttu-id="66119-241">LwM2M Istemcisine nesne uygulamasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="66119-241">Add object implementation to the LwM2M Client.</span></span> |
| <span data-ttu-id="66119-242">***nx_lwm2m_client_object_remove***</span><span class="sxs-lookup"><span data-stu-id="66119-242">***nx_lwm2m_client_object_remove***</span></span> | <span data-ttu-id="66119-243">LwM2M Istemcisinden nesne uygulamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="66119-243">Remove object implementation from the LwM2M Client.</span></span> |
| <span data-ttu-id="66119-244">***nx_lwm2m_client_object_instance_add***</span><span class="sxs-lookup"><span data-stu-id="66119-244">***nx_lwm2m_client_object_instance_add***</span></span> | <span data-ttu-id="66119-245">Nesneye nesne örneği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="66119-245">Add object instance to the Object.</span></span> |
| <span data-ttu-id="66119-246">***nx_lwm2m_client_object_instance_remove***</span><span class="sxs-lookup"><span data-stu-id="66119-246">***nx_lwm2m_client_object_instance_remove***</span></span> | <span data-ttu-id="66119-247">Nesne örneğini nesneden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="66119-247">Remove object instance from the Object.</span></span> |

<span data-ttu-id="66119-248">Nesne yöntemi geri çağırma işlevinin aşağıda gösterilen imzası vardır.</span><span class="sxs-lookup"><span data-stu-id="66119-248">The object method callback function has signature shown below.</span></span>

```c
typedef UINT (*NX_LWM2M_CLIENT_OBJECT_OPERATION_CALLBACK)(
    UINT operation, 
    NX_LWM2M_CLIENT_OBJECT *object_ptr,
    NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr,
    NX_LWM2M_CLIENT_RESOURCE *resource,
    UINT *resource_count,
    VOID *args_ptr,
    UINT args_length);
```

### <a name="the-read-method"></a><span data-ttu-id="66119-249">' Read ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="66119-249">The ‘Read’ Method</span></span>

<span data-ttu-id="66119-250">' Read ' yöntemi, kaynak değerlerini bir nesne örneğinden okumak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66119-250">The ‘Read’ method is used to read Resource values from an Object Instance.</span></span> <span data-ttu-id="66119-251">Parametreleri aşağıdaki gibi tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="66119-251">The parameters are defined as follows.</span></span>

| <span data-ttu-id="66119-252">Parametre</span><span class="sxs-lookup"><span data-stu-id="66119-252">Parameter</span></span> | <span data-ttu-id="66119-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-253">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-254">**çalışmasını**</span><span class="sxs-lookup"><span data-stu-id="66119-254">**operation**</span></span> | <span data-ttu-id="66119-255">**NX_LWM2M_CLIENT_OBJECT_READ**</span><span class="sxs-lookup"><span data-stu-id="66119-255">**NX_LWM2M_CLIENT_OBJECT_READ**</span></span> |
| <span data-ttu-id="66119-256">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-256">**object_ptr**</span></span> | <span data-ttu-id="66119-257">Nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-257">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="66119-258">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-258">**instance_ptr**</span></span> | <span data-ttu-id="66119-259">Nesne örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="66119-259">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="66119-260">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="66119-260">**resource**</span></span> | <span data-ttu-id="66119-261">Okunacak kaynakların kimliklerini içeren **NX_LWM2M_CLIENT_RESOURCE** dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-261">Pointer to an array of **NX_LWM2M_CLIENT_RESOURCE** containing the IDs of the resources to read.</span></span> <span data-ttu-id="66119-262">Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="66119-262">On return the array is filled with corresponding types and values.</span></span> |
| <span data-ttu-id="66119-263">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="66119-263">**resource_count**</span></span> | <span data-ttu-id="66119-264">Okunacak kaynak sayısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-264">Pointer to the number of resources to read.</span></span> |
| <span data-ttu-id="66119-265">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-265">**args_ptr**</span></span> | <span data-ttu-id="66119-266">Okuma için kullanılmayan parametre.</span><span class="sxs-lookup"><span data-stu-id="66119-266">Unused parameter for read.</span></span> |
| <span data-ttu-id="66119-267">**args_length**</span><span class="sxs-lookup"><span data-stu-id="66119-267">**args_length**</span></span> | <span data-ttu-id="66119-268">Okuma için kullanılmayan parametre.</span><span class="sxs-lookup"><span data-stu-id="66119-268">Unused parameter for read.</span></span> |

### <a name="the-discover-method"></a><span data-ttu-id="66119-269">' Keşfet ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="66119-269">The ‘Discover’ Method</span></span>

<span data-ttu-id="66119-270">' Keşfet ' yöntemi, bir nesne tarafından uygulanan tüm kaynakların listesini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66119-270">The ‘Discover’ method is used to retrieve the list of all Resources implemented by an Object.</span></span> <span data-ttu-id="66119-271">Parametreleri aşağıdaki gibi tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="66119-271">The parameters are defined as follows.</span></span>

| <span data-ttu-id="66119-272">Parametre</span><span class="sxs-lookup"><span data-stu-id="66119-272">Parameter</span></span> | <span data-ttu-id="66119-273">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-273">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-274">**çalışmasını**</span><span class="sxs-lookup"><span data-stu-id="66119-274">**operation**</span></span> | <span data-ttu-id="66119-275">**NX_LWM2M_CLIENT_OBJECT_DISCOVER**</span><span class="sxs-lookup"><span data-stu-id="66119-275">**NX_LWM2M_CLIENT_OBJECT_DISCOVER**</span></span> |
| <span data-ttu-id="66119-276">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-276">**object_ptr**</span></span> | <span data-ttu-id="66119-277">Nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-277">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="66119-278">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-278">**instance_ptr**</span></span> | <span data-ttu-id="66119-279">Nesne örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="66119-279">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="66119-280">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="66119-280">**resource**</span></span> | <span data-ttu-id="66119-281">NX_LWM2M_CLIENT_RESOURCE dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-281">Pointer to an array of NX_LWM2M_CLIENT_RESOURCE.</span></span> <span data-ttu-id="66119-282">Dönüş sırasında dizi karşılık gelen kaynak bilgileriyle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="66119-282">On return the array is filled with corresponding resource info.</span></span> |
| <span data-ttu-id="66119-283">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="66119-283">**resource_count**</span></span> | <span data-ttu-id="66119-284">Bulunacak kaynak sayısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-284">Pointer to the number of resources to discover.</span></span> <span data-ttu-id="66119-285">Dönüş sırasında bu parametrenin doğru değer olarak güncellenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="66119-285">On return this parameter must be updated as the true value.</span></span> |
| <span data-ttu-id="66119-286">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-286">**args_ptr**</span></span> | <span data-ttu-id="66119-287">Bulma için kullanılmamış parametre.</span><span class="sxs-lookup"><span data-stu-id="66119-287">Unused parameter for discover.</span></span> |
| <span data-ttu-id="66119-288">**args_length**</span><span class="sxs-lookup"><span data-stu-id="66119-288">**args_length**</span></span> | <span data-ttu-id="66119-289">Bulma için kullanılmamış parametre.</span><span class="sxs-lookup"><span data-stu-id="66119-289">Unused parameter for discover.</span></span> |

### <a name="the-write-method"></a><span data-ttu-id="66119-290">' Write ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="66119-290">The ‘Write’ Method</span></span>

<span data-ttu-id="66119-291">' Write ' yöntemi, bir nesne örneğinin kaynaklarını güncelleştirmek veya değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66119-291">The ‘Write’ method is used to update or replace resources of an Object Instance.</span></span> <span data-ttu-id="66119-292">Parametreleri aşağıdaki gibi tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="66119-292">The parameters are defined as follows.</span></span>

| <span data-ttu-id="66119-293">Parametre</span><span class="sxs-lookup"><span data-stu-id="66119-293">Parameter</span></span>  | <span data-ttu-id="66119-294">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-294">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-295">**çalışmasını**</span><span class="sxs-lookup"><span data-stu-id="66119-295">**operation**</span></span> | <span data-ttu-id="66119-296">**NX_LWM2M_CLIENT_OBJECT_WRITE**</span><span class="sxs-lookup"><span data-stu-id="66119-296">**NX_LWM2M_CLIENT_OBJECT_WRITE**</span></span> |
| <span data-ttu-id="66119-297">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-297">**object_ptr**</span></span> | <span data-ttu-id="66119-298">Nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-298">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="66119-299">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-299">**instance_ptr**</span></span> | <span data-ttu-id="66119-300">Nesne örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="66119-300">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="66119-301">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="66119-301">**resource**</span></span> | <span data-ttu-id="66119-302">Okunacak kaynakların kimliklerini içeren **NX_LWM2M_CLIENT_RESOURCE** dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-302">Pointer to an array of **NX_LWM2M_CLIENT_RESOURCE** containing the IDs of the resources to read.</span></span> <span data-ttu-id="66119-303">Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="66119-303">On return the array is filled with corresponding types and values.</span></span> |
| <span data-ttu-id="66119-304">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="66119-304">**resource_count**</span></span> | <span data-ttu-id="66119-305">Bulunacak kaynak sayısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-305">Pointer to the number of resources to discover.</span></span> |
| <span data-ttu-id="66119-306">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-306">**args_ptr**</span></span> | <span data-ttu-id="66119-307">Yazma bayrakları.</span><span class="sxs-lookup"><span data-stu-id="66119-307">Write flags.</span></span> |
| <span data-ttu-id="66119-308">**args_length**</span><span class="sxs-lookup"><span data-stu-id="66119-308">**args_length**</span></span> | <span data-ttu-id="66119-309">Bağımsız değişkenlerin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="66119-309">The length of the arguments.</span></span> |

<span data-ttu-id="66119-310">Aşağıdaki yazma işlemleri *bayrak* parametresine belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="66119-310">The following write operations can be specified to the *flag* parameter.</span></span>

| <span data-ttu-id="66119-311">İşlem</span><span class="sxs-lookup"><span data-stu-id="66119-311">Operation</span></span> | <span data-ttu-id="66119-312">Eylem</span><span class="sxs-lookup"><span data-stu-id="66119-312">Action</span></span> | <span data-ttu-id="66119-313">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-313">Description</span></span> |
| --- | ---| --- |
| <span data-ttu-id="66119-314">0</span><span class="sxs-lookup"><span data-stu-id="66119-314">0</span></span> | <span data-ttu-id="66119-315">Kısmi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="66119-315">Partial Update</span></span> | <span data-ttu-id="66119-316">Yeni değerde belirtilen kaynakları ekler veya güncelleştirir ve diğer mevcut kaynakları değişmeden bırakır.</span><span class="sxs-lookup"><span data-stu-id="66119-316">Adds or updates Resources provided in the new value and leaves other existing Resources unchanged.</span></span>
| <span data-ttu-id="66119-317">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE**</span><span class="sxs-lookup"><span data-stu-id="66119-317">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_INSTANCE**</span></span> | <span data-ttu-id="66119-318">Örneği Değiştir</span><span class="sxs-lookup"><span data-stu-id="66119-318">Replace Instance</span></span> | <span data-ttu-id="66119-319">Nesne örneğini, belirtilen yeni kaynak değerleriyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="66119-319">Replaces the Object Instance with the new provided resource values.</span></span>
| <span data-ttu-id="66119-320">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE**</span><span class="sxs-lookup"><span data-stu-id="66119-320">**NX_LWM2M_CLIENT_OBJECT_WRITE_REPLACE_RESOURCE**</span></span> |  <span data-ttu-id="66119-321">Kaynağı değiştir</span><span class="sxs-lookup"><span data-stu-id="66119-321">Replace Resource</span></span> | <span data-ttu-id="66119-322">Kaynakları, belirtilen yeni kaynak değerleriyle (birden çok kaynağı değiştirmek için kullanılır) değiştirir.</span><span class="sxs-lookup"><span data-stu-id="66119-322">Replaces the Resources with the new provided resource values (used to replace Multiple Resources).</span></span> |
| <span data-ttu-id="66119-323">**NX_LWM2M_CLIENT_OBJECT_WRITE_CREATE**</span><span class="sxs-lookup"><span data-stu-id="66119-323">**NX_LWM2M_CLIENT_OBJECT_WRITE_CREATE**</span></span> | <span data-ttu-id="66119-324">Örnek Oluştur</span><span class="sxs-lookup"><span data-stu-id="66119-324">Create Instance</span></span> | <span data-ttu-id="66119-325">Yeni oluşturulan nesne örneğini, belirtilen kaynak değerleriyle ( **_nx_lwm2m_object_create_** yönteminden çağırılır) başlatır.</span><span class="sxs-lookup"><span data-stu-id="66119-325">Initializes the newly created Object Instance with the provided resource values (called from the **_nx_lwm2m_object_create_** method).</span></span> |
| <span data-ttu-id="66119-326">**NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP**</span><span class="sxs-lookup"><span data-stu-id="66119-326">**NX_LWM2M_CLIENT_OBJECT_WRITE_BOOTSTRAP**</span></span> | <span data-ttu-id="66119-327">Önyükleme yazma</span><span class="sxs-lookup"><span data-stu-id="66119-327">Bootstrap Write</span></span> | <span data-ttu-id="66119-328">Önyükleme sırası sırasında çağırılır.</span><span class="sxs-lookup"><span data-stu-id="66119-328">Called during Bootstrap sequence.</span></span> |

### <a name="the-execute-method"></a><span data-ttu-id="66119-329">' Execute ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="66119-329">The ‘Execute’ Method</span></span>

<span data-ttu-id="66119-330">' Execute ' yöntemi, bir nesne kaynağının yürütülmesini uygular.</span><span class="sxs-lookup"><span data-stu-id="66119-330">The ‘Execute’ method implements the execution of an Object Resource.</span></span>

<span data-ttu-id="66119-331">Giriş parametreleri aşağıdaki gibi tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="66119-331">The input parameters are defined as follows.</span></span>

| <span data-ttu-id="66119-332">Parametre</span><span class="sxs-lookup"><span data-stu-id="66119-332">Parameter</span></span>  | <span data-ttu-id="66119-333">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-333">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-334">**çalışmasını**</span><span class="sxs-lookup"><span data-stu-id="66119-334">**operation**</span></span> | <span data-ttu-id="66119-335">NX_LWM2M_CLIENT_OBJECT_EXECUTE</span><span class="sxs-lookup"><span data-stu-id="66119-335">NX_LWM2M_CLIENT_OBJECT_EXECUTE</span></span> |
| <span data-ttu-id="66119-336">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-336">**object_ptr**</span></span> | <span data-ttu-id="66119-337">Nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-337">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="66119-338">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-338">**instance_ptr**</span></span> | <span data-ttu-id="66119-339">Nesne örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="66119-339">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="66119-340">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="66119-340">**resource**</span></span> | <span data-ttu-id="66119-341">Okunacak kaynakların kimliklerini içeren **NX_LWM2M_CLIENT_RESOURCE** dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-341">Pointer to an array of **NX_LWM2M_CLIENT_RESOURCE** containing the IDs of the resources to read.</span></span> <span data-ttu-id="66119-342">Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="66119-342">On return the array is filled with corresponding types and values.</span></span> |
| <span data-ttu-id="66119-343">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="66119-343">**resource_count**</span></span> | <span data-ttu-id="66119-344">Bulunacak kaynak sayısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-344">Pointer to the number of resources to discover.</span></span> |
| <span data-ttu-id="66119-345">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-345">**args_ptr**</span></span> | <span data-ttu-id="66119-346">Bağımsız değişkenlerin işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="66119-346">Pointer to the arguments.</span></span> |
| <span data-ttu-id="66119-347">**args_length**</span><span class="sxs-lookup"><span data-stu-id="66119-347">**args_length**</span></span> | <span data-ttu-id="66119-348">Bağımsız değişkenlerin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="66119-348">The length of the arguments.</span></span>  |

<span data-ttu-id="66119-349">Kaynak KIMLIĞI yoksa işlevin **NX_LWM2M_CLIENT_NOT_FOUND** döndürmesi veya yürütmeyi desteklememesi durumunda **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** gerekir.</span><span class="sxs-lookup"><span data-stu-id="66119-349">The function must return **NX_LWM2M_CLIENT_NOT_FOUND** if the Resource ID doesn’t exist, or **NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED** if it doesn’t support execution.</span></span>

### <a name="the-create-method"></a><span data-ttu-id="66119-350">' Create ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="66119-350">The ‘Create’ Method</span></span>

<span data-ttu-id="66119-351">' Create ' yöntemi, yeni bir nesne örneği oluşturulmasını uygular.</span><span class="sxs-lookup"><span data-stu-id="66119-351">The ‘Create’ method implements the creation of a new Object Instance.</span></span>

<span data-ttu-id="66119-352">Giriş parametreleri aşağıdaki gibi tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="66119-352">The input parameters are defined as follows.</span></span>

| <span data-ttu-id="66119-353">Parametre</span><span class="sxs-lookup"><span data-stu-id="66119-353">Parameter</span></span>  | <span data-ttu-id="66119-354">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-355">**çalışmasını**</span><span class="sxs-lookup"><span data-stu-id="66119-355">**operation**</span></span> | <span data-ttu-id="66119-356">**NX_LWM2M_CLIENT_OBJECT_CREATE**</span><span class="sxs-lookup"><span data-stu-id="66119-356">**NX_LWM2M_CLIENT_OBJECT_CREATE**</span></span> |
| <span data-ttu-id="66119-357">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-357">**object_ptr**</span></span> | <span data-ttu-id="66119-358">Nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-358">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="66119-359">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-359">**instance_ptr**</span></span> | <span data-ttu-id="66119-360">Kullanılmayan parametre.</span><span class="sxs-lookup"><span data-stu-id="66119-360">Unused parameter.</span></span> |
| <span data-ttu-id="66119-361">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="66119-361">**resource**</span></span> | <span data-ttu-id="66119-362">Okunacak kaynakların kimliklerini içeren **NX_LWM2M_CLIENT_RESOURCE** dizisine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-362">Pointer to an array of **NX_LWM2M_CLIENT_RESOURCE** containing the IDs of the resources to read.</span></span> <span data-ttu-id="66119-363">Dönüş sırasında dizi karşılık gelen türler ve değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="66119-363">On return the array is filled with corresponding types and values.</span></span> |
| <span data-ttu-id="66119-364">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="66119-364">**resource_count**</span></span> | <span data-ttu-id="66119-365">Bulunacak kaynak sayısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-365">Pointer to the number of resources to discover.</span></span> |
| <span data-ttu-id="66119-366">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-366">**args_ptr**</span></span> | <span data-ttu-id="66119-367">Nesne örneği kimliği.</span><span class="sxs-lookup"><span data-stu-id="66119-367">Object instance id.</span></span> |
| <span data-ttu-id="66119-368">**args_length**</span><span class="sxs-lookup"><span data-stu-id="66119-368">**args_length**</span></span> | <span data-ttu-id="66119-369">Bağımsız değişkenlerin uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="66119-369">The length of the arguments.</span></span> |

### <a name="the-delete-method"></a><span data-ttu-id="66119-370">' DELETE ' yöntemi</span><span class="sxs-lookup"><span data-stu-id="66119-370">The ‘Delete’ Method</span></span>

<span data-ttu-id="66119-371">' DELETE ' yöntemi bir nesne örneğinin silinmesini uygular, giriş parametreleri aşağıdaki gibi tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="66119-371">The ‘Delete’ method implements the deletion of an object instance, the input parameters are defined as follows.</span></span>

| <span data-ttu-id="66119-372">Parametre</span><span class="sxs-lookup"><span data-stu-id="66119-372">Parameter</span></span>  | <span data-ttu-id="66119-373">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66119-373">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66119-374">**çalışmasını**</span><span class="sxs-lookup"><span data-stu-id="66119-374">**operation**</span></span> | <span data-ttu-id="66119-375">NX_LWM2M_CLIENT_OBJECT_DELETE</span><span class="sxs-lookup"><span data-stu-id="66119-375">NX_LWM2M_CLIENT_OBJECT_DELETE</span></span> |
| <span data-ttu-id="66119-376">**object_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-376">**object_ptr**</span></span> | <span data-ttu-id="66119-377">Nesne uygulamasına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="66119-377">Pointer to the Object implementation.</span></span> |
| <span data-ttu-id="66119-378">**instance_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-378">**instance_ptr**</span></span> | <span data-ttu-id="66119-379">Nesne örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="66119-379">Pointer to the Object Instance.</span></span> |
| <span data-ttu-id="66119-380">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="66119-380">**resource**</span></span> | <span data-ttu-id="66119-381">Kullanılmayan parametre.</span><span class="sxs-lookup"><span data-stu-id="66119-381">Unused parameter.</span></span> |
| <span data-ttu-id="66119-382">**resource_count**</span><span class="sxs-lookup"><span data-stu-id="66119-382">**resource_count**</span></span> | <span data-ttu-id="66119-383">Kullanılmayan parametre.</span><span class="sxs-lookup"><span data-stu-id="66119-383">Unused parameter.</span></span> |
| <span data-ttu-id="66119-384">**args_ptr**</span><span class="sxs-lookup"><span data-stu-id="66119-384">**args_ptr**</span></span> | <span data-ttu-id="66119-385">Kullanılmayan parametre.</span><span class="sxs-lookup"><span data-stu-id="66119-385">Unused parameter.</span></span> |
| <span data-ttu-id="66119-386">**args_length**</span><span class="sxs-lookup"><span data-stu-id="66119-386">**args_length**</span></span> | <span data-ttu-id="66119-387">Kullanılmayan parametre.</span><span class="sxs-lookup"><span data-stu-id="66119-387">Unused parameter.</span></span> |

<span data-ttu-id="66119-388">Başarılı olduğunda, nesne örnek verilerini ve örnek tarafından ayrılan diğer kaynakları serbest bırakmalıdır.</span><span class="sxs-lookup"><span data-stu-id="66119-388">On success the Object must release the Object Instance data and any other resource allocated by the instance.</span></span>

## <a name="example-of-lwm2m-client-application"></a><span data-ttu-id="66119-389">LWM2M Istemci uygulaması örneği</span><span class="sxs-lookup"><span data-stu-id="66119-389">Example of LWM2M Client Application</span></span>

<span data-ttu-id="66119-390">Aşağıdaki kod, bir sıcaklık sensörden ve hafif anahtardan oluşan özel bir cihaz uygulayan basit bir LWM2M Istemci uygulamasına bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="66119-390">The following code is an example of a simple LWM2M Client Application which implements a custom device consisting of a temperature sensor and a light switch.</span></span>

<span data-ttu-id="66119-391">Cihaz, bir sunucunun ısı algılayıcısı değerini ve ışık anahtarının Boole durumunu okumasına izin verir ve ışığı açık/kapalı olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="66119-391">The device allows a server to read the value of the temperature sensor and the boolean state of the light switch, and to set the light switch to on/off.</span></span>

```c
#include "nx_lwm2m_client.h"


/* Custom Object implementation. */

/* Temperature Object ID and resource IDs. */
#define IPSO_TEMPERATURE_OBJECT_ID   3303

#define IPSO_RESOURCE_MIN_VALUE      5601
#define IPSO_RESOURCE_MAX_VALUE      5602
#define IPSO_RESOURCE_RESET_MINMAX   5605
#define IPSO_RESOURCE_VALUE          5700
#define IPSO_RESOURCE_UNITS          5701

/* Actuation Object ID and resource IDs. */
#define IPSO_ACTUATION_OBJECT_ID     3306

#define IPSO_RESOURCE_ONOFF          5850

/* Define the Temperature Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_CLIENT_OBJECT_INSTANCE    object_instance;

    /* Resources Data */
    NX_LWM2M_FLOAT32                   temperature;
    NX_LWM2M_FLOAT32                   min_temperature;
    NX_LWM2M_FLOAT32                   max_temperature;

} IPSO_TEMPERATURE_INSTANCE;

/* Define the Actuation Object Instance structure */
typedef struct
{
    /* The LWM2M Object Instance */
    NX_LWM2M_CLIENT_OBJECT_INSTANCE    object_instance;

    /* Resources Data */
    NX_LWM2M_BOOL                      onoff;

} IPSO_ACTUATION_INSTANCE;

/* IPSO Temperature */
/* Define the 'Read' Method */
UINT ipso_temperature_read(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count)
{
IPSO_TEMPERATURE_INSTANCE *temp = ((IPSO_TEMPERATURE_INSTANCE *) instance_ptr);
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_MIN_VALUE:

            /* return the minimum measured temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> min_temperature);
            break;

        case IPSO_RESOURCE_MAX_VALUE:

            /* return the maximum measured temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> max_temperature);
            break;

        case IPSO_RESOURCE_VALUE:

            /* return the temperature value */
            nx_lwm2m_client_resource_float32_set(&resource[i], temp -> temperature);
            break;

        case IPSO_RESOURCE_RESET_MINMAX:

            /* Not readable */
            return(NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED);

        case IPSO_RESOURCE_UNITS:

            /* return the temperature units */
            nx_lwm2m_client_resource_string_set(&resource[i], "Cel", 3);
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}

/* Define the 'Discover' method */
UINT ipso_temperature_discover(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resources, UINT *resource_count)
{
    if (*resource_count < 5)
    {
        return(NX_LWM2M_CLIENT_BUFFER_TOO_SMALL);
    }

    /* return the list of supported resources IDs */
    *resource_count = 5;
    nx_lwm2m_client_resource_info_set(&resources[0], IPSO_RESOURCE_MIN_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[1], IPSO_RESOURCE_MAX_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[2], IPSO_RESOURCE_RESET_MINMAX, NX_LWM2M_CLIENT_RESOURCE_OPERATION_EXECUTABLE);
    nx_lwm2m_client_resource_info_set(&resources[3], IPSO_RESOURCE_VALUE, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);
    nx_lwm2m_client_resource_info_set(&resources[4], IPSO_RESOURCE_UNITS, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ);

    return(NX_SUCCESS);
}

/* Define the 'Execute' method */
UINT ipso_temperature_execute(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, const CHAR *args_ptr, UINT args_length)
{
IPSO_TEMPERATURE_INSTANCE *temp = ((IPSO_TEMPERATURE_INSTANCE *) instance_ptr);
NX_LWM2M_CLIENT_RESOURCE value;
NX_LWM2M_ID resource_id;

    /* Get resource id */
    nx_lwm2m_client_resource_info_get(resource, &resource_id, NX_NULL);

    switch (resource_id)
    {

    case IPSO_RESOURCE_MIN_VALUE:
    case IPSO_RESOURCE_MAX_VALUE:
    case IPSO_RESOURCE_VALUE:
    case IPSO_RESOURCE_UNITS:

        /* read-only resource */
        return(NX_LWM2M_CLIENT_METHOD_NOT_ALLOWED);

    case IPSO_RESOURCE_RESET_MINMAX:

        /* reset min/max values to current temperature */
        nx_lwm2m_client_resource_float32_set(&value, temp -> temperature);
        if (temp -> min_temperature != temp -> temperature)
        {
            temp -> min_temperature = temp -> temperature;
            nx_lwm2m_client_resource_info_set(&value, IPSO_RESOURCE_MIN_VALUE, NX_NULL);
            nx_lwm2m_client_object_resource_changed(object_ptr, instance_ptr, &value);
        }
        if (temp -> max_temperature != temp -> temperature)
        {
            temp -> max_temperature = temp -> temperature;
            nx_lwm2m_client_resource_info_set(&value, IPSO_RESOURCE_MAX_VALUE, NX_NULL);
            nx_lwm2m_client_object_resource_changed(object_ptr, instance_ptr, &value);
        }

        break;

    default:

        /* unknown resource ID */
        return(NX_LWM2M_CLIENT_NOT_FOUND);
    }

    return(NX_SUCCESS);
}

/* Define the operation callback function of Temperature Object */
UINT ipso_temperature_operation(UINT operation, NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT *resource_count, VOID *args_ptr, UINT args_length)
{

    switch (operation)
    {
    case NX_LWM2M_CLIENT_OBJECT_READ:

        /* Call read function */
        return ipso_temperature_read(object_ptr, object_instance_ptr, resource, *resource_count);
    case NX_LWM2M_CLIENT_OBJECT_DISCOVER:

        /* Call discover function */
        return ipso_temperature_discover(object_ptr, object_instance_ptr, resource, resource_count);

    case NX_LWM2M_CLIENT_OBJECT_EXECUTE:

        /* Call execute function */
        return ipso_temperature_execute(object_ptr, object_instance_ptr, resource, args_ptr, args_length);
    default:

        /*Unsupported operation */
        return(NX_LWM2M_CLIENT_NOT_SUPPORTED);
    }
}


/* IPSO Actuation */
/* Define the 'Read' Method */
UINT ipso_actuation_read(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count)
{
IPSO_ACTUATION_INSTANCE *act = ((IPSO_ACTUATION_INSTANCE *) instance_ptr);
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_ONOFF:

            /* return the on/off value */
            nx_lwm2m_client_resource_boolean_set(&resource[i], act -> onoff);
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}


/* Define the 'Discover' method */
UINT ipso_actuation_discover(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resources, UINT *resource_count)
{
    if (*resource_count < 1)
    {
        return(NX_LWM2M_CLIENT_BUFFER_TOO_SMALL);
    }

    /* return the list of supported resources IDs */
    *resource_count = 1;
    nx_lwm2m_client_resource_info_set(&resources[0], IPSO_RESOURCE_ONOFF, NX_LWM2M_CLIENT_RESOURCE_OPERATION_READ_WRITE);

    return(NX_SUCCESS);
}

/* Define the 'Write' method */
UINT ipso_actuation_write(NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT resource_count, UINT flags)
{
IPSO_ACTUATION_INSTANCE *act = ((IPSO_ACTUATION_INSTANCE *) instance_ptr);
UINT ret;
NX_LWM2M_BOOL onoff;
UINT i;
NX_LWM2M_ID resource_id;

    for (i = 0 ; i < resource_count; i++)
    {
        nx_lwm2m_client_resource_info_get(&resource[i], &resource_id, NX_NULL);
        switch (resource_id)
        {

        case IPSO_RESOURCE_ONOFF:

            /* assign on/off boolean value */
            ret = nx_lwm2m_client_resource_boolean_get(&resource[i], &onoff);
            if (ret != NX_SUCCESS)
            {
                /* invalid value type */
                return(ret);
            }
            if (onoff != act->onoff)
            {
                act->onoff = onoff;

                printf("Set actuation switch %s\n", onoff ? "On" : "Off");
            }
            break;

        default:

            /* unknown resource ID */
            return(NX_LWM2M_CLIENT_NOT_FOUND);
        }
    }

    return(NX_SUCCESS);
}

/* Define the operation callback function of Actuation Object */
UINT ipso_actuation_operation(UINT operation, NX_LWM2M_CLIENT_OBJECT *object_ptr, NX_LWM2M_CLIENT_OBJECT_INSTANCE *object_instance_ptr, NX_LWM2M_CLIENT_RESOURCE *resource, UINT *resource_count, VOID *args_ptr, UINT args_length)
{
UINT write_op;

    switch (operation)
    {
    case NX_LWM2M_CLIENT_OBJECT_READ:

        /* Call read function */
        return ipso_actuation_read(object_ptr, object_instance_ptr, resource, *resource_count);
    case NX_LWM2M_CLIENT_OBJECT_DISCOVER:

        /* Call discover function */
        return ipso_actuation_discover(object_ptr, object_instance_ptr, resource, resource_count);
    case NX_LWM2M_CLIENT_OBJECT_WRITE:

        /* Get the type of write operation */
        write_op = *(UINT *)args_ptr;

        /* Call write function */
        return ipso_actuation_write(object_ptr, object_instance_ptr, resource, *resource_count, write_op);
    default:

        /* Unsupported operation */
        return(NX_LWM2M_CLIENT_NOT_SUPPORTED);
    }
}


/* NetX data.  */
NX_IP                   ip_0;
NX_PACKET_POOL          pool_0;

/* LWM2M Client data.  */
NX_LWM2M_CLIENT         client;
ULONG                   client_stack[4096 / sizeof(ULONG)];
NX_LWM2M_CLIENT_SESSION session;

/* Objects and instances.  */
NX_LWM2M_CLIENT_OBJECT      temperature_object;
NX_LWM2M_CLIENT_OBJECT      actuation_object;
IPSO_TEMPERATURE_INSTANCE   temperature_instance;
IPSO_ACTUATION_INSTANCE     actuation_instance;

/* Define the session state callback */
void session_callback(NX_LWM2M_CLIENT_SESSION *session_ptr, UINT state)
{
    printf("LWM2M Callback: -> %d\n", state);

    switch (state)
    {

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_REQUESTING:

        printf("Start client initiated bootstrap\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_INITIATED:

        printf("Got message from boostrap server\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_FINISHED:

         /* Bootstrap session done, we can register to the LWM2M Server */
        printf( "Boostrap finished.\n");
#ifdef BOOTSTRAP
        tx_semaphore_put(&semaphore_bootstarp_finish);
#endif
        break;

    case NX_LWM2M_CLIENT_SESSION_BOOTSTRAP_ERROR:

        /* Failed to Bootstrap the LWM2M Client. */
        printf( "Failed to boostrap device, error=%02x\n", nx_lwm2m_client_session_error_get(session_ptr));
        break;

    case NX_LWM2M_CLIENT_SESSION_REGISTERED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device registered.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_DISABLED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device disabled.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_DEREGISTERED:

        /* Registration to the LWM2M Client done. */
        printf( "LWM2M device deregistered.\n");
        break;

    case NX_LWM2M_CLIENT_SESSION_ERROR:

        /* Failed to register to the LWM2M Client. */
        printf( "Failed to register device, error=%02x\n", nx_lwm2m_client_session_error_get(session_ptr));
        break;
    }
}


/* Application main thread */
void application_thread(ULONG info)
{

UINT status;
NX_LWM2M_ID server_id = 0;
NXD_ADDRESS server_addr;
CHAR *server_uri = NX_NULL;
UINT server_uri_len = 0;
UCHAR security_mode = 0;
   
    /* Create the LWM2M client */
    status = nx_lwm2m_client_create(&client, &ip_0, &pool_0, "nxlwm2mclient", sizeof("nxlwm2mclient") - 1, NX_NULL, 0, NX_LWM2M_CLIENT_BINDING_U, client_stack, sizeof(client_stack), 4);
    if (status)
    {
        return;
    }

    /* Define our custom objects: */
    /* Add Temperature Object */
    status = nx_lwm2m_client_object_add(&client, &temperature_object, IPSO_TEMPERATURE_OBJECT_ID, ipso_temperature_operation);
    if (status)
    {
        return;
    }

    /* Define a single instance */
    temperature_instance.temperature = 22.5f;
    temperature_instance.min_temperature = temperature_instance.temperature;
    temperature_instance.max_temperature = temperature_instance.temperature;
    status = nx_lwm2m_client_object_instance_add(&temperature_object, &temperature_instance.object_instance, NX_NULL);
    if (status)
    {
        return;
    }

    /* Add Actuation Object */
    status = nx_lwm2m_client_object_add(&client, &actuation_object, IPSO_ACTUATION_OBJECT_ID, ipso_actuation_operation);
    if (status)
    {
        return;
    }

    /* Define a single instance */
    actuation_instance.onoff = NX_FALSE;
    status = nx_lwm2m_client_object_instance_add(&actuation_object, &actuation_instance.object_instance, NX_NULL);
    if (status)
    {
        return;
    }

    /* Create a session */
    status = nx_lwm2m_client_session_create(&session, &client, session_callback);
    if (status)
    {
        return;
}

    /* Set bootstrap server address.  */
    server_addr.nxd_ip_version = NX_IP_VERSION_V4;
    server_addr.nxd_ip_address.v4 = IP_ADDRESS(23, 97, 187, 154);

    printf("Start boostraping\r\n");
    status = nx_lwm2m_client_session_bootstrap(&session, 0, &server_addr, 5783);
    if (status)
    {
        return;
    }

    status = nx_lwm2m_client_session_register_info_get(&session, NX_LWM2M_CLIENT_RESERVED_ID, &server_id, &server_uri, &server_uri_len, &security_mode, NX_NULL, NX_NULL, NX_NULL, NX_NULL, NX_NULL, NX_NULL);
    if (status || (security_mode != NX_LWM2M_CLIENT_SECURITY_MODE_NOSEC))
    {
        return;
    }

printf("Register to LWM2M server\r\n");
status = nx_lwm2m_client_session_register(&session, server_id, &server_addr, 5683);

    if (status)
    {
        return;
    }

    /* Application main loop */
    while (1)
    {

        /* application code... */
        tx_thread_sleep(NX_IP_PERIODIC_RATE);
    }

    /* Terminate the LWM2M Client */
    nx_lwm2m_client_delete(&client);
}

```