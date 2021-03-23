---
title: Bölüm 3-SMTP Istemci hizmetlerinin Istemci açıklaması
description: Bu bölüm, tipik bir SMTP Istemci uygulamasında kullanım sırasına göre tüm NetX Duo SMTP Istemci hizmetlerinin (aşağıda listelenmiştir) açıklamasını içerir.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f590ba5a4c020b4a0aec6628a89c0e5f0f8579d9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825787"
---
# <a name="chapter-3---client-description-of-smtp-client-services"></a><span data-ttu-id="cada8-103">Bölüm 3-SMTP Istemci hizmetlerinin Istemci açıklaması</span><span class="sxs-lookup"><span data-stu-id="cada8-103">Chapter 3 - Client description of SMTP Client services</span></span>

<span data-ttu-id="cada8-104">Bu bölüm, tipik bir SMTP Istemci uygulamasında kullanım sırasına göre tüm NetX Duo SMTP Istemci hizmetlerinin (aşağıda listelenmiştir) açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="cada8-104">This chapter contains a description of all NetX Duo SMTP Client services (listed below) in order of usage in a typical SMTP Client application.</span></span>

> [!NOTE]
> <span data-ttu-id="cada8-105">Aşağıdaki API açıklamalarındaki "dönüş değerleri" bölümünde, **kalın** olmayan değerler, API hata denetimini devre dışı bırakmak için kullanılan **_NX_DISABLE_ERROR_CHECKING_** tanımlanmasından etkilenmez, ancak kalın olmayan değerler tamamen devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="cada8-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **_NX_DISABLE_ERROR_CHECKING_** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nxd_smtp_client_create"></a><span data-ttu-id="cada8-106">nxd_smtp_client_create</span><span class="sxs-lookup"><span data-stu-id="cada8-106">nxd_smtp_client_create</span></span>

<span data-ttu-id="cada8-107">SMTP Istemci örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="cada8-107">Create an SMTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="cada8-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="cada8-108">Prototype</span></span>

```C
UINT nxd_smtp_client_create(NX_SMTP_CLIENT *client_ptr,
    NX_IP *ip_ptr, NX_PACKET_POOL
    *client_packet_pool_ptr,
    CHAR *username, CHAR *password,
    CHAR *from_address,
    CHAR *client_domain,
    UINT authentication_type, NXD_ADDRESS *server_address,
    UINT port);
```

### <a name="description"></a><span data-ttu-id="cada8-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cada8-109">Description</span></span>

<span data-ttu-id="cada8-110">Bu hizmet, belirtilen IP örneğinde bir SMTP Istemci örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cada8-110">This service creates an SMTP Client instance on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="cada8-111">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="cada8-111">Input Parameters</span></span>

- <span data-ttu-id="cada8-112">**client_ptr** SMTP Istemci denetim bloğu işaretçisi;</span><span class="sxs-lookup"><span data-stu-id="cada8-112">**client_ptr** Pointer to SMTP Client control block;</span></span>
- <span data-ttu-id="cada8-113">**ip_ptr** IP örneği işaretçisi;</span><span class="sxs-lookup"><span data-stu-id="cada8-113">**ip_ptr** Pointer to IP instance;</span></span>
- <span data-ttu-id="cada8-114">**packet_pool_ptr** Istemci paket havuzu işaretçisi;</span><span class="sxs-lookup"><span data-stu-id="cada8-114">**packet_pool_ptr** Pointer to Client packet pool;</span></span>
- <span data-ttu-id="cada8-115">**Kullanıcı adı** Kimlik doğrulaması için NULL ile sonlandırılmış \* \* Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="cada8-115">**username** NULL-terminated\*\* Username for authentication</span></span>
- <span data-ttu-id="cada8-116">**parola** Kimlik doğrulaması için NULL ile sonlandırılmış parola</span><span class="sxs-lookup"><span data-stu-id="cada8-116">**password** NULL-terminated password for authentication</span></span>
- <span data-ttu-id="cada8-117">**from_address** NULL ile sonlandırılmış gönderenin adresi</span><span class="sxs-lookup"><span data-stu-id="cada8-117">**from_address** NULL-terminated sender’s address</span></span>
- <span data-ttu-id="cada8-118">**client_domain** NULL ile sonlandırılmış etki alanı adı</span><span class="sxs-lookup"><span data-stu-id="cada8-118">**client_domain** NULL-terminated domain name</span></span>
- <span data-ttu-id="cada8-119">**authentication_type** İstemci kimlik doğrulaması türü.</span><span class="sxs-lookup"><span data-stu-id="cada8-119">**authentication_type** Client authentication type.</span></span> <span data-ttu-id="cada8-120">Desteklenen türler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cada8-120">Supported types are:</span></span>
  - <span data-ttu-id="cada8-121">NX_SMTP_CLIENT_AUTH_LOGIN</span><span class="sxs-lookup"><span data-stu-id="cada8-121">NX_SMTP_CLIENT_AUTH_LOGIN</span></span>
  - <span data-ttu-id="cada8-122">NX_SMTP_CLIENT_AUTH_PLAIN</span><span class="sxs-lookup"><span data-stu-id="cada8-122">NX_SMTP_CLIENT_AUTH_PLAIN</span></span>
  - <span data-ttu-id="cada8-123">NX_SMTP_CLIENT_AUTH_NONE</span><span class="sxs-lookup"><span data-stu-id="cada8-123">NX_SMTP_CLIENT_AUTH_NONE</span></span>
- <span data-ttu-id="cada8-124">**server_address** SMTP sunucusu IP adresi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="cada8-124">**server_address** Pointer to SMTP Server IP address</span></span>
- <span data-ttu-id="cada8-125">**SERVER_PORT** SMTP sunucusu TCP bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="cada8-125">**server_port** SMTP Server TCP port</span></span>

### <a name="return-values"></a><span data-ttu-id="cada8-126">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="cada8-126">Return Values</span></span>

- <span data-ttu-id="cada8-127">**NX_SUCCESS** (0x00) SMTP istemcisi başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cada8-127">**NX_SUCCESS** (0x00) SMTP Client successfully created.</span></span> <span data-ttu-id="cada8-128">TCP yuvası oluşturma durumu</span><span class="sxs-lookup"><span data-stu-id="cada8-128">TCP socket creation status</span></span>
- <span data-ttu-id="cada8-129">NX_SMTP_INVALID_PARAM (0xA5) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="cada8-129">NX_SMTP_INVALID_PARAM (0xA5) Invalid non pointer input</span></span>
- <span data-ttu-id="cada8-130">NX_IP_ADDRESS_ERROR (0x21) geçersiz IP adresi türü</span><span class="sxs-lookup"><span data-stu-id="cada8-130">NX_IP_ADDRESS_ERROR (0x21) Invalid IP address type</span></span>
- <span data-ttu-id="cada8-131">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="cada8-131">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cada8-132">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="cada8-132">Allowed From</span></span>

<span data-ttu-id="cada8-133">Uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="cada8-133">Application Code</span></span>

### <a name="example"></a><span data-ttu-id="cada8-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="cada8-134">Example</span></span>

```C
/* Create the SMTP Client instance. */
NX_PACKET_POOL client_packet_pool;
NX_IP client_ip;
NX_SMTP_CLIENT demo_client;

#define USERNAME “myusername”
#define PASSWORD “mypassword”
#define FROM_ADDRESS “<myname@mycompany.com>”
#define LOCAL_DOMAIN “mycompany.com”
#define SERVER_PORT 25

/* Define client authentication type as LOGIN. 
    If not specified or unknown the SMTP Client will set it to PLAIN. */
#define CLIENT_AUTHENTICATION_TYPE NX_SMTP_CLIENT_AUTH_LOGIN

NXD_ADDRESS server_ip_address;

#ifdef USE_IPV6
    /* Set up the Server IPv6 address. */
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
    server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    server_ip_address.nxd_ip_address.v6[1] = 0xf101;
    server_ip_address.nxd_ip_address.v6[2] = 0;
    server_ip_address.nxd_ip_address.v6[3] = 0x106;
#else
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip_address.nxd_ip_address.v4 = SERVER_IP_ADDRESS;
#endif

status = nxd_smtp_client_create(&demo_client, &client_ip, &client_packet_pool,
    USERNAME, PASSWORD, FROM_ADDRESS,
    LOCAL_DOMAIN, CLIENT_AUTHENTICATION_TYPE,
    &server_ip_address, SERVER_PORT);

/* If an SMTP Client instance was successfully created, status = NX_SUCCESS. */
```

## <a name="nx_smtp_client_delete"></a><span data-ttu-id="cada8-135">nx_smtp_client_delete</span><span class="sxs-lookup"><span data-stu-id="cada8-135">nx_smtp_client_delete</span></span>

<span data-ttu-id="cada8-136">SMTP Istemci örneğini silme</span><span class="sxs-lookup"><span data-stu-id="cada8-136">Delete an SMTP Client Instance</span></span>

### <a name="prototype"></a><span data-ttu-id="cada8-137">Prototype</span><span class="sxs-lookup"><span data-stu-id="cada8-137">Prototype</span></span>

```C
UINT nx_smtp_client_delete(NX_SMTP_CLIENT *client_ptr);
```

### <a name="description"></a><span data-ttu-id="cada8-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cada8-138">Description</span></span>

<span data-ttu-id="cada8-139">Bu hizmet, önceden oluşturulmuş bir SMTP Istemci örneğini siler.</span><span class="sxs-lookup"><span data-stu-id="cada8-139">This service deletes a previously created SMTP Client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="cada8-140">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="cada8-140">Input Parameters</span></span>

- <span data-ttu-id="cada8-141">**client_ptr** SMTP Istemci örneği işaretçisi.</span><span class="sxs-lookup"><span data-stu-id="cada8-141">**client_ptr** Pointer to SMTP Client instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cada8-142">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="cada8-142">Return Values</span></span>

- <span data-ttu-id="cada8-143">**NX_SUCCESS** (0x00) istemci başarıyla silindi</span><span class="sxs-lookup"><span data-stu-id="cada8-143">**NX_SUCCESS** (0x00) Client successfully deleted</span></span>
- <span data-ttu-id="cada8-144">NX_PTR_ERROR (0x07) geçersiz giriş işaretçisi parametresi</span><span class="sxs-lookup"><span data-stu-id="cada8-144">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cada8-145">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="cada8-145">Allowed From</span></span>

<span data-ttu-id="cada8-146">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="cada8-146">Threads</span></span>

### <a name="example"></a><span data-ttu-id="cada8-147">Örnek</span><span class="sxs-lookup"><span data-stu-id="cada8-147">Example</span></span>

```C
/* Delete the SMTP Client instance “my_client.” */

NX_SMTP_CLIENT demo_client;

status = nx_smtp_client_delete(&demo_client);

/* If an SMTP Client instance was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_smtp_mail_send"></a><span data-ttu-id="cada8-148">nx_smtp_mail_send</span><span class="sxs-lookup"><span data-stu-id="cada8-148">nx_smtp_mail_send</span></span>

<span data-ttu-id="cada8-149">SMTP posta öğesi oluşturma ve gönderme</span><span class="sxs-lookup"><span data-stu-id="cada8-149">Create and send an SMTP mail item</span></span>

### <a name="prototype"></a><span data-ttu-id="cada8-150">Prototype</span><span class="sxs-lookup"><span data-stu-id="cada8-150">Prototype</span></span>

```C
UINT nx_smtp_mail_send(NX_SMTP_CLIENT *client_ptr,
    CHAR *recipient_address,
    UINT priority, CHAR *subject,
    CHAR *mail_body,
    UINT mail_body_length);
```

### <a name="description"></a><span data-ttu-id="cada8-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cada8-151">Description</span></span>

<span data-ttu-id="cada8-152">Bu hizmet bir SMTP posta öğesi oluşturur ve gönderir.</span><span class="sxs-lookup"><span data-stu-id="cada8-152">This service creates and sends an SMTP mail item.</span></span> <span data-ttu-id="cada8-153">SMTP Istemcisi SMTP sunucusuyla bir TCP bağlantısı kurar ve bir dizi SMTP komutu gönderir.</span><span class="sxs-lookup"><span data-stu-id="cada8-153">The SMTP Client establishes a TCP connection with the SMTP Server and sends a series of SMTP commands.</span></span> <span data-ttu-id="cada8-154">Herhangi bir hatayla karşılaşılmaz, posta iletisini sunucuya iletir.</span><span class="sxs-lookup"><span data-stu-id="cada8-154">If no errors are encountered, it will transmit the mail message to the Server.</span></span> <span data-ttu-id="cada8-155">Posta başarıyla gönderiliyorsa bağımsız olarak TCP bağlantısını sonlandırır ve posta aktarımının sonucunu gösteren bir durum döndürür.</span><span class="sxs-lookup"><span data-stu-id="cada8-155">Regardless if the mail is sent successfully it will terminate the TCP connection and return a status indicating outcome of the mail transmission.</span></span> <span data-ttu-id="cada8-156">Uygulama, sınır olmadan gönderilmesi gereken çok sayıda posta iletisi için bu hizmeti çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="cada8-156">The application may call this service for as many mail messages as it needs to send without limit.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="cada8-157">Giriş Parametreleri</span><span class="sxs-lookup"><span data-stu-id="cada8-157">Input Parameters</span></span>

- <span data-ttu-id="cada8-158">**client_ptr** SMTP Istemcisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="cada8-158">**client_ptr** Pointer to SMTP Client</span></span>
- <span data-ttu-id="cada8-159">**recipient_address** NULL ile sonlandırılmış alıcı adresi.</span><span class="sxs-lookup"><span data-stu-id="cada8-159">**recipient_address** NULL-terminated recipient address.</span></span>
- <span data-ttu-id="cada8-160">**Konu** NULL ile sonlandırılmış konu satırı metni;.</span><span class="sxs-lookup"><span data-stu-id="cada8-160">**subject** NULL-terminated subject line text;.</span></span>
- <span data-ttu-id="cada8-161">**Öncelik** Postanın teslim edileceği öncelik düzeyi</span><span class="sxs-lookup"><span data-stu-id="cada8-161">**priority** Priority level at which mail is delivered</span></span>
- <span data-ttu-id="cada8-162">**mail_body** Posta iletisi işaretçisi</span><span class="sxs-lookup"><span data-stu-id="cada8-162">**mail_body** Pointer to mail message</span></span>
- <span data-ttu-id="cada8-163">**mail_body_length** Posta iletisinin boyutu</span><span class="sxs-lookup"><span data-stu-id="cada8-163">**mail_body_length** Size of mail message</span></span>

### <a name="return-values"></a><span data-ttu-id="cada8-164">Dönüş Değerleri</span><span class="sxs-lookup"><span data-stu-id="cada8-164">Return Values</span></span>

- <span data-ttu-id="cada8-165">**NX_SUCCESS** (0x00) posta başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="cada8-165">**NX_SUCCESS** (0x00) Mail successfully sent</span></span>
- <span data-ttu-id="cada8-166">SMTP oturumunun SMTP oturumu durumu sonucu için **NX_SMTP_CLIENT_NOT_INITIALIZED** (0xB2) SMTP istemci örneği başlatılmadı</span><span class="sxs-lookup"><span data-stu-id="cada8-166">**NX_SMTP_CLIENT_NOT_INITIALIZED** (0xB2) SMTP Client instance not initialized for SMTP session status Outcome of SMTP session</span></span>
- <span data-ttu-id="cada8-167">NX_PTR_ERROR (0x07) geçersiz işaretçi parametresi</span><span class="sxs-lookup"><span data-stu-id="cada8-167">NX_PTR_ERROR (0x07) Invalid pointer parameter</span></span>
- <span data-ttu-id="cada8-168">NX_SMTP_INVALID_PARAM (0xA5) geçersiz işaretçi girişi</span><span class="sxs-lookup"><span data-stu-id="cada8-168">NX_SMTP_INVALID_PARAM (0xA5) Invalid non pointer input</span></span>
- <span data-ttu-id="cada8-169">NX_CALLER_ERROR (0x11) Bu hizmet için geçersiz çağrı</span><span class="sxs-lookup"><span data-stu-id="cada8-169">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="cada8-170">İzin verilen</span><span class="sxs-lookup"><span data-stu-id="cada8-170">Allowed From</span></span>

<span data-ttu-id="cada8-171">İş Parçacıkları</span><span class="sxs-lookup"><span data-stu-id="cada8-171">Threads</span></span>

### <a name="example"></a><span data-ttu-id="cada8-172">Örnek</span><span class="sxs-lookup"><span data-stu-id="cada8-172">Example</span></span>

```C
/* Create and send a Client mail item. */

#define RECIPIENT_ADDRESS “<your@yourcompany.com>”
#define SUBJECT “NetX Duo SMTP Client Demo”
#define MAIL_BODY "NetX Duo SMTP client is an SMTP client ” \
    “implementation for embedded devices \r\n” \
    "to send email to SMTP servers.\r\n"

status = nx_smtp_mail_send(&demo_client, RECIPIENT_ADDRESS,
    NX_SMTP_MAIL_PRIORITY_NORMAL,
    SUBJECT_LINE, MAIL_BODY,
    sizeof(MAIL_BODY) - 1);

/* Return status being NX_SUCCESS indicates the mail has been
    successfully sent. */
```
