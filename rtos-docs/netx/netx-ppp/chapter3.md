---
title: Bölüm 3-Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX PPP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f24d7366d27a8223b069a54ef7b93f6b3e38bf3a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826651"
---
# <a name="chapter-3---description-of-azure-rtos-netx-point-to-point-protocol-ppp-services"></a><span data-ttu-id="b5b59-103">Bölüm 3-Azure RTOS NetX Noktadan Noktaya Protokolü (PPP) hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="b5b59-103">Chapter 3 - Description of Azure RTOS NetX Point-to-Point Protocol (PPP) services</span></span>

<span data-ttu-id="b5b59-104">Bu bölüm, tüm Azure RTOS NetX PPP hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-104">This chapter contains a description of all Azure RTOS NetX PPP services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="b5b59-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="b5b59-106">**nx_ppp_byte_receive**: *seri ISR 'den bayt alma*</span><span class="sxs-lookup"><span data-stu-id="b5b59-106">**nx_ppp_byte_receive**: *Receive a byte from serial ISR*</span></span>
- <span data-ttu-id="b5b59-107">**nx_ppp_chap_challenge**: *CHAP sınaması oluşturma*</span><span class="sxs-lookup"><span data-stu-id="b5b59-107">**nx_ppp_chap_challenge**: *Generate a CHAP challenge*</span></span>
- <span data-ttu-id="b5b59-108">**nx_ppp_chap_enable**: *CHAP kimlik doğrulamasını etkinleştir*</span><span class="sxs-lookup"><span data-stu-id="b5b59-108">**nx_ppp_chap_enable**: *Enable CHAP authentication*</span></span>
- <span data-ttu-id="b5b59-109">**nx_ppp_create**: *bir PPP örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="b5b59-109">**nx_ppp_create**: *Create a PPP instance*</span></span>
- <span data-ttu-id="b5b59-110">**nx_ppp_delete**: *bir PPP örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="b5b59-110">**nx_ppp_delete**: *Delete a PPP instance*</span></span>
- <span data-ttu-id="b5b59-111">**nx_ppp_dns_address_get**: *DNS IP adresini al*</span><span class="sxs-lookup"><span data-stu-id="b5b59-111">**nx_ppp_dns_address_get**: *Get DNS IP address*</span></span>
- <span data-ttu-id="b5b59-112">**nx_ppp_dns_address_set**:*DNS sunucusu IP adresini ayarla*</span><span class="sxs-lookup"><span data-stu-id="b5b59-112">**nx_ppp_dns_address_set**:*Set DNS Server IP address*</span></span>
- <span data-ttu-id="b5b59-113">**nx_ppp_secondary_dns_address_get**: *IKINCIL DNS sunucusu IP adresini al*</span><span class="sxs-lookup"><span data-stu-id="b5b59-113">**nx_ppp_secondary_dns_address_get**: *Get Secondary DNS Server IP address*</span></span>
- <span data-ttu-id="b5b59-114">**nx_ppp_secondary_dns_address_set**: *Secondary_DNS sunucusu IP adresini ayarla*</span><span class="sxs-lookup"><span data-stu-id="b5b59-114">**nx_ppp_secondary_dns_address_set**: *Set Secondary_DNS Server IP address*</span></span>
- <span data-ttu-id="b5b59-115">**nx_ppp_interface_index_get**: *IP arabirimi dizinini al*</span><span class="sxs-lookup"><span data-stu-id="b5b59-115">**nx_ppp_interface_index_get**: *Get IP interface index*</span></span>
- <span data-ttu-id="b5b59-116">**nx_ppp_ip_address_assign**: *IPCP için IP adresleri atama*</span><span class="sxs-lookup"><span data-stu-id="b5b59-116">**nx_ppp_ip_address_assign**: *Assign IP addresses for IPCP*</span></span>
- <span data-ttu-id="b5b59-117">**nx_ppp_link_down_notify**: *bağlantıyı aşağı bağlantıda bilgilendir*</span><span class="sxs-lookup"><span data-stu-id="b5b59-117">**nx_ppp_link_down_notify**: *Notify application on link down*</span></span>
- <span data-ttu-id="b5b59-118">**nx_ppp_link_up_notify**: *uygulamayı bağlantıda bilgilendir*</span><span class="sxs-lookup"><span data-stu-id="b5b59-118">**nx_ppp_link_up_notify**: *Notify application on link up*</span></span>
- <span data-ttu-id="b5b59-119">**nx_ppp_nak_authentication_notify**: *Authentication nak alınmışsa uygulamayı bilgilendir*</span><span class="sxs-lookup"><span data-stu-id="b5b59-119">**nx_ppp_nak_authentication_notify**: *Notify application if authentication NAK is received*</span></span>
- <span data-ttu-id="b5b59-120">**nx_ppp_pap_enable**: *PAP kimlik doğrulamasını etkinleştir*</span><span class="sxs-lookup"><span data-stu-id="b5b59-120">**nx_ppp_pap_enable**: *Enable PAP authentication*</span></span>
- <span data-ttu-id="b5b59-121">**nx_ppp_ping_request**: *bir LCP yankı isteği gönder*</span><span class="sxs-lookup"><span data-stu-id="b5b59-121">**nx_ppp_ping_request**: *Send an LCP echo request*</span></span>
- <span data-ttu-id="b5b59-122">**nx_ppp_raw_string_send**: *PPP olmayan dize gönder*</span><span class="sxs-lookup"><span data-stu-id="b5b59-122">**nx_ppp_raw_string_send**: *Send non PPP string*</span></span>
- <span data-ttu-id="b5b59-123">**nx_ppp_restart**: *PPP işlemeyi yeniden Başlat*</span><span class="sxs-lookup"><span data-stu-id="b5b59-123">**nx_ppp_restart**: *Restart PPP processing*</span></span>
- <span data-ttu-id="b5b59-124">**nx_ppp_start**: *PPP işlemeyi Başlat*</span><span class="sxs-lookup"><span data-stu-id="b5b59-124">**nx_ppp_start**: *Start PPP processing*</span></span>
- <span data-ttu-id="b5b59-125">**nx_ppp_status_get**: *geçerli PPP durumunu Al*</span><span class="sxs-lookup"><span data-stu-id="b5b59-125">**nx_ppp_status_get**: *Get current PPP status*</span></span>
- <span data-ttu-id="b5b59-126">**nx_ppp_stop**: *PPP işlemesini durdur*</span><span class="sxs-lookup"><span data-stu-id="b5b59-126">**nx_ppp_stop**: *Stop PPP processing*</span></span>
- <span data-ttu-id="b5b59-127">**nx_ppp_packet_receive**: *PPP paketi alma*</span><span class="sxs-lookup"><span data-stu-id="b5b59-127">**nx_ppp_packet_receive**: *Receive PPP packet*</span></span>
- <span data-ttu-id="b5b59-128">**nx_ppp_packet_send_set**: *PPP paketi gönderme işlevini ayarla*</span><span class="sxs-lookup"><span data-stu-id="b5b59-128">**nx_ppp_packet_send_set**: *Set PPP packet send function*</span></span>

## <a name="nx_ppp_byte_receive"></a><span data-ttu-id="b5b59-129">nx_ppp_byte_receive</span><span class="sxs-lookup"><span data-stu-id="b5b59-129">nx_ppp_byte_receive</span></span>

<span data-ttu-id="b5b59-130">Seri ıSR 'den bayt al</span><span class="sxs-lookup"><span data-stu-id="b5b59-130">Receive a byte from serial ISR</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-131">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-131">Prototype</span></span>

```c
UINT nx_ppp_byte_receive(NX_PPP *ppp_ptr, UCHAR byte);
```

### <a name="description"></a><span data-ttu-id="b5b59-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-132">Description</span></span>

<span data-ttu-id="b5b59-133">Bu hizmet genellikle uygulamanın seri sürücü kesme hizmeti yordamından (ıSR), alınan bir baytı PPP 'ye aktarmak için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-133">This service is typically called from the application’s serial driver Interrupt Service Routine (ISR) to transfer a received byte to PPP.</span></span> <span data-ttu-id="b5b59-134">Çağrıldığında, bu yordam alınan baytı bir dairesel bayt arabelleğine koyar ve uygun PPP iş parçacığını işlemeye bildirir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-134">When called, this routine places the received byte into a circular byte buffer and notifies the appropriate PPP thread for processing.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-135">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-135">Input Parameters</span></span>

- <span data-ttu-id="b5b59-136">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-136">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-137">**byte**: seri cihazdan alınan bayt</span><span class="sxs-lookup"><span data-stu-id="b5b59-137">**byte**: Byte received from serial device</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-138">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-138">Return Values</span></span>

- <span data-ttu-id="b5b59-139">**NX_SUCCESS**: (0x00) başarılı PPP bayt alma.</span><span class="sxs-lookup"><span data-stu-id="b5b59-139">**NX_SUCCESS**: (0x00) Successful PPP byte receive.</span></span>
- <span data-ttu-id="b5b59-140">**NX_PPP_BUFFER_FULL**: (0Xb1) PPP seri arabelleği zaten dolu.</span><span class="sxs-lookup"><span data-stu-id="b5b59-140">**NX_PPP_BUFFER_FULL**: (0xB1) PPP serial buffer is already full.</span></span>
- <span data-ttu-id="b5b59-141">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-141">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-142">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-142">Allowed From</span></span>

<span data-ttu-id="b5b59-143">İş parçacıkları, ISRs</span><span class="sxs-lookup"><span data-stu-id="b5b59-143">Threads, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-144">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-144">Example</span></span>

```c
/* Notify “my_ppp” of a received byte. */
status =  nx_ppp_byte_receive(&my_ppp, new_byte);

/* If status is NX_SUCCESS the received byte was successfully
   buffered. */
```

## <a name="nx_ppp_chap_challenge"></a><span data-ttu-id="b5b59-145">nx_ppp_chap_challenge</span><span class="sxs-lookup"><span data-stu-id="b5b59-145">nx_ppp_chap_challenge</span></span>

<span data-ttu-id="b5b59-146">CHAP sınaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5b59-146">Generate a CHAP challenge</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-147">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-147">Prototype</span></span>

```c
UINT nx_ppp_chap_challenge(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="b5b59-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-148">Description</span></span>

<span data-ttu-id="b5b59-149">Bu hizmet, PPP bağlantısı zaten çalışır durumda olduktan sonra bir CHAP sınaması başlatır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-149">This service initiates a CHAP challenge after the PPP connection is already up and running.</span></span> <span data-ttu-id="b5b59-150">Bu, uygulamaya düzenli aralıklarla bağlantının orijinalliğini doğrulama olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-150">This gives the application the ability to verify the authenticity of the connection on a periodic basis.</span></span> <span data-ttu-id="b5b59-151">Sınama başarısız olursa, PPP bağlantısı kapatılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-151">If the challenge is unsuccessful, the PPP link is closed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-152">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-152">Input Parameters</span></span>

- <span data-ttu-id="b5b59-153">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-153">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-154">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-154">Return Values</span></span>

- <span data-ttu-id="b5b59-155">**NX_SUCCESS**: (0x00) başarılı PPP sınaması başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-155">**NX_SUCCESS**: (0x00) Successful PPP challenge initiated.</span></span>
- <span data-ttu-id="b5b59-156">**NX_PPP_FAILURE**: (0Xb0) geçersiz PPP SıNAMASı, CHAP yalnızca yanıt için etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-156">**NX_PPP_FAILURE**: (0xB0) Invalid PPP challenge, CHAP was enabled only for response.</span></span>
- <span data-ttu-id="b5b59-157">**NX_NOT_IMPLEMENTED**: (0x80) CHAP mantığı NX_PPP_DISABLE_CHAP ile devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-157">**NX_NOT_IMPLEMENTED**: (0x80) CHAP logic was disabled via NX_PPP_DISABLE_CHAP.</span></span>
- <span data-ttu-id="b5b59-158">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-158">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="b5b59-159">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-159">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-160">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-160">Allowed From</span></span>

<span data-ttu-id="b5b59-161">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-161">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-162">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-162">Example</span></span>

```c
/* Initiate a PPP challenge for instance “my_ppp”. */
status =  nx_ppp_chap_challenge(&my_ppp);

/* If status is NX_SUCCESS a CHAP challenge “my_ppp” was successfully 
initiated. */
```

## <a name="nx_ppp_chap_enable"></a><span data-ttu-id="b5b59-163">nx_ppp_chap_enable</span><span class="sxs-lookup"><span data-stu-id="b5b59-163">nx_ppp_chap_enable</span></span>

<span data-ttu-id="b5b59-164">CHAP kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b5b59-164">Enable CHAP authentication</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-165">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-165">Prototype</span></span>

```c
UINT nx_ppp_chap_enable(NX_PPP *ppp_ptr, 
                        UINT (*get_challenge_values)(CHAR *rand_value,CHAR *id,CHAR *name),
                        UINT (*get_responder_values)(CHAR *system,CHAR *name,CHAR *secret),
                        UINT (*get_verification_values)(CHAR *system,CHAR *name,CHAR *secret)); 
```

### <a name="description"></a><span data-ttu-id="b5b59-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-166">Description</span></span>

<span data-ttu-id="b5b59-167">Bu hizmet, belirtilen PPP örneği için Challenge-Handshake kimlik doğrulama protokolü (CHAP) sunar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-167">This service enables the Challenge-Handshake Authentication Protocol (CHAP) for the specified PPP instance.</span></span>

<span data-ttu-id="b5b59-168">"\***Get_challenge_values**_" ve "_ \* _get_verification_values_\* \*" işlev işaretçileri belirtilmişse, bu PPP örneği için CHAP gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-168">If the “\***get_challenge_values**_” and “_\*_get_verification_values_\*\*” function pointers are specified, CHAP is required by this PPP instance.</span></span> <span data-ttu-id="b5b59-169">Aksi halde, CHAP yalnızca eşin sınama isteklerine yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-169">Otherwise, CHAP only responds to the peer’s challenge requests.</span></span>

<span data-ttu-id="b5b59-170">Gerekli geri çağırma işlevlerinde aşağıda başvurulan birkaç veri öğesi vardır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-170">There are several data items referenced below in the required callback functions.</span></span> <span data-ttu-id="b5b59-171">Veri öğeleri *gizli*, *adı* ve *sisteminin* , en fazla NX_PPP_NAME_SIZE-1 boyutuna sahip null ile sonlandırılmış dizeler olması beklenir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-171">The data items *secret*, *name*, and *system* are expected to be NULL-terminated strings with a maximum size of NX_PPP_NAME_SIZE-1.</span></span> <span data-ttu-id="b5b59-172">*Rand_value* veri öğesi, en fazla NX_PPP_VALUE_SIZE-1 boyutuna sahip null ile sonlandırılmış bir dize olması beklenir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-172">The data item *rand_value* is expected to be a NULL-terminated string with a maximum size of NX_PPP_VALUE_SIZE-1.</span></span> <span data-ttu-id="b5b59-173">Veri öğesi *kimliği* , bir basit işaretsiz karakter türüdür.</span><span class="sxs-lookup"><span data-stu-id="b5b59-173">The data item *id* is a simple unsigned character type.</span></span>

>[!NOTE]
> <span data-ttu-id="b5b59-174">Bu işlev, *nx_ppp_create* sonra, nx_ip_create veya *nx_ip_interface_attach* önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-174">This function must be called after *nx_ppp_create* but before nx_ip_create or *nx_ip_interface_attach*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-175">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-175">Input Parameters</span></span>

- <span data-ttu-id="b5b59-176">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-176">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-177">**get_challenge_values**: zorluk için kullanılan değerleri almak için uygulama işlevine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-177">**get_challenge_values**: Pointer to application function to retrieve values used for the challenge.</span></span> <span data-ttu-id="b5b59-178">*Rand_value*, *kimlik* ve *gizli* değerlerinin sağlanan hedeflere kopyalanması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b5b59-178">Note that the *rand_value*, *id*, and *secret* values must be copied into the supplied destinations.</span></span>
- <span data-ttu-id="b5b59-179">**get_responder_values**: bir Challenge 'a yanıt vermek için kullanılan değerleri alan uygulama işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-179">**get_responder_values**: Pointer to application function that retrieves values used to respond to a challenge.</span></span> <span data-ttu-id="b5b59-180">*System*, *Name* ve *Secret* değerlerinin sağlanan hedeflere kopyalanması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b5b59-180">Note that the *system*, *name*, and *secret* values must be copied into the supplied destinations.</span></span>
- <span data-ttu-id="b5b59-181">**get_verification_values**: sınama yanıtını doğrulamak için kullanılan değerleri alan uygulama işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-181">**get_verification_values**: Pointer to application function that retrieves values used to verify the challenge response.</span></span> <span data-ttu-id="b5b59-182">*System*,*Name* ve *Secret* değerlerinin sağlanan hedeflere kopyalanması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b5b59-182">Note that the *system*,*name*, and *secret* values must be copied into the supplied destinations.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-183">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-183">Return Values</span></span>

- <span data-ttu-id="b5b59-184">**NX_SUCCESS**: (0x00) başarılı PPP CHAP etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b5b59-184">**NX_SUCCESS**: (0x00) Successful PPP CHAP enable</span></span>
- <span data-ttu-id="b5b59-185">**NX_NOT_IMPLEMENTED**: (0x80) CHAP mantığı NX_PPP_DISABLE_CHAP ile devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-185">**NX_NOT_IMPLEMENTED**: (0x80) CHAP logic was disabled via NX_PPP_DISABLE_CHAP.</span></span>
- <span data-ttu-id="b5b59-186">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi veya geri çağırma işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-186">NX_PTR_ERROR: (0x07) Invalid PPP pointer or callback function pointer.</span></span> <span data-ttu-id="b5b59-187">*Get_challenge_values* belirtilmişse *get_verification_values* işlevinin da sağlanması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b5b59-187">Note that if *get_challenge_values* is specified, then the *get_verification_values* function must also be supplied.</span></span>
- <span data-ttu-id="b5b59-188">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-188">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-189">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-189">Allowed From</span></span>

<span data-ttu-id="b5b59-190">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-190">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-191">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-191">Example</span></span>

```c
CHAR    name_string[] = "username";
CHAR    rand_value_string[] = "123456";
CHAR    system_string[] = "system";
CHAR    secret_string[] = "secret";

/* Enable CHAP in both directions (CHAP challenger and CHAP responder) for 
“my_ppp”. */
status =  nx_ppp_chap_enable(&my_ppp,   get_challenge_values, 
                              get_responder_values,
                              get_verification_values);


/* If status is NX_SUCCESS, “my_ppp” has CHAP enabled. */
/* Define the CHAP enable routines.  */
UINT  get_challenge_values(CHAR *rand_value, CHAR *id, CHAR *name)
{
   UINT    i;
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;
   
   *id =  '1';  /* One byte  */
   for (i = 0; i< (NX_PPP_VALUE_SIZE-1); i++)
   {
      rand_value[i] =  rand_value_string[i];
   }
   rand_value[i] =  0;
   
   return(NX_SUCCESS);  
}


UINT  get_responder_values(CHAR *system, CHAR *name, CHAR *secret)
{
   UINT    i;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;

   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      system[i] =  system_string[i];
   }
   system[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      secret[i] =  secret_string[i];
   }
   secret[i] =  0;
   
   return(NX_SUCCESS);  
}

UINT  get_verification_values(CHAR *system, CHAR *name, CHAR *secret)
{
   UINT    i;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      name[i] = name_string[i];
   }
   name[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      system[i] =  system_string[i];
   }
   system[i] =  0;
   
   for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
   {
      secret[i] =  secret_string[i];
   }
   secret[i] =  0;
   
   return(NX_SUCCESS);  
}

```
## <a name="nx_ppp_create"></a><span data-ttu-id="b5b59-192">nx_ppp_create</span><span class="sxs-lookup"><span data-stu-id="b5b59-192">nx_ppp_create</span></span>

<span data-ttu-id="b5b59-193">Bir PPP örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5b59-193">Create a PPP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-194">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-194">Prototype</span></span>

```c
UINT  nx_ppp_create(NX_PPP *ppp_ptr, CHAR *name, NX_IP *ip_ptr, 
                    VOID *stack_memory_ptr, ULONG stack_size, 
                    UINT thread_priority, NX_PACKET_POOL *pool_ptr,
                    void (*ppp_invalid_packet_handler)(NX_PACKET *packet_ptr),
                    void (*ppp_byte_send)(UCHAR byte));
```

### <a name="description"></a><span data-ttu-id="b5b59-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-195">Description</span></span>

<span data-ttu-id="b5b59-196">Bu hizmet, belirtilen NetX IP örneği için bir PPP örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b5b59-196">This service creates a PPP instance for the specified NetX IP instance.</span></span>

>[!NOTE]
> <span data-ttu-id="b5b59-197">Genellikle NetX IP iş parçacığını, PPP iş parçacığı önceliğinden daha yüksek bir önceliğe göre oluşturmak iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-197">It is generally a good idea to create the NetX IP thread at a higher priority than the PPP thread priority.</span></span> <span data-ttu-id="b5b59-198">IP iş parçacığı önceliğini belirtme hakkında daha fazla bilgi için lütfen *nx_ip_create* hizmetine bakın.</span><span class="sxs-lookup"><span data-stu-id="b5b59-198">Please refer to the *nx_ip_create* service for more information on specifying the IP thread priority.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-199">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-199">Input Parameters</span></span>

- <span data-ttu-id="b5b59-200">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-200">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-201">**ad**: bu PPP örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-201">**name**: Name of this PPP instance.</span></span>
- <span data-ttu-id="b5b59-202">**ip_ptr**: henüz oluşturulmamış IP örneği için denetim bloğuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-202">**ip_ptr**: Pointer to control block for not-yet-created IP instance.</span></span>
- <span data-ttu-id="b5b59-203">**stack_memory_ptr**: PPP iş parçacığının yığın alanının başlangıcı işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-203">**stack_memory_ptr**: Pointer to start of PPP thread’s stack area.</span></span>
- <span data-ttu-id="b5b59-204">**stack_size**: iş parçacığının yığınında bayt cinsinden boyut.</span><span class="sxs-lookup"><span data-stu-id="b5b59-204">**stack_size**: Size in bytes in the thread’s stack.</span></span>
- <span data-ttu-id="b5b59-205">**pool_ptr**: varsayılan paket havuzuna yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-205">**pool_ptr**: Pointer to default packet pool.</span></span>
- <span data-ttu-id="b5b59-206">**thread_priority**: iç PPP iş parçacıklarının önceliği (1-31).</span><span class="sxs-lookup"><span data-stu-id="b5b59-206">**thread_priority**: Priority of internal PPP threads (1-31).</span></span>
- <span data-ttu-id="b5b59-207">**ppp_invalid_packet_handler**: tüm PPP olmayan paketler için uygulamanın işleyicisine yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-207">**ppp_invalid_packet_handler**: Function pointer to application’s handler for all non-PPP packets.</span></span> <span data-ttu-id="b5b59-208">NetX PPP, genellikle başlatma sırasında bu yordamı çağırır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-208">The NetX PPP typically calls this routine during initialization.</span></span> <span data-ttu-id="b5b59-209">Bu, uygulamanın modem komutlarına yanıt verebildiği veya Windows XP söz konusu olduğunda, NetX PPP uygulamasının "ISTEMCI sunucusu" ile Windows XP tarafından gönderilen ilk "ISTEMCI" ile yanıt vererek PPP başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-209">This is where the application can respond to modem commands or in the case of Windows XP, the NetX PPP application can initiate PPP by responding with“ CLIENT SERVER” to the initial “CLIENT” sent by Windows XP.</span></span>
- <span data-ttu-id="b5b59-210">**ppp_byte_send**: uygulamanın seri baytlık çıkış yordamına yönelik işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-210">**ppp_byte_send**: Function pointer to application’s serial byte output routine.</span></span>


### <a name="return-values"></a><span data-ttu-id="b5b59-211">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-211">Return Values</span></span>

- <span data-ttu-id="b5b59-212">**NX_SUCCESS**: (0x00) başarılı PPP oluştur.</span><span class="sxs-lookup"><span data-stu-id="b5b59-212">**NX_SUCCESS**: (0x00) Successful PPP create.</span></span>
- <span data-ttu-id="b5b59-213">NX_PTR_ERROR: (0x07) geçersiz PPP, IP veya Byte çıkış işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-213">NX_PTR_ERROR: (0x07) Invalid PPP, IP, or byte output function pointer.</span></span>
- <span data-ttu-id="b5b59-214">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-214">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-215">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-215">Allowed From</span></span>

<span data-ttu-id="b5b59-216">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-216">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-217">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-217">Example</span></span>

```c
/* Create “my_ppp” for IP instance “my_ip”. */
status =  nx_ppp_create(&my_ppp, “my PPP”, &my_ip, stack_start, 1024, 2, 
                        &my_pool, my_invalid_packet_handler, my_out_byte);

/* If status is NX_SUCCESS the PPP instance was successfully
   created. */
```

## <a name="nx_ppp_delete"></a><span data-ttu-id="b5b59-218">nx_ppp_delete</span><span class="sxs-lookup"><span data-stu-id="b5b59-218">nx_ppp_delete</span></span>

<span data-ttu-id="b5b59-219">Bir PPP örneğini silme</span><span class="sxs-lookup"><span data-stu-id="b5b59-219">Delete a PPP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-220">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-220">Prototype</span></span>

```c
UINT nx_ppp_delete(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="b5b59-221">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-221">Description</span></span>

<span data-ttu-id="b5b59-222">Bu hizmet, önceden oluşturulmuş PPP örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="b5b59-222">This service deletes the previously created PPP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-223">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-223">Input Parameters</span></span>

- <span data-ttu-id="b5b59-224">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-224">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-225">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-225">Return Values</span></span>

- <span data-ttu-id="b5b59-226">**NX_SUCCESS**: (0x00) başarılı PPP silme.</span><span class="sxs-lookup"><span data-stu-id="b5b59-226">**NX_SUCCESS**: (0x00) Successful PPP deletion.</span></span>
- <span data-ttu-id="b5b59-227">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-227">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="b5b59-228">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-228">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-229">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-229">Allowed From</span></span>

<span data-ttu-id="b5b59-230">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-230">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-231">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-231">Example</span></span>

```c
/* Delete PPP instance “my_ppp”. */
status =  nx_ppp_delete(&my_ppp);

/* If status is NX_SUCCESS the “my_ppp” was successfully deleted. */
```

## <a name="nx_ppp_dns_address_get"></a><span data-ttu-id="b5b59-232">nx_ppp_dns_address_get</span><span class="sxs-lookup"><span data-stu-id="b5b59-232">nx_ppp_dns_address_get</span></span>

<span data-ttu-id="b5b59-233">DNS IP adresini al</span><span class="sxs-lookup"><span data-stu-id="b5b59-233">Get DNS IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-234">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-234">Prototype</span></span>

```c
UINT nx_ppp_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a><span data-ttu-id="b5b59-235">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-235">Description</span></span>

<span data-ttu-id="b5b59-236">Bu hizmet, eş tarafından sağlanan DNS IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-236">This service retrieves the DNS IP address supplied by the peer.</span></span> <span data-ttu-id="b5b59-237">Eş tarafından bir IP adresi sağlanmadığında, 0 IP adresi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b5b59-237">If no IP address was supplied by the peer, an IP address of 0 is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-238">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-238">Input Parameters</span></span>

- <span data-ttu-id="b5b59-239">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-239">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-240">**dns_address_ptr**: DNS IP adresi hedefi</span><span class="sxs-lookup"><span data-stu-id="b5b59-240">**dns_address_ptr**: Destination for DNS IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-241">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-241">Return Values</span></span>

- <span data-ttu-id="b5b59-242">**NX_SUCCESS**: (0x00) başarılı PPP adresi Get.</span><span class="sxs-lookup"><span data-stu-id="b5b59-242">**NX_SUCCESS**: (0x00) Successful PPP address get.</span></span>
- <span data-ttu-id="b5b59-243">**NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP, eş ile anlaşmayı tamamlamadı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-243">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP has not completed negotiation with peer.</span></span>
- <span data-ttu-id="b5b59-244">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-244">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-245">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-245">Allowed From</span></span>

<span data-ttu-id="b5b59-246">Başlatma, iş parçacıkları, zamanlayıcılar, ISRs</span><span class="sxs-lookup"><span data-stu-id="b5b59-246">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-247">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-247">Example</span></span>

```c

ULONG  my_dns_address;

/* Get IP Server address supplied by peer. */
status =  nx_ppp_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the DNS IP address – 
   if the peer supplied one. */
```

## <a name="nx_ppp_secondary_dns_address_get"></a><span data-ttu-id="b5b59-248">nx_ppp_secondary_dns_address_get</span><span class="sxs-lookup"><span data-stu-id="b5b59-248">nx_ppp_secondary_dns_address_get</span></span>

<span data-ttu-id="b5b59-249">Ikincil DNS sunucusu IP adresini al</span><span class="sxs-lookup"><span data-stu-id="b5b59-249">Get Secondary DNS Server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-250">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-250">Prototype</span></span>

```c
UINT nx_ppp_secondary_dns_address_get(NX_PPP *ppp_ptr, ULONG *dns_address_ptr);
```

### <a name="description"></a><span data-ttu-id="b5b59-251">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-251">Description</span></span>

<span data-ttu-id="b5b59-252">Bu hizmet, bir ıPCP el sıkışmasının eşi tarafından sağlanan ikincil DNS IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-252">This service retrieves the secondary DNS IP address supplied by the peer in the IPCP handshake.</span></span> <span data-ttu-id="b5b59-253">Eş tarafından bir IP adresi sağlanmadığında, 0 IP adresi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b5b59-253">If no IP address was supplied by the peer, an IP address of 0 is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-254">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-254">Input Parameters</span></span>

- <span data-ttu-id="b5b59-255">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-255">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-256">**dns_address_ptr**: ikincil DNS sunucusu adresi için hedef</span><span class="sxs-lookup"><span data-stu-id="b5b59-256">**dns_address_ptr**: Destination for Secondary DNS server address</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-257">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-257">Return Values</span></span>

- <span data-ttu-id="b5b59-258">**NX_SUCCESS**: (0x00) başarılı DNS adresi Get.</span><span class="sxs-lookup"><span data-stu-id="b5b59-258">**NX_SUCCESS**: (0x00) Successful DNS address get.</span></span>
- <span data-ttu-id="b5b59-259">**NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP, eş ile anlaşmayı tamamlamadı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-259">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP has not completed negotiation with peer.</span></span>
- <span data-ttu-id="b5b59-260">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-260">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-261">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-261">Allowed From</span></span>

<span data-ttu-id="b5b59-262">Başlatma, iş parçacıkları, zamanlayıcılar, ISRs</span><span class="sxs-lookup"><span data-stu-id="b5b59-262">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-263">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-263">Example</span></span>

```c
ULONG  my_dns_address;

/* Get secondary DNS Server address supplied by peer. */
status =  nx_ppp_secondary_dns_address_get(&my_ppp, &my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” contains the secondary DNS Server address – if the peer supplied one. */
```

## <a name="nx_ppp_dns_address_set"></a><span data-ttu-id="b5b59-264">nx_ppp_dns_address_set</span><span class="sxs-lookup"><span data-stu-id="b5b59-264">nx_ppp_dns_address_set</span></span>

<span data-ttu-id="b5b59-265">Birincil DNS sunucusu IP adresini ayarla</span><span class="sxs-lookup"><span data-stu-id="b5b59-265">Set primary DNS Server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-266">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-266">Prototype</span></span>

```c
UINT nx_ppp_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a><span data-ttu-id="b5b59-267">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-267">Description</span></span>

<span data-ttu-id="b5b59-268">Bu hizmet, DNS sunucusu IP adresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-268">This service sets the DNS Server IP address.</span></span> <span data-ttu-id="b5b59-269">Eş, ıPCP durumunda bir DNS sunucusu seçenek isteği gönderirse, bu ana bilgisayar bu bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-269">If the peer sends a DNS Server option request in the IPCP state, this host will provide the information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-270">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-270">Input Parameters</span></span>

- <span data-ttu-id="b5b59-271">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-271">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-272">**dns_address**: DNS sunucusu adresi</span><span class="sxs-lookup"><span data-stu-id="b5b59-272">**dns_address**: DNS server address</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-273">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-273">Return Values</span></span>

- <span data-ttu-id="b5b59-274">**NX_SUCCESS**: (0x00) başarılı DNS adresi kümesi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-274">**NX_SUCCESS**: (0x00) Successful DNS address set.</span></span>
- <span data-ttu-id="b5b59-275">**NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP, eş ile anlaşmayı tamamlamadı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-275">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP has not completed negotiation with peer.</span></span>
- <span data-ttu-id="b5b59-276">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-276">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-277">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-277">Allowed From</span></span>

<span data-ttu-id="b5b59-278">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-278">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-279">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-279">Example</span></span>

```c

ULONG  my_dns_address = IP_ADDRESS(1,2,3,1);

/* Set DNS Server address. */
status =  nx_ppp_dns_address_set(&my_ppp, my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” will be the DNS Server address provided if the peer requests one. */

```

## <a name="nx_ppp_secondary_dns_address_set"></a><span data-ttu-id="b5b59-280">nx_ppp_secondary_dns_address_set</span><span class="sxs-lookup"><span data-stu-id="b5b59-280">nx_ppp_secondary_dns_address_set</span></span>

<span data-ttu-id="b5b59-281">İkincil DNS sunucusu IP adresini ayarla</span><span class="sxs-lookup"><span data-stu-id="b5b59-281">Set secondary DNS Server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-282">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-282">Prototype</span></span>

```c
UINT nx_ppp_secondary_dns_address_set(NX_PPP *ppp_ptr, ULONG dns_address);
```

### <a name="description"></a><span data-ttu-id="b5b59-283">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-283">Description</span></span>

<span data-ttu-id="b5b59-284">Bu hizmet, ikincil DNS sunucusu IP adresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-284">This service sets the secondary DNS Server IP address.</span></span> <span data-ttu-id="b5b59-285">Eş, ıPCP durumunda ikincil bir DNS sunucusu seçenek isteği gönderirse bu konak bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-285">If the peer sends a secondary DNS Server option request in the IPCP state, this host will provide the information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-286">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-286">Input Parameters</span></span>

- <span data-ttu-id="b5b59-287">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-287">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-288">**dns_address**: ikincil DNS sunucusu adresi</span><span class="sxs-lookup"><span data-stu-id="b5b59-288">**dns_address**: Secondary DNS server address</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-289">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-289">Return Values</span></span>

- <span data-ttu-id="b5b59-290">**NX_SUCCESS**: (0x00) başarılı DNS adresi kümesi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-290">**NX_SUCCESS**: (0x00) Successful DNS address set.</span></span> 
- <span data-ttu-id="b5b59-291">**NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP, eş ile anlaşmayı tamamlamadı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-291">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP has not completed negotiation with peer.</span></span>
- <span data-ttu-id="b5b59-292">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-292">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-293">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-293">Allowed From</span></span>

<span data-ttu-id="b5b59-294">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-294">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-295">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-295">Example</span></span>

```c
ULONG  my_dns_address = IP_ADDRESS(1,2,3,1);

/* Set DNS Server address. */
status =  nx_ppp_secondary_dns_address_set(&my_ppp, my_dns_address);

/* If status is NX_SUCCESS the “my_dns_address” will be the secondary DNS Server address provided if the peer requests one. */

```
## <a name="nx_ppp_interface_index_get"></a><span data-ttu-id="b5b59-296">nx_ppp_interface_index_get</span><span class="sxs-lookup"><span data-stu-id="b5b59-296">nx_ppp_interface_index_get</span></span>

<span data-ttu-id="b5b59-297">IP arabirimi dizinini al</span><span class="sxs-lookup"><span data-stu-id="b5b59-297">Get IP interface index</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-298">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-298">Prototype</span></span>

```c
UINT nx_ppp_interface_index_get(NX_PPP *ppp_ptr, UINT *index_ptr);
```

### <a name="description"></a><span data-ttu-id="b5b59-299">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-299">Description</span></span>

<span data-ttu-id="b5b59-300">Bu hizmet, bu PPP örneğiyle ilişkili IP arabirimi dizinini alır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-300">This service retrieves the IP interface index associated with this PPP instance.</span></span> <span data-ttu-id="b5b59-301">Bu, yalnızca PPP örneği bir IP örneğinin birincil arabirimi olmadığında yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-301">This is only useful when the PPP instance is not the primary interface of an IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-302">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-302">Input Parameters</span></span>

- <span data-ttu-id="b5b59-303">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-303">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-304">**index_ptr**: arabirim dizini hedefi</span><span class="sxs-lookup"><span data-stu-id="b5b59-304">**index_ptr**: Destination for interface index</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-305">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-305">Return Values</span></span>

- <span data-ttu-id="b5b59-306">**NX_SUCCESS**: (0x00) başarılı PPP dizini Get.</span><span class="sxs-lookup"><span data-stu-id="b5b59-306">**NX_SUCCESS**: (0x00) Successful PPP index get.</span></span>
- <span data-ttu-id="b5b59-307">**NX_IN_PROGRESS**: (0x37) PPP başlatmayı tamamlamadı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-307">**NX_IN_PROGRESS**: (0x37) PPP has not completed initialization.</span></span>
- <span data-ttu-id="b5b59-308">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-308">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-309">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-309">Allowed From</span></span>

<span data-ttu-id="b5b59-310">Başlatma, iş parçacıkları, zamanlayıcılar, ISRs</span><span class="sxs-lookup"><span data-stu-id="b5b59-310">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-311">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-311">Example</span></span>

```c
ULONG  my_index;

/* Get the interface index for this PPP instance. */
status =  nx_ppp_interface_index_get(&my_ppp, &my_index);

/* If status is NX_SUCCESS the “my_index” contains the IP interface index for
   this PPP instance. */

```
## <a name="nx_ppp_ip_address_assign"></a><span data-ttu-id="b5b59-312">nx_ppp_ip_address_assign</span><span class="sxs-lookup"><span data-stu-id="b5b59-312">nx_ppp_ip_address_assign</span></span>

<span data-ttu-id="b5b59-313">IPCP için IP adresleri atama</span><span class="sxs-lookup"><span data-stu-id="b5b59-313">Assign IP addresses for IPCP</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-314">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-314">Prototype</span></span>

```c
UINT nx_ppp_ip_address_assign(NX_PPP *ppp_ptr, ULONG local_ip_address, 
            ULONG peer_ip_address);
```

### <a name="description"></a><span data-ttu-id="b5b59-315">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-315">Description</span></span>

<span data-ttu-id="b5b59-316">Bu hizmet, Internet Protokolü Denetim Protokolü 'nde (ıPCP) kullanılmak üzere yerel ve eş IP adreslerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-316">This service sets up the local and peer IP addresses for use in the Internet Protocol Control Protocol (IPCP).</span></span> <span data-ttu-id="b5b59-317">PPP uygulaması bu hizmeti, kendisi ve diğer eşdüzey için geçerli IP adreslerine sahip bir PPP örneğinde çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-317">The PPP application should invoke this service on a PPP instance with valid IP addresses for itself and the other peer.</span></span>  <span data-ttu-id="b5b59-318">Bir PPP örneğiyle kayıtlı geçerli bir adres yoksa, IP adresini tanımlamak için PPP eşine güvenmelidir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-318">If no valid addresses are registered with a PPP instance, it must rely on the PPP peer to define its IP address.</span></span>


### <a name="input-parameters"></a><span data-ttu-id="b5b59-319">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-319">Input Parameters</span></span>

- <span data-ttu-id="b5b59-320">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-320">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-321">**local_ip_address**: yerel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-321">**local_ip_address**: Local IP address.</span></span>
- <span data-ttu-id="b5b59-322">**peer_ip_address**: eşin IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-322">**peer_ip_address**: Peer’s IP address.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-323">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-323">Return Values</span></span>

- <span data-ttu-id="b5b59-324">**NX_SUCCESS**: (0x00) başarılı PPP adresi ataması.</span><span class="sxs-lookup"><span data-stu-id="b5b59-324">**NX_SUCCESS**: (0x00) Successful PPP address assignment.</span></span>
- <span data-ttu-id="b5b59-325">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-325">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="b5b59-326">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-326">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-327">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-327">Allowed From</span></span>

<span data-ttu-id="b5b59-328">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-328">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-329">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-329">Example</span></span>

```c
/* Set IP addresses for “my_ppp”. */
status =  nx_ppp_ip_address_assign(&my_ppp, IP_ADDRESS(256,2,2,187), 
IP_ADDRESS(256,2,2,188));


/* If status is NX_SUCCESS the “my_ppp” has the IP addresses. */
```

## <a name="nx_ppp_link_down_notify"></a><span data-ttu-id="b5b59-330">nx_ppp_link_down_notify</span><span class="sxs-lookup"><span data-stu-id="b5b59-330">nx_ppp_link_down_notify</span></span>

<span data-ttu-id="b5b59-331">Bağlantıyı aşağı bağlantıda bilgilendir</span><span class="sxs-lookup"><span data-stu-id="b5b59-331">Notify application on link down</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-332">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-332">Prototype</span></span>

```c
UINT nx_ppp_link_down_notify(NX_PPP *ppp_ptr, 
                             VOID (*link_down_callback)(NX_PPP *ppp_ptr));
```

### <a name="description"></a><span data-ttu-id="b5b59-333">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-333">Description</span></span>

<span data-ttu-id="b5b59-334">Bu hizmet, uygulamanın bağlantı azaltma bildirimi geri aramasını belirtilen PPP örneğiyle kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b5b59-334">This service registers the application’s link down notification callback with the specified PPP instance.</span></span> <span data-ttu-id="b5b59-335">NULL değilse, bağlantının geri çağırma işlevi, bağlantı her gittiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-335">If non-NULL, the application’s link down callback function is called whenever the link goes down.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-336">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-336">Input Parameters</span></span>

- <span data-ttu-id="b5b59-337">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-337">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-338">**link_down_callback**: uygulamanın bağlantı azaltma uyarısı işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-338">**link_down_callback**: Application’s link down notification function pointer.</span></span> <span data-ttu-id="b5b59-339">NULL ise, bağlantı azaltma bildirimi devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-339">If NULL, link down notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-340">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-340">Return Values</span></span>

- <span data-ttu-id="b5b59-341">**NX_SUCCESS**: (0x00) bildirim geri çağırma kaydı başarıyla açıldı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-341">**NX_SUCCESS**: (0x00) Successful link down notification callback registration.</span></span>
- <span data-ttu-id="b5b59-342">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-342">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-343">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-343">Allowed From</span></span>

<span data-ttu-id="b5b59-344">Başlatma, iş parçacıkları, zamanlayıcılar, ISRs</span><span class="sxs-lookup"><span data-stu-id="b5b59-344">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-345">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-345">Example</span></span>

```c
/* Register “my_link_down_callback” to be called whenever the PPP
   link goes down. */
status =  nx_ppp_link_down_notify(&my_ppp, my_link_down_callback);


/* If status is NX_SUCCESS the function “my_link_down_callback” has been
   registered with this PPP instance. */

VOID my_link_down_callback(NX_PPP *ppp_ptr)
{

/* On link down, simply restart PPP.  */
    nx_ppp_restart(ppp_ptr);
} 
```
## <a name="nx_ppp_link_up_notify"></a><span data-ttu-id="b5b59-346">nx_ppp_link_up_notify</span><span class="sxs-lookup"><span data-stu-id="b5b59-346">nx_ppp_link_up_notify</span></span>

<span data-ttu-id="b5b59-347">Bağlantı üzerinde uygulamayı bilgilendir</span><span class="sxs-lookup"><span data-stu-id="b5b59-347">Notify application on link up</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-348">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-348">Prototype</span></span>

```c
UINT nx_ppp_link_up_notify(NX_PPP *ppp_ptr, 
                           VOID (*link_up_callback)(NX_PPP *ppp_ptr));
```
### <a name="description"></a><span data-ttu-id="b5b59-349">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-349">Description</span></span>

<span data-ttu-id="b5b59-350">Bu hizmet, uygulamanın bağlantı bildirimi geri aramasını belirtilen PPP örneğiyle kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b5b59-350">This service registers the application’s link up notification callback with the specified PPP instance.</span></span> <span data-ttu-id="b5b59-351">NULL olmadığında, bağlantının geri çağırma işlevi bağlantı her geldiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-351">If non-NULL, the application’s link up callback function is called whenever the link comes up.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-352">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-352">Input Parameters</span></span>

- <span data-ttu-id="b5b59-353">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-353">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-354">**link_up_callback**: uygulamanın bağlantı bildirim işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-354">**link_up_callback**: Application’s link up notification function pointer.</span></span> <span data-ttu-id="b5b59-355">NULL ise, bağlantı bildirimi devre dışıdır. \* \*</span><span class="sxs-lookup"><span data-stu-id="b5b59-355">If NULL, link up notification is disabled.\*\*</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-356">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-356">Return Values</span></span>

- <span data-ttu-id="b5b59-357">**NX_SUCCESS**: (0x00) başarılı bağlantı geri çağırma kaydı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-357">**NX_SUCCESS**: (0x00) Successful link up notification callback registration.</span></span>
- <span data-ttu-id="b5b59-358">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-358">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-359">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-359">Allowed From</span></span>

<span data-ttu-id="b5b59-360">Başlatma, iş parçacıkları, zamanlayıcılar, ISRs</span><span class="sxs-lookup"><span data-stu-id="b5b59-360">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-361">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-361">Example</span></span>

```c
/* Register “my_link_up_callback” to be called whenever the PPP
   link comes up. */
status =  nx_ppp_link_up_notify(&my_ppp, my_link_up_callback);


/* If status is NX_SUCCESS the function “my_link_up_callback” has been
   registered with this PPP instance. */

VOID my_link_up_callback(NX_PPP *ppp_ptr)
{
    /* On link up, the application my want to start sending/receiving
       UPD/TCP data.  */
}
```

## <a name="nx_ppp_nak_authentication_notify"></a><span data-ttu-id="b5b59-362">nx_ppp_nak_authentication_notify</span><span class="sxs-lookup"><span data-stu-id="b5b59-362">nx_ppp_nak_authentication_notify</span></span>

<span data-ttu-id="b5b59-363">Kimlik doğrulama NAK 'ı alındı ise uygulamayı bilgilendir</span><span class="sxs-lookup"><span data-stu-id="b5b59-363">Notify application if authentication NAK received</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-364">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-364">Prototype</span></span>

```c
UINT    nx_ppp_nak_authentication_notify(NX_PPP *ppp_ptr, 
                                         void (*nak_authentication_notify)(void));
```

### <a name="description"></a><span data-ttu-id="b5b59-365">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-365">Description</span></span>

<span data-ttu-id="b5b59-366">Bu hizmet, uygulamanın kimlik doğrulama nak Notification geri aramasını belirtilen PPP örneğiyle kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b5b59-366">This service registers the application’s authentication nak notification callback with the specified PPP instance.</span></span> <span data-ttu-id="b5b59-367">NULL değilse, bu geri çağırma işlevi, bir authentiaction sırasında her bir bir NAK aldığında çağırılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-367">If non-NULL, this callback function is called whenever the PPP instance receives a NAK during authentiaction.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-368">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-368">Input Parameters</span></span>

- <span data-ttu-id="b5b59-369">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-369">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-370">**nak_authentication_notify**: PPP örneği bir KIMLIK doğrulama nak 'ı aldığında çağrılan işlev işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-370">**nak_authentication_notify**: Pointer to function called when the PPP instance receives an authentication NAK.</span></span> <span data-ttu-id="b5b59-371">NULL ise, bildirim devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-371">If NULL, the notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-372">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-372">Return Values</span></span>

- <span data-ttu-id="b5b59-373">**NX_SUCCESS**: (0x00) başarılı bildirim geri çağırma kaydı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-373">**NX_SUCCESS**: (0x00) Successful notification callback registration.</span></span>
- <span data-ttu-id="b5b59-374">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-374">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-375">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-375">Allowed From</span></span>

<span data-ttu-id="b5b59-376">Başlatma, iş parçacıkları, zamanlayıcılar, ISRs</span><span class="sxs-lookup"><span data-stu-id="b5b59-376">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-377">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-377">Example</span></span>

```c
/* Register “my_nak_auth_callback” to be called whenever the PPP
   receives a NAK during authentication. */
status =  nx_ppp_nak_authentication_notify(&my_ppp, my_nak_auth_callback);

/* If status is NX_SUCCESS the function “my_nak_auth_callback” has been
   registered with this PPP instance. */

VOID my_nak_auth_callback(NX_PPP *ppp_ptr)
{
   /* Handle the situation of receiving an authentication NAK */
}

```

## <a name="nx_ppp_pap_enable"></a><span data-ttu-id="b5b59-378">nx_ppp_pap_enable</span><span class="sxs-lookup"><span data-stu-id="b5b59-378">nx_ppp_pap_enable</span></span>

<span data-ttu-id="b5b59-379">PAP kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b5b59-379">Enable PAP Authentication</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-380">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-380">Prototype</span></span>

```c

UINT  nx_ppp_pap_enable(NX_PPP *ppp_ptr, 
                        UINT (*generate_login)(CHAR *name, CHAR *password),
                        UINT (*verify_login)(CHAR *name, CHAR *password));
```

### <a name="description"></a><span data-ttu-id="b5b59-381">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-381">Description</span></span>

<span data-ttu-id="b5b59-382">Bu hizmet, belirtilen PPP örneği için parola kimlik doğrulama protokolü 'Nü (PAP) sunar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-382">This service enables the Password Authentication Protocol (PAP) for the specified PPP instance.</span></span> <span data-ttu-id="b5b59-383">"***Verify_login***" işlev işaretçisi belirtilmişse, bu PPP ÖRNEĞI için PAP gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-383">If the “***verify_login***” function pointer is specified, PAP is required by this PPP instance.</span></span> <span data-ttu-id="b5b59-384">Aksi halde, PAP yalnızca LCP anlaşması sırasında belirtildiği gibi eşin PAP gereksinimlerine yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-384">Otherwise, PAP only responds to the peer’s PAP requirements as specified during LCP negotiation.</span></span>

<span data-ttu-id="b5b59-385">Gerekli geri çağırma işlevlerinde aşağıda başvurulan birkaç veri öğesi vardır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-385">There are several data items referenced below in the required callback functions.</span></span> <span data-ttu-id="b5b59-386">Veri öğesi *adının* , en fazla NX_PPP_NAME_SIZE-1 boyutuna sahip null ile sonlandırılmış dize olması beklenir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-386">The data item *name* is expected to be NULL-terminated string with a maximum size of NX_PPP_NAME_SIZE-1.</span></span> <span data-ttu-id="b5b59-387">Veri öğesi *parolasının* , en fazla NX_PPP_PASSWORD_SIZE-1 boyutuna sahip null ile sonlandırılmış bir dize olması da beklenir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-387">The data item *password* is also expected to be a NULL-terminated string with a maximum size of NX_PPP_PASSWORD_SIZE-1.</span></span>

>[!NOTE]
> <span data-ttu-id="b5b59-388">Bu işlev, *nx_ppp_create* sonra, *nx_ip_create* veya *nx_ip_interface_attach* önce çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-388">This function must be called after *nx_ppp_create* but before *nx_ip_create* or *nx_ip_interface_attach*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-389">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-389">Input Parameters</span></span>

- <span data-ttu-id="b5b59-390">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-390">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-391">**generate_login**: eş tarafından kimlik doğrulaması için *ad* ve *parola* üreten uygulama işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-391">**generate_login**: Pointer to application function that produces a *name* and *password* for authentication by the peer.</span></span> <span data-ttu-id="b5b59-392">*Ad* ve *parola* değerlerinin sağlanan hedeflere kopyalanması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b5b59-392">Note that the *name* and *password* values must be copied into the supplied destinations.</span></span>
- <span data-ttu-id="b5b59-393">**verify_login**: eş tarafından sağlanan *adı* ve *parolayı* doğrulayan uygulama işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-393">**verify_login**: Pointer to application function that verifies the *name* and *password* supplied by the peer.</span></span> <span data-ttu-id="b5b59-394">Bu yordam, sağlanan *adı* ve *parolayı* karşılaştırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-394">This routine must compare the supplied *name* and *password*.</span></span> <span data-ttu-id="b5b59-395">Bu yordam NX_SUCCESS döndürürse, ad ve parola doğru ve PPP sonraki adıma geçebilirler.</span><span class="sxs-lookup"><span data-stu-id="b5b59-395">If this routine returns NX_SUCCESS, the name and password are correct and PPP can proceed to the next step.</span></span> <span data-ttu-id="b5b59-396">Aksi takdirde, bu yordam NX_PPP_ERROR döndürür ve PPP yalnızca başka bir ad ve parola bekler.</span><span class="sxs-lookup"><span data-stu-id="b5b59-396">Otherwise, this routine returns NX_PPP_ERROR and PPP simply waits for another name and password.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-397">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-397">Return Values</span></span>

- <span data-ttu-id="b5b59-398">**NX_SUCCESS**: (0x00) başarılı PPP PAP etkinleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-398">**NX_SUCCESS**: (0x00) Successful PPP PAP enable.</span></span>
- <span data-ttu-id="b5b59-399">**NX_NOT_IMPLEMENTED**: (0x80) PAP mantığı NX_PPP_DISABLE_PAP aracılığıyla devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-399">**NX_NOT_IMPLEMENTED**: (0x80) PAP logic was disabled via NX_PPP_DISABLE_PAP.</span></span>
- <span data-ttu-id="b5b59-400">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi veya uygulama işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-400">NX_PTR_ERROR: (0x07) Invalid PPP pointer or application function pointer.</span></span>
- <span data-ttu-id="b5b59-401">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-401">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-402">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-402">Allowed From</span></span>

<span data-ttu-id="b5b59-403">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-403">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-404">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-404">Example</span></span>

```c
CHAR    name_string[] = "username";
CHAR    password_string[] =  "password";

/* Enable PAP for PPP instance “my_ppp”. */
status =  nx_ppp_pap_enable(&my_ppp, my_generate_login, my_verify_login);

/* If status is NX_SUCCESS the “my_ppp” now has PAP enabled. */

/* Define callback routines for PAP enable.  */

UINT  generate_login(CHAR *name, CHAR *password)
{

UINT    i;

for (i = 0; i< (NX_PPP_NAME_SIZE-1); i++)
name[i] = name_string[i];
name[i] =  0;

for (i = 0; i< (NX_PPP_PASSWORD_SIZE-1); i++)
password[i] = password_string[i];
password_string[i] =  0;

return(NX_SUCCESS);  
}

UINT  verify_login(CHAR *name, CHAR *password)
{

/* Assume name and password are correct. Normally, 
a comparison would be made here!  */
printf("Name: %s, Password: %s\n", name, password);

return(NX_SUCCESS);  
}
```

## <a name="nx_ppp_ping_request"></a><span data-ttu-id="b5b59-405">nx_ppp_ping_request</span><span class="sxs-lookup"><span data-stu-id="b5b59-405">nx_ppp_ping_request</span></span>

<span data-ttu-id="b5b59-406">Bir LCP ping isteği gönder</span><span class="sxs-lookup"><span data-stu-id="b5b59-406">Send an LCP ping request</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-407">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-407">Prototype</span></span>

```c
UINT  nx_ppp_ping_request(NX_PPP *ppp_ptr, CHAR *data, 
                          UINT data_size, ULONG wait_opion);
```

### <a name="description"></a><span data-ttu-id="b5b59-408">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-408">Description</span></span>

<span data-ttu-id="b5b59-409">Bu hizmet bir LCP ping isteği gönderir ve PPP cihazının yankı yanıtı beklediğini belirten bir bayrak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-409">This service sends an LCP ping request and sets a flag that the PPP device is waiting for an echo response.</span></span> <span data-ttu-id="b5b59-410">İstek gönderildikten hemen sonra hizmet döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b5b59-410">The service returns as soon as the request is sent.</span></span> <span data-ttu-id="b5b59-411">Yanıt beklemez.</span><span class="sxs-lookup"><span data-stu-id="b5b59-411">It does not wait for a response.</span></span> 

<span data-ttu-id="b5b59-412">Eşleşen bir yankı yanıtı alındığında, PPP iş parçacığı görevi bayrağı temizler.</span><span class="sxs-lookup"><span data-stu-id="b5b59-412">When a matching echo response is received, the PPP thread task will clear the flag.</span></span> <span data-ttu-id="b5b59-413">PPP cihazının, PPP anlaşmasının LCP bölümünü tamamlamış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-413">The PPP device must have completed the LCP part of the PPP negotiation.</span></span>

<span data-ttu-id="b5b59-414">Bu hizmet, bağlantı durumu için donanımın yoklanamaması mümkün olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-414">This service is useful for PPP set ups where polling the hardware for link status may not be readily possible.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-415">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-415">Input Parameters</span></span>

- <span data-ttu-id="b5b59-416">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-416">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-417">**veri**: yankı isteğine gönderilmek üzere veri işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-417">**data**: Pointer to data to send in echo request.</span></span>
- <span data-ttu-id="b5b59-418">**data_size**: LCP yankı iletisini göndermek için beklenecek wait_option zaman göndermek için veri boyutu.</span><span class="sxs-lookup"><span data-stu-id="b5b59-418">**data_size**: Size of data to send wait_option Time to wait to send the LCP echo message.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-419">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-419">Return Values</span></span>

- <span data-ttu-id="b5b59-420">**NX_SUCCESS**: (0x00) gönderilen yankı Isteği başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="b5b59-420">**NX_SUCCESS**: (0x00) Successful sent echo request.</span></span>
- <span data-ttu-id="b5b59-421">**NX_PPP_NOT_ESTABLISHED**: (0xb5) PPP bağlantısı kurulmadı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-421">**NX_PPP_NOT_ESTABLISHED**: (0xB5) PPP connection not established.</span></span>
- <span data-ttu-id="b5b59-422">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi veya uygulama işlevi işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-422">NX_PTR_ERROR: (0x07) Invalid PPP pointer or application function pointer.</span></span>
- <span data-ttu-id="b5b59-423">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-423">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-424">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-424">Allowed From</span></span>

<span data-ttu-id="b5b59-425">Uygulama iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-425">Application threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-426">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-426">Example</span></span>

```c

CHAR    buffer[] = "username";
UINT    buffer_length =  strlen("username ");

/* Send an LCP ping request”. */
status =  nx_ppp_ping_request(&my_ppp, &buffer[0], buffer_length, 200);

/* If status is NX_SUCCESS the LCP echo request was successfully sent. Now wait to 
   receive a response. */

while(my_ppp.nx_ppp_lcp_echo_reply_id > 0)
{
    tx_thread_sleep(100);
}

/* Got a valid reply! */
```

## <a name="nx_ppp_raw_string_send"></a><span data-ttu-id="b5b59-427">nx_ppp_raw_string_send</span><span class="sxs-lookup"><span data-stu-id="b5b59-427">nx_ppp_raw_string_send</span></span>

<span data-ttu-id="b5b59-428">Ham ASCII dizesi gönder</span><span class="sxs-lookup"><span data-stu-id="b5b59-428">Send a raw ASCII string</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-429">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-429">Prototype</span></span>

```c
UINT  nx_ppp_raw_sting_send(NX_PPP *ppp_ptr, CHAR *string_ptr);
```

### <a name="description"></a><span data-ttu-id="b5b59-430">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-430">Description</span></span>

<span data-ttu-id="b5b59-431">Bu hizmet, PPP arabiriminden doğrudan PPP olmayan bir ASCII dizesi gönderir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-431">This service sends a non-PPP ASCII string directly out the PPP interface.</span></span> <span data-ttu-id="b5b59-432">PPP, modem denetimi bilgilerini içeren PPP olmayan bir paket aldıktan sonra genellikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-432">It is typically used after PPP receives a non-PPP packet that contains modem control information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-433">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-433">Input Parameters</span></span>

- <span data-ttu-id="b5b59-434">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-434">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-435">**string_ptr**: gönderileceği dize işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-435">**string_ptr**: Pointer to string to send.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-436">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-436">Return Values</span></span>

- <span data-ttu-id="b5b59-437">**NX_SUCCESS**: (0x00) başarılı PPP ham dize gönderme.</span><span class="sxs-lookup"><span data-stu-id="b5b59-437">**NX_SUCCESS**: (0x00) Successful PPP raw string send.</span></span>
- <span data-ttu-id="b5b59-438">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi veya dize işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-438">NX_PTR_ERROR: (0x07) Invalid PPP pointer or string pointer.</span></span>
- <span data-ttu-id="b5b59-439">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-439">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-440">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-440">Allowed From</span></span>

<span data-ttu-id="b5b59-441">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-441">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-442">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-442">Example</span></span>

```c

/* Send “CLIENTSERVER” to “CLIENT” sent by Windows 98 before PPP is
initiated.  */
status =  nx_ppp_raw_string_send(&my_ppp, “CLIENTSERVER”);

/* If status is NX_SUCCESS the raw string was successfully Sent via PPP. */
```
## <a name="nx_ppp_restart"></a><span data-ttu-id="b5b59-443">nx_ppp_restart</span><span class="sxs-lookup"><span data-stu-id="b5b59-443">nx_ppp_restart</span></span>

<span data-ttu-id="b5b59-444">PPP işlemesini yeniden Başlat</span><span class="sxs-lookup"><span data-stu-id="b5b59-444">Restart PPP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-445">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-445">Prototype</span></span>

```c
UINT  nx_ppp_restart(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="b5b59-446">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-446">Description</span></span>

<span data-ttu-id="b5b59-447">Bu hizmet, PPP işlemini yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-447">This service restarts the PPP processing.</span></span> <span data-ttu-id="b5b59-448">Genellikle bağlantının bir bağlantı geri çağrısından veya iletişimin kaybedilmediğini belirten PPP olmayan bir modem iletisiyle yeniden oluşturulması gerektiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-448">It is typically called when the link needs to be re-established either from a link down callback or by a non-PPP modem message indicating communication was lost.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-449">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-449">Input Parameters</span></span>

- <span data-ttu-id="b5b59-450">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-450">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-451">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-451">Return Values</span></span>

- <span data-ttu-id="b5b59-452">**NX_SUCCESS**: (0x00) başarılı PPP yeniden başlatması başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-452">**NX_SUCCESS**: (0x00) Successful PPP restart initiated.</span></span>
- <span data-ttu-id="b5b59-453">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-453">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="b5b59-454">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-454">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-455">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-455">Allowed From</span></span>

<span data-ttu-id="b5b59-456">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-456">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-457">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-457">Example</span></span>

```c
/* Restart the PPP instance “my_ppp”.  */
status =  nx_ppp_restart(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been restarted. */
```

## <a name="nx_ppp_start"></a><span data-ttu-id="b5b59-458">nx_ppp_start</span><span class="sxs-lookup"><span data-stu-id="b5b59-458">nx_ppp_start</span></span>

<span data-ttu-id="b5b59-459">PPP işlemesini Başlat</span><span class="sxs-lookup"><span data-stu-id="b5b59-459">Start PPP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-460">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-460">Prototype</span></span>

```c
UINT  nx_ppp_start(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="b5b59-461">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-461">Description</span></span>

<span data-ttu-id="b5b59-462">Bu hizmet, PPP işlemini başlatır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-462">This service starts the PPP processing.</span></span> <span data-ttu-id="b5b59-463">Genellikle nx_ppp_stop () çağrıldıktan sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-463">It is typically called after nx_ppp_stop() called.</span></span>

>[!NOTE]
> <span data-ttu-id="b5b59-464">PPP, bağlantı etkinleştirildiğinde otomatik olarak PPP işlemini başlatır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-464">PPP automatically starts the PPP processing when the link is enabled.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-465">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-465">Input Parameters</span></span>

- <span data-ttu-id="b5b59-466">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-466">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-467">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-467">Return Values</span></span>

- <span data-ttu-id="b5b59-468">**NX_SUCCESS**: (0x00) başarılı PPP başlatması başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-468">**NX_SUCCESS**: (0x00) Successful PPP start initiated.</span></span> 
- <span data-ttu-id="b5b59-469">**NX_PPP_ALREADY_STARTED**: (0xB9) PPP zaten başlatılmış.</span><span class="sxs-lookup"><span data-stu-id="b5b59-469">**NX_PPP_ALREADY_STARTED**: (0xb9) PPP already started.</span></span>
- <span data-ttu-id="b5b59-470">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-470">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="b5b59-471">NX_CALLER_ERROR: (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-471">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-472">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-472">Allowed From</span></span>

<span data-ttu-id="b5b59-473">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-473">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-474">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-474">Example</span></span>

```c
/* Start the PPP instance “my_ppp”.  */
status =  nx_ppp_start(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been started. */
```

## <a name="nx_ppp_status_get"></a><span data-ttu-id="b5b59-475">nx_ppp_status_get</span><span class="sxs-lookup"><span data-stu-id="b5b59-475">nx_ppp_status_get</span></span>

<span data-ttu-id="b5b59-476">Geçerli PPP durumunu al</span><span class="sxs-lookup"><span data-stu-id="b5b59-476">Get current PPP status</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-477">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-477">Prototype</span></span>

```c
UINT  nx_ppp_status_get(NX_PPP *ppp_ptr, UINT *status_ptr);
```
### <a name="description"></a><span data-ttu-id="b5b59-478">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-478">Description</span></span>

<span data-ttu-id="b5b59-479">Bu hizmet, belirtilen PPP örneğinin geçerli durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-479">This service gets the current status of the specified PPP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-480">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-480">Input Parameters</span></span>

- <span data-ttu-id="b5b59-481">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-481">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-482">**status_ptr**: PPP durumunun hedefi, aşağıdakiler olası durum değerleridir:</span><span class="sxs-lookup"><span data-stu-id="b5b59-482">**status_ptr**: Destination for the PPP status, the following are possible status values:</span></span>
    - <span data-ttu-id="b5b59-483">**NX_PPP_STATUS_ESTABLISHED**</span><span class="sxs-lookup"><span data-stu-id="b5b59-483">**NX_PPP_STATUS_ESTABLISHED**</span></span>
    - <span data-ttu-id="b5b59-484">**NX_PPP_STATUS_LCP_IN_PROGRESS**</span><span class="sxs-lookup"><span data-stu-id="b5b59-484">**NX_PPP_STATUS_LCP_IN_PROGRESS**</span></span>
    - <span data-ttu-id="b5b59-485">**NX_PPP_STATUS_LCP_FAILED**</span><span class="sxs-lookup"><span data-stu-id="b5b59-485">**NX_PPP_STATUS_LCP_FAILED**</span></span>
    - <span data-ttu-id="b5b59-486">**NX_PPP_STATUS_PAP_IN_PROGRESS**</span><span class="sxs-lookup"><span data-stu-id="b5b59-486">**NX_PPP_STATUS_PAP_IN_PROGRESS**</span></span>
    - <span data-ttu-id="b5b59-487">**NX_PPP_STATUS_PAP_FAILED**</span><span class="sxs-lookup"><span data-stu-id="b5b59-487">**NX_PPP_STATUS_PAP_FAILED**</span></span>
    - <span data-ttu-id="b5b59-488">**NX_PPP_STATUS_CHAP_IN_PROGRESS**</span><span class="sxs-lookup"><span data-stu-id="b5b59-488">**NX_PPP_STATUS_CHAP_IN_PROGRESS**</span></span>
    - <span data-ttu-id="b5b59-489">**NX_PPP_STATUS_CHAP_FAILED**</span><span class="sxs-lookup"><span data-stu-id="b5b59-489">**NX_PPP_STATUS_CHAP_FAILED**</span></span>
    - <span data-ttu-id="b5b59-490">**NX_PPP_STATUS_IPCP_IN_PROGRESS**</span><span class="sxs-lookup"><span data-stu-id="b5b59-490">**NX_PPP_STATUS_IPCP_IN_PROGRESS**</span></span>
    - <span data-ttu-id="b5b59-491">**NX_PPP_STATUS_IPCP_FAILED**</span><span class="sxs-lookup"><span data-stu-id="b5b59-491">**NX_PPP_STATUS_IPCP_FAILED**</span></span>

>[!NOTE]
> <span data-ttu-id="b5b59-492">Durum yalnızca API NX_SUCCESS döndürürse geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b5b59-492">The status is only valid if the API returns NX_SUCCESS.</span></span> <span data-ttu-id="b5b59-493">Ayrıca, \* _FAILED durum değerlerinden herhangi biri döndürülürse, PPP işleme, uygulama tarafından yeniden başlatılana kadar etkili bir şekilde durdurulur.</span><span class="sxs-lookup"><span data-stu-id="b5b59-493">In addition, if any of the \*_FAILED status values are returned, PPP processing is effectively stopped until it is restarted again by the application.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-494">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-494">Return Values</span></span>

- <span data-ttu-id="b5b59-495">**NX_SUCCESS**: (0x00) başarılı PPP durum isteği.</span><span class="sxs-lookup"><span data-stu-id="b5b59-495">**NX_SUCCESS**: (0x00) Successful PPP status request.</span></span>
- <span data-ttu-id="b5b59-496">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-496">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-497">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-497">Allowed From</span></span>

<span data-ttu-id="b5b59-498">Başlatma, iş parçacıkları, zamanlayıcılar, ISRs</span><span class="sxs-lookup"><span data-stu-id="b5b59-498">Initialization, threads, timers, ISRs</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-499">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-499">Example</span></span>

```c
UINT ppp_status;
UINT status;


/* Get the current status of PPP instance “my_ppp”.  */
status =  nx_ppp_status_get(&my_ppp, &ppp_status);

/* If status is NX_SUCCESS the current internal PPP status is contained in
   “ppp_status”. */
```
## <a name="nx_ppp_stop"></a><span data-ttu-id="b5b59-500">nx_ppp_stop</span><span class="sxs-lookup"><span data-stu-id="b5b59-500">nx_ppp_stop</span></span>

<span data-ttu-id="b5b59-501">PPP işlemesini Başlat</span><span class="sxs-lookup"><span data-stu-id="b5b59-501">Start PPP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-502">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-502">Prototype</span></span>

```c
UINT  nx_ppp_stop(NX_PPP *ppp_ptr);
```

### <a name="description"></a><span data-ttu-id="b5b59-503">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-503">Description</span></span>

<span data-ttu-id="b5b59-504">Bu hizmet, PPP işlemini durduruyor.</span><span class="sxs-lookup"><span data-stu-id="b5b59-504">This service stops the PPP processing.</span></span> <span data-ttu-id="b5b59-505">Kullanıcı ayrıca, gerekirse PPP işlemini başlatmak için nx_ppp_start () öğesini de çağırır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-505">User also can calls nx_ppp_start() to start the PPP processing if needed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-506">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-506">Input Parameters</span></span>

- <span data-ttu-id="b5b59-507">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-507">**ppp_ptr**: Pointer to PPP control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-508">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-508">Return Values</span></span>

- <span data-ttu-id="b5b59-509">**NX_SUCCESS**: (0x00) başarılı PPP başlatması başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-509">**NX_SUCCESS**: (0x00) Successful PPP start initiated.</span></span> 
- <span data-ttu-id="b5b59-510">**NX_PPP_ALREADY_STOPPED**: (0xB8) PPP zaten durduruldu.</span><span class="sxs-lookup"><span data-stu-id="b5b59-510">**NX_PPP_ALREADY_STOPPED**: (0xb8) PPP already stopped.</span></span>
- <span data-ttu-id="b5b59-511">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-511">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>
- <span data-ttu-id="b5b59-512">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-512">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-513">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-513">Allowed From</span></span>

<span data-ttu-id="b5b59-514">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-514">Threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-515">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-515">Example</span></span>

```c
/* Stop the PPP instance “my_ppp”.  */
status =  nx_ppp_stop(&my_ppp);

/* If status is NX_SUCCESS the PPP instance has been stopped. */
```
## <a name="nx_ppp_packet_receive"></a><span data-ttu-id="b5b59-516">nx_ppp_packet_receive</span><span class="sxs-lookup"><span data-stu-id="b5b59-516">nx_ppp_packet_receive</span></span>

<span data-ttu-id="b5b59-517">PPP paketi al</span><span class="sxs-lookup"><span data-stu-id="b5b59-517">Receive PPP packet</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-518">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-518">Prototype</span></span>

```c
UINT  nx_ppp_packet_receive(NX_PPP *ppp_ptr, NX_PACKET *packet_ptr);

```

### <a name="description"></a><span data-ttu-id="b5b59-519">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-519">Description</span></span>

<span data-ttu-id="b5b59-520">Bu hizmet, PPP paketini alır.</span><span class="sxs-lookup"><span data-stu-id="b5b59-520">This service receives PPP packet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-521">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-521">Input Parameters</span></span>

- <span data-ttu-id="b5b59-522">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-522">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-523">**packet_ptr**: PPP paketine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-523">**packet_ptr**: Pointer to PPP packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-524">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-524">Return Values</span></span>

- <span data-ttu-id="b5b59-525">**NX_SUCCESS**: (0x00) başarılı PPP durum isteği.</span><span class="sxs-lookup"><span data-stu-id="b5b59-525">**NX_SUCCESS**: (0x00) Successful PPP status request.</span></span>
- <span data-ttu-id="b5b59-526">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-526">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-527">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-527">Allowed From</span></span>

<span data-ttu-id="b5b59-528">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-528">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-529">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-529">Example</span></span>

```c
/* Receive the PPP packet of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_receive(&my_ppp, packet_ptr);

/* If status is NX_SUCCESS the PPP packet has received. */


```
## <a name="nx_ppp_packet_send_set"></a><span data-ttu-id="b5b59-530">nx_ppp_packet_send_set</span><span class="sxs-lookup"><span data-stu-id="b5b59-530">nx_ppp_packet_send_set</span></span>

<span data-ttu-id="b5b59-531">PPP paketi gönderme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="b5b59-531">Set the PPP packet send function</span></span>

### <a name="prototype"></a><span data-ttu-id="b5b59-532">Prototype</span><span class="sxs-lookup"><span data-stu-id="b5b59-532">Prototype</span></span>

```c
UINT  nx_ppp_packet_send_set(NX_PPP *ppp_ptr, 
                             VOID (*nx_ppp_packet_send)(NX_PACKET *packet_ptr));

```

### <a name="description"></a><span data-ttu-id="b5b59-533">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b59-533">Description</span></span>

<span data-ttu-id="b5b59-534">Bu hizmet, PPP paketi gönderme funcıton 'i ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b5b59-534">This service sets the PPP packet send funciton.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b5b59-535">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-535">Input Parameters</span></span>

- <span data-ttu-id="b5b59-536">**ppp_ptr**: PPP denetim bloğu işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-536">**ppp_ptr**: Pointer to PPP control block.</span></span>
- <span data-ttu-id="b5b59-537">**nx_ppp_packet_send**: PPP paketi gönderme yordamı.</span><span class="sxs-lookup"><span data-stu-id="b5b59-537">**nx_ppp_packet_send**: Routine to send PPP packet.</span></span>

### <a name="return-values"></a><span data-ttu-id="b5b59-538">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="b5b59-538">Return Values</span></span>

- <span data-ttu-id="b5b59-539">**NX_SUCCESS**: (0x00) başarılı PPP durum isteği.</span><span class="sxs-lookup"><span data-stu-id="b5b59-539">**NX_SUCCESS**: (0x00) Successful PPP status request.</span></span>
- <span data-ttu-id="b5b59-540">NX_PTR_ERROR: (0x07) geçersiz PPP işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="b5b59-540">NX_PTR_ERROR: (0x07) Invalid PPP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="b5b59-541">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="b5b59-541">Allowed From</span></span>

<span data-ttu-id="b5b59-542">Başlatma, iş parçacıkları</span><span class="sxs-lookup"><span data-stu-id="b5b59-542">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="b5b59-543">Örnek</span><span class="sxs-lookup"><span data-stu-id="b5b59-543">Example</span></span>

```c
/* Set the PPP packet send function of PPP instance “my_ppp”.  */
status =  nx_ppp_packet_send_set(&my_ppp, nx_ppp_packet_send);

/* If status is NX_SUCCESS the PPP packet send function has set. */


```