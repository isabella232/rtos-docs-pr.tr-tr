---
title: Bölüm 3-POP3 Istemci hizmetlerinin açıklaması
description: Bu bölüm, tüm NetX Duo POP3 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1f7681c8f3fe161db8a37a82574ab7d5e9bf348e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825841"
---
# <a name="chapter-3---description-of-pop3-client-services"></a><span data-ttu-id="82f1a-103">Bölüm 3-POP3 Istemci hizmetlerinin açıklaması</span><span class="sxs-lookup"><span data-stu-id="82f1a-103">Chapter 3 - Description of POP3 Client Services</span></span>

<span data-ttu-id="82f1a-104">Bu bölüm, tüm NetX Duo POP3 Istemci hizmetlerinin (aşağıda listelenmiştir) alfabetik sırada bir açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="82f1a-104">This chapter contains a description of all NetX Duo POP3 Client services (listed below) in alphabetical order.</span></span>

> [!NOTE]
> <span data-ttu-id="82f1a-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **NX_DISABLE_ERROR_CHECKING** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="82f1a-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_pop3_client_create"></a><span data-ttu-id="82f1a-106">nx_pop3_client_create</span><span class="sxs-lookup"><span data-stu-id="82f1a-106">nx_pop3_client_create</span></span>

<span data-ttu-id="82f1a-107">IPv4 için bir POP3 Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="82f1a-107">Create a POP3 Client instance for IPv4</span></span>

### <a name="prototype"></a><span data-ttu-id="82f1a-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="82f1a-108">Prototype</span></span>

```C
UINT nx_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    ULONG server_ip_address, ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a><span data-ttu-id="82f1a-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82f1a-109">Description</span></span>

<span data-ttu-id="82f1a-110">Bu hizmet, POP3 Istemcisinin bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="82f1a-110">This service creates an instance of the POP3 Client.</span></span> <span data-ttu-id="82f1a-111">Yalnızca IPv4 POP3 sunucu adreslerini destekler.</span><span class="sxs-lookup"><span data-stu-id="82f1a-111">It supports only IPv4 POP3 server addresses.</span></span>

<span data-ttu-id="82f1a-112">Cihaz uygulamasının, paketleri iletmek için POP3 Istemcisi için bir IP örneği ve bir paket havuzu oluşturması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="82f1a-112">Note that the device application must first create an IP instance and a packet pool for the POP3 Client to transmit packets.</span></span> <span data-ttu-id="82f1a-113">Bu paket havuzu, yalnızca POP3 Istemci görevi veya IP örneği oluşturmada kullanılan paket havuzu tarafından kullanılmak üzere oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="82f1a-113">This packet pool created for use exclusively by the POP3 Client task or the same packet pool used in the IP instance creation.</span></span> <span data-ttu-id="82f1a-114">Paket havuzu, Ethernet sürücü paketi havuzuyla de paylaşılabilir, ancak bu, yükü, POP3 Istemcisinin sunucuya görece küçük ve büyük boyutlu paketler alması amaçlanan büyük paket havuzları kullanmanın dezavantajudur.</span><span class="sxs-lookup"><span data-stu-id="82f1a-114">The packet pool may also be shared with the Ethernet driver packet pool but this has the disadvantage of using large packet pools whose payload is intended for receiving potentially large packets payload for the POP3 Client to send relatively small POP3 message packets to the server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="82f1a-115">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-115">Input Parameters</span></span>

- <span data-ttu-id="82f1a-116">**client_ptr** Oluşturulacak Istemci işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-116">**client_ptr** Pointer to Client to create</span></span>
- <span data-ttu-id="82f1a-117">**APOP_authentication** APOP kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="82f1a-117">**APOP_authentication** Enable APOP authentication</span></span>
- <span data-ttu-id="82f1a-118">IP örneğine **Ip_ptr işaretçisi**</span><span class="sxs-lookup"><span data-stu-id="82f1a-118">**ip_ptr Pointer** to IP instance</span></span>
- <span data-ttu-id="82f1a-119">**packet_pool_ptr** Istemci paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-119">**packet_pool_ptr** Pointer to Client packet pool</span></span>
- <span data-ttu-id="82f1a-120">**server_ip_address** POP3 sunucusu IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-120">**server_ip_address** POP3 server IPv4 address</span></span>
- <span data-ttu-id="82f1a-121">**SERVER_PORT** POP3 sunucu bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="82f1a-121">**server_port** POP3 server port</span></span>
- <span data-ttu-id="82f1a-122">**client_name** Istemci adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-122">**client_name** Pointer to Client name</span></span>
- <span data-ttu-id="82f1a-123">**client_password** Istemci parolası işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-123">**client_password** Pointer to Client password</span></span>

### <a name="return-values"></a><span data-ttu-id="82f1a-124">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-124">Return Values</span></span>

- <span data-ttu-id="82f1a-125">**NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="82f1a-125">**NX_SUCCESS** (0x00) Client successfully created</span></span>
- <span data-ttu-id="82f1a-126">**durum** NetX Duo ve ThreadX hizmeti çağrılarının durum bitimi</span><span class="sxs-lookup"><span data-stu-id="82f1a-126">**status** Status completion of NetX Duo and ThreadX service calls</span></span>
- <span data-ttu-id="82f1a-127">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-127">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="82f1a-128">NX_POP3_PARAM_ERROR (0xB1) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="82f1a-128">NX_POP3_PARAM_ERROR (0xB1) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="82f1a-129">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="82f1a-129">Allowed From</span></span>

<span data-ttu-id="82f1a-130">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="82f1a-130">Application code</span></span>

### <a name="example"></a><span data-ttu-id="82f1a-131">Örnek</span><span class="sxs-lookup"><span data-stu-id="82f1a-131">Example</span></span>

```C
/* Create the POP3 Client. Note that the Client uses its password for its APOP shared
    secret. */

/* Set up user defined callback services. */
/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD "pass"
#define POP3_SERVER_ADDRESS IP_ADDRESS(192,2,2,92)
#define POP3_SERVER_PORT 110

/* Create a NetX POP3 Client instance. */
status = nx_pop3_client_create(&demo_client,
    NX_FALSE /* disable APOP authentication */,
    &client_ip, &client_packet_pool,
    POP3_SERVER_ADDRESS, POP3_SERVER_PORT,
    LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nxd_pop3_client_create"></a><span data-ttu-id="82f1a-132">nxd_pop3_client_create</span><span class="sxs-lookup"><span data-stu-id="82f1a-132">nxd_pop3_client_create</span></span>

<span data-ttu-id="82f1a-133">IPv4 veya IPv6 için bir POP3 Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="82f1a-133">Create a POP3 Client instance for IPv4 or IPv6</span></span>

### <a name="prototype"></a><span data-ttu-id="82f1a-134">Prototype</span><span class="sxs-lookup"><span data-stu-id="82f1a-134">Prototype</span></span>

```C
UINT nxd_pop3_client_create(NX_POP3_CLIENT *client_ptr,
    UINT APOP_authentication, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool_ptr,
    NXD_ADDRESS *server_ip_address,
    ULONG server_port,
    CHAR *client_name, CHAR *client_password);
```

### <a name="description"></a><span data-ttu-id="82f1a-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82f1a-135">Description</span></span>

<span data-ttu-id="82f1a-136">Bu hizmet, POP3 Istemcisinin bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="82f1a-136">This service creates an instance of the POP3 Client.</span></span> <span data-ttu-id="82f1a-137">Hem IPv4 hem de IPv6 POP3 sunucu adreslerini destekler.</span><span class="sxs-lookup"><span data-stu-id="82f1a-137">It supports both IPv4 and IPv6 POP3 server addresses.</span></span> <span data-ttu-id="82f1a-138">POP3 Istemcisi oluşturma işlemi hakkında daha fazla bilgi için daha önce açıklanan *nx_pop3_client_create* hizmetine bakın.</span><span class="sxs-lookup"><span data-stu-id="82f1a-138">See the previously described *nx_pop3_client_create* service for more details on POP3 Client create process.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="82f1a-139">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-139">Input Parameters</span></span>

- <span data-ttu-id="82f1a-140">**client_ptr** Oluşturulacak Istemci işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-140">**client_ptr** Pointer to Client to create</span></span>
- <span data-ttu-id="82f1a-141">**APOP_authentication** APOP kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="82f1a-141">**APOP_authentication** Enable APOP authentication</span></span>
- <span data-ttu-id="82f1a-142">**ip_ptr** IP örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-142">**ip_ptr** Pointer to IP instance</span></span>
- <span data-ttu-id="82f1a-143">**packet_pool_ptr** Istemci paket havuzu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-143">**packet_pool_ptr** Pointer to Client packet pool</span></span>
- <span data-ttu-id="82f1a-144">**server_ip_address** POP3 sunucusu IPv6 veya IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-144">**server_ip_address** POP3 server IPv6 or IPv4 address</span></span>
- <span data-ttu-id="82f1a-145">**SERVER_PORT** POP3 sunucu bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="82f1a-145">**server_port** POP3 server port</span></span>
- <span data-ttu-id="82f1a-146">**client_name**  Istemci adı işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-146">**client_name**  Pointer to Client name</span></span>
- <span data-ttu-id="82f1a-147">**client_password** Istemci parolası işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-147">**client_password** Pointer to Client password</span></span>

### <a name="return-values"></a><span data-ttu-id="82f1a-148">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-148">Return Values</span></span>

- <span data-ttu-id="82f1a-149">**NX_SUCCESS** (0x00) istemci başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="82f1a-149">**NX_SUCCESS** (0x00) Client successfully created</span></span>
- <span data-ttu-id="82f1a-150">**durum** NetX Duo ve ThreadX hizmeti çağrılarının durum bitimi</span><span class="sxs-lookup"><span data-stu-id="82f1a-150">**status** Status completion of NetX Duo and ThreadX service calls</span></span>
- <span data-ttu-id="82f1a-151">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-151">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="82f1a-152">NX_POP3_PARAM_ERROR (0xB1) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="82f1a-152">NX_POP3_PARAM_ERROR (0xB1) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="82f1a-153">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="82f1a-153">Allowed From</span></span>

<span data-ttu-id="82f1a-154">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="82f1a-154">Application code</span></span>

### <a name="example"></a><span data-ttu-id="82f1a-155">Örnek</span><span class="sxs-lookup"><span data-stu-id="82f1a-155">Example</span></span>

```C
/* Create the POP3 Client. */

/* Create username and password for our POP3 Client mail drop. */
#define LOCALHOST "recipient@expresslogic.com"
#define LOCALHOST_PASSWORD "pass"
#define POP3_SERVER_PORT 110

/* Create a NetX POP3 Client instance. Also note the details of IPv6 address validation
    and enabling IPv6 and ICMPv6 services on the IP task are not shown here. See the
    NetX Duo User Guide for more details on this process.
*/
NXD_ADDRESS server_ip_address;

/* Set client IP interface address. */
server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
server_ip_address.nxd_ip_address.v6[1] = 0xf101;
server_ip_address.nxd_ip_address.v6[2] = 0;
server_ip_address.nxd_ip_address.v6[3] = 0x101;
status = nxd_pop3_client_create(&demo_client,
    NX_FALSE /* disable APOP authentication */,
    &client_ip, &client_packet_pool,
    &server_ip_address, POP3_SERVER_PORT,
    LOCALHOST, LOCALHOST_PASSWORD);

/* If the Client was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_delete"></a><span data-ttu-id="82f1a-156">nx_pop3_client_delete</span><span class="sxs-lookup"><span data-stu-id="82f1a-156">nx_pop3_client_delete</span></span>

<span data-ttu-id="82f1a-157">POP3 Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="82f1a-157">Delete a POP3 Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="82f1a-158">Prototype</span><span class="sxs-lookup"><span data-stu-id="82f1a-158">Prototype</span></span>

```C
UINT nx_pop3_client_delete(NX_POP3_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="82f1a-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82f1a-159">Description</span></span>

<span data-ttu-id="82f1a-160">Bu hizmet önceden oluşturulmuş bir POP3 Istemcisini siler.</span><span class="sxs-lookup"><span data-stu-id="82f1a-160">This service deletes a previously created POP3 Client.</span></span> <span data-ttu-id="82f1a-161">Bu hizmet POP3 Istemci paket havuzunu silmez.</span><span class="sxs-lookup"><span data-stu-id="82f1a-161">Not that this service does not delete the POP3 Client packet pool.</span></span> <span data-ttu-id="82f1a-162">Cihaz uygulamasının artık paket havuzu için kullanımı gerekmiyorsa, bu kaynağı ayrı olarak silmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="82f1a-162">The device application must delete this resource separately if it no longer has use for the packet pool.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="82f1a-163">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-163">Input Parameters</span></span>

- <span data-ttu-id="82f1a-164">**client_ptr** Silinecek Istemci işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-164">**client_ptr** Pointer to Client to delete</span></span>

### <a name="return-values"></a><span data-ttu-id="82f1a-165">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-165">Return Values</span></span>

- <span data-ttu-id="82f1a-166">**NX_SUCCESS** (0x00) istemci başarıyla silindi</span><span class="sxs-lookup"><span data-stu-id="82f1a-166">**NX_SUCCESS** (0x00) Client successfully deleted</span></span>
- <span data-ttu-id="82f1a-167">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-167">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="82f1a-168">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="82f1a-168">Allowed From</span></span>

<span data-ttu-id="82f1a-169">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="82f1a-169">Application code</span></span>

### <a name="example"></a><span data-ttu-id="82f1a-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="82f1a-170">Example</span></span>

```C
/* Delete the POP3 Client. */
status = nx_pop3_client_delete (&demo_client);

/* If the Client was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_delete"></a><span data-ttu-id="82f1a-171">nx_pop3_client_mail_item_delete</span><span class="sxs-lookup"><span data-stu-id="82f1a-171">nx_pop3_client_mail_item_delete</span></span>

<span data-ttu-id="82f1a-172">Istemci maildrop 'tan belirtilen bir posta öğesini silme</span><span class="sxs-lookup"><span data-stu-id="82f1a-172">Delete a specified mail item from the Client maildrop</span></span>

### <a name="prototype"></a><span data-ttu-id="82f1a-173">Prototype</span><span class="sxs-lookup"><span data-stu-id="82f1a-173">Prototype</span></span>

```C
UINT nx_pop3_client_mail_items_delete(NX_POP3_CLIENT *client_ptr,
    UINT mail_index);
```

### <a name="description"></a><span data-ttu-id="82f1a-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82f1a-174">Description</span></span>

<span data-ttu-id="82f1a-175">Bu hizmet, belirtilen posta öğesini Istemci maildrop 'dan siler.</span><span class="sxs-lookup"><span data-stu-id="82f1a-175">This service deletes the specified mail item from the Client maildrop.</span></span> <span data-ttu-id="82f1a-176">Posta öğesi indirildikten sonra, bazı POP3 sunucuları, Istemci tarafından istendikten sonra posta öğelerini otomatik olarak silebilir.</span><span class="sxs-lookup"><span data-stu-id="82f1a-176">It is intended for after downloading the mail item, although some POP3 servers may automatically delete mail items after being requested by the Client.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="82f1a-177">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-177">Input Parameters</span></span>

- <span data-ttu-id="82f1a-178">**client_ptr** Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-178">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="82f1a-179">**mail_index** Istemci maildrop 'a Dizin</span><span class="sxs-lookup"><span data-stu-id="82f1a-179">**mail_index** Index into Client maildrop</span></span>

### <a name="return-values"></a><span data-ttu-id="82f1a-180">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-180">Return Values</span></span>

- <span data-ttu-id="82f1a-181">**NX_SUCCESS** (0x00) silme isteği başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="82f1a-181">**NX_SUCCESS** (0x00) Delete request successful</span></span>
- <span data-ttu-id="82f1a-182">**NX_POP3_INVALID_MAIL_ITEM**(0xB2) geçersiz posta öğesi dizini</span><span class="sxs-lookup"><span data-stu-id="82f1a-182">**NX_POP3_INVALID_MAIL_ITEM**(0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="82f1a-183">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**(0xb6) istemci PAKETI yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="82f1a-183">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD**(0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="82f1a-184">**NX_POP3_SERVER_ERROR_STATUS**(0xb4) sunucu, hata durumuyla yanıt verir</span><span class="sxs-lookup"><span data-stu-id="82f1a-184">**NX_POP3_SERVER_ERROR_STATUS**(0xB4) Server replies with error status</span></span>
- <span data-ttu-id="82f1a-185">NX_POP3_CLIENT_INVALID_INDEX (0xB8) geçersiz posta dizini girişi</span><span class="sxs-lookup"><span data-stu-id="82f1a-185">NX_POP3_CLIENT_INVALID_INDEX(0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="82f1a-186">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-186">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="82f1a-187">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="82f1a-187">Allowed From</span></span>

<span data-ttu-id="82f1a-188">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="82f1a-188">Application code</span></span>

### <a name="example"></a><span data-ttu-id="82f1a-189">Örnek</span><span class="sxs-lookup"><span data-stu-id="82f1a-189">Example</span></span>

```C
ULONG item_index;

/* Delete the POP3 Client mail item. */
status = nx_pop3_client_mail_item_delete(&demo_client, item_index);

/* If the server accepts the DELE request (and deletes the mail item), status =
    NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_get"></a><span data-ttu-id="82f1a-190">nx_pop3_client_mail_item_get</span><span class="sxs-lookup"><span data-stu-id="82f1a-190">nx_pop3_client_mail_item_get</span></span>

<span data-ttu-id="82f1a-191">Belirtilen posta öğesini alma</span><span class="sxs-lookup"><span data-stu-id="82f1a-191">Retrieve a specified mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="82f1a-192">Prototype</span><span class="sxs-lookup"><span data-stu-id="82f1a-192">Prototype</span></span>

```C
UINT nx_pop3_client_mail_item_get(NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *item_size);
```

### <a name="description"></a><span data-ttu-id="82f1a-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82f1a-193">Description</span></span>

<span data-ttu-id="82f1a-194">Bu hizmet, Dizin mail_item tarafından belirtilen Istemci maildrop öğesinden bir posta öğesi almaya yönelik bir RETR isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="82f1a-194">This service makes a RETR request to retrieve a mail item from the Client maildrop specified by the index mail_item.</span></span> <span data-ttu-id="82f1a-195">Bir RETR isteği yaptıktan ve sunucudan olumlu bir yanıt aldıktan sonra Istemci, *nx_pop3_client_mail_item_message_get* hizmetini kullanarak posta iletisini indirmeye başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="82f1a-195">After making a RETR request, and receiving a positive response from the Server, the Client can start downloading the mail message using the *nx_pop3_client_mail_item_message_get* service.</span></span> <span data-ttu-id="82f1a-196">Hizmetin, sunucu yanıtlarından ayıklanan istenen posta öğesinin boyutunu da sağladığı unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="82f1a-196">Note that the service also supplies the size of the requested mail item extracted from the Server reply.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="82f1a-197">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-197">Input Parameters</span></span>

- <span data-ttu-id="82f1a-198">**client_ptr** Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-198">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="82f1a-199">**mail_item** Istemci maildrop 'a Dizin</span><span class="sxs-lookup"><span data-stu-id="82f1a-199">**mail_item** Index into Client maildrop</span></span>
- <span data-ttu-id="82f1a-200">**item_size** Posta iletisi boyutu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-200">**item_size** Pointer to size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="82f1a-201">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-201">Return Values</span></span>

- <span data-ttu-id="82f1a-202">**NX_SUCCESS** (0x00) posta öğesi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="82f1a-202">**NX_SUCCESS** (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="82f1a-203">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) geçersiz posta öğesi dizini</span><span class="sxs-lookup"><span data-stu-id="82f1a-203">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="82f1a-204">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xb6) istemci PAKETI yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="82f1a-204">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="82f1a-205">**NX_POP3_SERVER_ERROR_STATUS** (0xb4) sunucu, hata durumuyla yanıt verir</span><span class="sxs-lookup"><span data-stu-id="82f1a-205">**NX_POP3_SERVER_ERROR_STATUS** (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="82f1a-206">NX_POP3_CLIENT_INVALID_INDEX (0xB8) geçersiz posta dizini girişi</span><span class="sxs-lookup"><span data-stu-id="82f1a-206">NX_POP3_CLIENT_INVALID_INDEX (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="82f1a-207">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-207">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="82f1a-208">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="82f1a-208">Allowed From</span></span>

<span data-ttu-id="82f1a-209">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="82f1a-209">Application code</span></span>

### <a name="example"></a><span data-ttu-id="82f1a-210">Örnek</span><span class="sxs-lookup"><span data-stu-id="82f1a-210">Example</span></span>

```C
ULONG item_size;

/* Retrieve the POP3 Client mail item. */
status = nx_pop3_client_mail_item_get (&demo_client, 1, &item_size);

/* If the mail item was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_items_get"></a><span data-ttu-id="82f1a-211">nx_pop3_client_mail_items_get</span><span class="sxs-lookup"><span data-stu-id="82f1a-211">nx_pop3_client_mail_items_get</span></span>

<span data-ttu-id="82f1a-212">Maildrop 'daki posta öğelerinin sayısını alma</span><span class="sxs-lookup"><span data-stu-id="82f1a-212">Retrieve the number of mail items in maildrop</span></span>

### <a name="prototype"></a><span data-ttu-id="82f1a-213">Prototype</span><span class="sxs-lookup"><span data-stu-id="82f1a-213">Prototype</span></span>

```C
UINT nx_pop3_client_mail_items_get(NX_POP3_CLIENT *client_ptr,
    UINT *number_mail_items,
    ULONG *maildrop_total_size);
```

### <a name="description"></a><span data-ttu-id="82f1a-214">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82f1a-214">Description</span></span>

<span data-ttu-id="82f1a-215">Bu hizmet, posta öğelerinin sayısını ve Istemci maildrop 'tan gelen posta iletisi verilerinin toplam boyutunu almak için bir STAT isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="82f1a-215">This service makes a STAT request to retrieve the number of mail items and total size of mail message data from the Client maildrop.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="82f1a-216">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-216">Input Parameters</span></span>

- <span data-ttu-id="82f1a-217">**client_ptr** Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-217">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="82f1a-218">**number_mail_item** Istemci maildrop 'daki posta sayısı</span><span class="sxs-lookup"><span data-stu-id="82f1a-218">**number_mail_item** Number of mail in Client maildrop</span></span>
- <span data-ttu-id="82f1a-219">**maildrop_total_size** Tüm posta iletisinin boyutu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-219">**maildrop_total_size** Pointer to size of all mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="82f1a-220">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-220">Return Values</span></span>

- <span data-ttu-id="82f1a-221">**NX_SUCCESS** (0x00) posta öğesi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="82f1a-221">**NX_SUCCESS** (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="82f1a-222">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) geçersiz posta öğesi dizini</span><span class="sxs-lookup"><span data-stu-id="82f1a-222">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="82f1a-223">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xb6) istemci PAKETI yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="82f1a-223">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="82f1a-224">**NX_POP3_SERVER_ERROR_STATUS** (0xb4) sunucu, hata durumuyla yanıt verir</span><span class="sxs-lookup"><span data-stu-id="82f1a-224">**NX_POP3_SERVER_ERROR_STATUS** (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="82f1a-225">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-225">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="82f1a-226">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="82f1a-226">Allowed From</span></span>

<span data-ttu-id="82f1a-227">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="82f1a-227">Application code</span></span>

### <a name="example"></a><span data-ttu-id="82f1a-228">Örnek</span><span class="sxs-lookup"><span data-stu-id="82f1a-228">Example</span></span>

```C
UINT number_mail_items;

ULONG maildrop_total_size;

/* Retrieve the size and number of items in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_get (&demo_client, 1, &number_mail_items,
    &maildrop_total_size);

/* If the maildrop data was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_message_get"></a><span data-ttu-id="82f1a-229">nx_pop3_client_mail_item_message_get</span><span class="sxs-lookup"><span data-stu-id="82f1a-229">nx_pop3_client_mail_item_message_get</span></span>

<span data-ttu-id="82f1a-230">Belirtilen posta öğesi iletisini Al</span><span class="sxs-lookup"><span data-stu-id="82f1a-230">Retrieve the specified mail item message</span></span>

### <a name="prototype"></a><span data-ttu-id="82f1a-231">Prototype</span><span class="sxs-lookup"><span data-stu-id="82f1a-231">Prototype</span></span>

```C
UINT nx_pop3_client_mail_item_message_get(
    NX_POP3_CLIENT *client_ptr,
    NX_PACKET **recv_packet_ptr,
    ULONG *bytes_retrieved,
    UINT *final_packet);
```

### <a name="description"></a><span data-ttu-id="82f1a-232">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82f1a-232">Description</span></span>

<span data-ttu-id="82f1a-233">Bu hizmet posta öğesi iletisini, posta iletisinin boyutunu ve posta iletisindeki son paket ise alır.</span><span class="sxs-lookup"><span data-stu-id="82f1a-233">This service retrieves the mail item message, size of the mail message, and if it is the last packet in the mail message.</span></span> <span data-ttu-id="82f1a-234">Final_packet NX_TRUE recv_packet_ptr tarafından işaret edilen paket, posta öğesi iletisindeki son pakettir.</span><span class="sxs-lookup"><span data-stu-id="82f1a-234">If final_packet is NX_TRUE the packet pointed to by recv_packet_ptr is the final packet in the mail item message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="82f1a-235">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-235">Input Parameters</span></span>

- <span data-ttu-id="82f1a-236">**client_ptr** Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-236">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="82f1a-237">**recv_packet_ptr** İleti verisi paketi alındı</span><span class="sxs-lookup"><span data-stu-id="82f1a-237">**recv_packet_ptr** Received packet of message data</span></span>
- <span data-ttu-id="82f1a-238">**number_mail_item** Istemci maildrop 'daki posta sayısı</span><span class="sxs-lookup"><span data-stu-id="82f1a-238">**number_mail_item** Number of mail in Client maildrop</span></span>
- <span data-ttu-id="82f1a-239">**maildrop_total_size** Tüm posta iletisinin boyutu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-239">**maildrop_total_size** Pointer to size of all mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="82f1a-240">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-240">Return Values</span></span>

- <span data-ttu-id="82f1a-241">**NX_SUCCESS** (0x00) posta öğesi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="82f1a-241">**NX_SUCCESS** (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="82f1a-242">**NX_POP3_CLIENT_INVALID_STATE** (0xb7) istemci PAKETI yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="82f1a-242">**NX_POP3_CLIENT_INVALID_STATE** (0xB7) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="82f1a-243">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-243">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="82f1a-244">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="82f1a-244">Allowed From</span></span>

<span data-ttu-id="82f1a-245">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="82f1a-245">Application code</span></span>

### <a name="example"></a><span data-ttu-id="82f1a-246">Örnek</span><span class="sxs-lookup"><span data-stu-id="82f1a-246">Example</span></span>

```C
NX_PACKET *recv_packet_ptr;

ULONG bytes_retrieved;

UINT final_packet;

/* Retrieve the size and number of items in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_message_get (&demo_client, &recv_packet_ptr,
    bytes_retrieved, final_packet);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```

## <a name="nx_pop3_client_mail_item_size_get"></a><span data-ttu-id="82f1a-247">nx_pop3_client_mail_item_size_get</span><span class="sxs-lookup"><span data-stu-id="82f1a-247">nx_pop3_client_mail_item_size_get</span></span>

<span data-ttu-id="82f1a-248">Belirtilen posta öğesinin boyutunu al</span><span class="sxs-lookup"><span data-stu-id="82f1a-248">Retrieve the size of the specified mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="82f1a-249">Prototype</span><span class="sxs-lookup"><span data-stu-id="82f1a-249">Prototype</span></span>

```C
UINT nx_pop3_client_mail_item_size_get(
    NX_POP3_CLIENT *client_ptr,
    UINT mail_item, ULONG *size);
```

### <a name="description"></a><span data-ttu-id="82f1a-250">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82f1a-250">Description</span></span>

<span data-ttu-id="82f1a-251">Bu hizmet, belirtilen posta öğesinin boyutunu almak için bir LISTE isteği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="82f1a-251">This service makes a LIST request to obtain the size of the specified mail item.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="82f1a-252">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-252">Input Parameters</span></span>

- <span data-ttu-id="82f1a-253">**client_ptr** Istemci örneği işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-253">**client_ptr** Pointer to Client instance</span></span>
- <span data-ttu-id="82f1a-254">**mail_item** Istemci maildrop 'a Dizin</span><span class="sxs-lookup"><span data-stu-id="82f1a-254">**mail_item** Index into Client maildrop</span></span>
- <span data-ttu-id="82f1a-255">**Boyut** Posta iletisi boyutu işaretçisi</span><span class="sxs-lookup"><span data-stu-id="82f1a-255">**size** Pointer to size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="82f1a-256">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="82f1a-256">Return Values</span></span>

- <span data-ttu-id="82f1a-257">**NX_SUCCESS** (0x00) posta öğesi başarıyla alındı</span><span class="sxs-lookup"><span data-stu-id="82f1a-257">**NX_SUCCESS** (0x00) Mail item successfully retrieved</span></span>
- <span data-ttu-id="82f1a-258">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) geçersiz posta öğesi dizini</span><span class="sxs-lookup"><span data-stu-id="82f1a-258">**NX_POP3_INVALID_MAIL_ITEM** (0xB2) Invalid mail item index</span></span>
- <span data-ttu-id="82f1a-259">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xb6) istemci PAKETI yükü POP3 isteği için çok küçük.</span><span class="sxs-lookup"><span data-stu-id="82f1a-259">**NX_POP3_INSUFFICIENT_PACKET_PAYLOAD** (0xB6) Client packet payload too small for POP3 request.</span></span>
- <span data-ttu-id="82f1a-260">**NX_POP3_SERVER_ERROR_STATUS** (0xb4) sunucu, hata durumuyla yanıt verir</span><span class="sxs-lookup"><span data-stu-id="82f1a-260">**NX_POP3_SERVER_ERROR_STATUS** (0xB4) Server replies with error status</span></span>
- <span data-ttu-id="82f1a-261">NX_POP3_CLIENT_INVALID_INDEX (0xB8) geçersiz posta dizini girişi</span><span class="sxs-lookup"><span data-stu-id="82f1a-261">NX_POP3_CLIENT_INVALID_INDEX (0xB8) Invalid mail index input</span></span>
- <span data-ttu-id="82f1a-262">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="82f1a-262">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="82f1a-263">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="82f1a-263">Allowed From</span></span>

<span data-ttu-id="82f1a-264">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="82f1a-264">Application code</span></span>

### <a name="example"></a><span data-ttu-id="82f1a-265">Örnek</span><span class="sxs-lookup"><span data-stu-id="82f1a-265">Example</span></span>

```C
ULONG size;

UINT mail_item;

/* Retrieve the size of the specified mail item in POP3 Client maildrop. */

status = nx_pop3_client_mail_item_size_get (&demo_client, mail_item, &size);

/* If the maildrop message packet was successfully obtained, status = NX_SUCCESS. */
```
