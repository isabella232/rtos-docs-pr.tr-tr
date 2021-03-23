---
title: Bölüm 3-Azure RTOS NetX POP3 Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm Azure RTOS NetX POP3 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1a0ab96a454bea9f56ced0d7aa8de5d481b284e9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826662"
---
# <a name="chapter-3---description-of-azure-rtos-netx-pop3-client-services"></a><span data-ttu-id="fe1ce-103">Bölüm 3-Azure RTOS NetX POP3 Istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="fe1ce-103">Chapter 3 - Description of Azure RTOS NetX POP3 Client services</span></span>

<span data-ttu-id="fe1ce-104">Bu bölüm, tüm Azure RTOS NetX POP3 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-104">This chapter contains a description of all Azure RTOS NetX POP3 Client services (listed below) in alphabetical order.</span></span>

<span data-ttu-id="fe1ce-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="fe1ce-106">nx_pop3_client_create: *BIR POP3 Istemci örneği oluşturma*</span><span class="sxs-lookup"><span data-stu-id="fe1ce-106">nx_pop3_client_create: *Create a POP3 Client Instance*</span></span>
- <span data-ttu-id="fe1ce-107">nx_pop3_client_delete: *BIR POP3 istemci örneğini silme*</span><span class="sxs-lookup"><span data-stu-id="fe1ce-107">nx_pop3_client_delete: *Delete a POP3 Client instance*</span></span>
- <span data-ttu-id="fe1ce-108">nx_pop3_client_ mail_item_get: *sunucu maildrop 'dan bir istemci posta öğesini silme*</span><span class="sxs-lookup"><span data-stu-id="fe1ce-108">nx_pop3_client_ mail_item_get: *Delete a Client mail item from Server maildrop*</span></span>
- <span data-ttu-id="fe1ce-109">nx_pop3_client_mail_item_get: *belirli bir posta iletisi boyutunu alın*</span><span class="sxs-lookup"><span data-stu-id="fe1ce-109">nx_pop3_client_mail_item_get: *Retrieve a specific mail message size*</span></span>
- <span data-ttu-id="fe1ce-110">nx_pop3_client_mail_items_get: *maildrop 'daki posta öğelerinin sayısını alma*</span><span class="sxs-lookup"><span data-stu-id="fe1ce-110">nx_pop3_client_mail_items_get: *Obtain the number of mail items in maildrop*</span></span>
- <span data-ttu-id="fe1ce-111">nx_pop3_client_mail_item_message _get: *belirli bir posta Iletisini indirin*</span><span class="sxs-lookup"><span data-stu-id="fe1ce-111">nx_pop3_client_mail_item_message _get: *Download a specific mail message*</span></span>
- <span data-ttu-id="fe1ce-112">nx_pop3_client_mail_item_size_get: *belirli bir posta öğesinin boyutunu alma*</span><span class="sxs-lookup"><span data-stu-id="fe1ce-112">nx_pop3_client_mail_item_size_get: *Obtain the size of a specific mail item*</span></span>

## <a name="nx_pop3_client_create"></a><span data-ttu-id="fe1ce-113">nx_pop3_client_create</span><span class="sxs-lookup"><span data-stu-id="fe1ce-113">nx_pop3_client_create</span></span>

<span data-ttu-id="fe1ce-114">POP3 Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe1ce-114">Create a POP3 Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="fe1ce-115">Prototype</span><span class="sxs-lookup"><span data-stu-id="fe1ce-115">Prototype</span></span>

```c
UINT nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
                        UINT APOP_authentication, NX_IP *ip_ptr,
                        NX_PACKET_POOL *packet_pool_ptr,
                        ULONG server_ip_address,
                        ULONG server_port,
                        CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a><span data-ttu-id="fe1ce-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe1ce-116">Description</span></span>

<span data-ttu-id="fe1ce-117">Bu hizmet, POP3 Istemcisinin bir örneğini oluşturur ve yapılandırmasını giriş parametreleriyle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-117">This service creates an instance of the POP3 Client and sets up its configuration with the input parameters.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fe1ce-118">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-118">Input Parameters</span></span>

- <span data-ttu-id="fe1ce-119">**client_ptr**: oluşturulacak istemciye yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-119">**client_ptr**: Pointer to Client to create</span></span>
- <span data-ttu-id="fe1ce-120">**APOP_authentication**: APOP kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fe1ce-120">**APOP_authentication**: Enable APOP authentication</span></span>
- <span data-ttu-id="fe1ce-121">**ip_ptr**: IP örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-121">**ip_ptr**: Pointer to IP instance</span></span>
- <span data-ttu-id="fe1ce-122">**packet_pool_ptr**: istemci paket havuzuna yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-122">**packet_pool_ptr**: Pointer to Client packet pool</span></span>
- <span data-ttu-id="fe1ce-123">**server_ip_address**: POP3 sunucu adresi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-123">**server_ip_address**: POP3 server address</span></span>
- <span data-ttu-id="fe1ce-124">**SERVER_PORT**: POP3 sunucu bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="fe1ce-124">**server_port**: POP3 server port</span></span>
- <span data-ttu-id="fe1ce-125">**client_name**: istemci adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-125">**client_name**: Pointer to Client name</span></span>
- <span data-ttu-id="fe1ce-126">**client_password**: istemci parolası işaretçisi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-126">**client_password**: Pointer to Client password</span></span>

### <a name="return-values"></a><span data-ttu-id="fe1ce-127">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-127">Return Values</span></span>

- <span data-ttu-id="fe1ce-128">**NX_SUCCESS**: (0x00) istemci başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="fe1ce-128">**NX_SUCCESS**: (0x00) Client successfully created</span></span>
- <span data-ttu-id="fe1ce-129">**durum**: NETX ve threadx hizmeti çağrılarının durum bitimi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-129">**status**: Status completion of NetX and ThreadX service calls</span></span>
- <span data-ttu-id="fe1ce-130">NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-130">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="fe1ce-131">NX_POP3_PARAM_ERROR: (0xB1) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-131">NX_POP3_PARAM_ERROR: (0xB1) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fe1ce-132">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fe1ce-132">Allowed From</span></span>

<span data-ttu-id="fe1ce-133">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="fe1ce-133">Application code</span></span>

### <a name="example"></a><span data-ttu-id="fe1ce-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="fe1ce-134">Example</span></span>

```c
/* Create the POP3 Client. */

/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST                   "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD          "pass"
#define POP3_SERVER_ADDRESS         IP_ADDRESS(192,2,2,92
#define POP3_SERVER_PORT            110

/* Create a NetX POP3 Client instance. */
ULONG server_ip_address = IP_ADDRESS(1,2,3,4);
status = nx_pop3_client_create(&demo_client,
        NX_FALSE /* disable APOP authentication */,
        &client_ip, &client_packet_pool,
        server_ip_address, POP3_SERVER_PORT,
        LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_delete"></a><span data-ttu-id="fe1ce-135">nx_pop3_client_delete</span><span class="sxs-lookup"><span data-stu-id="fe1ce-135">nx_pop3_client_delete</span></span>

<span data-ttu-id="fe1ce-136">POP3 Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="fe1ce-136">Delete a POP3 Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="fe1ce-137">Prototype</span><span class="sxs-lookup"><span data-stu-id="fe1ce-137">Prototype</span></span>

```c
UINT nx_pop3_client_delete(NX_POP3_CLIENT *client_ptr)
```

### <a name="description"></a><span data-ttu-id="fe1ce-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe1ce-138">Description</span></span>

<span data-ttu-id="fe1ce-139">Bu hizmet önceden oluşturulmuş bir POP3 Istemcisini siler.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-139">This service deletes a previously created POP3 Client.</span></span> <span data-ttu-id="fe1ce-140">Bu hizmet POP3 Istemci paket havuzunu silmez.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-140">Not that this service does not delete the POP3 Client packet pool.</span></span> <span data-ttu-id="fe1ce-141">Cihaz uygulamasının artık paket havuzu için kullanımı gerekmiyorsa, bu kaynağı ayrı olarak silmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-141">The device application must delete this resource separately if it no longer has use for the packet pool.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fe1ce-142">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-142">Input Parameters</span></span>

- <span data-ttu-id="fe1ce-143">**client_ptr**: silinecek istemciye yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-143">**client_ptr**: Pointer to Client to delete</span></span>

### <a name="return-values"></a><span data-ttu-id="fe1ce-144">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-144">Return Values</span></span>

- <span data-ttu-id="fe1ce-145">**NX_SUCCESS**: (0x00) istemci başarıyla silindi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-145">**NX_SUCCESS**: (0x00) Client successfully deleted</span></span>
- <span data-ttu-id="fe1ce-146">NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-146">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fe1ce-147">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fe1ce-147">Allowed From</span></span>

<span data-ttu-id="fe1ce-148">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="fe1ce-148">Application code</span></span>

### <a name="example"></a><span data-ttu-id="fe1ce-149">Örnek</span><span class="sxs-lookup"><span data-stu-id="fe1ce-149">Example</span></span>

```c
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a><span data-ttu-id="fe1ce-150">nx_pop3_client_mail_item_delete</span><span class="sxs-lookup"><span data-stu-id="fe1ce-150">nx_pop3_client_mail_item_delete</span></span>

<span data-ttu-id="fe1ce-151">Istemci maildrop 'tan belirtilen bir posta öğesini silme</span><span class="sxs-lookup"><span data-stu-id="fe1ce-151">Delete a specified mail item from the Client maildrop</span></span>

### <a name="prototype"></a><span data-ttu-id="fe1ce-152">Prototype</span><span class="sxs-lookup"><span data-stu-id="fe1ce-152">Prototype</span></span>

```c
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
                                    UINT mail_index)
```

### <a name="description"></a><span data-ttu-id="fe1ce-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe1ce-153">Description</span></span>

<span data-ttu-id="fe1ce-154">Bu hizmet, belirtilen posta öğesini Istemci maildrop 'dan siler.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-154">This service deletes the specified mail item from the Client maildrop.</span></span> <span data-ttu-id="fe1ce-155">Posta öğesi indirildikten sonra, bazı POP3 sunucuları, Istemci tarafından istendikten sonra posta öğelerini otomatik olarak silebilir.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-155">It is intended for after downloading the mail item, although some POP3 servers may automatically delete mail items after being requested by the Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fe1ce-156">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-156">Input Parameters</span></span>

- <span data-ttu-id="fe1ce-157">**client_ptr**: istemci örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-157">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="fe1ce-158">**mail_index**: istemci maildrop 'a Dizin</span><span class="sxs-lookup"><span data-stu-id="fe1ce-158">**mail_index**: Index into Client maildrop</span></span>

### <a name="return-values"></a><span data-ttu-id="fe1ce-159">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-159">Return Values</span></span>

- <span data-ttu-id="fe1ce-160">**NX_SUCCESS**: (0x00) silme isteği başarılı</span><span class="sxs-lookup"><span data-stu-id="fe1ce-160">**NX_SUCCESS**: (0x00) Delete request successful</span></span>
- <span data-ttu-id="fe1ce-161">**NX_POP3_INVALID_MAIL_ITEM**: (0Xb2) geçersiz posta öğesi dizini</span><span class="sxs-lookup"><span data-stu-id="fe1ce-161">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="fe1ce-162">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0Xb6) istemci paket yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-162">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="fe1ce-163">**NX_POP3_SERVER_ERROR_STATUS**: (0Xb4) sunucu, hata durumuyla yanıt verir</span><span class="sxs-lookup"><span data-stu-id="fe1ce-163">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="fe1ce-164">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) geçersiz posta dizini girişi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-164">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="fe1ce-165">NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-165">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fe1ce-166">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fe1ce-166">Allowed From</span></span>

<span data-ttu-id="fe1ce-167">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="fe1ce-167">Application code</span></span>

### <a name="example"></a><span data-ttu-id="fe1ce-168">Örnek</span><span class="sxs-lookup"><span data-stu-id="fe1ce-168">Example</span></span>

```c
ULONG     item_index;

/* Delete the POP3 Client mail item. */
status = nx_pop3_client_mail_item_delete(&demo_client, item_index);

/* If the server accepts the DELE request (and deletes the mail item), status = 
   NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_get"></a><span data-ttu-id="fe1ce-169">nx_pop3_client_mail_item_get</span><span class="sxs-lookup"><span data-stu-id="fe1ce-169">nx_pop3_client_mail_item_get</span></span>

<span data-ttu-id="fe1ce-170">Belirtilen posta öğesini alma</span><span class="sxs-lookup"><span data-stu-id="fe1ce-170">Retrieve a specified mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="fe1ce-171">Prototype</span><span class="sxs-lookup"><span data-stu-id="fe1ce-171">Prototype</span></span>

```c
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
                                UINT mail_item, ULONG *item_size)
```

### <a name="description"></a><span data-ttu-id="fe1ce-172">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe1ce-172">Description</span></span>

<span data-ttu-id="fe1ce-173">Bu hizmet, Dizin mail_item tarafından belirtilen Istemci maildrop öğesinden bir posta öğesi almaya yönelik bir RETR isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-173">This service makes a RETR request to retrieve a mail item from the Client maildrop specified by the index mail_item.</span></span> <span data-ttu-id="fe1ce-174">Bir RETR isteği yaptıktan ve sunucudan olumlu bir yanıt aldıktan sonra Istemci, *nx_pop3_client_mail_item_message_get* hizmetini kullanarak posta iletisini indirmeye başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-174">After making a RETR request, and receiving a positive response from the Server, the Client can start downloading the mail message using the *nx_pop3_client_mail_item_message_get* service.</span></span> <span data-ttu-id="fe1ce-175">Hizmetin, sunucu yanıtlarından ayıklanan istenen posta öğesinin boyutunu da sağladığı unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-175">Note that the service also supplies the size of the requested mail item extracted from the Server reply.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fe1ce-176">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-176">Input Parameters</span></span>

- <span data-ttu-id="fe1ce-177">**client_ptr**: istemci örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-177">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="fe1ce-178">**mail_item**: istemci maildrop 'a Dizin</span><span class="sxs-lookup"><span data-stu-id="fe1ce-178">**mail_item**: Index into Client maildrop</span></span>
- <span data-ttu-id="fe1ce-179">**item_size**: posta iletisi boyutu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-179">**item_size**: Pointer to size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="fe1ce-180">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-180">Return Values</span></span>

- <span data-ttu-id="fe1ce-181">**NX_SUCCESS**: (0x00) posta öğesi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="fe1ce-181">**NX_SUCCESS**: (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="fe1ce-182">**NX_POP3_INVALID_MAIL_ITEM**: (0Xb2) geçersiz posta öğesi dizini</span><span class="sxs-lookup"><span data-stu-id="fe1ce-182">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="fe1ce-183">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0Xb6) istemci paket yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-183">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="fe1ce-184">**NX_POP3_SERVER_ERROR_STATUS**: (0Xb4) sunucu, hata durumuyla yanıt verir</span><span class="sxs-lookup"><span data-stu-id="fe1ce-184">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="fe1ce-185">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) geçersiz posta dizini girişi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-185">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="fe1ce-186">NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-186">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fe1ce-187">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fe1ce-187">Allowed From</span></span>

<span data-ttu-id="fe1ce-188">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="fe1ce-188">Application code</span></span>

### <a name="example"></a><span data-ttu-id="fe1ce-189">Örnek</span><span class="sxs-lookup"><span data-stu-id="fe1ce-189">Example</span></span>

```c
ULONG     item_size;

/* Retrieve the POP3 Client mail item. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &item_size);

/* If the mail item was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_items_get"></a><span data-ttu-id="fe1ce-190">nx_pop3_client_mail_items_get</span><span class="sxs-lookup"><span data-stu-id="fe1ce-190">nx_pop3_client_mail_items_get</span></span>

<span data-ttu-id="fe1ce-191">Maildrop 'daki posta öğelerinin sayısını alma</span><span class="sxs-lookup"><span data-stu-id="fe1ce-191">Retrieve the number of mail items in maildrop</span></span>

### <a name="prototype"></a><span data-ttu-id="fe1ce-192">Prototype</span><span class="sxs-lookup"><span data-stu-id="fe1ce-192">Prototype</span></span>

```c
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
                                UINT *number_mail_items,
                                ULONG *maildrop_total_size)
```

### <a name="description"></a><span data-ttu-id="fe1ce-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe1ce-193">Description</span></span>

<span data-ttu-id="fe1ce-194">Bu hizmet, posta öğelerinin sayısını ve Istemci maildrop 'tan gelen posta iletisi verilerinin toplam boyutunu almak için bir STAT isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-194">This service makes a STAT request to retrieve the number of mail items and total size of mail message data from the Client maildrop.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fe1ce-195">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-195">Input Parameters</span></span>

- <span data-ttu-id="fe1ce-196">**client_ptr**: istemci örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-196">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="fe1ce-197">**number_mail_item**: istemci maildrop 'daki posta sayısı</span><span class="sxs-lookup"><span data-stu-id="fe1ce-197">**number_mail_item**: Number of mail in Client maildrop</span></span>
- <span data-ttu-id="fe1ce-198">**maildrop_total_size**: tüm posta iletisinin boyutu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-198">**maildrop_total_size**: Pointer to size of all mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="fe1ce-199">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-199">Return Values</span></span>

- <span data-ttu-id="fe1ce-200">**NX_SUCCESS**: (0x00) posta öğesi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="fe1ce-200">**NX_SUCCESS**: (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="fe1ce-201">**NX_POP3_INVALID_MAIL_ITEM**: (0Xb2) geçersiz posta öğesi dizini</span><span class="sxs-lookup"><span data-stu-id="fe1ce-201">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="fe1ce-202">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0Xb6) istemci paket yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-202">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="fe1ce-203">**NX_POP3_SERVER_ERROR_STATUS**: (0Xb4) sunucu, hata durumuyla yanıt verir</span><span class="sxs-lookup"><span data-stu-id="fe1ce-203">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) Server replies with error status</span></span> 
- <span data-ttu-id="fe1ce-204">NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-204">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fe1ce-205">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fe1ce-205">Allowed From</span></span>

<span data-ttu-id="fe1ce-206">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="fe1ce-206">Application code</span></span>

### <a name="example"></a><span data-ttu-id="fe1ce-207">Örnek</span><span class="sxs-lookup"><span data-stu-id="fe1ce-207">Example</span></span>

```c
UINT      number_mail_items;
ULONG     maildrop_total_size;

/* Retrieve the size and number of items in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &number_mail_items,
                                        &maildrop_total_size);

/* If the maildrop data was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_message_get"></a><span data-ttu-id="fe1ce-208">nx_pop3_client_mail_item_message_get</span><span class="sxs-lookup"><span data-stu-id="fe1ce-208">nx_pop3_client_mail_item_message_get</span></span>

<span data-ttu-id="fe1ce-209">Belirtilen posta öğesi iletisini Al</span><span class="sxs-lookup"><span data-stu-id="fe1ce-209">Retrieve the specified mail item message</span></span>

### <a name="prototype"></a><span data-ttu-id="fe1ce-210">Prototype</span><span class="sxs-lookup"><span data-stu-id="fe1ce-210">Prototype</span></span>

```c
UINT nx_pop3_client_mail_item_message_get(
                NX_POP3_CLIENT *client_ptr,
                NX_PACKET **recv_packet_ptr,
                ULONG *bytes_retrieved,
                UINT *final_packet)
```

### <a name="description"></a><span data-ttu-id="fe1ce-211">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe1ce-211">Description</span></span>

<span data-ttu-id="fe1ce-212">Bu hizmet posta öğesi iletisini, posta iletisinin boyutunu ve posta iletisindeki son paket ise alır.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-212">This service retrieves the mail item message, size of the mail message, and if it is the last packet in the mail message.</span></span> <span data-ttu-id="fe1ce-213">`final_packet`NX_TRUE, tarafından işaret edilen paket, `recv_packet_ptr` posta öğesi iletisindeki son pakettir.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-213">If `final_packet` is NX_TRUE the packet pointed to by `recv_packet_ptr` is the final packet in the mail item message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fe1ce-214">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-214">Input Parameters</span></span>

- <span data-ttu-id="fe1ce-215">**client_ptr**: istemci örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-215">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="fe1ce-216">**recv_packet_ptr**: İleti verisi paketi alındı</span><span class="sxs-lookup"><span data-stu-id="fe1ce-216">**recv_packet_ptr**: Received packet of message data</span></span>
- <span data-ttu-id="fe1ce-217">**number_mail_item**: istemci maildrop 'daki posta sayısı</span><span class="sxs-lookup"><span data-stu-id="fe1ce-217">**number_mail_item**: Number of mail in Client maildrop</span></span>
- <span data-ttu-id="fe1ce-218">**maildrop_total_size**: tüm posta iletisinin boyutu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-218">**maildrop_total_size**: Pointer to size of all mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="fe1ce-219">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-219">Return Values</span></span>

- <span data-ttu-id="fe1ce-220">**NX_SUCCESS**: (0x00) posta öğesi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="fe1ce-220">**NX_SUCCESS**: (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="fe1ce-221">**NX_POP3_CLIENT_INVALID_STATE**: (0Xb7) istemci paket yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-221">**NX_POP3_CLIENT_INVALID_STATE**: (0xB7) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="fe1ce-222">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-222">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fe1ce-223">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fe1ce-223">Allowed From</span></span>

<span data-ttu-id="fe1ce-224">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="fe1ce-224">Application code</span></span>

### <a name="example"></a><span data-ttu-id="fe1ce-225">Örnek</span><span class="sxs-lookup"><span data-stu-id="fe1ce-225">Example</span></span>

```c
NX_PACKET     *recv_packet_ptr;
ULONG         bytes_retrieved;
UINT          final_packet;

/* Retrieve the size and number of items in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_message_get (&demo_client, &recv_packet_ptr,
                                                bytes_retrieved, final_packet);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_size_get"></a><span data-ttu-id="fe1ce-226">nx_pop3_client_mail_item_size_get</span><span class="sxs-lookup"><span data-stu-id="fe1ce-226">nx_pop3_client_mail_item_size_get</span></span>

<span data-ttu-id="fe1ce-227">Belirtilen posta öğesinin boyutunu al</span><span class="sxs-lookup"><span data-stu-id="fe1ce-227">Retrieve the size of the specified mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="fe1ce-228">Prototype</span><span class="sxs-lookup"><span data-stu-id="fe1ce-228">Prototype</span></span>

```c
UINT nx_pop3_client_mail_item_size_get(
                NX_POP3_CLIENT *client_ptr,
                UINT mail_item, ULONG *size)
```

### <a name="description"></a><span data-ttu-id="fe1ce-229">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe1ce-229">Description</span></span>

<span data-ttu-id="fe1ce-230">Bu hizmet, belirtilen posta öğesinin boyutunu almak için bir LISTE isteği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-230">This service makes a LIST request to obtain the size of the specified mail item.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="fe1ce-231">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-231">Input Parameters</span></span>

- <span data-ttu-id="fe1ce-232">**client_ptr**: istemci örneğine yönelik işaretçi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-232">**client_ptr**: Pointer to Client instance</span></span>
- <span data-ttu-id="fe1ce-233">**mail_item**: istemci maildrop 'a Dizin</span><span class="sxs-lookup"><span data-stu-id="fe1ce-233">**mail_item**: Index into Client maildrop</span></span>
- <span data-ttu-id="fe1ce-234">**Boyut**: posta iletisi boyutu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-234">**size**: Pointer to size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="fe1ce-235">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="fe1ce-235">Return Values</span></span>

- <span data-ttu-id="fe1ce-236">**NX_SUCCESS**: (0x00) posta öğesi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="fe1ce-236">**NX_SUCCESS**: (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="fe1ce-237">**NX_POP3_INVALID_MAIL_ITEM**: (0Xb2) geçersiz posta öğesi dizini</span><span class="sxs-lookup"><span data-stu-id="fe1ce-237">**NX_POP3_INVALID_MAIL_ITEM**: (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="fe1ce-238">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0Xb6) istemci paket yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="fe1ce-238">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**: (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="fe1ce-239">**NX_POP3_SERVER_ERROR_STATUS**: (0Xb4) sunucu, hata durumuyla yanıt verir</span><span class="sxs-lookup"><span data-stu-id="fe1ce-239">**NX_POP3_SERVER_ERROR_STATUS**: (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="fe1ce-240">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) geçersiz posta dizini girişi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-240">NX_POP3_CLIENT_INVALID_INDEX: (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="fe1ce-241">NX_PTR_ERROR: (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="fe1ce-241">NX_PTR_ERROR: (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="fe1ce-242">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="fe1ce-242">Allowed From</span></span>

<span data-ttu-id="fe1ce-243">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="fe1ce-243">Application code</span></span>

### <a name="example"></a><span data-ttu-id="fe1ce-244">Örnek</span><span class="sxs-lookup"><span data-stu-id="fe1ce-244">Example</span></span>

```c
ULONG     size;
UINT      mail_item;

/* Retrieve the size of the specified mail item in POP3 Client maildrop. */
status = nx_pop3_client_mail_item_size_get (&demo_client, mail_item, &size);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```
